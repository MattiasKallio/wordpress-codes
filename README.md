# wordpress-codes
Some nifty wordpress-codes like filters, functions, shortcodes etc.

Just a bunch of things that I use from time to time or things that took a while to figure out and might be usefull for others. :)

Everything is placed under /files and should be named to understand what i does and have a description too.

## [Export Orders to XML](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/woocommerce_orders_dump.md)
To export orders from Woocommerce to import with some plugin, I use Order Export Import XML

##  [Use an Elementor template as a footer](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/add_elementor_template_as_footer.md)
Add a template, or a section under the Elementor library. In this example, the template is called "snillrik-footer".  This is the nicename of the template.

## [Add metadata fields to WordPress search](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/add_metadata_to_search.md)
This is for adding metadata to the wordpress search.  This is useful for custom post types and custom fields.

## [Hide thumbnail image on single post](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/hide_thumbnail_image.md)
If you want to add a checkbox to hide the thumbnail image on a single post, but still show it on list pages, archive pages etc.  This is how you do it.

## [Replace part of text in postmeta](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/SQL_replace_part.md)
I just need to remember this SQL query to replace part of a text in a postmeta field. The "where" key is important, otherwise you will replace all the text in all the postmeta fields.

## [Custom login logotype](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/custom_login_logo.md)
This code will replace the default WordPress logo with your own logo. Add the following code to your theme's functions.php file.

## [Disable popup if no consent from CookieYes](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/disablepopup_if_no_consent.md)
In WordPress Popupbuider, you can use the following code to disable the popup if the user has not given consent to cookies.  This is useful if you want to show a cookie consent popup before showing other popups.

## [Add a custom field for customer price in WooCommerce](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/add_field_for_customer_price_woocommerce.md)
This code example adds a custom field for the customer's own price on the product page. The custom price is added to the cart and displayed on the checkout page. The custom price is also used in the calculation of the total price.

## [Add export data to User Insights](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/add_export_data_to_userinsights.md)
If you want to add custom data to the User Insights plugin, you can use the following code snippet. This code adds a custom field to the User Insights plugin and populates it with data from the BuddyPress avatar or the WordPress avatar if it is not a Gravatar.

## [Block products per country in woocommerce checkout](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/block_products_per_country.md)
This code snippet will block products from being bought in a specific country. In this example, the product with the ID 11012 can only be bought in Sweden. If the customer tries to buy the product from another country, they will be redirected to the cart page with an error message.