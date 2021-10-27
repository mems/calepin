- [Unique identifier — Wikipedia](https://en.wikipedia.org/wiki/Unique_identifier)
- [International Bank Account Number — Wikipedia](https://en.wikipedia.org/wiki/International_Bank_Account_Number)

Data sets:

- [Insee - National Institute of Statistics and Economic Studies](https://www.insee.fr/en/accueil)
- [An awesome list of high-quality open datasets in public domains](https://github.com/caesar0301/awesome-public-datasets)
- [Wikidata](https://www.wikidata.org/wiki/Wikidata:Main_Page) - see [How to Extract Data from Wikipedia and Wikidata // Link To Sheets](https://linktosheets.com/extract-data-from-wikipedia-wikidata/) and [maxlath/wikidata-sdk: A javascript tool-suite to query Wikidata and simplify its results](https://github.com/maxlath/wikidata-sdk)
- [Data Packaged Core Datasets](https://github.com/datasets) - see [Core Datasets - Frictionless Open Data](http://data.okfn.org/roadmap/core-datasets)
- [Datasets | Kaggle](https://www.kaggle.com/datasets)

- [Category:Fictional brands — Wikipedia](https://en.wikipedia.org/wiki/Category:Fictional_brands)
- [Fictional brand — Wikipedia](https://en.wikipedia.org/wiki/Fictional_brand)

Other:

- [Curated list of falsehoods programmers believe in](https://github.com/kdeldycke/awesome-falsehood)
- [Digital asset management — Wikipedia](https://en.wikipedia.org/wiki/Digital_asset_management)
- [Content Management Interoperability Services — Wikipedia](https://en.wikipedia.org/wiki/Content_Management_Interoperability_Services)
- [GraphQL | A query language for your API](http://graphql.org/)

## Human

- [OSINT Search Tool by IntelTechnique | Open Source Intelligence](https://inteltechniques.com/menu.html)
- [Michael Bazzell' Blog  » Blog Archive   » Updated OSINT Flowcharts](https://inteltechniques.com/blog/2018/03/06/updated-osint-flowcharts/)
- [Person](./Person/Person.md)

## File

> Path delimiters aren't the same across platforms (/ on \*nix, \\ on windows). A trailing slash may or may not mean the same thing depending on what operation you're doing. Not all platforms allow or disallow the same characters in directory or filenames. Quoting and escaping spaces in a path name is done differently on different platforms. Multiple delimiters in a row may mean nothing in the file system (e.g. `/usr/bin` and `/usr////bin` may be the same path) but splitting those on `/` will yield different results.
>
> In addition, some special paths like 8+3 short names `(C:\>LONGDI~1.COM)` include special characters that may not be legal on some platforms. Shortcuts for a home directory like `~` aren't always the same. Etc.
>
> Using string functions or regexes will break and/or not handle things properly.
>
> In other words a path isn't just a string, it's a thing (an object) with semantics and behaviors that are best parsed by a library, which handles all the edge cases and implements all the POSIX/ISO/RFC crap and is well tested so you don't have to worry about it. Just like validating an email address!
>
> Python and PHP have good path libraries. Perl and Ruby too I think. Many of those also handle URI formats like `scheme://user@host:port/path/resource` with `password` somewhere in there.
>
> ---
>
> The amount of people who don't realize `\directory\directory\file` is a valid and absolute path on Windows, or what it means, is too damn high.
>
> Also `\\?\UNC\` and other fun stuff.
>
> — [commentaires de BundleOfJoysticks sur BREAKING!! NPM package ‘ua-parser-js’ with more than 7M weekly download is compromised](https://old.reddit.com/r/programming/comments/qdlela/breaking_npm_package_uaparserjs_with_more_than_7m/hhpm8z0/)


