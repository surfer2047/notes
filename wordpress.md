#Creating Themes form scratch
Go to wp-content/themes/
$ sudo mdir -p wp-content/themes/learningwordpress
$ cd learningwordpress
$ touch index.php, style.css #Just create two files named as index.php and style.css

Ok let us code style.css file

style.css file
--------------
/*
Theme Name: xtermnepal
Author: @nix197
Author URI: http://plus.google.com/+nix1947
Version: 1.0


*/


index.php
-----------
<h1> Hello </h1>	




wordpress functions
---------------------
the_excerpt();
have_posts(); //to check for the posts whether there are posts or not
get_header(); //function to call the header section
get_footer(); //function to call the footer section
the_title(); //pull the post heading
the_permalink(); //pull href tag of the post title
the_content(); //pull the body of the post
<html <?php language_attributes(); ?>
<meta charset="<?php bloginfo('charset'); ?>" >
<meta name="viewport" content="width=device-width">
<title><?php bloginfo('name') ?> </title>
wp_head(); //later on if we add different plugins, it will allow to add the other plugin to add the code after our code
<body body_class(); ?> //use for resetting
bloginfo('name') //Give the name of the blog
bloginfo('description') //Give the tag line of the blog
bloginfo('charset')  // set the charset of the blog
echo home_url(); //will output the value of homepage domain_name
the_title(); //pull the title of the post
echho wp_footer()
date('Y');
wp_nav_menu();
wp_enque_style('style', get_stylesheet_uri());
add_action('wp_enqueue_scripts', 'learningWOredpress_resources'); // learningWordpress_resources is the name of function
register_nav_menus(array(
 'primary' = __(" Primary Menu"),
 'footer' = __("Footer Menu"),
));
the_time('F jS, Y')
<?php the_time('F jS, Y g:i a');?> To dislay the data and time of the post

is_page(14) 
get_post_ancestors() // this will give the array

<?php wp_list_pages($args) ?>
<?php 

$args = array(
	'child_of' => $post->ID
	);
   wp_list_pages($args);

?>
get_post_format()

customize the header and footer
----------------------------------
To customize the header and footer, create the two file called 
1. header.php
2. footer.php

when these file present in the folder, this file will automatically override the header and footer with their settings/code


header.php
-------------
Header is not the exiciting file, but one of the more important files, This is the page, where your put your code that all the pages need, just like analytics files
DOCTYPE, just open the HTML tag in header and close that html tag in footer, we open the body tag in html and close it into the footer.php file

<!DOCTYPE html>
<html>
<head>
	<meta charset="<?php bloginfo('charset'); ?>" >
	<meta name="viewport" content="width=device-width">
	<title><?php  bloginfo('name'); ?></title>
	<?php wp_head(); ?>
</head>

<body <?php  body_class(); ?> >

<!-- header -->
<header>
	<h1><a href="<?php  echo home_url(); ?>"><?php bloginfo('name'); ?></a></h1>
	<h5><?php  bloginfo('description'); ?></h5>
	

</header>

<!-- end site-header -->






footer.php
----------
</body>
</html>

functions.php
---------------
This file is used to include the css/javascripts 

<?php

function load_wordress_stylesheet(){

	wp_enqueue_style('style', get_stylesheet_uri()); //get the wordpress uri

}

add_action('wp_enqueue_scripts', 'load_wordress_stylesheet');

?>


css
--------
/*
Theme Name: Jubhung
Author: @nix1947
Author URI: http://openpy.com
Version : 1.0he

*/

body {
	font-family: sans-serif;
	color: #333;
}

p {
	line-height: 1.65em;
}
a:link,
a:visited {
	color: #61A534
}

/* General layout */

div.container {
	max-width: 920px;
	margin: 0 auto; /* Center it horizontially */
	padding-left: 20px;
	padding-right: 20px;
}

article.post{
	border-bottom: 2px dotted green;
}

article.post:last-of-type{
	border-bottom: none;

}

.site-header {
	border-bottom: 2px solid green;
}

/* footer css */
.site-footer {
	margin-top: 20px; 
	border-bottom: 2px solid green;

}


wordpress navigation menu
-----------------------------
This will in header.php just below the </header> tag
<div class="site-container">
		<header class="site-header">
			<h1><a href="<?php echo home_url(); ?>"><?php bloginfo('name'); ?> </a> </h1>
			<h5> <?php bloginfo('description'); ?> </h5>

			<!-- navigation menu below the header -->
			<nav class="site-nav">
				<?php wp_nav_menu(); ?>
			</nav> <!-- end of site nav-->
			
		</header> <!-- end of site-header -->



creating menu location in wordpress
--------------------------------------
<nav class="site-nav">
				<?php 
					$args = array('theme_location' => 'primary' );

				?>
				<?php wp_nav_menu($args); ?>
			</nav> <!-- end of site nav-->
................ AND
	
	<footer class="site-footer">
		<nav class="site-nav">
			<?php $args = array('theme_location' => 'footer' );?>
		</nav>
		<p><a href="<?php home_url(); ?>"> <?php bloginfo('name'); ?> </a> &copy; <?php  echo date('Y'); ?></p>
		
	</footer> <!-- end of site-footer -->
	</div> <!-- end of site-container -->
	<?php wp_footer(); ?> 
</body> <!-- end of body tag from header.php file -->
</html> <!-- end of html tag from header.php file --> 

After creating menu, we need to register those menus
-------------------------------------------------------
// registering Menus

	register_nav_menus(array(

		'primary' => __("Primary Menu"),
		'footer' => __("Footer Menu"),
		));


styling the pages
---------------------
we can style the page by making the page.php
just copy the index.php code and make the changes

different layout for different pages

condition logic and page templates to make layout the pages
--------------------------------------------------------------
in the header.php file
if(is_page('about-us')
{
	echo "Thank you for visiting this page"
}

To entierly make new page layout just create a new page-slugname.php or page-id.php file and copy the content from the page.php into the newely created file
to create a template_layout we need to put the /* Template Name: Something like this to the template Layout */


special template page.php
---------------------------
<?php 
/*
Template Name: Special Template

*/
get_header();
if(have_posts()) : 
	while(have_posts()) : the_post(); ?>

	<article class="post page">
		<h2><?php the_title(); ?></h2>
		<!-- Disclaimer Box -->
		<div class="info-box">
		Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
		tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
		quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
		consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
		cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
		proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
			
		</div>
		<p><?php the_content(); ?></p>
	</article>

	<?php 
	endwhile; 

else :
	echo "<p> Post cannot found </p>";
endif;


get_footer();
?>


managing child pages and its link
-------------------------------------
<span class="parent-link"><a href="<?php echo get_the_permalink(get_top_ancestor_id());  ?>"><?php echo get_the_title(get_top_ancestor_id()); ?></a></span>



working with the metadata in wordrpress
---------------------------------------------
Displaying date in post
<?php the_time('m/d/y') ?>
<?php the_time('F jS, Y g:i a'), he use the class post-info to define these fields

Displaying author Name
<p class="post-info"><?php the_time('F js, Y gLi a') ?> | <?php the_author() ?> </p> <!-- This will Display author and time -->

Now let us make a link to the author that takes to the archive of that author 

<a href="<?php echo get_author_posts_url(get_the_author_meta('ID')); ?>"> <php the_author(); ?> </a> => This will display the archives post by the 
so Now let us add the categories this post belongs to

<p> | Posted in <?php 
	$categories = get_the_category(); //this will return array of category 
	$seperators = ", ";
	$output = '';

	if($categories)
	{
	 foreach($categories as $category)
		{
			$output .= $category->cat_name .$seperators;
		}
        	echo trim($output, $seperators); //This will remove the comma
	}

 ?>

Now let us add the links, and also remove comma at the end
just use the code <?php echo trim($output, $seperators); ?>

To add link just use this
<?php $output .= '<a href="'. get_category_link($category -> term_id) .'">' .$category->cat_name . '</a>' .$seperators  ?> //note not semicolon on the page



Archive tutorials
====================
archive.php
-------------	
COntrol the output of the archives pages, On default the wordpress use the index.php file as the template for the archive, so it would be nice with the Name of 
the archives,
you can copy and paste the content from the index.php and put the archive title using the php code
<?php   

<?php  

		if(is_category())
		{
			echo "Category Archive";
		}elseif (is_tag()) {
			echo "Tag Archive";
		}elseif (is_author()) {
			echo "Author Archive";
		}elseif (is_day()) {
			echo "Day archive";
		}elseif (is_month()) {
			echo "Month Archive";
		}elseif (is_year()) {
			echo "Year archive";
		}
		else
		{
			echo "Archives";
		}



 ?>

?>


Wordpress Excerpt title
========================
go to the any page temeplate you want to customize and look for the the_content();
<?php the_content('Continue Reading &raquo;') ?>

<?php the_excerpt(); ?>

excerpt text are those customs text which will displayed just below the text. you can adjust this by going into the screen options.

for all post to have excerpt setting just create the page called single.php, copy the content of index.php and just replace the content
with the_excerpt();
<?php the_excerpt(); ?> 

//use this code 
<p><?php echo get_the_excerpt(); ?>
		<a href="<?php echo the_permalink(); ?>">Read more &raquo; </a>
		</p>

By default wordpress display the 55 words in the excerpt, so let us customize this method, to set this features we need to add some code in functions.php file


// Customize customize excerpt word count lenght

function custom_excerpt_length()
{
  return 25; // this will return 25 word
} 

we need to call this function

// add_filter
add_action('excerpt_length', 'custom_excerpt_length');

if($post->post_excerpt) 
{

<p><?php echo get_the_excerpt(); ?>
		<a href="<?php echo the_permalink(); ?>">Read more &raquo; </a>
		</p>


}
else
{
 the_content();
}


Wordpress Featured Image tutorials
======================================
adding some code to functions.php file to make sure that our theme supports features images 
function.php

// Add features image support
add_theme_support('post-thumbnails');
// add features image to the post
	//add_theme_support('post-thumbnails') bad way
	//correct way is
	function feature_image_support()
	{
		add_theme_support('post-thumbnails');
		add_image_size('small-thumbnail' 180, 120, true) // 180px width 120px tall if not fitsize just crop the image true will crop the image
		banner_image_size(920, 210, true)
	}

add_action('after_setup_theme', 'feature_image_support');
---------------------------------------------------------------
No display this featured image in this post, Now go to index.php folder and output the image in thumbnail size
just above the content 
<?php the_post_thumbnail('small-thumbnail); ?> //small-thumbnail is defined in function.php above just put the small version of this image

so, let us just register the new theme images support in function.php file in the add features image section

so now let us specify which part of the image should be crop using the code
<?php banner_image_size(920, 210, array(top, left)) ?>

so let us position the image using css,
<div class="post-image">

</div>

.post-image 
{


}


wordpress search functionality
=================================
we will add the search bar in the header section
<?php get_serach_form()?>
To customize the searchform we need to create a new file called searchform.php file where we can customize the search bar of the wordpress theme

search.php file
--------------------
In search.php file wordpress put the search results in this file, if there is no search.php file it will use the index.php to display the search, to customize the search just copy the index.php file and modified it
<h2>php search Result for <?  the_search_query(); ?>


template part 1 tutorial
=========================
get_template_part(); //allow our code to be dry
jut cut the code inside the while loop in index.php and paste into the page called content.php and use the function get_template_part(); in that cut are as
//get_template_part('content');

if(is_search()) 

Post formating
==============
There are nine different types of post format in wordpress
we will enable post format and handcraft the presentation
go to the functions.php and add the following code to support these features inside any function
<?php // Add post format support
		add_theme_support('post-formats', array('aside', 'gallary', 'link')); //support aside, gallary and link theme support ?> and after adding this 
in index.php file pass the parameter name get_post_format() function to 
//get_template_part('content-aside', get_post_format());

create the new page content-aside.php file and put all the formatting there
in content-aside.php this will only change the aside post format


working with link post format
=============================
content-link.php
-------------------
<article class="post post-link">
	<a href="<?php echo get_the_content(); ?>


working with widgets
=====================
DISPLAYED on website

Find the location where to put the widgets

//code to enable the sidebarwidgets in functions.php

//Add our widgets locations

function ourwidgetinitilize()
{
register_sidebar(array(

 'name' => 'Sidebar',
 'id' => 'sidebar1',
 'before-widget' => '<div class="mytitle">', //used to put div tag in category title
 'after-widget' => '</div'> //used to put div tag in category title
 'before-title' =>
));

so call this widgets in our templeate
<p><?php dynamic_sidebar('sidebar1'); ?> </p>
By this you can create the number of widgets area, where id will be the seperator

}

add_action('widgets_init', ourwidgetinitilze')


<?php if(is_active_sidebar('sidebar1') :  />
 <div>
 <?php dynamic_sidebar('sidebar1'); ?>
 </div>

endif;


Actually the above code will be site in the sidebar.php file

so let us create the sidebar.php file

and in the index.php file where the code was cut call the function called
<?php get_sidebar(); ?>



wordpress Custom Home page
==============================
Generally wordpress look for the front-page.php file to display for the homepage customize if there is not front-page.php file, then it will display the page.php template, 
what we will generally do is copy the content of page.php and dump that into the front-page.php we will make wp_query(); to push the files



wp_query()
============
// pull the post that have the category of mail

$mailcategory = new WP_Query('cat=7&post_per_page=2&order_by=title&order_of=DESC&post_per_page=2')  //if there post_per_page not given display all the post with category with mail
if ($mail -> have_posts()) : 				//by default wp_query pull the post by latest data, we can also pull by the query
 while($mail -> have_posts()) : $mail -> the_post()

 //output the content however we do
	<h2>

 endwhile;
 
 else :
   echo "<h1";
endif;
wp_reset_post_data(); //always need to run this code after calling the wp_query 



wordress Meta boxes
======================
