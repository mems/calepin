## DNS

- [How DNS works](https://howdns.works/)
- [linux - Force dig to resolve without using cache - Server Fault](https://serverfault.com/questions/372066/force-dig-to-resolve-without-using-cache/372071#372071)

### DNS records

Names (exemples for `example.com`):

- `@` naked name (`example.com`), the domain itself
- `*` fallback subdomain (`*.example.com`, but doesn't match `*.test.example.com` if `test.example.com` is declared)
- `www` subdomain (`www.example.com`)
- `test.www` subsubdomain (`test.www.example.com`)
- `*.www` fallback subsubdomain (`*.www.example.com`)

`* CNAME @` is not possible with all DNS servers, and not recommanded (need 2 DNS requests to resolve subdomain)

```dns-zone
@ IN A 192.0.2.1
@ IN TXT "some text"
```

```sh
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

```
23:50:52:658: Network: POST http://host/folder [HTTP/1.1 301 Moved Permanently 947ms]
23:50:53:614: Network: GET http://host/folder/ [HTTP/1.1 200 OK 400ms]
```

> When you use a 301 or 302 redirect, the browser will change the method on the redirect to be a GET request, even if the original method was a POST request.

**Use the 307 and 308 status codes instead if you need to retain the method**

- [301s, 302s, 307s & 308s: Report URI's journey to a permanent redirect](https://scotthelme.co.uk/report-uri-journey-to-a-permanent-redirect/)
- [web development - Why doesn't HTTP have POST redirect? - Software Engineering Stack Exchange](https://softwareengineering.stackexchange.com/questions/99894/why-doesnt-http-have-post-redirect/99966#99966)

### Define generated filename

```http
Content-Disposition: "attachment; filename=generated_filename.ext"
```

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

```
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
```

- [Using NGINX as a WebSocket Proxy](https://www.nginx.com/blog/websocket-nginx/)
- [Websockets SSL/TLS Termination Using NGINX Proxy · Pankaj Malhotra](http://pankajmalhotra.com/Websockets-SSL-TLS-Termination-Using-NGINX-Proxy/)

For Apache:

Example of Apache-as-proxy configuration (require `mod_proxy` and `mod_proxy_wstunnel` - require httpd 2.4.5)

```apache
# Reverse proxy to nodejs
<Location /ws-service>
	Require all granted
	ProxyPass ws://localhost:9000
	ProxyPassReverse ws://localhost:9000
</Location>
```

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
 
 ```apache
<Location /index.html>
	Header add Link "</css/site.css>;rel=preload;as=style"
	Header add Link "</images/logo.jpg>;rel=preload;as=image"
</Location>
```

Inline `Link: </css/my.css>;rel=preload;as=style, </js/jquery.js>;rel=preload;as=script` works too

Or define it via PHP:

```php
header('Link: </css/my.css>;rel=preload;as=style', false);
```

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

```php
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
```

- [HTTP/2 push is tougher than I thought - JakeArchibald.com](https://jakearchibald.com/2017/h2-push-tougher-than-i-thought/)
- [Creating a Cache-aware HTTP/2 Server Push Mechanism | CSS-Tricks](https://css-tricks.com/cache-aware-server-push/)
- [A Comprehensive Guide To HTTP/2 Server Push – Smashing Magazine](https://www.smashingmagazine.com/2017/04/guide-http2-server-push/#pushes-may-not-be-cached)
- [HTTP/2 Directives - Configure - H2O - the optimized HTTP/2 server](https://h2o.examp1e.net/configure/http2_directives.html#http2-casper)
- [Hypertext Transfer Protocol Version 2 (HTTP/2)](https://http2.github.io/http2-spec/#RST_STREAM) - see [http - RST_STREAM frame in HTTP2 - Stack Overflow](https://stackoverflow.com/questions/28736463/rst-stream-frame-in-http2)

### Force download

```http
Content-Disposition: attachment;filename=file.ext
```

You can use also:

```http
Content-Type: application/octet-stream
```

```http
X-Download-Options: noopen
```

### Access

- [XSS and injection prevention](../Security/Data%20access%20and%20integrity/Data%20access%20and%20integrity.md#xss-and-injection-prevention) - CORS, CSP, SI, etc.

### Referer

See [Security](Security#http-referer)

### Method

Aka POST, GET, HEAD, PUT, etc.

See [RESTful](#restful) and [API](#api)

- `X-HTTP-Method` (Microsoft), `X-HTTP-Method-Override` (Google/GData), `X-Method-Override` (IBM)
- [The Definitive Guide to GET vs POST - Treehouse Blog](http://blog.teamtreehouse.com/the-definitive-guide-to-get-vs-post)

### Simple HTTP Server

**Run in controlled environments only!**. Useful for testing purposes or for application demonstrations

- [http.server — HTTP servers — Python 3 documentation](https://docs.python.org/3/library/http.server.html) `python -m http.server 8000 -d /path/to/wwwroot`
- [PHP: Built-in web server - Manual](http://php.net/manual/en/features.commandline.webserver.php) - `php -S localhost:8000 -t /path/to/wwwroot`
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

### Cache

Aka cache policy

> Sending `last-modified: Thu, 01 Jan 1970 00:00:01 GMT` prevents the page from updating. Gives it super long cache heuristic, and makes revalidation think it never ever changes.
> — [kornel@mastodon.social on Twitter: "New fun failure mode added to my collection: Sending `last-modified: Thu, 01 Jan 1970 00:00:01 GMT` prevents the page from updating. Gives it super long cache heuristic, and makes revalidation think it never ever changes." / Twitter](https://twitter.com/kornelski/status/1250769178455408640)

- [kornelski/http-cache-semantics: RFC 7234 in JavaScript. Parses HTTP headers to correctly compute cacheability of responses, even in complex cases](https://github.com/kornelski/http-cache-semantics)

### Content language

`lang` HTML attribute indicates the language of the text, whereas `Content-Language` provides metadata about the intended audience of the document.

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
 
 ```php
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
```

IPv4 to number & number to IPv4:

```php
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
```

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

```http
Cache-Control: no-transform
```

Apache config (ex.: in `.htaccess`):

```apache
<IfModule headers_module>
	Header set Cache-Control no-transform
</IfModule>
```

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

```apache
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
```

`endpoint.php`:

```php
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
```

`pac.php`:

```php
<?php header('Content-Type: application/x-javascript-config') ?>
function FindProxyForURL(url, host)
{ 
	 return "PROXY <?php echo $_SERVER['SERVER_ADDR'] ?>:<?php echo $_SERVER['SERVER_PORT'] ?>; DIRECT";
}
```

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

### URI template

```
https://example.com/{file}
https://example.com/search{?q*,lang}
```

- [RFC 6570 - URI Template](https://tools.ietf.org/html/rfc6570)
- [hannesg/uri_template: A URI template library for ruby.](https://github.com/hannesg/uri_template)
- [medialize/URI.js: Javascript URL mutation library](https://github.com/medialize/URI.js)
- [grncdr/uri-template: CoffeeScript/Javascript implementation of RFC 6570 for URI-templates](https://github.com/grncdr/uri-template)
- [geraintluff/uri-templates: JavaScript utility for RFC 6570: URI Templates](https://github.com/geraintluff/uri-templates)

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

```
application/font-woff
```

```
data:application/pdf;name=document.pdf;base64,BASE64_DATA_ENCODED
```

- Firefox require hash to be encoded/escaped
- IE require more chars to be encoded/escaped

- [CSS # Sprites vs Data URI](../Development/CSS/CSS.md#sprites-vs-data-uri)
- [Formats and protocols/URI](../Formats%20and%20protocols/URI/URI.md#data-uri)
- [SVG gradient and backgrounds]()
- [Optimizing SVGs in data URIs by Taylor Hunt on CodePen](http://codepen.io/Tigt/blog/optimizing-svgs-in-data-uris)
- [Probably Don't Base64 SVG | CSS-Tricks](https://css-tricks.com/probably-dont-base64-svg/)
- [Getting URL encoded SVG to work in IE](http://codepen.io/chriscoyier/pen/ZQgvyG/)
- [Blue Box Data URI (svg](http://codepen.io/AmeliaBR/details/xijuv/)
- [Sass function to encode SVG as a data uri without it being in base64](https://github.com/waldemarfm/sass-svg-uri)

#### Data URI base 64 encoding

See [Base64](Base64)

Works with IE 9+ and others browsers

```css
background: red url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHZpZXdCb3g9JzAgMCAxMDAgMTAwJz48cmVjdCBmaWxsPSdncmVlbicgd2lkdGg9JzEwMCcgaGVpZ2h0PScxMDAnLz48L3N2Zz4=");
```

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

```css
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
```

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

Aka postback, pixel

- [Webhook - Wikipedia](https://en.wikipedia.org/wiki/Webhook)
- [WebSub](https://www.w3.org/TR/websub/) - Open protocol for distributed pub–sub communication on the internet
- [WebSub Rocks!](https://websub.rocks/)
- [Postback - Wikipedia](https://en.wikipedia.org/wiki/Postback)
