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
