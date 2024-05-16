# Add information for local pickup shipping method

```php
// Fin the selected shipping method and add a message to the cart and checkout page
add_action( 'woocommerce_after_shipping_rate',
function( $method, $index )
{
    if( 'local_pickup' === $method->method_id )
    {
        $picked_methods = WC()->session->get( 'chosen_shipping_methods' );
        $picked_method = reset( $picked_methods );
        if( strpos( $picked_method, 'local_pickup' ) !== false && is_cart() )
        {
            echo '<br><span class="pickup-warning-cart">We´ll contact you when you can pick up your stuff</span>';
        }   
    }
}, 20, 2 );

//add field after woocommerce-shipping-totals because some payment gateways dont pickup above hook.
add_action( 'woocommerce_review_order_after_shipping', function() {
    $picked_methods = WC()->session->get( 'chosen_shipping_methods' );
    $picked_method = reset( $picked_methods );
    if( strpos( $picked_method, 'local_pickup' ) !== false )
    {
    echo '<tr class="pickup-warning"><td colspan="2">We´ll contact you when you can pick up your stuff</td></tr>';
    }
} );
```