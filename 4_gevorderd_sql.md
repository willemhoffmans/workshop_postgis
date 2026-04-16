# DEEL 4: Gevorderd SQL

## Inleiding
In het vorige deel hebben we één tabel bevraagd, en met relatief eenvoudige queries. In dit deel brengen we wat verdieping aan:

* een query op meerdere tabellen tegelijk, op basis van geometrische vergelijkingen,
* een stukje beheer: van een query-resultaat een view (virtuele tabel) maken,
* GIS analyse: buffer (maar dan in SQL)

Net als in Deel 3 houden we het relatief eenvoudig. Voor de snelle leerlingen: wees creatief, denk buiten de lijntjes en geef er je eigen draai aan. Aan het eind staan nog wat ideeën voor wat je nog meer zou kunnen analyseren.

## Koppeling van twee tabellen

Een voorbeeld: analyse van bomen (puntlocaties) en gebieden (vlakken).
```
SELECT bomen.gid, bomen.soort, bomen.geom, gebieden.naam 
FROM bomen, gebieden
WHERE ST_Within(bomen.geom, gebieden.geom)
AND gebieden.naam = 'Drunense Duinen';
```
Wat zien we hier? 

* We beginnen bij `FROM`. Hier zien we twee tabellen, gescheiden door een komma. Dit is een kort-door-de-bocht manier om in een bevraging twee tabellen aan elkaar te koppelen.
* In de `WHERE` voorwaarde zien we *hoe* de bomen en de gebieden worden gekoppeld. Met `ST_Within` geef je aan dat de geometrie van de boom in de geometrie van het gebied moet liggen.
* Er is echter nog een tweede `WHERE` voorwaarde waaraan we moeten voldoen, die staat in de `AND` regel. Namelijk dat de gebieden worden ingeperkt tot alleen het gebied met de naam 'Drunense Duinen'.
* Ofwel: de andere gebieden worden niet geselecteerd. En dat betekent dan meteen ook dat de bomen die *niet* in het gebied 'Drunense Duinen' liggen niet meekomen.
* In de `SELECT` regel laten we een paar kolommen uit de bomen tabel (én de geometrie) meekomen, en de naam uit de gebieden tabel.

**N.B.** Omdat we met meer dan één tabel werken moeten we bij het opvragen van kolommen steeds ook aangeven uit welke tabel de opgevraagde kolom komt. Dat doen we door `tabelnaam.kolomnaam` in de query op te geven. Dit moet in *alle* regels in de query, dus in dit geval zowel bij `SELECT` als bij `WHERE`.   

## Oefeningen

1. Koppel op (ongeveer) de manier van bovenstaand voorbeeld de windturbines aan jouw favoriete gemeente. Zorg ervoor dat je dus alléén de turbines in die gemeente terugkrijgt, en doe de naam van de gemeente er als kolom bij.
2. Laad het resultaat in QGIS, om te checken of het er goed uitziet. Hoeveel windturbines liggen er in jouw gemeente?.
3. Bereken het totale vermogen (kw) aan windenergie dat in jouw gemeente wordt opgewekt. Iets met `SUM`, hoe zat dat ook alweer?
4. Bereken van álle gemeenten het totale vermogen. Als basis kun je best wel je vorige query gebruiken, maar de beperking tot één gemeente in de `WHERE` voorwaarde moet hier natuurlijk uit. En we moeten gaan aggregeren (`GROUP BY`). Check eventueel het syntax overzicht in [Deel 3](3_database_bevragen.md).
5. Welke gemeente heeft het grootste vermogen aan windenergie? Sorteer je tabel dusdanig dat die gemeente bovenaan komt te staan (`ORDER BY`). Nog beter: als je aan het eind van je query `LIMIT 1` toevoegt krijg je alléén die gemeente terug. 
6. Laad het resultaat van (4) in QGIS. Vergeet uiteraard niet om ook de geometrie mee te selecteren.
7. Maak van het resultaat van (4) een view, door aan het begin van de dit toe te voegen: `CREATE VIEW windenergie_per_gemeente AS <plak hier je query van oefening 4>`, en laad de view (virtuele tabel) in QGIS. 
8. Maak er een *tabel* van! In plaats van `CREATE VIEW windenergie_per_gemeente` krijg je `CREATE TABLE windenergie2`. Als dit lukt zul je zien dat er wat rare dingen mee zijn: welke? Probeer ze op te lossen of vraag de docent!
9. Opmaat GIS analyse: maak buffers rondom de windturbines. Dit kan, net zoals in 'gewoon' GIS. Selecteer uit de windturbines tabel in plaats van gewoon de geometrie zelf: `ST_Buffer(geom, 1000)`. En laad dát in QGIS!

## Extra vragen (voor de diehards!)
10. Totaal vermogen in kilowatt (oefening 4) geeft wel hele hoge getallen, kun je er geen megawatt of gigawatt van maken?
11. Het is wel netjes om bij de rangschikking van gemeenten met het hoogste vermogen rekening te houden met de oppervlakte (`ST_Area(geom)`) van de gemeenten, zodat je een zuiverdere analyse krijgt: bijvoorbeeld kilowatt per km<sup>2</sup>. Welke gemeente scoort dan het hoogst?
12. Voor het berekenen van hinder (b.v. woningen te dichtbij windturbines) kun je uiteraard buffers gebruiken, maar de grootte daarvan moet wel afhangen van de tiphoogte: **bufferafstand = 2 tiphoogte**, ofwel: **bufferafstand = 2 ashoogte + diameter**. Buffer de windturbines niet met 1000 meter zoals in oefening 9, maar met de juiste, variabele afstand.
