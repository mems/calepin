## Firefox

Awesome bar:

> - Add `^` to search for matches in your browsing history.
> - Add `*` to search for matches in your bookmarks.
> - Add `+` to search for matches in pages you've tagged.
> - Add `%` to search for matches in your currently open tabs.
> - Add `~` to search for matches in pages you've typed.
> - Add `#` to search for matches in page titles.
> - Add `@` to search for matches in web addresses (URLs).
> - Add `$` to search for matches in suggestions.
– [Awesome Bar - Search your Firefox bookmarks, history and tabs from the address bar | Firefox Help](https://support.mozilla.org/en-US/kb/awesome-bar-search-firefox-bookmarks-history-tabs#w_changing-results-on-the-fly_2)

- Open Tabs to the right of the current tab: `about:config?filter=browser.tabs.insertAfterCurrent`, https://addons.mozilla.org/en-US/firefox/addon/always-right/

### Network debug

- [HTTP logging - Mozilla | MDN](https://developer.mozilla.org/en-US/docs/Mozilla/Debugging/HTTP_logging)

### Session / tabs

1. open `about:support` (profile directory)
2. open the directory
3. open the sub directory `sessionstore-backups`

Files in this directory:

- `previous.jsonlz4`: cleanBackup: copy of sessionstore.js from previous session that was loaded successfully
- `recovery.jsonlz4`: latest version of the sessionstore written during runtime
- `recovery.baklz4`: previous version of the sessionstore written during runtime
- `upgrade.jsonlz4-<build_id>`: backup created during an upgrade of Firefox

See also:

- [Session History Scrounger for Firefox (with lz4 support) — Fx File Utilities](https://www.jeffersonscher.com/ffu/scrounger.html) - read file format in `sessionstore-backups` directory

### Integrated authentication

Aka silent authentication

> authenticate the user to an Intranet server or proxy without prompting the user for a username or password

- [HTTP authentication - The Chromium Projects](https://www.chromium.org/developers/design-documents/http-authentication)
- [microHOWTO: Configure Firefox to authenticate using SPNEGO and Kerberos](http://www.microhowto.info/howto/configure_firefox_to_authenticate_using_spnego_and_kerberos.html)
- [Integrated Authentication - Mozilla | MDN](https://developer.mozilla.org/en-US/docs/Mozilla/Integrated_authentication)
- [header - Authentication issues with WWW-Authenticate: Negotiate - Stack Overflow](https://stackoverflow.com/questions/4265975/authentication-issues-with-www-authenticate-negotiate)

1. go to `about:config`
2. accept harmful consequences warning
3. search `network.negotiate-auth.trusted-uris` and update with value `.example.com` to allow auto login on that domains
4. if required, search `network.negotiate-auth.allow-non-fqdn` and set to `true` to allow non fully qualified domain names in the previous given list

For the list of trusted URIs, see:

- `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\CurrentVersion\Internet Settings\ZoneMap\Domains`
- [Internet Explorer security zones registry entries for advanced users](https://support.microsoft.com/en-us/help/182569/internet-explorer-security-zones-registry-entries-for-advanced-users)
- [How to configuring IE Site Zone mapping using group policy without locking out the user](http://www.grouppolicy.biz/2012/07/how-to-configuring-ie-site-zone-mapping-using-group-policy-without-locking-out-the-user/)

## Thunderbird

Wrap lines:

	mail.compose.wrap_to_window_width = true
	mail.wrap_long_lines = false

- [Autoconfiguration in Thunderbird - Mozilla | MDN](https://developer.mozilla.org/en-US/docs/Mozilla/Thunderbird/Autoconfiguration) - Create config profile for Thunderbird
- [Rebuilding the Global Database - Mozilla Support Community](https://support.mozilla.org/t5/Troubleshooting/Rebuilding-the-Global-Database/ta-p/15801)

### maildir format

By default, Thunderbird (before v38+~) use mbox format to store emails (use a huge file with all entries in it), and these files are not made easy for backup.

In advanced (config editor) (or in prefs.js if Thunderbird is closed): update `mail.serverDefaultStoreContractID` to `@mozilla.org/msgstore/maildirstore;1` (by default it's `@mozilla.org/msgstore/berkeleystore;1`), will set by default this format for all new accounts.

If you want to convert an existing mail box, for a given account/%account%

1. If it's not an IMAP account, copy folders/emails/rss to a backup account (ex.: Local Folders). For this backup account, favor local accounts (Local Folders, Mailspool/Movemail, RSS, etc.)
2. Close Thunderbird
3. backup `prefs.js` and `Mail/%account%` or `ImapMail/%account%`
4. change the pref `storeContractID` for the target account to `@mozilla.org/msgstore/maildirstore;1`
5. remove all files in and `Mail/%account%` or `ImapMail/%account%` (but you can keep `msgFilterRules.dat` for Email accounts and `feeditems.rdf` and `feeds.rdf` for Feeds accounts)
6. Open Thunderbird
7. If it's an IMAP account, just "Get mail", else restore by copy form the backup account

An other solution (when Thunderbird is closed) is to use a backup account which use already maildir format, copy folders/emails/rss to it, and replace files of the updated account with ones created in backup account

Don't forget to rebuild the "Global Database" (`global-messages-db.sqlite`)

See [Maildir](Maildir)

### Read local mail

[Since few versions](https://bugzilla.mozilla.org/show_bug.cgi?id=365879), Thunderbird OSX don't include "Unix Mailspool" account type.

The workaround is get the file [`movemail.rdf`](https://github.com/mozilla/releases-comm-central/blob/master/mailnews/base/ispdata/movemail.rdf) and install it in `Thunderbird.app/Contents/MacOS/isp`. Then follow [the instructions to configure an "Unix Mailspool" account](http://askubuntu.com/questions/1916/how-can-i-access-system-mail-in-var-mail-via-thunderbird)

For `Mail.app`, follow these intructions: [Access local mail via Mail.app - Mac OS X Hints](http://hints.macworld.com/article.php?story=20040313194905606)

## Excel

And LibreOffice

**LibreOffice use `;` as values separator in formulas.** And base on language/locale used, the decimal separator could be `.` or `,`

Conditional Formatting
Formula: Cell coords like `F6` are relative and `$F$6` is absolute. Relative cells coords are resolved during the formula evaluation, relative to the first one in range, then apply the relative coords to others.

### Median formula

| Price ($)		| Quantity (unit)	|
|---------------|-------------------|
| 1				| 99				|
| 2				| 20				|
| 7				| 3					|
| 10			| 1					|
|---------------|-------------------|
| Median		| 1$				|

Formula:

`=LOOKUP(-0,5;-PROB(ROW(A1:A100);B1:B100/SUM(B1:B100);ROW(A1:A100);2^20);A1:A100)` where `A1:100` are values and `B1:B100` are quantities.

> This is equivalent to looking up the 50% mark within a column of cumulative percentages. (Data is ordered so that the lookup function can be applied.)

- [Weight Median Help Requested (Part Quantity and Part Weight) : excel](https://www.reddit.com/r/excel/comments/2nadqs/weight_median_help_requested_part_quantity_and/)
- [Median with Quantity Column - ExcelBanter](https://www.excelbanter.com/excel-worksheet-functions/231843-median-quantity-column.html)

### Average formula

| Price ($)		| Quantity (unit)	|
|---------------|-------------------|
| 1				| 99				|
| 2				| 20				|
| 7				| 3					|
| 10			| 1					|
|---------------|-------------------|
| Average		| 1.3821138211$		|

`=SUMPRODUCT(A1:A100;B1:B100)/SUM(B1:B100)` where `A1:100` are values and `B1:B100` are quantities.

- [Calculate the average of a group of numbers - Excel](https://support.office.com/en-us/article/calculate-the-average-of-a-group-of-numbers-e158ef61-421c-4839-8290-34d7b1e68283)

### Excel seconds to dates

Divide the number of seconds by 86400 (the number of seconds in a day: 24 * 60 * 60):

- value: `145`
- formula: `=A1 / 86400`
- computed: `0.001678241`
- formated `00:02:25` (time, `HH:MM:SS` or `[HH]:MM:SS` or `dd:hh:mm:ss`)

Milliseconds are not supported by dates. Could be defined in format to be always 0: `HH:MM:SS.000`, `[SS].000`

See also:

- `=TEXT(A1/86400,CHOOSE(MATCH(A2,{0,60,3600},1),"s ""sec""","m ""min"" s ""sec""","[h] ""hrs"" m ""min"" s ""sec"""))` give `64 hrs 8 min 21 sec`
- [How to convert dd hh mm time format to hours or minutes in Excel?](https://www.extendoffice.com/documents/excel/4050-excel-convert-dd-hh-mm-to-hours.html)

## MAMP

### Logs files

Since El Capitain, symlink to a folder no longer work in Console, need to create symlink directly to the log file

	cd ~/Library/Logs
	mkdir -p MAMP
	cd MAMP
	ln -s /Applications/MAMP/logs/*.log .

### PHP

There multiple `php.ini` in MAMP.

In non Pro version: You should edit (where `*.*.*` is active PHP version):

`MAMP/bin/php/php*.*.*/conf/php.ini`

An other location:

`MAMP/conf/php*.*.*/php.ini`

But seem not used (any explanations? Regenerated by Pro version from `php.ini` template file?)

MAMP Pro, use also templates : `File > Edit Templates > PHP *.*.* php.ini` (or edit `MAMP/bin/php/php*.*.*/conf/php.ini.temp`)

#### Debugger

	[xdebug]
	
	xdebug.default_enable=1
	
	xdebug.remote_enable=1
	xdebug.remote_handler=dbgp
	xdebug.remote_host=localhost
	xdebug.remote_port=9000
	xdebug.remote_autostart=1
	
	zend_extension="/Applications/MAMP/bin/php5/lib/php/extensions/no-debug-non-zts-xxxxxxxx/xdebug.so"

### Apache

`MAMP/conf/apache/httpd.conf`

### MySQL

Create `MAMP/conf/my.cnf`

- https://stackoverflow.com/questions/678645/does-mysql-included-with-mamp-not-include-a-config-file
- http://bensch.be/mysql-config-with-mamp

Be carefull of params in `MAMP/conf/startMysql.sh`

- [Server adminstration (Linux) # MySQL (sql server) Fichiers de configuration]()

### PHP Intl lib

	sudo port install php54-intl

Copy `/opt/local/lib/php54/extensions/no-debug-non-zts-20100525/intl.so` to `/Applications/MAMP/bin/php/php5.4.10/lib/php/extensions/no-debug-non-zts-20100525/intl.so`

Add in `/Applications/MAMP/bin/php/php5.4.10/conf/php.ini`:

	extension=intl.so

## 1Password

Charles proxy with 1password disable port 127.0.0.1:59488

Edit custom form fields.

If JS is used to validate form field, prefer create manually login entry in 1Password, deleted form fields seem still saved

Standalone license:

> Those of you with a standalone license for version 6 will be prompted to subscribe or purchase a license when the beta first opens. Licenses will be available for $64.99 when we launch later this year, but are available now for only $39.99.
> [...]
> We put the link for purchasing the standalone license directly in the upgrade screens that you’ll see after you install and launch the beta. In other words we have it set up as an in-app purchase.
> — https://blog.agilebits.com/2018/03/28/the-1password-7-beta-for-mac-is-lit-and-you-can-be-too/#comment-16839

- [Workaround for adding web form fields](https://discussions.agilebits.com/discussion/comment/93335/#Comment_93335)
- [Where does 1Password store its data? - 1Password for Mac Knowledgebase - version 5](https://guides.agilebits.com/1password-mac-kb/5/en/topic/data-locations)

## COD MW2

Redirect UDP 28960

- [Required Ports for Steam - Network/Connection Issues - Knowledge Base - Steam Support](https://support.steampowered.com/kb_article.php?ref=8571-GLVN-8711)

## Chrome

- [List of Chromium Command Line Switches « Peter Beverloo](https://peter.sh/experiments/chromium-command-line-switches/)

### Network debug

NetLog log:

- queueing delay to schedule DNS resolves to threads
- stalls due to exceeding socket pool limits
- attempts to do a TCP connect to an IP address
- speculative DNS resolves
- proxy resolution
- cache hits for DNS resolves
- reads/writes from disk cache
- network change events
- proxy configuration change events
- stalls due to chrome extensions pausing requests
- errors
- cookie store

> Features needing reliable network information should never be built on top of NetLog
> - [NetLog: Chrome’s network logging system - The Chromium Projects](https://www.chromium.org/developers/design-documents/network-stack/netlog)

- chrome://net-export/#
- [List of event types](https://cs.chromium.org/chromium/src/net/log/net_log_event_type_list.h)
- [How to capture a NetLog dump - The Chromium Projects](https://www.chromium.org/for-testers/providing-network-details)
- `--net-log-capture-mode=IncludeCookiesAndCredentials` or `IncludeSocketBytes` `--log-net-log=/path/to/file` (ex: `netlog.json` or `net-export/chrome-net-export-log.json`)
- [NetLog viewer](https://netlog-viewer.appspot.com/#events)
- [chromium tools - chrome_proxy/webdriver/common.py](https://chromium.googlesource.com/chromium/src/tools/+/6dd06e1a895bd96e385f3bacd13d2c7a84a69915/chrome_proxy/webdriver/common.py#668) and [chromium catapult - netlog_viewer/netlog_viewer/log_util.js](https://chromium.googlesource.com/catapult/+/refs/heads/master/netlog_viewer/netlog_viewer/log_util.js#250) - About the invalidity of NetLog output when used with `--log-net-log` and a workaround
- [NetLog: Chrome’s network logging system - The Chromium Projects](https://www.chromium.org/developers/design-documents/network-stack/netlog)
- [Life of a URLRequest](https://chromium.googlesource.com/chromium/src/+/master/net/docs/life-of-a-url-request.md)
- [NetLog viewer sources](https://chromium.googlesource.com/catapult/+/master/netlog_viewer/)
- [Importateurs de violoneux](https://blog.arcoptimizer.com/importateurs-de-violoneux)
- [ericlaw1979/FiddlerImportNetlog: Fiddler Importer for Chromium NetLog .json files](https://github.com/ericlaw1979/FiddlerImportNetlog)
- Event time: `new Date(data.constants.timeTickOffset + parseInt(event.time))`
- [Network Traffic Annotations](https://chromium.googlesource.com/chromium/src/+/master/docs/network_traffic_annotations.md) and [tools/traffic_annotation - chromium/src](https://chromium.googlesource.com/chromium/src/+/refs/heads/master/tools/traffic_annotation/) - "What is the intent behind each network request"

To know what extension handle requests (marked as `307 Internal Redirect`, see `delegate_info`, `CHROME_EXTENSION_REDIRECTED_REQUEST`, `URL_REQUEST_FAKE_RESPONSE_HEADERS_CREATED`)

```js
const readline = require("readline");
const {createReadStream} = require("fs");

async function readNetLogFile(file, eventFilter = null){
  const readlineIterable = readline.createInterface({
    input: createReadStream(file),
    crlfDelay: Infinity,
  });

  let result = null;

  const useEventFilter = typeof eventFilter === "function";

  let parent = null;
  lineLoop: for await(const line of readlineIterable){
    switch(true){
      // header
      case line.startsWith("{\"constants\":"):{
        result = {
          ...JSON.parse(line.slice(0, -1) + "}"),
          events: [],
          polledData: null,
        };// remove trailing comma and add the closing parenthese
        break;
      }
      // start events section
      case line.startsWith("\"events\":"):
        parent = "events";
        break;
      // event
      case parent === "events":{
        const eof = line.endsWith("]}");
        const isLastEvent = eof || line.endsWith("],");
        // If it's the last event, before next section
        // then skip the events array close braket and trailing comma
        // else skip the trailing comma
        const rawData = line.slice(0, isLastEvent ? -2 : -1);
        const event = JSON.parse(rawData);

        // Filter events
        if(!useEventFilter || eventFilter(event, result)){
          result.events.push(event);
        }

        if(eof){
          parent = null;
          break lineLoop;
        }

        if(isLastEvent){
          parent = null;
        }
        break;
      }
      // footer
      case line.startsWith("\"polledData\":"):
        // TODO
        break;
      // EOF
      case line === "}":
        parent = null;
        break lineLoop;
      default:
    }
  }

  return result;
}
```

### Custom device with higher granularity

https://developer.chrome.com/devtools/docs/device-mode#custom-devices


trunk/Source/devtools/front_end/emulation/EmulatedDevices.js


WebInspector.settings.createSetting("customEmulatedDeviceList", [])

in customEmulatedDeviceList each entry:
.capabilities = [];//["touch","mobile"]
.type = "notebook";//"phone"//"tablet"//"unknown"
For default value: 0 or ""

WebInspector.EmulatedDevicesList.dispatchEventToListeners(WebInspector.EmulatedDevicesList.Events.CustomDevicesUpdated); 


chrome.experimental.devtools.* 

https://api.github.com/repos/GoogleChrome/devtools-device-data/contents/devices.json?ref=release
https://github.com/GoogleChrome/devtools-device-data/blob/release/devices.json

~/Library/Application Support/Google/Chrome/Default/Preferences
JSON: devtools.preferences.customEmulatedDeviceList parse as JSON

## Handbrake Protected DVD

Use VideoLAN's libdvdcss

- http://download.videolan.org/libdvdcss/1.2.12/macosx/libdvdcss.2.dylib

Copy it in `/usr/local/lib` (create lib folder if not exist)

`xattr -d com.apple.quarantine /usr/local/lib/libdvdcss.2.dylib` or double click on the file

- [El Capitan apparently broke Handbrake ripping copy-protected DVDs. Any clue what to do? : osx](https://www.reddit.com/r/osx/comments/3n6gz4/el_capitan_apparently_broke_handbrake_ripping/)

If still 99 titles are available, the DVD is protected. Use an other software (like VLC or DVD Player) to read it and go to the main movie and get the correct title (DVD Player: push your cursor to the top of the display to reveal the menu bar. From that menu bar choose Go -> Title. Scan down the long list of titles and you’ll see a check next to one of the titles. This is the title number of the real main feature)

## Finder

Search input (by default input field in top right of Finder's window) find same files as Spotlight.

### Advanced Search

Use `NOT` keyword as a prefix of search term: `NOT keyword`. `OR` and `()` can be used too: `Terminal AND (Safari OR "defaults write")`

Alt/Opt click on the `+` button to create a condition group (need at least on criterion added): simple click `+` first, then Alt + click `+` (key down Alt will show `…`). This allow to use condition: Any (OR), All (AND), or None (NOT)

- [OS X Yosemite: Narrow down search results](https://support.apple.com/kb/PH18758?locale=en_US)

## LibéCompta

plist based format .lbc (default), .lbcx (binary) and .xml (XML)

Lien fichier (alias) inode. See BookmarkData format

Ajouter un (ou plusieurs) compte charge/achat "intracommunautaire"
2035: BA (à voir)
TP: BJ (à voir)
TVA: 0031
Taux TVA: 20% (à voir)
Utiliser écritures associé: compte "achat intra"
Associera automatiquement les comptes TVA déductible et TVA due intra

How to fix Crédit Agricole OFX import:
Create LCB XML version

1. Import first as Crédit Agricole (Update bank account filter in Accounts)
2. Save & backup the file
3. Delete entries
4. Import as HSBC
5. Compare with `diff import_CA.xml import_HSBC.xml` (not unified)
6. Replace patch content and list:
	
		/([0-9a-f,]+\n<\s*<date[^<].*\n---\n>\s*<date.*)/g
		$1\n
7. Apply `patch import_CA.xml fix.patch`
8. Open the result file and copy/drag&drop entries

Si il est impossible de "Transférer en comptabilité" une opération auxiliaire, recréer le fichier LCB (certaines pièce jointes seront perdues) avec la bonne année

### Unlock LibeCompta

File > (Key Alt) Save as... > "LibéCompta XML" (see also `plutil -convert xml1 -o <output file> <input file>`)
and remove:

	<key>secur</key>
	<dict>
		<key>cloture</key>
		<true/>
		<key>clotureDate</key>
		<date>2018-04-30T22:00:00Z</date>
	</dict>

### LibeCompta Data

Frais kilométriques `/Applications/LibéCompta/Contents/Resources/BNC.plist` et `BIC.plist`

Libellé			Jusqu'à 3000km	De 3001 km à 6000 km	Au-delà de 6000 km
Plus de 5 CV	d x 0,518		(d x 0,067) + 1,351		d x 0,292

Donne :

		<array>
			<integer>518</integer>
			<integer>67</integer>
			<integer>1351</integer>
			<integer>292</integer>
		</array>

Certaines sections de véhicules on été retiré en 2014

## Captvty

- [Forum Captvty • (neo-net.fr)](http://neo-net.fr/forum/viewforum.php?f=31)

### Package Captvty for Mac

[Captvty](http://captvty.fr/)

With Winebottler, create Application bundle from the zip version:

1. Prefix template: new prefix (default)
2. Program installation: select the `Captvty.exe`
3. Installation mode:
	WineBottler 1.8rc4 the following not work properly:
	> copy file (Program) and all files in the folder to the App Bundle
4. System: `XP`
5. don't include Mono and Gecko
6. DLL Override: `mscoree=n,b;mshtml=n,b` (see [Wine DLL overrides](#wine-dll-overrides))
6. Winetricks: `dotnet40` (or `dotnet45` for v3). Recommanded, but not required: `flash`, `gdiplus`, `ie8`
7. App Bundle:
	Copyright: `© Captvty`
	Version: _use the Captvty version number_
	Identifier: `fr.captvty.captvty`
	Category Type: `Video`
8. Click on Install
9. Save as `Captvty.app` (**but not in the folder of the .exe**)
10. (.Net Framework 4 Client Installer) Install (restart later)
11. (Flash Installer) Install (without updates)
12. (IE8 Install) Install, (Without updates: Microsoft Update, Malware remover, etc.), restart later
13. (See step 3, if second option choosen) Copy all files from Captvty ZIP to `Captvty.app/Contents/Resources/wineprefix/drive_c/winebottler/` (right click on Captvty.app, see Bundle content)
14. Move/Copy `Captvty.app` to `/Applications`
15. Ready to watch

Note: Version 3 can show an error but works. "Direct" not work

- [Foire aux question | Captvty](http://captvty.fr/faq#linux)

## Filebot

### Build filebot for Mac

1. Download https://github.com/filebot/filebot/archive/master.zip
2. Check if you have Java JDK 8u91+ and ant installed
3. Download http://ant.apache.org/ivy/download.cgi (binary version) and https://mvnrepository.com/artifact/org.tukaani/xz/1.0 (Download JAR)
4. Uncompress and copy `ivy-2.X.X.jar` in `lib/jars`
5. (optional) update in `appbundle-maspkg-core` `<param name="application.mode" value="Rename|Episodes|SFV|Filter|List" />` to `<param name="application.mode" value="Rename|Episodes|SFV|Filter|List|Subtitles" />`
6. (optional) change

		<target name="revision" depends="init">
			<exec executable="git" outputproperty="revision" failonerror="true">
				<arg line="rev-list --count master" />
			</exec>
			<echo>Revision: ${revision}</echo>
		</target>
	
	to (number of https://github.com/filebot/filebot commits)
	
		<target name="revision" depends="init">
			<echo>Revision: 4498</echo>
		</target>
6. start `ant -lib lib/jars resolve fatjar appbundle` in the project folder
7. could require on macOS to start following commands before get GUI works
 
	java -jar /Applications/FileBot.app/Contents/Java/FileBot_4.7.jar -help
	java -jar FileBot.jar -script fn:artwork.tvdb /path/to/tvshows_dir/

- [How about sharing your CLI scripts? - FileBot](http://www.filebot.net/forums/viewtopic.php?f=4&t=5#p204)
- https://github.com/filebot/filebot
- https://downloads.sourceforge.net/project/filebot/filebot/HEAD/FileBot.jar

## MW2

MW2 Nat strict

- http://rigelt.blogspot.fr/2009/12/modern-warfare-2-nat-strict-or-open.html
- http://steamcommunity.com/sharedfiles/filedetails/?id=165136021
- http://www.se7ensins.com/forums/threads/how-can-i-set-my-nat-type-open-on-a-mac.1206549/
- http://www.clubic.com/forum/jeux-video-pc/probleme-de-nat-strict-mw2-ouverture-de-ports-id678364-page1.html
- http://blog.gameagent.com/aspyr-mac-faqs-call-duty-modern-warfare-2-call-duty-modern-warfare-3/

## Android Virtual Device

How to change proxy settings:

1. Open settings app
2. > Wireless & Networks > More... > Mobile networks | Cellular networks
3. Check "Data enabled"
4. > Access Point Names
5. Select one point name
6. **Update or clear proxy username/password fields (defaults are "none"/"none", clear value to not use any username and password)**
7. **Use return button to submit** or use `⁝` (kebab menu) > Save

- [Android emulator proxy setting - Stack Overflow](https://stackoverflow.com/questions/35502437/android-emulator-proxy-setting)

Add this shell script in `/Applications`:

	#!/bin/sh
	/Developer/SDKs/android-sdk/tools/android &
	exit

Install an application on virtual device

	adb install /path/to/app.apk

	$ANDROID_SDK/platform-tools/adb

- https://github.com/PaulKinlan/chromium-android-installer
- [Chrome APKs - APKMirror](http://www.apkmirror.com/apk/google-inc/chrome/)
- [Android Debug Bridge | Android Studio](https://developer.android.com/studio/command-line/adb.html)

## IntelliJ Applications

Aka WebStorm, PhpStorm, IntelliJ IDEA

Grunt task output `Task "watch" passed` or `Task "watch" failed` are handled by the app: [Grunt feedback : WEB-11713](https://youtrack.jetbrains.com/issue/WEB-11713#comment=27-718038)

- Command keyboard shortcut match only US layout: [National keyboard layouts support : IDEA-165950](https://youtrack.jetbrains.com/issue/IDEA-165950#comment=27-2053321)
- Support ANSI sequences in Run tool (use terminal for NodeJS registry key, at least in PhpStorm 2018.3 and WebStorm 2018.2): [Console output manipulation is not supported when using WebStorm Run : IDEA-154313](https://youtrack.jetbrains.com/issue/IDEA-154313#focus=streamItem-27-2842206.0-0)
- Help > Find Action > Check "UML support" on, right click on file or folder > Diagram. [Module Dependency Diagrams - Help | PhpStorm](https://www.jetbrains.com/help/phpstorm/module-dependency-diagram.html)

List of files in search:

```js
// In a webpage, add the following code in dev tools console, then past in the page the copied content of "Export to text file" of the Find Window
document.addEventListener("paste", function(event) {
	console.log(event.clipboardData.getData("Text").split(/\r?\n/).reduce((list, rawLine) => {
		const [, prefix = "", line = rawLine] = rawLine.match(/^((?: {4})*)(.*)$/) || [];
		
		switch(prefix){
			// indent 3, path + usage count
			case "            ":
				list.push({
					path: (line.match(/^(.*?)(\s*\(.*?\))?$/) || [])[1] || line,
					files: []
				});
				break;
			// indent 4, filename + usage count
			case "                ":
				list[list.length - 1].files.push((line.match(/^(.*?)(\s*\(.*?\))?$/) || [])[1] || line)
				break;
			// indent 5, line match + extract
			case "                    ":
			// others
			default:
				// ignore
				break;
		}
		
		return list;
	}, []).reduce((list, {path, files}) => list.concat(files.map(file => path + "\\" + file)), []).join("\n"))
});
```

## Adobe

### Uninstall Adobe

	/Library/Application Support/Adobe
	~/Library/Application Support/Adobe
	/Applications/Utilities/Adobe Application Manager
	/Applications/Utilities/Adobe Installers

See if hosts files doesn't contains blocked domains

### Adobe Illustrator

#### Get vectors from PSD

Open PSD to get vectors (shapes and masks):

- images with a vector mask will be converted to full width and height image (padded with transparent pixels)
- images with clipping mask (masque d'écrêtage) will be cropped as rectangle (rounded pixels outside shape) that match the bounding box of the shape
- Illustrator use the dpi of the PSD. If you want to use pixels in Illustrator, fix the correct resolution (pixel density) via image size modal (in Photoshop):
	1. open Image size modal
	2. keep in mind the pixel dimensions
	3. change resolution to 72dpi
	4. restore previous values of pixel dimensions
	5. now only document size width and height should changes
	
	Or (in Illustrator):
	
	Scale all imported elements as 300/72 ~= 416.666667%

	It's related to import as 300 dpi instead of 72 dpi
	
#### Scripts

- [Ajar Productions » Announcing Merge Text Extension for Adobe Illustrator](https://ajarproductions.com/blog/2008/11/23/merge-text-extension-for-illustrator/)

Install custom script:

`/Applications/Adobe Illustrator CS6/Presets.localized/xx_XX/Scripts/` where `Presets.localized` is translated in Finder and `xx_XX` is locale
Windows: `C:\Program Files\Adobe\Adobe Illustrator %VERSION%\Presets\xx_XX\Scripts`
Mac OS X: `Applications/Adobe Illustrator $VERSION/Presets/Scripts`

- [javascript - Where to put the script to appear under scripts menu in Illustrator cs5.1 - Stack Overflow](https://stackoverflow.com/questions/27013800/where-to-put-the-script-to-appear-under-scripts-menu-in-illustrator-cs5-1)

#### Fix SVG non-zero `viewbox`

When Illustrator output SVG document

eg. : `viewBox="29.053 214.6 137.451 108.398"` to `viewBox="0 0 137.451 108.398"`:

1. copy layers
2. create a new document
3. past layers in newly created document
4. move layers to zero
5. crop artboard

Or use SVGO (see [SVGOMG](https://jakearchibald.github.io/svgomg/))

#### SVG path element instead of primite element

(line, polygon, rect, etc.).

1. Make Compound Path (tracé transparent) with `CMD + 8`, or right click + Make Compound Path. Or use `Object > Path > Simplify`

#### Clipping mask

Aka masque d'écrêtage

1. Select 2 objects, the first one will be the clipping mask
2. `Object > Clipping Mask > Make`

- [How to use and edit clipping masks in Illustrator](https://helpx.adobe.com/illustrator/using/clipping-masks.html)

### Adobe Lightroom

- [Jeffrey Friedl's Blog » Accessing Lightroom’s SQLite DB Directly](http://regex.info/blog/2006-07-29/221)
 
	~/Pictures/Lightroom 5 Catalog.lrcat

To update, download Adobe DNG Converter (for [macOS](http://www.adobe.com/go/dng_converter_mac/) or [Windows](http://www.adobe.com/go/dng_converter_win/)) the open the install package (ex: with Suspicious Package)

And copy cameras profiles (`CameraProfiles`) and lenses profiles (`LensProfiles`) from `/Library/Application Support/Adobe/CameraRaw` in:

	/Applications/Adobe Photoshop Lightroom 5.app/Contents/Resources/*
	~/Library/Application Support/Adobe/CameraRaw/*

Then copy `/Library/Application Support/Adobe/CameraRaw/Settings` in `~/Library/Application Support/Adobe/CameraRaw/`

For Windows: `%USER_APPDATA%\Roaming\Adobe\CameraRaw\LensProfiles\1.0\Downloaded` and `C:\ProgramData\Adobe\CameraRaw\LensProfiles\1.0\`

## FFMpeg

If ffmpeg is used in a loop, you could need to use `< /dev/null`:

- [Strange errors when using ffmpeg in a loop - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/36310/strange-errors-when-using-ffmpeg-in-a-loop/36411#36411)
- [BashFAQ/089 - Greg's Wiki](http://mywiki.wooledge.org/BashFAQ/089)

- [bash - How to exit from find -exec if it fails on one of the files - Stack Overflow](https://stackoverflow.com/questions/14871147/how-to-exit-from-find-exec-if-it-fails-on-one-of-the-files)

Make a video from image slideshow:

	# KEYFRAME_INTERVAL=2
	# http://www.ffmpeg.org/ffmpeg-all.html#Options-23
	# https://trac.ffmpeg.org/wiki/Create%20a%20video%20slideshow%20from%20images
	# https://trac.ffmpeg.org/wiki/vpxEncodingGuide
	# http://en.wikipedia.org/wiki/H.264/MPEG-4_AVC#Profiles
	#
	# -r 1 = one frame per second. Simplify seeking
	# http://www.webmproject.org/about/faq/#what-are-the-limits-of-vp8-in-terms-of-resolution-datarate-and-framerate
	# -i *** = input file
	# -c:v libvpx = video codec is VP8 video encoder (libvpx)
	# -crf 10 = constant quality mode (CRF) (4 to 63)
	# -b:v 1M = target variable bitrate (VBR) to 1000kBit/s
	# -force_key_frames "expr:gte(t,n_forced*1)" = forced keyframe every frames
	# sequence00001.jpg
	# ffmpeg -r 1 -i "sequence_%05d.jpg" -c:v libvpx -qmin 4 -qmax 30 -crf 10 -b:v 100k -force_key_frames "expr:gte(n,n_forced*$KEYFRAME_INTERVAL)" sequence.webm

Include subtitles in a video:

	ffmpeg -i movie.mp4 -i subtitles.srt -map 0 -map 1 -c copy -c:v libx264 -crf 23 -preset veryfast output.mkv

Offset (soft) subtitle track embeded in a video container

	ffmpeg -i input.mp4 -itsoffset -0.7 -i input.mp4 -map 0:v -map 0:a -map 1:s -c copy output.mp4

- [How can I fix delayed subtitles in videos? - Super User](https://superuser.com/questions/494841/how-can-i-fix-delayed-subtitles-in-videos/1242613#1242613)

Offset subtitle track file (in seconds):

	ffmpeg -itsoffset -0.7 -i input.srt -c copy output.srt

Extract audio from video:

	# To 256kbps MP3
	ffmpeg -i video.mp4 -vn -ab 256 audio.mp3

Mute video:

	ffmpeg -i video.mp4 -an muted-video.mp4

Merge files (works on `*.srt` too) with identical codecs.

**Be careful sometimes this not work propelly**

	ffmpeg -i "concat:file1.avi|file2.avi" -c copy "file.avi"

Remove an audio track:

	ffmpeg -i file.mp4
	Stream #0.0: Video: [truncated]
	Stream #0.1: Audio: [truncated]
	Stream #0.2: Audio: [truncated]

	ffmpeg -i file.mp4 -map 0:0 -map 0:2 -acodec copy -vcodec copy new_file.mp4

Will copy the video and the second audio track

To remove all audio tracks use `-an` or `-vn` to remove video tracks:

	ffmpeg -i input_file.mp4 -vcodec copy -an output_file.mp4

- [How to merge audio and video file in ffmpeg - Super User](http://superuser.com/questions/277642/how-to-merge-audio-and-video-file-in-ffmpeg/277667#277667)

Convert to Apple ringstone (only the first 30 seconds will be played):

	# if already AAC
	ffmpeg -i Nuance.aac -f mp4 -c copy Nuance.m4r
	# else
	ffmpeg -i ringtone.mp3 -ac 1 -ab 128000 -f mp4 -acodec libvo_aacenc -y ringtone.m4r

Convert all WMA to MP3 (and remove it):

	find . -type f -iname "*.wma" | while read file; do < /dev/null ffmpeg -i "${file}" -acodec libmp3lame -ab 192k "${file/.wma/.mp3}" && rm "${file}"; done
	find . -type f -iname "*.wma" -exec bash -c 'ffmpeg -i "$1" -acodec libmp3lame -ab 192k "${1/.wma/.mp3}" && rm "$1"' - {} \;

Find invalid media files:

	find . -type f \( -iname "*.wma" -or -iname "*.mp3" -or -iname "*.m4a" -or -iname "*.mp4" -or -iname ".wav" -or -iname "*.ogg" \) \( -exec ffmpeg -v error -xerror -i "{}" -f null - 2>/dev/null \; -or -exec echo "{}" \; \)
	# To get the details into log file
	find . -type f \( -iname "*.wma" -or -iname "*.mp3" -or -iname "*.m4a" -or -iname "*.mp4" -or -iname ".wav" -or -iname "*.ogg" \) -exec bash -c 'echo "$1:" >> error.log; ffmpeg -v error -xerror -i "$1" -f null - 2>>error.log && echo "OK" >> error.log; exit $?' - {} \;

You can also detect black frame and/or slicence with [`blackdetect`](http://www.ffmpeg.org/ffmpeg-filters.html#blackdetect) and [`slicendetect`](https://ffmpeg.org/ffmpeg-filters.html#silencedetect): `-af silencedetect=d=3:n=0.0001` (you need to remove/update `-v error`, see also `-loglevel info`)

- [How can I check the integrity of a video file (avi, mpeg, mp4...)? - Super User](https://superuser.com/questions/100288/how-can-i-check-the-integrity-of-a-video-file-avi-mpeg-mp4)

Download RTMP stream:

	ffmpeg -i "rtmp://cp262207.edgefcs.net:80/ondemand/techchannel/10821/videos/10821_AA11149_Pair_Paradox_FL8_412x310_700K" -c copy "A Pair of Paradoxes.flv"

Get media metadata:

	ffmpeg -i file.avi -f ffmetadata pipe:1
	#or
	ffmpeg -i file.avi

Concat files:

	ffmpeg -f concat -safe 0 -i <(find $PWD -type f -iname *.mp4 -printf "file '%h/%f'\n") -c copy output.mp4

- [Concatenate – FFmpeg](https://trac.ffmpeg.org/wiki/Concatenate)

## Imagemagick

Pixel shader for channels [`fx`](http://www.imagemagick.org/script/fx.php), column (`i`) and row (`j`) are zero based.

Multiple files: 

Use `mogrify` or `find ./ -iname "tile_*.png" -exec bash -c 'filename="$1";echo "${filename%.*}"' _ {} \;`

Get trim area:

	# `-quiet` remove warnings
	convert test.png -trim -format "%G%O\n" -quiet info:
	convert test.png -format "%@" -quiet info:
	# You can save result and log info
	convert test.png -trim -format "%O\n" -quiet -write info: test_trim.png >> output.log

Get hash of image (only pixels, not metadata):

	identify -format "%#\n" image.png

Create a TIFF (support layers) with PNGs (from export of all layers in PS) due to strange PSD handling of ImageMagick (layers+1, cropped layers):

	# (First is in foreground, last in background)
	# convert app-decorations_0000_main.png app-decorations_0001_shadow1.png app-decorations_0002_shadow2.png app-decorations.tif

Crop and get final filenames without creating it

	# For the followin command:
	#convert largeimage.png -crop 2048x2048 -set filename:tile "%[fx:page.x/2048+1]_%[fx:page.y/2048+1]" +repage +adjoin "tile_%[filename:tile].png"
	convert largeimage.png -crop 2048x2048 -format "tile_%[fx:page.x/2048+1]_%[fx:page.y/2048+1].png\n" info:
	# To get the number of file will be created, append `| wc -l`

- [Fred's ImageMagick Scripts](http://www.fmwconcepts.com/imagemagick/)

Extend document size

	# mogrify/convert promote automatically 16 bits per channels if any pixels are modified. Need `-depth 8` to keep bit_depth=8 for PNGs
	mogrify -background none -extent 2048x2048 -depth 8 tile_*.png

Compose alpha:

	convert RGB.png Alpha.png -compose Copy_Opacity -composite RGBA.png
	convert RGBA.png -alpha off RGB.png
	# convert RGBA.png -channel a -fx "1" RGB.png

Pre-multiply alpha (aka premultiped alpha)

	convert in.png \( +clone -alpha Extract \) -channel RGB -compose Multiply -composite out.png

- [\[SOLVED\] Multiplying color by alpha - ImageMagick](http://www.imagemagick.org/discourse-server/viewtopic.php?t=23463)

Set color to transparent pixels

	convert in.png -channel rgb -fx 'a==0?1:s' out.png

Bleed outside:

	# Source image 32x32 -> 70x70
	convert tree.gif  -set option:distort:viewport 70x70-19-19 -virtual-pixel Edge -filter point -distort SRT 0 +repage virtual_edge.gif

Get average color of an image

	convert cat.png -resize 1x1 txt:- | awk 'NR==2{print $3}'
	# Or
	convert cat.png -scale 1x1\! -format '%[fx:int(255*r+.5)],%[fx:int(255*g+.5)],%[fx:int(255*b+.5)]‌​' info:- | sed 's/,/\n/g' | xargs -L 1 printf "%x"

Convert raw data to image

	# 2 RGB pixels: 2x1
	printf '\x00\xFF\x88\xFF\x00\xFF' | convert -depth 8 -size 2x1+0 rgb:- data.png
	# Create Nx4 bytes to generate Nx1 RGBA PNG
	printf '\x00\xFF\x88\xFF\xFF\x00\xFF\xFF' > data.bin; convert -depth 8 -size $(($(wc -c < data.bin)/4))x1+0 rgba:data.bin data.png

Create image (from nothing). `xc` "X Constant Image" / Canvas: [Canvas Creation -- IM v6 Examples](http://www.imagemagick.org/Usage/canvas/)

	convert -size 100x100 xc:white canvas.jpg

Remove metadata (see also `-define` and[PNG Metadata](PNG#metadata))

	convert -strip image.jpg image_slim.jpg

Force PNG to be 32 bits:

	mogrify -background none -define png:color-type=6 image.png

Swap / invert / intervert channels

	# Invert R with B (r=0, g=1, b=2 and a=3) and keep alpha + output always as PNG 32bit
	convert in.png -channel rgba -alpha on -set colorspace RGB -separate -swap 0,2 -combine -define png:color-type=6 out.png

- [swap colors/channels - ImageMagick](http://www.imagemagick.org/discourse-server/viewtopic.php?t=21846)

Get metadatas:

	convert image.jpg -moments infos.json
	convert -moments - json: < image.jpg > infos.json

- [Formats @ ImageMagick](https://www.imagemagick.org/script/formats.php) - ImageMagick can write JSON format
- [Command-line Tools: Identify @ ImageMagick](https://www.imagemagick.org/script/identify.php) - Supported options

Outline

- [Outline image on transparent background - ImageMagick](https://www.imagemagick.org/discourse-server/viewtopic.php?t=16399)

Generate blank image

	convert -size 100x100 xc:white canvas.jpg

### Convert SVG

[Drawing -- IM v6 Examples](http://www.imagemagick.org/Usage/draw/#svg)

	convert -background none a.svg b.png
	convert -density 150 -background none a.svg b.png

Try MSVG imagemagick's own SVG renderer

	convert -background none msvg:a.svg b.png

By default it delegate to `rsvg-convert` (`convert -list delegate | grep 'svg ='`), but could be not installed (`brew install imagemagick --use-rsvg` or `sudo port install ImageMagick +rsvg`)

- [ImageMagick convert SVG to PNG not working with RSVG enabled - Stack Overflow](https://stackoverflow.com/questions/11592085/imagemagick-convert-svg-to-png-not-working-with-rsvg-enabled)
- [osx - Use librsvg / rsvg to convert SVG images with ImageMagick - Stack Overflow](https://stackoverflow.com/questions/24513244/use-librsvg-rsvg-to-convert-svg-images-with-imagemagick)

## X11

Aka XQuartz, Xorg

Install with [MacPorts](https://www.xquartz.org/releases/#macports):

	sudo port -v install xorg-server +universal
	# Some libs don't use the right path:
	sudo ln -s /opt/local /usr/X11
	# see also /usr/X11R6

Uninstall XQuartz

	launchctl unload /Library/LaunchAgents/org.macosforge.xquartz.startx.plist && \
	sudo launchctl unload /Library/LaunchDaemons/org.macosforge.xquartz.privileged_startx.plist && \
	sudo rm -rf /opt/X11* /usr/X11* /Library/Launch*/org.macosforge.xquartz.* /Applications/Utilities/XQuartz.app /etc/*paths.d/*XQuartz && \
	sudo pkgutil --forget org.macosforge.xquartz.pkg  && \
	rm -rf ~/.serverauth* && rm -rf ~/.Xauthorit* && rm -rf ~/.cache && rm -rf ~/.rnd && \
	rm -rf ~/Library/Caches/org.macosforge.xquartz.X11 && rm -rf ~/Library/Logs/X11

- [Uninstall XQuartz.app from OSX Yosemite/El Capitan/Sierra](https://gist.github.com/pwnsdx/d127873e24cef159d4d603accaf37ee4)

Some times, after wakeup or deconnected from an external screen (clampshield), xorg don't work:

	$ xorg
	...
	Fatal server error:
	(EE) no screens found(EE)
	...

Then restart.

## Wine

See also Wineskin

macOS Wine: `Wine.app`

Install winetrick in current prefix: Wine menu > Wintricks

	/Applications/Wine.app/Contents/Resources/bin/wine app.exe
	WINEPREFIX=~/.wine /Applications/Wine.app/Contents/Resources/bin/wine app.exe

	exec wine "~/.wine/drive_c/My/program.exe" "-my" "-arguments"
	# The exec commands tell bash to morph into wine with the following arguments, so this is no longer bash running wine, but bash process becoming wine.
	# The PID remains. You don't have two processes running.

If error like `err:module:import_dll Library MSVCP140.dll` check if a winetrick is not required like `vcrun2015`

Some interesting files:

	~/Library/Application Support/Wine/winetricks
	~/Library/Application Support/Wine/winetricks.plist
	/Applications/Wine.app/Contents/Frameworks/WBottler.framework/Versions/A/Resources/applywinetricks.sh
	/Applications/Wine.app/Contents/Frameworks/WBottler.framework/Versions/A/Resources/winetricksextract.sh

- [command line - Transparently run wine programs - Unix & Linux Stack Exchange](http://unix.stackexchange.com/questions/70681/transparently-run-wine-programs)

If winetrick don't install (error log contains `pathchk: illegal option -- P`) get `https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks` and replace content of `~/Library/Application Support/Wine/winetricks`

`Wine.app` start `winetrick` with a `$PATH` as it's original value (for any spawned process), it's why you need when debug a wine app on macOS, always start with **absolute path** in Terminal: `/Applications/MyApp.app/Contents/MacOS/startwine`. See [Define PATH globaly](macOS#define-path-globaly)

> With the introduction of SIP, all environment variables matching DYLD_* will be stripped before executing a restricted binary.

> it seems SIP strips env variables if an application is launched from another application

- [Compiling Wine 1.9 from scratch on macOS with Retina mode | myByways](http://mybyways.com/blog/compiling-wine-from-scratch-on-macos-with-retina-mode)
- [Creating a wine.app bundle manually | myByways](http://mybyways.com/blog/creating-a-wine-app-bundle-manually)
- [Problem compiling Wine second time around | myByways](http://mybyways.com/blog/problem-compiling-wine-second-time-around)
- [WineBottler | Tech Specs](http://winebottler.kronenberg.org/specifications)
- [MacOS/Building - WineHQ Wiki](https://wiki.winehq.org/MacOS/Building)

`WINEDLLOVERRIDES`:

- `man wine`
- [Wine User's Guide - WineHQ Wiki](https://wiki.winehq.org/Wine_User%27s_Guide#WINEDLLOVERRIDES.3DDLL_Overrides)
- [FAQ - WineHQ Wiki](https://wiki.winehq.org/FAQ#How_can_I_prevent_Wine_from_changing_the_filetype_associations_on_my_system_or_adding_unwanted_menu_entries.2Fdesktop_links.3F) - it's written `winemenubuilder.exe=d` by `d` is not a valid load order value
- https://github.com/wine-mirror/wine/blob/master/dlls/ntdll/loadorder.c `parse_load_order`
- `*mscoree=native`, `mscoree`, `mshtml`, `winemenubuilder.exe=native`

### Wine DLL overrides

Error:

> err:module:import_dll Library mscoree.dll (which is needed by L"C:\\.....exe") not found

Open the Wine app and select (change) the app Template prefix (to edit).
Configuration > Libraries > Edit "DLL Overrides" to remove `mscoree` and `mshtml`:
See also remove in Control Panel > Add / remove Apps /Application > Update / Delete
Or edit `*.app/Contents/Resources/wineprefix/user.reg` and remove lines `"mscoree"=""` and `"mshtml"=""` (or set value as `n,b`) in section `[Software\\Wine\\DllOverrides]`.
**Before restart the application, the prefix created by the app `~/Application Support/*_xxxxxxxxxxxx` need to be removed.**
See also the field "Dll Override" in WineBottler. `mscoree,mshtml=n,b`, `mscoree=n,b;mshtml=n,b`. But [`bottler.sh` `winebottlerOverride`](https://bitbucket.org/winebottler/winebottler/src/master/WBottler/Resources/bottler.sh) ← [`default.sh`](https://bitbucket.org/winebottler/winebottler/src/master/WBottler/Resources/default.sh) ← [`WBottler`](https://bitbucket.org/winebottler/winebottler/src/master/WBottler/WBottler.m) ← [`WCustomController`](https://bitbucket.org/winebottler/winebottler/src/master/WineBottler/WCustomController.m) doesn't work as expected (`winebottlerWinetricks` where some dlls override are applied as builtin is right before `winebottlerInstall`)?

See [Wine User' Guide - WineHQ Wiki](https://wiki.winehq.org/Wine_User%27s_Guide#DLL_Overrides) and [Wine User' Guide - WineHQ Wiki](https://wiki.winehq.org/Wine_User%27s_Guide#Notes_About_System_or_Missing_DLLs)

Error:

> System.MissingMethodException: Method not found: '!!0[] System.Array.Empty()'.
Install .Net Framwork 4.6 with winetrick `dotnet46` (instead of `dotnet40`, will be installed with 4.6)

### Wine libraires issues

Error examples:

> Wine cannot find the FreeType font library.  To enable Wine to
> use TrueType fonts please install a version of FreeType greater than
> or equal to 2.0.5.
> http://www.freetype.org

> err:module:load_builtin_dll failed to load .so lib for builtin L"GLU32.dll": dlopen(/Applications/Wine.app/Contents/Resources/lib/wine/glu32.dll.so, 258): Library not loaded: /usr/X11/lib/libGLU.1.dylib
>   Referenced from: /Applications/Wine.app/Contents/Resources/lib/wine/glu32.dll.so
>   Reason: image not found

**Wine use i386 libs only.** Provided libs or compiled are often only for the local architecture (ex: x86_64 only) and not mixed version.

If install libs with MacPorts, builded for the local architecture, you need to build for i386 too: [howto/buildUniversal – MacPorts](https://trac.macports.org/wiki/howto/buildUniversal).
See also `universal_archs` in [`macports.conf)`](https://guide.macports.org/chunked/internals.configuration-files.html#internals.configuration-files.macports-conf), [`variants.conf`](https://guide.macports.org/chunked/internals.configuration-files.html#internals.configuration-files.variants-conf) and [Is MacPorts Universal?](https://trac.macports.org/wiki/FAQ#universal)).

**Install [X11 (XQuartz version)](#x11) could also fix the issue.** But you often don't wan't to mix XQuartz with MacPort or Brew versions.

Found which port build libs:

	port provides <filename>
	#see also port contents "*"

See dependents and dependencies:

	port dependents <portname>
	# or port echo dependentof:<portname>

	# See https://trac.macports.org/wiki/FAQ#alldependencies	
	port rdeps <portname>

	sudo port clean --all --archive <portname>
	sudo port -n upgrade --force <portname> +universal

Find lib locations:

	find / \( -name "<filename>" -o -name "<filename_symlink>" \) 2>/dev/null

Check if the lib is i386 compatible `Mach-O dynamically linked shared library i386`:

	file <filename>

See libs dependencies:

	otool -L <filename>

It's could needed to change the lib lookup location:

	install_name_tool -change /Users/mike/Documents/wine2/usr/lib/libfreetype.6.dylib /usr/lib/libfreetype.6.dylib /Applications/Wine.app/Contents/Resources/lib/libfreetype.6.dylib

- [Fun with rpath, otool, and install_name_tool – Chris Hamons – Medium](https://medium.com/@donblas/fun-with-rpath-otool-and-install-name-tool-e3e41ae86172)
- [WINE for Darwin and Mac OS X / Re: \[Darwine\] Problem with Darwine 0.9.3DP on OSX86 10.4.1](https://sourceforge.net/p/darwine/mailman/message/6359349/)
- [Linking an OSX external bundle with a .dylib library | How To - Step-By-Step Guides To Tasks In LiveCode | LiveCode Lessons](http://lessons.livecode.com/m/4071/l/15029-linking-an-osx-external-bundle-with-a-dylib-library)

To debug dylib loaded, edit bash script `MyWineApp.app/Contents/MacOS/startwine` of the bottled Wine app, prefix `"$WINEUSRPATH/bin/wine"....` with `DYLD_PRINT_LIBRARIES=1 `: `DYLD_PRINT_LIBRARIES=1 "$WINEUSRPATH/bin/wine...`

	otool -L /Applications/Wine.app/Contents/Resources/lib/libfreetype.6.dylib

## TexturePacker

http://texturepacker.software.informer.com/download/

`TexturePacker --install-license <name_of_the_license_file>`

`~/.config/code-and-web/TexturePacker.conf`

`~/Library/Preferences/de.code-and-web.TexturePacker.plist` cloned self in `licensing.data.rawdata` (clone with `Signature` -  rawdata sha256 Encryption check)

After the canonical 7 days of time trial, you will have extended time trial until the date you wrote

	firstStart = false;
	licensing.data.expiryDate = "2016-10-17";
	licensing.data.freeUpdatesUntil = "2999-01-01";
	licensing.data.licenseType = "trial";
	licensing.data.licensee = "trial user";//"essential"
	licensing.trialExpired = false;

If not match signature, Sprites replace with red message can appears (watermarks)

Windows: `HKEY_CURRENT_USER\Software\code-and-web.de\TexturePacker\licensing\data` set to `expiryDate=2999-01-01` and in `rawdata` and `trialExpired` in `HKEY_CURRENT_USER\Software\code-and-web.de\TexturePacker\licensing`

Uninstall the application from your computer (using Appzapper, AppCleaner, etc. delete everything related to that App like `de.code-and-web.TexturePacker.plist`). Install TexturePacker again and try to bypass license expiration.

	sudo chmod 444 /Users/youruser/Library/Preferences/de.code-and-web.TexturePacker.plist

In hosts (not required):

	127.0.0.1	secure.codeandweb.com

	%licensing.data.computerId%
	%autoUpdateCheck%
	%date% = current timestamp in ms
	https://www.codeandweb.com/releases/texturepacker/updatecheck.php?ex=pixijs&o=mac&ov=10.12&b=no&l=&c=%licensing.data.computerId%&v=4.2.3&lt=trial&m=%autoUpdateCheck%&bit=64&s=%date%

	POST https://secure.codeandweb.com/rpc/RPC.php
	call=getTrialLicense&computerId=%licensing.data.computerId%&osName=MacOS&osVersion=10.12&product=TexturePacker&version=4.2.3&security_request_hash=f078701acfa82bbaad363e02d93e84dd

- [CodeAndWeb - Game Developer Tools + Activation](https://leakforums.net/thread-625920)

## SWFTools

See [Convert (simple) SWF to PDF](https://gist.github.com/mems/5301297) for how to compile `gfx2gfx`

## VMware

- `/Applications/VMware Fusion.app/Contents/Library/isoimages/*.iso`
- [Installing VMware Tools in a Fusion virtual machine running Windows (1003417) | VMware KB](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1003417)

## TextEdit

Unsaved files:

	~/Library/Containers/com.apple.TextEdit/Data/Library/Autosave Information

## TextMate

Unsaved files:

	~/Library/Application Support/TextMate/Session

## Google AppEngine

https://cloud.google.com/appengine/docs/php/download

Installed files:

	~/.appcfg_oauth2_tokens
	/usr/local/bin/_php_runtime.py
	/usr/local/bin/_python_runtime.py
	/usr/local/bin/api_server.py
	/usr/local/bin/appcfg.py
	/usr/local/bin/backends_conversion.py
	/usr/local/bin/bulkload_client.py
	/usr/local/bin/bulkloader.py
	/usr/local/bin/dev_appserver.py
	/usr/local/bin/download_appstats.py
	/usr/local/bin/endpointscfg.py
	/usr/local/bin/gen_protorpc.py
	/usr/local/bin/php_cli.py
	/usr/local/bin/remote_api_shell.py
	/usr/local/bin/run_tests.py
	/usr/local/bin/wrapper_util.py
	/usr/local/google_appengine
	/usr/local/google_appengine.old

## TotalFinder

Finder Replacement, https://asepsis.binaryage.com/

Asepsis feature store `.DS_Store` files in `/usr/local/.dscache/`

## Kodi

Add-on dev:

- [Python development - Official Kodi Wiki](http://kodi.wiki/view/Python_development#PyDocs)
- [InfoLabels - Official Kodi Wiki](http://kodi.wiki/view/InfoLabels)
- [Welcome to SimplePlugin documentation! — SimplePlugin 2.3.1 documentation](http://romanvm.github.io/script.module.simpleplugin/index.html)
- [HOW-TO:Add a new view type to the skin - Official Kodi Wiki](http://kodi.wiki/view/HOW-TO:Add_a_new_view_type_to_the_skin)
- [xbmc/addons/skin.estuary/xml at master · xbmc/xbmc](https://github.com/xbmc/xbmc/tree/master/addons/skin.estuary/xml)

Possible themes:

- Amber
- Confluence (default)
- Aeon Nox
- Fire TV (fTV) http://forum.kodi.tv/showthread.php?tid=207475
- Xperience1080
- Titan

A file manager is included (to copy/past/rename/etc. files): System > File manager

- [Userdata - Official Kodi Wiki](http://kodi.wiki/view/userdata)

See also `sources.xml`. See also [Store passwords](#store-passwords)

	<!-- No complete -->
	<source>
		<name>Movies</name>
		<path pathversion="1">smb://user:password@192.168.3.4/Medias/Movies/</path>
		<allowsharing>true</allowsharing>
	</source>

- [Custom video entries - Official Kodi Wiki](http://kodi.wiki/view/Custom_video_entries)
- [NFO files - Official Kodi Wiki](http://kodi.wiki/view/NFO_files#NFO_Examples)
- Official Remote Apps [Downloads | Kodi](https://kodi.tv/download/)
- [Install SuperRepo - Worlds largest Kodi addons repository](https://superrepo.org/get-started/)
- Refreshing the library [Set content and scan - Official Kodi Wiki](http://kodi.wiki/view/Set_content_and_scan#Refreshing_the_library)
- Example of config files [XBMC/Kodi – Einrichtung der Medienquellen über Kommandozeile – www.it-system.info](http://www.it-system.info/xbmc-kodi-einrichtung-der-medienquellen-ueber-kommandozeile/)

On Android: 

`$SYSTEMDATA` should be something like `/storage/emulated/0/Android/data/org.xmbc.kodi/files/.kodi`. See [System data - Official Kodi Wiki](http://kodi.wiki/view/Systemdata)
`$USERDATA` should be something like `$SYSTEMDATA/userdata`. See [Userdata - Official Kodi Wiki](http://kodi.wiki/view/userdata)

If display "Add-on migration in progress - please wait", remove (or rename) the folder `$SYSTEMDATA/addons`

Remove control with [Web interface](https://kodi.wiki/view/Web_interface): use a port like 9080 (default could be already used or blocked)



### Set up centralized database in Kodi

Require an external access to MySQL/MariaDB server with full rights (create and drop tables)

Here prefixes `kodi_video` and `kodi_music` are defined (Ex. Kodi will create `kodi_videoXX` database, where `XX` is the [database version](http://kodi.wiki/view/Database_version))

Initial configuration (to creating the database, can be disabled later), require all granted privileges on target database

	GRANT ALL ON *.* TO 'kodi';

After install or upgrade use:

	GRANT ALL ON `MyMusic%`.* TO 'kodi';
	GRANT ALL ON `MyVideos%`.* TO 'kodi';

`$USERDATA/advancedsettings.xml`:

	<advancedsettings>
		<videodatabase>
			<type>mysql</type>
			<host>192.168.3.4</host>
			<port>3306</port>
			<user>kodi</user>
			<pass>password</pass>
			<name>kodi_video</name>
		</videodatabase>
		<musicdatabase>
			<type>mysql</type>
			<host>192.168.3.4</host>
			<port>3306</port>
			<user>kodi</user>
			<pass>password</pass>
			<name>kodi_music</name>
		</musicdatabase>
		<videolibrary>
			<importwatchedstate>true</importwatchedstate>
			<importresumepoint>true</importresumepoint>
		</videolibrary>
	</advancedsettings>

- [MySQL/Setting up MySQL - Official Kodi Wiki](http://kodi.wiki/view/MySQL/Setting_up_MySQL)
- [MySQL/Upgrading - Official Kodi Wiki](http://kodi.wiki/view/MySQL/Upgrading#Making_sure_Kodi_can_update_the_library)
- [MySQL - MrMC Wiki](http://wiki.mrmc.tv/index.php/MySQL#Restricting_MySQL_access_rights)

### Store passwords in Kodi

SMB error message `operation not permitted`

`$USERDATA/passwords.xml`:

	<passwords>
		<path>
			<from pathversion="1">smb://computername_or_ipaddress/</from>
			<to pathversion="1">smb://username:password@computername_or_ipaddress/</to>
		</path>
	</passwords>

Or in `$USERDATA/sources.xml`:

	<path>smb://domain;username:password@computername_or_ipaddress/sharename/path</path>

- [Log file/Advanced - Official Kodi Wiki](http://kodi.wiki/view/Log_file/Advanced#Password_warning)
- [MySQL/Setting up Kodi - Official Kodi Wiki](http://kodi.wiki/view/MySQL/Setting_up_Kodi#Make_files_accessible_over_the_network)
- [MySQL/Sync other parts of Kodi - Official Kodi Wiki](http://kodi.wiki/view/MySQL/Sync_other_parts_of_Kodi#Network_share_passwords)

## TinyMediaManager

You need to donate to unlock Kodi Scraper. See https://github.com/tinyMediaManager/tinyMediaManager/blob/master/src/main/java/org/tinymediamanager/core/License.java

But python scraper are not supported

1. `$TMM_APP/kodi_scraper/` or `$TMM_APP/Contents/Resources/Java/kodi_scraper/`
2. `%AppData%\`, `~/Library/Application Support/` or `~/` inside `Kodi/addons`, `.kodi/addons`, `kodi/addons`, `XMBC/addons`, `.xbmc/` or `xbmc/addons` folder
3. `%ProgramFiles%\`, `%ProgramData%`, `usr/share/`, `/usr/lib/`, `/Applications/Kodi.app/Contents/Resources` or `/Applications/XBMC.app/Contents/Resources` inside `Kodi/addons`, `kodi/addons`, `xbmc/addons` or `XMBC/addons`

Repo of Kobi scrapers: https://github.com/xbmc/repo-scrapers/tree/gotham
Release of plugin: `https://oss.sonatype.org/content/repositories/snapshots/org/tinymediamanager/plugins/scraper-kodi/`

## iTunes

Export to XML playlist: File > Library > Export playlist

Open in a browser then:

	let files = Array.from(document.documentElement.querySelectorAll("plist > dict:nth-of-type(1) > dict:nth-of-type(1) > dict")).reduce((list, track) => (list[track.querySelector(":scope > integer:nth-of-type(1)").textContent] = decodeURIComponent(track.querySelector(":scope > string:nth-last-of-type(1)").textContent.substr(7)), list), {});
	copy(Array.from(document.documentElement.querySelectorAll("plist > dict:nth-of-type(1) > array:nth-of-type(1) > dict:nth-of-type(1) > array:nth-of-type(1) > dict")).map(entry => files[entry.querySelector(":scope > integer:nth-of-type(1)").textContent]).join("\n"));

- [Doug's AppleScripts for iTunes - Super Remove Dead Tracks v4.7 - Official Download Site](http://dougscripts.com/itunes/scripts/ss.php?sp=removedeadsuper)

## Homeworld : Deserts of Kharak

Mac keybinding: replace `Control` by `LeftApple` or `RightApple`

- `default.dokhotkeys`
- [Hotkey Rebinding Documentation - Blackbird Interactive Forums](http://forums.blackbirdinteractive.com/forum/deserts-of-kharak/deserts-of-kharak-general-discussion/4174-hotkey-rebinding-documentation)
- [Unity - Scripting API: KeyCode](https://docs.unity3d.com/ScriptReference/KeyCode.html)

## Age of Empires II

- [Communauté Steam :: Guide :: Playing on Mac using Wine (No Bootcamp, No VM)](http://steamcommunity.com/sharedfiles/filedetails/?id=247537337) - for the HD Edition

## jDownloader

- [JDownloader.org - Official Homepage](http://jdownloader.org/knowledge/wiki/development/get-started)
- [JDownloader - developmentquicktutorial.title](http://beta.jdownloader.org/developmentquicktutorial)
- [JDownloader.org - Official Homepage](http://jdownloader.org/knowledge/wiki/linkprotection/container/dlc-rsdf-and-ccf)
- [JDownloader.org - Official Homepage](http://jdownloader.org/knowledge/wiki/linkprotection/container/dlcapi)
- [How to generate a DLC file for JDownloader? - Stack Overflow](https://stackoverflow.com/questions/8281684/how-to-generate-a-dlc-file-for-jdownloader)
- [On the fly DLC CCF RSDF container decryption - dcrypt.it](http://dcrypt.it/)
- [opendlc/dlc.py at master · posativ/opendlc](https://github.com/posativ/opendlc/blob/master/decrypt/dlc.py)

- svn://svn.jdownloader.org/jdownloader/trunk
- svn://svn.jdownloader.org/jdownloader/browser
- svn://svn.jdownloader.org/jdownloader/MyJDownloaderClient

- [mirror/jdownloader: JDownloader mirror](https://github.com/mirror/jdownloader)
- [svn2github/svn2github-jdownload: GitHub clone of SVN repo svn://svn.jdownloader.org/jdownloader/browser (cloned by http://svn2github.com/)](https://github.com/svn2github/svn2github-jdownload)
- [svn2github/MyJDownloaderClient: GitHub clone of SVN repo svn://svn.jdownloader.org/jdownloader/MyJDownloaderClient (cloned by http://svn2github.com/)](https://github.com/svn2github/MyJDownloaderClient)

Plugins infos are at `jdownloader/src/jd/plugins/hoster`

## Docker

- [Get started with Docker for Mac - Docker Documentation](https://docs.docker.com/docker-for-mac/)
- [Docker Community Edition for Mac - Docker Store](https://store.docker.com/editions/community/docker-ce-desktop-mac)

## Download video on iOS

A 2 minutes timer will kill/stop an application in background

Settings > Luminosity > Autolock > Never

https://forum.videolan.org/viewtopic.php?t=124758

Synology and iOS VLC:

- VLC download with cloud service > DS File
- DS File > Play with VLC (direct click on media file)
- (srt only) DS File > Send a copie > Copy in VLC

## ILSpy

[icsharpcode/ILSpy: .NET Decompiler](https://github.com/icsharpcode/ILSpy)

### Package ILSpy for Mac

Windows Version Info: 7

Select "Copy file (Program) and all files in the folder to the App Bundle" (binaries version)

- no mono nor gecko
- winetrick Net Framework 4.6 `dotnet46`
- Copyright: © ICSharpCode
- version: choose what you want
- Identifier: net.icsharpcode.ilspy
- Category type: Developer Tools
- don't hide install dialog (not work with `dotnet46`, that install version 4 and 4.5)
- save the generated App anywhere else than the folder contains ILSpy.exe (else it will make an infinite loop that copy the content of created app)

## dotPeek

- [dotPeek: Free .NET Decompiler & Assembly Browser by JetBrains](https://www.jetbrains.com/decompiler/)
- [Download dotPeek: Free .NET Decompiler by JetBrains](https://www.jetbrains.com/decompiler/download/#section=standalone)

### Package dotPeek for Mac

execute file (installer)

- no mono nor gecko
- winetrick Net Framework 4.5 `dotnet45`
- Copyright: © JetBrains
- version: choose what you want
- Identifier: net.icsharpcode.ilspy
- windows 7
- don't hide install dialog

## Inkscape

On macOS, Inkscape require [X11](#x11). If it's installed with MacPort, select `/Applications/MacPorts/X11.app` when Inkspace prompt the location of X11.
- [Inkscape 0.92.2 - Mac-Os-X : 107 : Dmg | Inkscape](https://inkscape.org/en/release/0.92.2/mac-os-x/107/dmg/dl/)

## USB Overdrive

Note: Registration key for 3.1 works for 3.3 too.

To force rebuild kernel and extension cache

	sudo kextcache -i /

If the device is not detected, may it's because it's pluged to a USB hub. Try to disconnect and connect again, or try to connect directly (without hub) first, the device should be reconnized by USB Overdrive (see Status tab), then you can connect to the hub

- [©1999-2017 Alessandro Levi Montalcini](http://www.usboverdrive.com/USBOverdrive/Support.html)

## Wireshark

- [srozzo/wireshark-uninstall-osx: Wireshark uninstall script for OS X](https://github.com/srozzo/wireshark-uninstall-osx)
