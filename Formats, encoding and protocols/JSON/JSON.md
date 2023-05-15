- [Parsing JSON is a Minefield](https://web.archive.org/web/20211012051215/http://seriot.ch/projects/parsing_json.html)
- [orangeduck/json2c: Convert JSON to C data literals](https://github.com/orangeduck/json2c)
- [mikechambers/as3corelib: An ActionScript 3 Library that contains a number of classes and utilities for working with ActionScript? 3. These include classes for MD5 and SHA 1 hashing, Image encoders, and JSON serialization as well as general String, Number and Date APIs.](https://github.com/mikechambers/as3corelib)
- [The Workbench: JSON Compression : Transpose & Binary](https://web.archive.org/web/20220210192810/https://mainroach.blogspot.com/2013/08/json-compression-transpose-binary.html)

## Parser

- [We released simdjson 0.3: the fastest JSON parser in the world is even better! – Daniel Lemire's blog](https://lemire.me/blog/2020/03/31/we-released-simdjson-0-3-the-fastest-json-parser-in-the-world-is-even-better/) - [Simdjson 0.3: Faster JSON parser | Hacker News](https://news.ycombinator.com/item?id=22745351)

## JSON path

- [RFC 6901 - JavaScript Object Notation (JSON) Pointer](https://tools.ietf.org/html/rfc6901)
- xpath
- [nemtsov/json-mask: Tiny language and engine for selecting specific parts of a JS object, hiding the rest.](https://github.com/nemtsov/json-mask)

## JSON query and field selection

- [nemtsov/json-mask: Tiny language and engine for selecting specific parts of a JS object, hiding the rest.](https://github.com/nemtsov/json-mask)
- jq (see [Tools](#tools))
- [RFC 6901: JavaScript Object Notation (JSON) Pointer](https://www.rfc-editor.org/rfc/rfc6901) - JSON pointer (used by JSON schema)
- JSON Path
	- [JSONPath Online Evaluator](https://jsonpath.com/)
	- [JSONPath - XPath for JSON](https://web.archive.org/web/20230208122238/https://goessner.net/articles/JsonPath/index.html)
	- [How to perform partial object serialization providing "paths" using Newtonsoft JSON.NET - Stack Overflow](https://stackoverflow.com/questions/30304128/how-to-perform-partial-object-serialization-providing-paths-using-newtonsoft-j/30333562#30333562)
- [Queries and Mutations | GraphQL](https://graphql.org/learn/queries/)
- Facebook (Social) Graph API fields:
	- [Fields - API Graph](https://developers.facebook.com/docs/graph-api/overview#fields)
	- [Field Expansion - API Graph](https://developers.facebook.com/docs/graph-api/guides/field-expansion)
	- `?metadata=1` to get all available fields
	- `https://graph.facebook.com/me?fields=id,name,albums.limit(5){name,photos.limit(2).after(MTAyMTE1OTQwNDc2MDAxNDkZD){name,picture.width(100).height(100).as(picture_small),picture.width(720).height(720).as(picture_large),tags.limit(2)}},posts.limit(5),adaccounts{campaigns{adsets{ads{insights.time_range({'since':'2020-05-01','until':'2020-05-01'}){adset_id,campaign_id,ad_id,clicks}}}}}`
	- `act_2222222/insights?fields=unique_actions,actions&level=account&time_ranges=[{since:'2020-06-12',until:'2020-06-12'}]`
	- see [Facebook Graph API Explorer](https://developers.facebook.com/tools/explorer/)
- [Retrieve selected fields from a search | Elasticsearch Guide \[8.6\] | Elastic](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-fields.html#search-fields-param) - Elasticsearch fields selection

## JSON schema

Media type with schema `application/json;schema="http://example.com/my-hyper-schema#`. See [JSON Schema: A Media Type for Describing JSON Documents](http://json-schema.org/draft-07/json-schema-core.html#rfc.section.11.2)
It's possible to use `Link` header with `rel` parameter instead. See [JSON Schema: A Media Type for Describing JSON Documents](http://json-schema.org/draft-07/json-schema-core.html#rfc.section.11.1)

There is not inherance, but a [validation rule](http://json-schema.org/draft-07/json-schema-validation.html#rfc.section.6.7.1) (more like interfaces):

```json
"allOf": [
	{
		"$ref": "#/definitions/some-object"
	},
	{
		"type": "object",
		"properties": {
			"specific-property": {
				"type": "number"
			}
		}
	}
]
```

- [Explain why inheritance isn't the right model · Issue #148 · json-schema-org/json-schema-org.github.io](https://github.com/json-schema-org/json-schema-org.github.io/issues/148)

Can be used to edit (with a dedicated UI) JSON and validate again a schema it with:

- [JSON Editor Online - view, edit and format JSON online](https://jsoneditoronline.org/)

JSON Schema editors and validators:

- [JSON Schema Validator - Newtonsoft](https://www.jsonschemavalidator.net/)
- [JSON Schema validation online](https://json-schema-validator.herokuapp.com/)
- [korzio/djv: Dynamic JSON Schema Validator - Supports draft-04/06](https://github.com/korzio/djv) - [RunKit + npm: djv](https://npm.runkit.com/djv)
- [Ajv - Another JSON Schema Validator](http://epoberezkin.github.io/ajv/) - [RunKit + npm: ajv](https://npm.runkit.com/ajv)
	1. open [RunKit + npm: ajv](https://npm.runkit.com/ajv)
	2. past the following code in the playground textarea
	3. fill it
	4. then "run" (button below the textarea)
	5. see the result

	```js
	const Ajv = require('ajv');
	const ajv = new Ajv({allErrors: true});
	ajv.addMetaSchema(require('ajv/lib/refs/json-schema-draft-06.json'));

	function test(data) {
	  const valid = validate(data);
	  if (valid){
		console.log('Valid!');
	  }
	  else{
		console.log('Invalid: ' + ajv.errorsText(validate.errors));
	  }
	}

	const schema ={
	  /* the content of CEDDL Schema */
	};

	const digitalData = {
	  /* your digitalData here */
	};

	const validate = ajv.compile(schema);
	test(digitalData);
	```
- [ebdrup/json-schema-benchmark: Benchmarks for Node.js JSON-schema validators](https://github.com/ebdrup/json-schema-benchmark)

Documentation:

- [Specification](http://json-schema.org/specification.html)
- [JSON Schema](http://json-schema.org/)
- [Understanding JSON Schema — Understanding JSON Schema 7.0 documentation](https://json-schema.org/understanding-json-schema/index.html)
- [JSON Schema Store](http://schemastore.org/json/) - List of common JSON Schema
- [JSON Schema](https://cswr.github.io/JsonSchema/) - For JSON Schema Draft 4 and below
- [jdorn/json-editor: JSON Schema Based Editor](https://github.com/jdorn/json-editor)

See also

- [JSchema](http://jschema.org/)

Data generator from schema:

- [Fake your JSON-Schemas!](https://json-schema-faker.js.org) - [json-schema-faker/json-schema-faker: JSON-Schema + fake data generators](https://github.com/json-schema-faker/json-schema-faker)
- [Online JSON Schema Validator and Generator](https://extendsclass.com/json-schema-validator.html)
- [andreineculau/json-schema-random: Given a JSON Schema, provide a random valid instance](https://github.com/andreineculau/json-schema-random)
- [jonahkagan/schematic-ipsum: A simple service that generates fake JSON data in accordance with a JSON Schema](https://github.com/jonahkagan/schematic-ipsum)
- [Humanstate/json-schema-tojson: Convert JSON Schema definitions to "fake" JSON structures for emulation and testing](https://github.com/Humanstate/json-schema-tojson)

## Related formats

- [ndjson/ndjson-spec: Specification](https://github.com/ndjson/ndjson-spec) - Newline delimited JSON

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
