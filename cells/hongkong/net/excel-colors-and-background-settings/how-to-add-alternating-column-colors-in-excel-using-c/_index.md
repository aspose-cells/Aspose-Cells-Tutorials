---
category: general
date: 2026-10-01
description: 使用 C# 為 Excel 設定交錯欄位顏色 – 學習如何從 DataTable 建立 Excel 檔案、設定儲存格背景顏色，以及將 DataTable
  匯入 Excel 並套用樣式化欄位。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: zh-hant
lastmod: 2026-10-01
og_description: 交替欄位顏色的 Excel 輕鬆上手。跟隨本指南，從 DataTable 建立 Excel 檔案、設定儲存格背景顏色（C#），以及將
  DataTable 匯入 Excel 並套用樣式欄位。
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: 使用 C# 為 Excel 添加交替列顏色 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: 如何使用 C# 在 Excel 中加入交替列顏色
url: /zh-hant/net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 C# 添加交替欄位顏色

如果您需要在應用程式產生的報告中加入 **alternating column colors excel**，本指南將提供完整解決方案。您將會看到如何從 `DataTable` 建立 Excel 檔案、以 C# 方式設定儲存格背景顏色，並在匯入資料表至 Excel 時為每個欄位套用不同的樣式。

本教學涵蓋您所需的一切：必備的 NuGet 套件、完整可執行的程式碼範例，以及每個步驟重要性的說明。完成後，您將擁有一個可直接在 Microsoft Excel 中開啟的已套用樣式的活頁簿。

## 前置條件

* .NET 6.0（或更新版本）SDK 已安裝  
* Visual Studio 2022（或任何相容 C# 的 IDE）  
* **Aspose.Cells for .NET** 函式庫 – 使用以下方式安裝  

```bash
dotnet add package Aspose.Cells
```

Aspose.Cells 提供範例中使用的 `Workbook`、`Worksheet`、`Style` 與 `BackgroundType` 類別。

## 步驟 1：將來源資料取得為 `DataTable`

第一步是取得您想匯出的資料。在實際專案中，您可能會從資料庫查詢、API 呼叫或任何記憶體集合填充 `DataTable`。

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**為什麼這很重要：**  
`DataTable` 是一個通用容器，可順利對映至 Excel 工作表。使用 `DataTable` 可讓您 **create excel file from datatable c#**，無需為每個欄位自行撰寫迴圈。

## 步驟 2：建立新活頁簿並取得第一個工作表

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**說明：**  
`Workbook` 為根物件；`Worksheets[0]` 取得預設工作表，資料將放置於此。

## 步驟 3：為每個欄位準備不同的樣式（交替背景顏色）

為了實現 **alternating column colors excel**，我們為每個欄位產生一個 `Style`，並指派在兩種淡色之間交替的背景顏色。

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**為什麼使用迴圈：**  
此迴圈確保 **set cell background color c#** 能一致套用，即使執行時欄位數量變動，也能使解決方案在動態報告中保持穩健。

## 步驟 4：將 `DataTable` 匯入工作表，套用欄位樣式

Aspose.Cells 可以直接匯入 `DataTable`，我們也能傳入樣式陣列以為每個欄位著色。

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**背後的運作原理：**  
`ImportDataTable` 會先寫入標題列，接著寫入每筆資料列。由於我們提供了 `columnStyles`，指定欄位的每個儲存格都會套用相對應的樣式，從而得到期望的交替顏色。

## 步驟 5：將已套用樣式的活頁簿儲存為檔案

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

當您在 Excel 中開啟 *StyledTable.xlsx* 時，會看到每個欄位交替上色，使表格更易於閱讀。

## 完整、可執行的範例

將所有部件組合起來，以下是一個可自行複製、貼上並執行的完整程式。

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### 預期輸出

* 一個名為 **StyledTable.xlsx**、位於 `C:\Temp\` 的檔案。  
* 工作表顯示三個欄位（`Id`、`Name`、`Score`），交替的背景顏色為：第 1 與第 3 欄為 *LightYellow*，第 2 欄為 *LightCyan*。  
* `DataTable` 的所有資料列皆顯示在標題列之下。

## 常見問題與邊緣情況

| Question | Answer |
|----------|--------|
| *我可以使用其他顏色嗎？* | 可以。將 `System.Drawing.Color.LightYellow` 與 `LightCyan` 替換為任意 `System.Drawing.Color` 值即可。 |
| *如果 DataTable 有很多欄位怎麼辦？* | 迴圈會自動為每個欄位建立樣式，因而在不修改程式碼的情況下即可擴展此模式。 |
| *我需要釋放活頁簿資源嗎？* | Aspose.Cells 實作了 `IDisposable`。若將 `Workbook` 包在 `using` 區塊中，資源會即時釋放。 |
| *如何將相同的交替顏色套用到列而非欄位？* | 為列建立 `Style[]`，並呼叫 `worksheet.Cells.ImportDataTable(..., rowStyles)` – Aspose.Cells 的多載支援兩者。 |
| *我可以直接寫入串流（例如用於 Web API）嗎？* | 可以。使用 `workbook.Save(stream, SaveFormat.Xlsx);` 取代檔案路徑即可。 |

## 現場小技巧

* **專業提示：** 若在單次執行中產生多個活頁簿，請快取樣式物件 – 建立樣式的成本相對低，但重複使用可減少記憶體佔用。  
* **注意事項：** 在非 Windows 平台使用 `System.Drawing.Color` 時，請加入 `System.Drawing.Common` NuGet 套件，並確保執行環境支援 GDI+。

## 結論

現在您已了解如何透過在 C# 中從 `DataTable` 建立 Excel 檔案、使用 Aspose.Cells 設定儲存格背景顏色，並以樣式化的欄位陣列 **import datatable to excel**，達成 **alternating column colors excel**。此方法快速、易於維護，且適用於任何規模的資料集。

### 後續步驟

* 探索 **set cell background color c#** 以實作條件格式（例如突顯低分）。  
* 將此技巧與 **create excel file from datatable c#** 結合，產生多工作表報告。  
* 研究 Aspose.Cells 的圖表 API，為同一本活頁簿加入視覺摘要。

歡迎依照專案需求調整顏色、檔案格式或資料來源。祝開發順利！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [Set Column Background in Excel with C# – Complete Guide](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Add background color excel – Alternating Row Styles in C#](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Create Workbook C# – Import DataTable to Excel with Styles](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}