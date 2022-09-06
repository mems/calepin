- goal
- prerequise
- target
- recipe

Make parse and execute. But not dynamically all makefile code is resolved before executed (no control of recipes "at the time of execution")

- `$@`: target
- `$<`: first prerequise
- `$^`: all prerequises (space separated)
- `$(@D)`: `$(basname)`
- `$(@F)`: `$(notdir $@)`

- [GNU make: Automatic Variables](https://www.gnu.org/software/make/manual/html_node/Automatic-Variables.html#Automatic-Variables)
- [GNU make: Name Index](https://www.gnu.org/software/make/manual/html_node/Name-Index.html#Name-Index)

`@:` it's a no-op (for recipe)

- [gnu make - What does @: (at symbol colon) mean in a Makefile? - Stack Overflow](https://stackoverflow.com/questions/8610799/what-does-at-symbol-colon-mean-in-a-makefile)

```makefile
$(addsuffix /path/%.png,image1 image2)
$(patsubst %.svg,%.png,image1.svg image2.svg)
```

Get files (if file exist):

```makefile
FILES := $(shell [ -d /tmp ] && find /tmp -type f \( -name "*.png" -o -name "*.png.tmp" \))
```

- [What’s Wrong With GNU make? - Conifer Systems](http://www.conifersystems.com/whitepapers/gnu-make/)
- [Troubles of using GNU Make « kmod's blog](http://blog.kevmod.com/2014/03/troubles-of-using-gnu-make/)
- [Makepp Cookbook — The best way to set up makefiles for various situations](http://makepp.sourceforge.net/2.0/makepp_cookbook.html)

See also

- [gnu make - How to get current relative directory of your Makefile? - Stack Overflow](https://stackoverflow.com/questions/18136918/how-to-get-current-relative-directory-of-your-makefile)
- [John Graham-Cumming: What Makefile am I in?](http://blog.jgc.org/2007/01/what-makefile-am-i-in.html)
- [shell - Force Makefile to execute script after building any target (just before exiting) - Stack Overflow](https://stackoverflow.com/questions/20582006/force-makefile-to-execute-script-after-building-any-target-just-before-exiting)

## Goals

```makefiles
```

- [GNU make: Phony Targets](https://www.gnu.org/software/make/manual/html_node/Phony-Targets.html)

Put first:

```makefile
.PHONY: help
help:
	@echo "Please use \`make <target>' where <target> is one of"
	@echo "  clean      to clean generated files"
	@echo "  install    to install binaries"
	@echo "  test       to run all tests"
```

### Common goals

- `all`
- `clean`
- `install`
- `dist`
- `test`

- [GNU make: Goals](https://www.gnu.org/software/make/manual/html_node/Goals.html#Goals)

## Platform specificities

**Note: Makefile don't support indentation cause the following snippet hard to read**

```makefile
	ifeq (Windows_NT,$(OS))
CCFLAGS += -D WIN32
ifeq (AMD64,$(PROCESSOR_ARCHITEW6432))
CCFLAGS += -D AMD64
else
ifeq (AMD64,$(PROCESSOR_ARCHITECTURE))
CCFLAGS += -D AMD64
endif
ifeq (x86,$(PROCESSOR_ARCHITECTURE))
CCFLAGS += -D IA32
endif
endif
else
UNAME_S := $(shell uname -s)
ifeq (Linux,$(UNAME_S))
CCFLAGS += -D LINUX
endif
ifeq (Darwin,$(UNAME_S))
CCFLAGS += -D OSX
endif
UNAME_P := $(shell uname -p)
ifeq (x86_64,$(UNAME_P))
CCFLAGS += -D AMD64
endif
ifneq (,$(filter %86,$(UNAME_P)))
CCFLAGS += -D IA32
endif
ifneq (,$(filter arm%,$(UNAME_P)))
CCFLAGS += -D ARM
endif
endif
```

- [os agnostic - OS detecting makefile - Stack Overflow](https://stackoverflow.com/questions/714100/os-detecting-makefile/12099167#12099167)
- [Sebastien Kramm: Writing portable makefiles](http://skramm.blogspot.fr/2013/04/writing-portable-makefiles.html)

## Debug

Debug targets, dependencies, etc. `make target --debug=b`

## Test availablility of third party program

```makefile
CONVERT := convert
ifeq (, $(shell command -v $(CONVERT) 2> /dev/null))
$(error "ImageMagick is not found. Install it via 'sudo brew install imagemagick', 'sudo port install ImageMagick', 'sudo apt-get install imagemagick' or from http://imagemagick.org/script/binary-releases.php.")
endif
```

- [Command line - Find the location of a command](Command line (Unix)#find-the-location-of-a-command)
- [gnu make - Check if a program exists from a Makefile - Stack Overflow](https://stackoverflow.com/questions/5618615/check-if-a-program-exists-from-a-makefile)

## Generic

```makefile
files = foo.md bar.md
```

```makefile
$(files): %.md: %.txt
	 cat $< > $@
```

- [GNU make: Static Usage](https://www.gnu.org/software/make/manual/html_node/Static-Usage.html#Static-Usage)

## Error in recipe

```makefile
clean:
	-rm -f *.o
```

- [GNU make](https://www.gnu.org/software/make/manual/make.html#Errors)

## Escape

In rule `$$i` will be `$i` in sh.

- [GNU make: Variables in Recipes](https://www.gnu.org/software/make/manual/html_node/Variables-in-Recipes.html#Variables-in-Recipes)

## Rule output multiple files

Useful when the result of a command create multiple files

```makefile
all: foo-new.txt bar-new.txt
```

```makefile
foo-new.txt bar-new.txt: bundle
.INTERMEDIATE: bundle
bundle: foo.txt bar.txt
	cat foo.txt > foo-new.txt
	cat bar.txt > bar-new.txt
```

To fix parallel problem, use `.SECONDARY` instead.

Each time on or both foo.txt or bar.txt will be changed, or each time on or both foo-new.txt or bar-new.txt missing `bundle` will be remade

- [automake: Multiple Outputs](http://www.gnu.org/software/automake/manual/html_node/Multiple-Outputs.html#Multiple-Outputs)
- [GNU Makefile rule generating a few targets from a single source file - Stack Overflow](https://stackoverflow.com/questions/2973445/gnu-makefile-rule-generating-a-few-targets-from-a-single-source-file)
- [wildcard - GNU Makefile: multiple outputs from single rule + preventing intermediate files from being deleted - Stack Overflow](https://stackoverflow.com/questions/3046117/gnu-makefile-multiple-outputs-from-single-rule-preventing-intermediate-files)
- [GNU make](https://www.gnu.org/software/make/manual/make.html#Pattern-Examples)

Or use pattern rule


```makefile
# Create both .c and .h from .y
%.tab.c %.tab.h: %.y
	bison -d $<
```

An other technique is to use an intermediary file to keep track changes.

- use a folder as prerequisite : because "a directory is considered "changed" whenever directory members are added or removed"
- `echo 'content' | cmp -s - $@ || echo 'content' > $@` where `$@` is the tracking file contains timestamp of files and `content` is list of file in folder using `date -r <file> +"%s%N"`

	```sh
#!/usr/bin/env bash
# Write index of folder content timestamps, only if timestamps has been changed or a file has been removed
# Usage: $0 <folder> <timestampsindex>
timestamps=""
if [ -d "$1" ]; then
	timestamps=`find $1 -type f -exec date -r '{}' +"%s%N" \;`
fi
echo -n $timestamps | cmp -s - $2 || echo -n $timestamps > $2
```
- Create a TAR file of outputed files

What about a broken state:
In this case, it's usefull to use `.DELETE_ON_ERROR:` (somewhere in Makefile). See [GNU make: Errors](https://www.gnu.org/software/make/manual/html_node/Errors.html) and [GNU make: Special Targets](https://www.gnu.org/software/make/manual/html_node/Special-Targets.html). But this not work for directories: [make - Bugs: bug #16372, .DELETE_ON_ERROR does not delete directories \[Savannah\]](http://savannah.gnu.org/bugs/?func=detailitem&item_id=16372)
Else touch the target to be older that its prerequisite to force regeneration

Not related [Makefile rule depend on directory content changes - Stack Overflow](https://stackoverflow.com/questions/25005637/makefile-rule-depend-on-directory-content-changes)

## Create a temporary folder for a rule

Create it full script:

```makefile
out.tar:
   set -e ;\
   TMP=$$(mktemp -d) ;\
   echo hi $$TMP/hi.txt ;\
   tar -C $$TMP cf $@ . ;\
   rm -rf $$TMP ;\
```

- [makefile - Define make variable at rule execution time - Stack Overflow](https://stackoverflow.com/questions/1909188/define-make-variable-at-rule-execution-time)

## Multiple rules using same recipe

```makefile
# Recipe content for make a JS bundle
define COPY
mkdir -p $$(dirname $@)
cp $< $@
endef

test/foo.txt: foo.txt
	$(COPY)

test/bar.txt: bar.txt
	$(COPY)
```

- [GNU make: Canned Recipes](https://www.gnu.org/software/make/manual/html_node/Canned-Recipes.html#Canned-Recipes)

## (Re)define specific variable for rule

```makefile
CONTENT = "foo"

foo.txt:
	echo $(CONTENT) > $@

bar.txt: CONTENT = "bar"
bar.txt:
	echo $(CONTENT) > $@
```

> Be aware that a given prerequisite will only be built once per invocation of make, at most. If the same file is a prerequisite of multiple targets, and each of those targets has a different value for the same target-specific variable, then the first target to be built will cause that prerequisite to be built and the prerequisite will inherit the target-specific value from the first target. It will ignore the target-specific values from any other targets.

- [GNU make: Target-specific](https://www.gnu.org/software/make/manual/html_node/Target_002dspecific.html#Target_002dspecific)

## Self calling

```makefile
# on top
MAKEFILE_MAIN := $(lastword $(MAKEFILE_LIST))

test :
	...
	@$(MAKE) -f $(MAKEFILE_MAIN) runtest --no-print-directory
```

- `--no-print-directory`` skip logs `make[1]: Entering directory `/working/dir/path/'`, can be defined globaly with `MAKEFLAGS += --no-print-directory`
- leading `@` is used to not log the current command

Could be use full if a recipe generate an unknow amount of file could be prerequisites

- [GNU make: Special Variables](https://www.gnu.org/software/make/manual/html_node/Special-Variables.html#index-makefiles_002c-and-MAKEFILE_005fLIST-variable)
- [GNU make: MAKE Variable](https://www.gnu.org/software/make/manual/html_node/MAKE-Variable.html)
- [GNU make: Recursion](https://www.gnu.org/software/make/manual/html_node/Recursion.html)

## Spaces in path

Folder or filename

Possible workarounds:

1. don't use spaces
2. use symlinks
3. use encoding, replace space with other chars like `%20` (encode `%` too): `$(subst \ ,%20,$(subst %,%25,$1))` then `$(subst %25,%,$(subst \ ,%20,$1))`

- [c++ - white space and makefile - Stack Overflow](https://stackoverflow.com/questions/9514920/white-space-and-makefile)
- [shell - Can GNU make handle filenames with spaces? - Stack Overflow](https://stackoverflow.com/questions/9838384/can-gnu-make-handle-filenames-with-spaces)
- [How do I handle files with spaces in my Makefile? - Stack Overflow](https://stackoverflow.com/questions/17965806/how-do-i-handle-files-with-spaces-in-my-makefile)

## Double colon

Multiple recipe for same target, all will be executed (It's not the case with simple colon)

```makefile
libxxx.a : sub1.o sub2.o
	ar rv libxxx.a sub1.o
	ar rv libxxx.a sub2.o
```

Is the same as:

```makefile
libxxx.a :: sub1.o
	ar rv libxxx.a sub1.o

libxxx.a :: sub2.o
	ar rv libxxx.a sub2.o
```

Can be usefull for parallelization

- [makefile - Parallelization of recursive jobs in GNU make - Stack Overflow](https://stackoverflow.com/questions/1681006/parallelization-of-recursive-jobs-in-gnu-make/1681123#1681123)
- [gnu make - What are double-colon rules in a Makefile for? - Stack Overflow](https://stackoverflow.com/questions/7891097/what-are-double-colon-rules-in-a-makefile-for)

## Parallelization

With make option `-j 4`. It's not recommanded to use `-j` without job limitation (eat lot of CPU and RAM)

- [makefile - Parallelization of recursive jobs in GNU make - Stack Overflow](https://stackoverflow.com/questions/1681006/parallelization-of-recursive-jobs-in-gnu-make)
- [parallel processing - How can I write a makefile to auto-detect and parallelize the build with GNU Make? - Stack Overflow](https://stackoverflow.com/questions/2527496/how-can-i-write-a-makefile-to-auto-detect-and-parallelize-the-build-with-gnu-mak)
- [parallel processing - Makefile: Automatically setting jobs (-j) flag for a multicore machine? - Stack Overflow](https://stackoverflow.com/questions/4778389/makefile-automatically-setting-jobs-j-flag-for-a-multicore-machine?noredirect=1&lq=1)
- Variable `MAKEFLAGS`

## Order only prerequiest

Be sure a "bootstrap" target is executed before. Not prerequist, but need to be executed before (like `mkdir -p $@`)

When order-only prerequisite are rebuild make does not mark target as needing an update (don't base on timestamp, only if exist) like a dir

```makefile
foo: x y z | bar
	$(MAKE) $^;
	# Make will run the bar rule before this `foo`. `bar` will not appear in $^
```

- [makefile - Order-only prerequisites not working correctly in GNU make? - Stack Overflow](https://stackoverflow.com/questions/24821611/order-only-prerequisites-not-working-correctly-in-gnu-make)
- [GNU make](http://www.gnu.org/software/make/manual/make.html#Prerequisite-Types)

## Pattern rules

```makefile
%.o: %.c
	#do it
```

```makefile
$(objects): %.o: %.c
	#do it
```

- [GNU make: Static Usage](https://www.gnu.org/software/make/manual/html_node/Static-Usage.html#Static-Usage)

## Common patterns

Implicit rules

```makefile
# Copy src file to dist
dist/%: src/%
	mkdir -p $$(dirname $@)
	cp $< $@

# Create compressed version of file
%.gz: %
	gzip -9 -k -f -n "$^"

# WebP from PNG
%.webp: %.png
	$(CONVERT) "$^" -quality 90 -alpha Background "$@"
#	cwebp -short -alpha_cleanup -q 90 "$^" -o "$@"

# Audio MP4 (aac) from PM3
%.m4a: %.mp3
	ffmpeg -i "$^" -y -hide_banner -loglevel error -c:a aac -strict experimental "$@"

# JPEG from PNG
%.jpg: %.png
	$(CONVERT) $(CONVERT_JPEG_FLAGS) $< $@
	$(IMAGEOPTIM) $@

# PNG from SVG
%.png: %.svg
	$(CONVERT) -density 75 $< $@

# DDS-DXT5 from PNG
%-dxt5.dds: %.png
	$(COMPRESSONATOR) -nomipmap -fd ASTC $< $@

# DDS-ASTC from PNG
%-astc.dds: %.png
	$(COMPRESSONATOR) -nomipmap -fd DXT5 $< $@
	# $(CONVERT) $< -format dds -define dds:compression=dxt5 -define dds:cluster-fit=true -define dds:mipmaps=0 $@

# PVR-PRVTC 4bpp from PNG
%.pvr: %.png
	$(TEXTURE_TOOL) -e PVRTC --channel-weighting-perceptual --bits-per-pixel-4 -f PVR -o $@ $<
```

## Multiline command

Use `.ONESHELL:`

Or

```makefile
file.txt:
	cd folder; echo "content" > $@
```

```makefile
file.txt:
	cd folder && echo "content" > $@
```

Or:

```makefile
file.txt: .SHELLFLAGS = -c eval
file.txt: SHELL = bash -c 'eval "$${@//\\\\/}"'
file.txt:
	@cat <<-there\
		line1\
		line2\
	there > $@
```

Or:

```makefile
define GITIGNOREDS
*.o
tmp/
endef

export GITIGNOREDS
.gitignore:
	echo "$$GITIGNOREDS" > $@
```

Or:

```makefile
define GITIGNOREDS
*.o\n\
tmp/\n
endef

.gitignore:
	echo -e "$GITIGNOREDS" | sed 's/\\n/\n/g' > $@
```

- [GNU make](https://www.gnu.org/software/make/manual/make.html#One-Shell)
- [bash - Makefile recipe with a here-document redirection - Stack Overflow](https://stackoverflow.com/questions/35516379/makefile-recipe-with-a-here-document-redirection)
- For bash `for` loops: [php - How do you abort on shell command errors in makefiles? - Stack Overflow](https://stackoverflow.com/questions/6805253/how-do-you-abort-on-shell-command-errors-in-makefiles)
