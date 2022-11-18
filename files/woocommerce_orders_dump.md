#Export Orders to XML

Dumping orders to XML-file that is importable by the plugin [Order Export Import XML](https://sv.wordpress.org/plugins/order-xml-file-export-import-for-woocommerce/)

I just run it with a shortcode, because I like to just reload a page and have it run once... But there are other ways to do it. ;)

<code>
add_shortcode('dump_woocommerce_orders', 'dump_woocommerce_orders');

function dump_woocommerce_orders() {
    //get all orders
    $orders = wc_get_orders(array(
        'limit' => 30,
        'orderby' => 'date',
        'order' => 'DESC'
    ));

    $xml_out = '';

    $items_match_array = array(
        "SKU" => "product_id",
        "Name" => "product_id",
        "Quantity" => "quantity",
        "Price" => "subtotal",
        "Total" => "total",
    );

    $order_match_array = array(
        "OrderId" => "id",
        "OrderNumber" => "id",
        "OrderDate" => "date_created",
        "OrderStatus" => "status",
        "OrderTotal" => "total",
        "OrderSubtotal" => "subtotal",
        "OrderShipping" => "shipping_total",
        "OrderTax" => "total_tax",
        "OrderDiscount" => "discount_total",
        "OrderPaymentMethod" => "payment_method",
        "OrderPaymentMethodTitle" => "payment_method_title",
        "TaxTotal"      => "total_tax",
        "PaymentMethodId" => "payment_method",
        "PaymentMethod" => "payment_method_title",
        "CustomerNotes" => "customer_note",
        "CustomerId" => "customer_id",
        "Currency" => "currency",
        "CompletedDate" => "date_completed",
    );

    $billing_match_array = array(
        "BillingFirstName" => "first_name",
        "BillingLastName" => "last_name",
        "BillingFullName"   => "first_name",
        "BillingCompany" => "company",
        "BillingAddress1" => "address_1",
        "BillingAddress2" => "address_2",
        "BillingCity" => "city",
        "BillingState" => "state",
        "BillingPostcode" => "postcode",
        "BillingCountry" => "country",
        "BillingEmail" => "email",
        "BillingPhone" => "phone",
    );
    $shipping_match_array = array(
        "ShippingFirstName" => "first_name",
        "ShippingLastName" => "last_name",
        "ShippingFullName"   => "first_name",
        "ShippingCompany" => "company",
        "ShippingAddress1" => "address_1",
        "ShippingAddress2" => "address_2",
        "ShippingCity" => "city",
        "ShippingState" => "state",
        "ShippingPostcode" => "postcode",
        "ShippingCountry" => "country",
        "ShippingEmail" => "email",
        "ShippingPhone" => "phone",
        "ShippingMethod" => "method_title",
        "ShippingMethodID" => "method_id",
        "ShippingCost" => "total",
        "ShippingTaxTotal" => "total_tax",
        "ShippingTotal" => "shipping_total"
    );

    //loop through orders
    foreach ($orders as $order) {
        //get order data
        $order_data = $order->get_data();
        //error_log(print_r($order_data, true));
        //get items in order
        $items = $order->get_items();
        $item_rows = "";

        $order_xml_out = "";

        //loop through items
        foreach ($items as $item) {
            //get item data
            $item_data = $item->get_data();
            //error_log("item: ".print_r($item_data, true));
            $item_rows = "<OrderLineItems>\n";
            foreach ($items_match_array as $key => $value) {
                if (isset($item_data[$value]))
                    $item_rows .= "\t<$key>" . $item_data[$value] . "</$key>\n";
            }
            $item_rows .= "</OrderLineItems>\n";
        }

        foreach ($order_match_array as $key => $value) {
            if (isset($order_data[$value])) {
                if ($value == "date_created") {
                    $order_xml_out .= "<$key>" . date("Y-m-d H:i:s", strtotime($order_data[$value])) . "</$key>\n";
                } else {
                    $order_xml_out .= "<$key>" . $order_data[$value] . "</$key>\n";
                }
            }
        }

        foreach ($billing_match_array as $key => $value) {
            if (isset($order_data['billing'][$value]))
                $order_xml_out .= "<$key>" . $order_data['billing'][$value] . "</$key>\n";
        }

        foreach ($shipping_match_array as $key => $value) {
            if (isset($order_data['shipping'][$value]))
                $order_xml_out .= "<$key>" . $order_data['shipping'][$value] . "</$key>\n";
        }

        // $date_created = $order_data["date_created"]->date("Y-m-d H:i:s");

        $xml_out .= "<Order>\n$order_xml_out\n$item_rows\n</Order>\n";
    }
    $full_xml = '<?xml version="1.0" encoding="UTF-8" standalone="no"?>
    <Orders>\n' . $xml_out . '\n</Orders>';

    //save as xml
    $file = fopen("orders.xml", "w");
    fwrite($file, $full_xml);
    fclose($file);
    return $full_xml;
}
</code>