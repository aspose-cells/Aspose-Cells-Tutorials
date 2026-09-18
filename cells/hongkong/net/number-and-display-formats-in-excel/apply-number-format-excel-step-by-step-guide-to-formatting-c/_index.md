---
category: general
date: 2026-02-26
description: 快速套用 Excel 數字格式，學習如何將欄位設定為貨幣、設定欄位數字格式，以及設定欄位字體顏色，只需幾行 C# 程式碼。
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: zh-hant
og_description: 在 C# 中輕鬆套用 Excel 數字格式。學習將欄位格式化為貨幣、設定欄位數字格式，以及設定欄位字體顏色，打造專業試算表。
og_title: 在 Excel 中套用數字格式 – 完整的欄位樣式指南
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: 在 Excel 中套用數字格式 – 格式化欄位的逐步指南
url: /zh-hant/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# apply number format excel – 如何在 C# 中設定 Excel 欄位樣式

有沒有想過在 **apply number format excel** 的同時，還要在迴圈處理 `DataTable` 時同時設定藍色字體的標題 *以及* 貨幣格式的欄位？你並不是唯一遇到這個問題的人。大多數開發者在需要同時完成藍字標題與貨幣欄位的匯入作業時，都會卡住。好消息是，只要寫幾行 C# 程式碼並使用正確的樣式物件，就能在匯入時一次完成，無需事後再處理工作表。

在本教學中，我們將一步步示範完整、可執行的範例，說明如何 **format column as currency**、**set column number format** 於其他欄位，甚至 **set column font color** 給標題。完成後，你將擁有一套可重複使用的模式，直接套用於任何 Aspose.Cells（或類似）專案。

## 你將學到

- 如何取得 `DataTable`，並將每一欄對應到特定的 `Style`。
- 使用 `Worksheet.Cells.ImportDataTable` **apply number format excel** 的完整步驟。
- 為什麼事先建立樣式比逐格設定更有效率。
- 當來源表格欄位多於已設定樣式時的例外處理方式。
- 完整、可直接複製貼上的程式碼範例，讓你今天就能執行。

> **先備條件：** 本指南假設你的專案已參考 Aspose.Cells for .NET（或任何提供 `Workbook`、`Worksheet`、`Style` API 的函式庫）。若使用其他函式庫，概念相同，只要替換型別名稱即可。

---

## 步驟 1：將來源資料取得為 DataTable

在進行任何樣式設定之前，必須先取得原始資料。實務上資料通常來自資料庫、CSV 或 API。為了說明，我們先模擬一個簡單的 `DataTable`，包含兩個欄位：*Product*（字串）與 *Price*（十進位）。

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;

public static DataTable GetData()
{
    var dt = new DataTable();
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Price", typeof(decimal));

    dt.Rows.Add("Apple", 1.25m);
    dt.Rows.Add("Banana", 0.75m);
    dt.Rows.Add("Cherry", 2.10m);

    return dt;
}
```

> **為什麼這很重要：** 把資料拉進 `DataTable` 後，就得到一個可直接供 `ImportDataTable` 使用的記憶體表格，省去逐格手動寫入的繁瑣。

## 步驟 2：建立樣式陣列 – 每個欄位一個

我們將使用的 `ImportDataTable` 重載接受一個 `Style` 陣列。陣列中的每個元素對應到欄位索引。若將某個元素保留為 `null`，該欄位會使用工作簿的預設樣式。

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

> **小技巧：** 在取得 `DataTable` 後才宣告陣列，可確保大小正好匹配，避免之後拋出 `IndexOutOfRangeException`。

## 步驟 3：為第一欄設定藍色字體

常見需求是將標題或關鍵欄位以不同字體顏色突顯。這裡我們把第一欄的文字設為藍色。

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

> **為什麼要使用樣式物件？** 樣式是可重複使用的，且一次套用於整欄，遠比匯入後逐格遍歷快得多。工作簿會先快取樣式，之後每個儲存格都直接引用。

## 步驟 4：將第二欄格式化為貨幣

Excel 內建的數字格式以索引編號表示。`14` 代表預設的貨幣格式（例如 `$1,234.00`）。若需要自訂格式，也可以直接指定格式字串。

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

> **例外情況：** 若工作簿使用的語系其貨幣符號不是 `$`，相同的索引會自動套用當地符號（例如德國語系會顯示 `€`）。

## 步驟 5：使用已定義的樣式匯入 DataTable

現在把所有步驟整合起來。`ImportDataTable` 會從儲存格 `A1`（第 0 列、第 0 欄）開始貼上資料，並套用先前準備好的樣式。

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- 第二個參數 `true` 告訴 Aspose.Cells 將 `DataTable` 的第一列視為欄位標題。
- `0, 0` 座標指定匯入的左上角起點。
- `columnStyles` 把每個欄位對應到各自的樣式。

## 步驟 6：儲存活頁簿（可選，但方便驗證）

如果想要在 Excel 中檢視結果，只要把活頁簿寫入磁碟即可。此步驟對樣式邏輯不是必須的，但有助於除錯。

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### 預期輸出

| **Product** (藍色字體) | **Price** (貨幣格式) |
|------------------------|----------------------|
| 蘋果                    | $1.25                |
| 香蕉                    | $0.75                |
| 櫻桃                    | $2.10                |

- *Product* 欄位以藍色顯示，突顯出來。
- *Price* 欄位則以預設貨幣符號與兩位小數呈現。

---

## 常見問題與變形

### 如何 **set column number format** 超過兩個欄位？

只要擴充 `columnStyles` 陣列即可。例如，想在第三欄顯示百分比：

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### 若需要自訂貨幣格式，例如 “USD 1,234.00” 該怎麼做？

把 `Number` 屬性改成格式字串：

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### 能否在數值欄位同時 **set column font color** 而不影響其數字格式？

絕對可以。樣式是可組合的，你可以在同一個 `Style` 例項上同時設定 `Font.Color` 與 `Number`：

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### 若 `DataTable` 的欄位數多於樣式陣列，會發生什麼事？

任何未明確指定樣式（`null`）的欄位，都會繼承工作簿的預設樣式。為避免不小心出現 `null`，可以先用基礎樣式初始化整個陣列：

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

然後只覆寫你在意的欄位。

### 這種做法在大型資料集（10k+ 列）下有效嗎？

有效。因為樣式在匯入前就已一次套用於每個欄位，整體運算仍為 O(N)（N 為列數），且記憶體使用保持低。避免在匯入後逐格迴圈，否則效能會急速下降。

---

## 完整可執行範例（直接複製貼上）

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelStyler
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Prepare style array (one per column)
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 4️⃣ Style first column – blue font
        columnStyles[0] = workbook.CreateStyle();
        columnStyles[0].Font.Color = Color.Blue;

        // 5️⃣ Style second column – built‑in currency format (ID 14)
        columnStyles[1] = workbook.CreateStyle();
        columnStyles[1].Number = 14;

        // 6️⃣ (Optional) Add more styles here – e.g., percentage, custom formats

        // 7️⃣ Import the DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 8️⃣ Save to file for verification
        workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created: StyledReport.xlsx");
    }

    // Helper method to mock data
    public static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Price", typeof(decimal));

        dt.Rows.Add("Apple", 1.25m);
        dt.Rows.Add("Banana", 0.75m);
        dt.Rows.Add("Cherry", 2.10m);
        return dt;
    }
}
```

執行程式後，開啟 `StyledReport.xlsx`，即可立即看到 **apply number format excel** 的結果。

---

## 結論

我們示範了一種簡潔且高效的方式，將 **apply number format excel** 套用於匯入的 `DataTable`。透過事先建立 `Style[]` 陣列，你可以在一次呼叫中 **format column as currency**、**set column number format**，以及 **set column font color**，不必再進行後處理。

歡迎自行擴充此模式：加入條件樣式、合併儲存格作為標題，或是注入公式。相同的原則可讓程式碼保持整潔，試算表也更具專業感。

---

### 接下來可以做什麼？

- 探索 **conditional formatting**，為超過門檻的數值加上醒目標示。
- 結合此技巧與 **pivot table generation**，打造動態報表。
- 嘗試為日期、百分比或自訂科學記號 **set column number format**。

有什麼新想法或實作心得嗎？歡迎在留言區分享，一起持續進步。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}