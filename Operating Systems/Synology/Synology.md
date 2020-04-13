- [Cross-compilation pour Synology - Blog Benjamin BALET](http://benjamin-balet.info/multimedia/synology/cross-compilation-pour-synology/)
- `inotify` [HOWTO: Show me the Latest Files - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=56439)
- [Les serveurs NAS Synology - /!\\ Lire page 1 SVP /!\\ \[Topic R+\] - Réseaux - Réseaux grand public / SoHo - FORUM HardWare.fr](https://forum.hardware.fr/hfr/reseauxpersosoho/Reseaux/serveurs-synology-page-sujet_5497_1.htm)

## Hardware

	cat /proc/cpuinfo | more
	lscpu
	uname --machine
	dmesg

- [What kind of CPU does my Synology NAS have?](https://www.synology.com/en-global/knowledgebase/DSM/tutorial/General/What_kind_of_CPU_does_my_NAS_have)

### Disk info

	sudo smartctl -a /dev/sdX | grep "^SATA"
	dmesg | grep -i sata | grep 'link up'
	sudo hdparm -I /dev/sdX

- [Is DS1815+ Native SATA III - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=95139) - SATA version and speed repartition (first ones support higher speed)
- [Mounting old Synology volumes in new hardware - Code, Rinse, Repeat](https://coderinserepeat.com/2017/05/13/mounting-existing-synology-volumes/)

### Replace disk

Aka repair disk

RAID mirror disks: remove a disk and rebuild volume

RAID without mirror or one disk: clone disk with `dd`. See [Clone disk](../Command%20line/Command%20line%20(Unix).md#clone-disk)

- [Replace Drives to Expand Storage Capacity | Synology Inc.](https://www.synology.com/en-us/knowledgebase/DSM/help/DSM/StorageManager/storage_pool_expand_replace_disk)
- [Can I use dd to upgrade 1-bay synology NAS to bigger HD? - Super User](https://superuser.com/questions/898367/can-i-use-dd-to-upgrade-1-bay-synology-nas-to-bigger-hd)
- [Adding a new disk drive to a Synology 2-bay drive - Super User](https://superuser.com/questions/575408/adding-a-new-disk-drive-to-a-synology-2-bay-drive)
- [Upgrading disks in a RAID1 Synology 2-bay drive - Super User](https://superuser.com/questions/469325/upgrading-disks-in-a-raid1-synology-2-bay-drive)
- [How to upgrade HDD for one bay model - SynologyWiki](https://web.archive.org/web/20160304194224/http://forum.synology.com/wiki/index.php/How_to_upgrade_HDD_for_one_bay_model)
- [Synology two-bay NAS with existing data? - Super User](https://superuser.com/questions/1060602/synology-two-bay-nas-with-existing-data)
- [Etendre Une Partition Sur Un Nouveau Disque Dur (Non Raid) - Installation, Démarrage et Configuration - NAS-Forum](http://www.nas-forum.com/forum/topic/44795-etendre-une-partition-sur-un-nouveau-disque-dur-non-raid/)
- [How can I recover data on my Synology NAS using a PC? | Synology Inc.](https://www.synology.com/en-us/knowledgebase/DSM/tutorial/Storage/How_can_I_recover_data_from_my_DiskStation_using_a_PC)

## Security

- [Hardening access to your Synology Diskstation, be prepared – Q&D](https://www.wijngaard.org/hardening-access-to-your-synology-diskstation-and-prepare/)

### TLS Certificates

- `/usr/syno/sbin/syno-letsencrypt-vv renew-all` `/usr/syno/etc/certificate/_archive/sP0YM1/cert.pem`
- [Certificate | Synology Inc.](https://www.synology.com/en-us/knowledgebase/DSM/help/DSM/AdminCenter/connection_certificate)
- [Challenge Types - Let's Encrypt - Free SSL/TLS Certificates](https://letsencrypt.org/docs/challenge-types/)
- [Reparlons de Let’s Encrypt - LinuxFr.org](https://linuxfr.org/news/reparlons-de-let-s-encrypt#lauthentification-http-01)

## SSH

root is the admin user

Super admin access in DSM6: log with an admin user, then use `sudo su` or `sudo -i` then use your password

- [Service & Support - Synology - Network Attached Storage (NAS)](https://www.synology.com/en-us/knowledgebase/DSM/tutorial/General/What_is_the_username_and_default_password_for_accessing_my_Synology_Product_via_Telnet_SSH)
- [nas - How do I change the root password on my Synology Rackstation? - Super User](http://superuser.com/questions/984521/how-do-i-change-the-root-password-on-my-synology-rackstation)
- [Synology DSM root password for ssh | Primal Cortex's Weblog](https://primalcortex.wordpress.com/2012/08/25/synology-dsm-root-password-for-ssh/)
- [Howto: (re-)Enable SCP/SSH Login on Synology DSM 6.0 for non admin users [UPDATE] « Beyond Technology](http://andidittrich.de/2016/03/howto-re-enable-scpssh-login-on-synology-dsm-6-0-for-non-admin-users.html)

### Password less login

Client side:

```sh
# Generate you public key if not already exist
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Server side (NAS):

```sh
mkdir ~/.ssh
touch ~/.ssh/authorized_keys
# copy content of your public key (client: ~/.ssh/id_rsa.pub)
# Fix permission on home directory (remove group and everyone write permission)
chmod 755 ~
# Fix permission of authorized keys file and parent directory
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

- [Configure Synology NAS SSH Key-based authentication](https://blog.aaronlenoir.com/2018/05/06/ssh-into-synology-nas-with-ssh-key/)
- [Adding public key to ~/.ssh/authorized_keys does not log me in automatically - Stack Overflow](https://stackoverflow.com/questions/6377009/adding-public-key-to-ssh-authorized-keys-does-not-log-me-in-automatically/6377073#6377073)
- [How to access files on Synology NAS via FTP | Synology Inc.](https://www.synology.com/en-us/knowledgebase/DSM/tutorial/File_Sharing/How_to_access_files_on_Synology_NAS_via_FTP#t2_5) - "SFTP offers secure file transfer to DSM users without the need of passwords, and reduces the leakage risk of user credentials"

## TimeMachine

Create a shared folder, with permissions, `Control Panel > File Services > Mac File Service > Time Machine`. This folder will be available in TimeMachine backup disks

## Shared and drop box

Inspiration of OSX: [OS X Yosemite: Share files with others who use your Mac](https://support.apple.com/kb/PH18716?locale=en_US)

`domain/index.cgi?launchApp=SYNO.SDS.App.FileStation3.Instance&launchParam=openfile%3D${ENCODED_PATH}`, where `ENCODED_PATH` is twice URI encoded the path -> `/Media/Videos/TV Shows/` gives `%252FMedia%252FVideos%252FTV%2520Shows%252F`
`launchParam` value is a URI encoded key value pairs (where values are also URI encoded)

- [Upload files on your Synology with a link and no access rights – Synoguide](https://synoguide.com/2016/04/15/upload-files-on-your-synology-with-a-link-and-no-access-rights/)

## Notifications

- [Support for "Custom Notifications" - Synology Forum](https://forum.synology.com/enu/viewtopic.php?f=3&t=92727)

## Applications

### Applications files & data

- package files (installed) `/var/packages/$APP_NAME/etc -> /usr/syno/etc/packages/$APP_NAME`
- app files (config, etc.) `/var/packages/$APP_NAME/target -> /volumeX/@appstore/$APP_NAME` and `/var/services/web/$APP_NAME`

- [Synology - Move Application Between Volumes - McLean IT Consulting](https://www.mcleanit.ca/blog/synology-move-application-volumes/)

### Download Station

It use transmission daemon for bittorrent downloads (`/volumeX/@download/transmissiond.log`)

**Set the temporary location on a fast volume (Download Station > Settings > General > Temporary destination, `/var/services/download` symlink to `/volumeX/@download`).** The download destination folder doesn't need to be on a fast drive.

About temporary location:

- the temporary destination keeps a copy of every single file/folder you are seeding. It could be hardlinks, but it's not (check with `du -hc --max-depth=0 /volume1/@download /$DOWNLOAD_DESTINATION`).
- files (in temporary location) will be deleted by download station, once torrents are deleted (from the Download Station UI)
- downloaded data is moved from temporary location to the destination folder, once the task is marked as terminated (no more sharing). See [Download station does not delete temp files - Synology Forum](https://forum.synology.com/enu/viewtopic.php?f=10&t=57517)
- you can move, modify or delete the files in destination folder, this will not impact the currently seeding tasks. (if it was hardlinks, you couldn't modify it without corrupt sharing task)

`/usr/bin/psql download` `download_queue`

[psql](https://www.postgresql.org/docs/current/static/app-psql.html) should be exec as root user (sudo or via task manager, user: root)

	/usr/bin/psql -t -A -U postgres -d download -c "SELECT filename from download_queue"

	#!/bin/ash
	/usr/bin/psql -t -A -U postgres -d download -c "DELETE from download_queue WHERE total_size = current_size and (seeding_elapsed >=176400 or total_size <= total_upload)"
	find /volume1/@download/ -mmin +2940 -exec rm -rf {} \;

- `mkdir -p /volume1/Downloads/incomplete/@download; sudo mount --bind /var/services/download /volume1/Downloads/incomplete/@download; mount -o remount,ro,bind /volume1/Downloads/incomplete/@download` (to unmout: `sudo umount -lf /volume1/Downloads/incomplete/@download`) to reach incomplete files. It's mounted inside `incomplete`, this allow to restrict access to the mount point (ex: administrators only).
- `/usr/syno/etc/packages/DownloadStation/download/settings.json` is deleted each time a torrent starts. See `/var/packages/DownloadStation/scripts/start-stop-status`. See [\[DSM5.0\] Execute script after torrent finishes - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=88918#p334755) and [Script to run when downloadstation is done - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=96553)

Re check torrents, aka resume torrent:

- [set up torrents which had been downloaded previously - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=41802#p169052)
- [Recuperer l'espace utilisé par download station et ranger ses downloads sans perdre le seed/upload - Download Station - NAS-Forum](http://www.nas-forum.com/forum/topic/54596-recuperer-lespace-utilis%C3%A9-par-download-station-et-ranger-ses-downloads-sans-perdre-le-seedupload/)

- [Auto clean & delete torrents from Downloadstation. - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=70586)
- [The SBS Guys – Actrix Networks » Blog Archive » Synology Download Station – RSS Feed stuck in Status ‘Updating’](http://thesbsguy.com/2013/08/09/synology-download-station-rss-feed-stuck-in-status-updating/)
- [A CLI for Synology Download Station](http://downloadstation.jroene.de/) http://downloadstation.jroene.de/downloadstation
- https://gitorious.org/synology/synology-script/source/master?p=synology:synology-script.git;a=summary
- [Optimize Your Synology NAS for Downloading | kvz.io](http://kvz.io/blog/2011/02/28/optimize-your-synology-for-downloading/)
- [\[Tuto\] Synology-Se proteger des déconnexions VPN ou Coupure de courant. - Forum de t411.li](http://forum.t411.li/index.php?p=/discussion/65956/tuto-synology-se-proteger-des-deconnexions-vpn-ou-coupure-de-courant.)
- [SynoBoost - Download Station Search Modules for Synology NAS](http://www.synoboost.com/)

#### Blocklist

- [Synology Download Station bittorrent blocklist | MikeBeach.org](https://mikebeach.org/2013/01/03/synology-download-station-bittorrent-blocklist/)
- [IP block list on Download Station - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=83926)
- [Resolu - Download Station Et Blocklist - Download Station - NAS-Forum](http://www.nas-forum.com/forum/topic/39969-resolu-download-station-et-blocklist/)
- [Bluetack block lists are now pay only - Free alternatives? - Transmission](https://forum.transmissionbt.com/viewtopic.php?t=15652)
- https://github.com/b0red/Synology/blob/master/UpdateBlocklist.sh
- [How to Add a Blocklist to Synology Download Station \[Tutorial\]](https://hipsterpixel.co/2017/01/28/how-to-add-a-blocklist-to-synology-download-station-tutorial/)
- (DSM 4) [How to enable the IPfilter blocklist in Synology Download Station’s aMule client | MikeBeach.org](https://mikebeach.org/2013/01/03/how-to-enable-the-ipfilter-blocklist-in-synology-download-stations-amule-client/)
- System wild [DiskStation Manager - Knowledge Base | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/help/DSM/AdminCenter/connection_security_autoblock)
- https://forum.synology.com/enu/viewtopic.php?f=38&t=83926&sid=f0d34ec4917245bcdd8124d72e36124a&start=15#p372971
- Block IPs for the torrent client: [Download Station: IP Blocklist installation – MylesFreeman.com](http://www.mylesfreeman.com/2014/08/25/download-station-ip-blocklist-installation/)

### Move applications

- [Synology - Move Application Between Volumes - McLean IT Consulting](http://www.mcleanit.ca/blog/synology-move-application-volumes/)
- [Script for moving packages on a synology disk station from one volume to another - EXPERIMENTAL!](https://gist.github.com/nobodypb/fc3e70b535bcd95b5de7659d6fbda434)

### MariaDB

	/var/packages/MariaDB10/target/mysql/<servername>.err 

Config file

	# see /usr/local/mariadb10/etc/mysql/my.cnf
	# Note: /var/packages/MariaDB10/etc/ -> /usr/syno/etc/packages/MariaDB10 and /usr/local/mariadb10/etc/mysql/my.cnf -> /volumeX/@appstore/MariaDB10/usr/local/mariadb10/etc/mysql/my.cnf
	sudo touch /var/packages/MariaDB10/etc/my.cnf
	sudo chown mysql:mysql /var/packages/MariaDB10/etc/my.cnf

By default MariaDB10 runs on port **3307**, where for MariaDB5.5 the port was 3306 (mysql default). To change the port, create a custom `my.cnf` and add: **Note: this seem not work anymore (`my.cnf` as not more effect on it)**

	[client]
	port = 3306
	
	[mysqld]
	port = 3306

Log file / users login attempts:

	[mysqld]
	general_log_file = /var/log/mysql/mysql.log
	general_log = 1
	expire_logs_days = 7
	max_binlog_size = 100M

	sudo chown system:log /var/log/mysql
	sudo chown mysql:mysql /var/log/mysql/mysql.log

See also, set in Web Station > PHP parameters > Advanced parameters > Extensions :

- `mysql.default_port`: 3307
- `mysql.default_socket`: `/run/msqyld/mysqld10.sock`

Use values from MariaDB 10 application

### DSM Audio player

Support `.m3u` (but not `.m3u8`)
Support only relative paths (start with `./` or `../`, not `/volumeX/`)

### Restart service / daemon

```sh
synoservicectl  --restart pkgctl-MariaDB10
```

```sh
synoservice --help
synoservicecfg --list
```

### Create application

GUI ExtJS

- [Package Developer Guide | Synology DSM6.0 Developer Guide](https://developer.synology.com/developer-guide/index.html)
- [Developers | Synology Inc.](https://www.synology.com/en-us/support/developer)
- [Rutorai/syno-library](https://github.com/Rutorai/syno-library), [Home · Rutorai/syno-library Wiki](https://github.com/Rutorai/syno-library/wiki) and [spksrc/spk at master · SynoCommunity/spksrc](https://github.com/SynoCommunity/spksrc/tree/master/spk) example app with embed app
- https://github.com/SynoCommunity/spksrc/blob/master/spk/debian-chroot/src/app/debian-chroot.js - example file for GUI
- [vletroye/Mods: Mods can be used to Create or Open/Edit and Generate packages for Synology](https://github.com/vletroye/Mods)
- [Init_3rdparty Skript und Sammlung von 3rd-Party Erweiterungen](http://www.synology-forum.de/showthread.html?3949-Init_3rdparty-Skript-und-Sammlung-von-3rd-Party-Erweiterungen)
- [3rd Party Packages - NAS-Forum](http://www.nas-forum.com/forum/forum/209-3rd-party-packages/)
- [CMJ Blog](http://blog.cmj.tw/SynologyApp.htm) - Synology 3rd-Party APP
- [Кросс-компиляция и сборка пакета под Synology DSM / Хабрахабр](https://habrahabr.ru/post/271011/)
- [SynoCommunity/spksrc: Cross compilation framework to create native packages for the Synology's NAS](https://github.com/SynoCommunity/spksrc)
- [SynoCommunity](https://synocommunity.com/packages)
- [syslogic.io ● Synology DSM: Multilingual 3rd Party Packages](https://blog.syslogic.io/2013/02/synology-dsm-detect-current-user-language-php)
- [Is there any Web UI API ? - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=121038)
- [filebot/filebot-node: FileBot Node is a client-server application that'll allow you to run filebot commands](https://github.com/filebot/filebot-node) - Package use NodeJS
- [Package Center specifications · SynoCommunity/spksrc Wiki](https://github.com/SynoCommunity/spksrc/wiki/Package-Center-specifications)
- [UI Develop · SynoCommunity/spksrc Wiki](https://github.com/SynoCommunity/spksrc/wiki/UI-Develop)
- [rednoah/ant-spk: Ant Task for creating SPK packages for Synology NAS](https://github.com/rednoah/ant-spk)
- `dsmuidir` and `SYNO.SDS.AppWindow`
- [Synology package files - SynologyWiki](https://web.archive.org/web/20160318143845/http://forum.synology.com/MediaWiki/index.php?title=Synology_package_files)
- [Cross-compilation and assembly of a packet under Synology DSM — IT daily blog, news, magazine, technologies](http://developers-club.com/posts/271011/)
- [WebUI module for Bitcoin - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=42401)
- [How to Create a SPK for Synology DSM to Distribute your LAMP | Amigo's Technical Notes](https://amigotechnotes.wordpress.com/2014/05/17/how-to-create-a-spk-for-synology-dsm-to-distribute-your-lamp/)
- `https://NAS:5001/webman/index.cgi?launchApp=$APP_ID` where `$APP_ID` is like `SYNO.SDS.AudioStation` or `SYNO.SDS.App.FileStation3.Instance` (see app JSON `/config` file for `"type":"app"`). See also [Application Portal | Synology Inc.](https://www.synology.com/en-us/knowledgebase/DSM/help/DSM/AdminCenter/application_appportalias)
- https://github.com/PrometeoFX/fire/blob/master/synoSDSjslib/sds.js [ecoreos/dsm6theme](https://github.com/ecoreos/dsm6theme) (`webman/*`) - files from DSM?
- [Search · SYNO.SDS.AppWindow](https://github.com/search?p=9&q=SYNO.SDS.AppWindow&type=Code&utf8=%E2%9C%93)

Dev environnement and tools:

- Install DSM on any harware with XPEnology (bootloader)
	
	- [Loader Releases - XPEnology Community](https://xpenology.com/forum/forum/30-loader-releases/)
	- [DSM 6.x.x Loader - DSM 6.x - XPEnology Community](https://xpenology.com/forum/topic/6253-dsm-6xx-loader/)
	
	[Synology Web Assistant](http://find.synology.com/) or Could need to use Synology Assistant [Download Center | Synology Inc.](https://www.synology.com/en-us/support/download)
	
	- [Create a Synology VM with XPEnology | iThinkVirtual™](https://ithinkvirtual.com/2016/04/30/create-a-synology-vm-with-xpenology/)
	- [Xpenology, installer un serveur Synology DSM 6 - Sky-Future](https://www.sky-future.net/2016/11/28/xpenology-installer-serveur-synology-dsm-6/)
	- [XPEnology (loader 1.02b) - DSM 6.1 on VMware Workstation Pro 12 (tutorial) - YouTube](https://www.youtube.com/watch?v=Si9Y1HNhYrI)
	- [en:building_xpenology \[XPEnology project\]](http://xpenology.com/wiki/en/building_xpenology)
- [Synology Open Source Project download | SourceForge.net](https://sourceforge.net/projects/dsgpl/)

### Subtitles with Multimedia Server App

`avi=video/x-ms-video,wav=audio/x-wav,str=text/srt,sub=plain/text`
`<VideoProfile container="mkv" codec="h264,mpeg4,mpeg2video" audioCodec="aac,ac3,mp3,dca" subtitleFormat="srt,''"/>`

text/x-subviewer
application/x-subviewer

- inject subtitles in MP4 or MKV
- `/var/packages/MediaServer/target/etc/initall.xml`, `http://192.168.1.4:50001/desc/device.xml`
- additional header `CaptionInfo.sec` or list *.srt files in directory too.
	* https://github.com/thibauts/node-upnp-mediarenderer-client/issues/6
	* https://sourceforge.net/p/mediatomb/patches/21/
	* [RS, external subtitles, DLNA and Samsung Smart TVs - DVBViewer Recording Service - DVBViewer community forum](http://www.dvbviewer.tv/forum/topic/55799-rs-external-subtitles-dlna-and-samsung-smart-tvs/)
- [TV DLNA COMPATIBILITY - LG LED INFINIA LE5500 - Synology Forum](https://forum.synology.com/enu/viewtopic.php?p=124471#p124471)
- http://www.nas-forum.com/forum/topic/34185-ds212j-freebox-upnp-et-sous-titres/
- http://blog.lesite.us/freebox-synology-activer-le-support-des-sous-titres-en-upnp.html
- [Solved: Re: Streaming External Subtitle Files (*.srt) - Sony's Community Site](https://community.sony.com/t5/Television-General/Streaming-External-Subtitle-Files-srt/m-p/253043/highlight/true#M5613)
- [Support des sous-titres avec DLNA Media Server + BubbleUPNP + Freebox Player - Tutorials - NAS-Forum](http://www.nas-forum.com/forum/topic/48818-support-des-sous-titres-avec-dlna-media-server-bubbleupnp-freebox-player/)
- http://dev.freebox.fr/bugs/index.php?do=details&action=details.addvote&task_id=12171
- [Accessing video/audio from a computer with a Freebox (using UPnP) | # cd /scratch](https://yeupou.wordpress.com/2012/10/14/accessing-videoaudio-from-a-computer-with-a-freebox-using-upnp/)
- [Writing profiles for DLNA devices... - Plex Forums](https://forums.plex.tv/discussion/73702)
- [dlna-http-server.js](https://gist.github.com/thibauts/5f5f8d8ce6566c8289e6)
- [Support des sous-titres avec DLNA Media Server + BubbleUPNP + Freebox Player - Tutorials - NAS-Forum](http://www.nas-forum.com/forum/topic/48818-support-des-sous-titres-avec-dlna-media-server-bubbleupnp-freebox-player/#comment-1319283655) and [rw_grim / docker-bubbleupnpserver — Bitbucket](https://bitbucket.org/rw_grim/docker-bubbleupnpserver)
- [Working DLNA Profiles - Plex Forums](https://forums.plex.tv/discussion/73703/working-dlna-profiles)

Freebox Mini Server: 

	WebSerOpen: /desc/device.xml, agent=Linux/2.6 UPnP/1.0 fbxlanbrowser/1.0

Freebox TV 4K:

	WebSerOpen: /desc/device.xml, agent=Android/5.0.2 UPnP/1.0 Cling/2.0
	uuid:00113252-18ab-0011-ab18-ab1852321100:urn:upnp-org:serviceId:ContentDirectory:GetSortCapabilities
	CDS_GetSortCapabilities,
	uuid:00113252-18ab-0011-ab18-ab1852321100:urn:upnp-org:serviceId:ContentDirectory:Browse
	ClientInfo: UserAgent:Android/5.0.2 UPnP/1.0 Cling/2.0, LoadProfile = Android Device, From:192.168.1.20

Freebox TV 4K (Android TV) MediaPlayer: use Stagefright, is the "New media framework that supports local file playback and HTTP progressive streaming" and Cling "Java/Android UPnP library and tools"

profileName: GPlayer

`/var/packages/MediaServer/target/etc/agent.conf` (need to restart package)

- `xmres`
- `transwav` : transcodage audio en WAV ?
- `transpcm` : transcodage audio en PCM ?
- `xalbart` : x album art...
- `revimgres`
- `xvcover`
- `transmkv` : transcodage MKV ??
- `trans_aac_copy` : transcodage audio AAC ?
- `trans_ac3_copy` : transcodage audio AC3 ?
- `videoalbart` : vidéo album art...
- `videosrt` : transmettre comme sous-titre les fichier SRT du même nom que la vidéo
- `photowithxlthumb` : aperçu des photo en grand format
- `videosubtitleitem` : visibilité des fichiers les sous titres dans l'explorateur
- `photoforcejpegpn`
- `xlibdlnamodule`
- `photoforcebgthumb` : toujours définir un background pour les aperçu de photo (pb de transparence) ?
- `customizesymbol`
- `origcover`
- `sendvsmetadata` : envoyer les métadonnées VideoStation
- `videowithext` : ajouter l'extension des vidéos dans leur nom
- `videocover_jpeg_sm` : vignettes en JPEG basse résolution ?
- `special_pcm_mimetype`
- `xpvsubtitle`
- `send_photo_thumb_size` : envoyer les dimensions des aperçu de photos ?
- `xkillvte`

More ?

- `roku`
- `musiconly`
- `wdtvlive`
- `samsungtv`
- `transmp3`

## Reverse proxy

- [Reverse Proxy sur Nas Synology et SSL - La Domotique de Sarakha63](http://sarakha63-domotique.fr/reverse-proxy-sur-nas-synology-ssl/)

## `dms.dmslog` file

DLNA debug log file

Rename `dms.dmslog` to `dms.tar.gz`

## Disk, file system, files

- `/var/packages/$APP_NAME`

### List files

Create a planified task

	find /volume3/Media -type f ! -path '*/@eaDir/*' ! -name '*@SynoResource' ! -name '*@SynoEAStream' ! -name '.DS_Store' > /volume2/Backups/medialist.txt

### Special shares

Created automatically, can't be renamed

By default some folder `homes`, `web`, `docker`, `web` are not visible. Set permission to RW (Read Write) to change the visibility

- `homes`
- `web` when Web Station is installed
- `docker` when Docker is installed
- `photo` when Audio Station is installed
- `music` when Video Station is installed
- `video` when Video Station is installed

To change the location, you need to 

#### Media folders

Create a trigger task (in Task scheduler):

User: root
Event: boot-up

	mount --bind /volume3/Media/Music /volume1/music
	mount --bind /volume3/Media/Pictures /volume1/photo
	mount --bind /volume3/Media/Videos /volume1/video

- [Change "music" folder - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=18976)
- [Change folders for Synology media server - King Foo](http://www.king-foo.com/2010/06/change-folders-for-synology-media-server/)
- [Synology Ds411j : Journal de bord J+6 - Mes NAS mes Données et Moi](https://sites.google.com/site/mesnasmesdonneesetmoi/student-of-the-month/synologyds411jjournaldebordj6)

### Special folders

- `*/@eaDir`: metadata (thumbnails of files) for iTunes Server (media indexation)
- `@download` used by Download Station as temporary folder (Can be changed Download Station > Settings > General)
- `@img_bkp_cache`
- `@database` used by MariaDB to store mysql databases
- `@afpd.core`
- `@aquota.user`
- `@aquota.group`
- `@backup.cgi.core`
- `@groupsettings.c.core`
- `@cloudsync`
- `@php.core`
- `@quarantine`
- `@smbd.core`
- `@syncd.core`
- `@SYNO.Core.Packa.core`
- `@synopkg.core`
- `@synotifyd.core`
- `@webdav`
- `@autoupdate`
- `@S2S`
- `@spool`
- `@synoavscan.core`
- `@SYNO.FileStatio.core`
- `@synoquota.db`
- `@syslog-ng.core`
- `@vtestreaming.cg.core`
- `@appstore` installed applications files
- `@tmp`
- `@img_bkp_cache`: used by Hyper Backup to store local cache
- `@syslog-ng.core`
- `@docker`
- `@cloudstation`
- `@optware`
- `@postfix`

- [Literati Tech: Those Annoying @eaDir Files (Synology DS210j NAS)](http://literatitech.blogspot.fr/2011/06/those-annoying-eadir-files-synology.html)
- [DSM: Move apps like AudioStation, CloudStation or PhotoStation to a different volume U-Labs](https://translate.googleusercontent.com/translate_c?act=url&depth=1&hl=en&ie=UTF8&prev=_t&rurl=translate.google.com&sl=auto&tl=en&u=https://u-labs.de/portal/dsm-apps-wie-audiostation-cloudstation-oder-photostation-auf-ein-anderes-volumen-verschieben/&usg=ALkJrhhBj5BQUp2YzWsKQ9r1lgCf6EendQ)
- [Move a package to another volume? - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=69529#p282313)
- [How to move applications from one volume to another on Synology – Costigator](http://costigator.com/uncategorised/how-to-move-applications-from-one-volume-to-another-on-synology/)
- `grep -R volume1 *` `sed -i "s/volume1/volume2/" <file_name>`

### Paths

`/dev/md0` is the DSM install partition (internal flash ~2.3GB)
`/dev/md1` is swap file partition (~2GB)
`/dev/mdX` where `X` is >=2, array volume

Drives: `/dev/sda`, `/dev/sdb`, `/dev/sdc`, etc. (partitions for the first disk: `/dev/sda` → `/dev/sda1`, `/dev/sda2`, etc.)

- RAID: `cat /proc/mdstat`, `sudo mdadm --detail --scan`
- mounted volumes: `cat /proc/mounts`, `df -h`
- disk and partitions: `cat /proc/partitions`
- Volume groups: `sudo vgdisplay -v`
- Volume `/volumeX`

- [Synology](https://github.com/midenok/hardware/wiki/Synology)

## Media index

TODO script: create file list from DB with mtime, create file list from Disk with mtime: compare added, deleted, updated files and call `synoindex` (see also `synoindexd`, `synoindexscand` and `/var/spool/syno_indexing_queue*`) or use inotify

	# to re-index path or dir
	# Should in "package" dir ex for video "/volume1/video"
	synoindex -R /volume1/video/<path>

- [synology [Clemens Wacha]](http://wacha.ch/wiki/synology)
- [Synology – automatic indexing via synoindex | naschenweng.info](http://www.naschenweng.info/2010/02/13/synology-automatic-indexing-via-synoindex/)
- [More on the Synology NAS – automatically indexing new files | codesourcery](https://codesourcery.wordpress.com/2012/11/29/more-on-the-synology-nas-automatically-indexing-new-files/)
- [synchronize your Synology NAS DLNA shares with synoindex and inotifywait](https://github.com/bonidier/synodlna-index)
- [[Synology] L’Indexation instantannée pour le DLNA](http://blogmotion.fr/systeme/indexer-media-11535)
- https://github.com/carljm/synology-mediamon

## Backup & Sync

Cloud Sync vs Hyper Backup

- Hyper Backup: the backup is Block-level (vs file level) Incremental Backup (cumulative incrementals, backs up only the blocks that changed since the last full backup)
	- incremental backup
	- allow to encrypt client side (before send data to the provider)
	- config: schedule backup (when), max versions
	- app data backup
- Cloud Sync: Real-time push replication not for backup (no backup history, but files version provider side), like a distant virtual filesystem. File updated often require to upload the whole file.
	- can be started and stopped with a task schedule

Some provider are only available with Cloud Sync, a workaround is create a local backup with Hyper Backup then sync it with Cloud Sync. See https://www.reddit.com/r/backblaze/comments/5ilifq/a_guide_on_how_to_backup_your_synology_nas_to/df01ric/

Note: Hyper Backup lot of API requests and it's not adpated for paid API request type plan

Log file `/var/log/messages` `grep img_backup`

- [Synology Data Backup: How to choose between Snapshot Replication, Cloud Station, and Hyper Backup? - ACE Peripherals ::: Comple](http://www.aceperipherals.com/2016/synology-data-backup-how-to-choose-between-snapshot-replication-cloud-station-and-hyper-backup)
- [DSM 6.0 - Data Backup - Synology - Network Attached Storage (NAS)](https://www.synology.com/en-global/dsm/data_backup)
- [Backing Up a Synology NAS](http://www.macdrifter.com/2014/11/backing-up-a-synology-nas.html)
- [Cheap, huge cloud backups for a Synology NAS – Marco.org](https://marco.org/2014/11/04/synology-backups)
- [Moving to a NAS-based storage solution — Max Lein](http://maxlein.com/blog/2015/2/4/moving-to-a-nas-based-storage-solution)
- [Synology Hybrid Backup, Part 1 – J Metz's Blog](https://jmetz.com/2015/08/synology-hybrid-backup-part-1/)
- [Synology DSM 6.0 for protecting your business data |](http://www.techblogger.io/2016/03/synology-dsm-6-0-for-protecting-your-business-data/)
- [Backblaze B2 Reaching "Class C Transactions Cap" with Synology NAS - Daniel Gibbs](https://danielgibbs.co.uk/2016/08/b2-class-c-transaction-caps-synology/) - Change _polling period_ from 60 seconds to 3600 (1 hour)

- CrashPlan speed PB [Speeding up CrashPlan Backups – Network Rockstar](http://networkrockstar.ca/2013/09/speeding-up-crashplan-backups/)
- Problem with file-level (content) of backup sparse bundle is hard link of folder (use instead block-level, raw content) [Cloning a Time Machine backup | Carbon Copy Cloner | Bombich Software](https://bombich.com/kb/ccc3/cloning-time-machine-backup)
- Use sparse bundle to clone a disk (not dmg nor sparseimage) [A New Backup Strategy | Blogarithms](http://blogarithms.com/2014/08/17/a-new-backup-strategy/comment-page-1/)
- create a specific user and share folder for each backuped TM machine on Synology. Its session could be killed if TM fail with an already in use error: [Apple Time Machine Backup on Synology NAS Fails | Read The Effin' Blog](https://rteb.wordpress.com/2012/07/03/apple-time-machine-backup-on-synology-nas-fails/)

Backup to USB disk (with Hyper Backup):

- [How to backup to external USB-disk? - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=96203)
- [DSM 5.0 and USB backup - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=83954)

### Hyper Backup

Store metadata in `/volumeX/@img_bkp_cache` in the installed volume. Can be take gigas (use 57GB for 430GB of data and 2.1TB with all versions). This data can be build/rebuild from relink with HyperBackup app with a remote repository
Exec `/var/packages/HyperBackup/target/bin/synouserdata` (see `/var/packages/HyperBackup/target/etc/userdata.config`)
You can create a version of backup on an USB drive before relink once it's uploaded

- [DiskStation Manager - Knowledge Base | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/help/DSM/Tutorial/backup_backup)
- [Create Backup Tasks | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/help/HyperBackup/data_backup_create)

Rotation advice for "Smart Recycle" (1 version per hour for last 24h, 1 per day for last 30 days, 1 per month for last year): with 66 (24+30+12, for the last year) version. Use 74 versions.
For 90 retention days, use (90+12+4) 106 (1 version per day for 3 months, 1 per month for 1 year, 1 year for 4 years)

Check Backup integrity:
> "Check backup integrity: Perform integrity check on backup data to know if the related backup task can proceed and if the backup data can be successfully restored."
> no data is actually transferred during the Integrity Check
> The integrity check simply checks on backup data to know if the related backup task can proceed and if the backup data can be successfully restored.
> This will check all the backed up files to make sure everything required for restore or continue backup exists on the cloud side.
- [Create Backup Tasks | Synology Inc.](https://www.synology.com/en-us/knowledgebase/DSM/help/HyperBackup/data_backup_create)

- [How to backup files directly between Synology DiskStation and Apple AirPort Time Capsule? | iknowsomething.com](http://iknowsomething.com/how-to-backup-files-directly-between-synology-diskstation-and-apple-airport-time-capsule/)
- `sudo /var/packages/HyperBackup/target/bin/synoimgbkptool --help`
- ?? `/var/packages/HyperBackup/target/bin/synoimgbkptool -r /volume1/@img_bkp_cache/aws_s3_synology.coene_AKIAII7X3LHP5R4HOUNA.Hkx7Wx -t ds414_1.hbk -S bkp -E /tmp/scoped_temp_file.XeMJPp`

```sh
sudo cat /var/log/messages | grep 'img_backup\|img_worker\|synolocalbkp\|synoimgbkptool'
```

#### Format and storage

Note: Hyper Backup use block-level incremental backups
Note: **If backup fail, try to backup smaller data set** (Backup task settings > Folders : check less folders), and incrementally add more folders
Note: `.hbk` hyperbackup image folder package (contains a empty file `SynologyHyperBackup.bkpi`) can be mount (with right click with File Station) and explored via a standard file protocol (e.g. AFP or SMB). Can be open with [HyperBackupExplorer](https://www.synology.com/en-global/knowledgebase/DSM/help/HyperBackupExplorer/hyperbackupexplorer). See [How to retrieve backup files with Hyper Backup Explorer](https://www.synology.com/en-global/knowledgebase/DSM/tutorial/Backup_Restore/How_to_retrieve_backup_files_with_Hyper_Backup_Explorer)
Note: If the backup fail `Error: DB (/XX/XX.hbk/Config/candidate_chunk.db) has tmp-file (/XX/XX.hbk/Config/candidate_chunk.db-shm) in version-complete`. It's due to the size of `candidate_chunk.db` should exceed the file system max file size limit (for FAT32, the file max size is 4GB). Use an other file system (ext4 or exFAT)

- [DiskStation Manager - Knowledge Base | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/tutorial/Storage/How_can_I_recover_data_from_my_DiskStation_using_a_PC)
- [Create Backup Tasks | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/help/HyperBackup/data_backup_create)

#### Encryption

**Always encrypt the data client side.**

The Hyper Backup package can use (client side) encryption:

> protect the backup data with password from unwanted access on the destination side.
— [DiskStation Manager - Knowledge Base | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/help/DSM/Tutorial/backup_backup)

> Client-side encryption to ensure data confidentiality at the backup destination:
> 
> - Data and file name encryption with AES256-CBC.
> - Key ring encryption with RSA2048.
— [Software spec - DSM 6.0 | Synology Inc.](https://www.synology.com/en-global/dsm/6.0/software_spec)

> The password is the only thing needed to decrypt the files, but Synology support (or whoever requests it from them or whoever you give it to) can also decrypt your files using the private key.
> Officially this is for when you forgot your password.
> [...]
> They encrypt each file with a random key and this random key with both, the public key and the passphrase.
> So you can decrypt the files if you have either the private key or the passphrase.
— [Cloud Sync encryption : password as key ?? - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=101361#p382876)

`.pem` file is `RSA PRIVATE KEY` is PKCS#1 (key object from PKCS#8, but without the version or algorithm identifier in front vs `PRIVATE KEY` is PKCS#8). See [openssl - what is the differences between "BEGIN RSA PRIVATE KEY" and "BEGIN PRIVATE KEY" - Stack Overflow](https://stackoverflow.com/questions/20065304/what-is-the-differences-between-begin-rsa-private-key-and-begin-private-key/20065522#20065522)

	# Not sure if we can do this:
	openssl rsautl -decrypt -in in.mp3 -out out.mp3 -inkey key/private.pem

- http://ukdl.synology.com/download/Tools/SynologyCloudSyncDecryptionTool/
- [Python Script to decrypt and extract files from a Synology HyperBackup backup](https://github.com/mistersandman/hyperbackup_decrypt) - see [HyperBackup Verschlüsselung (Client-side encryption) - Details](http://www.synology-forum.de/showthread.html?78953-HyperBackup-Verschl%C3%BCsselung-%28Client-side-encryption%29-Details)
- [Download Center - Support | Synology Inc.](https://www.synology.com/en-global/support/download/)
- [DiskStation Manager - Knowledge Base | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/tutorial/Application/What_is_Synology_Cloud_Sync_Decryption_Tool)

#### Local cache space

Or move location of `@img_bkp_cache` (`/usr/syno/etc/synobackup.conf`)

    # Remove local cache directory broke the local index ("Local index broken"), need to relink the target (redownload some parts from cloud)
    # Before: 170GB (for ~3TB)
    # After: 98GB ... 169GB ... no effect
	rm -rf /volume1/@img_bkp_cache/aws_s3_synology.coene_AKIAII7X3LHP5R4HOUNA.Hkx7Wx
    # Then relink the target (via HyperBackup UI)

	#vacuum cand-chunk db
	# For /volume1/@img_bkp_cache/aws_s3_horseradish-backups_ELPZYDFL16BE6BASQ3ZM.aGexMW/Armadillo.hbk
	du -h -d0 /volume1/@img_bkp_cache/aws_s3_horseradish-backups_ELPZYDFL16BE6BASQ3ZM.aGexMW
    # sudo /var/packages/HyperBackup/target/bin/synoimgbkptool -h
    # [...]
    # -e, --clear-cache-tmp        clear temp folders in all cloud caches
    # -p, --space-local            compute the local space usage for a target
    # -r, --repository             indicate the objective repository
    # -t, --target                 indicate the objective target
    # -V, --vacuum                 vacuum DB; cand: cand-chunk DB, ver: version-list DB
	sudo /var/packages/HyperBackup/target/bin/synoimgbkptool -r /volume1/@img_bkp_cache/aws_s3_horseradish-backups_ELPZYDFL16BE6BASQ3ZM.aGexMW -t Armadillo.hbk -p
	sudo /var/packages/HyperBackup/target/bin/synoimgbkptool -r /volume1/@img_bkp_cache/aws_s3_horseradish-backups_ELPZYDFL16BE6BASQ3ZM.aGexMW -t Armadillo.hbk -V cand
	sudo /var/packages/HyperBackup/target/bin/synoimgbkptool -r /volume1/@img_bkp_cache/aws_s3_horseradish-backups_ELPZYDFL16BE6BASQ3ZM.aGexMW -t Armadillo.hbk -V ver
    sudo /var/packages/HyperBackup/target/bin/synoimgbkptool -e

- [HyperBackup: Amazon cloud, local cache | Synology Community](https://community.synology.com/forum/17/post/102580)
- [@img_bkp_cache directory for HyperBackup | Synology Community](https://community.synology.com/forum/17/post/99706)

### Cloud Sync

- [Synology NAS and Backblaze B2 Cloud Storage](https://www.backblaze.com/b2/partner-synology.html)
- [How to back up the data on your Synology NAS to the public cloud | Synology Inc.](https://www.synology.com/en-us/knowledgebase/DSM/tutorial/Backup/How_to_back_up_the_data_on_your_Synology_NAS_with_public_cloud)

### Drive

Synology Drive (sync part) is remplacement of Cloud Station, see ["Differences between Drive and Cloud Station"](https://www.synology.com/en-global/knowledgebase/DSM/tutorial/Collaboration/What_do_I_need_to_know_before_upgrading_from_Cloud_Station_to_Synology_Drive#b_11)

- [What is On-demand Sync? | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/tutorial/Application/What_is_On-demand_Sync)
- [Why are files not synced between Synology Drive and Drive desktop application? | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/tutorial/Collaboration/Why_are_files_not_synced_between_Synology_Drive_and_Drive_desktop_application)
- [Drive for PC | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/help/SynologyDriveClient/synologydriveclient)
- [Drive (Android) | Synology Inc.](https://www.synology.com/en-global/knowledgebase/Mobile/help/Drive)
- [Drive | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/help/SynologyDrive/drive_desc)

Apps: 

- Web portal: <https://yourhost:port/?launchApp=SYNO.SDS.Drive.Application>
- PC & Mac: Synology Drive Client [Download Center - DS415+ | Synology Inc.](https://www.synology.com/en-global/support/download/DS415+#utilities)
- Android: Synology Drive [Download Center - DS415+ | Synology Inc.](https://www.synology.com/en-global/support/download/DS415+#androids)
- iOS: [‎Synology Drive on the App Store](https://itunes.apple.com/us/app/synology-drive/id1267275421?mt=8)

### OVH Public Cloud Storage vs HubiC

- OVH Public Cloud Storage: Cloud Sync
- HubiC: Hyper Backup

- http://tazintosh.com/faites-de-hubic-une-solution-de-backup/ see also https://hubic.com/en/apps.xml and https://github.com/jbfuzier/Synology/tree/master/Hubic

- [hubiC : Stockage en ligne pour tous vos fichiers – hubiC.com](https://hubic.com/fr/)

The default Openstack container is `default`. For other container: `https://hubic.com/home/browser/#mynewcontainer`

- hubic2swiftgate + ftp-cloudfs (mount Swift as FTP)[Faites de hubiC une solution de “backup” !](http://tazintosh.com/faites-de-hubic-une-solution-de-backup/)
- [Swift Explorer - 619.io](http://www.619.io/swift-explorer)
- [Node OpenStack Swift authentication for hubiC.com](https://github.com/gierschv/node-hubic-swiftauth)
- [Backups distant sur HubiC – J'ai acheté un PC neuf cassé ...](http://blog.ght1pc9kc.fr/Backup-distant-sur-HubiC/)

- [Dossier distant & Hubic/Synology - Page 5](https://forums.hubic.com/showthread.php?5648-Dossier-distant-amp-Hubic-Synology/page5)
- [Backup with Hubic - Synology Forum](https://forum.synology.com/enu/viewtopic.php?f=260&t=115155)
- (old use Cloud Sync, before Hyper Backup was included in DSM6) [Chiffrer une sauvegarde pour l’envoyer dans le cloud](http://blogmotion.fr/systeme/backup-synology-cloud-13121)
- (old use Cloud Sync, before Hyper Backup was included in DSM6) [Synology : backup chiffré dans le Cloud (HubiC) | Up and Clear](https://upandclear.org/2016/02/13/synology-backup-chiffre-dans-le-cloud-hubic/)
- [Backups dans le cloud hubic avec duplicity et rclone(rsync)](http://nogues.pro/blog/backup-hubic-duplicity-rsync.html)
- [hubiC, un retour d’expérience - PENtax Klub](http://pentaxklub.com/hubic-retour-dexperience/)
- [DiskStation Manager - Knowledge Base | Synology Inc.](https://www.synology.com/en-us/knowledgebase/DSM/help/CloudSync/cloudsync)

- [Synchronise Synology NAS with Object Storage using DiskStation Manager 6.0 - OVH](https://www.ovh.com/us/g2090.synchronise_synology_nas_with_object_storage_using_diskstation_manager_60)
- [OVH Public Cloud: Our Cloud Computing solutions - OVH](https://www.ovh.com/us/cloud/storage/)
- [OVH Public Cloud Object Storage et API OpenStack Swift](https://gist.github.com/BaptisteDixneuf/85dc4419a0398446d2d3)

## Time Machine

Can only have 1 folder for all machines (will contains all sparse bundles). 

The band size of sparse bundle don't have importance for block level backups (like Hyper Backup). It's better to have larger band (speed up transferts, but not too large) if it not encrypted images.
When use Hyper Backup, use smaller band if the sparse bundle is encrypted (sparse bundle chunk updated - full encrypted - and needed reuploaded completely)

- [Synology: Configuring Time Machine and Quotas - SFlanders.net](http://sflanders.net/2015/11/23/synology-configuring-time-machine-quotas/)

Hibernation can cause trouble with Time Machine. Disk with Time Machine share can take time to wake up and TM didn't wait long enough for the NAS to wake up.

Since the Time Machine backup cycle is 1h, **wait 1h before entering in hybernation**: Configuration panel > Power and hardware > (HDD) Hybernation. **Before to change this setting, check Client (OSX) system.log "backupd" if there is no error.**

- [DiskStation Manager - Knowledge Base | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/tutorial/General/What_is_the_difference_between_HDD_Hibernation_System_Hibernation_and_Deep_Sleep)
- [DiskStation Manager - Knowledge Base | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/tutorial/General/What_stops_my_Synology_NAS_from_entering_System_Hibernation)
- [Wake up too slow for Time Machine. - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=66316)
- [Hibernation with Apple Time Machine - Synology Forum](https://forum.synology.com/enu/viewtopic.php?t=27845)
- [Amazon](http://www.amazon.com/gp/aw/review/B00OZ0CTAU/R2YV6NQW6B765J/)

- [DiskStation Manager - Knowledge Base | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/tutorial/Virtualization/How_to_use_iSCSI_Targets_on_Mac_computers)

## Backup a remote server with FTP

Command line, see [backup external server](Command line (Unix)#backup-external-server)

or use Download station, (support FTP) (can use RSS as source list)

- [How to backup FTP to Synology Station - Evotec](https://evotec.xyz/how-to-backup-ftp-to-synology/)

## ipkg

### Install

Append to the end of `/root/.profile`:

	PATH=/opt/bin:/opt/sbin:$PATH

Add in `/etc/rc.local`:

	ln -s /volume1/@optware /opt

	ln -s /volume1/@optware/bin /opt
	ln -s /volume1/@optware/etc /opt
	ln -s /volume1/@optware/include /opt
	ln -s /volume1/@optware/lib /opt
	ln -s /volume1/@optware/man /opt
	ln -s /volume1/@optware/opt /opt
	ln -s /volume1/@optware/sbin /opt
	ln -s /volume1/@optware/share /opt
	ln -s /volume1/@optware/tmp /opt
	ln -s /volume1/@optware/var /opt

- [How to install IPKG on a Synology NAS](http://www.vspecialist.co.uk/2014/09/how-to-install-ipkg-on-a-synology-nas/)
- [Overview on modifying the Synology Server, bootstrap, ipkg etc - SynologyWiki](http://wayback.archive.org/web/20160323062956/http://forum.synology.com/wiki/index.php/Overview_on_modifying_the_Synology_Server,_bootstrap,_ipkg_etc#Installing_compiled.2Fbinary_programs_using_ipkg)
- [ipkg package manager installation on Synology NAS - ReScene](http://rescene.wikidot.com/synology-ipkg)
- [Installer ipkg NAS synology DS214 - Noobunbox](https://www.noobunbox.net/synology/installer-ipkg-nas-synology-ds214)

### Usage

	ipkg update && ipkg upgrade
	ipkg list
	ipkg install <package>
	ipkg remove <package>

## Debian chroot

Recommanded for advanced users only

- [Debian Chroot on Synology NAS – Mark’s Blog](https://markpith.wordpress.com/2015/10/26/debian-chroot-on-synology-nas/)
- [SynoCommunity](https://synocommunity.com/package/debian-chroot)
- [Synology debian chroot - Courville](http://www.courville.org/home/synology-debian-chroot)
- About Debian chroot [Ipkg Pour Ds213+ Ou Ds413 - Logiciels Compatibles - NAS-Forum](http://www.nas-forum.com/forum/topic/29527-ipkg-pour-ds213-ou-ds413/)

## Reset the admin password or network settings

Reset to factory default the admin password and network settings. Data will remain intact

- [DiskStation Manager - Knowledge Base | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/tutorial/General/How_to_reset_your_Synology_NAS)

## Notifications

Free Mobile (l'option doit être activée dans le compte)

`https://smsapi.free-mobile.fr/sendmsg?user=ID_ESPACE_ABONNE_FREEMOBILE&pass=CLE_IDENTIFICATION_AU_SERVICE&to=+33NUMERO_PORTABLE_A_JOINDRE&msg=Hello+World.` Pour free mobile le champ `to` n'est pas utilisé (mais au moins 4 champs sont requis par DSM. Free Mobile utilise celui lié au compte, cf. `user`). L'envois en POST est aussi possible. Free Mobile indique qu'il faut utiliser les `%20` pour les espaces, mais utiliser `+` (sinon le message de test sera "Test%Message%from%DiskStation")

- [Notification](https://www.synology.com/cgi/knowledgebase/?action=findHelpFile&dsm=6.1-15101&section=dsm&lang=fre&link=AdminCenter%2Fsystem_notification_sms.html&font=100&unique=synology_avoton_415%2B&version=6.1)
- [NAS Synology : notification par SMS via Free Mobile | Pascal's weblog](http://pled.fr/?p=9529)
- [Tutoriel : Utiliser la notification SMS Free Mobile avec un NAS (Synology)](http://www.universfreebox.com/article/26340/Tutoriel-Utiliser-la-notification-SMS-Free-Mobile-avec-un-NAS-Synology)

## VPN

**Don't forget to open port in firewall (see Configuration Application > External Access > Router Configuration, then create a new rule based on Application)**

L2TP/IPSec: Manual DNS: check it the default value (defined by Configuration Application > Network > General > Configure manually DNS server) is not an IPv6, not supported by PPPD (ms-dns), else you will get `invalid address parameter 'AAAA:AAAA:AAAA::AAAA' for ms-dns option`

- https://ppp.samba.org/pppd.html
- https://www.synology.com/en-global/knowledgebase/DSM/help/VPNCenter/vpn_setup

For routing traffic to LAN of the VPN server, need to add route

> OpenVPN support the concept of bridging

> but it requires the client side being able to do TAP (and the router needs to be set up as OpenVPN server with two routers and do layer-2 bridging  with GRE and IPsec)

Which means broadcast messages (like NetBIOS hostname, mDNS) on VPN server can be delivered to VPN client too. You can cheat it by write in hosts file

> L2TP/IPsec connection does not forward broadcast/multicast

Or use the same network as the DSM is. https://forum.synology.com/enu/viewtopic.php?t=40649#p173554

Note: the following doesn't fix the issue

For PPTP in `/var/packages/VPNCenter/etc/pptp/accel-pppd.conf` change `gw-ip-address` and `tunnel` in `[ip-pool]` section. See default values in `/usr/syno/etc/packages/VPNCenter/pptp/accel-pppd.conf`. (What about `/var/packages/VPNCenter/target/etc/pptp/accel-pppd.conf`?)
For L2TP in `/var/packages/VPNCenter/etc/l2tp/xl2tpd.conf` change `local ip` and `ip range` in `[lns default]` section. (What about `/var/packages/VPNCenter/target/etc/l2tp/xl2tpd.conf`?)
Shouldn't conflict with DHCP IP ranges. Don't forget to stop and start VPN Application before and after editing the conf file.

On macOS pour l'auto routing:

	# or without -n
	netstat -rn
	ifconfig
	#see ppp0 gateway
	# Use 255.255.255.0 as subnet mask
	sudo route add -net 192.168.3 -interface ppp0
	# Delete the route. It's remove when the interface is deconnected (?)
	sudo route -n delete -net 192.168.3 -interface ppp0
	
	# You can create a route when the VPN connect, by create a file /etc/ppp/ip-up same for /etc/ppp/ip-down
	# chmod 0755 /etc/ppp/ip-up


	# Client setting (same as server setting):
	# Use the same setting as you are using on
	# the server.
	# On most systems, the VPN will not function
	# unless you partially or fully disable
	# the firewall for the TUN/TAP interface.
	dev tap
	;dev tun
	# routed=tun bridge=tap
	# https://openvpn.net/index.php/open-source/documentation/howto.html#vpntype
	# https://docs.openvpn.net/docs/openvpn-connect/openvpn-connect-ios-faq.html tap is not supported by iOS client

	# "dev tun" will create a routed IP tunnel,
	# "dev tap" will create an ethernet tunnel.
	# Use "dev tap0" if you are ethernet bridging
	# and have precreated a tap0 virtual interface
	# and bridged it with your ethernet interface.

- https://www.synology.com/en-global/knowledgebase/DSM/tutorial/Application/How_to_connect_to_Synology_s_VPN_Server_using_a_Windows_PC_or_Mac#t4
- https://serverfault.com/questions/274882/cant-resolve-host-through-vpn-connection-from-mac-os-x
- https://forum.synology.com/enu/viewtopic.php?t=38103
- https://superuser.com/questions/4904/how-to-selectively-route-network-traffic-through-vpn-on-mac-os-x-leopard/206826#206826
- http://ethancbanks.com/2016/09/26/auto-adding-routes-when-mac-pptp-connection-comes-up/
- http://chris.eldredge.io/blog/2015/05/24/synology-vpn-server-route-advertising/
- http://hints.macworld.com/article.php?story=20080626194901370
- http://kcpolymath.blogspot.fr/2012/09/wire-to-wire-emulation-with-proxy-arp.html
- [NAT tricks for VPN with clients in private address ranges](http://www.nimlabs.org/dirtynat.html)

## Slow SMB Shares

Advanced Settings:

- ~~Minimum SMB protocol: SMB2~~
- Transport encryption mode: disabled **This setting increase the speed (more than ×10)**
- Enable Opportunistic Locking

- [What can I do to fix slow SMB file transfers on OS X 10.11.5? | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/tutorial/General/What_can_I_do_to_fix_slow_SMB_file_transfers_on_OS_X_10_11_5)
- [Turn off packet signing for SMB 2 and SMB 3 connections - Apple Support](https://support.apple.com/en-bh/HT205926)
- [SMB | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/help/DSM/AdminCenter/file_winmacnfs_win)
- `smbutil statshares -a` if share mounted has `SIGNING_ON	TRUE`

## Printers and scanners

```sh
sudo cat /var/log/messages | grep 'cupsd\|synoprint\|udev_printer\|synoscgi_SYNO.Core.ExternalDevice.Printer'
sudo tail -f /var/log/messages | grep --line-buffered 'cupsd\|synoprint\|udev_printer\|synoscgi_SYNO.Core.ExternalDevice.Printer'
```

### USB Scanner

With MFP (USB connected multi-function printer) you can use the scanner from Windows clients. On network scanner you can "upload" scans on SMB shares.
But for USB connected scanner only or MFP for non Windows clients, you need a server software like [SANE](http://www.sane-project.org/) to allow clients to use it.

- [External Devices | Synology Inc.](https://www.synology.com/en-global/knowledgebase/DSM/help/DSM/AdminCenter/system_externaldevice_printer)
- [SANE - Supported Devices](http://www.sane-project.org/sane-supported-devices.html)
- [Share a multifunctional printer (with your Synology) | Here and Now … Then and There](https://francois.aichelbaum.com/2016/03/10/share-multifunctional-printer-synology)
- [Attaching a scanner to my Synology Diskstation 107](https://web.archive.org/web/20110910090930/http://arnoutboer.nl:80/weblog/?p=223)
- [SANE Backends network scanning package for Synology NAS | PC LOAD LETTER](https://pcloadletter.co.uk/2015/12/16/sane-backends-syno-package/)
- [Manual: Network scanning with HPLIP and Sane (HP all in one) - Synology Forum](https://forum.synology.com/enu/viewtopic.php?f=27&t=14801)
- [ScanningHowTo - Community Help Wiki](https://help.ubuntu.com/community/ScanningHowTo)
- [Installer un serveur de numérisation, SANE](https://artisan.karma-lab.net/installer-serveur-numerisation-sane)

See also [macOS Scanning](../macOSmacOS.md#scanning)

### Printer server CUPS

CUPS WebInterface is not available (files in `/usr/lib/cups/cgi-bin/`, `/usr/share/cups/doc-root/`, `/usr/share/cups/templates/`, etc. doesn't exist)

Access control is not configured as [it should be](https://github.com/apple/cups/blob/5048d3ba8d38b2bc9c3cf33af043fbccebf90ea2/conf/cupsd.conf.in#L30-L47) (if the web interface is enabled, see also [How can I enable remote access to the Admin page in CUPS - Server Fault](https://serverfault.com/questions/836266/how-can-i-enable-remote-access-to-the-admin-page-in-cups))

Enable `WebInterface=yes` take to "Not Found" error

```sh
cat /etc/cups/cupsd.conf
synoservice --restart cupsd
```

- [Setting up a CUPS server with Docker on a Synology NAS for my Brother printer](http://www.theghostbit.com/2016/10/setting-up-cups-server-with-docker-on.html) - see [RoryQ/Docker-CUPS-for-Synology: Scripts for setting up CUPS server in Docker running on Synology Diskstation for Brother HL-1110](https://github.com/RoryQ/Docker-CUPS-for-Synology)
- [maxandersen/aircups: Cups print server with airprint enabled, works well with Synology](https://github.com/maxandersen/aircups)
	Based on [quadportnick/docker-cups-airprint: Docker image for CUPS intended as an AirPrint relay on Synology DSM](https://github.com/quadportnick/docker-cups-airprint)
- [mnbf9rca/cups-google-print: a CUPS printer with Google Cloud Print enabled](https://github.com/mnbf9rca/cups-google-print)
