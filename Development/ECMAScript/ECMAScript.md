See also [ECMAScript](../../Formats,%20encoding%20and%20protocols/ECMAScript%20-%20JavaScript/ECAMScript.md)

# Language

## Documentation

- [Understanding the ECMAScript spec, part 1 · V8](https://v8.dev/blog/understanding-ecmascript-part-1)
- [Understanding the ECMAScript spec, part 2 · V8](https://v8.dev/blog/understanding-ecmascript-part-2)

Properties notation: `Object#toString()` (for `Object.prototype.toString()`) vs static: `Object.create()`

- [JavaScript foo.prototype.bar notation · Mathias Bynens](https://mathiasbynens.be/notes/javascript-prototype-notation)
- [Exploring ES6: Upgrade to the next version of JavaScript](http://exploringjs.com/)
- http://www.codecademy.com/tracks/javascript
- [Speaking JavaScript](http://speakingjs.com/es5/index.html)
- [JS Tips – A JS tip per day!](http://www.jstips.co/)
- [Speaking JavaScript: An In-Depth Guide for Programmers](http://speakingjs.com/)
- [Exploring ES6: Upgrade to the next version of JavaScript](http://exploringjs.com/es6.html)
- [Exploring ES2016 and ES2017](http://exploringjs.com/es2016-es2017.html)
- [getify/You-Dont-Know-JS](https://github.com/getify/You-Dont-Know-JS)
- [All JavaScript Language Topics - Stack Overflow](https://stackoverflow.com/documentation/javascript/topics)
- [lydiahallie/javascript-questions: A long list of (advanced) JavaScript questions, and their explanations Updated weekly!](https://github.com/lydiahallie/javascript-questions)

Project documentation:

- [JSDoc](http://usejsdoc.org/index.html), see [Comments](#comments)
- [sphinx-js 2.0.1 : Python Package Index](https://pypi.python.org/pypi/sphinx-js/)
- [Introducing sphinx-js, a better way to document large JavaScript projects ★ Mozilla Hacks – the Web developer blog](https://hacks.mozilla.org/2017/07/introducing-sphinx-js-a-better-way-to-document-large-javascript-projects/)

## Tests

- [jsdoced.js - test your code with jsdoc](http://jsdocedjs.org/)
- [jsdoctest by yamadapc](http://www.yamadapc.com.br/jsdoctest/)

## Don't use experimental features

... only in experimentations or demos.

- [JavaScript Developers: Watch Your Language! - Web Standards - Bocoup](https://bocoup.com/weblog/javascript-developers-watch-your-language)

## Libaries

- [locutusjs/locutus: Bringing stdlibs of other programming languages to JavaScript for educational purposes](https://github.com/locutusjs/locutus) - standard libraries from php, c, python, etc. ported to JavaScript (previously called phpjs)
- [YourJS - Your Very Own JS Library](https://www.yourjs.com/)
- [dhurlburtusa/YourJS: A JS library you can use in YOUR chosen namespace.](https://github.com/dhurlburtusa/YourJS)
- [google/flatbuffers: Memory Efficient Serialization Library](https://github.com/google/flatbuffers) - serialize/deserialize data (binary) efficiently
- [epoberezkin/ajv: The fastest JSON Schema Validator. Supports draft-04/06/07](https://github.com/epoberezkin/ajv)
- [Benchmark.js](https://benchmarkjs.com/) - A benchmarking library that supports high-resolution timers & returns statistically significant results.
- [whitequark/ipaddr.js: IP address manipulation library in JavaScript](https://github.com/whitequark/ipaddr.js/)

## Formatting

- [ryanmcdermott/clean-code-javascript: Clean Code concepts adapted for JavaScript](https://github.com/ryanmcdermott/clean-code-javascript)

### Naming

Use camel casing

```js
variableName
```

Use name that mean something : content or action

Prefere `elementIndex` instead of `i`.

### Function

Don't use variable function

Use:

```js
function myfunction(){}
```

Not:

```js
var mufunction = function(){};
```

Name all function. Debug will be easer with stack traces contains those names

```js
function renameFunction(func, name){
  return Object.defineProperty(func, "name", {value: name});// https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/name
}
```

For a `function` used for an `Object` method:

```js
class MyClass {
	myMethod(){}
	myOtherMethod(){}
}
/*
MyClass.prototype = {
	myMethod: function myMethod(){}
	myOtherMethod: function myOtherMethod(){}
}
*/
```

Convert a function in strict mode to a function in sloppy (non-strict) mode (if it doesn’t have "use strict" in it):

```js
function sloppify(func) {
    return new Function('return ' + func)();
}
```

### Constant

Give uppercase name :

```js
var MY_CONST_NAME = "value";
```

Use [JSDoc comment](#comments) like:

```js
/**
 * My own constance
 * @const
 * @type {string}
 */
var MY_CONST_NAME = "value";
```

or

- https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Statements/const

### Induction variable

Use a name that describe it's usage like `childIndex` or `wheelIndex` instead of `i`, `j` or `ii`

### Semicolons

Are optional, but required in some cases

> if the next line start with a `[`, `(`, `` ` ``, `+`, `*`, `/`, `-`, `,`, `.`.

- [blog.izs.me](https://blog.izs.me/2010/12/an-open-letter-to-javascript-leaders-regarding)
- [JavaScript Semicolon Insertion](http://inimino.org/~inimino/blog/javascript_semicolons)

## Types

Use JSDoc used for type check

- `tsc --noEmit false --emitDeclarationOnly true`
- [JSDoc typings: all the benefits of TypeScript, with none of the drawbacks](https://web.archive.org/web/20210924000224/https://gils-blog.tayar.org/posts/jsdoc-typings-all-the-benefits-none-of-the-drawbacks/)

## Prototype

- [Document Object Model Prototypes, Part 1](https://msdn.microsoft.com/en-us/library/dd282900%28v=vs.85%29.aspx)

## Class

```js
class SubSub extends
	class Sub extends
		class Base {
			isBase = true
		}
	{
		isSub = true
	}
{
	isSubSub = true
}

console.log(new SubSub())// {isBase: true, isSub: true, isSubSub: true}
```

### Async instanciation

```js
class SomeClass {
	constructor() {
		if (someShortcutCondition) {
			return Promise.resolve(this);
		}

		return this.#init().then(() => this);
	}
	async #init(){
		await Promise.resolve('loading');
	}
}

await new SomeClass();
```

Use static factory method:

```js
class DataContainer {
	#data;
	static async create() {
		const data = await Promise.resolve('downloaded');
		return new this(data);
	}
	constructor(data) {
		this.#data = data;
	}
	get data() {
		return 'DATA: '+this.#data;
	}
}

const {data} = await DataContainer.create();
console.log(data);
```

> an important thing to note is that with the async constructor, you prevent exposing instances that are not completely initialized, not true with an async static helper unless you lock down the constructor so it cannot be used normally. subclassing gets weird in both

- [Techniques for instantiating classes](https://2ality.com/2019/11/creating-class-instances.html)
- [(2) Axel Rauschmayer on Twitter: "Asynchronously created instances. This is probably a better choice: class VM { static async create() { const data = await 'downloaded'; return new VM(data); } constructor(data) { this .data = data; } } VM.create().then(vm =&gt; console.log(vm .data));" / Twitter](https://twitter.com/rauschma/status/1192142696007241728?s=12)

## Modules

```js
// isDebug.js
export default new URLSearchParams(window.location.search.substring(1)).has("debug")

// config.js
const config = JSON.parse(document.querySelector("js-config").text);
export const debug = config.debug;
export const lang = config.lang;
export const region = config.region;
export const currency = config.currency;

export let counter = 0;
export function inc(){counter++}
```

- [ecmascript 6 - Javascript ES6 export const vs export let - Stack Overflow](https://stackoverflow.com/questions/32558514/javascript-es6-export-const-vs-export-let)

### Modules names

- [This or that? Component Names: index.js or Component.js | Brad Frost](http://bradfrost.com/blog/post/this-or-that-component-names-index-js-or-component-js/)

## Proxy

```js
const catcher = new Proxy(global, {
    // always pretend the property exists
    has(target, key){
        return true;
    },

    get(target, name){
        if(name in target){
            // return original value if exists
            return Reflect.get(...arguments);
        }
        // otherwise turn it into a string
        return `My name is ${String(name)}!`;
    }
});

with (catcher) {
  console.log(nobody);
  // > "My name is nobody!"
}
```

## Floating point numbers

See [IEE 754](../../Formats,%20encoding%20and%20protocols/IEEE%20754/IEE%20754.md)

Use a libs like https://github.com/dtrebbien/BigDecimal.js, https://github.com/MikeMcl/bignumber.js, https://github.com/MikeMcl/decimal.js or https://github.com/MikeMcl/big.js. See [What is the difference between big.js, bignumber.js and decimal.js?](https://github.com/MikeMcl/big.js/wiki)

```js
/**
* Corrects errors caused by floating point math.
*/
function correctFloatingPointError(number, precision = 5)
{
	//default returns (10000 * number) / 10000
	//should correct very small floating point errors
	const correction = Math.pow(10, precision);
	return Math.round(correction * number) / correction;
}

/**
* Tests if two numbers are <em>almost</em> equal.
*/
function fuzzyEquals(number1, number2, precision = 5)
{
	const difference = number1 - number2;
	const range = Math.pow(10, - precision);
	//default check:
	//0.00001 <difference> - 0.00001
	return difference < range && difference > - range;
}
```

```js
// From How to add by 0.1? https://www.reddit.com/r/learnjavascript/comments/i8v1ef/how_to_add_by_01/g1ayq8u/

// Original approach with precision problems
function addIncrements1() {
  const result = [];
  let start = 3;
  for (let i=0; i<15; i++) {
    result.push(start);
    start += 0.1;
  }
  return result;
}
console.log(addIncrements1());


// Rounding after each addition to fix the precision
function addIncrements2() {
  const result = [];
  let start = 3;
  for (let i=0; i<15; i++) {
    result.push(start);
    start += 0.1;
    start = Math.round(start * 10) / 10;
  }
  return result;
}
console.log(addIncrements2());


// Computing with integers, dividing them by 10 when necessary
function addIncrements3() {
  const result = [];
  let startTimesTen = 30;
  for (let i=0; i<15; i++) {
    result.push(startTimesTen/10);
    startTimesTen += 1;
  }
  return result;
}
console.log(addIncrements3());


// Adding 1/8 (which is base 2 and doesn’t cause precision problems)
function addIncrements4() {
  const result = [];
  let start = 3;
  for (let i=0; i<15; i++) {
    result.push(start);
    start += 0.125;
  }
  return result;
}
console.log(addIncrements4());
```

- [Number.EPSILON - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/EPSILON) - "EPSILON property represents the difference between 1 and the smallest floating point number greater than 1"
- [tc39/proposal-bigint: Arbitrary precision integer in JavaScript](https://github.com/tc39/proposal-bigint) - BigInt
- [dtrebbien/BigDecimal.js: Arbitrary-precision decimal library for JavaScript](https://github.com/dtrebbien/BigDecimal.js)
- [MikeMcl/big.js: A small, fast JavaScript library for arbitrary-precision decimal arithmetic.](https://github.com/MikeMcl/big.js)

## Array

- [Array iteration methods summarized](https://gist.github.com/ljharb/58faf1cfcb4e6808f74aae4ef7944cff)

Map to Array (note: I don't know how it's called, nor if it's ECMAScript):

```js
const map = new Map(/**/);
const result = Array.from(map.values(), ([name, value]) => name + "=" + value);

// eq. of if(cond) array.push('a')
// better than cond && arr.push('a') because `arr.push('a')` is converted to a boolean for nothing
const cond = false;
const result = [ ...(cond ? ['a'] : []), 'b'];
// ['b']

var chars = [..."test"];

// range
[...new Array(4).keys()]// [0, 1, 2, 3]
```

- [Defining Basic JavaScript Terms: map, filter, and reduce - Jim Nielsen’s Blog](https://web.archive.org/web/20210907154620/https://blog.jim-nielsen.com/2021/defining-basic-javascript-terms/) - "Understanding why APIs are named the way they are in a language is another plane of understanding code. It enhances your understanding in a way that experiential knowledge alone cannot."

### Spread operator

Convert Arguments to Array:

```js
let argsArray = [...arguments];
```

See also [Destructuring](#destructuring)

- [JavaScript & The spread operator – Hacker Noon](https://hackernoon.com/javascript-the-spread-operator-a867a71668ca)
- [spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)

### Array holes

- [ECMAScript 6: holes in Arrays](http://www.2ality.com/2015/09/holes-arrays-es6.html)

	Array.apply(null, {length: 2});//create a filled array [undefined, undefined]

	const numHarrys = 7;
	const harrys = [...numHarrys].map(() => new Object());// create instance object for each vs use same reference for `new Array(numHarrys).fill({})`

- [Annotated ES5](https://es5.github.io/#x15.3.4.3)
- [An adventure in sparse arrays](https://remysharp.com/2018/06/26/an-adventure-in-sparse-arrays)
- [Creating and filling Arrays of arbitrary lengths in JavaScript](http://2ality.com/2018/12/creating-arrays.html)

### Array fill

	Array.from({length: 3})// => [undefined, undefined, undefined]
	Array.from({length: 3}, (value, index, array) => 2 + index * 2)// => [2, 4, 6]

See [Array holes](#array-holes)

- [18. New Array features](http://exploringjs.com/es6/ch_arrays.html#sec_creating-filled-arrays)
- [Generate ranges in javascript](https://gist.github.com/xgrommx/a25ffa3a7753e01ee679)
- [Array.from() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
- [Creating and filling Arrays of arbitrary lengths in JavaScript](http://2ality.com/2018/12/creating-arrays.html)

## Constructor

```js
// Class & function but not generator nor arrow function
const isConstructorFunction = (value) => Boolean(value && value.prototype && value.prototype.constructor);

/*
// true
function(){}
class A {}
Array
Function
new Function

// false
undefined
null
1
new Number(1)
Array.prototype
Function.prototype
() => {}
{method() {}}.method
function*(){}
*/
```

```js
new function(){return ["test"]} // > Array [ "test" ]
```

- [How to check if a Javascript function is a constructor - Stack Overflow](https://stackoverflow.com/questions/40922531/how-to-check-if-a-javascript-function-is-a-constructor)

## Lookup table

```js
const table = new Map([
    ["key1", "value1"],
    ["key2", "value2"],
])
```

```js
// ES6
const table = Object.create(null, {
    key1: "value1",
    key2: "value2",
});
```

```js
// ES5
const table = {
    __proto__: null,// avoids the pitfall of inheriting properties such as 'toString'
    key1: "value1",
    key2: "value2",
};
```

- [Axel Rauschmayer on Twitter: "Lookup tables: If I create one via an object literal (and not via `new Map()`), I use the following pattern. const obj = { __proto__: null, key1: 'value1', // etc. }; That avoids the pitfall of inheriting properties such as 'toString': https://t.co/Q4siSPAmNt" / Twitter](https://twitter.com/rauschma/status/1154052569259376640?s=12)

## String

> slice vs splice
> shift vs unshift
> substr vs substring
>
> Always slice (never substr or substring)
> shift = how bash accesses args (left to right)

Split long string ([Long literal strings - String - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String#long_literal_strings))

```js
// With string concatenation
const str1 = "a"
	+ "b";
// With line continuation
const str2 = "a\
b";
```

See [quotes](#quotes)

- [Text Escaping and Unescaping in JavaScript](http://0xcc.net/jsescape/)
- [Chapter 24. Unicode and JavaScript](http://speakingjs.com/es5/ch24.html)
- [Hackvertor](https://hackvertor.co.uk/public), [Hackvertor](http://www.businessinfo.co.uk/labs/hackvertor/hackvertor.php) - see "Charsets" > *
- [JavaScript has a Unicode problem · Mathias Bynens](https://mathiasbynens.be/notes/javascript-unicode)
- [JavaScript’s internal character encoding: UCS-2 or UTF-16? · Mathias Bynens](https://mathiasbynens.be/notes/javascript-encoding)
- UTF-8 encoder/decoder https://github.com/mathiasbynens/utf8.js
- A collection of Regenerate sets for Unicode various properties https://github.com/mathiasbynens/regenerate-unicode-properties
- [Escape Codec Library module conformed to Closure Library](https://github.com/Kuniwak/Escape-Codec-Library-for-Closure) allow escape and unescape EUC-JP, JIS7, JIS8, Shift-JIS, Unicode, UTF16LE, UTF7, UTF8
- generating the shortest possible valid ASCII-only output https://github.com/mathiasbynens/jsesc
- implementation of character encoding
	- https://github.com/mathiasbynens/x-mac-cyrillic
	- https://github.com/mathiasbynens/windows-874
	- https://github.com/mathiasbynens/windows-1258
	- https://github.com/mathiasbynens/windows-1257
	- https://github.com/mathiasbynens/windows-1256
	- https://github.com/mathiasbynens/windows-1255
	- https://github.com/mathiasbynens/windows-1254
	- https://github.com/mathiasbynens/windows-1253
	- https://github.com/mathiasbynens/windows-1252
	- https://github.com/mathiasbynens/windows-1251
	- https://github.com/mathiasbynens/windows-1250
	- https://github.com/mathiasbynens/macintosh
	- https://github.com/mathiasbynens/koi8-u
	- https://github.com/mathiasbynens/koi8-r
	- https://github.com/mathiasbynens/iso-8859-8
	- https://github.com/mathiasbynens/iso-8859-8-i
	- https://github.com/mathiasbynens/iso-8859-7
	- https://github.com/mathiasbynens/iso-8859-6
	- https://github.com/mathiasbynens/iso-8859-5
	- https://github.com/mathiasbynens/iso-8859-4
	- https://github.com/mathiasbynens/iso-8859-3
	- https://github.com/mathiasbynens/iso-8859-2
	- https://github.com/mathiasbynens/iso-8859-16
	- https://github.com/mathiasbynens/iso-8859-15
	- https://github.com/mathiasbynens/iso-8859-13
	- https://github.com/mathiasbynens/iso-8859-14
	- https://github.com/mathiasbynens/iso-8859-10
	- https://github.com/mathiasbynens/ibm866
- Unicode data generator https://github.com/mathiasbynens/node-unicode-data and
	- https://github.com/mathiasbynens/unicode-1.1.5
	- https://github.com/mathiasbynens/unicode-2.0.14
	- https://github.com/mathiasbynens/unicode-2.1.2
	- https://github.com/mathiasbynens/unicode-2.1.5
	- https://github.com/mathiasbynens/unicode-2.1.8
	- https://github.com/mathiasbynens/unicode-2.1.9
	- https://github.com/mathiasbynens/unicode-3.0.0
	- https://github.com/mathiasbynens/unicode-3.0.1
	- https://github.com/mathiasbynens/unicode-3.1.0
	- https://github.com/mathiasbynens/unicode-3.2.0
	- https://github.com/mathiasbynens/unicode-4.0.0
	- https://github.com/mathiasbynens/unicode-4.0.1
	- https://github.com/mathiasbynens/unicode-4.1.0
	- https://github.com/mathiasbynens/unicode-5.0.0
	- https://github.com/mathiasbynens/unicode-5.1.0
	- https://github.com/mathiasbynens/unicode-5.2.0
	- https://github.com/mathiasbynens/unicode-6.0.0
	- https://github.com/mathiasbynens/unicode-6.1.0
	- https://github.com/mathiasbynens/unicode-6.2.0
	- https://github.com/mathiasbynens/unicode-6.3.0
	- https://github.com/mathiasbynens/unicode-7.0.0
	- https://github.com/mathiasbynens/unicode-8.0.0
	- https://github.com/mathiasbynens/unicode-9.0.0
	- https://github.com/mathiasbynens/unicode-loose-match
	- https://github.com/mathiasbynens/unicode-property-value-aliases
	- https://github.com/mathiasbynens/unicode-property-aliases
	- https://github.com/mathiasbynens/unicode-canonical-property-names
	- https://github.com/mathiasbynens/unicode-match-property
	- https://github.com/mathiasbynens/unicode-match-property-value
- Punycode converter https://github.com/bestiejs/punycode.js
- code points that Verisign allows by default in IDN https://github.com/mathiasbynens/idn-allowed-code-points-regex and https://github.com/mathiasbynens/idn-allowed-code-points
- Emoji data extracted https://github.com/mathiasbynens/unicode-tr51
- base64 encoder/decoder https://github.com/mathiasbynens/base64
- Remove Unicode variation selectors https://github.com/mathiasbynens/strip-variation-selectors and combining marks https://github.com/mathiasbynens/strip-combining-marks
- Unicode-aware string reverser  https://github.com/mathiasbynens/esrever
- Python scripts that generate JavaScript-compatible Unicode data https://github.com/mathiasbynens/unicode-data
- A letter case swapper with full Unicode support https://github.com/mathiasbynens/swapcase
- Normalization (composition) `String.prototype.normalize()` or https://github.com/walling/unorm
	- [Unicode equivalence — Wikipedia](https://en.wikipedia.org/wiki/Unicode_equivalence#Normalization)

```js
//Simple way to read and write UTF-8/UTF-16 string from/to UintArray
function uintToString(bytes) {
	return decodeURIComponent(escape(String.fromCharCode.apply(null, bytes)));
}
function stringToUTF8array(string) {
	let binaryString = unescape(encodeURIComponent(s)),
	let bytes = new Uint8Array(binaryString.length);
	for (let i = 0; i < bytes.length; i++){
		bytes[i] = binaryString.charCodeAt(i);
	}
	return bytes;
}
```

```js
// Should store length in bytes (not length in chars)
var utf8 = [];
var i = 0;

while (i < s.length) {
	var codePoint;

	// Decode UTF-16
	var a = s.charCodeAt(i++);
	if (a < 0xD800 || a >= 0xDC00) {
		codePoint = a;
	} else {
		var b = s.charCodeAt(i++);
		codePoint = (a << 10) + b + (0x10000 - (0xD800 << 10) - 0xDC00);
	}

	// Encode UTF-8
	if (codePoint < 0x80) {
		utf8.push(codePoint);
	} else {
		if (codePoint < 0x800) {
			utf8.push(((codePoint >> 6) & 0x1F) | 0xC0);
		} else {
			if (codePoint < 0x10000) {
				utf8.push(((codePoint >> 12) & 0x0F) | 0xE0);
			} else {
				utf8.push(
					((codePoint >> 18) & 0x07) | 0xF0,
					((codePoint >> 12) & 0x3F) | 0x80);
			}
			utf8.push(((codePoint >> 6) & 0x3F) | 0x80);
		}
		utf8.push((codePoint & 0x3F) | 0x80);
	}
}
```

```js
// From https://github.com/google/flatbuffers/blob/master/js/flatbuffers.js
var offset = 0;
var bytes = new DataView(...);
var length = bytes.readInt32(offset);
var result = "";
var i = 0;

while (i < length) {
	var codePoint;

	// Decode UTF-8
	var a = bytes.readUint8(offset + i++);
	if (a < 0xC0) {
		codePoint = a;
	} else {
		var b = bytes.readUint8(offset + i++);
		if (a < 0xE0) {
			codePoint =
				((a & 0x1F) << 6) |
				(b & 0x3F);
		} else {
			var c = bytes.readUint8(offset + i++);
			if (a < 0xF0) {
				codePoint =
					((a & 0x0F) << 12) |
					((b & 0x3F) << 6) |
					(c & 0x3F);
			} else {
				var d = bytes.readUint8(offset + i++);
				codePoint =
					((a & 0x07) << 18) |
					((b & 0x3F) << 12) |
					((c & 0x3F) << 6) |
					(d & 0x3F);
			}
		}

		// Encode UTF-16
		if (codePoint < 0x10000) {
			result += String.fromCharCode(codePoint);
		} else {
			codePoint -= 0x10000;
			result += String.fromCharCode(
				(codePoint >> 10) + 0xD800,
				(codePoint & ((1 << 10) - 1)) + 0xDC00);
		}
	}
}
```

```js
String.prototype.encodeURIComponent = function() {
	var result = [];
	var len = this.length;
	for (var i = 0; i < len; i++) {
		result.push(this.charAt(i).toUTF8());
	}
	return result.join("");
};
String.prototype.toUTF8 = function() {
	var code = this.charCodeAt(0);
	if (code <= 16) {
		return "%0" + code.toString(16);
	}
	var iByte = 0;
	var i = 0;
	var result = "";
	while (code > 0x7f) {
		iByte = code % 0x40;
		code = (code - iByte) / 0x40;
		result = "%" + (iByte | 0x80).toString(16).toUpperCase() + Result;
		i++;
	}
	prefix = [0x0, 0xc0, 0xe0, 0xf0, 0xf8, 0xfc];
	if (i > prefix.length) {
		i = 5;
	}
	result = "%" + (code | prefix[i]).toString(16).toUpperCase() + Result;
	return result;
};
String.prototype.encodeURI = function() {
	var result = [];
	var len = this.length;
	for (var i = 0; i < len; i++) {
		var code = this.charCodeAt(i);
		if (code < 255) {
			//if (code == 61 || code == 38) {
			result.push(this.charAt(i));
		} else {
			result.push(this.charAt(i).toUTF8());
		}
	}
	return result.join("");
};
var st = "http://220.133.52.91/????a=10&b=lamb-mei";
console.log(st.encodeURI());
console.log(st.encodeURIComponent());
```

Count number of chars (especially emojis):

```js
// From http://blog.jonnew.com/posts/poo-dot-length-equals-two
function fancyCount2(str){
  const joiner = "\u{200D}";
  const split = str.split(joiner);
  let count = 0;

  for(const s of split){
    //removing the variation selectors
    const num = Array.from(s.split(/[\ufe00-\ufe0f]/).join("")).length;
    count += num;
  }

  //assuming the joiners are used appropriately
  return count / split.length;
}
```

### Template literal

```js
const tmpl = addrs => `
	<table>
	${addrs.map(addr => `
		<tr><td>${addr.first}</td></tr>
		<tr><td>${addr.last}</td></tr>
	`).join('')}
	</table>
`;

const data = [
	{ first: '<Jane>', last: 'Bond' },
	{ first: 'Lars', last: '<Croft>' },
];

console.log(tmpl(data));
// Output:
// <table>
//
// 	<tr><td><Jane></td></tr>
// 	<tr><td>Bond</td></tr>
//
// 	<tr><td>Lars</td></tr>
// 	<tr><td><Croft></td></tr>
//
// </table>
```

### String is an array-like of chars

```js
Array.prototype.join.call("abc", "-")// "a-b-c"
Array.prototype.filter.call("abc", char => char != "b")// ["a", "c"]
Array.prototype.reduce.call("abc", (result, char) => result + char.charCodeAt(0), 0)// 294
Array.from("abc")// ["a", "b", "c"]
```

- [javascript - What does Array.prototype.join.call do in the background for a string? - Stack Overflow](https://stackoverflow.com/questions/33981796/what-does-array-prototype-join-call-do-in-the-background-for-a-string/33981853#33981853)

## Destructuring

```js
// Swap values
[a, b] = [b, a];
```

```js
let a = 1;
({a} = {a: 2});// a === 2
```

```js
const a = {
	b: 1
}

const {
	b,
	c = 2
} = a;

// c == 2
```

```js
// Get both a and a.b
const {a, a: {b}} = {a: {b: "hi"}};
// const {a, a: a1} = {a: "hi"};
```

```js
// Dynamically get / remove a key from an object
const key = 'name';
const { [key]: keyValue, ...rest } = obj;
```

```js
let {options: {value1, value2}} = param;// same as let value1 = param.options.value1, value2 = param.options.value2;
```

```js
let [x=5] = [b]; // x=5 if b=undefined (but not if b=null)
```

```js
function f(...[a, b, c]) {
	return a + b + c;
}
/*
f(1)          // NaN (b and c are undefined)
f(1, 2, 3)    // 6
f(1, 2, 3, 4) // 6 (the fourth parameter is not destructured)
*/
```

```js
function f([a, b, c]){
	return a + b + c;
}
/*
f([1, 2, 3])// 6
*/
```

```js
const obj = {
	...condition && { prop: value },
};

const arr = [
	...condition && ["a"] || [],// need a default value or it will throw a type error: boolean false is not iterable
];
```

```js
const x = {a: 1, b: 2};
const y = {};
for ([k, y[k]] of Object.entries(x));
y // {a: 1, b: 2}
/*
// Equivalent to:
for (let entry of Object.entries()) {
  k = entry[0];
  y[k] = entry[1];
}
*/
```

- [10. Destructuring](http://exploringjs.com/es6/ch_destructuring.html)
- [Destructuring assignment - JavaScript | MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Swapping_variables) - use destructuring to swap variables
- [Rest parameters - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters#Destructuring_rest_parameters)
- [The shortest way to conditional insert properties into an object literal - DEV Community 👩‍💻👨‍💻](https://dev.to/jfet97/the-shortest-way-to-conditional-insert-properties-into-an-object-literal-4ag7)

## Default parameters

```js
function({a = "foo", b = "bar"} = {}){
	console.log(a, b);
}
```

## Default value

If `expr` is falsy

	const x = expr || "default";

If `expr` is undefined:

	const x = x === undefined ? "default" : expr;
	const [x = "default"] = [expr];

## Object literal declaration

	let key3name = "key3";
	let ref = {key4: "Four"}
	let obj = {
		key1: "One",
		key2: "Two",
		[key3name]: "Three"
		property([parameters]) {},
		get property() {},
		set property(value) {},
		* generator() {},
		...ref
	};

- [Object initializer - JavaScript | MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Object_initializer)

## Function

Aka arrow function, method

Ordinary functions would be called methods and arrow functions would be called functions.

Or "dispatched method call" for `obj.foo()` and "direct method call" for `func.call(obj)`

- [12. Callable entities in ECMAScript 6](http://exploringjs.com/es6/ch_callables.html#sec_dispatched-direct-method-calls)

### Execution Context

- [JavaScript Visualizer](https://javascriptvisualizer.com/)

### Arrow function

Return without return keyword, use the [comma operator](#comma-operator)

	(param1) => (doSomething(), param1)

Equivalent to

	(param1) => {
		doSomething();
		return param1;
	}

Return an object

	(param) => ({attr1: "value1", attr1: "value2"})

### Function name

```js
// Fix Function#name on browsers that do not support it (IE):
if (!(function f() {}).name) {
	Object.defineProperty(Function.prototype, 'name', {
		get: function() {
			var name = (this.toString().match(/^function\s*([^\s(]+)/) || [])[1];
			// For better performance only parse once, and then cache the
			// result through a new accessor for repeated access.
			Object.defineProperty(this, 'name', { value: name });
			return name;
		}
	});
}
```

- [javascript - function.name not supported in IE. - Stack Overflow](https://stackoverflow.com/questions/6903762/function-name-not-supported-in-ie)

## Ternary

	var result = value > 10 ? getA() || getB()

	// If getA() return a "falsy" value, getB() will be the result
	var result = value > 10 && getA() || getB()

## Performance and optimization

See [Performance and optimization](Development#performance-and-optimization)

- [JS MythBusters, A JavaScript optimization handbook from a high level point of view.](https://mythbusters.js.org/)
- [Writing Fast, Memory-Efficient JavaScript – Smashing Magazine](https://www.smashingmagazine.com/2012/11/writing-fast-memory-efficient-javascript/)
- [Find common memory issues | Web Tools - Google Developers](https://developers.google.com/web/tools/chrome-devtools/profile/memory-problems/memory-diagnosis)
- [Memory Management - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management)
- [Optimization](Development#optimization)
- [Premature Optimization](http://wiki.c2.com/?PrematureOptimization)
- [.map() vs .forEach() vs for()](https://ryanpcmcquen.org/javascript/2015/10/25/map-vs-foreach-vs-for.html)
- [Optimizing dynamic JavaScript with inline caches · sq/JSIL Wiki](https://github.com/sq/JSIL/wiki/Optimizing-dynamic-JavaScript-with-inline-caches)
- reduce garbage collection time by using object pools
- in an async loop (like setTimeout or requestAnimationFrame) use `date.setTime(Date.now())` instead of recreate a `new Date()` object each iteration. [new Date() vs. setTime(Date.now()) · jsPerf](https://jsperf.com/new-date-vs-settime)
- [thejameskyle/js-memory-heap-profiling](https://github.com/thejameskyle/js-memory-heap-profiling) - Approximate memory usage (in bytes) of various types of objects
- [Adventures in Microbenchmarking - tomdale.net](https://tomdale.net/2017/07/adventures-in-microbenchmarking/) - store large data in a string instead of pure JS, then `JSON.parse()` when needed. See also [Mathias Bynens on Twitter: "That benchmark is testing caching, not JSON.parse vs. object literal. To test, create a JS file containing a large object literal, and a file containing the equivalent JSON.parse("..."). No loops or other boilerplate. Then run in d8 or with RCS https://t.co/ysinxs1fHv… https://t.co/ia8tBIOaEF"](https://twitter.com/mathias/status/1143818364059619329)

`if(obj !== undefined && obj !== null){return obj.x}` (explicit) vs `if(obj){return obj.x}` (implicit). The second is less performant (the first one is ~15% faster). See [Michael Haeuslmann on Twitter: "Not only is declarative code more readable, it also produces beautiful byte code and is therefore faster. Thanks @bmeurer @munichnug https://t.co/Iae0s3e40W"](https://twitter.com/michaelhaeu/status/845003383153025024) and [TurboFan: A new code generation architecture for V8 - Google Slides](https://docs.google.com/presentation/d/1_eLlVzcj94_G4r9j9d_Lj5HRKFnq6jgpuPJtnmIBs88/edit#slide=id.g2134da681e_0_596)
`let len = (obj !== undefined) ? obj.length : 0` vs `let len = obj && obj.length` convert length as boolean, then later check if it's a number. [More specific if conditions lead to ~10% faster render. by asolove · Pull Request #610 · developit/preact](https://github.com/developit/preact/pull/610#issuecomment-289981990)
`void 0` vs `undefined`. In Safari (JSC), the first one is cont, and the second one is global variable. See [olexandr on Twitter: "@kuvos @michaelhaeu @bmeurer @munichnug In JSC (Safari) it is better to use 'void 0'. undefined is global variable, but 'void 0' is const https://t.co/N4C5QQTYaQ"](https://twitter.com/alSkachkov/status/845331457761579009)
Use lot of WeakMap can be an issue: [Evan Wallace on Twitter: "@MarijnJH This was in 2019. Figma has a sandbox for plugins. We needed to associate metadata about Figma’s objects with handles inside the sandbox. Long story short there were a LOT of handles, and GC was pretty bad. Might be fine for your use case. Just avoid really big WeakMaps." / Twitter](https://twitter.com/evanwallace/status/1328459072794808320)

### Micro-optimization can be useless

Reverse loops, bitwise shift boolean, etc. put complexity to your code for a too much little gain (if they will in all browsers) and can be counterproductive

Result have often a tiny impact over millions iteration. Can only count in ultra intensive environnement like core or 3D engine or data (audio, video) processing. If so **add comments** to explain the choice.

Performances tests results can change over engines and versions.

- [Unsigned right shift bitwise operator versus OR logical operator](http://andrew.hedges.name/experiments/shifty/)
- [Speed test: === vs in vs hasOwnProperty](http://andrew.hedges.name/experiments/in/)
- Like [use `"` over `'`](https://stackoverflow.com/questions/242813/when-to-use-double-or-single-quotes-in-javascript/814376#814376) only because it's faster
- See "Understand before acting" in [How the Grinch stole array.length access](http://mrale.ph/blog/2014/12/24/array-length-caching.html)
- See "Recommendations" in [Performance optimizations and for loops](http://www.2ality.com/2013/07/for-loop-performance.html)
- (14/09/2016: unwrap function are double-parsed by Chakra and V8, but not by SpiderMonkey nor Nitro) [Avoid lazy parsing by adding parens around factory by bmaurer · Pull Request #774 · rollup/rollup](https://github.com/rollup/rollup/pull/774#issuecomment-231474820)
- [Genius or stupid? | CommitStrip](https://www.commitstrip.com/en/2016/01/26/genius-or-stupid/)
- `stringChunks.push("some string chunk")` vs `string += "some string chunk"` (the latest is now optimized, the former need to create an array in memory)
- A lib to rewrite JS to "optimize" syntax. Really? https://github.com/nolanlawson/optimize-js https://github.com/mishoo/UglifyJS2/issues/886
- `Map` vs plain object to store string keys values [dictionary - Map vs Object in JavaScript - Stack Overflow](https://stackoverflow.com/questions/18541940/map-vs-object-in-javascript/37994079#37994079)
- [Optimization killers](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)
- Absolute value (signed interger only), `y = Math.abs(x);`: `y = x < 0 ? -x : x`
- `y = Math.floor(x)`: `var x2 = x | 0; y = (x < 0 && x != x2) ? x2 - 1 : x2;` (`x | 0` for to 32bit signed integer)
- `y = Math.round(x)`: `y = x < 0 ? x + .5 == (x | 0) ? x : x - .5 : x + .5`
- `y = Math.ceil(x)`: `var x2 = x | 0; y = (x >= 0 && x != x2) ? x2 + 1 : x2;`
- `for(let i = 0, length = array.length; i < length; i++){}` cached in loop [\[JavaScript\] Shoud I have to cache my array’s length? – EternalCoding](https://www.eternalcoding.com/?p=33), [How the Grinch stole array.length access](http://mrale.ph/blog/2014/12/24/array-length-caching.html)

- [V8 JavaScript Engine: Retiring Octane](https://v8project.blogspot.fr/2017/04/retiring-octane.html)
- [Optimization killers · petkaantonov/bluebird Wiki](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)
- [Let’s get those Javascript Arrays to work fast | gamealchemist](https://gamealchemist.wordpress.com/2013/05/01/lets-get-those-javascript-arrays-to-work-fast/)
- [Announcing key advances to JavaScript performance in Windows 10 Technical Preview – IEBlog](https://blogs.msdn.microsoft.com/ie/2014/10/09/announcing-key-advances-to-javascript-performance-in-windows-10-technical-preview/)

See also [Bitwise operations](#bitwise-operations)

### Long Switch

Long switchs are used by state machine like parsers / tokenizers, wrapped in a loop. **But it's not adviced to use it for parsing,** use [recursive descent parser](https://en.wikipedia.org/wiki/Recursive_descent_parser) instead (see "C implementation").

Some JS/ECMAScript Engines are not optimised for extrem long switch. Use if-else instead.

```js
// A more complete HTML tokenizer: https://chromium.googlesource.com/chromium/src.git/+/master/ios/third_party/blink/src/html_tokenizer.mm
// See also https://www.w3.org/TR/html5/syntax.html#tokenization
const DATA = "Data";
const TAG_OPEN = "TagOpen";
const END_TAG_OPEN = "EndTagOpen";
const TAG_NAME = "TagName";

const isASCII = char => {let code = char.charCodeAt(0); return code >= 65/*A*/ && code <= 90/*Z*/ || code >= 97/*a*/ && code <= 122/*z*/}

let char;
let position = 0;
let stream = "<tag>link</tag>";
let state = DATA;
// Consume loop
consumeStream: while (true)
{
	char = stream.charAt(position);
	switch (state)
	{
		case DATA:
			if(char == "<"){
				state = TAG_OPEN;
			}else if(char == ""){
				console.log("token: end");
				console.log("end of stream")
				break consumeStream;
			} else {
				console.log(`token: append char "${char}" to data`);
			}
			break;
		case TAG_OPEN:
			if (char == "/"){
				state = END_TAG_OPEN;
			} else if(isASCII(char)){
				console.log(`token: start tag token with char "${char}"`)
				state = TAG_NAME;
			} else {
				console.log("token: end");
				console.log(char ? `invalid char "${char}" in tag name` : "end of stream");
				break consumeStream;
			}
			break;
		case END_TAG_OPEN:
			if (isASCII(char)){
				console.log(`token: start end tag token with char "${char}"`);
				state = TAG_NAME;
			} else {
				console.log("token: end");
				console.log(char ? `invalid char "${char}" in tag name` : "end of stream");
				break consumeStream;
			}
			break;
		case TAG_NAME:
			if (char == ">"){
				console.log("token: end");
				console.log("token: start data token");
				state = DATA;
			} else if (isASCII(char)){
				console.log(`token: append char "${char}" to tag name`);
				state = TAG_NAME;
			} else {
				console.log("token end");
				console.log(char ? `invalid char "${char}" in tag name` : "end of stream");
				break consumeStream;
			}
			break;

	}
	position++;
}
````

```js
// Pseudo code
while (true)
{
	nextToken = readToken()

	switch (true)
	{
		case currentToken is A && nextToken is B:
			currentToken = nextToken;
			continue;
		case currentToken is A && nextToken is C || currentToken is A && nextToken is D:
			currentToken = nextToken;
			continue;
		case currentToken is A && nextToken is E:
			currentToken = nextToken;
			continue;
		case currentToken is B && nextToken is C:
			...
			continue;
	}
	return;
}
```

- [Should I use big switch statements in JavaScript without performance problems? - Stack Overflow](https://stackoverflow.com/questions/18830626/should-i-use-big-switch-statements-in-javascript-without-performance-problems#comment27798374_18830724)

See [language parsing (see `goto`s)](Language parsing)

### Lookup table

To speed up results of often call function like `Math.sqrt`, pre-compute all values (with precision error):

```js
const lut = new LUT(2, 100, Math.sqrt);
lut.val(25);//

/**
*   A generic lookup table useful for caching the results of a function
*   @author Jackson Dunstan
*/
class LUT
{
	/** Table of function values*/
	//var table;

	/** 10^decimals of precision*/
	//var pow;

	/**
	*   Make the look up table
	*   @param max Maximum value to cache
	*   @param numDigits Number of digits places of precision
	*   @param func Function to call to generate stored values.
	*               Must be valid on [0,max).
	*   @throws Error If func is null or invalid on [0,max)
	*/
	constructor(numDigits, max, func)
	{
		const pow = this.pow = Math.pow(10, numDigits);
		const round = 1 / pow;
		const len = 1 + max * pow;
		const table = this.table = new Array(len);

		let val = 0;
		for (let i = 0; i < len; i++)
		{
			table[i] = func(val);
			val += round;
		}
	}

	/**
	*   Look up the value of the given input
	*   @param val Input value to look up the value of
	*   @return The value of the given input
	*/
	val(val)
	{
		return this.table[Math.floor(val * this.pow)];
	}
}
```

### Binary flags

aka bit fields

Save memory (instead of use 8 bytes in memory for each boolean)

Binary flags:

```js
const FLAG_1 = 1;
const FLAG_2 = 1 << 1;
const FLAG_3 = 1 << 2;
const FLAG_4 = 1 << 3;

//Set differents flags
let flags = FLAG_1 | FLAG_2;

//Add flag 3
flags |= FLAG_3;

//Remove flag 4
flags &= ~FLAG_4;

//Get flag
let hasFlag2 = (flags & FLAG_2) !== 0;
```

Where flag are unsigned integer with value power of 2: (0, 0x0), (1, 0x1), (2, 0x2, `1 << 1`), (4, 0x4, `1 << 2`), …

See [Bitwise operations](#bitwise-operations)

### Remove an item in an unsorted array

Instead (it's slow):

```js
array.splice(index, 1);
```

Replace the current element with the last array item and pop:

```js
array[index] = array[array.length - 1];// replace with the last item
array.pop();
```

## Bitwise operations

Aka bit twiddling

**See [Micro optimization are useless](#micro-optimization-are-useless) before**

is not exactly the same because bitwise will **clamp Number to 32bits integers**.

`~~0.5 == Math.round(0.5)`, `~2 == -(2+1)// == -3`

- [javascript - What does a tilde do when it precedes an expression? - Stack Overflow](https://stackoverflow.com/questions/12299665/what-does-a-tilde-do-when-it-precedes-an-expression)
- [Bitwise operators - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators)
- [Bit Twiddling Hacks](https://graphics.stanford.edu/~seander/bithacks.html) - collection of bit twiddling examples

```js
// Rotates x left n bits
function rol ( x, n ) {
	return ( x << n ) | ( x >>> ( 32 - n ) );
}

// Rotates x right n bits
function ror ( x, n ) {
	var nn = 32 - n;
	return ( x << nn ) | ( x >>> ( 32 - nn ) );
}

// Increment / decrement
// if i is 32bits interger:
i = -~i;//equal to i++
i = ~-i;//i--

// Multiplication (power of 2 only)
y = x << 1;//equals (~300% faster) to: y = x * 2;
y = x << 6;//y = x * 64

// Division (power of 2 only)
y = x >> 1;//equals (~350% faster) to: y = x / 2;
y = x >> 6;//y = x / 64

// Number to integer conversion
y = x >> 0;//equals to: y = int(x); or y = Math.floor(x);

// Swap integers without a temporary variable using XOR (integer only):
x ^= y;
y ^= x;
x ^= y;
/*
same as:
[x, y] = [y, x];
or:
const z = x;
x = y;
y = z;
*/

// Sign flipping using NOT or XOR (power of 2 only)
x = ~x + 1;//or
x = (x ^ -1) + 1;//equals to x = -x;

// Modulo operation using AND (power of 2 only)
z = x & (y - 1);//equals to z = x % y;

// Check if an integer is even/uneven using AND
(x & (y - 1)) == 0;//equals to: (x % y) == 0

// Absolute value (signed interger only)
y = (x ^ (x >> 31)) - (x >> 31);//equals to Math.abs()

// Sign comparaison (signed integers only)
z = x ^ y > 0;//equals (~35% faster) to: z = x * y > 0;

// Determining if an integer is a power of 2 (where `x` is integer tested and y is "if is power of 2")
y = !(x & (x - 1)) && x;

// indexOf
// Note: try to not use that way
var myWord = "mychar";
if(~myWord.indexOf("d"))// equals to myWord.contains("d")
	console.log("found")
else
	console.log("not found")

// Extract ammount of bits in unsigned integer:
y = (x >>> offset) & (0xffffffff >>> 32 - numBits);
y = (x >>> offset) & (Math.pow(2, numBits) - 1);
// Where `x` is an unsigned interger and `numBits` is value of bits need to extract.
```

- BitCalc Whiteboard for explaining bit-twiddling algorithms: [x&-x](https://alf.nu/s/bitcalc.html?t1=x+%3D+0x12340&t2=~x&t3=~x+%2B+1&t4=-x&t5=x&t6=x+%26+-x&t7=&t8=&t9=&t10=) and [snoob](https://alf.nu/s/bitcalc.html?t1=x+%3D+0x012300f0&t2=smallest+%3D+x+%26+-x&t3=ripple+%3D+x+%2B+smallest&t4=ones+%3D+x+%5E+ripple&t5=ones+%3D+%28ones+%3E%3E+2%29+%2F+smallest&t6=ripple+%7C+ones&t7=&t8=&t9=&t10=)

## Promises

Use async/await with destructuring

Note: until the first `await` is met, the begining of an async function body is sync. [javascript - Does async make everything inside it asynchronous? - Stack Overflow](https://stackoverflow.com/questions/51201786/does-async-make-everything-inside-it-asynchronous/51201849#51201849)

```js
const [user, image] = await Promise.all([fetch("/user"), fetch("/image.jpg")]);
```

```js
async function isPromiseResolved(promise){
	const ref = Symbol();
	return (await Promise.race([promise, ref])) !== ref;
}
// See also https://github.com/MattiasBuelens/remote-web-streams/blob/afe2a98832272d592e454a9d4640c47912f939cd/test/promise-utils.ts#L1
```

```js
/**
 * Set timeout for promise
 * @example promiseTimeout(100, fetch("https://example.com"))
 * @see https://italonascimento.github.io/applying-a-timeout-to-your-promises/#comment-3401043682
 * @see https://stackoverflow.com/questions/46946380/fetch-api-request-timeout/46946573#46946573
 */
function promiseTimeout(ms, promise) {
  let id;
  const timeout = new Promise((resolve, reject) => {
    id = setTimeout(() => {
      reject(`Timed out in ${ms}ms.`)
    }, ms)
  })

  return Promise.race([
    promise,
    timeout
  ]).then(result => {
    clearTimeout(id)
    return result
  })
}
```

- [Writing Promise-Using Specifications](https://www.w3.org/2001/tag/doc/promises-guide/#rejections-should-be-exceptional) - "Rejections must be used for exceptional situations"
- [Betamark - Mistakes we make using JavaScript Promises](https://www.betamark.com/blog/mistakes-using-javascript-promises/)
- [Beware of Async/Await | Brandon's Website](https://www.brandonsmith.ninja/blog/async-await#easy-mistakes)
- [Understanding JQuery.Deferred and Promise](http://joseoncode.com/2011/09/26/a-walkthrough-jquery-deferred-and-promise/)
- [javascript - Promise - is it possible to force cancel a promise - Stack Overflow](https://stackoverflow.com/questions/30233302/promise-is-it-possible-to-force-cancel-a-promise)

### How promise should be handled

**Note: Promise-returning functions should never synchronously throw errors**

```js
function asyncFunc() {
	return Promise.resolve()
	.then(() => {
		doSomethingSync();// called after the end of JS stack of current JS loop
		return doSomethingAsync();
	})
	.then(result => {
		//···
	});
}
```

```js
async function asyncFunc() {
	doSomethingSync();// call immediately
	await doSomethingAsync();
	//···
}
```

Handle promises rejection in HTML document:

```js
window.addEventListener("unhandledrejection", event => {
	// Prevent error output on the console:
	event.preventDefault();
	console.log("Promise unhandled rejection. Reason: " + event.reason);
});
```

`rejectionhandled` can also be used to handle unhandled rejection later handled (asynchrounous `promise.catch(reason => {});`)

Handle promises rejection in node v6.6.0+:

```js
process.on("unhandledRejection", error => console.log('Rejection', error));
```

- [TC39: Promises, Promises](https://thefeedbackloop.xyz/tc39-promises-promises/)
- [Promise-based functions should not throw exceptions](http://www.2ality.com/2016/03/promise-rejections-vs-exceptions.html)
- [Tracking unhandled rejected Promises](http://www.2ality.com/2016/04/unhandled-rejections.html)

## Cancel promise

```js
const controller = new AbortController();

someAsyncFunction(signal){
	return new Promise((resolve, reject) => {
		if(signal.aborted){
			reject(new AbortError())
		}

		signal.addEventListener("abort" event => {
			// cancel current operation
			reject(new AbortError());
		})

		// start async operation with some callbacks
	});
}

const promise = someAsyncFunction(controller.signal).catch(reason => console.log("promise catch", reason));
controller.abort();
```

Alternatively using iterator / generator:

```js
async someAsyncFunction(signal){
	//in loop over async iterator / generator
	{
		if(signal.aborted){
			throw new AbortError();
		}

		// pass the signal to sub async function and read iterator / generator (wait promise)
	}
}
```

- [AbortController - Web API | MDN](https://developer.mozilla.org/en-US/docs/Web/API/AbortController)
- [Async iterator and generator - JakeArchibald.com](https://jakearchibald.com/2017/async-iterators-and-generators/)

### Promise queue

Aka promise batch

```js
/**
 * Execute async tasks in parallel
 * @param {Iterable.<function():(Promise|*)>} tasks List of tasks to execute
 * @param {number} max Maximum tasks in parallel
 */
function parallel(tasks, max = 1){
	const taskMap = new Map();
	const promises = [];// create proxy promises for all tasks, will be resolved by the task promise is created
	for(const task of tasks){
		let resolve = null;
		promises.push(new Promise(r => resolve = r));
		taskMap.set(resolve, task);
	}

	(async () => {
		const pendingPromises = new Map();

		for(const [resolve, task] of taskMap) {
			// Wait until a slot of pending queue freed
			if(pendingPromises.size >= max){
				const ref = await Promise.race(pendingPromises.values());
				pendingPromises.delete(ref);
			}

			try{
				const promise = Promise.resolve(task());
				const ref = resolve;// use the resolve function as identifier, but could also use `const ref = Symbol();`
				pendingPromises.set(ref, promise.then(() => ref, () => ref));
				resolve(promise);// the task promise used as result of the "real" promise
			}catch(error){
				resolve(Promise.reject(error));
			}
		}
	})();

	return promises;
}

// Example: network requests
// on https://www.example.com/ enable slow connection
const tasks = Array.from({length: 21}).map((v, i) => () => fetch(`https://www.example.com/${i}`));
Promise.allSettled(parallel(tasks, 2)).then(results => console.table(results));

// Example: long running tasks
// or in performance tab under "Timings" (Chrome)
const wait = delay => new Promise(resolve => setTimeout(resolve, delay));
const tasks = Array.from({length: 21}).map((v, i, {length: total}) => () => {
	performance.mark(`task${i}-start`);
	return wait(500 + Math.random() * 1500).then(() => {
		performance.mark(`task${i}-end`);
		performance.measure(`measure task ${i} of ${total}`, `task${i}-start`, `task${i}-end`);
		return `task${i}`;
	});
});
Promise.allSettled(parallel(tasks, 2)).then(results => console.table(results));
```

- [Async map with limited parallelism in Node.js | by Alex Ewerlöf | codeburst](https://codeburst.io/async-map-with-limited-parallelism-in-node-js-2b91bd47af70)

## Type

**Prefere use one type by variable.**

JavaScript is dynamic type, but it hard to debug if you use more than one type per variable.

To make the debug easier comment variable type by using [JSDoc comment](#comments) like:

```js
/**
 * My own string variable
 * @type {string}
 */
const myString = "a string";
```

## Always declare object properties in same order

Don't:
```js
const a = {property1: "1", property2: "2"};
const b = {property2: "4", property1: "3"};
```

instead:

```js
const a = {property1: "1", property2: "2"};
const b = {property1: "3", property2: "4"};
```

Don't:

```js
const a = {property1: "1", property2: "2"};
const b = {property1: "3"};
if(condition){
	b.property2 = "4";
}
```

instead:

```js
const a = {property1: "1", property2: "2"};
const b = {property1: "3", property2: condition ? "4" : null};
```

or

```js
const a = {property1: "1", property2: "2"};
const b = {property1: "3", property2: null};
if(condition){
	b.property2 = "4";
}
```

See [hidden class](#hidden-classes)

## Don't use `delete`

Don't use `delete` on instance of classes or classless similar objects ("point" objects: `{x: 0, y: 0}`, etc.). It's modifies [hidden class](#hidden-classes) of the object.

Set to `null` instead, or (only if you have a prototype chain) use:

```js
if(someObject.hasOwnProperty("property")){
	delete someObject.property;
}
```

- [Understanding delete — Perfection Kills](http://perfectionkills.com/understanding-delete/)
- [delete operator - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete)
- [Writing Fast, Memory-Efficient JavaScript – Smashing Magazine](https://www.smashingmagazine.com/2012/11/writing-fast-memory-efficient-javascript/#de-referencing-misconceptions)

## Hidden classes

Always use the same type in same property

- [JavaScript Engines Hidden Classes (and Why You Should Keep Them in Mind) | victor felder](https://web.archive.org/web/20201021072104if_/https://draft.li/blog/2016/12/22/javascript-engines-hidden-classes/)
- [Design Elements](https://github.com/v8/v8/wiki/Design%20Elements#fast-property-access)
- [Performance Tips for JavaScript in V8 - HTML5 Rocks](http://www.html5rocks.com/en/tutorials/speed/v8/#toc-topic-hiddenclasses)
- [Understanding the V8 Runtime to Maximize Application Performance](http://www.slideshare.net/DanielFields9/understanding-the-v8-runtime-to-maximize-application-performance#slide=23)
- [Scratch Paper: V8: JavaScript Virtual Machine](http://lizstinson.blogspot.fr/2009/06/v8-javascript-virtual-machine.html)
- [Optimizations tricks in V8](https://medium.com/@ghaiklor/optimizations-tricks-in-v8-d284b6c8b183)
- [Breaking the JavaScript Speed Limit with V8 - Google IO 2012](http://v8-io12.appspot.com/#29)
- > Prefer monomorphic code to polymorphic code
	— [How the V8 engine works?](http://thibaultlaurens.github.io/javascript/2013/04/29/how-the-v8-engine-works/)

## Loop over array like

```js
for(let item of arraylike){

}
```

- [Performance optimizations and for loops](http://www.2ality.com/2013/07/for-loop-performance.html)

### Cache length

**It's not needed, because it faster only for millions of iterations.** See [Micro optimization are useless](#micro-optimization-are-useless)

```js
for (let i = 0; i < arr.length; i++);
```

vs

```js
for (let i = 0, len = arra.length; i < len; i++);
```

For array is seem not nesessary, but for Array like node collections (especially for [live collections](https://stackoverflow.com/questions/28163033/when-is-nodelist-live-and-when-is-it-static/28163742#28163742))

- [How the Grinch stole array.length access](http://mrale.ph/blog/2014/12/24/array-length-caching.html)

## Object

Always programming in object (OOP) instead of procedural if your code use more than 50 lines.

It's cleaner, easy to read and easier to debug.

Objects should fixed and immutable : new properties can't be added or be reconfigured, but properties can be changed if they are writable.

You have to create sub classes of defined classes if you want to add or reconfigure.

The concept of namespace don't exist on JS. Use es6 modules instead or simply use a name like `MLClass` for class `Class` of "mylib" namespace.

```js
this.[[HomeObject]] == Object.getPrototypeOf(Object.getPrototypeOf(this)).%method%.call(this);
```

ES6 class

- https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Object/create
- https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Object/defineProperty
- https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Object/seal
- https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Object/freeze

Private properties or methods use specific [name convention](#scoped-variable) like prefix `_` (eg. `_property`) or [double square brackets](http://www.ecma-international.org/ecma-262/5.1/#sec-8.6.2).

### Data properties on prototype

> A class body can only contain methods, no data properties. Prototypes having data properties is generally considered an anti-pattern, so this just enforces a best practice
— [Classes in ECMAScript 6 (final semantics)](http://www.2ality.com/2015/02/es6-classes-final.html)

> Avoid prototype properties with initial values for instance properties
— [Data in prototype properties](http://www.2ality.com/2013/09/data-in-prototypes.html)

> Class declarations to declare and define the capabilities of a class. Not its members. An ES6 class declaration defines its contract for its user.
> [...] a class definition defines prototype methods
— [javascript - ES6 class variable alternatives - Stack Overflow](https://stackoverflow.com/questions/22528967/es6-class-variable-alternatives/22986568#22986568)

So define in constructor, always in the same order without any condition

See also:

- [javascript - Should I put default values of attributes on the prototype to save space? - Code Review Stack Exchange](http://codereview.stackexchange.com/questions/28344/should-i-put-default-values-of-attributes-on-the-prototype-to-save-space)
- [OptionalProperties vs MandatoryProperties · jsPerf](http://jsperf.com/12312412354/2)
- [Design Elements - Chrome V8 — Google Developers](https://developers.google.com/v8/design#prop_access)

### `typeof` object

```js
typeof null === "object"
typeof function(){} === "function"
```

Use `obj === Object(obj)`

- [javascript - Underscore.js _.isObject = function (obj) { return obj === Object(obj); }; - Stack Overflow](https://stackoverflow.com/questions/23545656/underscore-js-isobject-function-obj-return-obj-objectobj)
- Not the same: [Object.is() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is)

### `this`

Could be equal to self

```js
const obj = {
	f(){
		return this;
	}
}
(false || obj.f)()// undefined
obj.f.apply(null)
```

```js
obj.method('a') // short for: obj.method.call(obj.method, 'a')
func('a') // short for: func.call(undefined, 'a')
```

- inside callable entities:
	- function call: `this === undefined` (strict mode)
		- sloppy mode: `this === window`
	- method call: `this` is receiver of call
		- direct method call: first parameter of `.call()`
	- `new: this` refers to newly created instance
- top-level scope:
	- `<script>` element: `this === window`
	- ES modules: `this === undefined`
	- CommonJS modules: `this === module.exports`

- [Why is (0,obj.prop)() not a method call?](http://www.2ality.com/2015/12/references.html)
- [JavaScript’s this: how it works, where it can trip you up](http://2ality.com/2014/05/this.html)

## Conditional function body

[GuardClause](http://c2.com/cgi/wiki?GuardClause)

Use:

```js
function myFunction(){
	if(condition){
		return;
	}

	// Rest of long code
}
```

Instead of:

```js
function myFunction(){
	if(!condition){
		// Rest of long code
	}
}
```js

In the same idea you can use labels and break:

```js
check: if(condition){
	if(other_condition){
		break check;
	}

	//...default
}

always_do_something;
```

```js
check: {
	//...
	if(condition){
		break check;
	}
	//...default
}

always_do_something;
```

## Function

Avoid as possible, function declared in other functions.

When your function is related to a different context of execution, use bound functions instead of closures:

```js
const callback = myObject.myFunction.bind(myObject);
//
callback();
// equal to:
myObject.myFunction();
```

Require a _ECMAScript 5th Edition_ / _JavaScript 1.8.5_ compatbile JavaScript engine.

That usally required when a callback is provided when listing event or when a control program flow (`addEventListener`, `setTimeout`, etc.)

Don't forget to keep a reference to the bounded function to remove it reference as listener: `removeEventListener("event", boundFunction, false)`

- https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Function/bind

Avoid as possible global variable in function:

```js
function mouseOnLeftSide(mouseX, windowWidth) {
	return mouseX < windowWidth / 2;
}
```

Instead of

```js
function mouseOnLeftSide(mouseX) {
	return mouseX < window.innerWidth / 2;
}
```

Allow test

[Immediately-invoked function expression (IIFE)](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression), aka self calling function, self invoking function or self-executing anonymous function:


```js
// ES5:
(function(arg){
	console.log(arg)
})("val1");
```

```js
// ES6 equivalent using a block statement:
{
	let arg = "val1";
	console.log(arg);
}
```

- [Making your JavaScript Pure · An A List Apart Article](http://alistapart.com/article/making-your-javascript-pure)

## Variable

Declare one variable per declaration.

```js
var variable1,
  variable2,
  variable3;
```

Instead:

```js
var variable1;
var variable2;
var variable3;
```

> using one “var” for multiple var decls tho means you can’t step through them with the debugger.
— https://twitter.com/ljharb/status/690695085239861249

## Increment operator

```js
let obj = {
	_val: 0,
	get p() {return this._val},
	set p(v) {this._val = v*10},
};
console.log(++obj.p, " ", obj.p);// > 1 " " 10
```

```js
let r = (++obj.p, obj.p);
```

- [A JavaScript Typed Array Gotcha « null program](https://nullprogram.com/blog/2019/01/23/)

## Common mistakes

### Missing variable declaration

Silently conflict with a global variable.

`for (name in obj){}` instead of `for (let name in obj){}`. Where global `name` (`window.name`) will be used as variable.

### Missing semilicon

```js
const test = {
  run () {
  }
}
```


```js
(() => {
  test.run()
})()
```

```
code.js:6
(() => {
^
TypeError: (intermediate value) is not a function
```

Is due to [Automatic Semicolon Insertion](https://github.com/getify/You-Dont-Know-JS/blob/master/types%20%26%20grammar/ch5.md#automatic-semicolons)
See also https://github.com/leebyron/async-to-gen/issues/25#issuecomment-251891170

## Private slots

- `#something`:
	- [tc39/proposal-class-fields: Orthogonally-informed combination of public and private fields proposals](https://github.com/tc39/proposal-class-fields#private-fields)
- Environment of constructor (closure / functions encapsulating lexical variables, hoisted block with or ES6 modules)
	- [15.3.1 Private data via constructor environments](http://exploringjs.com/es6/ch_classes.html#_private-data-via-constructor-environments)
- `WeakMap`:
	- [Hiding Implementation Details with ECMAScript 6 WeakMaps](http://fitzgeraldnick.com/2014/01/13/hiding-implementation-details-with-e6-weakmaps.html)
	- [15.3.3 Private data via WeakMaps](http://exploringjs.com/es6/ch_classes.html#sec_private-data-via-weakmaps)
- Symbol:
	Note: They are not fully private
	- [15.3.4 Private data via symbols](http://exploringjs.com/es6/ch_classes.html#_private-data-via-symbols)
	- [ECMAScript Wiki - Symbols](http://tc39wiki.calculist.org/es6/symbols/)
	- [Symbols in ECMAScript 6](http://www.2ality.com/2014/12/es6-symbols.html#symbols_as_keys_of_internal_properties)
- Naming convention:
	`this.__property__`, `this._method`, `this.["[[something]]"]` + use `Object.defineProperty` to set `enumerable:false`
	- [15.3.2 Private data via a naming convention](http://exploringjs.com/es6/ch_classes.html#_private-data-via-a-naming-convention)

- [Private Members in JavaScript](http://www.crockford.com/javascript/private.html)
- ['Private Variables in JavaScript' by Marcus Noble](https://marcusnoble.co.uk/2018-02-04-private-variables-in-javascript/)
- [15. Classes](http://exploringjs.com/es6/ch_classes.html#sec_private-data-for-classes)

## Weak references

- `WeakMap`
- [Expando](https://developer.mozilla.org/en-US/docs/Glossary/Expando) on [HTMLCollection](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection):

```js
function makeWeakRef(obj) {
	const key = "#weakref-" + (makeWeakRef.count = (makeWeakRef.count || 0) + 1);// non existing element, use a different key each call
	let collection = document.getElementsByTagName(key);// HTMLCollection (live)
	collection.expando = obj;
	collection = null;// unreference the collection to discard it in returned functions closures

	return {
		get() {
			return document.getElementsByTagName(key).expando;
		}
	};
}

let obj = { foo: 'bar' };
const wr = makeWeakRef(obj);
console.log('before', wr.get());
obj = null;

// ... later
console.log('later', wr.get());// could return object or undefined
```

- [tc39/proposal-weakrefs: WeakRefs](https://github.com/tc39/proposal-weakrefs)
- [Domenic Denicola on Twitter: "Weak reference polyfill, works in at least some browsers today: https://t.co/IU4nJkX6yi Who knew!!"](https://twitter.com/domenic/status/1052940242381103104?s=12)

## Data binding

- http://www.sellarafaeli.com/blog/native_javascript_data_binding

## Semicolon

- http://robertnyman.com/2008/10/16/beware-of-javascript-semicolon-insertion/

## Comments

Comment all your code particularly your functions. Give it a name is great, but not mean exactly what it's doing nor inputs (arguments) and ouputs (return)

Use [JSDoc](http://usejsdoc.org/index.html) to define meta informations like variable type, function return type, function parameters, etc.

```js
/**
 * @param {String|Array} [somebody=John Doe] Name or array of names
 * @returns {String}
 */
function getGreeting(somebody) {
	if (!somebody) {
		somebody = "John Doe";
	} else if (Array.isArray(somebody)) {
		somebody = somebody.join(", ");
	}
	return "Hello " + somebody;
}
```

Explain via comments the functioning of code blocks. But dont use useless comments, like your own feeling.

```js
// That's fuck up
```

- Function: description, arguments, return
- Program flow branch (if, else)(+ loops?): condition
- Code block : description
- Everywhere : description

Use also `TODO`.

- [Are JavaScript Comments Useless? | Zsolt Nagy](http://www.zsoltnagy.eu/are-javascript-comments-useless/)

### Comment toggle

```js
/*
[code]
//*/
```

```js
//*
[code]
//*/
```

Only add `/` char to comment

```js
//*
[code 1]
/*/
[code 2]
//*/
```

```js
/*
[code 1]
/*/
[code 2]
//*/
```

## Quotes

**No differences between simple vs double quotes. Only be consistent across your code.**

The "default" quote is double quote, so use it. Simple quotes are harder to read with ticks. (`""`, `''`, `` ``)

JSON use double quotes only. Some languages use double quotes only to represent a string.

Like in XML or HTML simple quote could be use, but don't use it. Use instead double quote, it's not PHP where [double quote are different than simple one](http://www.php.net/manual/en/language.types.string.php#language.types.string.parsing "Variable parsing in PHP").

```js
const rawHTML = "<input type=\"text\" value=\"test\">";
```

Or use JS templates:

```js
const rawHTML = `<input type="text" value="test">`;
```

- [JavaScript: single quotes or double quotes?](http://www.2ality.com/2012/09/javascript-quotes.html)
- [string - When to use double or single quotes in JavaScript? - Stack Overflow](https://stackoverflow.com/questions/242813/when-to-use-double-or-single-quotes-in-javascript)
- [Should I use (') or (")? : javascript](https://www.reddit.com/r/javascript/comments/4m715v/should_i_use_or/)

## Condition

If possible use positive conditions

> Stop the if ( !foo ). Stay sane and use if ( foo === false ), if ( foo === null ) or if ( foo === undefined )
— https://twitter.com/mrdoob/status/392411230863773696

### Conditional compilation

```js
// The compiler define global constant PRODUCTION as boolean
if(!PRODUCTION){
    console.log("debug");
}
```

or

```js
// The compiler define special packages
import {PRODUCTION} from "constants";

if(!PRODUCTION){
    console.log("debug");
}
```

- [DefinePlugin | webpack](https://webpack.js.org/plugins/define-plugin/)
- [Annotating JavaScript for the Closure Compiler · google/closure-compiler Wiki](https://github.com/google/closure-compiler/wiki/Annotating-JavaScript-for-the-Closure-Compiler#define-type-description)
- [Conditional Compilation (Windows Scripting - JScript) | Microsoft Docs](https://docs.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/scripting-articles/121hztk3%28v%253dvs.84%29?redirectedfrom=MSDN)

### Block condition

See [Return condition](#return-condition)

Block statment with a label:

```js
lotOfStatments: {
	statment1;
	statments;
	if(condition){
		break lotOfStatments;// stop any further statments of lotOfStatments
	}
	otherStatments;
}
```

- https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Statements/block

### Return condition

See [Block condition](#block-condition)

Filter first, use less conditional blocks

```js
function test(param = 0){
	if(param == 0){
		return
	}

	// do stuff
}
```

```js
function test(param = 0){
	if(param != 0){
		// do stuff
	}
}
```

## Getters/setters vs method

```js
class MyClass {
	constructor(n){
		this._total = n;
		this._store = [];
	}
	add(n) {
		this._store.push(n); // or whatever you need to store n
		this._total += n; // update the total sum
	}
	get sum() {
		// could use return this._store.reduce((prev, cur) => prev + cur, 0)
		return this._total;
	}
	// ...
}
```

Use methods when you are doing something (verb) and use getters/setters when you are checking a property (noun.)

## ES6

- http://blog.jetbrains.com/idea/2012/03/javascript-version-selector/
- http://blog.tastejs.com/rewriting-a-webapp-with-ecmascript-6
- [joshburgess/not-awesome-es6-classes: A curated list of resources on why ES6 (aka ES2015) classes are NOT awesome](https://github.com/joshburgess/not-awesome-es6-classes)

## Recursion

vs iteration

- [Tail call optimization in ECMAScript 6](http://2ality.com/2015/06/tail-call-optimization.html)
- [Tail call — Wikipedia](https://en.wikipedia.org/wiki/Tail_call)
- [Recursion, iteration and tail calls in JS](http://www.jstips.co/en/javascript/recursion-iteration-and-tail-calls-in-js/)
- [ES6 Tail Call Optimization Explained · Kyle Owen](http://benignbemine.github.io/2015/07/19/es6-tail-calls/)
- [JS ES6 Recursive Tail Call Optimization – Michael Laythe – Medium](https://medium.com/@mlaythe/js-es6-recursive-tail-call-optimization-feaf2dada3f6)
- [Javascript fonctionnel: Recursion suite: Algorithme d'Euclide et Tours de Hanoi](http://jsfunctionnal.blogspot.com/2008/09/recursion-suite.html) and [Javascript fonctionnel: Javascript récursif, suite](http://jsfunctionnal.blogspot.com/2008/09/javascript-rcursif-suite.html) - Example with Fibonacci suite

## Feature detection

- [Some ES6 features detection](https://gist.github.com/DaBs/89ccc2ffd1d435efdacff05248514f38) see also [ES6 feature detection, shamelessly copied from Netflix : javascript](https://www.reddit.com/r/javascript/comments/5q9gxg/es6_feature_detection_shamelessly_copied_from/)
- https://kangax.github.io/compat-table/es6/

Instead of:

```js
function something() {
	if("something" in obj) {
		// something
	}
	else {
		// fallback
	}
}
```

do:

```js
const something = ("something" in obj) ? function() {
	// something
} : function() {
	// fallback
};
```

If you need to detect host object, instead of `"WheelEvent" in self` or `"WheelEvent" in window`, use `typeof WheelEvent == "function"`.

See [detect a feature](Web#detect-a-feature)

## Don't extend build-in types

And the DOM.

Don't add expando properties (eg.: `object.newProperty = "value"`). Use `WeakMap` instead.

Unless it's to backport the features of newers ECMAscript engines (like `Array.forEach`).

- [What's wrong with extending the DOM — Perfection Kills](http://perfectionkills.com/whats-wrong-with-extending-the-dom/)
- [Inheritance and the prototype chain - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain#Bad_practice.3A_Extension_of_native_prototypes)

## Comma operator

```js
const x = ("a", "b", "c");// x == "c"
```

> The comma operator has the lowest priority of all operators

Usefull for [arrow function](#arrow-function): `x => (a(), b())`

- [Comma operator - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comma_Operator)

## Engines

- [cesanta/mjs: Embedded JavaScript engine for C/C++](https://github.com/cesanta/mjs)
- [cesanta/elk: A low footprint JavaScript engine for embedded systems](https://github.com/cesanta/elk)
- [XS7 @ TC-39](https://www.moddable.com/XS7-TC-39.php)
- [QuickJS Javascript Engine](https://bellard.org/quickjs/) - [bellard/quickjs](https://github.com/bellard/quickjs)
- [List of ECMAScript engines - Wikipedia](https://en.wikipedia.org/wiki/List_of_ECMAScript_engines)

- [Test262 Report](https://test262.report/)

- [Node.js](https://nodejs.org/)
- [denoland/deno: A secure JavaScript and TypeScript runtime](https://github.com/denoland/deno)
- [nodejs/node-chakracore: Node.js on ChakraCore](https://github.com/nodejs/node-chakracore)

### How engine works

- [dexteryy/spellbook-of-modern-webdev: A Big Picture, Thesaurus, and Taxonomy of Modern JavaScript Web Development](https://github.com/dexteryy/spellbook-of-modern-webdev#platform-compatibility-and-proposal-status)
— [How the V8 engine works?](http://thibaultlaurens.github.io/javascript/2013/04/29/how-the-v8-engine-works/)
- [V8 JavaScript Engine: Optimizing hash tables: hiding the hash code](https://v8project.blogspot.fr/2018/01/hash-code.html)
- [JavaScript engine fundamentals: optimizing prototypes · Mathias Bynens](https://mathiasbynens.be/notes/prototypes)
- [Compiler Compiler: A Twitch series about working on a JavaScript engine - Mozilla Hacks - the Web developer blog](https://hacks.mozilla.org/2020/06/compiler-compiler-working-on-a-javascript-engine/)
- [Speculation in JavaScriptCore | WebKit](https://webkit.org/blog/10308/speculation-in-javascriptcore/)
- [Warp: Improved JS performance in Firefox 83 - Mozilla Hacks - the Web developer blog](https://hacks.mozilla.org/2020/11/warp-improved-js-performance-in-firefox-83/)

### Event loop

![Nodejs Event Loop   Bert Belder](Nodejs%20event%20loop%20-%20Bert%20Belder.jpg)
![Nodejs Event Loop 2   Bert Belder](Nodejs%20event%20loop%202%20-%20Bert%20Belder.jpg)

> Immediately after every macrotask, the engine executes all tasks from microtask queue, prior to running any other macrotasks or rendering or anything else.
>
> — [Event loop: microtasks and macrotasks](https://javascript.info/event-loop#macrotasks-and-microtasks)

```js
setTimeout(() => console.log("timeout"));
Promise.resolve().then(() => console.log("promise"));
console.log("body");
requestAnimationFrame(() => console.log("requestAnimationFrame"));
await console.log("await");
console.log("after await");
requestAnimationFrame(() => console.log("requestAnimationFrame 2"));
// will log:
// (macrotask: script)
// 1. body: synchronous call
// (microtask)
// 2. await: this part of the script body is put the microtask queue and executed if the Promise is resolved. console.log() doesn't return a promise therefore it's considered as "resolved" ("fulfilled")
// 3. promise: resolved promise executed in from the microtask queue before next macrotask
// 4. after await: executed after the previous promise
// (update rendering if suitable)
// 5. requestAnimationFrame
// 6. requestAnimationFrame 2
// (macrotask: timers)
// 7. timeout
// (update rendering if suitable)
// (5 and 6 could instead be executed here)
```

- [Tasks, microtasks, queues and schedules - JakeArchibald.com](https://web.archive.org/web/20210419055331/https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/)
- [The Node.js Event Loop, Timers, and process.nextTick() | Node.js](https://web.archive.org/web/20201117083749/https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/)
- [Philip Roberts Help I'm stuck in an event loop - YouTube](https://www.youtube.com/watch?v=6MXRNXXgP_0)
- [Philip Roberts: What the heck is the event loop anyway? | JSConf EU 2014 - YouTube](https://www.youtube.com/watch?v=8aGhZQkoFbQ)
- [Jake Archibald: In The Loop - JSConf.Asia - YouTube](https://www.youtube.com/watch?v=cCOL7MC4Pl0&feature=youtu.be)
- [Event loop processing model - HTML Standard](https://html.spec.whatwg.org/multipage/webappapis.html#event-loop-processing-model)
- [⭐️🎀 JavaScript Visualized: Promises & Async/Await - DEV](https://web.archive.org/web/20201127083654/https://dev.to/lydiahallie/javascript-visualized-promises-async-await-5gke#tasks)

- [How JavaScript works: memory management + how to handle 4 common memory leaks | by Alexander Zlatkov | SessionStack Blog](https://web.archive.org/web/20201115130752/https://blog.sessionstack.com/how-javascript-works-memory-management-how-to-handle-4-common-memory-leaks-3f28b94cfbec?gi=e35da23f4d92)
- [Concurrency model and Event Loop - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)
- [Asynchronous Adventures in JavaScript: Understanding the Event Loop](https://web.archive.org/web/20191013173002/https://medium.com/dailyjs/asynchronous-adventures-in-javascript-understanding-the-event-loop-fc6f968d5f72)

## `finally` is executed after return

```js
function test(){
	try{
		console.log("before test() returns");
		return;
		console.log("after test() returns in try");// never called
	}
	finally{
		console.log("after test() returns in finally");
	}
}
```

```js
console.log("before test()");
test();
console.log("after test()");
```

Output:

1. `before test()`
2. `before test() returns`
3. `after test() returns in finally`
4. `after test()`

# Tips

## Check if variable is declared

```js
typeof undeclaredVariable === 'undefined'
```

- http://speakingjs.com/es5/ch09.html#_checking_whether_a_variable_exists

## Hexadecimal string as number

```js
function hexaToNumber(value){
	return parseInt(value.substr(1), 16);//#RRGGBB
}
```

```js
"#" + ( color | 0).toString(16).padStart(6, "0")
```

## Extract color component from color number

Aka hexadecimal color extraction

```js
const colorRGB = 0xff00cc;

const redChannel = colorRGB >> 16;
const greenChannel = colorRGB >> 8 & 0xff;
const blueChannel = colorRGB & 0xff;
```

Or 32 bit color (argb)

```js
const colorARGB32 = 0xddff00cc;

const alphaChannel = colorARGB >> 24 & 0xff;
const redChannel = colorARGB >> 16 & 0xff;
const greenChannel = colorARGB >> 8 & 0xff;
const blueChannel = colorARGB & 0xff;
```

```js
//Or alpha and 24 bits color:
const alphaChannel = colorARGB >> 24 & 0xff;
const colorRGB = colorARGB & 0xffffff;
```

## Color component to color number

Aka hexadecimal from color components

```js
const redChannel = 0xff;
const greenChannel = 0x00;
const blueChannel = 0xcc;
const colorRGB = redChannel << 16 | greenChannel << 8 | blueChannel;
```

Or 32 bit color (argb)

```js
const alphaChannel = 0xdd;
const redChannel = 0xff;
const greenChannel = 0x00;
const blueChannel = 0xcc;
const colorARGB32 = alphaChannel << 24 | redChannel << 16 | greenChannel << 8 | blueChannel;
```

## Ratio

Divide both terms of the ratio by the greatest common factor :

For `24:40` (`24/40`) the greatest common factor is 8:

```
24/8 = 3
40/8 = 5
```

`24:40` equals to `3:5`

- http://andrew.hedges.name/experiments/aspect_ratio/

## Duplicate values

Aka unique values, remove duplicated values

```js
const uniq = [... new Set([1, 2, 3, 4, 5, 1, 2, 6])];
```

```js
const hasDup = ![1, 2, 3, 4, 5, 1, 2, 6].every((value, index, array) => array.indexOf(value) === index);//true
const hasDup = array.length !== new Set(array).size;
```

```js
// Remove duplicate after
const uniq = [1, 2, 3, 4, 5, 1, 2, 6].filter((value, index, array) => index === 0 || array.indexOf(value) === index);//[1, 2, 3, 4, 5, 6]
// Remove duplicate first
const uniq = [1, 2, 3, 4, 5, 1, 2, 6].filter((value, index, array) => !array.includes(value, index + 1));//[3, 4, 5, 1, 2, 6]
```

```js
let uniqueValues = values.reduce((dest, search) => {
	if (dest.indexOf(search) < 0){
		dest.push(search);
	}
	return dest;
}, []);
```

## Store data as stringified JSON

Store object, array stringified JSON that could be parsed at execution, faster than JS.

- [Mathias Bynens on Twitter: "🚀 Perf tip: if your web app ships large JSON-like configuration as JavaScript object literals, consider using JSON.parse instead. It’s much faster, especially for cold loads! https://t.co/C0oQ4BLnfz https://t.co/p0WICUm7zx" / Twitter](https://twitter.com/mathias/status/1143551692732030979?s=12)
- [The cost of JavaScript in 2019 · V8](https://v8.dev/blog/cost-of-javascript-2019#json)
- [Faster apps with JSON.parse (Chrome Dev Summit 2019) - YouTube](https://www.youtube.com/watch?v=ff4fgQxPaO0)

## Relative index offset

Support forced direction

```js
var toIndex;// start
var fromIndex;// end
var forcedDirection;// -1, 0, +1
var count;// num elements
var offset = 0;
if(toIndex > fromIndex){
	offset = this._transitionDirection < 0 || toIndex - fromIndex > count / 2 ? count + fromIndex - toIndex : fromIndex - toIndex;
}else{
	offset = this._transitionDirection > 0 || fromIndex - toIndex > count / 2 ? count + toIndex - fromIndex : toIndex - fromIndex;
}
```

For infinite loop

```js
var index = fromIndex + offset;//offset = relative index
var absIndex = (count + index % count) % count;// real index (support negative index)
```

## Insert property in object with order

**It's recommended to use `Map` instead of an object with properties for that.** See why in [Don't use `delete`](#dont-use-delete).

```js
function insert(obj, {before, property, value}) {
	for (let p in obj) {
		if (p === before) {
			obj[property] = value;
			found = true;
		}

		// p comes after the new property, delete it and re-add it to push it to the end
		if (found) {
			let temp = obj[p];
			delete obj[p];
			obj[p] = temp;
		}
	}
}
```

- [Lea Verou on Twitter: "#JS The only way to insert a property before another in an object literal and maintain references to it, is to delete all properties onwards, insert your property, then re-add. Here are 3 different helpers for this: https://t.co/GTOgYmv3hp Which one is best? Can you do better?" / Twitter](https://twitter.com/LeaVerou/status/1329793951973470214)

## Inside rect

```js
function inside (x, y, box){
	return x > box.l && y > box.t && x < box.r && y < box.b;
}
```

## Days in month

```js
function daysInMonth ( y, m ) {
	return ( new Date( y, m, 0 ) ) .getDate();
}
daysInMonth( 2015, 2 ); //28
daysInMonth( 2016, 2 ); //29
```

## Progress

```js
let progress = (now - start) / duration % 1;// 0->1 cycles
progress = (progress < 0.5) ? progress * 2 : 1 - (progress - 0.5) * 2;// 0->1->0 cycles
```

### In time

```js
let filesize = ...;
let lastpercent = 0;
let starttime = Date.time();
function human(size){
	let units = ['B','KiB','MiB','GiB','TiB','PiB', 'EiB', 'ZiB', 'YiB'];
	let unitIndex = 0;
	while(size > 1024 && unitIndex < units.length){
		size /= 1024;
		unitIndex++;
	}

	return ((size * 10) / 10) + units[unitIndex];// round to ###.##
}

while(...){
	let currentseek = ...;

	if(currentseek / filesize > lastpercent){
		let percent = (currentseek / filesize * 1000) / 10;// round ###.##
		console.log(percent + '%');
		lastpercent += 0.01;
		console.log(human(currentseek) + '/' + human(filesize));
		if(percent != 0){
			let now = Date.time();
			let estimate = (now - starttime) / percent * 100
			eta = starttime + estimate - now
			console.log(`ETA: ${eta}s' (estimate ${estimate}s)`);
		}
	}
}
console.log("done!");
```

- XSLT `###.##` `format-number()`
- [Binary prefix — Wikipedia](https://en.wikipedia.org/wiki/Binary_prefix#kibi)

## Regular expression

Aka RegExp

- [Regular Expressions - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)
- [RegExr: Learn, Build, & Test RegEx](http://regexr.com/)
- [ES proposal: RegExp Unicode property escapes](http://2ality.com/2017/07/regexp-unicode-property-escapes.html)

- number: `/^[-+]?(\d*\.?\d+|\d+\.)$/` (-1, .05, +1000, 3.1415925)
- backref: `/('|").+?\1/g` `/('|")(\\?.)*?\1/g` `/<([a-z]+)>[^<]*<\/\1>/`

See also [RegExp](RegExp)

- single HTML tag `/^<([a-z][^\/\0>:\x20\t\r\n\f]*)[\x20\t\r\n\f]*\/?>(?:<\/\1>|)$/i` (from https://github.com/jquery/jquery/blob/master/src/core/var/rsingleTag.js)

### Look behind and look after

- [regex - Javascript: negative lookbehind equivalent? - Stack Overflow](https://stackoverflow.com/questions/641407/javascript-negative-lookbehind-equivalent)
- [Flagrant Badassery » Mimicking Lookbehind in JavaScript](http://blog.stevenlevithan.com/archives/mimic-lookbehind-javascript)

### Problems with the Flag "g"

Be carefull when create/inline regex in loops. Regex are muttable (`lastIndex` property is used to keep iterator infos)

```js
// Don’t do that:
var count = 0;
while (/a/g.test('babaa')) count++;
```

But

```js
var count = 0;
var regex = /a/g;
while (regex.test('babaa')) count++;
```

```js
// Don’t do that:
function extractQuoted(str) {
	var match;
	var result = [];
	while ((match = /"(.*?)"/g.exec(str)) != null) {
		result.push(match[1]);
	}
	return result;
}
```

But

```js
const QUOTE_REGEX = /"(.*?)"/g;
function extractQuoted(str) {
	QUOTE_REGEX.lastIndex = 0;
	var match;
	var result = [];
	while ((match = QUOTE_REGEX.exec(str)) != null) {
		result.push(match[1]);
	}
	return result;
}
```

- [Chapter 19. Regular Expressions # Problems with the Flag /g](http://speakingjs.com/es5/ch19.html#tips_flag_g)


## String padding

```js
var n = 13;
```

```js
String(n).padStart(3, "0");// -> "013"
```

```js
("000" + n).substr(-3, 3);// -> "013"
```

```js
("000" + n).slice(-3);// -> "013"
```

`"000"` replace with `"0".repeat(3)`

- [convert '1' to '0001' in JavaScript - Stack Overflow](https://stackoverflow.com/questions/5366849/convert-1-to-0001-in-javascript)
- [ES proposal: string padding](http://www.2ality.com/2015/11/string-padding.html)

## Power of two

### Is power of two

```js
let isPositivePowerOfTwo = a > 0 && (a & (a - 1)) == 0;
```

### Round to nearest power of two

```js
// returns the closest (high) number that is a power of two
function getNextPowerOfTwo(number)
{
	if (number > 0 && (number & (number - 1)) === 0)
	{
		return number;
	}
	else
	{
		var result = 1;

		while (result < number)
		{
			result <<= 1;
		}

		return result;
	}
}
```

```js
function roundToPowerOfTwo(value) {
	let rounded = 2;
	while (value > rounded) {
		rounded *= 2;
	}

	return rounded;
}
```

- [java - Nearest multiple of a power of two fraction - Stack Overflow](https://stackoverflow.com/questions/28238149/nearest-multiple-of-a-power-of-two-fraction)
- http://en.wikipedia.org/wiki/Power_of_two#Fast_algorithm_to_check_if_a_positive_number_is_a_power_of_two

Java `org.jctools.util.Pow2.roundToPowerOfTwo()`

### Round of two

```js
Math.ceil(value / 2) * 2;
```

See [Round to multiple](#round-to-multiple)

## Odd and even

```js
value % 2
```

```js
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9].map(value => Math.round(value % 2))
// -> [0, 1, 0, 1, 0, 1, 0, 1, 0, 1]
```

Double odd

```js
Math.round(value % 4 / 4)
```

```js
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9].map(value => Math.round(value % 4 / 4))
// -> [0, 0, 1, 1, 0, 0, 1, 1, 0, 0]
```

Triple odd:

```js
Math.round(value % 6 / 6)
```

etc.

## Center of 2 points

```js
let x1 = 10;
let x2 = 20;
let xC = (x1 + x2) / 2;// 15
```

## Scale control point

```js
let transformOriginX;
let transformOriginY;
let scale;
let x;
let y;
let newScale = scale;
let previousScale;
scale = newScale;

// Adjust with transformOrigin
let localTransformOriginX = (transformOriginX - x) / previousScale;
let localTransformOriginY = (transformOriginY - y) / previousScale;
x = transformOriginX - localTransformOriginX * newScale;
y = transformOriginY - localTransformOriginY * newScale;
```

## Type

### Detect type

**Do you realy need to check the type?**

Check primitive wrapped too (with `instanceof`) created by the `new` keyword `new Number(1)` (equivalent of `new Object(Number(value))`)

- [javascript - Why is 4 not an instance of Number? - Stack Overflow](https://stackoverflow.com/questions/472418/why-is-4-not-an-instance-of-number/472427#472427)

**Note: Full object constructors are per window**:
`Array` (`window.Array`) is not the same `Array` (`frame.contentWindow.Array`) in other window.
For that you should read build-in toString (not the overwritten one): `Object.prototype.toString.call(value) == "[Object Array]"`
Works for primitive wrapper too: `Object.prototype.toString.call(value) == "[Object Number]"` (`1` and `new Number(1)`)
Works for null too: `Object.prototype.toString.call(value) == "[Object Null]"`

Boolean, number, string and function:

```js
typeof value == "boolean"//"number", "string" and "function"
```

Optionaly you can use also:

```js
typeof value == "boolean" || value instanceof Boolean
```

Integer (number):

```js
Number.isInteger(value)
Number.isFinite(value)
isNaN(value)
```

Array:

```js
Array.isArray(value)
```

Array, Date and all other objects:

```js
value instanceof Array
```

Note: read above about window context of constructor and primitives

- [Nifty Snippets: Say what?](http://blog.niftysnippets.org/2010/09/say-what.html)

### Conversion

Array:

```js
Array.isArray(value) || (typeof value[Symbol.iterator] || "length" in value) && (value = Array.from(value)) || (value = Array.of(value))
```

Number:

`Number(value)` is equivalent to `+value`

```js
function strictParseFloat(value) {
	// Fix Number("")==0, Number(" ")==0, Number(null)==0, Number(), skip NaN
	if(value == undefined || value == null || value == "" || value.trim() == "" || isNaN(value)) return NaN;
	value = String(value);
	let firstChar = value.charAt(0);
	let sign = 1;
	// Fix isNaN(Number("-0x10"))
	if(firstChar == "-"){
		sign = -1;
		value = value.substr(1);
	}
	else if(firstChar == "+"){
		value = value.substr(1);
	}
	return sign * Number(value);
}

function strictParseInt(value) {
	// Fix Number("")==0, Number(" ")==0, Number(null)==0, Number(), skip NaN, value w/ decimals, negative exponent
	if(value == undefined || value == null || value == "" || value.trim() == "" || isNaN(value) || value.contains(".") || value.contains("e-")) return NaN;
	value = String(value);
	let firstChar = value.charAt(0);
	let sign = 1;
	// Fix isNaN(Number("-0x10"))
	if(firstChar == "-"){
		sign = -1;
		value = value.substr(1);
	}
	else if(firstChar == "+"){
		value = value.substr(1);
	}
	return sign * Number(value);
}
```

| value			| `parseFloat`	| `parseInt`	| `Number`		| `strictParseFloat`	| `strictParseInt`
| `"3"`			| `3`			| `3`			| `3`			| `3`					| `3`
| `"1.501"`		| `1.501`		| `1`			| `1.501`		| `1.501`				| `NaN`
| `".2"`		| `0.2`			| `NaN`			| `0.2`			| `0.2`					| `NaN`
| `"1e+10"`		| `10000000000`	| `1`			| `10000000000`	| `10000000000`			| `10000000000`
| `"2e30"`		| `2e+30`		| `2`			| `2e+30`		| `2e+30`				| `NaN`
| `"2.1e30"`	| `2.1e+30`		| `2`			| `2.1e+30`		| `2.1e+30`				| `NaN`
| `"1x"`		| `1`			| `1`			| `NaN`			| `NaN`					| `NaN`
| `"0x10"`		| `0`			| `16`			| `16`			| `16`					| `16`
| `"-0x10"`		| `-0`			| `-16`			| `NaN`			| `-16`					| `-16`
| `"0x10AF"`	| `0`			| `0`			| `4271`		| `4271`					| `4271`
| `"0o777"`		| `0`			| `0`			| `511`			| `511`					| `511`
| `"0o8"`		| `0`			| `0`			| `NaN`			| `NaN`					| `NaN`
| `"0b11"`		| `0`			| `0`			| `3`			| `3`					| `3`
| `""`			| `NaN`			| `NaN`			| `0`			| `NaN`					| `NaN`
| `" \r\n\t"`	| `NaN`			| `NaN`			| `0`			| `NaN`					| `NaN`
| `"Infinity"`	| `Infinity`	| `NaN`			| `Infinity`	| `Infinity`			| `Infinity`
| `null`		| `NaN`			| `NaN`			| `0`			| `NaN`					| `NaN`
| `undefined`	| `NaN`			| `NaN`			| `NaN`			| `NaN`					| `NaN`
| `A`			| `NaN`			| `NaN`			| `NaN`			| `NaN`					| `NaN`

Object:

See `value.valueOf()` (`Date` return number)

## Check date validity

```js
new Date(null)// > Thu Jan 01 1970 01:00:00 GMT+0100
```

```js
Number.isNaN(Number(new Date("")))// > date invalid: true
Number.isNaN(new Date("").getTime())// > date invalid: true
Number.isNaN(new Date("").valueOf())// > date invalid: true
```

Compare a date with an invalid one is always falsy: `new Date() => new Date("")`

```js
const now = new Date();
startDate, endDate
const isOpening = !(now < startDate) && !(now >= endDate);// not before and not after (handle invalid dates: compare a date with an invalid date is always falsy)
```

## Filter out `NaN`, `undefined` and `null` in Array

Aka clean

```js
[0, 1, undefined, , 2, NaN, 3, null].filter(value => typeof value == "number" && value === value);// -> [0, 1, 2, 3] keep only (real) numbers
```

```js
[0, 1, undefined, , 2, NaN, 3, null].filter(Boolean); //-> [1, 2, 3]
```

```js
[false, 0, null, undefined, ,].filter(value => !Number.isNaN(value) && value !== null && value !== undefined && value !== "");// -> [false, 0]
```

## Filter and map at the same time

```js
const persons = [
  {name: 'John', age: 73},
  {name: 'Alex', age: 3},
  {name: 'Jane', age: 22},
];
const adultNames = persons.flatMap(p => p.age >= 18 ? p.name : []);
// same as:
// persons.filter(p => p.age >= 18).map(p => p.name);
```

Note: `flatMap()` expects to see non-array entries as well as array entries

- [Arrays (`Array`) • JavaScript for impatient programmers](https://exploringjs.com/impatient-js/ch_arrays.html#flatmap-mapping-to-zero-or-more-values)

## Thousands separators

```js
// similar and simplified equivalent of toLocaleString('en-US', {minimumFractionDigits: 2})
function toLocaleString(value){
	var parts = value.split(".");
	var integerDigits = parts[0];
	var recomposedIntDigits = "";
	var offset = integerDigits.length;
	while(offset >= 3)
		grp = integerDigits.substr(offset -= 3, 3);
		recomposedIntDigits = (recomposedIntDigits == "" ? grp : grp + ",") + recomposedIntDigits
	grp = integerDigits.substr(0, offset)
	parts[0] = (grp == "+" || grp == "-" || grp == "" || recomposedIntDigits == "" ? grp : grp + ",") + recomposedIntDigits;
	return parts.join(".");
}
```

- [Number.prototype.toLocaleString() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString)

## Human byte unit

```js
var value = 12.34;
var modifier = "G";
// Decimal
switch(modifier) {
	case "Y":// yotta
		value *= 1000;
	case "Z":// zetta
		value *= 1000;
	case "E":// exa
		value *= 1000;
	case "P":// peta
		value *= 1000;
	case "T":// tera
		value *= 1000;
	case "G":// giga
		value *= 1000;
	case "M":// mega
		value *= 1000;
	case "k":// kilo
		value *= 1000;
}
// Binary (1024^x)
switch(modifier) {
	case "Yi":// yobi
		value *= 1024;
	case "Zi":// zebi
		value *= 1024;
	case "Ei":// exbi
		value *= 1024;
	case "Pi":// pebi
		value *= 1024;
	case "Ti":// tebi
		value *= 1024;
	case "Gi":// gibi
		value *= 1024;
	case "Mi":// mebi
		value *= 1024;
	case "Ki":// kibi
		value *= 1024;
}
```

Note: Switch without break will do all instructions from the matching case and continue to next break or to the end.

- [Binary prefix — Wikipedia](https://en.wikipedia.org/wiki/Binary_prefix)
- [Engineering notation — Wikipedia](https://en.wikipedia.org/wiki/Engineering_notation)
- [Metric prefix — Wikipedia](https://en.wikipedia.org/wiki/Metric_prefix)

## Clamp

```js
function clamp(value, min, max) {
	return Math.min(Math.max(min, value), max);
}
```

## Array of key-value tuples to object

```js
let obj = arr.reduce((obj, [key, value]) => ((obj[key] = value, obj)), {});
```

- [javascript - How to convert an array of key-value tuple into an object - Stack Overflow](https://stackoverflow.com/questions/32002176/how-to-convert-an-array-of-key-value-tuples-into-an-object)

## Array chunks

Split/fold array to arrays of specified size

```js
function chunk(array, size) {
	let sets = [];
	let chunks = array.length / size;

	for (let i = 0, j = 0; i < chunks; i++, j += size) {
		sets[i] = array.slice(j, j + size);
	}

	return sets;
};
```

```js
// Note about performance: reduce call callback on each value, where the previous example run loop only for each chunks
// If you have a large size, prefere using the loop
const chunk = (array, size) =>
	array.reduce(
		(sets, value, index, values) =>
			!(index % size) ? (sets.push(values.slice(index, index + size)), sets) : sets,
		[]
	)
```

## Math

	Math.exp(x) == Math.pow(Math.E, x)

	y = Math.pow(x, z)
	x = Math.pow(y, 1 / z)
	z = Math.log(y) / Math.log(x)

- https://stackoverflow.com/questions/4016213/whats-the-opposite-of-javascripts-math-pow

## Sort

Sort on multiple fields:

	items.sort((a, b) => a.prop1 - b.prop1 || a.prop2 - b.prop2);// if compare the first property gives 0, use the second property

- [json - JavaScript sort array by multiple (number) fields - Stack Overflow](https://stackoverflow.com/questions/13211709/javascript-sort-array-by-multiple-number-fields)

## Relative / absolute value

```js
/*
 * @returns "percentage" 0 -> 1
 */
function absoluteToRelative(value, min, max){
	return (value - min) / (max - min);
}

/*
 * @param value "percentage" (0 -> 1) between min and max. Where 0 = min and 1 = max
 * @returns value between min and max
 */
function relativeToAbsolute(value, min, max){
	return min + (max - min) * value;
}
```

## Median and average

Median:

```js
let sortedValues = values.slice().sort()
let halfCount = sortedValues.length / 2;
let median = sortedValues.length == 0 ? 0 : halfCount % 1 == 0 ? (sortedValues[halfCount - 1] + sortedValues[halfCount]) / 2 : sortedValues[Math.floor(halfCount)];
```

Average:

```js
let average = values.reduce((total, value) => total + value, 0) / values.length;
```

- [Median — Wikipedia](https://en.wikipedia.org/wiki/Median)
- Average Value of a Function over interval [Antiderivatives / Average Value of a Function - 1](http://archives.math.utk.edu/visual.calculus/5/average.1/index.html)

## Distribution

Over 2 stacks

```js
for(let index = 0, stack1Sum = 0, stack2Sum = 0, num = elements.length; index < num; index++){
	let element = elements[index];
	let value = element.value;
	if(stack1Sum <= stack2Sum){
		stack1Sum += value;
		stack1.push(element);
	}else{
		stack2Sum += value;
		stack2.push(element);
	}
}
```

## Random index

With linear distribution

```js
var length = 10;
var index = Math.round(Math.random() * length - 0.5);// give the same change for all indexes
```

## Flatten array

```js
function flatten(arr) {
	return [].concat.apply([], arr);
}
// flatten(["a", "b", ["c", "d"]]) => ["a", "b", "c", "d"]
```

## Get the first or last part of a string

Don't (not work if `/` is not present):

```js
let base = path.substring(0, path.indexOf("/"));
```

Use instead:

```js
let base = path.split("/", 1)[0];
let base = path.split("/", 1).shift();
// or use destructuring
let [base] = path.split("/", 1);
```

To get the last part: `path.split("/").pop()`

```js
function before(str, searchValue, fromIndex = 0){
	return str.slice(fromIndex, indexBefore(str, searchValue, fromIndex));
}

function after(str, searchValue, fromIndex = 0){
	return str.slice(indexAfter(str, searchValue, fromIndex), fromIndex);
}

function indexBefore(str, searchValue, fromIndex = 0){
	let endIndex = str.indexOf(searchValue, fromIndex);
	return endIndex < 0 ? str.length : endIndex;
}

function indexAfter(str, searchValue, fromIndex = 0){
	let endIndex = str.lastIndexOf(searchValue, fromIndex);
	return endIndex < 0 ? 0 : endIndex;
}
```

## DST (Daylight Saving Time)

Are we in DST. `date.getTimezoneOffset()` return the current offset to UTC. How to know if the user standard time (STD) or daylight saving time (DST)?

It's not accurate (due to ECMAScript standard): [javascript - Check if Daylight Saving Time is in effect, and if it is for how many hours - Stack Overflow](https://stackoverflow.com/questions/11887934/check-if-daylight-saving-time-is-in-effect-and-if-it-is-for-how-many-hours/13365722#13365722)

Or use a specific library: https://github.com/spiritit/timezonecomplete

- [Daylight saving time — Wikipedia](https://en.wikipedia.org/wiki/Daylight_saving_time)

## Random UUID

```js
crypto.randomUUID();
```

```js
// version 4 RFC-4122
function randomUUID(){
	return "xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx".replace(/[xy]/g, (c) => {
		const r = Math.random() * 16 | 0x0;
		return (c === "x" ? r : (r & 0x3 | 0x8)).toString(16);
	}).toUpperCase()
}
```

- [Crypto.randomUUID() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Crypto/randomUUID)
- [uuidjs/uuid: Generate RFC-compliant UUIDs in JavaScript](https://github.com/uuidjs/uuid)
- [Universally unique identifier - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Universally_unique_identifier)

## Random identifier

```js
Math.round(Math.random() * Number.MAX_SAFE_INTEGER).toString(36)// > "5lv1liy34k"
```

## Rounding numbers

Use bitwise operators for rounding, which convert numbers to a 32-bit sequence.

These alternatives will only work with positive signed 32-bit floats, i.e. numbers from 0 to +2,147,483,647 (2^31-1).

```js
2147483647.1|0; // 2147483647
2147483648.1|0; // -2147483648
```

```js
Math.round(n) === n + (n < 0 ? -0.5 : 0.5) >> 0;
Math.ceil(n) === n + (n < 0 ? 0 : 1) >> 0;
Math.floor(n) === n + (n < 0 ? -1 : 0) >> 0;
```

- [Rounding — Wikipedia](https://en.wikipedia.org/wiki/Rounding)
- [arithmetic - Rules for rounding (positive and negative numbers) - Mathematics Stack Exchange](http://math.stackexchange.com/questions/3448/rules-for-rounding-positive-and-negative-numbers/60690#60690)
- [Rounding Methods](https://www.mathsisfun.com/numbers/rounding-methods.html)

`Math.rint()`: rounds to an even integer

### Round towards zero

```js
3.14// 3
-3.14// -3
```

- Simple expression: `n > 0 ? Math.floor(n) : Math.ceil(n)`
- Bitwise OR with 0 + Math.floor and ceil for high values: `n >= 0 && n < 2 ^ 31 ? n|0 : n >= 0 ? Math.floor(n) : Math.ceil(n)`. See [Micro optimization are useless](#micro-optimization-are-useless)
- Real full expression: `typeof n === 'number' && !isNaN(n) && n !== Infinity ? n > 0 ? Math.floor(n) : Math.ceil(n) : 0`

Work only for 32bits signed floats :

- Double bitwise NOT: `~~n; // 3`
- Bitwise OR: `n | n; // 3`
- Bitwise OR with 0: `n | 0; // 3`
- Bitwise AND: `n & n; // 3`
- Bitwise left shift: `n << 0; // 3`
- Bitwise right shift: `n >> 0;` works also with negative numbers and ceil()'s them...

But not:

- Unsigned right shift: `n >>> 0;`

- http://jsperf.com/rounding-numbers-down
- [Double bitwise NOT (~~) – James Padolsey](http://james.padolsey.com/cool-stuff/double-bitwise-not/)
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#%28Bitwise_NOT%29

### Round away from zero

```js
3.14// 4
-3.14// -4
```

- Simple expression: `n > 0 ? Math.ceil(n) : Math.floor(n)`
- Real full expression: `typeof n === 'number' && !isNaN(n) && n !== Infinity ? n > 0 ? Math.ceil(n) : Math.floor(n) : 0`

### Round 1/2 away from zero

```js
1.5// 2
-1.5// -2
```

```js
value > 0 ? Math.round(value) : -Math.round(-value)
```

### Round precision

```js
function round(value, precision = 32){
	const exponent = Math.pow(10, precision);
	return Math.round(value * exponent) / exponent;
}

round(123.45, 1);// => 123.5
round(123.5, 0);// => 124
round(125, -1);// => 130
```

- [Math.trunc() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/trunc)
- [Math.ceil() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/ceil#Decimal_adjustment)
- [Number.EPSILON - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/EPSILON)

### Round to multiple

```js
function round(num, multiple){
	return Math.round(num / multiple) * multiple;
}

round(11, 5)// => 10
```

## To N decimals

```js
/**
* @param decimals Number of decimals. Can be negative
* @return string
*/
function toFixed(value, decimals = 0){
	if(isNaN(Number(decimals))){
		decimals = 0;
	}
	if(decimals < 0){
		value = Math.round(value * Math.pow(10, decimals));
	}
	return value.toFixed(Math.max(0, decimals));
}
```

Specificities: `(1000000000000000000000).toFixed(3) == "1e+21"` and `35.855*100 == 3585.4999999999995`

See [Floating point numbers](#floating-point-numbers)

- [Snippet: Rounding with Precision](http://yourjs.com/snippets/33)

## Remove item without changing original array

Aka [pure function](https://en.wikipedia.org/wiki/Pure_function)

```js
const removeAt = (array, index) => array.filter((_, i) => i !== index );
```

## Pseudo Random Number Generator

Aka PRNG

```js
// From http://codepen.io/quasimondo/pen/ogxJrZ
class PRNG{
    constructor(seed = 1){
        this.seed = seed;
    }
    next() { return (this.gen() / 2147483647); }
    nextRange(min, max)	{ return min + ((max - min) * this.next()) }
    gen() { return this.seed = (this.seed * 16807) % 2147483647; }
}

const rng = new PRNG(12275);

const order = [];
for ( var i = 0; i < 11; i++)
{
	order.splice((rng.next()*(order.length+1))|0,0,i);
}
```

Using `Array.prototype.sort()` depends browser's sort algorithm: http://codepen.io/quasimondo/pen/PwNXXQ

- [nquinlan/better-random-numbers-for-javascript-mirror: A direct mirror of Johannes Baagøe's wiki on implementations of Randomness in Javascript.](https://github.com/nquinlan/better-random-numbers-for-javascript-mirror)
- [TIFU by using Math.random() — Medium](https://medium.com/@betable/tifu-by-using-math-random-f1c308c4fd9d)
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/random

## Find range

```js
let testValue = 150;
let ranges = [0, 100, 200, 300];// contains minimal values. ranges: [0, 100) [100, 200) [200, 300) [300, +Infinity)
let foundRangeIndex = (value, finalIndex, rangeMinValue, rangeIndex) => value < rangeMinValue ? finalIndex : rangeIndex;
// Should in range 0, 1, 2 or 3. For 150 will get index 1
// If below the first range, will get index 0
let rangeIndex = ranges.reduce(foundRangeIndex.bind(this, testValue), 0);
```

## HSL

```js
// HSL (1978) = H: Hue / S: Saturation / L: Lightness
HSL_RGB = function (o) { // { H: 0-360, S: 0-100, L: 0-100 }
  var H = o.H / 360,
      S = o.S / 100,
      L = o.L / 100,
      R, G, B, _1, _2;

  function Hue_2_RGB(v1, v2, vH) {
    if (vH < 0) vH += 1;
    if (vH > 1) vH -= 1;
    if ((6 * vH) < 1) return v1 + (v2 - v1) * 6 * vH;
    if ((2 * vH) < 1) return v2;
    if ((3 * vH) < 2) return v1 + (v2 - v1) * ((2 / 3) - vH) * 6;
    return v1;
  }

  if (S == 0) { // HSL from 0 to 1
    R = L * 255;
    G = L * 255;
    B = L * 255;
  } else {
    if (L < 0.5) {
      _2 = L * (1 + S);
    } else {
      _2 = (L + S) - (S * L);
    }
    _1 = 2 * L - _2;

    R = 255 * Hue_2_RGB(_1, _2, H + (1 / 3));
    G = 255 * Hue_2_RGB(_1, _2, H);
    B = 255 * Hue_2_RGB(_1, _2, H - (1 / 3));
  }

  return {
    R: R,
    G: G,
    B: B
  };
};
```

## Simple hash

Stringify you data. Easy, but use lot of memory.

```js
let objHash = Object.keys(obj).sort().map(key => key+":"+obj[key]).join("\0");
let objHash = JSON.stringify(obj);// not work because properties could have different order. See https://stackoverflow.com/questions/16167581/sort-object-properties-and-json-stringify/35810961#35810961
```

- [Hash function — Wikipedia](https://en.wikipedia.org/wiki/Hash_function)
- [List of hash functions — Wikipedia](https://en.wikipedia.org/wiki/List_of_hash_functions)
- [c - Simple hash functions - Stack Overflow](https://stackoverflow.com/questions/14409466/simple-hash-functions/14409947#14409947)

```js
function crc32 (str) {

	function Utf8Encode(string) {
		string = string.replace(/\r\n/g,"\n");
		var utftext = "";

		for (var n = 0; n < string.length; n++) {

			var c = string.charCodeAt(n);

			if (c < 128) {
				utftext += String.fromCharCode(c);
			}
			else if((c > 127) && (c < 2048)) {
				utftext += String.fromCharCode((c >> 6) | 192);
				utftext += String.fromCharCode((c & 63) | 128);
			}
			else {
				utftext += String.fromCharCode((c >> 12) | 224);
				utftext += String.fromCharCode(((c >> 6) & 63) | 128);
				utftext += String.fromCharCode((c & 63) | 128);
			}

		}

		return utftext;
	};

	str = Utf8Encode(str);

	var table = new Uint32Array([0x00000000, 0x77073096, 0xEE0E612C, 0x990951BA, 0x076DC419, 0x706AF48F, 0xE963A535, 0x9E6495A3, 0x0EDB8832, 0x79DCB8A4, 0xE0D5E91E, 0x97D2D988, 0x09B64C2B, 0x7EB17CBD, 0xE7B82D07, 0x90BF1D91, 0x1DB71064, 0x6AB020F2, 0xF3B97148, 0x84BE41DE, 0x1ADAD47D, 0x6DDDE4EB, 0xF4D4B551, 0x83D385C7, 0x136C9856, 0x646BA8C0, 0xFD62F97A, 0x8A65C9EC, 0x14015C4F, 0x63066CD9, 0xFA0F3D63, 0x8D080DF5, 0x3B6E20C8, 0x4C69105E, 0xD56041E4, 0xA2677172, 0x3C03E4D1, 0x4B04D447, 0xD20D85FD, 0xA50AB56B, 0x35B5A8FA, 0x42B2986C, 0xDBBBC9D6, 0xACBCF940, 0x32D86CE3, 0x45DF5C75, 0xDCD60DCF, 0xABD13D59, 0x26D930AC, 0x51DE003A, 0xC8D75180, 0xBFD06116, 0x21B4F4B5, 0x56B3C423, 0xCFBA9599, 0xB8BDA50F, 0x2802B89E, 0x5F058808, 0xC60CD9B2, 0xB10BE924, 0x2F6F7C87, 0x58684C11, 0xC1611DAB, 0xB6662D3D, 0x76DC4190, 0x01DB7106, 0x98D220BC, 0xEFD5102A, 0x71B18589, 0x06B6B51F, 0x9FBFE4A5, 0xE8B8D433, 0x7807C9A2, 0x0F00F934, 0x9609A88E, 0xE10E9818, 0x7F6A0DBB, 0x086D3D2D, 0x91646C97, 0xE6635C01, 0x6B6B51F4, 0x1C6C6162, 0x856530D8, 0xF262004E, 0x6C0695ED, 0x1B01A57B, 0x8208F4C1, 0xF50FC457, 0x65B0D9C6, 0x12B7E950, 0x8BBEB8EA, 0xFCB9887C, 0x62DD1DDF, 0x15DA2D49, 0x8CD37CF3, 0xFBD44C65, 0x4DB26158, 0x3AB551CE, 0xA3BC0074, 0xD4BB30E2, 0x4ADFA541, 0x3DD895D7, 0xA4D1C46D, 0xD3D6F4FB, 0x4369E96A, 0x346ED9FC, 0xAD678846, 0xDA60B8D0, 0x44042D73, 0x33031DE5, 0xAA0A4C5F, 0xDD0D7CC9, 0x5005713C, 0x270241AA, 0xBE0B1010, 0xC90C2086, 0x5768B525, 0x206F85B3, 0xB966D409, 0xCE61E49F, 0x5EDEF90E, 0x29D9C998, 0xB0D09822, 0xC7D7A8B4, 0x59B33D17, 0x2EB40D81, 0xB7BD5C3B, 0xC0BA6CAD, 0xEDB88320, 0x9ABFB3B6, 0x03B6E20C, 0x74B1D29A, 0xEAD54739, 0x9DD277AF, 0x04DB2615, 0x73DC1683, 0xE3630B12, 0x94643B84, 0x0D6D6A3E, 0x7A6A5AA8, 0xE40ECF0B, 0x9309FF9D, 0x0A00AE27, 0x7D079EB1, 0xF00F9344, 0x8708A3D2, 0x1E01F268, 0x6906C2FE, 0xF762575D, 0x806567CB, 0x196C3671, 0x6E6B06E7, 0xFED41B76, 0x89D32BE0, 0x10DA7A5A, 0x67DD4ACC, 0xF9B9DF6F, 0x8EBEEFF9, 0x17B7BE43, 0x60B08ED5, 0xD6D6A3E8, 0xA1D1937E, 0x38D8C2C4, 0x4FDFF252, 0xD1BB67F1, 0xA6BC5767, 0x3FB506DD, 0x48B2364B, 0xD80D2BDA, 0xAF0A1B4C, 0x36034AF6, 0x41047A60, 0xDF60EFC3, 0xA867DF55, 0x316E8EEF, 0x4669BE79, 0xCB61B38C, 0xBC66831A, 0x256FD2A0, 0x5268E236, 0xCC0C7795, 0xBB0B4703, 0x220216B9, 0x5505262F, 0xC5BA3BBE, 0xB2BD0B28, 0x2BB45A92, 0x5CB36A04, 0xC2D7FFA7, 0xB5D0CF31, 0x2CD99E8B, 0x5BDEAE1D, 0x9B64C2B0, 0xEC63F226, 0x756AA39C, 0x026D930A, 0x9C0906A9, 0xEB0E363F, 0x72076785, 0x05005713, 0x95BF4A82, 0xE2B87A14, 0x7BB12BAE, 0x0CB61B38, 0x92D28E9B, 0xE5D5BE0D, 0x7CDCEFB7, 0x0BDBDF21, 0x86D3D2D4, 0xF1D4E242, 0x68DDB3F8, 0x1FDA836E, 0x81BE16CD, 0xF6B9265B, 0x6FB077E1, 0x18B74777, 0x88085AE6, 0xFF0F6A70, 0x66063BCA, 0x11010B5C, 0x8F659EFF, 0xF862AE69, 0x616BFFD3, 0x166CCF45, 0xA00AE278, 0xD70DD2EE, 0x4E048354, 0x3903B3C2, 0xA7672661, 0xD06016F7, 0x4969474D, 0x3E6E77DB, 0xAED16A4A, 0xD9D65ADC, 0x40DF0B66, 0x37D83BF0, 0xA9BCAE53, 0xDEBB9EC5, 0x47B2CF7F, 0x30B5FFE9, 0xBDBDF21C, 0xCABAC28A, 0x53B39330, 0x24B4A3A6, 0xBAD03605, 0xCDD70693, 0x54DE5729, 0x23D967BF, 0xB3667A2E, 0xC4614AB8, 0x5D681B02, 0x2A6F2B94, 0xB40BBE37, 0xC30C8EA1, 0x5A05DF1B, 0x2D02EF8D]);

	var crc = 0;
	var x = 0;
	var y = 0;

	crc = crc ^ (-1);
	for( var i = 0, iTop = str.length; i < iTop; i++ ) {
		y = ( crc ^ str.charCodeAt( i ) ) & 0xFF;
		x = table[y];
		crc = ( crc >>> 8 ) ^ x;
	}

	return crc ^ (-1);

}
```

## Hypotenuse

The square root of `x*x+y*y`

```js
let hypot = (x, y) => Math.sqrt(Math.pow(x, 2) + Math.pow(y, 2));
```

```js
// sqrt(a^2 + b^2) without under/overflow
function hypot(a, b) {
	if (Math.abs(a) > Math.abs(b)) {
		let r = b / a;
		return Math.abs(a) * Math.sqrt(1 + r * r);
	}

	if (b != 0) {
		let r = a / b;
		return Math.abs(b) * Math.sqrt(1 + r * r);
	}

	return 0;
}
```

## Required parameters

```js
const undefinedParameter = name => { throw new Error(`The parameter "${name}" is undefined.`); };
const hello = (name = undefinedParameter("name")) => { console.log(`hello ${name}`) };
// This will throw an error because no name is provided
hello();
```

## Compare two arrays

```js
array1.length == array2.length && array1.every(item => array2.includes(item));// will check if both arrays have the same length and contains the same elements (duplicated elements is possible)
array1.length == array2.length && array1.every((item, index) => item === array2[index]);// will check if both arrays have the same length and the order
```

- [How to compare arrays in JavaScript? - Stack Overflow](https://stackoverflow.com/questions/7837456/how-to-compare-arrays-in-javascript)

## Template literals

```js
function getFullString(strings, ...interpolatedValues) { // `...` essentially slices the arguments for us.
	return strings.reduce((total, current, index) => { // use an arrow function for brevity here
		total += current;
		if (interpolatedValues.hasOwnProperty(index)) {
			total += interpolatedValues[index];
		}
		return total;
	}, "");
}
```

`let b = getFullString``a ${a}``;` is the same thing as `let b = ``a = ${a}``;`

**Do not `s.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/'/g, "&#39;").replace(/"/g, "&quot;")`** to escape HTML

```js
function template(strings, ...interpolatedValues) {
	return strings.reduce((total, current, index) => {
		total += current;
		if (interpolatedValues.hasOwnProperty(index)) {
			total += String(interpolatedValues[index]);
		}
		return total;
	}, "");
}
var helpers = {
	if: (condition, thenTemplate, elseTemplate = "") => {
		return condition ? thenTemplate : elseTemplate;
	},
	unless: (condition, thenTemplate, elseTemplate) => {
		return !condition ? thenTemplate : elseTemplate;
	},
	registerHelper(name, fn) => {
		helpers[name] = fn;
	}
};
helpers.registerHelper("capitalize", (string) => {
	return string[0].toUpperCase() + string.slice(1).toUpperCase();
});
var page = ({ people, isAdmin }) => template`
	<h2>People</h2>
	<ul>
	${people.map(person => `
		<li>
			<span>${helpers.capitalize(person)}</span>
			${helpers.if(isAdmin,
				`<button>Delete ${helpers.capitalize(person)}</button>`
			)}
		</li>
	`)}
	</ul>
`;

page({ isAdmin: true, people: ['Keith', 'Dave', 'Amy' ] });
```

## Regex

### Dot match all chars

Aka dotall, dot doesn't match new line char

```js
"foo\nbar".match(/.*/)// ["foo"]
"foo\nbar".match(/.*/s)// ["foo\nbar"]
"foo\nbar".match(/[^]*/)// ["foo\nbar"]
// match all chars range could be: [^] (aka "match any character that is not nothing"), [\s\S], [\w\W], [\d\D]
```

- [javascript - how to use dotall flag for regex.exec() - Stack Overflow](https://stackoverflow.com/questions/23455614/how-to-use-dotall-flag-for-regex-exec/36006948#36006948)
- [RegExp.prototype.dotAll - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/dotAll#browser_compatibility)

## Never loop with float

**Don't (infinite loop):**

```js
for(let i = 0; i == 1; i+= 0.005){
	console.log(i);
}
```

```js
for(let i = 0; i < 1; i+= 0.005){
	console.log(i);
}
// Last i === 1.0000000000000007
```

Use:

```js
for(let i = 0; i < 200; i++){
	console.log(i * 0.005);
}
```

## Divide array items

Add array items separator / dividers.

As string:

```js
let sep = "-";
["a", "b", "c"].join(sep);
```

```js
let sep = "-";
["a", "b", "c"].reduce((result, item, index) => (index == 0 ? result.push(item) : result.push(sep, item), result), []);
```

With pre allocation:

```js
let sep = "-";
let arr = ["a", "b", "c"];
arr.reduce((result, item, index) => (result[index * 2] = sep, result[Math.min(index, 1) + index * 2] = item, result), new Array(Math.max(arr.length * 2 - 1, 0)));
```

Natural inline list (eg.: "1, 2 and 3")

```js
arr.reduce((result, item, index, items) => (index == 0 ? result.push(item) : result.push(index >= items.length - 1 ? " and " : ", ", item), result), []);
```

## To integer

```js
// From https://github.com/kangax/sputniktests-webrunner/blob/master/src/lib/numeric_conversion.js
function toInteger(p) {
	var x = Number(p);

	if(isNaN(x)){
		return +0;
	}

	if((x === +0)
	|| (x === -0)
	|| (x === Number.POSITIVE_INFINITY)
	|| (x === Number.NEGATIVE_INFINITY)){
		return x;
	}

	var sign = ( x < 0 ) ? -1 : 1;

	return sign * Math.floor(Math.abs(x));
}
```

## Number equals

Doesn't work with NaN

```js
// From https://github.com/kangax/sputniktests-webrunner/blob/master/src/lib/math_precision.js
function getPrecision(num)
{
	var log2num = Math.log(Math.abs(num)) / Math.LN2;
	var pernum = Math.ceil(log2num);
	return 2 * Math.pow(2, -52 + pernum);
}

function isEqual(num1, num2)
{
	if (num1 === Infinity) && num2 === Infinity)
	{
		return true;
	}
	if (num1 === -Infinity && num2 === -Infinity)
	{
		return true;
	}
	var prec = getPrecision(Math.min(Math.abs(num1), Math.abs(num2)));
	return Math.abs(num1 - num2) <= prec;
}
```

## Date

`Date.toJSON()` is an alias of `Date.toISOstring()`, see [javascript - Difference between Date.toJSON() and Date.toISOstring() - Stack Overflow](https://stackoverflow.com/questions/16198506/difference-between-date-tojson-and-date-toisostring)

```js
// https://github.com/kangax/sputniktests-webrunner/blob/master/src/lib/Date_constants.js
var hoursPerDay = 24;
var minutesPerHour = 60;
var secondsPerMinute = 60;

var msPerDay = 86400000;
var msPerSecond = 1000;
var msPerMinute = 60000;
var msPerHour = 3600000;

var date_1899_end = -2208988800001;
var date_1900_start = -2208988800000;
var date_1969_end = -1;
var date_1970_start = 0;
var date_1999_end = 946684799999;
var date_2000_start = 946684800000;
var date_2099_end = 4102444799999;
var date_2100_start = 4102444800000;

// https://github.com/kangax/sputniktests-webrunner/blob/master/src/lib/Date_library.js
//15.9.1.2 Day Number and Time within day
function day(t) {
	return Math.floor(t/msPerDay);
}

function timeWithinDay(t) {
	return t%msPerDay;
}

//15.9.1.3 year Number
function daysInYear(y){
	if(y%4 != 0) return 365;
	if(y%4 == 0 && y%100 != 0) return 366;
	if(y%100 == 0 && y%400 != 0) return 365;
	if(y%400 == 0) return 366;
}

function dayFromYear(y) {
	return (365*(y-1970)
					+ Math.floor((y-1969)/4)
					- Math.floor((y-1901)/100)
					+ Math.floor((y-1601)/400));
}

function timeFromYear(y){
	return msPerDay*DayFromYear(y);
}

function yearFromTime(t) {
	t = Number(t);
	var sign = ( t < 0 ) ? -1 : 1;
	var year = ( sign < 0 ) ? 1969 : 1970;

	for(var time = 0;;year += sign){
		time = timeFromYear(year);

		if(sign > 0 && time > t){
			year -= sign;
			break;
		}
		else if(sign < 0 && time <= t){
			break;
		}
	};
	return year;
}

function inLeapYear(t){
	if(DaysInYear(YearFromTime(t)) == 365)
		return 0;

	if(DaysInYear(YearFromTime(t)) == 366)
		return 1;
}

function dayWithinYear(t) {
	return day(t)-DayFromYear(YearFromTime(t));
}

//15.9.1.4 Month Number
function monthFromTime(t){
	var day = dayWithinYear(t);
	var leap = inLeapYear(t);

	if((0 <= day) && (day < 31)) return 0;
	if((31 <= day) && (day < (59+leap))) return 1;
	if(((59+leap) <= day) && (day < (90+leap))) return 2;
	if(((90+leap) <= day) && (day < (120+leap))) return 3;
	if(((120+leap) <= day) && (day < (151+leap))) return 4;
	if(((151+leap) <= day) && (day < (181+leap))) return 5;
	if(((181+leap) <= day) && (day < (212+leap))) return 6;
	if(((212+leap) <= day) && (day < (243+leap))) return 7;
	if(((243+leap) <= day) && (day < (273+leap))) return 8;
	if(((273+leap) <= day) && (day < (304+leap))) return 9;
	if(((304+leap) <= day) && (day < (334+leap))) return 10;
	if(((334+leap) <= day) && (day < (365+leap))) return 11;
}

//15.9.1.5 Date Number
function dateFromTime(t) {
	var day = dayWithinYear(t);
	var month = monthFromTime(t);
	var leap = inLeapYear(t);

	if(month == 0) return day+1;
	if(month == 1) return day-30;
	if(month == 2) return day-58-leap;
	if(month == 3) return day-89-leap;
	if(month == 4) return day-119-leap;
	if(month == 5) return day-150-leap;
	if(month == 6) return day-180-leap;
	if(month == 7) return day-211-leap;
	if(month == 8) return day-242-leap;
	if(month == 9) return day-272-leap;
	if(month == 10) return day-303-leap;
	if(month == 11) return day-333-leap;
}

//15.9.1.6 Week day
function weekDay(t) {
	var weekday = (Day(t)+4)%7;
	return (weekday < 0 ? 7+weekday : weekday);
}

//15.9.1.9 Daylight Saving time Adjustment
var localTZA = $LocalTZ*msPerHour;

function DaysInMonth(m, leap) {
	m = m%12;

	//April, June, Sept, Nov
	if(m == 3 || m == 5 || m == 8 || m == 10 ) {
		return 30;
	}

	//Jan, March, May, July, Aug, Oct, Dec
	if(m == 0 || m == 2 || m == 4 || m == 6 || m == 7 || m == 9 || m == 11){
		return 31;
	}

	//Feb
	return 28+leap;
}

function getSundayInMonth(t, m, count){
	var year = yearFromTime(t);
	var leap = inLeapYear(t);
	var day = 0;

	if(m >= 1) day += daysInMonth(0, leap);
	if(m >= 2) day += daysInMonth(1, leap);
	if(m >= 3) day += daysInMonth(2, leap);
	if(m >= 4) day += daysInMonth(3, leap);
	if(m >= 5) day += daysInMonth(4, leap);
	if(m >= 6) day += daysInMonth(5, leap);
	if(m >= 7) day += daysInMonth(6, leap);
	if(m >= 8) day += daysInMonth(7, leap);
	if(m >= 9) day += daysInMonth(8, leap);
	if(m >= 10) day += daysInMonth(9, leap);
	if(m >= 11) day += daysInMonth(10, leap);

	var month_start = timeFromYear(year)+day*msPerDay;
	var sunday = 0;

	if(count === "last"){
		for(var last_sunday = month_start+DaysInMonth(m, leap)*msPerDay;
			WeekDay(last_sunday)>0;
			last_sunday -= msPerDay
		){};
		sunday = last_sunday;
	}
	else {
		for(var first_sunday = month_start;
			WeekDay(first_sunday)>0;
			first_sunday += msPerDay
		){};
		sunday = first_sunday+7*msPerDay*(count-1);
	}

	return sunday;
}

function daylightSavingTA(t) {
	t = t-localTZA;

	var DST_start = getSundayInMonth(t, $DST_start_month, $DST_start_sunday)
									+$DST_start_hour*msPerHour
									+$DST_start_minutes*msPerMinute;

	var k = new date(DST_start);

	var DST_end	 = getSundayInMonth(t, $DST_end_month, $DST_end_sunday)
									+$DST_end_hour*msPerHour
									+$DST_end_minutes*msPerMinute;

	if ( t >= DST_start && t < DST_end ) {
		return msPerHour;
	} else {
		return 0;
	}
}

//15.9.1.9 Local time
function localTime(t){
	return t+localTZA+daylightSavingTA(t);
}

function utc(t) {
	return t-localTZA-daylightSavingTA(t-localTZA);
}

//15.9.1.10 Hours, Minutes, Second, and Milliseconds
function hourFromTime(t){
	return Math.floor(t/msPerHour)%hoursPerDay;
}

function minFromTime(t){
	return Math.floor(t/msPerMinute)%minutesPerHour;
}

function secFromTime(t){
	return Math.floor(t/msPerSecond)%secondsPerMinute;
}

function msFromTime(t){
	return t%msPerSecond;
}

//15.9.1.11 makeTime (hour, min, sec, ms)
function makeTime(hour, min, sec, ms){
	if ( !isFinite(hour) || !isFinite(min) || !isFinite(sec) || !isFinite(ms)) {
		return Number.NaN;
	}

	hour = toInteger(hour);
	min	= toInteger(min);
	sec	= toInteger(sec);
	ms	 = toInteger(ms);

	return ((hour*msPerHour) + (min*msPerMinute) + (sec*msPerSecond) + ms);
}

//15.9.1.12 MakeDay (year, month, date)
function makeDay(year, month, date) {
	if ( !isFinite(year) || !isFinite(month) || !isFinite(date)) {
		return Number.NaN;
	}

	year = toInteger(year);
	month = toInteger(month);
	date = toInteger(date );

	var result5 = year + Math.floor(month/12);
	var result6 = month%12;

	var sign = ( year < 1970 ) ? -1 : 1;
	var t =		( year < 1970 ) ? 1 :	0;
	var y =		( year < 1970 ) ? 1969 : 1970;

	if( sign == -1 ){
		for ( y = 1969; y >= year; y += sign ) {
			t += sign * daysInYear(y)*msPerDay;
		}
	} else {
		for ( y = 1970 ; y < year; y += sign ) {
			t += sign * daysInYear(y)*msPerDay;
		}
	}

	var leap = 0;
	for ( var m = 0; m < month; m++ ) {
		//if year is changed, than we need to recalculate leep
		leap = inLeapYear(t);
		t += daysInMonth(m, leap)*msPerDay;
	}

	if ( yearFromTime(t) != result5 ) {
		return Number.NaN;
	}
	if ( monthFromTime(t) != result6 ) {
		return Number.NaN;
	}
	if ( dateFromTime(t) != 1 ) {
		return Number.NaN;
	}

	return day(t)+date-1;
}

//15.9.1.13 MakeDate (day, time)
function makeDate( day, time ) {
	if(!isFinite(day) || !isFinite(time)) {
		return Number.NaN;
	}

	return day*msPerDay+time;
}

//15.9.1.14 TimeClip (time)
function timeClip(time) {
	if(!isFinite(time) || Math.abs(time) > 8.64e15){
		return Number.NaN;
	}

	return toInteger(time);
}
```

## Pretty date

```js
/*
 * JavaScript Pretty Date
 * Copyright (c) 2008 John Resig (jquery.com)
 * Licensed under the MIT license.
 */

/**
 * Takes an date and returns a string representing how long ago the date represents
 * @param {Date} date
 */
function prettyDate(date) {
	const diff = (Date.now() - date.getTime()) / 1000;
	const dayDiff = Math.floor(diff / 86400);

	if (isNaN(dayDiff) || dayDiff < 0 || dayDiff >= 31) return "";

	if (dayDiff === 0) {
		if (diff < 60) return "just now";
		if (diff < 120) return "1 minute ago";
		if (diff < 3600) return Math.floor(diff / 60) + " minutes ago";
		if (diff < 7200) return "1 hour ago";
		return Math.floor(diff / 3600) + " hours ago";
	}

	if (dayDiff === 1) return "Yesterday";
	if (dayDiff < 7) return dayDiff + " days ago";
	return Math.ceil(dayDiff / 7) + " weeks ago";
}
```
```js
const rtf = new Intl.RelativeTimeFormat("en", { numeric: "auto" });
console.log(rtf.format(-2, "day"));
```

- [Intl.RelativeTimeFormat - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/RelativeTimeFormat)

## Format date

```js
// https://docs.microsoft.com/en-us/dotnet/standard/base-types/custom-date-and-time-format-strings
// https://docs.microsoft.com/en-us/dotnet/standard/base-types/custom-timespan-format-strings
// https://source.dot.net/#System.Private.CoreLib/DateTimeFormat.cs,2fd25af5cf3e592e
// https://source.dot.net/#System.Private.CoreLib/TimeSpanFormat.cs,f2ad6faffa42da52
function format(date, format){
	return format.replace(/\\.|".+?"|'.+?'|%[dHM]|[dHM]+/g, function(match){
		switch(match.charAt(0)){
			// Escaped char
			case "\\": return match.charAt(1);
			// Literal string
			case '"':
			case "'": return match.substr(1, match.length - 2);
			// Single Custom Format Specifiers.
			case "%": match = match.substr(1); break;
			// fix length of custom format specifiers:
			case "H": match = match.substring(0, 2); break;
			case "d":
			case "M": match = match.substring(0, 4); break;
		}

		switch(match){
			case "dd": return String(date.getDate()).padStart(2, "0");
			case "HH": return String(date.getHours()).padStart(2, "0");
			case "MM": return String(date.getMonth() + 1).padStart(2, "0");
		}
		return "";// others, not implemented
	});
}

format(new Date(), "dd/MM");
format(new Date(), "HH\\h");
```

## Create range array

```js
const range = (from, to) => Array.from({length: to - from + 1}, (x, i) => from + i);
```

## Beautify

From minified source code

```
!0												true
!1												false
a && b											if(a){b}
(a, b, c)										a; b; c;
a && (b, c)										if(a){b; c;}
return void a()									a(); return;
a ? b() : (c(), d())							if(a){b()}else{c(); d();}
return a(), b									a(); return b;
if(a(), b){c()}									a(); if(b){c();}
1 == a ? b() : 2 == a ? c() : 3 == a && d()		switch(a){case 1: b(); break; case 2: c(); break; case 3: d(); break;}
for (; 0 > a;) b()								while(a < 0){ b() }
```

- [mishoo/UglifyJS: JavaScript parser / mangler / compressor / beautifier toolkit](https://github.com/mishoo/UglifyJS)
- [eth-sri/UnuglifyJS: A simpler open-source version of JavaScript deobfuscator JSNice](https://github.com/eth-sri/UnuglifyJS)

## Reduce by common divisor

Usefull for simplify aspect ratios.

```js
/**
 * Find the greatest common divisor using a recursive function
 * @see http://en.wikipedia.org/wiki/Greatest_common_divisor
 * @param a numerator
 * @param b denominator
 * @return common divisor (always positive)
 */
function findGCD(a, b){
	var t;
	a = Number(a);
	b = Number(b);
	// Not valid type (not a number)
	if (isNaN(a) || isNaN(b)){
		return NaN;
	}
	// Infinity
	if(!isFinite(a) || !isFinite(b)){
		return Number.POSITIVE_INFINITY;
	}
	// division-based version
	while(b !== 0){
		t = b;
		b = a % b;
		a = t;
	}

	// Common divisor is always a positive number
	return Math.abs(a);
}

/**
 * Reduce a numerator and denominator to it's smallest, ratio using Euclid's Algorithm
 */
function reduceRatio(numerator, denominator) {
	var numerator = Number(numerator);
	var denominator = Number(denominator);
	var divisor = findGCD(numerator, denominator);

	// Infinity
	if(!isFinite(numerator)){
		return [numerator, 1];
	}
	if(!isFinite(denominator)){
		return [1, denominator];
	}

	return [numerator / divisor, denominator / divisor];
}
```

- [Greatest common divisor — Wikipedia](https://en.wikipedia.org/wiki/Greatest_common_divisor)
- [Euclidean algorithm — Wikipedia](https://en.wikipedia.org/wiki/Euclidean_algorithm)
- [Aspect ratio — Wikipedia](https://en.wikipedia.org/wiki/Aspect_ratio)
- [Aspect ratio (image) — Wikipedia](https://en.wikipedia.org/wiki/Aspect_ratio_%28image%29)

## Normalize number

Angle between 0° and 360°

```js
angle = (angle % 360 + 360) % 360;
```

Angle between -180° and 180°

```js
angle = (angle % 360 + 540) % 360 - 180;
```

normalize an angle between -π and +π (https://stackoverflow.com/questions/24234609/standard-way-to-normalize-an-angle-to-%CF%80-radians-in-java)

```js
theta - TWO_PI * Math.floor((theta + Math.PI) / TWO_PI)
```

Angle between -179° and 180°

```js
angle = ((angle + 179) % 360 + 360) % 360 - 179;
```

Infinite index

```js
var values:Array = ["a", "b", "c"];
var index:int = -5;
var length:uint = values.length;
var realIndex:uint = (index % length + length) % length;// = 0, 1 or 2
values[realIndex];//= "b"
```

## Resize

- https://developer.mozilla.org/en-US/docs/Web/CSS/background-size
- https://developer.mozilla.org/en-US/docs/Web/CSS/object-fit
- https://developer.mozilla.org/en-US/docs/Web/CSS/object-position
- https://www.w3.org/TR/css3-images/img_scale.png

```js
const sourceWidth;
const sourceHeight;
const targetWidth;
const targetHeight;
```

### None fit

```js
const width = sourceWidth;
const height = sourceHeight;
```

### Contain fit

Also called letterbox (for movie on a screen)

Uniformly scales (homotheticaly) up content as much as possible, while still showing all content on the target.

```js
const sourceRatio = sourceWidth / sourceHeight;
const targetRatio = targetWidth / targetHeight;
const width = Math.min(sourceRatio, targetRatio) * targetHeight;
const height = targetWidth / Math.max(sourceRatio, targetRatio);
```

```js
const scale = Math.min(targetWidth / sourceWidth, targetHeight / sourceHeight);
```

### Fit height homotheticaly

```js
const sourceRatio = sourceWidth / sourceHeight;
const width = sourceRatio * targetHeight;
const height = targetHeight;
```

### Scale-down fit

with original max size homotheticaly

```js
const altTargetWidth = Math.min(targetWidth, sourceWidth);
const altTargetHeight = Math.min(targetHeight, sourceHeight);
const sourceRatio = sourceWidth / sourceHeight;
const altTargetRatio = altTargetWidth / altTargetHeight;
const width = Math.min(sourceRatio, altTargetRatio) * altTargetHeight;
const height = altTargetWidth / Math.max(sourceRatio, altTargetRatio);
```

### Cover fit

Crop to fit (zoom even) homotheticaly

Uniformly scales up content to fill the screen, while preserving aspect ratio. Some content may appear offscreen, if the new screen has a different aspect ratio.

```js
const sourceRatio = sourceWidth / sourceHeight;
const targetRatio = targetWidth / targetHeight;
const width = Math.max(sourceRatio, targetRatio) * targetHeight;
const height = targetWidth / Math.min(sourceRatio, targetRatio);
```

### Fill fit

Scale (zoom stretch)

Non-uniformly scales up content to fill the screen. All content will remain onscreen, but it may be stretched vertically or horizontally. It can distort display objects on devices (e.g., circles become ovals).

```js
const width = targetHeight;
const height = targetWidth;
```

### Complex case

Merge multiple modes

```js
const sourceRatio = sourceWidth / sourceHeight;
// First define a internal target to fit all
// portrait use 8:9 as minimal ratio
const altTargetRatio = Math.max(sourceRatio, 8 / 9);
const altTargetWidth = Math.min(sourceRatio, altTargetRatio) * sourceHeight;
const altTargetHeight = sourceWidth / Math.max(sourceRatio, altTargetRatio);
// Then define a final window to cover the target window
const targetRatio = targetWidth / targetHeight;
const width = Math.max(targetRatio, altTargetRatio) * targetHeight;
const height = targetWidth / Math.min(targetRatio, altTargetRatio);
// Center
const x = (altTargetWidth - width) / 2;
const y = (altTargetHeight - height) / 2;
```

## Can play through

Aka Estimate time needed for start playing media

Works better with CBR (Constant bitrate) media

See HTML Media [`canplaythrough`](https://developer.mozilla.org/en-US/docs/Web/Events/canplaythrough)

```js
if (duration > 0)
{
	const bufferingDuration = Date.now() - startTimer;
	const totalLoadTime = bytesLoaded == 0 ? Number.POSITIVE_INFINITY : bytesTotal / bytesLoaded * bufferingDuration;
	console.log("(" + bytesLoaded + "/" + bytesTotal + ")" + bufferingDuration + " : " + totalLoadTime.toFixed(2))
	if (totalLoadTime < duration || bufferingDuration + duration > totalLoadTime){
		// here the media can be play through
	}
}
```

Where `startTimer` is value of `Date.now()` defined at begin of the media loading and `duration` is length of media in ms.

## Date offset by month

```js
//Before = After - 5.5 months
const monthRatio = 5.5;
const today = new Date();
//console.log("today: " + today.toDateString())

const after = new Date(today.fullYear, today.month, today.date);
console.log("after: " + after.toDateString());

const before = new Date(today.fullYear, (today.month - uint(monthRatio)), 32);
console.log((32 - before.date) + " jours");
const before = new Date(before.fullYear, (today.month - uint(monthRatio)), today.date - Math.round(monthRatio % 1 * (32 - before.date)))
console.log("before (after - " + monthRatio + " months): " + before.toDateString())
```

## Integer to hexadecimal

```js
// From https://github.com/mikechambers/as3corelib/blob/master/src/com/adobe/utils/IntUtil.as
/** String for quick lookup of a hex character based on index */
const hexChars = "0123456789abcdef";

/**
 * Outputs the hex value of a int, allowing the developer to specify
 * the endinaness in the process.  Hex output is lowercase.
 *
 * @param n The int value to output as hex
 * @param bigEndian Flag to output the int as big or little endian
 * @return A string of length 8 corresponding to the hex representation of n ( minus the leading "0x" )
 *
 * @example toHex(3, false) === "03000000"
 * @example toHex(3, true) === "00000003"
 */
function toHex( n, bigEndian = false ) {
	let s = "";

	if ( bigEndian ) {
		for ( let i = 0; i < 4; i++ ) {
			s += hexChars.charAt( ( n >> ( ( 3 - i ) * 8 + 4 ) ) & 0xF )
				+ hexChars.charAt( ( n >> ( ( 3 - i ) * 8 ) ) & 0xF );
		}
	} else {
		for ( let x = 0; x < 4; x++ ) {
			s += hexChars.charAt( ( n >> ( x * 8 + 4 ) ) & 0xF )
				+ hexChars.charAt( ( n >> ( x * 8 ) ) & 0xF );
		}
	}

	return s;
}
```

## Stringify a number with a custom base

```js
/**
 * Encode a number to string with a custom charset. Don't confuse with binary encoding (like base64)
 * @param {number} value
 * @param {string} charset Each chars must be unique
 * @return {string}
 *
 * @example toBase(31415926535, "0123456789") === "31415926535"//base 10
 * @example toBase(31415926535, String.fromCharCode(...new Array(0x7E-0x20+1).fill(0).map((c,i)=>0x20+i))) === "$%b~(R"//base 95
 * @example toBase(0xDEADBEEF, "0123456789abcdef") === "deadbeef"//base 16
 * @example toBase(0b10101010, "01") === "10101010"//base 2
 * @example toBase(0o51, "01234567") === "51"//base 8
 * @example toBase(3, "abcd") === "d" && toBase(4, "abcd") === "ba"
 *
 * @see https://github.com/aseemk/bases.js
 */
function toBase(value, charset){
  let result = "";
  const base = charset.length;
  value = Math.abs(value);

  // execute at least once for the "zero"
  do{
    result = charset.charAt(value % base) + result;
    value = Math.floor(value / base);
  }while(value > 0);

  return result;
}
```

See also [Integer to hexadecimal](#integer-to-hexadecimal)

## Walk through object path

```js
var walk = (obj, path) => path.split('.').reduce((obj, key) => obj && obj[key], obj);
walk({foo: { bar: {baz: 1} }}, ["foo", "bar", "baz"]);// -> 1
```

## Array mutation inside loop

Array mutations inside loop map/forEach etc: Items will be skipped!

```js
[1,2,3,4,5].forEach((a,i,arr)=>{console.log(a); arr.splice(i,1)})// 1, 3, 5
```

## Simple CSV Parser

**TODO use [Recursive descent parser](https://en.wikipedia.org/wiki/Recursive_descent_parser)**

```js
function parseCSV(s){
	let i = 0;
	let y = 0;
	const results = [];
	while(true){
		if(i >= s.length)
			break;

		//new row
		if("\n\r".includes(s[i])){
			i++;
			y++;
			continue;
		}

		// skip whitespaces
		if(" \t".includes(s[i])){
			i++;
			continue
		}

		// Read value
		let value = "";
		if(s[i] === '"'){
			i++;
			// Handle escaped double quote with double quote
			for(; s[i] && (s[i] !== '"' || s[i+1] === '"'); i += s[i] === '"' ? 2 : 1)
				value += s[i]
			i++
		}
		else{
			while(s[i] && !",\n\r".includes(s[i]))
				value += s[i++]
		}

		(results[y] = results[y] || []).push(value);

		// Skip comma to read next value
		if(s[i] === ",") i++
	}
	return results;
}
```

```js
parseCSV(`a,b,c\n,"d
e",'f'`);
// -> [["a", "b", "c"], ["", "d\ne", "'f'"]]
```

## Error to JSON

`name`, `message` and `stack` are not enumerable, output error in JSON will give an empty object `{}`

```js
["name", "message", "stack", ...Object.keys(error)].reduce((result, key) => (result[key] = error[key], result), {})
Object.getOwnPropertyNames(error).reduce((result, key) => (result[key] = error[key], result), {})
```

See also [Stack trace](#stack-trace)

## Stack trace

- `new Error().stack`
- [console.trace() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Console/trace)
- [Error.prototype.stack - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error/Stack)
- [StackTrace.JS - Framework-agnostic, micro-library for getting stack trace in all web browsers](https://www.stacktracejs.com/)
- [stacktracejs/stacktrace.js: Generate, parse, and enhance JavaScript stack trace in all web browsers](https://github.com/stacktracejs/stacktrace.js/)
- [stacktracejs/error-stack-parser: Extract meaning from JS Errors](https://github.com/stacktracejs/error-stack-parser)


## Empty object

```js
o.constructor === Object && Object.keys(o).length === 0
// Note: Object.keys(new Date()).length === 0;
```

```js
function isEmpty(o) {
	for(var p in o) {
		if(o.hasOwnProperty(p)){
			return false;
		}
	}
	return JSON.stringify(o) === JSON.stringify({});
}
```

## Function source

```js
String(function(){console.log("Hello")}).slice(11, -1);// console.log("Hello")
```


## Tree traversal

- [Tree traversal with ES6 generator - Hemanth.HM](https://h3manth.com/new/blog/2014/tree-traversal-with-es6-generator/)
