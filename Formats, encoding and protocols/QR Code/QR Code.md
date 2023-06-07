Aka QRCode, Quick Response Code

See also:

- [Magnetic ink character recognition — Wikipedia](https://en.wikipedia.org/wiki/Magnetic_ink_character_recognition)
- [QR code — Wikipedia](https://en.wikipedia.org/wiki/QR_code)
- [WTF QR CODES](http://wtfqrcodes.com/)
- [Barcode](../Barcode/Barcode.md)

## Invert QR code colors

Aka light-on-dark QR codes

> You cannot invert QR code colors, dark areas have to stay dark, light areas have to stay light. Also there has to be at least 1 pixel light bounding rectangle around the whole QR code. So if you want to show QR code on dark background it should [draw white background behind QR code]
> [...]
> it just depends on the reader. Some readers are advanced enough to notice the pattern and invert the colors, and some don't do that.
>
> In iOS7, QR codes are now natively detectable through the AVFoundation library which, through testing, picks up inverse QR codes. It scans the image just fine.
>
> — [Inverted QR code is not scannable · Issue #1 · bennyguitar/BTCDonationViewController](https://github.com/bennyguitar/BTCDonationViewController/issues/1)

- [6 reasons why your QR code is not working - QRCode Monkey](https://www.qrcode-monkey.com/6-reasons-why-your-qr-code-is-not-working/)

## Datatypes

See [URI](../URI/URI.md)

- URI: `http:`/`https:`, `mms:`, `sms:` ([RFC 5724 - URI Scheme for GSM Short Message Service](https://tools.ietf.org/html/rfc5724)), `mailto:`, `tel:`, `geo:lat,long,alt`
- vCard
- WiFi access QR codes `WIFI:T:WPA;S:networkname;P:password;;`, `WIFI:S:networkname;T:WEP;P:password;;`, `H:true` https://github.com/zxing/zxing/wiki/Barcode-Contents#wifi-network-config-android https://cweiske.de/tagebuch/wifi-config-qrcode.htm
- iCal?

- [Barcode Contents](./ZXing/zxing.wiki/Barcode-Contents.md), [Barcode Contents · zxing/zxing Wiki](https://github.com/zxing/zxing/wiki/Barcode-Contents)
- [data type supported qrcode - Google Search](https://www.google.com/search?q=data+supported+qrcode&ie=utf-8&oe=utf-8#q=data+type+supported+qrcode)

## Reader

- [Web QR](https://webqr.com/) [Javascript QRCode scanner](https://github.com/LazarSoft/jsqrcode) port of ZXing
- [QR Code Generators Online – 2d-code](http://2d-code.co.uk/qr-code-generators/)

## Generator

- http://phpqrcode.sourceforge.net/
- https://developers.google.com/chart/infographics/docs/qr_codes
- [ZXing ("Zebra Crossing")](https://github.com/zxing/zxing)
- http://chart.googleapis.com/chart?chs=540x540&cht=qr&chld=L|5&chl=URL
- `copy("https://chart.googleapis.com/chart?cht=qr&chs=540x540&chld=L|0&chl=" + encodeURIComponent("https://...."))`
- [High quality QR Code generator library in Java, JavaScript, Python, C++](https://www.nayuki.io/page/qr-code-generator-library)

## With visual

- [Picture to QR code converter](https://www.qrpicture.com/) - [xyzzy/qrpicture: Picture to QR code converter hosted on www.QRpicture.com](https://github.com/xyzzy/qrpicture)
- [How to put your logo in a QR code | Hackaday](http://hackaday.com/2011/08/11/how-to-put-your-logo-in-a-qr-code/)
- [research!rsc: QArt Codes](https://web.archive.org/web/20230531022213/https://research.swtch.com/qart) - see https://code.google.com/archive/p/rsc (download `pubgo.zip `, uncompresse `pubgo/src/code.google.com/p/rsc/qr`) see also [swtch/qrweb at c77682714219669391367b69f970c27c6ffadd1b · rsc/swtch · GitHub](https://github.com/rsc/swtch/tree/c77682714219669391367b69f970c27c6ffadd1b/qrweb), [web package - rsc.io/swtch/qrweb - Go Packages](https://pkg.go.dev/rsc.io/swtch/qrweb)
- [Using generalizations of Kuznetsov-Tsybakov problem for new possibilities of steganography](qrsem.pdf)
- [Generate artistic QR code](https://github.com/kciter/qart.js)
- [Halftone QR Codes](http://vecg.cs.ucl.ac.uk/Projects/SmartGeometry/halftone_QR/halftoneQR_sigga13.html) [Halftone QR Codes Video](./Halftone QR Codes.mov) [hqrc_demo.zip](./hqrc_demo.zip)
- [QArt Python Implementation](https://github.com/7sDream/pyqart)
- [Creative Arabic Calligraphy: Square Kufic](https://design.tutsplus.com/tutorials/creative-arabic-calligraphy-square-kufic--cms-23012)
- [kochrt/qr-designer: QR designer web app with a novel method of designing qr codes that does not take advantage of error correction](https://github.com/kochrt/qr-designer) - [Create a swink - swink](https://web.archive.org/web/20230603221608/https://robko.ch/qr-designer/)
