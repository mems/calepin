- [OpenType: what's the difference between TTF and OTF??](https://pomax.github.io/1449438115186/opentype-what-s-the-difference-between-ttf-and-otf)
- [FontView](https://github.com/googlei18n/fontview) - Demo app that displays fonts with a free/libre/open-source text rendering stack: FreeType, HarfBuzz and Raqm
- [WOFF](../WOFF/WOFF.md)
- [Fonts](../Fonts/Fonts.md)
- [Rendering text](../../Graphics/Graphics.md#rendering-text)

- [photopea/Typr.js: Typr.js - process fonts in Javascript](https://github.com/photopea/Typr.js)
- [opentypejs/opentype.js: Read and write OpenType fonts using JavaScript.](https://github.com/opentypejs/opentype.js)

- TTF = OpenType TrueType outlines (glyf/loca data blocks)
- OTF = OpenType Type2 outlines (CFF data block)

## OpenType SVG

- https://www.w3.org/2013/10/SVG_in_OpenType/
- https://www.microsoft.com/typography/otspec/svg.htm
- https://wiki.mozilla.org/SVGOpenTypeFonts
- https://github.com/adobe-type-tools/opentype-svg

## Color

Font "Apple color Emoji" use `sbix` table format to store PNG (two sizes) for each glyphs. iOS use special [CgBI PNG format](http://iphonedevwiki.net/index.php/CgBI_file_format)

http://typophile.com/node/96671#comment-524375

> Version: 2 USHORTS, as usual for TTF tables. Version seems to be 1.1
> Num Sizes: ULONG -- 6, for Apple Color Emoji v.8.0d3e1
> numSizes * ULONG: offset for size table, relative to the start of the sbix chunk
>
> Each size table starts with
> Size USHORT
> Dpi USHORT
> The sizes in the six tables are 20, 40, 48, 64, 96, and 160 pixels (all individual images appear to be square). Dpi is '72' in all of the tables.
>
> Then follow (numChars + 1) * ULONG offsets from the start of the size table. numChars seems to be taken from the maxp table, plus 1 to add a 'last entry' file size.
>
> Each offset from the start of this table points to:
> 4 zero bytes \
> "png " / reminiscent of Apple's File Type/Creator data
> .... raw PNG data
>
> The file size of the PNG data seems to be calculated from the offset to the next image; the last one is empty.
>
> There seems to be no direct link from bitmap index to Unicode or the character map. The first 41 images seems to always be of size 0; inverse parallel to InDesign's Glyph panel, where the first 41 glyphs contain visible vector data (the bitmaps are not visible in InDesign).

COLR/CPAL: systems that support layered color TrueType fonts; this includes Windows 8.1 and later, as well as Mozilla Firefox and other Gecko-based applications running on any platform

- [How to generate colour bitmap fonts for Mac OS 10.7/8](http://typophile.com/node/103268)
- [Color bitmapfonts... thanks to Apple?! | Typophile](http://www.typophile.com/node/83760)
- [Proposed specification to add support for embedded color image glyphs in OpenType fonts](https://code.google.com/p/color-emoji/)
- [emoji sbix - Google Search](https://www.google.com/search?q=emoji+sbix)
- [mozilla/emojione-colr: EmojiOne font in COLR/CPAL layered format](https://github.com/mozilla/emojione-colr)

## Variable font

Aka dynamic style

From OpentType 1.8

- [Introducing OpenType Variable Fonts – Medium](https://medium.com/@tiro/https-medium-com-tiro-introducing-opentype-variable-fonts-12ba6cd2369)
- [The Typekit Blog | Variable fonts, a new kind of font for flexible design](http://blog.typekit.com/2016/09/14/variable-fonts-a-new-kind-of-font-for-flexible-design/)
- [Variable fonts — Wikipedia](https://en.wikipedia.org/wiki/Variable_fonts)
- [Variable Fonts on the Web | WebKit](https://webkit.org/blog/7051/variable-fonts-on-the-web/)
- [Axis-Praxis: typesetting with variable fonts (OpenType Variations)](http://www.axis-praxis.org/)
- [DECOVAR](https://github.com/typenetwork/fb-decovar) - A variable decorative sans by David Berlow
- [OpenType Font Variations Overview](https://www.microsoft.com/typography/otspec180/otvaroverview.htm)
- [Variable Fonts – Support](https://v-fonts.com/support/) - Application support of variable fonts
