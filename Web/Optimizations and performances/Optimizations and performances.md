# Optimizations and performances

Aka webperf, web perf

> respecting the medium

- [The Ethics of Web Performance - Web Performance Consulting | TimKadlec.com](https://timkadlec.com/remembers/2019-01-09-the-ethics-of-performance/)

Loading, parsing, rendering, etc.

> We don't want humans waiting on computers. We want computers waiting on humans.
>
> — Gregory Szorc

> Monitoring is your bank telling you you're overdrawn.
>
> Observability is the ability to tell you're running out of money because you're spending too much money on chocolates, cakes and sweets because you've recorded data on what you spent your money on throughout the month.
>
> — [Liz Fong-Jones (方禮真) sur Twitter : "Monitoring is your bank telling you you're overdrawn. Observability is the ability to tell you're running out of money because you're spending too much money on chocolates, cakes and sweets because you've recorded data on what you spent your money on throughout the month. https://t.co/kQcvlUWqqV" / Twitter](https://twitter.com/lizthegrey/status/1230979460708499456?s=12)

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
- [Turbocharging Walmart.com: Speed without compromise - Speaker Deck](https://speakerdeck.com/vasa/turbocharging-walmart-dot-com-speed-without-compromise)
- [Optimising Largest Contentful Paint – CSS Wizardry – Web Performance Optimisation](https://web.archive.org/web/20220413001805/https://csswizardry.com/2022/03/optimising-largest-contentful-paint/)

> Progressive JPEGs decode slower than Baseline ones. [..] decoding a progressive JPEG takes about 3.3× as long as a baseline one. (I would still absolutely recommend using progressive, because they feel a lot faster than their baseline counterparts.)
>
> — [Base64 Encoding & Performance, Part 2: Gathering Data – CSS Wizardry – Web Performance Optimisation](https://web.archive.org/web/20220109053656/https://csswizardry.com/2017/02/base64-encoding-and-performance-part-2/#some-interesting-things-i-learned)

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

## Control your content

- [The Washington Post cuts off ad tech vendors slowing its site - Digiday](https://digiday.com/media/washington-post-vendors/)

## Impacts

To mesure impacts ([KPI](https://en.wikipedia.org/wiki/Performance_indicator): [bounce rate](https://en.wikipedia.org/wiki/Bounce_rate), [conversion rate](https://en.wikipedia.org/wiki/Conversion_marketing#Conversion_rate)): use [A/B testing](https://en.wikipedia.org/wiki/A/B_testing)

- [The Impact of Web Performance | Simplified.](https://web.archive.org/web/20210814233129/https://simplified.dev/performance/impact-of-web-performance)
- [SpeedCurve on Twitter: "200ms start render = 16% bounce rate 1.8s start render = 49% bounce rate See how user engagement charts show you correlations between #webperf and #UX: https://t.co/Nz6ilYOuaA https://t.co/CpX5FRZ5xm" / Twitter](https://web.archive.org/web/20220125093206/https://twitter.com/SpeedCurve/status/938877356386611201)

## Mobile

- [Mobile-Friendly Test - Google Search Console](https://search.google.com/search-console/mobile-friendly)
- https://www.google.com/webmasters/tools/mobile-friendly/
- https://www.google.com/webmasters/tools/mobile-usability
- https://www.bing.com/webmaster/tools/mobile-friendliness
- [Mobile Web Application Best Practices](http://www.w3.org/TR/mwabp/)

## Reduce bytes

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

	```http
	set-cookie: key1=value1; key2=value2; domain=.example.com; expires=Fri, 21-Dec-2018 22:15:42 GMT; path=/
	```

	Use:

	```http
	set-cookie: key1=value1; domain=.example.com; expires=Fri, 21-Dec-2018 22:15:42 GMT; path=/
	set-cookie: key2=value2; domain=.example.com; expires=Fri, 21-Dec-2018 22:15:42 GMT; path=/
	```

	- [mnot’s blog: Designing Headers for HTTP Compression](https://www.mnot.net/blog/2018/11/27/header_compression)
	- [Headers](#headers)
	- [Header compression](#header-compression)
- use the right format (if supported, or a fallback):
	- ~~as binary representation of CSS (really usefull vs GZ?)~~
	- use image as data container (as colors, but could be lossy)
	- transparent video: WebM or side by side channels (RGB + A as RGB) videos. See [Alpha](Video#Alpha)
	- transparent image: instead of PNG use WebP (or JPEG-XR) or combined formats. See [Alpha compression](Image#Alpha compression)
	- animated image: use APNG or Animated WebP or looped video instead of GIF

		```html
		<video autoplay loop muted playsinline poster="original.jpg">
			<source type="video/webm" src="original.webm">
			<img src="original.gif">
		</video>
		```

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

## Reduce requests

- embed images in CSS using data URI, encoded with URI encoding or base64 (could have a negative impact on low end devices)
- JS, CSS in HTML in tags `<script>` and `<style>`
- CSS/HTML in JavaScript variables
- HTML prerendered (HTML + JS + data)
- bundle JS and/or CSS, image spriting https://github.com/clyfish/zerosprites http://yostudios.github.io/Spritemapper/
- add the right header(s) for server cache strategy (see [Cache](#cache))

Note: HTTP/2 [multiplex](#multiplexed--pipelining) and [push](#server-push) are not always a good alternative, because compression is more efficient on larger chunk data. [Musings on HTTP/2 and Bundling | CSS-Tricks](https://css-tricks.com/musings-on-http2-and-bundling/)

- [The Best Request Is No Request, Revisited · An A List Apart Article](https://alistapart.com/article/the-best-request-is-no-request-revisited) - Unbundle resources with HTTP/2.0 but be carefull

## Reduce latency

Mesure latency:

- [Nping - Network packet generation tool / ping utiliy](https://nmap.org/nping/)
- [Can you get a reply from a HTTPS site using the Ping command? - Super User](https://superuser.com/questions/326403/can-you-get-a-reply-from-a-https-site-using-the-ping-command/895070#895070) - tcping (ping TCP ACK)
- [hping - Wikipedia](https://en.wikipedia.org/wiki/Hping)

Use CDN

- [Optimizing HTTP/2 prioritization with BBR and tcp_notsent_lowat](https://blog.cloudflare.com/http-2-prioritization-with-nginx/)

Use a popular TLD do use DNS resolver cache:

- [Is your fancy new domain hurting your performance? Benchmarking the top-level domain names - BunnyCDN Blog](https://bunnycdn.com/blog/is-your-fancy-new-domain-hurting-your-performance-gtld-benchmark/)

### First packet size

- [wifi - What is the total length of pure TCP Ack sent over ethernet? - Stack Overflow](https://stackoverflow.com/questions/5543326/what-is-the-total-length-of-pure-tcp-ack-sent-over-ethernet)

#### Initial TCP window

> Minimize ATF (above-the-fold) content size: The first TCP connection isn’t able to fully utilize a connection’s bandwidth on the first roundtrip, which means the number of packets it can send is very limited. In order to render your ATF content it needs to be 148 kb or less
— [5 SEO Guidelines for Web Developers](https://www.sitepoint.com/5-seo-guidelines-for-web-developers/)

Congestion window: initial cwnd size is 10; 14.6KB = 10 packets of 1460 Bytes.

**TODO: where "148 kb" come from?**

- [TCP Slow-start](https://en.wikipedia.org/wiki/Slow-start)
- [Napkin Problem 15: Increase HTTP Performance by Fitting In the Initial TCP Slow Start Window](https://sirupsen.com/napkin/problem-15/)
- [Networking 101: Building Blocks of TCP - High Performance Browser Networking (O'Reilly)](https://hpbn.co/building-blocks-of-tcp/#slow-start)
- [Reduce the size of the above-the-fold content  |  PageSpeed Insights  |  Google Developers](https://developers.google.com/speed/docs/insights/PrioritizeVisibleContent)
- [Mobile Analysis in PageSpeed Insights  |  PageSpeed Insights  |  Google Developers](https://developers.google.com/speed/docs/insights/mobile)
- [networking - maximum packet size for a TCP connection - Stack Overflow](https://stackoverflow.com/questions/2613734/maximum-packet-size-for-a-tcp-connection)
- [draft-hkchu-tcpm-initcwnd-01 - Increasing TCP's Initial Window](https://tools.ietf.org/html/draft-hkchu-tcpm-initcwnd-01)
- [Tuning initcwnd for optimum performance - CDN Planet](http://www.cdnplanet.com/blog/tune-tcp-initcwnd-for-optimum-performance/)
- [Increasing tcp slow start Initial Window in linux 3.0 kernel - Server Fault](http://serverfault.com/questions/365614/increasing-tcp-slow-start-initial-window-in-linux-3-0-kernel)
- [Is it possible to configure the initial window size for tcp slow start on Windows? - Server Fault](http://serverfault.com/questions/160690/is-it-possible-to-configure-the-initial-window-size-for-tcp-slow-start-on-window)

### Fast Open

- [TCP Fast Open - Wikipedia](https://en.wikipedia.org/wiki/TCP_Fast_Open)
- [Blog Stéphane Bortzmeyer: Commencer les sessions TCP plus vite ?](http://www.bortzmeyer.org/tcp-ouverture-rapide.html)
- [TCP Fast Open - Wikitech](https://wikitech.wikimedia.org/wiki/TCP_Fast_Open#Detecting_server-side_TFO_support)
- [GitHub - bradleyfalzon/tcp-fast-open: Golang example of TCP Fast Open (RFC7413)](https://github.com/bradleyfalzon/tcp-fast-open)
- [Optimizing TCP slow start - Tuning Microsoft IIS - IISWebSpeed.com](https://www.iiswebspeed.com/documentation/iistuning/tcp-slow-start)
- [TCP Fast Open - KeyCDN Support](https://www.keycdn.com/support/tcp-fast-open/)
- [1188435 - Support TCP fastopen](https://bugzilla.mozilla.org/show_bug.cgi?id=1188435)

### Keep-Alive

Use Keep-Alive connection (more useful for HTTP/1.X connection than HTTP/2):

```apache
<IfModule mod_headers.c>
	Header set Connection keep-alive
</IfModule>
```

- [HTTP persistent connection — Wikipedia](https://en.wikipedia.org/wiki/HTTP_persistent_connection)

### IPv6

- [98.01% of sites on Cloudflare now use IPv6](https://blog.cloudflare.com/98-percent-ipv6/)
- [IPv6 measurements | Zaid Ali Kahn | Pulse | LinkedIn](https://www.linkedin.com/pulse/ipv6-measurements-zaid-ali-kahn)
- [IPv6: It's time to get on board | Engineering Blog | Facebook Code](https://code.facebook.com/posts/1192894270727351/ipv6-it-s-time-to-get-on-board/)

### Edge side includes

CDN or cache proxy agregade differents resource fragments with cache

- [Solving anything in VCL](https://www.slideshare.net/Fastly/solving-anything-in-vcl#11)
- [Edge Side Includes - Wikipedia](https://en.wikipedia.org/wiki/Edge_Side_Includes)
- [Server Side Includes - Wikipedia](https://en.wikipedia.org/wiki/Server_Side_Includes)
- [EdgeSuite 4.2 ESI Examples](http://esi-examples.akamai.com/)

### Dedicated domains cookies less

Reduce latency server side.

For statics resources (don't require cookies), use a dedicated domain.

With HTTP/2.0 it's no more useful, with [header compression](#header-compression).

### Multiple domains for static resources

Aka domain sharding, domain sharing

Allow multiple parallels requests.

Ex: `static1.example.com` and `static2.example.com`

**Not adviced if you use HTTP/2.0 or HTTPS**

- [Connection management in HTTP/1.x - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Connection_management_in_HTTP_1.x#Domain_sharding)
- [Performance Calendar » Reducing Domain Sharding](https://calendar.perfplanet.com/2013/reducing-domain-sharding/)

### Serve progressive HTML document

Serve the document using chunk encoding.

Note: browser often have a buffer of 4096 bytes

1. Send the HTTP headers
2. the HTML head (title, metas, scripts, styles, etc.)
3. first part of the HTML body
4. (*n) send chunks with `<p class="progress">Progress: XX%...</p>` to show progression
5. send chunk `<p class="progress">Complete</p>`
6. send chunk `<style>.progress{display: none}</style>`
5. send the remains HTML document part

### Precompress

See [Content encoding](#content-encoding)

For all text formats: CSS, SVG, JavaScript

Could also be used for generic data (other formats that don't already use compression), or if the compression mode in those format can be disabled (ex: uncompressed PNG + Content encoding)

- Create a gzip without store the original file name `gzip -9 -k -n file.ext`
- create a TAR of all .ext `COPYFILE_DISABLE=1 tar -cvf file.tar *.ext`
- `Content-Encoding: br` Brotli

- a CDN
- `mod_mem_cache` or `mod_disk_cache`: [webdirect.no Apache caching with gzip enabled | webdirect.no](http://webdirect.no/linux/apache-caching-with-gzip-enabled/)
- a proxy cache like Varnish

#### Server precompressed files with nginx

With nginx [`ngx_http_gzip_static_module`](https://nginx.org/en/docs/http/ngx_http_gzip_static_module.html#example) and [`ngx_brotli`](https://github.com/google/ngx_brotli) (there is no [`ngx_http_brotli_static_module`](https://trac.nginx.org/nginx/ticket/798))

#### Server precompressed files with Apache

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

##### Precompressed files and [`mod_rewrite`](https://httpd.apache.org/docs/current/en/mod/mod_rewrite.html)

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

#### Server precompressed files with Apache and [`mod_negotiation`](https://httpd.apache.org/docs/current/en/mod/mod_negotiation.html)

#####  Precompressed files and `MultiViews`

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

##### Precompressed files and [type maps](http://httpd.apache.org/docs/current/mod/mod_negotiation.html#typemaps)

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

### Multiplexed / Pipelining

HTTP/1.1 has pipelining, but not well supported (by proxies, etc.)
HTTP/2 is multiplexed

- [HTTP/2 Frequently Asked Questions](https://http2.github.io/faq/#why-is-http2-multiplexed)
- [Connection management in HTTP/1.x - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Connection_management_in_HTTP_1.x#HTTP_pipelining)

### TLS

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

### Use dedicated servers

Load balancer, localized CDN, etc.

- [How We Knew It Was Time to Leave the Cloud | GitLab](https://about.gitlab.com/2016/11/10/why-choose-bare-metal/)

### Cache

To control static resource version, **use checksum instead of build number**. Which means you only download a new copy _when it actually changes_ (see ETag).

Use forever cache (cache immutable) for static resources.

- [HTTP Heuristic Caching (Missing Cache-Control and Expires Headers) Explained – Paul Calvano](https://paulcalvano.com/index.php/2018/03/14/http-heuristic-caching-missing-cache-control-and-expires-headers-explained/)
- [Un tutoriel de la mise en cache pour les auteurs Web et les webmestres](https://www.mnot.net/cache_docs/)
- [Increasing Application Performance with HTTP Cache Headers | Heroku Dev Center](https://devcenter.heroku.com/articles/increasing-application-performance-with-http-cache-headers)
- https://restpatterns.mindtouch.us/Articles/Caching_Matters

#### Cached

max-age or expires headers, `Header append Cache-Control "public"`, `Header append Cache-Control "immutable"` avoid check of 304s

`.htaccess`:

```apache
 Requires mod_expires to be enabled.
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
```

PHP:

```php
header('Expires: '.gmdate('D, d M Y H:i:s \G\M\T', time() + (60 * 60 * 24 * 12)));// 2 weeks
```

Varnish script to Handle `Vary: User-Agent` to create classes to reduce variations.

```vcl
 recv
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

 Fetch
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
```

- [Device detection — Varnish version trunk documentation](https://www.varnish-cache.org/docs/trunk/users-guide/devicedetection.html)
- [Achieving a high hitrate — Varnish version trunk documentation](https://www.varnish-cache.org/docs/trunk/users-guide/increasing-your-hitrate.html#http-vary)
- https://github.com/varnishcache/varnish-devicedetect

- [Are Your Cache-Control Directives Doing What They Are Supposed to Do? — theScore Tech Blog](http://techblog.thescore.com/2014/11/19/are-your-cache-control-directives-doing-what-they-are-supposed-to-do/)
- [Caching best practices & max-age gotchas - JakeArchibald.com](https://jakearchibald.com/2016/caching-best-practices/)
- [mnot’s blog: The State of Browser Caching, Revisited](https://www.mnot.net/blog/2017/03/16/browser-caching)

- [RFC 7234 in JavaScript. Parses HTTP headers to correctly compute cacheability of responses, even in complex cases ](https://github.com/pornel/http-cache-semantics)

#### Not cached

Prevent back button to show cache page (ex.: after logout)

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store, must-revalidate
Expires: 0
```

```http
HTTP/1.0 200 OK
Pragma: no-cache
Cache-Control: max-age=0
```

Note: `Cache-Control: no-cache` is for HTTP/1.1 where `Pragma: no-cache` is for HTTP/1.0. See [http - Difference between Pragma and Cache-control headers? - Stack Overflow](https://stackoverflow.com/questions/10314174/difference-between-pragma-and-cache-control-headers/15050018#15050018)

```php
header('Expires: ' . gmdate('D, d M Y H:i:s', time()) . ' GMT');
//header('ETag: "' . sha1(time()) . '"');
```

- [http - Making sure a web page is not cached, across all browsers - Stack Overflow](https://stackoverflow.com/questions/49547/making-sure-a-web-page-is-not-cached-across-all-browsers)

#### Cache partitioning

- [Time to Say Goodbye to Google Fonts](https://web.archive.org/web/20201210165352/https://wicki.io/posts/2020-11-goodbye-google-fonts/)
- [Gaining security and privacy by partitioning the cache  |  Web](https://web.archive.org/web/20201202112031/https://developers.google.com/web/updates/2020/10/http-cache-partitioning)
- [Double-keyed HTTP cache · Issue #904 · whatwg/fetch](https://github.com/whatwg/fetch/issues/904)
- [shivanigithub/http-cache-partitioning](https://github.com/shivanigithub/http-cache-partitioning/)

### Reduce processing

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

### Relayout, repaint, reflow

See [Relayout, repaint, reflow](JavaScript#relayout-repaint-reflow)

## Reduce CPU/GPU usage

- prefer server-side rendering for primary content
- lazy load third party resources with facades
- deliver ES6 modules to up-to-date browsers

- [Small Bundles, Fast Pages: What To Do With Too Much JavaScript | Calibre](https://calibreapp.com/blog/bundle-size-optimization)

Ex., code markup:

- client side: Serve HTML + CSS + JS + Execute JS
- server side: Serve HTML (gzipped, a tiny tiny bit more) + CSS

- [Jake Archibald on Twitter: "I took the code examples from https://t.co/Oyiax6163l and compared with highlighting markup, and without (https://t.co/oIYkvupr2D). After gzip: With highlighting markup: 900b. Without highlighting markup: 723b. PrismJS: 5.2k.… https://t.co/0xcp53jdrB"](https://twitter.com/jaffathecake/status/1113017397655547905) - About syntax highlighting (in a blog post, example, etc.)

Other:

- [Don’t attach tooltips to document.body - Atif Afzal](https://web.archive.org/web/20220315215147/https://atfzl.com/don-t-attach-tooltips-to-document-body) - to invalidated a smaller subtree

## Control loading

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

### `<img>` vs `background-image`

- [Ivan Akulov 🇺🇦 on Twitter: "Moral: don’t use `background-image` for images that are important. They will download too late. More (non-perf) differences between \<img\> and background-image: https://t.co/DK5hbDtCNB"](https://web.archive.org/web/20220318130104/https://twitter.com/iamakulov/status/1504804851854704666)
- [html - When to use IMG vs. CSS background-image? - Stack Overflow](https://stackoverflow.com/questions/492809/when-to-use-img-vs-css-background-image)

### Buffering

Aka dynamic buffering

- [Dynamic Buffering revamping | Video Encoding & Streaming Technologies](https://sonnati.wordpress.com/2006/04/10/dynamic-buffering-revamping/) and [A Dynamic Buffering strategy | Video Encoding & Streaming Technologies](https://sonnati.wordpress.com/2005/12/03/241/) - prebuffer time (used to compute real required buffer size) + buffer to fill 80% at the current speed

### Resource hint

See also dns-prefetch, preconnect, prerender

See [Server Push](#server-push)

```html
<link rel="preload" as="style" href="style.css">
<link rel="prefetch" href="style.css">
```

Preload: load this resource (high priority to low priority based on the value of `as` attribute)
Prefetch: load this resource after all other resources (very low priority), will prefetched the resource when the browser is idle for future navigation

Preload will be started immediately and prefetch will be started only after the main page finishes loading.

Preload should be rarely used and only used for small media files (< 5 MB). It's often used as band-aid for an underlying issue. See [The cost of preload](https://web.archive.org/web/20210616120610/https://docs.google.com/document/u/0/d/1ZEi-XXhpajrnq8oqs5SiW-CXR3jMc20jWIzN5QRy1QA/mobilebasic)

Don't use both preload and prefetch in same time: `<link rel="preload prefetch" as="style" href="style.css">` because they don't have the same purpose. This create potentially 2 requests.

```http
Link: </styles/style.css>; rel=preload; as=style
```

```html
<link rel="preload" as="style" href="style.css">
```

```html
<meta http-equiv="Link" content="</styles/style.css>; rel=preload; as=style">
```

Using JavaScript, but prefer the link / header version:

```html
<script>
var res = document.createElement("link");
res.rel = "preload";
res.as = "style";
res.href = "styles/other.css";
document.head.appendChild(res);
</script>
```

Use [`<link rel="preload" href="styles.css" as="style">`](https://www.w3.org/TR/preload/), work for `fetch`, `audio`, `font`, `image`, `script`, `style`, `track`, `video` and `image`. See [Fetch Standard](https://fetch.spec.whatwg.org/#concept-request-destination)

Use type parameter to specify the format of the resource. It's usefull to let the browser choose the supported format. But should be carefull defined (a browser support all available choices will preload all). In case you want to preload a font available in both WOFF and WOFF2, reclare only the last one (`font/woff2`), because browsers support preload also support this more recent format.

Note about mandatory `as` attribute and valid value:

- [Intent to Implement and ship: Mandatory `as` value for link rel preload - Google Groups](https://groups.google.com/a/chromium.org/forum/#!topic/blink-dev/mKkVXwMhOLc)
- [173047 – \[preload\] Mandatory `as` value and related spec alignments](https://bugs.webkit.org/show_bug.cgi?id=173047)
- [Issue 2903653005: \[preload\] Mandatory `as` value and related spec alignments - Code Review](https://codereview.chromium.org/2903653005)

Reactive prefetch: [Google mobile search is getting faster - to be exact, 100-150 milliseconds fa...](https://plus.google.com/+IlyaGrigorik/posts/ahSpGgohSDo)

```js
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
```

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

### Preload ASAP

As soon as possible, use UDP Priming (pre request like HEAD) to let the server prepare response

Load list by fragments 1+1+X (better than X and 3+7+X) like streaming

- [Optimizing Facebook for iOS start time | Engineering Blog | Facebook Code](https://code.facebook.com/posts/1675399786008080/optimizing-facebook-for-ios-start-time/)

### Download priority

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

### On demand

Aka Lazyload, LOD, defered loading

Use `<noscript>` tags, or handle it with Service Worker (replace all `<img>` by a placeholder). See [`<noscript>` and search engines](#noscript-and-search-engines)

- [`<noscript>` and search engines](#noscript-and-search-engines)
- [Image lazyload](#image-lazyload) and [Non-blocking stylesheet](#non-blocking-stylesheet)
- [Extensible Web Resource Loading Manifesto - igvita.com](https://www.igvita.com/2014/10/02/extensible-web-resource-loading-manifesto/)
- [google - Is this a good approach to image Lazy Loading for SEO? - Webmasters Stack Exchange](http://webmasters.stackexchange.com/questions/26190/is-this-a-good-approach-to-image-lazy-loading-for-seo)
- [Redefining Lazy Loading With Lazy Load XT - Smashing Magazine](http://www.smashingmagazine.com/2015/02/03/redefining-lazy-loading-with-lazy-load-xt/)
- [Lazy loading and the SEO problem, solved! | Idea R Blog](https://www.idea-r.it/blog/110/en/lazy-loading-seo-problem#blogimage=5)
- [Make sure Google can see lazy-loaded content  |  Search  |  Google Developers](https://developers.google.com/search/docs/guides/lazy-loading)

Live streaming, or start play video when the file is not completely generated:

```html
<video>
	<source src="video.m3u8" type="application/x-mpegURL"><!-- HTTP Live Streaming, required by Safari in that case: if the media size is not known -->
	<source src="video.mpd" type="application/dash+xml"><!-- MPEG-DASH -->
	<source src="video.mp4" type="video/mp4"><!-- Use chunk encoding -->
	<!-- Or use JS to use MSE API for streaming protocols like DASH -->
</video>
```

- [MPEG-DASH](MPEG-DASH)
- [Live streaming web audio and video - App Center | MDN](https://developer.mozilla.org/en-US/Apps/Fundamentals/Audio_and_video_delivery/Live_streaming_web_audio_and_video)

#### Image lazyload

Use [`loading="lazy"` attribute](https://developer.mozilla.org/en-US/docs/Web/Performance/Lazy_loading#Images_and_iframes) for images (and iframes)

**Use a placeholder element, or at least [use a SVG in data URI for the `src` attribute](https://css-tricks.com/preventing-content-reflow-from-lazy-loaded-images/#article-header-id-5) to prevent reflow**

1. placeholder shouldn't be visible if script is not available (inlined CSS hide the placeholder)
2. placeholder should have `role="img"` and `aria-label` set with image `alt` (will be set by the JS)
3. should works with complex image content (eg. `<figure>`)

TODO: support all replaced elements: video, audio and iframe. Use a weakmap or additional property to store the replacement fragment (parse noscript HTML only one time)

 ```html
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
```

After a user action or intersection observation (scroll → visible in the viewport), replace the placeholder by the final HTML:

1. Read document visibility `document.visibilityState === "visible" || document.visibilityState === "prerender"`
2. Listen document visibility change `document.addEventListener("visibilitychange", documentVisibilityChange);` if hidden, store which placeholder(s) must be replaced then wait the document to be visible
3. Use the IntersectionObserver API of observe placeholders (currently) in the DOM
4. Use MutationObserver to handle DOM modifications (to observe later attached placeholders or disconnect detached placeholders). See [DOM mutation](../Development/JavaScript/Javascript.md#dom-mutation)
5. Use matchMedia API to match print media (to load all images)

	```js
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
	```
6. Replace placeholders: `placeholder.replaceWith(document.createRange().createContextualFragment(placeholder.dataset.srcdoc));`

	```js
	const range = document.createRange();
	range.selectNode(placeholder.parentNode);
	placeholder.replaceWith(range.createContextualFragment(placeholder.dataset.srcdoc));// Note: createContextualFragment() is supported by IE11+
	```

If the IntersectionObserver API is not supported:

- use the polyfill with caution, it's impact performance (use `getClientBoundingRect()` and `getComputedStyle`) and it's add weight to load. Additional the existing polyfill are not spec compilant, often don't handle visibility, parent non visible overflow or crop, CSS changes, etc.
- or fallback to scroll listener, `setInterval()` with a not too small delay and `getClientBoundingRect()`
- or load all lazyloaded images, it's the default behavior before lazyload has been implemented

See also:

- [`<noscript>` and search engines](#noscript-and-search-engines)
- [Progressive load](#progressive-load)
- [Progressivement en ‹img /› - da scritch net works](https://dascritch.net/post/2014/06/10/Progressivement-en-img#lazyloading)
- [aFarkas/lazysizes: High performance and SEO friendly lazy loader for images (responsive and normal), iframes and more, that detects any visibility changes triggered through user interaction, CSS or JavaScript without configuration.](https://github.com/aFarkas/lazysizes)

### Progressive load

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

```html
<link rel="stylesheet" href="styles/fonts.css" media="print" onload="media!='all'&&media='all'">
<noscript><link rel="stylesheet" href="styles/fonts.css"></noscript>
```

But this still blocking DOM parser on few browsers (IE11, Firefox 36). See https://github.com/scottjehl/css-inapplicable-load#the-bad
Can be use to load fonts (inlined in CSS). Or use preload font

Note: `media!='all'&&...` is required as a workaround for infinite event loop on Firefox, where change media dispatch a new load event.

- [Loading CSS without blocking render by Keith Clark](http://keithclark.co.uk/articles/loading-css-without-blocking-render/)
- [“Async” CSS without JavaScript by Taylor Hunt on CodePen](https://codepen.io/tigt/post/async-css-without-javascript)
- [Fonts and FOXX](CSS#fonts-and-foxx)

See [`<noscript>` and search engines](#noscript-and-search-engines)

### Critical path

Aka blocking dependencies, critical resources

To find blocking points / bottlenecks / critical rendering path

> A critical request is one that contains an asset that is essential to the content within the users viewport
>
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
		- [with the exception of WebKit that "defer execution of async scripts until until the document is loaded by default to reduce time to first paint."](https://trac.webkit.org/changeset/256808/webkit/)
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

#### Anatomy of a webpage

Aka wireframe of a webpage

**Note: always render document server side. All the document content must be delivered.**
JavaScript (client side) can be used to enhance experience (loading, UI elements, etc.). See [Progressive Enhancement](#progressive-enhancement)

**Have things (critical content) before 1000ms.** See [responsiveness](../../UI%20-%20UX/UI%20-%20UX.md#responsiveness)

Anatomy/wireframe of a webpage:

```html
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
		<base ...><!-- if base is used, but not recommended -->

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
		Critical script
		Script for critical content: display a loader, handle critical content interaction/layout while the non critical content is loading.
		Before critical styles to not block JS execution
		See [Critical rendering path](#critical-rendering-path)
		-->
		<script>/*inlined script*/</script>
		<script src="..."></script><!-- Only if pushed with HTTP/2.0 server push before the HTML document -->

		<!--
		Critical styles
		Style for critical content: above floating line (main nav, header, hero image, article) or show a loader, while the rest is loading.
		Shouldn't be used to display aside content: comments, commercial components/ads, popular content, related content, sharing widgets, etc.
		Do not use @import, it's a not recommended as Chrome have an issue with it https://bugs.chromium.org/p/chromium/issues/detail?id=1224629
		See [Critical rendering path](#critical-rendering-path)
		-->
		<style>/*inlined style*/</style>
		<link rel="stylesheet" href="..."><!-- Only if pushed with HTTP/2 server push -->
		<style>.icon{width:1em;height:1em}</style><!-- Use to prevent inlined SVG icons be unscaled -->

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
		<script src="" async></script>
		<script src="" defer></script>
		<script src="" type="module"></script>
		<link rel="stylesheet" href="/path/to/my.css" media="print" onload="media='all'"><!-- /path/to/my.css have a previous preload link tag -->

		<!--
		Metadata, manifest, document relationship, future navigation hint (prefetch, next, prerender), other SEO related tags, Open Graph, etc.
		Some Open Graph fetcher read only first 32k of the page: [Barry Pollard auf Twitter: "So unless your HEAD is more than 32k (in which case have a word with yourself will you!) you should be fine.… "](https://web.archive.org/web/20210211161623/https://twitter.com/tunetheweb/status/1359898874115145729)
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
```

See also [Critical rendering path](#critical-rendering-path) and [Blocking resources](#blocking-resources)

Use HTTP2:

```php
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
```

- [Get Your Head Straight - Speaker Deck](https://web.archive.org/web/20211104095209/https://speakerdeck.com/csswizardry/get-your-head-straight?slide=39) - [Smashing Magazine on Twitter: "🔖 For the bookmarks: Optimum \<head\> order for performance: \<meta /\> \<title\> preconnect \<script async\>\</script\> CSS with @imports sync JS sync CSS preload \<script defer\>\</script\> prefetch / prerender everything else (SEO, icons, open graph) via @csswizardry #webexpo #webperf https://t.co/Xar1kAjCY5" / Twitter](https://web.archive.org/web/20220123115517/https://twitter.com/smashingmag/status/1440697011985018881?s=12)
- [Understanding Critical CSS – Smashing Magazine](https://www.smashingmagazine.com/2015/08/understanding-critical-css/)
- https://github.com/bocoup/critical-css-boilerplate
- [DOMContentLoaded and stylesheets · molily](http://molily.de/domcontentloaded/#appendix)
- [DOMContentLoaded - Event reference | MDN](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded)
- Use progress events for media (img, video and audio) element. See [Image dispatch progress events](JavaScript#image-dispatch-progress-events)
- [CSSconf EU 2014 | Patrick Hamann: CSS and the Critical Path ](https://www.youtube.com/watch?v=_0Fk85to6hA)
- [Deep dive into the murky waters of script loading - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/speed/script-loading/)
- [Faster Pageloads: Effectively using HTTP Caching, Cache Busting, and a CDN](https://web.archive.org/web/20200803114642/https://www.foxy.io/blog/faster-pageloads-effectively-using-http-caching-cache-busting-and-a-cdn/)
- [Your Hero Images Need You: Save the Day with HTTP/2 Image Loading - YouTube](https://www.youtube.com/watch?v=66JINbkBYqw)
- Some [link tag are "body-ok"](https://html.spec.whatwg.org/multipage/links.html#body-ok) (aka allowed in the body, not only in the head)

#### Blocking resources

> Browser requests the HTML document Begins parsing and constructing DOM Discovers CSS/JS Waits for CSS response Constructs CSSOM Combines CSSOM and DOM intro render tree Font requests are dispatched after the render tree indicates which font variants are needed to render the specified text on the page.
>
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

##### Non-blocking stylesheet

Aka async stylesheet

```html
<link rel="preload" href="/path/to/my.css" as="style"><!-- optional, set fetch at highest priority -->
<link rel="stylesheet" href="/path/to/my.css" media="print" onload="media='all'">
```

Depreciated:

```html
<link rel="preload" href="styles.css" as="style" onload="rel='stylesheet';onload=0">
<noscript><link rel="stylesheet" href="styles.css"></noscript>
```

- [The Simplest Way to Load CSS Asynchronously | Filament Group, Inc.](https://web.archive.org/web/20211201142536/https://www.filamentgroup.com/lab/load-css-simpler/#can%E2%80%99t-rel%3Dpreload-do-this-too%3F)

## Reduce media memory usage

For images and videos

By drawing downscaled images when smaller image are required.

- https://github.com/PixelsCommander/CanvasImage

### Compressed textures

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

## Performance reporting

Aka client timing

See JavaScript [Performance API](https://developer.mozilla.org/en-US/docs/Web/API/Performance) (ex: `window.performance.getEntriesByType("resource")`) and `navigator.sendBeacon()`

![HTTPS ClientTimings](https://nickcraver.com/blog/content/HTTPS-ClientTimings.png) — From [Nick Craver - HTTPS on Stack Overflow: The End of a Long Road](https://nickcraver.com/blog/2017/05/22/https-on-stack-overflow/#preparing-for-a-proxy-client-timings)

- [SpeedCurve | Synthetic: WebPageTest](https://speedcurve.com/features/synthetic/)

## AMP

> CSS is limited to 50KB and only inline, custom JS is not allowed (other than via an iframe method), and all images are guaranteed to be lazy loading.
> [...]
> Technically correct AMP pages will perform very similar to any non-horrible web page.
> [...]
> Part of that answer you can probably guess: the cache is simply very fast. It’s hard to compete with a Google-class CDN. I imagine thousands of servers strategically placed worldwide on the best connections available.
> [...]
> on Google Search on mobile [...] Pretty much anything that page needs to render is **preloaded**, whether you actually open it not.
> [...]
> > The AMP page, which we all believe to be super fast and optimized for slow mobiles because it is AMP, isn’t that fast. Its true speed comes from preloading.
>
> — [AMP: the missing controversy – Ferdy Christant](https://ferdychristant.com/amp-the-missing-controversy-3b424031047)

Cache:

- [Overview  |  Google AMP Cache  |  Google Developers](https://developers.google.com/amp/cache/overview#google-amp-cache-updates)
- [Update AMP Content  |  Google AMP Cache  |  Google Developers](https://developers.google.com/amp/cache/update-cache)

Others links:

- [How AMP Works – AMP](https://www.ampproject.org/learn/about-how/)
- [Everything You Need To Know About Google's Accelerated Mobile Pages — Smashing Magazine](https://www.smashingmagazine.com/2016/02/everything-about-google-accelerated-mobile-pages/)
- [Adactio: Journal—AMPstinction](https://adactio.com/journal/13964)
- [Google AMP lowered our page speed, and there's no choice but to use it - unlike kinds](https://unlikekinds.com/amp/article/google-amp-page-speed)

## Third parties webperf

See also [Third parties](../Web.md#third-parties)

- [Hard Costs of Third-Party Scripts - daverupert.com](https://daverupert.com/2018/10/hard-costs-of-third-party-scripts/)
- [How website trackers affect the performance of the world's top news sites](https://royal.pingdom.com/trackers-impact-performance/)
- [Improving third-party web performance at The Telegraph](https://medium.com/the-telegraph-engineering/improving-third-party-web-performance-at-the-telegraph-a0a1000be5)
- [Third-Party Script Prevalence on Alexa Top 50 | Trent Walton](http://trentwalton.com/notes/2018/01/23/third-party-script-prevalence-on-alexa-top-50.html)
- [Loading Third-Party JavaScript  |  Web Fundamentals  |  Google Developers](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/loading-third-party-javascript/)
- [Performance Calendar » Reducing Single Point of Failure using Service Workers](https://calendar.perfplanet.com/2015/reducing-single-point-of-failure-using-service-workers/) - Block slow third-party with service worker
- [Improving third-party web performance at The Telegraph](https://medium.com/the-telegraph-engineering/improving-third-party-web-performance-at-the-telegraph-a0a1000be5) - "delete old third party scripts and see if anyone complains"
- [After GDPR, The New York Times cut off ad exchanges in Europe - and kept growing ad revenue - Digiday](https://digiday.com/media/gumgumtest-new-york-times-gdpr-cut-off-ad-exchanges-europe-ad-revenue/) - "serving regular, un-targeted ads could actually increase revenue" (remove cookie syncing and retargeting, that generate large amount of requests)
- [Andy Davies sur Twitter : "Only load what’s needed to display the initial button and then lazy-load the rest is an approach every live chat, feed widget etc should take. Currently they typically have a 500KB to 1MB bundle which just displays a button unless someone interacts with it!… https://t.co/ZNblwfAVwJ"](https://twitter.com/andydavies/status/1199236204723613696?s=12)
- [Loading Third-Party JavaScript  |  Web Fundamentals  |  Google Developers](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/loading-third-party-javascript/#lazy-load_third_party_resources) - "Lazy-load Third Party Resources"
- [How 3rd Party Scripts can be performant citizens on the web](https://www.twnsnd.com/posts/performant_third_party_scripts.html)
- [Taking Back Control Over Third Party Content – Conffab](https://conffab.com/video/taking-back-control-over-third-party-content/) - Slides: [Taking back control over 3rd party content](https://yoavweiss.github.io/taking_back_control_velocity_16/)
- [Web Performance Calendar » Self-hosting third-party resources: the good, the bad and the ugly](https://calendar.perfplanet.com/2019/self-hosting-third-party-resources-the-good-the-bad-and-the-ugly/)
- [How Third-Party Tags and Trackers Impact Site Performance](https://wp-rocket.me/blog/how-third-party-tags-and-trackers-impact-website-performance/)
- [Third party tags: their impact on web performance - Fasterize](https://www.fasterize.com/en/blog/third-parties-tags-impact-performance/)
- [Third Parties | 2019 | The Web Almanac by HTTP Archive](https://almanac.httparchive.org/en/2019/third-parties)
- [Simon Hearne | Deep dive into third-party performance | performance.now() 2019 - YouTube](https://www.youtube.com/watch?v=uXv9JFvrnwo)
- [Data | Third-Party Web](https://www.thirdpartyweb.today/) - [patrickhulce/third-party-web: Data on third party entities and their impact on the web.](https://github.com/patrickhulce/third-party-web)
- [Analyzing 3rd Party Performance via HTTP Archive + CrUX - Analysis - HTTP Archive](https://discuss.httparchive.org/t/analyzing-3rd-party-performance-via-http-archive-crux/1359)
- [Performance and Resilience: Stress-Testing Third Parties – CSS Wizardry – Web Performance Optimisation](https://csswizardry.com/2017/07/performance-and-resilience-stress-testing-third-parties/#request-blocking)
- [Cloudflare acquires Zaraz to enable cloud loading of third-party tools](https://web.archive.org/web/20220302050546/https://blog.cloudflare.com/cloudflare-acquires-zaraz-to-enable-cloud-loading-of-third-party-tools/)
- [Zaraz use Workers to make third-party tools secure and fast](https://web.archive.org/web/20220302050535/https://blog.cloudflare.com/zaraz-use-workers-to-make-third-party-tools-secure-and-fast/)
