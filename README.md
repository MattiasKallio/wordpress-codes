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

## [Add text after add to cart if no consent from CookieYes](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/disablepopup_if_no_consent.md)
Add a text after the add to cart button if the user has not given consent to cookies. In some themes you just get an error when trying to add to cart if you have not given consent to cookies. This is a way to inform the user about this.

## [Add a custom field for customer price in WooCommerce](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/add_field_for_customer_price_woocommerce.md)
This code example adds a custom field for the customer's own price on the product page. The custom price is added to the cart and displayed on the checkout page. The custom price is also used in the calculation of the total price.

## [Add export data to User Insights](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/add_export_data_to_userinsights.md)
If you want to add custom data to the User Insights plugin, you can use the following code snippet. This code adds a custom field to the User Insights plugin and populates it with data from the BuddyPress avatar or the WordPress avatar if it is not a Gravatar.

## [Block products per country in woocommerce checkout](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/block_products_per_country.md)
This code snippet will block products from being bought in a specific country. In this example, the product with the ID 11012 can only be bought in Sweden. If the customer tries to buy the product from another country, they will be redirected to the cart page with an error message.

## [Link or menu to this date](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/link_or_menu_this_date.md)
If you want a shortcode or a menu item that links to the current date, this is how you do it. You can just skip the manad array if you're not interested in the month name in swedish. The links in the examples are like 24-december and assumes you have a page for each day of the year.

## [Show products only from the coupon selection](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/only_show_products_from_coupon_selection.md)
### OK, still working on this, sort of working, but it's not perfect yet.
This code snippet will show products only from the coupon selection. If the customer has not selected a coupon, they will get a message that they have to use a coupon to see the products associated with that code. If the customer has selected a coupon, they will only see products that are associated with that coupon. The products are associated with the coupon by selecting a product category in the coupon settings.

## [Contact Form 7 - Temp disable button](https://github.com/MattiasKallio/wordpress-codes/blob/main/files/contact_form_7_temp_disable_button.md)
This code will disable the submit button for 5 seconds when the form is submitted. This is to prevent multiple submissions of the form. The submit button will be disabled and the text will change to "Sending..." for 5 seconds. After 5 seconds, the submit button will be enabled again and the text will change back to "Send".