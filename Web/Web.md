> The web is not one platform.
> It is a multitude of platforms, most of which you’ll never test on.
> — Peter-Paul Koch

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

```http
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
```

It's used also for form upload with `multipart/form-data` used only by HTTP requests

### Multiple Choices

```http
HTTP/1.1 300 Multiple Choices
Link: <http://example.org/books/1234>; rel="alternate"; type="application/hal+json", <http://example.org/books/1234>; rel="alternate"; type="application/hal+xml", <http://example.org/books/1234>; rel="alternate"; type="application/atom+xml;type=entry"
```

```http
HTTP/1.1 300 Multiple Choices
Content-type: text/uri-list

# metadata
URI1
# metadata
URI2
```

- [RFC 2483 - URI Resolution Services Necessary for URN Resolution # The `text/uri-list` Internet Media Type](http://tools.ietf.org/html/rfc2483#section-5)

### External-Body type

Note: It's used by emails

Set `Content-Type` to:

```http
message/external-body; access-type=URL; URL="http://www.foo.com/file"
```

```http
message/external-body; access-type=local-file; name="file:/local/path/file.html"
```

- [RFC 2017 - Definition of the URL MIME External-Body Access-Type](https://tools.ietf.org/html/rfc2017)

## Server environnements

1. local
2. development (or testing, integration) (could have a dedicated env. for Quality Assurance and User acceptance Testing)
3. staging, uat, preprod
4. production

- [Deployment environment — Wikipedia](https://en.wikipedia.org/wiki/Deployment_environment)

## Detection

**Always use feature detection (Don't sniff User Agent! Never!)** instead of browser/platform detection. Easyer client side with JavaScript or CSS.

> `var webkit = !document.uniqueID && !window.opera && !window.globalStorage`: old code that evaluates to true in IE, Opera + Firefox today.
> — [Mike Taylor on Twitter](https://twitter.com/miketaylr/status/598211928272437248)

- [Browserhacks](http://browserhacks.com/)
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

```apache
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
```

## Analytics

Tracking and analytics

Use [Navigator.sendBeacon() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)

### Tracking data

- page view
- printing

	```html
	<link rel="stylesheet" href="track_printing.css" media="print" type="text/css" />
	```

	`track_printing.css` (should be served with header that disable cache):

	```css
	body { background: url("http://path.to/tracker_script"); }
	```
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

```html
<script type="text/javascript">
	(window._gaq = _gaq || []).push(
		["_setAccount", "UA-XXXXX-X"],
		["_trackPageview"]
	);
	(function(d,t,s,l) {s=d.createElement(t),l=d.getElementsByTagName(t)[0];s.async=true;s.src="http"+("https:"==document.location.protocol?"s://ssl":"://www")+".google-analytics.com/ga.js";l.parentNode.insertBefore(s,l);})(document, "script");
</script>
```

```js
_gaq.push(["_trackEvent", category, action, label/*optional*/, value/*integer, optional*/, opt_noninteraction/*boolean, optional*/]);
```

- [Introduction to ga.js (Legacy)  |  Analytics for Web (ga.js)  |  Google Developers](https://developers.google.com/analytics/devguides/collection/gajs/)
- [Google Analytics Tracking Code  |  Analytics for Web (ga.js)  |  Google Developers](https://developers.google.com/analytics/devguides/collection/gajs/methods/)

#### Universal Analytics tracking library

Aka `analytics.js`

[Universal Analytics tracking library (analytics.js)](https://developers.google.com/analytics/devguides/collection/analyticsjs/):

 ```js
ga("send", "event", category, action, label/*optional*/, value/*integer, optional*/, noninteraction/*boolean, optional*/);
ga("send", "event", category, action, label/*optional*/, value/*integer, optional*/, {nonInteraction: noninteraction}/*boolean, optional*/);
```

```html
<!-- Google Analytics -->
<script>
window.ga=window.ga||function(){(ga.q=ga.q||[]).push(arguments)};ga.l=+new Date;
ga("create", "UA-XXXXX-Y", "auto");
ga("send", "pageview");
</script>
<script async src="https://www.google-analytics.com/analytics.js"></script>
<!-- End Google Analytics -->
```

For a custom function name: (ex: `__gaTracker`)

```html
<!-- Google Analytics -->
<script>
(function(w,n){w.GoogleAnalyticsObject=n;w[n]=w[n]||function(){(w[n].q=w[n].q||[]).push(arguments)};w[n].l=+new Date;})(window,"__gaTracker");
__gaTracker("create", "UA-XXXXX-Y", "auto");
__gaTracker("send", "pageview");
</script>
<script async src="https://www.google-analytics.com/analytics.js"></script>
<!-- End Google Analytics -->
```

GoogleAnalyticsObject

```js
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
```

- [Adding analytics.js to Your Site  |  Analytics for Web (analytics.js)  |  Google Developers](https://developers.google.com/analytics/devguides/collection/analyticsjs/)
- [The ga Command Queue Reference  |  Analytics for Web (analytics.js)  |  Google Developers](https://developers.google.com/analytics/devguides/collection/analyticsjs/command-queue-reference)

 ```js
// Use beacon or fallback to xhr (instead of image)
ga("set", "transport", navigator.sendBeacon ? "beacon" : "xhr");
```

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

```js
_gaq.push(['_trackPageview', path/*optional*/]);

ga("set", {page: path, title: title});/*optional, if need to defined a different location and title than the current document location
ga("send", "pageview");
```

- [Single Page Application Tracking  |  Analytics for Web (analytics.js)  |  Google Developers](https://developers.google.com/analytics/devguides/collection/analyticsjs/single-page-applications)

#### Tracking scripts errors

Track errors, like front end (`window.onerror`) or backend errors with https://developers.google.com/analytics/devguides/collection/analyticsjs/exceptions

```js
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
```

- [Website Exception Monitoring Template](https://www.google.com/analytics/web/template?uid=dPxbEfBpSOWlNBQvG_l85g)
- https://stackoverflow.com/questions/21718481/report-for-exceptions-from-google-analytics-analytics-js-exception-tracking
- https://davidwalsh.name/track-errors-google-analytics

## Anchor hash tag behaviour

- (prefered) use an anchor (`<span id="target"></span>`) in targeted element (don't use `a` without `href`) (via `position: absolute; top: -200px;` etc.). Position absolute can also be used, to prevent autoscroll
- (on click on link) `event.preventDefault();`, `history.pushState()` (`window.location.hash` will scroll automatically, so need to override `document.body.scrollTop` and `document.body.scrollLeft` after changing its value)
- rename target IDs. Some browser keep in memory the position of the previous ID

- `History.scrollRestoration = "manual"` https://developer.mozilla.org/en-US/docs/Web/API/History/scrollRestoration
- http://lea.verou.me/2011/05/change-url-hash-without-page-jump/
- http://css-tricks.com/hash-tag-links-padding/
- [Autoscroll to anchors](JavaScript#autoscroll-to-anchors)

## in frame blocking

```js
<script>
	if (self !== top) {
		document.body.style.display = "none";
		top.location = self.location;
	}
</script>
```

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
	Use only I-Frames or B-frames (B for bidirectional frame). See [Frame types](../Formats,%20encoding%20and%20protocols/Video/Video.md#frame-types)
3. use images:
	Can use format like [APNG](../Formats,%20encoding%20and%20protocols/PNG/PNG.md#APNG), [MNG](../Formats,%20encoding%20and%20protocols/PNG/PNG.md), [JNG](../Formats,%20encoding%20and%20protocols/Image/Image.md#jng), [Animated WebP](../Formats,%20encoding%20and%20protocols/WebP/WebP.md), SVG (animation), [QTVR](../Formats,%20encoding%20and%20protocols/MOV/MOV.md#quickTime-vr), tar archive contains images and data files.
	If multiple images use the same container, [content encoding](#content-encoding) could be used to compress more (GZip, Brotli) to reduce redonancy between images. For JPEG, use same DCT coefficients and omit it to reduce weight.
	Use codecs of [compressed texture format](../Formats,%20encoding%20and%20protocols/Texture%20format/Texture%20format.md), JPEG, PNG, etc.

	1. images diff (pixels + metadata) and draw the patched image (frames: `I,P,P,P...`) `P` images could refer to the I frame or to the previous P frame (see [how APNG works](../Formats,%20encoding%20and%20protocols/PNG/PNG.md#apng))
		Need fine control of playback
	2. bunch of images loaded into blobs and load into the DOM (IMG or Canvas or via ImageData) and drawn on canvas (frames: `I,I,I,I...`)

Examples, using differents methods:

- iPhone 5 webpage
	- [iPhone 5 website teardown: How Apple compresses video using JPEG, JSON, and \<canvas\>](https://web.archive.org/web/20201009042250/https://docs.google.com/document/pub?id=1GWTMLjqQsQS45FWwqNG9ztQTdGF48hQYpjQHR_d1WsI)
	- [iPhone 5 web teardown: How Apple compresses video using JPEG, JSON, and canvas | Hacker News](https://news.ycombinator.com/item?id=4531088)
- [Video Packer Player](https://web.archive.org/web/20151220090428/http://www.bigbossstudio.com/packed_player/index.html)
- [samiare/whitewater-mobile-video: An encoding system for playing inline videos on the mobile web.](https://github.com/samiare/whitewater-mobile-video)
- Phosphor:
	- [Phosphor - divergent media](https://web.archive.org/web/20161115144939/http://www.divergentmedia.com/phosphor#overview)
	- [Phosphor Manual - divergent media](https://web.archive.org/web/20170608060127/http://www.divergentmedia.com/support/documentation/phosphor)
	- [divergentmedia/phosphorframework: Player framework for Phosphor encoded video content](https://github.com/divergentmedia/phosphorframework)
	- https://itunes.apple.com/us/app/phosphor/id589654268
	- http://chrisdowling.biz/demos/phosphor-filesize/
- Sublimetext:
	- [sublimehq/anim_encoder](https://github.com/sublimehq/anim_encoder)
	- [Animated GIFs the Hard Way | Hacker News](https://news.ycombinator.com/item?id=4532146)
- Mac Pro webpage
	- [How Apple made the new Mac Pro web page - YouTube](https://www.youtube.com/watch?v=-Qo9BAI4TQE)
	- [Apple Mac Pro page deconstructed](https://web.archive.org/web/20160607153247/https://ihatetomatoes.net/apple-mac-pro-page-deconstructed/)

- [Image Sequences: Let Me Count The Ways « Thomas Reynolds](http://awardwinningfjords.com/2012/03/08/image-sequences.html) - Use CSS animation or Canvas or DOM image suite

## Third parties

> Don't trust your third parties

See also [Third parties webperf](./Optimizations%20and%20performances.md#third-parties-webperf)

Comments services alternatives:

- [Replacing Disqus with Github Comments · Gazoo.vrv](http://donw.io/post/github-comments/)
- [Comments - Social Plugins](https://developers.facebook.com/docs/plugins/comments/)

### Website JS plugins

To isolate a third party script (or DOM access, geolocation, modal APIs, etc.), use:

- iframe with a cross origin (third party origin or null), ex: iframe with sandbox attribute but without `allow-same-origin`
- a virutal machine like [QuickJS](https://bellard.org/quickjs/) ([bellard/quickjs](https://github.com/bellard/quickjs)) or [Duktape](https://github.com/svaarala/duktape) or [any other JS engine](https://github.com/GoogleChromeLabs/jsvu#supported-engines-per-os) (that could be cross-compiled to WebAssembly)
    - [maple3142/wasm-jseval: A safe eval library based on WebAssembly and Duktape/QuickJS.](https://github.com/maple3142/wasm-jseval)
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

## Web Application

- [Script to create custom shortcuts on the iOS springboard. Check it out at: http://dev.fokkezb.nl/shortcutter](https://gist.github.com/FokkeZB/5899387) - Generate data URI HTML document (to bookmark), allow to start native apps with custom arguments
- [Shortcuts JS](https://shortcuts.fun/)

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

## Privacy

Aka GDPR or EU Cookie Law, law and privacy legislations

See also [Cookies](#cookies)

See Do Not Track https://www.eff.org/dnt-policy [`navigator.doNotTrack`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/doNotTrack) https://en.wikipedia.org/wiki/Do_Not_Track

- [Cookies - Comment vraiment respecter la loi ? - Korben](http://korben.info/respecter-loi-cookies-site.html)
- [Cookies - European commission](http://ec.europa.eu/ipg/basics/legal/cookies/index_en.htm)
- [5 steps to make sure you are compliant with the EU Cookie Directive | Reason Digital](http://reasondigital.com/advice-and-training/5-steps-to-make-sure-you-are-compliant-with-the-eu-cookie-directive/)
- [Europe is planning to finally scrap those annoying cookie pop-ups on websites](http://www.businessinsider.fr/us/europe-plans-remove-cookie-pop-ups-banners-websites-leaked-law-draft-consent-2016-12/)

## Cookies

See also [Privacy](#privacy)

- [Cookie Status :: Current Status Of Browser Tracking Prevention | cookiestatus.com](https://www.cookiestatus.com/)

## App Download Interstitials

- [Google+: A case study on App Download Interstitials](http://googlewebmastercentral.blogspot.ca/2015/07/google-case-study-on-app-download-interstitials.html)
- [Mobile-friendly web pages using app banners](http://googlewebmastercentral.blogspot.ca/2015/09/mobile-friendly-web-pages-using-app.html)

## App Association

### Open native application

- [ios - How to check if an app is installed from a web-page on an iPhone? - Stack Overflow](https://stackoverflow.com/questions/13044805/how-to-check-if-an-app-is-installed-from-a-web-page-on-an-iphone)
- [ios - Is it possible to register a http+domain-based URL Scheme for iPhone apps, like YouTube and Maps? - Stack Overflow](https://stackoverflow.com/questions/1108693/is-it-possible-to-register-a-httpdomain-based-url-scheme-for-iphone-apps-like)
- [URL schemes for iOS and Android (1/2)](https://gist.github.com/FokkeZB/6340484) - [URL schemes for iOS and Android (1/2) | Fokke Zandbergen](https://fokkezb.nl/2013/08/26/url-schemes-for-ios-and-android-1/)
- [URL schemes for iOS and Android (2/2)](https://gist.github.com/FokkeZB/6635236) - [URL schemes for iOS and Android (2/2) | Fokke Zandbergen](https://fokkezb.nl/2013/09/20/url-schemes-for-ios-and-android-2/)

### App Install Banner

```html
<meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL">

<link rel="manifest" href="/manifest.json">
```

```json
{
	"prefer_related_applications": true,
	"related_applications": [
		{
			"platform": "play",
			"id": "com.google.samples.apps.iosched"
		}
	]
}
```

- [Promoting Apps with Smart App Banners](https://developer.apple.com/library/mac/documentation/AppleApplications/Reference/SafariWebContent/PromotingAppswithAppBanners/PromotingAppswithAppBanners.html)
- [Increasing Engagement with Web App Install Banners  |  Web  |  Google Developers](https://developers.google.com/web/updates/2015/03/increasing-engagement-with-app-install-banners-in-chrome-for-android#native)

### Android App Links

Android App Link: `https://<domain>/.well-known/assetlinks.json`

- [Handling Android App Link  |  Android Developers](https://developer.android.com/training/app-links/)
- [Verify Android App Link  |  Android Developers](https://developer.android.com/training/app-links/verify-site-associations#the-difference)
- http://example.digitalassetlinks.org/.well-known/assetlinks.json

### Apple App Site Association

Aka AASA or Universal Links

`https://<domain>/apple-app-site-association` or `https://<domain>/.well-known/apple-app-site-association` without redirect (200 OK only)

Fetch/apdated when (no expired):

- app install
- app update

Can't use MITM to handle/override association (certificate pinning)

- [security - Are Universal Link cached in iOS? Do they work offline? - Stack Overflow](https://stackoverflow.com/questions/41305334/are-universal-links-cached-in-ios-do-they-work-offline/41305871#41305871)
- [App Search Programming Guide: Support Universal Links](https://developer.apple.com/library/archive/documentation/General/Conceptual/AppSearch/UniversalLinks.html)
- [Universal Link – A Few Thing to be Prepared for – Shine Solution Group](https://shinesolutions.com/2017/06/15/universal-linking-a-few-things-to-be-prepared-for/)

## Dummy and placeholder media

Aka Video test pattern, test image, sample image

See [Sample files](../Formats,%20encoding%20and%20protocols/Sample%20files)

```
data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='450' height='300'/%3E
```

16/9 image:

```
data:image/svg+xml,%3Csvg xmlns='w3.org/2000/svg' viewBox='0 0 16 9' width='16' height='9'%3E%3C/svg%3E
```

 ```svg
<svg version="1.1" xmlns="http://www.w3.org/2000/svg">
	<g stroke="purple" stroke-width="2">
		<line x1="0" y1="0" x2="100%" y2="100%"/>
		<line x1="100%" y1="0" x2="0" y2="100%"/>
		<rect x="0" y="0" width="100%" height="100%" fill="none" stroke-width="4" />
	</g>
</svg>
```

```svg
<svg version="1.1" xmlns="http://www.w3.org/2000/svg">
	<g stroke="purple" stroke-width="2">
		<line x1="14.64%" y1="14.64%" x2="85.36%" y2="85.36%"/>
		<line x1="85.36%" y1="14.64%" x2="14.64%" y2="85.36%"/>
		<ellipse cx="50%" cy="50%" rx="50%" ry="50%" fill="none" stroke-width="4"/>
	</g>
</svg>
```

## Web fonts

See [CSS - Font web safe](../Development/CSS/CSS.md#font-web-safe)

## Favicon

For icons, use a large one 180×180 icon for iOS and Android

Some browsers usally try to get the following resource: `/favicon.ico`

```svg
<svg xmlns="http://w3.org/2000/svg" viewBox="0 0 100 100">
    <text y=".9em" font-size="90">📦</text>
</svg>
```

- `convert favicon.png -background none -resize 256×256 -define icon:auto-resize="256,128,96,64,48,32,16" favicon.ico`
- [Thumbnails -- IM v6 Examples](http://www.imagemagick.org/Usage/thumbnails/#favicon)
- [audreyr/favicon-cheat-sheet: Obsessive cheat sheet to favicon sizes/types. Please contribute! (Note: this may be in flux as I learn new things about favicon best practices.)](https://github.com/audreyr/favicon-cheat-sheet)
- [FavIcon from Pics -- free favicon.ico for your website (animated, static, text, iPod icons)](http://favicon.htmlkit.com/favicon/)
- [How iOS scales the Apple Touch icon - Favicon's blog](https://realfavicongenerator.net/blog/how-ios-scales-the-apple-touch-icon/)
- [How Android Chrome scales down icons - Favicon's blog](https://realfavicongenerator.net/blog/how-android-chrome-scales-down-icons/)
- [Favicon Generator for all platforms: iOS, Android, PC/Mac...](http://realfavicongenerator.net/)
- https://github.com/RealFaviconGenerator/realfavicongenerator/issues/211
- https://github.com/GoogleChrome/lighthouse/issues/291#issuecomment-219074630
- [Favicon — Wikipedia](https://en.wikipedia.org/wiki/Favicon)
- [(1) Lea Verou on Twitter: "Now that all modern browsers support SVG favicons, here's how to turn any emoji into a favicon.svg: &lt;svg xmlns="https://t.co/TJalgdayix" viewBox="0 0 100 100"&gt; &lt;text y=".9em" font-size="90"&gt;💩&lt;/text&gt; &lt;/svg&gt; Useful for quick apps when you can't be bothered to design a favicon! https://t.co/S2F8IQXaZU" / Twitter](https://twitter.com/LeaVerou/status/1241619866475474946)

## Browsers

### Browsers version fragmentation

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

### User Agent String

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

### Browsers extension

#### Web Extensions

Chrome, Firefox, Edge, Safari

#### Safari Extensions

##### Safari App Extension

- [Safari App Extension | Apple Developer Documentation](https://developer.apple.com/documentation/safariservices/safari_app_extensions)

##### Safari Extension

Depreciated by Safari 12

Use [xar](https://en.wikipedia.org/wiki/Xar_%28archiver%29)

```sh
xar -x -f XXXXX.safariextz
```

Ex: https://safari-extensions.apple.com/details/?id=com.diigo.safari.awesomescreenshot-5DXNM3K2CT

```js
(new URL(window.ex.render.install_link(window.ex.data.getItemByID((new URL(location)).searchParams.get("id"))), document.baseURI)).href
```

### Kiosk mode

- Chrome: `chrome --chrome --fullscreen --kiosk URI`
    - `chrome --kiosk "https://example.com"`, see also `--kiosk-printing` and `--chrome-frame`
    - [Running latest Chrome for Windows in kiosk mode - Super User](https://superuser.com/questions/716426/running-latest-chrome-for-windows-in-kiosk-mode)
- Opera: `opera -kioskmode -noexit URI`
- Firefox: `firefox --headless URI`
    - `firefox --kiosk`
    - [158968 - command line option for kiosk mode](https://bugzilla.mozilla.org/show_bug.cgi?id=158968)
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

### Firefox

Awesome bar:

> - Add `^` to search for matches in your browsing history.
> - Add `*` to search for matches in your bookmarks.
> - Add `+` to search for matches in pages you've tagged.
> - Add `%` to search for matches in your currently open tabs.
> - Add `~` to search for matches in pages you've typed.
> - Add `#` to search for matches in page titles.
> - Add `@` to search for matches in web addresses (URLs).
> - Add `$` to search for matches in suggestions.
– [Awesome Bar - Search your Firefox bookmarks, history and tabs from the address bar | Firefox Help](https://support.mozilla.org/en-US/kb/awesome-bar-search-firefox-bookmarks-history-tabs#w_changing-results-on-the-fly_2)

- Open Tabs to the right of the current tab: `about:config?filter=browser.tabs.insertAfterCurrent`, https://addons.mozilla.org/en-US/firefox/addon/always-right/

Source code:

- [Phabricator](https://phabricator.services.mozilla.com/)
- [Viewing and searching Mozilla source code online - Mozilla | MDN](https://developer.mozilla.org/en-US/docs/Mozilla/Tech/Viewing_and_searching_Mozilla_source_code_online)
- [mozilla-central - DXR](https://dxr.mozilla.org/mozilla-central/source/)
- [Firefox DevTools](https://github.com/firefox-devtools)

Dev tools:

- [client · mozilla-central](https://phabricator.services.mozilla.com/source/mozilla-central/browse/default/devtools/client/;4e6dd979ed238a6c0be55ecfb8a42d6ca417d865)
- [protocol.md - mozsearch](https://searchfox.org/mozilla-central/source/devtools/docs/backend/protocol.md)
- [Remote Debugging Protocol · GitBook](https://docs.firefox-dev.tools/backend/protocol.html)

#### Network debug

- [HTTP logging - Mozilla | MDN](https://developer.mozilla.org/en-US/docs/Mozilla/Debugging/HTTP_logging)

#### Session / tabs

1. open `about:support` (profile directory)
2. open the directory
3. open the sub directory `sessionstore-backups`

Files in this directory:

- `previous.jsonlz4`: cleanBackup: copy of sessionstore.js from previous session that was loaded successfully
- `recovery.jsonlz4`: latest version of the sessionstore written during runtime
- `recovery.baklz4`: previous version of the sessionstore written during runtime
- `upgrade.jsonlz4-<build_id>`: backup created during an upgrade of Firefox

See also:

- [Session History Scrounger for Firefox (with lz4 support) — Fx File Utilities](https://www.jeffersonscher.com/ffu/scrounger.html) - read file format in `sessionstore-backups` directory

#### Integrated authentication

Aka silent authentication

> authenticate the user to an Intranet server or proxy without prompting the user for a username or password

- [HTTP authentication - The Chromium Projects](https://www.chromium.org/developers/design-documents/http-authentication)
- [microHOWTO: Configure Firefox to authenticate using SPNEGO and Kerberos](http://www.microhowto.info/howto/configure_firefox_to_authenticate_using_spnego_and_kerberos.html)
- [Integrated Authentication - Mozilla | MDN](https://developer.mozilla.org/en-US/docs/Mozilla/Integrated_authentication)
- [header - Authentication issues with WWW-Authenticate: Negotiate - Stack Overflow](https://stackoverflow.com/questions/4265975/authentication-issues-with-www-authenticate-negotiate)

1. go to `about:config`
2. accept harmful consequences warning
3. search `network.negotiate-auth.trusted-uris` and update with value `.example.com` to allow auto login on that domains
4. if required, search `network.negotiate-auth.allow-non-fqdn` and set to `true` to allow non fully qualified domain names in the previous given list

For the list of trusted URIs, see:

- `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\CurrentVersion\Internet Settings\ZoneMap\Domains`
- [Internet Explorer security zones registry entries for advanced users](https://support.microsoft.com/en-us/help/182569/internet-explorer-security-zones-registry-entries-for-advanced-users)
- [How to configuring IE Site Zone mapping using group policy without locking out the user](http://www.grouppolicy.biz/2012/07/how-to-configuring-ie-site-zone-mapping-using-group-policy-without-locking-out-the-user/)

### Safari

Source code:

- [trunk dans webkit. – WebKit](http://trac.webkit.org/browser/webkit/trunk)
- https://sourcegraph.com/search?q=repo%3Awebkit%2Fwebkit+%s

Dev tools:

- [WebInspectorUI dans webkit/trunk/Source. – WebKit](http://trac.webkit.org/browser/trunk/Source/WebInspectorUI)

### Chrome

- [List of Chromium Command Line Switches « Peter Beverloo](https://peter.sh/experiments/chromium-command-line-switches/)
- [Version Selection - ChromeDriver - WebDriver for Chrome](https://chromedriver.chromium.org/downloads/version-selection)
- [Index of chromium-browser-snapshots/](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html)
- [Download Chromium - The Chromium Projects](https://www.chromium.org/getting-involved/download-chromium)
- [Version Numbers - The Chromium Projects](https://www.chromium.org/developers/version-numbers)
- [OmahaProxy - Google Chrome](https://omahaproxy.appspot.com/) - Look up information about a given Chrome release
- [Chromium Dash](https://chromiumdash.appspot.com/schedule)
- `https://crrev.com/<branch_position|commit>`
- `https://storage.googleapis.com/chromium-find-releases-static/d4a.html#<commit>`
- `https://omahaproxy.appspot.com/deps.json?version=<version>` (`Major.Minor.Branch.Patch`)

Source code:

- [chromium Git repositories - Git at Google](https://chromium.googlesource.com/)
- [Code Search](https://cs.chromium.org/)

Dev tools:

- [ChromeDevTools](https://github.com/ChromeDevTools)
- [Chrome DevTools Protocol Viewer - latest (tip-of-tree)](https://chromedevtools.github.io/devtools-protocol/tot/)
- [GoogleChrome/puppeteer: Headless Chrome Node.js API](https://github.com/GoogleChrome/puppeteer)

Skia:

- [CSS Paint Times and Page Render Weight - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/speed/css-paint-times/)
- [skia/tools/skp at master · google/skia](https://github.com/google/skia/tree/master/tools/skp)
- [skia/Viewer.cpp at master · google/skia](https://github.com/google/skia/blob/master/tools/viewer/Viewer.cpp)
- [Skia Viewer](https://skia.org/user/sample/viewer)
- [How can i write a SkBitmap to a file - Google Groups](https://groups.google.com/forum/#!topic/skia-discuss/dsUqLOATq94)
- [How to save .skp files from Chromium - The Chromium Projects](https://www.chromium.org/developers/how-tos/trace-event-profiling-tool/saving-skp-s-from-chromium)
- [skia/modules/canvaskit at master · google/skia](https://github.com/google/skia/tree/master/modules/canvaskit)

Enable Chrome developer tools experiments:

1. chrome://flags/#enable-devtools-experiments
2. webdev tools "Settings"
3. webdev tools "Experiment" tab
4. press "Shift" 6 times to show more experiments

#### Network debug

NetLog log:

- queueing delay to schedule DNS resolves to threads
- stalls due to exceeding socket pool limits
- attempts to do a TCP connect to an IP address
- speculative DNS resolves
- proxy resolution
- cache hits for DNS resolves
- reads/writes from disk cache
- network change events
- proxy configuration change events
- stalls due to chrome extensions pausing requests
- errors
- cookie store

> Features needing reliable network information should never be built on top of NetLog
> - [NetLog: Chrome’s network logging system - The Chromium Projects](https://www.chromium.org/developers/design-documents/network-stack/netlog)

- chrome://net-export/#
- [List of event types](https://chromium.googlesource.com/chromium/src/+/refs/heads/master/net/log/net_log_event_type_list.h)
- [How to capture a NetLog dump - The Chromium Projects](https://www.chromium.org/for-testers/providing-network-details)
- `--net-log-capture-mode=IncludeCookiesAndCredentials` or `IncludeSocketBytes` `--log-net-log=/path/to/file` (ex: `netlog.json` or `net-export/chrome-net-export-log.json`)
- [Analyzing Network Traffic Logs (NetLog json) | text/plain](https://textslashplain.com/2020/04/08/analyzing-network-traffic-logs-netlog-json/)
- [NetLog viewer](https://netlog-viewer.appspot.com/#events)
- [chromium tools - chrome_proxy/webdriver/common.py](https://chromium.googlesource.com/chromium/src/tools/+/6dd06e1a895bd96e385f3bacd13d2c7a84a69915/chrome_proxy/webdriver/common.py#668) and [chromium catapult - netlog_viewer/netlog_viewer/log_util.js](https://chromium.googlesource.com/catapult/+/refs/heads/master/netlog_viewer/netlog_viewer/log_util.js#250) - About the invalidity of NetLog output when used with `--log-net-log` and a workaround
- [NetLog: Chrome’s network logging system - The Chromium Projects](https://www.chromium.org/developers/design-documents/network-stack/netlog)
- [Life of a URLRequest](https://chromium.googlesource.com/chromium/src/+/master/net/docs/life-of-a-url-request.md)
- [NetLog viewer sources](https://chromium.googlesource.com/catapult/+/master/netlog_viewer/)
- [Importateurs de violoneux](https://blog.arcoptimizer.com/importateurs-de-violoneux)
- [ericlaw1979/FiddlerImportNetlog: Fiddler Importer for Chromium NetLog .json files](https://github.com/ericlaw1979/FiddlerImportNetlog)
- Event time: `new Date(data.constants.timeTickOffset + parseInt(event.time))`
- [Network Traffic Annotations](https://chromium.googlesource.com/chromium/src/+/master/docs/network_traffic_annotations.md) and [tools/traffic_annotation - chromium/src](https://chromium.googlesource.com/chromium/src/+/refs/heads/master/tools/traffic_annotation/) - "What is the intent behind each network request". See also `DefineNetworkTrafficAnnotation`

To know what extension handle requests (marked as `307 Internal Redirect`, see `delegate_info`, `CHROME_EXTENSION_REDIRECTED_REQUEST`, `URL_REQUEST_FAKE_RESPONSE_HEADERS_CREATED`)

```js
const readline = require("readline");
const {createReadStream} = require("fs");

async function readNetLogFile(file, eventFilter = null){
  const readlineIterable = readline.createInterface({
    input: createReadStream(file),
    crlfDelay: Infinity,
  });

  let result = null;

  const useEventFilter = typeof eventFilter === "function";

  let parent = null;
  lineLoop: for await(const line of readlineIterable){
    switch(true){
      // header
      case line.startsWith("{\"constants\":"):{
        result = {
          ...JSON.parse(line.slice(0, -1) + "}"),
          events: [],
          polledData: null,
        };// remove trailing comma and add the closing parenthese
        break;
      }
      // start events section
      case line.startsWith("\"events\":"):
        parent = "events";
        break;
      // event
      case parent === "events":{
        const eof = line.endsWith("]}");
        const isLastEvent = eof || line.endsWith("],");
        // If it's the last event, before next section
        // then skip the events array close braket and trailing comma
        // else skip the trailing comma
        const rawData = line.slice(0, isLastEvent ? -2 : -1);
        const event = JSON.parse(rawData);

        // Filter events
        if(!useEventFilter || eventFilter(event, result)){
          result.events.push(event);
        }

        if(eof){
          parent = null;
          break lineLoop;
        }

        if(isLastEvent){
          parent = null;
        }
        break;
      }
      // footer
      case line.startsWith("\"polledData\":"):
        // TODO
        break;
      // EOF
      case line === "}":
        parent = null;
        break lineLoop;
      default:
    }
  }

  return result;
}
```

#### Custom device with higher granularity

https://developer.chrome.com/devtools/docs/device-mode#custom-devices

```
trunk/Source/devtools/front_end/emulation/EmulatedDevices.js


WebInspector.settings.createSetting("customEmulatedDeviceList", [])

in customEmulatedDeviceList each entry:
.capabilities = [];//["touch","mobile"]
.type = "notebook";//"phone"//"tablet"//"unknown"
For default value: 0 or ""

WebInspector.EmulatedDevicesList.dispatchEventToListeners(WebInspector.EmulatedDevicesList.Events.CustomDevicesUpdated);


chrome.experimental.devtools.*

https://api.github.com/repos/GoogleChrome/devtools-device-data/contents/devices.json?ref=release
https://github.com/GoogleChrome/devtools-device-data/blob/release/devices.json

~/Library/Application Support/Google/Chrome/Default/Preferences
JSON: devtools.preferences.customEmulatedDeviceList parse as JSON
```

#### Update loop

> Nearly up to date! Relaunch Google Chrome to finish updating.

- [How to fix chrome update loop "Nearly up-to-date! Relaunch Google Chrome to finish updating. Relaunch" - Tech Antidote](https://techantidote.com/fix-problem-nearly-up-to-date-relaunch-google-chrome-to-finish-updating-relaunch/)

### How a web browser works

inter-frame, event loop

Caches: ( Application DNS cache) → ( libc DNS cache ) → ( gateway DNS cache ) → ( DNS caching resolver cache ) → ( DNS nameserver authoritative cache ) → Filesystem Cache → Hard disk Device Cache → ( JavaScript JIT cache ) → HTTP cache → HTTP push cache → HTTP Preload cache → CPU L1 → CPU L2 → (CPU L3) → ( HTTP proxy cache ) → (N hops invoking many of these steps N times) → ( HTTP router/relay cache ) → ( HTTP Reverse Proxy cache ) → HTTP Server request caching. (add also CSS cache and Image cache)

See also [How ECMAScript engine works](..//Development/ECMAScript/ECMAScript.md#how-engine-works) (event loop, etc.)

- [Demystifying Browsers | text/plain](https://textslashplain.com/2020/02/09/demystifying-browsers/)
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
- event loop
    - Event loop: frame (vsynced): input (events) → Javascript and rAF → Frame commit (style, layout, paint, compose) (→ idle callbacks?); then other frame (vsynced); With the exception of intersection observers & element resize observers, which happen after raf.
    - [requestAnimationFrame Scheduling For Nerds – Medium](https://medium.com/@paul_irish/requestanimationframe-scheduling-for-nerds-9c57f7438ef4)
    - [atotic/event-loop: event loop docs](https://github.com/atotic/event-loop)
- [High-performance browser-grade HTML5 parser](https://github.com/servo/html5ever)
- [Lazy frame construction - Google Groups](https://groups.google.com/forum/#!topic/mozilla.dev.tech.layout/k_ZKKNQOpjw)
- [Call stack from a URL typed by a user to the HTTP request](https://gist.github.com/mildred/1c12cd7b4af6f24c145b)
- [Design Elements](https://github.com/v8/v8/wiki/Design%20Elements) - About V8, ECMAScript engine used in Chromium and NodeJS
- [requestAnimationFrame Scheduling For Nerds – Paul Irish – Medium](https://medium.com/@paul_irish/requestanimationframe-scheduling-for-nerds-9c57f7438ef4)
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
- [Why Did Mozilla Remove XUL Add-ons?](https://yoric.github.io/post/why-did-mozilla-remove-xul-addons/)
- [Using Hardware to Decode and Load JPG Images up to 45% faster in Internet Explorer 11 – IEBlog](https://blogs.msdn.microsoft.com/ie/2013/09/12/using-hardware-to-decode-and-load-jpg-images-up-to-45-faster-in-internet-explorer-11/)

### Headless browser

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

#### Headless browser detection

It's a [cat-and-mouse game](https://en.wikipedia.org/wiki/Cat_and_mouse)

- [puppeteer-extra/packages/puppeteer-extra-plugin-stealth at master · berstend/puppeteer-extra](https://github.com/berstend/puppeteer-extra/tree/master/packages/puppeteer-extra-plugin-stealth) - Puppeteer plugin to prevent detection
- [Detecting Chrome Headless](http://antoinevastel.github.io/bot%20detection/2017/08/05/detect-chrome-headless.html)
- [berstend/puppeteer-extra: 💯 Teach puppeteer new tricks through plugins.](https://github.com/berstend/puppeteer-extra)
- [puppeteer-extra/packages/puppeteer-extra-plugin-recaptcha at master · berstend/puppeteer-extra](https://github.com/berstend/puppeteer-extra/tree/master/packages/puppeteer-extra-plugin-recaptcha)
- [Detecting Chrome headless | Hacker News](https://news.ycombinator.com/item?id=14936025)
- [How to bypass “slider CAPTCHA” with JS and Puppeteer](https://medium.com/@filipvitas/how-to-bypass-slider-captcha-with-js-and-puppeteer-cd5e28105e3c)

### Reader view

Firefox Reader view, based on Readability:

- [QA/Reader view - MozillaWiki](https://wiki.mozilla.org/QA/Reader_view)
- https://github.com/mozilla/readability/blob/c3c91a739beab6fd067404cd7610f6d64f53ad5a/Readability.js#L1721
- [javascript - How Does Firefox Reader View Operate (FF version 38.0.5) - Stack Overflow](https://stackoverflow.com/questions/30661650/how-does-firefox-reader-view-operate-ff-version-38-0-5/)
- [mozilla-release mozilla/toolkit/components/reader/ReaderMode.jsm](https://mxr.mozilla.org/mozilla-release/source/toolkit/components/reader/ReaderMode.jsm)
- [How to disable firefox's reader view from my website? - Stack Overflow](https://stackoverflow.com/questions/30615447/how-to-disable-firefoxs-reader-view-from-my-website)
- [Reader View - Chrome Web Store](https://chrome.google.com/webstore/detail/reader-view/ecabifbgmdmgdllomnfinbmaellmclnh) - [rNeomy/reader-view: Access Firefox's built in reader view from right click context menu](https://github.com/rNeomy/reader-view),

Safari reader mode, based on Readability:

- [Masquer les publicités et les distractions dans Safari sur l’iPhone - Assistance Apple](https://support.apple.com/fr-fr/guide/iphone/iphdc30e3b86/ios)
- `/Applications/Safari/Contents/Resources` (`Reader.html`, `ReaderThumb.png`, `ReaderTrack.png`, `ReaderBg.png`, `ScratchBg.png`)
- [Thoughts on Safari Reader’s generated HTML · Mathias Bynens](https://mathiasbynens.be/notes/safari-reader-html)
- [How to enable Safari Reader on your site? · Mathias Bynens](https://mathiasbynens.be/notes/safari-reader)

> 1. open safari web inspector.
> 2. disable (pause) Javascript in the Safari console debugger
> 3. open a web page that can be view in reader mode

See also [Safari Reader Source Code](http://blog.manbolo.com/2013/03/18/safari-reader-source-code) and [anonyme.js](https://gist.github.com/euskadi31/ec3e82bf94da2ea9bd430a5f3a1042af) (`ReaderArticleFinder`)

Other:

- [Mercury by Postlight](https://mercury.postlight.com/) - [postlight/mercury-parser: 📜 Extract meaningful content from the chaos of a web page](https://github.com/postlight/mercury-parser)

### "Request Desktop Site"

On mobile browsers

## Links and alternate

Canonical URL = the preferred URL (same document content, aka duplicated content)
Alternate URL = other version of this canonicalized document (mobile or other lang)

For languages alternate, each canonicalized document must include the list of all languages available, even itself

**Use alternate URL only for canonicalzed documents**

![hreflang and canonical links relations](http://www.rebelytics.com/wp-content/uploads/2015/06/hreflang-canonical.jpg)

On desktop:

```html
<link rel="alternate" media="only screen and (max-width: 640px)" hreflang="en-gb" href="http://m.example.com/page">
```

or via http header:

```http
Link: <http://m.example.com/page>; rel="alternate"; hreflang="en-gb"; media="only screen and (max-width: 640px)"
```

And on mobile:

```html
<link rel="canonical" href="http://www.example.com/page">
```

For HTTPS page (on `http://www.example.com/page`):

```html
<link rel="canonical" href="https://www.example.com/page">
```

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

```
Date#toJSON()
```

```php
date('c', time());
$date->format(DateTime::ATOM/*use it instead of ISO8601*/);
```

```php
$date = new DateTime("2010-07-05T06:00:00Z");
// To offset with a timezone:
$date->setTimeZone(new DateTimeZone("Europe/Amsterdam");
```

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

> 1. open Chrome
> 2. open a white page:
>     1. open a new tag
>     2. write this URL in address bar + enter : about:blank
> 3. open developement tools:
>     - Crtl+Maj+I
>     - or Menu at the top right (< ⁝ >), then "More tools", then "Developement tools"
>     - or right clic on page, then "Inspect"
> 4. enable history logs perservation:
>     1. open "Console" tab
>     2. open the menu "Console settings" (< ⚙️ >)
>     3. check "Preserve log"
> 5. enable requests history perservation:
>     1. open "Network" tab
>     2. check "Preserve log"
> 6. follow your scenario: **keep developement tools opened in background**
>     1. open the first page (in the browser tab by write/pasting it URL in the address bar + enter)
>     2. the follow the rest of the scenario
> 7. once the scenario is complete, **without closing the browser tab**, show the developement tools window
> 8. save console logs:
>     1. go to "Console" tab
>     2. right click on the main area (where you see yellow, red and white entries)
>     3. choose "Save as..."
> 9. save requests hisoty:
>     1. go to "Network" tab
>     2. right click on the main area (where you see all logged entries)
>     3. choose "Save all as HAR with content"
> 10. send us both saved files

## Cross domain & integrity

- `integrity` `<script>` and `<link>` attribute
- `crossorigin` `<script>`, `<img>` attribute
- `noreferrer`
- `noopener`
- `X-Frame-Options` header (depreciated)
- `Content-Security-Policy` header

See [XSS and injection prevention](../Security/Data%20access%20and%20integrity/Data%20access%20and%20integrity.md#xss-and-injection-prevention)

### Subresource checksum

JavaScript:

```js
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
```

PHP:

```php
$script = 'alert("Hello, world.");';
$algo = 'sha256';// 'sha384' // 'sha512'
$script_hash = base64_encode(hash($algo, $script, true));
header('Content-Security-Policy: default-src \'self\'; script-src \'self\' \''.$algo.'-'.$script_hash.'\'');// sha256-qznLcsROx4GACP2dm0UCKCzCG+HiZ1guq6ZZDob/Tng= or sha512-YWIzOWNiNzJjNDRlYzc4MTgwMDhmZDlkOWI0NTAyMjgyY2MyMWJlMWUyNjc1ODJlYWJhNjU5MGU4NmZmNGU3OAo=
echo '<script>'.$script.'</script>';
```

Command line (sh, openSSL):

```sh
echo sha256-$(echo -n 'alert("Hello, world.");' | openssl dgst -sha256 -binary | openssl enc -base64 | tr -d '\n')
```

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

```http
Server-Timing: cache;desc="Cache Read";dur=23.2,fs;dur=600;desc="File System",cpu;dur=1230;desc="Total CPU"
```

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

```js
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
```

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

- tools for browser for users or authors: zoom and font size settings, [reduce motion](https://developers.google.com/web/updates/2019/03/prefers-reduced-motion), [custom font](https://www.dyslexiefont.com/en/chrome-extension/), screen reader, [colors inversion](http://adrianroselli.com/2017/11/os-high-contrast-versus-inverted-colors.html), video sub titles, keyboard navigation, [etc.](https://chrome.google.com/webstore/category/collection/accessibility))
- advice against using web accessibility overlay tools / add-on accessibility / plug and play solutions ([accessiBe](https://en.wikipedia.org/wiki/AccessiBe), Facil'iti)
    - [Web accessibility overlay tools: lies and gum balls - Le Lutin du Web](https://www.lelutinduweb.fr/en/web-accessibility-overlays-lies-gum-balls/)
    - [Be Wary of Add-on Accessibility | Adrian Roselli](https://web.archive.org/web/20201111022804/https://adrianroselli.com/2015/11/be-wary-of-add-on-accessibility.html)
    - [#accessiBe Will Get You Sued | Adrian Roselli](https://adrianroselli.com/2020/06/accessibe-will-get-you-sued.html)
    - [2019 Review: AccessiBe Automatic Website Solution Accessibility Using AI | Kris Rivenburgh](https://krisrivenburgh.com/2019-review-accessibe-automatic-website-solution-accessibility-using-ai/)
    - [Web Accessibility Overlays Don't Work](https://web.archive.org/web/20201005172019/https://blog.tenon.io/web-accessibility-overlays-dont-work)
    - [Les outils de surcouche d’accessibilité web : mensonges et boules de gomme - La Lutine du Web](https://web.archive.org/web/20201015162302/https://www.lalutineduweb.fr/surcouche-accessibilite-web-mensonges-boules-gommes/)
- [Accessibility: The Missing Ingredient – A List Apart](https://alistapart.com/article/accessibility-the-missing-ingredient/)
- [thetuttingtutor/accessibility-disability-justice: Accessibility and disability justice resources](https://github.com/thetuttingtutor/accessibility-disability-justice)
- [WebAIM: Articles](https://webaim.org/articles/)
- [Accessibility Wins, curated by Marcy Sutton](https://a11ywins.tumblr.com/)
- [Home - The A11Y Project](https://www.a11yproject.com/)
- [An Alphabet of Accessibility Issues](https://the-pastry-box-project.net/anne-gibson/2014-july-31) - Blind, color blind, epilepsy, poor hearing, vertigo, fractured multiple fingers
- [Mobile Dyslexic – Get this Extension for 🦊 Firefox (en-US)](https://addons.mozilla.org/en-US/firefox/addon/mobile-dyslexic/) - "Mobile Dyslexic replaces all fonts of all web pages with carefully crafted special font which is easier to read by people with dyslexia."

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

## A/B testing

![Lifecycle of client-side vs server-side experimentations](https://blog.optimizely.com/wp-content/uploads/2017/05/fullstackblog3.png)

- [Why Experiment Server-Side? - DZone Web Dev](https://dzone.com/articles/why-experiment-server-side)
- [A/B testing - Wikipedia](https://en.wikipedia.org/wiki/A/B_testing)

## Content blocking

Safe Browsing (UrlSubresourceFilter, BetterAds)

- [Category:Ad blocking software - Wikipedia](https://en.wikipedia.org/wiki/Category:Ad_blocking_software)
- [Ad blocking - Wikipedia](https://en.wikipedia.org/wiki/Ad_blocking)
- [Chromium Blog: Under the hood: How Chrome's ad filtering works](https://blog.chromium.org/2018/02/how-chromes-ad-filtering-works.html)
- [Bloqueur de publicités de Chrome : EasyList utilisé pour le blocage, de nouveaux détails](https://www.nextinpact.com/news/106147-bloqueur-publicites-chrome-easylist-utilise-pour-blocage-nouveaux-details.htm)
- [Here’s how Google Chrome’s new ad blocker works – Ctrl blog](https://www.ctrl.blog/entry/chrome-adblocker)
- [Should web browsers adopt Google’s new selective ad blocking tech? – Ctrl blog](https://www.ctrl.blog/entry/google-adblocking-competition)
- `chrome://components/`
- [Blockthrough/PageFair Adblock Reports | Blockthrough](https://blockthrough.com/pagefair-annual-adblock-reports/)
- [2019 US ad-blocking usage report – eyeo GmbH](https://eyeo.com/2019-us-ad-blocking-usage-report/)

- ITP (Intelligent Tracking Prevention) used by Safari - third party cookies isolation
	- [Intelligent Tracking Prevention 2.0 | WebKit](https://webkit.org/blog/8311/intelligent-tracking-prevention-2-0/)
	- [ITP Debug Mode in Safari | Simo Ahava's blog](https://web.archive.org/web/20201205112922/https://www.simoahava.com/privacy/itp-debug-mode-in-safari/)
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
- `/System/Library/PrivateFrameworks/SafariSafeBrowsing.framework`

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

Aka source map, VLQ, variable-length quantity

For CSS and JavaScript

- [DIY source maps / Stoyan's phpied.com](https://www.phpied.com/diy-source-maps/)
- [Source Mapper](https://sourcemaps.info/)
- [Source Map Revision 3 Proposal](https://sourcemaps.info/spec.html)
- [mozilla/source-map: Consume and generate source maps.](https://github.com/mozilla/source-map)
- [Introduction to JavaScript Source Maps - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/developertools/sourcemaps/)
- [Source maps: languages, tools and other info · ryanseddon/source-map Wiki](https://github.com/ryanseddon/source-map/wiki/Source-maps%3A-languages%2C-tools-and-other-info)
- [Anatomy of source maps | Bugsnag Blog](https://www.bugsnag.com/blog/source-maps)
- [Decoding and Encoding Base64 VLQs in Source Maps - Lucidchart](https://www.lucidchart.com/techblog/2019/08/22/decode-encoding-base64-vlqs-source-maps/)
- [Yet another explanation on sourcemap - NGUYEN Trung - Medium](https://medium.com/@trungutt/yet-another-explanation-on-sourcemap-669797e418ce)
- [SourceMap - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/SourceMap)
- [Rich-Harris/sourcemap-codec: Encode/decode sourcemap mappings](https://github.com/Rich-Harris/sourcemap-codec)
- [source-map-visualization](https://sokra.github.io/source-map-visualization/)
- [lydell/source-map-visualize: Quickly open an online source map visualization with local files](https://github.com/lydell/source-map-visualize)

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

## Parties

- first party: the host, the application
- second party: CDN (substitution)
- [third parties](#third-parties)
