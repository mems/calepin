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
- [\[Résolu\] Filezilla \<-\> FreeBox HD V5 : manque des fichiers vid - Internet & Réseaux - Zebulon](https://forum.zebulon.fr/topic/192646-r%C3%A9solu-filezilla-freebox-hd-v5-manque-des-fichiers-vid/)

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

Freebox Revolution V6 mini 4K (IR) use Freebox Crystal, v5 or Alice codes

Logitech Harmony 350
[Contour 4 | One For All](https://www.oneforall.com/universal-remotes/urc-1240-contour-4/support)
One For All Contour 4 Device 2018 (URC 1240 R01)
One For All Contour 4 Device 2016 (URC 1240 R00)
One For All Zapper+ (URC 6820 R00)

freebox mini 4K  (SAT)
URC 7960, freebox: 1482, 1976, (1455, 1976, 1961, 1624 ?)
URC 1240, Alice: 3455, 1585
URC 1240, Freebox: 1976, 3455

> La télécommande One for All URC 7955 Smart Control 5 fonctionne avec la Freebox mini 4K en utilisant le code 3455 et la touche LIST à la place de Marche/Arrêt.
> — [Univers Freebox :: Voir le sujet - (Mini 4K) Télécommande universelle One for All URC 7955 Smar](https://forum.universfreebox.com/viewtopic.php?t=70122)

> touches tres reactives, rayon IR large, memorisation facile, j'ai mis juste un peu de temps
> pour configurer la telecommande de Feebox revolution (code 3455) car le bouton Power ne repondait pas du coup j'ai transféré le signal de l'ancienne telecommande universelle par IR la commande. depuis tout marche à merveille!
> — [ONE FOR ALL SMART CONTROL 5 Télécommande universelle avec raccourci vers services de vidéo en streaming - télécommande tv, avis et prix pas cher - Cdiscount](https://www.cdiscount.com/high-tech/accessoires/one-for-all-smart-control-5-telecommande-universel/f-1062810-div8716184065590.html)

> La Freebox Mini 4K a un récepteur IR, donc pas besoin de dongle. La keymap est celle de la télécommande de la Freebox Crystal, la touche Free correspond à la touche "home" d'Android. Il suffit donc de configurer votre télécommande harmony de la même façon que pour la Freebox Crystal.
> — [FS#16363 : Port Infrarouge](https://dev.freebox.fr/bugs/task/16363)

> télécommande universelle infrarouge pourront bientôt piloter leur Freebox Revolution grâce à un dongle USB
> [...]
> que les codes pour les télécommandes universelles seront les mêmes que ceux enregistrés pour la comptabilité avec l’Alicebox v5.
> — [Free propose un adaptateur infrarouge pour sa Freebox Revolution](https://www.numerama.com/magazine/20479-free-propose-un-adaptateur-infrarouge-pour-sa-freebox-revolution.html)

> Vous confirmez que la télécommande du player Delta /one (V7) est bien wifi ?
> [...]
> Pouvoir aussi utiliser d'autre contrôleur infrarouge en attendant l'API de télécommande comme par exemple les Broadlin RMPRO ou MINI3
> [...]
> Les 2 télécommandes sont bien bluetooth.
> Il y a déjà un dongle infrarouge intégré
> — [FS#23059 : Infrarouge USB](https://dev.freebox.fr/bugs/task/23059)

- [FS#31148 : Player POP : Contrôle via Télécommande Infra Rouge Universelle](https://dev.freebox.fr/bugs/task/31148)
- [FS#21200 : Télécommande universelle one for all](https://dev.freebox.fr/bugs/task/21200)
- [Player Devialet Free : Contrôle depuis Broadlink RM ou Logitech Harmony](https://www.planete-domotique.com/blog/2019/02/27/player-devialet-rm-harmony/)
- [Freebox player et télécommande Harmony – Play With Free](http://play.with.free.fr/index.php/freebox-player-et-telecommande-harmony/comment-page-1/)
- [FS#3797 : Compatibilité Infra Rouge pour télécommandes universelles](https://dev.freebox.fr/bugs/task/3797)
- [Freebox Revolution et télécommande universelle « SD blog](http://sd55.free.fr/wordpress/?p=493&cpage=1)

> télécommande alice et freebox
>
> 0x80382601 1
> 0x80382602 2
> 0x80382603 3
> 0x80382604 4
> 0x80382605 5
> 0x80382606 6
> 0x80382607 7
> 0x80382608 8
> 0x80382609 9
> 0x80382600 0
> 0x8038265c ENTER
> 0x80382699 UP
> 0x8038269b LEFT
> 0x8038269c RIGHT
> 0x8038269a DOWN
> 0x8038265a VOLUMEDOWN
> 0x8038265b VOLUMEUP
> 0x8038260c POWER
> 0x803826cc MENU
> 0x8038260d MUTE
> 0x8038266d RED
> 0x8038266e GREEN
> 0x8038266f YELLOW
> 0x80382670 BLUE
> 0x80382683 BACK
> 0x803826d7 HOMEPAGE
> 0x80382697 PROGRAM
> 0x80382658 CHANNELUP
> 0x80382659 CHANNELDOWN
> 0x8038260f INFO
> 0x80382681 HELP
> 0x80382687 FAVORITES
> 0x80382654 OPTION
> 0x80382631 STOP
> 0x803826b8 PLAY
> 0x80382637 RECORD
> 0x8038264d PREVIOUSSONG
> 0x8038264c NEXTSONG
> 0x8038262e FASTFORWARD
> 0x8038262f REWIND
> 0x8038269e EXIT
> 0x80382649 MEDIA
> — [FS#17570 : Télécommandes universelles](https://dev.freebox.fr/bugs/task/17570)

Bouton long press (2s) On/Off = ouverture de l'assistant vocal

- [Univers Freebox :: Voir le sujet - (V6) télécommande universelle one for all urc 7960](https://forum.universfreebox.com/viewtopic.php?t=55615)
- [Freebox V6 et télécommande IR - One for all](https://forum.freenews.fr/index.php?topic=74473.0)

- [télécommande compatible Freebox](http://carnetress.free.fr/documentation/telecommande_universelle.html)
- [Freebox Revolution et télécommande universelle « SD blog](http://sd55.free.fr/wordpress/?p=493)

### One for all codes

> ## URC1240, URC1280: How do I program my code on the Contour remote?
>
> To program the basic code on your Contour remote, please follow the instructions mentioned below:
>
> 1. Press the device key (e.g. TV key) corresponding to the device you wish to control (e.g. television).
> 2. Press and hold down the SETUP key until the red LED underneath the POWER key blinks twice (the red LED will blink once then twice).
> 3. Enter the four-digit device code using the number keys. The red LED should blink twice.
>
> — [How do I program my code on the Contour remote?](https://www.oneforall.com/support/faq/urc1240-urc1280-how-do-i-program-my-code-contour-remote)

> ## All replacement remotes: How can I learn a missing function on my Replacement Remote using the original remote control?
>
> Your One For All remote is capable of copying functions straight from the original remote control that came with your device.
>
> To use the Learning feature, please follow the instructions below:
>
> 1. Press and hold the Green and Yellow keys until the light blinks once and then twice.
> 2. Enter 975, the LED light will blink twice.
> 3. Press the key on the Replacement remote where you would like to place the learned function, the LED will flash rapidly.
> 4. Press and hold the key on the original remote control that you wish to learn until the LED on the replacement remote blinks twice.
> 5. Repeat the above two steps by pressing any other key you wish to learn on.
> 6. Press and hold the OK key to store the learned function until the LED blinks twice.
>
> Additional information:
>
> - It is possible to learn up to 50 functions on this remote
> - A time-out will occur if no signal is received from the original remote within 5 seconds. To retry, press the key to be learned on again.
> - One long blink indicates the remote did not capture the signal correctly.
> - Two long blinks indicate the memory is full.
>
> — [How can I learn a missing function on my Replacement Remote using the original remote control?](https://www.oneforall.com/support/faq/all-replacement-remotes-how-can-i-learn-missing-function-my-replacement-remote-using-original-remote-control)

> ## All replacement remotes: How can I delete a learned key on my Replacement Remote?
>
> If you would like to delete a learned function that you no longer require, please follow the procedure outlined below:
>
> 1. Press and hold the Green and Yellow keys until the light blinks once and then twice.
> 2. Enter 976, the LED will blink twice.
> 3. Press the learned key you wish to reset twice, the LED will blink twice.
>
> Additional Information:
>
> - You can delete a learned key by overwriting it with a new learned function.
> - If a learned function used in a macro is subsequently deleted, the macro will revert to sending the keys original function.
>
> — [How can I delete a learned key on my Replacement Remote?](https://www.oneforall.com/support/faq/all-replacement-remotes-how-can-i-delete-learned-key-my-replacement-remote)

> ## All replacement remotes: How do I perform a factory reset on my Replacement Remote?
>
> Before resetting the replacement remote , please take the following into account:
> If you have ever sent in your remote control to our Upgrade Service for an update, these codes will be erased as well. In that case, it is highly advised not to perform a factory reset.
>
> To reset your remote to the manufacturer's setting, please follow the procedure outlined below
>
> If you have the chip version R00, then please do the following steps:
>
> 1. Hold down the GREEN + YELLOW key, until the LED blinks twice
> 2. Enter the code 981
> 3. The LED blinks now four times and everything is deleted from your remote control
>
>
>
> If you have the chip version R01, then please do the following steps:
>
> 1. Remove a battery from the remote and press a button to discharge the remote entirely
> 2. Reinsert the battery – the LED should blink twice
> 3. Press the digits 2 and 8 simultaneously within 6 seconds – the LED should blink twice
> 4. Enter the code 981, the LED will blink 4 times
> 5. The remote is now reset to its factory defaults
>
> You can now setup your remote again.
>
> N.B. The procedure must be performed within 6 seconds of applying power to the remote, that is, inserting batteries. After 6 seconds of Power it will not activate.
>
> — [How do I perform a factory reset on my Replacement Remote?](https://www.oneforall.com/support/faq/all-replacement-remotes-how-do-i-perform-factory-reset-my-replacement-remote)

> ## All replacement remotes: Blinking back the device code
>
> 1. Press the device key (e.g. TV key) corresponding to the device you wish to control (e.g. television).
> 2. Press and hold down the SETUP key until the red LED underneath the POWER key blinks twice (the red LED will blink once then twice).
> 3. Press 990, the light should blink twice.
> 4. Press 1, count the number of blinks. (1st digit)
> 5. Press 2, count the number of blinks. (2nd digit)
> 6. Press 3, count the number of blinks. (3rd digit)
> 7. Press 4, count the number of blinks. (4rd digit)
>
> If the remote does not blink it means the number is 0.
> This is your 3-digit setup code.

> ## URC1240, URC1280: How do I reset a device on my Contour remote?
>
> If you would like to reset a device mode, please use the following procedure:
>
> 1. Hold down SETUP until the light blinks once and then twice .
> 2. Enter the code 992 (the light should blink twice).
> 3. Press twice the device key to reset, the light will blink twice.
> 4. The device key has now been deactivated.
>
> Additional Information:
>
> Mode reassignment erases all Key Moved and learned keys for that mode.
>
> — [How do I reset a device on my Contour remote?](https://www.oneforall.com/support/faq/urc1240-urc1280-how-do-i-reset-device-my-contour-remote)

> ## Redefining a device key
>
> 1. Press the device key (e.g. TV key) corresponding to the device you wish to control (e.g. television).
> 2. Press and hold down the SETUP key until the red LED underneath the POWER key blinks twice (the red LED will blink once then twice).
> 3. Enter code 992.
> 4. Press the device key to reset, key you want moved
> 5. Press the device key you want to replace.
>
> Example: If you want the Aux key to be a TV key:
> "MAGIC" (2 blinks) 9 - 9 - 2, TV (you want to move TV)
> Then AUX (you want to replace AUX).

> ## URC6430, URC6440: How do I associate the volume keys to one particular device on my Simple remote?
>
> It is possible to lock the volume on your Simple remote to a single device key (for example: the volume control could be linked only to a TV). This means that when the remote is in DVD or SAT mode and the volume keys are pressed, the TV volume will still be activated.
>
> If you would like to have the volume locked to a particular device, please follow the procedure outlined below:
>
> 1. Hold down Setup until the light blinks once and then twice.
> 2. Enter code 993, the light will blink twice.
> 3. Press the relevant device you wish to assign volume control to.
>
> — [How do I associate the volume keys to one particular device on my Simple remote?](https://www.oneforall.com/support/faq/urc6430-urc6440-how-do-i-associate-volume-keys-one-particular-device-my-simple-remote)

> ## Volume Default
>
> Use this to get the original volume to work on each device.
>
> 1. Hold down Setup until the light blinks once and then twice.
> 2. Enter code 993
> 3. Press the VOLUME+ key, you will get two blinks.
>
> Now The volume is set for all original devices.

> ## URC1240, URC1280: How can I program a missing function on my Contour remote?
>
> It is possible to add missing functions via a procedure known as “Key Magic.”
> If you provide the relevant information via this web form we will supply a 5 digit code to be programmed for each missing function and the programming procedure.
>
> To use the Key Magic procedure, please follow the instructions outlined below:
>
> 1. Press the relevant device key.
> 2. Hold the Setup key until the light blinks twice.
> 3. Enter 994, the light blinks twice.
> 4. Press the Setup key once and let go.
> 5. Enter the 5 digit function code of the required function.
> 6. Press the One For All key you wish to assign the function to.
> 7. The light blinks twice and that key should now function.
>
> — [How can I program a missing function on my Contour remote?](https://www.oneforall.com/support/faq/urc1240-urc1280-how-can-i-program-missing-function-my-contour-remote)

> ## URC1210, URC1240, URC1280: How can I delete a macro on my Contour remote?
>
> In order to delete a macro, please follow the instructions below:
>
> 1. Hold the Setup key down until the light blinks twice.
> 2. Press 995, the light should blink twice.
> 3. Press the key you assigned the Macro to.
> 4. Hold the Setup key down to delete the Macro, the light will blink twice.
>
> — [How can I delete a macro on my Contour remote?](https://www.oneforall.com/support/faq/urc1210-urc1240-urc1280-how-can-i-delete-macro-my-contour-remote)

- [Manual Programming - 9xx Commands - JP1 Remotes](https://web.archive.org/web/20180814211735/http://www.hifi-remote.com/wiki/index.php?title=Manual_Programming_-_9xx_Commands)
- [Everything under control with the official One For All homepage.](https://web.archive.org/web/20190302000603/http://hifi-remote.com/ofaold/e2pro2.html)
- URC 1240 [Knowledge base | One For All](https://www.oneforall.com/faqs?search=URC1240)
- [Infrarouge : bidouilles avec WinLIRC      \[ PafGadget \]](http://pafgadget.free.fr/bidouillages/infrarouge.htm)

## Netflix

L'application "mobile" fonctionne, mais n'apparait pas sur le launcher (accessible uniquement via Settings > Applications > Downloaded applications). L'interface n'est pas vraiment navigable avec une télécommande (utiliser une souris USB)

See [Android TV apps](Android#android-tv-apps)

- [Freebox mini 4k : comment installer Netflix facilement](http://www.universfreebox.com/article/35826/Freebox-mini-4k-comment-installer-Netflix-facilement)
- [Tuto : comment installer Netflix facilement sur Freebox mini 4K](http://www.universfreebox.com/article/40235/Tuto-comment-installer-Netflix-facilement-sur-Freebox-mini-4K)

- [Netflix - Android Apps on Google Play](https://play.google.com/store/apps/details?id=com.netflix.ninja) - Android touch devices (mobile & tablet)
- [Netflix - Android Apps on Google Play](https://play.google.com/store/apps/details?id=com.netflix.mediaclient) - Android TV version
- [Netflix APKs - APKMirror](https://www.apkmirror.com/apk/netflix-inc/netflix/)
- [Netflix APKs - APKMirror](https://www.apkmirror.com/apk/netflix-inc/netflix-android-tv/)
