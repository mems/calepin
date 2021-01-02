> - `greenfield` : Cette option, si elle est activée, permet aux équipements compatibles 802.11n de communiquer entre eux plus rapidement si aucun autre composant WiFi antérieur (802.11a, 802.11b ou 802.11g) n’est présent dans leur champ d’action.
> - `shortgi20`, `shortgi40` : Permettent, si cochées, de réduire les intervalles de transmissions (Guard interval) afin d'augmenter les vitesses de transfert.
> - `ldpc` (Low Density Parity Check) / Codes "Gallager" : Codes linéaires correcteurs d'erreurs hérités de la norme 802.16e (Mobile WiMAX), ne concernant que les normes 802.11n et 802.11ac.
> - `smps` : Coupe une partie des antennes quand il n'y a pas d'activité afin de réduire la consommation d'énergie.
> - `rx_stbc` / `tx_stbc` : Améliore la fiabilité du transfert (RX ou TX) en envoyant plusieurs fois les mêmes paquets, ce qui réduit les erreurs mais réduit grandement le débit également.
> - `delayed_ba` : Permet d'envoyer l'acquittement pour plusieurs trames d'un coup au lieu d'un acquittement pour chacune. Améliore le débit mais augmente aussi la latence.
> - `max_amsdu_7935` : Permet d'agréger plusieurs paquets de données en un seul gros paquet de 7935 octets, ce qui donne moins d'encapsulation et accélère donc le debit, mais plus de données sont perdues en cas d'erreur.
> - `dsss_cck_40` : Vieux standard hérité de la norme 802.11b.

> — [\[Tuto\] - Optimisations WiFi - Association WDA - Forums](http://forum.wda-fr.org/viewtopic.php?f=13&t=2463#p14634)

Réglages Freebox:

- `greenfield`: On
- `shortgi20`, `shortgi40`: On
- `ldpc`: Off (désactivé)
- `smps`: "Désactivé", "Dynamic" semble ne pas marcher avec la freebox (fait planter la carte)
- `rx_stbc` / `tx_stbc`: On
- `delayed_ba`: Off
- `max_amsdu_7935` : On
- `dsss_cck_40`: Off (désactivé)
- `psmp`: Off (désactivé)
- `lsig_txop_prot`: Off (désactivé)

- [freeboxv6_boosterwifi - Qui n’a jamais rêvé d’avoir un réseau WiFI performant ?](https://doc.ubuntu-fr.org/freeboxv6_boosterwifi)
- [Quel canal Wi-Fi choisir pour optimiser son débit ?](https://lafibre.info/wifi/quel-canal-wi-fi-choisir-pour-optimiser-son-debit/)

## SD Card Wi-Fi server

- [Eye-Fi orphans 14 products, which will therefore cease to function | Boing Boing](https://web.archive.org/web/20201111172652/https://boingboing.net/2016/06/30/eye-fi-orphans-14-products-wh.html)
- Charles Lohr hacks
	- [AVR Communicating with Transcend WiFi SD - YouTube](https://www.youtube.com/watch?v=-Z9TrZQw16s)
	- [OLED Display and Internet Status on Transcend WiFi with Motherboard - YouTube](https://www.youtube.com/watch?v=HT4W3CPlnAU)
	- [Mini Host and Display for Transcend Wifi SD Card - YouTube](https://www.youtube.com/watch?v=5Rr9kSqjX98)
	- [electrical - Revision 741: /SDComputer](https://web.archive.org/web/20170621004355/https://cnlohr.net/pubsvn/electrical/SDComputer/)
- [eCos Open Source License – Eye-Fi](https://web.archive.org/web/20160316224128/https://help.eyefi.com/hc/en-us/articles/301754-eCos-Open-Source-License)
- [Best of Both Worlds: Hacking an EyeFi SD Card to run CHDK | Under Design](https://web.archive.org/web/20160405092006/http://blog.undr.com/2011/02/best-of-both-worlds-hacking-an-eyefi-sd-card-to-run-chdk/)
- [Return Boolean True: Eye Fi Standalone Server Version 2.0](https://web.archive.org/web/20190906155716/http://www.returnbooleantrue.com/2009/04/eye-fi-standalone-server-version-20.html) - [tachang/EyeFiServer: An open source Eye-Fi Server written in Python](https://github.com/tachang/EyeFiServer)
- [Hacking An SD Slot For WiFi | Hackaday](https://web.archive.org/web/20201108090444/http://hackaday.com/2015/08/15/hacking-an-sd-slot-for-wifi/)
- [Standalone Eye-Fi Upload | Hackaday](https://web.archive.org/web/20201022185508/https://hackaday.com/2009/03/15/standalone-eye-fi-upload/)
- [Transcend Wifi SD Card Is A Tiny Linux Server | Hackaday](https://web.archive.org/web/20201108094227/https://hackaday.com/2016/06/30/transcend-wifi-sd-card-is-a-tiny-linux-server/)
- [Biobug.org » Hacking the eye-fi to keep your data home](https://web.archive.org/web/20200608190149/http://biobug.org/index.php/2009/03/14/hacking-the-eye-fi-to-keep-your-data-home/) - https://web.archive.org/web/20200223235204/http://biobug.org/dist/
- [Eye-Fi | Magic Lantern Firmware Wiki | Fandom](https://web.archive.org/web/20200724165212/https://magiclantern.fandom.com/wiki/Eye-Fi)


- [Wi-Fi positioning system - Wikipedia](https://en.wikipedia.org/wiki/Wi-Fi_positioning_system)
