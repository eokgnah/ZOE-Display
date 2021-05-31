# ZOE CAN ESP32

Bei diesem Projekt handelt es sich um eine Display-Platine zum Auslesen von Fahrzeugdaten (z.B. State of Health, Ladeleistung, Reifendruck) für die Renault ZOE Phase 1 (Q210, R210, R240, Q90 und R90, nur bis 2019).

Das Display wird mittels einer 3D-druckbaren Halterung in die Ablage unterhalb des R-Link eingelegt und über den direkt darunterliegenden OBD-Port an den CAN-Bus des Fahrzeugs angeschlossen. Es verwendet einen ESP32-Mikrocontroller mit WLAN-Funktionalität und kann per Webbrowser konfiguriert werden. 

Weitere Informationen und Bilder gibt es im GoingElectric-Forum unter https://www.goingelectric.de/forum/viewtopic.php?t=37914

Platine V5 wird über den USB-Port des R-Link mit Strom versorgt. 

Bei den Platinen V7 und V8 erfolgt die Stromversorgung über den OBD-Port. Hierbei schaltet sich die Platine beim Aufschließen des Fahrzeugs oder Starten eines Ladevorgangs automatisch ein (sobald der CAN-Bus aktiv ist). Nach Abschließen des Fahrzeugs bzw. Beendigung des Ladevorgangs kann sich das Display nach einer konfigurierbaren Zeitdauer auch selbst wieder ausschalten.
Optional kann eine USB-Buchse integriert werden, über welche beispielsweise Mobilgeräte aufgeladen werden können.

Für die Platine V8 existiert eine ausführliche Lötanleitung unter https://github.com/eokgnah/ZOE-Display/blob/master/Platine%20V8/README.md.
Der Aufbau sollte damit auch für Unerfahrene kein allzu großes Problem darstellen.

<pre>
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!! OHNE GEWÄHR, ALLES AUF EIGENE GEFAHR, NUR ZU TESTZWECKEN !!!!
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
</pre>

## Verwendete Bauteile

- ESP32-Development-Board (z.B. https://www.ebay.de/itm/162572643462 oder https://www.amazon.de/gp/product/B071P98VTG)
- 2,8 Zoll 240 x 320 SPI TFT Panel resistiver Touchscreen (mit Display-Treiber ILI9341, z.B. https://www.amazon.de/gp/product/B0749N3S33/)
- alternativ mit kapazitivem Touchscreen (Adafruit 1947 mit Display-Treiber ILI9341, z.B. https://www.amazon.de/gp/product/B00R3R65C0/ oder https://www.mouser.de/ProductDetail/Adafruit/1947?qs=GURawfaeGuArmJSJoJoDJA%3D%3D)
- SD-Karte (bei resistivem Touchscreen) bzw. microSD-Karte (bei kapazitivem Touchscreen)
- optional GPS-Modul (z.B. https://www.ebay.de/itm/163636495985 oder https://www.amazon.de/gp/product/B01N38EMBF/)
- Kleinteile (siehe Ordner zur jeweiligen Platinen-Version)

## Verbindungen mit resistivem Touchscreen
<pre>
ESP32 Dev Board Pinout

Wohin           Bezeich.       ESP32 Pins       Bezeich.    Wohin

                            3V3         GND
                            EN          G23     MOSI        Display,Touch,SD
                ST          G36         G22
                            G39         G1      (TX)
                            G34         G3      (RX)
                (CAN2 RX)   G35         G21     CS          Touch
                (CAN2 TX)   G32         GND
                HR          G33         G19     MISO        Display,Touch,SD
                            G25         G18     SCLK        Display,Touch,SD
GPS             GPS TX      G26         G5 
GPS             GPS RX      G27         G17     CAN TX      CAN Bus
BUZZER+                     G14         G16     CAN RX      CAN Bus 
                POWER OFF   G12         G4      RST         Display
                            GND         G0      (BOOT)
SD              CS          G13         G2      DC          Display
                (Flash)     G9          G15     CS          Display
                (Flash)     G10         G8      (Flash)
                (Flash)     G11         G7      (Flash)
                            5V          G6      (Flash)
</pre>                    
RX und TX gibt den Pin an, mit dem es verbunden werden muss. GPS TX muss also auf den Pin
TX am GPS Modul! 

CAN2 ist derzeit experimentell. 

ST = Screen Turn, ST=1 (mit 10k auf 3V3) -> Bildschirm um 180 Grad gedreht

HR = Helligkeitsregelung, kann einen Transistor ansteuern, über den die LED-Hintergrundbeleuchtung des Displays gedimmt werden kann.

POWER OFF = Ausschalt-Pin für die Stromversorgung über den OBD-Port

## Verbindungen mit kapazitivem Touchscreen
<pre>
ESP32 Dev Board Pinout

Wohin           Bezeich.       ESP32 Pins       Bezeich.    Wohin

                            3V3         GND
                            EN          G23     SPI MOSI    Display
                ST          G36         G22     I²C SCL     Display
                            G39         G1      (TX)
                            G34         G3      (RX)
                (CAN2 RX)   G35         G21 
                (CAN2 TX)   G32         GND
Display         HR          G33         G19     SPI MISO    Display
Display         I²C SDA     G25         G18     SPI SCLK    Display
GPS             GPS TX      G26         G5
GPS             GPS RX      G27         G17     CAN TX      CAN Bus
BUZZER+                     G14         G16     CAN RX      CAN Bus 
                POWER OFF   G12         G4      RST         Display
                            GND         G0      (BOOT)
Display         CARDCS      G13         G2      DC          Display
                (Flash)     G9          G15     CS          Display
                (Flash)     G10         G8      (Flash)
                (Flash)     G11         G7      (Flash)
                            5V          G6      (Flash)
</pre>                    
RX und TX gibt den Pin an, mit dem es verbunden werden muss. GPS TX muss also auf den Pin
TX am GPS Modul! 

CAN2 ist derzeit experimentell. 

ST = Screen Turn, ST=1 (mit 10k auf 3V3) -> Bildschirm um 180 Grad gedreht

HR = Helligkeitsregelung, an Pin GPIO33 liegt ein PWM Signal an, welches über Pin D5 am Display
(neben CARDCS) die Regelung der Displayhelligkeit erlaubt. Achtung: Die Lötbrücke #5 auf der 
Displayplatine muss hierfür gesetzt werden.

POWER OFF = Ausschalt-Pin für die Stromversorgung über den OBD-Port
                    
## Allgemein
-  Beim Betrieb des resistiven Displays mit 3,3 V sollte der Jumper J1 am Display gesetzt (verbunden) werden (Ausschalten
des Spannungsreglers des Displays, sonst sinken die 3,3 V auf irgendwas unter 3 V). Der Touch IRQ Pin bleibt leer.
- Das Display mit kapazitivem Touchscreen erhält 5 V Versorgungsspannung. Falls das verwendete Display keine IOREF-Lötbrücke besitzt bzw. diese auf 5 V gesetzt wurde, muss eine geeignete Maßnahme vorgesehen werden, um die Spannungspegel am I²C-Bus auf max. 3,3 V zu begrenzen (das Display zieht die Leitungen nämlich mit 10-kΩ-Pull-Up-Widerständen gegen 5 V).
