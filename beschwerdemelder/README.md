# Beschwerdemelder

Studienprototyp aus dem Modul Natural User Interfaces (ZHAW). Wache Patientinnen und Patienten auf der Intensivstation, die nicht sprechen und die Hand nicht sicher bewegen können, melden damit eine Beschwerde und deren Stärke. **Mit dem Blick wählen sie ein Feld, ein bewusstes langes Blinzeln bestätigt.**

> **Testprototyp für Gesunde, kein Medizinprodukt.** Nicht für den Einsatz mit echten Patientinnen und Patienten.

Alles steckt in einer einzigen Datei: `Beschwerdemelder_Kamera.html`.

## Start

Chrome erlaubt die Kamera nur, wenn die Seite über einen lokalen Server läuft. Ein Doppelklick auf die Datei reicht dafür nicht.

### Variante A: VS Code mit Live Server (empfohlen unter Windows)

1. Installieren Sie in VS Code die Erweiterung **Live Server** von Ritwick Dey (Erweiterungen: `Ctrl+Shift+X`).
2. Öffnen Sie mit **File → Open Folder…** den Ordner mit der HTML-Datei.
3. Klicken Sie mit der rechten Maustaste auf `Beschwerdemelder_Kamera.html` und wählen Sie **Open with Live Server**.
4. Öffnen Sie in Chrome `http://127.0.0.1:5500/Beschwerdemelder_Kamera.html`.

Live Server lädt die Seite bei jedem Speichern der Datei neu. Das Protokoll geht dabei verloren, exportieren Sie es also vorher.

### Variante B: Python

```bash
python3 -m http.server 8000
```

Dann `http://localhost:8000/Beschwerdemelder_Kamera.html` in Chrome öffnen.

**Internet beim ersten Start:** Die Erkennungsmodelle werden beim ersten Start über das Internet geladen (siehe Technik). Das Kamerabild selbst verlässt den Rechner nie.

## Ablauf

```
Ruhe ──langes Blinzeln──▶ Beschwerde ──▶ Stärke: Bereich ──▶ Stärke: Zahl ──▶ Prüfen ──Senden──▶ Gesendet
 ▲                       (6 Felder)      Leicht 0–4          nur Zahlen des              │
 │                                       Mittel 5–7          Bereichs                    ├─ Zurücknehmen (bis zur Quittung)
 │                                       Stark 8–10                                      ▼
 └────────────────────────────── «Die Pflege kommt» ◀── Pflege quittiert ◀─────────────────┘
```

- **Im Ruhezustand** reagiert das System nicht auf den Blick, nur auf langes Blinzeln.
- **In jedem aktiven Zustand** gibt es «Zurück» und «Abbrechen». **Abbrechen sendet nie etwas.**
- **Auf «Stimmt das?»** ist beim Erscheinen nichts markiert. Gesendet wird nur, wenn «Senden» angeschaut und dann lang geblinzelt wird.
- **Nach dem Senden** kann die Meldung zurückgenommen werden, bis die Pflege quittiert. «Zurücknehmen» ist bewusst nicht vormarkiert und nicht übergross, damit ein langes Blinzeln beim Warten die Meldung nicht versehentlich zurücknimmt.
- **Pflege simuliert:** Für Tests ohne Testleitung quittiert die Pflege automatisch nach 10 s (einstellbar unter «Wizard und Ablauf», abschaltbar). Im Protokoll steht das als «automatisch, simuliert». Mit `Q` quittiert die Testleitung sofort.

## Bedienung

### Erkennung durch die Kamera

1. Klicken Sie auf **Kamera starten**.
2. **Langes Blinzeln:** Die Augen müssen zwischen «Lang ab ms» (Standard 800) und «Max ms» (Standard 3000) geschlossen sein.
   - Ein **hoher Ton** zeigt an, dass die Mindestdauer erreicht ist.
   - Ein **tiefer Ton** heisst «zu lang, wird verworfen».
   - Kurzes Blinzeln wird ignoriert und gezählt.
3. Klicken Sie auf **Blick kalibrieren** (siehe unten). Danach ist «Blick per Kamera» an.
   - Das Feld unter dem Blick wird **gestrichelt** umrandet und nach etwa 0,7 s **fest** markiert.
   - Beginnen sich die Augen zu schliessen, friert der Blickpunkt ein. Ein langes Blinzeln wählt das Feld, das beim Schliessen fest markiert war.
4. **Gesicht nicht erkannt:** Die Seite schaltet automatisch auf Pause («Ich sehe Ihre Augen nicht»), es wird nichts gewählt. Bei der zweiten Pause im Durchgang erscheint der Hinweis, den Abtastmodus anzubieten.

### Wizard-Tasten

Die Tasten funktionieren immer, auch ohne Kamera.

| Taste | Wirkung |
|---|---|
| `Leertaste` | langes Blinzeln (im Vorabtest «Bewusstes Blinzeln»: angesagten Versuch zählen) |
| `← → ↑ ↓` | Markierung bewegen |
| `X` | Blick unklar, Markierung entfernen |
| `P` | Pause ein/aus |
| `A` | Abtastmodus: Felder leuchten alle 2 s nacheinander auf, langes Blinzeln wählt. Braucht keinen Blick. |
| `F` | simulierter Fehler: Markierung springt aufs Nachbarfeld |
| `Q` | Pflege quittiert (sofort; sonst automatisch nach 10 s, falls eingeschaltet) |
| `N` | Pflegeansicht |
| `R` | neuer Durchgang |
| `W` | Steuerung ein/aus (für die Testperson einklappen, dann werden die Felder grösser) |
| `H` | Anleitung |
| `C` | Blick-Mitte nachjustieren |
| `Esc` | Kalibrierung abbrechen bzw. Ergebnis übernehmen |

Ein **Mausklick** auf ein Feld wählt es ebenfalls. Die **Höhe der Steuerung** ziehen Sie mit der Maus an der Leiste darüber. Ein Doppelklick setzt sie zurück.

Die Leiste unten zeigt jederzeit, **was echt erkannt und was simuliert wird**. Daneben schalten Sie den Farbmodus um (Auto, Hell, Dunkel).

### Kalibrierung

1. **Sitzposition:**
   - Abstand **50–70 cm**, das Gesicht füllt ein Drittel bis die Hälfte des Kamerabilds.
   - **Licht von vorn**, kein Fenster im Rücken.
   - Kamera auf Augenhöhe.
   - **Kopf anlehnen** und während der Kalibrierung nur die Augen bewegen.
2. **Kalibrierbereich:** Er legt sich beim Kalibrieren **automatisch auf die Beschwerdefelder** (Häkchen «Bereich automatisch auf die Felder legen»). So entstehen keine Punkte über leeren Flächen wie der Überschrift. Mit **Bereich mit Maus anpassen** lässt er sich von Hand festlegen, dann ist die Automatik aus.
3. **Blick kalibrieren:**
   - Die Seite geht in den Vollbildmodus.
   - Es erscheinen 9 oder 13 Punkte. Schauen Sie auf den kleinen Punkt in der Mitte des Rings, bis der Ring grün wird. Punkte mit zu wenig Messwerten werden automatisch wiederholt.
4. **Kontrolle an 3 neuen Punkten:**
   - Die Seite zeigt Zielpunkt und Schätzung sowie die **mittlere Abweichung in % der Bildschirmgrösse**, gesamt, horizontal und vertikal.
   - Eine systematische Verschiebung wird automatisch korrigiert.
   - Danach **Übernehmen** oder **Neu kalibrieren**.
5. **Während des Tests:** Im Vollbild bleiben. Bei leichter Verschiebung **C** drücken und die Mitte anschauen. Nach einer Änderung der Sitzposition neu kalibrieren.

## Protokoll und Vorabtests

- **Inhalt jeder Zeile:** Durchgang, Zeit im Durchgang, Zeit seit Programmstart, **Quelle** (Kamera = echt erkannt, Wizard, Maus, System) und Ereignis.
  - Simulierte Fehler sind mit `[SIMULIERTER FEHLER]` markiert.
  - Bei `R` und beim Export kommt eine Bilanz pro Durchgang dazu.
- **Export:** «Als Datei speichern» erzeugt eine Textdatei. Ihr Kopf enthält die Einstellungen.
- **Freies Schauen 2 Min:** zählt Fehlauslösungen, also lange Blinzeln, die nicht beabsichtigt waren.
- **Bewusstes Blinzeln:** Die Testleitung drückt bei jedem angesagten Versuch die Leertaste. Am Ende steht die Erkennungsrate im Protokoll.

## Datenschutz

- Kamerabild und Blickdaten werden nur im Browser ausgewertet und **nirgends gespeichert oder gesendet**.
- Es gibt keinen `localStorage`, keine IndexedDB und keine Cookies. Auch die Kalibrierung wird nicht gespeichert, nach dem Neuladen muss neu kalibriert werden.
- Die einzige Datei, die entsteht, ist das Protokoll, das Sie selbst exportieren.
- Über das Netz geladen werden nur Programmcode und Modelle von den unten genannten Quellen.

## Technik

| Zweck | Bibliothek | Quelle |
|---|---|---|
| Langes Blinzeln, Gesicht weg, «Augen offen» | MediaPipe Face Landmarker (`@mediapipe/tasks-vision@0.10.14`, Blendshapes `eyeBlinkLeft/Right`) | cdn.jsdelivr.net, Modell von storage.googleapis.com |
| Blickpunkt | WebGazer.js `3.5.3` (Ridge-Regression auf Augenbildern, Kalman-Filter) | cdn.jsdelivr.net |
| Schrift | Atkinson Hyperlegible | Google Fonts |

**Gemeinsamer Kamerastrom:** In Chrome könnten zwei Bibliotheken auf derselben Seite grundsätzlich beide die Kamera öffnen. Das bringt aber unnötige Last und unter Windows unter Umständen Auflösungskonflikte. Darum öffnet der Prototyp die Kamera **einmal** und übergibt WebGazer denselben Strom (`webgazer.setStaticVideo(stream)`). Das ist im Test nachgewiesen: eine Videospur, beide Bibliotheken laufen.

**Anpassungen an WebGazer:**
- Das Gesichtsmodell wird vom CDN geladen statt relativ zur Seite.
- Das Speichern von Kalibrierdaten ist ausgeschaltet.
- Maus und Klicks trainieren das Modell nicht nach.
- Das Datenfenster der Regression ist von 50 auf 400 Proben vergrössert. Sonst würden bei 13 Punkten die ersten Punkte vergessen.
- WebGazer bekommt nur Proben bei sicher offenen Augen, die Information dazu liefert MediaPipe.

## Bekannte Grenzen

### Wie genau ist Webcam-Blicksteuerung realistisch?

- **Grössenordnung:** Mit einer normalen Laptop-Webcam und WebGazer liegt die Abweichung typischerweise **im Bereich von etwa 10–20 % der Bildschirmbreite**. Bei 60 cm Abstand entspricht das mehreren Zentimetern auf dem Bildschirm. Das ist eine grobe Einordnung, die Werte schwanken stark nach Person, Licht und Kamera. Massgebend ist die gemessene Abweichung aus der eigenen Kontrolle, sie steht im Protokoll.
- **Treffbare Ziele:** Zuverlässig treffbar sind **wenige grosse Felder**, etwa drei nebeneinander. Elf Felder in einer Reihe (Skala 0–10) waren im Selbsttest praktisch nicht bedienbar, darum gibt es die zweistufige Auswahl.
- **Vertikal schlechter:** Vertikal ist die Schätzung meist schlechter als horizontal, weil Lid und Wimpern die Iris verdecken und die Kamera von oben schaut. Die Auswahlen liegen deshalb nebeneinander.
- **Kopfbewegung:** Bewegt sich der Kopf, wird die Schätzung schlechter. WebGazer lernt das Augenbild bei einer bestimmten Kopfhaltung. Nach Umsetzen braucht es Taste C oder eine neue Kalibrierung.
- **Drift:** Mit der Zeit verschiebt sich die Schätzung oft. Taste C korrigiert das.
- **Licht und Brille:** Gegenlicht, wechselndes Licht, Spiegelungen in Brillengläsern und wenig Kontrast im Gesicht bei schwachem Licht verschlechtern die Erkennung.
- **Fenstergrösse:** Die Kalibrierung gilt nur für die Fenstergrösse, in der sie gemacht wurde. Verlassen Sie den Vollbildmodus, erscheint ein Hinweis.

### Weitere Grenzen

- **Liegende Personen:** Getestet wurde nur sitzend am Laptop. Liegend, mit schräger Kamera und anderem Blickwinkel, ist mit schlechteren Werten zu rechnen. Das ist für die Intensivstation die eigentliche Frage.
- **Rechenlast:** Zwei Gesichtsmodelle laufen gleichzeitig. Auf älteren Laptops kann die Blickschätzung stocken. Netzbetrieb hilft.
- **Browser:** Getestet in Chrome. Andere Browser sind möglich, aber ungeprüft.
- **Netz:** Ohne Internet beim Start laden die Modelle nicht. Wizard, Maus, Pflegeansicht und Protokoll funktionieren trotzdem.
- **Pflegeansicht:** Sie ist eine Simulation im selben Fenster, es gibt keine echte Übertragung an ein anderes Gerät.

## Weitere Dateien

- `Meilenstein2_Learnings.md`: Befunde aus den Selbsttests und daraus abgeleitete Änderungen, für den Meilenstein-2-Report.
