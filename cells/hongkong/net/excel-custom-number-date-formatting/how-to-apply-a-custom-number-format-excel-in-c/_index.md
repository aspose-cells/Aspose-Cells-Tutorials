---
category: general
date: 2026-10-26
description: 學習如何在 C# 中設定自訂數字格式的 Excel 檔案，透過設定有效位數、建立 Excel 活頁簿，並將其儲存為 XLSX 檔案。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format excel
- set significant digits
- how to set number format
- create excel workbook c#
- save workbook xlsx
language: zh-hant
lastmod: 2026-10-26
og_description: 在 C# 中使用 Excel 的自訂數字格式，可讓您控制有效位數、建立 Excel 活頁簿，並將其儲存為 XLSX。請跟隨本完整教學。
og_image_alt: Excel cell A1 displaying a number formatted with 4 significant digits
  using C#
og_title: C# 中的 Excel 自訂數字格式 – 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  headline: How to apply a custom number format excel in C#
  type: TechArticle
- description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  name: How to apply a custom number format excel in C#
  steps:
  - name: Using a custom format string instead of global options
    text: 'If you need a format that applies only to a single range, you can assign
      a format string directly:'
  - name: Applying the setting to an entire column
    text: '```csharp // Apply the same significant‑digit rule to column B ws.Cells.Columns[1].ApplyNumberFormatOptions(
      new NumberFormatOptions { SignificantDigits = 4 }); ```'
  - name: Dealing with negative numbers
    text: 'The global `SignificantDigits` option works uniformly for positive and
      negative numbers. If you want a different display for negatives, combine it
      with a custom format:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: 如何在 C# 中套用 Excel 的自訂數字格式
url: /zh-hant/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中套用自訂數字格式 Excel

如果您需要一個 **custom number format excel** 以顯示特定的有效位數，本指南將會完整說明如何在 C# 中實作。您將會看到如何設定有效位數、建立 Excel 工作簿，並將工作簿儲存為 XLSX 檔案──只需幾行程式碼。

以程式方式操作 Excel 檔案時，通常必須控制數字的顯示方式。使用 Aspose.Cells for .NET，您可以定義全域的 number‑format 選項，強制每個數值儲存格遵守指定的有效位數。本教學涵蓋完整工作流程，從專案設定到在 Excel 中驗證輸出結果。

## 前置條件

在開始之前，請確保您已具備：

* .NET 6.0 或更新版本（程式碼亦相容於 .NET Framework 4.7.2+）
* Visual Studio 2022 或您偏好的任何 C# IDE
* **Aspose.Cells** NuGet 套件 (`Install-Package Aspose.Cells`) —— 完全受管理的 Excel 操作函式庫
* 基本的 C# 語法熟悉度

## 步驟 1：在 C# 中建立 Excel 工作簿

第一步是實例化一個新的 `Workbook` 物件。此物件在記憶體中代表整個 Excel 檔案。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook wb = new Workbook();

        // The workbook now contains a default worksheet named "Sheet1"
        // You can access it via the Worksheets collection.
        Worksheet ws = wb.Worksheets[0];
```

**為什麼重要**：`Workbook` 是所有 Excel 操作的入口點。先建立它即可確保產生一個乾淨的檔案，之後再儲存為 XLSX。

## 步驟 2：設定數字格式以指定有效位數

Aspose.Cells 提供一個全域設定 `NumberFormatOptions`。將 `SignificantDigits = 4` 後，除非有更具體的格式覆寫，否則每個數值儲存格都會顯示最多四個有效位數。

```csharp
        // Step 2: Set the global number‑format option to 4 significant digits
        WorkbookSettings.SetNumberFormatOptions(
            new NumberFormatOptions { SignificantDigits = 4 });
```

**為什麼重要**：使用 `SetNumberFormatOptions` 可在不必為每個儲存格撰寫格式字串的情況下定義 **custom number format excel**。它相當於 Excel 中 *格式儲存格 → 數值 → 自訂* 對話框的「有效位數」選項。

## 步驟 3：寫入數值並驗證 custom number format excel

現在將數值寫入儲存格。全域設定會自動套用四位規則。

```csharp
        // Step 3: Write a numeric value into cell A1 (row 0, column 0)
        ws.Cells[0, 0].PutValue(123.456789);

        // Optional: Add a label so you can see the effect in Excel
        ws.Cells[0, 1].PutValue("Original value:");
        ws.Cells[0, 2].PutValue(123.456789);
```

開啟已儲存的檔案時，儲存格 **A1** 會顯示 `123.5`（四捨五入至四個有效位數）。原始值在底層資料中保持不變，您可在公式列中確認。

**邊緣案例提示**：若儲存極大數值如 `12345678.9`，相同設定會顯示 `1.235E+07`（科學記號），因為 Excel 會選擇最緊湊的表示方式，同時保留四個有效位數。

## 步驟 4：將工作簿儲存為 XLSX

最後，將工作簿寫入磁碟。`Save` 方法會根據副檔名自動選擇檔案格式。

```csharp
        // Step 4: Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\SigDigits.xlsx";
        wb.Save(outputPath);

        // Inform the user
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**為什麼重要**：儲存為 **XLSX** (`save workbook xlsx`) 可確保與現代 Excel、Office 365 以及其他試算表工具的最高相容性。

## 預期結果

在 Microsoft Excel 中開啟 *C:\Temp\SigDigits.xlsx*，您應該會看到：

| A          | B               | C               |
|------------|-----------------|-----------------|
| **123.5**  | 原始值：        | **123.456789**  |

*儲存格 A1* 顯示四位有效數字的四捨五入結果，而 *C1* 保留完整精度以供比較。

## 常見變化與如何為特定儲存格設定數字格式

### 使用自訂格式字串取代全域選項

如果您只想讓單一範圍套用格式，可直接指定格式字串：

```csharp
ws.Cells["D1"].PutValue(0.0012345);
Style style = wb.CreateStyle();
style.Custom = "0.####"; // shows up to 4 decimal places, not significant digits
ws.Cells["D1"].SetStyle(style);
```

### 將設定套用至整欄

```csharp
// Apply the same significant‑digit rule to column B
ws.Cells.Columns[1].ApplyNumberFormatOptions(
    new NumberFormatOptions { SignificantDigits = 4 });
```

### 處理負數

全域 `SignificantDigits` 選項對正負數皆一致。如果想要負數有不同顯示方式，可結合自訂格式：

```csharp
Style negStyle = wb.CreateStyle();
negStyle.Custom = "#,##0.###;[Red]-#,##0.###";
ws.Cells["E1"].PutValue(-9876.54321);
ws.Cells["E1"].SetStyle(negStyle);
```

## 專業提示與常見陷阱

* **專業提示**：在寫入任何資料之前先設定 number‑format 選項。於填入儲存格後再變更設定，不會自動重新格式化已存在的值。
* **注意**：使用 `PutValue` 並傳入看似數字的 **字串**（例如 `"123.45"`）。Excel 會將其視為文字，custom number format excel 不會套用。
* **效能說明**：全域設定成本低，但若對數百萬儲存格套用樣式會增加記憶體使用。盡可能使用欄位層級的格式設定。

## 後續步驟

既然您已能透過設定 `NumberFormatOptions` 來 **custom number format excel** 並限制有效位數，接下來可以探索：

* **如何使用 `Style.Custom` 設定日期與貨幣的數字格式**。
* **建立圖表**，使其遵循您的 custom number format excel。
* **匯出為 CSV** 同時保留數值精度（`save workbook xlsx` → `wb.Save("file.csv", SaveFormat.Csv)`）。

上述主題皆基於此處示範的 `Workbook` 與 `Worksheet` 概念。

---

**摘要**

您已學會透過配置 `NumberFormatOptions` 以 **set significant digits**，在 C# 中建立 Excel 工作簿、寫入數值，並 **saving the workbook as an XLSX** 檔案，從而實作 **custom number format excel**。上方完整可執行的程式碼示範每一步驟、說明其必要性，並提供常見變化的技巧。歡迎將這些片段套用至自己的專案，並嘗試其他格式化情境。

## 接下來該學什麼？

以下教學與本指南所示技術緊密相關，並以步驟說明與完整範例協助您掌握更多 API 功能或探索替代實作方式：

- [C# 中的自訂數字格式 Excel – 完整指南](/cells/english/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/)
- [在 C# 中建立 Excel 工作簿 – 限制有效位數 Excel](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-c-limit-significant-digits-excel/)
- [如何使用 Aspose.Cells 套用 number format excel](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}