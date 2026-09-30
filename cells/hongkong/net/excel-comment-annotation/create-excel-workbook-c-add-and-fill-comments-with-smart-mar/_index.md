---
category: general
date: 2026-03-21
description: 使用 C# 建立 Excel 工作簿，學習如何在 Excel 中加入註解，並利用 Smart Markers 自動填入註解。開發者逐步指南。
draft: false
keywords:
- create excel workbook c#
- add comment to excel
- how to add comment
- how to fill comment
- fill excel comment
language: zh-hant
og_description: 使用 C# 建立 Excel 工作簿，快速為 Excel 加上註解，然後使用 Smart Markers 填寫註解。完整教學與程式碼。
og_title: 使用 C# 建立 Excel 工作簿 – 新增與填寫註解
tags:
- C#
- Excel automation
- Aspose.Cells
title: 建立 Excel 活頁簿 C# – 加入並填寫帶有智慧標記的註解
url: /zh-hant/net/excel-comment-annotation/create-excel-workbook-c-add-and-fill-comments-with-smart-mar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 Excel 工作簿 C# – 使用智慧標記新增與填入註解

有沒有曾經需要 **create Excel workbook C#**，卻想知道如何嵌入會自動更新的註解？你並非唯一有此需求的人。在許多報表情境下，你會希望儲存格註解顯示 *「Created by Alice on 2024‑07‑15」*，而不必每次都硬寫姓名或日期。  

在本教學中，我們將完整示範 **how to add comment to Excel**，以及使用 Aspose.Cells 的 Smart Markers **how to fill comment**。完成後，你將擁有一個可直接執行的程式，能建立工作簿、插入動態註解，並儲存檔案——只需幾個簡潔步驟。

> **你將獲得：** 完整、可編譯的 C# 主控台應用程式、每行程式碼的說明、常見陷阱的提示，以及擴充解決方案的想法。

## 前置條件

- .NET 6.0 SDK 或更新版本（程式碼同樣適用於 .NET Core 與 .NET Framework）  
- Visual Studio 2022 或任何你偏好的 IDE  
- **Aspose.Cells for .NET** NuGet 套件 (`Install-Package Aspose.Cells`) —— 此函式庫提供下列使用的 `Workbook`、`Worksheet` 與 `SmartMarkerProcessor` 類別。  
- 具備基本的 C# 語法概念 —— 只要寫過 `Console.WriteLine`，即可開始。

既然前置作業已完成，讓我們開始吧。

![建立 Excel 工作簿 C# 範例截圖](excel-workbook.png "建立 Excel 工作簿 C# 範例")

## 步驟 1：初始化新工作簿 – Create Excel Workbook C# 基礎

首先，我們需要一個全新的工作簿物件。把 `Workbook` 想像成空白畫布；沒有它就無法放置任何儲存格、列或註解。

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // fresh Excel file
            Worksheet worksheet = workbook.Worksheets[0];    // default sheet named "Sheet1"
```

**為什麼這很重要：** `Workbook` 會自動建立預設工作表，除非需要額外分頁，否則不必呼叫 `Add`。存取 `Worksheets[0]` 是開始填入資料的最快方式。

## 步驟 2：插入智慧標記註解 – How to Add Comment with Tokens

接著，我們在儲存格 **B2** 放入包含智慧標記代碼 (`«UserName»` 與 `«CreatedDate»`) 的註解。這些代碼稍後會被實際值取代。

```csharp
            // Step 2: Add a comment that contains Smart Marker tokens
            var comment = worksheet.Cells["B2"].CreateComment();
            comment.Note = "Created by «UserName» on «CreatedDate»";
```

**說明：**  
- `CreateComment()` 若不存在則建立註解物件；若已存在則回傳現有的。  
- `Note` 屬性保存可見文字。將佔位符包在 `« »` 之中，即告訴 Aspose.Cells 這些是 **Smart Markers** —— 可一次性取代的佔位符。

> **專業提示：** 若需要多行註解，可在字串內使用 `\n`，例如 `"Line1\nLine2"`。

## 步驟 3：準備資料物件 – How to Fill Comment Dynamically

智慧標記需要資料來源。在 C# 中，最簡單的方式是使用與佔位符名稱相符的匿名型別。

```csharp
            // Step 3: Prepare the data that will replace the tokens
            var markerData = new
            {
                UserName = "Alice",
                CreatedDate = DateTime.Now   // will be formatted automatically
            };
```

**為什麼使用匿名型別？**  
它輕量、無需額外類別檔，且屬性名稱 (`UserName`、`CreatedDate`) 完全對應代碼名稱。若偏好強型別模型，只需建立具有相同屬性的類別即可。

## 步驟 4：處理智慧標記 – How to Fill Comment Using the Data Object

現在魔法發生了。`SmartMarkerProcessor` 會掃描工作簿中所有 `«…»` 代碼，並以 `markerData` 中的值取代它們。

```csharp
            // Step 4: Process the Smart Markers in the worksheet using the data object
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Process(worksheet, markerData);
```

**背後原理是什麼？**  
`SmartMarkerProcessor` 會遍歷每個儲存格、註解、標頭等，尋找 `«Token»` 樣式。找到後，它利用反射讀取 `markerData` 中對應的屬性，並寫回值。無需手動迴圈。

## 步驟 5：儲存工作簿 – Fill Excel Comment and Persist the File

最後，我們將工作簿寫入磁碟。註解現在會顯示類似 *「Created by Alice on 03/21/2026 10:15 AM」* 的文字。

```csharp
            // Step 5: Save the workbook with the filled comment
            string outputPath = @"YOUR_DIRECTORY\CommentFilled.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**結果驗證：** 在 Excel 中開啟 `CommentFilled.xlsx`，將滑鼠移至儲存格 **B2**，即可看到包含實際使用者名稱與時間戳記的註解。未來執行時不需再更改程式碼，只要修改 `markerData` 的值即可。

---

## 常見變化與邊緣情況

### 使用自訂日期格式

若想將日期顯示為 `yyyy‑MM‑dd` 格式，請調整資料物件：

```csharp
CreatedDate = DateTime.Now.ToString("yyyy-MM-dd")
```

### 新增多個註解

你可以對其他儲存格重複 **Step 2**。每個註解可以有自己的代碼集合，若資訊通用也可共用相同代碼。

### 使用現有工作簿

不要使用 `new Workbook()`，而是載入既有檔案：

```csharp
Workbook workbook = new Workbook(@"ExistingFile.xlsx");
```

其餘步驟保持相同——Smart Markers 在新檔與既有檔皆可運作。

### 處理 Null 值

若代碼可能缺少，請將屬性包成可為 null 的型別或提供備用值：

```csharp
UserName = user?.Name ?? "Unknown"
```

當來源為 `null` 時，處理器會插入 *「Unknown」*。

---

## 完整可執行範例（直接貼上即可）

以下是 **完整程式**，可直接放入主控台應用程式專案並立即執行（只需將 `YOUR_DIRECTORY` 替換為實際資料夾路徑）。

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Add a comment that contains Smart Marker tokens
            var comment = worksheet.Cells["B2"].CreateComment();
            comment.Note = "Created by «UserName» on «CreatedDate»";

            // Step 3: Prepare the data that will replace the tokens
            var markerData = new
            {
                UserName = "Alice",
                CreatedDate = DateTime.Now
            };

            // Step 4: Process the Smart Markers in the worksheet using the data object
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Process(worksheet, markerData);

            // Step 5: Save the workbook with the filled comment
            string outputPath = @"YOUR_DIRECTORY\CommentFilled.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

執行程式，開啟產生的檔案，即可在儲存格 **B2** 看到動態註解。很簡單，對吧？

---

## 常見問答 (FAQ)

**Q: 這在 .NET Framework 4.7 上能運作嗎？**  
A: 當然可以。Aspose.Cells 支援 .NET Framework 4.0 以上以及 .NET Core/5/6/7。只要引用相應的 DLL 或 NuGet 套件即可。

**Q: 我能將此方法用於資料驗證或條件格式化嗎？**  
A: Smart Markers 主要用於在儲存格、註解、標頭與頁腳插入值。若需條件格式化，仍須使用一般的 `Style` API。

**Q: 若要在 **不同** 的工作表加入註解該怎麼做？**  
A: 取得目標工作表 (`workbook.Worksheets["MySheet"]`) 後，在該工作表的儲存格上重複 **Step 2**。

---

## 往後步驟與相關主題

- **How to add comment to Excel** 程式化於多個儲存格（使用迴圈遍歷範圍）。  
- **Fill Excel comment** 從資料庫取得資料（使用 `DataTable` 作為 Smart Markers 的資料來源）。  
- 探索 **Smart Marker arrays** 以自動產生表格。  
- 了解 **Aspose.Cells styling**，以設定註解的字型、顏色與大小。

試玩這些程式碼片段，替換資料來源，你將快速掌握在任何 Excel 自動化情境中 **how to fill comment** 的技巧。

---

### 結語

我們剛剛完整說明了使用 Smart Markers 進行 **create excel workbook c#**、**add comment to excel** 與 **fill excel comment** 的全流程。此解決方案簡潔、可重用，且已可投入生產。

試試看，調整佔位符，讓函式庫負責繁重的工作。若遇到任何問題，歡迎在下方留言——祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}