- [Data URI scheme — Wikipedia](https://en.wikipedia.org/wiki/Data_URI_scheme)
- [Data URIs - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URIs)
- [Base64 encoding and decoding - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/WindowBase64/Base64_encoding_and_decoding#The_Unicode_Problem)
- [StringView - Mozilla | MDN](https://developer.mozilla.org/en-US/Add-ons/Code_snippets/StringView)
- https://github.com/blueimp/JavaScript-Canvas-to-Blob
- https://github.com/beatgammit/base64-js
- https://github.com/dankogai/js-base64

Encode to base64:

`recode ../b64 < file.png`, `base64 -w 0 < file.png`, `openssl enc -base64 < file.png | tr -d '\n'` or `uuencode`. add ` | pbcopy` to copy in clipboard (OSX) or ` > file.b64`

	base64 -w 0 < file.png | pbcopy

	function dataurl() {
		local mimeType=$(file -b --mime-type "$1");
		if [[ $mimeType == text/* ]]; then
			mimeType="${mimeType};charset=utf-8";
		fi
		echo "data:${mimeType};base64,$(openssl base64 -in "$1" | tr -d '\n')";
	}

Decode from base64:

	pbpaste | base64 -d > file.png
