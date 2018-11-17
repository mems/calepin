Object listing

- [Numérisation — Wikipédia](https://fr.wikipedia.org/wiki/Num%C3%A9risation)
- [Digital object identifier — Wikipedia](https://en.wikipedia.org/wiki/Digital_object_identifier)
- [Préparer des images numériques - E.Bacquet - Librairie Eyrolles](http://www.eyrolles.com/Audiovisuel/Livre/preparer-des-images-numeriques-9782212123432) and [Préparer des images numériques - extract Chapter 7 - E.Bacquet.pdf]()

Volume d’information utile à capter sur un film argentique:

Format de film			Gris 8 bits		RVB 24 bits		Résolution d’analyse
Vue d’un film 35 mm		7 Mo			20 Mo			4 000 ppi
Film 24 × 36 mm			20 Mo			60 Mo			4 000 ppi
Film 6 × 6 cm			40 Mo			120 Mo			3 000 ppi
Film 4 × 5 pouces		50 Mo			150 Mo			1 800 ppi
Film 8 × 10 pouces		130 Mo			4 000 Mo		1 400 ppi


## Objectif

- https://github.com/danielquinn/paperless
- [DocumentSnap: Going Paperless And The Paperless Office](http://www.documentsnap.com/)

Listing et numérisation d'un objet permet de rattacher des données à celui ci et d'avoir une représentation numérique (dans le cas ou c'est possible).

Exemple : le listing d'une voiture, cela permet :

- d'y faire référence de façon numérique dans des documents (carte grise, assurance, factures répartitions, etc.)
- de lier des données comme le numéro d'immatriculation, la couleur, nombre de place, trajet parcourus, nombre de kilomètres parcourut, date d'achat, conducteur / pilote, etc.
- de rechercher, filtrer en fonction de critères basé sur les données parmi un ensemble d'objets numérisés

Exemple : la numérisation un document, cela permet :
 
- d'y faire référence de façon numérique (document : page → line ou anchor)
- de lier des données comme le contexte, la date de réception, le type de document (facture, devis, contrat, etc.)...
- transmettre, copier ça représentation numérique de façon infinie, sans contraintes physique (un document est une représentation physique d'informations)
- de rechercher, filtrer en fonction de critères basé sur les données parmi un ensemble d'objets numérisés

Un objet sera listé et le produit de la numérisation donner lieu à un autre objet (copie numérique) qui sera lié au premier

## Marqueur

Code bar, QR code, empreinte, marquage ou watermark.

Pour une identification physique rapide et sûr il est nécessaire d'apposer sur l'objet indexé un marqueur.

Si l'objet dispose déjà d'un marqueur permettant sont identification unique (même entre objet identique) dans un autre système, il est possible d'utiliser celui-ci, mais cela n'est pas recommandé.

Mais dans certains cas, il n'est pas possible ou nécessaire de le faire :

- aucune modification physique possible (manque de place, surface non compatible, laisser tel quel) : utilisation d'un container si cela est possible (ex. : une pochette plastique transparente)
- original n'est pas conservé (comme les chèques bancaire)

Les données de l'objet devront faire mention de cet état (dans un container, non identifié matériellement, etc.).

Le marqueur prend la forme d'un étiquette auto-collante (stiker), d'une impression (marquage à l'encre) ou de gravage apposant visuellement l'identificateur (identifiant URN).
Il est possible aussi en supplément (les deux sont complémentaires) d'utiliser une puce RFID embarqué (dans une étiquette collé ou intégré dans la matière).

Dans la forme visuelle, l'identifiant doit prendre la forme d'un QR Code (plus de données possible qu'un code 2D).
Il peux contenir aussi un identifiant secondaire (optionnel)

### Marqueur d'ensemble

`1/1` `1/5`

TODO

### Marqueur de sous-ensemble

Un objet peux être constitué d'un ensemble d'objet
Identifie un autre objet de l'ensemble sous ensemble (autres parties feuillet quand plusieurs pages, partie détachable matériel, etc.)

`2/5`

TODO

## Objet

Tous objet palpable est susceptible d'être listé. Mais tous ne peuvent être numérisé de la même façon pour qu'il soit utilisable numériquement de la même façon que physiquement. Par exemple, la numérisation d'un véhicule se résumera surtout à des métadonnées: la fiche technique, les contrats liés, l'historique des trajets effectués.

Parties séparables physiquement dans les conditions normal d'utilisation qui ne donne pas lieu à l'indexation séparé d'objet

Mais tous ne doivent pas être listé. Cela dépend de l'usage de cet objet. Par exemple les consommables comme les timbres postaux ou les feuilles de papier ne nécessite pas vraiment de listing
Pour les les billets de banque, par exemple, si leur enregistrement est nécessaire, cela peut se faire par un autre dispositif que celui décrit ici.

## Metadata

Ces données permettent par la suite à un système numérique et par le biais d'une recherche de trouver les objet connexes : lies, similaire, même type, etc.

Par objet, un jeu de donnée est stocké sous le format RDF (Dublin Core + Custom)

Ces données sont :

- identifiant (URN EPC / UUID)
- (optionnel) identifiant secondaire (simplifié, ex: numéros)
- (optionnel) nom / libellé / label
- type : physique ou numérique
- (si type = physique) état du marqueur : conteneur, absent
- classification : document papier — 2035, machine — perceuse, document numérique — contrat d'assurance, etc. (facture, facturette, lettre administrative)
- état : indexé (actif), désindexé (transformé, détruit, vendu, etc.)
- processus (+ historique) : création, indexation, utilisation, destruction
- date d'indexation
- auteur de l'indexation
- (optionnel) informations sur le stockage physique : localisation, méthode, nature, etc.
- autres objet liés & références : scan (numérisation), notice d'utilisation, facture d'achat, contrat d'assurance, photo (objets "taggé" dessus), etc.
- (si type = collection) sous ensemble (parties séparables physiquement dans les conditions normal d'utilisation)
- (si type = numérique, Dataset) données : textes, multimédia (images, 3D, videos, sons), etc.
- autres métadonnés :
	
	* identifiants et codes bar donnés par un tiers
	* dimension, taille, forme
	* tout autre métadonnés provenant des données

Plus d'informations :

- http://fr.wikipedia.org/wiki/Classification
- https://developers.facebook.com/docs/opengraph/creating-object-types/
- http://en.wikipedia.org/wiki/Document
- http://web.utk.edu/~ledger/docs/transactiontypecodes.pdf
- http://site.ovid.com/site/products/fieldguide/eric/DTC__DOCUMENT_TYPE_CODE.jsp
- http://lhc-proj-qawg.web.cern.ch/lhc-proj-qawg/CD-ROM/Quality/QA202.pdf

### Format RDF

#### Dublin Core

`http://purl.org/dc/dcmitype/PhysicalObject`
 
	<!-- Example: Image -->
	<rdfs:Class rdf:about="http://purl.org/dc/dcmitype/Image">
		<rdfs:label>Image</rdfs:label>
		<rdfs:isDefinedBy rdf:resource="http://purl.org/dc/dcmitype/"/>
		<rdfs:seeAlso rdf:resource="http://dublincore.org/documents/dcmi-type-vocabulary/"/>
		<rdfs:comment>
		An image is a primarily symbolic visual representation other than text.
		For example - images and photographs of physical objects, paintings,
		prints, drawings, other images and graphics, animations and moving
		pictures, film, diagrams, maps, mu
		sical notation. Note that image may
		include both electronic
		and physical representations.
		</rdfs:comment>
		<rdf:type rdf:resource="http://purl.org/dc/dcmitype/DCMIType"/>
	</rdfs:Class>

	<?xml version="1.0"?>
	<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:dcq="http://purl.org/dc/terms/">
		<dcq:Image>
			<dc:creator>Carl</dc:creator>
		</dcq:Image>
	</rdf:RDF>

- https://en.wikipedia.org/wiki/Dublin_Core
- http://www.bnf.fr/documents/oai_dublincore.pdf
- http://radar.oreilly.com/2009/02/oreilly-labs-rdf-for-all-of-ou.html
- http://labs.oreilly.com/opmi.html
- http://code.google.com/p/darwin-sw/wiki/Examples
- http://openweb.eu.org/articles/dublin_core
- http://www.agls.gov.au/documents/agls-document/

### Identifiant

L'identifiant est un URI (URN) contenant soit un EPC (Pure identity), soit UUID ou tout autre URN tant que celui permet une identification unique d'un objet.

Différents exemples :

	urn:epc:id:sgtin:0037000.030241.1041970
	urn:epc:id:sscc:123456.00000010146
	urn:uuid:6e8bc430-9c3a-11d9-9669-0800200c9a66 (UUID)

Cette donnée ne doit pas évoluer dans le temps et rester lié à l'objet.

- [Digital object identifier — Wikipedia](https://en.wikipedia.org/wiki/Digital_object_identifier)
- http://en.wikipedia.org/wiki/Electronic_Product_Code
- http://en.wikipedia.org/wiki/Global_Trade_Item_Number
- http://www.ecis2009.it/papers/ecis2009-0382.pdf
- http://msdn.microsoft.com/en-us/library/bb970583%28v=bts.10%29.aspx
- [Part number — Wikipedia](https://en.wikipedia.org/wiki/Part_number)
- [International Article Number (EAN) — Wikipedia](https://en.wikipedia.org/wiki/International_Article_Number_(EAN))

### Identifiant secondaire

L'identifiant secondaire permet une identification humaine. Elle permet de lire plus facilement, dans une système d'identification privé / interne le code d'identification de l'objet. Elle sera utilisé dans le cas d'un tri à la main d'objet, par exemple.

Peut être confondu avec le nom / libellé / label.

### Données numériques (dataset)

Elles sont la résultant du processus de numérisation permettant de transformer un élément physique avec sa copie numérique (métadonnés).

Pour un document papier, par exemple, ces données proviennent du traitement du scanner et d'un logiciel OCR (searchable PDF) sont sous la forme de fichier :

- sans traitements (TIFF ou ces dérivé — DNG ou TIFF/EP contenant RGB + IR + UV etc.) : RAW
- traité ("hardware processed" — crop, rotation, infrared cleaning, grain reduction, OCR) : PDF, JPEG

Ces donnés, sont la plus part du temps utilisable directement dans un logiciel informatique courant : traitement de texte, d'image, multimédia.

#### Format PDF

Pour les documents, le format PDF est privilégié :

- conteneur de métadonnés (XMP)
- chiffrement
- lecture seul (même si ce n'est pas une méthode sûr)
- embed des données OCR

- http://www.nsa.gov/ia/_files/app/pdf_risks.pdf

#### Métadonnés embarqués

Les documents résultant d'une numérisation peuvent embarquer des métadonnés (copie des informations définissant l'objet digitalisé).

Elles sont sous la forme de (fonction du format) :

- commentaire — `//` ou `/*  */`
- EXIF
- XMP
- [Fork](http://en.wikipedia.org/wiki/Fork_%28file_system%29)
- [Sidecar file](http://en.wikipedia.org/wiki/Sidecar_file) (`.xmp`, `.exf`, `*.`)
	 Dans ce cas, il adviendra d'utiliser un fichier conteneur permettant de grouper les données quelque soit leur format de type [TAR](http://en.wikipedia.org/wiki/Tar_%28file_format%29), 7z ou ZIP en mode Archive (non-solid) (see Open Document Format), de préférence en omettant l'[ACL](https://en.wikipedia.org/wiki/Access_control_list) (pour les formats qui le gère)

Ces métadonnées peuvent être :

- matériel de numérisation utilisé et réglages (DPI, bit-depth, fps, etc.)
- auteur de la numérisation
- date de numérisation
- auteur
- date de création / modification
- preview
- mots clés (définit manuellement ou via OCR)
- ...

Elles peuvent nécessiter d'être mise à jour lors de l'indexation du fichier (si celui existait précédemment).

##

https://en.wikipedia.org/wiki/Digital_preservation

## Stockage

Les donnés, sous forme de fichier peuvent être stocké dans une boite de dépot (FTP, boite email, lecteur réseau, carte CF, Dropbox, etc.).