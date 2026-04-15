# DEEL 4: Gevorderd SQL

## Inleiding
In het vorige deel hebben we één tabel bevraagd, en met relatief eenvoudige queries. In dit deel brengen we wat verdieping aan:

* een query op meerdere tabellen tegelijk, op basis van geometrische vergelijkingen,
* een stukje beheer: van een query-resultaat een view (virtuele tabel) maken,
* GIS analyse: buffer (maar dan in SQL)

Net als in Deel 3 houden we het relatief eenvoudig. Voor de snelle leerlingen: wees creatief, denk buiten de lijntjes en geef er je eigen draai aan. Aan het eind staan nog wat ideeën voor wat je nog meer zou kunnen analyseren.

## Koppeling van twee tabellen

Een voorbeeld:
```
SELECT puntentabel.gid, puntentabel.ash, puntentabel.geom, vlakkentabel.naam 
FROM puntentabel, vlakkentabel
WHERE ST_Within(puntentabel.geom, vlakkentabel.geom)
AND vlakkentabel.naam = 'Vught';
```
Wat zien we hier? 

* We beginnen bij `FROM`. Hier zien we twee tabellen, gescheiden door een komma. Dit is een kort-door-de-bocht manier om in een bevraging twee tabellen aan elkaar te koppelen.
* In de `WHERE` voorwaarde zien we hoe de punten en de vlakken worden gekoppeld. Met `ST_Within` geef je aan dat de geometrie van het punt in de geometrie van het vlak moet liggen.
* Er is echter nog een tweede `WHERE` voorwaarde waaraan we moeten voldoen, die staat in de `AND`regel. Namelijk dat de vlakkentabel wordt beperkt tot alleen het vlak met de naam 'Vught'.
* Ofwel: de vlakken met een andere naam worden niet geselecteerd. En dat betekent dan meteen ook dat de punten die *niet* in  het vlak 'Vught' liggen niet meekomen.
* In de `SELECT` regel laten we een paar kolommen uit de puntentabel (én de geometrie) meekomen, en de naam uit de vlakkentabel.

**N.B.** Omdat we met meer dan één tabel werken moeten we bij het opvragen van kolommen steeds ook aangeven uit welke tabel de opgevraagde kolom komt. Dat doen we door `tabelnaam.kolomnaam` in de query op te geven. Dit moet in *alle* regels in de query, dus in dit geval zowel bij `SELECT` als bij `WHERE`.   



7. Koppeling: windturbines in jouw favoriete gemeente.
8. dat in QGIS laden.
9. totale kw in jouw gemeente
10. totale kw per gemeente (GROUP BY)
11. welke gemeente heeft de meeste kw?
12. 10 met geom, maak er een view van.
13. buffer windturbines
14. extra vragen 
