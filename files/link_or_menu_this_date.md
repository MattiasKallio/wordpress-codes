# Link or menu to this date
If you want a shortcode or a menu item that links to the current date, this is how you do it.
You can just skip the manad array if you're not interested in the month name in swedish.
The links in the examples are like 24-december and assumes you have a page for each day of the year.

```php
add_shortcode('dagens_datum', function () {
     $manad = [
        "januari", "februari", "mars", "april", "maj", "juni",
        "juli", "augusti", "september", "oktober", "november", "december"
    ];

    $dag = date("j");
    $manad = $manad[date("n") - 1];
    $link_with_date = get_home_url() . "/" .$dag . "-" . strtolower($manad);   

    return "<a href='$link_with_date'>$dag $manad</a>";
});

add_filter('wp_nav_menu_objects', function ($items, $args) {
    foreach ($items as $item) {
        if (strpos($item->url, 'datumlank') !== false) {
            $manad = [
                "januari", "februari", "mars", "april", "maj", "juni",
                "juli", "augusti", "september", "oktober", "november", "december"
            ];
        
            $dag = date("j");
            $manad = $manad[date("n") - 1];
            $link_with_date = get_home_url() . "/" .$dag . "-" . strtolower($manad);   
            $item->url = $link_with_date;
        }
    }
    return $items;
}, 10, 2);
```