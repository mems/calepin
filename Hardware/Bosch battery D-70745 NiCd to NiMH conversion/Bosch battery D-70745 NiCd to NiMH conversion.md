Bosch 14,4 V 1,5 Ah replace Ni Cd to lithium-ion
Batterie Bosch type D-70745

- BMS 4S 40A~, ex: [OKY3399-7 OKYSTAR - Protection PCB | Nombre de mailles: 4; Li-Ion; Ifsm: 40A; 16,8VDC | TME - Composants électroniques](https://www.tme.eu/fr/details/oky3399-7/piles-boites-et-portants/okystar/)
- Lithium battery 18650 (3.7V 2200mAh) x4, ex: [INR18650-MH1 LG CHEM - Batt: Li-Ion | 18650,MR18650; 3,6V; 3200mAh; Ø18,4x65,1mm; 10A; ACCU-18650-3.2LG | TME - Composants électroniques](https://www.tme.eu/fr/details/accu-18650-3.2lg/accumulateurs/lg-chem/inr18650-mh1/), [INR18650 M26 LG CHEM - Batt: Li-Ion | 18650,MR18650; 3,65V; 2600mAh; Ø18,4x65,2mm; 10A; ACCU-INR18650-M26 | TME - Composants électroniques](https://www.tme.eu/fr/details/accu-inr18650-m26/accumulateurs/lg-chem/inr18650-m26/), [ICR 18650-22P SAMSUNG SDI - Batt: Li-Ion | 18650,MR18650; 3,6V; 2200mAh; Ø18,25x65mm; 10A; ACCU-18650-2.2P-HV | TME - Composants électroniques](https://www.tme.eu/fr/details/accu-18650-2.2p-hv/accumulateurs/samsung-sdi/icr-18650-22p/)
- Nikel strip (0.1x5x10m)
- Heat shrink PVC (2m 6.5ft Width 85mm Blue PVC Heat)

- [Lithium Battery + BMS + Nicd/Nimh Charger, Is it possible? Bosch cordless drill 14.4V PSR 1440 - YouTube](https://www.youtube.com/watch?v=ukKuCGG38n8)
- [Bosch 14,4 V replace Ni Cd to Lithium battery 14 4 - YouTube](https://www.youtube.com/watch?v=rvG3VEedmHw)

4x li-ion 2300

> Bms 4s 40A balanced. Connect BMS to 16.8V charger - BMS must activate.

**BMS Blanced is important** because it's let the batteries charging correctly. See [Battery balancing - Wikipedia](https://en.wikipedia.org/wiki/Battery_balancing)

About

> NiCd batteries have a nominal voltage of 1.2V and when fully charged they reach up to 1.3V. The old battery pack contained 12, which corresponds to a nominal battery voltage of 14.4V and a maximum of 15.6V at full charge. Instead the new battery is composed of 4 NMC lithium cells which have a nominal voltage of 3.7V but when fully charged they reach up to 4.2V and overall correspond to 16.8V at full charge. The charger of the old battery is built to charge up to a voltage of 15.6V so if you use it to charge the new lithium cells you will not damage them at all, but rather you will always charge them up to about 80% and it is an optimal condition for the life of lithium batteries. Obviously you will not exploit their potential to the maximum but if this is enough for you, this is fine! Hope I've been of help, congratulations again!
>
> — [Lithium Battery + BMS + Nicd/Nimh Charger, Is it possible? Bosch cordless drill 14.4V PSR 1440 - YouTube](https://www.youtube.com/watch?v=ukKuCGG38n8&lc=UgxDok-YbVQpI1Mg2rx4AaABAg)

> if you will charge your Li-Ion battery with 2 or more Amps, its not good for battery, they will heat up and battery life will be shorter. The Ni-Cd charger in video gives 2 Amps for sure.
>
> — [Lithium Battery + BMS + Nicd/Nimh Charger, Is it possible? Bosch cordless drill 14.4V PSR 1440 - YouTube](https://www.youtube.com/watch?v=ukKuCGG38n8&lc=UgxDok-YbVQpI1Mg2rx4AaABAg.9HH11Hx7iQp9NGn4aWwotg)

> Check the output voltage of the charger. If it's not over the fully charged voltage of the battery pack you want to charge and you have a bms, it should be safe, as long as the max charge current is within the li-ion cell charge specs.
>
> — [Lithium Battery + BMS + Nicd/Nimh Charger, Is it possible? Bosch cordless drill 14.4V PSR 1440 - YouTube](https://www.youtube.com/watch?v=ukKuCGG38n8&lc=UgxGo-OjTKCvIc5MFJp4AaABAg.978nziiRDv69AeliPUtu96)

> He is using the correct BMS (4S 40A). Which is designed for, as the name suggests, a 4 cells in series. 40A is the maximum continuous discharge current and 20A is the maximum continuous charging current. Those numbers assume very good cooling so they're to be considered an upper limit. One thing to note about the connections (soldering) is that the inner connections between the 4 cells and the BMS don't need to be heavy gauge. They won't be carrying any serious current as they're for sensing.
>
> As far as i can see and keep in mind that i am a bit old. That's an AL 60 DV Bosch charger for the 14.4v Ni-Cd battery. The old battery got 12 cells each with 1.2v nominal to make the total of 14.4v. The charger output voltage is around 15.83v which was just fine for the old Ni-Cd at 1.32v per cell but a bit low for the 18650. The new 18650s can take up to 4.2v per cell or 16.8 for the battery as he says at 17:12 in the video.
>
> Long story short, the charger output is a bit lower than what the BMS can work with if you want 4.2v per cell. I think that BMS needs something like 18.1v input to be able to charge the new cells fully. So you can either gut the charger, keep the shell and the contacts and install a small 18v SMPS  board inside which is kind of a crappy solution because it won't supply the current for fast charging. Or you can hack whatever board Bosch put in there to get the 18 volts you need. Some of those charger revisions work with PICs, Max232s or the TL494.
>
> — [Lithium Battery + BMS + Nicd/Nimh Charger, Is it possible? Bosch cordless drill 14.4V PSR 1440 - YouTube](https://www.youtube.com/watch?v=ukKuCGG38n8&lc=UgyuJgQMyNxR9hIfbv54AaABAg.96aZCjFUDwv96aulyrMNyl)

## Solder batteries

- [How to Solder Li-ion 18650 Cells Correctly in 2023 - No Welding! - YouTube](https://www.youtube.com/watch?v=CkbKCwelx0g)

- 435-455°C, wide tip
- don't use acid based flux
- rough the cell ends with sandpaper
- few seconds (1-3) of applying the iron

- [batteries - Is soldering wires directly on a NiMh battery safe? - Electrical Engineering Stack Exchange](https://electronics.stackexchange.com/questions/75057/is-soldering-wires-directly-on-a-nimh-battery-safe)
- [Le soudage des éléments](https://web.archive.org/web/20210603094706/http://www.overrc.com/techniques/accus/cablageaccus/soudage.htm)
- [RC Infos ¦ Site informatif sur le modélisme](https://web.archive.org/web/20210603094707/http://www.rcinfos.com/2006/2006_03_11_accus.php)
- [Souder un pack d’accus 1/10 éme :](https://web.archive.org/web/20210122211314/http://christopheb34.free.fr/Technique/souder_un%20pack_1-10eme.htm)
- [\[Aeromodelisme.com - Le webzine de l’aéromodélisme\] La fabrication d'un accus en image](https://web.archive.org/web/20160324172921/http://aero.modelisme.com/spip.php?article60)
- [Créer réparer vos pack d’accus au Nickel – Ni-Cd.net](https://web.archive.org/web/20210127024711/https://ni-cd.net/wpnicd/index.php/creer-reparer-vos-pack-daccus-au-nickel/)

Other solutions:

- buy batteries with solder tab
- use spot welding
