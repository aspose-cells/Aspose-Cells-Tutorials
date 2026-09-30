---
category: general
date: 2026-02-15
description: 使用 C# 建立工作簿，將 DataTable 匯出至 Excel，設定列格式與列背景，並可在數分鐘內自動化 Excel 任務。
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: zh-hant
og_description: 快速使用 C# 建立工作簿、套用列樣式，並自動化 Excel 匯出，提供完整程式碼範例與最佳實踐技巧。
og_title: 建立工作簿 C# – 將 DataTable 匯出至 Excel 並套用格式
tags:
- C#
- Excel
- DataExport
title: 建立工作簿 C# – 匯出 DataTable 至 Excel 並套用格式
url: /zh-hant/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立工作簿 C# – 匯出 DataTable 至 Excel 並套用格式

有沒有曾經需要 **create workbook C#** 並將 `DataTable` 匯入 Excel 並套用自訂樣式？你並不孤單。在許多行業應用程式中，需求是輸出一份格式美觀的試算表，讓非技術使用者能立即開啟並理解。  

在本教學中，我們將一步步示範完整、可直接執行的解決方案，說明 **how to create workbook C#**、套用 **excel export formatting**、設定 **row background**，以及運用 **excel automation c#** 產出精緻檔案。沒有模糊的「請參考文件」捷徑——只有完整程式碼、每行程式碼的重要說明，以及你明天就能用上的小技巧。

---

## 前置條件

- .NET 6（或 .NET Framework 4.6 以上）。  
- Visual Studio 2022 或任何相容 C# 的 IDE。  
- **Aspose.Cells for .NET** NuGet 套件（或任何提供 `Workbook`、`Worksheet`、`Style` 的函式庫）。  
- 基本的 `DataTable` 使用經驗。  

如果尚未安裝 Aspose.Cells，請執行：

```bash
dotnet add package Aspose.Cells
```

**小技巧：** 免費試用版可滿足大多數開發情境；只要在正式發佈前記得替換授權金鑰即可。

---

![建立工作簿 C# 範例，顯示在 Excel 中已套用樣式的列]( "建立工作簿 C# 範例，含列背景顏色")

---

## 步驟 1：初始化 Workbook 與 Worksheet（Create Workbook C#）

第一件事就是建立一個 `Workbook` 實例。把它想像成在記憶體中開啟一個全新的 Excel 檔案。

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // Create a new workbook – this is the core of create workbook C#
        var workbook = new Workbook();

        // Grab the first worksheet (index 0) – it's already there by default
        var worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this worksheet with data and styling
        ExportDataTableWithStyling(workbook, worksheet);
    }
}
```

**為什麼要這樣做？**  
`Workbook` 包含整個 Excel 文件，而 `Worksheet` 代表單一工作表。從乾淨的 workbook 開始，可確保你能掌控輸出的每個細節——不會有隱藏的預設樣式偷偷跑進來。

---

## 步驟 2：準備範例 DataTable（Export DataTable Excel）

在實際專案中你會從資料庫撈資料，但為了說明，我們直接在程式中建立一個小型 `DataTable`。

```csharp
private static DataTable GetSampleData()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Id", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
    dt.Rows.Add(2, "Bob Smith", "IT", 68000);
    dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
    dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);

    return dt;
}
```

**此步驟的重要性：**  
將 `DataTable` 匯出至 Excel 是最常見的表格資料傳遞方式。上述方法是完整自足的，你可以直接 copy‑paste 到任何專案中使用。

---

## 步驟 3：為每列建立 Style（Excel Export Formatting）

為了讓每列都有自己的背景色，我們會為 `DataTable` 中的每一列產生一個 `Style` 物件。這正是 **excel export formatting** 發揮威力的地方。

```csharp
private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
{
    var styles = new Style[rowCount];

    // Define a palette of background colors – feel free to extend
    var colors = new[] { System.Drawing.Color.LightYellow,
                         System.Drawing.Color.LightCyan,
                         System.Drawing.Color.LightGreen,
                         System.Drawing.Color.LightPink };

    for (int i = 0; i < rowCount; i++)
    {
        // Create a fresh style instance
        var style = workbook.CreateStyle();

        // Cycle through our color array so rows get alternating shades
        style.ForegroundColor = colors[i % colors.Length];
        style.Pattern = BackgroundType.Solid;

        // Optional: make the font a little bolder for readability
        style.Font.IsBold = true;

        styles[i] = style;
    }

    return styles;
}
```

**為什麼要逐列設定樣式？**  
如果需要突顯特定記錄（例如逾期發票），只要把簡單的顏色循環換成條件判斷——根據列資料設定 `style.ForegroundColor` 即可。

---

## 步驟 4：匯入 DataTable 並套用列樣式（Set Row Background）

現在把資料、工作簿與樣式全部結合起來。

```csharp
private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
{
    // 1️⃣ Get the data
    DataTable dt = GetSampleData();

    // 2️⃣ Build a style for each row
    Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

    // 3️⃣ Import the DataTable starting at cell A1.
    //    The `true` flag tells Aspose.Cells to include column headers.
    worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

    // 4️⃣ Save the workbook to disk
    string outputPath = "EmployeesReport.xlsx";
    workbook.Save(outputPath);
    Console.WriteLine($"Workbook saved to {outputPath}");
}
```

**執行結果會是什麼樣子：**  
開啟 `EmployeesReport.xlsx` 後，第一列（標題）使用預設格式，接下來的四筆資料列各自帶有淡色背景。最終呈現的報表看起來像是手工製作，而非單純的資料傾印。

---

## 步驟 5：進階 Excel Automation C# 小技巧（Excel Automation C#）

以下列出幾個可以在基本範例上再加強的快速技巧：

| 小技巧 | 程式碼片段 | 使用時機 |
|-----|--------------|-------------|
| **自動調整欄寬** | `worksheet.AutoFitColumns();` | 匯入資料後避免文字被截斷。 |
| **凍結標題列** | `worksheet.WindowPane.SplitRows = 1;` | 表格可能會超出螢幕捲動時。 |
| **條件格式化** | <details><summary>顯示</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | 高亮顯示超過門檻的薪資。 |
| **保護工作表** | `worksheet.Protect(ProtectionType.All, "myPassword");` | 需要唯讀報表時。 |

這些片段展示了 **excel automation c#** 的廣度——你可以在不重寫核心匯入邏輯的前提下，持續擴充工作簿功能。

---

## 常見問題與邊緣案例

**如果 DataTable 有上千筆資料會怎樣？**  
Aspose.Cells 會有效率地串流資料，但為了節省記憶體，建議不要為每一列都建立樣式。可以改為對整個範圍套用單一樣式：

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**可以匯出成 .csv 而不是 .xlsx 嗎？**  
可以，只要更改儲存格式：

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

樣式會遺失（CSV 不支援樣式），但資料匯出仍然相同。

**這個方式能在 .NET Core 上執行嗎？**  
能。Aspose.Cells 支援 .NET Standard 2.0 以上，所以相同程式碼可在 .NET 6、.NET 7 或 .NET Framework 上執行。

---

## 完整可執行範例（Copy‑Paste Ready）

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – core of create workbook C#
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // 2️⃣ Export DataTable with styling
        ExportDataTableWithStyling(workbook, worksheet);
    }

    private static DataTable GetSampleData()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
        dt.Rows.Add(2, "Bob Smith", "IT", 68000);
        dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
        dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);
        return dt;
    }

    private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
    {
        var styles = new Style[rowCount];
        var colors = new[]
        {
            System.Drawing.Color.LightYellow,
            System.Drawing.Color.LightCyan,
            System.Drawing.Color.LightGreen,
            System.Drawing.Color.LightPink
        };

        for (int i = 0; i < rowCount; i++)
        {
            var style = workbook.CreateStyle();
            style.ForegroundColor = colors[i % colors.Length];
            style.Pattern = BackgroundType.Solid;
            style.Font.IsBold = true;
            styles[i] = style;
        }

        return styles;
    }

    private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
    {
        DataTable dt = GetSampleData();
        Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

        // Import with row styles – sets row background (set row background)
        worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

        // Optional polish
        worksheet.AutoFitColumns();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}