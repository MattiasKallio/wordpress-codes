# Custom Login Logo
This code will replace the default WordPress logo with your own logo. Add the following code to your theme's functions.php file.

```php
add_action('login_head', function()
{
    $logo_url = 'urltologo.. ../logo.png';
    echo '<style type="text/css">' .
        'h1 a { 
				background-image:url(' . $logo_url . ') !important;
				background-size:100% !important;
                width:265px !important;
                height:184px !important;
				line-height:inherit !important;
				}' .
        '</style>';
});
```