---
category: general
date: 2026-10-04
description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
  formatting python, cell background color python, and format cells date python in
  a full example.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: en
lastmod: 2026-10-04
og_description: Create Excel workbook python with Aspose.Cells. This tutorial shows
  excel conditional formatting python, cell background color python, and format cells
  date python step‑by‑step.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Create Excel workbook python – full guide with conditional formatting
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Create Excel workbook python with conditional formatting and cell background
  color
url: /python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel workbook python with conditional formatting and cell background color

If you need to **create Excel workbook python** quickly, this guide shows you exactly how. You’ll see a complete, runnable example that adds **excel conditional formatting python**, changes the **cell background color python**, and **format cells date python** for a “Yesterday” highlight.  

In many reporting scenarios the visual cue of a colored cell makes the data instantly understandable. This tutorial walks you through every line of code, explains why each step matters, and gives you a ready‑to‑run script you can adapt to your own projects.

## What you’ll accomplish

By the end of this article you will be able to:

1. **create Excel workbook python** using the Aspose.Cells library.  
2. Apply **excel conditional formatting python** that automatically highlights dates that fall on “Yesterday”.  
3. Set the **cell background color python** to pink (or any color you prefer).  
4. **format cells date python** so the dates appear in the standard Excel date style.  

No prior experience with Aspose.Cells is required—just a working Python 3 environment and pip access.

## Prerequisites

- Python 3.8 or newer installed.  
- `aspose-cells` and `aspose-pydrawing` packages installed via `pip install aspose-cells aspose-pydrawing`.  
- Basic familiarity with Python syntax and Excel concepts (workbooks, worksheets, cells).  

> **Pro tip:** If you run the script in a virtual environment, you avoid version conflicts with other projects.

## Step 1: Set up the project and import required classes

The first step when you **create Excel workbook python** is to import the Aspose.Cells classes you’ll need. These classes give you direct access to workbook creation, conditional formatting, and styling.

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*Why this matters:* Importing only the needed symbols keeps the namespace tidy and makes the script easier to read. `Workbook` is the entry point for **create Excel workbook python**, while `FormatConditionType` and `TimePeriodType` are essential for **excel conditional formatting python**.

## Step 2: Create a new workbook and obtain the first worksheet

Now we actually **create Excel workbook python**. The `Workbook()` constructor gives you an empty Excel file with a default worksheet.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Explanation:* Every Excel file starts with at least one worksheet. By default Aspose.Cells names it “Sheet1”. You can add more sheets later, but for this demonstration a single sheet keeps the example focused.

## Step 3: Define the target range for conditional formatting

Conditional formatting works on a rectangular range. Here we choose the range `I19:K20`, which gives us three columns and two rows to play with.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Why we do this:* The `get` method returns a `ConditionalFormatting` object tied to the specified range. If the range does not yet have any formatting, Aspose.Cells creates a new collection automatically.

## Step 4: Add a TIME_PERIOD condition and set the background color

This is the core of **excel conditional formatting python**. We add a `TIME_PERIOD` rule that highlights cells containing dates that fall on “Yesterday”.

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*Deep dive:*  
- `FormatConditionType.TIME_PERIOD` tells Excel to evaluate dates relative to the current date.  
- `TimePeriodType.YESTERDAY` is a built‑in enum that automatically updates each day, so the workbook always highlights the most recent “Yesterday”.  
- By setting `background_color` to `Color.pink` and the pattern to `SOLID`, we achieve the **cell background color python** effect without extra VBA code.

## Step 5: Populate the range with sample dates and apply date formatting

To see the conditional formatting in action, we need real date values. We also need to **format cells date python** so Excel treats them as dates rather than plain numbers.

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*Explanation:*  
- The `style.number = 30` line is the **format cells date python** step. Format code 30 corresponds to the short date format (`m/d/yy`).  
- Using a helper function keeps the code DRY (Don’t Repeat Yourself) and makes it easy to add more dates later.

## Step 6: Add a descriptive label

A small label helps anyone opening the workbook understand why the cells are colored.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## Step 7: Save the workbook to disk

Finally, we **create Excel workbook python** on disk by calling `save`. The `SaveFormat.XLSX` constant ensures the file is in the modern Office Open XML format.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

When you open `TimePeriodDemo.xlsx` in Excel, you’ll see:

- Cells `I19` and `K20` contain dates.  
- The cell that matches “Yesterday” (in this static example, `I19`) is highlighted pink.  
- The label “Yesterday” appears in `I20`.  

> **Tip:** If you run the script on a different day, the conditional formatting still highlights the cell whose date is exactly one day before the current system date—no code changes required.

## Full script – ready to copy and run

Below is the complete, self‑contained program that incorporates all the steps above. Copy it into a file named `conditional_format_demo.py`, adjust `YOUR_DIRECTORY`, and execute with `python conditional_format_demo.py`.

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Expected output

Running the script prints a confirmation line:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Opening the generated file shows the pink background on the cell that matches the “Yesterday” rule, confirming that **excel conditional formatting python** and **cell background color python** are working together.

## Common variations and edge cases

| Situation | How to adapt the code |
|-----------|-----------------------|
| **Different highlight color** | Change `Color.pink` to any other `Color` constant, e.g., `Color.light_green`. |
| **Highlight “Today” instead of “Yesterday”** | Set `condition.time_period = TimePeriodType.TODAY`. |
| **Apply formatting to an entire column** | Use a range like `"A:A"` and adjust the `target_range` variable accordingly. |
| **Use a custom date format** | Replace `style.number = 30` with `style.custom = "dd-mmm-yyyy"` for a more readable format. |
| **Multiple conditions on the same range**


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}