Note: code is also data

**It's impossible to prevent access to data provided to untrusted parties, NEVER!** It's too late.

The reader / browser / VM must be able to read your files and since it has no idea of what encryption you use, you must "load" a encrypted file, and the algorithm of your encrypted file is in the loader. But what do you do with the loader itself then?

- encryption (AES / XOR / ROT…) on the value in memory
- encryption (AES / XOR / ROT…) on the packets
- Encrypted Files (code) in conjunction with super high code obfuscation of preloader.
- isolate code/class definition/context and checking for existing definition
- Memory Hacking Prevention, String & Binary Obfuscation, binary level obfuscation, key encrypting
- use different radix, etc.:

	```
	"A" == "1000001" == "		 	"
	```

	```js
	// ascii string to whitespaces
	"Hello"
		.replace(/./g, function(w){return w.charCodeAt(0).toString(2).padStart(7, "0").replace(/0/g, ' ').replace(/1/g, "	")})
	// whitespaces to ascii string
	"	  	   		  	 			 		  		 		  		 				"
		.replace(/.{7}/g, function(w){return String.fromCharCode(parseInt(w.replace(/ /g, "0").replace(/	/g, "1"), 2))})
	```

	See [javascript - Detect when "Inspect Element" is open - Stack Overflow](https://stackoverflow.com/questions/42193700/detect-when-inspect-element-is-open/42194142#comment71551031_42194142)

```as3
class Test {
	static function main() {
		var ldr:Dynamic = new flash.display.Loader();
		var ba:flash.utils.ByteArray = new flash.utils.ByteArray();
		for (i in Data.data) {
			ba.writeByte(i-1); // secret de-obfuscation algorithm: i - 1
		}
		ldr.loadBytes(ba);
		flash.Lib.current.addChild(ldr);
	}
}
```

## Sanitization

Aka redact sensitive data, edited, censored, censorship, classified, secrecy protection, data anonymization, blacking out, over up tape, data erasure

Sensitive in text document could be recovered if not well removed.

Black or white rectangles:

...can be recovered if short parts missing.
![DW19QBdWsAAPCJk.jpeg](./Data access and integrity/Prevent and detect violation/DW19QBdWsAAPCJk.jpg)
[Tom 7 on Twitter: "Redaction pro-tip: Most short word will have distinct length in a proportional font like Time New Roman. I think it' pretty clear, but decide for yourself...(Thi i the Democratic "rebuttal" #memo unclassified today, page 3.)… https://t.co/eQvmiDwL1M"](https://twitter.com/tom7/status/967568358861430785)

Pixelated:

- [beurtschipper/Depix: Recovers passwords from pixelized screenshots](https://github.com/beurtschipper/Depix)
- [Recovering passwords from pixelized screenshots](https://web.archive.org/web/20201210024934/https://www.linkedin.com/pulse/recovering-passwords-from-pixelized-screenshots-sipke-mellema/)
- [Spibblez on Twitter: "I created a tool for recovering passwords from pixelized images: https://t.co/94QugVryjH https://t.co/DEXWDdsqDB" / Twitter](https://twitter.com/spibblez/status/1335638633970348032)

Blur:

- [Deblur](../../Algorithms/Deblur/Deblur.md)

See also:

- [Classified information - Wikipedia](https://en.wikipedia.org/wiki/Classified_information)
- [Sanitization (classified information) - Wikipedia](https://en.wikipedia.org/wiki/Sanitization_%28classified_information%29)
- [Data anonymization - Wikipedia](https://en.wikipedia.org/wiki/Data_anonymization)

## Steganography

See also [Alternative data storage](../../Data%20access%20and%20integrity.md#alternative-data-storage)

Hide data in data or metadata in a carrier format (image, video, etc.)

- append data at the end of file (or the begin, for format that support it)
	- easy detectable, file size
- hiding data in junk field
	- can be easily detectable for dedicated comment fields (or metadata)
	- add use larger fields (exemple: use 16bits palette instead of 8bits, give extra data)
- hidding data in LSB's (Least significant bit), minor offset values
	or Selected Least Significant Bit, LSB matching, etc.
	- doesn't impact file size

	- [Intensity Adaptive LSB Method Applying a Revised Matching - pxc3888468.pdf](http://research.ijcaonline.org/volume70/number27/pxc3888468.pdf)
- palette manipulation
	Reduce colors and duplocate palette entries, allow to create an other image by swapting palette
- encrypt before hide (reduce visual detection of LSB)
- spread hidden data over all bytes, not only in first bytes. Use a noise function to put interval between hidden data (Frequency space manipulation).
- don't hide in repeated data (image without enought contrasts, etc.)

- [stegosploit_pocgtfo8_submission](http://stegosploit.info/)
- SVG is a vector format, this allow to draw elements or vectorized texts in very small size to hide in in the image
- Corrumpt deliberately your files. Only you can restore it
	- [ImpulseAdventure - Fix Corrupt JPEG Photos!](http://www.impulseadventure.com/photo/fix-corrupt-jpeg-photo.html)
- Use unused colors in an image palette to encore data
	Limited to few bytes, max 256 colors = store data potential 765 Bytes max (255 * 24 bits)
- Recive C&C instructions by send HTTP request with absolute URI `GET http://example.com` to an IP address (which not related to the requested domain). Can send data by faking upload of a fake JPEG (only headers). [Dimnie: Hiding in Plain Sight](http://researchcenter.paloaltonetworks.com/2017/03/unit42-dimnie-hiding-plain-sight/)
	-> fake proxy recieve the HTTP request, response with a fake image contains instructions
	act as if it's was a regular HTTP traffic
- Store image / audio data in an audio / image format (lossy or lossless)
	Lossy can destroy too much information. Because audio and image/video codecs are adpated to human senses limitation ([auditory masking](https://en.wikipedia.org/wiki/Auditory_masking), chroma reduction: eye is less sensitive to fine color details than to fine brightness details, etc.)

	- [MP3 for Image Compression (2006) | Hacker News](https://news.ycombinator.com/item?id=14133221)
	- [Avian’s Blog: Lossy compression](https://www.tablix.org/~avian/blog/archives/2006/01/lossy_compression/)

	```sh
	sox mo.wav -e unsigned -b 8 -c 1 -r 48k mo.raw
	bytes=`stat -f %z mo.raw`
	width=`echo sqrt\($bytes\) | bc`
	square_bytes=`echo $width \* $width | bc`
	dd if=mo.raw of=mo_square.raw bs=$square_bytes count=1
	gm convert -depth 8 -size ${width}x${width} gray:mo_square.raw -quality 50 mo_square.jpg
	gm convert mo_square.jpg gray:mo_square_jpg.raw
	sox -e unsigned -b 8 -c 1 -r 48k -t raw mo_square_jpg.raw mo_jpg.wav
	```

- [Windowlicker — Wikipedia](https://en.wikipedia.org/wiki/Windowlicker)
- [wbStego Steganography Tool](http://wbstego.wbailer.com/)
- [Steganography — Wikipedia](https://en.wikipedia.org/wiki/Steganography)
- [Steghide](http://steghide.sourceforge.net/) - steganography program that hide data in JPEG, BMP, WAV and AU files
- [nullcon 2010 - Steganography & Stegananalysis: A Technical & Psycholo…](https://www.slideshare.net/null0x00/nullcon-2010-steganography-stegananalysis-a-technical-psychological-perspective)
- [» Secure Printing «](https://engineering.purdue.edu/~prints/publications.shtml) - Fingerprint / watermarks of printed or scanned documents
- [albinoloverats ~ stegfs](https://albinoloverats.net/projects/stegfs) - steganographic file system (use FUSE)
- [StegoShare — Wikipedia](https://en.wikipedia.org/wiki/StegoShare#Use_in_the_file_sharing_networks) - Use in the anonymous file sharing networks to transmit data
- [OpenPuff - Steganography & Watermarking](http://embeddedsw.net/OpenPuff_Steganography_Home.html) - steganography tool. See [OpenPuff — Wikipedia](https://en.wikipedia.org/wiki/OpenPuff)
- [ZEDZ.NET: purveyors of crypto since 1994.](http://zedz.net/) ftp://ftp.zedz.net/pub/security/steganography/ zedz.net/wiretapped.net Stenography examples (local copy in "zedz.net steganographic software")
- [owencm/js-steg: Javascript JPEG steganography library. Includes JS JPEG encoder and decoder with coefficient access helper functions.](https://github.com/owencm/js-steg)
- [Punk Ode: Hiding Shellcode in Plain Sight](https://www.blackhat.com/presentations/bh-usa-06/BH-US-06-Sutton.pdf)

### Hide data in text

In document, user's comment, chat message, source code / script, source code's comment, source code variable name or value (strings), etc.

- using white spaces, lookalike chars substitution (confusable homoglyphs), diacritic, capitalization, unicode escape sequences and the differents way to encode it (ex. for HTML: `&#233;` vs `&#x00E9;` vs `&eacute;` vs `é`, etc. vs non escaped chars), surrogate pairs, etc.
	- https://github.com/reinderien/mimic and https://github.com/reinderien/mimic/wiki/Character-Set
	- [A tool can compress JavaScript code to any ascii image and still run normally](https://github.com/xinyu198736/js2image)
	- [Off-side rule — Wikipedia](https://en.wikipedia.org/wiki/Off-side_rule#Off-side_rule_languages)
	- [Whitespace (programming language) — Wikipedia](https://en.wikipedia.org/wiki/Whitespace_%28programming_language%29)
	- [Voidmaker - JSFiddle](https://jsfiddle.net/Lcjo35h4/1/)
	- [Homoglyph — Wikipedia](https://en.wikipedia.org/wiki/Homoglyph)
	- Ruby annotation are usally not visible
		> They tend not to have any rendering in fonts, since they’re control characters, and Unicode actually recommends they not be exposed directly to users at all, so there are no rules for how to actually display them

		`<ruby><rb>日本語</rb><rp>（</rp><rt>にほんご</rt><rp>）</rp></ruby>` `[U+FFF9]日本語[U+FFFA]にほんご[U+FFFB]`
	- Unicode decomposition `"한글" !== "한글"` `"ㅎㅏㄴ ㄱㅡㄹ"`
	- http://www.unicode.org/Public/security/latest/confusables.txt see [UTS #39: Unicode Security Mechanisms](http://www.unicode.org/reports/tr39/#confusables)
	- [vhf/confusable_homoglyphs: ϲοｎｆｕѕаｂｌе＿һοｍоɡｌｙｐｈｓ](https://github.com/vhf/confusable_homoglyphs)
	- replace some Latin characters with their Cyrillic doppelgänger ("aceijopsxy" -> "асеіјорѕху"), or Roman Numerals ("ⅰⅴⅹⅼⅽⅾⅿ" -> "ivxlcdm"):
		- [(1) Martin Kleppe on Twitter: "Evil note: In JavaScript you can replace some Latin characters with their Cyrillic doppelgänger ("aceijopsxy" =&gt; "асеіјорѕху") to use reserved words as your variable names such as: var vаr = function functіon(functіon){ cаtch = "me"; іf \[you = "can"\]; } vаr (breаk = true);" / Twitter](https://twitter.com/aemkei/status/1146884713371578369?s=12)

		```js
		var vаr = function functіon(functіon){
		  cаtch = "me";
		  іf [you = "can"];
		}

		vаr (breаk = true);
		```

		```js
		dо='',vаr=!dо+dо,breаk=!vаr+dо,cаtch=dо+{},іf=vаr[dо++],ѕwitch=vаr[іn=dо],thiѕ=++іn+dо,cоnst=cаtch[іn+thiѕ],vаr[cоnst+=cаtch[dо]+(vаr.breаk+cаtch)[dо]+breаk[thiѕ]+іf+ѕwitch+vаr[іn]+cоnst+іf+cаtch[dо]+ѕwitch][cоnst](breаk[dо]+breаk[іn]+vаr[thiѕ]+ѕwitch+іf+"(dо)")()
		```

		```js
		[breаk,caѕe,cаtch,contіnue,dеbugger,defаult,dеlete,dо,elѕe,fіnally,fоr,functіon,іf,іn,inѕtanceof,nеw,rеturn,ѕwitch,thiѕ,thrоw,trу,typeоf,vаr,voіd,whіle,wіth] = "cyrillic doppelgänger of reserved words";
		```

		```js
		var сonst = "W";
		let vаr = "T";
		const lеt = "F";
		сonst + vаr + lеt // WTF
		```

		```js
		([cοnst,cοnst,сοnst,сοnst,сοnst,сοnst]=[]+{},[сonst,cоnst,conѕt,соnst,сonѕt,сonѕt,cоnѕt,соnѕt,сοnѕt,сοnѕt,cοnѕt]=[!!cοnst]+!cοnst+cοnst.cοnst)[сοnst+=cοnst+cοnѕt+соnѕt+сonst+cоnst+conѕt+сοnst+сonst+cοnst+cоnst][сοnst](сonѕt+cоnѕt+соnst+cоnst+сonst+'("const")')()
		```
- Zero width chars:

	```html
	<!-- [SmallestJS](http://schierlm.users.sourceforge.net/smallestjs.html) -->
	<!-- Use zero-width (invisible as text) chars: U+200D, U+FEFF, U+200C, U+200B, made visible here with unicode escape sequence -->
	<meta charset="utf-8"><script>q="\ufeff‌‍​\ufeff‌​​\ufeff‌​‌\ufeff​‍​\ufeff​\ufeff‍\ufeff​‍‌\ufeff​\ufeff\ufeff\ufeff‌‍​\ufeff​\ufeff‍\ufeff‌​​\ufeff​‍‌\ufeff‌‍\ufeff\ufeff‌​‍\ufeff‌\ufeff\ufeff\ufeff​‍‌\ufeff​\ufeff‍‍‌‌‍‍‌‍‌\ufeff‌‌‍\ufeff‌\ufeff\ufeff\ufeff‌​‍\ufeff‌​‍\ufeff‌​​‍‌‍‌‍‌‌\ufeff";l=q.length;s="substring";for(i=0;i<l;i+=4)
	{w="";for(j=0;j<4;j++){w+=(q.charCodeAt(i+j)*5/2)&3};q+=String.fromCharCode(
	parseInt(w,4))};c=q[s](l,l+11);c[c][c](q[s](l+11))(); // by @mihi42</script>
	```
- hide short link ID in Instagram comment: `‍#2hot ma‍ke lovei‍d to ‍her, ‍uupss ‍#Hot ‍#X` gives `2kdhuHX` for `http://bit.ly/` ID.

	```js
	let regexp = /(?:\u200d(?:#|@)?)(\w)/g;
	let match;
	let result = "";
	let str = "asmith2155: ‍#2hot ma‍ke lovei‍d to ‍her, ‍uupss ‍#Hot ‍#X";
	// This string contains Unicode Character 'ZERO WIDTH JOINER' (U+200D)
	// "#" (prepend hashtags) or "@" (prepend a username) characters are used to justify capital letters in the middle of a sentence, without breaking it ability to be recognized as hashtag or username
	while((match = regexp.exec(str)) !== null){
		result += match[1]
	}
	result;// "2kdhuHX" prepend it with http://bit.ly/
	```

	- [Turla’s watering hole campaign: An updated Firefox extension abusing Instagram](https://www.welivesecurity.com/2017/06/06/turlas-watering-hole-campaign-updated-firefox-extension-abusing-instagram/)
	- [You’ll never guess where Russian spies are hiding their control servers | Ars Technica](https://arstechnica.com/security/2017/06/russian-hackers-turn-to-britney-spears-for-help-concealing-espionage-malware/)
- `snow` append whitespaces to the end of lines
- ```` Function`$${atob`YWxlcnQoMSk`}``` /*same as: alert(1)*/ ```` - [Martin Kleppe on Twitter: "Here is a quick explanation: atob`YWxlcnQoMSk=` // decodes to string to: // "alert(1)" `$${"alert(1)"}` // results in the tag components: // \["$", ""\], "alert(1)" Function(\["$", ""\], "alert(1)") // creates an anonymous function // function($,) {alert(1)}" / Twitter](https://twitter.com/aemkei/status/1240399576487600128)

### Hide data by using permissively

It's still valid, but add extra data will be invisible / ingored when read normaly

- HTML is permissive
	- `<div a="b><span></span></div>` eq. `<html><head></head><body></body></html>`
	- `<div a=b"><span></span></div>` eq. `<html><head></head><body><div a="b&quot;"><span></span></div></body></html>`
	- `<div something="else"<span>test</span></div>` eq. `<html><head></head><body><div something="else" <span="">test</div></body></html>` (attributes: `something` and `<span`)

	- [Attribute names - HTML Standard](https://html.spec.whatwg.org/multipage/syntax.html#attributes-2)
	- [Tag omission in text/html - HTML 5.1: 3. Semantics, structure, and APIs of HTML documents](https://www.w3.org/TR/html/dom.html#tag-omission-in-text-html)
	- [8 The HTML syntax — HTML5](https://www.w3.org/TR/html5/syntax.html#tokenization)
	- [void elements](https://www.w3.org/TR/html51/syntax.html#void-elements)
	- [The Actual Browser Problems with Unquoted Attributes | CSS-Tricks](https://css-tricks.com/problems-with-unquoted-attributes/)
	- [Unquoted attribute values in HTML and CSS/JS selectors · Mathias Bynens](https://mathiasbynens.be/notes/unquoted-attribute-values)
	- "A p element’s end tag may be omitted if the p element is immediately followed by an [...]" — [HTML 5.1: 4.4. Grouping content](https://www.w3.org/TR/html/grouping-content.html#the-p-element)
- base64 variant could allow chars outside alphabet (ignored) means you can write text/url with it. [Some decoder ignore only spaces](https://html.spec.whatwg.org/multipage/webappapis.html#atob:space-character) (`atob("Hello world") == "ée£\n+"`)
	- [Stupid certificate tricks | rya.nc](https://rya.nc/cert-tricks.html)
	- [PGP ASCII Art - cem](https://www.cem.me/20150706-pgp-art.html)
- HTTP chunk encoding (browsers) ignore remains chunks after a chunk with zero length
- HTTP Field parameters allow to escape any char in parameter value: `Content-Disposition: application/octet-stream; filename="w\hat th\e\ hel\l is going \on.mp3"` gives "hello"
- `gzip-steg` ftp://ftp.mirrorservice.org/sites/ftp.wiretapped.net/pub/security/steganography/gzip-steg/
	> gzip uses LZ77 which compresses data by storing length/offset pairs that refer back in the uncompressed data stream to previous occurrences of the information being compressed. gzip considers a length of 3 to be the shortest acceptable length. We allow gzip to find the length/offset pairs and then do the following.
	>
	> If the length is at least 5 then we subtract 1 and set bit 0 to the value of the bit that we need to hide. We have now hidden information in the length without pushing it beyond a valid value.  Drawbacks are a slight decrease in compression (very slight) since we have to disallow lengths of 4 and some of our meddling will decrease the actual matched length by 1. The hidden file is totally invisible to the normal operation of gzip, gunzip et al and (if encrypted) will only be visible to those in the know.
- JSON indentation / whitespaces between tokens

### Hide data with optional fields

In metadata, comment, extra fields or unused fields

- PNG `tEXt` chunk (comment)
	See also [chunks `zTXt` and `iTXt`](https://sno.phy.queensu.ca/~phil/exiftool/TagNames/PNG.html#TextualData)

	```bash
	exiftool "-Comment<=/path/to/secret.txt" dummy.png
	exiftool -b -Comment dummy.png > secret.txt
	```

	- PHP contains base64 contains PNG with data encoded in `tEXt` chunk (comment)
		- [When Bad Guys are Pwning Bad Guys... - SANS Internet Storm Center](https://isc.sans.edu/forums/diary/When+Bad+Guys+are+Pwning+Bad+Guys/22410/)
		- [backdoor as stripped from RC-SHELL](https://gist.github.com/anonymous/319ef7124affebec67ebc56bc83cbe87)
- PNG custom chunk
	- [Pozo/punk: Hiding a payload in PNG files with JAVA](https://github.com/Pozo/punk)
	- [Hiding a payload in PNG files with Python](http://blog.brian.jp/python/png/2016/07/07/file-fun-with-pyhon.html)
- gzip stream can optionaly contains additional data and often ignored when not handling files (like HTTP response):
	* extra header (2 Bytes + 256 Bytes max)
	* original filename: N Bytes + 1 Byte (`\0`)
	* creation date: 4 Bytes (POSIX timestamp)
	* comment N Bytes + 1 zero Byte (`\0`)

	See `gzip -N`

	It's also possible to concatenate gzip stream in one `cat file1.gz file2.gz file3.gz > all.gz`. This could be ignored (the reader read only the first part). See [Concatenation](GZip#Concatenation)

	You can also add extra data after gzip stream, some tools/libs ignore them (`gunzip -q`)
- HTTP/1.1 chunk encoding use chunk extension (kind of comment), always ignored https://tools.ietf.org/html/rfc7230#section-4.1.1
- matroska media container can contains additional tags to store fonts, text, image, binary, etc.
- HTTP chunk encoding tailers are often ignored (but visible with the header `Trailer:`)
- HTTP allow unlimited unstandardized headers
- HTTP message using `multipart/*` support multiple resources [subtypes share the same syntax](https://tools.ietf.org/html/rfc2046#section-5.1.1)
- MIME External-Body Subtype: `message/external-body`, in "phantom body"
- JPEG and some videos codecs like H.264 need the number of pixel to be a multiple of 8 or 16 (macroblocks). All this data is encoded, it's clamped to the image size.
	Odd-sized like 1x1 JPEG image will contains 16x16 pixels (or 8x8 pixels)
	That means data could be written in this border area, but never rendered by common JPEG/video librairies. Only if you rewrite the image size before decoding it.
	- [Block splitting](https://en.wikipedia.org/wiki/JPEG#Block_splitting)
	- [Source Coding and Compression](http://iphome.hhi.de/schwarz/assets/pdfs/08_ImageCoding.pdf#page=23)
	- [Comment ajouter une légende invisible à une image JPEG. - YouTube](https://www.youtube.com/watch?v=RuqAV_By7ig)
	- [JPEG effets de bord et sous-échantillonnage chroma - YouTube](https://www.youtube.com/watch?v=V7LvgXqsh60)
- [NTFS Alternate Data Streams: Hiding data in plain sight since 1993 – EventSentry Blog](https://www.eventsentry.com/blog/2008/07/ntfs-alternate-data-streams-hi.html)
- embedded font or image in PDF, HTML, SVG, etc.

- [ExifTool FAQ](https://sno.phy.queensu.ca/~phil/exiftool/faq.html#Q10) - "How does ExifTool handle coded character sets?", type-specific details are given below about comment handling for EXIF, IPTC, XMP, PNG, ID3, PDF, Photoshop, QuickTime, AIFF, RIFF, MIE and Vorbis information

### Hide data in pixels

Better if image is lossless

Ex: use PNG 64-bit RGBA to store less visible data, images in PDF

Can use 1 or more color channels

```js
/*
https://en.wikipedia.org/wiki/Steganography#Digital_steganography
https://en.wikipedia.org/wiki/File:StenographyOriginal.png https://upload.wikimedia.org/wikipedia/commons/a/a8/Steganography_original.png (access-control-allow-origin: *)
*/
(async() => {
	const img = Object.assign(new Image(), {crossOrigin: "anonymous", src: "https://upload.wikimedia.org/wikipedia/commons/a/a8/Steganography_original.png"});
	await img.decode();
	const {width, height} = img;
	const canvas = Object.assign(document.createElement("canvas"), {width, height});
	const context = canvas.getContext("2d");
	context.drawImage(img, 0, 0);
	const imageData = context.getImageData(0, 0, width, height);
	for(let {data} = imageData, i = data.length; i--;)
		data[i] = parseInt(data[i].toString(2).substr(-2), 2) * 85;
	context.putImageData(imageData, 0, 0);
	document.body.appendChild(canvas);
})();
```

- [owencm/js-steg: Javascript JPEG steganography library. Includes JS JPEG encoder and decoder with coefficient access helper functions.](https://github.com/owencm/js-steg)
- [Small JS library that packs your files into a PNG](https://github.com/claus/PNGDrive)
- [skeeto/pngarch: Archive files inside a PNG image](https://github.com/skeeto/pngarch)
- Compress data / JS code using pixels of a PNG: [Compression using Canvas and PNG-embedded data - Nihilogic](http://wayback.archive.org/web/20131209074604/http://blog.nihilogic.dk/2008/05/compression-using-canvas-and-png.html)
- [Colin Keigher: Going viral on Imgur with Powershell and PNG](http://colin.keigher.ca/2016/12/going-viral-on-imgur-with-powershell.html)
- [Using ImageMagick to reveal existence of hidden steganographic messages with DIY IM-simpleGUI tool | Guidance Blog](http://saisa.eu/blogs/Guidance/?p=1128)
- Hide data in Youtube video [Hijacking Youtube to transmit your Data – Hiding in plain sight](https://banmeihack.wordpress.com/2016/07/26/hijacking-youtube-to-transmit-your-data/) and [Hijacking YouTube to transmit your data | Hacker News](https://news.ycombinator.com/item?id=12166332)
- [week4 : 3 : Steganography and Image hiding](https://codepen.io/garethesn/pen/jbaarj)
- [petereigenschink/steganography.js: Hide secret messages with JavaScript and this library](https://github.com/petereigenschink/steganography.js/)
- [Virus Bulletin :: Script in a lossy stream](https://www.virusbulletin.com/virusbulletin/2015/03/script-lossy-stream)
	> You can perturb the input of the DCT so that a specific IDCT implementation will generate the desired output
	>
	> In general signal-processing terms, this is known as preemphasis/equalisation --- since the communications channel will distort the signal in a known way, by sending a signal distorted appropriately in the opposite direction, it will arrive "undistorted" at the destination.
	>
	> You can also consider using ECC codes, so that any small errors introduced can be corrected.
	> — https://news.ycombinator.com/item?id=17589503
- [Another nasty trick in malicious PDF](https://blog.avast.com/2011/04/22/another-nasty-trick-in-malicious-pdf/)

### Hide data with combination

Prepend or append data. Easily detectable.

- ZIP and RAR can have prepend data before header
	>  The spec is specifically that the last header is the only valid header

	`zip` return a warning "extra bytes at beginning or within zipfile"

	- [Doesn't respect zip format · Issue #148 · gildas-lormeau/zip.js](https://github.com/gildas-lormeau/zip.js/issues/148)

	Ex: prepend data with a valid image

	```sh
	zip -r secret.zip file1 file2
	cat cat.gif secret.zip > fun.gif
	# Upload fun.gif
	unzip fun.gif
	```

### VeraCrypt partition hidden in MP4 video

![VeraCrypt partition in MP4 file](http://keyj.emphy.de/files/tcsteg.svg)

- [KeyJ's Blog : Blog Archive » Real Steganography with TrueCrypt](http://keyj.emphy.de/real-steganography-with-truecrypt/)

### Hidden partition in encrypted partition

Require 2 passwords. You can provide the first one if forced if the existance of the encrypted container is known (susception of encrypted data, ex: an image contains steganography data). But the revelated data can't prove an hidden data exist

volume: decoy (encrypted data) + outer (encrypted data of the hidden volume)

![The layout of a standard VeraCrypt volume before and after a hidden volume was created within it](https://download-codeplex.sec.s-msft.com/Download?ProjectName=veracrypt&DownloadId=931263)
![Example Layout of System Drive Containing Hidden Operating System](https://download-codeplex.sec.s-msft.com/Download?ProjectName=veracrypt&DownloadId=931269)

- can start the decoy operation system (normaly)
- can load additional volume
- can start the hidden operating system (require password)

- [Deniable encryption — Wikipedia](https://en.wikipedia.org/wiki/Deniable_encryption)
- [Plausible deniability — Wikipedia](https://en.wikipedia.org/wiki/Plausible_deniability)
- [Déni plausible (cryptologie) — Wikipédia](https://fr.wikipedia.org/wiki/D%C3%A9ni_plausible_%28cryptologie%29)
- [VeraCrypt - Documentation](https://veracrypt.codeplex.com/wikipage?title=Hidden%20Volume) - Hidden Volume
- [Add smart card support for outer and hidden volumes · Issue #2 · ggkitsas/cryptostick-truecrypt](https://github.com/ggkitsas/cryptostick-truecrypt/issues/2) - Volume Format
- [VeraCrypt - Documentation](https://veracrypt.codeplex.com/wikipage?title=VeraCrypt%20Hidden%20Operating%20System) - Hidden Operating System
- [VeraCrypt : comment chiffrer et cacher un OS complet](https://www.nextinpact.com/news/103280-veracrypt-comment-chiffrer-et-cacher-os-complet.htm)

### Polyglot files

Note: About polyglot files contains HTML/JS. With Web browser, it could be blocked by `X-Content-Type-Options: nosniff` (for `<script src="image.jpg">`) to prevent CSP bypass. See:

Note: ZIP (APK, ODT, DOCX, JAR…), 7z, RAR, HTML, PDF (header must be in the first 1024 bytes) are not enforced to have the signature at offset 0 (could be prepend with something else)

- [1288361 – Return a network error for requests whose type is "script" and response has a MIME type that starts with image/](https://bugzilla.mozilla.org/show_bug.cgi?id=1288361)
- [433049 - Security: Block scripts that start with a valid image header - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=433049)
- [Polyglot (computing) — Wikipedia](https://en.wikipedia.org/wiki/Polyglot_%28computing%29)
- [Schedule 31. Chaos Communication Congress](http://wayback.archive.org/web/20150423114933/https://events.ccc.de/congress/2014/Fahrplan/events/5930.html)
- https://events.ccc.de/congress/2014/Fahrplan/system/attachments/2562/original/Funky_File_Formats.pdf
- [Polyglot Inception: JPEG = CSS = JS = HTML](http://incept10n.com/)
- [International Journal of Proof-of-Concept or Get The Fuck Out (PoC||GTFO)](https://www.alchemistowl.org/pocorgtfo/)
	> 0x15 is a laser-projectable PDF that's also a ZIP containing, among other things, another PDF that is also a Git repo of its own source code.
	> 0x16 is a polyglot that is valid as a PDF document, a ZIP archive, and a Bash script that runs a Python webserver which hosts Kaitai Struct’s WebIDE which, allowing you to view the file’s own annotated bytes.
	> 0x17 is a PDF that's also a valid ZIP and valid firmware for Apollo Guidance Computer.
- Bulletproof Images: Hide payload in JPEG which will keep unchanged after libgd transformations
	Detect what bytes are not recreated after parsed and saved (image recreation)

	JPEG:
	- [Обход безопасной загрузки изображений - RDot](https://rdot.org/forum/showthread.php?t=2780) (generate an error, but works with GD)
	- [Bulletproof JPEGs - virtualabs.fr](http://www.virtualabs.fr/Nasty-bulletproof-Jpegs-l)
	PNG:
	- [Encoding Web Shells in PNG IDAT chunks | Application Security](https://www.idontplaydarts.com/2012/06/encoding-web-shells-in-png-idat-chunks/)
	GIF:
	- [Exploiting PHP-GD imagecreatefromgif() function](https://github.com/fakhrizulkifli/Defeating-PHP-GD-imagecreatefromgif) - Proof-of-concept to exploit the flaw in the PHP-GD built-in function, `imagecreatefromgif()`
- [pocorgtfo/README.md at master · angea/pocorgtfo](https://github.com/angea/pocorgtfo/blob/master/writeups/19/README.md#rename-extension) - HTML parser can be stopped by `<script>document.documentElement.innerHTML = document.getElementById("mypage").innerHTML;</script>`: "The page payload escapes out of the whole file so that the browser stops loading the whole file (which is 64 Mb)."
- [pocorgtfo/README.md at master · angea/pocorgtfo](https://github.com/angea/pocorgtfo/blob/master/writeups/19/README.md#write-up) - Polyglot PDF - ZIP - HTML file
- [How to create polyglot HTML/JS/Wasm module | WebAssembly Security](https://webassembly-security.com/polyglot-webassembly-module-html-js-wasm/)

### Polyglot JPEG - ZIP file

Could also works with all other formats that support ICC: TIFF, GIF, JPEG 2000, [PSD](http://justsolve.archiveteam.org/wiki/Photoshop_Image_Resources)

ZIP data in JPEG survive image processing (resize, stripping EXIF data, recompressing, etc.)

Use ICC profiles, ICC profile chunk size limits (65376 for the first file, else 65521 for the others, this why the zip for bigger files must contains multipart .rar)

> In a JPEG file, an APP2 marker with an identifier of "ICC_PROFILE" is used for ICC profiles. See the ICC profile specification for details. Note that large ICC profiles must be split up, to accommodate JPEG's 64KB segment size limit.

> Yes, if you open the file as text you will find the magic number of icc profile (acsp) follwoed by a bunch of random bytes and that of zip (PK/x03/x04). It is quite easy to append arbitrary data to JPEG files [0] and however there is no guarantee that it will survive image processing, so it was necessary to hide it within an ICC　profile. As for zip, unzip will happily decode any data stream as long as it makes sense and ignore the parts that don't.

> It isn't massively complex, but it did require some custom encoding/decoding logic.

- [Dаvіd Вucһаnаn on Twitter: "Assuming this all works out, the image in this tweet is also a valid ZIP archive, containing a multipart RAR archive, containing the complete works of Shakespeare. This technique also survives twitter's thumbnailer :P… https://t.co/glgrQSz7cK"](https://twitter.com/David3141593/status/1057042085029822464)
- [Dаvіd Вucһаnаn on Twitter: "Source code. This one is also a PDF :P… "](https://twitter.com/David3141593/status/1057609354403287040)
- [JPEG image of Shakespeare which is also a zip file containing his complete works | Hacker News](https://news.ycombinator.com/item?id=18342042)
- [Command-line Options @ ImageMagick](http://www.imagemagick.org/script/command-line-options.php#profile)

	```sh
	curl 'https://pbs.twimg.com/media/DqteCf6WsAAhqwV.jpg' > tmp.zip  && unzip tmp.zip && unrar e shakespeare.part001.rar
	curl 'https://pbs.twimg.com/media/Dq1iEpfXgAADZRg.jpg' > tmp.pdf  && unzip tmp.pdf
	```

	```
	binwalk DqteCf6WsAAhqwV.jpg
	DECIMAL	   HEXADECIMAL	 DESCRIPTION
	--------------------------------------------------------------------------------
	0			 0x0			 JPEG image data, JFIF standard 1.01
	182		   0xB6			Zip archive data, at least v1.0 to extract, ..., name: shakespeare.part001.rar
	...
	1971177	   0x1E13E9		End of Zip archive
	```

### Polyglot JPEG - HTML file

This webpage is also a JPEG image: http://lcamtuf.coredump.cx/squirrel/.

1. The file is a valid jpeg file with some html in metadata
2. The server responds with `Content-Type: text/html`, making browser interpret the response body as html
3. Content before `<html>` tag are included in body (permissive behavior or HTML5), needed to be hidden
4. The html in the jpeg metadata ends with `<!--` , which starts html comment
5. The html has `<img src="#">` that renders the file as image (self reference)

```sh
exiftool -comment='<style>*{visibility: hidden;} div{visibility: visible; position: absolute;}</style><div><h1>Web Scale Big Database</h1><img src="#"><!--' image.jpg
mv image.jpg index.html
```

See [This HTML page is also a JPEG : programming](https://www.reddit.com/r/programming/comments/4wak58/this_html_page_is_also_a_jpeg/d65fe6m/)

### Polyglot GIF - JS file

[Funky File Formats \[31c3\] - YouTube](https://www.youtube.com/watch?v=Ub5G_t-gUBc&t=571) and https://speakerdeck.com/ange/funky-file-formats-31c3?slide=42

```py
header = (
	b'\x47\x49\x46\x38\x39\x61'  #Signature + Version  GIF89a
	b'\x2F\x2A' #Encoding /* it's a valid Logical Screen Width
	b'\x0A\x00' #Smal Logical Screen Height
	b'\x00' #GCTF
	b'\xFF' #BackgroundColor
	b'\x00' #Pixel Ratio
	b'\x2C\x00\x00\x00\x00\x2F\x2A\x0A\x00\x00\x02\x00\x3B' #GlobalColorTable + Blocks
	b'\x2A\x2F' #Commenting out */
	b'\x3D\x31\x3B' # enable the script side by introducing =1;
)
trailer = b'\x3B'
 I made this explicit, step by step .
f.write(header)
f.write(payload)
f.write(trailer)

///////
"""
Injects the payload into existing GIF
NOTE: if the GIF contains \xFF\x2A and/or \x2A\x5C might caouse issues
"""
 I know, I can do it all in memory and much more fast.
 I wont do it here.
with open(fname + "_malw.gif", "w+b") as fout:
	with open(fname, "rt") as fin:
		for line in fin:
			ls1 = line.replace(b'\x2A\x2F', b'\x00\x00')
			ls2 = ls1.replace(b'\x2F\x2A', b'\x00\x00')
			fout.write(ls2)
	fout.seek(6,0)
	fout.write(b'\x2F\x2A') #/*

f = open(fname + "_malw.gif", "a+b") #appending mode
f.write(b'\x2A\x2F\x3D\x31\x3B')
f.write(payload)
f.write(b'\x3B')
```

An other example:

- [Perl::Visualize - search.cpan.org](http://search.cpan.org/~jnagra/Perl-Visualize-1.02/Visualize.pm) and http://cpansearch.perl.org/src/JNAGRA/Perl-Visualize-1.02/Visualize.pm
- [ThinkFu › GIF/Javascript Polyglots](https://web.archive.org/web/20200301052900/http://www.thinkfu.com/blog/gifjavascript-polyglots)

### Polyglot JPEG - JS file

- [PortSwigger Web Security Blog: Bypassing CSP using polyglot JPEGs](http://blog.portswigger.net/2016/12/bypassing-csp-using-polyglot-jpegs.html)
- [JS Bin - Collaborative JavaScript Debugging](https://jsbin.com/kenuka/edit?html,output)
- http://portswigger-labs.net/csp/csp.php?x=%3Cscript%20charset=%22ISO-8859-1%22%20src=%22http://portswigger-labs.net/polyglot/jpeg/xss.jpg%22%3E%3C/script%3E
- [XSS and injection vulnerabilities](#xss-and-injection-vulnerabilities)

### Polyglot PNG

> The idea is that PNG data can be interpreted depending on the Color Type among other types as RGB values (color type =2) or as indexed values (color type =3) together with a palette (PLTE).

- [PNG Merge - YobiWiki](https://web.archive.org/web/20200205032506/http://wiki.yobi.be/wiki/PNG_Merge)
- [Executable PNGs - djhworld](https://web.archive.org/web/20201227120231/https://djharper.dev/post/2020/12/26/executable-pngs/)

### Polyglot JSON - JS file

- [JSON hijacking for the modern web | PortSwigger Research](https://web.archive.org/web/20201108090739/https://portswigger.net/research/json-hijacking-for-the-modern-web)
- [Why Facebook's api starts with a for loop - DEV](https://web.archive.org/web/20201108102203/https://dev.to/antogarand/why-facebooks-api-starts-with-a-for-loop-1eob)
- [Crafty Tricks for Avoiding XSSI | patorjk.com](https://web.archive.org/web/20201007205809/http://patorjk.com/blog/2013/02/05/crafty-tricks-for-avoiding-xssi/)
- [api - How does including a magic prefix to a JSON response work to prevent XSSI attacks? - Information Security Stack Exchange](https://security.stackexchange.com/questions/110539/how-does-including-a-magic-prefix-to-a-json-response-work-to-prevent-xssi-attack)

### Polyglot JSON - HTML file

- [WDR](https://web.archive.org/web/20201209220539/https://webdatarender.com/)

### Angecryption

> With Angecryption, you can basically encrypt anything into whatever you want

AES(A) = B; where A and B are documents (image, pdf, etc.)

```sh
python2.7 angecrypt.py source target result [key] [algo] > decrypt.py
# where algo could be aes
#python2.7 -m pip install --user pycrypto
```

- [Fortinet Blog](https://blog.fortinet.com/2014/03/31/angecryption-at-insomni-hack)
- https://github.com/cryptax/angepoc
- https://code.google.com/archive/p/corkami/
- [when AES(☢) = ☠ --- a crypto-binary magic trick](http://www.slideshare.net/ange4771/when-aes-a-cryptobinary-magic-trick)
- [Joue à la crypto ! (french) // Speaker Deck](https://speakerdeck.com/ange/joue-a-la-crypto-french)
- https://www.blackhat.com/docs/eu-14/materials/eu-14-Apvrille-Hide-Android-Applications-In-Images.pdf
- [Encrypting a PNG into an Android application](https://github.com/cryptax/angeapk)

### IP-over-DNS

> iodine lets you tunnel IPv4 data through a DNS server. This can be usable in different situations where internet access is firewalled, but DNS queries are allowed.

- [kryo.se: iodine (IP-over-DNS, IPv4 over DNS tunnel)](https://code.kryo.se/iodine/)

## Esoteric programming languages

- [Esoteric programming language — Wikipedia](https://en.wikipedia.org/wiki/Esoteric_programming_language)
- [Brainfuck — Wikipedia](https://en.wikipedia.org/wiki/Brainfuck)
- [Brainfuck - Esolang](https://esolangs.org/wiki/Brainfuck)
- [Whitespace (programming language) — Wikipedia](https://en.wikipedia.org/wiki/Whitespace_%28programming_language%29)
- [Malbolge — Wikipedia](https://en.wikipedia.org/wiki/Malbolge)
- [Brainfuck minifier](https://mothereff.in/brainfuck-minifier) - [A brainfuck minifier written in JavaScript](https://github.com/mathiasbynens/brnfckr)
- [AA86 - Symbolic assembler demo](http://utf-8.jp/public/sas/) - Generate MS-DOS COM file with only symbols
- [Non-alpha PHP code](http://wayback.archive.org/web/20150319140303/http://sla.ckers.org/forum/read.php?24,36986)

### JSFuck and similar

Valid JavaScript, use implicit type coercion.

See also [Obfuscation (code)](#obfuscation2028code29)

- [JSFuck — Wikipedia](https://en.wikipedia.org/wiki/JSFuck)
- [JSFuck - Write any JavaScript with 6 Characters: \[\]()!+](http://www.jsfuck.com/) - see https://github.com/aemkei/jsfuck/blob/master/jsfuck.js
- [JSF*ck - \[\]()!+](http://utf-8.jp/public/jsfuck.html) - **Broken**
- [Folders - Esolang](https://esolangs.org/wiki/Folders) - Encode data using folder structure
- [Language list - Esolang](https://esolangs.org/wiki/Language_list)
- [Brainfuck beware: JavaScript is after you! | Patricio Palladino](http://patriciopalladino.com/blog/2012/08/09/non-alphanumeric-javascript.html) and https://github.com/alcuadrado/hieroglyphy
- [Converts javascript command into no alnum version using only []()+! characters](http://discogscounter.getfreehosting.co.uk/js-noalnum_com.php)
- [Java/script: no alnum cheat sheets](http://wayback.archive.org/web/20150420005536/http://sla.ckers.org/forum/read.php?24,33349,33405)
- [YAUC Less chars needed to run arbitrary JS code = 6! (JS GREAT WALL)](http://wayback.archive.org/web/20150319154336/http://sla.ckers.org/forum/read.php?24,32930)
- [Diminuitive NonAlNum JS - Arbitrary](http://wayback.archive.org/web/20111230091043/http://sla.ckers.org/forum/read.php?24,35081)
- [Diminutive JS Code Challenge, from OWASP](http://wayback.archive.org/web/20110708231619/http://sla.ckers.org/forum/read.php?24,30015)
- [Diminutive NoAlNum JS Contest](http://wayback.archive.org/web/20150319163133/http://sla.ckers.org/forum/read.php?24,28687)
- [Hackvertor](https://hackvertor.co.uk/public) [Hackvertor](http://www.businessinfo.co.uk/labs/hackvertor/hackvertor.php) - see ("Hacker" >) 3chr_nonalpha, aaencode, phpnonalpha, phpnonalpha2, hasegawa, etc.
- [aaencode - Encode any JavaScript program to Japanese style emoticons (^_^)](http://utf-8.jp/public/aaencode.html)
- [jjencode - Encode any JavaScript program using only symbols](http://utf-8.jp/public/jjencode.html)
- [Diminuitive NonAlNum JS - Arbitrary](http://wayback.archive.org/web/20111230091043/http://sla.ckers.org/forum/read.php?24,35081)
- [New JavaScript obfuscator: JScrambler](http://wayback.archive.org/web/20111230080027/http://sla.ckers.org/forum/read.php?24,33722)
- [Code Obfuscation Algorithms](http://wayback.archive.org/web/20131109221321/http://sla.ckers.org/forum/read.php?24,28674)
- [String hacks (ways to make a string)](http://wayback.archive.org/web/20131109230330/http://sla.ckers.org/forum/read.php?24,28642)
- [deobfuscation - How does this obfuscated javascript code work? - Stack Overflow](https://stackoverflow.com/questions/21955230/how-does-this-obfuscated-javascript-code-work/21955587)
- [obfuscation - Obfuscated javascript code with binary values? - Stack Overflow](https://stackoverflow.com/questions/3910353/obfuscated-javascript-code-with-binary-values)
- [obfuscation - How does this magic Javascript work? - Stack Overflow](https://stackoverflow.com/questions/22588223/how-does-this-magic-javascript-work)
- [KoreBlog javascript_deobfuscation](https://blog.korelogic.com/blog/2015/01/12/javascript_deobfuscation)
- [Edit fiddle - JSFiddle](http://jsfiddle.net/e6na63L8/)
- [DW56-1-JSObfuscation.pdf](http://www.digitalwhisper.co.il/files/Zines/0x38/DW56-1-JSObfuscation.pdf)
- [mame/jsfuck-quine: A JavaScript Quine written in the JSFuck style](https://github.com/mame/jsfuck-quine)
- [שלום עולם – JavaScript Written in the Hebrew Alphabet](http://aem1k.com/%D7%A9%D7%9C%D7%95%D7%9D-%D7%A2%D7%95%D7%9C%D7%9D/)
- [aurebesh.js – Translate JavaScript to Other Writing Systems](http://aem1k.com/aurebesh.js/)

- `13 + !0 === 14`
- `null == undefined`
- `+"3" === 3`, `isFinite(null) === true` (unary plus converting something into a number)
- `(null < 0) === false && (null > 0) === false && (null == 0) === false && (null === 0) === false` but `(null + 1) === 1`, `null <= 0 && null >= 0`, `!null === true` (null is integerflexible)
- `"200" - 0 === 200; "200" + 0 === 200`

```js
var $ = ~[];				// -1
$ = {
	___: ++$,				// 0   : 	-1 + 1 is 0
	$$$$: (![] + "")[$],	// "f" : ![] is false, +"" converts false to "false" "false"[0] is "f"
	__$: ++$,				// 1   : 0 + 1 is 1
	$_$_: (![] + "")[$],	// "a" : "false"[1] is "a"
	_$_: ++$,				// 2   : 1 + 1 is 2
	$_$$: ({} + "")[$],		// "b" : {} is an object, +"" converts it to "[object Object]", "[Object object]"[2] is "b"
	$$_$: ($[$] + "")[$],	// "d" : 2[2] is undefined, +"" converts it to "undefined", "undefined"[2] is "d"
	_$$: ++$,				// 3   : 2 + 1 is 3
	$$$_: (!"" + "")[$],	// "e" : !"" is true, +"" converts it to "true", "true"[3] is "e"
	$__: ++$,				// 4   : 3 + 1 is 4
	$_$: ++$,				// 5   : 4 + 1 is 5
	$$__: ({} + "")[$],		// "c" : {} is an object, +"" converts it to "[object Object]", "[Object object]"[5] is "c"
	$$_: ++$,				// 6   : 5 + 1 is 6
	$$$: ++$,				// 7   : 6 + 1 is 7
	$___: ++$,				// 8   : 7 + 1 is 8
	$__$: ++$				// 9   : 8 + 1 is 9
};
```

```js
$.$_ = ($.$_ = $ + "")[$.$_$] + ($._$ = $.$_[$.__$]) + ($.$$ = ($.$ + "")[$.__$]) + ((!$) + "")[$._$$] + ($.__ = $.$_[$.$$_]) + ($.$ = (!"" + "")[$.__$]) + ($._ = (!"" + "")[$._$_]) + $.$_[$.$_$] + $.__ + $._$ + $.$;

// Explanation:
// $.$_ = "[object Object]"[5] + "[object Object]"[1] + "undefined"[2] +
// "false"[3] + "[object Object]"[6] + "true"[1] + "true"[2] + "c"+"t"+"o"+ "r";

// Result:
// $.$_ = "c"+"o"+"n"+"s"+"t"+"r"+"u"+"c"+"t"+"o"+"r";
```

```js
$.$$ = $.$ + (!"" + "")[$._$$] + $.__ + $._ + $.$ + $.$$;
//	 "r" + "true"[3]		 + "t"  + "u" + "r" + "n" ;
```

```js
$.$ = ($.___)[$.$_][$.$_];
```

```js
// No alphanumeric characters, all 32 ASCII symbols
-~!/#/^("\@"._*[,]>='<'?$&+_|$:``%{});// === 1
```

Then evaluate JavaScript. See [Parse JavaScript using the native parser](JavaScript#parse-javascript-using-the-native-parser)

```js
var w = this;
for(p1 in w)
	// 110 = "n"
	// 114 = "r"
	if(p1.length == 9 && p1.charCodeAt(0) == 110 && p1.charCodeAt(8) == 114){
		break;
	}
for(p2 in w[p1]){
	// 112 = "p"
	// 115 = "s"
	if(p2.length == 7 && p2.charCodeAt(0) == 112 && p2.charCodeAt(6) == 115){
		break;
	}
}
//w = "window", p1 = "navigator", p2 = "plugins"
w[p1][p2]["length"];
```

> [The minus operator (`-`)](http://www.ecma-international.org/ecma-262/7.0/index.html#sec-subtraction-operator-minus) coerces both of its operands to numbers.
> [The plus operator (`+`)](http://www.ecma-international.org/ecma-262/7.0/index.html#sec-addition-operator-plus) is special in that it has two modes.
> First, its normal mode is adding two numbers. Therefore, many values are coerced to numbers
> Second, using plus for string concatenation is also supported. Therefore, as soon as one of the operands is a string, the other one is converted to a string, too
> The exact algorithm for + looks like this:
> 1. Ensure that both operands are primitives. Objects `obj` are converted to primitives via the internal operation `ToPrimitive(obj)`, which calls `obj.valueOf()` and – if that doesn’t work – `obj.toString()`. For dates, `obj.toString()` is called first.
> 2. If either operand is a string, then convert both to strings and return the concatenation of the results.
> 3. Otherwise, convert both operands to numbers and return the sum of the results.

— ["200" + 0 returns "2000", but "200" - 0 return 200...wtf javascript](https://www.reddit.com/r/javascript/comments/55jh40/200_0_returns_2000_but_200_0_return_200wtf/d8b7b2a)
- `[] + [] === ""`, `String([] + {}) === "[Object object]"`, `{} + [] === 0`, `String(new Array(16)) === ",,,,,,,,,,,,,,,"`

- `[1] + [2] - [3] == 9` - [Why does \[1\] + [2] - [3] = 9 : javascript](https://www.reddit.com/r/javascript/comments/5lmgpz/why_does_1_2_3_9/)
- [What is {} + {} in JavaScript?](http://www.2ality.com/2012/01/object-plus-object.html)
- [You Don't Know JS: Types & Grammar - You-Dont-Know-JS/ch4.md at master · getify/You-Dont-Know-JS](https://github.com/getify/You-Dont-Know-JS/blob/master/types%20%26%20grammar/ch4.md)
- [Arithmetic operators - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators)
- [Equality comparisons and sameness - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)
- [wtfjs - a little code blog about that language we love despite giving us so much to hate](http://wtfjs.com/)
- [JS Comparison Table](https://dorey.github.io/JavaScript-Equality-Table/)
- [Zeros in JavaScript](http://zero.milosz.ca/)

## Code obfuscation

See [Hacking](#hacking)

Obfuscate code and bytecode

Pirates bypass anti-viruses. Client integrity — prevent client to modify instruction/code. See [Malware](#malware)

- Ajouter du bruit / Injection de code inutile (alourdir volontairement le code pour noyer dans la masse)
	* ajout d'instructions valides inutiles et/ou d'arguments inutiles aux fonctions (pour rendre la lecture du code plus complexe)
	* ajout d'instructions invalides et un saut au-dessus de ces instructions pour dérégler les désassembleurs ne supportant pas ce genre de « protection »
	* Utiliser différents contexts, récursions, remplacement de boucles, conditions et opérations par des version plus complexes (`x/2` -> `x >>> 1`)
	* http://en.wikipedia.org/wiki/Write-only_language
	* [Spaghetti code — Wikipedia](https://en.wikipedia.org/wiki/Spaghetti_code)
- mangle names: identifiants renommés avec des noms sémantiquement muets, avec caractères non affichables ([espace visible ou non](http://en.wikipedia.org/wiki/Space_%28punctuation%29#Spaces_in_Unicode), null char `\x0`, charactères spéciaux `/\"'(){}`) ou nom portant confusion avec l'API native
- `base64(base64(payload))`, `btoa(pako.deflate(root.dca_compressor.utf16to8(JSON.stringify(requests)), {to: "string"}))`

	See also:

	* [mikemo » AprilScript: ActionScript worst practices](http://wayback.archive.org/web/20111029080653/http://www.morearty.com/blog/2009/04/01/aprilscript-actionscript-worst-practices/)
	* [How To Write Unmaintainable Code](https://www.thc.org/root/phun/unmaintain.html)
- remove indentation, remove non significative spaces
- remove comments
- [Polymorphic code — Wikipedia](https://en.wikipedia.org/wiki/Polymorphic_code). Different operation give the same output (`1+3 == 6-2`, etc.)
- use different types: string or bits / bytes vs numbers
- intermediate state (use evaluation/decoding step)
	* [ROT13 — Wikipedia](https://en.wikipedia.org/wiki/ROT13), ROT47 - translate charset to an other charset. [Substitution cipher — Wikipedia](https://en.wikipedia.org/wiki/Substitution_cipher)
	* Encoder des informations (clés, bytecode…) dans les fichiers image, audio, etc.: [Hide data](#hide-data)
	* Encoder les informations (clés) dans des chaines courantes "This program cannot be run in DOS mode."
		- [assembly - Is it possible to hide a password defined within C++ code - Stack Overflow](https://stackoverflow.com/questions/5316562/is-it-possible-to-hide-a-password-defined-within-c-code/5316925#5316925)
- Use predictible but unsual / non logical / ambigous operations:
	* instead of boolean, return `String(boolean).charCodeAt(x)`, `func() == y` → `function foo(){(""+boolean)[1] == "r"} foo() == "y"`
	- (languages that support operator overloading) `path / file == path + "/" + file`
	* https://github.com/kitcambridge/evil.js - mess up Javascript native functions (ex. `isNaN()` always return true). See also https://github.com/mathiasbynens/evil.sh
	* use special chars or lookalike chars (confusable homoglyphs):
		- invisible char zero-width chars (U+200B, U+00AD): `window["test"] = "test"`, but `window["te​st"] != "test"`
			`var a = "http://e­x­a­m­p­l­e­.­com", b = "http://example.com"; a != b; a.split(/\s+/).join() == b`
		- http://www.unicode.org/Public/security/latest/confusables.txt see [UTS #39: Unicode Security Mechanisms](http://www.unicode.org/reports/tr39/#confusables)
		- [vhf/confusable_homoglyphs: ϲοｎｆｕѕаｂｌе＿һοｍоɡｌｙｐｈｓ](https://github.com/vhf/confusable_homoglyphs) (use the file provided by Unicode consortium)
		- greek question mark `;` (U+037E) vs. semicolon `;`
		- greek chars `Α, Β, Ε, Ζ, Η, Ι, Κ, Μ, Ν, Ο, Ρ, Τ, Υ, Χ, Ϊ, Ϋ, ο, Ϲ, Ϻ` vs `A, B, E, Z, H, I, K, M, N, O, P, T, Y, X, Ï, Ÿ, o, C, M`
		- Roman Numerals: `ⅰ, ⅴ, ⅹ, ⅼ, ⅽ, ⅾ, ⅿ` vs `i, v, x, l, c, d, m`
		- russia chars (depends fonts & styles): `а, е, и, м, о, о, п, р, р, с, т, у, х` vs `a, e, u, M, o, O, n, P, р, c, m, y, x`
		- diacritics: `é, è, ë, ê, ...` vs `e`. See [Diacritic — Wikipedia](https://en.wikipedia.org/wiki/Diacritic)
		- `﹩` vs `$`
		- `˸` vs `:`
		- ` ` vs `-`: ` 2 != -2`. `(2+ 40) == 42`. ` ` is a white space (Unicode `WSpace` `U+1680 OGHAM SPACE MARK`) See [Hyphen — Wikipedia](https://en.wikipedia.org/wiki/Hyphen#Unicode), [javascript - Why does 2+ 40 equal 42? - Stack Overflow](https://stackoverflow.com/questions/31507143/why-does-2-40-equal-42)
		- with JS implicit type coercion `"-2" == -2`, but `"−2" != -2` (`-` vs `−`)
		-`2*2==4`, but `2✲2==undefined`
		- `𝟣+𝟣` (`SyntaxError: Invalid or unexpected token`/`SyntaxError: illegal character`) `MATHEMATICAL SANS-SERIF DIGIT` [Unicode Characters in the 'Number, Decimal Digit' Category](http://www.fileformat.info/info/unicode/category/Nd/list.htm)
		- https://en.wikipedia.org/wiki/Whitespace_character#Spaces_in_Unicode
		- `'mañana' != 'mañana'; 'ma\xF1ana' != 'man\u0303ana'; 'ma\xF1ana'.length == 6; 'man\u0303ana'.length == 7;` https://mathiasbynens.be/notes/javascript-unicode#accounting-for-lookalikes

		Note: all languages / parsers / engines are not compatible

		See [Fancy transformation](Text#Fancy transformation)

		- https://github.com/reinderien/mimic and https://github.com/reinderien/mimic/wiki/Character-Set
		- [JavaScript variable name validator](https://mothereff.in/js-variables)
		- https://mathiasbynens.be/notes/javascript-identifiers-es6 and https://github.com/mathiasbynens/mothereff.in/tree/master/js-variables and https://stackoverflow.com/questions/1661197/what-characters-are-valid-for-javascript-variable-names
		- [Unicode Utilities: Confusables](https://util.unicode.org/UnicodeJsps/confusables.jsp)

	* Use RLO (Right-to-Left Override) or Bidi chars:

		```js
		(eye="‮rotator")+eval('alert(eye)')
		```

		```js
		"‮";(llun=eval)
		"‮";llun(`"‮";alert
		(llun)`)
		```

		```js
		(a=1) > 0; (א=1) > 0;
		```

		- [JS Bin - Collaborative JavaScript Debugging](https://jsbin.com/nihifi/edit?html,output)
		- [JS Bin - Collaborative JavaScript Debugging](https://jsbin.com/heriku/edit?html,output)
		- [Unicode Bidirectional Algorithm basics](https://www.w3.org/International/articles/inline-bidi-markup/uba-basics#mirroring)
	* [Mind your languages - 09-mind-languages.pdf](http://static.sstic.org/rumps2014/09-mind-languages.pdf) and ["Mind Your Languages" - Nouvel article sur l'importance des langages pour la sécurité - ANSSI](http://www.ssi.gouv.fr/fr/anssi/publications/publications-scientifiques/articles-de-conferences/mind-your-languages-nouvel-article-sur-l-importance-des-langages-pour-la.html)
	* [A Collection of JavaScript Gotchas - CodeProject](http://www.codeproject.com/Articles/182416/A-Collection-of-JavaScript-Gotchas)
	* 	eval(unescape(escape`𩁯𨱵𫑥𫡴𛡷𬡩𭁥𨀼𨱡𫡶𨑳𘁩𩀽𠐠𪁥𪑧𪁴🐲𝐰🡠𞱦𫱲𚁑🐶𩐴𞱑𛐭𞱁𛡧𩑴𠱯𫡴𩑸𭁠𜡤𨀮𩡩𫁬𤡥𨱴𚁑𙐳𜀰𛁑𛰳𜀰𛀱𛁉𛰹𜀩𚑦𫱲𚁖👘👑𛰱𜀰𙐳𛐲𛁗👙👑𛰳𩐴𛐱𛁉🐹𜀻𢐭𛐦𙡗𚡗🀹𞱗👚𚱚𚱙𚑚👖𚡗𛁖👖𚡖𛑗𚡗𚱘`.replace(/u../g,''))) // draw mandelbrot with 140 chars
		- [xem on Twitter: "eval(unescape(escape`𩁯𨱵𫑥𫡴𛡷𬡩𭁥𨀼𨱡𫡶𨑳𘁩𩀽𠐠𪁥𪑧𪁴🐲𝐰🡠𞱦𫱲𚁑🐶𩐴𞱑𛐭𞱁𛡧𩑴𠱯𫡴𩑸𭁠𜡤𨀮𩡩𫁬𤡥𨱴𚁑𙐳𜀰𛁑𛰳𜀰𛀱𛁉𛰹𜀩𚑦𫱲𚁖👘👑𛰱𜀰𙐳𛐲𛁗👙👑𛰳𩐴𛐱𛁉🐹𜀻𢐭𛐦𙡗𚡗🀹𞱗👚𚱚𚱙𚑚👖𚡗𛁖👖𚡖𛑗𚡗𚱘`.replace(/u../g,''))) // 140brot https://t.co/GPSFxeYwSD"](https://twitter.com/MaximeEuziere/status/843397121369956354)
	* [IEEE 754](../../../../IEEE%20754.md) Floating-point numbers limitations
		- [particularité de IEEE 754 Floating-point numbers:](https://stackoverflow.com/questions/3730019/why-not-use-double-or-float-to-represent-currency)
		- [`0.1 + 0.2 != 0.3`](https://stackoverflow.com/questions/588004/is-floating-point-math-broken))
		- `0.2 + 0.4 !== 0.6`
		- `9999999999999999 == 10000000000000000`, `9999999999999999 + 2 == 10000000000000002`, `9999999999999999 + 3 == 10000000000000004`, `35.855*100 == 3585.4999999999995`
		- `Math.sin(Math.PI) < Number.EPSILON` `1.2246467991473532e-16 < 2.2204460492503130808472633361816E-16//2 ** -52`
		- `Math.abs(0.2 - 0.3 + 0.1) < Number.EPSILON`
		See `Number.EPSILON`
		- https://github.com/brianleroux/wtfjs/blob/master/posts/2010-02-16-more-floating-point-rounding.md
	* ECMAScript[wtfjs](https://github.com/brianleroux/wtfjs) - contains some posts about ECMAScript specificities
	* ECMAScript date with timezone: `new Date("2016-03-28").getDate() // could returns 27` "New Date(dateString), creates a new date object as ZERO time PLUS the input. You must take timezone-offset into account. If you don't specify a time-zone, the date-object defaults to your browser's time-zone (which might be different from UTC)"
		"Date string is parsed as UTC, then converted to local timezone. So in Boston, new Date("2017-02-28") is Feb 27 2017 19:00:00 GMT-0500 (EST)"
	* ECMAScript bitwise opertations transform 64 bits float to 32 bit integer
		- `~~0.5 == 0`
		[Tilde or the Floor? Practical use for JavaScript bitwise operators. (#1) | rocha.la](http://rocha.la/JavaScript-bitwise-operators-in-practice)
	* ECMAScript null
		`!(null > 0) && !(null == 0) && null >= 0`
		- [Javascript : The Curious Case of Null \>= 0 – Camp Vanilla](https://blog.campvanilla.com/javascript-the-curious-case-of-null-0-7b131644e274)
	* ECMAScript, zeros
		- `-0 === +0`
		- `3 / -0 === -Infinity` (or `Math.pow(-0, -1)`) where `3 / +0 === Infinity` (or `Math.pow(+0, -1)`)
		- http://speakingjs.com/es5/ch11.html#_distinguishing_the_two_zeros
	* ECMAScript, implicit type coercion, see [JSFuck and similar](#jsfuck-and-similar)
	* ECMAScript, rewrite test:
		- `let a = new Number(10); a.valueOf => 20; //-> a == 20; a !== 20; Number.prototype.valueOf.apply(a) === 10 // String(a) == "10" && a.toString() == "10" // typeof a == "object"` primitive can be wrapped by an object
		- `Symbol.hasInstance`, `Symbol.toPrimitive`, `Symbol.toStringTag`: http://www.2ality.com/2015/09/well-known-symbols-es6.html
	* ECMAScript, trailing comma don't add an element: [Trailing commas in JavaScript - Stack Overflow](https://stackoverflow.com/a/11306770/470117)
	* ECMAScript, `var x = NaN; x !== x`
	* ECMAScript: `0[["__proto__"]] === Number.prototype`: [An Abusive Relationship with AngularJS](http://slideshare.net/x00mario/an-abusive-relationship-with-angularjs)
	* Java:
		- `Integer.valueOf(6) == Integer.valueOf(6)` but `Integer.valueOf(1000) != Integer.valueOf(1000)` (`==` is not `equal()`)
		- `(byte) + (char) - (int) + (long) - 1` (give `1`) (equivalent to `+ - + -1` and `-(-1)`?)
		Explainations: [Some Education While Feeding a Code Troll | Danimo's blog](https://daniel.molkentin.net/2015/02/18/some-education-while-feeding-a-code-troll/)
	* ECMAScript, `(new Date('2012-08-01')).getTime() - (new Date('2012-8-01')).getTime() !== 0`, `(new Date('2012-08-01')).getTime() - (new Date('2012/08/01')).getTime() !== 0`
	* ECMAScript, `this` in a closure or in global refer to `window` (ex.: in event listener) but not in arrow function nor in ES6 module
	* ECMAScript: `parseInt(0.0000008, 10) === 8` but `parseInt("0.0000008", 10) === 0` and `parseFloat(0.0000008, 10) === 8e-7`. Because `String(0.0000008) === 8e-7`. See [Chapter 11. Numbers](http://speakingjs.com/es5/ch11.html#parseInt)
	* ECMAScript, `window["eval"]()`
	* ECMAScript `Number("") === 0` `Number(" ") === 0` `Number("\u00A0") === 0`
	* ECMAScript `"--undefined--".search(undefined) == 0` `"--undefined--".search("undefined") == 2` `"--undefined--".search("a") == -1`
	* ECMAscript, [11 Ways to Invoke a Function](https://gist.github.com/myshov/05800f083a0afce56e0f782314a103eb)
	* ECMAScript, `[Function("console.log(this)")][0]()` `this` is the array itself. `const arr = [function(){return this === arr}]; arr[0]();// true` It's a method call (JS quirk of Array elements being properties). `arr` is an object, `0` is a method name, `this` is bound to `arr`
	* ECMAScript `var \u{61};` (valid in ES6)
	* ECMAScript `let n1 = 123,456,789;// 789`
	* ECMAScript `12 === 0xC === 0b1100 === 9+3`
	* ECMAScript [commas operators](http://speakingjs.com/es5/ch09.html#comma_operator).
		`var x = 0; var y = (x++, 10); x == 1 && y == 10;` can be written `var x = 0, y = (x++, 10);`
		`[].concat[1,2,3];` will return `[1,2,3]` if you do `Array.prototype.concat[3] = [1,2,3];` first.
		Other example: `({baz: "a"})["foo","bar","baz"]` is the same as `({baz: "a"})["baz"]`

		- http://www.2ality.com/2016/11/concat-array-literal.html
	* ECMAScript `void 4+7 === (void 4)+7`, `void 4+7 !== void (4+7)` http://speakingjs.com/es5/ch09.html#void_operator
	* ECMAScript: `["10", "10", "10"].map(parseInt) // [10, NaN, 2]`
		Because in `array.map(callback)`, the `callback` receive [3 parameters (`currentValue`, `index`, `array`)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map#Parameters).
		And `parseInt()` accept [2 parameters (`string`, `radix`)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt#Parameters)

		Use `["10", "10", "10"].map(value => parseInt(value))` instead
	* ECMAScript: `Array.prototype.push("test"); let empty = []; empty.length === 0; empty[0] === "test"; Array.prototype[0] === "test"` `Array.isArray(Array.prototype))` same as `Object.prototype.foo = "bar"; let empty = {}; empty.foo === "bar"`
	* ECMAScript proxy: https://github.com/mathiasbynens/tpyo `const array = tpyo(['a', 'b', 'c']);array.lnegth;array.tosTr1ng();`
	- ECMAScript proxy:
		```js
		with (MëtalÜmlauts()) {
			consöle.ërror('Mëtal');
			alërt('Ümlauts');
		}

		function MëtalÜmlauts(){
			const handler = {
				// always pretend the property exists
				has(){
					return true;
				},

				// remplace umlauts in properties
				get(target, name){
					const ascii = String(name).normalize("NFKD").replace(/[\u0300-\u036F]/g, "");
					const property = Reflect.get(target, ascii);
					switch(typeof property){
						case "object":
							return new Proxy(property, handler);
							break;
						case "function":
							return property.bind(target);
							break;
						default:
							return property;
					}
				}
			};

			return new Proxy(window, handler);
		}
		```
	* ECMAScript regexp previous match:

		```js
		"abc".match(/b/);
		console.log(RegExp["$`"]);// a
		console.log(RegExp["$&"]);// b
		console.log(RegExp["$'"]);// c
		console.log("abc".replace("b", "$`"));// aac
		console.log("abc".replace("b", "$&"));// abc
		console.log("abc".re:place("b", "$'"));// acc
		```
	* ECMAScript string template

		```js
		alert`1`				// no parenthesis needed
		Function`alert\`1\````	// escaped back-ticks
		!{[alert`1`]:null}		// back-tick & computed
		+{valueOf() alert`1`}	// method shorthand
		`hello`-alert`1`-`goodbye`	// concatenation
		`hello${alert(1)}goodbye`	// expression interpolation

		Function`$${atob`YWxlcnQoMSk`}```
		/*
		atob`YWxlcnQoMSk`
		// Note: the end "=" padding can be dropped
		// decodes to string to:
		// "alert(1)"

		`$${"alert(1)"}`
		// results in the tag components:
		// ["$", ""], "alert(1)"

		Function(["$", ""], "alert(1)")
		// creates an anonymous function
		// function($,) {alert(1)}
		*/
		```
	* ECMAScript:

		```js
		let x = (() => {
			for (var i = 0; i < 5; i++) {
				try { return i; }
				finally { if (i != 3) continue; }
			}
		})();
		console.log( x ); // -> 3
		```

		- [c# - Why can't a 'continue' statement be inside a 'finally' block? - Stack Overflow](https://stackoverflow.com/questions/17991036/why-cant-a-continue-statement-be-inside-a-finally-block)
	* Esoteric programming language that are subset of a language
		see [JSFuck](#esoteric-programming-languages)
	* closures
	* enumerable
	* write or switch Object prototype
	* ECMAScript (and other language support) destructuring `[a, b] = [b, a]`
	* ECMAScript: redefined global variable, like undefined:
		- (≤ ES4) `undefined = "a"; typeof undefined != "undefined"`
		- in using function parameter `(function(undefined = "a") {typeof undefined != "undefined"})();`
		- `with({undefined: 1}){1 === undefined}`
		- `(() => {var undefined = 1; return 1 === undefined;})()`

		To resolve it, just use: `var trueUndefined = (function(undefined) {return undefined})();` or `var trueUndefined = void(0);`
	* PHP, copy array instead of using it reference. See [Is there a function to make a copy of a PHP array to another? - Stack Overflow](https://stackoverflow.com/questions/1532618/is-there-a-function-to-make-a-copy-of-a-php-array-to-another/1532632#1532632)
	* JS: [DOM clobbering](#dom-clobbering)
	* CSS: escaped char can be followed by space `.\65 lement{}` is same as `.element{}` but not `.e lement{}` (spaces are often used to combine selectors) [Using character escapes in markup and CSS](https://www.w3.org/International/questions/qa-escapes#cssescapes)
	* C, `#define true false`, `#define if(x) if((rand % 10) ? (x) : !(x))`, `#define if(x) if((x) && ( ((double)rand()*10.0 / (double)RAND_MAX) < 1.0))`
	* PHP `$func = 'foo';$func();// This calls foo()`: [PHP: Variable functions - Manual](http://php.net/manual/en/functions.variable-functions.php)
	* HTML: `<a href="#">Link</a href="#">` where the tag name is `a href="#"` where space is EN QUAD (U+2000) [#HTMLQuiz](http://html5te.st/quiz/)
	* [The following code](https://gist.github.com/avafloww/b1143f42883b3b0ee1237bc9bd0b7b2c) is syntactically valid in both PHP and Java:
		```
		/*<?php
		//*/public class PhpJava { public static void main(String[] args) { System.out.printf("/*%s",
		//\u000A\u002F\u002A
		class PhpJava {
		    static function main() {
		        echo(//\u000A\u002A\u002F
		        "Hello World!");
		}}
		//\u000A\u002F\u002A
		PhpJava::main();
		//\u000A\u002A\u002F
		```
	* Math phenomens:
		- `1/99980001 = 1/Math.pow(9999, 2) = 0.00000001000200030004000500060007…9994999599969997999900000001000200030004…` (but without 9998)
		- `1/998001 = 1/Math.pow(999, 2) = 0.000001002003004005006007…994995996997999000001002003004…` (but without 998)
		- `1/9801 = 1/Math.pow(99, 2) = 0.000102030405…9697990001020304…` (sequence from 00 to 99, but without 98)
		- `1/81 = 1/Math.pow(9, 2) = 012345679/999999999 = 0.0123456790123456790123…` (without 8)

		`Math.floor(Math.pow(10, 1 + x)/81) % 10 == x// but doesn't works for all x (x=8 gives 9, x=9 gives 0, x=10 gives 1, etc.)`
		See [998,001 and its Mysterious Recurring Decimals - Numberphile - YouTube](https://www.youtube.com/watch?v=daro6K6mym8&feature=youtu.be&app=desktop)

		```
		12345679*9 = 111111111
		```

		```
		1*8+1=9
		12*8+2=98
		123*8+3=987
		1234*8+4=9876
		12345*8+5=98765
		123456*8+6=987654
		1234567*8+7=9876543
		12345678*8+8=98765432
		123456789*8+9=987654321
		1234567890*8+0=9876543210
		```

	* C `main(){printf(&unix["\021%six\012\0"], (unix)["have"]+"fun"-0x60);}` print `unix` when compiled on unix [`main(){printf(&unix\["\021%six\012\0"\], (unix)["have"]+"fun"-0x60);}` - faehnri.ch](http://faehnri.ch/have-fun/)
	* Auto expand, in HTML `<table><td></td></table>` is parsed as `<HTML><HEAD></HEAD><BODY><TABLE><TBODY><TR><TD></TD></TR></TBODY></TABLE></BODY></HTML>`. See also HTML5 with non closed tags
	* HTML head and its children are not display by default, but can be `head,meta,title,link,script,style,base{display: block !important;min-width: 50px;min-height: 20px;overflow: visible;}`
	* Retro compatibility of ECMAScript RegExps [The madness of parsing real world JavaScript regexps | Hacker Noon](https://web.archive.org/web/20200829130541/https://hackernoon.com/the-madness-of-parsing-real-world-javascript-regexps-d9ee336df983)
	* ActionScript

		```as3
		package {
			import flash.display.*
			import flash.text.*

			public class AprilFools extends Sprite {
				エイプリルフール var Number = 4..toString()

				use namespace エイプリルフール

				function AprilFools()
				{
					get = set
					set = get

					with (createTextField())
					text = new Date(Number).toDateString()
				}

				function get get() { return Number + <><{Number}
					b={"/"+Number.split(/\//)[0]*502.25}/>..@b }
				function set get(set) { Number = set+'/'+set/4 }

				function get set() { return Number }
				function set set(get) { Number = get }

				// nothing fun here
				function createTextField():TextField
				{
					stage.scaleMode = StageScaleMode.NO_SCALE;
					stage.align = StageAlign.TOP_LEFT;
					var textField:TextField = new TextField();
					textField.width = 1000;
					addChild(textField);
					return textField;
				}
			}
		}

		namespace エイプリルフール
		```

		- [mikemo » AprilScript: ActionScript worst practices](http://wayback.archive.org/web/20111029080653/http://www.morearty.com/blog/2009/04/01/aprilscript-actionscript-worst-practices/)
	- Python: [Obfuscating "Hello world!" – Ben Kurtovic](https://benkurtovic.com/2014/06/01/obfuscating-hello-world.html)
	- SQL: [SQL obfuscation](http://wayback.archive.org/web/20120203032738/http://sla.ckers.org/forum/read.php?24,35405)
- Hide you script in commonly used lib (ex: jQuery add special method or option)
- Centraliser le moins possible de méthodes ou objets
- encrypt the program if it's possible, like DRM, but require a full capable and trusted chain (end-to-end)
- remote execution : a part of the program is downloaded at each launch
	* Rendre le moins prévisible le fonctionnement (différentes méthodes, instructions provenant du server). Version de façon unique et "jettable" (méthodes et algorithmes différents)
- Control Flow obfuscation / Dynamic Code wrapping / Statement-Level Randomization
- simple:
	compress (deflate) + XOR with a key `This obfuscation is intended to discourage XXXX from making modifications to the YYYY. We know this 'encryption' is easily broken.`

	- [Orange: \[Bug Bounty\] GitHub Enterprise SQL Injection](http://blog.orange.tw/2017/01/bug-bounty-github-enterprise-sql-injection.html)
	- [decrypt obfuscated GitHub Enterprise .rb files](https://gist.github.com/geoff-codes/02d1e45912253e9ac183)
- Some good advices [How To Write Unmaintainable Code](https://github.com/Droogans/unmaintainable-code)
- SWF obfuscation
	See [SWF obfuscation](SWF#Obfuscation)
- [Gamasutra: Mary Min's Blog - Six Strategies for Protecting Your Mobile Games Against Hackers, Crackers & Copycatters](http://www.gamasutra.com/blogs/MaryMin/20150610/245625/Six_Strategies_for_Protecting_Your_Mobile_Games_Against_Hackers_Crackers__Copycatters.php)
- [Tricherie, piratage, vol de données… Bienvenue dans les jeux Facebook | Roxane](http://www.roxane-company.com/blog/2014/06/05/tricherie-piratage-vols-de-donn%C3%A9es-bienvenue-sur-les-jeux-facebook/)
- [Unbundling Pokémon Go — Applidium](https://applidium.com/en/news/unbundling_pokemon_go/)

See also:

- [ProGuard](http://proguard.sourceforge.net/) (obfuscation for Java)
- [Jscrambler | Make Your JavaScript Application Protect Itself](https://jscrambler.com/fr/) - Commercial solution for JavaScript
- [Obfuscation (software) - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Obfuscation_(software))
- [Previous IOCCC Winners](http://www.ioccc.org/years.html) and [Spoiler summary](http://www.ioccc.org/all/summary.txt)
- [Dissecting a spammer's spam script – Our Technical Narrative](https://jelleraaijmakers.nl/2016/04/dissecting-spammers-spam-script)
- [PHP Code Deobfuscator](https://github.com/technopagan/php-code-deobfuscator) use `ltrace -e memcpy`
- [Cheat Engine :: View topic - [Library] Gamehacking Tools](http://forum.cheatengine.org/viewtopic.php?t=309234)
- [web-obfuscation - Web Application Obfuscation - Google Project Hosting](https://code.google.com/p/web-obfuscation/)
- [hackme: Deconstructing an ELF File](http://manoharvanga.com/hackme/)
- [How I Cracked a Keylogger and Ended Up in Someone's Inbox](https://www.trustwave.com/Resources/SpiderLabs-Blog/How-I-Cracked-a-Keylogger-and-Ended-Up-in-Someone-s-Inbox/)
	.Net keylogger cracked, reveal attacker's email credentials (but all email are forwarded to an other account)
