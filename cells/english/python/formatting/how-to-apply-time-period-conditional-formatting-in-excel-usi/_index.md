---
category: general
date: 2026-09-15
description: Learn how to apply time period conditional formatting and save workbook
  as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: en
lastmod: 2026-09-15
og_description: Apply time period conditional formatting in Excel using Python and
  save workbook as XLSX. Follow this complete guide for Aspose.Cells.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Apply time period conditional formatting in Excel with Python
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: How to apply time period conditional formatting in Excel using Python
url: /python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to apply time period conditional formatting in Excel using Python

If you need **time period conditional formatting** in an Excel file, this tutorial shows you exactly how to do it with Python. You’ll see a complete, runnable example that creates a workbook, highlights yesterday’s dates, and **save workbook as XLSX** in just a few lines of code.

Conditional formatting is a powerful way to draw attention to data that meets a specific rule. In this guide we focus on the “Yesterday” time period, but the same pattern works for other built‑in periods such as Today, LastWeek, and NextMonth. By the end of the tutorial you will be able to **how to create excel workbook python**‑style scripts that are ready for production.

## Prerequisites

- Python 3.8+ installed  
- `aspose-cells` and `aspose-pydrawing` packages (`pip install aspose-cells aspose-pydrawing`)  
- Basic familiarity with Python syntax  

No additional Office installation is required because Aspose.Cells handles the file generation internally.

## Time period conditional formatting with Aspose.Cells in Python

This section walks through every line of code needed for the primary task. The code block below is the full script; comments explain the purpose of each step.

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### Why each step matters

1. **Creating the workbook** gives you an in‑memory Excel file you can manipulate without opening Excel.  
2. **Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies, keeping the logic isolated.  
3. **Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`. This avoids manual date calculations and automatically updates when the file is opened on a different day.  
4. **Setting the style** (`background_color` and `pattern`) determines how the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.  
5. **Writing sample dates** with number format 30 ensures Excel displays them as short dates rather than serial numbers.  
6. **Auto‑fitting the column** improves readability for anyone opening the file later.  
7. **Saving as XLSX** produces a widely compatible file that can be opened in Excel, Google Sheets, or any modern spreadsheet program.

## How to create Excel workbook Python‑style with Aspose.Cells

The script above already demonstrates the minimal steps to **how to create excel workbook python**. In practice you may want to:

- Add multiple worksheets (`workbook.worksheets.add("Report")`).  
- Populate large data tables with loops or pandas DataFrames (`worksheet.cells.import_data_table`).  
- Apply additional formatting (fonts, borders) using `cell.get_style()`.

All of these actions follow the same pattern: obtain the object, modify its properties, and call `set_style` or `save`.

## Add conditional formatting Python – other useful patterns

Beyond the “Yesterday” example, Aspose.Cells supports several conditional‑formatting types:

| FormatConditionType | Typical use case |
|---------------------|------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | Custom formulas (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | Simple comparisons (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | Gradient colour scales |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | In‑cell bar visualisation |

To **add conditional formatting python** for a numeric threshold, you would replace `FormatConditionType.TIME_PERIOD` with `FormatConditionType.CELL_VALUE` and set `condition.operator_type` and `condition.formula1`.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Save workbook as XLSX – best practices

When you **save workbook as xlsx**, consider:

- **Specifying the correct `SaveFormat`** (`SaveFormat.XLSX`) to avoid legacy formats.  
- **Using a deterministic file name** if the script runs in a loop (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Closing resources** (`workbook.dispose()`) in long‑running services to free native memory.

The example already uses `SaveFormat.XLSX`, which produces a modern, zip‑based workbook that retains all conditional‑formatting rules.

## Highlight yesterday in Excel – verification steps

After running the script, open `TimePeriodExample.xlsx`:

1. Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.  
2. The cell `I20` shows the text “Yesterday”.  
3. If you change your system date to **July 30 2008** and reopen the file, the cells with matching dates are automatically filled with pink.  
4. Changing the system date to any other day removes the pink fill, confirming the rule reacts to the **time period conditional formatting** logic.

## Common pitfalls and how to avoid them

- **Missing `aspose-pydrawing`** – the `Color` class lives in this package; forgetting to install it raises an `ImportError`.  
- **Incorrect number format** – using the default General format shows serial numbers (e.g., 39822). Always set `style.number = 30` for short dates.  
- **Range mismatch** – the conditional formatting range must include the cells you intend to highlight; otherwise the rule has no effect.

## Pro tip: reuse the formatting routine

If you need the same “Yesterday” rule in multiple workbooks, wrap the logic in a helper function:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Call `apply_yesterday_highlight(worksheet, "A1:A10")` wherever needed.

## Conclusion

This guide showed you how to implement **time period conditional formatting** in Excel using Python, how to **save workbook as XLSX**, and how to **highlight yesterday in Excel** with a single, reusable script. You now have a solid foundation to **add conditional formatting python** code to any automation project, whether you’re generating daily reports, building dashboards, or preparing data exports.

**Next steps**

- Explore other `TimePeriodType` values such as `TODAY` or `LAST_WEEK`.  
- Combine multiple conditional rules on the same range for richer visual cues.  
- Integrate the workbook generation into a web service or scheduled job.

Happy coding, and enjoy the visual clarity that conditional formatting brings to your Excel automation!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET : A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Master Aspose.Cells .NET : Apply Conditional Formatting to Alternate Rows in Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}