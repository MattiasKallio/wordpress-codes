
# Disable popup if no consent from CookieYes
In WordPress Popupbuider, you can use the following code to disable the popup if the user has not given consent to cookies.  This is useful if you want to show a cookie consent popup before showing other popups.

```javascript

let cookieyesset = getCookie("cookieyes-consent");

if(cookieyesset.indexOf('consent:yes') !== -1){
    return true;
}
return false;
