---
category: general
date: 2026-05-23
description: 在 C# 中建立 Excel 活頁簿，學習如何套用自訂數字格式、以程式方式設定儲存格樣式、將儲存格格式化為科學記號，最後將活頁簿儲存為 xlsx。
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: zh-hant
og_description: 快速使用 C# 建立 Excel 活頁簿。學習如何以程式方式套用自訂數字格式、設定儲存格樣式、格式化科學記號，並儲存為 xlsx。
og_title: 在 C# 中建立 Excel 工作簿 – 套用自訂數字格式
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: 在 C# 中建立 Excel 工作簿 – 套用自訂數字格式
url: /zh-hant/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中建立 Excel 工作簿 – 套用自訂數字格式

在 C# 中建立 Excel 工作簿比你想像的更簡單。在本指南中，我們將逐步說明如何套用自訂數字格式、將儲存格以科學記號格式化、以程式方式設定儲存格樣式，最後將工作簿儲存為 xlsx 檔案。

如果你曾經盯著空白的試算表，想知道如何自動化整個流程——從填入資料到讓數字呈現出你需要的樣子——本教學正適合你。完成後，你將擁有一個功能完整的 Excel 檔案，能在任何試算表程式中開啟，且你會了解 **為何** 每一步重要，而不僅是 **如何** 輸入程式碼。

## 需要的條件

- **.NET 6+**（或任何支援此函式庫的較新 .NET Framework）  
- **Aspose.Cells for .NET**（或其他提供 `Workbook`、`Cell`、`CellFormat` 類別的 API）  
- 具備基本的 C# 經驗——只要會寫 `Console.WriteLine`，就能上手。  

不需要額外的設定檔、COM 互操作，也絕不需要手動安裝 Excel。

---

## 建立 Excel 工作簿 – 初始化 Workbook 物件

我們首先要做的事是建立一個空的工作簿。把 `Workbook` 類別想像成一張空白畫布，你可以在上面繪製列、欄與樣式。

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

就是這樣——只需一行程式碼，你就擁有一個全新的 Excel 檔案於記憶體中。`Workbook` 建構函式會建立預設的工作表集合，讓你可以立即開始加入資料。

> **小技巧：** 若需要多個工作表，可在填寫儲存格之前呼叫 `workbook.Worksheets.Add()`。

![建立 Excel 工作簿範例](image-placeholder.png "建立 Excel 工作簿螢幕截圖")

*圖片說明：顯示在 IDE 中的空白 Excel 工作表範例*

## 為儲存格套用自訂數字格式

既然工作簿已建立，讓我們在 **A1** 儲存格輸入一個數字並套用自訂格式。自訂數字格式讓你能控制數字的顯示方式——貨幣、百分比、日期，或在本例中的科學記號。

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

為什麼要先取得樣式？因為 `Cell` 物件會儲存一個 **Style** 物件，裡面包含字型、邊框、對齊與數字格式等設定。編輯 `Custom` 屬性即可告訴 Excel「以科學記號且保留兩位小數的方式顯示此值」。

> **常見問題：** *我可以使用內建格式而非自訂格式嗎？*  
> 可以——將 `style.Number = 10` 設為內建的科學記號格式，但自訂字串能讓你精確控制小數位數。

## 以程式方式設定儲存格樣式（超越數字格式）

通常你會需要的不只是數字格式。讓我們加入粗體字與淡灰色背景，使儲存格更突出。

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

請注意，我們再次使用先前調整過的 `style` 物件。這就是 **以程式方式設定儲存格樣式** 的好處——只需一次取得樣式，修改所需屬性後寫回。無需重新建立物件或失去已設定的數字格式。

## 以科學記號格式化儲存格（特殊情況處理）

當處理極大或極小的數字時，科學記號是救星。我們使用的自訂格式 (`0.00E+00`) 保證小數點後兩位，且指數前強制加號。以下是一個快速驗證：

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

開啟產生的檔案時，B2 會顯示為 `1.23E-05`，證實 **以科學記號格式化儲存格** 的指示對大數與小數皆有效。

## 儲存工作簿為 XLSX

所有操作的最後一步是將檔案寫入磁碟。`Save` 方法負責繁重的工作，將記憶體中的表示轉換為正式的 `.xlsx` 套件。

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

這行程式碼完成了 **儲存工作簿為 xlsx** 的目標。若目錄不存在，`Save` 會拋出例外——因此請先建立資料夾，或將呼叫包在 try/catch 區塊中。

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

現在你已擁有一個可直接分享的 Excel 檔案，內含格式良好的科學記號數字、粗體樣式與淡灰色背景。

## 完整範例程式

以下是完整、可直接複製貼上的程式，將所有步驟串接起來。它可編譯為主控台應用程式，但你也可以將程式碼放入任何 C# 專案中。

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**預期結果：** 開啟 `CustomFormatted.xlsx` 後，你會看到：

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

兩個儲存格皆為粗體、淡灰色填滿，且以兩位小數的科學記號顯示數字。

---

## 小結

我們剛剛從頭 **建立 Excel 工作簿**、**套用自訂數字格式**、**以科學記號格式化儲存格**、**以程式方式設定儲存格樣式**，以及 **儲存工作簿為 xlsx**——全部只需幾行 C# 程式碼。此方法具可擴充性：只要迴圈處理列、複製 `style` 物件，即可在數秒內產生完整樣式的報表。

### 接下來？

- **動態格式化：** 根據數值大小切換格式（例如貨幣或百分比）。  
- **多工作表：** 使用 `workbook.Worksheets.Add("Summary")` 建立儀表板。  
- **進階樣式：** 邊框、條件格式與資料驗證

## 相關教學

- [如何使用 Aspose.Cells for .NET 建立並儲存 Excel 工作簿為 ODS](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [建立與儲存 Excel 工作簿（Aspose Cells .NET）](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [建立與儲存 Excel 工作簿為 PDF（Aspnet Aspose Cells）](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}