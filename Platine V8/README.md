# Platine V8

von Michi (kepppfeff-ZOE)

<pre>
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!! OHNE GEWÄHR, ALLES AUF EIGENE GEFAHR, NUR ZU TESTZWECKEN !!!!
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
</pre>

## Benötigte Bauteile

Zusätzlich zu den unter https://github.com/eokgnah/ZOE-Display aufgelisteten Hauptkomponenten und dem 3D-Druck werden folgende Bauteile benötigt (diese sind alle bei der Sammelbestellung enthalten):

#### Module & Halbleiter
- U2: Spannungsregler LC78_05-0.5 oder vergleichbar (Ausgang 5 V, 500 mA) bzw. bei Anschluss einer USB-Buchse Spannungsregler OKI-78SR-5/1.5-W36-C oder vergleichbar (Ausgang 5 V, 1500 mA)
- U3: Spannungsregler LC78_03-0.5 oder vergleichbar (Ausgang 3,3 V, 500 mA), stattdessen kann auch der interne Spannungsregler des ESP32 verwendet werden
- Q1: P-Kanal-MOSFET IRFU9024N
- IC4: CAN-Transceiver MCP2562 (DIP8)
- D3, D4: Schottky-Dioden 1N5817
- T1: NPN-Transistor BC547C (nur bei Verwendung des kapazitiven Displays)
- T4: PNP-Transistor BC327-25
- T5, T6: NPN-Transistoren BC547C

#### Passive Bauelemente
- R1: Widerstand 100 kΩ ± 50 % (nur bei Verwendung des kapazitiven Displays)
- R3: Widerstand 1,5 kΩ ± 5 % (nur bei Verwendung des resistiven Displays mit eingebautem Transistor) bzw. Widerstand 5,1 Ω ± 5 % (nur bei Verwendung des resistiven Displays ohne eingebauten Transistor)
- R4: Widerstand 15 kΩ ± 5 % (nur bei Verwendung des kapazitiven Displays der alten Version)
- R5: Widerstand 120 Ω ± 10 %
- R6: Widerstand 15 kΩ ± 5 %
- R7: Widerstand 15 kΩ ± 5 % (nur bei Verwendung des kapazitiven Displays der alten Version)
- R8: Widerstand 100 kΩ ± 5 %
- R9: Widerstand 470 kΩ ± 10 %
- R10, R11: Widerstände 1,2 MΩ ± 5 %
- R12: Widerstand 470 kΩ ± 5 %
- R13: Widerstand 47 kΩ ± 5 %
- C1: Elektrolyt-Kondensator 10 μF, min. 10 V
- C2, C3, C4: Keramik-Kondensatoren 100 nF
- C5: Elektrolyt-Kondensator 10 μF, min. 25 V
- C6: Elektrolyt-Kondensator 22 μF, min. 6,3 V

#### Steckverbinder & Elektromechanik
- OBD-Stecker
- Piezo-Summer, mit Kabeln oder für Printmontage (RM 7,6 mm)
- IC-Sockel DIP8 (für MCP2562)
- USB-Buchse (optional)
- Schraubklemmblock 3-polig (RM 5 mm) für Stromversorgung (12 V Eingang, 5 V Ausgang)
- Schraubklemmblock 2-polig (RM 5 mm) für CAN-Bus
- Kabel zum Anschluss von OBD-Stecker und ggf. USB-Buchse
- Stiftleisten (für GPS-Modul, resistives Display und ggf. als Abstandshalter)

## Benötigtes Werkzeug und Verbrauchsmaterial
Zum Zusammenbau der Elektronik benötigt ihr folgendes:
- Lötkolben
- Lot
- Seitenschneider bzw. Vornschneider
- Spitzzange
- Abisolierzange
- Schlitz-Schraubendreher

## Hinweise zum resistiven Touchscreen

Bei Verwendung des Displays mit resistivem Touchscreen werden die Widerstände R1, R4 und R7 sowie der Transistor T1 nicht benötigt.

Falls ihr das Display mit resistivem Touchscreen verwendet, solltet ihr zunächst prüfen, ob dieses einen eingebauten Transistor für die LED-Hintergrundbeleuchtung eingebaut hat oder nicht. Nur wenn ein Transistor eingebaut ist, könnt ihr die Helligkeit des Displays steuern.
Von der Versionsbezeichnung des Displays hängt dies scheinbar nicht ab; ich habe schon Bilder von V1.1 und V1.2 jeweils sowohl mit und ohne Transistor gesehen! Ihr müsst also tatsächlich den Transistor auf der Display-Platine suchen. Es handelt sich um ein kleines schwarzes Bauteil mit drei Pins, welches auf der Platine mit **Q1** beschriftet sein muss (es gibt ein gleich aussehendes Bauteil, welches mit U1 beschriftet ist, das ist aber kein Transistor, sondern ein Spannungsregler). 
- Falls euer Display *zwei* kleine schwarze Bauteile mit je drei Pins hat, von denen eines mit U1 und eines mit Q1 beschriftet ist, dann habt ihr ein Display *mit* eingebautem Transistor. **In diesem Fall muss für R3 ein 1,5-kΩ-Widerstand eingesetzt werden. Außerdem sollte die Lötbrücke SJ5 gesetzt werden, damit die Display-Helligkeit vom ESP32 gesteuert werden kann.**
- Falls euer Display nur *ein* kleines schwarzes Bauteil mit drei Pins hat, welches auf der Platine mit U1 beschriftet ist, dann hat das Display *keinen* Transistor eingebaut. **In diesem Fall muss für R3 ein 5,1-Ω-Widerstand eingesetzt werden (anders als auf dem Bestückungsdruck angegeben!). Die Lötbrücke SJ5 muss offen bleiben, da sonst der ESP32 Schaden nehmen kann!**

Das resistive Display besitzt eine Lötbrücke (J1), die ggf. gesetzt werden muss. Hierzu bitte den Abschnitt „Hinweise zu den Lötbrücken zur Auswahl der Stromversorgung“ beachten.

## Hinweise zum kapazitiven Touchscreen

Bei Verwendung des Displays mit kapazitivem Touchscreen wird der Widerstand R3 nicht benötigt.

Falls ihr das Display mit kapazitivem Touchscreen verwendet, solltet ihr zunächst prüfen, ob ihr die alte oder die neue Version des Displays besitzt. Kleine Anmerkung am Rande: Auf den beiden folgenden Fotos wurde jeweils rechts die 6-polige ISP-Buchse abgelötet, dies ist jedoch bei der Platine V8 nicht erforderlich!

### Alte Version
![Alte Version](/Platine%20V8/Bilder/Kapazitiv-alt.jpg)
Hier müsst ihr lediglich die Lötbrücke „backlight #5“ setzen, wie im Foto zu sehen, damit die LED-Hintergrundbeleuchtung gedimmt werden kann. Die Lötbrücken „13“, „12“ und „11“ sind bei dieser Version bereits standardmäßig (über feine Leiterbahnen) gesetzt.

**Bei der Bestückung der Platine sind die beiden 15-kΩ-Widerstände R4 und R7 zwingend erforderlich, da ohne diese der ESP32 eine zu hohe Spannung vom Display abbekommt.**

### Neue Version
![Neue Version](/Platine%20V8/Bilder/Kapazitiv-neu.jpg)
Wie man sieht, gibt es hier die zusätzliche Lötbrücke IOREF. Diese müsst ihr (anders als im Foto!) auf 3,3 V setzen, also das mittlere und das linke (mit „3V“ beschriftete) Pad mit einem Tropfen Lot verbinden. 

**Bei der Bestückung der Platine sollten dann die beiden 15-kΩ-Widerstände R4 und R7 weggelassen werden.**

Außerdem müsst ihr die Lötbrücken „backlight #5“, „13“, „12“ und „11“ setzen (wie im Foto zu sehen).

## Hinweise zu den Lötbrücken zur Auswahl der Stromversorgung

Der 3,3-V-Spannungsregler **U3** (LC78_03-0.5 oder ähnlich) ist nicht unbedingt erforderlich, da alternativ auch der interne (lineare) Spannungsregler des ESP32 verwendet werden kann. Zur Auswahl zwischen diesen beiden Varianten dienen die Lötbrücken SJ2, SJ3 und SJ4.

### Falls die Platine mit Spannungsregler U3 bestückt wird, ...

... werden ESP32, GPS-Modul und resistives Display vom Spannungsregler U3 mit 3,3 V versorgt. 

**Hierzu muss die Lötbrücke SJ4 gesetzt werden. Bei Verwendung des resistiven Displays muss zusätzlich dessen Lötbrücke J1 gesetzt werden.**

Wenn die Platine nur über den USB-Port des ESP32 betrieben wird (z.B. zum Flashen), ist das kapazitive Display bei dieser Schaltungsvariante nicht in Betrieb! Wer dies ändern möchte, kann zusätzlich die Lötbrücke SJ2 setzen, allerdings wird dadurch bei Versorgung über den OBD-Port die Spannungswandlung ineffizienter, da der interne Spannungsregler des ESP32 ständig „mitläuft“.

### Falls der Spannungsregler U3 weggelassen wird, ...

... werden ESP32, GPS-Modul und resistives Display vom Spannungsregler U2 mit 5 V versorgt. Alle drei nutzen dann ihre internen linearen Spannungsregler, um die Spannungsdifferenz zu verbraten. 

**Hierzu müssen die Lötbrücken SJ2 und SJ3 gesetzt werden. Bei Verwendung des resistiven Displays muss dessen Lötbrücke J1 offen bleiben.**

## Platine löten
### Schritt 1: Lötbrücken setzen

Als erstes solltet ihr alle benötigten Lötbrücken setzen. 

- SJ1 bestimmt über die Ausrichtung des Bildschirms. Bei Verwendung des 3D-gedruckten ZOE-Einlegers sollte diese Lötbrücke für das resistive Display normalerweise auf die Seite mit dem „S“ und für das kapazitive Display auf die Seite mit der „1“ gesetzt werden. An diese Lötbrücke kommt man auch später noch ganz gut dran, sodass es kein Problem ist, wenn sie falsch gesetzt wurde.
- Wie ihr SJ2, SJ3 und SJ4 setzen müsst, findet ihr unter „Hinweise zu den Lötbrücken zur Auswahl der Stromversorgung“.
- SJ5 sollte nur bei Verwendung eines resistiven Displays mit eingebautem Transistor gesetzt werden.

### Schritt 2: Widerstände und Dioden

Als nächstes kommen die flachen Bauteile dran. Bei Widerständen ist die Polarität egal, bei den Dioden ist der Strich, welcher den Minuspol kennzeichnet, auf dem Bestückungsdruck eingezeichnet. 

Bitte beachtet: Je nachdem, welche Display-Version ihr verwendet, müssen die Widerstände R1, R3, R4 und R7 gegebenenfalls nicht oder abweichend bestückt werden.

### Schritt 3: IC-Sockel

### Schritt 4: Keramik-Kondensatoren

### Schritt 5: Piezo-Summer

### Schritt 6: Stiftleiste für GPS-Modul

### Schritt 7: Transistoren

### Schritt 8: Schraubklemmblöcke

### Schritt 9: ESP32

### Schritt 10: 3,3-V-Spannungsregler

### Schritt 11: Elektrolyt-Kondensatoren

### Schritt 12: 5-V-Spannungsregler

### Schritt 13: Display

Bevor ihr Display und Platine zusammenfügt, kontrolliert nochmal, ob alle Lötstellen gut aussehen und ob ihr am Display alle erforderlichen Lötbrücken gesetzt habt, denn ihr kommt anschließend nicht mehr dran!

### Schritt 14: GPS-Modul

### Schritt 15: IC einsetzen

## USB-Buchse

![USB-Buchse](/Platine%20V8/Bilder/20190320_204215.jpg)

## OBD-Stecker
