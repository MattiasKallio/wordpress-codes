# Hide thumbnail image on single post
If you want to add a checkbox to hide the thumbnail image on a single post, but still show it on list pages, archive pages etc.  This is how you do it.

###Add this to your functions.php file  (or where you put your custom functions)

```php
//add admin meta box with checkbox for not showing image on single post
add_action('add_meta_boxes', function () {
    add_meta_box('snillrik_hide_image', 'Dölj bild på enskild sida', function ($post) {
        $value = get_post_meta($post->ID, 'snillrik_hide_image', true);
        $checked = $value == "true" ? "checked" : "";
        echo "<p>För att dölja bilden på inläggets sida, den kommer fortfarande synas på list-sidor och arkiv-sidor etc.</p><input type='checkbox' name='snillrik_hide_image' value='true' $checked>";
    }, 'post', 'side', 'low');
});

//save the checkbox value
add_action('save_post', function ($post_id) {
    if (array_key_exists('snillrik_hide_image', $_POST)) {
        update_post_meta(
            $post_id,
            'snillrik_hide_image',
            $_POST['snillrik_hide_image']
        );
    }
    //else remove it
    else {
        delete_post_meta($post_id, 'snillrik_hide_image');
    }
});

//if is sigle, and checkbox is checked, filter has_post_thumbnail
add_filter('has_post_thumbnail', function ($has_thumbnail, $post_id) {
    $snillrik_hide_image = get_post_meta($post_id, 'snillrik_hide_image', true);
    //error_log("has_post_thumbnail $snillrik_hide_image");
    if (is_singular("post") && is_main_query() && ($snillrik_hide_image == "true" || $snillrik_hide_image == true)) {
        return false;
    }
    return $has_thumbnail;
}, 10, 2);
```

###Put somthing like this in you single.php file or where you want to hide the thumbnail image.

```php
	<?php if ( has_post_thumbnail(get_the_ID()) ) : ?>
		<div class="post-thumbnail">
			<?php the_post_thumbnail(); ?>
		</div>
	<?php endif; ?>
```