---
category: general
date: 2026-08-11
description: 在 C# 中從 DataTable 建立 Excel 工作表，並將 DataTable 匯出至 Excel，支援自動工作表命名。學習如何向
  DataTable 新增列，並將活頁簿儲存為 xlsx 格式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: zh-hant
lastmod: 2026-08-11
og_description: 在 C# 中從 DataTable 建立 Excel 工作表。本教學示範如何將資料表匯出至 Excel、向資料表新增列、產生多個 Excel
  工作表，並將活頁簿儲存為 xlsx。
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: 在 C# 中從 DataTable 建立 Excel 工作表 – 完整程式設計指南
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: 從 DataTable 建立 Excel 工作表（C#）–逐步指南
url: /zh-hant/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 DataTable 建立 Excel 工作表（C#） – 步驟指南

如果您需要 **create excel sheet** 從 `DataTable` 於 C# 中建立，本指南將一步步說明如何操作。您將會看到如何 **export datatable to excel**、新增列、處理重複工作表名稱，最後 **save workbook as xlsx**。

此範例使用 Aspose.Cells，這是一套廣泛使用的 .NET Excel 自動化函式庫。相同概念亦適用於支援 SmartMarker 風格處理的其他函式庫，但以下程式碼在 Aspose.Cells 22.12 或更新版本即可直接執行。

## 前置條件

在開始之前，請確保您已具備：

* .NET 6.0 SDK 或更新版本已安裝  
* 參考 **Aspose.Cells** NuGet 套件 (`Install-Package Aspose.Cells`)  
* 熟悉 `DataTable` 與 C# 主控台應用程式的基本概念  

這些需求確保教學自成一體，且不需額外工具。

## 步驟 1：建立將匯出至 Excel 的 DataTable

第一步是建立一個 `DataTable`，其結構與您想要在工作表中呈現的資料相符。此處我們建立名為 **Sheet1** 的表格，加入 `Id` 欄位，並插入兩筆資料。

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**為什麼這很重要：**  
`DataTable` 是一種方便的記憶體內表格資料表示方式。將表格命名為 `"Sheet1"` 可讓 Aspose.Cells 在處理 SmartMarkers 時知道要對應哪一個工作表。

## 步驟 2：向 DataTable 新增列（可選擇性擴充）

如果來源資料是動態的，您通常需要在迴圈中新增列。以下程式碼示範了一個常見的模式：

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**提示：** 新增大量列時，考慮關閉約束 (`dataTable.Constraints.Clear()`) 以提升效能。

## 步驟 3：設定 SmartMarker 選項以自動建立多個 Excel 工作表

SmartMarker 選項讓您控制重複工作表名稱的處理方式。將 `DetailSheetNewName` 設為 `"Sheet1_{0}"`，即可讓 Aspose.Cells 將後續工作表重新命名為 `Sheet1_1`、`Sheet1_2`，以此類推。

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**為什麼這很重要：**  
當您處理多個名稱相同的 `DataTable` 時，Excel 會因工作表名稱必須唯一而拋出錯誤。`DetailSheetNewName` 的命名模式會自動避免此衝突。

## 步驟 4：處理 SmartMarkers 並將 DataTable 匯出至 Excel

現在我們建立一個全新的 `Workbook`，執行 `ProcessSmartMarkers`，讓 Aspose.Cells 依據 `DataTable` 填充工作表。

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**說明：**  
`ProcessSmartMarkers` 會掃描工作簿中的標記（例如 `&=Sheet1!A1`，此處未示範），並以 `dataTable` 的資料取代它們。因為我們從空白工作簿開始，Aspose.Cells 會依表格名稱建立新工作表，並填入先前新增的列。

## 步驟 5：將工作簿另存為 xlsx

最後，將工作簿以現代的 OpenXML 格式（`.xlsx`）寫入磁碟。您可以自行調整路徑以符合環境需求。

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**結果：**  
執行程式後會產生一個 Excel 檔案，內容如下：

| 工作表名稱 | 列 |
|------------|------|
| Sheet1     | 1, 2, 3, 4, 5 |
| Sheet1_1   | (如果處理另一個同名的 DataTable) |

工作表重新命名的邏輯確保 **create multiple excel sheets** 無需手動管理名稱。

## 常見變體與邊緣案例

| 情況 | 處理方式 |
|-----------|------------------|
| **非常大的表格** (≥ 100 000 列) | 在處理前使用 `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` 以降低記憶體使用量。 |
| **自訂欄位順序** | 在呼叫 `ProcessSmartMarkers` 前重新排列 `DataTable` 中的 `DataColumn` 物件。 |
| **多個不同名稱的 DataTable** | 為每個表格呼叫 `ProcessSmartMarkers`；Aspose.Cells 會自動為每個名稱建立獨立工作表。 |
| **需要帶樣式的標題列** | 處理完畢後，存取 `Worksheet.Cells["A1"]` 並套用 `Style` 屬性（字型、背景）。 |
| **改為儲存至串流而非檔案** | 將 `workbook.Save(outputPath, SaveFormat.Xlsx)` 換成 `workbook.Save(stream, SaveFormat.Xlsx)`。 |

**專業提示：** 總是將檔案系統操作包在 `try…catch` 區塊中，以便及早發現權限問題。

## 完整原始碼（可直接複製）

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### 預期輸出

執行程式會印出：

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

開啟 `DuplicateSheets.xlsx` 後，可看到名為 **Sheet1** 的工作表，其 `Id` 欄位包含值 `1, 2, 3, 4, 5`。若您之後在同一工作簿中再處理另一個名稱為 `"Sheet1"` 的 `DataTable`，Aspose.Cells 會自動建立 **Sheet1_1**、**Sheet1_2** 等工作表。

## 結論

您現在已掌握如何 **create excel sheet** 從 `DataTable` 於 C# 中建立、**export datatable to excel**、**add rows to datatable**，以及使用自動命名產生 **create multiple excel sheets**，最後 **save workbook as xlsx**。完整可執行的範例示範了端對端工作流程，並提供大型資料集與自訂樣式的實用技巧。

### 接下來做什麼？

* 探索 **cell formatting**（字型、顏色、邊框），於 `ProcessSmartMarkers` 後存取 `Worksheet.Cells` 進行設定。  
* 使用 **SmartMarker loops** 在單一工作簿中產生主從報表。  
* 若需要純文字表示，可改為 **CSV export**，只要將 `SaveFormat.Csv` 取代即可。  

歡迎將程式碼套用到您自己的資料來源——無論是資料庫查詢、API 回應，或是記憶體集合。祝您開發順利！

## 接下來應該學什麼？

以下教學與本指南緊密相關，能進一步深化您所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並探索在專案中使用的其他實作方式。

- [如何使用 Aspose.Cells for .NET 建立並儲存 Excel 工作簿為 ODS](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [如何使用 Aspose.Cells for Java 建立並儲存 Excel 工作簿為 SVG](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [如何使用 Aspose.Cells Java 建立並匯出 Excel 為 HTML | 工作簿操作指南](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}