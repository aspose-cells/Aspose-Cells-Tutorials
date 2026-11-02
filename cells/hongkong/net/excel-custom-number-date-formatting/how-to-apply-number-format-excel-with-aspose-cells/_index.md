---
category: general
date: 2026-10-10
description: 透過匯入 DataTable，快速在 Excel 套用數字格式、設定日期與貨幣格式，並在單一步驟中保留標題列。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: zh-hant
lastmod: 2026-10-10
og_description: 在 C# 中使用 Aspose.Cells 套用 Excel 數字格式。學習設定 Excel 日期格式、設定 Excel 貨幣格式，以及在匯入
  DataTable 時保留 Excel 標題列。
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: 在 C# 中套用 Excel 數字格式 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: 如何在 Aspose.Cells 中套用 Excel 數字格式
url: /zh-hant/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Aspose.Cells 中套用 Excel 數字格式

如果您需要在從 `DataTable` 載入資料時 **套用 Excel 數字格式**，本指南將逐步說明。您還將學習如何 **設定 Excel 日期格式**、**設定 Excel 貨幣格式**，以及在匯入過程中 **保留 Excel 標題列**，使最終工作表看起來專業，無需額外的後處理。

我們將從安裝函式庫說明到撰寫完整可執行的程式碼示例。完成後，您將能夠將任何 `DataTable` 匯入 Excel 活頁簿，自動格式化數值欄位，並保持標題列完整——只需幾行 C# 程式碼。

## 前置條件

* .NET 6.0 或更新版本（此程式碼亦相容於 .NET Framework 4.6+）
* Visual Studio 2022（或您偏好的任何 C# IDE）
* **Aspose.Cells for .NET** – 透過 NuGet 安裝：

```bash
dotnet add package Aspose.Cells
```

* `DataTable` 資料來源 — 範例使用輔助方法 `GetTable()` 來返回示範資料。

> **專業提示：** Aspose.Cells 為商業函式庫，但提供免費評估模式，可在最多 30 天內停用浮水印。

## 步驟 1：建立活頁簿並存取第一個工作表

Workbook 物件是所有 Excel 操作的入口。建立新活頁簿會自動產生索引為 0 的預設工作表。

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*為什麼需要這一步？*  
`Workbook` 管理檔案格式、計算引擎與樣式儲存庫。提前存取 `Worksheet` 可讓我們稍後將目標工作表傳遞給匯入方法。

## 步驟 2：將來源資料取得為 DataTable

在實際專案中，資料通常來自資料庫查詢、CSV 解析器或 API 回應。為說明起見，我們產生一個包含三個欄位的簡易 `DataTable`：**Product**、**Price** 與 **ReleaseDate**。

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*為什麼需要這一步？*  
`DataTable` 提供一個記憶體中的表格表示，Aspose.Cells 可直接匯入，且會保留欄位順序與資料類型。

## 步驟 3：準備 `Style` 陣列 – 每個欄位一個樣式

Aspose.Cells 允許在匯入時透過傳遞 `Style` 物件陣列，為每個欄位套用不同樣式。陣列長度必須與來源表格的欄位數相同。

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*為什麼需要這一步？*  
如果省略明確建立 (`CreateStyle()`) ，在設定 `Number` 時會拋出 `NullReferenceException`。初始化每個 `Style` 可確保之後的指派成功。

## 步驟 4：指定數字格式 – 貨幣與日期

Excel 透過 ID 識別內建數字格式。  
* **14** – 貨幣（例如 `$1,234.00`）  
* **22** – 短日期（`mm/dd/yyyy`）

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **注意：** 若需要自訂格式（例如 `"¥#,##0.00"`），請使用 `Style.Custom = "¥#,##0.00"` 取代內建 ID。

*為什麼需要這一步？*  
在匯入時套用正確的 **數字格式** 可免除後續遍歷儲存格二次變更格式的步驟。亦可確保 **format excel cells date** 與 **set currency format excel** 在所有列中保持一致。

## 步驟 5：匯入 DataTable 並保留標題列

`ImportDataTable` 方法可複製資料、保留第一列作為標題，並套用先前準備的欄位樣式。

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**預期輸出** – 開啟 `FormattedReport.xlsx` 後您會看到：

| 產品 | 價格（貨幣） | 發佈日期（日期） |
|------|------------|----------------|
| Widget A| $12.99 | 05/01/2023 |
| Widget B| $23.50 | 06/15/2023 |
| Widget C| $7.75 | 07/30/2023 |

標題列保持完整，**Price** 欄位顯示貨幣符號，**ReleaseDate** 欄位則呈現短日期格式——全部不需額外的樣式程式碼。

### 處理常見邊緣案例

| 情況                               | 解決方案 |
|-----------------------------------|----------|
| **欄位數多於樣式數**               | 確保 `columnStyles.Length` 等於 `sourceTable.Columns.Count`。缺少的項目會預設使用活頁簿的預設樣式。 |
| **數值欄位的 Null 值**            | Excel 會將 `null` 視為空儲存格；當之後輸入值時，數字格式仍會套用。 |
| **自訂地區特定貨幣**              | 使用 `columnStyles[i].Custom = "\"€\"#,##0.00"`，並將 `columnStyles[i].Number = -1` 以停用內建 ID。 |
| **大型表格（> 100 000 列）**       | 考慮使用帶有 `ImportTableOptions` 的 `ImportDataTable` 重載，以串流資料並降低記憶體壓力。 |
| **將相同樣式套用至多個欄位**       | 在陣列中重複使用相同的 `Style` 實例（例如 `columnStyles[1] = columnStyles[2] = dateStyle;`）。 |

## 加分項：使用自訂格式字串

若內建 ID 無法滿足需求，您可以自行定義自訂數字格式：

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

此方法讓您能完全掌控 **format excel cells date** 與 **set currency format excel**，超越預先定義的 ID。

## 結論

現在您已了解在使用 Aspose.Cells 匯入 `DataTable` 時，如何有效地 **套用 Excel 數字格式**。透過建立每欄位的 `Style` 陣列、指派內建或自訂的數字 ID，並使用能 **保留 Excel 標題列** 的 `ImportDataTable` 重載，您即可一次操作產生可直接發布的工作表。

### 接下來？

* 探索使用自訂模式（如 `"dddd, mmmm dd, yyyy"`）的 **set date format excel**。
* 將此技巧與 **conditional formatting** 結合，以突顯超出範圍的值。
* 在樞紐分析表或圖表中使用 **format excel cells date** 以進行動態報告。

歡迎嘗試不同的數字 ID 或自訂字串，以符合貴公司的樣式指南。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [套用 Excel 數字格式 – 分步說明欄位格式化指南](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [建立 Excel 活頁簿 C# – 套用貨幣格式並匯入 DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [使用 C# 設定 Excel 日期格式 – 完整匯入格式化指南](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}