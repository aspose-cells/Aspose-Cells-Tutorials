---
category: general
date: 2026-06-05
description: 在使用 Aspose.Cells 匯入時套用儲存格樣式。了解如何匯入帶格式的 DataTable、設定列樣式，並保持工作表整潔。
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: zh-hant
og_description: 在將 DataTable 匯入 Aspose.Cells 工作表時套用儲存格樣式。逐步指南，提供完整程式碼與技巧。
og_title: 使用 Aspose.Cells 套用儲存格樣式 – 匯入 DataTable
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  headline: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  type: TechArticle
- description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  name: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  steps:
  - name: How It Works
    text: 1. **Headers** – Because we passed `true`, Aspose writes “Name” and “Score”
      into the first row. 2. **Data Rows** – Each subsequent row receives the corresponding
      style from `importStyles`. 3. **Performance** – The method streams the data
      directly into the worksheet, which is faster than looping cell
  - name: What if My DataTable Has More Columns Than Styles?
    text: Aspose will apply the last style in the array to any extra columns. To avoid
      unexpected colors, always match the array length to the column count, or pass
      `null` for columns you don’t want styled.
  - name: Can I Apply Different Styles to Specific Rows?
    text: 'Absolutely. After the import, you can loop through rows and assign new
      `Style` objects based on conditions (e.g., highlight scores > 90 in green).
      Here’s a quick snippet:'
  - name: Does This Work with Large DataSets?
    text: Yes. `ImportDataTable` streams data efficiently, and applying a static style
      array adds negligible overhead. For millions of rows, consider using `ImportDataTable`
      in chunks or leveraging `Cells.ImportDataTable` with a `DataReader` for even
      better memory usage.
  - name: How Do I Preserve Existing Formatting in the Worksheet?
    text: If the target range already has formatting you want to keep, set the `ImportDataTable`
      overload’s `importOptions` parameter (`ImportTableOptions`) and tweak `ImportDataTableOptions.PreserveCellFormatting`.
      The default behavior overwrites styles with the ones you supply.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DataTable
title: 使用 Aspose.Cells 套用儲存格樣式 – 匯入具格式的 DataTable
url: /zh-hant/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 套用儲存格樣式 – 匯入 DataTable 並保留格式

有沒有想過在將 `DataTable` 拉入 Excel 工作表時如何 **套用儲存格樣式**？你並不是唯一有此疑問的人。在許多報表情境下，你需要資料一開始就呈現良好外觀——不需要之後手動格式化。好消息是 Aspose.Cells 讓 **匯入並保留格式** 變得輕鬆，讓你的列可以是紅色、藍色、粗體或任何你想要的樣式。

在本教學中，我們將逐步示範一個完整且可執行的範例，說明 **如何匯入 DataTable** 到工作表並 **套用儲存格樣式**。完成後，你將擁有一個可直接執行的 C# 主控台應用程式，能建立工作簿、為前兩欄設定樣式，並儲存檔案——全部使用 `aspose cells import` API。

## 你將學到什麼

- 在 .NET 專案中設定 Aspose.Cells  
- 建立一個模擬真實資料的範例 `DataTable`  
- 定義用於紅色與藍色字型的 `Style` 物件  
- 使用 `Worksheet.Cells.ImportDataTable` **匯入 DataTable 工作表** 同時套用樣式  
- 驗證結果並儲存工作簿  

不需要任何外部工具，只需純粹的 C# 與 Aspose.Cells。讓我們開始吧。

---

## 前置條件

在深入程式碼之前，請確保你具備以下條件：

| 需求 | 為何重要 |
|------|----------|
| .NET 6.0 或更新版本 | Aspose.Cells 23.x 目標為 .NET Standard 2.0+，因此 .NET 6 可提供最新的執行時功能。 |
| Aspose.Cells for .NET (NuGet) | 此函式庫提供我們需要的 `Workbook`、`Worksheet`、`Style` 與 `ImportDataTable` 方法。 |
| 基本的 C# 知識 | 你將了解類別、陣列與 `using` 陳述式。 |
| 開發工具 (IDE)（Visual Studio、VS Code、Rider） | 任意編輯器皆可使用，但需還原 NuGet 套件。 |

你可以在命令列中安裝此套件：

```bash
dotnet add package Aspose.Cells
```

---

## 步驟 1：建立新工作簿並存取第一個工作表

首先，讓我們建立一個 `Workbook` 並取得第一張工作表。可將工作簿想像成一本空白筆記本；第一個工作表就是我們要寫入的頁面。

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create a new workbook (equivalent to a new Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **小技巧：** 若需要多個工作表，只要使用 `wb.Worksheets.Add()` 新增，然後以名稱或索引來參考即可。

---

## 步驟 2：準備範例 DataTable（如何匯入 DataTable）

現在我們需要一些資料來匯入。實際專案中會呼叫資料庫，但為了說明，我們將在記憶體中建立一個 `DataTable`。

```csharp
        // Build a sample DataTable with two columns: Name and Score
        DataTable dataTable = new DataTable("Results");
        dataTable.Columns.Add("Name", typeof(string));
        dataTable.Columns.Add("Score", typeof(int));

        // Populate rows – imagine these came from a query
        dataTable.Rows.Add("Alice", 85);
        dataTable.Rows.Add("Bob", 92);
        dataTable.Rows.Add("Charlie", 78);
        dataTable.Rows.Add("Diana", 91);
```

> **為何重要：** 具備 `DataTable` 可讓我們在不依賴外部資源的情況下測試 **aspose cells import** 流程。

---

## 步驟 3：定義要套用到匯入儲存格的樣式

這裡就是魔法發生的地方。我們會建立兩個 `Style` 物件：一個使用紅色字型，另一個使用藍色字型。匯入時會依欄位套用這些樣式。

```csharp
        // Define an array of styles – one per column
        Style[] importStyles = new Style[2];

        // Style for the first column (Name) – red text
        Style redStyle = wb.CreateStyle();
        redStyle.Font.Color = Color.Red;
        importStyles[0] = redStyle;

        // Style for the second column (Score) – blue text
        Style blueStyle = wb.CreateStyle();
        blueStyle.Font.Color = Color.Blue;
        importStyles[1] = blueStyle;
```

> **注意：** `importStyles` 的長度必須與匯入的欄位數相同，否則 Aspose 會拋出 `ArgumentException`。

---

## 步驟 4：將 DataTable 匯入工作表 **並保留格式**

現在把所有步驟結合起來。我們使用的 `ImportDataTable` 重載接受 `Style[]` 陣列，讓我們在資料寫入工作表時 **套用儲存格樣式**。

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### 工作原理

1. **標題** – 由於我們傳入 `true`，Aspose 會在第一列寫入 “Name” 與 “Score”。  
2. **資料列** – 每一筆後續資料列皆會從 `importStyles` 取得對應的樣式。  
3. **效能** – 此方法直接將資料串流至工作表，比逐格迴圈更快。

---

## 步驟 5：驗證結果並儲存工作簿

讓我們檢視前幾個儲存格，確認樣式已套用，然後將檔案寫入磁碟。

```csharp
        // Optional: Quick sanity check – print the first row's values
        Console.WriteLine("Header Row:");
        Console.WriteLine($"{worksheet.Cells[0, 0].StringValue} | {worksheet.Cells[0, 1].StringValue}");

        // Save the workbook to an Excel file
        string outputPath = "StyledImport.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

當你開啟 **StyledImport.xlsx** 時，會看到：

- “Name” 欄位的文字為 **紅色**。  
- “Score” 欄位的文字為 **藍色**。  
- 欄位標題使用預設樣式（你也可以自行設定樣式，但那是另一篇教學）。

![套用儲存格樣式範例](https://example.com/images/apply-cell-styles.png "Aspose.Cells 中的套用儲存格樣式示例")

> **注意：** 上圖示範最終的外觀。`alt` 屬性包含主要關鍵字，以符合 SEO 要求。

---

## 常見問題與邊緣情況

### 如果我的 DataTable 欄位數多於樣式數量會怎樣？

Aspose 會將陣列中的最後一個樣式套用到所有多餘的欄位。為避免出現意外的顏色，請確保陣列長度與欄位數相同，或對不想套用樣式的欄位傳入 `null`。

### 我可以對特定列套用不同的樣式嗎？

當然可以。匯入後，你可以遍歷列，根據條件指派新的 `Style` 物件（例如，將分數 > 90 的列以綠色標示）。以下是一段簡短程式碼示例：

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++) // start at 1 to skip header
{
    int score = worksheet.Cells[i, 1].IntValue;
    if (score > 90)
    {
        Style highScore = wb.CreateStyle();
        highScore.Font.Color = Color.Green;
        worksheet.Cells[i, 1].SetStyle(highScore);
    }
}
```

### 這在大型資料集上也能運作嗎？

可以。`ImportDataTable` 能有效率地串流資料，且套用靜態樣式陣列的開銷可忽略不計。若處理數百萬列，建議分批使用 `ImportDataTable`，或搭配 `DataReader` 使用 `Cells.ImportDataTable` 以進一步降低記憶體使用量。

### 如何保留工作表中已存在的格式？

如果目標範圍已有想保留的格式，可設定 `ImportDataTable` 重載的 `importOptions` 參數（`ImportTableOptions`），並調整 `ImportDataTableOptions.PreserveCellFormatting`。預設行為會以你提供的樣式覆寫原有格式。

---

## 重點回顧：我們完成了什麼

- **在 aspose cells 匯入操作中套用儲存格樣式**。  
- 透過傳入 `Style[]` 陣列示範 **匯入並保留格式**。  
- 展示 **如何將 DataTable 匯入工作表** 並儲存結果。  
- 探討樣式數量不匹配與條件列樣式等邊緣情況。

以上全部皆在單一、獨立的主控台應用程式中完成——不需外部腳本，也不必手動操作 Excel。你現在已具備堅實基礎，可用於任何需要精緻 Excel 輸出的報表或資料匯出功能。

---

## 往後步驟

想要更進一步嗎？以下是幾個在你剛學會的基礎上延伸的想法：

- **為標題列設定樣式**（例如粗體、背景色）。  
- 使用 `Worksheet.Cells[i, j].ConditionalFormattingCollection` **套用條件格式**。  
- 使用 `wb.Save("file.pdf", SaveFormat.Pdf)` **匯出為其他格式**（如 CSV 或 PDF）。  
- **將多個 DataTable 合併** 到同一本工作簿，每個工作表使用相同的樣式方法。

如果遇到任何問題，歡迎留言或查閱 Aspose 官方文件中關於 `ImportDataTable` 的說明。祝開發順利，盡情享受這些精美樣式的 Excel 檔案吧！

---

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎延伸。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [如何使用 Aspose.Cells for .NET 將 DataTable 匯入 Excel（步驟指南）](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [如何使用 Aspose.Cells for .NET 在 Excel 中設定字型樣式（步驟指南）](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [如何使用 Aspose.Cells .NET 在 Excel 中套用文字陰影（步驟指南）](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}