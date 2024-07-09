- [Develop Locally, Use Images from Production | CSS-Tricks](https://css-tricks.com/develop-locally-use-images-production/)
- [pozorvlak | Falsehoods programmers believe about build systems](https://pozorvlak.dreamwidth.org/174323.html)

## Debug

- [Debugging Node.js with Chrome DevTools – Medium](https://medium.com/@paul_irish/debugging-node-js-nightlies-with-chrome-devtools-7c4a1b95ae27) - `node --inspect index.js` then open the provieded URL (start with `chrome-devtools://`)
- [RemoteDebug, an initiative to unify remote debugging across browsers.](http://remotedebug.org/)
- [google/tamperchrome: Tamper Chrome is a Chrome extension that allows you to modify HTTP requests on the fly and aid on web security testing. Tamper Chrome works across all operating systems (including Chrome OS).](https://github.com/google/tamperchrome)
- [RemoteDebug Protocol Compatibility Tables](https://compatibility.remotedebug.org/)
- [RemoteDebug, an initiative to unify remote debugging across browsers.](https://remotedebug.org/adaptors/)
- [WICG/devtools-protocol: DevTools Protocol](https://github.com/WICG/devtools-protocol)
- [ChromeDevTools/awesome-chrome-devtools: Awesome tooling and resources in the Chrome DevTools & DevTools Protocol ecosystem](https://github.com/ChromeDevTools/awesome-chrome-devtools#browser-adapters)
- [Microsoft/edge-diagnostics-adapter: Microsoft Edge Diagnostics Adapter is a protocol adapter that enables tools to debug Microsoft Edge using the Chrome DevTools Protocol.](https://github.com/Microsoft/edge-diagnostics-adapter)
- [Microsoft Edge DevTools Protocol - Microsoft Edge Development | Microsoft Docs](https://docs.microsoft.com/en-us/microsoft-edge/devtools-protocol/)

### Debug webpage on remote iOS Safari

Only for Safari, or webview in application **developper version only** (installed via XCode or App for [iOS simulator](../Operating%20Systems/iOS/iOS.md#test-application))

At least works with iOS 11.4:

1. connect iOS device with a cable
2. install iTunes, because usbmuxd can't configure correcly USB devices on Windows: [ios - Why are Windows binaries of libimobiledevice dependent on iTunes? - Stack Overflow](https://stackoverflow.com/questions/48851719/why-are-windows-binaries-of-libimobiledevice-dependent-on-itunes)
3. start iTunes and allow paring (iTunes show an alert)
4. "trust this computer" (iOS show an alert). See [Apple Support page](https://support.apple.com/en-ca/HT202778)
5. install `ios-webkit-debug-proxy` (win64 release comes with libimobiledevice) [Releases · google/ios-webkit-debug-proxy](https://github.com/google/ios-webkit-debug-proxy/releases)
6. allow Web Inpsector on iOS: Settings > Safari > Advanced > Web Inspector = ON
7. start `ios_webkit_debug_proxy.exe`
8. open chrome://inspect/#devices in Chrome

- [How to build libimobiledevice on Windows? · Issue #582 · libimobiledevice/libimobiledevice](https://github.com/libimobiledevice/libimobiledevice/issues/582)
- [libimobiledevice-win32/libimobiledevice: A cross-platform protocol library to communicate with iOS devices](https://github.com/libimobiledevice-win32/libimobiledevice)
- [google/ios-webkit-debug-proxy: A DevTools proxy (Chrome Remote Debugging Protocol) for iOS devices (Safari Remote Web Inspector).](https://github.com/google/ios-webkit-debug-proxy#installation)
- [RemoteDebug/remotedebug-ios-webkit-adapter: Debug Safari and WebViews on iOS from tools like VS Code, Chrome DevTools, Mozilla Debugger.html](https://github.com/RemoteDebug/remotedebug-ios-webkit-adapter) - Not required if you use ios-webkit-debug-proxy and Chrome
- [Install Quamotion iMobileDevice for Windows — Quamotion WebDriver 0.1 documentation](http://docs.quamotion.mobi/en/latest/imobiledevice/install.html)
- [Inspect docs](https://inspectdev.notion.site/Inspect-docs-ce34803e95d04b48ac5fe1255c0c3f6f)

Install a Fiddler proxy certificate:

1. [Configure Fiddler for iOS | Progress Telerik Fiddler](https://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/ConfigureForiOS)
2. go to http://ipv4.fiddler:8888/ (update the right port Fiddler use) and click _FiddlerRoot certificate_ and install
3. **Important** Settings > General > About > Certificate Trust Settings and trust the installed root certificate (for the option : Fiddler > Tools > Options... > HTTPS > Capture HTTPS CONNECTs > Decrypt HTTPS traffic)

### Debug webpage on remote Android device

1. install Android SDK (could be [command line tools only](https://developer.android.com/studio/#command-tools)). Exemple in `%PROGRAMFILES(X86)%\Google\Android SDK`
2. install plaform tools `.\tools\bin\sdkmanager.bat "platform-tools"`. Note: if you install in "Program Files" folder, you need adminstrative rights to execute this commande, overwise you will get an error "Failed to read or create install properties file" or "Warning: File C:\Users\XXXXX\.android\repositories.cfg could not be loaded."
3. enable USB Debugging on the smartphone
4. `.\platform-tools\adb devices`
5. if needed, install USB drivers
6. open `chrome://inspect/` with Chrome (or in DevTools > Menu "Customize and Control DevTools" > More Tools > Remove devices)

- [Chrome DevTools Devices does not detect device when plugged in - Stack Overflow](https://stackoverflow.com/questions/21925992/chrome-devtools-devices-does-not-detect-device-when-plugged-in/22028058#22028058)
- [sdkmanager  |  Android Developers](https://developer.android.com/studio/command-line/sdkmanager)
- [Get Started with Remote Debugging Android Devices  |  Tools for Web Developers  |  Google Developers](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
- [Start the emulator from the command line  |  Android Developers](https://developer.android.com/studio/run/emulator-commandline)
- [How can I install the GUI android SDK manager without installing Android Studio - Stack Overflow](https://stackoverflow.com/questions/43685301/how-can-i-install-the-gui-android-sdk-manager-without-installing-android-studio/51429889#51429889)
- [Is GUI for Android SDK manager gone? - Stack Overflow](https://stackoverflow.com/questions/41407396/is-gui-for-android-sdk-manager-gone)
- [WebView docs (go/webview-docs) - Net debugging in WebView](https://chromium.googlesource.com/chromium/src/+/HEAD/android_webview/docs/net-debugging.md)

Android Emulator:

- [Download Android Studio and SDK tools  |  Android Developers](https://developer.android.com/studio#cmdline-tools) - "Command line tools only"
- [How to update Android emulator without Android Studio? - Stack Overflow](https://stackoverflow.com/questions/43147699/how-to-update-android-emulator-without-android-studio/43148199#43148199)
- [Releases · intel/haxm](https://github.com/intel/haxm/releases)
- [Paste text on Android Emulator - Stack Overflow](https://stackoverflow.com/questions/3391160/paste-text-on-android-emulator/16618811#16618811)
- [Use modified hosts file on Android Emulator – Code, Procedure and Rants – Medium](https://medium.com/code-procedure-and-rants/use-modified-hosts-file-on-android-emulator-4f29f5d12ac1)
- [android - Why is the intel x86 emulator accelerator (HAXM installer) is showing not compatible with windows? - Stack Overflow](https://stackoverflow.com/questions/41408552/why-is-the-intel-x86-emulator-accelerator-haxm-installer-is-showing-not-compat/43656782#43656782) (activate virtualization - Intel® VT-x - in the BIOS then install HAXM)

### Debug cookie written by JS

Add a debugger breakpoint when a cookie is written.

```js
const desc = Object.getOwnPropertyDescriptor(Document.prototype, "cookie");// Object.getPrototypeOf(Object.getPrototypeOf(document);
Object.defineProperty(document, "cookie", {...desc, set(...args) {debugger;return desc.set.apply(this, args);}});
```

See also

- [Network features reference  |  Chrome DevTools  |  Chrome for Developers](https://developer.chrome.com/docs/devtools/network/reference?hl=en#filter-by-property) - DevTools filter `cookie-name:`

## Console

- [console.delight – Frontend Masters Boost](https://web.archive.org/web/20240226194603/https://frontendmasters.com/blog/console-delight/#b456d489-1a38-4839-b543-b60424b8b4c6-link)

## Tools & Workflow

Export, Packing, Application packer (simple app/site vs. complexe app/site)

### Tasks

- generate output: HTML, CSS, JS, JSON, Image
- include/inject
- loose bits:
	- minification (optimize/reduce without require reverse operation)
		- use progressive images
		- remove unessary data (duplicates, unused), tags, selectors

- compact/compress (require processing to recover operable state): pre-gzip

- http://incident57.com/codekit/
- http://hammerformac.com/
- http://alphapixels.com/prepros/
- http://yeoman.io/
- [Grunt](http://gruntjs.com/configuring-tasks)
- https://speakerdeck.com/addyosmani/automating-front-end-workflow
- [Package Webproject with `make`]()
- http://www.nofluffjuststuff.com/blog/eric_wendelin/2011/08/continuous_integration_for_javascript

### NPM

	npm shrinkwrap && shrinkpack

	npm install someModule --ignore-scripts

- [shrinkwrap | npm Documentation](https://docs.npmjs.com/cli/shrinkwrap)
- https://www.npmjs.com/package/shrinkpack
- [Vulnerability Note VU#319816 - npm fails to restrict the actions of malicious npm packages](https://www.kb.cert.org/vuls/id/319816)

### Transcode

### Package

- https://github.com/rollup/rollup

## Package with `ninja`

- [Ninja, a small build system with a focus on speed](http://martine.github.io/ninja/)

## Build with `cmake`

- https://github.com/kogmbh/ViewerJS/blob/master/CMakeLists.txt
- https://github.com/markand/cmake-modules/blob/master/FindNode.cmake
- https://github.com/kogmbh/WebODF/blob/master/webodf/CMakeLists.txt
- [The Kitware Blog - CMake: building with all your cores](http://www.kitware.com/blog/home/post/434)
- https://stackoverflow.com/questions/11524481/minify-css-and-javascripts-files-before-packing-into-zip-using-cmake

## Build with `make`

- [.mobo — Se passer de Grunt/Gulp/Brunch/Broccoli/Mimosa/Jake grâce à Make](http://dotmobo.github.io/makefile-frontend.html)
- [GNU make](https://www.gnu.org/software/make/manual/make.html)
- https://algorithms.rdio.com/post/make/
- http://www.vittoriozaccaria.net/wmake/#make https://github.com/vzaccaria/make4web/blob/master/makefile.mk
- https://stackoverflow.com/questions/8385359/compile-all-less-file-using-a-makefile
- http://blog.yjl.im/2013/03/using-makefile-to-minify-and-switch.html
- http://blogs.mpr.org/developer/2014/02/makefile/
- http://nefariousdesigns.co.uk/website-builds-using-make.html
- [Simple makefile to minify CSS and JS - wonko.com](http://wonko.com/post/simple-makefile-to-minify-css-and-js)
- http://en.wikipedia.org/wiki/Make_(software)
- https://stackoverflow.com/questions/1079832/how-can-i-configure-my-makefile-for-debug-and-release-builds
- [Building Web Applications With Make – Smashing Magazine](http://www.smashingmagazine.com/2015/10/building-web-applications-with-make/)
- [Making the case for make | Shape Shed](http://shapeshed.com/making-the-case-for-make/)

Examples:

- [Makefile](https://gist.github.com/joho/7297517)
- https://github.com/es-shims/es-shim-api/blob/master/Makefile
- https://github.com/const-io/numeric-constants/blob/master/Makefile

 ```make
# scripts and map
scripts.js scripts.js.map: js-and-map
# And
js-and-map: scripts.js
	touch scripts.js
	touch scripts.js.map

.INTERMEDIATE: js-and-map
```

Few notes:

- [Recursive Make Considered Harmful](http://miller.emu.id.au/pmiller/books/rmch/)

Use make

#### Pro

- c'est une roue, pas besoin qu'elle soit réinventée
- n'intègre pas de package manager, quelques doit l'outils certain dépendances / outils (imagemagick, PHP, python, ruby, etc.) nécessitent d'être installés séparément (à la main ou via des package manager comme port, apt-get, composer, npm, gem, etc.)
- can be multicore task (use the parameter `-j`)

#### Cons

- can't handle space in paths
- http://www.conifersystems.com/whitepapers/gnu-make/
- plusieurs versions existent
- plutôt UNIX

Escape some chars:

```sh
VAR="Hello $USER! This symbole '#' is a hash."
```

Must be escaped as:

```sh
VAR="Hello $$USER! This symbole '\#' is a hash"
```

To not be considered as a comment

- [make - Anomalies: bug #712, GNU make can't handle spaces in... [Savannah]](http://savannah.gnu.org/bugs/?712)
- [shell - Can GNU make handle filenames with spaces? - Stack Overflow](https://stackoverflow.com/questions/9838384/can-gnu-make-handle-filenames-with-spaces)

### Steps `./configure && make && make install`

```sh
./configure
```

tells you whether are quite ready to build the application. It will check if you have everything needed to build the application, and, if it sees any critical errors it will inform you.

```sh
make
```

builds (compiles) the source code. Compiler compiles the code, but, most of the times, the code cannot stand alone, it requires external libraries (usually provided by ubuntu packages) to be installed. After this step the executable(s) of this specific application you are trying to install will be created.

```sh
sudo make install
```

moves all the needed for the application files to the appropriate system directories. This has to be done after make because the executables of the application have been created and can be moved to the appropriate system directory (e.g. /usr/bin/) for later use.

Libraries are necessary, because they allow a programmer to use code made by other people to achieve certain things. i.e. if I wanted to do some disk formatting in my program, I could use the libs someone already wrote to do the formatting, and I just have to make my program call those libraries. If that person finds an issue in their library, they can fix it, and it will fix it in my program too. This is how open-source software can be written so fast and be so stable.

http://askubuntu.com/questions/173088/what-does-configure-make-make-install-do

### When files changes

Continuous integration

- [automation - Do something when a file is changed - Super User](http://superuser.com/questions/416846/do-something-when-a-file-is-changed)
- [makefile - Is there a smarter alternative to "watch make"? - Stack Overflow](https://stackoverflow.com/questions/7539563/is-there-a-smarter-alternative-to-watch-make)
- http://superuser.com/questions/181517/how-to-execute-a-command-whenever-a-file-changes
- https://stackoverflow.com/questions/1515730/is-there-a-command-like-watch-or-inotifywait-on-the-mac
- http://andries.filmer.nl/kb/Monitoring-file-system-events-with-inotify,-incron-and-authctl/129
- [The Refresh CSS Bookmarklet -or- How to iterate quickly when debugging CSS - Paul Irish](https://www.paulirish.com/2008/how-to-iterate-quickly-when-debugging-css/)

#### Bash script

```sh
#!/bin/sh
while true ; do make ; sleep 1 ; done
```

#### watch command

```sh
watch make
```

```sh
watch -n 0.5 "make 2>&1"
```

- [coderwall.com : establishing geek cred since 1305712800](https://coderwall.com/p/e0kj9w/watch-for-changes-and-then-rebuild-source-code-using-make)

#### watchman

https://github.com/facebook/watchman

```sh
brew install watchman
```

```sh
sudo port install watchman
```

#### fswatch

https://github.com/alandipert/fswatch

```sh
brew install fswatch
```

```sh
cd /tmp && git clone https://github.com/alandipert/fswatch && cd fswatch/ && make && cp fswatch /usr/local/bin/fswatch
```

#### inotifywait

Via `inotify-tools` package

Only available on LINUX

- http://liquidat.wordpress.com/2013/11/14/howto-acting-on-inotify-events-in-a-shell-with-inotifywait/
- http://blog.lagentz.com/general/automate-your-shell-scripts-using-inotify-and-inotifywait/
- https://stackoverflow.com/questions/18289449/how-to-get-recursive-directory-path-using-inotify-tools-in-terminal
- https://stackoverflow.com/questions/tagged/inotify-tools
- http://xaroumenosloukoumas.wordpress.com/2011/01/28/watching-directories-for-file-changes-with-inotifywait/

### Filename with spaces

Make generaly don't handle filename with space (spaces used as separators)

- Use quotes when it's possible
- `touch $(subst \,\\,$@)`

- http://www.cmcrossroads.com/article/gnu-make-meets-file-names-spaces-them?page=0%2C2
- https://stackoverflow.com/questions/9838384/can-gnu-make-handle-filenames-with-spaces

### Dependencies

## Others

- https://github.com/ai/autoprefixer/tree/master/lib/hacks
- http://www.phpied.com/diy-source-maps/
- http://www.phpied.com/css-diff/

### Java

http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html#javasejdk

### Google Closure Compiler

`/usr/share/java/closure-compiler.jar`

Externs:

```js
// ==ClosureCompiler==
// @output_file_name default.js
// @compilation_level ADVANCED_OPTIMIZATIONS
// @js_externs window.sas = {}
// @js_externs window.sas.setup = function(config){config.networkid;config.domain}
// ==/ClosureCompiler==
window.sas;
sas.setup({networkid: 0, domain: 0})
```

- [Advanced Compilation and Extern  |  Closure Compiler  |  Google Developers](https://developers.google.com/closure/compiler/docs/api-tutorial3#externs)
- [Advanced Compilation and Extern  |  Closure Compiler  |  Google Developers](https://developers.google.com/closure/compiler/docs/api-tutorial3#howto-api)

#### `git && ant`

```sh
#!/bin/bash
mkdir closure-compiler
cd closure-compiler
git clone https://github.com/google/closure-compiler.git .
ant jar
sudo cp -f ./build/compiler.jar /opt/local/share/java/closure-compiler.jar
cd ..
rm -rf closure-compiler
```

#### Download

```sh
#!/bin/bash
wget -qO- -O compiler-latest.zip http://dl.google.com/closure-compiler/compiler-latest.zip
unzip compiler-latest.zip -d compiler-latest
cp -f compiler-latest/compiler.jar /opt/local/share/java/closure-compiler.jar
rm -rf compiler-latest
```

https://github.com/google/closure-compiler
http://dl.google.com/closure-compiler/compiler-latest.zip

Homebrew
https://github.com/Homebrew/homebrew/blob/master/Library/Formula/closure-compiler.rb
https://groups.google.com/forum/#!topic/brew-test-bot/OiQ3aliyUkw
https://github.com/gmarty/grunt-closure-compiler/issues/2

Debian
https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=705565
https://packages.debian.org/source/sid/closure-compiler

### Nailgun

Nailgun (for java)
http://www.martiansoftware.com/nailgun/
https://github.com/Homebrew/homebrew/issues/21880
https://github.com/sethp-jive/homebrew/blob/0f0a86819d8f5bd53251f263a26ae8119f88dc20/Library/Formula/nailgun.rb

```sh
#!/bin/bash
# Server (java)
sudo wget -qO- -O /opt/local/share/java/nailgun.jar http://central.maven.org/maven2/com/martiansoftware/nailgun-server/0.9.1/nailgun-server-0.9.1.jar
# Client (c)
mkdir nailgun-client
cd nailgun-client
git clone https://github.com/martylamb/nailgun.git .
# Will install ng in /usr/local/bin/ng
sudo make install
cd ..
rm -rf nailgun-client
```

Exist as a variant of jruby: https://trac.macports.org/ticket/20552

## Bundling

- [Modern web apps without JavaScript bundling or transpiling](https://world.hey.com/dhh/modern-web-apps-without-javascript-bundling-or-transpiling-a20f2755)
- [Webpack](#webpack)

## Webpack

- [How webpack works - sokra](https://github.com/sokra/slides/blob/master/data/how-webpack-works.pdf)

Webpack use enhanced-resolve

- [enhanced-resolve/ResolverFactory.js at 5c1495a947060cf11106abc325b8adf1a0eff9b1 · webpack/enhanced-resolve](https://github.com/webpack/enhanced-resolve/blob/5c1495a947060cf11106abc325b8adf1a0eff9b1/lib/ResolverFactory.js#L160-L173)
- [API - Document When a Plugin Should Call `doResolve()` · Issue #1458 · webpack/webpack.js.org](https://github.com/webpack/webpack.js.org/issues/1458) - webpack resolver waterfall/sequential of resolution
- [rename-loader - npm](https://www.npmjs.com/package/rename-loader)
- [shaketbaby/directory-named-webpack-plugin: A Webpack plugin that treats a file with the name of directory as the index file](https://github.com/shaketbaby/directory-named-webpack-plugin)

Import a file that is not in the filesystem:

- data URI, or loader without resource but with [inline matchResource](https://webpack.js.org/api/loaders/#inline-matchresource)
- [v5 module dep invalidation not working in cases that do in v4 · Issue #11074 · webpack/webpack](https://github.com/webpack/webpack/issues/11074#issuecomment-648658214)
- use a custom scheme [reactjs - Module build failed: UnhandledSchemeError: Reading from "alias:/path" is not handled by plugins (Unhandled scheme) - Stack Overflow](https://stackoverflow.com/questions/66278241/module-build-failed-unhandledschemeerror-reading-from-alias-path-is-not-han)

Loaders:

- Loader rule/condition: `resourceQuery` (match the resource query string), `issuer` (parent resource)
- [Loaders | webpack](https://webpack.js.org/loaders/) and [list of loaders · webpack/docs Wiki](https://github.com/webpack/docs/wiki/list-of-loaders)

Other:

- [javascript - How to import library which is not module in webpack - Stack Overflow](https://stackoverflow.com/questions/50176740/how-to-import-library-which-is-not-module-in-webpack/51360811#51360811)
- [Plugins | webpack](https://webpack.js.org/plugins/) and [list of plugins · webpack/docs Wiki](https://github.com/webpack/docs/wiki/list-of-plugins)
- [scinos/webpack-plugin-hash-output: Plugin to replace webpack chunkhash with an md5 hash of the final file conent.](https://github.com/scinos/webpack-plugin-hash-output)

## Puppeteer

See also [playwright](https://github.com/microsoft/playwright)

- [puppeteer/examples at master · GoogleChrome/puppeteer](https://github.com/GoogleChrome/puppeteer/tree/master/examples)
- [Migrating from Puppeteer to Playwright | Checkly](https://web.archive.org/web/20211116174819/https://www.checklyhq.com/guides/puppeteer-to-playwright/)

### Update DOM objects

```js
page.evaluateOnNewDocument(() => {
	// Return fake languages preferences
	Object.defineProperty(navigator, "languages", {
	  get: function() {
		return ["en-US", "en", "bn"];
	  }
	});
});
```

```js
page.evaluateOnNewDocument(() => {
	// Return fake list of plugins
	const mimetype = Object.create(MimeType.prototype, {
		description: {value: "Portable Document Format"},
		suffixes: {value: "pdf"},
		type: {value: "application/x-google-chrome-pdf"},
	});
	const plugin = Object.create(Plugin.prototype, {
		description: {value: "Portable Document Format"},
		filename: {value: "internal-pdf-viewer"},
		length: {value: 1},
		name: {value: "Chrome PDF Plugin"},
		[mimetype.type]: {value: mimetype},
		0: {value: mimetype},
	});
	Object.defineProperty(mimetype, "enabledPlugin", {value: plugin});

	const pluginsArray = Object.create(PluginArray.prototype, {
		0: {value: plugin},
		[plugin.name]: {value: plugin},
		length: {value: 1},
	});

	// Fix item/namedItem listing
	for(const [{prototype}, type] of [[PluginArray, Plugin], [Plugin, MimeType]]){
		Object.defineProperties(prototype, {
			item: {value: function item(index){
				index = parseInt(index);
				return !isNaN(index) && this[index] instanceof type ? this[index] : null;
			}},
			namedItem: {value: function namedItem(name){
				return this[name] instanceof type ? this[name] : null;
			}},
		});
	}

	// TODO:
	// - implement iterator protocol on plugin array
	// - set correctly object properties descriptions (enumerable, configurable)
	// - set correctly function toString() -> "function namedItem() { [native code] }"
	Object.defineProperty(navigator, "plugins", {
		configurable: true,
		enumerable: true,
		get: function plugins() {
			return pluginsArray;
		}
	});
});
```

- [puppeteer/api.md at master · GoogleChrome/puppeteer](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#pageevaluateonnewdocumentpagefunction-args)

### Get page metrics

```js
await page.goto(url, {waitUntil: 'load'});
const performance = JSON.parse(await page.evaluate(() => performance.toJSON()));
```

```js
await this._client.send('Performance.enable');
const metrics = await page._client.send('Performance.getMetrics');
```

- [How can we get response time? Page metrics doesn't have it. · Issue #1368 · GoogleChrome/puppeteer](https://github.com/GoogleChrome/puppeteer/issues/1368#issuecomment-343866624)
- [puppeteer/api.md at master · GoogleChrome/puppeteer](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#pagemetrics)

### Get cookies

Get only first party cookies (see https://stackoverflow.com/questions/50252943/puppeteer-get-3rd-party-cookies):

```js
const cookies = await page.cookies();// gives only first party cookies
```

To get all (first and third) parties cookies, we need to use Dev Tools protocol (low level)

```js
const {cookies} = await page._client.send('Network.getAllCookies');
```

### Listen page events

Use an exposed function ([`Page.exposeFunction()`](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#pageexposefunctionname-puppeteerfunction))

- [javascript - Puppeteer: How to listen to object events - Stack Overflow](https://stackoverflow.com/questions/47107465/puppeteer-how-to-listen-to-object-events/56173142#56173142)
- [puppeteer/custom-event.js at master · GoogleChrome/puppeteer](https://github.com/GoogleChrome/puppeteer/blob/master/examples/custom-event.js)

## Extending tools

### Extending ESLint

Aka write a plugin for ESLint

- [javascript - How to forbid a specific named function with ESlint - Stack Overflow](https://stackoverflow.com/questions/40977713/how-to-forbid-a-specific-named-function-with-eslint/40979625#40979625)

### Extending Prettier

Aka write a plugin for Prettier

TODO

### Extending Babel

Aka write a plugin for Babel

TODO

### Extending webpack

Aka write a plugin for webpack, write a loader for webpack

- [Writing a Plugin | webpack](https://webpack.js.org/contribute/writing-a-plugin/#root)
- [Writing a Loader | webpack](https://webpack.js.org/contribute/writing-a-loader/)
