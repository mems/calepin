## Security

### Audit — Lynis

Scans the system and available software, to detect security issues. Beside security related information it will also scan for general system information, installed packages and configuration mistakes

This software aims in assisting automated auditing, software patch management, vulnerability and malware scanning of Unix based systems. It can be run without prior installation, so inclusion on read only storage is no problem (USB stick, cd/dvd).

Lynis assists auditors in performing Basel II, GLBA, HIPAA, PCI DSS and SOX (Sarbanes-Oxley) compliance audits.

Install:

	sudo apt-get install lynis

Exec:

	sudo lynis -c

	sudo grep Warning /var/log/lynis.log

	sudo grep Suggestion /var/log/lynis.log

- http://www.rootkit.nl/projects/lynis.html
- http://www.rootkit.nl/files/lynis-documentation.html

## Localized folders

- `xdg-user-dir`
- http://askubuntu.com/questions/194124/how-to-get-language-variables-desktop-folder-name-document-folder-name-etc

## Too many open files

	lsof | awk '{ print $2; }' | uniq -c | sort -rn | head

	lsof > ~/Desktop/lsof.log
	cat ~/Desktop/lsof.log | awk '{ print $2 " " $1; }' | sort -rn | uniq -c | sort -rn | head -20
	vim ~/Desktop/lsof.log

- [filesystem - Too many open files - how to find the culprit - Ask Ubuntu](http://askubuntu.com/questions/181215/too-many-open-files-how-to-find-the-culprit)

## Selective sync using Dropbox

- [Simplify your server using Dropbox, Selective Sync < blog :: buildcontext the personal blog of Ben Hedrington](http://buildcontext.com/blog/2012/dropbox-linux-ubuntu-ec2-linode-selective-sync)

## Command autocomplete

See `complete` buildin command

http://www.linuxjournal.com/content/more-using-bash-complete-command

## Find on which physical device a folder is located

	df /root
	Filesystem           1K-blocks      Used Available Use% Mounted on
	/dev/sda1              1043289    194300    795977  20% /

## Live USB drive

Live CD, live USB, bootable USB

- [UNetbootin - Homepage and Downloads](https://unetbootin.github.io/)