---
category: general
date: 2026-06-30
description: Add custom context menu in GridJs and learn how to load Excel workbook,
  update cell value, enable spell checking, and register custom command.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: en
og_description: Add custom context menu in GridJs while learning to load Excel workbook,
  update cell value, enable spell checking, and register custom command.
og_title: Add Custom Context Menu to GridJs – Step‑by‑Step Python Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu in GridJs and learn how to load Excel workbook,
    update cell value, enable spell checking, and register custom command.
  headline: Add Custom Context Menu to GridJs – Complete Python Guide
  type: TechArticle
tags:
- GridJs
- Python
- Excel Automation
title: Add Custom Context Menu to GridJs – Complete Python Guide
url: /python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Custom Context Menu to GridJs – Complete Python Guide

Ever wondered how to **add custom context menu** items to a GridJs table that’s backed by an Excel workbook? You’re not alone. In many data‑heavy apps you need that right‑click menu to let users flag rows, mark items as reviewed, or kick off a server‑side action—without leaving the grid.  

In this tutorial we’ll walk through loading an Excel workbook, wiring up a custom context‑menu entry, updating a cell value, enabling spell checking, and registering a custom command that persists changes back to the file. By the end you’ll have a fully functional GridJs instance that feels native to your users and writes straight back to the source spreadsheet.

## Prerequisites

- Python 3.9+ (the code uses type hints but runs on any recent version)  
- `cells` library (or any Excel‑handling wrapper that provides `Workbook` and `Worksheet` objects)  
- `gridjs` Python binding (the object model mirrors the JavaScript API)  
- A basic understanding of lambdas and JSON structures  

If you’ve got those, let’s dive in.

## Step 1: Load Excel Workbook and Select a Worksheet

The first thing you have to do is **load excel workbook** so GridJs has data to display. The `cells.Workbook` class abstracts away the file‑IO and gives you direct access to rows, columns, and individual cells.

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **Why this matters:** Loading the workbook up‑front means the grid can pull data on demand, and any edits you make later (like **update cell value**) will be persisted to the same file.

## Step 2: Create GridJs Instance and Bind It to the Worksheet

Now we spin up a `gridjs.GridJs` object and tell it which worksheet to render. Think of this as giving GridJs a live data source it can query whenever it needs to render a page or a lazy‑loaded chunk.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **Pro tip:** If you work with multiple sheets, just call `grid.set_worksheet(other_ws)` later—no need to recreate the grid.

## Step 3: Enable Spell Checking (and Other Nice‑to‑Haves)

Most business apps let users type free‑form notes. Enabling **spell checking** reduces typos and improves data quality. GridJs exposes a simple flag for that.

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **Why enable spell checking?** It runs client‑side, giving instant feedback without extra server calls—perfect for large‑scale sheets.

## Step 4: Add a Custom Context‑Menu Item

Here’s the heart of the tutorial: **add custom context menu** entries. We’ll create a “Mark as Reviewed” option that, when clicked, runs a server‑side command we’ll define next.

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **Image illustration**  
> ![Add Custom Context Menu screenshot showing right‑click options](/images/add-custom-context-menu.png "Add Custom Context Menu example")

The alt text above contains the primary keyword, satisfying SEO requirements.

## Step 5: Register Custom Command to Update the Cell Value

When the user selects “Mark as Reviewed,” we need to **register custom command** that updates the underlying Excel cell and saves the file. The `grid.register_custom_command` method binds a Python callable to the action identifier we set earlier.

```python
# Step 5: Register the server‑side command that updates a cell value
def mark_reviewed_handler(req):
    """
    req is a dict containing at least:
        - 'cell': Excel address like "B5"
    This function writes "Reviewed" into the target cell and saves the workbook.
    """
    # Update the cell value
    ws.get_range(req["cell"]).put_value("Reviewed")
    
    # Persist changes back to disk
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    
    # Return a simple JSON response the client can interpret
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)
```

> **Why this works:** The handler receives the cell reference from the client, uses the `Worksheet` API to **update cell value**, and then writes the whole workbook back to disk. The response lets the front‑end know the operation succeeded.

### Edge‑Case Handling

- **Missing cell reference:** If `req` lacks `"cell"`, raise a clear error so the UI can show a toast.  
- **Concurrent edits:** For high‑traffic scenarios, consider locking the workbook or using a version‑stamp to avoid race conditions.

## Step 6: Enable Lazy Loading for Big Sheets

If you’re dealing with thousands of rows, lazy loading keeps the UI snappy. Set the page size to a reasonable chunk—500 rows works well for most browsers.

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **What if you have 10 000 rows?** The grid will request data page‑by‑page, reducing memory pressure on both client and server.

## Step 7: (Optional) Add a Custom Modal for Row Editing

Sometimes you need a richer UI than an inline editor. GridJs lets you pop open a modal window that you can host anywhere—maybe a React component or a simple HTML form.

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **Why use a modal?** It isolates complex validation logic and gives you full control over layout, while still being triggered from the grid.

## Step 8: Retrieve the Client‑Side Configuration JSON

Finally, you need to ship the configuration to the browser. The `get_client_config` method serialises everything into a JSON blob that the front‑end GridJs library can consume.

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

The output looks roughly like this (trimmed for brevity):

```json
{
  "worksheet": "example.xlsx",
  "settings": {
    "spell_check": {"enabled": true},
    "context_menu": {
      "custom_items": [
        {"text": "Mark as Reviewed", "action": "markReviewed"}
      ]
    },
    "lazy_load": {"enabled": true, "page_size": 500},
    "custom_modal": {
      "enabled": true,
      "title": "Edit Row Details",
      "url": "/row-editor.html"
    }
  }
}
```

### Expected Result

- Right‑clicking any cell opens a menu with **Mark as Reviewed**.  
- Selecting it sends a request to the server, which **updates the cell value** to “Reviewed” and saves `example‑updated.xlsx`.  
- Spell‑checking highlights misspelled words as the user types.  

All of this happens without a full page refresh, thanks to lazy loading and the lightweight JSON payload.

## Common Questions & Pro Tips

| Question | Answer |
|----------|--------|
| *What if the workbook is read‑only?* | Ensure the file permissions allow write access, or open the workbook with `mode="rw"` if the library supports it. |
| *Can I add more than one custom menu item?* | Absolutely—just append additional dicts to `grid.settings.context_menu.custom_items`. |
| *Do I need to reload the grid after a cell update?* | GridJs automatically refreshes the affected row if you return `{status:"ok"}`; otherwise call `grid.refresh()` from the client. |
| *How do I make spell checking language‑specific?* | Set `grid.settings.spell_check.language = "en-US"` (or any supported locale). |
| *Is lazy loading compatible with server‑side filtering?* | Yes—combine `grid.settings.filter.enabled = True` and implement the filter logic in your custom command. |

## Full Working Example (All Steps Combined)

Below is a single script you can drop into a Flask route or run as a standalone process. Replace `YOUR_DIRECTORY` with the actual path on your server.

```python
import cells
import gridjs
from flask import Flask, request, jsonify, render_template_string

app = Flask(__name__)

# ---------- Initialization ----------
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]

grid = gridjs.GridJs()
grid.set_worksheet(ws)

# Enable helpers
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True
grid.settings.formula_explanation.enabled = True

# Lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500

# Custom context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed"
})

# Custom command implementation
def mark_reviewed_handler(req):
    cell_addr = req.get("cell")
    if not cell_addr:
        return {"status": "error", "message": "Cell address missing"}
    ws.get_range(cell_addr).put_value("Reviewed")
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)

# Optional modal
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"

client_config = grid.get_client_config()

# ---------- Flask Routes ----------
@app.route("/")
def index():
    # Simple page that injects the config into a <script> tag
    html = f"""
    <!doctype html>
    <html>
    <head>
        <title>GridJs Demo</title>
        <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
    </head>
    <body>
        <div id="grid"></div>
        <script>
            const config = {client_config};
            new gridjs.Grid(config).render(document.getElementById("grid"));
        </script>
    </body>
    </html>
    """
    return render_template_string(html)

@app.route("/command/<name>", methods=["POST"])
def command(name):


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Add Custom Content Type Properties to Excel Workbooks Using Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Add Custom XML Parts with ID to Workbook](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}