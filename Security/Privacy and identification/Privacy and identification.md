- Hidden input allow the webpage get more infos than the user want to share (with autocomplete)
	* [Oversharing with the browser’s autofill / Stoyan's phpied.com](http://www.phpied.com/oversharing-with-the-browsers-autofill/)
	* https://twitter.com/anttiviljami/status/816585860661518336
- [Have I been pwned? Check if your email has been compromised in a data breach](https://haveibeenpwned.com/)
- [Did you know that the NSA uses Uber Drivers and Soccer Moms to Spy on You?](https://medium.com/@amuse/did-you-know-that-the-nsa-uses-uber-drivers-and-soccer-moms-to-spy-on-you-d912fe74befd)
- [Restore Privacy | Your online privacy resource center](https://restoreprivacy.com/)
- [All Sites - ACCOUNTKILLER.COM](https://www.accountkiller.com/en/all-sites)
- Facebook image tracking data (image identifier)
    - [(1) Edin Jusupovic on Twitter: "#facebook is embedding tracking data inside photos you download. I noticed a structural abnormality when looking at a hex dump of an image file from an unknown origin only to discover it contained what I now understand is an IPTC special instruction. Shocking level of tracking.. https://t.co/WC1u7Zh5gN" / Twitter](https://mobile.twitter.com/oasace/status/1149181539000864769)
    - [IPTC metadata automatically added to uploaded images on Facebook - Stack Overflow](https://stackoverflow.com/questions/31120222/iptc-metadata-automatically-added-to-uploaded-images-on-facebook)
    - [watzon/fbmdob: Facebook image Metadata Obfuscation server](https://github.com/watzon/fbmdob)

- [OSINT Search Tool by IntelTechnique | Open Source Intelligence](https://inteltechniques.com/menu.html)
- [Michael Bazzell' Blog  » Blog Archive   » Updated OSINT Flowcharts](https://inteltechniques.com/blog/2018/03/06/updated-osint-flowcharts/)

## Nothing to hide argument

- [Facebook Graph Shortcuts](http://graph.tips/)
- [Je n'ai rien à cacher.](https://web.archive.org/web/20220204024429/https://jenairienacacher.fr/)
- [Rien à cacher (argument) — Wikipédia](https://fr.wikipedia.org/wiki/Rien_%C3%A0_cacher_%28argument%29)
- [Lettre ouverte à ceux qui n’ont rien à cacher | InternetActu.net](http://www.internetactu.net/2010/05/21/lettre-ouverte-a-ceux-qui-nont-rien-a-cacher/)
- [Google Analytics In Real Life - Online Checkout - YouTube](https://www.youtube.com/watch?v=3Sk7cOqB9Dk)
- Social experiment about privacy about public toilets [Snoopers Charter - Very public toilet - YouTube](https://www.youtube.com/watch?v=_-RSravgi_Y)

## HTTP Referer

Referrer (correct spelling)

- [Everything you could ever want to know (and more) about controlling the Referer header | FastMail Blog](https://blog.fastmail.com/2016/06/20/everything-you-could-ever-want-to-know-and-more-about-controlling-the-referer-header/)
- `Referrer-Policy` HTTP header [Referrer-Policy - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referrer-Policy)
- `<meta name="referrer" content="same-origin">` prevent to transmit referrer (ex: contains a sensitive URL)
- `referrerpolicy` attribute [\<a\> - HTML | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#attr-referrerpolicy)

## Any data can contains private information

Aka redacted, pixelated, unclassified, black box

Uploading a document can expose/leak private data. This data and metadata should be stripped if exposed publicly.

- Any file:
	- File name: [More Than Meets The Eye - The Hacker Factor Blog](http://www.hackerfactor.com/blog/index.php?/archives/565-More-Than-Meets-The-Eye.html) - generator, last used tool/service
- Picture:
	- (EXIF) author
	- (EXIF) location
	- (EXIF) editor
	- human faces
	- plate number
	- serial number
	- credit card number
	- phone number
	- human fingerprint / eye iris
	- user name / account
	- address
	- transparent pixels (of format that support it like `*.png`) could kept original color information, put transparency to 0% reveal original content

	Directly or in reflects
- Word document:
	- author
	- [changes](https://support.office.com/en-us/article/Track-changes-while-you-edit-024158a3-7e62-4f05-8bb7-dc3ecf0295c4), etc.
- PDF document:
	- original OCR data:
- HTTP protocol:
	- Some ISP add specific headers. See [Header Enrichment or ISP Enrichment? Emerging Privacy Threats in Mobile Networks - headerenrichment15.pdf](https://www.icsi.berkeley.edu/pubs/networking/headerenrichment15.pdf)

Metadata:

- [Metadata](Image#medata)
- [Image Scrubber](https://everestpipkin.github.io/image-scrubber/) - [everestpipkin/image-scrubber: A tool for anonymizing photographs taken at protests](https://github.com/everestpipkin/image-scrubber)
- [Metadata removal tool - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Metadata_removal_tool)
- [Remove hidden data and personal information by inspecting documents - Office Support](https://support.office.com/en-us/article/Remove-hidden-data-and-personal-information-by-inspecting-documents-356b7b5d-77af-44fe-a07f-9aa4d085966f)
- [Document Metadata Extraction - ForensicsWiki](http://www.forensicswiki.org/wiki/Document_Metadata_Extraction)
- [Exchangeable image file format - Wikipedia, the free encyclopedia - Privacy and security](https://en.wikipedia.org/wiki/Exchangeable_image_file_format#Privacy_and_security)
- [FotoForensics](http://fotoforensics.com/tutorial-meta.php)

Pixelated text:

- [Never Use Text Pixelation To Redact Sensitive Information | Bishop Fox](https://web.archive.org/web/20220216230121/https://bishopfox.com/blog/unredacter-tool-never-pixelation)
- [beurtschipper/Depix: Recovers passwords from pixelized screenshots](https://github.com/beurtschipper/Depix)

See also:

- [virtualabs.fr - Le dragueur trahi par sa clef USB](https://web.archive.org/web/20200122223609/https://virtualabs.fr/Le-dragueur-trahi-par-sa-clef-USB.html):
- [Source Protection: Sensitive Document Checklist | Global Investigative Journalism Network](https://web.archive.org/web/20171124154646/https://gijn.org/2017/06/19/protecting-sources-when-releasing-sensitive-documents/)
- [Deblur / deconvolution](/Users/mems/Materials/Algorithms/Deblur/Deblur.md)
- [Forensically, free online photo forensics tools - 29a.ch](https://29a.ch/photo-forensics/#forensic-magnifier)
- [AT&#38;T leaks sensitive info in NSA suit - CNET](https://web.archive.org/web/20220217001954/https://www.cnet.com/tech/tech-industry/at-38t-leaks-sensitive-info-in-nsa-suit/)
- https://en.wikipedia.org/wiki/Sanitization_(classified_information)
- [firstlookmedia/pdf-redact-tools: a set of tools to help with securely redacting and stripping metadata from documents before publishing](https://github.com/firstlookmedia/pdf-redact-tools)
- [Let’s Enhance! How we found @rogerkver’s $1,000 wallet obfuscated private key](https://web.archive.org/web/20220131013122/https://www.freecodecamp.org/news/lets-enhance-how-we-found-rogerkver-s-1000-wallet-obfuscated-private-key-8514e74a5433/) - "they showed a few images unblurred of parts of the QR code and the plain text code. The rest was brute forced and reconstructed from the QR code format."
- [Deconstructing Swirl Face | MatzJB](https://web.archive.org/web/20210611023556/https://matzjb.se/2015/07/26/deconstructing-swirl-face/)
- [Why blurring sensitive information is a bad idea | dheera.net | Dheera Venkatraman's web site](https://web.archive.org/web/20140714183916/http://dheera.net/projects/blur)
- [Cryptologists decipher a term censored in a CIA "memo" to George Bush](https://web.archive.org/web/20210915051747/https://cryptome.org/cia-decrypt.htm)
- [forensics - How secure is 'blacking out' sensitive information using MS Paint? - Information Security Stack Exchange](https://security.stackexchange.com/questions/126932/how-secure-is-blacking-out-sensitive-information-using-ms-paint)

## Fingerprinting

- [Entropy](https://en.wikipedia.org/wiki/Entropy_(information_theory))

See also

- [Fingerprinting Protections · brave/brave-browser Wiki](https://github.com/brave/brave-browser/wiki/Fingerprinting-Protections)
- [Temporary user tracking in major browsers and Cross-domain information leakage and attacks](https://web.archive.org/web/20141214141849/http://landing2.trusteer.com/sites/default/files/Temporary_User_Tracking_in_Major_Browsers.pdf)
- [p0f v3](http://lcamtuf.coredump.cx/p0f3/) - P0f is a tool that utilizes an array of sophisticated, purely passive traffic fingerprinting mechanisms to identify the players behind any incidental TCP/IP communications
- [Now sites can fingerprint you online even when you use multiple browsers | Ars Technica UK](https://arstechnica.co.uk/security/2017/02/now-sites-can-fingerprint-you-online-even-when-you-use-multiple-browsers/) - Use WebGL capabilities. See [crossbrowsertracking_NDSS17.pdf](http://yinzhicao.org/TrackingFree/crossbrowsertracking_NDSS17.pdf)
- How advertisers merge user profiles with cookie syncing [Privacy Conference - Keynote: Lorrie Cranor - YouTube](https://www.youtube.com/watch?v=G7QOJ6lmXGg&t=31m20s) (end 40m11s)
- [acsac2016-device-fingerprinting.pdf](http://people.scs.carleton.ca/~paulv/papers/acsac2016-device-fingerprinting.pdf)
- [Security/Anonymous Browsing - MozillaWiki](https://wiki.mozilla.org/Security/Anonymous_Browsing)
- [A Primer on Information Theory and Privacy | Electronic Frontier Foundation](https://www.eff.org/deeplinks/2010/01/primer-information-theory-and-privacy)
- [How Unique Is Your Web Browser?](https://panopticlick.eff.org/browser-uniqueness.pdf)
- [Fingerprinting - MozillaWiki](https://wiki.mozilla.org/Fingerprinting)
- [Zombie cookie — Wikipedia](https://en.wikipedia.org/wiki/Zombie_cookie)
- [HTTP cookie — Wikipedia](https://en.wikipedia.org/wiki/HTTP_cookie#Alternatives_to_cookies)
- [Tracking the Trackers: Microsoft Advertising | Center for Internet and Society](http://cyberlaw.stanford.edu/blog/2011/08/tracking-trackers-microsoft-advertising)
- [BrowserLeaks.com — Web Browser Security Checklist for Identity Theft Protection](https://www.browserleaks.com/)
- [anonymous browser fingerprinting - valve's](http://valve.github.io/blog/2013/07/14/anonymous-browser-fingerprinting/) and https://github.com/Valve/fingerprintjs2
- [Legal Guidelines For The Use Of Location Data On The Web – Smashing Magazine](https://www.smashingmagazine.com/2016/03/location-data-web-development-and-the-law/)
- [Technical analysis of client identification mechanisms - The Chromium Projects](https://www.chromium.org/Home/chromium-security/client-identification-mechanisms)
- [Online tracking: A 1-million-site measurement and analysis](https://webtransparency.cs.princeton.edu/webcensus/index.html)
- [PowerPoint Presentation - Is_preventing_browser_fingerprinting_a_lost_cause.pdf](https://www.w3.org/wiki/images/7/7d/Is_preventing_browser_fingerprinting_a_lost_cause.pdf)
- https://github.com/Valve/fingerprintjs2
- [phaseIII.eps - 1503.01408.pdf](https://arxiv.org/pdf/1503.01408.pdf)
- [JavaScript and Daylight Savings for tracking users. | Application Security](https://www.idontplaydarts.com/2011/10/javascript-and-daylight-savings-for-tracking-users/) - each country have timezone and daylight different rules, across the history
- [Fingerprinting Firefox users with cached intermediate CA certificates (#fiprinca) - shift or die](https://shiftordie.de/blog/2017/02/21/fingerprinting-firefox-users-with-cached-intermediate-ca-certificates-fiprinca/)
- [Printers | Electronic Frontier Foundation](https://www.eff.org/issues/printers) - Pinter watermarks
- [Pixel Perfect: Fingerprinting Canvas in HTML5](https://hovav.net/ucsd/dist/canvas.pdf)

Other

- [Cancel That Card | Share a little](http://cancelthat.cc/), an automated service that tweets at people who post pictures of their credit or debit cards online
- [Privacy - Manage Your Privacy - Apple](http://www.apple.com/privacy/manage-your-privacy/)
- [Privacy - Approach to Privacy - Apple](http://www.apple.com/privacy/approach-to-privacy/)

To protect against entropy and protect privacy (obfuscation): generate noise, fake informations

- [Opt Out From Online Behavioral Advertising By Participating Companies (BETA)](http://www.aboutads.info/choices/)
- [TrackMeNot](http://cs.nyu.edu/trackmenot/)
- [Obfuscation | The MIT Press](https://mitpress.mit.edu/books/obfuscation)
- https://addons.mozilla.org/en-US/firefox/addon/canvasblocker/

Tools to finger print web browsers:

- [Panopticlick](https://panopticlick.eff.org/)
- [Browserprint](https://browserprint.info/)
- [Device Fingerprint](http://noc.to/)

### Timing attack

Can use side-channel leaks (time attack) to measure time of the response for cache data, HSTS, system/browser files, etc.

Use a resource (like image or video).

This example is inaccurate, mainly measure download time (impact of the network) of the resource:

```js
const image = new Image();
image.onerror = function(){
	// Stop timer
	const end = performance.now();
	const delta = end - start;
	console.log(`Loading took ${delta}ms.`);
};
// Start timer
const start = performance.now();
image.src = "https://example.com/admin.php";// invalid image
// The login form page is returned quicker than full admin page (less HTML code to load)
```

An improved example:

```js
const video = document.createElement("video");
let start = NaN;
// suspend event: download complete
video.onsuspend = function(){
	// Start timer
	start = performance.now();
}
// error event: parsing complete
video.onerror = function(){
	// Stop timer
	const end = performance.now();
	const delta = end - start;
	console.log(`Loading took ${delta}ms.`);
};
video.src = "https://example.com/admin.php";// invalid video
```

An other example using Service worker (Cache Storage Attack):

```js
const url = "https://example.com/admin.php";
const dummyRequest = new Request("dummy");
let start = NaN;
fetch(url, {
	credentials: "include",
	mode: "no-cors"
}).then(function(response){
	// download complete
	// Start timer
	start = performance.now();
	return cache.put(dummyRequest, response.clone());
}).then(function(){
	// resource stored in the cache
	// Stop timer
	const end = performance.now();
	const delta = end - start;
	console.log(`Loading took ${delta}ms.`);
})
```

Compare 2 string take less time if string provided is small or start with identical chars (for same length), etc. like using a safe string compare (time is less impacted by optimizations):

```js
// Not executed faster depends b
function safeCompare(a, b) {
	a = String(a);
	b = String(b);
	var length = a.length;
	var result = 0;

	if (length !== b.length) {
		b = a;
		result = 1;
	}

	for (let index = 0; index < length; index++) {
		result |= (a.charCodeAt(index) ^ b.charCodeAt(index));// XOR
	}

	return result === 0;
};
```

Compare password hash, etc.:

See

- [PHP: rfc:timing_attack](https://wiki.php.net/rfc/timing_attack)
- [PHP: hash_equals - Manual](http://php.net/manual/en/function.hash-equals.php)
- [PHP: password_verify - Manual](http://php.net/manual/en/function.password-verify.php)
- [Mathias Bynens — Front-End Performance: The Dark Side on Vimeo](https://vimeo.com/163113209#t=1m34s)
- [sirdarckcat: [Matryoshka] - Web Application Timing Attacks (or.. Timing Attacks against JavaScript Applications in Browsers)](http://sirdarckcat.blogspot.fr/2014/05/matryoshka-web-application-timing.html)
- [Using Node.js Event Loop for Timing Attacks](https://snyk.io/blog/node-js-timing-attack-ccc-ctf/)
- [Dev.Opera — Front-End Performance: The Dark Side](https://dev.opera.com/blog/timing-attacks/)
- [Timing Attacks in the Modern Web - tom.vg](https://tom.vg/2016/08/browser-based-timing-attacks/)
- [Mathias Bynens on Twitter: "More about timing attacks on the web...](https://twitter.com/mathias/status/760359100177846272)
- [Browser-based Timing Attacks](https://labs.tom.vg/browser-based-timing-attacks/)
- [Mathias Bynens — Front-End Performance: The Dark Side on Vimeo](https://vimeo.com/163113209#t=8m22s)
- [Mathias Bynens — Front-End Performance: The Dark Side on Vimeo](https://vimeo.com/163113209#t=15m19s)
- [Academic - VaGoSec](https://vagosec.org/academic/#ccs2015-timing)
- [Constant-Time Character Encoding in PHP Projects](https://github.com/paragonie/constant_time_encoding)
- [Timing attack — Wikipedia](https://en.wikipedia.org/wiki/Timing_attack)

### Private mode

```js
try { localStorage.test = 2; } catch (e) {
	alert('You are in Private Browsing mode (in Safari)');
}
```

Note: will not works with Chrome's Incognito Mode

- [ios - (How) Can a web site determine if Safari Private Browsing is turned on? - Ask Different](http://apple.stackexchange.com/questions/131587/how-can-a-web-site-determine-if-safari-private-browsing-is-turned-on/131588)
- [web browser - Can web sites detect whether you are using private browsing mode? - Information Security Stack Exchange](http://security.stackexchange.com/questions/9037/can-web-sites-detect-whether-you-are-using-private-browsing-mode)

### Native application is installed

iOS and Android

Allow to open native apps with custom arguments

- [Open native application](Web#open-native-application)
- [Twitter detect installed Apps on iOS `canOpenURL`](https://gist.github.com/genadyo/295a5e8f0d743f57137f)
	http://nikf.org/blog/twitter-ads-app-detection
	[Andreas Kurtz on Twitter: "iOS Twitter determines installed apps by checking the 2.551 custom URI schemes (canOpenURL) listed in main bundle's app_store_app_data.json"](https://twitter.com/aykay/status/537976040996749312)
- Discover and Hack URL Handlers: [ouspg/urlhandlers: Discover and Hack URL handlers](https://github.com/ouspg/urlhandlers) and [Discover and Hack URL Handlers (Prototype)](http://hack.urlhandlers.info/)

### Other data

User:

- typing speed
- facial recognition
- vocal inflexions
- room ambiance (sound)
- reflex delay
- interesets
- name
- birth date
- living area

See also:

- [Facebook: 'Nanotargeting' Users Based Solely on Their Perceived Interests - Unite.AI](https://web.archive.org/web/20211021165832/https://www.unite.ai/facebook-nanotargeting-users-based-solely-on-their-perceived-interests/)

Software and hardware:

- protocol supported / used (+ meta data in this protocol)
	* [Fingerprinting Browsers Using Protocol Handlers](http://itsecuritysolutions.org/2010-03-29_fingerprinting_browsers_using_protocol_handlers/)
	* [Links to local pages do not work - MozillaZine Knowledge Base](http://kb.mozillazine.org/Links_to_local_pages_don't_work)
	* [browser - Open Explorer window from Website - Stack Overflow](https://stackoverflow.com/questions/1431112/open-explorer-window-from-website)
	* [Per-domain Configurable Security Policies are no longer available (Affected) | Firefox Site Compatibility](https://www.fxsitecompat.com/en-CA/docs/2014/per-domain-configurable-security-policies-are-no-longer-available/)
- format supported by the video, audio, image (Accept header and Accept-Encoding) same as OS+Hardware+browser ?
- Canvas fingerprint, same as OS+Hardware+browser
	* [Canvas fingerprinting — Wikipedia](https://en.wikipedia.org/wiki/Canvas_fingerprinting)
	* https://www.browserleaks.com/canvas
- Video decoder finderprint: Colors are not decoded the same way and can cause a difference
	* https://stackoverflow.com/questions/28603552/html5-video-color-difference-chrome-internet-explorer
	[Digital video fingerprinting — Wikipedia](https://en.wikipedia.org/wiki/Digital_video_fingerprinting)
- `getClientRects()` fingerpint (browser rendering engine, fonts installed)
	* [Advanced Tor Browser Fingerprinting](http://jcarlosnorte.com/security/2016/03/06/advanced-tor-browser-fingerprinting.html#getclientrects-fingerprinting)
- `AudioContext` fingerprint
	* [AudioContext Fingerprint Test Page](https://audiofingerprint.openwpm.com/)
- browser (User-Agent header)
- screen size, color depth, pixel ratio, GPU
	* `screen.*`
	* [WEBGL_debug_renderer_info - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_debug_renderer_info)
- battery status
	> When battery is running low, people might be prone to some - otherwise different - decisions
	— [Battery Status readout as a privacy risk](https://blog.lukaszolejnik.com/battery-status-readout-as-a-privacy-risk/)

	> When your phone is down to 5 per cent battery and that little icon on the iphone turns red, people start saying I’d better get home or I don’t know how I’m going to get home otherwise
	— [Keith Chen Is Uber's Head Of Economics And Decides When Uber Surges Price : NPR](http://www.npr.org/2016/05/17/478266839/this-is-your-brain-on-uber)

	> The amount of battery users had left was “one of the strongest predictors of whether or not you are going to be sensitive to surge” – in other words, agree to pay 1.5 times, 2 times or more the normal cost of a journey
	— [Uber knows when your phone is running out of battery | The Independent](http://www.independent.co.uk/life-style/gadgets-and-tech/news/uber-knows-when-your-phone-is-about-to-run-out-of-battery-a7042416.html)
- OS
- CPU speed (use webworker for intensive task)
- available plugins
- time zone
- cookies and other storages systems (`window.name`, Web Storage, browser cache)
	* [Samy Kamkar - evercookie - virtually irrevocable persistent cookies](http://samy.pl/evercookie/) and [samyk/evercookie: Produce persistent, respawning "super" cookie in a browser, abusing over a dozen techniques. It goal i to identify user after they've removed standard cookie and other privacy data such a Flash cookie (LSOs), HTML5 storage, SilverLight storage, and others.](https://github.com/samyk/evercookie)
- Mouse move and mouse wheel deltas
- History via
	- CSS `:visited` selector (before March 2010) https://developer.mozilla.org/en-US/docs/Web/CSS/Privacy_and_the_:visited_selector [Jeremiah Grossman: I know where you've been](http://blog.jeremiahgrossman.com/2006/08/i-know-where-youve-been.html)
	- HSTS (detect to detect history of HTTPS visited websites using HSTS)
		- [Sniffy](https://zyan.scripts.mit.edu/sniffly/) and https://github.com/diracdeltas/sniffly
		- [RadicalResearch HSTS Super Cookies](http://www.radicalresearch.co.uk/lab/hstssupercookies)
		- [Anatomy of a browser dilemma – how HSTS ‘supercookies’ make you choose between privacy or security – Naked Security](https://nakedsecurity.sophos.com/2015/02/02/anatomy-of-a-browser-dilemma-how-hsts-supercookies-make-you-choose-between-privacy-or-security/)
		- [Protecting Against HSTS Abuse | WebKit](https://webkit.org/blog/8146/protecting-against-hsts-abuse/)
		- [Criteo’s Shares Plummet on Revenue Forecast - WSJ](https://www.wsj.com/articles/criteos-shares-plummet-on-revenue-forecast-1513279308) - "using HTTP Strict Transport Security Protocol, usually used to secure web connections, allowed it to create a user ID without cookies"
	- cache systems (ServiceWorkers, HTTP headers ETags, etc.)
	- cross domain cookies
- system/browser files (load with iframe src, etc.): `res://C:\\Program Files\\Fiddler2\\Fiddler.exe/#3/#32512`, `chrome://ghostery/content/options.html`, `resource:///defaults/preferences/firefox.js`
	* [863246 – resource:// URIs leak information](https://bugzilla.mozilla.org/show_bug.cgi?id=863246)
	* https://github.com/beefproject/beef/wiki/Module:-browser-fingerprint
	* https://blog.malwarebytes.com/cybercrime/exploits/2016/06/neutrino-ek-fingerprinting-in-a-flash/ http://malware.dontneedcoffee.com/2014/10/cve-2013-7331-and-exploit-kits.html
- available fonts
- geolocation
- IP address
- language(s) (Accept-Language header)
- cookies disabled, javascript disabled, popup disabled
- [Device fingerprint — Wikipedia](https://en.wikipedia.org/wiki/Device_fingerprint) [TCP/IP stack fingerprinting — Wikipedia](https://en.wikipedia.org/wiki/TCP/IP_stack_fingerprinting)
- installed apps
- OS/Browser UI: (macOS, Windows, Linux) scrollbar size, input default styles, etc.
- third party autentification
	Use login auth mecanisms to detect if the user is logged in:

	```html
	<img onload="alert('logged in to Facebook')" onerror="alert('not logged in to Facebook')" src="https://www.facebook.com/login.php?next=https%3A%2F%2Fwww.facebook.com%2Ffavicon.ico">
	```

	- use [`SameSite`](https://www.owasp.org/index.php/SameSite) cookies
	- [Your Social Media Fingerprint](https://robinlinus.github.io/socialmedia-leak/)
- The feature, font used in a document can used to detect the original creation date / year
	- [Les polices de caractères incorporées dans des outils comme Office pourraient servir d'indicateurs, pour détecter les fraudeurs](https://www.developpez.com/actu/149640/Les-polices-de-caracteres-incorporees-dans-des-outils-comme-Office-pourraient-servir-d-indicateurs-pour-detecter-les-fraudeurs/)
	- [Dani Rodrik's weblog: Did Microsoft steal its fonts from the Turkish army?](http://rodrik.typepad.com/dani_rodriks_weblog/2012/10/did-microsoft-steal-its-fonts-from-the-turkish-army.html)
	- [How Microsoft’s Calibri font doomed Sharif family in Panama Case – Daily Pakistan](https://en.dailypakistan.com.pk/pakistan/how-microsofts-calibri-font-doomed-sharif-family-in-panama-case/)

## Email hash

For CRM matching often use email hash (MD5 or SHA256).

Email hash shouldn't be considered as pseudonymised data. It's an identifier ("personal data" as GDPR sens).

- [hash - Anonymous Gravatar Problem - Cryptography Stack Exchange](https://crypto.stackexchange.com/questions/22936/anonymous-gravatar-problem)
- [Four cents to deanonymize: Companies reverse hashed email addresses](https://web.archive.org/web/20210113201618/https://freedom-to-tinker.com/2018/04/09/four-cents-to-deanonymize-companies-reverse-hashed-email-addresses/)
- [Gravatar - Globally Recognized Avatars](https://en.gravatar.com/site/implement/hash/) - Gravatar use MD5 email hashes
