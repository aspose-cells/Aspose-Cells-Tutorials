---
category: general
date: 2026-03-27
description: 如何在 C# 中使用 Aspose.Cells 建立樞紐分析表 – 學習新增資料、啟用重新整理，並在同一教學中將工作簿儲存為 xlsx。
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: zh-hant
og_description: 如何在 C# 中使用 Aspose.Cells 建立樞紐分析表。本指南將示範如何新增資料、啟用重新整理，並將工作簿儲存為 xlsx。
og_title: 如何在 C# 中建立樞紐分析表 – 完整的 Aspose.Cells 教學
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何在 C# 中建立樞紐分析表 – 使用 Aspose.Cells 的完整指南
url: /zh-hant/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中建立樞紐分析表 – 完整 Aspose.Cells 教學

有沒有想過 **如何在 C# 中建立樞紐分析表**，卻不想與 COM interop 纏鬥？你並不是唯一有此疑問的人。在許多資料驅動的應用程式中，我們需要快速將原始銷售數據轉換成整潔的彙總，而 Aspose.Cells 讓這變得輕而易舉。  

在本教學中，我們將逐步說明：加入資料、建立樞紐分析表、啟用自動重新整理，最後 **save workbook as xlsx**，讓使用者能立即在 Excel 開啟。完成後，你將擁有一個可直接使用的 `PivotRefresh.xlsx` 檔案，並深入了解每一行程式碼的意義。

## 前置條件

- .NET 6+（或 .NET Framework 4.7.2 以上）– 任何較新的執行環境皆可。  
- Aspose.Cells for .NET – 可從 NuGet 取得 (`Install-Package Aspose.Cells`)。  
- 具備基本的 C# 語法概念 – 不需要深入的 Excel 知識。  

> **專業提示：** 若你使用公司電腦，請確保已套用 Aspose 授權；否則產生的檔案會出現浮水印。

## 步驟 1 – 如何將資料新增至新工作簿

在建立樞紐分析表之前，必須先有來源資料表。我們會建立一個全新的工作簿，將第一個工作表命名為 *SalesData*，並加入幾筆模擬真實銷售資料的列。

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**為什麼這很重要：**  
- 使用 `PutValue` 會自動設定儲存格類型，之後就不必擔心字串與數值類型不匹配的問題。  
- 在第 1 列定義標題，讓樞紐分析引擎在映射欄位時有可參考的依據。

## 步驟 2 – 建立用來放置樞紐分析表的工作表

樞紐分析表會放在自己的工作表上，讓來源資料保持乾淨，報表也更整齊。

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **如果已經有工作表該怎麼辦？** 只需使用索引（`workbook.Worksheets["MySheet"]`）直接參考，而不必新增工作表。

## 步驟 3 – 定義來源範圍（如何新增資料 → 定義範圍）

Aspose.Cells 需要一個 `CellArea` 或範圍字串，包含標題列與資料列。我們在此假設最多 100 列，實際使用時可自行調整。

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**特殊情況：** 若資料集是動態的，可使用 `salesDataSheet.Cells.MaxDataRow` 計算最後使用的列號，並依此建立範圍。

## 步驟 4 – 如何建立樞紐分析表 – 插入樞紐分析表

現在進入有趣的部分：告訴 Aspose.Cells 建立一個連結至剛才設定範圍的樞紐分析表。

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

請注意公式式的參照 (`=SalesData!A1:D100`)。這與在 Excel 中輸入的語法相同，使 API 更直觀。

## 步驟 5 – 設定列、欄與資料欄位（如何新增資料 → 欄位）

我們會將 *Region* 放在列區，*Product* 放在欄區，並對 *Units* 與 *Revenue* 進行加總。

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**為什麼使用這些索引？**  
Aspose.Cells 的欄位索引從 0 開始，因此 `0` 代表 *Region*。`DataFields.Add` 方法允許你重新命名欄位（例如「Sum of Units」）並選擇彙總類型——`Sum` 是數值資料最常用的彙總方式。

## 步驟 6 – 如何啟用重新整理 – 讓樞紐分析表在開啟時自動更新

如果之後來源資料變更，你可能希望樞紐分析表自動反映這些變化。這時 `RefreshDataOnOpen` 就派上用場。

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **注意：** 此旗標僅在工作簿於 Excel 中開啟時生效；若在 Aspose.Cells 內部則不會重新計算，除非手動呼叫 `pivotTable.RefreshData()`。

## 步驟 7 – 儲存工作簿為 XLSX（如何儲存工作簿為 XLSX）

最後，我們將檔案寫入磁碟。`.xlsx` 格式是現代的、基於 zip 的 Excel 檔案類型，具備跨平台相容性。

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

執行程式後會在執行目錄產生名為 **PivotRefresh.xlsx** 的檔案。於 Excel 開啟後，你會看到一個排版整齊的樞紐分析表，列為 *Region*、欄為 *Product*，且顯示加總的 *Units* 與 *Revenue* 數值。由於已啟用重新整理，對 *SalesData* 工作表的任何編輯，下次開啟工作簿時都會自動更新樞紐分析表。

### 預期輸出

| 地區 | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **總計** | **120** | **85** |   |

（數字會依你加入的列而有所不同。）

---

## 常見問題與變化

### 如果需要多個樞紐分析表該怎麼辦？

你可以使用不同的名稱與位置重複 **步驟 4**。每次呼叫 `PivotTables.Add` 都會回傳一個新索引，可用來取得該樞紐分析表物件。

### 如何將彙總方式改為 *Average*（平均）而非 *Sum*（加總）？

在 `DataFields.Add` 呼叫中，將 `PivotTableDataAggregationType.Sum` 改為 `PivotTableDataAggregationType.Average`。

### 可以為樞紐分析表設定樣式（字型、顏色）嗎？

可以。建立樞紐分析表後，你可以存取其 `Style` 屬性，或對包含樞紐分析表的範圍套用儲存格格式。例如：

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### 是否可以在儲存工作簿後再新增列？

當然可以。使用 `new Workbook("PivotRefresh.xlsx")` 載入檔案，將列加入 *SalesData* 工作表，然後在再次儲存前呼叫 `pivotTable.RefreshData()`。

---

## 完整範例（可直接複製貼上）

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

儲存檔案、執行程式，然後開啟產生的 **PivotRefresh.xlsx** —— 你已經掌握了 **如何在 C# 中建立樞紐分析表**。

---

## 結語

我們已說明了如何以程式方式 **建立樞紐分析表**、如何 **新增資料**、如何 **啟用重新整理**，以及最後如何使用 Aspose.Cells **儲存工作簿為 xlsx**。程式碼

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}