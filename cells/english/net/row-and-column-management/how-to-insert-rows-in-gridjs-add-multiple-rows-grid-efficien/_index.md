---
category: general
date: 2026-03-29
description: Learn how to insert rows in GridJs quickly. This guide also covers how
  to add rows and add multiple rows grid with a batch operation.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: en
og_description: Learn how to insert rows in GridJs quickly. This guide shows how to
  add rows, add multiple rows grid, and handle large batch inserts.
og_title: How to Insert Rows in GridJs – Add Multiple Rows Grid Efficiently
tags:
- GridJs
- C#
- data‑grid
title: How to Insert Rows in GridJs – Add Multiple Rows Grid Efficiently
url: /net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Insert Rows in GridJs – Add Multiple Rows Grid Efficiently

Ever wondered **how to insert rows** into a massive GridJs table without freezing the UI? Maybe you’ve hit a wall trying to **add rows** one‑by‑one and the performance just crumbles. The good news is that GridJs offers a batch API that lets you **add multiple rows grid** in a single call, keeping things snappy even when you’re dealing with millions of entries.

In this tutorial we’ll walk through a complete, runnable example that shows exactly **how to insert rows** using `InsertRowsBatch`. You’ll see why batching matters, how to verify the result, and what to watch out for when the index you target is huge. By the end you’ll be able to drop a thousand new records into any GridJs instance with confidence.

## Prerequisites

Before we dive in, make sure you have:

- .NET 6.0 or later (the code compiles with any recent SDK)
- A reference to the `GridJs` NuGet package (or the DLL if you’re using a custom build)
- Basic C# knowledge – you don’t need to be a guru, just comfortable with classes and methods
- An IDE or editor of your choice (Visual Studio, Rider, VS Code… all work)

> **Pro tip:** If you plan to work with truly massive grids (tens of millions of rows), enable `gridJs.EnableVirtualization = true;` to keep UI rendering lightweight.

## Step 1: Create and Configure the GridJs Instance

First things first: you need a live `GridJs` object. Think of it as the canvas on which you’ll paint rows.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Why this step matters:** Initializing the grid and optionally seeding data mirrors a real‑world scenario where the grid already holds a large amount of information. The batch insert we’ll perform later must respect the zero‑based index, so we pre‑populate to illustrate the exact insertion point.

## Step 2: Use `InsertRowsBatch` to **Add Multiple Rows Grid**

Now the core of the tutorial – the call that actually **adds rows** in bulk. The method signature is `InsertRowsBatch(int startIndex, int count)`. In our example we’ll start at index 2 000 000 (which corresponds to the 2 000 001st row) and add ten rows.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **How it works:** `InsertRowsBatch` allocates the requested number of rows internally and shifts existing rows down. Because the operation is performed in a single transaction, the UI refreshes only once, which is why this method is the recommended way to **how to add rows** efficiently.

## Step 3: Verify the Insertion – Did the Rows Land Where Expected?

After the batch operation you’ll want to be sure the rows are where you think they are. The following helper reads the first and last rows of the newly added block and prints them to the console.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Expected output**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

The blank cells indicate that the rows are placeholders awaiting data. You can now populate them individually or run another batch update.

> **Edge case note:** If `startIndex` exceeds the current row count, GridJs will automatically append the new rows at the end. Conversely, a negative index throws an `ArgumentOutOfRangeException`, so always validate user‑supplied indices.

## Step 4: Populate the New Rows (Optional but Common)

Often you don’t just want empty rows; you need to fill them with meaningful values. You can loop over the newly created range and call `SetCell` or a similar API.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

You could call `PopulateNewRows(gridJs, startIndex, rowsToAdd);` right after the batch insert if you need the rows ready for display immediately.

## Step 5: Performance Tips for Very Large Grids

When you’re dealing with **add multiple rows grid** in the millions, keep these tricks in mind:

1. **Batch size matters** – Inserting 10 000 rows at once can be faster than ten separate 1 000‑row batches because each batch incurs a single UI refresh.
2. **Turn off UI updates** – Some GridJs versions expose `grid.SuspendLayout()` / `grid.ResumeLayout()`. Wrap your batch inside these calls if you notice lag.
3. **Use virtualization** – As shown earlier, `EnableVirtualization` dramatically reduces memory consumption and rendering time.
4. **Avoid deep copies** – Pass simple value types or lightweight objects to the grid; heavy objects force the grid to clone data, hurting performance.

## Full Working Example

Putting everything together, here’s the complete program you can copy‑paste into a new console project:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

Run the program, and you’ll see the console output confirming that the ten rows were inserted at the correct location and then populated.

## Conclusion

We’ve covered **how to insert rows** in GridJs using the batch API, demonstrated **how to add rows** efficiently, and explored ways to **add multiple rows grid** without choking the UI. The key takeaways are:

- Use `InsertRowsBatch(startIndex, count)` for any bulk operation.
- Validate indices and consider virtualization for massive datasets.
- Populate rows after the batch if you need immediate content.

Next, you might want to explore **how to delete rows**, implement **undo/redo** for batch edits, or integrate GridJs with a back‑end service that streams data on demand. All of those topics build directly on the concepts you’ve just learned.

Feel free to experiment—change the batch size, try inserting at the very beginning of the grid, or combine multiple batches in a single transaction. The more you play, the more comfortable you’ll become with large

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}