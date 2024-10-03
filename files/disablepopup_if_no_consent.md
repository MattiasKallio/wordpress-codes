
# Disable popup if no consent from CookieYes
In WordPress Popupbuider, you can use the following code to disable the popup if the user has not given consent to cookies.  This is useful if you want to show a cookie consent popup before showing other popups.

```javascript

let cookieyesset = getCookie("cookieyes-consent");

if(cookieyesset.indexOf('consent:yes') !== -1){
    return true;
}
return false;

```

Not for the popup, but fitted here anyway because it's a cookieyes thing... 
Add a text after the add to cart button if the user has not given consent to cookies. In some themes you just get an error when trying to add to cart if you have not given consent to cookies. This is a way to inform the user about this.
    
```php
    add_action('woocommerce_after_add_to_cart_button', function () {
	//<!--consentid:jadajadakoodmobillii,consent:yes,action:yes,necessary:yes,functional:yes,analytics:yes,performance:yes,advertisement:yes,other:yes-->
    $cookie_yes = isset($_COOKIE['cookieyes-consent']) ? $_COOKIE['cookieyes-consent'] : '';
    if (strpos($cookie_yes, 'consent:yes') == false && strpos($cookie_yes, 'functional:yes') == false) {
        echo "<br /><span class='kak-product-cookie-info'>You might need functional cookies for this ajax thingimabob to work as intended</span>";
    }
}, 10, 0);
```