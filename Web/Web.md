> The web is not one platform.
> It is a multitude of platforms, most of which you’ll never test on.
— Peter-Paul Koch

- [How to keep up to date on Front-End Technologies - The Recipe](https://uptodate.frontendrescue.org/)
- [HTTP Archive](http://httparchive.org/)
- [A little holiday present: 10,000 reqs/sec with Nginx! » WebFaction Blog](https://blog.webfaction.com/2008/12/a-little-holiday-present-10000-reqssec-with-nginx-2/)

See also:

- [dexteryy/spellbook-of-modern-webdev: A Big Picture, Thesaurus, and Taxonomy of Modern JavaScript Web Development](https://github.com/dexteryy/spellbook-of-modern-webdev)

News

- [All issues | Web Platform News](https://webplatform.news/issues) - https://webplatform.news/feed.xml
- [simevidas/webplatformnews-feeds: An OPML file containing over 600 feeds for web developers](https://github.com/simevidas/webplatformnews-feeds)
- [webplatformdaily-site/content/dailies at 53c36a5daf62633a1c3f4f769071585f4aaddf6f · simevidas/webplatformdaily-site](https://github.com/simevidas/webplatformdaily-site/tree/53c36a5daf62633a1c3f4f769071585f4aaddf6f/content/dailies)
- [web-platform-timeline.md](https://gist.github.com/simevidas/cccf3e9885327a52fb7ccb23c4be3a5c)
- [https://webplatform.news](https://gist.github.com/simevidas/2a207094f505aa177d625b8e2c1ac010)
- [All issues | Web Platform News](https://webplatform.news/issues)
- [webplatformnews-weekly/issues at master · simevidas/webplatformnews-weekly](https://github.com/simevidas/webplatformnews-weekly/tree/master/issues)
- [simevidas/browser-intents](https://github.com/simevidas/browser-intents)
- [Web Platform News (@WebPlatformNews) | Twitter](https://twitter.com/webplatformnews)

## DNS

- [How DNS works](https://howdns.works/)
- [linux - Force dig to resolve without using cache - Server Fault](https://serverfault.com/questions/372066/force-dig-to-resolve-without-using-cache/372071#372071)

### DNS records

DNS records

Names (exemples for `example.com`):

- `@` naked name (`example.com`), the domain itself
- `*` fallback subdomain (`*.example.com`, but doesn't match `*.test.example.com` if `test.example.com` is declared)
- `www` subdomain (`www.example.com`)
- `test.www` subsubdomain (`test.www.example.com`)
- `*.www` fallback subsubdomain (`*.www.example.com`)

`* CNAME @` is not possible with all DNS servers, and not recommanded (need 2 DNS requests to resolve subdomain)

```
@ IN A 192.0.2.1
@ IN TXT "some text"
```

```
# dig www.example without DNS cache
dig @$(dig example.com NS +short | head -n1) www.example.com ANY +noall +answer
```

- [List of DNS record types - Wikipedia](https://en.wikipedia.org/wiki/List_of_DNS_record_types)
- [Domain Name System - Wikipedia](https://en.wikipedia.org/wiki/Domain_Name_System#Resource_records)

## HTTP

Note: don't name your local server `*.local`. See [Local TLD](macOS#local-tld)
Note: `Range` header could be ignore if the content need to be gzipped (It's the case with nginx)

FQDN:
	[fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), with the trailing dot (root zone)
TLD:
	[top level domain](https://en.wikipedia.org/wiki/Top-level_domain) (e.g. .com, .net, .bmw, .us). See the [list of TLDs](http://data.iana.org/TLD/tlds-alpha-by-domain.txt)
eTLD:
	effective top level domain (e.g. .com, .co.uk and .pvt.k12.wy.us). See the [public suffix list](https://publicsuffix.org/)
eTLD+1:
	effective top level domain plus one level (e.g. example.com, example.co.uk)
SLD:
	second level domain (e.g. co is the SLD of www.example.co.uk)

See also:

- [We Suck at HTTP](http://gadgetopia.com/post/9236?retitle)
- [Proxy auto-config — Wikipedia](https://en.wikipedia.org/wiki/Proxy_auto-config)
- [Journey to HTTP/2 · @kamranahmedse](http://kamranahmed.info/blog/2016/08/13/http-in-depth/)
- [HTTP: HTTP/2 - High Performance Browser Networking (O'Reilly)](https://hpbn.co/http2/)
- [Network](https://github.com/dexteryy/spellbook-of-modern-webdev#network)
- [Wireshark · Go Deep.](https://www.wireshark.org/) - network protocol analyzer

### Headers

`X-` prefix is discouraged ("SHOULD NOT") if this header would come a standard

- [RFC 7230 - Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing](https://tools.ietf.org/html/rfc7230#section-3.2.2)
- [Custom HTTP headers : naming conventions - Stack Overflow](https://stackoverflow.com/questions/3561381/custom-http-headers-naming-conventions/3561399#3561399)
- [RFC 6648 - Deprecating the "X-" Prefix and Similar Constructs in Application Protocols](https://tools.ietf.org/html/rfc6648)

### Use right status

- `401 Unauthorized`: concern authentification
- `403 Forbidden`: concern authorization

- [File:Http-headers-status.svg - Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Http-headers-status.svg)
- [Choosing an HTTP Status Code — Stop Making It Hard | Racksburg](http://racksburg.com/choosing-an-http-status-code/)
- [410 Gone](http://gadgetopia.com/post/6370)
- [HTTP Status Codes — httpstatuses.com](https://httpstatuses.com/)
- [RFC for the 7XX Range of HTTP Status codes - Developer Errors](https://github.com/joho/7xx-rfc)
- https://restpatterns.mindtouch.us/HTTP_Status_Codes

### Redirects can break `POST`

...or any other method other than `GET`.

	23:50:52:658: Network: POST http://host/folder [HTTP/1.1 301 Moved Permanently 947ms]
	23:50:53:614: Network: GET http://host/folder/ [HTTP/1.1 200 OK 400ms]

> When you use a 301 or 302 redirect, the browser will change the method on the redirect to be a GET request, even if the original method was a POST request.

**Use the 307 and 308 status codes instead if you need to retain the method**

- [301s, 302s, 307s & 308s: Report URI's journey to a permanent redirect](https://scotthelme.co.uk/report-uri-journey-to-a-permanent-redirect/)
- [web development - Why doesn't HTTP have POST redirect? - Software Engineering Stack Exchange](https://softwareengineering.stackexchange.com/questions/99894/why-doesnt-http-have-post-redirect/99966#99966)

### Define generated filename

	Content-Disposition: "attachment; filename=generated_filename.ext"

`filename*0=""`

### HTTPS (TLS)

See [Transport Layer Security](Security#transport-layer-security) and [Decrypt TLS](Security#decrypt-tls)

About mixed content:

- `Content-Security-Policy: upgrade-insecure-requests;` - see [CSP: upgrade-insecure-requests - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/upgrade-insecure-requests)
- [Troy Hunt: Disqus' mixed content problem and fixing it with a CSP](https://www.troyhunt.com/disqus-mixed-content-problem-and-fixing-it-with-a-csp/)
- [The Complete Guide To Switching From HTTP To HTTPS – Smashing Magazine](https://www.smashingmagazine.com/2017/06/guide-switching-http-https/)
- See also HSTS

### Streaming and Push

Server Side Event, WebSocket or long-polling HTTP request, pull

For live content (live number of watchers, real-time transport traffic, real-time updated article, etc.), doesn't require bi-directional (full-duplex) communication, use [SSE](#server-side-event) first

- [Google Maps .Net Control](http://gmapsdotnetcontrol.blogspot.fr/2006/08/exploring-reverse-ajax-ajax.html)
- [Push technology — Wikipedia](https://en.wikipedia.org/wiki/Push_technology)
- [Comet (programming) — Wikipedia](https://en.wikipedia.org/wiki/Comet_%28programming%29)
- [Streaming media — Wikipedia](https://en.wikipedia.org/wiki/Streaming_media)
- [Progressive download — Wikipedia](https://en.wikipedia.org/wiki/Progressive_download)
- [How Facebook Live Streams to 800,000 Simultaneous Viewers - High Scalability -](http://highscalability.com/blog/2016/6/27/how-facebook-live-streams-to-800000-simultaneous-viewers.html)
- [Browser APIs and Protocols: XMLHttpRequest - High Performance Browser Networking (O'Reilly)](https://hpbn.co/xmlhttprequest/#real-time-notifications-and-delivery)
- [WebSockets vs Server-Sent Events vs Long-polling](http://dsheiko.com/weblog/websockets-vs-sse-vs-long-polling)

**Note: proxy servers and firewalls could buffer the response, increasing the latency of the message delivery. Antivirus software may block the event streaming data chunks. TLS could be use to solve this problem:**

Note: don't forget to push/flush the content: - [php - Server sent events work, but with a massive time delay - Stack Overflow](https://stackoverflow.com/questions/12297740/server-sent-events-work-but-with-a-massive-time-delay) 

- [Networking 101: Transport Layer Security (TLS) - High Performance Browser Networking (O'Reilly)](https://hpbn.co/transport-layer-security-tls/#proxies-intermediaries-tls-and-new-protocols-on-the-web)
- [html5 - JavaScript EventSource SSE not firing in browser - Stack Overflow](https://stackoverflow.com/questions/12978466/javascript-eventsource-sse-not-firing-in-browser/13135995#13135995)
- [Sophos AV blocks server-sent events (SSE) on Mac OS X Yosemite - Sophos Anti-Virus for Mac Home Edition - Free Tools - Sophos Community](https://community.sophos.com/products/free-antivirus-tools-for-desktops/f/sophos-anti-virus-for-mac-home-edition/5750/sophos-av-blocks-server-sent-events-sse-on-mac-os-x-yosemite)
- [Server Sent Events blocked by Download Scanner - Sophos Endpoint Software - Endpoint Security and Control - Sophos Community](https://community.sophos.com/products/endpoint-security-control/f/sophos-endpoint-software/74878/server-sent-events-blocked-by-download-scanner)

#### Server Side Event

Aka SSE, EventSource

SSE use vanilla HTTP (eg thru load-balancers) and do auto-reconnect

- [Browser APIs and Protocols: Server-Sent Events (SSE) - High Performance Browser Networking (O'Reilly)](https://hpbn.co/server-sent-events-sse/)
- [Stream Updates with Server-Sent Events - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/eventsource/basics/)
- [Using server-sent events - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events)
- [Server-Sent Events explained with usecases](https://streamdata.io/blog/server-sent-events/)
- [html5 - Server-Sent Events vs Polling - Stack Overflow](https://stackoverflow.com/questions/9397528/server-sent-events-vs-polling)
- [Yaffle/EventSource: a polyfill for http://www.w3.org/TR/eventsource/](https://github.com/Yaffle/EventSource#server-side-nodejs) - Example of Server-sent events with Node.js
- [SSE vs Websockets - Streamdata.io](https://streamdata.io/blog/push-sse-vs-websockets/)
- [Server-Sent Events with Node.js (Express)](https://tomkersten.com/articles/server-sent-events-with-node/)


#### Websocket

Aka WS

- [Fanout Blog » You might not need a WebSocket](http://blog.fanout.io/2014/06/24/you-might-not-need-a-websocket/)
- [WebSockets, caution required!](https://samsaffron.com/archive/2015/12/29/websockets-caution-required)
- [600k concurrent websocket connections on AWS using Node.js - Jayway](http://www.jayway.com/2015/04/13/600k-concurrent-websocket-connections-on-aws-using-node-js/) - [600k concurrent websocket connections on AWS using Node.js (2015) | Hacker News](https://news.ycombinator.com/item?id=21222913)
- websocket server library used by Stack Overflow: https://github.com/StackExchange/NetGain
- [node.js - Proxying WebSockets with TCP load balancer without sticky sessions - Stack Overflow](https://stackoverflow.com/questions/15266702/proxying-websockets-with-tcp-load-balancer-without-sticky-sessions/15270860#15270860)
- [HTML5 WebSocket - A Quantum Leap in Scalability for the Web](http://www.websocket.org/quantum.html)

For Nodejs:

- [Starting Node.js using forever with --nouse-idle-notification and other flags - Stack Overflow](https://stackoverflow.com/questions/12901358/starting-node-js-using-forever-with-nouse-idle-notification-and-other-flags)

For Ngnix:

Example of Ngnix-as-proxy configuration:

	http {
		map $http_upgrade $connection_upgrade {
			default upgrade;
			'' close;
		}
		
		upstream ws_server {
			server localhost:9000;
		}
		
		server {
			ssl on;
			ssl_certificate /path/to/crt;
			ssl_certificate_key /path/to/key;
			
			root /data/www/public;
				
			location / {
			}
		
			location /app {
				proxy_pass http://ws_server;
				proxy_http_version 1.1;
				proxy_set_header Upgrade $http_upgrade;
				proxy_set_header Connection $connection_upgrade;
				proxy_set_header Host $host;
				proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
			}
		}
	}

- [Using NGINX as a WebSocket Proxy](https://www.nginx.com/blog/websocket-nginx/)
- [Websockets SSL/TLS Termination Using NGINX Proxy · Pankaj Malhotra](http://pankajmalhotra.com/Websockets-SSL-TLS-Termination-Using-NGINX-Proxy/)

For Apache:

Example of Apache-as-proxy configuration (require `mod_proxy` and `mod_proxy_wstunnel` - require httpd 2.4.5)

	# Reverse proxy to nodejs
	<Location /ws-service>
		Require all granted
		ProxyPass ws://localhost:9000
		ProxyPassReverse ws://localhost:9000
	</Location>

- https://stackoverflow.com/questions/30443999/how-to-add-mod-proxy-wstunnel-to-apache2-2-2-on-raspberry-pi-backport-mod-proxy

### Content type

- HTML
- XML
- [JSON](https://en.wikipedia.org/wiki/JSON)
- [Action Message Format (AMF)](https://en.wikipedia.org/wiki/Action_Message_Format)
- [Concise Binary Object Representation (CBOR)](https://tools.ietf.org/html/rfc7049)

Note: use `text/html` even if it's a fragment of a HTML document

See also

- [Comparison of data serialization formats — Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_data_serialization_formats)
- [JSON Homogeneous Collections Compression (JSONH)](https://github.com/WebReflection/JSONH)

### HSTS

To disable HSTS use the following header (when HTTPS): `Strict-Transport-Security: max-age=0` (in `.htaccess`: `Header set Strict-Transport-Security "max-age=0"`)

- [tls - Is there a problem with issuing a HSTS header in PHP? - Information Security Stack Exchange](http://security.stackexchange.com/questions/43148/is-there-a-problem-with-issuing-a-hsts-header-in-php)
- [Preloading HSTS | Mozilla Security Blog](https://blog.mozilla.org/security/2012/11/01/preloading-hsts/)

See [HSTS](Security#hsts)

### Server Push

Aka HTTP/2 Server Push

Adviced order, push while processing (while waiting for the app response): static assets (`script`, `image`, `style`, `fetch`, etc.) then the html (let the time to the server to processing the request and render the response).
Possible to send status `103 Early Hints` then `200 OK`
Concatenate small files

Browsers often implent HTTP/2.0 only over TLS

- Required Assets: CSS, JavaScript, and image assets required by a web page
- Uncacheable Assets: Pushing dynamic assets = reduce page load time
- Likely Next Pages: the page that a user is likely to load (e.g., the link they’re hovering over), make it look like it loads instantaneously
- Redirects
 
	<Location /index.html>
		Header add Link "</css/site.css>;rel=preload;as=style"
		Header add Link "</images/logo.jpg>;rel=preload;as=image"
	</Location>

Inline `Link: </css/my.css>;rel=preload;as=style, </js/jquery.js>;rel=preload;as=script` works too

Or define it via PHP:

	header('Link: </css/my.css>;rel=preload;as=style', false);

Note: I you don't want the server push the resource (preload only) with Link header, use `nopush` as: `Link: </css/image.webp>;rel=preload;as=image;type=image/webp;nopush` Use this if the header `Save-Data: on`
It's usefull in case the resource format is not widely supported

- [mod_http2 - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/current/mod/mod_http2.html#h2push)
- [HTTP/2 Server Push — Wikipedia](https://en.wikipedia.org/wiki/HTTP/2_Server_Push)
- [Preload](https://www.w3.org/TR/preload/#server-push-http-2)
- [Using HTTP/2 Server Push with PHP](https://blog.cloudflare.com/using-http-2-server-push-with-php/)
- [HTTP/2 Frequently Asked Questions](https://http2.github.io/faq/)
- [OptimizingForSpdy - mod-spdy - How to tune your server to serve pages over SPDY efficiently - Apache SPDY module - Google Project Hosting](https://code.google.com/p/mod-spdy/wiki/OptimizingForSpdy#Using_SPDY_server_push)
- [concept-request-type](https://fetch.spec.whatwg.org/#concept-request-type)
- [Reorganizing Website Architecture for HTTP/2 and Beyond](http://www.slideshare.net/kazuho/reorganizing-website-architecture-for-http2-and-beyond)

#### Cache-aware server push

	// https://css-tricks.com/cache-aware-server-push/
	function pushAssets() {
		$pushes = array(
			'/css/styles.css' => substr(md5_file('/var/www/css/styles.css'), 0, 8),
			'/js/scripts.js' => substr(md5_file('/var/www/js/scripts.js'), 0, 8)
		);
	
		if (!isset($_COOKIE['h2pushes'])) {
			$pushString = buildPushString($pushes);
			header($pushString);
			setcookie('h2pushes', json_encode($pushes), 0, 2592000, '', '.myradwebsite.com', true);
		} else {
			$serializedPushes = json_encode($pushes);
	
			if ($serializedPushes !== $_COOKIE['h2pushes']) {
				$oldPushes = json_decode($_COOKIE['h2pushes'], true);
				$diff = array_diff_assoc($pushes, $oldPushes);
				$pushString = buildPushString($diff);
				header($pushString);
				setcookie('h2pushes', json_encode($pushes), 0, 2592000, '', '.myradwebsite.com', true);
			}
		}
	}
	
	function buildPushString($pushes) {
		$pushString = 'Link: ';
	
		foreach($pushes as $asset => $version) {
			// TODO add "as" parameter (style, script, etc.)
			$pushString .= '<' . $asset . '>; rel=preload';
	
			if ($asset !== end($pushes)) {
				$pushString .= ',';
			}
		}
	
		return $pushString;
	}
	
	// Push those assets!
	pushAssets();

- [HTTP/2 push is tougher than I thought - JakeArchibald.com](https://jakearchibald.com/2017/h2-push-tougher-than-i-thought/)
- [Creating a Cache-aware HTTP/2 Server Push Mechanism | CSS-Tricks](https://css-tricks.com/cache-aware-server-push/)
- [A Comprehensive Guide To HTTP/2 Server Push – Smashing Magazine](https://www.smashingmagazine.com/2017/04/guide-http2-server-push/#pushes-may-not-be-cached)
- [HTTP/2 Directives - Configure - H2O - the optimized HTTP/2 server](https://h2o.examp1e.net/configure/http2_directives.html#http2-casper)
- [Hypertext Transfer Protocol Version 2 (HTTP/2)](https://http2.github.io/http2-spec/#RST_STREAM) - see [http - RST_STREAM frame in HTTP2 - Stack Overflow](https://stackoverflow.com/questions/28736463/rst-stream-frame-in-http2)

### Force download

	Content-Disposition: attachment;filename=file.ext

You can use also:

	Content-Type: application/octet-stream

	X-Download-Options: noopen

### Referer

See [Security](Security#http-referer)

### Method

Aka POST, GET, HEAD, PUT, etc.

See [RESTful](#restful) and [API](#api)

- `X-HTTP-Method` (Microsoft), `X-HTTP-Method-Override` (Google/GData), `X-Method-Override` (IBM)
- [The Definitive Guide to GET vs POST - Treehouse Blog](http://blog.teamtreehouse.com/the-definitive-guide-to-get-vs-post)

### Simple HTTP Server

**Run in controlled environments only!**. Useful for testing purposes or for application demonstrations

- [20.19. SimpleHTTPServer — Simple HTTP request handler — Python 2.7.13 documentation](https://docs.python.org/2/library/simplehttpserver.html) - `python -m SimpleHTTPServer 8000`
- [PHP: Built-in web server - Manual](http://php.net/manual/en/features.commandline.webserver.php) - `php -S localhost:8000`
- [Netcat — Wikipedia](https://en.wikipedia.org/wiki/Netcat) - `while true; do nc -l 8000 < response.http; done`. Will serve an unique stream/page. To get the raw HTTP response, use `printf "GET / HTTP/1.1\nHost:example.com\nUser-Agent:Firefox\Connection: close\n\n" | nc example.com 80 > response.http` or write/edit it with text editor
- [A simple HTTP/2 server for development](https://github.com/GoogleChrome/simplehttp2server) - Written in Go
- [kzahel/web-server-chrome: An HTTP Web Server for Chrome (chrome.socket API)](https://github.com/kzahel/web-server-chrome)

### Content encoding

See [Precompress](#precompress)

Note: sometimes you can't encode content, event if the final client support it, mediators could not (proxies, cache servers, etc.): [Who’s not getting gzip? | High Performance Web Sites](http://www.stevesouders.com/blog/2009/11/11/whos-not-getting-gzip/)

Aka brotli, gzip, zlib, deflate

- `gzip` is the _GZIP_ file format: GZIP headers (can contains filename and a timestamp), _DEFLATE_ data, and a checksum
- `deflate` is actually the _ZLIB_ data format: zlib header, _DEFLATE_ data, and a checksum

Some clients do also accept the actual _DEFLATE_ data format for deflate.

Note: GZip remove the advantage UTF-16 might have over UTF-8 for East Asian-heavy text.

About brotli vs gzip:

> Brotli is mostly nice for clients, with decompression performance comparable to gzip while significantly improving the compression ratio. These are powerful properties for serving static content such as fonts and html pages.
> However compression performance, at least for the current implementation, is considerably slower than gzip, which makes Brotli unsuitable for on-the-fly compression in http servers or other data streams.
— [OpenCPU - Compression Benchmarks: brotli, gzip, xz, bz2](https://www.opencpu.org/posts/brotli-benchmarks/)

- [GZip](GZip)
- [Content-Encoding - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Encoding)
- [Compression Tests: About](http://wayback.archive.org/web/20150102111552/http://www.vervestudios.co/projects/compression-tests/)
- [Lose the Wait: HTTP Compression - Zoompf Web Performance](https://zoompf.com/blog/2012/02/lose-the-wait-http-compression)
- [compression - Why use deflate instead of gzip for text files served by Apache? - Stack Overflow](https://stackoverflow.com/questions/388595/why-use-deflate-instead-of-gzip-for-text-files-served-by-apache)
- [You're Reading The World's Most Dangerous Programming Blog](https://blog.codinghorror.com/youre-reading-the-worlds-most-dangerous-programming-blog/)
- [http - Why do real-world servers prefer gzip over deflate encoding? - Stack Overflow](https://stackoverflow.com/questions/883841/why-do-real-world-servers-prefer-gzip-over-deflate-encoding/1579506#1579506)
- [Lose the Wait: HTTP Compression - Zoompf Web Performance](https://zoompf.com/blog/2012/02/lose-the-wait-http-compression/)

### Content language

`lang` indicates the language of the text, whereas `Content-Language` provides metadata about the intended audience of the document.

- [Types of language declaration](https://www.w3.org/International/questions/qa-text-processing-vs-metadata)

### Request content encoding

See [Content encoding](#content-encoding)

Send compressed request body

If the server doesn't support the given encoding, should response with the status 415 (Unsupported Media Type)

- [gzip - Compressing HTTP Post Data sent from browser - Stack Overflow](https://stackoverflow.com/questions/13031968/compressing-http-post-data-sent-from-browser)
- [Is it possible to enable http compression for requests? - Server Fault](https://serverfault.com/questions/56700/is-it-possible-to-enable-http-compression-for-requests)

### Transfert encoding

> Note that chunked is always acceptable for HTTP/1.1 recipients

- [Chunked transfert encoding](PHP#chunked-transfert-encoding)
- [TE - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/TE)
- [Transfer-Encoding - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Transfer-Encoding)
- [Trailer - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Trailer)
- [Chunked transfer encoding — Wikipedia](https://en.wikipedia.org/wiki/Chunked_transfer_encoding)
- [http - How to make PHP generate Chunked response - Stack Overflow](https://stackoverflow.com/questions/2481858/how-to-make-php-generate-chunked-response)
- [How to generate Chunked response with a Trailer in Apache/PHP? - Stack Overflow](https://stackoverflow.com/questions/11820138/how-to-generate-chunked-response-with-a-trailer-in-apache-php)

About ranges and chunked transfert encoding:

- [HTTP range requests - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Range_requests#Comparison_to_chunked_Transfer-Encoding) - 
- [Byte serving — Wikipedia](https://en.wikipedia.org/wiki/Byte_serving)

### Send binary data in JSON

See [Request content encoding](#request-content-encoding)

base64 or `multipart/form-data`

- [Binary Data in JSON String. Something better than Base64 - Stack Overflow](https://stackoverflow.com/questions/1443158/binary-data-in-json-string-something-better-than-base64/28080392#28080392)
- [javascript - fetch post with multipart form data - Stack Overflow](https://stackoverflow.com/questions/35192841/fetch-post-with-multipart-form-data)

### WebRTC

- [Janus WebRTC Gateway ](https://github.com/meetecho/janus-gateway) - WebRTC protocol used in client-server architecture
- [serverless-webrtc - A demo of using WebRTC with no signaling server](https://github.com/cjb/serverless-webrtc/)
- https://github.com/js-platform/node-webrtc
- https://github.com/mappum/electron-webrtc

### Measure network quality

https://docs.google.com/document/d/1eBix6HvKSXihGhSbhd3Ld7AGTMXGfqXleu1XKSFtKWQ/edit

### Get client IP

Or proxy's IP

- [wp-geoip-detect/api.php at d48a2d6134a4edf9843d5e4c7c0e4bfd8c4e139d · yellowtree/wp-geoip-detect](https://github.com/yellowtree/wp-geoip-detect/blob/d48a2d6134a4edf9843d5e4c7c0e4bfd8c4e139d/api.php#L177-L220)

- [X-Forwarded-For — Wikipedia](https://en.wikipedia.org/wiki/X-Forwarded-For)
 
	// Note: X-Forwarded-For contains a list of IP address, where the first one is the client's IP
	if (array_key_exists('HTTP_CLIENT_IP', $_SERVER)) {
		$ipaddress = $_SERVER['HTTP_CLIENT_IP'];
	} else if (array_key_exists('HTTP_X_FORWARDED_FOR', $_SERVER)) {
		$ipaddress = $_SERVER['HTTP_X_FORWARDED_FOR'];
	} else if (array_key_exists('HTTP_X_FORWARDED', $_SERVER)) {
		$ipaddress = $_SERVER['HTTP_X_FORWARDED'];
	} else if (array_key_exists('HTTP_FORWARDED_FOR', $_SERVER)) {
		$ipaddress = $_SERVER['HTTP_FORWARDED_FOR'];
	} else if (array_key_exists('HTTP_FORWARDED', $_SERVER)) {
		$ipaddress = $_SERVER['HTTP_FORWARDED'];
	} else if (array_key_exists('REMOTE_ADDR', $_SERVER)) {
		$ipaddress = $_SERVER['REMOTE_ADDR'];
	} else {
		$ipaddress = null;// not known
	}

	$_SERVER['HTTP_X_REAL_IP'];

	$iptype = 'unknown';
	if(!empty($iptype)){
		if(preg_match("/^[0-9a-f]{1,4}:([0-9a-f]{0,4}:){1,6}[0-9a-f]{1,4}$/", $ip) != 0){
			$iptype = 'IPv6';
		}else if(preg_match("/^([0-9]{1,3}\.){3}[0-9]{1,3}$/", $ip) != 0){
			$iptype = 'IPv4';
		}
	}

IPv4 to number & number to IPv4:

	function ipv4ToNumberumber($ip) { 
		list($a, $b, $c, $d) = explode('.', $ip); 
		return (double) ($a*16777216)+($b*65536)+($c*256)+($d);
	}
	function numberToIPv4($number) { 
		$a = ($number/16777216)%256; 
		$b = ($number/65536)%256; 
		$c = ($number/256)%256; 
		$d = ($number)%256; 
		return $a.'.'.$b.'.'.$c.'.'.$d;
	} 

- [apache - How to set REMOTE_ADDR to HTTP_X_REAL_IP? - Stack Overflow](https://stackoverflow.com/questions/27329499/how-to-set-remote-addr-to-http-x-real-ip/27340127#27340127)

### Geo IP

- [apilayer/geolocationapi: IP Geolocation API is a free service for locating your visitors in real-time with detailed country information.](https://github.com/apilayer/geolocationapi)
- [IP Geolocation API \[ip-api\]](http://ip-api.com/docs/)
- [The Google Maps Geolocation API | Google Maps Geolocation API | Google Developers](https://developers.google.com/maps/documentation/geolocation/intro)
- [freegeoip.net](http://freegeoip.net/?q=90.63.250.12)
- http://dev.maxmind.com/geoip/legacy/downloadable/
- https://countryblocklist.com/
- [Major IP Addresses Blocks By Country](http://www.nirsoft.net/countryip/index.html)
- http://www.ipdeny.com/ipblocks/data/countries/

### Proxy

#### Proxy can transform content

Can transform content: remove comments (HTML, JS, CSS), recompress (reduce JPEG quality), block files, change formats (APNG → PNG, remove fdAT and fcTL chunks), rewrite links (`src` or `href` attributes), etc.

(SFR) if file header looklike an image header (JPEG or PNG), the following content could be broken

- Mobile network providers/ISP like SFR (FR), Bouygues Telecom (FR), O2 (UK), Centertel, China Mobile, Cingular, Connex, Nextel, NTT DoCoMo, Orange, Proximus, Sprint Nextel, T-Mobile, Telefónica Móviles, O2, Vodafone (IE, DE), Willcom... often use [Citrix ByteMobile Proxy](http://www.citrix.com/products/bytemobile-adaptive-traffic-management/overview.html)
- Cache proxies
- Proxy browsers like Opera Mini (use Citrix ByteMobile Proxy too), UCBrowser or Puffin. "reduce data usage" mode in mobile Chrome.
- Other Proxies/VPN like [Opera Turbo](http://www.opera.com/fr/turbo), [Opera Max](http://www.opera.com/mobile/max), [Mozilla Janus](https://wiki.mozilla.org/Mobile/Janus), Google [Data Saver](https://chrome.google.com/webstore/detail/data-saver-beta/pfmgfdlgomnbgkofeojodiodmgpgmkac)

To prevent proxys from modifying the website's content, serve the content with this HTTP header:

	Cache-Control: no-transform

Apache config (ex.: in `.htaccess`):

	<IfModule headers_module>
		Header set Cache-Control no-transform
	</IfModule>

Serve HTTPS can't always resolve issues.

- [HTTP/1.1: Header Field Definitions - 14.9.5 No-Transform Directive](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9.5)
- [Performance Calendar » Mobile ISP image recompression](http://calendar.perfplanet.com/2013/mobile-isp-image-recompression/)
- [SFR modifie le source HTML des pages que vous visitez en 3G : Reflets](http://reflets.info/sfr-modifie-le-source-html-des-pages-que-vous-visitez-en-3g/)
- [Stop mobile network proxy from injecting JavaScript - Stack Overflow](https://stackoverflow.com/questions/4113268/stop-mobile-network-proxy-from-injecting-javascript)
- [Mobile ISP can break WebSocket connections](http://blog.hekkers.net/2012/12/09/websockets-and-mobile-network-operators/)
- [Any reason not to add "Cache-Control: no-transform" header to every page? - Stack Overflow](https://stackoverflow.com/questions/20134257/any-reason-not-to-add-cache-control-no-transform-header-to-every-page)
- [Bytemobile and Opera Software Form Partnership for Browser Optimization - Opera Software](http://www.operasoftware.com/press/releases/desktop/bytemobile-and-opera-software-form-partnership-for-browser-optimization)
- [Cache-Control — Wikipédia](http://fr.wikipedia.org/wiki/Cache-Control#no-transform)

See also Ads / Content blockers like [Focus](https://support.mozilla.org/en/products/focus-firefox) or [Adblock Plus](https://adblockplus.org/) or Anti Ad blocker https://github.com/reek/anti-adblock-killer/
See [Validity of CSS class names and ids](HTML#validity-of-css-class-names-and-ids)

#### Proxy Server

- [mitmproxy/mitmproxy: An interactive TLS-capable intercepting HTTP proxy for penetration testers and software developers.](https://github.com/mitmproxy/mitmproxy)
- [Charles Web Debugging Proxy • HTTP Monitor / HTTP Proxy / HTTPS & SSL Proxy / Reverse Proxy](https://www.charlesproxy.com/)
- [Fiddler - Free Web Debugging Proxy - Telerik](https://www.telerik.com/fiddler)

##### Use Apache as proxy server

Serve http://X.X.X.X:8080/pac.php

(Listen 8080)
Some browsers map internaly `localhost` without proxy. To skip that, add the FQDN trailing dot to it (IE7+): `localhost.`

`<proxy *>` or `<proxy http://www.google.com>`

`proxy.conf`:

	# Forward proxy server
	<VirtualHost *:8080>
		ProxyRequests On
		ProxyVia On
	
		<Proxy *>
			Order deny,allow
			Deny from all
			Allow from 127.0.0.1
			Allow from 192.168
		
			RewriteEngine on
			RewriteCond %{REQUEST_URI} !/pac.php
			RewriteRule ^ /endpoint.php [L]
		</Proxy>
	</VirtualHost>

`endpoint.php`:

	<?php
	// Don't handle domain existance
	$url = $_SERVER['REQUEST_URI'];
	$url_parts = parse_url($url);
	// Some security checks (no local file...)
	if(false === $url_parts || empty($url_parts['scheme']) || !in_array($url_parts['scheme'], array('http', 'https'))){
		die();
	}
	
	$headers_raw = '';
	foreach ($_SERVER as $name => $value)
	{
		if (substr($name, 0, 5) == 'HTTP_')
		{
			$name = str_replace(' ', '-', ucwords(strtolower(str_replace('_', ' ', substr($name, 5)))));
			$headers_raw .= $name . ': ' . $value . "\r\n";
		} else if ($name == "CONTENT_TYPE") {
			$headers_raw .= 'Content-Type: ' . $value . "\r\n";
		} else if ($name == "CONTENT_LENGTH") {
			$headers_raw .= 'Content-Length: ' . $value . "\r\n";
		}
	}
	
	// http://php.net/manual/en/context.http.php
	$context = stream_context_create(array(
		'http' => array(
			'method' => $_SERVER['REQUEST_METHOD'],
			'header' => $headers_raw,
			'ignore_errors' => true,
			'content' => file_get_contents('php://input')
		)
	));
	$content = file_get_contents($url, false, $context);
	
	$content_type = 'application/octet-stream';// "text/html"
	$content_type_raw = $content_type;// "text/html; charset=UTF-8"
	foreach($http_response_header as $response_header){
		if('Content-Type:' == substr($response_header, 0, 13)){
			$content_type_raw = substr($response_header, 14);
			$content_type = strstr($content_type_raw, ';', true);
			header($response_header);
		}
		elseif('Content-Encoding:' == substr($response_header, 0, 17) && 'gzip' == substr($response_header, 18, 4))
		{
			//Now lets uncompress the compressed data
			$content = gzinflate(substr($content, 10, -8));
		}
		elseif('Content-Length:' == substr($response_header, 0, 15))
		{
			//Skip it
		}
		else{
			header($response_header);
		}
	}
	
	// Content transforms
	//var_dump($url_parts);exit();
	if('text/html' == $content_type){
		echo str_replace('cat', 'dog', $content);
	}else{
		echo $content;
	}

`pac.php`:

	<?php header('Content-Type: application/x-javascript-config') ?>
	function FindProxyForURL(url, host)
	{ 
		 return "PROXY <?php echo $_SERVER['SERVER_ADDR'] ?>:<?php echo $_SERVER['SERVER_PORT'] ?>; DIRECT";
	}

- [Proxy auto-config - Wikipedia, the free encyclopedia](http://en.wikipedia.org/wiki/Proxy_auto-config)
- [PHP+Apache as forward/reverse proxy: ¿how to process client requests and server responses in PHP? - Server Fault](http://serverfault.com/questions/222823/phpapache-as-forward-reverse-proxy-how-to-process-client-requests-and-server)
- [jenssegers/php-proxy](https://github.com/jenssegers/php-proxy)

##### Internet Content Adaptation Protocol

Aka ICAP

- [Internet Content Adaptation Protocol - Wikipedia, the free encyclopedia](http://en.wikipedia.org/wiki/Internet_Content_Adaptation_Protocol)
- http://wiki.squid-cache.org/Features/ICAP
- [php-icap-server - Internet Content Adaptation Protocol Server implemented in PHP - Google Project Hosting](https://code.google.com/p/php-icap-server/)
- [icapjs/icap_server.js at master · LordEidi/icapjs](https://github.com/LordEidi/icapjs/blob/master/icap_server.js)

### HTTP/2.0

- [Performance testing HTTP/1.1 vs HTTP/2 vs HTTP/2 + Server Push for REST APIs](https://evertpot.com/h2-parallelism/)

#### Header compression

Aka HPACK

- [Headers](#headers)
- [mnot’s blog: Designing Headers for HTTP Compression](https://www.mnot.net/blog/2018/11/27/header_compression)
- [RFC 7541 - HPACK: Header Compression for HTTP/2](https://tools.ietf.org/html/rfc7541)
- [HPACK: the silent killer (feature) of HTTP/2](https://blog.cloudflare.com/hpack-the-silent-killer-feature-of-http-2/)
- [h2load - HTTP/2 benchmarking tool - HOW-TO — nghttp2 1.36.0-DEV documentation](https://nghttp2.org/documentation/h2load-howto.html)

#### Anonymous requests require clean connection

> Requests without credentials use a separate connection
> — [HTTP/2 push is tougher than I thought - JakeArchibald.com](https://jakearchibald.com/2017/h2-push-tougher-than-i-thought/#requests-without-credentials-use-a-separate-connection)

Fonts require to be loaded as CORS anonymous or require CORS authorization: [CSS Fonts Module Level 3](https://www.w3.org/TR/css-fonts-3/#font-fetching-requirements)

- [CORS Anonymous requests complicates preconnect · Issue #32 · w3c/resource-hints](https://github.com/w3c/resource-hints/issues/32)
- Chrome prefix `group_name` for `SOCKET->TRANSPORT_CONNECT_JOB group_name` as `pm/` (example of `pm/ssl/example.com:443` vs `ssl/example.com:443`, `pm/example.com:80` vs `example.com:80`) for anonymous connections `chrome://net-internals/#events&q=type:SOCKET,TRANSPORT_CONNECT_JOB`

#### Shared connection with multiple hosts 

Aka connection coalescing

Multiple hosts can use the same connection, but need the same IP (?) and (when HTTPS) require to use the same certificate (that use [Subject Alternative Names](https://en.wikipedia.org/wiki/Subject_Alternative_Name))
But may not support this.

> HTTP/2 supports multi-host multiplexing which further reduces RTTs. SPDY only supports single-host multiplexing.
> — [HTTP/2 - What Does it Mean for a CDN?](https://www.keycdn.com/blog/http2-cdn/)

- [linux - HTTP2: different domain but same IP, multiple connection or one connection? - Stack Overflow](https://stackoverflow.com/questions/48701719/http2-different-domain-but-same-ip-multiple-connection-or-one-connection)
- [HTTP/2 connection coalescing | daniel.haxx.se](https://daniel.haxx.se/blog/2016/08/18/http2-connection-coalescing/)
- [Shifting from SPDY to HTTP/2 | StackPath Blog](https://blog.stackpath.com/spdy-to-http2)
- [What is HTTP/2 - The Ultimate Guide by Kinsta](https://kinsta.com/learn/what-is-http2/)

## API

See also [API](../Development/Development.md#api)

`Location: https://...` for POST `201 Created` entity. https://restpatterns.mindtouch.us/HTTP_Status_Codes/201_-_Created

Infos and docs:

- [How to design a REST API | OCTO Talks !](https://blog.octo.com/en/design-a-rest-api/)
- [Web API - Wikipedia](https://en.wikipedia.org/wiki/Web_API)
- [API designs for low-connectivity | OCTO Talks !](https://blog.octo.com/en/api-designs-for-low-connectivity/) - How to handle API calls when the network fail
- [How To Design Better JavaScript APIs – Smashing Magazine](https://www.smashingmagazine.com/2012/10/designing-javascript-apis-usability/)
- [How to Create a custom Authentication Provider (current)](http://symfony.com/doc/current/security/custom_authentication_provider.html)
- http://techblog.appnexus.com/2012/on-restful-api-standards-just-be-cool-11-rules-for-practical-api-development-part-1-of-2/
- http://techblog.appnexus.com/2012/on-restful-api-standards-just-be-cool-11-rules-for-practical-api-development-part-2-of-2/
- [API Design is UI for Developers – Terence Eden's Blog](https://shkspr.mobi/blog/2012/03/api-design-is-ui-for-developers/#comment-15885)
- [API Design - Matt Gemmell](http://mattgemmell.com/api-design/)
- [You Really Should Log Client-Side Errors](http://openmymind.net/2012/4/4/You-Really-Should-Log-Client-Side-Error/)
- [Reverse-engineering Instagram to access the private API](http://blog.will3942.com/reverse-engineering-instagram)
- [The Definitive Guide to GET vs POST - Treehouse Blog](http://blog.teamtreehouse.com/the-definitive-guide-to-get-vs-post)
- [The art of creating simple but flexible APIs - Jos de Jong](http://josdejong.com/blog/2014/10/18/the-art-of-creating-simple-but-flexible-apis/)
- [APIs are about Policy — Acko.net](http://acko.net/blog/apis-are-about-policy/)

Tools:

- [API Monitoring and Testing · Runscope API Testing & Monitoring](https://www.runscope.com/)
- [A server side OAuth2 Bundle for Symfony2 ](https://github.com/FriendsOfSymfony/FOSOAuthServerBundle)
- [JSON API — A specification for building APIs in JSON](http://jsonapi.org/)
- [World's Most Popular API Framework | Swagger](https://swagger.io/)
- [Welcome | RAML](https://raml.org/) - "RESTful API Modeling Language (RAML) makes it easy to manage the whole API lifecycle from design to sharing."
- [API Blueprint | API Blueprint](https://apiblueprint.org/) - "A powerful high-level API description language for web APIs."

Examples:

- [API Events Proposal · DozroK/mp2013 Wiki](https://github.com/DozroK/mp2013/wiki/API-Events-Proposal) - opensource API of the opendata database of all events of Marseille Provence 2013
- [Events  |  Google Calendar API  |  Google Developers](https://developers.google.com/google-apps/calendar/v3/reference/events)
- [Flickr Services](https://www.flickr.com/services/api/)
- [Google Universal Analytics for AS3](https://github.com/zwetan/as3-universal-analytics)
- [guidelines/DINA-Web-API-Guidelines.md at master · DINA-Web/guidelines](https://github.com/DINA-Web/guidelines/blob/master/DINA-Web-API-Guidelines.md)
- [LiveDNS API](https://doc.livedns.gandi.net/#reference)

Paging:

- `Link` header with rel `next`, `prev`, `last`, `first`
- [GitHub API v3 | GitHub Developer Guide](https://developer.github.com/v3/#pagination)
- [RFC 5988 - Web Linking](https://tools.ietf.org/html/rfc5988#page-6)

Rate limit (quotas):

- for a resource
- for a user/token/etc. (context, allotted to)
- with a limit (max)
- within a period (window, per hour)
- reset (when the period is renewed)
- -> count / remaining
- HTTP headers `Retry-After` ([`toUTCString`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toUTCString)), `X-Rate-Limit` and `X-Rate-Limit-Remaining`
	- [Example of HTTP API Rate Limiting HTTP Response header - Stack Overflow](https://stackoverflow.com/questions/16022624/examples-of-http-api-rate-limiting-http-response-headers)
	- [Retry-After - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Retry-After)
- HTTP status code 429
	- [rest - Recommended HTTP status code for "plan limit exceeded" response - Software Engineering Stack Exchange](https://softwareengineering.stackexchange.com/questions/288376/recommended-http-status-code-for-plan-limit-exceeded-response)

See also:

- [Rate limiting - Wikipedia](https://en.wikipedia.org/wiki/Rate_limiting)
- [GitHub API v3 | GitHub Developer Guide](https://developer.github.com/v3/#rate-limiting)
- [Rate Limiting](https://developer.twitter.com/en/docs/basics/rate-limiting)

### RESTful

Aka REST, Hypermedia API

CRUD:

- create: `PUT` / `POST` (`201 Created` / `202 Accepted` + `Location: <URI to created resource>` or `303 See Other` + `Location: <URI to related resource>`)
- read (retrieve): `GET` (`200 OK`)
- update (modify): `PUT` / `POST` / `PATCH` (`200 OK`, `204 No Content`)
- delete (destroy): `DELETE`

Note: `PUT` is a 'replace' operation. It dictates what URI to use.

Could use `422 Unprocessable Entity` instead of `400 Bad Request` when the request body is valid (syntax is valid), but the server is unable to process the instruction. See [rest - 400 vs 422 response to POST of data - Stack Overflow](https://stackoverflow.com/questions/16133923/400-vs-422-response-to-post-of-data)

- [REST API Tutorial](http://www.restapitutorial.com/)
- [Create, read, update and delete - Wikipedia](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete)
- [api - Call a Server-side Method on a Resource in a RESTful Way - Stack Overflow](https://stackoverflow.com/questions/16877968/call-a-server-side-method-on-a-resource-in-a-restful-way)
- [Please. Don't Patch Like An Idiot. · William Durand](http://williamdurand.fr/2014/02/14/please-do-not-patch-like-an-idiot/)
- [The RESTful cookbook](http://restcookbook.com/)
- [Understanding And Using REST APIs — Smashing Magazine](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/)
- [angular-symfony/src/Flyers/FrontendBundle/Resources/public/js/services.js at master · FlyersWeb/angular-symfony](https://github.com/FlyersWeb/angular-symfony/blob/master/src/Flyers/FrontendBundle/Resources/public/js/services.js)
- [How I Explained REST to My Wife | Looah](http://www.looah.com/source/view/2284)
- [How RESTful is Your API? | BitNative by Cory House](http://www.bitnative.com/2012/08/26/how-restful-is-your-api/)
- [Proper response for a REST insert - full new record, or just the record id value? - Programmers Stack Exchange](http://programmers.stackexchange.com/questions/171122/proper-response-for-a-rest-insert-full-new-record-or-just-the-record-id-value)
- [REST APIs must be hypertext-driven » Untangled](http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven)
- [REST APIs with Symfony2- The Right Way | William DURAND](http://williamdurand.fr/2012/08/02/rest-apis-with-symfony2-the-right-way/)
- [RestWiki- Front Page](http://wayback.archive.org/web/20101125033613/http://rest.blueoxen.net/cgi-bin/wiki.pl?FrontPage)
- [RestWiki- Jeff Bone](http://wayback.archive.org/web/20110110160649/http://rest.blueoxen.net/cgi-bin/wiki.pl?JeffBone)
- [The HTTP OPTIONS method and potential for self-describing RESTful APIs | zacstewart.com](http://zacstewart.com/2012/04/14/http-options-method.html)
- [The Real-time Web in REST Services at IMVU | IMVU Engineering Blog](http://engineering.imvu.com/2014/12/27/the-real-time-web-in-rest-services-at-imvu/)
- [web services - Link headers vs link elements for RESTful JSON - Stack Overflow](https://stackoverflow.com/questions/9742380/link-headers-vs-link-elements-for-restful-json)
- [JSON API :: A standard for building APIs in JSON.](http://jsonapi.org/)
- [How your API could benefit from Hypermedia — Unexpected Token — Medium](https://medium.com/unexpected-token/how-your-api-could-benefit-from-hypermedia-b62780771ccb)
- [REST APIs must be hypertext-driven » Untangled](http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven)
- [The HTTP OPTIONS method and potential for self-describing RESTful APIs | zacstewart.com](http://zacstewart.com/2012/04/14/http-options-method.html)
- [The Real-time Web in REST Services at IMVU | IMVU Engineering Blog](http://engineering.imvu.com/2014/12/27/the-real-time-web-in-rest-services-at-imvu/)
- [Marcelo Cure: Software Engineer: REST anti-patterns](http://marcelo-cure.blogspot.fr/2016/09/rest-anti-patterns.html)
- [Principles of good RESTful API Design](https://codeplanet.io/principles-good-restful-api-design/)
- [Best Practices for Designing a Pragmatic RESTful API | Vinay Sahni](http://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api)
- [API design guidance | Microsoft Docs](https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design)
- [api-guidelines/Guidelines.md at master · Microsoft/api-guidelines](https://github.com/Microsoft/api-guidelines/blob/master/Guidelines.md)
- [Introduction · HTTP API Design](https://geemus.gitbooks.io/http-api-design/content/en/) - [interagent/http-api-design: HTTP API design guide extracted from work on the Heroku Platform API](https://github.com/interagent/http-api-design)
- [HTTP status code for update and delete? - Stack Overflow](https://stackoverflow.com/questions/2342579/http-status-code-for-update-and-delete)

#### Specs / docs format

And generators

- [Apiary — Home](http://apiary.io/)
- [API Blueprint - API Documentation with powerful tooling](https://apiblueprint.org/#hello_world)
- [RAML - RESTful API modeling language](http://raml.org/)
- [Swagger 2.0](http://swagger.io/)
- [Swagger- A simple, open standard for describing REST APIs with JSON | Reverb for Developers](https://helloreverb.com/developers/swagger)
- [mashery/iodocs](https://github.com/mashery/iodocs)
- [Mashape - Free API Management Platform & Marketplace](https://www.mashape.com/)
- [Web Application Description Language — Wikipedia](https://en.wikipedia.org/wiki/Web_Application_Description_Language)
- [RSDL - Wikipedia, the free encyclopedia](http://en.wikipedia.org/wiki/RSDL)
- https://github.com/nelmio/NelmioApiDocBundle

- [Paw – The ultimate REST client for Mac](http://luckymarmot.com/paw)

- [API Spec Comparison Tool | MIKESTOWE.COM](http://www.mikestowe.com/2014/12/api-spec-comparison-tool.php)
- [RAML vs. Swagger vs. API Blueprint | MIKESTOWE.COM](http://www.mikestowe.com/2014/07/raml-vs-swagger-vs-api-blueprint.php)

- [Home · wordnik/swagger-core Wiki](https://github.com/wordnik/swagger-core/wiki)

Hypermedia and 

- [The Hypertext Application Language](http://stateless.co/hal_specification.html)
- [JSON:API — A specification for building APIs in JSON](https://jsonapi.org/)
- [kevinswiber/siren: Structured Interface for Representing Entities, super-rad hypermedia](https://github.com/kevinswiber/siren)
- [RFC 8288 - Web Linking](https://tools.ietf.org/html/rfc8288)
- HTML5 links

#### API examples

`http://lifeforms.org/<alias>` redirect to (305) `http://lifeforms.org/<Kingdom>/<Phylum>/<Class>/<Order>/<Family>/<Genus>/<Species>`

- [RESTBase docs](https://en.wikipedia.org/api/rest_v1/) - [REST API - MediaWiki](https://www.mediawiki.org/wiki/REST_API)
- [API References and Guides - PayPal Developer](https://developer.paypal.com/reference/)
- [GitHub API v3 | GitHub Developer Guide](https://developer.github.com/v3/) and https://api.github.com/
- [timdorr/model-s-api](https://github.com/timdorr/model-s-api)
- [Tesla Model S JSON API—by apiary.io](http://docs.timdorr.apiary.io/)
- [API REST](https://www.creditagricolestore.fr/castore-data-provider/docs/V1/rest.html)
- [Rest api - Redmine](http://www.redmine.org/projects/redmine/wiki/Rest_api)
- [Developers - REST API Reference - Thingiverse](http://www.thingiverse.com/developers/rest-api-reference)
- [DELETE Object - Amazon Simple Storage Service](http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectDELETE.html)
- https://github.com/WhiteHouse/api-standards
- https://github.com/Microsoft/api-guidelines

#### Security

There is no session

- [rest - Do sessions really violate RESTfulness? - Stack Overflow](https://stackoverflow.com/questions/6068113/do-sessions-really-violate-restfulness)
- [web applications - Should cookies be used in a RESTful API? - Software Engineering Stack Exchange](https://softwareengineering.stackexchange.com/questions/141019/should-cookies-be-used-in-a-restful-api)
- [zanox OAuth with REST - zanox Developer Portal](https://developer.zanox.com/authentication/zanox-oauth/oauth-rest) - [RESTful API authentication - Wiki.zanox.com](http://wiki.zanox.com/en/RESTful_API_authentication)
- [rest - RESTful Authentication - Stack Overflow](https://stackoverflow.com/questions/319530/restful-authentication/7158864#7158864)
- [Secure Your REST API... The Right Way - Stormpath User Identity API](https://stormpath.com/blog/secure-your-rest-api-right-way/)
- [Remote access API - Jenkins - Jenkins Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Remote+access+API)
- [Documentation | Words API](https://www.wordsapi.com/docs)

#### Implementation / libs

- [Homepage - Silex - The PHP micro-framework based on Symfony2 Components](http://silex.sensiolabs.org/)
- [Slim Framework - Slim Framework](http://www.slimframework.com/)
- [Apigility](https://www.apigility.org/)
- [badgateway/ketting: Ketting is a Hypermedia client for javascript](https://github.com/badgateway/ketting)

- [Create a REST API with PHP « Gen X Design | Ian Selby](http://wayback.archive.org/web/20150428075600/http://www.gen-x-design.com/archives/create-a-rest-api-with-php/)
- [Building A RESTful PHP Server: Understanding the Request - LornaJaneLornaJane](http://www.lornajane.net/posts/2012/building-a-restful-php-server-understanding-the-request)

### WebHook

- [WebSub](https://www.w3.org/TR/websub/) - Open protocol for distributed pub–sub communication on the internet
- [WebSub Rocks!](https://websub.rocks/)

## User Agent String

Can be used server side to detect browser, bot, etc.

Apple Shortcuts App: `Shortcuts/700 CFNetwork/974.2.1 Darwin/18.0.0`

See [Detection](#detection)

- [WebAIM: History of the browser user-agent string](http://webaim.org/blog/user-agent-string-history/)
- [User agent - Wikipedia, the free encyclopedia](http://en.wikipedia.org/wiki/User_agent)
- [The Mobile Web should just work for everyone - IEBlog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/ie/archive/2014/07/31/the-mobile-web-should-just-work-for-everyone.aspx)
- [Tech Stuff - Browser ID Strings (a.k.a. User Agent ID)](http://www.zytrax.com/tech/web/browser_ids.htm)
- [The User Agent Search Engine](http://ua.theafh.net/)
- [List of User-Agents](http://www.user-agents.org/allagents.xml)
- [Understanding user-agent strings (Internet Explorer)](https://msdn.microsoft.com/en-us/library/ms537503%28v=vs.85%29.aspx)
- [User agent — Wikipedia](https://en.wikipedia.org/wiki/User_agent)
- [Full Featured PHP Browser Detection & OS Detection](https://github.com/smxi/php-browser-detection)
- [lightweight PHP class for detecting mobile devices](https://github.com/serbanghita/Mobile-Detect)
- [User-Agent - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent) and [Firefox user agent string reference - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent/Firefox)
- [Botopedia - Complete bot identifier | Bot User Agent Checker](http://www.botopedia.org/)
- [List of User Agent Strings :: udger.com](https://udger.com/resources/ua-list)
- [UserAgent parsing done right](https://github.com/ThaDafinser/UserAgentParser)
- [Comparison results from UserAgentParser](https://github.com/ThaDafinser/UserAgentParserComparison)
- Not up to date [UserAgentString.com - List of User Agent Strings](http://www.useragentstring.com/pages/useragentstring.php)
- [Mobile Detect - lightweight PHP class for detecting mobile devices (including tablets)](http://mobiledetect.net/) and https://github.com/serbanghita/Mobile-Detect
- [UserAgentString.com](http://www.useragentstring.com/)
- [User-Agent detection, history and checklist ★ Mozilla Hacks – the Web developer blog](https://hacks.mozilla.org/2013/09/user-agent-detection-history-and-checklist/)
- [Google crawlers - Search Console Help](https://support.google.com/webmasters/answer/1061943?hl=en)
- [User Agent: archive.org_bot : Free Data : Download & Streaming : Internet Archive](https://archive.org/details/archive.org_bot)
- [Samsung DeX brings a new Dimension to the Mobile Web](https://medium.com/samsung-internet-dev/samsung-dex-brings-a-new-dimension-to-the-mobile-web-f80d7edcab29)

- [Web crawler — Wikipedia](https://en.wikipedia.org/wiki/Web_crawler)
- [WebAIM: History of the browser user-agent string](http://webaim.org/blog/user-agent-string-history/)

## URI/URL

URI Template format definition: [RFC 6570 - URI Template](https://tools.ietf.org/html/rfc6570)

- absolute URL: `http://domain/path/to/some/resource` https://url.spec.whatwg.org/#concept-absolute-url
- scheme-relative (or Network-path reference or protocol-relative) URL : `//domain/path/to/some/resource` https://url.spec.whatwg.org/#concept-scheme-relative-url
	Use it but http://www.paulirish.com/2010/the-protocol-relative-url/
- absolute-path-relative URL: `/path/to/some/resource` https://url.spec.whatwg.org/#concept-absolute-path-relative-url
- path-relative URL: `path/to/some/resource` https://url.spec.whatwg.org/#concept-path-relative-url

- origin-form: path and query string of the URI. The query string may or may not be present.
- absolute-form: an absolute URI.
- authority-form: the authority part of a URI, made up of a maximum of 3 parts – user-info (optional), host and port (optional). The user-info may require a password too – user:password. We end up with a pattern of user:password@host:port. The user-info may also have require an
- asterisk-form: just the string, *

- same origin: same scheme, host, and port. [URL Standard](https://url.spec.whatwg.org/#host-same-site) and [HTML Standard](https://html.spec.whatwg.org/multipage/origin.html#same-origin)
- same origin-domain: [HTML Standard](https://html.spec.whatwg.org/multipage/origin.html#same-origin-domain)
- same site: same registrable domain. [URL Standard](https://url.spec.whatwg.org/#host-same-site)

`scheme:[//[user:password@]host[:port]][/]path[?query][#fragment]`

- `http://[::1]:80/`, `http://[::]:80/`, `http://0.0.0.0:80/`, `http://127.0.0.1/`, `http://localhost/`, `http://3232235778/` (IP decimal notation, is the same as `http://192.168.1.2/` [how to convert](https://www.mkyong.com/java/java-convert-ip-address-to-decimal-number/))
- `mysql://user:pass@host/mydatabase`
- `smtps://username:password@smtp.example.com/?pool=true`
- `memcached://localhost:11211/meta`
- `redis://user:secret@localhost:6379/0?foo=bar&qux=baz` https://www.iana.org/assignments/uri-schemes/prov/redis
- [Uniform Resource Identifier (URI) Schemes](https://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml)
- https://github.com/sidorares/node-mysql2/blob/9218f055ceeb95ae7205348e06c07b89b799d031/lib/connection_config.js#L88-L118
- [IPv4 - Wikipedia](https://en.wikipedia.org/wiki/IPv4#Addressing)

Note: https://-inevitablelament.tumblr.com/ is a valid URL (subdomain start with minus char), see [Bug #668926 “can't resolve domain names starting with a dash (mi...” : Bugs : resolvconf package : Ubuntu](https://bugs.launchpad.net/ubuntu/+source/resolvconf/+bug/668926)

### Scheme-relative URLs

Aka protocol-relative URLs.

**It's recommended to always use `https://` URLs**.

This not work if the protocol is not the same. Example: in email this URLs are not supported

- [Stop Using the Protocol-relative URL - Jeremy Wagner](https://jeremywagner.me/blog/stop-using-the-protocol-relative-url)
- [The protocol-relative URL - Paul Irish](http://www.paulirish.com/2010/the-protocol-relative-url/)
- [Protocol Relative URLs, Why to Use Them, and Common Pitfalls - Bill Patrianakos](http://billpatrianakos.me/blog/2013/04/18/protocol-relative-urls/)
- [Wikipedia:Protocol-relative URL — Wikipedia](https://en.wikipedia.org/wiki/Wikipedia:Protocol-relative_URL)
- http://tools.ietf.org/html/rfc3986#section-4.2
- https://url.spec.whatwg.org/#concept-scheme-relative-url

Don't use it in email (could be resolve as file protocol: `file:///...`)

### Domain

Naked domain = domain without subdomain (eg. `www.`).
Aka apex domain, base, bare, naked, root apex, or zone apex

|--------------------|-----------------------|-------------------|
| Domain			 | Registrable domain	 | Public suffix	 |
|--------------------|-----------------------|-------------------|
| edition.cnn.com	 | cnn.com				 | com				 |
| money.cnn.com		 | cnn.com				 | com				 |
| w3c.github.io		 | w3c.github.io		 | github.io		 |
| tc39.github.io	 | tc39.github.io		 | github.io		 |
|--------------------|-----------------------|-------------------|

Note: [public suffix](https://en.wikipedia.org/wiki/Public_Suffix_List) aka effective top-level domain (eTDL).

- [www. is not deprecated – really](http://www.yes-www.org/) and [Why use www? | Hacker News](https://news.ycombinator.com/item?id=11004396)
- Suffixes, like `.com`, `.co.uk`, `pvt.k12.ma.us`, etc. [Public Suffix List](https://publicsuffix.org/)
- [Second-level domain — Wikipedia](https://en.wikipedia.org/wiki/Second-level_domain)

### Password

HTTP Authentification

`http://user:password@example.com`
`http://user:p%40ssword@example.com` (user, p@ssword)

Encode special chars: `mypass#gh647` to `mypass%23gh647`

### Write URI well

See [RESTful](Development#restful) and [API](Development#api)

- [Good Practice for Capability URLs](https://www.w3.org/TR/capability-urls/)
- [Use Canonical URLs, Please](http://gadgetopia.com/post/7390)
- [Benefits of Plain English URLs](http://gadgetopia.com/post/6346)
- [The Peril of Self-Replicating Hyperlinks](http://gadgetopia.com/post/6374)
- [Semantic URL — Wikipedia](https://en.wikipedia.org/wiki/Semantic_URL)
- [Choosing between www and non-www URLs - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Choosing_between_www_and_non-www_URLs#Using_%3Clink_relcanonical%3E)
- [Set your preferred domain (www or non-www) - Search Console Help](https://support.google.com/webmasters/answer/44231?hl=en)
- [How To Create Your Own URL Scheme | CSS-Tricks](https://css-tricks.com/create-url-scheme/)
- Slug [Semantic URL — Wikipedia](https://en.wikipedia.org/wiki/Semantic_URL#Slug)
- [URLs are UI - Scott Hanselman](https://www.hanselman.com/blog/URLsAreUI.aspx)
- https://restpatterns.mindtouch.us/Articles/Designing_URIs

## Subordinate resource

Aka subresource, hash, fragment identifier

Aka fragment

Selectors:

- [RFC 3236 - The 'application/xhtml+xml' Media Type](https://tools.ietf.org/html/rfc3236) - HTML: `page.html#namedSection`
- [RFC 3778 - The application/pdf Media Type](https://tools.ietf.org/html/rfc3778) - PDF: `slides.pdf#page=10&viewrect=50,50,640,480`
- [RFC 5147 - URI Fragment Identifiers for the text/plain Media Type](https://tools.ietf.org/html/rfc5147#section-2) - Plain Text: `text.txt#char=0,10`, `text.txt#line=10,20`
- [RFC 3023 - XML Media Types](https://tools.ietf.org/html/rfc3023) - XML: `page.xml#xpointer(/a/b/c)`, `page.html#xpointer(string-range(//,"target text"))`
- [RFC 3870 - application/rdf+xml Media Type Registration](https://tools.ietf.org/html/rfc3870) - RDF/XML: `data.rdf#namedResource`
- [RFC 7111 - URI Fragment Identifiers for the text/csv Media Type](https://tools.ietf.org/html/rfc7111) - CSV: `data.csv#row=5-7`
- [Media Fragments URI 1.0 (basic)](https://www.w3.org/TR/media-frags/) - Media: `image.jpg#xywh=50,50,640,480`, `video.ogv#t=60,100`
- [Linking – SVG 1.1 (Second Edition)](https://www.w3.org/TR/SVG11/linking.html#SVGFragmentIdentifiers) - SVG: `image.svg#svgView(viewBox(50,50,640,480))`
- [EPUB Canonical Fragment Identifier (epubcfi) Specification](http://www.idpf.org/epub/linking/cfi/epub-cfi-20140628.html) - EPUB3: `book.epub#epubcfi(/6/4[chap01ref]!/4[body01]/10[para05]/3:10)`
- [Selectors and States](https://www.w3.org/TR/selectors-states/#frags) - Media, Text, RDF/HTML/XML: `page.html#selector(type=CssSelector,value=%23elemid%20>%20.elemclass%20+%20p)`
- [Web Annotation Data Model](https://www.w3.org/TR/annotation-model/#fragment-selector)
- [Using CSS Selectors as Fragment Identifiers](http://simonstl.com/articles/cssFragID.html) - `page.html#css(.myclass)`
	- [CSS Selectors as Fragment Identifiers Community Group](https://www.w3.org/community/cssselfrags/)
	- [Laurian/CSSFrag: Fork of Shaun Inman 'CSS Selectors as Fragment Identifiers' implementation.](https://github.com/Laurian/CSSFrag)
- [npm-package.json | npm Documentation](https://docs.npmjs.com/files/package.json#git-urls-as-dependencies) - Github repo `github.com/npm/cli#semver:^5.0`
- [fragmention - IndieWeb](https://indieweb.org/fragmention) - `page.html##text`
- [NYTimes/Emphasis: Dynamic Deep-Linking and Highlighting](https://github.com/NYTimes/Emphasis) - HTML/XML `page.html#h5s1,2`
- [bokand/ScrollToTextFragment: Proposal to allow specifying a text snippet in a URL fragment](https://github.com/bokand/ScrollToTextFragment) - `page.html#targetText=percent%20encoded`
- [RFC 6901 - JavaScript Object Notation (JSON) Pointer](https://tools.ietf.org/html/rfc6901) - JSON: `data.json#/foo/0`
- `jar:https://domain.com/path/to/jar.jar!/Pictures/a.jpg` (`jar:<url>!/{entry}`)
- `zip:password@http://domain.com/path/to/file#/Pictures/a.jpg`
- `swf:http://domain.com/path/to/file.swf#com.domain.ClassName` and `http://domain.com/path/to/file.swc#com.domain.ClassName`
- [xpath.js](https://gist.github.com/antimatter15/223708) - HTML/XML: `page.html#xpath:/html/body/p[3]`. [XPath Bookmark Bookmarklet – Blog](http://antimatter15.com/wp/2009/11/xpath-bookmark-bookmarklet/#xpath:/html/body/div/div[3]/div/div/div/div/p[6]/strong/em)

More infos:

- [Fragment identifier - Wikipedia](https://en.wikipedia.org/wiki/Fragment_identifier)
- [Best Practices for Fragment Identifiers and Media Type Definitions](https://www.w3.org/TR/fragid-best-practices/)
- [List of valid characters for the fragment identifier in an URL? - Stack Overflow](https://stackoverflow.com/questions/2849756/list-of-valid-characters-for-the-fragment-identifier-in-an-url)
- [brettz9/jump-to-anchor: Jump to the closest anchor for a selected element](https://github.com/brettz9/jump-to-anchor)
- [Rumperuu/Pinpointer: A browser extension to create and share links to arbitrary bits of webpages.](https://github.com/Rumperuu/Pinpointer) - [Developing Pinpointer – bengoldsworthy.net](https://bengoldsworthy.net/2018/04/developing-pinpointer/)
- [karanlyons/pinpoint: Link anywhere.](https://github.com/karanlyons/pinpoint)
- [ericclemmons/unique-selector: Given a DOM node, return a unique CSS selector matching only that element](https://github.com/ericclemmons/unique-selector)
- [Find an element / text](../../Development/JavaScript/JavaScript.md#find-an-element--text)

### Data URI

On some browser, data URI are considered from different domain. See [javascript - Programmatically accessing an iframe that uses a data URI as a source - Stack Overflow](https://stackoverflow.com/questions/14149523/programmatically-accessing-an-iframe-that-uses-a-data-uri-as-a-source/14149618#14149618).

	application/font-woff

	data:application/pdf;name=document.pdf;base64,BASE64_DATA_ENCODED

- Firefox require hash to be encoded/escaped
- IE require more chars to be encoded/escaped

- [CSS # Sprites vs Data URI](CSS#sprites-vs-data-uri)
- [Formats and protocols/URI](#data)
- [SVG gradient and backgrounds]()
- [Optimizing SVGs in data URIs by Taylor Hunt on CodePen](http://codepen.io/Tigt/blog/optimizing-svgs-in-data-uris)
- [Probably Don't Base64 SVG | CSS-Tricks](https://css-tricks.com/probably-dont-base64-svg/)
- [Getting URL encoded SVG to work in IE](http://codepen.io/chriscoyier/pen/ZQgvyG/)
- [Blue Box Data URI (svg](http://codepen.io/AmeliaBR/details/xijuv/)
- [Sass function to encode SVG as a data uri without it being in base64](https://github.com/waldemarfm/sass-svg-uri)

#### Data URI base 64 encoding

See [Base64](Base64)

Works with IE 9+ and others browsers

	background: red url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHZpZXdCb3g9JzAgMCAxMDAgMTAwJz48cmVjdCBmaWxsPSdncmVlbicgd2lkdGg9JzEwMCcgaGVpZ2h0PScxMDAnLz48L3N2Zz4=");

- [Base64 Encoding & Performance, Part 1: What’s Up with Base64? – CSS Wizardry – CSS Architecture, Web Performance Optimisation, and more, by Harry Roberts](https://csswizardry.com/2017/02/base64-encoding-and-performance/)
- [Base64 Encoding & Performance, Part 2: Gathering Data – CSS Wizardry – CSS Architecture, Web Performance Optimisation, and more, by Harry Roberts](https://csswizardry.com/2017/02/base64-encoding-and-performance-part-2/)

#### Data URI percentage encoding

Using `encodeURIComponent()`

Escapes all characters (including UTF-8 sequences) except the following: alphabetic, decimal digits, `-`, `_`, `.`, `!`, `~`, `*`, `'`, `(`, `)`.

Note:

For data URI contains SGML like documents, (if it's allowed) you can use simple quote instead of double quotes for attributes values or mix both.
This reduce the number of chars used by encoding 1 (`'`) vs. 3 (`%22`). If the data URI must be quoted, double quote can be used with additional encoding: Example with CSS: use `url("data:...value%3D'data'")` with double quotes, simple quotes are not escaped.
See [xhtml - How to properly escape quotes inside html attributes? - Stack Overflow](https://stackoverflow.com/questions/4015345/how-to-properly-escape-quotes-inside-html-attributes)

It's possible to not encode all chars.

Some browsers require some encoded chars:

- Firefox require `#` to be encoded
- IE 11 & Edge require `%` to be encoded (no invalid escape sequences, eg. `width='100%' `, must be `height='100%25' ` instead)

It's safe to keep unencoded:

- ` ` (space, `%20`)
- `=` (`%3D`)
- `:` (`%3A`)
- `/` (`%2F`)

> For security reasons, data URIs are restricted to downloaded resources. Data URIs cannot be used for navigation, for scripting, or to populate frame or iframe elements.
> 
> Data URIs cannot be larger than 32,768 characters.
> 
> The resource data must be properly encoded; otherwise, an error occurs and the resource is not loaded. The "#" and "%" characters must be encoded, as well as control characters, non-US ASCII characters, and multibyte characters. 
— [data Protocol](https://msdn.microsoft.com/en-us/library/cc848897%28v=vs.85%29.aspx)

	copy("data:image/svg+xml," + encodeURI(`<svg xmlns="...</svg>`.replace(/"/g, "'").replace(/(^|>)\s+(<|$)/g, "$1$2")).replace(/%20/g, " ").replace(/#/g, "%23"));

- [Percent-encoding — Wikipedia](https://en.wikipedia.org/wiki/Percent-encoding#Types_of_URI_characters)
- [encodeURIComponent() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent)
- [encodeURI() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURI)
- [Optimizing SVGs in data URIs by Taylor Hunt on CodePen](https://codepen.io/tigt/post/optimizing-svgs-in-data-uris)
- [URL-encoder for SVG](http://yoksel.github.io/url-encoder/)
- [Probably Don't Base64 SVG | CSS-Tricks](https://css-tricks.com/probably-dont-base64-svg/)

### MHTML URI

Multipart document

IE?-8 only

	/*
	Content-Type: multipart/related; boundary="_ANY_STRING_WILL_DO_AS_A_SEPARATOR"
	
	--_ANY_STRING_WILL_DO_AS_A_SEPARATOR
	Content-Location:locoloco
	Content-Transfer-Encoding:base64
	
	iVBORw0KGgoAAAANSUhEUgAAAAQAAAADCAIAAAA7ljmRAAAAGElEQVQIW2P4DwcMDAxAfBvMAhEQMYgcACEHG8ELxtbPAAAAAElFTkSuQmCC
	--_ANY_STRING_WILL_DO_AS_A_SEPARATOR
	Content-Location:polloloco
	Content-Transfer-Encoding:base64
	
	iVBORw0KGgoAAAANSUhEUgAAABkAAAAUBAMAAACKWYuOAAAAMFBMVEX///92dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnYvD4PNAAAAD3RSTlMAACTkfhvbh3iEewTtxBIFliR3AAAAUklEQVQY02NgIBMwijgKCgrAef5fkHnz/y9E4kn+/4XEE6z/34jEE///A4knev7zAwQv7L8RQk40/7MiggeUQpjJff+zIpINykbIbhFSROIRDQAWUhW2oXLWAQAAAABJRU5ErkJggg==
	*/
	
	#test1 {
		background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAQAAAADCAIAAAA7ljmRAAAAGElEQVQIW2P4DwcMDAxAfBvMAhEQMYgcACEHG8ELxtbPAAAAAElFTkSuQmCC"); /* normal */
		*background-image: url(mhtml:http://phpied.com/files/mhtml/mhtml.css!locoloco); /* IE < 8 */
	}
	
	#test2 {
		background-image: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABkAAAAUBAMAAACKWYuOAAAAMFBMVEX///92dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnZ2dnYvD4PNAAAAD3RSTlMAACTkfhvbh3iEewTtxBIFliR3AAAAUklEQVQY02NgIBMwijgKCgrAef5fkHnz/y9E4kn+/4XEE6z/34jEE///A4knev7zAwQv7L8RQk40/7MiggeUQpjJff+zIpINykbIbhFSROIRDQAWUhW2oXLWAQAAAABJRU5ErkJggg=="); /* normal */
		*background-image: url(mhtml:http://phpied.com/files/mhtml/mhtml.css!polloloco); /* IE < 8 */
	}

- [MHTML — Wikipedia](https://en.wikipedia.org/wiki/MHTML)
- [MHTML – when you need data: URIs in IE7 and under / Stoyan's phpied.com](http://www.phpied.com/mhtml-when-you-need-data-uris-in-ie7-and-under/)

### `mailto:` protocol

See [mailto](URI#mailto)

Note: Be carefull with non encoded chars. Chrome don't open mailto url if not all required chars that require encoding are not.

You can open mailto in `_self` or `_blank` window. If an protocol handler is enable to `mailto:` this should open the related page (in self or blank, based on the target window).

- as link `<a href="mailto:?subject=Hello&body=Hello%20world!" target="_blank">maitlo</a>`
- as script `window.open("mailto:?subject=Hello&body=Hello%20World!", "_blank")`
- as form `<form action="mailto:" target="_blank"><input type="hidden" name="subject" value="hello"><input type="hidden" name="body" value="Hello world!"><button>mailto</button></form>`.
	**It's not a usefull method for the following reasons:**

	- with GET, spaces fields name and values will be replace with `+`.
	- for file fields (`<input type="file">`), the value will be replace with the name of the selected file
	- with POST and with encoding type `text/plain`, the body will contains all fields: one per line with `name=value`

Target can be omited (default to `_self`).

### `tel:` protocol

See [tel](URI#tel)

### Well known

Aka `/.well-known/`

Site-wide metadata files

- [Well-Known URIs](https://www.iana.org/assignments/well-known-uris/well-known-uris.xhtml)
- `www.mysite.com/robots.txt` symlink to `www.mysite.com/.well-known/robots.txt` (only 301 redirection are recommended, see [robots.txt](#robots-txt))
- [App Search Programming Guide: Support Universal Links](https://developer.apple.com/library/content/documentation/General/Conceptual/AppSearch/UniversalLinks.html) - `/.well-known/apple-app-site-association`
- [Getting Started | Google Digital Asset Links | Google Developers](https://developers.google.com/digital-asset-links/v1/getting-started) - `/.well-known/assetlinks.json`
- [WebFinger](https://webfinger.net/) - `https://<domain>/.well-known/webfinger?resource=<resource>` (where resource value - URI encoded - is `acct:<email-address>`)

### About URI

- `about:blank`
- `about:invalid`

- [about URI scheme - Wikipedia](https://en.wikipedia.org/wiki/About_URI_scheme)
- ["about" URI Tokens](https://www.iana.org/assignments/about-uri-tokens/about-uri-tokens.xhtml)

## PDF

- [Parameters for Opening PDF Files - pdf_open_parameters_v9.pdf](http://wwwimages.adobe.com/www.adobe.com/content/dam/Adobe/en/devnet/acrobat/pdfs/pdf_open_parameters_v9.pdf)

## Media type

Aka MIME type, content type

- [Media type](../Development/htaccess.md#media-type)
- [Media type](../Formats,%20encoding%20and%20protocols/Formats,%20encoding%20and%20protocols.md#media-type)
- `application/x-www-form-urlencoded`
- `text/event-stream` used by [server-sent events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events) (Set charset could be required `text/event-stream; charset=utf-8`)

Some subtypes support optional parameters`image/webp;animation=y`, `image/webp;version=0.3`

- [Properly Configuring Server MIME Types - Web security | MDN](https://developer.mozilla.org/en-US/docs/Web/Security/Securing_your_site/Configuring_server_MIME_types)

### Charset case

Note: `utf-8` or `UTF-8`? (**Don't use `UTF8` nor `utf8`**). Prefer [`UTF-8`](http://www.iana.org/assignments/character-sets/character-sets.xhtml). It's case insensitive, stick to one.

- [Is “UTF-8” case-sensitive in XML declaration? | Coding Out Loud](https://blog.codingoutloud.com/2009/04/08/is-utf-8-case-sensitive-in-xml-declaration/)
- [Setting the HTTP charset parameter](https://www.w3.org/International/articles/http-charset/index.en)
- [XML file encoding format "utf-8" VS "UTF-8"? - Stack Overflow](https://stackoverflow.com/questions/3251954/xml-file-encoding-format-utf-8-vs-utf-8)
- [HTTP: Are Character Set Names Case-Sensitive? - Stack Overflow](https://stackoverflow.com/questions/19391221/http-are-character-set-names-case-sensitive)
- > Canonical names are, by convention, usually in upper case.
	— [Charset (Java Platform SE 7 )](https://docs.oracle.com/javase/7/docs/api/java/nio/charset/Charset.html)

### Multipart resource

Works only for images (used by MJPEG images):

	Content-Type: multipart/x-mixed-replace;boundary=xxboundaryxx
	
	--xxboundaryxx
	
	Content-Type: image/jpeg
	Content-Length: 1000
	
	JIFFdata..frame1.1000
	
	--xxboundaryxx
	
	Content-Type: image/jpeg
	Content-Length: 1000
	
	JIFFdata..frame2.1000
	
	--xxboundaryxx
	

It's used also for form upload with `multipart/form-data` used only by HTTP requests

### Multiple Choices

	HTTP/1.1 300 Multiple Choices
	Link: <http://example.org/books/1234>; rel="alternate"; type="application/hal+json", <http://example.org/books/1234>; rel="alternate"; type="application/hal+xml", <http://example.org/books/1234>; rel="alternate"; type="application/atom+xml;type=entry"

	HTTP/1.1 300 Multiple Choices
	Content-type: text/uri-list
	
	# metadata
	URI1
	# metadata
	URI2

- [RFC 2483 - URI Resolution Services Necessary for URN Resolution # The `text/uri-list` Internet Media Type](http://tools.ietf.org/html/rfc2483#section-5)

### External-Body type

Note: It's used by emails

Set `Content-Type` to:

	message/external-body; access-type=URL; URL="http://www.foo.com/file"

	message/external-body; access-type=local-file; name="file:/local/path/file.html"

- [RFC 2017 - Definition of the URL MIME External-Body Access-Type](https://tools.ietf.org/html/rfc2017)

## How a web browser works

inter-frame, event loop

Event loop: frame (vsynced): input (events) → Javascript and rAF → Frame commit (style, layout, paint, compose) (→ idle callbacks?); then other frame (vsynced)
Note: With the exception of intersection observers & element resize observers, which happen after raf.

Caches: ( Application DNS cache) → ( libc DNS cache ) → ( gateway DNS cache ) → ( DNS caching resolver cache ) → ( DNS nameserver authoritative cache ) → Filesystem Cache → Hard disk Device Cache → ( JavaScript JIT cache ) → HTTP cache → HTTP push cache → HTTP Preload cache → CPU L1 → CPU L2 → (CPU L3) → ( HTTP proxy cache ) → (N hops invoking many of these steps N times) → ( HTTP router/relay cache ) → ( HTTP Reverse Proxy cache ) → HTTP Server request caching. (add also CSS cache and Image cache)

See [How ECMAScript engine works](ECMAScript#how-engine-works) (event loop, etc.)

- [Design Documents - The Chromium Projects](http://www.chromium.org/developers/design-documents)
- [How Web Works](https://github.com/vasanthk/how-web-works)
- [How Browsers Work: Behind the scenes of modern web browsers - HTML5 Rocks](http://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)
- [What happens when you type google.com into your browser and press enter?](https://github.com/alex/what-happens-when)
- [Rendering performance | Web Fundamentals - Google Developers](https://developers.google.com/web/fundamentals/performance/rendering/)
- [Constructing the Object Model | Web Fundamentals - Google Developers](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/constructing-the-object-model?hl=en) and https://github.com/google/WebFundamentals/blob/master/src/content/en/fundamentals/performance/critical-rendering-path/constructing-the-object-model.markdown and 
- [Debounce your input handlers | Web Fundamentals - Google Developers](https://developers.google.com/web/fundamentals/performance/rendering/debounce-your-input-handlers?hl=en)
- [Aerotwist - The Anatomy of a Frame](https://aerotwist.com/blog/the-anatomy-of-a-frame/)
- https://w3c.github.io/requestidlecallback/#figure1
- [Smoother scrolling in Firefox 46 with APZ ★ Mozilla Hacks – the Web developer blog](https://hacks.mozilla.org/2016/02/smoother-scrolling-in-firefox-46-with-apz/)
- [Working with multiprocess Firefox - Mozilla | MDN](https://developer.mozilla.org/en-US/Add-ons/Working_with_multiprocess_Firefox)
- [About Layout in Firefox](http://fr.slideshare.net/mijia/about-layout-in-firefox/)
- [Overview of Events and Handlers - Web developer guides | MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Overview_of_Events_and_Handlers)
- [Waterfall - Firefox Developer Tools | MDN](https://developer.mozilla.org/en-US/docs/Tools/Performance/Waterfall)
- [Chromium docs](https://github.com/ds-hwang/wiki/wiki/Chromium-docs)
- [requestAnimationFrame Scheduling For Nerds – Medium](https://medium.com/@paul_irish/requestanimationframe-scheduling-for-nerds-9c57f7438ef4#.4rtn8enir)
- [High-performance browser-grade HTML5 parser](https://github.com/servo/html5ever)
- [Lazy frame construction - Google Groups](https://groups.google.com/forum/#!topic/mozilla.dev.tech.layout/k_ZKKNQOpjw)
- [Call stack from a URL typed by a user to the HTTP request](https://gist.github.com/mildred/1c12cd7b4af6f24c145b)
- [Design Elements](https://github.com/v8/v8/wiki/Design%20Elements) - About V8, ECMAScript engine used in Chromium and NodeJS
- [requestAnimationFrame Scheduling For Nerds – Paul Irish – Medium](https://medium.com/@paul_irish/requestanimationframe-scheduling-for-nerds-9c57f7438ef4)
- HTML parser
	- [Idiosyncrasies of the HTML parser - The HTML Parser Book](https://htmlparser.info/)
- How JavaScript works
	- [How JavaScript works: the rendering engine and tip to optimize it performance](https://blog.sessionstack.com/how-javascript-works-the-rendering-engine-and-tips-to-optimize-its-performance-7b95553baeda?gi=f9dbf39c03c1)
	- [How JavaScript works: tracking change in the DOM using MutationObserver](https://blog.sessionstack.com/how-javascript-works-tracking-changes-in-the-dom-using-mutationobserver-86adc7446401)
	- [How JavaScript works: Service Workers, their lifecycle and use cases](https://blog.sessionstack.com/how-javascript-works-service-workers-their-life-cycle-and-use-cases-52b19ad98b58?gi=ecd8ff7038fa)
	- [How JavaScript works: The building block of Web Worker + 5 case when you should use them](https://blog.sessionstack.com/how-javascript-works-the-building-blocks-of-web-workers-5-cases-when-you-should-use-them-a547c0757f6a?gi=383f1a02823b)
	- [How JavaScript works: A comparison with WebAssembly + why in certain case it’ better to use it…](https://blog.sessionstack.com/how-javascript-works-a-comparison-with-webassembly-why-in-certain-cases-its-better-to-use-it-d80945172d79?gi=51fbfec54aa7)
	- [How JavaScript works: Deep dive into WebSocket and HTTP/2 with SSE + how to pick the right path](https://blog.sessionstack.com/how-javascript-works-deep-dive-into-websockets-and-http-2-with-sse-how-to-pick-the-right-path-584e6b8e3bf7?gi=b3e0a5c8ecc9)
	- [How JavaScript works: Event loop and the rise of Async programming + 5 way to better coding with…](https://blog.sessionstack.com/how-javascript-works-event-loop-and-the-rise-of-async-programming-5-ways-to-better-coding-with-2f077c4438b5?gi=94b62da6cef)
	- [How JavaScript works: memory management + how to handle 4 common memory leaks](https://blog.sessionstack.com/how-javascript-works-memory-management-how-to-handle-4-common-memory-leaks-3f28b94cfbec?gi=de5c907380e)
	- [How JavaScript works: inside the V8 engine + 5 tip on how to write optimized code](https://blog.sessionstack.com/how-javascript-works-inside-the-v8-engine-5-tips-on-how-to-write-optimized-code-ac089e62b12e?gi=d83c5a6d2b2d)
	- [How JavaScript works: an overview of the engine, the runtime, and the call stack](https://blog.sessionstack.com/how-does-javascript-actually-work-part-1-b0bacc073cf?gi=b2dea8ef07f8)
	- [How JavaScript works: the mechanic of Web Push Notifications](https://blog.sessionstack.com/how-javascript-works-the-mechanics-of-web-push-notifications-290176c5c55d?gi=938cbbf1cb2c)
	- [How JavaScript works: the rendering engine and tip to optimize it performance](https://blog.sessionstack.com/how-javascript-works-the-rendering-engine-and-tips-to-optimize-its-performance-7b95553baeda?gi=f9dbf39c03c1)
- [Life of a URLRequest](https://chromium.googlesource.com/chromium/src/+/master/net/docs/life-of-a-url-request.md)
- [A Crash Course in Debugging with chrome://net-internals](https://chromium.googlesource.com/chromium/src/+/master/net/docs/crash-course-in-net-internals.md)
- [Profiling with the Gecko Profiler - Mozilla | MDN](https://developer.mozilla.org/en-US/docs/Mozilla/Performance/Profiling_with_the_Built-in_Profiler)
- `about:telemetry`, `about:performance`, `about:memory` (Firefox) https://addons.mozilla.org/en-US/firefox/addon/task-manager/ https://addons.mozilla.org/en-US/firefox/addon/tab-data/ [515352 - Implement Firefox own Task Manager (with live updating of per-tab CPU and memory usage)](https://bugzilla.mozilla.org/show_bug.cgi?id=515352)
- Task Manager (Chrome)
- [perf-apis-2/performance-techniques.pdf at master · manucorporat/perf-apis-2](https://github.com/manucorporat/perf-apis-2/blob/master/performance-techniques.pdf) - Page 14
- Inside look at modern web browser
	- [Inside look at modern web browser (part 1)  |  Web  |  Google Developers](https://developers.google.com/web/updates/2018/09/inside-browser-part1)
	- [Inside look at modern web browser (part 2)  |  Web  |  Google Developers](https://developers.google.com/web/updates/2018/09/inside-browser-part2)
	- [Inside look at modern web browser (part 3)  |  Web  |  Google Developers](https://developers.google.com/web/updates/2018/09/inside-browser-part3)
	- [Inside look at modern web browser (part 4)  |  Web  |  Google Developers](https://developers.google.com/web/updates/2018/09/inside-browser-part4)
- From URL to Interactive
	- [From URL to Interactive · An A List Apart Article](https://alistapart.com/article/from-url-to-interactive)
	- [Server to Client · An A List Apart Article](https://alistapart.com/article/server-to-client)
	- [Tags to DOM · An A List Apart Article](https://alistapart.com/article/tags-to-dom)
	- [Braces to Pixels · An A List Apart Article](https://alistapart.com/article/braces-to-pixels)
	- [var to JIT · An A List Apart Article](https://alistapart.com/article/var-to-jit)

- [Using Hardware to Decode and Load JPG Images up to 45% faster in Internet Explorer 11 – IEBlog](https://blogs.msdn.microsoft.com/ie/2013/09/12/using-hardware-to-decode-and-load-jpg-images-up-to-45-faster-in-internet-explorer-11/)

## Headless browser

- [Headless browser — Wikipedia](https://en.wikipedia.org/wiki/Headless_browser)
- Puppeteer: Node API for [Headless Chrome](https://github.com/GoogleChrome/puppeteer) and [Headless Firefox](https://github.com/GoogleChrome/puppeteer/tree/master/experimental/puppeteer-firefox) - [Puppeteer API](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md)
- [Headless web browsers](https://gist.github.com/evandrix/3694955)
- [PhantomJS | PhantomJS](http://phantomjs.org/)
- [Nightmare](http://www.nightmarejs.org/)
- [selenium - Headless Browser and scraping - solutions - Stack Overflow](https://stackoverflow.com/questions/18539491/headless-browser-and-scraping-solutions)
- [SeleniumHQ/docker-selenium: Docker images for Selenium Grid Server (Standalone, Hub, and Nodes).](https://github.com/SeleniumHQ/docker-selenium)
- [Headless Chrome/Firefox testing in NodeJS with Selenium and Xvfb | CodeUtopia](http://codeutopia.net/blog/2013/07/13/headless-chromefirefox-testing-in-nodejs-with-selenium-and-xvfb/)
- [`chrome --headless --remote-debugging-port=9222 https://chromium.org`](https://chromium.googlesource.com/chromium/src/+/lkgr/headless/README.md)
- [Getting Started with Headless Chrome | Web | Google Developers](https://developers.google.com/web/updates/2017/04/headless-chrome)
- https://developer.mozilla.org/en-US/Firefox/Headless_mode
- Chrome: `--user-agent="..."`, could require `--single-process`. See also `--use-mobile-user-agent`

See [Data - Web scrapping](../Data/Web%20scrapping/Web%20scrapping.md)

### Headless browser detection

It's a [cat-and-mouse game](https://en.wikipedia.org/wiki/Cat_and_mouse)

- [puppeteer-extra/packages/puppeteer-extra-plugin-stealth at master · berstend/puppeteer-extra](https://github.com/berstend/puppeteer-extra/tree/master/packages/puppeteer-extra-plugin-stealth) - Puppeteer plugin to prevent detection
- [Detecting Chrome Headless](http://antoinevastel.github.io/bot%20detection/2017/08/05/detect-chrome-headless.html)
- [berstend/puppeteer-extra: 💯 Teach puppeteer new tricks through plugins.](https://github.com/berstend/puppeteer-extra)
- [puppeteer-extra/packages/puppeteer-extra-plugin-recaptcha at master · berstend/puppeteer-extra](https://github.com/berstend/puppeteer-extra/tree/master/packages/puppeteer-extra-plugin-recaptcha?source=post_page---------------------------)
- [Detecting Chrome headless | Hacker News](https://news.ycombinator.com/item?id=14936025)
- [How to bypass “slider CAPTCHA” with JS and Puppeteer](https://medium.com/@filipvitas/how-to-bypass-slider-captcha-with-js-and-puppeteer-cd5e28105e3c)

## Server environments

1. local
2. development (or testing, integration) (could have a dedicated env. for Quality Assurance and User acceptance Testing)
3. staging
4. preprod
5. production

- [Deployment environment — Wikipedia](https://en.wikipedia.org/wiki/Deployment_environment)

## Optimizations and performances

Aka WebPerfs

> respecting the medium

- [The Ethics of Web Performance - Web Performance Consulting | TimKadlec.com](https://timkadlec.com/remembers/2019-01-09-the-ethics-of-performance/)

Loading, parsing, rendering, etc.

> We don't want humans waiting on computers. We want computers waiting on humans.
— Gregory Szorc

- [SpeedCurve on Twitter: "200ms start render = 16% bounce rate 1.8s start render = 49% bounce rate See how user engagement charts show you correlations between #webperf and #UX: https://t.co/Nz6ilYOuaA… https://t.co/fIPquBIH2P"](https://twitter.com/SpeedCurve/status/938877356386611201)
- [High Performance Browser Networking (O'Reilly)](https://hpbn.co/)
- [Front-End Performance Checklist 2019 \[PDF, Apple Pages, MS Word\] — Smashing Magazine](https://www.smashingmagazine.com/2019/01/front-end-performance-checklist-2019-pdf-pages/)
- [Improving Smashing Magazine's Performance: A Case Study](https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/)
- [Mobile-Friendly Test - Google Search Console](https://search.google.com/search-console/mobile-friendly)
- [Le web mobile et la performance – 24 jours de web](http://www.24joursdeweb.fr/2014/le-web-mobile-et-la-performance/)
- [Performance-Bookmarklet helps to analyze the current page through the Resource Timing API, Navigation Timing API and User-Timing](https://github.com/micmro/performance-bookmarklet)
- [Fixing a parallax scrolling website to run in 60 FPS - Adventures in WebKit land](http://kristerkari.github.io/adventures-in-webkit-land/blog/2013/08/30/fixing-a-parallax-scrolling-website-to-run-in-60-fps/)
- [ResourceLoader/Features - MediaWiki](http://www.mediawiki.org/wiki/ResourceLoader/Features#Front-end)
- Example of audits on famous website, applications [Performance audits for the web](https://github.com/perfs/audits/issues)
- [Design and development standards to align and guide your project - Performance](https://github.com/north/north#performance)
- [Best Practices for Speeding Up Your Web Site - Yahoo Developer Network](https://developer.yahoo.com/performance/rules.html)
- [Book of Speed](http://www.bookofspeed.com/index.html)
- [Don’t abuse enabling GPU acceleration on iOS! – Medium](https://medium.com/@MerciMichel/don-t-abuse-enabling-gpu-acceleration-on-ios-95520da2428)
- [High Performance Web Sites](http://stevesouders.com/hpws/rules.php)
- [A curated list of Web Performance Optimization](https://github.com/davidsonfellipe/awesome-wpo)
- See [\[Infographic\] Ultimate Checklist for Optimizing Web Performance - Yottaa](http://www.yottaa.com/infographic-the-ultimate-checklist-for-optimizing-web-perfo/)
- [WPO Stats](https://wpostats.com/)
- [Essential Image Optimization](https://images.guide/)
- [JavaScript Start-up Optimization | Web Fundamentals | Google Developers](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/javascript-startup-optimization/)

> Progressive JPEGs decode slower than Baseline ones. [..] decoding a progressive JPEG takes about 3.3× as long as a baseline one. (I would still absolutely recommend using progressive, because they feel a lot faster than their baseline counterparts.)

See also [Images](Images), [Content Security Policy](Security#content-security-policy)

Small DOMs, no CSS descendant selectors (offsetTop, etc. trigger layout)

Take account traffic, processing time, etc.

Tools (audit, checklist, benchmark, best practices, etc.):

- Tools collection [Quelques outils en ligne pour analyser votre site | Darklg Blog](http://darklg.me/2014/02/quelques-outils-en-ligne-pour-analyser-votre-site/)
- [Browserling - Live interactive cross-browser testing](https://www.browserling.com/)
- [testling-ci](https://ci.testling.com/)
- [WebPageTest private instance server](https://github.com/jpvincent/WPT-server)
- [Observatory by Mozilla](https://observatory.mozilla.org/)
- [CSP Evaluator](https://csp-evaluator.withgoogle.com/)
- [Performance Calendar » Testing with Realistic Networking Conditions](http://calendar.perfplanet.com/2016/testing-with-realistic-networking-conditions/#recommended_tools)
- [Web Developer Checklist](http://webdevchecklist.com/)
- [HTML_CodeSniffer](http://squizlabs.github.io/HTML_CodeSniffer/)
- [Scan your website for issues - Microsoft Edge Development](https://developer.microsoft.com/en-us/microsoft-edge/tools/staticscan/)
- [Analyse your HTTP response headers](https://securityheaders.io/)
- [Web Developer Security Checklist – Simple Security](https://simplesecurity.sensedeep.com/web-developer-security-checklist-f2e4f43c9c56)
- [Les bonnes pratiques de la qualité Web - Opquast Checklists](https://checklists.opquast.com/fr/)
- [Lighthouse | Web | Google Developers](https://developers.google.com/web/tools/lighthouse/)

- [WebPagetest - Website Performance and Optimization Test](https://www.webpagetest.org/)
- [GTmetrix | Website Speed and Performance Optimization](https://gtmetrix.com/)
- [PageSpeed Tools  |  Google Developers](https://developers.google.com/speed/pagespeed/)
- [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)
- [Website speed test](https://tools.pingdom.com/)

### Control your content

- [The Washington Post cuts off ad tech vendors slowing its site - Digiday](https://digiday.com/media/washington-post-vendors/)

### Mobile

- [Mobile-Friendly Test - Google Search Console](https://search.google.com/search-console/mobile-friendly)
- https://www.google.com/webmasters/tools/mobile-friendly/
- https://www.google.com/webmasters/tools/mobile-usability
- https://www.bing.com/webmaster/tools/mobile-friendliness
- [Mobile Web Application Best Practices](http://www.w3.org/TR/mwabp/)

### Reduce bytes

> http://www.haratetsuo.com/wp-content/themes/haratetsuo2018_cms_v2/images/ico/arrow.svg
> The 30MB SVG image is a simple arrow! It's served uncompressed (gzipped would be 24MB and brotli would be 3.8MB). It contains 82 base64 encoded JPG images (one per image size). There are only 10 unique base64 images encoded in the file, so a lot of repetition...  
> [Paul Calvano on Twitter: "Exactly! The 30MB SVG image is a simple arrow!… https://t.co/ci2hz7WpLI"](https://twitter.com/paulcalvano/status/1164466648260198400)

> The fastest byte is a byte not sent.
— Ilya Grigorik http://chimera.labs.oreilly.com/books/1230000000545

Reduce page weight can give a (wrong) feedback about the page load time increase:

> When I was at Google, someone told me a story about a time that “they” completed a big optimization push only to find that measured page load times increased. When they dug into the data, they found that the reason load times had increased was that they got a lot more traffic from Africa after doing the optimizations. The team’s product went from being unusable for people with slow connections to usable, which caused so many users with slow connections to start using the product that load times actually increased.
— Dan Luu in [Most of the web really sucks if you have a slow connection](https://danluu.com/web-bloat/)

Blocking deliberately or unintentionally device or connection capacities (browser version) will give wrong feedback about "users don't use old browser" (because they can't) or "users don't have slow connection" (because page can't load in decent time)
See also [Page Weight Matters](http://blog.chriszacharias.com/page-weight-matters).

- [Speeding up the web with the Save-Data header - Frontend Web Developer, Oxfordshire, UK - Matt Hobbs](https://nooshu.github.io/blog/2019/09/01/speeding-up-the-web-with-save-data-header/)

**Always reduce before encrypt** (aka always compress before encode), not the inverse:

- [Appcanary: Should you encrypt or compress first?](http://blog.appcanary.com/2016/encrypt-or-compress.html)
- [encryption - When compressing and encrypting, should I compress first, or encrypt first? - Stack Overflow](https://stackoverflow.com/questions/4676095/when-compressing-and-encrypting-should-i-compress-first-or-encrypt-first)

- minification:
	- optimize/reduce without require reverse operation
	- remove unessary data (duplicates, unused tags, selectors)
	- merge/round similar data, reduce precision (`0.2345` -> `.23`)
	
	- http://cssstats.com/
	- https://isellsoap.github.io/specificity-visualizer/
- compact/compress (require processing to recover operable state): pre-gzip. See [Precompress](#precompress) and [Content encoding`](#content-encoding)
- use different compression algorithm, or a better tool/algorithm implementation (like zopfli for deflate)
	- [Guetzli](https://github.com/google/guetzli/) can be use in conjunction of tools like [ImageOptim](https://imageoptim.com/)
	- brotli (vs gzip)
	
	Note some framework read the `zlib.output_compression` value to define the header `Content-Encoding` to gzip (set `zlib.output_compression = Off` in `php.ini`)
	
	Example: compress CSS with optimized dictionary based alogrithms (like gzip use huffman tables): blocks, selectors, media queries, properties, values. See [Compression & Minification](CSS#Compression & Minification)
	
	- [Optimising GIFs for the Web](https://bitsofco.de/optimising-gifs/) - use `gifsicle -O3 --lossy=80 -o compressed.gif original.gif`
- split commbined HTTP headers values: to use HPACK (HTTP/2.0)
	Instead of:
	
		set-cookie: key1=value1; key2=value2; domain=.example.com; expires=Fri, 21-Dec-2018 22:15:42 GMT; path=/
	
	Use:
	
		set-cookie: key1=value1; domain=.example.com; expires=Fri, 21-Dec-2018 22:15:42 GMT; path=/
		set-cookie: key2=value2; domain=.example.com; expires=Fri, 21-Dec-2018 22:15:42 GMT; path=/
	
	- [mnot’s blog: Designing Headers for HTTP Compression](https://www.mnot.net/blog/2018/11/27/header_compression)
	- [Headers](#headers)
	- [Header compression](#header-compression)
- use the right format (if supported, or a fallback):
	- ~~as binary representation of CSS (really usefull vs GZ?)~~
	- use image as data container (as colors, but could be lossy)
	- transparent video: WebM or side by side channels (RGB + A as RGB) videos. See [Alpha](Video#Alpha)
	- transparent image: instead of PNG use WebP (or JPEG-XR) or combined formats. See [Alpha compression](Image#Alpha compression)
	- animated image: use APNG or Animated WebP or looped video instead of GIF
	
			<video autoplay loop muted playsinline poster="original.jpg">
				<source type="video/webm" src="original.webm">
				<img src="original.gif">
			</video>
		
		See [Animated image](Image#Animated image). See also [Image sequence](#image-sequence)
	- Use a video with only 1 frame as image (ex: WebP), could done with H.264/H.265, see [Use video codec](Image#Use video codec)
	- Use code/lib to animate elements instead of video or sprites: https://github.com/bodymovin/bodymovin
	- VP9 (8bit) good on small screens (but not on big)
		- [Does VP9 deserve attention – Part II | Video Encoding & Streaming Technologies](https://sonnati.wordpress.com/2016/06/17/does-vp9-deserve-attention-part-ii/)
	- [Don’t use JPEG-XR on the Web](https://calendar.perfplanet.com/2018/dont-use-jpeg-xr-on-the-web/) (JPEG-XRs are decoded on "the software-side on the CPU" by Internet Explorer and Microsoft Edge, the only browsers that support it)
- HTML: remove comments, spaces, not required closing tags, attibutes, chars like `"`, entities (when not required), etc.
- CSS: remove comments, prefixed properties, useless selectors, regroup using shorthand properties (like `background` for: `background-image`, etc.), etc.
	- [CSS](CSS)
- SVG:
	- [SVG](SVG#Optimizations)
- JavaScript: optimize by remove dead code (treeshaking), uglify (rename variables for shorter name, inline function, resolve static expressions), etc.
	- [The Cost Of JavaScript In 2018 – Addy Osmani – Medium](https://medium.com/@addyosmani/the-cost-of-javascript-in-2018-7d8950fbb5d4)
- Images:
	- image compression options (if applicable, cf. formats)
		- [JPEG - Compression](JPEG#Compression)
		- [PNG - Compression](PNG#Compression)
		- [Image - Compression and optimisation](Image#Compression and optimisation) and [Image - Mixed formats](Image#Mixed formats)
		- [Video - Compression and optimisation](Video#Compression and optimisation)
		- [compression by upscaling](Formats and protocols/Images#Compression by upscaling) technique
		- [ImageOptim](https://imageoptim.com/)
	
		Use other (experimental) formats like [BPG](BPG) or [FLIF](FLIF)
	
		To investigate: store vector using SWF, decompress on the fly (to SVG) with ServiceWorker; decompress biJPEG to PNG or webp with OfflineCanvas
	- use the right dimensions (ex.: thumbnails)
- 3D models:
	drops leading zeroes (`-0.5` -> `-.5`) and changes the scale of the model

	- https://jsfiddle.net/w43q2mac/ - optimize OBJ file
	- [😏 on Twitter: "in case you want to reduce obj file by 20-40% https://t.co/saHVrLtdjm"](https://twitter.com/makc3d/status/896495973572247553)
	- [OBJ compression to the smallest file size possible – Compress-Or-Die](https://compress-or-die.com/obj/)
	- https://compress-or-die.com/public/javascript/OBMLoader.min.js - [OBJ compression to the smallest file size possible – Compress-Or-Die](https://compress-or-die.com/obj-process?example)
- fonts:
	- use [WOFF](WOFF) especially WOFF2 (use a Brotli instead of Deflate, a gain of ~26%). For WOFF (v1) optimize compression with Zopfli
	- create WOFF files from OpenType/CFF font (instead of TrueType) (OpenType/CFF use cubic Bézier vs quadratic Bézier for TrueType)
	- use only subset. use `pyftsubset` from [fonttools](https://github.com/fonttools/fonttools) (a library to manipulate font files from Python). Be carefull when set this parameter, with content changes or languages could invalidate it.
	- reduce the `unitsPerEm` to 256 (usally 1000 or 2048). This use a byte (8 bits) instead of a short (16 bits) to store coordinates. Reduce precision, but for regular text, the difference is invisible.
	
	- [Saving the internet 2000 terabytes a day: fixing Font Awesome's fonts – Pixelambacht](https://pixelambacht.nl/2016/font-awesome-fixed/)
	- [The Typekit Blog | The Benefits Of OpenType/CFF Over TrueType](https://blog.typekit.com/2010/12/02/the-benefits-of-opentypecff-over-truetype/)
	- [The Glyph Data Table](https://www.microsoft.com/typography/OTSPEC/glyf.htm)
	- [Front-end Forward: Font performance - YouTube](https://www.youtube.com/watch?v=S8_sy2sWPZQ)
- other formats:
	- Optimize tarball by sorting by file extension and dir. `find ./source \! -type d | rev | sort | rev | tar cjf archive.tar.bz2 --files-from=-`
		That group similar files together, allow compression from redundancy across files similar files. (due to limited window size to 32K)
	- remove optional filename and timestamp from gzipped stream (option `-n`): `gzip -9 -n -k file`

### Reduce requests

- embed images in CSS using data URI, encoded with URI encoding or base64 (could have a negative impact on low end devices)
- JS, CSS in HTML in tags `<script>` and `<style>`
- CSS/HTML in JavaScript variables
- HTML prerendered (HTML + JS + data)
- bundle JS and/or CSS, image spriting https://github.com/clyfish/zerosprites http://yostudios.github.io/Spritemapper/
- add the right header(s) for server cache strategy (see [Cache](#cache))

Note: HTTP/2 [multiplex](#multiplexed--pipelining) and [push](#server-push) are not always a good alternative, because compression is more efficient on larger chunk data. [Musings on HTTP/2 and Bundling | CSS-Tricks](https://css-tricks.com/musings-on-http2-and-bundling/)

- [The Best Request Is No Request, Revisited · An A List Apart Article](https://alistapart.com/article/the-best-request-is-no-request-revisited) - Unbundle resources with HTTP/2.0 but be carefull

### Reduce latency

Use CDN

- [Optimizing HTTP/2 prioritization with BBR and tcp_notsent_lowat](https://blog.cloudflare.com/http-2-prioritization-with-nginx/)

#### First packet size

- [wifi - What is the total length of pure TCP Ack sent over ethernet? - Stack Overflow](https://stackoverflow.com/questions/5543326/what-is-the-total-length-of-pure-tcp-ack-sent-over-ethernet)

##### Initial TCP window

> Minimize ATF (above-the-fold) content size: The first TCP connection isn’t able to fully utilize a connection’s bandwidth on the first roundtrip, which means the number of packets it can send is very limited. In order to render your ATF content it needs to be 148 kb or less
— [5 SEO Guidelines for Web Developers](https://www.sitepoint.com/5-seo-guidelines-for-web-developers/)

Congestion window: initial cwnd size is 10; 14.6KB = 10 packets of 1460 Bytes.

**TODO: where "148 kb" come from?**

- [TCP Slow-start](https://en.wikipedia.org/wiki/Slow-start)
- [Networking 101: Building Blocks of TCP - High Performance Browser Networking (O'Reilly)](https://hpbn.co/building-blocks-of-tcp/#slow-start)
- [Reduce the size of the above-the-fold content  |  PageSpeed Insights  |  Google Developers](https://developers.google.com/speed/docs/insights/PrioritizeVisibleContent)
- [Mobile Analysis in PageSpeed Insights  |  PageSpeed Insights  |  Google Developers](https://developers.google.com/speed/docs/insights/mobile)
- [networking - maximum packet size for a TCP connection - Stack Overflow](https://stackoverflow.com/questions/2613734/maximum-packet-size-for-a-tcp-connection)
- [draft-hkchu-tcpm-initcwnd-01 - Increasing TCP's Initial Window](https://tools.ietf.org/html/draft-hkchu-tcpm-initcwnd-01)
- [Tuning initcwnd for optimum performance - CDN Planet](http://www.cdnplanet.com/blog/tune-tcp-initcwnd-for-optimum-performance/)
- [Increasing tcp slow start Initial Window in linux 3.0 kernel - Server Fault](http://serverfault.com/questions/365614/increasing-tcp-slow-start-initial-window-in-linux-3-0-kernel)
- [Is it possible to configure the initial window size for tcp slow start on Windows? - Server Fault](http://serverfault.com/questions/160690/is-it-possible-to-configure-the-initial-window-size-for-tcp-slow-start-on-window)

#### Fast Open

- [TCP Fast Open - Wikipedia](https://en.wikipedia.org/wiki/TCP_Fast_Open)
- [Blog Stéphane Bortzmeyer: Commencer les sessions TCP plus vite ?](http://www.bortzmeyer.org/tcp-ouverture-rapide.html)
- [TCP Fast Open - Wikitech](https://wikitech.wikimedia.org/wiki/TCP_Fast_Open#Detecting_server-side_TFO_support)
- [GitHub - bradleyfalzon/tcp-fast-open: Golang example of TCP Fast Open (RFC7413)](https://github.com/bradleyfalzon/tcp-fast-open)
- [Optimizing TCP slow start - Tuning Microsoft IIS - IISWebSpeed.com](https://www.iiswebspeed.com/documentation/iistuning/tcp-slow-start)
- [TCP Fast Open - KeyCDN Support](https://www.keycdn.com/support/tcp-fast-open/)
- [1188435 - Support TCP fastopen](https://bugzilla.mozilla.org/show_bug.cgi?id=1188435)

#### Keep-Alive

Use Keep-Alive connection (more useful for HTTP/1.X connection than HTTP/2):

	<IfModule mod_headers.c> 
		Header set Connection keep-alive 
	</IfModule>

- [HTTP persistent connection — Wikipedia](https://en.wikipedia.org/wiki/HTTP_persistent_connection)

#### Preload ASAP

As soon as possible, use UDP Priming (pre request like HEAD) to let the server prepare response

Load list by fragments 1+1+X (better than × or 3+7+X) like streaming

- [Optimizing Facebook for iOS start time | Engineering Blog | Facebook Code](https://code.facebook.com/posts/1675399786008080/optimizing-facebook-for-ios-start-time/)

#### IPv6

- [98.01% of sites on Cloudflare now use IPv6](https://blog.cloudflare.com/98-percent-ipv6/)
- [IPv6 measurements | Zaid Ali Kahn | Pulse | LinkedIn](https://www.linkedin.com/pulse/ipv6-measurements-zaid-ali-kahn)
- [IPv6: It's time to get on board | Engineering Blog | Facebook Code](https://code.facebook.com/posts/1192894270727351/ipv6-it-s-time-to-get-on-board/)

#### Edge side includes

CDN or cache proxy agregade differents resource fragments with cache

- [Solving anything in VCL](https://www.slideshare.net/Fastly/solving-anything-in-vcl#11)
- [Edge Side Includes - Wikipedia](https://en.wikipedia.org/wiki/Edge_Side_Includes)
- [Server Side Includes - Wikipedia](https://en.wikipedia.org/wiki/Server_Side_Includes)
- [EdgeSuite 4.2 ESI Examples](http://esi-examples.akamai.com/)

#### Dedicated domains cookies less

Reduce latency server side.

For statics resources (don't require cookies), use a dedicated domain.

With HTTP/2.0 it's no more useful, with [header compression](#header-compression).

#### Multiple domains for static resources

Aka domain sharding, domain sharing

Allow multiple parallels requests.

Ex: `static1.example.com` and `static2.example.com`

**Not adviced if you use HTTP/2.0 or HTTPS**

- [Connection management in HTTP/1.x - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Connection_management_in_HTTP_1.x#Domain_sharding)
- [Performance Calendar » Reducing Domain Sharding](https://calendar.perfplanet.com/2013/reducing-domain-sharding/)

#### Serve progressive HTML document

Serve the document using chunk encoding.

Note: browser often have a buffer of 4096 bytes

1. Send the HTTP headers
2. the HTML head (title, metas, scripts, styles, etc.)
3. first part of the HTML body
4. (*n) send chunks with `<p class="progress">Progress: XX%...</p>` to show progression
5. send chunk `<p class="progress">Complete</p>`
6. send chunk `<style>.progress{display: none}</style>`
5. send the remains HTML document part

#### Precompress

See [Content encoding](#content-encoding)

For all text formats: CSS, SVG, JavaScript

Could also be used for generic data (other formats that don't already use compression), or if the compression mode in those format can be disabled (ex: uncompressed PNG + Content encoding)

- Create a gzip without store the original file name `gzip -9 -k -n file.ext`
- create a TAR of all .ext `COPYFILE_DISABLE=1 tar -cvf file.tar *.ext`
- `Content-Encoding: br` Brotli

With nginx: http://nginx.org/en/docs/http/ngx_http_gzip_static_module.html#example

With Apache:
 
	# If an asset (CSS, JS, SVG, HTML, JSON, TAR, etc.) exist in a pre-encoded form, serve as is
	# http://developer.yahoo.com/performance/rules.html#gzip
	<IfModule mod_rewrite.c>
		# If the browser accepts gzip and the requested file exists under
		# pre-encoded version, then rewrite to that version.
		# Requires both mod_rewrite and mod_headers to be enabled.
		<IfModule mod_headers.c>
			RewriteEngine on
			
			# *.br
			# Serve gzip compressed CSS files if they exist and the client accepts brotli.
			RewriteCond %{HTTP:Accept-Encoding} \bbr\b
			RewriteCond %{REQUEST_FILENAME}.br -s
			RewriteRule (.*) $1.br [QSA]
			
			# *.gz
			# Serve gzip compressed CSS files if they exist and the client accepts gzip.
			RewriteCond %{HTTP:Accept-Encoding} \bgzip\b
			RewriteCond %{REQUEST_FILENAME}.gz -s
			RewriteRule (.*) $1.gz [QSA]
			
			# *.svg to *.svgz
			RewriteCond %{HTTP:Accept-Encoding} \bgzip\b
			RewriteCond %{REQUEST_FILENAME} .svg$
			RewriteCond %{REQUEST_FILENAME}z -s
			RewriteRule (.*) $1z [QSA]
			
			<FilesMatch "\.((js|css|html|xml|svg|json|tar)\.(gz|br)|svgz)$">
				# Tell caching proxy servers to cache the file based on encoding
				# Apache should add it automatically: http://httpd.apache.org/docs/current/mod/mod_rewrite.html#rewritecond
				Header append Vary Accept-Encoding
				# Do this to set proper ETags for server clusters
				FileETag MTime Size
			</FilesMatch>
			
			<FilesMatch "\.((js|css|html|xml|svg|json|tar)\.gz|svgz)$">
				# Prevent double compression
				SetEnv no-gzip 1
				# We serve a gzipped stream
				Header set Content-Encoding br
			</FilesMatch>
			
			<FilesMatch "\.(js|css|html|xml|svg|json|tar)\.br$">
				# Prevent double compression
				SetEnv no-brotli 1
				# We serve a gzipped stream
				Header set Content-Encoding gzip
			</FilesMatch>
			
			# And set proper media type:
			RewriteRule \.js\.(gz|br)$ - [T=application/javascript]
			RewriteRule \.css\.(gz|br)$ - [T=text/css]
			RewriteRule \.svg(z|\.gz|br)$ - [T=image/svg+xml]
			RewriteRule \.html\.(gz|br)$ - [T=text/html]
			RewriteRule \.xml\.(gz|br)$ - [T=text/xml]
			RewriteRule \.json\.(gz|br)$ - [T=application/json]
			# Allow for example JS to access tar data already ungzipped (done by the browser, instead using JS to decode)
			#RewriteRule \.tar\.(gz|br)$ - [T=application/x-tar]
			# For browsers compatibility we can't use the right media type but:
			RewriteRule \.tar\.(gz|br)$ - [T=application/octet-stream]
		</IfModule>
	</IfModule>

	RewriteRule \.js\.gz$ - [E=no-gzip:1,H=Content-Encoding:gzip,T=application/javascript]

An other way (**need to test**: content not double encoded, `.gz.html` output). It is use [content negotiation](http://httpd.apache.org/docs/2.4/en/content-negotiation.html):

	# Activate Content Negotiation
	Options +MultiViews
	RemoveType .gz
	AddEncoding gzip .gz
	RewriteRule \.html\.gz$ - [T=text/html,E=no-gzip:1]
	RewriteRule \.css\.gz$ - [T=text/css,E=no-gzip:1]
	RewriteRule \.js\.gz$ - [T=application/javascript,E=no-gzip:1]
	# By using content negociation, Apache will add Content-Encoding to Vary header

Or:

- use a CDN
- use `mod_mem_cache` or `mod_disk_cache`: [webdirect.no Apache caching with gzip enabled | webdirect.no](http://webdirect.no/linux/apache-caching-with-gzip-enabled/)
- use a proxy cache like Varnish

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

#### Multiplexed / Pipelining

HTTP/1.1 has pipelining, but not well supported (by proxies, etc.)
HTTP/2 is multiplexed

- [HTTP/2 Frequently Asked Questions](https://http2.github.io/faq/#why-is-http2-multiplexed)
- [Connection management in HTTP/1.x - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Connection_management_in_HTTP_1.x#HTTP_pipelining)

#### TLS

- avoiding full TLS handshakes
- TLS resumption
- reduce the certificate chain
- enable the correct cipher, following Mozilla's guidelines.
- verify that web server is running on a system with a CPU that support correct instructions


- [Is TLS Fast Yet?](https://istlsfastyet.com/)
- [Security/Server Side TLS - MozillaWiki](https://wiki.mozilla.org/Security/Server_Side_TLS)
- [SSL Performance Diary #4: Optimizing the TLS Handshake - Zoompf Web Performance](https://zoompf.com/blog/2014/12/optimizing-tls-handshake)
- [SSL Performance Diary #1: The Certificate Chain - Zoompf Web Performance](https://zoompf.com/blog/2014/06/ssl-performance-diary-1-the-certificate-chain)
- [Enabling HTTPS Without Sacrificing Your Web Performance - Moz](https://moz.com/blog/enabling-https-without-sacrificing-web-performance)
- [SSL/TLS Performance Diary #3: Optimizing Data Encryption - Zoompf Web Performance](https://zoompf.com/blog/2014/11/ssl-performance-diary-3-optimizing-data-encryption) - (old)

#### Use dedicated servers

Load balancer, localized CDN, etc.

- [How We Knew It Was Time to Leave the Cloud | GitLab](https://about.gitlab.com/2016/11/10/why-choose-bare-metal/)

#### Cache

To control static resource version, **use checksum instead of build number**. Which means you only download a new copy _when it actually changes_ (see ETag).

Use forever cache (cache immutable) for static resources.

- [HTTP Heuristic Caching (Missing Cache-Control and Expires Headers) Explained – Paul Calvano](https://paulcalvano.com/index.php/2018/03/14/http-heuristic-caching-missing-cache-control-and-expires-headers-explained/)
- [Un tutoriel de la mise en cache pour les auteurs Web et les webmestres](https://www.mnot.net/cache_docs/)
- [Increasing Application Performance with HTTP Cache Headers | Heroku Dev Center](https://devcenter.heroku.com/articles/increasing-application-performance-with-http-cache-headers)
- https://restpatterns.mindtouch.us/Articles/Caching_Matters

##### Cached

max-age or expires headers, `Header append Cache-Control "public"`, `Header append Cache-Control "immutable"` avoid check of 304s

`.htaccess`: 

	# Requires mod_expires to be enabled.
	<IfModule mod_expires.c>
		# Enable expirations.
		ExpiresActive On
		
		# Cache all files for 2 weeks after access (A).
		ExpiresDefault A1209600
		
		<FilesMatch \.php$>
		  # Do not allow PHP scripts to be cached unless they explicitly send cache
		  # headers themselves. Otherwise all scripts would have to overwrite the
		  # headers set by mod_expires if they want another caching behavior. This may
		  # fail if an error occurs early in the bootstrap process.
		  ExpiresActive Off
		</FilesMatch>
	</IfModule>

PHP:

	header('Expires: '.gmdate('D, d M Y H:i:s \G\M\T', time() + (60 * 60 * 24 * 12)));// 2 weeks

Varnish script to Handle `Vary: User-Agent` to create classes to reduce variations.

	# recv
	if (req.http.host ~ "^example.com$") {
		if (req.http.User-Agent ~ "MSIE\s[1-10]\." || req.http.User-Agent ~ "Edge\/[1-10]\." || req.http.User-Agent ~ "Trident\/.*rv:[1-10]\." || req.http.User-Agent ~ "Firefox\/[1-41]\." || req.http.User-Agent ~ "Safari\/[1-8]\." || req.http.User-Agent ~ "Version\/[1-8]\.")
		{
			# Set header for "old browser"
			set req.http.X-UA-Device = "old";
		}
		elsif (req.http.User-Agent ~ "facebookexternalhit\/" || req.http.User-Agent ~ "Facebot" || req.http.User-Agent ~ "Pinterest\/")
		{
			# Set header for "bot"
			set req.http.X-UA-Device = "bot";
		}
		else
		{
			# Set header for "recent browser"
			set req.http.X-UA-Device = "new";
		}
	}
	
	# Fetch
	if (req.http.host ~ "^example.com$") {
		set beresp.http.X-UA-Device = req.http.X-UA-Device;
		
		# Vary by X-UA-Device, so varnish will keep distinct object copies by X-UA-Device value
		if (beresp.http.Vary)
		{
			set beresp.http.Vary = beresp.http.Vary + ",X-UA-Device";
		}
		else
		{
			set beresp.http.Vary = "X-UA-Device";
		}
		
		# Remove User-Agent from Vary (provide by App)
		if (beresp.http.Vary ~ "User-Agent") {
			set beresp.http.Vary = regsub(beresp.http.Vary, ",? *User-Agent *", "");
			set beresp.http.Vary = regsub(beresp.http.Vary, "^, *", "");
			if (beresp.http.Vary == "") {
				unset beresp.http.Vary;
			}
		}
	}

- [Device detection — Varnish version trunk documentation](https://www.varnish-cache.org/docs/trunk/users-guide/devicedetection.html)
- [Achieving a high hitrate — Varnish version trunk documentation](https://www.varnish-cache.org/docs/trunk/users-guide/increasing-your-hitrate.html#http-vary)
- https://github.com/varnishcache/varnish-devicedetect

- [Are Your Cache-Control Directives Doing What They Are Supposed to Do? — theScore Tech Blog](http://techblog.thescore.com/2014/11/19/are-your-cache-control-directives-doing-what-they-are-supposed-to-do/)
- [Caching best practices & max-age gotchas - JakeArchibald.com](https://jakearchibald.com/2016/caching-best-practices/)
- [mnot’s blog: The State of Browser Caching, Revisited](https://www.mnot.net/blog/2017/03/16/browser-caching)

- [RFC 7234 in JavaScript. Parses HTTP headers to correctly compute cacheability of responses, even in complex cases ](https://github.com/pornel/http-cache-semantics)

##### Not cached

Prevent back button to show cache page (ex.: after logout)

	HTTP/1.1 200 OK
	Cache-Control: no-cache, no-store, must-revalidate
	Expires: 0

	HTTP/1.0 200 OK
	Pragma: no-cache
	Cache-Control: max-age=0

Note: `Cache-Control: no-cache` is for HTTP/1.1 where `Pragma: no-cache` is for HTTP/1.0. See [http - Difference between Pragma and Cache-control headers? - Stack Overflow](https://stackoverflow.com/questions/10314174/difference-between-pragma-and-cache-control-headers/15050018#15050018)

	header('Expires: ' . gmdate('D, d M Y H:i:s', time()) . ' GMT');
	//header('ETag: "' . sha1(time()) . '"');

- [http - Making sure a web page is not cached, across all browsers - Stack Overflow](https://stackoverflow.com/questions/49547/making-sure-a-web-page-is-not-cached-across-all-browsers)

#### Reduce processing

- [JavaScript Start-up Performance – reloading – Medium](https://medium.com/reloading/javascript-start-up-performance-69200f43b201)
- [Time spent in JS parse & eval for average JS - Google Sheets](https://docs.google.com/spreadsheets/d/1wHcNNQea28LhwQ_amFamT33d5woVrJfJy53Z1k6V090/edit) - Parse times for a 1MB bundle of JavaScript across desktop & mobile devices of differing classes
- [Too Hot To Handle - Optimizing for Low Powered Devices // Speaker Deck](https://speakerdeck.com/simonhearne/too-hot-to-handle-optimizing-for-low-powered-devices) - JS framework are too heavy for low-end devices
- [Ember.js - Glimmer.js Progress Report](https://emberjs.com/blog/2017/10/10/glimmer-progress-report.html#toc_binary-templates) - Ember.js use binary templates for faster parse
	- [glimmer-vm/packages/@glimmer/bundle-compiler at master · glimmerjs/glimmer-vm](https://github.com/glimmerjs/glimmer-vm/tree/master/packages/@glimmer/bundle-compiler)
	- [Glimmer: Blazing Fast Rendering for Ember.js, Part 1 | LinkedIn Engineering](https://engineering.linkedin.com/blog/2017/03/glimmer--blazing-fast-rendering-for-ember-js--part-1)
	- [Glimmer: Blazing Fast Rendering for Ember.js, Part 2 | LinkedIn Engineering](https://engineering.linkedin.com/blog/2017/06/glimmer--blazing-fast-rendering-for-ember-js--part-2)
	- [The Glimmer Binary Experience | LinkedIn Engineering](https://engineering.linkedin.com/blog/2017/12/the-glimmer-binary-experience)
	- [Glimmer's Optimizing Compiler](https://www.linkedin.com/pulse/glimmers-optimizing-compiler-chad-hietala?articleId=6321437215352242176)
- [JSON.parse() vs eval() - corrected · jsPerf](https://web.archive.org/web/20171119085518/https://jsperf.com/json-parse-vs-eval-corrected/1)

#### Relayout, repaint, reflow

See [Relayout, repaint, reflow](JavaScript#relayout-repaint-reflow)

### Reduce CPU/GPU

Code markup:

Client side: Serve HTML + CSS + JS + Execute JS
Server side: Serve HTML (gzipped, a tiny tiny bit more) + CSS

- [Jake Archibald on Twitter: "I took the code examples from https://t.co/Oyiax6163l and compared with highlighting markup, and without (https://t.co/oIYkvupr2D). After gzip: With highlighting markup: 900b. Without highlighting markup: 723b. PrismJS: 5.2k.… https://t.co/0xcp53jdrB"](https://twitter.com/jaffathecake/status/1113017397655547905)

### Control loading

Load based on the device or network capabilities:

- [adaptive bitrate streaming](https://en.wikipedia.org/wiki/Adaptive_bitrate_streaming) (see [MPEG-DASH](MPEG-DASH) and similar solutions)
- responsive images (`srcset` attribute and `@media` CSS rules)

78KB for first data (total, can be compressed) to ensure an optimal experience on LTE, for under 200ms delivery (determined empirically, 75% of handset will load in less than or equal to 200ms): [MobilePerf Insights: Why LTE Has Slowed by 50% in the US This Year - Twin Prime](http://twinprime.com/lte-has-slowed-by-50-in-the-us/)

Full raw data vs. data + computations (ex: BMP vs PNG)

Use [cache](#cache)

- [Service worker](../Development/JavaScript/JavaScript.md#service-worker)
- [push content with HTTP/2](#server-push)
- [Fonts and FO*T](CSS#fonts-and-fot)
- use `font-display` property for fonts
- use fallback font
- download only diff of images (like videos using relative compression + keyframes): render in canvas
- progressive data (JPEG, Video). It's even better with HTTP2 multiplexing
- adaptative byterate with DASH https://gist.github.com/ddennedy/16b7d0c15843829b4dc4

"preload" metadata like size, duration, dominant color / thumbnail, LOD, deepth, etc.

> The simple summary is
> - preload: when you use on the **same** page
> - prefetch: for future use (**next** page)

#### Buffering

Aka dynamic buffering

- [Dynamic Buffering revamping | Video Encoding & Streaming Technologies](https://sonnati.wordpress.com/2006/04/10/dynamic-buffering-revamping/) and [A Dynamic Buffering strategy | Video Encoding & Streaming Technologies](https://sonnati.wordpress.com/2005/12/03/241/) - prebuffer time (used to compute real required buffer size) + buffer to fill 80% at the current speed

#### Resource hint

See also dns-prefetch, preconnect, prerender

See [Server Push](#server-push)

	<link rel="preload" as="style" href="style.css">
	<link rel="prefetch" href="style.css">

Preload: load this resource (high priority to low priority based on the value of `as` attribute)
Prefetch: load this resource after all other resources (very low priority), will prefetched the resource when the browser is idle for future navigation

Preload will be started immediately and prefetch will be started only after the main page finishes loading.

**Note: using this only for small media files (< 5 MB).**

Don't use both preload and prefetch in same time: `<link rel="preload prefetch" as="style" href="style.css">` because they don't have the same purpose. This create potentially 2 requests.

	Link: </styles/style.css>; rel=preload; as=style

	<link rel="preload" as="style" href="style.css">

	<meta http-equiv="Link" content="</styles/style.css>; rel=preload; as=style">

Using JavaScript, but prefer the link / header version:

	<script>
	var res = document.createElement("link");
	res.rel = "preload";
	res.as = "style";
	res.href = "styles/other.css";
	document.head.appendChild(res);
	</script>

Use [`<link rel="preload" href="styles.css" as="style">`](https://www.w3.org/TR/preload/), work for `fetch`, `audio`, `font`, `image`, `script`, `style`, `track`, `video` and `image`. See [Fetch Standard](https://fetch.spec.whatwg.org/#concept-request-destination)

Use type parameter to specify the format of the resource. It's usefull to let the browser choose the supported format. But should be carefull defined (a browser support all available choices will preload all). In case you want to preload a font available in both WOFF and WOFF2, reclare only the last one (`font/woff2`), because browsers support preload also support this more recent format.

Note about mandatory `as` attribute and valid value:

- [Intent to Implement and ship: Mandatory `as` value for link rel preload - Google Groups](https://groups.google.com/a/chromium.org/forum/#!topic/blink-dev/mKkVXwMhOLc)
- [173047 – \[preload\] Mandatory `as` value and related spec alignments](https://bugs.webkit.org/show_bug.cgi?id=173047)
- [Issue 2903653005: \[preload\] Mandatory `as` value and related spec alignments - Code Review](https://codereview.chromium.org/2903653005)

Reactive prefetch: [Google mobile search is getting faster - to be exact, 100-150 milliseconds fa...](https://plus.google.com/+IlyaGrigorik/posts/ahSpGgohSDo)

	// <a href="https://example.com/">Example</a>
	// Will start to load the following resource even if the browser didn't start loading the main resource
	// It's like Link preload header but before the browser start the connection to the host
	myExampleLink.addEventListener("click", event => {
		for(const src of [
			"https://example.com/style.css",
			"https://example.com/script.js",
			"https://example.com/image.jpg",
		]){
			const hint = document.createElement("link");
			hint.rel = "prefetch";
			hint.href = url;
			document.head.appendChild(hint);
		}
	});

- [Preload - Use cases](https://w3c.github.io/preload/#use-cases)
- [Preload](https://www.w3.org/TR/preload/#h-attributes)
- [Preload: What Is It Good For? – Smashing Magazine](https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/)
- [Resource Hints](https://www.w3.org/TR/resource-hints/)
- [Preload img with CSS](CSS#preload-img-with-css)
- [Link prefetching FAQ - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Link_prefetching_FAQ)
- [Preloading content with rel="preload" - HTML | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Preloading_content)
- [Link prefetching — Wikipedia](https://en.wikipedia.org/wiki/Link_prefetching)
- [Prefetching, preloading, prebrowsing | CSS-Tricks](https://css-tricks.com/prefetching-preloading-prebrowsing/)
- [A Link: rel=preload Analysis From the Chrome Data Saver Team – reloading – Medium](https://medium.com/reloading/a-link-rel-preload-analysis-from-the-chrome-data-saver-team-5edf54b08715#.hewz602sh)
- [GoogleChromeLabs/quicklink: ⚡️Faster subsequent page-loads by prefetching in-viewport links during idle time](https://github.com/GoogleChromeLabs/quicklink)
- [instant.page](https://instant.page/) - Prefetch pages under pointer before the user click (~300ms with cursor, ~90ms with touch) [Technical details — instant.page](https://instant.page/tech) [instantpage/instant.page: Make your site’s pages instant in 1 minute and improve your conversion rate by 1%](https://github.com/instantpage/instant.page)

#### Download priority

- HTML (highest)
- CSS (highest)
- images (low or medium)
- XHR/Fetch (high)
- fonts (highest)
- scripts: low (async, defer or type module), medium (`<script src="script.js"></script>`) or high (`<script src="script.js"></script>` before an image)

**Note: this is how Chrome prioritize resources**

- [The Critical Request | CSS-Tricks](https://css-tricks.com/the-critical-request/#article-header-id-0)

- Browsers can’t possibly download background-images until they’ve built the CSSOM.
- Browsers shouldn’t base—thus delay—the downloading of `<img>`s on CSSOM completion.
- Browsers will download `<img>` completely independently of CSSOM construction. Blocking `<img>` on CSSOM construction seems very inefficient, and would lead to delays in downloading content.
- Accordingly, browsers will download `<img>` that end up being hidden from view, i.e. display: none;. If the browser starts downloading `<img>` before CSSOM construction (as I expect) then it has no way of knowing yet whether that image is needed or not.

- [Image Inconsistencies: How and When Browsers Download Images – CSS Wizardry – CSS Architecture, Web Performance Optimisation, and more, by Harry Roberts](https://csswizardry.com/2018/06/image-inconsistencies-how-and-when-browsers-download-images/)
- [Deep dive into the murky waters of script loading - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/speed/script-loading/)

#### On demand

Aka Lazyload, LOD, defered loading

Use `<noscript>` tags, or handle it with Service Worker (replace all `<img>` by a placeholder). See [`<noscript>` and search engines](#noscript-and-search-engines)

- [`<noscript>` and search engines](#noscript-and-search-engines)
- [Image lazyload](#image-lazyload) and [Non-blocking stylesheets](#non-blocking-stylesheet)
- [Extensible Web Resource Loading Manifesto - igvita.com](https://www.igvita.com/2014/10/02/extensible-web-resource-loading-manifesto/)
- [google - Is this a good approach to image Lazy Loading for SEO? - Webmasters Stack Exchange](http://webmasters.stackexchange.com/questions/26190/is-this-a-good-approach-to-image-lazy-loading-for-seo)
- [Redefining Lazy Loading With Lazy Load XT - Smashing Magazine](http://www.smashingmagazine.com/2015/02/03/redefining-lazy-loading-with-lazy-load-xt/)
- [Lazy loading and the SEO problem, solved! | Idea R Blog](https://www.idea-r.it/blog/110/en/lazy-loading-seo-problem#blogimage=5)
- [Make sure Google can see lazy-loaded content  |  Search  |  Google Developers](https://developers.google.com/search/docs/guides/lazy-loading)

Live streaming, or start play video when the file is not completely generated:

	<video>
		<source src="video.m3u8" type="application/x-mpegURL"><!-- HTTP Live Streaming, required by Safari in that case: if the media size is not known -→
		<source src="video.mpd" type="application/dash+xml"><!-- MPEG-DASH -→
		<source src="video.mp4" type="video/mp4"><!-- Use chunk encoding -→
		<!-- Or use JS to use MSE API for streaming protocols like DASH -→
	</video>

- [MPEG-DASH](MPEG-DASH)
- [Live streaming web audio and video - App Center | MDN](https://developer.mozilla.org/en-US/Apps/Fundamentals/Audio_and_video_delivery/Live_streaming_web_audio_and_video)

##### Image lazyload

**Use a placeholder element, or at least [use a SVG in data URI for the `src` attribute](https://css-tricks.com/preventing-content-reflow-from-lazy-loaded-images/#article-header-id-5) to prevent reflow**

1. placeholder shouldn't be visible if script is not available (inlined CSS hide the placeholder)
2. placeholder should have `role="img"` and `aria-label` set with image `alt` (will be set by the JS)
3. should works with complex image content (eg. `<figure>`)
	
TODO: support all replaced elements: video, audio and iframe. Use a weakmap or additional property to store the replacement fragment (parse noscript HTML only one time)
 
	<style>
	.img,
	.img-placeholder{
		display: block;
		/* height style of 69.44% is the equivalent for 16/9 of the width. See CSS#Vertical%20percentages */
		padding-top: 69.44%;
		background: grey;
		position: relative;
	}
	/* image fallback text (alt attribute) */
	.img::before{
		display: flex;
		position: absolute;
		top: 0;
		left: 25%;
		height: 100%;
		width: 50%;
		align-items: center;
		justify-content: center;
	}
	</style>
	<!--
	Don't display placeholders if script is disabled
	Can be a declared in linked (external) stylesheet but it's not recommended
	-->
	<style id="noscript-style">.img-placeholder{display: none;}</style>
	
	<script>
	document.getElementById("noscript-style").remove();
	document.addEventListener("DOMContentLoaded", event => {
		// documents without browsing context don't load resources (images will not be loaded)
		const doc = document.implementation.createHTMLDocument("");
		// Note: longdesc couldn't be direclty replaced by aria-describedby or aria-details
		const filterOutAttrs = "alt class crossorigin ismap longdesc referrerpolicy sizes src srcset usemap".split(" ");
		// Upgrade placeholder with all required attributes (role=img and aria-label) and remove noscript tags
		document.querySelectorAll(".img-placeholder").forEach(placeholder => {
			const noscript = placeholder.firstElementChild;
			doc.body.innerHTML = noscript.textContent;
			const img = doc.querySelector("img");
			// Copy all attributes from noscript tag to the placeholder
			Array.from(img.attributes).filter(attr => !filterOutAttrs.includes(attr.name)).forEach(attr => placeholder.setAttribute(attr.name, attr.value));
			// We don't need XML namespace here (HTML5 don't support it). Else use placeholder.setAttributeNS(attr.namespace, attr.localName, attr.value)
			placeholder.setAttribute("role", "img");
			placeholder.setAttribute("aria-label", img.alt);
			placeholder.dataset.srcdoc = noscript.textContent;// store raw HTML for later use
			// Remove the noscript tag
			noscript.remove()
		})
	});
	</script>
	
	<span class="img-placeholder" style="background: grey;"></span>
	<noscript><img class="img" src="cat.jpg" alt="A photography of a cat"></noscript>
	
	<figure>
		<span class="img-placeholder" style="background: brown;"></span>
		<noscript><img class="img" srcset="dog_2x.jpg 2x" src="dog.jpg" alt="A photography of a dog"></noscript>
		<figcaption>Fig1. A dog</figcaption>
	</figure>

	<span class="media-placeholder" style="background: red;"></span>
	<noscript><video class="media" src="fish.mp4">A video of a fish</video></noscript>

After a user action or intersection observation (scroll → visible in the viewport), replace the placeholder by the final HTML:

1. Read document visibility `document.visibilityState === "visible" || document.visibilityState === "prerender"`
2. Listen document visibility change `document.addEventListener("visibilitychange", documentVisibilityChange);` if hidden, store which placeholder(s) must be replaced then wait the document to be visible
3. Use the IntersectionObserver API of observe placeholders (currently) in the DOM
4. Use MutationObserver to handle DOM modifications (to observe later attached placeholders or disconnect detached placeholders). See [DOM mutation](../Development/JavaScript/Javascript.md#dom-mutation)
5. Use matchMedia API to match print media (to load all images)

		const mediaQuery = window.matchMedia("print");
		function mediaQueryChange(){
			if(!mediaQuery.matches){
				return;
			}
			mediaQuery.removeListener("change", mediaQueryChange);
			/*replace placeholder*/
		}
		mediaQueryChange();
		mediaQuery.addListener("change", mediaQueryChange);
6. Replace placeholders: `placeholder.replaceWith(document.createRange().createContextualFragment(placeholder.dataset.srcdoc));`

		const range = document.createRange();
		range.selectNode(placeholder.parentNode);
		placeholder.replaceWith(range.createContextualFragment(placeholder.dataset.srcdoc));// Note: createContextualFragment() is supported by IE11+

If the IntersectionObserver API is not supported:

- use the polyfill with caution, it's impact performance (use `getClientBoundingRect()` and `getComputedStyle`) and it's add weight to load. Additional the existing polyfill are not spec compilant, often don't handle visibility, parent non visible overflow or crop, CSS changes, etc.
- or fallback to scroll listener, `setInterval()` with a not too small delay and `getClientBoundingRect()`
- or load all lazyloaded images, it's the default behavior before lazyload has been implemented

See also:

- [`<noscript>` and search engines](#noscript-and-search-engines)
- [Progressive load](#progressive-load)
- [Progressivement en ‹img /› - da scritch net works](https://dascritch.net/post/2014/06/10/Progressivement-en-img#lazyloading)
- [aFarkas/lazysizes: High performance and SEO friendly lazy loader for images (responsive and normal), iframes and more, that detects any visibility changes triggered through user interaction, CSS or JavaScript without configuration.](https://github.com/aFarkas/lazysizes)

#### Progressive load

Or partial load

- load a thumbnail, then load the full image: [Faster Image Loading With Embedded Image Previews — Smashing Magazine](https://www.smashingmagazine.com/2019/08/faster-image-loading-embedded-previews/)
- [Dominant Colors for Lazy-Loading Images | manu.ninja](https://manu.ninja/dominant-colors-for-lazy-loading-images)
- [Progressive image](https://github.com/bompo/streamingtextures/)
- [WebGL — Progressive loading](http://www.khronos.org/webgl/public-mailing-list/archives/1104/msg00056.html)
- [Performance Calendar » Progressive jpegs: a new best practice](https://calendar.perfplanet.com/2012/progressive-jpegs-a-new-best-practice/)
- [How Medium does progressive image loading - JMPerez Blog](https://jmperezperez.com/medium-image-progressive-loading-placeholder/)
- [An Introduction to Progressive Image Rendering | Cloudinary Blog](https://cloudinary.com/blog/an_introduction_to_progressive_image_rendering)
- [Lazy loading images using Intersection Observer | Dean Hume](http://deanhume.com/home/blogpost/lazy-loading-images-using-intersection-observer/10163)
- Use same DCT coefficients, JPEGs with elided quant tables to reduce bytes loaded (recreate JPEG headers)
	Plus use blur and scale to display the thumb
	[The technology behind preview photos | Engineering Blog | Facebook Code](https://code.facebook.com/posts/991252547593574/the-technology-behind-preview-photos/)
- progressive JPEG and interlaced PNG: [Introduction to PNG - nuwen.net](http://nuwen.net/png.html) & [Progressive Image Rendering](http://blog.codinghorror.com/progressive-image-rendering/).
	But can make file larger: [png - When to interlace an image? - Stack Overflow](https://stackoverflow.com/questions/13449314/when-to-interlace-an-image/14124340#14124340)
	
	Benefit of HTTP2 multiplexing and progressive image to speed up first paint sooner
	
	See also [JPEG - Progressive](JPEG#Progressive) (scan config and number of it can be tweak)

For images (works better with progressive images), in Edge Workers (Service Workers for CDN):

1. receive the client request (for document, images, etc.)
2. send first 521B/1kB (headers of image / metadata - size) for the browser to do the layout as soon as possible
3. wait 20ms to let the client to process CSS, JS and other critical resources
4. send first 15% of the resource (~15% = contains the progressive bytes of the image)
5. wait for other resources (for the same client/requested document/referrer) to let the browser render first layers, before it recieve the rest of the resources
6. send the rest

- [Kornel Lesiński | Image Optimization | performance.now() 2018 - YouTube](https://www.youtube.com/watch?v=jTXhYj2aCDU?start=1035&end=1650)
- [HTTP/2 progressive image streaming](https://blog.cloudflare.com/parallel-streaming-of-progressive-images/)

- [“Async” CSS without JavaScript by Taylor Hunt on CodePen](https://codepen.io/tigt/post/async-css-without-javascript)
- [Modern Asynchronous CSS Loading | Filament Group, Inc., Boston, MA](https://www.filamentgroup.com/lab/async-css.html)
- [The Simplest Way to Load CSS Asynchronously | Filament Group, Inc.](https://www.filamentgroup.com/lab/load-css-simpler/)

An other solution:

	<link rel="stylesheet" href="styles/fonts.css" media="print" onload="media!='all'&&media='all'">
	<noscript><link rel="stylesheet" href="styles/fonts.css"></noscript>

But this still blocking DOM parser on few browsers (IE11, Firefox 36). See https://github.com/scottjehl/css-inapplicable-load#the-bad
Can be use to load fonts (inlined in CSS). Or use preload font

Note: `media!='all'&&...` is required as a workaround for infinite event loop on Firefox, where change media dispatch a new load event.

- [Loading CSS without blocking render by Keith Clark](http://keithclark.co.uk/articles/loading-css-without-blocking-render/)
- [“Async” CSS without JavaScript by Taylor Hunt on CodePen](https://codepen.io/tigt/post/async-css-without-javascript)
- [Fonts and FOXX](CSS#fonts-and-foxx)


See [`<noscript>` and search engines](#noscript-and-search-engines)

#### Critical path

Aka blocking dependencies, critical resources

To find blocking points / bottlenecks / critical rendering path

> A critical request is one that contains an asset that is essential to the content within the users viewport
> — [Ben Schwarz](https://speakerdeck.com/benschwarz/the-critical-request?slide=26)

- [Progressive Web Apps with React.js: Part 2 — Page Load Performance – Medium](https://medium.com/@addyosmani/progressive-web-apps-with-react-js-part-2-page-load-performance-33b932d97cf2#.w02rdqvxt)

Example: the hero image

> Optimise for the critical rendering path, get everything at the top of the page in view as fast as possible. Then lazy load the rest.

- [Mission Critical: optimizing CSS for CDN | Filament Group, Inc., Boston, MA](https://www.filamentgroup.com/lab/critical-cdn.html)
- [The Critical Request | CSS-Tricks](https://css-tricks.com/the-critical-request/#article-header-id-1)
- [Critical Rendering Path  |  Web Fundamentals  |  Google Developers](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/)
- [Rendering on the Web  |  Web  |  Google Developers](https://developers.google.com/web/updates/2019/02/rendering-on-the-web)

- [Bottleneck (production) — Wikipedia](https://en.wikipedia.org/wiki/Bottleneck_%28production%29)
- [Critical path method — Wikipedia](https://en.wikipedia.org/wiki/Critical_path_method)
- [Gantt chart — Wikipedia](https://en.wikipedia.org/wiki/Gantt_chart)

- HTML parser / main scanner:
	- build the DOM
	- blocked by the network
	- blocked by synchronous scripts (can alter the HTML stream), (wait for script to download and parsed, not always the case with speculative parsing), executed
		- [Scripts block parsing](https://3perf-server-delay-demo-kqemjsiqkk.now.sh/)
	- blocked by async JavaScript execution
	- recent engine preload resources even if the parser is paused
- preload scanner
	- if speculative parsing is not used, it's the same HTML parser
	- discover sub resources (CSS, JS, images)
	- blocked by the network
	- doesn't always support all kind of resources Firefox and IE/Edge
	- often operate when the main/HTML parser/scanner is blocked

	- [CSS Preload Scanner in WebKit · ariya.io](https://ariya.io/2013/04/css-preload-scanner-in-webkit)
	- [How the Browser Pre-loader Makes Pages Load Faster - Andy Davies](https://andydavies.me/blog/2013/10/22/how-the-browser-pre-loader-makes-pages-load-faster/)
	- [Building the DOM faster: speculative parsing, async, defer and preload - Mozilla Hacks - the Web developer blog](https://hacks.mozilla.org/2017/09/building-the-dom-faster-speculative-parsing-async-defer-and-preload/)
	- [CSS and Network Performance – CSS Wizardry – CSS Architecture, Web Performance Optimisation, and more, by Harry Roberts](https://csswizardry.com/2018/11/css-and-network-performance/)
	Note all CSS will be loaded, even if that doesn't match the current media, see [blog.tomayac.com » Blog von Thomas Steiner » homoblogiens](https://blog.tomayac.com/2018/11/08/why-browsers-download-stylesheets-with-non-matching-media-queries-180513)
- JavaScript
	- load start by preload scanner
	- blocked by the network
	- if async or synchronous, ran after downloaded
	- if defer, ran in order after HTML parser complete
	- if synchronous, ran only after CSSOM of previous (synchronous) stylesheets
		- https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2017/09/blocking-bold@2x-1.png
		- tips: move the script before blocking stylesheet if no need of CSSOM (often the case)
- readystatechange event (readyState = "interactive")
	
	- [readystatechange - Event reference | MDN](https://developer.mozilla.org/en-US/docs/Web/Events/readystatechange)
- readystatechange event (readyState = "complete")
	
	- [readystatechange - Event reference | MDN](https://developer.mozilla.org/en-US/docs/Web/Events/readystatechange)
- DOM Content Loaded event
	- fired after defer scripts are executed if any, else after HTML parser complete
	- fired after the transition to "interactive" but before the transition to "complete" of document readyState
	
	- [HTML Standard](https://html.spec.whatwg.org/#event-domcontentloaded)
	- [DOMContentLoaded - Event reference | MDN](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded)
	- [HTML Standard](https://html.spec.whatwg.org/#dom-document-readystate-dev)
- DOM Content Loaded event execution
	- fired after executing all listener of DOMContentLoaded event
- load event / fully loaded
	- after DOMContentLoaded event execution
	- fired when the document has finished loading
	
	- [HTML Standard](https://html.spec.whatwg.org/#event-load)
	- [load - Event reference | MDN](https://developer.mozilla.org/en-US/docs/Web/Events/load)
- background image
	- load start only if an element in the page use it (based on stylesheet)
	- blocked by the network
- stylesheet
	- building CSSOM
	- load start by preload scanner
	- laoded with low priorty if the media dosen't match
	- if in import rule, load start only after the parent stylesheet is loaded or by preload scanner if the parent stylesheet is inlined in the document
	- blocked by the network
	- blocked by import: CSSOM is complete after all sub stylesheets are loaded and parsed
- image
	- load start by preload scanner
	- blocked by the network
- DNS prefetch
	- start by preload scanner
- preconnect
	- start by preload scanner
- prefetch
	- start by preload scanner
- preload
	- start by preload scanner
- prerender
	- start by preload scanner
- start Render - the time from the start of the initial navigation until the first non-white content is painted
	- blocked ("rendering of subsequent content" / for progressive rendering) by sync stylesheets that match current media
		- [CSS and Network Performance – CSS Wizardry – CSS Architecture, Web Performance Optimisation, and more, by Harry Roberts](https://csswizardry.com/2018/11/css-and-network-performance/#firefox-and-ieedge-place-import-before-js-and-css-in-html#place-link-relstylesheet--in-body)
		- [The future of loading CSS - JakeArchibald.com](https://jakearchibald.com/2016/link-in-body/)
	- [Metrics - WebPagetest Documentation](https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics)
- font
	- load start only if an element in the page use it
- text render
	- if font face for custom font is declared, use it, else use fallback
	- if `font-display: auto`, wait for font load 3s maximum, then render the text with use the fallback if the custom font is not loaded
		> in all major browsers, this means the browser will wait 3 seconds for the custom font to download
		> Note: in Microsoft Edge, the font-display: auto behavior is different. With it, if the custom font is not cached, Edge immediately renders the text in the fallback font and substitutes the custom font later when it’s loaded. This is not a bug because font-display: auto lets browsers define the loading strategy.
	- if `font-display: fallback`, the text is rendered with custom font if is cached, else use the fallback font. The text is rerendered when the custom font is loaded
	- if `font-display: optional`, the text is rendered with custom font if is cached, else use the fallback font.
	- use fallback font (default serif)
		- [font-family - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/font-family#Values)
		- [Fundamental text and font styling - Learn web development | MDN](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Fundamentals#Web_safe_fonts)
		
	- [font-display - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display)
	- [Font-display playground](https://font-display.glitch.me/)
	- [`font-display` for the Masses | CSS-Tricks](https://css-tricks.com/font-display-masses/)
- Time To First Byte (TTFB)
- First Meaningful Paint (TTFMP / FMP) - The paint after which the biggest above-the-fold layout change has happened, and web fonts have loaded
	- when some contentful thing (text, image, canvas, or SVG) is painted for the first time
	- blocked by loading fonts (only for font that contains more than 200 characters, until the font is displayed with loaded font or with fallback font if 3 seconds timeout exceeded, based on `font-display`?)
	- [Time to First Meaningful Paint: a layout-based approach - Google Docs](https://docs.google.com/document/d/1BR94tJdZLsin5poeet0XoTW60M0SjvOJQttKT-JK8HI/edit)
- Time to First Paint (TTFP / FP) - The time when the browser first rendered after navigation. This excludes the default background paint, but includes non-default background paint.
	- when the browser first rendered after navigation. This excludes the default background paint, but includes non-default background paint and the enclosing box of an iframe.
	- [Time to First Meaningful Paint: a layout-based approach - Google Docs](https://docs.google.com/document/d/1BR94tJdZLsin5poeet0XoTW60M0SjvOJQttKT-JK8HI/edit)
	
	Heuristic/guess are used when "meaningful" was (the paint after the largest layout change). See also LCP.
	
	- [Paint Timing 1](https://w3c.github.io/paint-timing/#first-paint)
- Time to First Contentful Paint (TTFCP / FCP) - When the browser first rendered any text, image (including background images), non-white canvas or SVG. Text and graphics start to render (but often catches non-leaningful paints, e.g. headers, nav bars)
	- when the browser first rendered any text, image (including background images), non-white canvas or SVG. This excludes any content of iframes, but includes text with pending webfonts
		"Styles are loaded and browser can paint content"

	- [Paint Timing 1](https://w3c.github.io/paint-timing/#first-contentful-paint)
- Largest Contentful Paint (LCP) - when the main content of a web page has loaded
	
	- [Largest Contentful Paint  |  web.dev](https://web.dev/largest-contentful-paint/)
- First Input Delay (FID)
	First Click (Click Interaction Time), First scroll (Scroll Interaction Time), First Key (Key Interacton Time)
	- based on users interaction, based on RUM
- FCI (First CPU Idle) / TFI (Time to First Interactive) - Page is minimally interactive, most visible UI elements are interactive, repsonds to user input reasonably quickly
	
	- [First Input Delay  |  Web  |  Google Developers](https://developers.google.com/web/updates/2018/05/first-input-delay)
- Time to interactive (TTI) / Time to Consistently Interactive (TCI) - when the page is first expected to be usable and will respond to input quickly
	It is the first span of 5 seconds where the browser main thread is never blocked for more than 50ms after First Contentful Paint with no more than 2 in-flight requests
	Displays useful content, event handlers are registered for most visible elements, page responds to user interaction within 50ms
	- fired when page's resources are loaded (load event) and the main thread is idle (for at least 5 seconds)
	
	- [webpagetest/TimeToInteractive.md at master · WPO-Foundation/webpagetest](https://github.com/WPO-Foundation/webpagetest/blob/master/docs/Metrics/TimeToInteractive.md)
	- [First Input Delay  |  Web  |  Google Developers](https://developers.google.com/web/updates/2018/05/first-input-delay)
	- [GoogleChromeLabs/first-input-delay](https://github.com/GoogleChromeLabs/first-input-delay)
- Speed Index - the average time at which visible parts of the page are displayed. It is expressed in milliseconds
	- [Speed Index - WebPagetest Documentation](https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index)
- Visual Complete - first time when the visual progress reaches 100%

Composite metric examples (based on what the user care about):
	
- Pinterest use Pinner Wait Time (PWT)
	- [Get Down to Business: Why the Web Matters (Chrome Dev Summit 2018) - YouTube](https://www.youtube.com/watch?v=Xryhxi45Q5M&t=1214)
	- "For us, that’s images. Until the above-the-fold images are loaded, to our users, page load is not complete."
	- "Time to Interactive" and "Above-the-Fold Images"
- Twitter use Time to First Tweet (TFT)
- Hero Rendering Times (HRT) - Combination of when the largest IMG, H1, and background image in the viewport are rendered
	Don't work for image carousels and popups
	- `max(h1, (biggest_img || bg_img))`
	- [SpeedCurve | Hero Rendering Times: New metrics for measuring UX](https://speedcurve.com/blog/web-performance-monitoring-hero-times/)
- Time To Interactive (TTI)
- largest background image rendered
- largest image render
- H1 render
- Second Meaningful Content (SMC) for page with A/B tests
	- [Second Meaningful Content: the Worst Performance Metric | Filament Group, Inc., Boston, MA](https://www.filamentgroup.com/lab/second-meaningful-content.html)

Which metric is best?

- deliver any content: Start render
- deliver significant amount of content: speed index, FMP
- deliver critical content: Hearo Rendering Times

- [Web Performance Calendar » Developing the Largest Contentful Paint Metric](https://calendar.perfplanet.com/2019/developing-the-largest-contentful-paint-metric/) - What makes a good metric? (tl;dr: representative, accurate, stable, interpretable, simple, elastic, realtime, orthogonal)
- [SpeedCurve | Evaluating rendering metrics](https://speedcurve.com/blog/rendering-metrics/)
- [Picker - Rendering Metrics](http://lab.speedcurve.com/rendering/picker.php)

##### Anatomy of a webpage

Aka wireframe of a webpage

**Note: always render document server side. All the document content must be delivered.**
JavaScript (client side) can be used to enhance experience (loading, UI elements, etc.). See [Progressive Enhancement](#progressive-enhancement)

**Have things (critical content) before 1000ms.** See [responsiveness](UI - UX#responsiveness)

Anatomy/wireframe of a webpage:

	<!--
	HTTP header `Link` dns-prefetch, preconnect and preload for critical style, script and content
	Critical styles and scripts should be in the [Initial TCP window](#initial-tcp-window)
	Inlined scripts below, can be files if pushed with HTTP/2 server push before the HTML document
	-->
	<!DOCTYPE html>
	<html lang="en">
		<head>
			<!--
			Page format
			Before any other resource and content
			-->
			<meta charset="utf-8"><!-- First, must be within the first 1024 bytes. Required or use a BOM or charset parameter in Content-Type header -->
			<meta http-equiv="..." content="...">
			<base ...><!-- if base is used, not adviced -->
			
			<!--
			Meta viewport and title
			On top
			-->
			<meta name="viewport" content="width=device-width, initial-scale=1">
			<title>...</title><!-- Limited to 80 chars max -->
			
			<!--
			Prerequises scripts
			Device detection (mediaqueries, etc.) or page location redirection that not require to display anything
			-->
			<script>/*inlined script*/</script>
			
			<!--
			Critical styles
			Style for critical content: above floating line (main nav, header, hero image, article) or show a loader, while the rest is loading.
			Shouldn't be used to display aside content: comments, commercial components/ads, popular content, related content, sharing widgets, etc.
			See [Critical rendering path](#critical-rendering-path)
			-->
			<style>/*inlined style*/</style>
			<link rel="stylesheet" href="..."><!-- Only if pushed with HTTP/2 server push -->
			<style>.icon{width:1em;height:1em}</style><!-- Use to prevent inlined SVG icons be unscaled -->
			
			<!--
			Critical script
			Script for critical content: display a loader, handle critical content interaction/layout while the non critical content is loading.
			See [Critical rendering path](#critical-rendering-path)
			-->
			<script>/*inlined script*/</script>
			<script src="..."></script><!-- Only if pushed with HTTP/2.0 server push before the HTML document -->
			
			<!--
			Resources hint (dns-prefetch, preconnect and preload)
			Can be set as Link header
			-->
			<link rel="preconnect dns-prefetch" href="..."><!-- more than one relationship can be used, here dns-prefetch is used as a fallback. Note: this can create multiple network call -->
			<!-- Preload only if the resources must be start loading before the critical content, like the hero image. See "For non critical content" section -->
			<link rel="preload" href="..." as="style"><!-- for images, fonts, etc. Attributes type="" and media="" can also be used -->
			<!-- Examples: -->
			<link rel="preload" href="font.woff" as="font" type="font/woff" media="min-width: 768px" crossorigin>
			<link rel="preload" href="font.woff2" as="font" type="font/woff2" media="min-width: 768px" crossorigin>
			
			<!--
			For non critical content
			Non blocking resource (styles and scripts)
			See also [Non-blocking stylesheet](#non-blocking-stylesheet) and [Blocking resources](#blocking-resources)
			-->
			<noscript>
				<link rel="stylesheet" href="styles.css">
				<!-- script that inject other SVGs icons (symbols) -->
				<script src="..."></script><!-- other scripts -->
				<link rel="preload" href="..." as="style"><!-- for images, fonts, etc. Attributes type="" and media="" can also be used -->
			</noscript>
			<script>/*script that listen DOMContentLoaded then inject the content of the noscript (resource are inserted as non blocking)*/</script>
			
			<!--
			Metadata, manifest, document relationship, future navigation hint (prefetch, next, prerender), etc.
			Others things that should be in the header
			See https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types
			See https://developer.mozilla.org/en-US/docs/Web/HTTP/Link_prefetching_FAQ
			-->
			<meta name="..." content="...">
			<meta property="..." content="...">
			<link rel="alternate" type="application/rss+xml" title="..." href="..."><!-- RSS -->
			<link rel="alternate" type="application/json" title="..." href="...">
			<link rel="canonical" href="...">
			<script type="application/json">...</script><!-- store data for machines, will be fetched by JavaScript after defer or DOMContentLoaded events -->
			<script type="application/ld+json">...</script>
			<link rel="icon" type="image/svg+xml" sizes="any" href="/favicon.svg"><!-- Favicon, prefer SVG and fallback to PNG. See https://realfavicongenerator.net/faq -->
		</head>
		<body>
			<!--
			Critical content
			-->
			<img src="..." alt="">
			<svg><symbol>...</symbol></svg><!-- inlined SVGs icons (symbols) required by critical content. Note: HTML5 spec doesn't allow `svg` element to be in `head` -->
			
			<!--
			Non critical content
			See [Image lazyload](#image-lazyload)
			-->
			<link rel="stylesheet" href="..."><!-- only if use HTTP/2.0 (allowed in body) https://html.spec.whatwg.org/multipage/links.html#body-ok https://jakearchibald.com/2016/link-in-body/#a-simpler-better-way -->
			<style id="noscript-style">.media-placeholder{display: none;}</style><!-- can be placed anywhere before in the body or the header. ("[can be used] in the body, where flow content is expected.") https://www.w3.org/TR/html52/document-metadata.html#the-style-element
			<script>/*progressive enhancement of media placeholder script*/</script><!-- can be in the footer -->
			<span class="media-placeholder" style="background: grey;"></span><noscript><img class="media" src="cat.jpg" alt="A photography of a cat"></noscript>
			<span class="media-placeholder" style="background: black;"></span><noscript><video class="media" src="dog.mp4">A video of a dog play with a ball</video></noscript>
			<p>...</p>
			
			<!--
			Non critical scripts and styles
			For tracking, ads, etc..
			See [Blocking resources](#blocking-resources)
			Could be in the section "For non critical content" inside noscript in the header
			-->
			<script src="" defer></script>
			<!-- No inlined scripts here or only if not big and support async API, something like: `window.cmd=window.cmd||[];cmd.push(() => console.log("do something"))` -->
		</body>
	</html>

See also [Critical rendering path](#critical-rendering-path) and [Blocking resources](#blocking-resources)

Use HTTP2:

	<?php
	// Is HTTP/2.X
	if(substr($_SERVER['SERVER_PROTOCOL'], 0, 7) === 'HTTP/2.'){
		header('Link: </styles/critical.css>; rel=preload; as=style');
		echo '<link href="/styles/critical.css" rel="stylesheet">';
		// script 1, script 2, script 3...
	}else{
		echo '<style>';
		include('styles/critical.css');
		echo '</style>';
		// script bundle
	}
	// then the method used to load async /styles/content.css
	?>

- [Understanding Critical CSS – Smashing Magazine](https://www.smashingmagazine.com/2015/08/understanding-critical-css/)
- https://github.com/bocoup/critical-css-boilerplate
- [DOMContentLoaded and stylesheets · molily](http://molily.de/domcontentloaded/#appendix)
- [DOMContentLoaded - Event reference | MDN](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded)
- Use progress events for media (img, video and audio) element. See [Image dispatch progress events](JavaScript#image-dispatch-progress-events)
- [CSSconf EU 2014 | Patrick Hamann: CSS and the Critical Path ](https://www.youtube.com/watch?v=_0Fk85to6hA)
- [Deep dive into the murky waters of script loading - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/speed/script-loading/)
- [Faster Pageloads: Effectively using HTTP Caching, Cache Busting, and a CDN - FoxyCart](http://www.foxycart.com/blog/caching-and-cdn#.VPZa0xfHNE4)
- [Your Hero Images Need You: Save the Day with HTTP/2 Image Loading - YouTube](https://www.youtube.com/watch?v=66JINbkBYqw)

##### Blocking resources

> Browser requests the HTML document Begins parsing and constructing DOM Discovers CSS/JS Waits for CSS response Constructs CSSOM Combines CSSOM and DOM intro render tree Font requests are dispatched after the render tree indicates which font variants are needed to render the specified text on the page.
> — Slide 16 of [To push, or not to push?!](https://noti.st/patrickhamann/ocAYxy/to-push-or-not-to-push) by Patrick Hamann

![To Push, Or Not To Push   Slide 16](Optimizations%20and%20performances/To%20push,%20or%20not%20to%20push%20-%20slide%2016.jpg)
![Compare classic script, async, defer, module and async module blocking behaviors](https://developers.google.com/web/fundamentals/primers/imgs/async-defer.svg) https://developers.google.com/web/fundamentals/primers/modules#defer

Blocking parser and blocking rendering

> A friendly reminder that any `<link rel="stylesheet">` in your `<head>` will block first paint until **all** of them are done downloading.

[Stylesheet are blocking resources](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css).

> Synchronous scripts in body block rendering

Defer and async script

**Prefer `defer` over `async` for regular scripts.**

These scripts shouldn't contains `window.write()` (blocking)

Defer: Use the script as non blocking script. Be executed when the HTML document is done being parsed (aka DOM Interactive or `performance.timing.domInteractive`)
Async: Use the script as non blocking script. Be executed as soon as possible, **don't respect execution based on the order in document (out-of-order)**
At the bottom: Use the script as blocking script. Should be executed after all previous blocking resources being loaded and parsed. (before document load event). **Prefer defer or async instead**

![Font critical rendering path](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/images/font-crp.png) [Web Font Optimization | Web Fundamentals | Google Developers](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/webfont-optimization?hl=en#the_default_behavior)

- [Building the DOM faster: speculative parsing, async, defer and preload ★ Mozilla Hacks – the Web developer blog](https://hacks.mozilla.org/2017/09/building-the-dom-faster-speculative-parsing-async-defer-and-preload/)
- [Load Non-blocking JavaScript with HTML5 Async and Defer](https://www.sitepoint.com/non-blocking-async-defer/)
- [Async scripts for asm.js - Game development | MDN](https://developer.mozilla.org/en-US/docs/Games/Techniques/Async_scripts)
- [\<script\> - HTML | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#attr-async)
- [Performance Calendar » Prefer DEFER Over ASYNC](http://calendar.perfplanet.com/2016/prefer-defer-over-async/)
- [Async Attribute and Scripts At The Bottom | CSS-Tricks](https://css-tricks.com/async-attribute-scripts-bottom/)
- [Loading Third-Party JavaScript  |  Web Fundamentals  |  Google Developers](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/loading-third-party-javascript/#use_async_or_defer)
- [Optimizing HTTP/2 prioritization with BBR and tcp_notsent_lowat](https://blog.cloudflare.com/http-2-prioritization-with-nginx/#browsersandrequestprioritization)
- [Download priority](#download-priority)
- [Load external script](Javascript.md#load-external-script)

###### Non-blocking stylesheet

	<link rel="preload" href="styles.css" as="style" onload="rel='stylesheet';onload=0">
	<noscript><link rel="stylesheet" href="styles.css"></noscript>

### Reduce media memory usage

For images and videos

By drawing downscaled images when smaller image are required.

- https://github.com/PixelsCommander/CanvasImage

#### Compressed textures

Use compressed textures and/or less bytes per channels (require canvas).

See [Decompression using GPU](Video#decompression-using-gpu)

See [Texture format](Texture format)

- [WebGLRenderingContext.texImage2D() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/WebGLRenderingContext/texImage2D)
- [WebGLRenderingContext.compressedTexImage2D() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/WebGLRenderingContext/compressedTexImage2D)
- [WebGL best practices - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/WebGL_best_practices)
- [WEBGL_compressed_texture_pvrtc - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_compressed_texture_pvrtc)
- [TojiCode: Compressed Textures in WebGL](http://blog.tojicode.com/2011/12/compressed-textures-in-webgl.html)
- [Texture Format Tester](http://toji.github.io/texture-tester/)
- [How to write portable WebGL - Codeflow](http://codeflow.org/entries/2013/feb/22/how-to-write-portable-webgl/)
- http://wayback.archive.org/web/20141203033529/http://web5.projekti.info/webgl/examples/
- [Android OpenGL Texture Compression - Stack Overflow](https://stackoverflow.com/questions/9148795/android-opengl-texture-compression/9514396#9514396)
- [WebGL Browser Report — WebGL Detection — WebGL Tester — BrowserLeaks.com](https://www.browserleaks.com/webgl)
- [WebGL Stats](http://webglstats.com/)
- [Unity - Mobile Hardware Stats](http://hwstats.unity3d.com/mobile/gpu.html)

Major compressed texture formats support (from WebGL Stats 02/2016):

1. `WEBGL_compressed_texture_s3tc` 84.2%
2. `WEBGL_compressed_texture_etc1` 13.1%
3. `WEBGL_compressed_texture_pvrtc` 7.4%
4. `WEBGL_compressed_texture_atc` 2.4%
5. `WEBGL_compressed_texture_astc` (Mali GPU, ex.: Galaxy S6)

Watch texture max size `gl.getParameter(gl.MAX_TEXTURE_SIZE)`. Prefer use 4096 × 4096

> Error: WebGL: compressedTexImage2D: the maximum texture size for level 0 is 4096

WebGL DDS + texture atlas 4096 require `bufferData`/`texImage2D` + check an `OUT_OF_MEMORY` errors

RGBA4444 = 16bit **but not related to paletted**, use `context.texImage2D(context.TEXTURE_2D, 0, context.RGBA, context.RGBA, context.UNSIGNED_SHORT_4_4_4_4, data);` where `data` must be an `Uint16Array` (4bits for each colors, something like `Uint4ClampedArray`) with each channel must be clamped to `0xF` (not directly compatible with a PNG16 image)

Note: In WebGL 2, `PALETTE8_RGBA8_OES` can be used with `compressedTexImage2D()` to upload paletted colors (like from PNG8): https://www.opengl.org/registry/specs/OES/OES_compressed_paletted_texture.txt

### Performance reporting

Aka client timing

See JavaScript [Performance API](https://developer.mozilla.org/en-US/docs/Web/API/Performance) (ex: `window.performance.getEntriesByType("resource")`) and `navigator.sendBeacon()`

![HTTPS ClientTimings](https://nickcraver.com/blog/content/HTTPS-ClientTimings.png) — From [Nick Craver - HTTPS on Stack Overflow: The End of a Long Road](https://nickcraver.com/blog/2017/05/22/https-on-stack-overflow/#preparing-for-a-proxy-client-timings) 

- [SpeedCurve | Synthetic: WebPageTest](https://speedcurve.com/features/synthetic/)

### AMP

> CSS is limited to 50KB and only inline, custom JS is not allowed (other than via an iframe method), and all images are guaranteed to be lazy loading.
> [...]
> Technically correct AMP pages will perform very similar to any non-horrible web page.
> [...]
> Part of that answer you can probably guess: the cache is simply very fast. It’s hard to compete with a Google-class CDN. I imagine thousands of servers strategically placed worldwide on the best connections available.
> [...]
> on Google Search on mobile [...] Pretty much anything that page needs to render is **preloaded**, whether you actually open it not.
> [...]
> > The AMP page, which we all believe to be super fast and optimized for slow mobiles because it is AMP, isn’t that fast. Its true speed comes from preloading.
— [AMP: the missing controversy – Ferdy Christant](https://ferdychristant.com/amp-the-missing-controversy-3b424031047)

Cache:

- [Overview  |  Google AMP Cache  |  Google Developers](https://developers.google.com/amp/cache/overview#google-amp-cache-updates)
- [Update AMP Content  |  Google AMP Cache  |  Google Developers](https://developers.google.com/amp/cache/update-cache)

Others links:

- [How AMP Works – AMP](https://www.ampproject.org/learn/about-how/)
- [Everything You Need To Know About Google's Accelerated Mobile Pages — Smashing Magazine](https://www.smashingmagazine.com/2016/02/everything-about-google-accelerated-mobile-pages/)
- [Adactio: Journal—AMPstinction](https://adactio.com/journal/13964)
- [Google AMP lowered our page speed, and there's no choice but to use it - unlike kinds](https://unlikekinds.com/amp/article/google-amp-page-speed)

### Third parties webperf

See also [Third parties](#third-parties)

- [Hard Costs of Third-Party Scripts - daverupert.com](https://daverupert.com/2018/10/hard-costs-of-third-party-scripts/)
- [Improving third-party web performance at The Telegraph](https://medium.com/the-telegraph-engineering/improving-third-party-web-performance-at-the-telegraph-a0a1000be5)
- [Smashing Magazine sur Twitter : "⌘ Taking control over third-party content to maintain performance. https://t.co/YzjrLvVc3y http](https://mobile.twitter.com/smashingmag/status/944920025823174657)
- [Third-Party Script Prevalence on Alexa Top 50 | Trent Walton](http://trentwalton.com/notes/2018/01/23/third-party-script-prevalence-on-alexa-top-50.html)
- [Loading Third-Party JavaScript  |  Web Fundamentals  |  Google Developers](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/loading-third-party-javascript/)
- [Performance Calendar » Reducing Single Point of Failure using Service Workers](https://calendar.perfplanet.com/2015/reducing-single-point-of-failure-using-service-workers/) - Block slow third-party with service worker
- [Improving third-party web performance at The Telegraph](https://medium.com/the-telegraph-engineering/improving-third-party-web-performance-at-the-telegraph-a0a1000be5) - "delete old third party scripts and see if anyone complains"
- [After GDPR, The New York Times cut off ad exchanges in Europe - and kept growing ad revenue - Digiday](https://digiday.com/media/gumgumtest-new-york-times-gdpr-cut-off-ad-exchanges-europe-ad-revenue/) - "serving regular, un-targeted ads could actually increase revenue" (remove cookie syncing and retargeting, that generate large amount of requests)
- [Andy Davies sur Twitter : "Only load what’s needed to display the initial button and then lazy-load the rest is an approach every live chat, feed widget etc should take. Currently they typically have a 500KB to 1MB bundle which just displays a button unless someone interacts with it!… https://t.co/ZNblwfAVwJ"](https://twitter.com/andydavies/status/1199236204723613696?s=12)
- [Loading Third-Party JavaScript  |  Web Fundamentals  |  Google Developers](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/loading-third-party-javascript/#lazy-load_third_party_resources) - "Lazy-load Third Party Resources"

## Detection

**Always use feature detection (Don't sniff User Agent! Never!)** instead of browser/platform detection. Easyer client side with JavaScript or CSS.

> `var webkit = !document.uniqueID && !window.opera && !window.globalStorage`: old code that evaluates to true in IE, Opera + Firefox today.
— [Mike Taylor on Twitter](https://twitter.com/miketaylr/status/598211928272437248)

- [User Agent String](#user-agent-string)
- [Detect touch device](JavaScript#detect-touch-device)
- [peter.michaux.ca - Feature Detection: State of the Art Browser Scripting](http://peter.michaux.ca/articles/feature-detection-state-of-the-art-browser-scripting)
- [Browser Detection (and What to Do Instead)](http://jibbering.com/faq/notes/detect-browser/)
- [Same Markup: Writing Cross-Browser Code - IEBlog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/ie/archive/2010/04/14/same-markup-writing-cross-browser-code.aspx)
- http://detectmobilebrowsers.com/ - Simplified (support lot of language) and not up-to-date UA detection.
- [Browser detection using the user agent | MDN](https://developer.mozilla.org/en-US/docs/Browser_detection_using_the_user_agent)
- [4 Bad Reasons To Detect Mobile Browsers](http://markonphp.com/4-bad-reasons-to-detect-mobile-browsers/) 
- [Mobile Grade (A, B, C)](http://jquerymobile.com/browser-support/)
	* A-grade: Full enhanced experience with Ajax-based animated page transitions.
	* B-grade: Enhanced experience except without Ajax navigation features.
	* C-grade: Basic, non-enhanced HTML experience that is still functional.
- [Modernizr: the feature detection library for HTML5/CSS3](https://modernizr.com/)
- [User-Agent detection, history and checklist ★ Mozilla Hacks – the Web developer blog](https://hacks.mozilla.org/2013/09/user-agent-detection-history-and-checklist/)
- [Detector — feature-detection library](https://github.com/dmolsen/Detector)
- [Client-Hints](https://github.com/igrigorik/http-client-hints) - intended to be used as input to proactive content negotiation
- [WhichBrowser/Parser: Browser sniffing gone too far — A useragent parser library for PHP](https://github.com/WhichBrowser/Parser)
- [serbanghita/Mobile-Detect: Mobile_Detect is a lightweight PHP class for detecting mobile devices (including tablets). It uses the User-Agent string combined with specific HTTP headers to detect the mobile environment.](https://github.com/serbanghita/Mobile-Detect) - Can also detect crawler / bots
- [Adapting for the Times // Speaker Deck](https://speakerdeck.com/steveworkman/adapting-for-the-times?slide=22)
 
	# From https://speakerd.s3.amazonaws.com/presentations/0c3a0cee177346fcb5acbe81a440377d/slide_21.jpg?1476842385
	<IfModule mod_rewrite.c>
		RewriteEngine on
		
		# See https://github.com/serbanghita/Mobile-Detect
		
		# Check for mobile
		# Android is only being used below 2.3 and "Mobile" above to ignore android tablets
		RewriteCond %{HTTP_USER_AGENT} "iPhone|Android|BlackBerry|Windows CE|IEMobile|Alcatel-OT|Opera Mobi|Opera Mini|DoCoMo.*N905i|DoCoMo.*P900i|Obigo|Wapsilon|WinCE|YourWap|Motorola|Samsung-|SAMSUNG-|portalmm|Telit_Mobile_Terminals|MobilePhone|SIE-|SCH-|GoodAccess|NEC-|Mitsu|Ericsson|AUDIOVOX-|LGE-|Sanyo-|Nokia|Alcatel-B|KDDI-|WAPman|WapTunner|WinWAP|ACS-NF\/3.0 NEC-|Vodafone|ZTE-|LG-|Sendo|SHARP-|TSM-|SAGEM-|MOT-|WIG Browser|Amoi|Symbian|J2ME|HTC|SPV|MOTO|Moto|SEC-SGH|Xda|XDA|iPAQ|MDA-vario|MDA Vario|MDA Touch|MDA_Vario|MDA_compact|MDA compact|MDA_Touch|MDA_vario|Novarra|webOS"
		RewriteRule .* - [E=device:simplephone]
		
		# Check for smartphones
		# WebKit: iPhone 4+ (& iPod), Android 2.3+, Blackberry 6+
		RewriteCond %{HTTP_USER_AGENT} "((iPhone(.* )OS( +)(([4-9])|([0-9]+[0-9]))[^0-9])|(Android( *)((2[^0-9][1-9])|([4-9][^0-9])|([0-9]+[0-9][^0-9])))|(BlackBerry( *)(([6-9])|([0-9]+[0-9]))[^8-9]))(.*)AppleWebKit"
		RewriteRule .* - [E=device:smartphone]
		
		# Check for devices that look like phones but are really tablets
		# That's Android 3.x - all of which are tablets
		RewriteCond %{HTTP_USER_AGENT} "Android( ?)3\."
		RewriteRule .* - [E=device:default]
		
		# Override settings by cookie for device switchers
		RewriteCond %{HTTP_COOKIE} device=([^;]+) [NC]
		RewriteRule .* - [E=device:%1]
		
		# Override setting with query string for testing
		RewriteCond %{QUERY_STRING} "^(.+&)?device=([^&]+)(&.+)?"
		RewriteRule .* - [E=device:%2]
		
		# Set environment variable mobile=1 in case smart of simple phone
		# Se query string fragment: qs4device in case smart or simple phone
		RewriteCond %{ENV:device} ^(.*phone)$
		RewriteRule .* - [E=mobile:1,E=qs4device:device\=%1]
		
		# Otherwise it's desktop
		RewriteCond %{ENV:device} "^(default)?$"
		RewriteRule .* - [E=device:default,E=qs4device:layout=desktop]
		</ifModule>
		
		# Setting the Vary: User-Agent
		# Make sure proxies and google crawl the pages with different UserAgents
		# See also: https://developers.google.com/webmasters/smartphone-sites/details
	<ifModule mod_headers.c>
		Header set Vary "User-Agent"
	</ifModule>

## Analytics

Tracking and analytics

Use [Navigator.sendBeacon() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)

### Tracking data

- page view
- printing

		<link rel="stylesheet" href="track_printing.css" media="print" type="text/css" />

	`track_printing.css` (should be served with header that disable cache): 

		body { background: url("http://path.to/tracker_script"); }
- default font size (use blank iframe)
- default zoom level
- screen size
- language
- user timing

### Tracking events

- **[Google Analytics Classic is repreciated](https://support.google.com/analytics/answer/4457764?hl=en)**
- https://developers.google.com/analytics/devguides/collection/analyticsjs/

- [GA Event Tracking Code Generator](https://raventools.com/gaconfig/google-analytics-event-tracking/general-event/)
- https://support.google.com/analytics/answer/1033068?hl=en
- https://developers.google.com/analytics/devguides/collection/analyticsjs/events
- https://developers.google.com/analytics/devguides/collection/analyticsjs/field-reference
- https://developers.google.com/analytics/devguides/collection/analyticsjs/command-queue-reference

**[Be carefull of types (integer for eventValue)](https://stackoverflow.com/questions/31204495/google-analytics-not-logging-events-with-a-value)**

#### Google Analytics Legacy

Aka `ga.js`

**Use [analytics.js](#universal-analytics-tracking-library) instead**

**Use async, via `_gaq.push()`**

	<script type="text/javascript">
		(window._gaq = _gaq || []).push(
			["_setAccount", "UA-XXXXX-X"],
			["_trackPageview"]
		);
		(function(d,t,s,l) {s=d.createElement(t),l=d.getElementsByTagName(t)[0];s.async=true;s.src="http"+("https:"==document.location.protocol?"s://ssl":"://www")+".google-analytics.com/ga.js";l.parentNode.insertBefore(s,l);})(document, "script");
	</script>

	_gaq.push(["_trackEvent", category, action, label/*optional*/, value/*integer, optional*/, opt_noninteraction/*boolean, optional*/]);

- [Introduction to ga.js (Legacy)  |  Analytics for Web (ga.js)  |  Google Developers](https://developers.google.com/analytics/devguides/collection/gajs/)
- [Google Analytics Tracking Code  |  Analytics for Web (ga.js)  |  Google Developers](https://developers.google.com/analytics/devguides/collection/gajs/methods/)

#### Universal Analytics tracking library

Aka `analytics.js`

[Universal Analytics tracking library (analytics.js)](https://developers.google.com/analytics/devguides/collection/analyticsjs/):
 
	ga("send", "event", category, action, label/*optional*/, value/*integer, optional*/, noninteraction/*boolean, optional*/);
	ga("send", "event", category, action, label/*optional*/, value/*integer, optional*/, {nonInteraction: noninteraction}/*boolean, optional*/);

	<!-- Google Analytics -→
	<script>
	window.ga=window.ga||function(){(ga.q=ga.q||[]).push(arguments)};ga.l=+new Date;
	ga("create", "UA-XXXXX-Y", "auto");
	ga("send", "pageview");
	</script>
	<script async src="https://www.google-analytics.com/analytics.js"></script>
	<!-- End Google Analytics -→

For a custom function name: (ex: `__gaTracker`)

	<!-- Google Analytics -→
	<script>
	(function(w,n){w.GoogleAnalyticsObject=n;w[n]=w[n]||function(){(w[n].q=w[n].q||[]).push(arguments)};w[n].l=+new Date;})(window,"__gaTracker");
	__gaTracker("create", "UA-XXXXX-Y", "auto");
	__gaTracker("send", "pageview");
	</script>
	<script async src="https://www.google-analytics.com/analytics.js"></script>
	<!-- End Google Analytics -→

	GoogleAnalyticsObject

	ga("send", "event", {
		eventCategory: "Category",
		eventAction: "Action",
		eventLabel: "Label"/*optional*/,
		eventValue: 55/*integer, optional*/,
		eventNonInteraction: 55/*integer, optional*/
	});

	ga("send", {
		hitType: "event",
		eventCategory: "Category",//ex: Videos
		eventAction: "Action",//ex: play
		eventLabel: ""//ex: video title
	});

- [Adding analytics.js to Your Site  |  Analytics for Web (analytics.js)  |  Google Developers](https://developers.google.com/analytics/devguides/collection/analyticsjs/)
- [The ga Command Queue Reference  |  Analytics for Web (analytics.js)  |  Google Developers](https://developers.google.com/analytics/devguides/collection/analyticsjs/command-queue-reference)
 
	// Use beacon or fallback to xhr (instead of image)
	ga("set", "transport", navigator.sendBeacon ? "beacon" : "xhr");

- [Sending Data to Google Analytics  |  Analytics for Web (analytics.js)  |  Google Developers](https://developers.google.com/analytics/devguides/collection/analyticsjs/sending-hits#specifying_different_transport_mechanisms)

Social interactions:

- [Social Interactions  |  Analytics for Web (analytics.js)  |  Google Developers](https://developers.google.com/analytics/devguides/collection/analyticsjs/social-interactions)

#### Google Tag Manager

Aka GTM

Handle inclusion of libraries (third party services).

See also: [Third parties](#third-parties)

Allow predefined set of events (category + action + label + value, etc.) with macros, conditions, etc.

```html
<script>(window.dataLayer=window.dataLayer||[]).push({'gtm.start':new Date().getTime(),event:'gtm.js'});)</script>
<script src="https://www.googletagmanager.com/gtm.js?id=GTM-XXXX" async></script>
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-XXXX" height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<script>
document.addEventListener("someevent", () => {
	window.dataLayer = window.dataLayer || [];

	dataLayer.push({
		event: "some event name",
		customData: "some value"
	})
});
</script>
```

- [Quick Start Guide  |  Google Tag Manager for Web Tracking  |  Google Developers](https://developers.google.com/tag-manager/quickstart)
- [Developer Guide  |  Google Tag Manager for Web Tracking  |  Google Developers](https://developers.google.com/tag-manager/devguide)
- [Reference  |  Google Tag Manager for Web Tracking  |  Google Developers](https://developers.google.com/tag-manager/reference)

#### Privacy

**Use "do not track" feature [`navigator.doNotTrack`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/doNotTrack)**

```js
function trackOutboundLink(url) {
	// check if the GA object exists and that it has initialized
	if(window.ga && ga.loaded && navigator.doNotTrack == "1") {
		// if yes, rely on GA to follow link
		ga('send', 'event', 'outbound', 'click', url, {
			'transport': 'beacon',
			'hitCallback': function(){document.location = url;}
		});
	} else {
		// if not, follow link ourselves
		document.location = url;
	}
}
```

- [Track outbound links - Analytics Help](https://support.google.com/analytics/answer/1136920?hl=en)

#### Tracking virtual pageviews

Ex: Ajax pages of Single Page Application (SPA)

	_gaq.push(['_trackPageview', path/*optional*/]);

	ga("set", {page: path, title: title});/*optional, if need to defined a different location and title than the current document location
	ga("send", "pageview");

- [Single Page Application Tracking  |  Analytics for Web (analytics.js)  |  Google Developers](https://developers.google.com/analytics/devguides/collection/analyticsjs/single-page-applications)

#### Tracking scripts errors

Track errors, like front end (`window.onerror`) or backend errors with https://developers.google.com/analytics/devguides/collection/analyticsjs/exceptions

	function trackJavaScriptError(event) {
		//ga("send", "event", "JavaScript Error", event.message, `${event.filename}:${event.lineno}:${event.colno}`, {nonInteraction: 1 });
		
		ga("send", "exception", {
			exDescription: `${event.message} ${event.filename}:${event.lineno}:${event.colno}`,
			exFatal: true,
			appName: APP_NAME,
			appVersion: APP_VERSION
		});
		/*
		ga("send", {
			hitType: "exception",
			page: "/current-url",
			exDescription: `${event.message} ${event.filename}:${event.lineno}:${event.colno}`,
			exFatal: true,
			appName: APP_NAME,
			appVersion: APP_VERSION
		});
		*/
	}
	
	window.addEventListener("error", trackJavaScriptError, false);

- [Website Exception Monitoring Template](https://www.google.com/analytics/web/template?uid=dPxbEfBpSOWlNBQvG_l85g)
- https://stackoverflow.com/questions/21718481/report-for-exceptions-from-google-analytics-analytics-js-exception-tracking
- https://davidwalsh.name/track-errors-google-analytics

## SEO and ASO

[Search engine optimization](https://en.wikipedia.org/wiki/Search_engine_optimization) and [App store optimization](https://en.wikipedia.org/wiki/App_store_optimization)

- [Your Guide to App Store Optimization (ASO)](https://www.sitepoint.com/your-guide-to-app-store-optimization-aso/)

Things changes over time, but [10 Things Google Wished You Knew - Search Engine People Blog | Search Engine People](http://www.searchenginepeople.com/blog/what-google-wished-you-knew.html)

See also [HTML Accessibility](../Development/HTML/HTML.md#accessibility) and [HTML Semantics](../Development/HTML/HTML.md#patterns-markup-semantics-and-snippets).

- [Search Appearance - Search Console Help](https://support.google.com/webmasters/topic/4589289)
- International, Mobile, Quality: [Follow our guidelines - Search Console Help](https://support.google.com/webmasters/topic/6001981)
- [Mobile SEO — Webmaster's Mobile Guide](https://developers.google.com/webmasters/mobile-sites/mobile-seo/index)
- [Google Trends](https://www.google.com/trends/)

- [SEO is Not Hard — A step-by-step SEO Tutorial for beginners that will get you ranked every single… – Startup Grind – Medium](https://medium.com/startup-grind/seo-is-not-hard-a-step-by-step-seo-tutorial-for-beginners-that-will-get-you-ranked-every-single-1b903b3ab6bb#.rbfo6cqji)
- Google could dislike you [Search Risk - How Google Almost Killed ProtonMail - ProtonMail Blog](https://protonmail.com/blog/search-risk-google/)

- [Google Analytics In Real Life - Landing Page Optimization - YouTube](https://www.youtube.com/watch?v=N5WurXNec7E)
- [Google Analytics In Real Life - Site Search - YouTube](https://www.youtube.com/watch?v=cbtf1oyNg-8)
- [Google Analytics In Real Life - Online Checkout - YouTube](https://www.youtube.com/watch?v=3Sk7cOqB9Dk)

"sitelinks" (pages entries list below search result item) are automatically generated (using an algorithm). See [Sitelinks - Search Console Help](https://support.google.com/webmasters/answer/47334?hl=en)

Note: 404 pages are often ignored. **Check your page HTTP status.**

> - Quality and depth of content: Quality content needs to have value to your audience.
> - Shares/links from related sites: If you have accounts on several networks and want Google to know they are all related to you, link them together. If you share, keep it relevant.
> - Popularity: Who and how many people share your content, are SEO variable.
> - Accurate keywords in content, meta tags, URL: Keywords is the title of your content. Be able to sum up your content with five searchable meta tags. Be accurate, interesting, and searchable.
> - Being the original source: The person who posted it first is considered the original source.
> - Ads-to-content ratio: There is a fine line to walk between giving an audience good content, while still making enough money to run your business.
> - Good UI and UX of website: If you have confusing navigation, links that lead to broken/missing pages, navigation that requires more clicks than necessary, then it means you’re not maintaining
> - Steady flow of produced content: Another part of good UX is not being flooded by ads on a page. Continually create. Google wants fresh content on top.
— [SEO Secrets: Reverse-Engineering Google’s Algorithm](https://medium.freecodecamp.com/seo-secrets-reverse-engineering-googles-algorithm-92fad4f5a39)

Tools, audit, checklist, etc.:

- https://github.com/marcobiedermann/search-engine-optimization Checklist
- [The 2016 SEO Checklist - ClickMinded](http://www.clickminded.com/seo-checklist/)
- [Local SEO Checklist | SEO Checklist 2016](http://localseochecklist.org/)
- [SEO Crawler | Rob Hammond](https://robhammond.co/tools/seo-crawler)
- [On-page SEO Analysis | Rob Hammond](https://robhammond.co/tools/html-analysis)
- [Yellow Lab Tools](http://yellowlab.tools/) and https://github.com/gmetais/YellowLabTools
- [Varvy SEO tool and optimization guide](https://varvy.com/)
- [Search Console - Home](https://www.google.com/webmasters/tools/home)
- [WebPagetest - Website Performance and Optimization Test](http://www.webpagetest.org/)
- [WooRank.com | SEO Checker - Website Review](https://www.woorank.com/)
- [Search Console - Disavow links](https://www.google.com/webmasters/tools/disavow-links-main) see [Disavow backlinks - Search Console Help](https://support.google.com/webmasters/answer/2648487)
- [Web Page Analyzer Free Tool for SEO](http://www.seowebpageanalyzer.com/)
- [Structured Data Testing Tool](https://search.google.com/structured-data/testing-tool) see [Home - schema.org](http://schema.org/), [Official Google Webmaster Central Blog: An improved search box within the search results](https://webmasters.googleblog.com/2014/09/improved-sitelinks-search-box.html)
- [Bing - Analyseur SEO](http://www.bing.com/toolbox/seo-analyzer)
- [Structured Data Linter](http://linter.structured-data.org/)
- [The W3C Markup Validation Service](https://validator.w3.org/)
- [Structured Data Markup Helper](https://www.google.com/webmasters/markup-helper/u/0/)
- [Validator.nu](https://validator.nu/)
- https://github.com/saymedia/seosuite
- https://github.com/eyecatchup/SEOstats
- https://github.com/mattclements/SEO-Audit
- [#1 Free Web & Mobile Analytics Software](https://matomo.org/) - analytics service (previously Piwik)
- [Open Web Analytics](http://www.openwebanalytics.com/) - analytics service
- https://github.com/Kickball/awesome-selfhosted/blob/master/README.md#analytics
- http://seositecheckup.com
- http://majesticseo.com
- http://ahrefs.com
- http://nibbler.silktide.com
- http://feedthebot.com

### Rank factors

1. Content
	- There is a measurable correlation between the quality of content and rankings. This is demonstrated by, among others, the analysis of two new features based primarily on word co-occurrence analysis: Proof and Relevant Terms.
	- The length of content continues to increase.
	- A good internal linking structure is an important factor, and probably the most underrated SEO measure.
2. Onpage Technical SEO
	- Onpage, the keyword remains an important part of the overall concept for SEO, often represented by a balanced presence in Title, Description, Body copy, H1, H2, etc. Needless to say, that keyword stuffing should still be avoided. However, there is a definite trend towards developing keywords to topics to generate holistic content.
	- Site load speed is a veryRF Robot important performance factor.
	- Good site architecture is the beginning and end of effective SEO.
3. Backlinks
	- The quantity and especially the quality of backlinks remains important.
	- The number of keyword backlinks continues to decrease, even if the correlation increases.
	- Backlink features for Brands (Point 6 below) appear to work differently to the rest of the URLs in SERPs.
4. Social Signals
	- There were minor changes to the previous year, with Social signals correlating slightly less with good rankings than last year.
	- Average values rose slightly.
5. User Signals
	- Both the click-through rate and the time-on-site are considerably higher in better ranking sites – this may appear obvious, but average values determined over many URLs can be used as a benchmark for your own optimization.
	- The bounce rate is lower for top-ranking URLs.
6. Improved* Brand Factor
	- There seem to be special consideration for big brands.
	- The Brand Factor and its definition have been revised this year, to show the increasing complexity of its influence and quality.

1. Relevant, comprehensive content is more important than ever
	Factors associated with the quality of content on web pages are increasing in importance. Higher ranking pages tend to have more words and are better able to give searchers the information they are looking for by covering topics more comprehensively, as well as being easier to read and understand1.Since last year the average word count on pages in the top 10 search results has increased by around a quarter (rising from 975 to 1285 words), while there is evidence that high ranking pages cover topics more comprehensively touching on a variety of related topics.
2. Pay attention to user experience and user signals
	Websites which rank higher are better structured, more often responsive, have a better internal link structure and offer a user-friendly experience. “Closely relate to the content and user experience are user signals such as time on site and bounce rates because they tell Google if people find your information useful and engaging,” said Tober. “Google can measure these signals very effectively, for example by analyzing user behavior from people who use its Google Chrome web browser. So if you want your pages to rank well, you can’t get away with providing content that isn’t relevant or by providing a poor experience.”
3. Technical optimization is a basis requirement for rankings
	In addition, technical factors such as having a title tag and description in a web page’s underlying source code, and having pages that are quick to load, are standard requirements that almost all pages in the top 30 results display.
4. Decline of single keyword focus and relevance of backlinks
	The number of backlinks to a page from other pages is still a factor that is highly correlated with search ranking positions but its importance is declining.

- [Flesch–Kincaid readability tests - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Flesch%E2%80%93Kincaid_readability_tests)
- [Knowledge-Base | Searchmetrics](http://www.searchmetrics.com/knowledge-base/)
- [Searchmetrics Ranking Factors Study 2015](http://www.searchmetrics.com/knowledge-base/ranking-factors/)
- [Official Google Webmaster Central Blog: Helping users easily access content on mobile](https://webmasters.googleblog.com/2016/08/helping-users-easily-access-content-on.html)

### Data type

- [Home - schema.org](http://schema.org/)
- [Introduction to Structured Data Types  |  Search  |  Google Developers](https://developers.google.com/search/docs/data-types/data-type-selector)
- [Data types supported by Data Highlighter - Search Console Help](https://support.google.com/webmasters/topic/2774098)

### Title and meta

More useful for human than search engines.

Define a meta `og:description`, if you don't want a page content bribe as snippet (works also for Facebook share)

> Title: The first blue line of any search result is the title of the webpage. Click the title to go to the site.
> URL: In green, you'll see the web address of the web page.
> Snippet: Below the URL is text that helps show how the page relates to your query. The words you search for will show in bold to make it easier for you to decide if the page has what you're looking for.
— [Google search results page - Search Help](https://support.google.com/websearch/answer/35891?hl=en#results)

- [Create good titles and snippets in Search Results - Search Console Help](https://support.google.com/webmasters/answer/35624)
- Google Search Console > Select a property / website > Search Appearance "!" icon > "Search Appearance Overview" modal

### Sitemap

Usefull for large site, or when link discovering is hard (all links couldn't be found on each pages)

Size is limited to 50,000 URLs and 50 MB

- [Increasing the size limit of Sitemaps file to address evolving webmaster needs | Webmaster Blog](https://blogs.bing.com/webmaster/November-2016/Increasing-the-size-limit-of-Sitemaps-file-to-addr)
- [Site map — Wikipedia](https://en.wikipedia.org/wiki/Site_map)
- [Sitemaps — Wikipedia](https://en.wikipedia.org/wiki/Sitemaps)
- [Learn about sitemaps - Search Console Help](https://support.google.com/webmasters/answer/156184?hl=en)
- [sitemaps.org - Home](https://www.sitemaps.org/)

### Flash and search engines

See [JavaScript and search engines](#javascript-and-search-engines)

- [Providing alternative content for SWF files | Adobe Developer Connection](http://wayback.archive.org/web/20120911162007/http://www.adobe.com/devnet/flashplayer/articles/alternative_content.html)
- [SEO | Adobe Developer Connection](http://wayback.archive.org/web/20150505144120/http://www.adobe.com/cn/devnet/seo.html)
- [Official Google Webmaster Central Blog: Improved Flash indexing](https://webmasters.googleblog.com/2008/06/improved-flash-indexing.html)
- [SWF searchability FAQ | Adobe Developer Connection](http://wayback.archive.org/web/20120920193005/http://www.adobe.com/devnet/flashplayer/articles/swf_searchability.html)

### JavaScript and search engines

**For multiple reasons (SEO, accessibility, archive, etc.), make the content your website accessible without script.**

All crawler engines can't execute JS. Even Google Bot (one of the most advanced engine) don't always execute JS (only in rendering phase, but in crawl phase).

> Even with an improved ability to crawl JavaScript, Google will prefer pure HTML content because it takes up fewer resources.

> Googlebot uses a web rendering service (WRS) that is based on Chrome 41 (M41)
– [Rendering on Google Search | Search | Google Developers](https://developers.google.com/search/docs/guides/rendering) - 2017-08-25 (Chrome 41 was released in march 2015)

> Today, we are happy to announce that Googlebot now runs the latest Chromium rendering engine (74 at the time of this post) when rendering pages for Search. Moving forward, Googlebot will regularly update its rendering engine to ensure support for latest web platform features.
– [Official Google Webmaster Central Blog: The new evergreen Googlebot](https://webmasters.googleblog.com/2019/05/the-new-evergreen-googlebot.html)

- [Fix Search-related JavaScript problems  |  Search  |  Google Developers](https://developers.google.com/search/docs/guides/fix-search-javascript)
- [Implement dynamic rendering  |  Search  |  Google Developers](https://developers.google.com/search/docs/guides/dynamic-rendering)
- [Google Renders 98% Of Pages They Crawl But It Can Take Weeks](https://www.seroundtable.com/google-render-slow-26538.html)
- [Going Beyond Google: Are Search Engines Ready for JavaScript Crawling & Indexing? - Moz](https://moz.com/blog/search-engines-ready-for-javascript-crawling)
- [Use Fetch a Google for website - Search Console Help](https://support.google.com/webmasters/answer/6066468?hl=en) - 10 fetches per days
- [JavaScript SEO Test](http://pstenstrm.se/seo/)
- [Does Google crawl and index dynamic content?](http://www.centrical.com/test/google-json-ld-and-javascript-crawling-and-indexing-test.html)
- [Does Google execute JavaScript? | Stephan Boyer](https://www.stephanboyer.com/post/122/does-google-execute-javascript)
- [An update (March 2016) on the current state & recommendations for JavaScript in Google Search](https://plus.google.com/+JohnMueller/posts/LT4fU7kFB8W)
- [JavaScript & SEO - What You Need To Know #SMXParis](https://www.slideshare.net/Badams/javascript-seo-what-you-need-to-know-smxparis) - Crawler, Indexer and Ranker
- [Can Google Properly Crawl and Index JavaScript Frameworks? A JavaScript SEO Experiment. | Elephate](https://www.elephate.com/blog/javascript-seo-experiment/)
- [What version of Chrome is Google actually using for rendering? - DeepCrawl](https://www.deepcrawl.com/blog/news/what-version-of-chrome-is-google-actually-using-for-rendering/)

#### `<noscript>` and search engines

Some people advice to not use noscript tag, but is not. Google itself advice using it for accessibility (and progressive enhancement) purposes:

> Place the same content from the JavaScript in a `<noscript>` tag. If you use this method, ensure the contents are exactly the same as what’s contained in the JavaScript, and that this content is shown to visitors who do not have JavaScript enabled in their browser.
— [Hidden text and links - Webmaster Tools Help](https://support.google.com/webmasters/answer/66353)

But it's recommended to use this tag for render HTML without JS especially for resources lazyloading (`img`, `video` and `audio`), but try to avoid it (especially for links) by rendrer directly in document and use unobtrusive JavaScript handle/replace it.

Note: content inside noscript tag that match a specific search will not be hightlighted in Google Search results. Because it doesn't be included in the link description, aka [snippet](https://support.google.com/websearch/answer/35891?hl=en#results).

What happend, if the script execution fail?

> À moins que javascript ne soit désactivé par le navigateur, l'image n'est pas chargée naturellement et donc peut ne jamais apparaître en cas de plantage ;
— http://dascritch.net/post/2014/06/12/Finesse-en-img#methode_noscript

- [Use of <noscript> to replace image containing text - Google Product Forums](https://productforums.google.com/forum/#!topic/webmasters/YLIQcabBrjA)
- [seo - Images within noscript - Webmasters Stack Exchange](http://webmasters.stackexchange.com/questions/38398/images-within-noscript)
- [SEO & noscript - Does Google index links in a NOSCRIPT tag?](http://www.nickpower.com/google-index-links-noscript-tag/)
- https://stackoverflow.com/questions/18245019/is-content-loaded-styled-parsed-in-the-noscript-tag-even-when-javascript-is-en
- http://www.searchenginepeople.com/blog/what-google-wished-you-knew.html
- http://searchengineland.com/google-io-new-advances-in-the-searchability-of-javascript-and-flash-but-is-it-enough-19881

### Hidden text

See [hide graphicaly a text](CSS#hide-graphicaly-a-text)

### Nofollow

- [nofollow - Wikipedia](https://en.wikipedia.org/wiki/Nofollow)
- [What About Nofollow Links?](http://www.webpagemistakes.ca/nofollow/)
- [Use rel="nofollow" for specific link - Search Console Help](https://support.google.com/webmasters/answer/96569)

### URLs

See [URI/URL](#uriurl) and [Links and alternate](#links-and-alternate)

Don't have a real impact: [15 SEO Best Practices for Structuring URLs - Moz](http://moz.com/blog/15-seo-best-practices-for-structuring-urls)

#### URL Fragments

- [Frequently Asked Questions - Webmasters — Google Developers](https://developers.google.com/webmasters/ajax-crawling/docs/faq)
- [Full Specification - Webmasters — Google Developers](https://developers.google.com/webmasters/ajax-crawling/docs/specification)
- [Guide to AJAX crawling for webmasters and developers - Webmaster Tools Help](https://support.google.com/webmasters/answer/174992?hl=en)

### Crawler

- [Robots meta tag and X-Robots-Tag HTTP header specifications  |  Webmasters  |  Google Developers](https://developers.google.com/webmasters/control-crawl-index/docs/robots_meta_tag)

### `robots.txt`

```
# www.robotstxt.org/

# Allow crawling of all content
User-agent: *
Disallow:
```

Redirect `/robots.txt` to `/.well-known/robots.txt` is supported (not recommended), but with only 301 status code

- [google search console - Can Googlebot handle robots.txt with a 302 redirect? - Webmasters Stack Exchange](https://webmasters.stackexchange.com/questions/55324/can-googlebot-handle-robots-txt-with-a-302-redirect)
- [seo - Redirecting robots.txt when moving to a new domain - Webmasters Stack Exchange](https://webmasters.stackexchange.com/questions/106943/redirecting-robots-txt-when-moving-to-a-new-domain)
- [redirect - Google robots.txt for http site after redirection to https - Stack Overflow](https://stackoverflow.com/questions/47162841/google-robots-txt-for-http-site-after-redirection-to-https)
- [Test your robots.txt with the robots.txt Tester - Search Console Help](https://support.google.com/webmasters/answer/6062598?hl=en)
- [Planning on moving to HTTPS? Here are 13 FAQs! What's missing? Let me know in...](https://web.archive.org/web/20190130051831/https://plus.google.com/+JohnMueller/posts/PY1xCWbeDVC)
- [Create a robots.txt file - Search Console Help](https://support.google.com/webmasters/answer/6062596?hl=en)
- [web crawlers - Can robots.txt be in a server's sub-directory? - Webmasters Stack Exchange](https://webmasters.stackexchange.com/questions/89395/can-robots-txt-be-in-a-servers-sub-directory/125858#125858)

**Don't block web crawler for public content**:

	# Don't do it!
	User-agent: *
	Disallow: /

But:

	User-agent: *
	Crawl-delay: 3600

Or

	User-agent: *
	Disallow: /user/private_page

To exclude folder but not sub part (files or directory) (Only with non standard `Allow` directive):

	# Allow first then disallow
	User-agent: *
	Allow: /folder/archive/
	Allow: /folder/lsic/
	Disallow: /folder/

- Si une URL a déjà été indexée par Google, alors la bloquer dans le robots.txt ne changera rien : en tout cas l'URL restera indexée. En effet, Google n'ayant plus l'autorisation de crawler la page, celle-ci ne sera plus crawlée et restera dans l'index telle quelle. Pour désindexer une URL, il faut autoriser son crawl et utiliser une balise meta robots noindex ou un entête HTTP `X-Robots-Tag: noindex` (ou bien, exception, aller faire une demande de suppression d'URL dans Google Webmaster Tools).
- Ne bloquez pas le crawl des URL qui se font rediriger, sinon les moteurs ne pourront pas se rendre compte de cette redirection
- La taille maximale d'un fichier robots.txt est de 500Kb soit "seulement" 62,5Ko (ce qui dépasse sera ignoré par Google)
- le fichier robots.txt peut se retrouver lui-même indexé dans Google. Pour le désindexer, vous devez soit utiliser `X-Robots-Tag` soit interdire le crawl du fichier puis le faire supprimer de l'index dans Google Search Console.
- La directive `Crawl-delay` est gérée par Bing mais ignorée par Google (pour ce dernier, il faut configurer ce paramétrage dans Google Search Console).
- La directive `Allow` n'est pas standard, mais Google la gère
- il doit y avoir un fichier `robots.txt` pour chaque sous-domaine et pour chaque protocole (HTTP et HTTPS)
- Google accepte le fichier `robots.txt` sur le protocole FTP
- Seules 4 directives sont prises en compte par Google (la casse est ignorée pour ces directives) : `user-agent`, `disallow`, `allow`, `sitemap`

- [Robots.txt - Archiveteam](http://www.archiveteam.org/index.php?title=Robots.txt)
- [Help:Using the Wayback Machine - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Help:Using_the_Wayback_Machine#Limitations)
- [Robots.txt Specifications  |  Webmasters  |  Google Developers](https://developers.google.com/webmasters/control-crawl-index/docs/robots_txt?hl=en)
- [Robots exclusion standard - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Robots_exclusion_standard)
- [The Web Robots Pages](http://www.robotstxt.org/orig.html)
- https://en.wikipedia.org/robots.txt
- [seo - How to configure robots.txt file to block all but 2 directories - Stack Overflow](https://stackoverflow.com/questions/6460895/how-to-configure-robots-txt-file-to-block-all-but-2-directories)

### Mobile and search engines

If redirect base on User-Agent header, use:

	Vary: User-Agent

- [Separate URLs  |  Mobile Friendly Websites  |  Google Developers](https://developers.google.com/webmasters/mobile-sites/mobile-seo/separate-urls)

What about Google with websites desktop + mobile / desktop + AMP / desktop + mobile + AMP: [Comment Google indexe le mobile-first du site sans version mobile mais avec AMP ? - Arobasenet.com](http://www.arobasenet.com/2016/11/google-amp-mobile-first-3498.html)

### Print and search engines

- [Tracking Printed Pages (or How to Validate Assumptions) - Web Standards Sherpa](http://webstandardssherpa.com/reviews/tracking-printed-pages/)

## Anchor hash tag behaviour

- (prefered) use an anchor (`<span id="target"></span>`) in targeted element (don't use `a` without `href`) (via `position: absolute; top: -200px;` etc.). Position absolute can also be used, to prevent autoscroll
- (on click on link) `event.preventDefault();`, `history.pushState()` (`window.location.hash` will scroll automatically, so need to override `document.body.scrollTop` and `document.body.scrollLeft` after changing its value)
- rename target IDs. Some browser keep in memory the position of the previous ID

- `History.scrollRestoration = "manual"` https://developer.mozilla.org/en-US/docs/Web/API/History/scrollRestoration
- http://lea.verou.me/2011/05/change-url-hash-without-page-jump/
- http://css-tricks.com/hash-tag-links-padding/
- [Autoscroll to anchors](JavaScript#autoscroll-to-anchors)

## in frame blocking

	<script>
		if (self !== top) {
			document.body.style.display = "none";
			top.location = self.location;
		}
	</script>

Use header `Content-Security-Policy: frame-ancestors 'self'` (or the depreciated `X-Frame-Options: SAMEORIGIN`)

See [Clickjacking](Security#clickjacking)

## Adaptive

Aka adaptive web design, responsive, adaptative web design

Deliver the best possible experience to the widest possible audience

> Device Detection: Don't Do It!

Note: Sometimes it's better to have a dedicated version for a context. Ex: mobile version

- RWD (responsive web design) = provide an optimal viewing experience, adapts the layout to the viewing environment by using fluid, proportion-based grids, flexible images, and CSS3 media queries, an extension of the @media rule
- Progressive enhancement = Allows everyone to access the basic content and functionality of a web page, using any browser or Internet connection, while also providing an enhanced version of the page to those with more advanced browser software or greater bandwidth

Depends on features detections and usage:

- output (interactive screen, print, projection)
- screen capabilities (screensize, dpi)
- network capabilities (latency, upload and download bandwidth)
- touch capability
- supported formats (video, audio, etc.)
- number of users (usually one)

- [Media - App Center | MDN](https://developer.mozilla.org/en-US/Apps/Progressive/Responsive/Media_types)
- [Responsive Web Design](https://github.com/north/north#responsive-web-design)
- [Adaptive vs Responsive, What’s The Difference? | Viljami Salminen](https://viljamis.com/2012/adaptive-vs-responsive-design/)
- [Content adaptation — Wikipedia](https://en.wikipedia.org/wiki/Content_adaptation)
- [Responsive web design — Wikipedia](https://en.wikipedia.org/wiki/Responsive_web_design)

### Responsive images

Aka content aware image cropping and art direction

Define an interest area or predefined crop rules based on breakpoints

See also [HTML - Responsive image](HTML#responsive-image)

> _art direction_ problem involves wanting to change the image displayed to suit different image display sizes
— [Responsive images - Learn web development | MDN](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images#Art_direction)

![Art Direction](art%20direction.jpg)
![Art direction example](https://www.drupal.org/files/project-images/image-replace-art-direction.png)

- define find the focal point(s)
- [Automatically Art-Directed Responsive Images? Here You Go. – Smashing Magazine](https://www.smashingmagazine.com/2016/02/automatically-art-directed-responsive-images-go/)
- https://github.com/jwagner/smartcrop.js/ https://github.com/jwagner/smartcrop-cli - Content aware image cropping library
- [Thoughts on Responsive "Art Direction" • gskinner blog](http://blog.gskinner.com/archives/2015/05/thoughts-on-responsive-art-direction.html)
- [Learning to Compose with Professional Photographs on the Web](https://arxiv.org/pdf/1702.00503v1.pdf) - paper
- [Sensible jumps in responsive image file sizes - Cloud Four](https://cloudfour.com/thinks/sensible-jumps-in-responsive-image-file-sizes/)
- [WordPress Ideas — Better Art Direction for Image Cropping](https://wordpress.org/ideas/topic/art-direction-and-image-cropping)
- [Why cropping is bad – Ming Thein | Photographer](https://blog.mingthein.com/2013/01/21/why-cropping-is-bad/)
- [Use Cases and Requirements for Standardizing Responsive Images](https://www.w3.org/TR/respimg-usecases/)
- [An XMP schema for responsive metadata](https://github.com/universalimages/rmd) - a W3C Community work

	-[Universal Images Community Group](https://www.w3.org/community/universalimages/)
	- https://github.com/sbaechler/thumbor-rmd-demo
	- https://github.com/sbaechler/thumbor-universalimages

Service generate art directed images:

- [Cloudinary - Cloud image service, upload, storage & CDN](http://cloudinary.com/)
- [Imagefly - Responsive images on-demand](http://imagefly.io/)
- [imgix • Real-time image processing and image CDN](https://www.imgix.com/)

### Progressive Enhancement

Aka feature detection

See offline-first approach, [Progressive Enhancement (CSS)](CSS#progressive-enhancement)

- [Progressive enhancement — Wikipedia](https://en.wikipedia.org/wiki/Progressive_enhancement)
- [Progressive Enhancement and Data Visualizations | CSS-Tricks](http://css-tricks.com/progressive-enhancement-data-visualizations/)
- [Progressive Enhancement is not about JavaScript availability. | Christian Heilmann](http://christianheilmann.com/2015/02/18/progressive-enhancement-is-not-about-javascript-availability/)
- [Progressive Enhancement](https://github.com/north/north#progressive-enhancement)

## Old browsers support

**Only in the case of progressive enhancement, if it's not work and no alternative is available for a major functionality, show a message about it.**

- [Browse Happy](http://browsehappy.com/)
- [Browsers - GOV.UK](https://www.gov.uk/help/browsers)
- [Outdated Browser](http://outdatedbrowser.com/en)

## Internationalization

Aka I18n

- [W3C I18n Checker](https://validator.w3.org/i18n-checker/)
- [Project Fluent](https://projectfluent.org/)

## Image sequence

Aka turn table, Object VR, 360° object, object VR

Use turntable to captures differents angles.

Similar to a video, but with the ability to play in both ways, seek, without any audio track

Methods:

1. decompose effect and recreate it with 3D models, JS, CSS, SVG... But won't look the same
2. use video with specific frames encoding.
	Use only I-Frames or B-frames (B for bidirectional frame). See [Frame types](Video#Frame types)
3. use images:
	Can use format like [APNG](PNG#APNG), [MNG](PNG), [JNG](JNG), [Animated WebP](WebP), SVG (animation), QTVR, tar archive contains images and data files.
	If multiple images use the same container, [content encoding](#content-encoding) could be used to compress more (GZip, Brotli) to reduce redonancy between images. For JPEG, use same DCT coefficients and omit it to reduce weight.
	Use codecs of [compressed texture format](Texture format), JPEG, PNG, etc.
	
	1. images diff (pixels + metadata) and draw the patched image (frames: I,P,P,P...) P images could refer to the I frame or to the previous P frame (see [how APNG works](PNG#APNG))
		Need fine control of playback
	2. bunch of images loaded into blobs and load into the DOM (IMG or Canvas or via ImageData) and drawn on canvas (frames: I,I,I,I...)

Examples, using diff method like:

- [iPhone 5 website teardown_ How Apple compresses video using JPEG, JSON, and \<canvas\>](https://docs.google.com/document/pub?id=1GWTMLjqQsQS45FWwqNG9ztQTdGF48hQYpjQHR_d1WsI) and [iPhone 5 web teardown: How Apple compresses video using JPEG, JSON, and canvas | Hacker News](https://news.ycombinator.com/item?id=4531088)
- http://www.bigbossstudio.com/packed_player/index.html
- [samiare/whitewater-mobile-video: An encoding system for playing inline videos on the mobile web.](https://github.com/samiare/whitewater-mobile-video)
- Phosphor:
	- [Phosphor - divergent media](http://www.divergentmedia.com/phosphor)
	- [divergentmedia/phosphorframework: Player framework for Phosphor encoded video content](https://github.com/divergentmedia/phosphorframework)
	- https://itunes.apple.com/us/app/phosphor/id589654268
	- http://chrisdowling.biz/demos/phosphor-filesize/
- Sublimetext:
	- [sublimehq/anim_encoder](https://github.com/sublimehq/anim_encoder)
	- [Animated GIFs the Hard Way | Hacker News](https://news.ycombinator.com/item?id=4532146)

- [Image Sequences: Let Me Count The Ways « Thomas Reynolds](http://awardwinningfjords.com/2012/03/08/image-sequences.html) - Use CSS animation or Canvas or DOM image suite

## Websites informations and tips

Logos: https://github.com/larsenwork/social.svg.min
- [Web scrapping](Web scrapping)
- [site-deaths - IndieWeb](https://indieweb.org/site-deaths)

- [anticontainer/plugins at master · downthemall/anticontainer](https://github.com/downthemall/anticontainer/tree/master/plugins)
- [jdownloader/src/jd/plugins/hoster at master · mirror/jdownloader](https://github.com/mirror/jdownloader/tree/master/src/jd/plugins/hoster) - see [jDownloadder](Applications#jdownloader)
- [tinyMediaManager](https://github.com/tinyMediaManager)

- [Bit rate - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Bit_rate#MP3)

Creative networks:

- https://cargocollective.com
- https://thedisplay.me
- https://deviantart.com
- https://behance.net

### Access

Services not available in China: [GreatFire.org - Expanding Online Freedom of Speech in China and Beyond](https://en.greatfire.org/)
Twitter, Github, Microsoft's OneDrive, Dropbox, Google Drive, Youtube, Instragram can be blocked in Turkey
LinkedIn is blocked in Russia

Social network are not the same everywhere. Ex.: in China Facebook and Twitter are banned, Chinese use WeChat and Weibo instead.

This can also impact dependencies like styles, fonts, images, video, scripts (libs, API scripts), etc.

- [The Essential Meta Tags for Social Media | CSS-Tricks](https://css-tricks.com/essential-meta-tags-social-media/)
- [File:Most popular social networking sites by country.svg — Wikipedia](https://en.wikipedia.org/wiki/File:Most_popular_social_networking_sites_by_country.svg)
- [List of virtual communities with more than 100 million active users — Wikipedia](https://en.wikipedia.org/wiki/List_of_virtual_communities_with_more_than_100_million_active_users)
- [List of social networking websites — Wikipedia](https://en.wikipedia.org/wiki/List_of_social_networking_websites)
- [Russia starts blocking LinkedIn website after court ruling | Reuters](http://www.reuters.com/article/us-russia-linkedin-idUSKBN13C0RN)
- [How Google’s CDN prevents your site from loading in China](https://edjiang.com/how-googles-cdn-prevents-your-site-from-loading-in-china-67504845cd04)
- [Dropbox, Google Drive and Microsoft OneDrive cloud services blocked in Turkey following leaks - Turkey Blocks](https://turkeyblocks.org/2016/10/08/google-drive-dropbox-blocked-in-turkey/)

### Social media dimensions

- https://docs.google.com/spreadsheets/d/1IpTYTTMJLcSXcPDtW9zSbPBHQyRdrLfKERohGIIkE_Q/edit#gid=1990145635
- [Social media image size cheat sheet and tips: 2015 edition - The American Genius](http://theamericangenius.com/social-media/social-media-image-size-cheat-sheet-tips-2015-edition/)
- [The Ridiculously Exhaustive Social Media Dimensions Blueprintjeffberezny.com](http://jeffberezny.com/2013/02/12/the-ridiculously-exhaustive-social-media-dimensions-blueprint-infographic/)
- [Raidious Support Your Owned Media Strategy by Creating Graphics - Raidious](http://www.raidious.com/support-your-owned-media-strategy-by-creating-graphics/)
- [The Complete Social Media Image Size Guide: With Awesome Design Tips [Infographic] – Design School](https://designschool.canva.com/blog/social-media-image-size/)

### Intent URLs

See also [Web Intents](http://www.webintents.org/) and [WebActivities](https://wiki.mozilla.org/WebAPI/WebActivities)

See also [`navigator.share()` API](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/share) and [`navigator.canShare()` API](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/canShare)

Some social network have a direct access to share an URL, text or to prefill a message

With `TITLE = encodeURIComponent("TITLE")` (same for `URL`, `DESCRIPTION`, `IMAGE_SRC`):

- no value: `?key1&key2`
- empty value: `?key1=&key2=`
- default method: `GET`
- default pair separator: `&`
- values must be encoded (`GET`: URL encoding)

Share activity:

+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Network				| URI															| Parameters
+=======================+===============================================================+==========================================================
| Twitter				| https://www.twitter.com/share									| - `url`: `{URL}` or `{TITLE}:{URL}`
| 						| 																| - `text`: `{TEXT}`
| 						| 																| - `via` (optional): `{TWITTER_HANDLE}`
| 						| 																| - `related` (optional): `{TWITTER_RELATED}`, ex: `twitterapi,twittermedia,twitter` or `twitterapi:For platform info,twittermedia:For great tips` (usernames list or relations plus usernames list)
| 						| 																| - `hashtags` (optional): `{TWITTER_HASHTAGS_LIST}`, ex: `hashtag1,hashtag2,hashtag3` (list separated by commas)
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Twitter				| https://twitter.com/intent/tweet								| - `text`: `{DESCRIPTION}` or `{URL} {TITLE}` (max 280 chars or ~260 if contains an URL, which will be shortened)
| 						| 																| - `url`: `{URL}`
| 						| 																| - `in_reply_to` (optional): `{TWEET_ID}`
| 						| 																| - `via` (optional): `{TWITTER_HANDLE}`
| 						| 																| - `hashtags` (optional): `{TWITTER_HASHTAGS_LIST}`, ex: `hashtag1,hashtag2,hashtag3` (list separated by commas)
| 						| 																| 
| 						| 																| - [Overview — Twitter Developers](https://developer.twitter.com/en/docs/twitter-for-websites/web-intents/overview.html#retweet-a-tweet)
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Twitter				| https://twitter.com/intent/retweet							| - `tweet_id`: `{TWEET_ID}`
| 						| 																| - `related` (optional): `{TWITTER_RELATED}`
| 						| 																| 
| 						| 																| - [Overview — Twitter Developers](https://developer.twitter.com/en/docs/twitter-for-websites/web-intents/overview.html#retweet-a-tweet)
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Twitter				| https://twitter.com/home										| - `status`: `{URL}` or `RT @author {MESSAGE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Facebook				| https://www.facebook.com/sharer/sharer.php					| - `u`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Facebook				| https://www.facebook.com/sharer.php							| - `s`: `100`
| 						| 																| - `p[url]`: `{URL}`
| 						| 																| - `p[title]` (ignored): `{TITLE}`
| 						| 																| - `p[summary]` (ignored): `{DESCRIPTION}`
| 						| 																| - `p[images][0]` (ignored): `{IMAGE_SRC}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Facebook				| https://facebook.com/dialog/share								| - `app_id`: `{FACEBOOK_APP_ID}`, ex: `249377268519431`
| 						| 																| - `display`: `popup`
| 						| 																| - `href`: `{URL}`
| 						| 																| - `quote` (optional): `{DESCRIPTION}`
| 						| 																| - `hashtag` (optional): `{HASHTAG}`, ex: `#facebook` (include the hash symbol)
| 						| 																| 
| 						| 																| - [Share Dialog - Sharing](https://developers.facebook.com/docs/sharing/reference/share-dialog)
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Facebook				| https://www.facebook.com/dialog/send							| - `app_id`: `{FACEBOOK_APP_ID}`, ex: `249377268519431`
| 						| 																| - `display`: `popup`
| 						| 																| - `link`: `{URL}`
| 						| 																| - `locale` (optional): `{LANG}`, ex: `en_US`
| 						| 																| - `redirect_uri` (optional): `{REDIRECT_URL}`
| 						| 																| - `to` (optional): `{FB_RECIPIENT_USER_ID}` (app-scoped user ID)
| 						| 																| 
| 						| 																| - [Send Dialog - Sharing](https://developers.facebook.com/docs/sharing/reference/send-dialog)
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Google+				| https://plus.google.com/share									| - `url`: `{URL}`
| 						| 																| - `hl`: `{LANG}`, ex: `en`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Google+				| https://plus.google.com/{PAGE_ID}/share						| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| 						| https://plusone.google.com/_/+1/confirm						| - `hl`: `{LANG}`, ex: `en`
| 						| 																| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Linkedin				| https://www.linkedin.com/shareArticle							| - `mini`: `true`
| 						| 																| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `summary`: `{DESCRIPTION}`
| 						| 																| - `source`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Pinterest				| https://www.pinterest.com/pin/create/button/					| - `url`: `{URL}`
| 						| 																| - `description`: `{DESCRIPTION}`
| 						| 																| - `media`: `{IMAGE_SRC}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Pinterest				| https://www.pinterest.com/pin/create/link/					| - `url`: `{URL}`
| 						| 																| - `description`: `{DESCRIPTION}`
| 						| 																| - `media`: `{IMAGE_SRC}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Pinterest				| https://www.pinterest.com/pin/find/							| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| AddThis				| https://api.addthis.com/oexchange/0.8/offer					| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Diaspora				| https://share.diasporafoundation.org/							| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Flattr				| https://flattr.com/submit/auto								| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `description`: `{DESCRIPTION}`
| 						| 																| - `user_id`: `{FLATTR_USER_ID}`
| 						| 																| - `hidden`: `0` or `1`
| 						| 																| - `category`: `text` or other?
| 						| 																| - `tags`: ?
| 						| 																| 
| 						| 																| - [HowTo: Flattr in WordPress.com](https://blog.flattr.com/2011/06/flattr-in-wordpress-com/)
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Reddit				| https://www.reddit.com/submit/								| - `url`: `{URL}`
| 						| 																| - `title` (optional): `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Hacker News			| https://news.ycombinator.com/submitlink						| - `u`: `{URL}`
| 						| 																| - `t`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Viadeo				| https://www.viadeo.com/shareit/share/							| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Tumblr				| https://www.tumblr.com/share									| - `v`: `3`
| 						| 																| - `u`: `{URL}`
| 						| 																| - `t`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Tumblr				| https://tumblr.com/widgets/share/tool							| - `canonicalUrl`: `{URL}`
| 						| 																| - `posttype` (optional): `link`
| 						| 																| - `title` (optional): `{TITLE}`
| 						| 																| - `caption` (optional): `{TITLE}`
| 						| 																| - `content` (optional): `{URL}`
| 						| 																| - `shareSource` (optional): `tumblr_share_button`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Digg					| https://digg.com/submit										| - `url`: `{URL}`
| 						| 																| - `title={TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Skype					| https://web.skype.com/share									| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Delicious				| https://delicious.com/save_url								| - `v`: `5`
| 						| 																| - `provider`: `getsocial`
| 						| 																| - `noui`: no value
| 						| 																| - `jump`: `close`
| 						| 																| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `pic`: `{IMAGE_SRC}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| StumbleUpon			| https://www.stumbleupon.com/badge/							| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Stumbleupon			| https://www.stumbleupon.com/submit							| - `url`: `{URL}`
| 						| 																| - `title` (optional): `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Odnoklassniki			| https://www.ok.ru/dk											| - `st.cmd`: `addShare`
| 						| 																| - `st.s`: `1`
| 						| 																| - `st._surl`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Buffer				| https://buffer.com/add										| - `url`: `{URL}`
| 						| 																| - `text`: `{TITLE}`
| 						| 																| - `picture`: `{IMAGE_SRC}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Yummly				| https://www.yummly.com/urb/verify								| - `url`: `{URL}`
| 						| 																| - `imageurl`: `{IMAGE_SRC}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Draugiem.lv			| https://www.draugiem.lv/say/ext/add.php						| - `title`: `{TITLE}`
| 						| 																| - `link`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Slack					| https://slack.com/oauth/authorize								| - `scope`: `incoming-webhook,chat:write:user`
| 						| 																| - `client_id`: `{SLACK_CLIENT_ID}`, ex: `11072499345.25274635444`
| 						| 																| - `redirect_uri`: `{REDIRECT_URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Evernote				| https://www.evernote.com/clip.action							| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Flipboard				| https://share.flipboard.com/bookmarklet/popout				| - `v`: `2`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Pocket				| https://getpocket.com/save									| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| VKontakte				| https://vk.com/share.php										| - `url`: `{URL}`
| 						| 																| - `title` (optional): `{TITLE}`
| 						| 																| - `description` (optional): `{DESCRIPTION}`
| 						| 																| - `image` (optional): `{IMAGE_SRC}`
| 						| 																| - `noparse` (optional): `true`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Xing					| https://www.xing-share.com/app/user							| - `op`: `share`
| 						| 																| - `url`: `{URL}`
| 						| 																| - `sc_p` (optional): `xing-share`
| 						| 																| 
| 						| 																| Note: use `;` as pairs separator
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Xing					| https://www.xing.com/app/user									| - `op`: `share`
| 						| 																| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| 
| 						| 																| Note: use `;` as pairs separator
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Xing					| https://www.xing.com/social_plugins/share						| - `h` (optional): `1`
| 						| 																| - `url`: `{URL}`
| 						| 																| 
| 						| 																| Note: use `;` as pairs separator
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Xing					| https://www.xing.com/spi/shares/new							| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| RenRen				| https://share.renren.com/share/buttonshare					| - `link`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| RenRen				| https://share.renren.com/share/buttonshare.do					| - `link`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| YoudaoNote			| https://note.youdao.com/memory/								| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `sumary`: ``
| 						| 																| - `pic`: `{IMAGE_SRC}`
| 						| 																| - `product`: ``
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Facenama				| https://facenama.com/links/									| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Cloob					| https://www.cloob.com/share/link/add							| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Telegram				| https://t.me/share/url										| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Telegram				| https://telegram.me/share/url									| - `text`: `{TEXT}`
| 						| 																| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Telegram				| https://telegram.me/share/									| - `text`: `{TITLE}`
| 						| 																| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Yahoo App				| ymsgr:sendim													| - `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Afsaran				| http://www.afsaran.ir/link/share								| - `from`: `out`
| 						| 																| - `id`: `0`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Baidu					| https://like.baidu.com/set									| - `url`: `{URL}`
| 						| 																| - `buttontype` (optional): `small`
| 						| 																| - `cb` (optional): `{JS_CALLBACK_NAME}`, ex: `bdShare.ajax._callbacks.bd4bb141b`
| 						| 																| - `index` (optional): `0`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Baidu					| https://hi.baidu.com/pub/show/share							| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Baidu					| https://s.share.baidu.com/									| - `click`: `1`
| 						| 																| - `url`: `{URL}`
| 						| 																| - `to`: `bdhome`
| 						| 																| - `type`: `text`
| 						| 																| - `pic`: `{IMAGE_SRC}`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `sign`: `on`
| 						| 																| - `l`: ?, ex: `1auq178vh1auq17a0t1auq18luh`
| 						| 																| - `linkid`: ?, ex: `iu5kdble07c`
| 						| 																| - `sloc`: ?, ex: `570.1.1.95.17.75.16.97.31.1.1404.836.1043.1440.803`
| 						| 																| - `apiType`: `0`
| 						| 																| - `buttonType`: `0`
| 						| 																| - `firstime`: ?, ex: `1476184008114`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Weibo					| https://service.weibo.com/share/share.php						| - `url`: `{URL}`
| 						| 																| - `title` (optional): `{TITLE}`
| 						| 																| - `pic` (optional): `{IMAGE_SRC}`
| 						| 																| - `appkey` (optional): `SINA_AKEY` or empty value
| 						| 																| - `ralateUid` (optional): `{SINA_USER}` or empty value, ex: `SinaWeibo`; RelatedID http://open.weibo.com/sharebutton
| 						| 																| - `language` (optional): `{LANG}`, ex: `zh_cn`
| 						| 																| - `searchPic` (optional): `false`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| QZone					| https://sns.qzone.qq.com/cgi-bin/qzshare/cgi_qzshare_onekey	| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `desc`: empty value
| 						| 																| - `summary`: empty value
| 						| 																| - `site`: empty value
| 						| 																| - `pics`: `{IMAGE_SRC}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Tencent Weibo			| https://v.t.qq.com/share/share.php							| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Qzone					| https://sns.qzone.qq.com/cgi-bin/qzshare/cgi_qzshare_onekey	| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| QQWeibo				| https://share.v.t.qq.com/index.php							| - `c`: `share`
| 						| 																| - `a`: `index`
| 						| 																| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `pic`: `{IMAGE_SRC}`
| 						| 																| - `appkey`: `QQT_APPKEY`, ex: `QQWeibo`; AppKey http://open.t.qq.com/apps/share/explain.php
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| QQEmail Me			| https://mail.qq.com/cgi-bin/qm_share							| - `t`: `qm_mailme`
| 						| 																| - `email`: `{QQ_EMAIL_ID}`, ex: `QQEmail`; Code http://open.mail.qq.com/
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| QQChat Me 			| https://wpa.qq.com/msgrd										| - `v`: `3`
| 						| 																| - `uin`: `{QQ_TALK_ID}`, ex: http://wpa.qq.com/msgrd?v=3&uin={NUM}&site=XiaoMac&menu=yes
| 						| 																| - `site`: `{URL}`
| 						| 																| - `menu`: `yes`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Threema App			| threema://compose												| - `text`: `{TEXT} {URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| WeChat				| 																| WeChat require JS API or display a QRCode to be scanned with WeChat
| 						| 																| 
| 						| 																| - http://dev.wechat.com/
| 						| 																| - http://admin.wechat.com/wiki/index.php?title=JS_SDK_DOCUMENT
| 						| 																| - https://github.com/weui/weui/wiki/%E5%BE%AE%E4%BF%A1JSAPI
| 						| 																| - https://stackoverflow.com/questions/22636071/wechat-sharing-how-to-change-re-share-description-and-thumbail
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Twitter App			| twitter://post												| - `message`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| WhatsApp App			| whatsapp://send												| - `text`: `{URL}` or `{TEXT} {URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| WhatsApp App			| https://api.whatsapp.com/send									| - `phone`: phone number (international format, without spaces, etc.)
| 						| 																| - `text`: `{TEXT}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| WhatsApp App			| https://wa.me/{PHONE}											| - [WhatsApp FAQ - Using Click to Chat](https://faq.whatsapp.com/en/android/26000030/)
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Line App				| line://msg/text/{URL}											| 
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Mail					| mailto:														| - `to`: `{RECIPIENT_EMAIL}`
| 						|																| - `subject`: `{TITLE}`
| 						|																| - `body`: `{URL}` or `{DESCRIPTION}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------



Others activities:

|---------------------------|---------------------------------------------------------------|----------------------------------------------------------
| Activity					| URI															| Parameters
|---------------------------|---------------------------------------------------------------|----------------------------------------------------------
| Print						| javascript:window.print()										| 
|---------------------------|---------------------------------------------------------------|----------------------------------------------------------
| Add to Google Calendar	| https://www.google.com/calendar/event							| - `text`: `{TITLE}`
| 							| https://calendar.google.com/calendar/r/eventedit				| - `action` (optional): `TEMPLATE`
| 							|																| - `pprop` (optional): `HowCreated:QUICKADD`
| 							|																| - `sprop` (optional): ex: `website:www.justgiving.com`
| 							|																| - `sprop` (optional): ex: `name:Justgiving`
| 							|																| - `sf` (optional): `true`
| 							|																| - `dates`: `{START_DATE}/{END_DATE}` (format for each dates: `YYYYMMDD` or `YYYYMMDDTHHmmSS`)
| 							|																| - `details`: `{DESCRIPTION}` (multilines)
| 							|																| - `location`: `{LOCATION}` (could be an address, only one line, parts separated by comma `,`)
| 							|																| - `output` (optional): `xml`
| 							| 																| 
| 							| 																| - [Add a Google calendar to your website - Calendar Help](https://support.google.com/calendar/answer/41207?hl=en&visit_id=1-636677701437823955-3736175218&rd=2)
|---------------------------|---------------------------------------------------------------|------------------------------------------------------------------------------------------------
| Add to Yahoo Calendar		| https://calendar.yahoo.com/									| - `text`: `{TITLE}`
| 							|																| - `v`: `60`
| 							|																| - `DUR` (optional): `{DURATION}` (format `HHmm`) For all-day event, dont use this field
| 							|																| - `TITLE`: `{TITLE}`
| 							|																| - `ST`: `{START_DATE}` (format: YYYYMMDD for all-day event or YYYYMMDDTHHmmSS)
| 							|																| - `in_loc`: `{LOCATION}`
| 							|																| - `DESC`: `{DESCRIPTION}`
| 							|																| - `URL`: `{URL}` page to link back to from the calendar
| 							|																| - `REND`: `{END_DATE}` format: total seconds since 1/1/1970 12:00:00 AM
| 							|																| - `RPAT`: `{REPEAT_DELAY}` format:
| 							|																| 	- Day: `01Dy`
| 							|																| 	- Week: `01Wk`
| 							|																| 	- Month: `01Mh`
| 							|																| 	- Year: `01Yr`
| 							|																| 	- Mon Wedn Fri: `01MoWeFr`
| 							|																| 	- Tues Thurs: `01TuTh`
| 							|																| 	- Mon - Fri: `01MoTuWeThFr`
| 							|																| 	- Sat - Sun: `01SuSa`
|---------------------------|---------------------------------------------------------------|----------------------------------------------------------
| Add to Windows Live		| https://calendar.live.com/calendar/calendar.aspx				| - `rru`: `addevent`
| 							|																| - `summary`: `{TITLE}`
| 							|																| - `location`: `{LOCATION}`
| 							|																| - `dtstart`: `{START_DATE}` (format: `YYYYMMDDTHHmmSS` or `YYYYMMDD` for all-day event)
| 							|																| - `dtend`: `{END_DATE}` (format: same as `dtstart`)
| 							|																| - `description`: `{DESCRIPTION}`
|---------------------------|---------------------------------------------------------------|----------------------------------------------------------
| QRCode (WeChat, etc.)		| https://chart.googleapis.com/chart							| - `chs`: `{WIDTH}x{HEIGHT}`, ex: `400×400`
| 							| 																| - `cht`: `qr`
| 							| 																| - `chld`: `{QRCODE_ECL}|{MARGIN}`, ex: `L|5`
| 							| 																| - `chl`: `{URL}`
| 							| 																| 
| 							| 																| - [QR Codes  |  Infographics  |  Google Developers](https://developers.google.com/chart/infographics/docs/qr_codes)
|---------------------------|---------------------------------------------------------------|----------------------------------------------------------
| iCalendar file			| data:text/calendar,											| URL encoded content of iCalendar
| 							| 																| 
| 							| 																| [iCalendar - Wikipedia](https://en.wikipedia.org/wiki/ICalendar)
|---------------------------|---------------------------------------------------------------|----------------------------------------------------------

More networks and informations:

- https://github.com/bradvin/social-share-urls
- https://github.com/cferdinandi/social-sharing#2-add-the-markup-to-your-html
- [The Simplest (and Most Performant) Way to Offer Sharing Links for Social Media | CSS-Tricks](https://css-tricks.com/simple-social-sharing-links/)
- [url - Renren, Weibo, and Baidu Like buttons using only HTML (No Javascript) - Stack Overflow](https://stackoverflow.com/questions/10490443/renren-weibo-and-baidu-like-buttons-using-only-html-no-javascript)
- [How To Add Chinese Social Media Sharing Links in WordPress Jetpack Sharing | Duncan's Blog](https://blog.duncanworthy.me/misc/how-to-add-chinese-social-media-sharing-links-on-wordpress/)
- [How do I setup custom sharing? – Ideas and Knowledge Base for Netvibes](http://faq.netvibes.com/knowledgebase/articles/370909-how-do-i-setup-custom-sharing)
- https://wordpress.org/plugins/open-social/developers/

Plugins and libs:

- https://wordpress.org/plugins/2-click-socialmedia-buttons/

#### Interactions count

- [BuzzSumo - Chrome Web Store](https://chrome.google.com/webstore/detail/buzzsumo/gedpbnanjmblcmlfhgfficjnglidndfo)
- [Get number of shares from social platforms](https://gist.github.com/ihorvorotnov/9132596)
- [Get the share counts from various APIs](https://gist.github.com/jonathanmoore/2640302)

#### Open Intent URL

Use `target="_blank"` (adviced) and `rel="nofollow"` (required).

```js
// Note: chrome doesn't support "noopener", that break other features
const width = 600;
const height = 600;
const left = (window.screen.width - width) / 2 - 10;
const top = (window.screen.height - height) / 2 - 50;

// top and left not work when the opener window is at secondary screen.
const intentWindow = window.open("about:blank", "Share on Twitter", `resizable,scrollbars,noopener,status,width=${width},height=${height},left=${left},top=${top}`);

// Or:
//const intentWindow = window.open("about:blank", "Share on Twitter", `resizable,scrollbars,noopener,status`);
//intentWindow.resizeBy(width - shareWindow.innerHeight, height - shareWindow.innerWidth);// resize to match requested size for the content (innerWidth and innerHeight)
//intentWindow.moveTo(top, left);// don't support toolbars, scrollbars, and other UI element size. But let the browser to choose where the popup should be

// Clear opener (for security purpose)
intentWindow.document.write(`<script>window.opener=null;location.replace("${url}");setTimeout(function(){window.close();}, 2000)</script>`);// on iOS, when an Universal Link is registered by an app (ex: Twitter catch all URLs https://www.twitter.com/*), it could handle the URL, leaving the about:blank page opened. Else wait few second let the time to the next page to load and discard the setTimeout.
// doc.write is a navigation and require doc.close()
// data URI can't be used here because of IE. You can use blob URI, but it's not pratical because we need to revoke the object URL once the popup is loaded
```

Note: if the intent document load start can't be made direclty after the user interaction (set the final `window.open` href in click listener), open a blank document the intent window first, and later (after a asynchronous task, update the content of popup) set the final URL

- Facebook: 600×300 or 555×320
- Twitter: 550×420 or 500×310
- LinkedIn: 
	- login: content: 974×622, window.open(): 974×688 (Chrome macOS)
	- share: content: 550×475 (content call automatically `window.resizeBy(offsetX, offsetY)`)

- [Tabnabbing: Link and `target="_blank"` or `window.open()`](Security#tabnabbing-link-and-target_blank-or-windowopen)
- [Overview — Twitter Developers](https://developer.twitter.com/en/docs/twitter-for-websites/web-intents/overview)
- [Window.open() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/open)
- [javascript - Use window.open but block use of window.opener - Stack Overflow](https://stackoverflow.com/questions/40593632/use-window-open-but-block-use-of-window-opener)

### Share buttons

Is it really usefull?

> ils ne sont utilisé que moins d’une fois sur 5
– [De l'intérêt des boutons de partage - MediasSociaux.fr](http://www.mediassociaux.fr/2012/11/15/de-linteret-des-boutons-de-partage/)

- [Social media unbuttoned | Roxane](http://www.roxane-company.com/blog/2012/11/27/social-media-unbuttoned/)
- [How important are all those ugly Tweet Buttons to news sites? » Nieman Journalism Lab](http://www.niemanlab.org/2012/05/how-important-are-all-those-ugly-tweet-buttons-to-news-sites/)
- [Social Media Sharing Buttons. No JavaScript. No tracking. Super fast and easy.](http://sharingbuttons.io/)

### Map engine API

- [Category:Internet censorship by country — Wikipedia](https://en.wikipedia.org/wiki/Category:Internet_censorship_by_country)
- [All disruptions – Traffic – Google Transparency Report](https://www.google.com/transparencyreport/traffic/disruptions/#group=REGION)

HTTPS not supported by Google Apps for Crimea, Cuba, Iran, North Korea, Sudan, and Syria. That means accounts not working.

- [Countries or regions with restricted access - Google Apps Administrator Help](https://support.google.com/a/answer/2891389?hl=en)

Borders and labels are differents based where your request maps. Examples: Arunachal Pradesh and Kashmir (google.cn/maps, google.co.in/maps, google.com/maps)

- [Category:Territorial disputes by country — Wikipedia](https://en.wikipedia.org/wiki/Category:Territorial_disputes_by_country)
- [List of territorial disputes — Wikipedia](https://en.wikipedia.org/wiki/List_of_territorial_disputes)
- [Google Maps in China — Wikipedia](https://en.wikipedia.org/wiki/Google_Maps#Google_Maps_in_China)

In China?

- https://maps.googleapis.com with http://maps.google.cn
- [百度地图API-首页](http://lbsyun.baidu.com/) http://developer.baidu.com/map/jsdemo.htm#a5_1
	http://lbsyun.baidu.com/index.php?title=webapi/guide/webservice-geocoding
	http://lbsyun.baidu.com/index.php?title=jspopular
- [搜狗地图API - Sogou Maps JavaScript API](http://map.sogou.com/api/documentation/javascript/api2.5/basics.html)
- 	`http://api.map.baidu.com/staticimage?center=`${location.getLongitude()},${location.getLatitude()}&width=${width}&height=${height}&zoom=15&markers=${location.getLongitude()},${location.getLatitude()}`;
		http://api.map.baidu.com/staticimage?center=121,31&width=300&height=300&zoom=15

- [android - Using Google Maps and Baidu Maps in same app - Stack Overflow](https://stackoverflow.com/questions/18910361/using-google-maps-and-baidu-maps-in-same-app/29468356#29468356)

- [Websites blocked in mainland China — Wikipedia](https://en.wikipedia.org/wiki/Websites_blocked_in_mainland_China)

### Google Search Console

- [Malicious Google Search Console Verifications](https://blog.sucuri.net/2015/09/malicious-google-search-console-verifications.html)

### URL shorteners

- http://bit.ly/
- http://goo.gl/
- http://t.co/
- http://ow.ly/
- http://adf.ly/
- http://tinyurl.com/
- http://wp.me/

- http://amzn.to/
- http://youtu.be/

- http://bit.do/
- http://lnkd.in/
- http://db.tt/
- http://qr.ae/
- http://cur.lv/
- http://ht.ly/
- http://ity.im/
- http://q.gs/
- http://is.gd/
- http://po.st/
- http://bc.vc/
- http://u.to/
- http://j.mp/
- http://buzurl.com/
- http://cutt.us/
- http://u.bb/
- http://x.co/
- http://scrnch.me/
- http://vzturl.com/
- http://qr.net/
- http://1url.com/
- http://tweez.me/
- http://v.gd/
- http://tr.im/
- http://trib.al/
- http://zip.net/
- http://➡.ws/
- http://✩.ws/
- http://0.mk/
- http://888.hn/
- http://b54.in/
- http://bit.ly/
- http://budurl.com/
- http://doiop.com/
- http://korta.nu/
- http://lxcurl.com/
- http://s.coop/
- http://snipurl.com/
- http://tiny.cc/
- http://tinyurl.com/
- http://gg.gg/
- http://urlcut.org/
- http://qr.net/
- http://7.ly/
- http://clicky.me/
- http://bigly.us/
- http://minu.me/
- http://tinyarro.ws/
- http://urlrace.com/
- http://qoiob.com/
- http://sh.st/

Branded bitly

- [http://lemde.fr/](https://bitly.com/pages/landing/branded-short-domains-powered-by-bitly?bsd=lemde.fr)

- [List of URL Shorteners](http://bit.do/list-of-url-shorteners.php)
- [Sites about Url shortener](http://dig.do/about/url-shortener)
- [URL shortening — Wikipedia](https://en.wikipedia.org/wiki/URL_shortening)
- [List of URL Shorteners](http://l-lists.com/en/lists/gvaoif.html)
- [URL Toolbox: 90+ URL Shortening Services](http://mashable.com/2008/01/08/url-shortening-services/#XL2l1FTKhPq4)
- https://gist.github.com/MrSherlockHolmes/b3fc2b21b94040921c69
- https://www.techmaish.com/list-of-230-free-url-shorteners-services/

Unshorten:

- `https://unshorten.me/s/%s`
- `http://www.linkexpander.com/?url=%s`
 
	function unshorten_url($url) {
		// Don't use this in production: need to limit API access, need a resolved URL cache, have security issues (SSRF), etc.
		// Filter in Location localhost domains. See http://php.net/manual/en/function.curl-setopt.php#116223
		$ch = curl_init($url);
		curl_setopt_array($ch, array(
			
			CURLOPT_RETURNTRANSFER => true,     // don't output response
			CURLOPT_HEADER         => false,    // do not return headers
			CURLOPT_FOLLOWLOCATION => true,     // follow redirects. Note: CURLOPT_FOLLOWLOCATION cannot be activated when safe_mode is enabled or an open_basedir is set in. See http://php.net/manual/en/function.curl-setopt.php#113682
			CURLOPT_USERAGENT      => $_SERVER['HTTP_USER_AGENT'],
			CURLOPT_AUTOREFERER    => true,     // set referer on redirect
			CURLOPT_CONNECTTIMEOUT => 120,      // timeout on connect
			CURLOPT_TIMEOUT        => 120,      // timeout on response
			CURLOPT_MAXREDIRS      => 10,       // stop after 10 redirects
			CURLOPT_PROTOCOLS      =>  CURLPROTO_HTTP || CURLPROTO_HTTPS // limit to HTTP and HTTPS protocols
		));
		curl_exec($ch);
		$url = curl_getinfo($ch, CURLINFO_EFFECTIVE_URL);
		curl_close($ch);
		return $url;
	}

### Youtube

Link at time: `http://www.youtube.com/watch?v=cOde0332432&t=1m5s`

Embed with start time and stop (in seconds) `https://www.youtube.com/embed/7qkmGjWtG0w?start=840&end=1240&aut‌​oplay=1` or `https://www.youtube.com/v/7qkmGjWtG0w?start=840&end=1240&aut‌​oplay=1`
See [YouTube Embedded Players and Player Parameters  |  YouTube IFrame Player API  |  Google Developers](https://developers.google.com/youtube/player_parameters?#end) or [How to share a YouTube video with a specific start and end time? - Web Applications Stack Exchange](https://webapps.stackexchange.com/questions/61397/how-to-share-a-youtube-video-with-a-specific-start-and-end-time/61398)
But it's looklike the end parameter doesn't works (2018)

#### Youtube video view count

Require an API key

`https://www.googleapis.com/youtube/v3/videos?id=$1&key=$2&part=statistics`, `$2=API_KEY` `json.videos[0].statistics.viewCount` (see also `.likeCount`)

- [YouTube Data API Overview  |  YouTube Data API  |  Google Developers](https://developers.google.com/youtube/v3/getting-started)


#### API

Require embed src with param `enablejsapi=1`

Add it in with wordpress:

	/* add post message api mode for youtube embeds */
	add_filter('oembed_result' , function($html){
		return preg_replace_callback( '/(?<=")(https?:\/\/www.youtube.com\/embed\/[^"]+)/', function($matches){return add_query_arg('enablejsapi', '1', $matches[1]);}, $html);
	});

- [YouTube Player API Reference for iframe Embeds  |  YouTube IFrame Player API  |  Google Developers](https://developers.google.com/youtube/iframe_api_reference?hl=en)
- [YouTube Embedded Players and Player Parameters  |  YouTube IFrame Player API  |  Google Developers](https://developers.google.com/youtube/player_parameters?hl=en#Parameters)
- [javascript - YouTube iframe API: how do I control a iframe player that's already in the HTML? - Stack Overflow](https://stackoverflow.com/questions/7443578/youtube-iframe-api-how-do-i-control-a-iframe-player-thats-already-in-the-html)

##### Stop video

	iframe.contentWindow.postMessage("{"\"event/":\"command\",\"func\":\"stopVideo\",\"args\":\"\"}", "*");

##### Listen events

`event.data` is a serialized JSON object

	window.addEventListener("message", function(event){JSON.parse(event.data).event});
	iframe.contentWindow.postMessage("{\"event\":\"listening\"}", "*");

#### Watch video in full HD

	http://www.youtube.com/watch_popup?v=VIDEO_ID&vq=hd1080

#### Video formats

- taille standard : 320×180@330Kbps en H263 (Sorenson)
- taille "HD" : 480×270@570Kbps en H263

### Dailymotion

#### API

Require embed src with param `api=postMessage`.

Add it in with wordpress:

	/* add post message api mode for dailymotion embeds */
	add_filter('oembed_result' , function($html){
		return preg_replace_callback( '/(?<=")(https?:\/\/www.dailymotion.com\/embed\/[^"]+)/', function($matches){return add_query_arg('api', 'postMessage', $matches[1]);}, $html);
	});

- [Video Player Documentation - Dailymotion Developer Area](https://developer.dailymotion.com/player)

##### Pause video

	iframe.contentWindow.postMessage("{\"command\":\"pause\",\"parameters\":[]}", "*");

Previously?:

	iframe.contentWindow.postMessage("pause", "*");

- [javascript - Dailymotion stop video from iframe - Stack Overflow](https://stackoverflow.com/questions/26174793/dailymotion-stop-video-from-iframe)

##### Listen events

`event.data` is a query string

	window.addEventListener("message", function(event){new URLSearchParams(event.data).get("event")});

### Google Maps

- `https://www.google.com/maps/@${LAT},${LNG},${ZOOM}z`
- `https://maps.google.com/maps?daddr=${LAT},${LNG}&saddr=${?}` `saddr` is optional: start point, `daddr` is optional: destination point (add `+to:` for steps "via")
- `https://www.google.com/maps/dir/${START_POINT}/${DEST_POINT}` (`START_POINT` is optional, can be blank, `START_POINT` can be `current+location`). For steps "via" (multidestination / waypoints) add `/${POINT}` between start and dest. Encode space with `+` (`%20` is also supported). For multiline/multipart addresses (ex: street name, city, zipcode, country), replace line break with `,`
- `https://www.google.com/maps/place/?q=place_id:${PLACE_ID}` `PLACE_ID` start with `ChIJ...`
- `https://www.google.com/maps/place/${PLACE_NAME}/@${LAT},${LNG},${ZOOM}z/`

Bracket syntax (add a label for start or dest) doesn't work any more.

- [javascript - Google Maps Directions API Equivalent URL - Stack Overflow](https://stackoverflow.com/questions/16326143/google-maps-directions-api-equivalent-url/24065211#24065211)
- [Everything You Never Wanted to Know About Google Maps' Parameters - YouMoz - Moz](https://moz.com/ugc/everything-you-never-wanted-to-know-about-google-maps-parameters)
- [Google maps query parameter clarification - Stack Overflow](https://stackoverflow.com/questions/11354211/google-maps-query-parameter-clarification/11354743#11354743)
- [android - Can I add titles to locations for the directions url for maps.google.com? - Stack Overflow](https://stackoverflow.com/questions/12716152/can-i-add-titles-to-locations-for-the-directions-url-for-maps-google-com/12716995#12716995)
- [Google Maps URL Scheme | Google Maps SDK for iOS | Google Developers](https://developers.google.com/maps/documentation/ios-sdk/urlscheme)
- [Google Map Parameters - Google Mapki](http://web.archive.org/web/20110903160743/http://mapki.com/wiki/Google_Map_Parameters)

#### Google Maps My Maps

Use it as data source and editor (can output KML)

Import Google Drive Sheet in My Map : New Layer > Import > Google Drive. Must contains at least columns: Title, Latitude, Longitude

Original Google Drive Share Url: `https://drive.google.com/file/d/{KML_FILE_ID}`
Hosted KML file to use in your application: `https://googledrive.com/host/{KML_FILE_ID}`

- [Visualize your data on a custom map using Google My Maps – Google Earth Outreach](https://www.google.com/earth/outreach/learn/visualize-your-data-on-a-custom-map-using-google-my-maps/)
- [Mapping from a Google Spreadsheet – Google Earth Outreach](https://www.google.com/earth/outreach/learn/mapping-from-a-google-spreadsheet/)

#### Google Maps styles

Only for embeded maps

- [Snazzy Maps - Free Styles for Google Maps](https://snazzymaps.com/) `window.map.setMapTypeId(google.maps.MapTypeId.HYBRID)` or `window.editor.map.setMapTypeId(google.maps.MapTypeId.HYBRID)` for https://snazzymaps.com/editor/customize/XXXXX
- [Styling Wizard: Google Maps APIs](https://mapstyle.withgoogle.com/)
- [Start Styling your Map | Google Maps JavaScript API | Google Developers](https://developers.google.com/maps/documentation/javascript/styling)
 
	[
		{
			"elementType": "labels",
			"stylers": [
				{
					"visibility": "off"
				}
			]
		},
		{
			"featureType": "administrative.land_parcel",
			"stylers": [
				{
					"visibility": "off"
				}
			]
		},
		{
			"featureType": "administrative.neighborhood",
			"stylers": [
				{
					"visibility": "off"
				}
			]
		}
	]

#### API

	<!DOCTYPE html>
	<html>
		<head>
			<title>PlaceID finder</title>
			<meta name="viewport" content="initial-scale=1.0, user-scalable=no">
			<meta charset="utf-8">
			<style>
				html, body {
					height: 100%;
					margin: 0;
					padding: 0;
				}
				#map {
					height: 100%;
				}
				.controls {
					background-color: #fff;
					border-radius: 2px;
					border: 1px solid transparent;
					box-shadow: 0 2px 6px rgba(0, 0, 0, 0.3);
					box-sizing: border-box;
					font-family: Roboto;
					font-size: 15px;
					font-weight: 300;
					height: 29px;
					margin-left: 17px;
					margin-top: 10px;
					outline: none;
					padding: 0 11px 0 13px;
					text-overflow: ellipsis;
					width: 400px;
				}
	
				.controls:focus {
					border-color: #4d90fe;
				}
	
			</style>
		</head>
		<body>
			<input id="pac-input" class="controls" type="text"
					placeholder="Enter a location">
			<div id="map"></div>
	
			<script>
	// This sample uses the Place Autocomplete widget to allow the user to search
	// for and select a place. The sample then displays an info window containing
	// the place ID and other information about the place that the user has
	// selected.
	
	function initMap() {
		var map = new google.maps.Map(document.getElementById('map'), {
			center: {lat: -33.8688, lng: 151.2195},
			zoom: 13
		});
	
		var input = document.getElementById('pac-input');
	
		var autocomplete = new google.maps.places.Autocomplete(input);
		autocomplete.bindTo('bounds', map);
	
		map.controls[google.maps.ControlPosition.TOP_LEFT].push(input);
	
		var infowindow = new google.maps.InfoWindow();
		var marker = new google.maps.Marker({
			map: map
		});
		marker.addListener('click', function() {
			infowindow.open(map, marker);
		});
	
		autocomplete.addListener('place_changed', function() {
			infowindow.close();
			var place = autocomplete.getPlace();
			if (!place.geometry) {
				return;
			}
	
			if (place.geometry.viewport) {
				map.fitBounds(place.geometry.viewport);
			} else {
				map.setCenter(place.geometry.location);
				map.setZoom(17);
			}
	
			// Set the position of the marker using the place ID and location.
			marker.setPlace({
				placeId: place.place_id,
				location: place.geometry.location
			});
			marker.setVisible(true);
	
			infowindow.setContent('<div><strong>' + place.name + '</strong><br>' +
					'Place ID: ' + place.place_id + '<br>' +
					'Place loc: ' + place.geometry.location.lat() + "," + place.geometry.location.lng() + '<br>' +
					place.formatted_address);
			infowindow.open(map, marker);
		});
		
		// Get the placeID of point of interest ("poi", always visible on the map)
		var placesService = new google.maps.places.PlacesService(map);
		map.addListener('click', function(event){
			if (event.placeId) {
				// Calling e.stop() on the event prevents the default info window from
				// showing.
				// If you call stop here when there is no placeId you will prevent some
				// other map click event handlers from receiving the event.
				event.stop();
				
				placesService.getDetails({placeId: event.placeId}, function(place, status) {
					if (status === 'OK') {
						infowindow.close();
						infowindow.setPosition(place.geometry.location);
						// place.icon;
						infowindow.setContent('<div><strong>' + place.name + '</strong><br>' +
								'Place ID: ' + place.place_id + '<br>' +
								'Place loc: ' + place.geometry.location.lat() + "," + place.geometry.location.lng() + '<br>' +
								place.formatted_address);
						infowindow.open(map);
					}
				});
			}
			
		});
	}
	
			</script>
			<script src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY&libraries=places&callback=initMap" async defer></script>
		</body>
	</html>

- `https://maps.googleapis.com/maps/api/place/details/json?key=YOURAPIKEY&placeid=THEPLACEID` -> `json["result"]["url"]` `PLACE_ID` start with `ChIJ...`
- [google maps - How do I remove default markers? - Stack Overflow](https://stackoverflow.com/questions/7538444/how-do-i-remove-default-markers) - How to remove Points of Interest (colored marker for commercial places, monuments, etc.), use [style feature type `poi`](https://developers.google.com/maps/documentation/javascript/style-reference)
- [API Manager](https://console.developers.google.com/apis/api/maps_backend/overview)
- [PlaceID Finder | Google Maps JavaScript API | Google Developers](https://developers.google.com/maps/documentation/javascript/examples/places-placeid-finder)
- [POI Click Event | Google Maps JavaScript API | Google Developers](https://developers.google.com/maps/documentation/javascript/examples/event-poi)

Center to all markers

	var markers = [];//some array
	var bounds = new google.maps.LatLngBounds();
	for (var i = 0; i < markers.length; i++) {
	 bounds.extend(markers[i].place.location);
	}
	
	map.fitBounds(bounds);

- [javascript - Center/Set Zoom of Map to cover all visible Markers? - Stack Overflow](https://stackoverflow.com/questions/19304574/center-set-zoom-of-map-to-cover-all-visible-markers)

#### Icons

	https://mt.google.com/vt/icon/... = https://mt0.google.com/vt/icon/... = https://mt.google.com/vt/icon?... = https://www.google.com/maps/vt/icon/....

`https://www.google.com/maps/vt/icon/name=...&scale=...` or `https://www.google.com/maps/vt/icon?...=...&...=...` or `https://www.google.com/maps/vt/icon/...=...&...=...?...=...&...=...`

- `name=...` path (1,n) required. List of graphic resources to use. The last element is the first in front
- `highlight=...` color (1,n). Replace a color (ex. `assets/icons/poi/quantum/container_shadow-1-small.png`: none, `assets/icons/poi/quantum/container-1-small.png`: 0×00FF00, icon: 0xFF00FF) by the given color
- `scale=...` number 1 (default), 2 (retina, 2x), 3, 4. Scale of the result image
- `text=...` string. Text
- `psize=...` text size
- `font=...` font path eq. `fonts/Roboto-Bold.ttf`
- `color=...` color. text color
- `ax=...` number. Text x position
- `ay=...` number. Text y position

- `color`: hexadecimal: 0, ARGB, RRGGBB or AARRGGBB
- quantity `1, n`: could be 1 value or multiple values separated by `,`
- `...-3-large`, `...-2-medium`, `...-1-small`, `...-0-tiny`. All sizes are not supported by each icons. All support at least medium and small sizes. Width and height are related to size, resolution and icon

List of available resources (protocol buffer encoded data): https://www.gstatic.com/maps/res/CompactLegend-Roadmap-cbc3edfa467314789e34bc25eaddcfe2 (to get the last version, `view-source:https://www.google.com/maps/search/` and search `gstatic.com/maps/res/CompactLegend`)

	9 {
	  1: "bank_dollar-1-small"// name without full path and extension .png
	  2: 4//
	  5: 0// type/collection 0 poi assets/icons/poi/quantum/*, 9 assets/icons/poi/quantum/container*, 12 London related, 17 Sydney related see "transit/localizations/.../..."
	  6: 0×00ffffff// color. See highlight
	}

0×6d7be3, 0×8d6e63, 0xf57f17

- `name=icons/spotlight/restaurant_search_L_8x.png&scale=1`
- `name=icons/spotlight/lodging_search_L_8x.png&scale=1`
- `name=icons/spotlight/star_L_8x.png&scale=1`
- `name=icons/spotlight/generic_search_L_8x.png&scale=1`
- `name=icons/spotlight/spotlight-poi.png&scale=2`
- `name=assets/icons/poi/tactile/measle-2-medium.png&color=ff000000?scale=1`
- `name=assets/icons/road/transparent-2-medium.png&color=ff000000?scale=1`
- `name=assets/icons/spotlight/spotlight_poi-1-small.png&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container-19px-2-medium.png,assets/icons/poi/quantum/container-19px-2-medium.png,assets/icons/poi/quantum/branded/...`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/restaurant-1-small.png&highlight=ff000000,f57f17,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/generic-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/lodging-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/cemetery-1-small.png&highlight=ff000000,ffffff,7cb342&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/generic-1-small.png&highlight=ff000000,ffffff,8d6e63&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/golf-1-small.png&highlight=ff000000,ffffff,7cb342&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/historic-1-small.png&highlight=ff000000,ffffff,8d6e63&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/hospital_H-1-small.png&highlight=ff000000,ffffff,db4437&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/museum-1-small.png&highlight=ff000000,ffffff,8d6e63&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/note-1-small.png&highlight=ff000000,ffffff,8d6e63&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/paw-1-small.png&highlight=ff000000,ffffff,8d6e63&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/school-1-small.png&highlight=ff000000,ffffff,8d6e63&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/shoppingbag-1-small.png&highlight=ff000000,ffffff,6b79c5&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/stadium-1-small.png&highlight=ff000000,ffffff,8d6e63&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/worship_temple-1-small.png&highlight=ff000000,ffffff,8d6e63&color=ff000000?scale=1`
- `name=assets/icons/transit/localizations/ru/moscow-metro_ring-0-tiny.png,assets/icons/transit/localizations/ru/moscow-metro_circle-0-tiny.png,assets/icons/transit/localizations/ru/moscow-metro_m-0-tiny.png&highlight=143c9a,ffffff,e6362e&color=ff000000?scale=1`
- `name=assets/icons/transit/localizations/ru/moscow-metro_ring-1-small.png,assets/icons/transit/localizations/ru/moscow-metro_circle-1-small.png,assets/icons/transit/localizations/ru/moscow-metro_m-1-small.png&highlight=143c9a,ffffff,e6362e&color=ff000000?scale=1`
- `name=assets/icons/transit/quantum/container_shadow-0-tiny.png,assets/icons/transit/quantum/container-0-tiny.png,assets/icons/transit/quantum/train-0-tiny.png&highlight=0,b0ff,ffffff&color=ff000000?scale=1`
- `name=assets/icons/transit/quantum/container_shadow-1-small.png,assets/icons/transit/quantum/container-1-small.png,assets/icons/transit/quantum/train-1-small.png&highlight=0,b0ff,ffffff&color=ff000000?scale=1`
- `text=A&psize=16&font=fonts/arialuni_t.ttf&color=ff330000&name=icons/spotlight/spotlight-waypoint-b.png&ax=44&ay=48&scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/home-1-small.png&highlight=ff000000,78909c,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/restaurant-1-small.png&highlight=ff000000,f57f17,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/star_shadow-1-small.png,assets/icons/poi/quantum/star_container-1-small.png,assets/icons/poi/quantum/star-1-small.png&highlight=ff000000,cd814b,ffed47&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/library-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/civic_bldg-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/shoppingcart-1-small.png&highlight=ff000000,6d7be3,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/movie-1-small.png&highlight=ff000000,6d7be3,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/generic-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/shoppingbag-1-small.png&highlight=ff000000,6d7be3,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/generic-1-small.png&highlight=ff000000,6d7be3,ffffff&color=ff000000?scale=2`
- `name=assets/icons/transit/quantum/container_shadow-1-small.png,assets/icons/transit/quantum/container-1-small.png,assets/icons/transit/quantum/train-1-small.png&highlight=0,b0ff,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/stadium-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/worship_islam-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/transit/localizations/fr/paris-rail-1-small.png,assets/icons/transit/localizations/fr/paris-rail_inside-1-small.png&highlight=111b8a,ffffff&color=ff000000?scale=2`
- `name=assets/icons/transit/localizations/fr/paris-metro-1-small.png,assets/icons/transit/localizations/fr/paris-metro_inside-1-small.png&highlight=111b8a,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/museum-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/hospital_H-1-small.png&highlight=ff000000,db4437,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/camera-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/road/arrow-1-small.png&highlight=19286a&color=ff000000?scale=2`
- `name=assets/icons/transit/quantum/container_shadow-0-tiny.png,assets/icons/transit/quantum/container-0-tiny.png,assets/icons/transit/quantum/tram-0-tiny.png&highlight=0,b0ff,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/school-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/cemetery-1-small.png&highlight=ff000000,7cb342,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/lodging-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/theater-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/bar-1-small.png&highlight=ff000000,f57f17,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/monument-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/paw-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/transit/localizations/fr/paris-rail-0-tiny.png,assets/icons/transit/localizations/fr/paris-rail_inside-0-tiny.png&highlight=111b8a,ffffff&color=ff000000?scale=2`
- `name=assets/icons/transit/quantum/container_shadow-0-tiny.png,assets/icons/transit/quantum/container-0-tiny.png,assets/icons/transit/quantum/train-0-tiny.png&highlight=0,b0ff,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/bridge-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/historic-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/event_venue-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/worship_temple-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/tree-1-small.png&highlight=ff000000,7cb342,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/note-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/generic-1-small.png&highlight=ff000000,7cb342,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/bank_euro-1-small.png&highlight=ff000000,6d7be3,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/police-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/cafe-1-small.png&highlight=ff000000,f57f17,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-2-medium.png,assets/icons/poi/quantum/container-2-medium.png,assets/icons/poi/quantum/ferriswheel-2-medium.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-2-medium.png,assets/icons/poi/quantum/container-2-medium.png,assets/icons/poi/quantum/parking-2-medium.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-2-medium.png,assets/icons/poi/quantum/container-2-medium.png,assets/icons/poi/quantum/atm-2-medium.png&highlight=ff000000,6d7be3,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-2-medium.png,assets/icons/poi/quantum/container-2-medium.png,assets/icons/poi/quantum/cafe-2-medium.png&highlight=ff000000,f57f17,ffffff&color=ff000000?scale=2`
- `name=assets/icons/transit/quantum/container_shadow-1-small.png,assets/icons/transit/quantum/container-1-small.png,assets/icons/transit/quantum/bus-1-small.png&highlight=0,b0ff,ffffff&color=ff000000?scale=2`
- `name=assets/icons/transit/localizations/fr/paris-rail-3-large.png,assets/icons/transit/localizations/fr/paris-rail_inside-3-large.png&highlight=111b8a,ffffff&color=ff000000?scale=2`

- `https://maps.gstatic.com/mapfiles/api-3/images/spotlight-poi-dotless_hdpi.png`
- `https://maps.gstatic.com/mapfiles/api-3/images/spotlight-poi_hdpi.png`
- `https://maps.gstatic.com/mapfiles/api-3/images/icon_error.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/restaurant-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/generic_business-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/lodging-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/cafe-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/generic_recreational-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/bar-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/bus-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/civic_building-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/worship_general-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/museum-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/shopping-71.png`

- [Google Map icons with VisualRefresh - Stack Overflow](https://stackoverflow.com/questions/17746740/google-map-icons-with-visualrefresh)
- [image - What are the filenames of new colored Google maps markers? - Stack Overflow](https://stackoverflow.com/questions/19142242/what-are-the-filenames-of-new-colored-google-maps-markers)
- [javascript - Changing Color of New Google Markers (Google JS API v3) - Stack Overflow](https://stackoverflow.com/questions/22154188/changing-color-of-new-google-markers-google-js-api-v3)

#### Static image with hdpi resolution

	http://maps.googleapis.com/maps/api/staticmap?center=41.015408,28.970194&scale=2&zoom=15&size=470×250&sensor=false

See `scale=2` parameter, `scale=4` only available with key for "Google Maps API for Work"
Sizes are limited too.

https://developers.google.com/maps/documentation/staticmaps/

Grayscale : `...&style=feature:all|element:all|saturation:-100`

#### Streetview 3D depth

Google maps provide a depth image in a base64 encoded + zlib compressed format (inside XML) for streetview

	http://maps.google.com/cbk?output=xml&cb_client=maps_sv&v=4&dm=1&hl=en&panoid=4WGyVODT4of8gbmA48XKmw

- https://github.com/proog128/GSVPanoDepth.js/tree/master

### Google Search

Ignore country, go to http://www.google.com/ncr (No Country Redirect), to disable it, remove cookies

Search for specific country: http://www.google.com/search?hl=en&q=sample+query&gl=uk use `hl` for language and `gl` (for Geographic Location)

	/*
	Get Google search result as text
	But give not exacly the same as Google Search Page
	*/
	var urls = [], start = 0, rsz = 8;
	var site = "example.com";
	function xhrLoadHandler(event){
		var xhr = event.currentTarget;
		xhr.removeEventListener("load", xhrLoadHandler);
		xhr.removeEventListener("error", xhrErrorHandler);
		// should be a json
		var results;
		try {
			results = xhr.response["responseData"]["results"];
		}catch(error){
			console.log("Error at page " + start / rsz + ": " + error.message);
			console.log(urls.join("\n"));
			return;
		}
		
		for(var i = 0, l = results.length; i < l; i++){
			urls.push(results[i].url);
		}
	
		start += rsz;
		getNextPage();
	}
	function xhrErrorHandler(event){
		var xhr = event.currentTarget;
		xhr.removeEventListener("load", xhrLoadHandler);
		xhr.removeEventListener("error", xhrErrorHandler);
		console.log("Error at page " + start / rsz);
		console.log(urls.join("\n"));
	}
	function getNextPage(){
		var xhr = new XMLHttpRequest();
		xhr.addEventListener("load", xhrLoadHandler);
		xhr.addEventListener("error", xhrErrorHandler);
		xhr.open("GET", "https://ajax.googleapis.com/ajax/services/search/web?v=1.0&q=site:" + site + "&rsz=" + rsz + "&start=" + start);
		xhr.responseType = "json";
		xhr.send();
	}
	getNextPage();

### Chrome Web Store

#### Download Google Chrome extension without installing it

1. Find the ID of the extension you’re interested in. When on the details page of the extension, it will be something like `bfbmjmiodbnnpllbbbfblcplfjjepjdn` after `https://chrome.google.com/extensions/detail/` in the page URL
2. Paste this URL into your browser: `https://clients2.google.com/service/update2/crx?response=redirect&prodversion=38.0&x=id%3D{EXT_ID}%26installsource%3Dondemand%26uc` replacing `{EXT_ID}` with the extension ID.
3. You’ll be prompted to save a CRX file. Drag this file to a Chrome window and proceed with installation
 
	version = 10000 | 32.0
	os = mac | win | android | cros | openbsd | Linux
	product_channel = unknown
	product_id = chromecrx | chromiumcrx
	nacl_arch = arch = arm | x86-64 | x86-32
	https://clients2.google.com/service/update2/crx?response=redirect&os={os}&arch={arch}&nacl_arch={nacl_arch}&prod={product_id}&prodchannel={product_channel}&prodversion={version}&x=id%3D{EXT_ID}%26uc

Or:

- http://chrome-extension-downloader.com/

- https://addons.opera.com/en/extensions/details/download-chrome-extension-9/

See [CRX / NEX (Opera)](#crx--nex-opera)

#### CRX / NEX (Opera)

Find "PK" and remove all bytes before

	typedef struct {
	    SetBackColor(0xd8e5ed);
	    char magicNumber[4];
	    SetBackColor(0xd8edd8);
	    uint32 version;
	    SetBackColor(0xd8e5ed);
	    uint32 pkLength;
	    SetBackColor(0xd8edd8);
	    uint32 sigLength;
	    SetBackColor(0xf7d6c3);
	    byte pubKey[pkLength];
	    SetBackColor(0xd8edd8);    
	    byte sig[sigLength];
		byte zipData[];
	} CRX;
	

- [CRX Package Format - Google Chrome](https://developer.chrome.com/extensions/crx)

### Open Street Map

- [OpenStreetMap](https://www.openstreetmap.org/) `#map=12/49.2272/2.5303` (zoom/lat/lng)
- [Open styles, map gallery, catography](https://openmaptiles.org/styles/)
- [Maputnik](http://editor.openmaptiles.org/) `#11.6/47.3720/8.5420` (zoom/lat/lng)

### Vimeo

Link at time: `https://vimeo.com/1111111111#t=1m5s`

- taille standard : 504×404@440Kbps en On2 VP6
- taille "HD" : 1280×720@1500Kbps en On2 VP6

#### API

- [Player JavaScript API sur Vimeo sur l'API Vimeo Developer](https://developer.vimeo.com/player/js-api)

Require embed src with param `api=1` (only for listening messages, not required to send commands)

Add it in with wordpress:

	/* add post message api mode for vimeo embeds */
	add_filter('oembed_result' , function($html){
		return preg_replace_callback( '/(?<=")(https?:\/\/player.vimeo.com\/video/\/[^"]+)/', function($matches){return add_query_arg('api', '1', $matches[1]);}, $html);
	});

##### Pause video

	iframe.contentWindow.postMessage("{\"method\":\"pause\"}", "*");

##### Seek video

	iframe.contentWindow.postMessage("{\"method\":\"seekTo\", \"value\":0}", "*");// in seconds

##### Listen events

`event.data` is a serialized JSON object

	// register all event subscriptions you want: `pause`, `play`, `finish` or `playProgress`. `ready` don't need subscription, it's dispatched automatically
	iframe.contentWindow.postMessage("{\"method\":\"addEventListener\",\"value\":\"pause\"}", "*");
	window.addEventListener("message", function(event){JSON.parse(event.data).event});

### Digital Distribution Platforms

#### Apple Store

Badge:

- [App Store Marketing Guidelines - Apple Developer](https://developer.apple.com/app-store/marketing/guidelines/#downloadOnAppstore)

- http://www.apple.com/itunes/affiliates/resources/documentation/itunes-store-web-service-search-api.html
- https://linkmaker.itunes.apple.com/
- [Scrape ratings from iTunes store with PHP](https://gist.github.com/sgmurphy/1878352)

See also [Data/iTunes tips]()

App infos

	http://itunes.apple.com/lookup?id=%%&country=%REGION%&lang=%LANG%
	// Where %REGION% language ID like "us", "fr", "ca" (optional)
	// Where %LANG% language ID like "en", "fr", "es" (optional)
	// Return JSON with array (zero, one or more items, see `json.resultCount` field)

Artist or developper URL

	https://itunes.apple.com/artist/id%ARTIST_ID%

	https://itunes.apple.com/%REGION%/artist/id%ARTIST_ID%?l=%LANG%
	// Where %REGION% language ID like "us", "uk", "fr", "ca". But there are redirections like "us" → "en", "uk" → "gb"
	// Where %LANG% language ID like "en", "fr", "es"

App URL

	https://itunes.apple.com/app/id%APP_ID%

	https://itunes.apple.com/%REGION%/app/id%APP_ID%?l=%LANG%
	// Where %REGION% language ID like "us", "uk", "fr", "ca". But there are redirections like "us" → "en", "uk" → "gb"
	// Where %LANG% language ID like "en", "fr", "es"

#### Google Play

Badge:

- [Google Play Badge Generator | Android Developers](http://developer.android.com/distribute/tools/promote/badges.html)
- https://developer.android.com/downloads/brand/en_generic_rgb_wo.ai or https://android.googlesource.com/platform/frameworks/base/+/refs/heads/master/docs/downloads/brand/en_generic_rgb_wo.ai

App info

	https://play.google.com/store/xhr/getdoc
	// POST ids=%APP_ID%&hl=%LANG% (application/x-www-form-urlencoded)
	// Where %LANG% language ID like "en-us", "en_us" or "en"
	// Remove first 6 chars (JSONP XSS protection)
	// Replace "[," to "[null,", ",," to ",null," and ",]" to ",null]". You should use lookbehind and lookahead regexp
	// Parse it as JSON
	// `json[0][2][0]`: APP_ID is [0], APP_NAME is [8], user average rate is [16], user num reviews is [17], URL is [6]

- https://stackoverflow.com/questions/22134494/formatting-json-data-using-php

Or scrapper like http://code.google.com/p/google-playstore-api

- [PHP scrapper for Amazon App Store, Google Play Store and Windows Phone Store](https://github.com/pastfuture/MarketBot)
- [PHP scrapper for Google Play Store](https://github.com/thetutlage/Google-Play-Store-API)
- [JavaScript code to get reviews](http://android.stackexchange.com/questions/30185/how-to-display-comments-from-devices-that-i-dont-own/30668#30668)

Or use an unofficial API

- https://github.com/splitfeed/android-market-api-php (require a Google account)
- https://42matters.com/api/lookup
- http://playstore-api.herokuapp.com/playstore/apps/com.toj.gasnow

Developper URL

	https://play.google.com/store/apps/developer?id=%DEV_ID%

	https://play.google.com/store/apps/developer?id=%DEV_ID%&hl=%LANG%
	// Where %LANG% language ID like "en-us", "en_us" or "en"

App URL

	https://play.google.com/store/apps/details?id=%APP_ID%

	https://play.google.com/store/apps/details?id=%APP_ID%&hl=%LANG%
	// Where %LANG% language ID like "en-us", "en_us" or "en"
	

Other

Open an app

	<a href="intent://<anything>/#Intent;scheme=<scheme_name>;package=<must.open.this.p‌​ackage>;end">Force open by package_name app</a>

#### Windows Phone

App infos

	http://marketplaceedgeservice.windowsphone.com/v3.2/%LANG%/apps/%APP_ID%/
	// Where %LANG% language ID like "en-us"
	// Parse it as XML

Developper URL

	https://www.windowsphone.com/%LANG%/store/publishers?publisherId=%DEV_ID%
	// Where %LANG% language ID like "en-us"

App URL

	https://www.windowsphone.com/%LANG%/apps/%APP_ID%
	// Where %LANG% language ID like "en-us"

	http://windowsphone.com/s?appId=%APP_ID%

- `http://catalog.zune.net/v3.2/en-US/apps/APP_ID/?version=latest&clientType=CLIENT_TYPE&store=Zest`, where `APP_ID`, `CLIENT_TYPE` (optional) is `Zune+3.0` (Zune HD applications) or `WinMobile+7.1` (Windows Phone applications)
- [Windows Store app marketing guidelines - UWP app developer | Microsoft Docs](https://docs.microsoft.com/en-us/windows/uwp/publish/app-marketing-guidelines)
- [Publish Windows apps - Windows app development](https://developer.microsoft.com/en-us/store/publish-apps)
- [Coding4Fun ZuneDataViewer - Home](http://zunedata.codeplex.com/wikipage?title=Application%20Information)
- [How to get Windows app store dev center data - Stack Overflow](https://stackoverflow.com/questions/13912624/how-to-get-windows-app-store-dev-center-data/13912746#13912746)

#### Amazon

https://developer.amazon.com/appsandservices/resources/marketing-tools/using-badges
https://developer.amazon.com/announcements/tradebrand-guidelines.html

	http://www.amazon.com/gp/product/%ASIN%/

	http://www.amazon.com/gp/product/%ASIN%/ref=mas_pm_%APP_NAME%

### Facebook

Fakes likes, it's harmful: [Facebook Fraud - YouTube](https://www.youtube.com/watch?v=oVfHeWTKjag)

How stories are ranked: see [Rank content](Algorithms/Rank content)

	<html prefix="og: http://ogp.me/ns# fb: http://ogp.me/ns/fb#">
	…
	<meta property="og:title" content="…">
	<meta property="og:image" content="…">
	<meta property="og:site_name" content="…">
	<meta property="og:description" content="…">
	<meta property="og:url" content="…">
	<meta property="og:type" content="…">
	<meta property="fb:app_id" content="00000000000">

Supported locales: https://www.facebook.com/translations/FacebookLocales.xml

`https://www.facebook.com/photo.php?fbid=${PHOTO_ID}` and `https://www.facebook.com/${USER}/photos/${TIMELINE_ID}/${PHOTO_ID}/` where `00000000_${PHOTO_ID}_0000000000000000000_o.jpg` PHOTO_ID `00000000000000000` TIMELINE_ID `a.000000000000.000000.00000000000`

Default profile picture
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c29.0.100.100/p100×100/10354686_10150004552801856_220367501106153455_n.jpg?oh=e8ca515e48d1bc743308966715634bee&oe=58C66077
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c59.0.200.200/p200×200/10354686_10150004552801856_220367501106153455_n.jpg?oh=da4eafdad0da0d0958352977771c3fd7&oe=58BE4325
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c94.0.320.320/p320×320/10354686_10150004552801856_220367501106153455_n.jpg?oh=bc3e9e2ccfd2f54a246e4bfb77b63001&oe=58D3F5DE
https://scontent-cdg2-1.xx.fbcdn.net/t31.0-1/c379.0.1290.1290/10506738_10150004552801856_220367501106153455_o.jpg
https://scontent-cdg2-1.xx.fbcdn.net/t31.0-1/c379.0.1290.1290/10506738_10150004552801856_220367501106153455_o.png

Default page picture (flag)
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c9.0.32.32/p32×32/399548_10149999285987789_1102888142_n.png?oh=c46263750a4e4abc38892ff8b5ba1547&oe=58C587AD
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c19.0.64.64/p64×64/399548_10149999285987789_1102888142_n.png?oh=1ad605f9d9d0e204554e71ce8637135e&oe=58C38AF9
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c81.0.275.275/399548_10149999285987789_1102888142_n.png?oh=3b9a562b00802fed00b571fc7d1342bb&oe=58C907A0

Default xxx picture (student)
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c81.0.275.275/580846_10149999285985791_1565762244_n.png?oh=c46928fcbaf3660bd5834a2a48397fdf&oe=58B5F7C8

Default xxx picture (TV)
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c81.0.275.275/404798_10150000700901954_63461675_n.png?oh=d8d8add1bae05a606338c65cb9a4369e&oe=58CC165C

Default xxx picture (music note)
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c81.0.275.275/417197_10149999285992991_711134825_n.png?oh=ac147d4d487b0ead68b4c695d61b6cf1&oe=58D0AEFF

Default app picture (atomic box)
https://scontent-cdg2-1.xx.fbcdn.net/t39.2081-0/p128×128/851578_455087414601994_1601110696_n.png
https://scontent-cdg2-1.xx.fbcdn.net/t39.2081-0/851578_455087414601994_1601110696_n.png

- [Sharing Debugger - Facebook for Developers](https://developers.facebook.com/tools/debug/sharing/)
- [Facebook Crawler - Sharing](https://developers.facebook.com/docs/sharing/webmasters/crawler)
- [Open Graph Stories - Sharing](https://developers.facebook.com/docs/sharing/opengraph)
- [The Open Graph protocol](http://ogp.me/)
- [Webmasters - Sharing](https://developers.facebook.com/docs/sharing/webmasters/#markup)

#### Setup Facebook Website Application

**Note: the SDK is not available (loaded) in Firefox private mode by the Tracking Protection**

**The following examples will use Facebook Application ID `00000000000`**

Simply `<script src="https://connect.facebook.net/en_US/sdk.js#appId=00000000000&amp;version=v3.2" async></script>` then `window.fbAsyncInit = function(){console.log("FB SDK is ready")}`. Additional parameters can be provided, will auto init. So if you do it manually you will get [`FB.init has already been called - this could indicate a problem`](https://stackoverflow.com/questions/10415884/fb-init-has-already-been-called), see also [javascript - FB init function gives wrong version error - Stack Overflow](https://stackoverflow.com/questions/24019877/fb-init-function-gives-wrong-version-error).
Or use `document.createElement("script"); ... window.fbAsyncInit = function(){FB.init({appId: 00000000000, version: "v2.8"}); FB.getLoginStatus(...)}`

- `https://connect.facebook.net/en_US/sdk/debug.js`
- [Initialization - Web SDKs](https://developers.facebook.com/docs/javascript/reference/FB.init/v3.2)
- [Login Status - Web SDKs](https://developers.facebook.com/docs/reference/javascript/FB.getLoginStatus/)
- HTTPS is required, but `localhost` is allowed (but not `0.0.0.0`) [Requiring HTTPS for Facebook Login - Facebook for Developers](https://developers.facebook.com/blog/post/2018/06/08/enforce-https-facebook-login/) [Login Security - Facebook Login](https://developers.facebook.com/docs/facebook-login/security/#https)
 
	FB.login(..., {scope: "..."});

- [Reference - Facebook Login](https://developers.facebook.com/docs/facebook-login/permissions/v3.2)

For App ID, check it with `http://graph.facebook.com/00000000000`. For pages (TL;DR: you have to create an App ID):

- https://stackoverflow.com/questions/6997368/facebook-how-to-receive-app-id-for-official-page
- https://stackoverflow.com/questions/10339192/how-to-get-app-id-for-an-existing-facebook-page
- multiple domains is allowed, but must reflect Website URL (else you will get an error "App domains must match the domain of the Secure Canvas URL, Mobile Site URL, Unity Binary URL, Site URL or Secure Page Tab URL. Please correct these domains: foobaz.com"). Ex.: Website/Site URL = http://www.example.com App Domains = example.fr example.es example.de example.co.uk

#### Facebook login

	function doSomethingWithFBLoginStatus(response, state){
		// The user doesn't allow the app, even after rerequest
		// The user cancel relogin
		// Other reason...
		if(state !== "getstatus" && response.status !== "connected"){
			// Should display something to the user
			console.assert(false, "Something wrong with get FB login status", state);
			return;
		}
		
		switch(response.status){
			case "connected":
				doSomethingWithFB(response.authResponse.accessToken);
				break;
			case "not_authorized":
				// Request FB user to authorize the FBApp
				// https://developers.facebook.com/docs/reference/javascript/FB.login/v2.12 auth_type
				FB.login(response => doSomethingWithFBLoginStatus(response, "rerequest"), {scope: "permission1,permission2,permission3", auth_type: "rerequest"});
				break;
			case "unknown":
				// Request FB user to (re)login
				FB.login(response => doSomethingWithFBLoginStatus(response, "relogin"));
				break;
			default:
				console.assert(false, "Facebook status invalid", response.status);
		}
	}
	
	// https://developers.facebook.com/docs/facebook-login/web#checklogin
	FB.getLoginStatus(response => doSomethingWithFBLoginStatus(response, "getstatus"));

#### Facebook shares and likes count

Without access token:

`http://graph.facebook.com/?id=URL&fields=og_object%7Blikes.summary(total_count).limit(0)%7D,share` returns JSON `json.share.share_count`

With access token:

https://developers.facebook.com/tools/explorer/?method=GET&path=%3Fid%3DURL%26fields%3Dengagement&version=v2.9

- [Getting the Facebook like/share count for a given URL - Stack Overflow](https://stackoverflow.com/questions/9728279/getting-the-facebook-like-share-count-for-a-given-url)

#### Facebook share and like

Simple URL. See [Share URLs](#share-urls)

Following methods require an Facebook App ID:

- [Facebook Share button](https://stackoverflow.com/questions/6145489/is-the-facebook-share-button-being-deprecated/) (still works, but depreciated)
- Feed Dialog or Share Dialog URL:

		https://www.facebook.com/dialog/share?
		  app_id=145634995501895
		  &display=popup
		  &quote=An%20example%20quote
		  &href=https%3A%2F%2Fdevelopers.facebook.com%2Fdocs%2F

	Note: share popup with `quote` text and URL of animated gif file as `href` will not displayed exactly the same as shared animated gif URL (as `href`). The playback (play/pause) of the gif is not available (Facebook bug): click open URL. If the gif is not autoplayed (see "Auto-Play Videos" https://www.facebook.com/settings?tab=videos). On mobile the gif is display as standard link.

		https://www.facebook.com/dialog/feed?
		  app_id=145634995501895
		  &display=popup
		  &caption=An%20example%20caption
		  &link=https%3A%2F%2Fdevelopers.facebook.com%2Fdocs%2F
- Feed Dialog or Share Dialog from SDK. SDK need to be included, see [Setup Facebook Website Application](#setup-facebook-website-application).

		var dialog = FB.ui({
			method: "share",
			href: url,
			quote: message
		});
		// FB.UIServer._triggerDefault(dialog.id);// if need to close the dialog

> Share dialog, which gives people the most flexibility. They can choose where they want to share, including in groups and private messages on Messenger
> If you want to let someone post a plain text status update without a link attachment, you should use the Feed dialog. If you're sharing photos or videos rather than links, you will need to create a custom interface that lets people post to their own timeline, which requires implementing [Facebook Login](https://developers.facebook.com/docs/facebook-login/login-flow-for-web/) and requesting the [`publish_actions` permission](https://developers.facebook.com/docs/facebook-login/permissions/#reference-publish_actions)

- [Share Dialog - Sharing](https://developers.facebook.com/docs/sharing/reference/share-dialog)
- [Feed Dialog - Sharing](https://developers.facebook.com/docs/sharing/reference/feed-dialog/v2.1)

Note: undocumented parameters: `locale=en_US`

Metadata:

- [The Open Graph protocol](http://ogp.me/#structured)
- [opengraph - How does Facebook Sharer select Images? - Stack Overflow](https://stackoverflow.com/questions/1138460/how-does-facebook-sharer-select-images)
- [Facebook Content Sharing Best Practices](https://developers.facebook.com/docs/sharing/best-practices#images)
- [Creating Custom Stories](https://developers.facebook.com/docs/opengraph/creating-custom-stories#objecttypes-properties)
- https://developers.facebook.com/tools/debug/
- [Object Debugger](https://developers.facebook.com/tools/debug/og/object?q=%s)
- [Platform Update: Facebook Removes Pre-Filled Stream Stories, Like Box Configurator Gets Border Color | SocialTimes](http://www.adweek.com/socialtimes/pre-filled-stream-stories-like-box-border-color/263479?red=if)
- [Platform Policy 2.3](https://developers.facebook.com/docs/apps/review/prefill)
 
	<iframe src="https://www.facebook.com/plugins/like.php?href=YOUR_URL" scrolling="no" style="border:none; width:450px; height:80px"></iframe>

	https://www.facebook.com/plugins/like.php?
		href			URL
		layout			button_count
		width			75
		show_faces		true
		action			like
		colorscheme		light
		font			arial or lucida%20grande
		height			30
		app_id			120295828008556
		channel			...url
		container_width	0
		locale			en_US
		sdk				joey
		send			true
		share			false

- [Like Button - Social Plugins](https://developers.facebook.com/docs/plugins/like-button)
- [Social Plugins](https://developers.facebook.com/docs/plugins)

#### Stream

See [Facebook Graph API](#facebook-graph-api)

- (obselete) http://liljosh.com/facebook-page-json-rss-feed/
- (obselete) `https://www.facebook.com/feeds/page.php?id=163276271689&format=json` (`format=rss20`)

#### Facebook Graph API

**User ID are app scoped/specific**: [Graph API User](https://developers.facebook.com/docs/graph-api/reference/user/#Reading)

The field `username` is no more available. It's possible to get it by `https://www.facebook.com/app_scoped_user_id/APP_SCOPED_USER_ID/` (get with Graph API `/me?fields=link`) or `https://www.facebook.com/USER_ID/` (logged only) redirect to `https://www.facebook.com/USERNAME`

- Check validity of access token: https://graph.facebook.com/me?access_token=ACCESS_TOKEN (return `{"error": ...}` if it's invalid)
- [Expiration and Extension - Facebook Login](https://developers.facebook.com/docs/facebook-login/access-tokens/expiration-and-extension)
- [Access Token Tool - Facebook for Developers](https://developers.facebook.com/tools/access_tokens)
- [Access Token Debugger - Facebook for Developers](https://developers.facebook.com/tools/debug/accesstoken/)
- [Access Tokens - Facebook Login](https://developers.facebook.com/docs/facebook-login/access-tokens/)
- [Best practice for Facebook login flow with the JavaScript SDK and PHP SDK v4.1 :: Sammy Kaye Powers](https://www.sammyk.me/best-practice-for-facebook-login-with-the-javascript-sdk-and-php-sdk-v4-1)
- [How to create never expires Access Token for Facebook Page](https://medium.com/@Jenananthan/how-to-create-non-expiry-facebook-page-token-6505c642d0b1)
- Extends the validity of the access token (for be used by the server APP): https://graph.facebook.com/oauth/access_token?client_id=YOUR_APP_ID&client_secret=YOUR_APP_SECRET&grant_type=fb_exchange_token&fb_exchange_token=YOUR_ACCESS_TOKEN

Test with Demo application [Graph API Explorer](https://developers.facebook.com/tools/explorer/), "Access Token" > (button) "Get User Access Token" to select required permissions to test.
You can test JS code with https://developers.facebook.com/tools/javascript-console/

Common parameters:

- `summary=true` is available on `{user-id}/likes`, `{user-id}/friends` (where `summary` is always true) to return `{"data":[], summary: {"total_count": 131}}`
- `locale` set locale like `de_DE`
- `access_token` to set use you access token. Get it via an application
	https://graph.facebook.com/oauth/access_token?grant_type=client_credentials&client_id={app-id}&client_secret={app-secret}
	To get a user access token use param `user_id` and `user_secret` instead.
	See https://developers.facebook.com/docs/facebook-login/access-tokens/
	Ex. of invalid access token: `AAACZBLSe4fcoBAFcGMJZAUS9OthIr5o6ZCUySgXYj0nfWX7u08×7h0VZAFFuJJs9LmeWgud2u5ZCEZCeUHZCVIq1Y2j4gjKAjJ0gx5OY9PBihlABJn64njm`
- `limit=xx` is not fixed. Never rely to it for a fixed limit between pages. Ex: `limit=500`, but return `487` items for page 1 and `492` items for page 2.
	
	- [Maximum limit fetching facebook pages with Graph API - Stack Overflow](https://stackoverflow.com/questions/29730526/maximum-limit-fetching-facebook-pages-with-graph-api)
	- [The limit of Facebook's graph api "limit" parameter - Stack Overflow](https://stackoverflow.com/questions/14876105/the-limit-of-facebooks-graph-api-limit-parameter)
- `fields` to filder fields. Ex.: `me/albums?fields=count,name`: will get only `id`, photo `count` and `name` per album
- `order=reverse_chronological` works only for comments

- `/me/picture?type=large` but also `?width=1000` or `?height=1000` (preserve aspect ratio). If both width and height are defined, image will be cropped
- `{page-id}/feed?fields=id,shares,likes.limit(0).summary(true),comments.limit(0).summary(true)`
- `{post-id}?fields=id,shares,likes.limit(0).summary(true),comments.limit(0).summary(true)`

Error codes: [Using the Graph API](https://developers.facebook.com/docs/graph-api/using-graph-api/#errors)

	{
		"error": {
			"message": "Error validating access token: The user is enrolled in a blocking, logged-in checkpoint",
			"type": "OAuthException",
			"code": 190,
			"error_subcode": 490,
			"error_data": "{\"checkpoint_flow_id\":\"207799259245384\",\"checkpoint_content_id\":\"0\",\"show_native_checkpoints\":\"\"}",
			"fbtrace_id": "Dmruy525PeA"
		}
	}

	{
		"error": {
			"message": "Invalid OAuth access token.",
			"type": "OAuthException",
			"code": 190,
			"fbtrace_id": "F32VcO27MO3"
		}
	}

Get infos about a page:

- likes/fan count https://stackoverflow.com/questions/29702192/request-to-get-total-count-of-facebook-page-likes-in-v2-3-api
- likes `/{object-id}/likes?summary=true` `response.summary.total_count`
- feed https://stackoverflow.com/questions/28204978/facebook-rss-feeds-have-stopped-working/28291957#28291957

To get page categories (paged):

	/search?type=placetopic&topic_filter=all&limit=5000&locale=fr_FR

- https://gist.github.com/bloudermilk/2173940
- [Facebook Pages — Authoritative List of Categories - Stack Overflow](https://stackoverflow.com/questions/4216648/facebook-pages-authoritative-list-of-categories/)

Get count of posts, friends, likes and uploaded medias. Use jQuery Deferred (es2016 `Promise` like):

	<!DOCTYPE html PUBLIC>
	<html>
		<head>
			<title>Facebook stats</title>
			<script src="https://code.jquery.com/jquery-3.1.1.min.js"></script>
			<script src="//connect.facebook.net/fr_FR/sdk.js#appId=1509340019322396&version=v2.8&status=1" async></script>
		</head>
		<body>
			
			<button id="fb_start">Get my Facebook stats</button>
			<pre id="output"></pre>
			
			<script>
			var fbSDKInit = $.Deferred();
			// Facebook SDK init listener
			window.fbAsyncInit = () => fbSDKInit.resolve("FBSDKInit");
			
			function mergeObjects(obj1, obj2){
				// Both are arrays
				if(Array.isArray(obj1) && Array.isArray(obj2)){
					return obj1.concat(obj2);
				}
				
				return Object.assign({}, obj1, obj2);
			}
			
			// Doesn't support Multiple Requests https://developers.facebook.com/docs/graph-api/using-graph-api#multirequests nor batch requests https://developers.facebook.com/docs/graph-api/making-multiple-requests
			function getFBGraphAllData(graphURL){
				return getFBGraphResponse(graphURL).pipe(response => {
					// Paging https://developers.facebook.com/docs/graph-api/using-graph-api#paging
					// paging.next is available if next page exist (but could be empty)
					if(response.paging && response.paging.next){
						return getFBGraphAllData(response.paging.next).pipe(data => mergeObjects(response.data, data));
					}
		
					return response.data || response;// some edges return the field data as object  (`{}`, ex. `/user/picture/`) and no `paging` field
				});
			}
			
			// Get Facebook Graph API data as promise
			function getFBGraphResponse(relativeURL){
				var d = $.Deferred();
				FB.api(relativeURL, (response) => d[response && !response.error ? "resolve" : "reject"](response));
				return d.promise();
			}
			
			function loginFB(permissions, rerequest = false){
				var options = {
					scope: permissions.join(","),
					return_scopes: true
				};
				if(rerequest){
					options.auth_type = "rerequest";
				}
				
				var d = $.Deferred();
				// reject: The user user cancelled login or did not fully authorize.
				FB.login((response) => d[response.authResponse ? "resolve" : "reject"](response), options);
				
				return d.promise();
			}
			
			function checkFBStatus(){
				var d = $.Deferred();
				FB.getLoginStatus(response => d.resolve(response));
				return d.promise();
			}
			
			// Check if all values in array are in sourceArray
			function arrayMatchAll(array, sourceArray){
				return array.every(value => sourceArray.indexOf(value) >= 0)
			}
			
			// Log the user if not and check permissions
			// permissions called also scope/scopes
			// https://developers.facebook.com/docs/facebook-login/permissions
			function loginAndGrantPermissionsFB(requiredPermissions){
				return checkFBStatus().pipe(function(response){
					return checkFBStatus().pipe(function(response){
						var status = response.status;
						var promise;
						if(status === "connected"){
							promise = getFBGraphAllData("/me/permissions")
								.pipe(data => data.filter(permission => permission.status == "granted").map(permission => permission.permission))
								.pipe(grantedPermissions => {
									if(arrayMatchAll(requiredPermissions, grantedPermissions)){
										return grantedPermissions;
									}
				
									// Special case: add an oportunity to the user to grant permissions again
									return loginFB(requiredPermissions, true)
										.pipe(response => response.authResponse.grantedScopes.split(","));
								});
						}else{
							promise = loginFB(requiredPermissions, status === "not_authorized")
								.pipe(response => response.authResponse.grantedScopes.split(","));
						}
						
						return promise.pipe(grantedPermissions => {
							// If all requested permissions are granted
							if(arrayMatchAll(requiredPermissions, grantedPermissions)){
								return $.Deferred().resolve(grantedPermissions);
							}
							
							return $.Deferred().reject({error: {message: "All required permissions are not granted."}});
						});
					});
				});
			}
			
			function addCount(target, field, count){
				target[field] += count;
				return target;
			}
			function getLength(items){
				return items.length;
			}
			function getSummaryCount(result){
				return result.summary.total_count;
			}
			
			function getFBData(){
				var result = {
					name: null,
					picture: null,
					posts: 0,
					friends: 0,
					likes: 0,
					medias: 0
				};
				
				var addLikesCount = addCount.bind(null, result, "likes");
				var addMediaCount = addCount.bind(null, result, "medias");
				var lastYear = Math.floor(Date.now() / 1000 - 365*24*60*60);//timestamp in seconds
				
				return fbSDKInit
					
					.pipe(loginAndGrantPermissionsFB.bind(null, [
						// https://developers.facebook.com/docs/facebook-login/permissions
						// This permissions are approved by default
						"email", "public_profile", "user_friends",
						// Additional permissions
						"user_posts", "user_likes", "user_photos", "user_videos"
					]))
					.pipe(function(){
						return $.when(
							// Indentity
							getFBGraphResponse("/me?fields=name,picture.type(large)").pipe(response => {
								result.name = response.name;
								result.picture = response.picture.data.is_silhouette ? null : response.picture.data.url;
								return result;
							}),
				
							// Posts
							//getFBGraphAllData("/me/posts?fields=id&limit=500").pipe(getLength).pipe(addCount.bind(null, result, "posts")),
							getFBGraphAllData(`/me/posts?since=${lastYear}&fields=id&limit=500`).pipe(getLength).pipe(addCount.bind(null, result, "posts")),// posts over one year
				
							// Friends
							getFBGraphResponse("/me/friends?limit=0").pipe(getSummaryCount).pipe(addCount.bind(null, result, "friends")),
				
							// Likes
							getFBGraphResponse("/me/likes?limit=0&summary=true").pipe(getSummaryCount).pipe(addLikesCount),
							getFBGraphAllData("/me/games?fields=id&limit=500", true).pipe(getLength).pipe(addLikesCount),
							getFBGraphAllData("/me/books?fields=id&limit=500", true).pipe(getLength).pipe(addLikesCount),
							getFBGraphAllData("/me/movies?fields=id&limit=500", true).pipe(getLength).pipe(addLikesCount),
							getFBGraphAllData("/me/music?fields=id&limit=500", true).pipe(getLength).pipe(addLikesCount),
							getFBGraphAllData("/me/television?fields=id&limit=500", true).pipe(getLength).pipe(addLikesCount),
							getFBGraphAllData("/me/og.likes?fields=id&limit=500", true).pipe(getLength).pipe(addLikesCount),
		
							// Medias
							getFBGraphAllData("/me/albums?fields=count&limit=100", true).pipe(function(data){
								return data.reduce((total, album) => total + album.count, 0);
							}).pipe(addMediaCount),
							getFBGraphAllData("/me/videos?type=uploaded&fields=id", true).pipe(getLength).pipe(addMediaCount)
						);
					}).pipe(() => result);
			}
			
			document.getElementById("fb_start").addEventListener("click", function(){
				var start = Date.now();
				document.getElementById("output").textContent = "Getting Facebook stats...";
				getFBData().always(data => document.getElementById("output").textContent = `Facebook stats (duration: ${Date.now() - start}ms):\n\n${JSON.stringify(data, null, '\t')}`);
				// response.error.type == "OAuthException");// response.error.code https://developers.facebook.com/docs/graph-api/using-graph-api#errors
			});
			</script>
		</body>
	</html>

About getting the registration date:

No API provide this information. Previously, before app-scoped user-ids, an [estimation date could be done based on user ID](http://metadatascience.com/2013/03/11/inferring-facebook-account-creation-date-from-facebook-user-id/)
Then you find the first posts, photos or profile picture: [Facebook API: Get all profile pictures - Stack Overflow](https://stackoverflow.com/questions/5058144/facebook-api-get-all-profile-pictures)
From 10 year ago, `length=1` over 6 month with `until` and `since` (Unix timestamps) then try 5 year after
Note: It's possible to back dating content with `backdated_time`: https://developers.facebook.com/docs/graph-api/common-scenarios#backdating

##### Get age from Facebook user's birthdate

	// facebook-user-age.js
	/**
	 * Get Facebook user age from given birthdate
	 * Can be MM/DD/YYYY or MM/DD or YYYY
	 * @param {String} birthdate
	 * @returns {Number}
	 * @see https://developers.facebook.com/docs/graph-api/reference/user/
	 */
	module.exports = birthdate => {
		const currentYear = new Date().getFullYear();
		// Convert to UTC ISO-8601 date
	
		// MM/DD/YYYY
		if(birthdate.length === 10){
			const [month, day, year] = birthdate.split("/");
			return currentYear - new Date(`${year}-${month}-${day}`).getFullYear() - 1;
		}
	
		// YYYY
		if(birthdate.length === 4){
			const year = birthdate;
			return currentYear - parseInt(year, 10) - 1;
		}
	
		// MM/DD
	
		return NaN;
	};
	

#### Share an external Animation

Post an url to create a card/push with the animation + a link

GIF: Only posted URL, not file uploaded (in Facebook album)

##### Video

**To get a custom HTML5 player (embeded in Facebook feed), you must be whitlisted.** Don't know how. 

(need verification) Note: `og:video` can be defined multiple times (for types `text/html`, `application/x-shockwave-flash`, `video/mp4`, etc.). Even if it's not a video
Note: `og:video`, `og:video:type`, `og:video:width` and `og:video:width` should be explicited provided for each format
Note: `og:video:secure_url` is not required, but **`og:video`/`og:video:url` must use HTTPS**
Note: `fb:app_id` is not required
Note: `text/html` type it's seem to be **reserved to whitlisted domains**. No information is available about the process of whitlisting. Custom flash player is still possible (`application/x-shockwave-flash`) or use only `video/mp4`
Note: if the `og:video` as `text/html` is not valid, Facebook fallback to the first `og:video` url will be used as `src` for a `<video>` (directly in feed) and `og:video:type` as `type`
Note: a div with `me-cannotplay` class with a link "Download File" as child
Note: based on `og:image` file dimensions if width <= ~400 the image is squared and take 1/3 of the post width. Where the title and description take 2/3. If width > ~400 the image will take all the width and only the title and origin are visible (no description)
Note: does the size provided (`og:video:width` and `og:video:height`) have any impact? 

	<meta property="og:type" content="video">
	<meta property="og:image" content="poster.jpg">
	
	<!-- direct asset ref: -→
	<meta property="og:video" content="http://example.com/video.mp4">
	<meta property="og:video:type" content="video/mp4">
	<meta property="og:video:width" content="500">
	<meta property="og:video:height" content="400">
	
	<!-- Facebook iframe embed  -→
	<meta property="og:video:url" content="http://example.com/video.html">
	<meta property="og:video:type" content="text/html">
	<meta property="og:video:width" content="500">
	<meta property="og:video:height" content="400">
	
	<!--  legacy swf embed:  -→
	<meta property="og:video:url" content="http://example.com/animation.swf">
	<meta property="og:video:type" content="application/x-shockwave-flash">
	<meta property="og:video:height" content="500">
	<meta property="og:video:width" content="400">

2016/12/09: only MP4 and SWF served via HTTPS works. In user feed (desktop), MP4 will be played in native HTML5 player and SWF will be placed in object inside an isolated iframe. On mobile (native app) it's a simple link (not interaction)

It's related with `https://www.facebook.com/ajax/flash/expand_inline.php?...` `response.dompos[0][3].__html`

> When you call the debugger to scrap changes on your og:tags of your page, all previous Facebook shares of that URL will still show the old image/video. There is no way to update all previous posts and it's this way by design for security reasons. Otherwise, someone would be able to pretend that a user shared something that he/she actually didn't.
— [opengraph - Facebook Open Graph not clearing cache - Stack Overflow](https://stackoverflow.com/questions/5776567/facebook-open-graph-not-clearing-cache)

- https://developers.facebook.com/docs/sharing/webmasters#video
- https://developers.facebook.com/docs/reference/opengraph/object-type/video.other
- https://stackoverflow.com/questions/30934400/embed-video-iframe-in-facebook-wall
- https://stackoverflow.com/questions/8708233/share-html5-player-on-facebook-wall
- https://blog.kaltura.com/facebook-now-require-html5-and-fallback-in-open-graph/
- http://player.kaltura.com/modules/KalturaSupport/components/share/Share.html
- [Facebook video share - Stack Overflow](https://stackoverflow.com/questions/27525006/facebook-video-share/28987920#28987920)
- [Setting Videos not Hosted on Brightcove to Play within Facebook | Brightcove Support](https://support.brightcove.com/en/video-cloud/docs/setting-videos-not-hosted-brightcove-play-within-facebook)
- [html5 - How to embed a iframe player in FB's wall? - Stack Overflow](https://stackoverflow.com/questions/33215828/how-to-embed-a-iframe-player-in-fbs-wall/33226663#33226663)
- [How to embed my own flash video player in Facebook? - Stack Overflow](https://stackoverflow.com/questions/26367646/how-to-embed-my-own-flash-video-player-in-facebook/26399297#26399297)
- [Embedding video player html5 iframe in facebook share like YouTube - Stack Overflow](https://stackoverflow.com/questions/28815838/embedding-video-player-html5-iframe-in-facebook-share-like-youtube#comment45907003_28815838)

Note: HTTPS is required to be played (and the field `og:video:secure_url`? else it's recognized as video, but not displayed as video player)

##### GIF

Working GIFs:

- 600 × 400 for 319kB
- 499 × 499 for 931kB

Interlaced could not work well

The GIF is not working properly if you add `quote` using dialog share.

Note: GIF will be cached and converted as MP4

- [How to Post an Animated Image (Like .gif) On my Wall? | Facebook Help Community](https://www.facebook.com/help/community/question/?id=383880968404336)

Works ? Else detect the crawler and output the gif instead:

	header('Content-Length: ' . filesize($gif));
	header('Content-Type: ' . mime_content_type($gif));
	readfile($gif);
	exit();

	<meta property="og:site_name"   content="Site Name">
	<meta property="og:url"         content="url to GIF on web">
	<meta property="og:title"       content="Title of GIF page">
	<meta property="og:description" content="Some description">
	<meta property="og:type"        content="video.other">
	<meta property="og:image"       content="Same as og:url above">
	<meta property="og:image:width"  content="800">
	<meta property="og:image:height" content="400">

- [opengraph - How does Giphy share gifs to facebook? (2015, NOT FLASH ANYMORE) - Stack Overflow](https://stackoverflow.com/questions/31216481/how-does-giphy-share-gifs-to-facebook-2015-not-flash-anymore/35999163#35999163)

For `http://giphy.com/gifs/hot-funny-cartoon-fBEDuhnVCiP16`:

	<meta property="og:url" content="https://media.giphy.com/media/fBEDuhnVCiP16/giphy.gif">
	<meta property="og:title" content="The Simpsons GIF - Find &amp; Share on GIPHY">
	<meta property="og:description" content="Discover &amp; Share this The Simpsons GIF with everyone you know. GIPHY is how you search, share, discover, and create GIFs.">
	<meta property="og:type" content="video.other">
	<meta property="og:image" content="https://media.giphy.com/media/fBEDuhnVCiP16/giphy.gif">
	<meta property="og:image:width" content="500">
	<meta property="og:image:height" content="376">
	<meta property="og:type" content="video">
	<meta property="og:image" content="https://media.giphy.com/media/fBEDuhnVCiP16/giphy-facebook_s.jpg">
	<meta property="og:image:width" content="480">
	<meta property="og:image:height" content="270">
	<meta property="og:type" content="video">
    <meta property="og:image" content="https://media.giphy.com/media/fBEDuhnVCiP16/giphy-facebook_s.jpg">
    <meta property="og:image:width" content="480">
    <meta property="og:image:height" content="270">
    <meta property="og:video" content="https://giphygifs.s3.amazonaws.com/swiphy20141103.swf?api_hostname=&gif_url=https%3A%2F%2Fmedia.giphy.com%2Fmedia%2FfBEDuhnVCiP16%2Fgiphy.gif&giphy_height=376&video_url=https%3A%2F%2Fmedia.giphy.com%2Fmedia%2FfBEDuhnVCiP16%2Fgiphy.mp4&giphyWidth=500&path=%2Fgifs%2Fhot-funny-cartoon-fBEDuhnVCiP16&destination_url=http%3A%2F%2Fgiphy.com%2Fgifs%2Fhot-funny-cartoon-fBEDuhnVCiP16&giphyHeight=376&gif_id=fBEDuhnVCiP16&mode=embed&giphy_width=500">
    <meta property="og:video:secure_url" content="https://giphygifs.s3.amazonaws.com/swiphy20141103.swf?api_hostname=&gif_url=https%3A%2F%2Fmedia.giphy.com%2Fmedia%2FfBEDuhnVCiP16%2Fgiphy.gif&giphy_height=376&video_url=https%3A%2F%2Fmedia.giphy.com%2Fmedia%2FfBEDuhnVCiP16%2Fgiphy.mp4&giphyWidth=500&path=%2Fgifs%2Fhot-funny-cartoon-fBEDuhnVCiP16&destination_url=http%3A%2F%2Fgiphy.com%2Fgifs%2Fhot-funny-cartoon-fBEDuhnVCiP16&giphyHeight=376&gif_id=fBEDuhnVCiP16&mode=embed&giphy_width=500">
    <meta property="og:video:type" content="application/x-shockwave-flash">
    <meta property="og:video:width" content="470">
    <meta property="og:video:height" content="353">

#### Detect Facebook crawler

	if (
		strpos($_SERVER["HTTP_USER_AGENT"], 'facebookexternalhit/') !== false ||
		strpos($_SERVER["HTTP_USER_AGENT"], 'Facebot') !== false
	) {
		// it is probably Facebook's bot
	}
	else {
		// probably not
	}

- [Facebook Crawler - Sharing](https://developers.facebook.com/docs/sharing/webmasters/crawler)

### Twitter

Default profile picture: `https://abs.twimg.com/sticky/default_profile_images/default_profile_1_400×400.png` where `1` can be changed

**Note: [player card](https://dev.twitter.com/cards/types/player) require HTTPS and must be approved.** It's composed as an iframe playing a stream (video/audio). `twitter:player:stream` support only MP4 (H.264 and/or AAC)

Note: Twitter use meta `twitter:image` and remove mention to `twitter:image:src`, but only the lastest works (or have the precedence). See https://twittercommunity.com/t/twitter-image-src-or-twitter-image/16085/7
Note: Use `twitter:image:alt` to provide alternative text content. Equivalent of `alt` attribute of an `img` element. See [Twitter Has Alt Text! (with some caveats) | Adrian Roselli](http://adrianroselli.com/2016/03/twitter-has-alt-text-with-some-caveats.html)
Note: For Summary card with large image, the aspect ratio is 2:1. See [Advertiser creative specifications](https://business.twitter.com/en/help/campaign-setup/advertiser-card-specifications.html)

- [Twitter timeline in true chronological order include retweets](https://twitter.com/search?f=tweets&vertical=default&q=filter%3Afollows%20-filter%3Areplies%20include%3Anativeretweets) (click "Latest" on mobile)
- [Twitter timeline in true chronological order without retweets, liked tweets](https://twitter.com/search?f=tweets&q=filter%3Afollows%20-filter%3Areplies&src=typd)
- Exemple of complex search: https://twitter.com/search?f=tweets&vertical=default&q=to%3Awaxpancake%20-from%3Awaxpancake%20%28irony%20OR%20ironic%20OR%20%22else%27s%20retweet%22%20OR%20%22have%20found%22%20OR%20%22someone%20i%20follow%22%29%20since%3A2018-06-06%20-from%3Aadambanksdotcom&src=typd
- [Obfusc-a-tweet reloaded](http://xem.github.io/articles/#obfuscatweet_url_en)
- [API changelog](https://www.hitchhq.com/twitter/activities)
- [Big GIFs welcome: Twitter increases maximum GIF size to 15MB on web | Ars Technica](http://arstechnica.com/business/2016/07/big-gifs-welcome-twitter-increases-maximum-gif-size-to-15mb-on-web/)
- [Card Validator | Twitter Developers](https://cards-dev.twitter.com/validator)
- [Advertiser creative specifications](https://business.twitter.com/en/help/campaign-setup/advertiser-card-specifications.html)

- `https://pbs.twimg.com/media/MEDIA_ID?format=png&name=large`, `https://pbs.twimg.com/media/MEDIA_ID.png:large` (`.jpg`, without `:large`)

**Image at maximum resolution**, right-click -> View in new tab -> add `:orig` after the `.jpg` in the URL

Tweets: `https://twitter.com/i/profiles/show/{user}/timeline/tweets?include_available_features=1&include_entities=1&include_new_items_bar=true`
	max_position={last_tweet_id}
Headers:
	Accept: application/json, text/javascript, */*; q=0.01
	Referer: https://twitter.com/{user}
	User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/603.3.8 (KHTML, like Gecko) Version/10.1.2 Safari/603.3.8
	X-Twitter-Active-User: yes
	X-Requested-With: XMLHttpRequest
Response:
	"items_html"
	https://github.com/kennethreitz/twitter-scraper/blob/master/twitter_scraper.py

Media video:

Use same APIs used by `https://mobile.twitter.com`:
`https://api.twitter.com/2/timeline/conversation/${TWEET_ID}.json?include_profile_interstitial_type=1&include_blocking=1&include_blocked_by=1&include_followed_by=1&include_want_retweets=1&include_mute_edge=1&include_can_dm=1&include_can_media_tag=1&skip_status=1&cards_platform=Web-12&include_cards=1&include_ext_alt_text=true&include_reply_count=1&tweet_mode=extended&include_entities=true&include_user_entities=true&include_ext_media_color=true&send_error_codes=true&count=20&ext=mediaStats%2ChighlightedLabel`
Require header `authorization: Bearer ....`
Read the JSON, as `root[0].globalObjects.tweets[${TWEET_ID}].extended_entities.media[0].video_info.variants` 
Previously, in `https://api.twitter.com/1.1/conversation/show.json?include_profile_interstitial_type=1&include_blocking=1&include_blocked_by=1&include_followed_by=1&include_want_retweets=1&skip_status=1&cards_platform=Web-12&include_cards=1&include_ext_media_color=true&tweet_mode=extended&id=${TWEET_ID}&max_id=${TWEET_ID}`:
Read the JSON, as `roor[0].extended_entities.media[0].video_info.variants`

Or APIs used by 
`https://api.twitter.com/1.1/videos/tweet/config/${TWEET_ID}.json`
Require header `authorization: Bearer ....`
Read the JSON as `root.track.playbackUrl`

Or use jDownloader with `https://twitter.com/${USER}/status/${TWEET_ID}/video/1`

- [How I downloaded a video from Twitter using Curl | Zero One Labs](http://zeroonelabs.com/how-i-downloaded-a-video-from-twitter-using-curl/)
- [SAVEVIDEO.ME: Download Dailymotion Videos, Vimeo, Facebook, Twitter and more!](http://savevideo.me/)

#### Direct message

https://twitter.com/messages/compose?
	recipient_id	user ID. Ex: 3309375033 for @AppleSupport

You can send to yourself a direct message.
Share this link on Twitter create a special twitter card with "Send a private message" link

#### Share an animation

GIF or Video

Note: you need to request approval to allow your domain to be allowed to use twitter card player. See [twitter card validator](https://dev.twitter.com/cards/types/player)

	<!-- page URL: http://gifboom.com/x/771600be -→
	<meta name="twitter:card"       content="player">
	<meta name="twitter:player"     content="https://gifboom.com/p/771600be">
	<meta name="twitter:player:width" content="480">
	<meta name="twitter:player:height" content="270">
	<meta name="twitter:player:stream" content="https://medias.gifboom.com/medias/0928a540746501330b2e723c91561e03.mp4">
	<meta name="twitter:player:stream:content_type" content="video/mp4; codecs=&quot;avc1.42E01E, mp4a.40.2&quot;">

	<meta name="twitter:account_id" content="1020383864" />
	<meta name="twitter:card" content="player">
	<meta name="twitter:title" content="The Simpsons GIF - Find &amp; Share on GIPHY">
	<meta name="twitter:creator" content="@giphy">
	<meta name="twitter:site" content="@giphy">
	<meta name="twitter:description" content="Discover &amp; Share this The Simpsons GIF with everyone you know. GIPHY is how you search, share, discover, and create GIFs.">
	<meta name="twitter:image:src" content="https://media3.giphy.com/media/fBEDuhnVCiP16/giphy-facebook_s.jpg?t=1">
	<meta name="twitter:image" content="https://media3.giphy.com/media/fBEDuhnVCiP16/giphy-facebook_s.jpg?t=1">
	<meta name="twitter:domain" content="giphy.com">
	<meta name="twitter:player" content="https://giphy.com/embed/fBEDuhnVCiP16/twitter/iframe">
	<meta name="twitter:player:width" content="435">
	<meta name="twitter:player:height" content="327">

- https://github.com/twitterdev/cards-player-samples
- [Player Card validator — Twitter Developers](https://dev.twitter.com/cards/types/player)
- https://twittercommunity.com/t/animated-gifs-are-currently-supported-in-twitter-cards-via-the-player-card-but-how/16825/6

#### Twitter shares

- http://opensharecount.com/count.json?source=bubble&url=URL
- http://public.newsharecounts.com/count.json?url=URL (detect new shares within 60 seconds)
- https://api.twitter.com/1.1/search/tweets.json?q=URL (with valid access token)
- https://counts.twitcount.com/button/?url=URL (html for share button + count)
- [OpenShareCount](http://opensharecount.com/)

#### Twitter share and like

- [Share URLs](#share-urls)
- Twitter buttons [Twitter Publish](https://publish.twitter.com/)

#### Stream

	https://syndication.twitter.com/timeline/likes?callback=console.log&dnt=false&screen_name=%{user-name}&suppress_response_codes=true&lang=fr
	https://syndication.twitter.com/timeline/profile?callback=console.log&dnt=false&screen_name=%{user-name}&suppress_response_codes=true&lang=fr
	https://syndication.twitter.com/timeline/list?callback=console.log&dnt=false&list_slug=%{user-list-id}&screen_name=%{user-name}&suppress_response_codes=true&lang=fr

	See https://twitter.com/settings/widgets/new/search?query=
	https://cdn.syndication.twimg.com/widgets/timelines/%{widget-id}?&callback=console.log&suppress_response_codes=true&lang=fr

	https://twitter.com/i/profiles/popup?screen_name=%{user-name}&wants_hovercard=true&lang=fr
	https://twitter.com/i/profiles/popup?user_id=%{user-id}&wants_hovercard=true&lang=fr

- [Reference Documentation — Twitter Developers](https://dev.twitter.com/rest/reference)
- (JS) https://github.com/jasonmayes/Twitter-Post-Fetcher
- (PHP) https://packagist.org/packages/j7mbo/twitter-api-php
- (JS) https://github.com/jublonet/codebird-js
- https://dev.twitter.com/resources/twitter-libraries
- https://mikerogers.io/2013/02/25/how-use-twitter-oauth-1-1-javascriptjquery.html
- https://umerpasha.wordpress.com/2013/06/13/c-code-to-get-latest-tweets-using-twitter-api-1-1/
 
	<?php
	$username = isset($_GET['screen_name']) ? $_GET['screen_name'] : 'twitter';// 'privateaccount'
	$page_content = @file_get_contents('https://twitter.com/' . urlencode($username) . '?lang=en');
	
	if(preg_match('/<input type="hidden" id="init-data" class="json-data" value="([^"]+)/', $page_content, $matches)){
		$data = json_decode(html_entity_decode($matches[1]), true);
		$profile_data = json_encode($data['profile_user']);
		header('Content-Type: application/json');
		echo $profile_data;
	}

	<?php
	
	define('TWITTER_PROFILE_VALUES', 6);
	$username = isset($_GET['screen_name']) ? $_GET['screen_name'] : 'twitter';
	$page_content = file_get_contents('https://twitter.com/' . urlencode($username) . '?lang=en');
	$profileKeys = array('tweets', 'following', 'followers', 'likes', 'lists', 'moments');
	$profileValues = array();
	$matchOffset = 80000;//skip first 80kB
	while(preg_match('/<span class="ProfileNav-value"[^>]*>([^<]+)/', $page_content, $matches, PREG_OFFSET_CAPTURE, $matchOffset) && count($profileValues) < TWITTER_PROFILE_VALUES){
		$fullPatternMatch = $matches[0];
		$matchOffset = $fullPatternMatch[1] + strlen($fullPatternMatch[0]);
		$firstCapGroupMatch = $matches[1];
		$value = $firstCapGroupMatch[0];
		$value = str_replace(',', '', $value);
		$lastChar = strtoupper($value[strlen($value) - 1]);// abbreviation
		$value = floatval($value);
		switch($lastChar) {
			case 'T':// Trillion, Tera-
				$value *= 1000;
			case 'B':// Billion
			case 'G':// Giga-
				$value *= 1000;
			case 'M':// Million, Mega-
				$value *= 1000;
			case 'K':// Kilo-
				$value *= 1000;
		}
		array_push($profileValues, $value);
	}
	
	$data = array(
		'screenName' => '',
		'fullName' => ''
	);
	$data += array_combine($profileKeys, $profileValues);
	echo '<pre>';
	echo json_encode($data);
	echo '</pre>';

#### GIF

Twitter has a limit of max 15 MB

#### Detect Twitter crawler

	if (
		strpos($_SERVER["HTTP_USER_AGENT"], 'Twitterbot/') !== false
	) {
		// it is probably Twitter's bot
	}
	else {
		// probably not
	}

- [Getting Started Guide | Twitter Developers](https://dev.twitter.com/cards/getting-started#crawling)

### Instagram

To add line breaks in post caption on iOS, copy the caption and past in Note app to add lines break or use a [text replacement](https://support.apple.com/en-us/HT207525)

To add a text replacement for add a line break you need macOS synchronized with the same iCloud account than the iOS device (on iOS you can't add text replacement with only spaces / line breaks). Copy a line return, then go at System Preferences > Keyboard > Text, add a shortcut.

**Note: You need to remove all space before the last line of previous paragraph (automatically added after each hashtags, user names or text replacements)**

### Pinterest

#### Pinterest share count

`http://api.pinterest.com/v1/urls/count.json?url=$1`, returns `receiveCount({"url":"$1","count":0})` (optional: parameter `callback` eg. `console.log`)

#### Pinterest share

- [Share URLs](#share-urls)
- http://business.pinterest.com/widget-builder/
- [Pinterest Developers](https://developers.pinterest.com/docs/widgets/pin-it/)

#### Detect Pinterest crawler

	if (
		strpos($_SERVER["HTTP_USER_AGENT"], 'Pinterest/') !== false
	) {
		// it is probably Twitter's bot
	}
	else {
		// probably not
	}

### LinkedIn

#### Linkedin share count

`http://www.linkedin.com/countserv/count/share?url=$1&format=json` returns `{"count":1304,"fCnt":"1,304","fCntPlusOne":"1,305","url":"$1"}`

#### LinkedIn share

Parameter `mini` is required and must be `true`

- [Share on LinkedIn | LinkedIn Developer Network](https://developer.linkedin.com/docs/share-on-linkedin)

### Reddit

#### Reddit share

- [reddit.com: boutons reddit](https://www.reddit.com/buttons/)

### Google Calendar

https://calendar.google.com/calendar/event?action=TEMPLATE&text=Title+part&details=Details+part&dates=20180524T190000/20180524T200000&location=Somewhere

- [Google Calendar render action Template parameter documentation - Stack Overflow](https://stackoverflow.com/questions/22757908/google-calendar-render-action-template-parameter-documentation)

### Google+

- [Share URLs](#share-urls)
- [Share  |  Google+ Platform for Web  |  Google Developers](https://developers.google.com/+/web/share/#sharelink)

#### Google+ share and like

- https://developers.google.com/+/web/+1button/

#### GIF

OK: 800 × 480 px (3.14 MB)

### Github

Get Markdown of Wiki:

For home page `https://github.com/msndevs/protocol-docs/wiki` go to `https://github.com/msndevs/protocol-docs/wiki/Home.md` (redirect to `https://raw.githubusercontent.com/wiki/msndevs/protocol-docs/Home.md`)
For other page `https://github.com/msndevs/protocol-docs/wiki/Authentication` go to `https://github.com/msndevs/protocol-docs/wiki/Authentication.md` (redirect to `https://raw.githubusercontent.com/wiki/msndevs/protocol-docs/Authentication.md`)

`https://api.github.com/repos/${USER}/${REPO}/commits/${BRANCH}`

	const REGEX_GIST_URL     = /^https?:\/\/gist\.github\.com\/.+?\/([0-9a-f]+)(?:\/([0-9a-f]+))?/i;
	const REGEX_RAW_GIST_URL = /^https?:\/\/gist\.githubusercontent\.com\/(.+?\/[0-9a-f]+\/raw\/(?:[0-9a-f]+\/)?.+\..+)$/i;
	
	/**
	Matches a GitHub raw URL.
	
	Captures:
	
	1.  Username
	2.  Repo
	3.  Ref
	4.  File path
	**/
	const REGEX_RAW_REPO_URL = /^https?:\/\/raw\.github(?:usercontent)?\.com\/(.+?)\/(.+?)\/(.+?)\/(.+)/i;
	
	/**
	Matches a GitHub repo URL.
	
	Captures:
	
	1.  Username
	2.  Repo
	3.  Ref
	4.  File path
	**/
	const REGEX_REPO_URL = /^https?:\/\/github\.com\/(.+?)\/(.+?)\/(?!releases\/)(?:(?:blob|raw)\/)?(.+?)\/(.+)/i;

#### Gist

- `https://gist.github.com/${USER}/${ID}`
- `https://gist.github.com/${USER}/${ID}.js` - Script to insert embedded gist
- `https://api.github.com/gists/${ID}`
- `https://api.github.com/gists/${ID}/${VERSION}`

- [Customizing GitHub Gists / Coder's Block](http://codersblock.com/blog/customizing-github-gists/)

### Stackexchange

Aka Stackoverflow, etc.

Short URLs:

	https://*.stackexchange.com/q/QUESTION_ID
	https://*.stackexchange.com/a/ANSWER_ID

### Voyage SNCF

- [generates urls to voyages-sncf.com to book trains with prefilled form items](https://gist.github.com/mmuman/5ed425a130e65224b184)
- https://oui.sncf

### Gitweb

Download snapshot: `http://<gitweburl>/gitweb.cgi?p=<repo>;a=snapshot;h=HEAD` Use `h=HEAD` or `h=` (path hash, from `ls-tree`)
Or use "snapshot" link

Example:
`https://gitorious.org/microsoft-qt-interop/microsoft-qt-interop?p=microsoft-qt-interop:microsoft-qt-interop.git;a=summary`

- [git - gitweb snapshot of sub-directory - Stack Overflow](https://stackoverflow.com/questions/14444593/gitweb-snapshot-of-sub-directory)
- https://github.com/git/git/blob/master/gitweb/gitweb.perl

### Scribd

	?start_page=n
	#page=n
	#full

### Wikipedia

- `http://en.wikipedia.org/w/api.php?action=query&prop=revisions&rvprop=content&titles=%s&format=json&callback=%s`
- https://www.wikidata.org/wiki/Special:ApiSandbox#action=query&format=json
- [Wikidata Query Service](https://query.wikidata.org/)

Exemple:

- List of countries
	- [Wikidata Query Service](https://query.wikidata.org/#%23List%20of%20present-day%20countries%20and%20capital%28s%29%0ASELECT%20DISTINCT%20%3Fcountry%20%3FcountryLabel%20%3Fcapital%20%3FcapitalLabel%0AWHERE%0A%7B%0A%20%20%3Fcountry%20wdt%3AP31%20wd%3AQ3624078%20.%0A%20%20%23not%20a%20former%20country%0A%20%20FILTER%20NOT%20EXISTS%20%7B%3Fcountry%20wdt%3AP31%20wd%3AQ3024240%7D%0A%20%20%23and%20no%20an%20ancient%20civilisation%20%28needed%20to%20exclude%20ancient%20Egypt%29%0A%20%20FILTER%20NOT%20EXISTS%20%7B%3Fcountry%20wdt%3AP31%20wd%3AQ28171280%7D%0A%20%20OPTIONAL%20%7B%20%3Fcountry%20wdt%3AP36%20%3Fcapital%20%7D%20.%0A%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20%7D%0A%7D%0AORDER%20BY%20%3FcountryLabel)
	- [Wikidata:SPARQL query service/queries/examples - Wikidata](https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service/queries/examples#Countries) - List of present-day countries and capital(s)
	- [Research in programming Wikidata/Countries - Wikiversity](https://en.wikiversity.org/wiki/Research_in_programming_Wikidata/Countries)

### SlideShare

Permalink to a slide number: `http://www.slideshare.net/.../presentation-name` → `http://www.slideshare.net/.../presentation-name/10` for the slide 10

- [Friday Tip: create a permalink to a specific slide](https://blog.slideshare.net/2011/07/29/friday-tip-create-a-permalink-to-a-specific-slide)

### CONTENTdm

- [Download full size image from OLCL's CONTENTdm http:\/\/www.contentdm.org\/]https://gist.github.com/mems/4739515)

### Fashion Anthology bookmarlet

Show all fullres images (without watermark, + inaccessible ones) of a Fashion Anthology gallery in one page and without require any account 

Filename pattern `%designer_name% %collection% %year% %image_number%.jpg`

	javascript:var t=document.title.split(/\s+\|\s+/).slice(1).join(" ");$("head").append("<style>.pictures{margin:0px calc((100vw - 993px) / -2);padding:10px;display:flex;flex-wrap:wrap;}.picture-wrap{width:400px;flex-grow:1;box-sizing:border-box;padding:10px;}.picture{width: 100%;}</style>");var p=$(".bigphoto");var s=p.find("img").prop("src").replace(/\d{3}_m.jpg/, "");p.remove();var r=$("<div class='pictures'/>");var e=function(){$(this).parent().remove()};for(var i=1;i<=999;i++){var a=s+("000"+i).slice(-3)+".jpg";r.append($("<a class='picture-wrap'/>").attr("download", t+" "+i+".jpg").prop("href", a).append($("<img class='picture' src='#'>").error(e).prop("src", a)))};$(".allphotos").replaceWith(r);void(0);

- https://gist.github.com/mems/5a87941e00c8c15954ce

### Apple

#### Apple live stream URL 

Found the Apple live stream URL

1. Open `http://www.apple.com/live/` which redirect to something like `http://www.apple.com/live/2015-june-event/`
2. Find a loaded script like: `/live/2015-june-event/scripts/2015-june-event.built.js`
3. Open this script and search `p.events-delivery.apple.com.edgesuite.net`. You find something like `http://p.events-delivery.apple.com.edgesuite.net/15pijbnaefvpoijbaefvpihb06/js_files/event`
4. append to it `/url.json` (details: host + path + `url.json`)
5. Open the generated URL
6. Found an URL like `http://p.events-delivery.apple.com.edgesuite.net/15pijbnaefvpoijbaefvpihb06/m3u8/hls_mvp.m3u8`

Now you can watch it in VLC or any other videoplayer that support M3U and MP4(H.264+AAC)!

Previous Apple's website:

1. [...]
2. Find a loaded script like: `http://p.events-delivery.apple.com.edgesuite.net/15pijbnaefvpoijbaefvpihb06/js_files/event/url.js`
3. Grab the correct URL

- https://gist.github.com/mems/d54ad804d8d8d17d0011

### Online cursor editor

Add support of load an image in http://www.rw-designer.com/online-cursor-editor tool (Make CUR file) 

	/*
	Make CUR file using online editor, with basic support of load an image
	http://www.rw-designer.com/online-cursor-editor
	
	Require image file to base64 string convertion tool like:
	http://www.motobit.com/util/base64-decoder-encoder.asp
	*/
	
	//------------
	
	// Define draw position
	var × = 0;
	var y = 0;
	
	// Define canvas size 32 × 32
	var canvasWidth = 32;
	var canvasHeight = 32;
	
	var format = "image/png";
	// Define image base64
	var data = //"iVBORw0KGgoAAAANSUhEUgAAAAsAAAAaCAYAAABhJqYYAAAAbUlEQVR42mNgQAOeC3b8h2EGQmBU8ajioawYKLgJWQEevAmkWAGIvxJQCJJXgJleSUBxJbJTWIH4Gg6F14GYDd3tDkD8D00hiO+IKyQWoylegi/YxIH4PVQhiJYgFM5ZUMVZxEQKMxBPB9HocgARnh3leFIWmgAAAABJRU5ErkJggg=="
	//"iVBORw0KGgoAAAANSUhEUgAAAAsAAAAaCAYAAABhJqYYAAAAbUlEQVR42mNgQAN6rVb/YZiBEBhVPKp4KCsGCm5CVoAHbwIpVgDirwQUguQVYKZXElBciewUViC+hkPhdSBmQ3e7AxD/Q1MI4jviConFaIqX4As2cSB+D1UIoiUIhXMWVHEWMZHCDMTTQTS6HABLqs2uDLgrlgAAAABJRU5ErkJggg=="
	//"iVBORw0KGgoAAAANSUhEUgAAAAsAAAAaCAYAAABhJqYYAAAAbUlEQVR42mNgQAOv0zj+wzADITCqeFTxUFYMFNyErAAP3gRSrADEXwkoBMkrwEyvJKC4EtkprEB8DYfC60DMhu52ByD+h6YQxHfEFRKL0RQvwRds4kD8HqoQREsQCucsqOIsYiKFGYing2h0OQAUJ/3GEXDEHgAAAABJRU5ErkJggg=="
	"iVBORw0KGgoAAAANSUhEUgAAAAsAAAAaCAYAAABhJqYYAAAAbUlEQVR42mNgQAP9Zi//wzADITCqeFTxUFYMFNyErAAP3gRSrADEXwkoBMkrwEyvJKC4EtkprEB8DYfC60DMhu52ByD+h6YQxHfEFRKL0RQvwRds4kD8HqoQREsQCucsqOIsYiKFGYing2h0OQA5PiOv+GamsAAAAABJRU5ErkJggg=="
	//"iVBORw0KGgoAAAANSUhEUgAAAAsAAAAaCAYAAABhJqYYAAAAbUlEQVR42mNgQAOH12r/h2EGQmBU8ajioawYKLgJWQEevAmkWAGIvxJQCJJXgJleSUBxJbJTWIH4Gg6F14GYDd3tDkD8D00hiO+IKyQWoylegi/YxIH4PVQhiJYgFM5ZUMVZxEQKMxBPB9HocgBlExs5LfZeRAAAAABJRU5ErkJggg=="
	
	
	//------------
	//------------
	
	var img = document.createElement("img");
	img.src = "data:" + format + ";base64," + data;
	
	var canvas = document.createElement("canvas");
	canvas.width = canvasWidth;
	canvas.height = canvasHeight;
	
	var ctx = canvas.getContext("2d");
	
	ctx.drawImage(img, x, y);
	
	var imageData = ctx.getImageData(0, 0, canvasWidth, canvasHeight);
	var imageWidth = imageData.width;
	var imageHeight = imageData.height;
	var rawPixels = imageData.data;
	var numPixels = imageWidth * imageHeight;
	var argb;
	for(var i = 0; i < numPixels; i++){
		//32bits RGBA to ARGB
		argb = rawPixels[i * 4] << 16;//R
		argb |= rawPixels[i * 4 + 1] << 8;//G
		argb |= rawPixels[i * 4 + 2];//B
		argb |= rawPixels[i * 4 + 3] << 24;//A
		OCE_replacepixel(i, argb);
	}

- https://gist.github.com/mems/5338017

### App animations

First exec this in WebDev console for each page, copy in clipboard the iframes src of each videos + title + keywords

	copy(JSON.stringify(Array.from(document.querySelectorAll("article")).map(article => [article.querySelector("iframe").src, /<a[^>]*>([^<]+)/.exec(article.querySelector("textarea").value)[1], article.querySelector(".cat").textContent])))

Go to https://videos.sproutvideo.com/embed/189bdbb01e1ce7c790/98b77e706be88310, open WebDev console and exec:

	var videos = [
		/*PAST HERE the content of all pages*/
	];
	var output = "";
	// Decode function using XOR with key `t`
	function d(e, t) {
		var i, n, s, r, o, a, l, u;
		for (o = [], i = '', n = 0, u = s = 1; 255 >= s; u = s += 1) o[String.fromCharCode(u)] = u;
		for (l = r = 0, a = e.length - 1; a >= r; l = r += 1) i += String.fromCharCode(o[e.substr(l, 1)] ^ o[t.substr(n, 1)]),
		n = n < t.length ? n + 1 : 0;
		return i.replace(/[^\x20-\x7E]+/g, '')
	}
	var count = 0;
	var total = videos.length;
	for(let i = 0; i < total; i++){
		let video = videos[i];
		let xhr = new XMLHttpRequest();
		xhr.addEventListener("load", event => {
			let data = event.target.response.querySelector("script").textContent.slice(11, -2)
			let config = JSON.parse(atob(data));
			let url = d(unescape(config.hdvu), config.host);
			output += `		<file name="${video[1]}">
				<resources>
					<url type="http">${url}</url>
				</resources>
			</file>";
		
			if(++count >= total){
				copy(`<?xml version="1.0" encoding="UTF-8"?>
				<metalink version="3.0" xmlns="http://www.metalinker.org/">
					<files>
						${ouput}
					</files>
				</metalink>`);
				alert("You can now past clipboard content in a new file.")
			}
		})
		xhr.responseType = "document"
		xhr.open("GET", video[0])
		xhr.send()
	}

- [Download all videos from http://www.appanimations.com/](https://gist.github.com/mems/7e00ba82012d668d0164)

### ccMixter

[ccMixter](http://ccmixter.org/)

	copy(Array.from(document.querySelectorAll(".upload_info[about]")).map(info => info.getAttribute("about").trim()).join("\n"))

### Wayback Machine

`robots.txt` is retroactive

`http://web.archive.org/cdx/search/cdx?url=${domain}&matchType=${matchType}&output=json&fl=timestamp,original&fastLatest=true&filter=statuscode:200&collapse=original` `&from=${from}&to=${to}`
`http://web.archive.org/web/${timestamp}id_/${originalurl}`

- [Wayback Machine APIs | Internet Archive](https://archive.org/help/wayback_api.php)
- [Retrieving Snapshots · Internet Archive](https://archive.readme.io/docs/website-snapshots)
- [Internet Archive Frequently Asked Questions](http://archive.org/about/faqs.php)
- [hartator/wayback-machine-downloader: Download an entire website from the Wayback Machine.](https://github.com/hartator/wayback-machine-downloader/) - [Recovering missing content from the Internet Archive](https://simonwillison.net/2017/Oct/8/missing-content/)
- [waybackmachine.sh](https://gist.github.com/lazanet/872f88c9874e4a7a78fd)
- [Heritrix - Heritrix - IA Webteam Confluence](https://webarchive.jira.com/wiki/display/Heritrix)
- [Stop Throwing Away Your Content | Adrian Roselli](http://adrianroselli.com/2016/07/stop-throwing-away-your-content.html)
- [Surprisingly, the default for the Internet Archive is Don’t Archive](http://cogdogblog.com/2016/06/dont-archive/)

### Blog export

Save the RSS / Atom

- [Migration Overblog vers Blogger ou Wordpress - Iv Oam Blog](https://iv-oam.blogspot.fr/2013/08/sauvegarde-overblog.html)
- [blogtowp download | SourceForge.net](https://sourceforge.net/projects/blogtowp/) - Ruby script `ruby dialog.rb`
	Support only the old version of blog-spot
	See [Importer les commentaires d'un blog sous Wordpress (4) - Reedition - nouvelles fonctionnalités + Haut et Fort - jrcourtois: le blog](http://blog.jrcourtois.net/post/2009/07/30/Importer-les-commentaires-d-un-blog-sous-Wordpress-4)
	See [Sauvegarde Erog et export vers Wordpress (voire vers Blogger) - Iv Oam Blog](https://iv-oam.blogspot.fr/2013/02/export-d-vers-wordpress-voire-vers.html)
	But get only posts have a category:
	
	- execute first the tool (will create `files/index.html` and empty file `TheBigFile.xml`)
	- edit files/index.html to add `categorie-0.html">Uncategorized</a>`
- [Back up, import, or delete your blog - Blogger Help](https://support.google.com/blogger/answer/41387?hl=en)
- `httrack myblog.com/faq "-admin.over-blog.com/*" "-www.over-blog.com/*" -O "My blog" -s0` - add `--update` to update only

### RFC

- https://datatracker.ietf.org/doc/search/?rfcs=on&name=%s (where `%s` is 2616 for RFC 2616)
- [IETF | RFCs](https://www.ietf.org/standards/rfcs/)
- [📄 HTTP Documentation](https://httpwg.org/specs/)

## Browsers extension

### Web Extensions

Chrome, Firefox, Edge

### Safari Extensions

#### Safari App Extension

- [Safari App Extension | Apple Developer Documentation](https://developer.apple.com/documentation/safariservices/safari_app_extensions)

#### Safari Extension

Depreciated by Safari 12

Use [xar](https://en.wikipedia.org/wiki/Xar_%28archiver%29)

	xar -x -f XXXXX.safariextz

Ex: https://safari-extensions.apple.com/details/?id=com.diigo.safari.awesomescreenshot-5DXNM3K2CT

	(new URL(window.ex.render.install_link(window.ex.data.getItemByID((new URL(location)).searchParams.get("id"))), document.baseURI)).href

## Third parties

> Don't trust your third parties

See also [Third parties webperf](#third-parties-webperf)

Comments services alternatives:

- [Replacing Disqus with Github Comments · Gazoo.vrv](http://donw.io/post/github-comments/)
- [Comments - Social Plugins](https://developers.facebook.com/docs/plugins/comments/)

### Website JS plugins

To isolate a third party script (or DOM access, geolocation, modal APIs, etc.), use:

- iframe with a cross origin (third party origin or null), ex: iframe with sandbox attribute but without `allow-same-origin`
- a virutal machine like [QuickJS](https://bellard.org/quickjs/) or [Duktape](https://github.com/svaarala/duktape) or [any other JS engine](https://github.com/GoogleChromeLabs/jsvu#supported-engines-per-os) (that could be cross-compiled to WebAssembly)
- use the [Realm API](https://www.npmjs.com/package/realms-shim) (similar to `with(proxy){}`)

See also:

- [How to build a plugin system on the web and also sleep well at night](https://www.figma.com/blog/how-we-built-the-figma-plugin-system/)
- [An update on plugin security](https://www.figma.com/blog/an-update-on-plugin-security/)
- [Realms-shim Security Updates - Agoric](https://agoric.com/realms-shim-security-updates/)
- [Play safely in sandboxed IFrames - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/security/sandboxed-iframes/)
- [Sandboxing JavaScript - Zendesk Engineering - Medium](https://medium.com/zendesk-engineering/sandboxing-javascript-e4def55e855e)
- [Loading Third-Party JavaScript  |  Web Fundamentals  |  Google Developers](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/loading-third-party-javascript#avoid_scripts_that_pollute_the_global_scope) - "Be sure to conduct careful audits of the third-party scripts you load to ensure they’re being good actors."

### oEmbed

- [oEmbed](https://oembed.com/)
- [oEmbed - Wikipedia](https://en.wikipedia.org/wiki/OEmbed)
- [Programmatically Discovering Sharing Code With oEmbed — Smashing Magazine](https://www.smashingmagazine.com/2019/11/programmatically-discovering-sharing-code-oembed/)
- [How To Build an oEmbed Integration for Your Startup, and Why It’s Necessary](https://blog.ycombinator.com/how-to-build-an-oembed-integration-for-your-startup-and-why-its-necessary/)
- [oEmbed Provider API | Developer Resources](https://developer.wordpress.com/docs/oembed-provider-api/)

## Firefox Reader view

Based on Readability

- [QA/Reader view - MozillaWiki](https://wiki.mozilla.org/QA/Reader_view)
- https://github.com/mozilla/readability/blob/c3c91a739beab6fd067404cd7610f6d64f53ad5a/Readability.js#L1721
- [javascript - How Does Firefox Reader View Operate (FF version 38.0.5) - Stack Overflow](https://stackoverflow.com/questions/30661650/how-does-firefox-reader-view-operate-ff-version-38-0-5/)
- [mozilla-release mozilla/toolkit/components/reader/ReaderMode.jsm](https://mxr.mozilla.org/mozilla-release/source/toolkit/components/reader/ReaderMode.jsm)
- [How to disable firefox's reader view from my website? - Stack Overflow](https://stackoverflow.com/questions/30615447/how-to-disable-firefoxs-reader-view-from-my-website)

## "Request Desktop Site"

On mobile browsers

## Web Application

- [Script to create custom shortcuts on the iOS springboard. Check it out at: http://dev.fokkezb.nl/shortcutter](https://gist.github.com/FokkeZB/5899387) - Generate data URI HTML document (to bookmark), allow to start native apps with custom arguments
- [Shortcuts JS](https://shortcuts.fun/)

## Open native application

- [ios - How to check if an app is installed from a web-page on an iPhone? - Stack Overflow](https://stackoverflow.com/questions/13044805/how-to-check-if-an-app-is-installed-from-a-web-page-on-an-iphone)
- [ios - Is it possible to register a http+domain-based URL Scheme for iPhone apps, like YouTube and Maps? - Stack Overflow](https://stackoverflow.com/questions/1108693/is-it-possible-to-register-a-httpdomain-based-url-scheme-for-iphone-apps-like)
- [URL schemes for iOS and Android (1/2)](https://gist.github.com/FokkeZB/6340484) - [URL schemes for iOS and Android (1/2) | Fokke Zandbergen](https://fokkezb.nl/2013/08/26/url-schemes-for-ios-and-android-1/)
- [URL schemes for iOS and Android (2/2)](https://gist.github.com/FokkeZB/6635236) - [URL schemes for iOS and Android (2/2) | Fokke Zandbergen](https://fokkezb.nl/2013/09/20/url-schemes-for-ios-and-android-2/)

## Viewport size

| 							 | iPhone 4/4s			 | iPhone 5/5c/5s/SE	 | iPhone 6… 		 | iPhone 6… Plus		 | iPad pro 12.9		 | iPad pro 9.7			 |
| -------------------------- | --------------------- | --------------------- | ----------------- | --------------------- | --------------------- | --------------------- |
| Screen Size[1]			 | 	320 × 480 pt		 | 320 × 568 pt			 | 375 × 667 pt		 | 414 × 736 pt			 | 1366 × 1024 pt		 | 1024 × 768 pt		 |
| Rendered Pixels			 | 	640 × 960 (@2x)		 | 640 × 1136 (@2x)		 | 750 × 1334 (@2x)	 | 1242 × 2208 (@3x)	 | 2732 × 2048 (@2x)	 | 2048 × 1536 (@2x)	 |
| Physical Pixels			 | 	640 × 960			 | 640 × 1136			 | 750 × 1334		 | 1080 × 1920			 | 2732 × 2048			 | 2048 × 1536			 |
| Pixels Per Inch (PPI)		 | 326					 | 326					 | 326				 | 401					 | 264					 | 264					 |
| Browser viewport			 | -					 | -					 | -				 | -					 | -					 | -					 |
| - Portrait				 | 	-					 | -					 | -				 | -					 | -					 | -					 |
| 	* normal[2]				 | 320 × 372 px			 | 320 × 460 px			 | 375 × 559 px		 | 414 × 628 px			 | ?					 | ?					 |
| 	* minimal[3]			 | 320 × 440			 | 320 × 528			 | 375 × 627		 | 414 × 696			 | ?					 | ?					 |
| 	* fullscreen[4]			 | 320 × 460			 | 320 × 548			 | 375 × 647		 | 414 × 716			 | ?					 | ?					 |
| - Landscape 				 | -					 | -					 | -				 | -					 | -					 | -					 |
| 	* normal[2]				 | 480 × 212 px			 | 568 × 212 px			 | 667 × 267 px		 | 736 × 306 px			 | ?					 | ?					 |
| 	* minimal[3]			 | 480 × 280			 | 568 × 280			 | 667 × 335		 | 736 × 374			 | ?					 | ?					 |
| 	* fullscreen[4]			 | 480 × 300			 | 568 × 300			 | 667 × 355		 | 736 × 394			 | ?					 | ?					 |

1. JS: `screen.[height|width]`; CSS: `device-width`, `device-height`
2. normal-ui (with normal browser navigation bars) JS: `window.inner[Height|Width]`; CSS: `width`, `height`
3. minimal-ui (with the small browser navigation bars) JS: `window.inner[Height|Width]`; CSS: `width`, `height`
4. fullscreen (without any browser chrome for a web app, only status bar if any) JS: `screen.avail[Height|Width]`; CSS: `width`, `height`

- [iOS Resolutions and screen sizes](http://ios-resolution.com/)
- [mydevice.io, your device screen informations](http://www.mydevice.io/)
- [iPhone — Wikipedia](https://en.wikipedia.org/wiki/IPhone)
- [iPhone 6 Screen Size and Mobile Design Tips](http://www.kylejlarson.com/blog/2015/iphone-6-screen-size-web-design-tips/)
- [CSS Media Queries for iPads & iPhones | Stephen Gilbert](http://stephen.io/mediaqueries/)
- [Device and Viewport Size In JavaScript](http://ryanve.com/lab/dimensions/)
- [Safari on iOS 7 and HTML5: problems, changes and new APIs | Breaking the Mobile Web](http://www.mobilexweb.com/blog/safari-ios7-html5-problems-apis-review)
- [Media Queries for Standard Devices | CSS-Tricks](https://css-tricks.com/snippets/css/media-queries-for-standard-devices/)
- [Devices — Facebook Design Resources](http://facebook.github.io/design/devices.html)
- [The Ultimate Guide To iPhone Resolutions](http://www.paintcodeapp.com/news/ultimate-guide-to-iphone-resolutions)

## Law and privacy legislations

Aka GDPR or EU Cookie Law

See Do Not Track https://www.eff.org/dnt-policy [`navigator.doNotTrack`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/doNotTrack) https://en.wikipedia.org/wiki/Do_Not_Track

- [Cookies - Comment vraiment respecter la loi ? - Korben](http://korben.info/respecter-loi-cookies-site.html)
- [Cookies - European commission](http://ec.europa.eu/ipg/basics/legal/cookies/index_en.htm)
- [5 steps to make sure you are compliant with the EU Cookie Directive | Reason Digital](http://reasondigital.com/advice-and-training/5-steps-to-make-sure-you-are-compliant-with-the-eu-cookie-directive/)
- [Europe is planning to finally scrap those annoying cookie pop-ups on websites](http://www.businessinsider.fr/us/europe-plans-remove-cookie-pop-ups-banners-websites-leaked-law-draft-consent-2016-12/)

## App Download Interstitials 

- [Google+: A case study on App Download Interstitials](http://googlewebmastercentral.blogspot.ca/2015/07/google-case-study-on-app-download-interstitials.html)
- [Mobile-friendly web pages using app banners](http://googlewebmastercentral.blogspot.ca/2015/09/mobile-friendly-web-pages-using-app.html)

## App Association

### App Install Banner

	<meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL">

	<link rel="manifest" href="/manifest.json">

	{
		"prefer_related_applications": true,
		"related_applications": [
			{
				"platform": "play",
				"id": "com.google.samples.apps.iosched"
			}
		]
	}

- [Promoting Apps with Smart App Banners](https://developer.apple.com/library/mac/documentation/AppleApplications/Reference/SafariWebContent/PromotingAppswithAppBanners/PromotingAppswithAppBanners.html)
- [Increasing Engagement with Web App Install Banners  |  Web  |  Google Developers](https://developers.google.com/web/updates/2015/03/increasing-engagement-with-app-install-banners-in-chrome-for-android#native)

### Android App Links

Android App Link:
https://<domain>/.well-known/assetlinks.json

- [Handling Android App Link  |  Android Developers](https://developer.android.com/training/app-links/)
- [Verify Android App Link  |  Android Developers](https://developer.android.com/training/app-links/verify-site-associations#the-difference)
- http://example.digitalassetlinks.org/.well-known/assetlinks.json

### Apple App Site Association

Aka AASA or Universal Links

https://<domain>/apple-app-site-association or https://<domain>/.well-known/apple-app-site-association without redirect (200 OK only)

Fetch/apdated when (no expired):

- app install
- app update

Can't use MITM to handle/override association (certificate pinning)

- [security - Are Universal Link cached in iOS? Do they work offline? - Stack Overflow](https://stackoverflow.com/questions/41305334/are-universal-links-cached-in-ios-do-they-work-offline/41305871#41305871)
- [App Search Programming Guide: Support Universal Links](https://developer.apple.com/library/archive/documentation/General/Conceptual/AppSearch/UniversalLinks.html)
- [Universal Link – A Few Thing to be Prepared for – Shine Solution Group](https://shinesolutions.com/2017/06/15/universal-linking-a-few-things-to-be-prepared-for/)

## Dummy and placeholder media

Aka Video test pattern, test image, sample image

See [Sample files](Sample files)

16/9 image:

	data:image/svg+xml,%3Csvg xmlns='w3.org/2000/svg' viewBox='0 0 16 9' width='16' height='9'%3E%3C/svg%3E
 
	<svg version="1.1" xmlns="http://www.w3.org/2000/svg">
		<g stroke="purple" stroke-width="2">
			<line x1="0" y1="0" x2="100%" y2="100%"/>
			<line x1="100%" y1="0" x2="0" y2="100%"/>
			<rect x="0" y="0" width="100%" height="100%" fill="none" stroke-width="4" />
		</g>
	</svg>

	<svg version="1.1" xmlns="http://www.w3.org/2000/svg">
		<g stroke="purple" stroke-width="2">
			<line x1="14.64%" y1="14.64%" x2="85.36%" y2="85.36%"/>
			<line x1="85.36%" y1="14.64%" x2="14.64%" y2="85.36%"/>
			<ellipse cx="50%" cy="50%" rx="50%" ry="50%" fill="none" stroke-width="4"/>
		</g>
	</svg>

## Web fonts

See [CSS - Font web safe](CSS#font-web-safe)

## Favicon

For icons, use a large one 180×180 icon for iOS and Android

Some browsers usally try to get the following resource: `/favicon.ico`

- 	convert favicon.png -background none -resize 256×256 -define icon:auto-resize="256,128,96,64,48,32,16" favicon.ico
- [Thumbnails -- IM v6 Examples](http://www.imagemagick.org/Usage/thumbnails/#favicon)
- [audreyr/favicon-cheat-sheet: Obsessive cheat sheet to favicon sizes/types. Please contribute! (Note: this may be in flux as I learn new things about favicon best practices.)](https://github.com/audreyr/favicon-cheat-sheet)
- [FavIcon from Pics -- free favicon.ico for your website (animated, static, text, iPod icons)](http://favicon.htmlkit.com/favicon/)
- [How iOS scales the Apple Touch icon - Favicon's blog](https://realfavicongenerator.net/blog/how-ios-scales-the-apple-touch-icon/)
- [How Android Chrome scales down icons - Favicon's blog](https://realfavicongenerator.net/blog/how-android-chrome-scales-down-icons/)
- [Favicon Generator for all platforms: iOS, Android, PC/Mac...](http://realfavicongenerator.net/)
- https://github.com/RealFaviconGenerator/realfavicongenerator/issues/211
- https://github.com/GoogleChrome/lighthouse/issues/291#issuecomment-219074630
- [Favicon — Wikipedia](https://en.wikipedia.org/wiki/Favicon)

## Browsers version fragmentation

Version penetration

- [iOS 8 adoption](https://mixpanel.com/trends/#report/ios_8/from_date:-360,report_unit:day,to_date:0)
- [iOS 9 adoption](https://mixpanel.com/trends/#report/ios_9/from_date:-360,report_unit:day,to_date:0)
- [iOS 10 adoption](https://mixpanel.com/trends/#report/ios_10/from_date:-360,report_unit:day,to_date:0)
- [iOS Versions](https://mixpanel.com/trends/#report/ios_frag/from_date:0,to_date:0)
- [Android OS Adoption](https://mixpanel.com/trends/#report/android_os_adoption)
- [Android OS Versions](https://mixpanel.com/trends/#report/android_frag/from_date:0,to_date:0)
- [iOS Version Stats - David Smith](https://david-smith.org/iosversionstats/)

Browser support

- [Stay up-to-date with Internet Explorer - IEBlog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/ie/archive/2014/08/07/stay-up-to-date-with-internet-explorer.aspx)
- [Download The Total Economic Impact Of Microsoft Internet Explorer 11 from Official Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=45907)
- [IE11 Upgrade – Business, IT Pro Benefits | TechNet](https://technet.microsoft.com/en-us/ie/mt163707)
- [Microsoft Lifecycle Support policy for Internet Explorer](https://support.microsoft.com/en-us/lifecycle#gp/Microsoft-Internet-Explorer)

## Links and alternate

Canonical URL = the preferred URL (same document content, aka duplicated content)
Alternate URL = other version of this canonicalized document (mobile or other lang)

For languages alternate, each canonicalized document must include the list of all languages available, even itself

**Use alternate URL only for canonicalzed documents**

![hreflang and canonical links relations](http://www.rebelytics.com/wp-content/uploads/2015/06/hreflang-canonical.jpg)

On desktop:

	<link rel="alternate" media="only screen and (max-width: 640px)" hreflang="en-gb" href="http://m.example.com/page">

or via http header:

	Link: <http://m.example.com/page>; rel="alternate"; hreflang="en-gb"; media="only screen and (max-width: 640px)"

And on mobile:

	<link rel="canonical" href="http://www.example.com/page">

For HTTPS page (on `http://www.example.com/page`):

	<link rel="canonical" href="https://www.example.com/page">

- `x-default`
- [Use canonical URLs - Search Console Help](https://support.google.com/webmasters/answer/139066)
- [Use hreflang for language and regional URLs - Search Console Help](https://support.google.com/webmasters/answer/189077)
- [Separate URLs  |  Mobile Friendly Websites  |  Google Developers](https://developers.google.com/webmasters/mobile-sites/mobile-seo/separate-urls)
- [RFC 5988 - Web Linking](https://tools.ietf.org/html/rfc5988)
- [An Entity Header for Linked Resources](http://www.w3.org/Protocols/9707-link-header.html)
- [Official Google Webmaster Central Blog: 5 common mistakes with rel=canonical](https://webmasters.googleblog.com/2013/04/5-common-mistakes-with-relcanonical.html)
- [hreflang and canonical: How to use them together](http://www.rebelytics.com/hreflang-canonical/)
- [Set your preferred domain (www or non-www) - Search Console Help](https://support.google.com/webmasters/answer/44231?hl=en)

## Date

use ISO 8601 in JSON

	Date#toJSON()

	date('c', time());
	$date→format(DateTime::ATOM/*use it instead of ISO8601*/);

	$date = new DateTime("2010-07-05T06:00:00Z");
	// To offset with a timezone:
	$date→setTimeZone(new DateTimeZone("Europe/Amsterdam");

- [javascript - The "right" JSON date format - Stack Overflow](https://stackoverflow.com/questions/10286204/the-right-json-date-format/15952652#15952652)
- [ISO 8601 - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/ISO_8601)
- [PHP: DateTime - Manual](http://php.net/manual/en/class.datetime.php)
- [PHP DateTime::createFromFormat doesn't parse ISO 8601 date time - Stack Overflow](https://stackoverflow.com/questions/4411340/php-datetimecreatefromformat-doesnt-parse-iso-8601-date-time)

## Troubleshooting

- [Content blocking](#content-blocking)
- safe browsing / ad blocker issues:
	- `banner.jpg`, `ads.js` and `analytics.js`, `sponsor`
	- analytics can even fails
	- some HTML element like images or video with keywords like "publicité" (in URL or title) don't appears on some browsers
	- Firefox with the Tracking Protection block the Facebook SDK in private mode (by default)
	- Adblock block IDs starts with `ad`
	- [Class and ID to avoid because of AdBlock](https://gist.github.com/spyesx/42fe84c0ef757d1c38a4) https://github.com/easylist/easylist (IDs start with `###`, classes start with `##.`)
	- [Remove hint on beacon.js as it's apparently a bad name · ntzwrk/beacon@17c2042](https://github.com/ntzwrk/beacon/commit/17c20422b2912bed0c414093ebaaf672e1ea2a57)
	- [Don't use "ad" as a class · Issue #139 · rtsao/styletron](https://github.com/rtsao/styletron/issues/139)
	- [Avoid the Twitter icon being blocked by AdBlock · whatwg/whatwg.org@20beccb](https://github.com/whatwg/whatwg.org/commit/20beccbcd71cd3c1d242bdd2043f1feb1cf7c67a)
	- [Tim on Twitter: "Next.js uses nanoid, it’s a really small library to generate random ids. In this case the random id started with “ad_” which is on the Adblock list as “/static/ad_”, likeliness that another id like that will be generated is very low. We’ve patched it to be sure!… https://t.co/3wWnjrBN5N"](https://twitter.com/timneutkens/status/1112852174952939520)
	- Opera and UC Browser include ad blockers
- some pages or files are not display correctly. Do you use the `Vary` header to define on which request headers you use to deliver content (often `Accept-Encoding`, `User-Agent` or `Cookie`)
- [Proxies can transform content](#proxies-can-transform-content)
- scripts or content not executed/loaded because CSP don't allow it
- [Redirects can break `POST`](#redirects-can-break-post)

## Cross domain & integrity

- `integrity` `<script>` and `<link>` attribute
- `crossorigin` `<script>`, `<img>` attribute
- `noreferrer`
- `noopener`
- `X-Frame-Options` header (depreciated)
- `Content-Security-Policy` header

See [XSS and injection](Security#xss-and-injection)

### Subresource checksum

JavaScript:

	let source = 'alert("Hello, world.");';//string
	let algo = "sha256";//"sha256" / "sha384" / "sha512"
	const utf8Encoder = new TextEncoder();
	let sourceBytes = utf8Encoder.encode(source);
	const algos = {
		sha256: "SHA-256",
		sha384: "SHA-384",
		sha512: "SHA-512"
	};
	crypto.subtle.digest(algos[algo], sourceBytes).then(valueBuffer => {
		let hashBytes = new Uint8Array(valueBuffer);
		let valueChars = hashBytes.reduce((chars, byte) => (chars += String.fromCharCode(byte), chars), "");// to UTF-8
		let base64Value = btoa(valueChars);
		return "'" + algo + "-" + base64Value + "'";// "'" hash-algo "-" base64-value "'"
	}).then(checksum => console.log(checksum))

PHP:

	<?php
	$script = 'alert("Hello, world.");';
	$algo = 'sha256';// 'sha384' // 'sha512'
	$script_hash = base64_encode(hash($algo, $script, true));
	header('Content-Security-Policy: default-src \'self\'; script-src \'self\' \''.$algo.'-'.$script_hash.'\'');// sha256-qznLcsROx4GACP2dm0UCKCzCG+HiZ1guq6ZZDob/Tng= or sha512-YWIzOWNiNzJjNDRlYzc4MTgwMDhmZDlkOWI0NTAyMjgyY2MyMWJlMWUyNjc1ODJlYWJhNjU5MGU4NmZmNGU3OAo=
	echo '<script>'.$script.'</script>';

Command line (sh, openSSL):

	echo sha256-$(echo -n 'alert("Hello, world.");' | openssl dgst -sha256 -binary | openssl enc -base64 | tr -d '\n')

**Be carefull of (significant) spaces, quotes, etc. The hash could be different.**

- [Generating Subresource Integrity Checksums - Tenzer.dk](https://tenzer.dk/generating-subresource-integrity-checksums/)

### Bypass cross domain control

If your JS need a resource but it's disallow but the third party (does not allow with Access Control headers)

**Always filter which URL/domain you allow.** Else some evil people could use your proxy for illegal activity, etc.

- reverse proxy
- `http://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20html%20where%20url%3D%27http%3A%2F%2Fbbc.co.uk%27%0A&format=json` `select * from html where url='http://bbc.co.uk'`
- JSONP (previous example support `&callback=foo`)
- https://github.com/Athlon1600/php-proxy

**Note: CSP can block it.**

## Server logging

- [Chrome Logger - Server side application debugging](https://craig.is/writing/chrome-logger) - use `X-ChromeLogger-Data: jsonbase64data`
- [eshengsky/ServerLog: A simple, practical, and innovative Node.js log library that enables you to view logs in Chrome dev tools.](https://github.com/eshengsky/ServerLog) - use `X-Server-Log-Data`
- [Server Side Event](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events)

## Server timing

Aka Server Timing API

	Server-Timing: cache;desc="Cache Read";dur=23.2,fs;dur=600;desc="File System",cpu;dur=1230;desc="Total CPU"

- [Server Timing](https://w3c.github.io/server-timing/)

## CMS

- [Kirby is a file-based cms | Kirby](https://getkirby.com/) - see [Refonte de judbd.com : Étude de cas (2e partie : le CMS Kirby) - MARIE & JULIEN](http://mariejulien.com/post/2016/05/05/Refonte-de-judbd.com-%3A-%C3%89tude-de-cas-%282e-partie-%3A-le-CMS%29)
- [Blog Tool, Publishing Platform, and CMS — WordPress](https://wordpress.org/)
- [CodeIgniter Web Framework](https://www.codeigniter.com/)
- [Symfony, High Performance PHP Framework for Web Development](https://symfony.com/)
- [Drupal - Open Source CMS | Drupal.org](https://www.drupal.org/)
- [Blog Tool, Publishing Platform, and CMS — WordPress](https://wordpress.org/)

- [Laravel - The PHP Framework For Web Artisans](https://laravel.com/)
- [CakePHP - Build fast, grow solid | PHP Framework | Home](https://cakephp.org/)
- [Homepage - Silex - The PHP micro-framework based on the Symfony Components](https://silex.sensiolabs.org/)
- [Slim Framework - Slim Framework](https://www.slimframework.com/)

- [Contentful: a developer-friendly, API-first CMS](https://www.contentful.com/)
- [Sensei - A Learning Management System for WordPress](https://woocommerce.com/products/sensei/) - LMS

- [XForms - Wikipedia](https://en.wikipedia.org/wiki/XForms)

JSON Schema + form:

- [react-jsonschema-form playground](https://mozilla-services.github.io/react-jsonschema-form/) - [mozilla-services/react-jsonschema-form: A React component for building Web forms from JSON Schema.](https://github.com/mozilla-services/react-jsonschema-form)
- [JSON Schema Form](https://github.com/json-schema-form)
- [json-schema-form/angular-schema-form: Generate forms from a JSON schema, with AngularJS!](https://github.com/json-schema-form/angular-schema-form)

### Google Docs Sheets as CMS

- [IMPORTXML - Aide Éditeurs Docs](https://support.google.com/docs/answer/3093342?hl=fr)
- [Google Spreadsheets as a CMS](https://pixeline.be/blog/development/using-google-spreadsheets-as-a-cms-1096.html)
- [Mike Heavers | Google Spreadsheet Powered Content Management System](http://mikeheavers.com/tutorials/creating_a_website_with_a_google_spreadsheet_powered_cms/)
- [Use Google Spreadsheets as a CMS | Hacker News](https://news.ycombinator.com/item?id=7965652)
- [Use Google Sheets for Multilingual Chat - Talk in any Language](https://www.labnol.org/internet/multilingual-chat-in-google-sheets/28698/)

## User script

openuserjs: 

- it's possible to import Script from GitHub, and use a webhook to sync with the source repo
- don't forget to allow Github auth (Authorized OAuth Apps), and add a [licence field](https://openuserjs.org/user/add/scripts#user-block-copyright)

- [New Script | OpenUserJS](https://openuserjs.org/user/add/scripts)
- [Userscript Beginners HOWTO | About | OpenUserJS](https://openuserjs.org/about/Userscript-Beginners-HOWTO)

- [WebExtensions/UserScripts - MozillaWiki](https://wiki.mozilla.org/WebExtensions/UserScripts)
- [User Script Hosting - GreaseSpot Wiki](https://wiki.greasespot.net/User_Script_Hosting)
- [Greasemonkey – Get this Extension for 🦊 Firefox (en-US)](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/)
- [Tampermonkey - Chrome Web Store](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=en)

## Bookmarklet

See [Bookmarklet](JavaScript#bookmarklet)

Note: Bookmarklets are blocked by CSP in Firefox, where bookmarklet = `unsale-inline` script

	// http://www.squarefree.com/2005/05/16/bookmarklets-to-user-scripts/
	let userScriptURI = "data:text/javascript;charset=utf-8,"
	           + "// ==UserScript==%0A"
	           + "// @namespace http://www.squarefree.com/bookmarklets-to-user-scripts%0A"
	           + "// @name " + bookmarkletName + "%0A"
	           + "// @description Runs the " + bookmarkletName + " bookmarklet from " + location.href + "%0A"
	           + "// ==/UserScript==%0A"
	           + "%0A"
	           + encodeURIComponent(decodeURIComponent(bookmarklet.href))
	           + "%0A//.user.js"

	copy("javascript:" + prompt().replace(/[\s%]/g, match => `%${match.charCodeAt(0).toString(16).padStart(2, "0")}`))

- [Bookmarkleter](http://chriszarate.github.io/bookmarkleter/)
- [Installing Bookmarklets](https://mreidsma.github.io/bookmarklets/installing.html)
- [Bookmarklet - Wikipedia](https://en.wikipedia.org/wiki/Bookmarklet)

## Accessibility

Permanant, 

See [Accessibility](../Development/HTML/HTML.md#accessibility)

- EU: [ETSI EN 301 549](https://www.etsi.org/deliver/etsi_en/301500_301599/301549/02.01.02_60/en_301549v020102p.pdf "ETSI EN 301 549 – Accessibility requirements for ICT products and services"), require WCAG 2.1 Level AA
- FR: ETSI EN 301 549 and fallback to internations standards + use [RGAA](https://references.modernisation.gouv.fr/rgaa-accessibilite/ "Référentiel Général d'Accessibilité pour les Administrations") (based on WCAG 2.1) for technical requirements - public online communication services, public institutions, and the state
- DE: [BITV 2.0](https://www.einfach-fuer-alle.de/artikel/bitv_english/bitv_annex1/ "Barrierefreie Informationstechnik-Verordnung") (based on WCAG 2.1 Level AA) - government websites
- IT: [Stanca Act](https://www.agid.gov.it/dm-8-luglio-2005-allegato-A#requisiti "Disposizioni per favorire l’accesso dei soggetti disabili agli strumenti informatici") (based on WCAG 2.0 Level A)
- JP: JIS X 83141 (based on WCAG 2.1)
- ES: UNE 139803:2012 (based on WCAG 2.1 Level AA): government and government-funded organizations; or organizations larger than 100 employees; or with trading column greater than six million euros; or those providing financial, utility, travel/passenger, or retail services online
- US: [Section 508](https://www.section508.gov/) require WCAG 2.0 Level AA
- AU: Disability Discrimination Act (Advisory Notes, based on WCAG 2.0)

See also:

- [Décret sur l’accessibilité numérique : revue détaillée de ce nouveau cadre réglementaire - Access42](http://www.access42.net/decret-accessibilite-juillet-2019)
- [IDI Web Accessibility Checker : Web Accessibility Checker](https://achecker.ca/checker/index.php)
- [Loi n° 2005-102 du 11 février 2005 pour l'égalité des droits et des chances, la participation et la citoyenneté des personnes handicapées | Legifrance](https://www.legifrance.gouv.fr/affichTexte.do?cidTexte=JORFTEXT000000809647&dateTexte=)
- [Décret n° 2019-768 du 24 juillet 2019 relatif à l'accessibilité aux personnes handicapées des services de communication au public en ligne | Legifrance](https://www.legifrance.gouv.fr/affichTexte.do?cidTexte=JORFTEXT000038811937&categorieLien=id)
- [Accessibility Law: International Accessibility Regulations – Introduction to Web Accessibility](https://pressbooks.library.ryerson.ca/iwacc/chapter/international-accessibility-regulations-2/)

About support of old browser vs accessibiliy:

- [Support for old browsers — is it necessary? | Bartosz Mikulski](https://www.mikulskibartosz.name/support-for-old-browsers-is-it-necessary/#a-better-challenge)
- [They are your users • Rik Schennink](http://rikschennink.nl/thoughts/they-are-your-users/)
- [Rik Schennink on Twitter: "There’s more users with disabilities than people using IE8. Still, we tend to drop accessibility in favour of IE8 support. #fronteers14"](https://twitter.com/rikschennink/status/520521059884617728)
- "Prefer make website accessible rather than a full support of IE8"

Stats:

- [User Statistics – People with Disabilities | Unrepentant](http://john.foliot.ca/user-statistics-people-with-disabilities/)
- [Les chiffres-clés du handicap en France | OCIRP](https://www.ocirp.fr/actualites/les-chiffres-cles-du-handicap-en-france)
- [Personnes handicapées − Tableaux de l'économie française | Insee](https://www.insee.fr/fr/statistiques/2569386?sommaire=2587886#consulter)
- [Disability facts and figures - GOV.UK](https://www.gov.uk/government/statistics/disability-facts-and-figures)

Tools:

- [ARC Toolkit | The Paciello Group (TPG) – Digital Accessibility Solutions](https://www.paciellogroup.com/toolkit/) - Accessibility tool to evaluate screens for accessibility and uncover issues related to the WCAG 2.1 Level A/AA
- [AccessiWeb - Accueil](http://www.accessiweb.org/)
- [The W3C Markup Validation Service](http://validator.w3.org/)
- [ChromeLens](http://chromelens.xyz/)
- Checklist [Vox Product Accessibility Guidelines](http://accessibility.voxmedia.com/)
- [Accessibility Developer Tools](https://github.com/GoogleChrome/accessibility-developer-tools)
- [random a11y](http://www.randoma11y.com/) curate beautiful color palettes that are accessible
- [tota11y – an a11y visualization toolkit](http://khan.github.io/tota11y/)
- [GoogleChrome/accessibility-developer-tools](https://github.com/GoogleChrome/accessibility-developer-tools)
- [WebAIM: Using VoiceOver to Evaluate Web Accessibility](http://webaim.org/articles/voiceover/)
- [The Visual ARIA Bookmarklet](http://whatsock.com/training/matrices/visual-aria.htm)
- [Introducing aXe by Deque!](http://www.deque.com/products/axe/)
- https://github.com/nature/pa11y
- [Accessible-email.org - Accessibility Checker Results](http://accessible-email.org/)
- https://github.com/squizlabs/HTML_CodeSniffer
- [The Browser Accessibility Tree | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](https://www.paciellogroup.com/blog/2015/01/the-browser-accessibility-tree/)
- XCode Accessibility Inspector
- `chrome://accessibility/`
- Edge 14: F12 Developer Tools > Accessibility Tree viewer
- [ally.js](https://allyjs.io/)
- [tota11y – an a11y visualization toolkit](http://khan.github.io/tota11y/)
- https://tenon.io/ (non free)
- [dequelabs/axe-core: Accessibility engine for automated Web UI testing](https://github.com/dequelabs/axe-core)
- [Pa11y](http://pa11y.org/)
- [WebAIM: Three things you should know before using VoiceOver for testing](http://webaim.org/blog/three-things-voiceover/)
- [Css Accessibility Validator](http://elad2412.github.io/css-accessibility-validator/)
- [tota11y – an a11y visualization toolkit](http://khan.github.io/tota11y/)
- [WAVE Web Accessibility Tool](http://wave.webaim.org/)
- [Accessibility Reference  |  Tools for Web Developers  |  Google Developers](https://developers.google.com/web/tools/chrome-devtools/accessibility/reference)
- [axe - Web Accessibility Testing - Chrome Web Store](https://chrome.google.com/webstore/detail/axe-web-accessibility-tes/lhdoppojpmngadmnindnejefpokejbdd)

Other:

- [Accessibility: The Missing Ingredient – A List Apart](https://alistapart.com/article/accessibility-the-missing-ingredient/)

## Screensaver

1. télécharger l’application « HTML Screen Saver » sur http://myweb.tiscali.co.uk/djmclean/htmlscreensaver.html
2. l’installer l’application
3. ouvrir le panneau de configuration (du système) (click droit sur le bureau → personaliser)
4. ouvrir les préférences du économiseur d’écran / screen saver
5. choisir dans la liste déroulante « HTML Screen Saver », si c’est pas déjà le cas
6. cliquer sur options / settings
7. parcourir et sélectionner le fichier .html précédemment reçu
8. clicker sur Test pour prévisualiser
9. clicker sur OK

- [HTML Screensaver, Universal ScreenSaver, Web Screen Saver](http://myweb.tiscali.co.uk/djmclean/htmlscreensaver.html) - Windows only. Require `X-UA-Compatible` header/meta or `FEATURE_BROWSER_EMULATION` registery key. See [Web Browser Control & Specifying the IE Version - Rick Strahl's Web Log](https://weblog.west-wind.com/posts/2011/May/21/Web-Browser-Control-Specifying-the-IE-Version#RenderingChallenged)
- [liquidx/webviewscreensaver: Mac OS X Screen Saver powered by a Web View](https://github.com/liquidx/webviewscreensaver) - macOS only
- [brockgr/websaver: Automatically exported from code.google.com/p/websaver](https://github.com/brockgr/websaver)
- [tlrobinson/WebSaver: A WebKit-based Mac OS X screensaver. Use any webpage or JavaScript program as a screensaver.](https://github.com/tlrobinson/WebSaver) - enmpty wrapper for macOS
- [cwc/web-page-screensaver: Display a web page as your screensaver](https://github.com/cwc/web-page-screensaver/) - Windows only
- [Google Code Archive - Long-term storage for Google Code Project Hosting.](https://code.google.com/archive/p/web-page-screensaver/)

- [How to Scr: Writing an OpenGL Screensaver for Windows](http://www.cityintherain.com/howtoscr.html)
- [Creating a Screen Saver with C#](http://www.harding.edu/fmccown/screensaver/screensaver.html)

## Kiosk mode

- Chrome: `chrome --chrome --fullscreen --kiosk URI`
- Opera: `opera -kioskmode -noexit URI`
- Firefox: `firefox --headless URI`
- IE: `iexplore -k URI`

- `Windows + Shift + Enter` (fullscreen mode), like `F11`
- [Opening Chrome browser in full window or kiosk mode on windows 7 - Stack Overflow](https://stackoverflow.com/questions/39068389/opening-chrome-browser-in-full-window-or-kiosk-mode-on-windows-7)
- [chrome_switches.cc - Code Search](https://cs.chromium.org/chromium/src/chrome/common/chrome_switches.cc?q=kKioskMode&sq=package:chromium&type=cs&l=457)
- [Headless mode - Mozilla | MDN](https://developer.mozilla.org/en-US/Firefox/Headless_mode)
- [How to use Kiosk Mode in Microsoft Internet Explorer](https://support.microsoft.com/en-us/help/154780/how-to-use-kiosk-mode-in-microsoft-internet-explorer)
- [windows 7 - how can I start Internet Explorer 10 always in kiosk-mode? - Super User](https://superuser.com/questions/666899/how-can-i-start-internet-explorer-10-always-in-kiosk-mode)

See also:

- [iOS](iOS#kiosk-mode)
- [Android](Android#kiosk-mode)
- [Windows](Windows#kiosk-mode)
- [macOS](macOS#kiosk-mode)

## BaaS

Aka backend as a service, Mobile backend as a service (MBaaS)

- [Mobile backend as a service - Wikipedia](https://en.wikipedia.org/wiki/Mobile_backend_as_a_service)

Email:

- [Mailjet: Powerful and Effective Email Solutions](https://www.mailjet.com/)
- [Email Delivery Service | SendGrid](https://sendgrid.com/)
	> For sending via SMTP, provide the string `apikey` as the SMTP username, and use your API Key as the password.
	- [API Key - SendGrid Documentation | SendGrid](https://sendgrid.com/docs/Classroom/Send/How_Emails_Are_Sent/api_keys.html#-Via-SMTP)
- [Transactional Email API Service For Developers | Mailgun](https://www.mailgun.com/)
- [Transactional Email from MailChimp - Mandrill](http://www.mandrill.com/)
- [Amazon Simple Email Service | Fournisseur de messagerie cloud, SMTP, Business, Marketing | AWS](https://aws.amazon.com/fr/ses/)
- SMTP relay of [G Suite – Gmail, Docs, Drive, Calendar and More for Business](https://gsuite.google.com/)
	- [Gmail sending limit in G Suite - G Suite Administrator Help](https://support.google.com/a/answer/166852)
	- [SMTP relay: Route outgoing non-Gmail message through Google - G Suite Administrator Help](https://support.google.com/a/answer/2956491)
	- [Sending Email from an Instance  |  Compute Engine Documentation |  Google Cloud Platform](https://cloud.google.com/compute/docs/tutorials/sending-mail/)
	- [Send email from a printer, scanner, or app - G Suite Administrator Help](https://support.google.com/a/answer/176600?hl=en)

SMS and phone call (voice):

- [Nexmo - APIs for SMS, Voice and Phone Verifications](https://www.nexmo.com/)
- [Communication APIs for SMS, Voice, Video and Authentication](https://www.twilio.com/)
- [AWS | Amazon SNS - Service d'envoi de SMS et notifications push](https://aws.amazon.com/fr/sns/)
- [578 Telephony, SMS, and MMS APIs - Google Sheets](https://docs.google.com/spreadsheets/d/1BshonTqZfYcSBRA7bs4DsQ6PChdAeNRn9LV4tMgwEeo/edit#gid=0)

## Advertising

Aka Ads

See also:

- [Content blocking](#content-blocking) - blocked ads by filters
- [Acceptable Ad criteria](https://acceptableads.com/en/about/criteria) - Rules by AdBlock
- [SEO and ASO](#seo-and-aso) - balance between content and ads
- [The Initial Better Ad Standard - Coalition for Better Ads](https://www.betterads.org/standards/) - Coalition for Better Ads
- [Web Tools - Web Tools](https://www.google.com/webmasters/tools/ad-experience-unverified?pli=1) - [About the Ad Experience Report - Web Tool Help](https://support.google.com/webtools/topic/7073612?ref_topic=7566613)

## Content blocking

Safe Browsing (UrlSubresourceFilter, BetterAds)

- [Category:Ad blocking software - Wikipedia](https://en.wikipedia.org/wiki/Category:Ad_blocking_software)
- [Ad blocking - Wikipedia](https://en.wikipedia.org/wiki/Ad_blocking)	
- [Chromium Blog: Under the hood: How Chrome's ad filtering works](https://blog.chromium.org/2018/02/how-chromes-ad-filtering-works.html)
- [Bloqueur de publicités de Chrome : EasyList utilisé pour le blocage, de nouveaux détails](https://www.nextinpact.com/news/106147-bloqueur-publicites-chrome-easylist-utilise-pour-blocage-nouveaux-details.htm)
- [Here’s how Google Chrome’s new ad blocker works – Ctrl blog](https://www.ctrl.blog/entry/chrome-adblocker)
- [Should web browsers adopt Google’s new selective ad blocking tech? – Ctrl blog](https://www.ctrl.blog/entry/google-adblocking-competition)
- `chrome://components/`

- [Intelligent Tracking Prevention 2.0 | WebKit](https://webkit.org/blog/8311/intelligent-tracking-prevention-2-0/) - ITP (Intelligent Tracking Prevention), third party cookies isolation
- [Chromium Blog: Under the hood: How Chrome' ad filtering works](https://blog.chromium.org/2018/02/how-chromes-ad-filtering-works.html)
- [Focus by Firefox - Content Blocking for the Open Web - The Mozilla Blog](https://blog.mozilla.org/blog/2015/12/07/focus-by-firefox-content-blocking-for-the-open-web/)
- [Selectively Filtering Content in Web Browsers – IEBlog](https://blogs.msdn.microsoft.com/ie/2010/11/30/selectively-filtering-content-in-web-browsers/)
- [Storage access policy: Block cookies from trackers - Mozilla | MDN](https://developer.mozilla.org/fr/docs/Mozilla/Firefox/Privacy/Storage_access_policy#Tracking_protection_explained)
- [Microsoft Edge – All the news from Build 2019 - Microsoft Edge Blog](https://blogs.windows.com/msedgedev/2019/05/06/edge-chromium-build-2019-pwa-ie-mode-devtools/) - Privacy tools: tracking prevention
- [New Year, New Samsung Internet – Samsung Internet Developers – Medium](https://medium.com/samsung-internet-dev/new-year-new-samsung-internet-b74f282e4429) - Samsung Internet 9.2 includes Smart Anti-Tracking

See also:

- [Troubleshooting](#troubleshooting)
- [Advertising](#advertising)

### Safe browsing

- `chrome://safe-browsing/`
- [Security/Safe Browsing/Chromium Implementation Overview - MozillaWiki](https://wiki.mozilla.org/Security/Safe_Browsing/Chromium_Implementation_Overview)
- Google Safe Browsing
	- https://google.com/safebrowsing/diagnostic?tpl={safari|mozilla|}&site={host}&hl=en-US
	- https://www.google.com/safebrowsing/report_error/?tpl={safari}
	- [Safe Browsing Update API (v4)  |  Safe Browsing APIs (v4)](https://developers.google.com/safe-browsing/v4/update-api)
	- [Safe Browsing: malware and phishing – Google Transparency Report](https://transparencyreport.google.com/safe-browsing/search?hl=en) - Check site status
	- [Prevent & report phishing attacks - Google Search Help](https://support.google.com/websearch/answer/106318?hl=en)
	- [k-anonymity](https://en.wikipedia.org/wiki/K-anonymity) of the API:
		- Google first computes the SHA256 hash of each unsafe URL in its database, and truncates each hash down to a 32-bit prefix to save space.
		- Google sends the database of truncated hashes down to your browser.
		- Each time you visit a URL, your browser hashes it and checks if its 32-bit prefix is contained in your local database.
		- If the prefix is found in the browser’s local copy, your browser now sends the prefix to Google’s servers, which ship back a list of all full 256-bit hashes of the matching  URLs, so your browser can check for an exact match.
- Tencent Safe Browsing, Safe Browsing API is a drop-in replacement of Google's API
	- https://www.urlsec.qq.com/check.html?tpl={safari|}&site={host}
	- https://urlsec.qq.com/check.html?url={url|domain}
	- https://urlsec.qq.com/report.html?url={url} reportAnError
	- https://urlsec.qq.com/complain.html
	- https://safebrowsing.urlsec.qq.com
	- https://www.urlsec.qq.com/standard/s1.html Learn more
- [Firefox Website Warning | StopBadware](https://www.stopbadware.org/firefox)
- [(Safe) Safe Browsing Testing Links](https://testsafebrowsing.appspot.com/)

[Phishing facts](https://www.itgovernance.co.uk/blog/4-eye-opening-facts-about-phishing):

- phishing sites have a lifecycle of about 15 hours
- most malicious links are hidden within benign domains
- about 400,000 phishing sites are created each month

Code:

- [safe_browsing/ - Code Search](https://cs.chromium.org/chromium/src/chrome/browser/safe_browsing/?q=chrome/browser/safe_browsing/&sq=package:chromium&dr)
- [SafeBrowsingWarningCocoa.mm dans webkit/trunk/Source/WebKit/UIProcess/Cocoa. – WebKit](http://trac.webkit.org/browser/webkit/trunk/Source/WebKit/UIProcess/Cocoa/SafeBrowsingWarningCocoa.mm?rev=239408) - Safe Browsing
- /System/Library/PrivateFrameworks/SafariSafeBrowsing.framework

## Datasets

- [HTTP Archive FAQ](https://httparchive.org/faq#how-do-i-use-bigquery-to-write-custom-queries-over-the-data)
- [httparchive.org/gettingstarted_bigquery.md at master · HTTPArchive/httparchive.org](https://github.com/HTTPArchive/httparchive.org/blob/master/docs/gettingstarted_bigquery.md)
- [Chrome User Experience Report  |  Tools for Web Developers  |  Google Developers](https://developers.google.com/web/tools/chrome-user-experience-report/)
- [Chrome User Experience Report  |  Tools for Web Developers  |  Google Developers](https://developers.google.com/web/tools/chrome-user-experience-report/getting-started#example-queries)
- [blog.tomayac.com » Blog von Thomas Steiner » homoblogiens](https://blog.tomayac.com/2018/07/09/progressive-web-apps-in-the-http-archive-143748)
- [Sample BigQuery queries for the HTTP Archive dataset.](https://gist.github.com/igrigorik/5801492)
- [Overview: Standard SQL Reference  |  BigQuery  |  Google Cloud](https://cloud.google.com/bigquery/docs/reference/standard-sql/)
- [Using HTTPArchive and Chrome UX Report to Get Lighthouse Scores - DZone Performance](https://dzone.com/articles/using-httparchive-and-chrome-ux-report-to-get-ligh)

Datasets:

- [chrome-ux-report](https://bigquery.cloud.google.com/dataset/chrome-ux-report:all) (aka CrUX)
- [httparchive](https://bigquery.cloud.google.com/dataset/httparchive:runs.latest_pages)

## Sourcemap

Aka source map

For CSS and JavaScript

- [DIY source maps / Stoyan's phpied.com](https://www.phpied.com/diy-source-maps/)
- [Source Mapper](https://sourcemaps.info/)
- [mozilla/source-map: Consume and generate source maps.](https://github.com/mozilla/source-map)
- [Introduction to JavaScript Source Maps - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/developertools/sourcemaps/)
- [Source maps: languages, tools and other info · ryanseddon/source-map Wiki](https://github.com/ryanseddon/source-map/wiki/Source-maps%3A-languages%2C-tools-and-other-info)

## PWA

See also

- [Service worker](../Development/JavaScript/JavaScript.md#service-worker)
- [What’s new on iOS 12.2 for Progressive Web Apps – Maximiliano Firtman – Medium](https://medium.com/@firt/whats-new-on-ios-12-2-for-progressive-web-apps-75c348f8e945#06d6) - PWA lifecycle on iOS 12.2
- [iOS Add to Homescreen =\> simulate web app manifest](https://gist.github.com/PaulKinlan/d66f777f5bde04926f29fc5c7ff345e7) - simulate `start_url` manifest field in iOS

## Wi-Fi Captivate

Walled garden, captive portal

- with Captive Network Assistant (mini-browser / webview), some features can be disabled (persistant cookies, alert, confirm, popin, cross-origin AJAX, sessionStorage)
- [local area network - Captive portal popups: the definitive guide - Server Fault](https://serverfault.com/questions/679393/captive-portal-popups-the-definitive-guide)
- [Use captive Wi-Fi networks on your iPhone, iPad, or iPod touch - Apple Support](https://support.apple.com/en-us/HT204497)
- [Captive portal - Wikipedia](https://en.wikipedia.org/wiki/Captive_portal)
- [FX-Captive-Portals-Design/detection.md at master · vtsatskin/FX-Captive-Portals-Design](https://github.com/vtsatskin/FX-Captive-Portals-Design/blob/master/detection.md)
- [iOS: Open a Welcome Page in Safari, not CNA (post-authentication) - Stack Overflow](https://stackoverflow.com/questions/29744245/ios-open-a-welcome-page-in-safari-not-cna-post-authentication/30251103#30251103)
- [ios - Captive Wifi Popup: Click a link to open Safari - Stack Overflow](https://stackoverflow.com/questions/23281552/captive-wifi-popup-click-a-link-to-open-safari/40561556#40561556)
- [wifi - How to automatically login to captive portals on OS X? - Ask Different](https://apple.stackexchange.com/questions/45418/how-to-automatically-login-to-captive-portals-on-os-x/338596#338596)
- `/Library/Preferences/SystemConfiguration/CaptiveNetworkSupport/Settings.plist`
- `User-Agent: CaptiveNetworkSupport/1.0 wispr`
- `/System/Library/CoreServices/Captive Network Assistant.app`
- [Making Phones Believe the WiFi has Internet ~ Foxdog Studios](https://foxdogstudios.com/blog/making-phones-believe-the-wifi-has-internet) - [backup page](https://archive.is/hioCo)
- [tripflex/captive-portal: Mongoose OS Captive Portal Library](https://github.com/tripflex/captive-portal)
- ["Strange url in iOS CaptiveNetworkSupport binary" | itsme's blog](http://nlitsme.github.io/posts/2014-10-20-strange-url-in-ios-captivenetworksupport-binary/)
- [Captive Portal](https://wikileaks.org/ciav7p1/cms/page_31883312.html) - How to trick a device to launch its captive portal window

Tested URLs:

- http://www.apple.com/library/test/success.html
- http://captive.apple.com/hotspot-detect.html
- http://connectivitycheck/gstatic/com/generate_204
- [tripflex/captive-portal: Mongoose OS Captive Portal Library](https://github.com/tripflex/captive-portal#known-endpoints)

On iOS and OSX, when WiFi connection is detected, the OS try to open this URL: `http://captive.apple.com/hotspot-detect.html` (previously `http://apple.com/library/test/success.html`) which return `200 Ok` with content `<HTML><HEAD><TITLE>Success</TITLE></HEAD><BODY>Success</BODY></HTML>`

- https://stackoverflow.com/questions/18891706/ios7-and-captive-portals-changes-to-apple-request-url
- http://blog.erratasec.com/2010/09/apples-secret-wispr-request.html
- http://www.davidcalculli.com/blog/2012/10/apples-secret-connecting-to-a-wi-fi-network-requires-an-active-internet-connection
- [iOS Wi-Fi profiles: About Auto Join and per-connection password settings - Apple Support](https://support.apple.com/en-ca/HT202343)
- [How can I get Wifi if "http://www.apple.com/library/test/success.html" is blocked?](https://discussions.apple.com/message/19868615)
- https://en.wikipedia.org/wiki/Captive_portal
- `/System/Library/CoreServices called Captive Network Assistant.app` `/Library/Preferences/SystemConfiguration/CaptiveNetworkSupport/Settings.plist`
- http://apple.stackexchange.com/questions/211593/how-to-disable-captive-apple-com
- http://superuser.com/questions/937325/wifi-hotspot-why-os-does-not-detect-me-as-a-captive-portal
- http://blog.erratasec.com/2010/09/apples-secret-wispr-request.html

- http://www.dd-wrt.com/wiki/index.php/Chillispot
- http://coova.github.io/CoovaChilli/
- http://blog.trifork.com/2013/01/15/building-a-captive-portal-controlling-access-to-the-internet-from-your-network/
- https://www.howtoforge.com/tutorial/how-to-install-a-wireless-hotspot-with-captive-page-in-linux-using-coovachilli/
- https://learn.adafruit.com/setting-up-a-raspberry-pi-as-a-wifi-access-point/install-software
- http://www.pihomeserver.fr/2014/05/22/raspberry-pi-home-server-creer-hot-spot-wifi-captive-portal/
- http://www.pihomeserver.fr/2014/05/23/raspberry-pi-home-server-creer-hot-spot-wifi-portail-captif-22/

## Popup

Allow multiple popup, or open popup from non user action:

- Chrome:
	1. open website informations (from the URL bar)
	2. click website parameters (chrome://settings/content/siteDetails?site=http%3A%2F%2Fexample.com)
	3. set "Popups & redirections" to "Allowed"
- Firefox:
	1. open page informations (Tools > Page informations)
	2. go to permissions tab
	3. uncheck "default permissions" for "Open popus" and select "Allow"
- Edge:
	1. open Settings
	2. go to Advanced Settings
	3. switch Block Pop Ups Off
	4. after using the desired website, roll back these settings
