# Übergabe Routenplanung an Alex

**Projekt:** Routenplanung  
**Aktueller Stand:** v0.14  
**Übergabe:** Josef → Alex  
**Live-Anwendung:** https://joseflab.github.io/Routenplanung/

## Zweck der Anwendung

Die Web-App plant wirtschaftliche Fahrerrouten aus einer unbereinigten Excel- oder CSV-Adressliste. Nicht benötigte Spalten im Import dürfen enthalten bleiben. Standorte können vor der Planung über Checkboxen ein- oder ausgeschlossen werden.

## Typischer Arbeitsablauf

1. Excel- oder CSV-Datei im Bereich **Import** auswählen.
2. Prüfen, ob Straße, Hausnummer, PLZ, Ort und gegebenenfalls **Company_Name** korrekt übernommen wurden.
3. Nicht gefundene oder falsch erkannte Adressen über die angebotene Korrektur bearbeiten.
4. Gewünschte Standorte in der Übersicht angehakt lassen; nicht benötigte Standorte abwählen.
5. Anzahl der Fahrer und die Stoppzeit pro Standort einstellen.
6. Für jeden Fahrer Startzeit, Endzeit, Startdepot und Enddepot festlegen.
7. **Routen planen** auswählen.
8. Routen, Stoppnummern, Kilometer, Fahrzeiten und nicht eingeplante Adressen kontrollieren.
9. Bei Änderungen Checkboxen oder Fahrerangaben anpassen und **Routen neu planen** auswählen.
10. Pro Fahrer kann ein **Google-Maps-Link** zur Navigation geöffnet werden.
11. Mit **Excel erstellen** die Gesamtübersicht und die einzelnen Fahrerblätter exportieren.

## Importdatei

Die Erkennung unterstützt unterschiedliche Bezeichnungen für die wichtigsten Felder:

- Straße
- Hausnummer
- PLZ
- Ort
- Company_Name bzw. Firmenname

Die Datei muss vor dem Import nicht auf diese Spalten reduziert werden. Zusätzliche Daten werden ignoriert.

### Wichtig bei Adressen

- Kleine Schreibfehler können dazu führen, dass eine Adresse nicht eindeutig gefunden wird.
- Erkannte Korrekturvorschläge müssen vor der Tour geprüft werden.
- **Nicht gefundene Adressen dürfen nicht unbemerkt in der fertigen Planung fehlen.**
- Vor dem Export immer die Kartenstatus-Spalte und die Zahl der nicht eingeplanten Adressen kontrollieren.
- Die PLZ und der Ort sollen mit der tatsächlichen Adresse übereinstimmen und nicht nur aus einem Geokodierungs-Treffer übernommen werden.

## Fahrer und Zeitfenster

- Die Fahreranzahl ist einstellbar.
- Jeder Fahrer kann eigene Start- und Endzeiten erhalten.
- Start- und Enddepot können je Fahrer unterschiedlich sein.
- Bei identischen Depots können die Depotwerte übernommen werden.
- Die Planung soll innerhalb der verfügbaren Zeit möglichst viele ausgewählte Stopps einplanen.
- Reicht die verfügbare Zeit nicht aus, werden die übrigen Adressen als **nicht eingeplant** angezeigt.
- Die Stoppzeit je Adresse wird zusätzlich zur Fahrzeit berücksichtigt.

## Kartenansicht

- Jede Fahrerroute erhält eine eigene Darstellung.
- Start und Ende sind gesondert gekennzeichnet.
- Eingeplante Standorte zeigen ihre Stoppnummer direkt auf der Karte.
- Die Nummerierung gilt innerhalb der jeweiligen Fahrertour.
- Die Kartenansicht dient zur Kontrolle der Reihenfolge und auffälliger Umwege.

## Excel-Export

Der Export enthält:

- eine Gesamtübersicht über alle Touren,
- ein eigenes Tabellenblatt pro Fahrer,
- Company_Name, sofern im Import vorhanden,
- Reihenfolge und Adresse der Stopps,
- geplante Zeiten,
- Gesamtfahrzeit und Planzeit,
- Gesamtkilometer pro Tour,
- Google-Maps-Navigationslinks,
- nicht eingeplante Adressen,
- druckfreundliche Fahrerblätter im Querformat.

Vor dem Weitergeben oder Ausdrucken bitte prüfen:

- Sind alle gewünschten Adressen eingeplant?
- Stimmen Fahrer, Depot und Zeitfenster?
- Sind Stoppnummern und Reihenfolge plausibel?
- Stimmen die Gesamtkilometer?
- Sind Company_Name und Adressdaten vollständig?

## Filter und Sortierung

Die Adressübersicht kann nach Straße, Hausnummer, PLZ, Ort, Auswahlstatus und Kartenstatus gefiltert oder sortiert werden. Filter und Sortierung verändern nur die Ansicht. Für die Planung zählt der Status der Checkbox.

## Technischer Aufbau

- Das Projekt besteht derzeit im Wesentlichen aus einer einzelnen Datei: `index.html`.
- Hosting erfolgt über GitHub Pages vom Branch `main`.
- Es gibt keinen eigenen Server und keine Datenbank.
- Import, Planung und Export laufen direkt im Browser.
- Hochgeladene Dateien werden nicht auf einem eigenen Server gespeichert.
- Kartendarstellung: Leaflet / OpenStreetMap
- Adresssuche: öffentliche Nominatim-Schnittstelle
- Straßenrouting: öffentliche OSRM-Schnittstelle
- Excel-Verarbeitung: SheetJS und ExcelJS
- Erfolgreich geokodierte Adressen werden im Browser zwischengespeichert.

## Bekannte Grenzen

- Für Adresssuche, Karte, Routing und Google Maps ist eine Internetverbindung notwendig.
- Öffentliche Geokodierungs- und Routingdienste können zeitweise langsam oder nicht erreichbar sein.
- Die automatische Optimierung ist eine wirtschaftliche Näherung und keine mathematische Garantie für die weltweit kürzeste Route.
- Schreibfehler, falsche PLZ oder mehrdeutige Straßennamen müssen gegebenenfalls manuell korrigiert werden.
- Der lokale Adress-Zwischenspeicher gilt nur für den jeweiligen Browser und das jeweilige Gerät.
- Nach Änderungen an `index.html` kann GitHub Pages einige Minuten benötigen, bis die neue Version sichtbar ist.

## Änderungen am Projekt

Vor jeder Änderung:

1. neue Versionsnummer festlegen,
2. geplanten Umfang kurz mit Josef abstimmen,
3. erst nach Freigabe ändern,
4. Änderung auf `main` veröffentlichen,
5. Live-Seite testen,
6. Versionsnummer und Commit dokumentieren.

## Schnelltest nach einer Änderung

1. Seite neu laden.
2. Eine echte Importdatei laden.
3. Übernahme von Ort, PLZ, Hausnummer und Company_Name prüfen.
4. Mindestens eine Adresse abwählen.
5. Mit einem Fahrer planen.
6. Mit mehreren Fahrern und unterschiedlichen Depots planen.
7. Stoppnummern auf Karte und in Tabelle vergleichen.
8. Google-Maps-Link öffnen.
9. Excel exportieren und Gesamtübersicht sowie Fahrerblätter kontrollieren.
10. Druckvorschau im Querformat prüfen.

## Aktueller Ausgangspunkt

Die Anwendung befindet sich bei **v0.14**. Die Übergabedokumentation wurde als **v0.15** ergänzt; die eigentliche Planungslogik wurde dabei nicht verändert.
