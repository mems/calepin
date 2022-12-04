- [URI scheme - Wikipedia, the free encyclopedia](http://en.wikipedia.org/wiki/URI_scheme)
- [Uniform Resource Identifier (URI) Schemes](http://www.iana.org/assignments/uri-schemes/uri-schemes.xml)
- [RFC 4395 - Guidelines and Registration Procedures for New URI Schemes](http://tools.ietf.org/html/rfc4395)
- [handleOpenURL, Shared Interapp Communication on iOS](http://handleopenurl.com/)
- [Google Maps URL Scheme   |   Google Maps SDK for iOS   |   Google Developers](https://developers.google.com/maps/documentation/ios/urlscheme)
- [About Apple URL Schemes](https://developer.apple.com/library/ios/featuredarticles/iPhoneURLScheme_Reference/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007891-SW1)
- [christopherdwhite/iosWorkflows: This is a collection of bookmarklets, scripts and custom URL scheme actions that help bridge apps and manipulate the data you can send between them.](https://github.com/christopherdwhite/iosWorkflows)
- [Register protocol handler](../../Web/Websites.md#register-protocol-handler)

See also [URI/URL](../../Web/Web.md#uriurl)

## Mobile Application URL Schemes

iOS and/or Android

- [Open native application](../../Web/Web.md#open-native-application)
- [Fingerprinting - Native application is installed](../../Security/Security.md#native-application-is-installed)

- [IPhone URL Schemes - akosma wiki](https://web.archive.org/web/20161018100533/http://wiki.akosma.com:80/IPhone_URL_Schemes)
- [handleOpenURL, Shared Interapp Communication on iOS](https://web.archive.org/web/20161128234603/http://handleopenurl.com:80/)
- [x-callback-url](http://x-callback-url.com/)
- [URLs | Drafts](https://getdrafts.com/urls/) [Home | Drafts Action Directory](http://drafts4-actions.agiletortoise.com/) http://theaxx.net/actionpage/
- [Iconical](http://iconic.al/urls.html) [‎Iconical on the App Store](https://itunes.apple.com/us/app/iconical/id662522133?mt=8&ign-mpt=uo%3D4) support 80K application scheme
- iHasApp
	- [iHasApp/schemeApps.json at master · danielamitay/iHasApp](https://github.com/danielamitay/iHasApp/blob/master/iHasApp/schemeApps.json)
	- `http://itunes.apple.com/lookup?id=<id>&country=<country>`
	- [danielamitay/iHasApp: The iHasApp iOS Framework allows you to detect installed apps on a user's device.](https://github.com/danielamitay/iHasApp)
	- [HBehrens/collectIPAMetaData: extract and merge meaningful meta data from iOS IPAs such as URL schemes and app store ID](https://github.com/HBehrens/collectIPAMetaData)
- (from `Iconical.ipa`) `Iconical.app/actionapps.data`

## Apple Maps URI

```
x-maps-mapitemhandles://{plist_base64_encoded}
```

Sometimes, iOS keyboard predict a part of calendar event address links

```sh
pbpaste | base64 -d > data.plist
plutil -convert xml1 -o - - < data.plist
```

```
x-maps-mapitemhandles://YnBsaXN0MDDSAQIDBV8QFk1LTWFwSXRlbUxhdW5jaEhhbmRsZXNfECVNS01hcEl0ZW1MYXVuY2hBZGRpdGlvbnNMYXVuY2hPcHRpb25zoQRPENoIARLVAQiuTRDV8Yii35y6gskBGhIJDROymH1xSEAR+GmB4mzfAkAifAoGRnJhbmNlEgJGUhoOw45sZS1kZS1GcmFuY2UqBVBhcmlzMgVQYXJpczoFNzUwMThCC0dvdXR0ZSBkJ09yUg5QYXNzYWdlIFJ1ZWxsZVoBMWIQMSBQYXNzYWdlIFJ1ZWxsZYoBCDE4ZSBhcnIuigELR291dHRlIGQnT3IqDEljZSBLdWJlIEJhcjIQMSBQYXNzYWdlIFJ1ZWxsZTILNzUwMTggUGFyaXMyBkZyYW5jZdIGBwgJXxAtTUtMYXVuY2hPcHRpb25zRnJvbVRpbWVUb0xlYXZlTm90aWZpY2F0aW9uS2V5XxAkTUtMYXVuY2hPcHRpb25zUmVmZXJyYWxJZGVudGlmaWVyS2V5CF8QE2NvbS5hcHBsZS5tb2JpbGVjYWwACAANACYATgBQAS0BMgFiAYkBigAAAAAAAAIBAAAAAAAAAAoAAAAAAAAAAAAAAAAAAAGg
```

```plist
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>MKMapItemLaunchAdditionsLaunchOptions</key>
	<dict>
		<key>MKLaunchOptionsFromTimeToLeaveNotificationKey</key>
		<false/>
		<key>MKLaunchOptionsReferralIdentifierKey</key>
		<string>com.apple.mobilecal</string>
	</dict>
	<key>MKMapItemLaunchHandles</key>
	<array>
		<data>
		CAES1QEIrk0Q1fGIot+cuoLJARoSCQ0Tsph9cUhAEfhpgeJs3wJAInwKBkZy
		YW5jZRICRlIaDsOObGUtZGUtRnJhbmNlKgVQYXJpczIFUGFyaXM6BTc1MDE4
		QgtHb3V0dGUgZCdPclIOUGFzc2FnZSBSdWVsbGVaATFiEDEgUGFzc2FnZSBS
		dWVsbGWKAQgxOGUgYXJyLooBC0dvdXR0ZSBkJ09yKgxJY2UgS3ViZSBCYXIy
		EDEgUGFzc2FnZSBSdWVsbGUyCzc1MDE4IFBhcmlzMgZGcmFuY2U=
		</data>
	</array>
</dict>
</plist>
```

## Tel URI

```
tel:
```

See [Phone number](../../Data/Phone%20number/Phone%20number.md)

```html
<p>Appelez le <a href="tel:+33612345678">06 12 34 56 78</a>.</p>
```

Should support extensions: `tel:+00000;ext=00`, but often only `tel:+00000,00` is supported. See [Phone number](../../Data/Phone%20number/Phone%20number.md#extension)

Chars are composed as number (what about `w`/"wait for dial tone" or `p`/"pause").

- [RFC 3966 - The tel URI for Telephone Numbers](https://tools.ietf.org/html/rfc3966)
- [How to create click-to-call links for mobile browsers | Breaking the Mobile Web](http://www.mobilexweb.com/blog/click-to-call-links-mobile-browsers)
- [URI scheme - Wikipedia, the free encyclopedia](http://en.wikipedia.org/wiki/URI_scheme#tel:)
- [html - How to mark-up phone numbers? - Stack Overflow](https://stackoverflow.com/questions/1164004/how-to-mark-up-phone-numbers)
- [Extension (telephone) - Wikipedia, the free encyclopedia](http://en.wikipedia.org/wiki/Extension_(telephone))
- [html - How do I include extensions in the tel: URI? - Stack Overflow](https://stackoverflow.com/questions/9482633/how-do-i-include-extensions-in-the-tel-uri)

## SMS URI

```
sms:?body=http%3A%2F%2F…
```

## Geo URI

```
geo:{lat},{long}
```

- [The "geo:" URI scheme](http://geouri.org/)

## Mailto

```
mailto:
```

- [mailto - Wikipedia, the free encyclopedia](http://en.wikipedia.org/wiki/Mailto)

## Data URI

```
data:
```

- [RFC 2397 - The "data" URL scheme](http://tools.ietf.org/html/rfc2397)

### Base 64 encoding

Base64 encoding = 5/4 * original data size

To encode:

```sh
recode ../b64 < file.png
base64 < file.png
openssl enc -base64 < file.png | tr -d '\n'
uuencode -m -o /dev/stdout file
# To copy in clipboard on macOS, use:
# command | pbcopy
# Exemple:
# base64 < file.png | pbcopy
```

```sh
function dataurl() {
	local mimeType=$(file -b --mime-type "$1");
	if [[ $mimeType == text/* ]]; then
		mimeType="${mimeType};charset=utf-8";
	fi
	echo "data:${mimeType};base64,$(openssl base64 -in "$1" | tr -d '\n')";
}

# Usage:
dataurl file
```

- [arbitraryco/base64-encode: Base64 Encode is an OSX Service used to encode files to data URIs.](https://github.com/arbitraryco/base64-encode)
- `<?php echo base64_encode(file_get_contents('file.png')) ?>`

To decode:

```sh
echo B64STRING | recode b64/.. > file.png
openssl enc -base64 -d <<< B64STRING
echo B64STRING | base64 -D
```

```sh
openssl enc -base64 -d -A << EOF
B64STRING_LINE1
B64STRING_LINE2
EOF
```

See also [bash - How can I decode a base64 string from the command line? - Ask Ubuntu](https://askubuntu.com/questions/178521/how-can-i-decode-a-base64-string-from-the-command-line)

Or create a Automator Service (MacOSX only) with a shell command `cat "$1" | base64 | pbcopy` or `cat "$@" | base64 | pbcopy` (for concat all provided files)

See also:

- [Base64 - Wikipedia](https://en.wikipedia.org/wiki/Base64)

## Webcal URI

`webcal:`

- [Apple Breaks ICS Calendar Auto-Subscription In iOS 4.2](http://blog.fosketts.net/2011/01/13/apple-breaks-ics-calendar-autosubscription-ios-42/)

## Skype URI

`skype:`

- [Skype Developer - Skype URIs (home)](http://wayback.archive.org/web/20130821013555/http://dev.skype.com/skype-uri)
- [Skype Developer - Reference](http://wayback.archive.org/web/20130928164350/http://dev.skype.com/skype-uri/reference)
