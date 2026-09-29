---
category: general
date: 2026-03-30
description: 使用 C# 建立具貨幣格式的 Excel 工作簿。學習如何匯入 DataTable、在 Excel 中新增數字格式，並在幾分鐘內為欄位套用貨幣格式。
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: zh-hant
og_description: 使用 C# 建立 Excel 活頁簿，並即時將儲存格格式化為貨幣。本步驟教學示範如何將 DataTable 匯入 Excel 以及為欄位新增數字格式。
og_title: 使用 C# 建立 Excel 工作簿 – 貨幣格式設定指南
tags:
- Aspose.Cells
- C#
- Excel automation
title: 建立 Excel 工作簿 C# – 套用貨幣格式並匯入 DataTable
url: /zh-hant/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 Excel 工作簿 C# – 套用貨幣格式並匯入 DataTable

有沒有需要 **create Excel workbook C#**，但希望一開始就像完成的報表一樣？也許你正從資料庫撈取銷售數字，想讓價格欄位直接顯示美元符號，而不必手動在 Excel 裡調整。聽起來很熟悉吧？其實大多數開發者在第一次自動化 Excel 匯出時，都會遇到這個問題。

在本教學中，我們將一步步示範完整、可直接執行的解決方案，**建立 Excel 工作簿 C#**、匯入 `DataTable`，並 **將 Price 欄位格式化為貨幣**。完成後，你會得到一個名為 `StyledTable.xlsx` 的檔案，打開後即可看到已套用格式的數字，無需額外後處理。

> **你將學會**
> - 如何在 .NET 專案中設定 Aspose.Cells  
> - 如何 **import datatable to excel** 並使用樣式陣列  
> - 如何 **add number format excel** 為特定欄位設定格式  
> - 處理更多欄位或不同語系的技巧  

> **先備條件**  
> - 已安裝 .NET 6+（或 .NET Framework 4.6+）  
> - Aspose.Cells for .NET NuGet 套件（`Install-Package Aspose.Cells`）  
> - 具備基本的 C# 與 DataTable 應用知識  

---

## Step 1: Prepare the DataTable (import datatable to excel)

首先，我們需要一些範例資料。實際專案中通常會從資料庫查詢填入，但這裡使用硬編碼的方式讓示例更簡潔。

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*為什麼這很重要*：`DataTable` 是業務資料與 Excel 檔案之間的橋樑。Aspose.Cells 能直接匯入它，保留欄位名稱與資料型別。

---

## Step 2: Spin Up a New Workbook (create excel workbook c#)

接著建立實際的 Excel 檔案物件。把它想成你即將繪製的空白畫布。

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **專業小技巧**：若需要多個工作表，只要呼叫 `workbook.Worksheets.Add()` 並為每張工作表命名即可。

---

## Step 3: Define a Currency Style (format cells currency)

Aspose.Cells 允許你建立 `Style` 物件，定義儲存格的外觀。貨幣格式使用內建的數字格式 ID 164（`"$#,##0.00"`）。

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*為什麼不直接設定格式字串？* 使用內建 ID 可確保在不同 Excel 版本間的相容性，並避免語系特有的怪異行為。

---

## Step 4: Build the Style Array (apply currency format column)

匯入 `DataTable` 時，你可以傳入 `Style` 陣列——每個欄位對應一個樣式。`null` 代表「使用預設樣式」。此處我們只把 `priceStyle` 套用到第二欄。

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

若之後新增欄位，只要相應擴充陣列即可。`columnStyles` 的長度必須與匯入的欄位數相同，否則 Aspose 會拋出例外。

---

## Step 5: Import the DataTable with Styles (import datatable to excel)

現在魔法發生了——`DataTable` 會被寫入工作表，且價格欄位立即以貨幣格式顯示。

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*如果有超過兩個欄位怎麼辦？* 只要擴充 `columnStyles`，讓每個欄位都有適當的樣式（或 `null` 使用預設），這是最乾淨的 **add number format excel** 實作方式。

---

## Step 6: Save the Workbook (create excel workbook c#)

最後，將檔案寫入磁碟。選擇任意你有寫入權限的資料夾。

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

開啟 `StyledTable.xlsx`，你應該會看到：

| 產品   | 價格   |
|--------|--------|
| 蘋果   | $1.23 |
| 香蕉   | $0.78 |
| 櫻桃   | $2.50 |

**Price**（價格）欄位已自動套用貨幣格式——不需要額外步驟。

---

## Edge Cases & Variations

### More Columns, Different Formats

如果需要 **format cells currency** 給多個欄位（例如 Cost、Tax、Total），只要為每個欄位建立獨立的 `Style`，再填入 `columnStyles`：

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Locale‑Specific Currency

若要顯示歐元或英鎊，可使用不同的內建 ID（例如 165 代表 `€#,##0.00`）。或者自行設定自訂格式字串：

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Large Data Sets

Aspose.Cells 能處理上百萬列資料，但樣式物件會佔用記憶體。對所有貨幣欄位重複使用同一個 `Style` 實例，可降低記憶體使用量。

### Missing Styles

如果 `columnStyles` 的長度小於欄位數，Aspose 會對剩餘欄位套用預設樣式。這在只關心少數欄位時非常方便。

---

## Full Working Example (All Steps Combined)

以下是完整程式碼，可直接貼到 Console App 中執行。程式碼已包含前面討論的所有步驟與說明註解。

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**預期結果**：開啟 `StyledTable.xlsx` 時，`Price`（價格）欄位會顯示美元符號與兩位小數，正如 **format cells currency** 的需求所示。

---

## Frequently Asked Questions

**Q: 這能在 .NET Core 上使用嗎？**  
A: 完全可以。Aspose.Cells 符合 .NET standard，支援 .NET 5、.NET 6 以及更新的版本，無需額外修改。

**Q: 我的 DataTable 有 10 個欄位，但只想格式化第 5 欄，該怎麼做？**  
A: 建立長度為 10 的 `Style[]`，將索引 0‑4 與 6‑9 設為 `null`，在索引 4（第 5 欄，零基）放入自訂樣式即可。Aspose 會依照每個陣列項目套用樣式。

**Q: 可以隱藏標題列嗎？**  
A: 匯入後，可設定 `worksheet.Cells.Rows[0].Hidden = true;`，或在 `ImportDataTable` 時將 `includeColumnNames` 參數設為 `false`。

---

## Conclusion

我們已成功 **create Excel workbook C#**、匯入 `DataTable`，並使用 Aspose.Cells **apply a currency format column**。從資料準備、樣式定義、樣式陣列建立、以 `ImportDataTable` 匯入、最後儲存，這幾個核心步驟涵蓋了大多數 Excel 自動化需求。

接下來你可以探索：

- 為日期或百分比 **add number format excel**  
- 在同一檔案中匯出多張工作表  
- 使用 **format cells currency** 搭配不同語系符號  
- 依相同資料自動產生圖表  

不妨試試看，讓自己成為團隊中 Excel 報表的關鍵人物。有任何新想法或技巧想分享嗎？歡迎在下方留言——祝開發順利！

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}