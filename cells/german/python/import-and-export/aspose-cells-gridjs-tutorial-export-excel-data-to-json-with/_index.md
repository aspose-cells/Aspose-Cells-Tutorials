---
category: general
date: 2026-07-03
description: Aspose Cells GridJs‑Tutorial, das zeigt, wie man Excel‑Daten als JSON
  exportiert und ein Arbeitsblatt effizient mit Lazy Loading in JSON exportiert.
draft: false
keywords:
- aspose cells gridjs tutorial
- export excel data json
- export worksheet to json
language: de
og_description: Das Aspose Cells GridJs‑Tutorial erklärt, wie man Excel‑Daten in JSON
  exportiert und ein Arbeitsblatt mit Lazy Loading für große Tabellenkalkulationen
  in JSON exportiert.
og_title: Aspose Cells GridJs‑Tutorial – Excel‑Daten nach JSON exportieren
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  headline: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  type: TechArticle
- description: Aspose Cells GridJs tutorial showing how to export Excel data JSON
    and export worksheet to JSON efficiently using lazy loading.
  name: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed locally. - `asposecells` package (you can `pip
      install aspose-cells`). - A sizeable Excel file (e.g., `large-data.xlsx`) placed
      in a known directory. - Basic familiarity with Python and web development concepts.'
  - name: Exporting a specific worksheet
    text: 'The example above always uses the first worksheet (`Worksheets[0]`). To
      export a different sheet, simply change the index or use the sheet name:'
  - name: Changing the chunk size for massive files
    text: For files with millions of rows, a chunk size of 500 may still be too small,
      causing many round‑trips. You can increase it to 2000 or more, but remember
      that larger chunks consume more bandwidth per request.
  - name: Exporting to a stream instead of a file
    text: 'If your API returns the JSON directly, you don’t need to write to disk:'
  - name: Handling formulas and formatting
    text: 'By default, `ExportGridJsJson` includes the calculated values of formulas.
      If you need raw formulas instead, set:'
  type: HowTo
tags:
- Aspose.Cells
- Python
- GridJs
- JSON export
title: Aspose Cells GridJs‑Tutorial – Excel‑Daten in JSON exportieren mit Lazy Loading
url: /de/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells GridJs Tutorial – Excel‑Daten als JSON exportieren mit Lazy Loading

Haben Sie sich jemals gefragt, wie man **Excel‑Daten als JSON** aus einer riesigen Tabelle exportiert, ohne den Browser zu überlasten? In diesem Aspose Cells GridJs Tutorial führen wir Sie durch eine komplette, sofort einsatzbereite Lösung, die es Ihnen ermöglicht, **ein Arbeitsblatt als JSON zu exportieren** mittels Lazy Loading, sodass nur die benötigten Zeilen bei Bedarf abgerufen werden.

Wenn Sie mit riesigen `.xlsx`‑Dateien zu kämpfen haben und die Client‑Seite immer wieder einfriert, sind Sie nicht allein. Die gute Nachricht? Der hier vorgestellte Ansatz ist leichtgewichtig und skalierbar und lässt sich in jedes Python‑Projekt integrieren, das bereits die Aspose.Cells‑Bibliothek verwendet.

## Was dieser Leitfaden abdeckt

In den nächsten Minuten lernen Sie:

1. Ein großes Workbook mit Aspose.Cells zu laden.  
2. GridJs Lazy Loading zu aktivieren, sodass der Server Zeilen in Chunks streamt.  
3. Die GridJs‑Konfiguration in eine JSON‑Datei zu exportieren, die das Front‑End konsumieren kann.  
4. Die Chunk‑Größe für optimale Performance anzupassen.  
5. Die Ausgabe zu überprüfen und sie in eine einfache HTML‑Seite zu integrieren.

Keine externen Services, keine versteckte Magie – nur reines Python und die Aspose.Cells‑API. Am Ende haben Sie eine **komplette Export‑Worksheet‑to‑JSON**‑Pipeline, die Sie für Dashboards, Reporting‑Tools oder jede Daten‑Grid‑Komponente anpassen können.

### Voraussetzungen

- Python 3.8+ lokal installiert.  
- `asposecells`‑Paket (Sie können `pip install aspose-cells` ausführen).  
- Eine umfangreiche Excel‑Datei (z. B. `large-data.xlsx`) in einem bekannten Verzeichnis.  
- Grundlegende Kenntnisse in Python und Web‑Entwicklung.

Falls Ihnen etwas davon unbekannt ist, keine Panik – jeder Schritt enthält eine kurze „Warum‑Erklärung“, sodass Sie die Logik hinter dem Code verstehen.

---

## Schritt 1: Aspose.Cells installieren und importieren

Zuerst benötigen wir die Aspose.Cells‑Bibliothek. Es handelt sich um ein kommerzielles Produkt, aber eine kostenlose Testversion reicht für die Entwicklung.

```bash
pip install aspose-cells
```

Importieren Sie nun die notwendigen Klassen in Ihrem Skript.

```python
# Step 1: Import the Aspose.Cells workbook class
import asposecells
from asposecells import Workbook
```

> **Warum das wichtig ist:** Durch das Importieren von `Workbook` erhalten Sie Zugriff auf die Hochleistungs‑Engine, die Excel‑Dateien direkt in den Speicher liest und damit den langsameren `openpyxl`‑Ansatz umgeht.

## Schritt 2: Das Workbook mit dem großen Datensatz laden

Nachdem die Bibliothek bereitsteht, verweisen Sie sie auf Ihre Excel‑Datei. Der Pfad kann absolut oder relativ sein; stellen Sie nur sicher, dass die Datei existiert.

```python
# Step 2: Load the workbook that contains a large data set
workbook = Workbook("YOUR_DIRECTORY/large-data.xlsx")
```

> **Pro‑Tipp:** Wenn Ihr Workbook größer als ein paar hundert Megabyte ist, sollten Sie das Speicher‑Limit des Python‑Prozesses erhöhen oder einen 64‑Bit‑Interpreter verwenden, um `MemoryError` zu vermeiden.

## Schritt 3: GridJs Lazy Loading aktivieren

GridJs ist Asposes JavaScript‑Grid‑Komponente. Lazy Loading veranlasst den Server, nur einen Teil der Zeilen zu senden – ideal für riesige Tabellen.

```python
# Step 3: Enable lazy loading so the client fetches rows on demand
grid_options = workbook.Worksheets[0].Cells.GridJsOptions
grid_options.LazyLoading = True                 # fetch rows/columns only when needed
grid_options.LazyLoadingChunkSize = 500         # rows per server request
```

> **Warum Lazy Loading?** Ohne Lazy Loading würde das gesamte Arbeitsblatt auf einmal in JSON serialisiert, was leicht die Speichergrenzen des Browsers überschreiten kann. Durch Setzen von `LazyLoadingChunkSize` auf 500 trägt jede Anfrage eine handhabbare Datenmenge.

## Schritt 4: Die GridJs‑Konfiguration nach JSON exportieren

Jetzt lassen wir Aspose das JSON erzeugen, das die Front‑End‑GridJs‑Komponente erwartet. Dies ist der Kern der **export excel data json**‑Operation.

```python
# Step 4: Export the GridJs configuration to a JSON file for the client side
grid_json = workbook.Worksheets[0].Cells.ExportGridJsJson()
```

Die Methode `ExportGridJsJson` liefert ein `bytes`‑Objekt, das die JSON‑Repräsentation des Arbeitsblatts enthält und bereit ist, gespeichert oder gestreamt zu werden.

## Schritt 5: Das JSON in eine Datei schreiben (oder streamen)

Für einen schnellen Test schreiben wir das JSON auf die Festplatte. In einer Produktions‑API würden Sie es direkt von einem Flask/Django‑Endpoint zurückgeben.

```python
# Step 5: Persist the JSON to a file
output_path = "YOUR_DIRECTORY/lazygrid.json"
with open(output_path, "wb") as f:
    f.write(grid_json)

print(f"✅ GridJs JSON exported successfully to {output_path}")
```

> **Was Sie sehen werden:** Das Öffnen von `lazygrid.json` zeigt eine Struktur mit `columns`, `rows` und Paginierungs‑Metadaten. Das `rows`‑Array ist zunächst leer; GridJs fordert den ersten Chunk an, sobald die Seite geladen wird.

## Schritt 6: Das JSON in eine einfache HTML‑Seite einbinden (optional)

Wenn Sie das Grid in Aktion sehen möchten, erstellen Sie eine kleine HTML‑Datei, die GridJs von einem CDN lädt und auf das erzeugte JSON verweist.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Lazy‑Loaded GridJs Demo</title>
    <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
    <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
</head>
<body>
    <div id="wrapper"></div>
    <script>
        // Fetch the lazy‑loaded JSON and initialize GridJs
        fetch('lazygrid.json')
            .then(r => r.json())
            .then(config => {
                new gridjs.Grid({
                    ...config,
                    server: {
                        url: 'lazygrid.json',
                        then: data => data
                    }
                }).render(document.getElementById('wrapper'));
            });
    </script>
</body>
</html>
```

> **Warum das?** Es demonstriert den kompletten Round‑Trip: Python erzeugt das JSON, der Browser holt es ab und GridJs rendert die Daten Chunk‑für‑Chunk. Sie können nun mit verschiedenen `LazyLoadingChunkSize`‑Werten experimentieren, um den optimalen Wert für Ihr Netzwerk zu finden.

## Schritt 7: Verifizieren und Fehlersuche

Führen Sie das Python‑Skript aus:

```bash
python export_lazy_grid.py
```

Sie sollten die Erfolgsmeldung und eine `lazygrid.json`‑Datei sehen. Öffnen Sie die HTML‑Datei im Browser; das Grid sollte sofort die ersten 500 Zeilen anzeigen, mit Paginierungs‑Steuerelementen zum Laden weiterer Daten.

Falls das Grid leer erscheint:

- **Überprüfen Sie die JSON‑Dateigröße** – eine Null‑Byte‑Datei bedeutet meist, dass der Workbook‑Pfad falsch war.  
- **Stellen Sie sicher, dass Lazy Loading aktiviert ist** – das Flag `LazyLoading` muss `True` sein.  
- **Untersuchen Sie die Browser‑Konsole** – CORS‑ oder 404‑Fehler weisen darauf hin, dass das JSON nicht korrekt bereitgestellt wird.

---

## Häufige Variationen und Sonderfälle

### Export eines bestimmten Arbeitsblatts

Im obigen Beispiel wird immer das erste Arbeitsblatt (`Worksheets[0]`) verwendet. Um ein anderes Blatt zu exportieren, ändern Sie einfach den Index oder verwenden Sie den Blattnamen:

```python
sheet = workbook.Worksheets["DataSheet"]   # by name
grid_options = sheet.Cells.GridJsOptions
grid_json = sheet.Cells.ExportGridJsJson()
```

### Chunk‑Größe für massive Dateien anpassen

Bei Dateien mit Millionen von Zeilen kann eine Chunk‑Größe von 500 immer noch zu klein sein und viele Round‑Trips verursachen. Sie können sie auf 2000 oder mehr erhöhen, bedenken Sie jedoch, dass größere Chunks mehr Bandbreite pro Anfrage verbrauchen.

```python
grid_options.LazyLoadingChunkSize = 2000
```

### Export in einen Stream statt in eine Datei

Wenn Ihre API das JSON direkt zurückgibt, müssen Sie es nicht auf die Festplatte schreiben:

```python
from flask import Flask, Response
app = Flask(__name__)

@app.route("/api/gridjson")
def gridjson():
    json_bytes = workbook.Worksheets[0].Cells.ExportGridJsJson()
    return Response(json_bytes, mimetype="application/json")
```

### Umgang mit Formeln und Formatierungen

Standardmäßig beinhaltet `ExportGridJsJson` die berechneten Werte von Formeln. Wenn Sie stattdessen die rohen Formeln benötigen, setzen Sie:

```python
grid_options.ExportFormulas = True
```

---

## Fazit

In diesem **Aspose Cells GridJs Tutorial** haben wir alles behandelt, was Sie benötigen, um **Excel‑Daten als JSON** und **ein Arbeitsblatt als JSON** mit Lazy Loading zu exportieren. Von der Installation von Aspose.Cells, über das Aktivieren von Lazy Loading, das Erzeugen des JSON bis hin zur Einbindung in eine einfache HTML‑Seite – Sie besitzen nun ein Full‑Stack‑Muster, das sich elegant an massive Tabellen anpasst.

Probieren Sie es aus – passen Sie die Chunk‑Größe an, verweisen Sie auf verschiedene Arbeitsblätter oder integrieren Sie den Endpoint in eine Flask‑ oder Django‑App. Die Möglichkeiten sind endlos, und die Performance‑Gewinne sofort spürbar.

Bereit für den nächsten Schritt? Versuchen Sie, Spaltensortierung, benutzerdefinierte Zell‑Renderer oder sogar serverseitige Filter hinzuzufügen, um Ihr GridJs‑Grid wirklich interaktiv zu machen. Wenn Sie auf ein Problem stoßen, hinterlassen Sie einen Kommentar unten; happy coding!


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Features meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Import JSON Data into Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Load CSV & Export to JSON Using Aspose.Cells for .NET&#58; A Comprehensive Guide](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Export Excel Data Using Aspose.Cells .NET&#58; A Complete Guide for Seamless Data Export](/cells/english/net/import-export/export-excel-data-aspose-cells-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}