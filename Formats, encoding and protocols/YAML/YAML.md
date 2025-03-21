- [YAML — Wikipedia](https://en.wikipedia.org/wiki/YAML)
- [The Official YAML Web Site](http://yaml.org/)
- `*.yml`

## Syntax

- [syntax - How do I break a string in YAML over multiple lines? - Stack Overflow](https://stackoverflow.com/questions/3790454/how-do-i-break-a-string-in-yaml-over-multiple-lines/21699210#21699210)
- [Scripts and job logs | GitLab](https://docs.gitlab.com/ee/ci/yaml/script.html#use-special-characters-with-script) - "Use special characters with script": "commands that contain a colon (`:`) must be wrapped in single quotes (`'`)"

## YAML is a superset of JSON

JSON can be used as YAML, but:

- duplicated keys can't be used ("JSON's RFC4627 requires that mappings keys merely “SHOULD” be unique, while YAML insists they “MUST” be" — [YAML Ain’t Markup Language (YAML™) Version 1.2](https://yaml.org/spec/1.2-old/spec.html#id2759572))
- JSON must not use tabs as indentation ("yaml.scanner.ScannerError: while scanning for the next token found character '\t' that cannot start any token in "&lt;unicode string&gt;"") (some parsers support it)

> YAML can therefore be viewed as a natural superset of JSON, offering improved human readability and a more complete information model. This is also the case in practice; every JSON file is also a valid YAML file. This makes it easy to migrate from JSON to YAML if/when the additional features are required.
>
> — [YAML Ain’t Markup Language (YAML™) Version 1.2](https://yaml.org/spec/1.2-old/spec.html#id2759572)

- [YAML as a JSON superset and TAB characters - Stack Overflow](https://stackoverflow.com/questions/25974485/yaml-as-a-json-superset-and-tab-characters)

## Entity bomb

- [Billion laughs — Wikipedia](https://en.wikipedia.org/wiki/Billion_laughs)
