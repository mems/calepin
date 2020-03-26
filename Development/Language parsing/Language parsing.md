- [RFC 5234 - Augmented BNF for Syntax Specifications: ABNF](https://tools.ietf.org/html/rfc5234)
- [Extended Backus–Naur form — Wikipedia](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form)
- [Augmented Backus–Naur form — Wikipedia](https://en.wikipedia.org/wiki/Augmented_Backus%E2%80%93Naur_form)
- [Java SE Specifications](https://docs.oracle.com/javase/specs/)
- [PHP: List of Parser Tokens - Manual](http://www.php.net/manual/en/tokens.php)
- BNF for specific URL schemes [RFC 1738 - A Gopher URL Format](https://tools.ietf.org/html/rfc1738#section-5) (see also RFC updates [RFC 1738](https://datatracker.ietf.org/doc/rfc1738/))
- [Antidote 9 | Druide informatique inc.](http://www.antidote.info/antidote/caracteristiques)
- [GOLD Parsing System - Grammar Downloads](http://goldparser.org/grammars/index.htm)
- [Syntax (programming languages) — Wikipedia](https://en.wikipedia.org/wiki/Syntax_%28programming_languages%29)

About parsing and transpiling:

- [jamiebuilds/the-super-tiny-compiler: Possibly the smallest compiler ever](https://github.com/jamiebuilds/the-super-tiny-compiler)
- [Compiling Java and C# to SWF – blog.joa-ebert.com - Blog of Joa Ebert](https://blog.joa-ebert.com/2009/09/28/compiling-java-and-c-to-swf/)
- [How to be* a compiler — make a compiler with JavaScript – Medium](https://medium.com/@kosamari/how-to-be-a-compiler-make-a-compiler-with-javascript-4a8a13d473b4#.4mds8vf0s)
- [Easy Parsing with Parser Combinators](http://www.lihaoyi.com/post/EasyParsingwithParserCombinators.html)
- [Implementing a programming language in C - Part 1](http://wayback.archive.org/web/20150610090835/http://www.vnev.me/implementing-a-programming-language-in-c-part-1/)
- [Parsing CSS in JavaScript / jQuery - Stack Overflow](https://stackoverflow.com/questions/3326494/parsing-css-in-javascript-jquery/3326538#3326538)
- use source maps [Compiling to JavaScript, and Debugging with Source Maps ★ Mozilla Hacks – the Web developer blog](https://hacks.mozilla.org/2013/05/compiling-to-javascript-and-debugging-with-source-maps/)
- [How to Writing a parser](http://www.tcx.be/how-to/#parser)
- [Writing Your Own Toy Compiler Using Flex, Bison and LLVM (gnuu.org)](http://gnuu.org/2009/09/18/writing-your-own-toy-compiler/)
- [Free Compiler Construction Tools: Lexers, Parser Generators, Optimizers (thefreecountry.com)](http://www.thefreecountry.com/programming/compilerconstruction.shtml)
- [CmSc 315 Programming Languages](http://faculty.simpson.edu/lydia.sinapova/www/cmsc315/LN315_Pratt/ContentsLN315.htm)
- [Peachpie – The open-source PHP compiler to .NET](http://www.peachpie.io/)
- [niklasvh/php.js: PHP to JavaScript converter and VM written in JavaScript](https://github.com/niklasvh/php.js)
- [Crafting Interpreters](https://craftinginterpreters.com/) - [munificent/craftinginterpreters: Repository for the book "Crafting Interpreters"](https://github.com/munificent/craftinginterpreters)
- [Building a Scanner – Chelsea Troy](https://chelseatroy.com/2019/10/24/building-a-scanner/)
- [Building a Parser – Chelsea Troy](https://chelseatroy.com/2019/11/11/building-a-parser/)
- [Drawings of How Compilers Work – Chelsea Troy](https://chelseatroy.com/2019/10/17/drawings-of-how-compilers-work/)
- [Stuff I Wrote About Programming Languages – journal.stuffwithstuff.com](http://journal.stuffwithstuff.com/category/language/)
- [JSON Parser with JavaScript | Tan Li Hau](https://lihautan.com/json-parser-with-javascript/) - [Write a parser with JavaScript | Hacker News](https://news.ycombinator.com/item?id=21772336)

Concepts:

**Long switch in a loop, can be used for state machine, but it's not adviced to use long switch for parsing,** because it's often need multiple states (to restore previous ones). Use [recursive descent parser](https://en.wikipedia.org/wiki/Recursive_descent_parser) instead.

- [Parsing — Wikipedia](https://en.wikipedia.org/wiki/Parsing)
- [Parse tree — Wikipedia](https://en.wikipedia.org/wiki/Parse_tree)
- [Abstract syntax tree — Wikipedia](https://en.wikipedia.org/wiki/Abstract_syntax_tree)
- [Analyse syntaxique — Wikipédia](https://fr.wikipedia.org/wiki/Analyse_syntaxique)
- [Lexical analysis — Wikipedia](https://en.wikipedia.org/wiki/Lexical_analysis)
- [Lint (software) — Wikipedia](https://en.wikipedia.org/wiki/Lint_%28software%29)
- [Parsing expression grammar — Wikipedia](https://en.wikipedia.org/wiki/Parsing_expression_grammar)
- [CSS parsing: performance tips & tricks](https://www.slideshare.net/basisjs/css-parsing-performance-tips-tricks)
- [postcss/architecture.md at master · postcss/postcss](https://github.com/postcss/postcss/blob/master/docs/architecture.md)

Generators:

- [Comparison of parser generators — Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_parser_generators)
- [PEG.js – Parser Generator for JavaScript](https://pegjs.org/) - see [PEG.js: Parser generator for JavaScript](https://github.com/pegjs/pegjs)
- [re2c — re2c 0.16 documentation](http://re2c.org/)
- [fastparse: Writing Fast Parsers Fast in Scala](https://github.com/lihaoyi/fastparse)
- [Jison](http://zaa.ch/jison/) - Bison in JavaScript / JavaScript parser generator. See https://github.com/zaach/jison
- [A Parser Combinator library for C ](https://github.com/orangeduck/mpc)
- [Build parsers in Java](https://github.com/jparsec/jparsec)
- [tree-sitter/tree-sitter: An incremental parsing system for programmings tools](https://github.com/tree-sitter/tree-sitter)
- [SAP/chevrotain: Parser Building Toolkit for JavaScript](https://github.com/SAP/chevrotain)

Examples:

- [tree-sitter/tree-sitter: An incremental parsing system for programming tools](https://github.com/tree-sitter/tree-sitter)
- [retextjs/retext: Natural language processor powered by plugins based on @unifiedjs (and @vfile, @syntax-tree)](https://github.com/retextjs/retext) - Natural language parser (latin, english, etc.)
- [shift-regexp-acceptor-js/index.js at es2016 · shapesecurity/shift-regexp-acceptor-js](https://github.com/shapesecurity/shift-regexp-acceptor-js/blob/es2016/src/index.js)
- [Esprima](http://esprima.org/) - ECMAScript parser written in ECMAScript. See https://github.com/jquery/esprima
- JSCSSP written by Daniel Glazman
	- [therealglazou/jscssp: a fast and extensible CSS parser written in JavaScript](https://github.com/therealglazou/jscssp)
	- [JSCSSP, a CSS parser in JavaScript](http://glazman.org/JSCSSP/)
	- [therealglazou/JSCSSPHX](https://github.com/therealglazou/JSCSSPHX)
	- https://dxr.mozilla.org/mozilla-central/source/layout/style/nsCSSParser.cpp
	- https://dxr.mozilla.org/mozilla-central/source/layout/style/nsCSSScanner.cpp
	- [NV/CSSOM: CSS Object Model implemented in pure JavaScript. It's also a parser!](https://github.com/NV/CSSOM)
- [Mascara JavaScript Compiler](http://www.mascaraengine.com/) - see also [News - Mascara - The JavaScript of the future, today](http://blog.mascaraengine.com/)
- [Classes.Math Parser - JSFromHell.com: JavaScript Repository](http://jsfromhell.com/classes/math-parser)
- [Parser API - Mozilla | MDN](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/SpiderMonkey/Parser_API)
- [GLSL to HLSL transpiler code](https://github.com/MicrosoftEdge/WebGL/tree/master/GLSLParse)
- [Parse, Analyse, Clean GLSL code in JS](https://github.com/zz85/glsl-cleaner/)
- [Jsmn is a world fastest JSON parser/tokenizer](https://github.com/zserge/jsmn/blob/master/jsmn.c)
- [Very low footprint JSON parser written in portable ANSI C](https://github.com/udp/json-parser/blob/master/json.c)
- [Super-fast Java JSON parser](https://github.com/mitchhentges/json-parse/blob/master/src/main/java/ca/fuzzlesoft/JsonParse.java)
- [MBED3 port of Lightweight Embedded JSON Parser](https://github.com/warmcat/lejp/blob/master/source/lejp.c) 
- [A fast and small JSON parser and writer for Java](https://github.com/ralfstx/minimal-json/blob/master/com.eclipsesource.json/src/main/java/com/eclipsesource/json/JsonParser.java)
- [pvdz/tenko: An 100% spec compliant ES2020 JavaScript parser written in JS](https://github.com/pvdz/tenko)

Use `goto`s, "This is called computed (or assigned) goto and is a GCC extension"
- https://github.com/quartzjer/js0n/blob/master/src/js0n.c 
- https://gcc.gnu.org/onlinedocs/gcc/Labels-as-Values.html
- https://news.ycombinator.com/item?id=4387156

Syntax exemples:

	foobar : "foo" | "bar";

	// (4 * 2 * 11 + 2) - 5
	// 29 + 2 * 3 - 99 - (5 + 5 + 2) / 100
	expression : <product> (('+' | '-') <product>)*;
	product : <value>   (('*' | '/')   <value>)*;
	value : /[0-9]+/ | '(' <expression> ')';
	maths : /^/ <expression> /$/;

	// so c so c so c so c so c so c so c so c so c
	// wow c so language such book 
	adjective : "wow" | "many" | "so" | "such";
	noun      : "lisp" | "language" | "c" | "book" | "build";
	phrase    : <adjective> <noun>;
	doge      : /^/ <phrase>* /$/;

	ident     : /[a-zA-Z_][a-zA-Z0-9_]*/ ;
	number    : /[0-9]+/ ;
	character : /'.'/ ;
	string    : /\"(\\\\.|[^\"])*\"/ ;
	
	factor    : '(' <lexp> ')'
	          | <number>
	          | <character>
	          | <string>
	          | <ident> '(' <lexp>? (',' <lexp>)* ')'
	          | <ident> ;
	
	term      : <factor> (('*' | '/' | '%') <factor>)* ;
	lexp      : <term> (('+' | '-') <term>)* ;
	
	stmt      : '{' <stmt>* '}'
	          | \"while\" '(' <exp> ')' <stmt>
	          | \"if\"    '(' <exp> ')' <stmt>
	          | <ident> '=' <lexp> ';'
	          | \"print\" '(' <lexp>? ')' ';'
	          | \"return\" <lexp>? ';'
	          | <ident> '(' <ident>? (',' <ident>)* ')' ';' ;
	
	exp       : <lexp> '>' <lexp>
	          | <lexp> '<' <lexp>
	          | <lexp> \">=\" <lexp>
	          | <lexp> \"<=\" <lexp>
	          | <lexp> \"!=\" <lexp>
	          | <lexp> \"==\" <lexp> ;
	
	typeident : (\"int\" | \"char\") <ident> ;
	decls     : (<typeident> ';')* ;
	args      : <typeident>? (',' <typeident>)* ;
	body      : '{' <decls> <stmt>* '}' ;
	procedure : (\"int\" | \"char\") <ident> '(' <args> ')' <body> ;
	main      : \"main\" '(' ')' <body> ;
	includes  : (\"#include\" <string>)* ;
	smallc    : /^/ <includes> <decls> <procedure>* <main> /$/ ;

	node : '(' <node> ',' /foo/ ',' <node> ')' | <leaf>;
	leaf : /bar/;
	input : /^/ <node> /$/;

	
	number  \"number\"  : /[0-9]+/ ;
	symbol  \"symbol\"  : /[a-zA-Z0-9_+\\-*\\/\\\\=<>!&]+/ ;
	string  \"string\"  : /\"(\\\\.|[^\"])*\"/ ;
	comment             : /;[^\\r\\n]*/ ;
	sexpr               : '(' <expr>* ')' ;
	qexpr               : '{' <expr>* '}' ;
	expr                : <number>  | <symbol> | <string>
	                    | <comment> | <sexpr>  | <qexpr> ;
	lispy               : /^/ <expr>* /$/ ;

	// #line 10 "test"
	number        : /[0-9]+/ ;
	quoted_string : /\"(\\.|[^\"])*\"/ ;
	linepragma    : <line> <number> <quoted_string>;
	parser        : /^/ (<linepragma>)* /$/ ;

	// [my_func]\n  echo (a b c)\n
	qscript        : /^/ (<comment> | <resource>)* /$/ ;
		comment     : '#' /[^\\n]*/ ;
	resource       : '[' (<rtype> <rname>) ']' <inner_block> ;
		rtype       : /[*]*/ ;
		rname       : <qstring> ;
	
	inner_block    : (<comment> | <statement>)* ;
		statement   : <function> '(' (<comment> | <parameter> | <block>)* ')'  <seperator> ;
		function    : <qstring> ;
		parameter   : (<statement> | <literal>) ;
			literal  : (<number> | <qstring>) <seperator> ;
		block       : '{' <inner_block> '}' ;
		seperator   : ',' | \"\" ;
	
	qstring        : (<complexstr> | <simplestr>) <qstring>* ;
		simplestr   : /[a-zA-Z0-9_!@#$%^&\\*_+\\-\\.=\\/<>]+/ ;
		complexstr  : (/\"[^\"]*\"/ | /'[^']*'/) ;
	
	number         : (<float> | <int>) ;
		float       : /[-+]?[0-9]+\\.[0-9]+/ ;
		int         : /[-+]?[0-9]+/ ;
