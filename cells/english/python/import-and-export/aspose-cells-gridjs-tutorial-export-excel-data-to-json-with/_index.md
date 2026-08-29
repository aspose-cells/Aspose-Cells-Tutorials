---
category: general
date: 2026-07-03
description: Aspose Cells GridJs tutorial showing how to export Excel data JSON and
  export worksheet to JSON efficiently using lazy loading.
draft: false
keywords:
- aspose cells gridjs tutorial
- export excel data json
- export worksheet to json
language: en
og_description: Aspose Cells GridJs tutorial explains how to export Excel data JSON
  and export worksheet to JSON with lazy loading for large spreadsheets.
og_title: Aspose Cells GridJs tutorial – Export Excel data to JSON
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
title: Aspose Cells GridJs tutorial – Export Excel data to JSON with lazy loading
url: /python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells GridJs tutorial – Export Excel data JSON with lazy loading

Ever wondered how to **export Excel data JSON** from a massive spreadsheet without choking the browser? In this Aspose Cells GridJs tutorial we’ll walk through a complete, ready‑to‑run solution that lets you **export worksheet to JSON** using lazy loading, so only the rows you need are fetched on demand.

If you’ve been wrestling with huge `.xlsx` files and the client side keeps freezing, you’re not alone. The good news? The approach we cover here is both lightweight and scalable, and you can drop it into any Python project that already uses the Aspose.Cells library.

## What this guide covers

In the next few minutes you’ll learn how to:

1. Load a large workbook with Aspose.Cells.
2. Turn on GridJs lazy loading so the server streams rows in chunks.
3. Export the GridJs configuration to a JSON file that the front‑end can consume.
4. Tweak the chunk size for optimal performance.
5. Verify the output and integrate it with a simple HTML page.

No external services, no hidden magic—just pure Python and the Aspose.Cells API. By the end you’ll have a **complete export worksheet to JSON** pipeline that you can adapt to dashboards, reporting tools, or any data‑grid component.

### Prerequisites

- Python 3.8+ installed locally.
- `asposecells` package (you can `pip install aspose-cells`).
- A sizeable Excel file (e.g., `large-data.xlsx`) placed in a known directory.
- Basic familiarity with Python and web development concepts.

If any of these sound unfamiliar, don’t panic—each step includes a short “why” explanation so you’ll understand the reasoning behind the code.

---

## Step 1: Install and import Aspose.Cells

First things first, we need the Aspose.Cells library. It’s a commercial product, but a free trial works for development.

```bash
pip install aspose-cells
```

Now import the necessary classes in your script.

```python
# Step 1: Import the Aspose.Cells workbook class
import asposecells
from asposecells import Workbook
```

> **Why this matters:** Importing `Workbook` gives you access to the high‑performance engine that reads Excel files directly into memory, bypassing the slower `openpyxl` approach.

## Step 2: Load the workbook containing the large dataset

With the library ready, point it at your Excel file. The path can be absolute or relative; just make sure the file exists.

```python
# Step 2: Load the workbook that contains a large data set
workbook = Workbook("YOUR_DIRECTORY/large-data.xlsx")
```

> **Pro tip:** If your workbook is larger than a few hundred megabytes, consider increasing the Python process memory limit or using a 64‑bit interpreter to avoid `MemoryError`.

## Step 3: Enable GridJs lazy loading

GridJs is Aspose’s JavaScript grid component. Lazy loading tells the server to send only a subset of rows—perfect for huge sheets.

```python
# Step 3: Enable lazy loading so the client fetches rows on demand
grid_options = workbook.Worksheets[0].Cells.GridJsOptions
grid_options.LazyLoading = True                 # fetch rows/columns only when needed
grid_options.LazyLoadingChunkSize = 500         # rows per server request
```

> **Why lazy loading?** Without it, the entire worksheet would be serialized into JSON in one go, which can easily exceed browser memory limits. By setting `LazyLoadingChunkSize` to 500, each request carries a manageable payload.

## Step 4: Export the GridJs configuration to JSON

Now we ask Aspose to produce the JSON that the front‑end GridJs component expects. This is the core of the **export excel data json** operation.

```python
# Step 4: Export the GridJs configuration to a JSON file for the client side
grid_json = workbook.Worksheets[0].Cells.ExportGridJsJson()
```

The `ExportGridJsJson` method returns a `bytes` object containing the JSON representation of the worksheet, ready to be saved or streamed.

## Step 5: Write the JSON to a file (or stream it)

For a quick test, write the JSON to disk. In a production API you’d return it directly from a Flask/Django endpoint.

```python
# Step 5: Persist the JSON to a file
output_path = "YOUR_DIRECTORY/lazygrid.json"
with open(output_path, "wb") as f:
    f.write(grid_json)

print(f"✅ GridJs JSON exported successfully to {output_path}")
```

> **What you’ll see:** Opening `lazygrid.json` reveals a structure with `columns`, `rows`, and pagination metadata. The `rows` array will initially be empty; GridJs will request the first chunk when the page loads.

## Step 6: Hook the JSON into a simple HTML page (optional)

If you want to see the grid in action, create a tiny HTML file that loads GridJs from a CDN and points it at the generated JSON.

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

> **Why include this?** It demonstrates the full round‑trip: Python creates the JSON, the browser pulls it, and GridJs renders the data chunk‑by‑chunk. You can now experiment with different `LazyLoadingChunkSize` values to find the sweet spot for your network.

## Step 7: Verify and troubleshoot

Run the Python script:

```bash
python export_lazy_grid.py
```

You should see the success message and a `lazygrid.json` file. Open the HTML file in a browser; the grid should display the first 500 rows instantly, with pagination controls to load more.

If the grid appears empty:

- **Check the JSON file size** – a zero‑byte file usually means the workbook path was wrong.
- **Confirm lazy loading is enabled** – the `LazyLoading` flag must be `True`.
- **Inspect browser console** – any CORS or 404 errors indicate the JSON isn’t being served correctly.

---

## Common variations and edge cases

### Exporting a specific worksheet

The example above always uses the first worksheet (`Worksheets[0]`). To export a different sheet, simply change the index or use the sheet name:

```python
sheet = workbook.Worksheets["DataSheet"]   # by name
grid_options = sheet.Cells.GridJsOptions
grid_json = sheet.Cells.ExportGridJsJson()
```

### Changing the chunk size for massive files

For files with millions of rows, a chunk size of 500 may still be too small, causing many round‑trips. You can increase it to 2000 or more, but remember that larger chunks consume more bandwidth per request.

```python
grid_options.LazyLoadingChunkSize = 2000
```

### Exporting to a stream instead of a file

If your API returns the JSON directly, you don’t need to write to disk:

```python
from flask import Flask, Response
app = Flask(__name__)

@app.route("/api/gridjson")
def gridjson():
    json_bytes = workbook.Worksheets[0].Cells.ExportGridJsJson()
    return Response(json_bytes, mimetype="application/json")
```

### Handling formulas and formatting

By default, `ExportGridJsJson` includes the calculated values of formulas. If you need raw formulas instead, set:

```python
grid_options.ExportFormulas = True
```

---

## Conclusion

In this **Aspose Cells GridJs tutorial** we covered everything you need to **export Excel data JSON** and **export worksheet to JSON** with lazy loading. From installing Aspose.Cells, enabling lazy loading, generating the JSON, to wiring it up with a simple HTML page, you now have a full‑stack pattern that scales gracefully with massive spreadsheets.

Give it a spin—adjust the chunk size, point at different worksheets, or integrate the endpoint into a Flask or Django app. The possibilities are endless, and the performance gains are immediate.

Ready to take the next step? Try adding column sorting, custom cell renderers, or even server‑side filtering to make your GridJs grid truly interactive. If you hit a snag, drop a comment below; happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Import JSON Data into Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Load CSV & Export to JSON Using Aspose.Cells for .NET&#58; A Comprehensive Guide](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Export Excel Data Using Aspose.Cells .NET&#58; A Complete Guide for Seamless Data Export](/cells/english/net/import-export/export-excel-data-aspose-cells-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}