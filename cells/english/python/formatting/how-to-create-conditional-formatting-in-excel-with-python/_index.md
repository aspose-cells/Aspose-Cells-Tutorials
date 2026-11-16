---
category: general
date: 2026-11-16
description: Create conditional formatting in Excel using Python. Learn to add a conditional
  formatting range, highlight dates, and build a workbook programmatically.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: en
lastmod: 2026-11-16
og_description: Create conditional formatting in Excel with Python. This tutorial
  shows how to add a conditional formatting range, highlight dates, and generate a
  workbook.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Create conditional formatting in Excel with Python – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: How to create conditional formatting in Excel with Python
url: /python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create conditional formatting in Excel with Python

If you need to **create conditional formatting** in an Excel file while working in Python, this guide shows you exactly how to do it. You’ll learn to **create excel workbook python**‑style, define a formatting range, and highlight dates without leaving the IDE.

Conditional formatting lets you visually flag cells that meet specific criteria—perfect for dashboards, reports, or data‑validation sheets. By the end of this tutorial you will have a fully‑functional workbook that colors cells dated “Yesterday” in pink while the rest of the range stays green.

## What you’ll accomplish

* Build a new workbook from scratch.  
* Add a conditional‑format collection for a specific cell block.  
* Apply a **TIME_PERIOD** rule that highlights dates (the “how to highlight dates” scenario).  
* Save the file as an XLSX workbook ready for downstream processing.

**Prerequisites**  
* Python 3.8+  
* `aspose-cells` Python package (`pip install aspose-cells`)  
* Basic familiarity with Python’s `datetime` module  

---

## How to create conditional formatting in Python

The first step is to set up the workbook and the worksheet that will host the formatting rules.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Why this matters** – `Workbook` is the entry point for all Excel operations. Creating the workbook programmatically replaces the manual “File → New” step, enabling automated report pipelines.

---

## Preparing the conditional‑format collection – add conditional formatting range

Next we define the cell block that will receive the rule. In this example the range is **I19:K20**.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Explanation** – `conditional_formattings.add` registers a new collection tied to the address string. The first condition (`conds[0]`) works as a “default” style; the later rule will override it when its criteria are met.

---

## Adding a TIME_PERIOD condition – how to highlight dates

Now we add the actual logic that identifies “Yesterday” dates and paints them pink.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Why use TIME_PERIOD?** – Aspose.Cells provides built‑in enumerations like `YESTERDAY`, `TODAY`, and `LAST_WEEK`. They evaluate the cell’s date value against the current system date, removing the need for custom formulas.

---

## Populating sample data – demonstrate the rule

To see the formatting in action we insert a date that matches the rule and another that does not.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Edge case note** – The `TIME_PERIOD` rule works with *real* dates only. If a cell contains text (e.g., “N/A”), the rule is ignored, preventing unexpected color changes.

---

## Saving the workbook – add conditional formatting python

Finally, write the workbook to disk. The file can be opened in any spreadsheet program to verify the colors.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Expected result**  

| I19 (green → pink) | J19 (green) | K19 (green) |
|--------------------|------------|------------|
| 7/30/2008 (yesterday) | – | – |
| **I20**: “Yesterday” label | – | – |
| I21‑K21 (green)    | – | – |

The cell **I19** appears with a pink background because its date matches the “Yesterday” period, while **K20** remains green.

---

## Common questions and practical tips

* **Can I use a custom date range instead of a built‑in period?**  
  Yes. Replace `condition.time_period` with `condition.formula1 = "TODAY()-1"` and set `condition.type = FormatConditionType.FORMULA`.

* **What if my workbook already contains data?**  
  Use `worksheet.cells.import_data` to bulk‑load data before adding the conditional formatting collection.

* **Performance with large sheets?**  
  Adding many conditions can slow down rendering. Group cells with the same rule into a single range (e.g., “A1:C1000”) to keep the condition count low.

* **Cross‑platform compatibility?**  
  The generated XLSX file follows the Office Open XML standard, so it works on Windows, macOS, and Linux spreadsheet applications.

---

## Conclusion

You now know how to **create conditional formatting** in an Excel workbook using Python. The tutorial covered creating the workbook, defining an **add conditional formatting range**, applying a **how to highlight dates** rule, and saving the file—all with the **add conditional formatting python** approach provided by Aspose.Cells.

From here you can:

* Extend the rule set with other `TimePeriodType` values (e.g., `TODAY`, `LAST_MONTH`).  
* Combine multiple conditions on the same range for richer visual cues.  
* Integrate this workflow into automated reporting pipelines or web services.

Happy coding, and feel free to experiment with different colors, ranges, and date logic to suit your reporting needs!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}