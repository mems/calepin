- [EXIF specification](http://exif.org/Exif2-2.PDF)
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
- [Parsing Exif client-side using JavaScript | code.flickr.com](https://web.archive.org/web/20200922015317/https://code.flickr.net/2012/06/01/parsing-exif-client-side-using-javascript-2/)
- [Exif Orientation Page](https://web.archive.org/web/20200217001108/http://jpegclub.org/exif_orientation.html)
- [JPEG Orientation – magnushoff.com](https://web.archive.org/web/20201101172023/https://magnushoff.com/articles/jpeg-orientation/)
- [ImpulseAdventure - JPEG / Exif Orientation and Rotation](https://web.archive.org/web/20201029073959/https://www.impulseadventure.com/photo/exif-orientation.html)
- [EXIF Orientation Flag Values](https://web.archive.org/web/20190717053402/https://www.impulseadventure.com/photo/images/orient_flag.gif)
- https://github.com/php/php-src/blob/c5401854fcea27ff9aabfd0682ff4d81bbb3c888/ext/exif/exif.c

## Orientation

```js

/**
 * Get EXIF orientation
 * @param {Blob} file
 * @returns '1' means upper left, '3' lower right, '6' upper right, '8' lower left, '9' undefined; '-1' orientation missing, '-2' not JPEG
 */
export default async function(file) {
	const buffer = await file.arrayBuffer();

	const view = new DataView(buffer);
	if (view.getUint16(0, false) !== 0xFFD8) {
		return -2;
	}

	let offset = 2;
	while (offset < view.byteLength) {
		const marker = view.getUint16(offset, false);
		offset += 2;

		// APP1, Application Segment 1 (metadata)
		if (marker === 0xFFE1) {
			// Not an EXIF header (skip APP1 Data Size)
			if (view.getUint32(offset += 2, false) !== 0x45786966) {
				return -1;
			}

			const little = view.getUint16(offset += 6, false) === 0x4949;// check endianness with TIFF header (skip Exif Header)
			offset += view.getUint32(offset + 4, little);
			const tags = view.getUint16(offset, little);
			offset += 2;
			// Search in IFD0 tags
			for (const i = 0; i < tags; i++) {
				// If IFD0 tag Orientation (0x0112)
				if (view.getUint16(offset + (i * 12), little) === 0x0112) {
					return view.getUint16(offset + (i * 12) + 8, little);
				}
			}
		}
		// Not a marker?
		else if ((marker & 0xFF00) !== 0xFF00) {
			break;
		}
		// Skip that marker
		else {
			offset += view.getUint16(offset, false);
		}
	}

	return -1;
}
```
