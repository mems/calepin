## Resources

```sh
purge
```

- https://github.com/emred/osx-hack/blob/master/hack.sh
- https://gist.github.com/brandonb927/3195465#file-osx-for-hackers-sh
- [Mac system defaults tricks](https://gist.github.com/maxfenton/c5a316f4254d27b18cf3#file-defaults-md)
- [osx - The time using 'Set date and time automatically' differs between OS X and iOS - Ask Different](http://apple.stackexchange.com/questions/138486/the-time-using-set-date-and-time-automatically-differs-between-os-x-and-ios)
- https://archive.is/20150913113549/http://osxnotes.net/
- https://github.com/herrbischoff/awesome-osx-command-line
- [A practical guide to securing macOS](https://github.com/drduh/macOS-Security-and-Privacy-Guide)
- Self-hosting Apple Software Updates https://github.com/wdas/reposado
- [Startup key combinations for Mac - Apple Support](https://support.apple.com/en-us/HT201255)
- [Macs – The Eclectic Light Company](https://eclecticlight.co/category/macs/)
- [Mac OS X - ForensicsWiki](http://www.forensicswiki.org/wiki/Mac_OS_X)

## Time Machine

### Informations

> (Using AFP only) These presumably allow the disk image engine to force disk image journal data to write out all the way to the disk. Without such features, a network interruption can result in a corrupted filesystem on the disk image despite journaling. Remember, journaling relies on the journal being written all the way to disk before the changes take place. If you can't guarantee that (e.g., because of network/NAS buffering) then the journal is useless. Time Machine appears to rely heavily on disk journaling to deal with network drop-outs, interrupted backups, and the like. Take this away and your data is at risk.

- [Time Machine (OS X) — Wikipedia](https://en.wikipedia.org/wiki/Time_Machine_(OS_X)#How_it_works)
- [Time Machine Information | The Matrix Data Bank](http://www.schollnick.net/wordpress/macintosh-related/time-machine-information/)
- [Apple  OSX  and  Time  Machine  Tips](http://pondini.org/TM/Home.html) [Apple  OSX  and  Time  Machine  Tips](https://web.archive.org/web/20171011022033/http://pondini.org/TM/Home.html)
- (association between backupbundle and the machine via UUID) [Snow Leopard Time Machine Tweaks | Missives](https://porkrind.org/missives/snow-leopard-time-machine-tweaks/)
- [Dissecting Time Machine & Replacing It With rsync | Mr. Backup Blog](http://www.backupcentral.com/mr-backup-blog-mainmenu-47/13-mr-backup-blog/282-time-machine-rsync.html)
- [Format SparseBundle](../../Formats,%20encoding%20and%20protocols/Sparse%20bundle/Sparse%20bundle.md)
- [An Easier Way to Set Up Time Machine to Back Up to a Networked Windows Computer](http://lifehacker.com/5691649/an-easier-way-to-set-up-time-machine-to-back-up-to-a-networked-windows-computer)

- [I learned all about Time (Machine) so you don't have to | The Occasional Blog](http://mike.peay.us/blog/archives/248)
- [Mass Deploying Time Machine in Mac OS X Lion | krypted.com](http://krypted.com/mac-security/mass-deploying-time-machine/)
- [Time Machine 10.8 – Part 3 – Advanced Features > Amsys](http://www.amsys.co.uk/2013/04/time-machine-10-8-part-3-advanced-features/)
- automount remote disk at `/Volumes/.timemachine/{remote-machine-name}`
- TM process name: `com.apple.backupd`.
- Open `system.log` with Console.app, search for `backupd`
- ignore disk to be a TM target: `touch ".com.apple.timemachine.donotpresent"` in the root of the disk
- `.com.apple.timemachine.supported` if the folder must be backup by Time Machine
- current files used by Time Machine `sudo fs_usage -w -f filesys backupd`
- files ignored by TM with extended attribute `sudo mdfind "com_apple_backup_excludeItem = 'com.apple.backupd'"`
- [The ins and outs of using tmutil to backup, restore, and review Time Machine backups - krypted](https://krypted.com/mac-os-x/ins-outs-using-tmutil-backup-restore-review-time-machine-backups/)
- [Consolation, T2M2, Ulbow and log utilities – The Eclectic Light Company](https://eclecticlight.co/consolation-t2m2-and-log-utilities/) - T2M2 (TheTimeMachineMechanic) summarise TM logs, Mints
- [TM-Utilities  - Arthur Rosel, Ltd.](http://7clinton.com/TM-UtilitiesHelp.html)

Time Machine backup fiability:

- [Why I Don’t Rely on Time Machine](https://joeontech.net/why-i-dont-rely-on-time-machine.html)
- [Do you trust TimeMachine as backup/archival storage? : osx](https://www.reddit.com/r/osx/comments/4a8qtz/do_you_trust_timemachine_as_backuparchival_storage/)
- [Never.Ever.Trust.Time.Machine! | MacRumors Forums](http://forums.macrumors.com/threads/never-ever-trust-time-machine.1721681/)
- [Do not trust your Time Machine backups | Official Apple Support Communities](https://discussions.apple.com/thread/6323069?tstart=0)

### Similar tools

- [Time Machine for every Unix out there - IMHO](https://blog.interlinked.org/tutorials/rsync_time_machine.html)
	`.snapshots/daily.0/`

	```sh
	#!/bin/sh
	date=`date "+%Y-%m-%dT%H:%M:%S"`
	HOME=/home/user/
	rsync -aP \
		--link-dest=$HOME/Backups/current\
		$HOME $HOME/Backups/back-$date.incomplete
	mv $HOME/Backups/back-$date.incomplete $HOME/Backups/back-$date
	ln -sf back-$date $HOME/Backups/current
	```

	```sh
	#!/bin/sh
	date=`date "+%Y-%m-%dT%H_%M_%S"`
	HOME=/home/user/
	rsync -azP \
		--delete \
		--delete-excluded \
		--exclude-from=$HOME/.rsync/exclude \
		--link-dest=../current \
		$HOME user@backupserver:Backups/incomplete_back-$date \
	&& ssh user@backupserver \
		"mv Backups/incomplete_back-$date Backups/back-$date \
		&& ln -sf back-$date Backups/current"
	```

	See also [Easy Automated Snapshot-Style Backups with Rsync](http://www.mikerubel.org/computers/rsync_snapshots/)
- [osx - Using rsync to backup - Ask Different](http://apple.stackexchange.com/questions/224747/using-rsync-to-backup)
- [How to install & compile rsync on Mac OSX](https://gist.github.com/Sounds-of-Science/7561838) - Install rsync 3.x on macOS without macport or brew
- In Win 8+ use [File History](http://windows.microsoft.com/en-us/windows-8/how-use-file-history). It use Shadow Copy Service and backupd to VHD format. See also [Backup and Restore](https://en.wikipedia.org/wiki/Backup_and_Restore) and [File History](https://en.wikipedia.org/wiki/Features_new_to_Windows_8#File_History)
- [backup - Does an equivalent of Time Machine exist for Windows? - Super User](http://superuser.com/questions/7423/does-an-equivalent-of-time-machine-exist-for-windows)
- [duplicity: Main](http://duplicity.nongnu.org/)
- [Déjà Vu](http://propagandaprod.com/)
- [Fake Time Machine](https://gist.github.com/pmarreck/1237806)
- [Dissecting Time Machine & Replacing It With rsync | Mr. Backup Blog](http://www.backupcentral.com/mr-backup-blog-mainmenu-47/13-mr-backup-blog/282-time-machine-rsync.html)
- [Google Code Archive - Long-term storage for Google Code Project Hosting.](https://code.google.com/archive/p/flyback/) and [FlyBack — Wikipedia](https://en.wikipedia.org/wiki/FlyBack)
- https://github.com/samdoran/rsync-time-machine (see also https://github.com/samdoran/rsync-time-machine/commit/3610f7c73c2b1f8617c7462d880e12e73611d6b4#commitcomment-13078199 and https://github.com/minolasoft/rsync-time-machine)
- https://github.com/laurent22/rsync-time-backup
- [TimeVault - Ubuntu Wiki](https://wiki.ubuntu.com/TimeVault)
- [List of backup software — Wikipedia](https://en.wikipedia.org/wiki/List_of_backup_software)
- [Backing Up Your Mac: The Online Appendixes](https://joeontech.net/extras/buym/)
- [iBackup](http://grapefruit.ch/iBackup/)
- [rsnapshot | rsnapshot](http://rsnapshot.org/)
- [Cronopete](https://rastersoft.com/programas/cronopete.html)

GUI for rsync

- [arRsync](http://arrsync.sourceforge.net/) (for the source code, see `arrsync-X.X.X.tar.gz` and `arrsync-X.X.X.tar.bz2`)
- https://github.com/mileswu/arrsync
- [Documentation by rsyncOSX](https://rsyncosx.github.io/Documentation/)
- [OPByte: Grsync rsync GUI interface frontend for Linux, Windows and Mac OS X](http://www.opbyte.it/grsync/)

### Include files and folders

Included by default

From `$IBACKUP_APP/Contents/Resources/System Settings/` [iBackup](http://grapefruit.ch/iBackup/)

- Address Book (Cards, Groups, Plug-Ins)
	```
	~/Library/Address Book Plug-Ins
	~/Library/Application Support/AddressBook
	~/Library/Preferences/AddressBookMe.plist
	~/Library/Preferences/com.apple.AddressBook.plist
	```
- Dashboard
	```
	~/Library/Preferences/com.apple.dashboard.client.plist
	~/Library/Preferences/com.apple.dashboard.plist
	~/Library/Widgets
	```
- Desktop Pictures
	```
	~/Library/Desktop Pictures
	```
- Fonts
	```
	~/Library/Fonts
	```
- Keychains
	```
	~/Library/Keychains
	~/Library/Preferences/com.apple.keychainaccess.plist
	```
- Mail (Accounts, Mailboxes, Messages)
	```
	~/Library/Mail
	~/Library/Preferences/com.apple.mail.plist
	~/Library/Preferences/com.apple.mail.searchhistory
	~/Library/Mail Downloads
	```
- Printers
	```
	~/Library/Printers
	~/Library/Preferences/com.apple.print.custompresets.plist
	~/Library/Preferences/com.apple.print.PrintCenter.plist
	```
- Safari (Bookmarks, History, Preferences)
	```
	~/Library/Safari
	~/Library/Preferences/com.apple.Safari.plist
	~/Library/Cookies
	```
- Screen Savers
	```
	~/Library/Screen Savers
	```
- System Preferences (Bluetooth, Dock, Services ...)
	```
	~/Library/Application Support/Apple
	~/Library/Logs
	~/Library/PreferencePanes
	~/Library/Preferences/com.apple.ActivityMonitor.plist
	~/Library/Preferences/com.apple.airport.adminutility.plist
	~/Library/Preferences/com.apple.AppleShareClient
	~/Library/Preferences/com.apple.Aperture.plist
	~/Library/Preferences/com.apple.BezelServices.plist
	~/Library/Preferences/com.apple.Bluetooth.plist
	~/Library/Preferences/com.apple.BluetoothFileExchange.plist
	~/Library/Preferences/com.apple.BluetoothFirmwareUpdater.plist
	~/Library/Preferences/com.apple.calculator.plist
	~/Library/Preferences/com.apple.Console.plist
	~/Library/Preferences/com.apple.desktop.plist
	~/Library/Preferences/com.apple.DiskUtility.plist
	~/Library/Preferences/com.apple.dock.plist
	~/Library/Preferences/com.apple.DotMacSync.plist
	~/Library/Preferences/com.apple.driver.AppleHIDMouse.plist
	~/Library/Preferences/com.apple.finder.plist
	~/Library/Preferences/com.apple.FolderActions.plist
	~/Library/Preferences/com.apple.FontBook.plist
	~/Library/Preferences/com.apple.frontrow.plist
	~/Library/Preferences/com.apple.help.plist
	~/Library/Preferences/com.apple.helpviewer.plist
	~/Library/Preferences/com.apple.HIToolbox.plist
	~/Library/Preferences/com.apple.InterfaceBuilder.plist
	~/Library/Preferences/com.apple.InterfaceBuilder3
	~/Library/Preferences/com.apple.internetconfig.plist
	~/Library/Preferences/com.apple.internetconfigpriv.plist
	~/Library/Preferences/com.apple.LaunchServices.plist
	~/Library/Preferences/com.apple.loginwindow.plist
	~/Library/Preferences/com.apple.MenuBarClock.plist
	~/Library/Preferences/com.apple.menuextra.battery.plist
	~/Library/Preferences/com.apple.menuextra.textinput.plist
	~/Library/Preferences/com.apple.PhotoBooth.plist
	~/Library/Preferences/com.apple.NetworkUtility.plist
	~/Library/Preferences/com.apple.preference.desktopscreeneffect
	~/Library/Preferences/com.apple.Preview.bookmarks.plist
	~/Library/Preferences/com.apple.Preview.plist
	~/Library/Preferences/com.apple.PropertyListEditor.plist
	~/Library/Preferences/com.apple.recentitems.plist
	~/Library/Preferences/com.apple.scheduler.plist
	~/Library/Preferences/com.apple.ScriptEditor2.plist
	~/Library/Preferences/com.apple.Sherlock.plist
	~/Library/Preferences/com.apple.sidebarlists.plist
	~/Library/Preferences/com.apple.spotlight.plist
	~/Library/Preferences/com.apple.symbolichotkeys.plist
	~/Library/Preferences/com.apple.systempreferences.plist
	~/Library/Preferences/com.apple.systemuiserver.plist
	~/Library/Preferences/com.apple.Terminal.plist
	~/Library/Preferences/com.apple.TextEdit.plist
	~/Library/Preferences/com.apple.universalaccess.plist
	~/Library/Preferences/com.apple.x11.plist
	~/Library/Preferences/com.apple.Xcode.plist
	~/Library/Preferences/loginwindow.plist
	~/Library/Preferences/Sherlock
	~/Library/Recent Servers
	~/Library/Services
	~/Library/Scripts
	~/Library/Spotlight
	/Library/Preferences/com.apple.sharing.firewall.plist
	```
- iCal (Alarms, Events, To Do, Calendars)
	```
	~/Library/Calendars
	~/Library/Preferences/com.apple.iCal.alarmsCache.plist
	~/Library/Preferences/com.apple.iCal.AlarmScheduler.plist
	~/Library/Preferences/com.apple.iCal.plist
	~/Library/Preferences/com.apple.iCal.sources.plist
	~/Library/Application Support/iCal
	```
- iChat (Accounts, Preferences)
	```
	~/Library/Preferences/com.apple.iChat.AIM.plist
	~/Library/Preferences/com.apple.iChat.Jabber.plist
	~/Library/Preferences/com.apple.iChat.plist
	~/Library/Preferences/com.apple.iChat.SubNet.plist
	~/Library/Preferences/com.apple.iChatAgent.plist
	```
- iMovie (Preferences)
	```
	~/Library/iMovie
	~/Library/Preferences/com.apple.iMovie7.plist
	```
- iPhone
	```
	~/Library/Application Support/MobileSync/Backup
	```
- iPhoto
	```
	~/Library/Preferences/com.apple.iPhoto.plist
	```
- iPod
	```
	~/Library/Preferences/com.apple.iPod.plist
	```
- iTunes
	```
	~/Library/iTunes
	~/Library/Preferences/com.apple.iTunes.eq.plist
	~/Library/Preferences/com.apple.iTunes.plist
	```

### Exclude drives, folders and files

By default some folder/files are excluded. But some are not to allow a full restoration of a viable system (ex: `/private/var/log/` and its folders are kept but not their files).

How to:

- Fixed path exclusions System Preferences > Time Machine > Options, similar to `sudo tmutil addexclusion -p <drive, dir or file>` (but it's not the same). See also `/Library/Preferences/com.apple.TimeMachine.plist` and `/System/Library/CoreServices/backupd.bundle/Contents/Resources/StdExclusions.plist`
- Sticky exclusions `tmutil addexclusion <drive, dir or file>` same as `xattr -w com.apple.metadata:com_apple_backup_excludeItem com.apple.backupd <filename>`. ~~This not work for [files inside packages](http://apple.stackexchange.com/questions/158213/programmatically-mark-files-to-be-ignored-by-time-machine) (Spotlight don't index files in packages)~~
	`find /path/to/projects -type d  -path '*node_modules/*' -prune -o -type d -name 'node_modules' -exec xattr -w com.apple.metadata:com_apple_backup_excludeItem com.apple.backupd '{}' \;`
- files ignored by Spotlight still backup by Time Machine

Find sticky excluded files/folders `sudo mdfind "com_apple_backup_excludeItem = 'com.apple.backupd'"`

See also

- [How Time Machine Works its Magic Inclusion and Exclusion handling and the Preferences file](http://pondini.org/TM/Works4.html)
- [Time Machine - Frequently Asked Questions 11. What should I exclude, and what should I not exclude?](http://pondini.org/TM/11.html)
- [Exclude Mac OS X system, cache, log, and deleted files](http://www.immortalfiles.com/exclude-mac-os-x-system-cache-log-and-deleted-files.html)
- [osx - Where does Time Machine store its settings? - Ask Different](http://apple.stackexchange.com/questions/33494/where-does-time-machine-store-its-settings)
- [osx - On OS X, what files are excluded by rule from a Time Machine backup? - Ask Different](http://apple.stackexchange.com/questions/25779/on-os-x-what-files-are-excluded-by-rule-from-a-time-machine-backup)
- [backup - How to force a Time Machine deep traversal? - Ask Different](http://apple.stackexchange.com/questions/43631/how-to-force-a-time-machine-deep-traversal)
- Inspect bytecode of CCleanerLib, contains debug symbols

#### General

- `~/Download`
- `/Applications/Install OS X Yosemite.app`
- Folder of Dropbox, Box, Google Drive, iCloud (`~/Library/Mobile Documents/`) etc.

#### System

- (not adviced) `/private/var/folders/%random%/%random%/0/com.apple.LaunchServices-134$(id -u).csstore`
	Sometime this file is updated too often (< 1h) (after each Time Machine backup?)
	Maybe a rebuild is necessary: `find /System/Library/Frameworks -type f -name "lsregister" -exec {} -kill -seed -r \;` or `find /System/Library/Frameworks -type f -name "lsregister" -exec {} -kill -r -domain local -domain system -domain user \;`
	[Launch Services Database file](http://superuser.com/questions/20822/where-does-mac-os-x-store-file-association-information) is per user file
	134 on OSX 10.11, an other number on other OSX version) contains software file type/protocol association and maybe Login Items too
	See [com.apple.LaunchServices-014501.csstore keeps r... | Official Apple Support Communities](https://discussions.apple.com/thread/618919?tstart=0)
- (can break restoration of the system, contains small files) [`/private/var/db/BootCaches/`](http://www.real-world-systems.com/docs/bootCache.html) and `/private/var/db/systemstats`
- `~/.bash_sessions`

By exploring Time Machine backups delete backup of content of `/private/var/folders/` and files `/private/var/log/` (but keep folders tree intact)

- [Solving a "login loop" in Mac OS X Lion due to corrupt LaunchServices cache - Marcin's Musings](http://junkheap.net/blog/2011/09/22/solving-a-login-loop-in-mac-os-x-lion-due-to-corrupt/)

#### Steam

- `~/Library/Application Support/Steam/config/htmlcache`
- `~/Library/Application Support/Steam/appcache`
- [`~/Library/Application Support/Steam/SteamApps`](https://support.steampowered.com/kb_article.php?ref=7471-LWMD-2716)

#### Virtual Machines and simulators

VMware, Parallels, VirtualBox, etc.

- `Virtual Machines.localized` VMware Fusion
- `/Library/Developer/CoreSimulator/Profiles/Runtimes` iOS simulator
- `/Library/Android/sdk/system-images` Android SDK (depends installed location)

If possible, enable option to split vitual machine hard disk into small chunks. (VMWare Player: New Virtual Machine Wizard > Specify Disk Capacity > Split virtual disk into multiple files)

or use [sparse bundle to store VMs disks](http://wayback.archive.org/web/20150808000259/http://www.markwheadon.com/blog/2009/06/backing-up-virtual-machine-using-sparse-bundle/)

#### Adobe Creative Suite

- `~/Library/Preferences/Adobe/After Effects/11.0/Adobe After Effects Disk Cache - XXXXX.noindex` (should be already ignored by Spotlight, but seem not work)
- Photoshop scratch disk's temp files (where ?)

#### Lightroom

- `~/Pictures/Lightroom/Lightroom 5 Catalog Previews.lrdata`
- `~/Pictures/Lightroom/Lightroom 5 Catalog Smart Previews.lrdata`

#### Xcode

- `/Applications/Xcode.app`
- `~/Library/Developer/Shared/Documentation/DocSets`
- `~/Library/Developer/Xcode/DerivedData`

#### Google Chrome (see also Canary)

- [`~/Library/Application Support/Google/Chrome/Default/Application Cache`](https://code.google.com/p/chromium/issues/detail?id=28780) and https://code.google.com/p/chromium/issues/detail?id=25959
- `~/Library/Application Support/Google/Chrome/Default/GPUCache`
- `~/Library/Application Support/Google/Chrome/ShaderCache`
- `~/Library/Application Support/Google/Chrome/Default/Extension Rules/XXXXXX.log`
- `~/Library/Application Support/Google/Chrome/Default/Extension Rules/LOG`
- `~/Library/Application Support/Google/Chrome/Default/Extension Rules/LOG.old`
- `~/Library/Application Support/Google/Chrome/Default/Extension State/XXXXXX.log`
- `~/Library/Application Support/Google/Chrome/Default/Extension State/LOG`
- `~/Library/Application Support/Google/Chrome/Default/Extension State/LOG.old`
- `~/Library/Application Support/Google/Chrome/Default/Session Storage/XXXXXX.log`
- `~/Library/Application Support/Google/Chrome/Default/Session Storage/LOG`
- `~/Library/Application Support/Google/Chrome/Default/Session Storage/LOG.old`

- [Excluding Chrome's session storage from Time Machine - Ask Different](http://apple.stackexchange.com/questions/135668/excluding-chromes-session-storage-from-time-machine)

#### Spotify

- `~/Library/Application Support/Spotify/PersistentCache` (by default) or the path of Spotify Preferences > Advanced > Memory Cache

#### jDownloader

- `/Applications/jDownloader.app/Contents/java/app/tmp` (use fixed path exclusion)
- `/Applications/jDownloader.app/Contents/java/app/logs` (use fixed path exclusion)

#### Firefox

In `~/Library/Application Support/Firefox/Profiles/%ff_profile_id%/` files likes `places.sqlite`, `cookies.sqlite`, `content-prefs.sqlite` and `webappsstore.sqlite` can be quite big (N * 10MB) and often updated. Clean history and clean cookies or change `places.history.expiration.max_pages` and or `places.history.expiration.interval_seconds`. Could be [safely deleted](http://kb.mozillazine.org/Webappsstore.sqlite#Deleting) (a new file will be created when it is needed).
Clean up sqlite DB (reduce size): `echo "VACUUM;" | sqlite3 places.sqlite`. See https://wiki.mozilla.org/Firefox/Projects/Places_Vacuum

`~/Library/Application Support/Firefox/Profiles/%ff_profile_id%/weave/logs` could be excluded too

#### Thunderbird

See Firefox for `places.sqlite`, `cookies.sqlite`, `content-prefs.sqlite` and `webappsstore.sqlite`

- use maildir format in Thunderbird (store each email as individual file instead of a big file containing all emails)
- `~/Library/Thunderbird/Profiles/%tb_profile_id%/global-messages-db.sqlite`
- `~/Library/Thunderbird/Profiles/%tb_profile_id%/global-messages-db.sqlite-journal`
- `~/Library/Thunderbird/Profiles/%tb_profile_id%/panacea.dat` (Mail folder cache. It can be [safely deleted](http://kb.mozillazine.org/Files_and_folders_in_the_profile_-_Thunderbird))

- [Rebuilding the Global Database | Thunderbird Help](https://support.mozilla.org/en-US/kb/rebuilding-global-database)

#### MySQL

Use "InnoDB File-Per-Table Tablespaces":

In `my.cnf`

	[mysqld]
	innodb_file_per_table=1

- [database - How to shrink/purge ibdata1 file in MySQL - Stack Overflow](https://stackoverflow.com/questions/3456159/how-to-shrink-purge-ibdata1-file-in-mysql)

### Explore sparsebundle

Mount `*.sparsebundle` / `*.backupbundle` first: `hdiutil attach My.sparsebundle`

- `tmutil` (with `compare`, `uniquesize` or `calculatedrift`): `tmutil compare /Volumes/MyBackupVolume/Backups.backupdb/$COMPUTE_NAME%/2016-02-18-090818 /Volumes/MyBackupVolume/Backups.backupdb/$COMPUTE_NAME/2016-02-18-102050`. `+` added file, `-` removed file, `!` changed file
- `diskutil umount force /Volumes/com.apple.TimeMachine.TM_Prime-DA16D91F-3320-4834-91ED-2902CE57E46D`
- [BackupLoupe](http://www.soma-zone.com/BackupLoupe/) - Explore version (compare changes, size)
- [tms](https://github.com/toy/tms)
- [TimeTracker by CharlesSoft](http://www.charlessoft.com/) - Not work well with network drives
- [timedog](https://github.com/nlfiedler/timedog)
- `find /path/to/your/latest/backup -type f -links 1 -print` (Time Machine use hardlinks for unmodified files). But not realy usefull since some folder use hardlink too (and you can't exlude file in hardlinked folders)

### Control when to backup

More control, by can impact performances (battery, powernap, integrity, etc.)

Change:

- (before 10.8) `sudo defaults write /System/Library/LaunchDaemons/com.apple.backupd-auto StartInterval -int 7200` (7200 in seconds eq. 2 hours)
- (10.8+) update `BackupInterval` in `/System/Library/LaunchDaemons/com.apple.backupd-auto.plist`

Or use an app:

- Time Machine Destination Manager: https://github.com/dustinrue/Tedium and [Tedium for Mac | MacUpdate](http://www.macupdate.com/app/mac/41700/tedium)
- [TimeMachineEditor](http://tclementdev.com/timemachineeditor/)
- [TimeMachineScheduler - set the backup interval of Time Machine](http://www.klieme.com/TimeMachineScheduler.html) or [TimeMachineEditor](http://timesoftware.free.fr/timemachineeditor/) or update `sudo defaults write /System/Library/LaunchDaemons/com.apple.backupd-auto StartInterval -int 3600` (for 1 hours, 7200 = 2 hours, etc.)
- Use cron task
	By controling when enable/disable/start it:

	`sudo tmutil enable|disable` or `defaults write /Library/Preferences/com.apple.TimeMachine AutoBackup -boolean YES|NO` or `tmutil startbackup --auto --block`

	- [How can I execute sudo commands as a cron job? - Ask Different](http://apple.stackexchange.com/questions/27181/how-can-i-execute-sudo-commands-as-a-cron-job)

### Reduce size

```sh
tmutil listbackups
sudo tmutil delete '/Volumes/Time Machine Backups/Backups.backupdb/.../2018-'{01,02,03,04}*
sudo hdiutil compact '/Volumes/....sparsebundle'
```

- [Shrink Your Time Machine Backups and Free Disk Space - DZone Performance](https://dzone.com/articles/shrink-your-time-machine)
- [Create or resize sparsebundle](#create-or-resize-sparsebundle)
- [If the Time Machine backup disk for your Mac is full - Apple Support](https://support.apple.com/guide/mac-help/if-the-time-machine-backup-disk-is-full-mh15137/mac)
- [macos - How can I delete Time Machine files using the commandline - Super User](https://superuser.com/questions/162690/how-can-i-delete-time-machine-files-using-the-commandline/557425#557425)

#### Remove specific file from Time Machine backup

- `cd "/Volumes/Time Machine Backups/Backups.backupdb/<machinename>"`
- `ls -li *"/<drivename>/<path>/"*`, `sudo bypass rm -rf *"/<drivename>/<path>/"*`
- `ls -li *"/<drivename>/<file>"`, `sudo bypass rm -f *"/<drivename>/<path>/<file>"`
- [time machine - Delete all backups of specific file/folder with tmutil - Ask Different](https://apple.stackexchange.com/questions/333767/delete-all-backups-of-specific-file-folder-with-tmutil/357119#357119)
- [macos - How can I delete Time Machine files using the commandline - Super User](https://superuser.com/questions/162690/how-can-i-delete-time-machine-files-using-the-commandline/912432#912432)
- [macos - How can I delete Time Machine files using the commandline - Super User](https://superuser.com/questions/162690/how-can-i-delete-time-machine-files-using-the-commandline/557425#557425)

### Restore from a Time Machine backup

> You can't restore this backup because it was created by a different model of Mac

Could restore from a Time Machine Backup with [Migration Assistant](#migration-assistant).

Restore from a Time Machine backup should restore all files, but few things are not:

- System Preferences > Keyboard > Keyboard Shortcuts (key mapping, "open terminal here", etc.)
- Few softwares require to re-enter licencies credentials (which depends on hardware finger print?)
- Some login credentials
- System Preferences > Security & Privacy
- scanners and printers drivers and configurations
- file type/protocol association
- Character map recent and favs

Also don't erase immediatly all TM snapshots, some are not complete due to concurency with software that also write on disk in same time (or use large files)

### Change harddrive

```sh
sudo tmutil associatedisk -a mount_point snapshot_volume
sudo tmutil inheritbackup {machine_directory | sparsebundle}
```

- [Time Machine: Inherit Backup Using `tmutil` - Simon Heimlicher](https://simon.heimlicher.com/articles/2012/07/10/time-machine-inherit-backup-using-tmutil)
- [How can I use an existing Time Machine backup with my new computer? - Ask Different](http://apple.stackexchange.com/questions/32841/how-can-i-use-an-existing-time-machine-backup-with-my-new-computer)

### Local snapshots

```sh
sudo tmutil enablelocal
```

```sh
sudo tmutil disablelocal
```

```sh
tmutil snapshot
```

In folder `/.MobileBackups`

- http://pondini.org/TM/30.html
- http://apple.stackexchange.com/questions/80183/any-way-to-change-the-location-of-time-machine-local-backups-mobilebackups-t
- http://support.apple.com/kb/HT4878

### Create or resize sparsebundle

Aka specify a size

Sparsebundle are use on network drives.

Create a sparsebundle of 320GiB or use `320000000000b` (= 320GB)

```sh
hdiutil create -size 320g -type SPARSEBUNDLE -nospotlight -fs "HFS+J" -volname "MyMacBook Time Machine Backup" MyMacBook.sparsebundle
#
# Mount image
open MyMacBook.sparsebundle
# diskutil list
# sudo diskutil enableOwnership /dev/diskXsX
# Set Time Machine a destination volume
sudo tmutil setdestination "/Volumes/MyMacBook Time Machine Backup"
```

To create dynamic sparsebundle, create it without partition scheme.

Sparsebundle will increase by it's content

You can shrink sparseimage directly (should not be used). Could require a `compact` before

```sh
hdiutil resize -size 320g -shrinkonly /Volumes/Network_Drive_Name/path/to/timemachine.sparseimage
# -limits will just displays the minimum, current, and maximum sizes (in 512-byte sectors)
```

- reclaim unused bands (free space) `sudo hdiutil compact -verbose image.sparsebundle` (could be executed multiple times) or `hdiutil resize -verbose -sectors min image.sparseimage`.
	- [mac osx - How to reclaim all/most free space from a sparsebundle on OS X - Server Fault](https://serverfault.com/questions/14112/how-to-reclaim-all-most-free-space-from-a-sparsebundle-on-os-x)

	To fix `hdiutil: compact failed - internal error` see:
	- [Fixing corrupted time machine backup | Tony Lawrence](http://tonylawrence.com/post/unix/fixing-corrupted-time-machine-backups/)
	- [Repair Time Machine sparsebundle that will no longer mount - Ask Different](https://apple.stackexchange.com/questions/18482/repair-time-machine-sparsebundle-that-will-no-longer-mount/39842#39842)
- [Using Time Machine on unsupported volumes - Mac OS X Hints](http://hints.macworld.com/article.php?story=20140415132734925)
- [10.6: Set up Time Machine on networked AFP volume - Mac OS X Hints](http://hints.macworld.com/article.php?story=20090905212640957)
- [hdiutil returns error trying to resize sparsebu... | Apple Support Communities](https://discussions.apple.com/thread/2506183)
	If the image is large, try to resize in stages (2TB -> 1,5TB -> 500GB -> 10GB) or will there an error: `hdiutil: resize failed - Cannot allocate memory`
- [Time Machine - Troubleshooting A8. Changing the size or case-sensitivity of a sparse bundle](http://pondini.org/TM/A8.html)
- http://java.dzone.com/articles/shrink-your-time-machine
- http://www.readynas.com/?p=253

```sh
#!/bin/bash
# A bash script to create a time machine disk image suitable for
# backups with OS X 10.6 (Snow Leopard)
# This script probably only works for me, so try it at your own peril!
# Use, distribute, and modify as you see fit but leave this header intact.
# (R) sunkid - September 5, 2009

usage ()
{
     echo ${errmsg}"\n"
     echo "makeImage.sh"
     echo "	usage: makeImage.sh size [directory]"
     echo "	Create a disk image with a max storage size of <size> and copy it"
     echo "	to your backup volume (if specified)"
}

# test if we have two arguments on the command line
if [ $# -lt 1 ]
then
    usage
    exit
fi

# see if there are two arguments and we can write to the directory
if [ $# == 2 ]
then
	if [ ! -d $2 ]
	then
 		errmsg=${2}": No such directory"
    	usage
    	exit
	fi
	if [ ! -w $2 ]
	then
		errmsg="Cannot write to "${2}
		usage
    	exit
	fi
fi

SIZE=$1
DIR=$2
NAME=`scutil --get ComputerName`;
UUID=`system_profiler SPHardwareDataType | grep 'Hardware UUID' | awk '{print $3}'`

# get busy
echo -n "Generating disk image ${NAME}.sparsebundle with size ${SIZE}GB ... "
hdiutil create -size ${SIZE}G -fs HFS+J -type SPARSEBUNDLE \
	-volname 'Time Machine Backups' "${NAME}.sparsebundle" >> /dev/null 2>&1

echo "done!"

echo -n "Generating property list file with uuid $UUID ... "

PLIST=$(cat <<EOFPLIST
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
        <key>com.apple.backupd.HostUUID</key>
        <string>$UUID</string>
</dict>
</plist>
EOFPLIST
)

echo $PLIST > "${NAME}.sparsebundle"/com.apple.TimeMachine.MachineID.plist
echo "done!"

if [ $# == 2 ]
then
	echo -n "Copying ${NAME}.sparsebundle to $DIR ... "
	cp -pfr "${NAME}.sparsebundle" $DIR/"${NAME}.sparsebundle"
	echo "done"
fi

echo "Finished! Happy backups!"
```

### Change sparsebundle band size

If "Time Machine must recreate a new copy" occure too often, or if after few month of TM use, back is slow, or if the host of the sparsebundle don't support well lot of file in one dir (ex: ext4 <40000)

By default Time Machine use band in sparsebundle with size of 8MiB. It's can be problematic when the size of the backup is > 300GB. 16MiB (32768 blocks) could be a good compromise.

```sh
hdiutil convert -format UDSB -imagekey sparse-band-size=32768 -o new.sparsebundle old.sparsebundle
# Will take lot of time ~ hours
cp old.sparsebundle/com.apple.TimeMachine.MachineID* new.sparsebundle/
```

Note: Increase band size only for unencrypted backups. Large bands could be problematic with encrypted backups (take lot of time): download band, decrypt, update, encrypt then finally upload

> The sparse-band-size parameter is the number of 512-byte sectors (chunks), not the number of bytes. Since 512 is 1/2 1,024, then 262,144 B / 2 = 128 KiB.

Where 262144 equals 128MiB bands/byte sectors (`128 MiBytes == 128*1024*1024 bytes == 128*1024*1024/512 blocks = 262144 blocks`, `262144 / 2 / 1024 = 128MiB`)

Read it (for mounted sparsebundle):

```sh
hdiutil info -verbose | grep band-size
# Or accessible in Info.plist in the .sparsebundle
```

- [Improve Time Machine performance with Big Bands - The Endless Geek](http://endlessgeek.com/2014/03/improve-time-machine-performance-big-bands/)
- [The Reluctant Sysadmin: NAS Time Machine | David Wicks : Writing](http://sansumbrella.com/writing/2012/the-reluctant-sysadmin-nas-time-machine/)
- [OS X: Time Machine backup to Synology DS107+ | naschenweng.info](http://www.naschenweng.info/2008/07/15/os-x-time-machine-backup-to-synology-ds1/)
- [Time Machine on a network drive : you will need to increase the band size … « Zuzur's corner](http://arzur.net/2010/08/31/time-machine-on-a-network-drive-you-will-need-to-increase-the-band-size/)
- [10.5: Improve networked Time Machine performance - Mac OS X Hints](http://hints.macworld.com/article.php?story=2008050913104691)
- https://gist.github.com/Agiley/b3e9af8a641df1dc73c0
- About band size [Why Time Machine use Sparse Bundle Disk Image f... | Apple Support Communities](https://discussions.apple.com/thread/3734638?tstart=0)

### Backup into a sparsebundle file

This format is often created to backup on a shared network volume (that is not HFS+)

Mount it (db click in Finder) and

	sudo tmutil setdestination /Volumes/name-of-the-mounted-sparsebundle

SparseBundle sould be at the root of the volume. A workaround is to create a symbolic link `ln -s /volume1/backups/subfolder/subfolder/BackupImage.sparsebundle BackupImage.sparsebundle`, but only supported on OSX (Unix folder symlink are forbidden)

Can be required

	sudo diskutil enableOwnership /dev/disk2s2

- [Using Time Machine on unsupported volumes - Mac OS X Hints](http://hints.macworld.com/article.php?story=20140415132734925)
- http://pondini.org/TM/18.html#id18
- [How do I move a USB Time Machine backup to a Time Capsule? - Ask Different](http://apple.stackexchange.com/questions/104277/how-do-i-move-a-usb-time-machine-backup-to-a-time-capsule)
- [tmutil(8) Mac OS X Manual Page](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man8/tmutil.8.html)

### Troubleshooting

Catalina have issue with SMB (often disconnected and sometimes can't reconnect). Force to use AFP mounted disk instead. See [Time Machine in Catalina 10.15.3 has serious bugs – The Eclectic Light Company](https://eclecticlight.co/2020/02/12/time-machine-in-catalina-10-15-3-has-serious-bugs/) and [Catalina - no longer access NAS via Finder? Time Machine not working. | Synology Community](https://community.synology.com/enu/forum/1/post/129160)

- [Time Machine problems? Try T2M2: it’ll tell you what’s wrong – The Eclectic Light Company](https://eclecticlight.co/2017/05/22/time-machine-problems-try-t2m2-itll-tell-you-whats-wrong/)
- [maverick - How to repair time machine after it lose it history - Ask Different](https://apple.stackexchange.com/questions/146685/how-to-repair-time-machine-after-it-loses-its-history)
- [Time  Machine  -  Troubleshooting](https://web.archive.org/web/20171013143351/http://pondini.org:80/TM/Troubleshooting.html)
- [Time Machine - Troubleshooting A4.  Full  Reset  of  Time  Machine](https://web.archive.org/web/20171004211421/http://pondini.org:80/TM/A4.html)

#### Stuck on "Preparing backup..."

It's often related to spotlight indexing (can't backup when spotlight is indexing)

- [Fix Time Machine When Stuck on “Preparing Backup” in Mac OS X](http://osxdaily.com/2014/03/31/time-machine-stuck-preparing-backup-mac-fix/)
- [Troubleshooting Time Machine: stuck preparing backup, and the deep event scan – The Eclectic Light Company](https://eclecticlight.co/2017/02/20/troubleshooting-time-machine-stuck-preparing-backup-and-the-deep-event-scan/)

#### The backup is already in use

Aka "Failed to unmount disk mounted at [...]" on the server

On the server, disconnect the user or restart the AFP service

- [time machine - The backup on Server i already in use - Ask Different](https://apple.stackexchange.com/questions/117368/the-backup-on-server-is-already-in-use)

#### Time Machine backup is very slow

Disable low priority process throttle: `sudo sysctl -w debug.lowpri_throttle_enabled=0`. **Check before if it's happend with `sudo fs_usage -w -f filesys backupd`**

See also if it use SMB Shares, it could be slow itself (due to protocol version use or signing).

- [hard drive - Time Machine ridiculously slow after El Capitan upgrade - Ask Different](http://apple.stackexchange.com/questions/212537/time-machine-ridiculously-slow-after-el-capitan-upgrade)
- [Why Mavericks is slow or fast or needs an SSD - Google Groups](https://groups.google.com/forum/#!topic/comp.sys.mac.system/YMB8ATgsaaI)
- [Speed Up Time Machine by Removing Low Process Priority Throttling](http://osxdaily.com/2016/04/17/speed-up-time-machine-by-removing-low-process-priority-throttling/)

#### Other Time Machines errors

- [Fix For Read-Only Sparsebundles - Apple Mac OS X - We Got Served Forums](http://forum.wegotserved.com/index.php?/topic/22874-fix-for-read-only-sparsebundles/)
- [How to fix a Corrupted Time Machine Backup | Jthon's Place](http://blog.jthon.com/?p=31)
- [How to repair a sparsebundle image | tar.gz](http://docs.gz.ro/osx-repair-sparsebundle.html)
- [Repair Time Machine sparsebundle that will no longer mount - Ask Different](http://apple.stackexchange.com/questions/18482/repair-time-machine-sparsebundle-that-will-no-longer-mount)
- [Fix Time Machine Sparsebundle NAS Based Backup Errors | Garth Gillespie](http://www.garth.org/archives/2011,08,27,169,fix-time-machine-sparsebundle-nas-based-backup-errors.html)
- https://github.com/jamespayne/time-machine-sparse-bundle-fix and https://github.com/Parkcomm/time-machine-sparce-bundle-fix
- https://gist.github.com/dipdi/fedb28652f8e7de2b11b

### Time Machine Volume on Network

On non Mac Machine (AFP) or other network protocols

> Sparsebundle disk images cannot, however, be saved on SMB volumes and a handful of other filesystems due to their lack of support for "F_FULLFSYNC", which is a filesystem command that instructs the disk to write data from cache to media.

> If you are using Netatalk version 2.0.5 or better, this has the special new features added to avoid Time Machine disk corruption. If you have a version of Netatalk earlier than 2.0.5 (e.g. Ubuntu 9.10 currently has 2.0.4) [..]
>
> If you have Netatalk 2.0.5 installed, you should add the option “tm” to any share you use for Time Machine, in the AppleVolumes.default config file.
— [Using Ubuntu for Time Machine in Snow Leopard – Delivering Quality](http://www.markdeepwell.com/2009/11/using-ubuntu-for-time-machine-in-snow-leopard/#comment-513)

`sudo tmutil setdestination -p smb://user@Server._smb._tcp.local./Mount` or `sudo tmutil setdestination -p afp://user@Server.local/Mount`

- 10.11 `tmutil version 4.0.0 (built Oct  3 2015)` appears to not support SMB but only AFP. 10,13 `tmutil version 4.0.0 (built Jul 15 2017)` does
- Time Machine use an SMB extension `F_FullfSync` available in SMB3 (SAMBA 4.1 implement it) to ensure that data is actually written to disk. See [MacOS Sierra support Time Machine via SMB- but how? : apple](https://www.reddit.com/r/apple/comments/53upnj/macos_sierra_supports_time_machine_via_smb_but_how/)
- [Time Machine Over SMB Specification](https://developer.apple.com/library/content/releasenotes/NetworkingInternetWeb/Time_Machine_SMB_Spec/index.html)
- [Backup into a sparsebundle file](#backup-into-a-sparsebundle-file)
- `defaults write com.apple.systempreferences TMShowUnsupportedNetworkVolumes 1 && killall Finder` (apparently it's ignored with OSX 10.11, SIP?)
- [HowTo: Make Ubuntu A Perfect Mac File Server And Time Machine Volume ¦ kremalicious](https://kremalicious.com/ubuntu-as-mac-file-server-and-time-machine-volume/)
- Why can't I use a sparsebundle disk image on a filesystem that does not support the F_FULLFSYNC file control? [Backing up to a disk image | Carbon Copy Cloner | Bombich Software](https://bombich.com/kb/ccc4/backing-up-disk-image#fullfsync)

- [mac - Backup strategy for developer-focused Apple environments? - Server Fault](http://serverfault.com/questions/575357/backup-strategy-for-developer-focused-apple-environments)
- [backup - What is a safe way to back up a sparsebundle that is exported via afpd? - Server Fault](http://serverfault.com/questions/594939/what-is-a-safe-way-to-back-up-a-sparsebundle-that-is-exported-via-afpd)
- [Time Machine Server Requirements](https://developer.apple.com/library/mac/documentation/NetworkingInternetWeb/Conceptual/TimeMachineNetworkInterfaceSpecification/TimeMachineRequirements/TimeMachineRequirements.html#//apple_ref/doc/uid/TP40008951-CH100-SW1)

iSCSI initiator

But how to restore, since iSCSI is not supported natively?

- https://github.com/iscsi-osx/iSCSIInitiator
- [Droboshare Dashboard for Mac includes free Xtend SAN iSCSI Initiator (kind of) | Justus Beyer](https://justus.berlin/2014/01/droboshare-dashboard-for-mac-includes-free-xtend-san-iscsi-initiator-kind-of/)
- [Using Time Machine over iSCSI for Mac OS clients – daemonchild.com](https://daemonchild.com/2015/01/30/using-time-machine-over-iscsi-for-mac-os-clients/)
- [how to use iscsi to support an apple time machine](https://wiki.netbsd.org/tutorials/how_to_use_iscsi_to_support_an_apple_time_machine/)

### Large modified files

Since TM it's a file level not block level backup, these files can be corrupted (not include all updates), because rewritten (partially or not) when backup, all changes are not backup. That means this files are backup corrupted.

Ex: Virtual Machine disk

Ex: MySql DB files. Solution: cron mysqldump hourly (or less if large DB) + exlude DB files

## OS

### Install macOS

Use Option-Command (⌘)-R at startup to reinstall lastest version of the OS: [How to reinstall macOS - Apple Support](https://support.apple.com/en-us/HT204904)
For clean install, erase the drive with Disk Utility ([macOS Recovery](https://support.apple.com/en-us/HT201314)) first

Create ISO installer:

```sh
hdiutil create -o /tmp/Catalina -size 8050m -volname Catalina -layout SPUD -fs HFS+J
hdiutil attach /tmp/Catalina.dmg -noverify -mountpoint /Volumes/Catalina
sudo "/Applications/Install macOS Catalina.app/Contents/Resources/createinstallmedia" --volume /Volumes/Catalina --nointeraction
hdiutil detach "/Volumes/Install macOS Catalina"
hdiutil convert /tmp/Catalina.dmg -format UDTO -o ~/Desktop/Catalina.cdr
mv ~/Desktop/Catalina.cdr ~/Desktop/Catalina.iso
```

- [How to reinstall macOS from macOS Recovery - Apple Support](https://support.apple.com/en-us/HT204904)
- [osx - How can I get back a system file after deleting it from my Mac? - Ask Different](http://apple.stackexchange.com/questions/116611/how-can-i-get-back-a-system-file-after-deleting-it-from-my-mac/116612#116612)
- [OSX on Bootable USB](#osx-on-bootable-usb)
- [Restore from a Time Machine backup](#restore-from-a-time-machine-backup)

#### Install on Virtual Machine

```cmd
cd "C:\Program Files\Oracle\VirtualBox\"
#
# Virtualbox 5.x 00000001 000106e5 00100800 0098e3fd bfebfbff
# Virtualbox 4.x 00000001 000306a9 04100800 7fbae3ff bfebfbff
VBoxManage.exe modifyvm "Virtual Machine Name" --cpuidset 00000001 000106e5 00100800 0098e3fd bfebfbff
# use "MacBookPro11,3"
VBoxManage setextradata "Virtual Machine Name" "VBoxInternal/Devices/efi/0/Config/DmiSystemProduct" "iMac11,3"
VBoxManage setextradata "Virtual Machine Name" "VBoxInternal/Devices/efi/0/Config/DmiSystemVersion" "1.0"
# "Mac-2BD1B31983FE1663"
VBoxManage setextradata "Virtual Machine Name" "VBoxInternal/Devices/efi/0/Config/DmiBoardProduct" "Iloveapple"
VBoxManage setextradata "Virtual Machine Name" "VBoxInternal/Devices/smc/0/Config/DeviceKey" "ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc"
VBoxManage setextradata "Virtual Machine Name" "VBoxInternal/Devices/smc/0/Config/GetKeyFromRealSMC" 1
```

- [Creating a macOS Virtual Machine in Fusion](https://docs.vmware.com/en/VMware-Fusion/11/com.vmware.fusion.using.doc/GUID-474FC78E-4E77-42B7-A1C6-12C2F378C5B9.html)
- [myspaghetti/macos-virtualbox: Push-button installer of macOS Catalina, Mojave, and High Sierra guests in Virtualbox for Windows, Linux, and macOS](https://github.com/myspaghetti/macos-virtualbox)
- [kholia/OSX-KVM: Run macOS on QEMU/KVM. Only commercial support is available. With OpenCore + Big Sur support now!](https://github.com/kholia/OSX-KVM)
- [foxlet/macOS-Simple-KVM: Tools to set up a quick macOS VM in QEMU, accelerated by KVM.](https://github.com/foxlet/macOS-Simple-KVM)
- [jonanh/osx-vm-templates: macOS templates for Packer and VeeWee.](https://github.com/jonanh/osx-vm-templates) - [timsutton/osx-vm-templates: macOS templates for Packer and VeeWee.](https://github.com/timsutton/osx-vm-templates)
- [macOS / Hackintosh – Nicholas Sherlock](https://www.nicksherlock.com/category/macos/)
- [Notes on getting macOS Sierra running in Virtualbox on a Windows 10 host](https://gist.github.com/rob-smallshire/0c4403afb0523dd57c9f4b3693344f14)
- [mac - Install macOS High Sierra as VirtualBox guest (on macOS High Sierra)? - Ask Different](https://apple.stackexchange.com/questions/307099/install-macos-high-sierra-as-virtualbox-guest-on-macos-high-sierra)
- [Install macOS Sierra on VirtualBox? - Ask Different](https://apple.stackexchange.com/questions/290643/install-macos-sierra-on-virtualbox)
- [GitHub - paolo-projects/auto-unlocker: Unlocker for VMWare macOS](https://github.com/paolo-projects/auto-unlocker) - Allow macOS to be selected during VM creation + other fixes

### Bootable USB

```sh
hdiutil convert -format UDRW -o /path/to/target.img /path/to/ubuntu.iso
diskutil list
# (determine the device node assigned to your flash media (e.g. /dev/disk2))
diskutil unmountDisk /dev/diskN
sudo dd if=/path/to/downloaded.img.dmg of=/dev/rdiskN bs=1M
diskutil eject /dev/diskN
```

- [How to Copy an ISO to a USB Drive from Mac OS X with dd](http://osxdaily.com/2015/06/05/copy-iso-to-usb-drive-mac-os-x-command/)
- [Installation/FromImgFiles - Community Help Wiki](https://help.ubuntu.com/community/Installation/FromImgFiles)
- [Create a USB stick on OS X | Ubuntu](http://www.ubuntu.com/download/desktop/create-a-usb-stick-on-mac-osx)
- [Installing Debian Linux onto an external USB drive for Mac - AfterEcho - Android, Devops and other stuff](https://afterecho.uk/blog/installing-debian-linux-onto-an-external-usb-drive-for-mac.html)

#### macOS on Bootable USB

On an HFS+ (Journaled) formatted USB drive

	sudo /Applications/Install\ OS\ X\ Yosemite.app/Contents/Resources/createinstallmedia --volume /Volumes/Untitled --applicationpath /Applications/Install\ OS\ X\ Yosemite.app --nointeraction
	sudo /Applications/Install\ macOS\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/Untitled --applicationpath /Applications/Install\ macOS\ Sierra.app --nointeraction

- [How to create a bootable installer for macOS - Apple Support](https://support.apple.com/en-us/HT201372)
- [install - macOS High Sierra media installer - Ask Different](https://apple.stackexchange.com/questions/299731/macos-high-sierra-media-installer)
- http://arstechnica.com/apple/2014/10/how-to-make-your-own-bootable-os-x-10-10-yosemite-usb-install-drive/#image-9
- [How to make your own bootable macOS 10.12 Sierra USB install drive | Ars Technica](http://arstechnica.com/gadgets/2016/09/how-to-make-your-own-bootable-macos-10-12-sierra-usb-install-drive/)

### Bootloader

- [Clover](https://clover-wiki.zetam.org/Home)

### Migration Assistant

> Migration Assistant doesn’t overwrite new versions of applications with older ones
> [...] won’t overwrite an account with the same name by default. Migration Assistant prompts you about whether you want to rename the account from the old computer or overwrite the account on the new computer with the files from the old Mac
> [...] Files stored outside user accounts won’t be overwritten, but they could be merged, so a folder might contain a collection of old and new files.

- Applications (`/Applications` and `/Library/Application`)
- User accounts and groups (reset UserShell and NFSHomeDirectory for created users)
	For macports, see:

	```sh
	#!/bin/sh

	# Fix MacPorts user config
	# Sources here: https://trac.macports.org/browser/trunk/base/portmgr/dmg/postflight.in?rev=154110#L159

	# Variable provided by postinstall script, extracted from MacPort installer package (*.pkg)
	PREFIX="/opt/local"
	DSCL=/usr/bin/dscl
	RUNUSR=macports

	# List all users:
	# ${DSCL} . list /Users | grep -E -v ^_
	# Read user infos
	# ${DSCL} . read "/Users/${RUNUSR}"

	${DSCL} -q . -delete "/Users/${RUNUSR}" AuthenticationAuthority
	${DSCL} -q . -delete "/Users/${RUNUSR}" PasswordPolicyOptions
	${DSCL} -q . -delete "/Users/${RUNUSR}" dsAttrTypeNative:KerberosKeys
	${DSCL} -q . -delete "/Users/${RUNUSR}" dsAttrTypeNative:ShadowHashData
	${DSCL} -q . -create "/Users/${RUNUSR}" RealName MacPorts
	${DSCL} -q . -create "/Users/${RUNUSR}" Password "*"
	${DSCL} -q . -create "/Users/${RUNUSR}" PrimaryGroupID "$(${DSCL} -q . -read "/Groups/${RUNUSR}" PrimaryGroupID | /usr/bin/awk '{print $2}')"
	${DSCL} -q . -create "/Users/${RUNUSR}" NFSHomeDirectory "${PREFIX}/var/macports/home"
	${DSCL} -q . -create "/Users/${RUNUSR}" UserShell /usr/bin/false
	```

	- see [Non interactive user](#non-interactive-user)
	- if FileVault is enabled after macports has been installed (check it with `sudo fdesetup list | grep macports`), it could be necessary to disallow the user to decrypt the disk. Else it's visible on FileVault login window (even if it's a non interactive user). To disallow it: `sudo fdesetup remove -user macports`
	- [#30168 (adduser results in macports users appearing as interactive users) – MacPorts](https://trac.macports.org/ticket/30168#comment:16)
	- [Transferring from Time Machine shows "MacPorts". What is this and should I transfer it? - Ask Different](https://apple.stackexchange.com/questions/275708/transferring-from-time-machine-shows-macports-what-is-this-and-should-i-trans)
	- `dscacheutil -q user -a name macports`
	- [macos - How to delete MacPorts user after using the Migration Assistant - Ask Different](https://apple.stackexchange.com/questions/317576/how-to-delete-macports-user-after-using-the-migration-assistant)

	For Wireshark, see:

	- create user group `access_bpf`
	- [wireshark - what is access_bpf group? - Ask Different](https://apple.stackexchange.com/questions/138694/what-is-access-bpf-group/138728#138728)
	- https://code.wireshark.org/review/gitweb?p=wireshark.git;a=blob;f=packaging/macosx/Scripts/chmodbpf-postinstall.sh;hb=HEAD - postinstall script of Wireshark installer package
- Other files and folders, which covers the Shared folder in the Users folder and folders you created at the top level of a drive
- Computer & Network Settings

Setup Assistant (from clean install) or via `/Applications/Utilities/Migration Assistant.app` (could be problematic when migrate already exist accounts).

but doesn't migrate:

- `/etc/hosts`
- Time Machine configuration (destination and exclude list)
- hostname (Settings > Share)
- ByHost preferences

- `/Library/Logs/SystemMigration.log` or `/private/var/log/system.log` (sender MigrateTool)
- [macOS Sierra: Transfer your info from a computer or storage device](https://support.apple.com/kb/PH25651)
- [How to move data to your new Mac using Mountain Lion and earlier - Apple Support](https://support.apple.com/en-us/HT204320)
- [Restore from a Time Machine backup](#restore-from-a-time-machine-backup)
- [Install macOS](#install-macos)
- [Migration Assistant](#migration-assistant)

### Cleanup from previous upgrades

Use the Recovery System (restart and hold `CMD+R`)

Generate a list of files:

	LC_ALL=en_US.UTF-8 sudo find "/Volumes/Macintosh HD" -exec ls -Ald {} \; > tree.txt

Compare 2 version (before and after clean upgrade):

	comm -13 <(cat tree-pristine.txt | grep -o '/Volumes/.*' - | sort) <(cat tree-dirty.txt | grep -o '/Volumes/.*' - | sort)

After OS update some config files are replaced, where then previous one are kept and renamed as *~orig or *~previous

Note `dirname` command is not available in Recovery System

Before remove, backup unwanted files:

	mkdir -p "/Volumes/XX" && mv "/Volumes/XX/YY" "/Volumes/XX/ZZ/Volumes/XX/YY"

Files can be removed in 10.13.6:

	# Not sure
	/Volumes/Macintosh HD/usr/share/current-os.sdk
	/Volumes/Macintosh HD/usr/libexec/cups/backend/cups-pdf

	find "/Volumes/Macintosh HD/" \( -name "*~orig" -o -name "*~previous" \) -exec rm -rf {} \;

	/Volumes/Macintosh HD/usr/local/sbin/mount_fusefs_txantfs
	/Volumes/Macintosh HD/usr/local/sbin/newfs_fusefs_txantfs

	# For pre SIP with XQuartz and MacFUSE (or remains) installed:
	/Volumes/Macintosh HD/usr/X11
	/Volumes/Macintosh HD/usr/X11R6
	/Volumes/Macintosh HD/usr/bin/X
	/Volumes/Macintosh HD/usr/bin/Xephyr
	/Volumes/Macintosh HD/usr/bin/Xfake
	/Volumes/Macintosh HD/usr/bin/Xnest
	/Volumes/Macintosh HD/usr/bin/Xorg
	/Volumes/Macintosh HD/usr/bin/Xquartz
	/Volumes/Macintosh HD/usr/bin/Xvfb
	/Volumes/Macintosh HD/usr/bin/appres
	/Volumes/Macintosh HD/usr/bin/atobm
	/Volumes/Macintosh HD/usr/bin/bdftopcf
	/Volumes/Macintosh HD/usr/bin/bdftruncate
	/Volumes/Macintosh HD/usr/bin/bitmap
	/Volumes/Macintosh HD/usr/bin/bmtoa
	/Volumes/Macintosh HD/usr/bin/cups-calibrate
	/Volumes/Macintosh HD/usr/bin/cvt
	/Volumes/Macintosh HD/usr/bin/cxpm
	/Volumes/Macintosh HD/usr/bin/editres
	/Volumes/Macintosh HD/usr/bin/escputil
	/Volumes/Macintosh HD/usr/bin/fc-cache
	/Volumes/Macintosh HD/usr/bin/fc-cat
	/Volumes/Macintosh HD/usr/bin/fc-list
	/Volumes/Macintosh HD/usr/bin/fc-match
	/Volumes/Macintosh HD/usr/bin/fc-pattern
	/Volumes/Macintosh HD/usr/bin/fc-query
	/Volumes/Macintosh HD/usr/bin/fc-scan
	/Volumes/Macintosh HD/usr/bin/fc-validate
	/Volumes/Macintosh HD/usr/bin/font_cache
	/Volumes/Macintosh HD/usr/bin/fonttosfnt
	/Volumes/Macintosh HD/usr/bin/freetype-config
	/Volumes/Macintosh HD/usr/bin/fslsfonts
	/Volumes/Macintosh HD/usr/bin/fstobdf
	/Volumes/Macintosh HD/usr/bin/gccmakedep
	/Volumes/Macintosh HD/usr/bin/glxgears
	/Volumes/Macintosh HD/usr/bin/glxinfo
	/Volumes/Macintosh HD/usr/bin/gtf
	/Volumes/Macintosh HD/usr/bin/iceauth
	/Volumes/Macintosh HD/usr/bin/ico
	/Volumes/Macintosh HD/usr/bin/koi8rxterm
	/Volumes/Macintosh HD/usr/bin/libpng-config
	/Volumes/Macintosh HD/usr/bin/libpng16-config
	/Volumes/Macintosh HD/usr/bin/listres
	/Volumes/Macintosh HD/usr/bin/lndir
	/Volumes/Macintosh HD/usr/bin/luit
	/Volumes/Macintosh HD/usr/bin/makedepend
	/Volumes/Macintosh HD/usr/bin/mkfontdir
	/Volumes/Macintosh HD/usr/bin/mkfontscale
	/Volumes/Macintosh HD/usr/bin/oclock
	/Volumes/Macintosh HD/usr/bin/png-fix-itxt
	/Volumes/Macintosh HD/usr/bin/pngfix
	/Volumes/Macintosh HD/usr/bin/quartz-wm
	/Volumes/Macintosh HD/usr/bin/resize
	/Volumes/Macintosh HD/usr/bin/rvictl
	/Volumes/Macintosh HD/usr/bin/sessreg
	/Volumes/Macintosh HD/usr/bin/setxkbmap
	/Volumes/Macintosh HD/usr/bin/showfont
	/Volumes/Macintosh HD/usr/bin/showrgb
	/Volumes/Macintosh HD/usr/bin/smproxy
	/Volumes/Macintosh HD/usr/bin/startx
	/Volumes/Macintosh HD/usr/bin/sxpm
	/Volumes/Macintosh HD/usr/bin/twm
	/Volumes/Macintosh HD/usr/bin/ucs2any
	/Volumes/Macintosh HD/usr/bin/uxterm
	/Volumes/Macintosh HD/usr/bin/viewres
	/Volumes/Macintosh HD/usr/bin/x11perf
	/Volumes/Macintosh HD/usr/bin/x11perfcomp
	/Volumes/Macintosh HD/usr/bin/xauth
	/Volumes/Macintosh HD/usr/bin/xbacklight
	/Volumes/Macintosh HD/usr/bin/xcalc
	/Volumes/Macintosh HD/usr/bin/xclipboard
	/Volumes/Macintosh HD/usr/bin/xclock
	/Volumes/Macintosh HD/usr/bin/xcmsdb
	/Volumes/Macintosh HD/usr/bin/xcompmgr
	/Volumes/Macintosh HD/usr/bin/xconsole
	/Volumes/Macintosh HD/usr/bin/xcursorgen
	/Volumes/Macintosh HD/usr/bin/xcutsel
	/Volumes/Macintosh HD/usr/bin/xditview
	/Volumes/Macintosh HD/usr/bin/xdm
	/Volumes/Macintosh HD/usr/bin/xdmshell
	/Volumes/Macintosh HD/usr/bin/xdpr
	/Volumes/Macintosh HD/usr/bin/xdpyinfo
	/Volumes/Macintosh HD/usr/bin/xedit
	/Volumes/Macintosh HD/usr/bin/xev
	/Volumes/Macintosh HD/usr/bin/xeyes
	/Volumes/Macintosh HD/usr/bin/xfd
	/Volumes/Macintosh HD/usr/bin/xfindproxy
	/Volumes/Macintosh HD/usr/bin/xfontsel
	/Volumes/Macintosh HD/usr/bin/xfs
	/Volumes/Macintosh HD/usr/bin/xfsinfo
	/Volumes/Macintosh HD/usr/bin/xgamma
	/Volumes/Macintosh HD/usr/bin/xgc
	/Volumes/Macintosh HD/usr/bin/xhost
	/Volumes/Macintosh HD/usr/bin/xinit
	/Volumes/Macintosh HD/usr/bin/xinput
	/Volumes/Macintosh HD/usr/bin/xkbbell
	/Volumes/Macintosh HD/usr/bin/xkbcomp
	/Volumes/Macintosh HD/usr/bin/xkbevd
	/Volumes/Macintosh HD/usr/bin/xkbprint
	/Volumes/Macintosh HD/usr/bin/xkbvleds
	/Volumes/Macintosh HD/usr/bin/xkbwatch
	/Volumes/Macintosh HD/usr/bin/xkeystone
	/Volumes/Macintosh HD/usr/bin/xkill
	/Volumes/Macintosh HD/usr/bin/xload
	/Volumes/Macintosh HD/usr/bin/xlogo
	/Volumes/Macintosh HD/usr/bin/xlsatoms
	/Volumes/Macintosh HD/usr/bin/xlsclients
	/Volumes/Macintosh HD/usr/bin/xlsfonts
	/Volumes/Macintosh HD/usr/bin/xmag
	/Volumes/Macintosh HD/usr/bin/xman
	/Volumes/Macintosh HD/usr/bin/xmessage
	/Volumes/Macintosh HD/usr/bin/xmh
	/Volumes/Macintosh HD/usr/bin/xmodmap
	/Volumes/Macintosh HD/usr/bin/xmore
	/Volumes/Macintosh HD/usr/bin/xpr
	/Volumes/Macintosh HD/usr/bin/xprop
	/Volumes/Macintosh HD/usr/bin/xrandr
	/Volumes/Macintosh HD/usr/bin/xrdb
	/Volumes/Macintosh HD/usr/bin/xrefresh
	/Volumes/Macintosh HD/usr/bin/xscope
	/Volumes/Macintosh HD/usr/bin/xset
	/Volumes/Macintosh HD/usr/bin/xsetmode
	/Volumes/Macintosh HD/usr/bin/xsetpointer
	/Volumes/Macintosh HD/usr/bin/xsetroot
	/Volumes/Macintosh HD/usr/bin/xsm
	/Volumes/Macintosh HD/usr/bin/xstdcmap
	/Volumes/Macintosh HD/usr/bin/xterm
	/Volumes/Macintosh HD/usr/bin/xvinfo
	/Volumes/Macintosh HD/usr/bin/xwd
	/Volumes/Macintosh HD/usr/bin/xwininfo
	/Volumes/Macintosh HD/usr/bin/xwud
	/Volumes/Macintosh HD/usr/include
	/Volumes/Macintosh HD/usr/lib/X11
	/Volumes/Macintosh HD/usr/lib/bundle1.o
	/Volumes/Macintosh HD/usr/lib/crt1.10.5.o
	/Volumes/Macintosh HD/usr/lib/crt1.10.6.o
	/Volumes/Macintosh HD/usr/lib/crt1.o
	/Volumes/Macintosh HD/usr/lib/dri
	/Volumes/Macintosh HD/usr/lib/dylib1.10.5.o
	/Volumes/Macintosh HD/usr/lib/dylib1.o
	/Volumes/Macintosh HD/usr/lib/flat_namespace
	/Volumes/Macintosh HD/usr/lib/gcrt1.o
	/Volumes/Macintosh HD/usr/lib/lazydylib1.o
	/Volumes/Macintosh HD/usr/lib/libATCommandStudio.a
	/Volumes/Macintosh HD/usr/lib/libAppleWM.7.dylib
	/Volumes/Macintosh HD/usr/lib/libAppleWM.dylib
	/Volumes/Macintosh HD/usr/lib/libFS.6.dylib
	/Volumes/Macintosh HD/usr/lib/libFS.dylib
	/Volumes/Macintosh HD/usr/lib/libGL.1.dylib
	/Volumes/Macintosh HD/usr/lib/libGL.dylib
	/Volumes/Macintosh HD/usr/lib/libGLESv1_CM.1.dylib
	/Volumes/Macintosh HD/usr/lib/libGLESv1_CM.dylib
	/Volumes/Macintosh HD/usr/lib/libGLESv2.2.dylib
	/Volumes/Macintosh HD/usr/lib/libGLESv2.dylib
	/Volumes/Macintosh HD/usr/lib/libGLU.1.dylib
	/Volumes/Macintosh HD/usr/lib/libGLU.dylib
	/Volumes/Macintosh HD/usr/lib/libICE.6.dylib
	/Volumes/Macintosh HD/usr/lib/libICE.dylib
	/Volumes/Macintosh HD/usr/lib/libOSMesa.8.dylib
	/Volumes/Macintosh HD/usr/lib/libOSMesa.dylib
	/Volumes/Macintosh HD/usr/lib/libQMIParser.a
	/Volumes/Macintosh HD/usr/lib/libSM.6.dylib
	/Volumes/Macintosh HD/usr/lib/libSM.dylib
	/Volumes/Macintosh HD/usr/lib/libX11-xcb.1.dylib
	/Volumes/Macintosh HD/usr/lib/libX11-xcb.dylib
	/Volumes/Macintosh HD/usr/lib/libX11.6.dylib
	/Volumes/Macintosh HD/usr/lib/libX11.dylib
	/Volumes/Macintosh HD/usr/lib/libXRes.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXRes.dylib
	/Volumes/Macintosh HD/usr/lib/libXTrap.6.dylib
	/Volumes/Macintosh HD/usr/lib/libXTrap.dylib
	/Volumes/Macintosh HD/usr/lib/libXau.6.dylib
	/Volumes/Macintosh HD/usr/lib/libXau.dylib
	/Volumes/Macintosh HD/usr/lib/libXaw.6.dylib
	/Volumes/Macintosh HD/usr/lib/libXaw.7.dylib
	/Volumes/Macintosh HD/usr/lib/libXaw.8.dylib
	/Volumes/Macintosh HD/usr/lib/libXaw.dylib
	/Volumes/Macintosh HD/usr/lib/libXaw3d.8.dylib
	/Volumes/Macintosh HD/usr/lib/libXaw3d.dylib
	/Volumes/Macintosh HD/usr/lib/libXaw6.6.dylib
	/Volumes/Macintosh HD/usr/lib/libXaw6.dylib
	/Volumes/Macintosh HD/usr/lib/libXaw7.7.dylib
	/Volumes/Macintosh HD/usr/lib/libXaw7.dylib
	/Volumes/Macintosh HD/usr/lib/libXaw8.8.dylib
	/Volumes/Macintosh HD/usr/lib/libXaw8.dylib
	/Volumes/Macintosh HD/usr/lib/libXcomposite.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXcomposite.dylib
	/Volumes/Macintosh HD/usr/lib/libXcursor.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXcursor.dylib
	/Volumes/Macintosh HD/usr/lib/libXdamage.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXdamage.dylib
	/Volumes/Macintosh HD/usr/lib/libXdmcp.6.dylib
	/Volumes/Macintosh HD/usr/lib/libXdmcp.dylib
	/Volumes/Macintosh HD/usr/lib/libXevie.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXevie.dylib
	/Volumes/Macintosh HD/usr/lib/libXext.6.dylib
	/Volumes/Macintosh HD/usr/lib/libXext.dylib
	/Volumes/Macintosh HD/usr/lib/libXfixes.3.dylib
	/Volumes/Macintosh HD/usr/lib/libXfixes.dylib
	/Volumes/Macintosh HD/usr/lib/libXfont.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXfont.dylib
	/Volumes/Macintosh HD/usr/lib/libXfont2.2.dylib
	/Volumes/Macintosh HD/usr/lib/libXfont2.dylib
	/Volumes/Macintosh HD/usr/lib/libXfontcache.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXfontcache.dylib
	/Volumes/Macintosh HD/usr/lib/libXft.2.dylib
	/Volumes/Macintosh HD/usr/lib/libXft.dylib
	/Volumes/Macintosh HD/usr/lib/libXi.6.dylib
	/Volumes/Macintosh HD/usr/lib/libXi.dylib
	/Volumes/Macintosh HD/usr/lib/libXinerama.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXinerama.dylib
	/Volumes/Macintosh HD/usr/lib/libXmu.6.dylib
	/Volumes/Macintosh HD/usr/lib/libXmu.dylib
	/Volumes/Macintosh HD/usr/lib/libXmuu.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXmuu.dylib
	/Volumes/Macintosh HD/usr/lib/libXp.6.dylib
	/Volumes/Macintosh HD/usr/lib/libXp.dylib
	/Volumes/Macintosh HD/usr/lib/libXpm.4.dylib
	/Volumes/Macintosh HD/usr/lib/libXpm.dylib
	/Volumes/Macintosh HD/usr/lib/libXpresent.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXpresent.dylib
	/Volumes/Macintosh HD/usr/lib/libXrandr.2.dylib
	/Volumes/Macintosh HD/usr/lib/libXrandr.dylib
	/Volumes/Macintosh HD/usr/lib/libXrender.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXrender.dylib
	/Volumes/Macintosh HD/usr/lib/libXss.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXss.dylib
	/Volumes/Macintosh HD/usr/lib/libXt.6.dylib
	/Volumes/Macintosh HD/usr/lib/libXt.7.dylib
	/Volumes/Macintosh HD/usr/lib/libXt.dylib
	/Volumes/Macintosh HD/usr/lib/libXtst.6.dylib
	/Volumes/Macintosh HD/usr/lib/libXtst.dylib
	/Volumes/Macintosh HD/usr/lib/libXv.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXv.dylib
	/Volumes/Macintosh HD/usr/lib/libXvMC.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXvMC.dylib
	/Volumes/Macintosh HD/usr/lib/libXvMCW.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXvMCW.dylib
	/Volumes/Macintosh HD/usr/lib/libXxf86misc.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXxf86misc.dylib
	/Volumes/Macintosh HD/usr/lib/libXxf86vm.1.dylib
	/Volumes/Macintosh HD/usr/lib/libXxf86vm.dylib
	/Volumes/Macintosh HD/usr/lib/libcairo-script-interpreter.2.dylib
	/Volumes/Macintosh HD/usr/lib/libcairo-script-interpreter.dylib
	/Volumes/Macintosh HD/usr/lib/libcairo.2.dylib
	/Volumes/Macintosh HD/usr/lib/libcairo.dylib
	/Volumes/Macintosh HD/usr/lib/libdmx.1.dylib
	/Volumes/Macintosh HD/usr/lib/libdmx.dylib
	/Volumes/Macintosh HD/usr/lib/libfontconfig.1.dylib
	/Volumes/Macintosh HD/usr/lib/libfontconfig.dylib
	/Volumes/Macintosh HD/usr/lib/libfontenc.1.dylib
	/Volumes/Macintosh HD/usr/lib/libfontenc.dylib
	/Volumes/Macintosh HD/usr/lib/libfreetype.6.dylib
	/Volumes/Macintosh HD/usr/lib/libfreetype.dylib
	/Volumes/Macintosh HD/usr/lib/libgcc_s.10.4.dylib
	/Volumes/Macintosh HD/usr/lib/libgcc_s.10.5.dylib
	/Volumes/Macintosh HD/usr/lib/libglapi.0.dylib
	/Volumes/Macintosh HD/usr/lib/libglapi.dylib
	/Volumes/Macintosh HD/usr/lib/libglut.3.dylib
	/Volumes/Macintosh HD/usr/lib/libglut.dylib
	/Volumes/Macintosh HD/usr/lib/libgutenprint.2.dylib
	/Volumes/Macintosh HD/usr/lib/libkmod.a
	/Volumes/Macintosh HD/usr/lib/libkmodc++.a
	/Volumes/Macintosh HD/usr/lib/libl.a
	/Volumes/Macintosh HD/usr/lib/libpixman-1.0.dylib
	/Volumes/Macintosh HD/usr/lib/libpixman-1.dylib
	/Volumes/Macintosh HD/usr/lib/libpkstart.a
	/Volumes/Macintosh HD/usr/lib/libpng.3.dylib
	/Volumes/Macintosh HD/usr/lib/libpng.dylib
	/Volumes/Macintosh HD/usr/lib/libpng12.0.dylib
	/Volumes/Macintosh HD/usr/lib/libpng14.14.dylib
	/Volumes/Macintosh HD/usr/lib/libpng15.15.dylib
	/Volumes/Macintosh HD/usr/lib/libpng16.16.dylib
	/Volumes/Macintosh HD/usr/lib/libpng16.dylib
	/Volumes/Macintosh HD/usr/lib/libtclstub8.5.a
	/Volumes/Macintosh HD/usr/lib/libtkstub8.5.a
	/Volumes/Macintosh HD/usr/lib/libxcb-atom.1.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-aux.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-composite.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-composite.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-cursor.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-cursor.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-damage.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-damage.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-dpms.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-dpms.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-dri2.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-dri2.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-dri3.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-dri3.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-errors.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-errors.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-event.1.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-ewmh.2.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-ewmh.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-glx.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-glx.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-icccm.4.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-icccm.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-image.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-image.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-keysyms.1.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-keysyms.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-present.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-present.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-randr.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-randr.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-record.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-record.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-render-util.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-render-util.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-render.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-render.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-res.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-res.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-screensaver.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-screensaver.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-shape.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-shape.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-shm.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-shm.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-sync.1.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-sync.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-util.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-util.1.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-util.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-xf86dri.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-xf86dri.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-xfixes.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-xfixes.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-xinerama.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-xinerama.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-xkb.1.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-xkb.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-xtest.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-xtest.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-xv.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-xv.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-xvmc.0.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb-xvmc.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb.1.dylib
	/Volumes/Macintosh HD/usr/lib/libxcb.dylib
	/Volumes/Macintosh HD/usr/lib/libxkbfile.1.dylib
	/Volumes/Macintosh HD/usr/lib/libxkbfile.dylib
	/Volumes/Macintosh HD/usr/lib/libxkbui.1.dylib
	/Volumes/Macintosh HD/usr/lib/libxkbui.dylib
	/Volumes/Macintosh HD/usr/lib/libxshmfence.1.dylib
	/Volumes/Macintosh HD/usr/lib/libxshmfence.dylib
	/Volumes/Macintosh HD/usr/lib/liby.a
	/Volumes/Macintosh HD/usr/lib/pkgconfig/applewm.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/applewmproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/bigreqsproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/cairo-fc.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/cairo-ft.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/cairo-pdf.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/cairo-png.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/cairo-ps.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/cairo-script.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/cairo-svg.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/cairo-tee.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/cairo-xcb-shm.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/cairo-xcb.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/cairo-xlib-xcb.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/cairo-xlib-xrender.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/cairo-xlib.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/cairo-xml.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/cairo.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/compositeproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/damageproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/dmx.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/dmxproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/dri.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/dri2proto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/dri3proto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/evieproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/fixesproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/fontcacheproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/fontconfig.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/fontenc.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/fontsproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/fontutil.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/freetype2.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/gl.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/glesv1_cm.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/glesv2.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/glproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/glu.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/ice.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/inputproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/kbproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/libfs.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/libpng.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/libpng16.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/osmesa.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/pixman-1.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/presentproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/printproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/pthread-stubs.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/randrproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/recordproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/renderproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/resourceproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/scrnsaverproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/sm.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/trapproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/videoproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/x11-xcb.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/x11.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xau.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xaw3d.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xaw6.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xaw7.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-atom.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-aux.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-composite.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-cursor.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-damage.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-dpms.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-dri2.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-dri3.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-errors.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-event.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-ewmh.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-glx.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-icccm.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-image.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-keysyms.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-present.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-proto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-randr.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-record.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-render.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-renderutil.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-res.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-screensaver.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-shape.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-shm.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-sync.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-util.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-xf86dri.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-xfixes.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-xinerama.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-xkb.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-xtest.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-xv.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb-xvmc.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcb.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcmiscproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcomposite.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xcursor.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xdamage.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xdmcp.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xevie.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xext.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xextproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xf86bigfontproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xf86dgaproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xf86driproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xf86miscproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xf86rushproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xf86vidmodeproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xfixes.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xfont.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xfont2.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xfontcache.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xft.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xi.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xinerama.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xineramaproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xkbcomp.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xkbfile.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xkbui.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xmu.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xmuu.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xorg-server.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xp.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xpm.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xpresent.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xproxymngproto.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xpyb.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xrandr.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xrender.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xres.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xscrnsaver.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xshmfence.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xt.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xtrap.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xtst.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xv.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xvmc.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xxf86misc.pc
	/Volumes/Macintosh HD/usr/lib/pkgconfig/xxf86vm.pc
	/Volumes/Macintosh HD/usr/lib/python2.6
	/Volumes/Macintosh HD/usr/lib/xorg
	/Volumes/Macintosh HD/usr/libexec/cups/filter/commandtocanon
	/Volumes/Macintosh HD/usr/libexec/cups/filter/commandtoepson
	/Volumes/Macintosh HD/usr/libexec/cups/filter/rastertogutenprint.5.2
	/Volumes/Macintosh HD/usr/libexec/cups/filter/thnucups
	/Volumes/Macintosh HD/usr/libexec/launchd_startx
	/Volumes/Macintosh HD/usr/libexec/privileged_startx
	/Volumes/Macintosh HD/usr/libexec/rpmuxd
	/Volumes/Macintosh HD/usr/local/bin
	/Volumes/Macintosh HD/usr/local/doc
	/Volumes/Macintosh HD/usr/local/etc
	/Volumes/Macintosh HD/usr/local/include
	/Volumes/Macintosh HD/usr/local/lib
	/Volumes/Macintosh HD/usr/local/man
	/Volumes/Macintosh HD/usr/local/remotedesktop
	/Volumes/Macintosh HD/usr/local/sbin
	/Volumes/Macintosh HD/usr/local/share
	/Volumes/Macintosh HD/usr/sbin/cups-genppd.5.2
	/Volumes/Macintosh HD/usr/sbin/cups-genppdupdate
	/Volumes/Macintosh HD/usr/share/aclocal
	/Volumes/Macintosh HD/usr/share/doc/dri2proto
	/Volumes/Macintosh HD/usr/share/doc/randrproto
	/Volumes/Macintosh HD/usr/share/doc/xorg-docs
	/Volumes/Macintosh HD/usr/share/gtk-doc
	/Volumes/Macintosh HD/usr/share/man/man1/Xephyr.1
	/Volumes/Macintosh HD/usr/share/man/man1/Xmark.1
	/Volumes/Macintosh HD/usr/share/man/man1/Xnest.1
	/Volumes/Macintosh HD/usr/share/man/man1/Xorg.1
	/Volumes/Macintosh HD/usr/share/man/man1/Xquartz.1
	/Volumes/Macintosh HD/usr/share/man/man1/Xserver.1
	/Volumes/Macintosh HD/usr/share/man/man1/Xvfb.1
	/Volumes/Macintosh HD/usr/share/man/man1/appres.1
	/Volumes/Macintosh HD/usr/share/man/man1/atobm.1
	/Volumes/Macintosh HD/usr/share/man/man1/bdftopcf.1
	/Volumes/Macintosh HD/usr/share/man/man1/bdftruncate.1
	/Volumes/Macintosh HD/usr/share/man/man1/bitmap.1
	/Volumes/Macintosh HD/usr/share/man/man1/bmtoa.1
	/Volumes/Macintosh HD/usr/share/man/man1/cvt.1
	/Volumes/Macintosh HD/usr/share/man/man1/cxpm.1
	/Volumes/Macintosh HD/usr/share/man/man1/editres.1
	/Volumes/Macintosh HD/usr/share/man/man1/fc-cache.1
	/Volumes/Macintosh HD/usr/share/man/man1/fc-cat.1
	/Volumes/Macintosh HD/usr/share/man/man1/fc-list.1
	/Volumes/Macintosh HD/usr/share/man/man1/fc-match.1
	/Volumes/Macintosh HD/usr/share/man/man1/fc-pattern.1
	/Volumes/Macintosh HD/usr/share/man/man1/fc-query.1
	/Volumes/Macintosh HD/usr/share/man/man1/fc-scan.1
	/Volumes/Macintosh HD/usr/share/man/man1/fc-validate.1
	/Volumes/Macintosh HD/usr/share/man/man1/fonttosfnt.1
	/Volumes/Macintosh HD/usr/share/man/man1/freetype-config.1
	/Volumes/Macintosh HD/usr/share/man/man1/fslsfonts.1
	/Volumes/Macintosh HD/usr/share/man/man1/fstobdf.1
	/Volumes/Macintosh HD/usr/share/man/man1/gccmakedep.1
	/Volumes/Macintosh HD/usr/share/man/man1/gtf.1
	/Volumes/Macintosh HD/usr/share/man/man1/iceauth.1
	/Volumes/Macintosh HD/usr/share/man/man1/ico.1
	/Volumes/Macintosh HD/usr/share/man/man1/koi8rxterm.1
	/Volumes/Macintosh HD/usr/share/man/man1/listres.1
	/Volumes/Macintosh HD/usr/share/man/man1/lndir.1
	/Volumes/Macintosh HD/usr/share/man/man1/luit.1
	/Volumes/Macintosh HD/usr/share/man/man1/makedepend.1
	/Volumes/Macintosh HD/usr/share/man/man1/mkfontdir.1
	/Volumes/Macintosh HD/usr/share/man/man1/mkfontscale.1
	/Volumes/Macintosh HD/usr/share/man/man1/oclock.1
	/Volumes/Macintosh HD/usr/share/man/man1/quartz-wm.1
	/Volumes/Macintosh HD/usr/share/man/man1/resize.1
	/Volumes/Macintosh HD/usr/share/man/man1/sessreg.1
	/Volumes/Macintosh HD/usr/share/man/man1/setxkbmap.1
	/Volumes/Macintosh HD/usr/share/man/man1/showfont.1
	/Volumes/Macintosh HD/usr/share/man/man1/showrgb.1
	/Volumes/Macintosh HD/usr/share/man/man1/smproxy.1
	/Volumes/Macintosh HD/usr/share/man/man1/startx.1
	/Volumes/Macintosh HD/usr/share/man/man1/sxpm.1
	/Volumes/Macintosh HD/usr/share/man/man1/twm.1
	/Volumes/Macintosh HD/usr/share/man/man1/ucs2any.1
	/Volumes/Macintosh HD/usr/share/man/man1/uxterm.1
	/Volumes/Macintosh HD/usr/share/man/man1/viewres.1
	/Volumes/Macintosh HD/usr/share/man/man1/x11perf.1
	/Volumes/Macintosh HD/usr/share/man/man1/x11perfcomp.1
	/Volumes/Macintosh HD/usr/share/man/man1/xauth.1
	/Volumes/Macintosh HD/usr/share/man/man1/xbacklight.1
	/Volumes/Macintosh HD/usr/share/man/man1/xcalc.1
	/Volumes/Macintosh HD/usr/share/man/man1/xclipboard.1
	/Volumes/Macintosh HD/usr/share/man/man1/xclock.1
	/Volumes/Macintosh HD/usr/share/man/man1/xcmsdb.1
	/Volumes/Macintosh HD/usr/share/man/man1/xcompmgr.1
	/Volumes/Macintosh HD/usr/share/man/man1/xconsole.1
	/Volumes/Macintosh HD/usr/share/man/man1/xcursorgen.1
	/Volumes/Macintosh HD/usr/share/man/man1/xcutsel.1
	/Volumes/Macintosh HD/usr/share/man/man1/xditview.1
	/Volumes/Macintosh HD/usr/share/man/man1/xdm.1
	/Volumes/Macintosh HD/usr/share/man/man1/xdpr.1
	/Volumes/Macintosh HD/usr/share/man/man1/xdpyinfo.1
	/Volumes/Macintosh HD/usr/share/man/man1/xedit.1
	/Volumes/Macintosh HD/usr/share/man/man1/xev.1
	/Volumes/Macintosh HD/usr/share/man/man1/xeyes.1
	/Volumes/Macintosh HD/usr/share/man/man1/xfd.1
	/Volumes/Macintosh HD/usr/share/man/man1/xfindproxy.1
	/Volumes/Macintosh HD/usr/share/man/man1/xfontsel.1
	/Volumes/Macintosh HD/usr/share/man/man1/xfs.1
	/Volumes/Macintosh HD/usr/share/man/man1/xfsinfo.1
	/Volumes/Macintosh HD/usr/share/man/man1/xgamma.1
	/Volumes/Macintosh HD/usr/share/man/man1/xgc.1
	/Volumes/Macintosh HD/usr/share/man/man1/xhost.1
	/Volumes/Macintosh HD/usr/share/man/man1/xinit.1
	/Volumes/Macintosh HD/usr/share/man/man1/xinput.1
	/Volumes/Macintosh HD/usr/share/man/man1/xkbbell.1
	/Volumes/Macintosh HD/usr/share/man/man1/xkbcomp.1
	/Volumes/Macintosh HD/usr/share/man/man1/xkbevd.1
	/Volumes/Macintosh HD/usr/share/man/man1/xkbprint.1
	/Volumes/Macintosh HD/usr/share/man/man1/xkbvleds.1
	/Volumes/Macintosh HD/usr/share/man/man1/xkbwatch.1
	/Volumes/Macintosh HD/usr/share/man/man1/xkill.1
	/Volumes/Macintosh HD/usr/share/man/man1/xload.1
	/Volumes/Macintosh HD/usr/share/man/man1/xlogo.1
	/Volumes/Macintosh HD/usr/share/man/man1/xlsatoms.1
	/Volumes/Macintosh HD/usr/share/man/man1/xlsclients.1
	/Volumes/Macintosh HD/usr/share/man/man1/xlsfonts.1
	/Volumes/Macintosh HD/usr/share/man/man1/xmag.1
	/Volumes/Macintosh HD/usr/share/man/man1/xman.1
	/Volumes/Macintosh HD/usr/share/man/man1/xmessage.1
	/Volumes/Macintosh HD/usr/share/man/man1/xmh.1
	/Volumes/Macintosh HD/usr/share/man/man1/xmodmap.1
	/Volumes/Macintosh HD/usr/share/man/man1/xmore.1
	/Volumes/Macintosh HD/usr/share/man/man1/xpr.1
	/Volumes/Macintosh HD/usr/share/man/man1/xprop.1
	/Volumes/Macintosh HD/usr/share/man/man1/xrandr.1
	/Volumes/Macintosh HD/usr/share/man/man1/xrdb.1
	/Volumes/Macintosh HD/usr/share/man/man1/xrefresh.1
	/Volumes/Macintosh HD/usr/share/man/man1/xscope.1
	/Volumes/Macintosh HD/usr/share/man/man1/xset.1
	/Volumes/Macintosh HD/usr/share/man/man1/xsetmode.1
	/Volumes/Macintosh HD/usr/share/man/man1/xsetpointer.1
	/Volumes/Macintosh HD/usr/share/man/man1/xsetroot.1
	/Volumes/Macintosh HD/usr/share/man/man1/xsm.1
	/Volumes/Macintosh HD/usr/share/man/man1/xstdcmap.1
	/Volumes/Macintosh HD/usr/share/man/man1/xterm.1
	/Volumes/Macintosh HD/usr/share/man/man1/xvinfo.1
	/Volumes/Macintosh HD/usr/share/man/man1/xwd.1
	/Volumes/Macintosh HD/usr/share/man/man1/xwininfo.1
	/Volumes/Macintosh HD/usr/share/man/man1/xwud.1
	/Volumes/Macintosh HD/usr/share/man/man2
	/Volumes/Macintosh HD/usr/share/man/man3
	/Volumes/Macintosh HD/usr/share/man/man4/exa.4
	/Volumes/Macintosh HD/usr/share/man/man4/fbdevhw.4
	/Volumes/Macintosh HD/usr/share/man/man4/void.4
	/Volumes/Macintosh HD/usr/share/man/man5/Compose.5
	/Volumes/Macintosh HD/usr/share/man/man5/XCompose.5
	/Volumes/Macintosh HD/usr/share/man/man5/fonts-conf.5
	/Volumes/Macintosh HD/usr/share/man/man5/png.5
	/Volumes/Macintosh HD/usr/share/man/man5/xorg.conf.5
	/Volumes/Macintosh HD/usr/share/man/man5/xorg.conf.d.5
	/Volumes/Macintosh HD/usr/share/man/man7/Consortium.7
	/Volumes/Macintosh HD/usr/share/man/man7/Standards.7
	/Volumes/Macintosh HD/usr/share/man/man7/X.7
	/Volumes/Macintosh HD/usr/share/man/man7/XOrgFoundation.7
	/Volumes/Macintosh HD/usr/share/man/man7/XProjectTeam.7
	/Volumes/Macintosh HD/usr/share/man/man7/Xprint.7
	/Volumes/Macintosh HD/usr/share/man/man7/Xsecurity.7
	/Volumes/Macintosh HD/usr/share/pixmaps
	/Volumes/Macintosh HD/usr/share/pkgconfig
	/Volumes/Macintosh HD/usr/share/sgml
	/Volumes/Macintosh HD/usr/share/util-macros
	/Volumes/Macintosh HD/usr/share/xml

### Reset Setup Assistant

Integrate features of [Migration Assistant](#migration-assistant).

Remove `/var/db/.AppleSetupDone`:

1. reboot
2. hold `command + s`
3. in Terminal:

		mount -uw /
		rm /var/db/.AppleSetupDone
		shutdown -h now

or:

1. reboot
3. hold `command + r`
3. in Terminal ("Mackintosh HD" is the default name of the main disk, depends what has been defined when macOS was installed):

		rm "/Volumes/Mackintosh HD/var/db/.AppleSetupDone"
		shutdown -h now

- [How to Re-Run the OS X Setup Assistant - The Instructional](http://www.theinstructional.com/guides/how-to-re-run-the-os-x-setup-assistant)
- [OSX Tips Setting-up a new Mac from an old one, its Backups, or a PC](http://pondini.org/OSX/Setup.html)

### Boot Camp

- [Start up your Mac in Windows or macOS with Boot Camp - Apple Support](https://support.apple.com/guide/bootcamp-control-panel/bcmp29b8ac66/mac) - hold the Option key
- Windows: Configuration pannel > System & Security > Power management > Choose when the screen close (works only in native, not in a VM)
- Windows: `Compact.exe /CompactOS:always` to compact (`Compact.exe /CompactOS:never` to restore); `powercfg /h /type reduced` to reduce hibernation file size (`powercfg /h /size 100` to restore)
- macOS: Sytem preferences > Startup > Choose the disk you want to use at each startup (you still can use opt key to Start up to [Startup Manager](https://support.apple.com/en-us/HT202796))
- [Launching your Boot Camp partition in VMware Fusion (1014618)](https://kb.vmware.com/s/article/1014618)
- [Enabling Virtualization Support in Boot Camp with rEFInd | Chris Warrick](https://web.archive.org/web/20210724173225/https://chriswarrick.com/blog/2021/01/31/enabling-virtualization-support-in-boot-camp-with-refind/)

Windows boot `INACCESSIBLE_BOOT_DEVICE` error (after Windows Updates):

- [partitioning - Windows BSOD 'Inaccessible boot device' on Bootcamp/Macbook - Super User](https://superuser.com/questions/922752/windows-bsod-inaccessible-boot-device-on-bootcamp-macbook)
- [INACCESSIBLE_BOOT_DEVICE (SOLVED!) Mac Pro 2018 - Twocanoes Forum](https://web.archive.org/web/20181227213520/http://community.twocanoes.com/t/inaccessible-boot-device-solved-mac-pro-2018/2043)
- [You receive error: Stop error code 0x0000007B (INACCESSIBLE_BOOT_DEVICE) after you install Windows Updates](https://support.microsoft.com/en-us/topic/you-receive-error-stop-error-code-0x0000007b-inaccessible-boot-device-after-you-install-windows-updates-7cc844e4-4daf-a71c-cd23-f99b50d53e31)

How to install Windows:

- `/System/Applications/Utilities/Boot Camp Assistant.app`
- How it's work, Boot Camp Assistant automatically create 2 partition:
	1. `OSXRESERVED` (Microsoft Basic Data / ExFAT, ~10GB, contains [WinPE files](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/winpe-intro), plus drivers in `\$WinPEDriver$` and installer in `\Bootcamp`), which will be removed after the install of Windows is complete
	2. `BOOTCAMP` (Microsoft Basic Data) partition where Windows is installed of the size the user gave

	- [Apple Boot Camp No Longer Requires USB Flash Drive to Install Windows in El Capitan – Twocanoes Software](https://web.archive.org/web/20210506205544/https://twocanoes.com/apple-boot-camp-no-longer-requires-usb-flash-drive/)
- [3 Ways to Use Boot Camp - wikiHow](https://web.archive.org/web/20210725114642/https://www.wikihow.com/Use-Boot-Camp)
- [Fix: Please Wait While Boot Camp Assistant is Removing The Partitions it Created](https://web.archive.org/web/20210228114803/https://www.doncaprio.com/fix-please-wait-while-boot-camp-assistant-is-removing-the-partitions-it-created/)
- [Install Windows 10 on your Mac with Boot Camp Assistant - Apple Support](https://support.apple.com/en-us/HT201468)
- [Installing Windows 10 on a Mac without Bootcamp - Fotsies Technology Blog](https://web.archive.org/web/20210725115728/https://fgimian.github.io/blog/2016/03/12/installing-windows-10-on-a-mac-without-bootcamp/)
- Use USB drive to install Windows could not work with recent macbook because the USB3 is used, and Windows 10 (at least) don't support keyboard and pad in same time (which use USB 3 too) (WinPE will load, but couldn't use the keyboard or mouse): [If your keyboard or trackpad stop responding while installing Windows 8 on your Mac - Apple Support](https://support.apple.com/en-us/HT203755)
- [Advanced advice for Stop error 7B, Inaccessible_Boot_Device - Windows Client Management | Microsoft Docs](https://docs.microsoft.com/en-us/windows/client-management/troubleshoot-inaccessible-boot-device)
- [Windows Recovery Environment (Windows RE) | Microsoft Docs](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)

Drivers:

- open Boot Camp Assistant > Action (menu) > Download Windows Support Software
- [Download and install Windows support software on your Mac - Apple Support](https://support.apple.com/en-us/HT204923)
- [Apple - Support - Downloads](https://support.apple.com/downloads/boot-camp)
- graphics:
	- [Update AMD graphics drivers for Windows in Boot Camp - Apple Support](https://support.apple.com/en-us/HT208908)
	- [Apple Boot Camp Software Graphics Drivers | AMD](https://www.amd.com/en/support/kb/release-notes/apple-boot-camp)
- [timsutton/brigadier: Fetch and install Boot Camp ESDs with ease.](https://github.com/timsutton/brigadier) - `brigadier -m MacBookPro11,1 -o Bootcamp-MBP11.1`
- [Resolving INACCESSIBLE_BOOT_DEVICE Error after restoring Winclone image – Twocanoes Software](https://web.archive.org/web/20210507032351/https://twocanoes.com/knowledge-base/resolving-inaccessible_boot_device-error-after-restoring-winclone-image/)
- if you can start bootcamp OS (ex mounted in a Virtual Machine), install manually (download first: [Download and install Windows support software on your Mac - Apple Support](https://support.apple.com/en-us/HT204923#download)) by right click on each INF files, then "Install" (`*\WindowsSupport\$WinPEDriver$\*\*.inf`) (driver files will be copied in `C:\WINDOWS\inf\*.inf`, `C:\WINDOWS\System32\drivers\*.sys` and `C:\WINDOWS\System32\DriverStore\FileRepository\*\*.*`)
- `D:\$WinPEDriver$` [Limitations of $WinPeDriver$ - Windows Client | Microsoft Docs](https://docs.microsoft.com/en-us/troubleshoot/windows-client/deployment/limitations-dollar-sign-winpedriver-dollar-sign)
- inject in [WIM images](https://en.wikipedia.org/wiki/Windows_Imaging_Format) `D:\sources\boot.wim` and `D:\sources\install.wim`: [Inject Drivers into a Winclone Image – Twocanoes Software](https://web.archive.org/web/20210410143206/https://twocanoes.com/knowledge-base/inject-drivers-into-a-winclone-image/). See also [Create a Windows 10 Bootable USB Flash Drive on a Mac – Twocanoes Software](https://web.archive.org/web/20210506152206/https://twocanoes.com/create-a-windows-10-bootable-usb-flash-drive-on-a-mac/)
- inject product key by create a file `D:\sources\ID.txt` that contains:
	```ini
	[PID]
	Value=XXXXX-XXXXX-XXXXX-XXXXX-XXXXX
	```

Partitions:

- [Create a new partition after Bootcamp - Ask Different](https://apple.stackexchange.com/questions/187718/create-a-new-partition-after-bootcamp)
- [How to Free Resize Bootcamp Partition without Deleting Windows](https://www.partitionwizard.com/partitionmagic/reszie-boot-camp-partition.html)
- [windows - Bootcamp Not enough space but nothing helps! - Ask Different](https://apple.stackexchange.com/questions/335076/bootcamp-not-enough-space-but-nothing-helps)
- [Backup and Restore Boot Camp on a new mac for free - benchodroff.com](https://web.archive.org/web/20210506194350/https://www.benchodroff.com/2017/02/15/backup-and-restore-boot-camp-on-a-new-mac-for-free/)
- [macos - Can't reduce size of OSX partition in bootcamp - Ask Different](https://apple.stackexchange.com/questions/170702/cant-reduce-size-of-osx-partition-in-bootcamp)
- [bootcamp - How can I adjust the size of the OSXRESERVED partition that Boot Camp Assistant uses? - Ask Different](https://apple.stackexchange.com/questions/347756/how-can-i-adjust-the-size-of-the-osxreserved-partition-that-boot-camp-assistant)

Install on external drive:

- [bootcamp - Can I install and use Windows on an external USB 3 drive in Boot Camp - Ask Different](https://apple.stackexchange.com/questions/165214/can-i-install-and-use-windows-on-an-external-usb-3-drive-in-boot-camp#165242)
- [Tech Tip: How to Use Boot Camp on an External Drive](https://web.archive.org/web/20210508133846/https://eshop.macsales.com/blog/40947-tech-tip-how-to-use-boot-camp-on-an-external-drive/)
- set `HKLM\SYSTEM\HardwareConfig\{...uuid...}\BootDriverFlags` to `0x14`: [Booting unmodified Windows 10 over USB](https://web.archive.org/web/20210224002009/http://blog.zorinaq.com/boot-win10-over-usb/)

### Apple keyboard layout

See also [Keyboard layout](../Windows/Windows.md#keyboard-layout)

Useful when you use a remote desktop connection. The host doesn't have the Apple keyboard layout.

```reg
Windows Registry Editor Version 5.00

; Layouts installed by Boot Camp Support driver package
; Layout files are relative to "C:\Windows\System32"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts]

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000404]
"Layout Component ID"="7F611C89DF564F01AE5B4A405192D1FB"
"Layout File"="ChinaTA.dll"
"Layout ID"="00e2"
"Layout Text"="Chinese Traditional (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000405]
"Layout Component ID"="0C8DA389245B4792B4960E336F62AC3E"
"Layout File"="CzechA.dll"
"Layout ID"="00d4"
"Layout Text"="Czech (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000406]
"Layout Component ID"="C3996498F423440FB9CE2732A821E7D9"
"Layout File"="DanishA.dll"
"Layout ID"="00cc"
"Layout Text"="Danish (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000407]
"Layout Component ID"="B616E2191BF048D4A554E5C6BE224AB4"
"Layout File"="GermanA.dll"
"Layout ID"="00c3"
"Layout Text"="German (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000409]
"Layout Component ID"="B422390FE3C04f3a917D15AD1ACD710F"
"Layout File"="USA.dll"
"Layout ID"="00d1"
"Layout Text"="United States (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a000040a]
"Layout Component ID"="C3364C7C44BC444A88A50459135D35B5"
"Layout File"="SpanishA.dll"
"Layout ID"="00c5"
"Layout Text"="Spanish (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a000040b]
"Layout Component ID"="ECE9937799D242F5AE0CAA446EDEDC62"
"Layout File"="FinnishA.dll"
"Layout ID"="00cb"
"Layout Text"="Finnish (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a000040c]
"Layout Component ID"="2ECD3C77364749B18E910F9196B420FA"
"Layout File"="FrenchA.dll"
"Layout ID"="00c2"
"Layout Text"="French (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a000040e]
"Layout Component ID"="725BE97D2AD14042BA539D96030F93AA"
"Layout File"="HungaryA.dll"
"Layout ID"="00d5"
"Layout Text"="Hungarian (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000410]
"Layout Component ID"="6401AAA6058F431181B445C26BEF22D9"
"Layout File"="ItalianA.dll"
"Layout ID"="00c4"
"Layout Text"="Italian (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000413]
"Layout Component ID"="3844B95343FB43D68E9695D6E88F016E"
"Layout File"="DutchA.dll"
"Layout ID"="00c1"
"Layout Text"="Dutch (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000414]
"Layout Component ID"="74BE397ABD8143E4960D38111394D1A3"
"Layout File"="NorwayA.dll"
"Layout ID"="00c9"
"Layout Text"="Norwegian (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000415]
"Layout Component ID"="D3D2841618E34D09ABBCA0DA34A60FAE"
"Layout File"="PolishA.dll"
"Layout ID"="00cf"
"Layout Text"="Polish (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000416]
"Layout Component ID"="326773935C8C4597B0738FE2084D44AD"
"Layout File"="PortuguA.dll"
"Layout ID"="00ce"
"Layout Text"="Portuguese (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000419]
"Layout Component ID"="B0F62A69BE9446488ED502E800DBC36C"
"Layout File"="RussianA.dll"
"Layout ID"="00c8"
"Layout Text"="Russian (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a000041d]
"Layout Component ID"="8CC8067A1BFF4A0FAD38708DE4CD4BF1"
"Layout File"="SwedishA.dll"
"Layout ID"="00c7"
"Layout Text"="Swedish (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a000041f]
"Layout Component ID"="2513D09A670B4d9bA8F1BDAAAA32176F"
"Layout File"="TurkeyQA.dll"
"Layout ID"="00d3"
"Layout Text"="Turkish Q (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000804]
"Layout Component ID"="472ECFB106AE4249B0ADCF62F91D8AEE"
"Layout File"="ChinaSA.dll"
"Layout ID"="00e1"
"Layout Text"="Chinese Simplified (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000809]
"Layout Component ID"="1A4D378083AD454BB4FE02F208614EB6"
"Layout File"="BritishA.dll"
"Layout ID"="00c0"
"Layout Text"="United Kingdom (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000813]
"Layout Component ID"="D70C1682E8F24ED4B5B70AAD37B1BA42"
"Layout File"="BelgiumA.dll"
"Layout ID"="00cd"
"Layout Text"="Belgian (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000c0c]
"Layout Component ID"="517A729DDEC543E3A7F392E3F130C25F"
"Layout File"="CanadaA.dll"
"Layout ID"="00ca"
"Layout Text"="Canadian Multilingual (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a000100c]
"Layout Component ID"="CE4C7E2419DE400B8A553E1A5C3DCD04"
"Layout File"="SwissA.dll"
"Layout ID"="00c6"
"Layout Text"="Swiss (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0020409]
"Layout Component ID"="241A34D0-06DB-405e-8B4E-8CA2FC34D1C7"
"Layout File"="IntlEngA.dll"
"Layout ID"="00d0"
"Layout Text"="United States-International (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a100041f]
"Layout Component ID"="D1502D2EF02F4e4b8D313D3C0B0457D0"
"Layout File"="TurkeyA.dll"
"Layout ID"="00d2"
"Layout Text"="Turkish F (Apple)"
```

- Keyboard with Mac layout: Settings > Time & language > Region & language > select current language > Options > Add keyboard > select the same language layout but with "(Apple)" > optionaly you can remove the previous layout or a keyboard layout selector in taskbar will appears
    - [Change the Windows regional settings to modify the appearance of some data types - Access](https://support.office.com/en-us/article/change-the-windows-regional-settings-to-modify-the-appearance-of-some-data-types-edf41006-f6e2-4360-bc1b-30e9e8a54989)
    - [The Microsoft Keyboard Layout Creator](https://support.microsoft.com/en-us/help/823010/the-microsoft-keyboard-layout-creator)
- [Utiliser un clavier Apple avec Connexion Bureau à distance* – i3idouille](https://web.archive.org/web/20200914101629/https://www.i3idouille.fr/index.php/2011/12/sys-utiliser-un-clavier-apple-avec-connexion-bureau-a-distance/)
- [Use your Apple Keyboard in Windows with Boot Camp - Apple Support](https://support.apple.com/en-us/HT202676)
- [Keyboard mappings using a PC keyboard on a Macintosh](https://support.microsoft.com/en-us/help/970299/keyboard-mappings-using-a-pc-keyboard-on-a-macintosh)

## Network

- [What causes some Network Drives using SMB no longer connect to macOS Catalina? - Ask Different](https://apple.stackexchange.com/questions/362739/what-causes-some-network-drives-using-smb-no-longer-connect-to-macos-catalina) - SMB and NetBIOS (`/etc/nsmb.conf`) troubles

### Bandwidth limiter

Use "Network Link Conditioner" (but not work for localhost/127.0.0.1) or use a proxy instead (for HTTP/HTTPS)

Install:

1. download "Additional Tools for Xcode" from https://developer.apple.com/download/more/?q=Additional%20Tools
2. from DMG, double click to install `Network Link Conditioner.prefPane`

- http://nshipster.com/network-link-conditioner/
- https://developer.apple.com/downloads/index.action?q=Network%20Link%20Conditioner
- [macos - How to simulate slow internet connections on the mac - Ask Different](http://apple.stackexchange.com/questions/24066/how-to-simulate-slow-internet-connections-on-the-mac)

### VPN

- [macos - Mac OS X and VPN Option all traffic over vpn - Super User](https://superuser.com/questions/744174/mac-os-x-and-vpn-option-all-traffic-over-vpn)
- [Overriding Routing for VPNs on macOS - Dennis Tsang](https://dennistt.net/2019/05/05/overriding-routing-for-vpns-on-macos/)

### Local TLD

Use `*.localhost` instead of `*.local`. It's a reserved, internal TLD too.

- http://www.justincarmony.com/blog/2011/07/27/mac-os-x-lion-etc-hosts-bugs-and-dns-resolution/
- [Accessing .local domains is slow on Mac OS X • Charles Web Debugging Proxy](http://www.charlesproxy.com/documentation/faqs/accessing-local-domains-is-slow-on-mac-os/)
- [phishing - If someone bought the .local TLD could that be a security risk? - Information Security Stack Exchange](http://security.stackexchange.com/questions/14802/if-someone-bought-the-local-tld-could-that-be-a-security-risk)
- [Top level domain/domain suffix for private network? - Server Fault](http://serverfault.com/questions/17255/top-level-domain-domain-suffix-for-private-network)
- [Guidance on Internal Names - CAB Forum](https://cabforum.org/internal-names/)

### Hosts files

Fake DNS records

Require root access to update the content:


```sh
sudo vi /etc/hosts
```

- [The Mac Hosts File: How to Modify /etc/hosts in OS X with TextEdit](http://osxdaily.com/2016/02/29/modify-hosts-mac-os-x-textedit/)
- [specialunderwear/Hosts.prefpane: a Cocoa GUI for /etc/hosts](https://github.com/specialunderwear/Hosts.prefpane)

### Create link to Network Utility

```sh
cd /Applications/Utilities/
ln -s /System/Library/CoreServices/Applications/Network\ Utility.app Network\ Utility.app
```

Moved in CoreServices in 10.9

### Flush DNS cache

```sh
sudo killall -HUP mDNSResponder
```

- [Reset the DNS cache in OS X - Apple Support](https://support.apple.com/en-us/HT202516)

### Share network connection

- [macOS Sierra: Share the Internet connection on your Mac](https://support.apple.com/kb/ph25327?locale=en_US)
- [Reverse Tether - Share OSX Yosemite Wifi Connection Over Bluetooth - Ask Different](http://apple.stackexchange.com/questions/180578/reverse-tether-share-osx-yosemite-wifi-connection-over-bluetooth)

## UI

Finder, desktop, menus, etc.

### Reveal Libray folder

	chflags nohidden ~/Library

### Show hidden files

Or use the combination of <kbd>Shift ⇧</kbd> <kbd>Cmd ⌘</kbd> <kbd>.</kbd> or <kbd>Fn</kbd> <kbd>Shift ⇧</kbd> <kbd>Cmd ⌘</kbd> <kbd>.</kbd> (for French NUM? keyboards)

	defaults write com.apple.finder AppleShowAllFiles -bool YES && killall Finder
	defaults write com.apple.finder AppleShowAllFiles TRUE && killall Finder

- [Mac keyboard shortcuts - Apple Support](https://support.apple.com/en-us/HT201236)

### Hide specific file on desktop

If hidden files are not visible:

```sh
chflags hidden file
chflags nohidden file
```

Else :

1. Copy a transparent image (in preview: select image pixel area then copy)
2. Past it as icon of targeted file
3. Move to outside of desktop viewport

- [osx - Show hidden files on OS X except .DS_Store - Super User](http://superuser.com/questions/31580/show-hidden-files-on-os-x-except-ds-store)

### Reload "Open With" menu entries

```sh
/System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/LaunchServices.framework/Versions/A/Support/lsregister -kill -r -domain local -domain system -domain user
```

- [How to rebuild the LaunchServices database - Mac OS X Hints](http://hints.macworld.com/article.php?story=20031215144430486)

### Menulets / Menu extra

Menulets are of small icons located at the upper right corner of the Menu Bar

`/System/Library/CoreServices/Menu Extras/*.menu`

- [Menu extra - Wikipedia](https://en.wikipedia.org/wiki/Menu_extra)

### Finder view preferences System-wide

1. Close all Finder windows
2. `find ~ -name ".DS_Store" -depth -exec rm -f {} \;`
3. Kill finder: Force Quit → Finder
4. Open a Finder window, edit Folder View Options show and click on "Use as default"

- [osx - System-wide finder view preferences - Ask Different](http://apple.stackexchange.com/questions/10488/system-wide-finder-view-preferences)

### Localizable resource name

That use short language ISO code (ISO639).

Dans les fichiers `.strings` les retours à la ligne sont marqué `\n`. Voir aussi "\"", "\\". Le commentaires supporté (`/* ... */` et `// ...`). Ces fichiers doivent être enregistré en UTF-16

https://developer.apple.com/library/mac/documentation/FileManagement/Conceptual/FileSystemAdvancedPT/LocalizingtheNameofaDirectory/LocalizingtheNameofaDirectory.html

#### System (default)

Edit following file (require root's right)

	System/Library/CoreServices/SystemFolderLocalizations/fr.lproj/SystemFolderLocalizations.strings
	System/Library/CoreServices/SystemFolderLocalizations/zh_CN.lproj/SystemFolderLocalizations.strings

Add or update

	"Stuff" = "Choses";

	Stuff
		.localized

`.localized` is an empty file (0 bytes)

#### Folder

	Stuff.localized
		.localized
			de.strings
			en.strings
			fr.strings
			zh-Hans.strings

In `fr.strings`:

	"Stuff" = "Choses";

- `/Applications/VMware Fusion.app/Contents/ResourcesVirtual Machines.localized/.localized/*` (VMware Fusion 7.0)

#### Bundle

	Stuff
		Info.plist
		Resources
			de.lproj
			en.lproj
			fr.lproj
				InfoPlist.strings

In `Stuff/Info.plist`, we found:

	<key>CFBundleDisplayName</key>
	<string>Stuff</string>

It's not required but I we want localizable bundle, we need it.

We can found also `NSHumanReadableCopyright` (copyright) and `CFBundleName` (display app name in menu bar) which are also localizable.

In `Stuff/Resources/fr.lproj/InfoPlist.strings`, we found:

	CFBundleDisplayName = "Choses";

### Kiosk mode

- [How to use Parental Controls on your Mac: The ultimate guide | iMore](https://www.imore.com/parental-controls-mac-ultimate-guide#apps)
- [macos - Boot straight to an Application when Mac is turned on - Ask Different](https://apple.stackexchange.com/questions/134857/boot-straight-to-an-application-when-mac-is-turned-on)
- [Technical Note TN2062: Creating Kiosks](https://developer.apple.com/library/content/technotes/tn2062/_index.html)
- [Setting the Mac Login for Kiosk Mode](http://www.dummies.com/computers/macs/mac-operating-systems/setting-the-mac-login-for-kiosk-mode/)
- [Kiosk Mode Technical Note](https://developer.apple.com/library/content/technotes/KioskMode/Introduction/Introduction.html)
- [macos - run kiosk .app at startup in mac - Stack Overflow](https://stackoverflow.com/questions/4883236/run-kiosk-app-at-startup-in-mac)

### Keyboard layout

macOS on a MacBook (without special keys like page up/down keys):

- Page up : fn + up
- Page down : fn + down
- Home : fn + left
- End : fn + right
- Del : fn + backspace
- Enter (num) : fn + return

See also [Apple keyboard layout on Windows](../Windows/Windows.md#apple-keyboard-layout)

### Mouse acceleration

USB Overdrive works if you change system mouse speed to 0 (or -1)

- [©1999-2017 Alessandro Levi Montalcini](http://www.usboverdrive.com/USBOverdrive/News.html) - USB Overdrive
- [macos - How to disable mouse acceleration in Yosemite? - Ask Different](https://apple.stackexchange.com/questions/151539/how-to-disable-mouse-acceleration-in-yosemite)
- [Mouse Acceleration on a Mac – What it is and How to Adjust or Disable it](http://osxdaily.com/2010/08/25/mouse-acceleration/)
- [Removing Mouse Acceleration in MacOS and OSX (High Sierra) : macgaming](https://www.reddit.com/r/macgaming/comments/7bg3gg/removing_mouse_acceleration_in_macos_and_osx_high/)

System mouse speed

```sh
defaults read .GlobalPreferences com.apple.mouse.scaling
# same value as System Preferences > Mouse > Speed
#defaults write .GlobalPreferences com.apple.mouse.scaling -1
```

killmouseaccel:

Doesn't work with High Sierra due to depreciation of IOHID API.

```sh
#gcc killmouseaccel.c -o killmouseaccel -framework IOKit -framework Carbon
gcc killmouseaccel/main.c -o killmouseaccel/killmouseaccel -framework IOKit -framework Carbon
#chmod +x killmouseaccel
./killmouseaccel mouse
```

- [docwhat/killmouseaccel: Kills mouse acceleration dead (OS-X)](https://github.com/docwhat/killmouseaccel)
- [How to kill mouse acceleration in OS X | MacRumors Forums](https://forums.macrumors.com/threads/how-to-kill-mouse-acceleration-in-os-x.812687/)

### Restart Dock

Will restart Dock, Mission Control, Spaces, etc.

```sh
killall -KILL Dock
```

For menubar

```sh
killall -KILL SystemUIServer
```

Or Finder

```sh
killall -KILL Finder
```

### Spaces in dock

```sh
defaults write com.apple.dock persistent-apps -array-add '{tile-data={}; tile-type="spacer-tile";}'
killall Dock
```

### Continuity with Android

- [KDE Connect is Now Available for macOS (Updated) - OMG! Ubuntu!](https://www.omgubuntu.co.uk/2019/07/kde-connect-mac-os-integrate-android)
- [KDE Connect macOS Release | Inoki in KDE](https://kde.inoki.cc/2019/09/01/KDE-Connect-macOS-GSoC-Final-Release/)
- [Release GSoC Release · Inokinoki/kde-blog](https://github.com/Inokinoki/kde-blog/releases/tag/20190901)
- [KDE Connect - Apps on Google Play](https://play.google.com/store/apps/details?id=org.kde.kdeconnect_tp)

## Disk, file system and paths

- disk path: `/dev/diskX` where X is a number (start with 1)
- mounted in `/Volumes/XXXX`

See [FileVault](#filevault)

### Extended attribute

Aka quarantine, icons, thumbnail, `xattr`

See also [Spotlight](#spotlight) and [Uniform Type Identifier](#uniform-type-identifier)

Extended attribute `com.apple.FinderInfo` (same/similar binary format as [resource fork](https://en.wikipedia.org/wiki/Resource_fork) and [AppleDouble file](https://en.wikipedia.org/wiki/AppleSingle_and_AppleDouble_formats), [`com.apple.ResourceFork`](https://web.archive.org/web/20201031144833/https://eclecticlight.co/2017/12/12/xattr-com-apple-resourcefork-a-classic-mac-resource-fork/)):

> com.apple.FinderInfo (XATTR_FINDERINFO_NAME, ATTR_CMN_FNDRINFO getattrlist(2))
> 32 bytes of data for use by the Finder.  Equivalent to the concatenation of a FileInfo structure and an ExtendedFileInfo structure (or, for directories, a FolderInfo structure and an ExtendedFolderInfo structure).
> These structures are defined in <CarbonCore/Finder.h>.
>
> This attribute is not byte swapped by the file system.  The value of multibyte fields on disk is always big endian.
> When running on a little endian system (such as Darwin on x86), you must byte swap any multibyte fields.

- [xattr: com.apple.FinderInfo, information for the Finder – The Eclectic Light Company](https://web.archive.org/web/20201031174043/https://eclecticlight.co/2017/12/19/xattr-com-apple-finderinfo-information-for-the-finder/)
- [How to add a custom icon to an app without breaking its signature – The Eclectic Light Company](https://web.archive.org/web/20200311090951/https://eclecticlight.co/2019/07/20/how-to-add-a-custom-icon-to-an-app-without-breaking-its-signature/)

```sh
# Add a fake name
xattr -w com.apple.metadata:kMDItemDisplayName MyNewFilename.txt ActualFile.txt

# Hide file to Finder
xattr -px com.apple.FinderInfo testfile
#00 00 00 00 00 00 00 00 40 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
xattr -wx com.apple.FinderInfo "0000000000000000400000000000000000000000000000000000000000000000" filename
# or (spaces aren't important)
xattr -wx com.apple.FinderInfo "00 00 00 00 00 00 00 00 40 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00" filename
# Find some hidden files (kMDItemFSInvisible mapped from the extended attribute com.apple.FinderInfo)
mdfind kMDItemFSInvisible=1 -onlyin .

# Add custom colors and tags to a file
# https://eclecticlight.co/2017/12/27/xattr-com-apple-metadata_kmditemusertags-finder-tags/
xattr -wx com.apple.metadata:_kMDItemUserTags "62706c69 73743030 a3010203 584f7261 6e67650a 37585965 6c6c6f77 0a355949 6d706f72 74616e74 080c151e 00000000 00000101 00000000 00000004 00000000 00000000 00000000 00000028" filename
xattr -wx com.apple.metadata:_kMDItemUserTags "$(echo '["Orange\n7","Yellow\n5","Important"]' | plutil -convert binary1 -o - - | xxd -p)" filename
xattr -w com.apple.metadata:_kMDItemUserTags '("Red\n6","new tag")' filename
xattr -w com.apple.metadata:_kMDItemUserTags '<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd"><plist version="1.0"><array>...</array></plist>' filename
# Metadata see by Spotlight backend (metadata server)
mdls -plist - -name _kMDItemUserTags

# Set custom application association
# Even if the type is the default "public.data"
xattr -wx com.apple.LaunchServices.OpenWith "$(echo '{"version":0,"path":"\/Applications\/Hex Fiend.app","bundleidentifier":"com.ridiculousfish.HexFiend"}' | plutil -convert binary1 -o - - | xxd -p)" filename
# Get custom application association
xattr -p com.apple.LaunchServices.OpenWith /path/to/file | xxd -r -p - | plutil -convert json -o - -
#xattr -p com.apple.LaunchServices.OpenWith /path/to/file | xxd -r -p - | plutil -convert json -o - -
```

Other:

- [xattred, Sandstrip & xattr tools – The Eclectic Light Company](https://eclecticlight.co/xattred-sandstrip-xattr-tools/)
- [An introduction to extended attributes, xattrs – The Eclectic Light Company](https://web.archive.org/web/20200316222605/https://eclecticlight.co/2017/12/11/an-introduction-to-extended-attributes-xattrs/)
- [How to preserve metadata stored in a custom extended attribute – The Eclectic Light Company](https://web.archive.org/web/20200414045618/https://eclecticlight.co/2019/10/01/how-to-preserve-metadata-stored-in-a-custom-extended-attribute/)
- [Spotlight Metadata Attributes](https://developer.apple.com/library/archive/documentation/CoreServices/Reference/MetadataAttributesRef/Reference/CommonAttrs.html#//apple_ref/doc/uid/TP40001694-SW1)
- [About File Metadata Queries](https://developer.apple.com/library/archive/documentation/Carbon/Conceptual/SpotlightQuery/Concepts/Introduction.html)
- [xattr: com.apple.LaunchServices.OpenWith, sets a custom app to open a file – The Eclectic Light Company](https://web.archive.org/web/20201031170621/https://eclecticlight.co/2017/12/20/xattr-com-apple-launchservices-openwith-sets-a-custom-app-to-open-a-file/)
- [xattr: com.apple.metadata:_kMDItemUserTags, Finder tags – The Eclectic Light Company](https://web.archive.org/web/20190629034831/https://eclecticlight.co/2017/12/27/xattr-com-apple-metadata_kmditemusertags-finder-tags/)

### Icons and Cursors

```
/System/Library/Frameworks/ApplicationServices.framework/Versions/A/Frameworks/HIServices.framework/Versions/A/Resources/cursors
/System/Library/CoreServices/CoreTypes.bundle/Contents/Resources
```

### Sounds

```
/System/Library/Sounds/
/Library/Sounds/
~/Library/Sounds/
```

### AFPS

> Does Apple File System support directory hard links?
>
> Directory hard links are not supported by Apple File System. All directory hard links are converted to symbolic links or aliases when you convert from HFS+ to APFS volume formats on macOS.
> — [Frequently Asked Questions](https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/APFS_Guide/FAQ/FAQ.html)

### NTFS

Read only

Use NTFS-3G or use exFAT instead (supported natively)

- [howto/Ntfs3gFinder – MacPorts](https://trac.macports.org/wiki/howto/Ntfs3gFinder)

### Mount file system

- [Home - macFUSE](https://osxfuse.github.io/) (successor of MacFUSE)

#### Mount AFP share online

**Don't do that! It's not secure (same for NFS, CIFS, SMB). Use it over a VPN (or a SSH tunnel) or use SFTP** (use https://github.com/osxfuse/osxfuse/wiki/SSHFS)

Can contains Time Machine backups

Mount afp://ip_address/TIMEMACHINE

Port 548 should be open (and forwarded (TCP) to the target if the server is behind a router). **Don't allow guest access**

- [security - How secure is Apple File Protocol from Airport Extreme - Ask Different](http://apple.stackexchange.com/questions/34902/how-secure-is-apple-file-protocol-from-airport-extreme)
- [AFP File Server Security](https://developer.apple.com/library/mac/documentation/Networking/Conceptual/AFP/AFPSecurity/AFPSecurity.html)

### System links

Preference and help links

Open an pref

```
x-help-script://com.apple.machelp/scpt/OpnPrefsBndID.scpt?com.apple.Localization,InputMenu
```

Open an app:

```
x-help-script://com.apple.machelp/scpt/OpnAppBndID.scpt?open,com.apple.ScriptEditor2
```

```
help:anchor=%27mh28040%27%20bookID='com.apple.machelp'
```

Home (`help:anchor=%27access%27%20bookID=com.apple.machelp`)
Index (`help:anchor=%27xall%27%20bookID=com.apple.machelp`)

### System paths

- [Yelp/osxcollector: A forensic evidence collection & analysis toolkit for OS X](https://github.com/Yelp/osxcollector) - A forensic evidence collection & analysis toolkit for OS X

- [pstirparo/mac4n6: Collection of forensics artifacs location for Mac OS X and iOS](https://github.com/pstirparo/mac4n6)
- [Mac OS X 10.9 - Artifacts Location - ForensicsWiki](http://forensicswiki.org/wiki/Mac_OS_X_10.9_-_Artifacts_Location)
- [OS X Lion Artifacts v1.0 - Google Sheets](https://docs.google.com/spreadsheets/d/1VobbmKTw8h_wKr0fpNXiyqOc1eCTuqiRkhIguVk_eXA/edit#gid=0)

### Re-add `staff` premission

```sh
sudo chgrp staff path/to/item
sudo chmod g+r,+X path/to/item
```

- [How do I add permissions for "System" and "Staff"? | Official Apple Support Communities](https://discussions.apple.com/thread/2240708)

### Uniform Type Identifier

Aka UTI

Metadatas: `kMDItemContentType` and `kMDItemContentTypeTree` (hierarchical content type); `CFBundleDocumentTypes`, `UTImportedTypeDeclarations` and `UTExportedTypeDeclarations`

Get UTI from metadata server:

```sh
mdls -raw -name kMDItemContentType $FILE
```

For the same extension, mutliple UTI definitions could exist. But the last definition will be used. Exemple: Adobe Flash use `.as` for ActionScript files (source code), but `.as` is declared instead as "AppleSingle archive" (UTI: `com.apple.applesingle-archive`). Installing Adobe Flash should override the default declaration. See [uti - Revert Filetype Association - Ask Different](http://apple.stackexchange.com/questions/49447/revert-filetype-association/86762#86762)

- [What happens when you double-click a document? Processes, problems and solutions – The Eclectic Light Company](https://web.archive.org/web/20200815140318/https://eclecticlight.co/2020/05/04/what-happens-when-you-double-click-a-document-processes-problems-and-solutions/)
- [Introduction to Uniform Type Identifiers Overview](https://developer.apple.com/library/content/documentation/FileManagement/Conceptual/understanding_utis/understand_utis_intro/understand_utis_intro.html)
- [System-Declared Uniform Type Identifiers](https://developer.apple.com/library/content/documentation/Miscellaneous/Reference/UTIRef/Articles/System-DeclaredUniformTypeIdentifiers.html)
- `/System/Library/CoreServices/CoreTypes.bundle/Contents/Info.plist`
- [Fun with UTI | Cocoanetics](https://www.cocoanetics.com/2012/09/fun-with-uti/)
- https://github.com/schwa/UTI-Types/tree/master/Types - List of common UTI
- [Amit's Thoughts: Mac OS: Spotlight and source code](https://web.archive.org/web/20200805112003/http://amitp.blogspot.com/2014/05/mac-os-spotlight-and-source-code.html)
- [Amit's Thoughts: Mac OS: index source code](https://web.archive.org/web/20200922025246/http://amitp.blogspot.com/2014/06/mac-os-index-source-code.html)
- [Core Foundation Keys](https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CoreFoundationKeys.html#//apple_ref/doc/uid/20001431-101685)
- [macos - OSX: assign extension to content kind - Super User](http://superuser.com/questions/371892/osx-assign-extension-to-content-kind/371939#371939)
- `/System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/LaunchServices.framework/Versions/Current/Support/lsregister -dump` - list all registered UTI
- `/System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/LaunchServices.framework/Versions/Current/Support/lsregister -kill -r -domain local -domain system -domain user` - ro rebuild the Launch Services registry to fix a wrong attribution (after an App Upgrade)
- [filesystem - Change file kind / kMDItemContentType - Ask Different](http://apple.stackexchange.com/questions/134726/change-file-kind-kmditemcontenttype/134731#134731) - for bash script
- [UTI Property List Helper](http://boredzo.org/uti-plist-helper/) - generate UTI definition (plist) from existing UTI

### Fragmentation

Aka defragmentation

- [Ten Things Apple Did To Make Mac OS X Faster](http://osxbook.com/book/bonus/misc/optimizations/#FIVE) - On-the-fly Defragmentation
- [Ten Things Apple Did To Make Mac OS X Faster](http://osxbook.com/book/bonus/misc/optimizations/#THREE) - Hot File Clustering

### Disk image

> ## Create a disk image from a disk or connected device
>
> [...]
>
> - **Sparse bundle disk image:** Same as a sparse disk image (below), but the directory data for the image is stored differently. Uses the .sparsebundle file extension.
> - **Sparse disk image:** Creates an expandable file that shrinks and grows as needed. No additional space is used. Uses the .sparseimage file extension.
> - **Read/write disk image:** Allows you to add files to the disk image after it’s created. Uses the .dmg file extension.
> - **DVD/CD master:** Changes the size of the image to 177 MB (CD 8 cm). Uses the .cdr file extension.
>
> [...]
>
> ## Create a disk image from a folder or connected device
>
> [...]
>
> - **Read-only:** The disk image can’t be written to, and is quicker to create and open.
> - **Compressed:** Compresses data, so the disk image is smaller than the original data. The disk image is read-only.
> - **Read/write:** Allows you to add files to the disk image after it’s created.
> - **DVD/CD master:** Can be used with third-party apps. It includes a copy of all sectors of the disk image, whether they’re used or not. When you use a master disk image to create other DVDs or CDs, all data is copied exactly.
>
> — [Create a disk image using Disk Utility on Mac - Apple Support](https://support.apple.com/guide/disk-utility/create-a-disk-image-dskutl11888/mac)

- [Create or resize sparsebundle](#create-or-resize-sparsebundle)

### Split disk image

```sh
hdiutil segment -segmentSize 1G -o "disk-1G-parts.dmg" "/path/to/disk.dmg"
```

Will generate files `*.XXX.dmgpart` and `*.dmg`

### Folder action

See [Automator](#automator)

- [Mac Automation Scripting Guide: Watching Folders](https://developer.apple.com/library/archive/documentation/LanguagesUtilities/Conceptual/MacAutomationScriptingGuide/WatchFolders.html)
- [Folder Actions Reference](https://developer.apple.com/library/archive/documentation/AppleScript/Conceptual/AppleScriptLangGuide/reference/ASLR_folder_actions.html)
- [DouglasUrner/OS-X-Folder-Actions: Mac OS X folder action dispatcher and sample scripts.](https://github.com/DouglasUrner/OS-X-Folder-Actions)
- [macos - OSX: Execute bash script when file appears in folder - Stack Overflow](https://stackoverflow.com/questions/21385105/osx-execute-bash-script-when-file-appears-in-folder)
- [macos - How do I use OSX's Folder Actions to execute a command in Terminal when a file is added to a folder? - Stack Overflow](https://stackoverflow.com/questions/52770684/how-do-i-use-osxs-folder-actions-to-execute-a-command-in-terminal-when-a-file-i)
- [bash - Folder action not triggering shell script - Stack Overflow](https://stackoverflow.com/questions/38665137/folder-action-not-triggering-shell-script)

### Test disk speed

aka test USB thumb speed

```sh
# Write 1GB of zero to tsfile
dd if=/dev/zero bs=1024k of=tstfile count=1024
# Will output (if locale is english):
# 1024+0 records in
# 1024+0 records out
# 1073741824 bytes (1.1 GB) copied, 2.27431 s, 472 MB/s

# Read tsfile (1GB)
dd if=tstfile bs=1024k of=/dev/null count=1024
# Remove tsfile
rm tstfile
```

- [Benchmark your SSD or hard disk speed - Mac OS X Hints](https://web.archive.org/web/20200924161550/https://hints.macworld.com/article.php?story=20120704113548693):
- [‎Blackmagic Disk Speed Test on the Mac App Store](https://apps.apple.com/us/app/id425264550?mt=12)

## Startup and login

### Startup chime

Not work with OSX 10.10+

Mute

```sh
sudo nvram SystemAudioVolume=%80
```

Restore

```sh
sudo nvram -d SystemAudioVolume
```

- http://apple.stackexchange.com/questions/168092/disable-yosemite-startup-sound
- https://discussions.apple.com/message/28013107#28013107

### Lock message

Aka login screen text

> If found, please contact XXXX XXXX at YYYYYYYYYYY or at ZZZZZZ@ZZZZZZ.ZZZZ

Control+Command+Q

- [How to set a lock message on the login window of your Mac - Apple Support](https://support.apple.com/en-us/HT203580) - Settings > security and privacy > (unlock with padlock) > Show a message when the screen is locked
- [Onyx](https://www.titanium-software.fr/) - Settings > Session > Login screen message
- [How and Why You Should Customise Your Mac's Login Screen](https://computers.tutsplus.com/tutorials/how-and-why-you-should-customise-your-macs-login-screen--mac-56657)

See also [Change the language used at the login screen on your Mac - Apple Support](https://support.apple.com/en-us/HT202036)

### Reset NVRAM

[How to Reset NVRAM on your Mac - Apple Support](https://support.apple.com/en-us/HT204063)

### Start up item

Create in `/Library/LaunchDaemons` a file called like `info.mamp.start.apache.plist` contains

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>info.mamp.start.apache</string>
    <key>ProgramArguments</key>
    <array>
      <string>/path/to/binary</string>
      <string>arg1</string>
	  <string>arg2=value</string>
	  <string>arg3</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
	<!-- Use this user to launch daemon, remove if not defined -->
	<key>UserName</key>
	<string>YOUR_USERNAME</string>
	<!-- -->
  </dict>
</plist>
```

`Label` must reflect filename without `plist` extension.

	sudo chown root:wheel /Library/LaunchDaemons/info.mamp.start.apache.plist

- [A launchd Tutorial](http://launchd.info/)
- http://en.wikipedia.org/wiki/Launchd
- http://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CreatingLaunchdJobs.html

### Change/fix login keyboard layout

```sh
# Check current user keyboard
/usr/libexec/PlistBuddy -c "Print :AppleCurrentKeyboardLayoutInputSourceID" ~/Library/Preferences/com.apple.HIToolbox.plist
# defaults -currentHost read com.apple.HIToolbox
# Set global/default keyboard
sudo /usr/libexec/PlistBuddy -c "Set :AppleCurrentKeyboardLayoutInputSourceID com.apple.keylayout.French" /Library/Preferences/com.apple.HIToolbox.plist
```

See you current keyboard layout: `~/Library/Preferences/com.apple.HIToolbox.plist`

- [Fix an incorrect default keyboard layout at the OS X login prompt | MacIssues](https://www.macissues.com/2015/04/16/fix-an-incorrect-default-keyboard-layout-at-the-os-x-login-prompt/)
- [lion - How to remove or disable a default keyboard layout? - Ask Different](https://apple.stackexchange.com/questions/44921/how-to-remove-or-disable-a-default-keyboard-layout)
- [minoki/InputSourceSelector: A utility program to manipulate Input Sources on Mac OS X.](https://github.com/minoki/InputSourceSelector)
- [macos - Change OSX keyboard layout("input source") programmatically via terminal or AppleScript? - Stack Overflow](https://stackoverflow.com/questions/23729704/change-osx-keyboard-layoutinput-source-programmatically-via-terminal-or-appl.)

## Security

### System Integrity Protection

Aka SIP

- `/System`
- `/usr`
- `/bin`
- `/sbin`
- apps that are pre-installed with OS X

Some specific softwares require to disable it

- [Disable .DS_Store in OS X El Capitan](http://pixelcog.com/blog/2016/disable-ds_store-in-el-capitan/)

1. in Terminal: `csrutil status` to check status
2. restart
3. hold down command-R to boot into the Recovery System
4. in Utilities > Terminal `csrutil disable; reboot` or `csrutil enable; reboot` based on what you want

> SIP only applies to the volume you're currently booted from, so [one can] boot from the backup volume to delete [files]
> [CCC updated for El Capitan | Carbon Copy Cloner | Bombich Software](https://bombich.com/blog/2015/09/10/ccc-updated-el-capitan)

1. just boot into "Recovery" mode by pressing "CMD+R" while rebooting.
2. open Terminal
3. your disk will be mounted in `/Volumes/Macintosh HD` (based on your drive name)
4. update files (ex: delete files via `rm`): you have absolute control in that terminal

- [Running TotalSpaces2 on El Capitan with SIP fully enabled](https://totalspaces.binaryage.com/elcapitan-with-sip#mark-steps-1-3)
- [System Integrity Protection – Adding another layer to Apple’s security model | Der Flounder](https://derflounder.wordpress.com/2015/10/01/system-integrity-protection-adding-another-layer-to-apples-security-model/)
- `/Library/SystemMigration/History/Migration-[some UUID]/QuarantineRoot/`
- [System Integrity Protection - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/System_Integrity_Protection)
- [Sierra’s System Integrity Protection (SIP): beyond root – The Eclectic Light Company](https://eclecticlight.co/2017/04/28/sierras-system-integrity-protection-sip-beyond-root/)
- [About System Integrity Protection on your Mac - Apple Support](https://support.apple.com/en-us/HT204899)
- [high sierra - Is /dev protected by SIP? - Ask Different](https://apple.stackexchange.com/questions/304591/is-dev-protected-by-sip?noredirect=1&lq=1)

#### Terminal access error

If a command return an error like `Operation not permitted`, or `cat: ~/Library/path/to/file: Operation not permitted`, a SIP protected file is read.

Lift the restriction for Terminal: [Operation not permitted - Mojave security?](https://apple.stackexchange.com/questions/339862/ls-operation-not-permitted-mojave-security/345142#345142)

### App Sandbox

```
~/Library/Containers
```

- [Objective-See](https://objective-see.com/blog/blog_0x10.html)

### Downloaded file quarantine

```sh
find ~/Downloads/geeklog-1.6.1 -type f -exec xattr -d com.apple.quarantine {} \;
```

or

```sh
xattr -d -r com.apple.quarantine ~/Downloads
```

Disable

```sh
defaults write com.apple.LaunchServices LSQuarantine -bool NO
```

### Certificats

Delete Known Government-Linked Certificate Authorities: https://github.com/sammcj/delete-unknown-root-ca

### FileVault

FileVault display a loginwindow at startup hask the user to decrypt the disk with its password.

FileVault is not allowed for all users

```sh
diskutil cs list | grep "Conversion Progress"
diskutil apfs list | grep "FileVault"
```

```
Conversion Progress:       Optimizing 39%

FileVault:                 Yes (Unlocked)

FileVault:                 No (Encrypted at rest)
```

- To select which user can decrypt FileVault disk:
	1. login as admin local account
	2. open System Preferences
	3. open Security & Privacy
	4. select FileVault
	5. click on "Allow Users" (bottom of the window)
- `sudo fdesetup list`
- [Users not showing at login screen with MacOS FileVault Enabled - Stack Overflow](https://stackoverflow.com/questions/53586815/users-not-showing-at-login-screen-with-macos-filevault-enabled)
- `sudo sysadminctl -adminUser <adminUser> -adminPassword <adminPassword> -secureTokenOn <managementToken> -password <managmentPassword>`
- `sudo fdesetup add -usertoadd <username> -keychain`
- [How to View FileVault Progress When Encrypting a Mac Disk](http://osxdaily.com/2017/02/08/view-filevault-progress-mac/)
- [Secure Enclave, Mac SSD hardware encryption and the future of FileVault | Der Flounder](https://derflounder.wordpress.com/2018/01/08/secure-enclave-mac-ssd-hardware-encryption-and-the-future-of-filevault/)
- [Set a FileVault recovery key for computers in your institution - Apple Support](https://support.apple.com/en-us/HT202385) - Use same master key

### Firmware password

- [How to set a firmware password on your Mac - Apple Support](https://support.apple.com/en-us/HT204455)

### Users

Handled by OpenDirectory

> UIDs < 500 are reserved.

- auto login user `defaults read /Library/Preferences/com.apple.loginwindow | grep autoLoginUser | awk '{ print $3 }' | sed 's/;//'`
- `dscl . -read /Users/<username>`
- `dscl . list /Users | grep -v '_'` (prefixed user are daemons, etc.)
- `dscacheutil -q user`
- `/var/db/dslocal/nodes/Default/users/*.plist` data of OpenDirectory
- `sudo dscl . create /Users/<username> IsHidden 1`, hide user on loginwindow and fast user switching: [Hide a user account in macOS - Apple Support](https://support.apple.com/en-us/HT203998)
- disable guest user:
	1. ppen System Preferences
	2. go to "Users & Groups" and click the unlock icon
	3. click on “Guest User”
	4. uncheck the box for "Allow guests to log in to this computer"
- hide a user from login screen: `sudo defaults write /Library/Preferences/com.apple.loginwindow HiddenUsersList -array-add <username>`, to remove that config: `sudo defaults delete /Library/Preferences/com.apple.loginwindow HiddenUsersList`

#### Non interactive user

> loginwindow UI will consider a user as one that can't be logged in if the following occur
>
> the shell is /usr/bin/false
>
> or
>
> the AuthAuthority has ;disableduser; in it.
>
> or
>
> the AuthAuthority doesn't exist or contains ;basic; and the password is missing or is a single asterisk.
>
> or
>
> the record name is missing or blank \[RealName?\]
>
> or
>
> the uid is missing
>
> loginwindow UI doesn't care about the UIDs number.


But the user still appears in System Preferences > Sharing > File Sharing | Screen Sharing | etc. > Add User dialog.

- [#30168 (adduser results in macports users appearing as interactive users) – MacPorts](https://trac.macports.org/ticket/30168#comment:16)
- [macports-base/portutil.tcl at 1d1bcde3157908ef4ee58e72425f42d2265cdff3 · macports/macports-base](https://github.com/macports/macports-base/blob/1d1bcde3157908ef4ee58e72425f42d2265cdff3/src/port1.0/portutil.tcl#L2332-L2347) - How macports in `adduser` function set the user as non interactive user

## Applications

### Self-signed application

Create a self signed certificate `MyCertificateName` with Keychain and trust it for all the system

```sh
sudo codesign -s MyCertificateName -f /path/to/MyAppName.app --deep
```

That fix the issue with macOS open the alert popup "Do you want to the application MyAppName.app to accept incoming network connections?"

### Define `PATH` globaly

Set `export PATH=/my/path:$PATH` in `~/.profile` for command line, but not used by launched application (by spotlight, dock, finder, start restored windows)

A [security update](https://support.apple.com/en-us/HT207275) could break/change something:

> it seems SIP strips env variables if an application is launched from another application

- [Setting the system-wide PATH environment variable in Mavericks - Ask Different](http://apple.stackexchange.com/questions/106355/setting-the-system-wide-path-environment-variable-in-mavericks/106814#106814)
- (old) [macos - How to set PATH for Finder-launched applications - Ask Different](http://apple.stackexchange.com/questions/51677/how-to-set-path-for-finder-launched-applications)
- (old) [mac osx - how to set global PATH on OS X? - Server Fault](http://serverfault.com/questions/16355/how-to-set-global-path-on-os-x)

### Open application (twice and so on)

```sh
open -n /Applications/VOTRE_APPLICATION.app
```

Or add this as Automator script

```sh
do shell script "open -n /Applications/VOTRE_APPLICATION.app"
```

### Pass command line arguments to Application

#### Automator application

Automator > create an Application with `Library/Utilities/Run Shell Script`

```sh
open -a "Google Chrome" --args -pinned-tag-count=4
```

Replace app icon: `Get Info` on original App, select icon, `Cmd+C` -> `Get Info` on target App, select icon, `Cmd+V`

#### Application bundle

See [Create new application bundle](). **Not work anymore**

Edit `/Applications/Firefox.app/Contents/Info.plist`, change for `CFBundleExecutable` or `Executable File` the value to `firefox-bin-with-args.sh` (the original is `firefox-bin`)

In `/Applications/Firefox.app/Contents/MacOS/`, create a file `firefox-bin-with-args.sh` (called like change in `Info.plist`)

```sh
#!/usr/bin/env bash
exec exec $(dirname "$0")/firefox-bin -ProfileManager
```

```sh
chmod +x firefox-bin-with-args.sh
```

- http://superuser.com/questions/271678/how-do-i-pass-command-line-arguments-to-dock-items

### Create new application bundle

Script app (bash script) can't start anymore with OSX 10.10: "Can’t open the application %s because PowerPC applications are no longer supported."

- [Impedimenta/Suitcase: A flexible command line tool for instantly deploying user interfaces for simple commands and scripts.](https://github.com/Impedimenta/Suitcase)
- [How to create simple Mac apps from shell scripts · Mathias Bynens](https://mathiasbynens.be/notes/shell-script-mac-apps) (see [forks](https://gist.github.com/mathiasbynens/674099/forks)) and [appify — create the simplest possible Mac app from a shell script (adds an application icon)](https://gist.github.com/advorak/1403124) (see [forks](https://gist.github.com/advorak/1403124/forks))
- [Platypus - Create Mac apps from command line scripts](https://sveinbjorn.org/platypus)
- [DropScript](http://www.wsanchez.net/software/)
- [macos - Executing Shell Scripts from the OS X Dock? - Stack Overflow](https://stackoverflow.com/questions/281372/executing-shell-scripts-from-the-os-x-dock)
- `xattr -d com.apple.quarantine /Applications/My\ App.app`
- [macos - How does OS X detect a PowerPC application? - Ask Different](https://apple.stackexchange.com/questions/219361/how-does-os-x-detect-a-powerpc-application)
- [macos - How do I pass command line arguments to Dock items? - Super User](https://superuser.com/questions/271678/how-do-i-pass-command-line-arguments-to-dock-items)

### Allow Apps from Anywhere in Gatekeeper

"Allow apps downloaded from" "Anywhere" (from macOS Sierra)

"%s can’t be opened because it is from an unidentified developer"

```sh
sudo spctl --master-disable
```

```sh
# allow apps you trust without turning off code signing entirely
sudo spctl --add --label "It's OK, they're with me" /path/to/My.app
```

```sh
xattr -dr http://com.apple.quarantine /path/to/My.app
```

Crtl + Click on the App > click on "Open" button to add the app to the approved list
Right click > Open

- [How to Allow Apps from Anywhere in macOS Sierra Gatekeeper](http://osxdaily.com/2016/09/27/allow-apps-from-anywhere-macos-gatekeeper/)
- [Quick Tip: Override Gatekeeper with one click - Six Colors](https://sixcolors.com/post/2016/02/override-gatekeeper-with-one-click/)

### Build-in Apache

Conf: `/etc/apache2`
Extensions: `/usr/libexec/apache2`
`HTTPD_ROOT` `httpd -V`

Restart Apache:

```sh
sudo /usr/sbin/apachectl restart
```

or

```sh
sudo apachectl -k restart
```

### FileMerge

- [lion - Where can I download Filemerge - the app for comparing two tools and merging them? - Ask Different](https://apple.stackexchange.com/questions/42345/where-can-i-download-filemerge-the-app-for-comparing-two-tools-and-merging-the/42346#42346)
### Xcode

"Agreeing to the Xcode/iOS license requires admin privileges, please re-run as root via sudo."

Accept for this account:

```sh
xcodebuild -license
```

Accept for all accounts:

```sh
sudo xcodebuild -license
```

Install Xcode Command Line Tools:

```sh
xcode-select --install
```

### Macports

Why use Macports instead of Homebrew: [El Capitan and Homebrew | Hacker News](https://news.ycombinator.com/item?id=10309576)
TLDR: because it place packages in `/opt/local` and require `sudo`

Macports install in `/opt/local` where Homebrew install in `/usr/local`.

- [directory structure - What is the difference between /opt and /usr/local? - Unix & Linux Stack Exchange](http://unix.stackexchange.com/questions/11544/what-is-the-difference-between-opt-and-usr-local/11552#11552)

> `/usr/local`, for self, inhouse, compiled and maintained software.
> `/opt` is for non-self, external, prepackaged binary/application bundle installation area

- https://guide.macports.org/chunked/installing.macports.uninstalling.html
- http://trac.macports.org/wiki/Migration
- https://www.macports.org/install.php

> Macports is installed as root and uses its own account macports for some things.

Update and upgrade ports:

```sh
sudo port selfupdate && sudo port upgrade outdated
# later to remove old version
sudo port uninstall inactive
```

- [MacPorts Guide](https://guide.macports.org/#using.port.upgrade)

- [How to remove unused MacPorts packages? - Ask Different](https://apple.stackexchange.com/questions/10149/how-to-remove-unused-macports-packages)

Install ports:

```
# 1. Install Xcode Command Line Tools: `xcode-select --install`
# 2. Accept Xcode licence: `sudo xcodebuild -license`
# 3. Check installed version (newer version can exist for php, node, python, perl, ruby, JDK, etc.)

sudo port install \
wget rsync \
bash bash-completion \
coreutils diffutils findutils gsed gawk gpatch \
watch \
p5-file-rename \
openssl \
gzip gnutar \
git \
curl \
gettext \
ffmpeg \
ImageMagick +rsvg \
p5-image-exiftool \
cmake \
apache-ant \
httrack \
xorg-server

# Start D-Bus
sudo port install dbus
sudo port load dbus
#sudo launchctl load -w /Library/LaunchDaemons/org.freedesktop.dbus-system.plist
#launchctl load -w /Library/LaunchAgents/org.freedesktop.dbus-session.plist

# Add `/opt/local/libexec/gnubin` to PATH
if ! grep -q "export PATH=/opt/local/libexec/gnubin:" ~/.profile
then
	echo "" >> ~/.profile
	echo "# Use GNU coreutils by default (installed with macport)" >> ~/.profile
	echo "export PATH=/opt/local/libexec/gnubin:\$PATH" >> ~/.profile
fi

# To use bash_completion, add the following lines at the end of your .bash_profile:
if ! grep -q "/opt/local/etc/profile.d/bash_completion.sh" ~/.bash_profile
then
	echo "" >> ~/.bash_profile
	echo "# Enable bash-completion" >> ~/.bash_profile
	echo "if [ -f /opt/local/etc/profile.d/bash_completion.sh ]; then" >> ~/.bash_profile
	echo "        . /opt/local/etc/profile.d/bash_completion.sh" >> ~/.bash_profile
	echo "fi" >> ~/.bash_profile
fi

# NodeJS
# Note: nodejs and npm without version specified are not the lastest available
# sudo port install nodejs npm
sudo port install nodejs15 npm6
# Add to profile node config
if ! grep -q "export NODE_PATH=" ~/.profile
then
	echo "" >> ~/.profile
	echo "# Use global node modules (installed with macport)" >> ~/.profile
	echo "export NODE_PATH=/opt/local/lib/node_modules:\$NODE_PATH" >> ~/.profile
fi
# NPM can be updated with:
# sudo npm install -g npm@latest

# Install globally some tools
# use --python=python2.7 if required
#npm install -g sqlite3

# Note: never install globaly/system-wide npm packages (via `-g`). Install in ./node_module instead
# Clean cache: `sudo npm cache clean`
# If so packages are in /opt/local/lib/node_modules/ and remains even if npm is uninstalled or deactivate via macport
# To see outdated packages, use `npm outdated -g --depth=0`
# To update global packages, use `npm update -g`

# Install PHP and composer (PHP package manager)
sudo port install php
sudo port install php80-intl php80-openssl
#sudo port select --set php php80
# Create PHP config (dev only)
sudo cp /opt/local/etc/php80/php.ini-development /opt/local/etc/php80/php.ini

# [#42344 (new composer port request) – MacPorts](https://trac.macports.org/ticket/42344)
sudo port install php74-iconv php74-mbstring
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/opt/local/bin
sudo ln -s composer.phar /opt/local/bin/composer
# Or use in each project's folder `php -r "readfile('https://getcomposer.org/installer');" | php && php composer.phar install`
# Will install packages in ./vendor

# Install python and pip (Python package manager)
sudo port install python39 py39-pip
sudo port select --set python python39
sudo port select --set python3 python39
sudo port select --set pip pip39
# Or for OSX's default python come with easy_install
#sudo easy_install pip
#pip install --user package
# or
#python -m pip install --user package
# will install package in ~/Library/Python/X.Y/lib/python/site-packages
# could also be in ~/.local/lib/pythonX.Y/site-packages
# See
# - https://pip.pypa.io/en/latest/user_guide/#user-installs
# - https://www.python.org/dev/peps/pep-0370/
# - https://stackoverflow.com/questions/15912804/easy-install-or-pip-as-a-limited-user

# Install Python BeautifulSoup
pip install --user beautifulsoup4
# or with macports (system-wide):
#sudo port install py38-beautifulsoup4
# Then check
#python -c "help('modules')" | grep bs4

# Note: never install python packages system-wide http://scicomp.stackexchange.com/a/2988 (use always `--user`)

# Install ntfs-3g https://trac.macports.org/wiki/howto/Ntfs3gFinder (need to disable SIP)
sudo port install ntfs-3g
# TODO. See link

# TestDisk and photorec
sudo port install testdisk

# Ruby and gems (Ruby package manager)
sudo port install ruby27 rb-rubygems
sudo port select --set ruby ruby27

# Add to profile user's gems folder
if ! grep -q "export GEM_HOME=" ~/.profile
then
	echo "" >> ~/.profile
	echo "# Use user gems (rb-rubygems installed with macport)" >> ~/.profile
	echo "export PATH=~/.gem/bin:\$PATH" >> ~/.profile
	echo "export GEM_HOME=~/.gem" >> ~/.profile
	echo "export GEM_PATH=~/.gem:\$GEM_PATH" >> ~/.profile
fi

# Java / Open JDK
sudo port install openjdk15
```

## Preference pane

```
~/Library/PreferencePanes/
/Library/PreferencePanes/
```

Right click to remove prefpane

- [jlongman/speedlimit: Network bandwidth limiter for testing iphone apps](https://github.com/jlongman/speedlimit) - Network banwidth limiter
- [MySQL :: MySQL 5.7 Reference Manual :: 2.4.4 Installing and Using the MySQL Preference Pane](https://dev.mysql.com/doc/refman/5.7/en/osx-installation-prefpane.html) - MySQL Preference Pane
- [hschmidt/EnvPane: EnvPane - An OS X preference pane for environment variables](https://github.com/hschmidt/EnvPane) - Change environment variables
- [specialunderwear/Hosts.prefpane: a Cocoa GUI for /etc/hosts](https://github.com/specialunderwear/Hosts.prefpane) - Change hosts files (works with SIP enabled)
- [Lord-Kamina/SwiftDefaultApps: Replacement for RCDefaultApps, written in Swift.](https://github.com/Lord-Kamina/SwiftDefaultApps)
- (old, replace by SwiftDefaultApps) [Rubicode - RCDefaultApp](https://web.archive.org/web/20200312011847/http://www.rubicode.com/Software/RCDefaultApp/)  - "allows a user to set the default application used for various URL schemes, file extensions, file types, MIME types, and [Uniform Type Identifiers / UTIs](#uniform-type-identifier)"
- [Arcana Research - StartupSound.prefPane](http://www5e.biglobe.ne.jp/~arcana/StartupSound/index.en.html) - "controls the volume of the startup sound of your Macintosh computer"
- `/System/Library/CoreServices/Applications/Archive Utility.app/Contents/Resources/Archives.prefPane`

## Quicklook generators

Aka QLGenerator

To view handle types:

```sh
qrmanage -m
```

Precedence :

The order is currently (from the less important to the most important):
- System generators (in `/System/Library/QuickLook` - for Apple only)
- Local (in `/Library/QuickLook`)
- Home (in `~/Library/QuickLook`)
- Embedded in apps. (usally `./Contents/Library/QuickLook`)

It's impossible to desactivate a QLGenerator for same level or above other than juste rename it folder or update it's `Info.plist` to reflect only wanted format support
[How to disable auto preview for *.doc *.docx in finder? - Ask Different](https://apple.stackexchange.com/questions/33127/how-to-disable-auto-preview-for-doc-docx-in-finder)
http://lists.apple.com/archives/quicklook-dev/2010/Jun/msg00011.html

## Spotlight

Aka Metadata Server (`mds`)

See also [Extended attribute](#extended-attribute)

> Once the macOS does kick-off the extraction of metadata from a file, it does so through a Spotlight Importer. Spotlight Importers are plug-ins for the Mac OS that a developer provides specifically for helping files created by their applications to be searchable within Spotlight. Spotlight crawls through its list of changed files, handing each one to the appropriate importer. The importers then read the files, compile a list of metadata, and then hand the metadata back to Spotlight. At this point, the changed file is available for searching within Spotlight.

- [Spotlight and Document Bundles](https://developer.apple.com/library/archive/documentation/Carbon/Conceptual/MetadataIntro/Concepts/DocumentBundles.html#//apple_ref/doc/uid/TP40002007)
- [Section 11.8. Spotlight - Mac OS X Internals: A Systems Approach](https://web.archive.org/web/20130729230756/http://flylib.com/books/en/3.126.1.138/1/)

- `/System/Library/Spotlight`
- `/Library/Spotlight`
- `~/Library/Spotlight`
- App `./Content/Library/Spotlight`
- `/System/Library/Frameworks/CoreServices.framework/Frameworks/Metadata.framework/Versions/A/Support/mdworker`
- `/System/Library/LaunchDaemons/com.apple.metadata.com.apple.metadata.mds.scan.plist`
- `/System/Library/Frameworks/CoreServices.framework/Frameworks/Metadata.framework/Support/mds`
- `/System/Library/PrivateFrameworks/SpotlightDaemon.framework/Versions/A/SpotlightDaemon`
- `/System/Library/Frameworks/CoreSpotlight.framework/CoreSpotlightService`
- `/System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/Metadata.framework/Versions/A/Support/corespotlightd`

- [Troubleshooting Spotlight Importers](https://developer.apple.com/library/archive/documentation/Carbon/Conceptual/MDImporters/Concepts/Troubleshooting.html)

Turn off:

- `sudo launchctl unload -w /System/Library/LaunchDaemons/com.apple.metadata.mds.plist`
- System Preferences > Spotlight > Privacy
- (need to be verified) ignore files and directories ends with `.noindex` (and `.build`) and all (hidden) files start with `.`.
- `sudo defaults read /.Spotlight-V100/VolumeConfiguration.plist Exclusions` (that depends the filesystem)
	`sudo defaults write /.Spotlight-V100/VolumeConfiguration.plist Exclusions -array-add 'path/to/exclude'`
	`sudo defaults write /.Spotlight-V100/Store-V1/Exclusions Exclusions -array-add 'path/to/exclude'`
	`sudo defaults write /System/Volumes/Data/.Spotlight-V100/VolumeConfiguration.plist Exclusions -array-add 'path/to/exclude'`
	`sudo /usr/libexec/PlistBuddy -c "Add :Exclusions: string path/to/exclude" /System/Volumes/Data/.Spotlight-V100/VolumeConfiguration.plist`
	`sudo find / -type d -exec defaults write /.Spotlight-V100/VolumeConfiguration.plist Exclusions -array-add {}`
	`sudo launchctl stop com.apple.metadata.mds && sudo launchctl start com.apple.metadata.mds`
- put in `~/Library/`, `/System/`
- use [symlink](https://apple.stackexchange.com/questions/110915/find-symbolic-links-s-names-with-spotlight-finder) (see ["avi@ has confirmed with Apple that the indexer will not follow symlinks."](https://bugs.chromium.org/p/chromium/issues/detail?id=810617#c15))
- `.metadata_never_index` at the root of a volume, directory / folder (see also `.metadata_never_index_unless_rootfs`)

	- [Purpose of Files with the .metadata_never_index File Extension - FileTypeHelp.com](http://www.filetypehelp.com/purpose-files-metadataneverindex-file-extension/)
	- [395300 - Spotlight constantly indexing files in "Profile 2" - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=395300)
	- [apple : .Trashes, .fseventsd, and .Spotlight-V100](http://blog.hostilefork.com/trashes-fseventsd-and-spotlight-v100/)
- [810617 - Spotlight indexing Chrome data wastes power and CPU - chromium](https://bugs.chromium.org/p/chromium/issues/detail?id=810617#c14)

```sh
launchctl stop com.apple.metadata.mds && sudo launchctl start com.apple.metadata.mds
```

```sh
# Rename all node_modules to node_modules.noindex and create a symlink node_modules -> node_modules.noindex
find /path/to/projects -type d \( -path '*/.*' -o -path '*node_modules/*' -o -path '*node_module.noindex/*' \) -prune -o -type d -name 'node_modules' -exec mv '{}' '{}.noindex' \; -exec ls -s '{}.noindex' '{}' \;
```

Note: extended attribute `com.apple.FinderInfo` doesn't have any impact, `chflags hidden /path/to/file`, `touch folder-to-exclude/.metadata_never_index` too

Reindex drive

```sh
# Here the main drive mounted at /
# turn indexing off
sudo mdutil -i off /
# delete Spotlight folder
sudo rm -rf /.Spotlight*
# turn indexing on
sudo mdutil -i on /
# rebuild
sudo mdutil -E /
```

Reindex (eq. Finder's Search not work properly): `find . -name "*.md" -exec mdimport {} \;` or `sudo mdutil -E /` (where `/` affect the whole volume, or all volumes)

```sh
sudo launchctl unload -w /System/Library/LaunchDaemons/com.apple.metadata.mds.plist
sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.metadata.mds.plist
```

List file indexing (where PID is pid of process of `mdworker`, use `ps -e | grep mdworker`):

```sh
sudo opensnoop -n mdworker
# Use 0.1 or 0,1 depends locale or prepend command with `LANG=C`: (eg. `LANG=C sudo watch -n 0.1 "CMD"`)
sudo watch -n 0 "lsof +p PID"
sudo watch -n 0 "lsof -c mdworker"
strace -p PID -e trace=open,close
sudo fs_usage -w -f filesys mdworker | grep "open" | less +F --follow-name
```

Erase all Spotlight data (all volumes):

```sh
sudo mdutil -avE
```

Queries:

```sh
# Find all files
mdfind "*"
mdfind -onlyin "/" "kMDItemFSSize>0"

# List all metadata for a specific file
mdls /path/to/file

# Find DMG files
mdfind -0 "kMDItemFSName=*.dmg"
# Find Finder excluded files
mdfind "_kMDItemFinderExcluded=*"
mdfind "_kMDItemFinderExcluded=1"

# Find user tags / colors set by user
mdls -plist - -name _kMDItemUserTags

# Find ghost files ("if the Finder is in the middle of a copy and the source disk is suddenly disconnected") that aren't deletable ("Item XYZ is used by Mac OS X and can’t be opened.")
mdfind -onlyin /path/to/files -0 "kMDItemFSTypeCode==brok && kMDItemFSCreatorCode==MACS" | xargs -0 -n1 xattr -d com.apple.FinderInfo

# find all encrypted DMG
mdfind -0 "kMDItemFSName == '*.dmg'" | xargs -0 -IX ksh -c ' if hdiutil isencrypted "X" 2>&1 | grep -q "encrypted: YES" then echo "X -ENCRYPTED" fi'
```

- [Spotlight syntax, mdfind examples, and metadata attributes](http://osxnotes.net/spotlight.html)
- [MDItem - Core Services | Apple Developer Documentation](https://developer.apple.com/reference/coreservices/1658213-mditem)
- [osx - How can I add OS X "tags" to files programmatically? - Stack Overflow](https://stackoverflow.com/questions/19720376/how-can-i-add-os-x-tags-to-files-programmatically)
- [python - How to get list of files on Mac that have been tagged by Finder with a color? - Stack Overflow](https://stackoverflow.com/questions/34554852/how-to-get-list-of-files-on-mac-that-have-been-tagged-by-finder-with-a-color)
- [mavericks - Possible to tag a folder via terminal? - Ask Different](http://apple.stackexchange.com/questions/110662/possible-to-tag-a-folder-via-terminal)
- [Spotlight Metadata Attributes](http://www.real-world-systems.com/docs/mdAtt.1.html)

### Metadata importer

Aka Spotlight importers

```sh
# List all available metadatas
mdimport -X
# Infos about metadatas (nosearch, noindex, notokenize, multivalued, uniqued)
```

- [filesystem - What all file metadata is available in macOS? - Ask Different](https://apple.stackexchange.com/questions/274744/what-all-file-metadata-is-available-in-macos)
- [macOS persistence - Spotlight importers and how to create them · theevilbit blog](https://web.archive.org/web/20201106042208//)
- [Troubleshooting Spotlight Importers](https://developer.apple.com/library/archive/documentation/Carbon/Conceptual/MDImporters/Concepts/Troubleshooting.html)
- [MDImporter | Apple Developer Documentation](https://developer.apple.com/documentation/coreservices/file_metadata/mdimporter)
- [macOS persistence - Spotlight importers and how to create them · theevilbit blog](https://web.archive.org/web/20201106042208/https://theevilbit.github.io/posts/macos_persistence_spotlight_importers/)

```sh
mdimport -r ~/Library/Spotlight/SomeImporter.mdimporter
```

Add to `/System/Library/Spotlight/RichText.mdimporter/Contents/info.plist` (get file format `mdimport -n -d1 somefile.ext`) to search inside source code:

```xml
<string>public.c-header</string>
<string>public.c-plus-plus-header</string>
<string>public.c-source</string>
<string>public.objective-c-source</string>
<string>public.c-plus-plus-source</string>
<string>public.objective-c-plus-plus-source</string>
<string>com.sun.java-source</string>
<string>public.perl-script</string>
<string>public.python-script</string>
<string>public.csh-script</string>
<string>public.shell-script</string>
<string>public.ruby-script</string>
<string>public.php-script</string>
<string>com.netscape.javascript-source</string>
```

- Markdown to Spotlight [Mac OSX Spotlight Enhancement](https://gist.github.com/gereon/3150445#gistcomment-2764557)
- [Fixing Spotlight indexing of Markdown content - BrettTerpstra.com](http://brettterpstra.com/2011/10/18/fixing-spotlight-indexing-of-markdown-content/)
- [Problem with Spotlight (mds/mdimport)](https://www.rsmas.miami.edu/users/agleason/comp_other/mds.html)
- [Spotlight : réindexation des dossiers ou volumes - Assistance Apple](http://support.apple.com/fr-fr/ht2409)
- [Rebuilding Spotlight’s Index on OS X (Manually) | Walt-O-Matic](https://www.wwco.com/~wls/blog/2007/08/29/rebuilding-spotlights-index-on-os-x-manually/)
- [Spotlight tips](http://www.thexlab.com/faqs/stopspotlightindex.html)
- [osx - Is there a way to show Spotlight indexing status/progress in Yosemite? - Ask Different](http://apple.stackexchange.com/questions/155479/is-there-a-way-to-show-spotlight-indexing-status-progress-in-yosemite)

## Printer & scanner

Most post 2013 printers implement [IPP Everywhere](https://www.pwg.org/ipp/everywhere.html). AirPrint is based on IPP

- [VueScan Scanner Software for Windows, macOS Catalina and Linux](https://www.hamrick.com/) - scanner application support old scanners
- [Printer and scanner drivers for Mac - Apple Support](https://support.apple.com/en-us/HT201465) - list of old devices that don't implement IPP that macOS can auto install required drivers
- [Making an old USB printer support Apple AirPrint using a Raspberry Pi](https://web.archive.org/web/20211112203434/https://blog.jgc.org/2021/11/making-old-usb-printer-support-apple.html)

### Print on Windows shared printer

Will ask username / password for shared printer, use Windows auth credentials or `guest` for the **username and password**. If not asked, delete the entry of password in keychain app

- [On Hold - Authentication Error - Printing in OS... | Apple Support Communities](https://discussions.apple.com/message/16442328#16442328)
- [macos - How to add a network printer on mac that requires authentication - Ask Different](https://apple.stackexchange.com/questions/312882/how-to-add-a-network-printer-on-mac-that-requires-authentication/312886#312886) - Add advanced network printer via smb://someaddress/Some%20printer%20name URLs

## Calendar and contact accounts

CardDav, CalDav

SQLite3 with `principalInfo` binary PropertyList (`plutil -convert xml1 -o - - < data.plist`) (`ZVALUE`)

	~/Library/Accounts/Accounts3.sqlite

Old (not used to store accounts config):

	~/Library/Calendars/XXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX.caldav
	~/Library/Application Support/AddressBook/Sources/XXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/Configuration.plist ??

- [DaviCal and Addressbook Sync | blog.windfluechter.net](https://blog.windfluechter.net/comment/2579)
- [data synchronization - Can I sync Address Book to iCloud on Snow Leopard? - Ask Different](http://apple.stackexchange.com/questions/29832/can-i-sync-address-book-to-icloud-on-snow-leopard)
- [Howto: CardDAV in Mac OS X Addressbook with owncloud - Page 2 - ownCloud Forums](https://forum.owncloud.org/viewtopic.php?t=132&start=10) and https://github.com/owncloud/documentation/blob/stable6/user_manual/pim/sync_osx.rst
- [CardDav app - client settings - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=93093)

See also the possibility to create configuration profiles:

- [Using iOS Configuration Profiles to Improve CardDAV](https://www.fullcontact.com/blog/ios-configuration-profiles-carddav/)

## Clipbload CLI

```sh
pbcopy < file.txt
echo "test" | pbcopy
```

```sh
pbpaste
pbpaste > file.txt
```


## Simulate UI clicks from CLI

- [osx - How do I simulate a mouse click through the mac terminal? - Stack Overflow](https://stackoverflow.com/questions/4230867/how-do-i-simulate-a-mouse-click-through-the-mac-terminal/26687223)

## Corrupted executable script

Create a bash script and execute give:

> bad interpreter: Operation not permitted

```sh
chmod u+x file.sh
xattr -d com.apple.quarantine file.sh
```

## Scanning

- [VueScan Scanner Software for Windows, Mac OS X and Linux](https://www.hamrick.com/) - Support of old scanners

SANE:

- [SANE - Supported Devices](http://www.sane-project.org/sane-supported-devices.html)
- [chrspeich/SaneNetScanner: A Mac OS X Scanner Driver for sane net devices](https://github.com/chrspeich/SaneNetScanner) - This allow to use network scanner that support SANE with Image Capture, Preview
	See also [Possible bridge for TWAIN scanner: Image Capture → SaneNetScanner → localhost/saned → Scanner · Issue #13 · chrspeich/SaneNetScanner](https://github.com/chrspeich/SaneNetScanner/issues/13)
- [Install SANE drivers – BeagleScan](https://www.lazybrowndog.net/beaglescan/?page_id=6) - Install SANE drivers on macOS (`sane-find-scanner`, `scanimage -L`, `TWAINBridge.app` reinstall, `open /System/Library/Image Capture/Devices/TWAINBridge.app`, SANE > Open Scanner)
- [SwingSane](http://swingsane.com/) - Java SANE client
- [The MacPorts Project -- Available Ports](https://www.macports.org/ports.php?by=name&substr=twain-sane)
- [David Poole: Scanning from Apple AirPrint + AirScan](http://testcluster.blogspot.com/2014/03/scanning-from-apple-airprint-airscan.html)
- [phpSANE download | SourceForge.net](https://sourceforge.net/projects/phpsane/) - SANE frontend in PHP
- [SimulPiscator/AirSane: Apple AirScan compatible SANE web frontend.](https://github.com/SimulPiscator/AirSane) - Install that frontend on the device where SANE backend are used (where the USB scanner is connected) to share the scanner over AirScan
	See also [David Poole: Scanning from Apple AirPrint + AirScan](http://testcluster.blogspot.com/2014/03/scanning-from-apple-airprint-airscan.html)`
- [Snac - Mac OSX GUI for SANE scanimage](http://www.wallner.nu/fredrik/software/snac/)
- [TWAIN Scanners in OS X Maverick (and Yosemite) | janegil.net](https://janegil.net/2014/01/twain-scanners-in-os-x-maverick/) - TWAINBridge Maverick Fix, not useful on macOS 10.11 due to SIP
- [Axel-Erfurt/Sane-OSX-Xojo: Sane Scanner GUI with Xojo](https://github.com/Axel-Erfurt/Sane-OSX-Xojo) - SANE frontend written in [Xojo](https://en.wikipedia.org/wiki/Xojo) include support of tesseract (OCR lib)
	- [News - Axel Schneider - good old music](https://goodoldsongs.jimdo.com/news/)
- [fixed : use unsupported scanner in OSX 10.11 El_Capitan | MacManus.nl](https://macmanus.nl/2015/11/10/fixed-use-unsupported-scanner-in-osx-10-11-el_capitan/)

## Automator

- [localization - How to use AppleScript’s “localized string” inside an Automator workflow - Stack Overflow](https://stackoverflow.com/questions/9345648/how-to-use-applescript-s-localized-string-inside-an-automator-workflow)

## Delete core dump files

In `/cores` folder

Only deletes core files older than 24 hours.

	find /cores -name "core.*" -ctime 1 -delete

Use cron or launchd

- [Remove hidden core dump files to restore drive space - Mac OS X Hints](http://hints.macworld.com/article.php?story=20031001203255412)

## Screens and monitors

- [MonitorControl/MonitorControl: 🖥 Control your display's brightness & volume on your Mac as if it was a native Apple Display. Use Apple Keyboard keys or custom shortcuts. Shows the native macOS OSDs.](https://github.com/MonitorControl/MonitorControl)
- [waydabber/BetterDummy: Software Dummy Display Adapter for Apple Silicon/Intel Macs to Have Custom HiDPI Resolutions.](https://github.com/waydabber/BetterDummy) - also useful for headless Macs (servers)

### Custom screen resolution or HiDPI

[OSCAR LCD Panel 1024 × 768 (HiDPI) fix](https://gist.github.com/mems/2a4b5b180a7d04c9a967)

Find screen DisplayVendorID and DisplayProductID

```sh
ioreg -l -w0 -d0 -r -c AppleDisplay
```

Or in IORegistryExplorer (`/Developer/Applications/Utilities/IORegistryExplorer.app`) or IOJones, something like `IOService:/AppleACPIPlatformExpert/PCI0@0/AppleACPIPCI/P0P2@1/IOPP/GFX0@0/NVDA,Display-B@1/NVDA/display0/AppleDisplay`

`IOService:/AppleACPIPlatformExpert/PCI0@0/AppleACPIPCI/P0P2@1/IOPP/GFX0@0/NVDA,Display-A@0/NVDA/display0/AppleBacklightDisplay` is for built-in screen on Macbook Pro.

Map to `/System/Library/Displays/Overrides/DisplayVendorID-XXXXX/DisplayProductID-YYYYY` where `XXXXX` and `YYYYY` are 1 to N hexa char

- [Turn on HiDPI Retina Mode On An Ordinary Mac - Cocoa Manifest](http://cocoamanifest.net/articles/2013/01/turn-on-hidpi-retina-mode-on-an-ordinary-mac.html)
- [macbook - Issues with Screen Scaling on External Monitor - Ask Different](http://apple.stackexchange.com/questions/149149/issues-with-screen-scaling-on-external-monitor)
- [osx - How do you enable HiDpi mode for unsupported monitors like the Dell P2815Q in Mavericks? - Ask Different](http://apple.stackexchange.com/questions/125928/how-do-you-enable-hidpi-mode-for-unsupported-monitors-like-the-dell-p2815q-in-ma)
- [macbook - Mavericks not able to use external display at full resolution - Ask Different](http://apple.stackexchange.com/questions/106933/mavericks-not-able-to-use-external-display-at-full-resolution)

- [[Guide] [10.8] Add your custom retina / HiDPI resolution for your desktop display - Tutorials (The Genius Bar) - InsanelyMac Forum](http://www.insanelymac.com/forum/topic/290097-guide-108-add-your-custom-retina-hidpi-resolution-for-your-desktop-display/)
- [[Guide] Add your custom retina / HiDPI resolution for your desktop display](http://www.tonymacx86.com/graphics/102321-guide-add-your-custom-retina-hidpi-resolution-your-desktop-display.html)
- [Adding/Using HiDPI custom resolutions](http://www.tonymacx86.com/mavericks-laptop-support/133254-adding-using-hidpi-custom-resolutions.html)
- [HOWTO: 2880x1800 Without Scaling in OS X | Page 2 | MacRumors Forums](http://forums.macrumors.com/threads/howto-2880x1800-without-scaling-in-os-x.1387363/page-2#post-15052764)
- [Investigating a high resolution / retina utility for MacBook Pro 1x and 2x modes | Gareth Jenkins](http://garethjenkins.com/2012/07/01/investigating-a-high-resolution-retina-utility-for-macbook-pro-1x-and-2x-modes/)
- [Adafruit customer service forums • View topic - Qualia Display in full res HiDPI](http://forums.adafruit.com/viewtopic.php?f=47&p=265159) and [iccir/QualiaHiDPI](https://github.com/iccir/QualiaHiDPI)
- http://www.opensource.apple.com/source/IOKitUser/IOKitUser-120.4/graphics.subproj/IOGraphicsLib.c

Icon can be change be changed in `/System/Library/Displays/Overrides/Icons.plist`.

[EDID](http://en.wikipedia.org/wiki/Extended_Display_Identification_Data) can be override with `IODisplayEDID`. See [[HOW TO] Advanced EDID Injection - Graphics Cards - InsanelyMac Forum](http://www.insanelymac.com/forum/topic/281412-how-to-advanced-edid-injection/)

## Problems

- [macOS Sierra: If your Mac restart and a message appears](https://support.apple.com/kb/PH25498?locale=en_US)
- [macOS Sierra: Use Apple Diagnostic or Apple Hardware Test](https://support.apple.com/kb/PH25696?locale=en_US&viewlocale=en_US)

### In log `org.freedesktop.dbus-system` `Service exited with abnormal code: 1`

- [#19804 ("sudo launchctl load -w /Library/LaunchAgents/org.freedesktop.dbus-session.plist" should not sudo?) – MacPorts](https://trac.macports.org/ticket/19804)
- [macos - com.apple.launchd.peruser -\> org.freedesktop.dbus-session error - Super User](https://superuser.com/questions/162238/com-apple-launchd-peruser-org-freedesktop-dbus-session-error)

### Shutdown

- `pmset -g`
- `log show --predicate 'eventMessage contains "Previous shutdown cause"' --last 24h`
- [MacBook Pro's shutting down in sleep | Discussion | Jamf Nation](https://www.jamf.com/jamf-nation/discussions/24990/macbook-pro-s-shutting-down-in-sleep)
- [How Power Nap works on your Mac - Apple Support](https://support.apple.com/en-us/HT204032)

## DSLR as a webcam

Aka camera as webcam

- [Cam Link 4K | elgato.com](https://www.elgato.com/en/gaming/cam-link-4k) - Hardware HDMI-to-USB Webcam
- [Using your Canon EOS DSLR as a webcam/capture... - Oldershaw](https://web.archive.org/web/20150104173056/http://blog.oldershaw.org/post/54830169911/using-your-canon-eos-dslr-as-a-webcam-capture)
- [How to use your DSLR as a Webcam | Crowdcast Docs](https://docs.crowdcast.io/en/articles/1935406-how-to-use-your-dslr-as-a-webcam)
- [barrabinfc/camtwist-syphon: Pipe Syphon Video to/from virtual web cam](https://github.com/barrabinfc/camtwist-syphon)
- [v002/v002-Camera-Live: Live Syphon Camera](https://github.com/v002/v002-Camera-Live)
- [Using a DSLR as a Webcam - A guide & tutorial — OBS.Live | Open Broadcaster Software Streaming Knowledge Base](https://www.obs.live/articles/2019/6/7/using-a-dslr-as-a-webcam-a-guide-amp-tutorial)
- [johnboiles/obs-mac-virtualcam: Creates a virtual webcam device from the output of OBS. Especially useful for streaming smooth, composited video into Zoom, Hangouts, Jitsi etc. Like CatxFish/obs-virtualcam but for macOS.](https://github.com/johnboiles/obs-mac-virtualcam)
- [works for me 1 time but then doesn't let me select the camera on zoom/others · Issue #102 · v002/v002-Camera-Live](https://github.com/v002/v002-Camera-Live/issues/102#issuecomment-618312892)
- [Using a Canon DSLR as a webcam on macOS with Zoom – Nicholas Sherlock](https://www.nicksherlock.com/2020/04/using-a-canon-dslr-as-a-webcam-with-zoom-us/)

- [johnboiles/obs-mac-virtualcam: Creates a virtual webcam device from the output of OBS. Especially useful for streaming smooth, composited video into Zoom, Hangouts, Jitsi etc. Like CatxFish/obs-virtualcam but for macOS.](https://github.com/johnboiles/obs-mac-virtualcam)
- [Open Broadcaster Software®️ | OBS](https://obsproject.com/)

Linux: gphoto2 -> ffmpeg -> [v4l2loopback](https://github.com/umlaeute/v4l2loopback)

## Java

- Java 8 is the only supported version which runs applets
- `/System/Library/Frameworks/JavaVM.framework/Versions/A/Commands/java` is Apple's Java version. Keep it. (`/usr/libexec/java_home` and `/usr/bin/java` point to it). See ["**Do NOT remove any content** in the JavaVM.framework"](https://superuser.com/questions/564687/how-do-i-uninstall-java6-from-mac-os-x/712783#712783)
- `/System/Library/Java/JavaVirtualMachines/` is JDK location where Apple's Java 6 is installed (still the case?)
- `/Library/Java/JavaVirtualMachines/`  default location of JDK installs
- `/usr/libexec/java_home -V` get list of installed installed JVMs

Install JDK with `sudo port install openjdk14` or download it from [JDK Builds from Oracle](https://jdk.java.net/). See also:

- [Installation of the JDK and the JRE on macOS](https://docs.oracle.com/javase/10/install/installation-jdk-and-jre-macos.htm#JSJIG-GUID-2FE451B0-9572-4E38-A1A5-568B77B146DE)
- [Java SE - Downloads | Oracle Technology Network | Oracle](https://www.oracle.com/java/technologies/javase-downloads.html)

Uninstall Oracle Java by deleting the plug-in file (JRE, for applets):

```sh
sudo rm -rf "/Library/Internet Plug-Ins/JavaAppletPlugin.plugin"
sudo rm -rf "/Library/PreferencePanes/JavaControlPanel.prefpane"
sudo rm -fr "~/Library/Application Support/Oracle/Java"
```

Uninstall Oracle Java JDK:

```sh
sudo rm -rf "/Library/Java/JavaVirtualMachines/jdk-interim.update.patch.jdk"
```

- [java - What is the difference between JDK and JRE? - Stack Overflow](https://stackoverflow.com/questions/1906445/what-is-the-difference-between-jdk-and-jre/34510731#34510731) - JRE vs JDK
- [Download Java for OS X 2015-001](https://support.apple.com/kb/dl1572?locale=en_US)
- [How do I uninstall Java on my Mac?](https://www.java.com/en/download/help/mac_uninstall_java.xml)

## macOS is Unix

And mostly POSIX-compatible

- [Some Differences between macOS and Common Unix Systems](https://web.archive.org/web/20201226003512/https://www.dyx.name/posts/macunix.html)
- [Darwin (operating system) - Wikipedia](https://en.wikipedia.org/wiki/Darwin_%28operating_system%29)
