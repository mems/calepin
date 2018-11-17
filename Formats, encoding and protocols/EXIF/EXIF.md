- [Exif — Wikipedia](https://en.wikipedia.org/wiki/Exif)
- jhead [Exif Jpeg header manipulation tool](http://www.sentex.net/~mwandel/jhead/)
- [ExifTool by Phil Harvey](http://www.sno.phy.queensu.ca/~phil/exiftool/)
- [The libexif C EXIF library](http://libexif.sourceforge.net/)
- [Exiv2 - Image metadata library and tools](http://www.exiv2.org/) - A C++ library and a command line utility to easly read and write Exif, IPTC and XMP metadata
- [Exif Viewer :: Add-ons for Firefox](https://addons.mozilla.org/en-US/firefox/addon/exif-viewer/) - see also [Exif Viewer - a Mozilla Firefox/Thunderbird Extension](http://araskin.webs.com/exif/exif.html)
- [exif-js/exif-js- JavaScript library for reading EXIF image metadata](https://github.com/exif-js/exif-js)
- [Jeffrey Friedl's Image Metadata Viewer](http://exif.regex.info/exif.cgi)
- [media/java/android/media/ExifInterface.java - platform/frameworks/base - Git at Google](https://android.googlesource.com/platform/frameworks/base/+/master/media/java/android/media/ExifInterface.java)
- [sephiroth74/Android-Exif-Extended: Exif extended library for Android](https://github.com/sephiroth74/Android-Exif-Extended) - based on jhead
- [mattburns/exiftool.js: A pure javascript implementation of exiftool](https://github.com/mattburns/exiftool.js) - based on ExifTool by Phil Harvey
- [Parsing Exif client-side using JavaScript | code.flickr.com](http://code.flickr.net/2012/06/01/parsing-exif-client-side-using-javascript-2/)

## Orientation

	function getEXIFOrientation (file, callback) {
		var reader = new FileReader()
		reader.onload = e => {
			var view = new DataView(e.target.result)
			if (view.getUint16(0, false) !== 0xFFD8) {
				return callback(-2)
			}
			var length = view.byteLength
			var offset = 2
			while (offset < length) {
				var marker = view.getUint16(offset, false)
				offset += 2
				if (marker === 0xFFE1) {
					if (view.getUint32(offset += 2, false) !== 0x45786966) {
						return callback(-1)
					}
					var little = view.getUint16(offset += 6, false) === 0x4949
					offset += view.getUint32(offset + 4, little)
					var tags = view.getUint16(offset, little)
					offset += 2
					for (var i = 0; i < tags; i++) {
						if (view.getUint16(offset + (i * 12), little) === 0x0112) {
							return callback(view.getUint16(offset + (i * 12) + 8, little))
						}
					}
				} else if ((marker & 0xFF00) !== 0xFF00) {
					break
				} else {
					offset += view.getUint16(offset, false)
				}
			}
			return callback(-1)
		}
		reader.readAsArrayBuffer(file.slice(0, 65536))
	}