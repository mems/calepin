## Definitions

BCP 74 `fr-CA-u-sd-caqc` with subtags:

1. primary language `fr` (ISO 639-1: French)
2. region subtag `CA` (ISO 3166-1 alpha-2: Canada)
3. extension `U` (Unicode Locale):
	- key `sd` ([Region subdivision](https://github.com/unicode-org/cldr/blob/90aaf561d1827ce06b1e9c4173a70c018665c7d2/common/bcp47/variant.xml#L19-L22))
	- value `caqc` ([Quebec](https://github.com/unicode-org/cldr/blob/90aaf561d1827ce06b1e9c4173a70c018665c7d2/common/subdivisions/ca.xml#L404))

See [IETF language tag - Wikipedia](https://en.wikipedia.org/wiki/IETF_language_tag#Extension_U_%28Unicode_Locale%29) and [Unicode Extensions for BCP 47 - CLDR - Unicode Common Locale Data Repository](http://cldr.unicode.org/index/bcp47-extension)

- [Language localisation — Wikipedia](https://en.wikipedia.org/wiki/Language_localisation)
- [Territory — Wikipedia](https://en.wikipedia.org/wiki/Territory)
- [Region — Wikipedia](https://en.wikipedia.org/wiki/Region)
- [Country — Wikipedia](https://en.wikipedia.org/wiki/Country)
- [Administrative division — Wikipedia](https://en.wikipedia.org/wiki/Administrative_division)
- [Locale - ICU User Guide](http://userguide.icu-project.org/locale)
- [UTS #35: Unicode Locale Data Markup Language](http://www.unicode.org/reports/tr35/#Locale) - What is a Locale?. See Unicode Locale Identifier (ULI)
- [Locale (computer software) — Wikipedia](https://en.wikipedia.org/wiki/Locale_%28computer_software%29)
- Territories (regions) and languages from http://unicode.org/repos/cldr/trunk/common/supplemental/supplementalData.xml (`territoryContainment`):
	- `FR`: France
	- `US`: United States
	- `ZZ`: Unknown region/territory
	- `001`: World
	- `021`: Northern America (group of `BM`, `CA`, `GL`, `PM` and `US`)
	- etc.

	- `fr`: French
	- `und`: Unknown language
- languages from http://www.iana.org/assignments/language-subtag-registry/language-subtag-registry
	- `und`: Undetermined
	- `zxx`: No linguistic content
	- `mis`: Uncoded languages
	- `mul`: Multiple languages

- locale (rules): language + region/area (territory/country, global*) + variant
- territory (country subdivision): a non-sovereign geographic region
- region: area broadly divided by physical characteristics (physical geography), human-impact characteristics (human geography), and the interaction of humanity and the environment (environmental geography)
	Global regions (water and land)
	largest of land regions, known as continents
	largest of water regions known as oceans
- country: a region. A country may be an independent sovereign state
- divisions

- Locale: deals with breaking locale data into components, assembling a locale string from components and displaying the names of countries, languages etc in a specified locale.
- Collator: a means of comparing and sorting strings according to local rules.
- Number formatter: allows you to format numbers in a variety of ways, and to parse textual representations of numbers.
- Date formatter: allows you to format dates and to parse textual representations of dates.
- Message formatter: allows you to compose messages from parameterized strings while formatting the data inside according to local rules and allowing choices dependent on the actual parameter value.
- Normalizer: a means of bringing a Unicode string to a standard, unambiguous representation.
- Grapheme module: handles parsing a string into a set of graphemes.
- IDN: handles internationalized domain names format
- ResourceHandler

Locale tree
- `root` (default)
	* `en` (default English)
		- `en_US`
		- `en_GB`
		- ...
	* `es` (default Spanish)
		- `es_PE` (Spanish, Peru)
		- `es_ES` (Spanish, Spain)
		- `es_ES@currency=EUR` (Spanish, Spain prior to Euro support)

## Infos

- [Describing a Culture with LDML Data](https://msdn.microsoft.com/en-us/library/ms404373%28v=vs.100%29.aspx)
- [iuc34_CLDR.pptx](iuc34_CLDR.pptx)
- [Plural Rules - CLDR - Unicode Common Locale Data Repository](http://cldr.unicode.org/index/cldr-spec/plural-rules)
- [Formatting Messages - ICU User Guide](http://userguide.icu-project.org/formatparse/messages) - translated messages
- Resource bundle - sets of resources that the application can load on locale basis
	- [Java resource bundle — Wikipedia](https://en.wikipedia.org/wiki/Java_resource_bundle)
	- [PHP: ResourceBundle - Manual](http://php.net/manual/en/class.resourcebundle.php)
	- [php - ResourceBundle Editors - Stack Overflow](https://stackoverflow.com/questions/7136799/resourcebundle-editors)
- [php - Localizing strings in Korean dependent on the final consonant of an argument using MessageFormat - Stack Overflow](https://stackoverflow.com/questions/17406638/localizing-strings-in-korean-dependent-on-the-final-consonant-of-an-argument-usi)
- [Standard Numeric Format Strings](https://msdn.microsoft.com/en-us/library/dwhawy9k%28v=vs.110%29.aspx)
- [printf format string — Wikipedia](https://en.wikipedia.org/wiki/Printf_format_string) - to String with type and context `%0:local_number`
- [Tagging text with no language](https://www.w3.org/International/questions/qa-no-language)
- [Language and Locale Matching in Go - The Go Blog](https://blog.golang.org/matchlang) - finding the best match between the languages the application supports and those the user prefers
- [Accept-Language used for locale setting](https://www.w3.org/International/questions/qa-accept-lang-locales)
- [W3C I18N Spec Development Techniques](https://www.w3.org/International/techniques/authoring-html#language) - Checklist about language defined in a web project
- [Translate WordPress](https://make.wordpress.org/polyglots/handbook/)
- [Specifying a Locale — The Dojo Toolkit - Reference Guide](http://dojotoolkit.org/reference-guide/1.10/quickstart/internationalization/specifying-locale.html)
- [Localization Guide — Localization Guide 0.9.0 documentation](http://docs.translatehouse.org/projects/localization-guide/en/latest/index.html)

## Databases

- United Nations Standard country or area codes and geographical - geographical regions, sub-regions, and selected economic and other groupings. Use ISO 3166-1 alpha-3 codes and UN M.49 codes
	- [United Nations Statistics Division- Standard Country and Area Codes Classifications (M49)](https://millenniumindicators.un.org/unsd/methods/m49/m49.htm)
	- [United Nations Statistics Division- Standard Country and Area Codes Classifications (M49)](https://millenniumindicators.un.org/unsd/methods/m49/m49regin.htm) - Composition of macro geographical (continental) regions, geographical sub-regions, and selected economic and other groupings
	- [United Nations Statistics Division- Standard Country and Area Codes Classifications (M49)](https://millenniumindicators.un.org/unsd/methods/m49/m49alpha.htm) - Countries or areas, codes and abbreviations
- Unicode Common Locale Data Repository (CLDR) - Locale rules: date, time format, currency, plurial, etc. Use UN M.49 classification for territories
	- [Common Locale Data Repository — Wikipedia](https://en.wikipedia.org/wiki/Common_Locale_Data_Repository)
	- [CLDR Features - CLDR - Unicode Common Locale Data Repository](http://cldr.unicode.org/cldr-features)
	- [CLDR - Unicode Common Locale Data Repository](http://cldr.unicode.org/)
	- [UTS #35: Unicode Locale Data Markup Language](http://www.unicode.org/reports/tr35/)
	- [cldr - Revision 13270: /trunk/common](http://unicode.org/repos/cldr/trunk/common/)
- International Components for Unicode (ICU) - Use CLDR data + [conversion data (for codepage) and break iterator](http://userguide.icu-project.org/icudata#TOC-ICU-and-CLDR-Data)
	- [International Components for Unicode — Wikipedia](https://en.wikipedia.org/wiki/International_Components_for_Unicode)
- Joda-Time-I18N data
	- [Internationalization data based around Joda-Time](https://github.com/JodaOrg/joda-time-i18n)

Note: Not just translation, localization too, not necessary the same meaning, just text to display to user to provide information

## Codes schemes

- [IETF language tag — Wikipedia](https://en.wikipedia.org/wiki/IETF_language_tag) - language codes + country codes. Allow different schemes to define languages and countries codes
- UN M.49
	- [UN M.49 — Wikipedia](https://en.wikipedia.org/wiki/UN_M.49)

	See also:

	- [ISO 3166-1 numeric — Wikipedia](https://en.wikipedia.org/wiki/ISO_3166-1_numeric)
- ISO 3166 - codes for the names of countries, dependent territories, special areas of geographical interest, and their principal subdivisions (e.g., provinces or states)
	- [ISO - Publications and e-products](http://www.iso.org/iso/home/store/publication_item.htm?pid=PUB500001%3aen) - list of contries
	- [ISO 3166 — Wikipedia](https://en.wikipedia.org/wiki/ISO_3166)
	- [Online Browsing Platform (OBP)](https://www.iso.org/obp/ui/#search)

	See also:

	- [ISO 3166-1 alpha-2 — Wikipedia](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) - two-letter country codes
	- [ISO 3166-1 alpha-3 — Wikipedia](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3) - three-letter country codes
- [ISO 639 — Wikipedia](https://en.wikipedia.org/wiki/ISO_639) - Language and language groups
- [ISO 4217 — Wikipedia](https://en.wikipedia.org/wiki/ISO_4217) - currency and funds codes

	Region

	Commonwealth of Independent States:
	am=cis
	az=cis
	kg=cis
	kz=cis
	md=cis
	tj=cis
	tm=cis
	uz=cis
	ge=cis

	Middle East:
	dz=middle_east
	bh=middle_east
	td=middle_east
	km=middle_east
	dj=middle_east
	er=middle_east
	iq=middle_east
	jo=middle_east
	kw=middle_east
	lb=middle_east
	ly=middle_east
	mr=middle_east
	ma=middle_east
	om=middle_east
	ps=middle_east
	qa=middle_east
	sa=middle_east
	so=middle_east
	sd=middle_east
	ss=middle_east
	sy=middle_east
	tn=middle_east
	ae=middle_east
	ye=middle_east

	Latin America:
	cl=latin_america
	do=latin_america
	ni=latin_america
	uy=latin_america
	co=latin_america
	pe=latin_america
	ve=latin_america
	ec=latin_america
	gt=latin_america
	cu=latin_america
	bo=latin_america
	hn=latin_america
	py=latin_america
	sv=latin_america
	cr=latin_america
	pa=latin_america
	gq=latin_america
	pr=latin_america

	country codes to language names:
	bg=bg
	br=pt-BR
	by=be
	cz=cs
	de=de
	es=es-ES
	fr=fr
	hu=hu
	id=id
	it=it
	jp=ja
	no=nb
	pl=pl
	ro=ro
	rs=sr
	sk=sk
	tr=tr
	ua=uk
	cn=zh-cn
