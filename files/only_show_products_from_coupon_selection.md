# Show products only from the coupon selection
This code snippet will show products only from the coupon selection. If the customer has not selected a coupon, they will get a message that they have to use a coupon to see the products associated with that code. If the customer has selected a coupon, they will only see products that are associated with that coupon. The products are associated with the coupon by selecting a product category in the coupon settings.

```php
//show products only from the coupon selection
add_action('pre_get_posts', function ($q) { //because pre get posts works better than woocommerce_product_query
    $applied_coupons = WC()->cart->get_applied_coupons();
    if (empty($applied_coupons)) {
        $q->set('post__in', array(0));
    } else {
        $coupon_code = $applied_coupons[0];
        $coupon = new WC_Coupon($coupon_code);
        $product_categories = $coupon->get_product_categories();

        if (!empty($product_categories)) {
            $tax_query = $q->get('tax_query');
            $tax_query[] = array(
                'taxonomy' => 'product_cat',
                'field'    => 'term_id',
                'terms'    => $product_categories,
                'operator' => 'IN'
            );
            $q->set('tax_query', $tax_query);
        }
        else{
            $q->set('post__in', array(0));
        }
    }
}, 10);

//add a notice if no coupon is used
add_action('woocommerce_no_products_found', function() {
    if (empty(WC()->cart->get_applied_coupons())) {
        wc_print_notice(esc_attr__('You have to use a coupon to see the products assoiated with that code.'), 'error');
    }
});

//before content to show the coupon form
add_action('woocommerce_before_main_content', function(){
    if (empty(WC()->cart->get_applied_coupons())) {
        // reigster the form js and css
        wp_enqueue_script('wc-checkout');
        wp_enqueue_style('wc-checkout');
        wc_get_template('checkout/form-coupon.php', array('checkout' => WC()->checkout()));
    }
    else{
        $set_coupon = WC()->cart->get_applied_coupons();
        echo "<div class='woocommerce-info'>You have used the coupon code: $set_coupon[0]</div>";

    }
});

```