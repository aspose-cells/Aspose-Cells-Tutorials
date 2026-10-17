---
category: general
date: 2026-08-24
description: Create conditional formatting rule in Python using Aspose.Cells to highlight
  dates, with auto‑fit column and background color formatting.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: en
lastmod: 2026-08-24
og_description: Create conditional formatting rule in Python with Aspose.Cells. Learn
  how to highlight dates, set background colors, and auto‑fit columns in just a few
  lines of code.
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: Create a conditional formatting rule for dates in Python – step‑by‑step
  guide
schemas:
- author: Aspose
  dateModified: '2026-08-24'
  description: Create conditional formatting rule in Python using Aspose.Cells to
    highlight dates, with auto‑fit column and background color formatting.
  headline: How to create conditional formatting rule for dates in Python
  type: TechArticle
tags:
- Aspose.Cells
- Python
- Excel automation
- Conditional formatting
title: How to create conditional formatting rule for dates in Python
url: /python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create conditional formatting rule for dates in Python

If you need to **create conditional formatting rule** that reacts to dates, this guide shows you exactly how to do it with Aspose.Cells for Python. Whether you’re building a reporting dashboard or an automated spreadsheet, you’ll see how to highlight yesterday’s dates, apply a custom background color, and **auto fit column** widths so the result looks polished.

In this tutorial we’ll cover **conditional formatting by date**, demonstrate a **background color conditional format**, and finish with saving the workbook as an XLSX file. By the end you’ll have a reusable helper that you can adapt to any **date based conditional format** you require.

## What you’ll learn

* Set up a workbook and worksheet using Aspose.Cells.
* Write a helper function that adds a **date based conditional format** to any cell range.
* Populate cells with sample dates so the rule can be evaluated.
* Apply **auto fit column** to make the content readable.
* Save the workbook and verify the highlighted cells.

The only prerequisite is a working Python environment with the `aspose-cells` package installed.

## Prerequisites

| Requirement | Details |
|-------------|---------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Basic knowledge of Excel concepts | worksheets, cells, formatting |
| Optional: IDE (VS Code, PyCharm, etc.) | any editor that can run Python scripts |

## Step 1: Create a workbook and get the first worksheet

The first step is to **create conditional formatting rule**‑ready objects: a `Workbook` and its default `Worksheet`. These objects are the entry point for all subsequent operations.

```python
# Step 1 – initialize workbook and worksheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create a new, empty workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Why this matters:* The `Workbook` holds the entire Excel file, while the `Worksheet` is where you apply cells, styles, and **conditional formatting by date**. Without these objects the rest of the code has nowhere to act.

## Step 2: Build a helper to add a TIME_PERIOD conditional format

Rather than repeating the same boiler‑plate for each range, we encapsulate the logic in a helper function. This function attaches a **background color conditional format** that colors cells based on a `TimePeriodType` (e.g., Yesterday, Today, LastWeek).

```python
def add_time_period_condition(cell_range: str, bg_color: Color, period: TimePeriodType):
    """
    Attach a TIME_PERIOD conditional format to `cell_range`.
    The rule highlights cells that fall within `period` using `bg_color`.

    Args:
        cell_range: A1‑style range string, e.g., "I19:K20".
        bg_color:   Desired background color for matching cells.
        period:     Aspose.Cells TimePeriodType enum value.
    Returns:
        The FormatConditionCollection for further customization if needed.
    """
    # 1️⃣ Attach a new ConditionalFormatting block to the specified range
    worksheet.conditional_formattings.add(cell_range)

    # 2️⃣ Grab the collection of conditions for that block
    conditions = worksheet.conditional_formattings[-1].format_conditions

    # 3️⃣ (Optional) Set a default background for the whole range
    conditions.back_color = bg_color

    # 4️⃣ Add a TIME_PERIOD condition and configure its appearance
    idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[idx]

    # Apply the visual style – pink background in this example
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Define which period triggers the formatting
    condition.time_period = period

    return conditions
```

*Why we use a helper:* It isolates the **date based conditional format** logic, making the code easier to read, test, and reuse across multiple sheets or projects.

## Step 3: Apply the conditional formatting rule to a specific range

Now we use the helper to highlight cells that contain “Yesterday”. This is the core of our **create conditional formatting rule** operation.

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

When the workbook is opened, any cell in `I19:K20` whose date equals yesterday’s date will appear with a pink fill (the style we set in the helper). The `bg_color` argument shows how you can layer a default background behind the conditional color if desired.

## Step 4: Populate the range with sample dates

A conditional rule only becomes visible after the worksheet contains data that satisfies the condition. We’ll insert two dates: one that matches “Yesterday” and another that falls outside the period.

```python
# Step 4 – insert sample dates for demonstration

# Cell I19 will match the YESTERDAY period
yesterday_cell = worksheet.cells.get("I19")
yesterday_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008 is “yesterday” relative to 31‑Jul‑2008
yesterday_cell.get_style().number = 30          # 30 = built‑in date format
yesterday_cell.set_style(yesterday_cell.get_style())

# Cell K20 will NOT match the period (it’s a later date)
outside_cell = worksheet.cells.get("K20")
outside_cell.put_value(datetime(2008, 8, 3))     # 03‑Aug‑2008 is outside “Yesterday”
outside_cell.get_style().number = 30
outside_cell.set_style(outside_cell.get_style())

# Optional label for clarity – not part of the rule
worksheet.cells.get("I20").put_value("Yesterday")
```

*Why this matters:* By using `datetime` objects we ensure Excel treats the values as true dates, which is required for **conditional formatting by date** to work correctly. The numeric format (`30`) guarantees the cells display as recognizable dates.

## Step 5: Auto‑fit the column and save the workbook

After the data and formatting are in place, the final polish is to **auto fit column** widths so the dates are fully visible. Then we write the file to disk.

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

The `auto_fit_column` call examines the longest content in column 12 (which corresponds to column **L** in Excel) and expands the width accordingly. This small step prevents truncated dates and makes the **background color conditional format** clearly visible.

### Expected result

When you open `TimePeriodDemo.out.xlsx`:

| I19 (date) | I20 (label) | K20 (date) |
|------------|------------|------------|
| 30‑Jul‑2008 (highlighted pink) | Yesterday | 03‑Aug‑2008 (no highlight) |

* The cell with yesterday’s date shows a pink background because the **create conditional formatting rule** matched the `YESTERDAY` period.
* All other cells retain the default background (or the optional `medium_sea_green` you supplied).
* Column L is automatically widened, so the dates are fully readable.

## Common variations and edge cases

| Situation | How to adapt the code |
|-----------|-----------------------|
| **Highlight “Today” instead of “Yesterday”** | Replace `TimePeriodType.YESTERDAY` with `TimePeriodType.TODAY`. |
| **Use a different background color** | Change `condition.style.background_color = Color.pink` to any other `Color` (e.g., `Color.light_sky_blue`). |
| **Apply the rule to a non‑contiguous range** | Call `add_time_period_condition` multiple times with different `cell_range` strings (e.g., `"A1:A10", "C1:C10"`). |
| **Work with a pre‑existing workbook** | Load the file with `Workbook("myfile.xlsx")` instead of creating a new one. |
| **Multiple date‑based conditions on the same range** | After the first `add_time_period_condition` call, add another condition with `conditions.add_condition(FormatConditionType.TIME_PERIOD)` and set a different `time_period`. |

## Conclusion

You now know how to **create conditional formatting rule** that reacts to dates, apply a **background color conditional format**, and **auto fit column** widths using Aspose.Cells for Python. The helper function abstracts the logic, letting you reuse the same pattern for any **conditional formatting by date** scenario—whether it’s “Yesterday”, “LastWeek”, or a custom range.

Next, you might explore:

* Adding **icon sets** or **data bars** alongside date rules.
* Generating dynamic reports that pull dates from a database.
* Combining multiple **date based conditional format** rules on a single sheet.

Feel free to experiment with different colors, periods, and ranges to fit your project’s needs. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [How to Extract Conditional Formatting Colors Using Aspose.Cells for .NET](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}