See also [CSS](Formats, encoding and protocols/CSS/CSS)

- Old CSS techniques [CSS Discuss](http://css-discuss.incutio.com/wiki/Main_Page)
- [Improving CSS quality at Facebook and beyond | Engineering Blog | Facebook Code](https://code.facebook.com/posts/879890885467584)
- [Incomplete List of Mistakes in the Design of CSS \[CSS Working Group Wiki\]](https://wiki.csswg.org/ideas/mistakes)
- [CSS | CSS-Tricks](https://css-tricks.com/snippets/css/)
- [A collection of tips to help take your CSS skills pro](https://github.com/AllThingsSmitty/css-protips)

- [fantasai 54: Evolution of CSS Layout: 1990s to the Future](http://fantasai.inkedblade.net/weblog/2012/css-layout-evolution/)

> To change the mouse pointer with CSS, use "cursor"
> To set it to a pointer, use "default"
> To set it to a hand, use "pointer"
— [Jake Archibald](https://twitter.com/jaffathecake/status/832228132446990339)

## "HTML once, redesign CSS"

It's an utopy saying that when you change website design, you just need to change the CSS.

Because, data flow can't be controlled by CSS (not yet / partially), often for a full redesign you need to change the HTML structure (change the order of elements, wrap them, add attributes, etc.)

And because style have meaning to and related to ARIA attributes (like `aria-haspopup`, `role="document"`, `aria-expanded`, etc.) or others like `hidden`. Require JavaSscript to be enabled, to add ARIA attributes in same time of enable it's style (like adding a class `js` on root node)

**But it's not impossible.**

- https://en.wikipedia.org/wiki/Css#Limitations
- [8 CSS gotchas to start your morning off right – Isaac Lyman – Medium](https://medium.com/@isaaclyman/8-css-gotchas-to-start-your-morning-off-right-c5daade0731d)

## Write CSS

See [Classname and ID](HTML#classname-and-id)

- [Mini Convention CSS - Alsacreations](http://www.alsacreations.com/article/lire/1707-mini-convention-css.html)
- [CSS coding techniques ★ Mozilla Hacks – the Web developer blog](https://hacks.mozilla.org/2016/05/css-coding-techniques/)
- http://www.smashingmagazine.com/2007/05/10/70-expert-ideas-for-better-css-coding/
- http://alistapart.com/blog/post/getting-started-with-css-audits
- [Principles of writing consistent, idiomatic CSS](https://github.com/necolas/idiomatic-css)
- [CodePen's CSS by Chris Coyier on CodePen](http://codepen.io/chriscoyier/blog/codepens-css)
- http://ianfeather.co.uk/css-at-lonely-planet/
- http://openweb.eu.org/articles/prendre-des-conventions-et-les-documenter
- [CSS Best Practices](http://fantasai.inkedblade.net/style/talks/best-practices/#title)
- [Writing the best CSS when building with HTML5](http://toddmotto.com/writing-the-best-css-when-building-with-html5/)
- [MCSS](http://operatino.github.io/MCSS/en/)
- [Writing efficient CSS - Web developer guide | MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Writing_efficient_CSS)
- [You might not need a CSS framework ★ Mozilla Hacks – the Web developer blog](https://hacks.mozilla.org/2016/04/you-might-not-need-a-css-framework/)
- [Profiling CSS for fun and profit — Perfection Kills](http://perfectionkills.com/profiling-css-for-fun-and-profit-optimization-notes/)
- [The invisible parts of CSS · MadebyMike](https://madebymike.com.au/writing/the-invisible-parts-of-CSS/)

Lints & analysers:

- [CSSLint/csslint](https://github.com/CSSLint/csslint/)
- [SlexAxton/css-colorguard](https://github.com/SlexAxton/css-colorguard)
- [Yellow Lab Tools](http://yellowlab.tools/) and https://github.com/gmetais/YellowLabTools
- https://github.com/macbre/analyze-css

> Always document clever code.
> Always document magic numbers.
> Always comment obscure properties
— [Ethan Muller](http://seesparkbox.com/foundry/lets_write_beautiful_css_comments)

### Style guide and documentation

- [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.xml) - [Google HTML/CSS Style Guide](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml)
- [Code Guide by @mdo](http://codeguide.co/#css)
- [Website Style Guide Resources](http://styleguides.io/) - list of examples
- [CSS Guidelines (2.2.5) – High-level advice and guidelines for writing sane, manageable, scalable CSS](http://cssguidelin.es/) - https://github.com/csswizardry/CSS-Guidelines
- [Primer](http://primercss.io/scaffolding/) - The CSS toolkit and guidelines that power GitHub
- [GitHub's CSS · @mdo](http://markdotto.com/2014/07/23/githubs-css/)
- [How we do CSS at Ghost](https://dev.ghost.org/css-at-ghost/)
- [Sass Guidelines](http://sass-guidelin.es/) - can't be applied to LESS or plain CSS
- [Lightning Design System](https://www.lightningdesignsystem.com/guidelines/markup-and-style/)

Style guide generators:

- [Styleguide Generator Roundup | Welch Canavan](http://welchcanavan.com/styleguide-roundup/)
- [Topcoat](http://topcoat.io/)
- [Runway](http://runway-app.cfapps.io/guest_styleguides/new)
- [Create Free Brand & Design Style Guides with Frontify Style Guide](https://frontify.com/styleguide)

### Components

Patterns

- [GOV.UK elements](https://govuk-elements.herokuapp.com/)
- [Components · Bootstrap](http://getbootstrap.com/components/)
- [Lightning Design System](https://www.lightningdesignsystem.com/)
- [Design Patterns on CodePen](http://codepen.io/patterns)

## Viewport

- [JavaScript # Viewport sizes](JavaScript#viewport-dimension)
- [Display resolution - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Display_resolution)

Mobile: 16:9, 1280 × 800 @2dppx

`vh` is not the real viewport

### Viewport with collapsable UI

> `vh` units, which theoretically make a lot of sense in responsive designs, misfire due to this visual viewport change.
– [Toolbars, keyboards, and the viewports – Samsung Internet Developers – Medium](https://medium.com/samsung-internet-dev/toolbars-keyboards-and-the-viewports-10abcc6c3769)

- [Viewport height is taller than the visible part of the document in some mobile browsers](https://nicolas-hoizey.com/2015/02/viewport-height-is-taller-than-the-visible-part-of-the-document-in-some-mobile-browsers.html)

### Viewport ignore scrollbar thickness

- [html - Why does vw include the scrollbar as part of the viewport? - Stack Overflow](https://stackoverflow.com/questions/29551606/why-does-vw-include-the-scrollbar-as-part-of-the-viewport)
- [Viewport units: vw, vh, vmin, vmax - Web Design Weekly](https://web-design-weekly.com/2014/11/18/viewport-units-vw-vh-vmin-vmax/)

- [811403 – fix interaction of viewport units (vh,vw,vmin,vmax) with scrollbars](https://bugzilla.mozilla.org/show_bug.cgi?id=811403)
- [Bug 133271 – vw units not calculated properly when scrollbars are present and overflow is not auto](https://bugs.webkit.org/show_bug.cgi?id=133271)

## Scroll

See [Fixed elements](#fixed-elements) and [Sticky header](#sticky-header)

### Custom scrollbar

- [CSS deep-dive: matrix3d() for a frame-perfect custom scrollbar | Web | Google Developers](https://developers.google.com/web/updates/2017/03/custom-scrollbar)
- [ui-element-samples/custom-scrollbar at gh-pages · GoogleChrome/ui-element-samples](https://github.com/GoogleChrome/ui-element-samples/tree/gh-pages/custom-scrollbar)

- [scrollbar | CSS-Tricks](https://css-tricks.com/almanac/properties/s/scrollbar/)
- [Custom Scrollbars in WebKit | PoseLab](http://web.archive.org/web/20150908133656/http://poselab.com/en/custom-scrollbars-in-webkit/)
- [Customize Your Scrollbars with CSS3 and jQuery | Code Geekz](https://codegeekz.com/customize-your-scrollbars-with-css3-and-jquery/)
- [Custom Scrollbars in WebKit | CSS-Tricks](https://css-tricks.com/custom-scrollbars-in-webkit/)
- [Quick Tip: Styling Scrollbars to Match Your UI Design](https://webdesign.tutsplus.com/articles/quick-tip-styling-scrollbars-to-match-your-ui-design--webdesign-9430)

### Scroll indicator 

- [CSS only scroll indicator](http://codepen.io/MadeByMike/pen/ZOrEmr)

### Scrollable shadow

Use `background-attachment: local`

Require plain background color (ex.: white) and it's not a real shadow (below content)

- [Pure CSS scrolling shadows with background-attachment: local | Lea Verou](http://lea.verou.me/2012/04/background-attachment-local/)
- [Table Design Patterns On The Web — Smashing Magazine](https://www.smashingmagazine.com/2019/01/table-design-patterns-web/#style-the-scroll)
- [Table #3: Style the scroll (basic)](https://codepen.io/huijing/pen/XBGaNQ/left/)

### Scroll behavior

Smoothing

- [scroll-behavior - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-behavior)

### Snap points

- [CSS Scroll Snap Points - CSS | MDN](https://developer.mozilla.org/en/docs/Web/CSS/CSS_Scroll_Snap_Points)
- [Introducing CSS Scroll Snap Points | CSS-Tricks](https://css-tricks.com/introducing-css-scroll-snap-points/)
- [Native CSS Scroll Snap Points](https://blog.hospodarets.com/css-scroll-snap)
- [Well-Controlled Scrolling with CSS Scroll Snap  |  Web  |  Google Developers](https://developers.google.com/web/updates/2018/07/css-scroll-snap)
- [Practical CSS Scroll Snapping | CSS-Tricks](https://css-tricks.com/practical-css-scroll-snapping/)

### Prevent body to scroll

```css
body.noscroll {
	overflow: hidden;
	position: fixed;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	height: 100%;
	width: 100%;
}
```

### Animate with scroll

- [Bind CSS keyframe animation to scroll](https://codepen.io/scottkellum/pen/WWeXab) - use a CSS variable defined with JS to control `animation-delay` of a paused animation

## Mediaqueries

> Set media query breakpoints in `em` or `ch`, not always in `px`.
— [Elika J. Etemad](http://fantasai.inkedblade.net/style/talks/best-practices/#media-queries)

- [PX, EM or REM Media Queries? | Zell Liew's blog about web design and development](https://zellwk.com/blog/media-query-units/): use `rem`, but because of Safari bug, use `em`
- If, and, or, not, etc. [Logic in Media Queries | CSS-Tricks](https://css-tricks.com/logic-in-media-queries/)
- [Using media queries - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries)
- [@media - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/@media)

### Aspect ratio

	@media (min-aspect-ratio: 4/5) {
		/* and (min-height: 250px) */
		/* rules */
	}

### Screen/viewport size, responsiveness

**Small screen first, then larger screens**. Aka mobile first.

Note: don't forget `<meta name="viewport" content="width=device-width, initial-scale=1.0">` for mobiles

- https://stackoverflow.com/questions/18500836/should-i-use-max-device-width-or-max-width
- https://stackoverflow.com/questions/6747242/what-is-the-difference-between-max-device-width-and-max-width-for-mobile-web

**TODO: use `em` instead of `px`**

Use both `max-[width|height]` and `max-device-[width|height]`. Or `max-[width|height]` and `<meta name="viewport" content="width=device-width, initial-scale=1">` (but it has drawbacks)

	@media (width >= 64em) and (height < 48em){}/* only large screen (like desktop) */

	@media (min-width: 64.01em) and (min-height: 48.01em){}/* only large screen (like desktop) */
	@media (max-width: 64em), (max-height: 48em){}/* only small screens like tablets and smaller */
	@media (max-width: 37.5em){}/* only very small screens like smartphones, here minor fixes of previous mediaquery */

	/* Small screen (usally mobile) */
	@media (max-width: 420px), (max-height: 420px){
		/*...*/
	}
	/* Large screen (usally desktop and tablets) */
	@media (min-width: 421px) and (min-height: 421px){
		/*...*/
	}

	@media screen and (min-width: 320px) {} /* Mobile */
	@media screen and (min-width: 768px) {} /* Tablets */
	@media screen and (min-width: 1024px) {} /* Ipads */
	@media screen and (min-width: 1382px) {} /* Powerbooks */

	@media (min-width: 1025px) and (min-height: 769px){}/* only large screen (like desktop) */
	@media (max-width: 1024px), (max-height: 768px){}/* only small screens like tablets and smaller */
	@media (max-width: 600px){}/* only very small screens like smartphones, here minor fixes of previous mediaquery */

	/* Wide screens */
	@media (min-width: 640px), (min-height: 640px){
		/*...*/
		
		/* Nested rules for orientation */
		@media (orientation: portrait) {
			/*small screens in portrait*/
		}
		@media (orientation: landscape) {
			/*small screens in landscape*/
		}
	}

### Fullscreen

	:root:fullscreen{
		/* ... */
	}

	@media (device-width: 100vw) and (device-height: 100vh) {}/*deprecated by CSS Media Queries Level 4 https://www.w3.org/TR/mediaqueries-4/#mf-deprecated */

- [:fullscreen - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/:fullscreen)

### Resolution

- "Device pixel ratio" or "Device pixel density" or resolution
- "Physical pixel" or "Native pixel"

```
logical pixel x device pixel ratio = physical pixel
```

```css
/* 2 or more physical pixel per logical px */
@media (-webkit-min-device-pixel-ratio: 2)/* Webkit */,
	(min-resolution: 192dpi),/* IE, Safari */
	(min-resolution: 2dppx)/* Everyone else */{
	selector{
		background-image: url("image_2x.png");
		/* or image.2x.png image-2x.png image@2x.png */
	}
}

/* A better rule: 1.25 physical pixel per logical px */
/* remove rules when dppx is supported by all major browsers */
@media (-webkit-min-device-pixel-ratio: 1.25),/* Webkit */
	(min-resolution: 120dpi),/* IE, Safari */
	(min-resolution: 1.25dppx)/* Everyone else */{ 
	selector{
		background-image: url("image.png");
	}
}
```

Use `dppx` instead of `dpi`, but it's not currently supported everywhere

- https://developer.mozilla.org/en-US/docs/Web/CSS/resolution
- http://www.w3.org/blog/CSS/2012/06/14/unprefix-webkit-device-pixel-ratio/ [and more details](http://www.brettjankord.com/2012/11/28/cross-browser-retinahigh-resolution-media-queries/)
- http://www.quirksmode.org/blog/archives/2010/04/a_pixel_is_not.html
- http://msdn.microsoft.com/en-us/library/windows/desktop/ff684173%28v=vs.85%29.aspx
- http://mnt.github.io/dpitest/
- https://stackoverflow.com/questions/476815/can-you-access-screen-displays-dpi-settings-in-a-javascript-function/477049#477049
- http://graphics.wikia.com/wiki/Pixel
- [pixels-per-degree (PPD)](https://en.wikipedia.org/wiki/Retina_Display#Technical_definition)

See [Responsive typography](#responsive-typography)

### Reduced motion

	@media (prefers-reduced-motion){
		/* *{transition: none !important; animation: none !important;} */
	}

## `orientation` change when an input is focused

	/* landscape (but with a minimum aspect ratio 3/2) to not show it on Android portrait when the keyboard is open */
	@media (min-aspect-ratio: 3/2) {
		
	}

Can test `screen.orientation`

- [android - CSS Media Query - Soft-keyboard breaks css orientation rules - alternative solution? - Stack Overflow](https://stackoverflow.com/questions/8883163/css-media-query-soft-keyboard-breaks-css-orientation-rules-alternative-solut)

## Vendor prefixes

- [CodePen - PSA: don't use gradient generators](http://codepen.io/thebabydino/full/pjxVWp)
- [Les préfixes constructeurs | Openweb.eu.org](http://openweb.eu.org/articles/les-prefixes-constructeurs)

Use autoprefixer

## Bugs

	transform: translateZ(0);

	-webkit-text-size-adjust: 100%;
	-ms-text-size-adjust: 100%;

## Supports rules

	video{
		height: 100%;
		width: 100%;
		
		/* Workaround for object-fit: cover works only if video element has 16/9 ratio */
		$ratio: 16 / 9;// ex.: 1920 / 1080
		height: 100%;
		width: 100vh * $ratio;
		min-width: 100%;
		min-height: 100vw / $ratio;
		
		position: absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
	}
	
	/* not IE and Edge */
	@supports (object-fit: cover){
		video {
			/* restore values */
			object-fit: cover;
			width: 100%;
			min-width: 0;
			min-height: 0;
			left: auto;
			top: auto;
			transform: none;
		}
	}

See [Cover and contain of replaced element](#cover-and-contain-of-replaced-element)

- [@supports - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/@supports)

For selectors supports, all rules with one unsupport selector are ignored (from CSS1):

	supports:checked, /* only if pseudo class selector is supported, the next rules will be applied */
	input[type="checkbox"] {
		opacity: 0;
	}
	
	input[type="checkbox"]:not(:checked) + label {
		background: url(/unchecked-box.svg);
	}
	
	input[type="checkbox"]:checked + label {
		background: url(/checked-box.svg);
	}

- [@supports for selectors by Taylor Hunt on CodePen](http://codepen.io/tigt/post/supports-for-selectors)

## Layout

- [position: sticky is Amazing](https://gedd.ski/post/position-sticky/)
- [The stacking context - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)

### Float

- [How browser position float – Monica Dinculescu](https://meowni.ca/posts/float-layout/)
- [Understanding CSS Layout And The Block Formatting Context — Smashing Magazine](https://www.smashingmagazine.com/2017/12/understanding-css-layout-block-formatting-context/)

### Margin collapse

Set overflow other to `auto` or `scroll`:

	element{
		overflow: auto;/*suppress "Collapsing margins"*/
	}

or:

	element::before,
	element::after{
		content: "";
		display: table;/* used as separator */
	}

- [Revisiting Margin Collapse - Pine](https://pineco.de/revisiting-margin-collapse/)
- [Collapsing Margins - SitePoint](http://www.sitepoint.com/web-foundations/collapsing-margins/)
- [Box model](https://drafts.csswg.org/css2/box.html#collapsing-margins)
- [Box model](https://www.w3.org/TR/CSS21/box.html#collapsing-margins)
- [Mastering margin collapsing - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing)
- [css - Margin on child element moves parent element - Stack Overflow](https://stackoverflow.com/questions/1762539/margin-on-child-element-moves-parent-element)

### Clear both without any elements

Or use `display: flow-root`

...but with a pseudo element.

	element-with-floats::after {
		content: "";
		display: block;
		clear: both;
	}

Or use `display: table;` to stop margin collapsing.

- http://nicolasgallagher.com/micro-clearfix-hack/

### Columns

- [Multi-column manipulation: Every Layout](https://every-layout.dev/blog/multi-column-manipulation/)

#### Number of columns

Use `column-count` or flex with `flex-direction: column`

Mediaqueries can't always be used (eg. in email client). Use specificities of [`width` + `min-width` + `max-width`](https://medium.com/@hteumeuleu/the-fab-four-technique-to-create-responsive-emails-without-media-queries-baf11fdfa848) instead.

### Complex grid / masonry

Use CSS grid

- [Hardcore CSS calc( ) – Buildit @ Wipro Digital – Medium](https://medium.com/buildit/hardcore-css-calc-bdfb0162993c)
- [HOW TO: Pure CSS masonry layouts – Medium](https://medium.com/@_jh3y/how-to-pure-css-masonry-layouts-a8ede07ba31a#)
- [Create a Responsive CSS-only Masonry layout](http://w3bits.com/css-masonry/) (use columns) like https://codepen.io/AdamBlum/pen/fwrnE
- [CSS masonry with flexbox, :nth-child(), and order | Tobias Ahlin](https://tobiasahlin.com/blog/masonry-with-css/)
- (JS) https://github.com/desandro/masonry
- (JS), 2 cols:

		for(let index = 0, stack1 = 0, stack2 = 0, num = elements.length; index < num; index++){
			let element = elements[index];
			let height = element.offsetHeight;
			if(stack1 <= stack2){
				stack1 += height;
				list1.appendChild(element);
			}else{
				stack2 += height;
				list2.appendChild(element);
			}
		}

### Fixed elements

Is wildy supported. But can be buggy on few browsers...

- http://caniuse.com/css-fixed
- http://remysharp.com/2012/05/24/issues-with-position-fixed-scrolling-on-ios/
- http://bradfrostweb.com/blog/mobile/fixed-position/

#### Overflow fixed child

Because parent overflow not work for fixed child, use `clip-path: inset(0 0 0 0)` (or depreciated `clip: rect(0, auto, auto, 0);`) instead of overflow (the depreciated `clip` works only on absolute or fixed elements).

- http://jsfiddle.net/lmeurs/jf3t0fmf/
- https://miketaylr.com/posts/2015/06/position-fixed-overflow-hidden.html
- https://stackoverflow.com/questions/12463658/parent-child-with-position-fixed-parent-overflowhidden-bug/23859719#23859719

### Grids

The grid doesn't auto size, use display flexbox or table instead

![Content that fits nicely into the grid in English doesn’t work so well in French](https://cdn-images-1.medium.com/1*K5Ahhn4JOiJgpgOy7pZa-A.gif)

See [Flexbox](#flexbox)

	@supports (display: grid){
		.container{
			display: grid;
			grid-gap: 20px;
			grid-template:
				"header header  header  header" 50px
				"aside  image   image   image" auto
				"aside  text    text    text" 400px
				"footer footer  footer  footer" 80px /
				10%     30%     30%     30%
		}
		header{
			grid-area: header;
		}
		img{
			grid-area: image;
		}
		p{
			grid-area: text;
		}
		aside{
			grid-area: aside;
		}
		footer{
			grid-area: footer;
		}
	
	}

- [CSS Grid Layout - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)
- [ptcrt/learn-grid: Curated list of the best resources available to learn CSS Grid Layout 🌐](https://github.com/ptcrt/learn-grid)
- [A Complete Guide to Grid | CSS-Tricks](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [grid layout, vers la grille parfaite – La Tête dans le Flux](https://blog.goetter.fr/2016/01/02/grid-layout-vers-la-grille-parfaite/)
- [Are grid systems still relevant in digital product design? – Subform – Medium](https://medium.com/subform/are-grid-systems-still-relevant-in-digital-407beb4128c1)
- [Does CSS Grid Replace Flexbox? | CSS-Tricks](https://css-tricks.com/css-grid-replace-flexbox/)

### Flexbox

Usefull for sliders, etc. see [Slider](#slider)

- [A Complete Guide to Flexbox | CSS-Tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [CodePen - Flexbox playground](http://codepen.io/enxaneta/full/adLPwv/)
- [Flexbox Cheatsheet Cheatsheet](http://jonibologna.com/flexbox-cheatsheet/)
- [flexbox in 5 minutes](http://flexboxin5.com/)
- [Useful Flexbox Technique: Alignment Shifting Wrapping | CSS-Tricks](https://css-tricks.com/useful-flexbox-technique-alignment-shifting-wrapping/)
- [Understanding Flexbox · MadebyMike](http://madebymike.com.au/writing/understanding-flexbox/)
- [Flexbox Tester · MadebyMike](http://madebymike.com.au/demos/flexbox-tester/)
- [Visual CSS flexbox builder | Webflow](https://flexbox.webflow.com/)
- [Flexbox Patterns](http://www.flexboxpatterns.com/home)
- [CSS Flexbox Is Entirely Logical (Almost) / Paul Robert Lloyd](https://paulrobertlloyd.com/2016/03/logical_flexbox)
- Change layout of lastest elements with [`nth-child()`](#range-selector) [Quantity queries and Flexbox part 2 | Charlotte Jackson, Front-end developer](http://www.lottejackson.com/learning/quantity-queries-and-flexbox-part-2)
- [Quick Tip: How z-index and Auto Margins Work in Flexbox](https://www.sitepoint.com/quick-tip-how-z-index-and-auto-margins-work-in-flexbox/)

Notes:

- [Flexbox treats flex-container :before and :after as first class flex-items. They can really goof up alignment + centering](https://twitter.com/wesbos/status/743861247486099456)
- `min-width: 0;` (and `min-height: 0`, `overflow: hidden;` can also work) to allow containers with nowrap text or images/video/canvas to shrink

- [Flexbox and Truncated Text | CSS-Tricks](https://css-tricks.com/flexbox-truncated-text/)
- [(Flexbox) min-width: 0 is the new zoom: 1 – La Tête dans le Flux](https://blog.goetter.fr/2016/11/09/flexbox-min-width-0-is-the-new-zoom-1/)

`text-align` will not work in flex item with only one line of text. Don't use flex, or use `justify-content: center`. Demo `<p style="border: 1px solid; display: flex; text-align: center; width: 100px">text</p>`

#### Alternative

Performances and support can be better.

- [Almost complete guide to flexbox (without flexbox) | Kenan Yusuf](http://kyusuf.com/post/almost-complete-guide-to-flexbox-without-flexbox)

##### Table can replace flexbox

Don't forget to use `table-layout: fixed`

- [The Anti-hero of CSS Layout - "display:table" | Colin Toh](http://colintoh.com/blog/display-table-anti-hero)
- http://updates.html5rocks.com/2013/10/Flexbox-layout-isn-t-slow
- https://stackoverflow.com/questions/18419082/flexbox-vs-tables-why-do-we-need-flexbox
- http://benfrain.com/css-performance-test-flexbox-v-css-table-fight/

#### Flex image stretch

Larger image will stretch to it's natural height regardless of CSS width

	<style>
		.flex-container{
			width: 50px
		}
		.flex-item{
			width: 50px;
		}
	</style>
	<div class="flex-container">
		<img class="flex-item" src="image.jpg"><!-- natural width and height: 300px -->
	</div>

Override default `align-items: stretch` with `align-self: center` on `img` or `align-items: center` on flex container

#### Flexbox centering

See [Alignment](#alignment)

#### Nav bar

	<ul class="toc">
		<li class="toc-item"><a class="toc-item-link" href="">Link 1</a></li>
		<li class="toc-item"><a class="toc-item-link" href="">Link with long label 2</a></li>
		<li class="toc-item"><a class="toc-item-link" href="">Link 3</a></li>
		<li class="toc-item"><a class="toc-item-link" href="">Link 4</a></li>
		<li class="toc-item"><a class="toc-item-link" href="">Link with very long long label label label 5</a></li>
		<li class="toc-item"><a class="toc-item-link" href="">Link 6</a></li>
	</ul>
	<style>
	.toc{
		display: flex;
		align-items: stretch;
	}
	
	.toc-item{
		flex-grow: 1;
		width: 100px;
		display: flex;
	}
	
	.toc-item-link{
		flex-grow: 1;
		padding: 16px;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	</style>

#### Order

`order: N` for accessibility add `tabIndex: N`:

**Don't**, see [HTML#tabindex]

	<div style="display: flex;">
		<button style="order: 3;" tabindex="3">1</button>
		<button style="order: 2;" tabindex="2">2</button>
		<button style="order: 1;" tabindex="1">3</button>
	</div>

Use instead:

	<div style="display: flex;">
		<button id="b1" aria-flowto="b3" style="order: 3;">1</button>
		<button id="b2" aria-flowto="b1" style="order: 2;">2</button>
		<button id="b3" aria-flowto="b2" style="order: 1;">3</button>
	</div>

- http://ljwatson.github.io/decks/2016/cssday/index.html#31

#### Flex grow

Line break [Flex-grow 9999 Hack](http://joren.co/flex-grow-9999-hack/)

	.container {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
	}
	/*will grow only if item-b below */
	.item-a {
		flex-grow: 1;
	}
	.item-b {
		flex-grow: 9999;
		flex-basis: 20em;
	}
 
- [`flex-grow` is weird. Or is it? | CSS-Tricks](https://css-tricks.com/flex-grow-is-weird/)

### Inline list

- [Accessible inline list with bullets between items — Artem Sapegin’s Blog](https://blog.sapegin.me/all/accessible-inline-list/)

### Inline blocks

- flexboxes
- table and table-cell
- grid
- inline blocks (optionally with `white-space: nowrap;`): need to remove space between element with HTML comment `<!-- -->`
- float: hard to control
- columns

- [CodePen - Faire des colonnes : comparatif](http://codepen.io/vincent-valentin/full/ONPvXL/)
- [Fighting the Space Between Inline Block Elements | CSS-Tricks](https://css-tricks.com/fighting-the-space-between-inline-block-elements/)

#### Inline blocks and `text-align: justify`

- https://stackoverflow.com/questions/11589590/text-align-justify-inline-block-elements-properly
- http://www.barrelny.com/blog/text-align-justify-and-rwd/

### Alignment

See [Align text](SVG#align-text)

- [CSS Box Alignment Module Level 3](https://www.w3.org/TR/css-align-3/#overview)
- [Les alignements en CSS3 : passez-moi deux doliprane SVP – La Tête dans le Flux](https://blog.goetter.fr/2017/01/28/les-alignements-en-css3-passez-moi-deux-doliprane-svp/)
- [Box Alignment Cheatsheet - rachelandrew.co.uk](https://rachelandrew.co.uk/css/cheatsheets/box-alignment)

#### Horizontal align based on number of lines

	figure {
		text-align: center; /* Set text align to center */
	}
	figcaption {
		display: inline-block; /* Set this element to inline-block */
		text-align: left; /* Set text align to left */
	}

- [Aligning text smartly in CSS](http://nocode.in/aligning-text-smartly-in-css/)

#### Centering

vertical align, horizontal align

Don't use `line-height: 0; display: inline-block;` because overriding `line-height` can break lot of things

- [Centering in CSS: A Complete Guide | CSS-Tricks](https://css-tricks.com/centering-css-complete-guide/)

##### Centering with grid

	parent {
		display: grid;
		height: 400px;/* some height */
		place-items: center center;
	}

##### Centering with flexbox


	.parent { display: flex; }
	.child { margin: auto; }

or 

	.parent {
		display: flex;
		align-items: center;
		justify-content: center;
	}

Note: .child can be a text node (not an element)

Can be done with display table too.

- [css - How to absolutely position the baseline of text in HTML - Stack Overflow](https://stackoverflow.com/questions/20443220/how-to-absolutely-position-the-baseline-of-text-in-html)

##### Centering with table layout

	.parent {diplay: table; width: 100%;}
	.parent-content {display: table-cell; vertical-align: center;}
	.child {margin: 0 auto;}

##### Centering with pseudo element

	.parent {text-align: center;}
	.parent::before { content: ""; display: block; height: 100%; vertical-align: middle;}
	.child {display: inline-block; vertical-align: middle; text-align: left;/*restore*/}

The pseudo element can also use `inline-table` (`inline-block` doesn't work well in Firefox)

### Vertical percentages

Aka ratio

> A percentage value on top/bottom padding or margins is relative to the width of the containing block
> A percentage value on height is relative to the height of the containing block (same for min/max height)
> a Percentage value on top and bottom values for a positioned element is relative to the height of the containing block
> Percentage values are not allowed on border widths (not even left and right)

> The percentage is calculated with respect to the width of the generated box's containing block, even for 'padding-top' and 'padding-bottom'.
— http://www.w3.org/TR/CSS2/box.html#padding-properties

Sass:

	$ratio: 16/9;
	padding-top: 100% / $ratio;// 69.44%

- [Aspect Ratio Boxes | CSS-Tricks](https://css-tricks.com/aspect-ratio-boxes/) - about ratio + trick for overflow content
- [Vertical Percentages in CSS](https://www.impressivewebs.com/vertical-percentages-css/)
- [Creating Intrinsic Ratios for Video · An A List Apart Article](http://alistapart.com/article/creating-intrinsic-ratios-for-video)

### Responsive

- [Responsive Web Design Patterns | This Is Responsive](http://bradfrost.github.io/this-is-responsive/patterns.html)
- [Responsive Logos](http://www.responsivelogos.co.uk/)
- [Sizzy](https://sizzy.co/) - Tool display side by side differents screen resolutions of a website (use iframes). See [kitze/sizzy: A tool for developing responsive websites crazy-fast](https://github.com/kitze/sizzy)
- [The Flexbox Holy Albatross | HeydonWorks](http://www.heydonworks.com/article/the-flexbox-holy-albatross) - Kind of container query (configuration switch), based on `flex-basis`

See [Responsive typography](#responsive-typography)

#### Clamp values

Aka CSS locks, or min and max

	element { font-size: 1rem;  /* default below 600px */ }
	@media (min-width: 600px){
		element {
			font-size: calc(1rem * 3vw);
		}
	}

For font size lock

	/*========*\
	* Settings *
	\*========*/
	
	// What's your idea of a minimum readable font-size for body text?
	$base-font-size: (14px / 16px) * 1rem; // converts 14px to rems
	
	// How many units of the above do you want before your layout begins to grow?
	// These dementions will be used to determine your prefered aspect-ratio.
	// You will need to use integers in order for it to be considered a valid aspect ratio
	$base-layout-width: 60;
	$base-layout-height: 40;
	
	// On a scale from 0 to 1 how strong should the growth effect be?
	// (anything less that 1 will allow cmd+ & cmd- to work again)
	$growth-scalar: .5;
	
	
	/*===================*\
	* The Important Stuff *
	\*===================*/
	
	$aspect-ratio: "#{$base-layout-width}/#{$base-layout-height}";
	$min-growth-width: $base-font-size * $base-layout-width;
	$min-growth-height: $base-font-size * $base-layout-height;
	
	:root {
	  font-size: $base-font-size;
	
	  @media (min-width: $min-growth-width) and (min-height: $min-growth-height) {
		@media (max-aspect-ratio: $aspect-ratio) {
		  font-size: calc(#{$base-font-size} + ((#{100vw/$base-layout-width} - #{$base-font-size}) * #{$growth-scalar}));
		}
		@media (min-aspect-ratio: $aspect-ratio) {
		  font-size: calc(#{$base-font-size} + ((#{100vh/$base-layout-height} - #{$base-font-size}) * #{$growth-scalar}));
		}
	  }
	}

- [The math of CSS locks](https://fvsch.com/code/css-locks/)
- [Responsive typography](#responsive-typography)
- [Truly Fluid Typography With vh And vw Units – Smashing Magazine](https://www.smashingmagazine.com/2016/05/fluid-typography/#controlling-viewport-units-to-get-minimum-and-maximum-font-sizes)
- [Precise control over responsive typography · MadebyMike](http://madebymike.com.au/writing/precise-control-responsive-typography/)
- viewport units and aspect ratio http://codepen.io/webdesserts/pen/zqMZGo
- [Molten Leading in CSS | CSS-Tricks](https://css-tricks.com/molten-leading-css/)
- [The math of CSS locks](https://fvsch.com/code/css-locks/)
- [The Typekit Blog | Flexible typography with CSS locks](https://blog.typekit.com/2016/08/17/flexible-typography-with-css-locks/)

#### Responsive iframe

Use the padding (see [Vertical percentages](#vertical-percentages)) to autoscale iframes:

	<style>
		.iframe-container{
			height: 0;
			width: @width-value;
			padding-top: @width-value / (@svg-width / @svg-height);
			position: relative;
		}
		.iframe{
			position: absolute;
			top: 0;
			left: 0;
			width: 100%;
			height: 100%;
		}
	</style>
	<div class="iframe-container">
		<iframe class="iframe" ...
	</div>

Can be required for IE for inline SVG too.

- https://www.youtube.com/watch?v=lf7L8X6ZBu8#t=1343
- http://tympanus.net/codrops/2014/08/19/making-svgs-responsive-with-css/
- [Creating Intrinsic Ratios for Video · An A List Apart Article](http://alistapart.com/article/creating-intrinsic-ratios-for-video)/
- http://cjwainwright.co.uk/webdev/aspectratio/

#### Responsive table

Use `flex-direction: column;` on `tr`. But don't handle well cell with different height.

- [Designing Complex Responsive Tables In WordPress — Smashing Magazine](https://www.smashingmagazine.com/2019/09/designing-complex-responsive-tables-wordpress/)
- [Flexible data tables with CSS Grid](https://adamlynch.com/flexible-data-tables-with-css-grid/)
- [CSS only Responsive Tables](http://codepen.io/dbushell/pen/wGaamR)
- [CSS only Responsive Tables – David Bushell – Web Design & Front-end Development (based in Manchester, UK)](http://dbushell.com/2016/03/04/css-only-responsive-tables/)
- [Responsive Tables - a Collection by Chris Coyier on CodePen](http://codepen.io/collection/AdGVYP/)

### Relative positioning in table not work everywhere

- https://stackoverflow.com/questions/17526370/position-relative-not-working-with-display-table-cell

### Cover and contain of replaced element

Replaced element: image, video, canvas

Act like `background-size`

Use `object-fit` property

Fallback with CSS:

	.parent-element-to-video {
		overflow: hidden;
		position: relative; /* or absolute or fixed */
	}
	
	video {
		/* Workaround for object-fit: cover works only if video element has 16/9 ratio */
		/* cropping: */
		$ratio: 16 / 9;// ex.: 1920 / 1080
		height: 100%;
		width: 100vh * $ratio;
		min-width: 100%;
		min-height: 100vw / $ratio;
		
		/* centering: */
		position: absolute;
		left: 50%;
		top: 50%;/*
		transform: translate(-50%, -50%);
	}

Fabllback with SVG (works only for images):

	<svg viewBox="0 0 1 1" width="100" height="100">
		<image xlink:href="path/to/image.jpg" width="100%" height="100%" preserveAspectRatio="xMidYMid slice"/>
	</svg>

See also [Vertical percentages](#vertical-percentages)

- [javascript - simulate background-size:cover on \<video\> or <img> - Stack Overflow](https://stackoverflow.com/questions/10797632/simulate-background-sizecover-on-video-or-img/29997746#29997746)
- [html - Is there an equivalent to background-size: cover and contain for image elements? - Stack Overflow](https://stackoverflow.com/questions/11670874/is-there-an-equivalent-to-background-size-cover-and-contain-for-image-elements/31059913#31059913)
- [object-fit - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/object-fit)
- [Cropping Image Thumbnails with SVG - Cloud Four](https://cloudfour.com/thinks/cropping-image-thumbnails-with-svg/)

### Transform

Offset an element vertically bt its width:

	transform: rotate(90deg) translateX(100%) rotate(-90deg);

Is the same as use `transform-origin: bottom center;`

- [Tool to get `matrix3d`](http://codepen.io/fta/pen/ifnqH)

### Sticky header

- viewport height minu sticky header height
- keyboard navigation should use full height minus sticky header height
- anchor scroll position shifted with header height

- [Sticky headers — Medium](https://medium.com/@adactio/sticky-headers-fe9537519c83)
- [Autoscroll to anchors](JavaScript#autoscroll-to-anchors)

### Full width content

Aka banner, hero, bust-outs, takeover, full bleed

With CSS grid:

→ See links

With `*:not()` selector:

	post > *:not( img ):not( video ) {
		margin-left: auto;
		margin-right: auto;
		max-width: 50rem;
		padding-left: 5%;
		padding-right: 5%;
	

Use viewport units:

	.bust-out { margin: auto calc(50% - 50vw) }

	.bust-out-with-margins {
		margin-left: calc(50vw - 50% + [LEFT MARGIN HERE]);
		margin-right: calc(50vw - 50% + [RIGHT MARGIN HERE]);
	}

	.bust-out-with-max-width {
		margin: calc(50vw - 50%);
		max-width: 800px;
		transform: translateX(calc(50% - 50vw));
	}

Note: Using 100vw will display horizontal scrollbar if the document height is higher than the viewport

Use padding:

```html
<style>
.simple-page{
	margin: 0 auto;
	max-width: 1044px;
	position: relative;
	
	/*decorations*/
	font-family: sans-serif;
	/*end of decorations*/
}
.content{
	/*decorations*/
	background: green;
	padding: 20px;
	/*end of decorations*/
}
/* Some content of simple page overflow for full width */
.content-overflow{
	margin-left: calc(50% - 50vw);
	width: 100vw;
	min-width: 100%;
	padding: 0 calc(50vw - 50%);
	margin-right: calc(100% - 50vw);/* break line for flex parent */
	box-sizing: border-box;
	
	/*decorations*/
	background: gray;
	/*end of decorations*/
}
</style>
<div class="simple-page">
	<p class="content">Content</p>
	<div class="content-overflow">
		<p class="content">Full width content</p>
	</div>
</div>
```

Use a pseudo element. Fix issue if content larger than viewport

```html
<style>
.simple-page{
	margin: 0 auto;
	max-width: 1044px;
	
	/*decorations*/
	font-family: sans-serif;
	/*end of decorations*/
}
.content{
	/*decorations*/
	background: green;
	padding: 20px;
	/*end of decorations*/
}
/* Some content of simple page overflow for full width */
.content-overflow{
	position: relative;
}
.content-overflow::before{
	content: "";
	height: 100%;
	width: 100vw;
	left: calc(-50vw + 50%);
	position: absolute;
	margin-right: calc(100% - 50vw);/* break line for flex parent */
	z-index: -1;
	
	/*decorations*/
	background: gray;
	/*end of decorations*/
}
</style>
<div class="simple-page">
	<p class="content">Content</p>
	<div class="content-overflow">
		<p class="content">Full width content</p>
	</div>
</div>
```

- [Breaking Out With CSS Grid Layout - Cloud Four](https://cloudfour.com/thinks/breaking-out-with-css-grid-layout/)
- [Hassle-free Full Bleed with *:not() - daverupert.com](http://daverupert.com/2017/03/full-bleed-with-not/)
- [Bust elements out of their containers with one line of CSS by Taylor Hunt on CodePen](https://codepen.io/tigt/post/bust-elements-out-of-containers-with-one-line-of-css)
- [Full Width Containers in Limited Width Parents | CSS-Tricks](https://css-tricks.com/full-width-containers-limited-width-parents/)
- [Full Browser Width Bars | CSS-Tricks](https://css-tricks.com/full-browser-width-bars/)

### Z-index

Note:

- opacity change z-index
- new stack context (transform or perspective) kill z-index and fixed position

Negative z-index:

	a, css: null
		b, css: z-index = 1
		c, css: null → z-index == parent's z-index (here auto, means 0) "The stack level of the generated box in the current stacking context is the same as its parent's box."
		d, css: z-index = -1 → behind it's parent

- [Managing Z-Index In A Component-Based Web Application — Smashing Magazine](https://www.smashingmagazine.com/2019/04/z-index-component-based-web-application/) - TLDR; create a stacking context for each component
- [What No One Told You About Z-Index — Philip Walton](https://philipwalton.com/articles/what-no-one-told-you-about-z-index/)
- [The stacking context - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)
- [perspective - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/perspective)
- [CSS Positioned Layout Module Level 3](https://www.w3.org/TR/css3-positioning/#det-stacking-context)
- [z-index - CSS | MDN](https://developer.mozilla.org/en/docs/Web/CSS/z-index)

### Overflow

- [Heydon/forceFeed](https://github.com/Heydon/forceFeed) - To debug, add random words until it's break
- [Flexible Overflow](http://kizu.ru/en/blog/flexible-overflow/) - Overflow text

## Text

- [Plumber Documentation](https://jamonserrano.github.io/plumber-sass/)

### Font weight

Note: always declare `font-weight` in `@font-face` (if not `normal` or `400`). Don't use different font name for styles.

Tip: Changing weight based on ambient light. "Heavy" font in low-light. See also [Variable font](OpenType#variable-font)

If weight is unavailable, weights 100–500 will render as normal, 600–900 will render as bold, or use [font-synthesis - CSS | MDN](https://developer.mozilla.org/en/docs/Web/CSS/font-synthesis)

[Equivalent of values](http://www.w3.org/TR/css-fonts-3/#font-weight-numeric-values):

- `100`: thin
- `200`: extra-light / ultra-light
- `300`: light
- `400` and `normal`: normal / book / roman
- `500`: medium
- `600`: semi-bold / demi-bold
- `700` and `bold`: bold
- `800`: extra bold / ultra bold
- `900`: black / heavy

Other values

- `bolder`, `lighter`: A darker or lighter version of the font relative to the weight inherited from the parent.
- `inherit`: The element should have the same font-weight setting as the parent.

All foundries don't use the same names:

- http://help.typekit.com/customer/portal/articles/6855-using-multiple-weights-and-styles:
	- 100 thin
	- 200 extra-light
	- 300 light
	- 400 normal, book
	- 500 medium
	- 600 demi-bold
	- 700 bold
	- 800 heavy
	- 900 black
- http://www.webtype.com/info/articles/fonts-weights/:
	- 100 Extra Light or Ultra Light
	- 200 Light or Thin
	- 300 Book or Demi
	- 400 Normal or Regular
	- 500 Medium
	- 600 Semibold, Demibold
	- 700 Bold
	- 800 Black, Extra Bold or Heavy
	- 900 Extra Black, Fat, Poster or Ultra Black
- http://elliotjaystocks.com/blog/font-weight-in-the-age-of-web-fonts/:
	- 100 Ultra Light
	- 200 Thin
	- 300 Light
	- 400 Normal, Roman, or Regular
	- 500 Medium
	- 600 Bold
	- 700 Heavy
	- 800 Black
	- 900 Ultra or Extra Black
- http://en.wikipedia.org/wiki/Univers#Linotype_numbering_system and http://en.wikipedia.org/wiki/Univers#The_Frutiger_numbering_system (list all names in relative order):
	- Ultra Light
	- Thin
	- Light
	- Regular
	- Medium
	- Bold
	- Heavy
	- Black
	- Extra Black
- http://en.wikipedia.org/wiki/Font#Weight (list all names in relative order):
	- Hairline
	- Thin
	- Ultra-light
	- Extra-light
	- Light
	- Book
	- Normal / regular / roman / plain
	- Medium
	- Demi-bold / semi-bold
	- Bold
	- Extra-bold / extra
	- Heavy
	- Black
	- Extra-black
	- Ultra-black / ultra
- FontLab weights:
	- 100 Thin 100
	- 200 UltraLight / ExtraLight
	- 300 Light
	- 400 Book / Regular / Normal
	- 500 Medium
	- 600 DemiBold / SemiBold
	- 700 Bold
	- 800 ExtraBold
	- 900 Heavy / Black / Ultra / UltraBlack
	- 1000 Fat / ExtraBlack
- Fontforge weights:
	- 100 Thin
	- 200 Extra-Light
	- 300 Light
	- 400 Book
	- 500 Medium
	- 600 Demi-Bold
	- 700 Bold
	- 800 Heavy
	- 900 Black
- [OpenType specs](https://www.microsoft.com/typography/otspec/os2ver1.htm#wtc):
	- 100 Thin
	- 200 Extra-light (Ultra-light)
	- 300 Light
	- 400 Normal (Regular)
	- 500 Medium
	- 600 Semi-bold (Demi-bold)
	- 700 Bold
	- 800 Extra-bold (Ultra-bold)
	- 900 Black (Heavy)

- http://v1.jontangerine.com/silo/typography/naming/

### Font faces

- https://mathiasbynens.be/notes/unquoted-font-family

Use the same `font-family` name for all styles, weights and stretches. **Always include only the styles, weights and stretches you use.**

```css
@font-face {
	font-family: "Open Sans";
	font-style: normal;
	font-weight: 300;
	font-stretch: normal;
	src: local("Open Sans Light"), local("OpenSans-Light"),
		url(opensans-light.woff2) format("woff2"),
		url(opensans-light.woff) format("woff");
}
@font-face {
	font-family: "Open Sans";
	font-style: italic;
	font-weight: 300;
	font-stretch: normal;
	src: local("Open Sans Light Italic"), local("OpenSansLight-Italic"),
		url(opensans-lightitalic.woff2) format("woff2"),
		url(opensans-lightitalic.woff) format("woff");
}

/*
...do the same for all styles, weights and stretch you want to use
*/

@font-face {
	font-family: "Open Sans";
	font-style: italic;
	font-weight: 800;
	src: local("Open Sans Extrabold Italic"), local("OpenSans-ExtraboldItalic"),
		url(opensans-extrabolditalic.woff2) format("woff2"),
		url(opensans-extrabolditalic.woff) format("woff");
}

/*
... you can also use a font only for specific chars
*/
@font-face {
	font-family: "Open Sans";
	src: local("Open Sans Special"), local("OpenSansSpecial"),
		url(opensansspecial.woff2) format("woff2"),
		url(opensansspecial.woff) format("woff");
	unicode-range: U+2D, U+3D;/* use this font as "Open Sans" for only chars "-" and "="*/
}
```

Then use:

	font-family: "Open Sans", sans-serif;

#### Font web safe

`font-family: Helvetica, Arial, sans-serif` is the same as `font-family: sans-serif` (except iOS <= 5). See [fontfamily.io](http://fontfamily.io/sans-serif)

- [fontfamily.io](http://fontfamily.io/)
- [CSS Font Stack: Web Safe and Web Font Family with HTML and CSS code.](http://www.cssfontstack.com/)
- http://web.archive.org/web/20130426150237/http://www.codestyle.org/css/font-family/sampler-CombinedResultsFull.shtml

```css
*{
	font-family: Arial, Helvetica, sans-serif;
	font-family: Arial Black, Gadget, sans-serif;
	font-family: Bookman Old Style, serif;
	font-family: Comic Sans MS, cursive;
	font-family: Courier, monospace;
	font-family: Courier New, Courier, monospace;
	font-family: Garamond, serif;
	font-family: Georgia, serif;
	font-family: Impact, Charcoal, sans-serif;
	font-family: Lucida Console, Monaco, monospace;
	font-family: Lucida Sans Unicode, Lucida Grande, sans-serif;
	font-family: MS Sans Serif, Geneva, sans-serif;
	font-family: MS Serif, New York, sans-serif;
	font-family: Palatino Linotype, Book Antiqua, Palatino, serif;
	font-family: Symbol, sans-serif;
	font-family: Tahoma, Geneva, sans-serif;
	font-family: Times New Roman, Times, serif;
	font-family: Trebuchet MS, Helvetica, sans-serif;
	font-family: Verdana, Geneva, sans-serif;
	font-family: Webdings, sans-serif;
	font-family: Wingdings, Zapf Dingbats, sans-serif;
}
```

Times New Roman et serif

	font-family: Cambria, Hoefler Text, Utopia, Liberation Serif", Nimbus Roman No9 L Regular, Times, Times New Roman, serif;

Georgia

	font-family: Constantia, Lucida Bright, Lucidabright, Lucida Serif, Lucida, DejaVu Serif, Bitstream Vera Serif, Liberation Serif, Georgia, serif;

Garamond

	font-family: Palatino Linotype, Palatino, Palladio, URW Palladio L, Book Antiqua, Baskerville, Bookman Old Style, Bitstream Charter, Nimbus Roman No9 L, Garamond, Apple Garamond, ITC Garamond Narrow, New Century Schoolbook, Century Schoolbook, Century Schoolbook L, Georgia, serif;

Helvetica/Arial

	font-family: Frutiger, Frutiger Linotype, Univers, Calibri, Gill Sans, Gill Sans MT, Myriad Pro, Myriad, DejaVu Sans Condensed, Liberation Sans, Nimbus Sans L, Tahoma, Geneva, Helvetica Neue, Helvetica, Arial, sans serif;

Verdana

	font-family: Corbel, Lucida Grande, Lucida Sans Unicode, Lucida Sans, DejaVu Sans, Bitstream Vera Sans, Liberation Sans, Verdana, Verdana Ref, sans serif;

Trebuchet

	font-family: Segoe UI, Candara, Bitstream Vera Sans, DejaVu Sans, Bitstream Vera Sans, Trebuchet MS, Verdana, Verdana Ref, sans serif;

Impact

	font-family: Impact, Haettenschweiler, Franklin Gothic Bold, Charcoal, Helvetica Inserat, Bitstream Vera Sans Bold, Arial Black, sans serif;

Monospace

	font-family: Consolas, Andale Mono WT, Andale Mono, Lucida Console, Lucida Sans Typewriter, DejaVu Sans Mono, Bitstream Vera Sans Mono, Liberation Mono, Nimbus Mono L, Monaco, Courier New, Courier, monospace;

Github:

	font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol"

WordPress admin and Medium interface:

	font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", sans-serif;


### Fonts and FO*T

- FOUT (Flash Of Unstyled Text), FOFT (Flash Of Fallback Text) or FOUC (Flash Of Unstyled Text): default styles prior to loading an external CSS stylesheet
- FOIT (Flash Of Invisible Text): Load font with JS
- FOFT (Flash Of Faux Text): Load all font variants (bold & italic) before apply font

One of the technique use the `LocalStorage` to store the inlined critical CSS served for the first time (a JS load the rest of CSS + store this CSS in LS + set a cookie), and the next time, if there is a cookie set don't inline the CSS (a JS will retrive the critical CSS in LS) and add a link to rest of CSS. See [CSSconf EU 2014 | Patrick Hamann: CSS and the Critical Path @ 23:41](https://www.youtube.com/watch?v=_0Fk85to6hA#t=1421)
But DON'T use `LocalStorage` but browser's own mecanism: cache. `LocalStorage` is not suitable for font storage. It use memory (RAM), is synchronous, persistent (no cache management), size limited (by default something like 5MB), and disabled with private or incognito modes.
See WebService.

Find a fallback font with https://meowni.ca/font-style-matcher/ (https://github.com/notwaldorf/font-style-matcher) or 'x-height matching' on the [fontsquirrel webfont generator](https://www.fontsquirrel.com/tools/webfont-generator), under expert mode

See `font-display` property.

> FOIT-fix anti-pattern: embed fonts as Data URIs in main CSS, e.g. alibaba.com — instead of invisible text, this blocks page render.
— [Zach Leatherman on Twitter: "FOIT-fix anti-pattern: embed fonts as Data URIs in main CSS, e.g. http://t.co/ON6wJsomgd—instead of invisible text, this blocks page render."](https://twitter.com/zachleat/status/587725066244386816)

- [Font style matcher](https://meowni.ca/font-style-matcher/) - Tool to define for reduce FOUC
- [A Comprehensive Guide to Font Loading Strategies—zachleat.com](https://www.zachleat.com/web/comprehensive-webfonts/)
- [Non-blocking web fonts using LocalStorage — CrocoDillon](http://crocodillon.com/blog/non-blocking-web-fonts-using-localstorage)
- [Dev.Opera — Better @font-face with Font Load Events](https://dev.opera.com/articles/better-font-face/)
- [Smartphone Browser localStorage is up to 5x Faster than Native Cache (New Research) | Mobify](http://www.mobify.com/blog/smartphone-localstorage-outperforms-browser-cache/)
- [CSS Font Loading Module Level 3](http://dev.w3.org/csswg/css-font-loading/)
- [Fighting the @font-face FOUT - Paul Irish](http://www.paulirish.com/2009/fighting-the-font-face-fout/)
- http://blog.typekit.com/2013/03/28/introducing-adobe-blank/
- [How we use web fonts responsibly, or, avoiding a @font-face-palm | Filament Group, Inc., Boston, MA](http://www.filamentgroup.com/lab/font-loading.html)
- [Font Loading Revisited with Font Events | Filament Group, Inc., Boston, MA](http://www.filamentgroup.com/lab/font-events.html)
- [The Performance and Usability of Font Loading // Speaker Deck](https://speakerdeck.com/zachleat/the-performance-and-usability-of-font-loading)
- [Optimisez vos polices web - Alsacreations](https://www.alsacreations.com/article/lire/1741-Optimisez-vos-polices-web.html)
- [CSS font-display: The Future of Font Rendering on the Web — SitePoint](https://www.sitepoint.com/css-font-display-future-font-rendering-web/)

### Font size

Use `font-size: 100%` (or `1em` / `1rem`) on root for `~16px`

**You should'nt use absolute values (like `pt`, `px`, `vw`). Let the UA respect the user's font settings.** See [@heydon@mastodon.social on Twitter: "Periodic reminder: don't set your font sizes in `px`. At all. Ever. It still suppresses the ability to resize text in browser settings. #a11y https://t.co/uhQUm3P9aJ" / Twitter](https://twitter.com/heydonworks/status/1151443153657958405?s=12)

It's why we use `calc()` function.

- [Sara Soueidan‏: "\[...\] about using vw for font sizes \[...\] basically, don’t"](https://mobile.twitter.com/SaraSoueidan/status/749695520143093760)
- [Nice Web Type: "Type sized in pixels ignores user font-size preferences. This is Chrome 52 \[...\]"](https://twitter.com/nicewebtype/status/773174521268465665)
- [Nice Web Type: "Type sized with viewport units (vw, vh, vmin) *also* ignores user font-size preferences" ](https://twitter.com/nicewebtype/status/773176544634232832)

Browser implement now have a zoom function instead of text sizing, but it a false excuse to don't use `rem` and `em`.

Font size should not below equivalent of `10px` (Firefox limit to `10px` min). In some languages specifically CJK font size should be `12px` min

- Chrome: Go to settings > show advanced settings > web-content.
- Firefox: Go to preferences > content > fonts and colors.
- Internet Explorer: Click on page > text-size

Arguments against `em`: [In CSS: use pixels, not em](http://jgthms.com/in-css-use-pixels-not-em.html) (some arguments are incorrect)

- [CodePen - Accessibility of viewport percentage units](http://codepen.io/vcurd/full/ByerKw)
- [Accessibility at Penn State | Font Size on the Web](http://accessibility.psu.edu/fontsizehtml/)
- [Care With Font Size - Quality Web Tips](http://www.w3.org/QA/Tips/font-size)
- [Responsive typography](#responsive-typography)
- [REM vs EM – The Great Debate | Zell Liew's blog about web design and development](http://zellwk.com/blog/rem-vs-em/)
- [Building Resizeable Components with Relative CSS Units | CSS-Tricks](https://css-tricks.com/building-resizeable-components-relative-css-units/)
- [Size Calculator](http://sizecalc.com/)
- [Modularscale](http://www.modularscale.com/)

- See also [Graphics/Fonts]()

#### Responsive typography

Aka Responsive font, flexible typography

For `font-size` and/or `line-height`, etc.

```css
element{
	font-size: calc(2rem + 3vw);
}
```

- [Font size](#font-size)
- [Clamp values](#clamp-values)
- [Variable font](OpenType#variable-font)
- [Truly Fluid Typography With vh And vw Units – Smashing Magazine](https://www.smashingmagazine.com/2016/05/fluid-typography/)
- [The Typekit Blog | Flexible typography with CSS locks](https://blog.typekit.com/2016/08/17/flexible-typography-with-css-locks/)
- [Fluid Responsive Typography With CSS Poly Fluid Sizing – Smashing Magazine](https://www.smashingmagazine.com/2017/05/fluid-responsive-typography-css-poly-fluid-sizing/)

### Font metrics

- [Deep dive CSS: font metrics, line-height and vertical-align - Vincent De Oliveira](http://iamvdo.me/en/blog/css-font-metrics-line-height-and-vertical-align) - How metrics are computed and the relation with `line-height` and `vertical-align`

### Use unitless `line-height`

Prefer use unitless `line-height`.

- [Prefer unitless numbers for line-height values - line-height - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/line-height#Prefer_unitless_numbers_for_line-height_values)

### Text direction

Aka Vertical text

There is a CSS property for that, especially for Japanese scripts

- [writing-mode - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/writing-mode)
- [text-orientation - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/text-orientation)
- [text-combine-upright - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/text-combine-upright)
- [CSS Writing Mode](https://ishadeed.com/article/css-writing-mode/)

See also

- [direction - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/direction)

### Text position on baseline

```html
<p class="text">the baseline is at 100px</p>
```

```css
/**
Create a vertical spacer. It will be aligned with the parent's content baseline:
**/
.text::before{
	content: "";
	/*the Y value:*/
	height: 100px;
	width: 0px;
	display: inline-block;
}
```

- [css - How to absolutely position the baseline of text in HTML - Stack Overflow](https://stackoverflow.com/questions/20443220/how-to-absolutely-position-the-baseline-of-text-in-html/36476034#36476034)

### Ellipsis

Or text overflow and "..."/"…"

```css
*{
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
}
```

but can't be multilines (but workaround exist, see below)

- [text-overflow - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/text-overflow)
- [CSS text-overflow: ellipsis; not working? - Stack Overflow](https://stackoverflow.com/questions/17779293/css-text-overflow-ellipsis-not-working/17783233#17783233)
- [CSS Ellipsis: How to Manage Multi-Line Ellipsis in Pure CSS | Mobify](http://dev.mobify.com/blog/multiline-ellipsis-in-pure-css/)
- [Pure CSS for multiline truncation with ellipsis | Hacking UI](http://hackingui.com/front-end/a-pure-css-solution-for-multiline-text-truncation/)

### Underline

A different underline (than `text-decoration: underline`)

See [`text-decoration-skip`](https://developer.mozilla.org/en-US/docs/Web/CSS/text-decoration-skip)

Require a flat background color

```css
a {
	text-decoration: none;
	box-shadow: inset 0 -.14em 0 0 currentColor;
}
```

```css
a {
	--line-height: 1.2em;/* need the em unit */
	line-height: var(--line-height);
	/*background-attachment: local*/
	background: url("data:image/svg+xml,%3Csvg%20version='1.1'%20xmlns='http://www.w3.org/2000/svg'%3E%3Cline%20x='0'%20y='80%25'%20width='100%25'%20height='1'%20fill='%23cccccc'/%3E%3C/svg%3E") 0 0 / 100% var(--line-height) content-box;
	/*
	<svg version="1.1" xmlns="http://www.w3.org/2000/svg">
		<rect x="0" y="80%" width="100%" height="1" fill="#cccccc"/>
	</svg>
	*/
}
```

```css
/*
a{
	text-decoration: none;
	box-shadow: inset 0 -0.12em 0 0 rgba(255, 255, 255, 1), inset 0 -.14em 0 0 rgba(255, 255, 255, 0.5), inset 0 -.14em 0 0 currentColor;
	text-shadow: .05em 0 rgba(255, 255, 255, 1), -0.05em 0 rgba(255, 255, 255, 1), 1.5px 0 rgba(255, 255, 255, 1), -1.5px 0 rgba(255, 255, 255, 1);
}
*/
a{
	text-decoration: none;
	box-shadow:
		inset 0 calc(var(--text-underline-position) + var(--text-underline-size)) 0 0 var(--text-underline-background-color),
		inset 0 var(--text-underline-position) 0 0 color( var(--text-underline-background-color) alpha( calc( 1 - var(--text-underline-opacity) * 100% ) ) ),
		inset 0 var(--text-underline-position) 0 0 var(--text-underline-color);
	text-shadow:
		var(--text-underline-gap) 0 var(--text-underline-background-color),
		calc(-var(--text-underline-gap)) 0 var(--text-underline-background-color),
		var(--text-underline-gap-minimum) 0 var(--text-underline-background-color),
		-var(--text-underline-gap-minimum) 0 var(--text-underline-background-color);
}
```

- [Decorative Text Underline](http://codepen.io/jonneal/details/PzGYEE/)
- [Crafting link underlines on Medium](https://medium.design/crafting-link-underlines-on-medium-7c03a9274f9)
- `text-decoration-skip` editor draft

### Break words

Aka break inline blocks, wrap text

See [Ellipsis](#ellipsis), [Flexbox](#flexbox)

If used in table, use `table-layout: fixed` to force to break line.

By default use `<wbr>` or `&#8203;` to suggest break opportunities.
By default use `&shy;`/`&#173;` to suggest hyphens break opportunities (`hyphens: manual` is the default value).
By default use `<br>` to force line break

With or without, you can use:

1. `hyphens: auto` to add hyphen. But require the `lang` attribute. It's the better solution, but not well supported (can require prefixes). `&shy;`/`&#173;` can be used to suggest break opportunities.
	Only `hyphens: none` is supported on Chrome/Opera. Only manual hyphens can be used (but `hyphens: manual` is not supported).
	Result differ from browsers to browsers.
2. `word-wrap: break-word;/*compat IE*/ overflow-wrap: break-word;` to break long words anywhere.

Give the following CSS :

```css
*{
	word-wrap: break-word;/*compat IE*/
	overflow-wrap: break-word;
	-webkit-hyphens: auto;/*Safari*/
	-ms-hyphens: auto;
	hyphens: auto;/*don't forget to add lang attribute*/
}
```

Or use `overflow-wrap: break-word` or `white-space: pre-wrap` to break long lines in pre block, like URLs

`<wbr>` and `<br>` can be styled to disable it (ex: with class): `br{content: ""} br::before{content: " "}` (or `br{display: none}`). See also `br{content: ""} br::before{content: "\A\A\A"; white-space: pre}`

```css
@media(min-wdith: 500px){
	br{
		display: none;
	}
}
/* you can also use classes: <br class="br-smallscreen"> <br class="br-largescreen">*/
```

See also 

> _The Yahoo Style Guide_ recommends **breaking a URL _before_ punctuation**, to avoid leaving a punctuation mark at the end of the line, which the reader might mistake for the end of the URL.
— [\<wbr\> - HTML | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/wbr#Example)

- [Šime Vidas on Twitter: "😳 You can conditionally disable \<br\> line breaks via CSS media queries:… "](https://twitter.com/simevidas/status/1170834814259347456?s=12)
- [My takeaways from Florian Rivoal’s “Line breaking” talk# | Web Platform News](https://webplatform.news/issues/2019-04-01#my-takeaways-from-florian-rivoal-s-line-breaking-talk)
- [Injecting a Line Break | CSS-Tricks](https://css-tricks.com/injecting-line-break/)
- [Wrap at sibling's width](http://codepen.io/simurai/pen/evgVvm/) - Wrap text automatically at a sibling element's width
- [What is the difference between "word-break: break-all" versus "word-wrap: break-word" in CSS - Stack Overflow](https://stackoverflow.com/questions/1795109/what-is-the-difference-between-word-break-break-all-versus-word-wrap-break/15137272#15137272)
- [css - Using "word-wrap: break-word" within a table - Stack Overflow](https://stackoverflow.com/questions/5889508/using-word-wrap-break-word-within-a-table)
- [hyphens - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/hyphens#Suggesting_line_break_opportunities)
- [word-break - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/word-break)
- [More than anyone needs to know about word-break colon break-word.](https://miketaylr.com/posts/2014/01/word-break-break-word.html)
- [Hyphenation works! - QuirksBlog](http://www.quirksmode.org/blog/archives/2012/11/hyphenation_wor.html)
- [Word wrapping/hyphenation using CSS. — Kenneth Auchenberg](https://kenneth.io/blog/2012/03/04/word-wrapping-hypernation-using-css/)
- [Soft hyphen — Wikipedia](https://en.wikipedia.org/wiki/Soft_hyphen)
- [Issue 605840 - chromium - CSS hyphens property - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=605840)
- [overflow-wrap | CSS-Tricks](https://css-tricks.com/almanac/properties/o/overflow-wrap/)
- [Handling Long Words and URLs (Forcing Breaks, Hyphenation, Ellipsis, etc) | CSS-Tricks](https://css-tricks.com/snippets/css/prevent-long-urls-from-breaking-out-of-container/)

### Text edition, selection

`caret-color`, `::selection`

- [caret-color - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/caret-color)
- [::selection - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/::selection)
- [Coloring the insertion caret - Rego's Everyday Life](https://blogs.igalia.com/mrego/2017/01/09/coloring-the-insertion-caret/)

### Text fill, filters and clip

Aka knockout

Paragraph fadeout:

Use a mask:

```css
p {
	mask-image: linear-gradient(to top, transparent, black 2em);
}
```

or use background clip:

```css
p {
	background: linear-gradient(to top, transparent, black 2em, black);
	background-clip: text;
	color: transparent;
}
```

alternate version where `currentColor` can be used:

```css
p {
	/*color: red;*/
	background: linear-gradient(to top, transparent, currentColor 2em, currentColor);
	background-clip: text;
	-webkit-text-fill-color: transparent;
}
```

Letter spacing is supported for SVG text elements

```css
element {
	background: white;
	mix-blend-mode: screen;/*works only with black text over white bg*/
}
```

```css
element {
	background: black;
	color: white;
	mix-blend-mode: multiply;/*works only with white text over black bg*/
}
```

- [How to Create (Animated) Text Fills | Codrops](http://tympanus.net/codrops/2015/02/16/create-animated-text-fills/)
- [Applying SVG effects to HTML content - SVG | MDN](https://developer.mozilla.org/en-US/docs/Web/SVG/Applying_SVG_effects_to_HTML_content#Example_Filtering)
- [Clipping and Masking in CSS | CSS-Tricks](https://css-tricks.com/clipping-masking-css/)
- works only with plain colors [Knockout text with blending modes ✿ dabblet.com](http://dabblet.com/gist/ea2479217dcc469457b06d2aca7dbaf1), [Knockout text with pure CSS using blending modes](https://codepen.io/aertmann/pen/vKrKJx)
- [Using background clip for text with CSS fallback | Divya Manian](http://nimbupani.com/using-background-clip-for-text-with-css-fallback.html)

### Letter spacing from Photoshop

For CSS property `letter-spacing`. Use `em` unit

Photoshop space unit is 1/1000em

- [CSS letter-spacing in Photoshop and browsers | Justin Marsan](http://justinmarsan.com/css-letter-spacing-in-photoshop-and-browsers/)

### Text stroke, text border

```css
*{
	text-shadow:
	   -1px -1px 0 #000,  
		1px -1px 0 #000,
		-1px 1px 0 #000,
		 1px 1px 0 #000;
}
```

- [Adding Stroke to Web Text | CSS-Tricks](https://css-tricks.com/adding-stroke-to-web-text/)

### Font smooth

Aka `font-smooth`, font smoothing

> It seems silly to opt-out of a technically superior subpixel approach if supported on the user’s platform/browser

- [Laissez-faire Font Smoothing and Anti-aliasing—zachleat.com](https://www.zachleat.com/web/font-smooth/)

## Hide element

- [CSS Image Replacement](https://css-tricks.com/examples/ImageReplacement/)
- [Hiding DOM elements - ally.js](http://allyjs.io/tutorials/hiding-elements.html)
- [Image Replacement Techniques in the Modern Age](https://www.sitepoint.com/image-replacement-techniques-in-the-modern-age/)
- [css - display:none vs visibility:hidden vs text-indent:9999 How screen reader behave with each one? - Stack Overflow](https://stackoverflow.com/questions/1755656/displaynone-vs-visibilityhidden-vs-text-indent9999-how-screen-reader-behave-w)
- [Hidden text and links - Search Console Help](https://support.google.com/webmasters/answer/66353)

### Hide graphically a text

But still accessible (and selectable)

- [Hiding DOM elements - ally.js](https://allyjs.io/tutorials/hiding-elements.html#hiding-dom-elements)
- [WebAIM: CSS in Action - Invisible Content Just for Screen Reader Users](https://webaim.org/techniques/css/invisiblecontent/)

#### `padding-top`

Use `padding-top` to push down the content:

```css
*{
	display: block;/*or any other display mode where width is not defined by the content*/
	overflow: hidden;
	height: 0px;
	padding-top: 100px;
}
```

#### `text-indent`

```css
*{
	display: block;/*or any other display mode where width is not defined by the content*/
	text-indent: 9999px;
	overflow: hidden;
	white-space: nowrap;
}
```

Use `px` for `text-indent` with great value instead of `%` because percentages not work correctly every times (and don't require relative computations)

Some people don't recommand to use the `text-indent` techniques:

- [HTML “text-indent: -9999px” and holding the line | Maile Ohye: Love & Technology](http://maileohye.com/html-text-indent-not-messing-up-your-rankings/)
- [Disallow negative text indent · CSSLint/csslint Wiki](https://github.com/CSSLint/csslint/wiki/Disallow-negative-text-indent)
- [Replacing the -9999px hack (new image replacement) | Jeffrey Zeldman Presents The Daily Report: Web Design News & Insights Since 1995](http://www.zeldman.com/2012/03/01/replacing-the-9999px-hack-new-image-replacement/)

#### Text size or color

`font-size: 0;` or `color: transparent;` or `line-height: 0;` can also works, but have few drawbacks. Require `overflow: hidden;` (+ set height/width).

#### ARIA label

You can use [`aria-label` and/or `title` attributes](HTML#labelling) instead or with `aria-labelledby=ID`
It's accessible, but HTML is invalid when tag like `a`, `button`, `p`, `h1`, etc. are empty.

### Hide graphicaly an element

But still accessible (and selectable).

```css
/*
1. https://medium.com/@jessebeach/beware-smushed-off-screen-accessible-text-5952a4c2cbfe
*/
element:not(:active):not(:focus){
	/*Use !important to force higher specificity for possible overwrites*/
	position: absolute !important;
	width: 1px !important;
	height: 1px !important;
	clip: rect(1px, 1px, 1px, 1px) !important;
	clip-path: inset(100%) !important;
	overflow: hidden !important;
	white-space: nowrap !important;/* 1 */
	left: auto !important;
	top: auto !important;
	right: auto !important;
	bottom: auto !important;
	min-width: none !important;
	min-height: none !important;
	max-width: none !important;
	max-height: none !important;
	margin: 0 !important;
	border: 0 !important;
	padding: 0 !important;
	transform: none !important;
}
```

**Don't forget to display it when it's active**: http://littlebigdetails.com/post/110541390831/new-york-times-tabbing-reveals-accessibility
Don't use `visibility: hidden;` (http://accessibilitytips.com/2008/03/05/avoiding-visibility-hidden/) or `display: none;` because it hide content for all users. "line feeds are not interpreted as spaces". [Beware smushed off-screen accessible text – Medium](https://medium.com/@jessebeach/beware-smushed-off-screen-accessible-text-5952a4c2cbfe)
**Use `white-space: nowrap;`**, else the text will be read wrongly: "showmore", without spaces

- https://github.com/h5bp/html5-boilerplate/blob/dbc3ed973573a77122f6b8a2aebd0a76a44ad6a6/src/css/main.css#L130-L141
- [Hiding DOM elements - ally.js](https://allyjs.io/tutorials/hiding-elements.html#2017-edition-of-visuallyhidden)
- [Clip Your Hidden Content For Better Accessibility | tenydnblog - Yahoo](https://developer.yahoo.com/blogs/ydn/clip-hidden-content-better-accessibility-53456.html)
- [Text for Screen Readers Only (Updated) - Coolfields Consulting](http://www.coolfields.co.uk/2016/05/text-for-screen-readers-only-updated/)
- [Maintaining Accessibility in a Responsive World | Filament Group, Inc., Boston, MA](https://www.filamentgroup.com/lab/accessible-responsive.html)
- [Maintaining Accessibility in a Responsive World | CSS-Tricks](https://css-tricks.com/maintaining-accessibility-responsive-world/)
- [Beware smushed off-screen accessible text – J. Renée Beach – Medium](https://medium.com/@jessebeach/beware-smushed-off-screen-accessible-text-5952a4c2cbfe)
- [Cache-cache CSS – La vie en #ffoodd](http://www.ffoodd.fr/cache-cache-css/)
- [skiplinks not working correctly in iOS/Safari+VoiceOver and Android/Chrome+TalkBack · Issue #20732 · twbs/bootstrap](https://github.com/twbs/bootstrap/issues/20732)

### Hide an element to assistive technologies

Use `display: none` or `visibility: hidden` but will hide it graphicaly too.
Prefer using `aria-hidden="true"`, `role="presentation"` or `hidden` attributes. See [Hide an element](HTML#hide-an-element).
For images, set an empty `alt` attribute: `<img src="image.png" alt="">`
You can also use `content` CSS property. It will not be read.
Could not work if a role attribute is defined on the element.

`speak: none` is not a solution.

- [F87: Failure of Success Criterion 1.3.1 due to inserting non-decorative content by using :before and :after pseudo-elements and the 'content' property in CSS | Techniques for WCAG 2.0](http://www.w3.org/TR/WCAG20-TECHS/F87.html)
- [Testing the accessibility of the CSS generated content | cssgallery.info](http://cssgallery.info/testing-the-accessibility-of-the-css-generated-content/)
- [css - Can i prevent :after pseudo element from being read by screen readers? - Stack Overflow](https://stackoverflow.com/questions/26634156/can-i-prevent-after-pseudo-element-from-being-read-by-screen-readers/26634352#26634352)
- [html - Are ARIA roles inherited by descendants? - Stack Overflow](https://stackoverflow.com/questions/21699185/are-aria-roles-inherited-by-descendants)
- [HTML5 Accessibility: aria-hidden and role=”presentation” | Unrepentant](http://john.foliot.ca/aria-hidden/)
- [html - Is the css setting speak:none now equivalent to aria-hidden="true"? - Stack Overflow](https://stackoverflow.com/questions/27751738/is-the-css-setting-speaknone-now-equivalent-to-aria-hidden-true)
- [Improved .sr-only](https://gist.github.com/ffoodd/000b59f431e3e64e4ce1a24d5bb36034)
- [Cache-cache CSS – La vie en #ffoodd](http://www.ffoodd.fr/cache-cache-css/)

### Hide replaced element

Replaced element: iframe, object, embed

Use `visibility: hidden; position: fixed;` instead of `display: none`. Else document inside these tags don't have any dimensions (null viewport: `window.innerHeight == 0`) and styles are not computed (`window.getComputedStyle()` return null)

- [Javascript problem with iframe that's hidden before loaded - Stack Overflow](https://stackoverflow.com/questions/2730046/javascript-problem-with-iframe-thats-hidden-before-loaded/2786429#2786429)
- [548397 - window.getComputedStyle() returns null inside an iframe with display: none](https://bugzilla.mozilla.org/show_bug.cgi?id=548397)
- [91232 - iFrame Flash Video CSS display:none; - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=91232)
- [Bug Report: Hidden iframes don't work](https://www.quirksmode.org/bugreports/archives/2005/02/hidden_iframes.html)

## Image

See [Performance impact of images](HTML#performance-impact-of-images)
See [Content vs. decorative image](HTML#content-vs-decorative-image)

### Broken image

Use pseudo elements (works only when the image is broken): [Styling Broken Images](https://bitsofco.de/styling-broken-images/)

Or override the image src with CSS (don't do that, see above):

```css
*{
	content: url("data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==") / "";
}
```

[This syntax](https://www.w3.org/TR/css-content-3/#alt) is not widly supported. (15/09/2016: it's still an Editor's Draft). If not supported (or removed from spec), don't use it because **(if not empty) you should always let the alt text be displayed**. (or use `... / attr(alt)`)

Or use Shadow DOM selector (not work currently): [Border Around ALT Text in Email Signature > Litmus](https://litmus.com/community/code/4309-border-around-alt-text-in-email-signature)

### Content generated image

```css
*{
	content: url(image1.jpg) url(image2.jpg);
}
```

> content generated image is like `<img>` inside an anonymous `<span>`

That means you can't resize it or use srcset

- [Replace the Image in an \<img\> with CSS | CSS-Tricks](https://css-tricks.com/replace-the-image-in-an-img-with-css/)
- `content: url()` not work everywhere

### Compression

See [reduce bytes](Web#reduce-bytes)

### Sprites vs Data URI

Data URI should be used to inline image < 4KB

**Note: Don't base64 your SVGs.**

Sprites aka texture atlas or tiles.

- reduce HTTP requests
- Base64-encoded data URIs are 1/3 larger in size than their binary equivalent
- don't require mutliple subdomain servers to skip browser's max connection per domain
- Data URI are less efficient when SPDY used (vs separate images)
- require a specific tool / workflow to create sprites. Can be done easly manually for Data URI
- Sprite can't mix compression methods/formats: lossless or lossy, DCT(JPEG), paletted, transparency. JPEG vs PNG (vs WebP)
- (require more investigations) Drawing performance impact:
	* https://gist.github.com/KrofDrakula/3639830
	* https://stackoverflow.com/questions/831189/css-sprites-browser-rendering
	* scale with `background-size`
	* [Web # Data URI](#data-uri)
	* [CSS Sprites vs. Data URIs: Which is Faster on Mobile?](http://www.mobify.com/blog/css-sprites-vs-data-uris-which-is-faster-on-mobile/)
	* [Bryan McQuade at ChromeDevSummit 2013: data:uris in CSS is considered a render-blocking anti-pattern for delivering critical/minimal CSS](https://docs.google.com/presentation/d/1z49qp03iXAJIkbXaMtCmWW_Pnnq-MzXGW139Xw8-paM/edit#slide=id.g174590d5d_0194)
	* [On Mobile, Data URIs are 6x Slower than Source Linking (New Research) | Mobify](http://www.mobify.com/blog/data-uris-are-slow-on-mobile/)
	* [Data URI Performance: Don't Blame it on Base64 | Mobify](http://www.mobify.com/blog/base64-does-not-impact-data-uri-performance/)
	* accessibility concerns (embedded/data URI are always available with its CSS, where external file(s) couldn't, due to network or server issue)
	* http://buildnewgames.com/dom-sprites/
	* http://jsperf.com/sprite-sheet-speed-benefits
	* same memory footprint (not exactly: less footprint only one file header vs for each), but less texture/image loads
	* http://en.wikipedia.org/wiki/Texture_atlas
	* https://github.com/operasoftware/TextureAtlas
	* http://www.altdevblogaday.com/2012/09/17/building-an-html5-game-dont-shrug-off-atlases/
- embedded image usage is adviced by W3C: [Mobile Web Application Best Practices](https://www.w3.org/TR/mwabp/#bp-conserve-css-images)
- Sprite can't always be used correctly: can't be repeated easly and can't use `background-size` `cover`/`contain` or percentages
- Sprite require [bleed](http://en.wikipedia.org/wiki/Bleed_%28printing%29) or margin
	https://stackoverflow.com/questions/646901/do-i-still-need-to-pad-images-in-a-css-sprite
	https://code.google.com/p/forplay/issues/detail?id=44
	http://gamedev.stackexchange.com/questions/46963/how-to-avoid-texture-bleeding-in-a-texture-atlas
	https://stackoverflow.com/questions/13271205/threejs-custom-shader-screen-tearing/
- Data URIs are not separately cached from their containing documents (e.g. CSS or HTML files) so data is downloaded every time the containing documents are redownloaded.
- Both must be re-encoded and re-embedded every time a change is made.
- Data URI not work everywhere, can have maximum length support (of 32 KB IE8)
- Data URI (maybe sprites too) is included as a simple stream, and many processing environments (such as web browsers) may not support using containers (such as multipart/alternative or message/rfc822) to provide greater complexity such as metadata, data compression, or content negotiation.
- If served in a gzipped resource, CSS with data URIs images are almost certainly going to be a terrible strain on the server's resources! Images are traditionally very CPU intensive to compress, with very little reduction in size. Better if you pregzip the CSS after each update
- Data URIs make it more difficult for security software to filter content

More infos:

- See [Web#Data URI]()
- [Better CSS Sprites with SVG](http://w3.eleqtriq.com/2012/01/enhancing-css-sprites-and-background-image-with-svg/)
- http://coding.smashingmagazine.com/2010/03/26/css-sprites-useful-technique-or-potential-nuisance/

### SVG Stacks (fragment identifiers)

See [Fragment identifier and SVG stack](SVG#fragment-identifier-and-svg-stack)

`icons.svg#plus`

```html
<svg>
	<style>
	.icon{display: none;}
	.icon:target{display: inline;}
	</style>
	<g id="plus" class="icon"></g>
	<g id="chart" class="icon"></g>
</svg>
```css

> Works currently only for img, iframe, embed, object in Firefox, Opera, IE9, Chrome, Safari

- http://simurai.com/post/20251013889/svg-stacks
- http://jsfiddle.net/24DNn/5/
- https://github.com/preciousforever/SVG-Stacker
- [SVG `symbol` a Good Choice for Icons | CSS-Tricks](https://css-tricks.com/svg-symbol-good-choice-icons/)

### Icon font vs SVG icon

Icon font, inline SVG or background SVG

Prefer using SVG. Font it's realy hard to get a consitent (pixel) align correctly across browsers

> - each platform handles fonts varies a lot
> - icon-fonts have a smaller footprint
> - Opera mini doesn't support custom fonts
> - icon fonts fail a lot; especially on slow connections
> - users can disable fonts & therefore won't get them
> - icon fonts are limited in styling and animations
> - icon fonts they have zero semantics
> - adblockers sometimes block icon fonts

> 1. Vector! - Typically sharper than icon fonts because of non-text anti-aliasing
> 2. Easy multu-color! - More CSS control than any other method.
> 3. Animate! - Easy to apply transitions and animations
> 4. Script away! - Everything is in the DOM.
> 5. Better accessibility! Plus fallbacks! - Fool-proof, once you set it up well
> 6. Better semantics! - `<svg>` = "image" / `<span>` = "nothing"
> 7. Ease of use - Easy to manage individual icons, instant build processes.
> — Sarah Drasner, Chris Coyier, Seren Davies

> icon fonts do not use progressive enhancement by default
— [Performance Calendar » No @font-face Syntax will ever be Bulletproof, Nor Should It Be](http://calendar.perfplanet.com/2016/no-font-face-bulletproof-syntax/#addendum_okay_but_what_about_icon_fonts)

- [Ten reasons we switched from an icon font to SVG - Ian Feather](http://ianfeather.co.uk/ten-reasons-we-switched-from-an-icon-font-to-svg/)
- [» Seriously, Don’t Use Icon Fonts Cloud Four Blog](http://blog.cloudfour.com/seriously-dont-use-icon-fonts/)
- [Github changes to icon SVG from fonts, for no clear reason - Pomax.github.io](https://pomax.github.io/1456332505750/github-changes-to-icon-svg-from-fonts-for-no-clear-reason)
- [Delivering Octicons with SVG](https://github.com/blog/2112-delivering-octicons-with-svg)
- [css - SVG as icon font alternative - Stack Overflow](https://stackoverflow.com/questions/30820787/svg-as-icon-font-alternative)
- [Bulletproof Accessible Icon Fonts | Filament Group, Inc., Boston, MA](https://www.filamentgroup.com/lab/bulletproof_icon_fonts.html)
- (not sure Custom Elements is the best solution, but explain others solutions) [The Road to SVG and Custom Elements in Clarity Icons – Clarity Design System – Medium](https://medium.com/claritydesignsystem/the-road-to-svg-and-custom-elements-in-clarity-icons-1d691c6cc91#.2anohjioj)
- [Making the Switch Away from Icon Fonts to SVG: Converting Font Icons to SVG — Sara Soueidan – Freelance-Front-End UI/UX Developer](https://www.sarasoueidan.com/blog/icon-fonts-to-svg/)
- [How I learnt to stop using icon fonts (and love SVG) – Triggers & Sparks](https://triggersandsparks.com/talks/svg-icons/)

Align SVG icon with text:

- [Align SVG Icons to Text and Say Goodbye to Font Icons](https://medium.com/@Elliotdahl/align-svg-icons-to-text-and-say-goodbye-to-font-icons-d44b3d7b26b4)

### SVG auto scale

To force the SVG to auto scale (not using default sizes)

Set `width: 100%` on `img` or `object` or `embed` (for IE)

### Preload img with CSS

See [Preload and prefetch](Web#preload-and-prefetch)

```css
body::after {
	content: url(img01.jpg) url(img02.jpg) url(img03.jpg);
	display: none;
}
```

## Animation & transition

Use `transform` instead of `top`/`left`/`bottom`/`right` for better performances. See [relayout, repaint, reflow](#relayout-repaint-reflow).

Transition or animation on some devices (tablet or smartphone) are not perfectly synchronized, when lot of differents animated elements.

For complexe layout with text and/or `em` or `rem`, it's could be usefull to animate `font-size`. But it's trigger layout.

`animation-play-state` stop animation, but after next keyframe

To replay an animation, you need to reflow animated elements. Ex.: (just) `element.offsetWidth;`

Note: Declarations in a keyframe that are qualified with `!important` are ignored

- http://css-tricks.com/restart-css-animation/
- https://stackoverflow.com/questions/6268508/restart-animation-in-css3-any-better-way-than-removing-the-element

- [Animatable: One property, two values, endless possibilities](http://leaverou.github.io/animatable/)
- [Myth Busting: CSS Animations vs. JavaScript | CSS-Tricks](https://css-tricks.com/myth-busting-css-animations-vs-javascript/)
- [The ultimate guide to Web animation | Webdesigner Depot](http://www.webdesignerdepot.com/2015/05/the-ultimate-guide-to-web-animation/)
- [Keyframes generator](https://github.com/wholcman/css-animation-on-fly)
- ["will-change" must change? Animators beware. | GreenSock](https://greensock.com/will-change)

For accessibility, disable animations / transitions with:

```css
/* Can break scripts using events like animationend, transitionstart, etc. */
@media (prefers-reduced-motion: reduce){
	* {
		animation-duration: 0;
		animation-delay: 0;
		transition-duration: 0;
		transition-delay: 0;
	}
}
```

`auto` for `width` and `height` is not animatable (computed value):

- [Building performant expand & collapse animations | Web | Google Developers](https://developers.google.com/web/updates/2017/03/performant-expand-and-collapse) - Expand/collapse, accordion transition use scale transform + it inverse
- [Using CSS Transitions on Auto Dimensions | CSS-Tricks](https://css-tricks.com/using-css-transitions-auto-dimensions/)
- [CSS transition from/to auto values](http://n12v.com/css-transition-to-from-auto/)
- [\[css-transitions\] Transition to height (or width) "auto" · Issue #626 · w3c/csswg-drafts](https://github.com/w3c/csswg-drafts/issues/626)
- `element.style.height = window.getComputedStyle(element, null).height` explicitly define the dimension before animate (need adjusted when parent and children are reflowed)
- [Spring physics with CSS variables](https://codepen.io/valhead/pen/yXYYdm)
- [Codevember 11 #bike gsap svg stroke animation](https://codepen.io/alaricweb/pen/vWxPyp)

### Content

```css
body::before {
	animation: counter 10s infinite;
}
@keyframes counter {
	0%  { content: "1/10" }
	10% { content: "2/10" }
	20% { content: "3/10" }
	30% { content: "4/10" }
	40% { content: "5/10" }
	50% { content: "6/10" }
	60% { content: "7/10" }
	70% { content: "8/10" }
	80% { content: "9/10" }
	90% { content: "10/10" }
}
```

- [Animating the `content` Property | CSS-Tricks](https://css-tricks.com/animating-the-content-property/)

### Visibility

Use `visibility: hidden|visible` to hide completely or show an element (click events are not handled). This property is animable. Use the smalled duration `0s` (or `1ms` if not work) and delay.

https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animated_properties

### Sprite animation

```css
.animable {
	width: 50px;
	height: 50px;
	background-image: url("sprites.png");
	animation: play .8s steps(10) infinite;
}

@keyframes play {
   from { background-position:	0px; }
	 to { background-position: -500px; }
}
```

http://simurai.com/blog/2012/12/03/step-animation/

`Fichier > Scripts > Chargement des fichiers dans une pile...`

### Delay between animation repeat

Add "no change" keyframes:

```css
@keyframes{
	0%{
		top: 0;
	}
	50%{
		top: 20px;
	}
	100%{
		/* same value of the previous keyframe */
		top: 20px;
	}
}
```

### Underline animation

```css
a {
	text-decoration: none;
	background-image: linear-gradient(currentColor, currentColor);
	background-position: 0% 100%;
	background-repeat: no-repeat;
	background-size: 0% 4px;/* underline equivalent, but animatable */
	transition: background-size cubic-bezier(0,.5,0,1) 0.3s;
}

a:hover,
a:focus {
	text-decoration: none;
	background-size: 100% 4px;
}
```

- [Animated Multiline Link Underlines with CSS](https://www.dannyguo.com/blog/animated-multiline-link-underlines-with-css/)

### Roll over and out different animations

Use transition to restore the initial state and animation for hover.
If you want to use animation for both state transitions and don't want initial animation, you need to use animations it in conjunction with opacity/visibility animation/transition (but required initially hidden) on element or its parent

```html
<style>
	@keyframes roll{
		from {
			stroke-dashoffset: -100px;
		}
		to {
			stroke-dashoffset: 0px;
		}
	}
	.element{
	 	stroke-dasharray: 100px 100px;
		stroke-dashoffset: 100px;
		transition: stroke-dashoffset 1s;
		stroke: red;
		stroke-width: 20px;
	}
	html:hover .element{
		stroke-dashoffset: 0px;
		animation: roll 1s;
		transition: none 0;
	}
</style>
<svg>
	<path class="element" d="M0,0l100,0"/>
</svg>
```

Note: Firefox could require to replace `transition: none 0;` by `transition: none;` to work proprely

If roll over and roll out are both animations, an different `animation-name` is required

### Direction aware hover effect

- [Direction aware hover effect](https://codepen.io/electerious/full/xeJPbB)

### Fading out siblings on hover

- [Fading out siblings on hover in CSS | Trys Mudford](https://www.trysmudford.com/blog/fade-out-siblings-css-trick/)

### Don't define last frame value

That let browsers don't support or ignore animations (like IE9) to "jump to the end" of animation.

```css
@keyframe fade{
	from {
		left: 0;
	}
	/* to { left: 100px; } */
	/* skip "to"/"100%" keyframe, will compute final values of current style (without animation) */
}
.element{
	left: 100px;/* this will be used to compute empty last frames "to"/"100%" */
	animation: fade 1s;
}
```

It's not required for animation where the final value is the default value, like: `opacity: 0 → 1` or `visibility: hidden → visible`, `padding: 10px → 0px`, etc.

But prefer transition for simple animation (like normal for rollin then reverse for rollout)

### Animation fill mode declaration for `none` animation is ignored

```css
selector{
	animation: none 1s 10s backwards;
}
selector{
	animation-name: animname;
}
```

Will not work as expected. Because it's parsed as `animation-fill-mode: none; animation-duration: 1s; animation-delay: 10s; animation-name: backwards;`.
All words can be used as valid keywords are used to define properties other than `animation-name`.
To correct that use `animation: 1s 10s backwards;` instead.

See http://dev.w3.org/csswg/css-animations/#typedef-single-animation

### Animated blur

Update blur filter

For performance, clone the element with different stages of blurness (wrapped)

- [Animating a Blur | Web | Google Developers](https://developers.google.com/web/updates/2017/10/animated-blur)

- [Motion Blur Experiment](http://codepen.io/lbebber/pen/zxpMZw)

### Trigger JS event from CSS

use dummy animations to tigger `animationend` events in javascript

```css
/* Dummy animation with specific name, allow module CSS to change intro/outro duration */
@keyframes module-intro {from{visibility: visible}to{visibility: visible}}
@keyframes module-outro {from{visibility: visible}to{visibility: visible}}

.module--active{
	animation: module-intro 1s;
}
```

```html
module.addEventListener("animationend", function(event){
	if(event.animationName == "module-intro"){
		//
	}
})
```

dummy animation need keyframes (WebKit) with animatable property (IE)

### Animate gradient

Make a gradient larger than content-box (via `background-size`) and apply transition or animation on it (with `background-position`).

- http://codepen.io/jensgro/full/yhEGH

### Delay ignored

TODO test it

```css
selector{
	transition: opacity 0s 10s;
}
selector{
	transition-duration: 2s;
}
```

## Stripes animation

Aka barberpole

- [Barberpole Hover Animation](https://codepen.io/chriscoyier/pen/AzdcK)

## Selectors

Unsuall selector: `.foo:not(:hover) > .bar:hover` ("The parent of an element that is `:hover` is also in that state." — [CSS Selector Level 4](https://www.w3.org/TR/selectors4/#the-hover-pseudo)) only works for input's label hover or when forcing a hover style on .bar through the DevTools/inspector

See [JavaScript selectors](HTML#javascript-selectors)

- [CSS4-Selectors | All selectors from CSS4 to CSS1](https://css4-selectors.com/selectors/)
- [Splicing HTML’s DNA With CSS Attribute Selectors — Smashing Magazine](https://www.smashingmagazine.com/2018/10/attribute-selectors-splicing-html-dna-css/)
- [Label-to-Input States](http://kizu.ru/en/blog/label-to-input/)
- [Roma Komarov on Twitter: "CSS quiz! Are there cases when this selector would make sense —`.foo:not(:hover) \> .bar:hover` ?"](https://twitter.com/kizmarh/status/869534275976167424)

### Invalid selector

```css
*,
*::nope {
	background: red;
	/* nothing will have a red background, because ::nope is an invalid (pseudo-)selector that invalidate the whole ruleset (but there is some exceptions) */
}
```

- [One Invalid Pseudo Selector Equals an Entire Ignored Selector | CSS-Tricks](https://css-tricks.com/one-invalid-pseudo-selector-equals-an-entire-ignored-selector/)

### Case sensitivity

> When matching against a document which is in quirks mode, class names must be matched ASCII case-insensitively; class selectors are otherwise case-sensitive.
– [Selectors Level 4 — 6.6. Class selectors](https://drafts.csswg.org/selectors-4/#class-html) and [Selectors Level 4 — 6.7. ID selectors](https://drafts.csswg.org/selectors-4/#id-selector)

> By default case-sensitivity of attribute names and values in selectors depends on the document language
— [Selectors Level 4 — 6.3. Case-sensitivity](https://drafts.csswg.org/selectors-4/#attribute-case)

- [Selectors Level 4 — 3.7. Characters and case sensitivity](https://drafts.csswg.org/selectors-4/#case-sensitive)
- [Can I use camel-case in CSS class names - Stack Overflow](https://stackoverflow.com/questions/1547986/can-i-use-camel-case-in-css-class-names)
- [cross browser - Are CSS selectors case-sensitive? - Stack Overflow](https://stackoverflow.com/questions/7559205/are-css-selectors-case-sensitive)

### `@supports` for selectors

```css
element:-x-not-supported-dummy-selector(), selector {
	/* rules applied only if ":-x-not-supported-dummy-selector()" is supported */
}
```

- [@supports for selectors by Taylor Hunt on CodePen](https://codepen.io/tigt/post/supports-for-selectors)

See [Progressive Enhancement](#progressive-enhancement)

### Classname

See [HTML Classname](HTML#classname)

### Selector specificity

> Never use !important to get yourself out of a problem.
— Harry Roberts aka @csswizardry

Note: `!important` can take the precedence, but for some CSS engines animation/transition can take percedence over `!important`. See [More important than !important – The Sea of Ideas](https://paulbakaus.com/2017/07/27/more-important-than-important/)

`element:not(#id)`, have higher specificity than `element` (because `#id` = 10)

- [Specificity Visualizer](https://isellsoap.github.io/specificity-visualizer/)
- [More important than !important – The Sea of Ideas](https://paulbakaus.com/2017/07/27/more-important-than-important/)
- [KISS principle - Wikipedia, the free encyclopedia](http://en.wikipedia.org/wiki/KISS_principle)
- [Strategies for Keeping CSS Specificity Low | CSS-Tricks](http://css-tricks.com/strategies-keeping-css-specificity-low/)
- [Controlling the Specificity](http://kizu.ru/en/fun/controlling-the-specificity/)
- [CSS specificity graphs | Blog | Decade City](https://decadecity.net/blog/2014/11/26/css-specificity-graphs)
- [Assigning property values, Cascading, and Inheritance](https://www.w3.org/TR/CSS2/cascade.html#specificity)
- [CSS Specificity](http://cssspecificity.com/)
- [Specificity - CSS | MDN](https://developer.mozilla.org/en/docs/Web/CSS/Specificity)
- [Specificity Calculator](https://specificity.keegan.st/)
- [Batificity](http://batificity.com/)
- [Specifishity :: Specificity with Fish](https://specifishity.com/)
- [CSS Specificity Wars | Stuff & Nonsense blog](https://stuffandnonsense.co.uk/archives/css_specificity_wars.html) - [css-specificity-wars.png](https://stuffandnonsense.co.uk/archives/images/css-specificity-wars.png)

### Selector based on language

	html:lang(fr) blockquote {
		/* you can use html[lang=fr] for compatibility */
		quotes: "«\00A0" "\00A0»";
	}

	a[hreflang|="en"]::after {
		content: "\0000a0" url(/flag-uk.png);
	}

- http://sergeylukin.com/2013/styling-html-elements-based-on-locale/

### Range selector

`:nth-child( [cycle size] n + [offset] )`

`:first-child` == `:nth-child(1)`
`:last-child` == `:nth-last-child(1)`

`:nth-child(odd)` == `:nth-child(2n+1)`
`:nth-child(even)` == `:nth-child(2n+2)` or `:nth-child(2n+0)`

`:not(:last-child)` == `:nth-last-child(n+2)`
`:not(:first-child)` == `:nth-child(n+2)`
`:nth-last-child(n+3)`

- [CSS Mod Queries and Range Selectors](http://www.modqueries.com/)
- [Mastering the :nth-child | CSS3 pseudo classes and :nth-child ranges](http://nthmaster.com/)
- [QQ - Quantity Queries Builder](http://quantityqueries.com/)
- [Useful :nth-child Recipes | CSS-Tricks](https://css-tricks.com/useful-nth-child-recipies/)
- [:nth-child - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-child)
- [NTH-TEST | nth-child and nth-of-type Tester](http://nth-test.com/)
- https://github.com/pascalduez/postcss-quantity-queries
- [Quantity Queries pour CSS](https://la-cascade.io/quantity-queries-pour-css/)
- [Abusing CSS3's nth-child selector to invent new ones | grack](http://grack.com/blog/2015/01/09/abusing-css3-selectors/)
- [Using CSS Mod Queries with Range Selectors · An A List Apart Article](http://alistapart.com/article/using-css-mod-queries-with-range-selectors)
- [:nth-child - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-child)
- [How CSS pseudo-classes work, explained with code and lots of diagrams](https://medium.freecodecamp.com/explained-css-pseudo-classes-cef3c3177361)
- [Some Extremely Handy `:nth-child` Recipes as Sass Mixins | CSS-Tricks](https://css-tricks.com/extremely-handy-nth-child-recipes-sass-mixins/)

### Link to a specific website

	[href*="://itunes.apple.com/"]{
	}
	[href*="://twitter.com/"]{
	}
	[href*="://plus.google.com/"]{
	}
	[href*="://www.facebook.com/"]{
	}
	[href*="://www.linkedin.com/"]{
	}

Note: To support protocol relative links, use `[href*="//itunes.apple.com/"]` instead. But it's not adviced to use it (protocol relative links, use always HTTPS when it's possible).

### Efficient selectors

- http://csswizardry.com/2011/09/writing-efficient-css-selectors/

### Non generic selectors

	.project h2:not([class]){
		/* apply only to element without class attribute */
	}

### `::first-letter` works only on block elements

- http://www.w3.org/wiki/CSS3/Selectors/pseudo-elements/:first-letter
- http://www.w3.org/TR/css3-selectors/#first-letter

### Visited limitations

`:visited` can only use color properties. Inherit `currentColor` can be used.

Only color can be used

- [Privacy and the :visited selector - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Privacy_and_the_:visited_selector)
- [Color `currentColor` keyword](#color-currentcolor-keyword)

### CSS Engine selectors

**Depreciated**

http://wayback.archive.org/web/20070721083320/http://tanreisoftware.com/blog/?p=39

Use `@support` if it's supported, or use a JS lib like modernizr

### Use right selectors to be accessible compilant

`button[disabled].btn` instead of `.btn--disabled` ?

- [How Our CSS Framework Helps Enforce Accessibility | eBay Tech Blog](http://www.ebaytechblog.com/2015/11/04/how-our-css-framework-helps-enforce-accessibility/)

## Form fields

Don't hide `input[type=file]`, it support natively drag and drop. Just use opacity (maybe non-zero)

Resizable textarea: `resize: vertical;` https://developer.mozilla.org/en-US/docs/Web/CSS/resize

- [Designing with Pseudo Elements in IE10 | Jonathan Sampson](http://sampsonblog.com/615/ie10s-pseudo-elements)
- [Creative Form & Input Field Design Examples — Medium](https://medium.com/@saijogeorge/creative-form-input-field-design-examples-bfe5dd50808a)
- [WTF, forms?](http://wtfforms.com/) https://github.com/mdo/wtf-forms
- [CSS3 Checkbox Styles](https://codepen.io/bbodine1/pen/novBm)
- [A Closer Look At The Select Element](http://wayback.archive.org/web/20150913113152/http://www.hanseri.no/a-closer-look-at-the-select-element/) Hybrid (only the selector) or native or fully custom (but not a `<select>`, only for few elements, < 6)
- [List of Pseudo-Elements to Style Form Controls - TJ VanToll - Tutorials, Thoughts, and Ramblings on Front-End Development](http://tjvantoll.com/2013/04/15/list-of-pseudo-elements-to-style-form-controls/)
- [iOS 6 switch style checkboxes with pure CSS | Lea Verou](http://lea.verou.me/2013/03/ios-6-switch-style-checkboxes-with-pure-css/)
- [When to Override Native UI Components - Articles - Baymard Institute](http://baymard.com/blog/custom-vs-native-ui)
- [CSS Contact Form | CodyHouse](http://codyhouse.co/gem/css-contact-form)
- [Stuff you can do with the "Checkbox Hack" | CSS-Tricks](https://css-tricks.com/the-checkbox-hack/)
- [Styling and scripting sliders - QuirksBlog](http://www.quirksmode.org/blog/archives/2015/11/styling_and_scr.html)
- [Advanced styling for HTML forms - Web developer guides | MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/Advanced_styling_for_HTML_forms)
- [Form Validation UX in HTML and CSS | CSS-Tricks](https://css-tricks.com/form-validation-ux-html-css/)
- [Under-Engineered Custom Radio Buttons and Checkboxen | Adrian Roselli](http://adrianroselli.com/2017/05/under-engineered-custom-radio-buttons-and-checkboxen.html)
- [Customize Radio Buttons without Compromising Accessibility](https://blog.bitsrc.io/customise-radio-buttons-without-compromising-accessibility-b03061b5ba93)

Examples:

- [my sliders \[MOST DEMOS ARE NOW BROKEN\] - a Collection by Ana Tudor on CodePen](http://codepen.io/collection/DgYaMj/) - Range input designs
- [JS Bin - Collaborative JavaScript Debugging](http://jsbin.com/juvixufu/10/edit?html,css,js,output)
- [Text Input Effects | Set 1](https://tympanus.net/Development/TextInputEffects/index.html)
- [Inspiration for Custom Select Elements | Demo 1](https://tympanus.net/Development/SelectInspiration/index.html)
- https://css-tricks.com/html5-meter-element/
- http://www.hongkiat.com/blog/html5-progress-bar/
- https://css-tricks.com/html5-progress-element/
- https://css-tricks.com/styling-cross-browser-compatible-range-inputs-css/
- http://codepen.io/collection/DgYaMj/8/
- https://css-tricks.com/webkit-html5-search-inputs/
- https://css-tricks.com/numeric-inputs-a-comparison-of-browser-defaults/
- https://css-tricks.com/snippets/css/turn-off-number-input-spinners/
- https://css-tricks.com/snippets/css/custom-file-input-styling-webkitblink/
- http://qnimate.com/guide-to-styling-html5-input-elements/
- https://davidwalsh.name/style-textarea-resizer
- http://advprog.blogspot.com/2013/07/styling-html-media-inner-workings.html
- https://css-tricks.com/custom-controls-in-html5-video-full-screen/
- http://tylergaw.com/articles/fun-with-html-form-validation-styles
- http://webdesign.tutsplus.com/tutorials/bring-your-forms-up-to-date-with-css3-and-html5-validation--webdesign-4738
- http://thereforei.am/2011/07/01/css-selectors-for-html5-input-validation/
- [Cross Browser Styling of HTML5 Forms — Even In Older Browsers.](http://www.useragentman.com/blog/2012/05/17/cross-browser-styling-of-html5-forms-even-in-older-browsers/)

Accessibility:

- [Short note on the accessibility of styled form controls | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](https://developer.paciellogroup.com/blog/2018/07/short-note-on-the-accessibility-of-styled-form-controls/)
- [The Accessibility of Styled Form Controls & Friends | a11y_styled_form_controls](https://scottaohara.github.io/a11y_styled_form_controls/)

Other:

- [Lightning Design System](https://www.lightningdesignsystem.com/components/datepickers/)
- [CSS Form Styling Module Level 1](https://drafts.csswg.org/css-forms/)
- [\[css-forms\]\[css-ui\] Styling native components, a proposal from Lea Verou on 2016-03-22 (www-style@w3.org from March 2016)](https://lists.w3.org/Archives/Public/www-style/2016Mar/0310.html)

### Invalid state only after user interaction

[`:user-invalid`](https://drafts.csswg.org/selectors/#user-error-pseudo) or [`:user-error`](https://www.w3.org/TR/selectors4/#user-error-pseudo)

`If (input not empty or form sumibited or input value has changed) and input invalid` (Firefox model)
or
`If (form sumibited or input blur) and input invalid` (W3C CSS Selector 4)

- [Pseudo-class `:user-error`](http://www.w3.org/TR/selectors4/#user-pseudos)
- https://developer.mozilla.org/en-US/docs/Web/CSS/:-moz-ui-invalid
- [Improving HTML5 Forms' user experience with :-moz-ui-invalid and :-moz-ui-valid pseudo-classes - Mounir Lamouri's Blog](http://mounir.lamouri.fr/2011/05/improving-html5-forms-user-experience-with-moz-ui-invalid-and-moz-ui-valid-pseudo-classes.html)
- About `:invalid` W3C thread:
	* https://lists.w3.org/Archives/Public/public-whatwg-archive/2010Sep/thread.html#msg416
	* https://lists.w3.org/Archives/Public/public-whatwg-archive/2010Dec/thread.html#msg302
	* https://lists.w3.org/Archives/Public/public-whatwg-archive/2011Jan/thread.html#msg28
- [L'API HTML5 de contrainte de validation](http://dmouronval.developpez.com/tutoriels/javascript/api-contrainte-validation/)

### Labels and placeholders

See [User Interface and experience/Floating label]()

Never use placeholder as a label! [Remi Grumeau on Twitter: http://t.co/OJ9yUo3dN9](https://twitter.com/remi_grumeau/status/573410750674423808/photo/1) (the placeholder is truncated inside the input where the label is not)

### Select element

Aka `<select>`

	/* IE hide select arrow IE10+ */
	select::-ms-expand{
		display: none;
	}

- [Select styles with CSS only](https://github.com/filamentgroup/select-css)
- [::-ms-expand pseudo-element - Windows app development](https://msdn.microsoft.com/en-us/library/windows/apps/hh465742.aspx)

###  Range

`input[type=range]`

- [my sliders - a Collection by Ana Tudor on CodePen](http://codepen.io/collection/DgYaMj/)
- http://www.hongkiat.com/blog/html5-range-slider-style/
- http://css-tricks.com/styling-cross-browser-compatible-range-inputs-css/

### Empty input

`input:empty` (or non standard `input:blank`) match if there is any child, etc.
`input:invalid` not work for non-required fields
`input[value=""]` not work when the value is changed. Because it match the attribute not the property, and the attribute doesn't reflect property.
`::value` not work, selector pseudo element value

Proposition: `:empty-value`, `:filled`

Actually require JS:

- https://lists.w3.org/Archives/Public/www-style/2011Apr/thread.html#msg603
- https://lists.w3.org/Archives/Public/www-style/2012Mar/thread.html#msg269
- https://lists.w3.org/Archives/Public/www-style/2011May/thread.html#msg12

### Resizable textareas

	resize: vertical;
	resize: none;

### File input

- [Styling & Customizing File Inputs the Smart Way | Codrops](http://tympanus.net/codrops/2015/09/15/styling-customizing-file-inputs-smart-way/) and [Custom File Inputs | Codrops](http://tympanus.net/Tutorials/CustomFileInputs/)

### Checkbox

`input[type=checkbox]`

Don't forget to style `input[type=checkbox]:indeterminate`

- http://cssdeck.com/labs/css-checkbox-styles
- [Quick Tip: Easy CSS3 Checkboxes and Radio Buttons - Envato Tuts+ Web Design Article](http://webdesign.tutsplus.com/articles/quick-tip-easy-css3-checkboxes-and-radio-buttons--webdesign-8953)

## Performance

Chrome is better to animate (or make a transition using transform) a large container of tile vs Firefox is better to animate each tile independantly

**It's a hack and maybe not work in the future!** Force layer creation using `translate3d()` instead of `translate()` or use `transform: translateZ(0)`. Maybe usefull to use in conjunction with `backface-visibility: hidden;`

- CSS3 Gradients vs Image Gradients:
	- [CSS gradients are faster than SVG backgrounds | Lea Verou](http://lea.verou.me/2011/08/css-gradients-are-much-faster-than-svg/)
	- [CSS linear gradient that kills firefox's performance :'(](https://gist.github.com/foca/3888302)
	- [How does the performance of using background-gradients in CSS vs using images? - Stack Overflow](https://stackoverflow.com/questions/5793586/how-does-the-performance-of-using-background-gradients-in-css-vs-using-images)
	- [Runtime Performance with CSS3 vs Images | Jacob Wright](http://jacwright.com/476/runtime-performance-with-css3-vs-images/)
- [Fix scrolling performance with CSS will-change property – Four Kitchens](https://www.fourkitchens.com/blog/article/fix-scrolling-performance-css-will-change-property/)
- [Smooth as Butter: Achieving 60 FPS Animations with CSS3](https://medium.com/outsystems-experts/how-to-achieve-60-fps-animations-with-css3-db7b98610108)
- [GPU Animation: Doing It Right – Smashing Magazine](https://www.smashingmagazine.com/2016/12/gpu-animation-doing-it-right/)
- [Aerotwist - On translate3d and layer creation hacks](https://aerotwist.com/blog/on-translate3d-and-layer-creation-hacks/)
- [Myth busting the HTML5 performance of transform:translate vs. top/left | Tumult Company Blog](http://blog.tumult.com/2013/02/28/transform-translate-vs-top-left/)
- [High Performance Animations - HTML5 Rocks](http://www.html5rocks.com/en/tutorials/speed/high-performance-animations/)
- [Relayout,  repaint, reflow](JavaScript/Relayout, repaint, reflow)
- [Reflows & Repaints: CSS Performance making your JavaScript slow? | Stubbornella](http://www.stubbornella.org/content/2009/03/27/reflows-repaints-css-performance-making-your-javascript-slow/)
- [David Baron's weblog: Running animations on the compositor thread](http://dbaron.org/log/20150916-compositor-animations)
- [How I Destroyed my Blog's Performance with CSS Background-Blend-Modes – LearntEmail](https://learntemail.sam.today/blog/1-css-property-that-will-ruin-your-scroll-performance/)
- [CSS Containment in Chrome 52  |  Web  |  Google Developers](https://developers.google.com/web/updates/2016/06/css-containment)
- [contain - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/contain)

### Relayout, repaint, reflow

See [relayout, repaint, reflow](JavaScript#relayout-repaint-reflow)

- [CSS Triggers](https://csstriggers.com/)
- [Why moving elements with translate() is better than pos:abs top/left - Paul Irish](http://www.paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft/)
- [High Performance Animations - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/speed/high-performance-animations/)
- [What forces layout/reflow in Chrome. The comprehensive list.](https://gist.github.com/paulirish/5d52fb081b3570c81e3a)

### Tell the browser that element will change

Use:

	will-change: opacity, transform;

Previously this was used:

	transform: translateZ(0);

- [CSS Will Change Module Level 1](https://drafts.csswg.org/css-will-change/#using)

### Animate pseudo element instead of box-shadow

	/* The fast way */
	element {
	  box-shadow: 0 1px 2px rgba(0,0,0,0.15);
	}
	
	/* Pre-render the bigger shadow, but hide it */
	element::after {
	  box-shadow: 0 5px 15px rgba(0,0,0,0.3);
	  opacity: 0;
	  transition: opacity 0.3s ease-in-out:
	}
	
	/* Transition to showing the bigger shadow on hover */
	element:hover::after {
	  opacity: 1;
	}

- [How to animate "box-shadow" with silky smooth performance | Tobias Ahlin](http://tobiasahlin.com/blog/how-to-animate-box-shadow/)
- http://www.sassmeister.com/gist/c0b2a8d6945a88c76bd9459a0cf1752e

### Improve loading perception with backgrounds

Use background color (selective/average color) or mutliple background (useful for hero images): gradient or inlined svg to display average colors, simple geometric forms, etc. ?

- [Improving Perceived Performance with Multiple Background Images – CSS Wizardry – CSS, OOCSS, front-end architecture, performance and more, by Harry Roberts](http://csswizardry.com/2016/10/improving-perceived-performance-with-multiple-background-images/)

### Fix elements performance

... on Webkit or Blink

user `transform: translateZ(0);` or `translate: perspective(1px);`

- [Fix scrolling performance with CSS will-change property | Fourword: The Four Kitchens blog](https://www.fourkitchens.com/blog/article/fix-scrolling-performance-css-will-change-property)

## Border and outline

### Focus outline

> Removing focus outlines entirely is like setting `cursor: none` [eg. invisible cursor]. Aka a terrible idea.
— Hugo Giraudel @HugoGiraudel

Chrome display focus ring when button are clicked not only tabbed

**Don't**:

	:focus {
		/* Webkit + IE */
		outline: 0;
		/* and set a custom one */
		box-shadow: 0 0 0 3px red;
	}
	/* Firefox */
	::-moz-focus-inner {border:0;}

**Use JS instead**:

	// based on https://github.com/lindsayevans/outline.js and http://www.paciellogroup.com/blog/2012/04/how-to-remove-css-outlines-in-an-accessible-manner/
	(function(document){
		var element = document.createElement("style");
		element.textContent = ":focus{outline:0}::-moz-focus-inner{border:0;}";
		document.head.appendChild(element);
		
		function handleEvent(event){
			element.disabled = event.type == "keydown";
		}
		document.addEventListener("mousedown", handleEvent);
		document.addEventListener("keydown", handleEvent);
	})(document);

- [CSS outline property - outline: none and outline: 0](http://www.outlinenone.com/)
- [how to remove CSS outlines in an accessible manner? | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](http://www.paciellogroup.com/blog/2012/04/how-to-remove-css-outlines-in-an-accessible-manner/)
- https://stackoverflow.com/questions/71074/how-to-remove-firefoxs-dotted-outline-on-buttons-as-well-as-links/
- [Remove blue border from css custom-styled button in Chrome - Stack Overflow](https://stackoverflow.com/questions/20340138/remove-blue-border-from-css-custom-styled-button-in-chrome)
- http://css-tricks.com/removing-the-dotted-outline/
- https://code.google.com/p/chromium/issues/list?can=1&q=focus+ring&colspec=ID+Pri+M+Stars+ReleaseBlock+Cr+Status+Owner+Summary+OS+Modified&cells=tiles
- http://discourse.wicg.io/t/detecting-users-dont-require-visible-focus-rings/804/2

### `border-radius`

	border-radius: 9999px;/*border will not overlap and will make an half circle*/

- How border radius: [Boxed Into Corners: Shapes, Boxes, and Corner Radii](http://hansmuller-webkit.blogspot.fr/2014/01/boxed-into-corners-shapes-boxes-and.html)
- Border curves overlap: [css - Border-radius in percentage (%) and pixels (px) - Stack Overflow](https://stackoverflow.com/questions/29966499/border-radius-in-percentage-and-pixels-px/29966500#29966500) and [CSS Backgrounds and Borders Module Level 3](https://www.w3.org/TR/css3-border/#corner-overlap)
- [CSS Border-Radius Can Do That? | IO 9elements](https://9elements.com/io/css-border-radius/)
- https://drafts.csswg.org/css-backgrounds-3/#corner-overlap

### Jagged edges

Add `1px solid transparent`

- [Smoothing jagged edges on transformed objects in Firefox • Tiffany B. Brown](http://tiffanybbrown.com/2013/04/13/smoothing-jagged-edges-on-transformed-objects-in-firefox/)

### Border with radius and outline with box-shadow

Outline is squared even with `border-radius`. Use `box-shadow` to bypass that.

	element {
		box-shadow: 20px 20px 0px 20px blue,
					-20px -20px 0px 20px red,
					0px 0px 0px 40px gray;
	}

- https://bitsofco.de/the-box-shadow-property/
- [JS Bin - Collaborative JavaScript Debugging](https://jsbin.com/dikita/edit?html,css,output)

### Double borders with mutlpile background clip

- [background clip is configurable for every background gradient separately](https://www.stefanjudis.com/today-i-learned/background-clip-is-configurable-for-every-background-gradient-separately/)
- [Stefan Judis on Twitter: "I just felt like I understood a little bit more how all these creative developers make artworks "with just a few gradients". TIL: #css background clip is configurable for every background gradient separately. 😲 https://t.co/ceWAzQFW6a https://t.co/r6mDUGnaAE" / Twitter](https://mobile.twitter.com/stefanjudis/status/1086393334619402240)

## Shape

### Sloppy border

Aka clipped element

See [Mask](#mask)

Border with angle / angled edges

Possible solutions:

- `transform` (with or without pseudo element)
- border (see [CSS Arrow](#css-arrow))
- `clip-path`
- SVG background
- CSS mask

- [Sloped edges with consistent angle in CSS • CSS & HTML • Kilian Valkhof](https://kilianvalkhof.com/2017/design/sloped-edges-with-consistent-angle-in-css/)
- [Slopy Elements with CSS3](https://tympanus.net/codrops/2011/12/21/slopy-elements-with-css3/)
- [Angled Edges with CSS Masks and Transforms | Viget](https://www.viget.com/articles/angled-edges-with-css-masks-and-transforms)
- [Background Image Shapes | CSS-Tricks](https://css-tricks.com/background-image-shapes/)

### Arrow

Aka triangle

Possible solutions:

- borders
- SVG background
 
Empty arrow:

	element::after {
		content: "";
		position: absolute;
		right: 26px;
		top: 50%;
		width: 8px;
		height: 8px;
		margin: -4px;
		border-bottom: solid 1px black;
		border-right: solid 1px black;
		transform: rotate(-45deg);
	}

- [cssarrowplease](http://cssarrowplease.com/)
- [CSS tutorial - Using borders to produce angled shapes](http://www.howtocreate.co.uk/tutorials/css/slopes)
- [Animation to Explain CSS Triangles](http://codepen.io/chriscoyier/pen/lotjh)

### Border image

Aka 9 slice

- [border-image - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/border-image)
- [border-image-slice - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/border-image-slice)
- [Understanding border-image | CSS-Tricks](https://css-tricks.com/understanding-border-image/)
- [Aerotwist - Slicing SVG 9 Ways](https://aerotwist.com/blog/slicing-svg-9-ways/)
- [Resize](Graphics#resize)

Or use multiple backgrounds and background offset:

Smartphone screenshot

With ![](iphone6-shadow.png) and ![](iphone6.png)

	img{
		width: 230px;
		height: 410px;
		position: absolute;
		border: solid transparent;
		$border-top: (204px / 2);
		$border-left-right: (100px / 2);
		$border-bottom: (192px / 2);
		$iphone-x: (-32px / 2);
		$iphone-y: (-138px / 2);
		$iphone-width: (524px / 2);
		$iphone-height: (1084px / 2);
		$shadow-x: (-66px / 2);
		$shadow-y: (-172px / 2);
		$shadow-width: (148px * 2);
		$shadow-height: (288px * 2);
		border-width: $border-top $border-left-right $border-bottom;
		background: url("iphone6.png") $iphone-x $iphone-y / #{$iphone-width $iphone-height} no-repeat, url("iphone6-shadow.png") $shadow-x $shadow-y / #{$shadow-width $shadow-height} no-repeat;
	}

### Rounded corner hexagon

... use SVG instead as background for pseudo elements

- [CSS rounded corner hexagon](http://blog.andresgalante.com/howto/2015/10/19/css-rounded-corner-hexagon.html)

### Corner

Can't scale to 100% of it container, use SVG instead

See [Sloppy border](#sloppy-border)

	element{
		overflow: hidden;
		position: relative;
		/*display: block;*/
		
		$height: 200px;
		$rotate: 3deg;
		&::before,
		&::after{
			content: "";
			display: block;
			pointer-events: none;
			left: 0;
			right: 0;
			position: absolute;
			z-index: 1;
			background: $color;
			height: $height;
		}
		&::before{
			top: 0;
			transform: translateY(-$height) skewY(-$rotate);// use margin-top: -$height; to simplify transform, you want animate skewY()
			transform-origin: right bottom;
		}
		&::after{
			bottom: 0;
			transform: translateY($height) skewY($rotate);// use margin-bottom: $height; to simplify transform, you want animate skewY()
			transform-origin: right top;
		}
	}

	border-style: solid;
	border-width: 20px 40px 0 0;
	border-color: red transparent transparent transparent;

	border-top: 20px solid red;
	border-right: 40px solid transparent;

	height: 40px;
	width: 20px;
	/*
	Not work with Firefox:
	background: url("data:image/svg+xml;charset=utf8,%3Csvg version='1.1' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 1 1' preserveAspectRatio='none'%3E%3Cpolygon points='0,0 1,0 0,1' fill='%23ffffff'/%3E%3C/svg%3E");
	*/
	background: url("data:image/svg+xml;charset=utf8,%3Csvg version='1.1' xmlns='http://www.w3.org/2000/svg'%3E%3Csvg viewBox='0 0 1 1' preserveAspectRatio='none'%3E%3Cpolygon width='100%25' height='100%25' points='0,0 1,0 0,1' fill='grey'/%3E%3C/svg%3E%3C/svg%3E");

- [Code a Simple Folded Corner Effect With CSS | Design Shack](https://designshack.net/articles/css/code-a-simple-folded-corner-effect-with-css/)

### Mask

Aka clip

and `clip-path`

	mask: linear-gradient(to right, rgba(0,0,0,0) 0%, rgba(0,0,0,1) 5%, rgba(0,0,0,1) 95%, rgba(0,0,0,0) 100%);/*not work in FF38 nor IE11*/

- [Using Masks](https://developer.apple.com/library/safari/documentation/InternetWeb/Conceptual/SafariVisualEffectsProgGuide/Masks/Masks.html)
- [Clipping and Masking in CSS | CSS-Tricks](https://css-tricks.com/clipping-masking-css/)
- [CSS Masking - HTML5 Rocks](http://www.html5rocks.com/en/tutorials/masking/adobe/)
- [Creating Responsive Shapes With Clip-Path And Breaking Out Of The Box – Smashing Magazine](http://www.smashingmagazine.com/2015/05/11/creating-responsive-shapes-with-clip-path/)
- [Clip Path Generator - CSS Plant](http://cssplant.com/clip-path-generator)

### Spinner

Aka indeterminate progress bar, loader

Or use SVG with CSS animation or JS, canvas, etc.

- [How to create loading image using CSS only](http://web-tricks.org/content/how-create-loading-image-using-css-only)
- [The Tale of Three Spinners](https://blog.keanulee.com/2014/10/20/the-tale-of-three-spinners.html)
- [CSS loader spinner](http://codepen.io/anon/pen/VbgZpZ) - see discussion [Dave DeSandro on Twitter: "CSS challenge: Any way to refactor this loader spinner (without preprocessor loops)? https://t.co/RUz7qArjgS"](https://twitter.com/desandro/status/867023809047658496)

### Polygon

Polygon (`clip-path`) with 4 points with stagger animation (see `delay`):

	let from = [
		{x: 0, y: 0.25},//tl
		{x: 0, y: 0.5},//tr
		{x: 0, y: 0.5},//br
		{x: 0, y: 0.75},//bl
	];
	
	let to = [
		{x: 0, y: 0},//tl
		{x: 1, y: 0},//tr
		{x: 1, y: 1},//br
		{x: 0, y: 1},//bl
	];
	
	let duration = 0.5;
	let delay = 0.1;
	let staggerDuration = duration + (from.length - 1) * delay;
	let easing = k => ( k *= 2 ) < 1 ? 0.5 * k * k * k * k : - 0.5 * ( ( k -= 2 ) * k * k * k - 2 );// power 3
	let numKeyframes = 11;// for duration
	let keyframeDuration = staggerDuration / numKeyframes;
	
	let keyframes = new Array(numKeyframes);
	
	// Each keyframes
	for(let keyframeIndex = 0; keyframeIndex < keyframes.length; keyframeIndex++){
		let time = keyframeIndex * keyframeDuration;
		let values = keyframes[keyframeIndex] = new Array(from.length);
	
		// Each points
		for(let pointIndex = 0; pointIndex < values.length; pointIndex++){
			let localTime = time - pointIndex * delay;
			localTime = Math.min(Math.max(localTime, 0), duration);
			let progress = easing(localTime / duration);
		
			let pointFrom = from[pointIndex];
			let pointTo = to[pointIndex];
			values[pointIndex] = {
				x: pointFrom.x + (pointTo.x - pointFrom.x) * progress,
				y: pointFrom.y + (pointTo.y - pointFrom.y) * progress
			};
		}
	}
	
	let css = keyframes.reduce(
		(result, value, index) => {
			let points = value.map(value => `${(value.x * 100).toFixed(3)}% ${(value.y * 100).toFixed(3)}%`).join(",");
			result += `${index * 100 / (numKeyframes - 1)}%{-webkit-clip-path: polygon(${points}); clip-path: polygon(${points})}`;
			return result;
		},
		""
	);
	console.log(css);

- [Glue Cross-Browser Responsive Irregular Images with Sticky Tape | CSS-Tricks](https://css-tricks.com/glue-cross-browser-responsive-irregular-images-sticky-tape/)
- [Clippy — CSS clip-path maker](http://bennettfeely.com/clippy/)

## Rule equivalence

	width: 100%;
	max-width: 600px;

is the same as

	width: 600px;
	max-width: 100%;

## Counter

Note: `counter-reset()` doesn’t work only for element rule. Not for pseudo element. e.g. `element::before{counter-reset: counter-name;}`, use `element{counter-reset: counter-name;}` instead

CSS counter

- [Fun Times with CSS Counters / Coder's Block](http://codersblock.com/blog/fun-times-with-css-counters/)

## Hide video controls on iOS

	/*hide controls on iOS*/
	::-webkit-media-controls{
		display: none !important;
	}

or more specific

	/* play button */
	::-webkit-media-controls-start-playback-button{
		display: none !important;
	}
	
	/* text track */
	::-webkit-media-text-track-container
	::-webkit-media-text-track-background
	::-webkit-media-text-track-display
	
	/* see more selectors:
	- https://chromium.googlesource.com/chromium/blink/+/72fef91ac1ef679207f51def8133b336a6f6588f/Source/core/css/mediaControls.css
	- [Programming Tricks: Styling HTML Media Inner Workings](http://advprog.blogspot.fr/2013/07/styling-html-media-inner-workings.html)
	*/
	
	::cue

- [Adding captions and subtitles to HTML5 video - App Center | MDN](https://developer.mozilla.org/en-US/Apps/Fundamentals/Audio_and_video_delivery/Adding_captions_and_subtitles_to_HTML5_video)
- [865395 – Implement the ::cue pseudo-element](https://bugzilla.mozilla.org/show_bug.cgi?id=865395)

## Content

- [Displaying numeric CSS vars in generated content](https://codepen.io/cassie-codes/pen/22ea69e0f681d45f2f4c2ca5e6acf4ab) - Use `counter-reset` and `content`

## Quotes

```css
html[lang=fr] blockquote {
	quotes: "«\00A0" "\00A0»";
}
blockquote::before {
	content: open-quote;
}
blockquote::after {
	content: close-quote;
}
```

## Round values

- [Using decimal percentage values in responsive design | Divya Manian](http://nimbupani.com/using-decimal-percentage-values-in-responsive-design.html)

## Gradient

	background: linear-gradient(to bottom, rgba(0,0,0,0) 0%, rgba(0,0,0,0.4) 100%);

- [CSS linear-gradient helper](http://codepen.io/captainbrosset/pen/ByqRMB) and [captainbrosset/linear-gradient: A visualization tool for CSS linear-gradients](https://github.com/captainbrosset/linear-gradient)
- [Do you really understand CSS linear-gradients? – Medium](https://medium.com/@patrickbrosset/do-you-really-understand-css-linear-gradients-631d9a895caf)
- [linear-gradient() - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/linear-gradient)

(inline) SVG can be used as fallback:

	background: url("data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%201%201'%20preserveAspectRatio='none'%3E%3ClinearGradient%20id='g'%20x1='0%25'%20y1='0%25'%20x2='0%25'%20y2='100%25'%3E%3Cstop%20offset='0%25'%20stop-color='rgba(0,0,0,0)'/%3E%3Cstop%20offset='100%25'%20stop-color='rgba(0,0,0,0.4)'/%3E%3C/linearGradient%3E%3Crect%20fill='url(%23g)'%20width='1'%20height='1'/%3E%3C/svg%3E");/* IE9 SVG */
	background: linear-gradient(to bottom, rgba(0,0,0,0) 0%, rgba(0,0,0,0.4) 100%);

Gradient border (use SVG):

- [How To Apply SVG Linear Gradients To A Fill Or Stroke - Vanseo Design](http://vanseodesign.com/web-design/svg-linear-gradients/)

See [SVG/Gradient](SVG#gradient)

## Variables

Conditions:

	--big: 1;/* or 0 */
	prop: calc(25px * var(--big));/* when is big */
	prop: calc(25px * (1 - var(--big)));/* when is not big */

	/*
	Possible conditions, but all can't be with CSS calc()
	eq: 1 - abs(sign(a - b))
	neq: abs(sign(a - b))
	gt: max(sign(a - b), 0)
	lt: max(sign(b - a), 0)
	ge: 1 - lt(a, b)
	le: 1 - gt(a, b)
	and: a * b
	or: min(a + b, 1)
	xor (a + b) % 2
	not: 1 - a
	*/

	@supports (color: var(--)) { ... }
	/*
	Notes:
	- Can use any property (i.e. not color)
	- Don't have to include an actual variable name, var(--) works
	*/

Note: be carefull with the length of `calc()`:

> UAs must support `calc()` expressions of at least 20 terms, where each `NUMBER`, `DIMENSION`, or `PERCENTAGE` is a term. If a `calc()` expression contains more than the supported number of terms, it must be treated as if it were invalid.
— https://drafts.csswg.org/css-values-3/#calc-syntax

Note: `calc()` is not supported in all properties (like in `rgba()` channels)

- [Conditions for CSS Variables](http://kizu.ru/en/fun/conditions-for-css-variables/)

For colors, use explicit named color name `--light-blue` (`$light-blue`). **Don't use the context for variable name (ex: `blue-text`, `red-title`).** This allow minor adjustements.
If you need to use an other color globally, rename the variable to match to the new color name. Otherwise (the color is needed locally), create a new variable an use it.
Note: some keywords already exist: `white`, `black`, etc. See [color keywords](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value#Color_keywords)

```html
<button type="button" onclick="click()">Click me</button>
<style>
:root{
	--cond: root.style.background = x ? "rebeccapurple" : "oldenrod";
}
</style>
<script>
	let x = false;
	let condSrc = getComputedStyle(document.querySelector(":root")).getPropertyValue('--cond');
	function click(){
		x = !x;
		eval(condSrc);
	}
</script>
```

- [Logical Operations with CSS Variables | CSS-Tricks](https://css-tricks.com/logical-operations-with-css-variables/)
- [pixelass/hphn: A collection of intersing concepts using css variables.](https://github.com/pixelass/hphn)
- [CSS custom properties (native variables) In-Depth](https://blog.hospodarets.com/css_properties_in_depth)
- [Variables: The Backbone Of CSS Architecture – Smashing Magazine](https://www.smashingmagazine.com/2016/01/variables-in-css-architecture/)
- [Using CSS variables correctly - Mike Riethmuller](https://madebymike.com.au/writing/using-css-variables/)
- [DRY Switching with CSS Variables: The Difference of One Declaration | CSS-Tricks](https://css-tricks.com/dry-switching-with-css-variables-the-difference-of-one-declaration/)

## Color `currentColor` keyword

It's a keyword but act like a [variable](#variables)

Like a inherited color but used by border-color or background-color

Supported by all major browser (include IE9+)

- https://stackoverflow.com/questions/23936150/issues-with-css-currentcolor-keyword-in-ios-and-safari
- [\<color\> - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value#currentColor_keyword)
- [Difference between currentColor & Custom Properties | Mike Riethmuller](https://www.madebymike.com.au/writing/currentcolor-and-custom-properties/)

## Colors names

- http://graphicdesign.stackexchange.com/questions/5120/how-can-i-get-the-closest-color-word-for-a-hex-color
- http://chir.ag/projects/name-that-color/
- https://stackoverflow.com/questions/8318911/why-does-html-think-chucknorris-is-a-color

## Filters and blend modes

- already apply (only on rasterized or SVG)
- SVG filter on HTML elements
- `text-shadow` (only on text)
- CSS filter (if supported)

- [Methods for Contrasting Text Against Backgrounds | CSS-Tricks](https://css-tricks.com/methods-contrasting-text-backgrounds/)
- [Fixing the white glow in the CSS blur() filter by Taylor Hunt on CodePen](https://codepen.io/tigt/post/fixing-the-white-glow-in-the-css-blur-filter)
- [Gaussian Blur and CSS3/SVG - CSS-Plus](http://css-plus.com/2012/03/gaussian-blur/)
- [the new code – box-shadow property vs. drop-shadow filter: a complete comparison](http://thenewcode.com/598/boxshadow-property-vs-dropshadow-filter-a-complete-comparison)
- [Distorted Button Effects with SVG Filters | Codrops](http://tympanus.net/codrops/2016/05/11/distorted-button-effects-with-svg-filters/)
- [Image Effects with CSS](http://bennettfeely.com/image-effects/)
- [Photo Toning with Gradients & Blend Modes](http://daveshea.com/2016/10/24/photo-toning.html)
- `filter: drop-shadow(5px 5px 5px #222);` on transparent PNG/background. See https://stackoverflow.com/a/21074208/470117 and [the new code – Creating a True Cross-Browser Drop Shadow Effect With CSS & SVG](http://thenewcode.com/600/Creating-a-True-Cross-Browser-Drop-Shadow-Effect-With-CSS-amp-SVG)
- [Fixing the white glow in the CSS blur() filter by Taylor Hunt on CodePen](https://codepen.io/tigt/post/fixing-the-white-glow-in-the-css-blur-filter)
- [Switch font color for different backgrounds with CSS | CSS-Tricks](https://css-tricks.com/switch-font-color-for-different-backgrounds-with-css/)

## Newsletters

> Newsletters, the hardest thing after IE6

- [Email Marketing Guides | Campaign Monitor](https://www.campaignmonitor.com/resources/)
- [Guide to CSS support in email | Campaign Monitor](https://www.campaignmonitor.com/css/)
- [FreshInbox - Dynamic and Interactive Email (Kinetic) CSS Support](http://freshinbox.com/resources/css.php)
- http://www.pompage.net/pompe/cssemail/
- http://pompage.net/pompe/emails-html-dompter-la-bete/
- http://codepen.io/M_J_Robbins/full/MeeMew use CSS for interactivity

## Visible inside hidden

If a element with `visibility: visible;` is a child of an element with `visibility: hidden;` then the child still visible

> *hidden*: The generated box is invisible (fully transparent, nothing is drawn), but still affects layout. Furthermore, descendants of the element will be visible if they have 'visibility: visible'.
> — [CSS 2.1](http://www.w3.org/TR/CSS2/visufx.html#visibility)

Don't use `visibility: visibile`, use `visibility: inherit;` instead. Use `visibility: visibile` only if you need to show a child inside hidden element.

## SVG

SVG don't have box model (vs. HTML) means no content, padding or border boxes

Default value of `transform-origin` is `0 0` (vs. `50% 50%` for HTML). Absolute values are relative to SVG canvas. Percentage values are relative to element's bounding box (including stroke) but not works in Firefox (See https://bugzilla.mozilla.org/show_bug.cgi?id=891074)

3D transforms can work (but perspective don't on Chrome). There not hw. accelerated

See [Content vs. decorative image](HTML#content-vs-decorative-image)

## Normalize

CSS Fixes

https://github.com/necolas/normalize.css/blob/master/normalize.css

## Reset

	/* Button as DIV */
	button{
		font: inherit;
		/* ? line-height: inherit;*/
		display: block;
		padding: 0;
		border: 0;
		border-radius: 0;/*iOS*/
		color: inherit;
		text-align: inherit;
		box-sizing: content-box;
		background: none;
		overflow: visible;/*IE*/
		width: inherit;/*100% ?*/
	}
	
	/* input */
	input{
		font: inherit;
		color: inherit;
		box-sizing: content-box;
		border: 0;
		background: none;
		width: 100%;/*required for auto width*/
	}

	/* https://www.impressivewebs.com/fixing-styles-on-code-tags-nested-inside-links/ */
	code {
		/* some styles */
	}
	a code {
		background: inherit;
		color: inherit;
		padding: inherit;
	}	

- [Basic styling of `button` elements – tests](http://fvsch.com/code/button-css/test.html)

May be necessary:

		-webkit-appearance: none;
		-moz-appearance: none;
		appearance: none;

- appearance dropped from CSS3: [css4-ui features list [CSS Working Group Wiki]](https://wiki.csswg.org/spec/css4-ui#dropped-css3-features)

To reset as a interactive element, `cursor: pointer` could be required (**but you shouldn't**: [Buttons shouldn't have a hand cursor](UI - UX#buttons-shouldnt-have-a-hand-cursor)).
 
	/* Fieldset */
	legend {
		padding: 0;
		display: table;
	}
	fieldset {
		border: 0;
		padding: 0.01em 0 0 0;
		margin: 0;
		min-width: 0;
	}
	body:not(:-moz-handler-blocked) fieldset {
		display: table-cell;
	}

- http://thatemil.com/blog/2015/01/03/reset-your-fieldset/
- [Stop Using Resets: Visual Examples of the Practical Nonsense of Resets and Normalizers · Jens Oliver Meiert](https://meiert.com/en/blog/stop-using-resets/)

CSS for `<sub>` and `<sup>`:

	sub,
	sup {
		/* Specified in % so that the sup/sup is the
		right size relative to the surrounding text */
		font-size: 75%;
	
		/* Zero out the line-height so that it doesn't
		interfere with the positioning that follows */
		line-height: 0;
	
		/* Where the magic happens: makes all browsers position
		the sup/sup properly, relative to the surrounding text */
		position: relative;
	
		/* Note that if you're using Eric Meyer's reset.css, this
		is already set and you can remove this rule */
		vertical-align: baseline;
	}
	
	sup {
		/* Move the superscripted text up */
		top: -0.5em;
	}
	
	sub {
		/* Move the subscripted text down, but only
		half as far down as the superscript moved up */
		bottom: -0.25em;
	}

- [CSS for `<sub>` and `<sup>`](https://gist.github.com/unruthless/413930)

## List

> remove list element semantics when `list-style: none` is used
> - ["Fixing" Lists | scottohara.me](https://www.scottohara.me/blog/2019/01/12/lists-and-safari.html)

	.link{
		
	}
	.link-list{/*or .link-ul*/
		list-style: none;
		padding: 0;
		// Skip spaces
		font-size: 0;
		// Remove blank space
		word-spacing: 0px;
		text-align: center;
	}
	.link-li{
		// Restore font size, defined with the previous font-size: 0; that skip spaces
		font-size: @root-font-size;
		// Restore value
		word-spacing: normal;
		display: inline-block;
	}
	.link-li + .link-li{/* or .link-li:not(:last-child) or .link-li:nth-last-child(n+2) */
		margin-left: 20px;
	}
	/*
	or
	.link-li{
		margin-left: 20px;
	}
	.link-li:last-child{
		margin-left: 0;
	}
	*/

## Detect touch device

See [detect touch device](JS#detect-touch-device)

	@media (pointer: coarse) and (hover: none) {
		/* primary input mechanism is a touch screen, require larger interactive elements (!= small screen) */
	}

- [Size of touch screen button](UI - UX#size-of-touch-screen-button)
- [Dev.Opera — Interaction Media Features and their potential (for incorrect assumptions)](https://dev.opera.com/articles/media-features/)
- [pointer - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/pointer)
- [hover - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/hover)
- [A shim for the Media Queries Level 4 hover @media feature.](https://github.com/twbs/mq4-hover-shim) - require JS
- [The Good & Bad of Level 4 Media Queries | Blog | Stu Cox](http://www.stucox.com/blog/the-good-and-bad-of-level-4-media-queries/)
- [Media Query Level 4 Specs](http://drafts.csswg.org/mediaqueries/#hover)
- [Touch Devices Should Not Be Judged By Their Size | CSS-Tricks](https://css-tricks.com/touch-devices-not-judged-size/)

## Don't reveal element with hover

See [detect touch device](#detect-touch-device)

On touch only devices it's could be a problem, especially if it's a link. Apple circumvent that: [The Annoying Mobile Double-Tap Link Issue | CSS-Tricks](https://css-tricks.com/annoying-mobile-double-tap-link-issue/)

## CSS 3D

- [Things to Watch Out for When Working with CSS 3D | CSS-Tricks](https://css-tricks.com/things-watch-working-css-3d/)

## Chart

- [Interactive Pie chart \[all Browsers\]](https://codepen.io/captlid/pen/BvZybM) - use clip rect and rotate transform

### Pie chart

Use SVG instead, with a `stroke-width` smaller than circle radius (to fix IE rending bug), eg. for a radius of 50px, use `stroke-width: 49.9px`

## Line alternation in `pre`

	pre{
		line-height: 1.5;
		font-size: 0.75rem;
		background: white linear-gradient(rgb(238, 238, 238) 1.5em, rgb(221, 221, 221) 1.5em) repeat center / 100% 3em;
	}

## Table col/row highlight

- [Simple CSS-Only Row and Column Highlighting | CSS-Tricks](http://css-tricks.com/simple-css-row-column-highlighting/)

## Use pseudo element for line numbers

- [Prevent an element from being selected and copied with CSS](https://danoc.me/blog/css-prevent-copy/)

## Jokes

```css
#titanic{
	float: none;
}
#bermuda-triangle {
	display: none;
}
.sinper-mode-engaged{
	cursor: crosshair;
}
#periodic{
	display: table;
}
#big-bang::before { 
	content: "";
}
#chucknouris{
	color: #BADA55;
}
#nsa{
	opacity: 1;
}
#tower-of-pisa { 
	font-style: italic;
}
.ninja{
	visibility: hidden;
	color: black;
}
.obese{
	width: 200%;
	overflow: visible;
}
.yomama{
	width: 99999999px;
}
.wife{
	right: 100%
	margin: 0%;
}
#lego { 
	display: block;
}
.delorean{
	z-index: -1955;
}
.fear { 
	display: none;
}
.illuminati{
	position: absolute;
	visibility: hidden;
}
```

- [CSS Puns & CSS Jokes ~ Curated by Saijo George](http://saijogeorge.com/css-puns/)
- [CSS Humor (@CSSHumor) | Twitter](https://twitter.com/csshumor)

## Use filter opactiy for filter fallback

	element{
		filter: opacity(0%);/*will hide element if filter is supported*/
	}

- http://codepen.io/tigt/post/blurred-background-image-with-fallback

## Tab size for preserved whitespace sequence

	pre{
		/*implicit white-space: pre*/
		tab-size: 2;
	}

- [tab-size - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/tab-size)
- [white-space - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/white-space)

## The property `background` is propagated from `<body>` to `<html>`

> For documents whose root element is an HTML HTML element [HTML401] or an XHTML html element [XHTML11]: if the computed value of ‘background-image’ on the root element is ‘none’ and its ‘background-color’ is ‘transparent’, user agents must instead propagate the computed values of the background properties from that element's first HTML BODY or XHTML body child element. 
— https://www.w3.org/TR/css3-background/#body-background

> In other words, user agents must propagate the background of body through the viewport if html is not styled with a background. Meaning if html is styled with a background then the background of body will be only painted within the body's boundaries. 

> `body` does not mean the whole visible page. `html` does. `body` only means its contents.

- https://github.com/jonathantneal/sanitize.css/issues/42#issuecomment-150272962

## Odometer

Aka counter effect, timer, countdown

Each number char often don't have the same width, use a monospace font or:

	font-feature-settings: "tnum";
	font-variant-numeric: tabular-nums;

- https://github.com/coderitual/odoo
- [We Bo 🔥 on Twitter: "Countdown clock kept shifting because the width of number change. Got to use thi to fix it!…](https://twitter.com/wesbos/status/932644812582522880)

## Don't use `contenteditable="true"` and `text-overflow: ellipsis` in same time

Text that overflow is not visible and can't be selected

Or toggle `text-overflow` when field is focused.

- https://twitter.com/dotmariusz/status/776334849007316992

## Newline in CSS content

	element::before {
		content: "\A";
	}

- [css3 - How to insert a line break before an element using CSS - Stack Overflow](https://stackoverflow.com/questions/7363766/how-to-insert-a-line-break-before-an-element-using-css)

## Slider

Aka slideshow, carrousel

[scroll snap points](#snap-points) can be used.

	.items{
		overflow-x: auto;/*or overflow-x: hidden; allow to control scrollLeft to custom scroll*/
		display: flex;
	}
	.item{
		flex: 1 0 0;// allow to grow (>2: min-width, 2: 50% each, 1: 100%)
		min-width: 47%;// show at least 2 + a part of an other
	}

## Parallax effect

Use prespective on body, scale and `transform-style: preserve-3d` on elements

The effect works only if the perpective is set on a container that scroll overflow (rendered relative to the fixed perspective of the container). Doesn't work on root element (`<html>`) because overflow doesn't work the same way as other elements.

Position when rescale will be based on `transform-origin`

	<!DOCTYPE html>
	<html>
	<head>
		<meta charset="utf-8">
		<meta name="viewport" content="width=device-width">
		<title>JS Bin</title>
		<style>
			html{
				height: 100%;
				overflow: hidden;
			}
			body {
				overflow: auto;
				height: 100%;
				perspective: 1px;
				transform-style: preserve-3d;
				perspective-origin: top left;
			}
			
			.parallax {
				position: absolute;
				top: 200px;
				transform-origin: -250px -200px;/*based on position left and top to fix position after scale*/
				left: 250px;
				font-size: 24px;
			}
		</style>
	</head>
	<body>
		<div class="test">
			<div class="parallax" style="transform: translateZ(-1.2px) scale(2.2);">z = -1.2</div>
			<div class="parallax" style="transform: translateZ(-1.0px) scale(2);">z = -1.0</div>
			<div class="parallax" style="transform: translateZ(-0.8px) scale(1.8);">z = -0.8</div>
			<div class="parallax" style="transform: translateZ(-0.6px) scale(1.6);">z = -0.6</div>
			<div class="parallax" style="transform: translateZ(-0.4px) scale(1.4);">z = -0.4</div>
			<div class="parallax" style="transform: translateZ(-0.2px) scale(1.2);">z = -0.2</div>
			<div class="parallax" style="transform: translateZ(0px) scale(1);">z = 0</div>
			<div class="parallax" style="transform: translateZ(0.2px) scale(0.8);">z = 0.2</div>
			<div class="parallax" style="transform: translateZ(0.4px) scale(0.6);">z = 0.4</div>
			<div class="parallax" style="transform: translateZ(0.6px) scale(0.4);">z = 0.6</div>
			<div class="parallax" style="transform: translateZ(0.9px) scale(0.1);">z = 0.9</div>
			<div style="height: 1000px;"></div>
		</div>
	</body>
	</html>

	:root {
		--plx-perspective: 1;
	}
	
	.plx {
		overflow-x: hidden;
		overflow-y: scroll;
		transform-style: preserve-3d;
		perspective: calc(var(--plx-perspective) * 1px);
		perspective-origin: 0 0;
		perspective-origin-x: 100%;
	}
	.plx__child {
		--plx-scale: calc(var(--plx-perspective) - var(--plx-z));
		transform: translateZ(calc(var(--plx-z) * 1px)) translateY(calc(50% - 50vh)) scale(var(--plx-scale));
		transform-origin: 0 0;
		transform-origin-x: 100%;
	}
	.plx__child--fast {
		--plx-z: .3;
	}
	.plx__child--slow {
		--plx-z: -.3;
	}

- [Css only parallax](https://codepen.io/irksum/pen/qxbarb)
- [Pure CSS Parallax Websites by Keith Clark](http://keithclark.co.uk/articles/pure-css-parallax-websites/)
- [A grouped pure CSS parallax demo (with webkit overflow fix) by Keith Clark](http://keithclark.co.uk/articles/pure-css-parallax-websites/demo3-webkit-overflow-fix/)
- [Sass parallax example](http://codepen.io/scottkellum/details/bHEcA)
- [Parallax CSS & SVG](https://codepen.io/CodeXYZ/pen/vExPNy)
- [Pure CSS Parallax Scrolling](https://codepen.io/keithclark/pen/JycFw)
- [Performant Parallaxing  |  Web  |  Google Developers](https://developers.google.com/web/updates/2016/12/performant-parallaxing)
- [JS Bin - Collaborative JavaScript Debugging](http://jsbin.com/sexiwe/edit?output)
- [ui-element-samples/parallax at gh-pages · GoogleChrome/ui-element-samples](https://github.com/GoogleChrome/ui-element-samples/tree/gh-pages/parallax)
- [Landscape parallax using CSS](http://thewaterbear.com/pure-css-landscape-parallax/)

## Print

- [Designing For Print With CSS – Smashing Magazine](https://www.smashingmagazine.com/2015/01/designing-for-print-with-css/)
- [Modern framework to print correctly](https://github.com/BafS/Gutenberg)
- [I totally forgot about print style sheets – Medium](https://medium.com/@matuzo/i-totally-forgot-about-print-style-sheets-f1e6604cfd6)

### Base print stylesheet

	body {
		width: auto !important;
		margin: auto !important;
		font-family: serif;
		font-size: 12pt;
		background-color: white !important;
		color: black !important;
	}
	p, h1, h2, h3, h4, h5, h6, blockquote, ul, ol {
		color: black !important;
		margin: auto !important;
	}
	.print {
		display: block;/* show printable elements */
	}
	p, blockquote {
		orphans: 3;/* no line alone after */
		widows: 3;/* no line alone before */
	}
	blockquote, ul, ol {
		page-break-inside: avoid;/* no element cutted */
	}
	h1 {
		page-break-before: always;/* each h1 start at the begining of a page */
	}
	h1, h2, h3, caption {
		page-break-after: avoid;/* no page break after this elements */
	}
	a[href] {
		color: blue !important;
		text-decoration: underline !important;
	}
	a[href]:after {
		content: " (" attr(href) ")";/* display link URL */
	}

## Complexe background

Draw lines, etc. use SVG as background and/or multiple backgrounds

	<svg xmlns="http://www.w3.org/2000/svg" fill="red">
		<rect x="0" y="0" width="1" height="100%"/>
		<rect x="16.66%" y="0" width="1" height="100%"/>
		<rect x="33.33%" y="0" width="1" height="100%"/>
		<rect x="50%" y="0" width="1" height="100%"/>
		<rect x="66.66%" y="0" width="1" height="100%"/>
		<rect x="83.33%" y="0" width="1" height="100%"/>
		<rect x="100%" y="0" width="1" height="100%" transform="translate(-1, 0)"/>
	</svg>

## Hierarchy view

HTML:

	<!-- Main component -->
	<div class="hv-wrapper">
		<!-- Key component -->
		<div class="hv-item">
			<div class="hv-item-parent">
				<p>Parent</p>
			</div>
	
			<ul class="hv-item-children">
				<li class="hv-item-child">
					<!-- Key component -->
					<div class="hv-item">
						<div class="hv-item-parent">
							<p>Parent</p>
						</div>
	
						<ul class="hv-item-children">
							<li class="hv-item-child">
								<p>Child 1</p>
							</li>
	
							<li class="hv-item-child">
								<p>Child 2</p>
							</li>
	
							<li class="hv-item-child">
								<p>Child 2</p>
							</li>
						</ul>
					</div>
				</li>
	
				<li class="hv-item-child">
					<p>Child 2</p>
				</li>
	
				<li class="hv-item-child">
					<p>Child 3</p>
				</li>
			</ul>
		</div>
	</div>

CSS:

	@import url('https://fonts.googleapis.com/css?family=Poppins');
	
	$bottom-margin: 50px;
	$line-width: 2px;
	$line-color: rgba(#FFF, 0.7);
	$bg-color: #EFE6E2;
	
	body{
		background: $bg-color;
		font-family: 'Poppins', sans-serif;
		padding-top: 50px;
	}
	
	p{
		margin: 0;
		background-color: #fff;
		color: #DE5454;
		padding: 30px;
		border-radius: 7px;
		min-width: 70px;
		text-align: center;
		box-shadow: 0 3px 6px rgba(#CC8367, 0.22);
	}
	
	.hv-wrapper{
		display: flex;
		.hv-item{
			display: flex;
			flex-direction: column;
			margin: auto;
			.hv-item-parent{
				margin-bottom: $bottom-margin;
				position: relative;
				display: flex;
				justify-content: center;
				p{
					font-weight: bold;
					color: #DE5454;
				}
				&:after{
					position: absolute;
					content: '';
					width: $line-width;
					height: $bottom-margin / 2;
					bottom: 0;
					left: 50%;
					background-color: $line-color;
					transform: translateY(100%);
				}
			}
			.hv-item-children{
				display: flex;
				justify-content: center;
				.hv-item-child{
					padding: 0 15px;
					position: relative;
				
					&:before, &:after{
						content: '';
						position: absolute;
						background-color: $line-color;
						left: 0;
					}
				
					&:before{
						left: 50%;
						top: 0;
						transform: translateY(-100%);
						width: $line-width;
						height: $bottom-margin / 2;
					
					}
				
					&:after{
						top: -$bottom-margin / 2;
						transform: translateY(-100%);
						height: $line-width;
						width: 100%;
					}
				
					&:first-child:after{
						left: 50%;
						width: 50%;
					}
					
					&:last-child:after{
						width: calc(50% + 1px);
					}				
				
				}
			}
		}
	}

- [Hierarchy view component with pure CSS (SASS) – Medium](https://medium.com/@sichisichi/hierarchy-view-component-with-pure-css-sass-1ff5add5cad7#)

## Video player

- [mozilla-central: toolkit/themes/shared/media/videocontrols.css](http://hg.mozilla.org/mozilla-central/file/tip/toolkit/themes/shared/media/videocontrols.css)
- https://people-mozilla.org/~shorlander/files/video-controls-i03/videoControls-i02.html

## Progressive Enhancement

Aka fallback, feature detection

- [CSS and progressive enhancement | justmarkup](https://justmarkup.com/log/2017/02/css-and-progressive-enhancement/)
- [Using Feature Detection to Write CSS with Cross-Browser Support | CSS-Tricks](https://css-tricks.com/using-feature-detection-to-write-css-with-cross-browser-support/)

See [Progressive Enhancement](Web#progressive-enhancement)

## Lockup

Aka typographic header

> A type lockup is a typographic design where the words and characters are styled and arranged very specifically

Use inline SVG

![Gardens](https://cdn.css-tricks.com/wp-content/uploads/2015/11/gardens.jpg)

- [Creating a Web Type Lockup | CSS-Tricks](https://css-tricks.com/creating-web-type-lockup/)

## Pseudo elements

- [A Whole Bunch of Amazing Stuff Pseudo Elements Can Do | CSS-Tricks](https://css-tricks.com/pseudo-element-roundup/)

## Common bugs

- [9 Most Common IE Bugs and How to Fix Them](https://code.tutsplus.com/tutorials/9-most-common-ie-bugs-and-how-to-fix-them--net-7764)

## Table of contents

- [WebSlides - Table of Contents](https://codepen.io/webslides/pen/VMZJwj)

## Toggle

**Don't use it because it's not accessible**. It use a bit of JS to add/update ARIA attributes

Carousel / slideshow, modal, collpase, dropdown menu, burger menu, etc.

use `:target` `:checked`

- [Pure CSS / CSS3 Fullscreen Navigation with Hamburger Toggle - CSS Script](https://www.cssscript.com/pure-css-css3-fullscreen-navigation-with-hamburger-toggle/)
- [You can get pretty far in making a slider with just HTML and CSS | CSS-Tricks](https://css-tricks.com/can-get-pretty-far-making-slider-just-html-css/)
- [Stuff you can do with the "Checkbox Hack" | CSS-Tricks](https://css-tricks.com/the-checkbox-hack/)
