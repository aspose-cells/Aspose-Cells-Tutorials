---
category: general
date: 2026-06-08
description: Add custom context menu to GridJs and export grid to CSV with a download
  CSV file blob. Follow this step‑by‑step tutorial for a fully working example.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: en
og_description: Add custom context menu to GridJs and export grid to CSV with a download
  CSV file blob. Learn the full implementation in under 10 minutes.
og_title: Add Custom Context Menu to GridJs – Complete Guide
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
title: Add Custom Context Menu to GridJs – Complete Guide
url: /python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Custom Context Menu to GridJs – Complete Guide

Want to **add custom context menu** to a GridJs component? In this tutorial we'll walk you through exactly that, and show you how to **export grid to CSV** using a **download CSV file blob**. Whether you’re building a quick admin panel or a full‑blown reporting dashboard, a right‑click menu that lets users pull data out as CSV can be a real productivity boost.

We'll cover everything you need: the Python side with Flask, the JavaScript handler that creates the Blob, and the HTML/JS that GridJs spits out. By the end you’ll have a self‑contained example you can drop into any project.

---

## What You’ll Need

Before we dive in, make sure you have:

- **Python 3.9+** and **Flask** installed (`pip install flask`).
- The **gridjs** Python wrapper (or the JavaScript library directly) – for this guide we’ll assume a thin Python wrapper that mirrors the JavaScript API.
- A basic understanding of **async JavaScript** (`fetch`, `Promise`) – but don’t worry, we’ll explain each line.
- An editor you like (VS Code, PyCharm, or even a simple text editor will do).

That’s it. No extra front‑end build tools, no Node npm dance. Just plain Flask serving the HTML that GridJs generates.

---

## Add Custom Context Menu to GridJs

The first thing you have to do is tell GridJs that you want a custom right‑click menu. By default GridJs ships with a minimal set (copy, paste, etc.), but you can replace it entirely.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Why this matters:**  
Setting `CustomContextMenu` replaces the default list with the one you provide. The string `"Export CSV"` is just a label – the real work happens when the user clicks it, which we’ll wire up in the next step.

> *Pro tip:* Keep the list short. A cluttered context menu defeats the purpose of quick actions.

---

## Export Grid to CSV with a Blob Download

Now that the menu item exists, we need a JavaScript handler that talks to the server, fetches the CSV, turns it into a **Blob**, and forces a download. This is where the phrase **download CSV file blob** lives.

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

### Breaking Down the Handler

| Line | What It Does |
|------|--------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Calls a Flask route (`/export/csv`) passing the sheet name as a query string. |
| `.then(r => r.blob())` | Converts the HTTP response to a **Blob** – essentially a binary container for the CSV data. |
| `URL.createObjectURL(b)` | Generates a temporary URL that the browser can treat like a file. |
| `a.download = cell.sheetName + ".csv"` | Sets the filename that the user will see in the download dialog. |
| `a.click()` | Programmatically clicks the hidden anchor, prompting the browser to download the Blob. |

> **Why use a Blob?**  
> Browsers can’t directly download raw text returned from `fetch` without turning it into something file‑like. The Blob‑URL trick is the most reliable, cross‑browser way to trigger a **download CSV file blob** without refreshing the page.

---

## Setting Up the Flask Backend

The front‑end handler expects an endpoint at `/export/csv`. Here’s a minimal Flask view that takes the sheet name, pulls data from the workbook, and streams a CSV back.

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

### Key Points

- **`io.StringIO`** lets us build the CSV in memory without touching the filesystem.
- **`Content‑Disposition`** tells the browser the file is an attachment and suggests a filename. Even though the front‑end also sets `a.download`, having it on the server side provides a fallback for non‑JS clients.
- The route is deliberately simple; you can add authentication, permission checks, or streaming for huge datasets later.

---

## Rendering the Grid on the Client

With the context menu and backend ready, the final piece is to render the GridJs component and ship the HTML/JS to the browser.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

In a Flask view you’d typically do:

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

When the page loads, GridJs builds the table, injects the custom context menu, and the JavaScript handler we defined earlier is ready to fire. Right‑click any cell, pick **Export CSV**, and watch the browser download a file named after the sheet.

---

## Full Working Example (All Files)

Below is the complete, runnable code you can copy‑paste into a new folder. Install Flask (`pip install flask`) and run `python app.py`.

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


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Load Csv Files Custom Parsers Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Csv Export Java Code](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}