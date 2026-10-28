---
category: general
date: 2026-02-23
description: 如何使用 Aspose.Cells 建立工作簿並以 JSON 陣列加入標記。學習如何加入標記、使用 JSON 陣列，以及在幾分鐘內使用 Aspose.Cells
  的智慧標記。
draft: false
keywords:
- how to create workbook
- how to add markers
- use json array
- smart markers aspose.cells
language: zh-hant
og_description: 如何使用 Aspose.Cells 建立工作簿、加入標記並使用 JSON 陣列。本一步一步的指南會向你展示所有所需內容。
og_title: 如何使用智慧標記建立工作簿 – Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: 如何使用智慧標記建立工作簿 – Aspose.Cells 指南
url: /zh-hant/net/smart-markers-dynamic-data/how-to-create-workbook-with-smart-markers-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用智慧標記建立工作簿 – Aspose.Cells 指南

Ever wondered **如何建立工作簿** that automatically fills data from a JSON source? You’re not the only one—developers constantly ask how to add markers that pull values from arrays, especially when working with Aspose.Cells. The good news? It’s pretty straightforward once you grasp the smart‑marker concept. In this tutorial we’ll walk through creating a workbook, adding markers, using a JSON array, and configuring smart markers in Aspose.Cells so you can generate Excel files on the fly.

We’ll cover everything you need to know: initializing the workbook, building a `MarkerCollection`, feeding a JSON array, toggling the “ArrayAsSingle” flag, and finally applying the markers. By the end you’ll have a fully functional C# program that produces an Excel file with the values **A**, **B**, and **C** populated automatically. No external services, just pure Aspose.Cells magic.

## 前置條件

- .NET 6.0 或更新版本（此程式碼亦可在 .NET Framework 4.6+ 上執行）
- Aspose.Cells for .NET NuGet 套件（`Install-Package Aspose.Cells`）
- 基本的 C# 語法了解（如果您是新手，程式碼片段已加上大量註解）
- Visual Studio 或任何您偏好的 IDE

If you already have these, great—let’s dive in.

## 第一步：如何建立工作簿（初始化 Excel 檔案）

The first thing you need is an empty workbook object. Think of it as a blank canvas that Aspose.Cells will later paint with data.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // reference to the default sheet
```

> **Why this matters:** `Workbook` is the entry point for every Excel operation. Without it you can’t attach smart markers or save the file. Creating the workbook first also ensures you have a clean environment for the subsequent steps.

## 第二步：如何新增標記 – 初始化 Marker Collection

Smart markers live inside a `MarkerCollection`. This collection is where you define placeholders (the markers) and the data that will replace them.

```csharp
        // Step 2: Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();
```

> **Pro tip:** You can reuse the same `MarkerCollection` for multiple worksheets, but keeping one per sheet makes debugging easier.

## 第三步：使用 JSON 陣列 – 新增帶有 JSON 資料的標記

Now we actually add a marker. The placeholder `{SmartMarker}` will be replaced by the JSON array we supply. The JSON must be a stringified array, e.g., `["A","B","C"]`.

```csharp
        // Step 3: Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");
```

> **Explanation:** The `Add` method takes two arguments: the marker text and the data source. Here the data source is a JSON array, which Aspose.Cells can parse automatically. This is the core of **使用 JSON 陣列** with smart markers.

## 第四步：設定標記 – 將陣列視為單一值

By default, Aspose.Cells expands a JSON array into separate rows. If you want the whole array to be treated as a single cell value (useful for dropdown lists or concatenated strings), set the `ArrayAsSingle` flag.

```csharp
        // Step 4: Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;
```

> **When to use it:** If you need the array to appear in one cell (e.g., `"A,B,C"`), enable this flag. Otherwise, Aspose.Cells will write each element into its own row.

## 第五步：將標記附加至工作表並套用

Finally, bind the marker collection to the worksheet and tell Aspose.Cells to replace the placeholders with actual data.

```csharp
        // Step 5: Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Optional: write the placeholder into a cell so you can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook to disk
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

> **Result:** After running the program, `SmartMarkerResult.xlsx` contains the value **A** (or the whole array if `ArrayAsSingle` is true) in cell `A1`. Open the file to verify.

### 預期輸出

| A |
|---|
| A |   *(如果 `ArrayAsSingle` 為 false，第一個元素會填入儲存格)*

If you set `ArrayAsSingle = true`, cell `A1` will contain the string `["A","B","C"]`.

## 第六步：如何新增標記 – 進階情境（可選）

You might wonder, *what if I need more than one marker?* The answer is simple: just call `Add` again.

```csharp
        smartMarkerCollection.Add("{SecondMarker}", "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]");
        // You can also control each marker individually:
        smartMarkerCollection["SecondMarker"] = false; // expand into rows
```

> **Why this works:** Each marker operates independently, so you can mix “array as single” and “expand into rows” within the same worksheet. This flexibility is a hallmark of **smart markers aspose.cells**.

## 常見陷阱與避免方法

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| Marker not replaced | Placeholder text missing or typo | Ensure the cell contains the exact marker string (`{SmartMarker}`) |
| JSON not parsed | Invalid JSON syntax (missing quotes) | Use a JSON validator or double‑escape quotes in C# strings |
| Array expands unexpectedly | `ArrayAsSingle` left at default `false` | Set `["ArrayAsSingle"] = true` for the specific marker |
| Workbook saved empty | `Apply()` not called before `Save()` | Always call `worksheet.SmartMarkers.Apply()` before saving |

## 完整可執行範例（直接複製貼上）

Below is the complete program you can drop into a console app. No additional files are required.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();

        // Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");

        // Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;

        // Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Place the marker in a cell so we can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

Run the program, open `SmartMarkerResult.xlsx`, and you’ll see the JSON array (or its first element) neatly placed in cell **A1**.

## 後續步驟：擴充解決方案

Now that you know **how to create workbook**, **how to add markers**, and **use json array** with Aspose.Cells, consider these follow‑up ideas:

1. **Multiple Worksheets** – Loop through a list of worksheets and attach different marker collections to each.
2. **Dynamic JSON** – Pull JSON from a web API (`HttpClient`) and feed it directly into `smartMarkerCollection.Add`.
3. **Styling Output** – After applying markers, format cells (fonts, colors) to make the report look polished.
4. **Export Formats** – Save the workbook as PDF, CSV, or HTML by changing `workbook.Save("file.pdf")`.

Each of these topics naturally involves **smart markers aspose.cells**, so you’ll be extending the same core concepts you just learned.

## 結論

We’ve walked through **how to create workbook** from scratch, **how to add markers**, and how to **use json array** with Aspose.Cells smart markers. The complete, runnable example demonstrates the entire workflow, from initializing the `Workbook` to saving the final file. By toggling the `ArrayAsSingle` flag you gain fine‑grained control over how JSON data appears in Excel, making the solution adaptable to a wide range of reporting scenarios.

Give the code a spin, tweak the JSON, and experiment with additional markers. When you master these building blocks, generating sophisticated Excel reports becomes a piece of cake. Got questions or want to share a cool use‑case? Drop a comment below—happy coding! 

![顯示如何使用智慧標記在 Aspose.Cells 中建立工作簿的圖示](https://example.com/images/create-workbook-smart-markers.png "如何使用 Aspose.Cells 智慧標記建立工作簿")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}