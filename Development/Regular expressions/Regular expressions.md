Aka regex, regexp

A regex is a function with subroutines (instruction)

- [devongovett/regexgen: Generate regular expressions that match a set of strings](https://github.com/devongovett/regexgen)
- [fent/randexp.js: Create random strings that match a given regular expression.](https://github.com/fent/randexp.js)
- IrRegex [Irregexp | Hummus and Magnets](http://h14s.p5r.org/2009/02/irregexp.html)
- [YARR! - Yet Another Regex Runtime](https://trac.webkit.org/browser/trunk/Source/JavaScriptCore/yarr)
- [Comparison of regular-expression engines - Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_regular-expression_engines)
- [wregex - How Regular Expression Engines Work](http://wstoop.co.za/wregex.php)
- [Regexper](https://regexper.com/) - [javallone/regexper-static: Regular Expression Visualization Site (static site version)](https://github.com/javallone/regexper-static)
- [Email Address Regular Expression That 99.99% Works.](http://emailregex.com/)

W3C [HTML 5.2: 4.10. Forms](https://www.w3.org/TR/html/sec-forms.html#valid-e-mail-address) (see also [HTML 5.1 2nd Edition: 4.10. Forms](https://www.w3.org/TR/html51/sec-forms.html#valid-e-mail-address)) regular expression for email fields:

```regexp
/^[a-zA-Z0-9.!#$%&'*+\/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$/
```

A match is faster. Try all execution paths start at each char is very long.
Regular Expression engines always find the cheapest (simpliest, shortest) first match: "Always matches as early possible in string on leftmost possible alternative in regex"

## Documentation and tools

- [Online regex tester and debugger: PHP, PCRE, Python, Golang and JavaScript](https://regex101.com/)
- [RegExr: Learn, Build, & Test RegEx](https://regexr.com/)
- [Regulex：JavaScript Regular Expression Visualizer](https://jex.im/regulex/)
- [Debuggex: Online visual regex tester. JavaScript, Python, and PCRE.](https://www.debuggex.com/)
- [Regexper](https://regexper.com/)
- [txt2re: headache relief for programmers :: regular expression generator](https://www.txt2re.com/index_php3.html) - Regular expression from text
- [Refiddle](http://refiddle.com/)

- [VerbalExpressions](https://github.com/VerbalExpressions) - "Regular Expressions made easy" with library to build regular expression: `VerEx().startOfLine().then("http").maybe("s").then("://").maybe("www.").anythingBut(" ").endOfLine()` gives `/^(http)(s)?(\:\/\/)(www\.)?([^\ ]*)$/`
- [Understanding and Using Regular Expressions](https://www.infoq.com/presentations/regex) - [Understanding and Using Regular Expressions by Damian Conway](https://videoh.infoq.com/presentations/14-mar-regularexpressions-B.mp4?Key-Pair-Id=APKAIMZVI7QH4C5YKH6Q&Signature=BZMZnJA751nsDqL5iT7mtyspeSDzrQZTYeuh363H~ijASn11EL0e1~SehHoWaylFeCxwqjXgECdcff6blWouQR16ZsHkYRQHYPrqPzSxp27UHzA1Y3O-aNJF6RlADXuDW5TUPAbTROm8ByJN1vGldfF0Qe8tIQ7-k7ALqZK9mgs_&Policy=eyJTdGF0ZW1lbnQiOiBbeyJSZXNvdXJjZSI6IioiLCJDb25kaXRpb24iOnsiRGF0ZUxlc3NUaGFuIjp7IkFXUzpFcG9jaFRpbWUiOjE0ODg5NzI1Mzh9LCJJcEFkZHJlc3MiOnsiQVdTOlNvdXJjZUlwIjoiMC4wLjAuMC8wIn19fV19)
- [Regex Crossword](https://regexcrossword.com/) - Game with regexp
- [Regular-Expressions.info - Regex Tutorial, Examples and Reference - Regexp Patterns](https://www.regular-expressions.info/)

## Non-greedy quantifier

Aka lazy quantifier

> _Greedy_ means match longest possible string.
> _Lazy_ means match shortest possible string.

Usefull for enclosed match (attribute value, text in quotes)

```regexp
/("|')(.*?)(\1)/g
```

- [DasSur.ma – My most useful RegExp trick](https://dassur.ma/things/regexp-quote/)
- [regex - What do 'lazy' and 'greedy' mean in the context of regular expressions? - Stack Overflow](https://stackoverflow.com/questions/2301285/what-do-lazy-and-greedy-mean-in-the-context-of-regular-expressions)

## Lookbehind and lookahead

Assert but doesn't match: _zero-width assertion_.

- lookbehind `(?<=a)bc`, `(?<!a)bc`
- lookahead `ab(?=c)`, `ab(?!c)`

- [ES2018: RegExp lookbehind assertions](http://2ality.com/2017/05/regexp-lookbehind-assertions.html)

## Exclude

```regexp
^(?!(class|image|instanceof)$).*$
```

Use lookbehind to exlude full match keywords.

Will match:

- `test`
- `images`
- `some-image`

But not:

- `class`
- `image`

## Optimization

Reduce backtracking to improve performance. Especially with nested quantifiers. Have an impact on performance (if not crash or throw an error)

Because backtracking have a huge impact on regex, it could be used to make [ReDoS](https://en.wikipedia.org/wiki/ReDoS)

Instead `/'.*'/`, use `/'.*?'/` (`/'.*?'/.test("You say 'tomayto' ...but I say 'tomahto'")`) only if the rest after the match in the string is very long vs the length of the match

Ex. 1: For a trim using regexp: `/^[\s\u200c]+|[\s\u200c]+$/g` or `/^[\s\uFEFF\xA0]+|[\s\uFEFF\xA0]+$/g` on with a string contains (not at the begin nor the end) 20000 consecutive whitespaces, the RegExp engine will track it 200,010,000 times = 20,000+19,999+19,998+…+3+2+1

Replace with `substring`.

See [Stack Exchange Network Status — Outage Postmortem - July 20, 2016](http://stackstatus.net/post/147710624694/outage-postmortem-july-20-2016)

Ex. 2: `(\w+?\d*,)*` `\w` will match `\d` too, the engine try differents approches. `AA00,` can be matched with `\w\w\d\d,` but with `\w\w\w\d,` or `\w\w\w\w,`. When the engine can't match the next occurence, it try differents possibilities. 2^N:
`AA00,BB11,CC22` give `\w\w\d\d,\w\w\d\d,`, `\w\w\w\d,\w\w\d\d,`, `\w\w\w\w,\w\w\d\d,`, `\w\w\w\w,\w\w\w\d,`,  `\w\w\d\d,\w\w\w\d,`, `\w\w\d\d,\w\w\w\w,`, `\w\w\w\d,\w\w\w\w,`...

Use `([^\W\d]+?\d*,)*` or `(((?!\d)\w)+?\d*,)*` instead to always select char (not digit) first then digit, or use atomic group: `(?>\w+?\d*,)*` (aka "do not change backtrack match")

See [Catastrophic Backtracking ‒ When Regular Expressions Explode on Vimeo](https://vimeo.com/112065252)

- [Infinite backtracking problem | JavaScript Tutorial](http://javascript.info/tutorial/infinite-backtracking-problem)
- [javascript - How can I make this regular expression not result in "catastrophic backtracking"? - Stack Overflow](https://stackoverflow.com/questions/10218594/how-can-i-make-this-regular-expression-not-result-in-catastrophic-backtracking)
- [Backtracking in Regular Expressions](https://msdn.microsoft.com/en-us/library/dsy130b4(v=vs.110).aspx)
- [Flagrant Badassery » Performance of Greedy vs. Lazy Regex Quantifiers](http://blog.stevenlevithan.com/archives/greedy-lazy-performance)
- [Simple Regex Engine in JavaScript (Backtracking Algorithm)](https://github.com/richardartoul/regex-engine)
- [Catastrophic Backtracking—Exponential Matches—ReDos](http://www.rexegg.com/regex-explosive-quantifiers.html)
- [Runaway Regular Expressions: Catastrophic Backtracking](http://www.regular-expressions.info/catastrophic.html)

## Comments

With the `x` flag.

```regexp
^(?:(?!ab).)+$
```

```regexp
(?x)    # enable regex comment mode
^       # match start of line/string
(?:     # begin non-capturing group
  (?!   # begin negative lookahead
    ab  # literal text sequence ab
  )     # end negative lookahead
  .     # any single character
)       # end non-capturing group
+       # repeat previous match one or more times
$       # match end of line/string
```

- [DmitrySoshnikov/babel-plugin-transform-modern-regexp: Babel plugin for modern RegExp features in JavaScript](https://github.com/DmitrySoshnikov/babel-plugin-transform-modern-regexp#extended-x-flag)
- [New flags :: XRegExp](http://xregexp.com/flags/)
- [javascript - Commenting Regular Expressions - Stack Overflow](https://stackoverflow.com/questions/15463257/commenting-regular-expressions)
- [RegExp `x` flag](https://esdiscuss.org/topic/regexp-x-flag)
