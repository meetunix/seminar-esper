# Esper

* java-basierende Software für CEP / ESP (Event Stream Processing)
* Bietet eine deklarative Programmiersprache namens EPL (Event Processing Language)

Beispiel aus Wikipedia:

    select count(*) from OrderEvent.win:time(3 min) having count(*) >= 5

* Stark verbreitet nach *Marktübersich Fraunhofer*

# konspekt zu *Complex Event Processing* - Essentials, Springer, Ralf Bruns 2015


## Einleitung

* Unternehmen und öffentliche Organisatione
    * enorme Menge an Daten muss gehandhabt werden
    * weitere Steigerung der Datenmenge
    * Entscheidungen auf basis von immer mehr Daten müssen getroeffen werden

* Analyse großer Daten bisher auf statischen Datenbeständen
    * **jetzt** kontinuirliche Datenströme mit aktuallsten Daten
    * CEP: Softwaretechniologie zur systematischen Analyse von massiven Daten**strömen**



# Kapitel 1 Motivation

* wachsende Datenmengen von
    * Smartphones
    * Sensornetzen
    * Produktionsmaschinen
    * IoT-Devices
    * RFID-Tags
    * Finanzmärkte
    * soziale Netzwerke

* Auswertung von BigData ist zentrale Fragestellung für Unternehmen / öfftl. Organ.
    * Wettbewerbsvorteil
    * Vorhersage (Kundenverhalten, Finanzprodukte ..)
    * Vorhersage (Erdbeben, Stau ..)
    * soll automatisiert verlaufen
    * soll zusammenhänge erkennen
    
**Datenströme**

* beinhalten **LIVE-Daten**: Jeder Datensatz bezieht sich auf gerade stattgefundenes Ereignis
    * Reihenfolge spielt eine Rolle
    * Auftrittzeiten spielt Rolle

* Daten sind häufig *feingranular* / atomar (Mein Begriff)
    * geringe komplexität, lassen sich einfach beschreiben
    * z.B. Temp. eines Sensors, Preis einer Aktie

* Ströme *feingranularer* Daten sind hochfrequent / massiv

* Ströme sind unbegrenzt

* Ströme sind volatil
    * nicht alle Ereignisse können gespeichert werden

* Datensätze stehen zueinander in einer impliziten Beziehung
    * z.B. zwei benachbarte Sensoren
    * Daten eines bestimmten Kunden
    
Massive Datenströme müssen in Echtzeit verarbeitet werden:

* Finanzmärkte algorithmic trading und froud detection
    * innerhalb von sekundenbruchteilen muss entschieden werden:
        * verkau/kauf
        * Betrug

* Sensornetze: Bindeglied zwischen physikalischer und rechnergestützer Welt
    * z.B. Warenflüsse -> RFID Chips


**Ereignisse**

* Jeder Datensatz neues Ereignis
    * z.B. Jede Kursänderung einer Aktie

Betrachtung eines einzelnen Ereignis reicht nicht aus um Schlüsse zu ziehen
-> Daten müssen **korreliert** werden -> Erst die Betrachtung über einen längeren Zeitraum lässt Schlüsse zu.

* [gutes Beispiel Solarmodul]

* Informationsgehalt eines Ereignisstromes ergibt sich erst aus dem Erkennen von
    * Zusammenhängen
    * Abhängigkeiten
    * Korrelationen
 zwischen mehreren Ereignissen

* Die beziehung zwischen Zusammenhängenden E. bilden spezifisches Muster (**event pattern**)
    * Ziel ist es diese Muster zu erkennen (**patern matching**)

* [schöne grafik]

* Ein erkanntes Muster wird durch ein komplexex Ereignis (**high level event**) repräsentiert.
    * Es existiert somit immer ein kausaler Zusammenhang zwischen Ereignismuster und Komplexem Ereignis

**Grundzyklus Ereignisgesteuerter Systeme**

,,The real world is mostly event driven“
(R. Schulte, Gartner Inc., Vortrag ,,Event Processing in Business Applications“, 15. März 2006.)

Reagieren - Erkennen
   \            /
    \          /
    Verarbeiten 

1. Erkennen (**sense**)

* Asugangspunkt
* Erkennen von Informationen/Sachverhalten -> Ereignisse
* unmittelbare Ereknnung (Keine Zeitverzögerung)

2. Verarbeiten (**process** bzw, **analyze**)

* Analyse der Erkannten Ereignisse
* korrelation, aggregation,abstraktion,klassifizierung, Verwerfung von Ereignissen
* Mustersuche
    * in Ereignisströmen
    * zwischen verschiedenen Ereignisströmen

3. Reagieren (**respond**)

* Wenn Muster erkannt -> zeitnahe Reaktionen
    * Warnmeldung
    * initiierung von Aktionen ...
    * Auch die Generierung von neuen komplexen Ereignissen in einer weiteren Abstraktionsebene ist möglich

**Architektur ereignisgesteuerter Systeme**

# Kapitel 2 CEP im Überblick

## 2.1 Charakterisieren von Ereignissen

"Ein Ereignis kann alles sein, was passiert oder von dem erwartet wird, dass es passiert [18]: eine Aktivität,
ein Vorgang, eine Entscheidung etc. Im Allgemeinen bezieht sich ein Ereignis auf die Veränderung eines Zustands,
also typischerweise auf die Änderung des Wertes einer Eigenschaft eines realen oder virtuellen Objekts."

* Ereignisse müssen relevante Daten für die weiterverarbeitung als Ereignisdaten mit führen
    * Ereignisdaten beschreiben den Kontext, indem das E. auftrat

* **Ereignisdaten** bestehen aus
    * Metadaten
        * eindeutige ID
        * Zeitstempel
        * (Ereignisquelle)
        * (Ereignistyp)
    * Kontextdaten
        * Nutzdaten (z.B. Luftfeuchtigkeit)

## 2.2 Grundbegriffe CEP

Complex Event Processing ist eine Softwaretechnologie für die dynamische Analyse von massivenDaten- bzw.
Ereignisströmen in Echtzeit. Mit CEP ist es möglich, kausale, temporale, räumliche und andere Beziehungen
zwischen Ereignissen auszudrücken. Diese Beziehungen spezifizieren Muster, nach denen die Ereignismenge durchsucht
wird (event pattern matching) [17].

**Ereignismuster**

* zur Erkennung muss Ereignisstrom nach Ereignismustern durchsucht werden
    * betrachtung über einen gewissen Zeitraum

* Je nach Art der Operatoren unterscheidet man drei Arten der  Mustererkennung:

* Erkennung einfacher Muster
    * Es werden Einzelereignisse erkannt
    * Es werden boolesche Kombinationen von Ereignissen erkannt
        * A && B !C

* Erkennung komplexer Ereignismuster
    * Definition von weiteren Operatoren
        * Reihenfolge von Ereignissen
        * Zeitfenster in dem E auftreten

* Abstraktion von Ereignismustern
    * Asbtraktion zu komplexen Ereignissen
        * Bilden von Summen / Durchschnittswerten

**Ereignisverarbeitung mit Regeln**

**Ereignisregel:**
Eine Ereignisregel (event processing rule) beschreibt eine spezifische Reaktion, die bei Erkennen
eines Musters erfolgen soll. Jede Regel setzt sich aus einem Bedingungs- und einem Aktionsteil
zusammen:

* Bedingungsteil:
    * besteht aus verknüpften Mustern -> abgleich mit Ereignisstrom -> Muster matched ->
*Aktionsteil
    * legt Reaktion fest, welche ausgeführt wird
        * neues Ereignis, Meldung ..

* Formulierung erfolgt in speziellen Regelsprachen
    * EPLs (Event Processing Languages)
    * deklarative Beschreibung möglich
        * keine implementierung des Algorithmus zur Suche der Muster notwendig
        * stattdessen Modellierung

* Es existiert kein Standard für EPLs

## 2.3 Event Processing Agents

Ein Event Processing Agent ist ein Softwaremodul, das komplexe Ereignisse verarbeiten und
Ereignismuster in einem Strom von Ereignissen erkennen kann [18].

-> Nette Grafik

## 2.4 Event Driven Architecture

Event-Driven Architecture ist ein Architekturstil, in dem einige Komponenten
ereignisgesteuert sind und die Interaktion durch den Austausch von Ereignissen erfolgt [18].

--> nette Grafik (Gut für die Einoordnung von CEP in das Thema EDA)


# Kapitel 3 - Sprachkonzepte und Ereignisverarbeitung

**Ereignisalgebren:**

1. Ereignisbasierte Muster

2. Kontextbedingung

3. Sliding Window

4. Aggregationsfunktion

5. 

(Ich glaube, das brauch ich nicht mehr, da ich ja direkt aus ESPER eingehe)




