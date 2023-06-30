#Add metadata fields to WordPress search

This is for adding metadata to the wordpress search.  This is useful for custom post types and custom fields.

<code>
// Add metadata to WordPress search
function add_metadata_to_search($search, $wp_query) {
    global $wpdb;

    // Check if this is a search query
    if (!is_admin() && $wp_query->is_search) {
        $search_terms = $wp_query->query_vars['s'];
        
        // Append additional search conditions based on metadata
        // Modify this section to add your custom metadata conditions
        $search .= $wpdb->prepare("
            OR (
                {$wpdb->posts}.post_title LIKE %s
                OR {$wpdb->posts}.post_content LIKE %s
                OR EXISTS (
                    SELECT * FROM {$wpdb->postmeta}
                    WHERE post_id = {$wpdb->posts}.ID
                    AND meta_value LIKE %s
                )
            )",
            '%' . $wpdb->esc_like($search_terms) . '%',
            '%' . $wpdb->esc_like($search_terms) . '%',
            '%' . $wpdb->esc_like($search_terms) . '%'
        );
    }

    return $search;
}
add_filter('posts_search', 'add_metadata_to_search', 10, 2);
</code>