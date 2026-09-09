---
category: general
date: 2026-03-01
description: 使用 C# 將帶格式的資料匯入 Excel。學習如何將 DataTable 匯入 Excel，並在幾個步驟內為儲存格添加背景顏色。
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: zh-hant
og_description: 使用 C# 將帶格式的資料匯入 Excel。逐步指南示範如何匯入 DataTable 並為儲存格添加背景色。
og_title: 將資料與格式匯入 Excel – C# 指南
tags:
- C#
- Excel
- DataTable
- Formatting
title: 使用 C# 將帶格式的資料匯入 Excel
url: /zh-hant/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 將資料匯入 Excel 並保留格式

是否曾經需要 **匯入帶格式的資料** 到 Excel 活頁簿，卻只得到一張平淡無奇的工作表？你並不孤單。大多數開發者在發現預設的匯入會把他們在來源資料中辛苦設定的顏色與樣式全部剝除時，都會卡在這裡。

在本教學中，我們將一步步示範一個完整、可直接執行的解決方案，**將 DataTable 匯入 Excel** 並 **同時為 Excel 儲存格加入背景色**。不需要額外的後處理——你的試算表會直接以你想要的樣子呈現。

## 你將學會

- 如何將資料取回至 `DataTable`。
- 如何定義一組攜帶背景色的 `Style` 物件陣列。
- 如何使用這些樣式呼叫 `ImportDataTable`，讓匯入同時保留格式。
- 一個完整、可執行的範例，直接貼到 Console App 即可立即看到結果。
- 實務專案中的技巧、常見陷阱與變化寫法。

### 前置條件

- .NET 6.0 或更新版本（程式碼同樣適用於 .NET Framework 4.6+）。
- **GemBox.Spreadsheet** 套件（免費版已足夠示範）。
- 具備基本的 C# 與 Excel 概念。

如果你在想 *為什麼選 GemBox？*，原因在於它提供單行的 `ImportDataTable` 方法，接受樣式陣列——正是我們在 **匯入資料並保留格式** 時所需要的。

---

## 第一步：建立專案並加入 GemBox.Spreadsheet

先建立一個新的 Console App：

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **專業小技巧：** 免費版會將工作表限制在 150 k 個儲存格，對於示範來說已相當足夠。若遇到上限，可升級或改用 EPPlus，但 API 會稍有不同。

## 第二步：將來源資料取回為 `DataTable`

我們首先需要一個 `DataTable`，模擬平常從資料庫撈出的資料。以下是一段在記憶體中建立它的簡易輔助程式：

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**為什麼這很重要：** 透過將資料取得獨立成方法，你可以隨時換成任何來源——SQL、CSV、Web Service——而不必觸碰匯入邏輯。這樣的寫法讓本教學的 **如何將 DataTable 匯入 Excel** 更具可重用性。

## 第三步：定義要套用的樣式

接下來就是有趣的部分：我們會建立一個 `Style` 物件陣列，每個物件都有不同的 `ForegroundColor`。GemBox 允許設定 `BackgroundPatternColor`（儲存格填滿）與 `ForegroundColor`（文字顏色）。此示範會為前兩欄設定不同的顏色。

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**說明：**  
- `Style` 物件是輕量的容器；不需要為每個儲存格都新建一個。  
- 只要讓陣列的順序與欄位順序對應，GemBox 便會在匯入時自動套用相對應的樣式。  
- 這就是 **匯入資料並保留格式** 的關鍵——格式會隨資料一起傳遞，而不是事後再處理。

## 第四步：使用樣式將 `DataTable` 匯入工作表

資料與樣式都備妥後，我們可以建立活頁簿、取得第一張工作表，然後呼叫 `ImportDataTable`。方法簽章如下：

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

以下是實際使用方式：

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**背後發生了什麼？**  
- `true` 代表 GemBox 會把欄位名稱寫入第一列。  
- `0, 0` 表示匯入起始於 A1 儲存格。  
- `importStyles` 把每一欄與先前定義的顏色對應起來。  

當你開啟 *Report.xlsx* 時，會看到 **ID** 欄位呈淡藍色、**Name** 欄位呈淡綠色，而 **Score** 欄位則保持預設白色。這就是一次呼叫完成的 **匯入資料並保留格式**。

## 第五步：驗證結果（預期輸出）

開啟產生的 `Report.xlsx`，你應該會看到類似下表的內容：

| ID (淡藍色) | Name (淡綠色) | Score |
|------------|---------------|-------|
| 1          | Alice         | 93.5 |
| 2          | Bob           | 78.0 |
| 3          | Charlie       | 85.2 |
| 4          | Diana         | 91.3 |
| 5          | Ethan         | 67.8 |

- **ID** 欄位的儲存格背景為淡藍色。  
- **Name** 欄位的儲存格背景為淡綠色。  
- **Score** 欄位則保留預設的白色背景。

這樣的視覺提示讓報表一目了然，僅僅一點小小的設計，就能顯著提升使用者體驗。

![Excel 工作表顯示匯入資料並保留格式 – ID 欄位淡藍色，Name 欄位淡綠色](excel-screenshot.png "匯入資料並保留格式範例")

*圖片的 alt 文字已包含主要關鍵字以利 SEO。*

---

## 常見問題與邊緣案例

### 我可以套用的不只有背景顏色嗎？

當然可以。`Style` 允許設定字型、邊框、數字格式，甚至條件格式。例如，將分數大於 90 的儲存格設為粗體紅字：

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### 如果我的 DataTable 欄位比樣式陣列多，會怎樣？

GemBox 只會對陣列中有對應的欄位套用樣式。多出的欄位會使用預設樣式——不會拋出錯誤。

### 大量資料集可以使用嗎？

可以，但請留意免費版的儲存格上限（150 k 個儲存格）。若需產出巨量報表，建議購買授權或改用逐列寫入 `worksheet.Cells[row, col].Value = …` 的方式——那樣就失去一次匯入的便利性。

### 如何從既有的 Excel 範本匯入資料並保留格式？

可以先載入範本活頁簿：

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

這樣就能保留標頭圖示、頁腳以及任何既有樣式，同時對動態資料部份執行 **匯入資料並保留格式**。

---

## 完整可執行範例（直接複製貼上）

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

執行程式 (`dotnet run`) 後，開啟產生的 *Report.xlsx*，即可立即看到顏色套用的效果。

---

## 結論

現在你已掌握一套穩固、完整的方式，能在 **匯入資料並保留格式** 時，同時完成 DataTable 到 Excel 的轉換，讓報表即時具備視覺辨識度，提升使用者的閱讀效率。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}