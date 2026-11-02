---
category: general
date: 2026-03-01
description: How to insert rows in GridJs made easy—learn to add 100 rows, create
  empty rows, and check total rows in just a few lines of C#.
draft: false
keywords:
- how to insert rows
- add multiple rows
- add 100 rows
- create empty rows
- check total rows
language: en
og_description: How to insert rows in GridJs quickly. This guide shows you how to
  add multiple rows, create empty rows, and check total rows with clean C# code.
og_title: How to Insert Rows in GridJs – Fast Guide
tags:
- C#
- GridJs
- data‑grid
title: How to Insert Rows in GridJs – Add Multiple Rows Quickly
url: /net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Insert Rows in GridJs – Add Multiple Rows Quickly

Ever wondered **how to insert rows** into a GridJs data‑grid without writing a loop that drags on forever? You're not the only one. In many enterprise apps you’ll hit a point where you need to make space for a bulk import, a template, or just a placeholder for future data. The good news? GridJs gives you a single method that does the heavy lifting for you.

In this tutorial we’ll walk through a complete, runnable example that shows you how to **add 100 rows**, **create empty rows**, and **check total rows** after the operation. By the end you’ll have a solid pattern you can drop into any C# project that uses GridJs.

## Prerequisites

Before we dive in, make sure you have:

- .NET 6.0 or later (the API works the same on .NET Framework 4.8, but the newer SDK gives you nicer tooling).
- A reference to the `GridJs` NuGet package or the compiled DLL that contains the `GridJs` class.
- Basic familiarity with C# syntax—nothing exotic, just standard `using` statements and object‑oriented basics.

If any of those raise a red flag, pause for a minute and get them sorted. The steps that follow assume the grid object is already instantiated and ready to accept rows.

![how to insert rows illustration](gridjs-insert-rows.png)

## Step 1: Set Up the Grid Instance

First things first, you need a `GridJs` object. In a real‑world app this would probably come from a service layer or be injected via dependency injection, but for clarity we’ll create it locally.

```csharp
using System;
using GridJsLibrary;   // <-- replace with the actual namespace of GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create or obtain the grid you want to modify
            GridJs gridJs = new GridJs();   // replace with your actual grid initialization
```

> **Why this matters:** Instantiating the grid gives you a clean slate, ensuring that the row‑insertion logic won’t clash with leftover state from previous runs.

## Step 2: Insert 100 Rows at a Specific Index

Now comes the core of **how to insert rows**. The `InsertRows` method takes two arguments: the zero‑based start index and the number of rows you want to add. Let’s insert 100 rows starting at row 5.

```csharp
            // Step 2: Insert 100 rows starting at row index 5 (zero‑based)
            // This pushes existing rows down and creates space for new data.
            gridJs.InsertRows(5, 100);
```

> **Pro tip:** If you need to add rows at the very end of the grid, you can use `gridJs.RowCount` as the start index. That way you’re effectively “appending” rather than inserting.

### What Happens Under the Hood?

- **Memory Allocation:** `InsertRows` allocates a block of empty row objects internally, so you don’t have to manually instantiate each one.
- **Index Shifting:** All rows that were at index 5 or later move down by 100 positions, preserving their original data.
- **Performance:** Because the operation is handled in a single call, it’s usually faster than looping `InsertRow` 100 times.

## Step 3: Verify the Insertion (Check Total Rows)

After you’ve added rows, it’s a good habit to **check total rows** to confirm the operation succeeded. The `RowCount` property gives you the current number of rows in the grid.

```csharp
            // Step 3: (Optional) Verify the insertion or continue processing
            int newRowCount = gridJs.RowCount; // example property to check total rows
            Console.WriteLine($"Grid now contains {newRowCount} rows.");
```

If you started with, say, 20 rows, you should see `120` printed to the console. This simple verification step can save you hours of debugging later on.

## Step 4: Populate the Newly Created Empty Rows (Optional)

Often you’ll want to fill those freshly created rows with placeholder data or default objects. Since `InsertRows` gives you a block of empty rows, you can loop over the range and assign values.

```csharp
            // Optional: Fill the newly created rows with default values
            for (int i = 5; i < 5 + 100; i++)
            {
                var row = gridJs.GetRow(i); // assume GetRow returns a mutable row object
                row["Name"] = $"Placeholder {i - 4}";
                row["CreatedOn"] = DateTime.UtcNow;
            }

            // Verify a sample row
            var sample = gridJs.GetRow(5);
            Console.WriteLine($"First inserted row name: {sample["Name"]}");
        }
    }
}
```

> **Why you might do this:** Creating empty rows is handy when you need a template for user input, a batch upload placeholder, or simply want to reserve space for future calculations.

## Common Variations & Edge Cases

### Adding Fewer Than 100 Rows

If you only need to **add multiple rows**—say 10 or 25—the same `InsertRows` call works; just replace `100` with the desired count.

```csharp
gridJs.InsertRows(startIndex, 25); // adds 25 rows
```

### Inserting at the Top of the Grid

Want to prepend rows? Use `0` as the start index:

```csharp
gridJs.InsertRows(0, 5); // adds 5 rows at the very beginning
```

### Handling Out‑Of‑Range Indices

Passing an index larger than `RowCount` throws an `ArgumentOutOfRangeException`. Guard against this:

```csharp
int safeIndex = Math.Min(requestedIndex, gridJs.RowCount);
gridJs.InsertRows(safeIndex, 100);
```

### Dealing with Read‑Only Grids

Some GridJs configurations expose a read‑only view. In that scenario, you’ll need to switch to a writable instance or temporarily disable the read‑only flag before calling `InsertRows`.

## Performance Tips

- **Batch Operations:** If you’re inserting rows repeatedly in a loop, batch them into a single `InsertRows` call whenever possible. This reduces internal list reallocations.
- **Avoid UI Refreshes:** In UI‑bound grids, suspend rendering (`gridJs.BeginUpdate()`) before inserting rows and resume (`gridJs.EndUpdate()`) afterward to prevent flicker.
- **Memory Profiling:** Large inserts (e.g., >10,000 rows) can spike memory usage. Consider paging or streaming data instead of a single massive insert.

## Full Working Example Recap

Putting everything together, here’s the complete, copy‑and‑paste‑ready program:

```csharp
using System;
using GridJsLibrary;   // replace with the actual namespace

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create the grid instance
            GridJs gridJs = new GridJs();

            // Insert 100 rows starting at index 5
            gridJs.InsertRows(5, 100);

            // Verify insertion
            int newRowCount = gridJs.RowCount;
            Console.WriteLine($"Grid now contains {newRowCount} rows.");

            // Optional: Fill new rows with placeholder data
            for (int i = 5; i < 5 + 100; i++)
            {
                var row = gridJs.GetRow(i);
                row["Name"] = $"Placeholder {i - 4}";
                row["CreatedOn"] = DateTime.UtcNow;
            }

            // Show a sample row
            var sample = gridJs.GetRow(5);
            Console.WriteLine($"First inserted row name: {sample["Name"]}");
        }
    }
}
```

Run this program, and you’ll see the console output confirming the row count and the name of the first placeholder row. That’s the entire answer to **how to insert rows** in GridJs, complete with verification and optional data population.

## Conclusion

We’ve walked through a clear, end‑to‑end solution for **how to insert rows** in GridJs, covering how to **add 100 rows**, **create empty rows**, and **check total rows** after the operation. The pattern scales—just tweak the start index and count to **add multiple rows** wherever you need them.  

Next steps? Try combining this technique with bulk data imports from CSV files, or experiment with conditional row creation based on user input. If you’re curious about deleting rows, sorting, or applying conditional formatting, those are natural extensions of the same API surface.

Happy coding, and may your grids always stay perfectly sized!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}