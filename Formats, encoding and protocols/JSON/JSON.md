- [seriot.ch - Parsing JSON is a Minefield 💣](http://seriot.ch/parsing_json.html)
- Convert JSON to C data literals. https://github.com/orangeduck/json2c
- [mikechambers/as3corelib: An ActionScript 3 Library that contains a number of classes and utilities for working with ActionScript? 3. These include classes for MD5 and SHA 1 hashing, Image encoders, and JSON serialization as well as general String, Number and Date APIs.](https://github.com/mikechambers/as3corelib)

## JSON Schema

- [JSON Schema Store](http://schemastore.org/json/)
- [JSON Schema](http://json-schema.org/)
- [jdorn/json-editor: JSON Schema Based Editor](https://github.com/jdorn/json-editor)
- [Understanding JSON Schema — Understanding JSON Schema 1.0 documentation](https://spacetelescope.github.io/understanding-json-schema/)
- [Fake your JSON-Schemas!](http://json-schema-faker.js.org/)

## Binary data

Base64, Base92, etc.

	// Get list of available chars inside string that use 1 byte (last code point usable in UTF-8 is 0x7F https://en.wikipedia.org/wiki/UTF-8, ASCII 7bits only) and doesn't require JSON encoding
	JSON.parse(JSON.stringify(String.fromCharCode(...Array.from({length: 0x7F + 1}, (value, index) => index))).replace(/\\(u[0-9a-z]{4,}|.)/gi, ""))

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

## Comments

Comment syntax not exist in JSON (like `/* ... */` or `// ...`). Use a field for that (could start with `_`, `@`, `#`, `//`, etc.)

For multilines:

You should not use duplicated keys. It's could be supported by parser/writer but it's not standard.

	{
		"@comment": [
			"comment line 1",
			"comment line 2"
		]
	}

- [Comment in JSON I removed comment from JSON because I saw people were usin...](https://plus.google.com/+DouglasCrockfordEsq/posts/RK8qyGVaGSr)
- [standards - Does JSON syntax allow duplicate keys in an object? - Stack Overflow](https://stackoverflow.com/questions/21832701/does-json-syntax-allow-duplicate-keys-in-an-object)
- [javascript - Can I comment a JSON file? - Stack Overflow](https://stackoverflow.com/questions/244777/can-i-comment-a-json-file)
- [seriot.ch - Parsing JSON is a Minefield 💣](http://seriot.ch/parsing_json.html#41)
