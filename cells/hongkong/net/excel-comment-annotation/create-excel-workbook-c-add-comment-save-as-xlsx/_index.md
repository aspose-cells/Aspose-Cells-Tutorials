---
category: general
date: 2026-03-18
description: 使用 C# 建立帶有註解的 Excel 工作簿，並將工作簿另存為 XLSX。學習如何加入註解、產生 Excel 註解，以及自動化 Excel
  檔案。
draft: false
keywords:
- create excel workbook c#
- add excel comment
- save workbook as xlsx
- how to add comment
- generate excel comment
language: zh-hant
og_description: 使用 C# 建立含註解的 Excel 工作簿，並儲存為 XLSX。請依照本逐步指南，為 Excel 加入註解並以程式方式產生註解。
og_title: 使用 C# 建立 Excel 活頁簿 – 新增註解並儲存為 XLSX
tags:
- C#
- Excel Automation
- Aspose.Cells
title: 使用 C# 建立 Excel 活頁簿 – 加入註解並另存為 XLSX
url: /zh-hant/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 Excel 工作簿 C# – 新增註解並儲存為 XLSX

有沒有需要 **create Excel workbook C#** 並在儲存格內貼上一則備註，但卻不知從何開始？你並非唯一的開發者——大家常常會問 *how to add comment*，而不想手動開啟 Excel。

在本教學中，你將獲得一個完整、可直接執行的解決方案，示範 **how to add excel comment**、使用 Smart Marker **generate excel comment**，以及 **save workbook as xlsx** 的完整流程。沒有多餘的參照，只要把程式碼貼到 Visual Studio 即可執行。

## 你將學到什麼

- 使用 C# 從頭開始初始化 Excel 工作簿。
- 插入會變成 Excel 註解的 Smart Marker。
- 提供 JSON 資料將標記轉換為真實註解。
- 將檔案持久化為 `.xlsx` 工作簿。
- 提供不使用 Smart Marker 的可選註解加入方式。

### 前置條件

- .NET 6（或 .NET Framework 4.7+）。  
- **Aspose.Cells for .NET** NuGet 套件 – 提供 Smart Marker 功能的程式庫。  
- 基本的 C# 開發環境（Visual Studio、VS Code、Rider…）。

> **Pro tip:** 如果預算有限，Aspose 提供完整功能的免費試用版，可用於開發與測試。

---

## 第一步：建立 Excel 工作簿 C# – 設定專案

首先，讓我們建立一個新的 console 應用程式，並加入 Aspose.Cells 套件。

```bash
dotnet new console -n ExcelCommentDemo
cd ExcelCommentDemo
dotnet add package Aspose.Cells
```

現在開啟 `Program.cs`。我們首先要做的事是 **create a new workbook**。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1️⃣: Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();               // creates an empty Excel file in memory
        Worksheet ws = workbook.Worksheets[0];            // default sheet is named "Sheet1"
```

為什麼要從全新工作簿開始？這樣可以確保乾淨的起點，消除隱藏的格式，並讓你從頭掌控所有設定——非常適合自動化報表產生。

---

## 第二步：如何新增註解 – 使用 Smart Marker

Smart Markers 是 Aspose 在執行時會以資料取代的佔位符。透過嵌入符合 **`${Comment:UserComment}`** 格式的標記，我們告訴引擎將此佔位符轉換為實際的註解。

```csharp
        // Step 2️⃣: Place a Smart Marker in B2 that will become a comment
        ws.Cells["B2"].PutValue("${Comment:UserComment}");
```

注意到 `Comment:` 前綴了嗎？這是處理器將該值視為註解而非純文字的提示。如果你在想 *「這能用在其他儲存格類型嗎？」*——答案是肯定的，你可以將相同的標記套用到任何儲存格，甚至是合併儲存格範圍。

---

## 第三步：準備 JSON 資料 – 註解內容

接下來的部分是資料來源。這裡我們使用簡單的 JSON 字串，但你也可以提供 DataTable、List，甚至自訂物件。

```csharp
        // Step 3️⃣: Define JSON that supplies the comment text
        string json = "{ \"UserComment\": \"Reviewed by QA\" }";
```

你可以自由將 `"Reviewed by QA"` 換成任何動態值——例如時間戳記、使用者名稱，或是問題追蹤系統的連結。鍵名 (`UserComment`) 必須與標記的識別子相符。

---

## 第四步：產生 Excel 註解 – 處理 Smart Marker

現在我們將 JSON 交給 Smart Marker 處理器。這就是 **generate excel comment** 真正發生的時刻。

```csharp
        // Step 4️⃣: Process the marker and turn it into a real comment
        ws.SmartMarkerProcessor.Process(json);
```

在背後，Aspose 會解析 JSON，找到 `UserComment` 欄位，並將其注入為附加在儲存格 **B2** 的註解。儲存格顯示的值仍為原始佔位文字，但在 Excel 中將滑鼠懸停時會顯示註解。

---

## 第五步：儲存工作簿為 XLSX – 持久化結果

最後，我們將工作簿寫入磁碟。這滿足了 **save workbook as xlsx** 的需求。

```csharp
        // Step 5️⃣: Save the file – you’ll see the comment in B2 when you open it
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

在 Excel 中開啟 `output.xlsx`，將滑鼠懸停於儲存格 **B2**，即可看到註解 *「Reviewed by QA」* 出現。就這樣——不需要手動操作、也不需要 COM interop，純粹使用 C#。

---

## 替代方案：如何在不使用 Smart Markers 的情況下新增註解

如果你偏好更直接的方式，也可以自行建立註解物件：

```csharp
// Direct comment creation (no Smart Marker)
Comment comment = ws.Comments[ws.Comments.Add("B2")];
comment.Note = "Directly added comment";
```

當註解文字在編譯時已知，或需要設定作者、寬度或高度等額外屬性時，此方法相當方便。然而，透過 Smart Markers **generate excel comment** 在面對大量列與欄的資料驅動情境時更為強大。

---

## 專業提示與常見陷阱

| 情況 | 需留意事項 | 建議解決方案 |
|-----------|-------------------|-----------------|
| 大型資料集（10k+ 列） | Smart Marker 處理可能佔用大量記憶體 | 使用支援串流資料的 `SmartMarkerProcessor.Process` 重載，或將工作簿分割成多個區塊 |
| 需要自訂作者名稱 | 預設作者為空白 | 在建立註解後設定 `comment.Author = "MyApp";` |
| 想讓註解預設可見 | Excel 會在懸停前隱藏註解 | 設定 `comment.Visible = true;` |
| 使用較舊的 Excel 版本 | 可能不支援 `.xlsx` | 改為使用 `SaveFormat.Xls` 儲存，但需注意某些註解功能會有所不同 |

---

## 預期輸出

- **工作簿檔案：** `output.xlsx` 位於專案的 bin 資料夾。  
- **儲存格 B2：** 顯示佔位文字 `${Comment:UserComment}`（可透過將儲存格字型顏色設為白色來隱藏）。  
- **附加於 B2 的註解：** 懸停時顯示「Reviewed by QA」。

![建立 Excel 工作簿 C# 範例，顯示 B2 儲存格的註解](https://example.com/placeholder-image.png "建立 Excel 工作簿 C# 範例，顯示 B2 儲存格的註解")

*圖片替代文字:* **建立 Excel 工作簿 C# 範例，顯示 B2 儲存格的註解**

---

## 回顧 – 我們完成了什麼

我們 **created an Excel workbook C#**，插入了會轉換成 **excel comment** 的 **Smart Marker**，提供 JSON 以 **generate excel comment**，最後 **saved workbook as xlsx**。整個流程僅以數十行簡潔、獨立的 C# 程式碼完成。

## 接下來？擴充解決方案

- **批次註解產生：** 迭代 DataTable，對每一列套用 Smart Marker 以加入列特定的備註。  
- **註解樣式設定：** 調整字型大小、顏色，或使用 `Comment.RichText` 集合加入富文字。  
- **匯出為 PDF：** 使用 `workbook.Save("output.pdf", SaveFormat.Pdf);` 以保留註解的方式分享報表。

如果你對在其他情境下以程式方式 **add excel comment**（例如使用 OpenXML SDK 或 EPPlus）感到好奇，這些函式庫同樣支援註解建立，只是 API 介面有所不同。

### 最後的想法

從 C# 為 Excel 檔案新增註解不必是繁雜的工作。透過 Aspose.Cells 的 Smart Marker 引擎，你可以以簡潔、資料驅動的方式 **add excel comment**、**generate excel comment**，並 **save workbook as xlsx**，且僅需最少的樣板程式碼。  

試試看，調整 JSON，即可快速將原始資料轉換為精緻、充滿註解的試算表。祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}