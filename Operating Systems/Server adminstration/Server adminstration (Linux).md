- [Admin Debian | Tutoriels sur l'administration du système Debian](http://www.admin-debian.com/)
- [Configuration d'un serveur dédié de A à Z - Alsacreations](http://www.alsacreations.com/tuto/lire/621-Configuration-d-un-serveur-dedie-de-A-a-Z.html)
- [Sécurisation du serveur (SSH, firewall iptables, fail2ban...) - Alsacreations](http://www.alsacreations.com/tuto/lire/622-Securite-firewall-iptables.html)
- [ISPConfig Hosting Control Panel](http://www.ispconfig.org/)

# Softwares

## Proftp (FTP server)

- [Documentation/Réseaux/Application/FTP : Sécuriser proftpd [Root Me : plateforme d'apprentissage dédiée au Hacking et à la Sécurité de l'Information]](http://www.root-me.org/fr/Documentation/Reseaux/Application/FTP/Securiser-proftpd)
- [HOWTO : Create a FTP server with user access (proftpd)](http://ubuntuforums.org/showthread.php?t=79588)

### Bloquer les utilisateurs dans leurs dossier par défaut

Editer le fichier `/etc/proftpd/proftpd.conf` :

	DefaultRoot ~

Exclure des utilisateurs systèmes d'accès au FTP :

	/etc/ftpusers

Il faut que dans `/etc/prodtpd/proftpd.conf` il y ai l'instruction :

	UseFtpUsers on

* `man ftpusers`

### Log of files transactions

	/var/log/proftpd/xferlog

* http://linux.die.net/man/5/xferlog

### Connections

Voir les connections en live

	ftptop

### FTP over TLS/SSL

* http://www.proftpd.org/docs/howto/TLS.html

## Apache

- [Documentation/Réseaux/Application/HTTP : Sécuriser Apache [Root Me : plateforme d'apprentissage dédiée au Hacking et à la Sécurité de l'Information]](http://www.root-me.org/fr/Documentation/Reseaux/Application/HTTP/Securiser-Apache)

Activer une configuration de virtual host (site), correspondant au fichier `example.com` dans `/etc/apache2/sites-available/` :

	a2ensite example.com

Désactiver une configuration :

	a2dissite example.com

Activer un module, disponible dans `/etc/apache2/mods-available` :

	a2enmod mime_magic

Désactiver un module :

	a2dismod mime_magic

### Recharger la configuration d'Apache

	/etc/init.d/apache2 reload

### Live de logs d'accès d'apache

	tail -f /var/log/apache2/access.log

### Configuration

Il est possible de définir les configurations d'apache (et php), dans les fichiers `.htaccess` ou directement dans les informations de vhosts.

Exemple, pour la limite de mémoire de PHP (directive `PHP_INI_SYSTEM`):

	<VirtualHost *:80>
		DocumentRoot "..."
		ServerName ...
		php_admin_value memory_limit 128M
	</VirtualHost>

- http://php.net/manual/en/configuration.changes.php
- http://www.php.net/manual/en/ini.list.php

## MySQL (sql server)

### Backup entière des bases :

	mysqldump -u root -p --all-databases | /bin/gzip > mysql_backup.sql.gz

	mysqldump -h localhost -u root -p'password%$' --all-databases > /srv/data/tmp/mysql_backup/`date '+%F'`.databases.sql ; rm /srv/data/tmp/mysql_backup/`date '+%F' --date '1 weeks ago'`.databases.sql

### Fichiers de configuration

Default options are read from the following files in the given order:

`/etc/my.cnf` (global), `/usr/local/etc/my.cnf` (server-specific as `mysql-data-dir/my.cnf`), `~/.my.cnf` (user-specific)

For MAMP (Mac Apache MySQL PHP) it's include also the default (server-specific) file location `/Applications/MAMP/conf/my.cnf`

To get configuration file sorted by order of preference

	mysql --help | grep cnf

To know current running mysql server conf file:

	ps ax | grep '[m]ysqld'
	# or
	cat /proc/$(pidof mysqld)/cmdline | tr '\0' '\n'
	# or
	tr '\0' '\n' < /proc/$(pidof mysqld)/environ | grep -i cnf

And find `--defaults-file` argument

- http://www.dbasquare.com/2012/04/01/how-to-find-mysql-configuration-file/

### Reset root password

Start daemon :

	mysqld --skip-grant-tables &

Login in root user without password (skip) :

	mysql -u root -p mysql

(optionally) Restore root account infos: (in mysql interactive mode or by SQL file) :

	INSERT INTO `user` (`Host`, `User`, `Password`, `Select_priv`, `Insert_priv`, `Update_priv`, `Delete_priv`, `Create_priv`, `Drop_priv`, `Reload_priv`, `Shutdown_priv`, `Process_priv`, `File_priv`, `Grant_priv`, `References_priv`, `Index_priv`, `Alter_priv`, `Show_db_priv`, `Super_priv`, `Create_tmp_table_priv`, `Lock_tables_priv`, `Execute_priv`, `Repl_slave_priv`, `Repl_client_priv`, `Create_view_priv`, `Show_view_priv`, `Create_routine_priv`, `Alter_routine_priv`, `Create_user_priv`, `ssl_type`, `ssl_cipher`, `x509_issuer`, `x509_subject`, `max_questions`, `max_updates`, `max_connections`, `max_user_connections`) VALUES (0x6c6f63616c686f7374, 0x726f6f74, 0x2a30303045314145434438383730463730443332433041333546384632393236464636373244333333, 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', '', '', '', '', 0, 0, 0, 0), (0x6865646765686f67, 0x726f6f74, 0x2a30303045314145434438383730463730443332433041333546384632393236464636373244333333, 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', '', '', '', '', 0, 0, 0, 0);

Change root password :

	SET PASSWORD FOR root@localhost = PASSWORD('newpwd');

or

	UPDATE user SET Password=PASSWORD('newpwd') WHERE User='root';

and check it

	SELECT Host, User, Password FROM user WHERE User = 'root';

(optionally)

	flush privileges;

shutdown daemon

	mysqladmin -u root -p shutdown

Restart after

	/etc/init.d/mysql start

* [Resetting a forgotten MySQL root password](http://www.debian-administration.org/articles/442)

### Logs

	grep mysql /var/log/syslog | less

### Accès remote

Dans le fichier de configuration:

	# Disable Remote Connections
	bind-address=127.0.0.1

## PPTP (VPN)

### Installation de pptpd

Lancer la commande :

	apt-get install pptpd

Editer le fichier `/etc/pptpd.conf` :

	# Adresse IP attribuée au serveur sur le VPN
	localip 192.168.1.1
	
	# Adresses IP attribuables automatiquement par le VPN (de 128 à 255)
	remoteip 192.168.1.128-255

Editer le fichier `/etc/ppp/pptpd-options` :

	# Nom du VPN, il sera utilisé dans le fichier "/etc/ppp/chap-secrets"
	name LeNomDuVPN
	
	# Ca doit avoir un rapport avec l'encryptage et l'authentification
	require-mschap-v2
	require-mppe-128

	# Configuration des DNS
	# Il semble que ce soit aussi possible dans /etc/PPP/options
	# mais je ne connais pas la différence
	ms-dns 208.67.222.222
	ms-dns 208.67.220.220

Editer le fichier `/etc/ppp/chap-secrets` :

	# Fichier des comptes utilisateurs
	# Il est possible d'utiliser l'authentification du système (ou Samba), mais ce n'est pas le but ici
	# Le paramètre "LeNomDuVPN" doit correspondre avec le paramètre "name" du fichier "/etc/ppp/pptpd-options"
	
	# Un utilisateur dont l'IP est définie manuellement
	# Attention à ne pas définir une IP se trouvant dans "remoteip"
	tutu LeNomDuVPN UnAutreMotDePasse 192.168.66.85
	
	# Un utilisateur dont l'IP est obtenue dans "remoteip" de /etc/pptpd.conf
	toto LeNomDuVPN UnMotDePasse *

Redémarrer le VPN :

	/etc/init.d/pptpd restart

### Création de la passerelle réseau

Lancer les commandes :

	# Autoriser l'IP Forwarding 
	echo 1 > /proc/sys/net/ipv4/ip_forward
	
	# Mettre en place la translation de l'adresse
	iptables -t nat -A POSTROUTING -s 192.168.1.0/24 -j MASQUERADE

Sauvegarder la configuration d'iptables lors des reboot, voir {PARTIE CONCERNEE}

* [Création d'un serveur VPN Poptop](http://free.korben.info/index.php/Cr%C3%A9ation_d%27un_serveur_VPN_Poptop)
* [Configurer une passerelle réseau]](http://free.korben.info/index.php/Configurer_une_passerelle_r%C3%A9seau)
* [Getting IPTables to survive a reboot](http://www.debian-administration.org/articles/445)

## Postfix (SMTP server)

* http://christian.caleca.free.fr/smtp/installation_de_postfix.htm
* http://postfix.traduc.org/

## SVN

* http://svn1clicksetup.tigris.org/
* http://tortoisesvn.net/docs/release/TortoiseSVN_fr/index.html
* http://subversion.tigris.org/faq.html#multi-proj
* http://svnbook.red-bean.com/

## Cron

* http://en.wikipedia.org/wiki/Cron

## Network sharing

Use allow network sharing only via local network or secured VPN

Prefer use SMB2 or greater

Note: NFS allow on by IP not by user

- [HELIOS - AFP vs. SMB and NFS file sharing for network clients](http://www.helios.de/web/EN/news/AFP_vs_SMB-NFS.html)
- [NFS vs SAMBA](http://techno.firenode.net/article.sh?id=d201608040826134297)
- [ELI5 : What is the difference between SMB, CIFS and Samba? And NFS, if you want. : homelab](https://www.reddit.com/r/homelab/comments/2fawvq/eli5_what_is_the_difference_between_smb_cifs_and/)
- [Network File System — Wikipedia](https://en.wikipedia.org/wiki/Network_File_System)
- [Server Message Block — Wikipedia](https://en.wikipedia.org/wiki/Server_Message_Block)

## Email

SPF

- [Sender Policy Framework — Wikipedia](https://en.wikipedia.org/wiki/Sender_Policy_Framework)
- Gandi SPF record [Create a SPF record on Gandi - mail-tester.com](https://www.mail-tester.com/spf/gandi) [Sender Policy Framework (SPF) Records in DNS - Welcome to Gandi's Online Documentation Wiki - Gandi Docs](https://wiki.gandi.net/en/dns/zone/spf-record)
- [HOWTO - Define an SPF Record](http://www.zytrax.com/books/dns/ch9/spf.html)

## Service discovery

- [SRV record — Wikipedia](https://en.wikipedia.org/wiki/SRV_record)
- [Autoconfiguration in Thunderbird - Mozilla | MDN](https://developer.mozilla.org/en-US/docs/Mozilla/Thunderbird/Autoconfiguration) - Create config profile for Thunderbird