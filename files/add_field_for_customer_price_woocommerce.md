# Add a field for customer price in WooCommerce

This code example adds a custom field for the customer's own price on the product page. The custom price is added to the cart and displayed on the checkout page. The custom price is also used in the calculation of the total price.

```php
// Show the custom price field on the product page
add_action(
    'woocommerce_before_add_to_cart_button',
    function () {
        echo '<div class="custom-price">';
        echo '<label for="custom_price">' . __('Enter Your Price:', 'woocommerce') . '</label>';
        echo '<input type="number" step="any" min="0" name="custom_price" id="custom_price" value="' . esc_attr(isset($_POST['custom_price']) ? $_POST['custom_price'] : '') . '" />';
        echo '</div>';
    },
    20
);

// Add the custom price to the cart item
add_filter('woocommerce_add_cart_item_data', function ($cart_item_data, $product_id, $variation_id) {
    if (isset($_POST['custom_price'])) {
        $cart_item_data['custom_price'] = wc_clean($_POST['custom_price']);
    }
    return $cart_item_data;
}, 10, 3);

// Show the custom price in the cart
add_filter('woocommerce_get_item_data', function ($item_data, $cart_item) {
    if (isset($cart_item['custom_price'])) {
        $item_data[] = array(
            'key'     => __('Your Price', 'woocommerce'),
            'value'   => wc_price($cart_item['custom_price'])
        );
    }
    return $item_data;
}, 10, 2);

// Show the custom price in the checkout
add_action('woocommerce_before_calculate_totals', function ($cart_object) {
    foreach ($cart_object->get_cart() as $cart_item_key => $cart_item) {
        if (isset($cart_item['custom_price'])) {
            $cart_item['data']->set_price($cart_item['custom_price']);
        }
    }
}, 10, 1);
```