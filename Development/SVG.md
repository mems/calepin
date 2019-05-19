- [A Compendium of SVG Information | CSS-Tricks](https://css-tricks.com/mega-list-svg-information/)
- [SVG – Sara Soueidan – Freelance Front-end Web Developer](https://sarasoueidan.com/tags/svg/index.html)
- [Pocket Guide to Writing SVG](http://svgpocketguide.com/book/)
- [Styling And Animating SVGs With CSS – Smashing Magazine](https://www.smashingmagazine.com/2014/11/styling-and-animating-svgs-with-css/)
- [An SVG Primer for Today's Browsers](https://www.w3.org/Graphics/SVG/IG/resources/svgprimer.html)
- [A Practical Guide to SVGs on the web](https://svgontheweb.com/)
- [How Designers Should Think About SVG – Design + Sketch – Medium](https://medium.com/sketch-app-sources/how-designers-should-think-about-svg-b2b92efc4d77)
- [A simple pie chart in SVG](https://hackernoon.com/a-simple-pie-chart-in-svg-dbdd653b6936)
- [The SVG `path` Syntax: An Illustrated Guide | CSS-Tricks](https://css-tricks.com/svg-path-syntax-illustrated-guide/)
- [Tools to Visualize and Edit SVG Paths (Kinda!) | CSS-Tricks](https://css-tricks.com/tools-visualize-edit-svg-paths-kinda/)
- [Tips for Creating and Exporting Better SVGs for the Web](https://sarasoueidan.com/blog/svg-tips-for-designers/)

Tools:

- [SVG manipulate paths](https://codepen.io/netsi1964/pen/pJzWoz)
- [xvg](https://xvg.now.sh/) - Chrome extension. See [XVG - debug SVG paths in the browse](https://github.com/winkerVSbecks/xvg)
- [SVG Path Builder](https://codepen.io/anthonydugois/pen/mewdyZ)
- [cubic Bézier curve with SVG](http://codepen.io/thebabydino/pen/EKLNvZ)
- [Svgbob Editor - Convert your ascii diagram scribbles into happy little SVG](https://ivanceras.github.io/svgbob-editor/)

Good to know:

- Presentation attributes will overwrite inherited styles specified on a parent element
- Links inside an SVG embedded as an `<object>` will open inside the boundaries of that `<object>`
- Certain CSS characters like brackets will cause an XML error when used inside an SVG file

## Accessibility

Only `img`, `iframe` and `object` can provide alternative content. `img` only provide text alternative (via the `alt` attribute)

- [Making SVG accessible](http://ljwatson.github.io/decks/2017/lws/index.html)
- [demosthenes.info – Making SVG Accessible](http://demosthenes.info/blog/1026/Making-SVG-Accessible)
- http://www.paciellogroup.com/blog/2013/12/using-aria-enhance-svg-accessibility/
- http://www.sitepoint.com/tips-accessible-svg/
- https://github.com/SVG-access-W3CG
- [Making composed-tree.svg more accessible](http://svg-access-w3cg.github.io/use-case-examples/composed-tree-notes.html)
- [Accessible SVGs | CSS-Tricks](https://css-tricks.com/accessible-svgs/)
- [Managing focus in SVG - ally.js](https://allyjs.io/tutorials/focusing-in-svg.html)
- [Heating ice](http://svg-access-w3cg.github.io/use-case-examples/beaker.html) - See [SVG Heating ice - accessibility notes](http://svg-access-w3cg.github.io/use-case-examples/beaker-notes.html) and ['Chaals' Nevile sur Twitter : "Using SVG animation and aria-live to make an accessible interactive STEM demo: https://t.co/UxEaZE4lgQ with notes at https://t.co/pFi3XzRSiL"](https://mobile.twitter.com/chaals/status/838474855037067265)
- [highchart screenreaders chart - offline version](http://svg-access-w3cg.github.io/use-case-examples/hc-chart/notes.html)
- [7 solutions for creating more accessible SVGs » Simply Accessible](http://simplyaccessible.com/article/7-solutions-svgs/)

## Restrictions

| SVG Embed Technique											 | External resources (styles, images)		 | Scripts		 | Interactivity (links, etc.)		 | CSS Animations		 | [CSS Inheritance][css-inheritance]	 |
|----------------------------------------------------------------|-------------------------------------------|---------------|-----------------------------------|-----------------------|---------------------------------------|
| `<svg> … </svg>` (inlined)									 | Yes										 | Yes			 | Yes								 | Yes					 | Yes									 |
| `<svg><use xlink:href="image.svg"></svg>` [^1]				 | Yes										 | Yes			 | Yes								 | Yes					 | Yes									 |
| `<object type="image/svg+xml" data="image.svg"></object>`		 | Yes										 | Yes			 | Yes								 | Yes, only inlined	 | No									 |
| `<embed type="image/svg+xml" src="image.svg">`				 | Yes										 | Yes			 | Yes								 | Yes, only inlined	 | No									 |
| `<iframe src="image.svg"></iframe>`							 | Yes										 | Yes			 | Yes								 | Yes, only inlined	 | No									 |
| `<img src="img.svg" alt="">`									 | No [^2]									 | No			 | No								 | Yes, only inlined?	 | No									 |
| `element::before{content: url(img.svg);}`						 | No [^2]									 | No			 | No								 | Yes, only inlined?	 | No									 |
| `background-image: url(image.svg);`							 | No [^2]									 | No			 | No								 | Yes, only inlined?	 | No									 |

[css-inheritance]: https://developer.mozilla.org/en-US/docs/Web/CSS/inheritance

[^1]: "For security reasons, browsers could apply the [same-origin policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) on `use` elements and could refuse to load a cross-origin URL in the [`href`](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/href) attribute.". IE11 don't support load from external URI
[^2]: no other URI that data URI can be used inside image SVG (Blob works only with Firefox, not Chrome, not Safari)

**TODO test CSS Animations for "SVG as an Image" aka "SVG img src", SMIL animations (apprears to works at least with Safari)**

~~When used as an image: iframe doesn't work (no data URI, no srcdoc)~~ (don't know what I wanted to say there)

> Basically when using a foreign object tag [in fact elements inside SVG as an Image] all its content must be origin free

- [SVG as an Image - SVG | MDN](https://developer.mozilla.org/en-US/docs/Web/SVG/SVG_as_an_Image#Restrictions)
- [SVG `use` with External Reference, Take 2 | CSS-Tricks](https://css-tricks.com/svg-use-with-external-reference-take-2/)
- `LayoutTests/http/tests/security/svg-imge-with-url-data-image.html` and `LayoutTests/http/tests/security/resources/image-with-url-data-image.svg`
- [141261 – SVG animation is slow only when the SVG is the background of the \<body\>](https://bugs.webkit.org/show_bug.cgi?id=141261)

Related bugs:

- [100269 – SVG Images don't load referenced resources, including data URIs](https://bugs.webkit.org/show_bug.cgi?id=100269)
- [99677 – When using SVG as an image, we should load datauri images when these images are not in the image cache.](https://bugs.webkit.org/show_bug.cgi?id=99677)
- [170560 - \[SVG\] embeded images does not preloading (\<img\> tag) - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=170560)
- [552707 - Chrome fails to display createObjectURL encoded image pattern in a svg data uri - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=552707)
- [176591 - SVG inside of a Blob cannot access its own defs element. - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=176591)
- [Issues - chromium - An open-source project to help move the web forward. - Monorail](https://bugs.chromium.org/p/chromium/issues/list?q=component:Blink%3ESVG)

## Fragment identifier and SVG stack

	<img src="sprite.svg#instagram-icon" alt="Instagram icon">

	<svg>
		<view id="instagram-icon" viewBox="64 0 32 32" />
	</svg>

- [An Overview of SVG Sprite Creation Techniques ◆ 24 ways](https://24ways.org/2014/an-overview-of-svg-sprite-creation-techniques/)
- https://bugs.webkit.org/show_bug.cgi?id=91790
- https://code.google.com/p/chromium/issues/detail?id=128055
- [How to Use SVG Image Sprites](https://www.sitepoint.com/use-svg-image-sprites/)
- http://dev.w3.org/csswg/css-images/#image-notation
- http://caniuse.com/#feat=svg-fragment
- [How SVG Fragment Identifiers Work | CSS-Tricks](https://css-tricks.com/svg-fragment-identifiers-work/)

## SVG symbols

Aka icon

- The `viewBox` can be defined on the symbol, so you don't need to use it in the markup (easier and less error prone).
- `title` and `desc` tags can be added within the `<symbol>` and they kinda "come along for the ride" when the symbol gets used, making accessibility easier to do right.
- Symbols don't display as you define them, so no need for a `<defs>` block.
- This is probably what `<symbol>` was invented for anyway
 
	<svg xmlns="http://www.w3.org/2000/svg" style="display: none;">
	  <symbol id="symbol-1" viewBox="214.7 0 182.6 792">
	  	<title>symbol's-title</title> 
	    <desc>symbol's-desc</desc>
	    <!-- <path>s and whatever other shapes in here -->  
	  </symbol>
	  <symbol id="symbol-2" viewBox="0 26 100 48">
	  	<title>symbol's-title</title> 
	    <desc>symbol's-desc</desc>
	    <!-- <path>s and whatever other shapes in here -->  
	  </symbol>
	</svg>
	
	<svg class="icon">
	  <use xlink:href="#symbol-1" />
	</svg>

- [Comment travailler avec des icônes en SVG](https://la-cascade.io/comment-travailler-avec-des-icones-en-svg/)
- [SVG `symbol` a Good Choice for Icons | CSS-Tricks](https://css-tricks.com/svg-symbol-good-choice-icons/)

## SVG Path

- [SVG Path Strings - Road to Larissa](http://roadtolarissa.com/blog/2015/02/22/svg-path-strings/)
- [The SVG `path` Syntax: An Illustrated Guide | CSS-Tricks](https://css-tricks.com/svg-path-syntax-illustrated-guide/)

### Relative ↔︎ Absolute path

- [Utility: Convert SVG path to all-relative or all-absolute commands | Lea Verou](http://lea.verou.me/2019/05/utility-convert-svg-path-to-all-relative-or-all-absolute-commands/)
- https://stackoverflow.com/questions/14179333/convert-svg-path-to-relative-commands/14179367#14179367
- https://stackoverflow.com/questions/9677885/convert-svg-path-to-absolute-commands/9677915#9677915
- https://github.com/DmitryBaranovskiy/raphael/blob/bef7f6b0e259030138193d42f2c74b754c292f3e/dev/raphael.core.js#L1646

### SVG Path Data API

`SVGPathSeg`, `getPathData()` and `setPathData()`

- [jarek-foksa/path-data-polyfill.js: Polyfill for SVG 2 getPathData() and setPathData() methods.](https://github.com/jarek-foksa/path-data-polyfill.js)
- [progers/pathseg: SVGPathSeg polyfill](https://github.com/progers/pathseg/)

### Primitives to path

See `MorphSVGPlugin.convertToPath` (require to be Club GreenSock membership)

Polyline to path: `<polygon points="x1,y1 x2,y2 x3,y3"/>` as `<path d="Mx1,y1 x2,y2 x3,y3Z"/>`

	<!--
	http://codepen.io/niorad/pen/xmfza
	Convert SVG-Shapes into paths so they can be animated. 
	The script converts all non-path-elements to paths so the stroke-dashoffset-trick works.
	Note: this doesn't implement all syntaxes allowed by SVG specs
	-->
	
	<script>
		//inspired by http://product.voxmedia.com/post/68085482982/polygon-feature-design-svg-animations-for-fun-and
		
		//If you want to add SVG to the DOM, jQuery won't do
		//http://www.benknowscode.com/2012/09/using-svg-elements-with-jquery_6812.html
		
		function SVG(tag) {
		    return document.createElementNS('http://www.w3.org/2000/svg', tag);
		}
		
		function replaceRectsWithPaths(parentElement) {
		    var rects = $(parentElement).find('rect');
			
		    $.each(rects, function() {
		        var rectX = $(this).attr('x');
		        var rectY = $(this).attr('y');
				
		        var rectX2 = parseFloat(rectX) + parseFloat($(this).attr('width'));
		        var rectY2 = parseFloat(rectY) + parseFloat($(this).attr('height'));
				
		        var convertedPath = 'M' + rectX + ',' + rectY + ' ' + rectX2 + ',' + rectY + ' ' + rectX2 + ',' + rectY2 + ' ' + rectX + ',' + rectY2 + ' ' + rectX + ',' + rectY;
				
		        $(SVG('path'))
		        .attr('d', convertedPath)
		        .attr('fill', $(this).attr('fill'))
		        .attr('stroke', $(this).attr('stroke'))
		        .attr('stroke-width', $(this).attr('stroke-width'))
		        .insertAfter(this);
		    });
			
		    $(rects).remove();
		}
		
		function replaceLinesWithPaths(parentElement) {
		    var lines = $(parentElement).find('line');
			
		    $.each(lines, function() {
		        var lineX1 = $(this).attr('x1');
		        var lineY1 = $(this).attr('y1');
				
		        var lineX2 = $(this).attr('x2');
		        var lineY2 = $(this).attr('y2');
				
		        var convertedPath = 'M' + lineX1 + ',' + lineY1 + ' ' + lineX2 + ',' + lineY2;
				
		        $(SVG('path'))
		        .attr('d', convertedPath)
		        .attr('fill', $(this).attr('fill'))
		        .attr('stroke', $(this).attr('stroke'))
		        .attr('stroke-width', $(this).attr('stroke-width'))
		        .insertAfter(this);
		    });
			
		    $(lines).remove();
		}
		
		function replaceCirclesWithPaths(parentElement) {
		    var circles = $(parentElement).find('circle');
			
		    $.each(circles, function() {
		        var cX = $(this).attr('cx');
		        var cY = $(this).attr('cy');
		        var r = $(this).attr('r');
		        var r2 = parseFloat(r * 2);
				
		        var convertedPath = 'M' + cX + ', ' + cY + ' m' + (-r) + ', 0 ' + 'a ' + r + ', ' + r + ' 0 1,0 ' + r2 + ',0 ' + 'a ' + r + ', ' + r + ' 0 1,0 ' + (-r2) + ',0 ';
				
		        $(SVG('path'))
		        .attr('d', convertedPath)
		        .attr('fill', $(this).attr('fill'))
		        .attr('stroke', $(this).attr('stroke'))
		        .attr('stroke-width', $(this).attr('stroke-width'))
		        .insertAfter(this);
		    });
			
		    $(circles).remove();
		}
		
		function replaceEllipsesWithPaths(parentElement) {
		    var ellipses = $(parentElement).find('ellipse');
			
		    $.each(ellipses, function() {
		        var cX = $(this).attr('cx');
		        var cY = $(this).attr('cy');
		        var rX = $(this).attr('rx');
		        var rY = $(this).attr('ry');
				
		        var convertedPath = 'M' + cX + ', ' + cY + ' m' + (-rX) + ', 0 ' + 'a ' + rX + ', ' + rY + ' 0 1,0 ' + rX*2 + ',0 ' + 'a ' + rX + ', ' + rY + ' 0 1,0 ' + (-rX*2) + ',0 ';
				
		        $(SVG('path'))
		        .attr('d', convertedPath)
		        .attr('fill', $(this).attr('fill'))
		        .attr('stroke', $(this).attr('stroke'))
		        .attr('stroke-width', $(this).attr('stroke-width'))
		        .insertAfter(this);
		    });
			
		    $(ellipses).remove();
		}
		
		function replacePolygonsWithPaths(parentElement) {
		    var polygons = $(parentElement).find('polygon');
			
			// https://www.w3.org/TR/SVG/shapes.html#PointsBNF
		    $.each(polygons, function() {
		        var points = $(this).attr('points');
		        var polyPoints = points.split(/[ ,]+/);
		        var endPoint = polyPoints[0] + ', ' + polyPoints[1];
				
		        $(SVG('path'))
		        .attr('d', 'M' + points + ' ' + endPoint)
		        .attr('fill', $(this).attr('fill'))
		        .attr('stroke', $(this).attr('stroke'))
		        .attr('stroke-width', $(this).attr('stroke-width'))
		        .insertAfter(this);
		    });
			
		    $(polygons).remove();
		}
		
		function replacePolylinesWithPaths(parentElement) {
		    var polylines = $(parentElement).find('polyline');
			
		    $.each(polylines, function() {
		        var points = $(this).attr('points');
				
		        $(SVG('path'))
		        .attr('d', 'M' + points)
		        .attr('fill', $(this).attr('fill'))
		        .attr('stroke', $(this).attr('stroke'))
		        .attr('stroke-width', $(this).attr('stroke-width'))
		        .insertAfter(this);
		    });
			
		    $(polylines).remove();
		}
		
		function hideSVGPaths(parentElement) {
		    var paths = $(parentElement).find('path');
			
		    //for each PATH..
		    $.each( paths, function() {
		        //get the total length
		        var totalLength = this.getTotalLength();
				
		        //set PATHs to invisible
		        $(this).css({
		            'stroke-dashoffset': totalLength,
		            'stroke-dasharray': totalLength + ' ' + totalLength
		        });
		    });
		}
		
		function drawSVGPaths(_parentElement, _timeMin, _timeMax, _timeDelay) {
		    var paths = $(_parentElement).find('path');
			
		    //for each PATH..
		    $.each( paths, function(i) {
		        //get the total length
		        var totalLength = this.getTotalLength();
				
		        //set PATHs to invisible
		        $(this).css({
		            'stroke-dashoffset': totalLength,
		            'stroke-dasharray': totalLength + ' ' + totalLength
		        });
				
		        //animate
		        $(this).delay(_timeDelay*i).animate({
		            'stroke-dashoffset': 0
		        }, {
		            duration: Math.floor(Math.random() * _timeMax) + _timeMin
		            ,easing: 'easeInOutQuad'
		        });
		    });
		}
		
		function replaceWithPaths(parentElement) {
		    replaceRectsWithPaths(parentElement);
		    replaceLinesWithPaths(parentElement);
		    replaceEllipsesWithPaths(parentElement);
		    replaceCirclesWithPaths(parentElement);
		    replacePolygonsWithPaths(parentElement);
		    replacePolylinesWithPaths(parentElement);    
		}
		
		function startSVGAnimation(parentElement) {
		    drawSVGPaths(parentElement, 1000, 2000, 50);
		}
		
		replaceWithPaths($('svg'));
		startSVGAnimation($('svg'));
	</script>
	
	<svg version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
	     width="800px" height="800px" viewBox="0 0 800 800" enable-background="new 0 0 800 800" xml:space="preserve">
	<circle fill="#FFFFFF" stroke="#000000" stroke-width="4" stroke-miterlimit="10" cx="115.5" cy="119.5" r="55.5"/>
	<ellipse fill="#FFFFFF" stroke="#000000" stroke-width="2" stroke-miterlimit="10" cx="284" cy="123" rx="69" ry="23"/>
	<rect x="403" y="71" fill="#FFFFFF" stroke="#000000" stroke-width="2" stroke-miterlimit="10" width="98" height="97"/>
	<path fill="#FFFFFF" stroke="#000000" stroke-width="2" stroke-miterlimit="10" d="M672,158c0,5.523-4.477,10-10,10h-82
	    c-5.523,0-10-4.477-10-10V81c0-5.523,4.477-10,10-10h82c5.523,0,10,4.477,10,10V158z"/>
	<polyline fill="#FFFFFF" stroke="#000000" stroke-width="2" stroke-miterlimit="10" points="66,292 115.5,239 171,321 194,251 
	    236,280 268,251 318,291 343,239 368,275 "/>
	<path fill="#FFFFFF" stroke="#000000" stroke-width="2" stroke-miterlimit="10" d="M452,293c0,0,0-61,72-44c0,0-47,117,81,57
	    s5-110,10-67s-51,77.979-50,33.989"/>
	</svg>

## Transform

- [Transforms on SVG Elements | CSS-Tricks](https://css-tricks.com/transforms-on-svg-elements/)

### `transform-origin` in SVG not the same as HTML

Default values:

- HTML: `center, center`
- SVG: `0, 0`

### Transform on Firefox

`transform-origin: 50% 50%` is not supported in Firefox. Use `translate(-halfWpx -halfHpx) ... translate(halfWpx halfHpx)` or `transform-origin: 200px 200px` instead

## Animation

SMIL animation in SVG are powerfull, but hard to control. Prefer use CSS animation/transition but it is not supported in IE -11+. A pure JS fallback is the solution.

- http://jakearchibald.com/2013/animated-line-drawing-svg/

Animation as a huge impact on performance, especially on mobile. Rasterization is the problem. May be use canvas instead.

> [SVG is] perfect for mobile… as long as it doesn’t move. There is no way to animate it smoothly on Android - rasterization won’t give you a chance.

- https://github.com/kdzwinel/progress-bar-animation
- https://github.com/kdzwinel/progress-bar-animation/issues/1

### SMIL

Can't make multiple transform in the same time. Don't have an equivalent of `transform-orign` (it's the fault of SVG transform)

	<!-- Animate element's translate -->
	<animateTransform attributeName="transform" attributeType="XML" type="translate" from="589 122" to="580 -57" dur="250ms" fill="freeze" calcMode="spline" keySplines="0.43 0 0 1"/>
	<!-- Animate opacity -->
	<animate class="target" attributeName="opacity" attributeType="XML" from="1" to="0" dur="250ms" fill="freeze" calcMode="spline" keySplines="0.43 0 0 1"/>

Control it with JS: Add `begin="indefinite"` to `animate*` element, and `element.beginElement()` or `element.endElement()` (and few others methods) to control it.

- http://leunen.me/fakesmile/index.html
- http://css-tricks.com/guide-svg-animations-smil/
- http://tutorials.jenkov.com/svg/svg-animation.html
- http://oak.is/thinking/animated-svgs
- http://apike.ca/prog_svg_smil.html
- https://developer.mozilla.org/en-US/docs/Web/SVG/SVG_animation_with_SMIL

### CSS

- https://stackoverflow.com/questions/24302615/css3-animation-is-not-working

### JS

- [TweenMax](https://github.com/greensock/GreenSock-JS)
- http://codepen.io/GreenSock/full/gpDrC/
- http://www.w3.org/TR/SVG/animate.html#DOMAnimationExample

Now (05/11/2014) there no lib that can animate SVG transform attribute.

Interpolation:

- http://www.w3.org/TR/css3-transforms/#interpolation-of-transform-functions
- http://www.w3.org/TR/css3-transforms/#transform-function-lists
- https://wiki.csswg.org/topics/transform-interpolation
- `transform-origin: 200px 300px; transform: rotate(45deg);` is equivalent to: `transform: translate(200px 300px) rotate(45deg) translate(-200px -300px)`. Apply it to `scale`, `rotate`, ``
	(exist in SVG only for rotate: `transform="rotate(45 200 300)"` ). http://www.w3.org/TR/css3-transforms/#transformation-matrix-computation
- https://stackoverflow.com/questions/19154631/how-to-get-coordinates-of-an-svg-element https://github.com/mbostock/d3/blob/48ad44fdeef32b518c6271bb99a9aed376c1a1d6/src/math/transform.js

- http://greensock.com/forums/tags/forums/svg/
- http://greensock.com/forums/topic/10666-svg-animations-in-ie/
- http://greensock.com/forums/topic/10684-apply-transforms-with-transform-attr-instead-of-inline-style-on-svg/
- http://greensock.com/forums/topic/10725-animating-svgs-fill-opacity/
- http://greensock.com/forums/topic/7376-general-purpose-svg-plug-in/
- https://github.com/akbr/GSAPSvgPlugin/blob/master/SvgPlugin.js
- https://gist.github.com/raldred/7769278
- http://www.benknowscode.com/2012/09/diving-into-matrices-with-css3_4970.html
- http://www.w3.org/TR/SVG/coords.html#TransformMatrixDefined
- https://github.com/jcoglan/sylvester

### Stroke animation

Works only on path elements. See code below to do that.

- `stroke-dashoffset`
- can be used for pie chart (camembert) animation. Use large `stroke-width` of a `<circle>`. On IE use a value minus <1px (50px → 49.9px)
- [SVG-Stroke Animation](http://codepen.io/niorad/pen/xmfza)
- [Animated line drawing in SVG - JakeArchibald.com](https://jakearchibald.com/2013/animated-line-drawing-svg/)
- [css - Animate Path in Internet Explorer - Stack Overflow](https://stackoverflow.com/questions/24918529/animate-path-in-internet-explorer)
- [Three Illustrator tricks for better SVG stroke animations | Val Head - Web & UI animation expert](http://valhead.com/2017/03/03/three-illustrator-tricks-for-better-svg-stroke-animations/)

## Stroke

- [Paths: Stroking and Offsetting | Tavmjong Bah's Blog](http://tavmjong.free.fr/blog/?p=1257)

## Pattern

- [An Overview of SVG Patterns : Adobe Dreamweaver Team Blog](http://blogs.adobe.com/dreamweaver/2015/09/svg-patterns.html)

## Unit

- stroke-width
- stroke-dasharray
- ...

unit less (5) = viewBox
percentage (5%) = viewport

## DOM

Don't forget the SVG namespace:

	var image = document.createElementNS("http://www.w3.org/2000/svg", "image");
	image.setAttributeNS("http://www.w3.org/2000/svg", "style", "opacity: 0.5");
	// Use the default NS
	image.setAttributeNS(null, "style", "opacity: 0.5");
	image.setAttribute("style", "opacity: 0.5");
	image.setAttributeNS('http://www.w3.org/1999/xlink', "href", "");

## Filter

- [My Article on SVG Filters at Smashingmag | eleqtriq](http://w3.eleqtriq.com/2015/05/the-svg-filter-and-why-its-awesome/)
- [SVG Filter Effects—3 Simple Filter Primitives - Vanseo Design](http://vanseodesign.com/web-design/simple-filter-primitives/)
- [SVG Filters](https://yoksel.github.io/svg-filters/#/)
- [SVG Filters 101 | Codrops](https://tympanus.net/codrops/2019/01/15/svg-filters-101/)

- [SVG Gradient Map Filter](https://yoksel.github.io/svg-gradient-map/#/)

### Filter cropped, filter size

By default filter are `<filter x="-10%" y="-10%" width="120%" height="120%">`. If you want a bigger drop shadow, blur, etc. use `<filter x="-30%" y="-30%" width="160%" height="160%">`.

- [SVG Filters | tutorials.jenkov.com](http://tutorials.jenkov.com/svg/filters.html)
- [SVG Basics Tutorials - feOffset Filter Effect](http://www.svgbasics.com/filters3.html)

## Filter

- [Clipping in CSS and SVG — The clip-path Property and \<clipPath\> Element](https://www.sarasoueidan.com/blog/css-svg-clipping/)

## Use clip-path over alpha channel filter as mask

...when it's possible for better performances

## Mask

Mask SVG qui disparaissent quand certain elements en contiennent ne sont plus affiché (`visibility: hidden;`, `display: none;`, removed)

## `<use>` with external source

Not work properly on IE9-11+?

- [Ajaxing for your SVG Sprite | CSS-Tricks](http://css-tricks.com/ajaxing-svg-sprite/)
- [SVG `use` with External Source | CSS-Tricks](http://css-tricks.com/svg-use-external-source/)

## Optimizations

Don't remove `xmlns="http://www.w3.org/2000/svg"` if you not inline the SVG document in an HTML document.

- element used once (`<use xlink:href="#ID" />`), replace replace it directly
- remove useless `id="ID"` attribute (if not reference by `xlink:ref="#ID"`, `clip-path="url(#ID)"`, etc.)
- same attributes (like `fill`, `stroke`, `stroke-***`, `style`, etc.) create a `<g></g>` wrapper with this attributes (will inherit attributes)
- remove useless namespace (like: `xmlns:xlink`) if not used
- remove whitespaces before and after value of `d=""`, `points=""`
- change color like #FFFFFF to it's named equivalent black...
- simplify transform matrix `matrix(1 0 0 1 $e $f)` to `translate($e $f)`, `translate(...) rotate(...) scale(...)...` to `matrix(...)`
- remove subtle transforms ex: `matrix(1 0 0 1 -1.220703e-04 -6.103516e-05)`
- remove on root `<svg></svg>` attributes like `id`, `x`, `y`, `width`, `height`, `enabled-background`, `xml:space`...
- precompress (gzip) and use appropriate headers http://kaioa.com/node/45

- `<?xml version="1.0"?>` can be omitted
- `xmlns:xlink="http://www.w3.org/1999/xlink"` can be removed if not used
- `version="1.1"` on `svg` node can be omitted
- `<linearGradient>` inside `<defs>` not necessary
- `width` and `height` when `viewBox` is defined on `svg` node are not required
- `stop-opacity` on `stop` nodes are optional
- `stop-color="#ffffff"` and `stop-opacity="0"` can be merged to `stop-color="rgba(255,255,255,0)"`
- attribute quotes could be simple ones: `attribute='value'` instead of `attribute="value"`
- Remove all uncessary whites spaces like new lines, tabs

Some tools already exist:

- https://github.com/svg/svgo
- https://code.google.com/p/svgmin/
- https://petercollingridge.appspot.com/svg-editor

- http://creativedroplets.com/export-svg-for-the-web-with-illustrator-cc/
- [Common Pitfalls when Serving SVGs and How to Solve Them - José M. Pérez](https://jmperezperez.com/spotify-svg/)
- [Optimising SVGs for Web Use — Part 1 – Larsenwork – Medium](https://medium.com/larsenwork-andreas-larsen/optimising-svgs-for-web-use-part-1-67e8f2d4035)
- [Optimising SVGs for Web Use — Part 2 – Larsenwork – Medium](https://medium.com/larsenwork-andreas-larsen/optimising-svgs-for-web-use-part-2-6711cc15df46)
- [Optimising SVGs for Web Use — Part 2½ – Larsenwork – Medium](https://medium.com/larsenwork-andreas-larsen/optimising-svgs-for-web-use-part-2-1-598815d74f9c)

## Performances

Use HTML+CSS hardware acceleration (split SVG and wrap in HTML elements differents parts), Canvas (2D or WebGL) or just an still image (PNG) instead of SVG:

- [Goodbye, Layout Invalidation: Animating SVGs with CSS Transforms | Charlie Marsh](http://www.crmarsh.com/svg-performance/)
- [Maker here. I meant it as a way of saying good-bye to SVG as for the past years ... | Hacker News](https://news.ycombinator.com/item?id=12434230)
- [Performance of canvas versus SVG | Boris Smus](http://smus.com/canvas-vs-svg-performance/)
- Some well compressed PNG are smaller than the SVG version (often small icons) and the rendering time is the best by far
- [High Performance SVGs | CSS-Tricks](https://css-tricks.com/high-performance-svgs/)
- [shape-rendering - SVG | MDN](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/shape-rendering)

Inlined or as separate document vs CSS background image (data URI or separate document) impact rendering time and memory usage:

- [Bug 108999 – SVG background-image memory usage is absurd](https://bugs.webkit.org/show_bug.cgi?id=108999)
- [196524 - an svg background image eats up browser memory - chromium - Monorail](https://code.google.com/p/chromium/issues/detail?id=196524)
- [Bug 106159 – Remove the bitmap SVG image cache](https://bugs.webkit.org/show_bug.cgi?id=106159)
- [Case Study: Tricky SVG Background Images | Targetprocess - Visual management software](https://www.targetprocess.com/blog/2013/03/case-study-tricky-svg-background-images/)
- [Parashuram's blog: Icons - Font, Inline SVG or Background SVGs ?](http://blog.nparashuram.com/2015/05/icons-font-inline-svg-or-background-svgs.html), https://docs.google.com/spreadsheets/d/1j8YnjlnBR1rFxZ89JYwrNRV2cXVaoCm-9BexErRj2Hs/edit#gid=1538311979 and https://github.com/web-perf/svg-perf-test

### CSS animations applied on definition elements

CSS animations applied on elements used by `use` can be realy bad and not recommended.

## Case sensitivity

Since SVG is XML, node's name are case sensitive. Be carefull when create element in XML stream or via DOM (`createElement()`).
 
- http://ejohn.org/blog/nodename-case-sensitivity/

## Gradient

https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Gradients

> Linear gradients can be defined as horizontal, vertical or angular gradients:
> - Horizontal gradients are created when y1 and y2 are equal and x1 and x2 differ
> - Vertical gradients are created when x1 and x2 are equal and y1 and y2 differ
> - Angular gradients are created when x1 and x2 differ and y1 and y2 differ

	<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 1 1' preserveAspectRatio='none'>
		<linearGradient id='g' x1='0%' y1='0%' x2='100%' y2='0%'>
			<stop offset='0%' stop-color='rgba(255,255,255,0.5)'/>
			<stop offset='100%' stop-color='rgba(255,255,255,0.8)'/>
		</linearGradient>
		<rect fill='url(#g)' width='100' height='100'/>
	</svg>

- [How To Apply SVG Linear Gradients To A Fill Or Stroke - Vanseo Design](http://vanseodesign.com/web-design/svg-linear-gradients/)

### Gardient — Left to right

	<linearGradient id="g">

### Gardient — Top to bottom

	<linearGradient id="g" x1="0%" y1="0%" x2="100%" y2="0%">

## Coordinates, position and viewport

If `viewBox` is not defined nor `width` and `height`, SVG dimentions will not scale
Use `viewBox` instead of `width`, `height`, `x` and `y`.

Responsive

- [How to Scale SVG | CSS-Tricks](https://css-tricks.com/scale-svg/)
- [Mimic Relative Positioning Inside an SVG with Nested SVGs](https://sarasoueidan.com/blog/mimic-relative-positioning-in-svg/)
- [How to Translate from DOM to SVG Coordinates and Back Again](https://www.sitepoint.com/how-to-translate-from-dom-to-svg-coordinates-and-back-again/)
- [Understanding SVG Coordinate Systems and Transformations (Part 1) — The viewport, \<code\>viewBox</code>, and <code>preserveAspectRatio</code>](https://sarasoueidan.com/blog/svg-coordinate-systems/)
- [Interactive Data Visualization: Animating the viewBox | CSS-Tricks](https://css-tricks.com/interactive-data-visualization-animating-viewbox/)
- [SVG & media queries - JakeArchibald.com](https://jakearchibald.com/2016/svg-media-queries/)
- [CSSconf EU 2014 | Sara Soueidan: Styling and Animating Scalable Vector Graphics with CSS - YouTube](https://www.youtube.com/watch?v=lf7L8X6ZBu8#t=1083)

### Adaptive image

- http://w3.eleqtriq.com/2014/02/everything-is-relative-the-art-of-the-adaptive-image/
- [Four sliced scaling for SVG | eleqtriq](http://w3.eleqtriq.com/2014/02/the-4-slice-scaling-technique-for-svg/)
- 9 slice in SVG: [The Holy Grail of Image Scaling | eleqtriq](http://w3.eleqtriq.com/2014/03/the-holy-grail-of-image-scaling/)
- http://css-tricks.com/scale-svg/

### Scale bug on IE

- http://www.seowarp.com/blog/2011/06/svg-scaling-problems-in-ie9-and-other-browsers/
- http://benfrain.com/svg-backgrounds-dont-zoom-correctly-in-internet-explorer-10/

### `preserveAspectRatio`

`preserveAspectRatio="xMidYMid meet"` (default, CSS equivalent `background: center / contain`) has no effect if `viewBox` is not set

Scaling:

keyword	| CSS equivalent
`meet`	| `background-size: contain`
`slice`	| `background-size: cover`
`none`	| `background-size: 100% 100%` (stretching or squishing to fit the height and width)

For alignment (in conjuction with `meet` or `slice`), use 2 keywords concatenated (like `xMinYMin`):

keyword	| CSS equivalent
`xMin`	| `background-position-x: left`
`xMid`	| `background-position-x: center`
`xMax`	| `background-position-x: right`
`YMin`	| `background-position-y: top`
`YMid`	| `background-position-y: center`
`YMax`	| `background-position-y: bottom`

- [Why and how `preserveAspectRatio`? by Taylor Hunt on CodePen](http://codepen.io/tigt/post/why-and-how-preserveaspectratio) - equivalent to `background-position` and `background-size`

## Align text

	<text text-anchor="middle" dy=".3em">Center aligned text</text>

- [Easily center text vertically, with SVG! | Lea Verou](http://lea.verou.me/2013/03/easily-center-text-vertically-with-svg/)

## Fallback

```svg
<svg>
	<switch>
		<use xlink:href="#icon-twitter"></use>
		<foreignObject>
			<div class="fallback icon-twitter-fallback"></div>
		</foreignObject>
	</switch>
</svg>
<style>
	.icon-twitter-fallback{
		background-image: url("icon-twitter.png");
	}
</style>
```

> the logic is embedded inside the `<svg>` and use the `<foreignObject>` element to insert the non-SVG fallback. Using `<switch>`, SVG-capable browsers will render the first markup they understand (the SVG) and ignore the rest (the contents of the `<foreignObject>`). IE will do the opposite: it ignore the SVG it does not understand and renders the contents of the `<foreignObject>` because it is plain HTML.

- [SVG Fallbacks | CSS-Tricks](https://css-tricks.com/svg-fallbacks/)
- [A Complete Guide to SVG Fallbacks | CSS-Tricks](https://css-tricks.com/a-complete-guide-to-svg-fallbacks/)
- Chapter 28: Using SVGs As An Icon Font Replacement (Or, How To Create SVG Sprites And Use Them As An Icon System) (page 335) - Mastering SVG For Responsive Web Design by Sara Soueidan
- [Smashing Book 5 Real-Life Responsive Web Design - Part 1 - Smashing Magazine | Typography | Web Page](https://fr.scribd.com/document/279207475/Smashing-Book-5-Real-Life-Responsive-Web-Design-Part-1-Smashing-Magazine)
- [Inline SVG Fallback](http://www.kaizou.org/2009/03/inline-svg-fallback/)


## HTML Entities

```js
// create a doctype that includes definitions for all HTML entities - http://en.wikipedia.org/wiki/List_of_XML_and_HTML_character_entity_references
const HTML_ENTITIES = {
	"quot": 34,
	"amp": 38,
	"apos": 39,
	"lt": 60,
	"gt": 62,
	"nbsp": 160,
	"iexcl": 161,
	"cent": 162,
	"pound": 163,
	"curren": 164,
	"yen": 165,
	"brvbar": 166,
	"sect": 167,
	"uml": 168,
	"copy": 169,
	"ordf": 170,
	"laquo": 171,
	"not": 172,
	"shy": 173,
	"reg": 174,
	"macr": 175,
	"deg": 176,
	"plusmn": 177,
	"sup2": 178,
	"sup3": 179,
	"acute": 180,
	"micro": 181,
	"para": 182,
	"middot": 183,
	"cedil": 184,
	"sup1": 185,
	"ordm": 186,
	"raquo": 187,
	"frac14": 188,
	"frac12": 189,
	"frac34": 190,
	"iquest": 191,
	"Agrave": 192,
	"Aacute": 193,
	"Acirc": 194,
	"Atilde": 195,
	"Auml": 196,
	"Aring": 197,
	"AElig": 198,
	"Ccedil": 199,
	"Egrave": 200,
	"Eacute": 201,
	"Ecirc": 202,
	"Euml": 203,
	"Igrave": 204,
	"Iacute": 205,
	"Icirc": 206,
	"Iuml": 207,
	"ETH": 208,
	"Ntilde": 209,
	"Ograve": 210,
	"Oacute": 211,
	"Ocirc": 212,
	"Otilde": 213,
	"Ouml": 214,
	"times": 215,
	"Oslash": 216,
	"Ugrave": 217,
	"Uacute": 218,
	"Ucirc": 219,
	"Uuml": 220,
	"Yacute": 221,
	"THORN": 222,
	"szlig": 223,
	"agrave": 224,
	"aacute": 225,
	"acirc": 226,
	"atilde": 227,
	"auml": 228,
	"aring": 229,
	"aelig": 230,
	"ccedil": 231,
	"egrave": 232,
	"eacute": 233,
	"ecirc": 234,
	"euml": 235,
	"igrave": 236,
	"iacute": 237,
	"icirc": 238,
	"iuml": 239,
	"eth": 240,
	"ntilde": 241,
	"ograve": 242,
	"oacute": 243,
	"ocirc": 244,
	"otilde": 245,
	"ouml": 246,
	"divide": 247,
	"oslash": 248,
	"ugrave": 249,
	"uacute": 250,
	"ucirc": 251,
	"uuml": 252,
	"yacute": 253,
	"thorn": 254,
	"yuml": 255,
	"OElig": 338,
	"oelig": 339,
	"Scaron": 352,
	"scaron": 353,
	"Yuml": 376,
	"fnof": 402,
	"circ": 710,
	"tilde": 732,
	"Alpha": 913,
	"Beta": 914,
	"Gamma": 915,
	"Delta": 916,
	"Epsilon": 917,
	"Zeta": 918,
	"Eta": 919,
	"Theta": 920,
	"Iota": 921,
	"Kappa": 922,
	"Lambda": 923,
	"Mu": 924,
	"Nu": 925,
	"Xi": 926,
	"Omicron": 927,
	"Pi": 928,
	"Rho": 929,
	"Sigma": 931,
	"Tau": 932,
	"Upsilon": 933,
	"Phi": 934,
	"Chi": 935,
	"Psi": 936,
	"Omega": 937,
	"alpha": 945,
	"beta": 946,
	"gamma": 947,
	"delta": 948,
	"epsilon": 949,
	"zeta": 950,
	"eta": 951,
	"theta": 952,
	"iota": 953,
	"kappa": 954,
	"lambda": 955,
	"mu": 956,
	"nu": 957,
	"xi": 958,
	"omicron": 959,
	"pi": 960,
	"rho": 961,
	"sigmaf": 962,
	"sigma": 963,
	"tau": 964,
	"upsilon": 965,
	"phi": 966,
	"chi": 967,
	"psi": 968,
	"omega": 969,
	"thetasym": 977,
	"upsih": 978,
	"piv": 982,
	"ensp": 8194,
	"emsp": 8195,
	"thinsp": 8201,
	"zwnj": 8204,
	"zwj": 8205,
	"lrm": 8206,
	"rlm": 8207,
	"ndash": 8211,
	"mdash": 8212,
	"lsquo": 8216,
	"rsquo": 8217,
	"sbquo": 8218,
	"ldquo": 8220,
	"rdquo": 8221,
	"bdquo": 8222,
	"dagger": 8224,
	"Dagger": 8225,
	"bull": 8226,
	"hellip": 8230,
	"permil": 8240,
	"prime": 8242,
	"Prime": 8243,
	"lsaquo": 8249,
	"rsaquo": 8250,
	"oline": 8254,
	"frasl": 8260,
	"euro": 8364,
	"image": 8465,
	"weierp": 8472,
	"real": 8476,
	"trade": 8482,
	"alefsym": 8501,
	"larr": 8592,
	"uarr": 8593,
	"rarr": 8594,
	"darr": 8595,
	"harr": 8596,
	"crarr": 8629,
	"lArr": 8656,
	"uArr": 8657,
	"rArr": 8658,
	"dArr": 8659,
	"hArr": 8660,
	"forall": 8704,
	"part": 8706,
	"exist": 8707,
	"empty": 8709,
	"nabla": 8711,
	"isin": 8712,
	"notin": 8713,
	"ni": 8715,
	"prod": 8719,
	"sum": 8721,
	"minus": 8722,
	"lowast": 8727,
	"radic": 8730,
	"prop": 8733,
	"infin": 8734,
	"ang": 8736,
	"and": 8743,
	"or": 8744,
	"cap": 8745,
	"cup": 8746,
	"int": 8747,
	"there4": 8756,
	"sim": 8764,
	"cong": 8773,
	"asymp": 8776,
	"ne": 8800,
	"equiv": 8801,
	"le": 8804,
	"ge": 8805,
	"sub": 8834,
	"sup": 8835,
	"nsub": 8836,
	"sube": 8838,
	"supe": 8839,
	"oplus": 8853,
	"otimes": 8855,
	"perp": 8869,
	"sdot": 8901,
	"lceil": 8968,
	"rceil": 8969,
	"lfloor": 8970,
	"rfloor": 8971,
	"lang": 9001,
	"rang": 9002,
	"loz": 9674,
	"spades": 9824,
	"clubs": 9827,
	"hearts": 9829,
	"diams": 9830,
};

const SVG_DOCTYPE = `<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd" [ 
	${Object.entries(HTML_ENTITIES).map(([name, value]) => `<!ENTITY ${name} "&#${value};">`).join("\n\t")}
]>`;
```

- [Character entity references in HTML 4](https://www.w3.org/TR/html4/sgml/entities.html)
