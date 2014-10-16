Coda2-WordPress-Clip
====================

Coda2用のWordPressクリップ

## Usage

```
git clone https://github.com/gatespace/Coda2-WordPress-Clip.git
```

`WordPress.clips` Double click.

## Clips

### WordPress Modify main query(pre_get_posts actiob hook)

type : `pre_get_posts￼￼ + [TAB]`

```
<?php
/**
 * pre_get_posts を使ってメインクエリーを書き換える
 * http://notnil-creative.com/blog/archives/1996
 */

add_action( 'pre_get_posts', 'foo_modify_main_query' );
function foo_modify_main_query( $query ) {
	if ( is_admin() || ! $query->is_main_query() )
		return;

	if ( $query->is_category() ) {
		$query->set( 'posts_per_page', -1 );
		return;
	}
}
```

### WordPress new WP_Query()

type : `wp_query￼￼ + [TAB]`

```
<?php
	$args = array(
		'posts_per_page'   => 5,
		'post_type'        => 'post',
	);
	$the_query = new WP_Query( $args );
?>
<?php if ( $the_query->have_posts() ) : ?>
	<?php while ( $the_query->have_posts() ) : $the_query->the_post(); ?>
		<?php
			/* do stuff 
			the_title(), the_permalink() 等使用可
			*/
		?>
	<?php endwhile; ?>
<?php else : ?>
	// no posts found
<?php endif; ?>
<?php wp_reset_postdata(); ?>
```

### WordPress get_posts()

type : `wp_get_posts￼￼ + [TAB]`

```
<?php
	$args = array(
		'posts_per_page'   => 5,
		'offset'           => 0,
		'category'         => '',
		'orderby'          => 'post_date',
		'order'            => 'DESC',
		'include'          => '',
		'exclude'          => '',
		'meta_key'         => '',
		'meta_value'       => '',
		'post_type'        => 'post',
		'post_mime_type'   => '',
		'post_parent'      => '',
		'post_status'      => 'publish',
		'suppress_filters' => true
	);
	$my_posts = get_posts( $args );
	global $post; // テンプレートファイル内なら書かなくても良い
?>
<?php if ( !empty( $my_posts ) ) : ?>
	<?php foreach ( $my_posts as $post ) : setup_postdata( $post ); ?>
		<?php
			/* do stuff 
			the_title(), the_permalink() 等使用可
			*/
		?>
	<?php endforeach; ?>
<?php else : ?>
	// no posts found
<?php endif;?>
<?php wp_reset_postdata();?>
```

- - - -

This software is released under the MIT License, see LICENSE.txt.