---
category: general
date: 2026-06-21
description: 快速將 JSON 匯入 Excel，學習如何將 JSON 轉換為 XLSX、從 JSON 產生 Excel，並在幾個簡單步驟中將 JSON
  匯出至試算表。
draft: false
keywords:
- import json to excel
- convert json to xlsx
- generate excel from json
- save json as excel
- export json to spreadsheet
language: zh-hant
og_description: 輕鬆將 JSON 匯入 Excel。本指南將教您如何將 JSON 轉換為 XLSX、從 JSON 產生 Excel，以及使用 C#
  將 JSON 匯出至試算表。
og_title: 使用 Aspose.Cells 將 JSON 匯入 Excel – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  headline: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  type: TechArticle
- description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  name: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints:'
  - name: 1. Import Multiple JSON Arrays into Different Sheets
    text: 'If you have several arrays—say `"Employees"` and `"Departments"`—you can
      import each into its own worksheet:'
  - name: 2. Styling the Generated Table
    text: 'You can apply a style after the data expands:'
  - name: 3. Using a JSON File Instead of a String
    text: 'If your JSON lives on disk, just read it first:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: 使用 Aspose.Cells 匯入 JSON 至 Excel – 完整程式設計指南
url: /zh-hant/net/excel-data-import-export/import-json-to-excel-with-aspose-cells-complete-programming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 匯入 JSON 至 Excel – 完整程式指南

有沒有想過 **如何在不自行編寫解析器的情況下匯入 JSON 至 Excel**？你並不孤單。許多開發者在需要將 JSON 資料轉成整齊的試算表以供報表或資料分析時，常會卡關。好消息是？使用 Aspose.Cells，你只需要幾行程式碼就能 **將 JSON 轉換為 XLSX**，而且整個過程既快速又具型別安全性。

在本教學中，我們將逐步說明 **從 JSON 產生 Excel** 的全部步驟，將結果儲存為 `.xlsx` 檔，甚至還會探討一些實用的變化——例如在變更來源資料時自動更新的試算表。完成後，你將擁有一段可重複使用的程式碼，隨時可以放入任何 .NET 專案。

## 前置條件

在開始之前，請確保你已具備：

- .NET 6.0 或更新版本（此程式碼亦可在 .NET Framework 上執行）
- 有效的 Aspose.Cells for .NET 授權或暫時的評估金鑰
- Visual Studio 2022（或任何你慣用的 C# IDE）
- 基本的 JSON 結構與 C# 語法概念

不需要額外的 NuGet 套件，除了 **Aspose.Cells** 之外，設定相當輕量。

## 步驟 1：安裝 Aspose.Cells 並建立專案

首先，將 Aspose.Cells 套件加入你的專案。開啟 Package Manager Console，執行：

```powershell
Install-Package Aspose.Cells
```

如果你使用 .NET CLI，等價指令為：

```bash
dotnet add package Aspose.Cells
```

> **小技巧：** 安裝完成後，將授權檔 (`Aspose.Cells.lic`) 放到專案根目錄，並在程式啟動時載入：

```csharp
// Load the Aspose.Cells license (optional but removes evaluation watermark)
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

現在，你已經可以開始 **匯入 JSON 至 Excel** 了。

## 步驟 2：準備 JSON 資料

為了示範，我們使用一個簡單的「人員」陣列。實務上，你可能會從檔案、API 回應或資料庫讀取這段字串。

```csharp
// Step 2: Define the JSON data to be imported
string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";
```

可以看到 JSON 是一個平面陣列——這正是 Aspose.Cells 智慧標記（smart markers）最適合的結構。

## 步驟 3：設定 JSON 載入選項

Aspose.Cells 允許你將整個 JSON 陣列視為 *單一* 資料來源。當你希望工作表內的列自動展開時，這點相當重要。

```csharp
// Step 3: Configure JSON loading options to treat the whole array as a single data source
var loadOptions = new Aspose.Cells.JsonLoadOptions
{
    // When true, the whole array becomes one data source (e.g., "People")
    ArrayAsSingle = true
};
```

將 `ArrayAsSingle = true` 設為 true，表示程式庫 **會產生一個會對陣列中每個元素重複的智慧標記**，這是 **將 JSON 轉換為 XLSX** 工作流程的核心。

## 步驟 4：建立 Workbook 並匯入 JSON

接著，我們建立一個全新的 `Workbook` 實例，並使用名為 `"People"` 的智慧標記匯入 JSON。

```csharp
// Step 4: Create a new workbook and import the JSON using a smart marker named "People"
var workbook = new Aspose.Cells.Workbook();
workbook.ImportJson(json, loadOptions, new Aspose.Cells.SmartMarkerOptions
{
    DataSourceName = "People"
});
```

在背後，Aspose.Cells 會解析 JSON，將每個屬性（`Name`、`Age`）對應到欄位，並產生一個稍後會展開成多列的佔位符。

## 步驟 5：在工作表中放置智慧標記

智慧標記的寫法是 `{{People}}`。當工作簿儲存時，Aspose.Cells 會把這個標記取代成包含 JSON 陣列全部資料的表格。

```csharp
// Step 5: Put the smart marker in cell A1 so the data expands when saved
workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");
```

你可以把標記放在任何位置——左上角是常見的選擇，因為它讓表格可以向下與向右自由擴展。

## 步驟 6：將 Workbook 儲存為 XLSX 檔案

最後，把工作簿寫入磁碟。這一步即是 **將 JSON 儲存為 Excel**，產生可在 Excel、Google Sheets 或其他試算表應用程式開啟的正式 `.xlsx` 檔。

```csharp
// Step 6: Save the workbook to a file (convert JSON to XLSX)
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
workbook.Save(outputPath, Aspose.Cells.SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

開啟 `JsonSingleCell.xlsx` 後，你會看到類似以下的內容：

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 28  |

這就是 **從 JSON 產生 Excel** 的實際效果。

## 完整範例程式

把前面的步驟全部組合起來，即成為以下可直接執行的完整程式：

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load license (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Cells.lic");

        // Step 1: Define JSON data
        string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Step 2: Configure loading options
        var loadOptions = new JsonLoadOptions { ArrayAsSingle = true };

        // Step 3: Create workbook and import JSON
        var workbook = new Workbook();
        workbook.ImportJson(json, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });

        // Step 4: Insert smart marker
        workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");

        // Step 5: Save as XLSX (export JSON to spreadsheet)
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Excel file generated successfully at: {outputPath}");
    }
}
```

### 預期輸出

執行程式會在主控台印出：

```
Excel file generated successfully at: C:\YourProject\JsonSingleCell.xlsx
```

開啟產生的檔案會看到兩列資料，欄位 **Name** 與 **Age** 完全對應原始 JSON 陣列。

## 進階變化

### 1. 將多個 JSON 陣列匯入不同工作表

如果你有多個陣列，例如 `"Employees"` 與 `"Departments"`，可以分別匯入至各自的工作表：

```csharp
// Load a more complex JSON with two arrays
string complexJson = @"
{
  ""Employees"": [{""Name"":""John"",""Age"":30}],
  ""Departments"": [{""Dept"":""HR"",""Count"":5}]
}";
var options = new JsonLoadOptions { ArrayAsSingle = false };
var wb = new Workbook();
wb.ImportJson(complexJson, options, new SmartMarkerOptions());

// Place markers
wb.Worksheets[0].Cells["A1"].PutValue("{{Employees}}");
wb.Worksheets.Add();
wb.Worksheets[1].Cells["A1"].PutValue("{{Departments}}");
wb.Save("MultipleSheets.xlsx");
```

現在你已經 **將 JSON 匯出至多分頁試算表**，每個分頁都對應不同的資料集。

### 2. 為產生的表格套用樣式

資料展開後，你可以套用樣式：

```csharp
var table = workbook.Worksheets[0].Cells["A1"].GetSmartMarkerTable();
var style = workbook.CreateStyle();
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightBlue;
style.Pattern = BackgroundType.Solid;
table.ApplyStyle(style);
```

這個小技巧能讓標題列更醒目，對於報表儀表板相當有幫助。

### 3. 使用 JSON 檔案取代字串

如果 JSON 存在於磁碟上，只需先讀取檔案：

```csharp
string jsonFromFile = File.ReadAllText(@"C:\Data\people.json");
workbook.ImportJson(jsonFromFile, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });
```

其餘步驟完全相同，讓你可以從任何來源 **將 JSON 儲存為 Excel**。

## 常見問題與避免方式

- **忘記設定 `ArrayAsSingle`** – 若遺漏此旗標，程式會把每個物件當成獨立資料來源，導致儲存格為空。處理頂層陣列時務必設定。
- **智慧標記名稱錯誤** – 標記 (`{{People}}`) 必須與 `DataSourceName` (`"People"`) 完全相同。拼寫錯誤會使佔位符未被取代。
- **授權未載入** – 評估模式下，輸出檔會出現水印。請盡早載入授權，以保持工作簿乾淨。
- **檔案路徑權限** – 嘗試寫入受保護的資料夾會拋出例外。使用 `Environment.CurrentDirectory` 或使用者可寫入的路徑即可。

## 程式化測試匯出結果

若想在不開啟 Excel 的情況下驗證匯出是否成功，可以讀回第一個儲存格：

```csharp
var wbCheck = new Workbook("JsonSingleCell.xlsx");
string firstName = wbCheck.Worksheets[0].Cells["A2"].StringValue; // Should be "John"
Console.WriteLine($"First imported name: {firstName}");
```

簡單的主控台檢查即可確認 **將 JSON 轉換為 XLSX** 已如預期執行。

## 結論

我們已完整說明如何使用 Aspose.Cells **匯入 JSON 至 Excel**：從安裝套件、準備 JSON、設定智慧標記，到最終 **將 JSON 儲存為 Excel**。無論你是要 **將 JSON 轉換為 XLSX**、**從 JSON 產生 Excel**，或是 **將 JSON 匯出至試算表** 進行分析，流程皆相同——智慧標記負責所有繁重工作。

歡迎自行嘗試樣式調整、多工作表或在執行階段重新匯入 JSON 以實現動態更新。下一步可以把此程式碼整合到 Web API，讓 Excel 報表即時回傳給用戶——只要把檔案寫入改為回傳串流即可。

有關巢狀 JSON 物件或大資料集的疑問嗎？歡迎在下方留言，祝開發順利！

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化你對 API 功能的掌握，並提供其他實作方式的範例：

- [使用 Aspose.Cells for Java 高效匯入 JSON 至 Excel：完整指南](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)
- [使用 Aspose.Cells Java 匯入 JSON 資料至 Excel：完整指南](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [使用 Aspose.Cells for .NET 輕鬆匯入 JSON 至 Excel](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}