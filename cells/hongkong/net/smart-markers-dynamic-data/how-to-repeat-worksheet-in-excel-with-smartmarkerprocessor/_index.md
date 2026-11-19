---
category: general
date: 2026-11-19
description: 如何在使用陣列資料填充 Excel 時重複工作表。學習只需幾個步驟即可產生多個工作表並從清單填充工作表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: zh-hant
lastmod: 2026-11-19
og_description: 如何使用 SmartMarkerProcessor 重複工作表。請參考本指南，以陣列資料填充 Excel、產生多個工作表，並從清單填充工作表。
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: 如何在 Excel 中重複工作表 – 步驟指南
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: 如何在 Excel 中使用 SmartMarkerProcessor 重複工作表
url: /zh-hant/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 SmartMarkerProcessor 在 Excel 中重複工作表

如果您在產生 Excel 報表時需要 **how to repeat worksheet**，本指南將為您展示一個完整、可執行的解決方案。完成本教學後，您將能夠使用 SmartMarkerProcessor 函式庫 **populate Excel with array** 資料、**generate multiple worksheets**，以及 **populate worksheet from list**。

在每個部門、區域或時間段都需要自己的分頁時，重複工作表是一項常見需求。以下範例示範了完整步驟，說明每個設定為何重要，並涵蓋空清單或自訂命名等邊緣情況。

## 前置條件

在開始之前，請確保您已具備：

- .NET 6.0 或更新版本已安裝
- 參考包含 `SmartMarkerProcessor` 的 **GroupDocs.Viewer**（或等效）NuGet 套件
- 一個 Excel 範本工作簿（`.xlsx`），其中在您想要重複的列上放置 `${repeat:Dept}` 標記
- 具備 C# 與 LINQ 的基本知識（可選，但有助於理解）

不需要額外的第三方函式庫。

## 步驟 1：建立 SmartMarkerProcessor 實例

處理器負責協調標記取代與工作表複製。未傳入參數即建立實例時，會使用預設選項。

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

提前建立處理器可讓您在套用任何資料前先設定全域選項。這是正確執行 **how to repeat worksheet** 的基礎。

## 步驟 2：啟用工作表重複

預設情況下，處理器僅在目前的工作表上取代標記。將 `RepeatWorksheet` 設為 `true`，即可指示引擎為資料集合中的每個項目克隆整個工作表。

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

啟用此選項是 **generate multiple worksheets** 的關鍵——處理器會為 `Dept` 陣列中的每個元素建立一個新分頁，並保留原始格式。

## 步驟 3：將資料來源準備為陣列或清單

SmartMarkerProcessor 可接受任何可列舉集合，但使用陣列能在您想要 **populate worksheet from list** 時更清晰。此處我們建立一個匿名物件，內含 `Dept` 屬性，該屬性保存字串陣列。

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

如果您已經有 `List<string>`，也可以直接傳入；處理器會以相同方式處理。重要的是屬性名稱（`Dept`）必須與範本中的 `${repeat:Dept}` 標記相符。

## 步驟 4：載入範本工作表

假設您已有 `ExcelPackage`（來自 EPPlus）或 `Workbook` 物件，取得您想要重複的工作表。變數 `ws` 代表該工作表。

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

如果您偏好其他函式庫（例如 ClosedXML），原理相同：取得實作所需介面的工作表物件即可。

## 步驟 5：使用資料處理工作表

現在將資料套用到範本。處理器會為每個部門克隆工作表，將 `${repeat:Dept}` 標記取代為實際的部門名稱，其他部分則保持不變。

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

`Process` 完成後，`ws` 成為多個工作表中的第一個——每個部門一個。原始工作表的名稱會被保留，複製的工作表則會得到遞增的後綴（例如 “Sheet1 (1)”、 “Sheet1 (2)”）。如果需要自訂命名，可在之後重新命名。

### 預期輸出

開啟產生的活頁簿時，您應該會看到：

- **Sheet1** – 原始範本（通常留空或作為主模板）
- **Sheet1 (1)** – 填入 “HR”
- **Sheet1 (2)** – 填入 “IT”
- **Sheet1 (3)** – 填入 “Finance”

每個工作表的版面相同，只是 `${repeat:Dept}` 出現的地方已被部門名稱取代。

## 處理邊緣情況

### 空陣列或 null 陣列

若 `Dept` 為 null 或空陣列，處理器不會建立任何額外工作表。為避免活頁簿完全空白，您可以加入防護：

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### 自訂工作表名稱

預設的命名規則未必符合所有報表需求。處理完畢後，可使用迴圈為每個工作表重新命名：

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### 填充額外欄位

若需 **populate excel with array** 超過單一標記的值，可擴充資料物件：

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

然後將範本標記調整為 `${repeat:Dept.Name}` 與 `${repeat:Dept.Headcount}`。處理器會為每個部門重複該列，並同時填入兩個欄位。

## 完整範例

以下是一個自包含的 Console 應用程式，示範從載入範本到儲存最終活頁簿的完整流程。

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Explanation of key sections**

- **Processor creation** – establishes the engine that will interpret markers.
- **RepeatWorksheet option** – activates the core feature that answers *how to repeat worksheet*.
- **Data source** – uses an array (`new[]`) to satisfy **populate excel with array**.
- **Template loading** – demonstrates a common way to obtain a worksheet object.
- **Processing** – performs the duplication and data insertion in one call.
- **Renaming** – shows how to turn the generic “(1)”, “(2)” names into meaningful titles, a typical requirement after **generate multiple worksheets**.

執行此程式會產生 `Result.xlsx`，其中包含三個部門專屬的分頁，皆由陣列填入資料。

## 常見陷阱與專業提示

- **Marker spelling** – the marker must match the property name exactly (`${repeat:Dept}`). A typo prevents repetition.
- **Worksheet index** – after processing, the original sheet stays at index 0; generated sheets follow sequentially. Mis‑indexing can lead to renaming the wrong tab.
- **Large data sets** – generating hundreds of worksheets can increase file size dramatically. Consider splitting reports or using a single sheet with grouped sections if performance becomes an issue.
- **Thread safety** – `SmartMarkerProcessor` is not thread‑safe. Create a separate instance per thread if you process multiple workbooks in parallel.

## 結論

您現在已掌握如何使用 SmartMarkerProcessor 在 Excel 中 **how to repeat worksheet**、如何 **populate excel with array** 資料、如何 **generate multiple worksheets**，以及如何高效 **populate worksheet from list**。完整範例將所有概念串聯，且可選的重新命名步驟讓您產出乾淨、使用者友好的分頁名稱。

接下來，您可以探索：

- 使用 **populate worksheet from list** 處理複雜物件（巢狀集合）
- 在工作表複製後套用條件格式
- 將產生的活頁簿匯出為 PDF 或 CSV 供下游使用

歡迎將程式碼套用到您自己的報表情境，盡情自動化 Excel 活頁簿吧！

## 接下來您可以學習什麼？

以下教學與本指南所示技術緊密相關，能進一步深化您的應用。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在專案中探索替代實作方式。

- [如何重複工作表 – Excel 自動化完整指南](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [為每個項目建立工作表 – 在 C# 中如何重複工作表](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [如何在 Excel 中展開陣列並填充範本](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}