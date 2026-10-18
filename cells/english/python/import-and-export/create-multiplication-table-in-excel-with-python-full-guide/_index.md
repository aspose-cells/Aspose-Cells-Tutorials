---
category: general
date: 2026-06-21
description: Create multiplication table in Excel using Python. Learn how to use lambda,
  how to use makearray, display excel array and read excel values python in a step‑by‑step
  tutorial.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: en
og_description: Create multiplication table in Excel using Python. This tutorial shows
  how to use lambda, makearray, display excel array and read excel values python efficiently.
og_title: Create multiplication table in Excel with Python – Complete Guide
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: Create multiplication table in Excel with Python – Full Guide
url: /python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create multiplication table in Excel with Python – Full Guide

Ever wondered how to **create multiplication table** in Excel without manually typing each cell? You're not alone. In many reporting scenarios you need a quick 5×5 (or larger) grid of products, and doing it by hand is a waste of time.  

In this tutorial we’ll walk through a clean, Python‑driven way to generate that table, embed it with a `MAKEARRAY` formula, and then pull the results back into your script. Along the way we’ll answer **how to use lambda**, show **how to use makearray**, and demonstrate **display excel array** as well as **read excel values python**—all in one cohesive example.

By the end you’ll have a reusable snippet that works with any workbook, and you’ll understand why this approach is both fast and future‑proof.

## What You’ll Need

- Python 3.8+ (the latest stable release is fine)
- The `openpyxl` library (or any Excel‑aware library that supports formulas)
- A basic understanding of lambda expressions in Python
- No special Excel add‑ins; the native `MAKEARRAY` function (available in Excel 365) does the heavy lifting

If you’re missing any of these, just `pip install openpyxl` and you’re good to go.

## Create multiplication table – Overview

The core idea is simple: we create a fresh workbook, write a `MAKEARRAY` formula that builds a 5 × 5 multiplication matrix, force Excel to calculate it, and finally read the resulting values back into Python.

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Running the script prints:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

That’s a fully‑functional **create multiplication table** in Excel, generated entirely from Python.

### Why use `MAKEARRAY` instead of a Python loop?

- **Performance**: Excel handles the calculation natively, which is faster for large matrices.
- **Live updating**: If you later change the dimensions in the formula, the sheet auto‑recalculates.
- **Readability**: The formula expresses intent (“make an array”) directly, keeping your Python code tidy.

## How to use lambda in Python for Excel formulas

The `LAMBDA` part of the `MAKEARRAY` call is an Excel‑side anonymous function, not a Python lambda. Still, the concept is the same: you define a small, inline piece of logic that takes `r` (row index) and `c` (column index) and returns `r*c`.  

If you’re new to **how to use lambda** in the Excel world, think of it as a mini‑function that lives only inside the formula. No need to declare a separate function elsewhere. In Python we simply embed the string:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

That line tells Excel: *“For each cell in a 5‑by‑5 block, compute row × column.”*  

Because the lambda is evaluated by Excel, you don’t have to worry about Python’s own lambda syntax here—just the Excel syntax.

## How to use makearray to generate arrays

`MAKEARRAY` is a relatively new addition to the Excel function library (available in Microsoft 365 as of 2022). It replaces older tricks like `INDEX` + `ROW`/`COLUMN` combos. The signature is:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – number of rows you want.
- **columns** – number of columns you want.
- **lambda** – an Excel LAMBDA that receives `(row, column)` and returns a value.

In our example we passed `5,5` for a classic multiplication table, but you could easily change those numbers:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

That would give you a 10 × 10 table without touching any Python loops. This demonstrates **how to use makearray** for any kind of deterministic grid, whether it’s a lookup table, a heatmap, or a financial schedule.

## Display excel array – pulling the data back into Python

Once Excel has calculated the formula, the resulting values reside in the sheet just like any manually‑entered cell. To **display excel array**, we iterate over the range and print each row:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

A couple of tips:

- Use `worksheet.cell(row, column).value` rather than the dictionary‑style indexing if you need to handle larger ranges; it’s a tad faster.
- If you want a prettier table, consider `tabulate` or `pandas.DataFrame` to format the output.

Below is a screenshot of the resulting sheet (the image alt text includes the primary keyword for SEO):

![Screenshot showing create multiplication table in Excel using Python](/images/multiplication-table-excel.png)

## Read excel values python – extracting the matrix for further processing

Often the next step after **display excel array** is to feed those numbers into a data‑analysis pipeline. That’s where **read excel values python** shines. The same loop we used for printing can be repurposed to build a list of lists, a NumPy array, or a Pandas DataFrame:

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

Output:

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

Now you have a fully‑typed DataFrame that you can plot, export to CSV, or feed into a machine‑learning model. This completes the **read excel values python** part of the workflow.

## Edge Cases & Practical Tips

- **Formula recalculation**: If you modify the workbook after the initial `calculate_formula()` call, you must invoke it again; otherwise the cached array stays stale.
- **Non‑365 Excel**: Older Excel versions don’t support `MAKEARRAY`. In that case fall back to a Python‑generated table and write each cell individually.
- **Large tables**: For matrices larger than ~100 × 100, consider streaming the data to avoid loading the entire sheet into memory.
- **Error handling**: Wrap the calculation and reading steps in `try/except` blocks to catch `InvalidFileException` or `FormulaError`.

## Conclusion

We’ve just shown you how to **create multiplication table** in Excel using Python, leveraging the power of **how to use lambda** and **how to use makearray**. You’ve seen how to **display excel array**, read those values back with **read excel values python**, and even turn the result into a Pandas DataFrame for downstream analysis.

Want to go further? Try swapping the multiplication logic for something more complex—maybe a distance matrix, a probability table, or a dynamic pricing grid. The same pattern applies: one line of `MAKEARRAY`, a quick `calculate_formula()`, and a handful of Python loops to pull the data out.

If you found this guide helpful, give it a star on GitHub, share it with teammates, or drop a comment with your own use‑case. Happy coding, and enjoy the brevity of generating Excel tables with a single formula!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET Tutorial: How to Create and Modify Excel Workbooks Easily](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [How to Create and Style Named Ranges in Excel Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}