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
- U3: Spannungsregler LC78_03-0.5 oder LMO78_03-0.5 oder vergleichbar (Ausgang 3,3 V, 500 mA), stattdessen kann auch der interne Spannungsregler des ESP32 verwendet werden
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

## Grundlegendes Vorgehen

Wer bereits Platinen bestückt hat, kann diesen Abschnitt gerne überspringen ;-)

Zum Zusammenbau der Elektronik benötigt ihr Folgendes:
- Lötkolben und Lötzinn, Lötspitzen-Reinigungstool (feuchter Schwamm, Spiralwolle etc.)
- Seitenschneider bzw. Vornschneider
- Spitzzange
- Abisolierzange
- Schlitz-Schraubendreher
- Heißklebepistole und -sticks
- Eventuell (falls ihr etwas falsch verlötet habt): Entlötsaugpumpe, Entlötlitze etc.

Bei dieser Platine werden alle Bauteile in Durchsteckmontage (Printmontage) bestückt. Die grundlegende Vorgehensweise, um ein Bauteil einzulöten, ist Folgende:

1. Anschlussdrähte des Bauteils zurechtbiegen (falls nötig).
2. Bauteil von der Seite der Platine, auf der der Bestückungsdruck für das Bauteil angebracht ist, durch die entsprechenden Kontaktlöcher stecken.
3. Platine umdrehen und die herausragenden Drähte (bzw. Metallstifte) nacheinander mit den Leiterbahnen verlöten. Zum Löten sollte man in der Regel zuerst den Lötkolben an die beiden zu verlötenden Metallteile halten (hier Draht und Leiterplattenkontakt), sodass die Lötspitze *beide* Teile erhitzt. Direkt anschließend gibt man das Lötzinn hinzu, welches sich nun kegelförmig (nicht kugelförmig :D) um den Draht verteilen sollte. 
4. Erst jetzt überstehende Drähte abschneiden (falls vorhanden).

Hierbei kann man entweder alle Bauteile einzeln nacheinander durchstecken und verlöten oder auch mehrere auf einmal. Damit die Bauteile während des Lötens nicht nach unten aus der Platine herausrutschen können, macht es Sinn, mit den flachsten Bauteilen anzufangen und sich nach und nach zu den höchsten Bauteilen vorzuarbeiten. Im Idealfall liegt die Platine dann immer auf dem Bauteil auf, welches als Nächstes angelötet werden soll. 

## Hinweise zum resistiven Touchscreen

Bei Verwendung des Displays mit resistivem Touchscreen werden die Widerstände R1, R4 und R7 sowie der Transistor T1 nicht benötigt.

Falls ihr das Display mit resistivem Touchscreen verwendet, solltet ihr zunächst prüfen, ob dieses einen eingebauten Transistor für die LED-Hintergrundbeleuchtung eingebaut hat oder nicht. Nur wenn ein Transistor eingebaut ist, könnt ihr die Helligkeit des Displays steuern.
Von der Versionsbezeichnung des Displays hängt dies scheinbar nicht ab; ich habe schon Bilder von V1.1 und V1.2 jeweils sowohl mit und ohne Transistor gesehen! Ihr müsst also tatsächlich den Transistor auf der Display-Platine suchen. Es handelt sich um ein kleines schwarzes Bauteil mit drei Pins, welches auf der Platine mit **Q1** beschriftet sein muss (es gibt eventuell ein gleich aussehendes Bauteil, welches anders beschriftet ist, das ist aber kein Transistor, sondern ein Spannungsregler). 
- Falls euer Display *zwei* kleine schwarze Bauteile mit je drei Pins hat, von denen eines mit U1 und eines mit Q1 beschriftet ist, dann habt ihr ein Display *mit* eingebautem Transistor. **In diesem Fall muss für R3 ein 1,5-kΩ-Widerstand eingesetzt werden. Außerdem sollte die Lötbrücke SJ5 gesetzt werden, damit die Display-Helligkeit vom ESP32 gesteuert werden kann.**
- Falls euer Display nur *ein* kleines schwarzes Bauteil mit drei Pins hat, dann hat das Display *keinen* Transistor eingebaut. **In diesem Fall muss für R3 ein 5,1-Ω-Widerstand eingesetzt werden (anders als auf dem Bestückungsdruck angegeben!). Die Lötbrücke SJ5 muss offen bleiben, da sonst der ESP32 Schaden nehmen kann!**

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
Wie man sieht, gibt es hier die zusätzliche Lötbrücke IOREF. Diese müsst ihr (anders als im Foto!) auf 3,3 V setzen, also das mittlere und das linke (mit „3V“ beschriftete) Pad mit einem Tropfen Lötzinn verbinden. 

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
#### Schritt 1: Lötbrücken setzen

Als erstes solltet ihr alle benötigten Lötbrücken setzen. 

- SJ1 bestimmt über die Ausrichtung des Bildschirms. Bei Verwendung des 3D-gedruckten ZOE-Einlegers sollte diese Lötbrücke für das resistive Display normalerweise auf die Seite mit dem „S“ und für das kapazitive Display auf die Seite mit der „1“ gesetzt werden. An diese Lötbrücke kommt man auch später noch ganz gut dran, sodass es kein Problem ist, wenn sie falsch gesetzt wurde.
- Wie ihr SJ2, SJ3 und SJ4 setzen müsst, findet ihr unter „Hinweise zu den Lötbrücken zur Auswahl der Stromversorgung“.
- SJ5 sollte nur bei Verwendung eines resistiven Displays mit eingebautem Transistor gesetzt werden.

#### Schritt 2: Widerstände und Dioden

Als nächstes kommen die flachen Bauteile dran. Bei Widerständen ist die Polarität egal, bei den Dioden ist der Strich, welcher den Minuspol kennzeichnet, auf dem Bestückungsdruck eingezeichnet. 

#### Schritt 3: IC-Sockel

Damit der CAN-Transceiver-IC (IC4) nicht durch die Hitze Schaden nimmt, wird er nicht auf die Platine gelötet, sondern nur ein passender Sockel, in den der IC später eingesteckt wird. Die Einbaurichtung des ICs kann über eine einseitige Einkerbung kontrolliert werden, welche auf dem Bestückungsdruck eingezeichnet ist.

#### Schritt 4: Keramik-Kondensatoren

Nun sind C2, C3 und C4 an der Reihe. Es können Keramik-Kondensatoren mit 2,5 mm oder 5 mm Rastermaß verwendet werden. Die Polarität ist egal. 

#### Schritt 5: Piezo-Summer

Falls ein Piezo-Summer für Printmontage verbaut wird, sollte dieser je nach Abmessungen jetzt oder etwas später eingelötet werden. Bei einigen Piezo-Summern muss die Polarität beachtet werden (z.B. wenn die Beinchen verschieden lang sind, das längere ist dann Plus), bei anderen nicht.

#### Schritt 6: Stiftleiste für GPS-Modul

Als Nächstes wird eine Stiftleiste eingelötet, auf die später das GPS-Modul montiert werden kann. Das GPS-Modul selbst sollte jetzt noch nicht mit angelötet werden, da es die Anschlüsse für das kapazitive Display teilweise verdecken würde. Je nach GPS-Modul wird eine Stiftleiste mit 4 oder 5 Pins benötigt. Es empfiehlt sich, die Metallstifte etwas zu kürzen, damit sie später nicht so weit herausstehen.

Inzwischen sollte die Platine ungefähr so aussehen:

![Platine](/Platine%20V8/Bilder/Platine1.jpg)

#### Schritt 7: Transistoren

Jetzt sind die bipolaren Transistoren T1, T4, T5, T6 und der MOSFET Q1 an der Reihe. Bei den bipolaren Transistoren muss jeweils der mittlere Pin vorsichtig etwas zurechtgebogen werden. Die Einbaurichtung dürfte selbsterklärend sein. Der MOSFET muss so herum eingebaut werden, dass die Beschriftung zum Rand der Platine zeigt (und die Metallfläche entsprechend in Richtung der Kabelanschlüsse). 

#### Schritt 8: Schraubklemmblöcke

Nun werden die 3-polige Schraubklemme für die Stromversorgung und die 2-polige Schraubklemme für den CAN-Bus eingelötet.

#### Schritt 9: ESP32

Beim ESP32 bietet es sich an, auf die vier äußersten Pins jeweils als Abstandshalter ein Plastikteil einer Stiftleiste draufzuschieben, ähnlich wie hier: https://c1.staticflickr.com/5/4850/39953812743_f40f2e705d.jpg. Damit sitzt er in der perfekten Höhe.

#### Schritt 10: 3,3-V-Spannungsregler

Der 3,3-V-Spannungsregler kommt in das mit „LC78_03-0.5“ beschriftete Rechteck. Falls der Spannungsregler LMO78_03-0.5 verwendet wird (wie im gleich folgenden Foto), sollte dieser eventuell ein wenig gekippt eingebaut werden, da er sonst etwas zu weit in Richtung des Kondensators C6 übersteht, sodass dieser nicht mehr richtig passt.

#### Schritt 11: Elektrolyt-Kondensatoren

Bei den Elkos (C1, C5 und C6) muss auf die Polarität geachtet werden. Der Pluspol ist durch einen längeren Draht, der Minuspol durch einen auffälligen weißen Strich auf dem Gehäuse gekennzeichnet.

#### Schritt 12: 5-V-Spannungsregler

Der 5-V-Spannungsregler gehört in das mit „LC78_05-0.5“ beschriftete Rechteck. 

Anschließend sollte die Platine ungefähr so aussehen:

![Platine](/Platine%20V8/Bilder/Platine2.jpg)

#### Schritt 13: Display

Bevor ihr Display und Platine zusammenfügt, kontrolliert nochmal, ob alle Lötstellen gut aussehen und ob ihr am Display alle erforderlichen Lötbrücken gesetzt habt, denn ihr kommt anschließend nicht mehr dran! 

Beim kapazitiven Display empfehle ich, dieses erstmal in den 3D-gedruckten Einleger zu setzen (microSD-Karte nicht vergessen!), anschließend die Platine darauf zu platzieren und erst dann, im „lose eingebauten Zustand“, beides zu verlöten. 

Beim resistiven Display ist dieses Vorgehen nicht erforderlich, hier bietet es sich stattdessen an, wieder vier Plastikteile einer Stiftleiste als Abstandshalter zu nutzen. Achtet darauf, dass der SD-Karten-Halter nicht mit von der Platine abstehenden Drähten in Berührung kommt. 

#### Schritt 14: GPS-Modul

Als Nächstes wird das GPS-Modul auf die zuvor eingelötete Stiftleiste gelötet.

#### Schritt 15: IC einsetzen

Zu guter Letzt wird der CAN-Transceiver-IC in den zuvor eingelöteten Sockel gesteckt. Bei „fabrikfrischen“ ICs müssen hierzu meist die Beinchen etwas nach innen gebogen werden, damit sie passen. 

## Verkabelung

Die Drähte zur USB-Buchse, zum OBD-Stecker und zum Piezo-Summer (falls einer mit Kabeln verwendet wird) können auf drei verschiedene Arten an der Platine angeschlossen werden: Durch Anschrauben in angelötete Schraubklemmblöcke, über die SMD-Lötpads oder durch direktes Einlöten der Kabel in die Löcher für die Schraubklemmblöcke. 

Die Beschriftung der Anschlüsse befindet sich jeweils an den SMD-Lötpads, die direkt an die zugehörigen Schraubklemmen angrenzen.

#### USB-Buchse

Um die USB-Buchse in den 3D-gedruckten Einleger zu bekommen, müssen zunächst die beiden Montagepins des Buchsengehäuses etwas gekürzt werden. Anschließend die vier Anschlusspins (Masse, D+, D- und +5 V) nach hinten umbiegen und darauf achten, dass sie nicht mit dem Buchsengehäuse in Berührung kommen. 

An Masse (GND) und +5 V lötet ihr Drähte an, die dann an der Platine angeschlossen werden können. Achtet darauf, dass durch das Lötzinn keine Verbindung mit dem Buchsengehäuse hergestellt wird.

Die beiden Datenleitungen (die mittleren Pins) können im einfachsten Fall kurzgeschlossen werden, dies entspricht der EU-standardisierten Signalisierung eines USB-Ladegeräts. Hierzu einfach die beiden Drähte etwas zur Mitte biegen und mit einem Tropfen Lötzinn verbinden (wieder darf keine Verbindung zum Buchsengehäuse entstehen). Manche USB-Geräte akzeptieren diese Signalisierung allerdings nicht und laden entweder gar nicht oder nur langsam. Um die USB-Buchse für solche Geräte kompatibel zu machen, müsst ihr eventuell statt der Kurzschlussmethode mit Widerständen bestimmte Spannungen an die Datenleitungen anlegen. Mehr Infos dazu findet ihr z.B. hier: http://dh2mic.darc.de/files/usb-adapter-v12.pdf

![USB-Buchse](/Platine%20V8/Bilder/20190320_204215.jpg)

Zum Schluss noch alles mit Heißkleber versiegeln, damit kein Kurzschluss entstehen kann und die USB-Buchse nicht herausrutscht.

#### OBD-Stecker

Die Belegungen einer OBD2-Schnittstelle findet ihr hier: https://commons.wikimedia.org/wiki/File:OBD2-Buchse-Stecker-Belegung.jpg

Vier Pins werden benötigt: Fahrzeugmasse (GND) und +12 V zur Stromversorgung sowie CAN High und CAN Low zur Datenübertragung. 

Achtung: Den Lötkolben nicht zu lange an die Metallstifte des OBD-Steckers halten, da sonst das Plastik drumherum aufweicht, wodurch der Metallstift sich womöglich leicht verdreht oder verschiebt. 

Am Ende sollte es etwa so aussehen. Ich habe für Masse und CAN Low einen schwarzen und für +12 V und CAN High einen roten Draht verwendet (ist leider auf dem Foto nicht erkennbar). Gegebenenfalls sollten die Lötstellen noch mit Heißkleber umhüllt werden, damit kein Kurzschluss entstehen kann.

![OBD-Stecker](/Platine%20V8/Bilder/OBD-Stecker-beschriftet.jpg)

#### Schraubklemmblöcke

Um die Drähte gut in den Schraubklemmblöcken befestigen zu können, sollten die Enden jeweils verdrillt und mit dem Lötkolben verzinnt werden. Wer über das entsprechende Equipment verfügt, kann (und soll) natürlich stattdessen Aderendhülsen verwenden. 

Wer eine USB-Buchse verwendet, muss zwei GND-Drähte in eine Schraubklemme zwängen. Hierzu sollten diese beiden Drähte zusammen verzinnt bzw. zusammen in eine Aderendhülse gecrimpt werden.
