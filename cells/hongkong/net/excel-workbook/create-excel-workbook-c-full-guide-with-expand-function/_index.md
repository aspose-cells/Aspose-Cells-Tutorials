---
category: general
date: 2026-06-08
description: 一步一步使用 C# 建立 Excel 活頁簿，並學習在 Excel 中使用 EXPAND 函數處理動態範圍。非常適合 .NET 開發者。
draft: false
keywords:
- create excel workbook c#
- use expand function in excel
language: zh-hant
og_description: 使用 C# 建立 Excel 活頁簿，提供清晰範例，並探索如何在 Excel 中使用 EXPAND 函數產生動態陣列。
og_title: 使用 C# 建立 Excel 工作簿 – 完整程式設計指南
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  headline: Create Excel Workbook C# – Full Guide with Expand Function
  type: TechArticle
- description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  name: Create Excel Workbook C# – Full Guide with Expand Function
  steps:
  - name: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
    text: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
  - name: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
    text: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
  - name: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
    text: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
  - name: '**Creates an Excel workbook C#** using Aspose.Cells.'
    text: '**Creates an Excel workbook C#** using Aspose.Cells.'
  - name: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
    text: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
  - name: Adds a cotangent formula (`COT(PI()/4)`).
    text: Adds a cotangent formula (`COT(PI()/4)`).
  - name: Saves the file and optionally auto‑fits columns.
    text: Saves the file and optionally auto‑fits columns.
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells targets .NET Standard 2.0, which is compatible
      with both .NET Core and the classic Framework.
    question: Does this work with .NET Framework 4.8?
  - answer: Use `ws.Protect(ProtectionType.All, "yourPassword");` before saving.
    question: What if I need to protect the sheet?
  - answer: 'Yes—`workbook.Save(stream, SaveFormat.Xlsx);` is handy for web APIs that
      return the file as a download. --- ## TL;DR We built a **complete C# console
      app** that: 1. **Creates an Excel workbook C#** using Aspose.Cells. 2. **Uses
      the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5 block.'
    question: Can I write the workbook directly to a `MemoryStream`?
  type: FAQPage
tags:
- csharp
- excel
- aspose-cells
- .net
title: 使用 C# 建立 Excel 活頁簿 – 完整指南與展開功能
url: /zh-hant/net/excel-workbook/create-excel-workbook-c-full-guide-with-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 Excel 工作簿 C# – 完整指南與 EXPAND 函數

Ever wondered how to **create Excel workbook C#** without wrestling with COM interop or fiddling with XML? You're not the only one. In many .NET projects we need to spit out a spreadsheet, fill it with formulas, and hand it off to non‑technical users. The good news? With a modern library like **Aspose.Cells** the whole process is a piece of cake.

在本教學中，我們將逐步示範一個完整且可執行的範例，**creates an Excel workbook C#**、加入幾個公式——包括如何 **use expand function in Excel**——並將檔案儲存，讓你能立即在 Excel 中開啟。完成後，你不只會知道 *要輸入什麼*，更會了解 *為什麼每一行程式碼很重要*，並且得到一個可以直接複製到任何專案的範本。

## Prerequisites

Before we dive in, make sure you have:

- .NET 6 SDK (or any recent .NET version) installed.
- A NuGet‑compatible IDE (Visual Studio, VS Code, Rider, etc.).
- The **Aspose.Cells** NuGet package – it provides the `Workbook` and `Worksheet` classes used in the code.
- Basic C# familiarity; no Excel‑specific experience required.

Got all that? Great—let’s get started.

## Step 1: Set Up the Project and Add Aspose.Cells

First, spin up a console app and pull in the library.

```bash
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** If you’re on a corporate network, you might need to configure a NuGet proxy. The Aspose.Cells package is lightweight, so the install finishes in seconds.

Now open `Program.cs`. You’ll see the default `Main` method—replace it with the skeleton below.

```csharp
using System;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // All of our Excel logic will go here.
        }
    }
}
```

The `using Aspose.Cells;` line brings the spreadsheet classes into scope. If you forget it, the compiler will complain that `Workbook` is undefined—something we’ll avoid later.

## Step 2: Create Excel Workbook C# and Access the First Worksheet

With the project ready, we can finally **create Excel workbook C#**. The `Workbook` constructor gives us a fresh, empty workbook, and the `Worksheets[0]` index returns the default sheet (named “Sheet1”).

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx file in memory
Worksheet ws = workbook.Worksheets[0];            // reference to the first (default) sheet
```

Why do we grab the first worksheet explicitly? Because many downstream APIs (like setting formulas) require a `Worksheet` object, not just the `Workbook`. This also makes the code clearer for anyone reading it later.

## Step 3: Use Expand Function in Excel to Fill a Dynamic Range

Now comes the star of the show: **use expand function in Excel**. The `EXPAND` function (available from Excel 365 onward) takes a source array and pads it to a desired size. In our example we’ll start with a 3‑row vertical array generated by `SEQUENCE(3)` and expand it into a 5 × 5 block.

```csharp
// Step 3: Insert the EXPAND formula into cell A1
ws.Cells["A1"].Formula = "EXPAND(SEQUENCE(3),5,5)";
```

What actually happens?

1. `SEQUENCE(3)` produces a vertical array `{1;2;3}`.
2. `EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.
3. The result is a 5 × 5 grid where the first three rows contain the numbers 1‑3 repeated across columns, and the remaining two rows are blank.

Because we’re writing the formula as a string, Excel evaluates it *when the file is opened*, not at runtime. That means the workbook stays lightweight, and any changes to the source array will automatically ripple through.

> **Edge case:** If a user opens the workbook in an older version of Excel that doesn’t support `EXPAND`, the cell will display `#NAME?`. To guard against that you could wrap the formula in `IFERROR`, but for modern environments it’s safe to rely on the function.

## Step 4: Add a Cotangent Formula for Good Measure

Let’s sprinkle in another formula to showcase how simple it is to add mathematical expressions. We’ll calculate the cotangent of π/4, which is exactly `1`.

```csharp
// Step 4: Insert a cotangent calculation in cell B1
ws.Cells["B1"].Formula = "COT(PI()/4)";
```

Excel’s `COT` function isn’t as commonly used as `SIN` or `COS`, yet it’s perfect for trigonometric workflows. When you open the workbook, cell **B1** will display `1`.

## Step 5: Save the Workbook and Verify the Result

All that work would be pointless if we didn’t persist the file. The `Save` method writes the in‑memory workbook to disk. Choose a folder you have write access to, and give the file a friendly name.

```csharp
// Step 5: Save the workbook to the output folder
string outputPath = @"./output.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Run the program:

```bash
dotnet run
```

You should see the console message confirming the save. Open `output.xlsx` in Excel, and you’ll notice:

- Cells **A1:E5** filled with the expanded sequence (1,2,3 on the first three rows, blanks on rows 4‑5).
- Cell **B1** showing the value `1` from the cotangent formula.

That’s the full cycle: **create excel workbook c#**, embed formulas, and produce a usable spreadsheet.

![產生的 Excel 工作簿螢幕截圖，顯示展開的陣列與餘切結果](/images/create-excel-workbook-csharp.png "create excel workbook c# 範例")

*Image alt text: create excel workbook c# – view of the populated spreadsheet.*

## Step 6: Optional – Auto‑Fit Columns for a Polished Look

If you plan to distribute the file to end‑users, a quick auto‑fit makes it look professional.

```csharp
// Optional: Auto‑fit all columns in the used range
ws.AutoFitColumns(0, ws.Cells.MaxColumn);
```

This line loops through every column that contains data and adjusts its width to the longest entry. It’s a tiny touch, but it prevents the dreaded “…###” overflow when numbers are wider than the default column width.

## Step 7: Wrap‑Up and Next Steps

Congratulations—you’ve just mastered how to **create excel workbook c#** from scratch and learned how to **use expand function in excel** to generate dynamic arrays. The code is deliberately minimal so you can copy‑paste it into any project, but the concepts scale:

- **Dynamic data sources:** Replace `SEQUENCE(3)` with a reference to another range or a named table.
- **Conditional formatting:** Use `ws.Cells["A1:E5"].Style` to add colors based on values.
- **Charts and graphics:** Aspose.Cells can embed charts, pictures, and even pivot tables.

Feel free to experiment—swap the `EXPAND` dimensions, try `FILTER` or `SORT`, or chain multiple formulas together. The library handles all of it without you ever touching the low‑level OpenXML format.

---

### Frequently Asked Questions

**Q: Does this work with .NET Framework 4.8?**  
A: Absolutely. Aspose.Cells targets .NET Standard 2.0, which is compatible with both .NET Core and the classic Framework.

**Q: What if I need to protect the sheet?**  
A: Use `ws.Protect(ProtectionType.All, "yourPassword");` before saving.

**Q: Can I write the workbook directly to a `MemoryStream`?**  
A: Yes—`workbook.Save(stream, SaveFormat.Xlsx);` is handy for web APIs that return the file as a download.

---

## TL;DR

We built a **complete C# console app** that:

1. **Creates an Excel workbook C#** using Aspose.Cells.  
2. **Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5 block.  
3. Adds a cotangent formula (`COT(PI()/4)`).  
4. Saves the file and optionally auto‑fits columns.

You now have a solid foundation for any automation task that involves generating Excel files from .NET. Happy coding, and may your spreadsheets always stay error‑free!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [How to Create and Use Union Ranges in Excel with Aspose.Cells .NET (C# Guide)](/cells/english/net/range-management/excel-union-range-aspose-cells-net/)
- [Create Excel Workbook with Charts Using Aspose.Cells .NET | Step-by-Step Guide](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}