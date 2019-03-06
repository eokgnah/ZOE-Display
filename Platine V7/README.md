## Platine V7

Diese Version funktioniert mit dem kapazitiven Display einwandfrei und passt auch in den 3D-Druck-Einleger.

Das resisitve Display funktioniert technisch auch, allerdings passt die Platine damit nicht in den 3D-Druck-Einleger!

### Allgemeine Hinweise zur Bestückung

- Es können nur Keramikkondensatoren mit 2,5 mm Rastermaß verwendet werden, obwohl auf der Platine jeweils ein zusätzliches Pad für 5 mm Rastermaß vorhanden ist. Denn diese Pads ist nicht angeschlossen!
- Bei den beiden Spannungsreglern ist leider auf dem Bestückungsdruck nicht ersichtlich, welcher wohin gehört. Der 5-V-Spannungsregler muss auf die Seite in Richtung ESP32, der 3,3-V-Spannungsregler auf die Seite in Richtung Anschlussbuchsen.
- Ein 3,3-V-Spannungsregler ist nicht unbedingt erforderlich, da alternativ auch der interne Spannungsregler des ESP32 genutzt werden kann. Falls die Platine mit 3,3-V-Spannungsregler bestückt wird, muss die Lötbrücke SJ4 gesetzt werden; andernfalls müssen die Lötbrücken SJ2 und SJ3 gesetzt werden.
- Der MOSFET (Q1) muss so herum eingebaut werden, dass die Beschriftung in Richtung Spannungsregler zeigt.

### Bei Verwendung des kapazitives Displays

- Die Bauteile R1, R2, R3, R14 sowie T1, T2 und T3 werden nicht benötigt.
- Beim Display müssen die Lötbrücken „backlight“, „13“, „12“ und „11“ gesetzt werden.
- Falls ein Display der neusten Version mit IOREF-Lötbrücke zum Einsatz kommt, sollte diese Lötbrücke auf 3,3 V („3V“) gesetzt werden. Die Widerstände R4 und R7 werden dann nicht benötigt.
- Ich empfehle, das Display erst dann anzulöten, wenn Platine und Display bereits lose im 3D-gedruckten Einleger platziert sind. Ansonsten wird es wahrscheinlich sehr schwierig, diese hineinzubekommen.
