# Show products only from the coupon selection
This code snippet will show products only from the coupon selection. If the customer has not selected a coupon, they will get a message that they have to use a coupon to see the products associated with that code. If the customer has selected a coupon, they will only see products that are associated with that coupon. The products are associated with the coupon by selecting a product category in the coupon settings.

```php
add_action('woocommerce_product_query', function ($q) {
    $applied_coupons = WC()->cart->get_applied_coupons();
    if (empty($applied_coupons)) {
        $q->set('post__in', array(0));
    } else {
        $coupon_code = $applied_coupons[0];
        $coupon = new WC_Coupon($coupon_code);
        $product_categories = $coupon->get_product_categories();

        if (!empty($product_categories)) {
            $q->set('tax_query', array(
                array(
                    'taxonomy' => 'product_cat',
                    'field'    => 'term_id',
                    'terms'    => $product_categories,
                )
            ));
        }
    }
}, 10, 1);

add_action('woocommerce_no_products_found', 'custom_no_products_message');

function custom_no_products_message() {
    if (empty(WC()->cart->get_applied_coupons())) {
        wc_print_notice(esc_attr__('You have to use a coupon to see the products assoiated with that code.'), 'error');
    }
}
```