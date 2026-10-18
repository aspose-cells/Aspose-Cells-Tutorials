---
category: general
date: 2026-05-30
description: 學習如何在 C# 工作表中加入交錯列色彩、以實心填滿模式設定儲存格背景，並輕鬆自訂工作表儲存格樣式。
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: zh-hant
og_description: 在 C# 工作表中輕鬆實現交錯列色彩。學習設定儲存格背景、使用純色填滿模式，並精通工作表儲存格樣式。
og_title: C# 工作表交替列顏色 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: C# 工作表交錯列色彩完整指南
url: /zh-hant/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 工作表中交替列顏色 – 完整指南

有沒有想過如何透過 **交替列顏色** 讓你的 Excel 匯出看起來更精緻？你並不孤單——開發者常常問如何在不寫上千行程式碼的情況下 *為列加入背景顏色*。  

在本教學中，我們將一步步說明如何 **設定儲存格背景**、套用 **實心填滿樣式**，以及控制 **工作表儲存格樣式**，讓最終結果既易讀又具視覺吸引力。

## 你將學會

- 將資料取回為 `DataTable`（或任何表格來源）。  
- 建立交替兩種顏色的 `Style` 物件陣列。  
- 在匯入 `DataTable` 時套用這些樣式至工作表。  
- 驗證輸出結果，並在需要時微調顏色或樣式。  

不需要額外工具，只要有 .NET 環境與試算表函式庫（範例使用 **Aspose.Cells**）即可。完成後，你將擁有一個可重複使用的方法，能直接嵌入任何報表流程。

---

## 步驟 1：將來源資料取回為 `DataTable`

首先，沒有資料就無法套用樣式。以下是一個簡易的輔助程式，會建立一個帶有範例列的 `DataTable`。在實際專案中，你可以改成資料庫呼叫或 CSV 解析。

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **為什麼這很重要：** 把資料放在 `DataTable` 中，可讓工作表引擎一次 **匯入**，自動保留欄位名稱與資料型別。

## 步驟 2：建立 **交替列顏色** 樣式

接下來，我們會產生一個 `Style` 物件陣列——每一列對應一個樣式，使偶數列使用淡黃色，奇數列使用淡青色。這就是 **交替列顏色** 的核心技巧。

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### 為什麼使用 **實心填滿樣式**？

`Pattern` 屬性告訴引擎如何繪製顏色。`Solid` 填滿可確保整個儲存格背景被完整上色，避免出現淡淡的格線。這是想要 **設定儲存格背景** 且保持乾淨外觀時最常用的方式。

## 步驟 3：以已備好的樣式匯入 `DataTable`

樣式陣列準備好後，匯入呼叫只需要一行程式碼。Aspose.Cells 會自動將對應的樣式套用到每一列。

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **底層發生了什麼？**  
> 函式庫會遍歷每一列，將值寫入儲存格，然後從 `rowStyles` 取出相對應的 `Style` 套用。因為我們已設定 **實心填滿樣式**，同一列的所有儲存格會繼承相同的背景顏色，從而產生完美的 **交替列顏色**。

## 步驟 4：儲存活頁簿並驗證結果

簡單儲存後，即可在 Excel（或任何相容檢視器）開啟檔案，觀察效果。

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

開啟檔案時，第 1、3、5… 列會是淡黃色，第 2、4、6… 列會是淡青色。欄位標題保持白色，讓資料更突出。

![Worksheet showing alternating row colors](/images/alternating-row-colors.png "Screenshot of worksheet with alternating row colors")

*Image alt text:* **alternating row colors** screenshot of a worksheet where each row’s background alternates between light yellow and light cyan.

## 步驟 5：進一步自訂（可選）

### 更換顏色

如果品牌使用不同色調，只要把 `Color.LightYellow` 與 `Color.LightCyan` 換成任意 `System.Drawing.Color` 即可。例如：

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### 使用不同的 **背景類型**

雖然 `BackgroundType.Solid` 最常見，你也可以嘗試 `BackgroundType.Gray125`、`BackgroundType.Horizontal`，或任何函式庫支援的圖樣。這會改變視覺質感，同時仍然 **加入背景顏色**。

### 為特定欄位套用 **工作表儲存格樣式**

有時只想在資料欄位套用交替效果，保留第一欄（如 ID）不變。可以為該欄位建立獨立樣式，並在匯入後指定：

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## 結論

現在你已掌握在 C# 工作表中實作 **交替列顏色** 的完整、可重複使用方案。透過建立 `Style` 物件陣列、以 **實心填滿樣式** **設定儲存格背景**，以及一次呼叫匯入 `DataTable`，即可產出專業外觀的報表，且程式碼量極少。  

接下來你可以：

- 為標題列 **加入背景顏色** 以加強強調。  
- 結合條件格式，提供動態視覺提示。  
- 探索其他 **工作表儲存格樣式** 屬性，如字型、邊框或數字格式。

在你的下一次匯出流程中試試看吧——使用者一定會感謝更整潔、易讀的試算表。快樂編程！

## 接下來該學什麼？

- [Set Row Height in Worksheet with Aspose.Cells for .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Convert Excel Cell Names to Row and Column Indices Using Aspose.Cells for .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Set Worksheet Tab Colors in Excel Using Aspose.Cells .NET - A Comprehensive Guide](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}