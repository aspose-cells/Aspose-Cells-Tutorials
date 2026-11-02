---
category: general
date: 2026-07-20
description: Create Excel workbook Python with Aspose.Cells, set cell background color,
  and add conditional formatting python to style cells by date.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: en
lastmod: 2026-07-20
og_description: Create Excel workbook Python using Aspose.Cells. Learn how to set
  cell background color and add conditional formatting python to format cells by date.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Create Excel Workbook Python – Add Conditional Formatting
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: Create Excel Workbook Python – Conditional Formatting Guide
url: /python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook Python – Conditional Formatting Guide

Ever wondered how to **create Excel workbook Python** from scratch and make it look polished without opening the UI? You’re not alone. Many developers hit a wall when they need to **set cell background color** or apply date‑based styles programmatically.  

In this tutorial we’ll walk through a complete, runnable example that uses Aspose.Cells to **add conditional formatting python** rules, format cells by date, and save the result as a modern XLSX file. By the end you’ll have a self‑contained script you can drop into any project.

## What You’ll Learn

- How to initialize a workbook and grab the first worksheet.  
- Ways to **set cell background color** for an entire range.  
- Using **aspose cells conditional formatting** to highlight “Yesterday” dates.  
- Auto‑fitting columns and persisting the file to disk.  

No external configuration is required—just Python 3 and the Aspose.Cells package. If you’ve already installed `aspose-cells`, you’re good to go; otherwise a quick `pip install aspose-cells` will do.

## Prerequisites

- Python 3.8+ (the code works on 3.9, 3.10, and newer).  
- Aspose.Cells for Python via .NET (`aspose-cells` NuGet wrapper).  
- Basic familiarity with Excel concepts (cells, ranges, formatting).  

Got those? Great—let’s dive in.

## Create Excel Workbook Python – Setup and Worksheet

First things first: we need a fresh workbook object and a reference to the default worksheet. This is the canvas where all later operations will happen.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **Why this matters:** `Workbook()` constructs an in‑memory Excel file, eliminating the need for any temporary files. The `worksheet` variable is our entry point for cell‑level actions.

## Set Cell Background Color

Before we add any rules, it’s nice to give the target range a base colour so the conditional formatting stands out. The helper below both retrieves (or creates) a `FormatConditionCollection` for a given range and paints the cells with a solid background.

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **Pro tip:** If you plan to reuse the same range with multiple rules, call this helper once and keep the returned collection; it saves a few API calls.

## Add Conditional Formatting Python for Date Ranges

Now the fun part: we’ll create a **time‑period conditional formatting** rule that highlights cells containing yesterday’s date. This demonstrates the power of **format cells by date** using Aspose.Cells.

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **Why use `TIME_PERIOD`?** It abstracts away the need to write custom formulas. Aspose.Cells evaluates the date against the current system date, so the rule always stays relevant.

### Running the Rule

```python
apply_yesterday_rule()
```

When you open the resulting file, cells `I19` will glow pink (because they are “Yesterday”), while `K20` remains the base green colour.

## Auto‑Fit Columns and Save Workbook

A tidy spreadsheet looks professional. Auto‑fitting ensures our data isn’t cramped.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Edge case:** If you target a directory that doesn’t exist, `workbook.save` will raise an error. Wrap the save call in a `try/except` block if you need graceful handling.

### Full Script (Copy‑Paste Ready)

Below is the entire script, ready to run. Just replace `YOUR_DIRECTORY` with a valid folder on your machine.

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Running this script will produce `TimePeriodExample.xlsx` with the conditional formatting we described.

## Common Questions & Tips

- **Can I target a different date range?**  
  Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample dates accordingly.

- **What if I need a custom formula instead of `YESTERDAY`?**  
  Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for example, `=TODAY()-A1=1` to mimic yesterday.

- **How do I apply multiple rules to the same range?**  
  Call `conditions.add_condition` again with a different `FormatConditionType`. The order matters; later rules can override earlier ones.

- **Is there a way to set font colour together with background?**  
  Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).

## Conclusion

You now know how to **create Excel workbook Python** using Aspose.Cells, **set cell background color**, and **add conditional formatting python** that formats cells by date. The script is fully functional, handles edge cases like missing directories, and can be extended to more sophisticated scenarios such as multi‑rule conditional logic or dynamic range detection.

Ready for the next step? Try swapping the “Yesterday” rule for “Last Week”, experiment with gradient fills, or generate a full report with dozens of formatted tables. The building blocks are all here, and you’ve just mastered the core of **aspose cells conditional formatting** in Python.

Happy coding, and feel free to share your own variations in the comments!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}