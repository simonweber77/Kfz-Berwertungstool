# Kfz-Bewertungstool – WBW-Marktrecherche & Sammel-PDF

Einzelne HTML-Datei (`index.html`), läuft im Browser, keine Installation. Daten verlassen den Rechner nicht.

## Ablauf
1. **Fall & Bewertungsfahrzeug** – Schadennummer, EZ, km, Stichtag, APS-Treffer. Optional *DAT-PDF einlesen*.
2. **Inserat-PDFs** in das Feld ziehen – Preis/EZ/km werden vorbefüllt (gelb = prüfen).
3. **Vorschäden** einzeln erfassen oder „keine erkennbar“ anhaken.
4. **Prüfliste** oben abarbeiten (Leitfaden I/2026: Kap. 3 Pkt. 11, 27, 29a; Kap. 4 Pkt. 1).
5. **Sammel-PDF erstellen** → Deckblatt + APS-Auszug + alle Inserate mit Beilagen-Stempel → weDAT® Zusatzdokumente.

*Fall speichern* sichert alles inkl. PDFs als `.json`; *Fall laden* stellt ihn wieder her.

## Methodik
Rechenkern identisch zur Marktanalyse der RSG-SV-Toolbox (Freitag, SV 3/2014):
Wunschpreisabzug 5 %, Privataufschlag 10 %, Alter 0,5 %/Monat (Deckel ±10 %),
km 0,4 % (> 100 % Abweichung 0,65 %) bzw. 0,2 % je 1.000 km, Δ = Bewertungs- − Vergleichsfahrzeug.
Ergänzt um Ausstattungsdifferenz je Inserat, optionale APS-Gewichtung (mit Begründungspflicht) und Rundung auf 10 € (Kap. 3 Pkt. 29a).

## Integration in die SV-Toolbox
CSS ist unter `#wbw-app`, JS im Namensraum `window.WBW` gekapselt; Design-Tokens `--rsg-*` kommen dann aus der Toolbox.
Die Toolbox-CSP erlaubt keine CDNs: pdf-lib, jsPDF und jspdf-autotable müssen eingebettet werden (pdf.js ist dort vorhanden).

## SV-Toolbox (Ordner `toolbox/`)
`toolbox/SV-Toolbox.html` = Ihre RSG-SV-Toolbox mit folgenden Ergänzungen im Bereich **Marktrecherche**:
- **Schieber „Rundung WBW“** (Karte „Fall & Stichtag“): 10 € oder 100 €. Neue Fälle: 10 € (Leitfaden Kap. 3 Pkt. 29a). Bereits gespeicherte Fälle behalten 100 €.
- **Feld „APS-Treffer“**: Bei weniger als 4 Treffern verlangt „Was fehlt noch?“ mindestens ein Vergleichsfahrzeug mit Beleg (Leitfaden Kap. 4 Pkt. 1).
- **Rundung auch ohne WBW-Endberechnung**: Der Wert „Wiederbeschaffungswert aus Marktanalyse“ wird jetzt ebenfalls gerundet (vorher stand „gerundet“, der Wert war es aber nicht).
