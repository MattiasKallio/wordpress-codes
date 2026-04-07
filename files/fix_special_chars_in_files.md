# Fix special characters in file names in uploads
This code will replace special characters in file names in the uploads folder with their ASCII equivalents. This is useful if you have files with special characters in their names that are not displaying correctly on the website. The code will run once and then mark itself as done using an option in the database, so it won't run again on every page load.


```php
add_action('init', function() {
	if (get_option('uploads_filenames_fixed_pages')) {
		return; // Har redan körts, gör inget
	}

	// Get both posts and pages
	$posts = get_posts([
		'posts_per_page' => -1,
		'post_type' => ['page'] // Added pages to the query
	]);
	
	foreach ($posts as $post) {
		$content = $post->post_content;
		$new_content = preg_replace_callback(
			'#uploads/([^"\']+)#',
			function($matches) {
				$filename = $matches[1];
				$fixed = str_replace(
					['Å', 'Ä', 'Ö', 'å', 'ä', 'ö'],
					['A', 'A', 'O', 'a', 'a', 'o'],
					$filename
				);
				error_log("Fixing filename: $filename to $fixed");
				return 'uploads/' . $fixed;
			},
			$content
		);
		
		if ($new_content !== $content) {
			wp_update_post(['ID' => $post->ID, 'post_content' => $new_content]);
		}
	}

	update_option('uploads_filenames_fixed_pages', 1); // Markera som klar
});
```