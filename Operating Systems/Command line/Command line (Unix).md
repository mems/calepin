- [UNIX Tutorial for Beginners](http://wayback.archive.org/web/20150218174409/http://acad.coloradocollege.edu/dept/pc/SciCompLab/UnixTutorial/)
- [BashFAQ - Greg's Wiki](http://mywiki.wooledge.org/BashFAQ)
- [jlevy/the-art-of-command-line: Master the command line, in one page](https://github.com/jlevy/the-art-of-command-line)
- [The Bash Hackers Wiki \[Bash Hackers Wiki\]](https://wiki.bash-hackers.org/start)
- [Code Snippet - Snipplr Social Repository](https://snipplr.com/all?language=Bash)
- [BashGuide - Greg's Wiki](http://mywiki.wooledge.org/BashGuide)
- [Bash scripting Tutorial - LinuxConfig.org](https://linuxconfig.org/bash-scripting-tutorial)

- [GNU/Linux Command-Line Tools Summary](https://tldp.org/LDP/GNU-Linux-Tools-Summary/html/GNU-Linux-Tools-Summary.html)
- [Bash Guide for Beginners](https://tldp.org/LDP/Bash-Beginners-Guide/html/Bash-Beginners-Guide.html)
- [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/abs-guide.html)

Commands tips and examples:

- [explainshell.com - match command-line arguments to their help text](https://explainshell.com/)
- [One-liners | Basic | Cheat sheet | Linux Command Library](https://linuxcommandlibrary.com/basic/oneliners.html)
- [General purpose command-line tools](http://www.compciv.org/unix-tools/)
- [All commands sorted by votes](https://www.commandlinefu.com/commands/browse/sort-by-votes)
- [Linux Commands - Complete Guide](https://linoxide.com/linux-how-to/linux-commands-brief-outline-examples/)
- [What is your single most favorite command-line trick using Bash? - Stack Overflow](https://stackoverflow.com/questions/68372/what-is-your-single-most-favorite-command-line-trick-using-bash)
- [dannguyen/bashfoo: My personally curated list of bash/command-line commands and snippets that are very useful yet I keep on forgetting](https://github.com/dannguyen/bashfoo#toc)

![bash tips](https://pbs.twimg.com/media/C75R5xUVsAEwlwf.jpg:large)

## Configuration

### Conserver la configuration d'iptables lors des démarrages

```sh
# Sauvegarde de la configuration d'iptables dans un fichier
iptables-save > /etc/iptables.conf

# Création d'un fichier sh dans le dossier ...
echo "#!/bin/sh" > /etc/network/if-up.d/iptables

# ... qui restaurera les règles sauvegardé dans le fichier /etc/iptables.conf
echo "iptables-restore < /etc/iptables.conf" >> /etc/network/if-up.d/iptables
# Rendre executable le script bash
chmod +x /etc/network/if-up.d/iptables
```

Il est nécéssaire de relancer ce script à chaque modifications d'iptables

### Gestion des services

(must be executable: `chmod +x /etc/init.d/blah`)

```sh
#! /bin/sh
# /etc/init.d/blah
## BEGIN INIT INFO
# Provides: blah
# Required-Start: $local_fs $syslog $remote_fs dbus
# Required-Stop: $local_fs $syslog $remote_fs
# Default-Start: 2 3 4 5
# Default-Stop: 0 1 6
# Short-Description: Start blah
## END INIT INFO

# Some things that run always
touch /var/lock/blah

# Carry out specific functions when asked to by the system
case "$1" in
  start)
    echo "Starting script blah"
    echo "Could do more here"
    ;;
  stop)
    echo "Stopping script blah"
    echo "Could do more here"
    ;;
  *)
    echo "Usage: /etc/init.d/blah {start|stop}"
    exit 1
    ;;
esac

exit 0
```

Define when service have to be start or stop:

```sh
update-rc.d blah defaults
```

To remove from the startup sequence

```sh
update-rc.d -f blah remove
```

- https://help.ubuntu.com/community/UbuntuBootupHowto
- http://www.debian-administration.org/articles/28
- `man update-rc.d`
- http://en.wikipedia.org/wiki/Runlevel
- http://www.debuntu.org/how-to-managing-services-with-update-rc-d/
- List all runlevel for the service `apache2`: `ls -l /etc/rc?.d/*apache2`

## User prompt

```sh
#!/bin/bash
echo "Yes,No?"
read answer
echo "You're answer: $answer"
```

- http://www.tldp.org/LDP/Bash-Beginners-Guide/html/Bash-Beginners-Guide.html#sect_08_02_01

## User administration

```sh
# Show user rights
ls -l
# or, but show folders "." and ".."
ls -all

# User informations
id USERNAME

# Show last logs of users
lastlog

# Show last logged users
last

# Show current user
who -a

# Command history
~/.bash_history
~/.history
# for root user
/root/.bash_history

# Be sure no user can hide his command history (a = append only, i = immutable)
chattr +a /home/user/.bash_history
chattr +i /home/user/.profile
# See also
# http://www.akyl.net/securing-bashhistory-file-make-sure-your-linux-system-users-won%E2%80%99t-hide-or-delete-their-bashhistory
# http://zero202.free.fr/bash/html/ar01s01.html#id336074

# https://en.wikipedia.org/wiki/Chattr
chattr
chwon
chmod
```

## Network

Note: ifconfig, route, mii-tool, nslookup commands are obsolete

```sh
# Show status of ethernet interface eth0
ethtool eth0

#Manually set ethernet interface speed
ethtool --change eth0 autoneg off speed 100 duplex full

# Show status of wireless interface eth1
iwconfig eth1

# Manually set wireless interface speed
iwconfig eth1 rate 1Mb/s fixed

# List wireless networks in range
iwlist scan

# List network interfaces
ip link show

# Rename interface eth0 to wan
ip link set dev eth0 name wan

# Bring interface eth0 up (or down)
ip link set dev eth0 up

# List addresses for interfaces
ip addr show

# Add (or del) ip and mask (255.255.255.0)
ip addr add 1.2.3.4/24 brd + dev eth0

# List routing table
ip route show

# Set default gateway to 1.2.3.254
ip route add default via 1.2.3.254

# Lookup DNS ip address for name or vice versa
host pixelbeat.org

# Lookup local ip address (equivalent to host `hostname`)
hostname -i

# Lookup whois info for hostname or ip address
whois pixelbeat.org

# List internet services on a system
netstat -tupl

# List active connections to/from system
netstat -tup

# DNS record
dig example.com

# Reverse DNS
ping -a 8.8.8.8
nslookup -type=ptr 8.8.8.8

# Machine name
hostname

# Test if remote port is open
nc -vz example.com 80
nmap -p 80 example.com
telnet example.com 80
timeout 1 bash -c "</dev/tcp/example.com/80" && echo Port open || echo Port closed
```

`/etc/hostname` `/etc/hosts`

- [Configurer une passerelle réseau — Korben Wiki](https://wiki.korben.info/Configurer_une_passerelle_r%C3%A9seau)

### Windows networking

Note: samba is the package that provides all this windows specific networking support

```sh
# Find windows machines. See also findsmb
smbtree

# Find the windows (netbios) name associated with ip address
nmblookup -A 1.2.3.4

# List shares on windows machine or samba server
smbclient -L windows_box

# Mount a windows share
mount -t smbfs -o fmask=666,guest //windows_box/share /mnt/share

# Send popup to windows machine (off by default in XP sp2)
echo 'message' | smbclient -M windows_box

# Mount a windows network share
mount -t smbfs -o username=user,password=pass //WinClient/share /mnt/share

# Netbios name resolution
nbtscan ip_addr

# Netbios name resolution
nmblookup -A ip_addr

# Show remote shares of a windows host
smbclient -L ip_addr/hostname

# Like wget can download files from a host windows via smb
smbget -Rr smb://ip_addr/share
```

### HTTP

```sh
# Get headers
curl -s -D - https://example.com -o /dev/null
# Raw body
curl -s --ignore-content-length --raw https://example.com

# Get HTTP response
echo -en "GET /feed/ HTTP/1.1\r\nHost:example.com\r\nUser-Agent:Firefox\r\n\r\n" | nc infoheap.com 80
# Get the header Content-Type
echo -en "GET /feed/ HTTP/1.1\r\nHost:example.com\r\nUser-Agent:Firefox\r\n\r\n" | nc localhost 80 | head -n 30 | grep -a Content-Type
# Search if test is in first 1000 bytes (include header)
echo -en "GET /feed/ HTTP/1.1\r\nHost:example.com\r\nUser-Agent:Firefox\r\n\r\n" | nc localhost 80 | head -c1K | grep -a test
# Get body length
echo -e "GET / HTTP/1.1\r\nHost: example.com\r\nAccept-Encoding: gzip, deflate\r\n\r\n" | nc localhost 80 | sed ':a;N;$!ba;s/^.*\r\n\r\n//g' | wc -c
# Get body uncompressed length (should be gzipped)
echo -e "GET / HTTP/1.1\r\nHost: example.com\r\nAccept-Encoding: gzip, deflate\r\n\r\n" | nc 93.184.216.34 80 | sed ':a;N;$!ba;s/^.*\r\n\r\n//g' | gzip -d | wc -c

# Simple HTTP server
echo -e "GET / HTTP/1.1\r\nHost:example.com\r\nUser-Agent:Firefox\r\n\r\n" | nc example.com 80 > response.http
while true; do nc -l 8000 < response.http; done

# Create `.htpasswd` file
htpasswd -c /path/.htpasswd USERNAME
```

[How to display request headers with command line curl - Stack Overflow](https://stackoverflow.com/questions/3252851/how-to-display-request-headers-with-command-line-curl/26644485#26644485)

#### wget

Multi purpose download tool

```sh
# Store local browsable version of a page to the current dir
(cd dir/ && wget -nd -pHEKk http://www.pixelbeat.org/cmdline.html)

# Continue downloading a partially downloaded file (with the ability to stop the download and resume later)
wget -c http://www.example.com/large.file

# Download a set of files to the current directory
wget -r -nd -np -l1 -A '*.jpg' http://www.example.com/dir/

# FTP supports globbing directly
wget ftp://remote/file[1-9].iso/

# Process output directly
wget -q -O- http://www.pixelbeat.org/timeline.html | grep 'a href' | head

# Download url at 1AM to current dir
echo 'wget url' | at 01:00

# Do a low priority download (limit to 20KB/s in this case)
wget --limit-rate=20k url

# Check links in a file
wget -nv --spider --force-html -i bookmarks.html

# Efficiently update a local copy of a site (handy from cron)
wget -m http://www.example.com/
wget -m -U "" http://example.com/path/dir
```

### SSH Tunnel

```sh
# Redirect local port to a remote machine
ssh -NfL 8080:127.0.0.1:0808 user@host
```

- [Set Up SSH Tunneling on a Linux / Unix / BSD Server To Bypass NAT - nixCraft](https://www.cyberciti.biz/faq/set-up-ssh-tunneling-on-a-linux-unix-bsd-server-to-bypass-nat/)

### Backup external server

Use `rsync` if possible, or `lftp`, `curl`, `wget`, `scp`, `sftp`. See also `unison`, `bacula` or `amanda`

### Copy files over SSH

```sh
scp /path/localfile user@host:/path/remotefile

scp /path/localfile user@host:/path/remotedir/

scp /path/localdir user@host:/path/remotedir

scp -i /home/username/.ssh/id_rsa -r -p username@www.mydomain.tld:/ /dst/dir
```

### Copy files with `sftp`

```sh
sftp -i /path/to/private/keyfile remote.host.tld
```

### Copy files with `lftp`

`/dst/dir.lftp`:

```
set ftp:list-options -a
#set cmd:fail-exit true
# To use keyfile
# http://www.adminschoice.com/how-to-configure-ssh-without-password
# ssh-keygen -t rsa -f keyfile -N ""
#set sftp:connect-program "ssh -a -x -i <keyfile>"
open -u user,pass sftp://sftp.dc0.gpaas.net
mirror --verbose --delete --parallel=4 --only-newer --exclude ^snapshots/ --exclude ^vhosts/ --exclude ^lamp0/\.config --exclude ^lamp0/var/admin/gandi.cnf$ --exclude ^lamp0/var/admin/logrotate.conf$ --exclude ^lamp0/var/cron/admin/logrotate$ --exclude ^lamp0/var/cron/admin/phpsess$ --exclude ^lamp0/db/ --exclude ^lamp0/var/log/.+ --exclude ^lamp0/var/php/www/.+ "${SRC_DIR}" "${DST_DIR}"
exit
```

```sh
# For paths in variables used in sed, see https://stackoverflow.com/a/29613573/470117
SRC_DIR=/src/dir; DST_DIR=/dst/dir; sed -e "s#\${SRC_DIR}#$SRC_DIR#" -e "s#\${DST_DIR}#$DST_DIR#" /dst/dir.lftp | lftp -f /dev/stdin
```

```sh
lftp -u username,password ftphost << EOF
mirror -Re --use-cache /home/ /backup/
mirror -Re --use-cache /etc/ /backup/
mirror -Re --use-cache /var/www/ /backup/
quit 0
EOF
```

`--exclude` / `-x` use extended regular expression (see `egrep`) `\.nfo`. Folders path don't start with slash, but have a trailing slash: `etc/bin/`

Add `--reverse` to restore backup

For `lftp –> Fatal error: Certificate verification: Not trusted`:

```sh
mkdir -p /root/.lftp
echo "set ssl:verify-certificate no" >> /root/.lftp/rc
```

- https://linux.die.net/man/1/lftp
- http://mewbies.com/lftp_basic_usage_tutorial.htm
- [linux - Transfer files using lftp in bash script - Stack Overflow](https://stackoverflow.com/questions/27635292/transfer-files-using-lftp-in-bash-script)
- [Fastest segmented parallel sync of a remote directory over ssh | commandlinefu.com](http://www.commandlinefu.com/commands/view/13759/fastest-segmented-parallel-sync-of-a-remote-directory-over-ssh)
- [`~/.lftp.rc` parameters detailed](https://gist.github.com/gaubert/822090)
- [Shell scripting and LFTP | A Pipe and a Keyboard](http://apipeandakeyboard.com/2013/05/11/shell-scripting-and-lftp/)
- [How to store lftp command result to a variable](https://www.experts-exchange.com/questions/25279654/How-to-store-lftp-command-result-to-a-variable.html)
- [calling lftp from a bash script; howto pass variables into the command syntax](http://www.linuxquestions.org/questions/programming-9/calling-lftp-from-a-bash-script%3B-howto-pass-variables-into-the-command-syntax-4175444669/)

### Copy files from FTP with `wget`

Use a `.wgetrc` file to store configuration

`/dst/dir.wget`:

```
# Credentials
ftp_user=user
ftp_password=password
# Other commands
exclude_directories=/snapshots,/vhosts,/lamp0/.config,/lamp0/db,/lamp0/var/log,/lamp0/var/php/www
#reject=.listing
#cut_dirs=0
quiet=on
no_parent=on
mirror=on
add_hostdir=off
#retr_symlinks=on
```

```sh
cd /dst/dir
WGETRC=/dst/dir.wget wget ftp://www.mydomain.tld/
# Clean up obselete files
find . -type f -name ".listing" -exec bash -c 'cd $(dirname "{}"); find . -maxdepth 0 ! -name ".listing" -printf "%P\n" | fgrep -vf ".listing" | while read file; do rm $(basename "$file"); done;' \;
# find . -type f -name ".listing" -exec bash -c 'cd $(dirname "{}"); find . -maxdepth 0 ! -name ".listing" -printf "%P\n" | fgrep -vf ".listing" | xargs -r rm' \;
```

Note: if you set password in URL don't forget to encode special chars: `mypass#gh647` to `mypass%23gh647`

- [GNU Wget 1.20 Manual](https://www.gnu.org/software/wget/manual/wget.html#Wgetrc-Commands)

### Copy files with `rsync`

Network efficient file copier

- [Handling renamed files or directories in rsync - Server Fault](https://serverfault.com/questions/489289/handling-renamed-files-or-directories-in-rsync/596707#596707)

Use the `--dry-run` option for testing

```sh
# Copy as archive (oneway, for backup)
rsync -a username@www.mydomain.tld:/ /dst/dir

rsync -r -t -v /path/srcdir /path/destdir
rsync -r -t -v /path/srcdir remote:~/My\ documents
# Escape spaces, and keep special char interpreted at the destination. See "How to rsync over ssh when directory names have spaces - Unix & Linux Stack Exchange" https://unix.stackexchange.com/questions/104618/how-to-rsync-over-ssh-when-directory-names-have-spaces
DEST="~/My\ documents"; rsync -r -t -v /path/srcdir "remote:${DEST// /\\ }"

# Only get diffs. Do multiple times for troublesome downloads
rsync -P rsync://rsync.server.com/path/to/file file

# Locally copy with rate limit. It's like nice for I/O
rsync --bwlimit=1000 fromfile tofile

# Mirror web site (using compression and encryption)
rsync -az -e ssh --delete ~/public_html/ remote.com:'~/public_html'

# Synchronize current directory with remote one
rsync -auz -e ssh remote:/dir/ . && rsync -auz -e ssh . remote:/dir/
date=$(date +%Y%m%d-%H%M)
#[for loop over users]
older=( $backups/$user/*(N/om) )
rsync --archive --recursive \
	--fuzzy --partial --partial-dir=$backups/$user/.rsync-partial \
	--log-file=$tempfile --link-dest=${^older[1,20]} \
	--files-from=$configdir/I-$user \
	--exclude-from=$configdir/X-$user \
	$user@$from:/ $backups/$user/$date/

# Copy folder to folder (if mounted)
rsync -ah --progress --exclude='$RECYCLE.BIN' --exclude='$Recycle.Bin' --exclude='.AppleDB' --exclude='.AppleDesktop' --exclude='.AppleDouble' --exclude='.com.apple.timemachine.supported' --exclude='.dbfseventsd' --exclude='.DocumentRevisions-V100*' --exclude='.DS_Store' --exclude='.fseventsd' --exclude='.PKInstallSandboxManager' --exclude='.Spotlight*' --exclude='.SymAV*' --exclude='.symSchedScanLockxz' --exclude='.TemporaryItems' --exclude='.Trash*' --exclude='.vol' --exclude='.VolumeIcon.icns' --exclude='Desktop DB' --exclude='Desktop DF' --exclude='hiberfil.sys' --exclude='lost+found' --exclude='Network Trash Folder' --exclude='pagefile.sys' --exclude='Recycled' --exclude='RECYCLER' --exclude='System Volume Information' --exclude='Temporary Items' --exclude='Thumbs.db' /src/dir/ /dst/dir/

# With exlude list `--exclude-from=exclude-list.txt`:
cat > exclude-list.txt << 'EOF'
# https://alexkaloostian.com/2015/01/22/what-are-all-these-hidden-items-on-my-mac-part-1/
# http://superuser.com/questions/180582/what-are-desktop-db-or-desktop-df-files-on-external-hd
# http://forum.mac4ever.com/pourquoi-t73534.html#p997828
# http://netatalk.sourceforge.net/wiki/index.php/Special_Files_and_Folders
# Apple OS
.AppleDouble
.com.apple.timemachine.donotpresent
.com.apple.timemachine.supported
.Spotlight-V100
.DocumentRevisions-V100
.DS_Store
.Trash
.Trashes
.VolumeIcon.icns
._.Trashes
.fseventsd
.dbfseventsd
.metadata_never_index
.LSOverride
.MobileBackups
.TemporaryItems
.file
.hotfiles.btree
.quota.ops.user
.quota.user
.quota.ops.group
.quota.group
.vol
.PKInstallSandboxManager
.PKInstallSandboxManager-SystemSoftware
# Max OS6-9
Desktop DB
Desktop DF
# AFP
.AppleDB
.AppleDesktop
Temporary Items
Network Trash Folder
.apdisk
# Sherlock files Mac OS 8.5 to OSX 10.3
TheFindByContentFolder
TheVolumeSettingsFolder
.FBCIndex
.FBCSemaphoreFile
.FBCLockFolder
# http://apple.stackexchange.com/questions/14980/why-are-dot-underscore-files-created-and-how-can-i-avoid-them
# https://en.wikipedia.org/wiki/AppleSingle_and_AppleDouble_formats
# See also dot_clean command
#._*

# Linux
lost+found

# Windows
$RECYCLE.BIN
$Recycle.Bin
Thumbs.db
ehthumbs.db
ehthumbs_vista.db
pagefile.sys
hiberfil.sys
desktop.ini
Recycled
RECYCLER
System Volume Information

# Other
.SymAV*
.symSchedScanLockxz

# Package manager cache
node_modules
EOF
```

Resources for exclude metadata and system files:

- https://github.com/github/gitignore
- https://github.com/joeblau/gitignore.io/tree/master/data
- https://gist.github.com/keithmorris/c652b2a4d88788e5416d
- https://github.com/dotphiles/dotphiles/blob/master/git/gitignore

- [Rsync --exclude List for Mac OS X - Alan W. Smith](http://alanwsmith.com/rsync-exclude-list-for-mac-osx)
- [rsync on OS X says its complete but it's really not? : unix](https://www.reddit.com/r/unix/comments/4ozc9e/rsync_on_os_x_says_its_complete_but_its_really_not/)

## Math

```sh
# Quick math (Calculate φ). See also bc
echo '(1 + sqrt(5))/2' | bc -l

# Calculate π the unix way
seq -f '4/%g' 1 2 99999 | paste -sd-+ | bc -l

# More complex (int) e.g. This shows max FastE packet rate
echo 'pad=20; min=64; (100*10^6)/((pad+min)*8)' | bc

# Python handles scientific notation
echo 'pad=20; min=64; print (100E6)/((pad+min)*8)' | python

# Plot FastE packet rate vs packet size
echo 'pad=20; plot [64:1518] (100*10**6)/((pad+x)*8)' | gnuplot -persist

# Base conversion (decimal to hexadecimal)
echo 'obase=16; ibase=10; 64206' | bc

# Base conversion (hex to dec) ((shell arithmetic expansion))
echo $((0x2dec))

# Unit conversion (metric to imperial)
units -t '100m/9.58s' 'miles/hour'

# Unit conversion (SI to IEC prefixes)
units -t '500GB' 'GiB'

# Definition lookup
units -t '1 googol'

# Add a column of numbers. See also add and funcpy
seq 100 | (tr '\n' +; echo 0) | bc
```

## Date and clock

```sh
# Display a calendar
cal -3

# Display a calendar for a particular month year
cal 9 1752

# System date
date

# Set system date and time `MonthDayhoursMinutesYear.Seconds`
date 041217002020.00

# save date changes on BIOS
clock -w

# What date is it this friday. See also day
date -d fri

# Exit a script unless it's the last day of the month
[ $(date -d '12:00 +1 day' +%d) = '01' ] || exit

# What day does xmas fall on, this year
date --date='25 Dec' +%A

# Convert seconds since the epoch (1970-01-01 UTC) to date
date --date='@2147483647'

# What time is it on west coast of US (use tzselect to find TZ)
TZ='America/Los_Angeles' date

# What's the local time for 9AM next Friday on west coast US
date --date='TZ="America/Los_Angeles" 09:00 next Fri'
```

## Locale

```sh
# Print number with thousands grouping appropriate to locale
printf "%'d\n" 1234

# Use locale thousands grouping in ls. See also l
BLOCK_SIZE=\'1 ls -l

# Extract info from locale database
echo "I live in $(locale territory)"

# Lookup locale info for specific country. See also ccodes
LANG=en_IE.utf8 locale int_prefix

# List fields available in locale database
locale -kc $(locale | sed -n 's/\(LC_.\{4,\}\)=.*/\1/p') | less
```

## Packages

RPM Packages ( Fedora, Red Hat and like):

```sh
# install a rpm package
rpm -ivh [package.rpm]

# install a rpm package ignoring dependencies requests
rpm -ivh --nodeeps [package.rpm]

# upgrade a rpm package without changing configuration files
rpm -U [package.rpm]

# upgrade a rpm package only if it is already installed
rpm -F [package.rpm]

# remove a rpm package
rpm -e [package]

# show all rpm packages installed on the system
rpm -qa

# show all rpm packages with the name "httpd"
rpm -qa | grep httpd

# obtain information on a specific package installed
rpm -qi [package]

# show rpm packages of a group software
rpm -qg "System Environment/Daemons"

# show list of files provided by a rpm package installed
rpm -ql [package]

# show list of configuration files provided by a rpm package installed
rpm -qc [package]

# show list of dependencies required for a rpm packet
rpm -q [package] --whatrequires

# show capability provided by a rpm package
rpm -q [package] --whatprovides

# show scripts started during installation / removal
rpm -q [package] --scripts

# show history of revisions of a rpm package
rpm -q [package] --changelog

# verify which rpm package belongs to a given file
rpm -qf /etc/httpd/conf/httpd.conf

# show list of files provided by a rpm package not yet installed
rpm -qp [package.rpm] -l

# import public-key digital signature
rpm --import /media/cdrom/RPM-GPG-KEY

# verify the integrity of a rpm package
rpm --checksig [package.rpm]

# verify integrity of all rpm packages installed
rpm -qa gpg-pubkey

# check file size, permissions, type, owner, group, MD5 checksum and last modification
rpm -V [package]

# check all rpm packages installed on the system - use with caution
rpm -Va

# verify a rpm package not yet installed
rpm -Vp [package.rpm]
- `rpm -ivh /usr/src/redhat/RPMS/`arch`/[package.rpm]`: install a package built from a rpm source

# extract executable file from a rpm package
rpm2cpio [package.rpm] | cpio --extract --make-directories *bin*

# build a rpm package from a rpm source
rpmbuild --rebuild [package.src.rpm]

# List all packages by installed size (Bytes) on rpm distros
rpm -q -a --qf '%10{SIZE}\t%{NAME}\n' | sort -k1,1n
```

YUM packages tool (Fedora, RedHat and alike):

```sh
# download and install a rpm package
yum -y install [package]

# That will install an RPM, and try to resolve all the dependencies for you using your repositories.
yum localinstall [package.rpm]

# update all rpm packages installed on the system
yum -y update

# upgrade a rpm package
yum update [package]

# remove a rpm package
yum remove [package]

# list all packages installed on the system
yum list

# find a package on rpm repository
yum search [package]

# clean up rpm cache erasing downloaded packages
yum clean [package]

# remove all files headers that the system uses to resolve dependency
yum clean headers

# remove from the cache packages and headers files
yum clean all
```

DEB packages (Debian, Ubuntu and like):

```sh
# install / upgrade a deb package
dpkg -i [package.deb]

# remove a deb package from the system
dpkg -r [package]

# show all deb packages installed on the system
dpkg -l

# show all deb packages with the name "httpd"
dpkg -l | grep httpd

# obtain information on a specific package installed on system
dpkg -s [package]

# show list of files provided by a package installed on system
dpkg -L [package]

# show list of files provided by a package not yet installed
dpkg --contents [package.deb]

# verify which package belongs to a given file
dpkg -S /bin/ping

# List all packages by installed size (KBytes) on deb distros
dpkg-query -W -f='${Installed-Size;10}\t${Package}\n' | sort -k1,1n
```

APT packages tool (Debian, Ubuntu and alike):

```sh
# returns list of packages which corresponds string "searched-packages"
apt-cache search [package]

# install / upgrade a deb package from cdrom
apt-cdrom install [package]

# install / upgrade a deb package
apt-get install [package]

# update the package list
apt-get update

# upgrade all of the installed packages
apt-get upgrade

# remove a deb package from system
apt-get remove [package]

# verify correct resolution of dependencies
apt-get check

# clean up cache from packages downloaded
apt-get clean
```

Pacman packages tool (Arch, Frugalware and alike):

```sh
# Install package `name` with dependencies
pacman -S name

# Delete package `name` and all files of it
pacman -R name
```

## Monitoring / debugging

```sh
fuser
lsof
ls -l  /proc/[process id]/fd
ls -l  /proc/*/fd
for p in [0-9]*; do ls -l /proc/$p/fd ;done
strace ls
someexe > /dev/null & sudo dtruss -f -t open -p $!
inotifywait -m -r -e OPEN /path/to/traced/directory
```

auditctl
inotify
- [monitoring - List the files accessed by a program - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/18844/list-the-files-accessed-by-a-program)
- [How to determine which process is creating a file? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/13776/how-to-determine-which-process-is-creating-a-file)
- [linux - how to list files that are NOT open using find command - Server Fault](http://serverfault.com/questions/359945/how-to-list-files-that-are-not-open-using-find-command)

```sh
# Get process details for process ID 3117
/proc/3117

# Monitor messages in a log file
tail -f /var/log/messages

# Summarise/profile system calls made by command
strace -c ls >/dev/null

# Show file opens
echo exit | strace bash -li |& grep '^open'

# List system calls made by command
strace -f -e open ls >/dev/null

# Monitor what's written to stdout and stderr
strace -f -e trace=write -e write=1,2 ls >/dev/null

# List library calls made by command
ltrace -f -e getenv ls >/dev/null

# List opened files and ports
# http://en.wikipedia.org/wiki/Lsof
lsof

# List paths that process id has open
lsof -p $$

# List processes that have specified path open
lsof ~

# Show network traffic except ssh. See also tcpdump_not_me
tcpdump not port 22

# List processes in a hierarchy
ps -e -o pid,args --forest

# List processes by % cpu usage
ps -e -o pcpu,cpu,nice,state,cputime,args --sort pcpu | sed '/^ 0.0 /d'

# List processes by mem (KB) usage. See also ps_mem.py
ps -e -orss=,args= | sort -b -k1,1n | pr -TW$COLUMNS

# List all threads for a particular process
ps -C firefox-bin -L -o pid,tid,pcpu,state

# List elapsed wall time for particular process IDs
ps -p 1,$$ -o etime=

# Show system reboot history
last reboot

# Show amount of (remaining) RAM (-m displays in MB)
free -m

# Watch changeable data continuously
watch -n.1 'cat /proc/interrupts'

# Monitor udev events to help configure rules
udevadm monitor

# Active processes
ps -A

# Active processes - Tree processes
/bin/ps acxfwwwe

# Active processes - Live display
top

# List active network connections (TCP) with corresponding processes
netstat -ape
```

## System

### System information

See also `sysinfo`.

```sh
# Show name and version of distribution
head -n1 /etc/issue

# Show kernel version and system architecture
uname -a
# show architecture of machine(2)
uname -m
# show used kernel version
uname -r

# show architecture of machine
arch
# show information CPU info
cat /proc/cpuinfo
# show interrupts
cat /proc/interrupts
# verify memory use
cat /proc/meminfo
# show file(s) swap
cat /proc/swaps
# show version of the kernel
cat /proc/version
# show network adpters and statistics
cat /proc/net/dev
# show mounted file system(s)
cat /proc/mounts
# Show RAM total seen by the system
grep MemTotal /proc/meminfo
# Show CPU(s) info
grep "model name" /proc/cpuinfo
# Show PCI info
lspci -tv
# Show USB info
lsusb -tv
# Show state of cells in laptop battery
grep -F capacity: /proc/acpi/battery/BAT0/info
# Display SMBIOS/DMI information
dmidecode -q | less
```

## Power management

Aka shutdown, restart and logout of a system

```sh
# shutdown system(2)
init 0

# leaving session
logout

# reboot(2)
reboot

# shutdown system(1)
shutdown -h now

# planned shutdown of the system at 16:30
shutdown -h 16:30 &

# cancel a planned shutdown of the system
shutdown -c

# reboot
shutdown -r now

# shutdown system
telinit 0
```

## Interactive

See also linux keyboard shortcuts

```sh
# Line editor used by bash, python, bc, gnuplot, ...
readline

# Virtual terminals with detach capability, ...
screen

# Visual file manager that can browse rpm, tar, ftp, ssh, ...
mc

# Interactive/scriptable graphing
gnuplot

# Web browser
links

# open a file or url with the registered desktop application
xdg-open .
```

## Shell

- [Minimal safe Bash script template | Better Dev](https://web.archive.org/web/20201225070311/https://betterdev.blog/minimal-safe-bash-script-template/)
- [explainshell.com - match command-line arguments to their help text](https://explainshell.com/)
- [dylanaraps/pure-bash-bible: 📖 A collection of pure bash alternatives to external processes.](https://github.com/dylanaraps/pure-bash-bible)

The default shell is defined for a specific user by the file `/etc/passwd`

```sh
# List available shells
cat /etc/shells

# Clear shell cache
hash -r
```

In `/etc/bashrc` or `~/.bashrc`

```sh
# If id command returns zero, you’ve root access.
if [ $(id -u) -eq 0 ];
then you are root, set red colour prompt
	PS1="\\[$(tput setaf 1)\\]\\u@\\h:\\w\\[$(tput sgr0)\\]"
else normal
	PS1="[\\u@\\h:\\w] $"
fi
```

- [How to: Change / Setup bash custom prompt (PS1)](http://www.cyberciti.biz/tips/howto-linux-unix-bash-shell-setup-prompt.html)

### Shell config

```sh
# Display current shell prompt setting
echo $PS1
# Change current shell prompt setting
export PS1="..."
export PS1="\[\033[0m\]\[\033[0;30;47m\] \u\[\033[0m\]\[\033[0;30;47m\]@\h\[\033[0m\] \w\n\[\033[1;32m\] \@ \$ \[\033[0m\]"
export PS1="[${LOGNAME}@$(hostname)]"
```

Defined by (in order):

1. (global system) `/etc/profile`
2. (global system) `/etc/bashrc`
3. (user) `~/.bash_profile`
4. (user) `~/.bash_login`
5. (user) `~/.profile`
6. (user) `~/.bashrc`
7. (user) `~/.bash_logout` au logout

(and `/etc/bash.bashrc`, `/etc/bash.bashrc.local`?)

To reload a configuration file (here the file `~/.bashrc`)

```sh
source ~/.bashrc
# or
. ~/.bashrc
```

By convention, the prompt ends with `$` for users and by `#` for root

- [Bash prompt basics](http://linuxconfig.org/Bash_prompt_basics)
- [Shell startup scripts — flowblok’s blog](https://blog.flowblok.id.au/2013-02/shell-startup-scripts.html)

### Command alias

```sh
# quick dir listing
alias l='ls -l --color=auto'
```

### Programmable bash completions

See `complete` buildin command

- [iridakos - Creating a bash completion script](https://iridakos.com/tutorials/2018/03/01/bash-programmable-completion-tutorial)
- [git/git-completion.bash at master · git/git](https://github.com/git/git/blob/master/contrib/completion/git-completion.bash)
- [Bash Reference Manual: Programmable Completion](https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion.html#Programmable-Completion)
- [Bash Reference Manual: Programmable Completion Builtins](https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins.html#Programmable-Completion-Builtins)
- [Bash Reference Manual: A Programmable Completion Example](https://www.gnu.org/software/bash/manual/html_node/A-Programmable-Completion-Example.html#A-Programmable-Completion-Example)
- [Bash Reference Manual: Bash Variables](https://www.gnu.org/software/bash/manual/html_node/Bash-Variables.html#Bash-Variables)

### Terminal history auto complete

In `~/.inputrc` or `/etc/inputrc`:

```sh
# History auto complete with "start with" filter
"\e[5~": history-search-backward
"\e[6~": history-search-forward
set show-all-if-ambiguous on
set completion-ignore-case on
```

- http://www.gnu.org/software/bash/manual/html_node/Readline-Init-File.html
- https://stackoverflow.com/questions/1030182/how-do-i-change-bash-history-completion-to-complete-whats-already-on-the-line

On OSX Page up and Page down in Terminal are by default use to manipulat buffer instead to send key stroke

You can change it in `Preferences → Settings → Keyboard`:

- Page down : `\033[6~`
- Page up : `\033[5~`
- End : `\033OF` (works in vi, vim, etc.) ou `\033[4~`, `\033[F`, `\005`
- Home : `\033OH` (works in vi, vim, etc.) ou `\033[1~`, `\033[H`, `\001`

Use esc to type these strings (add `\033` in input field) or past (via the context menu)

### Shell variables

```sh
env
```

### Colors and control sequences

For `ls` colors:

```sh
export CLICOLOR=1
export TERM=xterm-color
export LSCOLORS=DxFxcxdxBxegedbxHxacHd
```

`key=effect;foreground colour;background colour` separated by `:`.

Ex.: a symlink bright pink `ln=01;95;40` give:

```sh
export LS_COLORS="di=01;33;40:ln=01;95;40"
```

To known color config:

```sh
man ls
```

- [LSCOLORS Generator](https://web.archive.org/web/20201212101406/https://geoff.greer.fm/lscolors/)
- [Configuring LS_COLORS](https://web.archive.org/web/20201112025523/http://www.bigsoft.co.uk/blog/2008/04/11/configuring-ls_colors)

```sh
#
# Dont forget to call ~/.bashrc in your ~/.profile script
#

export CLICOLOR=1
alias ll='ls -l'
alias la='ls -A'
alias vi='vim'
alias l='ls -CF'

function cyan_red_prompt {
	local CYAN="\[\033[0;36m\]"
	local GRAY="\[\033[0;37m\]"
	local RED="\[\033[0;31m\]"
	PS1="${CYAN}[\u@\h ${RED}\w${CYAN}]${GRAY} "
}

cyan_red_prompt
```

- [TIL: Moving the terminal cursor](https://ddfreyne.github.io/til/2016/12-03-terminal-cursor-movement/)
- [danyspin97's site - Colorize your CLI](https://danyspin97.org/blog/colorize-your-cli/)

### Command alias

```sh
alias NICKNAME='COMMAND -withargs'
```

A ajouter dans `~/.bashrc`

- [Create cmd aliases in Windows | Displayobject](https://web.archive.org/web/20200918172228/http://www.displayobject.fr/2010/03/07/create-cmd-aliases-in-windows/)

### Shell script file

Create a shell script `file.sh` the execute the following command to allow it to be executable:

```sh
chmod +x /path/to/file.sh
```

Celui-ci devra contenir un shebang sur la première ligne indiquant quel interpréteur var être utilisé pour executer le contenu du fichier.

```sh
#!/bin/sh
```

Les plus courant sont `sh`, `php`, `python` ou encore `perl`.

- http://en.wikipedia.org/wiki/Shebang_%28Unix%29

Il est possible d'être générique, et de ne pas indiquer directement le chemin de l'interpréteur :

```sh
#!/usr/bin/env php
```

- http://en.wikipedia.org/wiki/Shebang_%28Unix%29#Portability

Include shell script into an other

```sh
source /path/to/script.sh
```

But it's relative to execution path, not current script path.

So use this instead:

```sh
source $(dirname $0)/script.sh
```

Or:

```sh
CURRENT_DIR=`dirname $0`
$CURRENT_DIR/script.sh
```

Node shebang:

```sh
#!/usr/bin/env node
```

Or use if support system with nodejs instead of node. (`:` command in bash is noop)

```sh
#!/usr/bin/env sh
':' //; exec "$(command -v nodejs || command -v node)" "$0" "$@"

console.log('Hello world!');
```

- [scripting - Universal Node.js shebang? - Unix & Linux Stack Exchange](http://unix.stackexchange.com/questions/65235/universal-node-js-shebang)

### Shell script syntax

Use `$( )`, and don't use \`\` anymore: [Bash FAQ 82](http://mywiki.wooledge.org/BashFAQ/082).

Avoid using UPPERCASE variable names. That namespace is generally reserved by the shell for special purposes (like `PATH`), so using it for your own variables is a bad idea.

Escape special char in argument:

```sh
command $'\t'
```

Wildcard files:

```sh
for file in *.ext1; do echo "${file} ${file/.ext1/.ext2}"; done
```

```sh
ls file_*{.png,.jpg}
```

File [Wildcards](http://www.tldp.org/LDP/GNU-Linux-Tools-Summary/html/x11655.htm#STANDARD-WILDCARDS)

Brace expansion

```sh
sudo mv /path/file{,.old}
sudo ln {/path1,/path2}/file
```

- [Bash Reference Manual: Brace Expansion](https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion.html)



### Redirection

File pointer and file redirection

- [BashGuide/InputAndOutput - Greg's Wiki](http://mywiki.wooledge.org/BashGuide/InputAndOutput#Redirection)
- [I/O Redirection](http://tldp.org/LDP/abs/html/io-redirection.html)
- [Bash scripting quirks & safety tips - Julia Evans](http://jvns.ca/blog/2017/03/26/bash-quirks/)
- named pipe (`mkfifo`)

```sh
while read item; do
	echo $item
done < sql.res
```

Bash support [process substitution](https://www.gnu.org/software/bash/manual/html_node/Process-Substitution.html#Process-Substitution):

```sh
cat <(echo "tmp file content")
```

Is similar to: `echo hello > file; cat file; rm file`

`$(cat file)` is same as `$(< file)`

```sh
cat <<< hello

diff <(cd dir1; ls) <(cd dir2; ls)

(
	echo open ip_address
	echo user username password
	echo put -O $today $file_gnome_curr
	echo bye
) | lftp -f /dev/stdin >> lftp.log 2>&1
```
Here-doc & here-string:

```sh
cat > /path/to/file << EOF
Some thing.
Blahblah!
$somevar
EOF

cat > /path/to/file <<< "Some thing."

cat <<EOF
test1
test2
EOF

(cat <<'EOF'
file1
file2
EOF
) | while read -r file; do
	cp "from/$file" "to/$file";
done;

cat <<EOF >> greetings.txt
line 1
line 2
EOF

# Here-doc to var
read -r -d '' MYVAR <<'EOF'
abc'asdf"
$(dont-execute-this)
foo"bar"''
EOF
```

- [How to assign a heredoc value to a variable in Bash? - Stack Overflow](https://stackoverflow.com/questions/1167746/how-to-assign-a-heredoc-value-to-a-variable-in-bash)

File descriptors (fd) :

- 0 is `stdin` IN
- 1 is `stdout` OUT
- 2 is `stderr` ERROR

`2>&1` redirects fd 2 to 1 (`stderr` to `stdout`)

```sh
# Empty a file (ex: clean a log file)
> /var/log/apache2/error.log

# Append to a file
echo "Appended text" >> /path/file

# Log all infos (and erros) of following commands to a file `/tmp/log.txt`
( /bin/ps acxfwwwe 2>&1; /usr/sbin/lsof -Pwln 2>&1; /bin/netstat -anpe 2>&1; /usr/bin/lastlog 2>&1; /usr/bin/last 2>&1; /usr/bin/who -a 2>&1 ) > /tmp/log.txt
```

- `man -P less\ +/^REDIRECTION bash`
- http://www.tldp.org/LDP/Bash-Beginners-Guide/html/Bash-Beginners-Guide.html#sect_08_02_03_02
- [In the bash shell, what is "2>&1"](https://stackoverflow.com/questions/818255/in-the-bash-shell-what-is-21)
- `/usr/include/unistd.h`
- http://en.wikipedia.org/wiki/File_descriptor
- [bash - How to pipe stderr, and not stdout? - Stack Overflow](https://stackoverflow.com/questions/2342826/how-to-pipe-stderr-and-not-stdout)

Pipe:

- [Pipeline (Unix) — Wikipedia](https://en.wikipedia.org/wiki/Pipeline_%28Unix%29)

### Fork process

Execute in background

> If a command is terminated by the control operator &, the shell executes the command in the background in a subshell

```sh
echo '' > .mycmd.pid
mycmd & echo "$!" >> .mycmd.pid
# ... later
cat .mycmd.pid | xargs -n 1 kill -9
```

### Add a bin folder to global executables

Pour éviter de tapper le chemin entier vers les commandes / executables

```sh
PATH=$PATH:/path/bindir
export PATH
```

```sh
PATH=$PATH:/path/bindir command-use-path
PATH=$PATH:/path/bindir bash -c 'echo $PATH'
PATH=$PATH:/path/bindir bash -c 'command1 | command2'
(export PATH=$PATH:/path/bindir; command1 | command2)
```

Pour l'ajouter de façon permanente, l'écrire dans `~/.profile` ou `~/.bashrc`

- [Path (variable) - Wikipedia](http://en.wikipedia.org/wiki/Path_%28variable%29)

### Dotfiles

- [mathiasbynens/dotfiles: .files, including ~/.macos — sensible hacker defaults for macOS](https://github.com/mathiasbynens/dotfiles)

### Tree navigation

```sh
# Enter to directory `/home`
cd /home
# Go back one level
cd ..
# Go back two levels
cd ../..
# Go to home directory
cd
# Go to home directory
cd ~user1
# Go to previous directory
cd -

# Get the current working directory
pwd
```

## Directory navigation

```sh
# Go to previous directory
cd -

# Go to $HOME directory
cd

# Go to dir, execute command and return to current dir
(cd dir && command)

# Put current dir on stack so you can popd back to it
pushd .
```

## Files and folders operations

File name:

> Using `sed` or other external processes to do simple string operations like stripping extensions and prefixes is inefficient. Instead, use parameter expansions which are part of the shell (no external process means it will be faster). Some helpful articles on the subject are listed below:
>
> [Bash FAQ 73](http://mywiki.wooledge.org/BashFAQ/073): Parameter expansions
> [Bash FAQ 100](http://mywiki.wooledge.org/BashFAQ/100): String manipulations

### File searching

Find support [shell pattern](https://www.gnu.org/software/findutils/manual/html_mono/find.html#Shell-Pattern-Matching) for `-path` and `-ipath` parameters:

- `*/file.ext`
- `*.ext`
- `*/file.*`

- [bash - How do I make find fail if -exec fails? - Ask Different](https://apple.stackexchange.com/questions/49042/how-do-i-make-find-fail-if-exec-fails)

```sh
# Find all files that have been modified in the past 7 days
find . -type f -mtime -7

# Search binary files are not used in the last 100 days
find /usr/bin -type f -atime +100

# Find all JPEGs that have been modified more than 30 days ago
find . -name \*.jpg -mtime +30

# Move all JPEGs from the current folder (recursively) that are greater than 40k into the folder /tmp/2
find . -name \*.jpg -size +40k -exec mv {} /tmp/2 +

# search files and directories belonging to `user1`
find / -user user1

# List files by date. See also newest and find_mm_yyyy
ls -lrt

# Print in 9 columns to width of terminal
ls /usr/bin | pr -T9 -W$COLUMNS

# Search 'expr' in this dir and below. See also findrepo
find -name '*.[ch]' | xargs grep -E 'expr'

# Search all regular files for 'example' in this dir and below
find -type f -print0 | xargs -r0 grep -F 'example'

# Search all regular files for 'example' in this dir
find -maxdepth 1 -type f | xargs grep -F 'example'

# Process each item with multiple commands (in while loop)
find -maxdepth 1 -type d | while read dir; do echo $dir; echo cmd2; done

find ./ -name "tile_*.png" -exec bash -c 'filename="$1";echo "${filename%.*}"' _ {} \;

# search files with `.bin` extension within directory `/home/user1`
find /home/user1 -name \*.bin

# Search files with `.rpm` extension and modify permits
find / -name *.rpm -exec chmod 755 '{}' \;

# Search files with `.rpm` extension ignoring removable partitions as cdrom, pen-drive, etc.…
find / -xdev -name \*.rpm

# Find files with the `.ps` extension - first run `updatedb` command
locate \*.ps

#Search cached index for names. This re is like glob *file*.txt
locate -r 'file[^/]*\.txt'

# Find files not readable by all (useful for web site)
find -type f ! -perm -444

# Find dirs not accessible by all (useful for web site)
find -type d ! -perm -111

# Search for empty files and folder (or file with only whitespaces)
find -empty
```

- [bash - Find and replace filename recursively in a directory - Stack Overflow](https://stackoverflow.com/questions/9393607/find-and-replace-filename-recursively-in-a-directory/9394625#9394625)

```sh
# Use a simple shell loop, to process each of the images.
mkdir thumbnails
for f in *.jpg
do convert $f -thumbnail 200x90 thumbnails/$f.gif
done

# Use find to substitute filenames into a 'convert' command.
# This also provides the ability to recurse though directories by removing
# the -prune option, as well as doing other file checks (like image type,
# or the disk space used by an image).
find * -prune -name '*.jpg' \
	-exec  convert '{}' -thumbnail 200x90 thumbnails/'{}'.gif \;

# Use xargs -- with a shell wrapper to put the argument into a variable
# This can be combined with either "find" or "ls" to list filenames.
ls *.jpg | xargs -n1 sh -c 'convert $0 -thumbnail 200x90 thumbnails/$0.gif'

# An alternative method on linux (rather than plain unix)
# This does not need a shell to handle the argument.
ls *.jpg | xargs -r -I FILE convert FILE -thumbnail 200x90 FILE_thumb.gif

# Quickly search (sorted) dictionary for prefix
look reference

# Highlight occurances of regular expression in dictionary
grep --color reference /usr/share/dict/words
```

- [command line - How to find all empty files and folders in a specific directory including files which just look empty but are not? - Ask Ubuntu](https://askubuntu.com/questions/719912/how-to-find-all-empty-files-and-folders-in-a-specific-directory-including-files)
- [unix - Appending new lines to multiple files - Super User](https://superuser.com/questions/1327969/appending-new-lines-to-multiple-files/1327980#1327980) - How to use `echo "test" >> {}` within find exec

#### Find missing files

- [How do I find which files are missing from a list? - Unix & Linux Stack Exchange](http://unix.stackexchange.com/questions/11989/how-do-i-find-which-files-are-missing-from-a-list)

#### Find duplicates files

	find -not -empty -type f -printf "%s\n" | sort -rn | uniq -d | xargs -I{} -n1 find -type f -size {}c -print0 | xargs -0 md5sum | sort | uniq -w32 --all-repeated=separate | awk '{$1=""; print substr($0,2)}'

- [diff - Wikipedia](https://en.wikipedia.org/wiki/Diff)
- [How do I do a binary diff on two identically sized files under Linux? - Super User](https://superuser.com/questions/135911/how-do-i-do-a-binary-diff-on-two-identically-sized-files-under-linux)
- [shell - Finding duplicate files according to md5 with bash - Stack Overflow](https://stackoverflow.com/questions/19551908/finding-duplicate-files-according-to-md5-with-bash)

Remove duplicates

```sh
#!/bin/bash
gawk '
  {
    cmd="md5 -r " q FILENAME q
    cmd | getline cksm
    close(cmd)
    sub(/ .*$/,"",cksm)
    if(a[cksm]++){
      cmd="rm " q FILENAME q
      system(cmd)
      close(cmd)
    }
    nextfile
  }' q='"' *
```

- [bash - How to remove duplicated files in a directory? - Super User](http://superuser.com/questions/386199/how-to-remove-duplicated-files-in-a-directory/386209#386209)

[Rdfind – redundant data find](https://rdfind.pauldreik.se/):

```sh
rdfind -makehardlinks true

fdupes

find -not -empty -type f -printf "%s\n" | sort -rn | uniq -d | xargs -I{} -n1 find -type f -size {}c -print0 | xargs -0 md5sum | sort | uniq -w32 --all-repeated=separate
```

BTRFS [Deduplication - btrf Wiki](https://btrfs.wiki.kernel.org/index.php/Deduplication)

See also `diff -q --binary` or `cmp -s $1 $2 && echo "identical" || echo "different"`

- [Comparing and Merging Files](http://www.gnu.org/software/diffutils/manual/diffutils.html#Binary)
- [centos - What's the quickest way to find duplicated files? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/277697/whats-the-quickest-way-to-find-duplicated-files/277767#277767)

	```sh
	find -not -empty -type f -printf "%s\n" | sort -rn | uniq -d | xargs -I{} -n1 find -type f -size {}c -print0 | xargs -0 md5sum | sort | uniq -w32 --all-repeated=separate
	```

	Replace the use of md5sum with `diff` or `cmp`: [How do I do a binary diff on two identically sized files under Linux? - Super User](https://superuser.com/questions/135911/how-do-i-do-a-binary-diff-on-two-identically-sized-files-under-linux)
- [dupe-krill/README.md at master · kornelski/dupe-krill](https://github.com/kornelski/dupe-krill/blob/master/README.md)
- [idealo/imagededup: 😎 Finding duplicate images made easy!](https://github.com/idealo/imagededup)
- [birkenfeld/fddf: Fast data dupe finder](https://github.com/birkenfeld/fddf)
- [haibison / scan4df — Bitbucket](https://bitbucket.org/haibison/scan4df/src/master/)

Then replace files by [hardlink](#hard-link)

- [Is there an easy way to replace duplicate files with hardlinks? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/3037/is-there-an-easy-way-to-replace-duplicate-files-with-hardlinks)
- [hardlink - Finding files that are *not* hard links via a shell script - Stack Overflow](https://stackoverflow.com/questions/16282618/finding-files-that-are-not-hard-links-via-a-shell-script)

#### Find all files by content

```sh
# Find multiple exec a executed only if the previous one exit with 0 https://stackoverflow.com/questions/5119946/find-exec-with-multiple-commands#comment34296391_6043896
find -type f -iname "*.properties" -exec grep -q -i -E '^abtest=false$' {} \; -print
find -type f -iname "*.properties" -exec grep -q -i -E '^abtest=' {} \; -exec sed -i 's/^abtest=.*/abtest=true/i' {} \; -print

# Use test to inverse the grep exit value https://stackoverflow.com/a/30495279/470117 (-v/--invert-match option is not useful for that case), for that we need also sh interpreter to use builtin test command
# For append mode (redirection), need to use sh interpreter directly, else {} will be interpreted directly by Bash. See https://superuser.com/questions/1327969/appending-new-lines-to-multiple-files/1327980#1327980
# -exec sh -c 'echo "command name: $0, first arg: $1"' test {} \;
find -iname "*.properties" -exec sh -c 'grep -q -i -E "^abtest=" $1; test $? -eq 1' match {} \; -exec sh -c 'echo -e "\n\nabtest=true" >> $1' append {} \; -print

find -iname "*.properties" -type f -print0 | xargs -0 grep -EHi '^abtest='
# Same as (flexibity of find vs glob include/exclude filters):
grep -EHir --include="*.properties" '^abtest=' /path/to/dir
grep -ir  --include=\*.{php,js,css} "/api/v1/"

# Example search in all .less files that contains `url("<url>")` or `url('<url>')` or `url(<url>)`
find "$wd" -iname "*.less" \( -not -ipath "*/node_modules/*" \) -type f -print0 | xargs -0 grep -EliZ 'url\(('"'"'|"|)(.*?)\1\)' | xargs -0 -n1 echo "Do something with that file:"
```

- [find -exec vs find | xargs](https://www.everythingcli.org/find-exec-vs-find-xargs/)

### Create archive from file list

```sh
#!/bin/bash
# Create temp list
list=$(mktemp "/tmp/archive_list.XXXXXXXXXX")
# Write stdin file / folder list
cat > "$list"
# Get destination folder based on first file / folder
first=$(head -n 1 "$list")
folder=$(dirname "$first")
# Temporary file and final file
final="$folder/Archive.zip"
file="$final.tmp"
# Create archive file (zip, ultra)
/opt/local/bin/7z a -tzip -mx=9 "$file" @"$list"
# Move to final destination
mv "$file" "$final"
# Remove temp list
rm "$list"
```

### Copy files from m3u playlist

```sh
# Extract music from m3u (ignore lines start with #, whitespace or are empty)
# Playlists entries could be relative
cd "/path/to/playlists"
cat "playlist1.m3u" "playlist1.m3u" "playlist3.m3u" | grep "^[^# \t]" | tr -s '\n' | while read -r line; do cp --parent -v "$line" /destination; done
```

### Get extensions of all files

```sh
find . -type f | while read file; do filename=$(basename "$file"); ext=$([[ "$filename" = *.* ]] && echo ".${filename##*.}" || echo ''); echo $ext; done | sort | uniq
```

### File checksum

```sh
# SHA256, used in chef cookbooks
openssl dgst -sha256 path/to/myfile

# MD5
openssl dgst -md5 path/to/myfile
```

### Split files

FAT32 maximum file size is ["4 GiB minus 1 byte"](https://en.wikipedia.org/wiki/File_Allocation_Table#FAT32) (4294967295 bytes)

To write file with a size larger than that limit, you need to split it.

In destination folder, execute following command:

```sh
split -b 4294967295 example.dmg example.dmg.part.
```

(the part `example.dmg.part.` will be used to name output files like `example.dmg.part.aa`, `example.dmg.part.ab` and so on)

```sh
cat example.dmg.part.* > example.dmg
```

### Mass rename

https://stackoverflow.com/questions/417916/how-to-do-a-mass-rename

```sh
for i in 'Ref_00'*.jpg; do mv $i $(echo $i | sed 's/Ref_00/anim/'); done;

# Will rename `Ref_00001.jpg` to `anim001.jpg`
find . -name 'Ref_00*.jpg' -prune -print | while read i; do mv $i $(echo $i | sed 's/Ref_00/anim/'); done;

# Will rename `sprite1.png` to `sprite0.png` (if change the offset, be careful of sort order)
find . -maxdepth 1 -type f -exec mv "{}" "{}.tmp" \; -print | awk 'match($0,"^(.*atlas-)([0-9]+)(.*)$",a){print "\""a[1]a[2]a[3]".tmp\" \""a[1]a[2]-1a[3]"\""}' | while read args; do eval "mv $args"; done
```

With `rename`:

```sh
# Rename *.JPG to *.jpg
rename 's/\.JPG/\.jpg/' *.JPG
# Strip spaces
rename 's/ //' *.jpg
# Lower case
rename 'y/A-Z/a-z/' *
```

On macOS install it with port `port install p5-file-rename` (but should use the cmd `rename-5.22` where `22` is installed version via port instead of `rename`) or brew `brew install rename`

### Remove files

```sh
rm -f file1 file2

find . -name 'tile_*.png' -delete

# Remove all files with exceptions:
find . -type f -not \( -name '*.php' -or -name '*.iso' \) -exec rm {} \;

# With a list of exceptions:
find . -type f -printf "%P\n" ! -name "list.txt" | fgrep -vf list.txt | xargs -r rm
```

- http://www.cyberciti.biz/faq/linux-bash-delete-all-files-in-directory-except-few/
- [unix - BASH: How to remove all files except those named in a manifest? - Stack Overflow](https://stackoverflow.com/questions/2782602/bash-how-to-remove-all-files-except-those-named-in-a-manifest)
- [linux - find files not in a list - Stack Overflow](https://stackoverflow.com/questions/7306971/find-files-not-in-a-list)

### Remove empty dir

```sh
find <path> -type d -empty -delete

find <path> -type d -empty -print0 | xargs -0 -I {} rmdir "{}"

find <path> -type d -print0 | xargs -0 -r rmdir -p --ignore-fail-on-non-empty

# or
# handle trailing dot rmdir error: rmdir -p "./test" -> rmdir: failed to remove directory '.': Invalid argument
find -mindepth 1 -type d -printf '%P\0' | xargs -0 -r rmdir -p --ignore-fail-on-non-empty

# find all dirs in reverse order (depth first), remove empty dir to top
find -mindepth 1 -type d -print0 | tac -s $'\0' | xargs -0 -r rmdir --ignore-fail-on-non-empty
```

- [Unix tip: Recursively removing empty directories | Network World](https://www.networkworld.com/article/2773290/unix-tip--recursively-removing-empty-directories.html)

### Change file extension

```sh
for j in /path/dir/*.html
do
	n=${j/.html}
	mv "$j" "$n.php"
done

# Other way:
for j in *; do mv "$j" "$n.bin"; done;
```

### Hard link

Aka hardware link

It's not possible to create hardlink with a directory (due to the risk of loops in tree)

```sh
# Create hardlink
ln /path/to/source_file /path/to/target_file
ln -T /etc/apache2/sites-available/example.com /etc/apache2/sites-enabled/example.com

# Remove file link
unlink /etc/apache2/sites-enabled/websiteA.exemple
```

### Symbolic link

```sh
# create a symbolic link to file or directory
ln -s file1 lnk1
```

### Read write race condition

```sh
cat tmp | head -1 >new && mv new tmp
{ cat tmp | head -1; } >tmp
```

- [bash - How to make reading and writing the same file in the same pipeline always "fail"? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/409893/how-to-make-reading-and-writing-the-same-file-in-the-same-pipeline-always-fail/409896#409896)

### Choose incremental filename

Test if `dirB/file.ext` exist else choose dest file name as `dirB/file-1.ext`, if already exist choose `dirB/file-2.ext` and so one

```sh
source=dirA/file.ext
dest_dir=dirB

file=$(basename file.ext)
basename=${file%.*}
ext=${file##*.}

if [[ ! -e "$dest_dir/$basename.$ext" ]]; then
	# file does not exist in the destination directory
	mv "$source" "$dest_dir"
else
	num=2
	while [[ -e "$dest_dir/$basename-$num.$ext" ]]; do
		(( num++ ))
	done
	mv "$source" "$dest_dir/$basename-$num.$ext"
fi
```

### File type

```sh
# Get file type if known by libmagic
file --mime /path/file

# Get information about files in the current folder
find . -maxdepth 1 -type f -exec file "{}" \;
```

Supported formats are listed by:

- files in `/etc/magic`
- `/etc/magic.mime`
- `/usr/share/misc/magic.mgc`
- `/usr/share/file/magic.mgc`
- `/opt/local/share/misc/magic.mgc`
- files in `/opt/local/share/misc/magic`
- `~/.magic.mgc`
- `~/.magic`

The extension of compiled magic: `*.mgc`

### Test if a file exist

```sh
#!/bin/bash
filename=$1
if [ -f $filename ]
then
	echo "$filename exists"
else
	echo "$filename does NOT exist"
fi
```

### Name, extension and parent folder

**Note: Don't use parameter substitution, it's not work with all cases**

```sh
folder=/tmp
dirname "$folder"
# /
basename "$folder"
# tmp
echo "${folder%/*}"
#
echo "${folder%/*.*}"
# /tmp
echo "${folder##*/}"
# tmp
echo "${folder##*.}"
# /tmp

folder2=/tmp/folder
dirname "$folder2"
# /tmp
basename "$folder2"
# folder
echo "${folder2%/*}"
# /tmp
echo "${folder2%/*.*}"
# /tmp/folder
echo "${folder2##*/}"
# folder
echo "${folder2##*.}"
# /tmp/folder

file=/tmp/file.png
dirname "$file"
# /tmp
basename "$file"
# file.png
echo "${file%/*}"
# /tmp
echo "${file%/*.*}"
# /tmp
echo "${file##*/}"
# file.png
echo "${file##*.}"
# png
```

```sh
extension=$([[ "$file" = *.* ]] && echo "${file##*.}" || echo '')
```

- [Parameter Substitution](http://www.tldp.org/LDP/abs/html/parameter-substitution.html)
- [Bash Reference Manual: Shell Parameter Expansion](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html)
- [bash - Get file directory path from filepath - Stack Overflow](https://stackoverflow.com/questions/6121091/get-file-directory-path-from-filepath)
- [string - Extract filename and extension in Bash - Stack Overflow](https://stackoverflow.com/questions/965053/extract-filename-and-extension-in-bash)

### Delete all Unix hidden files

```sh
# All files or folders that start with `.`, like `.htaccess` or `.DS_STORE`
rm -rf .[^.]*

# All files dir `.git`
find . -type d -name ".git" -exec rm -rf {} +
```

### Affichage de fichier / flux

```sh
# Affichage
cat /path/file

# Pageurs (affichage page par page) :
less /path/file
# ou
more /path/file

# Affichage en live des modifications:
tail -f /path/file
```

### List all folders and files

```sh
# Ordered by size :
du -ak . | sort -nr | less

# List top 10 largest files and directories
du -a /var | sort -n -r | head -n 10
```

### Find text in files

```sh
# Find text in files:
grep -rn "texttofind" *
grep "string text to find in all files" . -R
```

### Create or truncate a file

```sh
# Create or tuncate a file
> /var/log/apache2/error.log
# Create an empty file or change the modification date
touch file.ext

# Create a large test file (taking no space)
dd bs=1 seek=2TB if=/dev/null of=file.ext
```

### Copy file

```sh
# Copying a file
cp file1 file2
# copy all files of a directory within the current work directory
cp dir/* .
# copy a directory within the current work directory
cp -a /tmp/dir1 .
# copy a directory
cp -a dir1 dir2
# outputs the mime type of the file as text
cp file file1
```

### File comparaisons

Note: you can export LANG=C for speed. Also these assume no duplicate lines within a file

```sh
# Union of unsorted files
sort file1 file2 | uniq

# Intersection of unsorted files
sort file1 file2 | uniq -d

# Difference of unsorted files
sort file1 file1 file2 | uniq -u

# Symmetric Difference of unsorted files
sort file1 file2 | uniq -u

# Union of sorted files
join -t'\0' -a1 -a2 file1 file2

# Intersection of sorted files
join -t'\0' file1 file2

# Difference of sorted files
join -t'\0' -v2 file1 file2

# Symmetric Difference of sorted files
join -t'\0' -v1 -v2 file1 file2
```

### Use diff and patch

Compare 2 folders:

Sans `-q` mais avec `-u` pour faire un patch

```sh
diff -rq /path/dirA /path/dirB
```

Et sans prendre en compte les fichiers metadonnées d'OSX et de Windows, le tout ordonné :

```sh
diff -uqr /path/dirA /path/dirB | grep -v -e 'DS_Store' -e 'Thumbs' | sort
```

Comparer 2 files:

```sh
diff -u /path/fileA /path/fileB
```

- [The Ten Minute Guide to diff and patch](http://jungels.net/articles/diff-patch-ten-minutes.html)

Apply a patch:

```sh
patch -i my.patch
```

Use heredoc

```sh
patch -i -p1 - <<EOF
diff -ur a/Makefile.in b/Makefile.in
--- a/Makefile.in	2016-03-13 01:08:14.000000000 +0100
+++ b/Makefile.in	2016-03-13 01:09:13.000000000 +0100
@@ -1,3 +1,4 @@
+vpath = src
 top_builddir = ..
 srcdir = @srcdir@
 top_srcdir = @top_srcdir@
EOF
```

Use `-p1` to strip path `a/` and `b/`

### Folder bind

Aka folder link, like symlink but for folder (standart implementation don't allow to link folder)

```sh
# Mount a folder at a specific point (here `/path/destdir`)
mount --bind /path/srcdir /path/destdir
# Unmount
umount /path/destdir
```

The mount point is registerd in `/etc/fstab` as `fs-type`: `bind`

### Archives and compression

```sh
# Encrypt file
gpg -c file

# Decrypt file
gpg file.gpg

# Make compressed archive of dir/
tar -c dir/ | bzip2 > dir.tar.bz2

# Extract archive (use gzip instead of bzip2 for tar.gz files)
bzip2 -dc dir.tar.bz2 | tar -x

# Make encrypted archive of dir/ on remote machine
tar -c dir/ | gzip | gpg -c | ssh user@remote 'dd of=dir.tar.gz.gpg'

# Make archive of subset of dir/ and below
find dir/ -name '*.txt' | tar -c --files-from=- | bzip2 > dir_txt.tar.bz2

# Make copy of subset of dir/ and below
find dir/ -name '*.txt' | xargs cp -a --target-directory=dir_txt/ --parents

# Copy (with permissions) copy/ dir to /where/to/ dir
( tar -c /dir/to/copy ) | ( cd /where/to/ && tar -x -p )

# Copy (with permissions) contents of copy/ dir to /where/to/
( cd /dir/to/copy && tar -c . ) | ( cd /where/to/ && tar -x -p )

# Copy (with permissions) copy/ dir to remote:/where/to/ dir
( tar -c /dir/to/copy ) | ssh -C user@remote 'cd /where/to/ && tar -x -p'

# Backup harddrive (raw) to remote machine
dd bs=1M if=/dev/sda | gzip | ssh user@remote 'dd of=sda.gz'
```

### Incremental listing

Incrementaly add/changed/delete files (list made from `cron` or similar)

```sh
find . -type f -mtime -7 -exec ls -l {} \; > list.txt
find . -type f -exec ls -i {} + | sort -k2 > list.txt
tar --create --file=archive.1.tar --listed-incremental=/var/log/usr.snar .
tar -cf /dev/null -g /var/log/usr.snar .
date +%s
```

```sh
/backupdevice/folder
date +%s%N > /backupdevice/folder.index
```

- [Introduction to Inodes!](https://web.archive.org/web/20201112021029/https://www.grymoire.com/Unix/Inodes.html)
- [inodes – ctime, mtime, atime | *nix Shell](https://web.archive.org/web/20200805044513/https://nixshell.wordpress.com/2010/10/07/inodes-ctime-mtime-atime/)
- [timestamps - On what occasion will inode change? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/31255/on-what-occasion-will-inode-change)
- [linux - Find the files that have been changed in last 24 hours - Stack Overflow](https://stackoverflow.com/questions/16085958/find-the-files-that-have-been-changed-in-last-24-hours)
- [rsync - How to diff two folders by inodes - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/57825/how-to-diff-two-folders-by-inodes)
- [command line - List all recently changed files (recursive) - Ask Ubuntu](https://askubuntu.com/questions/704160/list-all-recently-changed-files-recursive)
- [bash - Show both ctime and atime in ls output - Super User](https://superuser.com/questions/234158/show-both-ctime-and-atime-in-ls-output)
- [backup - Incremental file back up by date - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/132819/incremental-file-back-up-by-date)

- [GNU tar 1.32: 5.2 Using tar to Perform Incremental Dumps](https://www.gnu.org/software/tar/manual/html_node/Incremental-Dumps.html)
- [GNU tar 1.32: Format of the Incremental Snapshot Files](https://www.gnu.org/software/tar/manual/html_node/Snapshot-Files.html)
- [linux - Updating tar.gz daily only with changed files - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/25541/updating-tar-gz-daily-only-with-changed-files)
- [archive - Linux tar - just create the .snar file - Stack Overflow](https://stackoverflow.com/questions/27763248/linux-tar-just-create-the-snar-file)
- [A quick guide to backups using tar | TuxRadar Linux](https://web.archive.org/web/20180322022053/http://www.tuxradar.com/content/quick-guide-backups-using-tar)
- [Backup Linux to NTFS Using GNU tar](https://web.archive.org/web/20201030053025/http://chxo.com/be2/tar_backup_to_ntfs.html)

### Change encoding

Use `recode` that obsoletes iconv, dos2unix, unix2dos

```sh
# Show available conversions (aliases on each line)
recode -l
#iconv -l

# Windows "ansi" to local charset (auto does CRLF conversion)
recode windows-1252.. file_to_change.txt

# Windows utf8 to local charset
recode utf-8/CRLF.. file_to_change.txt

# Latin9 (western europe) to utf8
recode iso-8859-15..utf8 file_to_change.txt
#iconv -f iso-8859-15 -t utf-8 <infile> -o <outfile>

# Base64 encode / decode
recode ../b64 < file.png

# Quoted printable decode
recode /qp.. < file.qp > file.txt

# Text to HTML
recode ..HTML < file.txt > file.html

# Lookup table of characters
recode -lf windows-1252 | grep euro

# Convert a text file format from MSDOS to UNIX (line-ending CRLF to LF)
recode ibmpc..latin1 file file2
#dos2unix file file2
#cat file | tr -d '\r' > file2 && mv -v file2 file
#sed -i s/\r//g file

# convert a text file format from UNIX to MSDOS (line-ending LF to CRLF)
recode latin1..ibmpc file file2
#unix2dos file file2
#sed -i 's/$/\r/' file

# Show what a code represents in latin-9 charmap
echo -n 0x80 | recode latin-9/x1..dump

# Show latin-9 encoding
echo -n 0x20AC | recode ucs-2/x2..latin-9/x

# Show utf-8 encoding
echo -n 0x20AC | recode ucs-2/x2..utf-8/x
```

## Relative path

```sh
function relative_path_from_to() {
    # strip trailing slashes
    path1=${1%\/}
    path2=${2%\/}
    # common part of both paths
    common=$(printf '%s\x0%s' "${path1}" "${path2}" | sed 's/\(.*\/\).*\x0\1.*/\1/')
    # how many directories we have to go up to the common part
    up=$(grep -o "/" <<< ${path1#$common} | wc -l)
    # create a prefix in the form of ../../ ...
    prefix=""; for ((i=0; i<=$up; i++)); do prefix="$prefix../"; done
    # return prefix plus second path without common
    printf "$prefix${2#$common}"
}

relative_path_from_to /path/test1/file /path/test2/file
# > ../../test2/file
```

```sh
# require the path of both file and dir to exist, resolve symlink
realpath --relative-to=DIR FILE
```

- [command line - How to calculate a relative path from two absolute paths in Linux shell? - Super User](https://superuser.com/questions/140590/how-to-calculate-a-relative-path-from-two-absolute-paths-in-linux-shell/1268217#1268217)
- [shell - Convert absolute path into relative path given a current directory using Bash - Stack Overflow](https://stackoverflow.com/questions/2564634/convert-absolute-path-into-relative-path-given-a-current-directory-using-bash)

## Find corrupted files

Find files with 100 consecutive zero bytes (partially downloaded, etc.)

```sh
find . -type f -exec egrep "\x00{100,}" {} \; -exec echo {} \;
# If not work try with grep -P
```

Note: If you get `grep: invalid repetition count(s)`, use `(\x00\x00\x00\x00){250,}` instead of `\x00{1000,}` (because repetition as limitation)

- [linux - How to grep for special character NUL (^@^@^@) - Super User](https://superuser.com/questions/507267/how-to-grep-for-special-character-nul)

## Text operations

Aka text processing

- [learnbyexample/Command-line-text-processing: From finding text to search and replace, from sorting to beautifying text and more](https://github.com/learnbyexample/Command-line-text-processing)
- [bash - How can I test if a variable is empty or contains only spaces? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/146942/how-can-i-test-if-a-variable-is-empty-or-contains-only-spaces)

```sh
# Echo multiline string (use the newline separator `\n`)
echo -e "a\nb"

# Add line to begin of file, aka prepend text
echo "firstline" | cat - file.txt > file.txt.tmp && mv file.txt.tmp file.txt

# Convert from lower case in upper case
tr '[:lower:]' '[:upper:]'

# Sort contents of two files
sort file1 file2

# Sort contents of two files omitting lines repeated
sort file1 file2 | uniq

# Sort contents of two files by viewing only unique line
sort file1 file2 | uniq -u

# Sort contents of two files by viewing only duplicate line
sort file1 file2 | uniq -d

# Sort IPV4 ip addresses
sort -t. -k1,1n -k2,2n -k3,3n -k4,4n

# Filter non printable characters
tr -dc '[:print:]'

# cut fields separated by blanks
tr -s '[:blank:]' '\t'

# Count lines
wc -l

# Number row of a file
cat -n file1

# Compare contents of two files by deleting only unique lines from `file1`
comm -1 file1 file2

# Compare contents of two files by deleting only unique lines from `file2`
comm -2 file1 file2

# Compare contents of two files by deleting only the lines that appear on both files
comm -3 file1 file2

# Find differences between two files
diff file1 file2

# Look up words "Aug" on file `/var/log/messages`
grep Aug /var/log/messages

# Look up words that begin with "Aug" on file `/var/log/messages`
grep ^Aug /var/log/messages

# Select from file `/var/log/messages` all lines that contain numbers
grep [0-9] /var/log/messages

# Search string "Aug" at directory `/var/log` and below
grep Aug -R /var/log/*

# Merging contents of two files for columns
paste file1 file2

# Merging contents of two files for columns with `+` delimiter on the center
paste -d '+' file1 file2

# Find differences between two files and merge interactively alike `diff`
sdiff file1 file2
```

### Sed

Aka stream editor

- [sed — Wikipedia](https://en.wikipedia.org/wiki/Sed)
- [Is it possible to escape regex metacharacters reliably with sed - Stack Overflow](https://stackoverflow.com/questions/29613304/is-it-possible-to-escape-regex-metacharacters-reliably-with-sed/29613573#29613573)

Note: sed uses stdin and stdout. Newer versions support inplace editing with the -i option

Remove multiline comment:

```sh
# Remove in place all multiline comments
# Note: see also m regex flag
sed -Ei -e '1h;2,$H;$!d;g' -e 's|/\*.*?\*/||g' file.ext

# Single line only (sed match by default on line basis)
sed -i '/<!--.*-->/ d' file

# Note: the , implied the multiple lines.
sed -i '/<!--/,/-->/ d' file
```

See also:

- [regular expression - How can I use sed to replace a multi-line string? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/26284/how-can-i-use-sed-to-replace-a-multi-line-string/235016#235016)
- [sed - Remove multi-line comments - Stack Overflow](https://stackoverflow.com/questions/13061785/remove-multi-line-comments)
- [Multiline techniques (sed, a stream editor)](https://www.gnu.org/software/sed/manual/html_node/Multiline-techniques.html)

Search an replace in files

```sh
#/bin/bash

# Search files that match some pre conditions then apply remplacements
# find . -type f -iname "*.aspx" -exec grep -q -i -E "Page Language=\"VB\"" {} \; -exec grep -q -i -E "<Fnac:HtmlFooter" {} \; -exec ./substitute.sh {} \; -exec unix2dos -q {} \; -print

REGEXP='<Fnac:HtmlFooter\s+ID="HtmlFooter"\s+runat="server"(\s+Omniture="Default")?\s+OmnitureEVar2="([^"]*)"(\s+OmniturePageName="([^"]*)")?(\s+TagCommander="Default")?\s+TagCommanderIdentifier="1"\s+TagCommanderTemplateType="([^"]*)"\s+TagCommanderTemplateName="([^"]*)"\s+/>'

# All chars must be escaped, only newlines are kept for readability
REPLACEMENT=$(cat <<EOF | sed ':a;N;$!ba;s/\n/\\n/g'
<%
' Html.SetTrackingValues(Tracker.Omniture, new {...});
TrackingHelpers.SetTrackingValues(Tracker.TagCommander, New With
{
  Key .template_type = "\6",
  Key .template_name = "\7"
})
TrackingHelpers.SetTrackingValues(Tracker.Omniture, New With
{
  Key .eVar2 = "\2",
  Key .pageName = "\4"
})
%>
<%=WebFormsMvcUtilities.Partial("~/Shared/_Tracking.cshtml", New List(Of Tracker)({ Tracker.TagCommander, Tracker.Omniture }))%>
</body>
</html>
EOF
)

sed -Ei 's|<%@ Register TagPrefix="fnac" TagName="HtmlFooter" Src="~/Nav/Core/Common/HtmlControls/HtmlFooter.ascx" %>||' "$@"
sed -Ei -e '1h;2,$H;$!d;g' -e "s|$REGEXP|$REPLACEMENT|" "$@"
```

```sh
# Replace text in file, need a temp file
# Note: if `old-text` contains slashes `/`, back slash them: `../..` give `..\/..`
sed "s/old-text/new-text/g" file.txt > file.txt.tmp && mv file.txt.tmp file.txt

# Replace string1 with string2
sed 's/string1/string2/g'

# Modify anystring1 to anystring2
sed 's/\(.*\)1/\12/g'

# Remove comments and blank lines
sed '/^ *#/d; /^ *$/d'

# Concatenate lines with trailing \
sed ':a; /\\$/N; s/\\\n//; ta'

# Remove trailing spaces from lines
sed 's/[ \t]*$//'

# Escape shell metacharacters active within double quotes
sed 's/\([`"$\]\)/\\\1/g'

# Right align numbers
seq 10 | sed "s/^/      /; s/ *\(.\{7,\}\)/\1/"

# Duplicate a column
seq 10 | sed p | paste - -

# Print 1000th line
sed -n '1000{p;q}'

# Print lines 10 to 20
sed -n '10,20p;20q'

# Extract title from HTML web page
sed -n 's/.*<title>\(.*\)<\/title>.*/\1/ip;T;q'

# Delete a particular line
sed -i 42d ~/.ssh/known_hosts

# Replace "string1" with "string2"
sed 's/string1/string2/g'

# Remove all blank lines
sed '/^$/d'

# Remove comments and blank lines
sed '/ *#/d; /^$/d'

# Eliminates the first line
sed -e '1d'

# View only lines that contain the word `string1`
sed -n '/string1/p'

# Remove empty characters at the end of each row
sed -e 's/ *$//'

# Remove only the word "string1" from text and leave intact all
sed -e 's/string1//g'

# Print from 1th to 5th row of example.txt
sed -n '1,5p'

# Print row number 5 of example.txt
sed -n '5p;5q'

# Replace more zeros with a single zero
sed -e 's/00*/0/g'
```

### AWK

> AWK reads the input a line at a time. A line is scanned for each pattern in the program, and for each pattern that matches, the associated action is executed.

```sh
# Print all fields
awk '{print NR": "$0; for(i=1;i<=NF;++i) print "\t"i": "$i}'

# Remove all even lines
awk 'NR%2==1'

# View the first column of a line
echo a b c | awk '{print $1}'

# View the first and third column of a line
echo a b c | awk '{print $1,$3}'
```

```sh
#!/usr/bin/env awk -f

{print $0}
```

- [AWK - Wikipedia](https://en.wikipedia.org/wiki/AWK)
- [awk](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/awk.html)
- [The AWK programming language : Aho, Alfred V : Free Download, Borrow, and Streaming : Internet Archive](https://archive.org/details/pdfy-MgN0H1joIoDVoIC7)
- [awk: BEGIN { ... | Jemma Issroff](https://web.archive.org/web/20201030181353/https://jemma.dev/blog/awk-part-1)
- [awk: END { ... | Jemma Issroff](https://web.archive.org/web/20201101093640/https://jemma.dev/blog/awk-part-2)
- [Awk-Batteries/csv.awk at master · Nomarian/Awk-Batteries](https://github.com/Nomarian/Awk-Batteries/blob/master/Units/csv.awk) - parse CSV `gawk -f "$AWK/Units/csv.awk" -e '{print NF}'`
- [awk-scripts/talk.txt at master · rethab/awk-scripts](https://github.com/rethab/awk-scripts/blob/master/talk.txt)
- [onetrueawk/awk: One true awk](https://github.com/onetrueawk/awk)
- [wernsey/d.awk: An Awk script to generate documentation from Markdown comments in C/C++/Java/JavaScript/C# source code.](https://github.com/wernsey/d.awk)

## Disk operations

```sh
# Mounting a Filesystem:
# force umount when the device is busy
fuser -km /mnt/hda2
# mount disk called hda2 - verify existence of the directory `/mnt/hda2`
mount /dev/hda2 /mnt/hda2
# mount a floppy disk
mount /dev/fd0 /mnt/floppy
# mount a cdrom / dvdrom
mount /dev/cdrom /mnt/cdrom
# mount a cdrw / dvdrom
mount /dev/hdc /mnt/cdrecorder
# mount a cdrw / dvdrom
mount /dev/hdb /mnt/cdrecorder
# mount a file or iso image
mount -o loop file.iso /mnt/cdrom
# mount a Windows FAT32 file system
mount -t vfat /dev/hda5 /mnt/hda5
# mount a usb pen-drive or flash-drive
mount /dev/sda1 /mnt/usbdisk
# mount a windows network share
mount -t smbfs -o username=user,password=pass //WinClient/share /mnt/share
# unmount disk called hda2 - exit from mount point `/mnt/hda2` first
umount /dev/hda2
# run umount without writing the file /etc/mtab - useful when the file is read-only or the hard disk is full
umount -n /mnt/hda2

# Show all partitions registered on the system
cat /proc/partitions
# List mounted filesystems on the system (and align output)
mount | column -t

# Show info about disk sda
hdparm -i /dev/sda
# displays the characteristics of a hard-disk
hdparm -i /dev/hda
# perform test reading on a hard-disk
hdparm -tT /dev/sda

# Do a read speed test on disk sda
hdparm -tT /dev/sda
# Test for unreadable blocks on disk sda
badblocks -s /dev/sda
# How long has this disk (system) been powered on in total
smartctl -A /dev/sda | grep Power_On_Hours
```

### Disk space

See also FSlint

```sh
# Show files by size, biggest last
ls -lSr | more
# Show top disk users in current dir. See also dutop
du -s * | sort -k1,1rn | head
# Sort paths by easy to interpret disk usage
du -hs /home/* | sort -k1,1h
# Show size of the files and directories sorted by size
du -sk * | sort -rn
# Estimate space used by directory `dir1`
du -sh dir1
# Show free space on mounted filesystems aks disk usage
df -h
# Show free inodes on mounted filesystems
df -i
# Show disks partitions sizes and types (run as root)
fdisk -l

```

### Clone disk

Aka duplicate disks

For supported partitions (on source drive), use Disk Utility

For not supported partitions

Clone exact disk (boot sector, all partitions & data, etc.) to an other drive (to a file, use a path to a file instead of `/dev/sdX`, see [this page](https://wiki.archlinux.org/index.php/disk_cloning#Create_disk_image) for other options like split the image and `dd` man page for partial copy etc.)

For disk use `/dev/sdX` (or `/dev/hdX`, or BSD `/dev/diskX` or even [`/dev/rdiskX` for better speed](https://superuser.com/questions/631592/why-is-dev-rdisk-about-20-times-faster-than-dev-disk-in-mac-os-x))

```sh
sudo dd if=/dev/sdX of=/dev/sdY bs=64K conv=noerror,sync status=progress
```

Change `bs` to find the optimal value. **64K seem a good value**, but it's related to hardware and software (USB2.0 to USB2.0 RAID). Try to use the same value as the disk cache `8388608` size, or the block size `4096`.

With `bs=64K`:

- USB 2.0 to USB 2.0: 20 to 11 MB/s
- SATA 3.0 (3.0 Gb/s) to SATA 3.0 (3.0 Gb/s): 130 MB/s

Check disk ID (here X and Y) in XXXXX

- [Disk cloning - ArchWiki](https://wiki.archlinux.org/index.php/disk_cloning)
- [Some dd examples - LQWiki](http://wiki.linuxquestions.org/wiki/Some_dd_examples)
- [linux - dd: How to calculate optimal blocksize? - Stack Overflow](https://stackoverflow.com/questions/6161823/dd-how-to-calculate-optimal-blocksize)
- [performance - Is there a way to determine the optimal value for the bs parameter to dd? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/9432/is-there-a-way-to-determine-the-optimal-value-for-the-bs-parameter-to-dd)
- [linux - Does the "bs" option in "dd" really improve the speed? - Server Fault](https://serverfault.com/questions/650086/does-the-bs-option-in-dd-really-improve-the-speed)
- [partitioning - How would I speed up a full disk dd? - Ask Ubuntu](https://askubuntu.com/questions/523037/how-would-i-speed-up-a-full-disk-dd)

### CDs

```sh
# Save copy of data cdrom
gzip < /dev/cdrom > cdrom.iso.gz

# Create cdrom image from contents of dir
mkisofs -V LABEL -r dir | gzip > cdrom.iso.gz

# Mount the cdrom image at /mnt/dir (read only)
mount -o loop cdrom.iso /mnt/dir

# Clear a CDRW
cdrecord -v dev=/dev/cdrom blank=fast

# Burn cdrom image (use dev=ATAPI -scanbus to confirm dev)
gzip -dc cdrom.iso.gz | cdrecord -v dev=/dev/cdrom -

# Rip audio tracks from CD to wav files in current dir
cdparanoia -B

# Make audio CD from all wavs in current dir (see also cdrdao)
cdrecord -v dev=/dev/cdrom -audio -pad *.wav
```

## Command operations

```sh
# Show full path name of command
which command
# Show location of a binary file, source or man
whereis command
# Show full path to a binary / executable
which command

# See how long a command takes
time command

# Start stopwatch. Ctrl-d to stop. See also sw
time cat

# Show commands pertinent to string. See also threadsafe
apropos whatis

# Find the location of a command
command -v git 2> /dev/null
```

- [shell - Why not use "which"? What to use then? - Unix & Linux Stack Exchange](http://unix.stackexchange.com/questions/85249/why-not-use-which-what-to-use-then/85250#85250)
- [shell - `command` vs `type` - Locate program file in user's PATH - Unix & Linux Stack Exchange](http://unix.stackexchange.com/questions/150512/command-vs-type-locate-program-file-in-users-path)
- [bash: which vs command -v - Stack Overflow](https://stackoverflow.com/questions/37056192/bash-which-vs-command-v)

### Command help

Aka man, command documentation

```sh
man mv

# find any related commands
man -k mv

# make a pdf of a manual page
man -t ascii | ps2pdf - > ascii.pdf
```

Section numbers of the `man` manual:

1. executable programs or shell commands
2. system calls (functions provided by the kernel)
3. library calls (functions within program libraries)
4. special files (usually found in /dev)
5. file formats and conventions eg /etc/passwd
6. games
7. miscellaneous (including macro  packages  and  conventions), e.g. `man(7)`, `groff(7)`
8. system administration commands (usually only for root)
9. kernel routines (non standard)

- [What do the parentheses and number after a Unix command or C function mean? Like: man(8), ftok(2), mount(8)?](http://superuser.com/questions/297702/what-do-the-parentheses-and-number-after-a-unix-command-or-c-function-mean)

Some commands support also (or instead) an option that show the help, could be:

- `--help`
- `-h`
- `help`
- `-?`
- `/?`

## Convert PDF 1.4

Force version

```sh
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4  -dColorConversionStrategy=/LeaveColorUnchanged -dDownsampleMonoImages=false -dDownsampleGrayImages=false -dDownsampleColorImages=false -dAutoFilterColorImages=false -dAutoFilterGrayImages=false -dColorImageFilter=/FlateEncode -dGrayImageFilter=/FlateEncode -o airbus_ar_2016_pdf1.4.pdf airbus_ar_2016.pdf
```

## SSH

Aka Secure SHell

```sh
# Run command on $HOST as $USER (default command=shell)
ssh $USER@$HOST command

# Run GUI command on $HOSTNAME as $USER
ssh -f -Y $USER@$HOSTNAME xeyes

# Copy with permissions to $USER's home directory on $HOST
scp -p -r $USER@$HOST: file dir/

# Use faster crypto for local LAN. This might saturate GigE
scp -c arcfour $USER@$LANHOST: bigfile

# Forward connections to $HOSTNAME:8080 out to $HOST:80
ssh -g -L 8080:localhost:80 root@$HOST

# Forward connections from $HOST:1434 in to imap:143
ssh -R 1434:imap:143 root@$HOST

# Install public key for $USER@$HOST for password-less log in
ssh-copy-id $USER@$HOST
```

### SSH Disallow remote root login

In `/etc/ssh/sshd_config` update/add:

	PermitRootLogin no

### SSH Keyfile

	# If `-f filename` is not defined, will generate 2 files (by default `~/.ssh/id_rsa` and `~/.ssh/id_rsa.pub`)
	ssh-keygen -t rsa -b 4096 -f ~/.ssh/user@host_rsa
	ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f ~/.ssh/your_email@example.com_rsa
	ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f ~/.ssh/your_email@example.com-hostname.ext_rsa

In `~/.ssh/config`:

	# username@hostname
	Host hostname
	RSAAuthentication yes
	IdentityFile ~/.ssh/username@hostname_rsa
	User username

- [Generating a new SSH key and adding it to the ssh-agent - User Documentation](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
- SSH Configurations - [Tower Help - Connecting & Authenticating](http://www.git-tower.com/help/mac/remote-repositories/connect-authenticate)

## Write email in local spool

	mail -s "Hello" localusername </dev/null

	/var/spool/mail/$USER
