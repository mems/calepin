# Freebox

## Enregistrements protégé

### Software


- Freebox Revolution, Server: `/private/apps/fbxpvr/private-records`
- Freebox HD: `/.private-records`
 
	Vidéo
	ID : 68 (0x44)
	ID de menu : 1 (0x1)
	Format : AVC
	Format/Info : Advanced Video Codec
	Profil du format : High@4.0
	Durée : 43s 613ms
	Encryption : Encrypted

	Audio #1
	ID : 69 (0x45)
	ID de menu : 1 (0x1)
	Format : AAC
	Format/Info : Advanced Audio Codec
	Langue : Français
	Encryption : Encrypted

Use XFS attributes to store infos:

	user._signature="abe69b8d357ec2c303c22e6c1b1e4cd6a6fdf9aa"
	user.index-file-path="/media/Disque dur/.private-records//.C+ Cinema - Bienvenue chtis - 23-03-2009 20h44 1h46m.ts.idx"
	user.record-bouquet="FREEBOX TV"
	user.record-channel="41"
	user.record-control-url
	user.record-date="20090323"
	user.record-ecm-pid="1500"
	user.record-scramble-key="163a172eb304d872b1eed109e2ba44b5"
	user.record-service="219"
	user.record-time="2044"
	user.resume-offset=0sAIBAAAAAAAA=

Use CAS Conditional Access System? Ni CSA (Common Scrambling algorithm)

- [\[NATIONAL\] Opération à coeur ouvert : changer le disque dur interne de la Freebox HD - Commentaires - Journal du Freenaute : Les forums](https://www.journaldufreenaute.fr/forum/index.php?/topic/1201-national-op%C3%A9ration-%C3%A0-coeur-ouvert-changer-le-disque-dur-interne-de-la-freebox-hd/)
- [\[NATIONAL\] Opération à coeur ouvert : changer le disque dur interne de la Freebox HD - Page 4 - Commentaires - Journal du Freenaute : Les forums](https://www.journaldufreenaute.fr/forum/index.php?/topic/1201-national-op%C3%A9ration-%C3%A0-coeur-ouvert-changer-le-disque-dur-interne-de-la-freebox-hd/&page=4&tab=comments#comment-54806)
- http://www.lacelluledusat.tv/showthread.php?4854-Cherche-infos-compl%E9mentaires-sur-proc%E9d%E9-de-d%E9cryptage-TS-%28Freebox-Revolution%29

### Hardware

- http://www.commentcamarche.net/forum/affich-3317545-freebox-comment-recuperer-enregistrements

## Wi-Fi

- [Univers Freebox :: Voir le sujet - Configuration radio et options des parametres avancés](http://forum.universfreebox.com/viewtopic.php?p=441970&sid=328e17ef854d486c10cfc18f7c610ab0#441970)
- [FS#15008 : Documentation des paramètres Wifi Avancés](http://dev.freebox.fr/bugs/task/15008)

## VPN

See [VPN](VPN).

Activer le serveur VPN IPSec/IKEv2 au préalable

- serveur : ip publique de la Freebox on l'un de ses nom de domain (sauf `mafreebox.freebox.fr`, si on veux pouvoir accéder de l'extérieur au VPN)
- id. distant : info donné dans la configuration sur serveur VPN. Quelque chose comme `fbxvpn_psk`

## Media partagés

Utiliser le SMB avec l'application native si possible. Si Android, utiliser VLC ou Kodi

Eviter d'utiliser le UPnP/DLNA car les sous titres ne sont pas supporté (sauf si ils sont embarqués dans le fichier video)

## Remote

To increase reactivity on Freebox Mini 4K player disable HDMI CEC. **Need to be checked.** See [FS#16584 : allumage du player impossible avec la télécommande](http://dev.freebox.fr/bugs/task/16584)

## Télécommande universelle

Freebox Mini 4k support Freebox Crystal IR

- [FS#17570 : Télécommandes universelles](https://dev.freebox.fr/bugs/task/17570)
- [La télécommande - Assistance Free](http://www.free.fr/assistance/91.html)
- [Freebox — Wikipédia](https://fr.wikipedia.org/wiki/Freebox)

Logitech Harmony 350:
- manufacturer: "Free Telecom"
- device model number: "Free Telecom Freebox mini 4K"
- power delay: 1.5s
- inter-key delay: 100ms
- inter-device delay: 500ms
- device command repeat: 0

## Netflix

L'application "mobile" fonctionne, mais n'apparait pas sur le launcher (accessible uniquement via Settings > Applications > Downloaded applications). L'interface n'est pas vraiment navigable avec une télécommande (utiliser une souris USB)

See [Android TV apps](Android#android-tv-apps)

- [Freebox mini 4k : comment installer Netflix facilement](http://www.universfreebox.com/article/35826/Freebox-mini-4k-comment-installer-Netflix-facilement)
- [Tuto : comment installer Netflix facilement sur Freebox mini 4K](http://www.universfreebox.com/article/40235/Tuto-comment-installer-Netflix-facilement-sur-Freebox-mini-4K)

- [Netflix - Android Apps on Google Play](https://play.google.com/store/apps/details?id=com.netflix.ninja) - Android touch devices (mobile & tablet)
- [Netflix - Android Apps on Google Play](https://play.google.com/store/apps/details?id=com.netflix.mediaclient) - Android TV version
- [Netflix APKs - APKMirror](https://www.apkmirror.com/apk/netflix-inc/netflix/)
- [Netflix APKs - APKMirror](https://www.apkmirror.com/apk/netflix-inc/netflix-android-tv/)