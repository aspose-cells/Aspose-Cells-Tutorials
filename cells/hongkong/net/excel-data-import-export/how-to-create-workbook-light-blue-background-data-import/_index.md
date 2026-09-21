---
category: general
date: 2026-02-09
description: 如何在 C# 中建立工作簿，設定淡藍色背景並匯入帶有標題的資料。學習如何加入淡藍色背景、使用 Excel 預設樣式以及匯入 DataTable。
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: zh-hant
og_description: 如何在 C# 中建立具有淡藍色背景的工作簿、匯入含標題的資料，並套用 Excel 預設樣式——一篇簡潔指南。
og_title: 如何建立工作簿 – 淡藍色背景，資料匯入
tags:
- C#
- Excel
- Aspose.Cells
title: 如何建立工作簿 – 淺藍背景，資料匯入
url: /zh-hant/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何建立 Workbook – 淡藍背景與資料匯入

有沒有想過 **如何在 C# 中建立 workbook**，讓它一開始就看起來更美觀？或許你已經從資料庫取得了 `DataTable`，卻對那一成不變的白色儲存格感到厭倦。在本教學中，我們將一步步示範如何建立新的 workbook、為某一欄加入淡藍背景，並在保留 Excel 預設樣式的同時匯入帶有標題的資料。

我們也會穿插幾個「如果…」的情境，例如處理 null 值或同時自訂多個欄位。完成後，你將擁有一個完整樣式的 Excel 檔案，直接交給利害關係人而不需要額外後處理。

## 前置條件

在開始之前，請確保你已具備：

* **.NET 6+**（此程式碼亦可在 .NET Framework 4.6+ 上執行）  
* **Aspose.Cells for .NET** – 提供 `Workbook`、`Style` 與 `ImportDataTable` 功能的函式庫。請透過 NuGet 安裝：  

  ```bash
  dotnet add package Aspose.Cells
  ```

* 一個 `DataTable` 資源 – 範例中會自行建立假資料，你也可以改用任何 ADO.NET 查詢。

都準備好了嗎？好，讓我們開始吧。

## 步驟 1：初始化新的 Workbook（主要關鍵字）

首先要做的就是 **如何建立 workbook** – 就是字面上的意思。`Workbook` 類別代表整個 Excel 檔案，而它的建構子會給你一張全新的空白工作表。

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **為什麼這很重要：** 從全新 `Workbook` 開始，讓你從一開始就能掌控所有樣式。如果直接開啟既有檔案，會繼承原作者留下的樣式，容易造成格式不一致。

## 步驟 2：準備要匯入的 DataTable

為了說明，我們先建立一個簡單的 `DataTable`。在實務上，你可能會呼叫 stored procedure 或使用 ORM 方法。

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **小技巧：** 若必須完全保留資料庫中欄位的順序，請將 `ImportDataTable` 的 `importColumnNames` 參數設為 `true`。這樣 Aspose.Cells 會自動為你寫入欄位標題。

## 步驟 3：定義欄位樣式 – 預設 + 淡藍背景

現在要解決 **add light blue background** 的需求。Aspose.Cells 允許你傳入一個 `Style` 陣列，對應到每個要匯入的欄位。第一個元素是第 0 欄的樣式，第二個是第 1 欄，以此類推。若樣式數量少於欄位數，未指定的欄位會使用 workbook 的預設樣式。

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **為什麼只需要兩種樣式？** 在範例中我們有四個欄位，但只想讓第二欄（Name）突出。陣列長度不必與欄位數相同；缺少的項目會自動繼承 workbook 的預設樣式。

## 步驟 4：匯入 DataTable（含標題與樣式）

這一步結合了 **excel import datatable c#** 與 **import data with headers**。`ImportDataTable` 方法負責寫入欄位名稱、資料列，並套用前面建立的樣式陣列。

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### 預期結果

執行程式後，`workbook` 會包含一個工作表，外觀如下：

| **ID** | **Name** (淡藍) | **HireDate** | **Salary** |
|-------|----------------|--------------|------------|
| 1     | Alice Johnson  | 5/12/2020    | 72000      |
| 2     | Bob Smith      | 3/4/2019     | 68000      |
| 3     | Carol White    | *(blank)*   | 75000      |

* **Name** 欄位呈現淡藍背景，證明樣式陣列已正確套用。  
* 由於 `importColumnNames` 設為 `true`，欄位標題會自動產生。  
* null 值會顯示為空白儲存格，這是 Aspose.Cells 的預設行為。

## 步驟 5：儲存 Workbook（可選但實用）

通常你會想把檔案寫入磁碟或回傳給前端。儲存非常簡單：

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **專業提示：** 若目標是較舊的 Excel 版本，將 `SaveFormat.Xlsx` 改成 `SaveFormat.Xls` 即可。API 會自動處理轉換。

## 邊緣案例與變化

### 多個已樣式化的欄位

若需要超過一個欄位套用樣式，只要擴充 `columnStyles` 陣列即可：

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

現在 **Name** 與 **Salary** 兩個欄位都會是淡藍色。

### 使用條件格式取代固定樣式

有時想讓欄位在數值超過門檻時變紅。這時 **use default style excel** 可以結合條件格式：

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### 不匯入標題

如果下游系統已自行提供標題，只要把 `importColumnNames` 參數設為 `false`。資料會從 `A1` 開始，你可以之後自行寫入自訂標題。

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## 完整範例（全部

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}