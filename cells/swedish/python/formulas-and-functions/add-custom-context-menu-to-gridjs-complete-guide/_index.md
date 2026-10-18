---
category: general
date: 2026-06-08
description: Lägg till en anpassad snabbmeny i GridJs och exportera rutnätet till
  CSV med en nedladdningsbar CSV‑fil som blob. Följ den här steg‑för‑steg‑handledningen
  för ett fullt fungerande exempel.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: sv
og_description: Lägg till en anpassad kontextmeny i GridJs och exportera rutnätet
  till CSV med en nedladdningsbar CSV‑filblob. Lär dig hela implementeringen på under
  10 minuter.
og_title: Lägg till anpassad kontextmeny i GridJs – Komplett guide
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
title: Lägg till anpassad kontextmeny i GridJs – Komplett guide
url: /sv/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till anpassad kontextmeny i GridJs – Komplett guide

Vill du **lägga till en anpassad kontextmeny** i en GridJs-komponent? I den här handledningen går vi igenom exakt det och visar dig hur du **exporterar ett rutnät till CSV** med en **nedladdnings-CSV-fil-blob**. Oavsett om du bygger ett snabbt admin‑panel eller en fullständig rapporterings‑dashboard, kan en högerklicksmeny som låter användare hämta data som CSV ge en verklig produktivitetsökning.

Vi kommer att gå igenom allt du behöver: Python‑delen med Flask, JavaScript‑hanteraren som skapar Blob‑en, och HTML/JS som GridJs genererar. När du är klar har du ett självständigt exempel som du kan lägga in i vilket projekt som helst.

---

## Vad du behöver

- **Python 3.9+** och **Flask** installerade (`pip install flask`).
- Python‑wrappern **gridjs** (eller JavaScript‑biblioteket direkt) – för den här guiden antar vi en tunn Python‑wrapper som speglar JavaScript‑API‑et.
- En grundläggande förståelse för **async JavaScript** (`fetch`, `Promise`) – men oroa dig inte, vi förklarar varje rad.
- En redigerare du gillar (VS Code, PyCharm eller till och med en enkel textredigerare räcker).

Det är allt. Inga extra front‑end‑byggverktyg, ingen Node npm‑dans. Bara ren Flask som levererar HTML som GridJs genererar.

---

## Lägg till anpassad kontextmeny i GridJs

Det första du måste göra är att tala om för GridJs att du vill ha en anpassad högerklicksmeny. Som standard levereras GridJs med en minimal uppsättning (kopiera, klistra in osv.), men du kan ersätta den helt.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Varför detta är viktigt:**  
Att sätta `CustomContextMenu` ersätter standardlistan med den du tillhandahåller. Strängen `"Export CSV"` är bara en etikett – det egentliga arbetet sker när användaren klickar på den, vilket vi kopplar ihop i nästa steg.

> *Proffstips:* Håll listan kort. En rörig kontextmeny urvinner syftet med snabba åtgärder.

---

## Exportera rutnät till CSV med en Blob‑nedladdning

Nu när menyalternativet finns behöver vi en JavaScript‑hanterare som kommunicerar med servern, hämtar CSV‑filen, omvandlar den till en **Blob** och tvingar en nedladdning. Det är här frasen **download CSV file blob** förekommer.

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

### Genomgång av hanteraren

| Rad | Vad den gör |
|------|--------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Anropar en Flask‑rutt (`/export/csv`) och skickar med bladnamnet som en query‑sträng. |
| `.then(r => r.blob())` | Omvandlar HTTP‑svaret till en **Blob** – i princip en binär behållare för CSV‑data. |
| `URL.createObjectURL(b)` | Skapar en temporär URL som webbläsaren kan behandla som en fil. |
| `a.download = cell.sheetName + ".csv"` | Ställer in filnamnet som användaren ser i nedladdningsdialogen. |
| `a.click()` | Klickar programatiskt på den dolda ankaren, vilket får webbläsaren att ladda ner Blob‑en. |

> **Varför använda en Blob?**  
> Webbläsare kan inte direkt ladda ner rå text som returneras från `fetch` utan att omvandla den till något fil‑liknande. Blob‑URL‑tricket är det mest pålitliga, webbläsar‑oberoende sättet att trigga en **download CSV file blob** utan att uppdatera sidan.

---

## Konfigurera Flask‑backend

Front‑end‑hanteraren förväntar sig en endpoint på `/export/csv`. Här är en minimal Flask‑vy som tar emot bladnamnet, hämtar data från arbetsboken och strömmar tillbaka en CSV.

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

### Viktiga punkter

- **`io.StringIO`** låter oss bygga CSV‑filen i minnet utan att röra filsystemet.
- **`Content‑Disposition`** talar om för webbläsaren att filen är en bilaga och föreslår ett filnamn. Även om front‑end också sätter `a.download`, ger det på serversidan en reserv för icke‑JS‑klienter.
- Routen är avsiktligt enkel; du kan senare lägga till autentisering, behörighetskontroller eller streaming för enorma dataset.

---

## Rendera rutnätet på klienten

Med kontextmenyn och backend klar är sista delen att rendera GridJs‑komponenten och skicka HTML/JS till webbläsaren.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

I en Flask‑vy skulle du vanligtvis göra:

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

När sidan laddas bygger GridJs tabellen, injicerar den anpassade kontextmenyn, och JavaScript‑hanteraren vi definierade tidigare är redo att köras. Högerklicka på någon cell, välj **Export CSV**, och se webbläsaren ladda ner en fil med bladets namn.

---

## Fullt fungerande exempel (alla filer)

Nedan är den kompletta, körbara koden som du kan kopiera‑klistra in i en ny mapp. Installera Flask (`pip install flask`) och kör `python app.py`.

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


## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Ladda Csv-filer med anpassade parsers Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Csv-export Java-kod](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Exportera Excel Csv tomma rader Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}