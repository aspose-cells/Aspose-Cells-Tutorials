---
category: general
date: 2026-03-25
description: 從 JSON 建立 Excel 工作簿並將其儲存為 xlsx。學習如何在幾分鐘內將 JSON 匯出為 xlsx、從 JSON 產生 Excel，以及從
  JSON 填充 Excel。
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: zh-hant
og_description: 即時從 JSON 建立 Excel 活頁簿。本指南示範如何將 JSON 匯出為 XLSX、從 JSON 產生 Excel，並使用 Aspose.Cells
  從 JSON 填充 Excel。
og_title: 從 JSON 建立 Excel 工作簿 – 完整 C# 教學
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: 從 JSON 建立 Excel 工作簿 – 步驟指南
url: /zh-hant/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 JSON 建立 Excel 工作簿 – 完整 C# 教程

是否曾經需要 **create excel workbook** 從 JSON 資料負載，但不知從何開始？你並不孤單；許多開發者在將 API 資料轉換成整齊的試算表時，都會卡在這一步。好消息是，只要寫幾行 C# 程式碼並使用 Aspose.Cells，就能 **export json to xlsx**、**generate excel from json**，以及 **populate excel from json**，而不必依賴第三方轉換工具。

在本指南中，我們將完整示範整個流程——從原始 JSON 字串、放入 SmartMarker，最後 **save workbook as xlsx** 到磁碟。完成後，你將得到一個可直接使用的 Excel 檔案，長相如下：

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **Pro tip:** 如果你已在專案的其他地方使用 Aspose.Cells，可以重複使用相同的 `Workbook` 實例來匯入多個 JSON——非常適合批次處理。

---

## 需要的環境

- **.NET 6+**（或任何支援 C# 10 的近期 .NET Framework）
- **Aspose.Cells for .NET** – 透過 NuGet 安裝：`dotnet add package Aspose.Cells`
- 基本的 C# 語法了解（不需要深入的 Excel 知識）

就這些。無需外部服務、無需 COM interop，純粹的受管理程式碼。

---

## Step 1: Initialize a New Excel Workbook

首先，我們建立一個全新的 workbook 物件。把它想像成打開一個空白的 Excel 檔案，之後會把資料放進去。

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

為什麼要從新 workbook 開始？這樣可以確保乾淨的起點，避免前一次執行遺留下的樣式，且檔案大小保持最小——非常適合自動化流水線。

---

## Step 2: Prepare the JSON Data You Want to Import

為了示範，我們使用一個小型的 JSON 陣列，你也可以自行替換成從 Web 服務、檔案或資料庫查詢取得的任何有效 JSON。

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

注意雙斜線跳脫的引號（`\"`）——這只是 C# 字串文字的語法。在實務上，你通常會從檔案讀取：

```csharp
// string jsonData = File.ReadAllText("data.json");
```

---

## Step 3: Tell SmartMarker to Treat the Whole Array as One Record

Aspose.Cells 的 SmartMarker 引擎可以自動遍歷集合。啟用 **ArrayAsSingle** 後，我們會把整個 JSON 陣列視為單一記錄，這正是產生平面表格所需要的行為。

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

如果忘記設定此旗標，SmartMarker 會為每個元素建立一個獨立的工作表——顯然不是你想要的簡易表格。

---

## Step 4: Place a SmartMarker Token in the Worksheet

SmartMarker 代碼看起來像 `${jsonArray}`。處理器執行時會把代碼替換成 JSON 資料。我們把代碼放在 **A1** 儲存格，讓輸出從左上角開始。

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

你也可以在處理前先格式化標題列。例如，將第一列設定為粗體：

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

---

## Step 5: Run the SmartMarker Processor

現在魔法發生了。處理器會讀取 JSON，將每個屬性對應到欄位，並在代碼下方寫入資料列。

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

在背後，Aspose.Cells 會：

1. 將 JSON 解析成 .NET 物件。
2. 將屬性名稱（`Name`、`Score`）對應到欄位標題。
3. 把每個陣列元素寫成新的一列。

如果你的 JSON 包含巢狀物件，可以使用點記法（`${parent.child}`）來引用——對於更複雜的報表非常實用。

---

## Step 6: Save the Workbook as an XLSX File

最後，將 workbook 儲存到磁碟。`.xlsx` 副檔名告訴 Excel（以及大多數其他試算表程式）這是一個 OpenXML 工作簿。

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

當然，如果你在開發 Web API，也可以直接把 workbook 串流回 HTTP 回應：

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

---

## Full Working Example

以下是完整、可直接執行的程式碼，涵蓋上述所有步驟。複製貼上到新的 Console 專案，然後按 **F5** 執行。

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**Expected result:** 開啟 `json-single.xlsx` 後會看到兩列資料位於粗體標題之下——`John` 的分數為 `90`，`Anna` 的分數為 `85`。欄位名稱會自動從 JSON 屬性名稱推斷。

---

## Common Questions & Edge Cases

### What if my JSON keys contain spaces or special characters?

SmartMarker 需要有效的識別名稱。請將空格改為底線，或使用自訂對應：

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### How do I export a large JSON array (thousands of rows)?

處理器會在內部串流資料，因此記憶體使用量保持適中。不過，你可能需要：

- 增加工作表的 `MaxRows` 限制（`worksheet.Cells.MaxRow = 1_048_576;` —— Excel 的最大列數）。
- 為提升效能關閉格線顯示（`worksheet.IsGridlinesVisible = false;`）。

### Can I add multiple JSON tables to the same workbook?

可以。只要在不同區域放置不同的 SmartMarker 代碼（例如，在 `A10` 放 `${orders}`，在 `D1` 放 `${customers}`），然後對每個代碼呼叫一次 `Process`，或一次傳入包含多個陣列的複合 JSON 物件。

---

## Bonus: Adding a Simple Chart (Optional)

如果想要視覺化分數，可在資料填入後快速加入柱狀圖：

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

圖表會自動參照新加入的資料列，讓你的報表一次完成。

---

## Conclusion

現在你已掌握 **how to create excel workbook** 從 JSON 字串、**export json to xlsx**、**generate excel from json**，以及 **populate excel from json** 的完整流程，全部透過 Aspose.Cells 的 SmartMarker 功能實現。從初始化 workbook、設定 SmartMarker、處理 JSON，到儲存檔案，只需少量程式碼，卻能支援大規模資料。

接下來可以嘗試把靜態 JSON 換成 API 呼叫、根據分數加入條件格式，或為不同資料領域產生多個工作表。同樣的模式也適用於 CSV、XML，甚至資料庫結果集——只要更換來源字串並調整 SmartMarker 代碼即可。

祝開發順利，願你的試算表永遠保持整潔！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}