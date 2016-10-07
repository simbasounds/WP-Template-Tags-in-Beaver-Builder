# WP-Template-Tags-in-Beaver-Builder
A short snippet to demonstrate how to get your WordPress post and CPT content into Beaver Builder layout templates.


##The problem
If you programmatically assign a Beaver Builder template to a post, the most obvious way of fetching and outputting WordPress content within modules is via a shortcode.

But the template has to set up its own query which tends to break shortcodes. This is because the shortcode is unable to access the original post's ID via the normal methods.


##The solution
You can literally just access the global $post variable to utilise the original ID of the current post:
```php
global $post;
$post_id = $post->ID;
```

##Example usage
Here’s a shortcode which outputs the featured image: [bbtt-thumb]

The code to add to functions.php which creates the shortcode is:
```php
function bbtt_thumb() {
  ob_start();
 
  global $post;
  $post_id = $post->ID;
  the_post_thumbnail($post_id);
 
  return ob_get_clean();
}
add_shortcode( 'bbtt-thumb', 'bbtt_thumb' );
```

Note the ob_start(); and ob_get_clean();
They buffer the content so it is output in the right place on the page.

You can create further shortcodes for your content by referencing [the codex page](https://codex.wordpress.org/Template_Tags).
