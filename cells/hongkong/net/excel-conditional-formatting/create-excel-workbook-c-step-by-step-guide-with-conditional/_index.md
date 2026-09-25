---
category: general
date: 2026-03-27
description: 使用 C# 與 Aspose.Cells 建立 Excel 工作簿、套用條件格式、將 DataTable 匯入 Excel，並將工作簿儲存為
  xlsx——一次教學完成。
draft: false
keywords:
- create excel workbook c#
- apply conditional formatting
- import datatable to excel
- save workbook as xlsx
- create excel file programmatically
language: zh-hant
og_description: 使用 C# 及 Aspose.Cells 建立 Excel 活頁簿，套用條件格式，將 DataTable 匯入 Excel，並在數分鐘內將活頁簿儲存為
  xlsx。
og_title: 使用 C# 建立 Excel 工作簿 – 完整指南與條件格式設定
tags:
- Aspose.Cells
- C#
- Excel automation
title: 使用 C# 建立 Excel 活頁簿 – 含條件格式化的逐步指南
url: /zh-hant/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 Excel 工作簿 C# – 完整程式教學

是否曾經需要即時 **create excel workbook c#**，卻不知從何開始？你並非唯一遇到此問題的人——許多開發者在首次自動化報表時都會卡住。於本指南中，我們將完整示範如何使用 Aspose.Cells **create excel workbook c#**、套用條件格式、將 DataTable 匯入 Excel，最後將工作簿儲存為 xlsx。  

本教學將提供一個可直接執行的主控台應用程式，產生彩色的 Excel 檔案，並對每一行程式碼作清晰說明，讓你能套用到自己的專案。無需額外文件，只要複製、貼上並執行即可。  

### 先決條件

- .NET 6+（或 .NET Framework 4.7.2+）已安裝  
- Visual Studio 2022 或任何你喜歡的 C# 編輯器  
- Aspose.Cells for .NET（可取得免費試用版 NuGet 套件）  

如果你已具備上述環境，讓我們開始吧。

## 建立 Excel 工作簿 C# – 初始化工作簿

首先，你必須透過實例化 `Workbook` 類別來 **create excel workbook c#**。此物件在記憶體中代表整個 Excel 檔案。

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                // <-- creates the workbook
        Worksheet worksheet = workbook.Worksheets[0];      // first sheet (Sheet1)
```

> **Why this matters:** `Workbook` 類別抽象化了檔案格式，讓你不必處理低階的 XML 或 COM 互操作。它同時直接提供樣式、表格與智慧標記的存取。

## 套用條件格式

現在工作簿已建立，讓我們 **apply conditional formatting** 以突顯數量超過 100 的列。條件格式是設定在工作表上，而非單一儲存格，因而具備可重複使用的特性。

```csharp
        // Step 4: Apply conditional formatting to highlight quantities > 100
        int cfIndex = worksheet.ConditionalFormattings.Add();               // add a new CF collection
        var conditionalFormatting = worksheet.ConditionalFormattings[cfIndex];
        var condition = conditionalFormatting.AddCondition(
            FormatConditionType.CellValue, OperatorType.Greater, "100");   // > 100

        // Define the style that will be applied when the condition is true
        condition.Style = workbook.CreateStyle();
        condition.Style.Font.Color = Color.Red;               // red font
        condition.Style.Pattern = BackgroundType.Solid;       // solid background
        condition.Style.ForegroundColor = Color.Yellow;      // yellow fill
```

> **Pro tip:** 若需要更複雜的規則（例如介於兩個值之間），只要再次呼叫 `AddCondition` 並使用 `OperatorType.Between` 即可。

## 寫入標題與智慧標記

在 **import datatable to excel** 之前，我們需要佔位儲存格——智慧標記（smart markers），程式庫會將其替換為實際資料。可將其視為模板標籤。

```csharp
        // Step 2: Write the header row
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // Step 3: Define smart markers that will be replaced by data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");
```

> **Why smart markers?** 它讓你將 Excel 版面與程式碼分離。你只需設計一次工作表，然後提供 `DataTable`，程式庫便會自動完成其餘工作。

## 匯入 DataTable 至 Excel

以下是 **import datatable to excel** 的核心。我們建立一個與智慧標記欄位相對應的 `DataTable`，並將其傳遞給 `ImportDataTable`。

```csharp
        // Step 5: Build a simple DataTable that matches the smart marker fields
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // Step 6: Populate the worksheet with the DataTable via smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");
```

> **Edge case:** 若資料表的欄位多於需求，只需在智慧標記中省略多餘的欄位；程式庫會忽略它們。

## 儲存工作簿為 XLSX

最後，我們將 **save workbook as xlsx** 儲存至磁碟。`Save` 方法會自動依檔案副檔名判斷格式。

```csharp
        // Step 7: Save the result to an Excel file
        workbook.Save("SmartMarkersConditional.xlsx");   // <-- saves as .xlsx
    }
}
```

以上即為完整程式。執行後，你會在輸出資料夾看到名為 `SmartMarkersConditional.xlsx` 的檔案。

### 預期輸出

| Product | Quantity | Status |
|---------|----------|--------|
| Apple   | 120      | High   |
| Banana  | 80       | Low    |
| Cherry  | 150      | High   |

具有 **Quantity > 100**（Apple 與 Cherry）的列，因先前加入的條件格式，將顯示黃色背景紅色文字。

## 程式化建立 Excel 檔案 – 完整原始碼清單

以下提供完整、可直接複製的原始碼，包含我們討論的所有部分，並附加少量說明以增進清晰度。

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write header cells
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // 3️⃣ Insert smart markers – placeholders for our data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");

        // 4️⃣ Apply conditional formatting (highlight >100)
        int cfIdx = worksheet.ConditionalFormattings.Add();
        var cf = worksheet.ConditionalFormattings[cfIdx];
        var cond = cf.AddCondition(FormatConditionType.CellValue, OperatorType.Greater, "100");
        cond.Style = workbook.CreateStyle();
        cond.Style.Font.Color = Color.Red;
        cond.Style.Pattern = BackgroundType.Solid;
        cond.Style.ForegroundColor = Color.Yellow;

        // 5️⃣ Build a DataTable that matches the markers
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // 6️⃣ Import the DataTable – this replaces the smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");

        // 7️⃣ Save the workbook – this will create an .xlsx file
        workbook.Save("SmartMarkersConditional.xlsx");
    }
}
```

> **Tip:** 若需產生多個工作表，只要在透過 `workbook.Worksheets.Add()` 取得的新 `Worksheet` 實例上重複第 2‑6 步即可。

## 為何選擇 Aspose.Cells 進行 C# Excel 自動化？

- **Performance:** 完全在記憶體中運作，無需 COM 互操作，即使處理大型資料集亦相當快速。  
- **Feature‑rich:** 支援智慧標記、條件格式、圖表、樞紐分析表等多項功能。  
- **Cross‑platform:** 可在 Windows、Linux 與 macOS 上執行，支援 .NET Core/5/6+。  

如果在某個功能上卡住——例如加入圖表或保護工作表——只要搜尋 “asp​ose.cells add chart c#” 即可找到相似範例。

## 往後步驟與相關主題

- **Export to PDF:** 完成 **create excel workbook c#** 後，可立即使用 `workbook.Save("output.pdf")` 匯出為 PDF。  
- **Read existing Excel files:** 使用 `new Workbook("ExistingFile.xlsx")` 來修改範本。  
- **Bulk import:** 若資料量龐大，可考慮使用 `ImportArray` 或搭配 `ImportOptions` 的 `ImportDataTable` 以提升速度。  

歡迎嘗試不同的條件規則、顏色，或使用公式加入合計列。只要 **create excel file programmatically**，你的創意無限。

---

*想親自試試看嗎？取得程式碼、執行，然後開啟產生的 `SmartMarkersConditional.xlsx`。若遇到任何問題，請在下方留言——祝編程愉快！*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}