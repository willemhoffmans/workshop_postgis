# Deel 1: Een PostGIS connectie maken
Als het goed is heb je in het vorige deel, naast het installeren van PostgreSQL / PostGIS, ook een ruimtelijke database gemaakt. Zo niet, ga dan terug naar [de introductie](README.md).

In dit deel maken we een verbinding met de database in QGIS. Het voordeel van QGIS is dat je meteen een geweldig goede omgeving hebt om je geodata in beeld te brengen, én je hebt de beschikking over krachtige tools om datasets in de database te importeren en te bevragen. Maar je bent uiteraard vrij om een andere 'voordeur' te kiezen zoals pgAdmin of de commandline. 

## QGIS
Open QGIS en begin in een nieuw (leeg) project.<br>
Kies voor *Layers -> Add Layer > PostgreSQL*, en vervolgens op **New**.

(plaatje)

Zo'n verbinding is als volgt opgebouwd (let op: namen in het
plaatje niet letterlijk overnemen):

* <ins>Name</ins> mag je zelf kiezen.
* <ins>Host</ins> geeft aan op welke server de database te vinden
is. In dit geval (lokaal) is dit *localhost*.
* <ins>Port</ins>: 5432 is de standaardpoort waarover
gecommuniceerd wordt, tenzij je bij installatie van
PostgreSQL een andere standaardpoort hebt
gekozen.
* Bij <ins>Database</ins> geef je de naam van de door jou zelf
gemaakte database op.
* Bij *Authentication > Basic* moet je <ins>User name</ins> en <ins>Password</ins> invullen. Heb je bij de installatie de default gekozen dan is dit *Postgres / Postgres*. Zo niet, dan weet je hopelijk nog wat het wél moet zijn.

Met *Test Connection* kun je checken of er daadwerkelijk een
connectie tot stand kan worden gebracht. Als dat niet het
geval is wordt het troubleshooten: vaak is de naamgeving net
niet goed (denk aan hoofdletters).

Verder is het voor nu ook goed om de laatste twee opties aan
te vinken:

* Also list tables with no geometry. Doe dit vooral: als je een nog maagdelijke database hebt aangemaakt zitten er nog geen geodata in en krijg je niets te zien! 
zijn.
* Use estimated table metadata: dit zorgt ervoor
dat de inhoud van de database sneller wordt gescand bij het inlezen.

Als alles goed is ingevuld en getest, klik *OK*, en vervolgens op *Connect*.
De connectie is nu tot stand gebracht. Je kan nu als het goed is de inhoud van de database zien. Hier doen we echter niks mee: QGIS heeft handigere tools om met een PostGIS database te werken, zoals **DB Manager**. Die gaan we nu gebruiken.

## DB Manager
