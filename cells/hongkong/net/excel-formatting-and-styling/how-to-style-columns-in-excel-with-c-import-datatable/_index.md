---
category: general
date: 2026-02-21
description: 學習在使用 C# 將 DataTable 匯入 Excel 時如何設定欄位樣式。內容包括為 Excel 第二欄上色的技巧，以及使用 C#
  匯入 DataTable 至 Excel 的方法。
draft: false
keywords:
- how to style columns
- import datatable to excel
- how to import datatable
- color second column excel
- import datatable excel c#
language: zh-hant
og_description: 使用 C# 將 DataTable 匯入 Excel 時，如何設定欄位樣式。一步一步的程式碼、將 Excel 第二欄上色，以及最佳實踐。
og_title: 如何使用 C# 為 Excel 欄位設定樣式 – 完整指南
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: 使用 C# 為 Excel 欄位設定樣式 – 匯入 DataTable
url: /zh-hant/net/excel-formatting-and-styling/how-to-style-columns-in-excel-with-c-import-datatable/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# 為 Excel 欄位設定樣式 – 匯入 DataTable

有沒有想過 **如何為 Excel 工作表的欄位設定樣式**，同時直接從 `DataTable` 取得資料？你並非唯一有此疑問的人。許多開發者在需要快速加上顏色時會卡住——例如第一欄紅色、第二欄藍色——而不想在匯入後逐一手動調整每個儲存格。  

好消息是？只需要幾行 C# 程式碼，就能在資料寫入的瞬間得到完整樣式的工作表。在本教學中，我們還會涵蓋 **import datatable to excel**、示範 **color second column excel**，並說明為何此方法同時適用於 .NET Framework 與 .NET 6+ 專案。

---

## 你將學會

- 取得已填充的 `DataTable`（或即時建立）。  
- 為每個欄位定義 `Style` 物件以設定前景色。  
- 建立 Workbook、取得第一個 Worksheet，並匯入套用樣式的資料表。  
- 處理空資料表、客製化起始列、動態欄位數等邊緣情況。  

完成後，你就能將已套用樣式的 Excel 檔案直接放入任何報表流程——不需要後續處理。

> **先決條件：** 具備 C# 基本知識，並引用支援 `ImportDataTable` 的試算表函式庫（例如 Aspose.Cells、GemBox.Spreadsheet，或搭配輔助程式的 EPPlus）。以下程式碼使用 **Aspose.Cells**，因為它的 `ImportDataTable` 重載可直接接受 `Style[]`。

## 步驟 1：設定專案並加入 Excel 函式庫

在我們能設定樣式之前，需要先建立一個參考 Excel 操作函式庫的專案。

```csharp
// Install-Package Aspose.Cells -Version 24.7
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;   // For Color
```

*小技巧：* 若使用 .NET 6，可透過 `dotnet add package Aspose.Cells` 加入套件。此函式庫支援 Windows、Linux 與 macOS，讓你未來無憂。

## 步驟 2：取得或建立來源 DataTable

本教學的核心在於樣式設定，但仍需一個 `DataTable`。以下提供一個快速輔助程式來建立範例資料；在正式環境中請改為自行的 `GetTable()` 呼叫。

```csharp
/// <summary>
/// Returns a DataTable with three columns and five rows of demo data.
/// </summary>
static DataTable GetTable()
{
    var dt = new DataTable("Demo");
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));

    dt.Rows.Add(1, "Alice", 92.5);
    dt.Rows.Add(2, "Bob", 85.3);
    dt.Rows.Add(3, "Charlie", 78.9);
    dt.Rows.Add(4, "Diana", 88.1);
    dt.Rows.Add(5, "Ethan", 91.4);

    return dt;
}
```

> **為何重要：** 使用 `DataTable` 可讓資料來源保持中立——不論來自 SQL、CSV 或記憶體集合，匯入邏輯皆相同。這是 **how to import datatable** 高效運作的基礎。

## 步驟 3：定義欄位樣式（“如何為欄位設定樣式”的核心）

現在我們告訴 Worksheet 每個欄位的外觀。`Style` 類別允許設定字型、顏色、邊框等。此範例僅變更前景色。

```csharp
// Step 3: Define column styles – red for first, blue for second, default for others
Style[] columnStyles = new Style[3]; // Assuming three columns; adjust as needed

// Style for column 0 (first column) – red text
columnStyles[0] = new Style();
columnStyles[0].ForegroundColor = Color.Red;

// Style for column 1 (second column) – blue text
columnStyles[1] = new Style();
columnStyles[1].ForegroundColor = Color.Blue;

// Column 2 (third column) – keep default styling
columnStyles[2] = new Style(); // No changes, but array entry required
```

*如果有更多欄位呢？* 只要擴大陣列大小並填入需要的樣式即可。未設定樣式的欄位會自動繼承 Worksheet 的預設樣式。

## 步驟 4：建立 Workbook 並以樣式匯入 DataTable

資料與樣式準備好後，就可以把一切結合起來。

```csharp
static void Main()
{
    // Retrieve the data
    DataTable dataTable = GetTable();

    // Initialize a new workbook (in‑memory)
    Workbook workbook = new Workbook();

    // Grab the first worksheet (index 0)
    Worksheet worksheet = workbook.Worksheets[0];

    // Import the DataTable starting at cell A1 (row 0, column 0)
    // The 'true' flag tells Aspose.Cells to include column headers
    worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

    // Optional: Auto‑fit columns for a cleaner look
    worksheet.AutoFitColumns();

    // Save the result to disk
    string outputPath = "StyledDataTable.xlsx";
    workbook.Save(outputPath);

    Console.WriteLine($"Excel file saved to {outputPath}");
}
```

**剛剛發生了什麼？**  
- `ImportDataTable` 會複製列、欄，並*可選*地複製標題列。  
- 透過傳入 `columnStyles`，每個欄位會套用先前定義的 `Style`。  
- 只需一行程式碼，即可完成 **import datatable excel c#** 的操作。

## 步驟 5：驗證結果 – 預期輸出

在 Excel（或 LibreOffice）開啟 `StyledDataTable.xlsx`，你應該會看到：

| **ID** (red) | **Name** (blue) | **Score** (default) |
|--------------|-----------------|----------------------|
| 1            | Alice           | 92.5                 |
| 2            | Bob             | 85.3                 |
| …            | …               | …                    |

- 第一欄的文字顯示為 **紅色**，符合「如何為欄位設定樣式」的需求。  
- 第二欄的文字為 **藍色**，同時回應 **color second column excel** 的查詢。

若檔案能順利開啟且無錯誤，即表示你已成功掌握在樣式化欄位的同時 **how to import datatable**。

## 常見問題與邊緣情況

### 如果 DataTable 為空？

`ImportDataTable` 仍會建立標題列（若你傳入 `true`）。不會加入資料列，但樣式仍會套用於標題儲存格。

### 需要從不同的儲存格開始匯入？

調整 `ImportDataTable` 的 `rowIndex` 與 `columnIndex` 參數。例如，要從 `B2` 開始，使用 `1, 1` 取代 `0, 0`。

### 想要為列而非欄位設定樣式？

匯入後可遍歷 `worksheet.Cells.Rows`，為每列指派 `Style`。然而，欄位層級的樣式設定效能更佳，因為函式庫僅對每個欄位套用一次樣式。

### 使用 EPPlus 或 ClosedXML？

這些函式庫未提供直接接受樣式陣列的 `ImportDataTable` 重載。解決方式是先匯入資料表，然後遍歷欄位範圍並設定 `Style.Font.Color.SetColor(...)`。邏輯相同，只是多了幾行程式碼。

## 生產環境最佳實踐

- **重複使用樣式：** 為每個欄位都建立新的 `Style` 會浪費資源。可將可重用的樣式存於以顏色或字型粗細為鍵的字典中。  
- **避免硬編碼欄位數量：** 偵測 `dataTable.Columns.Count`，動態建立 `columnStyles` 陣列。  
- **執行緒安全性：** 若平行產生大量 Workbook，請為每個執行緒實例化獨立的 `Workbook`；Aspose.Cells 物件並非執行緒安全。  
- **效能考量：** 當資料表超過 10 k 列時，建議關閉 `AutoFitColumns`（會掃描每個儲存格），改手動設定欄寬。

## 完整範例（可直接複製貼上）

```csharp
// ------------------------------------------------------------
// Full example: How to style columns while importing a DataTable
// ------------------------------------------------------------
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetTable();

        // 2️⃣ Define per‑column styles
        int colCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[colCount];

        // Red for first column
        columnStyles[0] = new Style { ForegroundColor = Color.Red };

        // Blue for second column (if it exists)
        if (colCount > 1)
            columnStyles[1] = new Style { ForegroundColor = Color.Blue };

        // Default style for remaining columns
        for (int i = 2; i < colCount; i++)
            columnStyles[i] = new Style(); // no special formatting

        // 3️⃣ Create workbook and import with styles
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
        sheet.AutoFitColumns();

        // 4️⃣ Save to file
        string path = "StyledDataTable.xlsx";
        workbook.Save(path);
        Console.WriteLine($"File saved: {path}");
    }

    // Helper: sample DataTable
    static DataTable GetTable()
    {
        var dt = new DataTable("Demo");
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        dt.Rows.Add(1, "Alice", 92.5);
        dt.Rows.Add(2, "Bob", 85.3);
        dt.Rows.Add(3, "Charlie", 78.9);
        dt.Rows.Add(4, "Diana", 88.1);
        dt.Rows.Add(5, "Ethan", 91.4);
        return dt;
    }
}
```

執行程式，開啟產生的 `StyledDataTable.xlsx`，即可立即看到彩色欄位。這就是完整的 **import datatable excel c#** 工作流程。

## 結論

我們剛剛說明了在使用 C# **import datatable to excel** 時，**如何為欄位設定樣式**。只要定義 `Style[]` 陣列並傳入 `ImportDataTable`，即可將第一欄設為紅色、第二欄設為藍色，其餘保持預設——全部只需一行程式碼。

此方法具備可擴充性：可為更多欄位新增 `Style` 物件、調整起始列，或改用具有相似 API 的其他函式庫取代 Aspose.Cells。現在，你可以自動產出精美的 Excel 報表，無需手動編輯檔案。

**Next steps** you might explore:

- 使用 **條件格式** 動態突顯數值（與 “color second column excel” 相關）。  
- 從單一 `DataTable` 集合匯出多個工作表（適合月度儀表板）。  
- 結合 **CSV → DataTable** 轉換，構建端對端的……

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}