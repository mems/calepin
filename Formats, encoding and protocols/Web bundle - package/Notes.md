- [packages.md](https://gist.github.com/wycats/220039304b053b3eedd0)
- [zip fragments](https://gist.github.com/annevk/6295844) and [zip URLs](https://gist.github.com/annevk/6174119)
- [HTML Resource Packages](http://wayback.archive.org/web/20130226043223/http://people.mozilla.org/~jlebar/respkg/)
- [Packaged Web Apps (Widgets) - Packaging and XML Configuration (Second Edition)](http://www.w3.org/TR/widgets/)
- [Making browsers faster: Resource Packages — Alex Limi](http://limi.net/articles/resource-packages/)
- [Asset bundles for faster page fetching (fewer requests to the server) from jxtps435 on 2009-11-08 (public-html-comments@w3.org from November 2009)](https://lists.w3.org/Archives/Public/public-html-comments/2009Nov/0003.html)
- [new HTML feature: <link rel="cache" type="application/zip" href="small-files.zip" /> from Kuzma Deretuke on 2010-02-08 (public-html-comments@w3.org from February 2010)](https://lists.w3.org/Archives/Public/public-html-comments/2010Feb/0012.html)
- [[whatwg] An BinaryArchive API for HTML5? from Gregg Tavares on 2009-07-30 (whatwg@whatwg.org from July 2009)](https://lists.w3.org/Archives/Public/public-whatwg-archive/2009Jul/0918.html)
- [ECMAScript 6 modules in future browsers](http://www.2ality.com/2013/11/es6-modules-browsers.html#bundling)
- [[whatwg] Zip archives as first-class citizens from Anne van Kesteren on 2013-08-28 (public-whatwg-archive@w3.org from August 2013)](https://lists.w3.org/Archives/Public/public-whatwg-archive/2013Aug/0278.html)
- [Packaging on the Web](https://w3ctag.github.io/packaging-on-the-web/)
- [WebAPI/ArchiveAPI - MozillaWiki](https://wiki.mozilla.org/WebAPI/ArchiveAPI)
- [Zip - WHATWG Wiki](https://wiki.whatwg.org/wiki/Zip)
- [Open Archives Initiative Protocol - Object Exchange and Reuse](http://www.openarchives.org/ore/)

- [Vulnerability Note VU#715737 - Mozilla-based browsers jar: URI cross-site scripting vulnerability](http://www.kb.cert.org/vuls/id/715737)

Use `Content-Encoding: gzip`, only if `Accept-Encoding: gzip`

## HTTP/2.0

In flavor of HTTP/2 "push" mode ([draft-ietf-httpbis-http2-17 - Hypertext Transfer Protocol version 2 - 8.2. Server Push](https://tools.ietf.org/html/draft-ietf-httpbis-http2-17#section-8.2))

> We ultimately decided to scrap resource packages in favor of HTTP pipelining and spdy, each of which gets you most of the speedup you'd get with packaging but doesn't require changes to web content.
— [681967 – Web packaging format](https://bugzilla.mozilla.org/show_bug.cgi?id=681967#c4)

- [Link prefetching FAQ - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Link_prefetching_FAQ)
- [LINK rel=subresource - The Chromium Projects](http://www.chromium.org/spdy/link-headers-and-server-hint/link-rel-subresource)

An possible use of Service Workers (replace Application Cache/Cache Manifest) with [FetchEvent](https://developer.mozilla.org/en-US/docs/Web/API/FetchEvent)

## Service Worker as proxy

Use regular URLs

Defining bundles location can be required:

	<link rel="assetbundle" src="/assetbundle.zip" ...>
	<link rel="cache" type="application/zip" href="small-files.zip">
	<link rel="resource-package" type="application/zip" href="site-resources.zip">

## `message/http` with a body that is Multipart MIME

Or `multipart/form-data` or `multipart/mixed`

	http://someplace.com/somearchive.tgz!/myimage.png

	For unsupported browsers load the full URL where supporte only archive

	MIME-Version: 1.0
	Content-Type: multipart/mixed; boundary="|||"
	--|||
	Content-Type: image/gif
	.......(base64).....
	--|||--

- [MIME — Wikipedia](https://en.wikipedia.org/wiki/MIME)
- [Content-Type: multipart](https://msdn.microsoft.com/en-us/library/ms527355%28v=exchg.10%29.aspx)
- [http - application/x-www-form-urlencoded or multipart/form-data? - Stack Overflow](https://stackoverflow.com/questions/4007969/application-x-www-form-urlencoded-or-multipart-form-data)

## Serialized JavaScript

- https://github.com/wavesoft/jbb
- [JBB: Javascript Binary Bundles for faster resource loading](http://wavesoft.github.io/javascript-binary-bundles)

## App manifest

- https://github.com/meryn/parse-appcache-manifest/blob/master/src/parse-appcache-manifest.coffee