# Use an Elementor template as a footer

Add a template, or a section under the Elementor library. In this example, the template is called "snillrik-footer".  This is the nicename of the template.

```php
// Add metadata to WordPress search
add_filter('wp_footer', function ($html) {
	if (class_exists('\Elementor\Plugin')) { //check if Elementor is active
		
        $html_out = '';
		$args = array(
			'name' => 'snillrik-footer', //this is the nicename of the template
			'post_type' => 'elementor_library',
			'post_status' => 'publish'
		);
		
        $template = new WP_Query($args);

		if ($template->have_posts()) {
			while ($template->have_posts()) {
				$template->the_post();
				$html_out .= \Elementor\Plugin::$instance->frontend->get_builder_content(get_the_ID(), true); // get the template, true is if preview
			}
		}

		wp_reset_postdata();
		echo $html_out;

	}
});
```