> The characters “U+” are an ASCIIfied version of the MULTISET UNION “⊎” U+228E character (the U-like union symbol with a plus sign inside it), which was meant to symbolize Unicode as the union of character sets
>
> — [codepoint - Why is 'U+' used to designate a Unicode code point? - Stack Overflow](https://stackoverflow.com/questions/1273693/why-is-u-used-to-designate-a-unicode-code-point/8891122#8891122)

- [A Programmer’s Introduction to Unicode – Nathan Reed’s coding blog](http://reedbeta.com/blog/programmers-intro-to-unicode/)
- [The Absolute Minimum Every Software Developer Absolutely, Positively Must Know About Unicode and Character Sets (No Excuses!) – Joel on Software](https://web.archive.org/web/20201212114246/https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/)

## Composite and Precomposed Characters

> Unicode contains a vast number of characters, many of which have different Unicode numbers, but are in fact the same character. A simple example is the letter _e-acute_: this can be represented by _é_, which in UTF-8 encoding is the two hex bytes `c3 a9`, or by _é_, which is the three hex bytes `65 cc 81`. In some fonts there may be small differences, but in most cases we see identical characters and expect our computers to treat them the same.

> é and é

- [janlelis/uniscribe: Debug help for Unicode strings](https://github.com/janlelis/uniscribe)
- [Precomposed character — Wikipedia](https://en.wikipedia.org/wiki/Precomposed_character)
- [Technical Q&A QA1235: Converting to Precomposed Unicode](https://developer.apple.com/library/mac/qa/qa1235/_index.html)
- [Unicode equivalence — Wikipedia](https://en.wikipedia.org/wiki/Unicode_equivalence#Normalization)
- [Dark corners of Unicode / fuzzy notepad](https://eev.ee/blog/2015/09/12/dark-corners-of-unicode/)
- [UAX #15: Unicode Normalization Forms](http://unicode.org/reports/tr15/)
- [How to normalise strings, and a new command tool to help – The Eclectic Light Company](https://eclecticlight.co/2017/04/10/how-to-normalise-strings-and-a-new-command-tool-to-help/)
- Apfelstrudel, [Downloads – The Eclectic Light Company](https://eclecticlight.co/downloads/)

Normalization forms:

- NFC: Precomposed string with canonical mapping
- NFD: Decomposed string with canonical mapping
- NFKC: Precomposed string with compatibility mapping
- NFKD: Decomposed string with compatibility mapping
