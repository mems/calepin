-[.htaccess Snippets phanan/htaccess](https://github.com/phanan/htaccess)
- https://github.com/h5bp/html5-boilerplate/blob/master/dist/.htaccess

See also [Pre compress assets, GZip - Deflate](Web#pre-compress-assets-gzip---deflate)

## Authorized access

```apache
Require all granted
```

- http://httpd.apache.org/docs/current/mod/mod_authz_core.html#require
- [ClientDeniedByServerConfiguration - Httpd Wiki](https://wiki.apache.org/httpd/ClientDeniedByServerConfiguration)

## Module identifier

- [apache 2.2 - \<IfModule\> filename vs. module id - Server Fault](http://serverfault.com/questions/401064/ifmodule-filename-vs-module-id)
- [What is the difference between apache modules with and without the ".c" extension? - Server Fault](http://serverfault.com/questions/671200/what-is-the-difference-between-apache-modules-with-and-without-the-c-extensio)
- [List of Apache modules — Wikipedia](https://en.wikipedia.org/wiki/List_of_Apache_modules)

## Smart serve image formats

Note: It's not recommended to use that way but [\<picture\>: The Picture element - HTML: Hypertext Markup Language | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture).

```apache
# Check if Accept header is image/webp, if an image is requested in "classic" folder with a classic format, and check if the corresponding webp image exists. If yes, rewrite the requested classic image URI to the WebP image URI.
RewriteCond %{HTTP_ACCEPT} image/webp
RewriteCond %{REQUEST_FILENAME} (.*)images/classic/(.*)\.(png|jpg|gif)$
RewriteCond %1images/webp/%2\.webp -f
RewriteRule .* images/webp/%2.webp [L]
```

```apache
<IfModule mod_rewrite.c>
    RewriteEngine on
    RewriteCond %{HTTP_ACCEPT} image/webp
    RewriteCond %{DOCUMENT_ROOT}/$1.webp -f
    RewriteRule (.+)\.(jpe?g|png)$ $1.webp [T=image/webp,E=accept:1]
</IfModule>

<IfModule mod_headers.c>
    Header append Vary Accept env=REDIRECT_accept
</IfModule>

AddType image/webp .webp
```

## Auto compress

```apache
# Be carefull, in Apache <= 2.2, AddOutputFilterByType was part of mod_deflate not mod_filter
<IfModule mod_filter.c>
	# Use Brotoli:
	#<IfModule mod_brotli.c>
	#	AddOutputFilterByType BROTLI_COMPRESS ...
	#</IfModule>
	<IfModule mod_deflate.c>
	AddOutputFilterByType DEFLATE \
		application/atom+xml \
		application/javascript \
		application/json \
		application/ld+json \
		application/manifest+json \
		application/rdf+xml \
		application/rss+xml \
		application/schema+json \
		application/vnd.geo+json \
		application/vnd.ms-fontobject \
		application/x-font-ttf \
		application/x-javascript \
		application/x-web-app-manifest+json \
		application/xhtml+xml \
		application/xml \
		font/eot \
		font/opentype \
		image/bmp \
		image/svg+xml \
		image/vnd.microsoft.icon \
		image/x-icon \
		text/cache-manifest \
		text/css \
		text/html \
		text/javascript \
		text/plain \
		text/vcard \
		text/vnd.rim.location.xloc \
		text/vtt \
		text/x-component \
		text/x-cross-domain-policy \
		text/xml
	</IfModule>
</IfModule>
```

```apache
DeflateCompressionLevel 9
DeflateFilterNote ratio
```

For PHP, which return `text/html` it handled with `AddOutputFilterByType`

An other version:

```apache
<IfModule mod_deflate.c>
	# Force deflate for mangled headers https://web.archive.org/web/20130209130731/http://developer.yahoo.com/blogs/ydn/posts/2010/12/pushing-beyond-gzipping/
	<IfModule mod_setenvif.c>
	<IfModule mod_headers.c>
		SetEnvIfNoCase ^(Accept-EncodXng|X-cept-Encoding|X{15}|~{15}|-{15})$ ^((gzip|deflate)\s*,?\s*)+|[X~-]{4,13}$ HAVE_Accept-Encoding
		RequestHeader append Accept-Encoding "gzip,deflate" env=HAVE_Accept-Encoding
	</IfModule>
	</IfModule>

	<IfModule version.c>
	<IfModule filter_module.c>
	<IfVersion >= 2.4>
		FilterDeclare   COMPRESS
		FilterProvider COMPRESS DEFLATE "%{CONTENT_TYPE} = 'text/html'"
		#...
		FilterChain     COMPRESS
		FilterProtocol COMPRESS DEFLATE change=yes;byteranges=no
	</IfVersion>
	<IfVersion <= 2.2>
		FilterDeclare   COMPRESS
		FilterProvider COMPRESS DEFLATE resp=Content-Type $text/html
		#...
		FilterChain     COMPRESS
		FilterProtocol  COMPRESS  DEFLATE change=yes;byteranges=no
	</IfVersion>
	</IfModule>
	</IfModule>
</IfModule>
```

- [mod_filter - Apache HTTP Server Version 2.4](http://httpd.apache.org/docs/2.4/en/mod/mod_filter.html#addoutputfilterbytype)
- [Apache AddOutputFilterByType is deprecated. How to rewrite using mod_filter? - Stack Overflow](https://stackoverflow.com/questions/5230202/apache-addoutputfilterbytype-is-deprecated-how-to-rewrite-using-mod-filter)
- https://gist.github.com/FlorianKromer/aa08762387183404a506#file-htaccess-L101-L178
- [Pushing Beyond Gzipping · YDN Blog](https://web.archive.org/web/20130209130731/http://developer.yahoo.com/blogs/ydn/posts/2010/12/pushing-beyond-gzipping/)

## Content handling

```apache
# Discard exploit.php.jpg
<FilesMatch \.php$>
	SetHandler application/x-httpd-php
	# see also fastcgi-script
</FilesMatch>
```

- [PHP: Apache 2.x on Unix systems - Manual](http://php.net/manual/en/install.unix.apache2.php)
- [mod_deflate - Apache HTTP Server Version 2.4](http://httpd.apache.org/docs/current/mod/mod_deflate.html)

## Media type

Use header `Content-type`

```apache
# Set encoding for file extensions
<IfModule mod_mime.c>
	# audio
	AddType audio/ogg oga ogg

	# video
	AddType video/ogg ogv
	AddType video/mp4 mp4
	AddType video/webm webm

	# Proper svg serving. Required for svg webfonts on iPad
	# https://twitter.com/FontSquirrel/status/14855840545
	AddType image/svg+xml svg svgz
	AddEncoding gzip svgz

	# webfonts
	AddType application/vnd.ms-fontobject eot
	AddType font/truetype ttf
	AddType font/opentype otf
	AddType font/woff woff
	AddType font/woff2 woff2

	# assorted types
	AddType image/vnd.microsoft.icon ico
	AddType image/webp webp
	AddType image/avif avif
	#AddType image/avif avif heif heifs hif
	AddType text/cache-manifest manifest
	AddType text/x-component htc
	AddType application/x-chrome-extension crx
	AddType application/x-xpinstall xpi
	AddType application/octet-stream safariextz

	AddType text/plain txt
	AddType text/markdown md markdown mdown
</IfModule>
```

See also [Media type](../Formats,%20encoding%20and%20protocols/Formats,%20encoding%20and%20protocols.md#media-type)

## Documentation and editors

http://www.htaccesseditor.com/en.shtml
http://www.thejackol.com/htaccess-cheatsheet/
http://alexking.org/blog/2007/08/30/friendly-search-urls
http://www.webrankinfo.com/analyses/autres/url-rewriting-debutants.php
http://www.sitepoint.com/article/guide-url-rewriting/4

http://httpd.apache.org/docs/2.0/mod/mod_rewrite.html

## HSTS

And redirect HTTP to HTTPS

See [HSTS](Security#http-strict-transport-security)

You should add a mecanism to redirect HTTP to HTTPS too. It's adviced to **use [VirtualHost](https://stackoverflow.com/questions/13376219/htaccess-redirect-http-to-https/13376534#13376534)**:

```apache
<IfModule mod_rewrite.c>
	# Force HTTPS
	# Inspired from https://stackoverflow.com/questions/13376219/htaccess-redirect-http-to-https/
	RewriteEngine on
	RewriteCond %{HTTPS} !on
	# Header used by proxies or load balancers (CDN):
	RewriteCond %{HTTP:X-Forwarded-Proto} !https
	# Some load balancer use other methods:
	# RewriteCond %{HTTPS} !1
	# RewriteCond %{SERVER_PORT} !443
	# RewriteCond %{HTTP:X-Forwarded-SSL} !on
	# RewriteCond %{HTTP:CF-Visitor} '"scheme":"http"'
	# RewriteCond %{ENV:HTTPS} !on
	RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
</IfModule>
```

```apache
<IfModule mod_headers.c>
	# Force HTTPS
	Header always set Strict-Transport-Security "max-age=63072000; includeSubdomains; preload"
</IfModule>
```

```apache
<IfModule mod_headers.c>
	# Force HTTPS only for www.example.com
	SetEnvIf Host "^www\.example\.com$" StrictTransportSecurity
	Header always set Strict-Transport-Security "max-age=63072000; preload" env=StrictTransportSecurity
</IfModule>
```

- [RewriteHTTPToHTTPS - Httpd Wiki](https://wiki.apache.org/httpd/RewriteHTTPToHTTPS)
- Detect how to know if it's HTTPS with PHP https://github.com/rlankhorst/really-simple-ssl/blob/master/ssl-test-page.php

## CORS

```apache
# Add CORS header for domain1.org, domain2.com and domain3.net only
<IfModule mod_headers.c>
	SetEnvIf Origin "^http(s)?://(www\.)?(domain1\.org|domain2\.com|domain3\.net)$" AccessControlAllowOrigin=$0$1
	Header add Access-Control-Allow-Origin %{AccessControlAllowOrigin}e env=AccessControlAllowOrigin
	Header set Access-Control-Allow-Credentials true
	Vary: Origin
</IfModule>
```

- [apache - .htaccess - how to set headers dynamically per domain? - Stack Overflow](https://stackoverflow.com/questions/15469482/htaccess-how-to-set-headers-dynamically-per-domain)
- [.htaccess - handle multiple domains with Access-Control-Allow-Origin header in Apache - Stack Overflow](https://stackoverflow.com/questions/20673882/handle-multiple-domains-with-access-control-allow-origin-header-in-apache)

## Rewrite / redirect

```sh
curl -Ls -w %{url_effective} -o /dev/null https://example.com/?redirect
```

```apache
# Redirect to naked domain: www.example.com to example.com
<IfModule mod_rewrite.c>
    RewriteEngine On
	RewriteCond %{HTTP_HOST} ^(.*\.)?www\.(.*)(:\d+)?$ [NC]
	RewriteRule ^ https://%2%{REQUEST_URI} [QSA,R=301,L]
</IfModule>
```

```apache
# Redirect to HTTPS
<IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteCond %{HTTPS} ^off$ [NC]
    RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [QSA,R=301,L]
</IfModule>
```

- [.htaccess - htaccess https off condition - Stack Overflow](https://stackoverflow.com/questions/15010874/htaccess-https-off-condition)

```apache
# Redirect example.com to https://www.example.com
<IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteCond %{HTTP_HOST} !^www\. [NC]
    RewriteRule ^(.*)$ https://www.%{HTTP_HOST}/$1 [R=301,L]
</IfModule>
```

- [Redirect non-www to www in .htaccess - Stack Overflow](https://stackoverflow.com/questions/12050590/redirect-non-www-to-www-in-htaccess)

```apache
<IfModule mod_rewrite.c>
	RewriteEngine on

	# Determine the RewriteBase automatically and set it as environment variable.
	# If you are using Apache aliases to do mass virtual hosting or installed the
	# project in a subdirectory, the base path will be prepended to allow proper
	# resolution of the files and to redirect to the correct URI. It will
	# work in environments without path prefix as well, providing a safe, one-size
	# fits all solution. But as you do not need it in this case, you can comment
	# the following 2 lines to eliminate the overhead.
	RewriteCond %{REQUEST_URI}::$1 ^(/.+)/(.*)::\2$
	RewriteRule ^(.*) - [E=BASE:%1]

	RewriteCond %{REQUEST_URI} !^%{ENV:BASE}/subfolder/
	RewriteRule ^(.*)$ %{ENV:BASE}/subfolder/$1 [L]
</IfModule>
```

```apache
<IfModule rewrite_module>
	RewriteEngine on

	RewriteCond %{DOCUMENT_ROOT} ^(.*)$ [NC]
	RewriteRule ^ - [E=doc_root:%1]
	# Will add an header `X-Debug` with value equal DOCUMENT_ROOT (see the syntax `%{xxxx}e`)
	Header append X-Debug "%{doc_root}e"

	# Add cookie `test` to `1`
	RewriteRule ^ - [CO=test:1:%{HTTP_HOST}]

	# Test cookie `test` == `1`
	RewriteCond %{HTTP:Cookie} \test=1(;|$)

	# Skip next RewriteRule (use 2 instead 1 to skip more, 3... or use L)
	RewriteRule ^ - [S=1]

	# Test if env var `test` equal `1`
	RewriteCond %{ENV:test} ^1$
	RewriteRule...
</IfModule>
```

From Symfony https://github.com/symfony/symfony-standard/blob/master/web/.htaccess, see also [.htaccess - What Double Colon does in RewriteCond? - Stack Overflow](https://stackoverflow.com/questions/37605218/what-double-colon-does-in-rewritecond):

```apache
# Use the front controller as index file. It serves as a fallback solution when
# every other rewrite/redirect fails (e.g. in an aliased environment without
# mod_rewrite). Additionally, this reduces the matching process for the
# start page (path "/") because otherwise Apache will apply the rewriting rules
# to each configured DirectoryIndex file (e.g. index.php, index.html, index.pl).
DirectoryIndex app.php

# By default, Apache does not evaluate symbolic links if you did not enable this
# feature in your server configuration. Uncomment the following line if you
# install assets as symlinks or if you experience problems related to symlinks
# when compiling LESS/Sass/CoffeScript assets.
# Options FollowSymlinks

# Disabling MultiViews prevents unwanted negotiation, e.g. "/app" should not resolve
# to the front controller "/app.php" but be rewritten to "/app.php/app".
<IfModule mod_negotiation.c>
    Options -MultiViews
</IfModule>

<IfModule mod_rewrite.c>
    RewriteEngine on

    # Determine the RewriteBase automatically and set it as environment variable.
    # If you are using Apache aliases to do mass virtual hosting or installed the
    # project in a subdirectory, the base path will be prepended to allow proper
    # resolution of the app.php file and to redirect to the correct URI. It will
    # work in environments without path prefix as well, providing a safe, one-size
    # fits all solution. But as you do not need it in this case, you can comment
    # the following 2 lines to eliminate the overhead.
    RewriteCond %{REQUEST_URI}::$1 ^(/.+)/(.*)::\2$
    RewriteRule ^(.*) - [E=BASE:%1]

    # Sets the HTTP_AUTHORIZATION header removed by Apache
    RewriteCond %{HTTP:Authorization} .
    RewriteRule ^ - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]

    # Redirect to URI without front controller to prevent duplicate content
    # (with and without `/app.php`). Only do this redirect on the initial
    # rewrite by Apache and not on subsequent cycles. Otherwise we would get an
    # endless redirect loop (request -> rewrite to front controller ->
    # redirect -> request -> ...).
    # So in case you get a "too many redirects" error or you always get redirected
    # to the start page because your Apache does not expose the REDIRECT_STATUS
    # environment variable, you have 2 choices:
    # - disable this feature by commenting the following 2 lines or
    # - use Apache >= 2.3.9 and replace all L flags by END flags and remove the
    #   following RewriteCond (best solution)
    RewriteCond %{ENV:REDIRECT_STATUS} ^$
    RewriteRule ^app\.php(?:/(.*)|$) %{ENV:BASE}/$1 [R=301,L]

	## Not part of Symfony
	# Ignore /admin/ and /mobile/ subfolders
	# https://stackoverflow.com/a/24319167/470117
	RewriteCond "%{ENV:BASE}/admin/ %{REQUEST_URI}" "(^[^ ]*) \1" [OR]
	RewriteCond "%{ENV:BASE}/mobile/ %{REQUEST_URI}" "(^[^ ]*) \1"
	RewriteRule ^ - [L]
	## /Not part of Symfony

    # If the requested filename exists, simply serve it.
    # We only want to let Apache serve files and not directories.
    RewriteCond %{REQUEST_FILENAME} -f
    RewriteRule ^ - [L]

    # Rewrite all other queries to the front controller.
    RewriteRule ^ %{ENV:BASE}/app.php [L]
</IfModule>

<IfModule !mod_rewrite.c>
    <IfModule mod_alias.c>
        # When mod_rewrite is not available, we instruct a temporary redirect of
        # the start page to the front controller explicitly so that the website
        # and the generated links can still be used.
        RedirectMatch 302 ^/$ /app.php/
        # RedirectTemp cannot be used instead
    </IfModule>
</IfModule>
```

and use [Base](./PHP/PHP.md#base-path)

```apache
# http://mydomain/seach/a10/b30/c9/f99 -> http://mydomain/myscript.php?param_a=10&param_b=30&param_c_new=9&param_f=99
RewriteRule ^/seach/(.*) /myscript.php/$1
```

```apache
RewriteRule ^/myscript.php/([a-z])([0-9]+)/(.*) /myscript.php/$3?param_$1=$2 [QSA,N]
RewriteRule ^/myscript.php/([a-z])([0-9]+)$ /myscript.php?param_$1=$2 [QSA,L]
```

```apache
///WAP-redirect, based upon accepted file type
RewriteCond %{HTTP_ACCEPT} (x-)*(application|text)/(x-)*(vnd[-.])*(wap[-.]|wml)+
RewriteRule ^(index.html)*$ index.wml [L]
```

```apache
# http://www.mysite.com/keyword/j1_1/j2_2/j3_3/j4_4/j5_5/j6_6/j7_7/... -> http://www.mysite.com/index.php?j1=1&j2=2&j4=4&j5=5&j7=7...
# http://www.mysite.com/keyword/j2_2/j3_3/j4_4/j5_5/j6_6/j7_7/... -> http://www.mysite.com/index.php?j2=2&j4=4&j5=5&j7=7...
# Skip following section if not a "keyword/" request
rewriterule !^keyword/ - [S=9]
#
# Else copy/append keywords to user-defined variable "tQuery"
rewriterule ^keyword(/[^/]+)*/j1_([^/]+) - [NC,E=tQuery:%{ENV:tQuery}j1=$2]
rewriterule ^keyword(/[^/]+)*/j2_([^/]+) - [NC,E=tQuery:%{ENV:tQuery}&j2=$2]
rewriterule ^keyword(/[^/]+)*/j3_([^/]+) - [NC,E=tQuery:%{ENV:tQuery}&j3=$2]
rewriterule ^keyword(/[^/]+)*/j4_([^/]+) - [NC,E=tQuery:%{ENV:tQuery}&j4=$2]
rewriterule ^keyword(/[^/]+)*/j5_([^/]+) - [NC,E=tQuery:%{ENV:tQuery}&j5=$2]
rewriterule ^keyword(/[^/]+)*/j6_([^/]+) - [NC,E=tQuery:%{ENV:tQuery}&j6=$2]
rewriterule ^keyword(/[^/]+)*/j7_([^/]+) - [NC,E=tQuery:%{ENV:tQuery}&j7=$2]
#
# Strip leading "&" from tQuery (if any)
RewriteCond %{ENV:tQuery} ^&(.+)$
rewriterule ^keyword/ - [NC,E=tQuery:%1]
# Tweaked to look for city name (if any)
rewriterule ^keyword(_[^/]+)? - [NC,E=tQuery:%1]
# Rewrite the URL-path to index.php query format
# Tweaked to look for city name (if any)
rewriterule ^keyword(_[^/]+)? /index.php?%{ENV:tQuery} [NC,L]
```

```apache
# http://mysite.com/keyword/test/page2 -> http://mysite.com/data.php?method=keyword&criteria=test&page=2
# http://mysite.com/date/06-05-02 -> http://mysite.com/data.php?method=keyword&criteria=06-05-02
# Skip following section if not a "keyword/" request
rewriterule !^(keyword|date|category) - [skip=4]
# Else copy/append keywords to user-defined variable "tmpQuery"
RewriteRule ^(keyword|date|category).*$ - [env=tmpQuery:%{ENV:tmpQuery}method=$1]
RewriteRule ^(keyword|date|category)/([^/]*).*$ - [env=tmpQuery:%{ENV:tmpQuery}&criteria=$2]
RewriteRule ^(keyword|date|category)/([^/]*)/page(\d+).*$ - [env=tmpQuery:%{ENV:tmpQuery}&page=$3]
# Rewrite the URL-path to data.php query format
rewriterule ^(keyword|date|category).* /data.php?%{ENV:tmpQuery} [last]
# http://www.dracos.co.uk/code/apache-rewrite-problem/
```

```apache
/// Rewrite by accept language given by client
RewriteEngine on
RewriteCond %{HTTP:Accept-Language} (sv) [NC]
RewriteRule .* http://www.sverige.hms-solutions.com [R,L]
RewriteCond %{HTTP:Accept-Language} (nn) [NC]
RewriteRule .* http://www.norge.hms-solutions.com [R,L]
RewriteCond %{HTTP:Accept-Language} (da) [NC]
RewriteRule .* http://www.danmark.hms-solutions.com [R,L]
RewriteCond %{HTTP:Accept-Language} (en) [NC]
RewriteRule .* http://www.english.hms-solutions.com [R,L]
RewriteCond %{HTTP:Accept-Language} .* [NC]
RewriteRule .* http://www.international.hms-solutions.com [R,L]
```

```apache
// Feed redirect
RewriteCond %{THE_REQUEST} ^[A-Z]{3,9}\ /(feed|wp-atom|wp-feed|wp-rss|wp-rdf|wp-commentsrss)(.*)\ HTTP/ [NC,OR]
RewriteCond %{QUERY_STRING} ^feed [NC]
RewriteCond %{HTTP_USER_AGENT} !^(FeedBurner|FeedValidator|talkr) [NC]
RewriteRule .* http://feeds.askapache.com/apache/htaccess? [R=307,L]
```

```apache
# In the .htaccess
<IfModule mod_alias.c>
	# Use status "gone" for 410 (HTTP status)
	# Note: if you need to match query string, use mod_rewrite instead.
	# See https://web.archive.org/web/20220820210007/https://simonecarletti.com/blog/2009/01/apache-query-string-redirects/
	Redirect gone /a
	Redirect gone /b
	RedirectMatch gone \.gif$
</IfModule>
```

- `RewriteMap`
    - [mod_rewrite - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/current/en/mod/mod_rewrite.html#rewritemap)
    - [Using RewriteMap - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/current/en/rewrite/rewritemap.html)
- [mod_rewrite - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/current/en/mod/mod_rewrite.html)
- [Logging - mod_rewrite - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/current/en/mod/mod_rewrite.html#logging) Debug `LogLevel rewrite:trace8`
- [mod rewrite - mod_rewrite not sending Vary: accept-language when RewriteCond matches - Stack Overflow](https://stackoverflow.com/questions/3698363/mod-rewrite-not-sending-vary-accept-language-when-rewritecond-matches) - "header name will not be added to the `Vary` response header if it is not sent by the client."
- [mod rewrite - how to use "AND", "OR" for RewriteCond on Apache? - Stack Overflow](https://stackoverflow.com/questions/922399/how-to-use-and-or-for-rewritecond-on-apache/31572003#31572003)
- [mod_alias - Apache HTTP Server Version 2.2](https://httpd.apache.org/docs/2.2/mod/mod_alias.html#redirect)

## Cookies

Set cookie

```apache
# This code sends the Set-Cookie header to create a cookie on the client with the value of a matching item in 2nd parantheses.
RewriteRule ^(.*)(de|es|fr|it|ja|ru|en)/$ - [co=lang:$2:.askapache.com:7200:/]
```

Get cookie

```apache
RewriteCond %{HTTP_COOKIE} lang=([^;]+) [NC]
RewriteRule ^(.*)$ /$1?cookie-value=%1 [R,QSA,L]
```

Rewirte base on cookie

```apache
RewriteCond %{HTTP_COOKIE} lang=([^;]+) [NC]
RewriteRule ^(.*)$ /$1?lang=%1 [NC,L,QSA]
```

Redirect if cookie not set

```apache
RewriteCond %{HTTP_COOKIE}!^.*cookie-name.*$ [NC]
RewriteRule .* /login-error/set-cookie-first.cgi [NC,L]
```

## Environnement variables

- [Apache: Environment Variables Visibility with SetEnv, SetEnvIf and RewriteRule Directives | TurboFlash](https://web.archive.org/web/20180820235431/http://www.onlinesmartketer.com/2010/05/27/apache-environment-variables-visibility-with-setenv-setenvif-and-rewriterule-directives/)
- [php - When setting environment variables in Apache RewriteRule directives, what causes the variable name to be prefixed with "REDIRECT_"? - Stack Overflow](https://stackoverflow.com/questions/3050444/when-setting-environment-variables-in-apache-rewriterule-directives-what-causes)

### Pass variable to script

Pass env variable to PHP, should start with `HTTP_`, eg. `$_SERVER['HTTP_MY_VARIABLE']`:

```apache
SetEnv MY_VARIABLE "my value"
```

Or use query param

```apache
RewriteRule ^(.*) index.php?cur_url=/$1&my_variable=my+value?%{QUERY_STRING}
```

## Echo all header back

```apache
Header echo ^.*
```

## Caching

```apache
<IfModule mod_expires.c>
ExpiresActive on

# Perhaps better to allowlist expires rules? Perhaps.
ExpiresDefault                          "access plus 1 month"

# cache.appcache needs re-requests in FF 3.6 (thanks Remy ~Introducing HTML5)
ExpiresByType text/cache-manifest       "access plus 0 seconds"

# Your document html
ExpiresByType text/html                 "access plus 0 seconds"

# CSS and JavaScript
ExpiresByType text/css                  "access plus 1 year"
ExpiresByType text/javascript           "access plus 1 year"

# Data
ExpiresByType text/xml                  "access plus 0 seconds"
ExpiresByType application/xml           "access plus 0 seconds"
ExpiresByType application/json          "access plus 0 seconds"
ExpiresByType application/ld+json       "access plus 0 seconds"
ExpiresByType application/vnd.geo+json  "access plus 0 seconds"

# Feed
ExpiresByType application/rss+xml       "access plus 1 hour"
ExpiresByType application/atom+xml      "access plus 1 hour"

# Favicon (cannot be renamed)
ExpiresByType image/x-icon              "access plus 1 week"

# Manifest files
ExpiresByType application/manifest+json             "access plus 1 year"
ExpiresByType application/x-web-app-manifest+json   "access plus 0 seconds"
ExpiresByType text/cache-manifest                   "access plus 0 seconds"

# Media: images, video, audio
ExpiresByType image/gif                             "access plus 1 month"
ExpiresByType image/png                             "access plus 1 month"
ExpiresByType image/jpg                             "access plus 1 month"
ExpiresByType image/jpeg                            "access plus 1 month"
ExpiresByType video/ogg                             "access plus 1 month"
ExpiresByType audio/ogg                             "access plus 1 month"
ExpiresByType video/mp4                             "access plus 1 month"
ExpiresByType video/webm                            "access plus 1 month"

# Webfonts
ExpiresByType application/font-woff                 "access plus 1 month"
ExpiresByType application/font-woff2                "access plus 1 month"
ExpiresByType application/vnd.ms-fontobject         "access plus 1 month"
ExpiresByType application/x-font-ttf                "access plus 1 month"
ExpiresByType font/opentype                         "access plus 1 month"
ExpiresByType image/svg+xml                         "access plus 1 month"
</IfModule>
```

```apache
# 1 YEAR
<FilesMatch "\.(ico|pdf|flv)$">
Header set Cache-Control "max-age=29030400, public"
</FilesMatch>
# 1 WEEK
<FilesMatch "\.(jpg|jpeg|png|gif|swf)$">
Header set Cache-Control "max-age=604800, public"
</FilesMatch>
# 2 DAYS
<FilesMatch "\.(xml|txt|css|js)$">
Header set Cache-Control "max-age=172800, proxy-revalidate"
</FilesMatch>
# 1 MIN
<FilesMatch "\.(html|htm|php)$">
Header set Cache-Control "max-age=60, private, proxy-revalidate"
</FilesMatch>
```

ETag removal

```apache
# FileETag None is not enough for every server.
<IfModule mod_headers.c>
  Header unset ETag
</IfModule>

# Since we're sending far-future expires, we don't need ETags for
# static content.
#   developer.yahoo.com/performance/rules.html#etags
FileETag None
```

- https://gist.github.com/FlorianKromer/aa08762387183404a506#file-htaccess-L180-L241

## Serve pre-encoded resources

Aka serve precompressed files

> This limitation of `mod_deflate` is prominently mentioned in the documentation, [which recommends](https://httpd.apache.org/docs/2.4/mod/mod_deflate.html#precompressed) using [`mod_rewrite`](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html) to rewrite requests to their compressed alternatives when appropriate. Although this method can work [...] it has the major drawback that you are reimplementing content negotiation (which [`mod_negotiation`](https://httpd.apache.org/docs/2.4/mod/mod_negotiation.html) was designed to do) and are likely to get it wrong and lack features supported by `mod_negotiation`. Some common problems and pitfalls with this approach:
> - Sending an incorrect or missing `Content-Encoding` header.
> - Not sending the `Vary` header or setting it incorrectly (overwriting previous values for other headers which cause the response to vary).
> - Sending `Content-Type: application/x-gzip` instead of the underlying type.
> - Sending double-gzipped content due to forgetting to set `no-gzip` in the environment to exclude the response from `mod_deflate`.
> - Not respecting client preferences (i.e. quality values/qvalues). According to [RFC 7231](https://tools.ietf.org/html/rfc7231#section-5.3.4) (and [RFC 2616](https://tools.ietf.org/html/rfc2616#section-14.3) before it) clients can send a numeric value between 0 and 1 (inclusive) to express their relative preference for each encoding. An `Accept-Encoding: gzip;q=0` header would signify that the client wants “anything but gzip”. Most `mod_rewrite` implementations would send them gzip. A more realistic example would be a client that sends `Accept-Encoding: br;q=1, gzip;q=0.5, deflate;q=0.1` to signify that they prefer Brotli, then gzip, then deflate. Writing `mod_rewrite` rules which properly handle these sorts of expressed preferences is extremely difficult.
>
> - [Serving Pre-Compressed Files with Apache MultiViews - Kevin Locke's Homepage](https://web.archive.org/web/20200829235117/https://kevinlocke.name/bits/2016/01/20/serving-pre-compressed-files-with-apache-multiviews/#non-multiviews-methods)

- Serving pre-compressed content [mod_deflate - Apache HTTP Server Version 2.4](http://httpd.apache.org/docs/current/en/mod/mod_deflate.html#precompressed)
- [Getting more out of GZIP for web content](http://mainroach.blogspot.fr/2013/09/getting-more-out-of-gzip-for-web-content.html)
- [Code Grill: How To Serve Pre-Compressed Static Files in Apache](http://blog.codegrill.org/2009/07/how-to-pre-compress-static-files-in.html)
- [caching - How to force Apache to use manually pre-compressed gz file of CSS and JS files? - Stack Overflow](https://stackoverflow.com/questions/9076752/how-to-force-apache-to-use-manually-pre-compressed-gz-file-of-css-and-js-files)
- [javascript - How to host static content pre-compressed in apache? - Stack Overflow](https://stackoverflow.com/questions/16883241/how-to-host-static-content-pre-compressed-in-apache)
- [Simple gzip Support for Apache with mod_rewrite - CraveDIY](http://www.cravediy.com/59-simple-gzip-support-for-apache-with-mod_rewrite.html)
- [apache - How to configure mod_deflate to serve gzipped assets prepared with assets:precompile - Stack Overflow](https://stackoverflow.com/questions/7509501/how-to-configure-mod-deflate-to-serve-gzipped-assets-prepared-with-assetsprecom)
- [Gzip Your CSS and JavaScript | ODLAN](http://odlan.com/gzip-your-css-and-js/)
- [Optimizing Mendix for low bandwidth - Using Compression](https://forum.mendixcloud.com/link/questions/3475)
- [Simple gzip Support for Apache with mod_rewrite - CraveDIY](http://www.cravediy.com/59-Simple-gzip-Support-for-Apache-with-mod_rewrite.html)
- [http - How can I pre-compress files with mod_deflate in Apache 2.x? - Stack Overflow](https://stackoverflow.com/questions/75482/how-can-i-pre-compress-files-with-mod-deflate-in-apache-2-x)
- [w3-total-cache-fixed/Minify_Environment.php at d7c4e8f9648f6dde232430feec27d241359761f1 · szepeviktor/w3-total-cache-fixed](https://github.com/szepeviktor/w3-total-cache-fixed/blob/d7c4e8f9648f6dde232430feec27d241359761f1/Minify_Environment.php#L395-L398)
- [Serving Pre-Compressed Files with Apache MultiViews - Kevin Locke's Homepage](https://kevinlocke.name/bits/2016/01/20/serving-pre-compressed-files-with-apache-multiviews/)

### Serve pre-encoded resources with `mod_rewrite`

- [`mod_rewrite`](https://httpd.apache.org/docs/current/en/mod/mod_rewrite.html)

```apache
# If the browser accepts gzip/br and the requested file exists under pre-encoded version, then serve that version directly.
<IfModule mod_rewrite.c>
	<IfModule mod_headers.c>
		# Brotli
		<IfModule mod_brotli.c>
			RewriteEngine On
			RewriteCond %{HTTP:Accept-Encoding} br
			RewriteCond %{REQUEST_FILENAME}.br -f
			RewriteRule (.*) $1.br [L,E=no-brotli:1,E=PRE_ENCODED_CODING:br]
		</IfModule>

		# Deflate / Gzip
		<IfModule mod_deflate.c>
			RewriteEngine On

			RewriteCond %{HTTP:Accept-Encoding} gzip
			RewriteCond %{REQUEST_FILENAME}.gz -f
			RewriteRule (.*) $1.gz [L,E=no-gzip:1,E=PRE_ENCODED_CODING:gzip]

			# Special case for *.svg -> *.svgz
			RewriteCond %{HTTP:Accept-Encoding} gzip
			RewriteCond %{REQUEST_FILENAME} .svg$
			RewriteCond %{REQUEST_FILENAME}z -f
			RewriteRule (.*) $1z [L,E=no-gzip:1,E=PRE_ENCODED_CODING:gzip]
		</IfModule>

		# Special case for internal redirection (pre encoded) response only
		# For "REDIRECT_" env var prefix see https://stackoverflow.com/questions/3050444
		# Some directives support env vars conditions (Header does, but RemoveType doesn't)
		<If "-n env('REDIRECT_PRE_ENCODED_CODING')">
			# Debian (and related distributions) set AddType application/x-gzip gz in their default conf (/etc/apache2/mods-available/mime.conf)
			# or you the Content-Type will be override to application/x-gzip
			RemoveType gz
			Header always set Content-Encoding %{REDIRECT_PRE_ENCODED_CODING}e
			# Apache already append Accept-Encoding to Vary http://httpd.apache.org/docs/current/mod/mod_rewrite.html#rewritecond
		</If>
	</IfModule>
</IfModule>
```

## Serve pre-encoded resources with `MultiViews`

- `MultiViews` comes from [`mod_negotiation`](https://httpd.apache.org/docs/current/mod/mod_negotiation.html)

To handle content encoding.

`MultiViews` allow to list all files (recognized by [`mod_mime`](https://httpd.apache.org/docs/current/mod/mod_mime.html#multiviewsmatch)) in the same folder for the given name:

```console
> curl --header "Accept: example/*; q=1.0" -s -D - -o /dev/null https://example.com/test
HTTP/1.1 406 Not Acceptable
Date: Sat, 19 Sep 2020 18:36:20 GMT
Server: Apache/2.4.38 (Debian)
Alternates: {"test.html" 1 {type text/html} {length 13}}, {"test.html.gz" 1 {type text/html} {encoding gzip} {length 38}}, {"test.php" 1 {type application/x-httpd-php} {length 59}}
Vary: negotiate,accept,accept-encoding

```

You need to restrict content negotiation by include directives in [a `<Directory>`, `<Files>` or `.htaccess`](https://httpd.apache.org/docs/current/sections.html) for a subset of directories, file types.

The major drawback, [only requests for files which do not exist are negotiated](https://httpd.apache.org/docs/current/mod/mod_negotiation.html#multiviews). That means you need to rename uncompressed files for an additional extension (ex: `index.html.html` and `index.html.gz` for `https://example.com/index.html`) which is not pratical.

```apache
# Let Apache choose media type, encoding, etc. based on client preferences.
# Need rewrite to force use pre encoded version because MultiViews only negotiates requests for files which do not exist.
<IfModule mod_mime.c>
	<IfModule mod_rewrite.c>
		# Brotli
		<IfModule mod_brotli.c>
			Options +MultiViews
			RewriteEngine On

			# Note: BR is a RFC 3066 language
			RemoveLanguage br
			AddEncoding br br
		</IfModule>

		# Deflate / Gzip
		<IfModule mod_deflate.c>
			Options +MultiViews
			RewriteEngine On

			# Case for * -> *.gz
			# Debian (and related distributions) set AddType application/x-gzip gz in their default conf (/etc/apache2/mods-available/mime.conf)
			RemoveType .gz
			AddEncoding gzip gz

			# Case for *.svg -> .svgz
			AddEncoding gzip svgz
		</IfModule>
	</IfModule>
</IfModule>
```

- [http - How can I pre-compress files with mod_deflate in Apache 2.x? - Stack Overflow](https://stackoverflow.com/questions/75482/how-can-i-pre-compress-files-with-mod-deflate-in-apache-2-x/34932031#34932031)

### Precompressed files and type maps

- `type maps` comes from [`mod_negotiation`](https://httpd.apache.org/docs/current/mod/mod_negotiation.html#typemaps)

```apache
# Treat not as application/gzip type
RemoveType .gz
# Handle type maps
AddHandler type-map .var

RewriteCond %{REQUEST_FILENAME}.var -f
RewriteRule (.*) $1.var [QSA]
```

Exemple, for `test.html` `test.html.gz` and `test.html.br`, create a file `test.var`, for a request `/test`
```
URI: test

Content-type: text/html; qs=0.7
Content-Encoding: gzip
URI: index.html.gz

Content-type: text/html; qs=0.8
Content-Encoding: br
URI: index.html.br
```

- [50848 – Content Negotiation type map file precedence could be clarified](https://bz.apache.org/bugzilla/show_bug.cgi?id=50848)
- [Apache HTTP encoding negotiation notes | mrclay.org](https://web.archive.org/web/20161009225339/http://www.mrclay.org/2008/05/25/apache-http-encoding-negotiation-notes/)
- [Pre-encoding vs. mod_deflate | mrclay.org](https://web.archive.org/web/20161010115837/http://www.mrclay.org/2008/06/03/pre-encoding-vs-mod_deflate/)

## Variables

`.htaccess`:

```apache
RewriteEngine on
RewriteBase /
RewriteRule .* - [E=INFO_API_VERSION:%{API_VERSION},NE]
RewriteRule .* - [E=INFO_AUTH_TYPE:%{AUTH_TYPE},NE]
RewriteRule .* - [E=INFO_CONTENT_LENGTH:%{CONTENT_LENGTH},NE]
RewriteRule .* - [E=INFO_CONTENT_TYPE:%{CONTENT_TYPE},NE]
RewriteRule .* - [E=INFO_DOCUMENT_ROOT:%{DOCUMENT_ROOT},NE]
RewriteRule .* - [E=INFO_GATEWAY_INTERFACE:%{GATEWAY_INTERFACE},NE]
RewriteRule .* - [E=INFO_HTTPS:%{HTTPS},NE]
RewriteRule .* - [E=INFO_HTTP_ACCEPT:%{HTTP_ACCEPT},NE]
RewriteRule .* - [E=INFO_HTTP_ACCEPT_CHARSET:%{HTTP_ACCEPT_CHARSET},NE]
RewriteRule .* - [E=INFO_HTTP_ACCEPT_ENCODING:%{HTTP_ACCEPT_ENCODING},NE]
RewriteRule .* - [E=INFO_HTTP_ACCEPT_LANGUAGE:%{HTTP_ACCEPT_LANGUAGE},NE]
RewriteRule .* - [E=INFO_HTTP_CACHE_CONTROL:%{HTTP_CACHE_CONTROL},NE]
RewriteRule .* - [E=INFO_HTTP_CONNECTION:%{HTTP_CONNECTION},NE]
RewriteRule .* - [E=INFO_HTTP_COOKIE:%{HTTP_COOKIE},NE]
RewriteRule .* - [E=INFO_HTTP_FORWARDED:%{HTTP_FORWARDED},NE]
RewriteRule .* - [E=INFO_HTTP_HOST:%{HTTP_HOST},NE]
RewriteRule .* - [E=INFO_HTTP_KEEP_ALIVE:%{HTTP_KEEP_ALIVE},NE]
RewriteRule .* - [E=INFO_HTTP_MOD_SECURITY_MESSAGE:%{HTTP_MOD_SECURITY_MESSAGE},NE]
RewriteRule .* - [E=INFO_HTTP_PROXY_CONNECTION:%{HTTP_PROXY_CONNECTION},NE]
RewriteRule .* - [E=INFO_HTTP_REFERER:%{HTTP_REFERER},NE]
RewriteRule .* - [E=INFO_HTTP_USER_AGENT:%{HTTP_USER_AGENT},NE]
RewriteRule .* - [E=INFO_IS_SUBREQ:%{IS_SUBREQ},NE]
RewriteRule .* - [E=INFO_ORIG_PATH_INFO:%{ORIG_PATH_INFO},NE]
RewriteRule .* - [E=INFO_ORIG_PATH_TRANSLATED:%{ORIG_PATH_TRANSLATED},NE]
RewriteRule .* - [E=INFO_ORIG_SCRIPT_FILENAME:%{ORIG_SCRIPT_FILENAME},NE]
RewriteRule .* - [E=INFO_ORIG_SCRIPT_NAME:%{ORIG_SCRIPT_NAME},NE]
RewriteRule .* - [E=INFO_PATH:%{PATH},NE]
RewriteRule .* - [E=INFO_PATH_INFO:%{PATH_INFO},NE]
RewriteRule .* - [E=INFO_PHP_SELF:%{PHP_SELF},NE]
RewriteRule .* - [E=INFO_QUERY_STRING:%{QUERY_STRING},NE]
RewriteRule .* - [E=INFO_REDIRECT_QUERY_STRING:%{REDIRECT_QUERY_STRING},NE]
RewriteRule .* - [E=INFO_REDIRECT_REMOTE_USER:%{REDIRECT_REMOTE_USER},NE]
RewriteRule .* - [E=INFO_REDIRECT_STATUS:%{REDIRECT_STATUS},NE]
RewriteRule .* - [E=INFO_REDIRECT_URL:%{REDIRECT_URL},NE]
RewriteRule .* - [E=INFO_REMOTE_ADDR:%{REMOTE_ADDR},NE]
RewriteRule .* - [E=INFO_REMOTE_HOST:%{REMOTE_HOST},NE]
RewriteRule .* - [E=INFO_REMOTE_IDENT:%{REMOTE_IDENT},NE]
RewriteRule .* - [E=INFO_REMOTE_PORT:%{REMOTE_PORT},NE]
RewriteRule .* - [E=INFO_REMOTE_USER:%{REMOTE_USER},NE]
RewriteRule .* - [E=INFO_REQUEST_FILENAME:%{REQUEST_FILENAME},NE]
RewriteRule .* - [E=INFO_REQUEST_METHOD:%{REQUEST_METHOD},NE]
RewriteRule .* - [E=INFO_REQUEST_TIME:%{REQUEST_TIME},NE]
RewriteRule .* - [E=INFO_REQUEST_URI:%{REQUEST_URI},NE]
RewriteRule .* - [E=INFO_SCRIPT_FILENAME:%{SCRIPT_FILENAME},NE]
RewriteRule .* - [E=INFO_SCRIPT_GROUP:%{SCRIPT_GROUP},NE]
RewriteRule .* - [E=INFO_SCRIPT_NAME:%{SCRIPT_NAME},NE]
RewriteRule .* - [E=INFO_SCRIPT_URI:%{SCRIPT_URI},NE]
RewriteRule .* - [E=INFO_SCRIPT_URL:%{SCRIPT_URL},NE]
RewriteRule .* - [E=INFO_SCRIPT_USER:%{SCRIPT_USER},NE]
RewriteRule .* - [E=INFO_SERVER_ADDR:%{SERVER_ADDR},NE]
RewriteRule .* - [E=INFO_SERVER_ADMIN:%{SERVER_ADMIN},NE]
RewriteRule .* - [E=INFO_SERVER_NAME:%{SERVER_NAME},NE]
RewriteRule .* - [E=INFO_SERVER_PORT:%{SERVER_PORT},NE]
RewriteRule .* - [E=INFO_SERVER_PROTOCOL:%{SERVER_PROTOCOL},NE]
RewriteRule .* - [E=INFO_SERVER_SIGNATURE:%{SERVER_SIGNATURE},NE]
RewriteRule .* - [E=INFO_SERVER_SOFTWARE:%{SERVER_SOFTWARE},NE]
RewriteRule .* - [E=INFO_THE_REQUEST:%{THE_REQUEST},NE]
RewriteRule .* - [E=INFO_TIME:%{TIME},NE]
RewriteRule .* - [E=INFO_TIME_DAY:%{TIME_DAY},NE]
RewriteRule .* - [E=INFO_TIME_HOUR:%{TIME_HOUR},NE]
RewriteRule .* - [E=INFO_TIME_MIN:%{TIME_MIN},NE]
RewriteRule .* - [E=INFO_TIME_MON:%{TIME_MON},NE]
RewriteRule .* - [E=INFO_TIME_SEC:%{TIME_SEC},NE]
RewriteRule .* - [E=INFO_TIME_WDAY:%{TIME_WDAY},NE]
RewriteRule .* - [E=INFO_TIME_YEAR:%{TIME_YEAR},NE]
RewriteRule .* - [E=INFO_TZ:%{TZ},NE]
RewriteRule .* - [E=INFO_UNIQUE_ID:%{UNIQUE_ID},NE]
RequestHeader set INFO_API_VERSION "%{INFO_API_VERSION}e"
RequestHeader set INFO_AUTH_TYPE "%{INFO_AUTH_TYPE}e"
RequestHeader set INFO_CONTENT_LENGTH "%{INFO_CONTENT_LENGTH}e"
RequestHeader set INFO_CONTENT_TYPE "%{INFO_CONTENT_TYPE}e"
RequestHeader set INFO_DOCUMENT_ROOT "%{INFO_DOCUMENT_ROOT}e"
RequestHeader set INFO_GATEWAY_INTERFACE "%{INFO_GATEWAY_INTERFACE}e"
RequestHeader set INFO_HTTPS "%{INFO_HTTPS}e"
RequestHeader set INFO_HTTP_ACCEPT "%{INFO_HTTP_ACCEPT}e"
RequestHeader set INFO_HTTP_ACCEPT_CHARSET "%{INFO_HTTP_ACCEPT_CHARSET}e"
RequestHeader set INFO_HTTP_ACCEPT_ENCODING "%{INFO_HTTP_ACCEPT_ENCODING}e"
RequestHeader set INFO_HTTP_ACCEPT_LANGUAGE "%{INFO_HTTP_ACCEPT_LANGUAGE}e"
RequestHeader set INFO_HTTP_CACHE_CONTROL "%{INFO_HTTP_CACHE_CONTROL}e"
RequestHeader set INFO_HTTP_CONNECTION "%{INFO_HTTP_CONNECTION}e"
RequestHeader set INFO_HTTP_COOKIE "%{INFO_HTTP_COOKIE}e"
RequestHeader set INFO_HTTP_FORWARDED "%{INFO_HTTP_FORWARDED}e"
RequestHeader set INFO_HTTP_HOST "%{INFO_HTTP_HOST}e"
RequestHeader set INFO_HTTP_KEEP_ALIVE "%{INFO_HTTP_KEEP_ALIVE}e"
RequestHeader set INFO_HTTP_MOD_SECURITY_MESSAGE "%{INFO_HTTP_MOD_SECURITY_MESSAGE}e"
RequestHeader set INFO_HTTP_PROXY_CONNECTION "%{INFO_HTTP_PROXY_CONNECTION}e"
RequestHeader set INFO_HTTP_REFERER "%{INFO_HTTP_REFERER}e"
RequestHeader set INFO_HTTP_USER_AGENT "%{INFO_HTTP_USER_AGENT}e"
RequestHeader set INFO_IS_SUBREQ "%{INFO_IS_SUBREQ}e"
RequestHeader set INFO_ORIG_PATH_INFO "%{INFO_ORIG_PATH_INFO}e"
RequestHeader set INFO_ORIG_PATH_TRANSLATED "%{INFO_ORIG_PATH_TRANSLATED}e"
RequestHeader set INFO_ORIG_SCRIPT_FILENAME "%{INFO_ORIG_SCRIPT_FILENAME}e"
RequestHeader set INFO_ORIG_SCRIPT_NAME "%{INFO_ORIG_SCRIPT_NAME}e"
RequestHeader set INFO_PATH "%{INFO_PATH}e"
RequestHeader set INFO_PATH_INFO "%{INFO_PATH_INFO}e"
RequestHeader set INFO_PHP_SELF "%{INFO_PHP_SELF}e"
RequestHeader set INFO_QUERY_STRING "%{INFO_QUERY_STRING}e"
RequestHeader set INFO_REDIRECT_QUERY_STRING "%{INFO_REDIRECT_QUERY_STRING}e"
RequestHeader set INFO_REDIRECT_REMOTE_USER "%{INFO_REDIRECT_REMOTE_USER}e"
RequestHeader set INFO_REDIRECT_STATUS "%{INFO_REDIRECT_STATUS}e"
RequestHeader set INFO_REDIRECT_URL "%{INFO_REDIRECT_URL}e"
RequestHeader set INFO_REMOTE_ADDR "%{INFO_REMOTE_ADDR}e"
RequestHeader set INFO_REMOTE_HOST "%{INFO_REMOTE_HOST}e"
RequestHeader set INFO_REMOTE_IDENT "%{INFO_REMOTE_IDENT}e"
RequestHeader set INFO_REMOTE_PORT "%{INFO_REMOTE_PORT}e"
RequestHeader set INFO_REMOTE_USER "%{INFO_REMOTE_USER}e"
RequestHeader set INFO_REQUEST_FILENAME "%{INFO_REQUEST_FILENAME}e"
RequestHeader set INFO_REQUEST_METHOD "%{INFO_REQUEST_METHOD}e"
RequestHeader set INFO_REQUEST_TIME "%{INFO_REQUEST_TIME}e"
RequestHeader set INFO_REQUEST_URI "%{INFO_REQUEST_URI}e"
RequestHeader set INFO_SCRIPT_FILENAME "%{INFO_SCRIPT_FILENAME}e"
RequestHeader set INFO_SCRIPT_GROUP "%{INFO_SCRIPT_GROUP}e"
RequestHeader set INFO_SCRIPT_NAME "%{INFO_SCRIPT_NAME}e"
RequestHeader set INFO_SCRIPT_URI "%{INFO_SCRIPT_URI}e"
RequestHeader set INFO_SCRIPT_URL "%{INFO_SCRIPT_URL}e"
RequestHeader set INFO_SCRIPT_USER "%{INFO_SCRIPT_USER}e"
RequestHeader set INFO_SERVER_ADDR "%{INFO_SERVER_ADDR}e"
RequestHeader set INFO_SERVER_ADMIN "%{INFO_SERVER_ADMIN}e"
RequestHeader set INFO_SERVER_NAME "%{INFO_SERVER_NAME}e"
RequestHeader set INFO_SERVER_PORT "%{INFO_SERVER_PORT}e"
RequestHeader set INFO_SERVER_PROTOCOL "%{INFO_SERVER_PROTOCOL}e"
RequestHeader set INFO_SERVER_SIGNATURE "%{INFO_SERVER_SIGNATURE}e"
RequestHeader set INFO_SERVER_SOFTWARE "%{INFO_SERVER_SOFTWARE}e"
RequestHeader set INFO_THE_REQUEST "%{INFO_THE_REQUEST}e"
RequestHeader set INFO_TIME "%{INFO_TIME}e"
RequestHeader set INFO_TIME_DAY "%{INFO_TIME_DAY}e"
RequestHeader set INFO_TIME_HOUR "%{INFO_TIME_HOUR}e"
RequestHeader set INFO_TIME_MIN "%{INFO_TIME_MIN}e"
RequestHeader set INFO_TIME_MON "%{INFO_TIME_MON}e"
RequestHeader set INFO_TIME_SEC "%{INFO_TIME_SEC}e"
RequestHeader set INFO_TIME_WDAY "%{INFO_TIME_WDAY}e"
RequestHeader set INFO_TIME_YEAR "%{INFO_TIME_YEAR}e"
RequestHeader set INFO_TZ "%{INFO_TZ}e"
RequestHeader set INFO_UNIQUE_ID "%{INFO_UNIQUE_ID}e"
```

`index.php`:

```php
<?php
header('Content-Type: text/plain');

$infos = array();
foreach($_SERVER as $key => $value)
{
	if(substr($key, 0, 5) == 'HTTP_')
	{
		$infos[$key] = $value;
	}
}

ksort($infos);
print_r($infos);
?>
```

- `getenv`, `putenv`, `apache_getenv` and `apache_setenv`
- [apache - Set an environment variable in .htaccess and retrieve it in PHP - Stack Overflow](https://stackoverflow.com/questions/17550223/set-an-environment-variable-in-htaccess-and-retrieve-it-in-php)
- [Server alert you of File Not Found and other Errors | Lerner Consulting](http://website-tech.glerner.com/2013-server-alert-you-file-not-found-errors/)

## Other

From drupal:

```apache
# Protect files and directories from prying eyes.
<FilesMatch "\.(engine|inc|info|install|make|module|profile|test|po|sh|.*sql|theme|tpl(\.php)?|xtmpl)(~|\.sw[op]|\.bak|\.orig|\.save)?$|^(\..*|Entries.*|Repository|Root|Tag|Template|composer\.(json|lock))$|^#.*#$|\.php(~|\.sw[op]|\.bak|\.orig\.save)$">
  Order allow,deny
</FilesMatch>
```

```apache
# PHP 5 settings, Apache 1 and 2.
<IfModule mod_php5.c>
  php_flag magic_quotes_gpc                 off
  php_flag magic_quotes_sybase              off
  php_flag register_globals                 off
  php_flag session.auto_start               off
  php_value mbstring.http_input             pass
  php_value mbstring.http_output            pass
  php_flag mbstring.encoding_translation    off
</IfModule>
```

```apache
<IfModule mod_rewrite.c>
  RewriteEngine on

  # Set "protossl" to "s" if we were accessed via https://.  This is used later
  # if you enable "www." stripping or enforcement, in order to ensure that
  # you don't bounce between http and https.
  RewriteRule ^ - [E=protossl]
  RewriteCond %{HTTPS} on
  RewriteRule ^ - [E=protossl:s]

  # Make sure Authorization HTTP header is available to PHP
  # even when running as CGI or FastCGI.
  RewriteRule ^ - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]

  # Block access to "hidden" directories whose names begin with a period. This
  # includes directories used by version control systems such as Subversion or
  # Git to store control files. Files whose names begin with a period, as well
  # as the control files used by CVS, are protected by the FilesMatch directive
  # above.
  #
  # NOTE: This only works when mod_rewrite is loaded. Without mod_rewrite, it is
  # not possible to block access to entire directories from .htaccess, because
  # <DirectoryMatch> is not allowed here.
  #
  # If you do not have mod_rewrite installed, you should remove these
  # directories from your webroot or otherwise protect them from being
  # downloaded.
  RewriteRule "(^|/)\." - [F]

  # If your site can be accessed both with and without the 'www.' prefix, you
  # can use one of the following settings to redirect users to your preferred
  # URL, either WITH or WITHOUT the 'www.' prefix. Choose ONLY one option:
  #
  # To redirect all users to access the site WITH the 'www.' prefix,
  # (http://example.com/... will be redirected to http://www.example.com/...)
  # uncomment the following:
  # RewriteCond %{HTTP_HOST} .
  # RewriteCond %{HTTP_HOST} !^www\. [NC]
  # RewriteRule ^ http%{ENV:protossl}://www.%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
  #
  # To redirect all users to access the site WITHOUT the 'www.' prefix,
  # (http://www.example.com/... will be redirected to http://example.com/...)
  # uncomment the following:
  # RewriteCond %{HTTP_HOST} ^www\.(.+)$ [NC]
  # RewriteRule ^ http%{ENV:protossl}://%1%{REQUEST_URI} [L,R=301]
</IfModule>
```

## Special chars with `RewriteRule`

Ex: a file or folder named `tést $a?` (`te%CC%81st%20%24a%3F`) is translated internaly to `te\xcc\x81st $a` (discarding handling `?`)

Potential solution: use flag `B` or double URL encoding `?`

- [Using /, ? and & in the path with Apache mod_rewrite and PHP](http://www.gerd-riesselmann.net/development/using-and-path-apache-modrewrite-and-php/)
- [apache 2.2 - htaccess rule to rewrite %3F to ? and %3D to = - Server Fault](http://serverfault.com/questions/713856/htaccess-rule-to-rewrite-3f-to-and-3d-to)
- [mod rewrite - How to re-write %3f to ? in apache - Stack Overflow](https://stackoverflow.com/questions/13196398/how-to-re-write-3f-to-in-apache)
- flag `B` [RewriteRule Flags - Apache HTTP Server Version 2.4](http://httpd.apache.org/docs/current/en/rewrite/flags.html#flag_b)
- flag `NE` [RewriteRule Flags - Apache HTTP Server Version 2.4](http://httpd.apache.org/docs/current/en/rewrite/flags.html#flag_ne)
- [php - How to pass a Persian string as a argument in the URL? - Stack Overflow](https://stackoverflow.com/questions/34564364/how-to-pass-a-persian-string-as-a-argument-in-the-url)
- [php - htaccess decodes both %2B and + into space - Stack Overflow](https://stackoverflow.com/questions/32502135/htaccess-decodes-both-2b-and-into-space)
- [mod rewrite - How to encode special characters using mod_rewrite & Apache? - Stack Overflow](https://stackoverflow.com/questions/459667/how-to-encode-special-characters-using-mod-rewrite-apache)

## Bots

```apache
# redirect bots to one page
RewriteEngine on
RewriteCond %{HTTP_USER_AGENT} facebookexternalhit [NC,OR]
RewriteCond %{HTTP_USER_AGENT} Facebot [NC,OR]
RewriteCond %{HTTP_USER_AGENT} Twitterbot [NC,OR]
RewriteCond %{HTTP_USER_AGENT} Baiduspider [NC,OR]
RewriteCond %{HTTP_USER_AGENT} MetaURI [NC,OR]
RewriteCond %{HTTP_USER_AGENT} mediawords [NC,OR]
RewriteCond %{HTTP_USER_AGENT} FlipboardProxy [NC]
RewriteCond %{REQUEST_URI} !\/nocrawler.html
RewriteRule .* /nocrawler.html [L]
```

Or

```apache
# show a 403
SetEnvIfNoCase User-Agent "facebookexternalhit" bot
SetEnvIfNoCase User-Agent "Facebot" bot
SetEnvIfNoCase User-Agent "Twitterbot" bot
SetEnvIfNoCase User-Agent "Baiduspider" bot
SetEnvIfNoCase User-Agent "MetaURI" bot
SetEnvIfNoCase User-Agent "mediawords" bot
SetEnvIfNoCase User-Agent "FlipboardProxy" bot

<Limit GET POST HEAD>
	Order Allow,Deny
	Allow from all
	Deny from env=bot
</Limit>
```

Or use `robot.txt`

To get the list: add a honeypot URL, or use `wp-login` if it's a Wordpress website (but it will including you and others humans admin/users)

```sh
grep "honeypot" access.log | sort | uniq -c | sort -n
```

- https://github.com/serbanghita/Mobile-Detect/blob/c08a459521496f2925c3dcb186a910f5b8d7e336/Mobile_Detect.php#L554
