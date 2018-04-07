---
id: 23
title: Adding Tags Taxonomy To WordPress Comments
date: 2016-06-13T05:57:40+00:00
author: Shah
layout: post
guid: http://hameid.net/2016/06/13/adding-tags-taxonomy-to-wordpress-comments/
permalink: /adding-tags-taxonomy-to-wordpress-comments/
categories:
  - Programming
tags:
  - Code Snippet
  - PHP
  - Programming
  - Wordpress
---
In some edge cases, You may want to add tags or other taxonomies to comments of your WordPress website. Adding taxonomy to comments is not natively supported in WordPress. But that doesn't mean you cannot do it. 

You can probably create a new Custom Post Type for comments and replace the comment forms, the logic and everything related to comments. It requires a higher level of effort and more number of work-hours to do that though.

The another way to add taxonomy terms to a comment is to use comment meta to store and retrieve the taxonomy terms for every comment. Using comment meta to store taxonomy terms of comments can save you a lot of time. And the core logic of comments is maintained as is. 

Let me show you how to add taxonomy terms to WordPress comments.

### Adding Tags To WordPress Comments {#addingtagstowordpresscomments}

First of all, You have to add a field to the comment form using which the user can select the tags. You can hook into `comment_form_defaults` filter and add a field.

Place the following code in your theme's `functions.php` file. This will add a `Select` field with all the tags populated to the comment form.

<pre><code class="language-prettyprint lang-php">add_filter( 'comment_form_defaults', 'change_comment_form_defaults');  
function change_comment_form_defaults( $default ) {  
    $commenter = wp_get_current_commenter();
    $out = '&lt;label for="comment_tags"&gt;Tags:&lt;/label&gt;';
    $out .= '&lt;select name="comment_tags" multiple&gt;';
    foreach ( get_tags() as $tag ) {
        $out .= '&lt;option value="&lt;?php echo $tag-&gt;term_id; ?&gt;"&gt;&lt;?php echo $tag-&gt;name; ?&gt;&lt;/option&gt;';
    }
    $out .= '&lt;/select&gt;';
    $default[ 'comment_field' ] .= $out;
    return $default;
}
</code></pre>

Now whenever a comment is inserted, The tags selected should be saved as metadata. The action `comment_post` is triggered immediately after a comment is inserted into the database. We can use it to update the metadata of the comment to include tags. 

<pre><code class="language-prettyprint lang-php">add_action('comment_post', 'add_tags_to_comment', 10, 2);  
function add_tags_to_comment( $comment_ID, $comment_approved ) {  
    foreach($_POST["comment_tags"] as $comment_tag) {
        add_comment_meta( $comment_ID, "comment_tag", $comment_tag );
    }
}
</code></pre>

The above code should also go in your theme's **functions.php** file.

Do note that Instead of storing all the terms as an array in a single record, I prefer to store each term as an individual record. That will make it easier when you have to search the comments by tags.

### Displaying Tags Of A Comment {#displayingtagsofacomment}

To display the tags of a comment, You can simply use `get_comment_meta` function to retrieve all the tags of a particular comment. Here is a raw code on how to do it.

<pre><code class="language-prettyprint lang-php">$tags = get_comment_meta($comment_ID, "comment_tag");
echo "&lt;ul&gt;";  
foreach($tags as $tag_id) {  
    $tag_term = get_term($tag_id, 'post_tag');
    echo "&lt;li&gt;" . $tag_term-&gt;name . "&lt;/li&gt;";
}
echo "&lt;/ul&gt;";  
</code></pre>

Place the code in the place where you want to display the tags. Make sure `$comment_ID` variable contains the correct ID of the comment. 

### Searching Comments Based On Tags {#searchingcommentsbasedontags}

When you want to search comments based on tags, you can use `WP_Comment_Query` class to do so. Below is a sample code to search comments based on tags. 

<pre><code class="language-prettyprint lang-php">$tags = array(1,32,5,4); /* Replace it with tags you want to search */
$args = array(
    'meta_query' =&gt; array(
        array(
            'key' =&gt; 'comment_tag',
            'value' =&gt; $tags,
            'compare' =&gt; 'IN'
        )
    )
 );
$comments_query = new WP_Comment_Query( $args );
$comments = $comments_query-&gt;query();
</code></pre>

The `$comments` variable will contain an array of the comments associated with the tags. You can loop through it to display the comments. 

* * *

Was the post helpful? Have a query? Or Know a better approach? Let me know in the comments, I'll be glad to hear.