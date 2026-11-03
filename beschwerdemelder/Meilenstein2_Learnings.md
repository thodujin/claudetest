# Beschwerdemelder – Learnings für den Meilenstein-2-Report

Testprototyp für Gesunde, kein Medizinprodukt. Stand: 2. November 2026 (zwei Selbsttests).

## Kontext des ersten Tests

- **Art:** erster explorativer Selbsttest durch das Projektteam (n = 1), kein formaler Nutzertest
- **Aufbau:** Laptop-Webcam, Chrome, Seite über VS Code / Live Server
- **Blick:** WebGazer 3.5.3 (Kalibrierung mit 13 Punkten)
- **Blinzeln:** MediaPipe Face Landmarker
- **Getestete Version:** Stärke als Skala 0–10, 11 Felder in einer Reihe

> Die folgenden Befunde sind qualitative Beobachtungen aus diesem einen Test. Sie geben die Richtung für das Redesign vor, belegen aber noch nichts. Zur Bestätigung braucht es Tests mit weiteren Personen.

## Befunde

| # | Befund | Folgerung für das Design |
|---|---|---|
| B1 | **Die Kalibrierung reicht noch nicht.** Der geschätzte Blickpunkt ist zu ungenau, um Felder zuverlässig zu treffen. | Kalibrierung verbessern (siehe M2). Die Genauigkeit vor jedem Test messen und protokollieren. |
| B2 | **Die Skala 0–10 lässt sich mit den Augen kaum bedienen.** Elf schmale Felder nebeneinander sind mit dem Blick schwer anzusteuern und zu bestätigen. | Weniger und grössere Ziele pro Bildschirm (siehe M1). |
| B3 | **Horizontal wählen ist deutlich leichter als vertikal.** Links und rechts gelingt besser als oben und unten. | Auswahlen möglichst **nebeneinander** anordnen, wenig vertikale Unterscheidung. |
| B4 | **Drei Felder pro Auswahl sind ideal.** | Stufenweise auswählen: erst ein grober Bereich, dann der genaue Wert. |

Zu B3 eine Vermutung, noch ungeprüft: Das Augenlid verdeckt die Iris bei vertikalen Bewegungen teilweise, und die Webcam blickt von oben. Darum ist die vertikale Schätzung typischerweise schlechter. Die neue Kalibrieranzeige gibt die Abweichung horizontal und vertikal getrennt aus. Damit lässt sich die Vermutung im nächsten Test prüfen.

## Umgesetzte Massnahmen

### M1 – Stärke in zwei Stufen (aus B2, B3, B4)

1. **Bereich wählen:** drei Felder nebeneinander
   - **Leicht (0–4)**, grün
   - **Mittel (5–7)**, gelb-orange
   - **Stark (8–10)**, rot
2. **Zahl wählen:** Danach erscheinen nur die Zahlen dieses Bereichs, ebenfalls in einer Reihe, im selben Farbton. Das sind 3 Felder (Mittel, Stark) oder 5 Felder (Leicht).

Weitere Punkte:
- **Bedeutung nicht nur über Farbe:** Die Farbe steht immer zusammen mit Wort und Zahlen, damit auch Menschen mit Farbsehschwäche die Bereiche unterscheiden können.
- **Markierung auf farbigen Feldern:** Auf «Mittel» war die orange Markierung kaum sichtbar. Darum zeigen farbige Felder die Markierung als dicken dunklen Rahmen.
- **Zurück:** Von der Zahl geht es zurück zum Bereich, vom Bereich zurück zur Beschwerde, aus «Prüfen» zurück zur Zahl.
- **Protokoll und Pflegeansicht** zeigen Zahl und Bereich, zum Beispiel «Schmerzen 6/10 (Mittel)».
- **Grenzen:** Die Vorgabe lautete «stark 7–10», das überschneidet sich mit «mittel 5–7». Umgesetzt ist 8–10. *Bitte im Team bestätigen.*

### M2 – Kalibrierung überarbeitet (aus B1)

- **Fixierpunkt:** ein Ring mit kleinem Punkt in der Mitte statt einer grossen Scheibe, damit der Blick genauer auf einer Stelle ruht.
- **Mehr Daten pro Punkt:** 12–22 Proben über mindestens 1,5 s statt 8–14. Die Einschwingzeit nach dem Erscheinen des Punktes ist länger (0,9 s). Proben werden nur genommen, wenn die Augen sicher offen sind.
- **Automatische Wiederholung:** Punkte mit zu wenig gültigen Proben werden einmal wiederholt.
- **Sichtbares Ergebnis:** Nach den 3 Kontrollpunkten zeigt die Seite Zielpunkt und Schätzung mit einer Verbindungslinie. Die Testleitung entscheidet dann «Übernehmen» oder «Neu kalibrieren».
- **Verschiebung korrigiert:** Liegen alle Schätzungen in dieselbe Richtung daneben, wird diese Verschiebung automatisch ausgeglichen, wie bei Taste C.
- **Urteil nach der Anordnung:** Die Einschätzung, ob die Genauigkeit reicht, richtet sich vor allem nach der horizontalen Abweichung, weil alle Auswahlen nebeneinander liegen.
- **Protokoll:** Jede Kalibrierung wird mit Gesamt-, horizontaler und vertikaler Abweichung, Verschiebung und Fenstergrösse protokolliert, als Kennwerte für den Report.

## Zweiter Selbsttest (nach M1 und M2)

| # | Befund | Folgerung für das Design |
|---|---|---|
| B5 | **Die Kalibrierung ist deutlich besser.** Dazu beigetragen hat auch eine bessere Sitzposition: Abstand 50–70 cm, Kopf ruhig, Licht von vorn. | Die überarbeitete Kalibrierung (M2) beibehalten. Vor jedem Test Abstand, Licht und Kopfhaltung vorgeben und in der Anleitung festhalten. |
| B6 | **Die Auswahl über drei Felder nebeneinander klappt deutlich besser** als über die Skala mit 11 Feldern. | Bestätigt B2 bis B4. Bei allen Auswahlen das Muster «wenige grosse Felder nebeneinander» verwenden. |
| B7 | **Grössere Felder würden die Auswahl weiter erleichtern**, besonders Senden, Zurück und Abbrechen. Auf «Stimmt das?» blieb viel Fläche ungenutzt. | Siehe M3. |
| B8 | **Nach längerer Benutzung werden die Augen müde.** | Ermüdung als eigenes Kriterium erheben. Die Zahl der bewussten Blinzeln und die Fixierdauer pro Meldung senken (siehe offene Fragen). |

Mögliche Ursachen von B8, noch nicht geprüft:
- **Bewusste Lidschlüsse:** Pro Meldung braucht es mindestens 5 lange Blinzeln von je mindestens 0,8 s (Aktivieren, Beschwerde, Bereich, Zahl, Senden).
- **Fixieren:** Jede Markierung verlangt etwa 0,7 s ruhiges Fixieren, bei ungenauer Schätzung länger oder wiederholt.
- **Seltener spontan blinzeln:** Bei konzentrierter Bildschirmarbeit blinzelt man seltener, die Augen trocknen aus.
- **Kalibrierung:** 13 Punkte mit Fixieren kommen zu Beginn noch dazu.

Für die Patientengruppe ist B8 besonders relevant. Wer auf der Intensivstation liegt, ist oft ohnehin erschöpft, und die Augen sind wegen Lagerung oder Beatmung womöglich trocken.

### M3 – Grössere Auswahlfelder (aus B7)

- **Zurück und Abbrechen auf allen Seiten:** mindestens 110 px bzw. 14 % der Fensterhöhe statt 76 px, grössere Schrift.
- **«Stimmt das?» und «Gesendet»:** Senden, Zurück, Abbrechen und Zurücknehmen füllen den freien Platz, mindestens 24 % der Fensterhöhe.

### M4 – Sicherheit und Feinschliff

- **Nichts vormarkiert:** Auf «Stimmt das?» ist «Senden» beim Erscheinen nicht mehr markiert. Vorher hätte ein einziges unbeabsichtigtes langes Blinzeln sofort gesendet. Jetzt muss «Senden» erst angeschaut werden.
- **Bereiche bestätigt:** Leicht 0–4, Mittel 5–7, Stark 8–10.
- **Farbmodus:** Hell und Dunkel lassen sich umschalten, nicht nur automatisch nach Systemeinstellung. Die Bereichsfarben sind auch im dunklen Modus gut erkennbar.
- **Keine Übergangsanimationen mehr:** Es bleibt nur die kurze grüne Bestätigung beim Wählen.
- **Kein Überlappen:** Bei kleinem Fenster oder aufgeklappter Steuerung überlappen sich Felder nicht mehr, die Seite scrollt stattdessen.

### M5 – Wartezeit nach dem Senden (dritter Selbsttest)

- **Befund B9:** Die Anzeige «Gesendet» bleibt zu lange stehen. Ohne Testleitung quittiert niemand, und der Ablauf hängt.
- **Massnahme Pflege-Simulation:** Für Tests ohne Testleitung quittiert die Pflege automatisch nach 10 s. Die Zeit ist einstellbar, die Automatik abschaltbar. Im Protokoll steht die Quittung als simuliert.
- **Befund zu «Zurücknehmen»:** Als einziges und sehr grosses Feld war «Zurücknehmen» per Blick praktisch dauernd markiert. Ein längeres Augenschliessen beim Warten hätte die Meldung ungewollt zurückgenommen.
- **Massnahme «Zurücknehmen»:** Das Feld hat wieder normale Grösse und liegt unten. Es wird nur markiert, wenn man es bewusst anschaut.
- **Folgerung für das Design:** «Gross» ist nicht immer besser. Bei einem einzelnen Feld mit Folgen, das nicht gewählt werden soll, verhindert eine kleinere Zielfläche ungewolltes Auslösen.

### M6 – Kalibrierbereich und Standardwerte

- **Automatischer Bereich:** Der Kalibrierbereich legt sich automatisch auf die Fläche der Beschwerdefelder, so wie die Testperson sie mit eingeklappter Steuerung sieht. Vorher lagen Punkte auch über der Überschrift, wo es nichts zu wählen gibt.
- **Neue Standardwerte:** 13 Punkte, «Markieren nach» 900 ms statt 700 (seltener ein Sprung auf ein falsches Feld, wenn der Blickpunkt wackelt), «Glättung» 500 ms statt 350 (ruhigerer Blickpunkt).

### M7 – Kalibrierpunkte auf den Feldmitten (aus B10)

- **Befund B10:** Die untere Beschwerdereihe (Durst, Hunger, Unbequeme Lage) ist manchmal schwierig zu wählen.
- **Ursache 1 (gefunden):** Die Kalibrierpunkte lagen in einem gleichmässigen Raster. Die mittlere Punktreihe fiel dabei auf die Fuge zwischen den beiden Beschwerdereihen. Auf Höhe von Durst/Hunger/Lage gab es keinen Kalibrierpunkt.
- **Ursache 2 (vermutet):** Die Reihe hat Nachbarn oben und unten, eine vertikale Ungenauigkeit (B3) wirkt sich also in beide Richtungen aus.
- **Massnahme:** Bei automatischem Bereich liegt je ein Kalibrierpunkt auf jeder Spalte und jeder Reihe: obere Reihe, untere Reihe, Zurück/Abbrechen. Die 4 Zusatzpunkte liegen dazwischen. Die 3 Kontrollpunkte liegen je einer pro Reihe, so misst die Kontrolle die untere Reihe gezielt mit.
- **Weitere Option, falls B10 bleibt:** Zurück und Abbrechen an die Seiten statt nach unten. Dann hätte die untere Beschwerdereihe nur noch einen vertikalen Nachbarn.

### M8 – Obere Kante dazunehmen (aus B11)

- **Befund B11:** Nach M7 war die **obere** Reihe schwieriger zu wählen. Vorher war es die untere.
- **Erklärung:** Die Regression von WebGazer staucht Schätzungen zur Mitte hin. Liegen die äussersten Kalibrierpunkte nur auf den Feldmitten, fehlt der Zug nach oben, und ein Blick nach oben landet zu tief.
- **Massnahme:** Je eine Punktreihe auf dem oberen Rand des Bereichs, auf der oberen Reihe, auf der unteren Reihe und auf Zurück/Abbrechen (4 × 3 Punkte plus 1 Mittelpunkt).
- **Folgerung für das Design:** Mit drei Ebenen übereinander (2 Beschwerdereihen plus Zurück/Abbrechen) und je etwa 20–25 % Höhe liegt die vertikale Genauigkeit (11–16 %) an der Grenze. Welche Reihe schwierig ist, verschiebt sich mit der Kalibrierung. Robuster wäre ein Layout mit nur zwei Ebenen: Zurück und Abbrechen an die Seiten.

## Kennwerte für den nächsten Test (bitte eintragen)

| Durchgang | Abweichung gesamt | horizontal | vertikal | nach Korrektur | Bemerkung (Licht, Brille, Abstand) |
|---|---|---|---|---|---|
| 1 | | | | | |
| 2 | | | | | |

Die Werte stehen nach jeder Kalibrierung unter «Kamera» und im exportierten Protokoll.

## Offene Fragen für den nächsten Test

1. Werden die drei Bereichsfelder mit dem Blick zuverlässig getroffen? Und die 5 Zahlen bei «Leicht»? Falls nicht: «Leicht» teilen (0–2 / 3–4) oder 0 als eigenes Feld «keine».
2. Liegen «Zurück» und «Abbrechen» unter den Feldern gut, oder stören sie, weil sie vertikal angewählt werden müssen?
3. Ist die vertikale Abweichung in den Messwerten tatsächlich grösser als die horizontale (B3)?
4. Helfen die Farben oder lenken sie ab? Wirkt Rot für «Stark» alarmierend?
6. **Augenermüdung (B8) messen:** Nach jedem Durchgang die Ermüdung erfragen, zum Beispiel auf einer Skala von 0 bis 10 («Wie müde sind Ihre Augen?»), und notieren, nach wie vielen Meldungen sie spürbar wird. Wie viele lange Blinzeln und wie viel Zeit eine Meldung braucht, steht im exportierten Protokoll (Bilanz pro Durchgang).
7. **Massnahmen gegen Ermüdung vergleichen:** kürzere Mindestdauer für langes Blinzeln (zum Beispiel 600 statt 800 ms), weniger Schritte pro Meldung, dunkler Modus gegen Blendung, Kalibrierung mit 9 statt 13 Punkten, Pausen zwischen den Durchgängen.
5. Wie lange dauert ein ganzer Durchgang von «Ruhe» bis «Gesendet» im Vergleich zur alten Skala? Das lässt sich aus den Zeitstempeln im Protokoll ablesen.
