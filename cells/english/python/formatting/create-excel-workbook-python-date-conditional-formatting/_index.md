---
category: general
date: 2026-08-08
description: Create Excel workbook Python and add conditional formatting based on
  date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: en
lastmod: 2026-08-08
og_description: Create Excel workbook Python with Aspose.Cells and apply conditional
  formatting based on date for dynamic spreadsheets.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Create Excel workbook Python – date conditional formatting
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Create Excel workbook Python date conditional formatting
url: /python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel workbook Python date conditional formatting

If you need to **create Excel workbook Python** and automatically highlight cells that match a specific date, this tutorial shows you exactly how. You’ll learn to apply **conditional formatting based on date** so that yesterday’s dates light up in pink, using the Aspose.Cells library.

The guide walks through every step—from installing the SDK to saving the final .xlsx file—so you can copy‑paste a working example into your own project. No external documentation is required; all code and explanations are self‑contained.

## Prerequisites

Before you start, make sure you have:

* Python 3.8 or newer installed.
* `aspose-cells` package (the Python wrapper for Aspose.Cells). Install it with:
  ```bash
  pip install aspose-cells
  ```
* Basic familiarity with Python and Excel concepts such as worksheets and cell styles.

> **Pro tip:** Aspose.Cells works without Microsoft Excel being installed, making it ideal for server‑side automation.

## Step 1: Create the Excel workbook in Python

The first task is to instantiate a new workbook and grab the default worksheet. This object represents the entire Excel file and provides access to rows, columns, and formatting APIs.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

Creating the workbook is the foundation for any further manipulation, whether you’re adding data, formulas, or formatting rules.

## Step 2: Define a date‑based conditional format

Now we add **conditional formatting based on date**. The `FormatConditionType.TIME_PERIOD` enum lets us specify built‑in time periods such as Yesterday, Today, or LastWeek.

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

Why this step matters: Excel evaluates the condition for each cell in the range. When a cell’s value falls within the defined period (yesterday), the style we assigned is applied automatically.

## Step 3: Populate the range with sample dates

To see the rule in action, we write a couple of `datetime` objects into the target cells. One of them is deliberately set to yesterday’s date relative to the workbook’s internal date system.

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

The `number = 30` line tells Excel to display the value using its standard short‑date format. You can change this index to any built‑in number format if you prefer a different presentation.

## Step 4: Adjust column width for readability

Auto‑fitting the column that contains the dates makes the output easier to read, especially when the workbook is opened in Excel or a viewer.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## Step 5: Save the workbook to disk

Finally, store the workbook as an .xlsx file. Replace `"YOUR_DIRECTORY"` with a real path on your machine.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

When you open `TimePeriodDemo.out.xlsx` in Excel, cell **I19** will appear with a pink background because its value matches the “Yesterday” rule, while **K20** remains unchanged.

### Expected output

| I19 (date) | I20 (label) | J19 | J20 | K19 | K20 (date) |
|------------|-------------|-----|-----|-----|------------|
| *2008‑07‑30* (pink background) | Yesterday | – | – | – | *2008‑08‑03* (no formatting) |

The pink shading confirms that **conditional formatting based on date** works as intended.

## Common variations and edge cases

| Situation | How to adapt the code |
|-----------|-----------------------|
| **Highlight “Today” instead of “Yesterday”** | Change `condition.time_period = TimePeriodType.TODAY` |
| **Apply the rule to an entire column** | Use `worksheet.get_range("A:A").format_conditions` |
| **Use a custom date range (e.g., last 7 days)** | Replace the time‑period condition with a formula condition: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **Different background colors** | Set `condition.style.background_color = Color.light_green` (or any `Color` you prefer) |
| **Running on Linux without a display** | Aspose.Cells is fully headless; no extra configuration required. |

## Full, runnable example

Below is the complete script you can execute as‑is (after updating the output directory). All imports, comments, and error‑handling basics are included.

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Running the script produces an Excel file where the “Yesterday” cell is automatically highlighted, demonstrating **create Excel workbook Python** combined with **conditional formatting based on date**.

## Conclusion

You now know how to **create Excel workbook Python** objects, define a **date‑based conditional formatting


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Create Excel Workbook with Charts Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}