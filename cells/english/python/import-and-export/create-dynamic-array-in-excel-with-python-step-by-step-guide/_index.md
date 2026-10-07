---
category: general
date: 2026-06-21
description: Create dynamic array using Python and the SEQUENCE function in Excel.
  Learn to read formula result, recalculate Excel formulas, and see an Excel SEQUENCE
  example.
draft: false
keywords:
- create dynamic array
- sequence function excel
- read formula result
- recalculate excel formulas
- excel sequence example
language: en
og_description: Create dynamic array in Excel using Python. This tutorial shows how
  to use the SEQUENCE function, recalculate Excel formulas, and read formula result.
og_title: Create Dynamic Array in Excel with Python – Complete Guide
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create dynamic array using Python and the SEQUENCE function in Excel.
    Learn to read formula result, recalculate Excel formulas, and see an Excel SEQUENCE
    example.
  headline: Create Dynamic Array in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
tags:
- excel
- python
- xlwings
- dynamic arrays
title: Create Dynamic Array in Excel with Python – Step‑by‑Step Guide
url: /python/import-and-export/create-dynamic-array-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Dynamic Array in Excel with Python – Complete Guide

Ever wondered how to **create dynamic array** formulas in Excel without leaving your Python script? You're not the only one. Whether you're automating a monthly report or building a lightweight data‑engine, being able to drop a `SEQUENCE` formula into a workbook, recalculate, and pull the spill range back into Python is a game‑changer.

In this tutorial we'll walk through a real‑world **excel sequence example**, show you how to **read formula result**, and explain the best way to **recalculate excel formulas** after you inject new logic. By the end you’ll have a self‑contained script you can copy‑paste, run, and adapt to your own needs.

## What You'll Learn

- How the `SEQUENCE` function works and why it’s perfect for generating matrices.
- The difference between a regular cell value and a spill range address.
- Using `wb.calculate_formula()` (or its equivalent) to force Excel to evaluate new formulas.
- Extracting the address of a dynamic array with `ANCHORARRAY`.
- A full, runnable Python example that you can drop into any project.

No prior experience with Excel’s new dynamic‑array engine is required—just a basic familiarity with Python and a library like **xlwings** that can talk to Excel.

---

## How to Create Dynamic Array with SEQUENCE in Excel Using Python

The first step is to write a **dynamic array** formula directly into a worksheet cell. In modern Excel, the `SEQUENCE` function can generate a matrix of numbers on the fly. Here’s the syntax we’ll use:

```python
# Step 1: Write a dynamic array formula that generates a 3×2 matrix starting at 10 with step 5
ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"   # Returns a 3×2 array
```

**Why `SEQUENCE`?**  
Think of it as Excel’s built‑in `range()` for spreadsheets. It lets you specify rows, columns, a start value, and an increment—all in one tidy line. In our case we ask for 3 rows and 2 columns, beginning at 10 and stepping by 5, which yields:

|   | A | B |
|---|---|---|
|1|10|15|
|2|20|25|
|3|30|35|

Because the formula lives in `A1`, Excel automatically “spills” the result into the neighboring cells `A1:B3`. That spill is what we’ll later retrieve.

---

## Using the SEQUENCE Function in Excel – A Quick Excel Sequence Example

If you open Excel manually and type `=SEQUENCE(3,2,10,5)` in a cell, you’ll see the same matrix appear instantly. The function is part of Excel’s **dynamic array** engine introduced in Office 365, which means:

- No need for Ctrl+Shift+Enter.
- The result can expand or contract automatically.
- You can reference the entire spill range with functions like `@` or `#`.

In Python, the only difference is that we assign the formula as a string to the cell’s `.formula` property. The library takes care of the rest.

---

## Retrieving the Spill Range Address with ANCHORARRAY

Once the dynamic array is in place, you often need to know where Excel actually placed the values. That’s where `ANCHORARRAY` shines. It returns the address of the top‑left cell of the spill range—exactly what we need to read back into our script.

```python
# Step 2: Retrieve the address of the spill range produced by the formula in A1
ws.cells["C1"].formula = "=ANCHORARRAY(A1)"      # Returns the address of the spill range
```

Placing this formula in `C1` gives us a text string like `"A1:B3"`. Notice we’re **reading the formula result** as a plain value, not as another formula. This tiny trick avoids the need to parse the worksheet manually.

---

## Recalculating Excel Formulas and Reading the Result

Excel doesn’t always recalculate instantly when a new formula is injected from an external script. To guarantee that the workbook reflects the latest changes, we explicitly trigger a calculation pass.

```python
# Step 3: Recalculate all formulas in the workbook and read the result
wb.calculate_formula()               # Forces Excel to evaluate pending formulas
print(ws.cells["C1"].value)          # → "A1:B3"
```

**Why call `calculate_formula()`?**  
If you skip this step, `ws.cells["C1"].value` might still return `None` or an old address because Excel is still busy updating its dependency tree. By forcing a recalculation we ensure the **read formula result** is up‑to‑date.

---

## Full Script – From Start to Finish

Below is a complete, ready‑to‑run example that ties everything together. It assumes you have **xlwings** installed (`pip install xlwings`) and that Excel is available on your machine.

```python
import xlwings as xw

def create_dynamic_array_example():
    # Open a new workbook (or attach to an existing one)
    wb = xw.Book()               # Creates a fresh Excel workbook
    ws = wb.sheets[0]            # Grab the first worksheet

    # 1️⃣ Write the SEQUENCE formula – this creates a 3×2 matrix starting at 10, step 5
    ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"

    # 2️⃣ Use ANCHORARRAY to capture the spill range address in C1
    ws.cells["C1"].formula = "=ANCHORARRAY(A1)"

    # 3️⃣ Force Excel to recalculate so that the ANCHORARRAY result is current
    wb.calculate_formula()

    # 4️⃣ Read back the address – this is our **read formula result** step
    spill_address = ws.cells["C1"].value
    print(f"The dynamic array spills into: {spill_address}")

    # 5️⃣ Optionally, fetch the actual values from the spill range
    # xlwings can read a range by address, so we demonstrate that too
    data = ws.range(spill_address).value
    print("Matrix values:")
    for row in data:
        print(row)

    # Clean up – close without saving to keep the demo tidy
    wb.close(save=False)

if __name__ == "__main__":
    create_dynamic_array_example()
```

### Expected Output

```
The dynamic array spills into: A1:B3
Matrix values:
[10, 15]
[20, 25]
[30, 35]
```

Running the script will open Excel, inject the `SEQUENCE` formula, recalculate, and then print both the spill address and the matrix itself. No manual clicks required.

---

## Common Pitfalls and Pro Tips

- **Pitfall:** Forgetting `wb.calculate_formula()`.  
  *Result:* `C1` stays blank or shows a stale address.  
  *Fix:* Always trigger a calculation after writing new formulas.

- **Pitfall:** Using an older version of Excel that lacks the `SEQUENCE` function.  
  *Result:* `#NAME?` error.  
  *Fix:* Ensure you have Office 365 or Excel 2021+.

- **Pro tip:** If you need the spill range for further processing (e.g., charting), you can feed the address directly into `ws.range(spill_address)` as shown above.

- **Pro tip:** `ANCHORARRAY` works with any dynamic array, not just `SEQUENCE`. Swap in `=SORT(A2:A10)` or `=FILTER(...)` and you’ll still get the correct spill address.

- **Edge case:** When the target area is already occupied, Excel will return a `#SPILL!` error. In that case, either clear the destination range first or move the formula to a different cell.

---

## Extending the Example – What Next?

Now that you know how to **create dynamic array** formulas, **read formula result**, and **recalculate excel formulas**, you can explore more advanced scenarios:

- **Dynamic chart data** – feed a spill range into a chart source and let the chart grow automatically.
- **Conditional formatting** – apply rules to the spill range using its address.
- **Cross‑workbook references** – write a dynamic array in one workbook and pull the data into another via `xlwings` links.

Each of these builds on the core concepts covered here, so feel free to experiment. The only limit is your imagination (and maybe Excel’s maximum rows/columns).

---

## Conclusion

We’ve just walked through a complete workflow to **create dynamic array** formulas in Excel from Python, use the **SEQUENCE function excel**, retrieve the spill range with **ANCHORARRAY**, **recalculate excel formulas**, and finally **read formula result** back into your script. The short example demonstrates how powerful Excel’s new dynamic‑array engine can be when paired with automation tools like **xlwings**.

Give it a try in your own projects, tweak the matrix dimensions, or replace `SEQUENCE` with any other dynamic function. As you get comfortable, you’ll find that automating Excel becomes not only possible but pleasantly straightforward.

Got questions or want to share how you extended this pattern? Drop a comment below, and happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Processing Data Using Array Function in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)
- [Create Dynamic Line Charts in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Create Dynamic Excel Charts with Aspose.Cells Java&#58; A Comprehensive Guide for Developers](/cells/english/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}