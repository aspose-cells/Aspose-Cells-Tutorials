---
category: general
date: 2026-06-17
description: 使用 C# 設定 Excel 日期格式，同時設定儲存格背景、套用前景色，並在匯入時為 Excel 欄位著色。一步一步學習。
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: zh-hant
og_description: 使用 C# 在 Excel 中設定日期格式，同時設定儲存格背景、套用前景色，並在匯入時為 Excel 欄位著色。完整教學。
og_title: 使用 C# 在 Excel 中設定日期格式 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: 設定 Excel 日期格式（使用 C#）– 完整匯入格式化指南
url: /zh-hant/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中使用 C# 設定日期格式 – 完整匯入格式化指南

是否曾經需要在由 C# 程式產生的 Excel 工作表中 **設定日期格式**，同時又想為欄位設定自訂的背景或文字顏色？你並不是唯一的需求者。在許多報表情境下，我們會從資料庫取得 `DataTable`，直接放入工作表，然後急忙調整日期顯示與欄位顏色，使其看起來更佳。

在本教學中，我們將一步步示範一個乾淨、端到端的解決方案，能 **設定日期格式**、**設定儲存格背景**、**套用前景色**，甚至 **為 Excel 欄位著色**，在匯入資料的同時完成。完成後，你將擁有一套可重複使用的 **excel import formatting** 模式，省去一再試錯的麻煩。

> **你需要的環境**  
> * .NET 6+（或 .NET Framework 4.7+）  
> * Aspose.Cells for .NET（免費試用版即可測試）  
> * `DataTable` 資料來源 – 任意 ADO.NET 查詢皆可  
> * Visual Studio 或你慣用的 IDE  

讓我們開始吧。

---

## 解決方案概觀

我們將問題拆成三個邏輯區塊：

1. **取得來源資料** – 包含欲匯出的 `DataTable`。  
2. **建立欄位專屬樣式** – 為日期欄位、文字欄位各自建立樣式，並可自行加入其他樣式。  
3. **以樣式匯入資料表** – 使用 `Worksheet.Cells.ImportDataTable`，讓每個欄位自動套用先前準備好的樣式。

為什麼採用這種方式？因為 Aspose.Cells 允許在 `ImportDataTable` 呼叫時直接附加 `Style` 陣列，省去二次遍歷重新套用格式的步驟。這樣更快、更不易出錯，也讓程式碼更整潔。

---

## 步驟 1：取得要匯出的資料

首先，你必須有一個 `DataTable`。在真實專案中，你可能會呼叫 stored procedure 或使用 Entity Framework 來填充它，但為了說明，我們先模擬一個簡單的表格，包含日期欄位與文字欄位。

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **小技巧：** 若來源資料的日期欄位允許 null，請確保欄位型別為 `typeof(DateTime?)` – Aspose 仍會遵循之後指定的格式。

---

## 步驟 2：建立樣式陣列 – 每個欄位一個樣式

現在，我們建立一個長度等於 `DataTable` 欄位數的 `Style[]`。每個元素都會保存對應欄位的格式設定。

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 為第一欄設定日期格式

第一欄（`OrderDate`）應顯示為「MM/dd/yyyy」。Aspose 內建的短日期格式編號為 14，你也可以自行提供自訂格式字串。

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**為什麼這很重要：** Excel 以序號方式儲存日期。指定數字格式後，Excel 會把這些序號轉換為可讀的日期，而非原始數字。

### 2.2 為第二欄設定儲存格背景

我們為 `CustomerName` 欄位加上淡藍色背景。這正是 **set cell background** 發揮作用的地方。

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **注意：** 若未將 `Pattern` 設為 `Solid`，前景色將不會顯示，因為預設圖樣為「None」。

### 2.3 套用前景（文字）顏色 – 可選額外項目

如果你也想讓文字本身呈現對比色，只要在同一個樣式中調整即可：

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

這樣即可滿足 **apply foreground color** 的需求，同時保留欄位的背景設定。

---

## 步驟 3：以已定義的樣式匯入 DataTable

樣式準備好後，最後一步只需要一行程式碼，即可匯入資料並逐欄套用樣式。

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**運作原理：** Aspose 會讀取 `columnStyles` 陣列，將每個 `Style` 對應到相同索引的欄位。標題列會使用預設樣式，除非你為第 0 列提供了另一套樣式。

### 3.1 儲存活頁簿

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

執行程式，開啟 *FormattedReport.xlsx*，你應該會看到：

- **OrderDate** 欄位以日期顯示（例如 `06/15/2026`）。  
- **CustomerName** 欄位有淡藍色填滿且文字為深藍色。  

這就是在不到 30 行 C# 程式碼內完成的 **excel import formatting** 工作流程。

---

## 步驟回顧（含原因說明）

| 步驟 | 你要做什麼 | 為什麼重要 |
|------|------------|------------|
| **取得資料** | 呼叫 `GetData()` 取得 `DataTable`。 | 提供 Aspose 可直接 ingest 的結構化來源。 |
| **建立樣式陣列** | 配置與欄位數相同的 `Style[]`。 | 讓單次匯入即可完成逐欄樣式設定。 |
| **設定日期格式** | `columnStyles[0].Number = 14;` | 確保 Excel 正確顯示日期。 |
| **設定背景顏色** | `ForegroundColor = LightBlue; Pattern = Solid;` | 突顯欄位，滿足 **set cell background**。 |
| **套用前景顏色** | `Font.Color = DarkBlue;` | 提升可讀性，符合 **apply foreground color**。 |
| **匯入並套用樣式** | `ImportDataTable(..., columnStyles);` | 一次匯入即保留全部格式。 |
| **儲存活頁簿** | `wb.Save(...);` | 將結果寫入檔案供下游使用。 |

---

## 處理例外情況與常見問題

### 若欄位超過兩個怎麼辦？

只要擴充 `columnStyles` 陣列，並為每個索引指定 `Style` 即可。未指定的索引會使用預設樣式，這通常沒問題。

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### 如何把欄位格式化為貨幣？

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### 可以單獨變更標題列樣式嗎？

可以。匯入完成後，取得第一列並套用不同的樣式：

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### 若 DataTable 含有 null 日期該怎麼處理？

Aspose 會將這些儲存格留空。若想顯示「N/A」等佔位文字，可先前置處理表格：

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

然後調整樣式，使用自訂格式在偵測到哨兵值時顯示「N/A」。

---

## 完整範例程式

以下是可直接複製貼上的完整程式。以 Console 應用程式執行，即可產生格式化好的 Excel 檔案。

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelExportDemo
{
    static void Main()
    {
        // 1️⃣ 取得資料
        DataTable dataTable = GetData();

        // 2️⃣ 建立活頁簿與樣式陣列
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 2a️⃣ 日期欄位 – 設定日期格式
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date (MM/dd/yyyy)

        // 2b️⃣ 文字欄位 – 設定背景與前景顏色
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].ForegroundColor = Color.LightBlue;
        columnStyles[1].Pattern = BackgroundType.Solid;
        columnStyles[1].Font.Color = Color.DarkBlue; // apply foreground color

        // 3️⃣ 匯入並套用格式
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 可選：設定標題列樣式
        Style headerStyle = wb.CreateStyle();
        headerStyle.Font.IsBold = true;
        headerStyle.ForegroundColor = Color.Gold;
        headerStyle.Pattern = BackgroundType.Solid;
        ws.Cells


## 接下來你可以學什麼？

以下教學與本指南內容緊密相關，能幫助你進一步掌握 API 功能，或探索在專案中使用的其他實作方式。

- [在 Aspose.Cells for .NET 中設定 Excel 儲存格字體顏色](/cells/english/net/formatting/setting-font-color/)
- [使用 Aspose.Cells 在 .NET Excel 中設定字體顏色](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [使用 Aspose.Cells for .NET 以像素設定 Excel 欄寬 – 步驟指南](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}