- [Valentin Simonov on Programming » AS3 is weird. True story!](http://wayback.archive.org/web/20130702055820/http://va.lent.in/blog/2010/03/08/as3-is-weird-true-story/)

Resources

- http://mycroft.mozdev.org/download.html?name=Actionscript+3
- http://www.brajeshwar.com/reference/as2/
- http://wiki.mediabox.fr/documentation/flash

Play generated pcm wave data

- http://www.flashbrighton.org/wordpress/?p=9

Ogg support

- http://flash.j-ogg.de/test_app.swf
- http://www.j-ogg.de/core/main?/index.html
- http://www.flumotion.net/cortado/
- http://jflac.sourceforge.net/
- http://www.jcraft.com/jorbis/
- [Ogg Vorbis Encoder for Flash: Alchemy Series Part 1 | Hook - Labs](http://labs.byhook.com/2011/02/15/ogg-vorbis-encoder-for-flash-alchemy-series-part-1/)

AS3 PNG

- http://www.5etdemi.com/blog/archives/2006/12/as3-png-encoder-faster-better/

- http://blog.je2050.de/imageprocessing-library/

Adobe(R) Flash(R) Video format (FLV) to MPEG4 Transcoder.

- http://sourceforge.net/projects/vixynet/

Rend engine for XHTML, SVG, XForms, XFrames, arbitrary XML (e.g. RSS), styled by CSS 3

- http://deng.com.br/
- http://www.flash-creations.com/notes/sample_svgtoflash.php
- http://blog.tiagocardoso.eu/mainada/comics-sketch/2008/07/04/svg-viewer-demo/

ColorMatrix

- http://www.adobe.com/devnet/flash/articles/matrix_transformations_print.html

- http://www.brajeshwar.com/reference/as2/
- http://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/index.html

- http://blog.pixelbreaker.com/flash/as30-jit-vs-interpreted/

AS architercural UML

- http://www.gskinner.com/gmodeler/app/run.html

Decompile & Protect

- http://articles.techrepublic.com.com/5100-22-5111586.html

Make screensaver

- http://www.instantstorm.com/features/

AVE Imperator

- http://www.ave-imperator.com/index.php

Bitmap

- http://blog.je2050.de/2007/09/03/optimized-seam-carving/
- http://blog.je2050.de/2007/08/28/analyzing-bitmaps-bigger-than-512x512/
- http://blog.je2050.de/2007/10/01/converting-a-number-to-4-bytes-and-vice-versa/

Gaia framework

- http://www.gaiaflashframework.com/

- http://rsizr.com/

Tween curves

- http://www.robertpenner.com/easing/easing_demo.html
- http://labs.zeh.com.br/blog/?p=120

Realtime image post-processing with flash

- http://www.lifeztream.com/blog/?p=99&language=en

Flash FPS Monitor AS2,AS3

- http://www.lifeztream.com/blog/?p=97&language=en

Disable Right clicking (JS)

- http://www.kirupa.com/forum/showthread.php?t=270568

Flash AS3 VM bytecode compiler

- http://code.google.com/p/as3c/

Windows 2003 serve Flv files

- http://kb.adobe.com/selfservice/viewContent.do?externalId=tn_19439&sliceId=2

???

- http://www.blog.lessrain.com/?p=552
- http://labs.zeh.com.br/blog/?p=95
- http://www.rockonflash.com/blog/?page_id=32
- http://www.rockonflash.com/blog/?p=29
- http://theflashblog.com/?p=197
- http://www.insearchofabrilliantwhitecloud.com/Papervision3D.htm
- http://labs.blitzagency.com/?p=118

AS 3.0 Language and Components Reference

- http://livedocs.adobe.com/flash/9.0/ActionScriptLangRefV3/
- http://help.adobe.com/en_US/AS3LCR/Flash_10.0/index.html

Raycasting

- http://www.bytearray.org/?p=67

Flash CS3 Fonts

- http://prinzipiell.com/2007/05/03/embed-fonts-with-as3/

- http://www.actionscriptclasses.com/

Math classes (AS2)

- http://members.shaw.ca/flashprogramming/wisASLibrary/wis/index.html

C++ to AS3

- http://blogs.adobe.com/kiwi/2006/05/as3_language_101_for_cc_coders.html

Download Player & Cie

- http://www.adobe.com/support/flashplayer/downloads.html

Old player versions

- http://kb.adobe.com/selfservice/viewContent.do?externalId=tn_14266&sliceId=1

Download Flex SDK

- http://opensource.adobe.com/wiki/display/flexsdk/Download+Flex+3

Speed up ExternalInterface in IE

- http://codinginparadise.org/weblog/2006/02/how-to-speed-up-flash-8s.html

TweenLite, TweenMax

- http://blog.greensock.com/category/tweening/

Bugs

- https://bugs.adobe.com/jira/browse/FP
- https://bugs.adobe.com/flashplayer/


## Fonts

Embed font with AS3:

	package
	{
		import flash.text.Font;
	
		[Embed( source="../../assets.swf", fontFamily="Arial Unicode MS", fontStyle="normal", fontWeight="normal", fontName="Embedded font name")]
		public class ArialUnicode extends Font
		{
		
		}
	}

- [Embedding fonts tutorial](http://www.adobe.com/devnet/flash/quickstart/embedding_fonts/) on Adobe Developer Connection

### Bitmap fonts

Flash renames bitmap fonts and adds the suffix: `__{size}_pt_st`, where `_{size}_` is the bitamp size of the font.

Exemple:

- Verdana in 12 pixels becomes `Verdana_12pt_st`
- Arial in 12 pixels becomes `Arial_12pt_st`

### Effects on no-embedded fonts (alpha, rotation, etc.)

In FlashPlayer 9, to apply alpha, use `filters`, cacheAsBitmap or blend mode "layer"

	textField.filters = [new BlurFilter(0,0,0)];//use empty filter to cache text
	//or
	textField.blendMode = BlendMode.LAYER;
	//and finaly
	textField.alpha = 0.5;

For other effect (rotation, scale, etc.) draw `TextField` in a `BitmapData`

In FlashPlayer 10, no more problems with alpha, but remain for transfrom effects like rotation, scale, etc.

In FlashPlayer 10 `flash.text.engine` natively support it

## Flash player

### Adoption / market penetration

6 to 9 month for all new version to reach ~90% of adoption

- [Adobe Flash Player figure adoption by version](http://www.adobe.com/products/player_census/flashplayer/version_penetration.html)
- [Graphic of adpotion during time for all version](http://spreadsheets.google.com/pub?key=pjaKnZUqwo-1XaUCJLlBQeA&amp;gid=0)

### Flash right click (disable ContextMenu)

	/**
	 * 
	 * Copyright 2007
	 * 
	 * Paulius Uza
	 * http://www.uza.lt
	 * http://www.uza.lt/blog/2007/08/solved-right-click-in-as3
	 * 
	 * Dan Florio
	 * http://www.polygeek.com
	 * 
	 * Project website:
	 * http://code.google.com/p/custom-context-menu/
	 * 
	 * --
	 * RightClick for Flash Player. 
	 * Version 0.6.2
	 * 
	 */
	
	var RightClick = {
		/**
		 *  Constructor
		 */ 
		init: function () {
			this.FlashObjectID = "customRightClick";
			this.FlashContainerID = "flashcontent";
			this.Cache = this.FlashObjectID;
			if(window.addEventListener){
				 window.addEventListener("mousedown", this.onGeckoMouse(), true);
			} else {
				document.getElementById(this.FlashContainerID).onmouseup = function() { document.getElementById(RightClick.FlashContainerID).releaseCapture(); }
				document.oncontextmenu = function(){ if(window.event.srcElement.id == RightClick.FlashObjectID) { return false; } else { RightClick.Cache = "nan"; }}
				document.getElementById(this.FlashContainerID).onmousedown = RightClick.onIEMouse;
			}
		},
		/**
		 * GECKO / WEBKIT event overkill
		 * @param {Object} eventObject
		 */
		killEvents: function(eventObject) {
			if(eventObject) {
				if (eventObject.stopPropagation) eventObject.stopPropagation();
				if (eventObject.preventDefault) eventObject.preventDefault();
				if (eventObject.preventCapture) eventObject.preventCapture();
		   		if (eventObject.preventBubble) eventObject.preventBubble();
			}
		},
		/**
		 * GECKO / WEBKIT call right click
		 * @param {Object} ev
		 */
		onGeckoMouse: function(ev) {
		  	return function(ev) {
			if (ev.button != 0) {
				RightClick.killEvents(ev);
				if(ev.target.id == RightClick.FlashObjectID &amp;&amp; RightClick.Cache == RightClick.FlashObjectID) {
					RightClick.call();
				}
				RightClick.Cache = ev.target.id;
			}
		  }
		},
		/**
		 * IE call right click
		 * @param {Object} ev
		 */
		onIEMouse: function() {
		  	if (event.button > 1) {
				if(window.event.srcElement.id == RightClick.FlashObjectID &amp;&amp; RightClick.Cache == RightClick.FlashObjectID) {
					RightClick.call(); 
				}
				document.getElementById(RightClick.FlashContainerID).setCapture();
				if(window.event.srcElement.id)
				RightClick.Cache = window.event.srcElement.id;
			}
		},
		/**
		 * Main call to Flash External Interface
		 */
		call: function() {
			document.getElementById(this.FlashObjectID).rightClick();
		}
	}

### `ExternalInterface` JavaScript evaluation

`ExternalInterface` evaluate given JavaScript string (anonymous functions): `ExternalInterface.call("(function(param1, param2) {/* javascript code here */})", parameter1, parameter2);`

Note: don’t use the dash character "-" or other special chars in the DOM id of your flash element. IE need id attribute for using ExtenralInterface, others need name attribute.

### IE native JavaScript function for hanlding Flash & JS exchanges

	function __flash__arrayToXML(obj)
	{
		var s = "<array>";
		for (var i=0; i<obj.length; i++)
			s += "<property id=\"" + i + "\">" + __flash__toXML(obj[i]) + "</property>";
		return s+"</array>";
	}
	
	function __flash__argumentsToXML(obj, index)
	{
		var s = "<arguments>";
		for (var i=index; i<obj.length; i++)
			s += __flash__toXML(obj[i]);
		return s+"</arguments>";
	}
	
	function __flash__objectToXML(obj)
	{
		var s = "<object>";
		for (var prop in obj)
			s += "<property id=\"" + prop + "\">" + __flash__toXML(obj[prop]) + "</property>";
		return s+"</object>";
	}
	
	function __flash__escapeXML(s)
	{
		return s.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/'/g, "&apos;");
	}
	
	function __flash__toXML(value)
	{
		var type = typeof(value);
		if (type == "string")
			return "<string>" + __flash__escapeXML(value) + "</string>";
		else if (type == "undefined")
			return "<undefined/>";
		else if (type == "number")
			return "<number>" + value + "</number>";
		else if (value == null)
			return "<null/>";
		else if (type == "boolean")
			return value ? "<true/>" : "<false/>";
		else if (value instanceof Date)
			return "<date>" + value.getTime() + "</date>";
		else if (value instanceof Array)
			return __flash__arrayToXML(value);
		else if (type == "object")
			return __flash__objectToXML(value);
		else
			return "<null/>"; //???
	}
	
	function __flash__addCallback(instance, name)
	{
		instance[name] = function()
			{ 
				return eval(instance.CallFunction("<invoke name=\""+name+"\" returntype=\"javascript\">" + __flash__argumentsToXML(arguments,0) + "</invoke>"));
			}
	}
	
	function __flash__removeCallback(instance, name)
	{
		instance[name] = null;
	}

- [IE ExternalInterface](http://www.pasz.com/articles/flash8ASDoc/files/external/ExternalInterface-as.html)

## Extending Flash

### Execute command line through JSFL

	FLfile.runCommandLine("command line here");

## Metadata

### Add document metadata in Flash:

	var frame = fl.getDocumentDOM().timelines[0].layers[0].frames[0];
	var headerText = "[SWF(width=800, height=800, backgroundColor=0xffffff, frameRate=24)]\n"
		+ "stage.align = StageAlign.TOP_LEFT;\n"
		+ "stage.scaleMode = StageScaleMode.NO_SCALE;\n\n";
	frame.actionScript = headerText + frame.actionScript;

### `[Transient]` metadata

	package foo
	{
		[RemoteClass(alias="foo.Bar")]
		public class Bar
		{
			// public field
			public var prop1:String;
			
			// private field but keeped
			[Transient]
			private var prop2:Array;
		}
	}

Applied in all places using AMF encoding (`RemoteObject`, `NetConnection`, `byteArray.readObject();`)

See `flash.net.registerClassAlias()`

### Use AS3 metadata

`-keep-as3-metadata+=Meta1,Meta2`

	package
	{
		[Meta2(param1 = "param 1 value")]
		public class TestClass
		{
			[Meta1(param1 = "param 1 value", param2 = "param 2 value")]
			public var test1:String;
			
			[Meta2(paramA = "param 1 value", paramB = "param 2 value")]
			public function get test2():String
			{
				return null;
			}
			
			public function set test2(val:String):void
			{
				
			}
			
			[Meta1(param1 = "param 1 value")]
			public function someMethod():void
			{
				
			}
		}
	}

	var classMetadatas:XMLList = describeType(TestClass).factory.metadata;
	var methodsMetadatas:XMLList = describeType(TestClass).factory.method.metadata;
	var variablesMetadatas:XMLList = describeType(TestClass).factory.variable.metadata;
	var accessorsMetadatas:XMLList = describeType(TestClass).factory.accessor.metadata;

## Conditional compilation

- [Flex 3 - Adobe Flex 3 Help](http://livedocs.adobe.com/flex/3/html/help.html?content=compilers_21.html)
- [C Preprocessor Fun - kirupaForum](http://www.kirupa.com/forum/showthread.php?t=256400)
 
	-define=namespace::variable_name,value

	CONDITIONAL_COMPILATION::value
	{
		//Do something only when compilation condition is verified
	}

	if(some condition)
	{
		//Do something
	}
	else
	{
		CONDITIONAL_COMPILATION::value
		{
			//Something only when compilation condition is verified
		}
	}

	CONDITIONAL_COMPILATION::value = 'true'

Inline

	package
	{
		CONFIG::debugging
		public class MyClass
		{
			//some declarations
		}
		
		CONFIG::release
		public class MyClass
		{
			//some declarations
		}
	}

	CONFIG::debugging = 'true'
	CONFIG::release = '!CONFIG::debugging'

	private static const companyName:String = NAMES::Company;

	NAMES::Company = '"Company name"'

Conditional compilation is string replacement

	CONDITIONAL_COMPILATION::value = '1 > 2'
	CONDITIONAL_COMPILATION::value1 = 'false'
	CONDITIONAL_COMPILATION::value2 = 'CONDITIONAL_COMPILATION::value1 && false'

## Libraries

- [Adrian Parr's Blog » Blog Archive » AS3 Code Libraries (APIs)](http://www.adrianparr.com/?p=83)

- [APE](http://www.cove.org/ape/index.htm)
- [Box2D Flash](http://box2dflash.sourceforge.net/)
- [Fisix Engine](http://www.fisixengine.com/)
- [FOAM](http://blog.generalrelativity.org/?p=17)
- [Glaze](http://code.google.com/p/glaze/)
- [Motor2](http://code.google.com/p/motor2/)
- [Physicsengine](http://lab.andre-michelle.com/physics-engine)
- [Papervision3d](http://code.google.com/p/papervision3d/)
- [FZip](http://codeazur.com.br/lab/fzip/)
- [ziplib](http://nochump.com/blog/?p=15)
- [QueueLoader](http://code.google.com/p/queueloader-as3/)
- [BulkLoader](http://code.google.com/p/bulk-loader/)
- [AS3 crypto](http://crypto.hurlant.com/)

## XML

### Intercept E4X XML events

	xml.setNotification(callback:Function);

	function callback(currentTarget:Object, type:String, target:Object, value:Object, detail:Object):void;

Types:

- `attributeAdded`: Occur when an attribute was added
- `attributeChanged`: Occur when an attribute was changed
- `attributeRemoved`: Occur when an attribute was removed
- `nodeAdded`: Occur when a node was added
- `nodeChanged`: Occur when a node was changed
- `nodeRemoved`: Occur when a node was removed
- `nameSet`: Occur when the node name changed
- `namespaceAdded`: Occur when a namespace was added to the node
- `namespaceRemoved`: Occur when a namespace was removed
- `namespaceSet`: Occur when the node's namespace changed
- `textSet`: Occur when a text node was added to the node
	
### E4X

Exemple:

	<node name="Mike" age="34"><address><![CDATA[Fake address]]></address></node>

Get in `items` all XML nodes `node`:

	xml.node.(items.push(new User(@name, uint(@age))));

The same but with address:

	xml.node.(
		items.push(item = new User(@name, uint(@age))),
		item.address = address[0].toString()
	);

Get all nodes with age greater than 30:

	xml.node.(int(@age)>30).(
		items.push(item = new User(@name, uint(@age))),
		item.address = address[0].toString()
	);

The same but with only one cycle

	xml.node.(
		// ?: condition
		int(@age)>30 ? (
			// if condition equals TRUE actions, separated by commas
			item = new User(@name, uint(@age)),
			items.push(item),
			item.address = address[0].toString()
		) : false // if condition equals FALSE actions
	);

### Application domain

Child SWF uses parent domain definitions. If defined there, otherwise its own.

	var childDefinitions:LoaderContext = new LoaderContext();
	childDefinitions.applicationDomain = new ApplicationDomain(ApplicationDomain.currentDomain);

child SWF adds its unique definitions to parent SWF; both SWFs share the same domain child SWFs definitions do not overwrite parents

	var addedDefinitions:LoaderContext = new LoaderContext();
	addedDefinitions.applicationDomain = ApplicationDomain.currentDomain;

child SWF domain is completely separate and each SWF uses its own definitions

	var separateDefinitions:LoaderContext = new LoaderContext();
	separateDefinitions.applicationDomain = new ApplicationDomain();

set loader context in load()

	myLoader.load(request, separateDefinitions);

## ASDocs

Bugs : [Talk:ASDoc:Creating ASDoc Comments - Adobe Labs](http://labs.adobe.com/wiki/index.php/Talk:ASDoc:Creating_ASDoc_Comments)

Don't use `<code></code>` in your @see text description.

The comment: `/** @see "oops can't document this." */` will also cause the same exception

- [Using ASDoc -- Flex 2.01](http://livedocs.adobe.com/flex/201/html/wwhelp/wwhimpl/common/html/wwhelp.htm?context=LiveDocs_Book_Parts&amp;file=asdoc_127_1.html)

## A better Flash

- Openness
- No standards
- Proprietary
- <del>Not on mobile/iphone</del>
- Binary format

- [Sites Flash : vingt-cinq raisons de dire non, Patrick Murris, Septembre 2002](http://patrick.murris.com/articles/flash25.htm)
- [Website Tools and Applications with Flash | Free NN/g Report](https://www.nngroup.com/reports/website-tools-and-applications-flash/)
- [Pourquoi flash est une technologie de merde :) - LinuxFr.org](http://linuxfr.org/users/psychoslave__/journaux/pourquoi-flash-est-une-technologie-de-merde)
- [Pour en finir avec Patrick Murris et pour commencer avec une critique de Flash intelligente - LinuxFr.org](http://linuxfr.org/users/tcws/journaux/pour-en-finir-avec-patrick-murris-et-pour-commencer-avec-une-cri)
- [Flash: 99% Bad](https://www.nngroup.com/articles/flash-99-percent-bad/)
- [Flash Sucks - I’m Mike](http://wayback.archive.org/web/20100611220541/http://immike.net/blog/2007/07/31/flash-sucks/)

### Solvable, common sense

- Make HTML alternative

#### Introductions

- Remove it
- Shorten it
- Give the ability to skip it

#### Search engine visibility

- Google and Yahoo have SWF reading ability
- Make a HTML alternative (better solution)

#### Accessibility

See [Accessibility](#Accessibility)

#### Takes long to load

- Use H264 rather than VP6 or Sorenson Spark Codecs
- Package your media (SWF, `flash.utils.ByteArray.uncompress`, `flash.utils.ByteArray.deflate`, [FZip](http://codeazur.com.br/lab/fzip/), [ziplib](http://nochump.com/blog/?p=15))
- Load handling, cache data ([QueueLoader](http://code.google.com/p/queueloader-as3/), [BulkLoader](http://code.google.com/p/bulk-loader/))
- Use AMF rather than XML ([AMFPHP](http://www.amfphp.org/), [Red5](http://red5.org/))
- Check unsed data (for SWF embeded classes: [`mxmlc -link-report=link-report.xml`](http://blog.iconara.net/2007/02/25/visualizing-mxmlcs-link-report/))

#### CPU hog

- Use low quality filters
- Use mipmap
- Use bitmap rather than vector
- [take care with `cacheAsBitmap`](http://www.bytearray.org/?p=290)
- Optimize code ([Joa Ebert's wiki](http://wiki.joa-ebert.com/index.php/Main_Page), [haXe](http://haxe.org/))

#### Can't bookmark pages / back history

- Use deep linking ([SWFAddress](http://sourceforge.net/projects/swfaddress/))

## Video and sound

	StreamClient(){
		onCuePoint(infos:Object):void
		onImageData(infos:Object):void
		onLastSecond(infos:Object):void
		onMetaData(infos:Object):void
		onPlayStatus(infos:Object):void
		onTextData(infos:Object):void
		onXMPData(infos:Object):void
	}

	// Dynamic Buffering
	// From http://sonnati.wordpress.com/2006/04/10/dynamic-buffering-revamping/ http://sonnati.wordpress.com/2005/12/03/241/
	
	// Init
	startBL = 2;
	mainBL = 15;
	in_ns.setBufferTime(startBL);
	in_ns.onStatus = function statusHandler(infoObject:Object) {
		if (infoObject["code"] == "NetStream.Buffer.Full"){
			in_ns.setBufferTime(mainBL);
		}
		if (infoObject["code"] == "NetStream.Buffer.Empty"){
			in_ns.setBufferTime(startBL);
		}
	}

	// Load video bytes
	// http://www.bytearray.org/?p=1689
	// retrieve the FLV stream
	var bytes:ByteArray = event.currentTarget.data;
	// put the NetStream class into Data Generation mode
	netstream.play(null);
	// before appending new bytes, reset the position to the beginning
	netstream.appendBytesAction(NetStreamAppendBytesAction.RESET_BEGIN);
	// append the FLV video bytes
	netstream.appendBytes(bytes);

	// HTTP Dynamic stream/HTTP Streaming
	public class MiniStream extends Sprite
	{
			private var _buffer:ByteArray = new ByteArray();
			private var _ns:NetStream;
			private var _nc:NetConnection;
			private var _video:Video;
			private var _tc:Number = 0;
			private var _ustream:URLStream;
			private var _elapsed_bytes:uint = 0;
		
			public function MiniStream(onVideo:Function)
			{
					_video = new Video(400,300);
					addChild(_video);
					_ustream = new URLStream();
					_ustream.addEventListener(IOErrorEvent.IO_ERROR, onErr);
					_ustream.addEventListener(ProgressEvent.PROGRESS, onProgress);
			}
		
			public function play():void
			{
					_nc = new NetConnection();
					_nc.connect(null);
			
					if(_ns)
					{
							_ns.removeEventListener(NetStatusEvent.NET_STATUS, onStatus);
					}	 
					_ns = new NetStream(_nc);
					_ns.addEventListener(NetStatusEvent.NET_STATUS, onStatus);
					_ns.client = {};
					_ns.bufferTime = 3;
					_video.attachNetStream(_ns);
			
					_ns.play(null);
					_ns.appendBytesAction(NetStreamAppendBytesAction.RESET_BEGIN);
			
					_ustream.load("http://example.com/h264vid.flv");
			}
		
			private function onStatus(e:NetStatusEvent):void
			{
					trace(e.info.code);
			}
		
			private function onProgress(e:ProgressEvent):void
			{
					//stores in our BA buffer
					_ustream.readBytes(_buffer,0,_ustream.bytesAvailable);
					_buffer.position = 0;
					if(_buffer.bytesAvailable > 0)
					{
							_ns.appendBytes(_buffer);
							_elapsed_bytes += _buffer.length;
							_buffer.clear();
					}
			}
		
			private function onErr(e:IOErrorEvent):void
			{
					//trace("ERROR", e.text);
			}
	}

- [Red5](http://red5.org/)
- [MediaCoder](http://mediacoder.sourceforge.net/)
- [Fake Streaming FLV video via PHP](http://www.flashcomguru.com/index.cfm/2005/11/2/Streaming-flv-video-via-PHP-take-two)
- [FlashPlayer – h264](http://h264.code-shop.com/trac/wiki/FlashPlayer) - pseudo streaming with MP4 file
- [actionscript - How to implement the Adobe HTTP Streaming spec without using their Streaming server - Stack Overflow](https://stackoverflow.com/questions/4443146/how-to-implement-the-adobe-http-streaming-spec-without-using-their-streaming-serv)
- [opensource - Revision 24058: /osmf/trunk/framework/OSMF/org/osmf/net/httpstreaming/f4f](http://opensource.adobe.com/svn/opensource/osmf/trunk/framework/OSMF/org/osmf/net/httpstreaming/f4f/)
- [flex - How to get current frame of currently playing video file? - Stack Overflow](https://stackoverflow.com/questions/4366093/how-to-get-current-frame-of-currently-playing-video-file)
- [Live video streaming online | Adobe HTTP Dynamic Streaming](http://www.adobe.com/products/hds-dynamic-streaming.html)
- [Adobe ActionScript 3.0 * Using cue points and metadata](http://help.adobe.com/en_US/ActionScript/3.0_ProgrammingAS3/WSD30FA424-950E-43ba-96C8-99B926943FE7.html)

## Display

- [Bitmap Drawing API](http://www.bytearray.org/?p=67)
- [Display list wikipedia](http://en.wikipedia.org/wiki/Display_list)
- [Clipping wikipedia](http://en.wikipedia.org/wiki/Clipping_%28computer_graphics%29)
- [Category 3D computer graphics wikipedia](http://en.wikipedia.org/wiki/Category:3D_computer_graphics)
	
### Draw a `DisplayObject` into a `BitmapData`

	var displayObject:DisplayObject;
	var bounds:Rectangle = displayObject.getBounds(displayObject);
	var bitmapData:BitmapData = new BitmapData(uint(bounds.width + 0.5), uint(bounds.height + 0.5), true, 0);
	bitmapData.draw(displayObject, new Matrix(1, 0, 0, 1, -bounds.x, -bounds.y));

### Pixelize a `DisplayObject`

Draw it into a `BitmapData` (see above) with scale

	var displayObject:DisplayObject;
	var scale:Number = 0.5;
	var bounds:Rectangle = displayObject.getBounds(displayObject);
	var bitmapData:BitmapData = new BitmapData(uint((bounds.width + 0.5) * scale), uint((bounds.height + 0.5) * scale), true, 0);
	bitmapData.draw(displayObject, new Matrix(scale, 0, 0, scale, -bounds.x * scale, -bounds.y * scale));

Then, set bitmap width & height to original sizes (`bounds.width` & `bounds.height`)

### NetStream `BitmapData` capture

	video.attachNetStream(null);
	var snapshot:BitmapData = new BitmapData(…);
	snapshot.draw(video);
	video.attachNetStream(stream);

### Outlined Text

	new GlowFilter(0x000000, 1.0, 2.0, 2.0, 10, 2)

## Network & File IO

### Upload file with `URLLoader`	

	/**
	* Original:
	* http://www.jooce.com/blog/?p=143
	* Uploads a file using a given URLLoader object.
	* 
	* @param loader The URLLoader object to use
	* @param url The location of the script recieving the upload
	* @param file The file to upload
	* @param fileName The name of the file
	* @param contentType The content-type of the file
	*/
	
	var loader:URLLoader = new URLLoader();
	var file:ByteArray = new ByteArray();
	file.writeUTFBytes("Fake file content text.");
	
	var request:URLRequest = new URLRequest("my/path/upload.php");
	var fileName:String = "myfile.txt";
	var contentType:String = "text/plain";//"application/octet-stream"
	
	var i:int;
	var boundary:String = "--";
	var postData:ByteArray = new ByteArray;
	var bytes:String;
	
	for(i = 0; i < 0x10; i++)
		boundary += String.fromCharCode(int(97 + Math.random() * 25));
	
	loader.dataFormat = URLLoaderDataFormat.BINARY;
	
	request.url = url;
	request.contentType = "multipart/form-data; boundary=" + boundary;
	request.method = URLRequestMethod.POST;
	
	postData.endian = Endian.BIG_ENDIAN;
	
	// -- + boundary
	postData.writeShort(0x2d2d);
	for (i = 0; i < boundary.length; i++)
		postData.writeByte(boundary.charCodeAt(i));
	
	// line break
	postData.writeShort(0x0d0a);
	
	// content disposition
	bytes = "Content-Disposition: form-data; name=\"Filename\"";
	for (i = 0; i < bytes.length; i++)
		postData.writeByte(bytes.charCodeAt(i));
	
	// 2 line breaks
	postData.writeInt(0x0d0a0d0a);
	
	// file name
	postData.writeUTFBytes(fileName);
	
	// line break
	postData.writeShort(0x0d0a);
	
	// -- + boundary
	postData.writeShort(0x2d2d);
	for (i = 0; i < boundary.length; i++)
		postData.writeByte(boundary.charCodeAt(i));
	
	// line break
	postData.writeShort(0x0d0a);
	
	// content disposition
	bytes = "Content-Disposition: form-data; name=\"Filedata\"; filename=\"";
	for (i = 0; i < bytes.length; i++)
		postData.writeByte(bytes.charCodeAt(i));
	
	// file name
	postData.writeUTFBytes(fileName);
	
	// missing "
	postData.writeByte(0x22);
	
	// line break
	postData.writeShort(0x0d0a);
	
	// content type
	bytes = "Content-Type: " + contentType;
	for (i = 0; i < bytes.length; i++)
		postData.writeByte(bytes.charCodeAt(i));
	
	// 2 line breaks
	postData.writeInt(0x0d0a0d0a);
	
	// file data
	postData.writeBytes(file, 0, file.length);
	
	// line break
	postData.writeShort(0x0d0a);
	
	// -- + boundary
	postData.writeShort(0x2d2d);
	for (i = 0; i < boundary.length; i++)
		postData.writeByte(boundary.charCodeAt(i));
	
	// line break 
	postData.writeShort(0x0d0a);
	
	// upload field
	bytes = "Content-Disposition: form-data; name=\"Upload\"";
	for (i = 0; i < bytes.length; i++)
		postData.writeByte(bytes.charCodeAt(i));
	
	// 2 line breaks
	postData.writeInt(0x0d0a0d0a);
	
	// submit
	bytes = "Submit Query";
	for (i = 0; i < bytes.length; i++)
		postData.writeByte(bytes.charCodeAt(i));
	
	// line break
	postData.writeShort(0x0d0a);
	
	// -- + boundary + --
	postData.writeShort(0x2d2d);
	for (i = 0; i < boundary.length; i++)
		postData.writeByte(boundary.charCodeAt(i));
	postData.writeShort(0x2d2d);
	
	request.data = postData;
	request.requestHeaders.push(new URLRequestHeader("Cache-Control", "no-cache"));
	loader.load(request);

- https://discuss.as3lang.org/t/send-a-file-to-a-server-as-an-attachment-in-an-urlrequest-urlloader/320

## Common errors

### Return nodes are not same object

	var dic:Dictionary = new Dictionary(false);
	var data:XML = <data><node/></data>;
	dic[data] = true;
	var node:XML = data.node[0];
	
	trace(dic[data])
	//output: true
	
	trace(dic[node.parent()])//must be true (see after)
	//output: undefined
	
	for(var key:* in dic)
		trace(key == node.parent(), key === node.parent())//output: true true

## `addFrameScript()`

Note: here `frame` is zero base index.

	movieClip.addFrameScript(frame:uint, frameScript:Function, ...args):void

	//Add multiples frames scripts in same time
	movieClip.addFrameScript(0, frame1Script, 3, frame3Script, 20, frame20Script);
	
	//Remove frame script
	movieClip.addFrameScript(0, null);
		
## Code tips & tricks

- [Kirupa "ActionScript 3 Tip of the Day" thread](http://www.kirupa.com/forum/showthread.php?t=223798)
- [polygonal labs » Bitwise gems - fast integer math](http://lab.polygonal.de/2007/05/10/bitwise-gems-fast-integer-math/)
- [Some ActionScript 3.0 Optimizations | Rozengain.com - Creative Technology Blog](http://rozengain.com/?postid=35)
- [AS3 optimization at blog.joa-ebert.com – Blog of Joa Ebert](http://blog.je2050.de/2005/11/02/as3-optimization/)
- [Random Etc. - Optimising Actionscript 3](http://www.tom-carden.co.uk/2008/01/07/optimising-actionscript-3/)
- [senocular.com - Flash Tutorials](http://www.senocular.com/flash/tutorials/)

### Convert `Array` to `Vector.<T>`

	var array:Array = ["a", "b", "c"];
	var vector:Vector.<String> = Vector.<String>(array);

### Conditional switch statement

	var value:int = 2;
	switch(value){
		case < 1:
			trace("Value is less than 1");
			break;
		case 2:
			trace("Value definitely equals 2");
			break;
		case >= 3:
			trace("Value is greater than or equal to 3");
			break;
		case > 1 && < 3:
			trace("Value is greater than 3 and less than 5");
			break;
		case !== 5:
			trace("Value definitely doesn't equal 5");
			break;
	}

### Compare real types of objects

With (final contructor) != `is` keyword

	public static function typeEquals(object:*, constructor:Class):Boolean
	{
		return o == null ? false : Object(object).constructor == constructor;
	}

### Extends `Array`

And support `Array`'s arguments

	public class SubArray extends Array
	{
		function SubArray():void
		{
			super.constructor.apply(this, arguments);
		}
	}

### Is SubClass extends SuperClass

	SuperClass.prototype.isPrototypeOf(SubClass.prototype);

### Disallow instantiation

	if(!instantiationAllowed)
		// %1 class cannot be instantiated.
		Error.throwError(IllegalOperationError, 2012, "MyClass");

### Desactivate constructor super call

	if (0)
		super();

### Estimate sound duration while loading

	var duration:Number = this.sound.length;
	if (this.sound.bytesTotal != this.sound.bytesLoaded && duration > 0)
		duration = (this.sound.bytesTotal / (this.sound.bytesLoaded / duration));

### Forcing Garbage collecting

	try
	{
		new LocalConnection().connect('foo');
		new LocalConnection().connect('foo');//The GC will perform a full mark/sweep on the second call.
	} catch (error:*) {}

### `LocalConnection` limits

`LocalConnection.send()` limited to 40960 bytes. For one ByteArray is limited to 40864 (+ AMF data for one ByteArray: 96 bytes ?)

### Throw error

	Error.throwError(RangeError, 1005 /*kArrayIndexNotIntegerError*/, -3);//throw Error #1005: Array index is not an integer (-3)
	Error.throwError(type:Class, errorID:uint, ...rest);

### Package are namespace

	namespace flash_events = "flash.events";
	trace(flash_events::MouseEvent); //output: [class MouseEvent]

### Loading events order

1.  `Event.OPEN`
2.  `ProgressEvent.PROGRESS * n`
3.  `Event.INIT` (if SWF, first frame loaded)
4.  `ProgressEvent.PROGRESS * n`
5.  `HTTPStatusEvent.HTTP_STATUS`
6.  `Event.COMPLETE`

### AS Native & Product

- [flashcoders:undocumented:asnative Open Source Flash](http://osflash.org/flashcoders/undocumented/asnative)

`https://www.macromedia.com/bin/flashdownload.cgi?product=fpupdatept&amp;signed=true&amp;A=t&amp;SA=t&amp;SV=t&amp;EV=t&amp;MP3=t&amp;AE=t&amp;VE=t&amp;ACC=f&amp;PR=t&amp;SP=t&amp;SB=f&amp;DEB=t&amp;V=WIN%209%2C0%2C115%2C0&amp;M=Adobe%20Windows&amp;R=1920x1200&amp;DP=72&amp;COL=color&amp;AR=1.0&amp;OS=Windows%20XP&amp;L=fr&amp;IME=f&amp;PT=External&amp;AVD=f&amp;LFD=f&amp;WD=f&amp;TLS=t&amp;what=descr…`

	Product("digitaleditions2x0")
	//AS2
	var p = new System.Product("notepad");
	p.download();
	trace(p.IsInstalled());
	trace(p.Launch());
	And you copy "notepad.exe" to
	// ApplicationData\Macromedia\FlashPlayer\www.macromedia.com\bin\notepad\
	
	//AS3
	var p:ProductManager = new adobe.utils.ProductManager()
	p.launch();
	p.download();
	p.installed;
	p.installedVersion;
	p.running;
	
	//AS3 launch AIR app
	myLauncher:ProductManager = new ProductManager("airappinstaller");
	var myArguments:Array = ["-launch", appID, publisherID, theOtherAppArguments];
	myLauncher.launch(myArguments.join(" "));

- `fpupdateax`
- `digitaleditions2x0`
- `airappinstaller`
- `fpupdatepl`

### Access to all members (inc. private) of a specified object (debug player only)

	import flash.sampler.getMemberNames;
	//…
	var members:Object = getMemberNames(myObject);
	
	for each (var name:QName in members)
		if (name.localName == "memberName")
			trace(myObject[name]);

### Get class from Loaded SWF

	loader.contentLoaderInfo.applicationDomain.getDefinition("FullQualifiedClassName") as Class

### Clone object

Not work on `DisplayObject`s

	package nc.utils
	{
		import flash.utils.ByteArray;
		import flash.net.registerClassAlias;
		import flash.utils.getQualifiedClassName;
		import flash.net.getClassByAlias;
		import flash.utils.describeType;
		import flash.utils.getDefinitionByName;
		
		public class ObjectUtils
		{
			/**
			*	Clone an Object
			*
			*	@param object The Object to clone (Object is not a part of the displayList
			*	and object don't need arguments in constructor)
			*
			*	@param type The Class of the Object to clone.
			*
			*	@return a clone of Object
			*/
			public static function clone(object:*):*
			{
				var alias:String = getQualifiedClassName(object).split('::').join('.');
				var type:Class = getDefinitionByName(alias) as Class;
				
				traverse(object);
				
				var r:ByteArray = new ByteArray();
				r.writeObject(object);
				r.position = 0;
				var clone:*;
			
				try
				{
					clone = r.readObject();
					return clone as type;
				}
				catch(error:TypeError)
				{ 
					//trace(error);
				}
			
				return null;
			}
			
			private static function traverse(object:*):void
			{
				var alias : String = getQualifiedClassName(object).split('::').join('.');
				var type : Class = getDefinitionByName(alias) as Class;
				try
				{
					getClassByAlias(alias);
				}
				catch(error:ReferenceError)
				{
					registerClassAlias(alias, type); 
				}
				
				var x:XML = describeType(object),
					childrens:XMLList = x.children(),
					l:int = childrens.length(),
					i:int = -1,
					xClass:XML;
			
				while (++i<l)
				{
					xClass = childrens[i] as XML;
					
					registerAll(xClass);
					
					var childName:String = xClass.attribute("name");
					if(xClass.name() == "variable")
					{
						var childObj:* = object[childName];
						if(null != childObj)
							traverse(childObj);
					}
				}
			}
			
			private static function registerAll(x:XML):void
			{
				var a : Array = ['type','declaredBy','returnType'],
				l : int = a.length,
				i : int = -1,
				raw : String,
				aSplit : Array,
				type : Class,
				alias : String;
				while (++i<l)
				{
					raw = x.attribute(a[i] as String).toString();
					if (raw.indexOf('::') != -1)
					{
						aSplit = raw.split('::');
						if (aSplit.length == 2)
						{
							alias = aSplit.join('.');
							type = getDefinitionByName(alias) as Class;
							try 
							{
								getClassByAlias(alias)
							}
							catch(error:ReferenceError)
							{
								trace("Register --> " + alias + " as " + type);
								registerClassAlias(alias, type);
							}
						}
					}
				}
			}
		}
	}

- http://niko.informatif.org/blog/2007_07_20_clone_an_object_in_as3

### Allow socket
		
	<?xml version="1.0" encoding="UTF-8"?>
	<cross-domain-policy xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://www.adobe.com/xml/schemas/PolicyFileSocket.xsd">;
		<allow-access-from domain="*" to-ports="*" secure="false" />
		<site-control permitted-cross-domain-policies="master-only" />
	</cross-domain-policy>

Deliver policy file with command line PHP

	#!/usr/local/bin/php
	<?php
	/**
	 * Flash Policy Service v0.9.c
	 *
	 * This script listens for <policy-file-request/> on port 843 and serves up
	 * an xml crossdomain policy file. This sort of service is necessary if any
	 * flash content is going to connect to sockets on the running host.
	 *
	 * I have made every effort to package everything you need into a single
	 * file here, even though it could easily have been split into 3 or more
	 * scripts.
	 *
	 * Requirements:
	 *  - PHP 5 with sockets, pcntl, and posix extensions
	 *  - Root access (to bind to a <1024 port)
	 *
	 * Use:
	 *  Simply execute the script from the command line as root:
	 *	# ./FlashPolicyService.php
	 *  You can enable debug mode by invoking the script with '-d' as a parameter:
	 *	# ./FlashPolicyService.php -d
	 *  To stop the daemon, simply send it a SIGTERM and it should attempt to
	 *  exit cleanly.
	 *
	 *  If you get 'bad interpreter' errors or the like, change the #! line to
	 *  reflect the actual installed location of your php cli.
	 *
	 * Configuration:
	 *  At present, there aren't very many config options. Simply edit the
	 *  section immediately following this header. Options are commented.
	 *
	 * License:
	 *  This code is made available under a Creative Commons Attribution 3.0
	 *  License. Basically, you can use it however you like, but I would
	 *  appreciate some credit when you do.
	 *
	 * Disclaimer:
	 *  I make no guarantees that this code won't make your server explode in a
	 *  shower of blue flames. However, I don't expect that it will. I am actually
	 *  confident that this code will be helpful.
	 *
	 *  That said, this is still my beta release. If you find any bugs, please
	 *  let me know so I can fix them.
	 *
	 * - Ammon Lauritzen [Apr 21, '08]
	 - http://ammonlauritzen.com/blog/2008/04/22/flash-policy-service-daemon/
	 *
	 * Changelog
	 * 0.9.c
	 - - Fixed some typoes that were the result of how I combined everything
	 *	 into a single file. Thanks Alex!
	 * 0.9.b
	 - - Original version to be posted at this url.
	 * 0.9.a
	 - - Original proof of concept code posted online.
	 */
	 
	/*** Config ***/
	
	// where should we save the log output?
	$log_filename = "/tmp/flash-policy.log";
	
	// uncomment these lines to choose which user to run the daemon as
	// default behavior is to look up and attempt to run as 'nobody'
	# $daemon_uid = 99;
	# $daemon_gid = 99;
	
	// set this if you want to use an external file in stead of the default
	$xml_filename = "";
	$default_xml =
		'<'.'?xml version="1.0" encoding="UTF-8"?'.'>'.
		'<cross-domain-policy xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://www.adobe.com/xml/schemas/PolicyFileSocket.xsd">'.
			'<allow-access-from domain="*" to-ports="*" secure="false" />'.
			'<site-control permitted-cross-domain-policies="all" />'.
		'</cross-domain-policy>';
		
	/*** You shouldn't have to edit anything below here ***/
	
	/////////////////////////////////////////////////////////////////////////////
	class Logger {
		public function __construct($logfile) {
			$this->logfile = $logfile;
			$this->open_log();
		}// end: constructor
		
		public function __destruct() {
			@fflush($this->fh);
			@fclose($this->fh);
		}// end: destructor
		
		public function log($msg) {
			// deal with redundant log spam
			if($msg == $this->last_msg) {
				$this->last_msg_count++;
				return;
			} else if($this->last_msg_count) {
				$this->write("Last message repeated ".$this->last_msg_count." times.");
			}
			$this->lasg_msg = $msg;
			$this->last_msg_count = 0;
			
			// actually write the log message out
			$this->write($msg);
		}// end: log
		
		private function write($msg) {
			$msg = sprintf("[%s] %s\n",date("y-m-d H:i:s"),$msg);
			$succ = @fwrite($this->fh, $msg);
			if($succ === FALSE) {
				echo $msg;
			}
		}// end: write
		
		private function open_log() {
			if(!file_exists($this->logfile)) {
				touch($this->logfile);
				chmod($this->logfile, 0664);
			}
			$this->fh = @fopen($this->logfile, "a");
		}
	}// end: logger class
	
	/////////////////////////////////////////////////////////////////////////////
	class Daemon {
		public function __construct() {
			error_reporting(0);
			set_time_limit(0);
			
			global $log_filename, $pid_filename;
			$this->logger = new Logger($log_filename);
			$this->pid_filename = $pid_filename;
			
			$this->log_tag = $this->daemon_tag = "launcher";
			$this->debug("constructed", $this->daemon_tag);
		}// end: constructor
		
		public function __destruct() {
			$this->debug("destructing", $this->daemon_tag);
		}// end: destructor
		
		protected function log($msg, $tag = false) {
			if($tag == false)
				$tag = $this->log_tag;
			$this->logger->log($tag.": ".$msg);
		}// end: log
		protected function debug($msg, $tag = false) {
			if(DEBUG)
				$this->log($msg, $tag);
		}// end: debug
		
		protected function main() {
			$this->log("override main() in daemon subclass", $this->daemon_tag);
			$this->stop();
		}// end: main
		
		public function start() {
			$this->log("starting daemon", $this->daemon_tag);
			if(!$this->_start()) {
				$this->log("unable to start daemon", $this->daemon_tag);
				return;
			}
			
			// report execution details
			$this->log("uid = ".posix_getuid().", gid = ".posix_getgid());
			$this->log("cwd = ".getcwd());
			
			// invoke main loop
			$this->running = true;
			while($this->running) {
				$this->main();
			}
		}// end: start
		private function _start() {
			if(!$this->_fork()) {
				return false;
			}// end: try to fork
			
			if(!posix_setsid()) {
				$this->log("unable to setsid()", $this->daemon_tag);
				return false;
			}// end: try to set sid
	   
			if(!$this->_suid()) {
				return false;
			}// end: try to set uid
	   
			// register signal handler
			declare(ticks = 1);
			pcntl_signal(SIGTERM, array(&$this, "on_sigterm"));
			// chdir somewhere moderately safe by default
			chdir('/tmp');
			return true;
		}// end: _start
		private function _fork() {
			$this->log("forking…", $this->daemon_tag);
			$pid = pcntl_fork();
			if($pid == -1) {
				// error
				$this->log("unable to fork", $this->daemon_tag);
				return false;
			} else if($pid) {
				// parent
				$this->debug("done with parent", $this->daemon_tag);
				exit(0);
			} else {
				// child
				$this->daemon_tag = "daemon";
				$this->child = true;
				$this->pid = posix_getpid();
				$this->debug("child pid = ".$this->pid);
				return true;
			}
		}// end: _fork
		private function _suid() {
			global $daemon_uid, $daemon_gid;
			if(!isset($daemon_uid) || !isset($daemon_gid)) {
				// we didn't get a uid/gid, try to make one up
				$this->debug("searching for info on 'nobody'", $this->daemon_tag);
				$res = posix_getpwnam("nobody");
				if($res !== FALSE) {
					$uid = $res['uid'];
					$gid = $res['gid'];
				} else {
					// the 'nobody' user doesn't exist on this system, refuse
					// to daemonize as root
					$this->log("unable to find info on 'nobody' user", $this->daemon_tag);
					return false;
				}
			} else {
				$this->debug("got uid/gid of $daemon_uid/$daemon_gid", $this->daemon_tag);
				$uid = $daemon_uid;
				$gid = $daemon_gid;
			}
			// actually try to switch now
			if(!posix_setgid($gid)) {
				$this->log("unable to set gid to ".$gid, $this->daemon_tag);
				return false;
			} else if(!posix_setuid($uid)) {
				$this->log("unable to set uid to ".$uid, $this->daemon_tag);
				return false;
			} else {
				return true;
			}
		}// end: _suid
		
		public function stop() {
			$this->log("stopping daemon", $this->daemon_tag);
			$this->running = false;
		}// end: stop
		
		protected function on_sigterm($sig) {
			if($sig == SIGTERM) {
				$this->log("got SIGTERM", $this->daemon_tag);
				$this->stop();
				exit(0);
			}
		}// end: on_sigterm
	}// end: daemon class
	
	/////////////////////////////////////////////////////////////////////////////
	class FlashPolicyService extends Daemon {
		public function __construct() {
			parent::__construct();
			$this->log_tag = "fps";
			$this->debug("constructing");
			
			$this->connections = array();
			$this->request_str = "<policy-file-request/>";
			$this->port = 843;
			
			// get our xml
			global $xml_filename, $default_xml;
			if(strlen($xml_filename) == 0 || !file_exists($xml_filename)) {
				$this->log("unable to read xml from '$xml_filename', using default");
				$this->xml = $default_xml;
			} else {
				$this->log("reading policy xml from $xml_filename");
				$this->xml = file_get_contents($xml_filename);
			}
			$this->debug("policy xml: ".$this->xml);
			// make sure we're null terminated
			$this->xml = trim($this->xml)."\n\0";
			
			// and get going
			$this->init();
		}// end: constructor
		
		public function __destruct() {
			parent::__destruct();
			if($this->sock)
				@fclose($this->sock);
		}// end: destructor
		
		private function init() {
			$this->debug("init…");
			if($this->check_socket()) {
				parent::start();
			} else {
				$this->log("not starting daemon");
			}
		}// end: init
		
		protected function main() {
			if($this->sock) {
				while(true) {
					$this->accept_socket();
				}
			} else {
				$this->log("server socket is closed?!");
				parent::stop();
			}
			// paranoia to keep from absolutely hosing cpu if something goes wrong
			usleep(10000);	// 10ms
		}// end: main
		
		private function check_socket() {
			$this->sock = @socket_create(AF_INET, SOCK_STREAM, SOL_TCP);
			if(!$this->sock) {
				$this->log("unable to create socket");
			} else {
				$succ = @socket_bind($this->sock, "0.0.0.0", $this->port);
				if(!$succ) {
					$this->log("unable to bind to port ".$this->port);
				} else {
					$backlog = 100;
					$succ = @socket_listen($this->sock, $backlog);
					if(!$succ) {
						$this->log("unable to listen with backlog of $backlog");
					} else {
						// everything's good
						return true;
					}
				}// end: able to bind
			}// end: able to create socket
			
			// if we got here, it's an error. abort.
			$errno = socket_last_error($this->sock);
			$errstr = socket_strerror($errno);
			$this->log("socket error: $errno: $errstr");
			return false;
		}// end: check_socket
		
		private function accept_socket() {
			$r_socks = array_merge(array($this->sock), $this->connections);
			$this->debug("selecting on ".count($r_socks)." sockets");
	   
			// block until something interesting happens
			$select = @socket_select($r_socks, $w_socks = NULL, $e_socks = NULL, NULL);
			if(!$select)
				return;
				
			// did we get a new connection?
			if(in_array($this->sock, $r_socks)) {
				$conn = @socket_accept($this->sock);
				if($conn !== false)
					@socket_getpeername($conn, $addr);
				$this->log("connection accepted from $addr, $conn");
				$this->connections[] = $conn;
			}// end: got a new connection
			
			// check for policy requests
			foreach($r_socks as $conn) {
				// ignore the server socket
				if($conn == $this->sock)
					continue;
					
				// read from the client
				$data = @socket_read($conn, 1024);
				if($data === FALSE) {
					$this->log("got disconnect from $conn");
				}// end: client closed connection
				else {
					$this->debug("read '".trim($data)."' from $conn");
					if(strpos($data, $this->request_str) !== FALSE) {
						$this->log("sending policy xml to $conn");
						@socket_write($conn, $this->xml);
					} else {
						$this->log("got invalid request from $conn");
					}
				}// end: got data from the client
				
				// and always disconnect after having read something, whether
				// it was a valid request or not - especially if it wasn't ;)
				@socket_close($conn);
				$key = array_search($conn, $this->connections);
				if($key !== FALSE)
					unset($this->connections[$key]);
			}// end: foreach socket
		}// end: accept_socket
		
	}// end: flash policy service class
	
	/////////////////////////////////////////////////////////////////////////////
	/**
	 * Actual execution code here. This checks if the php install has all of our
	 * requisite extensions, makes sure we're launching as root, and checks if
	 * debug mode was requested before actually starting the daemon.
	 */
	
	// make sure we have required extensions
	$required_extensions = array("sockets", "posix", "pcntl");
	$missing_extension = false;
	foreach($required_extensions as $ext) {
		if(!extension_loaded($ext)) {
			echo "Missing required php extension '$ext'.n";
			$missing_extension = true;
		}
	}
	if($missing_extension) {
		exit(1);
	}
	
	// make sure we launch as root, otherwise we can't bind to 843
	if(posix_getuid() != 0 || posix_getgid() != 0) {
		echo "Policy service must be started as root.n";
		exit(1);
	}
	
	// see if we're in debug mode
	define("DEBUG", in_array('-d',$argv));
	
	// start the daemon
	$fps = new FlashPolicyService();
	?>

	#!/usr/bin/php -q
	<?php
	
	error_reporting(E_ALL);
	
	set_time_limit(0);
	
	ob_implicit_flush();
	
	echo "Enter Server IP:\n";
	$address = trim(fgets(STDIN));
	//$address = '127.0.0.1';
	echo "Enter Port:\n";
	$port = trim(fgets(STDIN));
	//$port = 9999;
	echo "Attempting to connect to $address:$port\n";
	
	//---- Function to Send out Messages to Everyone Connected ----------------------------------------
	
	function send_Message($allclient, $buf) {
		global $client_list;
		foreach($allclient as $client) {
		if($client_list[$client]['state'] && $client_list[$client]['nick'] != ""){
			socket_write($client, trim($buf).chr(0));
		}
		}
	}
	
	function who($allclient, $socket) {
		global $client_list;
		$buf = "";
		$counter = 0;
		foreach($allclient as $client) {
		$buf.=$client_list[$client]['nick'].", ";
		$counter++;
		}
		socket_write($socket, "There are $counter people in this room: $buf".chr(0));
	}
	
	function send_Single($socket, $buf) {
		socket_write($socket, $buf.chr(0));
	}
	
	function shutDown($allclients, $master){
		global $abort;
		$abort = false;
		foreach($allclients as $client){
		echo "$client connection closed\n";
		socket_close($client);
		}
		echo "$master connection closed\n";
		socket_close($master);
		echo "Server shutdown complete\n";
	}
	
	//---- Start Socket creation for PHP 5 Socket Server -------------------------------------
	
	if (($master = socket_create(AF_INET, SOCK_STREAM, SOL_TCP)) < 0) {
		echo "socket_create() failed, reason: " . socket_strerror($master) . "\n";
	}else{
		echo "$master socket created\n";
	}
	
	socket_set_option($master, SOL_SOCKET,SO_REUSEADDR, 1);
	
	
	if (($ret = socket_bind($master, $address, $port)) < 0) {
		echo "socket_bind() failed, reason: " . socket_strerror($ret) . "\n";
	}else{
		echo "$ret socket bound to $address:$port\n";
	}
	
	
	if (($ret = socket_listen($master, 5)) < 0) {
		echo "socket_listen() failed, reason: " . socket_strerror($ret) . "\n";
	}else{
		echo "$ret listening…\n";
	}
	
	
	
	$read_sockets = array($master);
	$client_list = array($master);
	$abort = true;
	$policy_file =
		'<'.'?xml version="1.0" encoding="UTF-8"?'.'>'.
		'<cross-domain-policy xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://www.adobe.com/xml/schemas/PolicyFileSocket.xsd">'.
			'<allow-access-from domain="*" to-ports="*" secure="false" />'.
			'<site-control permitted-cross-domain-policies="master-only" />'.
		'</cross-domain-policy>';
		
	//---- Create Persistent Loop to continuously handle incoming socket messages ---------------------
	while ($abort) {
		$changed_sockets = $read_sockets;
		
		$num_changed_sockets = socket_select($changed_sockets, $write = NULL, $except = NULL, NULL);
		
		foreach($changed_sockets as $socket) {
			
		if ($socket == $master) {
			
			if (($client = socket_accept($master)) < 0) {
			echo "socket_accept() failed: reason: " . socket_strerror($msgsock) . "\n";
			continue;
			} else {
		echo "[connection]:$client\n";
			array_push($read_sockets, $client);
		$client_list[$client]['state'] = false;
		$client_list[$client]['nick'] = "";
		send_Single($client, $policy_file);
		send_Single($client, "<b>Enter a nickname:<b>");
			}
		} else {
			
			$bytes = socket_recv($socket, $buffer, 2048, 0);
			
			if ($bytes == 0) {
		$nick = $client_list[$socket]['nick'];
			$iindex = array_search($socket, $client_list);
			unset($client_list[$iindex]);
			$index = array_search($socket, $read_sockets);
			unset($read_sockets[$index]);
			$allclients = $read_sockets;
			array_shift($allclients);
		if($client_list[$socket]['nick'] != "" && $client_list[$socket]['nick'] != "<policy-file-request/>"){
			echo "[connection-terminated]:$socket\n";
				send_Message($allclients, "$nick has left the room");
		}
			socket_close($socket);
			}else{
		if($bytes){
			if($client_list[$socket]['state'] === false){
			$tempBuf = trim($buffer);
			$testCase = false;
			foreach($read_sockets as $clients){
				if ($client_list[$clients]['nick'] == $tempBuf) {
				$testCase = true;
				send_Single($socket, "Sorry, \"$tempBuf\" is already in use!");
				send_Single($socket, "Please choose another nickname:");
				break;
				}
			}
			if(!$testCase){
				$client_list[$socket]['nick'] = $tempBuf;
				echo "$tempBuf assigned to $socket\n";
				send_Single($socket, "Hello $tempBuf!	Welcome to the game!");
					$allclients = $read_sockets;
					array_shift($allclients);
				who($allclients, $socket);
				if($client_list[$socket]['nick'] != "" && $tempBuf != "<policy-file-request/>"){
					send_Message($allclients, $client_list[$socket]['nick']." has entered the game.");
				}
				$client_list[$socket]['state'] = true;
			}
			}else{
				$allclients = $read_sockets;
				array_shift($allclients);
			if(trim($buffer) == "shut-down-server"){
				shutDown($allclients, $master);
			}else{
				if(trim($buffer) == "/who"){
				who($allclients, $socket);
				}else{
					send_Message($allclients, $client_list[$socket]['nick']." wrote: ".$buffer);
				}
			}
			}
		}
			}
		}
		}
	}
	
	?>

	<?php
	// PHP SOCKET SERVER
	error_reporting(E_ERROR);
	// Configuration variables
	$host = "127.0.0.1";
	$port = 4041;
	$max = 20;
	$client = array();
	
	// No timeouts, flush content immediatly
	set_time_limit(0);
	ob_implicit_flush();
	
	// Server functions
	function rLog($msg){
				$msg = "[".date('Y-m-d H:i:s')."] ".$msg;
				print($msg."\n");
				
	}
	// Create socket
	$sock = socket_create(AF_INET,SOCK_STREAM,0) or die("[".date('Y-m-d H:i:s')."] Could not create socket\n");
	// Bind to socket
	socket_bind($sock,$host,$port) or die("[".date('Y-m-d H:i:s')."] Could not bind to socket\n");
	// Start listening
	socket_listen($sock) or die("[".date('Y-m-d H:i:s')."] Could not set up socket listener\n");
	
	rLog("Server started at ".$host.":".$port);
	// Server loop
	while(true){
				socket_set_block($sock);
				// Setup clients listen socket for reading
				$read[0] = $sock;
				for($i = 0;$i<$max;$i++){
								if($client[$i]['sock'] != null)
											$read[$i+1] = $client[$i]['sock'];
				}
				// Set up a blocking call to socket_select()
				$ready = socket_select($read,$write = NULL, $except = NULL, $tv_sec = NULL);
				// If a new connection is being made add it to the clients array
				if(in_array($sock,$read)){
								for($i = 0;$i<$max;$i++){
											if($client[$i]['sock']==null){
														if(($client[$i]['sock'] = socket_accept($sock))<0){
																	rLog("socket_accept() failed: ".socket_strerror($client[$i]['sock']));
														}else{
																	rLog("Client #".$i." connected");
														}
														break;
											}elseif($i == $max - 1){
														rLog("Too many clients");
											}
								}
								if(--$ready <= 0)
								continue;
				}
				for($i=0;$i<$max;$i++){
								if(in_array($client[$i]['sock'],$read)){
											$input = socket_read($client[$i]['sock'],1024);
											if($input==null){
														unset($client[$i]);
											}
											$n = trim($input);
											$com = split(" ",$n);
											if($n=="EXIT"){
														if($client[$i]['sock']!=null){
																	// Disconnect requested
																	socket_close($client[$i]['sock']);
																	unset($client[$i]['sock']);
																	rLog("Disconnected(2) client #".$i);
																	for($p=0;$p<count($client);$p++){
																					socket_write($client[$p]['sock'],"DISC ".$i.chr(0));
																	}
																	if($i == $adm){
																					$adm = -1;
																	}
														}
											}elseif($n=="TERM"){
														// Server termination requested
														socket_close($sock);
														rLog("Terminated server (requested by client #".$i.")");
														exit();
											}elseif($input){
														// Strip whitespaces and write back to user
														// Respond to commands
														/*$output = ereg_replace("[ \t\n\r]","",$input).chr(0);
														socket_write($client[$i]['sock'],$output);*/
														if($n=="PING"){
																	socket_write($client[$i]['sock'],"PONG".chr(0));
														}
														if($n=="<policy-file-request/>"){
																	rLog("Client #".$i." requested a policy file…");
																	$cdmp="<?xml version=\"1.0\" encoding=\"UTF-8\"?><cross-domain-policy xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xsi:noNamespaceSchemaLocation=\"http://www.adobe.com/xml/schemas/PolicyFileSocket.xsd\"><allow-access-from domain=\"*\" to-ports=\"*\" secure=\"false\" /><site-control permitted-cross-domain-policies=\"master-only\" /></cross-domain-policy>";
																	socket_write($client[$i]['sock'],$cdmp.chr(0));
																	socket_close($client[$i]['sock']);
																	unset($client[$i]);
																	$cdmp="";
														}
											}
								}else{
											//if($client[$i]['sock']!=null){
														// Close the socket
														//socket_close($client[$i]['sock']);
														//unset($client[$i]);
														//rLog("Disconnected(1) client #".$i);
											//}
								}
				}
	}
	// Close the master sockets
	socket_close($sock);
	?>

- http://www.functionblog.com/?p=67=1

### Threading

Therading is impossible in Flash. But:

- [Idea] Using `LocalConnection` between mutliple Flash embedded in same page ? (depend browser, but maybe all instance are in same os thread)
- Using asynchronous `ShaderJob`s (fp10)
- Use pseudo threading with small chunk of function

Implementation of pseudo threading:

- General relativity's [`GreenThread`](http://blog.generalrelativity.org/?p=29)
- Senocular's [tutorial](http://www.senocular.com/flash/tutorials/asyncoperations/)
 
	package
	{
		import flash.display.DisplayObjectContainer;
		import flash.events.Event;
		import flash.events.EventDispatcher;
		import flash.events.KeyboardEvent;
		import flash.events.MouseEvent;
		import flash.utils.getTimer;
		import flash.display.Sprite;
		
		public class PseudoThread extends EventDispatcher
		{
			public function PseudoThread(parent:Sprite, threadFunction:Function, threadObject:Object):void
			{
				fn = threadFunction;
				obj = threadObject;
				
				// add high priority listener for ENTER_FRAME
				parent.stage.addEventListener(Event.ENTER_FRAME, enterFrameHandler, false, 100);
				parent.stage.addEventListener(MouseEvent.MOUSE_MOVE, mouseMoveHandler);
				parent.stage.addEventListener(KeyboardEvent.KEY_DOWN, keyDownHandler);
				
				thread = new Sprite();
				parent.addChild(thread);
				thread.addEventListener(Event.RENDER, renderHandler);
			}
			
			// number of milliseconds we think it takes to render the screen
			public var RENDER_DEDUCTION:int = 10;
			
			private var fn:Function;
			private var obj:Object;
			private var thread:Sprite;
			private var start:Number;
			private var due:Number;
			
			private var mouseEvent:Boolean;
			private var keyEvent:Boolean;
			
			private function enterFrameHandler(event:Event):void
			{
				start = getTimer();
				var fr:Number = Math.floor(1000 / thread.stage.frameRate);
				due = start + fr;
				
				thread.stage.invalidate();
				thread.graphics.clear();
				thread.graphics.moveTo(0, 0);
				thread.graphics.lineTo(0, 0); 
			}
			
			private function renderHandler(event:Event):void
			{
				if (mouseEvent || keyEvent)
				due -= RENDER_DEDUCTION;
				
				while (getTimer() < due)
				{
					if (!fn(obj))
					{
						if (!thread.parent)
						return;
						
						thread.stage.removeEventListener(Event.ENTER_FRAME, enterFrameHandler);
						thread.stage.removeEventListener(MouseEvent.MOUSE_MOVE, mouseMoveHandler);
						thread.stage.removeEventListener(KeyboardEvent.KEY_DOWN, keyDownHandler);
						thread.parent.removeChild(thread);
						thread.removeEventListener(Event.RENDER, renderHandler);
						dispatchEvent(new Event("threadComplete"));
					}
				}
				
				mouseEvent = false;
				keyEvent = false;
			}
			
			private function mouseMoveHandler(event:Event):void
			{
				mouseEvent = true;
			}
			
			private function keyDownHandler(event:Event):void
			{
				keyEvent = true;
			}
		} 
	}

- http://blogs.adobe.com/aharui/2008/01/threads_in_actionscript_3.html

### Progressive SWF loading ("use later" code/assets or embedded preloader)

	//...
	public class MyClass1 extends MovieClip
	//...

	//...
	[Frame(factoryClass="MyClass1")]
	public class MyClass2
	//...

	//...
	[Frame(factoryClass="MyClass2")]
	public class MyClass3
	//...

Compile a SWF following:

- Frame 1
	- Include `MyClass1`
	- Create an instance of `MyClass1` and use it as root class
- Frame 2
	- Include `MyClass2`
- Frame 3
	- Include `MyClass3`

- You must to compile `MyClass3` as main class
- `MyClass1` must extends MovieClip (you can also extends Sprite, but some things will not work)
- You can check loading progression with loaderInfo's progress event
- You can check also frame loading (framesLoaded/totalFrames)
- To ask FlashPlayer to parse a frame (when is loaded), you must to play it (`with nextFrame()` or `gotoAndStop()`)
- `MyClass2` and `MyClass3` could not extends DisplayObject and are not executed
- If you want to use SWF metadata tag, you must use it in main class (which use to compile application), here `MyClass3`

If you want to add an extra class in a specific frame use `[Frame(extraClass="MyAsset")]`

Example (frames):

1. Loading
2. Libraries (classes …)
3. Main
 
	package {
		import flash.display.Sprite;
	
		//This tells the compiler to create a new frame this main class
		[Frame(factoryClass="PreloadedMain")]
	
		public class PreloadedMain extends Sprite
		{
			public function PreloadedMain():void
			{
				
			}
		}
	}

	package
	{
		
		import flash.display.DisplayObject;
		import flash.display.MovieClip;
		import flash.events.Event;
		import flash.utils.getDefinitionByName;
	
		public class Main extends MovieClip
		{
			public function Main():void
			{
				//Stop the timeline
				stop();
				//Set an eventlistener for the animation
				this.addEventListener(Event.ENTER_FRAME, this.enterFrameListener);
			}
			//Draw a bar, or your preloader of choice
			public function enterFrameListener(event:Event):void
			{
				if(this.framesLoaded == this.totalFrames)
				{
					this.removeEventListener(Event.ENTER_FRAME, this.enterFrameListener);
					//Move to the next frame when we're done
					this.nextFrame();
					//And initialize our main class
					//Get our main class
					var mainClass:Class = Class(getDefinitionByName("PreloadedMain"));
					if(mainClass)
					{
						//And instantiate it
						var app:Object = new mainClass();
						//finally we add it to the DisplayList
						this.addChild(app as DisplayObject);
					}
				}
			}
		}
	}

- http://www.dreaminginflash.com/2007/11/13/actionscript-3-preloader/
- http://www.bit-101.com/blog/?p=946

## Use MXML without Flex framework

	<d:Sprite xmlns:mx="http://www.adobe.com/2006/mxml" xmlns:d="flash.display.*">
		<mx:Metadata>
			[SWF(width="900", height="480", backgroundColor="#ffffff")]
		</mx:Metadata>
		<mx:Script>
			<![CDATA[
			public function sayHi():void
			{
				trace("hello world");
			}
			]]>
		</mx:Script>
	</d:Sprite>
	
	<w:Element xmlns:mx="http://www.adobe.com/2006/mxml" xmlns:d="flash.display.*" xmlns:t="flash.text.*" xmlns:w="*">
		<d:Shape />
		<w:Element>
			<t:TextField text="Test" />
		</w:Element>
	</w:Element>

	package
	{
		import flash.display.DisplayObject;
		import flash.display.Sprite;
		
		[DefaultProperty("children")]
		public class Element extends Sprite
		{
			private var _children:Vector.<DisplayObject> = new Vector.<DisplayObject>();
			/**
			* Array of DisplayObject instances to be added as children
			*/
			public function get children():Vector.<DisplayObject>
			{
				return _children;
			}
			
			public function set children( value:Vector.<DisplayObject> ):void
			{
				if ( _children != value )
				{
					_children = value;
					for each(var child:DisplayObject in value)
						addChild(child);
				}
			}
		}
	}

Using `[Bindable]` & `{}`:

- https://stackoverflow.com/questions/320499/how-does-binding-in-actionscript-work
- https://stackoverflow.com/questions/1561410/flex-binding-to-an-mxml-esque-binding-string-in-action-script
- http://code.google.com/p/flit/

----

Array implementation (http://wiki.ecmascript.org/doku.php?id=discussion:builtin_classes) can be found in Tamarin

	/* ***** BEGIN LICENSE BLOCK *****
	 * Version: MPL 1.1/GPL 2.0/LGPL 2.1
	 *
	 * The contents of this file are subject to the Mozilla Public License Version
	 * 1.1 (the "License"); you may not use this file except in compliance with
	 * the License. You may obtain a copy of the License at
	 * http://www.mozilla.org/MPL/
	 *
	 * Software distributed under the License is distributed on an "AS IS" basis,
	 * WITHOUT WARRANTY OF ANY KIND, either express or implied. See the License
	 * for the specific language governing rights and limitations under the
	 * License.
	 *
	 * The Original Code is [Open Source Virtual Machine.].
	 *
	 * The Initial Developer of the Original Code is
	 * Adobe System Incorporated.
	 * Portions created by the Initial Developer are Copyright (C) 2004-2006
	 * the Initial Developer. All Rights Reserved.
	 *
	 * Contributor(s):
	 - Adobe AS3 Team
	 *
	 * Alternatively, the contents of this file may be used under the terms of
	 * either the GNU General Public License Version 2 or later (the "GPL"), or
	 * the GNU Lesser General Public License Version 2.1 or later (the "LGPL"),
	 * in which case the provisions of the GPL or the LGPL are applicable instead
	 * of those above. If you wish to allow use of your version of this file only
	 * under the terms of either the GPL or the LGPL, and not to allow others to
	 * use your version of this file under the terms of the MPL, indicate your
	 * decision by deleting the provisions above and replace them with the notice
	 * and other provisions required by the GPL or the LGPL. If you do not delete
	 * the provisions above, a recipient may use your version of this file under
	 * the terms of any one of the MPL, the GPL or the LGPL.
	 *
	 * ***** END LICENSE BLOCK ***** */
	 
	 
	package
	{
		public dynamic class Array extends Object
		{
			// option flags for sort and sortOn
			public static const CASEINSENSITIVE:uint = 1;
			public static const DESCENDING:uint = 2;
			public static const UNIQUESORT:uint = 4;
			public static const RETURNINDEXEDARRAY:uint = 8;
			public static const NUMERIC:uint = 16;	
			
			// E262 {DontEnum, DontDelete}
			public native function get length():uint
			public native function set length(newLength:uint)
		
			// Array.length = 1 per ES3
			public static const length:int = 1
		
			// ECMA 15.4.2.2
			public function Array(...args)
			{
				var n:uint = args.length
				if (n == 1 && (args[0] is Number))
				{
					var dlen:Number = args[0];
					var ulen:uint = dlen
					if (ulen != dlen)
						Error.throwError( RangeError, 1005 /*kArrayIndexNotIntegerError*/, dlen );
					length = ulen;
				}
				else
				{
					length = n
					for (var i:uint=0; i < n; i++)
						this[i] = args[i]
				}
			}
		
			/**
			15.4.4.5 Array.prototype.join (separator)
			The elements of the array are converted to strings, and these strings are then concatenated, separated by
			occurrences of the separator. If no separator is provided, a single comma is used as the separator.
			The join method takes one argument, separator, and performs the following steps:
			1. Call the [[Get]] method of this object with argument "length".
			2. Call ToUint32(Result(1)).
			3. If separator is undefined, let separator be the single-character string ",".
			4. Call ToString(separator).
			5. If Result(2) is zero, return the empty string.
			6. Call the [[Get]] method of this object with argument "0".
			7. If Result(6) is undefined or null, use the empty string; otherwise, call ToString(Result(6)).
			8. Let R be Result(7).
			9. Let k be 1.
			10. If k equals Result(2), return R.
			11. Let S be a string value produced by concatenating R and Result(4).
			12. Call the [[Get]] method of this object with argument ToString(k).
			13. If Result(12) is undefined or null, use the empty string; otherwise, call ToString(Result(12)).
			14. Let R be a string value produced by concatenating S and Result(13).
			15. Increase k by 1.
			16. Go to step 10.
			*/
			
			private static function _join(o, sep):String
			{
				var s:String = (sep === undefined) ? "," : String(sep)
				var out:String = ""
				for (var i:uint = 0, n:uint=uint(o.length); i < n; i++)
				{
					var x = o[i]
					if (x != null)
						out += x
					if (i+1 < n)
						out += s
				}
				return out
			}
			AS3 function join(sep=void 0):String
			{
				return _join(this, sep)
			}
			prototype.join = function(sep=void 0):String
			{
				return _join(this, sep)
			}
			
			private static native function _pop(o)
			AS3 native function pop()
			prototype.pop = function()
			{
				return _pop(this)
			}
			
			/**
			15.4.4.2 Array.prototype.toString ( )
			The result of calling this function is the same as if the built-in join method were invoked for this object with no
			argument.
			The toString function is not generic; it throws a TypeError exception if its this value is not an Array object.
			Therefore, it cannot be transferred to other kinds of objects for use as a method.
			*/
		
			prototype.toString = function():String
			{
				var a:Array = this  // TypeError if not compatible
				return _join(a, ",");
			}
			
			/**
			15.4.4.3 Array.prototype.toLocaleString ( )
			The elements of the array are converted to strings using their toLocaleString methods, and these strings are
			then concatenated, separated by occurrences of a separator string that has been derived in an implementationdefined
			locale-specific way. The result of calling this function is intended to be analogous to the result of
			toString, except that the result of this function is intended to be locale-specific.
			The result is calculated as follows:
			1. Call the [[Get]] method of this object with argument "length".
			2. Call ToUint32(Result(1)).
			3. Let separator be the list-separator string appropriate for the host environment’s current locale (this is derived in
			an implementation-defined way).
			4. Call ToString(separator).
			5. If Result(2) is zero, return the empty string.
			6. Call the [[Get]] method of this object with argument "0".
			7. If Result(6) is undefined or null, use the empty string; otherwise, call ToObject(Result(6)).toLocaleString().
			8. Let R be Result(7).
			9. Let k be 1.
			10. If k equals Result(2), return R.
			11. Let S be a string value produced by concatenating R and Result(4).
			12. Call the [[Get]] method of this object with argument ToString(k).
			13. If Result(12) is undefined or null, use the empty string; otherwise, call ToObject(Result(12)).toLocaleString().
			14. Let R be a string value produced by concatenating S and Result(13).
			15. Increase k by 1.
			16. Go to step 10.
			The toLocaleString function is not generic; it throws a TypeError exception if its this value is not an Array
			object. Therefore, it cannot be transferred to other kinds of objects for use as a method.
			*/
			
			prototype.toLocaleString = function():String
			{
				var a:Array = this // TypeError if not compatible
				
				var out:String = ""
				for (var i:uint = 0, n:uint=a.length; i < n; i++)
				{
					var x = a[i]
					if (x != null)
						out += x.toLocaleString()
					if (i+1 < n)
						out += ","
				}
				return out
			}
			
			/**
			When the push method is called with zero or more arguments item1, item2, etc., the following steps are taken:
			1. Call the [[Get]] method of this object with argument "length".
			2. Let n be the result of calling ToUint32(Result(1)).
			3. Get the next argument in the argument list; if there are no more arguments, go to step 7.
			4. Call the [[Put]] method of this object with arguments ToString(n) and Result(3).
			5. Increase n by 1.
			6. Go to step 3.
			7. Call the [[Put]] method of this object with arguments "length" and n.
			8. Return n.
			The length property of the push method is 1.
			NOTE The push function is intentionally generic; it does not require that its this value be an Array object. Therefore it can be
			transferred to other kinds of objects for use as a method. Whether the push function can be applied successfully to a host object
			is implementation-dependent.
			*/
			AS3 native function push(...args):uint
			prototype.push = function(...args):uint
			{
				var n:uint = uint(this.length)
				for (var i:uint=0, argc:uint=args.length; i < argc; i++)
					this[n++] = args[i]
				this.length = n
				return n
			}
			
			private static native function _reverse(o)
			AS3 function reverse():Array
			{
				return _reverse(this)  // return will cast to Array
			}
			prototype.reverse = function()
			{
				return _reverse(this)
			}
			
			private static native function _concat(o, args:Array):Array
			AS3 function concat(...args):Array
			{
				return _concat(this, args)
			}
			prototype.concat = function(...args):Array
			{
				return _concat(this, args)
			}
			
			private static native function _shift(o)
			AS3 function shift()
			{
				return _shift(this)
			}
			prototype.shift = function()
			{
				return _shift(this)
			}
			
			private static native function _slice(o, A:Number, B:Number):Array
			AS3 function slice(A=0, B=0xffffffff):Array
			{
				return _slice(this, Number(A), Number(B))
			}
			prototype.slice = function(A=0, B=0xffffffff):Array
			{
				return _slice(this, Number(A), Number(B))
			}
			
			/**
			15.4.4.13 Array.prototype.unshift ( [ item1 [ , item2 [ , … ] ] ] )
			The arguments are prepended to the start of the array, such that their order within the array is the same as the
			order in which they appear in the argument list.
			When the unshift method is called with zero or more arguments item1, item2, etc., the following steps are taken:
			1. Call the [[Get]] method of this object with argument "length".
			2. Call ToUint32(Result(1)).
			3. Compute the number of arguments.
			4. Let k be Result(2).
			5. If k is zero, go to step 15.
			6. Call ToString(k–1).
			7. Call ToString(k+Result(3)–1).
			8. If this object has a property named by Result(6), go to step 9; but if this object has no property named by
			Result(6), then go to step 12.
			9. Call the [[Get]] method of this object with argument Result(6).
			10. Call the [[Put]] method of this object with arguments Result(7) and Result(9).
			11. Go to step 13.
			12. Call the [[Delete]] method of this object with argument Result(7).
			13. Decrease k by 1.
			14. Go to step 5.
			15. Let k be 0.
			16. Get the next argument in the part of the argument list that starts with item1; if there are no more arguments, go
			to step 21.
			17. Call ToString(k).
			18. Call the [[Put]] method of this object with arguments Result(17) and Result(16).
			19. Increase k by 1.
			20. Go to step 16.
			21. Call the [[Put]] method of this object with arguments "length" and (Result(2)+Result(3)).
			22. Return (Result(2)+Result(3)).
			The length property of the unshift method is 1.
			NOTE The unshift function is intentionally generic; it does not require that its this value be an Array object. Therefore it can
			be transferred to other kinds of objects for use as a method. Whether the unshift function can be applied successfully to a
			host object is implementation-dependent.
			*/
			native AS3 function unshift(...args):uint
			prototype.unshift = function(...args):uint
			{
				var len:uint = uint(this.length)
				var argc:uint = args.length
				var k:uint
				for (k=len; k > 0; )
				{
					k--
					var d:uint = k+argc
					if (k in this)
						this[d] = this[k]
					else
						delete this[d]
				}
				
				for (var i:uint = 0; i < argc; i++)
					this[k++] = args[i]
					
				len += argc
				this.length = len
				return len
			}
			
			private static native function _splice(o, args:Array):Array
			
			// splice with zero args returns undefined. All other cases return Array.
			AS3 function splice(...args)
			{
				if (!args.length)
					return undefined;
					
				return _splice(this, args)
			}
			prototype.splice = function(...args)
			{
				if (!args.length)
					return undefined;
					
				return _splice(this, args)
			}
			
			// sort can return an Array or a Number (unique sort option)
			private static native function _sort(o, args:Array)
			AS3 function sort(...args)
			{
				return _sort (this, args);
			}
			prototype.sort = function(...args)
			{
				return _sort (this, args);
			}
			
			private static native function _sortOn(o, names, options)
			AS3 function sortOn(names, options=0, ...ignored)
			{
				// this is our own addition so we don't have to make names be optional
				return _sortOn(this, names, options);
			}
			prototype.sortOn = function(names, options=0, ...ignored)
			{
				return _sortOn(this, names, options)
			}
			
			// Array extensions that are in Mozilla...
			// http://developer.mozilla.org/en/docs..._Objects:Array
			//
			// These all work on generic objects (array like objects) as well as arrays
			
			private static native function _indexOf (o, searchElement, fromIndex:int):int;
			AS3 function indexOf(searchElement, fromIndex=0):int
			{
				return _indexOf (this, searchElement, int(fromIndex));
			}
			prototype.indexOf = function(searchElement, fromIndex=0):int
			{
				return _indexOf (this, searchElement, int(fromIndex));
			}
			
			private static native function _lastIndexOf (o, searchElement, fromIndex:int=0):int;
			AS3 function lastIndexOf(searchElement, fromIndex=0x7fffffff):int
			{
				return _lastIndexOf (this, searchElement, int(fromIndex));
			}
			prototype.lastIndexOf = function(searchElement, fromIndex=0x7fffffff):int
			{
				return _lastIndexOf (this, searchElement, int(fromIndex));
			}
			
			// Returns true if every element in this array satisfies the provided testing function.
			private static native function _every(o, callback:Function, thisObject):Boolean;
			AS3 function every(callback:Function, thisObject=null):Boolean
			{
				return _every (this, callback, thisObject);
			}
			prototype.every = function(callback:Function, thisObject=null):Boolean
			{
				return _every (this, callback, thisObject);
			}
			
			// Creates a new array with all elements that pass the test implemented by the provided function.
			private static native function _filter(o, callback:Function, thisObject):Array;
			AS3 function filter(callback:Function, thisObject=null):Array
			{
				return _filter (this, callback, thisObject);
			}
			prototype.filter = function(callback:Function, thisObject=null):Array
			{
				return _filter (this, callback, thisObject);
			}
			
			// Calls a function for each element in the array.
			private static native function _forEach(o, callback:Function, thisObject):void;
			AS3 function forEach(callback:Function, thisObject=null):void
			{
				_forEach (this, callback, thisObject);
			}
			prototype.forEach = function(callback:Function, thisObject=null):void
			{
				_forEach (this, callback, thisObject);
			}
			
			// Creates a new array with the results of calling a provided function on every element in this array.
			private native static function _map(o, callback:Function, thisObject):Array;
			AS3 function map(callback:Function, thisObject=null):Array
			{
				return _map (this, callback, thisObject);
			}
			prototype.map = function(callback:Function, thisObject=null):Array
			{
				return _map (this, callback, thisObject);
			}
		
			// Returns true if at least one element in this array satisfies the provided testing function.
			private static native function _some(o, callback:Function, thisObject):Boolean;
			AS3 function some(callback:Function, thisObject=null):Boolean
			{
				return _some (this, callback, thisObject);
			}
			prototype.some = function(callback:Function, thisObject=null):Boolean
			{
				return _some (this, callback, thisObject);
			}
			
			_dontEnumPrototype(prototype);
		}
	}

## Internals

Sound use URLStream? (error #2029)

	flash.external::ExternalInterface$/_callIn


`public::trace`

`ApplicationDomain.currentDomain.getDefinition("trace") as Function`

- http://hg.mozilla.org/tamarin-central/file/e774dfe22b39/extensions/Trace.as

right now I can use it by default

	import flash.trace.Trace
	Trace.setLevel( Trace.METHODS_AND_LINES_WITH_ARGS, Trace.OFF );

or use my own traceListener function

	import flash.trace.Trace
	
	public function traceListener(line:String, index:int, method:Sring, args:String):void
	{
		trace("@" + index + " - " + line);
		trace(method + "(" + args + ")");
	}

## Equality

	  			null 	false	0		""		NaN
	------------------------------------------------
	isNaN()		-		-		-		-		x
	== ""		-		x	 	x	  	x	 	-	
	=== ""		-		-		-		x	 	-	 
	== null		x	 	-		-		-		-		  	  	  	 
	=== null	x		-		-		-		-	
	== 0		-		x	  	x	  	x	 	-	
	=== 0		-		-		x	  	-		-	
	== false	-		x	  	x	  	x	  	-	 
	=== false	-		x		-		-		-	
	is Number	-		-		x	 	-		x	 
	is String	-		-		-		x	  	-	 
	is Boolean	-		x		-		-		-		  	 
	is Object	-		x	  	x	  	x	  	x	 

Notice that NaN is actually a Number and an Object, that 0 == "" == false and that false is actually an Object

## Accessibility

- [WebAIM: Creating Accessible Flash Content](http://webaim.org/techniques/flash/)
- Use `flash.display.DisplayObject.accessibilityProperties` and `flash.accessibility.*`
- [Flash et l’accessibilité : halte à l’hypocrisie | FredCavazza.net](https://fredcavazza.net/2005/06/24/flash-et-l-accessibilite-halte-a-l-hypocrisie/)
- [Text equivalents](http://www.adobe.com/accessibility/products/flash/text.html#accessible-elements) - Accessible movie elements
- [Making user interfaces more accessible | Adobe Developer Connection \[ADC\]](https://www.adobe.com/jp/devnet/flash/quickstart/accessible_ui_as3.html)
- [Adobe accessibility](http://www.adobe.com/accessibility.html)