---
category: general
date: 2026-06-08
description: Fügen Sie ein benutzerdefiniertes Kontextmenü zu GridJs hinzu und exportieren
  Sie das Raster als CSV mit einem herunterladbaren CSV‑Datei‑Blob. Folgen Sie diesem
  Schritt‑für‑Schritt‑Tutorial für ein vollständig funktionierendes Beispiel.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: de
og_description: Füge ein benutzerdefiniertes Kontextmenü zu GridJs hinzu und exportiere
  das Raster als CSV mit einem herunterladbaren CSV‑Datei‑Blob. Lerne die vollständige
  Implementierung in weniger als 10 Minuten.
og_title: Ein benutzerdefiniertes Kontextmenü zu GridJs hinzufügen – Komplettanleitung
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add custom context menu to GridJs and export grid to CSV with a download
    CSV file blob. Follow this step‑by‑step tutorial for a fully working example.
  headline: Add Custom Context Menu to GridJs – Complete Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- Python
- Flask
title: Benutzerdefiniertes Kontextmenü zu GridJs hinzufügen – Komplettanleitung
url: /de/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Benutzerdefiniertes Kontextmenü zu GridJs hinzufügen – Komplettanleitung

Möchten Sie **ein benutzerdefiniertes Kontextmenü** zu einer GridJs‑Komponente hinzufügen? In diesem Tutorial führen wir Sie Schritt für Schritt durch genau das und zeigen Ihnen, wie Sie **die Grid‑Daten als CSV exportieren** können, indem Sie ein **CSV‑Datei‑Blob herunterladen**. Egal, ob Sie ein schnelles Admin‑Panel oder ein vollwertiges Reporting‑Dashboard bauen – ein Rechtsklick‑Menü, das Nutzern ermöglicht, Daten als CSV zu extrahieren, kann die Produktivität erheblich steigern.

Wir decken alles ab, was Sie benötigen: die Python‑Seite mit Flask, den JavaScript‑Handler, der das Blob erzeugt, und das HTML/JS, das GridJs ausgibt. Am Ende haben Sie ein eigenständiges Beispiel, das Sie in jedes Projekt einbinden können.

---

## Was Sie benötigen

Bevor wir loslegen, stellen Sie sicher, dass Sie Folgendes haben:

- **Python 3.9+** und **Flask** installiert (`pip install flask`).
- Den **gridjs**‑Python‑Wrapper (oder die JavaScript‑Bibliothek direkt) – für diese Anleitung gehen wir von einem dünnen Python‑Wrapper aus, der die JavaScript‑API spiegelt.
- Grundlegendes Verständnis von **async JavaScript** (`fetch`, `Promise`) – aber keine Sorge, wir erklären jede Zeile.
- Einen Editor Ihrer Wahl (VS Code, PyCharm oder sogar einen einfachen Texteditor).

Das war’s. Keine zusätzlichen Front‑End‑Build‑Tools, kein Node‑npm‑Tanz. Einfach Flask, das das HTML liefert, das GridJs erzeugt.

---

## Benutzerdefiniertes Kontextmenü zu GridJs hinzufügen

Das Erste, was Sie tun müssen, ist GridJs mitzuteilen, dass Sie ein benutzerdefiniertes Rechtsklick‑Menü wünschen. Standardmäßig liefert GridJs ein minimales Set (Kopieren, Einfügen usw.), aber Sie können es komplett ersetzen.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Warum das wichtig ist:**  
Durch das Setzen von `CustomContextMenu` ersetzen Sie die Standardliste durch die von Ihnen bereitgestellte. Der String `"Export CSV"` ist nur ein Label – die eigentliche Arbeit passiert, wenn der Nutzer darauf klickt, was wir im nächsten Schritt verbinden.

> *Profi‑Tipp:* Halten Sie die Liste kurz. Ein überladenes Kontextmenü verfehlt den Zweck schneller Aktionen.

---

## Grid als CSV mit einem Blob‑Download exportieren

Jetzt, wo das Menüelement existiert, benötigen wir einen JavaScript‑Handler, der mit dem Server kommuniziert, das CSV abruft, es in ein **Blob** verwandelt und den Download auslöst. Hier kommt der Ausdruck **download CSV file blob** zum Einsatz.

```python
# Step 4: Attach a JavaScript handler that runs when "Export CSV" is chosen.
#         The handler sends an AJAX request to a server endpoint,
#         receives the CSV file as a Blob, and triggers a download.
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""
```

### Aufschlüsselung des Handlers

| Zeile | Was es tut |
|------|------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Ruft eine Flask‑Route (`/export/csv`) auf und übergibt den Blattnamen als Query‑String. |
| `.then(r => r.blob())` | Wandelt die HTTP‑Antwort in ein **Blob** um – im Wesentlichen ein binärer Container für die CSV‑Daten. |
| `URL.createObjectURL(b)` | Erzeugt eine temporäre URL, die der Browser wie eine Datei behandeln kann. |
| `a.download = cell.sheetName + ".csv"` | Setzt den Dateinamen, den der Nutzer im Download‑Dialog sieht. |
| `a.click()` | Simuliert einen Klick auf das versteckte Anker‑Element und veranlasst den Browser, das Blob herunterzuladen. |

> **Warum ein Blob verwenden?**  
> Browser können nicht direkt rohen Text, der von `fetch` zurückkommt, herunterladen, ohne ihn in etwas Datei‑ähnliches zu verwandeln. Der Blob‑URL‑Trick ist die zuverlässigste, browserübergreifende Methode, um einen **download CSV file blob** auszulösen, ohne die Seite neu zu laden.

---

## Flask‑Backend einrichten

Der Front‑End‑Handler erwartet einen Endpunkt unter `/export/csv`. Hier ein minimaler Flask‑View, der den Blattnamen entgegennimmt, die Daten aus der Arbeitsmappe holt und ein CSV zurückstreamt.

```python
from flask import Flask, request, Response
import csv
import io

app = Flask(__name__)

# Assume `workbook` is a global object we created earlier
# (in a real app you’d probably fetch it from a database or session)
@app.route('/export/csv')
def export_csv():
    sheet_name = request.args.get('sheet', 'default')
    # Retrieve the sheet data – this is pseudo‑code; replace with your actual API
    sheet = workbook.get_sheet(sheet_name)

    # Convert rows to CSV in memory
    output = io.StringIO()
    writer = csv.writer(output)
    writer.writerow(sheet.headers)          # Header row
    writer.writerows(sheet.rows)            # Data rows

    # Create a Flask response with the correct MIME type
    csv_bytes = output.getvalue().encode('utf-8')
    return Response(
        csv_bytes,
        mimetype='text/csv',
        headers={'Content-Disposition': f'attachment;filename={sheet_name}.csv'}
    )
```

### Wichtige Punkte

- **`io.StringIO`** ermöglicht es uns, das CSV im Speicher zu erzeugen, ohne das Dateisystem zu berühren.
- **`Content‑Disposition`** teilt dem Browser mit, dass die Datei ein Anhang ist, und schlägt einen Dateinamen vor. Auch wenn das Front‑End bereits `a.download` setzt, bietet dies eine Rückfallebene für nicht‑JS‑Clients.
- Die Route ist bewusst einfach gehalten; später können Sie Authentifizierung, Berechtigungsprüfungen oder Streaming für sehr große Datensätze hinzufügen.

---

## Grid auf dem Client rendern

Mit dem Kontextmenü und dem Backend bereit, fehlt nur noch das Rendern der GridJs‑Komponente und das Ausliefern von HTML/JS an den Browser.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

In einem Flask‑View würde das typischerweise so aussehen:

```python
@app.route('/')
def index():
    html_output = grid_js.Render()
    return f"""
    <!doctype html>
    <html>
    <head>
        <title>Grid with Custom Context Menu</title>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
    </head>
    <body>
        {html_output}
    </body>
    </html>
    """
```

Wenn die Seite geladen wird, baut GridJs die Tabelle, fügt das benutzerdefinierte Kontextmenü ein, und der zuvor definierte JavaScript‑Handler steht bereit. Rechtsklicken Sie auf eine Zelle, wählen Sie **Export CSV**, und der Browser lädt eine Datei herunter, die nach dem Blatt benannt ist.

---

## Vollständiges funktionierendes Beispiel (Alle Dateien)

Unten finden Sie den kompletten, ausführbaren Code, den Sie in einen neuen Ordner kopieren‑und‑einfügen können. Installieren Sie Flask (`pip install flask`) und führen Sie `python app.py` aus.

**`app.py`**

```python
from flask import Flask, request, Response
import csv, io

# Mock classes to simulate the GridJs wrapper – replace with the real library
class Workbook:
    def __init__(self):
        self.sheets = {"Sheet1": Sheet()}
    def get_sheet(self, name):
        return self.sheets.get(name, self.sheets["Sheet1"])

class Sheet:
    def __init__(self):
        self.headers = ["ID", "Name", "Score"]
        self.rows = [
            [1, "Alice", 85],
            [2, "Bob", 92],
            [3, "Charlie", 78],
        ]

class GridJs:
    def __init__(self, workbook):
        self.workbook = workbook
        self.CustomContextMenu = []
        self.CustomContextMenuHandler = ""
    def Render(self):
        # Very simplified HTML – real GridJs would generate a lot more
        return f'''
        <div id="grid"></div>
        <script>
            const grid = new gridjs.Grid({{
                columns: {self.workbook.get_sheet("Sheet1").headers},
                data: {self.workbook.get_sheet("Sheet1").rows},
                search: true,
                pagination: true,
                customContextMenu: {self.CustomContextMenu},
                customContextMenuHandler: {self.CustomContextMenuHandler}
            }}).render(document.getElementById("grid"));
        </script>
        '''

app = Flask(__name__)

# Initialise workbook and grid
workbook = Workbook()
grid_js = GridJs(workbook)

# ==== Step 3: Custom context menu ====
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]

# ==== Step 4: Handler that downloads a CSV blob ====
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""

@app.route('/')
def index():
    html_output = grid_js.Render()
    return f'''
    <!doctype html>
    <html>
    <head>


## Was Sie als Nächstes lernen sollten


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Csv‑Dateien mit benutzerdefinierten Parsern laden – Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Csv‑Export Java‑Code](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Excel‑Csv‑Export – Leere Zeilen – Aspose Cells .NET](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}