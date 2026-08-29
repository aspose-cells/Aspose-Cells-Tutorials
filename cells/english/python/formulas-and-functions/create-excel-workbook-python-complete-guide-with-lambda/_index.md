---
category: general
date: 2026-06-08
description: Create Excel workbook Python example that shows how to use lambda in
  Excel, sum rows with BYROW, and automate calculations in a few steps.
draft: false
keywords:
- create excel workbook python
- how to use lambda
- how to sum rows
- use lambda excel
language: en
og_description: Create Excel workbook Python and learn how to use lambda in Excel
  to sum rows efficiently with BYROW formulas.
og_title: Create Excel Workbook Python – Complete Guide
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook Python example that shows how to use lambda in
    Excel, sum rows with BYROW, and automate calculations in a few steps.
  headline: Create Excel Workbook Python – Complete Guide with Lambda
  type: TechArticle
tags:
- python
- excel
- automation
title: Create Excel Workbook Python – Complete Guide with Lambda
url: /python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook Python – Complete Guide with Lambda

Ever wondered how to **create Excel workbook Python** scripts that automate boring number‑crunching? You're not alone—many developers hit a wall when they need to generate a sheet, drop a formula in, and pull the results back into their code.  

In this tutorial we'll also show **how to use lambda** in Excel, explain **how to sum rows** with the modern `BYROW` function, and give you a tidy, end‑to‑end example that you can copy‑paste and run today.

## What You’ll Learn

- Set up a fresh workbook from Python without opening Excel manually.  
- Fill a range with a 3 × 3 matrix of numbers.  
- Insert a `BYROW` formula that leverages **use lambda excel** syntax to sum each row.  
- Recalculate the sheet so the formula evaluates, then read the results back into Python.  

By the end of this guide you’ll have a self‑contained script you can adapt for invoices, score‑cards, or any situation where you need to **sum rows** on the fly.

### Prerequisites

- Python 3.8+ installed.  
- The `openpyxl` library (or `xlwings` if you prefer a COM‑based approach). We'll use `openpyxl` because it’s pure‑Python and works on all platforms.  
- A recent version of Microsoft Excel (365 or 2021) that supports the `BYROW` function and Lambda formulas.  

Install the library with:

```bash
pip install openpyxl
```

> **Pro tip:** If you run into permission issues on Windows, use `python -m pip install --user openpyxl`.

---

## Create Excel Workbook Python – Initialize Workbook

The first thing we need is a brand‑new workbook object that lives entirely in memory. With `openpyxl` this is a one‑liner:

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and grab the first worksheet
wb = Workbook()
ws = wb.active   # .active is the first sheet by default
```

Why do we use `wb.active` instead of indexing `Worksheets[0]`? `openpyxl` exposes the active sheet directly, which is clearer and avoids an extra list lookup. If you ever need to work with multiple sheets, you can always add them with `wb.create_sheet(title="MySheet")`.

---

## Fill the Worksheet with Data – A Simple 3×3 Matrix

Next, we populate the sheet with a small matrix. This mirrors the classic “sum each row” example and keeps the code compact.

```python
# Step 2: Define a 3×3 matrix of numbers
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Import the matrix into the worksheet starting at cell A1
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, value in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=value)
```

You might wonder why we loop manually instead of using `ws.append()` or `ws.values`. The explicit loops give us full control over the starting cell and make it easy to adjust offsets later—handy when you want to leave a header row or column blank.

---

## How to Use Lambda in Excel Formulas

Excel’s **use lambda excel** feature lets you write anonymous functions directly in a cell. Think of it as Python’s `lambda` but living inside the spreadsheet engine. The syntax is:

```
=LAMBDA(parameter1, parameter2, …, calculation)
```

When paired with `BYROW`, you can apply that lambda to each row of a range, producing a column of results. This is the core of our **how to sum rows** trick.

```python
# Step 3: Insert a BYROW formula that sums each row using a Lambda
ws["D1"] = "=BYROW(A1:C3, LAMBDA(r, SUM(r)))"
```

What’s happening under the hood?

- `A1:C3` is the source range (our matrix).  
- `LAMBDA(r, SUM(r))` defines a temporary function that receives a single row (`r`) and returns its sum.  
- `BYROW` runs that lambda for **each row** and spills the results into column D, starting at `D1`.  

Because `BYROW` is a *dynamic array* function, Excel automatically fills `D1:D3` with the three sums.

> **Note:** `BYROW` and Lambda formulas are only available in Excel 365/2021 and later. If you’re on an older version, you’ll need to fall back to traditional `SUM` formulas or VBA.

---

## How to Sum Rows with BYROW and Lambda

Now that the formula lives in the sheet, we must tell Excel to evaluate it. `openpyxl` itself doesn’t calculate formulas; it only reads/writes them. To trigger a calculation we can either:

1. Save the workbook and open it in Excel (manual).  
2. Use the `xlwings` COM engine to force recalculation (requires Excel installed).  

For a pure‑Python solution we’ll use `xlwings` just for the calculation step—nothing more.

```python
import xlwings as xw

# Step 4: Recalculate the workbook so the BYROW formula is evaluated
# Save the workbook to a temporary file first
temp_path = "temp_workbook.xlsx"
wb.save(temp_path)

# Open the file with xlwings, force a calculation, then close
app = xw.App(visible=False)
book = app.books.open(temp_path)
book.api.CalculateFull()          # Full recalculation
book.save()
book.close()
app.quit()
```

Why not call `wb.calculate()`? `openpyxl` lacks a native engine, so we lean on Excel itself via `xlwings`. The overhead is minimal for small sheets and gives us the exact result Excel would display.

---

## Recalculate and Retrieve Results – Pull the Sums Back into Python

Finally, we read the spilled results from column D. `openpyxl` makes this straightforward:

```python
# Step 5: Load the recalculated workbook and grab the results
wb = Workbook()  # re‑open the saved file
wb = xw.Book(temp_path).api  # alternative: use xlwings again to read values

# Using xlwings to fetch the range values as a Python list
results = xw.Range('D1:D3').value
print(results)   # Expected output: [6, 15, 24]
```

If you prefer to stay inside `openpyxl`, you can read the cells after the Excel recalculation:

```python
from openpyxl import load_workbook

wb = load_workbook(temp_path, data_only=True)  # data_only reads calculated values
ws = wb.active
results = [ws[f"D{row}"].value for row in range(1, 4)]
print(results)   # -> [6, 15, 24]
```

Both approaches give you the same list `[6, 15, 24]`, confirming that **how to sum rows** with `BYROW` + Lambda works as advertised.

---

## Edge Cases & Common Pitfalls

| Situation | What to Watch For | Fix |
|-----------|-------------------|-----|
| Excel version older than 365 | `BYROW` and `LAMBDA` appear as `#NAME?` | Use classic `=SUM(A1:C1)` copied down manually, or upgrade Excel. |
| Large matrices (10 k+ rows) | Recalculation can become slow | Call `book.api.CalculateFullRebuild()` only once, or split the workbook. |
| Running on a headless server without Excel | `xlwings` cannot launch Excel | Switch to a pure‑Python library like `pandas` + `numpy` for calculations, then write the results. |
| Locale issues (comma vs. semicolon) | Formula may be rejected | Use `ws["D1"].value = "=BYROW(A1:C3; LAMBDA(r; SUM(r)))"` for locales that use `;`. |

---

## Full Working Example (Copy‑Paste Ready)

```python
# ------------------------------------------------------------
# create_excel_workbook_python – full script
# ------------------------------------------------------------
import os
from openpyxl import Workbook, load_workbook
import xlwings as xw

# 1️⃣ Initialize workbook
wb = Workbook()
ws = wb.active

# 2️⃣ Populate with a 3×3 matrix
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, val in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=val)

# 3️⃣ Insert BYROW + Lambda formula


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook with Aspose.Cells Java - Complete Guide](/cells/english/java/automation-batch-processing/excel-automation-aspose-cells-java-guide/)
- [Create Excel Workbook & Automate Reports with Aspose.Cells](/cells/english/java/automation-batch-processing/aspose-cells-java-two-three-color-scales/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}