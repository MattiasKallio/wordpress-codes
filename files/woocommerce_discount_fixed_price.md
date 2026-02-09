# WooCommerce - Fixed Product Price Coupon

To add a new coupon type "fixed_product_price" that sets a fixed price on products in the cart. It's not a discount but a price override. The code also hides the coupon line in the cart totals if the discount amount is $0, and instead shows the fixed price applied by the coupon.

```php
add_filter('woocommerce_coupon_discount_types', function ($types) {
    $types['fixed_product_price'] = __('Fixed price', 'textdomain');
    return $types;
});
add_action('woocommerce_before_calculate_totals', function ($cart) {

    if (is_admin() && !defined('DOING_AJAX')) return;

    foreach ($cart->get_applied_coupons() as $coupon_code) {

        $coupon = new WC_Coupon($coupon_code);

        if ($coupon->get_discount_type() !== 'fixed_product_price') {
            continue;
        }

        $fixed_price = (float) $coupon->get_amount();
        $allowed_products = $coupon->get_product_ids();

        foreach ($cart->get_cart() as $item) {

            // If products are selected in the coupon
            if (!empty($allowed_products) &&
                !in_array($item['product_id'], $allowed_products)) {
                continue;
            }

            $item['data']->set_price($fixed_price);
        }
    }
});

// Hide coupon line in the cart totals when the discount is $0
add_filter('woocommerce_cart_totals_coupon_html', function ($coupon_html, $coupon, $discount_amount_html) {
    if ($coupon->get_discount_type() === 'fixed_product_price' && $coupon->get_amount() > 0) {
        $price = $coupon->get_amount();
        return 'Fixed price ' . wc_price($price); // Return empty string to hide the line
    }
    return $coupon_html;
}, 10, 3);
```