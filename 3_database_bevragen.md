# Deel 3: Basis SQL

## Inleiding
Uitleggen wat we hierin gaan doen. 
Vanwege de korte workshop gaan we wat kort door de bocht.
Meer ervaring? Doe het dan volgens je eigen (vast betere!) regels. 
En verzin zelf uitdagendere vragen.

## Opdrachten
1. Selecteer de hele gemeenten tabel
2. Selecteer jouw favoriete gemeente (WHERE)
3. Laad dat in QGIS in met "add as layer"
4. Alleen statnaam en statcode

## SQL syntax voor selecties
Eenvoudige SQL expresies in PostgreSQL (en PostGIS) gaan volgens een vast stramien. Hier een overzicht:

5
SELECT
verplicht
Kolom(men) die je wil selecteren. Met “*” selecteer je alles.
1
FROM
verplicht
Tabel(len) waaruit je wil selecteren
2
WHERE 
optioneel
Voorwaarde waaraan de selectie moet voldoen
3
GROUP BY 
optioneel
Samenvoegen (aggregeren) resultaten op 1 of meer kolommen
6
ORDER BY 
optioneel
Sorteren van de resultaten op 1 of meer kolommen

Belangrijk is de volgorde van de regels: die moet zijn zoals hier getoond. Echter: het is handig om bij het ontwerpen van een query de volgorde te hanteren zoals in de eerste kolom van dit overzicht. Dit is ook de volgorde die de database engine hanteert bij het uitvoeren.  
1. Begin dus bij FROM. Uit welke tabel wil je selecteren?
2. Daarna WHERE. Is er een voorwaarde?
3. GROUP BY. Moeten resultaten worden samengevoegd?
5. SELECT. Pas nu gaan we de kolommen selecteren! 
6. ORDER BY. Sorteren van de resultaten. ASC (oplopend) of DESC (aflopend).
