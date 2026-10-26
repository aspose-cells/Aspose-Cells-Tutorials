---
category: general
date: 2026-10-26
description: 學習如何使用 C# 與 Aspose.Cells 將 DataTable 匯入 Excel 工作表，僅需幾行程式碼即可保留樣式與標題。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: zh-hant
lastmod: 2026-10-26
og_description: 如何使用 C# 與 Aspose.Cells 將 DataTable 匯入 Excel 工作表。請參考本完整指南，以保留樣式、標題與格式。
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: 如何將 DataTable 匯入 Excel 工作表 – C# 步驟教學
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: 如何使用 C# 將 DataTable 匯入 Excel 工作表
url: /zh-hant/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中將 DataTable 匯入 Excel 工作表

如果您需要 **how to import datatable** 到 Excel 工作表，本指南將示範在 C# 中的完整步驟。無論是建構報表引擎或匯出 Grid 資料，您都能看到如何在 Aspose.Cells 的協助下保留欄位標題與儲存格樣式。此解決方案支援 .NET 6 以上，且只需幾行程式碼。

將 DataTable 匯入試算表是常見需求，但開發者常忘記啟用樣式傳遞或正確傳遞標題旗標。在本教學中，您將學會如何設定 **ImportTableOptions**、開啟 **ImportDataTableStyle**，以及安全呼叫 `ImportDataTable`。完成後，您將擁有一個可直接放入任何 C# 專案的即用方法。

## 前置條件

開始之前，請確保您已具備：

* 已安裝 .NET 6 SDK 或更新版本。
* 已取得 **Aspose.Cells for .NET** 的授權版（免費試用版可用於測試）。
* 具備 `DataTable` 與 Excel 基本概念的基礎知識。
* 如 Visual Studio 2022 等支援 C# 的 IDE（任何支援 C# 的編輯器皆可）。

除 `Aspose.Cells` 之外，無需額外的 NuGet 套件。

## 步驟 1：將來源資料取回為 DataTable

當您要回答 **how to import datatable** 時，第一件事就是先取得資料。在大多數實務情境中，`DataTable` 來源可能是資料庫查詢、CSV 解析器，或是記憶體集合。以下是一個最小範例，示範如何建立包含數筆資料的表格：

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*為什麼這很重要*：先建構 `DataTable`，即可自行決定欄位順序、資料型別與標題名稱——這些資訊在稍後匯入 Excel 工作表時都會被完整保留。

## 步驟 2：建立 `ImportTableOptions` 並啟用樣式匯入

在回答 **how to import datatable** 時，接下來要決定是否要保留來源 `DataTable` 已設定的視覺樣式（字型、顏色、框線）。Aspose.Cells 提供 `ImportTableOptions` 類別供您細部控制。將 `ImportDataTableStyle = true` 設為 `true` 後，樣式資訊會被複製到目標工作表。

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*為什麼這很重要*：若未啟用 `ImportDataTableStyle`，匯入的儲存格將使用預設工作表樣式，導致先前在 `DataTable` 上設定的自訂格式遺失。此旗標對於打造精緻的匯出結果相當關鍵。

## 步驟 3：將 DataTable 匯入工作表，並包含標題列

現在您已具備所有回答 **how to import datatable** 所需的資訊。建立工作簿、選取工作表，然後呼叫 `ImportDataTable`。方法的第二個參數（`true`）告訴 Aspose.Cells 在第一列寫入欄位標題。

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

執行 `ExportDataTableToExcel("Employees.xlsx")` 後，會產生 `Employees.xlsx` 檔案，第一列包含 **Id**、**Name** 與 **Department**，且每個儲存格皆保留原始 `DataTable` 定義的樣式。

### 完整可執行範例

以下是一個完整、獨立的主控台程式，示範 **how to import datatable** 並將結果儲存至目前目錄。只要複製貼上到新專案，即可執行。

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**預期輸出**  
開啟 `Employees.xlsx` 時，您會看到：

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

所有儲存格皆保留 DataTable 的預設樣式（字型、對齊方式）。若您在匯入前已對 `DataTable` 套用自訂樣式，這些樣式也會在工作表中完整呈現，因為 `ImportDataTableStyle` 已設為 `true`。

## 常見問題與最佳實踐

| 問題 | 為什麼會發生 | 如何避免 |
|------|--------------|----------|
| **標題遺失** | 在 `ImportDataTable` 的第二個參數傳入 `false`，會跳過欄位名稱。 | 需要標題時務必傳入 `true`，或在匯入前自行寫入標題列。 |
| **樣式未傳遞** | 忘記啟用 `ImportDataTableStyle`。 | 在 `ImportTableOptions` 中設定 `ImportDataTableStyle = true`。 |
| **大型表格效能下降** | 未分批匯入數百萬列資料。 | 使用分批匯入或利用 `ImportDataTable` 的 `startRow` 重載以串流方式寫入。 |
| **工作表參照錯誤** | 只存在一張工作表卻使用 `workbook.Worksheets[1]`。 | 使用 `workbook.Worksheets[0]`，或以 `workbook.Worksheets.Add()` 新增工作表。 |
| **授權過期** | Aspose.Cells 試用版在 30 天後會加上浮水印。 | 使用 `License license = new License(); license.SetLicense("Aspose.Cells.lic");` 套用有效授權。 |

**小技巧**：若匯入後需要套用自訂主題，可呼叫 `ws.Cells.ApplyStyle(style)`，其中 `style` 為您事先配置好的 `Style` 物件，可在多列間重複使用。

## 延伸應用

既然您已掌握 **how to import datatable**，可以進一步探索以下情境：

* **匯入多張資料表** – 在不同工作表上重複匯入動作。
* **條件格式化** – 匯入後使用 `ws.Cells.ApplyConditionalFormatting` 加入規則。
* **匯出為 CSV** – 若需純文字格式，可使用 `workbook.Save("file.csv", SaveFormat.Csv)`。
* **回寫至 DataTable** – 使用 `ws.Cells.ExportDataTable` 驗證資料的來回一致性。

上述所有延伸皆以本教學的核心流程為基礎：取得資料、設定匯入選項、呼叫單一 Aspose.Cells 方法。

## 結論

您現在已掌握使用 C# 透過 Aspose.Cells **how to import datatable** 到 Excel 工作表的完整、可投入生產環境的解法。本文說明了取得來源資料、以 `ImportTableOptions` 設定 `ImportDataTableStyle`，以及使用 `ImportDataTable` 完成匯入。依循範例程式碼，您即可自動保留標題與樣式，並可依需求擴充至更大資料集、多工作表或額外格式設定。

準備好自動化您的報表工作流程了嗎？試著將範例 `DataTable` 換成真實的資料庫查詢、實驗自訂儲存格樣式，並將此方法整合到現有的服務層。祝您開發順利！

## 接下來該學什麼？

以下教學與本篇內容密切相關，能進一步深化您對 API 功能的掌握，並提供其他實作方式的範例：

- [How to Import Arrays into Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [How to Import XML Data into Excel with Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [How to Import HTML-Formatted DataTables into Excel Using Aspose.Cells for .NET](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}