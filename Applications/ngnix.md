- How do you pronounce “NGINX”? [Frequently Asked Questions | NGINX](https://www.nginx.com/resources/wiki/community/faq/#how-do-you-pronounce-nginx)

## Nginx HTTPS configs 2016

	### Nginx main config: Tweaks & SSL settings (without the FastCGI-cache config parts)
	
	## http {} block:
	
	http {
	
	# [...]
	
		server_tokens off;
		reset_timedout_connection on;
		if_modified_since before;
	
		# Limit Request
		limit_req_status 403;
		limit_req_zone $binary_remote_addr zone=one:10m rate=1r/s;
	
		fastcgi_read_timeout 300;
		client_max_body_size 100m;
	
		ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
		ssl_ciphers "ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-CHACHA20-POLY1305:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!3DES:!MD5:!PSK";
	
		# Improves TTFB by using a smaller SSL buffer than the nginx default
		ssl_buffer_size 8k;
	
		ssl_session_cache builtin:1000 shared:SSL:200m;
		ssl_session_timeout 4h;
		ssl_ecdh_curve secp384r1;
		ssl_prefer_server_ciphers on;
		ssl_dhparam /etc/ssl/certs/dhparam.pem;
	
		# http://nginx.com/blog/improve-seo-https-nginx/
		ssl_session_tickets on;
	
		sendfile on;
		tcp_nopush on;
		tcp_nodelay on;
		keepalive_requests 500;
		keepalive_timeout 300 300;
		types_hash_max_size 2048;
	
		server_names_hash_max_size 1024;
		server_names_hash_bucket_size 96;
		server_name_in_redirect off;
	
		include mime.types;
		default_type application/octet-stream;
	
		open_log_file_cache max=1000 inactive=20s min_uses=2 valid=1m;
	
		gzip on;
		gzip_disable "msie6";
		gzip_vary on;
		gzip_proxied any;
		gzip_comp_level 6;
		gzip_buffers 16 8k;
		gzip_http_version 1.0;
		gzip_types application/xml;
		gzip_types application/xml+rss;
		gzip_types "application/x-javascript;charset=utf-8";
		gzip_types application/ecmascript;
		gzip_types application/javascript;
		gzip_types application/json;
		gzip_types application/pdf;
		gzip_types application/postscript;
		gzip_types application/x-javascript;
		gzip_types image/svg+xml;
		gzip_types image/bmp;
		gzip_types text/css;
		gzip_types text/csv;
		gzip_types text/javascript;
		gzip_types text/plain;
		gzip_types text/xml;
	
		open_file_cache     max=10000  inactive=10m;
		open_file_cache_valid   2m;
		open_file_cache_min_uses 1;
		open_file_cache_errors   on;
	
		fastcgi_buffers 128 32k;
		fastcgi_buffer_size 32k;
	
		fastcgi_param SERVER_NAME $http_host;
		fastcgi_ignore_headers  Cache-Control Expires Set-Cookie;
	
	# [...]
	
	}
	
	
	## server {} block port 80:
	
	server {
	
		listen   80 reuseport default_server backlog=65535 fastopen=5 deferred; ## listen for ipv4; this line is default and implied
		listen   [::]:80 reuseport default_server backlog=65535 fastopen=5 deferred; ## listen for ipv6
	
		server_name www.example.com example.com;
	
		# https://community.letsencrypt.org/t/howto-easy-cert-generation-and-renewal-with-nginx/3491
		location '/.well-known/acme-challenge' {
		default_type "text/plain";
		root        /tmp/letsencrypt-auto;
		}
	
		add_header Strict-Transport-Security "max-age=31536000;";
	
		location / {
		return 301 https://www.example.com$request_uri;
		}
	
	}
	
	
	## server {} block port 443 SSL:
	
	server {
	
		listen	443 reuseport default_server ssl http2 backlog=65535 fastopen=5 deferred;
		listen	[::]:443 reuseport default_server ssl http2 backlog=65535 fastopen=5 deferred;
	
		server_name www.example.com example.com;
	
		ssl_certificate /etc/letsencrypt/live/www.example.com/fullchain.pem;
		ssl_certificate_key /etc/letsencrypt/live/www.example.com/privkey.pem;
	
		ssl_stapling               on;
		ssl_stapling_verify        on;
		ssl_trusted_certificate /etc/letsencrypt/live/www.example.com/chain.pem;
	
		add_header Strict-Transport-Security "max-age=31536000;";
		add_header Access-Control-Allow-Origin *;
	    add_header X-Frame-Options "SAMEORIGIN" always;
	    add_header X-Xss-Protection "1; mode=block" always;
	    add_header X-Content-Type-Options "nosniff" always;
	    add_header Content-Security-Policy "default-src https: data: 'unsafe-inline' 'unsafe-eval'" always;
	
		access_log   /var/log/nginx/example.access.log;
		error_log    /var/log/nginx/example.error.log crit;
	
		root /home/example/www;
		index index.php index.htm index.html;
	
		add_header X-Frame-Options "SAMEORIGIN";
	
		# Use cached or actual file if they exists, Otherwise pass request to WordPress
		location / {
			try_files $uri $uri/ /index.php?$args;
		}
	
		location ~ ^/wp-content/cache/minify/(.+\.(css|js))$ {
			try_files $uri /wp-content/plugins/w3-total-cache/pub/minify.php?file=$1;
		}
	
		location ~ \.php$ {
			try_files $uri =404;
			include fastcgi_params;
			fastcgi_pass unix:/var/run/example-php.sock;
		}
	
		# Limit access to avoid brute force attack
		location = /wp-login.php {
			limit_req zone=one burst=1 nodelay;
			include fastcgi_params;
			fastcgi_pass unix:/var/run/example-php.sock;
		}
	
		# Disallow php in upload folder
		location /wp-content/uploads/ {
			location ~ \.php$ {
				#Prevent Direct Access Of PHP Files From Web Browsers
				deny all;
			}
		}
	
		# Yoast sitemap
		location ~ ([^/]*)sitemap(.*)\.x(m|s)l$ {
			rewrite ^/sitemap\.xml$ /sitemap_index.xml permanent;
			rewrite ^/([a-z]+)?-?sitemap\.xsl$ /index.php?xsl=$1 last;
			rewrite ^/sitemap_index\.xml$ /index.php?sitemap=1 last;
			rewrite ^/([^/]+?)-sitemap([0-9]+)?\.xml$ /index.php?sitemap=$1&sitemap_n=$2 last;
	
		# Following lines are options. Needed for WordPress seo addons
			rewrite ^/news_sitemap\.xml$ /index.php?sitemap=wpseo_news last;
			rewrite ^/locations\.kml$ /index.php?sitemap=wpseo_local_kml last;
			rewrite ^/geo_sitemap\.xml$ /index.php?sitemap=wpseo_local last;
			rewrite ^/video-sitemap\.xsl$ /index.php?xsl=video last;
	
		# Basic locations files
			location = /favicon.ico {
				access_log off;
				log_not_found off;
				expires max;
			}
	
			location = /robots.txt {
				access_log off;
				log_not_found off;
			}
	
		# Cache static files
			location ~* \.	(ogg|ogv|svg|svgz|eot|otf|woff|mp4|ttf|css|rss|atom|js|jpg|jpeg|gif|png|ico|zip|tgz|gz|rar|bz2|doc|xls|exe|ppt|tar|mid|midi|wav|bmp|rtf|swf|webp)$ {
				access_log off;
				log_not_found off;
				expires max;
				add_header Access-Control-Allow-Origin *;
				add_header Cache-Control "public, must-revalidate, proxy-revalidate";
				}
	
		# Deny hidden files
			location ~ /\. {
				deny  all;
				access_log off;
				log_not_found off;
			}
	
		# Deny backup extensions & log files
			location ~* ^.+\.(bak|log|old|orig|original|php#|php~|php_bak|save|swo|swp)$ {
				deny  all;
				access_log off;
				log_not_found off;
			}
	
	}
	
	
	### To compile Nginx:
	
	export PATH=/usr/lib/ccache:$PATH \
	DEB_CFLAGS_SET="-O3 -march=native -fstack-protector --param=ssp-buffer-size=4 -Wformat -Werror=format-security" \
	DEB_CXXFLAGS_SET="-O3 -march=native -fstack-protector --param=ssp-buffer-size=4 -Wformat -Werror=format-security" \
	DEB_FFLAGS_SET="-O3" \
	DEB_LDFLAGS_SET="-Wl,-z,relro"
	export DEB_CFLAGS_SET DEB_CXXFLAGS_SET DEB_FFLAGS_SET DEB_LDFLAGS_SET
	
	cd /usr/local/src/nginx-1.9.9
	make clean
	
	./configure --prefix=/opt/nginx19 --user=www-data --group=www-data --with-http_ssl_module --with-http_v2_module --with-openssl=/usr/local/src/openssl-1.0.2e --with-openssl-opt="enable-ec_nistp_64_gcc_128 threads" --with-md5=/usr/local/src/openssl-1.0.2e --with-md5-asm --with-sha1=/usr/local/src/openssl-1.0.2e --with-sha1-asm --with-pcre-jit --with-file-aio --with-http_flv_module --with-http_geoip_module --with-http_gzip_static_module --with-http_gunzip_module --with-http_mp4_module --with-http_realip_module --with-http_stub_status_module --with-threads --with-ipv6 --with-cc-opt="-DTCP_FASTOPEN=23 -O3 -march=native"
	
	sudo nice make install
	
	
	### OpenSSL patch for PolyChaCha cipher (apply to OpenSSL source code):
	
	wget "https://github.com/as-com/sslconfig/raw/master/patches/openssl__chacha20_poly1305_cf.patch"
	patch -p1 < openssl__chacha20_poly1305_cf.patch
	
	
	### CHECKS:
	
	SSL check: https://www.ssllabs.com/ssltest/
	Headers check: https://securityheaders.io
	
	Using Wordpress? DO NOT FORGET: IMPLEMENT FASTCGI-CACHING.
	https://easyengine.io/wordpress-nginx/tutorials/single-site/fastcgi-cache-with-purging/
	https://www.digitalocean.com/community/tutorials/how-to-setup-fastcgi-caching-with-nginx-on-your-vps