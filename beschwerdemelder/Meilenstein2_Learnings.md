# Beschwerdemelder – Learnings für den Meilenstein-2-Report

Testprototyp für Gesunde, kein Medizinprodukt. Stand: 3. November 2026 (iterative Selbsttests an zwei Tagen).

## Zusammenfassung für den Report

**Vorgehen:** iterative Selbsttests durch das Projektteam (n = 1) an zwei Tagen. Nach jeder Runde folgte eine Anpassung am Prototyp (M1–M9). Die Befunde sind qualitative Beobachtungen und geben die Richtung vor. Belegt sind sie erst nach Tests mit weiteren Personen.

### Gestaltungsprinzipien aus den Befunden

| # | Prinzip | Abgeleitet aus | Umgesetzt in |
|---|---|---|---|
| P1 | **Wenige grosse Ziele, höchstens drei nebeneinander.** Elf Felder in einer Reihe waren mit dem Blick kaum bedienbar, drei Felder funktionieren gut. | B2, B4, B6 | M1, M9 |
| P2 | **Horizontal statt vertikal unterscheiden.** Oben/unten ist mit der Webcam deutlich ungenauer als links/rechts. Mehrere Auswahlreihen übereinander führten zu Fehlwahlen, und die schwierige Reihe wechselte mit jeder Kalibrierung. | B3, B10, B11, B12 | M9 (nur noch eine Auswahlreihe plus Zurück/Abbrechen) |
| P3 | **Erst grob, dann genau.** Zweistufige Auswahl statt einer langen Liste: Gruppe → Beschwerde, Bereich → Zahl. | B2, B4, B12 | M1, M9 |
| P4 | **Sicherheit vor Tempo.** Folgenreiche Felder sind nie vormarkiert («Senden», «Zurücknehmen»). Ein einzelnes übergrosses Feld ist per Blick dauernd markiert und löst leicht ungewollt aus, «gross» ist also nicht immer besser. | B9 | M4, M5 |
| P5 | **Die Kalibrierung muss zur Oberfläche passen.** Punkte gehören auf die Felder und an den Rand des Bereichs, nicht in ein neutrales Raster. Das Ergebnis muss sichtbar und messbar sein. | B1, B5, B10, B11 | M2, M6, M7, M8 |
| P6 | **Rahmenbedingungen gehören zum System.** Licht, Abstand, Kopfhaltung und Tagesform bestimmen die Genauigkeit stärker als die Software. Darum vor jeder Nutzung neu kalibrieren, mit Nachjustieren (C) und Abtastmodus als Rückfallebene. | B5, B13 | M2, M6, Anleitung |
| P8 | **Das einfachste Verfahren kann das bessere sein.** Der Abtastmodus (Felder leuchten nacheinander auf, langes Blinzeln wählt) wirkte entspannter und angenehmer als die Blicksteuerung: keine Kalibrierung, kein Fixieren, keine Ungenauigkeit oben/unten. Dafür ist er langsamer. | B14 | Abtastmodus als gleichwertige Option prüfen, nicht nur als Notlösung |
| P7 | **Jeder Schritt kostet Kraft.** Langes Blinzeln und Fixieren ermüden die Augen. Jeder zusätzliche Schritt (z. B. die Gruppenwahl) muss sich durch weniger Fehlwahlen lohnen. | B8 | Zielkonflikt mit P3, zu messen |

### Zielkonflikte, die der Report benennen sollte

- **Genauigkeit gegen Aufwand:** Zweistufige Auswahl (P1–P3) bedeutet weniger Fehlwahlen, aber ein langes Blinzeln mehr pro Meldung (P7). Atemnot als dringendste Beschwerde braucht jetzt einen Schritt mehr.
- **Grösse gegen Sicherheit:** Grosse Felder sind leichter zu treffen, aber auch leichter ungewollt zu treffen (P4).
- **Tempo gegen Entspannung:** Die Blicksteuerung ist schneller, verlangt aber Kalibrierung, Fixieren und einen ruhigen Kopf. Der Abtastmodus ist langsamer, aber entspannter (B14). Für erschöpfte Patientinnen und Patienten zählt die Entspannung womöglich mehr als das Tempo.
- **Bewegungsfreiheit gegen Genauigkeit:** Die Blicksteuerung braucht einen ruhigen Kopf. Für Patientinnen und Patienten im Bett ist das schwer einzuhalten.

### Grenzen der bisherigen Erkenntnisse

- nur eine Testperson, Selbsttest durch das Projektteam
- nur sitzend am Laptop, nicht liegend wie auf der Intensivstation
- Kennwerte (Abweichung, Dauer, Ermüdung) noch nicht systematisch erhoben
- die Gruppen-Variante (M9) ist noch nicht getestet

### Nächste Schritte

1. Tests mit Kolleginnen und Kollegen nach der Testanleitung, mit Protokoll und Rückmeldevorlage.
2. Vergleich «6 Felder» gegen «2 Gruppen à 3»: Fehlwahlen, Dauer pro Meldung, Augenmüdigkeit.
3. Kennwerte der Kalibrierung (gesamt, horizontal, vertikal) systematisch sammeln, um B3 und B13 zu belegen.
4. Ein Test liegend oder halb liegend.

---

# Detailprotokoll der Befunde und Massnahmen

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
- **Verworfene Option:** Zurück und Abbrechen an die Seiten statt nach unten. Im Team verworfen, weil diese Funktionen nach der eigentlichen Auswahl unten erwartet werden und seitlich mit den Beschwerden vermischt würden. Gewählt wurde stattdessen M9.

### M8 – Obere Kante dazunehmen (aus B11)

- **Befund B11:** Nach M7 war die **obere** Reihe schwieriger zu wählen. Vorher war es die untere.
- **Erklärung:** Die Regression von WebGazer staucht Schätzungen zur Mitte hin. Liegen die äussersten Kalibrierpunkte nur auf den Feldmitten, fehlt der Zug nach oben, und ein Blick nach oben landet zu tief.
- **Massnahme:** Je eine Punktreihe auf dem oberen Rand des Bereichs, auf der oberen Reihe, auf der unteren Reihe und auf Zurück/Abbrechen (4 × 3 Punkte plus 1 Mittelpunkt).
- **Folgerung für das Design:** Mit drei Ebenen übereinander (2 Beschwerdereihen plus Zurück/Abbrechen) und je etwa 20–25 % Höhe liegt die vertikale Genauigkeit (11–16 %) an der Grenze. Welche Reihe schwierig ist, verschiebt sich mit der Kalibrierung. Robuster ist ein Layout mit nur einer Auswahlreihe, siehe M9.

### M9 – Beschwerden in zwei Gruppen (aus B3, B10, B11)

- **Befund B12:** Bei drei Ebenen übereinander (zwei Beschwerdereihen plus Zurück/Abbrechen) verschiebt sich die schwierige Reihe je nach Kalibrierung. Mit 3 Feldern in einer Reihe klappt die Auswahl besser (B4, B6).
- **Idee aus dem Team:** Zwei Hauptgruppen.
- **Massnahme, neuer Ablauf:**
  1. «Was haben Sie?» mit zwei grossen Feldern nebeneinander: **Körper (Schmerzen, Atemnot, Übelkeit)** und **Bedürfnisse (Durst, Hunger, Unbequeme Lage)**.
  2. «Was genau?» mit den drei Beschwerden der Gruppe nebeneinander.
- **Zurück:** von der Beschwerde zur Gruppe, aus «Wie stark?» zurück zur Beschwerde in ihrer Gruppe.
- **Folge:** Es gibt nirgends mehr zwei Auswahlreihen übereinander, nur noch eine Auswahlreihe plus Zurück/Abbrechen. Das ganze System folgt jetzt einem Muster: erst grob wählen, dann genau, mit höchstens drei Feldern nebeneinander.
- **Preis:** ein langes Blinzeln mehr pro Meldung (vgl. B8, Augenermüdung), auch für Atemnot.
- **Vergleichbarkeit:** Ein Schalter «Beschwerden: 2 Gruppen à 3 / 6 Felder» in der Steuerung erlaubt den Vergleich. Zu messen sind Fehlwahlen, Dauer pro Meldung und Augenmüdigkeit. Das gewählte Layout steht im Protokoll.

### B13 – Genauigkeit schwankt zwischen Sitzungen

- **Befund:** Am zweiten Testtag war die Kalibrierung bei derselben Person, demselben Gerät und demselben Verfahren deutlich schlechter als am Vortag. Laut Ergebnisanzeige lagen die Fehler bei etwa 20–25 %, in verschiedene Richtungen, also keine einfache Verschiebung.
- **Mögliche Ursachen (ungeprüft):** anderes Licht, andere Sitzposition oder anderer Kamerawinkel, müde Augen (vgl. B8), Kopfbewegung während der Kalibrierung, Zufall bei nur 3 Kontrollpunkten.
- **Folgerung für das Design:** Eine einmalige Kalibrierung reicht nicht. Vor jeder Nutzung neu kalibrieren, Ergebnis prüfen (Übernehmen / Neu kalibrieren), bei Bedarf C oder Abtastmodus. Auf der Intensivstation ist mit noch stärkeren Schwankungen zu rechnen: Licht, Lagerung, Erschöpfung.

### B14 – Abtastmodus wirkt entspannter als die Blicksteuerung

- **Befund:** Im Selbsttest wirkte der Abtastmodus deutlich entspannter und angenehmer als die Steuerung mit dem Blick.
- **Mögliche Gründe:**
  - keine Kalibrierung und keine Schwankung zwischen Sitzungen (B13)
  - kein aktives Fixieren, also vermutlich weniger Augenermüdung (B8)
  - keine Probleme mit vertikaler Ungenauigkeit (B3, B10–B12)
  - die Person muss nur im richtigen Moment blinzeln, nicht aktiv steuern
- **Preis:** Es ist langsamer. Bei 2 s pro Feld wartet man je nach Position bis zu etwa 10 s pro Schritt. Durch die zweistufige Auswahl mit wenigen Feldern (M1, M9) bleibt die Wartezeit aber begrenzt.
- **Folgerung für das Design:** Den Abtastmodus nicht nur als Notlösung bei Gesichtsverlust behandeln, sondern als **gleichwertige Bedienart** prüfen, eventuell als Standard für erschöpfte Personen. Denkbar ist auch eine Kombination: Abtasten als Grundmodus, Blick als schnellere Option für Personen, bei denen er gut funktioniert.
- **Zu prüfen:** Vergleich Blick gegen Abtasten bei denselben Aufgaben. Gemessen werden Dauer, Fehlwahlen, Augenmüdigkeit (0–10) und welche Bedienart die Person bevorzugt. Wichtig ist auch, ob 2 s pro Feld passen oder zu schnell bzw. zu langsam sind.

## Kennwerte für den nächsten Test (bitte eintragen)

| Durchgang | Abweichung gesamt | horizontal | vertikal | nach Korrektur | Bemerkung (Licht, Brille, Abstand) |
|---|---|---|---|---|---|
| 1 | | | | | |
| 2 | | | | | |

Die Werte stehen nach jeder Kalibrierung unter «Kamera» und im exportierten Protokoll.

## Offene Fragen für den nächsten Test

1. Werden die drei Bereichsfelder mit dem Blick zuverlässig getroffen? Und die 5 Zahlen bei «Leicht»? Falls nicht: «Leicht» teilen (0–2 / 3–4) oder 0 als eigenes Feld «keine».
2. Lassen sich «Zurück» und «Abbrechen» unter der einen Auswahlreihe zuverlässig treffen?
3. Ist die vertikale Abweichung in den Messwerten tatsächlich grösser als die horizontale (B3)?
4. Helfen die Farben oder lenken sie ab? Wirkt Rot für «Stark» alarmierend?
5. **Augenermüdung (B8) messen:** Nach jedem Durchgang die Ermüdung erfragen, zum Beispiel auf einer Skala von 0 bis 10 («Wie müde sind Ihre Augen?»), und notieren, nach wie vielen Meldungen sie spürbar wird. Wie viele lange Blinzeln und wie viel Zeit eine Meldung braucht, steht im exportierten Protokoll (Bilanz pro Durchgang).
6. **Massnahmen gegen Ermüdung vergleichen:** kürzere Mindestdauer für langes Blinzeln (zum Beispiel 600 statt 800 ms), weniger Schritte pro Meldung, dunkler Modus gegen Blendung, Kalibrierung mit 9 statt 13 Punkten, Pausen zwischen den Durchgängen.
7. Wie lange dauert ein ganzer Durchgang von «Ruhe» bis «Gesendet» mit «6 Felder» im Vergleich zu «2 Gruppen à 3»? Das lässt sich aus den Zeitstempeln im Protokoll ablesen.
9. **Blick gegen Abtasten (B14):** Welche Bedienart bevorzugen die Testpersonen? Wie unterscheiden sich Dauer, Fehlwahlen und Augenmüdigkeit? Passt das Tempo von 2 s pro Feld?
8. Sind die Gruppennamen «Körper» und «Bedürfnisse» verständlich? Findet man die gesuchte Beschwerde auf Anhieb in der richtigen Gruppe?
