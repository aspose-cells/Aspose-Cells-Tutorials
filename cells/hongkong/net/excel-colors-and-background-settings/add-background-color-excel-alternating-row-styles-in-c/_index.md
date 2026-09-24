---
category: general
date: 2026-04-07
description: 使用 C# 為 Excel 行添加背景顏色。學習如何套用交錯列顏色、設定實心背景樣式，並在單一工作流程中將 DataTable 匯入 Excel。
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: zh-hant
og_description: 使用 C# 為 Excel 行添加背景色。本指南示範如何套用交錯列顏色、設定純色背景，以及高效匯入 DataTable 至 Excel。
og_title: 在 Excel 中添加背景顏色 – C# 中的交錯列樣式
tags:
- C#
- Excel
- DataTable
- Styling
title: 在 Excel 中加入背景色 – C# 交替行樣式
url: /zh-hant/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中添加背景顏色 – 交錯列樣式（C#）

有沒有曾經需要 **add background color excel** 行，但不確定要怎樣在不寫上千行繁瑣程式碼的情況下做到？你並不孤單——大多數開發者在第一次嘗試讓試算表看起來不只是原始資料時，都會碰到這個問題。  

好消息是？只要幾分鐘，你就可以 **apply alternating row colors**、設定 **solid background**，甚至 **import datatable to excel**，使用 C# 中乾淨且可重用的模式。  

在本教學中，我們將一步步說明完整流程，從將資料拉入 `DataTable` 到以淡黃色‑白色條紋樣式為每一列加上樣式。除了像 **ClosedXML** 或 **GemBox.Spreadsheet** 這類可靠的 Excel 處理套件外，無需其他外部函式庫，你也會了解為何此方法既高效又易於維護。

## 你將學到什麼

- 如何取得資料並將其寫入 Excel 工作表。
- 如何使用交錯背景顏色 **style excel rows**。
- 使用 `Style` 物件實作 **set solid background** 的機制。
- 如何在保留列樣式的同時 **import datatable to excel**。
- 處理如空資料表或自訂配色方案等邊緣情況的技巧。

> **專業提示：** 如果你已經在使用支援樣式建立的函式庫的工作簿物件（`wb`），可以在多個工作表之間重複使用相同的 `Style` 實例──可節省記憶體並保持程式碼整潔。

---

## 步驟 1：取得資料 – 準備 DataTable

在任何樣式套用之前，我們需要一個列的來源。在大多數實務情境中，這通常來自資料庫、API 或 CSV 檔案。為了說明，我們僅在記憶體中建立一個簡單的 `DataTable`。

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**為什麼這很重要：** 使用 `DataTable` 可提供一個具結構認知的表格容器，讓 Excel 函式庫直接匯入，免除逐格寫入的需求。

---

## 步驟 2：建立列樣式 – **Apply alternating row colors**

現在我們將建立一個 `Style` 物件陣列——每列一個，讓每列都能擁有自己的背景。我們使用的模式是偶數列使用淡黃色，奇數列使用白色的經典交錯樣式。

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**說明：**  
- `wb.CreateStyle()` 會提供一個乾淨的樣式物件，你可以在不影響其他樣式的情況下調整它。  
- 三元運算子 `(i % 2 == 0)` 判斷列是偶數（淡黃色）還是奇數（白色）。  
- 設定 `Pattern = BackgroundType.Solid` 是關鍵步驟，可 **set solid background**；若不這樣設定，顏色會被忽略。

---

## 步驟 3：取得目標工作表

大多數函式庫都會提供工作表集合。我們將使用第一個工作表，但你也可以自行指定任何索引或名稱。

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

如果工作簿是全新建立，函式庫通常會自動為你建立一個預設工作表。否則，你可以明確地新增一個：

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## 步驟 4：匯入帶有列樣式的 DataTable – **Import datatable to excel**

樣式準備好後，最後一步是將 `DataTable` 推入工作表，同時為每一列套用相對應的樣式。

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**背後發生了什麼？**  
- `true` 表示方法會將欄位標題寫入第一列。  
- `0, 0` 標示左上角 (A1) 為插入點。  
- `rowStyles` 把每個 `Style` 與相對應的資料列對齊，讓我們得到先前準備的交錯顏色。

---

## 步驟 5：儲存工作簿

最後一步是將工作簿持久化為檔案，讓你可以在 Excel 中開啟並看到結果。

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

開啟檔案後，你應該會看到整齊排版的工作表：  

- 標題列為粗體（函式庫預設樣式）。  
- 第 1、3、5… 列為乾淨的白色背景。  
- 第 2、4、6… 列則填入淡黃色，方便閱讀。

### 預期輸出快照

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

第 2、4、6… 列會呈現淡黃色背景——正是我們想要的 **apply alternating row colors** 效果。

![Add background color excel example](https://example.com/excel-background.png "Add background color excel example")

*(Alt 文字包含主要關鍵字以利 SEO。)*

---

## 處理邊緣情況與變化

### 空的 DataTable

如果 `dataTable.Rows.Count` 為零，`rowStyles` 陣列會是空的，`ImportDataTable` 仍會寫入標題列（若 `includeHeaders` 為 `true`）。不會拋出例外，但你可能想要避免產生幾乎空白的檔案：

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### 自訂顏色方案

想要藍色/灰色條紋取代黃/白嗎？只要更換 `Color` 的值即可：

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

隨意從設定檔中取得顏色，讓非開發人員也能在不修改程式碼的情況下調整配色。

### 在多個工作表間重複使用樣式

如果你將多個資料表匯出到同一本工作簿，可以一次產生樣式陣列並重複使用：

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

只要注意兩個資料表的列數相同，或是為每個工作表產生新的陣列。

---

## 完整範例程式

把所有步驟整合起來，以下是一個可自行貼上至 console 應用程式的完整範例。

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

執行程式，開啟 `Report.xlsx`，即可看到如說明般的交錯背景。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}