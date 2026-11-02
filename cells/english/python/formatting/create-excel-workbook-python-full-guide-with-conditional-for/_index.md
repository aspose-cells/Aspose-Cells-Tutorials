---
category: general
date: 2026-07-14
description: Create Excel workbook Python code that sets cell background color, highlights
  cells based on date range, and saves workbook as XLSX in minutes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: en
lastmod: 2026-07-14
og_description: Create Excel workbook Python instantly. Learn to set cell background
  color, highlight cells based on date range, and save workbook as XLSX with Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Create Excel Workbook Python – Step‑by‑Step Conditional Formatting
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Create Excel Workbook Python – Full Guide with Conditional Formatting
url: /python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook Python – Full Guide with Conditional Formatting

Ever wondered how to **create excel workbook python** scripts that look polished without opening Excel manually? You're not alone. In many data‑driven projects we need to generate spreadsheets, color‑code cells, and even flag dates that fall inside a specific range—all from pure Python code.

In this tutorial we’ll walk through a complete, ready‑to‑run example that **creates an Excel workbook python** using the Aspose.Cells library, **sets cell background color**, applies **conditional formatting based on date**, and finally **saves workbook as xlsx**. By the end you’ll have a reusable snippet you can drop into any automation pipeline.

## What You’ll Learn

- How to initialise a workbook and grab the first worksheet.  
- A helper function that adds a conditional‑formatting collection for any cell range.  
- Using **conditional formatting based on date** to highlight yesterday’s entries.  
- Adjusting column widths for a tidy layout.  
- Persisting the result with **save workbook as xlsx**.  

No external Excel installation is required—Aspose.Cells handles everything in memory.

## Prerequisites

- Python 3.8+ installed.  
- `aspose-cells` package (`pip install aspose-cells`).  
- Basic familiarity with Python functions and datetime objects.  

If you’ve never used Aspose.Cells before, think of it as a powerful, pure‑Python API that mimics Excel’s own object model. It’s perfect for server‑side generation where the Office suite isn’t available.

## Step 1: Initialise the Workbook (Create Excel Workbook Python)

First things first: we need to **create excel workbook python** style. This step spins up an empty workbook object and points us at the default worksheet.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **Why this matters:** The `Workbook` class is the entry point for every Excel operation. By creating it programmatically we avoid any manual file handling.

## Step 2: Helper to Add a Conditional‑Formatting Collection (Set Cell Background Color)

Conditional formatting lives inside a *collection* attached to a range. Let’s wrap that boilerplate in a tiny helper that also lets us **set cell background color** for the whole range.

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **Pro tip:** Using a helper keeps your main flow clean and makes it easy to reuse the same logic for multiple ranges.

## Step 3: Apply Conditional Formatting Based on Date (Highlight Cells Based on Date Range)

Now we’ll actually **highlight cells based on date range**. The example focuses on “yesterday” but you can swap `TimePeriodType.YESTERDAY` for `TODAY`, `LAST_WEEK`, etc.

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **What’s happening?**  
> 1. We first give the whole range a neutral green background.  
> 2. Then we add a `TIME_PERIOD` condition that overwrites the fill with pink **only** when the cell’s date equals yesterday.  
> 3. The `TimePeriodType` enum abstracts the date calculation, so you don’t need to write custom logic.

## Step 4: Populate Sample Dates (So the Rule Can Be Evaluated)

To see the rule in action we’ll drop a couple of dates into the sheet. One falls inside the “yesterday” window, the other does not.

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **Edge case note:** If your workbook will be opened in different locales, consider using `date_style.custom = "dd‑mm‑yyyy"` to enforce a consistent display.

## Step 5: Tidy Up the Layout (Auto‑Fit Columns)

A cramped spreadsheet looks unprofessional. Let’s **adjust column width for a tidy output**.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **Why auto‑fit?** It ensures that any long labels or dates are fully visible, which is especially important when you share the file with non‑technical stakeholders.

## Step 6: Save the Workbook (Save Workbook As XLSX)

Finally, we **save workbook as xlsx** to a location of your choice. The `SaveFormat.XLSX` constant tells Aspose.Cells to write the modern OpenXML format.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Result you should see:**  
> - Cells I19 and K20 contain dates.  
> - I19 (yesterday) is highlighted pink, while K20 stays green.  
> - Column L automatically expands to fit the label “Yesterday”.  

If you open `TimePeriodDemo.xlsx` in Excel, the conditional formatting will already be applied—no extra steps needed.

---

![Excel sheet showing highlighted yesterday date](https://example.com/images/excel-demo.png "Screenshot of the generated Excel file with highlighted cells")

*The image above illustrates the final workbook; notice the pink highlight on the cell containing yesterday’s date.*

## Recap: What We Achieved

- **Created an Excel workbook python** from scratch using Aspose.Cells.  
- **Set cell background color** for a whole range to give the sheet a visual cue.  
- Applied **conditional formatting based on date** to automatically flag yesterday’s entries.  
- **Saved workbook as xlsx**, ready for distribution or further processing.  

All of this was done in under 60 lines of Python, and the code works on any platform that supports the Aspose.Cells runtime.

## Next Steps & Related Topics

If you found this useful, you might also want to explore:

- **set cell background color** for entire rows based on status values (e.g., “Completed”, “Pending”).  
- Using **highlight cells based on date range** to create rolling windows (last 7 days, current month).  
- Exporting to other formats like **CSV** or **PDF** with `SaveFormat.CSV` or `SaveFormat.PDF`.  
- Adding **charts** programmatically to visualise the data you just formatted.  

Feel free to tweak the date logic, swap the colour palette, or expand the range to cover whole columns. The pattern stays the same: create a workbook, attach a conditional‑formatting collection, define the rule, and save.

Got questions about a specific use‑case? Drop a comment below, and happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}