- [Advanced Web Scraping: Bypassing "403 Forbidden," captchas, and more | sangaline.com](http://sangaline.com/post/advanced-web-scraping-tutorial/)
- [Detecting Chrome Headless](http://antoinevastel.github.io/bot%20detection/2017/08/05/detect-chrome-headless.html)

# Tools

- [Options for HTML scraping? - Stack Overflow](https://stackoverflow.com/questions/2861/options-for-html-scraping)
- [parsing - How do you parse and process HTML/XML in PHP? - Stack Overflow](https://stackoverflow.com/questions/3577641/how-do-you-parse-and-process-html-xml-in-php)
- [Scrapy | A Fast and Powerful Scraping and Web Crawling Framework](https://scrapy.org/)
- https://gist.github.com/evandrix/3694955
- Python BeautifulSoup [Parser du HTML et XML avec python et la bibliothèque BeautifulSoup - Python Programmation Cours Tutoriel Informatique Apprendre](http://apprendre-python.com/page-beautifulsoup-html-parser-python-library-xml) and [How to scrape websites with Python and BeautifulSoup](https://medium.freecodecamp.com/how-to-scrape-websites-with-python-and-beautifulsoup-5946935d93fe)
- [tbodt/v8py: Write Python APIs, then call them from JavaScript using the V8 engine.](https://github.com/tbodt/v8py)

See also

- [Headless browser](Web#Headless browser)
- [Data scraping](Security#Data scraping)

## Simple way (declarative)

Use PHP

HTML Parser (as XML Document, Simple XML) + JS Parser generate an AST (as XML)

Then XML + custom XSL = data

JSON template with CSS selectors: http://www.jamapi.xyz/

	{
	  "title": "title",
	  "logo": ".nav-logo img",
	  "paragraphs": [{ "elem": ".home-post h1", "value": "text"}], 
	  "links": [{"elem": ".home-post > a:first-of-type", "location": "href"}]
	}

## Complex way (imperative)

Use PHP

Headless Web Browser (binded to PHP) + custom code "filter" (handle interactions, timers, js inspection, image/video/canvas access) generate data (XML, JSON, CVS, etc.)

- [Mink](https://github.com/Behat/Mink) use [Goutte](https://github.com/FriendsOfPHP/Goutte) or [Selenium](http://docs.seleniumhq.org/) or [WebDriver]
- http://phantomjs.org/ [Create WebPage Screenshots with Node.js and PhantomJS](https://davidwalsh.name/get-webpage-screenshot)
- https://code.google.com/p/php-webdriver-bindings/
- http://include-once.org/p/phpjs/
- http://www.w3.org/TR/2013/WD-webdriver-20130117/
- https://github.com/kohlschutter/boilerpipe

## Both

Template: declartive with impertive inclusions

# Websites

## Blogs: Blogger, Wordpress, etc.

- [Plateformes de blogs : comment transférer ses articles ? - Iv Oam Blog](http://iv-oam.blogspot.fr/2013/05/plateformes-de-blogs-et-transferts.html)
- http://ivoam.raidghost.com/index/conversions-en.html
- http://ivoam.raidghost.com/import/index.html by https://github.com/ivoam
- [Importing Content « WordPress Codex](https://codex.wordpress.org/Importing_Content)
- [Blogger 2 WordPress — WordPress Plugins](https://wordpress.org/plugins/blogger-2-wp/)
- [Blogger Importer — WordPress Plugins](https://wordpress.org/plugins/blogger-importer/)

## Itunes

- https://developer.apple.com/library/ios/documentation/LanguagesUtilities/Conceptual/iTunesConnect_Guide/8_AddingNewApps/AddingNewApps.html
- http://www.apple.com/itunes/affiliates/resources/documentation/itunes-store-web-service-search-api.html
- http://www.apple.com/itunes/affiliates/resources/documentation/enterprise-partner-feed-flat.html
- https://rss.itunes.apple.com/fr/

- http://itunes.apple.com/lookup?id=529882042&lang=fr
- http://itunes.apple.com/fr/lookup?id=529882042

- https://stackoverflow.com/questions/5610392/app-store-and-itunes-api-getting-icon
- https://discussions.apple.com/thread/3225104?tstart=0

- https://stackoverflow.com/questions/16164847/itunes-lookup-api-get-iphone-5-app-screenshots

### App Icon

- 1024 x 1024 pixels

### iPhone and iPod touch Screenshots

- 640x920 pixels for hi-res portrait (without status bar) minimum
- 640x960 pixels for hi-res portrait (full screen) maximum
- 960x600 pixels for hi-res landscape (without status bar) minimum
- 960x640 pixels for hi-res landscape (full screen) maximum

`screen568x568.jpeg` → `screen920x920.jpeg`

### iPhone 5 and iPod touch (5th gen) Screenshots

- 640x1096 pixels for portrait (without status bar) minimum
- 640x1136 pixels for portrait (full screen) maximum
- 1136x600 pixels for landscape (without status bar) minimum
- 1136x640 pixels for landscape (full screen) minimum

`screen568x568.jpeg` → `screen1136x1136.jpeg`

### iPhone 6

`screen1334x1334.jpeg`

### iPad Screenshots

- 1024x748 pixels for landscape (without status bar) minimum
- 1024x768 pixels for landscape (full screen) maximum
- 2048x1496 pixels for hi-res (without status bar) minimum
- 2048x1536 pixels for hi-res landscape (full screen) maximum
- 768x1004 pixels for portrait (without status bar) minimum
- 768x1024 pixels for portrait (full screen) maximum
- 1536x2008 pixels for hi-res portrait (without status bar) minimum
- 1536x2048 pixels for hi-res portrait (full screen) maximum

`screen480x480.jpeg` → `screen960x960.jpeg`, `screen1024x1024.jpeg`, `screen2048x2048.jpeg`

### Desktop Screenshot

- 1280x800 pixels
- 1440x900 pixels
- 2880x1800 pixels

`screen800x500.jpeg` → `screen1280x800.jpeg`
`mzl.anmvzyyt.225x225-75.jpg` → `mzl.anmvzyyt.png`

### View iTunes/App Store HTML

Enable WebKit’s Inspector (no more works):

	defaults write com.apple.iTunes WebKitDeveloperExtras -bool true
	defaults write com.apple.appstore WebKitDeveloperExtras -bool true

or

	defaults write -GlobalDomain WebKitDeveloperExtras -bool true

	defaults write NSGlobalDomain WebKitDeveloperExtras -bool true

Or request directly

	wget --header "User-Agent: iTunes/10.3.1 (Macintosh; Intel Mac OS X 10.6.8) AppleWebKit/533.21.1" --header "X-Apple-Store-Front: 143442,12" --header "X-Apple-Tz: -18000" --header "Accept-Language: en-us, en;q=0.50" https://itunes.apple.com/app/gasoil-now-prix-essence-comparateur/id681463839

Where `X-Apple-Store-Front` equals to one of following value

	[
		{
			"storefront":"143455-6,12",
			"name":"Canada"
		},
		{
			"storefront":"143441-1,12",
			"name":"United States"
		},
		{
			"storefront":"143565,12",
			"name":"Belarus"
		},
		{
			"storefront":"143446-2,12",
			"name":"Belgium"
		},
		{
			"storefront":"143526,12",
			"name":"Bulgaria"
		},
		{
			"storefront":"143494,12",
			"name":"Croatia"
		},
		{
			"storefront":"143557-2,12",
			"name":"Cyprus"
		},
		{
			"storefront":"143489,12",
			"name":"Czech Republic"
		},
		{
			"storefront":"143458-2,12",
			"name":"Denmark"
		},
		{
			"storefront":"143443,12",
			"name":"Deutschland"
		},
		{
			"storefront":"143454-8,12",
			"name":"España"
		},
		{
			"storefront":"143518,12",
			"name":"Estonia"
		},
		{
			"storefront":"143447-2,12",
			"name":"Finland"
		},
		{
			"storefront":"143442,12",
			"name":"France"
		},
		{
			"storefront":"143448,12",
			"name":"Greece"
		},
		{
			"storefront":"143482,12",
			"name":"Hungary"
		},
		{
			"storefront":"143558,12",
			"name":"Iceland"
		},
		{
			"storefront":"143449,12",
			"name":"Ireland"
		},
		{
			"storefront":"143450,12",
			"name":"Italia"
		},
		{
			"storefront":"143519,12",
			"name":"Latvia"
		},
		{
			"storefront":"143520,12",
			"name":"Lithuania"
		},
		{
			"storefront":"143451-2,12",
			"name":"Luxembourg"
		},
		{
			"storefront":"143530,12",
			"name":"Macedonia"
		},
		{
			"storefront":"143521,12",
			"name":"Malta"
		},
		{
			"storefront":"143523,12",
			"name":"Moldova"
		},
		{
			"storefront":"143452,12",
			"name":"Nederland"
		},
		{
			"storefront":"143457-2,12",
			"name":"Norway"
		},
		{
			"storefront":"143445,12",
			"name":"Österreich"
		},
		{
			"storefront":"143478,12",
			"name":"Poland"
		},
		{
			"storefront":"143453,12",
			"name":"Portugal"
		},
		{
			"storefront":"143487,12",
			"name":"Romania"
		},
		{
			"storefront":"143496,12",
			"name":"Slovakia"
		},
		{
			"storefront":"143499,12",
			"name":"Slovenia"
		},
		{
			"storefront":"143456,12",
			"name":"Sverige"
		},
		{
			"storefront":"143459-2,12",
			"name":"Switzerland"
		},
		{
			"storefront":"143480,12",
			"name":"Turkey"
		},
		{
			"storefront":"143444,12",
			"name":"United Kingdom"
		},
		{
			"storefront":"143469,12",
			"name":"Россия"
		},
		{
			"storefront":"143563,12",
			"name":"Algeria"
		},
		{
			"storefront":"143564,12",
			"name":"Angola"
		},
		{
			"storefront":"143524,12",
			"name":"Armenia"
		},
		{
			"storefront":"143568,12",
			"name":"Azerbaijan"
		},
		{
			"storefront":"143559,12",
			"name":"Bahrain"
		},
		{
			"storefront":"143525,12",
			"name":"Botswana"
		},
		{
			"storefront":"143516,12",
			"name":"Egypt"
		},
		{
			"storefront":"143573,12",
			"name":"Ghana"
		},
		{
			"storefront":"143467,12",
			"name":"India"
		},
		{
			"storefront":"143491,12",
			"name":"Israel"
		},
		{
			"storefront":"143528,12",
			"name":"Jordan"
		},
		{
			"storefront":"143529,12",
			"name":"Kenya"
		},
		{
			"storefront":"143493,12",
			"name":"Kuwait"
		},
		{
			"storefront":"143497,12",
			"name":"Lebanon"
		},
		{
			"storefront":"143531,12",
			"name":"Madagascar"
		},
		{
			"storefront":"143532,12",
			"name":"Mali"
		},
		{
			"storefront":"143533,12",
			"name":"Mauritius"
		},
		{
			"storefront":"143534,12",
			"name":"Niger"
		},
		{
			"storefront":"143561,12",
			"name":"Nigeria"
		},
		{
			"storefront":"143562,12",
			"name":"Oman"
		},
		{
			"storefront":"143498,12",
			"name":"Qatar"
		},
		{
			"storefront":"143479,12",
			"name":"Saudi Arabia"
		},
		{
			"storefront":"143535,12",
			"name":"Senegal"
		},
		{
			"storefront":"143472,12",
			"name":"South Africa"
		},
		{
			"storefront":"143572,12",
			"name":"Tanzania"
		},
		{
			"storefront":"143536,12",
			"name":"Tunisia"
		},
		{
			"storefront":"143481,12",
			"name":"UAE"
		},
		{
			"storefront":"143537,12",
			"name":"Uganda"
		},
		{
			"storefront":"143571,12",
			"name":"Yemen"
		},
		{
			"storefront":"143460,12",
			"name":"Australia"
		},
		{
			"storefront":"143560,12",
			"name":"Brunei Darussalam"
		},
		{
			"storefront":"143465-2,12",
			"name":"China"
		},
		{
			"storefront":"143463,12",
			"name":"Hong Kong"
		},
		{
			"storefront":"143476,12",
			"name":"Indonesia"
		},
		{
			"storefront":"143462-1,12",
			"name":"Japan"
		},
		{
			"storefront":"143517,12",
			"name":"Kazakhstan"
		},
		{
			"storefront":"143515,12",
			"name":"Macau"
		},
		{
			"storefront":"143473,12",
			"name":"Malaysia"
		},
		{
			"storefront":"143461,12",
			"name":"New Zealand"
		},
		{
			"storefront":"143477,12",
			"name":"Pakistan"
		},
		{
			"storefront":"143474,12",
			"name":"Philippines"
		},
		{
			"storefront":"143464,12",
			"name":"Singapore"
		},
		{
			"storefront":"143486,12",
			"name":"Sri Lanka"
		},
		{
			"storefront":"143470,12",
			"name":"Taiwan"
		},
		{
			"storefront":"143475,12",
			"name":"Thailand"
		},
		{
			"storefront":"143566,12",
			"name":"Uzbekistan"
		},
		{
			"storefront":"143471,12",
			"name":"Vietnam"
		},
		{
			"storefront":"143466,12",
			"name":"대한민국"
		},
		{
			"storefront":"143538,12",
			"name":"Anguilla"
		},
		{
			"storefront":"143540,12",
			"name":"Antigua and Barbuda"
		},
		{
			"storefront":"143505-2,12",
			"name":"Argentina"
		},
		{
			"storefront":"143539,12",
			"name":"Bahamas"
		},
		{
			"storefront":"143541,12",
			"name":"Barbados"
		},
		{
			"storefront":"143555-2,12",
			"name":"Belize"
		},
		{
			"storefront":"143542,12",
			"name":"Bermuda"
		},
		{
			"storefront":"143556-2,12",
			"name":"Bolivia"
		},
		{
			"storefront":"143503,12",
			"name":"Brasil"
		},
		{
			"storefront":"143543,12",
			"name":"British Virgin Islands"
		},
		{
			"storefront":"143544,12",
			"name":"Cayman Islands"
		},
		{
			"storefront":"143483-2,12",
			"name":"Chile"
		},
		{
			"storefront":"143501-2,12",
			"name":"Colombia"
		},
		{
			"storefront":"143495-2,12",
			"name":"Costa Rica"
		},
		{
			"storefront":"143545,12",
			"name":"Dominica"
		},
		{
			"storefront":"143508-2,12",
			"name":"Dominican Republic"
		},
		{
			"storefront":"143509-2,12",
			"name":"Ecuador"
		},
		{
			"storefront":"143506-2,12",
			"name":"El Salvador"
		},
		{
			"storefront":"143546,12",
			"name":"Grenada"
		},
		{
			"storefront":"143504-2,12",
			"name":"Guatemala"
		},
		{
			"storefront":"143553,12",
			"name":"Guyana"
		},
		{
			"storefront":"143510-2,12",
			"name":"Honduras"
		},
		{
			"storefront":"143511,12",
			"name":"Jamaica"
		},
		{
			"storefront":"143468,12",
			"name":"México"
		},
		{
			"storefront":"143547,12",
			"name":"Montserrat"
		},
		{
			"storefront":"143512-2,12",
			"name":"Nicaragua"
		},
		{
			"storefront":"143485-2,12",
			"name":"Panama"
		},
		{
			"storefront":"143513-2,12",
			"name":"Paraguay"
		},
		{
			"storefront":"143507-2,12",
			"name":"Peru"
		},
		{
			"storefront":"143548,12",
			"name":"St. Kitts and Nevis"
		},
		{
			"storefront":"143549,12",
			"name":"St. Lucia"
		},
		{
			"storefront":"143550,12",
			"name":"St. Vincent & The Grenadines"
		},
		{
			"storefront":"143554-2,12",
			"name":"Suriname"
		},
		{
			"storefront":"143551,12",
			"name":"Trinidad and Tobago"
		},
		{
			"storefront":"143552,12",
			"name":"Turks & Caicos"
		},
		{
			"storefront":"143514-2,12",
			"name":"Uruguay"
		},
		{
			"storefront":"143502-2,12",
			"name":"Venezuela"
		}
	]

Add to HTML document

	<base href="https://itunes.apple.com/">
	<script>
		// Add additionals headers
		(function(){
		XMLHttpRequest.prototype._send = XMLHttpRequest.prototype.send;
		XMLHttpRequest.prototype.send = function send(){
			//this.setRequestHeader("User-Agent", "iTunes/10.3.1 (Macintosh; Intel Mac OS X 10.6.8) AppleWebKit/533.21.1");
			this.setRequestHeader("X-Apple-Store-Front", "143442,12");
			this.setRequestHeader("X-Apple-Tz", "-18000");
			this.setRequestHeader("Accept-Language", "en-us, en;q=0.50");
			this._send.apply(this, arguments);
		};
		})();
	
	//window.navigator.userAgent.indexOf("MacAppStore")
	iTunes = {
		version: "11",
		getWindowById: function(n){
			//"main"
			//ITSProtocol.POPOVER_ID {close: function(){}}
			return iTunes.window;
		},
		window: {
			id: "main",
		height: 1000,
		WindowStyleApplicationDefinedPopover: "",
		WindowStyleTransientPopover: ""
		},
		showNavBarButton: function(/*ITSProtocol.NAV_BUTTON_ID*/){
			
		},
		setCreditBalance: function(c){
		
		},
		isHDCPAvailable: function(){
			return false
		},
		buy: function(p){
			/*
			p = {
			buyParams
			itemName
			preOrder
			freeDownload
			rent
			}
			*/
		},
		doAnonymousDownload: function(){
		
		},
		getMachineID: function(){
			return "none";
		},
		addProtocol: function(p){
		
		},
		doPodcastDownload: function(w/*,0*/){
		
		},
		platform: "Mac"/*"Windows"*/,
		putURLOnPasteboard: function(t/*,!0*/){
		
		},
		browseLocalLibrary: function(i/*{album:}*/,r){
		
		},
		putTracksOnClipboard: function(i/*{length:}*/){
		
		},
		currentPlayingTrack: {
			play: function(){}
		},
		currentTime: 0,
		playURL: function(u){
		
		},
		stop: function(){
		
		},
		getPreferences: function(){
			return {
				pingEnabled: false,
				parentalThresholdMovies: 10,
				parentalThresholdTV: 10,
				parentalThresholdMusic: 10,
				parentalThresholdApps: 10,
				podcastsEnabled: true,
				parentalThresholdBooks: 10,
				//[ITSParentalRatingUtil.Type.Music]: {ratingValue: 0 or 500},
				prefer1080pVideo: true
			};
		},
		getHistory: function(){
			return {
				removeCurrentPage: function(){
				
				},
				length: 0,
				back: function(){
				
				}
			}
		},
		getBag: function(){
			return {modifyAccount: ""}
		},
		startProgressSpinner: function(){
		
		},
		stopProgressSpinner: function(){
		
		},
		doDialogXML: function(i, s){
		
		},
		getUserDSID: function(){
			return "none"
		},
		getStoreItemStatus: function(e){
			return 0//number
		},
		findTracksByStoreID: function(e){
			return [/*{isRental, flavor, storeVersion:number}*/];
		},
		getCloudState: function(){
			return its.client.match.STATES.UNKNOWN;
		},
		setCloudState: function(e){
		
		},
		getCloudCompletedTracks: function(){
		
		},
		getCloudTotalTracks: function(){
		
		},
		getCloudMatchedTracks: function(){
		
		},
		getCloudTotalAvailableTracks: function(){
		
		},
		systemVersion: function(){
			return "10.9"
		},
		device: "",
		pingURL: function(g){
		
		},
		addEventListener: function(type, callback, b){
			//didreappear
		},
		removeEventListener: function(){
		
		},
		openNavBarPopover: function(p){
			/*
			p = {
				id: ITSProtocol.POPOVER_ID,
				url: "",
				width: 200,
				height: 200,
				style: iTunes.window.WindowStyleApplicationDefinedPopover or iTunes.window.WindowStyleTransientPopover,
				html: ""
			}
			*/
		},
		doAnonymousDownload: function(p){
			/*
			p = {
				itemName
			}
			*/
		},
		getMachineID: function(){
			return "none";
		},
		canPlay1080pVideo: true,
		showPreferences: function(p){
			// "store"
		},
		cookie: "",
		// Could be a function or something else (boolean?)
		screenReaderRunning: function(){
			return true
		},
		loggingEnabled: true,
		log: function(e){
			console.log(e)
		}
	}</script>

And open it with `/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --allow-file-access-from-files --disable-web-security`

https://gist.github.com/sgmurphy/1878352

## Flickr

- [Services Flickr](https://www.flickr.com/services/api/misc.urls.html)

### Image page from image URL

	https://farm{farm-id}.staticflickr.com/{server-id}/{id}_{secret}.jpg
		or
	https://farm{farm-id}.staticflickr.com/{server-id}/{id}_{secret}_[mstzb].jpg
		or
	https://farm{farm-id}.staticflickr.com/{server-id}/{id}_{o-secret}_o.(jpg|gif|png)

And use [Flickr Api Explorer - flickr.photos.getInfo](https://www.flickr.com/services/api/explore/flickr.photos.getInfo) and fill photo_id with `{id}` and secret with `{secret}`

## Facebook

### Image page from image URL

1. from `http://sphotos-b.ak.fbcdn.net/hphotos-ak-ash4/395011_296213017144925_709418796_n.png`
2. give `296213017144925`
3. final `http://facebook.com/296213017144925`

### Get album images href

	// Exemple: https://www.facebook.com/Simoneconti88/media_set?set=a.3415113746951.2152114.1543299430&type=3
	console.log(Array.prototype.map.call(document.querySelectorAll("#album_photos_pagelet a.uiMediaThumb"), function (a) {
		return (new URL(a.href)).searchParams.get("src");
	}).join("\n"));

## Crédit Agricole

### Crédit Agricole Login

https://github.com/brutasse/dotfiles/blob/master/bin/ca
https://github.com/bouil/userscripts/tree/master/src
https://www.languedoc-s2-g2-enligne.credit-agricole.fr/stb/entreeBam?origine=vitrine&situationTravail=BANQUAIRE&canal=WEB&&typeAuthentification=CLIC_ALLER
http://forum.ubuntu-fr.org/viewtopic.php?id=172360 https://github.com/bmispelon/pyCA
http://weboob.org/modules#mod_cragr

Hidden fields:

CCCRYC = num1pos,num2pos,num3pos,num4pos,num5pos,num6pos
CCCRYC2 = 000000 (one 0 for each code number)

see clicPosition()

	<td  onClick="clicPosition('13'); " ><a tabindex=
	14
	href="javascript:raf()" >
	&nbsp;&nbsp;3&nbsp;&nbsp;
	</a></td>

Crédit Agricole Alpes Provence						2014		https://www.ca-alpesprovence.fr/		https://www.alpesprovence-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole Alsace Vosges						DCIV2+frame	https://www.ca-alsace-vosges.fr/		https://www.alsace-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole Atlantique Vendée					DCIV2		https://www.ca-atlantique-vendee.fr/	https://www.atlantique-vendee-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole Brie Picardie						DCIV2+frame	https://www.ca-briepicardie.fr/			https://www.briepicardie-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole Centre Loire						DCIV2		https://www.ca-centreloire.fr/			https://www.centreloire-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole Centre-Est							DCIV2		https://www.ca-centrest.fr/				https://www.ce-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole Charente-Périgord					DCIV2b		https://www.ca-charente-perigord.fr/	https://www.charente-perigord-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole Corse								DCIV2		https://www.ca-corse.fr/				https://www.corse-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole d'Aquitaine							DCIV2b		https://www.ca-aquitaine.fr/			https://www.aquitaine-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole d'Ille-et-Vilaine					DCIV2		https://www.ca-illeetvilaine.fr/		https://www.illeetvilaine-g4-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole de Centre France					DCIV2		https://www.ca-centrefrance.fr/			https://www.cf-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole de Champagne-Bourgogne				DCIV2		https://www.ca-cb.fr/					https://www.cb-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole de Charente-Maritime Deux-Sèvres	DCIV2		https://www.ca-cmds.fr/					https://www.cmds-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole de Franche-Comté					DCIV2+frame	https://www.ca-franchecomte.fr/			https://www.franchecomte-g4-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole de Guadeloupe						DCIV2		https://www.ca-guadeloupe.fr/			https://www.guadeloupe-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole de l'Anjou et du Maine				DCIV2		https://www.ca-anjou-maine.fr/			https://www.anjou-maine-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole de la Martinique et de la Guyane	DCIV2		https://www.ca-martinique.fr/			https://www.martinique-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole de La Réunion						DCIV2		https://www.ca-reunion.fr/				https://www.reunion-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole de la Touraine et du Poitou			DCIV2		https://www.ca-tourainepoitou.fr/		https://www.tourainepoitou-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole de Lorraine							2015		https://www.ca-lorraine.fr/				https://www.lorraine-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole de Nord de France					DCIV2		https://www.ca-norddefrance.fr/			https://www.norddefrance-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole de Normandie						2016		https://www.ca-normandie.fr/			https://www.normand-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole de Normandie-Seine					DCIV2		https://www.ca-normandie-seine.fr/		https://www.normandie-seine-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole de Paris et d'Ile-de-France			DCIV2+frame	https://www.ca-paris.fr/				https://www.paris-g4-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole des Côtes d'Armor					DCIV2		https://www.ca-cotesdarmor.fr/			https://www.cotesdarmor-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole des Savoie							DCIV2		https://www.ca-des-savoie.fr/			https://www.ds-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole du Centre Ouest						DCIV2		https://www.ca-centreouest.fr/			https://www.centreouest-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole du Finistère						DCIV2		https://www.ca-finistere.fr/			https://www.finistere-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole du Languedoc						DCIV2		https://www.ca-languedoc.fr/			https://www.languedoc-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole du Morbihan							DCIV2		https://www.ca-morbihan.fr/				https://www.morbihan-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole du Nord Est							DCIV2		https://www.ca-nord-est.fr/				https://www.nord-est-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole Loire Haute-Loire					DCIV2		https://www.ca-loirehauteloire.fr/		https://www.lhl-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole Nord Midi-Pyrénées					DCIV2		https://www.ca-nmp.fr/					https://www.nmp-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole Provence Côte d'Azur				DCIV2		https://www.ca-pca.fr/					https://www.pca-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole Pyrénées Gascogne					DCIV2+frame	https://www.ca-pyrenees-gascogne.fr/	https://www.campg-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole Sud Méditerranée					DCIV2		https://www.ca-sudmed.fr/				https://www.sudmed-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole Sud Rhône-Alpes						DCIV2		https://www.ca-sudrhonealpes.fr/		https://www.sra-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole Toulouse 31							DCIV2		https://www.ca-toulouse31.fr/			https://www.toulousain-g3-enligne.credit-agricole.fr/stb/entreeBam
Crédit Agricole Val de France						DCIV2+frame	https://www.ca-valdefrance.fr/			https://www.valdefrance-g3-enligne.credit-agricole.fr/stb/entreeBam

DCIV2+frame: `startcomptes();`

### Regional Banks

http://www.ca-recrute.fr/connaitre_implantations.php
https://fr.wikipedia.org/wiki/Liste_des_caisses_r%C3%A9gionales_de_Cr%C3%A9dit_agricole

Alpes Provence
Alsace Vosges
Anjou et Maine
Aquitaine
Brie Picardie
Atlantique Vendée
Centre-est
Centre France
Centre Loire
Centre Ouest
Champagne-Bourgogne
Charente-Maritime Deux-Sèvres
Charente-Périgord
Corse
Côtes d'Armor
Finistère
Franche-Comté
Guadeloupe
Île-de-France
Ille-et-Vilaine
Languedoc
Loire Haute-Loire
Lorraine
Martinique et Guyane
Morbihan
Nord de France
Nord Est
Nord Midi Pyrénées
Normandie
Normandie-Seine
Provence Côte d'Azur
Pyrénées Gascogne
La Réunion
Savoie
Sud Méditerranée
Sud Rhône Alpes
Toulouse 31
Touraine et Poitou
Val de France

### Liste des codes banques du Réseau Crédit Agricole 

[LstBq_reseauCA - liste_banques_reseau_ca.pdf](https://www.aspone.fr/files/aspone/banques/liste_banques_reseau_ca.pdf)

Code BANQUE	FILIALE
10206	CRCA NORD EST
11006	CRCA CHAMPAGNE-BOURGOGNE
11206	CRCA NORD MIDI PYRENEES
11306	CRCA ALPES PROVENCE
11449	THEMIS
11706	CRCA CHAR.-MARIT.2 SEVRES
12006	CRCA CORSE
12206	CRCA COTES D ARMOR
12406	CRCA CHARENTE PERIGORD
12506	CRCA FRANCHE COMTE
12906	CRCA FINISTERE
13106	CRCA TOULOUSE 31
13210	CA Leasing
13306	CRCA AQUITAINE
13506	CRCA LANGUEDOC
13606	CRCA ILLE ET VILAINE
13906	CRCA SUD RHONE ALPES
14006	CRCA GUADELOUPE
14406	CRCA VAL DE FRANCE
14506	CRCA LOIRE - HTE LOIRE
14706	CRCA ATLANTIQUE VENDEE
14806	CRCA CENTRE LOIRE
15568	CREDIT LIFT
16006	CRCA MORBIHAN
16106	CRCA LORRAINE
16606	CRCA Normandie
16706	CRCA NORD DE FRANCE
16806	CRCA CENTRE FRANCE
16850	EUROFACTOR SA NV
16906	CRCA PYRENEES GASCOGNE
17106	CRCA SUD MEDITERRANEE
17206	CRCA ALSACE VOSGES
17806	CRCA CENTRE - EST
17859	BFO
17906	CRCA ANJOU MAINE
18106	CRCA SAVOIE
18206	BFT
18206	CRCA PARIS ILE DE FRANCE
18306	CRCA NORMANDIE SEINE
18706	CRCA BRIE PICARDIE
18729	BFC AG
19106	CRCA PROVENCE COTE D AZUR
19406	CRCA TOURAINE ET POITOU
19506	CRCA CENTRE OUEST
19806	CRCA MARTINIQUE
19906	CRCA REUNION
28860	FONCARIS
30002	LCL Crédit Lyonnais
30002	INTERFIMO
30006	CA-SA
31489	CA CIB 
41539	Sofinco