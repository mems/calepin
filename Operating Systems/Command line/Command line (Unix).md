- [UNIX Tutorial for Beginners](http://wayback.archive.org/web/20150218174409/http://acad.coloradocollege.edu/dept/pc/SciCompLab/UnixTutorial/)
- [BashFAQ - Greg's Wiki](http://mywiki.wooledge.org/BashFAQ)

![bash tips](https://pbs.twimg.com/media/C75R5xUVsAEwlwf.jpg:large)

## Command manual page

Aka man, command documentation

Obtenir le manuel de la commande `mv` :é

	man mv

Obtenir le manuel de la commande `mv` : 

	man man

- http://linux.die.net/man/

Section numbers of the (`man`) manual

	1   Executable programs or shell commands
	2   System calls (functions provided by the kernel)
	3   Library calls (functions within program libraries)
	4   Special files (usually found in /dev)
	5   File formats and conventions eg /etc/passwd
	6   Games
	7   Miscellaneous (including macro  packages  and  conven‐
	    tions), e.g. man(7), groff(7)
	8   System administration commands (usually only for root)
	9   Kernel routines [Non standard]

- [What do the parentheses and number after a Unix command or C function mean? Like: man(8), ftok(2), mount(8)?](http://superuser.com/questions/297702/what-do-the-parentheses-and-number-after-a-unix-command-or-c-function-mean)

Certaines commandes supportent aussi (où à la place) un paramètre dont sont utilisation permet l'affichage de l'aide. Ce paramètre dépend d'une commande à une autre :

- `--help`
- `-h`
- `help`
- `-?`
- `/?`

## Configuration

### Conserver la configuration d'iptables lors des démarrages

	# Sauvegarde de la configuration d'iptables dans un fichier
	iptables-save > /etc/iptables.conf
	
	# Création d'un fichier sh dans le dossier ...
	echo "#!/bin/sh" > /etc/network/if-up.d/iptables
	
	# ... qui restaurera les règles sauvegardé dans le fichier /etc/iptables.conf
	echo "iptables-restore < /etc/iptables.conf" >> /etc/network/if-up.d/iptables
	# Rendre executable le script bash
	chmod +x /etc/network/if-up.d/iptables

Il est nécéssaire de relancer ce script à chaque modifications d'iptables

### Gestion des services

(must be executable: `chmod +x /etc/init.d/blah`)

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

Define when service have to be start or stop: 

	update-rc.d blah defaults

To remove from the startup sequence

	update-rc.d -f blah remove

- https://help.ubuntu.com/community/UbuntuBootupHowto
- http://www.debian-administration.org/articles/28
- `man update-rc.d`
- http://en.wikipedia.org/wiki/Runlevel
- http://www.debuntu.org/how-to-managing-services-with-update-rc-d/
- List all runlevel for the service `apache2`: `ls -l /etc/rc?.d/*apache2`

## User prompt

	#!/bin/bash
	echo "Yes,No?"
	read answer
	echo "You're answer: $answer"

- http://www.tldp.org/LDP/Bash-Beginners-Guide/html/Bash-Beginners-Guide.html#sect_08_02_01

## User administration

Afficher les droits

	ls -l
	# or, but show folders "." and ".."
	ls -all

User informations

	id USERNAME

Voir le dernier log des utilisateurs

	lastlog

Voir les derniers utilisateurs loggés

	last

Montrer qui l'utilisateur courant

	who -a

Historique des commandes (le nom du fichier peux se nomer `.history`)

	~/.bash_history

ou (pour le root)

	/root/.bash_history

Pour éviter qu'un utilisateur masque l'historique des ces commandes (a = append only, i = immutable)

	chattr +a /home/user/.bash_history
	chattr +i /home/user/.profile

- http://www.akyl.net/securing-bashhistory-file-make-sure-your-linux-system-users-won%E2%80%99t-hide-or-delete-their-bashhistory
- http://zero202.free.fr/bash/html/ar01s01.html#id336074

	chattr
	chwon
	chmod

- http://en.wikipedia.org/wiki/Chattr

## Network

Note: ifconfig, route, mii-tool, nslookup commands are obsolete

Show status of ethernet interface eth0

	ethtool eth0


Manually set ethernet interface speed

	ethtool --change eth0 autoneg off speed 100 duplex full


Show status of wireless interface eth1

	iwconfig eth1


Manually set wireless interface speed

	iwconfig eth1 rate 1Mb/s fixed


List wireless networks in range

	iwlist scan


List network interfaces

	ip link show


Rename interface eth0 to wan

	ip link set dev eth0 name wan


Bring interface eth0 up (or down)

	ip link set dev eth0 up


List addresses for interfaces

	ip addr show


Add (or del) ip and mask (255.255.255.0)

	ip addr add 1.2.3.4/24 brd + dev eth0


List routing table

	ip route show


Set default gateway to 1.2.3.254

	ip route add default via 1.2.3.254


Lookup DNS ip address for name or vice versa

	host pixelbeat.org


Lookup local ip address (equivalent to host `hostname`)

	hostname -i


Lookup whois info for hostname or ip address

	whois pixelbeat.org


List internet services on a system

	netstat -tupl


List active connections to/from system

	netstat -tup

DNS record:

	dig example.com

Reverse DNS:

	ping -a 8.8.8.8

	nslookup -type=ptr 8.8.8.8

Nom de la machine:

	hostname

`/etc/hostname` `/etc/hosts`

## Math

Quick math (Calculate φ). See also bc

	echo '(1 + sqrt(5))/2' | bc -l


Calculate π the unix way

	seq -f '4/%g' 1 2 99999 | paste -sd-+ | bc -l


More complex (int) e.g. This shows max FastE packet rate

	echo 'pad=20; min=64; (100*10^6)/((pad+min)*8)' | bc


Python handles scientific notation

	echo 'pad=20; min=64; print (100E6)/((pad+min)*8)' | python


Plot FastE packet rate vs packet size

	echo 'pad=20; plot [64:1518] (100*10**6)/((pad+x)*8)' | gnuplot -persist


Base conversion (decimal to hexadecimal)

	echo 'obase=16; ibase=10; 64206' | bc


Base conversion (hex to dec) ((shell arithmetic expansion))

	echo $((0x2dec))


Unit conversion (metric to imperial)

	units -t '100m/9.58s' 'miles/hour'


Unit conversion (SI to IEC prefixes)

	units -t '500GB' 'GiB'


Definition lookup

	units -t '1 googol'


Add a column of numbers. See also add and funcpy

	seq 100 | (tr '\n' +; echo 0) | bc

## Calendar

Display a calendar

	cal -3


Display a calendar for a particular month year

	cal 9 1752


What date is it this friday. See also day

	date -d fri


exit a script unless it's the last day of the month

	[ $(date -d '12:00 +1 day' +%d) = '01' ] || exit


What day does xmas fall on, this year

	date --date='25 Dec' +%A


Convert seconds since the epoch (1970-01-01 UTC) to date

	date --date='@2147483647'


What time is it on west coast of US (use tzselect to find TZ)

	TZ='America/Los_Angeles' date


What's the local time for 9AM next Friday on west coast US

	date --date='TZ="America/Los_Angeles" 09:00 next Fri'

## Locales

Print number with thousands grouping appropriate to locale

	printf "%'d\n" 1234


Use locale thousands grouping in ls. See also l

	BLOCK_SIZE=\'1 ls -l


Extract info from locale database

	echo "I live in $(locale territory)"


Lookup locale info for specific country. See also ccodes

	LANG=en_IE.utf8 locale int_prefix


List fields available in locale database

	locale -kc $(locale | sed -n 's/\(LC_.\{4,\}\)=.*/\1/p') | less

## Packages

List all packages by installed size (Bytes) on rpm distros

	rpm -q -a --qf '%10{SIZE}\t%{NAME}\n' | sort -k1,1n


List all packages by installed size (KBytes) on deb distros

	dpkg-query -W -f='${Installed-Size;10}\t${Package}\n' | sort -k1,1n

## Monitoring / debugging

	fuser
	lsof
	ls -l  /proc/[process id]/fd
	ls -l  /proc/*/fd
	for p in [0-9]*; do ls -l /proc/$p/fd ;done 

strace
auditctl
inotifywait
inotify
- [monitoring - List the files accessed by a program - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/18844/list-the-files-accessed-by-a-program)
- [How to determine which process is creating a file? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/13776/how-to-determine-which-process-is-creating-a-file)
- [linux - how to list files that are NOT open using find command - Server Fault](http://serverfault.com/questions/359945/how-to-list-files-that-are-not-open-using-find-command)

Monitor messages in a log file

	tail -f /var/log/messages

Summarise/profile system calls made by command

	strace -c ls >/dev/null

List system calls made by command

	strace -f -e open ls >/dev/null

Monitor what's written to stdout and stderr

	strace -f -e trace=write -e write=1,2 ls >/dev/null

List library calls made by command

	ltrace -f -e getenv ls >/dev/null

List opened files and ports

	lsof

- http://en.wikipedia.org/wiki/Lsof

List paths that process id has open

	lsof -p $$

List processes that have specified path open

	lsof ~

Show network traffic except ssh. See also tcpdump_not_me

	tcpdump not port 22

List processes in a hierarchy

	ps -e -o pid,args --forest

List processes by % cpu usage

	ps -e -o pcpu,cpu,nice,state,cputime,args --sort pcpu | sed '/^ 0.0 /d'

List processes by mem (KB) usage. See also ps_mem.py

	ps -e -orss=,args= | sort -b -k1,1n | pr -TW$COLUMNS

List all threads for a particular process

	ps -C firefox-bin -L -o pid,tid,pcpu,state

List elapsed wall time for particular process IDs

	ps -p 1,$$ -o etime=

Show system reboot history

	last reboot

Show amount of (remaining) RAM (-m displays in MB)

	free -m

Watch changeable data continuously

	watch -n.1 'cat /proc/interrupts'

Monitor udev events to help configure rules

	udevadm monitor

### Active processes

	ps -A

Sous forme arborescente

	/bin/ps acxfwwwe

Affichage en live :

	top

### Processes details

	/proc/3117

Où `3117` un dossier ayant comme nom le pid du processus visé. 

### Connection réseau actives avec les processus correspondants

	netstat -ape

- http://en.wikipedia.org/wiki/Netstat

## System information

See also sysinfo. '#' means root access is required

Show kernel version and system architecture

	uname -a


Show name and version of distribution

	head -n1 /etc/issue


Show all partitions registered on the system

	cat /proc/partitions


Show RAM total seen by the system

	grep MemTotal /proc/meminfo


Show CPU(s) info

	grep "model name" /proc/cpuinfo


Show PCI info

	lspci -tv


Show USB info

	lsusb -tv


List mounted filesystems on the system (and align output)

	mount | column -t


Show state of cells in laptop battery

	grep -F capacity: /proc/acpi/battery/BAT0/info


Display SMBIOS/DMI information

	dmidecode -q | less


How long has this disk (system) been powered on in total

	smartctl -A /dev/sda | grep Power_On_Hours


Show info about disk sda

	hdparm -i /dev/sda


Do a read speed test on disk sda

	hdparm -tT /dev/sda


Test for unreadable blocks on disk sda

	badblocks -s /dev/sda

## Interactive

See also linux keyboard shortcuts

Line editor used by bash, python, bc, gnuplot, ...

	readline


Virtual terminals with detach capability, ...

	screen


Powerful file manager that can browse rpm, tar, ftp, ssh, ...

	mc


Interactive/scriptable graphing

	gnuplot


Web browser

	links


open a file or url with the registered desktop application

	xdg-open .

- http://www.linuxguide.it/linux_commands_line_en.htm

## Shell

- [explainshell.com - match command-line arguments to their help text](https://explainshell.com/)
- [dylanaraps/pure-bash-bible: 📖 A collection of pure bash alternatives to external processes.](https://github.com/dylanaraps/pure-bash-bible)

Lister les shells disponibles :

	cat /etc/shells

Le shell par défaut d'un utilisateur est définit dans le fichier `/etc/passwd`

Display current shell prompt setting:

	echo $PS1

And change it:

	export PS1="..."

	export PS1="\[\033[0m\]\[\033[0;30;47m\] \u\[\033[0m\]\[\033[0;30;47m\]@\h\[\033[0m\] \w\n\[\033[1;32m\] \@ \$ \[\033[0m\]"

	export PS1="[${LOGNAME}@$(hostname)]"

In `/etc/bashrc` or `~/.bashrc`

	# If id command returns zero, you’ve root access.
	if [ $(id -u) -eq 0 ];
	then you are root, set red colour prompt
		PS1="\\[$(tput setaf 1)\\]\\u@\\h:\\w\\[$(tput sgr0)\\]"
	else normal
		PS1="[\\u@\\h:\\w] $"
	fi

- [How to: Change / Setup bash custom prompt (PS1)](http://www.cyberciti.biz/tips/howto-linux-unix-bash-shell-setup-prompt.html)

### Working directory

Donner le dossier courant

	pwd

### Clear shell cache

	hash -r

### Shell config

Dans l'ordre :

1. (global system) `/etc/profile`
2. (global system) `/etc/bashrc`
3. (user) `~/.bash_profile`
4. (user) `~/.bash_login`
5. (user) `~/.profile`
6. (user) `~/.bashrc`
7. (user) `~/.bash_logout` au logout

(and `/etc/bash.bashrc`, `/etc/bash.bashrc.local`?)

Pour recharger un fichier de configuration (ici le fichier `~/.bashrc`)

	source ~/.bashrc

ou 

	. ~/.bashrc 

By convention, the prompt ends with `$` for users and by `#` for root

- [Bash prompt basics](http://linuxconfig.org/Bash_prompt_basics)

### Programmable bash completions

- [iridakos - Creating a bash completion script](https://iridakos.com/tutorials/2018/03/01/bash-programmable-completion-tutorial)
- [git/git-completion.bash at master · git/git](https://github.com/git/git/blob/master/contrib/completion/git-completion.bash)
- [Bash Reference Manual: Programmable Completion](https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion.html#Programmable-Completion)
- [Bash Reference Manual: Programmable Completion Builtins](https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins.html#Programmable-Completion-Builtins)
- [Bash Reference Manual: A Programmable Completion Example](https://www.gnu.org/software/bash/manual/html_node/A-Programmable-Completion-Example.html#A-Programmable-Completion-Example)
- [Bash Reference Manual: Bash Variables](https://www.gnu.org/software/bash/manual/html_node/Bash-Variables.html#Bash-Variables)

### Terminal history auto complete

In `~/.inputrc` or `/etc/inputrc`:

	# History auto complete with "start with" filter
	"\e[5~": history-search-backward
	"\e[6~": history-search-forward
	set show-all-if-ambiguous on
	set completion-ignore-case on

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

	env

### Shell colors et terminal control sequences

For `ls` colors:

	export CLICOLOR=1
	export TERM=xterm-color
	export LSCOLORS=DxFxcxdxBxegedbxHxacHd

`key=effect;foreground colour;background colour` separated by `:`.

Ex.: a symlink bright pink `ln=01;95;40` give:

	export LS_COLORS="di=01;33;40:ln=01;95;40"

To known color config:

	man ls

- http://geoff.greer.fm/lscolors/
- http://www.bigsoft.co.uk/blog/index.php/2008/04/11/configuring-ls_colors
 
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

### Command alias

	alias NICKNAME='COMMAND -withargs'

A ajouter dans `~/.bashrc`

- http://www.displayobject.fr/2010/03/07/create-cmd-aliases-in-windows

### Shell script file

Créer un fichier `.sh` et executer la commande suivante sur celui ci

	chmod +x /path/to/file.sh

Celui-ci devra contenir un shebang sur la première ligne indiquant quel interpréteur var être utilisé pour executer le contenu du fichier.

	#!/bin/sh

Les plus courant sont `sh`, `php`, `python` ou encore `perl`.

- http://en.wikipedia.org/wiki/Shebang_%28Unix%29

Il est possible d'être générique, et de ne pas indiquer directement le chemin de l'interpréteur :

	#!/usr/bin/env php

- http://en.wikipedia.org/wiki/Shebang_%28Unix%29#Portability

Include shell script into an other

	source /path/to/script.sh

But it's relative to execution path, not current script path.

So use this instead:

	source $(dirname $0)/script.sh

Or:

	CURRENT_DIR=`dirname $0`
	$CURRENT_DIR/script.sh

Node shebang:

	#!/usr/bin/env node

Or use if support system with nodejs instead of node. (`:` command in bash is noop)

	#!/usr/bin/env sh
	':' //; exec "$(command -v nodejs || command -v node)" "$0" "$@"
	
	console.log('Hello world!');

- [scripting - Universal Node.js shebang? - Unix & Linux Stack Exchange](http://unix.stackexchange.com/questions/65235/universal-node-js-shebang)

### Shell script syntax

Use `$( )`, and don't use \`\` anymore: [Bash FAQ 82](http://mywiki.wooledge.org/BashFAQ/082).

Avoid using UPPERCASE variable names. That namespace is generally reserved by the shell for special purposes (like `PATH`), so using it for your own variables is a bad idea.

Escape special char in argument:

	command $'\t'

Wildcard files:

	for file in *.ext1; do echo "${file} ${file/.ext1/.ext2}"; done

	ls file_*{.png,.jpg}

File [Wildcards](http://www.tldp.org/LDP/GNU-Linux-Tools-Summary/html/x11655.htm#STANDARD-WILDCARDS)

Brace expansion

	sudo mv /path/file{,.old}
	sudo ln {/path1,/path2}/file

- [Bash Reference Manual: Brace Expansion](https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion.html)

Here-doc & here-string:

	cat > /path/to/file << EOF
	Some thing.
	Blahblah!
	EOF

	cat > /path/to/file <<< "Some thing."

	read -r -d '' VAR <<'EOF'
	abc'asdf"
	$(dont-execute-this)
	foo"bar"''
	EOF

- [How to assign a heredoc value to a variable in Bash? - Stack Overflow](https://stackoverflow.com/questions/1167746/how-to-assign-a-heredoc-value-to-a-variable-in-bash)

### Redirection

File pointer and file redirection

- [BashGuide/InputAndOutput - Greg's Wiki](http://mywiki.wooledge.org/BashGuide/InputAndOutput#Redirection)
- [I/O Redirection](http://tldp.org/LDP/abs/html/io-redirection.html)
- [Bash scripting quirks & safety tips - Julia Evans](http://jvns.ca/blog/2017/03/26/bash-quirks/)
- named pipe (`mkfifo`)
 
	while read item; do
		echo $item
	done < sql.res

Create a fake tmp file:

	cat <(echo "tmp file content")

Same as: `echo hello > file; cat file`

```sh
cat <<< hello

diff <(cd dir1; ls) <(cd dir2; ls)

$(cat file) is same as $(< file)
	
(
	echo open ip_address
	echo user username password
	echo put -O $today $file_gnome_curr
	echo bye
) | lftp -f /dev/stdin >> lftp.log 2>&1
```

```sh
cat <<EOF
test1
test2
EOF
```

```sh
(cat <<'EOF'
file1
file2
EOF
) | while read -r file; do
	cp "from/$file" "to/$file";
done;
```

```sh
cat <<EOT >> greetings.txt
line 1
line 2
EOT
```

File descriptors (fd) :

- 0 is `stdin` IN
- 1 is `stdout` OUT
- 2 is `stderr` ERROR

`2>&1` redirects fd 2 to 1 (`stderr` to `stdout`)

Empty a file (ex: clean a log file):

```sh
> /var/log/apache2/error.log
```

Append to a file:

```sh
echo "Appended text" >> /path/file
```

Log all infos (and erros) of following commands to a file `/tmp/log.txt`: 

```sh
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

	echo '' > .mycmd.pid
	mycmd & echo "$!" >> .mycmd.pid
	# ... later
	cat .mycmd.pid | xargs -n 1 kill -9

### Add a bin folder to global executables

Pour éviter de tapper le chemin entier vers les commandes / executables

	PATH=$PATH:/path/bindir
	export PATH

	PATH=$PATH:/path/bindir command-use-path
	PATH=$PATH:/path/bindir bash -c 'echo $PATH'
	PATH=$PATH:/path/bindir bash -c 'command1 | command2'
	(export PATH=$PATH:/path/bindir; command1 | command2)

Pour l'ajouter de façon permanente, l'écrire dans `~/.profile` ou `~/.bashrc`

- [Path (variable) - Wikipedia](http://en.wikipedia.org/wiki/Path_%28variable%29)

### Dotfiles

- [mathiasbynens/dotfiles: .files, including ~/.macos — sensible hacker defaults for macOS](https://github.com/mathiasbynens/dotfiles)

## Directory navigation

Go to previous directory

	cd -


Go to $HOME directory

	cd


Go to dir, execute command and return to current dir

	(cd dir && command)


Put current dir on stack so you can popd back to it

	pushd .

## Files and folders operations

File name:

> Using `sed` or other external processes to do simple string operations like stripping extensions and prefixes is inefficient. Instead, use parameter expansions which are part of the shell (no external process means it will be faster). Some helpful articles on the subject are listed below:
> 
> [Bash FAQ 73](http://mywiki.wooledge.org/BashFAQ/073): Parameter expansions
> [Bash FAQ 100](http://mywiki.wooledge.org/BashFAQ/100): String manipulations

### File searching

- [bash - How do I make find fail if -exec fails? - Ask Different](https://apple.stackexchange.com/questions/49042/how-do-i-make-find-fail-if-exec-fails)

Find all files that have been modified in the past 7 days

	find . -mtime -7

Find all JPEGs that have been modified more than 30 days ago

	find . -name \*.jpg -mtime +30

Move all JPEGs from the current folder (recursively) that are greater than 40k into the folder /tmp/2

	find ./ -name \*.jpg -size +40k -exec mv {} /tmp/2 +

quick dir listing

	alias l='ls -l --color=auto'

List files by date. See also newest and find_mm_yyyy

	ls -lrt

Print in 9 columns to width of terminal

	ls /usr/bin | pr -T9 -W$COLUMNS


Search 'expr' in this dir and below. See also findrepo

	find -name '*.[ch]' | xargs grep -E 'expr'


Search all regular files for 'example' in this dir and below

	find -type f -print0 | xargs -r0 grep -F 'example'


Search all regular files for 'example' in this dir

	find -maxdepth 1 -type f | xargs grep -F 'example'

Process each item with multiple commands (in while loop)

	find -maxdepth 1 -type d | while read dir; do echo $dir; echo cmd2; done

	find ./ -name "tile_*.png" -exec bash -c 'filename="$1";echo "${filename%.*}"' _ {} \;

- [bash - Find and replace filename recursively in a directory - Stack Overflow](https://stackoverflow.com/questions/9393607/find-and-replace-filename-recursively-in-a-directory/9394625#9394625)
 
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
	ls *.jpg | xargs -r -I FILE   convert FILE -thumbnail 200x90 FILE_thumb.gif


Find files not readable by all (useful for web site)

	find -type f ! -perm -444


Find dirs not accessible by all (useful for web site)

	find -type d ! -perm -111


Search cached index for names. This re is like glob *file*.txt

	locate -r 'file[^/]*\.txt'


Quickly search (sorted) dictionary for prefix

	look reference


Highlight occurances of regular expression in dictionary

	grep --color reference /usr/share/dict/words

Search for empty files and folder (or file with only whitespaces)

- [command line - How to find all empty files and folders in a specific directory including files which just look empty but are not? - Ask Ubuntu](https://askubuntu.com/questions/719912/how-to-find-all-empty-files-and-folders-in-a-specific-directory-including-files)
- [unix - Appending new lines to multiple files - Super User](https://superuser.com/questions/1327969/appending-new-lines-to-multiple-files/1327980#1327980) - How to use `echo "test" >> {}` within find exec

### Create archive from file list

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

### Copy files from m3u playlist

	# Extract music from m3u (ignore lines start with #, whitespace or are empty)
	# Playlists entries could be relative
	cd "/path/to/playlists"
	cat "playlist1.m3u" "playlist1.m3u" "playlist3.m3u" | grep "^[^# \t]" | tr -s '\n' | while read -r line; do cp --parent -v "$line" /destination; done

### Get extensions of all files

	find . -type f | while read file; do filename=$(basename "$file"); ext=$([[ "$filename" = *.* ]] && echo ".${filename##*.}" || echo ''); echo $ext; done | sort | uniq

### File checksum

	# SHA256, used in chef cookbooks
	openssl dgst -sha256 path/to/myfile

	# MD5
	openssl dgst -md5 path/to/myfile

### Split files

FAT32 maximum file size is ["4 GiB minus 1 byte"](https://en.wikipedia.org/wiki/File_Allocation_Table#FAT32) (4294967295 bytes)

To write file with a size larger than that limit, you need to split it.

In destination folder, execute following command:

	split -b 4294967295 example.dmg example.dmg.part.

(the part `example.dmg.part.` will be used to name output files like `example.dmg.part.aa`, `example.dmg.part.ab` and so on)

	cat  example.dmg.part.* > example.dmg

### Mass rename

https://stackoverflow.com/questions/417916/how-to-do-a-mass-rename

	for i in 'Ref_00'*.jpg; do mv $i $(echo $i | sed 's/Ref_00/anim/'); done;

Or (a better solution):

	find . -name 'Ref_00*.jpg' -prune -print | while read i; do mv $i $(echo $i | sed 's/Ref_00/anim/'); done;

Will rename `Ref_00001.jpg` to `anim001.jpg`

	find . -maxdepth 1 -type f -exec mv "{}" "{}.tmp" \; -print | awk 'match($0,"^(.*atlas-)([0-9]+)(.*)$",a){print "\""a[1]a[2]a[3]".tmp\" \""a[1]a[2]-1a[3]"\""}' | while read args; do eval "mv $args"; done

Will rename `sprite1.png` to `sprite0.png` (if change the offset, be careful of sort order)

### Use `rename`

	# Rename *.JPG to *.jpg
	rename 's/\.JPG/\.jpg/' *.JPG
	# Strip spaces
	rename 's/ //' *.jpg
	# Lower case
	rename 'y/A-Z/a-z/' *

On OSX install it with port `port install p5-file-rename` (but should use the cmd `rename-5.22` where `22` is installed version via port instead of `rename`) or brew `brew install rename`

### Remove files

	rm -f file1 file2

	find . -name 'tile_*.png' -delete

Remove all files with exceptions:

	find . -type f -not \( -name '*.php' -or -name '*.iso' \) -exec rm {} \;

With a list of exceptions:

	find . -type f -printf "%P\n" ! -name "list.txt" | fgrep -vf list.txt | xargs -r rm

- http://www.cyberciti.biz/faq/linux-bash-delete-all-files-in-directory-except-few/
- [unix - BASH: How to remove all files except those named in a manifest? - Stack Overflow](https://stackoverflow.com/questions/2782602/bash-how-to-remove-all-files-except-those-named-in-a-manifest)
- [linux - find files not in a list - Stack Overflow](https://stackoverflow.com/questions/7306971/find-files-not-in-a-list)

### Find missing files

- [How do I find which files are missing from a list? - Unix & Linux Stack Exchange](http://unix.stackexchange.com/questions/11989/how-do-i-find-which-files-are-missing-from-a-list)

### Find duplicates files

	find -not -empty -type f -printf "%s\n" | sort -rn | uniq -d | xargs -I{} -n1 find -type f -size {}c -print0 | xargs -0 md5sum | sort | uniq -w32 --all-repeated=separate | awk '{$1=""; print substr($0,2)}'

- [How do I do a binary diff on two identically sized files under Linux? - Super User](https://superuser.com/questions/135911/how-do-i-do-a-binary-diff-on-two-identically-sized-files-under-linux)
- [shell - Finding duplicate files according to md5 with bash - Stack Overflow](https://stackoverflow.com/questions/19551908/finding-duplicate-files-according-to-md5-with-bash)

Remove duplicates

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

- [bash - How to remove duplicated files in a directory? - Super User](http://superuser.com/questions/386199/how-to-remove-duplicated-files-in-a-directory/386209#386209)

[Rdfind – redundant data find](https://rdfind.pauldreik.se/):

	rdfind -makehardlinks true

	fdupes

	find -not -empty -type f -printf "%s\n" | sort -rn | uniq -d | xargs -I{} -n1 find -type f -size {}c -print0 | xargs -0 md5sum | sort | uniq -w32 --all-repeated=separate
	
BTRFS [Deduplication - btrf Wiki](https://btrfs.wiki.kernel.org/index.php/Deduplication)

See also `diff -q --binary` or `cmp -s $1 $2 && echo "identical" || echo "different"`

- [Comparing and Merging Files](http://www.gnu.org/software/diffutils/manual/diffutils.html#Binary)
- [centos - What's the quickest way to find duplicated files? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/277697/whats-the-quickest-way-to-find-duplicated-files/277767#277767)

		find -not -empty -type f -printf "%s\n" | sort -rn | uniq -d | xargs -I{} -n1 find -type f -size {}c -print0 | xargs -0 md5sum | sort | uniq -w32 --all-repeated=separate
	
	Replace the use of md5sum with `diff` or `cmp`: [How do I do a binary diff on two identically sized files under Linux? - Super User](https://superuser.com/questions/135911/how-do-i-do-a-binary-diff-on-two-identically-sized-files-under-linux)
- [dupe-krill/README.md at master · kornelski/dupe-krill](https://github.com/kornelski/dupe-krill/blob/master/README.md)

Then replace files by hardlink:

	ln -f TARGET LINK_NAME

- [Is there an easy way to replace duplicate files with hardlinks? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/3037/is-there-an-easy-way-to-replace-duplicate-files-with-hardlinks)
- [hardlink - Finding files that are *not* hard links via a shell script - Stack Overflow](https://stackoverflow.com/questions/16282618/finding-files-that-are-not-hard-links-via-a-shell-script)

### Rename all files to a specific extension

	for j in /path/dir/*.html
	do
		n=${j/.html}
		mv "$j" "$n.php"
	done

	for j in *; do mv "$j" "$n.bin"; done;

### Hard link

Aka hardware link

Créer un pointeur sur les données d'un disque dur. Il est impossible de le faire sur un dossier (à cause du risque boucles dans une arborescence) 

Créer un pointeur : 

	ln /path/to/source_file /path/to/target_file

	ln -T /etc/apache2/sites-available/example.com /etc/apache2/sites-enabled/example.com

Détruire un pointeur :

	unlink /etc/apache2/sites-enabled/websiteA.exemple

### Choose incremental filename

Test if `dirB/file.ext` exist else choose dest file name as `dirB/file-1.ext`, if already exist choose `dirB/file-2.ext` and so one

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

### File type

Get information about files in the current folder

	find . -maxdepth 1 -type f -exec file "{}" \;

(Si reconnu par libmagic)

	file --mime /path/file

Le détails des formats est décrit dans l'un des dossiers suivants :

- les fichiers dans le dossier `/etc/magic`
- `/etc/magic.mime`
- `/usr/share/misc/magic.mgc`
- `/usr/share/file/magic.mgc`
- `/opt/local/share/misc/magic.mgc`
- les fichiers magic dans le dossier `/opt/local/share/misc/magic`
- `~/.magic.mgc`
- `~/.magic`

Extension du fichier magic compilé : `*.mgc`

- https://github.com/SaltwaterC/mime-magic

### Test if a file exist

	#!/bin/bash
	filename=$1
	if [ -f $filename ]
	then
		echo "$filename exists"
	else
		echo "$filename does NOT exist"
	fi

### Name, extension and parent folder

**Note: Don't use parameter substitution, it's not work with all cases**

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

	extension=$([[ "$file" = *.* ]] && echo "${file##*.}" || echo '')

- [Parameter Substitution](http://www.tldp.org/LDP/abs/html/parameter-substitution.html)
- [Bash Reference Manual: Shell Parameter Expansion](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html)
- [bash - Get file directory path from filepath - Stack Overflow](https://stackoverflow.com/questions/6121091/get-file-directory-path-from-filepath)
- [string - Extract filename and extension in Bash - Stack Overflow](https://stackoverflow.com/questions/965053/extract-filename-and-extension-in-bash)

### Supprimer tous les fichiers Unix cachés

Tous les fichiers/dossier commençant par ".", comme `.htaccess` ou `.DS_STORE`

	rm -rf .[^.]*

Tous les fichiers `.svn`

	find ./ -name ".svn" -exec rm -rf {} +

### Affichage de fichier / flux

Affichage 

	cat /path/file

Pageurs (affichage page par page) :

	less /path/file

ou

	more /path/file

Affichage en live des modifications:

	tail -f /path/file

### List all folders and files

Ordered by size :

	du -ak . | sort -nr | less

List top 10 largest files and directories

	du -a /var | sort -n -r | head -n 10

### Find text in files

Find text in files:

	grep -rn "texttofind" *

	grep "string text to find in all files" . -R

### Create an empty file or truncate a file

	> /var/log/apache2/error.log

	touch file.ext

Create a large test file (taking no space):

	dd bs=1 seek=2TB if=/dev/null of=file.ext

### Copy over SSH

	scp /path/localfile user@host:/path/remotefile

	scp /path/localfile user@host:/path/remotedir/

	scp /path/localdir user@host:/path/remotedir

### Copy with rsync

Network efficient file copier: Use the --dry-run option for testing

	rsync -r -t -v /path/srcdir /path/destdir

Only get diffs. Do multiple times for troublesome downloads

	rsync -P rsync://rsync.server.com/path/to/file file


Locally copy with rate limit. It's like nice for I/O

	rsync --bwlimit=1000 fromfile tofile


Mirror web site (using compression and encryption)

	rsync -az -e ssh --delete ~/public_html/ remote.com:'~/public_html'


Synchronize current directory with remote one

	rsync -auz -e ssh remote:/dir/ . && rsync -auz -e ssh . remote:/dir/


	date=$(date +%Y%m%d-%H%M)
	
	[for loop over users]
	
	older=( $backups/$user/*(N/om) )
	
	rsync --archive --recursive \
		--fuzzy --partial --partial-dir=$backups/$user/.rsync-partial \
		--log-file=$tempfile --link-dest=${^older[1,20]} \
		--files-from=$configdir/I-$user \
		--exclude-from=$configdir/X-$user \
		$user@$from:/ $backups/$user/$date/

Copy folder to folder (if mounted)

	rsync -ah --progress --exclude='$RECYCLE.BIN' --exclude='$Recycle.Bin' --exclude='.AppleDB' --exclude='.AppleDesktop' --exclude='.AppleDouble' --exclude='.com.apple.timemachine.supported' --exclude='.dbfseventsd' --exclude='.DocumentRevisions-V100*' --exclude='.DS_Store' --exclude='.fseventsd' --exclude='.PKInstallSandboxManager' --exclude='.Spotlight*' --exclude='.SymAV*' --exclude='.symSchedScanLockxz' --exclude='.TemporaryItems' --exclude='.Trash*' --exclude='.vol' --exclude='.VolumeIcon.icns' --exclude='Desktop DB' --exclude='Desktop DF' --exclude='hiberfil.sys' --exclude='lost+found' --exclude='Network Trash Folder' --exclude='pagefile.sys' --exclude='Recycled' --exclude='RECYCLER' --exclude='System Volume Information' --exclude='Temporary Items' --exclude='Thumbs.db' /src/dir/ /dst/dir/

Use list `--exclude-from=LIST`:

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

Resources for exclude metadata and system files:

- https://github.com/github/gitignore
- https://github.com/joeblau/gitignore.io/tree/master/data
- https://gist.github.com/keithmorris/c652b2a4d88788e5416d
- https://github.com/dotphiles/dotphiles/blob/master/git/gitignore

- [Rsync --exclude List for Mac OS X - Alan W. Smith](http://alanwsmith.com/rsync-exclude-list-for-mac-osx)
- [rsync on OS X says its complete but it's really not? : unix](https://www.reddit.com/r/unix/comments/4ozc9e/rsync_on_os_x_says_its_complete_but_its_really_not/)

### File comparaisons

Note: you can export LANG=C for speed. Also these assume no duplicate lines within a file

Union of unsorted files

	sort file1 file2 | uniq


Intersection of unsorted files

	sort file1 file2 | uniq -d


Difference of unsorted files

	sort file1 file1 file2 | uniq -u


Symmetric Difference of unsorted files

	sort file1 file2 | uniq -u


Union of sorted files

	join -t'\0' -a1 -a2 file1 file2


Intersection of sorted files

	join -t'\0' file1 file2


Difference of sorted files

	join -t'\0' -v2 file1 file2


Symmetric Difference of sorted files

	join -t'\0' -v1 -v2 file1 file2

### Use diff and patch

Compare 2 folders:

Sans `-q` mais avec `-u` pour faire un patch

	diff -rq /path/dirA /path/dirB

Et sans prendre en compte les fichiers metadonnées d'OSX et de Windows, le tout ordonné :

	diff -uqr /path/dirA /path/dirB | grep -v -e 'DS_Store' -e 'Thumbs' | sort

Comparer 2 files:

	diff -u /path/fileA /path/fileB

- [The Ten Minute Guide to diff and patch](http://jungels.net/articles/diff-patch-ten-minutes.html)

Apply a patch:

	patch -i my.patch

Use heredoc

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

Use `-p1` to strip path `a/` and `b/`

### Folder bind

Aka folder link, like symlink but for folder (standart implementation don't allow to link folder)

Monter une arborescence (d'un dossier) à l'endroit voulut (ici `/path/destdir`)

	mount --bind /path/srcdir /path/destdir

Démonter l'arborescence (ici l'equivalent de `/path/destdir` donné ci-dessus)

	umount /path/dir

Le point de montage apparaitra dans le fichier `/etc/fstab` en tant `fs-type` : `bind`

### Archives and compression

Encrypt file

	gpg -c file

Decrypt file

	gpg file.gpg

Make compressed archive of dir/

	tar -c dir/ | bzip2 > dir.tar.bz2

Extract archive (use gzip instead of bzip2 for tar.gz files)

	bzip2 -dc dir.tar.bz2 | tar -x

Make encrypted archive of dir/ on remote machine

	tar -c dir/ | gzip | gpg -c | ssh user@remote 'dd of=dir.tar.gz.gpg'

Make archive of subset of dir/ and below

	find dir/ -name '*.txt' | tar -c --files-from=- | bzip2 > dir_txt.tar.bz2

Make copy of subset of dir/ and below

	find dir/ -name '*.txt' | xargs cp -a --target-directory=dir_txt/ --parents

Copy (with permissions) copy/ dir to /where/to/ dir

	( tar -c /dir/to/copy ) | ( cd /where/to/ && tar -x -p )

Copy (with permissions) contents of copy/ dir to /where/to/

	( cd /dir/to/copy && tar -c . ) | ( cd /where/to/ && tar -x -p )

Copy (with permissions) copy/ dir to remote:/where/to/ dir

	( tar -c /dir/to/copy ) | ssh -C user@remote 'cd /where/to/ && tar -x -p' 

Backup harddrive (raw) to remote machine

	dd bs=1M if=/dev/sda | gzip | ssh user@remote 'dd of=sda.gz'

## Find corrupted files

Find files with 100 consecutive zero bytes (partially downloaded, etc.)

	find . -type f -exec egrep "\x00{100,}" {} \; -exec echo {} \;
	# If not work try with grep -P

Note: If you get `grep: invalid repetition count(s)`, use `(\x00\x00\x00\x00){250,}` instead of `\x00{1000,}` (because repetition as limitation)

- [linux - How to grep for special character NUL (^@^@^@) - Super User](https://superuser.com/questions/507267/how-to-grep-for-special-character-nul)

## Text operations

- [bash - How can I test if a variable is empty or contains only spaces? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/146942/how-can-i-test-if-a-variable-is-empty-or-contains-only-spaces)

Sortir une chaine multiligne

	echo -e "a\nb"

Add line to begin of file, aka prepend text

	echo "firstline" | cat - file.txt > file.txt.tmp && mv file.txt.tmp file.txt

Replace text in file

	sed "s/old-text/new-text/g" file.txt > file.txt.tmp && mv file.txt.tmp file.txt

Note: if `old-text` contains slashes `/`, back slash them: `../..` give `..\/..`

### Sed

Aka stream editor

- [sed — Wikipedia](https://en.wikipedia.org/wiki/Sed)
- [Is it possible to escape regex metacharacters reliably with sed - Stack Overflow](https://stackoverflow.com/questions/29613304/is-it-possible-to-escape-regex-metacharacters-reliably-with-sed/29613573#29613573)

Note: sed uses stdin and stdout. Newer versions support inplace editing with the -i option

Replace string1 with string2

	sed 's/string1/string2/g'


Modify anystring1 to anystring2

	sed 's/\(.*\)1/\12/g'


Remove comments and blank lines

	sed '/^ *#/d; /^ *$/d'


Concatenate lines with trailing \

	sed ':a; /\\$/N; s/\\\n//; ta'


Remove trailing spaces from lines

	sed 's/[ \t]*$//'


Escape shell metacharacters active within double quotes

	sed 's/\([`"$\]\)/\\\1/g'


Right align numbers

	seq 10 | sed "s/^/      /; s/ *\(.\{7,\}\)/\1/"


Duplicate a column

	seq 10 | sed p | paste - -


Print 1000th line

	sed -n '1000{p;q}'


Print lines 10 to 20

	sed -n '10,20p;20q'


Extract title from HTML web page

	sed -n 's/.*<title>\(.*\)<\/title>.*/\1/ip;T;q'


Delete a particular line

	sed -i 42d ~/.ssh/known_hosts


Sort IPV4 ip addresses

	sort -t. -k1,1n -k2,2n -k3,3n -k4,4n


Case conversion

	echo 'Test' | tr '[:lower:]' '[:upper:]'


Filter non printable characters

	tr -dc '[:print:]' < /dev/urandom


cut fields separated by blanks

	tr -s '[:blank:]' '\t' </proc/diskstats | cut -f4


Count lines

	history | wc -l

### Recode

Obsoletes iconv, dos2unix, unix2dos

Show available conversions (aliases on each line)

	recode -l | less

Windows "ansi" to local charset (auto does CRLF conversion)

	recode windows-1252.. file_to_change.txt

Windows utf8 to local charset

	recode utf-8/CRLF.. file_to_change.txt

Latin9 (western europe) to utf8

	recode iso-8859-15..utf8 file_to_change.txt

Base64 encode / decode (See also [Base64](Base64))

	recode ../b64 < file.png

Quoted printable decode

	recode /qp.. < file.qp > file.txt

Text to HTML

	recode ..HTML < file.txt > file.html

Lookup table of characters

	recode -lf windows-1252 | grep euro


Show what a code represents in latin-9 charmap

	echo -n 0x80 | recode latin-9/x1..dump


Show latin-9 encoding

	echo -n 0x20AC | recode ucs-2/x2..latin-9/x


Show utf-8 encoding

	echo -n 0x20AC | recode ucs-2/x2..utf-8/x

## Disk operations

### Disk space

See also FSlint

Show files by size, biggest last

	ls -lSr


Show top disk users in current dir. See also dutop

	du -s * | sort -k1,1rn | head


Sort paths by easy to interpret disk usage

	du -hs /home/* | sort -k1,1h


Show free space on mounted filesystems aks disk usage

	df -h


Show free inodes on mounted filesystems

	df -i


Show disks partitions sizes and types (run as root)

	fdisk -l

### Clone disk

Aka duplicate disks

For supported partitions (on source drive), use Disk Utility

For not supported partitions

Clone exact disk (boot sector, all partitions, all data, etc.) to an other drive (to a file, use a path to a file instead of `/dev/sdX`, see [this page](https://wiki.archlinux.org/index.php/disk_cloning#Create_disk_image) for other options like split the image and `dd` man page for partial copy etc.)

	sudo dd if=/dev/sdX of=/dev/sdY bs=64K conv=noerror,sync status=progress

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

Save copy of data cdrom

	gzip < /dev/cdrom > cdrom.iso.gz


Create cdrom image from contents of dir

	mkisofs -V LABEL -r dir | gzip > cdrom.iso.gz


Mount the cdrom image at /mnt/dir (read only)

	mount -o loop cdrom.iso /mnt/dir


Clear a CDRW

	cdrecord -v dev=/dev/cdrom blank=fast


Burn cdrom image (use dev=ATAPI -scanbus to confirm dev)

	gzip -dc cdrom.iso.gz | cdrecord -v dev=/dev/cdrom -


Rip audio tracks from CD to wav files in current dir

	cdparanoia -B


Make audio CD from all wavs in current dir (see also cdrdao)

	cdrecord -v dev=/dev/cdrom -audio -pad *.wav

## Command operations

Show commands pertinent to string. See also threadsafe

	apropos whatis

make a pdf of a manual page

	man -t ascii | ps2pdf - > ascii.pdf

Show full path name of command

	which command

See how long a command takes

	time command

Start stopwatch. Ctrl-d to stop. See also sw

	time cat

Find the location of a command

	command -v git 2> /dev/null

- [shell - Why not use "which"? What to use then? - Unix & Linux Stack Exchange](http://unix.stackexchange.com/questions/85249/why-not-use-which-what-to-use-then/85250#85250)
- [shell - `command` vs `type` - Locate program file in user's PATH - Unix & Linux Stack Exchange](http://unix.stackexchange.com/questions/150512/command-vs-type-locate-program-file-in-users-path)
- [bash: which vs command -v - Stack Overflow](https://stackoverflow.com/questions/37056192/bash-which-vs-command-v)

## Backup external server

**Note: Be carefull with [crendentials used in job schedulers](Security#crendentials-used-in-job-schedulers).** It's why we try to use configuration files instead pure command line

Use [`rsync`](#rsync) if possible, or `lftp`, `curl`, `wget`, `scp`, `sftp`. See also `unison`, `bacula`, `amanda`

### FTP

#### `wget`

Use a `.wgetrc` file to store configuration

`/dst/dir.wget`:

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

	cd /dst/dir
	WGETRC=/dst/dir.wget wget ftp://www.mydomain.tld/
	# Clean up obselete files
	find . -type f -name ".listing" -exec bash -c 'cd $(dirname "{}"); find . -maxdepth 0 ! -name ".listing" -printf "%P\n" | fgrep -vf ".listing" | while read file; do rm $(basename "$file"); done;' \;
	# find . -type f -name ".listing" -exec bash -c 'cd $(dirname "{}"); find . -maxdepth 0 ! -name ".listing" -printf "%P\n" | fgrep -vf ".listing" | xargs -r rm' \;

Note: if you set password in URL don't forget to encode special chars: `mypass#gh647` to `mypass%23gh647`

- https://www.gnu.org/software/wget/manual/wget.html#Wgetrc-Commands

### `lftp`

`/dst/dir.lftp`

	set ftp:list-options -a
	#set cmd:fail-exit true
	# To use keyfile
	# http://www.adminschoice.com/how-to-configure-ssh-without-password
	# ssh-keygen -t rsa -f keyfile -N ""
	#set sftp:connect-program "ssh -a -x -i <keyfile>"
	open -u user,pass sftp://sftp.dc0.gpaas.net
	mirror --verbose --delete --parallel=4 --only-newer --exclude ^snapshots/ --exclude ^vhosts/ --exclude ^lamp0/\.config --exclude ^lamp0/var/admin/gandi.cnf$ --exclude ^lamp0/var/admin/logrotate.conf$ --exclude ^lamp0/var/cron/admin/logrotate$ --exclude ^lamp0/var/cron/admin/phpsess$ --exclude ^lamp0/db/ --exclude ^lamp0/var/log/.+ --exclude ^lamp0/var/php/www/.+ "${SRC_DIR}" "${DST_DIR}"
	exit

	# For paths in variables used in sed, see https://stackoverflow.com/a/29613573/470117
	SRC_DIR=/src/dir; DST_DIR=/dst/dir; sed -e "s#\${SRC_DIR}#$SRC_DIR#" -e "s#\${DST_DIR}#$DST_DIR#" /dst/dir.lftp | lftp -f /dev/stdin

	lftp -u username,password ftphost << EOF
	mirror -Re --use-cache /home/ /backup/
	mirror -Re --use-cache /etc/ /backup/
	mirror -Re --use-cache /var/www/ /backup/
	quit 0
	EOF

`--exclude` / `-x` use extended regular expression (see `egrep`) `\.nfo`. Folders path don't start with slash, but have a trailing slash: `etc/bin/`

Add `--reverse` to restore backup

For `lftp –> Fatal error: Certificate verification: Not trusted`:

1. Create the .lftp directory with the command : `mkdir /root/.lftp`
2. Create and edit the rc file with the command : `vi /root/.lftp/rc`
3. Press `i` for edit mode
4. Add the line: `set ssl:verify-certificate no`
5. Exit edit mode by pressing Escape (twice)
6. Close and save the file by pressing Z (capital z) twice)

- https://linux.die.net/man/1/lftp
- http://mewbies.com/lftp_basic_usage_tutorial.htm
- [linux - Transfer files using lftp in bash script - Stack Overflow](https://stackoverflow.com/questions/27635292/transfer-files-using-lftp-in-bash-script)
- [Fastest segmented parallel sync of a remote directory over ssh | commandlinefu.com](http://www.commandlinefu.com/commands/view/13759/fastest-segmented-parallel-sync-of-a-remote-directory-over-ssh)
- [`~/.lftp.rc` parameters detailed](https://gist.github.com/gaubert/822090)
- [Shell scripting and LFTP | A Pipe and a Keyboard](http://apipeandakeyboard.com/2013/05/11/shell-scripting-and-lftp/)
- [How to store lftp command result to a variable](https://www.experts-exchange.com/questions/25279654/How-to-store-lftp-command-result-to-a-variable.html)
- [calling lftp from a bash script; howto pass variables into the command syntax](http://www.linuxquestions.org/questions/programming-9/calling-lftp-from-a-bash-script%3B-howto-pass-variables-into-the-command-syntax-4175444669/)

### Backup external server with `rsync`

	rsync -a username@www.mydomain.tld:/ /dst/dir

See [rsync](#rsync)

### `scp`

	scp -i /home/username/.ssh/id_rsa -r -p username@www.mydomain.tld:/ /dst/dir

### `sftp`

	sftp -i /path/to/private/keyfile remote.host.tld

### Other

Using tar or FTP, incrementaly add/changed/delete files (list made from `cron` or similar)

	find . -type f -mtime -7 -exec ls -l {} \; > list.txt
	find . -type f -exec ls -i {} + | sort -k2 > list.txt
	tar --create --file=archive.1.tar --listed-incremental=/var/log/usr.snar .
	tar -cf /dev/null -g /var/log/usr.snar .
	date +%s

	/backupdevice/folder
	date +%s%N > /backupdevice/folder.index

- http://www.grymoire.com/Unix/Inodes.html
- https://nixshell.wordpress.com/2010/10/07/inodes-ctime-mtime-atime/
- http://unix.stackexchange.com/questions/31255/on-what-occasion-will-inode-change
- https://stackoverflow.com/questions/16085958/scripts-find-the-files-have-been-changed-in-last-24-hours
- http://unix.stackexchange.com/questions/57825/how-to-diff-two-folders-by-inodes
- http://askubuntu.com/questions/704160/list-all-recently-changed-files-recursive
- http://superuser.com/questions/234158/show-both-ctime-and-atime-in-ls-output
- http://unix.stackexchange.com/questions/132819/incremental-file-back-up-by-date

- https://www.gnu.org/software/tar/manual/html_node/Incremental-Dumps.html
- https://www.gnu.org/software/tar/manual/html_node/Snapshot-Files.html
- http://unix.stackexchange.com/questions/25541/updating-tar-gz-daily-only-with-changed-files
- https://stackoverflow.com/questions/27763248/linux-tar-just-create-the-snar-file
- http://www.tuxradar.com/content/quick-guide-backups-using-tar
- http://chxo.com/be2/tar_backup_to_ntfs.html

## HTTP

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
	

[How to display request headers with command line curl - Stack Overflow](https://stackoverflow.com/questions/3252851/how-to-display-request-headers-with-command-line-curl/26644485#26644485)

### Simple HTTP server

	while true; do nc -l 8000 < response.http; done

	echo -e "GET / HTTP/1.1\r\nHost:example.com\r\nUser-Agent:Firefox\r\n\r\n" | nc example.com 80 > response.http

### Create `.htpasswd` file

	htpasswd -c /path/.htpasswd USERNAME

### wget

Multi purpose download tool

Store local browsable version of a page to the current dir

	(cd dir/ && wget -nd -pHEKk http://www.pixelbeat.org/cmdline.html)


Continue downloading a partially downloaded file

	wget -c http://www.example.com/large.file


Download a set of files to the current directory

	wget -r -nd -np -l1 -A '*.jpg' http://www.example.com/dir/


FTP supports globbing directly

	wget ftp://remote/file[1-9].iso/


Process output directly

	wget -q -O- http://www.pixelbeat.org/timeline.html | grep 'a href' | head


Download url at 1AM to current dir

	echo 'wget url' | at 01:00


Do a low priority download (limit to 20KB/s in this case)

	wget --limit-rate=20k url


Check links in a file

	wget -nv --spider --force-html -i bookmarks.html


Efficiently update a local copy of a site (handy from cron)

	wget -m http://www.example.com/

	wget -m -U "" http://example.com/path/dir

## Convert PDF 1.4

Force version

	gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4  -dColorConversionStrategy=/LeaveColorUnchanged -dDownsampleMonoImages=false -dDownsampleGrayImages=false -dDownsampleColorImages=false -dAutoFilterColorImages=false -dAutoFilterGrayImages=false -dColorImageFilter=/FlateEncode -dGrayImageFilter=/FlateEncode -o airbus_ar_2016_pdf1.4.pdf airbus_ar_2016.pdf

## SSH

Aka Secure SHell

Run command on $HOST as $USER (default command=shell)

	ssh $USER@$HOST command


Run GUI command on $HOSTNAME as $USER

	ssh -f -Y $USER@$HOSTNAME xeyes


Copy with permissions to $USER's home directory on $HOST

	scp -p -r $USER@$HOST: file dir/


Use faster crypto for local LAN. This might saturate GigE

	scp -c arcfour $USER@$LANHOST: bigfile


Forward connections to $HOSTNAME:8080 out to $HOST:80

	ssh -g -L 8080:localhost:80 root@$HOST


Forward connections from $HOST:1434 in to imap:143

	ssh -R 1434:imap:143 root@$HOST


Install public key for $USER@$HOST for password-less log in

	ssh-copy-id $USER@$HOST 

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

## Tunnel SSH

Redirection d'un port local vers une machine distante

	ssh -NfL 8080:127.0.0.1:0808 user@host

http://www.cyberciti.biz/faq/set-up-ssh-tunneling-on-a-linux-unix-bsd-server-to-bypass-nat/

## Windows networking

Note: samba is the package that provides all this windows specific networking support

Find windows machines. See also findsmb

	smbtree

Find the windows (netbios) name associated with ip address

	nmblookup -A 1.2.3.4

List shares on windows machine or samba server

	smbclient -L windows_box

Mount a windows share

	mount -t smbfs -o fmask=666,guest //windows_box/share /mnt/share

Send popup to windows machine (off by default in XP sp2)

	echo 'message' | smbclient -M windows_box

## Write email in local spool

	mail -s "Hello" localusername </dev/null

	/var/spool/mail/$USER
