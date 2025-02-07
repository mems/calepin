## Thunderbird

Wrap lines:

```
mail.compose.wrap_to_window_width = true
mail.wrap_long_lines = false
```

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

[Thunderbird version 91.0 release note](https://www.thunderbird.net/en-US/thunderbird/91.0/releasenotes/): "Movemail support removed". See [Bug 1625741](https://bugzilla.mozilla.org/show_bug.cgi?id=1625741)

The workaround is get the file [`movemail.rdf`](https://github.com/mozilla/releases-comm-central/blob/master/mailnews/base/ispdata/movemail.rdf) and install it in `Thunderbird.app/Contents/MacOS/isp`. Then follow [the instructions to configure an "Unix Mailspool" account](http://askubuntu.com/questions/1916/how-can-i-access-system-mail-in-var-mail-via-thunderbird).
See also:
- [RDF file support drop for direct implementation](https://github.com/mozilla/releases-comm-central/commit/9dfcbbfccada85731e849005e7aa83713580754e#diff-98446bcd20f1b8a4e15ac68e4df90a4912cd03cb91a9d91dc95ea442a8da69a6)
- [Alternative method of reading spool file in Thunderbird without movemail support? : Thunderbird](https://www.reddit.com/r/Thunderbird/comments/pptgvo/alternative_method_of_reading_spool_file_in/)

For `Mail.app`, follow these intructions: [Access local mail via Mail.app - Mac OS X Hints](http://hints.macworld.com/article.php?story=20040313194905606)

## Office

- [Office 2016 Volume Installer findings | Jamf Nation](https://www.jamf.com/jamf-nation/discussions/16761/office-2016-volume-installer-findings)

### Excel

And LibreOffice

**LibreOffice use `;` as values separator in formulas.** And base on language/locale used, the decimal separator could be `.` or `,`

- [Using Flash Fill in Excel](https://support.microsoft.com/en-us/office/using-flash-fill-in-excel-3f9bcf1e-db93-4890-94a0-1578341f73f7)

Conditional Formatting:

- [Excel: Change the row color based on cell value](https://www.ablebits.com/office-addins-blog/2013/10/29/excel-change-row-background-color/)
- [Excel tutorial: Conditional formatting formula in a table](https://exceljet.net/lessons/conditional-formatting-formula-in-a-table)

Formula: Cell coords like `F6` are relative and `$F$6` is absolute (`F$6` or `$F6` are also possible). Relative cells coords are resolved during the formula evaluation, relative to the first one in range, then apply the relative coords to others.

- [You Suck at Excel with Joel Spolsky - YouTube](https://www.youtube.com/watch?v=0nbkaYsR94c)

#### Median formula

| Price ($) | Quantity (unit) |
|-----------|-----------------|
| 1         | 99              |
| 2         | 20              |
| 7         | 3               |
| 10        | 1               |
| Median    | 1$              |

Formula:

`=LOOKUP(-0,5;-PROB(ROW(A1:A100);B1:B100/SUM(B1:B100);ROW(A1:A100);2^20);A1:A100)` where `A1:100` are values and `B1:B100` are quantities.

> This is equivalent to looking up the 50% mark within a column of cumulative percentages. (Data is ordered so that the lookup function can be applied.)

- [Weight Median Help Requested (Part Quantity and Part Weight) : excel](https://www.reddit.com/r/excel/comments/2nadqs/weight_median_help_requested_part_quantity_and/)
- [Median with Quantity Column - ExcelBanter](https://www.excelbanter.com/excel-worksheet-functions/231843-median-quantity-column.html)

#### Average formula

| Price ($) | Quantity (unit) |
|-----------|-----------------|
| 1         | 99              |
| 2         | 20              |
| 7         | 3               |
| 10        | 1               |
| Average   | 1.3821138211$   |

`=SUMPRODUCT(A1:A100;B1:B100)/SUM(B1:B100)` where `A1:100` are values and `B1:B100` are quantities.

- [Calculate the average of a group of numbers - Excel](https://support.office.com/en-us/article/calculate-the-average-of-a-group-of-numbers-e158ef61-421c-4839-8290-34d7b1e68283)

#### Excel seconds to dates

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

**Consider using docker instead:** [docker-compose with php/mysql/phpmyadmin/apache](https://gist.github.com/jcavat/2ed51c6371b9b488d6a940ba1049189b)

### Logs files

Since El Capitain, symlink to a folder no longer work in Console, need to create symlink directly to the log file

```sh
cd ~/Library/Logs
mkdir -p MAMP
cd MAMP
ln -s /Applications/MAMP/logs/*.log .
```

### PHP

There multiple `php.ini` in MAMP.

In non Pro version: You should edit (where `*.*.*` is active PHP version):

`MAMP/bin/php/php*.*.*/conf/php.ini`

An other location:

`MAMP/conf/php*.*.*/php.ini`

But seem not used (any explanations? Regenerated by Pro version from `php.ini` template file?)

MAMP Pro, use also templates : `File > Edit Templates > PHP *.*.* php.ini` (or edit `MAMP/bin/php/php*.*.*/conf/php.ini.temp`)

#### Debugger

```apache
[xdebug]

xdebug.default_enable=1

xdebug.remote_enable=1
xdebug.remote_handler=dbgp
xdebug.remote_host=localhost
xdebug.remote_port=9000
xdebug.remote_autostart=1

zend_extension="/Applications/MAMP/bin/php5/lib/php/extensions/no-debug-non-zts-xxxxxxxx/xdebug.so"
```

### Apache

`MAMP/conf/apache/httpd.conf`

### MySQL

Create `MAMP/conf/my.cnf`

- https://stackoverflow.com/questions/678645/does-mysql-included-with-mamp-not-include-a-config-file
- http://bensch.be/mysql-config-with-mamp

Be carefull of params in `MAMP/conf/startMysql.sh`

- [Server adminstration (Linux) # MySQL (sql server) Fichiers de configuration]()

### PHP Intl lib

```sh
sudo port install php54-intl
```

Copy `/opt/local/lib/php54/extensions/no-debug-non-zts-20100525/intl.so` to `/Applications/MAMP/bin/php/php5.4.10/lib/php/extensions/no-debug-non-zts-20100525/intl.so`

Add in `/Applications/MAMP/bin/php/php5.4.10/conf/php.ini`:

```apache
extension=intl.so
```

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

    ```
	/([0-9a-f,]+\n<\s*<date[^<].*\n---\n>\s*<date.*)/g
	$1\n
    ```
7. Apply `patch import_CA.xml fix.patch`
8. Open the result file and copy/drag&drop entries

Si il est impossible de "Transférer en comptabilité" une opération auxiliaire, recréer le fichier LCB (certaines pièce jointes seront perdues) avec la bonne année

### Unlock LibeCompta

File > (Key Alt) Save as... > "LibéCompta XML" (see also `plutil -convert xml1 -o <output file> <input file>`)
and remove:

```plist
<key>secur</key>
<dict>
	<key>cloture</key>
	<true/>
	<key>clotureDate</key>
	<date>2018-04-30T22:00:00Z</date>
</dict>
```

### LibeCompta Data

Frais kilométriques `/Applications/LibéCompta/Contents/Resources/BNC.plist` et `BIC.plist`

Libellé			Jusqu'à 3000km	De 3001 km à 6000 km	Au-delà de 6000 km
Plus de 5 CV	d x 0,518		(d x 0,067) + 1,351		d x 0,292

Donne :

```plist
<array>
	<integer>518</integer>
	<integer>67</integer>
	<integer>1351</integer>
	<integer>292</integer>
</array>
```

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
4. System: `XP 64bit` or `7 64bit`
5. don't include Mono and Gecko
6. check "Prepare for Distribution / Remove Users" and "Remove installers"
6. DLL Override: `mscoree=n,b;mshtml=n,b` (see [Wine DLL overrides](#wine-dll-overrides))
6. Winetricks: `dotnet40` (or `dotnet45` for v3). Recommanded, but not required: `flash`, `gdiplus`, `ie8`
7. App Bundle:
	Copyright: `© Captvty`
	Version: _use the Captvty version number_
	Identifier: `fr.captvty.captvty`
	Category Type: `Video`
8. Click on Install
9. Save as `Captvty.app` (**but not in the folder of the .exe**)
10. "Wine can't found wine-mono required for .Net application to work correctly": Cancel
10. (.Net Framework 4 Client Installer) Install (restart later)
11. (Flash Installer) Install (without updates)
12. (IE8 Install) Install, (Without updates: Microsoft Update, Malware remover, etc.), restart later
13. (See step 3, if second option choosen) Copy all files from Captvty ZIP to `Captvty.app/Contents/Resources/wineprefix/drive_c/winebottler/` (right click on Captvty.app, see Bundle content)
14. Move/Copy `Captvty.app` to `/Applications`
15. Ready to watch

Note: Version 3 can show an error but works. "Direct" not work

- [CaptvtyV3.sh · master · Paul WOISARD / Captvty script installateur pour Ubuntu · GitLab](https://framagit.org/Paullux/captvty-script-installateur-pour-ubuntu/blob/master/CaptvtyV3.sh) and [Problem with Captvty a french software to see TV - WineHQ Forums](https://forum.winehq.org/viewtopic.php?t=31778)
- [Foire aux question | Captvty](http://captvty.fr/faq#linux)

## Filebot

### Build filebot for Mac

1. Download https://github.com/filebot/filebot/archive/master.zip
2. Check if you have Java JDK 8u91+ and ant installed
3. Download http://ant.apache.org/ivy/download.cgi (binary version) and https://mvnrepository.com/artifact/org.tukaani/xz/1.0 (Download JAR)
4. Uncompress and copy `ivy-2.X.X.jar` in `lib/jars`
5. (optional) update in `appbundle-maspkg-core` `<param name="application.mode" value="Rename|Episodes|SFV|Filter|List" />` to `<param name="application.mode" value="Rename|Episodes|SFV|Filter|List|Subtitles" />`
6. (optional) change

    ```xml
	<target name="revision" depends="init">
		<exec executable="git" outputproperty="revision" failonerror="true">
			<arg line="rev-list --count master" />
		</exec>
		<echo>Revision: ${revision}</echo>
	</target>
    ```

	to (number of https://github.com/filebot/filebot commits)

    ```xml
	<target name="revision" depends="init">
		<echo>Revision: 4498</echo>
	</target>
    ```
6. start `ant -lib lib/jars resolve fatjar appbundle` in the project folder
7. could require on macOS to start following commands before get GUI works

```sh
java -jar /Applications/FileBot.app/Contents/Java/FileBot_4.7.jar -help
java -jar FileBot.jar -script fn:artwork.tvdb /path/to/tvshows_dir/
```

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

```sh
#!/bin/sh
/Developer/SDKs/android-sdk/tools/android &
exit
```

Install an application on virtual device

```sh
adb install /path/to/app.apk
```

```sh
$ANDROID_SDK/platform-tools/adb
```

- https://github.com/PaulKinlan/chromium-android-installer
- [Chrome APKs - APKMirror](http://www.apkmirror.com/apk/google-inc/chrome/)
- [Android Debug Bridge | Android Studio](https://developer.android.com/studio/command-line/adb.html)

## IntelliJ Applications

Aka WebStorm, PhpStorm, IntelliJ IDEA

Grunt task output `Task "watch" passed` or `Task "watch" failed` are handled by the app: [Grunt feedback : WEB-11713](https://youtrack.jetbrains.com/issue/WEB-11713#comment=27-718038)

Use Bash shell on Windows: in "Tools > Terminal" set "Shell path" to `C:\Program Files\Git\bin\bash.exe --login -i`

[Shell Script](https://plugins.jetbrains.com/plugin/13122-shell-script) Task Run/Debug Configuration (see [Shell scripts | IntelliJ IDEA](https://www.jetbrains.com/help/idea/shell-scripts.html)) on Windows without "Execute in the terminal" enabled generate the error `Error running '<task_name>': Cannot run program "\bin\sh" (in directory "<task_working_directory>"): CreateProcess error=2, The system cannot find the file specified`. To fix this issue, create a junction: `mklink /J "C:\bin" "C:\Program Files\Git\bin"`. See also https://youtrack.jetbrains.com/issue/IDEA-277486

- Command keyboard shortcut match only US layout: [National keyboard layouts support : IDEA-165950](https://youtrack.jetbrains.com/issue/IDEA-165950#comment=27-2053321)
- Support ANSI sequences in Run tool (use terminal for NodeJS registry key, at least in PhpStorm 2018.3 and WebStorm 2018.2): [Console output manipulation is not supported when using WebStorm Run : IDEA-154313](https://youtrack.jetbrains.com/issue/IDEA-154313#focus=streamItem-27-2842206.0-0)
- Help > Find Action > Check "UML support" on, right click on file or folder > Diagram. [Module Dependency Diagrams - Help | PhpStorm](https://www.jetbrains.com/help/phpstorm/module-dependency-diagram.html)

To add options in vmoption: [Help > Edit Custom VM Options...](https://intellij-support.jetbrains.com/hc/en-us/articles/206544869)

Plugins:

- [Implementing a Parser and PSI / IntelliJ Platform SDK DevGuide](https://www.jetbrains.org/intellij/sdk/docs/reference_guide/custom_language_support/implementing_parser_and_psi.html)
- [intellij-plugins/AngularJS/src/org/angularjs/lang at master · JetBrains/intellij-plugins](https://github.com/JetBrains/intellij-plugins/tree/master/AngularJS/src/org/angularjs/lang)

List of files in search:

```js
// In a webpage, add the following code in dev tools console, then past in the page the copied content of "Export to text file" of the Find Window
document.addEventListener("paste", function(event) {
  const lines = event.clipboardData.getData("Text").split(/\r?\n/);
  const PATH_PREFIX = " ".repeat(4 * 3);
  const FILE_PREFIX = " ".repeat(4 * 4);
  const USAGE_PREFIX = " ".repeat(4 * 5);
  const pathSep = "\\";
  const regexp = /<script.*?src=["']((?:@|https?:|<%=).*?)["'].*?>/i;// TODO retrive it autmatically "new RegExp(parsedSearch)" (but can't be detected if it's a regexp or not
  const usages = [];
  let path = "";
  let file = "";

  for(const rawLine of lines){
    const [, prefix = "", line = rawLine] = rawLine.match(/^((?: {4})*)(.*)$/) || [];

    switch(prefix){
      // indent 3, path + usage count
      case PATH_PREFIX:
        path = line.match(/^(.*?)(\s*\(.*?\))?$/)[1];
        continue;
      // indent 4, filename + usage count
      case FILE_PREFIX:
        file = line.match(/^(.*?)(\s*\(.*?\))?$/)[1];
        continue;
      // indent 5, line usage + extract (always one line)
      case USAGE_PREFIX:
        const [, lineNum, extract] = line.match(/^(\d+)\s+(.*)$/);
        usages.push({file: `${path}${pathSep}${file}`, line: lineNum, extract});
    }
  }

  // https://stackoverflow.com/questions/6020714/escape-html-using-jquery/6020820#6020820
  function e(value){
    const map = {
      '&': '&amp;',
      '<': '&lt;',
      '>': '&gt;',
      '"': '&quot;',
      "'": '&#x27;',
      '/': '&#x2F;'
    };

    return value.replace(/[&<>"'\/]/g, c => map[c]);
  }

  // const result = [...new Set(usages.map(({file}) => file))];
  // document.body.innerHTML = `<table>${result.map(item => `<tr><td>${e(item)}</td></tr>`).join("")}</table>`;

  const result = usages.map(({file, line, extract}) => ({file: `${file}:${line}`, extract: regexp.exec(extract)[1]}));
  const indexes = ["file", "extract"];
  document.body.innerHTML = `<table><tr>${indexes.map(index => `<td>${e(index).join("")}</td>`)}</tr>${result.map(item => `<tr>${indexes.map(index => `<td>${e(item[index] || "").join("")}</td>`)}</tr>`).join("")}</table>`;
});
```

### Configuration files

- [Directories used by the IDE to store settings, caches, plugins and logs – IDEs Support (IntelliJ Platform) | JetBrains](https://intellij-support.jetbrains.com/hc/en-us/articles/206544519)

### Scope

Settings > Appearance & Behavior > Scopes

`file[group:Libraries]:*/||file[Fnaccom-18.1-FR-BE-CH]:*/`

### Subprojects

Aka modules, WebStorm

Create in the subproject directory a file `.idea/MODULE_NAME.iml` (where `MODULE_NAME` can be whatever, can contains spaces, will be prefixed by the folder name in the root project "name-of-directory [name-of-subproject]" in the IDE) that contains :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<module type="WEB_MODULE" version="4">
	<component name="NewModuleRootManager">
		<content url="file://$MODULE_DIR$">
			<!--<excludeFolder url="file://$MODULE_DIR$/Src/www/Assets/dist" />-->
		</content>
		<orderEntry type="inheritedJdk" />
		<orderEntry type="sourceFolder" forTests="false" />
	</component>
</module>
```

Then open the project in "This Window" ("Attach"):

https://www.jetbrains.com/help/webstorm/opening-multiple-projects.html

It will add a new line in the root project `.idea/modules.xml`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project version="4">
	<component name="ProjectModuleManager">
		<modules>
			<module fileurl="file://$PROJECT_DIR$/path/to/module/.idea/MODULE_NAME.iml" filepath="$PROJECT_DIR$/path/to/module/.idea/MODULE_NAME.iml" />
		</modules>
	</component>
</project>
```

You can use a subproject folder with the attribute `group` (can contains `/` for multiple subfolder)

Modules order can't be changed: [How to order modules in intellij-idea? - Stack Overflow](https://stackoverflow.com/questions/31245847/how-to-order-modules-in-intellij-idea)

You can change in the root project `.idea/PROJECT_NAME.iml` to define module order (and hide files/folders of the root project by remove `<content...`)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<module type="WEB_MODULE" version="4">
	<component name="NewModuleRootManager">
		<orderEntry type="module" module-name="MODULE1_NAME" />
		<orderEntry type="module" module-name="MODULE2_NAME" />
	</component>
</module>
```

- [Managing Project under Version Control - Help | IntelliJ IDEA](https://www.jetbrains.com/help/idea/managing-projects-under-version-control.html)
- [Configuring project - Help | IntelliJ IDEA](https://www.jetbrains.com/help/idea/configuring-projects.html)
- [How to add a pure React project to an existing solution in Rider - Stack Overflow](https://stackoverflow.com/questions/66817169/how-to-add-a-pure-react-project-to-an-existing-solution-in-rider)

### External Tool

Aka Run/Debug Configuration for command line

There is not way to add a command line command or a process directly with Run/Debug. But you can choose the "interpreter" (ex: "Node interpreter" for a Node task) or use "External Tool" (Settings > Tools > External Tool)

`cmd.exe` with parameters `/C "echo test"`

To start powershell as admin (as regular user):

```
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -Command "Start-Process powershell \"-ExecutionPolicy Bypass -NoProfile -NoExit -Command `\"cd \`\"$ProjectFileDir$\10-Front\Tools\Scripts\Dev\Dev-Front\Src\`\"`\"\" -Verb RunAs"
```

- [Can I run a batch file (.bat) from within the IDE? – IDE Support (IntelliJ Platform) | JetBrains](https://intellij-support.jetbrains.com/hc/en-us/community/posts/207057025-Can-I-run-a-batch-file-bat-from-within-the-IDE-)
- [BashSupport - Bash plugin for IntelliJ / WebStorm / PyCharm | IntelliJ plugin development - www.plugin-dev.com](https://www.plugin-dev.com/project/bashsupport/)
- [PowerShell: Running a command a Administrator - Stack Overflow](https://stackoverflow.com/questions/7690994/powershell-running-a-command-as-administrator/39838527#39838527)

### Ignore files and folders

Index, hide in tree view

- Editor > File Types > Ignored Files and Folders
- Context Menu > Mark Folder As... > Excluded
- Settings/Preferences > Directories
- Context Menu > Tools > Stop Index

- [rider - How to excluder a folder from search and indexing (JetBrains IDEs)? - Stack Overflow](https://stackoverflow.com/questions/66059572/how-to-excluder-a-folder-from-search-and-indexing-jetbrains-ides)

## Adobe

### Adobe Creative Cloud

- install the app from Adobe Creative Cloud app "try", but do not open it untill Adobe Zii patch applied
- [Download Adobe Creative Cloud apps | Free Adobe Creative Cloud trial](https://www.adobe.com/creativecloud/desktop-app.html)
- [Adobe Zii](https://www.reddit.com/r/AdobeZii/)
	- [\[v4.5.0, v5.3.2, v6.1.7, v7.0.0\] Adobe Zii – Easiest Adobe CC all products Universal crack patcher for Mac | AppNee Freeware Group.](https://appnee.com/adobe-zii/)
	- [Adobe Zii for macOS – Adobe Zii](https://tntzii.com/mainhome-latestij/)
- CCMaker
- "MyApp.app is corrupted, can't be opened, you should move it to the trash" and "from unidentified developers" prompts: `sudo xattr -cr "MyApp.app"` (remove quarantie attribute)
- Adobe Creative Cloud Desktop on macOS create secured notes in keychains. "Open Keychain Access, click on Login on the left, then Secure Notes at the top. Select and delete anything with Adobe in the name. Should stop the popups for a while."
- [Use the Creative Cloud Cleaner tool to solve installation problems](https://helpx.adobe.com/creative-cloud/kb/cc-cleaner-tool-installation-problems.html#anameruncccleanertoolformacaUseCreativeCloudCleanertoolformacOS) - Creative Cloud Cleaner tool
- `sudo /usr/bin/codesign –force –deep –sign – /path/to/MyApp.app` `sudo codesign -fs – /Applications/Adobe\ Premiere\ Pro\ 2022/Adobe\ Premiere\ Pro\ 2022.app/Contents/Frameworks/Registration.framework/Versions/A/Registration`
- [Download Adobe Creative Cloud apps | Free Adobe Creative Cloud trial](https://www.adobe.com/creativecloud/desktop-app.html)

For RiD versions (ex: [Adobe Photoshop 2023 - Cmacked](https://cmacked.com/adobe-photoshop-2023/)):

1. use Creative Cloud cleaner Tool to remove previous version
2. install AntiCC
3. install the app (can require to execute directly `Install.app/Contents/MacOS/Install` if you get "Error The installation cannot continue as the installer file may be damaged. Download the installer file again.")
4. if the trial was not started, open the app then start the trial (as business team don't require credit card)
4. install the patch

Use firewall bock `Core Sync.app`, `CCXProcess.app`, `CC Troubleshooter.app`, `CCLibrary.app`, `Creative Cloud.app`, `Creative Cloud Helper.app`. See [Block connections to your Mac with a firewall - Apple Support](https://support.apple.com/guide/mac-help/block-connections-to-your-mac-with-a-firewall-mh34041/mac).

- [Camera Raw plug-in installer](https://helpx.adobe.com/camera-raw/kb/camera-raw-plug-in-installer.html)

```
# From https://www.reddit.com/r/AdobeZii/comments/z67rpm/potential_fix_for_adobe_genuine_software_popup_on/
127.0.0.1 ic.adobe.io
127.0.0.1 wip.adobe.com
127.0.0.1 adobeereg.com
127.0.0.1 wip1.adobe.com
127.0.0.1 wip2.adobe.com
127.0.0.1 wip3.adobe.com
127.0.0.1 wip4.adobe.com
127.0.0.1 3dns.adobe.com
127.0.0.1 ereg.adobe.com
127.0.0.1 bam.nr-data.net
127.0.0.1 practivate.adobe
127.0.0.1 ood.opsource.net
127.0.0.1 crl.verisign.net
127.0.0.1 3dns-1.adobe.com
127.0.0.1 3dns-2.adobe.com
127.0.0.1 3dns-3.adobe.com
127.0.0.1 3dns-4.adobe.com
127.0.0.1 hl2rcv.adobe.com
127.0.0.1 genuine.adobe.com
127.0.0.1 www.adobeereg.com
127.0.0.1 www.wip.adobe.com
127.0.0.1 www.wip1.adobe.com
127.0.0.1 www.wip2.adobe.com
127.0.0.1 www.wip3.adobe.com
127.0.0.1 www.wip4.adobe.com
127.0.0.1 ereg.wip.adobe.com
127.0.0.1 activate.adobe.com
127.0.0.1 adobe-dns.adobe.com
127.0.0.1 ereg.wip1.adobe.com
127.0.0.1 ereg.wip2.adobe.com
127.0.0.1 ereg.wip3.adobe.com
127.0.0.1 ereg.wip4.adobe.com
127.0.0.1 cc-api-data.adobe.io
127.0.0.1 practivate.adobe.ntp
127.0.0.1 practivate.adobe.ipp
127.0.0.1 practivate.adobe.com
127.0.0.1 adobe-dns-1.adobe.com
127.0.0.1 adobe-dns-2.adobe.com
127.0.0.1 adobe-dns-3.adobe.com
127.0.0.1 adobe-dns-4.adobe.com
127.0.0.1 lm.licenses.adobe.com
127.0.0.1 hlrcv.stage.adobe.com
127.0.0.1 prod.adobegenuine.com
127.0.0.1 practivate.adobe.newoa
127.0.0.1 activate.wip.adobe.com
127.0.0.1 activate-sea.adobe.com
127.0.0.1 uds.licenses.adobe.com
127.0.0.1 k.sni.global.fastly.net
127.0.0.1 activate-sjc0.adobe.com
127.0.0.1 activate.wip1.adobe.com
127.0.0.1 activate.wip2.adobe.com
127.0.0.1 activate.wip3.adobe.com
127.0.0.1 activate.wip4.adobe.com
127.0.0.1 na1r.services.adobe.com
127.0.0.1 lmlicenses.wip4.adobe.com
127.0.0.1 na2m-pr.licenses.adobe.com
127.0.0.1 wwis-dubc1-vip60.adobe.com
127.0.0.1 workflow-ui-prod.licensingstack.com
127.0.0.1 1b9khekel6.adobe.io
127.0.0.1 adobe-dns-01.adobe.com
127.0.0.1 adobe.demdex.net
127.0.0.1 adobe.tt.omtrdc.net
127.0.0.1 adobedc.demdex.net
127.0.0.1 adobeid-na1.services.adobe.com
127.0.0.1 assets.adobedtm.com
127.0.0.1 auth-cloudfront.prod.ims.adobejanus.com
127.0.0.1 auth.services.adobe.com
127.0.0.1 cai-splunk-proxy.adobe.io
127.0.0.1 cc-cdn.adobe.com
127.0.0.1 cc-cdn.adobe.com.edgekey.net
127.0.0.1 cclibraries-defaults-cdn.adobe.com
127.0.0.1 cclibraries-defaults-cdn.adobe.com.edgekey.net
127.0.0.1 cn-assets.adobedtm.com.edgekey.net
127.0.0.1 crlog-crcn.adobe.com
127.0.0.1 crs.cr.adobe.com
127.0.0.1 edgeproxy-irl1.cloud.adobe.io
127.0.0.1 ethos.ethos02-prod-irl1.ethos.adobe.net
127.0.0.1 geo2.adobe.com
127.0.0.1 lcs-cops.adobe.io
127.0.0.1 lcs-robs.adobe.io
127.0.0.1 pv2bqhsp36w.prod.cloud.adobe.io
127.0.0.1 services.prod.ims.adobejanus.com
127.0.0.1 ssl-delivery.adobe.com.edgekey.net
127.0.0.1 sstats.adobe.com
127.0.0.1 stls.adobe.com-cn.edgesuite.net
127.0.0.1 stls.adobe.com-cn.edgesuite.net.globalredir.akadns.net
127.0.0.1 use-stls.adobe.com.edgesuite.net
127.0.0.1 pv2yt8sqmh0.prod.cloud.adobe.io
127.0.0.1 a1815.dscr.akamai.net
127.0.0.1 e4578.dscd.akamaiedge.net
127.0.0.1 fp2e7a.wpc.phicdn.net
127.0.0.1 cctypekit.adobe.io
127.0.0.1 ph0f2h2csf.adobe.io
127.0.0.1 vcorzsld2a.adobe.io
127.0.0.1 9ngulmtgqi.adobe.io
127.0.0.1 r5hacgq5w6.adobe.io
127.0.0.1 4vzokhpsbs.adobe.io
127.0.0.1 69tu0xswvq.adobe.io
127.0.0.1 vajcbj9qgq.adobe.io
127.0.0.1 dyzt55url8.adobe.io
127.0.0.1 3ca52znvmj.adobe.io
127.0.0.1 7m31guub0q.adobe.io
```

> At first this didn't work for me, but I fixed it by manually finding the new address that Photoshop was using and adding it to the bottom of this hosts file. This approach doesn't require Radio Silence (which ultimately didn't work for me), and it's actually a relatively simple process:
>
> 1. Make sure PS is closed.
> 2. Download and install [Wireshark](https://www.wireshark.org/).
> 3. Start scanning traffic in Wireshark (watch up to 1:45 in [this video](https://www.youtube.com/watch?v=TkCSr30UojM) for a walkthrough).
> 4. Start PS and wait for the pop-up to appear.
> 5. Stop scanning in Wireshark and type "DNS" in the filter bar (demo of how to filter at 5:06 in the video linked above). Scroll to where you see packets that have adobe addresses on the right side (you can click the magnifying glass and find packets with "adobe.io" to make this easier).
> 6. Find a packet with an Info section that reads: "Standard query 0x13ef AAAA XXXXXXXXXX.adobe.io", where the Xs are a unique combination of letters and numbers.
> 7. Add your version of XXXXXXXXXX.adobe.io to the bottom of the hosts file, following the same format as the other entries, then save it.
> 8. Run this Terminal command to restart the mDNSResponder process (I saw it in another post, but not sure if it's actually necessary, so Windows users may be fine skipping this step):
>   1. `sudo killall -HUP mDNSResponder && sudo dscacheutil -flushcache`
> 9. Start PS and enjoy! Hope it works for you too.
>
> — [Adobe Photoshop (Genuine) and (Sorry App Is Not Available) Fix as of May 2023 : r/AdobeZii](https://www.reddit.com/r/AdobeZii/comments/13my2ij/comment/jlcok0s/)

### Offline packages

See first [Adobe Offline Package Generator v0.1.1 (macOS only)](https://gist.github.com/ayyybe/a5f01c6f40020f9a7bc4939beeb2df1d) (from [Download CC 2020 (+ old versions) directly from Adobe : AdobeZii](https://www.reddit.com/r/AdobeZii/comments/fmv3sm/download_cc_2020_old_versions_directly_from_adobe/))
Require Adobe Desktop Common (ADC) HDBox from Creative Cloud https://creativecloud.adobe.com/apps/all/desktop?action=install&source=apps&productId=creative-cloud

Get HDBox bins:

```
https://cdn-ffc.oobesaas.adobe.com/core/v1/applications?name=CreativeCloud&name=KCCC or https://cdn-ffc.oobesaas.adobe.com/core/v1/applications?name=CreativeCloud&name=KCCC&osVersion=10.12.4&platform=osx10
Find packageset "ADC", package "HDBox", and concat manifestUrl with https://ccmdls.adobe.com
curl -H 'x-api-key: CreativeCloud_v5_0' -H 'User-Agent: Creative Cloud' -H 'x-adobe-app-id: accc-hdcore-desktop' 'https://ccmdls.adobe.com/AdobeProducts/KCCC/1/osx10/packages/ACCC_5_1_0_HDBox_407/manifest.xml'
download the url manifest/asset_list/asset[0]/asset_path
read it as zip, insde /packages/HDBox/HDBox.pima, read it as zip, inside you find all tools
```

```sh
#!/bin/bash

# Based on https://gist.github.com/ayyybe/a5f01c6f40020f9a7bc4939beeb2df1d

#python3 -m pip install --target="$(pwd)" requests
#export PYTHONPATH=$PYTHONPATH:$(pwd)

#curl https://gist.githubusercontent.com/ayyybe/a5f01c6f40020f9a7bc4939beeb2df1d/raw/ccdl.py -o "ccdl.py"
#chmod +x "ccdl.py"

#Edit ccdl.py
#remove part with `if (not os.path.isfile('/Library/Application Support/Adobe/Adobe Desktop Common/HDBox/Setup')):`
#edit part with /Library/Application Support/Adobe/Adobe Desktop Common/HDBox

#python3 ccdl.py


PRODUCTS_DIR=Contents/Resources/products

# changes ? https://helpx.adobe.com/after-effects/kb/fixed-issues.html


#usage() {
#  if [ -n "$1" ]; then
#    echo -e "${RED}$1${CLEAR}\n";
#  fi
#
#  echo "Usage: $0 -b TFS_BRANCH -d TFS_DOMAIN -u TFS_USERNAME -p TFS_PASSWORD -v NPM_PACKAGE_VERSION -w TFS_WORKSPACE APPLICATION
#"
#  echo "  -b    TFS branch"
#  echo "  -d    TFS domain"
#  echo "  -u    TFS user"
#  echo "  -p    TFS password"
#  echo "  -v    NPM package version"
#  echo "  -w    TFS workspace name"
#  echo ""
#  echo "Example: $0 -d FNAC -u username -p password -v 0.0.0-develop -w my-workspace orderpipe"
#  exit 1
#}
#
#
#npm_install() {
#  local PACKAGE_NAME=$1
#  local PACKAGE_VERSION=$2
#
#  log "Running 'npm install'..."
#
#  npm install "$PACKAGE_NAME@$PACKAGE_VERSION" \
#    --save-exact \
#    --ignore-scripts \
#    --no-audit
#}
#
## Start parsing options
#while getopts "h?a:b:d:u:p:v:w:" opt; do
#  case "$opt" in
#    h|\?)   usage ;;
#    a)      ACTION=$OPTARG ;;
#    b)      TFS_BRANCH=$OPTARG ;;
#    d)      TFS_DOMAIN=$OPTARG ;;
#    u)      TFS_USERNAME=$OPTARG ;;
#    p)      TFS_PASSWORD=$OPTARG ;;
#    v)      NPM_PACKAGE_VERSION=$OPTARG ;;
#    w)      TFS_WORKSPACE=$OPTARG ;;
#  esac
#done



DST_DIR=
HDBOX_DIR=HDBox
HDBOX_TMP_DIR=hdbox-tmp

# Get HDBox:
#mkdir -p HDBox
# Get HDBox package infos of Creative cloud
# exact xpath: /applications/application[name="CreativeCloud" and plaform="osx10"]/packageSets/packageSet[name="ADC"]/packages/package[name="HDBox" and platform="osx10"]/manifestUrl
#https://stackoverflow.com/questions/15461737/how-to-execute-xpath-one-liners-from-shell
HDBOX_MANIFEST_PATH=$(curl -s "https://cdn-ffc.oobesaas.adobe.com/core/v1/applications?name=CreativeCloud&name=KCCC" | xmllint --xpath '//package[name="HDBox" and platform="osx10"]/manifestUrl[1]/text()' -)
# Get package asset location
# exact xpath: /manifest/asset_list/asset[0]/asset_path
HDBOX_PKG=$(curl -s -H 'x-api-key: CreativeCloud_v5_0' -H 'User-Agent: Creative Cloud' -H 'x-adobe-app-id: accc-hdcore-desktop' "https://ccmdls.adobe.com$HDBOX_MANIFEST_PATH" | xmllint --xpath '//asset_path[1]/text()' -)
# Extract package
mkdir -p "$HDBOX_TMP_DIR" "$HDBOX_DIR"
curl -s "$HDBOX_PKG" > "$HDBOX_TMP_DIR/hdbox.zip"
unzip -qqo "$HDBOX_TMP_DIR/hdbox.zip" "packages/HDBox/HDBox.pima" -d "$HDBOX_TMP_DIR"
unzip -qqo "$HDBOX_TMP_DIR/packages/HDBox/HDBox.pima" -d "$HDBOX_DIR"
rm -rf "$HDBOX_TMP_DIR"

# find the matching product (SAP_CODE, VERSION, NAME)

# get product dependencies (SAP_CODE, VERSION)

# loop dependencies (driver xml, curl config)
# https://stackoverflow.com/questions/34555278/bash-read-a-looping-on-null-delimited-string-variable/34557041#34557041
# https://stackoverflow.com/questions/8677546/reading-null-delimited-strings-through-a-bash-loop
# https://stackoverflow.com/questions/11426529/reading-output-of-a-command-into-an-array-in-bash/32931403#32931403

# download files from config file with curl https://curl.haxx.se/docs/manpage.html#-K


$NAME=product['displayName']
$SAP_CODE=prodInfo['sapCode'],
$VERSION=prodInfo['version'],
$LANGUAGE = installLanguag

read -r -d '' CURL_CONFIG << EOF
# Download core ${SAP_CODE} ${VERSION}
url = "example.com"
output = "file.ext"
user-agent = "superagent/1.0"
EOF

for ((i=0; i<$COUNT; i++))
do
	SAP_CODE=
	VERSION=
	read -r -d '' DEPENDENCIES_XML << EOF
${DEPENDENCIES_XML}
			<Dependency>
				<SAPCode>$SAP_CODE</SAPCode>
				<BaseVersion>$VERSION</BaseVersion>
				<EsdDirectory>./$SAP_CODE</EsdDirectory>
			</Dependency>
EOF
	read -r -d '' CURL_CONFIG << EOF
${CURL_CONFIG}
# Download dependency ${SAP_CODE} ${VERSION}
url = "example.com"
output = "file.ext"
user-agent = "superagent/1.0"
EOF
done

cat > $PRODUCTS_DIR/driver.xml << EOF
<DriverInfo>
	<ProductInfo>
		<Name>Adobe $NAME</Name>
		<SAPCode>$SAP_CODE</SAPCode>
		<CodexVersion>$VERSION</CodexVersion>
		<Platform>osx10-64</Platform>
		<EsdDirectory>./$SAP_CODE</EsdDirectory>
		<Dependencies>$DEPENDENCIES_XML
		</Dependencies>
	</ProductInfo>
	<RequestInfo>
		<InstallDir>/Applications</InstallDir>
		<InstallLanguage>$LANGUAGE</InstallLanguage>
	</RequestInfo>
</DriverInfo>
EOF


APP_BUNDLE_NAME="Install $NAME $VERSION.app"
APP_BUNDLE_DIR="$DST_DIR/$APP_BUNDLE_NAME"
cp "HDBox/Install.app/Contents/Resources/app.icns" "$APP_BUNDLE_DIR/Contents/Resources/applet.icns"

# after install and before apply patch
# see https://www.adobezii.com/adobezii-damaged/
sudo xattr -rd com.apple.quarantine /Applications/AppName.app
```

```js
// Open in a browser https://prod-rel-ffc-ccm.oobesaas.adobe.com/ then execute that script in Console
// SAP Code https://helpx.adobe.com/enterprise/package/help/apps-deployed-without-their-base-versions.html
/*
Camera Raw                  ACR
CCX Process                 CCXP
STI_ColorCommonSet_CMYK_HD  COCM
STI_Color_Photoshop_HD      COPS
STI_Color_HD                CORE
STI_ColorCommonSet_RGB_HD   CORG
Adobe Could Installer       KCCC https://cdn-ffc.oobesaas.adobe.com/core/v1/applications?name=CreativeCloud&name=KCCC https://ccmdls.adobe.com/*
After Effects               AEFT
Audition                    AUDT
InDesign                    IDSN
Illustrator                 ILST
Lightroom Classic           LTRM
Photoshop                   PHSP
Premier Pro                 PPRO
# Creative Cloud ADCS ?
# Photoshop PHXS ?
*/
async function search({sapCode, version, type = "Desktop", platformID}){
    //const base = new URL("https://cdn-ffc.oobesaas.adobe.com/");
    const base = new URL("https://prod-rel-ffc-ccm.oobesaas.adobe.com/");
    const productsURL = new URL("/adobe-ffc-external/core/v4/products/all?payload=true&_type=json", base);
    for(const [name, value] of [
        // API support multiple values as platform=win64&platform=win32 and platform=win64,win32
    ["channel", ["ccm", "sti", "ccp_hd_2", "services", "nocc", "mobileApps"]],// var a = Array.from({length: 26}, (_, i) => String.fromCharCode("a".charCodeAt(0) + i)); Array.from({length: 100000}, (_, i) => i.toString(26).replace(/*/, char => )).join(","); Array.from({length: 100000}, (_, i) => i.toString(10+26)).join(",")
        //["platform", ["win32", "win64", "osx10", "osx10-64"]],
        ["platform", platformID],
        ["productType", type],
    ]){
        productsURL.searchParams.append(name, value);
    }

    // curl -H 'User-Agent: Creative Cloud' -H 'x-adobe-app-id: AUSST_4_0' 'https://prod-rel-ffc-ccm.oobesaas.adobe.com/adobe-ffc-external/core/v4/products/all?channel=ccm&channel=sti&platform=osx10&platform=osx10-64&payload=true&productType=Desktop&_type=json'
    const channels = await (await fetch(productsURL, {
        headers: {
          "user-agent": "Creative Cloud",// optional
          "x-adobe-app-id": "AUSST_4_0",
        },
    })).json();

    let product = null;
    let platform = null;
    let application = null;
    const availableVersions = new Set();
    mainLoop: for(const {products} of channels.channel){
        for(const productEntry of products.product){
            // -> type === productEntry.type
            if(productEntry.id !== sapCode){
                continue;
            }

            for(const platformEntry of productEntry.platforms.platform){
                // -> platformEntry.id === platformID
                for(const applicationEntry of platformEntry.languageSet){
                    const {productVersion} = applicationEntry;
                    availableVersions.add(productVersion)
                    if(productVersion !== version){
                        continue;
                    }

                    product = productEntry;
                    platform = platformEntry;
                    application = applicationEntry;
                    break mainLoop;
                }
            }
        }
    }

    if(!application){
        throw new Error(
            availableVersions.size
            ? `Version ${version} not found. Versions found:${[...availableVersions].sort().reverse(). map(v => `\n- ${v}`)}}`
            : "No application match"
        );
    }

    // Not all params are required and could be ignored
    // curl -vs -H 'x-adobe-build-guid: 99170da3-16fc-423d-99c8-4dc267bd7d23' -H 'x-api-key: CreativeCloud_v5_0' -H 'x-adobe-app-id: accc-hdcore-desktop' 'https://prod-rel-ffc-ccm.oobesaas.adobe.com/core/v3/applications?name=ILST&version=24.0.3&platform=osx10-64&build=24.0.3.375'
    const applicationURL = new URL("/core/v3/applications", base);
    for(const [name, value] of [
        ["name", product.id],
        // ["version", application.baseVersion],
        ["platform", platform.id],
        ["build", application.productVersion],
    ]){
        applicationURL.searchParams.append(name, value);
    }

    const headers = {
        "x-adobe-build-guid": application.buildGuid,// required
        "x-api-key": "CreativeCloud_v5_0",
        "User-Agent": "CreativeCloud/5.0.0.354/Mac-10.14",// optional
        "x-adobe-app-id": "accc-hdcore-desktop",
    };
    const applicationDetails = await (await fetch(applicationURL, {headers})).json();

    let scriptSrc = `#!/bin/sh`;

    scriptSrc += `
# ${product.displayName} (${product.id}) ${application.productVersion} (${application.baseVersion}) ${platform.id}
mkdir -p "${product.id}"
curl${Object.entries(headers).map(([name, value]) => ` -H '${name}: ${value}'`).join("")} '${applicationURL}' -o "${product.id}/Application.json"
${applicationDetails.Packages.Package.map(package => {
    const filename = package.Path.split("/").slice(-1);
    const url = new URL(package.Path, "https://ccmdls.adobe.com/");
    return `curl -H 'x-api-key: CreativeCloud_v5_0' -H 'User-Agent: Creative Cloud' -H 'x-adobe-app-id: accc-hdcore-desktop' '${url}' -o "${product.id}/${filename}"`;
}).join("\n")}`;

    console.log(scriptSrc);

    for(const {sapCode, baseVersion} of application.dependencies.dependency){
        console.warn(`Require ${sapCode} ${baseVersion}`);
    }

    // TODO generate within an com.adobe.acc.installer.v2
    // PPRO_14.0.1.71/1/support/common/AMT/application.xml -> /Library/Application Support/Adobe/Premiere Pro/14.0/AMT/application.xml
}

await search({
    sapCode: "PPSH",
    version: "21.0.3.91",
    platformID: "osx10-64",
});
```

- [Drovosek01/adobe-packager: Script that allows to download portable installers of different versions Adobe software for macOS](https://github.com/Drovosek01/adobe-packager)
- [autopkg/adobe-ccp-recipes: Autopkg recipes for Creative Cloud Packager workflows](https://github.com/autopkg/adobe-ccp-recipes/blob/master/Adobe/CreativeCloudFeed.py) - See also [mosen/ccp-recipes](https://github.com/mosen/ccp-recipes)
- [timsutton/adobe-ccp-automation: Experimenting with automating CCP](https://github.com/timsutton/adobe-ccp-automation)
- https://github.com/Homebrew/homebrew-cask/blob/master/Casks/adobe-creative-cloud.rb
- https://github.com/PayalAwasthi/PythonApplication7/blob/master/config.py

- [How to download the Creative Cloud desktop app](https://helpx.adobe.com/download-install/kb/creative-cloud-desktop-app-download.html?red=a#ProblemsinstallingTryalternativedownloadlinks) + install apps trial version (but don't need to start evaluation)
- `sudo find /private/tmp/ \( -iname "*.dmg" -or -iname "*.pkg" \)` - Temp dir used by Creative Cloud app before install it
- `~/Library/Logs/CreativeCloud/ACC/AdobeDownload/HDInstaller.log`
- [Adobe Software Full Version Archives » Adobe Download](https://adobedownload.org/adobe-series/)
- [All the New Adobe CC 2019 Direct Download Links, Now Available! | ProDesignTools](https://prodesigntools.com/adobe-cc-2019-direct-download-links.html)
- [corbindavenport/creative-cloud-linux: PlayOnLinux install script for Adobe Creative Cloud](https://github.com/corbindavenport/creative-cloud-linux)

```sh
sudo killall ACCFinderSync "Core Sync" AdobeCRDaemon "Adobe Creative" AdobeIPCBroker node "Adobe Desktop Service" "Adobe Crash Reporter"
# Clear preferences: Shft + Alt + Cmd the exec the Adobe app
sudo rm -rf "/Library/Application Support/Adobe/SLCache/" "/Library/Application Support/Adobe/SLStore/" "/Library/Caches/."* "/private/tmp/zx"* "~/Library/Preferences/Adobe/."*
```

See also [How do I stop the Adobe Creative Cloud app from auto-launching on login? - Ask Different](https://apple.stackexchange.com/questions/138941/how-do-i-stop-the-adobe-creative-cloud-app-from-auto-launching-on-login/356217#356217)

- [AMTEmu Download | Adobe Universal Patcher](https://official-amtemu.com/)

```
# https://adobehostpatch.blogspot.com/
# https://superuser.com/a/1345088
0.0.0.0 activate.adobe.com
0.0.0.0 practivate.adobe.com
0.0.0.0 ereg.adobe.com
0.0.0.0 wip3.adobe.com
0.0.0.0 activate.wip3.adobe.com
0.0.0.0 3dns-3.adobe.com
0.0.0.0 3dns-2.adobe.com
0.0.0.0 adobe-dns.adobe.com
0.0.0.0 adobe-dns-2.adobe.com
0.0.0.0 adobe-dns-3.adobe.com
0.0.0.0 ereg.wip3.adobe.com
0.0.0.0 activate-sea.adobe.com
0.0.0.0 wwis-dubc1-vip60.adobe.com
0.0.0.0 activate-sjc0.adobe.com
0.0.0.0 hl2rcv.adobe.com
0.0.0.0 lm.licenses.adobe.com
0.0.0.0 na2m-pr.licenses.adobe.com
0.0.0.0 lmlicenses.wip4.adobe.com
0.0.0.0 lm.licenses.adobe.com
0.0.0.0 na1r.services.adobe.com
0.0.0.0 hlrcv.stage.adobe.com
```

### Uninstall Adobe

```
~/Library/Application Support/Adobe/*
~/Library/Preferences/Adobe/*
~/Documents/Adobe/*
/Library/Application Support/Adobe/*
```

```
/Applications/Utilities/Adobe Application Manager
/Applications/Utilities/Adobe Installers
```

See if hosts files doesn't contains blocked domains

- [Use the Creative Cloud Cleaner Tool to solve installation problems](https://helpx.adobe.com/creative-cloud/kb/cc-cleaner-tool-installation-problems.html)

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

- [Jeffrey Friedl's Blog » Accessing Lightroom’s SQLite DB Directly](https://web.archive.org/web/20230328220741/http://regex.info/blog/2006-07-29/221)

```
~/Pictures/Lightroom 5 Catalog.lrcat
```

To update, download Adobe DNG Converter (for [macOS](http://www.adobe.com/go/dng_converter_mac/) or [Windows](http://www.adobe.com/go/dng_converter_win/)) the open the install package (ex: with Suspicious Package)

And copy cameras profiles (`CameraProfiles`) and lenses profiles (`LensProfiles`) from `/Library/Application Support/Adobe/CameraRaw` in:

```
/Applications/Adobe Photoshop Lightroom 5.app/Contents/Resources/*
~/Library/Application Support/Adobe/CameraRaw/*
```

Then copy `/Library/Application Support/Adobe/CameraRaw/Settings` in `~/Library/Application Support/Adobe/CameraRaw/`

For Windows: `%USER_APPDATA%\Roaming\Adobe\CameraRaw\LensProfiles\1.0\Downloaded` and `C:\ProgramData\Adobe\CameraRaw\LensProfiles\1.0\`

- [Script to extract previews of lost or deleted photos](https://helpx.adobe.com/lightroom-classic/kb/extract-previews-for-lost-images-lightroom.html)

## FFMpeg

If ffmpeg is used in a loop, you could need to use `< /dev/null`:

- [Strange errors when using ffmpeg in a loop - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/36310/strange-errors-when-using-ffmpeg-in-a-loop/36411#36411)
- [BashFAQ/089 - Greg's Wiki](http://mywiki.wooledge.org/BashFAQ/089)

- [bash - How to exit from find -exec if it fails on one of the files - Stack Overflow](https://stackoverflow.com/questions/14871147/how-to-exit-from-find-exec-if-it-fails-on-one-of-the-files)

Make a video from image slideshow:

```sh
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
```

Include subtitles in a video:

```sh
ffmpeg -i movie.mp4 -i subtitles.srt -map 0 -map 1 -c copy -c:v libx264 -crf 23 -preset veryfast output.mkv
```

Offset (soft) subtitle track embeded in a video container

```sh
ffmpeg -i input.mp4 -itsoffset -0.7 -i input.mp4 -map 0:v -map 0:a -map 1:s -c copy output.mp4
```

- [How can I fix delayed subtitles in videos? - Super User](https://superuser.com/questions/494841/how-can-i-fix-delayed-subtitles-in-videos/1242613#1242613)

Offset subtitle track file (in seconds):

```sh
ffmpeg -itsoffset -0.7 -i input.srt -c copy output.srt
```

Extract audio from video:

```sh
# To 256kbps MP3
ffmpeg -i video.mp4 -vn -ab 256 audio.mp3
```

Mute video:

```sh
ffmpeg -i video.mp4 -an muted-video.mp4
```

Merge files (works on `*.srt` too) with identical codecs.

**Be careful sometimes this not work propelly**

```sh
ffmpeg -i "concat:file1.avi|file2.avi" -c copy "file.avi"
```

Remove an audio track:

```sh
ffmpeg -i file.mp4
#Stream #0.0: Video: [truncated]
#Stream #0.1: Audio: [truncated]
#Stream #0.2: Audio: [truncated]

ffmpeg -i file.mp4 -map 0:0 -map 0:2 -acodec copy -vcodec copy new_file.mp4
```

Will copy the video and the second audio track

To remove all audio tracks use `-an` or `-vn` to remove video tracks:

```sh
ffmpeg -i input_file.mp4 -vcodec copy -an output_file.mp4
```

- [How to merge audio and video file in ffmpeg - Super User](http://superuser.com/questions/277642/how-to-merge-audio-and-video-file-in-ffmpeg/277667#277667)

Convert to Apple ringstone (only the first 30 seconds will be played):

```sh
# if already AAC
ffmpeg -i Nuance.aac -f mp4 -c copy Nuance.m4r
# else
ffmpeg -i ringtone.mp3 -ac 1 -ab 128000 -f mp4 -acodec libvo_aacenc -y ringtone.m4r
```

Convert all WMA to MP3 (and remove it):

```sh
find . -type f -iname "*.wma" | while read file; do < /dev/null ffmpeg -i "${file}" -acodec libmp3lame -ab 192k "${file/.wma/.mp3}" && rm "${file}"; done
find . -type f -iname "*.wma" -exec bash -c 'ffmpeg -i "$1" -acodec libmp3lame -ab 192k "${1/.wma/.mp3}" && rm "$1"' - {} \;
```

Find invalid media files:

```sh
find . -type f \( -iname "*.wma" -or -iname "*.mp3" -or -iname "*.m4a" -or -iname "*.mp4" -or -iname ".wav" -or -iname "*.ogg" \) \( -exec ffmpeg -v error -xerror -i "{}" -f null - 2>/dev/null \; -or -exec echo "{}" \; \)
# To get the details into log file
find . -type f \( -iname "*.wma" -or -iname "*.mp3" -or -iname "*.m4a" -or -iname "*.mp4" -or -iname ".wav" -or -iname "*.ogg" \) -exec bash -c 'echo "$1:" >> error.log; ffmpeg -v error -xerror -i "$1" -f null - 2>>error.log && echo "OK" >> error.log; exit $?' - {} \;
```

You can also detect black frame and/or slicence with [`blackdetect`](http://www.ffmpeg.org/ffmpeg-filters.html#blackdetect) and [`slicendetect`](https://ffmpeg.org/ffmpeg-filters.html#silencedetect): `-af silencedetect=d=3:n=0.0001` (you need to remove/update `-v error`, see also `-loglevel info`)

- [How can I check the integrity of a video file (avi, mpeg, mp4...)? - Super User](https://superuser.com/questions/100288/how-can-i-check-the-integrity-of-a-video-file-avi-mpeg-mp4)

Download RTMP stream:

```sh
ffmpeg -i "rtmp://cp262207.edgefcs.net:80/ondemand/techchannel/10821/videos/10821_AA11149_Pair_Paradox_FL8_412x310_700K" -c copy "A Pair of Paradoxes.flv"
```

Get media metadata:

```sh
ffmpeg -i file.avi -f ffmetadata pipe:1
#or
ffmpeg -i file.avi
```

Concat files:

```sh
ffmpeg -f concat -safe 0 -i <(find $PWD -type f -iname *.mp4 -printf "file '%h/%f'\n") -c copy output.mp4
```

- [Concatenate – FFmpeg](https://trac.ffmpeg.org/wiki/Concatenate)

## Imagemagick

Pixel shader for channels [`fx`](http://www.imagemagick.org/script/fx.php), column (`i`) and row (`j`) are zero based.

Multiple files:

Use `mogrify` or `find ./ -iname "tile_*.png" -exec bash -c 'filename="$1";echo "${filename%.*}"' _ {} \;`

Get trim area:

```sh
# `-quiet` remove warnings
convert test.png -trim -format "%G%O\n" -quiet info:
convert test.png -format "%@" -quiet info:
# You can save result and log info
convert test.png -trim -format "%O\n" -quiet -write info: test_trim.png >> output.log
```

Get hash of image (only pixels, not metadata):

```sh
identify -format "%#\n" image.png
```

Create a TIFF (support layers) with PNGs (from export of all layers in PS) due to strange PSD handling of ImageMagick (layers+1, cropped layers):

```sh
# (First is in foreground, last in background)
# convert app-decorations_0000_main.png app-decorations_0001_shadow1.png app-decorations_0002_shadow2.png app-decorations.tif
```

Crop and get final filenames without creating it

```sh
# For the followin command:
#convert largeimage.png -crop 2048x2048 -set filename:tile "%[fx:page.x/2048+1]_%[fx:page.y/2048+1]" +repage +adjoin "tile_%[filename:tile].png"
convert largeimage.png -crop 2048x2048 -format "tile_%[fx:page.x/2048+1]_%[fx:page.y/2048+1].png\n" info:
# To get the number of file will be created, append `| wc -l`
```

- [Fred's ImageMagick Scripts](http://www.fmwconcepts.com/imagemagick/)

Extend document size

```sh
# mogrify/convert promote automatically 16 bits per channels if any pixels are modified. Need `-depth 8` to keep bit_depth=8 for PNGs
mogrify -background none -extent 2048x2048 -depth 8 tile_*.png
```

Compose alpha:

```sh
convert RGB.png Alpha.png -compose Copy_Opacity -composite RGBA.png
convert RGBA.png -alpha off RGB.png
# convert RGBA.png -channel a -fx "1" RGB.png
```

Pre-multiply alpha (aka premultiped alpha)

```sh
convert in.png \( +clone -alpha Extract \) -channel RGB -compose Multiply -composite out.png
```

- [\[SOLVED\] Multiplying color by alpha - ImageMagick](http://www.imagemagick.org/discourse-server/viewtopic.php?t=23463)

Set color to transparent pixels

```sh
convert in.png -channel rgb -fx 'a==0?1:s' out.png
```

Bleed outside:

```sh
# Source image 32x32 -> 70x70
convert tree.gif  -set option:distort:viewport 70x70-19-19 -virtual-pixel Edge -filter point -distort SRT 0 +repage virtual_edge.gif
```

Get average color of an image

```sh
convert cat.png -resize 1x1 txt:- | awk 'NR==2{print $3}'
# Or
convert cat.png -scale 1x1\! -format '%[fx:int(255*r+.5)],%[fx:int(255*g+.5)],%[fx:int(255*b+.5)]‌​' info:- | sed 's/,/\n/g' | xargs -L 1 printf "%x"
```

Convert raw data to image

```sh
# 2 RGB pixels: 2x1
printf '\x00\xFF\x88\xFF\x00\xFF' | convert -depth 8 -size 2x1+0 rgb:- data.png
# Create Nx4 bytes to generate Nx1 RGBA PNG
printf '\x00\xFF\x88\xFF\xFF\x00\xFF\xFF' > data.bin; convert -depth 8 -size $(($(wc -c < data.bin)/4))x1+0 rgba:data.bin data.png
```

Create image (from nothing). `xc` "X Constant Image" / Canvas: [Canvas Creation -- IM v6 Examples](http://www.imagemagick.org/Usage/canvas/)

```sh
convert -size 100x100 xc:white canvas.jpg
```

Remove metadata (see also `-define` and[PNG Metadata](PNG#metadata))

```sh
convert -strip image.jpg image_slim.jpg
```

Force PNG to be 32 bits:

```sh
mogrify -background none -define png:color-type=6 image.png
```

Swap / invert / intervert channels

```sh
# Invert R with B (r=0, g=1, b=2 and a=3) and keep alpha + output always as PNG 32bit
convert in.png -channel rgba -alpha on -set colorspace RGB -separate -swap 0,2 -combine -define png:color-type=6 out.png
```

- [swap colors/channels - ImageMagick](http://www.imagemagick.org/discourse-server/viewtopic.php?t=21846)

Get metadatas:

```sh
convert image.jpg -moments infos.json
convert -moments - json: < image.jpg > infos.json
```

- [Formats @ ImageMagick](https://www.imagemagick.org/script/formats.php) - ImageMagick can write JSON format
- [Command-line Tools: Identify @ ImageMagick](https://www.imagemagick.org/script/identify.php) - Supported options

Outline

- [Outline image on transparent background - ImageMagick](https://www.imagemagick.org/discourse-server/viewtopic.php?t=16399)

Generate blank image

```sh
convert -size 100x100 xc:white canvas.jpg
```

### Convert SVG

[Drawing -- IM v6 Examples](http://www.imagemagick.org/Usage/draw/#svg)

```sh
convert -background none a.svg b.png
convert -density 150 -background none a.svg b.png
```

Try MSVG imagemagick's own SVG renderer

```sh
convert -background none msvg:a.svg b.png
```

By default it delegate to `rsvg-convert` (`convert -list delegate | grep 'svg ='`), but could be not installed (`brew install imagemagick --use-rsvg` or `sudo port install ImageMagick +rsvg`)

- [ImageMagick convert SVG to PNG not working with RSVG enabled - Stack Overflow](https://stackoverflow.com/questions/11592085/imagemagick-convert-svg-to-png-not-working-with-rsvg-enabled)
- [osx - Use librsvg / rsvg to convert SVG images with ImageMagick - Stack Overflow](https://stackoverflow.com/questions/24513244/use-librsvg-rsvg-to-convert-svg-images-with-imagemagick)

## X11

Aka XQuartz, Xorg

Install with [MacPorts](https://www.xquartz.org/releases/#macports):

```sh
sudo port -v install xorg-server +universal
# Some libs don't use the right path:
sudo ln -s /opt/local /usr/X11
# see also /usr/X11R6
```

Uninstall XQuartz

```sh
launchctl unload /Library/LaunchAgents/org.macosforge.xquartz.startx.plist && \
sudo launchctl unload /Library/LaunchDaemons/org.macosforge.xquartz.privileged_startx.plist && \
sudo rm -rf /opt/X11* /usr/X11* /Library/Launch*/org.macosforge.xquartz.* /Applications/Utilities/XQuartz.app /etc/*paths.d/*XQuartz && \
sudo pkgutil --forget org.macosforge.xquartz.pkg  && \
rm -rf ~/.serverauth* && rm -rf ~/.Xauthorit* && rm -rf ~/.cache && rm -rf ~/.rnd && \
rm -rf ~/Library/Caches/org.macosforge.xquartz.X11 && rm -rf ~/Library/Logs/X11
```

- [Uninstall XQuartz.app from OSX Yosemite/El Capitan/Sierra](https://gist.github.com/pwnsdx/d127873e24cef159d4d603accaf37ee4)

Some times, after wakeup or deconnected from an external screen (clampshield), xorg don't work:

```sh
xorg
#...
#Fatal server error:
#(EE) no screens found(EE)
#...
```

Then restart.

## Wine

See also Wineskin

macOS Wine: `Wine.app` and [WineBottler](https://winebottler.kronenberg.org/) (see [winebottler sources on Bitbucket](https://bitbucket.org/winebottler/winebottler/src/master/))

Install winetrick in current prefix: Wine menu > Wintricks

```sh
/Applications/Wine.app/Contents/Resources/bin/wine app.exe
WINEPREFIX=~/.wine /Applications/Wine.app/Contents/Resources/bin/wine app.exe
```

```sh
exec wine "~/.wine/drive_c/My/program.exe" "-my" "-arguments"
# The exec commands tell bash to morph into wine with the following arguments, so this is no longer bash running wine, but bash process becoming wine.
# The PID remains. You don't have two processes running.
```

If error like `err:module:import_dll Library MSVCP140.dll` check if a winetrick is not required like `vcrun2015`

Some interesting files:

```
~/Library/Application Support/Wine/winetricks
~/Library/Application Support/Wine/winetricks.plist
/Applications/Wine.app/Contents/Frameworks/WBottler.framework/Versions/A/Resources/applywinetricks.sh
/Applications/Wine.app/Contents/Frameworks/WBottler.framework/Versions/A/Resources/winetricksextract.sh
```

- [command line - Transparently run wine programs - Unix & Linux Stack Exchange](http://unix.stackexchange.com/questions/70681/transparently-run-wine-programs)

If winetrick don't install (error log contains `pathchk: illegal option -- P`) get `https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks` and replace content of `~/Library/Application Support/Wine/winetricks`

`Wine.app` start `winetrick` with a `$PATH` as it's original value (for any spawned process), it's why you need when debug a wine app on macOS, always start with **absolute path** in Terminal: `/Applications/MyApp.app/Contents/MacOS/startwine.sh`. See [Define PATH globaly](macOS#define-path-globaly)

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
Or edit `*.app/Contents/Resources/wineprefix/user.reg` and remove lines `"mscoree"=""` and `"mshtml"=""` and maybe `"*mscoree"="native"` (or set value as `n,b`) in section `[Software\\Wine\\DllOverrides]`.
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

```sh
port provides <filename>
#see also port contents "*"
```

See dependents and dependencies:

```sh
port dependents <portname>
# or port echo dependentof:<portname>
```

```sh
# See https://trac.macports.org/wiki/FAQ#alldependencies
port rdeps <portname>
```

```sh
sudo port clean --all --archive <portname>
sudo port -n upgrade --force <portname> +universal
```

Find lib locations:

```sh
find / \( -name "<filename>" -o -name "<filename_symlink>" \) 2>/dev/null
```

Check if the lib is i386 compatible `Mach-O dynamically linked shared library i386`:

```sh
file <filename>
```

See libs dependencies:

```sh
otool -L <filename>
```

It's could needed to change the lib lookup location:

```sh
install_name_tool -change /Users/mike/Documents/wine2/usr/lib/libfreetype.6.dylib /usr/lib/libfreetype.6.dylib /Applications/Wine.app/Contents/Resources/lib/libfreetype.6.dylib
```

- [Fun with rpath, otool, and install_name_tool – Chris Hamons – Medium](https://medium.com/@donblas/fun-with-rpath-otool-and-install-name-tool-e3e41ae86172)
- [WINE for Darwin and Mac OS X / Re: \[Darwine\] Problem with Darwine 0.9.3DP on OSX86 10.4.1](https://sourceforge.net/p/darwine/mailman/message/6359349/)
- [Linking an OSX external bundle with a .dylib library | How To - Step-By-Step Guides To Tasks In LiveCode | LiveCode Lessons](http://lessons.livecode.com/m/4071/l/15029-linking-an-osx-external-bundle-with-a-dylib-library)

To debug dylib loaded, edit bash script `MyWineApp.app/Contents/MacOS/startwine` of the bottled Wine app, prefix `"$WINEUSRPATH/bin/wine"....` with `DYLD_PRINT_LIBRARIES=1 `: `DYLD_PRINT_LIBRARIES=1 "$WINEUSRPATH/bin/wine...`

```sh
otool -L /Applications/Wine.app/Contents/Resources/lib/libfreetype.6.dylib
```

### Wine 64bit

Fix WineBottle 4.0.1.1 to support macOS Catalina (10.15) 64 bit only:

- in `WineBottler.app/Contents/Frameworks/WBottler.framework/Resources/bottler.sh` and `Wine.app/Contents/Frameworks/WBottler.framework/Resources/bottler.sh`:
    - replace `export WINE="$WINEPATH/wine"` with `export WINE="$WINEPATH/wine64"`
    - replace `WINE_VERSION=$("$WINEPATH/wine" --version |sed 's/wine-//')` with `WINE_VERSION=$("$WINEPATH/wine64" --version |sed 's/wine-//')`
- in `WineBottler.app/Contents/Frameworks/WBottler.framework/Resources/startwine.sh` and `Wine.app/Contents/Frameworks/WBottler.framework/Resources/startwine.sh`:
    - replace `export WINEARCH=win32` with `export WINEARCH=win64`
    - replace all `/bin/wine` with `/bin/wine64`

## TexturePacker

http://texturepacker.software.informer.com/download/

```sh
TexturePacker --install-license <name_of_the_license_file>
```

`~/.config/code-and-web/TexturePacker.conf`

`~/Library/Preferences/de.code-and-web.TexturePacker.plist` cloned self in `licensing.data.rawdata` (clone with `Signature` -  rawdata sha256 Encryption check)

After the canonical 7 days of time trial, you will have extended time trial until the date you wrote

```
firstStart = false;
licensing.data.expiryDate = "2016-10-17";
licensing.data.freeUpdatesUntil = "2999-01-01";
licensing.data.licenseType = "trial";
licensing.data.licensee = "trial user";//"essential"
licensing.trialExpired = false;
```

If not match signature, Sprites replace with red message can appears (watermarks)

Windows: `HKEY_CURRENT_USER\Software\code-and-web.de\TexturePacker\licensing\data` set to `expiryDate=2999-01-01` and in `rawdata` and `trialExpired` in `HKEY_CURRENT_USER\Software\code-and-web.de\TexturePacker\licensing`

Uninstall the application from your computer (using Appzapper, AppCleaner, etc. delete everything related to that App like `de.code-and-web.TexturePacker.plist`). Install TexturePacker again and try to bypass license expiration.

```sh
sudo chmod 444 /Users/youruser/Library/Preferences/de.code-and-web.TexturePacker.plist
```

In hosts (not required):

```
127.0.0.1	secure.codeandweb.com
```

```
%licensing.data.computerId%
%autoUpdateCheck%
%date% = current timestamp in ms
https://www.codeandweb.com/releases/texturepacker/updatecheck.php?ex=pixijs&o=mac&ov=10.12&b=no&l=&c=%licensing.data.computerId%&v=4.2.3&lt=trial&m=%autoUpdateCheck%&bit=64&s=%date%
```

```http
POST https://secure.codeandweb.com/rpc/RPC.php
call=getTrialLicense&computerId=%licensing.data.computerId%&osName=MacOS&osVersion=10.12&product=TexturePacker&version=4.2.3&security_request_hash=f078701acfa82bbaad363e02d93e84dd
```

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

1. open the bundle editor `⌃⌥⌘B` (Bundles → Bundle Editor → Show Bundle Editor…)
2. create a personal bundle `⌘N`
3. create a new command `⌘N`
4. set "Name" to "Copy Path to Current Document"
5. set "Input" to "Nothing"
6. set "Output" to "Show in Tool Tip"
7. write in editor area:
    ```sh
    #!/bin/bash
    echo -n "$TM_FILEPATH" | pbcopy
    ```
8. save `⌘S`

- [Ciarán Walsh’s Blog » TextMate Tip – Where Am I?](https://web.archive.org/web/20210216113314/http://ciaranwal.sh/2007/11/27/textmate-tip-where-am-i)
- [Bundles — TextMate Manual](https://macromates.com/textmate/manual/bundles#bundle-editor)

Unsaved files: `~/Library/Application Support/TextMate/Session`

Rename untitled tab/file: in `~/Library/Application Support/TextMate/Session/` add xattr attribute `com.macromates.backup.custom-name` (plain text) with the custom name

See https://github.com/textmate/textmate/blob/346b52b108b387462d4b3def481fb74983ae89f3/Frameworks/document/src/OakDocument.mm#L355

See also:

- [TextMate Basics Tutorial](https://web.archive.org/web/20220924171805/http://projects.serenity.de/textmate/tutorials/basics/)
- [TextMate Manual](https://macromates.com/textmate/manual/)
- [TextMate 2 .tm_properties](https://gist.github.com/sipp11/3382426)

## Google AppEngine

https://cloud.google.com/appengine/docs/php/download

Installed files:

```
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
```

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

A file manager is included (to copy/past/rename/etc. files): System > File manager. It's the only way to access to Kodi files

- [Userdata - Official Kodi Wiki](https://kodi.wiki/view/Userdata)
- [Kodi data folder - Official Kodi Wiki](https://kodi.wiki/view/Kodi_data_folder)

See also `sources.xml`. See also [Store passwords](#store-passwords)

```xml
<!-- No complete -->
<source>
	<name>Movies</name>
	<path pathversion="1">smb://user:password@192.168.3.4/Medias/Movies/</path>
	<allowsharing>true</allowsharing>
</source>
```

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

Remote control with [Web interface](https://kodi.wiki/view/Web_interface): use a port like 9080 (default could be already used or blocked)

### Set up centralized database in Kodi

Require an external access to MySQL/MariaDB server with full rights (create and drop tables)

Here prefixes `kodi_video` and `kodi_music` are defined (Ex. Kodi will create `kodi_videoXX` database, where `XX` is the [database version](http://kodi.wiki/view/Database_version))

Initial configuration (to creating the database, can be disabled later), require all granted privileges on target database

```sql
GRANT ALL ON *.* TO 'kodi';
```

After install or upgrade use:

```sql
GRANT ALL ON `MyMusic%`.* TO 'kodi';
GRANT ALL ON `MyVideos%`.* TO 'kodi';
```

`$USERDATA/advancedsettings.xml`:

```xml
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
```

- [MySQL/Setting up MySQL - Official Kodi Wiki](http://kodi.wiki/view/MySQL/Setting_up_MySQL)
- [MySQL/Upgrading - Official Kodi Wiki](http://kodi.wiki/view/MySQL/Upgrading#Making_sure_Kodi_can_update_the_library)
- [MySQL - MrMC Wiki](http://wiki.mrmc.tv/index.php/MySQL#Restricting_MySQL_access_rights)

### Store passwords in Kodi

SMB error message `operation not permitted`

`$USERDATA/passwords.xml`:

```xml
<passwords>
	<path>
		<from pathversion="1">smb://computername_or_ipaddress/</from>
		<to pathversion="1">smb://username:password@computername_or_ipaddress/</to>
	</path>
</passwords>
```

Or in `$USERDATA/sources.xml`:

```xml
<path>smb://domain;username:password@computername_or_ipaddress/sharename/path</path>
```

- [Log file/Advanced - Official Kodi Wiki](http://kodi.wiki/view/Log_file/Advanced#Password_warning)
- [MySQL/Setting up Kodi - Official Kodi Wiki](http://kodi.wiki/view/MySQL/Setting_up_Kodi#Make_files_accessible_over_the_network)
- [MySQL/Sync other parts of Kodi - Official Kodi Wiki](http://kodi.wiki/view/MySQL/Sync_other_parts_of_Kodi#Network_share_passwords)

### Addons

Indigo

1. Enable unknown sources: From home screen > Add-Ons > Settings > Enable Unknown Sources
2. Add Fusion repository: From home screen > File Manager > Add Source > Enter `https://fusion.tvaddons.co` and name it "Fusion" > OK
3. Install add-on: From home screen > Add-Ons > Install from zip file > select "Fusion" > select `begin-here`

- [Category:Add-on development - Official Kodi Wiki](https://kodi.wiki/view/Category:Add-on_development)

### Issues

Cleanup thumbnails:

- /sdcard/Android/data/org.xbmc.kodi/files/.kodi/userdata/Database/Textures*.db
- /sdcard/Android/data/org.xbmc.kodi/files/.kodi/userdata/Thumbnails

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

```js
let files = Array.from(document.documentElement.querySelectorAll("plist > dict:nth-of-type(1) > dict:nth-of-type(1) > dict")).reduce((list, track) => (list[track.querySelector(":scope > integer:nth-of-type(1)").textContent] = decodeURIComponent(track.querySelector(":scope > string:nth-last-of-type(1)").textContent.substr(7)), list), {});
copy(Array.from(document.documentElement.querySelectorAll("plist > dict:nth-of-type(1) > array:nth-of-type(1) > dict:nth-of-type(1) > array:nth-of-type(1) > dict")).map(entry => files[entry.querySelector(":scope > integer:nth-of-type(1)").textContent]).join("\n"));
```

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

(re)create a self contained macOS application (that no more the case since ???):

1. install JDownloader 2
2. copy `/Applications/JDownloader 2/JDownloader2.app` to `/Applications/JDownloader.app`
3. in `/Applications/JDownloader 2/JDownloader2.app/Contents/Info.plist` replace `$APP_PACKAGE/..` by `$APP_PACKAGE/Contents/Resources/java`
4. create a directory in `/Applications/JDownloader.app/Contents/Resources/java`
5. copy the content of `/Applications/JDownloader 2` into `/Applications/JDownloader.app/Contents/Resources/java` (you can omit the files `JDownloader2.app` and `Uninstall JDownloader.app`)

Only the content of `/Applications/JDownloader.app/Contents/Resources/java` will be updated

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

```sh
sudo kextcache -i /
```

If the device is not detected, may it's because it's pluged to a USB hub. Try to disconnect and connect again, or try to connect directly (without hub) first, the device should be reconnized by USB Overdrive (see Status tab), then you can connect to the hub

- [©1999-2017 Alessandro Levi Montalcini](http://www.usboverdrive.com/USBOverdrive/Support.html)

## Wireshark

- [srozzo/wireshark-uninstall-osx: Wireshark uninstall script for OS X](https://github.com/srozzo/wireshark-uninstall-osx)

## Cisco AnyConnect

Replace Cisco VPN

About OpenConnect:

- [OpenConnect VPN client.](https://www.infradead.org/openconnect/)
- [Split Tunneling tutorial - with openconnect (tested, works with Cisco AnyConnect VPN) Source: http://lists.unix-ag.uni-kl.de/pipermail/vpnc-devel/2009-February/002990.html](https://gist.github.com/jagtesh/5531300)
- [Split tunneling with openconnect - A guide on how to use openconnect to establish a vpn connection to an enterprise cisco anyconnect vpn endpoint with client side routing.](https://gist.github.com/stefancocora/686bbce938f27ef72649a181e7bd0158)
- [Win10 split tunnelling (#281) · Issues · OpenConnect VPN projects / OpenConnect GUI · GitLab](https://gitlab.com/openconnect/openconnect-gui/-/issues/281)
- [\[Win\] vpnc-script.js vs. vpnc-script-win.js (#279) · Issues · OpenConnect VPN projects / OpenConnect GUI · GitLab](https://gitlab.com/openconnect/openconnect-gui/-/issues/279)
- [Allow specifying custom routes (#32) · Issues · OpenConnect VPN projects / OpenConnect GUI · GitLab](https://gitlab.com/openconnect/openconnect-gui/-/issues/32)

About offical client:

```sh
shasum -a 512 /path/to/file.pkg
```

Split tunnel is configurable only by the VPN admin, not by the client only.

- [Software Download - Cisco Systems](https://software.cisco.com/download/home/283000185) - AnyConnect Secure Mobility Client

- [Installez le Client à mobilité sécurisé Cisco AnyConnect sur un ordinateur de MAC - Cisco](https://www.cisco.com/c/fr_ca/support/docs/smb/routers/cisco-rv-series-small-business-routers/smb5642-install-cisco-anyconnect-secure-mobility-client-on-a-mac-com.html)
- `anyconnect-macos-Y.X.ZZZZZ-predeploy-k9.dmg` > open `AnyConnect.pkg` to install both VPN only (which are AnyConnect Secure Mobility Client and AnyConnect Secure DART, other packages aren't needed)
- `anyconnect-macos-Y.X.ZZZZZ-webdeploy-k9.pkg` > open as zip > mount `(zip root)/binaries/anyconnect-macos-Y.X.ZZZZZ-core-vpn-webdeploy-k9.dmg` > open `anyconnect-macos-X.Y.ZZZZZ-core-vpn-webdeploy-k9.pkg`
- [Split tunneling in Cisco VPN and AnyConnect Client – karneliuk.com](https://karneliuk.com/2016/02/split-tunneling-in-cisco-vpn-client-and-cisco-anyconnect/)

## Pulse Secure

VPN Protocol: Juniper Network Connect

```
Form action (remediate.cgi) likely indicates that TNCC/Host Checker failed.
Unknown form (name 'frm', id 'frm_142')
Authentication error; cannot obtain cookie
```

- [OpenConnect VPN projects / OpenConnect GUI · GitLab](https://gitlab.com/openconnect/openconnect-gui) - see "Snapshot builds"
- [Openconnect init script](https://gist.github.com/rtgibbons/ae083457d0962bd3fe3f)


> OpenConnect does not yet support all of the authentication options used by Pulse, nor does it support Host Checker/TNCC with Pulse

- [add TNCC support for Pulse protocol (#206) · Issues · OpenConnect VPN projects / OpenConnect · GitLab](https://gitlab.com/openconnect/openconnect/-/issues/206)

- [Client Download | Pulse Secure](https://www.pulsesecure.net/trynow/client-download/)
- [Get Pulse Secure - Microsoft Store](https://www.microsoft.com/en-us/p/pulse-secure/9nblggh3b0bp#activetab=pivot:overviewtab) - as VPN service in Windows, not work with all server configurations (and doesn't support "TNCC/Host Checker"?)

## Outlook

- [How to delete Skype for Business Contacts from Outlook - Sean Wallbridge - BrainLitter](https://itgroove.net/brainlitter/2016/06/10/7835/)

## Notepad++

- [How to install a Notepad++ plugin offline? - Stack Overflow](https://stackoverflow.com/questions/40015350/how-to-install-a-notepad-plugin-offline/52629470#52629470)

For Function List Panel (View > Function List) with Markdown:

In `functionList.xml` `/NotepadPlus/functionList/associationMap`:

```xml
<association id=    "markdown_title"      userDefinedLangName="Markdown" />
<!-- ======================================================================== -->
```

And in `/NotepadPlus/functionList/parsers` (use Perl/PCRE regex):

```xml
<!-- ============================================== [ Markdown ] -->
<!--
|   https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#headers
|   https://daringfireball.net/projects/markdown/syntax#header
\-->
<parser id="markdown_header" displayName="Markdown Header">
	<function
		mainExpr="(?x)                            					# Utilize inline comments (see `RegEx - Pattern Modifiers`)
					(?m)
					^												# start-of-line
					(?:
																	# ATX style
						\#{1,6}										# hash
						[ ]+										# space
						[^\r\n]*$									# whatever, until end-of-line
					|
																	# Setext style
						[^-\s]										# not start with - (used for list) or whitespaces
						[^\r\n]*									# whatever
						(?=											# lookafter
							\r?\n									# new line
							(?:
								=+									# underlining =
							|	-+									# underlining -
							)
							[ ]*									# optional spaces
							$
						)
					)
				"
	>
		<functionName>
			<!-- use if you need hierachy <nameExpr expr="^.*$(?= *#* *)$" /> -->
			<nameExpr expr="^(#* +)?\K.*$(?= *#* *)$" />
		</functionName>
	</function>
</parser>
```

- `%APPDATA%\Notepad++\userDefineLang.xml` and `functionList.xml`
- [nea/MarkdownViewerPlusPlus: A Notepad++ Plugin to view a Markdown file rendered on-the-fly](https://github.com/nea/MarkdownViewerPlusPlus)
- [Edditoria/markdown-plus-plus: Markdown syntax highlighting for Notepad++, by customized UDL (user defined language) file](https://github.com/Edditoria/markdown-plus-plus)
- [Notepad++ Function List](https://notepad-plus-plus.org/features/function-list.html)
- [xml - Notepad++ Custom Function List (Basic) - Stack Overflow](https://stackoverflow.com/questions/27046002/notepad-custom-function-list-basic)
- [regex - Extract Function name from Notepad++ for FunctionList - Stack Overflow](https://stackoverflow.com/questions/48410830/extract-function-name-from-notepad-for-functionlist)
- [Editing Configuration Files - Notepad++ Wiki](http://docs.notepad-plus-plus.org/index.php/Editing_Configuration_Files#FunctionList)
- [Function List - Notepad++ Wiki](http://docs.notepad-plus-plus.org/index.php/Function_List)

## WhatsApp

Backup WhatsApp data for iOS

- `AppDomainGroup group.net.whatsapp.WhatsApp.shared/ChatStorage.sqlite`
- [4 Ways to Transfer WhatsApp from iPhone to Android](https://web.archive.org/web/20210121165501/https://mobiletrans.wondershare.com/whatsapp/transfer-whatsapp-from-iphone-to-android.html)
- [lbalogh/WhatsAppDBReader: Open a WhatsApp database and display conversations](https://github.com/lbalogh/WhatsAppDBReader)
- [wiggin15/whatsapp_history: Get full chat history from Whatsapp and SMS/iMessage](https://github.com/wiggin15/whatsapp_history)

## Saved games and profiles

- GTA V: `%USERPROFILE%\Documents\Rockstar Games\GTA V\Profiles\<8 hexadecimals>` or in `%PROGRAMDATA%\Socialclub\<8 hexadecimals>` or in `%USERPROFILE%\Documents\Rockstar Games\Social Club\Profiles\<8 hexadecimals>` and contains
	- `cfg.dat`
	- `pc_settings.bin`
	- `SGTA50000`
	- `SGTA50000.bak`
	- `SGTA50015`
	- `SGTA50015.bak`
- Age of Empires: Definitive Edition: `%USERPROFILE%\Games\Age of Empires DE\Users\<user name>\Saved Games\*.aoe2spgame`
- Age of Empires 2: Definitive Edition: `%USERPROFILE%\Games\Age of Empires 2 DE\<17 digits>\savegame\*.aoe2spgame`
- World War Z: `%LOCALAPPDATA%\Saber\WWZ\client\storage`

## Tower

- [Tower - Account Management](https://account.git-tower.com/account/licenses)

On Windows:

- binaries: `%USERPROFILE%\AppData\Local\Tower`
- settings: `%USERPROFILE%\AppData\Local\fournova\Tower`
- enable logging by set in `%USERPROFILE%\AppData\Local\fournova\Tower\Settings\main.settings` the keys `EnableLog` and `EnableRestLog` to `true`. This will generate for the next application start log files in `%USERPROFILE%\AppData\Local\fournova\Tower\logs`

## SketchUp

- Free SketchUp : SketchUp Make 2017
	- [Downloading older versions | SketchUp Help](https://web.archive.org/web/20220330135556/https://help.sketchup.com/en/downloading-older-versions)
		- https://web.archive.org/web/20220217222923/https://download.sketchup.com/sketchupmake-2017-3-116-90851-en.dmg
		- https://web.archive.org/web/20220217222923/https://download.sketchup.com/sketchupmake-2017-2-2555-90782-en-x64.exe
