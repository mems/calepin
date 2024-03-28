File format, identification:

- [File Format Identification - ForensicsWiki](https://web.archive.org/web/20190910074620/www.forensicswiki.org/wiki/File_Format_Identification) - tools, libs, how to identify file types by content
- [File format — Wikipedia](https://en.wikipedia.org/wiki/File_format)
- [Type code — Wikipedia](https://en.wikipedia.org/wiki/Type_code) - replaced by [Uniform Type Identifier — Wikipedia](https://en.wikipedia.org/wiki/Uniform_Type_Identifier). See [System-Declared Uniform Type Identifiers](https://developer.apple.com/library/prerelease/content/documentation/Miscellaneous/Reference/UTIRef/Articles/System-DeclaredUniformTypeIdentifiers.html)

Infos, tools and code for some formats / protocols / encodings

- [Sustainability of Digital Formats: Planning for Library of Congress Collections](https://www.loc.gov/preservation/digital/formats/index.html)
- [Comparison of data serialization formats — Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_data_serialization_formats)
- [Formats/binary posters](https://github.com/corkami/pics#binary-posters) see also https://github.com/Invoke-IR/ForensicPosters
- [ForensicsWiki](https://web.archive.org/web/20190921172115/http://www.forensicswiki.org/wiki/Main_Page)
- [File Formats - Just Solve the File Format Problem](https://web.archive.org/web/20201126134021/http://fileformats.archiveteam.org/wiki/File_Formats)
- [www.FOURCC.org - Video Codecs and Pixel Formats](http://fourcc.org/)
- [MediaInfo / Code / \[r6865\] /MediaInfoLib/trunk/Source/MediaInfo](https://sourceforge.net/p/mediainfo/code/HEAD/tree/MediaInfoLib/trunk/Source/MediaInfo/)
- [MultimediaWiki](https://wiki.multimedia.cx/index.php/Main_Page)
- [XentaxWiki - Game File Format Central](http://wiki.xentax.com/index.php/Game_File_Format_Central)
- [Category:File Formats - GTAModding](https://www.gtamodding.com/wiki/Category:File_Formats)
- [File Formats - Coding - GTAForums](http://gtaforums.com/topic/267196-file-formats/)
- [List of file formats — Wikipedia](https://en.wikipedia.org/wiki/List_of_file_formats)
- [Why are the Microsoft Office file formats so complicated? (And some workarounds) – Joel on Software](https://www.joelonsoftware.com/2008/02/19/why-are-the-microsoft-office-file-formats-so-complicated-and-some-workarounds/)

- [FileOptimizer (English) - Software Javier Gutiérrez Chamorro (Guti): FileOptimizer, SumatraPDFOpt, TBClamAV, ClamAVOpt, RealSpeed, RLE64, WinVer, TXT2PDF, Lamark, XPlorer, SMETAR, MEMTRACE, ZEROFILL](http://nikkhokkho.sourceforge.net/static.php?page=FileOptimizer)
- [HaxeFoundation/format: Various files formats support for Haxe](https://github.com/HaxeFoundation/format) ZIP, SWF, TGA, WAV, JPEG, MP3, PDF, etc. reader and/or writer (with inflate, deflate, md5, crc32, alder, etc.)

File/data format Posters:

- [Carl Mehner's Album archive - Crypto Posters](https://get.google.com/albumarchive/115606090533118002214/album/AF1QipPRSwyqvMc1r-P58D3SB-A-LZicrov7W-NAv9Oe)
- [Carl Mehner's Album archive - updated posters](https://get.google.com/albumarchive/115606090533118002214/album/AF1QipNYOqtdUaRoWFj8a3Wa8LtNvIqedSuJzjA12Bkm)
- [Carl Mehner's Album archive - PKI Posters](https://get.google.com/albumarchive/115606090533118002214/album/AF1QipPkL9j0DZVCAba62WZugu7d_oWeX2lhCVpHsF4G)
- [PGP Poster - cem](https://www.cem.me/20150621-pgp-poster.html)
- [Certificate Binary Posters (Part One)](https://www.cem.me/20141221-cert-binaries.html)
- [cem Cert Binary Poster 2](https://www.cem.me/20150104-cert-binaries-2.html)
- [Crypto Posters 3 - cem](https://www.cem.me/20150121-cert-binaries-3.html)
- [x.509 Poster - cem](https://www.cem.me/20150209-cert-binaries-4.html)
- [pkcs#7 Poster - cem](https://www.cem.me/20150301-cert-binaries-5.html)
- [Keystore Posters - cem](https://www.cem.me/20150315-cert-binaries-6.html)
- [Revocation Posters - cem](https://www.cem.me/20150401-cert-binaries-7.html)

Games files:

- [Game Extractor download | SourceForge.net](https://sourceforge.net/projects/gameextractor/)
- Cities XL [MCPKUtil](https://sourceforge.net/p/mcpkutil/wiki/Home/) [Cities XL PakUnPak](http://wayback.archive.org/web/20141219223446/http://www.generation-city.com/citiesxl/pakunpak/Download.php) http://xlnation.city/resources/pakunpak-for-cities-x-xl.1900/ (need .NET Framework 4.0, can be decompiled, works with wine + winetrick dotnet40)
- [magcius/noclip.website: A digital museum of video game levels](https://github.com/magcius/noclip.website)

## Describe binary format

Tables likes:

> RECORDHEADER (long):
>
> | Field               | Type | Comment                                                         |
> |---------------------|------|-----------------------------------------------------------------|
> | TagCodeAndLength    | UI16 | Tag type and length of 0x3F Packed together as in short  header |
> | Length              | UI32 | Length of tag                                                   |
>
> [...]
>
> | Field                     | Type         | Comment                  |
> |---------------------------|--------------|--------------------------|
> | Header                    | RECORDHEADER | Tag type = 4             |
> | CharacterId               | UI16         | ID of character to place |
> | Depth                     | UI16         | Depth of character       |
> | Matrix                    | MATRIX       | Transform matrix data    |
> | ColorTransform (optional) | CXFORM       | Color transform data     |
>
> — [SWF File Format Specification](https://www.adobe.com/content/dam/acom/en/devnet/pdf/swf-file-format-spec.pdf)

[struct (C)](https://en.wikipedia.org/wiki/Struct_%28C_programming_language%29):

```c
uint32 constant00;
uint32 numBones;
struct Bone {
	float[16] Matrix4X4;
}
uint32 numVerts
struct Vert {
	float[3] CoordXYZ;
	float Weight;
	byte BoneID01;
	byte BoneID02;
	byte NULL1;
	byte NULL2;
	float[3] NormalXYZ;
	float[2] TexCoordUV;
}

uint32 numFaces;
numFaces Face {
	uint16[3] v1, v2, v3;
}
```

[Kaitai Struct](http://kaitai.io/):

```
meta:
  id: gif
  file-extension: gif
  endian: le
seq:
  - id: header
    type: header
  - id: logical_screen
    type: logical_screen
types:
  header:
    seq:
      - id: magic
        contents: 'GIF'
      - id: version
        size: 3
  logical_screen:
    seq:
      - id: image_width
        type: u2
      - id: image_height
        type: u2
      - id: flags
        type: u1
      - id: bg_color_index
        type: u1
      - id: pixel_aspect_ratio
        type: u1
```

- [File Format Gallery for Kaitai Struct](http://formats.kaitai.io/)
- [kaitai-io/kaitai_struct_formats: Kaitai Struct: library of binary file formats (.ksy)](https://github.com/kaitai-io/kaitai_struct_formats)
- [kaitai-io/kaitai_struct: Kaitai Struct: declarative language to generate binary data parsers in C++ / C# / Go / Java / JavaScript / Lua / Nim / Perl / PHP / Python / Ruby](https://github.com/kaitai-io/kaitai_struct)
- [KOLANICH/synalysis2kaitai: Work in progress, it's not finished.](https://github.com/KOLANICH/synalysis2kaitai)

Synalyze It Grammar:

- [The Grammar Page of Synalyze It!](https://www.synalysis.net/formats.xml)
- [synalysis/Grammars: Grammars for Synalyze It! and Hexinator](https://github.com/synalysis/Grammars/)

See also

- [BFF: A grammar for Binary File Formats](http://www.iwriteiam.nl/Ha_BFF.html)
- [Binary Format — WebAssembly 1.0](https://webassembly.github.io/spec/core/binary/index.html)
- [FlatBuffers: Writing a schema](https://google.github.io/flatbuffers/md__schemas.html)
- [Protocol Buffers  |  Google Developers](https://developers.google.com/protocol-buffers/)
- [Parsing Binary Files - antlr/antlr4](https://github.com/antlr/antlr4/blob/master/doc/parsing-binary-files.md)
- [General binary file parser — bin-parser latest documentation](https://bin-parser.readthedocs.io/en/latest/index.html)

## File signature

- [List of file signatures — Wikipedia](https://en.wikipedia.org/wiki/List_of_file_signatures)
- [Magic number (programming) — Wikipedia](https://en.wikipedia.org/wiki/Magic_number_%28programming%29)
- Binary File Format [BFF: A grammar for Binary File Formats](http://www.iwriteiam.nl/Ha_BFF.html) a form of extended BNF to describe binary file format
- [binfmt_misc — Wikipedia](https://en.wikipedia.org/wiki/Binfmt_misc) (Linux kernel) allows arbitrary executable file formats to be recognized

010 editor template (look similar to structure definitions in C/C++)

- https://github.com/d0c-s4vage/py010parser
- [github 010 templates - Google Search](https://www.google.com/search?q=github+010+templates)
- [010 Editor - Binary Templates - Parsing Binary Files](http://www.sweetscape.com/010editor/templates.html)
- [010 Editor - Binary Template Repository - Download Binary Templates](http://www.sweetscape.com/010editor/repository/templates/)

TrID and TrIDScan:

- [Marco Pontello's Home - Software - TrID](http://mark0.net/soft-trid-e.html)
- [file format specification for TrID definitions packages (TRD and TRS)?](http://mark0.net/forum/index.php?topic=639.0) (standard serialization of a .NET structure; signed int(16) little endian + chars)
- [Marco Pontello's Home - Software - TrIDScan](http://mark0.net/soft-tridscan-e.html)

Magic File:

- `/usr/share/magic` (database used by `magic(5)`)
- [The Fine Free File Command](https://www.darwinsys.com/file/)
- [file(1) command sources](https://github.com/file/file) - see https://github.com/file/file/tree/master/magic/Magdir
- [file(1): determine file type - Linux man page](https://linuxdienet/man/1/file)
- [mod_mime_magic - Apache HTTP Server Version 24](https://httpdapacheorg/docs/24/en/mod/mod_mime_magichtml#format)
- [net/base/mime_sniffer.cc - chromium/src.git - Git at Google](https://chromium.googlesource.com/chromium/src.git/+/master/net/base/mime_sniffer.cc)

[Tcl language](https://www.tcl.tk/) based definition:

- Hex Fiend
	- [HexFiend/templates at master · ridiculousfish/HexFiend](https://github.com/ridiculousfish/HexFiend/tree/master/templates)
	- [HexFiend/HFTclTemplateController.m](https://github.com/ridiculousfish/HexFiend/blob/master/app/sources/HFTclTemplateController.m)
- WinHex & X-Ways Forensics Templates
	- `*.tpl`
	- [WinHex: Template Editing](http://www.x-ways.net/winhex/templates.html)
	- [Additional Templates for WinHex & X-Ways Forensics](https://web.archive.org/web/20200216205414/http://www.x-ways.net/winhex/templates/)
	- https://www.x-ways.net/winhex/manual.pdf
	- http://www.x-ways.net/winhex/templates/tutorial.zip

## Media type

Aka MIME type / Mimetype (terme used for email "MIME - Multipurpose Internet Mail Extensions" specs), content type

By default `application/octet-stream` (`application/force-download` doesn't exist, fallback to the default)

- [Media type — Wikipedia](https://en.wikipedia.org/wiki/Media_type)
- [MIME — Wikipedia](https://en.wikipedia.org/wiki/MIME)
- [MIME types - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types)
- [Shared MIME-info Database](https://developer.gnome.org/shared-mime-info-spec/)
- [How to Register a Media Type for a W3C Specification](https://www.w3.org/2002/06/registering-mediatype2014.html)
- [Default applications - ArchWiki](https://wiki.archlinux.org/index.php/default_applications)
- [MimeTypesSupport - Debian Wiki](https://wiki.debian.org/MimeTypesSupport)
- [mime types - List of ALL MimeTypes on the Planet, mapped to File Extensions? - Stack Overflow](https://stackoverflow.com/questions/1735659/list-of-all-mimetypes-on-the-planet-mapped-to-file-extensions)
- [shared-mime-info-spec](https://www.freedesktop.org/wiki/Specifications/shared-mime-info-spec/) https://cgit.freedesktop.org/xdg/shared-mime-info/plain/HACKING
- [Manual:MIME type detection - MediaWiki](https://www.mediawiki.org/wiki/Manual:MIME_type_detection)
- WebP is not registered, but `image/webp` is used instead of `image/x-webp` [886 - Not an IANA standard - webm - Monorail](https://bugs.chromium.org/p/webm/issues/detail?id=886)
	> Add the WebP and webfont media types (that have not been registered by the same WHATWG idiots who regularly complain about servers not being configured correctly for mime types).
	— [\[Apache-SVN\] Revision 1085522](http://svn.apache.org/viewvc?view=revision&revision=1085522), [\[Apache-SVN\] Revision 1085507](http://svn.apache.org/viewvc?view=revision&revision=1085507)
- APNG is not registered. Mozilla specify to use `image/apng`. `image/png` can still be used, APNG still a PNG, but with (non specified by PNG specification) chunks.
	- Others media types (doesn't means it's valid): `image/mng`, `image/x-ang`, `image/x-apng`, `image/vnd.mozilla.apng`, `video/vnd.mozilla.apng`
	- [APNG Specification - MozillaWiki](https://wiki.mozilla.org/APNG_Specification#MIME_type)
	- [1160200 - Add image/apng MIME type so it can be used with `picture` type switching.](https://bugzilla.mozilla.org/show_bug.cgi?id=1160200)

- [RFC 6838 - Media Type Specifications and Registration Procedures](https://tools.ietf.org/html/rfc6838#section-5)
- [RFC 4289 - Multipurpose Internet Mail Extensions (MIME) Part Four: Registration Procedures](https://tools.ietf.org/html/rfc4289)

Sources:

- [Media Types list maintained by IANA](http://www.iana.org/assignments/media-types/media-types.xhtml)
- https://github.com/mime-types/mime-types-data
- Types used by MediaWiki [mime.types · mediawiki](https://phabricator.wikimedia.org/diffusion/MW/browse/master/includes/libs/mime/mime.types)
- List of types proposed by the W3C [How to Register a Media Type for a W3C Specification](https://www.w3.org/2002/06/registering-mediatype2014.html#RegStatus)
- https://gerrit.googlesource.com/gerrit/+/master/gerrit-server/src/main/resources/com/google/gerrit/server/mime/mime-types.properties
- [Apache common media types](http://svn.apache.org/repos/asf/httpd/httpd/trunk/docs/conf/mime.types) http://svn.apache.org/viewvc/httpd/httpd/trunk/docs/conf/mime.types?view=markup
- https://github.com/liluo/mime/tree/master/mime/types
- List of blocklisted types by MediaWiki [Manual talk:$wgMimeTypeBlacklist - MediaWiki](https://www.mediawiki.org/wiki/Manual_talk:$wgMimeTypeBlacklist#Default_changed_in_1.17)
- https://github.com/mime-types/mime-types-data
- [nginx media types](http://hg.nginx.org/nginx/raw-file/default/conf/mime.types)
- [python media types](https://github.com/python/cpython/blob/master/Lib/mimetypes.py)
- [Complete list of MIME types - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Complete_list_of_MIME_types)
- [Media Type overview with IANA, Apache, Wikipedia data from Bjoern Hoehrmann on 2011-11-29 (www-archive@w3.org from November 2011)](https://lists.w3.org/Archives/Public/www-archive/2011Nov/0079.html)
- [Mimetypes](http://wayback.archive.org/web/20140709234708/http://www.ltsw.se/knbase/internet/mime.htp)
- JavaScript list of media types [HTML Standard](https://html.spec.whatwg.org/#javascript-mime-type)
- [Mime types | Schemaphic Systems Blog](https://deepanjandas.wordpress.com/2010/06/07/mime-types/)
- [jshttp/mime-db: Media Type Database](https://github.com/jshttp/mime-db) (from iana, apache and ngnix)
- [The Filename Extension Database](https://datatypes.net/)
- see `!:mime` in https://github.com/file/file/tree/master/magic/Magdir using format [magic(5): file command's magic pattern file - Linux man page](https://linux.die.net/man/5/magic)

> The use of `text/` for interpreted languages (scripts) is discouraged already by IETF and things like javascript/ecmascript are already migrated to `application/*`, the legacy `text/*` definitions being deprecated.
> - [RFC 4329 - Scripting Media Types](https://tools.ietf.org/html/rfc4329#section-3) and [RFC 4329 - Scripting Media Types](http://tools.ietf.org/html/rfc4329#section-7)

Note: Fonts have now a dedicated type [`font`](http://www.iana.org/assignments/media-types/media-types.xhtml#font).
Instead of using `application/x-font-truetype-collection`, use `font/collection`

Script type:

- Bash: `text/x-shellscript`
- Java: `text/x-java-source`
- C: `text/x-c`, `text/x-csrc`
- C++: `text/x-c++`, `text/x-c++src`
- Python: `text/x-python`

Native executable:

- `application/x-msdownload; format=pe32`
- `application/x-msdownload;format=pe`
- `application/x-dosexec`
- `application/exe`
- `application/x-exe`
- `application/dos-exe`
- `vms/exe`
- `application/x-winexe`
- `application/msdos-windows`
- `application/x-msdos-program`

Audio & video types:

- WebM `.webm`, `video/webm` (video with optional audio), `audio/webm` (audio only)
	Examples:

	- `video/webm; codecs=vp8`
	- `video/webm; codecs=av01.0.08M.08.0.110.01.01.01.1`

	Video codecs:

	- VP8: `vp8` `vp8.0`
	- VP8: `vp9` `vp9.0`

	Audio codecs:

	- Vorbis: `vorbis`
	- Opus: `opus`
- Ogg `.ogg`, `.ogv`, `video/ogg` (video with optional audio), `audio/ogg` (audio only)
	Examples:

	- `audio/ogg`
	- `video/ogg`

	Video codecs:

	- Theora `theora`

	Audio codecs:

	- Vorbis `vorbis`
- MPEG `audio/mpeg`
	Examples:

	- `audio/mpeg; codecs="mp3"`

	Audio codecs:

	- MP1 `mp1`
	- MP2 `mp2`
	- MP3 `mp3`
- MP4 `.mp4`, `.m4a` (audio only), `video/mp4` (video with optional audio), `audio/mp4` (audio only), `application/ogg` (unspecified content)
	Examples:

	- `video/mp4; codecs="avc1.42E01E"`
	- `video/mp4; codecs="avc1.4D401E, mp4a.40.2"`
	- `audio/mp4; codecs="mp4a.40.2"`

	Video codecs:

	- H.264 Baseline (main and extended video compatible): `avc1.42E0xx`, where `xx` is the AVC level (ex: level 3 = `1E`)
	- H.264 Main: `avc1.4D40xx`, where `xx` is the AVC level (ex: level 3 = `1E`)
	- H.264 Extended profile (baseline-compatible): `avc1.58A0xx`, where `xx` is the AVC level (ex: level 3 = `1E`)
	- H.264 High: `avc1.6400xx`, where `xx` is the AVC level (ex: level 3 = `1E`)
	- MPEG-4 Visual Simple Profile Level 0: `mp4v.20.9`
	- MPEG-4 Visual Advanced Simple Profile Level 0: `mp4v.20.240`

	Audio codecs:

	- Low-Complexity AAC: `mp4a.40.2`
- RAW AAC `.aac` `audio/aac` (no MP4 container)
- HLS `application/x-mpegURL; codecs="avc1.42E01E"`

- [encoding - What audio formats and codecs are used for YouTube videos? - Sound Design Stack Exchange](https://sound.stackexchange.com/questions/39175/what-audio-formats-and-codecs-are-used-for-youtube-videos/39176#39176)
- [Web video codec guide - Web media technologies | MDN](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/Video_codecs)
- [The "codecs" parameter in common media types - Web media technologies | MDN](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/codecs_parameter)
- [ffmpeg - What is the difference between M4A and AAC Audio Files? - Stack Overflow](https://stackoverflow.com/questions/18110399/what-is-the-difference-between-m4a-and-aac-audio-files/18111039#18111039)
- [Video type parameters - WHATWG Wiki](https://wiki.whatwg.org/wiki/Video_type_parameters)
- [html5 video tag codecs attribute - Stack Overflow](https://stackoverflow.com/questions/16363167/html5-video-tag-codecs-attribute)
- [Media type - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Media_type)
- [RFC 2231 - MIME Parameter Value and Encoded Word Extensions: Character Sets, Languages, and Continuations](https://tools.ietf.org/html/rfc2231)
- [RFC 6381 - The 'Codecs' and 'Profiles' Parameters for "Bucket" Media Types](https://tools.ietf.org/html/rfc6381)
- [Getting the correct HTML codecs parameter for an AV1 video - JakeArchibald.com](https://web.archive.org/web/20221219225421/https://jakearchibald.com/2022/html-codecs-parameter-for-av1/)

- `audio/opus`
- `.m4b`
- `.mp4v`
- `.3gp`
- `.3g2`
- `audio/mp3`
- `audio/MPA`
- `audio/mpa-robust`
- `audio/x-m4a`
- `audio/MP4A-LATM`
- `audio/mpeg4-generic`
- `audio/wav; codecs="1"`
- `audio/wav`
- `audio/wave` (official)
- `audio/x-wav`
- `audio/x-pn-wav`
- `audio/flac` (preferred)
- `audio/x-flac`
- `.mkv`
- `video/x-matroska`
- `video/x-matroska; codecs="theora, vorbis"`

`/etc/mime.types`:

```
# audio
audio/ogg oga ogg

# video
video/ogg ogv
video/mp4 mp4
video/webm webm

# SVG
image/svg+xml svg svgz

# webfonts
application/vnd.ms-fontobject eot
font/truetype ttf
font/opentype otf
font/woff woff
font/woff2 woff2

# assorted types
image/vnd.microsoft.icon ico
image/webp webp
text/cache-manifest manifest
text/x-component htc
application/x-chrome-extension crx
application/x-xpinstall xpi
application/octet-stream safariextz

text/plain md markdown mdown txt

audio/ogg oga
audio/x-wav wav
application/ogg ogg
#application/x-javascript js
#application/ecmascript js
#application/javascript js
#text/ecmascript js
text/javascript js
application/xhtml+xml xhtml xht
image/gif gif
image/png png
image/jpeg jpg jpeg
image/svg+xml svg
text/css css
text/html html htm
text/xml xml
video/ogg ogv

text/h323	323
video/3gpp2	3g2
video/3gpp2	3gp2
video/3gpp	3gp
video/3gpp	3gpp
audio/aac	aac
application/octet-stream	aaf
application/octet-stream	aca
application/msaccess	accdb
application/msaccess	accde
application/msaccess	accdt
application/internet-property-stream	acx
audio/vnd.dlna.adts	adt
audio/vnd.dlna.adts	adts
application/octet-stream	afm
application/postscript	ai
audio/x-aiff	aif
audio/aiff	aifc
audio/aiff	aiff
text/cache-manifest	appcache
application/x-ms-application	application
image/x-jg	art
application/octet-stream	asd
video/x-ms-asf	asf
application/octet-stream	asi
text/plain	asm
video/x-ms-asf	asr
video/x-ms-asf	asx
application/atom+xml	atom
audio/basic	au
video/msvideo	avi
application/olescript	axs
text/plain	bas
application/x-bcpio	bcpio
application/octet-stream	bin
image/bmp	bmp
text/plain	c
application/vnd.ms-cab-compressed	cab
application/vnd.ms-office.calx	calx
application/vnd.ms-pki.seccat	cat
application/x-cdf	cdf
application/octet-stream	chm
application/x-java-applet	class
application/x-msclip	clp
image/x-cmx	cmx
text/plain	cnf
image/cis-cod	cod
application/x-cpio	cpio
text/plain	cpp
application/x-mscardfile	crd
application/pkix-crl	crl
application/x-x509-ca-cert	crt
application/x-csh	csh
text/css	css
application/octet-stream	csv
application/octet-stream	cur
application/x-director	dcr
application/octet-stream	deploy
application/x-x509-ca-cert	der
image/bmp	dib
application/x-director	dir
text/xml	disco
application/x-msdownload	dll
text/xml	dll.config
text/dlm	dlm
application/msword	doc
application/vnd.ms-word.document.macroEnabled.12	docm
application/vnd.openxmlformats-officedocument.wordprocessingml.document	docx
application/msword	dot
application/vnd.ms-word.template.macroEnabled.12	dotm
application/vnd.openxmlformats-officedocument.wordprocessingml.template	dotx
application/octet-stream	dsp
text/xml	dtd
application/x-dvi	dvi
video/x-ms-dvr	dvr-ms
drawing/x-dwf	dwf
application/octet-stream	dwp
application/x-director	dxr
message/rfc822	eml
application/octet-stream	emz
application/vnd.ms-fontobject	eot
application/postscript	eps
text/x-setext	etx
application/envoy	evy
application/octet-stream	exe
text/xml	exe.config
application/vnd.fdf	fdf
application/fractals	fif
application/octet-stream	fla
x-world/x-vrml	flr
video/x-flv	flv
image/gif	gif
application/x-gtar	gtar
application/x-gzip	gz
text/plain	h
application/x-hdf	hdf
text/x-hdml	hdml
application/x-oleobject	hhc
application/octet-stream	hhk
application/octet-stream	hhp
application/winhlp	hlp
application/mac-binhex40	hqx
application/hta	hta
text/x-component	htc
text/html	htm
text/html	html
text/webviewhtml	htt
text/html	hxt
image/x-icon	ico
text/calendar	ics
image/ief	ief
application/x-iphone	iii
application/octet-stream	inf
application/x-internet-signup	ins
application/x-internet-signup	isp
video/x-ivf	IVF
application/java-archive	jar
application/octet-stream	java
application/liquidmotion	jck
application/liquidmotion	jcz
image/pjpeg	jfif
application/octet-stream	jpb
image/jpeg	jpe
image/jpeg	jpeg
image/jpeg	jpg
#application/javascript	js
text/javascript	js
application/json	json
application/ld+json	jsonld
text/jscript	jsx
application/x-latex	latex
text/css	less
application/x-ms-reader	lit
application/octet-stream	lpk
video/x-la-asf	lsf
video/x-la-asf	lsx
application/octet-stream	lzh
application/x-msmediaview	m13
application/x-msmediaview	m14
video/mpeg	m1v
video/vnd.dlna.mpeg-tts	m2ts
audio/x-mpegurl	m3u
audio/mp4	m4a
video/mp4	m4v
application/x-troff-man	man
application/x-ms-manifest	manifest
text/plain	map
application/x-msaccess	mdb
application/octet-stream	mdp
application/x-troff-me	me
message/rfc822	mht
message/rfc822	mhtml
audio/mid	mid
audio/mid	midi
audio/mid	smf
application/octet-stream	mix
# SMAF audio
application/x-smaf	mmf
text/xml	mno
application/x-msmoney	mny
video/quicktime	mov
video/x-sgi-movie	movie
video/mpeg	mp2
audio/mpeg	mp3
video/mp4	mp4
video/mp4	mp4v
video/mpeg	mpa
video/mpeg	mpe
video/mpeg	mpeg
video/mpeg	mpg
application/vnd.ms-project	mpp
video/mpeg	mpv2
application/x-troff-ms	ms
application/octet-stream	msi
application/octet-stream	mso
application/x-msmediaview	mvb
application/x-miva-compiled	mvc
application/x-netcdf	nc
video/x-ms-asf	nsc
message/rfc822	nws
application/octet-stream	ocx
application/oda	oda
text/x-ms-odc	odc
application/oleobject	ods
audio/ogg	oga
video/ogg	ogg
video/ogg	ogv
application/onenote	one
application/onenote	onea
application/onenote	onetoc
application/onenote	onetoc2
application/onenote	onetmp
application/onenote	onepkg
application/opensearchdescription+xml	osdx
font/otf	otf
application/pkcs10	p10
application/x-pkcs12	p12
application/x-pkcs7-certificates	p7b
application/pkcs7-mime	p7c
application/pkcs7-mime	p7m
application/x-pkcs7-certreqresp	p7r
application/pkcs7-signature	p7s
image/x-portable-bitmap	pbm
application/octet-stream	pcx
application/octet-stream	pcz
application/pdf	pdf
application/octet-stream	pfb
application/octet-stream	pfm
application/x-pkcs12	pfx
image/x-portable-graymap	pgm
application/vnd.ms-pki.pko	pko
application/x-perfmon	pma
application/x-perfmon	pmc
application/x-perfmon	pml
application/x-perfmon	pmr
application/x-perfmon	pmw
image/png	png
image/x-portable-anymap	pnm
image/png	pnz
application/vnd.ms-powerpoint	pot
application/vnd.ms-powerpoint.template.macroEnabled.12	potm
application/vnd.openxmlformats-officedocument.presentationml.template	potx
application/vnd.ms-powerpoint.addin.macroEnabled.12	ppam
image/x-portable-pixmap	ppm
application/vnd.ms-powerpoint	pps
application/vnd.ms-powerpoint.slideshow.macroEnabled.12	ppsm
application/vnd.openxmlformats-officedocument.presentationml.slideshow	ppsx
application/vnd.ms-powerpoint	ppt
application/vnd.ms-powerpoint.presentation.macroEnabled.12	pptm
application/vnd.openxmlformats-officedocument.presentationml.presentation	pptx
application/pics-rules	prf
application/octet-stream	prm
application/octet-stream	prx
application/postscript	ps
application/octet-stream	psd
application/octet-stream	psm
application/octet-stream	psp
application/x-mspublisher	pub
video/quicktime	qt
application/x-quicktimeplayer	qtl
application/octet-stream	qxd
audio/x-pn-realaudio	ra
audio/x-pn-realaudio	ram
application/octet-stream	rar
image/x-cmu-raster	ras
image/vnd.rn-realflash	rf
image/x-rgb	rgb
application/vnd.rn-realmedia	rm
audio/mid	rmi
application/x-troff	roff
audio/x-pn-realaudio-plugin	rpm
application/rtf	rtf
text/richtext	rtx
application/x-msschedule	scd
text/scriptlet	sct
application/octet-stream	sea
application/set-payment-initiation	setpay
application/set-registration-initiation	setreg
text/sgml	sgml
application/x-sh	sh
application/x-shar	shar
application/x-stuffit	sit
application/vnd.ms-powerpoint.slide.macroEnabled.12	sldm
application/vnd.openxmlformats-officedocument.presentationml.slide	sldx
audio/x-smd	smd
application/octet-stream	smi
audio/x-smd	smx
audio/x-smd	smz
audio/basic	snd
application/octet-stream	snp
application/x-pkcs7-certificates	spc
application/futuresplash	spl
audio/ogg	spx
application/x-wais-source	src
application/streamingmedia	ssm
application/vnd.ms-pki.certstore	sst
application/vnd.ms-pki.stl	stl
application/x-sv4cpio	sv4cpio
application/x-sv4crc	sv4crc
image/svg+xml	svg
image/svg+xml	svgz
application/x-shockwave-flash	swf
application/x-troff	t
application/x-tar	tar
application/x-tcl	tcl
application/x-tex	tex
application/x-texinfo	texi
application/x-texinfo	texinfo
application/x-compressed	tgz
application/vnd.ms-officetheme	thmx
application/octet-stream	thn
image/tiff	tif
image/tiff	tiff
application/octet-stream	toc
application/x-troff	tr
application/x-msterminal	trm
video/vnd.dlna.mpeg-tts	ts
text/tab-separated-values	tsv
application/octet-stream	ttf
video/vnd.dlna.mpeg-tts	tts
text/plain	txt
application/octet-stream	u32
text/iuls	uls
application/x-ustar	ustar
text/vbscript	vbs
text/x-vcard	vcf
text/plain	vcs
application/vnd.ms-visio.viewer	vdx
text/xml	vml
application/vnd.visio	vsd
application/vnd.visio	vss
application/vnd.visio	vst
application/x-ms-vsto	vsto
application/vnd.visio	vsw
application/vnd.visio	vsx
application/vnd.visio	vtx
audio/wav	wav
audio/x-ms-wax	wax
image/vnd.wap.wbmp	wbmp
application/vnd.ms-works	wcm
application/vnd.ms-works	wdb
video/webm	webm
application/vnd.ms-works	wks
video/x-ms-wm	wm
audio/x-ms-wma	wma
application/x-ms-wmd	wmd
application/x-msmetafile	wmf
text/vnd.wap.wml	wml
application/vnd.wap.wmlc	wmlc
text/vnd.wap.wmlscript	wmls
application/vnd.wap.wmlscriptc	wmlsc
video/x-ms-wmp	wmp
video/x-ms-wmv	wmv
video/x-ms-wmx	wmx
application/x-ms-wmz	wmz
font/x-woff	woff
application/font-woff2	woff2
application/vnd.ms-works	wps
application/x-mswrite	wri
x-world/x-vrml	wrl
x-world/x-vrml	wrz
text/xml	wsdl
video/x-ms-wtv	wtv
video/x-ms-wvx	wvx
application/directx	x
x-world/x-vrml	xaf
application/xaml+xml	xaml
application/x-silverlight-app	xap
application/x-ms-xbap	xbap
image/x-xbitmap	xbm
text/plain	xdr
application/xhtml+xml	xht
application/xhtml+xml	xhtml
application/vnd.ms-excel	xla
application/vnd.ms-excel.addin.macroEnabled.12	xlam
application/vnd.ms-excel	xlc
application/vnd.ms-excel	xlm
application/vnd.ms-excel	xls
application/vnd.ms-excel.sheet.binary.macroEnabled.12	xlsb
application/vnd.ms-excel.sheet.macroEnabled.12	xlsm
application/vnd.openxmlformats-officedocument.spreadsheetml.sheet	xlsx
application/vnd.ms-excel	xlt
application/vnd.ms-excel.template.macroEnabled.12	xltm
application/vnd.openxmlformats-officedocument.spreadsheetml.template	xltx
application/vnd.ms-excel	xlw
text/xml	xml
x-world/x-vrml	xof
image/x-xpixmap	xpm
application/vnd.ms-xpsdocument	xps
text/xml	xsd
text/xml	xsf
text/xml	xsl
text/xml	xslt
application/octet-stream	xsn
application/octet-stream	xtp
image/x-xwindowdump	xwd
application/x-compress	z
application/x-zip-compressed	zip

# From https://github.com/apache/flex-sdk/blob/develop/modules/compiler/src/java/flex2/compiler/util/MimeMappings.java
text/mxml									mxml
text/as										as
text/fxg									fxg
application/x-actionscript-bytecode			abc
text/css									css
text/properties								properties
image/jpeg									jpg jpeg
image/jpg									jpg jpeg
image/png									png
image/gif									gif
image/svg									svg svgz
#image/svg-xml
audio/mpeg									mp3
application/x-shockwave-flash				swf
text/xml									xml
# Fonts; Depreciated, use font/*: font/truetype, font/opentype, font/woff and font/woff2
application/x-font-truetype					ttf
application/x-font-truetype-collection		ttc
application/x-font-opentype					otf
#application/x-font
application/x-dfont							dfont
application/x-pbj							pbj
image/tiff									tiff tif

# https://en.wikipedia.org/wiki/MPEG-4_Part_14#.MP4_versus_.M4A
video/mp4									mp4 m4a m4p m4b m4r m4v
# https://en.wikipedia.org/wiki/Ogg
video/ogg									ogg ogv ogx ogm
audio/ogg									oga spx opus

# https://en.wikipedia.org/wiki/Advanced_Systems_Format
audio/x-ms-wma								wma
video/x-ms-asf								wmv
application/vnd.ms-asf						asf
application/vnd.ms-asf						asr
application/vnd.ms-asf						asx
```

Unkown source, could be incorrect:

```
# Plain text files
text/plain							txt text def list log in
# Source files
text/x-asm							s asm
text/x-c							c cc cxx cpp h hh dic
text/x-fortran						f for f77 f90
text/x-pascal						p pas
text/x-java-source					java
text/x-php							php
application/x-php					php
application/x-httpd-php				php
text/x-setext						etx
text/plain							bas
text/plain							php phtml php5 phps
text/plain							asp aspx
text/plain							pl pm
text/plain							py pyw pyc pyo pyd
text/plain							rb rbw
application/x-wais-source			src
text/plain							make
application/x-sh					sh
text/csv							csv
text/tab-separated-values			tsv
# Configuration files
text/plain							cnf conf ini inf
# Manual / Documentation files
application/vndms-htmlhelp			chm
application/winhlp					hlp
text/troff							t tr roff man me ms
application/x-troff-man				man
application/x-font-ghostscript		gsf
application/x-font-linux-psf		psf
application/x-font-otf				otf
application/x-font-pcf				pcf
application/x-font-snf				snf
application/x-font-ttf				ttf ttc
application/x-font-type1			pfa pfb pfm afm
# HyperText Markup Language (HTML) markup
text/html							html htm
# eXtensible HyperText Markup Language (XHTML) markup
application/xhtml+xml				xhtml xht
# Handheld Device Markup Language (HDML) markup
text/x-hdml							hdml
# Wireless Markup Language (WML) markup
text/vndwapwml						wml
application/vndwapwmlc				wmlc
# Wireless Markup Language Script (WMLScript) (WLMS) markup
text/vndwapwmlscript				wmls
application/vndwapwmlscriptc		wmlsc
# WAP Binary XML (WBXML) markup
application/vndwapwbxml				wbxml
# Standard Generalized Markup Language (SGML) markup
application/sgml					sgml sgm
text/sgml							sgml sgm
# MIME HyperText Markup Language (MHTML) markup
message/rfc822						mhtml mht
multipart/related					mhtml mht
# application/maff+zip				maff maf
# application/x-maff				maff maf
# HyperText Markup Language Application (HTA) markup
application/x-hta					hta
# Server parsed HyperText Markup Language/Server Side Includes (SHTML/SSI) markup
text/x-server-parsed-html			shtml shtm stm ssi
# Extensible Markup Language (XML) markup
application/xml						xml xsl xsf xsd
text/xml							xml xsl xsf xsd
text/xsl							xsl
text/xml-external-parsed-entity		xml
application/xml-dtd					dtd
# Extensible Stylesheet Language Transformations (XSLT) markup
application/xslt+xml				xslt
# Web Services Description Language (WSDL) markup
application/wsdl+xml				wsdl
# Resource Description Framework (RDF) markup
application/rdf+xml					rdf
# Really Simple Syndicatio (RSS) markup
application/rss+xml					rss
# Atom Syndication Format (ATOM) markup
application/atom+xml				atom
# Cascading Style Sheets (CSS) markup
text/css							css
# ECMAScript (ES) markup
application/ecmascript				es ecma as
# JavaScript (JS) markup
#application/javascript				js mjs
#application/x-javascript			js
text/javascript						js mjs
application/json					json
# VBScript (VBS) markup
text/x-vbscript						vbs vbe wsf wsc
# Tcl, TeX and LaTeX markup
application/x-tcl					tcl
application/x-tex					tex
application/x-latex					latex
# Texinfo (TEXI) markup
application/x-texinfo				texi texinfo
# Mathematical Markup Language (MathML) markup
text/mathml							mml
text/mathml-renderer				mml
application/mathml+xml				mathml
# Mathematica (MA) markup
application/mathematica				ma nb mb
# Extensible Markup Language User Interface Language (XUL) markup
application/vndmozillaxul+xml		xul
# Magic eXtensible Markup Language (MXML)
application/x-mxml+xml				mxml
# Microsoft Extensible Application Markup Language (XAML) markup
application/xaml+xml				xaml
# Google Earth, Keyhole Markup Language (KML) markup
application/vndgoogle-earthkml+xml	kml
application/vndgoogle-earthkmz			kmz
# vCard (VCF) calendar
text/x-vcard							vcf vcard
# vCalendar (VCS) calendar
text/x-vcalendar										vcs
# iCalendar (ICS) calendar
text/calendar											ics ifb ical icalendar
# Microsft E-Mail Message (EML) document
message/rfc822											eml
# OpenOfficeorg 2+, StarOffice 8+, Open Document Format (ODF): document (ODT)
application/vndoasisopendocumenttext					odt
application/vndoasisopendocumenttext-template			ott
application/vndoasisopendocumenttext-master				otm
application/vndoasisopendocumenttext-web				oth
# OpenOfficeorg 2+, StarOffice 8+, Open Document Format (ODF): presentation (ODP)
application/vndoasisopendocumentpresentation			odp
application/vndoasisopendocumentpresentation-template	otp
# OpenOfficeorg 2+, StarOffice 8+, Open Document Format (ODF): spreadsheet (ODS)
application/vndoasisopendocumentspreadsheet				ods
application/vndoasisopendocumentspreadsheet-template	ots
# OpenOfficeorg 2+, StarOffice 8+, Open Document Format (ODF): graphics (ODG)
application/vndoasisopendocumentgraphics				odg
application/vndoasisopendocumentgraphics-template		otg
# OpenOfficeorg 2+, StarOffice 8+, Open Document Format (ODF): database (ODB)
application/vndoasisopendocumentdatabase				odb
# OpenOfficeorg 2+, StarOffice 8+, Open Document Format (ODF): formula (ODF)
application/vndoasisopendocumentformula					odf
application/vndoasisopendocumentformula-template		odft
# OpenOfficeorg 2+, StarOffice 8+, Open Document Format (ODF): others ()
application/vndoasisopendocumentchart					odc
application/vndoasisopendocumentchart-template			otc
application/vndoasisopendocumentimage					odi
application/vndoasisopendocumentimage-template			oti
application/vndopenofficeorgextension					oxt
# OpenOfficeorg 1, StarOffice 6-7, Binary format: document (SXW)
application/vndsunxmlwriter								sxw
application/vndsunxmlwritertemplate						stw
application/vndsunxmlwriterglobal						sxg
# OpenOfficeorg 1, StarOffice 6-7, Binary format: presentation (SXI)
application/vndsunxmlimpress							sxi
application/vndsunxmlimpresstemplate					sti
# OpenOfficeorg 1, StarOffice 6-7, Binary format: spreadsheet (SXC)
application/vndsunxmlcalc								sxc
application/vndsunxmlcalctemplate						stc
# OpenOfficeorg 1, StarOffice 6-7, Binary format: graphics (SXD)
application/vndsunxmldraw								sxd
application/vndsunxmldrawtemplate						std
# OpenOfficeorg 1, StarOffice 6-7, Binary format: formula (SXM)
application/vndsunxmlmath							sxm
# StarOffice 5, Binary format: document (SDW)
application/vndstardivisionwriter							sdw
application/vndstardivisionwriter							vor
application/vndstardivisionwriter-global							sgl
# StarOffice 5, Binary format: presentation (SDD)
application/vndstardivisionimpress							sdd
application/vndstardivisionimpress-packed							sdp
# StarOffice 5, Binary format: spreadsheet (SDC)
application/vndstardivisioncalc							sdc
# StarOffice 5, Binary format: graphics (SDA)
application/vndstardivisiondraw							sda
# StarOffice 5, Binary format: formula (SMF)
application/vndstardivisionmath							smf
# StarOffice 5, Binary format: others ()
application/vndstardivisionchart							sds
application/vndstardivisionmail							sdm
# StarOffice 1-4, Binary format: document (SDW)
application/x-starwriter							sdw
# StarOffice 1-4, Binary format: presentation (SDD)
application/x-starimpress							sdd
# StarOffice 1-4, Binary format: spreadsheet (SDC)
application/x-starcalc							sdc
# StarOffice 1-4, Binary format: graphics (SDA)
application/x-stardraw							sda
# StarOffice 1-4, Binary format: formula (SMF)
application/x-starmath							smf
# StarOffice 1-4, Binary format: others ()
application/x-starchart							sds
# Microsoft Office 12+, Office Open XML (OOXML/OpenXML): document (DOCX)
application/vndopenxmlformats-officedocumentwordprocessingmldocument							docx
application/vndopenxmlformats-officedocumentwordprocessingmltemplate							dotx
application/vndms-worddocumentmacroEnabled12							docm
application/vndms-wordtemplatemacroEnabled12							dotm
# Microsoft Office 12+, Office Open XML (OOXML/OpenXML): presentation (PPTX)
application/vndopenxmlformats-officedocumentpresentationmlpresentation							pptx
application/vndopenxmlformats-officedocumentpresentationmltemplate							potx
application/vndopenxmlformats-officedocumentpresentationmlslideshow							ppsx
application/vndms-powerpointpresentationmacroEnabled12							pptm
application/vndms-powerpointtemplatemacroEnabled12							potm
application/vndms-powerpointslideshowmacroEnabled12							ppsm
application/vndms-powerpointaddinmacroEnabled12							ppam
# Microsoft Office 12+, Office Open XML (OOXML/OpenXML): spreadsheet (XLSX)
application/vndopenxmlformats-officedocumentspreadsheetmlsheet							xlsx
application/vndopenxmlformats-officedocumentspreadsheetmltemplate							xltx
application/vndms-excelsheetmacroEnabled12							xlsm
application/vndms-exceltemplatemacroEnabled12							xltm
application/vndms-exceladdinmacroEnabled12							xlam
application/vndms-excelsheetbinarymacroEnabled12							xlsb
# Microsoft Office 12+, Office Open XML (OOXML/OpenXML): database (ACCDB)
application/msaccess							accdb accdt accde accdr
# Microsoft Office 1-11, Binary format: document (DOC)
application/msword							doc dot
# Microsoft Office 1-11, Binary format: presentation (PPT)
application/vndms-powerpoint							ppt pot pps ppa
application/vndms-powerpointaddinmacroenabled12							ppam
application/vndms-powerpointpresentationmacroenabled12							pptm
application/vndms-powerpointslidemacroenabled12							sldm
application/vndms-powerpointslideshowmacroenabled12							ppsm
application/vndms-powerpointtemplatemacroenabled12							potm
# Microsoft Office 1-11, Binary format: spreadsheet (XLS)
application/vndms-excel							xls xlt xlm xlw xla xlc xlk xlb xld xlv xll
application/vndms-exceladdinmacroenabled12							xlam
application/vndms-excelsheetbinarymacroenabled12							xlsb
application/vndms-excelsheetmacroenabled12							xlsm
application/vndms-exceltemplatemacroenabled12							xltm
# Microsoft Office 1-11, Binary format: database (MDB)
application/x-msaccess							mdb mdn mde mda mdt mdf mdw
application/x-msaccess							adp adn ade
# Microsoft Office 1-11, Binary format: others ()
application/vndms-project							mpp mpt
# Microsoft Works, Binary format ()
application/vndms-works							wps wks wk1 wcm wdb
# Microsoft Rich Text Format (RTF) document
application/rtf							rtf
text/rtf							rtf
text/richtext							rtx
# Wordperfect document (WPD)
application/vndwordperfect							wpd
# Lotus 1-2-3 spreadsheet (123)
application/vndlotus-1-2-3							123
# SYLK (SLK) spreadsheet
application/x-excel							slk
# dBASE (DBF) database
application/x-dbase							dbf
application/x-dbf							dbf
# QuarkXpress (QXD) document
application/vndquarkquarkxpress							qxd qxt qwd qwt qxl qxb
# Microsoft Favicon (ICO) lossless icon
image/vndmicrosofticon							ico
image/x-icon							ico
# X BitMap (XBM) lossless icon
image/x-xbitmap							xbm
image/x-xbm							xbm
# X Pixmap (XPM) lossless icon
image/x-xpixmap							xpm
image/x-xpm							xpm
# Portable Network Graphics (PNG) raster lossless image
image/png							png
# Portable Pixmap Format (PPM) lossless image
image/x-portable-pixmap							ppm
# Portable Graymap Format (PGM) lossless image
image/x-portable-graymap							pgm
# Portable Bitmap Format (PBM) lossless image
image/x-portable-bitmap							pbm
# Portable Anymap Format (PNM) lossless image
image/x-portable-anymap							pnm
# Microsoft Bitmap (BMP) raster lossless image
image/bmp							bmp dib
image/x-bmp							bmp dib
image/x-ms-bmp							bmp dib
# Apple MacPaint image (PNTG) raster lossless image
image/x-macpaint							pnt pntg mac
# Apple Quicktime image (QTIF) raster lossless image
image/x-quicktime							qti qtif
# PC Paintbrush/Personal Computer eXchange (PCX) raster lossless image
image/x-pcx							pcx
# Truevision TGA/Targa (TGA) raster lossless image
image/x-tga							targa tga tpic
image/x-targa							targa tga tpic
# Silicon Graphics Image (SGI) raster lossless image
image/x-sgi							sgi
image/x-rgb							rgb
# InterLeaved BitMap (ILBM) raster lossless image
image/x-ilbm							ilbm
# Sun Raster Graphic (RAS) raster lossless image
image/x-ras							# WebP, VP8 (WEBP) raster lossy image
image/webp							webp
# JPEG raster lossy image
image/jpeg							jpeg jpg jpe jif jfif jfi
# JPEG 2000 raster lossy image
image/jp2							jp2 j2k
image/jpx							jpx jpf
image/jpm							jpm
# JPEG XR raster lossy/lossless image
image/vndms-photo							hdp jxr wdp
# Microsoft Windows Media Photo (WMP) raster lossy image
video/x-ms-wmp							wmp
# Kodak PhotoCD (PCD) raster lossy image
image/x-pcd							pcd
image/x-photo-cd							pcd
# Animated Portable Network Graphics (APNG) animated raster lossless image
image/png							apng
# Multiple-image Network Graphics (MNG) animated raster lossless image
video/x-mng							mng
# Graphics Interchange Format (GIF) animated raster lossless image
image/gif							gif
# Scalable Vector Graphics (SVG) vector graphic
image/svg+xml							svg svgz
# Adobe Illustrator Artwork (AI) vector graphic
application/postscript							ai
# Macromedia Freehand (FH) vector graphic
image/x-freehand							fh fhc fh4 fh5 fh7
# Corel Draw (CDR) vector graphic
image/x-cdr							cdr
application/x-cdr							cdr
application/x-coreldraw							cdr
# Xara (XAR) vector graphic
application/vndxara							xar
# Microsoft Enhanced Metafile (EMF) vector graphic
image/x-emf							emf emz
# Microsoft Windows Metafile (WMF) vector graphic
application/x-msmetafile							wmf
image/x-wmf							wmf wmz
# Apple Picture (PICT) raster/vector graphic
image/x-pict							pict pct pic
# Computer Graphics Metafile (CGM) vector graphic
image/cgm							cgm
# eXperimental Computing Facility (XCF) graphic
image/x-xcf							xcf
# Tagged Image File Format (TIFF) graphic
image/tiff							tiff tif
image/tiff-fx							tiff tif
# Corel PhotoPaint (CPT) graphic
application/mac-compactpro							cpt
# PostScript (PS) compound image
application/postscript							ps
# Encapsulated PostScript (EPS) compound image
application/postscript							eps epsf epsi
# Adobe Photoshop (PSD) compound image
image/vndadobephotoshop							psd
image/x-photoshop							psd
image/x-psd							psd
# Dejavu/DjVu (DJVU) compound image
image/vnddjvu							djvu djv
image/x-djvu							djvu djv
# Adobe Portable Document Format (PDF) compound image
application/pdf							pdf
application/x-pdf							pdf
application/x-bzpdf							pdf
application/x-gzpdf							pdf
# Microsoft Open XML Paper Specification (OpenXPS) (XPS) document
application/oxps							oxps
application/vndms-xpsdocument							xps
# AutoCAD Drawing (DWG/DXF) drawing
image/vnddwg							dwg
image/x-dwg							dwg
application/x-dwg							dwg
image/vnddxf							dxf
image/x-dxf							dxf
application/x-dxf							dxf
model/vnddwf							dwf
image/x-dwf							dwf
application/x-dwf							dwf
application/x-autocad							dwg dxf dwf
# Initial Graphics Exchange Specification (IGES) drawing
model/iges							igs iges
# 3D Mesh Model (MESH) 3D model
model/mesh							msh mesh silo
# Extensible 3D Graphics (X3D) 3D graphic
model/x3d+vrml							x3d x3dz
model/x3d+xml							x3dv x3dvz
model/x3d+binary							x3db x3dbz
# Virtual Reality Modeling Language (VRML) 3D graphic
model/vrml							wrl wrz vrml
x-world/x-vrml							wrl wrz vrml
application/x-cc3d							wrl wrz vrml
# Synchronized Multimedia Integration Language (SMIL) markup
application/smil+xml							smi smil
# Xiphorg XML Shareable Playlist Format (XSPF) playlist
application/xspf+xml							xspf
# Winamp playlist (M3U/PLS) playlist
audio/x-mpegurl							m3u
application/vndapplempegurl							m3u8
video/vndmpegurl							mxu m4u
application/pls+xml							pls
audio/x-scpls							pls
# Foobar2000 playlist (FPL) playlist
application/octet-stream							fpl
# Microsoft Windows Media Player Playlist (WPL) playlist
application/vndms-wpl							wpl
# Microsoft Advanced Stream Redirector (ASX/LSX) playlist
video/x-ms-asf							asx
video/x-la-asf							lsx
# Microsoft Windows Media Video Redirector (WVX) shortcut
video/x-ms-wmx							wmx
audio/x-ms-wax							wax
video/x-ms-wvx							wvx
# MPEG (M3A) playlist
audio/mpeg							m3a
# WebM, VP8/Vorbis (WEBM) multimedia container
video/webm							webm
audio/webm							webm
# Matroska Multimedia Container (MKV/MKA/MKS) multimedia container
audio/x-matroska							mka
video/x-matroska							mkv mks
# Xiphorg Vorbis (OGX/OGG) multimedia container
application/ogg							ogx
audio/ogg							ogg
video/ogg							ogg
# Nullsoft Streaming Video (NSV) audio/video container
application/x-winamp							nsv nsa
# RealMedia Variable Bitrate (RMVB) audio/video container
application/vndrn-realmedia-vbr							rmvb
# RealMedia (RM) audio/video container
application/vndrn-realmedia							rm
audio/x-pn-realaudio-plugin							rmp
# Adobe Flash Video (FLV) audio/video container
audio/x-f4a							f4a f4b
audio/mp4							f4a f4b
video/x-f4v							f4v f4p
video/mp4							f4v f4p
video/x-fli							fli
video/x-flv							flv
video/x-m4v							m4v
# Third Generation Partnership Project (3GPP) multimedia container
audio/3gpp							3gp 3ggp
audio/3gpp2							3g2 3gp2
video/3gpp							3gp 3ggp
video/3gpp2							3g2 3gp2
# MPEG-4 Part 14, MP4 file format, MPEG-4 file format version 2 (MP4) multimedia container
application/mp4							mp4 mpg4 mp4s
audio/mp4							mp4 mpg4
video/mp4							mp4 mpg4
# Microsoft Advanced Systems Format (ASF) audio/video container
application/vndms-asf							asf
video/x-ms-asf							asf
video/x-la-asf							lsf
# Microsoft Audio Video Interleave (AVI) audio/video container
video/vndavi							avi
video/avi							avi
video/msvideo							avi
video/x-msvideo							avi
# Musical Instrument Digital Interface (MIDI) synthetized music
audio/midi							mid midi kar rmi
# Xiphorg Speex (OGA/OGG) lossy speech
audio/speex							spx
audio/ogg							spx
# Adaptive Multi-Rate Wideband (AMR-WB) lossy speech
audio/amr-wb							awb
# Adaptive Multi-Rate (AMR/AMR-NB) lossy speech
audio/amr							amr
# Xiphorg Free Lossless Audio Codec (FLAC) lossless audio
audio/x-flac							flac
# WavPack (WV) lossless audio
audio/x-wavpack							wv
# True Audio (TTA) lossless audio
audio/x-tta							tta
# Monkey's Audio (APE) lossless audio
audio/x-ape							ape apl
# Apple Lossless Audio Codec (ALAC) lossless audio
audio/x-alac							m4a
# Microsoft Windows Media Audio Lossless (WMA) lossless audio
audio/x-ms-wma							wma
# Sony Adaptive Transform Acoustic Coding (ATRAC) Advanced Lossless (AA3) lossless audio
audio/atrac-advanced-lossless							aa3 at3
# Shorten (SHN) lossless audio
audio/x-shorten							shn
# Apple Audio Interchange File Format (AIFF) lossless audio
audio/x-aiff							aif aiff aifc
audio/aiff							aif aiff aifc
# Adaptive Differential Pulse Code Modulation (ADPCM) lossless audio
audio/adpcm							adp adpcm
# Linear Pulse Code Modulation (LPCM) lossless audio
audio/l16							pcm l16
audio/l8							pcm
audio/l20							pcm
audio/l24							pcm
# Microsoft Waveform Audio File Format (WAVE) lossless audio
audio/vnd.wave							wav wave
audio/wav							wav wave
audio/wave							wav wave
audio/x-wav							wav wave
# Xiphorg Vorbis (OGA/OGG) lossy audio
audio/ogg							oga
audio/vorbis							oga
audio/vorbis-config							oga
# MusePack (MPC) lossy audio
audio/x-musepack							mpc mp+ mpp
audio/musepack							mpc mp+ mpp
# RealAudio (RA) lossy audio
audio/x-pn-realaudio							ra ram
# Microsoft Windows Media Audio (WMA) lossy audio
audio/x-ms-wma							wma
# Sony Adaptive Transform Acoustic Coding (ATRAC) (AA3) lossy audio
audio/atrac-x							aa3 at3
audio/atrac3							aa3 at3
audio/x-oma							oma
# DTS Theater System (DTS) lossy audio
audio/vnddts							dts
audio/vnddtshd							dtshd
# Dolby Digital (AC3) lossy audio
audio/ac3							ac3
# MPEG-4 Part 3, Audio, High-Efficiency Advanced Audio Coding (HE-AAC) (AAC) lossy audio
audio/aacp							aac
# MPEG-4 Part 3, Audio, Advanced Audio Coding (AAC) lossy audio
audio/x-aac							aac
audio/aac							aac
audio/mp4							aac
# MPEG-4 Part 3, Audio, various formats (M4A) lossy audio
audio/mp4							m4a mp4a m4p m4b m4r
audio/mp4a-latm							m4a
audio/mpeg4-generic							m4a
# MPEG-2 Part 3, Audio, Layer I/II/II (M2A) lossy audio
audio/mpeg							m2a mp2a
# MPEG-1 Part 3, Audio, Layer III (MP3) lossy audio
audio/mpeg							mp3
audio/mpa							mp3
audio/mpa-robust							mp3
# MPEG-1 Part 3, Audio, Layer II (MP2) lossy audio
audio/mpeg							mp2 mpa mpga mpega
audio/mpa							mp2 mpa mpga mpega
# MPEG-1 Part 3, Audio, Layer I (MP1) lossy audio
audio/mpeg							mp1 m1a mpa mpga mpega
audio/mpa							mp1 m1a mpa mpga mpega
# Sun Au file format (AU/SND) lossy audio
audio/basic							au snd
# Xiphorg Theora, VP3 (OGV/OGG) lossy video
video/ogg							ogv
# RealVideo (RV) lossy video
video/x-pn-realvideo							rv
video/x-rn-realvideo							rv
# Apple QuickTime File Format (QTFF) (QT/MOV) lossy video
video/quicktime							mov qt
video/x-sgi-movie							movie
# Microsoft Windows Media Video, VC-1 (WMV) lossy video
video/x-ms-wm							wm
video/x-ms-wmv							wmv
video/x-ms-wmx							wmx
video/x-ms-wvx							wvx
# MPEG-4 Part 10, Advanced Video Coding (AVC), H264 lossy video
video/h264							h264
# VCEG H261/H263 lossy video
video/h261							h261
video/h263							h263
# MPEG-4 Part 2, Visual, Advanced Simple Profile (ASP), Xvid/DivX lossy video
video/x-divx							xvid divx
# MPEG-4 Part 2/10/14, Video, various formats (M4V) video
video/mp4							m4v mp4v 3gp 3g2
video/mpeg4-generic							m4v
# MPEG-2 Part 2, Video, H262/DVD (M2V/VOB) lossy video
video/mpeg							m2v mpv2 vob
# MPEG-1 Part 2, Video, VideoCD (M1V) lossy video
video/mpeg							m1v mpv mpe mpg mpeg
video/mpv							m1v mpv mpe mpg mpeg
# Motion JPEG 2000 (M-JPEG2K) (MJ2) lossy/lossless video
video/mj2							mj2 mjp2
video/jpeg2000							mj2 mjp2
# Motion JPEG (M-JPEG) (MJPG) lossy video
video/x-motion-jpeg							mjpg
video/jpeg							jpgv
# Digital Video (DV) DV-DIF raw video (DV/DIF) lossy video
video/dv							dv dif
video/x-dv							dv dif
# RAD Game Tools Bink Video (BIK) lossy video
video/x-bink							bik
# RAD Game Tools Smacker Video (SMK) lossy video
video/x-smacker							smk
# Mozilla XPInstall (Cross-Platform Install) (XPI) application
application/x-xpinstall							xpi
# Adobe Adobe Integrated Runtime (AIR) application
application/vndadobeair-application-installer-package+zip							air
# Adobe Flash (SWF) application
application/x-shockwave-flash							swf
# Adobe Director (DIR) application
application/x-director							dir dcr dxr cst cct cxt w3d fgd swa
# Microsoft Silverlight (XAP) application
application/x-silverlight-app							xap
application/x-ms-xbap							xbap
# Java binaries
application/octet-stream							java
application/java-archive							jar
application/java-serialized-object							ser
application/java-vm							class
application/x-java-jnlp-file							jnlp
# Windows binaries
application/x-msdownload							exe dll ocx com bat msi mso
application/x-ms-manifest							manifest
# Linux / Mac OS binaries
application/octet-stream							bin dms lrf so o elf dist distz pkg bpk dump elc deploy
# Signatures
application/pgp-encrypted							pgp
application/pgp-signature							asc sig
# BinHex (HQX) encoding
application/mac-binhex40							hqx
application/mac-binhex							hqx
application/binhex							hqx
# UUEncode (UU) encoding
text/x-uuencode							uu
# Multi-Purpose Internet Mail Extension (MIME) encoding
message/rfc822							mime
# Encryption
application/pkcs10							p10
application/x-pkcs12							p12 pfx
application/pkcs7-mime							p7m p7c
application/pkcs7-signature							p7s
application/x-pkcs7-certificates							p7b spc
application/x-pkcs7-certreqresp							p7r
application/pkix-cert							cer
application/pkix-crl							crl
application/pkix-pkipath							pkipath
application/pkixcmp							pki
application/vndms-pkipko							pko
application/vndms-pkicertstore							sst
application/vndms-pkiseccat							cat
application/vndms-pkistl							stl
application/x-x509-ca-cert							der crt
# BitTorrent metadata (TORRENT) download
application/x-bittorrent							torrent
# Tape (TAR) archives
application/x-tar							tar
application/x-gtar							gtar
# Gzip (GZ) archives
application/x-gzip							gz tgz
application/x-compressed							tgz
# Bzip (BZ) archives
application/x-bzip							bz tbz
application/x-bzip2							bz2 boz tbz2 tb2
# Compress (Z) archives
application/x-compress							Z taz
# LZMA (LZMA) archives
application/x-lzma							lzma tlz
# LZMA2 (XZ) archives
application/x-xz							xz txz
# LZIP (LZ) archives
application/x-lzip							lz
# LHA and LZH archives
application/x-lzh-compressed							lha lzh
# LZX archives
application/x-lzx							lzx
# Disk Archiver (DAR) archives
application/x-dar							dar
# Compact File Set (CFS) archives
application/x-cfs-compressed							cfs
# 7-ZIP (7z) archives
application/x-7z-compressed							7z
# ZIP archives
application/zip							zip zipx
# RAR files
application/x-rar-compressed							rar rev r00 r01 r02 r03 r04 r05
# Cabinet (CAB) archives
application/vndms-cab-compressed							cab
# Stuffit (SIT) archives
application/x-stuffit							sit
application/x-stuffitx							sitx
# Debian (DEB) archives
application/x-debian-package							deb udeb
# Apple DiskImage (DMG) archive
application/x-apple-diskimage							dmg smi img
# ISO 9660 (ISO) archive
application/x-iso9660-image							iso

application/java-archive									jar
application/mathematica										nb
application/msword											doc dot

# Mobile XMF (Extensible Music Format)
audio/mobile-xmf											mxmf xmf
# NRT (Nokia Ring Tone)
audio/x-nrt													nrt
# Nokia ringtone
audio/x-rtx													rtx
# Nokia ringtone
audio/x-rt													rt
# Nokia ringtone
audio/x-dm													dm
# Nokia Monophonic ringtone
application/vnd.nokia.ringing-tone							rng
# Core Audio Format
audio/x-caf													caf
# Siemens Ringtone
audio/x-srt													srt

															wwd
# Motorola Motomixer
audio/x-bas													bas
# Nokia MIDI
audio/x-spmid												spmid
# LG ringtones
audio/x-jet													jet
```

### Protocole specific media type

Used by emails or HTTP

Multipart and stream:

- `text/event-stream` - [Server-Sent Events](https://www.w3.org/TR/eventsource/#parsing-an-event-stream)
- `multipart/mixed`
- `multipart/alternative`
- `multipart/related` - Can be use for directory listing (optionally with external bodies) [RFC 2387 - The MIME Multipart/Related Content-type](https://tools.ietf.org/html/rfc2387)
- `message/external-body` - [RFC 2017 - Definition of the URL MIME External-Body Access-Type](https://tools.ietf.org/html/rfc2017)

- `application/x-www-form-urlencoded`
- `multipart/appledouble`
- `multipart/byteranges` - for requests with multiple ranges - [HTTP byte ranges and multipart/byteranges alternatives? - Stack Overflow](https://stackoverflow.com/questions/19290033/http-byte-ranges-and-multipart-byteranges-alternatives)
- `multipart/digest`
- `multipart/encrypted`
- `multipart/form-data`
- `multipart/header-set`
- `multipart/parallel`
- `multipart/related`
- `multipart/report`
- `multipart/signed`
- `multipart/voice-message`
- `multipart/x-mixed-replace` - use to stream content. [MIME — Wikipedia](https://en.wikipedia.org/wiki/MIME#Mixed-Replace). See also `text/event-stream`

External body examples:

- `message/external-body; access-type=URL; URL="http://www.foo.com/file"`
- `message/external-body; access-type=local-file; name="file:/local/path/file.html"`

```http
Content-type: message/external-body; access-type=local-file; name="/u/nsb/Me.gif"
```

```http
Content-type:  image/gif
Content-ID: <id42@guppylake.bellcore.com>
Content-Transfer-Encoding: binary

THIS IS NOT REALLY THE BODY!
```

URIs:

- `text/uri-list`, `.uris` or `.uri`, [RFC 2483 - URI Resolution Services Necessary for URN Resolution](https://tools.ietf.org/html/rfc2483#section-5)

- [MIME — Wikipedia](https://en.wikipedia.org/wiki/MIME#Multipart_subtypes)
- [email - Mail multipart/alternative vs multipart/mixed - Stack Overflow](https://stackoverflow.com/questions/3902455/mail-multipart-alternative-vs-multipart-mixed)
- [email - Multipart messages including multiple attachments ("attachment" and "inline") with Zend Mail – RFC-compliant? - Stack Overflow](https://stackoverflow.com/questions/19497672/multipart-messages-including-multiple-attachments-attachment-and-inline-wi)
- [Content-Type: multipart](https://msdn.microsoft.com/en-us/library/ms527355%28v=exchg.10%29.aspx)
- [http - How to specify to accept multipart/related content type with particular content types for body part in the accept header field - Stack Overflow](https://stackoverflow.com/questions/36332842/how-to-specify-to-accept-multipart-related-content-type-with-particular-content)
- [\[MS-OXCMAIL\]: External Body Attachments](https://msdn.microsoft.com/en-us/library/gg671972%28v=exchg.80%29.aspx)
- [Support for message/external-body content type (RFC 2017) • mozillaZine Forums](http://forums.mozillazine.org/viewtopic.php?f=39&t=390222)

### Directory media type

- `text/plain`
- `vnd.android.document/directory`
- `inode/directory`, `inode/directory;role=remote.net.smb.workgroup`

Use `multipart/related`?

- [folder - MIME type for a directory - Stack Overflow](https://stackoverflow.com/questions/18869772/mime-type-for-a-directory)
- [Mime types for folders](https://lists.freedesktop.org/archives/xdg/2011-February/011797.html)
- https://www.iana.org/assignments/media-types/text/directory
- [Unified system](https://specifications.freedesktop.org/shared-mime-info-spec/latest/ar01s02.html#idm140622087696400)

## File system

- [Another Forensics Blog: Mounting an APFS image in Linux](https://web.archive.org/web/20210531025605/https://az4n6.blogspot.com/2018/01/mounting-apfs-image-in-linux.html)
- [sgan81/apfs-fuse: FUSE driver for APFS (Apple File System)](https://github.com/sgan81/apfs-fuse)
- [cugu/apfs.ksy: APFS filesystem format for Kaitai Struct](https://github.com/cugu/apfs.ksy)
- [About Apple File System | Apple Developer Documentation](https://developer.apple.com/documentation/foundation/file_system/about_apple_file_system)
- [mac_apt/plugins/helpers/apfs.py at master · ydkhatri/mac_apt](https://github.com/ydkhatri/mac_apt/blob/master/plugins/helpers/apfs.py)
- [mac_apt/plugins/helpers/apple_sparse_image.py at master · ydkhatri/mac_apt](https://github.com/ydkhatri/mac_apt/blob/master/plugins/helpers/apple_sparse_image.py)

## Reverse engineering data

- [Protocol Buffers](./Protocol%20Buffers/Protocol%20Buffers.md)
- string length (32 bits) + string data (ascii or utf-8 bytes)

> The timestamps could be stored as absolute values since unix epoch, or could be stored as relative to the previous sample, or relative to the start of the profile, and could be stored as floating point values or integers, and those integers might be big endian or small endian.

- [solemnwarning/rehex: Reverse Engineers' Hex Editor](https://github.com/solemnwarning/rehex)
- [Reverse Engineering Instruments’ File Format](http://jamie-wong.com/post/reverse-engineering-instruments-file-format/)
- [How to crack a Binary File Format](http://www.iwriteiam.nl/Ha_HTCABFF.html)
- [DGTEFF - THE DEFINITIVE GUIDE TO EXPLORING FILE FORMATS - XentaxWiki](http://wiki.xentax.com/index.php/DGTEFF)
- [Home of Hexinator - The Professional Hex Editor - Hexinator](https://hexinator.com/) - hex editor and binary analysis tool
- [Synalyze It! - more than a Hex Editor for Mac OS X](https://www.synalysis.net/) - hex editor and binary analysis tool
- [010 Editor - The Professional Text/Hex Editor with Binary Templates](http://sweetscape.com/010editor/)
- [Reverse Engineering Apple Location Services Protocol : programming](https://www.reddit.com/r/programming/comments/6abmlo/reverse_engineering_apple_location_services/)
- [RE for Beginners | Reverse Engineering](https://www.begin.re/)

## Sample files

See [Sample data](../Data/Sample%20data/Sample%20data.md)

- [JSONPlaceholder - Fake online REST API for developers](http://jsonplaceholder.typicode.com/)
- [SWAPI - The Star Wars API](http://swapi.co/)

- [Test files used by jMimeMagic](https://github.com/arimus/jmimemagic/tree/master/test_docs)

### Smallest files

- [Minimal PDF](https://brendanzagaeski.appspot.com/0004.html)
- [mathiasbynens/small: Smallest possible syntactically valid files of different types](https://github.com/mathiasbynens/small)
- [The Tiniest GIF Ever · Probably Programming](http://probablyprogramming.com/2009/03/15/the-tiniest-gif-ever)
- [Maxime Euzière](http://xem.github.io/articles/#webgl_quest)
- [The smallest 256x256 single-color PNG file, and where you've seen it](https://www.mjt.me.uk/posts/smallest-png/)

### Small video

```sh
# MP4 H.264
ffmpeg -r 1 -f image2 -i frame.png -vcodec libx264 -crf 25 -pix_fmt yuv420p test.mp4
```

```js
// The following video file is an h.264 encoded two-second video with four
// black frames generated with wide decoding compatibility in mind.
// File is 909 bytes (1212 in base64).
// Video file is generated by the following `ffmpeg` command:
//  $ffmpeg -f lavfi -i color=color=black:rate=2:size=100x100 -t 2
//  -profile:v baseline -preset slow
//  -pix_fmt yuv420p -vcodec libx264 /tmp/small.mp4
// From https://github.com/ampproject/amphtml/blob/1ba016051f20ee630e0032e87bd0b199c66a4d0d/src/service/video-manager-impl.js#L362
// https://github.com/ampproject/amphtml/pull/5297
video.src = 'data:video/mp4;base64,AAAAIGZ0eXBpc29tAAACAGlzb21pc28yYXZjMW1wNDEAAAAIZnJlZQAAAFttZGF0AAAAMmWIhD///8PAnFAAFPf3333331111111111111111111111111111111111111111114AAAABUGaOeDKAAAABkGaVHgygAAAAAZBmnZ4MoAAAAMKbW9vdgAAAGxtdmhkAAAAAAAAAAAAAAAAAAAD6AAAB9AAAQAAAQAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAgAAAjt0cmFrAAAAXHRraGQAAAAPAAAAAAAAAAAAAAABAAAAAAAAB9AAAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAABAAAAAAGQAAABkAAAAAAAkZWR0cwAAABxlbHN0AAAAAAAAAAEAAAfQAAAAAAABAAAAAAGzbWRpYQAAACBtZGhkAAAAAAAAAAAAAAAAAAAAAgAAAARVxAAAAAAALWhkbHIAAAAAAAAAAHZpZGUAAAAAAAAAAAAAAABWaWRlb0hhbmRsZXIAAAABXm1pbmYAAAAUdm1oZAAAAAEAAAAAAAAAAAAAACRkaW5mAAAAHGRyZWYAAAAAAAAAAQAAAAx1cmwgAAAAAQAAAR5zdGJsAAAAlnN0c2QAAAAAAAAAAQAAAIZhdmMxAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAGQAZABIAAAASAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGP//AAAAMGF2Y0MBQsAK/+EAGGdCwArZhz+efARAAAADAEAAAAMBA8SJmgEABWjJYPLIAAAAGHN0dHMAAAAAAAAAAQAAAAQAAAABAAAAFHN0c3MAAAAAAAAAAQAAAAEAAAAcc3RzYwAAAAAAAAABAAAAAQAAAAQAAAABAAAAJHN0c3oAAAAAAAAAAAAAAAQAAAA2AAAACQAAAAoAAAAKAAAAFHN0Y28AAAAAAAAAAQAAADAAAABbdWR0YQAAAFNtZXRhAAAAAAAAACFoZGxyAAAAAAAAAABtZGlyYXBwbAAAAAAAAAAAAAAAACZpbHN0AAAAHql0b28AAAAWZGF0YQAAAAEAAAAAR29vZ2xl';
```

```js
// mp4/h264 used by https://github.com/GoogleWebComponents/google-youtube/blob/e83e3356344ee1c5da57a1db1c3ca0c068a3dc7e/google-youtube.html#L412
mp4Source.src = "data:video/mp4;base64,AAAAFGZ0eXBNU05WAAACAE1TTlYAAAOUbW9vdgAAAGxtdmhkAAAAAM9ghv7PYIb+AAACWAAACu8AAQAAAQAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAgAAAnh0cmFrAAAAXHRraGQAAAAHz2CG/s9ghv4AAAABAAAAAAAACu8AAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAAAAAAAAABAAAAAAFAAAAA4AAAAAAHgbWRpYQAAACBtZGhkAAAAAM9ghv7PYIb+AAALuAAANq8AAAAAAAAAIWhkbHIAAAAAbWhscnZpZGVBVlMgAAAAAAABAB4AAAABl21pbmYAAAAUdm1oZAAAAAAAAAAAAAAAAAAAACRkaW5mAAAAHGRyZWYAAAAAAAAAAQAAAAx1cmwgAAAAAQAAAVdzdGJsAAAAp3N0c2QAAAAAAAAAAQAAAJdhdmMxAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAFAAOABIAAAASAAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGP//AAAAEmNvbHJuY2xjAAEAAQABAAAAL2F2Y0MBTUAz/+EAGGdNQDOadCk/LgIgAAADACAAAAMA0eMGVAEABGjuPIAAAAAYc3R0cwAAAAAAAAABAAAADgAAA+gAAAAUc3RzcwAAAAAAAAABAAAAAQAAABxzdHNjAAAAAAAAAAEAAAABAAAADgAAAAEAAABMc3RzegAAAAAAAAAAAAAADgAAAE8AAAAOAAAADQAAAA0AAAANAAAADQAAAA0AAAANAAAADQAAAA0AAAANAAAADQAAAA4AAAAOAAAAFHN0Y28AAAAAAAAAAQAAA7AAAAA0dXVpZFVTTVQh0k/Ou4hpXPrJx0AAAAAcTVREVAABABIAAAAKVcQAAAAAAAEAAAAAAAAAqHV1aWRVU01UIdJPzruIaVz6ycdAAAAAkE1URFQABAAMAAAAC1XEAAACHAAeAAAABBXHAAEAQQBWAFMAIABNAGUAZABpAGEAAAAqAAAAASoOAAEAZABlAHQAZQBjAHQAXwBhAHUAdABvAHAAbABhAHkAAAAyAAAAA1XEAAEAMgAwADAANQBtAGUALwAwADcALwAwADYAMAA2ACAAMwA6ADUAOgAwAAABA21kYXQAAAAYZ01AM5p0KT8uAiAAAAMAIAAAAwDR4wZUAAAABGjuPIAAAAAnZYiAIAAR//eBLT+oL1eA2Nlb/edvwWZflzEVLlhlXtJvSAEGRA3ZAAAACkGaAQCyJ/8AFBAAAAAJQZoCATP/AOmBAAAACUGaAwGz/wDpgAAAAAlBmgQCM/8A6YEAAAAJQZoFArP/AOmBAAAACUGaBgMz/wDpgQAAAAlBmgcDs/8A6YEAAAAJQZoIBDP/AOmAAAAACUGaCQSz/wDpgAAAAAlBmgoFM/8A6YEAAAAJQZoLBbP/AOmAAAAACkGaDAYyJ/8AFBAAAAAKQZoNBrIv/4cMeQ==";
```

```js
// webm used by https://github.com/GoogleWebComponents/google-youtube/blob/e83e3356344ee1c5da57a1db1c3ca0c068a3dc7e/google-youtube.html#L416
video.src = "data:video/webm;base64,GkXfo49CgoR3ZWJtQoeBAUKFgQEYU4BnAQAAAAAAF60RTZt0vE27jFOrhBVJqWZTrIIQA027jFOrhBZUrmtTrIIQbE27jFOrhBFNm3RTrIIXmU27jFOrhBxTu2tTrIIWs+xPvwAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAFUmpZuQq17GDD0JATYCjbGliZWJtbCB2MC43LjcgKyBsaWJtYXRyb3NrYSB2MC44LjFXQY9BVlNNYXRyb3NrYUZpbGVEiYRFnEAARGGIBc2Lz1QNtgBzpJCy3XZ0KNuKNZS4+fDpFxzUFlSua9iu1teBAXPFhL4G+bmDgQG5gQGIgQFVqoEAnIEAbeeBASMxT4Q/gAAAVe6BAIaFVl9WUDiqgQEj44OEE95DVSK1nIN1bmTgkbCBULqBPJqBAFSwgVBUuoE87EQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAB9DtnVB4eeBAKC4obaBAAAAkAMAnQEqUAA8AABHCIWFiIWEiAICAAamYnoOC6cfJa8f5Zvda4D+/7YOf//nNefQYACgnKGWgQFNANEBAAEQEAAYABhYL/QACIhgAPuC/rOgnKGWgQKbANEBAAEQEAAYABhYL/QACIhgAPuC/rKgnKGWgQPoANEBAAEQEAAYABhYL/QACIhgAPuC/rOgnKGWgQU1ANEBAAEQEAAYABhYL/QACIhgAPuC/rOgnKGWgQaDANEBAAEQEAAYABhYL/QACIhgAPuC/rKgnKGWgQfQANEBAAEQEAAYABhYL/QACIhgAPuC/rOgnKGWgQkdANEBAAEQEBRgAGFgv9AAIiGAAPuC/rOgnKGWgQprANEBAAEQEAAYABhYL/QACIhgAPuC/rKgnKGWgQu4ANEBAAEQEAAYABhYL/QACIhgAPuC/rOgnKGWgQ0FANEBAAEQEAAYABhYL/QACIhgAPuC/rOgnKGWgQ5TANEBAAEQEAAYABhYL/QACIhgAPuC/rKgnKGWgQ+gANEBAAEQEAAYABhYL/QACIhgAPuC/rOgnKGWgRDtANEBAAEQEAAYABhYL/QACIhgAPuC/rOgnKGWgRI7ANEBAAEQEAAYABhYL/QACIhgAPuC/rIcU7trQOC7jLOBALeH94EB8YIUzLuNs4IBTbeH94EB8YIUzLuNs4ICm7eH94EB8YIUzLuNs4ID6LeH94EB8YIUzLuNs4IFNbeH94EB8YIUzLuNs4IGg7eH94EB8YIUzLuNs4IH0LeH94EB8YIUzLuNs4IJHbeH94EB8YIUzLuNs4IKa7eH94EB8YIUzLuNs4ILuLeH94EB8YIUzLuNs4INBbeH94EB8YIUzLuNs4IOU7eH94EB8YIUzLuNs4IPoLeH94EB8YIUzLuNs4IQ7beH94EB8YIUzLuNs4ISO7eH94EB8YIUzBFNm3SPTbuMU6uEH0O2dVOsghTM";
```

```js
// 1x1 transparent WebM VP9
// convert xc:transparent -define png:color-type=6 image.png png:- | ffmpeg -i - -c:v libvpx-vp9 1x1_transparent.webm
video.src = "data:video/webm;base64,GkXfowEAAAAAAAAfQoaBAUL3gQFC8oEEQvOBCEKChHdlYm1Ch4ECQoWBAhhTgGcBAAAAAAACABFNm3RALE27i1OrhBVJqWZTrIHlTbuMU6uEFlSua1OsggEjTbuMU6uEHFO7a1OsggHj7AEAAAAAAACqAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAVSalmAQAAAAAAADIq17GDD0JATYCNTGF2ZjU3LjU2LjEwMFdBjUxhdmY1Ny41Ni4xMDBEiYhARAAAAAAAABZUrmsBAAAAAAAARq4BAAAAAAAAPdeBAXPFgQGcgQAitZyDdW5khoVWX1ZQOYOBASPjg4QCYloA4AEAAAAAAAARsIEBuoEBmoECU8CBAVSygQQfQ7Z1AQAAAAAAAGLngQCgAQAAAAAAAFahoIEAAACCSYNCAAAAAAYAOCQcGFQAACAgABG///9+GAAAdaEBAAAAAAAAKqYBAAAAAAAAIe6BAaWcgkmDQgAAAAAGADgkHBhUAAAgIAARv///kxEAABxTu2sBAAAAAAAAEbuPs4EAt4r3gQHxggF18IED"
```

- [Smallest possible syntactically valid files of different types](https://github.com/mathiasbynens/small)
- [The smallest possible valid (X)HTML documents · Mathias Bynens](https://mathiasbynens.be/notes/minimal-html)

### Sample filesystem hierarchy

- [generate a tree of diverse file names](https://github.com/jakeogh/angryfiles)
- [petrosagg/wtfiles: Files that make you go WTF!](https://github.com/petrosagg/wtfiles)

### Images

- [Standard test image - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Standard_test_image)
- [Yardstick pictures: Image Test Suite](https://yardstick.pictures/)
- [Welcome to Para-Dice in Sight - Compression DataBase](http://wayback.archive.org/web/20140617090355/http://cdb.paradice-insight.us/)
- [TID2008: TAMPERE IMAGE DATABASE 2008 | Computer Vision Online](http://www.computervisiononline.com/dataset/tid2008-tampere-image-database-2008)

- [Lorem.space - placeholder image generator](https://lorem.space/)
- [Dynamic Dummy Image Generator - DummyImage.com](https://dummyimage.com/)
- [Placeholder.com: Placeholder.com – The Free Image Placeholder Service Favoured By Designers](https://placeholder.com/)
- [LoremFlickr: free placeholder images](https://loremflickr.com/)

- [Tecnick's public test images](http://www.tecnick.com/public/code/cp_dpage.php?aiocp_dp=testimages)
- [Fractal art 2](http://morbid-sheep.deviantart.com/art/Final-Monster-Fractal-Pack-213288585)
- [Fractal art](http://greentunic.deviantart.com/art/Fractal-Pack-4-150661301)
- [Braid game graphics](http://www.davidhellman.net/braidbrief.htm)
- [wallpaper-jpegs](http://tincek-marincek.deviantart.com/art/Wallpaper-Pack-484504974)
- [icons8/flat-color-icons: Free Flat Color Icons](https://github.com/icons8/flat-color-icons)
- [guihints](http://guihints.openpandora.org/n22/best-before/2013-03-31/guihints01-0.8.2.0-alpha.zip)
- [google-material-design-icons](https://github.com/google/material-design-icons/releases/tag/1.0.0)
- Niels Fröhling's sparse color images
- [Wikipedia:Images — Wikipedia](https://en.wikipedia.org/wiki/Wikipedia:Images)
- [Plots](https://github.com/jonsneyers/FLIF/tree/master/benchmark)
- [WebP Lossless Alpha Gallery](https://developers.google.com/speed/webp/gallery2)
- [PNG photo images free clipart download](http://pngimg.com/)
- [High altitude aerial images](http://sipi.usc.edu/database/database.php?volume=aerials)
- [Amsterdam Library of Object Images (ALOI)](http://aloi.science.uva.nl/tars/aloi_stereo.tar)
- [The New Test Images](http://imagecompression.info/test_images/)
- [Kodak Lossless True Color Image Suite](http://r0k.us/graphics/kodak/)
- [Test images](http://sourceforge.net/projects/testimages/files/SAMPLING/8BIT/RGB/)
- [Database of faces](http://www.cl.cam.ac.uk/research/dtg/attarchive/facedatabase.html)
- [Lukas 2D 8 Bit Medical Image Corpus](http://www.data-compression.info/Corpora/LukasCorpus/)
- [Berkeley Segmentation Dataset](http://www.eecs.berkeley.edu/Research/Projects/CS/vision/bsds/)
- [Textures](http://sipi.usc.edu/database/database.php?volume=textures)
- [USC-SIPI Image Database](http://sipi.usc.edu/database/database.php?volume=misc)
- [Waterloo colour set](http://links.uwaterloo.ca/Repository.html)
- [Visions of the Future](http://www.jpl.nasa.gov/visions-of-the-future/)
- [Computer Graphics Data](http://graphics.cs.williams.edu/data/images.xml)
- [Lenna - Wikipedia, the free encyclopedia](http://en.wikipedia.org/wiki/Lenna)
- [Dynamic Dummy Image Generator - DummyImage.com](http://dummyimage.com/)
- [Placehold.it - Quick and simple image placeholders](http://placehold.it/)
- [Standard test image - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Standard_test_image)
- [SIPI Image Database - Misc](http://sipi.usc.edu/database/database.php?volume=misc)
- [The Rest of the Lenna Story](http://www.cs.cmu.edu/~chuck/lennapg/lenna.shtml)
- [Test Images for the ZaaIL project](https://github.com/ZaaLabs/ZaaIL-TestImages)
- [Katsushika Hokusai | The Art Institute of Chicago](https://www.artic.edu/collection?artist_ids=Katsushika%20Hokusai&page=1) - `https://www.artic.edu/iiif/2/{id}/full/max/0/default.jpg` (see https://iiif.io/api/image/#4-image-requests)

See also [Compare image](../Algorithms/Compare%20data/Compare%20data.md#compare-image)

### Videos

- [Download Sample Videos / Dummy Videos For Demo Use](http://www.sample-videos.com/)
- [Samples - Official Kodi Wiki](http://kodi.wiki/view/Samples)
- [Beauty of Science sur Vimeo](https://vimeo.com/beautyofscience2016)
- [QuickTime Sample files - Apple Support](https://support.apple.com/en-us/HT201549)

### Test media

Test page, test card, test pattern

- [Siemens star — Wikipedia](https://en.wikipedia.org/wiki/Siemens_star)
- [Test card — Wikipedia](https://en.wikipedia.org/wiki/Test_card)
- [Category:Test cards — Wikipedia](https://en.wikipedia.org/wiki/Category:Test_cards)
- [MPEG-2 HD Test Patterns](http://www.w6rz.net/) http://www.w6rz.net/hdtestpatterns.zip
- [E1-1CD22.PDF](./Sample%20files/Test%20media/E1-1CD22.PDF)
- [EIA1956.pdf](./Sample%20files/Test%20media/EIA1956.pdf)
- [ISO_12233-reschart.pdf](./Sample%20files/Test%20media/ISO_12233-reschart.pdf)
- [High Resolution Test Patterns](http://www.bealecorner.org/red/test-patterns/)
- [Test Charts | imatest](http://www.imatest.com/products/test-charts/)
- [ISO 12233:2000 - Photography -- Electronic still-picture cameras -- Resolution measurements](http://www.iso.org/iso/catalogue_detail?csnumber=33715)
- [ISO 12233:2017 - Photography -- Electronic still picture imaging -- Resolution and spatial frequency responses](http://www.iso.org/iso/home/store/catalogue_ics/catalogue_detail_ics.htm?csnumber=71696)
- [Using eSFR ISO Part 1 | imatest](http://www.imatest.com/docs/esfriso_instructions/)
- [EIZO monitors for offices, photos & design, medicine, gaming and industry](https://www.eizo.be/monitor-test/)

### Random data

- [thinkbroadband :: Download Test Files](http://www.thinkbroadband.com/download.html)

## Endianness

Aka little endian and big endian

- [On Endianness - 🪄 Technical Sourcery](https://web.archive.org/web/20220525075029/https://www.technicalsourcery.net/posts/on-endianness/)
