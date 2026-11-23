---
category: general
date: 2026-11-22
description: Learn how to serve Excel in a web app using Flask. This guide shows how
  to load Excel workbook and display Excel on the web with GridJs.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to serve excel
- load excel workbook
- display excel web
language: en
lastmod: 2026-11-22
og_description: How to serve Excel files using Flask and GridJs. Follow this complete
  tutorial to load an Excel workbook and display it on the web.
og_image_alt: Screenshot of a Flask‑powered GridJs table showing Excel data
og_title: How to serve Excel with Flask – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to serve Excel in a web app using Flask. This guide shows
    how to load Excel workbook and display Excel on the web with GridJs.
  headline: How to serve Excel files with Flask and GridJs
  type: TechArticle
- description: Learn how to serve Excel in a web app using Flask. This guide shows
    how to load Excel workbook and display Excel on the web with GridJs.
  name: How to serve Excel files with Flask and GridJs
  steps:
  - name: Load the Excel workbook
    text: '```python # Step 1: Load the workbook you want to expose via GridJs import
      cells'
  - name: Create a GridJs server‑side handler
    text: '```python # Step 2: Create a GridJs server‑side handler for the workbook
      grid_handler = cells.GridJsHandler(workbook) ```'
  - name: Enable optional features (lazy loading)
    text: '```python # Step 3: Enable optional features (e.g., lazy loading for large
      sheets) grid_handler.settings.lazy_load = True ```'
  - name: Set up a minimal Flask application
    text: '```python # Step 4: Set up a minimal Flask application to serve the GridJs
      UI from flask import Flask, request, jsonify'
  - name: Define the GridJs endpoint
    text: '```python # Step 5: Define an endpoint that returns the current view state
      # and applies any client‑side edits sent as JSON @app.route("/gridjs", methods=["GET",
      "POST"]) def gridjs(): if request.method == "POST": # Apply edits sent from
      the GridJs UI grid_handler.apply_changes(request.json) # Retur'
  - name: Run the Flask server
    text: '```python # Step 6: Run the Flask server (default port 5000) if __name__
      == "__main__": # Debug mode is off for production; enable it only during development.
      app.run(port=5000, debug=False) ```'
  type: HowTo
tags:
- Flask
- Python
- Excel
title: How to serve Excel files with Flask and GridJs
url: /python/integration-and-interoperability/how-to-serve-excel-files-with-flask-and-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to serve Excel files with Flask and GridJs

If you need to **how to serve excel** in a Python web application, this tutorial shows a complete solution. You’ll learn how to **load excel workbook** with the `cells` library, expose it through a Flask endpoint, and let users **display excel web** using GridJs.

We’ll walk through every line of code, explain why each piece matters, and give you a ready‑to‑run example. By the end of the guide you can embed any `.xlsx` file into a responsive, client‑side grid without writing custom JavaScript data parsers.

## Prerequisites

Before you start, make sure you have:

- Python 3.9+ installed  
- `flask` and `cells` packages (`pip install flask cells`)  
- A sample Excel file (e.g., `sample.xlsx`) in a known directory  

No additional front‑end framework is required; GridJs handles the UI automatically.

## Overview of the solution

The core idea is simple:

1. **Load** the Excel workbook on the server.  
2. **Create** a `GridJsHandler` that translates worksheet data to the JSON format GridJs expects.  
3. **Expose** a Flask route that returns the JSON view and accepts edits from the client.  
4. **Run** the Flask server so the browser can fetch the data and render the grid.

Now let’s implement each step.

## How to serve Excel with Flask and GridJs

### Step 1: Load the Excel workbook

```python
# Step 1: Load the workbook you want to expose via GridJs
import cells

workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)
```

**Why this matters:**  
`cells.Workbook` parses the `.xlsx` file into an in‑memory representation. Loading the workbook once at startup keeps the server fast because subsequent requests reuse the same object instead of hitting the file system repeatedly.

### Step 2: Create a GridJs server‑side handler

```python
# Step 2: Create a GridJs server‑side handler for the workbook
grid_handler = cells.GridJsHandler(workbook)
```

**Why this matters:**  
`GridJsHandler` abstracts the conversion from Excel rows/columns to the JSON schema GridJs consumes. It also tracks client‑side edits, allowing you to persist changes back to the workbook later if needed.

### Step 3: Enable optional features (lazy loading)

```python
# Step 3: Enable optional features (e.g., lazy loading for large sheets)
grid_handler.settings.lazy_load = True
```

**Why this matters:**  
When a worksheet contains thousands of rows, sending the entire dataset at once can overload the browser. Lazy loading streams data page by page, improving performance for the **display excel web** scenario.

### Step 4: Set up a minimal Flask application

```python
# Step 4: Set up a minimal Flask application to serve the GridJs UI
from flask import Flask, request, jsonify

app = Flask(__name__)
```

**Why this matters:**  
Flask provides a lightweight HTTP server that can serve JSON endpoints and static files. Keeping the Flask app minimal reduces attack surface and makes the example easy to adapt.

### Step 5: Define the GridJs endpoint

```python
# Step 5: Define an endpoint that returns the current view state
#         and applies any client‑side edits sent as JSON
@app.route("/gridjs", methods=["GET", "POST"])
def gridjs():
    if request.method == "POST":
        # Apply edits sent from the GridJs UI
        grid_handler.apply_changes(request.json)
    # Return the JSON view expected by GridJs
    return jsonify(grid_handler.get_view())
```

**Why this matters:**  

- **GET** – The browser fetches the initial worksheet view.  
- **POST** – When a user edits a cell, GridJs sends a JSON payload; `apply_changes` merges those edits back into the handler’s internal state.  

Returning `grid_handler.get_view()` ensures the client always receives the latest data, which is essential for a smooth **display excel web** experience.

### Step 6: Run the Flask server

```python
# Step 6: Run the Flask server (default port 5000)
if __name__ == "__main__":
    # Debug mode is off for production; enable it only during development.
    app.run(port=5000, debug=False)
```

**Why this matters:**  
Running on port 5000 is Flask’s default, making it easy to test locally (`http://localhost:5000/gridjs`). In production you would place Flask behind a WSGI server (e.g., Gunicorn) and possibly enable HTTPS.

## Expected JSON output

When you navigate to `http://localhost:5000/gridjs` with a GET request, the response looks like:

```json
{
  "columns": ["A", "B", "C"],
  "data": [
    ["Header1", "Header2", "Header3"],
    ["Row1Col1", "Row1Col2", "Row1Col3"],
    ["Row2Col1", "Row2Col2", "Row2Col3"]
  ],
  "settings": {
    "lazy_load": true
  }
}
```

GridJs consumes this payload automatically, rendering a searchable, sortable table in the browser.

## Full runnable example

Below is the complete script you can copy into `app.py` and execute:

```python
import cells
from flask import Flask, request, jsonify

# -------------------------------------------------
# 1. Load the Excel workbook
# -------------------------------------------------
workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)

# -------------------------------------------------
# 2. Create the GridJs handler
# -------------------------------------------------
grid_handler = cells.GridJsHandler(workbook)

# -------------------------------------------------
# 3. Enable lazy loading (optional but recommended)
# -------------------------------------------------
grid_handler.settings.lazy_load = True

# -------------------------------------------------
# 4. Initialize Flask
# -------------------------------------------------
app = Flask(__name__)

# -------------------------------------------------
# 5. Define the GridJs endpoint
# -------------------------------------------------
@app.route("/gridjs", methods=["GET", "POST"])
def gridjs():
    if request.method == "POST":
        # Apply client‑side edits
        grid_handler.apply_changes(request.json)
    # Return current view as JSON
    return jsonify(grid_handler.get_view())

# -------------------------------------------------
# 6. Run the server
# -------------------------------------------------
if __name__ == "__main__":
    app.run(port=5000, debug=False)
```

Run the script with:

```bash
python app.py
```

Open a browser and point it to a simple HTML page that loads GridJs (see GridJs docs for the `<script>` tag). The grid will display the Excel content instantly.

## Common variations and edge cases

| Situation | How to adapt |
|-----------|--------------|
| **Multiple worksheets** | Create a separate `GridJsHandler` for each sheet and expose distinct endpoints (`/gridjs/sheet1`, `/gridjs/sheet2`). |
| **Large files (>10 MB)** | Increase Flask’s request size limit (`app.config['MAX_CONTENT_LENGTH']`) and keep `lazy_load` enabled. |
| **Persisting edits back to the file** | After `apply_changes`, call `workbook.save("output.xlsx")` to write changes to disk. |
| **Authentication** | Wrap the endpoint with Flask‑Login or an API token check before returning data. |
| **CORS for external front‑ends** | Add `from flask_cors import CORS; CORS(app)` to allow cross‑origin requests. |

These tweaks let you scale the **load excel workbook** process to production workloads.

## Pro tips

- **Cache the JSON view** if the workbook rarely changes; use `functools.lru_cache` around `grid_handler.get_view()` to cut down on serialization overhead.  
- **Validate incoming edits** (`request.json`) to prevent malformed data from corrupting the workbook.  
- When serving over HTTPS, set `app.run(ssl_context=('cert.pem', 'key.pem'))` to encrypt traffic.

## Conclusion

You now know **how to serve excel** files using Flask and GridJs, from loading the workbook to returning a JSON view that the browser can render. The example covers the full lifecycle: **load excel workbook**, enable lazy loading, expose a REST endpoint, and run a production‑ready server.

Next, explore related topics such as **display excel web** in a React front‑end, or extend the handler to **load excel workbook** from cloud storage (e.g., AWS S3). Experiment with styling GridJs columns, adding pagination, or persisting user edits back to the original spreadsheet.

Happy coding, and enjoy turning static Excel files into interactive web tables!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Load and Modify Excel Files Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}