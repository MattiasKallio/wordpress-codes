# Block products per country in WooCommerce
This code snippet will block products from being bought in a specific country. In this example, the product with the ID 11012 can only be bought in Sweden. If the customer tries to buy the product from another country, they will be redirected to the cart page with an error message. 

```php
//Bara köpa vanligt medlemskap i sverige. 
add_action('woocommerce_check_cart_items', function () {
    $products = [11012];

    // Get customer country
    $country = WC()->session->get('customer')['shipping_country'];
    if (empty($country)) {
        $country = WC()->session->get('customer')['billing_country'];
    }
    // Not for SE
    if ($country != 'SE') {
        // Loop through cart items
        foreach (WC()->cart->get_cart() as $item) {
            // IF product is in cart
            if (in_array($item['product_id'], $products)) {
                $product_name = $item['data']->get_name();
                if (is_checkout()) {
                    wp_safe_redirect(wc_get_cart_url());
                } else {
                    wc_add_notice(sprintf('Det verkar som du har produkten %s i kundkorgen Den kan tyvärr bara köpas i Sverige.', $product_name), 'error');
                }

                break; // Stop the loop
            }
        }
    }
}, 1);
```