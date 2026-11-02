---
category: general
date: 2026-03-22
description: 如何匯出帶格式的 Excel 並保留數字格式。學習轉換 Excel 範圍、取得公式結果，以及使用 Aspose.Cells 匯出帶格式的
  Excel。
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: zh-hant
og_description: 如何匯出帶格式的 Excel 並保留數字格式。逐步指南：轉換 Excel 範圍、取得公式結果，並在 C# 中匯出帶格式的 Excel。
og_title: 如何匯出帶格式的 Excel – 保留數字格式
tags:
- C#
- Aspose.Cells
- Excel automation
title: 如何匯出帶格式的 Excel — 保留數字格式
url: /zh-hant/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何匯出 Excel 並保留格式 – 保持數字格式

有沒有想過 **如何匯出 Excel** 資料，同時讓每個儲存格的外觀完全如同在工作簿中看到的樣子？也許你需要把報告寄給客戶、填充資料格控制項，或只是把值存入資料庫。最常見的痛點是數字格式會遺失，或公式會變成純文字。

在本教學中，我們將一步步示範完整、可直接執行的 C# 範例，該範例 **保留數字格式**、**將 Excel 範圍轉換為 `DataTable`**、**取得公式結果**，最後使用 Aspose.Cells **匯出 Excel 並保留格式**。完成後，你將擁有一個可直接放入任何專案、以工作表參考呼叫的單一方法。

> **快速預覽：** 程式會建立一個活頁簿，寫入數值與公式，指示 Aspose.Cells 以格式化字串匯出儲存格，並印出 `123.456 | 246.912` ─ 正是 Excel 中會看到的結果。

---

## 需要的環境

- **Aspose.Cells for .NET**（免費試用版已足夠學習使用）
- .NET 6.0 或更新版本（在 .NET Framework 上 API 也相同）
- 基本的 C# 開發環境（Visual Studio、VS Code、Rider…自行選擇）

不需要除 Aspose.Cells 之外的其他 NuGet 套件。若尚未安裝，請執行：

```bash
dotnet add package Aspose.Cells
```

---

## Step 1 – 建立活頁簿並寫入值（含公式）

首先建立一個全新的活頁簿，並在 **A1** 放入數值。接著在 **B1** 加入一個簡單公式，將第一格的值乘以二。這為稍後示範 **取得公式結果** 做好鋪陳。

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**為什麼這很重要：**  
- `PutValue` 只儲存原始數字，而 `PutFormula` 則儲存計算式。  
- Aspose.Cells 會讓公式保持 **活躍**，因此稍後取得儲存格值時會得到 `246.912`，而不是字串 `"=A1*2"`。

---

## Step 2 – 告訴 Aspose.Cells 以格式化字串匯出值

如果直接使用預設設定呼叫 `ExportDataTable`，數值儲存格會以底層的 `double` 回傳，千分位、貨幣符號或自訂小數位等格式都會被去除。`ExportTableOptions` 類別讓我們 **保留數字格式** 並 **以字串匯出**。

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**重點說明：** `ExportNumberFormat = true` 是讓 **保留數字格式** 生效的旗標。若未設定此旗標，會看到 `"123.456"` 與 `"246.912"` 這樣的原始數字，雖然在程式碼中看起來沒問題，但貼到需要與 Excel 相同格式的 UI 時就會出問題。

---

## Step 3 – 列印匯出的資料（驗證）

現在我們已取得一個包含格式化字串的 `DataTable`，把內容輸出到主控台。這同時也證明我們成功 **取得公式結果**，而不需要自行計算公式。

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

執行程式會印出：

```
123.456 | 246.912
```

請注意第二欄顯示的是 **公式結果**，而非公式文字。這正是 **匯出 Excel 並保留格式** 時，下游處理所需要的行為。

---

## Step 4 – 轉換較大範圍的 Excel（可選）

上述範例只處理 `A1:B1` 這個小區塊，但實務上常需要匯出整張表格。相同的方法適用於任何矩形區域，只要調整 `firstRow`、`firstColumn`、`totalRows` 與 `totalColumns` 參數即可。

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**小技巧：** 若工作表已經有標題列，請將 `includeColumnNames` 設為 `true`。Aspose.Cells 會把範圍的第一列當作欄位名稱，對於之後將 `DataTable` 綁定至 UI 資料格非常方便。

---

## Step 5 – 常見陷阱與避免方式

| 問題 | 為什麼會發生 | 解決方式 |
|------|--------------|----------|
| **數字失去逗號或貨幣符號** | `ExportAsString` 為 `false` 或未設定 `ExportNumberFormat` | 同時設定 `ExportAsString = true` **以及** `ExportNumberFormat = true`。 |
| **公式儲存格回傳公式文字** | 匯出前未呼叫 `CalculateFormula`（僅在活頁簿未自動計算時需要） | 開啟自動計算 (`workbook.CalculateFormula()`) 或使用 `ExportAsString` 強制評估。 |
| **標題列被當成資料列** | `includeColumnNames` 為 `false`，但範圍內包含標題列 | 設定 `includeColumnNames = true`，將第一列視為欄位名稱。 |
| **大型範圍導致記憶體壓力** | 一次匯出整張工作表會一次載入全部資料到記憶體 | 分批匯出（例如每次 500 列），必要時再合併 `DataTable`。 |

---

## Step 6 – 完整可執行範例（直接複製貼上）

以下是完整程式碼，從 `using` 陳述式到 `Main` 方法。貼到 Console 應用程式後按 **F5**，即可立即看到格式化的輸出。

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**預期輸出**

```
123.456 | 246.912

Press any key to exit...
```

以上即為 **如何匯出 Excel** 的完整流程，保留格式、評估公式結果，並產生可供任何 .NET 消費者使用的乾淨 `DataTable`。

---

## 結論

我們已說明如何 **匯出 Excel** 資料，同時 **保留數字格式**、**將 Excel 範圍轉換為 `DataTable`**，以及 **取得公式結果** 而不需額外解析。關鍵在於 `ExportTableOptions` 的設定 ─ 只要把 `ExportAsString` 與 `ExportNumberFormat` 設為 `true`，Aspose.Cells 就會幫你完成繁重的工作。

接下來你可以：

- 把 `DataTable` 接到 WPF `DataGrid` 或 ASP.NET MVC 視圖。
- 將表格寫入 CSV 檔，同時保留完全相同的視覺呈現。
- 將此方法延伸至多個工作表或動態範圍。

歡迎自行嘗試不同的格式（貨幣、百分比）與更大的資料區塊。若遇到任何異常，請回顧 **常見陷阱** 表格 ─ 它涵蓋了在 **匯出 Excel 並保留格式** 時最常見的問題。

祝程式開發順利，願你的匯出試算表永遠保持與原始檔案同樣的精緻度！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}