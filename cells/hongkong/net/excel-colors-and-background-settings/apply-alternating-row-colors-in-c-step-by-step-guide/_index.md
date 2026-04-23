---
category: general
date: 2026-03-18
description: 學習如何在工作表中使用 C# 套用交錯列顏色。包括設定列背景顏色、加入淡黃色背景，以及交錯著色列。
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: zh-hant
og_description: 在 C# 中套用交替列色以提升可讀性。本指南示範如何設定列的背景色、加入淡黃色背景，以及交替為列著色。
og_title: 在 C# 中套用交替列顏色 – 完整教學
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: 在 C# 中套用交錯列顏色 – 步驟指南
url: /zh-hant/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中套用交錯列顏色 – 完整教學

是否曾需要 **apply alternating row colors** 於資料驅動的工作表，但不知從何下手？你並非唯一遇到這個問題的人——大多數開發者在首次想讓表格看起來更友善時，都會卡在這裡。好消息是，只要幾行 C# 程式碼，你就可以 **set row background color**，再加上一層 **add light yellow background**，即可得到即時提升可讀性的精緻格線。

在本教學中，我們將一步步說明完整流程，從將 `DataTable` 讀入記憶體，到為每一列套用淡黃‑白條紋。完成後，你將能自信地 **color rows alternately**，同時也會看到幾種在需要不同色調或動態主題時的實用變化。

## 您需要的條件

在開始之前，請確保您已具備以下項目：

- 一個目標為 .NET 6 或以上的 .NET 專案（此程式碼亦可在 .NET Framework 4.7+ 上執行）。  
- 一個支援樣式物件的試算表函式庫——範例使用的通用 `Workbook`/`Worksheet` API 與 **Aspose.Cells**、**GemBox.Spreadsheet** 或 **ClosedXML** 等函式庫相似。  
- 一個 `DataTable` 資源——可以是資料庫查詢、CSV 匯入，或任何記憶體集合。  

不需要額外的 NuGet 套件，除非你使用的試算表函式庫本身。若使用 Aspose.Cells，命名空間為 `Aspose.Cells`；若使用 ClosedXML，則為 `ClosedXML.Excel`。請依需求自行調整 `CreateStyle` 與 `ImportDataTable` 的呼叫方式。

## Step 1: Retrieve the Source Data as a DataTable

首先，取得要顯示的資料。實務上通常是從資料庫撈取，但為了說明，我們會以一個名為 `GetData()` 的輔助方法模擬，回傳已填充的 `DataTable`。

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Why this matters:** `DataTable` 定義了之後會套用交錯陰影的列與欄。若表格為空，則無法套用樣式，因此在繼續之前務必確認 `Rows.Count` > 0。

### 專業提示
若你是從 Entity Framework 取得資料，可在執行 `SqlCommand` 後使用 `DataTable.Load(reader)`。這樣可以保持程式碼整潔，避免手動定義欄位。

## Step 2: Allocate an Array to Hold a Style for Each Row

接著，我們需要一個與列數相同的容器。大多數試算表 API 允許將樣式陣列傳入匯入方法，因此我們會建立一個大小正好等於列數的 `Style[]`。

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Explanation:** 透過預先配置陣列，我們避免在每次迭代時重新建立樣式物件，這在處理上千列資料時可提升效能。

## Step 3: Apply Alternating Row Colors (Light Yellow / White)

現在進入核心：**apply alternating row colors**。我們會遍歷每一列，從 workbook 建立全新的樣式實例，並依據列索引設定背景色。偶數列使用淡黃色填充，奇數列則保持白色。

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### 為什麼這樣可行
- **`rowIndex % 2 == 0`** 用來檢查該列是否為偶數。  
- **`Color.LightYellow`** 提供柔和且不突兀的色調，非常適合資料表。  
- **`BackgroundType.Solid`** 確保填色覆蓋整個儲存格，達成 **set row background color** 的效果。  

你可以將 `Color.LightYellow` 換成其他色彩（例如 `Color.LightCyan`），若想要不同的外觀亦可。相同的邏輯也能讓你 **color rows alternately**，依據其他條件（如狀態旗標）來變換顏色。

## Step 4: Import the DataTable into the Worksheet with the Prepared Styles

最後，我們將所有資料寫入工作表。大多數函式庫提供接受樣式陣列的 `ImportDataTable` 重載。`true` 參數表示寫入欄位標題，`0, 0` 座標則從左上角儲存格開始。

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Result:** 工作表現在會以乾淨的 **alternating row shading** 方式呈現資料——偶數列為淡黃色，奇數列為白色。使用者可以更順暢地掃描表格，眼睛不會來回跳動。

### 預期輸出
若開啟產生的試算表，會看到類似以下的結果：

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

第 1、3、5… 列具有 **light yellow background**，而第 2、4、6… 列則保持 **white**。標題列（第 0 列）會使用預設樣式，除非另行自訂。

## Optional Variations & Edge Cases

### 1. 使用不同的色彩調色盤
如果淡黃色與品牌形象衝突，只需將 `Color.LightYellow` 替換為其他 `System.Drawing.Color`。例如想要藍灰主題，可使用：

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. 依資料動態陰影
有時需要突顯符合條件的列（例如庫存過低）。只要將取模檢查與自訂測試結合即可：

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. 僅對特定欄位套用樣式
若只想在特定欄位上使用 **set row background color**，可為每個欄位建立獨立樣式，並在匯入後透過工作表的儲存格範圍 API 指派。

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. 大型表格的效能提示
當處理超過 10,000 列時，建議為每種顏色僅重複使用單一樣式物件，而非每列都新建。陣列只需保存兩個共享樣式的參考，能大幅降低記憶體使用量。

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## Full Working Example

以下是一個可直接貼到 Console 應用程式的完整範例。它使用虛構的 `Workbook`/`Worksheet` API；請自行替換為你所使用函式庫的類型。

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Output:** 產生名為 `AlternatingRows.xlsx` 的檔案，裡面的每一列會在淡黃色與白色之間交替，讓表格更易於閱讀。

## Frequently Asked Questions

**Q: 此做法能否與 Excel 風格的條件格式化一起使用？**  
A: 能。若你的函式庫支援條件規則，你可以將相同的邏輯轉換為檢查 `MOD(ROW(),2)=0` 的規則。此程式碼方式在缺乏內建條件格式化的函式庫中更具可移植性。

**Q: 若要在 PDF 表格而非 Excel 工作表中 **color rows alternately**，該怎麼做？**  
A: 大多數 PDF 表格產生器（例如 iTextSharp、PdfSharp）都允許為每列設定 `BackgroundColor`。只要套用相同的取模計算即可—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}