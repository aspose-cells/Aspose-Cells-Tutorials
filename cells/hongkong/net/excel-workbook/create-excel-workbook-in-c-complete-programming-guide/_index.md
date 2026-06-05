---
category: general
date: 2026-06-05
description: 快速在 C# 中建立 Excel 工作簿，並學習如何設定儲存格的數字格式、匯出 Excel 儲存格，以及將儲存格值轉換為保留兩位小數的字串。
draft: false
keywords:
- create excel workbook
- set cell number format
- format number with two decimals
- how to export excel cell
- convert cell value to string
language: zh-hant
og_description: 在 C# 中建立 Excel 活頁簿，精通設定儲存格數字格式、將 Excel 儲存格匯出為字串，以及將數字格式化為兩位小數。
og_title: 在 C# 中建立 Excel 工作簿 – 完整逐步指南
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  headline: Create Excel Workbook in C# – Complete Programming Guide
  type: TechArticle
- description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  name: Create Excel Workbook in C# – Complete Programming Guide
  steps:
  - name: What if the cell already has a style?
    text: The `GetStyle` method returns a copy of the existing style, so any previous
      formatting (font, color, etc.) is retained. You only overwrite the `Custom`
      property, leaving everything else untouched.
  - name: How does culture affect the decimal separator?
    text: 'Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead
      of a dot, set:'
  - name: Can I export a range of cells at once?
    text: Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range
      address. The `ExportTableOptions` you defined for a single cell can be reused
      for the whole range.
  - name: What if I don’t want the value rounded but truncated?
    text: 'Change the custom format to `"0.00"` with a rounding mode, or manually
      truncate before putting the value:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: 在 C# 中建立 Excel 工作簿 – 完整程式設計指南
url: /zh-hant/net/excel-workbook/create-excel-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中建立 Excel 工作簿 – 完整程式指南

有沒有想過如何在 C# 中 **create Excel workbook** 而不必與 COM interop 或雜亂的 CSV 技巧糾纏？你並不孤單。許多開發者需要一種乾淨、.NET 原生的方式來產生 .xlsx 檔案、在儲存格中填入數字，然後將該值匯出為格式良好的字串。  

在本教學中，我們將一步步示範——從空白工作簿開始，設定儲存格的數字格式、將數字格式化為兩位小數，最後學習 **how to export Excel cell** 資料為字串。最後你也會看到如何 **convert cell value to string** 而不失去精度。

> **Pro tip:** 以下方法使用 **Aspose.Cells for .NET** 函式庫，這是一個經過實戰驗證、商業等級的 API。如果你在尋找免費的替代方案，EPPlus 或 ClosedXML 也有類似功能，但程式碼片段會略有不同。

## 前置條件

- .NET 6.0 SDK（或任何較新的 .NET 版本）已安裝。
- Visual Studio 2022 或 VS Code（搭配 C# 擴充功能）。
- **Aspose.Cells** NuGet 套件 (`Install-Package Aspose.Cells`)。

不需要其他相依性——所有其他功能都內建於函式庫中。

## 步驟 1：安裝 Aspose.Cells 並設定專案

在終端機（或套件管理員主控台）中執行以下指令：

```powershell
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

這會建立一個名為 `ExcelDemo` 的全新主控台應用程式，並取得 `Aspose.Cells` 程式集。  

此步驟重要的原因在於：若沒有此函式庫，你將無法 **create Excel workbook** 物件或以型別安全的方式操作儲存格。

## 步驟 2：建立工作簿並取得第一個工作表

現在開啟 `Program.cs`，將預設程式碼替換為下方片段。它展示了在 **create Excel workbook** 時的第一件事——實例化 `Workbook` 類別，並取得預設工作表的參考。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a new .xlsx in memory
        Worksheet ws = workbook.Worksheets[0];           // first (default) sheet

        // The rest of the steps will follow here...
```

> **Why?** `Workbook` 物件是 Excel 檔案在記憶體中的表示。預設情況下它包含一個工作表，我們透過零基索引來存取它。

## 步驟 3：將數值寫入特定儲存格

我們將目標設定為第 5 列、第 2 欄（零基索引），並插入一個小數。這將在稍後示範 **format number with two decimals**。

```csharp
        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];          // corresponds to cell C6 in Excel UI
        cell.PutValue(12345.6789);          // raw value with many decimal places
```

`PutValue` 方法會儲存原始的 double。此時，Excel 會顯示完整精度，除非我們套用格式。

## 步驟 4：設定儲存格數字格式（兩位小數）

這裡我們會 **set cell number format**。我們將使用 `Style` 物件定義自訂數字格式 `"0.00"`——恰好兩位小數。

```csharp
        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();               // clone existing style
        style.Custom = "0.00";                       // forces two digits after the dot
        cell.SetStyle(style);                        // apply the style back to the cell
```

為什麼使用樣式而不是字串轉換？將儲存格保留為數值型別可保留其可計算的特性（仍可進行加總、平均等），同時顯示正確的格式。

## 步驟 5：將儲存格值匯出為格式化字串

有時你需要將 **how to export excel cell** 的值以純文字形式取得——可能是寫入日誌檔或透過 Web API 傳送。Aspose.Cells 允許你為儲存格附加匯出選項，指示函式庫使用相同的數字格式將值呈現為字串。

```csharp
        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // forces string output
            NumberFormat = "0.00"           // matches the style we set earlier
        };
        cell.ExportOptions = exportOptions; // attach options to the cell
```

## 步驟 6：取得格式化字串（Convert Cell Value to String）

現在實際執行匯出並查看結果。`ExportString` 方法會回傳儲存格內容的字串，並套用我們先前附加的 `ExportTableOptions`。

```csharp
        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");
```

執行程式後，主控台會印出：

```
Formatted cell value: 12345.68
```

請注意 `12345.6789` 被四捨五入為 `12345.68`——這就是 **format number with two decimals** 的效果。

## 步驟 7：（可選）將工作簿儲存至磁碟

如果你也想在實際的 `.xlsx` 檔案中看到結果，只需呼叫 `Save`：

```csharp
        // Optional: write the workbook to a file so you can open it in Excel
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

開啟 `DemoWorkbook.xlsx` 後，可在儲存格 **C6** 看到相同的數字，已以兩位小數格式顯示。

## 邊緣案例與常見問題

### 如果儲存格已經有樣式呢？

`GetStyle` 方法會回傳現有樣式的副本，因此先前的格式設定（字型、顏色等）會被保留。你只會覆寫 `Custom` 屬性，其他設定保持不變。

### 文化設定如何影響小數點分隔符號？

Aspose.Cells 會遵循執行緒的 `CultureInfo`。如果需要使用逗號而非句點，請設定：

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("fr-FR");
```

相同的 `"0.00"` 格式現在會呈現 `12 345,68`。

### 我可以一次匯出一個儲存格範圍嗎？

可以——使用 `Worksheet.ExportDataTable` 或 `Worksheet.ExportString` 並指定範圍位址。你為單一儲存格定義的 `ExportTableOptions` 可重複使用於整個範圍。

### 如果我不想四捨五入而是截斷值呢？

將自訂格式改為帶有截斷模式的 `"0.00"`，或在寫入值之前手動截斷：

```csharp
double raw = Math.Truncate(12345.6789 * 100) / 100; // yields 12345.67
cell.PutValue(raw);
```

## 完整可執行範例（可直接複製貼上）

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];
        cell.PutValue(12345.6789);

        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();
        style.Custom = "0.00";
        cell.SetStyle(style);

        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "0.00"
        };
        cell.ExportOptions = exportOptions;

        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");

        // Optional: save the workbook for visual verification
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

**預期的主控台輸出**

```
Formatted cell value: 12345.68
```

開啟 `DemoWorkbook.xlsx` → 前往儲存格 **C6** → 你會看到相同的數字，且顯示兩位小數。

## 結論

我們已說明了在 C# 中 **create Excel workbook**、**set cell number format**、**format number with two decimals**、了解 **how to export Excel cell** 資料，以及 **convert cell value to string** 用於後續處理所需的全部知識。  

重點如下：

1. 使用 `Workbook` 與 `Worksheet` 在記憶體中建立 Excel 檔案。  
2. 套用自訂樣式 (`"0.00"`) 以強制顯示兩位小數。  
3. 當需要符合相同格式的字串表示時，將 `ExportTableOptions` 附加至儲存格。

從此你可以自行實驗——新增更多儲存格、套用條件格式，甚至產生圖表。如果你對字型樣式或加入公式感興趣，請參閱 Aspose.Cells 文件中的 **cell styling** 與 **formula evaluation**。

對 C# 中的 Excel 自動化還有其他問題嗎？歡迎留言，祝編程愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索替代實作方式。

- [Master Workbook Operations in Aspose.Cells .NET&#58; Load Excel Files and Trace Cell Precedents Effectively](/cells/english/net/workbook-operations/aspose-cells-net-master-workbook-operations/)
- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Master Aspose.Cells for .NET&#58; Advanced Excel Workbook and Cell Management](/cells/english/net/advanced-features/excel-aspose-cells-net-create-manage/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}