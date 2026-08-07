---
category: general
date: 2026-06-08
description: Adj hozzá egyedi helyi menüt a GridJs-hez, és exportáld a rácsot CSV-be
  egy letölthető CSV-fájl blobbal. Kövesd ezt a lépésről‑lépésre útmutatót egy teljesen
  működő példához.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: hu
og_description: Adj hozzá egyedi helyi menüt a GridJs-hez, és exportáld a rácsot CSV-be
  egy letölthető CSV-fájl blobbal. Ismerd meg a teljes megvalósítást 10 percnél kevesebb
  idő alatt.
og_title: Egyedi helyi menü hozzáadása a GridJs-hez – Teljes útmutató
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
title: Egyéni helyi menü hozzáadása a GridJs-hez – Teljes útmutató
url: /hu/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyedi helyi menü hozzáadása a GridJs‑hez – Teljes útmutató

Szeretnél **egyedi helyi menüt** hozzáadni egy GridJs komponenshez? Ebben a tutorialban pontosan ezt mutatjuk be, és megmutatjuk, hogyan **exportálhatod a rácsot CSV‑be** egy **CSV fájl blob letöltésével**. Akár egy gyors admin panelt, akár egy teljes körű jelentéskészítő dashboardot építesz, egy jobb‑gombos menü, amely lehetővé teszi a felhasználók számára, hogy CSV‑ként kinyerjék az adatokat, valódi termelékenységnövelő lehet.

Mindent lefedünk, amire szükséged lesz: a Python oldalt Flask‑kel, a JavaScript kezelőt, amely létrehozza a Blob‑ot, valamint a HTML/JS‑t, amelyet a GridJs generál. A végére egy önálló példát kapsz, amelyet bármelyik projektbe beilleszthetsz.

---

## Amire szükséged lesz

Mielőtt belevágnánk, győződj meg róla, hogy rendelkezel a következőkkel:

- **Python 3.9+** és **Flask** telepítve (`pip install flask`).
- A **gridjs** Python wrapper (vagy közvetlenül a JavaScript könyvtár) – ebben az útmutatóban egy vékony Python wrapper‑t feltételezünk, amely tükrözi a JavaScript API‑t.
- Alapvető ismeretek az **async JavaScript**‑ről (`fetch`, `Promise`) – de ne aggódj, minden sort elmagyarázunk.
- Egy kedvenc szerkesztő (VS Code, PyCharm, vagy akár egy egyszerű szövegszerkesztő).

Ennyi. Nincs szükség extra front‑end build eszközökre, nincs Node npm „tánc”. Csak egy egyszerű Flask szerver, amely a GridJs által generált HTML‑t szolgálja ki.

---

## Egyedi helyi menü hozzáadása a GridJs‑hez

Az első lépés, hogy elmondd a GridJs‑nek, hogy egy egyedi jobb‑gombos menüt szeretnél. Alapértelmezés szerint a GridJs egy minimális menüt (copy, paste, stb.) tartalmaz, de teljesen felülírhatod.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Miért fontos ez:**  
A `CustomContextMenu` beállítása felváltja az alapértelmezett listát az általad megadottal. A `"Export CSV"` csak egy címke – a valódi munka akkor történik, amikor a felhasználó rákattint, amit a következő lépésben kötünk össze.

> *Pro tipp:* Tartsd a listát röviden. Egy zsúfolt helyi menü aláássa a gyors műveletek célját.

---

## Grid exportálása CSV‑be Blob letöltéssel

Most, hogy a menüpont létezik, szükségünk van egy JavaScript kezelőre, amely kommunikál a szerverrel, lekéri a CSV‑t, Blob‑ba alakítja, és kényszeríti a letöltést. Itt jelenik meg a **download CSV file blob** kifejezés.

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

### A kezelő részletezése

| Sor | Mit csinál |
|------|------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Meghív egy Flask útvonalat (`/export/csv`), a lap nevét query stringként átadva. |
| `.then(r => r.blob())` | Átalakítja a HTTP választ **Blob**‑ra – lényegében egy bináris tároló a CSV adatok számára. |
| `URL.createObjectURL(b)` | Ideiglenes URL‑t generál, amelyet a böngésző fájlként kezelhet. |
| `a.download = cell.sheetName + ".csv"` | Beállítja a fájlnevet, amelyet a felhasználó a letöltési párbeszédablakban lát. |
| `a.click()` | Programozottan rákattint a rejtett horgonylinkre, így a böngésző letölti a Blob‑ot. |

> **Miért használunk Blob‑ot?**  
> A böngészők nem tudnak közvetlenül nyers szöveget letölteni a `fetch`‑ből anélkül, hogy azt fájlszerűvé ne alakítanák. A Blob‑URL trükk a legmegbízhatóbb, böngésző‑független módja egy **download CSV file blob** kiváltásának anélkül, hogy az oldal újratöltődne.

---

## Flask backend beállítása

A front‑end kezelő egy `/export/csv` végpontot vár. Íme egy minimális Flask view, amely megkapja a lap nevét, kinyeri az adatokat a munkafüzetből, és CSV‑ként streameli vissza.

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

### Fontos pontok

- **`io.StringIO`** lehetővé teszi, hogy a CSV‑t memóriában építsük fel, anélkül, hogy a fájlrendszert érintenénk.
- **`Content‑Disposition`** jelzi a böngészőnek, hogy a fájl egy melléklet, és javasol egy fájlnevet. Bár a front‑end is beállítja az `a.download` attribútumot, a szerveroldali beállítás tartalékot nyújt nem‑JS kliensek számára.
- Az útvonal szándékosan egyszerű; később hozzáadhatsz hitelesítést, jogosultság‑ellenőrzést vagy streaminget nagy adathalmazokhoz.

---

## A rács megjelenítése a kliensen

A helyi menü és a backend készen áll, a végső lépés a GridJs komponens renderelése és a HTML/JS elküldése a böngészőnek.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

Egy Flask view‑ban általában így néz ki:

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

Amikor az oldal betöltődik, a GridJs felépíti a táblázatot, beilleszti az egyedi helyi menüt, és a korábban definiált JavaScript kezelő készen áll a futtatásra. Jobb‑gombbal kattints bármely cellára, válaszd az **Export CSV**‑t, és a böngésző letölt egy a lap nevére nevezett fájlt.

---

## Teljes működő példa (minden fájl)

Az alábbiakban a teljes, futtatható kódot találod, amelyet egyszerűen bemásolhatsz egy új mappába. Telepítsd a Flask‑t (`pip install flask`) és futtasd a `python app.py` parancsot.

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


## Mit érdemes következőként megtanulni?


Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes működő kódrészleteket lépésről‑lépésre magyarázattal, hogy segítsen elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Load Csv Files Custom Parsers Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Csv Export Java Code](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}