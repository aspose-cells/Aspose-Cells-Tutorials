---
category: general
date: 2026-09-05
description: Create Excel workbook in Python and add conditional formatting to highlight
  yesterday cells. Learn the full code and why each step matters.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: en
lastmod: 2026-09-05
og_description: Create Excel workbook in Python and add conditional formatting to
  highlight yesterday cells. Follow this step‑by‑step guide for a complete solution.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Create Excel workbook in Python – add conditional formatting
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Create Excel workbook in Python with conditional formatting
url: /python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel workbook in Python with conditional formatting

If you need to **create Excel workbook python** for a reporting task, this guide shows you how to generate a workbook and apply a conditional formatting rule that highlights yesterday’s dates. You’ll see the exact code, why each line exists, and how to adapt the solution for other date ranges.

Conditional formatting is a powerful way to draw attention to data that meets a specific condition. In this tutorial we use the Aspose.Cells library for Python via .NET, which provides full Excel feature support without requiring Microsoft Office. By the end of the guide you will have a file where cells in the range *I19:K20* turn pink when they contain yesterday’s date.

## Prerequisites

Before you start, make sure you have:

* Python 3.9+ installed
* `aspose-cells` package (install with `pip install aspose-cells`)
* Basic familiarity with Python syntax
* Write permission to the directory where the workbook will be saved

The code works on Windows, macOS, and Linux as long as the .NET runtime is available.

## Create Excel workbook in Python

The first step is to instantiate a `Workbook` object and grab the default worksheet. This object represents the entire Excel file in memory.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Why this matters*: `Workbook()` creates an empty workbook with a single worksheet. Accessing `worksheets[0]` gives you a handle to add data, styles, and formatting later.

## Add conditional formatting range

Next we define the area that will be evaluated by the conditional rule. The range `I19:K20` covers six cells across two rows.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Why this matters*: Adding a conditional formatting collection to a specific range isolates the rule, preventing it from affecting unrelated cells. This satisfies the **add conditional formatting range** requirement.

## Define the rule: highlight cells based on date

We now create a condition of type `TIME_PERIOD`. This tells Excel to compare each cell’s value against a predefined time window.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Why this matters*: `TIME_PERIOD` is the only built‑in type that directly supports “Yesterday”, “Today”, “Last Week”, etc. By setting `condition.time_period` to `YESTERDAY`, the rule automatically evaluates each cell’s date value against the day before the current date.

## Style the cells that meet the condition

Conditional formatting also needs a visual style. Here we choose a pink solid fill to make the matching cells stand out.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Why this matters*: The style object defines how Excel will render cells that meet the condition. Using a solid pink fill satisfies the **highlight cells based on date** requirement and makes the result easy to verify.

## Populate sample dates for evaluation

To see the rule in action we insert two dates—one that falls on yesterday’s date and one that does not. The `number` format `30` corresponds to the built‑in date format `mm-dd-yy`.

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*Why this matters*: Providing both a matching and a non‑matching date lets you verify that the conditional formatting works correctly. Adjust the dates to the current month when you run the script, or replace them with dynamic values.

## Save the workbook

Finally we write the file to disk. The `SaveFormat.XLSX` constant ensures the output is a modern Excel file.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Why this matters*: Persisting the workbook lets you open it in Excel, LibreOffice, or any viewer that supports XLSX. The printed path confirms where the file was written.

## Full script

Putting all pieces together, the complete, runnable script looks like this:

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Expected output

When you open `TimePeriodExample.xlsx`:

* Cell **I19** appears with a pink background because its value matches yesterday.
* Cell **K20** retains the default background because its date is outside the period.
* The label **“Yesterday”** sits in cell I20 for clarity.

## Common variations and edge cases

| Situation | Adjustment |
|-----------|------------|
| **Highlight today instead of yesterday** | Change `condition.time_period = TimePeriodType.TODAY`. |
| **Apply the rule to a larger area** | Update the range string in `add("I19:K20")` to something like `"A1:Z100"`. |
| **Use a different fill color** | Replace `DrawingColor.pink` with any other `DrawingColor` (e.g., `DrawingColor.light_green`). |
| **Work with dynamic dates** | Compute `datetime.now() - timedelta(days=1)` for yesterday and write that value into the cells before applying the rule. |

**Pro tip:** When you generate the workbook programmatically for many users, keep the conditional formatting definition separate from data insertion. That way you can reuse the same style across multiple sheets without duplicating code.

## Verify the result programmatically (optional)

If you want to confirm the formatting without opening Excel, you can inspect the style of a cell after saving:

```python
# Load the saved file
loaded_wb = Workbook(output_path)
loaded_ws = loaded_wb.worksheets[0]
styled_cell = loaded_ws.cells.get


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}