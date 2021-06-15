> it's a common misconception that JavaScript isn't an elegant language. The real issue is that it's the only language with a monopoly. So people who want to work on the web have to use it. This results in people being forced to use it against their will. So obviously a lot of people don't like it - probably because it doesn't have that feature they really like from their primary language - whatever that is. If we invented a replacement language, the issue would not go away, but simply shift.
>
> — [Thomas Watson](https://news.ycombinator.com/item?id=13849478)

See also [ECMAScript](../ECMAScript/ECMAScript.md)

- [HTML DOM - Common tasks of managing HTML DOM with vanilla JavaScript](https://htmldom.dev/)

## Best pratices — Coding conventions

Style guide, code conventions:

- [AS3 Coding Standards - TechWiki](https://web.archive.org/web/20130727234942/http://techwiki.openstructs.org/index.php/AS3_Coding_Standards)
- [Flex SDK / Wiki / Coding Conventions](https://web.archive.org/web/20201112103845/https://sourceforge.net/adobe/flexsdk/wiki/Coding%20Conventions/)
- [Code Conventions for the JavaScript Programming Language](http://javascript.crockford.com/code.html)
- [JavaScript Style Guide | Contribute to jQuery](https://contribute.jquery.org/style-guide/js/)
- [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)
- [airbnb/javascript: JavaScript Style Guide](https://github.com/airbnb/javascript)
- [Code Guidelines for Rich Internet Application Development](https://web.archive.org/web/20200107195821/http://jibbering.com/faq/notes/code-guidelines/)
- [JavaScript Style Guide](https://web.archive.org/web/20160614115731/http://neil.rashbrook.org/JS.htm)
- [standard/standard: 🌟 JavaScript Style Guide, with linter & automatic code fixer](https://github.com/standard/standard)
- [Popular Coding Convention on Github](http://sideeffect.kr/popularconvention/#javascript)
- [JavaScript best practices - W3C Wiki](https://www.w3.org/wiki/JavaScript_best_practices)

- [Seravo/js-winning-style: JavaScript, the winning style](https://github.com/Seravo/js-winning-style)
- [Google Code Archive - Long-term storage for Google Code Project Hosting.](https://code.google.com/archive/p/gmaps-utility-library-dev/wikis/JavascriptCodingConventions.wiki)
- [JavaScript Tips - Mozilla | MDN](https://developer.mozilla.org/en-US/docs/Mozilla/JavaScript_Tips)
- [JS: The Right Way](https://web.archive.org/web/20201110175718/https://jstherightway.org/)
- https://github.com/Reactive-Extensions/RxJS/blob/master/doc/gettingstarted/categories.md
- [ryanmcdermott/clean-code-javascript: Clean Code concepts adapted for JavaScript](https://github.com/ryanmcdermott/clean-code-javascript)
- [JavaScript naming conventions: do’s and don’ts](https://web.archive.org/web/20201101050757/https://www.freecodecamp.org/news/javascript-naming-conventions-dos-and-don-ts-99c0e2fdd78a/)

- [Simple Techniques for Writing More Semantic and Maintainable JavaScript Apps — Space Camp — Medium](https://medium.com/space-camp/three-simple-techniques-for-writing-more-semantic-and-maintainable-javascript-apps-206b4fb89f15)

- [Don't use functions as callbacks unless they're designed for it - JakeArchibald.com](https://web.archive.org/web/20210224194223/https://jakearchibald.com/2021/function-callback-risks/)
- [JavaScript Patterns](https://shichuan.github.io/javascript-patterns/)
- [Learning JavaScript Design Patterns](http://addyosmani.com/resources/essentialjsdesignpatterns/book/)
- [Don't use these examples](http://code-de-porc.tumblr.com)
- [Superhero.js](https://web.archive.org/web/20201108135951/http://superherojs.com/)

## Documentation

See also [Documentation](../ECMAScript/ECMAScript.md#documentation)

## Tools

- http://code.google.com/p/closure-compiler/wiki/DesignDocuments
- https://developers.google.com/closure/compiler/docs/api-tutorial3
- [User Timing API - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/User_Timing_API) [`performance.measure(...)`](https://developer.mozilla.org/en-US/docs/Web/API/Performance/measure)

```js
const requestStart = (() => {
	const now = Date.now()
	// Try to use the performanceNavigationTiming API
	if (window.PerformanceNavigationTiming) {
		// use performance.now() to adjust requestStart from context time (monotonic time) to epoch time (UNIX time)
		return now - performance.now() + performance.getEntriesByType("navigation")[0].requestStart;
	}
	// fallback to the former performanceTiming API or Date.now().
	return performance.timing ? performance.timing.requestStart : now;
})();
```

### Debug

Debug with conditional breakpoint:

Add conditional breakpoint to inject code to execute: `console.log("here")` (`log()` return `undefined` which is a falsy value). You can't control the flow (like if it's executed in a child function). The last statment should be a boolean indicate if the breakpoint should pause (true) the execution of the script

Or use in Chrome devtools: Sources tab > Event Listener Breakpoints > Script > Script First Statement

```js
Object.defineProperties(window, {
	scroll: {value: console.trace},
	scrollTo: {value: console.trace},
	scrollBy: {value: console.trace},
	scrollY: {set: console.trace, get: () => 55},
	scrollX: {set: console.trace, get: () => 55}
});
Object.defineProperties(document.scrollingElement, {
	scroll: {value: console.trace},
	scrollTo: {value: console.trace},
	scrollBy: {value: console.trace},
	scrollTop: {set: console.trace, get: () => 55},
	scrollLeft: {set: console.trace, get: () => 55}
});

const waitForGlobalProp = new Promise((resolve, reject) => {
	const propName = "OneTrust";
	if(self[propName]){
		resolve(self[propName]);
		return;
	}

	const timeoutID = setTimeout(() => reject(`${propName} timeout`), 1000);

	// Property proxy
	Object.defineProperty(self, propName, {
		set: (value) => {
			clearTimeout(timeoutID);
			Object.defineProperty(self, propName, {value, configurable: true, writable: true, enumerable: true});// Equivalent to self[propName] = value but required or we will get a recursive call (the setter call himeself)
			resolve(value);
		}
		get: () => undefined,
		configurable: true
	});
});
```

- [Set a conditional breakpoint - Firefox Developer Tools | MDN](https://developer.mozilla.org/en-US/docs/Tools/Debugger/How_to/Set_a_conditional_breakpoint)
- [Fixing memory leaks in web applications | Read the Tea Leaves](https://nolanlawson.com/2020/02/19/fixing-memory-leaks-in-web-applications/)

## Libraries and frameworks

See [localization](Development#localization), [libaries](ECMAScript#libaries)

Collections:

- [Cross-browser / Polyfill Libraries](https://github.com/dexteryy/spellbook-of-modern-webdev#cross-browser--polyfill-libraries)
- [Universal Utility Libraries](https://github.com/dexteryy/spellbook-of-modern-webdev#universal-utility-libraries)
- [UX Libraries](https://github.com/dexteryy/spellbook-of-modern-webdev#ux-libraries)
- [Graphic Libraries](https://github.com/dexteryy/spellbook-of-modern-webdev#graphic-libraries)

Some libraries:

- Angular 1 scope can be accessed by any JS, with `angular.element(domElement).scope()` (an read: `scope.myVar`, `scope.$parent.myOtherVar` or update: `scope.$apply()`)
    For Angular 2 `ng.probe($0)._debugInfo._view.changeDetectorRef.detectChanges()` `ng.probe($0).componentInstance` `ng.probe($0).triggerEventHandler('click')`, `ng.getComponent(...)`
    For Angular 9 `$0.__ngContext__` (human readable only when debug mode is enabled with debug view `$0.__ngContext__.debug`)
- https://github.com/michalsnik/aos - scroll trigger **-> use `IntersectionObserver`**
- [Svelte • The magical disappearing UI framework](https://svelte.technology/)
- videoplayer [mozilla-central: toolkit/content/widgets/videocontrols.xml](http://hg.mozilla.org/mozilla-central/file/tip/toolkit/content/widgets/videocontrols.xml)
- [aFarkas/lazysizes: High performance and SEO friendly lazy loader for images (responsive and normal), iframes and more, that detects any visibility changes triggered through user interaction, CSS or JavaScript without configuration.](https://github.com/aFarkas/lazysizes) - Lazyload
- [WebReflection/event-target: The EventTarget Class Polyfill.](https://github.com/WebReflection/event-target)
- [Plyr - A simple HTML5 media player](https://plyr.io/) - Player video
- [schteppe/p2.js: JavaScript 2D physics library](https://github.com/schteppe/p2.js) - 2D physics engine
- [schteppe/cannon.js: A lightweight 3D physics engine written in JavaScript.](https://github.com/schteppe/cannon.js) - 3D physics engine
- [barmalei/zebkit: JavaScript library that follow easy OOP concept, provide HTML5 Canva based Rich UI and include Java to JavaScript converter tool](https://github.com/barmalei/zebkit) - UI framework
- [kornelski/slip: Slip.js — UI library for manipulating lists via swipe and drag gestures](https://github.com/kornelski/slip)
- [cure53/DOMPurify: DOMPurify - a DOM-only, super-fast, uber-tolerant XSS sanitizer for HTML, MathML and SVG. DOMPurify works with a secure default, but offers a lot of configurability and hooks. Demo:](https://github.com/cure53/DOMPurify) - Remove "dirty" HTML, filter out tags and attributes
- [FFMPEG.WASM](https://ffmpegwasm.github.io/) - "ffmpeg.wasm is a pure WebAssembly / JavaScript port of FFmpeg. It enables video & audio record, convert and stream right inside browsers."
- [TrevorSundberg/h264-mp4-encoder: H264 encoder + MP4 output for the web](https://github.com/TrevorSundberg/h264-mp4-encoder)

### Choose and use libraries

> Use third-party libraries to solve user problems, not developer problems
>
> — Adrian Holovaty [Adrian Holovaty | How I optimized my JS sheet music rendering engine | performance.now() 2018 - YouTube](https://www.youtube.com/watch?v=XH5EtQge_Bg&t=2216)

> How much of an advantage does that really give you?
> [...]
> But if you are truly worried about speed, surely your whole site should be behind a CDN – not just a few JS libraries?
> [...]
> if you’re using v1.2 and another site is using v1.2.1 the browser can’t take advantage of cacheing.
> [...]
> If you serve your JS from the same source as your main site, there is less chance of a user getting a broken experience.
> [...]
> What happens if someone hacks your CDN?
>
> — [Please stop using CDNs for external Javascript libraries – Terence Eden’s Blog](https://web.archive.org/web/20201026140353/https://shkspr.mobi/blog/2020/10/please-stop-using-cdns-for-external-javascript-libraries/)

- prefere common libaries with larger community and support.
- don't use libraries to make something you can do yourself or just for prototypes or P.O.C.
- don't use overweight libraries just for doing a simple tasks
- use complexe libraries if performance are really a need
- if you make your own patch on a library write about it somewere even if it's a simple comment in lib file header. Provide a .patch file.
- if possible pick only needed parts of that lib / custom builds

- [jQuery Builder](http://projects.jga.me/jquery-builder/)
- [Modernizr Download Builder](https://modernizr.com/download)

jQuery: `$('.foo > .bar')` is way faster than `$fooEl.find('> .bar')` because jQuery mutate `$fooEl` element (set a temporary ID, that trigger a reflow) to match rooted queries (`element.querySelector()` don't support it). Use `$fooEl.children('.bar')` instead. See [John Resig - Thoughts on querySelectorAll](http://ejohn.org/blog/thoughts-on-queryselectorall/)

- [vladocar/nanoJS: Minimal standalone JS library for DOM manipulation](https://github.com/vladocar/nanoJS)
- [You Don't Need](https://github.com/you-dont-need)
- [dgraham/eslint-plugin-jquery: Disallow jQuery functions with native equivalents.](https://github.com/dgraham/eslint-plugin-jquery)
- [You Might Not Need jQuery](http://youmightnotneedjquery.com/)
- [Thou shalt not depend on me: analysing the use of outdated JavaScript libraries on the web | the morning paper](https://blog.acolyer.org/2017/03/07/thou-shalt-not-depend-on-me-analysing-the-use-of-outdated-javascript-libraries-on-the-web/)
- [You \(probably\) don't need a JavaScript framework | Slack](https://slack-files.com/T03JT4FC2-F151AAF7A-13fe6f98da)
- [nefe/You-Dont-Need-jQuery: Examples of how to do query, style, dom, ajax, event etc like jQuery with plain javascript.](https://github.com/nefe/You-Dont-Need-jQuery)
- [you-dont-need/You-Dont-Need-Lodash-Underscore: List of JavaScript methods which you can use natively + ESLint Plugin](https://github.com/you-dont-need/You-Dont-Need-Lodash-Underscore)
- [reindexio/youmightnotneedunderscore: https://www.reindex.io/blog/you-might-not-need-underscore/](https://github.com/reindexio/youmightnotneedunderscore)
- [Does ES6 Mean The End Of Underscore / Lodash?](https://derickbailey.com/2016/09/12/does-es6-mean-the-end-of-underscore-lodash/)
- [captbaritone/eslint-plugin-underscore: ESLint rules for Underscore](https://github.com/captbaritone/eslint-plugin-underscore)

### Include library from CDN

Always make sure you have the library available locally, as fallback of the CDN. The used CDN could be unavailable.
Prefer to use library locally direclty. Use [`integrity` attribute](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity), see [Subresource Integrity](../../Security/Data%20access%20and%20integrity/Data%20access%20and%20integrity.md#subresource-integrity).

**Always use HTTPS for external resources.** Don't use protocol relative URLs or HTTP (without TLS)

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.2.6/jquery.min.js" data-fallback-src="/path/to/your/jquery-1.2.6.min.js" integrity="sha512-4pean7m+KYmoRi7hfc/a4JtcsGFLJJxkrB0NV5vWvRpoA4mZVgLT3ls+/kVRzhziZEX+SU3kRIqFDJkue+HnmA==" onerror="document.head.appendChild(Object.assign(document.createElement('script'),{src:dataset.fallbackSrc}))"></script>
```

Note: in the example above, the attribute `onerror` will not work if the [CSP](../../Security/Data%20access%20and%20integrity/Data%20access%20and%20integrity.md#content-security-policy) doesn't allow inline scripts.

### Simple framework

- [stimulusjs/stimulus: A modest JavaScript framework for the HTML you already have](https://github.com/stimulusjs/stimulus)

### HTML templating

And Virtual DOM

- [The Web smallest DOM diffing library - Andrea Giammarchi - Medium](https://medium.com/@WebReflection/the-web-smallest-dom-diffing-library-5b69ac4d1f4d)
- [Polymer/lit-html: HTML template literals in JavaScript](https://github.com/Polymer/lit-html)
- [WebReflection/hyperHTML: A Fast & Light Virtual DOM Alternative](https://github.com/WebReflection/hyperHTML) - Use compile an object based on [Template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) [hyperHTML: A Virtual DOM Alternative – Medium](https://medium.com/@WebReflection/hyperhtml-a-virtual-dom-alternative-279db455ee0e)
	```js
	let render = (strings, ...args) => console.log(strings, ...args);
	render`a${1}b${2}`;//["a", "b", "", raw: Array(3)], 1, 2
	render`a${3}b${4}`;//["a", "b", "", raw: Array(3)], 3, 4
	// each times, strings argument (the first one) is the same reference: call2Strings === call1Strings; callNStrings === call1Strings
	// this how string template works
	```
- [Reactive UI's with VanillaJS - Part 2: Class Based Components | CSS-Tricks](https://css-tricks.com/reactive-uis-vanillajs-part-2-class-based-components/)
- [Building a React-esque component using vanilla javascript.](https://medium.com/@bluepnume/building-a-react-esque-component-using-vanilla-javascript-ddc99e76b867)
- [lit-html vs hyperHTML vs lighterhtml – Andrea Giammarchi – Medium](https://medium.com/@WebReflection/lit-html-vs-hyperhtml-vs-lighterhtml-c084abfe1285)

- [A Virtual DOM and diffing algorithm](https://github.com/Matt-Esch/virtual-dom)
- [DOM diffing with vanilla JS | Go Make Things](https://web.archive.org/web/20201026215850/https://gomakethings.com/dom-diffing-with-vanilla-js/)
- [maxogden/yo-yo: A tiny library for building modular UI components using DOM diffing and ES6 tagged template literals](https://github.com/maxogden/yo-yo)
- [Web Reflection: The DOM Is NOT Slow, Your Abstraction Is](https://web.archive.org/web/20201108115943/http://webreflection.blogspot.com/2015/04/the-dom-is-not-slow-your-abstraction-is.html)
- [JSX + jQuery = jreact](https://glitch.com/~jquery-jsx-pragma) - Custom JSX renderer based on jQuery (no react)

### Date and time

- [date-fns - modern JavaScript date utility library](https://date-fns.org/)
- https://github.com/datejs/Datejs

### Video

- [JW Player](https://github.com/jwplayer/jwplayer)
- Generate video from canvas (MJPEG AVI) http://ushiroad.com/mjpeg/js/lib/mjbuilder.js
- Read HTTP Live Streaming https://github.com/RReverser/mpegts
- Read MPEG1 [JSMpeg – Decode it like it's 1999](http://jsmpeg.com/)

### Edit controls

- [Cleave.js - Format input text content when you are typing](https://nosir.github.io/cleave.js/)

#### Text editors

- [Monaco Editor](https://microsoft.github.io/monaco-editor/) - the code editor that powers VS Code
- [Example | Sir Trevor JS | Made by Many](http://madebymany.github.io/sir-trevor-js/example.html) - smart editor using blocks. see [Rich content editing entirely re-imagined for the web](https://github.com/madebymany/sir-trevor-js)
- [Ace (Ajax.org Cloud9 Editor)](https://ace.c9.io/)
- [CodeMirror](http://codemirror.net/)
- [CKEditor.com | The best web text editor for everyone](http://ckeditor.com/)
- [TinyMCE | The Most Advanced WYSIWYG HTML Editor](https://www.tinymce.com/)
- [Facebook](http://facebook.com) implements rich editing via textarea and an overlayed element on top to visualize mentions
- [Google plus](http://plus.google.com) has `contenteditable="plaintext-only"` which seems to be completely JS-driven plain element
- [Grammarly](http://grammarly.com) implements grammar-correcting-underlines via textarea + element on top (reasons: contenteditable is slow to render, no way to clean markup, hard to do proper selection/annotations)
- [Quip](http://quip.com) has a hybrid editor (each paragraph is a contenteditable line; same with http://notion.so)
- [Trix editor](http://trix-editor.org/) ignores contentEditable and maintains its own internal model (to avoid dealing with x-browser inconsistencies and complexities); same with [ProseMirror](https://github.com/ProseMirror/prosemirror#prosemirror)
- (Math specific) [MathQuill](https://github.com/mathquill/mathquill) see also https://github.com/mathjax/MathJax
- [pell - jaredreich.com](https://jaredreich.com/pell)

See also [`contentEditable`](#contenteditable)

#### Table editors

JS Excel code snipet:

```html
<!-- from http://jsfiddle.net/ondras/o3tzx1px/ -->
<p>This is an updated version of <a href="http://jsfiddle.net/ondras/hYfN3/">http://jsfiddle.net/ondras/hYfN3/</a>. Some people argued that the original approach was too hacky and incompatible with strict/ES2015, so here we go again <strong>without <code>with</code>:</strong></p>

<ul>
	<li>25 lines of vanilla ES2015: arrow functions, destructuring, template literals, spread</li>
	<li>No libraries or frameworks</li>
	<li>Excel-like syntax (formulas start with "=")</li>
	<li>Support for arbitrary expressions (=A1+B2*C3)</li>
	<li>Circular reference prevention</li>
	<li>Automatic localStorage persistence</li>
</ul>

<table></table>

<footer><p>&copy; 2017 <a href="http://ondras.zarovi.cz/">Ondřej Žára</a></p></footer>

<style>
li {  list-style: none; }

li:before {
	position: relative;
	content: "✓";
	width: 0;
	display: inline-block;
	left: -2ch;
}

input {
	border: none;
	width: 80px;
	font-size: 14px;
	padding: 2px;
}

input:hover { background-color: #eee; }
input:focus { background-color: #ccf; }

input:not(:focus) {
	text-align: right;
}

table { border-collapse: collapse; }

td {
	border: 1px solid #999;
	padding: 0;
}

tr:first-child td, td:first-child {
	background-color: #ccc;
	padding: 1px 3px;
	font-weight: bold;
	text-align: center;
}

footer { font-size: 80%; }
</style>

<script>
for (let i=0; i<6; i++) { /* build the table */
	let row = document.querySelector("table").insertRow()
	for (let j=0; j<6; j++) {
		let letter = String.fromCharCode("A".charCodeAt(0)+j-1)
		row.insertCell().innerHTML = i&&j ? `<input id=${letter}${i} />` : i||letter
	}
}
let keys = Array.from(document.querySelectorAll("input")).map(i => i.id) // spread not in Edge

function valueOf(key) { /* recursively compute a value */
	let val = localStorage[key] || ""
	if (val[0] == "=") {
		let f = new Function(...keys, `return eval("${val.substr(1)}")`)
		return f(...keys.map(key => ({valueOf: _ => valueOf(key)}))).valueOf()
	} else {
		return isNaN(parseFloat(val)) ? val : parseFloat(val)
	}
}

(window.update = _ => keys.forEach(key => { /* update all fields */
	try { document.getElementById(key).value = valueOf(key) } catch (e) {}
}))()

window.addEventListener("focus", e => e.target.value = localStorage[e.target.id] || "", true)
window.addEventListener("blur", e => (localStorage[e.target.id] = e.target.value, update()), true)
</script>
```

### Polyfills

> A polyfill …, is a piece of code or plugin that provides the technology that you, the developer, expect the browser to provide natively. Flattening the API landscape if you will.
>
> — [What is a Polyfill?](https://remysharp.com/2010/10/08/what-is-a-polyfill)

> A ponyfill, in contrast, doesn't monkey patch anything, but instead exports the functionality as a normal module, so you can use it locally without affecting other code.
>
> — [sindresorhus/ponyfill: 🦄 Like polyfill but with pony pureness](https://github.com/sindresorhus/ponyfill)

- [Loading Polyfills Only When Needed — Philip Walton](https://philipwalton.com/articles/loading-polyfills-only-when-needed/) - [blog/loading-polyfills-only-when-needed.md at master · philipwalton/blog](https://github.com/philipwalton/blog/blob/master/articles/loading-polyfills-only-when-needed.md)
- [Polyfills and the evolution of the Web](https://www.w3.org/2001/tag/doc/polyfills/)
- [inexorabletash/polyfill](https://github.com/inexorabletash/polyfill)
- https://github.com/inexorabletash/polyfill#readme
- [URL Polyfill](https://gist.github.com/arv/1384398) https://github.com/inexorabletash/polyfill/blob/master/url.js
- https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-browser-Polyfills
- [Paper.js](http://paperjs.org/) - Vector. See https://github.com/paperjs/paper.js

### MathML

- https://www.mathjax.org/
- Math TeX https://github.com/mathiasbynens/math-tex

### Data processing

https://github.com/wellflat/imageprocessing-labs

Computer vision, Image, video, audio, etc.:

- Fast Fourier Transform
- etc.

- [dosaygo-coder-0/Uint1Array: Uint1Array - JavaScript's missing Typed Array](https://github.com/dosaygo-coder-0/Uint1Array)

### Use cached libs CDN

- [Google Hosted Libraries CDN - Developer's Guide](https://developers.google.com/speed/libraries/devguide)
- http://www.jsdelivr.com/
- http://cdnjs.com/

**Note: third parties can be innaccessibles (ex: blocked)**

### Howler

Change gain (room effect):

```js
if(Howler.usingWebAudio){
	volume = Howler.masterGain;
	lowpass = Howler.ctx.createBiquadFilter();
	lowpass.type = "lowpass";
	lowpass.frequency.value = 200;
	volume.disconnect();
	volume.connect(lowpass);
	lowpass.connect(Howler.ctx.destination);
	volume.gain.value = baseVolume;
}
// later
if(Howler.usingWebAudio){
	TweenMax.to(lowpass.frequency, 0.3, {value: 2200});
}
// and
if(Howler.usingWebAudio){
	TweenMax.to(lowpass.frequency, 0.3, {value: 200});
}
```

### Canvas 2D and 3D

- [Fabric.js Javascript Canvas Library](http://fabricjs.com/)
- [photonstorm/phaser: Phaser is a fun, free and fast 2D game framework for making HTML5 games for desktop and mobile web browsers, supporting Canvas and WebGL rendering.](https://github.com/photonstorm/phaser)

#### Three.js

Find object at camera target

```js
const intersects = raycaster.intersectObjects(targetList);
```

Sprites and custom shaders, aka custom sprite material: [Three.js sprites and custom shaders? | Coding on acid.](https://makc3d.wordpress.com/2015/03/20/three-js-sprites-custom-shaders/). See http://jsdo.it/makc/cozIcan

Sprites and custom shaders:

```js
// we start with basic example from https://github.com/mrdoob/three.js/blob/master/README.md

var scene, camera, renderer;
var geometry, material, mesh;

init();
animate();

function init() {
	scene = new THREE.Scene();

	camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 1, 10000 );
	camera.position.z = 1000;

	geometry = new THREE.BoxGeometry( 200, 200, 200 );
	material = new THREE.MeshBasicMaterial( { color: 0xff0000, wireframe: true } );

	mesh = new THREE.Mesh( geometry, material );
	scene.add( mesh );

		// to this example, we shall add some sprites

		for (var i = 0; i < 100; i++) {
			var sprite = new THREE.Sprite (new THREE.SpriteMaterial ({
				color: Math.floor (0xffffff * Math.random())
			}));
			sprite.position.set (
				500 * (Math.random() - Math.random()),
				500 * (Math.random() - Math.random()),
				500 * (Math.random() - Math.random())
			);
			sprite.scale.multiplyScalar (100);
			mesh.add (sprite);
		}

		// and we shall render these sprites with custom shader

		setSpriteMaterial ();

	renderer = new THREE.WebGLRenderer();
	renderer.setSize( window.innerWidth, window.innerHeight );

	document.body.appendChild( renderer.domElement );
}

function animate() {
	requestAnimationFrame( animate );

	mesh.rotation.x += 0.01;
	mesh.rotation.y += 0.02;

	renderer.render( scene, camera );

	// update time parameter

	THREE.SpritePlugin.uniforms.time.value = (Date.now() % 1000) * 1e-3;
}

function setSpriteMaterial () {
	var spritePluginSource = THREE.SpritePlugin.toString();

	// find "program" variable

	var program = /useProgram\(([^)]+)\)/.exec(spritePluginSource)[1];

	// inject support for custom shader code

	var shaders = ['vertex', 'fragment'];
	var spritePluginSource = spritePluginSource
	.replace(/(shaderSource)([^\[]*)(\[)/g, function (match, p1, p2, p3) {
	  return p1 + p2 + 'THREE.SpritePlugin.' + shaders.shift() + 'ShaderSource||' + p3;
	})

	// inject shaders debug stuff

	.replace(/([\w]+)(\.compileShader\()([^\)]+)(\);)/g, function (match, p1, p2, p3, p4) {
	  return p1 + p2 + p3 + p4 + 'console.log(' + p1 + '.getShaderInfoLog(' + p3 + '));';
	})

	// inject support for custom uniforms

	.replace(/([\w]+)(\.drawElements)/g, function (match, p1, p2) {
	  return '' +
		'var extraUniforms = THREE.SpritePlugin.uniforms;' +
		'if (extraUniforms) {' +
		  'for (var extraName in extraUniforms) {' +
			  'var extraUniform = extraUniforms[extraName];' +
			  'extraUniform.location = extraUniform.location || ' + p1 + '.getUniformLocation(' + program + ', extraName);' +
			  p1 + '.uniform1f (extraUniform.location, extraUniform.value);' +
		  '}' +
		'}\n' + p1 + p2;
	});

	eval('THREE.SpritePlugin = ' + spritePluginSource);

	// finally, set the material - hearts based on http://glslsandbox.com/e#23617.0

	THREE.SpritePlugin.fragmentShaderSource = '\
		precision highp float;\
		uniform vec3 color;\
		uniform float time;\
		varying vec2 vUV;\
		vec4 heart( float x, float y ) {\
			float s = fract( time + color.r ) / 8.0;\
			s = 0.9 + 0.8*(1.0-exp(-5.0*s)*sin(50.0*s));\
			x *= s;\
			y *= s;\
			float a = atan(x,y)/3.14159265359;\
			float r = sqrt(x*x*1.5+y*y);\
			float h = abs(a);\
			float d = (13.0*h - 22.0*h*h + 10.1*h*h*h)/(6.0-5.0*h);\
			float g = pow(1.0-clamp(r/d,0.0,1.0),0.25);\
			return vec4(0.5+0.5*g, 0.4*color.g, 0.8*color.b, min(g * 3.0, 1.0));\
		}\
		void main () {\
			vec2 p = (-1.0+2.0*vUV);\
			gl_FragColor = heart(p.x, p.y-0.35);\
		}';

	// and its time parameter

	THREE.SpritePlugin.uniforms = {
	  time : { value : 0 }
	}

}
```

3D to 2D position (used to display DOM elements), overriding Object3D’s `updateMatrixWorld()`

- [Three.js and 2D overlays | Coding on acid.](https://makc3d.wordpress.com/2015/04/04/three-js-and-2d-overlays/)
- [2D overlays in three.js - jsdo.it - Share JavaScript, HTML5 and CSS](http://jsdo.it/makc/hw0L/fullscreen)
- [Raycaster](https://threejs.org/docs/api/core/Raycaster.html) "Raycasting is used for mouse picking"

2D position to 3D:

```js
// we start with basic example from https://github.com/mrdoob/three.js/blob/master/README.md ThreeJS r71

// we define this balloon class to handle 2D overlay stuff for us

function Balloon( html ) {
	THREE.Object3D.call( this );

	this.popup = document.createElement( 'div' );
	this.popup.classList.add( 'balloon' );
	this.popup.innerHTML = html;

	this.addEventListener( 'added', (function () {
	    container.appendChild( this.popup );
	}).bind( this ));

	this.addEventListener( 'removed', (function () {
	    container,removeChild( this.popup );
	}).bind( this ));
}

Balloon.prototype = Object.create( THREE.Object3D.prototype );
Balloon.prototype.constructor = Balloon;

Balloon.prototype.updateMatrixWorld = (function () {
	var screenVector = new THREE.Vector3 ();
	var raycaster = new THREE.Raycaster ();

	return function( force ) {
		THREE.Object3D.prototype.updateMatrixWorld.call( this, force );

		screenVector.set( 0, 0, 0 ); this.localToWorld( screenVector );

		raycaster.ray.direction.copy( screenVector );

		raycaster.ray.origin.set( 0, 0, 0 ); camera.localToWorld( raycaster.ray.origin );
		raycaster.ray.direction.sub( raycaster.ray.origin );

		var distance = raycaster.ray.direction.length();
		raycaster.ray.direction.normalize();

		var intersections = raycaster.intersectObject( scene, true );
		if( intersections.length && ( intersections[0].distance < distance )) {

			// overlay anchor is obscured
			this.popup.style.display = 'none';

		} else {

			// overlay anchor is visible
			screenVector.project( camera );

			this.popup.style.display = '';
			this.popup.style.left = Math.round((screenVector.x + 1) * container.offsetWidth / 2 - 50) + 'px';
			this.popup.style.top = Math.round((1 - screenVector.y) * container.offsetHeight / 2 - 50) + 'px';
		}
	};
}) ();

var scene, camera, renderer;
var geometry, material, mesh;

init();
animate();

function init() {
	scene = new THREE.Scene();

	camera = new THREE.PerspectiveCamera( 75, container.offsetWidth / container.offsetHeight, 1, 10000 );
	camera.position.z = 1000;

	// we change here box to sphere, apply earth texture to it

	THREE.ImageUtils.crossOrigin = '';

	geometry = new THREE.SphereGeometry( 400, 30, 20 );
	material = new THREE.MeshBasicMaterial( { map: THREE.ImageUtils.loadTexture('http://i.imgur.com/DhOF0XH.jpg'/*earth texture*/) } );

	mesh = new THREE.Mesh( geometry, material );
	scene.add( mesh );

	renderer = new THREE.WebGLRenderer();
	renderer.setClearColor( 0xffffff );
	renderer.setSize( container.offsetWidth, container.offsetHeight );

	// and wrap the whole thing into the div

	container.appendChild( renderer.domElement );

	// oh yes, add some overlays

	var africa = new Balloon( 'Africa<div class="arrow"></div>' );
	africa.position.set( 1, 0.2, -0.4 ).normalize().multiplyScalar( 400 + 1 );
	mesh.add( africa );

	var australia = new Balloon( 'Australia<div class="arrow"></div>' );
	australia.position.set( -1, -0.6, -1 ).normalize().multiplyScalar( 400 + 1 );
	mesh.add( australia );
}

function animate() {
	requestAnimationFrame( animate );

	mesh.rotation.x += 0.001;
	mesh.rotation.y += 0.020;

	renderer.render( scene, camera );
}
```

- [Portal](http://sketches.vlucendo.com/portal/)
- [Techniques for Rendering Text with WebGL | CSS-Tricks](https://css-tricks.com/techniques-for-rendering-text-with-webgl/)

### Documents

- [automerge/automerge: A JSON-like data structure that can be modified concurrently by different users, and merged again automatically.](https://github.com/automerge/automerge)

## Language and API

See [Language](../ECMAScript/ECMAScript.md#language)

- [HTML APIs: What They Are And How To Design A Good One — Smashing Magazine](https://www.smashingmagazine.com/2017/02/designing-html-apis/)

### Reference to the global scope

Use `self` instead `window`. It's available in Web Workers

- [Window.self - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/self)

### String

- escaping CSS strings and identifiers with `CSS.escape()` polyfill [mathiasbynens/CSS.escape: A robust polyfill for the CSS.escape utility method as defined in CSSOM.](https://github.com/mathiasbynens/CSS.escape), [mathiasbynens/cssesc: A JavaScript library for escaping CSS strings and identifiers while generating the shortest possible ASCII-only output.](https://github.com/mathiasbynens/cssesc)
- [mathiasbynens/brnfckr: A brainfuck minifier written in JavaScript](https://github.com/mathiasbynens/brnfckr)
- [mathiasbynens/q-encoding: A robust & character encoding–agnostic JavaScript implementation of the `Q` encoding as defined by RFC 2047.](https://github.com/mathiasbynens/q-encoding)
- [mathiasbynens/quoted-printable: A robust & character encoding–agnostic JavaScript implementation of the `Quoted-Printable` content transfer encoding as defined by RFC 2045.](https://github.com/mathiasbynens/quoted-printable)
- [mathiasbynens/rot: Perform simple rotational letter substitution (such as ROT-13) in JavaScript.](https://github.com/mathiasbynens/rot)
- [mathiasbynens/gulp-regexpu: Gulp plugin to transpile ES6 Unicode regular expressions to ES5 with regexpu.](https://github.com/mathiasbynens/gulp-regexpu)

### Detect a feature

Don't use `document.implementation.hasFeature()`:

> `hasFeature()` originally would report whether the user agent claimed to support a given DOM feature, but experience proved it was not nearly as reliable or granular as simply checking whether the desired objects, attributes, or methods existed. As such, it should no longer be used, but continues to exist (and simply returns true) so that old pages don't stop working.
> — [DOM Standard](https://dom.spec.whatwg.org/#dom-domimplementation-hasfeature)

> - don't expose the objects etc when feature is not available (like no underlying hardware gyroscope for instance)
> - always expose (due to avoiding fingerprinting) but let object throw (NotAvailableError or similar) when instantiated - this way you can see whether the browser support the feature or not, but not whether the hardware does
>
> [...]
>
> - no diff between regular mode and privacy preserving mode (incognito)
> - keeping fingerprinting to the minimum (people can know browser from UA string and features available)
> - this involves permissions
>
> — [Best practices for feature detection of DOM API · Issue #137 · w3ctag/design-principles](https://github.com/w3ctag/design-principles/issues/137#issuecomment-606486358)

```js
// Presence of a namespace
if ('bluetooth' in navigator) { /*...*/ }

// Presence of an object
if ('NFCReader' in window) { /*...*/ }

// Properties on objects, eg. Media Capture
const capabilities = videoTrack.getCapabilities();
if ("pan" in capabilities) { /*...*/ }
```

See [feature detection](../ECMAScript/ECMAScript.md#feature-detection) and [detect a feature](../../Web/Web.md#detection)

- [Best practices for feature detection of DOM API · Issue #137 · w3ctag/design-principles](https://github.com/w3ctag/design-principles/issues/137)
- [Web Platform Design Principles](https://w3ctag.github.io/design-principles/#feature-detect) - "New features should be detectable"

### Don't override native logic

In click handler (especially on links)

```js
// Let native actions happend (download, open in new tab, etc.)
// Or catch only the Left button (= Right button for left-handed mouses)
if(
	!event.touches && event.button != 0
	|| event.altKey
	|| event.ctrlKey
	|| event.metaKey
){
	return;
}

// Do click action here
event.preventDefault();
```

Never prevent `contextmenu` (use the [`menu` element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/menu) instead), `copy` and `past` events

See

- [Don't override native logic](UI - UX#dont-override-native-logic)
- [The disadvantages of single page applications | Adam Silver | UX design, Front-end Engineering and Strategy | London, UK.](http://adamsilver.io/articles/the-disadvantages-of-single-page-applications/)

### Progressive enhancement

Aka unobtrusive JavaScript, polyfill, shim. What happen if script fail to load?

> DRY: DO repeat yourself!
> Web development requires you to repeat yourself. If you have an Ajax script that adds data to the page, make sure there’s also a simple link somewhere.
> You write the same functionality twice.
> Not all software engineering principles make sense on the web because the web is not one platform
>
> — Peter-Paul Koch

> 1. identify core functionality
> 2. build this with the simplest tech
> 3. enhance
>
> — Jeremy Keith

Choose carrefully want it very important, provide polyfill (when it's possible) and fallback

If you make Progressive Web Apps (client-side rendering), be careful. Verify if your content successfully renders to search crawlers. Use an hybrid rendering approach.

Hide element to reduce rendering flicker (initial state to complete state) for font loading, app initialization, etc. and fallback to an other inlined style (if no JS) or to CSS animation (if the JS fail: load error or script error)

```html
<style>
body {animation: doc-timeout 0s 5s forwards;}
@keyframes doc-timeout {
  0% {opacity: 0;}
  100% {opacity: 1;}
}
</style>
<noscript><style>body {opacity: 1}</style></noscript>
<script src="..." async></script>
```

- [Modern Script Loading](https://jasonformat.com/modern-script-loading/) - How to load JavaScript module and it fallback
- `noscript` and fallback
- [Polyfills](#polyfills)
- [Adactio: Journal—Just what is it that you want to do?](https://adactio.com/journal/7774)
- [Don’t tell me what my browser can’t do! | Christian Heilmann](https://www.christianheilmann.com/2016/01/16/dont-tell-me-what-my-browser-cant-do/)
- [Everyone has JavaScript, right?](http://kryogenix.org/code/browser/everyonehasjs.html)
- [js;dr = Pages that are empty without JS: dead to history (archive-org) - Tantek](http://tantek.com/2015/069/t1/js-dr-javascript-required-dead)
- [Unobtrusive JavaScript — Wikipedia](https://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [Why availability matters](http://www.kryogenix.org/code/browser/why-availability/)
- [Loading Polyfills Only When Needed — Philip Walton](https://philipwalton.com/articles/loading-polyfills-only-when-needed/)
- [Official Google Webmaster Central Blog: Building Indexable Progressive Web Apps](https://webmasters.googleblog.com/2016/11/building-indexable-progressive-web-apps.html)
- [Progressive Misconceptions, From the Notebook of Aaron Gustafson](https://www.aaron-gustafson.com/notebook/progressive-misconceptions/?utm_source=codropscollective)
- [\[Insert Clickbait Headline About Progressive Enhancement Here\], From the Notebook of Aaron Gustafson](https://www.aaron-gustafson.com/notebook/insert-clickbait-headline-about-progressive-enhancement-here/)
- [The disadvantages of Javascript polyfills | Adam Silver | UX design, Front-end Engineering and Strategy | London, UK.](http://adamsilver.io/articles/the-disadvantages-of-javascript-polyfills/)
- [Progressive Enhancement](https://remysharp.com/2019/07/24/progressive-enhancement)

### Document location

- `String(window.location)`
- `String(document.location)`
- `window.location.href`
- `document.URL`
- `node.baseURI`
- `document.createElement("a").href`

```js
window.location === document.location;//true
```

To only read the document's location, use `document.URL`.
If you need to interact with location, use `window.location`. Because the API is related to the browsing context not the document itself.
Use `document.baseURI` instead `windows.location` for relatives URLs (see [`URL`](https://developer.mozilla.org/en-US/docs/Web/API/URL) constructor `base` parameter) because it's use `<base href=...>`

- https://stackoverflow.com/questions/2430936/whats-the-difference-between-window-location-and-document-location-in-javascrip
- [Document.location - Web API Interfaces | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document.location)
- [Window.location - Web API Interfaces | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window.location)

### Don't use `document.write()`

...unless you know what are you doing.

browser’s preload scanner, create a synchronous blocking script tag when encounter `document.write()` even if it's not executed

- https://developer.mozilla.org/en/Optimizing_Your_Pages_for_Speculative_Parsing
- [Intervening against document.write() | Web Updates - Google Developers](https://developers.google.com/web/updates/2016/08/removing-document-write)
- [Blocking the load of cross-origin, parser-blocking scripts inserted via document.write for users on slow connections - Chrome Platform Status](https://www.chromestatus.com/features/5652436521844736)
- https://github.com/WICG/interventions/issues/17
- [If you use use document.write, you suck at JavaScript - Pomax.github.io](https://pomax.github.io/1473270609919/if-you-use-use-document-write-you-suck-at-javascript)

How to reference an external script that use `document.write()` with async:

```js
// This script allow the script to use document.write() (synchronous script, append HTML chunks) in a context where it would erase the current document (async, after the document is complete)
// "Open a document stream for writing. If a document exists in the target, this method clears it."
var orgWriteDesc = Object.getOwnPropertyDescriptor(document, "write") || Object.getOwnPropertyDescriptor(Document.prototype, "write") || Object.getOwnPropertyDescriptor(HTMLDocument.prototype, "write");

var script = document.createElement("script");
script.src = "https://example.com/script-with-document-write.js";
// Restore native document.write()
script.onload = function(){
  Object.defineProperty(document, "write", orgWriteDesc);
};

var proxyScript = document.createElement("script");
proxyScript.src = "data:application/javascript,0";// empty script (IE need at least one statement)
proxyScript.onload = function(){
  Object.defineProperty(document, "write", {value: script.insertAdjacentHTML.bind(script, "afterend"), configurable: true});
};

document.body.appendChild(proxyScript);
document.body.appendChild(script);
```

See [Load external script](#load-external-script)

See also [krux/postscribe: Asynchronously write javascript, even with document.write.](https://github.com/krux/postscribe)

### Don't put CSS and template in script

Baking CSS and templates into scripts will increase the memory footprint of your web app. You’re obstructing the browsers’ optimizations.

> Browsers are clever; they use threaded parsing and compilation for both script and other resource types (e.g. CSS)
> Those parsers look for resources to fetch (pre-parsing and scanning). When you bake that into script, you defeat that whole system.
> But it's not just parsers! When you bake, e.g., CSS & templates into script, those things live in the heap. We can't drop them (usually).
>
> — [Alex Russell - @slightlylate](https://twitter.com/slightlylate/status/793617048253247488)

### Don't use `event.stopPropagation()` or `event.stopImmediatePropagation()`

Use `event.preventDefault()` instead

### Events

Event handler: `el.onload = func;`. Note: when func has its scope to `eventTarget` and its `this` value. Ex: `onload="console.log(prop===this.prop)"`, properties can be used without `this` (but not functions). See [DOM on-event handlers - Developer guides | MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Event_handlers#Event_handler's_parameters_this_binding_and_the_return_value) and [HTML Standard - "callback this value"](https://html.spec.whatwg.org/multipage/webappapis.html#the-event-handler-processing-algorithm) and [HTML Standard - "internal raw uncompiled handler FunctionCreate Scope"](https://html.spec.whatwg.org/multipage/webappapis.html#internal-raw-uncompiled-handler)
Event listener: `el.addEventListener("load", listener);`, where listener is a `function` or an object (`EventListener`) implement `handleEvent` method

```js
handleEvent()
handleSubjectEvent()
handleNameChange()
handleChange()
handleFormReset()
handleReset()
```

- [DOM on-event handlers - Web developer guides | MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Event_handlers)
- [EventListener - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/EventListener)

### Global scope

- https://stackoverflow.com/questions/4670805/javascript-eval-on-global-scope
- https://stackoverflow.com/questions/3277182/how-to-get-the-global-object-in-javascript/
- http://perfectionkills.com/global-eval-what-are-the-options/
- http://2ality.com/2016/11/trace-globals-proxy.html

### Variables

- [Difference between variable declaration syntaxes in Javascript (including global variables)? - Stack Overflow](https://stackoverflow.com/questions/4862193/difference-between-variable-declaration-syntaxes-in-javascript-including-global/4862268#4862268)

### Naming convention

Aka case style, casing, Design JavaScript APIs

Examples of native functions/methods or properties:

- `encodeURIComponent`
- `DOMContentLoaded`
- `Math.PI`
- `DOMElement`
- `toJSON`
- `getBoundingClientRect`
- `Number.MAX_SAFE_INTEGER`
- `Node.ELEMENT_NODE`
- `innerHTML`
- `getElementById`
- `getElementsByTagNameNS`

Are browser-specific additions (by Microsoft for Internet Explorer):

- `XMLHttpRequest` should be `XMLHTTPRequest`
- `onreadystatechange` should be `onReadyStateChange`
- `onclick` should be `onClick`

Event names:

- multiple element dispatch the same event: [`change` event](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/change_event) is dispatched by `<input>`, `<select>`, `<textarea>`
- use the present form, not the past form: [`paste`](https://developer.mozilla.org/en-US/docs/Web/API/Element/paste_event) (not `pasted`):
	- `addtrack`
	- `slotchange`
	- `canplaythrough`
	- `canplay`
	- `playing` (right name?)
	- `play`
	- `beforeinput` and `input`
	- `animationcancel`
	- `animationend`
	- `transitioncancel`
- cancellability:
	- [`selectstart`](https://developer.mozilla.org/en-US/docs/Web/API/Document/selectstart_event) (cancellable) -> [`selectionchange`](https://developer.mozilla.org/en-US/docs/Web/API/Document/selectionchange_event) (not cancellable)
	- (subbmitter) [`mousedown`](https://developer.mozilla.org/en-US/docs/Web/API/Element/mousedown_event) (cancellable) -> (subbmitter) [`mouseup`](https://developer.mozilla.org/en-US/docs/Web/API/Element/mouseup_event) (cancellable) -> (subbmitter) [`click`](https://developer.mozilla.org/en-US/docs/Web/API/Element/click_event) (cancellable) -> (form) [`submit`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/submit_event) (cancellable) -> (window) [`beforeunload`](https://developer.mozilla.org/en-US/docs/Web/API/Window/beforeunload_event) (cancellable) -> (window) [`unload`](https://developer.mozilla.org/en-US/docs/Web/API/Window/unload_event) (not cancellable)
- related information:
	- [`selectionchange`](https://developer.mozilla.org/en-US/docs/Web/API/Document/selectionchange_event): [`document.getSelection()`](https://developer.mozilla.org/en-US/docs/Web/API/Document/getSelection)
	- [`submit`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/submit_event): [`event.submitter`](https://developer.mozilla.org/en-US/docs/Web/API/SubmitEvent/submitter)
	- focus events: [`event.relatedTarget`](https://developer.mozilla.org/en-US/docs/Web/API/FocusEvent/relatedTarget)
	- mouse events: [`event.relatedTarget`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/relatedTarget)
	- keyboard events: [`event.key`](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/key) (and [other properties](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent#properties))
	- mutation events ([depreciated](https://dom.spec.whatwg.org/#mutationevent)): [`event.prevValue` and `event.newValue`](https://www.w3.org/TR/DOM-Level-3-Events/#interface-mutationevent)
	- [touch events](https://developer.mozilla.org/en-US/docs/Web/API/Touch_events): [`event.changedTouches`](https://developer.mozilla.org/en-US/docs/Web/API/TouchEvent/changedTouches)
- workflow:
	- `new PaymentRequest()` -> `paymentRequest.show(details)` -> [`paymentmethodchange` event](https://developer.mozilla.org/en-US/docs/Web/API/PaymentRequest/paymentmethodchange_event) -> `event.updateWith(details)` (if details/errors need to be updated) -> `paymentRequest.show()` promise resolved
- event name in lowercase
- see other event names: [Event reference | MDN](https://developer.mozilla.org/en-US/docs/Web/Events)
- [Input Event Order](https://www.w3.org/TR/DOM-Level-3-Events/#events-inputevent-event-order): `beforeinput` -> (DOM element is updated) -> `input`

Examples: `userID` and `profileURL`

See also:

- [Why String.prototype.startsWith but not String.prototype.startWith? : javascript](https://www.reddit.com/r/javascript/comments/a2etsp/why_stringprototypestartswith_but_not/eaxnxip/) - "String starts with?" ('Does "foobar" start with "foo"?' → '"Foobar" starts with "foo"')
- [Web Platform Design Principles](https://www.w3.org/TR/design-principles/#casing-rules)
- [javascript - Why does XMLHttpRequest not seem to follow a naming convention? - Software Engineering Stack Exchange](https://softwareengineering.stackexchange.com/questions/157375/why-does-xmlhttprequest-not-seem-to-follow-a-naming-convention)
- [coding style - Acronyms in CamelCase - Stack Overflow](https://stackoverflow.com/questions/15526107/acronyms-in-camelcase)
- [wp-calypso/javascript.md at master · Automattic/wp-calypso](https://github.com/Automattic/wp-calypso/blob/master/docs/coding-guidelines/javascript.md#naming-conventions)
- [Coding Standards: Naming conventions for abbreviated camel-case · Issue #2511 · WordPress/gutenberg](https://github.com/WordPress/gutenberg/issues/2511)
- [Naming convention for multi-word identifiers with initialisms](https://esdiscuss.org/topic/naming-convention-for-multi-word-identifiers-with-initialisms)
- [Naming principles - Web Platform Design Principles](https://www.w3.org/TR/design-principles/#naming-is-hard) - W3C design principles
- [HTML APIs: What They Are And How To Design A Good One — Smashing Magazine](https://www.smashingmagazine.com/2017/02/designing-html-apis/)

See [Naming convention](Development#naming-convention)

## Custom elements

- [Progressive Enhancement](https://remysharp.com/2019/07/24/progressive-enhancement#web-components)

# Tips & snippets

- [JavaScript | CSS-Tricks](https://css-tricks.com/snippets/javascript/)

## Worker

```js
navigator.hardwareConcurrency
```

- [navigator.hardwareConcurrency - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorConcurrentHardware/hardwareConcurrency)
- [web worker - Get number of CPU cores in JavaScript? - Stack Overflow](https://stackoverflow.com/questions/3289465/get-number-of-cpu-cores-in-javascript)
- [ES proposal: Shared memory and atomics](http://2ality.com/2017/01/shared-array-buffer.html)
- [A crash course in memory management ★ Mozilla Hacks – the Web developer blog](https://hacks.mozilla.org/2017/06/a-crash-course-in-memory-management/)

### Inline worker

```js
function worker() {
	setInterval(function() {
		postMessage({foo: "bar"});
	}, 1000);
}

var code = worker.toString();
//code = code.substring(code.indexOf("{")+1, code.lastIndexOf("}"));
code = `(${code})()`;

var blob = new Blob([code], {type: "application/javascript"});
//var blob = new File([code], "worker.js", {type: "application/javascript"});
var workerInstance = new Worker(URL.createObjectURL(blob));// will not works in IE10

workerInstance.onmessage = function(m) {
	console.log("worker msg", m);
};
```

- [The Basics of Web Workers - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/workers/basics/#toc-inlineworkers)
- https://stackoverflow.com/questions/10343913/how-to-create-a-web-worker-from-a-string
- [Using Web Workers - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers#Embedded_workers)

## Components

- [Building a modern carousel with CSS scroll snap, smooth scrolling, and pinch-zoom | Read the Tea Leaves](https://nolanlawson.com/2019/02/10/building-a-modern-carousel-with-css-scroll-snap-smooth-scrolling-and-pinch-zoom/)

## Form

### Submit form programmatically

When you call `form.submit()` the listener attached to the `submit` event are not triggered (depends browsers?). Also contraints are not validated.

The workaround is create on-the-fly a submit button attach it to the form, click it, and finally remove it

```js
/**
 * Submit the owner form (parent or defined via the attribute `form` on input tag)
 * @see http://dabblet.com/gist/97a733d9c787dcf99cff
 * @see http://www.w3.org/html/wg/drafts/html/master/forms.html#implicit-submission
 */
function submitImplicitly(input){
	var form = input.form;
	//TODO:
	// find first avaialble submit button in form.elements (nodeName == "BUTTON" && type == "submit" || nodeName == "INPUT" && type == "reset" || nodeName == "INPUT" && type == "submit" || nodeName == "INPUT" && type == "image") && !nodeName.disabled
	// see "Get the form submitter"
	// or create a fake button (but spec say not submit when no button available):
	var button = form.ownerDocument.createElement("input");
	// Hide it (style and for ATs)
	button.style.display = "none";
	button.tabIndex = -1;
	button.setAttribute("aria-hidden", "true");
	button.setAttribute("role", "presentation");
	button.type = "submit";
	form.appendChild(button).click();
	form.removeChild(button);
};
```

- https://stackoverflow.com/questions/645555/should-jquerys-form-submit-not-trigger-onsubmit-within-the-form-tag
- https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement.submit
- https://gist.github.com/mems/97a733d9c787dcf99cff

### Get the form submitter

It can be:

- non disabled button(`button[type=submit],input[type=button],input[type=image]`) with current form as owner form (inside form or with `form="id-of-current-form"`)
- an implicity submitter field (with type: Text, Search, URL, Telephone, E-mail, Password, Date, Time, Number) (virtually submit the first non disabled button if exist, see below).

```js
form.addEventListener("submit", event => {
	event.submitter;// standard
	event.explicitOriginalTarget;//(Firefox only) form submitter: input or button
	form.ownerDocument.activeElement;//works for user interactions, but not works for programmatically submitter (ex.: focus input and call button.click(), activeElement match input not button)
});
```

- [SubmitEvent.submitter - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/SubmitEvent/submitter)
- [javascript - Can I find out on the client which submit button was pressed when listening to the submit event? - Stack Overflow](https://stackoverflow.com/questions/29087977/can-i-find-out-on-the-client-which-submit-button-was-pressed-when-listening-to-t)
- [4.10 Forms — HTML5](http://www.w3.org/TR/html5/forms.html#form-submission-0)
- [Comparison of Event Targets - Web API Interfaces | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Event/Comparison_of_Event_Targets)

### Get the form action

form.action or submitter(button[type=submit]|input[type=button]) formaction

See [get the form submitter](#get-the-form-submitter)

### Android form keyboard submitter

Next or Go

See [Don't override native logic](#dont-override-native-logic)

- [HTML: Why does Android browser show "Go" instead of "Next" in keyboard? - Stack Overflow](https://stackoverflow.com/questions/6545086/html-why-does-android-browser-show-go-instead-of-next-in-keyboard)
- [android - Replace Go button on soft keyboard with Next in Phonegap - Stack Overflow](https://stackoverflow.com/questions/23470439/replace-go-button-on-soft-keyboard-with-next-in-phonegap)


### Submit form with AJAX

Use `FormData` but require to use `POST` and content type `multipart/form-data`.

```js
var form;
var submitter;//non disabled button[type=submit]|input[type=button]|input[type=image]. See [get the form submitter](#get-the-form-submitter)
var xhr = new XMLHttpRequest();
var method = "POST"/*submitter.formMethod !== "" ? submitter.formMethod : form.method*/;// FormData works only with POST
var enctype = submitter.formEnctype !== "" ? submitter.formEnctype : form.enctype;// Use FormData overwrite content type to "multipart/form-data;boundary=RANDOM_STRING"
// TODO handle form.acceptCharset
var action = submitter.formAction !== "" ? submitter.formAction : form.action;
var data = new FormData(form);// FormData don't add button[type=submit]|input[type=button]
// Add submitter
if(submitter.name !== ""){
	data.append(submitter.name, submitter.value);
}
xhr.open(method, action);
//xhr.setRequestHeader("Content-Type", enctype);//see enctype
xhr.send(data);
```

Or use `FormDataReader` and `FormDataEncoder` or any other reader/encoder:

```js
import FormDataReader from "syk/FormDataReader.js"
import FormDataEncoder from "syk/FormDataEncoder.js"
//...
let entries = FormDataReader.getEntries(form);
if(submitter.name !== ""){
	entries.push(new FormDataEntry(submitter.name, submitter.value, "submit"));
}
var formEncoder = new FormDataEncoder();
//...
xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded; charset=UTF-8");
formEncoder.encode(entries);
// when formEncoder.readyState == FormDataEncoder.DONE:
xhr.send(formEncoder.result);
```

### Form validation

```html
<style>
	label.valid {}
	label.valid input {}
	label.valid span {}
	label.invalid {}
	label.invalid input {}
	label.invalid span {}
</style>
<script>
	// Suppress native error messages
	form.addEventListener("invalid", event => event.preventDefault());

	// Trigger validation onblur
	form.addEventListener("blur", ({target}) => {
		if (target.nodeName === 'INPUT') {
			validateField(target);
		}
	});
	form.addEventListener("submit", event => {/*...*/});

	function validateField(field){
		if (!field.validity.valid) {
			// set class to invalid
		} else if (field.validity.valid && field.value) {
			// set class to valid
		} else {
			// remove both classes
		}
	}
</script>
<form novalidate>
	<label>
		Your name
		<input name=“name” required>
		<span>This field is required</span>
	</label>
</form>
```

- [formvalidation_CSSDay - formvalidation_CSSDay.pdf](https://quirksmode.org/presentations/Spring2017/formvalidation_CSSDay.pdf)
- [Form tests - what we want](https://quirksmode.org/dom/forms/examples_correct.html)
- [Files for form validation presentation - ppk](https://quirksmode.org/forms/)
- [Constraint Validation: Native Client Side Validation for Web Forms - HTML5 Rocks](http://www.html5rocks.com/en/tutorials/forms/constraintvalidation/)

### Autoresize form fields

```js
field.style.height = "0";
var scrollHeight = this._element.scrollHeight;
var offsetHeight = this._element.offsetHeight;
var ctnBoxPadding = offsetHeight - this._element.clientHeight;//padding and border (if box-sizing: border-box)
field.style.height = Math.ceil(scrollHeight + ctnBoxPadding) + "px";
```

- [Stretchy: Form element autosizing, the way it should be.](http://leaverou.github.io/stretchy/)

### Form reset event

It's dispatched before the change occure (cancelable event). Require a setTimeout to execute code after reset changes. Change or input events are not dispatched on fields.

### Form validation

- [Form Validation Techniques](https://bitsofco.de/form-validation-techniques/)
- [Realtime Form Validation](https://bitsofco.de/realtime-form-validation/)

### Stale field

Aka (inverse of) dirty

```js
el.value == el.defaultvalue;
el.checked == el.defaultChecked;
```

## Communication between tabs and windows (same origin)

- `localStorage`
- `SharedWorker`
- `IndexedDB`

- https://stackoverflow.com/questions/12107424/communication-between-browser-tab

## Storage

**Don't use Local Storage to store sensitive data.** See [Please Stop Using Local Storage](https://dev.to/rdegges/please-stop-using-local-storage-1i04)

- `IndexedDB`
- `localStorage`

- [Breaking the Borders of IndexedDB ★ Mozilla Hacks – the Web developer blog](https://hacks.mozilla.org/2014/06/breaking-the-borders-of-indexeddb/)
- https://github.com/dfahlander/Dexie.js
- [Window.localStorage - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)

### Concurrent app versions access to same data

1. App loaded (v1) in tab 1 (tab or window)
2. App loaded (v2) in tab 2

1. Loaded apps v2 must be in "wait for upgrade" state (display a message to the user he have to go to other tabs to save or discard changes) untill apps v1 are close
2. Loaded apps v1 must be in "save or discard" state (display a message to the user if he want to save or discard changes) untill apps v2 are opened
3. For each v1, once the user save or discard changes, reload as v2
4. Once all v1 are closed, set state as "upgrade"
5. Once upgrade end, remove state "upgrade"

> Do you use localStorage, idb etc? Do you prepare for 2 tabs running different versions of your app with potentially different schemas?
> …as in one tab opened more recently, and the new version stores data differently or in a different place
> …IDB won't allow a migration while connections remain to the current version. Means the new ver hangs unless until the old ver closes.
> …both tabs get events, the old version can close db & go read only. Lots of defensive coding needed though. Does anyone do this?
> as the old ver needs to cater for versionchange, I imagine you've got a problem you can't rectify by the time you realise you have a problem
— https://twitter.com/jaffathecake/status/502779501936652289

Tab 1:

```js
function log(val) {
  console.log(val);
  var div = document.createElement('div');
  div.textContent = val;
  document.body.appendChild(div);
}

var request = indexedDB.open("upgradetest", 1);

request.onupgradeneeded = function(event) {
  log('Upgrading from version ' + event.oldVersion);
  var db = request.result;
  switch (event.oldVersion) {
	case 0:
	  var store = db.createObjectStore('keyval');
	  store.put('world', 'hello');
  }
};

request.onsuccess = function() {
  log("Connected to DB");
  var db = request.result;
  db.onversionchange = function() {
	log("onversionchange event, so we know there's a newer version trying to connect - press c to close db");
  };
  document.onkeyup = function(event) {
	if (event.keyCode == 67) {
	  db.close();
	  log('Database closed - go back to the other tab');
	}
  };
}

request.onerror = function() {
  log(request.error);
}
```

Tab 2:

```js
function log(val) {
  console.log(val);
  var div = document.createElement('div');
  div.textContent = val;
  document.body.appendChild(div);
}

var request = indexedDB.open("upgradetest", 2);

request.onupgradeneeded = function(event) {
  log('Upgrading from version ' + event.oldVersion);
  var db = request.result;
  switch (event.oldVersion) {
	case 0:
	  var store = db.createObjectStore('keyval');
	  store.put('world', 'hello');
	case 1:
	  var store = request.transaction.objectStore('keyval');
	  store.put('foo', 'bar');
  }
};

request.onblocked = function(event) {
  log('Blocked - look in the other tab');
};

request.onsuccess = function() {
  log("Connected to DB - you win!");
  log("Press d to delete db & start again")
  var db = request.result;
  document.onkeyup = function(event) {
	if (event.keyCode == 68) {
	  db.close();
	  log('Deleting database');
	  indexedDB.deleteDatabase('upgradetest').onsuccess = function() {
		log('Database deleted');
	  };
	}
  };
}

request.onerror = function() {
  log(request.error);
}
```

- https://jsbin.com/velolu/1/quiet
- https://gist.github.com/jakearchibald/abf8489a93d564055244

### `IndexDB`

> IDB transaction auto-closes if it doesn't have anything left do once microtasks have been processed
> - [jakearchibald/idb: IndexedDB, but with promises](https://github.com/jakearchibald/idb#transaction-lifetime)

That means if couldn't do an async operation (with a `setTimeout()`, [`requestIdleCallback()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/requestIdleCallback), `fetch`, user click, etc.) then use a transaction.

Use transaction in an unload event is not guarantied to works, implementations could works differently: [Re: \[IndexedDB\] Transactions during window.unload? from Jonas Sicking on 2012-03-01 (public-webapps@w3.org from January to March 2012)](https://lists.w3.org/Archives/Public/public-webapps/2012JanMar/0944.html)

- [How do you keep an indexeddb transaction alive? - Stack Overflow](https://stackoverflow.com/questions/10385364/how-do-you-keep-an-indexeddb-transaction-alive)

## Break `console.log()`

It's a fake problem, that must be fixed by browser makers, and don't protect data from someone with bad intentions

```js
(function() {
	try {
		var $_console$$ = console;
			Object.defineProperty(window, "console", {
				get: function() {
					if ($_console$$._commandLineAPI)
						throw "Sorry, for security reasons, the script console is deactivated on netflix.com";
					return $_console$$
				},
				set: function($val$$) {
					$_console$$ = $val$$
				}
			})
	} catch ($ignore$$) {
	}
})();
```

This example work only on Webkit (Chrome only?) browsers

Restore hosting/console functions:

```js
console.log = Object.getPrototypeOf(console).log;
// or
delete console.log
// or
var i = document.createElement("iframe");
i.style = "position: absolute;visibility: hidden;";
document.body.appendChild(i);
window.console = i.contentWindow.console;
```

See [javascript - Restoring console.log() - Stack Overflow](https://stackoverflow.com/questions/7089443/restoring-console-log)

In others browser (or if redefine `console` property is not possible), log a message:

Log in console in non Chrome browsers:

```js
// From Facebook
let j = 'Stop!';
let k = 'This is a browser feature intended for developers. If someone told you to copy-paste something here to enable a Facebook feature or "hack" someone\'s account, it is a scam and will give them access to your Facebook account.';
let url = 'https://www.facebook.com/selfxss';
let l = `See ${url} for more information.`;
if ((window.chrome || window.safari)) {
	var m = 'font-family:helvetica; font-size:20px; ';
	[
		[j, m + 'font-size:50px; font-weight:bold; ' + 'color:red; -webkit-text-stroke:1px black;'],
		[k, m],
		[l, m],
		['', '']
	].map(function (s) {
		setTimeout(console.log.bind(console, '\n%c' + s[0], s[1]));
	});
} else {
	let n = [
		'',
		' .d8888b.  888					   888',
		'd88P  Y88b 888					   888',
		'Y88b.	  888					   888',
		' "Y888b.   888888  .d88b.  88888b.   888',
		'	"Y88b. 888	d88""88b 888 "88b  888',
		'	  "888 888	888  888 888  888  Y8P',
		'Y88b  d88P Y88b.  Y88..88P 888 d88P',
		' "Y8888P"   "Y888  "Y88P"  88888P"   888',
		'						   888',
		'						   888',
		'						   888'
	];
	let o = ('' + k).match(/.{35}.+?\s+|.+$/g);
	let p = Math.floor(Math.max(0, (n.length - o.length) / 2));
	for (let q = 0; q < n.length || q < o.length; q++) {
		let r = n[q];
		n[q] = r + new Array(45 - r.length).join(' ') + (o[q - p] || '');
	}
	console.log('\n\n\n' + n.join('\n') + '\n\n' + l + '\n');
}
```

- https://stackoverflow.com/questions/21692646/how-does-facebook-disable-the-browsers-integrated-developer-tools
- http://davidwalsh.name/disable-console
- https://bugzilla.mozilla.org/show_bug.cgi?id=656433
- https://code.google.com/p/chromium/issues/detail?id=82181
- https://stackoverflow.com/questions/7559409/disable-developer-tools

## Enum

- https://github.com/rauschma/enumify and http://www.2ality.com/2016/01/enumify.html

## Garbage collecting and references

- Kept: Root reference (any entities) or loading XHR (itself and all attached listeners), or closure (any entities), timeout (callback)
- Released (not immedialy): not a root referenced, not in kept closure, not an timeout callback, not loading XHR, not a loading XHR listener

- [Memory Leaks with XMLHttpRequest Objects](https://web.archive.org/web/20201112002717/https://nullprogram.com/blog/2013/02/08/)
- [4 Types of Memory Leaks in JavaScript and How to Get Rid Of Them](https://web.archive.org/web/20201109020415/https://auth0.com/blog/four-types-of-leaks-in-your-javascript-code-and-how-to-get-rid-of-them/)
- [Understand memory leaks in JavaScript applications](http://www.ibm.com/developerworks/library/wa-jsmemory/)
- [Fix Memory Problems  |  Web  |  Google Developers](https://developers.google.com/web/tools/chrome-devtools/memory-problems/#discover_detached_dom_tree_memory_leaks_with_heap_snapshots))
- [Static Memory Javascript with Object Pools - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/speed/static-mem-pools/) - Use object pools (recycle). See [Slay'n the Waste Monster by Colt McAnlis (#perfmatters at SFHTML5) - YouTube](https://www.youtube.com/watch?v=RWmzxyMf2cE)
- [GCview](https://github.com/adobe-research/GCview) - GC / memory management visualization and monitoring framework
- [Event listeners and garbage collection - JakeArchibald.com](https://web.archive.org/web/20201108193011/https://jakearchibald.com/2020/events-and-gc/)

- [WebGL progressive texture](#webgl-progressive-texture)

## WebGL, Canvas2D

Chrome `chrome://gpu/`

- [Clean canvas's WebGL context](https://stackoverflow.com/a/23606581/470117)
- [WebGL Anti Patterns « games.greggman.com](http://games.greggman.com/game/webgl-anti-patterns/)
- [The Lessons | Learning WebGL](http://learningwebgl.com/blog/?page_id=1217)
- [Best Practices for Working with Vertex Data](https://developer.apple.com/library/content/documentation/3DDrawing/Conceptual/OpenGLES_ProgrammingGuide/TechniquesforWorkingwithVertexData/TechniquesforWorkingwithVertexData.html#//apple_ref/doc/uid/TP40008793-CH107-SW1)
- [Best Practices for Working with Texture Data](https://developer.apple.com/library/content/documentation/3DDrawing/Conceptual/OpenGLES_ProgrammingGuide/TechniquesForWorkingWithTextureData/TechniquesForWorkingWithTextureData.html#//apple_ref/doc/uid/TP40008793-CH104-SW1)
- [Best Practices for Shaders](https://developer.apple.com/library/content/documentation/3DDrawing/Conceptual/OpenGLES_ProgrammingGuide/BestPracticesforShaders/BestPracticesforShaders.html#//apple_ref/doc/uid/TP40008793-CH7-SW3)
- [Tuning Your OpenGL ES App](https://developer.apple.com/library/content/documentation/3DDrawing/Conceptual/OpenGLES_ProgrammingGuide/Performance/Performance.html#//apple_ref/doc/uid/TP40008793-CH105-SW22)
- [Unity - Manual: Memory Considerations when targeting WebGL](https://docs.unity3d.com/Manual/webgl-memory.html)
- [Crunching megapixels in WebGL | Naming Things](http://lacquer.fi/pauli/blog/2012/06/crunching-megapixels-in-webgl/)
- [Weighted Blended Order-Independent Transparency](https://cesiumjs.org/2014/03/14/Weighted-Blended-Order-Independent-Transparency/) and https://github.com/bagnell/bagnell.github.io/tree/master/OITDemo
- [HTML 5 Canvas Composite Operation Demo](http://balefrost.org/programming/CanvasComposite/index.html)
- [Some aspects of WebGL optimisation | codedoc's notes](https://codedoc255.wordpress.com/2015/06/29/some-aspects-of-webgl-optimisation/)
- [WebGL Masking & Composition – Your Majesty Co. – Medium](https://medium.com/@Zadvorsky/webgl-masking-composition-75b82dd4cdfd#)
- [Thoughts On Fast Bitmap Image Rendering · openlayers/openlayers Wiki](https://github.com/openlayers/openlayers/wiki/Thoughts-On-Fast-Bitmap-Image-Rendering)

- [Thinking in WebGL: Reducing Memory Usage | Goo Learn](https://goocreate.com/learn/reducing-memory-usage/)
- [Thinking in WebGL: Reducing Draw Calls | Goo Learn](https://goocreate.com/learn/reducing-draw-calls/)
- [Thinking in WebGL: Reducing CPU calculations | Goo Learn](https://goocreate.com/learn/reducing-cpu-calculations/)

WebGL: Combine textures to texture atlas (decrease texture binds)

To use WebGL for 2D, you can use [`pixi.js`](http://www.pixijs.com/) or [`OrthographicCamera` in Three.js](https://www.script-tutorials.com/WEBGL-WITH-THREE-JS-LESSON-9/)

- [javascript - Three.js - Orthographic camera - Stack Overflow](https://stackoverflow.com/questions/17558085/three-js-orthographic-camera)
- [Three.js Orthographic Camera - Interactive 3D Graphics - YouTube](https://www.youtube.com/watch?v=k3adBAnDpos)
- [Infinite Tubes with Three.js | Codrops](https://tympanus.net/codrops/2017/05/09/infinite-tubes-with-three-js/)

### Reduce WebGL memory usage

- use compressed textures: (WebGL1) S3TC DXT, ASTC, PVRTC, ETC1 or lower precision pixel format: RGB565, RGBA5551, or RGBA4444
- disable mipmap if you don't scale too much (0.75 < n < 1.25) or limit its number
- clear canvas/images used to genereate uploaded textures (be carefull of webgl context loss)
- split to smaller individual elements to remove hidden surface (wasted/unused areas)

### Reduce WebGL artifacts

See [Texture format](Texture format#reduce-artifacts)

### Draw DOM Objects to Canvas2D

Aka Draw DOM node, Draw node, render node

Using `foreignObject` tag, but require document as XHTML not HTML

Note: Safari marked as trainted canvas where SVG contains `foreignObject` elements is drawn. It's appreas to be the same for blob URI SVG.

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="200" height="200">
	<foreignObject x="40" y="40" width="100" height="100" requiredExtensions="http://www.w3.org/1999/xhtml">
		<div xmlns="http://www.w3.org/1999/xhtml">test</div>
	</foreignObject>
</svg>
```

```js
var doc = document.implementation.createHTMLDocument("");
doc.write(html);
doc.documentElement.setAttribute("xmlns", doc.documentElement.namespaceURI);
var html = (new XMLSerializer).serializeToString(doc);
```

The SVG element can be the alternative content of used canvas

See [Restrictions](SVG#restrictions)

- `new XMLSerializer().serializeToString(svgnode)`
- [Drawing DOM objects into a canvas - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Drawing_DOM_objects_into_a_canvas) - [Drawing DOM objects into a canvas - Web APIs | MDN](https://web.archive.org/web/20181006205840/https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Drawing_DOM_objects_into_a_canvas) (archive)
- [cburgmer/rasterizeHTML.js: Renders HTML into the browser's canvas](https://github.com/cburgmer/rasterizeHTML.js)
- https://github.com/niklasvh/html2canvas http://html2canvas.hertzen.com/
- [gabelerner/canvg](https://github.com/gabelerner/canvg)
- [DasSur.ma – DOM2Texture: Abusing Arcane APIs](http://dassur.ma/things/dom2texture/)
- [trevorlinton/webkit.js: Pure JavaScript Port of WebKit](https://github.com/trevorlinton/webkit.js)

### Draw with Canvas2D

- draw roundedRect [How to use arcTo() on an HTML5 canvas](http://www.dbp-consulting.com/tutorials/canvas/CanvasArcTo.html)
- [Drawing lines and arcs with arrow heads on HTML5 Canvas](http://www.dbp-consulting.com/tutorials/canvas/CanvasArrow.html)
- Pencil lines [Exploring canvas drawing techniques — Perfection Kills](http://perfectionkills.com/exploring-canvas-drawing-techniques/)
- SVG [SVG & media queries - JakeArchibald.com](https://jakearchibald.com/2016/svg-media-queries/)

### Canvas2D Interpolation

- bilinear
- bicubic

- https://stackoverflow.com/questions/2303690/resizing-an-image-in-an-html5-canvas
- https://stackoverflow.com/questions/17861447/html5-canvas-drawimage-how-to-apply-antialiasing
- https://jsperf.com/pixel-interpolation/16
- [Bicubic Interpolation : javascript](https://www.reddit.com/r/javascript/comments/jxa8x/bicubic_interpolation/)
- [Pure javascript / HTML5 canvas bilinear image interpolation : programming](https://www.reddit.com/r/programming/comments/o6tx9/pure_javascript_html5_canvas_bilinear_image/)
- [Pure javascript HTML5 canvas bilinear image interpolation](http://strauss.pas.nu/js-bilinear-interpolation.html)
- https://github.com/osuushi/Smooth.js/
- [Bilinear filtering — Wikipedia](https://en.wikipedia.org/wiki/Bilinear_filtering)
- [Bilinear interpolation — Wikipedia](https://en.wikipedia.org/wiki/Bilinear_interpolation)
- [Bicubic interpolation — Wikipedia](https://en.wikipedia.org/wiki/Bicubic_interpolation)
- https://github.com/hughsk/bicubic

### WebGL progressive texture

Aka WebGL progressive image

- [Progressive image](https://github.com/bompo/streamingtextures/) or use bytearray chunks to blob + <img> as native img decoder
- [WebGL — Progressive loading](http://www.khronos.org/webgl/public-mailing-list/archives/1104/msg00056.html)
- [Performance Calendar » Progressive jpegs: a new best practice](http://calendar.perfplanet.com/2012/progressive-jpegs-a-new-best-practice/)

### Use `Uint32Array` to speedup pixel write in Canvas2D

```js
// **TODO: Check endianness**. Uint32Array use the CPU endianness (Intel/x86 is little endian). Use DataView instead
var canvas = document.getElementById('canvas');
var canvasWidth  = canvas.width;
var canvasHeight = canvas.height;
var ctx = canvas.getContext('2d');
var imageData = ctx.getImageData(0, 0, canvasWidth, canvasHeight);
var buf = new ArrayBuffer(imageData.data.length);
var data32 = new Uint32Array(buf);

for (var y = 0; y < canvasHeight; ++y) {
	for (var x = 0; x < canvasWidth; ++x) {
		var value = x * y & 0xff;

		data32[y * canvasWidth + x] =
			(255   << 24) |	// alpha
			(value << 16) |	// blue
			(value <<  8) |	// green
			 value;			// red
	}
}

imageData.data.set(new Uint8ClampedArray(buf));
ctx.putImageData(imgData, 0, 0);
```

- http://jsperf.com/canvas-pixel-manipulation

Or use WebGL, draw in Canvas with WebGL:

```js
// Helper function to compile webGL program
function createWebGLProgram(ctx, vertexShaderSource, fragmentShaderSource) {
	this.ctx = ctx;

	this.compileShader = function(shaderSource, shaderType) {
		var shader = this.ctx.createShader(shaderType);
		this.ctx.shaderSource(shader, shaderSource);
		this.ctx.compileShader(shader);
		return shader;
	};

	var program = this.ctx.createProgram();
	this.ctx.attachShader(program, this.compileShader(vertexShaderSource, this.ctx.VERTEX_SHADER));
	this.ctx.attachShader(program, this.compileShader(fragmentShaderSource, this.ctx.FRAGMENT_SHADER));
	this.ctx.linkProgram(program);
	this.ctx.useProgram(program);

	return program;
}

var image = document.getElementById('image');// some image in DOM

if(image.complete){
	desaturateImage(image);
} else {
	image.onload = function(){
		desaturateImage(image);
	};
}

function desaturateImage(image) {

	var canvas = document.createElement('canvas');
	image.parentNode.insertBefore(canvas, image);
	canvas.width  = image.width;
	canvas.height = image.height;
	image.parentNode.removeChild(image);

	var ctx;
	try {
	  ctx = canvas.getContext("webgl");
	} catch(e) {}

	if (!ctx) {
		// You could fallback to 2D methods here
		alert("Sorry, it seems WebGL is not available.");
	}

	const fragmentShaderSource = `
precision mediump float;
uniform sampler2D u_image; // the texture
varying vec2 v_texCoord; // the texCoords passed from the vertex shader.

void main() {
	vec4 color = texture2D(u_image, v_texCoord);
	float grey = (0.2126 * color.r) + (0.7152 * color.g) + (0.0722 * color.b);
	color.rgb += (grey - color.rgb);
	gl_FragColor = color;
}
`;
	const vertexShaderSource = `
attribute vec2 a_position;
attribute vec2 a_texCoord;
uniform vec2 u_resolution;
varying vec2 v_texCoord;

void main() {
	vec2 clipSpace = (a_position / u_resolution) * 2.0 - 1.0; // convert the rectangle from pixels to clipspace
	gl_Position = vec4(clipSpace * vec2(1, -1), 0, 1);
	v_texCoord = a_texCoord; // pass the texCoord to the fragment shader
}
`;
	var program = createWebGLProgram(ctx, vertexShaderSource, fragmentShaderSource);

	// Expose canvas width and height to shader via u_resolution
	var resolutionLocation = ctx.getUniformLocation(program, "u_resolution");
	ctx.uniform2f(resolutionLocation, canvas.width, canvas.height);

	// Position rectangle vertices (2 triangles)
	var positionLocation = ctx.getAttribLocation(program, "a_position");
	var buffer = ctx.createBuffer();
	ctx.bindBuffer(ctx.ARRAY_BUFFER, buffer);
	ctx.bufferData(ctx.ARRAY_BUFFER, new Float32Array([
		0, 0,
		image.width, 0,
		0, image.height,
		0, image.height,
		image.width, 0,
		image.width, image.height]), ctx.STATIC_DRAW);
	ctx.enableVertexAttribArray(positionLocation);
	ctx.vertexAttribPointer(positionLocation, 2, ctx.FLOAT, false, 0, 0);

	//Position texture
	var texCoordLocation = ctx.getAttribLocation(program, "a_texCoord");
	var texCoordBuffer = ctx.createBuffer();
	ctx.bindBuffer(ctx.ARRAY_BUFFER, texCoordBuffer);
	ctx.bufferData(ctx.ARRAY_BUFFER, new Float32Array([
		0.0, 0.0,
		1.0, 0.0,
		0.0, 1.0,
		0.0, 1.0,
		1.0, 0.0,
		1.0, 1.0]), ctx.STATIC_DRAW);
	ctx.enableVertexAttribArray(texCoordLocation);
	ctx.vertexAttribPointer(texCoordLocation, 2, ctx.FLOAT, false, 0, 0);

	// Create a texture.
	var texture = ctx.createTexture();
	ctx.bindTexture(ctx.TEXTURE_2D, texture);
	// Set the parameters so we can render any size image.
	ctx.texParameteri(ctx.TEXTURE_2D, ctx.TEXTURE_WRAP_S, ctx.CLAMP_TO_EDGE);
	ctx.texParameteri(ctx.TEXTURE_2D, ctx.TEXTURE_WRAP_T, ctx.CLAMP_TO_EDGE);
	ctx.texParameteri(ctx.TEXTURE_2D, ctx.TEXTURE_MIN_FILTER, ctx.NEAREST);
	ctx.texParameteri(ctx.TEXTURE_2D, ctx.TEXTURE_MAG_FILTER, ctx.NEAREST);
	// Load the image into the texture.
	ctx.texImage2D(ctx.TEXTURE_2D, 0, ctx.RGBA, ctx.RGBA, ctx.UNSIGNED_BYTE, image);

	// Draw the rectangle.
	ctx.drawArrays(ctx.TRIANGLES, 0, 6);
}
```

- [Canvas image manipulation techniques · MadebyMike](https://madebymike.com.au//writing/canvas-image-manipulation/)

### WebGL context loosing

Can be forced to release resources. Or happend unexceptly (often after page `hide`)

- https://github.com/mrdoob/three.js/issues/5857
- forceContextLoss `extensions.get( 'WEBGL_lose_context' ).loseContext()` https://github.com/mrdoob/three.js/blob/363648ed473639c7abe3c78b9bbe61386344e297/src/renderers/WebGLRenderer.js#L310
- https://github.com/pixijs/pixi.js/issues/2233
- [WebGL WEBGL_lose_context Khronos Ratified Extension Specification](https://www.khronos.org/registry/webgl/extensions/WEBGL_lose_context/)

### WebGL pre-multiplied alpha

It's enabled by default for WebGL context

Could need to call `blendFunc` with source and destination factors

`gl.pixelStorei(gl.UNPACK_PREMULTIPLY_ALPHA_WEBGL, true);` to pre multiply alpha of pixels of textures (call it before uploading pixel data with `texImage2D()` and `texSubImage2D()` only)
`gl.blendFunc(gl.SRC_ALPHA, gl.ONE_MINUS_SRC_ALPHA);` blend mode when draw with a compressed texture without pre-multiplied alpha
`gl.blendFunc(gl.ONE, gl.ONE_MINUS_SRC_ALPHA);` blend mode when draw with a compressed texture with pre-multiplied alpha
`gl.blendFuncSeparate(gl.SRC_ALPHA, gl.ONE_MINUS_SRC_ALPHA, gl.ONE, gl.ONE_MINUS_SRC_ALPHA);`

See also `getContext("3d", {premultipliedAlpha: false})`

But it's not recommended to work with non pre-multiplied alphas

See [Premultiplied alpha](Blend modes#premultiplied-alpha)

- [WebGL and Alpha](http://webglfundamentals.org/webgl/lessons/webgl-and-alpha.html)
- [WebGL: Why does transparent canvas show clearColor color component when alpha is 0? - Stack Overflow](https://stackoverflow.com/questions/20362023/webgl-why-does-transparent-canvas-show-clearcolor-color-component-when-alpha-is)
- [WebGl Transparency and alpha blending problem](http://in2gpu.com/2014/04/11/webgl-transparency/)
- [WebGL and Canvas Blending](http://balefrost.org/programming/canvas_translucency/index.html)
- http://jsfiddle.net/greggman/pWPPC/
- [Blending with HTML background in WebGL - Stack Overflow](https://stackoverflow.com/questions/11521035/blending-with-html-background-in-webgl)
- [WebGL Specification](https://www.khronos.org/registry/webgl/specs/1.0/#PIXEL_STORAGE_PARAMETERS)
- [WebGL Specification](https://www.khronos.org/registry/webgl/specs/1.0/#TEXIMAGE2D_HTML)
- [WebGL Specification](https://www.khronos.org/registry/webgl/specs/1.0/#PREMULTIPLIED_ALPHA)
- [WebGL, Blending, and Why You're Probably Doing it Wrong](https://limnu.com/webgl-blending-youre-probably-wrong/)
- TL;DR `putImageData()` is a lossly operation [javascript - How can I stop the alpha-premultiplication with canvas imageData? - Stack Overflow](https://stackoverflow.com/questions/23497925/how-can-i-stop-the-alpha-premultiplication-with-canvas-imagedata)

### WebGL detect software rendering

> indicates if a context will be created if the system performance is low

```js
canvas.getContext("3d", {failIfMajorPerformanceCaveat: true});
```

- http://blog.tojicode.com/2013/12/failifmajorperformancecaveat-with-great.html

### SVG filter in canvas

```html
<svg height="0"><filter id="n"><feTurbulence type="fractalNoise" baseFrequency=".01 .01" numOctaves="5"/></filter></svg>
<canvas></canvas>
<script>
const context = document.querySelector("canvas").getContext("2d");
context.filter = "url(#n)";
context.fillRect(0, 0, 1, 1);
</script>
```

### Replace DOM by canvas

Replace all DOM by Canvas.

Maybe it's not the right solution

- [60fps on the mobile web — Flipboard Engineering](http://engineering.flipboard.com/2015/02/mobile-web/)

### Canvas stress test

Usefull for detect low-end devices or old tablets/smartphones

```js
var canvas = document.createElement("canvas");
canvas.width = canvas.height = 1000;
var context = canvas.getContext("2d");
var t0 = performance.now();
// first call drawImage twice. Required by Chrome, Opera, IE and Safari Mobile: it take time at cold start, not in next reloads
context.drawImage(canvas, 0, 0, 1, 1);
context.drawImage(canvas, 0, 0, 1, 1);
var t1 = performance.now();
for(var iter = 0; iter < 50; iter++){
	context.translate(-10, -10);
	context.rotate(Math.PI/2);
	context.translate(10, 10);
	context.drawImage(canvas, 0, 0, 20, 20, 0, 0, 19, 19);
}
var t2 = performance.now();
document.body.textContent = "\ncanvas stress test: "+(t2 - t1).toFixed(4)+"ms (init: "+(t1 - t0).toFixed(4)+"ms)";
```

- https://gist.github.com/mems/39831f33d2a3372af1ff

### 2D WebGL shader

```html
<!--
Chromatic aberration effect
From https://codepen.io/robin-dela/pen/oMOeGg/
-->
<style>
body {
	margin: 0;

}

#bg {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	min-width: 100%;
	min-height: 100%;
	z-index: 0;
}

canvas {
	width: calc(80vh * 1.5);
	height: 80vh;/*calc(80vw / 1.5);*/
	display: block;
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	border: 7px solid rgba(255, 255, 255, .1);
	box-shadow: 0px 0px 10px #00000038;
	z-index: 1;
}
</style>
<canvas id="canvas"></canvas>
<img src="https://robindelaporte.fr/codepen/background.jpg" id="bg" alt="">

<!-- vertex shader -->
<script id="vs" type="f">
	attribute vec2 position;
	attribute vec2 texcoord;

	uniform mat3 u_matrix;

	varying vec2 v_texcoord;

	void main() {
		 gl_Position = vec4(u_matrix * vec3(position, 1), 1);
		 v_texcoord = texcoord;
	}
</script>

<!-- fragment shader -->
<script id="fs" type="f">
	precision mediump float;

	uniform vec2 u_mouse;

	uniform sampler2D u_originalImage;

	varying vec2 v_texcoord;

	void main() {
		 vec4 originalR = texture2D(u_originalImage, (v_texcoord + (u_mouse * 1.0)));
		 vec4 originalG = texture2D(u_originalImage, (v_texcoord + (u_mouse * 0.6)));
		 vec4 originalB = texture2D(u_originalImage, (v_texcoord + (u_mouse * 0.2)));

		 vec4 red = vec4(originalR.r, 0.0, 0.0, 1.0);
		 vec4 green = vec4(0.0, originalG.g, 0.0, 1.0);
		 vec4 blue = vec4(0.0, 0.0, originalB.b, 1.0);

		 gl_FragColor = blue + red + green;
	}
</script>
<script>
function main() {
	// Get A WebGL context
	/** @type {HTMLCanvasElement} */
	const canvas = document.getElementById("canvas");
	const gl = canvas.getContext("webgl");
	if (!gl) {
		return;
	}

	let originalImage = { width: 1, height: 1 }; // replaced after loading
	const originalTexture = twgl.createTexture(gl, {
		src: "https://robindelaporte.fr/codepen/marie.jpg",
		crossOrigin: '',
	}, (err, texture, source) => {
		originalImage = source;
	});

	// compile shaders, link program, lookup location
	const programInfo = twgl.createProgramInfo(gl, ["vs", "fs"]);

	// calls gl.createBuffer, gl.bindBuffer, gl.bufferData for a quad
	const bufferInfo = twgl.primitives.createXYQuadBufferInfo(gl);

	const mouse = [0, 0];
	canvas.addEventListener('mousemove', (event) => {
		mouse[0] = (event.clientX / gl.canvas.clientWidth  * 2 - 1) * -0.025;
		mouse[1] = (event.clientY / gl.canvas.clientHeight * 2 - 1) * -0.025;
	});

	canvas.addEventListener('mouseout', (event) => {
		mouse[0] = 0;
		mouse[1] = 0;
	});

	canvas.addEventListener('touchmove', (event) => {
		mouse[0] = (event.touches[0].clientX / gl.canvas.clientWidth  * 2 - 1) * -0.02;
		mouse[1] = (event.touches[0].clientY / gl.canvas.clientHeight * 2 - 1) * -0.02;
	});

	canvas.addEventListener('touchend', (event) => {
		mouse[0] = 0;
		mouse[1] = 0;
	});

	var nMouse = [0, 0];
	var oMouse = [0, 0];

	requestAnimationFrame(render);

	function render() {
		twgl.resizeCanvasToDisplaySize(gl.canvas);

		gl.viewport(0, 0, gl.canvas.width, gl.canvas.height);

		gl.clearColor(0, 0, 0, 0);
		gl.clear(gl.COLOR_BUFFER_BIT);

		gl.useProgram(programInfo.program);

		// calls gl.bindBuffer, gl.enableVertexAttribArray, gl.vertexAttribPointer
		twgl.setBuffersAndAttributes(gl, programInfo, bufferInfo);

		const canvasAspect = gl.canvas.clientWidth / gl.canvas.clientHeight;
		const imageAspect = originalImage.width / originalImage.height;
		const mat = m3.scaling(imageAspect / canvasAspect, -1);

		nMouse[0] += (mouse[0] - nMouse[0]) * 0.05;
		nMouse[1] += (mouse[1] - nMouse[1]) * 0.05;

		// calls gl.activeTexture, gl.bindTexture, gl.uniformXXX
		twgl.setUniforms(programInfo, {
			u_matrix: mat,
			u_originalImage: originalTexture,
			u_mouse: nMouse,
		});

		// calls gl.drawArrays or gl.drawElements
		twgl.drawBufferInfo(gl, bufferInfo);

		requestAnimationFrame(render);
	}
}

main();
</script>
```

### WebGL shader performance

- minimise branching (if/else, etc.), nested branches, etc. because each branche will be executed (in series), the after the result will be picked
- minimise texture quantity
- minimise

- [Steve Sanderson - Write massively-parallel GPU code for the browser with WebGL on Vimeo](https://vimeo.com/97329154#t=44m52s)

### Computing with WebGL

See [GPU computing](Algorithms#gpu-computing)

using GPU

- [Write massively-parallel GPU code for the browser with WebGL (NDC 2014)](http://blog.stevensanderson.com/2014/06/11/write-massively-parallel-gpu-code-for-the-browser-with-webgl-ndc-2014/)
- [Steve Sanderson - Write massively-parallel GPU code for the browser with WebGL on Vimeo](https://vimeo.com/97329154)
- stream reduction (reduce multiple data to one) using intermedaire texture to parallalise over groups (e.g. rows)

See also SIMD

- [SIMD - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SIMD)
- [Introducing SIMD.js ★ Mozilla Hacks – the Web developer blog](https://hacks.mozilla.org/2014/10/introducing-simd-js/)
- [gpujs/gpu.js: GPU Accelerated JavaScript](https://github.com/gpujs/gpu.js) - JS function to shader

### Generate images

- [Generating Images in JavaScript Without Using the Canvas API](https://medium.com/the-guardian-mobile-innovation-lab/generating-images-in-javascript-without-using-the-canvas-api-77f3f4355fad)

### Antialias

Tips:

- disable antialias
- use mipmap
- force canvas supersampling (same value as retina display)

## Selection

```js
input.selectionStart
input.setSelectionRange()
```

```js
var selection = window.getSelection();
if(selection.rangeCount){
	var range = selection.getRangeAt(0);
	range.commonAncestorContainer
	range.endOffset
}
```

- https://developer.mozilla.org/en-US/docs/Web/API/Range
- https://stackoverflow.com/questions/17678843/cant-restore-selection-after-html-modify-even-if-its-the-same-html
- http://www.quirksmode.org/dom/range_intro.html
- https://code.google.com/p/rangy/wiki/RangySelection

### Position in viewport

**Note: on mobile there is a custom menu for selection (iOS).** If a menu is displayed use a delay `document.body.addEventListener("mouseup", event => setTimeout(showMenu, 100));`

```js
var selection = window.getSelection()
if (selection.rangeCount > 0) {
	selection.toString().trim(); // get the text
	selection.anchorNode.parentNode; // get the element wrapping the text
	selection.getRangeAt(0).getBoundingClientRect(); // get the bounding box
}
```

## `contentEditable`

`document.documentElement.contentEditable = true;` is the same as `document.designMode = "on";`

Aka richtext / rich textarea

About:

- [ContentEditable — The Good, the Bad and the Ugly — Content Uneditable — Medium](https://medium.com/content-uneditable/contenteditable-the-good-the-bad-and-the-ugly-261a38555e9c)
- [Why ContentEditable is Terrible — Medium Engineering — Medium](https://medium.com/medium-eng/why-contenteditable-is-terrible-122d8a40e480)
- [Fixing ContentEditable — Content Uneditable — Medium](https://medium.com/content-uneditable/fixing-contenteditable-1a9a5073c35d)
- [Content Editable is a Scary Place — Florian’s Blog](http://florian.rivoal.net/blog/2016/12/content-editable-is-a-scary-place/)

See also [text editors libraries](Text editors)

## Custom Controls

- scrollable
- default action `input:default`
- `.tabIndex = -1`, `.removeAttribute("tabindex")`

If open a select box, use an hidden select and open it with (only works on Chrome ?-53 but not 53+ and Safari):

```js
var element;
var eventDispatched = false;
if(document.createEvent) {
	var event = new MouseEvent("mousedown");//document.createEvent("MouseEvents");
	//event.initMouseEvent("mousedown", true, true, window, 0, 0, 0, 0, 0, false, false, false, false, 0, null);
	eventDispatched = element.dispatchEvent(event);
}
if(!eventDispatched) {
	// Old browser or fail to do it
}
```

-
- [javascript - How can you programmatically tell an HTML SELECT to drop down (for example, due to mouseover)? - Stack Overflow](https://stackoverflow.com/questions/249192/how-can-you-programmatically-tell-an-html-select-to-drop-down-for-example-due/10136523#10136523)
- [Using WAI-ARIA in HTML — Custom Control Accessible Development Checklist](http://w3c.github.io/aria-in-html/#custom-control-accessible-development-checklist)
- [Roving tabindex -- A11ycasts #06 - YouTube](https://www.youtube.com/watch?v=uCIC2LNt0bk)
- [Keyboard-navigable JavaScript widgets - Accessibility | MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/Keyboard-navigable_JavaScript_widgets)
- [Keyboard Event Viewer](https://w3c.github.io/uievents/tools/key-event-viewer.html)

### Suggest email address corrections (domain e.g. gnail.com → gmail.com)

Test domain availability (DNS or IP).
Display a message (after a timeout) (for "luke@gnail.com") "Did you mean luke@gmail.com?" (click on this message update the input).
But be carefull, this can add errors like hotmail.com and hotmail.co.uk (used by UK users)
In addition: suggest `.` for `。` (chinese)
Autocomplete is weird (using the [`<datalist>`](https://developer.mozilla.org/en/docs/Web/HTML/Element/datalist) element) to complete addresses the system don't know yet (only the user know it at this point). See [Awesomplete: Ultra lightweight, highly customizable, simple autocomplete, by Lea Verou](http://leaverou.github.io/awesomplete/)

- [cxpartners | Towards an easier way to enter email addresses](http://www.cxpartners.co.uk/cxblog/towards-an-easier-way-to-enter-email-addresses/)
- [Edit distance — Wikipedia](https://en.wikipedia.org/wiki/Edit_distance)
- [List of Popular Domains · mailcheck/mailcheck Wiki](https://github.com/mailcheck/mailcheck/wiki/list-of-popular-domains)

### Credit card field

Field mask

```html
<!-- http://jsfiddle.net/Lhxpg6wb/1/ -->
<style>
	html{
		font-family: sans-serif;
	}
	.js .extended{
		position: absolute !important;
		overflow: hidden;
		clip: rect(0px, 0px, 0px, 0px);
		width: 1px;
		height: 1px;
		border: none;
		opacity: 0;
	}
	.extended-input, input{
		min-height: 1em;
		line-height: 1.4em;
		width: 200px;
		display: inline-block;

		/* Look like input field */
		font: 16px sans-serif;
		padding: 0.4em;
		background-color: white;
		border: 1px solid #F0F0F0;
		color: #000;
		cursor: text;
	}
	.extended-input-part{
		display: inline-block;
	}
	.extended-input-part + .extended-input-part::before{
		content: " - ";
		white-space: pre
	}
</style>
<form action="" id="form" method="post">
	<p>
		<label for="cc-number-alt">Credit Card (Without JS):</label>
		<input id="cc-number-alt" name="cc-number-alt" pattern="[0-9]" maxlength="16">
	</p>
	<p>
		<label for="cc-number">Credit Card:</label>
		<input id="cc-number" name="cc-number" maxlength="16">
	</p>
	<button>Send</button>
</form>
<script>
	var html = document.documentElement;
	html.classList.add("js");
	var body = document.body;
	var form = document.getElementById("form");

	var input = document.getElementById("cc-number");
	input.classList.add("extended");

	var extendedInput = document.createElement("div");
	extendedInput.contentEditable = true;
	extendedInput.setAttribute("aria-controls", input.id);
	extendedInput.classList.add("extended-input");

	extendedInput.addEventListener("input", event => {
		var groupLength = 4;
		var rawContent = extendedInput.textContent;
		var content = rawContent.substr(0, input.maxLength).replace(/(?:\s|[^0-9])+/, "");
		// TODO support insertions and maxLength
		var numChars = content.length;

		// No changes
		if(rawContent == input.value){
			console.log(content, rawContent);
			return;
		}

		// Get current caret position
		var selection = window.getSelection();
		var range;
		var caretPos = -1;
		// TODO loop through all ranges
		if(selection.rangeCount){
			range = selection.getRangeAt(0);
			var node = range.endContainer;
			if(node == extendedInput){
				caretPos = 0;
			}
			// A text node outside spans
			if(node.nodeType == Node.TEXT_NODE && node.parentNode == extendedInput){
				caretPos = 0;
				while( (node = node.previousSibling) != null ){
					caretPos += node.nodeType == Node.TEXT_NODE ? node.length : /*should be a generated span*/ groupLength;
				}
				caretPos += range.endOffset;
			}
			else if (extendedInput.contains(node)) {
				caretPos = 0;
				// Text node (span should only contains one text node)
				if(node.nodeType == Node.TEXT_NODE){
					node = node.parentNode;
				}
				// Find the right span
				while( (node = node.previousSibling) != null ){ caretPos += groupLength; }
				caretPos += range.endOffset;
			}

			// Limit to max chars (ex.: when forbidden chars are added)
			Math.min(caretPos, Math.max(numChars - 1, 0));
		}

		// TODO optimize it (re-use spans)
		var index = 0;
		var richContent = "";
		while(index < numChars){
			richContent += "<span class=\"extended-input-part\">" + content.substr(index, groupLength) + "</span>";
			index += groupLength;
		}

		// Update content
		input.value = content;
		extendedInput.innerHTML = richContent;

		// if caret exist and was placed after 0
		if(caretPos > 0){
			var range = document.createRange();
			var spans = extendedInput.getElementsByTagName("span");
			var selectedNode;
			var selectionOffset;
			if(spans.length > 0){
				var spanIndex = caretPos / groupLength | 0;
				// Last char of last span
				if(spanIndex >= spans.length){
					selectedNode = spans[spanIndex - 1].firstChild;
					selectionOffset = groupLength;
				}else{
					selectedNode = spans[spanIndex].firstChild;
					selectionOffset = caretPos % groupLength;
				}
			}else{
				// content.length should equals 0
				selectedNode = extendedInput;
				selectionOffset = 0;
			}

			range.setStart(selectedNode, selectionOffset);
			range.setEnd(selectedNode, selectionOffset);
			selection.removeAllRanges();
			selection.addRange(range);
		}
	}, false);

	input.parentNode.insertBefore(extendedInput, input.nextSibling);
</script>
```

To go further, Input masking:

- listen past event (to detect inserts/replaces) `event.clipboardData.types["text/plain"]`
- Test if richcontent not changed like bold or italic
- aria input method
- read and listen input value changes
- (tabindex -1 for input)
- display none input
- fix replace with maxlength
- valid test for credit card (see [Luhn algorithm](Algorithms#luhn)), not all credit card number use this algorithm
- credit card detect issuer (see [Credit Card](Credit Card))

Formatting examples:

- credit card (groups changes based on card type)
- phone number (groups changes based on country)
- dates: DD/MM/YYYY, MM/YYYY, etc.
- numeral: 1,000,000.000
- ISBN 978-3-16-148410-0 (as barcode 9 783161 484100) Check other patterns: [International Standard Book Number — Wikipedia](https://en.wikipedia.org/wiki/International_Standard_Book_Number)
- custom: 0000·000·000·000 PREFIX-0000-0000-0000
- VAT, IBAN, etc.

See also: `input.selectionStart`, `input.selectionEnd` and `input.selectionDirection`

- (method on blur show a formatted element) https://css-tricks.com/input-masking/#article-header-id-3 and https://github.com/filamentgroup/politespace
- [datalist experiment](http://demo.agektmr.com/datalist/)
- https://github.com/kenkeiter/skeuocard
- https://jsfiddle.net/nosir/aLnhdf3z/ (usage examples)

### Form submitter and `novalidate` for some fields

```js
// In spec activable element will dispatch a click event
// works also with implicit submission (where you hit enter in a text field and it picks the default submit button)
// https://www.w3.org/Bugs/Public/show_bug.cgi?id=23320
// http://www.w3.org/TR/html5/forms.html#default-button
// http://www.w3.org/TR/html5/forms.html#concept-submit-button
// http://www.w3.org/TR/html5/forms.html#submit-button-state-%28type=submit%29
// http://www.w3.org/TR/html5/forms.html#image-button-state-%28type=image%29
// http://www.w3.org/TR/html5/forms.html#the-button-element
// https://stackoverflow.com/questions/2066162/how-can-i-get-the-button-that-caused-the-submit-from-the-form-submit-event

var submitter = null;
var form;
form.addEventListener("click", click, false);
form.addEventListener("submit", submit, false);

// save when click on form:
// Not called if the propagation stopped or the button disabled
function click(event){
	// If the default action was prevented
	if(event.defaultPrevented){
		return;
	}

	// Find the submitter. But not if the default action was prevented
	var element = event.target;
	while(element && element != this._form){
		if(
			element.nodeName == "INPUT" && (element.type == "submit" || element.type == "image")
			|| element.nodeName == "BUTTON" && element.type == "submit"
		){
			submitter = element;

			break;
		}
		element = element.parentElement;
	}
}

function submit(event){
	submitter;
}

// Should listen invalid and submit event and change based on submitter
```

### Implicit submission

```js
var form = input.form;// Form owner (parent or defined via the attribute `form` on input tag)
var button = form.ownerDocument.createElement("input");
// Hide it (style and for ATs)
button.style.display = "none";
button.tabIndex = -1;
button.setAttribute("aria-hidden", "true");
button.setAttribute("role", "presentation");
button.type = "submit";
form.appendChild(button).click();
form.removeChild(button);
```

- http://dabblet.com/gist/97a733d9c787dcf99cff
- [HTML 5.1: 4.10. Forms#formsReferenced in:4.2.3. The base element10.7.1. Links, forms, and navigationElements](https://www.w3.org/TR/html51/sec-forms.html#implicit-submission)

### Tabindex

- http://fluidproject.org/blog/2008/01/09/getting-setting-and-removing-tabindex-values-with-javascript/
- http://www.weba11y.com/blog/2007/11/29/fun-with-the-tabindex-attribute/

### Color picker

- [React Color](http://casesandberg.github.io/react-color/)

### Date picker

- [10 jQuery Time Picker Plugins](https://www.sitepoint.com/10-jquery-time-picker-plugins/)
- [Useful Calendar & Date Picker Scripts For Web Developers - Hongkiat](http://www.hongkiat.com/blog/useful-calendar-date-picker-scripts-for-web-developers/)
- [Date picker module accessibility](https://docs.google.com/spreadsheets/d/1Q-apLCPEyV-hJYVBN-wN3FS7AOSx9YqQJGj-Y2rW6No/edit#gid=0) (yes for: [jQuery UI DatePicker](http://www.deque.com/blog/accessible-jquery-ui-datepicker/), [Pikaday](https://github.com/dbushell/Pikaday/pull/522), [Accessible Bootstrap Date Picker](http://eureka2.github.io/ab-datepicker/))

See [Calendar](HTML#calendar) for valid markup / semantic

From https://bugzilla.mozilla.org/show_bug.cgi?id=1069609#attach_8710338

```html
<!DOCTYPE html>
  <head>
	<title>Calendar</title>
	<meta charset="UTF-8"/>
	<style>
	  :root {
		--dateRangeTransformOrigin: 0 0;
		--dateRangeTransition: 0.3s linear;
	  }

	  #calendar {
		position: absolute;
		min-width: 220px;
		box-shadow: 0 0 4px rgba(0, 0, 0, 0.2);
		border: 1px solid rgb(209, 209, 209);
		border-radius: 4px;
		padding: 4px;
		font-family: Segoe UI;
		font-size: 12px;
		-moz-user-select: none;
	  }

	  #options {
		display: flex;
		margin-bottom: 2px;
	  }

	  button {
		border: 1px solid rgb(209, 209, 209);
		border-radius: 2px;
		background-color: rgb(251, 251, 251);
	  }

	  button:not(:last-child) {
		margin-right: 2px;
	  }

	  a {
		text-decoration: none;
		color: black;
	  }

	  #previous,
	  #next {
		width: 20px;
		padding: 0;
		background-position: 50%;
		background-repeat: no-repeat;
	  }

	  #previous[disabled] {
		background-image:  url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAICAYAAADED76LAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsQAAA7EAZUrDhsAAAAGYktHRAD/AP8A/6C9p5MAAAAHdElNRQffBwYJLS5L2us5AAAARklEQVQoU22PMQoAMAgDQ9/l6LPd9F8pBWnRepOSQwk44O45kQuNiICZ5QYUoYeHK0zh4XvRuYKIQFVze5QLo5RtCq8muQGeQE7l/ncOAQAAAABJRU5ErkJggg==);
	  }

	  #previous {
		background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAICAYAAADED76LAAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAAsTAAALEwEAmpwYAAAAB3RJTUUH3wcGCS0uS9rrOQAAADdJREFUGNNj+P//PwM6ZmBgaICzsUkyMDD8x6oAJolVAbIksgImBkKAaCtwOZIFi4kNjIyMcD4ASftyG4GZFz4AAAAASUVORK5CYII=);
	  }

	  #next {
		background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAICAYAAADED76LAAAABmJLR0QAAAAAAAD5Q7t/AAAACXBIWXMAAAsTAAALEwEAmpwYAAAAB3RJTUUH3wcGCSgVh6b2WAAAADNJREFUGNNj+P//P8P///8ZGBgYGmBsZMyApOA/NkXoCjAUYVOAooiJgRAg1Qq8jsTqTQDquIQCHxMrkAAAAABJRU5ErkJggg==);
	  }

	  #next[disabled] {
		background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAICAYAAADED76LAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsQAAA7EAZUrDhsAAAAGYktHRAD/AP8A/6C9p5MAAAAHdElNRQffBwYJLS5L2us5AAAARElEQVQoU3XPsQ0AIAhEUeJclIxNB3thMBeNoK+C8BsowMww3QaBqpK7Yzt2kF7RFaQataBqgYgQM2MrQT0u+ObzZsQEgQBO5bVjtH8AAAAASUVORK5CYII=);
	  }

	  #current {
		flex-grow: 1;
	  }

	  #picker {
		position: relative;
		width: 220px;
		height: 143px;
		overflow: hidden;
	  }

	  .days,
	  .months {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		border: 1px solid rgb(193, 193, 193);
		border-radius: 2px;
		border-spacing: 0;
		cursor: default;
		transform-origin: var(--dateRangeTransformOrigin);
		transition: var(--dateRangeTransition);
	  }

	  .days.hidden {
		transform: scaleX(0.25) scaleY(0.333333);
		pointer-events: none;
		opacity: 0;
	  }

	  .days th {
		width: 14.285714285714285714285714285714%;
		font-weight: normal;
		background-color: rgb(235, 235, 235);
		color: gray;
		border-bottom: 1px solid rgb(193, 193, 193);
	  }

	  .days :-moz-any(th, td) {
		height: 20px;
	  }

	  :-moz-any(.days, .months) :-moz-any(th, td) {
		padding: 0;
		text-align: center;
	  }

	  :-moz-any(.days, .months) td {
		border-radius: 2px;
	  }

	  :-moz-any(.days, .months) td:not(.selected):-moz-any(:hover,:focus) {
		background-color: rgb(191, 228, 246);
	  }

	  .previous-timespan {
		top: -143px;
	  }

	  .next-timespan {
		top: 143px;
	  }

	  .show-previous .previous-timespan {
		top: 0;
	  }

	  .show-previous .current-timespan {
		top: 143px;
	  }

	  .show-next .next-timespan {
		top: 0;
	  }

	  .show-next .current-timespan {
		top: -143px;
	  }

	  .otherMonth {
		color: gray;
	  }

	  .selected {
		background-color: rgb(0, 149, 221);
		color: white;
	  }

	  .months {
		pointer-events: none;
		transform: scaleX(4.1) scaleY(3);
		position: absolute;
		opacity: 0;
		transform-origin: var(--dateRangeTransformOrigin);
		transition: var(--dateRangeTransition);
	  }

	  .months.display {
		transform: scale(1);
		pointer-events: auto;
		opacity: 1;
	  }

	  .months td {
		height: 47px;
	  }
	</style>
	<script>
	function selectDate(evt) {
	  var selectedDate = document.querySelector(".selected");
	  if (selectedDate) {
		selectedDate.classList.remove("selected");
	  }

	  if (evt.target.localName === "td") {
		if (evt.target.classList.contains("otherMonth")) {
		  var picker = document.getElementById("picker");
		  var currentID = "";
		  if (evt.target.textContent < 15) {
			switchToNextDateRange();

			switch (picker.className) {
			  case "":
				currentID = "days-current";
				break;

			  case "show-next":
				currentID = "days-next";
				break;
			}
		  } else {
			switchToPreviousDateRange();

			switch (picker.className) {
			  case "show-previous":
				currentID = "days-previous";
				break;

			  case "":
				currentID = "days-current";
				break;
			}
		  }

		  if (currentID !== "") {
			var days = document.querySelectorAll("#" + currentID + " td:not(.otherMonth)");

			for (var i = 0; i < days.length; i++) {
			  if (days[i].textContent === evt.target.textContent) {
				var clickEvent = new MouseEvent("click", {
				  view: window,
				  bubbles: true,
				  cancelable: true
				});
				days[i].dispatchEvent(clickEvent);
				break;
			  }
			}
		  }
		} else {
		  evt.target.classList.add("selected");
		}
	  }
	}

	function expandDateRange() {
	  var days = document.getElementById("days-current");
	  days.classList.toggle("hidden");

	  var months = document.getElementById("months-current");
	  months.style.display = "table";
	  months.classList.toggle("display");

	  var current = document.getElementById("current");

	  current.textContent = months.classList.contains("display") ? "2016" : "January, 2016";
	}

	function switchToPreviousDateRange() {
	  var picker = document.getElementById("picker");
	  var previousButton = document.getElementById("previous");
	  var nextButton = document.getElementById("next");

	  switch (picker.className) {
		case "":
		  picker.className = "show-previous";
		  current.textContent = "December, 2015";
		  previousButton.disabled = true;
		  break;

		case "show-next":
		  picker.className = "";
		  current.textContent = "January, 2016";
		  nextButton.disabled = false;
		  break;
	  }
	}

	function switchToNextDateRange() {
	  var picker = document.getElementById("picker");
	  var previousButton = document.getElementById("previous");
	  var nextButton = document.getElementById("next");

	  switch (picker.className) {
		case "":
		  picker.className = "show-next";
		  current.textContent = "February, 2016";
		  nextButton.disabled = true;
		  break;

		case "show-previous":
		  picker.className = "";
		  current.textContent = "January, 2016";
		  previousButton.disabled = false;
		  break;
	  }
	}

	function changeDateRange(evt) {
	  if (evt.deltaY > 0) {
		switchToNextDateRange();
	  } else {
		switchToPreviousDateRange();
	  }
	}

	window.addEventListener("load", () => {
	  var picker = document.getElementById("picker");
	  picker.addEventListener("click", selectDate);
	  picker.addEventListener("wheel", changeDateRange);

	  var previousButton = document.getElementById("previous");
	  previousButton.addEventListener("click", switchToPreviousDateRange);

	  var nextButton = document.getElementById("next");
	  nextButton.addEventListener("click", switchToNextDateRange);

	  var month = document.getElementById("current");
	  month.addEventListener("click", expandDateRange);
	});
	</script>
  </head>
  <body>
	<div id="calendar">
	  <div id="options">
		<button id="previous" tabindex="1"></button>
		<button id="current" tabindex="2">January, 2016</button>
		<button id="next" tabindex="3"></button>
		<button id="today" tabindex="4">today</button>
	  </div>
	  <div id="picker">
		<table id="months-current" class="months">
		  <tbody>
			<tr>
			  <td>Jan</td>
			  <td>Feb</td>
			  <td>Mar</td>
			  <td>Apr</td>
			</tr>
			<tr>
			  <td>May</td>
			  <td>Jun</td>
			  <td>Jul</td>
			  <td>Aug</td>
			</tr>
			<tr>
			  <td>Sep</td>
			  <td>Oct</td>
			  <td>Nov</td>
			  <td>Dec</td>
			</tr>
		  </tbody>
		</table>
		<table id="days-previous" class="days previous-timespan">
		  <thead>
			<tr>
			  <th>Sun</th>
			  <th>Mon</th>
			  <th>Tue</th>
			  <th>Wed</th>
			  <th>Thu</th>
			  <th>Fri</th>
			  <th>Sat</th>
			</tr>
		  </thead>
		  <tbody>
			<tr>
			  <td class="otherMonth">29</td>
			  <td class="otherMonth">30</td>
			  <td>1</td>
			  <td>2</td>
			  <td>3</td>
			  <td>4</td>
			  <td>5</td>
			</tr>
			<tr>
			  <td>6</td>
			  <td>7</td>
			  <td>8</td>
			  <td>9</td>
			  <td>10</td>
			  <td>11</td>
			  <td>12</td>
			</tr>
			<tr>
			  <td>13</td>
			  <td>14</td>
			  <td>15</td>
			  <td>16</td>
			  <td>17</td>
			  <td>18</td>
			  <td>19</td>
			</tr>
			<tr>
			  <td>20</td>
			  <td>21</td>
			  <td>22</td>
			  <td>23</td>
			  <td>24</td>
			  <td>25</td>
			  <td>26</td>
			</tr>
			<tr>
			  <td>27</td>
			  <td>28</td>
			  <td>29</td>
			  <td>30</td>
			  <td>31</td>
			  <td class="otherMonth">1</td>
			  <td class="otherMonth">2</td>
			</tr>
			<tr>
			  <td class="otherMonth">3</td>
			  <td class="otherMonth">4</td>
			  <td class="otherMonth">5</td>
			  <td class="otherMonth">6</td>
			  <td class="otherMonth">7</td>
			  <td class="otherMonth">8</td>
			  <td class="otherMonth">9</td>
			</tr>
		  </tbody>
		</table>
		<table id="days-current" class="days current-timespan">
		  <thead>
			<tr>
			  <th>Sun</th>
			  <th>Mon</th>
			  <th>Tue</th>
			  <th>Wed</th>
			  <th>Thu</th>
			  <th>Fri</th>
			  <th>Sat</th>
			</tr>
		  </thead>
		  <tbody>
			<tr>
			  <td class="otherMonth" tabindex="5">27</td>
			  <td class="otherMonth" tabindex="6">28</td>
			  <td class="otherMonth" tabindex="7">29</td>
			  <td class="otherMonth" tabindex="8">30</td>
			  <td class="otherMonth" tabindex="9">31</td>
			  <td tabindex="10">1</td>
			  <td tabindex="11">2</td>
			</tr>
			<tr>
			  <td tabindex="12">3</td>
			  <td tabindex="13">4</td>
			  <td tabindex="14">5</td>
			  <td tabindex="15">6</td>
			  <td tabindex="16">7</td>
			  <td tabindex="17">8</td>
			  <td tabindex="18">9</td>
			</tr>
			<tr>
			  <td tabindex="19">10</td>
			  <td tabindex="20">11</td>
			  <td tabindex="21">12</td>
			  <td tabindex="22">13</td>
			  <td tabindex="23">14</td>
			  <td tabindex="24">15</td>
			  <td tabindex="25">16</td>
			</tr>
			<tr>
			  <td tabindex="26">17</td>
			  <td tabindex="27">18</td>
			  <td tabindex="28">19</td>
			  <td tabindex="29">20</td>
			  <td class="selected" tabindex="30">21</td>
			  <td tabindex="31">22</td>
			  <td tabindex="32">23</td>
			</tr>
			<tr>
			  <td tabindex="33">24</td>
			  <td tabindex="34">25</td>
			  <td tabindex="35">26</td>
			  <td tabindex="36">27</td>
			  <td tabindex="37">28</td>
			  <td tabindex="38">29</td>
			  <td tabindex="39">30</td>
			</tr>
			<tr>
			  <td tabindex="40">31</td>
			  <td class="otherMonth" tabindex="41">1</td>
			  <td class="otherMonth" tabindex="42">2</td>
			  <td class="otherMonth" tabindex="43">3</td>
			  <td class="otherMonth" tabindex="44">4</td>
			  <td class="otherMonth" tabindex="45">5</td>
			  <td class="otherMonth" tabindex="46">6</td>
			</tr>
		  </tbody>
		</table>
		<table id="days-next" class="days next-timespan">
		  <thead>
			<tr>
			  <th>Sun</th>
			  <th>Mon</th>
			  <th>Tue</th>
			  <th>Wed</th>
			  <th>Thu</th>
			  <th>Fri</th>
			  <th>Sat</th>
			</tr>
		  </thead>
		  <tbody>
			<tr>
			  <td class="otherMonth">31</td>
			  <td>1</td>
			  <td>2</td>
			  <td>3</td>
			  <td>4</td>
			  <td>5</td>
			  <td>6</td>
			</tr>
			<tr>
			  <td>7</td>
			  <td>8</td>
			  <td>9</td>
			  <td>10</td>
			  <td>11</td>
			  <td>12</td>
			  <td>13</td>
			</tr>
			<tr>
			  <td>14</td>
			  <td>15</td>
			  <td>16</td>
			  <td>17</td>
			  <td>18</td>
			  <td>19</td>
			  <td>20</td>
			</tr>
			<tr>
			  <td>21</td>
			  <td>22</td>
			  <td>23</td>
			  <td>24</td>
			  <td>25</td>
			  <td>26</td>
			  <td>27</td>
			</tr>
			<tr>
			  <td>28</td>
			  <td>29</td>
			  <td class="otherMonth">1</td>
			  <td class="otherMonth">2</td>
			  <td class="otherMonth">3</td>
			  <td class="otherMonth">4</td>
			  <td class="otherMonth">5</td>
			</tr>
			<tr>
			  <td class="otherMonth">6</td>
			  <td class="otherMonth">7</td>
			  <td class="otherMonth">8</td>
			  <td class="otherMonth">9</td>
			  <td class="otherMonth">10</td>
			  <td class="otherMonth">11</td>
			  <td class="otherMonth">12</td>
			</tr>
		  </tbody>
		</table>
	  </div>
	</div>
  </body>
</html>
```

### Keypad

- [Better keyboard navigation with progressive enhancement | Christian Heilmann](https://www.christianheilmann.com/2016/08/15/better-keyboard-navigation-with-progressive-enhancement/?utm_source=codropscollective)

### AJAX Form

- [Enhancing a comment form: From basic to custom error message to BackgroundSync | justmarkup](https://justmarkup.com/log/2016/10/enhancing-a-comment-form/)
- [Submit form with AJAX](#submit-form-with-ajax)

### Combobox with multiselect listbox

- [Non-editable combobox with multiselect listbox](http://accessibleculture.org/misc/aria/combobox/combobox.html) see also https://twitter.com/jkiss/status/757780446541336576

## Native loading indicator

> Polling triggers loading indicator and will communicate mixed signals to your visitors. There’s iframe hacks around this, yes, iframe hacks.
— Arnout Kazemier

- [Browser Busy Indicators | High Performance Web Sites](http://www.stevesouders.com/blog/2013/06/16/browser-busy-indicators/)

## Application cache

http://alistapart.com/article/application-cache-is-a-douchebag

## Templating

- http://sylvainpv.developpez.com/tutoriels/javascript/guide-templating-client/
- XSLT

## SVG document communication with parent document

[Context messaging](#context-messaging) or listen load event on object/embed/iframe and access to `getSVGDocument()` or `contentDocument`

Inside SVG doc `element.ownerDocument` and `window.parent` or `parent` equals window of parent

> Acid3 test checks for (subtest #74)

- https://productforums.google.com/forum/#!topic/chrome/VdHczHa7vxM
- https://stackoverflow.com/questions/4911525/is-it-possible-to-navigate-svg-objects-elements-from-enclosing-html
- https://stackoverflow.com/questions/337293/how-to-check-if-an-embedded-svg-document-is-loaded-in-an-html-page/3510578#3510578
- https://stackoverflow.com/questions/15980971/inline-svg-vs-object-embedded

## Relayout, repaint, reflow

Use `transform` instead of `top`/`left`/`bottom`/`right` style properties. These last ones repaint elements where the first one don't.

```js
element.offsetHeight;// get the value and evaluate it (else it's will be discarded, and the reflow will not be triggered)
// or
void(element.offsetHeight);
```

> you force a synchronous style flush any time you query for style information after the DOM has changed within the same frame tick. Depending on whether or not the style information you’re asking for has something to do with size or position, you may also cause a layout recalculation (also referred to as layout flush or reflow)

```js
requestAnimationFrame(() => {
	setTimeout(() => {
		// This code will be run ASAP after Style and Layout information have
		// been calculated and the paint has occurred. Unless something else
		// has dirtied the DOM very early, querying for style and layout information
		// here should be cheap.

		// Do _not_ under any circumstances write to the DOM in one of these callbacks!
	}, 0);
});
```

```js
(async () => {
	// do something...
	while(true){
		const now = await new Promise((resolve) => requestAnimationFrame(resolve));
		// do something just before repaint
	}
})()
```

Layout triggers :

- Element
	* clientHeight
	* clientLeft
	* clientTop
	* clientWidth
	* focus()
	* getBoundingClientRect()
	* getClientRects()
	* innerText
	* offsetHeight
	* offsetLeft
	* offsetParent
	* offsetTop
	* offsetWidth
	* outerText
	* scrollByLines()
	* scrollByPages()
	* scrollHeight
	* scrollIntoView()
	* scrollIntoViewIfNeeded()
	* scrollLeft
	* scrollTop
	* scrollWidth
- Frame, Image
	* height
	* width
- Range
	* getBoundingClientRect()
	* getClientRects()
- SVGLocatable
	* computeCTM()
	* getBBox()
- SVGTextContent
	* getCharNumAtPosition()
	* getComputedTextLength()
	* getEndPositionOfChar()
	* getExtentOfChar()
	* getNumberOfChars()
	* getRotationOfChar()
	* getStartPositionOfChar()
	* getSubStringLength()
	* selectSubString()
- SVGUse
	* instanceRoot
- window
	* getComputedStyle()
	* scrollBy()
	* scrollTo()
	* scrollX
	* scrollY
	* webkitConvertPointFromNodeToPage()
	* webkitConvertPointFromPageToNode()
- ...

See [relayout, repaint, reflow](CSS#relayout-repaint-reflow)

- [DIY Web Animations: Promises + rAF + Transitions — surma.dev](https://web.archive.org/web/20210110231841/https://surma.dev/things/raf-promise/)
- [What forces layout/reflow. The comprehensive list.](https://gist.github.com/paulirish/5d52fb081b3570c81e3a)
- [Fastersite: How (not) to trigger a layout in WebKit](http://gent.ilcore.com/2011/03/how-not-to-trigger-layout-in-webkit.html)
- [Rendering: repaint, reflow/relayout, restyle / Stoyan's phpied.com](http://www.phpied.com/rendering-repaint-reflowrelayout-restyle/)
- [Improving the Performance of your HTML5 App - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/speed/html5/)
- [Minimizing browser reflow  |  PageSpeed Insights  |  Google Developers](https://developers.google.com/speed/articles/reflow)
- [What Every Frontend Developer Should Know About Webpage Rendering — Frontend Babel](http://frontendbabel.info/articles/webpage-rendering-101/)
- [Guillermo Rauch on Twitter: "The DOM is not slow, Layout is slow"](https://twitter.com/rauchg/status/735880942791757824) and [Sometime I want to do a big, detailed blog post full of supporting data on this ... | Hacker News](https://news.ycombinator.com/item?id=9155614)
- [Reflows & Repaints: CSS Performance making your JavaScript slow? | Stubbornella](http://www.stubbornella.org/content/2009/03/27/reflows-repaints-css-performance-making-your-javascript-slow/)
- [Dev.Opera — Efficient JavaScript](https://dev.opera.com/articles/efficient-javascript/?page=3#reflow)
- [Notes on HTML Reflow](http://www-archive.mozilla.org/newlayout/doc/reflow.html)
- [Performance best practices for Firefox front-end engineers - Mozilla | MDN](https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Performance_best_practices_for_Firefox_fe_engineers#Detecting_and_avoiding_synchronous_style_flushes) - Detecting and avoiding synchronous style flushes
- [Performance best practices for Firefox front-end engineers - Mozilla | MDN](https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Performance_best_practices_for_Firefox_fe_engineers#How_do_I_avoid_triggering_uninterruptible_reflow) - How do I avoid triggering uninterruptible reflow
- [Avoid Large, Complex Layouts and Layout Thrashing  |  Web Fundamentals  |  Google Developers](https://developers.google.com/web/fundamentals/performance/rendering/avoid-large-complex-layouts-and-layout-thrashing)

## Check the visibility of an element

`element.getBoundingClientRect()` return `0,0,0,0` for not displayed elements

`element.offsetHeight == 0` means the element is not displayed but not work if element without padding nor border contains no element (or out of flow elements). Plus that trigger a reflow

`element.offsetParent !== null` return `null` when element is not displayed (!= not visible or transparent). But... [javascript - What would make offsetParent null? - Stack Overflow](https://stackoverflow.com/questions/306305/what-would-make-offsetparent-null) [HTMLElement.offsetParent - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetParent)

[Determine if an Element is Visible](https://davidwalsh.name/offsetheight-visibility)

Use same rules as CSS for detection `element.match()`, `window.matchMedia`

You can use intersection observers' root option to find out when an element appears/disappears:

```js
const box = document.querySelector('.box');

new IntersectionObserver(([entry]) => {
	if (entry.intersectionRatio) {
		console.log('Box rendered!');
	}
	else {
		console.log('Box unrendered!');
	}
}, {
	root: document.body
}).observe(box);
```

- [JS Bin - Collaborative JavaScript Debugging](https://jsbin.com/fonuma/edit?css,js,console,output)
- [Jake Archibald on Twitter: "TIL: You can use intersection observers' root option to find out when an element appears/disappears. Demo: https://t.co/s8DP2m1iHZ https://t.co/hxfDls1SLM"](https://twitter.com/jaffathecake/status/857537625154097152)

## Restart CSS animation/transition

Trigger a [reflow](#relayout-repaint-reflow). Or set `animation` to `none` then after an immediate timeout (delay=0), reset `animation` to its original value.

## Get data from stylesheet

Use CSS variable. You should escape with backslash `;`, `{`, `}` and `!`. "Comments" before semilicon are also included.

```html
<style>
:root{
	--data: abc\;\}\{def \!important /* included */;/* excluded */
}
</style>
<script>
window.getComputedStyle(document.documentElement).getPropertyValue("--data").trim() == "abc\\;\\}\\{def \\!important /* included */"
//getPropertyCSSValue("--data").primitiveType == CSSPrimitiveValue.CSS_STRING
</script>
```

## Detect if navigation is canceled

After the user click on a link:

```js
const beforeUnload = event => {
	window.removeEventListener("beforeunload", beforeUnload);
	// If the event has been prevented (by other any script)
	if(event.defaultPrevented){
		return;
	}
	clearTimeout(timeout);
};
const timeout = () => {
	// navigation has been cancel
	const blob = new Blob([value], {type: "text/html;charset=utf-8"});
	// use blob instead of doc.open() write() close() which works only for HTML doc, not for XML (SVG) docs
	window.location = URL.createObjectURL(blob);
};

// listen unload event to wait a potential navigation event
window.addEventListener("beforeunload", beforeUnload);
// and set timeout to 100ms as fallback
// 100ms is enough to be sure the navigation event is triggered before
const unloadTimeoutID = setTimeout(timeout, 100);
```

## Document ready

```js
let domContentLoaded = new Promise(resolve => {
	if(document.readyState === "interactive" || document.readyState === "complete"){
		resolve(true);
		return;
	}
	document.addEventListener("DOMContentLoaded", event => {
		resolve(true);
	});
})
```

```js
// If DOMContentLoaded is already dispatched (or will be)
if(document.readyState == "interactive" && document.body || document.readyState == "complete"){
	main();
}else{
	document.addEventListener("DOMContentLoaded", event => main());
}
```

```js
if(document.readyState == "uninitialized" || document.readyState == "loading"){
	document.addEventListener("DOMContentLoaded", event => main());
}else{
	main();
}
```

- https://stackoverflow.com/questions/9457891/how-to-detect-if-domcontentloaded-was-fired
- [Mozilla's dev answer about `DOMContentLoaded` is the event when `document.readyState === "interactive"` (but after defered scripts)](https://stackoverflow.com/questions/3665561/document-readystate-of-interactive-vs-ondomcontentloaded/9973472#9973472)
- https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded
- https://code.google.com/p/dart/source/detail?r=5984

## Load external script

Use `<script src="https://connect.facebook.net/en_US/sdk.js#xfbml=1" async></script>`

- [Script-injected "async scripts" considered harmful - igvita.com](https://www.igvita.com/2014/05/20/script-injected-async-scripts-considered-harmful/)
- [Performance Calendar » Prefer DEFER Over ASYNC](http://calendar.perfplanet.com/2016/prefer-defer-over-async/)

Script-created scripts are by default async. (but not with `document.write()`)

```js
const script = document.createElement("script");
script.src = "https://connect.facebook.net/en_US/sdk.js#xfbml=1";
document.head.appendChild(script);
```

- [<script> - HTML (HyperText Markup Language) | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#Async_support)
- [javascript - Is the "async" attribute/property useful if a script is dynamically added to the DOM? - Stack Overflow](https://stackoverflow.com/questions/3408805/is-the-async-attribute-property-useful-if-a-script-is-dynamically-added-to-the/5160676#5160676)
- [The non-blocking script loader pattern](http://www.lognormal.com/blog/2012/12/12/the-script-loader-pattern/)

See:

- [Don't use `document.write()`](#dont-use-documentwrite)`)
- [Blocking resources](Web.md#blocking-resources)

## Animation

Animation should be based on **elapsed time**, not on iterations (`requestAnimationFrame`, `setInterval` or `setTimeout`), else if the framerate is low, the movement will be slower than 60fps

Round iteration base animation:

```js
var x = currentX + (targetX - currentX) * 0.1
// Round below 0.1
if(Math.abs(x - currentX) < 0.1){
	x = targetX;
}
```

If use transform, use `translate3d(X, Y, Z)` even if use want to use only one axis (with `translate(X, Y)`, `translateX(X)`, etc.), it will not benefit of hardware acceleration on some browser (Safari, for others like FF or Chrome it's OK)

- [javascript - How can I make setInterval also work when a tab is inactive in Chrome? - Stack Overflow](https://stackoverflow.com/questions/5927284/how-can-i-make-setinterval-also-work-when-a-tab-is-inactive-in-chrome)
- [Chrome and Firefox throttle setTimeout/setInterval in inactive tabs](https://content.pivotal.io/blog/chrome-and-firefox-throttle-settimeout-setinterval-in-inactive-tabs)

FLIP (First, Last, Invert, Play):

```js
// Get the first position.
var first = el.getBoundingClientRect();
// Now set the element to the last position.
el.classList.add('totes-at-the-end');
// Read again. This forces a sync layout, so be careful.
var last = el.getBoundingClientRect();
// You can do this for other computed styles as well, if needed.
// Just be sure to stick to compositor-only props like transform
// and opacity where possible.
var invert = first.top - last.top;
// Invert.
el.style.transform = 'translateY(' + invert + 'px)';
// Wait for the next frame so we know all the style changes have taken hold.
requestAnimationFrame(function() {
  // Switch on animations.
  el.classList.add('animate-on-transforms');
  // GO GO GOOOOOO!
  el.style.transform = '';
});
// Capture the end with transitionend
el.addEventListener('transitionend', tidyUpAnimations);
```

- [Aerotwist - FLIP Your Animations](https://aerotwist.com/blog/flip-your-animations/)
- [Animating Layouts with the FLIP Technique | CSS-Tricks](https://css-tricks.com/animating-layouts-with-the-flip-technique/)

See also [Animation](CSS#animation), [Debounce function](#debounce-function)

- [GianlucaGuarini/animore: 1kb script that will make your DOM state transitions smoother & easier](https://github.com/GianlucaGuarini/animore)
- [DasSur.ma – 2018: 120fps and no jank](https://dassur.ma/things/120fps/)
- https://output.jsbin.com/fatubik/3

Tools

- [NanoFL vector and animation editor](http://nanofl.com/)
- [bodymovin - after effects to html library](https://github.com/bodymovin/bodymovin) - After Effects plugin for exporting animations to svg/canvas/html + js

### Animation API

- [Intro to the Web Animations API](https://pawelgrzybek.com/intro-to-the-web-animations-api/)

## Viewport dimension

See [Viewport](CSS#viewport)

Aka window dimension, viewport size, window size

```js
// visual viewport (w/ zoom) relative to document, w/ scrollbars:
window.innerWidth;
window.innerHeight;
// layout viewport (w/o zoom), document dimension, w/o scrollbars:
document.documentElement.clientWidth;
document.documentElement.clientHeight;
document.body.clientWidth;
document.body.clientHeight;
// element:
element.clientWidth;
element.clientHeight;
```

But... (zoom, support of old browsers)

- [A tale of two viewports — part one](http://www.quirksmode.org/mobile/viewports.html) and [A tale of two viewports — part two](http://www.quirksmode.org/mobile/viewports2.html)
- http://ryanve.com/lab/dimensions/
- https://stackoverflow.com/questions/1248081/get-the-browser-viewport-dimensions-with-javascript/8876069#8876069
- [javascript - How to get the window size of the fullscreen (minimal-ui) view when not in fullscreen? - Stack Overflow](https://stackoverflow.com/questions/26801943/how-to-get-the-window-size-of-the-fullscreen-minimal-ui-view-when-not-in-fulls)
- [gajus/scream](https://github.com/gajus/scream)

And without scrollbars: https://bugzilla.mozilla.org/show_bug.cgi?id=189112#c7

And prefer use `element.getBoundingClientRect()` to know position of an element related to the viewport
Because `offset[Left|Top]` is not available on SVG nodes and don't take account of scroll positions (viewport and all others scrollable elements): need offsetTop + scrollTop of each offsetParents and no CSS transforms used (parse CSS is required)

## Document dimension

```js
document.documentElement.offsetWidth
document.documentElement.offsetHeight
```

## Element dimension and position

- `clientHeight` (HTML element only) (rounded) includes the height and vertical padding.
- `offsetHeight` (HTML element only) (rounded) includes the height, vertical padding, and vertical borders.
- `scrollHeight` (HTML element only) (rounded) includes the height of the contained document (would be greater than just height in case of scrolling), vertical padding, and vertical borders.
- `getBBox()` (SVG element only) equivalent to offset/clientwidth, doesn't take the transformations into consideration
- `getClientRect()` and `getBoundingClientRect()` transform

- [Determining the dimensions of elements - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Determining_the_dimensions_of_elements)

## Interactions and animations

```js
window.addEventListener("scroll", function() {
	const speed = 5.0;
	document.body.style.backgroundPosition = (-window.pageXOffset/speed)+"px "+(-window.pageYOffset/speed)+"px";
})
```

- [Keyboard Event Viewer](https://w3c.github.io/uievents/tools/key-event-viewer.html)

See also:

- Use CSS instead of JS: [Parallax effect](CSS#parallax-effect)
- [scroll](#scroll)
- Scroll with momentum / kinetic scrolling: [JavaScript Kinetic Scrolling: Part 2](http://ariya.ofilabs.com/2013/11/javascript-kinetic-scrolling-part-2.html)
- Horizontal swipe + parallax effect: [JavaScript Kinetic Scrolling: Part 4](http://ariya.ofilabs.com/2013/12/javascript-kinetic-scrolling-part-4.html)
- Cover Flow: [JavaScript Kinetic Scrolling: Part 5 (Cover Flow Effect)](http://ariya.ofilabs.com/2014/01/javascript-kinetic-scrolling-part-5-cover-flow-effect.html)
- [kinetic](http://ariya.ofilabs.com/tag/kinetic)
- [Cheapass Parallax - daverupert.com](https://daverupert.com/2018/02/cheapass-parallax/)

### Detect touch device

See [detect touch device](CSS#detect-touch-device)

> We found that some sites are assuming that “if this web browser supports touch events, then it shouldn’t support mouse events at the same time.” e.g. Apple.com and Wells Fargo.
>
> — SeoJin Kim, Principal Engineer for Samsung Internet

Do you mean: Is it an hover media? or: What is precision of the pointer? (none, coarse, fine)

It's complexe and yet inaccurate.

```js
// if the mediaquery is supported (media="not all" if not supported)
// See https://github.com/Modernizr/Modernizr/blob/master/feature-detects/touchevents.js
// true = at least one media query match (others are not supported or doesn't match)
// false = at least one media query is supported, but none of supported media query match
// null = none of media queries are supported
const isTouchMediaMatches = [
  '(pointer: coarse)',
  '(hover: none)',
  '(-moz-touch-enabled)',
].reduce((result, query) => {
  const {media, matches} = matchMedia(query);

  // This media query is not supported
  if(media === "not all"){
    return result;
  }

  return result || matches;
}, null);
// fallback to API detection for browsers that dont support used mediaqueries
const isTouchWithFallback = isTouchMediaMatches !== null ? isTouchMediaMatches : ('ontouchstart' in window) || window.TouchEvent || window.DocumentTouch && document instanceof DocumentTouch;

// is primary pointer have limited accuracy or the primary input mechanism can hover
// see also isMobile
export const isTouch = isTouchWithFallback;
```

```js
// Test if the browser support of `touch*` events (but there no guarantee it's a touch device)
"ontouchstart" in window;
//"onpointerdown" in document
// Test if the browser support mutli touch points (== 0 if no touch)
Boolean(navigator.msMaxTouchPoints) || Boolean(navigator.maxTouchPoints);
// Test if via media queries level 4, don't support hover nor have fine pointer
var mqList;
window.matchMedia && (mqList = window.matchMedia('(pointer: coarse), (hover: none)')) && (mqList.media == "not all"/*if `hover` MQ not supported*/ || mqList.matches/*supported and match*/);
<UIEvent>.sourceCapabilities.firesTouchEvents// non standard
```

```js
// https://github.com/GoogleChrome/lighthouse/blob/ecbbc388f87d515224484a4b978552d10d552445/lighthouse-core/lib/emulation.js#L79-L102
function injectedTouchEvents() {
    const touchEvents = ['ontouchstart', 'ontouchend', 'ontouchmove', 'ontouchcancel'];
    const recepients = [window.__proto__, document.__proto__];
    for (let i = 0; i < touchEvents.length; ++i) {
      for (let j = 0; j < recepients.length; ++j) {
        if (!(touchEvents[i] in recepients[j])) {
          Object.defineProperty(recepients[j], touchEvents[i], {
            value: null, writable: true, configurable: true, enumerable: true,
          });
        }
      }
    }
}
```

- [Touch Devices Should Not Be Judged By Their Size | CSS-Tricks](https://css-tricks.com/touch-devices-not-judged-size/)
- [Modernizr/touchevents.js at master · Modernizr/Modernizr](https://github.com/Modernizr/Modernizr/blob/master/feature-detects/touchevents.js)
- [You Can't Detect A Touchscreen | Blog | Stu Cox](http://www.stucox.com/blog/you-cant-detect-a-touchscreen/)
- [jquery - Detecting touch screen devices with Javascript - Stack Overflow](https://stackoverflow.com/questions/3974827/detecting-touch-screen-devices-with-javascript)
- [jquery - What's the best way to detect a 'touch screen' device using JavaScript? - Stack Overflow](https://stackoverflow.com/questions/4817029/whats-the-best-way-to-detect-a-touch-screen-device-using-javascript)
- https://github.com/qqTYXn7/browserprint/blob/54e1b15262e7f6202a99d737fb0069c1d46aa0b2/WebContent/scripts/fjs2.js#L193-L215 - Script that try to detect touch device
- [Modernizr.touch detects touch events not touch devices · Issue #548 · Modernizr/Modernizr](https://github.com/Modernizr/Modernizr/issues/548)
- [Detecting touch: it's the 'why', not the 'how' ★ Mozilla Hacks – the Web developer blog](https://hacks.mozilla.org/2013/04/detecting-touch-its-the-why-not-the-how/)

### `input` event

The `input` event The `beforeinput` and `input` events are [defined in UI Events](https://w3c.github.io/uievents/#events-inputevents), and [extended in Input Events](https://www.w3.org/TR/input-events-2/). The `beforeinput` event has only recently been implemented in [Blink](https://www.chromestatus.com/feature/5656380006465536) and [WebKit](https://webkit.org/blog/7358/enhanced-editing-with-input-events/), but the `input` event is already [widely supported](https://caniuse.com/#feat=input-event), and can be used to detect when the user changes the value of an `<input type="text">` or `<textarea>` element.

A few notes about this event:

- The `input` event is not specific to keyboard actions, and can be used to detect user input regardless of the original source. The event fires once per keystroke (between `keypress` and `keyup`), roughly once per word during voice input (“speech to text” button on virtual keyboards), and once after a cut, paste, and drag and drop action.
- A keystroke results in an `input` event only if the field’s value has changed. Hence, <kbd>Enter</kbd> triggers the event in `<textarea>` elements but not in `<input type="text">` elements, <kbd>Backspace</kbd> and <kbd>Delete</kbd> trigger the event only if a character was deleted (so not when, for instance, the field is empty), while some keys such as <kbd>Shift</kbd> and the arrow keys, don’t trigger the event at all.
- Some browsers (e.g. Chrome for Android) dispatch `keydown` and `keyup` events alongside the `input` event during voice input.

### Always listen `touchend`/`pointerup` **and** `touchcancel`/`pointercancel`

> …whenever a default action like scroll or zoom is triggered, you’ll get a `pointercancel` event, to let you know that the browser has taken control of the pointer. […] You can stop the browser from taking control with the CSS `touch-action` property.
>
> — [Pointing the Way Forward  |  Web  |  Google Developers](https://developers.google.com/web/updates/2016/10/pointer-events)

"If you listen to touchend events, be sure to also listen for touchcancel":

> The touchend event fires whenever a finger lifts normally from the touchscreen.  All browsers can also fire a touchcancel event (http://www.w3.org/TR/touch-events/#the-touchcancel-event) to indicate that a touch has terminated abnormally.  This can happen, for example, if focus is taken away from the page (such as by the browser's menu being activated), or for any number of other implementation-defined reasons.  The reason this is a separate event is that you may want to avoid triggering some action (eg. a tap that ends with a touchend should activate something, but one that ends in touchcancel should not).
>
> I've seen many websites which listen for touchend but ignore touchcancel entirely.  This results in some subtle but nasty bugs.  For example, the app may think that a finger is stuck down when there are no fingers on the page at all.  When a new touchstart occurs, the app may get very confused - possibly thinking two fingers are now down.
>
> This is particularly problematic for Chrome.  Chrome sends a touchcancel event whenever scrolling starts (i.e. whenever there has been enough movement without the app calling preventDefault on any of the touchmove events) [edit: this is no longer true - see http://updates.html5rocks.com/2014/05/A-More-Compatible-Smoother-Touch].  Chrome does this in order to maximize performance of scrolling.  Scrolling normally occurs on a separate thread (from the main thread which runs JavaScript) in order to allow scrolling to proceed smoothly.  But if we were to send touchmove events throughout the scroll then we'd probably have to block on the main thread for every scroll update, making it potentially janky.  Besides, we've found that the majority of sites that handle touchmove events during scroll are doing it by accident (eg. they've forgotten to call preventDefault, or they care only about taps not dragging gestures).  If the app is also manipulating the DOM in these handlers then the problem can be even worse (in the worst case, forcing a layout on every scroll update) - resulting in scrolling that is unbearably janky.
>
> Chrome for Android has always had this optimization, and now in M32 Chrome desktop is changing (http://crbug.com/240735) to match the Android behavior.  You can see this in action here: http://www.rbyers.net/janky-touch-scroll.html.  Enable the "do lots of work" and "empty touchmove handler" checkboxes.  Scrolling will take a little while to start (to verify the page doesn't want to prevent scrolling entirely), but once it starts it will proceed smoothly on browsers that have this touchcancel behavior (or other such optimizations).  For bonus points, scroll down and try the same thing with the scrollable element.  In Chrome we work hard to try to make scrolling of elements behave the same as document scrolling, but there are some (shrinking) scenarios where this isn't yet possible (and so it will be janky when scrolling the document is smooth).
>
> The precise behavior here is painfully specific to each browser.  I've put some details here: https://docs.google.com/a/chromium.org/document/d/12k_LL_Ot9GjF8zGWP9eI_3IMbSizD72susba0frg44Y/edit#heading=h.nxfgrfmqhzn7.  At least this is very well specified in Pointer Events (http://www.w3.org/TR/pointerevents/), and Chrome's behavior is equivalent to the Pointer Event behavior.  We're talking at the W3C at trying to improve consistency between browsers for this touch event case (see http://lists.w3.org/Archives/Public/public-webevents/2013AprJun/0040.html).
>
> — [If you listen to touchend events, be sure to also listen for touchcancel The…](https://plus.google.com/+RickByers/posts/Ny6ZXuzWdN5)

- [pointercancel - Event reference | MDN](https://developer.mozilla.org/en-US/docs/Web/Events/pointercancel)

### Lock drag to scroll in one direction (vertical | horizontal)

Allow 2 axis scroll degree free, but once the user start to scroll in one direction (s)he can't scroll in same time over the other axis

Example with iOS's Springboard (home):

- horizontal: scroll between screens
- vertical (to bottom): display Spotlight input field

When scroll outside bounds (spring effect), use diffWithBound / 2

```js
var touchDirectionLock;
var touchStartX;
var touchStartY;
element.addEventListener("touchstart", touchStart);

function touchStart(event){
	touchDirectionLock = null;//Reset
	var firstTouch = event.touches[0];
	touchStartX = firstTouch.clientX;
	touchStartY = firstTouch.clientY;

	window.addEventListener("touchmove", touchMove);
	window.addEventListener("touchend", touchEnd);
	window.addEventListener("touchcancel", touchEnd);
}
function touchMove(event){
	var firstTouch = event.touches[0];
	var diffX = firstTouch.clientX - touchStartX;
	var diffY = firstTouch.clientY - touchStartY;
	var distance = Math.sqrt(diffX * diffX + diffY * diffY);//absolute distance from touchStartX and Y

	// If the lock direction not defined yet and touch moves enough to determine it
	// Require at least 20px distance
	if(touchDirectionLock === null && distance >= 20){
		touchDirectionLock = Math.abs(diffX) < Math.abs(diffY) ? "vertical" : "horizontal";
		// reset touchStartX|Y to current pos.
		touchStartX = firstTouch.clientX;
		touchStartY = firstTouch.clientY;
	}

	// No direction lock determined yet
	if(touchDirectionLock === null){
		console.log("Touch direction lock not determined yet");
		return;
	}

	// Prevent event default's action here (eg. scroll by touch drag)
	console.log("Touch direction lock", touchDirectionLock);
}
function touchEnd(event){
	if(touchDirectionLock === null){
		console.log("Can't determine touch direction lock");
		return;
	}

	console.log("Touch direction lock", touchDirectionLock);
}
```

### Mouse and touch drag and drop

Drag and drop an interactive element, start drag & stop drag

	add listeners on target element: mousedown->pointerDown and touchstart->pointerDown

	pointerDown:
		// note: will be called by events from element: mousedown and touchstart
		// filter to handle only event.button === 0 (match left button or right button on left handed mouse)
		// add listeners on document: mousemove->dragMove, touchmove->dragMove, mouseup->pointerUp, touchend->pointerUp and touchcancel->pointerUp
		// store event.clientX|Y or event.offsetX|Y if drag relative to the element

	pointerMove:
		// note: will be called by events from document/window: mousemove and touchmove
		// move your draggable element, etc. ex.: apply offset between last stored value and the new value (new - prev)
		// store event.clientX|Y or event.offsetX|Y

	pointerUp:
		// note: will be called by events from document/window: mouseup, touchend and touchcancel
		// remove listeners on document: pointerMove and pointerUp
		// note: you can use event.preventDefault() but will dispatch mouseevent on touch devices

		// ease to final position using lastPointerVelocity * 300, where (in pointerMove) lastPointerVelocity = (clientX - lastPointerX|Y) / (now - lastPointerTime)

Note: listen mousemove, touchmove, mouseup, touchend, touchcancel on document or window makes no differences. Because it bubbling events.

```js
//pointerDown:
let firstPointer = event.touches ? event.touches[0] : event;
pointerMoved = 0;// cumulative distance in px of pointer moved between down and up
lastPointerPosX = firstPointer.clientX;
lastPointerPosY = firstPointer.clientY;

//pointerMove:
let firstPointer = event.touches ? event.touches[0] : event;
pointerMoved += Math.sqrt(Math.pow(firstPointer.clientX - lastPointerPosX, 2) + Math.pow(firstPointer.clientY - lastPointerPosY, 2));

//pointerUp:
// DRAG_DISTANCE_MIN ~= 10
if(pointerMoved > DRAG_DISTANCE_MIN){
	// the user drag
}else{
	// the user click
}
```

To prevent content selection and scrolling:

TL;DR: prevent default of in combination with `selectstart` and `dragstart` (with listeners added in _pointerDown_ and removed in _pointerUp_) + set `-moz-user-select: none` (or `style.MozUserSelect = "none"`, in _pointerDown_ + remove/revert in _pointerUp_) because Firefox don't `selectstart`

- add listeners in _pointerDown_ (and remove it in _pointerUp_) on element for `selectstart` event (for text) and `dragstart` event (for images) then cancel the default action: `event.preventDefault()`. But Firefox don't support `selectstart`
- in pointerDown (revert it in _pointerUp_) enable a class/set style `user-select: none` for text and add `draggable="false"` to all images (or `pointer-events: none`?)
- call `window.getSelection().removeAllRanges()` in _pointerMove_ (Not sure that works on imgs too)
- cancel default action in _pointerDown_: `event.preventDefault()` but some event append outside the viewport are not dispatched (some browsers Firefox, Chrome: iframe)
- cancel default action in _pointerMove_: `event.preventDefault()` but works only for some browsers (Chrome, not Firefox)

See also `touch-action: none;`

To prevent click event when _pointerUp_:

cancel default action in _pointerDown_, but break outside the viewport events (see above)

or

1. Listen the `click` event in _pointerUp_ with `useCapture=true` (you can add a condition: only if pointer has moved)
2. In click listener cancel the event then remove click event listener (with `useCapture=true`)

### Drag and drop item

Use `event.dataTransfer.items` instead of `event.dataTransfer.files` or `event.dataTransfer.getData()`: [javascript - event.dataTransfer.files vs. event.dataTransfer.items - Stack Overflow](https://stackoverflow.com/questions/44842247/event-datatransfer-files-vs-event-datatransfer-items)

Drag image should be visible (on Chrome). Create a top level clone with a negative z-index (require an opaque body's background)?

- [File drag and drop - Web API | MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API/File_drag_and_drop)
- [Drag Operations - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API/Drag_operations)
- [HTML Drag and Drop API - Web API | MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API)
- [Drag Operation - Web API | MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API/Drag_operations#droptargets)
- http://www.kryogenix.org/code/browser/custom-drag-image.html

### Double click/tap

```js
var time = Number.NEGATIVE_INFINITY;
function click(event){
	//TODO test if there no touchmove for touches (for tap, similar to click)
	//TODO a click can be dispatched after touch. touchend+event.preventDefault() can resolve that?
	var now = Date.now();
	// between 500ms
	if(now - time >= 500){
		return;
	}
	time = now;

	//Double Click/Touch!
}

document.addEventListener("click", click);
document.addEventListener("touchend", click);
```

- [doubletap event for jquery](https://gist.github.com/asgeo1/1652946)
- [Handling Events](https://developer.apple.com/library/mac/documentation/AppleApplications/Reference/SafariWebContent/HandlingEvents/HandlingEvents.html#//apple_ref/doc/uid/TP40006511-SW12)

### Mouseup+mousedown on a translating element don't dispatch click event

Because your element contains sub-elements. Since translating is like moving the pointer, mousedown and mouseup occur on different elements (`event.target`).
Could happend when there is an css transform transition at hover state of the element.

To prevent that, use `pointer-events: none;` on sub elements or listen `mouseup` instead of `click`.

- [css - Browser sometimes ignores a jQuery click event during a CSS3 transform - Stack Overflow](https://stackoverflow.com/questions/15786891/browser-sometimes-ignores-a-jquery-click-event-during-a-css3-transform)

### Click only with left button

No more right click or middle click. Only the left click (or right button of left-handed mouses).

```js
element.addEventListener("click", linkClick.bind(this), false);

function _linkClick(event){
	// Only left button
	if(event.button != 0/*event.buttons != 1*/){
		return;
	}

	// Do stuff
}
```

See also:

- https://stackoverflow.com/questions/3944122/detect-left-mouse-button-press/12737882#12737882
- https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent.button
- https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent.buttons
- https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent.which
- https://developer.mozilla.org/en-US/docs/Web/API/event.button
- http://www.quirksmode.org/js/events_properties.html#button

### Pointer position

- `clientX`, `clientY`: Mouse position relative to the browser's visual viewport.
- `screenX`, `screenY`: Mouse position relative to the user's physical screen.
- `offsetX`, `offsetY`: Mouse position relative to the target element.
- `pageX`, `pageY`: Mouse position relative to the html document (ie. layout viewport).

```js
const isTouch = "touches" in event;
const clientX = isTouch ? event.touches[0].clientX : event.clientX;
```

To compute `offsetX|Y` use: `event(.touches[0]).clientX|Y - .getBoundingClientRect().left|right`, be carefull this add the border width (`offsetX|Y` should be relative to the padding-box)

- [Cross-browser mouse positioning](http://www.jacklmoore.com/notes/mouse-position/)

### Pinch (for zoom/dezoom)

1. start: store as _start distance_ the distance between points (`event.touches[0]` and `event.touches[1]`)
2. move: diff _current distance_ and _start distance_

```js
export default function getPointerEventsDistance(point1, point2){
	return Math.sqrt(
		Math.pow(point1.clientX - point2.clientX, 2) + Math.pow(point1.clientY - point2.clientY, 2)
	);
}
```

### Mouse wheel

Use `wheel` event, not any other. If possible use it as a passive event (don't need `event.preventDefault()`): `element.addEventListener("wheel", handler, {passive:true});`

iframe trap `wheel` events, only scroll if `wheel` event is not catched by iframe content will automatically scroll parent content (when edges are reached)

- https://github.com/jquery/jquery-mousewheel

### Device orientation and screen orientation

Device orientation is absolute orientation, without any screen orientation consideration.

Get value: `screen.orientation.angle`, `screen.mozOrientation.angle`, `screen.msOrientation.angle`, `window.orientation` (depreciated)
Listen event: `window.screen.orientation.addEventListener("change", ...)`, `window.screen.addEventListener("orientationchange", ...)` (not standard), `window.addEventListener("orientationchange", ...)` (depreciated)

```js
// <div id="test" style="background: red; width: 100px; height: 100px; margin: -50px; position: fixed; top: 50%; left: 50%;"></div>
window.addEventListener("deviceorientation", function(event){
	let orientation = window.screen.orientation.angle;
	// Fix gamma and beta with screen orientation
	let relativeGamma = event.gamma * Math.cos(orientation * Math.PI / 180) + event.beta * Math.sin(orientation * Math.PI / 180);
	let relativeBeta = event.beta * Math.cos(orientation * Math.PI / 180) + event.gamma * Math.sin(-orientation * Math.PI / 180);
	test.style.transform = `translate(${relativeGamma*10}px, ${relativeBeta*10}px)`;
}, false);
```

Test it and rotate the screen (on mobile devices for example)

- [Dev.Opera — Practical Application and Usage of the W3C Device Orientation API](https://dev.opera.com/articles/w3c-device-orientation-usage/)
- [motion vs orientation](http://ariya.ofilabs.com/2010/12/motion-vs-orientation.html)
- [Standalone device orientation + motion detection, normalization and conversion library](https://github.com/adtile/Full-Tilt)
- [Orientation and motion data explained - Web developer guides | MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Orientation_and_motion_data_explained)

In ThreeJS has [`DeviceOrientationControls`](https://github.com/mrdoob/three.js/blob/dev/examples/js/controls/DeviceOrientationControls.js) for that.

Other examples: https://github.com/adtile/Full-Tilt/blob/master/examples/vr_test.html https://github.com/richtr/threeVR/blob/master/examples/vr_basic.html

To add offset (like drag and drop with touch): [javascript - Add offset to DeviceOrientationControls in three.js - Stack Overflow](https://stackoverflow.com/questions/36314415/add-offset-to-deviceorientationcontrols-in-three-js)

See [3D orientation](Math#3d-orientation):

- [deviceorientation - quaternion & rotation matrix manipulation - w/ three.js](http://rawgit.com/richtr/threeVR/master/examples/vr_basic.html)
- [FULLTILT DeviceOrientation three.js test page](http://rawgit.com/adtile/Full-Tilt/master/examples/vr_test.html)

### Page transition

As onepage (fetch/XHR + History API) or with multipages with [iframe trick](#parse-streamed-html) or with `document.open()`. The only one issue is with living timers and listeners added to the previous page.

- [Improving User Flow Through Page Transitions – Smashing Magazine](https://www.smashingmagazine.com/2016/07/improving-user-flow-through-page-transitions/)

### Disabled field events

- [Events and disabled form fields - JakeArchibald.com](https://jakearchibald.com/2017/events-and-disabled-form-fields/)

## Scroll

> Overriding the browser’s default scrolling behavior introduces a whole lot of complexity, and that has implications.

And it's not 100% forward compatible. Native user experience can or native UI change, a new browser version can be broken with this script

- [Scroll to](#scroll-to)
- [UI - UX#Scroll]()
- [Scroll-linked effects - Mozilla | MDN](https://developer.mozilla.org/en-US/docs/Mozilla/Performance/Scroll-linked_effects)
- [Asynchronous scrolling in Firefox - staktrace.com](https://staktrace.com/spout/entry.php?id=834)
- [Six things I learnt about iOS Safari's rubber band scrolling](http://blog.christoffer.me/six-things-i-learnt-about-ios-safaris-rubber-band-scrolling/)
- [Scrolling on the web: A primer - Microsoft Edge Dev BlogMicrosoft Edge Dev Blog](https://blogs.windows.com/msedgedev/2017/03/08/scrolling-on-the-web/)

- [Scroll indicator](CSS#scroll-indicator)

**ALWAYS USE ROUNDED VALUES**: `window.scroll[X|Y]`, `element.scroll[Left|Top]` are rounded!

### Smooth scroll

CSS `scroll-behavior: smooth;`

- Element
	* scrollByLines()
	* scrollByPages()
	* scrollHeight
	* scrollIntoView() `element.scrollIntoView({behavior: "smooth"})`
	* scrollIntoViewIfNeeded()
	* scrollLeft
	* scrollTop
	* scrollWidth
- window
	* scrollBy() `window.scrollBy({behavior: "smooth"})`
	* scrollTo() `window.scrollTo({behavior: "smooth"})`
	* scrollX
	* scrollY

smooth behavior support: `"scrollBehavior" in document.documentElement.style`

Use `transform` to update postion of section with easing

Smooth scroll impl

- [smooth scroll polyfill](http://iamdustan.com/smoothscroll/) and [Smooth Scroll behavior polyfill](https://github.com/iamdustan/smoothscroll)
- [mozdev.org - smoothwheel: index](http://smoothwheel.mozdev.org/)
- [1010538 – Implement CSSOM-View scroll-behavior CSS property](https://bugzilla.mozilla.org/show_bug.cgi?id=1010538)
- [How to Implement Smooth Scrolling in Vanilla JavaScript](http://www.sitepoint.com/smooth-scrolling-vanilla-javascript/)
- [Smooth Scrolling | CSS-Tricks](https://css-tricks.com/snippets/jquery/smooth-scrolling/)

### Sticky

- [Auto-Hiding Navigation in CSS and jQuery | CodyHouse](https://codyhouse.co/gem/auto-hiding-navigation/)

### Autoscroll to anchors

Potential solutions:

- Use History API (`[push|replace]State()`)
- Rename all affected ID (do it first with JS, and handle hash change or clicks)
- (not work propely) remove ID of affected element, change hash the restore ID
- use position fixed
- use `History.scrollRestoration = "manual"` https://developer.mozilla.org/en-US/docs/Web/API/History/scrollRestoration

Behaviors:

- autoscroll to the anchor when a hash match it (via link click or location.hash update)
- autoscroll to the anchor despite it's ID/name changed for history back/forward. For Chrome, IE and Firefox
- IE scroll to anchor async (define location.hash don't jump directly)

- [Anchor hash tag behaviour](Web#anchor-hash-tag-behaviour)
- [javascript - Modifying document.location.hash without page scrolling - Stack Overflow](https://stackoverflow.com/questions/1489624/modifying-document-location-hash-without-page-scrolling)
- [Jump links and viewport positioning – Nicolas Gallagher](http://nicolasgallagher.com/jump-links-and-viewport-positioning/)

### Scroll event, timeout and interval timers

On mobile browsers, scroll event not always emitted when scrolling (momentum, animation)

- http://tjvantoll.com/2012/08/19/onscroll-event-issues-on-mobile-browsers/
- https://github.com/cubiq/iscroll
- https://stackoverflow.com/questions/9225525/how-can-i-monitor-scroll-position-while-scrolling-in-safari-on-ios
- https://stackoverflow.com/questions/11177774/setinterval-pauses-in-iphone-ipad-mobile-safari-during-scrolling

### Delay DOM updates when scroll

Use `requestAnimationFrame` (but `setInterval` shouldn't be better?)

See "Fix 2. use requestAnimationFrame for resize and scroll event handlers" in [Fixing a parallax scrolling website to run in 60 FPS - Adventures in WebKit land](http://kristerkari.github.io/adventures-in-webkit-land/blog/2013/08/30/fixing-a-parallax-scrolling-website-to-run-in-60-fps/)

See [Relayout, repaint, reflow](#relayout-repaint-reflow)

### Scroll value

#### Viewport (window)

For all browsers, window is the main scrollable. But some browsers use the body `document.body.scrollTop` as an alias of `window.scrollY` (getter) and `window.scroll()` (setter) where other use the html element `document.documentElement.scrollTop` (webkit)

Use `document.scrollingElement` for that. Note: a [polyfill](https://github.com/mathiasbynens/document.scrollingElement) exist for that.

	document.documentElement.scrollTop || document.body.scrollTop

jQuery: `$(window).scrollTop()`

`window.scrollY`

	var x = window.scrollX//window.pageXOffset is an alias
	var y = window.scrollY//window.pageYOffset is an alias
	// Or use document.documentElement.scrollLeft or document.body.scrollLeft as fallback

For fallback (old IE < Edge):

	var supportPageOffset = window.pageXOffset !== undefined;//IE < 9
	var isCSS1Compat = ((document.compatMode || "") === "CSS1Compat");

	var x = supportPageOffset ? window.pageXOffset : isCSS1Compat ? document.documentElement.scrollLeft : document.body.scrollLeft;
	var y = supportPageOffset ? window.pageYOffset : isCSS1Compat ? document.documentElement.scrollTop : document.body.scrollTop;

	var x = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollLeft;

Or use (used in jQuery):

	var x = (window.pageXOffset || document.documentElement.scrollLeft) - (document.documentElement.clientLeft || 0)

`clientLeft` substraction used to correct for situations where you have applied a border (not padding or margin, but actual border) to the root element, and at that, possibly only in certain browsers.

- https://developer.mozilla.org/en-US/docs/Web/API/Window.scrollY
- http://www.howtocreate.co.uk/tutorials/javascript/browserwindow

Get max value:

```js
Math.max( document.body.scrollHeight, document.documentElement.clientHeight, document.documentElement.scrollHeight) - window.innerHeight
```

```js
document.documentElement.scrollHeight - document.documentElement.clientHeight;//it's fine with webkit too
```

#### Scrollable element

other than viewport

```js
element.scrollTop
```

Get max value:

```js
element.scrollTop - element.clientHeight
```

### Scroll to

#### Viewport (window)

```js
window.scroll(x, y)
```

jQuery: `$(window).scrollTop(offset)` or `$("html,body").scrollTop(offset)` or `$("html,body").animate({scrollTop: offset})`. Be carefull complete callback is **called twice**


### Scroll by

#### Scroll by pixel
#### Scroll by page
#### Scroll by line

## `NodeList` or `HTMLCollection` (as static) to `Array`

```js
let nodes = Array.from(document.querySelectorAll("*"));
```

```js
let nodes = [...document.querySelectorAll("*")];
```

```js
// slice()
let nodes = Array.prototype.slice.call(document.querySelectorAll("*"));
```

```js
// Regular loop
let nodes = new Array(nodeList.length);
for(let nodeIndex = 0; nodeIndex < nodeList.length; nodeIndex++){
	nodes.push(nodeList[i]);
}
```

Others: http://jsperf.com/nodelist-to-array/63

- https://developer.mozilla.org/en/docs/Web/API/NodeList#Why_can%27t_I_use_forEach_or_map_on_a_NodeList.3F
- https://developer.mozilla.org/en/docs/Web/API/NodeList#How_can_I_convert_NodeList_to_Array.3F
- https://stackoverflow.com/questions/3199588/fastest-way-to-convert-javascript-nodelist-to-array

## `scroll` events on mobile

http://developer.telerik.com/featured/scroll-event-change-ios-8-big-deal/

## DOM

See [JavaScript selectors](HTML#javascript-selectors)

### DOM Relations

	node.compareDocumentPosition(otherNode);

	node.contains(otherNode);

	node.parentNode;
	node.parentElement;

	node.firstChild
	node.lastChild
	node.childNodes

	node.previousSibling
	node.nextSibling

	...

- [Node.compareDocumentPosition() - Web API Interfaces | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node.compareDocumentPosition)

### Wrap DOM API

- [CanvasBlocker/lib at master · kkapsner/CanvasBlocker](https://github.com/kkapsner/CanvasBlocker/tree/master/lib) - Wrap window, Canvas, etc.

### Create node

```js
var div = Object.assign(document.createElement("div"), {
	id: "foo",
	className: "bar",
});
```

### Insert node

Prefer using `ref.parentNode.insertBefore(node, ref);` instead of `ref.parentNode.appendChild(node);`

See also [Parse HTML using the native parser](#parse-html-using-the-native-parser)

- [Surefire DOM Element insertion - Paul Irish](http://www.paulirish.com/2011/surefire-dom-element-insertion/)

### Insert text

- (prefered): (for elements without children elements) `element.textContent = text`
- `element.appendChild(document.createTextNode(text))`
- `element.insertAdjacentText("beforeend", text)` (Firefox 48+, all others)

See also [Parse HTML using the native parser](#parse-html-using-the-native-parser)

- http://jsperf.com/textcontent-vs-createtextelement

### Read text

- `element.text` HTMLStyleElement don't have that property
- `element.innerText` trigger reflow to handle hidden elements, return trimmed text with space collapsed
- `element.textContent` return all text nodes (even in hidden elements), keep all spaces

- [The poor, misunderstood innerText — Perfection Kills](http://perfectionkills.com/the-poor-misunderstood-innerText/)
- [JSON Miller 🦊⚛ on Twitter: "Demo: https://t.co/Bzi5OTohaR… "](https://twitter.com/_developit/status/1064548728906964994)
- [The difference between the Node.textContent and Element.innerText properties in vanilla JS | Go Make Things](https://web.archive.org/web/20210203180413/https://gomakethings.com/the-difference-between-the-node.textcontent-and-element.innertext-properties-in-vanilla-js/)
- [Andrea Giammarchi 🍥 on Twitter: "as both Chrome \[0\] and Safari \[1\] share pretty much the same Node.cpp file, you might like to know that node.textContent is *always* a safe bet, in terms of intent, while node.nodeValue is a CharacterData.cpp only matter 1/2 \[0\] https://t.co/tBHKDPlR77 \[1\] https://t.co/bzep1Mv6Sa" / Twitter](https://twitter.com/WebReflection/status/1361742040833400832)

### Element visibility

`element.getBoundingClientRect()` return `0,0,0,0` for not displayed elements

`element.offsetHeight === 0` means the element is not displayed but not work if element without padding nor border contains no element (children elements are out of the flow). This trigger a reflow.

`element.offsetParent !== null` return `null` when element is not displayed (!= not visible or transparent). See [javascript - What would make offsetParent null? - Stack Overflow](https://stackoverflow.com/questions/306305/what-would-make-offsetparent-null) and [HTMLElement.offsetParent - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetParent)

### `className` of SVG Element

To get class(es):

	node.getAttribute("class");

or

	typeof SVGAnimatedString !== "undefined" && node.className instanceof SVGAnimatedString ? node.className.animVal : node.className;

To set class(es):

	node.setAttribute("class", value);

or

	if(typeof SVGAnimatedString !== "undefined" && node.className instanceof SVGAnimatedString){
		node.className.baseVal = value;
	}else{
		node.className = value;
	}

### DOM clobbering

**Don't name your inputs or buttons `submit`, `action`, `method`, `style`, `dataset`, `id`, `attributes`, `children`, etc.**

```html
<form id="form" action="somewhere" method="post">
	<input type="text" name="action" value="pay">
	<input type="text" name="method" value="credit-card">
	<input type="text" name="attributes" value="something">
	<button name="submit">Send</button>
<form>
<script>
	let form = document.getElementById("form");
	form === window.form
	form.action// HTMLInputElement instead of String "somewhere"
	form.method// HTMLInputElement instead of String "post"
	form.submit// HTMLButtonElement instead of Function
	form.attributes// HTMLInputElement instead of NamedNodeMap
</script>
```

See [DOM clobbering](../../Security/Security.md#dom-clobbering)

### Clear all child nodes

Empty children, remove children

```js
// https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/replaceChildren#Examples
parent.replaceChildren();

// With textContent
parent.textContent = "";

// This method have an issue with IE: it "permanently destroys all descendant text nodes"
// see https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent#Description
// see https://stackoverflow.com/questions/28741528/is-there-a-bug-in-internet-explorer-9-10-with-innerhtml
parent.innerHTML = "";

// Use lastChild cause less layout than fistChild
while (parent.lastChild && !parent.lastChild.remove());
//while (parent.lastChild !== null) parent.lastChild.remove();
while (parent.lastChild && !parent.removeChild(parent.lastChild));
//while (parent.lastChild !== null) parent.removeChild(parent.lastChild);

// Remplace parentNode with a clone of itself without his children
// But all attached listeners and references will not match the new element
node.parentNode.replaceChild(node.cloneNode(false), node);
```

- [Remove all child elements of a DOM node in JavaScript - Stack Overflow](https://stackoverflow.com/questions/3955229/remove-all-child-elements-of-a-dom-node-in-javascript)

For replace the whole document:

```js
document.documentElement.replaceWith(newDocEl);
```

or

```js
document.replaceChild(newDocEl, document.documentElement);
```

### Find a node

- `document.getElementById()` (only element)
- `document.getElementsByTagName()` (only element)
- `element.childNodes`
- `element.querySelector()` (only element)
- `element.querySelectorAll()` (only element)
- `element.children` (only element)
- `TreeWalker` and `NodeIterator`
- ...

See also:

- [javascript - querySelector search immediate children - Stack Overflow](https://stackoverflow.com/questions/6481612/queryselector-search-immediate-children/18607777#18607777) - `element.querySelector(":scope > children")`
- [Why is getElementsByTagName() faster than querySelectorAll()? - Human Who Codes](https://humanwhocodes.com/blog/2010/09/28/why-is-getelementsbytagname-faster-that-queryselectorall/)
- [TreeWalker performance](https://codepen.io/mmems/pen/dwWyxv) - Performance of differents APIs
- [dom - Is it possible to get reference to comment element/block by JavaScript? - Stack Overflow](https://stackoverflow.com/questions/6027830/is-it-possible-to-get-reference-to-comment-element-block-by-javascript/42652191#42652191)

### Find an element / text

See also [Subordinate resource](../../Web/Web.md#subordinate-resource)

Syntaxes:

```
http://.../#css()
http://.../#xpath:/html/body/div[3]
```

Less specific = sensible to document changes
Why not just search for the text chunk: like [Adblock Plus specific CSS selector `:-abp-contains()`](https://adblockplus.org/filter-cheatsheet#elementhideemulation), [jQuery specific CSS selector `:contains()`](https://api.jquery.com/contains-selector/), [CSS selector `:contains()` removed from CSS selectors level 3 spec](https://www.w3.org/TR/selectors-3/#content-selectors) or XPath `//div[text()="bananas"]`

```js
document.evaluate('//*[contains(text(),"text to search")]', $0, null, XPathResult.FIRST_ORDERED_NODE_TYPE, null).singleNodeValue
// For IE, see [XPath, unleashed — coming to Internet Explorer 5+ HTML DOM near you | Dimitri Glazkov](https://glazkov.com/2004/04/06/xpath-unleashed/) and the code here: [XPath over HTML for MSIE download | SourceForge.net](https://sourceforge.net/projects/html-xpath/)
```

Find the nearest 50px? ascendant / neighour

1. find the nearest root
	- `body`
	- `:root` (SVG document where document.documentElement)
2. less specific
	- `#id ...`
	- `#id ~ ...`
	- `#id + ...`
3. find the path to the element
	- `element`
	- `.class`
	- `[attr=]`
	- search for siblings uniqueness
4. Match if the target is the first element that match
	- try first to find unique ascendant:

`[id=]`, `[name=]`

Or

1. `#id`
2. siblings uniqueness
	- `#id ~ ...`
	- `#id + ...`
3. element
4. `ns|...`
5. `.class`
6. `[attr]` (not name and not id) with approximation `[attr=value]` `[attr~=value]` `[attr|=value]` `[attr^=value]` `[attr$=value]` `[attr*=value]`
7. `:first-child`
8. `:nth-of-type(5)` `:nth-last-child()`
9. `:nth-child(5)` `:nth-last-of-type()`
10. restart at 1 with parent

```js
// XPath selector of an element
for(var path = '', elt = ...; elt && elt.nodeType == 1; elt = elt.parentNode){
	let idx = elt.parentNode ? Array.from(elt.parentNode.children).filter(child => child.tagName === elt.tagName).indexOf(elt) + 1 : 1;
	path = '/'+elt.tagName.toLowerCase() + (idx > 1 ? '['+idx+']' : '') + path;
}
```

Test:
- https://www.metafilter.com/175389/None-Dare-Call-It-Treason

- [WICG/ScrollToTextFragment: Proposal to allow specifying a text snippet in a URL fragment](https://github.com/WICG/ScrollToTextFragment)
- [Chrome deploys deep-linking tech in latest browser build despite privacy concerns • The Register](https://www.theregister.co.uk/2020/02/20/chrome_deploys_deeplinking/)
- [Scroll To Text Fragment · Issue #194 · mozilla/standards-positions](https://github.com/mozilla/standards-positions/issues/194)
- [Pinpointer – Add-ons for Firefox](https://addons.mozilla.org/en-US/firefox/addon/pinpointer/) - [Pinpointer/pinpointer.js at master · Rumperuu/Pinpointer](https://github.com/Rumperuu/Pinpointer/blob/master/content_scripts/pinpointer.js)
- [ericclemmons/unique-selector: Given a DOM node, return a unique CSS selector matching only that element](https://github.com/ericclemmons/unique-selector) - used by Cypress
- [Show HN: Pinpointer – A Firefox extension to share links to page elements | Hacker News](https://news.ycombinator.com/item?id=17556805)
- [pinpoint/end.js at 4b2ec192c0400f26d7ff80ec3a652e467d5ee563 · karanlyons/pinpoint](https://github.com/karanlyons/pinpoint/blob/4b2ec192c0400f26d7ff80ec3a652e467d5ee563/Pinpoint.safariextension/end.js#L98)
- [Shorter link that still works with your addon: https://en.wikipedia.org/wiki/Nel... | Hacker News](https://news.ycombinator.com/item?id=17557686)
- [Comparison of CSS Selectors and XPath - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors/Comparison_with_XPath)

### Iterate with XPath

```js
XPathResult.prototype[Symbol.iterator] = function*(){for(let node; node = this.iterateNext();){yield node}}

let toc = [...document.evaluate("/html/body//h2", document, null, XPathResult.ANY_TYPE, null)].map(h2 => h2.textContent.trim());
console.log(toc.join("\n"));
```

- [Document.evaluate() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/evaluate)

### Find all links in DOM

```js
const html = document.documentElement.cloneNode(true);

function patchURL(value, base){
	return value;
}

for(let [property, collection] of [
	["src", null, html.querySelectorAll("img, video, audio, track, source, iframe, script, embed")],
	["srcset", null, html.querySelectorAll("img, picture")],
	["data", null, html.querySelectorAll("object")],
	// inc. SVG 2 where href doesn't need anymore to be namespaced
	["href", null, html.querySelectorAll("link, a, area, base, animate, linearGradient, radialGradient, discard, feImage, hatch, image, mesh, meshgradientmpath, pattern, scripttextPath, use")],
	// SVG 1.1
	["href", "http://www.w3.org/1999/xlink", html.querySelectorAll("a, animate, linearGradient, radialGradient, discard, feImage, hatch, image, mesh, meshgradientmpath, pattern, scripttextPath, use")],
]){
	for(let element of collection){
		const isSVGElement = element instanceof SVGElement;

		// Some elements have deliberately this missing attribute (like <script> or <video><source src=""></video>)
		if(!element.hasAttributeNS(property)){
			continue;
		}

		let value = element[property];

		if(property === "srcset"){
			value = value.split(",").map(value => {
				// https://html.spec.whatwg.org/multipage/images.html#srcset-attribute
				let [url, descriptor] = value.trim().split(/\s+/);
				url = patchURL(url, base);
				return [url, descriptor].join(" ");
			}).join(",");
		}else{
			value = patchURL(value, base);
		}

		// Update the property (JSDOM doesn't rebase metas, we use absolute URLs)
		// It's often better to use absolute URLs for metas
		// But loose the ability to update base tag href
		element[property] = value;
	}
}
```

### Destructuring DOM nodes

**Note: be carefull if multiple input have same id/name.**

```js
const [deg, x, y, z] = Array.from(document.querySelectorAll("input[name=deg], input[name=x], input[name=y], input[name=z]"), input => input.value);
```

### Node name and case sensitivity

- [John Resig - .nodeName Case Sensitivity](https://web.archive.org/web/20200814104737/https://johnresig.com/blog/nodename-case-sensitivity/)

### Search text and wrap

```js
for (const range of[...findTexts('hello world')]) {
	const mark = document.createElement('mark');
	mark.appendChild(range.extractContents());
	range.insertNode(mark);
}

function* findTexts(str, {
	root = document.body
} = {}) {
	let matchPos = 0;
	let startContainer = null;
	let startOffset = 0;

	for (const textNode of nodeIterator(root, NodeFilter.SHOW_TEXT)) {
		const text = textNode.nodeValue;

		for (let i = 0; i < text.length; i++) {
			if (text[i] == str[matchPos]) {
				// Possible match
				if (matchPos == 0) {
					startContainer = textNode;
					startOffset = i;
				}

				matchPos++;

				// Total match
				if (matchPos == str.length) {
					const range = document.createRange();
					range.setStart(startContainer, startOffset);
					range.setEnd(textNode, i + 1);

					yield range;

					matchPos = 0;
					startContainer = null;
					startOffset = 0;
				}
			}
			// Match failure
			else if (matchPos) {
				matchPos = 0;
				startContainer = null;
				startOffset = 0;
			}
		}
	}
}

function* nodeIterator(...args) {
	const ittr = document.createNodeIterator(...args);

	while (true) {
		const node = ittr.nextNode();
		if (!node) return;
		yield node;
	}
}
```

- [JS Bin - Collaborative JavaScript Debugging](http://jsbin.com/walaga/edit?html,js,output)

### Wrap node children

```js
var wrapper = container.ownerDocument.createElement("button");
while (container.firstChild) {
	wrapper.appendChild(container.firstChild);
}
container.appendChild(wrapper);
```

- [Wrapping a set of DOM elements using JavaScript - Stack Overflow](https://stackoverflow.com/questions/3337587/wrapping-a-set-of-dom-elements-using-javascript)

### Loop through all elements

```js
var el = document.documentElement;
while(el){
	console.log(el);

	nextEl = el.firstElementChild/*down*/;
	/*or next or up and next*/
	if(!nextEl){
		//go up if no sibling
		while(el && el.nextElementSibling === null){
			el = el.parentElement;
		}
		// sibling or null (end)
		nextEl = el ? el.nextElementSibling : null;
	}
	el = nextEl;
}
```

### Parse SVG path using the native parser

```js
var path = document.createElementNS("http://www.w3.org/2000/svg", "path");
var parseError;
try{
	path.setAttribute("d", "m10,10C45.812,24.024,45.673,24,45.529,24H31.625c0.482-3.325,6.464-2.758,8.913-3.155z");
}
catch(error){
	parseError = error;
	console.log(error);
}

if(!parseError){
	path.pathSegList;// path data
}
```

Polygon or polyline can be used too (with the points attribute) but support only lines (only pairs of coords). Path can use points as: `d="M%POINTS%z"` where `%POINTS%` is value of the attribute `points` of the polygon/polyline.

- https://github.com/hughsk/svg-path-parser
- https://github.com/jkroso/parse-svg-path

### Parse CSS using the native parser

Parse a CSS without apply it to the current document. Resources (backgrounds, fonts, etc.) will not be loaded

```js
var doc = document.implementation.createHTMLDocument("");
var baseElement = doc.createElement('base');
//Define a base for relative URL inside stylesheet
baseElement.href = window.location;
doc.head.appendChild(baseElement);
var style = doc.createElement("style");
style.appendChild(doc.createTextNode("body{background: url(\"machine-feature1-bg.jpg\");}"));
doc.head.appendChild(style);
```

You can also listen "error" and "load" events (on `style` element) to know when the `style.sheet` is available (all import are parsed also)

Or parse rule with `stylesheet.insertRule("body{background: url(\"machine-feature1-bg.jpg\");}")`

### Parse HTML using the native parser

**Prefer use [`<template>` element](https://www.html5rocks.com/en/tutorials/webcomponents/template/)**

- https://developer.mozilla.org/en-US/docs/Code_snippets/HTML_to_DOM
- http://jsperf.com/domparser-vs-innerhtml-vs-createhtmldocument/8
- https://developer.mozilla.org/en-US/docs/JXON

All these methods don't handle charset/encoding, which is by default `UTF-8`. You can redefine it by adding manually (if it's not already included):

- XML/SVG/XHTML: update `<?xml version="1.0" ?>` to `<?xml version="1.0" encoding="ENCODING" ?>`
- HTML: insert `<meta http-equiv="Content-Type" content="text/html;charset=ENCODING">` just after the `<head>`

You can also re-encode manually the content of `htmlString`.

See also https://developer.mozilla.org/en-US/docs/Web/API/XMLSerializer

See jQuery [`$.parseHTML()`](https://github.com/jquery/jquery/blob/master/src/core/parseHTML.js) and [`$(element).load("http://example.com css-selector-of-element-in-loaded-document")`](https://github.com/jquery/jquery/blob/master/src/ajax/load.js) (v1 != v3, In v3 `$.parseHTML()` can get a different context to use a document without browsing context)

#### As nodes of the current document

**Content will be automatically loaded**: img and styles but not scripts nor iframes

##### A (detached) root node

```js
var node = document.createElement("html");
// html element will be striped (ignored, but not its content)
// head and body will be generated
// scripts, link, meta and title elements will be append to head
// Other elements will be append to body
// Note: Scripts elements (inline or external) will not be executed
node.innerHTML = htmlString;
```

##### As a sibling nodes

```js
element.insertAdjacentHTML("beforeend", htmlString);// at the end of element
```

**Note: injected HTML is parsed with the [scripting flag](https://html.spec.whatwg.org/#scripting-flag) disabled, that means like `.innerHTML` script elements are not executed**

- [Element.insertAdjacentHTML() - Web API Interfaces | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentHTML)

##### As child nodes

Note: Scripts elements (inline or external) will not be executed.

```js
element.innerHTML = htmlString;
let nodes = element.childNodes;
```

##### As `DocumentFragment`

Note: Scripts elements will be executed, only after been appended (like `document.createElement("script").textContent = "alert('inline script')"`). Images start loading immediatly (like `(new Image()).src = "image.png"`)

```js
let range = document.createRange();
range.selectNode(parent);// set the context element for the parser not required, by default it's will be document.body
let nodes = range.createContextualFragment(htmlString);
```

- [Range.createContextualFragment() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/range/createContextualFragment)
- [javascript - Inserting arbitrary HTML into a DocumentFragment - Stack Overflow](https://stackoverflow.com/questions/9284117/inserting-arbitrary-html-into-a-documentfragment/25225983#25225983)

#### As a document with browsing context

Content (img, scripts, styles, iframes, etc.) will start loading/executed immediatly.
But you can stop it with `<meta http-equiv="Content-Security-Policy" content="script-src 'none';">`

See [`iframe`](#iframe)

With `document.write()`

```js
// iframe must be added to an online document
var frameDoc = iframe.contentWindow.document;
frameDoc.open();
//Note: update iframe content force new history record.
frameDoc.write('<html><head><title>' + document.title + '</title><script>var frameHash="' + _hash + '";</script></head><body>&nbsp;</body></html>');
frameDoc.close();
```

Or with `innerHTML`

```js
iframe.contentDocument.documentElement.innerHTML = htmlString;
```

Or with Data URI

```js
// With data URI
iframe.src = "data:text/html," + encodeURIComponent(htmlString);
```

```js
// With Blob
iframe.src = URL.createObjectURL(new Blob([htmlString], {type: "text/html"}));
//iframe.src = URL.createObjectURL(new File([htmlString], "iframe.html", {type: "text/html"}));
```

```js
// With srcdoc attribute
iframe.srcdoc = htmlString
```

Document access to iframes with Data URI, can fail on some browsers for [security reason (crossdomain)](https://stackoverflow.com/a/14149618/470117). Use others methods (Blob or `srcdoc` attribute)

##### As replacement of an existing document

```js
document.open();
document.write(htmlChunk);
document.write(htmlChunk2);
document.close();
```

Note: It create a new history entry (navigated to `wyciwyg://0/DOCUMENT_URL`) if the document have a browsing context (cancel the current navigation if any). To not an history entry, use `document.open("text/html", "replace")` instead.

- [Document.open() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/open#Notes)

##### As sandboxed document

You can't access direclty to the document, you need to use `iframe.contentWindow.postMessage()`

```js
let iframe = document.createElement("iframe");
iframe.sandbox = "";// enable sandbox mode, same as iframe.setAttribute("sandbox", "");
iframe.srcdoc = htmlString;// not supported by IE and Edge http://caniuse.com/#feat=iframe-srcdoc Note: document.URL will be about:srcdoc
// or iframe.src = "javascript:'" + htmlString.replace(/\\/, "\\").replace(/'/, "\\'") + "'";// becarefull with the javascript protocol, it's affected by the URI length can be limited
// or iframe.src = "data:text/html," + htmlString;// can be affected by cross domain rules or not
// of iframe.src = blobURI;
iframe.hidden = true;// hide
document.body.appendChild(iframe);
```

#### As a document without browsing context

**Content (img, scripts, styles, iframes, etc.) will not be loaded/executed.** It's allow to clean up the HTML by removing script, `on[event]` attributes, iframes, etc.

If you need to remove all unsafe code, use [DOMPurify](https://github.com/cure53/DOMPurify).

To load element from a document without browsing context, you have to adopt it to a document with browsing context:

```js
// Add a base to fix issues with some browsers. See https://github.com/jquery/jquery/issues/2965
let base = doc.createElement("base");
base.href = document.location.href;
doc.head.appendChild(base);
img;// from doc

document.adoptNode(img);
// Now, we you need to load it:
// add it to the current document's tree
document.body.appendChild(img);
// or update the src
let src = img.src;
img.src = "about:blank";
img.src = src;// need async operation?
```

Or clone it with `var node = document.importNode(nodeFromOtherDoc);`

Note: to know if a node is has no browsing context test `node.ownerDocument.defaultView == null` (or `node.baseURI == "about:blank" || node.ownerDocument.readyState == "uninitialized"` could works too).

Note: `document.adoptNode()` and `document.importNode()` are not supported by IE?-8

> And the `Document` originally created for an `iframe element, which has since been [removed from the document](https://html.spec.whatwg.org/multipage/infrastructure.html#remove-an-element-from-a-document), has no associated browsing context, since that browsing context was [discarded](https://html.spec.whatwg.org/multipage/browsers.html#a-browsing-context-is-discarded).

- [HTML Standard](https://html.spec.whatwg.org/multipage/browsers.html#concept-document-bc)

##### As a document without browsing context with `createHTMLDocument`

```js
var doc = document.implementation.createHTMLDocument("");
// innerHTML
doc.documentElement.innerHTML = htmlString;
// or with doc.body.innerHTML or doc.head.innerHTML
// or with doc.….insertAdjacentHTML("beforeend", htmlString)
// write():
// 	doc.open();
// 	// Can use HTML chunks, like: "<span", ">test</s", "pan>"
// 	doc.write(htmlChunk);
// 	doc.write(htmlChunk2);
// 	doc.close();
```

- [`wysiwyg://ID/http://...`](http://www.xav.com/scripts/axs/help/1510.html)
- https://github.com/jakearchibald/streaming-include/blob/master/polyfill/index.js#L42 - stream HTML into an element, that handle templates node too

##### As a document without browsing context with `DOMParser`

... and `text/html`

Note: For XML it don't throw a parse error if fail to parse the document source. Instead it return an [error document](https://developer.mozilla.org/en-US/docs/Web/API/DOMParser#Error_handling).
For HTML documents parser are permissive https://www.w3.org/TR/html5/single-page.html#parse-error https://www.w3.org/TR/html5/single-page.html#syntax-errors

> `script` elements get marked unexecutable and the contents of `noscript` get parsed as markup.
> - [DOM Parsing and Serialization](https://w3c.github.io/DOM-Parsing/#the-domparser-interface)

```js
const parser = new DOMParser();
const doc = parser.parseFromString(htmlString, "text/html");
```

```js
// Parse encoded HTML, HTML entities
const str = "&lt;p&gt;";
new DOMParser().parseFromString('<!doctype html><body>' + str, 'text/html').body.textContent
// > "<p>"
```

- https://developer.mozilla.org/en-US/docs/Web/API/DOMParser

##### As a document without browsing context with `XMLHttpRequest`

Note: The Fetch API don't allow to parse a HTML/SVG document. See https://developer.mozilla.org/en-US/docs/Web/API/Body. It's still possible to extend Body to support it (add method like `body.xDocument()`)

```js
var xhr = new XMLHttpRequest();
// With Blob (recommended)
var uri = URL.createObjectURL(new Blob([htmlString], {type: "text/html"}));
// With data URI (not recommended)
//var uri = "data:text/html," + encodeURIComponent(htmlString);
xhr.open("GET", uri);
xhr.responseType = "document";
xhr.addEventListener("load", () => {
	URL.revokeObjectURL(uri);//only for blob URI
	var doc = xhr.response;
	console.log(doc);
});
xhr.send(null);
```

Note: This method (XHR + data URI) is not supported by all browsers (eg.: Safari).

- https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest
- https://github.com/w3c/web-platform-tests/blob/master/XMLHttpRequest/data-uri.htm

#### Parse streamed HTML

HTML Document or fragment.

See [Streamed data](#streamed-data)

Note: scripts insert in parent document shouldn't be executed (but Edge, Safari & Chrome all do) https://html.spec.whatwg.org/multipage/syntax.html#scripts-that-modify-the-page-as-it-is-being-parsed https://twitter.com/zcorpan/status/806150847184928768
What about `<meta http-equiv="Content-Security-Policy" content="script-src 'none';">`?

- https://cspvalidator.org/

```js
var content = document.querySelector('.content');
// Create an iframe:
var iframe = document.createElement('iframe');
// Put it in the document (but hidden):
iframe.style.display = 'none';
document.body.appendChild(iframe);
content.innerHTML = '';
// Wait for the iframe to be ready:
iframe.onload = function() {
	// Ignore further load events:
	iframe.onload = null;

	var xhr = new XMLHttpRequest();// can be done with fetch too
	var charsLoaded = 0;
	// Write a dummy tag:
	iframe.contentDocument.write('<div class="xhr-content-wrapper">');
	// Get a reference to that element:
	// Pull it out of the iframe & into the parent document:
	content.appendChild(iframe.contentDocument.querySelector('.xhr-content-wrapper'));

	// Here, the parser maintains a stack of open elements https://html.spec.whatwg.org/multipage/syntax.html#stack-of-open-elements

	// Write some more content (async):
	xhr.onprogress = function() {
		iframe.contentDocument.write(xhr.response.slice(charsLoaded));
		charsLoaded = xhr.response.length;
	};

	// Keep writing content like above, and then when we're done:
	xhr.onload = function() {
		iframe.contentDocument.write('</div>');
		iframe.contentDocument.close();
	};

	xhr.responseType = "text";
	xhr.open('GET', 'comments.inc.txt');
	xhr.send();
};
// Initialise the iframe
iframe.src = 'about:blank';
```

- [Fun hacks for faster content - JakeArchibald.com](https://jakearchibald.com/2016/fun-hacks-faster-content/#using-iframes-and-documentwrite-to-improve-performance)
- https://github.com/jakearchibald/streaming-html

### Load SVG inline

```html
<svg><use xlink:href="symbols.svg#signal"/></svg>
<iframe src="signal.svg" onload="this.before(contentDocument.children[0]);this.remove();"></iframe>
```

- [CodePen - Inline an SVG file in HTML, declaratively & asynchronously!](https://codepen.io/scottjehl/project/full/XrzdYk)

### `iframe`

Note: Until the iframe is added to an online document, the `iframe.contentDocument` and `iframe.contentWindow` will be `null` (and not loaded). Once the iframe has been added to an online document, it's could be removed from that document (but must be done asynchronously)

`iframe.sandbox` can be used to disable scripts, popups, top navigation, etc. even same orgin access (but useless since the contained scripts could disabled it)

```html
<iframe id="iframe" src="data:text/html;charset=UTF-8,<!DOCTYPE html><html><head></head><body><h1>FAIL</h1></body></html>"></iframe>
<script>
	let iframe = document.getElementById("iframe")
	console.log(iframe.contentDocument.body.innerHTML); // ""
	iframe.contentDocument.body = "PASS 1"; // works because data uri has not yet resolved. Will be overwritten.
	setTimeout(function(){ iframe.contentDocument.body = "PASS 2"; }, 10); // will throws security error
</script>
```

An iframe don't inherit it's parent's CSP if sandbox attribute has `allow-same-origin` disabled:

```js
// In a document with a strict CSP. Ex: script-src 'self'
let iframe = document.createElement("iframe");
iframe.srcdoc = `<html><head><script src='https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js'></script></head><body><script>$(document.body).text('Hello from jQuery')</script></body></html></iframe>`;
iframe.sandbox = "allow-scripts";
document.body.appendChild(iframe);
```

### Create a new SVG document without browsing context

```js
const svg = document.implementation.createDocument("http://www.w3.org/2000/svg", "svg:svg", null);
```

### DOM mutation

Note: Observe the common ancestor of targeted nodes (eg. `document.documentElement`, `document.body` or deeper) instead of small subtrees (multiple observers)

All mutation happend even for disconnected nodes. Mutation happend on newly created node are "muted":

```js
const a = document.body.firstChild;
const b = document.createElement("div");
b.appendChild(a);// mutation: a removed from body
document.body.appendChild(b);// mutation: b added to body
```

```js
const a = document.body.firstChild;
const b = document.createElement("div");
document.body.appendChild(b);// mutation: b added to body
b.appendChild(a);// mutation: a removed from body + a added to b
```

Note: It's impossible to observe only namespaced attributes like `xlink:href`, because it's not supported: [javascript - Why does MutationObserver not recognize the xlink:href attribute in the attributeFilter array? - Stack Overflow](https://stackoverflow.com/questions/39047902/why-does-mutationobserver-not-recognize-the-xlinkhref-attribute-in-the-attribut). The spec exclude nodes when ["`attributeFilter` does not contain name or namespace is non-null"](https://dom.spec.whatwg.org/#queueing-a-mutation-record).

Note, contenteditable elements do not trigger MutationObserver:

> Using the MutationObserver polyfill, it isn't possible to monitor mutations of an element marked `contenteditable`.
> See [the mailing list](https://groups.google.com/forum/#!msg/polymer-dev/LHdtRVXXVsA/v1sGoiTYWUkJ)

You need to listen some events like `input` or `DOMSubtreeModified` (depreciated): [javascript - contenteditable change events - Stack Overflow](https://stackoverflow.com/questions/1391278/contenteditable-change-events)

- use `MutationObserver` or use Live Collections with `requestAnimationFrame` (or `setInterval`)
- [Three Real-World Uses for Mutation Observer - Eager Blog](https://eager.io/blog/three-real-world-use-cases-for-mutation-observer/)
- [javascript - Performance of MutationObserver to detect nodes in entire DOM - Stack Overflow](https://stackoverflow.com/questions/31659567/performance-of-mutationobserver-to-detect-nodes-in-entire-dom/39332340#39332340) - Tips about observing node in the whole document
- [Mutation Observer notes - QuirksBlog](https://www.quirksmode.org/blog/archives/2017/11/mutation_observ.html)
- [Examples Using the MutationObserver API - a Collection by Louis Lazaris on CodePen](https://codepen.io/collection/njwmrK/#)

### Create a stylesheet

See [Parse CSS using the native parser](#parse-css-using-the-native-parser)

```js
const s = document.createElement("style");
s.type = "text/css";
s.appendChild(document.createTextNode("body { background: #222; } /*... more css ..*/"));// don't use .innterText
document.head.appendChild(s);
```

Or to link to a file:

```js
const s = document.createElement("link");
s.type = "text/css";
s.rel = "stylesheet";
s.href = "/url/to/css/file.css";
document.head.appendChild(s);
```

### Iterate over stylesheet

See [tree traversal stack](../../Algorithms/Tree%20traversal/Tree%20traversal.md#stack)

**The loop does not support modifications (insert/delete)**

Stylesheet rule walker:

```js
console.group("sheet:");
var treeIndexes = [];
var deep = 0;
var index = 0;
var group = this._stylesheet;
var rules = group.cssRules;
var numRules = rules.length;
// The loop on rules and child rules
while(true){
	// Go up
	if(index >= numRules){
		// This is the end
		if(deep === 0){
			break;
		}

		// Read previous index saved
		// Continue iterate to parent
		deep--;
		index = ++treeIndexes[deep];
		group = group.parentRule || group.parentStyleSheet;
		rules = group.cssRules;
		numRules = rules.length;
		// Continue the loop but on next parent rules (if any)
		continue;
	}

	let rule = rules[index];
	switch(rule.type){
		// CSSGroupingRule
		// -> CSSConditionRule
		//	-> CSSMediaRule
		//	-> CSSSupportsRule
		case CSSRule.MEDIA_RULE:
		case CSSRule.SUPPORTS_RULE:
			// CSSKeyframesRule
		case CSSRule.KEYFRAMES_RULE:
			// CSSImportRule
		case CSSRule.IMPORT_RULE:
			// CSSDocumentRule
		case CSSRule.DOCUMENT_RULE:
			// CSSViewportRule
		case CSSRule.VIEWPORT_RULE:
			// CSSRegionStyleRule
		case CSSRule.REGION_STYLE_RULE:
		{
			treeIndexes[deep] = index;
			deep++;
			index = 0;
			group = rule.type == CSSRule.IMPORT_RULE ? rule.styleSheet : rule;
			rules = group.cssRules;
			numRules = rules.length;
			// Continue the loop but on child rules
			continue;
		}
		case CSSRule.STYLE_RULE:
		// CSSPageRule https://developer.mozilla.org/en-US/docs/Web/CSS/@page
		case CSSRule.PAGE_RULE:
		// CSSKeyframeRule
		case CSSRule.KEYFRAME_RULE:
		{
			console.log(rule.selectorText || rule.keyText);
			let propIndex = 0;
			// https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration
			let styleDec = rule.style;
			while((propName = styleDec.item(propIndex++)) !== ""){
				switch(propName){
					// Shorthand (like margin, padding and background) are expanded properties are not used here (IE9, Chrome 40, FF 36)
					// But spec is unclear
					// http://lists.w3.org/Archives/Public/www-style/2012Jan/1122.html
					// http://lists.w3.org/Archives/Public/www-style/2011Apr/0331.html
					// https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Properties_Reference
					case "height":
					case "margin-top":
					//...
					{
						propValue = styleDec.getPropertyValue(propName);
						// Rewrite value
						styleDec.setProperty(propName, propValue, styleDec.getPropertyPriority(propName));
						break;
					}
				}
			}
			break;
		}
	}

	index++;
}
console.groupEnd();
```

Remove all `:hover` and `:active` rules:

```js
const selectorFilter = (selector) => !selector.match(":hover") && !selector.match(":active");
var rulesGroups = Array.from(document.styleSheets);
while(rulesGroups.length > 0){
	let rulesGroup = rulesGroups.shift();

	for (let index = rulesGroup.cssRules.length - 1; index >= 0; index--) {
		let rules = rulesGroup.cssRules;
		let rule = rules[index];

		switch(rule.type){
			// CSSGroupingRule
			// -> CSSConditionRule
			//	-> CSSMediaRule
			//	-> CSSSupportsRule
			case CSSRule.MEDIA_RULE:
			case CSSRule.SUPPORTS_RULE:
			// // CSSKeyframesRule
			// case CSSRule.KEYFRAMES_RULE:
			// CSSImportRule
			case CSSRule.IMPORT_RULE:
			// CSSDocumentRule
			case CSSRule.DOCUMENT_RULE:
			// CSSViewportRule
			case CSSRule.VIEWPORT_RULE:
			// CSSRegionStyleRule
			case CSSRule.REGION_STYLE_RULE:
				rulesGroups.push(rule.type == CSSRule.IMPORT_RULE ? rule.styleSheet : rule);
				continue;
			case CSSRule.STYLE_RULE:
			// CSSPageRule
			case CSSRule.PAGE_RULE:
			// CSSKeyframeRule
			// case CSSRule.KEYFRAME_RULE:
			{
				let selectors = rule.selectorText;
				let filteredSelectors = selectors.split(",").filter(selectorFilter).join(",");
				if (selectors != filteredSelectors) {
					// If multiple selectors and selectors remains
					if(filteredSelectors != ""){
						let content = rule.cssText.split("{")[1].slice(0, -1);// content, between accolades: selector{content}
						rulesGroup.insertRule(`${filteredSelectors}{${content}}`, rules.length);
					}
					rulesGroup.deleteRule(index);
				}
				break;
			}
		}
	}
}
```

```js
// Note: if you just want to remove some selector / rules, use:
// style.textContent = style.textContent.replace(/(.some-selector)(:|\s|,|{)/g, "$1__disabled__$2");
// Update style as raw CSS instead of use CSSOM is ~110x quicker (ex: 0.2ms vs 23.7ms)

var style = document.getElementById("onetrust-style");
// CSSStyleSheet and CSSGroupingRule (CSSMediaRule, CSSSupportsRule, CSSDocumentRule, CSSPageRule)
function removeSelector(rulesSet, filter){
	var cssRules = rulesSet.cssRules;
	for(var i = 0; i < cssRules.length;){
		var rule = cssRules[i];
		var keep = true;
		switch(rule.type){
			case 1://CSSRule.STYLE_RULE:
				// /!\ "," can be ecaped, see https://mathiasbynens.be/notes/css-escapes
				// should be selectorText.split(/(?<=[^\\](?:\\\\)*),/)
				// but look behind is not well supported, simplify by hope escaped "," is not used by this stylesheet
				var selector = rule.selectorText = rule.selectorText.trim().split(/\s*,\s*/).filter(filter).join(", ");
				keep = selector.length > 0;
				break;
			// rules group CSSGroupingRule
			case 4://CSSRule.MEDIA_RULE:
			case 12://CSSRule.SUPPORTS_RULE:
			case 13://CSSRule.DOCUMENT_RULE:
			case 6://CSSRule.PAGE_RULE:
				keep = removeSelector(rule, filter);
				break;
			case 3://CSSRule.IMPORT_RULE:
				keep = removeSelector(rule.styleSheet, filter);// /!\ "null if the style sheet has not yet been loaded or if the style sheet was not loaded because, for example, the media type did not apply."
				break;
		}

		if(keep){
			i++;
			continue;
		}

		rulesSet.deleteRule(i);
	}

	return cssRules.length > 0;
}

removeSelector(style.sheet, function(selector){
	return true;
});
```

### Remove all children

#### Don't

```js
parent.innerHTML = "";
```

Slow, less efficient than `removeChild()` and not available with SVG nodes.
Also destroy content grandchild's content too (on IE)

- https://github.com/WebKit/webkit/blob/1aa97d5db6fdb85f703378daff3cb9759bb9687f/Source/WebCore/editing/markup.cpp#L1086
- [javascript - Is there a bug in Internet Explorer 9/10 with innerHTML=""? - Stack Overflow](https://stackoverflow.com/questions/28741528/is-there-a-bug-in-internet-explorer-9-10-with-innerhtml)

#### Do

```js
while (parent.firstChild) {
	parent.removeChild(parent.firstChild);
}
```

`parent.textContent = ""` could also be used, but less performant than `removeChild()` (jQuery use this method)

- [Remove all child elements of a DOM node in JavaScript? - Stack Overflow](https://stackoverflow.com/questions/3955229/remove-all-child-elements-of-a-dom-node-in-javascript)
- [What is the best way to empty an node in JavaScript - Stack Overflow](https://stackoverflow.com/questions/13798796/what-is-the-best-way-to-empty-an-node-in-javascript)
- [.empty() | jQuery API Documentation](http://api.jquery.com/empty/)

### Match invalid ID or class with `querySelector`

```js
document.querySelector("#" + element.id.replace(/(\*|\.|\\|:|\s|\[|\]....TODO....)/g, "\\$1"));
```

- https://stackoverflow.com/questions/448981/what-characters-are-valid-in-css-class-selectors

### Compare document/node

- https://github.com/patrick-steele-idem/morphdom

### Get all comments nodes

```js
var nodeIterator = document.createNodeIterator(
	document.body,
	NodeFilter.SHOW_COMMENT,
	node => NodeFilter.FILTER_ACCEPT
);
// For each comment node
while ( nodeIterator.nextNode() ) {
	nodeIterator.referenceNode.nodeValue
}
```

```js
node.nodeType === Node.COMMENT_NODE;//8
```

- [Document.createTreeWalker() - Web API Interfaces | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/createTreeWalker)

### Access to the script element's content

	script.text;
	script.textContent;
	script.normalize();script.firstChild.nodeValue;

- [4.11 Scripting — HTML5](http://www.w3.org/TR/html5/scripting-1.html#dom-script-text)

### Update text and attributes of all nodes

Could be used to localize. Will search and replace in all text nodes and attributes. It's adviced to do it for a document without browsing context, because it can update resources source path.

```js
function l10nString(value){
	return value.replace(/__MSG_(.+)__/g, (match, group1) => i18n.getMessage(group1));
}

function l10nDocument(document){
	document.normalize();// merge all adjacent text nodes
	let nodeIterator = document.createNodeIterator(
		document.documentElement,
		NodeFilter.SHOW_ELEMENT | NodeFilter.SHOW_TEXT,
		node => node.nodeType == Node.ELEMENT_NODE && node.hasAttributes() || node.nodeType == Node.TEXT_NODE ? NodeFilter.FILTER_ACCEPT : NodeFilter.FILTER_REJECT
	);
	while(nodeIterator.nextNode()){
		let node = nodeIterator.referenceNode;

		if(node.nodeType == Node.TEXT_NODE){
			node.nodeValue = l10nString(node.nodeValue);
			continue;
		}

		if(node.nodeType == Node.ELEMENT_NODE){
			Array.from(node.attributes).forEach(attr => {
				let value = attr.value;
				let newValue = l10nString(value);
				if(newValue == value){
					return;
				}

				node.setAttribute(attr.name, newValue);// We don't need XML namespace here (HTML5 don't support it). Else use .setAttributeNS(attr.namespace, attr.localName, attr.value)
			});
			continue;
		}
	}
}
```

### Tables

Table section: tbody, thead, tfoot

- `tableOrTableSection.insertRow()`, `tableOrTableSection.deleteRow()`
- `table.createTHead()`, `table.deleteTHead()`, etc.
- `tableOrTableSection.rows`
- `table.tBodies`
- `table.caption`
- ...

- [HTMLTableElement - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLTableElement)

### Empty document

- about:blank
- data:text/html;,<!doctype html>
- `iframe srcdoc=""`
- javascript:false javascript:undefined

- [Jake Archibald on Twitter: "The fact that about:blank, LITERALLY AN EMPTY PAGE, is full of weird edge cases, is the most 'web' thing."](https://twitter.com/jaffathecake/status/926097042140815360)
- [The Joy of about:blank](https://hsivonen.fi/about-blank/)

### DOM API trigger event

> `.focus()`, `.blur()`, `.click()`, `.reset()` - triggered a DOM-event. All with the exception of the `.submit()` method, which did not trigger a DOM-event when invoked programmatically.

> DOM-methods don't always lead to DOM-events. For example, if I call `.focus()` on an element that is already focused, then there is no subsequent "focus" event. Same with the "blur" event.

> user-triggered events and system-triggered events

> programmatic form submission

### Parse float attribute

Lossy parse float attribute

	var val = parseFloat(element.getAttribute("data-length")) || 0;

if attr not exist `getAttribute` returns null. parseFloat return `NaN` for invalid float (like null) with the OR condition 0 will be returned.

### `window.name`

Browsers keep the window name across ~~origns~~ navigation in the same tab/frame.
This property can store string (can be objects serialized to string or [encrypted string](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/encrypt)).

This property is not intended to be use as a storage. **Use `sessionStorage` to keep data across navigation in the same tab/frame. Use `postMessage()` to share data between different origins.**

> [In Firefox 82,] if a new page from another domain is loaded into a tab, then window.name is set to the empty string (the original string is restored if the tab reverts back to the original page)

> IE7 runs slower as soon as you start putting more than 2MB into window.name. FF3 runs pretty stable even with +200MB.
> [...]
> When I type new url on address bar. The Firefox take all my CPU around 30 sec and then display the warning to continue or terminate the running script

> IE11 is DEFINITELY clearing the window.name property on every page request. (set random chars)
> [...]
> I had the same problem and found out that you need to rename the window AFTER you set the new window.location

- [HTTP cookie - Wikipedia](https://en.wikipedia.org/wiki/HTTP_cookie#%22window.name%22_DOM_property)
- [javascript - Why is window.name cached? - Stack Overflow](https://stackoverflow.com/questions/33074840/why-is-window-name-cached)
- [Google Code Archive - Long-term storage for Google Code Project Hosting.](https://code.google.com/archive/p/quipt/)
- [window.name Transport - Blog | SitePen](https://www.sitepen.com/blog/2008/07/22/windowname-transport/)
- [window.name won't be preserved after navigation - Microsoft Edge Development](https://developer.microsoft.com/en-us/microsoft-edge/platform/issues/105516/)
- [internet explorer - Javascript set window.name - issue in IE - Stack Overflow](https://stackoverflow.com/questions/12645374/javascript-set-window-name-issue-in-ie)
- [50513 - window.open("", "name") will not reuse existing/opened windows - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=50513)
- [444222 - window.name can be used as an XSS attack vector](https://bugzilla.mozilla.org/show_bug.cgi?id=444222)

### Web component

- [Web Components | MDN](https://developer.mozilla.org/en-US/docs/Web/Web_Components)
- [HTML Standard](https://html.spec.whatwg.org/multipage/custom-elements.html#valid-custom-element-name)
- [html - W3C validation for \<ui-select\> - Stack Overflow](https://stackoverflow.com/questions/28508533/w3c-validation-for-ui-select/28711028#28711028) - W3C HTML Checker (validator) support Web components
- [Web Components will replace your frontend framework](https://medium.com/@drmoerkerke/web-components-will-replace-your-frontend-framework-3b17a580831c)
- [Shadow DOM v1: Self-Contained Web Components  |  Web Fundamentals  |  Google Developers](https://developers.google.com/web/fundamentals/web-components/shadowdom)
- [What's New in Shadow DOM v1 (by examples) — hayato.io](https://hayato.io/2016/shadowdomv1/) - Differences between draft (v0) and spec (v1)

Polyfills:

- [tuespetre/shadow-dom: A Shadow DOM v1 polyfill](https://github.com/tuespetre/shadow-dom)
- [webcomponents/webcomponentsjs: A suite of polyfills supporting the HTML Web Components specs](https://github.com/webcomponents/webcomponentsjs)

About SEO:

- [Is or how can Shadow DOM be 'SEO friendly'? · Issue #500 · w3c/webcomponents](https://github.com/w3c/webcomponents/issues/500)

### Document contains

Aka test if the element attached to the document

```js
element.ownerDocument.body.contains(element)
element.ownerDocument.contains(element)// not supported by IE11
element.isConnected// not supported by IE11
Boolean(element.ownerDocument.compareDocumentPosition(element) & Node.DOCUMENT_POSITION_CONTAINED_BY)
```

- [Node.isConnected - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/isConnected)
- [Node.contains() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/contains)
- [Node.compareDocumentPosition() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/compareDocumentPosition)

## Parse JavaScript using the native parser

- [`HTMLScriptElement#src=x`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLScriptElement/href) via URI of a resource contains script code
- for a script element [`Node#innerText`](https://developer.mozilla.org/en-US/docs/Web/API/Node/innerText), [`Node#textContent`](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent) (with a newly created script element)
- [HTMLScriptElement#text=x](https://developer.mozilla.org/en-US/docs/Web/API/HTMLScriptElement#text_property) (with a newly created script element)
- for a script element, [`Node#appendChild(new TextNode(x))`](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild), [`ParentNode#append(new TextNode(x))`](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode/append) via a `TextNode` contains script code
- [`Document#write(x)`](https://developer.mozilla.org/en-US/docs/Web/API/Document/write) via HTML contains script tag
- [`Document#writeln(x)`](https://developer.mozilla.org/en-US/docs/Web/API/Document/writeln) via HTML contains script tag
- [`Worker(x)`](https://developer.mozilla.org/en-US/docs/Web/API/Worker/Worker) via URI of a resource contains script code
- [`eval(x)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval) via script code string
- [`Function(x)()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function) via script code string
- [`WindowOrWorkerGlobalScope#setTimeout(x)`](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout) via script code string
- [`WindowOrWorkerGlobalScope#setInterval(x)`](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setInterval) via script code string
- [`Window#setImmediate(x)`](https://developer.mozilla.org/en-US/docs/Web/API/Window/setImmediate) and prefixed version `Window#msSetImmediate(x)` via script code string
- [`Document#execCommand()`](https://developer.mozilla.org/en-US/docs/Web/API/Document/execCommand) (how?)
- [CSS dynamic property value `expression(x)`](https://msdn.microsoft.com/en-us/library/ms537634%28v=vs.85%29.aspx) (IE?-8 only) via script code expression in CSS → all CSS injection points could be used
- [`CSSStyleDeclaration#setExpression(x)`](https://msdn.microsoft.com/en-us/library/aa768724%28v=vs.85%29.aspx) via script code string (?? `CSSStyleDeclaration#cssText = x`, `HTMLElement#setAttribute("style", x)`, style element and stylesheet API)
- [attribute expression `HTMLElement#setExpression(x)`](https://msdn.microsoft.com/en-us/library/ms531196%28v=vs.85%29.aspx) (IE?-8 only) via script code string
- [`Location`](https://developer.mozilla.org/en-US/docs/Web/API/Location) available via [`Window#location`](https://developer.mozilla.org/en-US/docs/Web/API/Window/location) and [`Document#location`](https://developer.mozilla.org/en-US/docs/Web/API/Document/location) with javascript: protocol:
	- for `Window#location` or `Document#location`: [`HTMLHyperlinkElementUtils#href=x`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLHyperlinkElementUtils/href) via javascript: protocol
	- [`Location#replace(x)`](https://developer.mozilla.org/en-US/docs/Web/API/Location/replace) via javascript: protocol
	- [`Location#assign(x)`](https://developer.mozilla.org/en-US/docs/Web/API/Location/assign) via javascript: protocol
- [`Document#URL=x`](https://developer.mozilla.org/en-US/docs/Web/API/Document/URL) via javascript: protocol
- [`WindowClient#navigate(x)`](https://developer.mozilla.org/en-US/docs/Web/API/WindowClient/navigate) via javascript: protocol
- [`execScript(x)`](https://msdn.microsoft.com/en-us/library/ms536420%28v=vs.85%29.aspx) (IE?-10 only)
- [`Crypto#generateCRMFRequest(x)`](https://developer.mozilla.org/en-US/docs/Archive/Mozilla/JavaScript_crypto/generateCRMFRequest) (Firefox ?-33)
- [`Range#createContextualFragment(x)`](https://developer.mozilla.org/en-US/docs/Web/API/Range/createContextualFragment) via HTML contains script tag
- [`Window#open(x)`](https://developer.mozilla.org/en-US/docs/Web/API/Window/open) via javascript: protocol
- [`Window#showModalDialog(x)`](https://developer.mozilla.org/en-US/docs/Web/API/Window/showModalDialog) via javascript: protocol
- [`Window#showModelessDialog(x)`](https://msdn.microsoft.com/en-us/library/ms536761%28v=vs.85%29.aspx) via javascript: protocol
- [`Element#innerHTML=x`](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML) via HTML contains script tag
- [`Element#outerHTML=x`](https://developer.mozilla.org/en-US/docs/Web/API/Element/outerHTML) via HTML contains script tag
- for an anchor, [`HTMLHyperlinkElementUtils.href=x`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLHyperlinkElementUtils/href) via javascript: protocol
- [`HTMLInputElement#formAction=x`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement) via javascript: protocol. Require the form to be submitted
- [`HTMLFormElement#action=x`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/action) via javascript: protocol. Require the form to be submitted
- [`HTMLObjectElement#data=x`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLObjectElement) via javascript: protocol
- [`HTMLIFrameElement#src=x`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLIFrameElement/src) via URI of a resource contains script code
- [`HTMLIFrameElement#srcdoc=x`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLIFrameElement/srcdoc) via HTML contains script tag
- Depends the element, [`Element.on*=x`]() via script code string. Require to call `Element.on*()` after the definition
- [`Element#insertAdjacentHTML(x)`](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentHTML) via HTML contains script tag
- [`elm.y=x`]() (where `y` is an attribute name that support javascript string like `onclick`)
- [`elm.attributes.y.value=x`]() (where `y` is an attribute name that support javascript string like `onclick`)

(works where?) `location(x)`, `Location#protocol=x`, `elm.movie=x`, `elm.value=x`, `elm.values=x`

```js
// https://source.chromium.org/chromium/_/chromium/devtools/devtools-frontend/+/dbebc4acd3b6d8c31615823c97e5f79c26984657:front_end/object_ui/JavaScriptREPL.js;l=20;drc=d99073444212bb89db6b2e763672c17e3e8f093f
function wrapObjectLiteral(code) {
    // Only parenthesize what appears to be an object literal.
    if (!(/^\s*\{/.test(code) && /\}\s*$/.test(code))) {
      return code;
    }

    const parse = (async () => 0).constructor;
    try {
      // Check if the code can be interpreted as an expression.
      parse('return ' + code + ';');

      // No syntax error! Does it work parenthesized?
      const wrappedCode = '(' + code + ')';
      parse(wrappedCode);

      return wrappedCode;
    } catch (e) {
      return code;
    }
  }

```

- [In the DOM, no one will hear you scream](https://slideshare.net/x00mario/in-the-dom-no-one-will-hear-you-scream/20)

## Eval stack name

> script-eval.js:W:Z

instead of:

> script.js line X > eval:W:Z

```js
eval("/*code*/\n//# sourceURL=script-eval.js")
(new Function("/*function body*/\n//# sourceURL=script-eval.js"))()
```

- [Debug eval sources - Firefox Developer Tools | MDN](https://developer.mozilla.org/en-US/docs/Tools/Debugger/How_to/Debug_eval_sources)

## Global error handler

Catch error, then send [beacon](#beacon)

```js
window.addEventListener("error", event => {
	//ErrorEvent
	const data = event.message.startsWith("Script error") ? {
		// Script error from inaccessible crossorigin script, values (filename, line, col, error, etc.) are not available
		message: "Uncaught Error: Crossorigin script error"
	} : {
		message: event.message,// Message
		filename: event.filename,// URL of the script
		lineno: event.lineno,// Line
		colno: event.colno,// Column
		stack: event.error && event.error.stack || "[stack trace unavailable]",// Stack
		timestamp: event.timeStamp,
		docurl: document.URL,// document URL
		url: location.href// current URL
	}

	// sendBeacon could be not supported by the browser, you need to use AJAX as fallback
	if(!navigator.sendBeacon("/error", new URLSearchParams(data))){
		console.error(event);// the amount of data to be queued exceeds the user agent limit
	}
});
```

```js
window.onerror = function (message, name, lineno, colno, error) {
	//...
	return false;
};
```

And wrap addEventListener, setTimeout, setInterval callback

For inaccessible crossorigin scripts errors (`Script Error.` or `Script Error, Line 0`):

- [Cryptic "Script Error." reported in Javascript in Chrome and Firefox - Stack Overflow](https://stackoverflow.com/questions/5913978/cryptic-script-error-reported-in-javascript-in-chrome-and-firefox)
- [What the heck is "Script error"?](https://blog.sentry.io/2016/05/17/what-is-script-error)
- [Script Error: JavaScript Forensics](https://trackjs.com/blog/script-error-javascript-forensics/)

See also [Tracking scripts errors](Web#tracking-scripts-errors)

- [Capture and report JavaScript errors with window.onerror](https://blog.sentry.io/2016/01/04/client-javascript-reporting-window-onerror.html)
- [GlobalEventHandlers.onerror - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers/onerror)
- [Javascript global error handling - Stack Overflow](https://stackoverflow.com/questions/951791/javascript-global-error-handling/10556743#10556743)
- [Debug Rendering Problems | Search | Google Developers](https://developers.google.com/search/docs/guides/debug-rendering)
- [Sentry | Error Tracking Software — JavaScript, Python, PHP, Ruby, more](https://sentry.io/welcome/)

## Global resource error handler

Catch error, then send [beacon](#beacon)

```js
document.documentElement.addEventListener(
	"error",
	function handleErrorCapture (event){
		console.group("Resource Error event");
		console.log("Target:", event.target);
		console.log("Source:", event.target.src);
		console.groupEnd();
	},
	// https://dom.spec.whatwg.org/#introduction-to-dom-events
	// According to the DOM (Document Object Model) specification, the ERROR and
	// LOAD events for Images do not BUBBLE up through the DOM tree. As such, we
	// have to use the CAPTURE phase, which starts at the top of the DOM and
	// descends down into the DOM toward the target element.
	true
);
```

- [Tracking Image Error Event Using Event Delegation In JavaScript](https://www.bennadel.com/blog/3429-tracking-image-error-events-using-event-delegation-in-javascript.htm)

## Watch `iframe` content load

Some browsers (Chrome) don't dispatch load event for iframe contains attachment file (handled by the embedded PDF reader).

`Content-disposition: inline; filename="file.pdf"`

> The client algorithm:
>
> 1. Generate a random unique token.
> 2. Submit the download request, and include the token in a GET/POST field.
> 3. Show the "waiting" indicator.
> 4. Start a timer, and every second or so, look for a cookie named "filedl_" + token (or whatever you decide).
> 5. If the cookie exists, and its value matches the token, hide the "waiting" indicator and delete the cookie.
>
> The server algorithm:
>
> 1. Look for the GET/POST field in the request.
> 2. If it has a non-empty value, drop a cookie (e.g. "filedl_" + token), and set its value to anything (like "1").
> — https://stackoverflow.com/a/4168965/470117

Use `Transfer-Encoding: chunked` to serve the file and set cookie in trailer. **Shouldn't work because `Set-Cookie` is forbidden in trailer (and because some client don't read trailers)**. https://en.wikipedia.org/wiki/Chunked_transfer_encoding#Applicability.

- [Jake Opines : Events to Expect when Dynamically Loading iFrames in JavaScript](https://web.archive.org/web/20150318030620/http://www.atalasoft.com/cs/blogs/jake/archive/2009/06/18/events-to-expect-when-dynamically-loading-iframes-in-javascript.aspx)

## Clipboard API

Aka DataTransfer

`text/uri-list`, `text/plain`, `text/html`

```js
var pasteEvent = new ClipboardEvent("paste");
pasteEvent.clipboardData.items.add("My string", "text/plain");
document.dispatchEvent(pasteEvent);
```

- [html - Click button copy to clipboard using jQuery - Stack Overflow](https://stackoverflow.com/questions/22581345/click-button-copy-to-clipboard-using-jquery/22581382#22581382)

Require a condition: short-lived event handler for a user action, works only if the document is HTML (not SVG nor XML)

```js
// execCommand will not been executed if a frame or an iframe is focused
if(["IFRAME","FRAME"].includes(document.activeElement.tagName)){
	let focusable = document.createElement("span");
	focusable.tabIndex = -1;// focusable
	focusable.setAttribute("aria-hidden", "true");// will not be announced by AT
	focusable.style.position = "fixed";
	document.documentElement.appendChild(focusable);// don't use doc.body because in case of frame the body is the frameset and execCommand will not work
	focusable.focus();// force focus, but will not scroll into view, because it have fixed position
	focusable.remove();// remove focus, without force to scroll into view to an other element
}
let elementCopy = event => {
	document.removeEventListener("copy", elementCopy, true);// one time listener
	event.preventDefault();
	let clipboardData = event.clipboardData;
	clipboardData.clearData();
	clipboardData.setData("text/plain", "Hello, world!");
	clipboardData.setData("text/html", "<b>Hello, world!</b>");
	// Add any other clipboard data
	/*
	Alternative:
	let items = clipboardData.items;
	items.clear();
	items.add("Hello, world!", "text/plain");
	items.add("<b>Hello, world!</b>", "text/html");
	items.add(new File(["Rough Draft ...."], "Draft1.txt", {type: "text/plain"; lastModified: new Date(2013, 12, 5, 16, 23, 45, 600)}));// only WD yet, not implemented. See https://www.w3.org/TR/FileAPI/#file-constructor
	*/
};
document.addEventListener("copy", elementCopy, true);
document.execCommand("copy");// will dispatch copy event
```

- [DataTransferItemList.add() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/DataTransferItemList/add)
- [javascript - Copy image to clipboard from Chrome App (not Extension or Page) - Stack Overflow](https://stackoverflow.com/questions/35234958/copy-image-to-clipboard-from-chrome-app-not-extension-or-page)
- [javascript - Can one hack "paste image" support into a textarea in Firefox? - Stack Overflow](https://stackoverflow.com/questions/14151018/can-one-hack-paste-image-support-into-a-textarea-in-firefox/14423247) - (old workaround) Focus an contenteditable in past event listener, then wait (async) an img element with src base64 png will be added to the content. Use `clipboardData.items` instead
- [Canvas Image Copy / Paste Demo](https://codepen.io/tmrDevelops/details/YxGQaW)
- [487266 - Chrome doesn't expose all of the formats on the clipboard - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=487266#c5)

### Past file

```js
document.addEventListener("paste", event => {
	event.clipboardData.types;
	event.clipboardData.files;
	event.clipboardData.items;

	/*
	loop{
		// event.clipboardData.getData(item.type)
		if(item.kind != "file"){
			continue;//need an other implementation
		}
		let blob = item.getAsFile();
		if(!blob){
			continue;
		}

		let reader = new FileReader();
		reader.addEventListener("load", event => {
			console.log(event.target.result); // raw bytes
		});
		reader.readAsArrayBuffer(blob);
	}
	*/
})
```

### Update clipboard

When a text is selected and copied or cut

```js
document.addEventListener("copy", event => {
	event.preventDefault();
	let plainText = event.clipboardData.getData("text/plain") + "\n\nRead more at: " + document.URL;
	//let plainText =  window.getSelection() + "\n\nRead more at: " + document.URL;

	// Recommanded version:
	event.clipboardData.setData("text/plain", "Hello, world!");
	event.clipboardData.setData("text/html", "<b>Hello, world!</b>");

	// Alternative version 1 (data type "text" alias of "text/plain" and "url" alias of "text/uri-list" with only one URL):
	// (event.clipboardData || window.clipboardData/*IE*/).setData("Text", text);

	// Alternative version 2 (create a temporary element, select, copy and restore selection ranges):
	/*
	// Backup current ranges and remove it
	let selection = window.getSelection();
	let ranges = new Array(selection.rangeCount);
	for(let rangeIndex = 0, rangeIndex < selection.rangeCount; rangeIndex++){
		selectionRanges[rangeIndex] = selection.getRangeAt(rangeIndex)
	}
	selection.removeAllRanges();

	{
		// Create a new range with a new element
		let range = document.createRange();
		let node = document.createElement("p");
		document.body.appendChild(node);
		range.selectNode(node);
		selection.addRange(range);

		if(document.queryCommandSupported("copy")){
			let copied = false;
			try{
				copied = document.execCommand("copy");
			}catch(){}
			// not copied? fail
		}
	}

	// Restore original ranges
	selection.removeAllRanges();
	for(let range of ranges){
		selection.addRange(range);
	}
	*/
});
```

- https://github.com/NiklasGollenstede/es6lib/blob/bd5a3584dc7b4abc08b02c405bba0efe726374f8/dom.js#L177-L199
- [javascript - How to add extra info to copied web text - Stack Overflow](https://stackoverflow.com/questions/2026335/how-to-add-extra-info-to-copied-web-text)
- [Recommended Drag Types - Web developer guide | MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Recommended_Drag_Types)
- [copy - Event reference | MDN](https://developer.mozilla.org/en-US/docs/Web/Events/copy)
- [Cut and Copy Commands  |  Web  |  Google Developers](https://developers.google.com/web/updates/2015/04/cut-and-copy-commands)
- [timdown/rangy: A cross-browser JavaScript range and selection library.](https://github.com/timdown/rangy)

## `document.execCommand()`

Some `execCommand` require an element to be focused, but not work if it's a frame or an iframe

```js
// execCommand will not been executed if a frame or an iframe is focused
if(["IFRAME","FRAME"].includes(document.activeElement.tagName)){
	let focusable = document.createElement("span");
	focusable.tabIndex = -1;// focusable
	focusable.setAttribute("aria-hidden", "true");// will not be announced by AT
	focusable.style.position = "fixed";
	document.documentElement.appendChild(focusable);// don't use doc.body because in case of frame the body is the frameset and execCommand will not work
	focusable.focus();// force focus, but will not scroll into view, because it have fixed position
	focusable.remove();// remove focus, without force to scroll into view to an other element
}
let listener = event => {
	document.removeEventListener("copy", listener);// one time listener
	// Do whaterver you want. Exemple: in copy event, use event.clipboardData
};
document.addEventListener("copy", listener);
document.execCommand("copy");// will dispatch copy event
```

- [CodePen - Use execCommands to edit HTML content in your browser](http://codepen.io/netsi1964/full/QbLLGW/)

## History API

> Per spec, back() is asynchronous, but pushState() is synchronous.

- [Manipulating the browser history - Web developer guide | MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/API/DOM/Manipulating_the_browser_history)

- `history.replaceState(null, "", base + "/somehash")` and `document.location.replace(base + "#somehash")`
- `history.pushState("", base + "/somehash")` and `document.location.assign(base + "#somehash")`

Where `base` can be:

```js
let [base] = location.href.split("#", 1);
```

Or use `URL`:

```js
let url = (new URL("#somehash", location.href)).href;
```

...

```js
let hash = link.href.split("#").slice(1).join("#");
```

```js
let hash = link.hash.substr(1);
```

## Debounce function

Aka throttle, throttling, de-spam

For spammy event: resize, scroll, etc.

Note: de-bouncing is not the same as throttling

```js
// Example in a chat app (where the log is always scrolled to bottom) where the function scrollToEnd() is called after each new log entry is appended (but only if the log view is already at bottom before the message is appended)
// Use requestIdleCallback to debounce the request of scrolling
function scrollToEnd(){
	requestIdleCallback(() => {
		logView.scrollIntoView({
			behavior: 'smooth',
			block: 'end'
		});
	});
});
```

- [resize - Event reference | MDN](https://developer.mozilla.org/en-US/docs/Web/Events/resize#Examples)
- [Basic JavaScript Event Throttling by Amelia Bellamy-Royds on CodePen](https://codepen.io/AmeliaBR/post/basic-javascript-event-throttling)
- [Limit the frame-rate being targeted with requestAnimationFrame](https://gist.github.com/addyosmani/5434533)

Or

```js
/**
 * Returns a function, that, as long as it continues to be invoked, will not
 * be triggered. The function will be called after it stops being called for
 * N milliseconds.
 * @param {function} func
 * @param {number} wait
 * @param {boolean} [immediate] trigger the function on the leading edge, instead of the trailing
 * @see http://davidwalsh.name/javascript-debounce-function
 * @see http://en.wikipedia.org/wiki/Switch#Contact_bounce
 */
function debounce(func, wait, immediate) {
	var timeout;
	return function() {
		var context = this, args = arguments;
		var later = function() {
			timeout = null;
			if (!immediate) func.apply(context, args);
		};
		var callNow = immediate && !timeout;
		clearTimeout(timeout);
		timeout = setTimeout(later, wait);
		if (callNow) func.apply(context, args);
	};
}
```

```js
window.addEventListener("resize", function(event){console.log("scroll")}, false);
window.addEventListener("resize", debounce(function(event){console.log("scroll [debounced]")}), false);
```

```js
var rafID = 0;
window.addEventListener("resize", function(){
	if(rafID !== 0){
		return;
	}

	rafID = requestAnimationFrame(layout);
});
function layout(){
	rafID = 0;
	console.log("scroll [debounced]");
}
```

## Audio and sound effects

- [Audio Sprites (and fixes for iOS)](https://remysharp.com/2010/12/23/audio-sprites)
- [Overcoming iOS HTML5 audio limitations](http://www.ibm.com/developerworks/library/wa-ioshtml5/)
- [Solve Your Game Audio Problems on iOS and Android with Web Audio API | Code Theory](http://codetheory.in/solve-your-game-audio-problems-on-ios-and-android-with-web-audio-api/)
- [Playing with Pervasive Code: currentTime not working with the HTML5 Audio tag.. a solution!](http://pervasivecode.blogspot.fr/2012/09/currenttime-not-working-with-html5.html)
- [Making HTML5 audio actually work on mobile | Pupunzi](http://pupunzi.open-lab.com/2013/03/13/making-html5-audio-actually-work-on-mobile/)

## Resolution

Aka Device pixel density

prefer use media query, it's per screen, where `window.devicePixelRatio` is not (depends browser?)

- [Window.devicePixelRatio - Web API Interfaces | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/devicePixelRatio)
- [devicePixelRatio - QuirksBlog](http://www.quirksmode.org/blog/archives/2012/06/devicepixelrati.html) and [More about devicePixelRatio - QuirksBlog](http://www.quirksmode.org/blog/archives/2012/07/more_about_devi.html)
- [High DPI Images for Variable Pixel Densities - HTML5 Rocks](http://www.html5rocks.com/en/mobile/high-dpi/)

See also [Resolution](CSS#resolution)

## Partial AJAX load/upload

Using the HTTP Range header. Server should return 206 if range request is accepted or 200 if not.
Upload require XHR2 and `Content-Range` header (see [Art & Logic – » Ajax Upload Part II: XHR2 (and FileReader)](http://www.artandlogic.com/blog/2013/04/ajax-upload-part-ii-xhr2-and-filereader/))

- [ajax - Using the HTTP Range Header with a range specifier other than bytes? - Stack Overflow](https://stackoverflow.com/questions/1434647/using-the-http-range-header-with-a-range-specifier-other-than-bytes)
- [Javascript tail -f using XMLHttpRequest (Ajax) and Byte-serving (HTTP 1.1 Range)](http://www.davehennessey.com/computerjunk/javascript/tail-dash-f.html)
- [ASP.NET Web API and HTTP Byte Range Support - .NET Web Development and Tools Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/webdev/archive/2012/11/23/asp-net-web-api-and-http-byte-range-support.aspx), [Answer for: Need Ajax Code for downloading Large file from server to client pc - CodeProject](http://www.codeproject.com/Questions/575054/answer.aspx)
- Could not work on non HTTP protocols like `file://`: [733259 – jQuery and Headers with Content-Range Handling](https://bugzilla.mozilla.org/show_bug.cgi?id=733259)
- Not supported every where, but custom type can be used: [ajax - Using the HTTP Range Header with a range specifier other than bytes? - Stack Overflow](https://stackoverflow.com/questions/1434647/using-the-http-range-header-with-a-range-specifier-other-than-bytes)
- And have cache issues: [Issue 440904 - chromium - Extraneous 1 byte range requests issued prior to normal range request for interrupted request - An open-source project to help move the web forward. - Google Project Hosting](https://code.google.com/p/chromium/issues/detail?id=440904), [626027 – HTTP byte range requests are not cached](https://bugzilla.mozilla.org/show_bug.cgi?id=626027)
	[Workaround to prevent caching of byte range requests in Safari by pusherman · Pull Request #91 · gildas-lormeau/zip.js](https://github.com/gildas-lormeau/zip.js/pull/91)

## Release resource

- img set `src` to `about:blank`
- media (video or audio) remove `<source>`s and `src` attribute

## Test media autoplay or play without user interaction

```js
var video = document.createElement("video");
var src = document.createElement("source");
src.src = "data:video/webm;base64,GkXfo0AgQoaBAUL3gQFC8oEEQvOBCEKCQAR3ZWJtQoeBAkKFgQIYU4BnQI0VSalmQCgq17FAAw9CQE2AQAZ3aGFtbXlXQUAGd2hhbW15RIlACECPQAAAAAAAFlSua0AxrkAu14EBY8WBAZyBACK1nEADdW5khkAFVl9WUDglhohAA1ZQOIOBAeBABrCBCLqBCB9DtnVAIueBAKNAHIEAAIAwAQCdASoIAAgAAUAmJaQAA3AA/vz0AAA=";
src.type = "video/webm; codecs=vp8";
video.appendChild(src);
src = document.createElement("source");
src.src = "data:video/mp4;base64,AAAAHGZ0eXBpc29tAAACAGlzb21pc28ybXA0MQAAAAhmcmVlAAAAG21kYXQAAAGzABAHAAABthADAowdbb9/AAAC6W1vb3YAAABsbXZoZAAAAAB8JbCAfCWwgAAAA+gAAAAAAAEAAAEAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAIAAAIVdHJhawAAAFx0a2hkAAAAD3wlsIB8JbCAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAQAAAAAAIAAAACAAAAAABsW1kaWEAAAAgbWRoZAAAAAB8JbCAfCWwgAAAA+gAAAAAVcQAAAAAAC1oZGxyAAAAAAAAAAB2aWRlAAAAAAAAAAAAAAAAVmlkZW9IYW5kbGVyAAAAAVxtaW5mAAAAFHZtaGQAAAABAAAAAAAAAAAAAAAkZGluZgAAABxkcmVmAAAAAAAAAAEAAAAMdXJsIAAAAAEAAAEcc3RibAAAALhzdHNkAAAAAAAAAAEAAACobXA0dgAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAIAAgASAAAAEgAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABj//wAAAFJlc2RzAAAAAANEAAEABDwgEQAAAAADDUAAAAAABS0AAAGwAQAAAbWJEwAAAQAAAAEgAMSNiB9FAEQBFGMAAAGyTGF2YzUyLjg3LjQGAQIAAAAYc3R0cwAAAAAAAAABAAAAAQAAAAAAAAAcc3RzYwAAAAAAAAABAAAAAQAAAAEAAAABAAAAFHN0c3oAAAAAAAAAEwAAAAEAAAAUc3RjbwAAAAAAAAABAAAALAAAAGB1ZHRhAAAAWG1ldGEAAAAAAAAAIWhkbHIAAAAAAAAAAG1kaXJhcHBsAAAAAAAAAAAAAAAAK2lsc3QAAAAjqXRvbwAAABtkYXRhAAAAAQAAAABMYXZmNTIuNzguMw==";
src.type = "video/mp4; codecs=\"avc1.42E01E\"";//baseline H.264
video.appendChild(src);
//video.autoplay = true;//instead of video.play() you can test autoplay
video.style.cssText = "position:absolute;display:none;height:0;width:0";
document.body.appendChild(video);
video.load();
```

Then:

```js
video.play().catch(reason => {
	reason instanceof DOMException && reason.name == "NotAllowedError"// can't autoplay or play without user interaction
});
```

Or, if play promise is not supported:

```js
video.play();
video.paused == true// can't autoplay or play without user interaction
```

Finally (if promise supported, put this in the catch callback):

```js
video.pause();
document.body.removeChild(video);
video.innerHTML = "";
video.removeAttribute("src");
video = src = null;
```

## Check font load

Check font with font style loading

Note: embeded fonts using data URI are not immediatly available with Webkit

- [FontFaceSet.load() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/FontFaceSet/load)
- [WebfontLoader](https://github.com/typekit/webfontloader)
- [Detect loaded font](https://stackoverflow.com/questions/4383226/using-jquery-to-know-when-font-face-fonts-are-loaded)
- [How to detect a loaded stylesheet](https://stackoverflow.com/questions/17747616/webkit-dynamically-created-stylesheet-when-does-it-really-load)
- [Modernizr fontface detection](https://github.com/Modernizr/Modernizr/blob/master/feature-detects/css/fontface.js)
- [A Comprehensive Guide to Font Loading Strategies—zachleat.com](https://www.zachleat.com/web/comprehensive-webfonts/)

## Resize event

> put a video on DOM dispatch a `resize` event

- [video element put on dom dispatch a resize event](https://codepen.io/Seraf_NSS/pen/dyYmQxd?editors=1111)
- [resize - Event reference | MDN](https://developer.mozilla.org/en-US/docs/Web/Events/resize#Examples)

## Focus management

- [Managing focus in animated UI - ally.js](https://allyjs.io/tutorials/focusing-in-animated-ui.html)
- [Managing focus in SVG - ally.js](https://allyjs.io/tutorials/focusing-in-svg.html)
- https://github.com/medialize/ally.js/tree/master/src/query
- https://github.com/medialize/ally.js/tree/master/src/when

### Get focused element

`document.activeElement` and `document.hasFocus()`

- [Focus management in HTML - HTML (HyperText Markup Language) | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Focus_management_in_HTML)
- [HTML Standard - 6.4.6 Focus management APIs](https://html.spec.whatwg.org/#focus-management-apis)
- [javascript - How do I find out which DOM element has the focus? - Stack Overflow](https://stackoverflow.com/questions/497094/how-do-i-find-out-which-dom-element-has-the-focus/7821694#7821694)
- http://jsfiddle.net/mklement/72rTF/

## Exit fullscreen video on iOS

`videoElement.webkitExitFullscreen()` after `ended` and `paused` video's events

- [Controlling Media with JavaScript](https://developer.apple.com/library/safari/documentation/AudioVideo/Conceptual/Using_HTML5_Audio_Video/ControllingMediaWithJavaScript/ControllingMediaWithJavaScript.html#//apple_ref/doc/uid/TP40009523-CH3-SW13)

## Media states

Video or audio

Properties:

- paused: `media.paused` (`media.play()` was fired but the video could still be loading or playing)
- playing (really): `media.currentTime > 0 && !media.paused && !media.ended && !media.seeking && media.readyState >= media.HAVE_FUTURE_DATA;`

Events:

- Time change on media: `timeupdate` and `seeking`
- Update manual captions: `timeupdate`
- Display duration: `durationchange` and `loadedmetadata`
- Handle the media finishing: `ended`
- Check for buffer progress: `progress` and `playing`
- Handle native mute: `volumechange`
- Handle play/pause: `play`, `pause` and `ended`
- Loading: `waiting`, `canplay`, `seeked`
- Ready: `canplaythrough`, can `media.play()` (will work only if user interaction is not required)
- Playing or paused: `playing`, `pause`, `ended`
- Playing or paused (really): `playing`, `pause`, `ended`, `seeking`, `suspend` and `waiting`

- [Media events - Web developer guides | MDN](https://developer.mozilla.org/en/docs/Web/Guide/Events/Media_events)
- [Dev.Opera — Everything You Need to Know About HTML5 Video and Audio](https://dev.opera.com/articles/everything-you-need-to-know-html5-video-audio/)
- [javascript - How to tell if a \<video\> element is currently playing? - Stack Overflow](https://stackoverflow.com/questions/6877403/how-to-tell-if-a-video-element-is-currently-playing)

## Create SVG matrix

```js
document.createElementNS("http://www.w3.org/2000/svg", "svg").createSVGMatrix();
```

## Download generated data

Note: With blob or data URI, use `application/octet-stream` to force download.

Aka save file

```html
<a href="blob:..." download="filename.ext">Generated file</a><!-- a blob or a file: new File(["Hello"], "data.txt", {type: "plain/text"}) -->
```

`"data:application/octet-stream;base64," + btoa(data)` where `data`:

```js
let bytes = new Uint8Array(dataBytes);
let data = bytes.reduce((chars, byte) => (chars += String.fromCharCode(byte), chars), "");// as raw string
```

Not supported everywhere. Also blob URI not work on iOS, use data URI. Or use [service worker](#service-worker).

```js
let uri = "data:application/octet-stream;base64," + dataBase64;// could be a blob URI
let filename = "data.bin";
let link = document.createElement("a");
link.download = filename;
link.href = uri;
// link.type = mediatype;// Does this have any impact?
document.body.appendChild(link);// requireb by Firefox (not Chrome)
link.click();
link.remove();
```

```js
let msg = "Hello world!";
let blob = new File([msg], "hello.txt", {"type": "application/octet-stream"});
let link = document.createElement("a");
link.href = URL.createObjectURL(blob);
window.location.href = link;
```

- [Can I use... Support tables for HTML5, CSS3, etc](http://caniuse.com/#feat=download)
- https://github.com/eligrey/FileSaver.js
- [Using HTML5/Javascript to generate and save a file - Stack Overflow](https://stackoverflow.com/questions/2897619/using-html5-javascript-to-generate-and-save-a-file)

And drag and drop to desktop

- blob
- `navigator.msSaveOrOpenBlob`: [msSaveOrOpenBlob method (Internet Explorer)](https://msdn.microsoft.com/en-us/library/hh772332(v=vs.85).aspx)
- `X-Download-Options: noopen`
- dataTransfert `downloadURL` type. Chrome
- `HTMLAnchorElement.download`: [<a> - HTML | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#attr-download)
- open a new window/tab
- https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/draggable

```css
[draggable='true'] {
	-khtml-user-drag: element;
	-webkit-user-drag: element;
	-khtml-user-select: none;
	-moz-user-select: none;
	-webkit-user-select: none;
	user-select: none;
}
```

```js
drag.addEventListener("dragstart", function(e) {
	var dt = e.dataTransfer,
	// IE doesn't like anything other than "Text"
	type = /*@cc_on!@*/0 ? "Text" : "text/plain";
	dt.setData( type, "Some data to set" );
}, false);
```

```js
drop.addEventListener("drop", function(e) {
	var dt = e.dataTransfer,
	// IE doesn't like anything other than "Text"
	data = dt.getData( /*@cc_on!@*/0 ?
	"Text" : "text/plain" );
	alert(data);
}, false);
```

## Download multiple files with one interaction

Note: Chome can display the message "This site is attempting to download multiple files"

Solution 1:

1. Create one link per download file
2. Set for each the `href` attribute to the URI of the resource (HTTP, blob or data URI)
3. Set for each the `download` attribute to the filename
4. Trigger a click event (via `.click()` or via `.dispatchEvent(new MouseEvent("click"))`) (advice: add ~500ms delay between each click)
5. (optional) Remove the link (advice: add ~500ms delay before remove generated links)

```js
let link = document.createElement('a');
let list = ["file1.txt", "file2.txt", "file3.txt"];
let i = 1;
document.body.appendChild(link);
for(let file of list){
	link.href = file;
	link.setAttribute("download", file);
	link.click();//link.dispatchEvent(new MouseEvent("click"));
}
link.remove();
```

Solution 2:

1. Create one iframe per download file
2. Set the `src` attribute to the URI of the resource

Note: a given filename can't be defined and file can't be forced downloaded unless the server send the resource with proper HTTP headers (`Content-Type: octet/stream` or `Content-Disposition: attachment; filename=foo.pdf`)

Solution 3:

The server need to support `GET /file.ext?` or `POST /file.ext`

1. Create a form
2. set `action` to the first file
3. set `target` to `_blank`
4. set `method` to `get` or `post` according the server support (get will append `?` to the requested URL)
5. submit form `form.submit()`
6. do it (reuse the same form) for all other files

- [http - Download multiple files with a single action - Stack Overflow](https://stackoverflow.com/questions/2339440/download-multiple-files-with-a-single-action)
- [How to overcome “This site is attempting to download multiple files” dialog in android chrome | Urva TechLabs](http://blog.urvatechlabs.com/how-to-overcome-this-site-is-attempting-to-download-multiple-files-dialog-in-android-chrome/)

## Developper jokes

Use greek question mark `;` (U+037E) instead of semicolon `;`
Use zero-width chars: U+200d, U+feff, U+200c, U+200b:

```
<meta charset="UTF-8"><script>q="﻿‌‍​﻿‌​​﻿‌​‌﻿​‍​﻿​﻿‍﻿​‍‌﻿​﻿﻿﻿‌‍​﻿​﻿‍﻿‌​​﻿​‍‌﻿﻿​​‍​​﻿‍‌﻿​‍‍﻿﻿﻿﻿﻿​‍​​﻿﻿﻿​‍‍‌﻿​‍​​‍﻿‌​﻿﻿‍​‍﻿‌‍﻿‍﻿​​‍‍﻿​﻿‍​﻿﻿‌﻿‌‍‌​﻿‍​‌‍﻿​​​‍​​‍‍﻿﻿​﻿​‍﻿‍‍﻿​‍‌‍​‍‌‍‌‍​‌​﻿‌​‍‍​​﻿﻿​‍﻿‍‍‌​‍​‌​﻿​‍​‍‍﻿​﻿​​‍‍﻿‍‌﻿﻿‍﻿﻿‌​‍‍​‌​﻿‌‌﻿‍‌‌​‍​​﻿‍​﻿‍‍‌‌﻿‍﻿‍‍﻿​‌​﻿​﻿​‍‍﻿​‍﻿‍‌‍‍​‌﻿​﻿​‍‌‌​‍​​﻿‍‌‌‍﻿​‍﻿﻿‍﻿​‍‌‌​﻿‌‌‌‍‌‌﻿‍‌‌‌‍​﻿﻿‍‌​​‍​‍‌‍‌‌﻿‍‌﻿‌‍​‍​﻿​​﻿‍​‌​﻿​‍﻿‍‌‌​‍‍﻿‌‍﻿‍‍﻿​‍‍﻿‍‌​﻿​‍​﻿‌﻿﻿﻿‍‌﻿‍‌﻿‍‍‌‌‍﻿​﻿​‍‌​‍‍​﻿‍‍‌‌﻿‍‌‌﻿﻿​​﻿‍​‌​﻿‌‍​‍​​﻿﻿﻿‍‌‍‌​‍﻿‌​‍‍‌‌​‍​‍﻿‍​‍﻿‍﻿﻿‌﻿‌‍​﻿﻿‌​﻿‌‍​﻿﻿​﻿﻿﻿‌​﻿‌‍​﻿﻿​﻿‍‌‌‍﻿﻿‍‌‍‌‌​‍​‍﻿‍​‍﻿‍‌‌﻿‍‌‌﻿‍‌‌‍‍﻿﻿‌‍‌‍‍‍‌​​‍‌​​‍‌‍‍﻿‌‍‌﻿​‌﻿‍‌‍‍﻿‍‍‍‍﻿‍​‍‍​​‍﻿﻿​﻿﻿​‍‍‌﻿​‍​‌​‍‍﻿﻿﻿‌‍​‍‍﻿‍‍​​﻿﻿‌﻿‌﻿​﻿﻿﻿‌​‌﻿‌‍​﻿​﻿‍﻿‌‌﻿﻿﻿‍‍‍‌‌‍‍‌‌﻿‍‌‍‍﻿​‌​‍‍﻿﻿‍﻿​﻿﻿​‍‌‍‍﻿​﻿‌‍​﻿﻿‍‍‍﻿​﻿﻿​‍‌﻿​﻿﻿﻿‌‍​﻿​﻿‍﻿‌​​﻿​‍‌‍‌‍‌‍‌‌​‍‍‍‌‍﻿​‌‍‍‌‍‍​​​‍﻿‌﻿‍​‌​‍‍﻿﻿﻿‌​﻿﻿‌‍﻿﻿​‍‍‍‍﻿‌﻿﻿​​‍​﻿﻿‍‌​‍‍​﻿‌‍​﻿﻿‍​‍‌‍​﻿​‍​‌﻿‍‌​‍﻿﻿​​‍​﻿‍‍‌​‍﻿﻿​​‍​‍​‍﻿﻿‌‍‍﻿﻿‍﻿‍﻿‍‍﻿​‍﻿‍‌‍‍﻿﻿﻿﻿‍﻿‍﻿​﻿﻿​‍‌‍‍‌​‍​‌​﻿‌‌﻿‍‌‌​‍‌‌​‍‌‌﻿﻿​‌​‍‍﻿﻿﻿‌‍‌‍‍﻿​‍​‍‍‍​‍‍‍​‍‍‍​‍‍‍‌‍‌‍‌‌​‍﻿​﻿﻿​‍‌﻿‍﻿​‍‌‌﻿‍‌​‌﻿​﻿‍﻿‌​​﻿﻿‍​‍‍‌﻿‍‌‌‍‍​﻿‍‍﻿﻿‌‍﻿‍﻿‍‌‌​‍​​﻿﻿‌‍‌‍‌​‌﻿​​‍‍‌‌‍﻿‌‍‌‍‍‌​‍‌​﻿‍​﻿‍‍﻿﻿‌﻿​​﻿﻿‌‍‍‍‌‌‍‍‍﻿﻿‍‍​‌‍﻿‍﻿‍​​﻿‍﻿‍﻿‍‌‍﻿‍‌‍‌‍‌‌​﻿‌‌‌‍‌‌﻿‍‌​‌﻿‌‌‌﻿‌​​‍﻿​‌‍‌‌‍﻿‌​﻿﻿‌‍﻿﻿​‍‍﻿﻿‌​﻿‌‌‌﻿﻿​﻿‍﻿﻿‌﻿​​﻿‍‍‍‌﻿‌​​﻿‍​﻿‍‍‌‍‍​​​‍﻿‌﻿‍​​﻿﻿﻿﻿​‍‌‍﻿‍‌‍​‍​​​﻿‌‌‌﻿‌​​‍﻿​‌‍‌‌‍‍﻿‍﻿‍﻿﻿‌﻿​​﻿‍​‌​‍﻿‌‌﻿​﻿​﻿‍​‌‍﻿﻿﻿‍‌‌‍﻿﻿​‍‍‌﻿​‍​​‍﻿﻿‌‌﻿‌​﻿﻿‌​‍‍‍‍﻿﻿​​‌‍﻿​﻿﻿​‌﻿‍﻿​‍‍​​‌‍﻿‍‍﻿‌‍‌﻿﻿‌﻿﻿​‌﻿﻿​‌​﻿‌﻿‌﻿‌​​‍‌﻿‍‍‌​﻿﻿‌﻿‌﻿‌‍﻿﻿‌​﻿﻿‌‌﻿﻿‌​‍﻿​‌﻿‍​‌‌﻿﻿﻿‌﻿﻿​‌﻿‌﻿‍﻿‌‍﻿﻿‌​‌﻿‌‍﻿‍‌​‍﻿‍‍﻿﻿‍​‌﻿‌‍﻿﻿‌​‍‍‌​‍﻿‍‌‍﻿‌﻿﻿﻿‌​‍﻿​﻿‌﻿‍​‍﻿‌‌﻿﻿‌‍​﻿‌‍﻿‍‌​‍﻿​‍​﻿‌‍﻿﻿‌​‌﻿​‍​‍‌​﻿﻿​‍​﻿‌﻿﻿﻿‍​‌﻿‌﻿‌‍​‌​﻿​​﻿‍﻿‍‍‍‍‍​﻿​‌​﻿‌﻿‍﻿‌‌﻿﻿​‍​﻿​‍‍﻿‌​‍﻿‌‍﻿﻿​‌﻿‍​‌‌﻿‌‍‌﻿‌​‍﻿‌​​﻿‌‍​﻿‌‌​‍​‌​﻿​﻿​﻿‌‌﻿﻿‌﻿‍﻿​﻿‍﻿‌‌‍‍​‌‌‍​‌﻿‍​‍‍‍‌﻿﻿‍​‌​﻿‌‌‍﻿‌﻿﻿﻿‌‌﻿﻿‌﻿​﻿﻿‌‌‍​‌‌‍​‍‌‍​‍‍‍​‍‍﻿​‍‍﻿​‌‍‍​‌​﻿​​﻿‍﻿‍‍‍‍​​‍﻿​﻿﻿​‌﻿‍﻿​‍‍‍‍﻿﻿‌​﻿﻿‍​‍﻿‌‍﻿‍‌‍‍﻿﻿‌‌﻿​﻿‍﻿​‍‍‍‌​﻿﻿‌﻿﻿﻿​‍﻿﻿​﻿﻿﻿‌‌﻿﻿​﻿‌‍‍﻿​﻿‍‍​﻿﻿‍‍‍﻿﻿﻿‍‌﻿‍‍‌​﻿﻿﻿﻿‍﻿​‌﻿﻿​‍‍﻿‌﻿﻿‍‌‍‌‍‌‍‍﻿‌‍​﻿﻿‍‍‍﻿﻿﻿‍‌﻿‍‍‍﻿​‍﻿﻿﻿﻿​‌‍﻿​﻿‍‍‌​​﻿﻿‌‌﻿‌​﻿﻿‌​‍‍​‌​‍﻿​​‍​​﻿﻿‌‌﻿﻿​‍​﻿‌​​‍‌​﻿‍​‌‍‍​‌‍‍​﻿﻿‍​‌﻿‍‌​﻿‍​‍﻿‍‌‍‌‍‍‍﻿﻿​﻿‍﻿‌‌﻿﻿​﻿‍‍﻿​‍‍﻿﻿‍‍‍​​﻿​﻿‍﻿‌‌﻿﻿​﻿‍‍﻿​‍‍‍‍﻿‍‌​​﻿​​‌﻿‌‍‌﻿﻿‌﻿﻿​‌﻿‍‍‍﻿﻿‌‌‍‍​‍﻿‍﻿﻿‍‍‌‍‍‍‌​﻿‍‌‍‍﻿‍‍​‍‍﻿‍‍‌‍‍﻿‌﻿﻿﻿​﻿‌﻿﻿​‌﻿​‌﻿‍‌‍‍﻿‍‌‌﻿‌‍﻿﻿​﻿‌﻿‌‍﻿﻿​‌‌﻿﻿‌‍﻿‌​​‍‌‍‍﻿​‍​﻿‍﻿‍﻿‌‍​‍﻿‌‍﻿‌‍​﻿﻿‌﻿‍﻿‌‍﻿‌​‍﻿‌​​﻿‌​​﻿‌‌​‍﻿​‌﻿‌﻿​﻿﻿‌‍﻿‌‌‍‍﻿‌‍﻿​‍​﻿‌‍﻿﻿‌​﻿﻿‌﻿﻿‍‌​‌‍‌​‌‍‌​‌‍‍​​﻿‌‌‍‍​‍﻿﻿‍﻿‌‍​​‍﻿‌‌﻿‍​​‌﻿‌‍‌﻿​‌﻿‍‌‍‍﻿‌​﻿﻿‌‌﻿﻿‌‌‍﻿‌‌﻿‍‌‍‍‍‌﻿‌﻿‌​‍﻿​﻿‍‍​‌​﻿​‍​﻿‌‍​﻿‌‌‍﻿‌‌﻿﻿﻿​‌﻿‌​‍﻿‌​﻿‍‌‍‍﻿‌‍﻿﻿​﻿‍‍‌‍‍﻿​﻿﻿﻿​‍​﻿﻿​‌﻿​‍​‍‌‍‍﻿‌﻿‍﻿‌​​﻿​﻿‍‍‌‍‍﻿​‍​﻿‍﻿‍﻿‌‍​﻿‌﻿﻿﻿‌‍‍﻿‌﻿​‍﻿‌‍﻿‌﻿‍﻿‌​​﻿​﻿‍‍‌‍‍﻿‌​‌﻿‍​‍‍‌﻿‌﻿‌﻿​﻿​﻿‍‍​‌​‍‌​‍‍‌‍‍‍​​‍﻿‌‍﻿‍‌‍‍﻿‌‌‍﻿​‍‌﻿‌﻿﻿﻿‌﻿‌‍‍﻿​﻿﻿‌‌﻿​﻿‍﻿​‍‍‍​‌‌‍‌​​‍‌​​﻿​﻿‍﻿​﻿​﻿‌‌﻿﻿​﻿‍‍﻿﻿﻿﻿​‍‌‍‌​‌﻿‌‍​﻿‌​​﻿‌​﻿‍‌​​‍﻿‍​﻿​​​﻿‍‍‍‍﻿‍​‍‍​​﻿‌‍﻿‍​​‌‍‍​​﻿‌‌﻿‍​​‌‍‍​​﻿​‍‍﻿‍﻿‌﻿‍‌﻿﻿‌​‌‍‌‍‍﻿‌﻿‌﻿‌‍﻿﻿‌‍​﻿​﻿‍‍‌​‍‍‌‍‍﻿‌​​﻿‌﻿‌‍‌‍‍﻿‌‍​﻿‍﻿‍﻿​‍​‍﻿‌‍﻿​﻿​‍﻿‌‍﻿‍‌​‍﻿‌‍﻿​﻿﻿﻿​‍​‍﻿​‌﻿‌﻿​‍‌‍‍﻿​‍​﻿‌​​﻿‌​﻿‍﻿‌‍﻿﻿﻿﻿﻿‌​‌﻿‌‌﻿﻿‌‍​﻿﻿‌﻿‍﻿‌‍﻿​﻿‍﻿‍​‌﻿‌‍​﻿‌‌​﻿​‍​﻿﻿‌‍﻿‌​​‍‌‍‍﻿​‍‍﻿​﻿﻿﻿‌​‍﻿‌​‍‍‌‍‍﻿‌​​﻿‌﻿‌﻿﻿‌‍﻿‌‌‍﻿‌‌﻿﻿​‍​‍‌‍‍‍﻿​﻿﻿​﻿﻿‍‌﻿‍‍‌‍‍‍​‌‌‍‌‌﻿‍‍​​﻿​‍‍﻿‍﻿‌﻿​‌‌‍﻿‌​‍﻿​‌‍‍‌‍﻿​​​﻿‌‍﻿‍﻿​‍﻿​‍‌﻿​﻿‍‍‌‌‍‍​﻿‍‍​‍‌‍﻿﻿‌‍‌​​‍‌​​‍‍‌‍‍‌‍‍﻿​‌﻿﻿‍﻿‍‍‌‍‍﻿‍‌‌﻿﻿‍​‍‌‍‍﻿‌‌‍﻿﻿​‌﻿‌﻿﻿‍‍​​‍‍‍​‍‍‍﻿‍﻿​‌‍‍‌‍‍‌‍‍﻿‌‌﻿﻿‌﻿‍‍‍﻿​﻿‌﻿​﻿‌​​‍‌‍‌﻿﻿‌‍﻿​‌﻿﻿​‍‍﻿‌﻿﻿‍‍﻿​﻿‌‍‌﻿‍​﻿﻿​﻿‍﻿﻿‍‍‍‌‍‌‍‌‍‍‍﻿‌﻿‍‍﻿​﻿‍‍​‍‍﻿‍‍‌‍‌﻿‍﻿‌﻿‍​​﻿‍​﻿‍‍‌‍‍﻿‌​﻿‌​​﻿‍​﻿‍‍‌‍﻿​​​‍‍​​‍‍‍​‍​​‌﻿﻿​‍‍‌﻿​‍﻿﻿‌‍‍‍‌﻿‌﻿​﻿‌​​‍​​​﻿﻿‍‍﻿‌‍​﻿‌​‍﻿‌‌﻿﻿‌‍​﻿‌‌​‍​​﻿﻿‌‍​‍‍﻿‍‍​‌​﻿‌‍​‍‍﻿‍‍‌‌‍‍﻿﻿‌‍‍‍﻿‍​​‌‍﻿‍‍‍​​‍‍‍‍‌‍﻿‌‌﻿‌﻿​﻿‍​‍﻿‍﻿﻿‍﻿​‍﻿‌​﻿﻿‌﻿﻿‍‌﻿‍﻿‍‍‌﻿​‌﻿﻿‍‌﻿﻿‌﻿‍‍‌‌‍‍‌‍‌‍‍‍​‍﻿﻿﻿﻿​‌‍﻿​﻿‍﻿‍‌​﻿‌﻿﻿﻿‌‍﻿‍‍﻿‍﻿‌​​﻿‌​﻿﻿​‍‍‍﻿‍﻿﻿​‍​‍‍﻿﻿﻿​﻿‌﻿‍‌​‍‌‍‍‍‍﻿‌‍​​﻿﻿﻿‍​‍‍‌﻿‍‌​‌﻿‌﻿‌﻿​‍‌﻿‌​​﻿‌​﻿﻿‍‍​‍‍​‍‍‌‌‍‍‍﻿​‍​​﻿‍‌‍‌‍‍‌‍﻿​‍‍﻿‍​﻿‍‍‌﻿﻿​﻿‍﻿​‍‌‍﻿​‌﻿‌﻿​‍‍‌​‍‌​‌‍﻿​‍﻿‌​‌﻿‌﻿​﻿​﻿‍﻿‌‌‍‍‍​‍﻿‌‌‍﻿‍‌​﻿‍‍​﻿﻿‌﻿﻿‌﻿﻿‍‍​‌﻿‌‌‌‍​​﻿‍​‍‍‍​‌​﻿‌‌‌‍​​‍‍​﻿‍‍​‌​﻿‌‌‌‍‌‌​‍‌‌​‍‌‌﻿﻿​‌​‍‍​​‍​​‍‍‌​​‍﻿‍‍﻿﻿​‍﻿﻿​‍﻿‌​‌‍﻿‍﻿﻿​‍‌﻿‌﻿﻿﻿​‍​‍﻿‍‌‍‌‍‌‍​‌​﻿‌‍‍‍‌‌‍‍﻿‍​﻿‌​﻿﻿‌‌﻿﻿‌‌‍﻿‌‌﻿‍​﻿‍‍​‍‌‍﻿﻿‍‍​​‌﻿﻿‍​﻿‌​﻿﻿‌‍﻿﻿‌​‍‍﻿​‍‍﻿​﻿﻿‍‌‌﻿﻿‍​‍﻿﻿﻿﻿​﻿‍﻿‌﻿﻿‍﻿﻿‌‍‌‌﻿‍​‌​‍﻿﻿​﻿​‍​﻿‌‍​﻿​‍‌﻿﻿​‍‍‌﻿​‍‌‌​﻿﻿​‍‍‌﻿​﻿‌‌﻿﻿​‍‍﻿​﻿‍‍​​‌‍﻿‌‍﻿‌﻿﻿‍‌‍‍‍﻿‌﻿﻿​﻿‌﻿‌‍﻿﻿‌​‍﻿​﻿﻿﻿‌﻿﻿‍﻿‌‌﻿‌﻿‍﻿‌​​﻿‌‍​﻿​﻿﻿﻿‌​﻿﻿‌﻿﻿‍‌﻿‍‍‌​‌‍﻿‌​‍​‌‌‍‍​​﻿​‍‍‍‍‍﻿‍‍‍​‍‌‍‍﻿‌‌﻿﻿‌﻿‍‍‍﻿​‍﻿​‍﻿‌​‍﻿‌﻿﻿‍﻿​﻿﻿​‍​﻿​﻿‍‍﻿​‌﻿‌‌﻿﻿‌​‌‍﻿​​‍‌‍‍﻿‌‍​﻿‌‌‍﻿‍‌​﻿​‍​﻿‍​‍‍‌‍﻿‍‌​‌﻿​‍​﻿​‍‍﻿‌​‍﻿‌‌﻿﻿​﻿‍‍‌‌‍‍‌‍‌‍‌﻿‍﻿‌​‌﻿​﻿‍‍​​​‍‌‍‌‍‌‌﻿‍‌​‌﻿‍﻿‍﻿‌​​﻿​﻿﻿﻿​‍‌﻿‍﻿‌‍‍‍﻿﻿​‍‍‍​​‌﻿‍﻿​‍‌​‌﻿‌‍​‍‍​‍﻿‍‍﻿﻿​﻿‍‍‌‌‍﻿‌‌﻿﻿‍‌​﻿‌‍﻿﻿​‍‌﻿‍​‍﻿‌﻿﻿﻿​﻿‍﻿‍​﻿﻿​﻿﻿﻿​﻿‍﻿‍​‌﻿​‍‌﻿‌‌﻿﻿﻿‍‍﻿‌​​﻿‌​‌﻿﻿‍﻿﻿‌‌﻿‍​​﻿‍​‍‍‍​‌​﻿‌‌﻿‍​​‍﻿﻿‍‌﻿​‍﻿﻿﻿‌​﻿​‍​﻿﻿​﻿‍‌‌‍﻿‌​‍﻿﻿﻿​‍﻿﻿﻿﻿‌​﻿﻿​‍‍﻿‌​‍﻿‌‍﻿‍﻿﻿﻿﻿﻿‌‍‍‌‍‍﻿​﻿‍﻿﻿‌﻿﻿‌​​﻿‌﻿‍﻿﻿‌‌﻿‌‌‍﻿​﻿‍﻿﻿​‌﻿‌﻿﻿﻿​‍‌﻿﻿​​‍​‌‍‍​‍‌‍​‍‍﻿‌‍‍﻿‌﻿‌﻿‌​​﻿​‍‌﻿​‌‌﻿﻿‍​﻿‌‍​﻿‍​‌﻿​‍‍﻿​﻿‍﻿​​‍﻿​‍​﻿​﻿﻿﻿‌‍‌﻿​‍​‍‍‌﻿﻿​​‌﻿‌‌‍﻿‌﻿﻿﻿‌‍﻿﻿‌﻿‍‍‍‍﻿﻿​​​‍‌‍‌‍​​‌‍‌﻿​‍​‌​﻿‌﻿‌﻿‌​​﻿​‍‌‍‌‌‍﻿﻿‌﻿‍‌‍‍﻿‌‌﻿﻿‌​‌‍‌‍‍‍‌﻿‍‍​​﻿‍‌﻿​﻿​​​﻿​​‌﻿​​‍﻿​‌‌﻿‌‍‍﻿﻿​​﻿﻿​‌﻿﻿‌‌﻿﻿‌﻿﻿﻿‌‍﻿﻿﻿​﻿﻿‍‌﻿﻿‍﻿﻿﻿‍‍﻿‍​‌﻿‍​﻿﻿‍​‍﻿‍‌​﻿‍﻿​﻿‍﻿‌﻿‍﻿‍‍​​​‍‌﻿‍‍‌‍﻿‍﻿​​‍﻿​‌‍﻿​﻿‍﻿​‍‍﻿‌​‍﻿‌‌‍﻿‌﻿‍﻿‌‍‍﻿﻿​‍﻿﻿‌‍﻿﻿﻿‍﻿﻿‍‍﻿‍​‍﻿‍‌‍﻿‍﻿‍﻿‍‍‍‍​​‍‍​‌‍‍​‍‍‍‌​‍‍‌﻿‍‍‌‍‍‍﻿​‍‍﻿‌‍‍﻿﻿‍‍﻿‍‍‍‍​‍‍‍‌‍‍‍﻿‍‌﻿​‍‌‌﻿﻿​﻿​﻿‌‌﻿﻿​﻿‍﻿‌‌‍‍‌‌‍﻿﻿​​‍‌​‌﻿​‍​﻿​‍‍﻿‌​‍﻿‌‌﻿﻿​﻿‍‍‌‌‍‍‌﻿‍﻿﻿‌​﻿﻿‌﻿﻿﻿​﻿‍‌‌﻿‍‌‌﻿﻿﻿​​‍​​﻿﻿‌‌‌﻿‌​​﻿‌‌﻿﻿‌​‌‍‌‌‍﻿​‍‍﻿‌​​﻿​‍‍‍‌‌‍‍‌‌﻿‍‌‌﻿‍​‌​﻿‌﻿﻿﻿​﻿‌﻿‌‍﻿﻿‌​‍‍‌‌‍﻿﻿​​‍‌‌﻿";l=q.length;s="substring";for(i=0;i<l;i+=4)
{w="";for(j=0;j<4;j++){w+=(q.charCodeAt(i+j)*5/2)&3};q+=String.fromCharCode(
parseInt(w,4))};c=q[s](l,l+11);c[c][c](q[s](l+11))(); // by @mihi42</script>
```

From [SmallestJS](http://schierlm.users.sourceforge.net/smallestjs.html)

Use Unicode Roman Numerals: ⅰ, ⅴ, ⅹ, ⅼ, ⅽ, ⅾ, ⅿ... (not to be confused with i, v, x, l, c, d, m)

See [Obfuscation (code)](Security#obfuscation-code))

## Listen user page navigation

```js
window.addEventListener("beforeunload", event => console.log(event));// dispatched when the user request a page navigation (link, history, form, etc.)
window.addEventListener("unload", event => console.log(event));// dispatched when the document is unloaded juste before the new one appears
```

`setTimeout` for 100ms after `beforeunload` to be sure the user doesn't cancel the unload. **TODO** make a POC

Use `event.returnValue = "some message"` (1024 chars max) or `event.preventDefault()` in `beforeunload` handler to allow the user to cancel the page navigation. Usefull if a input state or any other data has not been saved.

Sometimes, force repaint can be necessary (`document.body.offsetWidth;`) if classes changes are not visible after clicking on a link

You can use a [beacon](#beacon) to log it.

- [HTML Standard](https://html.spec.whatwg.org/#prompt-to-unload-a-document)

## Bytes

### Use a different TypedArray

```js
new SomeTypedArray(typedarray.buffer, typedarray.byteOffset, Math.floor(typedarray.byteLength / SomeTypedArray.BYTES_PER_ELEMENT))
new DataView(typedarray.buffer, typedarray.byteOffset, typedarray.byteLength)
```

**Do not use** `new SomeTypedArray(typedarray)`, **only values will be copied (doesn't use the same buffer)**. Example: if the typed array is `Uint8Array[0x01, 0x02, 0x03, 0x04]` and use `Uint32Array`, the result will be `Uint32Array[0x01, 0x02, 0x03, 0x04]` not `Uint32Array[0x01020304]`
**Be carefull with [endianess](#typedarray-endianness)

### Use `StringView` to read/write strings in `ArrayBuffer`

- [StringView - Mozilla | MDN](https://developer.mozilla.org/en-US/Add-ons/Code_snippets/StringView)

### TypedArray endianness

**`TypedArray` where `BYTES_PER_ELEMENT > 1` (> 8 bits) use the host endianness. Use `DataView` instead (to use big endian).**

Intel / x86 cpu are little endian. But files format, or network data are fixed and often use big endian.

```js
const isLittleEndian = new Uint16Array(new Uint8Array([1, 0]).buffer)[0] === 1;
```

- [Typed Arrays in ECMAScript 6](http://www.2ality.com/2015/09/typed-arrays.html#endianness)
- [Javascript Typed Arrays and Endianness - Stack Overflow](https://stackoverflow.com/questions/7869752/javascript-typed-arrays-and-endianness)
- https://github.com/jDataView/jDataView

Use `DataView` (by default use big endian / network byte order) to read received data / files or to send data and `TypedArray` (use platform's endianess) for internal use (memory, Canvas2D ImageData or WebGL)

- [TypedArray or DataView: Understanding byte order ★ Mozilla Hacks – the Web developer blog](https://hacks.mozilla.org/2017/01/typedarray-or-dataview-understanding-byte-order/)

### Uint8Array vs Uint8ClampedArray

`Uint8ClampedArray` assign a value: `value = Math.min(Math.max(Math.round(value), 0), 255)`
`Uint8Array` assign a value: `value = value & 0xff` (lowest 8 bits)

### Store bytes in JS source

Aka embed binary data

#### Store bytes in JS source as unicode string

Use UTF-8 encoding (natively supported by JS, use UTF-16, 16 bits in memory to store on char) to encode special chars code 0 >= n >= 127 (0b01111111, 0x7F). Use 2 bytes plus escape special chars (newline, carriage return, `\` and `"` or `'`)

The compress ratio is between 1:1 and 2:1

```js
let buffer = (new Uint8Array(256)).fill(0).map((i, y) => y).buffer;//Uint8Array 0 to 255
```

To generate the corresponding code:

```js
let stringDelimiter = "\"";//"'"// can measure how many " ' or \r\n the string contains
let stringDelimiterCharCode = stringDelimiter.charCodeAt(0);
let multilineString = stringDelimiter != "\"" && stringDelimiter != "\'";
let escapedString = (new Uint8Array(buffer)).reduce((result, charCode) => {
	let char = String.fromCharCode(charCode);
	return result
		+ (
			char == stringDelimiter ? "\\" + stringDelimiter
			: !multilineString && char == "\n" ? "\\n"
			: !multilineString && char == "\r" ? "\\r"
			: char == "\\" ? "\\\\"
			: multilineString && char == "$" ? "\\" + char
			: char
		);
}, "");
console.log(`Array.prototype.reduce.call(${stringDelimiter}${escapedString}${stringDelimiter}, (result, value, index) => (result[index] = value.charCodeAt(0), result), new Uint8Array(${buffer.byteLength})).buffer`);
```

Note: It's limited to 2<sup>53</sup>-1 bytes that could be stored. It could be limited by the heap max size (see `window.performance.memory.jsHeapSizeLimit`)

> The String type is the set of all ordered sequences of zero or more 16-bit unsigned integer values (“elements”) up to a maximum length of 2<sup>53</sup>-1 elements
>
> — [ECMAScript® 2016 Language Specification](http://www.ecma-international.org/ecma-262/7.0/index.html#sec-ecmascript-language-types-string-type)

#### Store bytes in JS source as hexadecimal

Aka hexastring to binary data

The ratio is 2:1 bytes

```js
var data = "78da93e0e6b4d35f79d292d5c436c7b286d1daeedeb5684619658f1faf99";// must data.length % 2 == 0

// Encode
bytes.reduce((result, byte) => (result += byte.toString(16).padStart(2, "0"), result), "");

let bytes = new Uint8Array(data.length / 2);
for(let i = 0, j = 0; i < data.length; i += 2, j++){
	 bytes[j] = parseInt(data.substr(i, 2), 16)
}

let bytes = new DataView(new ArrayBuffer());
let i;
let j = bytes.byteOffset;
// Write 4 bytes
for(i = 0; i < data.length - (data.length % 8); i += 8, j += 4){
	bytes.setUint32(j, parseInt(data.substr(i, 8), 16));
}
// Write the rest of bytes (n % 8)
for(; i < data.length; i += 2, j++){
	bytes.setUint8(j, parseInt(data.substr(i, 2), 16));
}
```

#### Store bytes in JS source as base64

See [Store bytes in JS source as Data URI](#store-bytes-in-js-source-as-data-uri)

Base64 to bytes. The ratio is 4:3 bytes

```js
function base64ToBytes(data){
	// Use atob() but less performant for big data (string->string->arraybuffer)
	//let decodedData = atob(data);
	//let bytes = new Uint8Array(decodedData.length);
	//for (let i = 0, l = bytes.length; i < l; i++) {
	//	bytes[i] = decodedData.charCodeAt(i);
	//}
	//
	//return bytes.buffer;

	// Parts from https://developer.mozilla.org/en-US/Add-ons/Code_snippets/StringView
	// from StringView.base64ToBytes
	// Invalid chars https://bugzilla.mozilla.org/show_bug.cgi?id=73026#c12
	let cleanedData = data.replace(/\x20\t\r\n=/g, "");
	if (/[^A-Za-z0-9\+\/]/g.test(cleanedData)) {
		throw new DOMException("Invalid base64 data", "DataError");
	}
	let dataLength = cleanedData.length;
	let numBytes = /*length ? Math.ceil((dataLength * 3 + 1 >>> 2) / length) * length : */dataLength * 3 + 1 >>> 2;
	if (numBytes % 4 > 0) {
		throw new DOMException("Invalid data URI", "DataError");
	}
	let bytes = new Uint8Array(numBytes);

	for (let mod3, mod4, buffer = 0, index = 0, dataIndex = 0; dataIndex < dataLength; dataIndex++) {
		mod4 = dataIndex & 3;
		let charCode = cleanedData.charCodeAt(dataIndex);
		// from StringView.b64ToUint6
		if(charCode > 64 && charCode < 91){
			charCode -= 65
		}else if(charCode > 96 && charCode < 123){
			charCode -= 71
		}else if(charCode > 47 && charCode < 58){
			charCode += 4
		}else if(charCode === 43){
			charCode = 62
		}else if(charCode === 47){
			charCode = 63
		}else{
			charCode = 0
		}
		buffer |= charCode << 18 - 6 * mod4;
		if (mod4 === 3 || dataLength - dataIndex === 1) {
			for (mod3 = 0; mod3 < 3 && index < numBytes; mod3++, index++) {
				bytes[index] = buffer >>> (16 >>> mod3 & 0b11000) & 0xff;
			}
			buffer = 0;
		}
	}

	return bytes.buffer;
}

function urlB64ToUint8Array(base64String) {
	const padding = "=".repeat((4 - base64String.length % 4) % 4);
	const base64 = (base64String + padding)
		.replace(/\-/g, "+")
		.replace(/_/g, "/");

	const rawData = window.atob(base64);
	const outputArray = new Uint8Array(rawData.length);

	for (let i = 0; i < rawData.length; ++i) {
		outputArray[i] = rawData.charCodeAt(i);
	}
	return outputArray;
}

function uint8ArrayToBase64Url(uint8Array, start, end) {
	start = start || 0;
	end = end || uint8Array.byteLength;

	const base64 = window.btoa(String.fromCharCode.apply(null, uint8Array.subarray(start, end)));
	return base64
		.replace(/\=/g, "") // eslint-disable-line no-useless-escape
		.replace(/\+/g, "-")
		.replace(/\//g, "_");
}
```

- [Base64 encoding and decoding - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/WindowBase64/Base64_encoding_and_decoding#The_Unicode_Problem)
- [StringView - Mozilla | MDN](https://developer.mozilla.org/en-US/Add-ons/Code_snippets/StringView)
- https://github.com/blueimp/JavaScript-Canvas-to-Blob
- https://github.com/beatgammit/base64-js
- https://github.com/dankogai/js-base64
- [javascript - Convert Data URI to File then append to FormData - Stack Overflow](https://stackoverflow.com/questions/4998908/convert-data-uri-to-file-then-append-to-formdata)
- [jquery - How to convert dataURL to file object in javascript? - Stack Overflow](https://stackoverflow.com/questions/6850276/how-to-convert-dataurl-to-file-object-in-javascript)
- [javascript - Blob from DataURL? - Stack Overflow](https://stackoverflow.com/questions/12168909/blob-from-dataurl)
- [Sending and Receiving Binary Data - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Sending_and_Receiving_Binary_Data)
- [javascript - Converting between strings and ArrayBuffers - Stack Overflow](https://stackoverflow.com/questions/6965107/converting-between-strings-and-arraybuffers/11058858#11058858)
- [Retrieving binary file content using Javascript, base64 encode it and reverse-decode it using Python - Stack Overflow](https://stackoverflow.com/questions/7370943/retrieving-binary-file-content-using-javascript-base64-encode-it-and-reverse-de/7372816#7372816)

#### Store bytes in JS source as base91

- [basE91 - binary to ASCII text encoding](http://base91.sourceforge.net/)

#### Store bytes in JS source as base124

**Or reconstruct data from UTF-8 encoded char, but can't work because can't control when bit header appears**

>  breaks up data across byte boundaries which then makes gzip significantly less efficient

**Better to compress before encode**. But in case of JS, gzip is better if bytes are use less efficient encoding

127 (0x00..0x7F) can be used without UTF-8 encode to 2 or more bytes

Exclude or need escape delimiter, escape char and special chars (`$` for multiline string - aka template literals; `\r` and `\n` for single line string):

124 or 123

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String

See http://blog.kevinalbs.com/base122 and https://github.com/kevinAlbs/Base122 and https://news.ycombinator.com/item?id=13049329

Against: performance (probably), less performant with deflate compression, not well supported and not standard

Inspiration (base122?):

```
/*
This table includes 11280 characters: characters are defined in Japanese Industrial Standards(JIS X 0208-1997), special characters is available in windows, “i-mode EMOJI”(pictogram).
The table is sorted by JIS code. The function making the table contained an ASCII string that was differential compressed and decoded script, this function will be executed when script file loaded.
This mechanism make some advantage: volume of the table decrease by half, works on any encode environment because it dose’nt include “Kanji”.
You can write direct this function to HTML, because it does’nt include characters that make a browser confusing such as “</”. The table used in escape/unescape functions about SJIS.
*/
// 12396 chars; Firefox: 12832B Chrome: 12424B
// JCT11280
var a = "zKV33~jZ4zN=~ji36XazM93y!{~k2y!o~k0ZlW6zN?3Wz3W?{EKzK[33[`y|;-~j^YOTz$!~kNy|L1$353~jV3zKk3~k-4P4zK_2+~jY4y!xYHR~jlz$_~jk4z$e3X5He<0y!wy|X3[:~l|VU[F3VZ056Hy!nz/m1XD61+1XY1E1=1y|bzKiz!H034zKj~mEz#c5ZA3-3X$1~mBz$$3~lyz#,4YN5~mEz#{ZKZ3V%7Y}!J3X-YEX_J(3~mAz =V;kE0/y|F3y!}~m>z/U~mI~j_2+~mA~jp2;~m@~k32;~m>V}2u~mEX#2x~mBy+x2242(~mBy,;2242(~may->2&XkG2;~mIy-_2&NXd2;~mGz,{4<6:.:B*B:XC4>6:.>B*BBXSA+A:X]E&E<~r#z+625z s2+zN=`HXI@YMXIAXZYUM8X4K/:Q!Z&33 3YWX[~mB`{zKt4z (zV/z 3zRw2%Wd39]S11z$PAXH5Xb;ZQWU1ZgWP%3~o@{Dgl#gd}T){Uo{y5_d{e@}C(} WU9|cB{w}bzvV|)[} H|zT}d||0~{]Q|(l{|x{iv{dw}(5}[Z|kuZ }cq{{y|ij}.I{idbof%cu^d}Rj^y|-M{ESYGYfYsZslS`?ZdYO__gLYRZ&fvb4oKfhSf^d<Yeasc1f&a=hnYG{QY{D`Bsa|u,}Dl|_Q{C%xK|Aq}C>|c#ryW=}eY{L+`)][YF_Ub^h4}[X|?r|u_ex}TL@YR]j{SrXgo*|Gv|rK}B#mu{R1}hs|dP{C7|^Qt3|@P{YVV |8&}#D}ef{e/{Rl|>Hni}R1{Z#{D[}CQlQ||E}[s{SG_+i8eplY[=[|ec[$YXn#`hcm}YR|{Ci(_[ql|?8p3]-}^t{wy}4la&pc|3e{Rp{LqiJ],] `kc(]@chYnrM`O^,ZLYhZB]ywyfGY~aex!_Qww{a!|)*lHrM{N+n&YYj~Z b c#e_[hZSon|rOt`}hBXa^i{lh|<0||r{KJ{kni)|x,|0auY{D!^Sce{w;|@S|cA}Xn{C1h${E]Z-XgZ*XPbp]^_qbH^e[`YM|a||+=]!Lc}]vdBc=j-YSZD]YmyYLYKZ9Z>Xcczc2{Yh}9Fc#Z.l{}(D{G{{mRhC|L3b#|xK[Bepj#ut`H[,{E9Yr}1b{[e]{ZFk7[ZYbZ0XL]}Ye[(`d}c!|*y`Dg=b;gR]Hm=hJho}R-[n}9;{N![7k_{UbmN]rf#pTe[x8}!Qcs_rs[m`|>N}^V})7{^r|/E}),}HH{OYe2{Skx)e<_.cj.cjoMhc^d}0uYZd!^J_@g,[[[?{i@][|3S}Yl3|!1|eZ|5IYw|1D}e7|Cv{OHbnx-`wvb[6[4} =g+k:{C:}ed{S]|2M]-}WZ|/q{LF|dYu^}Gs^c{Z=}h>|/i|{W]:|ip{N:|zt|S<{DH[p_tvD{N<[8Axo{X4a.^o^X>Yfa59`#ZBYgY~_t^9`jZHZn`>G[oajZ;X,i)Z.^~YJe ZiZF^{][[#Zt^|]Fjx]&_5dddW]P0C[-]}]d|y {C_jUql] |OpaA[Z{lp|rz}:Mu#]_Yf6{Ep?f5`$[6^D][^u[$[6^.Z8]]ePc2U/=]K^_+^M{q*|9tYuZ,s(dS{i=|bNbB{uG}0jZOa:[-]dYtu3]:]<{DJ_SZIqr_`l=Yt`gkTnXb3d@kiq0a`Z{|!B|}e}Ww{Sp,^Z|0>_Z}36|]A|-t}lt{R6pi|v8hPu#{C>YOZHYmg/Z4nicK[}hF_Bg|YRZ7c|crkzYZY}_iXcZ.|)U|L5{R~qi^Uga@Y[xb}&qdbd6h5|Btw[}c<{Ds53[Y7]?Z<|e0{L[ZK]mXKZ#Z2^tavf0`PE[OSOaP`4gi`qjdYMgys/?[nc,}EEb,eL]g[n{E_b/vcvgb.{kcwi`~v%|0:|iK{Jh_vf5lb}KL|(oi=LrzhhY_^@`zgf[~g)[J_0fk_V{T)}I_{D&_/d9W/|MU[)f$xW}?$xr4<{Lb{y4}&u{XJ|cm{Iu{jQ}CMkD{CX|7A}G~{kt)nB|d5|<-}WJ}@||d@|Iy}Ts|iL|/^|no|0;}L6{Pm]7}$zf:|r2}?C_k{R(}-w|`G{Gy[g]bVje=_0|PT{^Y^yjtT[[[l!Ye_`ZN]@[n_)j3nEgMa]YtYpZy].d-Y_cjb~Y~[nc~sCi3|zg}B0}do{O^{|$`_|D{}U&|0+{J3|8*]iayx{a{xJ_9|,c{Ee]QXlYb]$[%YMc*]w[aafe]aVYi[fZEii[xq2YQZHg]Y~h#|Y:thre^@^|_F^CbTbG_1^qf7{L-`VFx Zr|@EZ;gkZ@slgko`[e}T:{Cu^pddZ_`yav^Ea+[#ZBbSbO`elQfLui}.F|txYcbQ`XehcGe~fc^RlV{D_0ZAej[l&jShxG[ipB_=u:eU}3e8[=j|{D(}dO{Do[BYUZ0/]AYE]ALYhZcYlYP/^-^{Yt_1_-;YT`P4BZG=IOZ&]H[e]YYd[9^F[1YdZxZ?Z{Z<]Ba2[5Yb[0Z4l?]d_;_)a?YGEYiYv`_XmZs4ZjY^Zb]6gqGaX^9Y}dXZr[g|]Y}K aFZp^k^F]M`^{O1Ys]ZCgCv4|E>}8eb7}l`{L5[Z_faQ|c2}Fj}hw^#|Ng|B||w2|Sh{v+[G}aB|MY}A{|8o}X~{E8paZ:]i^Njq]new)`-Z>haounWhN}c#{DfZ|fK]KqGZ=:u|fqoqcv}2ssm}.r{]{nIfV{JW)[K|,Z{Uxc|]l_KdCb%]cfobya3`p}G^|LZiSC]U|(X|kBlVg[kNo({O:g:|-N|qT}9?{MBiL}Sq{`P|3a|u.{Uaq:{_o|^S}jX{Fob0`;|#y_@[V[K|cw[<_ }KU|0F}d3|et{Q7{LuZttsmf^kYZ`Af`}$x}U`|Ww}d]| >}K,r&|XI|*e{C/a-bmr1fId4[;b>tQ_:]hk{b-pMge]gfpo.|(w[jgV{EC1Z,YhaY^q,_G[c_g[J0YX]`[h^hYK^_Yib,` {i6vf@YM^hdOKZZn(jgZ>bzSDc^Z%[[o9[2=/YHZ(_/Gu_`*|8z{DUZxYt^vuvZjhi^lc&gUd4|<UiA`z]$b/Z?l}YI^jaHxe|;F}l${sQ}5g}hA|e4}?o{ih}Uz{C)jPe4]H^J[Eg[|AMZMlc}:,{iz}#*|gc{Iq|/:|zK{l&}#u|myd{{M&v~nV};L|(g|I]ogddb0xsd7^V})$uQ{HzazsgxtsO^l}F>ZB]r|{7{j@cU^{{CbiYoHlng]f+nQ[bkTn/}<-d9q {KXadZYo+n|l[|lc}V2{[a{S4Zam~Za^`{HH{xx_SvF|ak=c^[v^7_rYT`ld@]:_ub%[$[m](Shu}G2{E.ZU_L_R{tz`vj(f?^}hswz}GdZ}{S:h`aD|?W|`dgG|if{a8|J1{N,}-Ao3{H#{mfsP|[ bzn+}_Q{MT{u4kHcj_q`eZj[8o0jy{p7}C|[}l){MuYY{|Ff!Ykn3{rT|m,^R|,R}$~Ykgx{P!]>iXh6[l[/}Jgcg{JYZ.^qYfYIZl[gZ#Xj[Pc7YyZD^+Yt;4;`e8YyZVbQ7YzZxXja.7SYl[s]2^/Ha$[6ZGYrb%XiYdf2]H]kZkZ*ZQ[ZYS^HZXcCc%Z|[(bVZ]]:OJQ_DZCg<[,]%Zaa [g{C00HY[c%[ChyZ,Z_`PbXa+eh`^&jPi0a[ggvhlekL]w{Yp^v}[e{~;k%a&k^|nR_z_Qng}[E}*Wq:{k^{FJZpXRhmh3^p>de^=_7`|ZbaAZtdhZ?n4ZL]u`9ZNc3g%[6b=e.ZVfC[ZZ^^^hD{E(9c(kyZ=bb|Sq{k`|vmr>izlH[u|e`}49}Y%}FT{[z{Rk}Bz{TCc/lMiAqkf(m$hDc;qooi[}^o:c^|Qm}a_{mrZ(pA`,}<2sY| adf_%|}`}Y5U;}/4|D>|$X{jw{C<|F.hK|*A{MRZ8Zsm?imZm_?brYWZrYx`yVZc3a@f?aK^ojEd {bN}/3ZH]/$YZhm^&j 9|(S|b]mF}UI{q&aM]LcrZ5^.|[j`T_V_Gak}9J[ ZCZD|^h{N9{~&[6Zd{}B}2O|cv]K}3s}Uy|l,fihW{EG`j_QOp~Z$F^zexS`dcISfhZBXP|.vn|_HYQ|)9|cr]<`&Z6]m_(ZhPcSg>`Z]5`~1`0Xcb4k1{O!bz|CN_T{LR|a/gFcD|j<{Z._[f)mPc:1`WtIaT1cgYkZOaVZOYFrEe[}T$}Ch}mk{K-^@]fH{Hdi`c*Z&|Kt{if[C{Q;{xYB`dYIX:ZB[}]*[{{p9|4GYRh2ao{DS|V+[zd$`F[ZXKadb*A] Ys]Maif~a/Z2bmclb8{Jro_rz|x9cHojbZ{GzZx_)]:{wAayeDlx}<=`g{H1{l#}9i|)=|lP{Qq}.({La|!Y{i2EZfp=c*}Cc{EDvVB|;g}2t{W4av^Bn=]ri,|y?|3+}T*ckZ*{Ffr5e%|sB{lx^0]eZb]9[SgAjS_D|uHZx]dive[c.YPkcq/}db{EQh&hQ|eg}G!ljil|BO]X{Qr_GkGl~YiYWu=c3eb}29v3|D|}4i||.{Mv})V{SP1{FX}CZW6{cm|vO{pS|e#}A~|1i}81|Mw}es|5[}3w{C`h9aL]o{}p[G`>i%a1Z@`Ln2bD[$_h`}ZOjhdTrH{[j_:k~kv[Sdu]CtL}41{I |[[{]Zp$]XjxjHt_eThoa#h>sSt8|gK|TVi[Y{t=}Bs|b7Zpr%{gt|Yo{CS[/{iteva|cf^hgn}($_c^wmb^Wm+|55jrbF|{9^ q6{C&c+ZKdJkq_xOYqZYSYXYl`8]-cxZAq/b%b*_Vsa[/Ybjac/OaGZ4fza|a)gY{P?| I|Y |,pi1n7}9bm9ad|=d{aV|2@[(}B`d&|Uz}B}{`q|/H|!JkM{FU|CB|.{}Az}#P|lk}K{|2rk7{^8^?`/|k>|Ka{Sq}Gz}io{DxZh[yK_#}9<{TRdgc]`~Z>JYmYJ]|`!ZKZ]gUcx|^E[rZCd`f9oQ[NcD_$ZlZ;Zr}mX|=!|$6ZPZYtIo%fj}CpcN|B,{VDw~gb}@hZg`Q{LcmA[(bo`<|@$|o1|Ss}9Z_}tC|G`{F/|9nd}i=}V-{L8aaeST]daRbujh^xlpq8|}zs4bj[S`J|]?G{P#{rD{]I`OlH{Hm]VYuSYUbRc*6[j`8]pZ[bt_/^Jc*[<Z?YE|Xb|?_Z^Vcas]h{t9|Uwd)_(=0^6Zb{Nc} E[qZAeX[a]P^|_J>e8`W^j_Y}R{{Jp__]Ee#e:iWb9q_wKbujrbR}CY`,{mJ}gz{Q^{t~N|? gSga`V_||:#mi}3t|/I`X{N*|ct|2g{km}gi|{={jC}F;|E}{ZZjYf*frmu}8Tdroi{T[|+~}HG{cJ}DM{Lp{Ctd&}$hi3|FZ| m}Kr|38}^c|m_|Tr{Qv|36}?Up>|;S{DV{k_as}BK{P}}9p|t`jR{sAm4{D=b4pWa[}Xi{EjwEkI}3S|E?u=X0{jf} S|NM|JC{qo^3cm]-|JUx/{Cj{s>{Crt[UXuv|D~|j|d{YXZR}Aq}0r}(_{pJfi_z}0b|-vi)Z mFe,{f4|q`b{}^Z{HM{rbeHZ|^x_o|XM|L%|uFXm}@C_{{Hhp%a7|0p[Xp+^K}9U{bP}: tT}B|}+$|b2|[^|~h{FAby[`{}xgygrt~h1[li`c4vz|,7p~b(|mviN}^pg[{N/|g3|^0c,gE|f%|7N{q[|tc|TKA{LU}I@|AZp(}G-sz{F |qZ{}F|f-}RGn6{Z]_5})B}UJ{FFb2]4ZI@v=k,]t_Dg5Bj]Z-]L]vrpdvdGlk|gF}G]|IW}Y0[G| /bo|Te^,_B}#n^^{QHYI[?hxg{[`]D^IYRYTb&kJ[cri[g_9]Ud~^_]<p@_e_XdNm-^/|5)|h_{J;{kacVopf!q;asqd}n)|.m|bf{QW|U)}b+{tL|w``N|to{t ZO|T]jF}CB|0Q{e5Zw|k |We}5:{HO{tPwf_uajjBfX}-V_C_{{r~gg|Ude;s+}KNXH}! `K}eW{Upwbk%ogaW}9EYN}YY|&v|SL{C3[5s.]Y]I]u{M6{pYZ`^,`ZbCYR[1mNg>rsk0Ym[jrE]RYiZTr*YJ{Ge|%-lf|y(`=[t}E6{k!|3)}Zk} ][G{E~cF{u3U.rJ|a9p#o#ZE|?|{sYc#vv{E=|LC}cu{N8`/`3`9rt[4|He{cq|iSYxY`}V |(Q|t4{C?]k_Vlvk)BZ^r<{CL}#h}R+[<|i=}X|{KAo]|W<`K{NW|Zx}#;|fe{IMr<|K~tJ_x}AyLZ?{GvbLnRgN}X&{H7|x~}Jm{]-| GpNu0}.ok>|c4{PYisrDZ|fwh9|hfo@{H~XSbO]Odv]%`N]b1Y]]|eIZ}_-ZA]aj,>eFn+j[aQ_+]h[J_m_g]%_wf.`%k1e#Z?{CvYu_B^|gk`Xfh^M3`afGZ-Z|[m{L}|k3cp[it ^>YUi~d>{T*}YJ{Q5{Jxa$hg|%4`}|LAgvb }G}{P=|<;Ux{_skR{cV|-*|s-{Mp|XP|$G|_J}c6cM{_=_D|*9^$ec{V;|4S{qO|w_|.7}d0|/D}e}|0G{Dq]Kdp{}dfDi>}B%{Gd|nl}lf{C-{y}|ANZr}#={T~|-(}c&{pI|ft{lsVP}){|@u}!W|bcmB{d?|iW|:dxj{PSkO|Hl]Li:}VYk@|2={fnWt{M3`cZ6|)}|Xj}BYa?vo{e4|L7|B7{L7|1W|lvYO}W8nJ|$Vih|{T{d*_1|:-n2dblk``fT{Ky|-%}m!|Xy|-a{Pz}[l{kFjz|iH}9N{WE{x,|jz}R {P|{D)c=nX|Kq|si}Ge{sh|[X{RF{t`|jsr*fYf,rK|/9}$}}Nf{y!1|<Std}4Wez{W${Fd_/^O[ooqaw_z[L`Nbv[;l7V[ii3_PeM}.h^viqYjZ*j1}+3{bt{DR[;UG}3Og,rS{JO{qw{d<_zbAh<R[1_r`iZTbv^^a}c{iEgQZ<exZFg.^Rb+`Uj{a+{z<[~r!]`[[|rZYR|?F|qppp]L|-d|}K}YZUM|=Y|ktm*}F]{D;g{uI|7kg^}%?Z%ca{N[_<q4xC]i|PqZC]n}.bDrnh0Wq{tr|OMn6tM|!6|T`{O`|>!]ji+]_bTeU}Tq|ds}n|{Gm{z,f)}&s{DPYJ`%{CGd5v4tvb*hUh~bf]z`jajiFqAii]bfy^U{Or|m+{I)cS|.9k:e3`^|xN}@Dnlis`B|Qo{`W|>||kA}Y}{ERYuYx`%[exd`]|OyiHtb}HofUYbFo![5|+]gD{NIZR|Go}.T{rh^4]S|C9_}xO^i`vfQ}C)bK{TL}cQ|79iu}9a];sj{P.o!f[Y]pM``Jda^Wc9ZarteBZClxtM{LW}l9|a.mU}KX}4@{I+f1}37|8u}9c|v${xGlz}jP{Dd1}e:}31}%3X$|22i<v+r@~mf{sN{C67G97855F4YL5}8f{DT|xy{sO{DXB334@55J1)4.G9A#JDYtXTYM4, YQD9;XbXm9SX]IB^4UN=Xn<5(;(F3YW@XkH-X_VM[DYM:5XP!T&Y`6|,^{IS-*D.H>:LXjYQ0I3XhAF:9:(==.F*3F1189K/7163D,:@|e2{LS36D4hq{Lw/84443@4.933:0307::6D7}&l{Mx657;89;,K5678H&93D(H<&<>0B90X^I;}Ag1{P%3A+>><975}[S{PZE453?4|T2{Q+5187;>447:81{C=hL6{Me^:=7ii{R=.=F<81;48?|h8}Uh{SE|,VxL{ST,7?9Y_5Xk3A#:$%YSYdXeKXOD8+TXh7(@>(YdXYHXl9J6X_5IXaL0N?3YK7Xh!1?XgYz9YEXhXaYPXhC3X`-YLY_XfVf[EGXZ5L8BXL9YHX]SYTXjLXdJ: YcXbQXg1PX]Yx4|Jr{Ys4.8YU+XIY`0N,<H%-H;:0@,74/:8546I=9177154870UC]d<C3HXl7ALYzXFXWP<<?E!88E5@03YYXJ?YJ@6YxX-YdXhYG|9o{`iXjY_>YVXe>AYFX[/(I@0841?):-B=14337:8=|14{c&93788|di{cW-0>0<097/A;N{FqYpugAFT%X/Yo3Yn,#=XlCYHYNX[Xk3YN:YRT4?)-YH%A5XlYF3C1=NWyY}>:74-C673<69545v {iT85YED=64=.F4..9878/D4378?48B3:7:7/1VX[f4{D,{l<5E75{dAbRB-8-@+;DBF/$ZfW8S<4YhXA.(5@*11YV8./S95C/0R-A4AXQYI7?68167B95HA1*<M3?1/@;/=54XbYP36}lc{qzSS38:19?,/39193574/66878Yw1X-87E6=;964X`T734:>86>1/=0;(I-1::7ALYGXhF+Xk[@W%TYbX7)KXdYEXi,H-XhYMRXfYK?XgXj.9HX_SX]YL1XmYJ>Y}WwIXiI-3-GXcYyXUYJ$X`Vs[7;XnYEZ;XF! 3;%8;PXX(N3Y[)Xi1YE&/ :;74YQ6X`33C;-(>Xm0(TYF/!YGXg8 9L5P01YPXO-5%C|qd{{/K/E6,=0144:361:955;6443@?B7*7:F89&F35YaX-CYf,XiFYRXE_e{}sF 0*7XRYPYfXa5YXXY8Xf8Y~XmA[9VjYj*#YMXIYOXk,HHX40YxYMXU8OXe;YFXLYuPXP?EB[QV0CXfY{:9XV[FWE0D6X^YVP*$4%OXiYQ(|xp|%c3{}V`1>Y`XH00:8/M6XhQ1:;3414|TE|&o@1*=81G8<3}6<|(f6>>>5-5:8;093B^3U*+*^*UT30XgYU&7*O1953)5@E78--F7YF*B&0:%P68W9Zn5974J9::3}Vk|-,C)=)1AJ4+<3YGXfY[XQXmT1M-XcYTYZXCYZXEYXXMYN,17>XIG*SaS|/eYJXbI?XdNZ+WRYP<F:R PXf;0Xg`$|1GX9YdXjLYxWX!ZIXGYaXNYm6X9YMX?9EXmZ&XZ#XQ>YeXRXfAY[4 ;0X!Zz0XdN$XhYL XIY^XGNXUYS/1YFXhYk.TXn4DXjB{jg|4DEX]:XcZMW=A.+QYL<LKXc[vV$+&PX*Z3XMYIXUQ:ZvW< YSXFZ,XBYeXMM)?Xa XiZ4/EXcP3%}&-|6~:1(-+YT$@XIYRBC<}&,|7aJ6}bp|8)K1|Xg|8C}[T|8Q.89;-964I38361<=/;883651467<7:>?1:.}le|:Z=39;1Y^)?:J=?XfLXbXi=Q0YVYOXaXiLXmJXO5?.SFXiCYW}-;|=u&D-X`N0X^,YzYRXO(QX_YW9`I|>hZ:N&X)DQXP@YH#XmNXi$YWX^=!G6YbYdX>XjY|XlX^XdYkX>YnXUXPYF)FXT[EVTMYmYJXmYSXmNXi#GXmT3X8HOX[ZiXN]IU2>8YdX1YbX<YfWuZ8XSXcZU%0;1XnXkZ_WTG,XZYX5YSX Yp 05G?XcYW(IXg6K/XlYP4XnI @XnO1W4Zp-9C@%QDYX+OYeX9>--YSXkD.YR%Q/Yo YUX].Xi<HYEZ2WdCE6YMXa7F)=,D>-@9/8@5=?7164;35387?N<618=6>7D+C50<6B03J0{Hj|N9$D,9I-,.KB3}m |NzE0::/81YqXjMXl7YG; [.W=Z0X4XQY]:MXiR,XgM?9$9>:?E;YE77VS[Y564760391?14941:0=:8B:;/1DXjFA-564=0B3XlH1+D85:0Q!B#:-6&N/:9<-R3/7Xn<*3J4.H:+334B.=>30H.;3833/76464665755:/83H6633:=;.>5645}&E|Y)?1/YG-,93&N3AE@5 <L1-G/8A0D858/30>8<549=@B8] V0[uVQYlXeD(P#ID&7T&7;Xi0;7T-$YE)E=1:E1GR):--0YI7=E<}n9|aT6783A>D7&4YG7=391W;Zx<5+>F#J39}o/|cc;6=A050EQXg8A1-}D-|d^5548083563695D?-.YOXd37I$@LYLWeYlX<Yd+YR A$;3-4YQ-9XmA0!9/XLY_YT(=5XdDI>YJ5XP1ZAW{9>X_6R(XhYO65&J%DA)C-!B:97#A9;@?F;&;(9=11/=657/H,<8}bz|j^5446>.L+&Y^8Xb6?(CYOXb*YF(8X`FYR(XPYVXmPQ%&DD(XmZXW??YOXZXfCYJ79,O)XnYF7K0!QXmXi4IYFRXS,6<%-:YO(+:-3Q!1E1:W,Zo}Am|n~;3580534*?3Zc4=9334361693:30C<6/717:<1/;>59&:4}6!|rS36=1?75<8}[B|s809983579I.A.>84758=108564741H*9E{L{|u%YQ<%6XfH.YUXe4YL@,>N}Tv|ve*G0X)Z;/)3@A74(4P&A1X:YVH97;,754*A66:1 D739E3553545558E4?-?K17/770843XAYf838A7K%N!YW4.$T19Z`WJ*0XdYJXTYOXNZ 1XaN1A+I&Xi.Xk3Z3GB&5%WhZ1+5#Y[X<4YMXhQYoQXVXbYQ8XSYUX4YXBXWDMG0WxZA[8V+Z8X;D],Va$%YeX?FXfX[XeYf<X:Z[WsYz8X_Y]%XmQ(!7BXIZFX]&YE3F$(1XgYgYE& +[+W!<YMYFXc;+PXCYI9YrWxGXY9DY[!GXiI7::)OC;*$.>N*HA@{C|}&k=:<TB83X`3YL+G4XiK]i}(fYK<=5$.FYE%4*5*H*6XkCYL=*6Xi6!Yi1KXR4YHXbC8Xj,B9ZbWx/XbYON#5B}Ue}+QKXnF1&YV5XmYQ0!*3IXBYb71?1B75XmF;0B976;H/RXU:YZX;BG-NXj;XjI>A#D3B636N;,*%<D:0;YRXY973H5)-4FXOYf0:0;/7759774;7;:/855:543L43<?6=E,.A4:C=L)%4YV!1(YE/4YF+ F3%;S;&JC:%/?YEXJ4GXf/YS-EXEYW,9;E}X$}547EXiK=51-?71C%?57;5>463553Zg90;6447?<>4:9.7538XgN{|!}9K/E&3-:D+YE1)YE/3;37/:05}n<}:UX8Yj4Yt864@JYK..G=.(A Q3%6K>3(P3#AYE$-6H/456*C=.XHY[#S.<780191;057C)=6HXj?955B:K1 E>-B/9,;5.!L?:0>/.@//:;7833YZ56<4:YE=/:7Z_WGC%3I6>XkC*&NA16X=Yz2$X:Y^&J48<99k8}CyB-61<18K946YO4{|N}E)YIB9K0L>4=46<1K0+R;6-=1883:478;4,S+3YJX`GJXh.Yp+Xm6MXcYpX(>7Yo,/:X=Z;Xi0YTYHXjYmXiXj;*;I-8S6N#XgY}.3XfYGO3C/$XjL$*NYX,1 6;YH&<XkK9C#I74.>}Hd`A748X[T450[n75<4439:18A107>|ET}Rf<1;14876/Yb983E<5.YNXd4149>,S=/4E/<306443G/06}0&}UkYSXFYF=44=-5095=88;63844,9E6644{PL}WA8:>)7+>763>>0/B3A545CCnT}Xm|dv}Xq1L/YNXk/H8;;.R63351YY747@15YE4J8;46;.38.>4A369.=-83,;Ye3?:3@YE.4-+N353;/;@(X[YYD>@/05-I*@.:551741Yf5>6A443<3535;.58/86=D4753442$635D1>0359NQ @73:3:>><Xn?;43C14 ?Y|X611YG1&<+,4<*,YLXl<1/AIXjF*N89A4Z576K1XbJ5YF.ZOWN.YGXO/YQ01:4G38Xl1;KI0YFXB=R<7;D/,/4>;$I,YGXm94@O35Yz66695385.>:6A#5}W7n^4336:4157597434433<3|XA}m`>=D>:4A.337370?-6Q96{`E|4A}C`|Qs{Mk|J+~r>|o,wHv>Vw}!c{H!|Gb|*Ca5}J||,U{t+{CN[!M65YXOY_*B,Y[Z9XaX[QYJYLXPYuZ%XcZ8LY[SYPYKZM<LMYG9OYqSQYM~[e{UJXmQYyZM_)>YjN1~[f3{aXFY|Yk:48YdH^NZ0|T){jVFYTZNFY^YTYN~[h{nPYMYn3I]`EYUYsYIZEYJ7Yw)YnXPQYH+Z.ZAZY]^Z1Y`YSZFZyGYHXLYG 8Yd#4~[i|+)YH9D?Y^F~Y7|-eYxZ^WHYdYfZQ~[j|3>~[k|3oYmYqY^XYYO=Z*4[]Z/OYLXhZ1YLZIXgYIHYEYK,<Y`YEXIGZI[3YOYcB4SZ!YHZ*&Y{Xi3~[l|JSY`Zz?Z,~[m|O=Yi>??XnYWXmYS617YVYIHZ(Z4[~L4/=~[n|Yu{P)|];YOHHZ}~[o33|a>~[r|aE]DH~[s|e$Zz~[t|kZFY~XhYXZB[`Y}~[u|{SZ&OYkYQYuZ2Zf8D~[v}% ~[w3},Q[X]+YGYeYPIS~[y}4aZ!YN^!6PZ*~[z}?E~[{3}CnZ=~[}}EdDZz/9A3(3S<,YR8.D=*XgYPYcXN3Z5 4)~[~}JW=$Yu.XX~] }KDX`PXdZ4XfYpTJLY[F5]X~[2Yp}U+DZJ::<446[m@~]#3}]1~]%}^LZwZQ5Z`/OT<Yh^ -~]&}jx[ ~m<z!%2+~ly4VY-~o>}p62yz!%2+Xf2+~ly4VY-zQ`z (=] 2z~o2";

// JCT11280 map (char with its JIS code)
var C = {
	" ": 0,
	"!": 1
}
var c = 34;
var p;
var s = "";
var fromCharCode = String.fromCharCode;
var t = fromCharCode(12539);
for (let charCode = 34, code = 2; charCode < 127; charCode++){
	C[fromCharCode(c)] = charCode ^ 39 && charCode ^ 92 ? code++ : 0;
}
for (let c, i = 0; 0 <= (c = C[a.charAt(i++)]);){
	if (16 === c){
		if ((c = C[a.charAt(i++)]) < 87) {
			if (86 === c) c = 1879;
			for (; c--;) s += fromCharCode(++p)
		}
		else
		{
			s += s.substr(8272, 360);
		}
	}
	else if (c < 86){
		s += fromCharCode(p += c < 51 ? c - 16 : (c - 55) * 92 + C[a.charAt(i++)]);
	}
	else if ((c = ((c - 86) * 92 + C[a.charAt(i++)]) * 92 + C[a.charAt(i++)]) < 49152){
		s += fromCharCode(p = c < 40960 ? c : c | 57344);
	}
	else {
		c &= 511;
		for (; c--;) s += t;
		p = 12539
	}
}
//s
```

#### Store bytes in JS source as base65536

- [qntm/base65536: Unicode's answer to Base64](https://github.com/qntm/base65536)

#### Store bytes in JS source as Data URI

See [Store bytes in JS source as base64](#store-bytes-in-js-source-as-base64)

```js
const uri = "data:application/octet-stream;base64,..."
```

Easyier to transmit in data (XML, JSON)

But as a ratio of 4:3 bytes

- [Data URI scheme — Wikipedia](https://en.wikipedia.org/wiki/Data_URI_scheme)
- [Data URIs - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URIs)

Decode with XmlHttpRequest or fetch, but this could be not supported (see Safari)

Note: It's async, because `XMLHttpRequest` can't be used in synchronous mode because responseType other than the default value (equivalent of `"text"`) need async.

> (`responseType`) When set: throws an `InvalidAccessError` exception if the [synchronous flag](https://xhr.spec.whatwg.org/#synchronous-flag) is set
>
> — [XMLHttpRequest Standard](https://xhr.spec.whatwg.org/#the-responsetype-attribute)

Note: encoding scheme must be supported (base64 or unencoded)

```js
const xhr = new XMLHttpRequest();
xhr.open("GET", uri, true);
xhr.responseType = "arraybuffer";
xhr.addEventListener("error", event => console.log(event));
xhr.addEventListener("load", event => console.log(event.target.response));
xhr.send(null);
```

Decode directly, see [As base64](#as-base64)

```js
// https://github.com/graingert/datauritoblob/blob/master/dataURItoBlob.js
// https://stackoverflow.com/questions/6850276/how-to-convert-dataurl-to-file-object-in-javascript
// https://stackoverflow.com/questions/10412299/whats-the-difference-between-blobbuilder-and-the-new-blob-constructor
// https://stackoverflow.com/questions/5729842/what-parameters-are-possible-in-a-data-uris-mediatype
// https://tools.ietf.org/html/rfc2397
function dataURItoBytes(uri){
	if(!uri.startWidth("data:")){
		throw new URIError("Invalid data URI");
	}
	let [hashLessDataURI, hash] = dataURI.split("#");
	hash = hash.join("#");
	let [mediaType, ...data] = hashLessDataURI.split(",");
	// unescape is marked as depreciated, but could be used (retro compatibility)
	//let unescape = (str) => str.replace(/%([0-9A-F]{2})/g, (match, code) => String.fromCharCode('0x' + code));
	data = unescape(data.join(","));
	mediaType = mediaType.substr(5) || "text/plain";
	let [mediaTypeParametersLess, ...mediaTypeParameters] = mediaType.split(";");
	let encoding = mediaTypeParameters.length >= 1 && mediaTypeParameters[mediaTypeParameters.length - 1] == "base64" ? mediaTypeParameters.pop() : "none";

	if(encoding == "base64"){
		return base64ToBytes(data);
	}
	else if(encoding == "none"){
		//let charset = mediaTypeParameters.find(param => param.startsWith("encoding=")).substr(9) || "US-ASCII";
		let bytes = new Uint8Array(data.length);
		for (let i = 0, l = bytes.length; i < l; i++) {
			bytes[i] = data.charCodeAt(i);// ASCII chars
		}

		return bytes.buffer;
	}

	throw new Error(`Unknown encoding "${encoding}"`);
}
```

#### Store bytes in JS source as ArrayBuffer

Store the number array in a string that could be parsed as JSON. See [Store data as stringified JSON](../ECMAScript/ECMAScript.md#store-data-as-stringified-json)

The compress ratio is between 1:2 to 11:4

```js
let buffer = Uint32Array.from(JSON.parse("[0,1,2,...]")).buffer.slice(0);// not accurate, see below
```

To generate the corresponding code:

```js
let xhr = new XMLHttpRequest();
xhr.open("GET", "data:application/octet-stream;base64,AAECAwQFBgcICQ==");//0x010203040506070809
xhr.responseType = "arraybuffer";
xhr.addEventListener("error", event => console.log(event))
xhr.addEventListener("load", event => {
	// In the generated code, JavaScript will read an array of number (float64) first then write to it into the buffer
	//console.log(`Uint8Array.from([${Array.from(new Uint8Array(event.target.response)}]).buffer`);// a simple way to generate, to using uint8, but will use 8 more time & memory before write the buffer (javascript use float64 to store numbers/ints), but use between 2/1 and 4/1 bytes to store it, 0x00 -> 0xff = ",0" -> ",255"

	// Use Uint32Array is a better bet:
	// - it use less bytes to store the data: 2/4 to 11/4, 0x00000000 -> 0xffffffff = ",0" -> ",4294967295"
	// - it use the twice memory than the final buffer
	// Idealy we should use Uint64Array but this not exist in JS
	// But need to use DataView instead of Uint32Array to fix endianness (we don't know in advance what will be the platform's endianness)
	// (new DataView(new Uint8Array([0x01, 0x02, 0x03, 0x04]).buffer)).getUint32(0) == 0x01020304

	let typeBytes = 4;
	let buffer = event.target.response;
	let alignedByteLength = buffer.byteLength - buffer.byteLength % typeBytes;
	let alignedArray = new DataView(buffer, 0, alignedByteLength);
	let output = "";
	for(let byteIndex = 0; byteIndex < alignedByteLength; byteIndex += typeBytes){
		output += (byteIndex > 0 ? "," : "") + alignedArray.getUint32(byteIndex);
	}
	let aligned = alignedByteLength == buffer.byteLength;
	if(!aligned){
		// align bytes by filling with zeros
		let lastBytes = new Uint8Array(buffer, alignedByteLength, buffer.byteLength - alignedByteLength);
		let lastAlignedBytes = new Uint8Array(typeBytes);
		lastAlignedBytes.set(lastBytes);//fill first bytes
		output += (output.length > 0 ? "," : "") + (new DataView(lastAlignedBytes.buffer)).getUint32(0);
	}
	output = `JSON.parse("[${output}]").reduce((bytes, value, index) => (bytes.setUint32(index * 4, value), bytes), new DataView(new ArrayBuffer(${Math.ceil(buffer.byteLength / typeBytes) * typeBytes}))).buffer`;
	if(!aligned){
		output += `.slice(0, ${buffer.byteLength})`;
		//output = `ArrayBuffer.transfer(${output}, ${buffer.byteLength})`;// use transfert instead of slice (which copy buffer content), but it's not well supported
	}

	console.log(output);
});
xhr.send(null);
```

### Decompress GZIP

**Not work with raw deflate, because it's don't provide uncompressed length info. You need to read all compressed blocks first**

It's still could be a improvement if the data is only readed, but decompressed by the native PNG reader

As image

- end of file with comment
- use native PNG reader to decompress deflate data (GZIP, ZIP): add headers, load as blob URI, read using canvas
	And do the inverse: create GZIP, ZIP easily

- `printf '\x00\xFF\x88\x0F\xFF\x00\xFF\x0F' > data.rgb`, `convert -depth 8 -size `wc -c data.rgb`x1+0 rgb:data.rgb data.png`. Can't use the alpha channel due to pre-multiplied alpha applied to loaded images in canvas.
- https://en.wikipedia.org/wiki/Portable_Network_Graphics#Compression
- http://www.libpng.org/pub/png/spec/1.2/PNG-Chunks.html#C.IDAT
- https://stackoverflow.com/questions/388595/why-use-deflate-instead-of-gzip-for-text-files-served-by-apache
- https://stackoverflow.com/questions/2233062/javascript-deflate-implementation
- http://blog.calyptus.eu/seb/2009/05/png-parser-in-javascript/
- https://github.com/niegowski/node-pngjs
- http://www.forensicswiki.org/wiki/Gzip
- https://stackoverflow.com/questions/24082305/how-is-png-crc-calculated-exactly

 ```js
let deflateBytes = new Uint8Array();
// let blockType = deflateBytes[0] >> 5 & 0b00000011;
// // https://tools.ietf.org/html/rfc1951#section-3.2.4
// if(blockType == 0b00){
// 	let length = deflateBytes[1] << 8 | deflateBytes[2];
// 	let nlength = deflateBytes[3] << 8 | deflateBytes[4];
// 	if((length & ~nlen) != len) throw "Invalid block type 0 length";
// 	return new Uint8Array()
// }
compressedBytes.length / 4;
let canvas = document.createElement("canvas");
canvas.width = compressedBytes.length / 4
canvas.height = 1;
let context = canvas.getContext("2d");
let bytes = context.getImageData(0, 0, canvas.width, canvas.height).data;
```

### Read a blob

Create a blob from bytes:

```js
let blob = new Blob([bytes], {type: mediaType});
```

Read the blob with FileReader:

```js
let reader = new FileReader();
reader.addEventListener("loadend", () => console.log(reader.result, blob.type, blob.size));
reader.readAsArrayBuffer(blob);
```

Or with XHR:

```js
let url = URL.createObjectURL(blob);
let xhr = new XMLHttpRequest();
xhr.open("GET", url, true);
xhr.responseType = "arraybuffer";
xhr.addEventListener("error", event => console.log(event));
xhr.addEventListener("load", event => URL.revokeObjectURL(url), console.log(event.target.response, blob.type, event.target.getResponseHeader("Content-Type"), blob.size, event.target.getResponseHeader("Content-Length")));
xhr.send(null);
```

Note: `XMLHttpRequest` can't be used in synchronous mode because we can't change the `responseType`.

> (`responseType`) When set: throws an `InvalidAccessError` exception if the [synchronous flag](https://xhr.spec.whatwg.org/#synchronous-flag) is set
>
> — [XMLHttpRequest Standard](https://xhr.spec.whatwg.org/#the-responsetype-attribute)

## Send, load and receive data

- [Dweb: Decentralised, Real-Time, Interoperable Communication with Matrix - Mozilla Hacks - the Web developer blog](https://hacks.mozilla.org/2018/10/dweb-decentralised-real-time-interoperable-communication-with-matrix/)

### XHR

- [Browser APIs and Protocols: XMLHttpRequest - High Performance Browser Networking (O'Reilly)](https://hpbn.co/xmlhttprequest/#)

### Beacon

Equivalent APIs to use as beacon:

- `fetch("http://example.com", {keepalive: true, mode: "no-cors"})`
- `navigator.sendBeacon("http://example.com");`
- `new Image().src="http://example.com"`

`XMLHttpRequest` can't be really compared to APIs listed above, because it require CORS for cross-origin request and can't be used in `unload` event unless it use [synchronous flag](https://xhr.spec.whatwg.org/#synchronous-flag), **which is not recommended** (it's depreciated and some platforms has removed it support).

For the given data:

	const data = {
		foo: 1,
		bar: 2
	};

Send using search query

	const url = new URL("https://example.com");
	for(const [key, value] of Object.entries(data)){
		url.searchParams.set(key, value);
	}
	navigator.sendBeacon(url);

Send as URL encoded form:

	// In Chrome ?-64-? the Content-Type is incorrectly set to text/plain;charset=UTF-8
	navigator.sendBeacon("/log", new URLSearchParams(data));
	// In Chrome ?-64-? the request payload doesn't appreas in the Developer Tools (but sent)
	navigator.sendBeacon("/log", new Blob([new URLSearchParams(data)], {type: "application/x-www-form-urlencoded;charset=UTF-8"}));

Send as [multipart form data](https://developer.mozilla.org/en-US/docs/Web/API/FormData) with `FormData`:

	navigator.sendBeacon("/log", Object.entries(data).reduce((formData, [key, value]) => (formData.set(key, value), formData), new FormData()));

Send as JSON (doesn't work in Chrome 64, throw an [error](https://bugs.chromium.org/p/chromium/issues/detail?id=490015)):

	navigator.sendBeacon("/log", new Blob([JSON.stringify(data)], {type: "application/json"}));

Note: send a TypedArray will not send `Content-Type` header
Note: it is better that the server return a response with the code [`204 No Content`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/204)

- [Beacon](https://w3c.github.io/beacon/#dom-navigator-sendbeacon)
- [Navigator.sendBeacon() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)
- [Fetch keep alive flag](https://fetch.spec.whatwg.org/#request-keepalive-flag) - "allow the request to outlive the environment settings object, e.g., `navigator.sendBeacon` and the HTML `img` element set this flag"
- [WindowOrWorkerGlobalScope.fetch() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch#Parameters) - "Fetch with the `keepalive` flag is a replacement for the `Navigator.sendBeacon()` API"

### Send request without CORS

Send and forget request with fetch and opaque request:

	fetch("https://www.example/destination", {mode: "no-cors"})

or with a form and an iframe:

	<form id="form" target="iframe" action="https://www.example/destination" method="POST" style="position: fixed; visibility: hidden;">
		<iframe id="iframe" name="iframe" src="about:blank" sandbox=""></iframe>
	</form>
	<script>
		let form = document.getElementById("form");
		form.submit();
	</script>

### Image can be synchronously complete

	img.onload = () => console.log("script image onload");
	img.src = "image.png";
	console.log("script after set src");
	// Could be:
	// 1. "script after set src" then "script image onload"
	// 2. "script image onload" then "script after set src"

> The value of `complete` can thus change while a script is executing.
— http://www.w3.org/TR/html5/embedded-content-0.html#the-img-element

So complete needs to be re-checked after the callbacks have been added.
NOTE: complete will be true if the image has no src so best to check if the src is set. (TODO and the valid src="about:blank" ?)

For some browsers, loading data URI will be synchronous and won't trigger the `load` event event if it's set before `src`.

	img.src = "..."
	if(img.complete){
		// image is loaded
	}else{
		img.onload = image.onerror = image load event handler
		if(img.complete){
			img.onload = image.onerror = null
			// image is loaded
		}
	}

- `image.src = canvas.toDataURL("image/png")` is async in Chrome 57+ [514206 - Data URI image resource should be loaded async - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=514206)
- [Why does the value of img.complete can thus change while a script is executing? · Issue #1055 · whatwg/html](https://github.com/whatwg/html/issues/1055)
- https://twitter.com/kuvos/status/602167106499665922 "et tu, Chrome? `img.onload = function(){ img = null; }; log(img);` onload can fire before the log, so logs null :'( this used to be IE only."
- [`img.complete` can change](#imgcomplete-can-change)

### Image dispatch progress events

`loadstart`, `progress` and `loadend` events. Progress is dispatched only if the image is same origin or allowed with CORS

The fallback is to use XHR2 + blob URI to listen load progress.

- [Updating the image data - HTML Standard](https://html.spec.whatwg.org/#updating-the-image-data)
- [The SVG Micro DOM (uDOM) – SVG Tiny 1.2](https://www.w3.org/TR/SVGTiny12/svgudom.html#events__ProgressEvent)

### Image can dispatch multiple load events

With image with `srcset` attribute?

In case of `multipart/x-mixed-replace` image stream. But no `progress` nor `loadend` (dispatched only for the first image of the stream?)

### XHR with invalid JSON

`xhr.responseType = "json"` with invalid JSON, `xhr.response === null` and no error. You need to check your self the validity of JSON (e.g. don't use `xhr.responseType = "json"`)
It's not the case with `fetch(url).then(response => response.json())`, where the promise [will be rejected](https://github.com/github/fetch/blob/master/README.md#json).

- https://twitter.com/LeaVerou/status/726606275413315584
- https://hg.mozilla.org/mozilla-central/annotate/1461a4071341/dom/base/nsXMLHttpRequest.cpp#l964

### Fetch

fetch is a very explicit API:

- doesn't send cookies by default.
- doesn't send `Accept` header by default (image formats, html, json, etc.) the browser accept
- doesn't interpret HTTP status code as a motive of rejection (4XX or 5XX errors). See `response.ok`. Only reject for network errors (i.e. address could not be resolved, server is unreachable or CORS not permitted).
- CORS is disabled by default
- POST data must be a string (you must set the `Content-Type` header)
- abortable (using [AbortSignal](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal))
- promise will reject only for network error or CORS misconfiguration: [Using Fetch - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#Checking_that_the_fetch_was_successful)

```js
fetch(url)
	.then(response => {
		return response.json().then(data => {
			if (response.ok) {
				return data;
			} else {
				return Promise.reject({status: response.status, data});
			}
		});
	})
	.then(result => console.log('success:', result))
	.catch(error => console.log('error:', error));
```

Opaque response:

```js
fetch('https://example.com', {
	mode: 'no-cors'
})
.then(response => {
	/*
	Response {
	  body: null
	  bodyUsed: false
	  headers: Headers // always empty
	  ok: false
	  redirected: false
	  status: 0 // not a regular HTTP status code
	  statusText: "" // always empty
	  type: "opaque"
	  url: ""
	}
	*/
	return console.log(response)
}).catch(error => {
	return console.log(error)
});
```

**Note: I you store in cache API (via [Service Worker](#service-worker)) an opaque response is padded and count for around 7MB (Chrome) in quota limit. See [796060 - Cache Storage value rises on each refresh when Analytics code is in the html - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=796060#c17)**

- [CORS](#cors)
- [Using Fetch - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#Checking_that_the_fetch_was_successful)
- [Why I won’t be using Fetch API in my apps – Shahar Talmi – Medium](https://medium.com/@shahata/why-i-wont-be-using-fetch-api-in-my-apps-6900e6c6fe78)

### jsonp

jQuery can handle automatically the callback name

	$.getJSON("http://example.com/api.php?format=json&callback=?", function(data) {
		console.log(data);
	});

### Stop resource loading

**Not recommended:**

	if (window.stop !== undefined) {
		window.stop();
	}
	else if (document.execCommand !== undefined) {
		try{
			document.execCommand("Stop", false);
		}
		catch(error){}
	}

Will stop all images, scripts, stylesheet, xhr and all dependencies

- [Window.stop() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/stop)

### Cross domain access

Cross domain errors can't be catched in JS with Safari

If top domain is shared, update `document.domain`

- [Document.domain - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/domain)

### Parse URL

	new URL(location);

If not supported on old browser, you can use an `HTMLAnchorElement` (`document.createElement('a')`) to parse the URL (see `a.protocol`, `a.hostname`, `a.host`, `a.port`, `a.search`, `a.pathname`, `a.href`, `a.getAttribute("href")`)

	// don't support parameter array nor multiple param with same names
	let params = url.split("#", 1)[0].split("?").slice(1).join("?").split("&").reduce((params, pair) => {let [key, ...value] = pair.split("="); return params.set(key, decodeURIComponent(value.join("=")))}, new Map());
	let params = url.split("#", 1)[0].split("?").slice(1).join("?").split("&").reduce((params, pair) => {let [key, ...value] = pair.split("="); params[key] = decodeURIComponent(value.join("=")); return params}, {});

- [URL - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/URL)
- https://github.com/allmarkedup/purl
- http://james.padolsey.com/javascript/parsing-urls-with-the-dom/

#### Querystring

```js
new URLSearchParams(location.search)
```

```js
let params = {};
let search = Object.keys(params).map(key => encodeURIComponent(key) + "=" + encodeURIComponent(params[key])).join("&");
```

- [Javascript Madness: Query String Parsing](http://unixpapa.com/js/querystring.html)

### Custom HTTP authentification

The client should send `Authorization: somecredentials` header with custom method

The server should return `401 Unauthorized` with `WWW-Authenticate: MyCustomScheme` (scheme/challenge) if not `Authorization` header provided or indicate the provided credential is wrong

Like [WSSE](http://www.xml.com/pub/a/2003/12/17/dive.html)

- http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.4.2
- https://stackoverflow.com/questions/928874/how-do-i-keep-firefox-from-prompting-for-username-password-with-http-basic-auth
- https://stackoverflow.com/questions/1748374/http-401-whats-an-appropriate-www-authenticate-header-value
- https://stackoverflow.com/questions/9137611/how-to-prevent-safari-from-intercepting-401-responses-to-ajax-requests
- http://symfony.com/doc/master/cookbook/security/custom_authentication_provider.html
- http://www.teria.com/~koseki/tools/wssegen/

### Upload a generated binary data

	function upload(blobOrFile) {
		var xhr = new XMLHttpRequest();
		xhr.open('POST', 'https://httpbin.org/post', true);
		xhr.onload = e => {
			alert('Fully uploaded');
		};

		var progressBar = document.querySelector('progress');
		xhr.upload.onprogress = e => { // track upload progress
			if (e.lengthComputable) {
				progressBar.value = (e.loaded / e.total) * 100;
			}
		};

		xhr.send(blobOrFile);
	}

	button.addEventListener("click", () => {
		//upload(new File(["Hello world!"], "data.txt", {type: "text/plain"}));

		let mediatype = "image/png";
		let extension = ".png"
		canvas.toBlob(blob => {
			upload(new File([blob], `image${extension}`, {type: mediatype}));
		}, mediatype)

	});

### Network cache

Use blob to store RAW data

	var xhr = new XMLHttpRequest();
	xhr.open("GET", imageURL, true);
	xhr.responseType = "arraybuffer";
	xhr.onload = function() {
		var img = new Image();
		img.onload = function() {
			URL.revokeObjectURL(this.src);
			var tex = new THREE.Texture(this);
			//do something with this texture...
		};
		var blob = new Blob([xhr.response], {type : xhr.getResponseHeader("Content-Type") || 'application/octet-binary'});
		img.src = URL.createObjectURL(blob);
	};
	xhr.send(null);

See also cache API:

- [Cache - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Cache)
- [Using the Cache API  |  Web Fundamentals  |  Google Developers](https://developers.google.com/web/fundamentals/instant-and-offline/web-storage/cache-api)

### Service Worker

- [service worker receive fragment identifier (hash) in requests and can use fragment identifier in responses](https://github.com/w3c/ServiceWorker/issues/854), see also [Fetch API: Request#url includes the URL fragment - Chrome Platform Status](https://www.chromestatus.com/feature/4753419730419712)
- clone requests before reuse it: `self.addEventListener("fetch", event => event.respondWith(fetch(event.request.clone()))`, or it will throw `Cannot construct a Request with a Request object that has already been used.`
- you can't install service worker from data URI (`data:application/javascript,console.log('hello')`), but `importScripts` can (with Chrome, but not with Firefox "NetworkError: Failed to load worker script at data:...")
- "the scope determines which pages are controlled by the service worker. Once a page is controlled by a service worker, all HTTP requests originating from the page [...] will trigger the service worker's `fetch` event": [javascript - Understanding Service Worker scope - Stack Overflow](https://stackoverflow.com/questions/35780397/understanding-service-worker-scope#comment59275020_35780776)
- add listeners for `pushsubscriptionchange`, `install`, `push`, `notificationclick`, `message`, etc. events must be made  synchronously ("initial evaluation of worker script"), see ["The user agents are encouraged to show a warning that the event listeners must be added on the very first evaluation of the worker script."](https://www.w3.org/TR/service-workers/#run-service-worker)
- hash in location of the service worker are ignored (not available in worker scope: `self.location.hash === ""`)
- require HTTPS (with a verified certificate)
- fetch event handlers will be triggered in the order in which they were registered, until the first call is made to `event.respondWith()`. See [javascript - Sharing fetch handler logic defined across multiple service workers - Stack Overflow](https://stackoverflow.com/questions/45257602/sharing-fetch-handler-logic-defined-across-multiple-service-workers)
- service worker script is redownloaded at least each 24h (cache is max 24h). See [Service worker JavaScript update frequency (every 24 hours?) - Stack Overflow](https://stackoverflow.com/questions/38843970/service-worker-javascript-update-frequency-every-24-hours/38854905#38854905)
- [the max scope](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerContainer/register#Parameters) can be changed with the HTTP header `Service-Worker-Allowed`. See [Using Service Workers - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers#Why_is_my_service_worker_failing_to_register)
- use [`registration.update()`](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerRegistration/update) to force the update of the service worker script
- use [`fetchEvent.clientId`](https://developer.mozilla.org/en-US/docs/Web/API/FetchEvent/clientId): to get the controlled client id
- [ServiceWorker Cookbook](https://serviceworke.rs/)
- can be used for polyfill Client Hints
- [Service Worker & HTTP Client Hints](https://gist.github.com/deanhume/c04478df744ce833925c) - Rewrite URL if WebP is supported
- [Using Service Worker for server-side adaption based on network type - Tales of a Developer Advocate by Paul Kinlan](https://paul.kinlan.me/using-service-worker-server-side-adaption-based-on-network-type/) - Example (but shouldn't used as is) to send client Hint network infos
- [Service Workers — Gotchas — Medium](https://medium.com/@boopathi/service-workers-gotchas-44bec65eab3f)
- [delapuente/service-workers-101: An infographic to summarize the most important parts of the Service Workers' API](https://github.com/delapuente/service-workers-101/)
- [Service Worker, what are you? - Mariko Kosaka](http://kosamari.com/notes/Service-Worker-what-are-you)
- [javascript - What limitations apply to opaque responses? - Stack Overflow](https://stackoverflow.com/questions/39109789/what-limitations-apply-to-opaque-responses/39109790#39109790)
- [Workbox  |  Google Developers](https://developers.google.com/web/tools/workbox/) - A framework to handle cache in service worker
- [javascript - Understanding Service Worker scope - Stack Overflow](https://stackoverflow.com/questions/35780397/understanding-service-worker-scope) - `Service-Worker-Allowed` HTTP header to define the max scope

Avoid changing the URL of service worker script:

> If you've read [my post on caching best practices](https://jakearchibald.com/2016/caching-best-practices/), you may consider giving each version of your service worker a unique URL.
> **Don't do this!** This is usually bad practice for service workers, just update the script at its current location.
>
> It can land you with a problem like this:
>
> 1. `index.html` registers `sw-v1.js` as a service worker.
> 2. `sw-v1.js` caches and serves `index.html` so it works offline-first.
> 3. You update `index.html` so it registers your new and shiny `sw-v2.js`.
>
> If you do the above, the user never gets `sw-v2.js`, because `sw-v1.js` is serving the old version of `index.html` from its cache. You've put yourself in a position where you need to update your service worker in order to update your service worker.
>
> — [The Service Worker Lifecycle  |  Web Fundamentals  |  Google Developers](https://github.com/google/WebFundamentals/blob/72658bac3b48b9a57033e35fe9d585252daeaeb0/src/content/en/fundamentals/primers/service-workers/lifecycle.md)

Handle too long response (force third parties SLA)

```js
function timeout(delay){
	return new Promise((resolve, reject) => {
		setTimeout(() => {
			resolve(new Response("",  {
				status: 408,
				statusText: "Request timed out.",
			}));
		}, delay);
	});
}

self.adEventListener("fetch", event => {
	event.respondWith(Promise.race([timeout(2000), fetch(event.request)]));// handmade response or opaque response
});
```

Do some tasks before complete the installation (fill cache, dynamic additional `importScripts`, dynamic event listeners, etc.):

```js
addEventListener("install", event => {
  event.waitUntil(async function() {
// additional importScripts based on config, etc.
    const [cache, urls] = await Promise.all([
      caches.open("static-v1"),
      idbKeyval.get("urlsToCache")
    ]);
    await cache.addAll(urls);
  }());
});
```

See [Proposal: pass custom params in ServiceWorkerRegistration for future use · Issue #1157 · w3c/ServiceWorker](https://github.com/w3c/ServiceWorker/issues/1157#issuecomment-306469745) and [Fix the ServiceWorker mode to create the event handlers on the initial evaluation of the script · Issue #189 · kiwix/kiwix-js](https://github.com/kiwix/kiwix-js/issues/189)

### Streamed data

Aka URLStream

With `XMLHttpRequest`:

	var xhr = new XMLHttpRequest();
	var bytesLoaded = 0;
	xhr.open("GET", "streamed_data");
	xhr.overrideMimeType("text/plain; charset=x-user-defined");// if loaded content should be read as bytes, else remove it
	// because, for xhr.response: "If state is not done, return null." (for `xhr.responseType = "arraybuffer";`). See https://xhr.spec.whatwg.org/#dom-xmlhttprequest-response
	xhr.addEventListener("progress", event => {
		var chunk = xhr.response.slice(bytesLoaded);
		// process data chunk
		// ex: var firstChunkByte = chunk.charCodeAt(0);

		bytesLoaded = xhr.response.length;
	});
	xhr.send();

With `ReadableStream`:

Using [Newline delimited JSON (NDJSON)](http://specs.okfnlabs.org/ndjson/)

	// each lines are a JSON data
	const response = await fetch("comments.ndjson");
	const comments = response.body
		// From bytes to text:
		.pipeThrough(new TextDecoder())
		// Buffer until newlines:
		.pipeThrough(splitStream("\n"))
		// Parse chunks as JSON:
		.pipeThrough(parseJSON());

	for await (const comment of comments) {
		// Process each comment and add it to the page:
		// (via whatever template or VDOM you're using)
		addCommentToPage(comment);
	}

- [Fun hacks for faster content - JakeArchibald.com](https://jakearchibald.com/2016/fun-hacks-faster-content/#newline-delimited-json)

### Partial content

Note: **get a resource with `Range` header doesn't mean you will always get a response 206 and only the chunk you ask for**. Can be more data than requested (all, or a larger chunk)

	var xhr = new XMLHttpRequest;
	xhr.responseType = "arraybuffer";
	xhr.addEventListener("load", event => {
		console.log(xhr.status, xhr.getResponseHeader("Content-Range") || "no Content-Range header received", `${xhr.response.length} bytes (${xhr.getResponseHeader("Content-Length") || "no Content-Length head received"})`);
		// If no Content-Range header: all content is available, else read A-B/X (where X is the total bytes available)
	});

	xhr.open("GET", "image.png");
	xhr.setRequestHeader('Range', 'bytes=0-101'); // the 101 first bytes
	xhr.send(null);

- [javascript - XMLHttpRequest 206 Partial Content - Stack Overflow](https://stackoverflow.com/questions/15561508/xmlhttprequest-206-partial-content)

### WebSocket keep alive

	let timerId = 0;
	function keepAlive() {
		let timeout = 20000;
		if (webSocket.readyState == webSocket.OPEN) {
			webSocket.send('');
		}
		timerId = setTimeout(keepAlive, timeout);
	}
	function cancelKeepAlive() {
		if (timerId) {
			cancelTimeout(timerId);
		}
	}

### WebRTC

- [A real world guide to WebRTC](https://deepstreamhub.com/tutorials/protocols/webrtc-intro/) - [deepstreamIO/dsh-demo-webrtc-examples](https://github.com/deepstreamIO/dsh-demo-webrtc-examples/tree/master/) and [A real world guide to WebRTC | Hacker News](https://news.ycombinator.com/item?id=14787285)
- [How Zoom's web client avoids using WebRTC (DataChannel Update) - webrtcHacks](https://webrtchacks.com/zoom-avoids-using-webrtc/)

### Event Source

Aka Server-Sent Events

- [Using server-sent events - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events)
- [Yaffle/EventSource: a polyfill for http://www.w3.org/TR/eventsource/](https://github.com/Yaffle/EventSource#example)
- [Stream Updates with Server-Sent Events - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/eventsource/basics/)

### Push Notification

It's unrelated to [Notification API](https://developer.mozilla.org/en-US/docs/Web/API/Notifications_API)

One subscription channel per device / account on device. If the use visit the application on both mobile and desktop he potentially subscribe 2 times (un related). The server app could choose which one to send (like the mobile), but it's not pratical.

The endpoint is related to (provided by) the browser vendor (["There is only one push service per user agent"](https://www.w3.org/TR/push-api/#dfn-push-services), ex: Google `https://fcm.googleapis.com/fcm/send/xxxx`, Mozilla `https://updates.push.services.mozilla.com/update/xxxx`, etc. [Endpoint · web-push-libs/webpush-java Wiki](https://github.com/web-push-libs/webpush-java/wiki/Endpoints)). Only the application server use that endpoint to send notification (with credentials) using [Web Push Protocol](https://tools.ietf.org/html/rfc8030)

- [How Chrome Notification Subscription I Managed By Chrome](https://blog.izooto.com/here-is-why-you-are-getting-same-web-push-notifications-twice-on-chrome/)
- [Design - Mozilla Push Service Documentation](http://mozilla-push-service.readthedocs.io/en/latest/design/#simplepush-protocol) [Mozilla Push Service Documentation](http://mozilla-push-service.readthedocs.io/en/latest/)
- [web-push-libs/web-push-php: Web Push library for PHP](https://github.com/web-push-libs/web-push-php)
- [web-push](https://www.npmjs.com/package/web-push)
- [Sending VAPID identified WebPush Notification via Mozilla’ Push Service | Mozilla Services](https://blog.mozilla.org/services/2016/08/23/sending-vapid-identified-webpush-notifications-via-mozillas-push-service/)
- [web-push-libs](https://github.com/web-push-libs)
- [Push Companion](https://web-push-codelab.glitch.me/)

### WebSocket and streaming

See [Web — Streaming](Web#streaming)

### CORS

- [Send request without CORS](#send-request-without-cors)
- [Handle Third Party Requests  |  Workbox  |  Google Developers](https://developers.google.com/web/tools/workbox/guides/handle-third-party-requests#remember_to_opt-in_to_cors_mode)
- [javascript - Deadly CORS when http://localhost is the origin - Stack Overflow](https://stackoverflow.com/questions/10883211/deadly-cors-when-http-localhost-is-the-origin/10892392#10892392)

## `javascript:` protocol is async

It's navigation

`anchor.click()` or `anchor.dispatchEvent(new MouseEvent("click"))` on a link with `href = "javascript:test()"` will execute `test()` asynchronously.

**Never use link with `javascript:` protocol.**

The workaround is use `eval(anchor.href)` instead.

- [HTML Standard](https://html.spec.whatwg.org/multipage/browsers.html#navigating-across-documents:javascript-protocol) - Navigating across documents: "javascript" url scheme

## Why return undefined for `javascript:` URIs

```
javascript:void window.open("http://example.com/");
```

- http://speakingjs.com/es5/ch09.html#_what_is_void_used_for

## Catch global errors

```js
window.onerror = function (errorMsg, url, lineNumber, column, errorObj) {
	if (errorMsg.indexOf("Script error.") > -1) {
		return;
	}
	//alert('Error: ' + errorMsg + ' Script: ' + url + ' Line: ' + lineNumber
		+ ' Column: ' + column + ' StackTrace: ' +  errorObj);
}

window.onerror = function(message, url){
	/* critical error or same host script */
	if(message.match("Uncaught TypeError") || url.includes(location.host)){
		/*show fallback content*/
	}
}
```

- [Daniel Grant on Twitter: "Considering if it would be a good idea to pessimistically fallback to non-JS layout whenever there' a seriou error… "](https://twitter.com/djgrant_/status/734438032716271616)
- [Capture and Report JavaScript Error with window.onerror — SitePoint](https://www.sitepoint.com/capture-and-report-javascript-errors-with-window-onerror/#browsercompatibility)

## Get matched CSS rules

Get applied CSS rules.

```js
// It's a naive way. Stylesheet can be disabled, inaccessible, nested - via `@import` - or contains nested rules
function getMatchedCSSRules(a) {
	var sheets = document.styleSheets, o = [];
	for (var i in sheets) {
		var rules = sheets[i].rules || sheets[i].cssRules;
		for (var r in rules) {
			if (a.matches(rules[r].selectorText)) {
				o.push(rules[r]);
			}
		}
	}
	return o;
}
```

**Note: `window.getMatchedCSSRules` is depreciated**

- https://github.com/anselmh/object-fit/blob/master/src/polyfill.getMatchedCSSRules.js
- [javascript - Find all CSS rules that apply to an element - Stack Overflow](https://stackoverflow.com/questions/2952667/find-all-css-rules-that-apply-to-an-element)
- https://gist.github.com/ydaniv/3033012/forks
- [\[brothercake\] CSSUtilities](http://www.brothercake.com/site/resources/scripts/cssutilities/)
- http://jsfiddle.net/HP326/62/

## User location

- [Legal Guidelines For The Use Of Location Data On The Web – Smashing Magazine](https://www.smashingmagazine.com/2016/03/location-data-web-development-and-the-law/)

## Intersection observer

Element in viewport: Observing Position

https://github.com/WICG/IntersectionObserver

## Sync medias

Ex.: Sync 2 videos of same scene but with different view point.

> You can not rely on HTML5 video events

Because:

> - The suspend event were our biggest hope, but it actually doesn’t act like it should.
> - Once the video started, the canplay / canplaythrough / loadedmetadata events are effectively emitted but never again.
> - The pause event is triggered only when user pauses the video, not when the video was paused because of buffering.

Solutions:

> on each frame ( requestAnimationFrame ), check the currentTime continually against the buffer length

or

> on each frame, check if current timestamp minus “last time the video was updated” is inferior to a certain threshold

- [HTML5 Video](https://www.w3.org/2010/05/video/mediaevents.html)

## WebAssembly

- [Extending the browser with WebAssembly  |  Web  |  Google Developers](https://developers.google.com/web/updates/2018/08/wasm-av1)
- [Build your own WebAssembly Compiler](https://blog.scottlogic.com/2019/05/17/webassembly-compiler.html)
- [Strings in WebAssembly (Wasm) - Wasm - Medium](https://medium.com/wasm/strings-in-webassembly-wasm-57a05c1ea333)
- [What’s in that .wasm? Introducing: wasm-decompile · V8](https://v8.dev/blog/wasm-decompile)

Usage examples:

- compression
- games
- video editing
- text editors
- data visualisation
- deep learning
- stream processing
- data validation
- cryptography
- path finding
- encoding and decoding
- parallelisation
- transcoding
- custom file formats

### Shared memory can be used by pure JavaScript

Note: "When memory block is reallocated, the old ArrayBuffer gets invalidated, because the memory block it was pointing to might be no longer valid.". "the .grow doesn't invalidate old data, it just reallocates it to fit a new size."

```js
// Create a Worker we want to share memory with:
let w = new Worker(`data:text/javascript,
onmessage = ({data: memory}) => {
  // Got WebAssembly.Memory once, log same instance forever with no further postMessages:
  setInterval(() => console.log('Current buffer in worker:', memory.buffer), 5_000);
}
`);
// Create a shared growable memory:
let m = new WebAssembly.Memory({ initial:1, maximum: 65536, shared: true });
// Send memory to the worker:
w.postMessage(m);

// ... within 5 seconds you should see SharedArrayBuffer(65536) in the console, coming from the Worker

// Now, let's grow memory by one page from the main thread:
m.grow(1);

// ... within 5 seconds you should see SharedArrayBuffer(131072) in the console
// This demonstrates that the previously shared memory object auto-updates on growth.
```

### asm.js

Note: asm.js is replaced by WebAssembly

```js
a = x + y | 0// integer arithmetic x: int32, y: int32
a = +(x + y)// double arithmetic x: float64, y: float64
(a >>> 0) < (b >>> 0) // unsigned comparison
```

```js
var buffer = new ArrayBuffer(16 * 1024 * 1024);
function module(buffer, stdlib) {
  “use asm”;
  var heap8 = new Int8Array(buffer);
  function foo(a) {
	a = a | 0;
	return heap8[a] + 1 | 0;
  }
  return {foo: foo}
}
var mod = module(buffer, {print: print});
mod.foo(100);
```

## Passive Event Listeners

> onscroll is async, so passive is unnecessary. Only needed for touch* and wheel events.
— Paul Irish https://twitter.com/paul_irish/status/755175394140053505

There no drawback when using passive even if not necessary.

## Event loop

```js
const el = document.createTextNode("");
new MutationObserver(() => console.log("Mutation observer say hello!")).observe(el, {characterData: true});
el.textContent = "a";
requestAnimationFrame(() => console.log("Animation frame say hello!"));
setTimeout(() => console.log("Timeout say hello!"));
```

## Page focus

	document.defaultView.addEventListener("blur", pageStateChange);
	document.defaultView.addEventListener("focus", pageStateChange);
	document.addEventListener("visibilitychange", pageStateChange);// listen also webkitvisibilitychange
	function pageStateChange(){
		var inactive = document.hidden || !this._document.hasFocus();
	}

## Click with touch

Like click but with touch only (not mousedown, mouseup)

**TODO**

```js
// Touch simili hover
var countries = document.querySelectorAll(".dsp-country-wrp");
var currentTouchedCountry = null;
var startTouchedTarget = null;
function documentTouchStart(event){
	startTouchedTarget = event.target;
}
function documentTouchEnd(event){
	var target = event.target;
	var touchedCountry = null;
	if(event.type == "touchend"){
		for(var i = 0; i < countries.length; i++){
			var pos = target.compareDocumentPosition(countries[i]);
			if(pos == 0 || pos & 8){//self || Node.DOCUMENT_POSITION_CONTAINS
				touchedCountry = countries[i];
				break;
			}
		}
	}

	if(currentTouchedCountry == touchedCountry){
		return;// don't click twice
	}

	// Like click but with touches
	if(touchedCountry == startTouchedTarget && touchedCountry != currentTouchedCountry){
		country.classList.add("dsp-country-wrp--active");
	}else{
		lastCountryTouched.classList.remove("dsp-country-wrp--active");
	}

	currentTouchedCountry = touchedCountry;
}
document.addEventListener("touchstart", documentTouchEnd);
document.addEventListener("touchcancel", documentTouchEnd);
document.addEventListener("touchend", documentTouchEnd);
```

Or simply use touchstart only:

```js
var countries = document.querySelectorAll(".dsp-country-wrp");
var currentTouchedCountry = null;
function documentTouchStart(event){
	var touchedCountry = null;

	for(var i = 0; i < countries.length; i++){
		var pos = event.target.compareDocumentPosition(countries[i]);
		if(pos == 0 || pos & 8){//self || Node.DOCUMENT_POSITION_CONTAINS
			touchedCountry = countries[i];
			break;
		}
	}

	if(touchedCountry === currentTouchedCountry){
		return;
	}

	if(currentTouchedCountry){
		currentTouchedCountry.classList.remove("dsp-country-wrp--active");
	}
	if(touchedCountry){
		touchedCountry.classList.add("dsp-country-wrp--active");
	}
	currentTouchedCountry = touchedCountry;
}
document.addEventListener("touchstart", documentTouchStart);
```

## Localize data

```js
let options = {month: 'long', day: 'numeric', year: 'numeric'};
(new Date()).toLocaleString('en-us', options);// -> "October 5, 2016"
(new Date()).toLocaleString('en', options);// -> "October 5, 2016"
(new Date()).toLocaleString('de', options);// -> "5. Oktober 2016"
(new Date()).toLocaleString('fr', options);// -> "5 octobre 2016"
(new Date()).toLocaleString('hi', options);// -> "5 अक्तूबर 2016"
(new Date()).toLocaleString('zh-Hans-CN', options);// -> "2016年10月5日"

let amount = 1034532;
let options = {style: "currency", currency: "CAD"};
amount.toLocaleString("en-US", options);// -> "CA$1,034,532.00"
amount.toLocaleString("de-DE", options);// -> "1.034.532,00 CA$"
amount.toLocaleString("ar-EG", options);// -> "CA$ ١٬٠٣٤٬٥٣٢٫٠٠"
```

- [Date.prototype.toLocaleString() - JavaScript | MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString)
- [JavaScript Internationalization API | WebKit](https://webkit.org/blog/6978/javascript-internationalization-api/)

## Stack size and heap size

> RangeError: Maximum call stack size exceeded

Maxium of local variables per function (all function compared) will affect also the stack max size

> each function call takes up 48 bytes during the execution, and you are limited to less than 1MB for all local function frames.
> [...]
> Each boolean and number variable takes 8 bytes of memory.
> Only primitive types passed by value (Number, Boolean, references to objecs) are stored on the stack.
> Everything else is allocated dynamically from the shared pool of memory called heap

- [The maximum call stack size](http://www.2ality.com/2014/04/call-stack-size.html)
- [JavaScript stack size - Better world by better software](http://bahmutov.calepin.co/javascript-stack-size.html)

> Find and expand the `closure` property. It will show the contents of the closure, as well as properties of the closure object itself. Color coding is used to distinguish closure variables from properties.
> Find and expand the `consString` property. It will exhibit, that a concatenated string is stored as a linked list of its parts.
>
> — [Exploring the Heap Contents - Google Chrome](https://developer.chrome.com/devtools/docs/heap-profiling-containment) https://github.com/GoogleChrome/devtools-docs/blob/master/docs/heap-profiling-containment.html

- [How to Record Heap Snapshots  |  Web  |  Google Developers](https://developers.google.com/web/tools/chrome-devtools/memory-problems/heap-snapshots)

See [Garbage collecting and references](#garbage-collecting-and-references)

## Font metrics

See [Font metrics](CSS#font-metrics)

- [Calculate the cap height of fonts loaded with Web Font Loader](https://github.com/sebdesign/cap-height) - Use canvas to get font metrics
- [TextMetrics - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/TextMetrics)
- `text-rendering: optimizeLegibility;`

### Char kerning

**It's not perfect, because ligatures**

```js
let context = document.createElement("canvas").getContext("2d");
let fontSize = 48;
context.font = `${fontSize}px myfont`;
var kerning = context.measureText("a").width + context.measureText("v").width - context.measureText("av").width;
```

- `letter-spacing: 0`

## Read and write cookies

```js
// Read one cookie
var value = (document.cookie.match(/(?:^|;\s*)cookiename=([^;]*?)(?:\s*;)/) || [, ""])[1];// es5
//const [, value = ""] = document.cookie.match(/(?:^|;\s*)cookiename=([^;]*?)(?:\s*;)/];// es6

// const value = !!document.cookie.split(";").find(pair => /cookiename(\s*=\s*true|$)/.test(pair.trim()));// document.cookie = "cookiename=true"

// Read cookies (returns Map)
const cookies = document.cookie.split(";").reduce((cookies, pair) => {const [key, , ...valueChunks] = pair.trim().split(/\s*(=)\s*/); return cookies.set(key, decodeURIComponent(valueChunks.join("")))}, new Map());// cookie-pair *( ";" SP cookie-pair )
// Read cookies (returns Object)
const cookies = document.cookie.split(";").reduce((cookies, pair) => {const [key, , ...valueChunks] = pair.trim().split(/\s*(=)\s*/); cookies[key] = decodeURIComponent(valueChunks.join("")); return cookies}, {});// cookie-pair *( ";" SP cookie-pair )

// erase a cookie
document.cookie = "cookiename=;domain=example.com;path=/;expires=Thu, 01 Jan 1970 00:00:01 GMT";

// write a cookie
const value = "value";
const path = "/";
const domain = location.hostname.split(".").slice(-2).join(".");
const expires = new Date(Date.now() + 90*24*60*60*1000);// now +90 days
document.cookie = `cookiename=${encodeURIComponent(value)};path=${encodeURIComponent(path)};domain=${domain};expires=${expires.toUTCString()}`;
```

[Proxying of `document.cookie`](https://stackoverflow.com/questions/32410331/proxying-of-document-cookie):

```js
const cookieDesc = Object.getOwnPropertyDescriptor(Document.prototype, "cookie") || Object.getOwnPropertyDescriptor(HTMLDocument.prototype, "cookie");
if (cookieDesc && cookieDesc.configurable) {
    Object.defineProperty(document, "cookie", {
        get: function () {
            return cookieDesc.get.call(document);
        },
        set: function (val) {
            debugger;
            cookieDesc.set.call(document, val);
        }
    });
}
```

**TODO write:**

```
name[=value];
path,//cookie path
expires,//absolute expiration date for the cookie (Date object)
maxAge,//relative max age of the cookie from when the client receives it (seconds)
domain//domain for the cookie
secure
httpOnly
```

- Detect if cookies are enabled https://github.com/Modernizr/Modernizr/blob/master/feature-detects/cookies.js (Note: Server side scripts need a redirection to check if cookies are enabled)
- [RFC 6265 - HTTP State Management Mechanism](https://tools.ietf.org/html/rfc6265)
- https://github.com/jshttp/cookie

## Ready state

- `uninitialized`: Object is not initialized with data.
- `loading`: Object is loading its data.
- `loaded`: Object has finished loading its data.
- `interactive`: User can interact with the object even though it is not fully loaded.
- `complete`: Object is completely initialized.

`readystatechange` and `load` events

- [readyState property - Windows app development](https://msdn.microsoft.com/en-us/library/windows/apps/hh780200.aspx)

## Throw errors / exceptions

```js
throw new DOMException("The object is in an invalid state.", "InvalidStateError");
throw new Error("The object is in an invalid state.");
```

When a promise is used, the exception or error can be the reason of the promise's rejection.

- [DOMException - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/DOMException)
- [Web IDL](https://heycam.github.io/webidl/#idl-DOMException-error-names)
- [Error - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error#Error_types)
- [Control flow and error handling - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling#Exception_handling_statements)

## Replace `setTimeout()` and `setInterval()` with `requestAnimationFrame()`

Drop in replacements for setTimeout()/setInterval() that makes use of requestAnimationFrame() where possible for better performance

https://gist.github.com/joelambert/1002116#gistcomment-1953925

## Server Push

- non standardized methods (but valid)
	Send chunks of data over the same [persistent connection](https://en.wikipedia.org/wiki/HTTP_persistent_connection)

	- `multipart/x-mixed-replace`
	- chunk encoding
	- [long polling](https://en.wikipedia.org/wiki/Push_technology#Long_polling) see [How to implement COMET with PHP](http://www.zeitoun.net/articles/comet_and_php/start)
- Server-sent events / SSE
	- [Server-sent events](https://en.wikipedia.org/wiki/Server-sent_events)
	- [Using server-sent events - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events)
	- [Stream Updates with Server-Sent Events - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/eventsource/basics/)
	- [Server-Sent Events: The simplest realtime browser spec](https://segment.com/blog/2014-04-03-server-sent-events-the-simplest-realtime-browser-spec/)
	- [Server-Sent Events | HTML5 Doctor](http://html5doctor.com/server-sent-events/)
	- [Server-sent Events](https://www.sitepoint.com/server-sent-events/)
	- [php - Server sent events - text/event-stream ocasionally misenterpreted as text/html by chrome and firefox - Stack Overflow](https://stackoverflow.com/questions/31430839/server-sent-events-text-event-stream-ocasionally-misenterpreted-as-text-html-b)
- Websocket
- WebRTC

See also [JSONRequest](http://www.json.org/JSONRequest.html) `application/jsonrequest`

## iframe navigation create history entries

But if you nest an iframe inside an other iframe, no more history entries will be created

## Storage

Cookies can have there origin relaxed (in fact can use parent domain, see [Same-origin policy - Web security | MDN](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy#Changing_origin)) with `Secure` (not set allow both HTTP and HTTPS), [`Domain` and `Path`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#Scope_of_cookies)

Others APIs like `localStorage` can't have their cross domain origin relaxed like Cookies could.

- [Same-origin policy - Web security | MDN](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy#Cross-origin_data_storage_access) - "Cross-origin data storage access"
- [html5 - HTML 5 Storage's same origin policy - Stack Overflow](https://stackoverflow.com/questions/6645943/html-5-storages-same-origin-policy)
- [HTML Standard](https://html.spec.whatwg.org/multipage/webstorage.html#dom-localstorage)
- [HTML Standard](https://html.spec.whatwg.org/multipage/origin.html#concept-origin)

### Client database storage performances

- DOM Storage (`localStorage` and `sessionStorage`) is useful for storing smaller amounts of data
- IndexedDB is asynchronous

- [IndexedDB, WebSQL, LocalStorage – what blocks the DOM? | Read the Tea Leaves](https://nolanlawson.com/2015/09/29/indexeddb-websql-localstorage-what-blocks-the-dom/)

## Context messaging

iframe, window, worker, etc.

> `MessageChannel` is basically a 2-way communication pipe. Think of it as an alternative to `window.postMessage` / `window.onmessage` - but a somewhat easier and more configurable.

```js
const ch = new MessageChannel();

ch.port1.addEventListener('message', …);
ch.port1.start();

//vs
ch.port1.onmessage = …;
//ch.port1.start(); is automatically called
```

Note: if you listen an iframe with `sandbox` attribute that dispatch `message` events, you need to add `allow-same-origin`, else `event.origin` will always be equal to `"null"`. See [javascript - PostMessage from a sandboxed iFrame to the main window, origin is always null - Stack Overflow](https://stackoverflow.com/questions/37838875/postmessage-from-a-sandboxed-iframe-to-the-main-window-origin-is-always-null)

- [Dev.Opera — An Introduction to HTML5 Web Messaging](https://dev.opera.com/articles/window-postmessage-messagechannel/)
- [Using channel messaging - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Channel_Messaging_API/Using_channel_messaging)
- [Communicating between Web Workers via MessageChannel](http://www.2ality.com/2017/01/messagechannel.html)
- [html5 - Is cross-origin postMessage broken in IE10? - Stack Overflow](https://stackoverflow.com/questions/16226924/is-cross-origin-postmessage-broken-in-ie10)

## Postmessage

- [Is postMessage slow? — DasSur.ma](https://dassur.ma/things/is-postmessage-slow/)

## Canvas cursor

- [cursory hack](https://github.com/benfoxall/cursory-hack)
- [Custom animated cursor via canvas / Stoyan's phpied.com](http://www.phpied.com/custom-animated-cursor-via-canvas/)
- [Using URL values for the cursor property - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_User_Interface/Using_URL_values_for_the_cursor_property)

## Can play type

Aka can play media type

- `probably` if the browser is fairly confident it can play this format
- `maybe` if the browser thinks it might be able to play this format
- `` (an empty string) if the browser is certain it can't play this format

> Generally, a user agent should never return "probably" for a type that allows the codecs parameter if that parameter is not present.
>
> — [4.7 Embedded content — HTML5](http://www.w3.org/TR/html5/embedded-content-0.html#dom-navigator-canplaytype)

## `href` property vs `getAttribute()`

- `link.href`: full URL
- `link.getAttribute()`: what’s in source

- [javascript - getAttribute() versus Element object properties? - Stack Overflow](https://stackoverflow.com/questions/10280250/getattribute-versus-element-object-properties)

## Single page application

Aka SPA

- [The disadvantages of single page applications | Adam Silver | UX design, Front-end Engineering and Strategy | London, UK.](http://adamsilver.io/articles/the-disadvantages-of-single-page-applications/)

## Inline video

- [JSMpeg – MPEG1 Video & MP2 Audio Decoder in JavaScript](https://github.com/phoboslab/jsmpeg) and [MPEG1 Video Decoder in JavaScript - PhobosLab](http://phoboslab.org/log/2013/05/mpeg1-video-decoder-in-javascript) [JSMpeg – Decode it like it's 1999](http://jsmpeg.com/)

Screen sharing:

> ffmpeg -f avfoundation -i 1 -f mpegts -codec:v mpeg1video -b:v 100k -bf 0 http://127.0.0.1:8083/secret

## Bookmarklet

See [Bookmarklet](Web#bookmarklet)

```
javascript:{code;undefined}

javascript:(s=>{s=`Hello ${s}!`;alert(s)})("World")
```

Last instruction should return undefined (like `undefined` or `void(0)`), or the current page will navigate to a page with the result as HTML body. Ex: `javascript:"<b>Bold text</b>"`

Copy current document as Markdown link bookmarklet (see [Clipboard API](#clipboard-api)):

```js
// Encode with Uglify3 https://skalman.github.io/UglifyJS-online/
// copy("javascript:"+document.getElementById("out").value.replace(/[\s#%]/g, match => "%" + match.charCodeAt(0).toString(16).padStart(2, "0"))+"void(0)")
{
	let doc = document;
	let url = doc.URL;
	let title = [doc.title].concat(Array.from(doc.querySelectorAll("h1,h2"), element => element.textContent.replace(/\s+/g," ")), url)
		.reduce((title, value) => title || value.trim(), "");
	let encodeChars = (str, regexp, prefix = "&#x", suffix = ";") => str.replace(regexp, match => prefix + match.charCodeAt(0).toString(16).padStart(2, "0") + suffix);
	let escapedURL = encodeChars(url, /[()"]/g, "%", "");
	let isImage = doc.contentType.startsWith("image/");
	// expreg should match "file" for "/file.ext"; "file" for "/file"; "file.a" for "/file.a.ext"
	let [, filename = "Untitled"] = /\/([^/.]+$|[^/]+(?=\.[^.]*$))/g.exec(new URL(url).pathname) || [];
	filename += "." + doc.contentType.split("/")[1].split("+")[0];// base extension on Content-Type subtype https://www.iana.org/assignments/media-types/media-types.xhtml#image
	// execCommand will not been executed if a frame or an iframe is focused
	if(["IFRAME","FRAME"].includes(doc.activeElement.tagName)){
		let focusable = doc.createElement("span");
		focusable.tabIndex = -1;// focusable
		focusable.setAttribute("aria-hidden", "true");// will not be announced by AT
		focusable.style.position = "fixed";
		doc.documentElement.appendChild(focusable);// don't use doc.body because in case of frame the body is the frameset and execCommand will not work
		focusable.focus();// force focus, but will not scroll into view, because it have fixed position
		focusable.remove();// remove focus, without force to scroll into view to an other element
	}

	//TODO support SVGDocument (execCommand only exist on HTMLDocument) by create a iframe about:blank inside a foreignObject
	doc.addEventListener("copy", event => {
		let clipboardData = event.clipboardData;
		let setData = clipboardData.setData.bind(clipboardData);
		event.preventDefault();
		clipboardData.clearData();
		setData("text/x-moz-url", url);
		setData("text/uri-list", url);
		setData("text/html", isImage ? `<img src="${escapedURL}" alt="${encodeChars(filename, /["&<>]/g)}">` : `<a href="${escapedURL}">${encodeChars(title, /[&<>]/g)}</a>`);
		setData("text/plain", isImage || title !== url ? (isImage ? "!" : "") + "[" + (isImage ? filename : title).replace(/[\\<>\[\]]/g,"\\$&") + "](" + escapedURL + ")" : escapedURL);
	}, {once: true});
	// TODO attach to doc a temp textarea as fallback if copy is not dispatched, and remove it after exec command
	// TODO see also navigator.clipboard API https://developer.mozilla.org/en-US/docs/Web/API/Clipboard/write
	doc.execCommand("copy");
}

//javascript:{let%20e=document,t=e.URL,a=[e.title].concat(Array.from(e.querySelectorAll("h1,h2"),e=>e.textContent.replace(/\s+/g,"%20")),t).reduce((e,t)=>e||t.trim(),""),n=(e,t,a="&%23x",n=";")=>e.replace(t,e=>a+e.charCodeAt(0).toString(16).padStart(2,"0")+n),l=n(t,/[()"]/g,"%25",""),r=e.contentType.startsWith("image/"),[,i="Untitled"]=/\/([^/.]+$|[^/]+(?=\.[^.]*$))/g.exec(new%20URL(t).pathname)||[];if(i+="."+e.contentType.split("/")[1].split("+")[0],["IFRAME","FRAME"].includes(e.activeElement.tagName)){let%20t=e.createElement("span");t.tabIndex=-1,t.setAttribute("aria-hidden","true"),t.style.position="fixed",e.documentElement.appendChild(t),t.focus(),t.remove()}e.addEventListener("copy",e=>{let%20c=e.clipboardData,o=c.setData.bind(c);e.preventDefault(),c.clearData(),o("text/x-moz-url",t),o("text/uri-list",t),o("text/html",r?`<img%20src="${l}"%20alt="${n(i,/["&<>]/g)}">`:`<a%20href="${l}">${n(a,/[&<>]/g)}</a>`),o("text/plain",r||a!==t?(r?"!":"")+"["+(r?i:a).replace(/[\\<>\[\]]/g,"\\$&")+"]("+l+")":l)},{once:!0}),e.execCommand("copy")}void(0)
```

Older version:

```
javascript:{let%20e=document,t=e.URL,a=[e.title].concat(Array.from(e.querySelectorAll("h1,h2")),t).reduce((e,t)=>e||t.textContent&&t.textContent.trim().replace(/\s+/g,"%20")||t.trim(),""),n=(e,t,a="&%23x",n=";")=>e.replace(t,e=>a+e.charCodeAt(0).toString(16).padStart(2,"0")+n),r=n(t,/[()"]/g,"%25",""),l=e.contentType.startsWith("image/"),[,i="Untitled"]=/\/([^/.]+$|[^/]+(?=\.[^.]*$))/g.exec(new%20URL(t).pathname)||[];i+="."+e.contentType.split("/")[1].split("+")[0];let%20c=o=>{let%20p=o.clipboardData,d=p.setData.bind(p);e.removeEventListener("copy",c),o.preventDefault(),p.clearData(),d("text/x-moz-url",t),d("text/uri-list",t),d("text/html",l?`<img%20src="${r}"%20alt="${n(i,/["&<>]/g)}">`:`<a%20href="${r}">${n(a,/[&<>]/g)}</a>`),d("text/plain",l||a!==t?(l?"!":"")+"["+(l?i:a).replace(/[\\<>\[\]]/g,"\\$&")+"]("+r+")":r)};if(["IFRAME","FRAME"].includes(e.activeElement.tagName)){let%20t=e.createElement("span");t.tabIndex=-1,t.setAttribute("aria-hidden","true"),t.style.position="fixed",e.documentElement.appendChild(t),t.focus(),t.remove()}e.addEventListener("copy",c),e.execCommand("copy")}void(0)
```

- [Bookmarkleter](http://chriszarate.github.io/bookmarkleter/) - Doesn't support ES6
- [Create Bookmarklets - The Right Way](https://code.tutsplus.com/tutorials/create-bookmarklets-the-right-way--net-18154)
- [javascript - How a bookmarklet can avoid the popup blocker - Stack Overflow](https://stackoverflow.com/questions/4609936/how-a-bookmarklet-can-avoid-the-popup-blocker)
- [Bookmarklet - Wikipedia](https://en.wikipedia.org/wiki/Bookmarklet#Concept)

## Timeout limit

- setTimeout functions are limited to INT32 (2147483647 milliseconds or roughly 24.8 days)

- https://github.com/dirkbonhomme/infinite-timeout

## Time precision

- [Metronomes in JavaScript – Monica Dinculescu](https://meowni.ca/posts/metronomes/)

## Popup

> browsers allow web pages to open popups in response to a particular set of events: for example, click, mouseup, submit.

Must be called in event listener only from user-initiated (at least click).

- [javascript - Avoid browser popup blockers - Stack Overflow](https://stackoverflow.com/questions/2587677/avoid-browser-popup-blockers/25050893#25050893)
- [Dom.popup allowed events - MozillaZine Knowledge Base](http://kb.mozillazine.org/Dom.popup_allowed_events)
- [trusted event](https://www.w3.org/TR/uievents/#trusted-events)

## Case

```js
const camelToSnakeCase = name => name.replace(/[a-z][A-Z]/g, match => match.charAt(0) + "_" + match.charAt(1).toLowerCase()).toLowerCase();

const snakeToCamelCase = name => name.replace(/_([a-z])/g, match => match.charAt(1).toUpperCase());
```

## Data URI function

```js
// can throw error because it contains invalid escaped sequences
/*
getDataURIJavaScript("data:application/javascript;charset=UTF-8,'%E2%9C%93%20%C3%A0%20la%20mode'")// > function(){'✓ à la mode'}
getDataURIJavaScript("data:application/javascript;charset=US-ASCII,'la%20mode'")// > function(){'la mode'}
getDataURIJavaScript("data:application/javascript;charset=UTF-8;base64,J+KckyDDoCBsYSBtb2RlJw==")// > function(){'✓ à la mode'}
getDataURIJavaScript("data:application/javascript;charset=US-ASCII;base64,J2xhIG1vZGUn")// > function(){'la mode'}
 */
function getDataURIJavaScript(uri){
  const parseResult = /^data:(?:application|text)\/javascript(?:\s*;\s*charset=(UTF-8|US-ASCII))?(?:\s*;\s*(base64)\s*)?,(.*)$/.exec(uri);
  if(!parseResult){
    throw new TypeError(`Invalid or unsupported JavaScript data URI "${uri}"`);
  }

  const [, charset, encoding, precentEncodedData] = parseResult;

  let code;
  if(encoding === "base64"){
    const precentDecodedData = unescape(precentEncodedData);
    // Handle UTF-8 decoding
    // https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/btoa#Unicode_strings
    switch(charset){
      case "UTF-8":
        code = decodeURIComponent(escape(atob(precentDecodedData)));
        break;
      case "US-ASCII":
      default:
        code = atob(precentDecodedData);
        break;
    }
  }else if(!encoding){
    switch(charset){
      case "UTF-8":
        code = decodeURIComponent(precentEncodedData);
        break;
      case "US-ASCII":
      default:
        code = unescape(precentEncodedData);
        break;
    }
  }else{
    throw new Error(`Unknown encoding "${encoding}"`);
  }

  return new Function(code);
}
```

## Keyboard

Arrow keys, WASD or ZQSD

- [Some subtleties of keyboard inputs in JS games - Maxime Euzière](https://xem.github.io/articles/jsgamesinputs.html)
- [Arrow keys - Wikipedia](https://en.wikipedia.org/wiki/Arrow_keys#WASD_keys)
