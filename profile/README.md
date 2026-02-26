# OpenTrace Organisation

OpenTrace ist eine Open-Source-Initiative zur transparenten Darstellung von Produktinformationen. Ziel ist es, Nutzerinnen und Nutzern die Möglichkeit zu geben, Herkunft, Inhaltsstoffe, Transportwege und CO2-Emissionen von Konsumgütern nachzuvollziehen und dadurch bewusstere Entscheidungen zu treffen.

Die GitHub-Organisation besteht aus drei miteinander verbundenen Projekten:

* [opentrace](https://github.com/TheTrueOrigin/opentrace) (Mobile App)
* [opentrace-database](github.com/TheTrueOrigin/opentrace-database) (Datenbank)
* [opentrace-backend](github.com/TheTrueOrigin/opentrace-backend) (API)

Alle Komponenten sind voneinander getrennt entwickelt, greifen jedoch logisch ineinander.

---

## Architekturüberblick

Die OpenTrace App ruft Produktinformationen über das Backend ab.
Das Backend stellt die Daten aus der OpenTrace-Datenbank als API bereit.
Die Datenbank wird von der Community gepflegt und regelmäßig aktualisiert.

Ablauf:

Mobile App -> Backend API -> Datenbank

Community -> Datenbank -> Backend -> App

---

## [opentrace](https://github.com/TheTrueOrigin/opentrace) (Mobile App)

Die OpenTrace App ist eine React Native Anwendung auf Basis von Expo. Sie ermöglicht das Abrufen von Produktinformationen per Barcode oder Namenssuche.

Funktionen:

* Anzeige von Herkunft und Herstellungsort
* Darstellung von Transportwegen und berechneten CO2-Emissionen
* Anzeige von Nährwerten
* Übersicht über Bestandteile, Allergene und Labels
* Abruf der Daten über die OpenTrace Backend API

### Voraussetzungen

* Node.js
* npm

Pakete installieren:

```bash
npm install
```

Development starten:

```bash
npx expo start
```

Builds für Android können über Expo EAS erstellt werden, es ist in den Releases auch eine fertige apk-Datei enthalten.
Für iOS Standalone Builds wird macOS mit XCode benötigt.

Weitere Details zum Build-Prozess befinden sich im jeweiligen Repository.

## [opentrace-database](github.com/TheTrueOrigin/opentrace-database) (Datenbank)

Die OpenTrace-Datenbank ist ein strukturiertes, versioniertes Open-Source-Datenprojekt. Sie enthält Informationen zu:

* Produkten
* Unternehmen
* Bestandteilen
* Allergenen
* Labels

Ziel ist es, nachvollziehbare und überprüfbare Produktdaten bereitzustellen, die von der Community gepflegt werden.

Die Daten werden in strukturierter Textform erfasst und mit einem Python-Skript in eine SQLite-Datenbank überführt.

Datenbank erstellen:

```bash
python build.py
```

Ergebnis ist die Datei `database.db`.

### CO2-Berechnung

Die Emission eines Produkts wird nach folgender Formel berechnet:

Emission = Distanz × Gewicht × Emissionsfaktor

Es werden unterschiedliche Emissionsfaktoren je nach Transporttyp verwendet, unter anderem für Flug, LKW, Zug, Schiff und elektrische Transporte.

### Beitrag zur Datenbank

Neue Produkte, Unternehmen oder Bestandteile können über Pull Requests ergänzt werden.
Die genauen Struktur- und Formatvorgaben sind im Repository unter den dortigen Guidelines beschrieben.

## [opentrace-backend](github.com/TheTrueOrigin/opentrace-backend) (API)

Das OpenTrace Backend stellt die aktuelle Version der Datenbank als REST API bereit. Es basiert auf FastAPI und dient als Schnittstelle zwischen App und Datenbank.

Das Backend stellt sicher, dass die App stets auf die aktuellsten Daten zugreift.

### Endpunkte

* GET /produkt/id/{id}
* GET /produkt/barcode/{barcode}
* GET /produkt/name/{name}

Die API liefert strukturierte JSON-Antworten mit Produktdetails, Unternehmensinformationen, Bestandteilen, Nährwerten, Labels und berechneten Emissionen.

### Server starten

Abhängigkeiten installieren:

```bash
pip install -r requirements.txt
```

Server starten:

```bash
python -m fastapi run endpoints.py
```

Standardmäßig läuft der Server auf Port 8000.

## Ziel der Organisation

OpenTrace soll eine offene, transparente und gemeinschaftlich gepflegte Infrastruktur für nachhaltige Produktinformationen bereitstellen.

Durch die Trennung in App, Backend und Datenbank bleibt das System modular, erweiterbar und unabhängig weiterentwickelbar.

Beiträge aus der Community sind ausdrücklich erwünscht.
