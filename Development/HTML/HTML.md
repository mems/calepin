Best pratices: specs, common (bad or good) (see also http://www.w3.org/TR/html5/text-level-semantics.html examples etc.)

# Best pratices — Coding conventions

- http://mdo.github.io/code-guide/#html
- https://github.com/styleguide/templates
- https://github.com/hail2u/html-best-practices
- [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.xml)

Lint HTML:

- [Linting HTML using CSS](https://bitsofco.de/linting-html-using-css/)
- [debugCSS : (X)HTML debugging tool built with CSS](http://imbrianj.github.io/debugCSS/)

## Use lowercase

HTML is case insensitive for tag name, but lowercase is easier to read.

- [Is it bad to use uppercase letters for html tags? - Stack Overflow](https://stackoverflow.com/questions/19808514/is-it-bad-to-use-uppercase-letters-for-html-tags)

## Close tags

Prefer closing tags, HTML5 support enclosing unclosed tags, but it's harder to read. Use

	<p>Some text...</p>
	<p>Some text...</p>

Instead of

	<p>Some text...
	<p>Some text...

## Choose the right tag and attribute

See [Accessibility](#Accessibility) and [Patterns, markup, semantics and snippets](#Patterns, markup, semantics and snippets)

- http://html5doctor.com/i-b-em-strong-element/

> When there are multiple instances of a particular landmark role on a page, provide a unique accessible name for each landmark with the same role to enable users to differentiate among them.

## Buttons vs links

> Links that don’t go anywhere should be buttons
> - [Links that don’t go anywhere should be buttons | Christian Heilmann](https://christianheilmann.com/2019/02/05/links-that-dont-go-anywhere-should-be-buttons/)

**Interactive buttons should be injected by JS and not available without JS**

	<button type="button">Action 1</button>

instead of

	<a href="#">Action 1</a>
	<a>Action 2</a>
	<a href="javascript:;">Action 3</a>
	<span>Action 3</span>
	<span role="button">Action 4</span>

Remplace all links for tabbed interfaces, collabsibles, modal openers by a button (with JS)

- [Anchors vs Buttons](https://bitsofco.de/anchors-vs-buttons/)
- [Anchors, Buttons, and Accessibility // Formidable Labs](http://formidablelabs.com/blog/2014/05/08/anchors-buttons-and-accessibility/)
- [Links vs. Buttons in Modern Web Applications | MarcySutton.com](https://marcysutton.com/links-vs-buttons-in-modern-web-applications/)
- [A Bit on Buttons | CSS-Tricks](https://css-tricks.com/a-bit-on-buttons/)

Interactive elements use `button[type=button]` element or `role="button"`

Javascript use `<button type="button">` to interact with user clicks/actions.

> The only real reason you might have for using the button role is when progressively enhancing a link into a button using JavaScript; for example, to make the link open an overlay instead of a new page
— [How Our CSS Framework Helps Enforce Accessibility | eBay Tech Blog](http://www.ebaytechblog.com/2015/11/04/how-our-css-framework-helps-enforce-accessibility/)

- https://developer.mozilla.org/en-US/docs/Accessibility/ARIA/ARIA_Techniques/Using_the_button_role
- [Just use button -- A11ycasts #05 - YouTube](https://www.youtube.com/watch?v=CZGqnp06DnI)

## Object tag

- https://stackoverflow.com/questions/11199048/differences-between-the-html-tags-of-embed-object-and-video
- https://stackoverflow.com/questions/16660559/difference-between-iframe-embed-and-object-elements

> The object element can represent an external resource, which, depending on the type of the resource, will either be treated as an image, as a nested browsing context, or as an external resource to be processed by a plugin.

> Represents an integration point for an external(typically non-HTML) application or interactive content.
>
> The optional src attribute specifies the URL of the resource being embedded.
> 
> The optional type attribute specifies the MIME type of the plugin to instantiate. The value must be a valid MIME type, optionally with parameters. If both the type attribute and the src attribute are present, then the type attribute must specify the same MIME type as the explicit Content-Type metadata of the resource given by the src attribute.

Before HTML5:

- http://www.alistapart.com/articles/byebyeembed
- http://www.alistapart.com/d/byebyeembed/newwmv.html
- http://joliclic.free.fr/html/object-tag/en/index.php

If you want to interact with content from JS, use `contentDocument` (no crossdomain nor `postMessage`) or an iframe element and `contentWindow`

## `iframe`

Inline frame

Note: Sandbox Allow-scripts + allow-same-origin with a same origin url allows frame to remove its own sandbox and reload to escape the sandbox.

- [\<iframe\> - HTML | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)

Empty pages:

- No src `<iframe></iframe>`
- No value  `<iframe src></iframe>`
- Empty string as value `<iframe src=""></iframe>`

Acts similar to `about:blank`.

When `src` is omitted, `iframe.src` is empty.
When `src` is present but empty, `iframe.src` is parent url...

	<script>function doThings(){}</script>
	<iframe src="javascript:parent.doThings();'<a href=&quot;http://example.com?a=1&amp;b=2&quot;>Some HTML text</a>'"></iframe>

	<iframe src="javascript:'<a href=&quot;http://example.com?a=1&amp;amp;b=2&quot;>Some HTML text</a>'"></iframe>
	<!-- &, etc. need to be double encode as entity -->
	<!-- iframe.src == "about:srcdoc" -->

Is same as

	<iframe srcdoc="<p>Some HTML text</p>"></iframe>

- https://github.com/qfox/htmlday16/blob/master/htmlday2016.final.pdf

## Validator and tools

- [debugCSS : (X)HTML debugging tool built with CSS](http://yahoo.github.io/debugCSS/)
- [Css Accessibility Validator](http://elad2412.github.io/css-accessibility-validator/)
- [tota11y – an a11y visualization toolkit](http://khan.github.io/tota11y/)

## Common errors

Aka mistakes

Wrong:

	<meta http-equiv="refresh" content="0;http://foo.com">

Correct:

	<meta http-equiv="refresh" content="0;url=http://foo.com">

Wrong:

	<meta charset="utf8">

Correct:

	<meta charset="UTF-8">
	<meta charset="utf-8">

`UTF-8` is prefered, but `utf-8` works too. See [Media type - Charset case](Web#Charset case)

CDATA in HTML for script or style tags is not need in HTML5

See also [Avoiding common HTML5 mistakes | HTML5 Doctor](http://html5doctor.com/avoiding-common-html5-mistakes/)

## Implicites attributes

Implicit `role=""`: [3 Semantics, structure, and APIs of HTML documents — HTML5](http://www.w3.org/TR/html5/dom.html#sec-implicit-aria-semantics)

- [ARIA Implicit Roles (accessibility) | Foundation Forum from ZURB](http://foundation.zurb.com/forum/posts/18710-aria-implicit-roles-accessibility)
- [On HTML belts and ARIA braces (The Default Implicit ARIA semantics they didn’t want you to know about) | HTML5 Doctor](http://html5doctor.com/on-html-belts-and-aria-braces/)

## Favicon

	<link rel="icon" type="image/png" href="/favicon-32x32.png" sizes="32x32">
	<link rel="icon" type="image/png" href="/favicon-16x16.png" sizes="16x16">
	<link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">
	<link rel="manifest" href="/manifest.json">
	<link rel="mask-icon" href="/safari-pinned-tab.svg" color="#5bbad5">
	<meta name="theme-color" content="#ffffff">

See [Web](Web#Favicon)

## (depreciated) Conditional comment for IE

	<!--[if !IE]><!-->
	This is hidden from Internet Explorer.
	<!--<![endif]-->
	
	<!--[if IE 6]>
	Special instructions for IE 6 here
	<![endif]-->

http://www.quirksmode.org/css/condcom.html

## Data URI

See [Web#Data URI]

## Don't use `target="_blank"`

It's a security issue if the link is provided by user, in the target document `window.opener` is accessible and can change it `location`

- [When to use target="_blank" | CSS-Tricks](https://css-tricks.com/use-target_blank/)
- [Security # Link and `target="_blank"` or `window.open()`](Security#Link and `target="_blank"` or `window.open()`)

## Performance impact of images

Memory usage limit especially on low cpu/memory (like mobile):

- [iPad Safari image limit workaround - Rob LaPlaca](http://roblaplaca.com/blog/2010/05/05/ipad-safari-image-limit-workaround/)
- [Creating Compatible Web Content](https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariWebContent/CreatingContentforSafarioniPhone/CreatingContentforSafarioniPhone.html#//apple_ref/doc/uid/TP40006482-SW15)
- iPad 1 has a 4MB texture buffer (~5 1024×768 images)
- [What's the largest image size that the iOS browser display without downsampling? - Stack Overflow](https://stackoverflow.com/questions/5935785/whats-the-largest-image-size-that-the-ios-browser-display-without-downsampling/11864729#11864729)
- [ipad - Does Mobile Safari have an image file size limit? - Ask Different](http://apple.stackexchange.com/questions/17131/does-mobile-safari-have-an-image-file-size-limit/45848#45848)
- [javascript - Reading large images as thumbnails locally via HTML5 filereader - Stack Overflow](https://stackoverflow.com/questions/13905578/reading-large-images-as-thumbnails-locally-via-html5-filereader/14031674#14031674)

## Control layout with viewport meta

Small screen viewport size

	<meta name="viewport" content="width=device-width, initial-scale=1.0">

- **DO** use the viewport meta tag
- **DO** use media queries to render your page appropriately for various widths ranging from under 200px to 1024px or more
- **DO** use `width=device-width,initial-scale=1` in your viewport meta tag OR use `width=device-width` alone.
- **DO NOT** use `maximum-scale=1` nor `user-scalable=no`
- **DO NOT** use `width=<specific width>`
- **DO NOT** use `@media all and (device-width: <specific width>)`

- [Quick Tip: Never use maximum-scale=1.0 - The Accessibility Project](http://a11yproject.com/posts/never-use-maximum-scale/)
- http://tech.bluesmoon.info/2011/01/device-width-and-how-not-to-hate-your.html
- [Too many devs disable zoom on mobile. So we put "force enable zoom" in Opera](https://twitter.com/brucel/status/667647929889513472/photo/1)
- [Don’t Disable Zoom | Adrian Roselli](http://adrianroselli.com/2015/10/dont-disable-zoom.html)
- https://developer.mozilla.org/en-US/docs/Mozilla/Mobile/Viewport_meta_tag
- Apple changes in iOS9 https://twitter.com/awfulben/status/646382994496729088
- `user-scalable=no` is not more supported in iOS 10 [How to disable viewport scaling in iOS 10? You don't. - Wouter De Schuyter](https://wouterdeschuyter.be/blog/how-to-disable-viewport-scaling-in-ios-10-you-dont-941140811)
- [Proposal: devs SHOULD NOT use content="user-scalable=no | maximum-scale=1.0 " on meta · Issue #602 · w3c/html](https://github.com/w3c/html/issues/602)

## Attributes

### `alt` vs `title`

Note: [`title` attribute is not accessible](#`title` attribute is not accessible)

Alternative text is... the text version of image. Same information/data or summary, but with words. Ex.: "WordPress awesomeness has increased from 90% awesome in 2006, to 120% awesome in 2008".
Caption describe the meaning the image. Ex.: "WordPress awesomeness by time, based on data from the WordPress Awesomeness Institute"

Alt is not only for accessibility purpose, but also for SEO: [HTeuMeuLeu on Twitter: "Rappel : l'attribut alt, ça ne sert pas qu'aux lecteurs d'écrans. http://t.co/yZKY5FYLMQ"](https://twitter.com/HTeuMeuLeu/status/582470239201439744/photo/1)

- http://www.w3.org/TR/html5/embedded-content-0.html#alt
- http://www.w3.org/TR/WCAG20/#text-altdef
- http://www.w3.org/WAI/alt/

### Quotes

	<div class='container'></div>

	<div class=container></div>

	<div class="container"></div>

	<input type="checkox" checked>

	<input type="checkox" checked="checked">

Should use double quotes.

## Classname and ID

> It may require a bit more analysis, but it is always better to think of class names that represent the meaning/function of the specific element(s) rather than what happens to be their current presentation. That way when their presentation changes (as it inevitably does), or alternative presentations are designed for additional media types or devices, you avoid such confusing style rules like: `.black { color:navy; }`
— [Tantek, 2004](http://meyerweb.com/eric/thoughts/2004/07/18/competent-classing/#comment-529)

See [Common issues](Web#Common issues) about limitation adblocks order.
See also [Development](Development#Naming)

### IDs for robots

IDs could be used, but (could be) often changed by frontend developers. Instead use a dedicated data attribute, like `<button data-test-role="delete-comment" type="button">Delete comment</button>`

- [Software Testing Article - Data-QA Attribute! A better way to select elements for UI test automation](https://www.utest.com/articles/data-qa-attribute-a-better-way-to-select-elements-for-ui-test-automation)
- [Best Practices | Cypress Documentation](https://docs.cypress.io/guides/references/best-practices.html#Selecting-Elements)
- [selenium - Test automation html element selectors. Element ID or DataAttribute - Stack Overflow](https://stackoverflow.com/questions/37492803/test-automation-html-element-selectors-element-id-or-dataattribute)
- [Using "data-test" in Tests](http://blog.rstankov.com/using-rel-in-testing/)
- [Making your UI tests resilient to change – kentcdodds](https://blog.kentcdodds.com/making-your-ui-tests-resilient-to-change-d37a6ee37269)

### Validity of CSS class names and ids

**Double hyphen within the comment `--` is perceived as part of the comment and therefore its presence lead to error during document validation.** See [8 The HTML syntax — HTML5](https://www.w3.org/TR/html5/syntax.html#comments)

- https://stackoverflow.com/questions/448981/what-characters-are-valid-in-css-class-selectors
- [CSS character escape sequences · Mathias Bynens](https://mathiasbynens.be/notes/css-escapes)
- http://www.w3.org/TR/CSS21/grammar.html#scanner
- [Don't be stupid](https://mathiasbynens.be/demo/crazy-class)
- [Class and ID to avoid because of AdBlock](https://gist.github.com/spyesx/42fe84c0ef757d1c38a4) and https://github.com/easylist/easylist (IDs start with `###`, classes start with `##.`)
	- https://hg.adblockplus.org/easylist/
	- https://hg.adblockplus.org/easylist.adblockplus.org/
	- https://hg.adblockplus.org/easylistchina/
	- https://hg.adblockplus.org/easylistcombinations/
	- https://hg.adblockplus.org/easylistdutch/
	- https://hg.adblockplus.org/easylistgermany/
	- https://hg.adblockplus.org/easylistitaly/
	- https://hg.adblockplus.org/easylistspanish/
	- https://github.com/reek/anti-adblock-killer/

### Semantic name

- [Leveling up in CSS — Free Code Camp](https://medium.freecodecamp.com/leveling-up-css-44b5045a2667#ee22)
- [What Makes For a Semantic Class Name? | CSS-Tricks](https://css-tricks.com/semantic-class-names/)
- [Naming CSS Stuff Is Really Hard | Sparkbox | Web Design and Development](https://seesparkbox.com/foundry/naming_css_stuff_is_really_hard)
- [Naming Things ◆ 24 ways](https://24ways.org/2014/naming-things/)
- [Semantics and sensibility – CSS Wizardry – CSS, OOCSS, front-end architecture, performance and more, by Harry Roberts](http://csswizardry.com/2010/08/semantics-and-sensibility/)
- [About HTML semantics and front-end architecture – Nicolas Gallagher](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/)
- [What's in a Name? Anti-Patterns to a Hard Problem](http://www.sitepoint.com/whats-in-a-name-anti-patterns-to-a-hard-problem/)
- [The id attribute got more classy in HTML5 · Mathias Bynens](https://mathiasbynens.be/notes/html5-id-class)
- [The problem with atomic CSS – Simple = Human – Medium](https://medium.com/simple-human/the-problem-with-atomic-css-d0c09c7aa38e)
- [Yahoo reinvented inline styles through classes | Hacker News](https://news.ycombinator.com/item?id=14833630)

Who never saw that?

	.homepage-promos .grid-50 {width: 100%}
	.homepage-promos .grid-33 {width: 100%}
	.homepage-promos .grid-34 {width: 100%}
	#seo-container {display: none;}
	.cover.black {background-color: white;}
	<a class="padding-left-20 red" href="#"></a>
	<a class="P(20px)" href="#"></a>

> Name something based on what it is, not how it looks
> [..]
> styles change based on states
> [..]
> If you’re going to do `<div class="red">` you may as well do `<div style="color: red">`
— [MaintainableCSS - an approach to writing modular, scalable and maintainable CSS | By Adam Silver](http://maintainablecss.com/)

	<div class="stream">
	  <div class="streamItem">
	    <article class="postArticle">
	      <div class="postArticle-content">
	        <!-- content -->
	      </div>
	    </article>
	  </div>
	</div>

Component/template/object-oriented class name could be ideal, but semantic don't change over responsive where the presentation does. Ex.: a desktop carrousel, displayed as a list of images on smallscreens

- [MaintainableCSS - an approach to writing modular, scalable and maintainable CSS | By Adam Silver](http://maintainablecss.com/) and the joke https://github.com/marmelab/universal.css
- [Thoughts on semantic HTML class names and maintainability – Brett Jankord – Front-End Software Engineer](http://brettjankord.com/2013/02/09/thoughts-on-semantic-html-class-names-and-maintainability/)
- [More thoughts on HTML class naming conventions. – Brett Jankord – Front-End Software Engineer](http://brettjankord.com/2013/03/06/more-thoughts-on-html-class-naming-conventions/)
- [About HTML semantics and front-end architecture – Nicolas Gallagher](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/)
- [bjankord/CSS-Components-Modifiers-And-Subcomponents-Collection](https://github.com/bjankord/CSS-Components-Modifiers-And-Subcomponents-Collection)
- [MindBEMding – getting your head ’round BEM syntax – CSS Wizardry – CSS, OOCSS, front-end architecture, performance and more, by Harry Roberts](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)
- https://github.com/sturobson/BEM-resources
- [Question about naming items with BEM and CSS : Frontend](https://www.reddit.com/r/Frontend/comments/2z437s/question_about_naming_items_with_bem_and_css/)
- [BEM — FAQ](http://getbem.com/faq/)
- [Semantic HTML — Wikipedia](https://en.wikipedia.org/wiki/Semantic_HTML#Considerations)
- [Use class with semantics in mind - Quality Web Tips](http://www.w3.org/QA/Tips/goodclassnames)
- [BEM 101 | CSS-Tricks](https://css-tricks.com/bem-101/)
- [Battling BEM (Extended Edition): 10 Common Problems And How To Avoid Them – Smashing Magazine](https://www.smashingmagazine.com/2016/06/battling-bem-extended-edition-common-problems-and-how-to-avoid-them/)
- [Leveling up in CSS — Free Code Camp](https://medium.freecodecamp.com/leveling-up-css-44b5045a2667#)
- [Grandchild elements in BEM | Assortment - For the practical developer](https://assortment.io/posts/grandchild-elements-bem-css)

### Inspiration

- [Foobar — Wikipedia](https://en.wikipedia.org/wiki/Foobar)
- http://www.schema.org/docs/full.html
- http://thesaurus.com/browse/
- http://seesparkbox.com/foundry/naming_css_stuff_is_really_hard
- [Abbreviations.com](http://www.abbreviations.com/)
- [All Acronyms Dictionary](http://www.allacronyms.com/)
- [List of glossing abbreviations — Wikipedia](https://en.wikipedia.org/wiki/List_of_glossing_abbreviations)
- http://en.wikibooks.org/wiki/LaTeX/Document_Structure
- [hcard-input-formats · Microformats Wiki](http://microformats.org/wiki/hcard-input-formats)
- [Full Hierarchy - schema.org](http://schema.org/docs/full.html)
- [word choice - Looking for the most common abbreviation to indicate the end of a working day - English Language & Usage Stack Exchange](http://english.stackexchange.com/questions/137458/looking-for-the-most-common-abbreviation-to-indicate-the-end-of-a-working-day)
- Rules: [Variables: The Backbone Of CSS Architecture – Smashing Magazine](https://www.smashingmagazine.com/2016/01/variables-in-css-architecture/#variables-nomenclature)

#### Triage

From [C# Controls abbreviation](https://gist.github.com/andyyou/3052671) and [abbreviation of controls](https://social.msdn.microsoft.com/forums/windows/en-us/9f1cda78-930e-48f8-bd88-e0cfc0190ab5/abbreviation-of-controls):

	AdRotator / ar
	BackgroundWorker / bgw
	BindingNavigator / bdn
	BindingSource / bds
	Button / btn
	Calender / cal
	CheckBox / cb
	CheckBox / chk
	CheckBoxList / cbl / chklst
	CheckedListBox / ckl
	ColorDialog / cld
	Column (DataGridView的) / col
	ColumnHeader (ListView 的) / ch
	Combobox / cbo / cmb
	CompareValidator / cv
	ContextMenuStrip / cms
	CrystalReportViewer / crv / rptvew
	DataGrid / dg
	DataGridView / dgv
	DataList / dl
	DataSet / dts
	DateTimePicker / dtp
	DirectoryEntry / dre
	DirectorySearcher / drs
	DomainUpDown / dud
	DropDownList / dd / ddl
	ErrorProvider / err
	EventLog / evl
	FileSystemWatcher / fsw
	FileUpload / ful
	FlowLayoutPanel / flp
	FolderBrowserDialog / fbd
	FontDialog / fnd
	Form / frm
	GridView / gv
	GroupBox / grp
	HelpProvider / hlp
	HiddenField / hf
	HScrollBar / hsc
	Hyperlink / hl
	Image / img
	ImageButton / ib / imgbtn
	ImageList / il / img
	Label / lbl
	LinkButton / lbtn / lnkbtn
	LinkLabel / llb
	ListBox / lb / lst
	ListView / lv / lvw
	Literal / lit
	MaskedTextBox / mtx
	MenuStrip / mns / ms
	MessageQueue / msq
	MonthCalendar / cdr
	NotifyIcon / icn
	NumeircUpDown / nud
	ObjectDataSource / ods
	OpenFileDialog / ofd
	PagedDataSource / pds
	PageSetupDialog / psd
	Panel / pnl
	PerformanceCounter / pfc
	PictureBox / pic
	PlaceHolder / ph
	PrintDialog / prd
	PrintDocument / pdc
	PrintPreviewControl / prv
	PrintPreviewDialog / ppd
	Process / prc
	ProgressBar / prg
	PropertyGrid / prg
	RadioButton / rb / rdo
	RadioButtonList / rbl / rdolst
	RangeValidator / rv
	RegularExpressionValidator / rev
	Repeater / rpt
	ReportDocument / rpd
	ReportViewer / rpv
	RequiredFieldValidator / rfv
	RichTextBox / rtx
	SaveFileDialog / sfd
	SerialPort / spt
	ServiceController / scl
	SplitContainer / spl
	Splitter / spl
	StatusLabel / slbl
	StatusStrip / ss / ssr
	TabControl / tab
	Table / tbl
	TableLayoutPanel / tlp
	TabPage / tp
	Textbox / tb / txt
	Timer / tmr
	ToolStrip / ts / tsr
	ToolStripButton / tsbtn
	ToolStripContainer / tsc
	ToolStripDropDownButton / tsddb
	ToolStripLabel / tslbl
	ToolStripMenuItem / tsmi
	ToolTip / tip
	TrackBar / trb
	TreeView / tv / tvw
	ValidatorSummary / vs
	VScrollBar / vsc
	WebBrowser / wbs

And from [What are the naming guidelines for ASP.NET controls? - Stack Overflow](https://stackoverflow.com/questions/181597/what-are-the-naming-guidelines-for-asp-net-controls/25086425#25086425):

	STANDARD CONTROLS:
	btn Button
	cb CheckBox
	cbl CheckBoxList
	ddl DropDownList
	fu FileUpload
	hdn HiddenField
	lnk Hyperlink
	img Image
	ibtn(btn) ImageButton
	lbl Label
	lbtn(btn) LinkButton
	lb ListBox
	lit Literal
	mv MultiView
	pnl Panel
	ph PlaceHolder
	rb RadioButton
	rbl RadioButtonList
	tbl Table
	txt TextBox
	v View
	
	DATA CONTROLS
	dtl DataList
	dp DataPager
	dtv DetailsView
	ets EntityDataSource
	fv FormView
	gv GridView
	lds LinqDataSource
	lv - ListView
	ods ObjectDataSource
	qe QueryExtender
	rpt Repeater
	smd SiteMapDataSource
	sds SqlDataSource
	xds XmlDataSource
	
	VALIDATION CONTROLS
	cpv CompareValidator
	ctv CustomValidator
	rv RangeValidator
	rev RegularExpressionValidator
	rfv RequiredFieldValidator
	vs ValidationSummary
	
	VALIDATION CONTROLS:
	cpv // CompareValidator
	ctv CustomValidator
	rv RangeValidator
	rev RegularExpressionValidator
	rfv RequiredFieldValidator

Sequences: 

1. intro
2. bridge
3. hero
4. standard
5. outro
 
	.some-module {}
	.some-module__sub-compontent {}
	.some-module--modifier {}
	.some-module--modifier .some-module__sub-compontent{}
	.some-module:first-child .some-module__sub-compontent{}
	.some-module__sub-compontent--modifier {}

	.person{}
	.person__hand{}
	.person--female{}
	.person--female__hand{}
	.person__hand--left{}

### Categories

How to: [The Roles Model | Accessible Rich Internet Applications (WAI-ARIA) 1.0](https://www.w3.org/WAI/PF/aria/roles#roles_categorization)

#### General

- caption
- detail
- summary, overview
- preview
- details
- description / desc
- drop cap / initial cap (usally selected with CSS selector `::first-letter`) (see http://en.wikipedia.org/wiki/Initial)
- category
- legal
- featured
- location
- password / pwd
- list, enumeration / enum, index
- list-item
- group, set
- collection
- keypoints
- keypoint, strong point
- keyfacts
- key figures / kf
- keyword / kword / kd / kw
- legend / leg
- tag
- terms
- conditions
- road map
- thesis / report
- literature (published work on a subject) / documentation
- recommendation
- review
- testimonials
- related
- bounds / boundary
- strip
- poster
- thumb
- decoration
- about*
- the-rest
- explanation
- dummy

#### Structure

- section
- body
- page
- content / cnt
- container / cntr / ctr / cont
- header
- footer
- landmark
- wrapper / wrp / wrap
- bit, piece, chunk, slice, snippet, part
- section, component
- progress tracker, progress indicator, stepper (number of steps in order to complete a specified process, for wizard. ex: order steps `shipping > billing > confirm order`)
- breadcrumb (list) / bc (fil d'ariane)
- fieldset / fset
- pagination / pag
- relationship / relation
- leading / trailing / head / tail
- divider / separator
- stack
- step
- dispatch / compass / boussole: language and/or region selector, 404 page with main links.
- interstitial (user age selector, language and/or region selector, full screen ads) [Interstitial webpage — Wikipedia](https://en.wikipedia.org/wiki/Interstitial_webpage) [Interstitial Ads  |  Mobile Ads SDK for Android  |  Google Developers](https://developers.google.com/ad-manager/mobile-ads-sdk/android/interstitial)
- aside
- stage
- (main)

#### Application

UI

- notice
- alert
- command hierarchy / cmd hrchy or menu hierarchy (in docs, like `File > Save`. See [Hierarchy](Text#Hierarchy))
- bookmark / bm
- notification
- message / msg
- success
- placeholder
- inlays (incrustation) / expands
- modal or transient [Transient screen — Wikipedia](https://en.wikipedia.org/wiki/Transient_screen)
- more / discover (go further)
- hint (role=alert), clue, tip, infotip (tooltip)
- chart
- gimmick
- push (promote the use, sale, or acceptance of; to advertise, publicize, promote) / focus
- (graphical) disclosure (for toggled hidden/visible, reveal content)
- (graphical) banner / [hero image](https://en.wikipedia.org/wiki/Hero_image)
- (graphical) hero content / grid (see hero image)
- (graphical) ticker
- (graphical) polygon / plyg

Widgets

- caret (arrow down for select)
- toggle / tgl (button)
- action (buttons: submit and button, link / lnk, context menu items)
- textfield / tf
- primary button (Positive: ‘Send’ or ‘Submit’, Negative: ‘Replace’ or ‘Delete’), secondary button (‘Cancel’)

Function / action:

- newsletter / nl / subscribe
- share / social
- interaction, connect, request
- submit
- register
- (go to the) next
- (go to the) previous

- (js) observer / obs
- (js) context / ctx
- (js) complex / cx / cmplx
- (js) controller / cntlr
- (data) slug

#### Document

webpage, text, image, video, map

- title
- [headline](http://en.wiktionary.org/wiki/headline) (main title, title of main article)
- introduction / intro, summary line / brief paragraph (above or below the headline, often in the `<header>`)
- [lead paragraph](https://en.wikipedia.org/wiki/Lead_paragraph) / lead / lede (chapeau, opening paragraph of an article, essay, news story or chapter after the headline or title, often in the `<header>`, answers to the questions of Five Ws: "who, what, why, when, where, and how")
- tagline (slogan)
- strapline (advertising: slogan attached to a brand name), a subsidiary heading or caption in a newspaper or magazine. A secondary heading, especially one printed above another
- catchphrase / catch, teaser (accorche, kind of introduction)
- document
- [excerpt](http://en.wiktionary.org/wiki/excerpt) ("a short extract from a film, broadcast, or piece of music or writing")
- toc/table of content (TOC) https://en.wikipedia.org/wiki/Table_of_contents (use `role="directory"`)
- abstract
- main / body
- conclusion
- guideline
- topic
- overview
- quote
- summary
- metadata, meta (can use `dl`)
- caption
- note
- annex
- chapter
- material
- subheader (sous-titre)
- marker (marque, balise, repère, jalon)
- author
- toc/table of content (TOC) https://en.wikipedia.org/wiki/Table_of_contents (use `role="directory"`)
- colophon (about the document / website): author, co-authors, publishing date, editors, used softwares, etc.
	> about the publication of a book such as the place of publication, the publisher, and the date of publication
	— [Colophon (publishing) — Wikipedia](https://en.wikipedia.org/wiki/Colophon_(publishing))
	
	See also:
	
	* [Paratexte — Wikipédia](https://fr.wikipedia.org/wiki/Paratexte)
	* [Colophon - The Web Standards Project](http://www.webstandards.org/about/colophon/)
- lead-article
- amend (in conjonction with `ins` element)
- timing
- copyright / copy, disclaimer, license, statement

#### Text

- conjunction / CONJ / CNJ (and, or, nor)
- adp (adposition: preposition/postposition)
- unit

#### Product

- name
- sku http://en.wikipedia.org/wiki/Stock_keeping_unit
- set (kit, collection)
- range, product-range (gamme)
- product-line (ligne de produit)
- variations, variant (of product)
- product-mix (line: width, length, depth, consistency) https://en.wikipedia.org/wiki/Product_lining#Related_jargon http://smallbusiness.chron.com/product-mix-639.html
- attributes (product details)
- price
- tier prices (quantity discount)
- brand
- manufacturer / mfr / mfg, manufacture / mfr, manufacturing / mfg
- all-in-one / aio
- scope of supply (ensemble des composants / ensemble des fournitures) [scope of supply - English-French Dictionary WordReference.com](http://www.wordreference.com/enfr/scope%20of%20supply)
- components
- sector
- feature
- issue

#### E-commerce & services

- offer (coupon) (use `aside` or `footer`?) (or as offer page to choose pricing plan/table) 
- supply
- gift/discount voucher (coupon/bon de réduction)
- digital distribution platform (itunes, app store, google play, windows phone store, etc.)
- partner
- [Shopping] cart (US), [Shopping] basket (UK) http://english.stackexchange.com/questions/29356/shopping-basket-or-shopping-cart
- store
- sponsors / advertisers
- call you back / cub
- promotion, advertising / advert / ad

#### Recipe

- title
- ingredient / ingrd
- instructions / instr (préparation)
- prerequisite

#### People

- bio
- first name
- middle name
- last name
- title http://en.wikipedia.org/wiki/Title http://fr.wikipedia.org/wiki/Titre_de_civilit%C3%A9

#### Others

See [Development](Development#Few words)

#### Modifier / States / Actions (provided as information, usefull for JS)

- spotlighted, highlight/highlighted, emphasize/emphasized, target/targeted (only for one fragment / main / large content, corresponds to [`:target`](https://developer.mozilla.org/en-US/docs/Web/CSS/:target) pseudo class. Could have a specific hash), stress, underline, focus attention on, draw attention to, spotlight...
	If it's just text (highlighted in yello), use [`<mark>`](#`mark` element)
- set back/unhighlight
- show/visible, shown, open - close
- hide/hidden
- untarget
- active - inactive (activate - desactivate/inactivate)
- collapse/collapsed/unexpanded/folded - expand/expanded/uncollapse/unfolded (toggle between both states, see disclosure)
- focus
- spotlight
- alternative / alt
- required / rqrd
- previous / prev, next
- pristine (interacted with), default (default or changed + reset), dirty, changed, touched (has been blurred), untouched (hasn't been blurred)
- success, error
- disabled

Animations:

- wobble

#### Form

Some field/control names are reserved for an other purpose, by the backend or as search parameter (query string)

- label / lbl
- (form) field / control / widget
- civility (title of, mr mrs ms) / honorific prefix
	* [Honorific - Wikipedia, the free encyclopedia](http://en.wikipedia.org/wiki/Honorific)
- http://drafts.htmlwg.org/html/master/forms.html#inappropriate-for-the-control
	Also:
	* "home", meaning the field/control is for contacting someone at their residence
	* "work", meaning the field/control is for contacting someone at their workplace
	* "mobile", meaning the field/control is for contacting someone regardless of location
	* "fax", meaning the field/control describes a fax machine's contact details
	* "pager", meaning the field/control describes a pager's or beeper's contact details
	
	Family name + First name or Single name (mononym)
- [HTML Standard - 4.10.19.8 Autofill](https://html.spec.whatwg.org/multipage/forms.html#autofill)
- [Field Specifications for E-Commerce v1.1](http://www.ietf.org/rfc/rfc3106.txt)
- [html - Form field names used by personal data auto-fill in browsers (Safari, Opera) - Stack Overflow](https://stackoverflow.com/questions/1027462/form-field-names-used-by-personal-data-auto-fill-in-browsers-safari-opera)
- [Is there a naming convention for HTML form fields for good auto completion across all modern browsers? - Stack Overflow](https://stackoverflow.com/questions/6365395/is-there-a-naming-convention-for-html-form-fields-for-good-auto-completion-acros)
- [RFC 2706 - ECML v1: Field Names for E-Commerce](http://tools.ietf.org/html/rfc2706)
- [RFC 3106 - ECML v1.1: Field Specifications for E-Commerce](http://tools.ietf.org/html/rfc3106)
- [RFC 4112 - Electronic Commerce Modeling Language (ECML) Version 2 Specification](http://tools.ietf.org/html/rfc4112)
- https://stackoverflow.com/questions/6365395/is-there-a-naming-convention-for-html-form-fields-for-good-auto-completion-acros
- Wordpress use `name` as a default query parameter, use something like `first_name` or `fullname`: http://contactform7.com/faq/are-there-any-reserved-or-unavailable-words-for-the-name-of-an-input-field/

### JavaScript selectors

Use data attribute `[data-slideshow]` or classname `.js-slideshow`

## Escape chars

- [Using character escapes in markup and CSS](https://www.w3.org/International/questions/qa-escapes#cssescapes)

## DOM Clobbering

Some `name` attribute can override element's properties (like `name`, `attributes`, `childNodes`, etc.)

See [DOM Clobbering](JavaScript#DOM Clobbering)

## Entities and emoji

and symbols

Sometimes it's better to use image or svg instead

- [Symbols](Text#Symbols)
- [You, Me And The Emoji: Character Sets, Encoding And Emoji – Smashing Magazine](https://www.smashingmagazine.com/2016/11/character-sets-encoding-emoji/)
- [Emoji on the Web – Making Faces (and Other Emoji) – Medium](https://medium.com/making-faces-and-other-emoji/emoji-on-the-web-537c5769dffa)

# Accessibility

Aka a11y

![Persona Spectrum - Inclusive, A Microsoft Design Toolkit](Persona%20Spectrum.png)

> Attention to detail is important. Especially where a11y is concerned.

> Programmers program for the person they know best
— Jim Allen

> Accessibility techniques don’t just benefit disabled users either — for example:
> - Pages that are more accessible to screen readers are also more accessible to search engine algorithms. Simple accessibility techniques such as using alt-text on images, using descriptive text in links, using CSS for style only (never for meaning), and using HTML5’s semantic tags improve the overall SEO of a page.
> - Transcripts of video content aren’t just good for people with auditory impairments — they are also useful for users on mobile devices in low bandwidth areas that can’t download the video, and people in noisy environments that can’t hear the video. And more text content means more opportunity for relevant keywords, so again, more SEO.
— https://hacks.mozilla.org/2016/07/make-the-web-work-for-everyone/

> Valid HTML isn't always accessible

- `lang` attribute should match the actual content language, else the screen reader's interpretation will be incomprehensible (`lang` attribute is also used by CSS for `hyphens`, quotes, etc.)
- VoiceOver don't handle elements with `width: 0; height: 0;`
- images `alt` attribute with null value (`alt=""`) are usally ignored. AT assume it is for decorative purposes.
- avoid usage of line return for `alt` value: [Short note on coding alt text | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](http://www.paciellogroup.com/blog/2015/09/short-note-on-coding-alt-text/) 
- duplicate content should be avoided. **Don't** Ex: `<a href="register.html"><img src="register.png" alt="Register">Register</a>`, image `alt` should null (else AT show : "Register, Register link")
	or use `aria-hidden="true"` in conjonction with `role="presentation"`. But with an image, using CSS is recommended
- using `role=button` can be sometimes irrevelant (for example if the node is an heading level. http://heydonworks.com/practical_aria_examples/#comment-1178134652). A child element is required to fix that.
- > `role="presentation"` tells screen readers that the semantics of an element are inaccurate and should be ignored (useful in situations where you’re unable to change the element’s type to `<div>`).
	> `aria-hidden="true"` completely hides an element from screen readers (useful for e.g. decorative SVG icons).
	— [The Accessibility Difference Between Aria-hidden and role="presentation"](http://csskarma.com/blog/difference-rolepresentation-aria-hiddentrue/)
	
	> If you feel a need to do `<nav role="presentation">` or `<header role="presentation">` or `<article role="presentation">` **use `<div>` instead**
	— https://twitter.com/stevefaulkner/status/798835014670512128
- **DONT:** Remove focus outline, underline, and no diff color for links (people with parkinson are unable to use the website, hovering over text to find the links is difficult with this condition)
- > Links without href attributes are cannot be focused. It's a [placeholder hyperlink](#placeholder hyperlink)
- > An overkill of web animations and parallaxing can make people physically sick. Be kind to your users.
	* https://twitter.com/zeldman/status/492805247455072256
- > Animation can be a useful tool to make a focus state more obvious and at the same time easier on the eyes.
- HTML tags are for semantic. `role` and other aria attributes are for interactions description
- role attribute force elements for be exposed to AT. See who to [hide an element to assistive technologies](CSS#Hide an element to assistive technologies)
- > don't replace a native control with a scripted one that doesn't retain the same semantics
	Example using select2 where selected item is not announced
	* [Custom UI Widget Accessibility Problems - YouTube](https://www.youtube.com/watch?v=mydQJjf981g)
	* [Accessibility Usertest: Select2 – Make WordPress Accessible](https://make.wordpress.org/accessibility/2015/09/07/accessibility-usertest-select2/)
	* https://github.com/select2/select2/search?q=accessibility&type=Issues&utf8=%E2%9C%93
- question mark key should open keyboard shortcut help (see Twitter)

- [Accessibility according to actual people with disabilities - Axess Lab](https://axesslab.com/accessibility-according-to-pwd/) - First issue: media captions
- [Web Accessibility Perspectives Videos: Explore the Impact and Benefits for Everyone](https://www.w3.org/WAI/perspectives/)

> build a ramp instead of a staircase
— [The Veil of Ignorance](http://mrmrs.io/writing/2016/03/23/the-veil-of-ignorance/)

See [Color contrast](UI - UX#Color contrast)

Tools:

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

Examples (pattern, components):

- [WAI-ARIA Authoring Practices 1.1](https://www.w3.org/TR/wai-aria-practices-1.1/)
- [Accessibility Wins, curated by Marcy Sutton](http://a11ywins.tumblr.com/)
- [Accessibility section - jQuery Plugins - By Nicolas Hoffmann](http://a11y.nicolas-hoffmann.net/)
- [Web Components punch list | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](http://www.paciellogroup.com/blog/2014/09/web-components-punch-list/)
- Examples and docs: [The Accessibility Project](http://a11yproject.com/)
- [Patterns - The Accessibility Project](http://a11yproject.com/patterns/) - The A11Y Project patterns
- [Practical ARIA Examples](http://heydonworks.com/practical_aria_examples/)
- [3needs: WAI-ARIA techniques with code examples](http://3needs.org/en/testing/sr-aria.html)
- https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Test_Cases#Spinner_2
- [Aria Examples](http://accessibility.athena-ict.com/aria/aria-examples-index.shtml)
- [WAI-ARIA 1.0 Authoring Practices](http://www.w3.org/TR/wai-aria-practices/)
- [OpenAjax Accessibility: OpenAjax Examples](http://oaa-accessibility.org/)
- [IT Accessibility Handbook – IT Accessibility](https://accessibility.oit.ncsu.edu/it-accessibility-at-nc-state/developers/accessibility-handbook/)
- [Accessible jQuery-ui Components Demo](http://hanshillen.github.io/jqtest/) and [hanshillen/aegisdemo](https://github.com/hanshillen/aegisdemo)
- [Design patterns](http://ljwatson.github.io/design-patterns/)
- [Aria Examples](http://accessibility.athena-ict.com/aria/aria-examples-index.shtml)
- [Creating an Accessible ARIA Tree Control - SSB BART Group](http://www.ssbbartgroup.com/blog/creating-an-accessible-aria-tree-control/)
- [Illinois Center for Information Technology Accessibility: ARIA Examples](http://test.cita.illinois.edu/aria/)
- [Adactio: Journal—Accessible progressive disclosure revisited](https://adactio.com/journal/10475)
- [eBay MIND Patterns - Accessibility Patterns for the Web](http://ianmcburnie.github.io/mindpatterns/index.html) - see https://github.com/ianmcburnie/mindpatterns and [eBay MIND Patterns · GitBook](https://www.gitbook.com/book/ebay/mindpatterns/details)
- [aria-current design patterns](https://ljwatson.github.io/design-patterns/aria-current/)
- [Frend — A collection of accessible, modern front-end components.](https://frend.co/)
- [Accessible UI Components List – Frameworks, Snippets, Themes, and Widgets for a Better Web](https://www.w3.org/blog/wai-components-gallery/)
- [w3c/aria-practices: WAI-ARIA Authoring Practices, maintained by ARIA WG https://www.w3.org/WAI/ARIA/](https://github.com/w3c/aria-practices)
- [Inclusive Components](http://inclusive-components.club/)
- [Shopify Polaris](https://polaris.shopify.com/components/get-started)
- [Category:ARIA Techniques - WCAG WG](https://www.w3.org/WAI/GL/wiki/Category:ARIA_Techniques)
- [Enter The Dragon (Drop): Accessible List Reordering — Smashing Magazine](https://www.smashingmagazine.com/2018/01/dragon-drop-accessible-list-reordering/)

Others (doc, about, etc.):

- See also [Input-Controlled Web Design](#Input-Controlled Web Design)
- See also [SVG](SVG#Accessibility)

- [Tips for making accessibility a core design principle](https://pixelpioneers.co/blog/2017/13-expert-tips-accessibility)
- [Notes on ARIA by Taylor Hunt on CodePen](https://codepen.io/tigt/post/notes-on-aria)
- [9 tips to get bare minimum of web accessibility – Abhijeet Kumar – Medium](https://medium.com/@realabhijeet4u/9-tips-to-get-bare-minimum-of-web-accessibility-739899a9437c)
- [WebAIM: Keyboard Accessibility](http://webaim.org/techniques/keyboard/)
- [List of awesome accessibility resources](https://github.com/brunopulis/awesome-a11y)
- [Web Accessibility - Test Your Site for Accessibility](https://www.webaccessibility.com/best_practices.php)
- [Inclusive - Microsoft Design](https://www.microsoft.com/en-us/design/inclusive)
- [The web accessibility basics - Marco's Accessibility Blog](https://www.marcozehe.de/2015/12/14/the-web-accessibility-basics/)
- https://github.com/GoogleChrome/accessibility-developer-tools/wiki/Audit-Rules
- [The ARIA Role Conformance Matrices](http://whatsock.com/training/matrices/)
- [Responses To The Screen Reader Strategy Survey | HeydonWorks](http://www.heydonworks.com/article/responses-to-the-screen-reader-strategy-survey)
- [Building better accessibility primitives](http://robdodson.me/building-better-accessibility-primitives/)
- [Web Accessibility | Udacity](https://www.udacity.com/course/web-accessibility--ud891)
- [Accessible Charts | amCharts](https://www.amcharts.com/accessible-charts/)
- [Danger! Testing Accessibility with real people — Medium](https://medium.com/@LeonieWatson/danger-testing-accessibility-with-real-people-4515f72db648)
- [a11yTips — Overview](http://dboudreau.tumblr.com/overview)
- [Carousels and slideshows: accessibility for developers | Access iQ](http://www.accessiq.org/create/content/carousels-and-slideshows-accessibility-for-developers)
- [Category:AriaBestPractices - W3C Wiki](http://www.w3.org/wiki/Category:AriaBestPractices)
- [Accessibility | Marco's Accessibility Blog](https://www.marcozehe.de/category/accessibility/)
- [Blog | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](https://www.paciellogroup.com/blog/)
- [Notes on ARIA by Taylor Hunt on CodePen](https://codepen.io/tigt/blog/notes-on-aria)
- [The Accessibility Cheatsheet | bitsofcode](http://bitsofco.de/2015/the-accessibility-cheatsheet/)
- [How to Meet WCAG 2.0](https://www.w3.org/WAI/WCAG20/quickref/)
- [How to Create More Accessible Content, Part 2: Media | Viget](https://www.viget.com/articles/how-to-create-more-accessible-content-part-2)
- https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/widgets/overview
- https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques
- [Web Content Accessibility Guidelines (WCAG) 2.0](http://www.w3.org/TR/WCAG20/)
- [Techniques for WCAG 2.0](http://www.w3.org/TR/WCAG20-TECHS/)
- [Accessibility - Learn web development | MDN](https://developer.mozilla.org/en-US/docs/Learn/Accessibility)
- http://www.nczonline.net/blog/tag/accessibility/
- [Introduction to Web Accessibility - Course](https://webaccessibility.withgoogle.com/course)
- "Prefer make website accessible rather than a full support of IE8" https://twitter.com/rikschennink/status/520521059884617728 https://twitter.com/rikschennink/status/521718069052596224
- http://alistapart.com/article/accessibility-the-missing-ingredient
- https://www.ssbbartgroup.com/blog/2014/06/05/how-not-to-misuse-aria-states-properties-and-roles/
- http://rawgithub.com/w3c/aria-in-html/master/index.html
- http://www.w3.org/TR/html5/dom.html#index-aria-global
- http://rawgithub.com/w3c/html-api-map/master/index.html#h2_html-element-to-accessibility-api-role-mapping-matrix
- [HTML5 accessibility - work in progress November 2014](http://www.html5accessibility.com/)
- [Mobile Accessibility: How WCAG 2.0 and Other W3C/WAI Guidelines Apply to Mobile](http://www.w3.org/TR/mobile-accessibility-mapping/)
- http://blog.atalan.fr/support-des-attributs-aria-par-les-lecteurs-decran/
- https://github.com/aaronshaf/web-development/blob/master/aria.md
- http://www.w3.org/TR/wai-aria/states_and_properties
- [a11y.css](http://ffoodd.github.io/a11y.css/)
- [WebAIM: Articles](http://webaim.org/articles/#html)
- [Patterns for accessible webchats | Accessibility](https://accessibility.blog.gov.uk/2016/12/09/patterns-for-accessible-webchats/)
- [CSS outline property - outline: none and outline: 0](http://outlinenone.com/)
- [how to remove CSS outlines in an accessible manner? | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](http://www.paciellogroup.com/blog/2012/04/how-to-remove-css-outlines-in-an-accessible-manner/)
- [Accessibility Wins](http://a11ywins.tumblr.com/)
- [paypal/AATT](https://github.com/paypal/AATT)
- [Notes On Client-Rendered Accessibility](http://www.smashingmagazine.com/2015/05/06/client-rendered-accessibility/)
- [AccessiWeb - Accueil](http://www.accessiweb.org/)
- [Why Implementing Swipe Gestures Causes A Mobile Accessibility Issue | Jennison Asuncion | LinkedIn](https://www.linkedin.com/pulse/why-implementing-swipe-gestures-causes-mobile-issue-jennison-asuncion)
- [The web accessibility basics – Marco's Accessibility Blog](https://www.marcozehe.de/2015/12/14/the-web-accessibility-basics/)
- [Accessibility - Usability - Google design guidelines](https://www.google.com/design/spec/usability/accessibility.html)
- [Designing A Dementia-Friendly Website – Smashing Magazine](https://www.smashingmagazine.com/2016/05/designing-a-dementia-friendly-website/)
- [Accessible Name and Description: Computation and API Mappings 1.1](https://www.w3.org/TR/accname-aam-1.1/)
- [Semantic HTML: The Unbearable Rightness of Being — Shopify UX — Medium](https://medium.com/shopify-ux/semantic-html-the-unbearable-rightness-of-being-9b3c493e1791#)
- [Controlling focus with tabindex -- A11ycasts #04 - YouTube](https://www.youtube.com/watch?v=Pe0Ce1WtnUM)
- [Writing JavaScript with Accessibility in Mind — SitePoint](https://www.sitepoint.com/writing-javascript-with-accessibility-in-mind/)
- [Don’t Use Tabindex Greater than 0 | Adrian Roselli](http://adrianroselli.com/2014/11/dont-use-tabindex-greater-than-0.html)
- [A11ycasts with Rod Dodson - YouTube](https://www.youtube.com/playlist?list=PLNYkxOF6rcICWx0C9LVWWVqvHlYJyqw7g)
- [Accessibility – Marco's Accessibility Blog](https://www.marcozehe.de/category/accessibility/)
- [Dos and don'ts on designing for accessibility | Accessibility](https://accessibility.blog.gov.uk/2016/09/02/dos-and-donts-on-designing-for-accessibility/), https://github.com/UKHomeOffice/posters/tree/master/accessibility
- [Using the aria-current attribute – Tink](http://tink.uk/using-the-aria-current-attribute/)
- [Writing HTML with accessibility in mind – A List Apart Sidebar – Medium](https://medium.com/alistapart/writing-html-with-accessibility-in-mind-a62026493412)
- [Writing JavaScript with accessibility in mind – A List Apart Sidebar – Medium](https://medium.com/@matuzo/writing-javascript-with-accessibility-in-mind-a1f6a5f467b9)
- [Notice d’accessibilité HTML, CSS et JavaScript | AcceDe Web](http://www.accede-web.com/notices/html-css-javascript/)
- [Accessibility | Web | Google Developers](https://developers.google.com/web/fundamentals/accessibility/)
- [WCAG 2.0 AA Accessibility Testing Checklist](https://www.icloud.com/numbers/0FUl7Nd3r-8VsOboCnaNjsomA#WCAG_2.0_AA_Accessibility_Testing_Checklist) - [Paul J. Adam sur Twitter : "Made a New WCAG 2.0 AA #A11y Testing Checklist in Numbers sheet. I'm open to collaborating/updating from feedback. https://t.co/rj6dcp6cbq https://t.co/JhA91plOU1"](https://mobile.twitter.com/pauljadam/status/948912600632479744)
- [Va11yS: Verified Accessibility Samples](https://ibma.github.io/Va11yS/)
- [Useful accessibility resources](https://www.stefanjudis.com/useful-accessibility-resources/)

## Access key

- [the new code – Creating Accesskey Shortcuts For Site Navigation](https://thenewcode.com/189/Creating-Accesskey-Shortcuts-For-Site-Navigation)

## Labelling

> The `aria-label` attribute is used to define a string that labels the current element. Use it in cases where a text label is not visible on the screen. If there is visible text labeling the element, use `aria-labelledby instead.
— [Using the aria-label attribute - Accessibility | MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-label_attribute)

	<a href="" aria-label="Learn more about opening an online store with Shopify">Learn more</a>

`aria-label`:

	<ul aria-label="Vehicle Models Available:"> 
		<li>Dodge Shadow</li>
		<li>Ford Focus</li>
		<li>Chevy Lumina</li>
	</ul>

`aria-labelledby`:

	<div role="dialog" aria-labelledby="dialogheader">
		<h2 id="dialogheader">Choose a File</h2>
		... Dialog contents
	</div>

Avoid the title attribute. Because touch can't handle it on link, abbr, images, etc. Some screen reader ignore it too.

Don't use `aria-describedby` for that. It's describe the element "provides more information that the user might need".

Don't use the `title` attribute (see [`title` attribute is not accessible](#`title` attribute is not accessible)), but a graphical hidden span to explain the linked document:

	<p>
		Washington has announced plans to stimulate economic growth.
		<a href="#"> <span>Washington stimulates economic growth </span> Full Story</a>
	</p>

	<dl>
		<dt>Winnie the Pooh </dt>
			<dd><a href="winnie_the_pooh.html">
				<span>Winnie the Pooh </span>HTML</a></dd>
			<dd><a href="winnie_the_pooh.pdf">
				<span>Winnie the Pooh </span>PDF</a></dd>
		...
	</dl>

- Image alt attribute: [HTML5: Techniques for providing useful text alternatives](http://dev.w3.org/html5/alt-techniques/)
- [4.7 Embedded content — HTML5](https://www.w3.org/TR/html5/embedded-content-0.html#alt)
- [Adactio: Journal—Unlabelled search fields](https://adactio.com/journal/10910)
- [Using aria-label for link purpose - WCAG WG](http://www.w3.org/WAI/GL/wiki/Using_aria-label_for_link_purpose)
- [html5 - Accessibility: recommended alt-text convention for SVG and MathML? - Stack Overflow](https://stackoverflow.com/questions/4697100/accessibility-recommended-alt-text-convention-for-svg-and-mathml)
- [I thought title text improved accessibility. I was wrong. | Silktide blog](http://blog.silktide.com/2013/01/i-thought-title-text-improved-accessibility-i-was-wrong/)
- [C7: Using CSS to hide a portion of the link text | Techniques for WCAG 2.0](http://www.w3.org/TR/2012/NOTE-WCAG20-TECHS-20120103/C7)
- [3 Semantics, structure, and APIs of HTML documents — The title attribute | HTML 5.1 Nightly](http://www.w3.org/html/wg/drafts/html/master/dom.html#the-title-attribute)
- [L’attribut title : à consommer avec modération – 24 jours de web](http://www.24joursdeweb.fr/2013/attribut-title-avec-moderation/)
- [Utilisabilité des <abbr> (tactile et vocale) (avec tweets) · tetue · Storify](https://storify.com/tetue/utilisabilite-des-abbr-tactile-et-vocale)
- [`abbr` element]()
- [Dev.Opera — UX accessibility with aria-label](https://dev.opera.com/articles/ux-accessibility-aria-label/)
- [Screen Reader Testing](http://jnurthen.users.sonic.net/test.html)
- [Writing for all people: how to use alternative text well — Shopify UX — Medium](https://medium.com/shopify-ux/writing-for-all-people-how-to-use-alternative-text-well-1205a18307a1#)

## Update content (script, AJAX)

- [AJAX progress/loader](#AJAX progress/loader)
- `output` element
- [Accessible forms with ARIA live regions – Tink](http://tink.uk/accessible-forms-with-aria-live-regions/)
- [Using the ARIA application role – Tink](http://tink.uk/using-the-aria-application-role/)

## Tabbed interface/content/section

Use this syntax for slideshow/carousel too.

If list of slides are visible:

	<ul aria-label="Elements" role="tablist"><!-- before augment to slideshow with JS the role should be role="directory" -->
		<li><a href="#element-1" role="tab" aria-selected="true">Element 1</a></li>
		<li><a href="#element-2" role="tab" aria-selected="false">Element 2</a></li>
		<li><a href="#element-3" role="tab" aria-selected="false">Element 3</a></li>
		<li><a href="#element-4" role="tab" aria-selected="false">Element 4</a></li>
	</ul>
	<div role="tabpanel" id="element-1" aria-hidden="false">
		<h2>Tab 1</h2>
	</div>
	<div role="tabpanel" id="element-2" aria-hidden="true">
		<h2>Tab 2</h2>
	</div>
	...

	<!-- Not really recommanded -->
	<fieldset aria-controls="elements">
		<ul>
			<li><button type="button">Previous</button></li>
			<li><button type="button">Next</button></li>
		</ul>
	</fieldset>
	<div id="elements" aria-live="polite">
		<div aria-hidden="true">
			<h2>Tab 1</h2>
		</div>
		<div aria-hidden="false">
			<h2>Tab 2</h2>
		</div>
		...
	</div>

- [How Tabs Should Work ◆ 24 ways](https://24ways.org/2015/how-tabs-should-work/)
- https://github.com/nico3333fr/jquery-accessible-tabs-aria
- [Using tabbed interfaces with a screen reader – Tink](http://tink.uk/using-tabbed-interfaces-with-a-screen-reader/)
- Don't use `role=listbox`: [javascript - WAI-ARIA Roles for Carousels (a.k.a. sliders, slideshows, galleries) - Stack Overflow](https://stackoverflow.com/questions/16840054/wai-aria-roles-for-carousels-a-k-a-sliders-slideshows-galleries)
- [The Unbearable Inaccessibility of Slideshows](http://www.sitepoint.com/unbearable-accessible-slideshow/)
- [ARIA carousel example](http://accessibility.athena-ict.com/aria/examples/carousel.shtml)
- [Carousel Concepts • Carousels • WAI Web Accessibility Tutorials](http://www.w3.org/WAI/tutorials/carousels/)
- [Advanced ARIA tip #1: Tabs in web apps – Marco's Accessibility Blog](https://www.marcozehe.de/2013/02/02/advanced-aria-tip-1-tabs-in-web-apps/)
- Incorrect example: [Danger! ARIA tabs » Simply Accessible](http://simplyaccessible.com/article/danger-aria-tabs/), read [Danger! Testing Accessibility with real people — Medium](https://medium.com/@LeonieWatson/danger-testing-accessibility-with-real-people-4515f72db648) and [ARIA tabs, UI problems and standards | AlastairC](https://alastairc.ac/2016/05/aria-tabs-ui-problems-and-standards/)

## `aria-controls`

**Don't use it.**

- [Aria-Controls is Poop | HeydonWorks](http://www.heydonworks.com/article/aria-controls-is-poop)

## AJAX progress/loader

	<!-- add aria-valuemin, aria-valuemax, and aria-valuenow if a progress value is known -->
	<!-- aria-valuetext could be used to give humand version of aria-valuenow -->
	<!-- aria-valuenow should not defined if the progress is undetermined -->
	<p id="indicatorID" aria-busy="true" role="progressbar or status">status message</p>
	
	<!-- aria-busy should be true until load complete (or error). For load error, set aria-invalid=true -->
	<div id="contentID" aria-describedby="indicatorID" aria-live="polite" aria-busy="true">content will be updated</div>

- http://www.w3.org/TR/wai-aria/roles#progressbar

## Hide / Show element dynamically

Change `hidden` attribute and use `arial-live="polite"` on the hidden/shown element (depends on the `role` attribute)

Use `[hidden]{display: none;}` to fallback for browser that don't support `hidden` attribute

Using `hidden` don't allow to make transitional states with CSS only. If you want to use transitional states, use `aria-hidden` instead

- http://tjvantoll.com/2013/01/09/html5-hidden-attribute-browser-support/
- https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes#hidden
- https://stackoverflow.com/questions/10349987/how-to-notify-screen-readers-using-wai-aria-that-a-div-is-now-visible/10351673#10351673
- [HTML5 Accessibility Chops: hidden and aria-hidden | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](https://www.paciellogroup.com/blog/2012/05/html5-accessibility-chops-hidden-and-aria-hidden/)

## Collapsible

See [Details and summary](#Details and summary)

Note: Ideally, expandable items should be following the item that expands and collapses them

- [Using aria-expanded to indicate the state of a collapsible element - WCAG WG](https://www.w3.org/WAI/GL/wiki/Using_aria-expanded_to_indicate_the_state_of_a_collapsible_element)
- [Using the WAI-ARIA aria-expanded state to mark expandable and collapsible regions - WCAG WG](https://www.w3.org/WAI/GL/wiki/Using_the_WAI-ARIA_aria-expanded_state_to_mark_expandable_and_collapsible_regions)
- [Example 22 - Hide/Show: Region is exclusive](http://oaa-accessibility.org/example/22/)

## Modal

	<style>
	.box-hidden {
		display: none;
		position: absolute;
		top: 19em; left:15em; width:20em; height:5em;
		border: 2px solid black;
		padding:0 1em 1em 1em;
		background-color: #eee;
		z-index:1002;
		overflow: auto;
	}		
	</style>
	
	<script>
	var dialogOpen = false, lastFocus, dialog, okbutton, pagebackground;
	
	function showDialog(el) {
		lastFocus = el || document.activeElement;
		toggleDialog('show');
	}
	function hideDialog(el) {
		toggleDialog('hide');
	}
	
	function toggleDialog(sh) {
		dialog = document.getElementById("box");
		okbutton = document.getElementById("ok");
		pagebackground = document.getElementById("content");
	
		if (sh == "show") {
			dialogOpen = true;
	
			// show the dialog 
			dialog.style.display = 'block';
		
			// after displaying the dialog, focus an element inside it
			okbutton.focus();// be carefull, if you have animations and overflow: hidden, you shoud do elementWithOverflowHidden.scroll[Left|Top] = 0
		
			// only hide the background *after* you've moved focus out of the content that will be "hidden"
			pagebackground.setAttribute("aria-hidden","true");
		
		} else {
			dialogOpen = false;
			dialog.style.display = 'none';
			pagebackground.setAttribute("aria-hidden","false");
			lastFocus.focus(); 
		}
	}
	
	// Focus trap
	document.addEventListener("focus", function(event) {
		var d = document.getElementById("box");
	
		if (dialogOpen && !d.contains(event.target)) {
			event.stopPropagation();
			d.focus();
		}
	}, true);
	
	document.addEventListener("keydown", function(event) {
		if (dialogOpen && event.keyCode == 27) {
			toggleDialog('hide');
		}
	}, true);
	
	</script>
	
	<div id="content">
	<!--[...]-->
	<p><a onclick="showDialog(this); return false;" href="#box" role="button">Display a dialog</a></p>
	<!--[...]-->
	</div>
	
	<div role="dialog" aria-labelledby="myDialog" id="box" class="box-hidden" tabindex="-1">
		<h3 id="myDialog">Just an example.</h3>
		<button id="ok" onclick="hideDialog(this);" class="close-button">OK</button>
		<button onclick="hideDialog(this);" class="close-button">Cancel</button>		
	</div>

Specific case for the "orientation lock" alert:

- **orientation lock should be avoided**
- specific to mobile where viewport = screen
- use the role alert instead of dialog/alertdialog (because user can't response to it to the "orientation lock" alert)

- [A11y Dialog - A very lightweight and flexible accessible modal dialog](https://github.com/edenspiekermann/a11y-dialog)
- http://www.nczonline.net/blog/2013/02/12/making-an-accessible-dialog-box/
- [The Incredible Accessible Modal Window, Version 3](http://accessibility.oit.ncsu.edu/training/aria/modal-window/version-3/) and [gdkraus/accessible-modal-dialog](https://github.com/gdkraus/accessible-modal-dialog)
- [Using ARIA role=dialog to implement a modal dialog box - WCAG WG](http://www.w3.org/WAI/GL/wiki/Using_ARIA_role%3Ddialog_to_implement_a_modal_dialog_box)
- [Screen reader testing of aria role=dialog](http://3needs.org/en/testing/code/role-dialog.html)
- [Advanced ARIA Tip #2: Accessible modal dialogs | Marco's Accessibility Blog](https://www.marcozehe.de/2015/02/05/advanced-aria-tip-2-accessible-modal-dialogs/)
- [Using the dialog role - Accessibility | MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_dialog_role)
- http://www.smashingmagazine.com/2014/09/15/making-modal-windows-better-for-everyone/
- [ARIA Dialog Example](http://accessibility.athena-ict.com/aria/examples/dialog.shtml)
- [WAI-ARIA 1.0 Authoring Practices](http://www.w3.org/TR/wai-aria-practices/#dialog_modal)
- [Accessible Modal Windows: Revisited | scottohara.me](http://www.scottohara.me/article/modal-window-revisited.html)
- [Modaal - An accessible dialog window library for all humans](https://github.com/humaan/Modaal) - An WCAG 2.0 Level AA accessible modal window plugin

## Notification

- [Accessible timeout notifications – Tink](http://tink.uk/accessible-timeout-notifications/)

## Accessible drag and drop

- [Accessible Drag and Drop with Multiple Items](http://www.sitepoint.com/accessible-drag-drop/) and [sitepoint-editors/accessible-drag-and-drop](https://github.com/sitepoint-editors/accessible-drag-and-drop)

## Accessible canvas

If it's a simple scene, use alt text:

	<canvas role="img" aria-label="This would be the alt text."></canvas>

Or use a shadow DOM/subdom:

	<canvas>
		<button type="button"></button>
	</canvas>
	<script>
		var canvas = document.getElementsByTagName("canvas")[0];
		var button = canvas.firstElementChild;
		var ctx = canvas.getContext("2d");
		button.focus();
		function draw(){
			ctx.clearRect(0, 0, canvas.width, canvas.height);
			ctx.beginPath();
			ctx.rect(10, 10, 30, 30);
			ctx.drawFocusIfNeeded(button);// will draw if button is focused (on Chrome it's draw system focus ring)
			requestAnimationFrame(draw);
		}
		draw();
	</script>
	<p>Use tab key to focus the button</p>

- [HTML5 canvas sub DOM | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](http://www.paciellogroup.com/blog/2015/02/html5-canvas-sub-dom/)
- [Flipboard – React Canvas Accessibility | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](http://www.paciellogroup.com/blog/2015/02/flipboard-react-canvas-accessibility/)
- [Notes on accessibility of text replacement using HTML5 canvas | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](https://www.paciellogroup.com/blog/2009/06/notes-accessibility-of-text-replacement-using-html5-canvas/)
- [WebAIM: Future Web Accessibility: canvas](http://webaim.org/blog/future-web-accessibility-html-canvas/)
- [Basic usage of canvas - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Basic_usage)
- [Hit regions and accessibility - Web API Interfaces | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Hit_regions_and_accessibility)
- [AddedElementCanvas - HTML WG Wiki](https://www.w3.org/html/wg/wiki/AddedElementCanvas)
- [Canvas hit testing - W3C Wiki](https://www.w3.org/wiki/Canvas_hit_testing)
- [Reading text in canvas - W3C Wiki](https://www.w3.org/wiki/Reading_text_in_canvas)
- [Canvas | Scripted Interactivity | EPUB 3 Accessibility Guidelines](http://www.idpf.org/accessibility/guidelines/content/script/canvas.php)
- [Canvas Uses and Techniques for WCAG](http://www.jumis.com/cme-tech.html)
- [HTML5 Canvas and the Canvas Shadow DOM (Internet Explorer)](https://msdn.microsoft.com/en-us/library/hh968259(v=vs.85).aspx)
- [495912 – Expose alternative content in Canvas element to ATs](https://bugzilla.mozilla.org/show_bug.cgi?id=495912)
- [HTML5 Canvas and Accessibility: Sub Dom - HTML5 Canvas, 2nd Edition [Book]](https://www.safaribooksonline.com/library/view/html5-canvas-2nd/9781449335847/ch01s12.html)

## Focus

### `tabindex`

- Elements with `tabindex="0"` are part of the natural tab sequence
- Elements with `tabindex="-1"` are not, but are focusable with scripting
- Elements with `tabindex=">0"` are never a good idea

- [Using the tabindex attribute | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](https://www.paciellogroup.com/blog/2014/08/using-the-tabindex-attribute/)

### Focusable

`document.body` is the default `document.activeElement` but it's not a focusable element. Use `document.documentElement.focus()` instead.

## Spelling is important

Especially when you use a screen reader.

Use right chars:

- minus: `&minus;`/`−` (U+2212 / minus sign) instead of `-` (U+002D / hyphen-minus)
- multiply: `×` instead of `*`
- division: `÷` instead of `/`

- (french) "Ca" → 💬"ka", "Ça" → 💬"sa"
- (french) "Acceuil" → 💬"ak-seuil", "Accueil" → 💬"akeuil"
- (french) "UN GENDARME TUE" (a police officer kill) → "UN GENDARME TUÉ" (a police officer killed)
- "CONTACT US" → 💬"Contact U S". Use CSS text-transform instead

> ‘eg’ can sometimes be read aloud as ‘egg’ by screen reading software. Instead use ‘for example’ or ‘such as’ or 'like' or ‘including’ - whichever works best in the specific context.
> ‘etc’ can usually be avoided. Try using ‘for example’ or ‘such as’ or ‘including’. Never use ‘etc’ at the end of a list starting with ‘for example’ or ‘such as’ or ‘including’.
> ‘ie’ - used to clarify a sentence - isn’t always well understood. Try (re)writing sentences to avoid the need to use it. If that isn’t possible, use an alternative such as ‘meaning’ or ‘that is’.
– [Changes to the style guide: no more eg, and ie, etc | Inside GOV.UK](https://insidegovuk.blog.gov.uk/2016/07/20/changes-to-the-style-guide-no-more-eg-and-ie-etc/)

Note: 'eg' should be written 'e.g.' and 'ie' 'i.e.'

- [Orthographe et accessibilité | nota-bene.org](http://nota-bene.org/Orthographe-et-accessibilite)
- [Dash — Wikipedia](https://en.wikipedia.org/wiki/Dash)
- [UK government changes website guidelines due to buggy screen readers | Hacker News](https://news.ycombinator.com/item?id=12164831)

## `title` attribute is not accessible

Accessible to user with AT but for touch device users too.

See [Labelling](#Labelling)

- [Using the HTML title attribute – Updated Dec 2012 | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](https://www.paciellogroup.com/blog/2010/11/using-the-html-title-attribute/)

## Tooltip

- [Simple standalone toggletip widget pattern | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](https://www.paciellogroup.com/blog/2016/01/simple-standalone-toggletip-widget-pattern/)

## Scrollable element

Firefox: scrollable elements are focusable (via keytab) without `tabindex` attribute

- [Short note on improving usability of scrollable regions | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](https://www.paciellogroup.com/blog/2016/02/short-note-on-improving-usability-of-scrollable-regions/)

## Extra text ease accessibility

For Text Alternative Computation

Use `aria-label` (better):

	<h2 aria-label="The Lord of the Rings: The Two Towers">The Lord of the Rings <span class="sub">The Two Towers</span></h2>

	<a href="" aria-label="Learn more about opening an online store with Shopify">Learn more</a>

	<a href="" arial-label="En savoir plus">En savoir +</a>

Or use CSS with extra elements:

	<style>
	.sep, .extra {display: block; position: absolute; overflow: hidden;width:1px; height: 0px; padding-top: 1px}/*See [Hide graphicaly an element](CSS#Hide graphicaly an element)*/
	.sub {display:block; font-style:italic;}
	</style>

	<h2>The Lord of the Rings<span class="sep">: <span><span class="sub">The Two Towers</span></h2>

	<a href="">Learn more<span class="extra"> about Victorian Room</span></a>

- `<span role="img" aria-label="peach or bum">🍑</span>` [Accessible Emoji, Tweaked | Adrian Roselli](http://adrianroselli.com/2016/12/accessible-emoji-tweaked.html)
- [Tagline & subheader](#Tagline & subheader)
- [Aesthetics of the invisible | Francesco Schwarz](https://francescoschwarz.de/en/blog/aesthetics-of-the-invisible/)
- [Text for Screen Readers Only (Updated) - Coolfields Consulting](http://www.coolfields.co.uk/2016/05/text-for-screen-readers-only-updated/)
- [The Roles Model | Accessible Rich Internet Applications (WAI-ARIA) 1.0](https://www.w3.org/TR/wai-aria/roles#textalternativecomputation)
- [Accessible emoji – Tink](http://tink.uk/accessible-emoji/)

## Media player

- [HTML 5 Form Elements](https://dequeuniversity.com/assets/html/jquery-summit/html5/slides/video.html)

### Play / pause

Toggle buttons (should be like a checkbox) should have persistent labels "Play"

> "play, [ARIA: "not pressed"]" and "play, [ARIA: "pressed"]"

> Play/Pause should not use aria-pressed

Stop should be a button to untoggle play / pause

- https://twitter.com/heydonworks/status/777419213065580544
- [WAI-ARIA Authoring Practices 1.1](https://www.w3.org/TR/wai-aria-practices-1.1/#button)
- [icons - Alternates to the "play/pause" button - User Experience Stack Exchange](http://ux.stackexchange.com/questions/9184/alternates-to-the-play-pause-button)
- [Should a toggle button show its current state or the state to which it will change? - User Experience Stack Exchange](http://ux.stackexchange.com/questions/1318/should-a-toggle-button-show-its-current-state-or-the-state-to-which-it-will-chan)
- [Dev.Opera — A More Accessible HTML5 \<video\> Player](https://dev.opera.com/articles/more-accessible-html5-video-player/)
- [The different aspects of video accessibility | ginger's thoughts](http://gingertech.net/2009/08/03/aspects-of-video-accessibility/)

## Sortable list

Aka drag and drop list, dnd list, orderable list, reorderable list

- [Accessible Drag and Drop with Multiple Items](https://www.sitepoint.com/accessible-drag-drop/)
- [Dev.Opera — Accessible Drag and Drop Using WAI-ARIA](https://dev.opera.com/articles/accessible-drag-and-drop/)
- [Accessibility & Native Drag and Drop | HTML5 Doctor](http://html5doctor.com/accessibility-native-drag-and-drop/)
- [Accessible drag & drop sortable list](https://codepen.io/barrytsmith/details/kfiqj)

## Tree view

> ![](https://dropboxtechblog.files.wordpress.com/2017/04/tree.gif)
> Tree view depicting a sample folder hierarchy in Dropbox, along with some of its corresponding HTML. By pressing arrow keys, user can navigate up and down through the tree, as well as expand and collapse folder nodes. In the HTML, the tree’s aria-activedescendant attribute automatically updates to the id of the currently selected tree item. Individual tree items’ aria-expanded and aria-selected attributes update to reflect their current state.

- use `aria-activedescendant` if collapsible

## Dynamic area

- [Using aria-live](https://bitsofco.de/using-aria-live/)
- [ARIA Live Regions | MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions)

# Patterns, markup, semantics and snippets

> Semantic HTML is HTML which makes a positive contribution to the meaning conveyed by the plain language of the page.
— @heydonworks

> Turn off CSS.
> If the page makes no sense, fix your markup.
— [Elika J. Etemad](http://fantasai.inkedblade.net/style/talks/best-practices/#no-css)

- [Understanding semantics – Tink](http://tink.uk/understanding-semantics/)

Define for marking up something has no dedicated mechanism in HTML

Accessiblilty is highly based on correct semantics. But semantics are also used by SEO (and other machine learning) for both static (HTML) and dynamic (DHTML) content (a bot can execute JavaScript):

Ex. Firefox reader view detect presence of some nodes types to enable it

- [WebAIM: Web Accessibility and SEO](http://webaim.org/blog/web-accessibility-and-seo/)
- [High Accessibility Is Effective Search Engine Optimization · An A List Apart Article](http://alistapart.com/article/accessibilityseo)

- http://www.w3.org/html/wg/drafts/html/master/common-idioms.html
- http://html5doctor.com/element-index/
- http://patterns.alistapart.com/
- http://www.w3.org/wiki/HTML_structural_elements
- http://www.w3.org/wiki/Category:HTML
- http://www.w3.org/wiki/Marking_up_textual_content_in_HTML
- http://diveintohtml5.info/semantics.html#new-elements
- http://www.w3.org/community/webed/wiki/Lesser_-_known_semantic_elements
- https://github.com/tpryan/whichelement
- http://html5forwebdesigners.com/semantics/
- http://www.impressivewebs.com/html5-section/
- http://html5doctor.com/microformats/#uf-wiki
- https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Sections_and_Outlines_of_an_HTML5_document
- https://support.google.com/webmasters/?hl=en&rd=1#topic=21997
- [Promote Your Content with Structured Data Markup   |   Structured Data   |   Google Developers](https://developers.google.com/structured-data/)
- [HTML Reference - A free guide to all HTML elements and attributes.](http://htmlreference.io/)

- [Money semantics](https://stackoverflow.com/questions/9632311/which-html5-tags-are-more-appropriate-for-money)
- [Techniques for WCAG 2.0](http://www.w3.org/TR/WCAG20-TECHS/)

- http://snipplr.com/popular/language/html
- http://css-tricks.com/snippets/

- [alexpate/awesome-design-systems: 💅🏻 ⚒ A collection of awesome design systems](https://github.com/alexpate/awesome-design-systems) - Components examples

## Microdata

- [A Tragedy in 2 Acts by Taylor Hunt on CodePen](https://codepen.io/tigt/post/a-tragedy-in-2-acts)
- [Home - schema.org](https://schema.org/) and [Structured Data Testing Tool   |   Google Developers](https://developers.google.com/structured-data/testing-tool/)
- [HTML Microdata](http://www.w3.org/TR/microdata/)
- [microformats 2 · Microformats Wiki](http://microformats.org/wiki/microformats2)

## `header` element

By default its `role` is `banner`

> There is a crucial difference between the header element and the general accepted usage of header (or masthead). There’s usually only one header or ‘masthead’ in a page. In HTML5 you can have as many as you want. The spec defines it as “a group of introductory or navigational aids”. You can use a header in any section on your site. In fact, you probably should use a header within most of your sections. The spec describes the section element as “a thematic grouping of content, typically with a heading.”

Can contains title, subtitles, tagline, strapline, aside, introduction, navigation

- [Tagline & subheader](#Tagline & subheader)

## `h1`-`h6`

`h1` should reflect content of the page/document

	<p><!--logo-->Bob's Chunky Bacon Store</p>
	<h1>Smoked Bacon</h1>
	<p>Bacon bacon bacon bacon etc...</p>

	<p><!--logo-->Bob's Chunky Bacon Store</p>
	<h1>About Bob's Chunky Bacon Store</h1>
	<p>About the store etc...</p>

- See [Tagline & subheader](#Tagline & subheader)

About the brand's logo:

- should be in the `<main>` because it's "excludes content that is repeated across a set of documents"
- [Your logo is an image, not a <h1> – CSS Wizardry – CSS, OOCSS, front-end architecture, performance and more, by Harry Roberts](http://csswizardry.com/2010/10/your-logo-is-an-image-not-a-h1/)

### Nested

Aka document outline

The heading level (h1, h2, h3, etc.) should reflect deepth of the container (by default the owner page - as root document title / page title, else `section` or `article`, `nav`, `aside`)

	<body>
		<h1>top level heading</h1>
		<section>
			<h2>(intended) 2nd level heading</h2>
			<section>
				<h3>(intended) 3nd level heading</h3>
			</section>
		</section>
	</section>

- [Computer says NO to HTML5 document outline | HTML5 Doctor](http://html5doctor.com/computer-says-no-to-html5-document-outline/)
- [HTML/Usage/Headings/h1only - W3C Wiki](https://www.w3.org/wiki/HTML/Usage/Headings/h1only)
- [Do not recommend using nested sections with h1 · Issue #169 · w3c/html](https://github.com/w3c/html/issues/169)

In HTML5 is't allowed to use h1 only:

- [The Truth About Multiple H1 Tags in the HTML5 Era - Tuts+ Web Design Article](http://webdesign.tutsplus.com/articles/the-truth-about-multiple-h1-tags-in-the-html5-era--webdesign-16824)

It's no more true with HTML 5.1

## Head

`title`, `base`, `style`, `script`, `meta`, `link`

- [A collection of HTML head elements](https://github.com/joshbuchea/HEAD/blob/master/README.md)
- [ManifeStation - Automagically create your Web App Manifest](https://webmanife.st/)
- [Web App Manifest](https://www.w3.org/TR/appmanifest/)

## Content vs. decorative image

`img[alt]:not([alt=""])` element vs. `img[alt=""]` or CSS `background-image`

	<span style="background: url(image.jpg)" role="img" aria-label="[place alt text here]"></span>
	<!-- the background style could be defined for the parent element instead -->

- If you remove the image (ex. image load error) (or remove all CSS), does the content still have a meaning? Yes: CSS or `img[alt=""]`, No: img
- If the element is interactive and you remove the CSS or the bg not load, does it still comprehensible (not a fully transparent area)?
- Logo or diagram or person (real person, not stock photo people) should be an image
- you can use `aria-label` or `aria-labelledby` and `title`. Note: [`title` attribute is not accessible](#`title` attribute is not accessible)
- CSS can use aspect ratio with `padding-top: 100%` (percentage of padding are relative to element's width). But it's predefined, not based on image's real aspect ratio.
- If its logo or icon, does have a alternative if the image not loaded (alt attribute for image) or label (aria-label)? You should use text with the icon.
- CSS allows to add img with CSS using pseudo elements: `div::after{content: url("image.jpg") / "alt text"}`. See links below
- see also `aria-hidden="true"`

> A picture is worth a thousand words

> Images are more than just decoration; they have the power to make or break a user’s experience
— Nick Babich in [More Than Just Pretty: How Imagery Drives User Experience – Smashing Magazine](https://www.smashingmagazine.com/2017/01/more-than-just-pretty-how-imagery-drives-user-experience/)

Only for "fix" technical issue:

- img can't be a sprite
- img is printed by default
- background can be embedded in style (when the alt text is hidden)
- css background allow multiple image composition
- image can be streched (it's the case with css background with `background-size`)
- img has better rendering performance
- css background allow image transition `transition: background-image 1s`
- background can be fit area (img too with `object-fit`)

If you have to define multiple size based on dppx or viewport size, you can use both: (img) with srcset or (CSS) with media queries in style tag

**Note: If you use SVG as inlined icon (in HTML, using `<use>`), always define a inlined stylesheet: `<style>.icon { width: 1em; height: 1em; fill: currentColor; }</style>` in case of faulty CSS loading.** See [SVG Style Inheritance and the ‘Flash Of Unstyled SVG’](https://sarasoueidan.com/blog/svg-style-inheritance-and-FOUSVG/) and http://d.pr/i/cHS2/2XMaVh29

Image alternative:

- [Writing for all people: how to use alternative text well — Shopify UX — Medium](https://medium.com/shopify-ux/writing-for-all-people-how-to-use-alternative-text-well-1205a18307a1#)
- [Alternative Text and Images](https://bitsofco.de/alternative-text-and-images/)
- [Images Concepts • Images • WAI Web Accessibility Tutorials](https://www.w3.org/WAI/tutorials/images/)
- https://stackoverflow.com/questions/492809/when-to-use-img-vs-css-background-image
- [F3: Failure of Success Criterion 1.1.1 due to using CSS to include images that convey important information | Techniques for WCAG 2.0](http://www.w3.org/TR/WCAG20-TECHS/F3.html)
- [mezzoblue § Testing Grounds](http://www.mezzoblue.com/tests/revised-image-replacement/)

- [How Can I Make My Icon System Accessible? | CSS-Tricks](https://css-tricks.com/can-make-icon-system-accessible/)
- [CSS image replacement with pseudo-elements (NIR) – Nicolas Gallagher](http://nicolasgallagher.com/css-image-replacement-with-pseudo-elements/)
- [Alternative Text for Speech — CSS Generated Content Module Level 3](https://www.w3.org/TR/css-content-3/#alt)
- [Image Replacement with Invisible Webfonts by Taylor Hunt on CodePen](https://codepen.io/tigt/blog/image-replacement-with-the-adobe-blank-webfont)
- [Are icons content? | CSS-Tricks](https://css-tricks.com/are-icons-content/)
- [SVG `symbol` a Good Choice for Icons | CSS-Tricks](https://css-tricks.com/svg-symbol-good-choice-icons/)
- [It's Time to Be Honest about Image Replacement Techniques](https://www.sitepoint.com/its-time-to-be-honest-about-image-replacement-techniques/)
- [More Than Just Pretty: How Imagery Drives User Experience – Smashing Magazine](https://www.smashingmagazine.com/2017/01/more-than-just-pretty-how-imagery-drives-user-experience/)
- [Alternate text for background images, alt text accessibility](http://davidmacd.com/blog/alternate-text-for-css-background-images.html)

See also [CSS - Image](CSS#Image)

## Responsive image

Aka Adaptive image

- `srcset` = what you got
- `sizes` = how big it gonna be

Note: Use SVG if srcset not supported
 
	<img src="kirkjufell.jpg" srcset="kirkjufell_2x.jpg 2x" alt="Photograph of a blurred waterfall in Iceland with a conical mountain behind it">

- [When Responsive Images Get Ugly by Taylor Hunt on CodePen](https://codepen.io/tigt/blog/when-responsive-images-get-ugly)
- [4 The elements of HTML | HTML 5.1 Nightly](http://www.w3.org/html/wg/drafts/html/master/semantics.html#attr-img-srcset)
- [RespImageLint](https://ausi.github.io/respimagelint/) - Lint image element to check against a list of common mistakes and best practises. See https://github.com/ausi/RespImageLint
- [Cropping Image Thumbnails with SVG - Cloud Four](https://cloudfour.com/thinks/cropping-image-thumbnails-with-svg/)
- [Responsive images with srcset and sizes – Medium](https://medium.com/@woutervanderzee/responsive-images-with-srcset-and-sizes-fc434845e948#)
- [How to Build Responsive Images with srcset](https://www.sitepoint.com/how-to-build-responsive-images-with-srcset/)
- [Tutoriels sur les Images Responsives](https://la-cascade.io/tag/images-responsives/)

## Form

Empty `action` attribute: [web standards - Is it a good practice to use an empty URL for a HTML form's action attribute? (action="") - Stack Overflow](https://stackoverflow.com/questions/1131781/is-it-a-good-practice-to-use-an-empty-url-for-a-html-forms-action-attribute-a)

	<div role="alert">
		<p>There were errors with your form submission:</p>
		<ol>
			<li><a href="#message">Message</a> is a required field</li>
			<li><a href="#name">Name</a> is a required field</li>
			<li><a href="#email">Email</a> is a required field</li>
		</ol>
	</div>
	
	<p>
		<label for="email">Your Email</label>
		<input type="email" id="email" name="email" required aria-describedby="email-note email-error">
		<em id="email-note">We will only use your email address to respond to your message.</em>
		<strong id="email-error">Your email address is required</strong>
	</p>
	
	<p>
		<label for="preferred_phone">Preferred Phone <abbr title="required">*</abbr></label>
		<input type="tel" id="preferred_phone" name="preferred_phone" placeholder="ex. 123-456-7890">
	</p>

When a form is submitted, and the result is the same page (with error message, etc.) by default take the focus of the same form (or the error message or the faulty input, etc.)

- [Making password managers play ball with your login form](https://hiddedevries.nl/en/blog/2018-01-13-making-password-managers-play-ball-with-your-login-form)
- [nsLoginManager.js - DXR](https://dxr.mozilla.org/firefox/source/toolkit/components/passwordmgr/src/nsLoginManager.js#626) - Firefox source code of utils to find login and password inputs
- [1119454 - (password-recipes) Support per-sites recipes for capturing and filling the user's login credentials](https://bugzilla.mozilla.org/show_bug.cgi?id=1119454)
- [Label and name inputs properly — Web Fundamentals](https://developers.google.com/web/fundamentals/input/form/label-and-name-inputs?hl=en)
- http://blog.paciellogroup.com/2011/07/html5-accessibility-chops-form-control-labeling/
- [Accessible Forms 1: Labels and identification | Web Usability](http://usability.com.au/2013/04/accessible-forms-1-labels-and-identification/)
- [Accessible Forms 2: Required Fields and Extra Information | Web Usability](http://usability.com.au/2013/05/accessible-forms-2-required-fields-and-extra-information/)
- http://accessibility.oit.ncsu.edu/training/forms/multiple-inputs.html
- http://accessibility.oit.ncsu.edu/training/forms/aria-live-notification.html
- [How to make error messages accessible](https://hiddedevries.nl/en/blog/2017-04-04-how-to-make-error-messages-accessible)

### Submit button

Note: button can also be a button (not a submit button) `<button type="button"></button>`. It's not owned by any form.

	<input type="submit" value="Send">

or

	<button>Send</button>

The second one are much easier to style. But in old IE, innerHTML was sent, [plus few others bugs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Button#Notes). Type attribute with value `submit` is the default value.

Button should be in a phrasing content: a `p` element as parent (but not required) or in `<li>`

### Form validation

- [Native form validation — part 1 – Samsung Internet Developers – Medium](https://medium.com/samsung-internet-dev/native-form-validation-part-1-bf8e35099f1d)

### Placeholder

- [Don’t Use The Placeholder Attribute — Smashing Magazine](https://www.smashingmagazine.com/2018/06/placeholder-attribute/)

### Placeholder as label

Aka Label inside input

**It's a bad idea!**

> **Warning!** Use of the `placeholder` attribute as a replacement for a `label` can reduce the accessibility and usability of the control for a range of users including older users and users with cognitive, mobility, fine motor skill or vision impairments. While the hint given by the control’s `label` is shown at all times, the short hint given in the `placeholder` attribute is only shown before the user enters a value. Furthermore, `placeholder` text may be mistaken for a pre-filled value, and as commonly implemented the default color of the `placeholder` text provides insufficient contrast and the lack of a separate visible `label` reduces the size of the hit region available for setting focus on the control.
— http://w3c.github.io/html/sec-forms.html#element-attrdef-input-placeholder

See also:

- [Labels in input fields aren’t such a good idea | Laura Kalbag](http://laurakalbag.com/labels-in-input-fields-arent-such-a-good-idea/)
- [The HTML5 placeholder attribute is not a substitute for the label element | 456 Berea Street](http://www.456bereastreet.com/archive/201204/the_html5_placeholder_attribute_is_not_a_substitute_for_the_label_element/)
- [HTML5 Accessibility Chops: the placeholder attribute | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](https://www.paciellogroup.com/blog/2011/02/html5-accessibility-chops-the-placeholder-attribute/)
- [UI - UX - Placeholder as label](UI - UX#Placeholder as label)

### Input inside label

**Don't:**

	<label>
		<input type="text" name="lastname">
		Last Name
	</label>

> Nest the `<input>` within the `<label>` tag, is semantically incorrect since the input is not a part of the label, being only its counterpart

Also because with this technique, the input can have only have one associated label ([in HTML4](http://www.w3.org/TR/html401/interact/forms.html#idx-label-1). [In HTML5](http://www.w3.org/TR/html5/forms.html#the-label-element)), it's not specified clearly.

- [F68: Failure of Success Criterion 4.1.2 due to a user interface control not having a programmatically determined name | Techniques for WCAG 2.0](http://www.w3.org/TR/WCAG20-TECHS/F68.html)
- [H44: Using label elements to associate text labels with form controls | Techniques for WCAG 2.0](http://www.w3.org/TR/WCAG20-TECHS/H44.html)

### Error message

	<form>
		<p>
			<label for="username">Username</label>
			<input type="text" id="username" name="username" required inputmode="verbatim" aria-describedby="username-error">
		</p>
		<!--
			Could add the "hidden" attribute in case of JS will use that message later (front end custom validation)
			or use style display:none by default, and remove it when used
		-->
		<p id="username-error" role="alert">Username is already taken</p>
	</form>

- [Accessible form](#Accessible form)
- http://html5doctor.com/the-output-element/#comment-47159 Use `output` element as error message for input
- https://stackoverflow.com/questions/4707936/error-message-span-vs-label
- https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_alert_role

### Input format

	<form>
		<p>
			<label for="birthday">Date of birth</label>
			<input type="text" id="birthday" name="birthday" aria-describedby="birthday-format">
		</p>
		<p id="birthday-format">Date must be DD/MM/YYYY</p>
	</form>

- [Adactio: Journal—Marking up help text in forms](https://adactio.com/journal/11109)

### Checkbox

- [ARIA Checkbox – IT Accessibility](https://accessibility.oit.ncsu.edu/it-accessibility-at-nc-state/developers/accessibility-handbook/aria-checkbox/)

### Select with unselected option

Without (valid) selection

	<select>
		<option value="1900">1900</option>
		<option value="1901">1901</option>
		<!--...-->
		<!-- Define label as "Undefined" or (&ndash;) "–" or (&horbar;) "―" or (math) "{}", "∅", and " ∅ " or "  ⃠ " -->
		<option selected value="">No selection</option>
		<!-- Or use the label attribute with space or other non empty value the user can't select -->
		<option disabled selected value="" label=" "></option>
	</select>

You can also use JS, it's but not the best solution:

	document.getElementById("myDropdown").selectedIndex = -1;

- [html - default select option as blank - Stack Overflow](https://stackoverflow.com/questions/8605516/default-select-option-as-blank)

### Disabled vs readonly

An input field is disabled to indicate that it cannot currently be used. This might be because it is not applicable, e.g. due to the value of some other field.

> The basic difference between disabled and readonly for text inputs is that you cannot access a disabled input in any way whatsoever.  For a readonly input, you cannot change the value, but you can, for example, highlight the value and copy it, then paste it elsewhere....
https://bugzilla.mozilla.org/show_bug.cgi?id=88512#c14

The Disabled attribute:

- Indicate that it cannot currently be used. This might be because it is not applicable, e.g. due to the value of some other field. Require an application action or a user action to enable/disable its usage
- Values for disabled form elements are not passed to the processor method. The W3C calls this a successful element.(This works similar to form check boxes that are not checked.)
- Some browsers may override or provide default styling for disabled form elements. (Gray out or emboss text) Internet Explorer 5.5 is particularly nasty about this.
- Disabled form elements do not receive focus.
- Disabled form elements are skipped in tabbing navigation.

The Read Only Attribute:

- The data that must be submitted as a value along with the form (like an hidden input, but shown to the user)
- Not all form elements have a readonly attribute. Most notable, the `<select>`, `<option>`, and `<button>` elements do not have readonly attributes (although thy both have disabled attributes)
- Browsers provide no default overridden visual feedback that the form element is read only.
- Form elements with the readonly attribute set will get passed to the form processor (if a name attribute is defined).
- Read only form elements can receive the focus
- Read only form elements are included in tabbed navigation.
- `tabIndex="-1"` can be used and it won't be editable (and focusable as an input would be)

- http://kreotekdev.wordpress.com/2007/11/08/disabled-vs-readonly-form-fields/
- http://www.w3.org/TR/html4/interact/forms.html#h-17.12
- https://html.spec.whatwg.org/multipage/forms.html#the-readonly-attribute

### Fields

`ul>li`, `ol>li`, `p`, `span`, etc.?

> In real life the form is just an unordered (or ordered) list of inputs

Use list for radios, with a fieldset:

	<form action="">
		<fieldset>
			<legend>Shipping method:</legend>
			<ul>
				<li>
					<input id="overnight" type="radio" name="shipping" value="overnight">
					<label for="overnight">Overnight</label>
				</li>
				<li>
					<input id="twoday" type="radio" name="shipping" value="twoday">
					<label for="twoday">Two day</label>
				<li>
				</li>
					<input id="ground" type="radio" name="shipping" value="ground">
					<label for="ground">Ground</label>
				</li>
			</ul>
		</fieldset>
		<!-- equivalent of:
		<p>
			<label for="shipping">Shipping method</label>
			<select id="shipping" name="shipping">
				<option value="overnight">Overnight</option>
				<option value="twoday">Two day</option>
				<option value="ground">Ground</option>
			</select>
		</p>
		-->
		
		<button>Submit</button>
	</form>
	<!-- [WebAIM: Creating Accessible Forms - Accessible Form Controls](http://webaim.org/techniques/forms/controls#radio) -->

Note: the fieldset's legend [can contains a checkbox](https://www.w3.org/wiki/HTML/Elements/fieldset#Example_B) [to controls the content](https://www.w3.org/TR/html5/forms.html#the-fieldset-element)

Use the fieldset when you have:

- a single multiple choice question (using radio buttons or checkboxes).
- several questions relating to the same topic (like text boxes, or any other type of field). ("Your address" = Street + Town or city + County + Postcode)

Don't use fieldset when you have a single form field that asks for a single piece of information.


And for self explanatory choices (radios, like gender), without fieldset:

	<form action="">
		<ul>
			<li>
				<label for="male">Male</label>
				<input name="gender" value="male" id="male" type="radio">
			</li>
			<li>
				<label for="female">Female</label>
				<input name="gender" value="female" id="female" type="radio">
			</li>
		</ul>
		
		<button>Submit</button>
	</form>

Use paragraphs for others

But **always use a label**:

> Web Content Accessibility Guidelines (WCAG) 2.0, Level AA: 1.4.5 Images of Text
> A paragraph was found without text in it. While this tends to have a low severity, it does create an unnecessary nuisance for users of screen readers who are likely to hear the announcement of the empty paragraph as they navigate through content. If this empty paragraph exists to behave as margin, use CSS for this purpose instead.

	<form action="">
		<p>
			<label for="some-input">Some input</label>
			<input id="some-input">
		</p>
		<p>
			<label for="other-input">Other input</label>
			<select id="other-input"></select>
		</p>
		<p>
			<label for="other-input2">Other input 2</label>
			<input id="other-input2" type="checkbox">
		</p>
		
		<button type="submit">Submit</button>
	</form>

mad-libs script like / natural language form interface:

	<form action="">
		<p>Hello. My <label for="name">name</label> is <input id="name">!</p>
		<p>I, <input id="name"><label for="name">(name)</label> of; <input id="city"><label>(Residence City or State)</label>...
	</form>

- http://www.w3.org/TR/html5/forms.html#forms and http://www.w3.org/TR/html5/grouping-content.html#the-p-element use `<p>` and `input` inside `label`.
- http://www.whatwg.org/specs/web-apps/current-work/multipage/forms.html#writing-a-form%27s-user-interface
- https://stackoverflow.com/questions/16875963/why-use-ol-and-ul-lists-for-label-and-input-elements-in-html5-forms
- https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/How_to_structure_an_HTML_form
- https://stackoverflow.com/questions/519234/why-use-definition-lists-dl-dd-dt-tags-for-html-forms-instead-of-tables
- [Marking up a search result list with HTML5 semantics - Stack Overflow](https://stackoverflow.com/questions/3255109/marking-up-a-search-result-list-with-html5-semantics)
- http://alistapart.com/article/prettyaccessibleforms
- https://stackoverflow.com/questions/2094344/is-it-wrong-to-use-paragraph-tags-for-html-for-inputs
- http://www.obiwankimberly.com/2011/05/27/i-shouldve-bet-money-on-using-paragraphs-in-forms/
- https://stackoverflow.com/questions/6934452/why-does-the-w3c-advise-wrapping-input-elements-in-p-tags
- https://stackoverflow.com/questions/774054/should-i-put-input-tag-inside-label-tag
- [Natural Language Form with Custom Input Elements](http://tympanus.net/codrops/2013/05/21/natural-language-form-with-custom-input-elements/)
- [Using the fieldset and legend elements | Accessibility](https://accessibility.blog.gov.uk/2016/07/22/using-the-fieldset-and-legend-elements/)
- (example of natural language form) [Simulateur de coût d'embauche](http://sgmap.github.io/cout-embauche/)

### Related inputs

Examples:

- date: year, month, day, hour, minute
- address: place nearby, building number, street, city name, zip/postal code, country, etc. (some fields are useless in some area)
- name: First name, middle name, last name, 

Instead use date input:

	<!-- format: yyyy-mm-dd -->
	<!-- native widget mostly supported by mobile browsers but not desktop browser other than Chrome (2015 q3) -->
	<!-- max="2014-01-01" can be added, but not work on all browsers (2015 q3) -->
	<label for="bday">Birthday</label><input id="bday" type="date" autocomplete="bday">

- [Accessible Date Input (and more) Using aria-labelledby | NC State University IT Accessibility Blog](http://accessibility.oit.ncsu.edu/blog/2011/06/22/accessible-date-input-and-more-using-aria-labelledby/)
- [Accessible Form Elements with Multiple Inputs Using aria-labelledby](http://accessibility.oit.ncsu.edu/training/forms/multiple-inputs.html)

### Multiselect component

- [How to Make Accessible Web Components — a Brief Guide](https://www.sitepoint.com/accessible-web-components/)

### Autocomplete

#### Native autocomplete

`autocomplete` attribute and `requestautocomplete();`

> The "off" keyword indicates either that the control's input data is particularly sensitive (for example the activation code for a nuclear weapon); or that it is a value that will never be reused (for example a one-time-key for a bank login) and the user will therefore have to explicitly enter the data each time, instead of being able to rely on the UA to prefill the value for him; or that the document provides its own autocomplete mechanism and does not want the user agent to provide autocompletion values.

- [Designing your website to work best with 1Password - 1Password Support](https://support.1password.com/compatible-website-design/)
- [HTML Standard](https://html.spec.whatwg.org/multipage/forms.html#autofill)
- [<input> - HTML | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-autocomplete)
- [» Autofill: What web devs should know, but don’t Cloud Four Blog](http://blog.cloudfour.com/autofill-what-web-devs-should-know-but-dont/)

- `autocomplete="off"` not work for login fields https://developer.mozilla.org/en-US/docs/Web/Security/Securing_your_site/Turning_off_form_autocompletion
- http://www.w3.org/TR/html5/forms.html#autofilling-form-controls:-the-autocomplete-attribute
- http://www.w3.org/html/wg/drafts/html/master/forms.html#autofilling-form-controls:-the-autocomplete-attribute
- [Help users checkout faster with Autofill](http://updates.html5rocks.com/2015/06/checkout-faster-with-Autofill)
- [» Autofill: What web devs should know, but don’t Cloud Four Blog](http://blog.cloudfour.com/autofill-what-web-devs-should-know-but-dont/)

#### Custom autocomplete

Aka value/word/option completion/suggestion

Pick a predefined value (suggest any value match the entered data), but allow to add freely any other value.

See also [Multiselect component](#Multiselect component) and [`autocomplete` attribute]()

> The search field
> 
> - The auto-suggest input must have a descriptive label
> - The input field must have a `role="combobox"` attribute
> - The input field must have an `aria-autocomplete` attribute
> - The input field must have an `aria-owns` attribute
> - The input field must have an `aria-activedescendant` attribute that changes value with each selection
> 
> Keyboard Access
> 
> - The auto-suggest must be able to be operated using only a keyboard
> - Focus must alxways be visible
> - Suggestions can be selected using _Up Arrow_ and _Down Arrow_ keys (wrapping through the text box whe, the top or bottom of the list is reached)
> - _Up Arrow_ and _Down Arrow_ keys move through suggestions highlighting the current option
> - _Enter_ key selects the hightlighted option and close the list
> - _ESC_ when suggesteions visible closes the list and leaves the user typed text in the textbox
> 
> Suggestions
> 
> - Avaiable suggestions must be displayed directly below the input field and come directly after the input field in the page source
> - Number of available suggestions must be announced to screen readers
> - Suggestions container has `role="listbox"` attribute
> - Individual suggestion has `role="option"` attribute and an `id` attribute with a unique id
> - When selected a suggestion has `aria-selected="true"`
— [@demicifci slide about auto-suggests at respond17](https://twitter.com/paulmsmith/status/860047704885526528)

- [alphagov/accessible-typeahead: A typeahead component, built to be accessible.](https://github.com/alphagov/accessible-typeahead)
- [Accessible Autocomplete](https://haltersweb.github.io/Accessibility/autocomplete.html)
- [alphagov/accessible-autocomplete: An autocomplete component, built to be accessible.](https://github.com/alphagov/accessible-autocomplete)
- [jQuery accessible autocomplete list (with ARIA) - By Nicolas Hoffmann and Aurélien Lévy](https://a11y.nicolas-hoffmann.net/autocomplet-list/)
- [Anatomy of an accessible auto suggest](https://codepen.io/ademcifcioglu/pen/xdOyXv)
- [Basic autocomplete (activedescendent)](https://codepen.io/goetsu/pen/wKYRvM/)
- [Easy ARIA Tip #7: Use “listbox” and “option” roles when constructing AutoComplete lists – Marco's Accessibility Blog](https://www.marcozehe.de/2014/03/11/easy-aria-tip-7-use-listbox-and-option-roles-when-constructing-autocomplete-lists/)

`datalist` element

	<label>Object:</label>
	<datalist id="object-list">
		<!--
		The backend should handle FormData with 2 values with same field name:
		`...&object=Apple&object=` or `...&object=&object=Apple`
		Depending datalist support. One for the select and the other for the input
		-->
		<select name="object">
			<option>Apple</option>
			<option>Bananna</option>
			<option>Cat</option>
		</select>
		<label>Or specify:</label>
	</datalist>
	<input list="object-list" name="object">

- [HTML 5 DataList Element with Fallback option for Old Browsers](http://www.devcurry.com/2011/08/html-5-datalist-element-with-fallback.html)
- [Adactio: Journal—The design of datalist](https://adactio.com/journal/4272/)
- [Bug 28033 – HTML5 Datalist Element and Input Element's List Attribute Dead on Arrival](https://www.w3.org/Bugs/Public/show_bug.cgi?id=28033)
- [Awesomplete: Ultra lightweight, highly customizable, simple autocomplete, by Lea Verou](http://leaverou.github.io/awesomplete/)

##### AJAX selector or datalist

Country division selector

	<p>
		<label for="country">Country:</label>
		<select id="country" aria-controls="division postal-code">
			<option>Country 1</option>
			<option>Country 2</option>
		</select>
	</p>
	
	<p>
		<!-- Postal code could be cleared by country change -->
		<!-- Postal code could control division with its value (parser depends on selected country) -->
		<label for="postal-code">Postal code:</label>
		<input id="postal-code">
	</p>
	
	<p>
		<!-- administrative/political division: State (US, Mexico, Australia), Province (Canada), Region (Japan, France) -->
		<label for="division">Division:</label>
		<select id="division" aria-live="polite" aria-atomic="true">
			<!-- Options will be added later, dynamically with JS. -->
			<!-- Don't forget to set "aria-busy" attribute: `aria-busy=true` when loading and `aria-busy=false` when it's complete -->
			<!-- and aria-invalid=true if an error -->
			<!--
			<option>Division 1</option>
			<option>Division 2</option>
			-->
		</select>
	</p>

- https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions (interactive, AJAX, live content)
- [Redesigning The Country Selector - Smashing Magazine](http://www.smashingmagazine.com/2011/11/10/redesigning-the-country-selector/)

### `output` element

	<input id="in">
	<output for="in"></output>

- [HTML/Elements/output - W3C Wiki](https://www.w3.org/wiki/HTML/Elements/output)
- [The output element | HTML5 Doctor](http://html5doctor.com/the-output-element/)

### Tri state of checkbox

Require script to define it

	checkbox.indeterminate = true;

	input[type=checkbox]:indeterminate

- [:indeterminate - CSS | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/:indeterminate)
- [<input type="checkbox"> - HTML | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox)

### Target can be defined to forms

Aka open POST in a new tab.

	<form action="http://othersite.com" method="post" target="_blank">
		<input type="submit">
	</form>

### Disable autofill

(Aka disable prepopulation of forms by the browser)

But keep autocomplete, for form where password field with wrong data: login credentials autofilled on an other page with a form, form where credentials are not required (admin add a new user form, profile update form where the password field can be update only if not empty), multiple password fields, etc.

Recent browser ignore `autocomplete="off"` for user credentials (Firefox 38+, Google Chrome 34+, IE 11+).

Some workarounds:

- Use a correct value like `autocomplete="new-password"` (password field). Else use `autocomplete="off"` on form or on the field. 
- Use header like `Cache-Control: no-store` (`no-cache`, `private` too?)
- Use a delayed script (timeout) and after page load to clear data (revert value to defaultValue)
- Use a script after page load to select all auto filled fields (webkit only: `input:-webkit-autofill`) and revert value to default

		// https://stackoverflow.com/a/41530164/470117
		const style = document.createElement("style");
		style.textContent = "@keyframes autofillstart{from{}to{}}@keyframes autofillend{from{}to{}}input:-webkit-autofill{animation-name: autofillstart}input:not(:-webkit-autofill){animation-name: autofillend}";
		document.body.addEventListener("animationstart", function(event){
			if(event.animationName !== "autofillstart" && event.animationName !== "autofillend") return;
			var autofill = event.animationName === "autofillstart";
			// do something: event.target.value = event.target.defaultValue;
			/*
			var changeEvent = document.createEvent('Event');
			changeEvent.initEvent('change', true, false);
			event.target.dispatchEvent(changeEvent);
			*/
		});
		document.body.appendChild(style);
		
- Use an honey pot: Add dummy a text and a password field (given name doesn't matter) before any other fields. These fields should be hidden: `style="display:none"`
- Some people use readonly/disable attr (and update when focus), create fields onfly

- [How to Turn Off Form Autocompletion - Web security | MDN](https://developer.mozilla.org/en-US/docs/Web/Security/Securing_your_site/Turning_off_form_autocompletion#The_autocomplete_attribute_and_login_fields)
- [input - How can I prevent Firefox's Autocomplete? - Stack Overflow](https://stackoverflow.com/questions/682439/how-can-i-prevent-firefoxs-autocomplete)
- [html - Disabling Chrome Autofill - Stack Overflow](https://stackoverflow.com/questions/15738259/disabling-chrome-autofill/15917221#15917221)
- [Issue 352347 - chromium - Don't autofill passwords where confirmation is required - An open-source project to help move the web forward. - Google Project Hosting](https://code.google.com/p/chromium/issues/detail?id=352347)
- [web application - Should websites be allowed to disable autocomplete on forms or fields? - Information Security Stack Exchange](http://security.stackexchange.com/questions/49326/should-websites-be-allowed-to-disable-autocomplete-on-forms-or-fields)

### Field type

Don't use number type thing that use digit like identifier (credit card number, CCV, ISBN, barcode, activation/product key, etc.), postcode, date, phone number, social security number, etc.

Instead use `type="tel"`, `type="email"`, `type="url"`. If no type match, use `type="text"` with `pattern` attribute and `inputmode` attribute if needed (`numeric`).

- [I Wanted To Type a Number | Filament Group, Inc., Boston, MA](https://www.filamentgroup.com/lab/type-number.html)
- [Payment card number — Wikipedia](https://en.wikipedia.org/wiki/Payment_card_number)
- [Identifier — Wikipedia](https://en.wikipedia.org/wiki/Identifier)

Note: Maybe you can use `<input type="number" value="0.00">` to show the user he could use floating point number

Note: color input can have datalist for color palette

Input date value use [RFC 3339](http://tools.ietf.org/html/rfc3339) format. YYYY-MM-DD **with 0 padded numbers**.

	<input type="date" value="<?php echo date("Y-m-d");?>">

### Tabular form 

Aka booking form, book an appointment

- [Form Inside Table Demo](http://adamsilver.github.io/kitty/src/demos/FormTable/)

### Rating field

Star rating

Use radios in a fieldset

- http://lunarlogic.github.io/starability/ https://github.com/LunarLogic/starability
- [Accessible star rating widget with pure CSS | Lea Verou](http://lea.verou.me/2011/08/accessible-star-rating-widget-with-pure-css/)

### Search form

	<form role="search">
		<input type="search" aria-label="search text" size="20">
		<input type="submit" value="Search"">
	</form>

Note: according to step 3 of “[General Principles of Landmark Design](https://w3c.github.io/aria-practices/#general-principles-of-landmark-design),” if there are multiple search landmarks on the same page, each one should have a unique label—provided via the `aria-label` attribute, or by referencing the landmark’s heading via the `aria-labelledby` attribute.

- [WAI-ARIA Authoring Practices 1.1](https://w3c.github.io/aria-practices/#aria_lh_search) - Search landmarks

## `a` element

> When you link to something, make sure the group of words you link to work as a standalone thing. [...] If you remove the words around the link, someone should be able to predict the type of content they’re going to get
— [How to make blog posts accessible | GDS Digital Engagement](https://gdsengagement.blog.gov.uk/2016/11/28/how-to-make-blog-posts-accessible/)

## `article` element

All things need a inclusion? (a product, a blog post, a comment, a part of other document, a forum post, a magazine or newspaper article)

The teaser should also be an `article` – the teaser `article` and the fulltext `article` are different `article`s, although they refer to the same entity.

Don't use unorder list for list of articles, news, items. Just use `<article><!--content--></article><article><!--content--></article><article><!--content--></article>`.

Use dedicated elements like `figure` for a graphical element with a legend, etc.

	<article>
		<h1>Product #1</h1>
		
		<p>Description blah...</p>
		
		<!-- attributes -->
		<dl>
			<dt>Color</dt>
			<dd>Red</dd>
			<dt>Size</dt>
			<dd>2 x 3 x 4cm</dd>
		</dl>
		
		<!-- actions, etc. -->
		<footer>
			<a href="/delete">Delete</a>
		</footer>
	</article>

- http://www.w3.org/TR/2013/CR-html5-20130806/sections.html#the-article-element
- http://html5doctor.com/the-article-element/

## `i` vs `em` vs `b` vs `cite` vs `strong`

	Our favorite cruise was on the <i>Explorer of the Seas</i><!-- italicize the name of a ship -->,
	which we read about in <cite>Cruising</cite><!-- reference the name of a publication --> magazine,
	and we <em>loved</em><!-- emphasize a feeling --> it.
	
	(<b>Note:</b><!-- start a note with bolded text --> This was before everyone got all sick
	and was throwing up <strong>everywhere</strong><!-- make a strong statement -->.)

## `i` element

Separate tone or mood, alternate voice, voiceover
Thoughts and technical terms, an idiomatic phrase from another language, a taxonomic designation
Usally used in conjonction with quotes

http://html5doctor.com/element-index/#i

Can be the equivalent of usage of [Angle brackets](https://en.wikipedia.org/wiki/Bracket#Angle_brackets): `⟨word⟩`

## `b` element

Represents a span of text to be stylistically offset from the normal prose without conveying any extra importance
Identifies text that is stylistically different than normal text, but doesn't have any semantically different meaning
Keywords in a document abstract or product names in a review

> How is this different than using `<span>`? The key is that `<b>` communicates a lack of semantic meaning.

- http://html5doctor.com/element-index/#b

## `em` element

Emphasized text, something you’d pronounce differently
Emphasised pronunciation on a word that can change the nuance of a sentence

http://html5doctor.com/element-index/#em

## `strong` element

Strongly emphasized text
Represents strong importance for its contents

	<strong>Warning</strong>. This dungeon is dangerous. <strong>Avoid the ducks.</strong> Take any gold you find.

http://html5doctor.com/element-index/#strong

Use `mark` element for [quotation emphasis](#`mark` element)

## `s` element

	<p>Sale on now!</p>
	<p><s>Get up to 25% off</s></p>
	<p><strong>Now down to 50% off</strong></p>

> The `s` element represents contents that are no longer accurate or no longer relevant.

## `sub` and `sup`

> 	<p>The most beautiful women are
> 	<span lang="fr"><abbr>M<sup>lle</sup></abbr> Gwendoline</span> and
> 	<span lang="fr"><abbr>M<sup>me</sup></abbr> Denise</span>.</p>
> 
> the `sub` element is used to represent the subscript that identifies the variable in a family of variables:
> 
> 	<p>The coordinate of the <var>i</var>th point is
> 	(<var>x<sub><var>i</var></sub></var>, <var>y<sub><var>i</var></sub></var>).
> 	For example, the 10th point has coordinate
> 	(<var>x<sub>10</sub></var>, <var>y<sub>10</sub></var>).</p>
— [4 The elements of HTML | HTML 5.1 Nightly](http://www.w3.org/html/wg/drafts/html/master/semantics.html#the-sub-and-sup-elements)

## `dfn`

> In the following fragment, the term "Garage Door Opener" is first defined in the first paragraph, then used in the second. In both cases, its abbreviation is what is actually displayed.
> 
> 	<p>The <dfn><abbr title="Garage Door Opener">GDO</abbr></dfn>
> 	is a device that allows off-world teams to open the iris.</p>
> 	<!-- ... later in the document: -->
> 	<p>Teal'c activated his <abbr title="Garage Door Opener">GDO</abbr>
> 	and so Hammond ordered the iris to be opened.</p>
> 
> With the addition of an a element, the reference can be made explicit:
> 
> 	<p>The <dfn id=gdo><abbr title="Garage Door Opener">GDO</abbr></dfn>
> 	is a device that allows off-world teams to open the iris.</p>
> 	<!-- ... later in the document: -->
> 	<p>Teal'c activated his <a href=#gdo><abbr title="Garage Door Opener">GDO</abbr></a>
> 	and so Hammond ordered the iris to be opened.</p>
— [4 The elements of HTML | HTML 5.1 Nightly](http://www.w3.org/html/wg/drafts/html/master/semantics.html#the-dfn-element)

## `mark` element

Use `mark` element for

- quotation emphasis
- search results hightlights
- a code fragment a refered by a preceding paragraph

- [Draw attention with mark | HTML5 Doctor](http://html5doctor.com/draw-attention-with-mark/)
- [HTML 5.2: 4.5. Text-level semantics](http://w3c.github.io/html/textlevel-semantics.html#the-mark-element)

## List

TODO Create to make a flowchart diagram for choices

> Lists are used to group related pieces of information together, so they are clearly associated with each other and easy to read. [...]
> Lists are good from a structural point of view as they help create a well-structured, more accessible, easy-to-maintain document.
— [HTML lists - W3C Wiki](http://www.w3.org/wiki/HTML_lists)

A list enumerate (summarily, w/ or w/o order) items of a collection for a global view of this collection.

When you use a list: for an **enumeration** (more than one item) of short items; less than a phrase, small images, icons, links, index, table of content, listing, references (use `<ol>`), choices (`<input type="radio">` and `<input type="checkbox">`), etc.

For other cases:

- Use table for mutliple items with lot of keys (non-null) in common with a row for each item and `<thead>` for key listing (see also [Key-value pairs]())
- Use `<p>`s (for each texts chunks or images or videos), `<article>`s (title + body), etc. when items representation use a large portion of UI or are complexe: multiple lines, title + body, full image, etc.
- Use `role="list"` and `role="listitem"`

`<ol>` represents a sequence, whereas `<ul>` represents a set.

Order in `<ol>` can be controlled by using `<ol start="10">`, `<ol reversed>` and `<li value="15">`

See also:

- (no `<p>` in `<li>`) [jquery - <ol> sub-section with <p> in its <li>'s - Stack Overflow](https://stackoverflow.com/questions/23914129/ol-sub-section-with-p-in-its-lis)
- [Section]()
- [`nav` element]()
- [Enumeration — Wikipedia](https://en.wikipedia.org/wiki/Enumeration)
- [Listicle — Wikipedia](https://en.wikipedia.org/wiki/Listicle)
- [List (abstract data type) — Wikipedia](https://en.wikipedia.org/wiki/List_(abstract_data_type))

## Key-value pairs

Glossary, description list, metadata, **key-value pairs: keyword(s) / name(s)** with one or more definition

- http://html5doctor.com/the-dl-element/
- https://stackoverflow.com/questions/22062434/html-semantics-for-displaying-form-like-data/
- https://stackoverflow.com/questions/8900571/two-column-table-or-dl
- http://www.w3.org/html/wg/drafts/html/master/grouping-content.html#the-dl-element (Examples)

### `dl` element (definition list)

	<dl>		 
		<dt>Name: </dt>
		<dd>John Don</dd>
			 
		<dt>Age: </dt>
		<dd>23</dd>
				 
		<dt>Gender: </dt>
		<dd>Male</dd>
				 
		<dt>Day of Birth:</dt>
		<dd>12th May 1986</dd>
	</dl>

Pro.: multiple keys or multiple values.
Pro.: wrapper (`<div>`) can be used to group multiple elements (`dt`s and `dd`s). See [Allow \<div\> around each \<dt\>\<dd\> group in \<dl\> (#1945) · whatwg/html@5454d70](https://github.com/whatwg/html/commit/5454d702e0262749aba55576dda32c48e0e498f0)

Key-value can be on same line (using `float: left` and `clear: left;` for dt) and pseudo element on each first `dt` or last `dd`

Don't use it for [Conversations](#Conversations), use `p` instead.

### `p` element
   
	<p>Name: John Don</p>
	<p>Age: 23</p>
	<p>Gender: Male</p>
	<p>Day of Birth: 12th May 1986</p>

### `table` element

	<table>
		<tr>
			<th scope="row">Name: </th>
			<td>John Don</td>
		</tr>
		<tr>
			<th scope="row">Age: </th>
			<td>23</td>
		</tr>
		<tr>
			<th scope="row">Gender: </th>
			<td>Male</td>
		</tr>	
		<tr>
			<th scope="row">Day of Birth:</th>
			<td>12th May 1986</td>
		</tr>
	</table>

Pro.: May be less adapted semantically. Can be used for complex styles (horizontal list, where `th` is upper `td`).
Con.: wrapp each pairs, but no multiple keys or values

### `ul` element (unordered list)

	<ul>
		<li>Phone: 613-000-1111</li>
		<li>Fax: 613-000-1112</li>
		<li>E-mail: me@somewhere.com</li>
		<li>Website: www.mysite.com</li>
	</ul>

Pro.: Simple.
Con.: Semantically correct, but maybe too general, no mutliple keys or values

Can use the table layout by adding a wrapper for each keys and values.

### Simplified

For the last example could be simplified to:

	<p>
		613-000-1111<br>
		613-000-1112 (Fax)<br>
		me@somewhere.com<br>
		www.mysite.com
	</p>

Since the value format decribe itself (you can easily identify a phone number, an email address, a website address, a postal address, etc.).

## Tables

- https://stackoverflow.com/questions/3247370/semantic-html-markup-for-complex-tables
- http://webaim.org/techniques/tables/data
- http://www.w3.org/TR/html51/tabular-data.html#table-examples
 
	<table>
		<thead>
			<tr>
				<th>Col 1</th>
				<th>Col 2</th>
			</tr>
		</thead>
		<tbody>
			<tr>
				<td>Data 1</td>
				<td>Data 2</td>
			</tr>
			<tr>
				<td>Data 3</td>
				<td>Data 4</td>
			</tr>
		</tbody>
	</table>

### `tfoot` element

Column summaries:
a total line, footnotes for data or repeat header (for long tables)

## `hr` element

> The hr element represents a paragraph-level thematic break, e.g. a scene change in a story, or a transition to another topic within a section of a reference book.
> — [HTML Standard](https://html.spec.whatwg.org/multipage/grouping-content.html#the-hr-element)

Is the same semantically as `section`. But is more for thematic breaks, such as separating different topics within a section of prose, or between scenes in a novel

- [The small & hr elements | HTML5 Doctor](http://html5doctor.com/small-hr-element/#element-hr)

## `main` element

> The main content of the body of a document or application. The main content area consists of content that is directly related to or expands upon the central topic of a document or central functionality of an application.

> The main content area of a document includes content that is unique to that document and excludes content that is repeated across a set of documents such as site navigation links, copyright information, site logos and banners and search forms (unless the document or applications main function is that of a search form).
- [4 The elements of HTML | HTML 5.1](http://www.w3.org/TR/html51/semantics.html#the-main-element)

"→ skip to content", without global header, aside and footer

Print only the main element in print stylesheet.

More than one main element is allowed, but only on must be active. Other ones must use the `hidden` attribute.

- [L'élément \<main\> - Alsacreations](https://www.alsacreations.com/actu/lire/1776-element-main-html5.html)
- [The main element | HTML5 Doctor](http://html5doctor.com/the-main-element/)
- http://www.w3.org/html/wg/wiki/User:Sfaulkne/main-usecases
- [Use Only One <main> on a Page | Adrian Roselli](http://adrianroselli.com/2015/09/use-only-one-main-on-a-page.html)

## `abbr` element

For non common abbreviations only. Title is not always accessible, use [footnotes](#footnotes) instead.

Don't use it for:

- i.e.: that is, in other words)
- etc.: et cetera desunt/et ainsi de suite)
- c.f.
- c.-à-d
- ASAP: As Soon As Possible/aussi vite que possible)
- B.C.: before Christ
- some common acronyms like UNESCO or HTML, PDF, AIDS, NATO, UN, EU, ABS, OVNI (FR), Benelux, laser, radar...

But (could be) required for:

- group (company, VIP) might not well know by the reader: MTA (US), RATP (FR), MEDEF (FR), JFK (US), PPDA (FR), W3C (tech), IEEE (tech)...

- See [Labelling](#Labelling)
- [Utilisabilité des <abbr> (tactile et vocale) (avec tweets) · tetue · Storify](https://storify.com/tetue/utilisabilite-des-abbr-tactile-et-vocale)
- [Comment utiliser <abbr> en HTML?](http://fvsch.com/code/utiliser-abbr/)
- [Acronym - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Acronym)
- [The abbr element | HTML5 Doctor](http://html5doctor.com/the-abbr-element/)

## `noscript` element

> The noscript element is a blunt instrument. Sometimes, scripts might be enabled, but for some reason the page's script might fail. For this reason, it's generally better to avoid using noscript, and to instead design the script to change the page from being a scriptless page to a scripted page on the fly, as in the next example
— [HTML/Elements/noscript - W3C Wiki](http://www.w3.org/wiki/HTML/Elements/noscript)

It's could be required to duplicate it with an HTML comment (for compatibility reason with IE7-8).

	<noscript><img src="image.jpg"></noscript>

- [`<noscript>` and search engines](Web#`<noscript>` and search engines)
- [Lazyload and async load stylesheets and imgs](JavaScript#Lazyload and async load stylesheets and imgs)

## Quote

`<blockquote>` as block quote and `<q>` as inline quote

TODO: How to markup a picture of the author before the blockquote?

Recommended by WHATWG:

	<blockquote>
	 <p>I contend that we are both atheists. I just believe in one fewer
	 god than you do. When you understand why you dismiss all the other
	 possible gods, you will understand why I dismiss yours.</p>
	</blockquote>
	<p>— Stephen Roberts</p>

	<figure>
	  <blockquote>
		<p>For writing maintainable and scalable HTML documents.</p>
	  </blockquote>
	  
	  <figcaption>— HTML Best Practices</figcaption>
	</figure>

	<figure>
	 <blockquote>
	  <p>The truth may be puzzling. It may take some work to grapple with.
	  It may be counterintuitive. It may contradict deeply held
	  prejudices. It may not be consonant with what we desperately want to
	  be true. But our preferences do not determine what's true. We have a
	  method, and that method helps us to reach not absolute truth, only
	  asymptotic approaches to the truth — never there, just closer
	  and closer, always finding vast new oceans of undiscovered
	  possibilities. Cleverly designed experiments are the key.</p>
	 </blockquote>
	 <figcaption>Carl Sagan, in "<cite>Wonder and Skepticism</cite>", from
	 the <cite>Skeptical Inquirer</cite> Volume 19, Issue 1 (January-February
	 1995)</figcaption>
	</figure>

	<p>He began his list of "lessons" with the following:</p>
	<blockquote>One should never assume that his side of
	the issue will be recognized, let alone that it will
	be conceded to have merits.</blockquote>
	<p>He continued with a number of similar points, ending with:</p>
	<blockquote>Finally, one should be prepared for the threat
	of breakdown in negotiations at any given moment and not
	be cowed by the possibility.</blockquote>
	<p>We shall now discuss these points...	

- [HTML Standard](https://html.spec.whatwg.org/multipage/semantics.html#the-blockquote-element)

Recommended by W3C:

	<blockquote class="twitter-tweet">
		<p>♥ Bukowski in <a href="https://twitter.com/search?q=%23HTML5&src=hash">#HTML5</a> spec examples
		<a href="http://t.co/0FIEiYN1pC">http://t.co/0FIEiYN1pC</a></p><cite>— karl dubost (@karlpro) 
		<a href="https://twitter.com/karlpro/statuses/370905307293442048">August 23, 2013</a></cite>
	</blockquote>

- [4.4 Grouping content — HTML5](https://www.w3.org/TR/html5/grouping-content.html#the-blockquote-element)
- [4.5 Text-level semantics — HTML5](https://www.w3.org/TR/html5/text-level-semantics.html#the-cite-element)
- [HTML/Elements/blockquote - W3C Wiki](https://www.w3.org/wiki/HTML/Elements/blockquote)

Other:

	<blockquote>
		<p>The small element represents so-called “small print” such as legal disclaimers and caveats.</p>
		<footer><cite><a href="http://dev.w3.org/html5/markup/small.html" title="HTML5: small – small print (CHANGED)">W3C specification</a></cite></footer>
	</blockquote>

- [Quoting and citing with <blockquote>, <q>, <cite>, and the cite attribute | HTML5 Doctor](http://html5doctor.com/blockquote-q-cite/)

## `code`, `kbd`, `var` and `samp`

Element		Purpose 			Example 
`code`		Computer code		`The <code>fruitdb</code> program can be used for tracking fruit production.`
`var`		Variables			`If there are <var>n</var> fruit in the bowl, at least <var>n</var>÷2 will be ripe.`
`samp`		Computer output		`The computer said <samp>Unknown error -3</samp>.`
`kbd`		User input			`Hit <kbd>F1</kbd> to continue.`

	<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd>

	<pre><samp>mike:mysite mike$ <kbd>git status</kbd>
	
	# On branch master
	nothing to commit (working directory clean)
	mike:mysite mike$</samp></pre>

> `<var>` is not suitable for (non-dynamic) prices

- [demosthenes.info – Code and Keys in HTML: Using the code, var, samp and kbd elements](http://demosthenes.info/blog/1019/Code-and-Keys-in-HTML-Using-the-code-var-samp-and-kbd-elements)
- [4.5 Text-level semantics — HTML5](https://www.w3.org/TR/html5/text-level-semantics.html#usage-summary)
- [semantics - Which HTML5 tags are more appropriate for money? - Stack Overflow](https://stackoverflow.com/questions/9632311/which-html5-tags-are-more-appropriate-for-money/9838798#9838798)

## Non-breaking chars

For space `&nbsp;`:

- Units: `12&nbsp;m/s`
- Time: `8&nbsp;PM`
- Proper nouns: `Dairy&nbsp;Queen`

https://en.wikipedia.org/wiki/Non-breaking_space#Non-breaking_behavior

For hyphen `&#8209;`

For breaking oportunity, use `<wbr>` or `&#8203;`. See [line break](Text#Line break)

## Tagline & subheader

Or subheading, subtitle, alternative title, sub header, sub title

> h1–h6 elements must not be used to markup subheadings, subtitles, alternative titles and taglines unless intended to be the heading for a new section or subsection.
— [4.3 Sections — HTML5](https://www.w3.org/TR/html5/sections.html#headings-and-sections), [4.12 Common idioms without dedicated elements — HTML5](https://www.w3.org/TR/html5/common-idioms.html#common-idioms)

> In the following example the subtitle of a book is on the same line as the title separated by a colon

	<h1>The Lord of the Rings: The Two Towers</h1>

> In the following example part of an album title is included in a `span` element, allowing it to be styled differently from the rest of the title.

	<style>
		.sub {display:block; font-style:italic;}
	</style>
	
	<h1>
		The Mothers 
		<span class="sub">Fillmore East - June 1971</span> 
	</h1>

> In the following example the title and strapline for a news article are grouped using a `header` element. The title is marked up using a `h2` element and the strapline is in a `p` element.

	<header>
		<p>Magazine of the Decade</p>
		<h1>THE MONTH</h1>
		<p>The Best of UK and Foreign Media</p>
	</header>

- [4 The elements of HTML | HTML 5.1](http://www.w3.org/TR/html51/semantics.html#sub-head)
 
	<style>
		.sep {display: block; position: absolute; overflow: hidden;width:1px; height: 0px; padding-top: 1px}/*See [Hide graphicaly an element](CSS#Hide graphicaly an element)*/
		.sub {display:block; font-style:italic;}
	</style>
	
	<h2>The Lord of the Rings<span class="sep">: <span><span class="sub">The Two Towers</span></h2>

See [`h1`-`h6`](#`h1`-`h6`) and [`header` element](#header-element)

## Breadcrumb

Aka fil d'ariane (FR)

> Authors are encouraged to markup bread-crumb navigation as a list. The `nav` element can be used to mark the list containing links as being a navigation block.
— [4 The elements of HTML | HTML 5.1](http://www.w3.org/TR/html51/semantics.html#rel-up)

> Note: The use of the right angle bracket symbol ">" to indicate path direction is discouraged as its meaning, in the context used, is not clearly conveyed to all users.

Use the `→` char instead.

	<nav>
		<ul>
			<li><a href="/">Main</a> →</li> 
			<li><a href="/products/">Products</a> →</li> 
			<li><a href="/products/dishwashers/">Dishwashers</a> →</li> 
			<li><a aria-current="location">Second hand</a></li>
		</ul>
	</nav>

Some peoples use only a series of links in a paragraph ([in a previous - draft version of HTML5.1](http://dev.w3.org/html5/spec-author-view/common-idioms-without-dedicated-elements.html#rel-up)):

	<nav>
		<p>
			<a href="/">Main</a> &gt;
			<a href="/second-hand/">Second hand</a> &gt;
			<a aria-current="location">Dishwashers</a>
		</p>
	</nav>

... or with hierachical lists:

	<nav>
		<ul>
			<li>
				<a href="#">Top Level</a>
				<ul>
					<li>
						<a href="#">Second Level</a>
						<ul>
							<li>
								<a href="#">Third Level</a>
								<ul>
									<li><a aria-current="location">Current Item</a></li>
								</ul>
							</li>
						</ul>
					</li>
				</ul>
			</li>
		</ul>
	</nav>

- [Exploring Markup for Breadcrumbs | CSS-Tricks](https://css-tricks.com/markup-for-breadcrumbs/)
- [Breadcrumbs   |   Structured Data   |   Google Developers](https://developers.google.com/structured-data/breadcrumbs)
- [BreadcrumbList - schema.org](http://schema.org/BreadcrumbList)
 
	<body itemscope itemtype="http://schema.org/WebPage">
		<nav itemprop="breadcrumb" itemscope itemtype="http://schema.org/BreadcrumbList">
			<ul>
				<li itemprop="itemListElement" itemscope itemtype="http://schema.org/ListItem">
					<a class="belm-bcrumb__link" href="" itemprop="item"><span itemprop="name" rel="index">Accueil</span></a>
					<span class="belm-bcrumb__sep"> →</span>
					<meta itemprop="position" content="1">
				</li>
				<li class="belm-bcrumb__item" itemprop="itemListElement" itemscope
					itemtype="http://schema.org/ListItem">
					<a class="belm-bcrumb__link" href="" rel="self" itemprop="item"><span itemprop="name">My account</span></a>
					<meta itemprop="position" content="2">
				</li>
			</ul>
		</nav>
	</body>

## `nav` element

	<nav aria-label="Search navigation">...

> Intended for major navigation information. A group of links grouped together isn’t enough reason to use the nav element. Site-wide navigation, on the other hand belongs in a nav element.

- major navigation
- Table of Contents
- Previous/next buttons (or pagination). **Note: don't forget `rel="next"` or `rel="prev"`, and `accesskey="."`**
- (if it's important to the navigation of the site) Search form
- (if breadcrumb trail is an important navigation aid, specialy on large sites) [Bread crumbs]
- (potential) Skip links ("Skip content" and "skip navigation")

Use `ul` and `li` for to list links (`a`), and set `aria-current="page"` for current page

But not for:

- sponsors/ advertisers links

- https://stackoverflow.com/questions/5544885/should-i-use-uls-and-lis-inside-my-navs
- http://css-tricks.com/navigation-in-lists-to-be-or-not-to-be/
- [1.6 Structurer les menus de navigation avec des listes | AcceDe Web](http://www.accede-web.com/notices/html-css-javascript/1-structure/1-6-menus-navigation-listes/)

## Block level links (anchors, `a`, block link)

HTML5 allow to wrap multiple elements with a link

But we can't do it to `tr` (table row). That require a little bit of JS emulate a click on the (first?) link in the row

http://wiki.whatwg.org/wiki/FAQ#HTML_should_support_href_on_any_element.21

> 	<aside class="advertising">
> 		<h1>Advertising</h1>
> 		<a href="http://ad.example.com/?adid=1929&amp;pubid=1422">
> 			<section>
> 				<h2>Mellblomatic 9000!</h2>
> 				<p>Turn all your widgets into mellbloms!</p>
> 				<p>Only $9.99 plus shipping and handling.</p>
> 			</section>
> 		</a>
> 		<a href="http://ad.example.com/?adid=375&amp;pubid=1422">
> 			<section>
> 				<h2>The Mellblom Browser</h2>
> 				<p>Web browsing at the speed of light.</p>
> 				<p>No other browser goes faster!</p>
> 			</section>
> 		</a>
> 	</aside>
— http://dev.w3.org/html5/spec-preview/the-a-element.html#the-a-element

Link as wrapper / block-level link:

	<article>
		<a href="story1.html">
			<h3>Bruce Lawson voted sexiest man on Earth</h3>
			<p><img src="bruce.jpg" alt="gorgeous lovebundle. ">A congress representing all the planet's women unanimously voted Bruce Lawson as sexiest man alive.</p>
			<p>Read more</p>
		</a>
	</article>

- [“Block-level” links in HTML5 | HTML5 Doctor](http://html5doctor.com/block-level-links-in-html-5/)

## `section` element

> Used for grouping together thematically-related content. Sounds like a div element, but its not. The div has no semantic meaning. Before replacing all your div’s with section elements, always ask yourself, “Is all of the content related?”

> A general rule is that the section element is appropriate only if the element’s contents would be listed explicitly in the document’s outline.

> `section` is a blob of content that you could store as an individual record in a database.

> The theme of each section should be identified, typically by including a heading (h1-h6 element) as a child of the section element.

> A List of DOs…
> 
> DO use section for each individual section of a tab switcher or content slider (if an unordered list isn’t needed)
> DO use section to divide a lengthy “terms and conditions” (or similar) page into numbered sections
> DO nest section elements if necessary (as you might do with the “terms and conditions” page)
> 
> A List of DON’Ts…
> 
> DON’T use section to divide content from the header and footer; use div instead (see the doctor)
> DON’T use section to wrap a tab switcher for DOM manipulation or styling
> DON’T use section for sidebar or other tangentially-related content boxes; use aside instead
> DON’T use section just to add a border or drop shadow around something; use div instead
> DON’T use section for the wrapper when implementing faux columns; again, use div instead
> DON’T use section to nest elements when trying to avoid IE6′s float double-margin bug (or a similar layout-related issue); again, use div
> DON’T use section to hold an individual author bio on a blog post or news article; use aside instead
— http://www.impressivewebs.com/html5-section/
- [Sectioning Content in HTML5 - div or section or article? | bitsofcode](http://bitsofco.de/2015/sectioning-content-in-html5/)

- https://stackoverflow.com/questions/7173558/html5-section-inside-unordered-list
- http://html5doctor.com/the-section-element/
- http://gsnedders.html5.org/outliner/

## `figure` element

	<figure>
		<img src="juliana.jpg" alt="Juliana Bicycles">
		<figcaption>Juliana Bicycles treats content chunks more visually.</figcaption>
	</figure>


	<figure class="code" id="figure1">
		<pre><code class="language-markup">&lt;label for="firstname"&gt;First name:&lt;/label&gt;
	&lt;input type="text" id="firstname"&gt;
	&lt;label for="lastname"&gt;Last name:&lt;/label&gt;
	&lt;input type="text" id="lastname"&gt;</code></pre>
		<figcaption><b>Figure 5.1:</b> Labels are visually associated by proximity with text input fields. In code, labels are programmatically connected using the <code>&lt;label&gt;</code> element, the <code>“for”</code> attribute, and the input field’s <code>“id”</code> attribute making the connection.</figcaption>
	</figure>

	<figure class="quote" id="figure6">
		<blockquote>
			<p><b>User:</b> I’d like to place an order. Here’s all my information.</p>
			<p><b>Your site:</b> Thanks. Got it. We’ll send this to you within three days.</p>
		</blockquote>
	</figure>

Image-map style annotated image (flickr like picture annotations):

	<figure>
		<img src="bike.jpg" alt="Photograph of me on my bike">
		
		<figcaption>
			<b>Things to note:</b>
		
			<ul>
				<!-- Positions of the list-items. These need defining inline. -->
				<li style="top:255px; left:150px;">Helmet.</li>
				<li style="top:420px; left:140px;">Ruptured ligaments in my ankle.</li>
				<li style="top:480px; left:130px;">Low pressures.</li>
				<li style="top:390px; left:325px;">The trailer I just jumped from.</li>
			</ul>
			
			<i>Photo by Suzanna Haworth</i>
		</figcaption>
	</figure>

For infographic: bullet point lists are a good way, alternative way to sum up the information conveyed in an infographic

## `img` element

Always use alt attribute (at least empty value)

	<p><img src="about:blank" alt=""></p>

Empty src is disallowed, use `src="about:blank"` instead (or "#", see [Data types (common microsyntaxes) - HTML5](http://w3c.github.io/html-reference/datatypes.html#common.data.uri.non-empty), but will create a network request).

## `pre` element

- Including an e-mail, with paragraphs indicated by blank lines, lists indicated by lines prefixed with a bullet, and so on.
- Including fragments of computer code, with structure indicated according to the conventions of that language.
- Displaying ASCII art.
 
	<p>This is the <code>Panel</code> constructor:</p>
	<pre><code>function Panel(element, canClose, closeHandler) {
	  this.element = element;
	  this.canClose = canClose;
	  this.closeHandler = function () { if (closeHandler) closeHandler() };
	}</code></pre>

> The pre element represents a block of preformatted text, in which structure is represented by typographic conventions rather than by elements.
> [...]
> To represent a block of computer code, the pre element can be used with a code element; to represent a block of computer output the pre element can be used with a samp element. Similarly, the kbd element can be used within a pre element to indicate text that the user is to enter.
— http://www.w3.org/TR/html5/grouping-content.html#the-pre-element

## Non-breaking space

- [L’espace insécable chez Vincent Valentin.](http://vincent-valentin.name/articles/l-espace-insecable)
- [Espace insécable — Wikipédia](https://fr.wikipedia.org/wiki/Espace_ins%C3%A9cable)
- [Non-breaking space - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Non-breaking_space)

## Secondary content, side comments

legal disclaimers and caveats, legalese (copyright statement, disclaimer, licensing information), side comment, small print

By default `aside` has `role` of `complementary` and `footer` has `role` of `contentinfo`

> `aside` - Used for tangentially related content. Just because some content appears to the left or right of the main content isn’t enough reason to use the aside element. Ask yourself if the content within the aside can be removed without reducing the meaning of the main content. Pullquotes are an example of tangentially related content.

- https://stackoverflow.com/questions/9261748/is-it-semantically-valid-to-put-an-aside-tag-inside-a-header-tag TL;DR: aside can be in `header`

The `aside` element can now represent secondary content when used outside of an `article`

If you can remove the content of the `aside` element and the article content, to which it is relevant, becomes incomplete then you should not be using the `aside` element

The `aside` should be used for content tangentially related to the content surrounding it, such as related reading links and glossaries

`aside`: Pullquotes are a good example of tangentially related content; they’re nice to have, but you can remove them without affecting the comprehension of the main content.

side explanations, blogroll, shares, credits, copyrights, advertisements, biography of the author

Put `aside` in article if it's related to the article, else put in page's body if it's related to the whole page (like blogroll or twitter messages from the blog author)

	<aside><blockquote></blockquote></aside>

	<aside><p>Written by Alex Feyerke</p></aside>

Social links:

	<aside>
		<h1>Share it on</h1>
		<ul>
			<li><a href="http://twitter.com/intent/tweet?url=http://domain.example&amp;text=Title&amp;via=someone">Twitter</a></li>
			<li><a href="http://www.facebook.com/sharer.php?u=http://domain.example&amp;t=Title">Facebook</a></li>
			<li><a href="https://plus.google.com/share?url=http://domain.example">Google+</a></li>
		</ul>
	</aside>

http://html5doctor.com/your-questions-16/

Copyright:

	<p><small>Copyright<small></p>

	<footer>
		<address>
			For more details, contact
			<a href="mailto:hello@html5doctor.com">HTML5 Doctor</a>.
		</address>
		<small> © copyright HTML5 Doctor. </small>
	</footer>

- http://html5doctor.com/small-hr-element/
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/aside
- http://www.w3.org/TR/html5/sections.html#the-aside-element
- http://html5doctor.com/tag/aside/
- [Annotation - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Annotation)
- [Note (typography) - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Note_(typography))

### Large sec. content

Use `aside` or `footer`

When used inside the content of the `aside` element must be relevant to the `article` content

### Short runs of text

Use `small` for short runs of text.

	<dl>
		<dt>Single room
		<!-- price and disclaimer -->
		<dd>199 € <small>breakfast included, VAT not included</small>
		<dt>Double room
		<dd>239 € <small>breakfast included, VAT not included</small>
	</dl>

	<p>Example Corp today announced record profits for the
	second quarter <small>(Full Disclosure: Foo News is a subsidiary of
	Example Corp)</small>, leading to speculation about a third quarter
	merger with Demo Group.</p>

The `small` element is marked as being important small print.

	<p><strong><small>Continued use of this service will result in a kiss.</small></strong></p>

- http://html5doctor.com/small-hr-element/
- See also [Secondary content, side comments]()

### Footnotes

Also called annotation, comment and incorrectly "footer notes". Use `aside` or `small` (for inline)

Note: [`title` attribute is not accessible](#`title` attribute is not accessible)

> For annotations, the `a` element should be used, pointing to an element later in the document. The convention is that the contents of the link be a number in square brackets.

> In this example, a footnote in the dialogue links to a paragraph below the dialogue. The paragraph then reciprocally links back to the dialogue, allowing the user to return to the location of the footnote.

	<p> Announcer: Number 16: The <i>hand</i>.
	<p> Interviewer: Good evening. I have with me in the studio tonight
	Mr Norman St John Polevaulter, who for the past few years has been
	contradicting people. Mr Polevaulter, why <em>do</em> you
	contradict people?
	<p> Norman: I don't. <sup><a href="#fn1" id="r1">[1]</a></sup>
	<p> Interviewer: You told me you did!
	...
	<section>
	 <p id="fn1"><a href="#r1">[1]</a> This is, naturally, a lie,
	 but paradoxically if it were true he could not say so without
	 contradicting the interviewer and thus making it false.</p>
	</section>

> For side notes, longer annotations that apply to entire sections of the text rather than just specific words or sentences, the `aside` element should be used.

> In this example, a sidebar is given after a dialogue, giving it some context.

	<p> <span class="speaker">Customer</span>: I will not buy this record, it is scratched.
	<p> <span class="speaker">Shopkeeper</span>: I'm sorry?
	<p> <span class="speaker">Customer</span>: I will not buy this record, it is scratched.
	<p> <span class="speaker">Shopkeeper</span>: No no no, this's'a tobacconist's.
	<aside>
	 <p>In 1970, the British Empire lay in ruins, and foreign
	 nationalists frequented the streets — many of them Hungarians
	 (not the streets — the foreign nationals). Sadly, Alexander
	 Yalt has been publishing incompetently-written phrase books.
	</aside>

> For figures or tables, footnotes can be included in the relevant `figcaption` or `caption` element, or in surrounding prose.
.. or [`tfoot` element](#`tfoot` element)

> In this example, a table has cells with footnotes that are given in prose. A `figure` element is used to give a single legend to the combination of the table and its footnotes.

	<figure>
	 <figcaption>Table 1. Alternative activities for knights.</figcaption>
	 <table>
	  <tr>
	   <th> Activity
	   <th> Location
	   <th> Cost
	  <tr>
	   <td> Dance
	   <td> Wherever possible
	   <td> £0<sup><a href="#fn1">1</a></sup>
	  <tr>
	   <td> Routines, chorus scenes<sup><a href="#fn2">2</a></sup>
	   <td> Undisclosed
	   <td> Undisclosed
	  <tr>
	   <td> Dining<sup><a href="#fn3">3</a></sup>
	   <td> Camelot
	   <td> Cost of ham, jam, and spam<sup><a href="#fn4">4</a></sup>
	 </table>
	 <p id="fn1">1. Assumed.</p>
	 <p id="fn2">2. Footwork impeccable.</p>
	 <p id="fn3">3. Quality described as "well".</p>
	 <p id="fn4">4. A lot.</p>
	</figure>

- [4 The elements of HTML | HTML 5.1](http://www.w3.org/TR/html51/semantics.html#footnotes)
- [Accessible Footnotes with CSS](http://www.sitepoint.com/accessible-footnotes-css/)

## Address

> The `address` element represents contact information for a person, people or organization. It should include physical and/or digital location/contact information and a means of identifying a person(s) or organization the information pertains to.

> The address element represents the contact information for its nearest article or body element ancestor

> In this example the footer contains contact information and a copyright notice.

	<footer>
	 <address>
	  For more details, contact
	  <a href="mailto:js@example.com">John Smith</a>.
	 </address>
	 <p><small>© copyright 2038 Example Corp.</small></p>
	</footer>

- [HTML 5.2: 4.4. Grouping content](https://w3c.github.io/html/grouping-content.html#the-address-element)
- http://html5doctor.com/the-address-element/
- [Allow usage of `address` element in all contexts](https://github.com/w3c/html/issues/606#issuecomment-262320587)

## Contact information

TODO

- http://rachaelmoore.name/posts/design/html/html5-microdata-contact-info/
- http://rachaelmoore.name/posts/design/html/html5-vcards-markup-people-in-microdata/
- https://stackoverflow.com/questions/2359440/what-is-the-most-semantic-way-to-display-a-street-address-in-html
- https://stackoverflow.com/questions/5691855/is-microformats-vcard-still-a-best-semantic-way-to-code-contact-information-i

## Footer

By default its `role` is `contentinfo`

> Sounds like its a description of the position, but its not. Footer elements contain information about it’s containing element: who wrote it, copyright, links to related content, etc. Whereas we usually have one footer for an entire document, HTML5 allows us to also have footer within sections.

> Typically contains metadata about its enclosing section, such as who wrote it, links to related documents, copyright data, etc.
> Contact information for the section given in a footer should be marked up using the address element

> Here is a page with two footers, one at the top and one at the bottom, with the same content:

	<body>
	 <footer><a href="../">Back to index...</a></footer>
	  <h1>Lorem ipsum</h1>
	  <h2>The ipsum of all lorems</h2>
	 <p>A dolor sit amet, consectetur adipisicing elit, sed do eiusmod
	 tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim
	 veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex
	 ea commodo consequat. Duis aute irure dolor in reprehenderit in
	 voluptate velit esse cillum dolore eu fugiat nulla
	 pariatur. Excepteur sint occaecat cupidatat non proident, sunt in
	 culpa qui officia deserunt mollit anim id est laborum.</p>
	 <footer><a href="../">Back to index...</a></footer>
	</body>

> Here is an example which shows the footer element being used both for a site-wide footer and for a section footer.

	<!DOCTYPE HTML>
	<HTML><HEAD>
	<TITLE>The Ramblings of a Scientist</TITLE>
	<BODY>
	<H1>The Ramblings of a Scientist</H1>
	<ARTICLE>
	 <H1>Episode 15</H1>
	 <VIDEO SRC="/fm/015.ogv" CONTROLS PRELOAD>
	  <P><A HREF="/fm/015.ogv">Download video</A>.</P>
	 </VIDEO>
	 <FOOTER> <!-- footer for article -->
	  <P>Published <TIME DATETIME="2009-10-21T18:26-07:00">on 2009/10/21 at 6:26pm</TIME></P>
	 </FOOTER>
	</ARTICLE>
	<ARTICLE>
	 <H1>My Favorite Trains</H1>
	 <P>I love my trains. My favorite train of all time is a Köf.</P>
	 <P>It is fun to see them pull some coal cars because they look so
	 dwarfed in comparison.</P>
	 <FOOTER> <!-- footer for article -->
	  <P>Published <TIME DATETIME="2009-09-15T14:54-07:00">on 2009/09/15 at 2:54pm</TIME></P>
	 </FOOTER>
	</ARTICLE>
	<FOOTER> <!-- site wide footer -->
	 <NAV>
	  <P><A HREF="/credits.html">Credits</A> —
		 <A HREF="/tos.html">Terms of Service</A> —
		 <A HREF="/index.html">Blog Index</A></P>
	 </NAV>
	 <P>Copyright © 2009 Gordon Freeman</P>
	</FOOTER>
	</BODY>
	</HTML>

> Some site designs have what is sometimes referred to as "fat footers" — footers that contain a lot of material, including images, links to other articles, links to pages for sending feedback, special offers... in some ways, a whole "front page" in the footer.
> 
> This fragment shows the bottom of a page on a site with a "fat footer":

	...
	 <footer>
	  <nav>
	   <section>
		<h2>Articles</h2>
		<p><img src="images/somersaults.jpeg" alt=""> Go to the gym with
		our somersaults class! Our teacher Jim takes you through the paces
		in this two-part article. <a href="articles/somersaults/1">Part
		1</a> · <a href="articles/somersaults/2">Part 2</a></p>
		<p><img src="images/kindplus.jpeg"> Tired of walking on the edge of
		a clif<!-- sic -->? Our guest writer Lara shows you how to bumble
		your way through the bars. <a href="articles/kindplus/1">Read
		more...</a></p>
		<p><img src="images/crisps.jpeg"> The chips are down, now all
		that's left is a potato. What can you do with it? <a
		href="articles/crisps/1">Read more...</a></p>
	   </section>
	   <ul>
		<li> <a href="/about">About us...</a>
		<li> <a href="/feedback">Send feedback!</a>
		<li> <a href="/sitemap">Sitemap</a>
	   </ul>
	  </nav>
	  <p><small>Copyright © 2015 The Snacker —
	  <a href="/tos">Terms of Service</a></small></p>
	 </footer>
	</body>

http://www.whatwg.org/specs/web-apps/current-work/multipage/sections.html#the-footer-element

## Tag clouds

> In general, authors are encouraged to either mark up such lists using `ul` elements with explicit inline counts that are then hidden and turned into a presentational effect using a style sheet, or to use SVG.

	<style>
	@media screen, print, handheld, tv {
		/* should be ignored by non-visual browsers */
		.tag-cloud > li > span { display: none; }
		.tag-cloud > li { display: inline; }
		.tag-cloud-1 { font-size: 0.7em; }
		.tag-cloud-2 { font-size: 0.9em; }
		.tag-cloud-3 { font-size: 1.1em; }
		.tag-cloud-4 { font-size: 1.3em; }
		.tag-cloud-5 { font-size: 1.5em; }
	}
	</style>
	<!-- ... -->
	<ul class="tag-cloud">
		<li class="tag-cloud-4"><a title="28 instances" href="/t/apple">apple</a> <span>(popular)</span>
		<li class="tag-cloud-2"><a title="6 instances"  href="/t/kiwi">kiwi</a> <span>(rare)</span>
		<li class="tag-cloud-5"><a title="41 instances" href="/t/pear">pear</a> <span>(very popular)</span>
	</ul>

> The actual frequency of each tag is given using the `title` attribute. A CSS style sheet is provided to convert the markup into a cloud of differently-sized words, but for user agents that do not support CSS or are not visual, the markup contains annotations like "(popular)" or "(rare)" to categorize the various tags by frequency, thus enabling all users to benefit from the information.

Note: [`title` attribute is not accessible](#`title` attribute is not accessible)

> The `ul` element is used (rather than `ol`) because the order is not particularly important: while the list is in fact ordered alphabetically, it would convey the same information if ordered by, say, the length of the tag.

> The `tag` `rel`-keyword is _not_ used on these `a` elements because they do not represent tags that apply to the page itself; they are just part of an index listing the tags themselves.

## Conversations

Conversation transcript or chat

See also [forum post](#Forum post)

**Note: for chat wrap conversation with `role="log" aria-live="polite" aria-relevant="additions"`.** See [ARIA Live Regions - Accessibility | MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions) and [Using the aria-relevant attribute - Accessibility | MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-relevant_attribute)

> Instead, authors are encouraged to mark up conversations using `p` elements and punctuation. Authors who need to mark the speaker for styling purposes are encouraged to use `span` or `b`. Paragraphs with their text wrapped in the `i` element can be used for marking up stage directions.

> This example demonstrates this using an extract from Abbot and Costello's famous sketch, _Who's on first_:

	<p>Costello: Look, you gotta first baseman?</p>
	<p>Abbott: Certainly.</p>
	<p>Costello: Who's playing first?</p>
	<p>Abbott: That's right.</p>
	<p>Costello becomes exasperated.</p>
	<p>Costello: When you pay off the first baseman every month, who gets the money?</p>
	<p>Abbott: Every dollar of it.</p>

> The following extract shows how an IM conversation log could be marked up, using the `data` element to provide Unix timestamps for each line. Note that the timestamps are provided in a format that the `time` element does not support, so the `data` element is used instead (namely, Unix `time_t` timestamps). Had the author wished to mark up the data using one of the date and time formats supported by the `time` element, that element could have been used instead of `data`. This could be advantageous as it would allow data analysis tools to detect the timestamps unambiguously, without coordination with the page author.

	<!-- datetime attribute can be used on <time> -->
	<p><time>14:22</time> <b>egof</b> I'm not that nerdy, I've only seen 30% of the star trek episodes</p>
	<p><time>14:23</time> <b>kaj</b> if you know what percentage of the star trek episodes you have seen, you are inarguably nerdy</p>
	<p><time>14:23</time> <b>egof</b> it's unarguably</p>
	<p><time>14:23</time> <i>* kaj blinks</i></p>
	<p><time>14:24</time> <b>kaj</b> you are not helping your case</p>

> HTML does not have a good way to mark up graphs, so descriptions of interactive conversations from games are more difficult to mark up. This example shows one possible convention using `dl` elements to list the possible responses at each point in the conversation. Another option to consider is describing the conversation in the form of a DOT file, and outputting the result as an SVG image to place in the document. http://www.graphviz.org/content/dot-language

	<p> Next, you meet a fisherman. You can say one of several greetings:
	<dl>
	 <dt> "Hello there!"
	 <dd>
	  <p> He responds with "Hello, how may I help you?"; you can respond with:
	  <dl>
	   <dt> "I would like to buy a fish."
	   <dd> <p> He sells you a fish and the conversation finishes.
	   <dt> "Can I borrow your boat?"
	   <dd>
		<p> He is surprised and asks "What are you offering in return?".
		<dl>
		 <dt> "Five gold." (if you have enough)
		 <dt> "Ten gold." (if you have enough)
		 <dt> "Fifteen gold." (if you have enough)
		 <dd> <p> He lends you his boat. The conversation ends.
		 <dt> "A fish." (if you have one)
		 <dt> "A newspaper." (if you have one)
		 <dt> "A pebble." (if you have one)
		 <dd> <p> "No thanks", he replies. Your conversation options		
		 at this point are the same as they were after asking to borrow
		 his boat, minus any options you've suggested before.
		</dl>
	   </dd>
	  </dl>
	 </dd>
	 <dt> "Vote for me in the next election!"
	 <dd> <p> He turns away. The conversation finishes.
	 <dt> "Sir, are you aware that your fish are running away?"
	 <dd>
	  <p> He looks at you skeptically and says "Fish cannot run, sir".
	  <dl>
	   <dt> "You got me!"
	   <dd> <p> The fisherman sighs and the conversation ends.
	   <dt> "Only kidding."
	   <dd> <p> "Good one!" he retorts. Your conversation options at this
	   point are the same as those following "Hello there!" above.
	   <dt> "Oh, then what are they doing?"
	   <dd> <p> He looks at his fish, giving you an opportunity to steal
	   his boat, which you do. The conversation ends.
	  </dl>
	 </dd>
	</ul>

> In some games, conversations are simpler: each character merely has a fixed set of lines that they say. In this example, a game FAQ/walkthrough lists some of the known possible responses for each character:

	<section>
	 <h2>Dialogue</h2>
	 <p><small>Some characters repeat their lines in order each time you interact
	 with them, others randomly pick from amongst their lines. Those who respond in
	 order have numbered entries in the lists below.</small>
	 <h3>The Shopkeeper</h3>
	 <ul>
	  <li>How may I help you?
	  <li>Fresh apples!
	  <li>A loaf of bread for madam?
	 </ul>
	 <h3>The pilot</h3>
	 <p>Before the accident:
	 <ul>
	  </li>I'm about to fly out, sorry!
	  </li>Sorry, I'm just waiting for flight clearance and then I'll be off!
	 </ul>
	 <p>After the accident:
	 <ol>
	  <li>I'm about to fly out, sorry!
	  <li>Ok, I'm not leaving right now, my plane is being cleaned.
	  <li>Ok, it's not being cleaned, it needs a minor repair first.
	  <li>Ok, ok, stop bothering me! Truth is, I had a crash.
	 </ol>
	 <h3>Clan Leader</h3>
	 <p>During the first clan meeting:
	 <ul>
	  <li>Hey, have you seen my daughter? I bet she's up to something nefarious again...
	  <li>Nice weather we're having today, eh?
	  <li>The name is Bailey, Jeff Bailey. How can I help you today?
	  <li>A glass of water? Fresh from the well!
	 </ul>
	 <p>After the earthquake:
	 <ol>
	  <li>Everyone is safe in the shelter, we just have to put out the fire!
	  <li>I'll go and tell the fire brigade, you keep hosing it down!
	 </ol>
	</section>

## Details and summary

	<details>
		<summary>W Group Site Navigation</summary>
		<ul>
			<li><a href="#">Aeronautics</a></li>
			<li><a href="#">Pharma</a></li>
			<li><a href="#">Railways</a></li>
			<li><a href="#">Shipping</a></li>
		</ul>
	</details>

- [How do you mark up an accordion? — Sara Soueidan – Freelance-Front-End UI/UX Developer](https://www.sarasoueidan.com/blog/accordion-markup/)

## Forum post

Note: you can use `<time>` tag:

	<article>
	 <h1><a href="http://bacon.example.com/?blog=109431">Bacon on a crowbar</a></h1>
	 <article>
	  <header><strong>t3yw</strong> 12 points 1 hour ago</header>
	  <p>I bet a narwhal would love that.</p>
	  <footer><a href="?pid=29578">permalink</a></footer>
	  <article>
	   <header><strong>greg</strong> 8 points 1 hour ago</header>
	   <blockquote><p>I bet a narwhal would love that.</p></blockquote>
	   <p>Dude narwhals don't eat bacon.</p>
	   <footer><a href="?pid=29579">permalink</a></footer>
	   <article>
		<header><strong>t3yw</strong> 15 points 1 hour ago</header>
		<blockquote>
		 <blockquote><p>I bet a narwhal would love that.</p></blockquote>
		 <p>Dude narwhals don't eat bacon.</p>
		</blockquote>
		<p>Next thing you'll be saying they don't get capes and wizard
		hats either!</p>
		<footer><a href="?pid=29580">permalink</a></footer>
		<article>
		 <article>
		  <header><strong>boing</strong> -5 points 1 hour ago</header>
		  <p>narwhals are worse than ceiling cat</p>
		  <footer><a href="?pid=29581">permalink</a></footer>
		 </article>
		</article>
	   </article>
	  </article>
	  <article>
	   <header><strong>fred</strong> 1 points 23 minutes ago</header>
	   <blockquote><p>I bet a narwhal would love that.</p></blockquote>
	   <p>I bet they'd love to peel a banana too.</p>
	   <footer><a href="?pid=29582">permalink</a></footer>
	  </article>
	 </article>
	</article>

- http://www.whatwg.org/specs/web-apps/current-work/multipage/grouping-content.html#the-blockquote-element-2
- [HTML Standard](https://html.spec.whatwg.org/multipage/semantics.html#the-blockquote-element)

## Pictures media

	<picture>
		<source srcset="image.png" media="(max-height: 1000px)">
		<source srcset="image_small.png" media="(max-height: 700px)">
		<source srcset="image_big.png" media="(min-height: 1000px)">
		<img src="image_big.png" alt="">
	</picture>

	<picture>
		<source srcset="image.png" type="image/x-apng">
		<source srcset="image.gif" type="image/gif">
		<img src="image.gif" alt="">
	</picture>

	<object role="img" data="image.svg" type="image/svg+xml" title="Description of image"></object>

	<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 500 450" preserveAspectRatio="xMidYMid meet">
		<title>Description of image</title>
		
		<style>
			svg {
				background-size: 100% 100%;
				background-repeat: no-repeat;
			}
			
			@media screen and (max-width: 400px) {
				svg {
					background-image: url("small.png");
				}
			}
			
			@media screen and (min-width: 401px) and (max-width: 700px) {
				svg {
					background-image: url("medium.png");
				}
			}
			
			@media screen and (min-width: 701px) and (max-width: 1000px) {
				svg {
					background-image: url("big.png");
				}
			}
			
			@media screen and (min-width: 1001px) {
				svg {
					background-image: url("huge.png");
				}
			}
		</style>
	</svg>

See [Responsive image](#Responsive image)

Some techniques used below are based on SVG with CSS media queries, but exist before `<picture>` element exist. Keep here for historical reason and for inspiration:

- [How To Solve Adaptive Images In Responsive Web Design](https://www.smashingmagazine.com/2013/06/clown-car-technique-solving-for-adaptive-images-in-responsive-web-design/) (see also Accessibility section)
- [estelle/clowncar: Clown Car Responsive Image Technique](https://github.com/estelle/clowncar)
- [Better SVG Fallback and Art Direction With The <picture> Element](http://sarasoueidan.com/blog/svg-picture/)
- [Responsive Images: Clown Car Technique | Standardista](http://www.standardista.com/responsive-images-clown-car-technique/) https://github.com/estelle/clowncar
- [Responsive Image Container - blog](http://blog.yoav.ws/2013/09/Responsive-Image-Container)
- [the new code – Art-Directed Adaptive Images With SVG and JavaScript](http://thenewcode.com/722/Art-Directed-Adaptive-Images-With-SVG-and-JavaScript)
- [\<picture\> - HTML | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture)
- [Picturefill](http://scottjehl.github.io/picturefill/)

## Time

http://www.w3.org/html/wg/drafts/html/master/semantics.html#dom-time-datetime

## Event log

And for timed text. For conversation see [conversations](#Conversations)

Note: if it's live use `aria-live="polite" aria-relevant="additions"`. If live with element with removed elements (current connected players) use `aria-live="polite" aria-relevant="additions removals"` instead

With DL,DT+DD:

	<dl role="log">
		<dt><time datetime="2001-05-15 19:00">3 hours ago</time></dt>
		<dd>Event log 1 content</dd>
		<dt><time datetime="2001-05-15 20:00">2 hours ago</time></dt>
		<dd>Event log 2 content</dd>
		<dt><time datetime="2001-05-15 21:00">1 hours ago</time></dt>
		<dd>Event log 3 content</dd>
		<dt><time datetime="2001-05-15 22:00">Just happend</time></dt>
		<dd>Event log 4 content</dd>
	</dl>

Or with P:

	<div role="log">
		<p><time datetime="2001-05-15 19:00">3 hours ago</time>: Event log 1 content</p>
		<p><time datetime="2001-05-15 20:00">2 hours ago</time>: Event log 2 content</p>
		<p><time datetime="2001-05-15 21:00">1 hours ago</time>: Event log 3 content</p>
		<p><time datetime="2001-05-15 22:00">Just happend</time>: Event log 4 content</p>
	</div>

If log data has more than few fields (id, time, location, context, tags, etc.) it's preferable to use an `<article>` instead or a table

## Simple timeline

Use progressive enhancement for:

- Basic: CSS styles
- Datavis : SVG timeline with unobtrusive JavaScript
 
	<dl class="timeline">
		<dt>1969</dt><dd>UNICS</dd>
		<dt>1971</dt><dd>UNIX Time-Sharing System</dd>
		<dt>1978</dt><dd>BSD</dd>
		<dt>1980</dt><dd>XENIX OS</dd>
		<dt>1981</dt><dd>UNIX System III</dd>
		<dt>1982</dt><dd>SunOS</dd>
		<dt>1983</dt><dd>UNIX System V</dd>
		<dt>1986</dt>
			<dd>GNU (Trix)</dd>
			<dd>HP-UX</dd>
		<dt>1987</dt><dd>Minix</dd>
		<dt>1989</dt>
			<dd>NeXTSTEP</dd>
			<dd>SCO UNIX</dd>
		<dt>1990</dt><dd>Solaris</dd>
		<dt>1991</dt><dd>Linux</dd>
		<dt>1993</dt><dd>FreeBSD</dd>
		<dt>1995</dt><dd>OpenBSD</dd>
		<dt>1999</dt><dd>Mac OS X</dd>
		<!-- use aria-current="true" for the current item -->
	</dl>

- [Progressive Enhancement and Data Visualizations | CSS-Tricks](http://css-tricks.com/progressive-enhancement-data-visualizations/)

## Placeholder hyperlink

Use where you want to use an anchor element, but not have it navigate anywhere. For marking up the current page in a navigation menu or breadcrumb trail.

> links to the current page might become a placeholder

- [HTML 5.1: 4.5. Text-level semantics](https://www.w3.org/TR/html/textlevel-semantics.html#the-a-element)
- [What Are HTML5 Placeholder Links For?](http://webdesign.about.com/od/html5tutorials/qt/html5-placeholder-links.htm)

## Progress tracker

or progress indicator or stepper or multi-step progress. Number of steps in order to complete a specified process, for wizard. ex: order steps `shipping > billing > confirm order`

Similar to breadcrumb (but not the same).

	<nav>
		<ol>
			<li><a href="order/1">shipping</a></li>
			<li><a href="order/2">billing</a></li>
			<li><a aria-current="step">confirm order</a></li>
		</ol>
	</nav>

- [Progress Trackers in Web Design: Examples and Best Practices – Smashing Magazine](http://www.smashingmagazine.com/2010/01/progress-trackers-in-web-design-examples-and-best-design-practices/)
- [How do you indicate progress to users in a multi-step form? - User Experience Stack Exchange](http://ux.stackexchange.com/questions/3454/how-do-you-indicate-progress-to-users-in-a-multi-step-form)

## Comic markup

	<article class="comic" lang="en-us">
	  <header>
	    <h1>Frantic Stein</h1>
	    <address>by <a href="/george-mercer" rel="author">George Mercer</a></address>
	    <time datetime="2010-01-15">January 15th, 2010</time>
	  </header>
	  <svg role="list">
	    <g class="panel" role="listitem">
	        <text class="caption">F.B.I. Headquarters...</text>

	      <image xlink:href="panel-1.png">
	        <title>Frantic Stein's boss addresses him within his office.</title>
	        <desc>The boss sits behind his desk, with his policeman's cap on the desktop. He's striking a very odd pose.</desc>
	      </image>

	      <g class="speech-balloon">
	        <title>Stein's boss growls:</title>
	        <text>We've received a tip to the effect that there will be an attempt to harm the steamer <tspan class="u">Atlantis</tspan> on its good-will voyage to Europe! I want you to foil any such attempt!</text>
	      </g>
	    </g>

	    <g class="panel" role="listitem">
	      <image xlink:href="panel-2.png">
	        <title>Frantic realizes the gravity of the situation.</title>
	        <desc>We close in on Frantic's face. He looks very serious.</desc>
	      </image>

	      <g class="speech-balloon">
	        <title>Stein says:</title>
	        <text>So I board the steamer to Europe! Sounds interesting!</text>
	      </g>

	      <text class="caption">Next day Frantic Stein is aboard The Atlantis as it sets out to sea--and an indeterminable fate!</text>
	    </g>

	    <g class="panel" role="listitem">
	      <image xlink:href="panel-3.png">
	        <title>The Atlantis, a large steamer ship, cruises the open sea.</title>
	        <desc>The weather is clear, with the sea wavy but calm. The Atlantis cuts swiftly through the waves. It has 3 smokestacks and 2 radio masts.</desc>
	      </image>

	      <g class="speech-balloon">
	        <title>Stein's voice rings out from the ship:</title>
	        <text>Saw only one suspicious character... but he turned out to be the captain of the ship!</text>
	      </g>
	    </g>

	    <g class="panel" role="listitem">
	      <image xlink:href="panel-4.png">
	        <title>From their backs, we see Frantic and an unknown woman look out over the ocean.</title>
	        <desc>They are gazing over the ship's railing. Frantic is smoking, wearing a fedora and trenchcoat, and is gripping the railing with one hand. The woman clasps her hands behind her back, and is wearing a dress, fitted jacket, and sun hat with a long, flowing ribbon.</desc>
	      </image>

	      <g class="speech-balloon">
	        <title>The woman says:</title>
	        <text>Surprise!</text>
	      </g>

	      <g class="speech-balloon">
	        <title>Frantic shouts:</title>
	        <text><tspan="strong">Darwyn!</tspan></text>
	      </g>

	      <text class="caption">Continued...</text>
	    </g>
	  </svg>
	  
	  <footer>
	    <small><a href="http://copyright.gov/title17/" rel="license">© 2010</a></small>
	  </footer>
	</article>

You can use `<figure>` with `<figcaption>`

- [How do you mark up a comic? by Taylor Hunt on CodePen](https://codepen.io/tigt/blog/how-do-you-mark-up-a-comic)

## Data

Human-readable (and locale aware) is not machine-readable, or "How to store data for JS?".

To store IDs, UPC codes, ISBN or other reference numbers, date, time, etc.

Use `<data>` or `<time>` (if it's time related)

	<data value="1">One</data>
	<data value="UPC:022014640201">North Coast Organic Apple Cider</data>

`data-*` attribute can also be used, but it's more script oriented

	<a href="tel:+33612345678">+33 6 12 34 56 78</a>

CSS can also be use to add spaces, slashes, etc. but require to add a locale aware parser for the markup ([North American group phone numbers by 3+4](https://en.wikipedia.org/wiki/National_conventions_for_writing_telephone_numbers#United_States.2C_Canada.2C_and_other_NANP_countries), where [French group by 5*2](https://en.wikipedia.org/wiki/National_conventions_for_writing_telephone_numbers#France))

- [4.5 Text-level semantics — HTML5](https://www.w3.org/TR/html5/text-level-semantics.html#the-data-element)
- [Identifier - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Identifier)

### Date or time

	<time datetime="2011-11-12">November 12th</time>

	 <?php
	 echo '<time datetime="'.date('c').'">'.date('Y - m - d').'</time>';

## Products comparaison table

Can be also in an offer page: pricing plan, princing table or roadmap / planning

Use a table or articles. But not list and list-items

	<article>
		<h2>Starter</h2>
		<p>£9/mo</p>
		<ul>
			<li>Shared</li>
			<li>512mb ram</li>
			<li>20gb HDD</li>
			<li>200gb bandwidth</li>
			<li><s>Choice of OS</s></li>
			<li><s>Host multiple sites</s></li>
		</ul>
		<a href="#">Order starter</a>
	</article>
	<article>
		<h2>Developer</h2>
		<p>£18/mo</p>
		<ul>
			<li>VPS</li>
			<li>4gb ram</li>
			<li>40gb SSD</li>
			<li>1tb bandwidth</li>
			<li>Choice of OS</li>
			<li>Host multiple sites</li>
		</ul>
		<a href="#">Order developer</article>
	</article>
	<article>
		<h2>Business</h2>
		<p>£36/mo</p>
		<ul>
			<li>Dedicated</li>
			<li>12gb ram</li>
			<li>120gb SSD</li>
			<li>1tb bandwidth</li>
			<li>Choice of OS</li>
			<li>Host multiple sites</li>
		</ul>
		<a href="#">Order business</a>
	</article>

- [Products Comparison Table | CodyHouse](https://codyhouse.co/demo/products-comparison-table/index.html)
- Example for CSS, but not for semantic: [Pricing table](https://codepen.io/stevemckinney/pen/rLJNYV)

## `script`

- [Everything I Know About The Script Tag - Eager Blog](https://eager.io/blog/everything-I-know-about-the-script-tag/)

## Popup menu

	<button aria-haspopup="true">Account</button>
	<div></div>

## Gender / plurial combined form

- [Gender / plurial combined form](Text#Gender / plurial combined form)

## Calendar

See [Date picker](JavaScript#Date picker)

For input use `<input type="date">`

- [Making input type=date complicated – Samsung Internet Developers – Medium](https://medium.com/samsung-internet-dev/making-input-type-date-complicated-a544fd27c45a#.rmrxvno0y)
 
	<table>
		<caption>July 2016</caption>
		<tr>
			<th>Mon</th>
			<th>Tue</th>
			<th>Wed</th>
			<th>Thu</th>
			<th>Fri</th>
			<th>Sat</th>
			<th>Sun</th>
		</tr>
		<tr>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td>1</td>
			<td>2</td>
			<td>3</td>
		</tr>
		<tr>
			<td>4</td>
			<td>5</td>
			<td>6</td>
			<td>7</td>
			<td>8</td>
			<td>9</td>
			<td>10</td>
		</tr>
		<tr>
			<td>11</td>
			<td>12</td>
			<td>13</td>
			<td>14</td>
			<td>15</td>
			<td aria-current="date"><!-- today, not the date selected -->16</td>
			<td>17</td>
		</tr>
		<tr>
			<td>18</td>
			<td>19</td>
			<td>20</td>
			<td>21</td>
			<td>21</td>
			<td>22</td>
			<td>23</td>
		</tr>
		<tr>
			<td>24</td>
			<td>25</td>
			<td>26</td>
			<td>27</td>
			<td>28</td>
			<td>29</td>
			<td>30</td>
		</tr>
		<tr>
			<td>31</td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
	</table>

Note: `<time datetime="2016-07-12">12</time>` can be used to add semantic for dates

## Time schedule

	<ul>
		<li>9am to 10am: Welcome</li>
		<li aria-current="time">10am to 11am: Keynote</li><!-- now -->
		<li>11am to 11.30pm: Break</li>
		<li>11.30am to 1pm: Workshop</li>
		<li>1pm to 2pm: Lunch</li>
		<li>2pm to 3pm: Lecture</li>
		<li>3pm to 3.30pm: Break</li>
		<li>3.30pm to 5pm: Workshop</li>
	</ul>


## Navigation

	<link rel="home" title="Home" href="index.html">
	<link rel="next" title="Next" href="services.html">
	<link rel="prev" title="Previous" href="products.html">
	<link rel="help" title="Get Help" href="about.html">

- [Accessibility Matters - Pagination](http://www.a11ymatters.com/pattern/pagination/)
 
	<nav>
		<ul>
			<li><a href="/" class="current" aria-current="page">Home</a></li>
			<li><a href="/">About</a></li>
			<li><a href="/">Contact</a></li>
		</ul>
	</nav>

Skip to content:

	<!-- don't put in <nav> -->
	<ul>
		<li><a href="#content">Skip to content</a></li>
		<li><a href="#search">Skip to search</a></li>
		<li><a href="#languages">Skip to languages</a></li>
	</ul>

Use [Hide graphicaly an element](CSS#Hide graphicaly an element)

	<nav id="navigation">
		<ul>
			<li><a href="/">Home</a></li>
			<li><a href="/about">About</a></li>
			<li><a href="/shop">Shop</a></li>
			<li><a href="/content">Content</a></li>
		</ul>
	</nav>

Enhanced to (with JS):

	<nav id="navigation">
		<button aria-expanded="false">Menu</button>
		<ul hidden>
			<li><a href="/">Home</a></li>
			<li><a href="/about">About</a></li>
			<li><a href="/shop">Shop</a></li>
			<li><a href="/contact">Contact</a></li>
		</ul>
	</nav>
	<!--
	var navButton = document.querySelector('#navigation button');
	navButton.addEventListener('click', function() {
	  let expanded = this.getAttribute('aria-expanded') === 'true' || false;
	  this.setAttribute('aria-expanded', !expanded);
	  let menu = this.nextElementSibling;
	  menu.hidden = !menu.hidden;
	});
	-->

- [Menus & Menu Buttons](https://inclusive-components.design/menus-menu-buttons/)
- [Accessible Dropdown Menus Revisited | Terrill Thompson](http://terrillthompson.com/blog/474)
- Improve rollover dropdown accessibility [Dropdown Menus with More Forgiving Mouse Movement Paths | CSS-Tricks](http://css-tricks.com/dropdown-menus-with-more-forgiving-mouse-movement-paths/)

## Menu

Application menu (not links)

- [Menus & Menu Buttons](https://inclusive-components.design/menus-menu-buttons/)

### `menu` element

List of commands and is an interactive element and more likely to be used exclusively in Web Applications

	<menu type="toolbar">
	  <li class="new">New</li>
	  <li class="open">Open</li>
	  <li class="save">Save</li>
	  <li class="quit">Quit</li>
	</menu>

`type` (attribute) as toolbar or popup

http://html5doctor.com/element-index/#menu
https://developer.mozilla.org/en-US/docs/Web/HTML/Element/menu

## Combo box

Used to enter a value (input). Don't use it for navigation.

Use `<select>`. If you want to use a custom widget use `aria-activedescendant` if collapsible.

- [Menus & Menu Buttons](https://inclusive-components.design/menus-menu-buttons/)
- [Combo box — Wikipedia](https://en.wikipedia.org/wiki/Combo_box)

## Underline

Use `<u>keyword</u>`

- [\<u\> Is Perfect for Syntax Highlighting by Taylor Hunt on CodePen](https://codepen.io/tigt/post/the-u-element-for-syntax-highlighting)

# Tips

- [HTML | CSS-Tricks](https://css-tricks.com/snippets/html/)

## Input pattern

- [html5pattern](http://www.html5pattern.com/) - Source of regularly used Input-Patterns

## Hide an element

With `tabindex="-1"` and with `aria-hidden="true"` and/or `role="presentation"` or simply `style="display:none"` (or `hidden` attribute, but not really supported)

See also [Hide an element to assistive technologies](CSS#Hide an element to assistive technologies)

- [Know your ARIA: 'Hidden' vs 'None'](http://www.scottohara.me/blog/2018/05/05/hidden-vs-none.html)
- http://asurkov.blogspot.fr/2012/02/aria-hidden-and-rolepresentation.html
- http://john.foliot.ca/aria-hidden
- http://www.paciellogroup.com/blog/2012/05/html5-accessibility-chops-hidden-and-aria-hidden/

## Input-Controlled Web Design

tabs, modal, carousel/slideshow, details, etc.

**Don't use it.** It require JS and to update aria attributes. So why use form fields?

States are saved by browsers ("remember form values"). To disable autofill, see [Disable autofill](#disable-autofill).
Inputs must use `position: fixed` to fix the possible autoscroll-when-focus (interest area).
If input is nested in form, `form=""` should be added.

> The elements used to create controls generally appear inside a FORM element, but may also appear outside of a FORM element declaration when they are used to build user interfaces
— [Forms in HTML documents](http://www.w3.org/TR/html401/interact/forms.html#h-17.2.1)

> Control elements such as INPUT, SELECT, BUTTON, TEXTAREA, and LABEL all respond to certain intrinsic events. When these elements do not appear within a form, they may be used to augment the graphical user interface of the document.
— [Scripts in HTML documents](http://www.w3.org/TR/html401/interact/scripts.html#h-18.2.3)

HTML5 use the concept of [form owner](https://html.spec.whatwg.org/multipage/forms.html#form-owner)

Input elements outside form should be added by script to control UI, like filter table with `input[type=text]` or a `select`, however it's better to use a form to allow user with UA without script support (or enabled) to use the filter/action (but handled by the server) or to handle the "submit" and global "input" event or allow form reset

For progressive enhancement (what the button/label/input do?): it's better to use link to local anchor (target the element with visibility toggled) for opening elements and use button[type=button] for closing elements. And save state if required with `history.replaceState(appStateJSONasString, "", document.URL)` or with SessionStorage or LocalStorage, depends if the state is share between windows/tabs and persistent. Should respect headers like `Cache-Control`?
What append when focusing label (accessibility)?

As an example, [interactive elements](https://html.spec.whatwg.org/multipage/forms.html#interactive-elements) like `details` and `dialog` states are not saved like input in form: [HTML Standard - 4.10.19.8.2 Processing model](https://html.spec.whatwg.org/multipage/forms.html#processing-model-4)

- [Radio-Controlled Web Design · An A List Apart Article](http://alistapart.com/article/radio-controlled-web-design)
- [CSS + HTML only Accordion Element](https://codepen.io/abergin/pen/ihlDf)
- https://github.com/NamPNQ/You-Dont-Need-Javascript

## HTTP hearder tag equivalent

	Link: </images/big.jpeg>; rel=prefetch

	<meta http-equiv="Link" content="</images/big.jpeg>; rel=prefetch">

	<link rel="prefetch" href="/images/big.jpeg">

## HTML entities

`&nbsp;` (non breaking space) not the same as space `&#32;`
You can use `&quot;` in attribute value `style="background: url(&quot;image.png&quot;)"` or use simple quote `style="background: url('image.png')"`

- [Character Entity Reference Chart](https://dev.w3.org/html5/html-author/charref)
- [HTML Symbols, Entities, Characters and Codes — HTML Arrows](https://www.toptal.com/designers/htmlarrows/)
- [Entity Lookup](http://entity-lookup.leftlogic.com/)

## Language attribute

Special subtags:

- `mis`: Uncoded languages
- `mul`: Multiple languages
- `und`: Undetermined
- `zxx`: No linguistic content, like lorem-ipsum text, identifiers (credit card number, ISBN, barcode, activation/product key, etc.)

- [Notes on `lang` by Taylor Hunt on CodePen](https://codepen.io/tigt/post/notes-on-lang)
- [UTS #35: Unicode Locale Data Markup Language](http://www.unicode.org/reports/tr35/#Unicode_Language_and_Locale_Identifiers)
- [IANA Language Subtag Registry](http://www.iana.org/assignments/language-subtag-registry/language-subtag-registry)
- [Tagging text with no language](https://www.w3.org/International/questions/qa-no-language)
- [BCP 47 - Tags for Identifying Languages](https://tools.ietf.org/html/bcp47)
- [RFC 3066 - Tags for the Identification of Languages](https://tools.ietf.org/html/rfc3066)
- [Why use the language attribute?](https://www.w3.org/International/questions/qa-lang-why.en)

## LTR and RTL

Can be done in inline text with unicode special char like "RIGHT-TO-LEFT EMBEDDING" (U+202B). Usefull for attribute where tag are not allowed: `<input name=t1 type=tel placeholder="&#x202B; رقم الهاتف 1 &#x202E;">`

- [How to use Unicode controls for bidi text](https://www.w3.org/International/questions/qa-bidi-unicode-controls)

## Disable style

There is no disable attribute for style. Use media attribute instead: `<style media="not all">` (or eventually use type: `<style type="text/plain">`)

## Use `<base>` is not recommended

`<base href="/">`

Base with only target attribute can still be used

You can inline SVG, but one of tricky thing is using `<base>` on HTML document will break local URLs everythings using [`FuncIRI` type](http://www.w3.org/TR/SVG/types.html#DataTypeFuncIRI):

- `clip-path`
- `color-profile`
- `src`
- `cursor`
- `fill`
- `filter`
- `marker`
- `marker-start`
- `marker-mid`
- `marker-end`
- `mask`
- `stroke`
- `xlink:href` (use, link)

Ex: `<use xlink:href="#path-1"></use>` or `<ellipse id="Oval-1" mask="url(#mask-2)" cx="182" cy="344.5" rx="13" ry="46.5"></ellipse>`

A workaround is to use domain less URL or absolute URL, but not work on IE

- see `xml:base`
- [Requiring \<base\> tags means I can't use SVG with clip-path, mask, etc... · Issue #8934 · angular/angular.js](https://github.com/angular/angular.js/issues/8934)
- [Fixes references to inline SVG elements when the \<base\> tag is in use.](https://gist.github.com/leonderijke/c5cf7c5b2e424c0061d2)
- [contextpath - Is it recommended to use the \<base\> html tag? - Stack Overflow](https://stackoverflow.com/questions/1889076/is-it-recommended-to-use-the-base-html-tag)
- [html - Using base tag on a page that contains SVG marker elements fails to render marker - Stack Overflow](https://stackoverflow.com/questions/18259032/using-base-tag-on-a-page-that-contains-svg-marker-elements-fails-to-render-marke/18265336#18265336)
- [\<base\> - HTML | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/base)

## Spellcheck

`<textarea>`, `<input>`, `contentEditable`

	<textarea spellcheck="false"></textarea>

But you shouldn't disable spell check juste because it's underlined misspelled words. But use correct attributes. Ex. `lang`:

	<!-- Klingon: -->
	<div contentEditable="true" lang="tlh">tlhIngan Hol</div>
	<!-- No linguistic content: -->
	<textarea lang="zxx">Lorem ipsum dolor sit amet, consectetur adipisicing elit.</textarea>
	<label for="isbn">ISBN:</label><input id="isbn" lang="zxx" type="text" value="978-3-16-148410-0">

See [Language attribute](#Language attribute) and [Field type](#Field type)

- [javascript - Turn off grammar correction in a contenteditable div in FireFox - Stack Overflow](https://stackoverflow.com/questions/5782835/turn-off-grammar-correction-in-a-contenteditable-div-in-firefox)
- [spellcheck - HTML | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/spellcheck)

## PDF reader

Inline reader with a fallback (download)

	<object type="application/pdf" data="yii.pdf#toolbar=1&amp;navpanes=0&amp;scrollbar=1&amp;page=1&amp;view=FitH">
		<a href="yii.pdf" target="_blank">Download yii.pdf</a>
	</object>

Inline reader:

	<iframe src="yii.pdf"></iframe>

Inline reader pure JS: [PDF.js](https://mozilla.github.io/pdf.js/) (same reader used by Firefox)

- [Parameters for Opening PDF Files - pdf_open_parameters_v9.pdf](http://wwwimages.adobe.com/www.adobe.com/content/dam/Adobe/en/devnet/acrobat/pdfs/pdf_open_parameters_v9.pdf)
