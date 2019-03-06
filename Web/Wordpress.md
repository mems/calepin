- http://roots.io/using-composer-with-wordpress/
- [roots/sage: WordPress starter theme with a modern development workflow](https://github.com/roots/sage)
- https://github.com/markjaquith/WordPress-Skeleton
- [How To Make WordPress Hard For Clients To Mess Up – Smashing Magazine](https://www.smashingmagazine.com/2016/07/how-to-make-wordpress-hard-for-clients-to-mess-up/)
- [Theme Check — WordPress Plugins](https://fr.wordpress.org/plugins/theme-check/)
- [Moving to HTTPS on WordPress | CSS-Tricks](https://css-tricks.com/moving-to-https-on-wordpress/)
- [Editing wp-config.php « WordPress Codex](https://codex.wordpress.org/Editing_wp-config.php)

## Composer

- [Using Composer With WordPress — Smashing Magazine](https://www.smashingmagazine.com/2019/03/composer-wordpress/)
 
	"extra": {
		"webroot-dir": "www",
		"webroot-package": "wordpress",
		"installer-paths": {
			"app/plugins/{$name}/": ["type:wordpress-plugin"],
			"app/mu-plugins/{$name}/": ["type:wordpress-muplugin"],
			"app/themes/{$name}/": ["type:wordpress-theme"]
		}
	}
	
	
	/** Absolute path to the WordPress directory. */
	if ( !defined('ABSPATH') )
		define('ABSPATH', dirname(__FILE__) . '/wordpress/');
	
	/** Absolute path to the WordPress wp-content directory, which holds your themes, plugins, and uploads */
	//define( 'WP_CONTENT_DIR', dirname(__FILE__) . '/wp-content' );
	
	//--------
	
	/**
	* Automatic Url + Content Dir/Url Detection for Wordpress
	*/
	$document_root = rtrim(str_replace(array('/', '\\'), '/', $_SERVER['DOCUMENT_ROOT']), '/');
	
	$root_dir = str_replace(array('/', '\\'), '/', __DIR__);
	$wp_dir = str_replace(array('/', '\\'), '/', __DIR__ . '/wp');
	$wp_content_dir = str_replace(array('/', '\\'), '/', __DIR__ . '/wp-content');
	
	$root_url = substr_replace($root_dir, '', stripos($root_dir, $document_root), strlen($document_root));
	$wp_url = substr_replace($wp_dir, '', stripos($wp_dir, $document_root), strlen($document_root));
	$wp_content_url = substr_replace($wp_content_dir, '', stripos($wp_content_dir, $document_root), strlen($document_root));
	
	$scheme = (isset($_SERVER['HTTPS']) AND $_SERVER['HTTPS'] != 'off' AND !$_SERVER['HTTPS']) ? 'https://' : 'http://';
	$host = rtrim($_SERVER['SERVER_NAME'], '/');
	$port = (isset($_SERVER['SERVER_PORT']) AND $_SERVER['SERVER_PORT'] != '80' AND $_SERVER['SERVER_PORT'] != '443') ? ':' . $_SERVER['SERVER_PORT'] : '';
	
	$root_url = $scheme . $host . $port . $root_url;
	$wp_url = $scheme . $host . $port . $wp_url;
	$wp_content_url = $scheme . $host . $port . $wp_content_url;
	
	define('WP_HOME', $root_url); //url to index.php
	define('WP_SITEURL', $wp_url); //url to wordpress installation
	define('WP_CONTENT_DIR', $wp_content_dir); //wp-content dir
	define('WP_CONTENT_URL', $wp_content_url); //wp-content url
	
	//-------
	
	include_once './vendor/autoload.php';
	require( './wordpress/wp-blog-header.php' );

- http://matgargano.com/modern-wordpress-development-composer/

## Rest API

- [Headless WordPress: The Ups And Downs Of Creating A Decoupled WordPress — Smashing Magazine](https://www.smashingmagazine.com/2018/10/headless-wordpress-decoupled/)

## WP Theme

Simple/cleared theme: [BlankSlate — Free WordPress Themes](https://wordpress.org/themes/blankslate/)

	remove_action('wp_head', 'rsd_link');
	remove_action('wp_head', 'wlwmanifest_link');
	remove_action('wp_head', 'wp_shortlink_wp_head');
	remove_action('wp_head', 'wp_generator');
	remove_action('wp_head', array( $sitepress, 'meta_generator_tag', 20 ) );
	add_filter('xmlrpc_enabled', '__return_false');
	add_filter('json_enabled', '__return_false');
	add_filter('json_jsonp_enabled', '__return_false');

- https://github.com/WordPress/WordPress/
- http://wordpress.org/
- http://codex.wordpress.org/Theme_Development
- https://github.com/roots/roots

## Performance / optimisation

Use [OPcache](http://php.net/manual/en/book.opcache.php)

Tools:

- [Debug Objects — WordPress Plugins](https://wordpress.org/plugins/debug-objects/)
- [P3 (Plugin Performance Profiler) — WordPress Plugins](https://wordpress.org/plugins/p3-profiler/) - Works only with PHP ≤ 5
- [WP-Optimize — WordPress Plugins](https://wordpress.org/plugins/wp-optimize/)

Plugins:

- [WP Super Cache — WordPress Plugins](https://wordpress.org/plugins/wp-super-cache/)
- [W3 Total Cache — WordPress Plugins](https://wordpress.org/plugins/w3-total-cache/)

[`SAVEQUERIES`](https://codex.wordpress.org/Editing_wp-config.php#Save_queries_for_analysis) should be false

- [How to Optimize MySQL Queries - WPML](https://wpml.org/faq/how-to-optimize-mysql-queries/)
- [How to Debug Performance Problems - WPML](https://wpml.org/faq/how-to-debug-performance-problems/)
- [Performance Optimization for Multilingual WordPress Sites with WPML](https://wpml.org/2012/01/can-your-site-run-faster/)

## Custom fields

- [Compare WP - Plugin Comparison - Content Type / Custom Fields - Google Sheets](https://docs.google.com/spreadsheets/d/1mSqienVYxLopTFGLPK0lGCJst2knKzXDtLQRgwjeBN8/edit#gid=3)
- [ACF | Advanced Custom Fields Plugin for WordPress](https://www.advancedcustomfields.com/) and https://wordpress.org/plugins/acf-to-rest-api/

## Regenerate thumbnails

- [Regenerate Thumbnails — WordPress Plugins](https://wordpress.org/plugins/regenerate-thumbnails/)
- [Force Regenerate Thumbnails — WordPress Plugins](https://wordpress.org/plugins/force-regenerate-thumbnails/)

## AJAX

- http://code.tutsplus.com/articles/getting-started-with-ajax-wordpress-pagination--wp-23099
- http://codex.wordpress.org/AJAX_in_Plugins
- http://www.smashingmagazine.com/2011/10/18/how-to-use-ajax-in-wordpress/

- https://wordpress.org/plugins/rest-api/

## Captcha

- http://wordpress.org/plugins/really-simple-captcha/

## Form

- [Contact Form 7 — WordPress Plugins](https://wordpress.org/plugins/contact-form-7/) - free
- [WordPress Forms - Gravity Forms Contact Form Builder and Lead Data Management Plugin For WordPress](http://www.gravityforms.com/) - emailing + [Gravity Flow - Automate your business processes with Gravity Forms.](https://gravityflow.io/) (request and approval process)
- [Contact Form & SMTP Plugin by PirateForms — WordPress Plugins](https://wordpress.org/plugins/pirate-forms/) - free

## User feedback

- http://wordpress.org/plugins/get-satisfaction-for-wordpress/
- http://wordpress.org/plugins/user-voice/
- http://www.onfry.com/projects/voteitup/

- https://getsatisfaction.com/getsatisfaction/topics/pulling_back_support_for_wordpress_integration
- https://developer.uservoice.com/docs/api/getting-started/
- http://feedback.uservoice.com/forums/1-general-feedback
- http://wordpress.org/plugins/uservoice-idea-list-widget/
- http://feedback.uservoice.com/knowledgebase/articles/56243-use-a-link-custom-trigger-to-open-the-uservoice
- http://feedback.uservoice.com/knowledgebase/articles/276635-use-just-smartvote-the-contact-form-or-satisfacti

- GetSatisfaction
- Zendesk
- Desk

## Job manager

- http://wordpress.org/plugins/job-manager/
- http://wordpress.org/plugins/wp-job-manager/
- http://premium.wpmudev.org/blog/6-wordpress-job-board-solutions/

## Social integration Twitter / Facebook

- http://wordpress.org/plugins/facebook/
- https://wordpress.org/plugins/twitter/
- [A widget for displaying recent tweets](http://wordpress.org/plugins/jetpack/)
- http://wordpress.org/plugins/recent-facebook-posts/
- http://wordpress.org/plugins/custom-facebook-feed/
- http://wordpress.org/plugins/fb-wallpost-widget/screenshots/
- FB as RSS

## Multilingual

Note: Has a performance impact

- [Set Up a Multilingual Blog — Support — WordPress.com](https://en.support.wordpress.com/set-up-a-multilingual-blog/)
- [Polylang — WordPress Plugins](https://wordpress.org/plugins/polylang/)
- [Multilingual WordPress « WordPress Codex](https://codex.wordpress.org/Multilingual_WordPress)
- [Bogo — WordPress Plugins](https://wordpress.org/plugins/bogo/)
- [MultilingualPress — WordPress Plugins](https://wordpress.org/plugins/multilingual-press/)
- WPML - quite slow and could break things (remove translations when save, etc.)
- [Internationalization for Your WordPress Theme — SitePoint](https://www.sitepoint.com/internationalization-wordpress-theme/)

## Localization

- http://wordpress.org/plugins/codestyling-localization/screenshots/
- http://wordpress.org/plugins/easy-translator-lite/screenshots/

## SVG

- [SVG uploads in WordPress (the Inconvenient Truth)](https://bjornjohansen.no/svg-in-wordpress)
- [Safe SVG — WordPress Plugins](https://wordpress.org/plugins/safe-svg/)
- Improving SVG Display in the Media Library [WordPress SVG Support: How to Enable SVGs in WordPress](https://www.sitepoint.com/wordpress-svg/#improving-svg-display-in-the-media-library)
- [SVG uploads in WordPress (the Inconvenient Truth)](https://bjornjohansen.no/svg-in-wordpress)

## Security

See [Wordpress](Security#Wordpress)

## File permissions for automatic update

Apache use a different group than FTP users. It's a safe measure, but updates can't be automatic (require SSH or FTP credentials).
Ex: FTP: user 522/538; Apache/PHP: 48/48 (www-data)

	#!/bin/bash
	USER=user
	PASSWD=password
	SITE=www.example.com
	#DIR_MOD=0755
	DIR_MOD=0775
	#FILE_MOD=0644
	FILE_MOD=0664
	ROOT_DIR=/public_html
	
	# use `cat` instead of last command after the last pipe for dry-run
	{
	lftp <<EOF
	open -u $USER,$PASSWD $SITE
	find $ROOT_DIR
	exit
	EOF
	} | gawk 'BEGIN { print "open -u '$USER','$PASSWD' '$SITE'" } { if (match($0 ,/\/$/)) printf "chmod '$DIR_MOD' \"%s\"\n", $0; else printf "chmod '$FILE_MOD' \"%s\"\n", $0 } END { print "exit" }' | lftp

> The Code is in [get_filesystem_method()](https://developer.wordpress.org/reference/functions/get_filesystem_method/). Wordpress tries to create a file 'wp-content/temp-write-test-'.time()

	define( 'FTP_USER', 'username' );
	define( 'FTP_PASS', 'password' );
	define( 'FTP_HOST', 'ftp.example.org' );

- [Editing wp-config.php « WordPress Codex](https://codex.wordpress.org/Editing_wp-config.php#WordPress_Upgrade_Constants)
- [php - Correct file permissions for WordPress - Stack Overflow](https://stackoverflow.com/questions/18352682/correct-file-permissions-for-wordpress)
- [Changing File Permissions « WordPress Codex](https://codex.wordpress.org/Changing_File_Permissions)
- [Updating WordPress « WordPress Codex](https://codex.wordpress.org/Updating_WordPress#Automatic_Update)
- [Fix wordpress file permissions](https://gist.github.com/Adirael/3383404)
- [Wordpress asking for my FTP credentials to install plugins - Stack Overflow](https://stackoverflow.com/questions/17922644/wordpress-asking-for-my-ftp-credentials-to-install-plugins)
- [plugins - What security concerns should I have when setting FS_METHOD to "direct" in wp-config? - WordPress Development Stack Exchange](https://wordpress.stackexchange.com/questions/189554/what-security-concerns-should-i-have-when-setting-fs-method-to-direct-in-wp-co)
