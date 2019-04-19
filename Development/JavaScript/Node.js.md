["Node.js" (written and spoken guidelines)](https://twitter.com/bitandbang/status/1087359646367731719)

- [Node.js Security Checklist | @RisingStack](https://blog.risingstack.com/node-js-security-checklist/)

## Libraries

- [NaturalIntelligence/fast-xml-parser: Validate XML, Parse XML to JS/JSON and vise versa, or parse XML to Nimn rapidly without C/C++ based libraries and no callback](https://github.com/NaturalIntelligence/fast-xml-parser) - Read and write XML with a DOM (pure JS)
	It's an alternative to [jindw/xmldom: A PURE JS W3C Standard based(XML DOM Level2 CORE) DOMParser and XMLSerializer.](https://github.com/jindw/xmldom)
- [libxmljs/libxmljs: libxml bindings for v8 javascript engine](https://github.com/libxmljs/libxmljs) - Read and write XML (native)
- [Stuk/jszip: Create, read and edit .zip files with Javascript](https://github.com/Stuk/jszip) - Read and write ZIP asynchronously
- [csstree/csstree: Fast detailed CSS parser with syntax validation](https://github.com/csstree/csstree) - Read and write CSS
- [http-auth/src at master · http-auth/http-auth](https://github.com/http-auth/http-auth/tree/master/src) - Basic and Digest HTTP Authentification (express)
- [jshttp/basic-auth: Generic basic auth Authorization header field parser](https://github.com/jshttp/basic-auth) - Basic HTTP Authentification (generic)
- [auth0/node-jsonwebtoken: JsonWebToken implementation for node.js](https://github.com/auth0/node-jsonwebtoken) - JSON Token generation and verification (for access token)
- [kelektiv/node.bcrypt.js: bcrypt for NodeJs](https://github.com/kelektiv/node.bcrypt.js) - bcrypt hash generation and verification (for password storage)
- [expressjs/session: Simple session middleware for Express](https://github.com/expressjs/session) - Handle clients sessions
- [dotenv](https://www.npmjs.com/package/dotenv) - Load environnement variable from `.env` file
- [mail-null](https://www.npmjs.com/package/mail-null) - `sleep 2 && open http://localhost:2345 & SMTP_PORT=3456 PORT=2345 ./node_modules/.bin/mail-null`
- [nodemailer](https://www.npmjs.com/package/nodemailer) - Email client

- [Server-side Libraries](https://github.com/dexteryy/spellbook-of-modern-webdev#server-side-libraries-nodejs)

## Relative path

	path.join(__dirname, "views");
	path.resolve(".")// > /path/to/dir

## List files recursively

	const path = require("path");
	const {promisify} = require("util");
	const fs = require("fs");
	const lstat = promisify(fs.lstat);
	const readdir = promisify(fs.readdir);
	// Walk directories
	const getFiles = async entry => {
		if((await lstat(entry)).isDirectory()){
			return entry;
		}
	
		const files = [];
		for(const subEntry of await readdir(entry)){
			files.push(...await getFiles(path.join(entry, subEntry)));
		}
		return files;
	};

TODO use generator function

- [List all file in a directory in Node.j recursively in a synchronou fashion](https://gist.github.com/kethinov/6658166)

## Keep local copy of dependencies

Usefull to keep it on version control system or in context of security

- https://github.com/JamieMason/shrinkpack
- https://docs.npmjs.com/cli/shrinkwrap

## Hard links to same dependencies across projects

In all `node_modules` directory on an hard drive.

- https://github.com/jeffbski/pkglink

## Turn off Spotflight indexation of dependencies

	find /path/to/projects -type d \( -name "node_modules" -o -name "bower_modules" \) -exec touch "{}/.metadata_never_index" \;

## Debug

- [Remote Debugging Node.js in Docker – SENSEI Developer Blog – Medium](https://medium.com/sensei-developer-blog/remote-debugging-node-js-in-docker-1936eb4ef522)
- [The Definitive Guide for Monitoring Node.js Applications | @RisingStack](https://blog.risingstack.com/monitoring-nodejs-applications-nodejs-at-scale/)
- [Keeping Node.js Fast: Tools, Techniques, And Tip For Making High-Performance Node.j Server — Smashing Magazine](https://www.smashingmagazine.com/2018/06/nodejs-tools-techniques-performance-servers/)

### Send log infos client side

HTTP header `X-ChromeLogger-Data: jsonbase64value`

- [Console messages - Firefox Developer Tools | MDN](https://developer.mozilla.org/en-US/docs/Tools/Web_Console/Console_messages#Server)
- [Chrome Logger - Tech Specs](https://craig.is/writing/chrome-logger/techspecs)
- [olahol/express-chrome-logger: Debug your express app using the Chrome console.](https://github.com/olahol/express-chrome-logger)
- [yannickcr/node-chromelogger: Implementation of the Chrome Logger protocol for Node.js](https://github.com/yannickcr/node-chromelogger)

## Child processes

Cluster is `child_process` in a more convenient way to listen the same port by all children (it use `child_process` internally): [Cluster | Node.j v9.6.1 Documentation](https://nodejs.org/api/cluster.html#cluster_how_it_works)

- [Node.js Child Processes: Everything you need to know](https://medium.freecodecamp.org/node-js-child-processes-everything-you-need-to-know-e69498fe970a)
- [Node.j Cluster and Express](http://rowanmanning.com/posts/node-cluster-and-express/)
- [Setting up a Node.j Cluster](http://stackabuse.com/setting-up-a-node-js-cluster/)

## Standart input / output

	const data = require("fs").readFileSync(0, {encoding: "utf-8"});// file 0 is stdin

## Command line

Shebang:

	#!/usr/bin/env node

## Express

Test server capacity with [mcollina/autocannon: fast HTTP/1.1 benchmarking tool written in Node.js](https://github.com/mcollina/autocannon)

**Order route registration from most specific to less specific: `/foo/bar`, `/foo`, `/`**

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

Internal redirect, aka reroute: [node.js - Forward request to alternate request handler instead of redirect - Stack Overflow](https://stackoverflow.com/questions/18136323/forward-request-to-alternate-request-handler-instead-of-redirect/22081112#22081112). See [Express 4.x - API Reference](http://expressjs.com/en/4x/api.html#app.METHOD)

Reroute:

	app.get("someroute", (req, res, next) => {
		// Reroute to index.html (could be handled by statics)
		req.url = "index.html";
		next("route");
	});

Global error handling

At app level or a parent route level, register the error handler (a middleware with 4 arguments) **after** all other used middleware and routes handlers

- [Express error handling](https://expressjs.com/en/guide/error-handling.html)

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

	req.ip

- `app.set('trust proxy', 'loopback')`
- [Expres 4.x - API Reference](http://expressjs.com/en/4x/api.html#app.settings.table) and [Expres 4.x - API Reference](http://expressjs.com/en/4x/api.html#trust.proxy.options.table)
- [node.j - What doe "trust proxy" actually do in express.js, and do I need to use it? - Stack Overflow](https://stackoverflow.com/questions/23413401/what-does-trust-proxy-actually-do-in-express-js-and-do-i-need-to-use-it)
- [Expres behind proxies](https://expressjs.com/en/guide/behind-proxies.html)
- [node.js - Express.js: how to get remote client addres - Stack Overflow](https://stackoverflow.com/questions/10849687/express-js-how-to-get-remote-client-address) - Responses are not correct, see the link above

## NPM

- [node.js - Difference between npm install and npm run build - Stack Overflow](https://stackoverflow.com/questions/43664200/difference-between-npm-install-and-npm-run-build)
- [`npm install` modifies `package-lock`! (changes resolved url protocol!) · Issue #20106 · npm/npm](https://github.com/npm/npm/issues/20106) - npm install issue that update `package-lock.json` by changing `https://` to `http://`. To fix it, use `rm -rf node_modules/ && npm cache clean --force && npm i`. See also [Some packages have dist.tarball as http and not https - 🐞 bugs - npm forum](https://npm.community/t/some-packages-have-dist-tarball-as-http-and-not-https/285/15)
- `NODE_OPTIONS=--max-old-space-size=4096 npm run myscript`, see [Best way to set --max-old-space-size when running npm? · Issue #12238 · npm/npm](https://github.com/npm/npm/issues/12238)

### Package variables

	{
		...
		"main": "server/index.js",
		"scripts": {
			"start": "node $npm_package_main",
			"start-dev": "NODE_ENV=dev node $npm_package_main"
		},
		...
		"engines": {
			"node": ">=9.0"
		}
	}

### Install for continuous integration

	npm ci

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

## Promisify

	import util from 'util';
	const result;
	try{
		result = await util.promisify(obj.method.bind(obj))("value1", "value2");
		console.log(result);
	}catch(error){
		console.error(error);
	}

Instead of:

	obj.method("value1", "value2", (error, result) => {
		if(error){
			console.error(error);
			return;
		}
		
		console.log(result);
	})

- [Util | Node.js v8.9.4 Documentation](https://nodejs.org/dist/latest-v8.x/docs/api/util.html#util_util_promisify_original)

## Modules

- `core-modules/module.js`
- [Requiring module in Node.js: Everything you need to know](https://medium.freecodecamp.org/requiring-modules-in-node-js-everything-you-need-to-know-e7fbd119be8)
- [Load node.j module from string in memory - Stack Overflow](https://stackoverflow.com/questions/17581830/load-node-js-module-from-string-in-memory)

## EACCES errors when installing global package

First: Just **don't install packages globally**

	npm install -g packagename

Install global with node-gyp can output errors:

	gyp WARN EACCES user "root" does not have permission to access the dev dir "/Users/username/.node-gyp/0.0.0"
	gyp WARN EACCES attempting to reinstall using temporary dev dir "/opt/local/lib/node_modules/packagename/.node-gyp"
	gyp WARN EACCES user "root" does not have permission to access the dev dir "/opt/local/lib/node_modules/packagename/.node-gyp/0.0.0"

Use `--unsafe-perm` paramter for `npm` to fix the issue, or update the `NODE_PATH` env var.

See [Warning "root" does not have permission to access the dev dir · Issue #454 · nodejs/node-gyp](https://github.com/nodejs/node-gyp/issues/454#issuecomment-155957449)

- [config | npm Documentation](https://docs.npmjs.com/misc/config#unsafe-perm)

## Parse URI as configuration

- https://github.com/sidorares/node-mysql2/blob/5f0fb8f1f5035e2c0207490aa2f0b838dc82fdc2/lib/connection_config.js#L166-L196
- https://github.com/nodemailer/nodemailer/blob/5da6c87766e258f1a5fa9b628f2d9f57c9d533ce/lib/shared/index.js#L16-L91

## Global error handling

- `process.setUncaughtExceptionCaptureCallback`

## Load balancer and reverse proxy

`process.env.IN_PASSENGER === "1"` `typeof PhusionPassenger !== "undefined"`

- [Passenger Library](https://www.phusionpassenger.com/library/) - Module for ngnix or Apache to handle configuration, deployment, reload, etc. of Node.js, Ruby, Python
- [Performance Best Practice Using Expres in Production](http://expressjs.com/en/advanced/best-practice-performance.html#use-a-reverse-proxy)
- [Understanding Passenger - Passenger + Node.j basic - Passenger Library](https://www.phusionpassenger.com/library/walkthroughs/basics/nodejs/fundamental_concepts.html)

## Node sources

- [node/lib at master · nodejs/node](https://github.com/nodejs/node/tree/master/lib)

Zlib will don't have extra gzip header fiels (empty values):

> If deflateSetHeader is not used, the default gzip header has text false, the time set to zero, and os set to 255, with no extra, name, or comment fields.
> - https://github.com/nodejs/node/blob/master/deps/zlib/zlib.h

Zlib binding:

- [node/node_zlib.cc at master · nodejs/node](https://github.com/nodejs/node/blob/master/src/node_zlib.cc)
- [node/zlib.js at master · nodejs/node](https://github.com/nodejs/node/blob/master/lib/zlib.js)
- [node/zlib.h at master · nodejs/node](https://github.com/nodejs/node/blob/master/deps/zlib/zlib.h)
