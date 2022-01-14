- [Parsing JSON is a Minefield](https://web.archive.org/web/20211012051215/http://seriot.ch/projects/parsing_json.html)
- Convert JSON to C data literals. https://github.com/orangeduck/json2c
- [mikechambers/as3corelib: An ActionScript 3 Library that contains a number of classes and utilities for working with ActionScript? 3. These include classes for MD5 and SHA 1 hashing, Image encoders, and JSON serialization as well as general String, Number and Date APIs.](https://github.com/mikechambers/as3corelib)
- [We released simdjson 0.3: the fastest JSON parser in the world is even better! – Daniel Lemire's blog](https://lemire.me/blog/2020/03/31/we-released-simdjson-0-3-the-fastest-json-parser-in-the-world-is-even-better/) - [Simdjson 0.3: Faster JSON parser | Hacker News](https://news.ycombinator.com/item?id=22745351)

## JSON Schema

- [JSON Schema](http://json-schema.org/)
- [Understanding JSON Schema — Understanding JSON Schema 7.0 documentation](https://json-schema.org/understanding-json-schema/index.html)
- [JSON Schema Store](http://schemastore.org/json/) - List of common JSON Schema
- [JSON Schema](https://cswr.github.io/JsonSchema/) - For JSON Schema Draft 4 and below
- [jdorn/json-editor: JSON Schema Based Editor](https://github.com/jdorn/json-editor)

Data generator from schema:

- [Fake your JSON-Schemas!](https://json-schema-faker.js.org) - [json-schema-faker/json-schema-faker: JSON-Schema + fake data generators](https://github.com/json-schema-faker/json-schema-faker)
- [Online JSON Schema Validator and Generator](https://extendsclass.com/json-schema-validator.html)
- [andreineculau/json-schema-random: Given a JSON Schema, provide a random valid instance](https://github.com/andreineculau/json-schema-random)
- [jonahkagan/schematic-ipsum: A simple service that generates fake JSON data in accordance with a JSON Schema](https://github.com/jonahkagan/schematic-ipsum)
- [Humanstate/json-schema-tojson: Convert JSON Schema definitions to "fake" JSON structures for emulation and testing](https://github.com/Humanstate/json-schema-tojson)

## Binary data

Base64, Base92, etc.

```js
// Get list of available chars inside string that use 1 byte (last code point usable in UTF-8 is 0x7F https://en.wikipedia.org/wiki/UTF-8, ASCII 7bits only) and doesn't require JSON encoding
JSON.parse(JSON.stringify(String.fromCharCode(...Array.from({length: 0x7F + 1}, (value, index) => index))).replace(/\\(u[0-9a-z]{4,}|.)/gi, ""))
```

```js
// Encode integer to include it in JSON string in first UTF-8 byte
function encode(value){
	value = Math.max(value, 0);// only unsigned value
	const charset = " !#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[]^_`abcdefghijklmnopqrstuvwxyz{|}~";
	const radix = charset.length;

	let s = "";
	do {
		s = charset.charAt(value % radix) + s;
		value = Math.floor(value / radix);
	} while(value >= 1)

	return s;
}

function decode (value) {
	// const charset = " !#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[]^_`abcdefghijklmnopqrstuvwxyz{|}~"
	const charset = "!#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[]^_`abcdefghijklmnopqrstuvwxyz{|}~";
	const radix = charset.length;

	let n = 0;
	for(let index = 0, length = value.length; index < length; index++){
		n += charset.indexOf(value.charAt(index)) * radix ** (length - 1 - index);
	}
	return n;
}
```

## Comments

Comment syntax does not exist in JSON (like `/* ... */` or `// ...`). Use a field for that, which could start with `$`, `@`, `#`, `//`, etc.

You should not use duplicated keys. It's could be supported by parser/writer but it's not standard.

Format used by [JSON Schema](https://json-schema.org/understanding-json-schema/reference/generic.html#comments):

```json
{
	"$comment": "comment line 1\ncomment line 2"
}
```

- [Comment in JSON I removed comment from JSON because I saw people were usin...](https://plus.google.com/+DouglasCrockfordEsq/posts/RK8qyGVaGSr)
- [standards - Does JSON syntax allow duplicate keys in an object? - Stack Overflow](https://stackoverflow.com/questions/21832701/does-json-syntax-allow-duplicate-keys-in-an-object)
- [javascript - Can I comment a JSON file? - Stack Overflow](https://stackoverflow.com/questions/244777/can-i-comment-a-json-file)
- [seriot.ch - Parsing JSON is a Minefield 💣](http://seriot.ch/parsing_json.html#41)

## Tools

- CLI [jq](https://stedolan.github.io/jq/)
	- [stedolan/jq: Command-line JSON processor](https://github.com/stedolan/jq)
	- [Extracting objects recursively with jq | Simon Willison’s TILs](https://til.simonwillison.net/jq/extracting-objects-recursively)
- [antonmedv/fx: Command-line tool and terminal JSON viewer 🔥](https://github.com/antonmedv/fx)
