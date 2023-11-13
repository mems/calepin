## Compression & Minification

Compress with optimized dictionary based alogrithms (like gzip use huffman tables): blocks, selectors, media queries, properties, values

Where some values can be the same: 0 == 0px (not every where), or 10.7125em can be 10.7em (destructive)

- [Improving compression with a preset DEFLATE dictionary](https://blog.cloudflare.com/improving-compression-with-preset-deflate-dictionary/)
- [CSS Compression : Property Name Enumeration](http://mainroach.blogspot.fr/2013/08/css-compression-property-name.html)
- [CSS Compression : Block Sorting](http://mainroach.blogspot.fr/2013/08/css-compression-block-sorting.html)
- [CSS Compression : A binary CSS format](http://mainroach.blogspot.fr/2013/07/css-compression-binary-css-format.html)
- [CSS Compression : Genetic Minification](http://mainroach.blogspot.fr/2013/07/css-compression-genetic-minification.html)
- [CSS Compression : Minifier Roulette](http://mainroach.blogspot.fr/2013/07/css-compression-minifier-roulette.html)
- [Format and Minify Your Code Online](http://www.cleancss.com/)

- [A comparison of CSS minifiers for node.js](https://github.com/GoalSmashers/css-minification-benchmark): use clean-css or [csso](https://github.com/css/csso)

## Other

- http://www.jetbrains.com/idea/webhelp/transpiling-sass-less-and-scss-to-css.html

## Tools

CSS analyzers:

- [Online CSS Code Quality Analyzer - Project Wallace](https://www.projectwallace.com/css-code-quality) - [GitHub - projectwallace/css-code-quality: Calculate the Code Quality score of your CSS based on a range of different quality guards.](https://github.com/projectwallace/css-code-quality)
- [Online CSS Analyzer - Project Wallace](https://www.projectwallace.com/analyze-css) - [GitHub - projectwallace/css-analyzer: Analytics for CSS](https://github.com/projectwallace/css-analyzer), [GitHub - projectwallace/wallace-cli: Pretty CSS analytics on the CLI](https://github.com/projectwallace/wallace-cli)

Lint:

- [GitHub - stylelint/stylelint: A mighty CSS linter that helps you avoid errors and enforce conventions.](https://github.com/stylelint/stylelint) - [Home | Stylelint](https://stylelint.io/)
- [GitHub - projectwallace/constyble: CSS complexity linter](https://github.com/projectwallace/constyble) - [Introducing Gromit - Blog - Project Wallace](https://www.projectwallace.com/blog/introducing-gromit)
- [\[brothercake\] Dust-Me Selectors](https://www.brothercake.com/dustmeselectors/) - [Dust-Me Selectors :: Add-ons for Firefox](https://web.archive.org/web/20160822063704/https://addons.mozilla.org/en-US/firefox/addon/dust-me-selectors/?src=external-brothercake),  https://web.archive.org/web/20181017204310if_/https://addons.cdn.mozilla.net/user-media/addons/5392/dust_me_selectors-4.1-fx.xpi?filehash=sha256:194e6542067d4bca9b4a5b68a0b37c596f5cc0bb2f309a69800f8dd3f866f709

Prettier:

- [Online CSS Prettifier - Project Wallace](https://www.projectwallace.com/prettify-css)

Prefixes:

- [Autoprefixer CSS online](https://autoprefixer.github.io/) - [postcss/autoprefixer: Parse CSS and add vendor prefixes to rules by Can I Use](https://github.com/postcss/autoprefixer)

Transform CSS/preprocessor:

- [postcss/postcss: Transforming styles with JS plugins](https://github.com/postcss/postcss)
- [peteboere/css-crush: CSS preprocessor.](https://github.com/peteboere/css-crush) - [CSS-Crush. CSS preprocessor](https://the-echoplex.net/csscrush/) with PHP
- [reworkcss/rework: Plugin framework for CSS preprocessing in Node.js](https://github.com/reworkcss/rework), and [segmentio/myth: A CSS preprocessor that acts like a polyfill for future versions of the spec.](https://github.com/segmentio/myth) based on rework
- [Sass, SCSS, and Less | IntelliJ IDEA Documentation](https://www.jetbrains.com/help/idea/transpiling-sass-less-and-scss-to-css.html)
- [debba/less2scss: Convert less files in scss on the fly.](https://github.com/debba/less2scss)
- [ekryski/less2sass: A little script to convert less to sass files](https://github.com/ekryski/less2sass)

Deadcode elimination:

- [uncss/uncss: Remove unused styles from CSS](https://github.com/uncss/uncss)

Parser:

- [postcss/benchmark: PostCSS benchmarks](https://github.com/postcss/benchmark#parsers) - Parsers benchmark
- [tabatkins/parse-css: :horse_racing: Standards-based CSS Parser](https://github.com/tabatkins/parse-css)
- [JSCSSP, a CSS parser in JavaScript](http://glazman.org/JSCSSP/)
- [CSSTidy](https://csstidy.sourceforge.net/)
- [sabberworm/PHP-CSS-Parser: A Parser for CSS Files written in PHP. Allows extraction of CSS files into a data structure, manipulation of said structure and output as (optimized) CSS](https://github.com/sabberworm/PHP-CSS-Parser)
- [csstree/csstree: A tool set for CSS including fast detailed parser, walker, generator and lexer based on W3C specs and browser implementations](https://github.com/csstree/csstree)
- [fb55/css-select: a CSS selector compiler & engine](https://github.com/fb55/css-select)
- [csscomb/csscomb: Tool for sorting CSS properties](https://github.com/csscomb/csscomb/tree/master)
- [tonyganch/gonzales-pe: CSS parser with support of preprocessors](https://github.com/tonyganch/gonzales-pe)
- [mck89/PAHDI: PAHDI (PHP Advanced HTML DOM Implementation) is a library that provides an advanced implementation of the Document Object Model in PHP starting from HTML code](https://github.com/mck89/PAHDI/tree/master) - [PAHDI/src/Parser/CSS/Builder.php at master · mck89/PAHDI](https://github.com/mck89/PAHDI/blob/master/src/Parser/CSS/Builder.php)

Other:

- [csscomb/csscomb.js: CSS coding style formatter](https://github.com/csscomb/csscomb.js) - based on Gonzales PE

## Preprocessor

- [Why I switched from LESS to Sass | Kitty Giraudel](https://kittygiraudel.com/2012/11/13/why-i-switched-from-less-to-sass/)
- [Converting from LESS to Sass - MStrutt.co.uk](https://web.archive.org/web/20220516143748/https://mstrutt.co.uk/blog/2013/08/converting-from-less-to-sass/#making-the-switch)
- [How To Convert from Less to Sass | Sprout Social](https://web.archive.org/web/20230529063826/https://sproutsocial.com/insights/less-to-sass/)
