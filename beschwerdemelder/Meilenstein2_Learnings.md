# Beschwerdemelder – Learnings für den Meilenstein-2-Report

Testprototyp für Gesunde, kein Medizinprodukt. Stand: 2. November 2026.

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

- **Fixierpunkt:** ein Ring mit kleinem schwarzem Kern statt einer grossen Scheibe, damit der Blick genauer auf einer Stelle ruht.
- **Mehr Daten pro Punkt:** 12–22 Proben über mindestens 1,5 s statt 8–14. Die Einschwingzeit nach dem Erscheinen des Punktes ist länger (0,9 s). Proben werden nur genommen, wenn die Augen sicher offen sind.
- **Automatische Wiederholung:** Punkte mit zu wenig gültigen Proben werden einmal wiederholt.
- **Sichtbares Ergebnis:** Nach den 3 Kontrollpunkten zeigt die Seite Zielpunkt und Schätzung mit einer Verbindungslinie. Die Testleitung entscheidet dann «Übernehmen» oder «Neu kalibrieren».
- **Verschiebung korrigiert:** Liegen alle Schätzungen in dieselbe Richtung daneben, wird diese Verschiebung automatisch ausgeglichen, wie bei Taste C.
- **Urteil nach der Anordnung:** Die Einschätzung, ob die Genauigkeit reicht, richtet sich vor allem nach der horizontalen Abweichung, weil alle Auswahlen nebeneinander liegen.
- **Protokoll:** Jede Kalibrierung wird mit Gesamt-, horizontaler und vertikaler Abweichung, Verschiebung und Fenstergrösse protokolliert, als Kennwerte für den Report.

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
5. Wie lange dauert ein ganzer Durchgang von «Ruhe» bis «Gesendet» im Vergleich zur alten Skala? Das lässt sich aus den Zeitstempeln im Protokoll ablesen.
