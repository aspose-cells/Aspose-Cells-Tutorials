---
category: general
date: 2026-06-08
description: Aggiungi un menu contestuale personalizzato a GridJs ed esporta la griglia
  in CSV con un blob di file CSV scaricabile. Segui questo tutorial passo‑passo per
  un esempio completamente funzionante.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: it
og_description: Aggiungi un menu contestuale personalizzato a GridJs ed esporta la
  griglia in CSV con un blob di file CSV scaricabile. Scopri l'implementazione completa
  in meno di 10 minuti.
og_title: Aggiungi un menu contestuale personalizzato a GridJs – Guida completa
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
title: Aggiungi un menu contestuale personalizzato a GridJs – Guida completa
url: /it/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungi un menu contestuale personalizzato a GridJs – Guida completa

Vuoi **aggiungere un menu contestuale personalizzato** a un componente GridJs? In questo tutorial ti guideremo passo passo, e ti mostreremo come **esportare la griglia in CSV** usando un **download CSV file blob**. Che tu stia costruendo un rapido pannello di amministrazione o una dashboard di reporting completa, un menu con click destro che permette agli utenti di estrarre i dati in CSV può essere un vero aumento di produttività.

Copriamo tutto ciò di cui hai bisogno: la parte Python con Flask, il gestore JavaScript che crea il Blob, e l'HTML/JS che GridJs genera. Alla fine avrai un esempio autonomo che potrai inserire in qualsiasi progetto.

---

## Cosa ti servirà

- **Python 3.9+** e **Flask** installati (`pip install flask`).
- Il wrapper Python **gridjs** (o direttamente la libreria JavaScript) – per questa guida assumiamo un leggero wrapper Python che rispecchia l'API JavaScript.
- Una conoscenza di base di **async JavaScript** (`fetch`, `Promise`) – ma non preoccuparti, spiegheremo ogni riga.
- Un editor a tua scelta (VS Code, PyCharm, o anche un semplice editor di testo andrà bene).

Tutto qui. Nessun tool di build front‑end aggiuntivo, nessuna danza con Node npm. Solo Flask semplice che serve l'HTML generato da GridJs.

---

## Aggiungi un menu contestuale personalizzato a GridJs

La prima cosa da fare è dire a GridJs che desideri un menu contestuale personalizzato. Per impostazione predefinita GridJs fornisce un set minimale (copia, incolla, ecc.), ma puoi sostituirlo completamente.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Perché è importante:**  
Impostare `CustomContextMenu` sostituisce l'elenco predefinito con quello fornito. La stringa `"Export CSV"` è solo un'etichetta – il vero lavoro avviene quando l'utente la clicca, cosa che collegheremo nel passo successivo.

> *Consiglio:* Mantieni l'elenco breve. Un menu contestuale ingombrante vanifica lo scopo delle azioni rapide.

---

## Esporta la griglia in CSV con un download Blob

Ora che l'elemento del menu esiste, ci serve un gestore JavaScript che comunichi con il server, recuperi il CSV, lo trasformi in un **Blob** e forzi il download. È qui che compare la frase **download CSV file blob**.

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

### Analisi del gestore

| Riga | Cosa fa |
|------|---------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Chiama una route Flask (`/export/csv`) passando il nome del foglio come stringa di query. |
| `.then(r => r.blob())` | Converte la risposta HTTP in un **Blob** – essenzialmente un contenitore binario per i dati CSV. |
| `URL.createObjectURL(b)` | Genera un URL temporaneo che il browser può trattare come un file. |
| `a.download = cell.sheetName + ".csv"` | Imposta il nome del file che l'utente vedrà nella finestra di download. |
| `a.click()` | Clicca programmaticamente l'ancora nascosta, facendo avviare il download del Blob da parte del browser. |

> **Perché usare un Blob?**  
> I browser non possono scaricare direttamente testo grezzo restituito da `fetch` senza trasformarlo in qualcosa di simile a un file. L'astuzia del Blob‑URL è il metodo più affidabile e cross‑browser per attivare un **download CSV file blob** senza ricaricare la pagina.

---

## Configurare il backend Flask

Il gestore front‑end si aspetta un endpoint su `/export/csv`. Ecco una vista Flask minimale che prende il nome del foglio, estrae i dati dalla cartella di lavoro e restituisce un CSV in streaming.

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

### Punti chiave

- **`io.StringIO`** ci permette di costruire il CSV in memoria senza toccare il filesystem.  
- **`Content‑Disposition`** indica al browser che il file è un allegato e suggerisce un nome file. Anche se il front‑end imposta `a.download`, averlo lato server fornisce un fallback per client non‑JS.  
- La route è deliberatamente semplice; in seguito potrai aggiungere autenticazione, controlli di permesso o streaming per dataset di grandi dimensioni.

---

## Rendering della griglia sul client

Con il menu contestuale e il backend pronti, l'ultimo pezzo è renderizzare il componente GridJs e inviare l'HTML/JS al browser.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

In una view Flask tipicamente faresti:

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

Quando la pagina si carica, GridJs costruisce la tabella, inietta il menu contestuale personalizzato, e il gestore JavaScript definito in precedenza è pronto a essere attivato. Fai click destro su qualsiasi cella, scegli **Export CSV**, e osserva il browser scaricare un file con il nome del foglio.

---

## Esempio completo funzionante (Tutti i file)

Di seguito trovi il codice completo e funzionante che puoi copiare‑incollare in una nuova cartella. Installa Flask (`pip install flask`) ed esegui `python app.py`.

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


## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Carica file CSV con parser personalizzati Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Esporta CSV Codice Java](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Esporta Excel CSV righe vuote Aspose Cells .NET](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}