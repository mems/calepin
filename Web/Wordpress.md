- [How To Make WordPress Hard For Clients To Mess Up – Smashing Magazine](https://www.smashingmagazine.com/2016/07/how-to-make-wordpress-hard-for-clients-to-mess-up/)
- [WordPress Developer Resources | Official WordPress Developer Resources](https://developer.wordpress.org/)
- [Using Web Components in WordPress is Easier Than You Think | CSS-Tricks](https://css-tricks.com/using-web-components-in-wordpress-is-easier-than-you-think/)

## Install and maintain

- [Command line interface for WordPress | WP-CLI](https://wp-cli.org/)
- [markjaquith/WordPress-Skeleton: Basic layout of a WordPress Git repository. I use this as a base when creating a new repo.](https://github.com/markjaquith/WordPress-Skeleton)
- [Moving to HTTPS on WordPress | CSS-Tricks](https://css-tricks.com/moving-to-https-on-wordpress/)

### Composer

- [Using Composer with WordPress | Roots](https://roots.io/using-composer-with-wordpress/)
- [Using Composer With WordPress — Smashing Magazine](https://www.smashingmagazine.com/2019/03/composer-wordpress/)

```json
"extra": {
	"webroot-dir": "www",
	"webroot-package": "wordpress",
	"installer-paths": {
		"app/plugins/{$name}/": ["type:wordpress-plugin"],
		"app/mu-plugins/{$name}/": ["type:wordpress-muplugin"],
		"app/themes/{$name}/": ["type:wordpress-theme"]
	}
}
```

```php
<?php
/** Absolute path to the WordPress directory. */
if ( !defined('ABSPATH') )
	define('ABSPATH', dirname(__FILE__) . '/wordpress/');

/** Absolute path to the WordPress wp-content directory, which holds your themes, plugins, and uploads */
//define( 'WP_CONTENT_DIR', dirname(__FILE__) . '/wp-content' );
?>
```

```php
<?php
include_once './vendor/autoload.php';
require( './wordpress/wp-blog-header.php' );
?>
```

### Docker

- [Quickstart: Compose and WordPress | Docker Documentation](https://docs.docker.com/compose/wordpress/)
- [nezhar/wordpress-docker-compose: Easy Wordpress development with Docker and Docker Compose](https://github.com/nezhar/wordpress-docker-compose)
- [wordpress - How to run wp cli in docker-compose.yml - Stack Overflow](https://stackoverflow.com/questions/50999848/how-to-run-wp-cli-in-docker-compose-yml)

### Config

```php
<?php
/*
Automatic Url + Content Dir/Url Detection for Wordpress
Based on https://gist.github.com/CMCDragonkai/7578784#gistcomment-1237365 and https://stackoverflow.com/questions/1175096/how-to-find-out-if-youre-using-https-without-serverhttps
*/
// Use realpath to resolve symlinks (like /homez.xxx/ to /home/)
$document_root = rtrim(str_replace(array('/', '\\'), '/', realpath($_SERVER['DOCUMENT_ROOT'])), '/');

$root_dir = str_replace(array('/', '\\'), '/', __DIR__);
$wp_dir = str_replace(array('/', '\\'), '/', rtrim(ABSPATH, '/'));
$wp_content_dir = str_replace(array('/', '\\'), '/', WP_CONTENT_DIR);

$root_url = substr_replace($root_dir, '', stripos($root_dir, $document_root), strlen($document_root));
$wp_url = substr_replace($wp_dir, '', stripos($wp_dir, $document_root), strlen($document_root));
$wp_content_url = substr_replace($wp_content_dir, '', stripos($wp_content_dir, $document_root), strlen($document_root));

$scheme = (isset($_SERVER['HTTPS']) && $_SERVER['HTTPS'] != 'off' || isset($_SERVER['SERVER_PORT']) && $_SERVER['SERVER_PORT'] == 443 || isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && strtolower($_SERVER['HTTP_X_FORWARDED_PROTO']) == 'https') ? 'https://' : 'http://';
$host = rtrim($_SERVER['SERVER_NAME'], '/');
$port = (isset($_SERVER['SERVER_PORT']) && $_SERVER['SERVER_PORT'] != '80' && $_SERVER['SERVER_PORT'] != '443') ? ':' . $_SERVER['SERVER_PORT'] : '';

$root_url = $scheme . $host . $port . $root_url;
$wp_url = $scheme . $host . $port . $wp_url;
$wp_content_url = $scheme . $host . $port . $wp_content_url;

define('WP_HOME', $root_url); //url to index.php
define('WP_SITEURL', $wp_url); //url to wordpress installation
define('WP_CONTENT_URL', $wp_content_url); //wp-content url
?>
```

- [Editing wp-config.php « WordPress Codex](https://codex.wordpress.org/Editing_wp-config.php)

### Update site URL

```sql
SET @current = 'http://some.example.com';
SET @next = 'https://www.example.com';
UPDATE wp_options SET option_value = replace(option_value, @curent, @next) WHERE option_name = 'home' OR option_name = 'siteurl';
UPDATE wp_posts SET post_content = replace(post_content, @curent, @next);
UPDATE wp_postmeta SET meta_value = replace(meta_value,@curent,@next);
UPDATE wp_usermeta SET meta_value = replace(meta_value, @curent,@next);
UPDATE wp_links SET link_url = replace(link_url, @curent,@next);
UPDATE wp_comments SET comment_content = replace(comment_content , @curent,@next);
# For images inside posts
UPDATE wp_posts SET post_content = replace(post_content, @curent, @next);
# For images linked in old link manager
UPDATE wp_links SET link_image = replace(link_image, @curent, @next);
# For images linked as attachments
UPDATE wp_posts SET guid = replace(guid, @curent, @next);
# Serialized data via serialize() or json_encode() aren't touched, see https://deliciousbrains.com/wp-migrate-db-pro/doc/serialized-data/
```

- [WP Migrate DB – WordPress plugin | WordPress.org](https://wordpress.org/plugins/wp-migrate-db/) - Free version handle metadata PHP serialization trouble
- [Changing The Site URL | WordPress.org](https://wordpress.org/support/article/changing-the-site-url/)

## Plugins

- [Proxy Cache Purge](https://fr.wordpress.org/plugins/varnish-http-purge/)
- [WP Statistics](https://fr.wordpress.org/plugins/wp-statistics/)

## Rest API

- [Reference | REST API Handbook | WordPress Developer Resources](https://developer.wordpress.org/rest-api/reference/)
- [Headless WordPress: The Ups And Downs Of Creating A Decoupled WordPress — Smashing Magazine](https://www.smashingmagazine.com/2018/10/headless-wordpress-decoupled/)

## Themes

Simple/cleared theme: [BlankSlate — Free WordPress Themes](https://wordpress.org/themes/blankslate/)

```php
<?php
remove_action('wp_head', 'rsd_link');
remove_action('wp_head', 'wlwmanifest_link');
remove_action('wp_head', 'wp_shortlink_wp_head');
remove_action('wp_head', 'wp_generator');
remove_action('wp_head', array( $sitepress, 'meta_generator_tag', 20 ) );
add_filter('xmlrpc_enabled', '__return_false');
add_filter('json_enabled', '__return_false');
add_filter('json_jsonp_enabled', '__return_false');
?>
```

- https://github.com/WordPress/WordPress/blob/master/wp-content/themes/twentyfourteen
- [WordPress/WordPress: WordPress, Git-ified. Synced via SVN every 15 minutes, including branches and tags! This repository is just a mirror of the WordPress subversion repository. Please do not send pull requests. Submit patches to https://core.trac.wordpress.org/ instead.](https://github.com/WordPress/WordPress/)
- [Theme Development « WordPress Codex](https://codex.wordpress.org/Theme_Development)
- [roots/sage: WordPress starter theme with a modern development workflow](https://github.com/roots/sage)
- [Theme Check — WordPress Plugins](https://fr.wordpress.org/plugins/theme-check/)

### Template hierarchy

- [Template Hierarchy | Theme Developer Handbook | WordPress Developer Resources](https://developer.wordpress.org/themes/basics/template-hierarchy/)

### Theme development

- [Theme Developer Handbook | WordPress Developer Resources](https://developer.wordpress.org/themes/)
- [Handbook – Make WordPress Themes](https://make.wordpress.org/themes/handbook/)
- [Theme Development « WordPress Codex](https://codex.wordpress.org/Theme_Development)

### Nav menu

Aka navigation menu

```php
<?php
// .sub-menu
add_filter( 'nav_menu_submenu_css_class', function ( $classes, $args, $depth ) {
	if($args->theme_location == 'primary') $classes = array($depth == 0 ? 'ns-main-nav-subsections' : 'ns-main-nav-items');
	return $classes;
}, 10, 3);
// .menu-item > a
add_filter( 'nav_menu_link_attributes', function ( $atts, $item, $args, $depth ) {
	if($args->theme_location == 'primary') $atts['class'] = $depth == 0 ? 'ns-main-nav-section-link' : 'ns-main-nav-link';
	return $atts;
}, 10, 4);
// .menu-item
add_filter( 'nav_menu_css_class', function ( $classes, $item, $args, $depth ) {
	if($args->theme_location == 'primary'){
		switch ($depth){
			case 0:
				$class = 'ns-main-nav-section';
				break;
			case 1:
				$class = 'ns-main-nav-subsection';
				break;
			default:
				$class = 'ns-main-nav-item';
				break;
		}
		$classes = array($class);
	}
	return $classes;
}, 10, 4);

// Add wrapper to .sub-menu
//class Custom_Walker_Nav_Menu extends Walker_Nav_Menu {
//	public function start_lvl( &$output, $depth = 0, $args = null ) {
//		if($depth == 0) $output .= '<div class="mcp-main-nav-subsections-wrapper">';
//		parent::start_lvl($output, $depth, $args);
//	}
//	public function end_lvl( &$output, $depth = 0, $args = null ) {
//		parent::end_lvl($output, $depth, $args);
//		if($depth == 0) $output .= '</div>';
//	}
//}

// Render the nav menu
wp_nav_menu(
	array(
		'container'  => '',
		'menu_class'  => 'ns-main-nav-sections',
		'items_wrap' => '<ul id="%1$s" class="%2$s">%3$s</ul>',
		'theme_location' => 'primary',
//		'walker' => new Custom_Walker_Nav_Menu(),
	)
);
?>
```

## Performance and optimisation

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
- [Nginx + WordPress + fastcgi_cache with conditional purging](https://easyengine.io/wordpress-nginx/tutorials/single-site/fastcgi-cache-with-purging/) - [How to Setup FastCGI Caching with Nginx on your VPS | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-setup-fastcgi-caching-with-nginx-on-your-vps)

## Custom fields

Fields starts with `_` are not visible defaut meta box for custom field

Gutenberg editor plugins can be written with JSX/ES6 or ES5 (without compilation)

- [Custom Fields – WordPress.org Forums](https://wordpress.org/support/article/custom-fields/)
- [How to Add Post Meta Fields to Gutenberg Document Sidebar - A White Pixel](https://awhitepixel.com/blog/how-to-add-post-meta-fields-to-gutenberg-document-sidebar/)
- [Compare WP - Plugin Comparison - Content Type / Custom Fields - Google Sheets](https://docs.google.com/spreadsheets/d/1mSqienVYxLopTFGLPK0lGCJst2knKzXDtLQRgwjeBN8/edit#gid=3)
- [ACF to REST API – WordPress plugin | WordPress.org](https://wordpress.org/plugins/acf-to-rest-api/)

Validation / sanitization / authorization:

- [sanitize_{$object_type}_meta_{$meta_key}_for_{$object_subtype} | Hook | WordPress Developer Resources](https://developer.wordpress.org/reference/hooks/sanitize_object_type_meta_meta_key_for_object_subtype/)
- [sanitize_{$object_type}_meta_{$meta_key} | Hook | WordPress Developer Resources](https://developer.wordpress.org/reference/hooks/sanitize_object_type_meta_meta_key/)
- [auth_{$object_type}_meta_{$meta_key}_for_{$object_subtype} | Hook | WordPress Developer Resources](https://developer.wordpress.org/reference/hooks/auth_object_type_meta_meta_key_for_object_subtype/)
- [auth_{$object_type}_meta_{$meta_key} | Hook | WordPress Developer Resources](https://developer.wordpress.org/reference/hooks/auth_object_type_meta_meta_key/)
- [`sanitize_callback` and `auth_callback` arguments](https://developer.wordpress.org/reference/functions/register_meta/) are depreciated
- [update_{$meta_type}_metadata_by_mid | Hook | WordPress Developer Resources](https://developer.wordpress.org/reference/hooks/update_meta_type_metadata_by_mid/) - see also
- [update_{$meta_type}_metadata | Hook | WordPress Developer Resources](https://developer.wordpress.org/reference/hooks/update_meta_type_metadata/)
- [add_{$meta_type}_metadata | Hook | WordPress Developer Resources](https://developer.wordpress.org/reference/hooks/add_meta_type_metadata/)

Some:

- [Home - Carbon Fields](https://carbonfields.net/)
- [ACF | Advanced Custom Fields Plugin for WordPress](https://www.advancedcustomfields.com/)
- [Home - Pods Framework](https://pods.io/)
- [Meta Box - WordPress Custom Fields and Custom Meta Boxes Framework](https://metabox.io/)
- [justintadlock/butterbean: A neat little post meta framework.](https://github.com/justintadlock/butterbean)
- [CMB2/CMB2: CMB2 is a developer's toolkit for building metaboxes, custom fields, and forms for WordPress that will blow your mind.](https://github.com/CMB2/CMB2)

See also:

- [Metadata | Plugin Developer Handbook | WordPress Developer Resources](https://developer.wordpress.org/plugins/metadata/)

## Custom post types

- [Custom Post Types | Apprendre WordPress](https://learn.wordpress.org/lesson-plan/custom-post-types/)
- [Registering Custom Post Types | Plugin Developer Handbook | WordPress Developer Resources](https://developer.wordpress.org/plugins/post-types/registering-custom-post-types/).

## Custom plugins

mu-plugins aka multi user plugins, must-use plugins

- [Plugin Developer Handbook | WordPress Developer Resources](https://developer.wordpress.org/plugins/)
- [Must Use Plugins | WordPress.org](https://wordpress.org/support/article/must-use-plugins/)
- [Traduire vos extensions WordPress - Alsacreations](https://www.alsacreations.com/tuto/lire/1840-traduire-extension-wordpress.html)
- [Plugins in mu-plugins folder are not loaded - WordPress Development Stack Exchange](https://wordpress.stackexchange.com/questions/26337/plugins-in-mu-plugins-folder-are-not-loaded)

## Taxonomy

Aka categories, tags

- [Categories vs. Tags – WordPress.com Support](https://wordpress.com/support/posts/categories-vs-tags/)

## Rewrite

- call `flush_rewrite_rules()`
- Settings > Permalinks > Save changes
- [Flushing Rewrite on Activation](https://developer.wordpress.org/reference/functions/register_post_type/#flushing-rewrite-on-activation)

## Regenerate thumbnails

- [Regenerate Thumbnails — WordPress Plugins](https://wordpress.org/plugins/regenerate-thumbnails/)
- [Force Regenerate Thumbnails — WordPress Plugins](https://wordpress.org/plugins/force-regenerate-thumbnails/)

## Responsive images

- [Responsive Images in WordPress 4.4 – Make WordPress Core](https://make.wordpress.org/core/2015/11/10/responsive-images-in-wordpress-4-4/)
- [Responsive Images Now Landed In WordPress Core — Smashing Magazine](https://www.smashingmagazine.com/2015/12/responsive-images-in-wordpress-core/)

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

Use full locale name in `.mo` filenames
For mu-plugins (see [`load_muplugin_textdomain()`](https://developer.wordpress.org/reference/functions/load_muplugin_textdomain/)):

```php
<?php
// In wp-content/mu-plugins/<pluginslug>/<pluginslug>.php (with a "loader" `wp-content/mu-plugins/<somename>.php`: `require WPMU_PLUGIN_DIR . '/<pluginslug>/<pluginslug>.php';`)
add_action('muplugins_loaded', fn() => load_muplugin_textdomain('textdomain', dirname(plugin_basename(__FILE__)) . '/languages'));
// This will try to load `<WP_LANG_DIR>/plugins/<textdomain>-<locale>.mo` else `wp-content/mu-plugins/<pluginslug>/languages/<textdomain>-<locale>.mo`
// Where `WP_LANG_DIR` is usually `wp-content/languages`
?>
```

For plugins (see [`load_plugin_textdomain()`](https://developer.wordpress.org/reference/functions/load_plugin_textdomain/)):

```php
<?php
// In wp-content/plugins/<pluginslug>/<pluginslug>.php
add_action('init', fn() => load_plugin_textdomain('textdomain', false, dirname(plugin_basename(__FILE__)) . '/languages'));
// This will try to load `<WP_LANG_DIR>/plugins/<textdomain>-<locale>.mo` else `wp-content/plugins/<pluginslug>/languages/<textdomain>-<locale>.mo`
// Where `WP_LANG_DIR` is usually `wp-content/languages`
?>
```

For theme (see [`load_theme_textdomain()`](https://developer.wordpress.org/reference/functions/load_theme_textdomain/)):

```php
<?php
// In wp-content/themes/<themeslug>/functions.php
add_action('after_setup_theme', fn() => load_theme_textdomain('textdomain', get_template_directory() . '/languages'));
// This will try to load `<WP_LANG_DIR>/themes/<textdomain>-<locale>.mo` else `wp-content/themes/<themeslug>/languages/<locale>.mo`
// Where `WP_LANG_DIR` is usually `wp-content/languages`
?>
```

See also [_get_plugin_data_markup_translate()](https://developer.wordpress.org/reference/functions/_get_plugin_data_markup_translate/), for a plugin with meta comment `Domain Path: /languages` (default to empty) and `Text Domain: text-domain` (require, or no text domain will be (auto-)loaded) will load `wp-content/plugin/<pluginslug><domainpath>/<textdomain>-<locale>.mo`.

To debug which `.mo` files are loaded:

```php
<?php
$debuginfo_textdomain_mofiles = [];
add_filter('load_textdomain_mofile', function ($mofile, $domain) {
	global $debug_textdomain_mofiles;
	$is_mofile_readable = is_readable($mofile);
	$mo = new MO();
	$e = new Exception();
	$debug_textdomain_mofiles[] = array(
		'filename' => $mofile,
		'domain' => $domain,
		'readable' => $is_mofile_readable,
		'trace' => $e->getTraceAsString(),
		'importable' => $is_mofile_readable && $mo->import_from_file($mofile)
	);
	return $mofile;
}, 10, 2);
// Then later in page:
//var_dump($debuginfo_textdomain_mofiles);
?>
```

```php
<?php
printf(
	/* translators: %s: Price amount. */
	__('Price: %s', 'my-text-domain'),
	get_product_price()
);
?>
```

- [wp i18n make-pot | WP-CLI Command | WordPress Developer Resources](https://developer.wordpress.org/cli/commands/i18n/make-pot/) - "Create a POT file for a WordPress project."
- [How to Internationalize Your Plugin | Plugin Developer Handbook | WordPress Developer Resources](https://developer.wordpress.org/plugins/internationalization/how-to-internationalize-your-plugin/)
- [filesystem - What is the difference between the .po .mo and .pot localization files? - WordPress Development Stack Exchange](https://wordpress.stackexchange.com/questions/227822/what-is-the-difference-between-the-po-mo-and-pot-localization-files/227829#227829)
- [I18n for WordPress Developers « WordPress Codex](https://codex.wordpress.org/I18n_for_WordPress_Developers)
- [Codestyling Localization – WordPress plugin | WordPress.org](https://wordpress.org/plugins/codestyling-localization/#screenshots)
- [Easy Translator – WordPress plugin | WordPress.org](https://wordpress.org/plugins/easy-translator-lite/#screenshots)
- [What's the difference between __(), _e(), _x(), and _ex()? - WP Engineer](https://web.archive.org/web/20220420165809/https://wpengineer.com/2237/whats-the-difference-between-__-_e-_x-and-_ex/)

### Plurals

```php
<?php
printf( _n( '%s person', '%s people', $count, 'text-domain' ), number_format_i18n( $count ) );
?>
```


- [_n() | Function | WordPress Developer Resources](https://developer.wordpress.org/reference/functions/_n/)
- [WordPress Localization - How plural forms work](https://web.archive.org/web/20220204122947/https://www.cssigniter.com/wordpress-localization-plural-forms-work/)
- [I18n for WordPress Developers « WordPress Codex](https://codex.wordpress.org/I18n_for_WordPress_Developers#Plurals)

## SVG

- [SVG uploads in WordPress (the Inconvenient Truth)](https://bjornjohansen.no/svg-in-wordpress)
- [Safe SVG — WordPress Plugins](https://wordpress.org/plugins/safe-svg/)
- Improving SVG Display in the Media Library [WordPress SVG Support: How to Enable SVGs in WordPress](https://www.sitepoint.com/wordpress-svg/#improving-svg-display-in-the-media-library)
- [SVG uploads in WordPress (the Inconvenient Truth)](https://bjornjohansen.no/svg-in-wordpress)

## Security

See [Wordpress](../Security/Security.md#wordpress)

## File permissions for automatic update

Apache use a different group than FTP users. It's a safe measure, but updates can't be automatic (require SSH or FTP credentials).
Ex: FTP: user 522/538; Apache/PHP: 48/48 (www-data)

```sh
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
```

> The Code is in [`get_filesystem_method()`](https://developer.wordpress.org/reference/functions/get_filesystem_method/). Wordpress tries to create a file `'wp-content/temp-write-test-'.time()`

```php
define( 'FTP_USER', 'username' );
define( 'FTP_PASS', 'password' );
define( 'FTP_HOST', 'ftp.example.org' );
```

- [Editing wp-config.php « WordPress Codex](https://codex.wordpress.org/Editing_wp-config.php#WordPress_Upgrade_Constants)
- [php - Correct file permissions for WordPress - Stack Overflow](https://stackoverflow.com/questions/18352682/correct-file-permissions-for-wordpress)
- [Changing File Permissions « WordPress Codex](https://codex.wordpress.org/Changing_File_Permissions)
- [Updating WordPress « WordPress Codex](https://codex.wordpress.org/Updating_WordPress#Automatic_Update)
- [Fix wordpress file permissions](https://gist.github.com/Adirael/3383404)
- [Wordpress asking for my FTP credentials to install plugins - Stack Overflow](https://stackoverflow.com/questions/17922644/wordpress-asking-for-my-ftp-credentials-to-install-plugins)
- [plugins - What security concerns should I have when setting FS_METHOD to "direct" in wp-config? - WordPress Development Stack Exchange](https://wordpress.stackexchange.com/questions/189554/what-security-concerns-should-i-have-when-setting-fs-method-to-direct-in-wp-co)

## Minify

- Autoptimize
- Merge + Minify + Refresh (doesn’t include an option to optimize your HTML)
- Fast Velocity Minify

- [We Tested 3 WordPress Minify Plugins: Our Results](https://themeisle.com/blog/wordpress-minify-plugins/)
- [Plugins categorized as minify | WordPress.org](https://wordpress.org/plugins/tags/minify/)

## Test

From [`westonruter/amp-wp-theme-compat-analysis/start.sh`](https://github.com/westonruter/amp-wp-theme-compat-analysis/blob/master/start.sh):

```sh
#!/bin/bash

set -x
set -e
lando start

if [ ! -e public ]; then
  mkdir public
fi

if [ ! -e public/index.php ]; then
  lando wp core download
fi

if ! lando wp core is-installed; then
  lando wp core install --url="https://amp-wp-theme-compat-analysis.lndo.site/" --title="AMP WP Theme Compatibility Analysis" --admin_user=admin --admin_password=password --admin_email=nobody@example.com
fi

lando wp plugin install --activate amp
lando wp option update --json amp-options '{"theme_support":"standard"}'

lando wp plugin install --activate wordpress-importer
lando wp plugin install --activate block-unit-test
#lando wp plugin install --activate coblocks

if [ ! -e themeunittestdata.wordpress.xml ]; then
  wget https://raw.githubusercontent.com/WPTRT/theme-unit-test/master/themeunittestdata.wordpress.xml
fi
if [[ 0 == $(lando wp menu list --format=count) ]]; then
  lando wp import --authors=create themeunittestdata.wordpress.xml
fi

if [[ 0 == $(lando wp post list --post_type=attachment --post_name=accelerated-mobile-pages-is-now-just-amp --format=count) ]]; then
  wget https://blog.amp.dev/wp-content/uploads/2019/04/only_amp.mp4
  lando wp media import --title="Accelerated Mobile Pages is now just AMP" only_amp.mp4
  rm only_amp.mp4
fi

lando wp create-monster-post
lando wp populate-initial-widgets

bash check-wporg-themes.sh 100
```

- [Theme Unit Test « WordPress Codex](https://codex.wordpress.org/Theme_Unit_Test)
- [WordPress | Lando](https://docs.lando.dev/config/wordpress.html)

## OOP

In `wp-content/themes/<themeslug>/functions.php`:

```php
<?php
class My_Theme
{
	public function __construct()
	{
		add_action('init', fn() => $this->init());
		//or add_action('init', Closure::fromCallable([$this, 'init']));
	}

	private function init()
	{
		// ...
	}
}

$my_theme = new My_Theme();
?>
```

## Code

- [WordPress/WordPress-Coding-Standards: PHP_CodeSniffer rules (sniffs) to enforce WordPress coding conventions](https://github.com/WordPress/WordPress-Coding-Standards)
