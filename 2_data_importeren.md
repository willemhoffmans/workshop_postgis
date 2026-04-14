Data importeren via DB Manager
Voor deze oefening heb je de plugin DB Manager in QGIS (menu Database) nodig. Als je die niet kan vinden,
kijk dan bij Plugins / Manage and install plugins of die aan staat (DB manager is een core plugin, dus hij is er
altijd). Zo niet, vink hem aan.
Tot nog toe hebben we in QGIS alleen maar gekeken naar hoe we bij de PostGIS database kunnen komen,
maar we hebben nog niets met data gedaan. We kunnen ook ‘gewone’ GIS data importeren, bijvoorbeeld
een shapefile of een geopackage. In dit geval gaan we de dataset res_regios_2023.gpkg importeren: deze
bevat de regiogrenzen van de Regionale Energie Strategie (RES). Via de QGIS DB Manager gaat dat vrij
eenvoudig:
 Gebruik de Importeer knop (zie screenshot hieronder, rood omkaderd) of kies de menu optie Tabel
– Laag / bestand importeren (deze optie wordt zichtbaar in de DB Manager na openen van een
PostGIS connectie).
Het volgende venster verschijnt:
In het bijbehorende dialoogscherm invullen:
• Invoerbestand: res_regios_2023
• Schema waarin de tabel moet komen selecteren ( public voor nu)
• Tabelnaam. Deze wordt automatisch ingevuld met de geopackagenaam, maar je mag uiteraard een
andere invoeren. Denk er aan: alleen kleine letters, cijfers en onderstreepje!
• Primaire sleutel: vul hier een nieuw te maken veld in. 'gid' is een goede optie, dan weet je vrijwel
zeker dat je geen gedoe krijgt met bestaande kolommen die al zo heten. Dit veld wordt automatisch
gevuld met unieke getallen.
• Naam voor de geometriekolom, gebruik standaard 'geom'.
• Bron- en doel SRID: vul hier 28992 (Rijksdriehoekstelsel) in.
• Veldnamen naar kleine letters converteren: zeker doen!
• Ruimtelijke index aanmaken: doen! Later meer daarover.En nu maar eens kijken of de import lukt. Zo ja, bekijk in de DB Manager de tabel en de voorvertoning, en
controleer of dit er inderdaad goed uitziet. Bekijk vervolgens de metadata van de nieuwe tabel (tabblad
info). Beantwoord de volgende vragen:
 Welke verschillende datatypen komen in de tabel voor?
 Wat voor type geometrie zit erin?
 Heeft de tabel een ruimtelijke index?
 Hoeveel RES regio’s bevat het bestand eigenlijk?
Sleep het bestand vervolgens vanuit de DB Manager direct het QGIS scherm in. Je kan er nu gewoon mee
GISsen zoals je gewend bent!
DB Manager: handig!(?)
Zoals is uitgelegd zijn er meerder ‘voordeuren’ om de PostgreSQL / PostGIS database te benaderen en te
gebruiken. We hebben er nu twee gezien: pgAdmin en DB Manager. Het grote voordeel van DB Manager is
dat je, gekoppeld aan QGIS, ook direct in beeld (de kaart) kan zien wat een bevraging op de database heeft
opgeleverd. Dit in tegenstelling tot bijvoorbeeld pgAdmin.
Gedurende het vervolg van de cursus gaan we heel veel met geodata doen, het ligt dan ook voor de hand
om voor de opdrachten DB Manager te gebruiken. Maar… je bent hier in principe vrij in!
En we zullen vast wel gaan zien dat DB Manager ook z’n beperkingen heeft.
