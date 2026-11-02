---
category: general
date: 2026-10-07
description: Create Excel workbook in Python, set cell background color, auto‑fit
  columns, and populate dates in Excel with a concise code example.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: en
lastmod: 2026-10-07
og_description: Create Excel workbook in Python, then set cell background color, auto‑fit
  columns, and populate dates in Excel. Follow this step‑by‑step guide to generate
  a TimePeriodDemo.xlsx file.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Create Excel workbook in Python – set background & auto‑fit
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: Create Excel workbook in Python and set cell background
url: /python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel workbook in Python and set cell background

Create Excel workbook in Python and apply conditional formatting with just a few lines of code. This tutorial shows you **how to create excel** files programmatically, set cell background color, auto‑fit Excel columns, and populate dates in Excel using the Aspose.Cells library.

You’ll learn how to:
* Initialize a workbook and obtain the first worksheet.  
* Define a conditional format that highlights “Yesterday” dates.  
* Insert sample dates into specific cells.  
* Auto‑fit columns so the data is clearly visible.  
* Save the workbook to a chosen folder.

The only prerequisite is a working Python 3 environment with the `aspose-cells` and `aspose-pydrawing` packages installed:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Create Excel workbook in Python – step by step

The following sections break the process into manageable steps. Each step includes the required code, an explanation of **why** it matters, and a tip to avoid common pitfalls.

### Step 1: Import required namespaces and define a helper function

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Why this matters*: Importing the correct classes gives you access to workbook creation, conditional formatting, and color handling.  
**Pro tip**: Keep imports at the top of the file; it makes the script easier to read and prevents circular‑import errors.

### Step 2: Create the workbook and get the first worksheet

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

The `Workbook()` constructor creates an empty Excel workbook in memory.  
**Why**: Starting with a fresh workbook ensures no leftover formatting from previous runs.

### Step 3: Set cell background color with a conditional format

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*Why*: Using a **time period** condition automatically highlights any cell that contains yesterday’s date, eliminating manual date checks.  
**Tip**: `Color.pink` is just an example; you can use any `Color` object (`Color.yellow`, `Color.light_green`, etc.).

### Step 4: Populate dates in Excel

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

Here we **populate dates in Excel** cells `I19` and `K20`. The first date will trigger the conditional formatting, while the second will not.  
**Why this matters**: Demonstrating both matching and non‑matching values helps you verify that the rule works as expected.

### Step 5: Auto‑fit Excel columns for better visibility

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` adjusts the column width based on the longest cell value.  
**Tip**: Call this after you have written all data; otherwise the width might be calculated on incomplete content.

### Step 6: Save the workbook

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

Saving the file writes the in‑memory workbook to disk in the modern XLSX format.  

### Full script – putting it all together

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**Expected output**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Open the generated file in Excel – cells `I19:K20` will show a pink background for the date that falls on “Yesterday,” and column L will be wide enough to display the label without clipping.

---

## Why this approach works best

* **Single‑pass workflow** – All operations happen on the same `Workbook` instance, avoiding unnecessary I/O.  
* **Conditional formatting** – Using `FormatConditionType.TIME_PERIOD` lets Excel handle date logic, which is more reliable than writing custom Python date checks.  
* **Explicit styling** – Setting `background_color` and `pattern` guarantees the visual result across Excel versions.  
* **Auto‑fit after data


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook Python – Full Guide](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Create Excel Workbook Python – Complete Step‑by‑Step Guide](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}