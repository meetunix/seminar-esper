# Seminar CEP am Beispiel von Esper

## Complex Event Processing Basics (Wikipedia)

* Erkennung, Analyse und Gruppierung voneinender abhängiger Ereignisse
* Sammelbegriff für Methoden, Techniken und Werkzeuge um Ereignisse zu verarbeiten
* Ereignisse werden kontinuirlich und zeitnah bearbeitet
* CEP leitet aus Ereignissen Wissen ab (sog. komplexe Ereignisse)
* CEP erkennt somit Situationen, welche nur durch Kombination mehrerer Ereignisse erkannt werden
* CEP-Systeme müssen Daten aus verschiedenen Quellen und in Echtzeit bearbeiten -> Hohe Last

**Einsatzgebiete**

* Netzwerküberwachung
* öffentliche Sicherheit
* Katastrophenschutz
* Energiemanagement

**Ziel**

* Abstraktionsebene erreichen
* Abhängigkeiten identifizieren:
    * horizontale Abhängigkeit:
        * Events die auf einer Abstraktionsebene aufeinender Einfluss haben, oder abhängen
    * vertikale Abhängigkeit
        * mehrere Events werden zu einer Gruppe zusammengeführt
        * damit Bildung eines übergeordneten Events -> komplexes Event
        * komplexes Event befindet sich eine abstraktionebene über den Einzelereignissen
         

### Unterschiede CEP und ereignisgesteuerte Applikationen

* in EDA wird Ablauf durch sequentielle Folge gesteuert
    
    Event (klick) -> Event (Fenster)

* CEP befasst sich mit Ereignissen/Events die
    * mehrfach redundant 
    * mehrläufig nebeneinander
    * unzuverlässig verkettet auftreten

* Die **Logik** des Auftretens ist unscharf (**Fuzzylogik**)
* Die CEP liefert Ereignisse als Status, überflüssige Ereignisse wurden eliminiert

#### Exkurs Fuzzylogik (wikipedia)
* fuzzy eng für verwischt
* Erweiterung der zweiwertigen Booleschen Logig
    * "ein wenig", "stark", "sehr"
    * ähnlich der mehrwertigen Logik
    * statt [0,1] elem N -> [0,1] elem R

* Eine Fuzzy-Menge wird nicht durch ihre enthaltenen Elemente bestimmt, sondern über
den Grad ihrer Zugehörigkeit dieser Menge.
    * Dafür existiert die Funktion \my: X -> [0,1] \elem R
    * Jedem Element aus X wird ein Zahl aus R zugeordnet (der Zugehörigkeitsgrad) 

* FL ist nützlich wenn keine mathematische Beschreibung des Problems vorliergt


### Events

Was ist ein Event?

* Etwas was passiert oder als passiert angesehen wird
* Ein Ereignis innerhalb eines Systems/ einer Domäne

**Events bei CEP**

* CEP-Ereignisse tretten erst durch das Zusammenwirken mehrerer atomarar Ereignisse auf

* Merkmale von CEP-Ereignissen und atomaren Ereignissen (**Komplexereignis**):
    * Komplexereignisse zeigen keine Wiederholung (?), nur Änderungen des Status
    * Ereignisse können nacheinander oder gleichzeitig eintreten
    * E. können hierarchisch abhängig sein und wiederholt in Verkettungen auftreten
    * Ereignisse können komplett unabhängig sein
    * ein Komplexereignis ist eine Sammlung von Einzelereignissen und definiert einen Status
    * Ereignisse können zusammenhängen, wenn best. Relation erfüllt ist
        * *Fuzzy*-Relation oder Zeitintervall
    *
*Alles was in der realität oder im Rechner passiert kann als Event angesehen werden.

## Complex Event Processing Basics (Gesellschaft für Informatik)

[Lexikon gesellschaft für Informatik: CEP](https://gi.de/informatiklexikon/complex-event-processing-cep/)

### Anwendungsgebiete

**Auslöser (Warum CEP):**

* **SOA** Service Oriented Architecture
* EDA
* kostengünstige Sensortechnik
* überwachung von Informationssystemen

Dadurch stetige Steigerung der Datenmengen -> Bedarf der zeitnahen systematischen verarbeitung
dieser Daten.

**Anwendungsgebiete**

* Business Activity Monitoring
    * Gechäftsprozessüberwachung
    * Chancenerkennung durch Key Performance indikatoren (komplexe Ereignisse)
        * z.B. "Dauer eines Prozesses"

* Sensor Netzwerke
    * kombination von mehreren Sensoren
    * minimierung von Fehlern
        * z.B. Schließen von Rauch/Temperatur auf Brandt

* Marktdaten
    * Auffassung von Aktien und Rohstoffpreisen als Events
    * zeitnahe Analyse zur Trendidentifikation und zur automatischen reaktion
    
### Arten von CEP

1. Komplexe Ereignisse werden als a-priori bekannte Muster über Ströme aus Ereignissen spezifiziert
2. Komplexe Ereignisse sollen über unbekannte Muster in den Strömen erkannt werden

zu **1.** Spezielle **Ereignisanfragesprachen** bieten komfortable Möglichkeiten zur spezifizierung und erkennung

zu **2.** Anwendung von MachineLearning und DataMining auf Ereignisse ()

### Abgrenzungzu anderen Gebieten

* auf erkannte Komplexe Ereignisse soll automatisch reagiert werden
* CEP steht in engem Zusammenhang mit Visualisierung von  ereignisbezogenen Daten


### Ereignisanfragen

Im gegensatz zu DB-Anfragen, werden Ereignisanfragen **kontinuierlich** auf einen endlosen
Ereignisstrom ausgewertet.


#### Aspekte die eine Ereignisanfragesprache beschreiben

* Extraktion von Daten
    * Ereignisse können wichtige Informationen für das weitere Vorgehen/ die Reaktion enthalten
    * Daten können zur Konstruktion von neuen Ereignissen benötigt werden
        * z.B. Verfügbarkeit in XML-Files

* Komposition
    * Zusammensetzen von über die Zeit verteilten Einzelereignissen zu Komplexereignisen
    * oft Datenbezogen (einen ort betreffen, einen Kunden ...)

* Zeitliche Zusammenhänge
    * Ereignisspachen bieten zeitliche Bedingungen
    * Ereignisse müssen in einer gewissen Zeitspanne
    * Ereignisse müssen in einer gewissen Reihenfolge auftreten

* Akkumulation
    * Anfragen auf das Fehlen eines Ereignissen machen bei Ereignisströmen keinen Sinn
    * Solche Anfragen können nur gegen gewisse endliche Ausschnitte (**Fenster**) gestellt werden

**Regeln für Ereignisanfragesprachen**

* deduktive Regeln
    * definieren Ereignisse auf Basis von Ereignisanfragen -> Keine Seiteneffekte
    * Operieren auf Ereignissen

* reaktive Regeln
    * spezifizieren, wie auf komplexe (Ereignisse) reagiert wird



































 
 
