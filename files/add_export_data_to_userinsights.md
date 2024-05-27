# Add export data to User Insights

If you want to add custom data to the User Insights plugin, you can use the following code snippet. This code adds a custom field to the User Insights plugin and populates it with data from the BuddyPress avatar or the WordPress avatar if it is not a Gravatar.

```php

//Adding field to users-insights
add_filter('usin_fields', function ($fields) {

        $fields[] = [
            'name' => 'Travatar',
            'id' => 'travatar',
            'order' => 10,
            'show' => 1,
            'fieldType' => 'general',
            'filter' => [
                'type' => 'text',
                'disallow_null' => 1,
            ]

        ];

        return $fields;
    },
    1000
);

//Adding field data to users-insights
add_filter('usin_users_raw_data', function ($data) {
    foreach ($data as $key => $user) {
        $user_id = $user->ID;

        $bp_avatar = bp_core_fetch_avatar(array('item_id' => $user_id, 'html' => false, 'type' => 'full'));
        
        //if not gravatar
        if (strpos($bp_avatar, "gravatar") !== false) {
            $bp_avatar = BP_XProfile_ProfileData::get_value_byid(2, $user_id);
            $uploads_dir = wp_upload_dir();
            $bp_avatar = $uploads_dir['baseurl'] . "/" . $bp_avatar;
        }
        if($bp_avatar !== "http://localhost/wptrasher/wp-content/uploads/") //ie no filename
            $data[$key]->travatar = $bp_avatar;
    }

    return $data;
}, 10, 1);

```