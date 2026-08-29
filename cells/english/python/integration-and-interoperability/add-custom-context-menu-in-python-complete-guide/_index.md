---
category: general
date: 2026-06-30
description: Add custom context menu to a Python Excel grid and write value to excel
  cell while saving the updated file. Learn to create right‑click menu and update
  cell value python style.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: en
og_description: Add custom context menu in Python to write value to excel cell and
  save updated excel file. This guide walks you through creating a right‑click menu
  with GridJs.
og_title: Add Custom Context Menu in Python – Step‑by‑Step Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu to a Python Excel grid and write value to excel
    cell while saving the updated file. Learn to create right‑click menu and update
    cell value python style.
  headline: Add Custom Context Menu in Python – Complete Guide
  type: TechArticle
tags:
- Python
- Excel Automation
- GridJs
- Context Menu
title: Add Custom Context Menu in Python – Complete Guide
url: /python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Custom Context Menu in Python – Complete Guide

Ever wondered how to **add custom context menu** items to a spreadsheet grid you’re serving from Python? Maybe you need a quick “Mark as Reviewed” button that pops up when a user right‑clicks a cell, writes a value to the Excel cell, and then saves the updated workbook—all without leaving the web UI.  

In this tutorial we’ll build exactly that: a **custom right‑click menu** powered by GridJs, a server‑side handler that **write(s) value to excel cell**, and a final step that **save(s) updated excel file** on disk. By the end you’ll have a reusable pattern you can drop into any Flask, FastAPI, or Django project.

> **Why care?**  
> Adding a custom context menu streamlines data review workflows, cuts down on manual copy‑pasting, and gives end‑users a native‑feel experience straight inside the grid. Plus, you’ll see how to **update cell value python**‑style, which is a core skill for any Excel automation task.

## Prerequisites

- Python 3.9+ (the code works on 3.10 as well)  
- `openpyxl` for Excel file handling  
- `gridjs` Python wrapper (or the JS library if you prefer the front‑end)  
- A basic web framework (Flask example shown)  
- A workbook file named `sample.xlsx` in your project folder  

If you’re missing any of these, run:

```bash
pip install openpyxl flask gridjs
```

Now let’s dive in.

---

## Step 1 – Add Custom Context Menu: Initialize GridJs and Bind Worksheet

The very first thing you need to do is spin up a `GridJs` instance and point it at the worksheet you plan to work with. This is where the **add custom context menu** phrase first appears in our code, and it sets the stage for everything else.

```python
# step_1_initialize.py
import openpyxl
from gridjs import GridJs

# Load the workbook – this could be any .xlsx file you own
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]                     # Grab the sheet you’ll display

# Create the GridJs object and bind it to the worksheet
grid = GridJs()
grid.set_worksheet(ws)                # <-- add custom context menu works on this sheet
```

**What’s happening?**  
`grid.set_worksheet(ws)` tells GridJs to use the data from `ws` as its data source. From here on, any context‑menu modifications we add will automatically target the same worksheet, keeping the UI and the file in sync.

> **Pro tip:** Keep your workbook open in read/write mode only once. Opening it repeatedly inside a request handler can cause file‑locking issues on Windows.

---

## Step 2 – Write Value to Excel Cell: Define the Action for the Menu Item

Now that the grid is ready, we need to **write value to excel cell** when the user selects our custom command. We’ll add a menu entry called “Mark as Reviewed” and give it an identifier `markReviewed`. The identifier is what the client‑side JavaScript will send back to the server.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**Why use a custom identifier?**  
The identifier decouples UI text from server logic, allowing you to change the label without touching the backend code. It also makes the **create right‑click menu** operation explicit and reusable.

---

## Step 3 – Create Right‑Click Menu: Register the Server‑Side Handler

With the menu item in place, we need to tell GridJs what to do when the user clicks it. This is where we **create right‑click menu** functionality that actually fires a request back to Python.

```python
# step_3_handler.py
def on_custom_command(request):
    """
    Server‑side handler for the 'markReviewed' custom command.
    It receives a JSON payload like {"cell": "C12"}.
    """
    # Extract the cell address from the incoming request
    cell_address = request["cell"]           # e.g., "C12"

    # Write the word "Reviewed" into that cell
    ws[cell_address] = "Reviewed"            # <-- write value to excel cell

    # Persist the change to disk (see next step)
    # We'll return a simple JSON response to the client
    return {"status": "ok"}
```

A few things to note:

1. **`ws[cell_address] = "Reviewed"`** is the most straightforward way to **update cell value python**. Under the hood, `openpyxl` translates the A1‑style address into row/column indices.
2. The handler returns a tiny JSON payload. GridJs expects a status indicator; you could expand this to include error messages if needed.

Now we bind the identifier to the handler:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**What if the cell is empty or protected?**  
- Empty cells are fine—`openpyxl` will create them on the fly.  
- For protected sheets, you’ll need to unprotect first (`ws.protection.sheet = False`) or catch a `PermissionError`.

---

## Step 4 – Update Cell Value Python: Persist the Change by Saving the Workbook

Writing a value is only half the story; you must **save updated excel file** so the change survives beyond the current session. This is where we finish the round‑trip from UI to disk.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**Why a separate folder?**  
Saving into an `output/` directory keeps the original template untouched, which is useful for audit trails. Adjust the path to match your deployment environment.

> **Watch out:** If you’re serving many concurrent users, consider using a thread‑safe lock (`threading.Lock`) around `wb.save()` to avoid race conditions.

---

## Step 5 – Generate Client Configuration JSON and Wire It All Together

Finally, we need to produce the JSON that the front‑end GridJs instance will consume. This JSON contains the worksheet data **and** the custom menu definition.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

When you embed `config_json` into your HTML page, GridJs will render the grid with the “Mark as Reviewed” entry right‑clickable on every cell.

### Full Flask Example

Below is a minimal Flask app that puts all the pieces together. Run it, open `http://localhost:5000` and right‑click any cell to see the custom menu in action.

```python
# app.py
from flask import Flask, request, jsonify, render_template_string
import openpyxl
from gridjs import GridJs

app = Flask(__name__)

# Load workbook once at startup
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]
grid = GridJs()
grid.set_worksheet(ws)

# ---- Add custom context menu item ----
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed",
    "icon": "check_circle"
})

# ---- Server‑side handler ----
def on_custom_command(req):
    cell = req["cell"]
    ws[cell] = "Reviewed"
    wb.save("output/sample-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", on_custom_command)

# ---- Routes ----
@app.route("/")
def index():
    config = grid.get_client_config()
    # Simple inline template; in production use a separate .html file
    html = f"""
    <!doctype html>
    <html>
      <head>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
      </head>
      <body>
        <div id="wrapper"></div>
        <script>
          const config = {config};
          new gridjs.Grid(config).render(document.getElementById("wrapper"));
        </script>
      </body>
    </html>
    """
    return render_template_string(html)

@app.route("/custom-command", methods=["POST"])
def custom_command():
    payload = request.get_json()
    result = on_custom_command(payload)
    return jsonify(result)

if __name__ == "__main__":
    app.run(debug=True)
```

**Expected outcome:**  
- Right‑click any cell → “Mark as Reviewed” appears.  
- Click it → the cell content changes to “Reviewed”.  
- The workbook `output/sample-updated.xlsx` now contains the new value.

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *What if I need multiple custom actions?* | Just add more objects to `grid.settings.context_menu.custom_items` and register each with its own identifier. |
| *Can I pass extra data (e.g., row ID) to the handler?* | Yes. Include extra keys in the JSON payload on the client side, then read them from `request` in `on_custom_command`. |
| *Is this approach compatible with async frameworks?* | Absolutely—just make `on_custom_command` an async function and use `await wb.save(...)` if you switch to `aiofiles` or similar. |
| *How do I style the menu icon?* | Provide any Material‑Icons name (`"icon": "edit"`). The front‑end automatically loads the icon font. |
| *What about large workbooks?* | Load only the required sheet, and consider streaming rows with `openpyxl.iter_rows()` to keep memory usage


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Preserve Single Quote Prefix of Cell Value or Range in Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}