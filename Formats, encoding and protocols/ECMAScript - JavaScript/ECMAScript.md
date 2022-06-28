Aka JavaScript (ECMAScript + DOM and Web APIs),

- http://msdn.microsoft.com/en-us/library/ie/121hztk3%28v=vs.94%29.aspx
- http://wiki.ecmascript.org/doku.php?id=resources:resources&s=conditional+compilation#microsoft_drafts

- [Jison](http://zaa.ch/jison/) - "Your friendly JavaScript parser generator!"

- http://en.wikipedia.org/wiki/Preprocessor
- http://en.wikipedia.org/wiki/C_preprocessor
- http://code.google.com/p/jspp/
- https://code.google.com/p/jsmake-preprocessor/
- http://js-preprocessor.com/
- http://www.nongnu.org/espresso/js-cpp.html
- https://github.com/mcoolin/Node-JavaScript-Preprocessor

- http://en.wikipedia.org/wiki/Abstract_syntax_tree
- https://developer.mozilla.org/en-US/docs/SpiderMonkey/Parser_API
- http://code.google.com/p/redtamarin/wiki/ABC
- https://learn.adobe.com/wiki/display/AVM2/4.+The+ActionScript+Byte+Code+%28abc%29+format

- [JSZap: Compressing JavaScript Code](http://research.microsoft.com/apps/pubs/?id=120832) (see also https://www.usenix.org/conference/webapps-10/jszap-compressing-javascript-code)

- http://creativejs.com/2012/06/jsexe-javascript-compressor/
- http://www.pouet.net/prod.php?which=59298
- [jssfx3](https://code.google.com/p/jssfx/) (see also http://skypher.com/index.php/2010/12/09/jssfx3/)
- [CrunchMe](http://crunchme.bitsnbites.eu/)
- http://mainroach.blogspot.fr/2013/09/extreme-javascript-minimization.html
- http://www.2ality.com/2011/01/what-is-javascript-equivalent-of-java.html
- http://www.2ality.com/2012/01/bytecode-myth.html

## Parser

- [jsparagus/js-quirks.md at master · mozilla-spidermonkey/jsparagus](https://github.com/mozilla-spidermonkey/jsparagus/blob/master/js-quirks.md#readme) - Why JavaScript syntax is hard to parse
- [parsing - Source](https://source.chromium.org/chromium/chromium/src/+/master:v8/src/parsing/) - V8
- [UglifyJS](https://github.com/mishoo/UglifyJS)
- [JSMin](http://www.crockford.com/javascript/jsmin.html)
- [Google Closure Compiler](https://developers.google.com/closure/compiler/)
- [Extreme Javascript Minimization](http://mainroach.blogspot.fr/2013/09/extreme-javascript-minimization.html)
- [ESTree](https://github.com/estree/estree) - ESTree Spec. Common format for ECMAScript tokens
- [pvdz/tenko: An 100% spec compliant ES2020 JavaScript parser written in JS](https://github.com/pvdz/tenko)
- [Esprima](http://esprima.org/) - ECMAScript parser written in ECMAScript. See https://github.com/jquery/esprima and [benjamn/recast: JavaScript syntax tree transformer, nondestructive pretty-printer, and automatic source map generator](https://github.com/benjamn/recast)
- [acornjs/acorn: A small, fast, JavaScript-based JavaScript parser](https://github.com/acornjs/acorn)
- [engine262/engine262 at parser](https://github.com/engine262/engine262/tree/parser)
- [webkit/Source/JavaScriptCore/parser at master · WebKit/webkit](https://github.com/WebKit/webkit/tree/master/Source/JavaScriptCore/parser)
- [KFlash/seafox: A blazing fast 100% spec compliant, self-hosted javascript parser written in Typescript](https://github.com/KFlash/seafox)
- [babel/packages/babel-parser at master · babel/babel](https://github.com/babel/babel/tree/master/packages/babel-parser) - Babel JS parser (previously Babylon), [@babel/parser · Babel](https://babeljs.io/docs/en/babel-parser)
- [swc-project/swc: Rust-based platform for the Web](https://github.com/swc-project/swc)

## Engine

- V8
	- Node.js
	- Google Chrome
	- [Everyone can now run JavaScript on Cloudflare with Workers](https://blog.cloudflare.com/cloudflare-workers-unleashed/)
- [Microsoft/ChakraCore: ChakraCore is the core part of the Chakra Javascript engine that power Microsoft Edge](https://github.com/Microsoft/ChakraCore)
	- [nodejs/node-chakracore: Node.js on ChakraCore](https://github.com/nodejs/node-chakracore)
	- Microsoft Edge

## Editor

It's will help you to found errors before you try/compile your code.

- IntelliJ IDEA / WebStorm
- [JSLint](http://www.jslint.com/)
- [JSHint](http://www.jshint.com/)

## Tools

- [gulp/browserify-uglify-sourcemap.md at master · gulpjs/gulp](https://github.com/gulpjs/gulp/blob/master/docs/recipes/browserify-uglify-sourcemap.md)
- [JavaScript Obfuscator Tool](https://obfuscator.io/) - [javascript-obfuscator/javascript-obfuscator: A powerful obfuscator for JavaScript and Node.js](https://github.com/javascript-obfuscator/javascript-obfuscator)
- [facebook/jscodeshift: A JavaScript codemod toolkit.](https://github.com/facebook/jscodeshift) - Use [recast](https://github.com/benjamn/recast). Exemple to [remove asyncs and switch promises to statements](https://astexplorer.net/#/gist/b8e4e9313c4805a8928d9a199e3c9b7e/e0f298d99d81976061f5dcc0727d2e8e656d7261)
- [benjamn/recast: JavaScript syntax tree transformer, nondestructive pretty-printer, and automatic source map generator](https://github.com/benjamn/recast)

### Unuglify

- [Unminify JS, CSS, HTML, XML and JSON Code](https://unminify.com/)
- [eth-sri/UnuglifyJS: A simpler open-source version of JavaScript deobfuscator JSNice](https://github.com/eth-sri/UnuglifyJS)
- [JS NICE: Statistical renaming, Type inference and Deobfuscation](http://jsnice.org/)
	[JSNice artifact instructions](https://files.sri.inf.ethz.ch/jsniceartifact/index.html)
- [Nice2Predict](http://nice2predict.org/)
- [Online JavaScript beautifier](https://beautifier.io/)
