- [Develop Locally, Use Images from Production | CSS-Tricks](https://css-tricks.com/develop-locally-use-images-production/)

## Debug

- [RemoteDebug/remotedebug-ios-webkit-adapter: Debug Safari and WebViews on iOS from tools like VS Code, Chrome DevTools, Mozilla Debugger.html](https://github.com/RemoteDebug/remotedebug-ios-webkit-adapter)
- [google/ios-webkit-debug-proxy: A DevTools proxy (Chrome Remote Debugging Protocol) for iOS devices (Safari Remote Web Inspector).](https://github.com/google/ios-webkit-debug-proxy)
- [Debugging Node.js with Chrome DevTools – Medium](https://medium.com/@paul_irish/debugging-node-js-nightlies-with-chrome-devtools-7c4a1b95ae27) - `node --inspect index.js` then open the provieded URL (start with `chrome-devtools://`)
- [RemoteDebug, an initiative to unify remote debugging across browsers.](http://remotedebug.org/)

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
- http://www.gnu.org/software/make/manual/make.html
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
 
	# scripts and map
	scripts.js scripts.js.map: js-and-map
	# And
	js-and-map: scripts.js
		touch scripts.js
		touch scripts.js.map
	
	.INTERMEDIATE: js-and-map

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

	VAR="Hello $USER! This symbole '#' is a hash."

Must be escaped as:

	VAR="Hello $$USER! This symbole '\#' is a hash"

To not be considered as a comment

- [make - Anomalies: bug #712, GNU make can't handle spaces in... [Savannah]](http://savannah.gnu.org/bugs/?712)
- [shell - Can GNU make handle filenames with spaces? - Stack Overflow](https://stackoverflow.com/questions/9838384/can-gnu-make-handle-filenames-with-spaces)

### Steps `./configure && make && make install`

	./configure

tells you whether are quite ready to build the application. It will check if you have everything needed to build the application, and, if it sees any critical errors it will inform you.

	make

builds (compiles) the source code. Compiler compiles the code, but, most of the times, the code cannot stand alone, it requires external libraries (usually provided by ubuntu packages) to be installed. After this step the executable(s) of this specific application you are trying to install will be created.

	sudo make install

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

	#!/bin/sh
	while true ; do make ; sleep 1 ; done

#### watch command

	watch make

	watch -n 0.5 "make 2>&1"

- [coderwall.com : establishing geek cred since 1305712800](https://coderwall.com/p/e0kj9w/watch-for-changes-and-then-rebuild-source-code-using-make)

#### watchman

https://github.com/facebook/watchman

	brew install watchman

	sudo port install watchman

#### fswatch

https://github.com/alandipert/fswatch

	brew install fswatch

	cd /tmp && git clone https://github.com/alandipert/fswatch && cd fswatch/ && make && cp fswatch /usr/local/bin/fswatch

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

### Others

- https://github.com/ai/autoprefixer/tree/master/lib/hacks
- http://www.phpied.com/diy-source-maps/
- http://www.phpied.com/css-diff/

#### Java

http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html#javasejdk

#### Google Closure Compiler

/usr/share/java/closure-compiler.jar

##### `git && ant`

	#!/bin/bash
	mkdir closure-compiler
	cd closure-compiler
	git clone https://github.com/google/closure-compiler.git .
	ant jar
	sudo cp -f ./build/compiler.jar /opt/local/share/java/closure-compiler.jar
	cd ..
	rm -rf closure-compiler

##### Download

	#!/bin/bash
	wget -qO- -O compiler-latest.zip http://dl.google.com/closure-compiler/compiler-latest.zip
	unzip compiler-latest.zip -d compiler-latest
	cp -f compiler-latest/compiler.jar /opt/local/share/java/closure-compiler.jar
	rm -rf compiler-latest

https://github.com/google/closure-compiler
http://dl.google.com/closure-compiler/compiler-latest.zip

Homebrew
https://github.com/Homebrew/homebrew/blob/master/Library/Formula/closure-compiler.rb
https://groups.google.com/forum/#!topic/brew-test-bot/OiQ3aliyUkw
https://github.com/gmarty/grunt-closure-compiler/issues/2

Debian
https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=705565
https://packages.debian.org/source/sid/closure-compiler

#### Nailgun

Nailgun (for java)
http://www.martiansoftware.com/nailgun/
https://github.com/Homebrew/homebrew/issues/21880
https://github.com/sethp-jive/homebrew/blob/0f0a86819d8f5bd53251f263a26ae8119f88dc20/Library/Formula/nailgun.rb

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

Exist as a variant of jruby: https://trac.macports.org/ticket/20552

#### Maven