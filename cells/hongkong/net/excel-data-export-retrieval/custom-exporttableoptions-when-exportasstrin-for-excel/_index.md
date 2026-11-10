---
category: general
date: 2026-10-26
description: 自訂 ExportTableOptions（當 ExportAsString 時）讓您在 C# 中將 Excel 資料匯出為字串。請跟隨逐步指南設定及執行匯出。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: zh-hant
lastmod: 2026-10-26
og_description: 當 ExportAsStrin 啟用僅字串 Excel 匯出時，自訂 ExportTableOptions。了解在 C# 中設定與執行匯出的完整步驟。
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: 自訂 ExportTableOptions 時 ExportAsString – 在 C# 中將 Excel 匯出為字串
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: 在 Excel 中使用 ExportAsStrin 時自訂 ExportTableOptions
url: /zh-hant/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Custom ExportTableOptions when ExportAsStrin – 在 C# 中將 Excel 匯出為字串

如果你需要 **Custom ExportTableOptions when ExportAsStrin** 以取得每個儲存格的純文字字串，本指南將一步步說明如何完成。無論你是在建構資料匯入管線，或是需要乾淨的 CSV 準備檔，都會了解為何以此方式設定選項可以避免型別轉換的意外。

在本教學中，你將學會 **如何使用 Aspose.Cells 套件將 excel 匯出為字串**，看到完整可執行的程式碼，並了解每個設定背後的原因。無需參考外部文件——所有資訊都在此處。

## 前置條件

在開始之前，請確保你已具備：

* .NET 6.0 SDK 或更新版本  
* Visual Studio 2022（或任何支援 .NET 的 IDE）  
* Aspose.Cells for .NET 套件（透過 NuGet 安裝：`Install-Package Aspose.Cells`）  
* 一個放在專案根目錄的 Excel 活頁簿（`sample.xlsx`）  

以上即為唯一的相依項目；程式碼可在 Windows、Linux 或 macOS 上執行，無需額外函式庫。

## 步驟 1：載入要匯出的活頁簿

使用 **Custom ExportTableOptions when ExportAsStrin** 時，第一件事就是從已載入的活頁簿取得 `Worksheet` 物件。此物件讓你可以存取列、欄以及匯出 API。

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*為什麼這很重要：*  
`Workbook` 只會讀取檔案一次，並將所有格式資訊保留在記憶體中。透過選取特定的 `Worksheet`，即可限制匯出範圍，避免不必要的隱藏工作表處理。

## 步驟 2：以 ExportAsString = true 設定 ExportTableOptions

**Custom ExportTableOptions when ExportAsStrin** 的核心是 `ExportTableOptions` 物件。將 `ExportAsString` 設為 `true` 會強制匯出器將每個儲存格視為字串，無論其原始資料型別（日期、數字、布林等）為何。啟用 `PreserveFormatting` 則會保留視覺樣式（例如貨幣符號）於最終字串中。

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*為什麼這很重要：*  
稍後呼叫 `ExportDataTable` 時，函式庫預設會嘗試推斷每個欄位的 .NET 型別。設定 `ExportAsString = true` 後，這一步會被略過，避免產生意外的 `DateTime` 或 `double` 轉換，從而破壞下游的 CSV 解析器。

## 步驟 3：使用自訂選項將範圍匯出為 DataTable

現在可以從工作表中匯出矩形範圍（第 0‑9 列，第 0‑4 欄）。此方法會回傳一個 `DataTable`，其中每個欄位皆為 `string`。

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*為什麼這很重要：*  
`ExportDataTable` 是將 Excel 資料搬移至多數 .NET API 已熟悉的關聯結構（例如 Entity Framework、Dapper）的最便利方式。透過傳入 **Custom ExportTableOptions when ExportAsStrin**，即可保證每個 `DataColumn.DataType` 為 `typeof(string)`。

## 步驟 4：驗證結果 – 所有值皆為字串

驗證匯出是否如預期是一個好習慣。以下迴圈會印出每個儲存格及其執行時型別。

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**預期輸出**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

每個儲存格皆顯示 `String` 為型別，證明 **Custom ExportTableOptions when ExportAsStrin** 已正確運作。

## 步驟 5：可選 – 將 DataTable 寫入 CSV

如果最終目標是純文字檔，你可以輕鬆將 `DataTable` 序列化為 CSV：



## 接下來該學什麼？

以下教學與本指南所示技術緊密相關，能幫助你進一步掌握 API 功能，並在自己的專案中探索其他實作方式。

- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Export Custom Properties Excel Pdf Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}