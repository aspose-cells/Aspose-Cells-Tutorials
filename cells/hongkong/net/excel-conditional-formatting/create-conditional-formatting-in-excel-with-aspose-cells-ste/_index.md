---
category: general
date: 2026-06-30
description: 使用 Aspose.Cells 在 Excel 工作簿中建立條件格式。了解如何設定儲存格背景、對儲存格進行排名，以及以程式方式建立檔案。
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: zh-hant
og_description: 使用 Aspose.Cells 在 Excel 工作簿中建立條件格式設定。跟隨本完整教學設定儲存格背景、對儲存格進行排名，並自動化
  Excel。
og_title: 使用 Aspose.Cells 在 Excel 中建立條件格式
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: 使用 Aspose.Cells 在 Excel 中建立條件格式化 – 步驟指南
url: /zh-hant/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中使用 Aspose.Cells 建立條件格式 – 步驟指南

有沒有想過如何在不開啟使用者介面的情況下**create conditional formatting**於 Excel 檔案中？你並不孤單。許多開發人員需要即時**create excel workbook**，而以程式方式完成則能省下大量手動操作的時間。在本教學中，我們將示範如何**create conditional formatting**、設定儲存格樣式，甚至為最高分排名——全部使用功能強大的 Aspose.Cells .NET 函式庫。

我們會以真實案例說明：產生成績表、以淡綠色標示高分、並為前 3 名的表現者加上金色背景。完成後，你將了解**how to set cell background**、**how to rank cells**，以及**how to use Aspose** 進行進階的 Excel 自動化。內容精簡、可直接在任何 C# 專案中執行。

## What You’ll Learn

- 如何使用 Aspose.Cells **create excel workbook**  
- 如何以隨機資料（成績）填滿範圍  
- 如何 **set cell background** 為純色  
- 如何套用公式規則以 **rank cells** 並標示前三名  
- 如何將結果儲存為 .xlsx 檔案  

前置條件：.NET 6+（或 .NET Framework 4.6+）、Visual Studio（或任何 C# IDE），以及已參考 Aspose.Cells NuGet 套件。若你從未使用過 Aspose，也不必擔心，我們會從頭說明**how to use Aspose**。

---

![Create conditional formatting example](https://example.com/images/create-conditional-formatting.png "Screenshot showing conditional formatting in the generated Excel file")

*圖片說明：使用 Aspose.Cells 產生的 Excel 活頁簿中 **create conditional formatting** 範例。*

## How to Create Excel Workbook with Aspose.Cells

First things first: you need a workbook object to work with. Aspose.Cells makes this a one‑liner.

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

Why do we rename the sheet? A clear name (like **Scores**) makes it easier to reference later, especially when you share the file with non‑technical users.  

Now that the workbook exists, let’s fill column A with random scores.

## How to Fill Data – Creating Random Scores

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

A quick note: `PutValue` automatically detects the data type, so you don’t have to cast to `int`. The loop starts at `i = 0` but writes to row `i + 1` because Excel rows are 1‑based while the `Cells` collection is 0‑based.

## How to Set Cell Background for High Scores

Now we’ll **create conditional formatting** that paints any score ≥ 80 in a light‑green shade.

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

The `ForegroundColor` property controls the fill color, while `Pattern = BackgroundType.Solid` tells Excel to use a solid fill rather than a gradient or pattern. This is the core of **how to set cell background** based on a numeric threshold.

## How to Rank Cells and Highlight the Top‑3

Ranking is a bit trickier because we need a formula that evaluates each cell against the whole range. Aspose.Cells lets you use the same Excel formula syntax you’d type into the UI.

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

Why `A2` in the formula? Aspose evaluates the formula relative to each cell in the range, so `A2` automatically shifts to `A3`, `A4`, etc., as the rule is applied row‑by‑row. The `RANK` function returns the position of a value within the specified range, and the `<=3` part ensures only the three highest scores get the gold fill.

## How to Save the Workbook

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

Replace `YOUR_DIRECTORY` with an absolute or relative path that your application can write to. After running the method, open the file in Excel and you’ll see:

- Light‑green cells for any score ≥ 80  
- Gold cells for the three highest scores, regardless of whether they’re also ≥ 80  

That’s the complete **create conditional formatting** pipeline.

---

## Full, Runnable Example

Here’s the entire method again, ready to copy‑paste into a console app or any C# class:

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### Expected Result

When you open `Scores_ConditionalFormatting.xlsx`:

- Cells with values **80** or higher glow light‑green.  
- The three highest numbers (even if they’re below 80) appear with a **gold** background.  
- All other cells retain the default white background.

That visual cue instantly tells a manager who the top performers are, without any manual sorting.

---

## Common Questions & Edge Cases

**What if I need more than three top scores?**  
Just change the `<=3` part of the formula to `<=5` (or any number you like). The rule will automatically adapt.

**Can I apply multiple formatting ranges?**  
Absolutely. Call `sheet.ConditionalFormattings.Add` again with a different range, then add conditions to that new `ConditionalFormatting` object.

**What about older Excel versions?**  
Aspose.Cells saves in the modern `.xlsx` format by default, which is compatible with Excel 2007 and later. If you need `.xls`, pass `SaveFormat.Excel97To2003` to the `Save` method.

**Is there a performance impact for large sheets?**  
Conditional formatting is stored as metadata, so it doesn’t significantly affect file size. However, generating hundreds of thousands of rows may increase memory usage—consider processing in batches.

---

## Next Steps

Now that you’ve mastered **how to create conditional formatting**, you might want to explore:

- **How to create Excel charts** programmatically (another Aspose.Cells gem)  
- **How to set cell background** based on text values (e.g., “Pass/Fail”)  
- **How to use Aspose.Cells for data validation** and drop‑down lists  

Each of these topics builds on the same fundamentals you just learned, so you’ll feel right at home.

---

## Wrap‑Up

We’ve just walked through a complete, end‑to‑end example of how to **create conditional formatting** in an Excel workbook using Aspose.Cells. From initializing the workbook, filling data, **setting cell background**, ranking the top performers, to finally saving the file, every step was covered with both **how to rank cells** and **how to use Aspose** in mind.  

Give the code a spin, tweak the thresholds, and watch how quickly you can generate polished reports for any business scenario. Got a twist you’d like to share? Drop a comment below—happy coding!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Automate Excel Conditional Formatting Using Aspose.Cells for Java&#58; A Complete Guide](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java&#58; A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}