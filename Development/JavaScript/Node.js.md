["Node.js" (written and spoken guidelines)](https://twitter.com/bitandbang/status/1087359646367731719)

![Written and spkoen guidelines](./Node.js%20written%20and%20spkoen%20guidelines.jpg)

- [Node.js Security Checklist | @RisingStack](https://blog.risingstack.com/node-js-security-checklist/)

## Libraries

- [Server-side Libraries](https://github.com/dexteryy/spellbook-of-modern-webdev#server-side-libraries-nodejs)

- moment - date handling
- yars, commander.js - helper for create CLI


Unorganized:

- [Stuk/jszip: Create, read and edit .zip files with Javascript](https://github.com/Stuk/jszip) - Read and write ZIP asynchronously
- [expressjs/session: Simple session middleware for Express](https://github.com/expressjs/session) - Handle clients sessions
- [mail-null](https://www.npmjs.com/package/mail-null) - `sleep 2 && open http://localhost:2345 & SMTP_PORT=3456 PORT=2345 npx mail-null`
	Unix: `PORT=3512 npx mail-null`, Windows: `set PORT=3512&&cmd /c start http://localhost:%PORT%&&npx mail-null`
- [nodemailer](https://www.npmjs.com/package/nodemailer) - Email client
- [Stuk/jszip: Create, read and edit .zip files with Javascript](https://github.com/Stuk/jszip)
- [expressjs/express: Fast, unopinionated, minimalist web framework for node.](https://github.com/expressjs/express) - [Express/Node introduction - Learn web development | MDN](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/Introduction)
- [SBoudrias/Inquirer.js: A collection of common interactive command line user interfaces.](https://github.com/SBoudrias/Inquirer.js/)
- [tj/commander.js: node.js command-line interfaces made easy](https://github.com/tj/commander.js) and [yargs/yargs: yargs the modern, pirate-themed successor to optimist.](https://github.com/yargs/yargs)

Configuration:

- parse [configuration file](https://en.wikipedia.org/wiki/Configuration_file) / [run commands](https://en.wikipedia.org/wiki/Run_command): [rc](https://www.npmjs.com/package/rc)
- load environnement variable (from `.env` file): ~~[dotenv](https://www.npmjs.com/package/dotenv)~~; do it view the command line instead: [bash - Set environment variables from file of key/value pairs - Stack Overflow](https://stackoverflow.com/questions/19331497/set-environment-variables-from-file-of-key-value-pairs/20909045#20909045)
- [davidtheclark/cosmiconfig: Find and load configuration from a package.json property, rc file, or CommonJS module](https://github.com/davidtheclark/cosmiconfig) - used by [stylelint](https://stylelint.io/user-guide/configure) to load `.myapprc`, `.myapprc.json`, `myapp.config.js`, etc.
- configuration overrides:
	- [stylelint](https://stylelint.io/user-guide/configure#overrides): https://github.com/stylelint/stylelint/blob/1cce8bd49ab6b5948381d10537796a7f30bd1bb8/lib/augmentConfig.js#L442-L476
	- [eslint](https://eslint.org/docs/latest/use/configure/configuration-files#how-do-overrides-work): https://github.com/eslint/eslintrc/blob/41efba80452ee0934ab60e4f5afbafac477ac3e7/lib/config-array-factory.js#L684-L713

Parse DOM (HTML, XML, SVG) and CSSOM:

- [jsdom/jsdom: A JavaScript implementation of the WHATWG DOM and HTML standards, for use with node.js](https://github.com/jsdom/jsdom) - use parse5 and saxes
- [WebReflection/linkedom: A triple-linked lists based DOM implementation.](https://github.com/WebReflection/linkedom)
- [fb55/htmlparser2: Forgiving html and xml parser](https://github.com/fb55/htmlparser2/)
- [inikulin/parse5: HTML parsing/serialization toolset for Node.js. WHATWG HTML Living Standard (aka HTML5)-compliant.](https://github.com/inikulin/parse5)
- [xmldom/xmldom: A pure JavaScript W3C standard-based (XML DOM Level 2 Core) DOMParser and XMLSerializer module.](https://github.com/xmldom/xmldom) - from [jindw/xmldom](https://github.com/jindw/xmldom) (dead project)
- [lddubeau/saxes: An evented streaming XML parser in JavaScript](https://github.com/lddubeau/saxes) - used by jsdom and [svgo's svg2js](https://github.com/svg/svgo/blob/master/lib/svgo/svg2js.js) (see also [js2svg](https://github.com/svg/svgo/blob/master/lib/svgo/js2svg.js))
- [NaturalIntelligence/fast-xml-parser: Validate XML, Parse XML to JS/JSON and vise versa, or parse XML to Nimn rapidly without C/C++ based libraries and no callback](https://github.com/NaturalIntelligence/fast-xml-parser) - Read and write XML with a DOM (pure JS), an alternative to jindw/xmldom
- [tildeio/simple-html-tokenizer: A lightweight JavaScript library for tokenizing non-`\<script\>` HTML expected to be found in the `\<body\>` of a document](https://github.com/tildeio/simple-html-tokenizer)
- [libxmljs/libxmljs: libxml bindings for v8 javascript engine](https://github.com/libxmljs/libxmljs) - Read and write XML (native)
- [rgrove/parse-xml: A fast, safe, compliant XML parser for Node.js and browsers.](https://github.com/rgrove/parse-xml) - Read XML
- [csstree/csstree: Fast detailed CSS parser with syntax validation](https://github.com/csstree/csstree) - Read and write CSS

Security:

- [http-auth/src at master · http-auth/http-auth](https://github.com/http-auth/http-auth/tree/master/src) - Basic and Digest HTTP Authentification (express)
- [jshttp/basic-auth: Generic basic auth Authorization header field parser](https://github.com/jshttp/basic-auth) - Basic HTTP Authentification (generic)
- [auth0/node-jsonwebtoken: JsonWebToken implementation for node.js](https://github.com/auth0/node-jsonwebtoken) - JSON Token generation and verification (for access token)
- [kelektiv/node.bcrypt.js: bcrypt for NodeJs](https://github.com/kelektiv/node.bcrypt.js) - bcrypt hash generation and verification (for password storage)

Network:

- [ljharb/qs: A querystring parser with nesting support](https://github.com/ljharb/qs) - `assert.deepEqual(qs.parse("foo[bar]=baz"), {foo: {bar: "baz"}});`

## Relative path

```js
path.join(__dirname, "views");
path.resolve(".")// > /path/to/dir
```

## Is parent path

Aka is subdir

```js
const path = require('path');

function isParentPath(parent, filepath){
	const relative = path.relative(parent, filepath);
	return !!relative && relative.split(path.sep, 1)[0] !== ".." && !path.isAbsolute(relative);
}
```

- [javascript - Determine if a path is subdirectory of another in Node.js - Stack Overflow](https://stackoverflow.com/questions/37521893/determine-if-a-path-is-subdirectory-of-another-in-node-js/45242825#comment81433484_45242825)

## List files recursively

```js
import path from "path";
import {lstat, readdir} from "fs/promise";

// Walk directories
async function* getFiles(entry){
	if(!(await lstat(entry)).isDirectory()){
		return entry;
	}

	for(const subEntry of await readdir(entry)){
		yield* getFiles(path.join(entry, subEntry));
	}
};

for(const file of await getFiles("/some/path")){
	console.log(file);
}
```

- [List all file in a directory in Node.j recursively in a synchronou fashion](https://gist.github.com/kethinov/6658166)

## Keep local copy of dependencies

Usefull to keep it on version control system or in context of security

- https://github.com/JamieMason/shrinkpack
- https://docs.npmjs.com/cli/shrinkwrap

## Hard links to same dependencies across projects

In all `node_modules` directory on an hard drive.

- https://github.com/jeffbski/pkglink

## Turn off Spotflight indexation of dependencies

```sh
find /path/to/projects -type d  -path '*node_modules/*' -prune -o -type d -name 'node_modules' -exec xattr -w com.apple.metadata:com_apple_backup_excludeItem com.apple.backupd '{}' \;
# find /path/to/projects -type d  -path '*node_modules/*' -prune -o -type d -name 'node_modules' -exec touch '{}/.metadata_never_index' \;
```

- [Prevent spotlight from indexing folders with a certain name - Ask Different](https://apple.stackexchange.com/questions/247019/prevent-spotlight-from-indexing-folders-with-a-certain-name/258791#258791)

## Performances

- [The drastic effects of omitting NODE_ENV in your Express.js applications | Dynatrace blog](https://www.dynatrace.com/news/blog/the-drastic-effects-of-omitting-node-env-in-your-express-js-applications/)
- [Keeping Node.js Fast: Tools, Techniques, And Tips For Making High-Performance Node.js Servers — Smashing Magazine](https://www.smashingmagazine.com/2018/06/nodejs-tools-techniques-performance-servers/)

### Load balancer and reverse proxy

`process.env.IN_PASSENGER === "1"` `typeof PhusionPassenger !== "undefined"`

- [Passenger Library](https://www.phusionpassenger.com/library/) - Module for ngnix or Apache to handle configuration, deployment, reload, etc. of Node.js, Ruby, Python
- [Performance Best Practice Using Expres in Production](http://expressjs.com/en/advanced/best-practice-performance.html#use-a-reverse-proxy)
- [Understanding Passenger - Passenger + Node.j basic - Passenger Library](https://www.phusionpassenger.com/library/walkthroughs/basics/nodejs/fundamental_concepts.html)

## Debug

- `node inspect server.js`
- [Debugging - Getting Started | Node.js](https://nodejs.org/en/docs/guides/debugging-getting-started/#inspector-clients) - Inspector Clients (Chrome, Edge)
- `NODE_ENV=development`
- `node --trace-warnings servefr.js`
- [evanw/node-source-map-support: Adds source map support to node.js (for stack traces)](https://github.com/evanw/node-source-map-support)
- [Remote Debugging Node.js in Docker – SENSEI Developer Blog – Medium](https://medium.com/sensei-developer-blog/remote-debugging-node-js-in-docker-1936eb4ef522)
- [The Definitive Guide for Monitoring Node.js Applications | @RisingStack](https://blog.risingstack.com/monitoring-nodejs-applications-nodejs-at-scale/)
- [Diagnostic report | Node.js v17.9.0 Documentation](https://nodejs.org/docs/latest-v17.x/api/report.html)
- [loglevel - npm](https://www.npmjs.com/package/loglevel)

### Send log infos client side

HTTP header `X-ChromeLogger-Data: jsonbase64value`

- [Console messages - Firefox Developer Tools | MDN](https://developer.mozilla.org/en-US/docs/Tools/Web_Console/Console_messages#Server)
- [Chrome Logger - Tech Specs](https://craig.is/writing/chrome-logger/techspecs)
- [olahol/express-chrome-logger: Debug your express app using the Chrome console.](https://github.com/olahol/express-chrome-logger)
- [yannickcr/node-chromelogger: Implementation of the Chrome Logger protocol for Node.js](https://github.com/yannickcr/node-chromelogger)

## Profile

CPU profile file:

- use the node `--cpu-prof` option that will generate a `cpuprofile` file
- use Chrome Dev Tools Performance tab to read the file as flamegraph where the x-axis represents when a call happened. It annotate the source code with the sampled traces this gives an approximate time how much each line took to execute
- use [speedscope](https://www.speedscope.app/) ([GitHub - jlfwong/speedscope: 🔬 A fast, interactive web-based viewer for performance profiles.](https://github.com/jlfwong/speedscope)) to read the file as flamegraph but it merge similar call-stacks together to see where the time is being spent, the x-axis represents time consumed of the total time. It referred to as a "left-heavy" visualization. It's not a standard flamegraph where the x-axis represents when a call happened.
- use `node --cpu-prof $(which npm) run myscript` to do it when [run a script](https://docs.npmjs.com/cli/commands/npm-run-script)

Heap profile file:

- use the node `--heap-prof` option that will generate a `heapprofile` file
- it can be open in Chrome Dev Tools Memory tab

- [--cpu-prof - Command-line API | Node.js Documentation](https://nodejs.org/api/cli.html#--cpu-prof)
- [--heap-prof - Command-line API | Node.js Documentation](https://nodejs.org/api/cli.html#--heap-prof)

## Performance

- [Performance | Electron](https://www.electronjs.org/docs/latest/tutorial/performance)
- Speeding up the JavaScript ecosystem
	- [Speeding up the JavaScript ecosystem - one library at a time](https://web.archive.org/web/20230929215348/https://marvinh.dev/blog/speeding-up-javascript-ecosystem/)
	- [Speeding up the JavaScript ecosystem - module resolution](https://web.archive.org/web/20230929222224/https://marvinh.dev/blog/speeding-up-javascript-ecosystem-part-2/)
	- [Speeding up the JavaScript ecosystem - eslint](https://web.archive.org/web/20230929215346/https://marvinh.dev/blog/speeding-up-javascript-ecosystem-part-3/)
	- [Speeding up the JavaScript ecosystem - npm scripts](https://web.archive.org/web/20230929215300/https://marvinh.dev/blog/speeding-up-javascript-ecosystem-part-4/)
	- [Speeding up the JavaScript ecosystem - draft-js emoji plugin](https://web.archive.org/web/20230929220034/https://marvinh.dev/blog/speeding-up-javascript-ecosystem-part-5/)
	- [Speeding up the JavaScript ecosystem - Polyfills gone rogue](https://web.archive.org/web/20230929211110/https://marvinh.dev/blog/speeding-up-javascript-ecosystem-part-6/)
	- [Speeding up the JavaScript ecosystem - The barrel file debacle](https://web.archive.org/web/20231105163013/https://marvinh.dev/blog/speeding-up-javascript-ecosystem-part-7/)
	- [Speeding up the JavaScript ecosystem - Tailwind CSS](https://web.archive.org/web/20231111003315/https://marvinh.dev/blog/speeding-up-javascript-ecosystem-part-8/)

## Child processes

Cluster is `child_process` in a more convenient way to listen the same port by all children (it use `child_process` internally): [Cluster | Node.j v9.6.1 Documentation](https://nodejs.org/api/cluster.html#cluster_how_it_works)

- [Node.js Child Processes: Everything you need to know](https://medium.freecodecamp.org/node-js-child-processes-everything-you-need-to-know-e69498fe970a)
- [Node.j Cluster and Express](http://rowanmanning.com/posts/node-cluster-and-express/)
- [Setting up a Node.j Cluster](http://stackabuse.com/setting-up-a-node-js-cluster/)

## Standart input / output

```js
const data = require("fs").readFileSync(0, {encoding: "utf-8"});// file 0 is stdin
```

## Command line

Aka CLI

Shebang:

```sh
#!/usr/bin/env node
```

Syntax check without executing:

```sh
# https://nodejs.org/api/cli.html#cli_c_check
node --check file.js
```

Parse command line arguments:

- [node:util parseArgs](https://nodejs.org/api/util.html#utilparseargsconfig)
- [command-line-args package](https://www.npmjs.com/package/command-line-args)
- [arg package](https://www.npmjs.com/package/arg)
- [minimist package](https://www.npmjs.com/package/minimist)
- [commander package](https://www.npmjs.com/package/commander)
- [yargs package](https://www.npmjs.com/package/yargs)

## Express

Test server capacity with [mcollina/autocannon: fast HTTP/1.1 benchmarking tool written in Node.js](https://github.com/mcollina/autocannon)

**Order route registration from most specific to less specific: `/foo/bar`, `/foo`, `/`**

```js
import express from "express";

const app = express();
const port = process.env.PORT || 3000;

app.get('/posts/:id', async (req, res, next) => {
	try {
		const id = req.params.id;
		const value = await getPostById(id);
		res.render("posts", {id, value});
	}
	catch (error) {
		next(error);
	}
});

app.listen(port);
```

Internal redirect, aka reroute: [node.js - Forward request to alternate request handler instead of redirect - Stack Overflow](https://stackoverflow.com/questions/18136323/forward-request-to-alternate-request-handler-instead-of-redirect/22081112#22081112). See [Express 4.x - API Reference](http://expressjs.com/en/4x/api.html#app.METHOD)

Reroute:

```js
app.get("someroute", (req, res, next) => {
	// Reroute to index.html (could be handled by statics)
	req.url = "index.html";
	next("route");
});
```

Global error handling

At app level or a parent route level, register the error handler (a middleware with 4 arguments) **after** all other used middleware and routes handlers

- [Express error handling](https://expressjs.com/en/guide/error-handling.html)

Examples:

- [OpenUserJS/OpenUserJS.org: The home of FOSS user scripts.](https://github.com/OpenUserJS/OpenUserJS.org)

### Express libraries

- [expressjs/compression: Node.j compression middleware](https://github.com/expressjs/compression) - http compression for express (Note: doesn't compress small responses, see [expressjs/compression: Node.j compression middleware](https://github.com/expressjs/compression#threshold))
- [kwhitley/apicache: Simple API-caching middleware for Express/Node.](https://github.com/kwhitley/apicache) - HTTP cache server side for express
- [cors](https://www.npmjs.com/package/cors) - CORS for express
- [helmetjs/helmet: Help secure Express apps with various HTTP headers](https://github.com/helmetjs/helmet)
- [dexteryy/spellbook-of-modern-webdev: A Big Picture, Thesaurus, and Taxonomy of Modern JavaScript Web Development](https://github.com/dexteryy/spellbook-of-modern-webdev#microservices--api-services-nodejs)

RESTful routing (resource, facet):

- [expressjs/restful-router: Simple RESTful url router.](https://github.com/expressjs/restful-router)
- [expressjs/express-resource: Resourceful routing for Express](https://github.com/expressjs/express-resource)
- [developit/resource-router-middleware: Express REST resources as middleware mountable anywhere](https://github.com/developit/resource-router-middleware)
- [resource-router-middleware/resource-router-middleware.js at master · mrapogee/resource-router-middleware](https://github.com/mrapogee/resource-router-middleware/blob/master/src/resource-router-middleware.js)

### Get client IP with Express

```js
req.ip
```

- `app.set('trust proxy', 'loopback')`
- [Expres 4.x - API Reference](http://expressjs.com/en/4x/api.html#app.settings.table) and [Expres 4.x - API Reference](http://expressjs.com/en/4x/api.html#trust.proxy.options.table)
- [node.j - What doe "trust proxy" actually do in express.js, and do I need to use it? - Stack Overflow](https://stackoverflow.com/questions/23413401/what-does-trust-proxy-actually-do-in-express-js-and-do-i-need-to-use-it)
- [Expres behind proxies](https://expressjs.com/en/guide/behind-proxies.html)
- [node.js - Express.js: how to get remote client addres - Stack Overflow](https://stackoverflow.com/questions/10849687/express-js-how-to-get-remote-client-address) - Responses are not correct, see the link above

## NPM and packages

- [how to set shell for npm run-scripts in windows - Stack Overflow](https://stackoverflow.com/questions/23243353/how-to-set-shell-for-npm-run-scripts-in-windows) - NPM can use bash as shell on Windows (require [git for Windows](https://git-scm.com/download/win))
- [node.js - Difference between npm install and npm run build - Stack Overflow](https://stackoverflow.com/questions/43664200/difference-between-npm-install-and-npm-run-build)
- [`npm install` modifies `package-lock`! (changes resolved url protocol!) · Issue #20106 · npm/npm](https://github.com/npm/npm/issues/20106) - npm install issue that update `package-lock.json` by changing `https://` to `http://`. To fix it, use `rm -rf node_modules/ && npm cache clean --force && npm i`. See also [Some packages have dist.tarball as http and not https - 🐞 bugs - npm forum](https://npm.community/t/some-packages-have-dist-tarball-as-http-and-not-https/285/15)
- `NODE_OPTIONS=--max-old-space-size=4096 npm run myscript`, see [Best way to set --max-old-space-size when running npm? · Issue #12238 · npm/npm](https://github.com/npm/npm/issues/12238)
- `npm install --legacy-peer-deps` to fix possible retrocompatibility issues between 14 and 16

Updates:

```sh
npm outdated --parseable | cut -d ':' -f 4 | xargs npm i
# or
npx npm-check-updates -u && npm i
# see also
npm-check -u
# and
npm update --latest
```

- `yarn upgrade-interactive --latest`
- [npm-upgrade - npm](https://www.npmjs.com/package/npm-upgrade)

### Security and trust

- [How to protect yourself from npm – Timo Tijhof](https://web.archive.org/web/20230226143640/https://timotijhof.net/posts/2019/protect-yourself-from-npm/)

### Format and lint package JSON

- sort `package.json` with `npx sort-package-json` - [npm - Is there a way to alphabetize package.json without installing a package? - Stack Overflow](https://stackoverflow.com/questions/34438465/is-there-a-way-to-alphabetize-package-json-without-installing-a-package/51773989#51773989)
- [matzkoh/prettier-plugin-packagejson: Prettier plugin for package.json](https://github.com/matzkoh/prettier-plugin-packagejson) use `sort-package-json`
- [tclindner/npm-package-json-lint: Configurable linter for package.json files](https://github.com/tclindner/npm-package-json-lint)

Prettier config to override default / projet config for package JSONs:

```json
{
	"overrides": [
		{
			"files": "**/(package|package-lock).json",
			"options": {
				"tabWidth": 2,
				"useTabs": false,
				"endOfLine": "lf"
			}
		}
	]
}
```

### Inspect package

```sh
# Extract package from cache
npm pack somepackagename | tail -n 1 | xargs tar -zxzf
cat package/package.json
# View registry infos
npm view somepackagename
```

- [npm-pack | npm Documentation](https://docs.npmjs.com/cli/pack.html)
- [npm-view | npm Documentation](https://docs.npmjs.com/cli/view)
- [npmgraph - NPM Dependency Diagrams](https://npmgraph.js.org/) - Visualize NPM package dependency graphs

### Package variables

Aka environment variables

```json
{
	"name": "test",
	"main": "server/index.js",
	"scripts": {
		"start": "node $npm_package_main $pm_package_config_port",
		"start-dev": "NODE_ENV=dev node $npm_package_main $pm_package_config_port"
	},
	"engines": {
		"node": ">=9.0"
	},
	"config": {
		"port": "8080"
	}
}
```

```js
const mainEntry = process.env.npm_package_main;
const port = process.env.pm_package_config_port;
```

- [scripts | npm Docs](https://docs.npmjs.com/cli/v9/using-npm/scripts#packagejson-vars)
- [package.json | npm Docs](https://docs.npmjs.com/cli/v9/configuring-npm/package-json#config)
- [config | npm Docs](https://docs.npmjs.com/cli/v9/using-npm/config#environment-variables)

### Install for continuous integration

```sh
npm ci
```

- [npm-ci Install a project with a clean slate](https://docs.npmjs.com/cli/ci)
- [The npm Blog — Introducing `npm ci` for faster, more reliable...](https://blog.npmjs.org/post/171556855892/introducing-npm-ci-for-faster-more-reliable)

### Packages version

`npm outdated` to list "Current", "Wanted" (aka fuzzy, latest minor release) and "Latest" (latest major release) version, use `npm install <package name>@latest` to install latest version

- to allow patch releases: `1.0` or `1.0.x` or `~1.0.4`
- to allow minor releases: `1` or `1.x` or `^1.0.4`
- to allow major releases: `*` or `x`

- [npm does not upgrade package even using "--force" - Stack Overflow](https://stackoverflow.com/questions/30699486/npm-does-not-upgrade-packages-even-using-force)
- [node.js - npm install vs. update - what' the difference? - Stack Overflow](https://stackoverflow.com/questions/12478679/npm-install-vs-update-whats-the-difference)
- [npm/node-semver: The semver parser for node (the one npm uses)](https://github.com/npm/node-semver#ranges)

### Scopes packages

Aka monorepos and multi packages

`@babel/*`, `@angular/*`, etc.

- [About scopes | npm Documentation](https://docs.npmjs.com/about-scopes)
- [npm-scope | npm Documentation](https://docs.npmjs.com/misc/scope)
- [The npm Blog — Monorepos and npm](https://blog.npmjs.org/post/186494959890/monorepos-and-npm)
- [babel/monorepo.md at master · babel/babel](https://github.com/babel/babel/blob/master/doc/design/monorepo.md)

### Local packages

```json
{
  "name": "baz",
  "dependencies": {
    "bar": "file:./foo/bar"
  }
}
```

- [package.json | npm Docs](https://docs.npmjs.com/cli/v6/configuring-npm/package-json#local-paths)

### Fix package with patch

- [GitHub - ds300/patch-package: Fix broken node modules instantly 🏃🏽‍♀️💨](https://github.com/ds300/patch-package)

### EACCES errors when installing global package

First: Just **don't install packages globally**

```sh
npm install -g packagename
```

Install global with node-gyp can output errors:

```
gyp WARN EACCES user "root" does not have permission to access the dev dir "/Users/username/.node-gyp/0.0.0"
gyp WARN EACCES attempting to reinstall using temporary dev dir "/opt/local/lib/node_modules/packagename/.node-gyp"
gyp WARN EACCES user "root" does not have permission to access the dev dir "/opt/local/lib/node_modules/packagename/.node-gyp/0.0.0"
```

Use `--unsafe-perm` paramter for `npm` to fix the issue, or update the `NODE_PATH` env var.

See [Warning "root" does not have permission to access the dev dir · Issue #454 · nodejs/node-gyp](https://github.com/nodejs/node-gyp/issues/454#issuecomment-155957449)

- [config | npm Documentation](https://docs.npmjs.com/misc/config#unsafe-perm)

### NPM install resolved packages from HTTPS to HTTP

`npm config get registry` should return `https://registry.npmjs.org/`

1. `rm -rf node_modules/`
2. `npm cache clean --force`
3. Revert the changes in your `package-lock.json` file
4. `npm i`

- [npm install downgrading resolved packages from https to http registry in package-lock.json - 🐞 bugs - npm forum](https://npm.community/t/npm-install-downgrading-resolved-packages-from-https-to-http-registry-in-package-lock-json/1818/7)
- ["resolved" link changes from https://registry.npmjs.com to http://registry.npmjs.com on npm install · Issue #20719 · npm/npm](https://github.com/npm/npm/issues/20719)

### Package overrides

- [package.json | npm Docs](https://docs.npmjs.com/cli/v8/configuring-npm/package-json#overrides)
- [\[DOCS\] Please document "The overrides key will only be considered when it is in the root package.json file for a project" · Issue #4517 · npm/cli](https://github.com/npm/cli/issues/4517)

### Inspect package

```sh
# The package doesn't need to be installed
npm view <packagename> dist.tarball
```

### Crossplatform scripts

```json
{
	"name": "myapp",
	"config": { "port" : "3000" },
	"scripts": {
		"start": "ver && node --harmony app.js %npm_package_config_port% || node --harmony app.js $npm_package_config_port"
	}
}
```

Note: `ver` only exist in `cmd.exe` (default shell used on Windows). The last part (after `||`) will be executed in other shell (usally `/bin/sh` on POSIX)

Write scripts like npm do for bins (in `node_modules/.bin/`):

`mycommand`:

```sh
#!/bin/sh
basedir=$(dirname "$(echo "$0" | sed -e 's,\\,/,g')")

case `uname` in
    *CYGWIN*|*MINGW*|*MSYS*) basedir=`cygpath -w "$basedir"`;;
esac

if [ -x "$basedir/node" ]; then
  exec "$basedir/node"  "$basedir/../path/to/mycommand_nodescript" "$@"
else
  exec node  "$basedir/../path/to/mycommand_nodescript" "$@"
fi
```

`mycommand.cmd`:

```cmd
@ECHO off
GOTO start
:find_dp0
SET dp0=%~dp0
EXIT /b
:start
SETLOCAL
CALL :find_dp0

IF EXIST "%dp0%\node.exe" (
  SET "_prog=%dp0%\node.exe"
) ELSE (
  SET "_prog=node"
  SET PATHEXT=%PATHEXT:;.JS;=;%
)

endLocal & goto #_undefined_# 2>NUL || title %COMSPEC% & "%_prog%"  "%dp0%\..\path\to\mycommand_nodescript" %*
```

`mycommand.ps1`:

```pwsh
#!/usr/bin/env pwsh
$basedir=Split-Path $MyInvocation.MyCommand.Definition -Parent

$exe=""
if ($PSVersionTable.PSVersion -lt "6.0" -or $IsWindows) {
  # Fix case when both the Windows and Linux builds of Node
  # are installed in the same directory
  $exe=".exe"
}
$ret=0
if (Test-Path "$basedir/node$exe") {
  # Support pipeline input
  if ($MyInvocation.ExpectingInput) {
    $input | & "$basedir/node$exe"  "$basedir/../path/to/mycommand_nodescript" $args
  } else {
    & "$basedir/node$exe"  "$basedir/../path/to/mycommand_nodescript" $args
  }
  $ret=$LASTEXITCODE
} else {
  # Support pipeline input
  if ($MyInvocation.ExpectingInput) {
    $input | & "node$exe"  "$basedir/../path/to/mycommand_nodescript" $args
  } else {
    & "node$exe"  "$basedir/../path/to/mycommand_nodescript" $args
  }
  $ret=$LASTEXITCODE
}
exit $ret
```

See also:

- [Creating cross-platform shell scripts • Shell scripting with Node.js](https://web.archive.org/web/20221128122630/https://exploringjs.com/nodejs-shell-scripting/ch_creating-shell-scripts.html)
- [ver | Microsoft Learn](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ver)
- [npm-run-script | npm Docs](https://docs.npmjs.com/cli/v9/commands/npm-run-script#script-shell)
- [Writing cross-platform Node.js | George Ornbo](https://web.archive.org/web/20221123000204/https://shapeshed.com/writing-cross-platform-node/#scripts-in-packagejson)
- [Cross-platform Node.js | Alan Norbauer](https://web.archive.org/web/20221207005516/https://alan.norbauer.com/articles/cross-platform-nodejs#scripts-in-packagejson)
- [charlesguse/run-script-os: run-script-os will let you use OS specific operations in npm scripts without specifying which OS you are on. It's not magic though... you still have to write OS specific scripts.](https://github.com/charlesguse/run-script-os)
- [kentcdodds/cross-env: 🔀 Cross platform setting of environment scripts](https://github.com/kentcdodds/cross-env)
- https://github.com/npm/cmd-shim/blob/49ab03fae831a5727c30c37d11ba94fa5700100f/lib/index.js

## Promisify

```js
import {promisify} from 'util';
const result;
try{
	result = await promisify(obj.method.bind(obj))("value1", "value2");
	console.log(result);
}catch(error){
	console.error(error);
}
```

Instead of:

```js
obj.method("value1", "value2", (error, result) => {
	if(error){
		console.error(error);
		return;
	}

	console.log(result);
})
```

```js
import {readFile} from "fs/promises";
const content = await readFile("./test.txt", "utf8");
```

- [File system | Node.js v14.9.0 Documentation](https://nodejs.org/docs/latest/api/fs.html#fs_fs_promises_api)
- [Util | Node.js v8.9.4 Documentation](https://nodejs.org/docs/latest/api/util.html#util_util_promisify_original)

## Modules

- `core-modules/module.js`
- [Requiring module in Node.js: Everything you need to know](https://medium.freecodecamp.org/requiring-modules-in-node-js-everything-you-need-to-know-e7fbd119be8)
- [Load node.j module from string in memory - Stack Overflow](https://stackoverflow.com/questions/17581830/load-node-js-module-from-string-in-memory)

## Use URI as configuration

- https://github.com/sidorares/node-mysql2/blob/5f0fb8f1f5035e2c0207490aa2f0b838dc82fdc2/lib/connection_config.js#L166-L196
- https://github.com/nodemailer/nodemailer/blob/5da6c87766e258f1a5fa9b628f2d9f57c9d533ce/lib/shared/index.js#L16-L91

## Global error handling

- `process.setUncaughtExceptionCaptureCallback`

## Node sources

- [node/lib at master · nodejs/node](https://github.com/nodejs/node/tree/master/lib)

Zlib will don't have extra gzip header fiels (empty values):

> If deflateSetHeader is not used, the default gzip header has text false, the time set to zero, and os set to 255, with no extra, name, or comment fields.
> - https://github.com/nodejs/node/blob/master/deps/zlib/zlib.h

Zlib binding:

- [node/node_zlib.cc at master · nodejs/node](https://github.com/nodejs/node/blob/master/src/node_zlib.cc)
- [node/zlib.js at master · nodejs/node](https://github.com/nodejs/node/blob/master/lib/zlib.js)
- [node/zlib.h at master · nodejs/node](https://github.com/nodejs/node/blob/master/deps/zlib/zlib.h)

## Read UTF-8 JSON with BOM

```js
const fs = require('fs');
cost config = fs.readFileSync('./config.json', 'utf-8');
// JSON.parse(config); fail if not start with an allowed char (`"`, `[`, `{`);
// BOM is 0xefbbbf and is considered white-space
// It can be stripped by `.trim()`:
JSON.parse(config.trim());
```

## Require a virtual file

```js
const fs = require("fs");
const path = require("path");
const filename = require.resolve("chrome-devtools-frontend/front_end/sdk/CookieParser.js");
// See https://github.com/ChromeDevTools/devtools-frontend/blob/4c46d0969f10f460f2a27116f4896f20f65d0989/front_end/sdk/CookieParser.js
let content = "const SDK = module.exports = {};\n" + fs.readFileSync(filename, "utf8");
const Module = require("module");// same as module.constructor
const m = new Module(filename, module/*or module.parent*/);
m._compile(content, filename);
m.filename = filename;
m.paths = Module._nodeModulePaths(path.dirname(filename));
m.loaded = true;
module.exports = m.exports;
```

- [node/loader.js at 6ce87c027dc2a16e1b8d85c753b52270ae0c6054 · nodejs/node](https://github.com/nodejs/node/blob/6ce87c027dc2a16e1b8d85c753b52270ae0c6054/lib/internal/modules/cjs/loader.js#L781-L816)
- [node/loader.js at 6ce87c027dc2a16e1b8d85c753b52270ae0c6054 · nodejs/node](https://github.com/nodejs/node/blob/6ce87c027dc2a16e1b8d85c753b52270ae0c6054/lib/internal/modules/cjs/loader.js#L945-L948)
- [Load node.js module from string in memory - Stack Overflow](https://stackoverflow.com/questions/17581830/load-node-js-module-from-string-in-memory/17585470#17585470)
- [Package override](#package-override)

## Warning

```js
// Log stack trace of warning like depreciation https://nodejs.org/api/util.html#util_util_deprecate_fn_msg_code
process.on("warning", warning => console.warn(warning.stack));
```

- [Process | Node.js v13.6.0 Documentation](https://nodejs.org/api/process.html#process_event_warning)

## Depreciation

```sh
node --trace-warnings --trace-deprecation index.js
```

```js
const util = require('util');
module.exports.someDepreciatedFunction = util.deprecate(() => {
	// Do something here.
}, "someDepreciatedFunction() is deprecated. Use someOtherFunction() instead.", "DEP_SOME_FUNCTION");
```

- [Command Line Options | Node.js v13.6.0 Documentation](https://nodejs.org/api/cli.html#cli_trace_deprecation)
- [Util | Node.js v13.6.0 Documentation](https://nodejs.org/api/util.html#util_util_deprecate_fn_msg_code)

## Path case sensitivity on Windows

Node handle pretty well path case insensibility on Windows. But if a module use a [symbolic link or a junction](https://stackoverflow.com/questions/9042542/what-is-the-difference-between-ntfs-junction-points-and-symbolic-links/48586946#48586946) and the working directory doesn't match the case of that path (`d:\mydir` instead of `D:\MyDir`) Node load the same module twice, for each path case. Note: NPM use junction for [local path modules](https://docs.npmjs.com/files/package.json#local-paths).

See an example:

```cmd
echo module.exports = class{get __filename(){return __filename}} > Class.js
mkdir example
echo module.exports = new (require("../Class")) > example/instance.js
:: Create a junction ./junction/* <==> ./example/*
:: Note: the junction store the case used when created ("mklink /j junction .\example" vs "mklink /j junction .\Example")
mklink /j junction .\example
::dir /AL /S .
:: Main script
echo const a = require("./junction/instance"); > index.js
echo const b = require("./example/instance"); >> index.js
echo const c = require("./class"); >> index.js
echo console.log("process.cwd() =", process.cwd()); >> index.js
echo console.log("junction/instance = a"); >> index.js
echo console.log("example/instance = b"); >> index.js
echo console.log("a instanceof c =", a instanceof c); >> index.js
echo console.log("b instanceof c =", b instanceof c); >> index.js
echo console.log("a super.__filename =", a.__filename); >> index.js
echo console.log("b super.__filename =", b.__filename); >> index.js
:: Enable node module debug (request, looking and load)
::set "NODE_DEBUG=module"
:: Use powsershell to start a process with the current working directory with lowercase as working directory
powershell "Start-Process -NoNewWindow -FilePath node.exe -ArgumentList 'index.js' -Wait -WorkingDirectory $(Get-Location).ToString().ToLower()"

:: Will log:
::
:: ```
:: process.cwd() = D:\somepath\test
:: junction/instance = a
:: example/instance = b
:: a === b = false
:: a instanceof c = false
:: b instanceof c = true
:: a super.__filename = D:\SomePath\Test\Class.js
:: b super.__filename = D:\somepath\test\Class.js
:: ```
::
:: Note the difference of path case between constructors of a and b
:: A and b should be the same object, have the same constructor from ./Class.js
:: It's because the case of the instance is not the same: != path case -> != modules
:: Compare  with:
powershell "Start-Process -NoNewWindow -FilePath node.exe -ArgumentList 'index.js' -Wait
```

- `node --input-type=module -e "import*as p from'node:fs/promises';const c=process.cwd(),r=await p.realpath(c);console.log(r);process.exit(c==r?0:1)"`
- [windows - What is the difference between NTFS Junction Points and Symbolic Links? - Stack Overflow](https://stackoverflow.com/questions/9042542/what-is-the-difference-between-ntfs-junction-points-and-symbolic-links/48586946#48586946)
- [Hard Links and Junctions - Win32 apps | Microsoft Docs](https://docs.microsoft.com/en-us/windows/win32/fileio/hard-links-and-junctions)

## Require specific version of NPM and node

```sh
# update your package.json to add:
# "engines": {
# 	"npm": ">=6.6.0",
# 	"node": ">=12.0.0"
# },
npm config set engine-strict false --userconfig ./.npmrc
```

If the version doesn't match, `npm install`:

```
npm ERR! code ENOTSUP
npm ERR! notsup Unsupported engine for <package>@<version>: wanted: {"npm":">=6.6.0","node":">=12.0.0"} (current: {"node":"<current-node-version>","npm":"<current-npm-version>"})
npm ERR! notsup Not compatible with your version of node/npm: <package>@<version>
npm ERR! notsup Required: {"npm":">=6.6.0","node":">=12.0.0"}
npm ERR! notsup Actual:   {"npm":"<current-npm-version>","node":"<current-node-version>"}

npm ERR! A complete log of this run can be found in:
npm ERR!     <log-file-path>
```

Note: that doesn't work for [`npm ci`](https://github.com/npm/cli/issues/1219) that ignore that check

- [npm-config | npm Documentation](https://docs.npmjs.com/misc/config#engine-strict)
- [npm-package.json | npm Documentation](https://docs.npmjs.com/files/package.json#engines)

### Encryption with Node.js

Asynmmetric encryption usally encrypt an symectric key used to encrypt: [RSA maximum bytes to encrypt, comparison to AES in terms of security? - Information Security Stack Exchange](https://security.stackexchange.com/questions/33434/rsa-maximum-bytes-to-encrypt-comparison-to-aes-in-terms-of-security/33445#33445)

- [Asymmetric Public / Private Key Encryption (RSA) in Node.js](https://coolaj86.com/articles/asymmetric-public--private-key-encryption-in-node-js/)
- [Encrypt and decrypt content with Nodejs - chris-rock](http://lollyrock.com/articles/nodejs-encryption/) - Symetric encryption

See security [cryptography - "Diffie-Hellman Key Exchange" in plain English - Information Security Stack Exchange](https://security.stackexchange.com/questions/45963/diffie-hellman-key-exchange-in-plain-english)

### Node IPC

```js
const path = isWindows ? "\\\\.\\pipe\\myprogram" : "/tmp/myprogram";// "myprogram" or a random string
```

- [Messages and IPC in Node](http://danespringmeyer.com/node-message-passing/#tcp-server)
- [Inter-process communication - Wikipedia](https://en.wikipedia.org/wiki/Inter-process_communication)
- [Redis](https://redis.io/)
- use the net module
- [Net | Node.js v9.5.0 Documentation](https://nodejs.org/api/net.html#net_identifying_paths_for_ipc_connections)
- [javascript - What's the most efficient node.js inter-process communication library/method? - Stack Overflow](https://stackoverflow.com/questions/6463945/whats-the-most-efficient-node-js-inter-process-communication-library-method/12448328#12448328)
- [Communication between N node.js processes - Stack Overflow](https://stackoverflow.com/questions/34374730/communication-between-n-node-js-processes/34404965#34404965)
- [Performance of Inter-process Communications in Node.js | 60devs](https://60devs.com/performance-of-inter-process-communications-in-nodejs.html)

## FNM

On Windows for Bash, add to `%USERPROFILE%\.bashrc`:

```sh
# See https://github.com/Schniz/fnm/tree/master#shell-setup and https://github.com/Schniz/fnm/blob/master/docs/configuration.md
eval "$(fnm env --use-on-cd --version-file-strategy=recursive --log-level=error)"
```

`%USERPROFILE%\.bash_profile`:

```sh
if [ -s ~/.bashrc ]; then source ~/.bashrc; fi
```

On Windows for CMD:

Exec the registry script:

```reg
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Command Processor]
"AutoRun"="@%USERPROFILE%\\autorun.cmd"
```

`%USERPROFILE%\autorun.cmd`:

```cmd
@echo off
:: See https://github.com/Schniz/fnm/tree/master?tab=readme-ov-file#windows-command-prompt-aka-batch-aka-wincmd and https://github.com/Schniz/fnm/blob/master/docs/configuration.md
:: "for /f" will launch a new instance of cmd so we create a guard to prevent an infnite loop
if not defined FNM_AUTORUN_GUARD (
    set "FNM_AUTORUN_GUARD=AutorunGuard"
    for /f "tokens=*" %%z in ('fnm env --use-on-cd --version-file-strategy=recursive --log-level=error') do call %%z
)
```

To spawn process without using a shell (`node`, `npm`, `npx`), use instead something like `C:\path\to\node.cmd` with the following content:

```
@echo off
fnm use --silent-if-unchanged
node %*
```

## Max memory size

Aka `--max-old-space-size`, "FATAL ERROR: CALL_AND_RETRY_LAST Allocation failed - JavaScript heap out of memory", "EXEC : FATAL error : Ineffective mark-compacts near heap limit Allocation failed - JavaScript heap out of memory"

Increase memory to 4GB: `node --max-old-space-size=4096 index.js`. 1024 for 1GB, 1536 for 1.5GB, 2048 for 2GB, 3072 for 3GB, 5120 for 5GB, 6144 for 6GB, 7168 for 7GB, 8192 for 8GB, etc.

> It is recommended to always explicitly set the `--max-old-space-size` instead of relying on default imposed by Node.js

> On a machine with 2 GiB of memory, consider setting this to 1536 (1.5 GiB) to leave some memory for other uses and avoid swapping.
>
> — [Command-line API - --max-old-space-size=SIZE (in megabytes)](https://nodejs.org/api/cli.html#--max-old-space-sizesize-in-megabytes)

- [node.js - Where do I set 'NODE_OPTIONS="--max-old-space-size=2048"' - Stack Overflow](https://stackoverflow.com/questions/56982005/where-do-i-set-node-options-max-old-space-size-2048/64409997#64409997)
- `node --max-old-space-size=4096 "$(which npm)" install`
- `node -r ts-node/register --max-old-space-size=4096 index.ts` for running TypeScript
- `v8.getHeapStatistics().heap_size_limit` for get the max memory size inside node process
- [Finch:increase max_old_space_size to 4 GB based on availability of ph… · v8/v8@b2f75b0](https://github.com/v8/v8/commit/b2f75b008d14fd1e1ef8579c9c4d2bc7d374efd3) - changes in v8 for "Increase max size of the old space to 4 GB for x64 systems with the physical memory bigger than 16 GB" (~ Node 14)
- [memory - How do I determine the correct "max-old-space-size" for Node.js? - Stack Overflow](https://stackoverflow.com/questions/48387040/how-do-i-determine-the-correct-max-old-space-size-for-node-js/63495296#63495296)
- node <= 11: default is 1.4 GB, <= 13: 2.0 GB, >= 14 only on x64 with > 16 GB: 4.0 GB
- [A tour of V8: Garbage Collection — jayconrod.com](https://web.archive.org/web/20230301112808/https://jayconrod.com/posts/55/a-tour-of-v8-garbage-collection)

## TypeScript

- [esbuild-kit/tsx: ⚡️ TypeScript Execute (tsx): Node.js enhanced with esbuild to run TypeScript & ESM](https://github.com/esbuild-kit/tsx)
- [TypeStrong/ts-node: TypeScript execution and REPL for node.js](https://github.com/TypeStrong/ts-node#swc-1)
- [swc-project/swc-node: Faster ts-node without typecheck](https://github.com/swc-project/swc-node)

## Single executable application

> SABs are not meant for bundling dependencies

- [Single executable applications](https://nodejs.org/api/single-executable-applications.html)
- [What do we consider to be a Single Executable Application? · nodejs/single-executable · Discussion #34](https://github.com/nodejs/single-executable/discussions/34)
- [vercel/pkg: Package your Node.js project into an executable](https://github.com/vercel/pkg)
- [nexe/nexe: 🎉 create a single executable out of your node.js apps](https://github.com/nexe/nexe)
- [Compiling a Node.js Application into an .exe File | Engineering Education (EngEd) Program | Section](https://web.archive.org/web/20230604094945/https://www.section.io/engineering-education/compile-your-nodejs-application-into-a-exe-file/) - Use pkg or nexe
- [criblio/js2bin: NodeJS application to native executable](https://github.com/criblio/js2bin)

## HTTP Proxy

Node use interally the package `undici`, which parse the proxy URI with URL API for which the protocol is not optional:

```
$ HTTPS_PROXY=example.com:8081 node -e "console.log(new URL(process.env.https_proxy ?? process.env.HTTPS_PROXY))"
URL {
  href: 'example.com:8081',
  origin: 'null',
  protocol: 'example.com:',
  username: '',
  password: '',
  host: '',
  hostname: '',
  port: '',
  pathname: '8081',
  search: '',
  searchParams: URLSearchParams {},
  hash: ''
}
$ HTTPS_PROXY=https://example.com:8081 node -e "console.log(new URL(process.env.https_proxy ?? process.env.HTTPS_PROXY))"
URL {
  href: 'https://example.com:8081/',
  origin: 'https://example.com:8081',
  protocol: 'https:',
  username: '',
  password: '',
  host: 'example.com:8081',
  hostname: 'example.com',
  port: '8081',
  pathname: '/',
  search: '',
  searchParams: URLSearchParams {},
  hash: ''
}
```


> EnvHttpProxyAgent automatically reads the proxy configuration from the environment variables `http_proxy`, `https_proxy`, and `no_proxy` and sets up the proxy agents accordingly. When `http_proxy` and `https_proxy` are set, `http_proxy` is used for HTTP requests and `https_proxy` is used for HTTPS requests. If only `http_proxy` is set, `http_proxy` is used for both HTTP and HTTPS requests. If only `https_proxy` is set, it is only used for HTTPS requests.
>
> `no_proxy` is a comma or space-separated list of hostnames that should not be proxied. The list may contain leading wildcard characters (`*`). If `no_proxy` is set, the EnvHttpProxyAgent will bypass the proxy for requests to hosts that match the list. If > `no_proxy` is set to `"*"`, the EnvHttpProxyAgent will bypass the proxy for all requests.
>
> Uppercase environment variables are also supported: `HTTP_PROXY`, `HTTPS_PROXY`, and `NO_PROXY`. However, if both the lowercase and uppercase environment variables are set, the uppercase environment variables will be ignored.

Need to set full URI (not just the host and the port), eg. `HTTPS_PROXY=http://example.com:8000`

For some libraires / tools the procotol is optional and could use http or https as default protocol

- https://github.com/nodejs/node/blob/2cd385ef6714b24b62edf22dd2ddd756eee9d16b/deps/undici/src/lib/dispatcher/env-http-proxy-agent.js#L35-L47
- https://github.com/nodejs/node/blob/2cd385ef6714b24b62edf22dd2ddd756eee9d16b/deps/undici/src/docs/docs/api/EnvHttpProxyAgent.md?plain=1#L7-L11

- https://github.com/nodejs/node/blob/5ad2ca920cdc6d99a8d673724b35115fef925e78/deps/openssl/openssl/crypto/http/http_client.c#L965C17-L965C36 -> https://github.com/nodejs/node/blob/5ad2ca920cdc6d99a8d673724b35115fef925e78/deps/openssl/openssl/crypto/http/http_lib.c#L74-L84
- NPM use [proxy-agent - npm](https://www.npmjs.com/package/proxy-agent), which use [proxy-from-env](https://www.npmjs.com/package/proxy-from-env) use the request procol as default https://github.com/Rob--W/proxy-from-env/blob/095d1c26902f37a12e22bea1b8c6b67bf13fe8cd/index.js#L47-L50 ("default to the requested URL's scheme")
- curl use HTTP as default protocol ("head: It's a HTTP proxy") https://github.com/curl/curl/blob/4af40b3646d3b09f68e419f7ca866ff395d1f897/lib/url.c#L4608-L4638
- wget use HTTP as default protocol ("Just prepend "http://" to URL.") https://git.savannah.gnu.org/cgit/wget.git/tree/src/retr.c?id=93c1517c4071c4288ba5a4b038e7634e4c6b5482#n1283 https://git.savannah.gnu.org/cgit/wget.git/tree/src/url.c?id=93c1517c4071c4288ba5a4b038e7634e4c6b5482#n609
- Python's urllib use request protocol as default https://github.com/python/cpython/blob/936135bb97fe04223aa30ca6e98eac8f3ed6b349/Lib/urllib/request.py#L801-L802

See also:

- [proxy - difference between http_proxy and https_proxy - Stack Overflow](https://stackoverflow.com/questions/58559109/difference-between-http-proxy-and-https-proxy)
- [https_proxy=httpとhttps_proxy=httpsは何が違うのか？ - Qiita](https://web.archive.org/web/20220517024816/https://qiita.com/testnin2/items/1d6c0108512e7ff44ee1)
- [Set up proxy using http_proxy & https_proxy environment variable in Linux? | GoLinuxCloud](https://web.archive.org/web/20240417033221/https://www.golinuxcloud.com/set-up-proxy-http-proxy-environment-variable/)
- [http - Are HTTP_PROXY, HTTPS_PROXY and NO_PROXY environment variables standard? - Super User](https://superuser.com/questions/944958/are-http-proxy-https-proxy-and-no-proxy-environment-variables-standard)
- [Proxy environment variables - everything curl](https://everything.curl.dev/usingcurl/proxies/env.html)
- [proxy-agents/packages/proxy-agent at main · TooTallNate/proxy-agents](https://github.com/TooTallNate/proxy-agents/tree/main/packages/proxy-agent)
- [make-fetch-happen/README.md at ecd8f33c411096e8f79ae6f7043edab11ab29289 · npm/make-fetch-happen](https://github.com/npm/make-fetch-happen/blob/ecd8f33c411096e8f79ae6f7043edab11ab29289/README.md#opts-proxy)
- [x/net/http/httpproxy: document proxy authentication support · Issue #61505 · golang/go](https://github.com/golang/go/issues/61505)
