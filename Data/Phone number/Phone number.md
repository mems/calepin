- [Category:Telephone numbers by country - Wikipedia](https://en.wikipedia.org/wiki/Category:Telephone_numbers_by_country)
- [googlei18n/libphonenumber: Google's common Java, C++ and JavaScript library for parsing, formatting, and validating international phone numbers.](https://github.com/googlei18n/libphonenumber)
- [catamphetamine/libphonenumber-js: A simpler (and smaller) rewrite of Google Android's libphonenumber library](https://github.com/catamphetamine/libphonenumber-js)
- [Long number - Wikipedia](https://en.wikipedia.org/wiki/Long_number)
- [Short code - Wikipedia](https://en.wikipedia.org/wiki/Short_code)

## Format

"tel"						+1 617 253 5702		Full telephone number, including country code
- "tel-country-code"		+1					Country code component of the telephone number
- "tel-national"			617 253 5702		Telephone number without the county code component, with a country-internal prefix applied if applicable
- - "tel-area-code"			617					Area code component of the telephone number, with a country-internal prefix applied if applicable
- - "tel-local"				2535702				Telephone number without the country code and area code components
- - - "tel-local-prefix"	253					First part of the component of the telephone number that follows the area code, when that component is split into two components
- - - "tel-local-suffix"	5702				Second part of the component of the telephone number that follows the area code, when that component is split into two components
"tel-extension"				1000				Telephone number internal extension code

From [HTML Standard](https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#attr-fe-autocomplete-tel)

- [National conventions for writing telephone numbers - Wikipedia](https://en.wikipedia.org/wiki/National_conventions_for_writing_telephone_numbers)
- [RFC 3966 - The tel URI for Telephone Numbers](https://tools.ietf.org/html/rfc3966)
- [RFC 5341 - The Internet Assigned Number Authority (IANA) tel Uniform Resource Identifier (URI) Parameter Registry](https://tools.ietf.org/html/rfc5341)

### Extension

like PBX

Common separators (some time with space around and uppercase): `,` (or `p`; pause), `;` (or `w`; wait for dial tone, some times prompt the user before) or `x`, `ext`, `ext.`

- iOS support `,` and `;` (pause = 1s)
- Android support `,`, `p`, `;` and `w` (not work for `tel:` protocol)
- Windows Phone support `,`, `p`, `w` (pause = 3s or 2s?)

- DTMF tones
- [Extension (telephone) - Wikipedia](https://en.wikipedia.org/wiki/Extension_%28telephone%29)
- [Can't dial phone numbers plus extension. \[36916084\] - Visible to Public - Issue Tracker](https://issuetracker.google.com/issues/36916084)
- [Calling options | Windows Phone How-to (United States)](https://web.archive.org/web/20160513071903/http://www.windowsphone.com/en-us/how-to/wp8/calling-and-messaging/calling-options) - Section "To use wait or pause dialing"
- [contacts - Dialing an extension automatically - Android Enthusiasts Stack Exchange](https://android.stackexchange.com/questions/32337/dialing-an-extension-automatically)
- [How do I dial an extension during a call?](https://support.skype.com/en/faq/fa22/how-do-i-dial-an-extension-during-a-call)
- [Dial phone extension from Contact - Microsoft Community](https://answers.microsoft.com/en-us/mobiledevices/forum/mdlumia-mdsettings/dial-phone-extension-from-contact/7831a526-4f92-4c2e-829e-8f2db0c3c47b)
- [RFC 3966 - The tel URI for Telephone Numbers](https://tools.ietf.org/html/rfc3966#section-5.3)
- [html - How do I include extensions in the tel: URI? - Stack Overflow](https://stackoverflow.com/questions/9482633/how-do-i-include-extensions-in-the-tel-uri)

### Length

15 digits (E.164 imposing a maximum length of 15 digits to telephone numbers) + ponctuation and extensions

- https://stackoverflow.com/questions/14894899/what-is-the-minimum-length-of-a-valid-international-phone-number
- https://en.wikipedia.org/wiki/Telephone_numbering_plan