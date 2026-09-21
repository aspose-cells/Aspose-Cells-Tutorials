---
category: general
date: 2026-09-21
description: Learn how to create Excel workbook in Python, set cell background color,
  and apply date based conditional formatting with Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: en
lastmod: 2026-09-21
og_description: Create Excel workbook in Python, set cell background color, and apply
  date based conditional formatting using Aspose.Cells. Follow the step‑by‑step guide.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Create Excel workbook in Python with conditional formatting
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Create Excel workbook in Python using conditional formatting
url: /python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel workbook in Python using conditional formatting

If you need to **create Excel workbook python** scripts that highlight dates automatically, this guide shows you exactly how. You’ll see how to **set cell background color**, add a “Yesterday” rule, and save the file—all with Aspose.Cells for Python.

Working with Excel files programmatically often means repeating the same formatting logic across many sheets. By the end of this tutorial you’ll have a reusable pattern for **excel conditional formatting python** that you can drop into any project.

## Prerequisites

- Python 3.8+ installed  
- `aspose-cells` package (`pip install aspose-cells`)  
- Basic familiarity with Python functions and the datetime module  

No additional libraries are required; Aspose.Cells handles all Excel operations.

## Step 1: Create the workbook and access the first worksheet

The first step is to **create excel workbook python** objects and grab the default worksheet. This gives you a clean canvas for further styling.

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Why this matters:* `Workbook()` creates an in‑memory Excel file. Accessing `worksheets[0]` avoids hard‑coding sheet names and works even if the default name changes.

## Step 2: Helper to add a TIME_PERIOD conditional format

To keep the code tidy, we wrap the conditional‑format creation in a helper. It receives a cell range, a background colour, and the desired time‑period rule.

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*Why this matters:* The helper abstracts the repetitive steps of creating a conditional format, making it easy to reuse for other date‑based rules such as “Today” or “Last Week”.

## Step 3: Apply the “Yesterday” rule to a range

Now we use the helper to highlight cells that contain yesterday’s date. The range `I19:K20` will turn **medium sea green** when the condition is met.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Why this matters:* `TimePeriodType.YESTERDAY` is part of Aspose.Cells’ built‑in enumeration, so you don’t need to calculate dates manually. The library evaluates the rule each time the workbook opens.

## Step 4: Populate the range with sample dates

To see the rule in action, we write two dates—one that matches “Yesterday” and one that does not. The `number` style `30` corresponds to a built‑in date format.

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*Why this matters:* By inserting concrete dates you can verify that the conditional formatting works without needing to open the file on a specific day.

## Step 5: Add a descriptive label and auto‑fit the column

A small label clarifies the purpose of the formatted range, and `auto_fit_column` makes the sheet readable.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## Step 6: Save the workbook

Finally, write the workbook to disk. The `os.makedirs` call ensures the target folder exists.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

When you open *TimePeriodDemo.xlsx* you’ll see:

- Cell **I19** shaded **medium sea green** because its value matches the “Yesterday” rule.  
- Cell **K20** retains the default background because its date does not satisfy the condition.  

This demonstrates **format cells by date** using a single line of Python code.

## Full, runnable example

Putting all pieces together, here’s the complete script you can copy‑paste and run:

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Run the script, open the resulting file, and you’ll see the conditional formatting in action.

## Common variations and edge cases

| Variation | How to implement | When to use |
|-----------|------------------|-------------|
| **Highlight “Today”** | Replace `TimePeriodType.YESTERDAY` with `TimePeriodType.TODAY` | Real‑time dashboards |
| **Multiple ranges** | Call `add_time_period` for each range, passing different colors | Complex reports |
| **Dynamic date range** | Use `TimePeriodType.LAST_7_DAYS` or `TimePeriodType.NEXT_MONTH` | Rolling reports |
| **Custom color** | Use `Color.from_argb(255, r, g, b)` to create any shade | Brand‑consistent styling |

**Pro tip:** Always set `condition.style.pattern = BackgroundType.SOLID` when you want a solid fill; otherwise Excel may display a gradient that looks inconsistent across versions.

## Conclusion

You now know how to **create Excel workbook python** scripts that **set cell background color**, apply **excel conditional formatting python**, and **format cells by date** using Aspose.Cells. The example covers a **date based conditional formatting** scenario, but the same pattern works for any time‑period rule.

Next, you might explore:

- Adding data bars or icon sets (`FormatConditionType.DATA_BAR`)  
- Combining multiple conditional rules on the same range  
- Exporting the workbook to PDF (`SaveFormat.PDF`) for reporting  

Feel free to experiment with different colours, ranges, and time‑period types to fit your specific reporting needs. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel Automation with Aspose.Cells .NET&#58; Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}