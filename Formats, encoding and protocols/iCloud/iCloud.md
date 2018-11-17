- [Archive or make copies of your iCloud data - Apple Support](https://support.apple.com/en-us/HT204055)
- (not free) [iPhone Backup Extractor for Windows and Mac - Recover your lost data](http://www.iphonebackupextractor.com/)

## How iCloud works

- [Search · icloud](https://github.com/search?utf8=%E2%9C%93&q=icloud)
- [Switch on/off iCloud sync service](https://gist.github.com/nballotta/3881bcd662248fb93916)
- [XEP-0060: Publish-Subscribe](https://xmpp.org/extensions/xep-0060.html)
- [picklepete/pyicloud: A Python + iCloud wrapper to access iPhone and Calendar data.](https://github.com/picklepete/pyicloud/) - most advanced icloud connector
- [Taconut/Icew1nd: A smörgåsbord of useful tools for doing all sorts of cool stuff with iOS](https://github.com/Taconut/Icew1nd)
- [smpanaro/icloud-tabs: Update iCloud tabs from Chrome.](https://github.com/smpanaro/icloud-tabs) - connect to icloud server to get the list of tabs
- [ndbroadbent/icloud_photos_downloader: A command-line tool to download photos from iCloud](https://github.com/ndbroadbent/icloud_photos_downloader)
- [131/icloud-api: iCloud / cloudkit API](https://github.com/131/icloud-api) - based on pyicloud
- [reimertz/underCloud: ☁️ Use iCloud as your backup solution](https://github.com/reimertz/underCloud) - use Mobile Documents to store files (macOS only)
- [horrorho/InflatableDonkey: iOS9/ iOS10/ iOS11 iCloud backup retrieval proof of concept](https://github.com/horrorho/InflatableDonkey)
- [Xenomega/iCloudLib: iCloudLib provides access to various Apple iCloud web services such as devices/tracking, contacts, etc.](https://github.com/Xenomega/iCloudLib)
- [Neal/FindMyiPhone: A PHP class for the Find My iPhone service by iCloud®.](https://github.com/Neal/FindMyiPhone)
- [tylerhall/sosumi: A PHP client for Apple's Find My iPhone service. This allows you to programmatically retrieve your phone's current location and push messages (and an optional alarm) to the remote device.](https://github.com/tylerhall/sosumi)
- [albeebe/PHP-FindMyiPhone: PHP class to locate, play sounds, and lock iOS devices](https://github.com/albeebe/PHP-FindMyiPhone)

- [meeee/pushproxy: A man-in-the-middle proxy for iOS and OS X device push connections](https://github.com/meeee/pushproxy)

Infos about iCloud and iOS

- [Finally! Sync your Address CardDav in OSX 10.6 Snow Leopard | MacRumors Forums](https://forums.macrumors.com/threads/finally-sync-your-address-carddav-in-osx-10-6-snow-leopard.1265730/)
- [iOS Reverse Engineering](http://ios-rev.tumblr.com/)
- [prabhu/iCloud: How iCloud.com works?](https://github.com/prabhu/iCloud)
- [macos - iCloud in OS X Implementation - which protocol does it use? - Ask Different](https://apple.stackexchange.com/questions/54762/icloud-in-os-x-implementation-which-protocol-does-it-use)
- [macos - Can the iCloud sync progress be observed? - Ask Different](https://apple.stackexchange.com/questions/68349/can-the-icloud-sync-progress-be-observed)
- [ICloud - dmfswiki](http://dmfs.org/wiki/index.php?title=ICloud)
- [Elcomsoft Phone Breaker | Elcomsoft Co.Ltd.](https://www.elcomsoft.com/eppb.html)
- [TCP and UDP ports used by Apple software products - Apple Support](https://support.apple.com/en-us/HT202944)

Old (not compatible with protocols used by recent iOS version):

- [horrorho/LiquidDonkey: iCloud backup download tool (Java)](https://github.com/horrorho/LiquidDonkey)
- [jurriaan/Ruby-iCloud: A Ruby utility for connecting to Apple iCloud services](https://github.com/jurriaan/Ruby-iCloud)
- [hackappcom/iloot: OpenSource tool for iCloud backup extraction](https://github.com/hackappcom/iloot)

## Events and contacts

Via cal and card DAV

[server id] like 05 (01 to 10)
[long string] like 91C0A18D-8889-44E2-8DB6-5774C9FCA6F2
[iCloud ID] like 1325673149


	https://p[server id]-caldav.icloud.com:443/[iCloud ID]/calendars/notification/
	https://p[server id]-caldav.icloud.com:443/[iCloud ID]/calendars/tasks/
	https://p[server id]-caldav.icloud.com:443/[iCloud ID]/calendars/inbox/
	https://p[server id]-caldav.icloud.com:443/[iCloud ID]/calendars/home/
	https://p[server id]-caldav.icloud.com:443/[iCloud ID]/calendars/work/
	https://p[server id]-caldav.icloud.com:443/[iCloud ID]/principal/
	https://p[server id]-caldav.icloud.com:443/[iCloud ID]/wcs/
	
	https://p[server id]-contacts.icloud.com:443/[iCloud ID]/carddavhome/card/[long string].vcf
	
	https://p[server id]-contacts.icloud.com:443/[iCloud ID]/carddavhome/addressbook/
	
	https://p[server id]-contactsws.icloud.com/co/mecard/?dsid=[iCloud ID]
	
	https://p[server id]-caldav.icloud.com/[iCloud ID]/calendars/91C0A18D-8889-44E2-8DB6-5774C9FCA6F2/70aaeba9-9d4d-450b-bcf2-4bec2153094e.ics


AppleID:Passwort
BASIC REALM
(base64, padded with "=" ?)

## App Files

If "Document & Data" is enabled in iCloud Sync

	~/Library/Mobile Documents/

iCloud drive files: `~/Library/Mobile Documents/com~apple~CloudDocs`

## Preferences

Bookmarks, opened tabs, etc.

If Safari is enabled in iCloud Sync

	~/Library/SyncedPreferences/com.apple.Safari.plist
	~/Library/SyncedPreferences/com.apple.syncedpreferences.plist

This folder is backup by TimeMachine

## Bookmarks and tabs

And reading list (stored as bookmarks)

`defaults write com.apple.Safari IncludeInternalDebugMenu 1` to activate debug menu in Safari, then in Safari Debug > Sync iCloud History

If Safari is enabled in iCloud Sync. Updated by `/System/Library/CoreServices/SafariSupport.bundle/Contents/MacOS/SafariBookmarksSyncAgent`

	~/Library/SyncedPreferences/com.apple.Safari.plist
	~/Library/Safari/Bookmarks.plist
	# SQLite updated when iCloud is sync
	~/Library/Safari/CloudTabs.db

The field `position` of table `cloud_tabs` in `CloudTabs.db` is deflate (zlib) of JSON like:

	{"sortValues":[{"changeID":0,"sortValue":2000,"deviceIdentifier":"72E06CBB-9C58-479B-AD70-92BE116AE0E5"}]}

You can export then decode with `openssl zlib -d < position.dat`.
See `-[NSData safari_dataByDecompressingData]` in `/System/Library/PrivateFrameworks/SafariCore.framework/SafariCore`

The field system_fields is binary [PList](PList) using [`NSKeyedUnarchiver`](NSKeyedArchiver) format

Order in the database doesn't match the order of tabs are opened. No logical order. Ex: tab 4, tab 5, tab 1, tab 6, tab 2, tab 7, tab 3

Device name should match:

	scutil --get LocalHostName
	scutil --get ComputerName

See [Generate a markdown links list from iCloud tabs](https://gist.github.com/mems/2c96233708c6b5b44ed1a26cb0ec5a0e)

The history timestamp `visit_time` is seconds from 2001-01-01 00:00:00

Tab title with "Favoris" (fr) / "Favorites" (en) by the URL, is often a PDF document

	# bookmarks to JSON using only
	plutil -convert xml1 -o - ~/Library/Safari/Bookmarks.plist | php('php://stdin','SimpleXMLElement',LIBXML_NOCDATA));"

- [Rebuilding iCloud Bookmarks | Sheep Systems](http://www.sheepsystems.com/files/support_articles/bkmx/rebuilding-icloud-bookmarks.html)
- [safari - iCloud tabs only shows one iOS device at a time - Ask Different](https://apple.stackexchange.com/questions/137029/icloud-tabs-only-shows-one-ios-device-at-a-time/275457#275457)
- [josh-/CloudyTabs: CloudyTabs is a simple menu bar application that lists your iCloud Tabs.](https://github.com/josh-/CloudyTabs) - use Safari local file
- [sindresorhus/icloud-tabs: Get the iCloud tabs for all synced devices (macOS)](https://github.com/sindresorhus/icloud-tabs) - use Safari local file
- [toddbluhm/CloudyTabs: CloudyTabs is a simple menu bar application that lists your iCloud Tabs.](https://github.com/toddbluhm/CloudyTabs) - use Safari local file
- [rlictd/rlictd.py at master · anoved/rlictd](https://github.com/anoved/rlictd/blob/master/rlictd.py) - use AppleScripts to add item to ReadList, use Safari local file
	Use [anoved/iCloudTabsReader: Python module to get list of iCloud Tabs currently known to the host Mac.](https://github.com/anoved/iCloudTabsReader)
- https://addons.mozilla.org/en-US/firefox/addon/icloud-bookmarks/

## Photo Stream

	~/Library/Application Support/iLifeAssetManagement/assets/sub/[subfolder]/*.png|*.jpg

Where subfolder call something like 013184d3f181aa175db7e48b08817861eff8cac25a (long hexa name).

## Backups

- [hackappcom/iloot · GitHub](https://github.com/hackappcom/iloot)
- [horrorho/LiquidDonkey · GitHub](https://github.com/horrorho/LiquidDonkey)