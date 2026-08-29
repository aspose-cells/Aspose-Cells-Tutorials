---
category: general
date: 2026-06-21
description: Enable spell check while you export Excel JSON using GridJs. Learn to
  convert xlsx to JSON, configure lazy loading, and load Excel workbook efficiently.
draft: false
keywords:
- enable spell check
- export excel json
- convert xlsx to json
- configure lazy loading
- load excel workbook
language: en
og_description: Enable spell check while exporting Excel JSON with GridJs. This guide
  shows how to convert xlsx to JSON, configure lazy loading, and load an Excel workbook.
og_title: Enable Spell Check & Export Excel JSON with GridJs
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Enable spell check while you export Excel JSON using GridJs. Learn
    to convert xlsx to JSON, configure lazy loading, and load Excel workbook efficiently.
  headline: Enable Spell Check & Export Excel JSON with GridJs
  type: TechArticle
tags:
- GridJs
- Excel
- JSON
- Python
title: Enable Spell Check & Export Excel JSON with GridJs
url: /python/import-and-export/enable-spell-check-export-excel-json-with-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Enable Spell Check & Export Excel JSON with GridJs

Ever needed to **enable spell check** in a web‑based spreadsheet UI and wondered how to get the data out as JSON at the same time? You're not alone. Many developers hit the same wall when they try to **export Excel JSON** from a workbook while keeping advanced features like formula validation alive.

In this tutorial we’ll walk through a complete, runnable example that shows you how to **load Excel workbook**, turn it into a JSON payload with GridJs, **configure lazy loading**, and of course **enable spell check**. By the end you’ll be able to **convert xlsx to JSON** in just a handful of lines—no mystery, no missing pieces.

> **What you’ll walk away with**  
> * A Python script that reads an `.xlsx` file, spins up a GridJs server object, and writes `grid_data.json`.  
> * Understanding of why each option matters (spell checking, formula checking, lazy loading).  
> * Tips for scaling the solution to larger workbooks.

---

## Prerequisites

Before we dive in, make sure you have the following on your machine:

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.9+ | Required for the `cells` package used below. |
| `cells` library (`pip install cells`) | Provides `Workbook` and `GridJs` classes. |
| A sample Excel file (`sample.xlsx`) | This is the source we’ll **load excel workbook** from. |
| Write permission to the output folder | Needed for the `grid.save()` step. |

If any of these sound unfamiliar, pause and install them first—otherwise the script will raise an import error.

---

## Step 1: Load Excel Workbook

The very first thing you do when you want to **convert xlsx to json** is to open the workbook. Think of it as unlocking the door before you can decorate the room.

```python
import cells

# Replace YOUR_DIRECTORY with the actual path on your system
workbook_path = "YOUR_DIRECTORY/sample.xlsx"

# Load the workbook – this is the entry point for all further operations
workbook = cells.Workbook(workbook_path)
print(f"Workbook loaded: {workbook_path}")
```

> **Pro tip:** If your file is huge, consider using `cells.Workbook(..., read_only=True)` to reduce memory consumption.

---

## Step 2: Create a GridJs Server Object

Now that the workbook is in memory, we need a **GridJs** object that will translate the sheets into JSON that the client UI can consume.

```python
# Create a GridJs instance linked to the workbook
grid = cells.GridJs(workbook)
print("GridJs server object created.")
```

The `grid` variable is essentially a thin wrapper around the workbook that knows how to serialize cells, formulas, and even styling information.

---

## Step 3: Enable Spell Check (and Formula Checker)

Here’s where the primary keyword shines. By toggling the `enableSpellCheck` flag, you give end‑users a safety net against typos—just like in Excel desktop.

```python
# Turn on advanced validation features
grid.options["enableFormulaChecker"] = True   # optional but handy
grid.options["enableSpellCheck"] = True       # <-- enable spell check
print("Spell check and formula checker enabled.")
```

Why enable both? Spell checking catches textual errors, while the formula checker guards against broken calculations. Together they make the web UI feel as polished as the native Excel experience.

---

## Step 4: Configure Lazy Loading

If you’re dealing with thousands of rows, sending the entire dataset in one payload will choke the browser. **Configure lazy loading** to ship data in bite‑size chunks (500 rows per request in our example).

```python
# Lazy loading improves performance for large sheets
grid.options["lazyLoading"] = {"pageSize": 500}
print("Lazy loading configured: 500 rows per request.")
```

You can tweak `pageSize` based on your network conditions. Smaller pages mean more round‑trips but smoother UI; larger pages reduce calls but may cause lag.

---

## Step 5: Export Excel JSON

All the heavy lifting is now behind the scenes. The final act is to **export excel json** to a file that your front‑end can request.

```python
# Destination for the generated JSON
output_path = "YOUR_DIRECTORY/grid_data.json"

# Persist the JSON representation
grid.save(output_path)
print(f"JSON exported to: {output_path}")
```

When the `save` method finishes, you’ll have a tidy `grid_data.json` containing:

* Sheet names and IDs  
* Row data (values, formulas, and formatting)  
* Metadata about enabled features (spell check, lazy loading, etc.)

You can verify the output by opening the file in a text editor or by loading it in a browser console:

```json
{
  "sheets": [
    {
      "name": "Sheet1",
      "rows": [
        {"c": [{"v": "Hello"}, {"v": 123}]},
        {"c": [{"v": "World"}, {"v": 456}]}
      ]
    }
  ],
  "options": {
    "enableSpellCheck": true,
    "enableFormulaChecker": true,
    "lazyLoading": {"pageSize": 500}
  }
}
```

That’s a **complete, self‑contained solution** for turning an Excel file into a JSON payload while keeping spell‑check alive.

---

## Full Script – Put It All Together

Below is the entire program you can copy‑paste, adjust the paths, and run. No hidden steps, no external scripts—just one file.

```python
import cells

# ----------------------------------------------------------------------
# Configuration – adjust these variables to match your environment
# ----------------------------------------------------------------------
WORKBOOK_PATH = "YOUR_DIRECTORY/sample.xlsx"
OUTPUT_JSON = "YOUR_DIRECTORY/grid_data.json"
PAGE_SIZE = 500   # rows per lazy‑load request

# ----------------------------------------------------------------------
# 1️⃣ Load the Excel workbook
# ----------------------------------------------------------------------
workbook = cells.Workbook(WORKBOOK_PATH)
print(f"[✓] Loaded workbook from {WORKBOOK_PATH}")

# ----------------------------------------------------------------------
# 2️⃣ Create GridJs server object
# ----------------------------------------------------------------------
grid = cells.GridJs(workbook)
print("[✓] GridJs instance ready")

# ----------------------------------------------------------------------
# 3️⃣ Enable spell check + formula checking
# ----------------------------------------------------------------------
grid.options["enableFormulaChecker"] = True
grid.options["enableSpellCheck"] = True
print("[✓] Spell check and formula checker enabled")

# ----------------------------------------------------------------------
# 4️⃣ Configure lazy loading for performance
# ----------------------------------------------------------------------
grid.options["lazyLoading"] = {"pageSize": PAGE_SIZE}
print(f"[✓] Lazy loading set to {PAGE_SIZE} rows per request")

# ----------------------------------------------------------------------
# 5️⃣ Export the workbook as JSON
# ----------------------------------------------------------------------
grid.save(OUTPUT_JSON)
print(f"[✓] Exported JSON to {OUTPUT_JSON}")
```

Save this as `export_gridjs.py` and run:

```bash
python export_gridjs.py
```

You should see a series of `[✓]` messages confirming each step succeeded.

---

## Common Questions & Edge Cases

**What if my workbook contains multiple sheets?**  
GridJs automatically iterates over every sheet, so the resulting JSON will have a `sheets` array. You can filter on the client side if you only need a subset.

**Can I disable spell check for a specific sheet?**  
The `options` dictionary applies globally. To toggle per‑sheet you’d need to create separate `GridJs` objects or post‑process the JSON.

**My file is larger than 10 MB—will lazy loading still help?**  
Absolutely. Lazy loading works at the API level; the server only streams the requested page. However, consider increasing the `pageSize` to 1000 if your network latency is low.

**Do I need to worry about Unicode characters?**  
`cells` handles UTF‑8 out of the box, so characters like emojis or non‑Latin scripts survive the round‑trip.

---

## Pro Tips for Production

* **Cache the JSON** – If the workbook rarely changes, cache `grid_data.json` in a CDN for lightning‑fast loads.  
* **Security** – Never expose the raw Excel file; serve only the generated JSON.  
* **Versioning** – Include a version number in the JSON filename (e.g., `grid_data_v2.json`) to avoid stale data after updates.  
* **Testing** – Write a small unit test that loads the JSON and checks that `enableSpellCheck` is `true`. It catches regressions early.

---

## Conclusion

You now have a solid, end‑to‑end recipe to **enable spell check** while you **export Excel JSON** using GridJs. From **loading excel workbook** to **configuring lazy loading** and finally **convert xlsx to json**, the process is straightforward and ready for production.  

Next steps? Try plugging the generated `grid_data.json` into a simple HTML page that uses the GridJs client library, experiment with custom cell renderers, or add authentication around the JSON endpoint. The sky’s the limit when you combine spell checking, lazy loading, and seamless Excel‑to‑JSON conversion.

Got more questions or a tricky workbook you’re wrestling with? Drop a comment below, and happy coding!  

---

![Enable spell check in GridJs](/images/enable-spell-check-gridjs.png "Screenshot showing spell check enabled in GridJs UI")


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Export Excel to JSON](/cells/english/java/excel-import-export/export-excel-to-json/)
- [Import JSON Data into Excel Using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [How to Efficiently Filter Data While Loading Excel Workbooks Using Aspose.Cells in Java](/cells/english/java/data-analysis/filter-data-excel-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}