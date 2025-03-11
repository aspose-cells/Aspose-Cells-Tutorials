---
title: 讀取工作表中線索評論的建立時間
linktitle: 讀取工作表中線索評論的建立時間
second_title: Aspose.Cells .NET Excel 處理 API
description: 學習使用 Aspose.Cells for .NET 在 Excel 中讀取執行緒註解的建立時間。包含程式碼範例的分步指南。
weight: 21
url: /zh-hant/net/worksheet-operations/read-threaded-comment-created-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 讀取工作表中線索評論的建立時間

## 介紹
使用 Excel 檔案時，管理註釋可能是資料協作和回饋的重要方面。如果您使用 Aspose.Cells for .NET，您會發現它對於處理各種 Excel 功能（包括執行緒註解）非常強大。在本教程中，我們將重點放在如何讀取工作表中線索評論的建立時間。無論您是經驗豐富的開發人員還是新手，本指南都將逐步引導您完成整個過程。
## 先決條件
在我們深入研究程式碼之前，讓我們確保您擁有開始使用所需的一切：
1. Aspose.Cells for .NET：請確保您已安裝 Aspose.Cells 函式庫。您可以從[阿斯普斯網站](https://releases.aspose.com/cells/net/).
2. Visual Studio：Visual Studio 或任何其他 .NET IDE 的有效安裝，您可以在其中編寫和執行 C# 程式碼。
3. C# 基礎知識：熟悉 C# 程式設計將有助於您更好地理解程式碼片段。
4.  Excel 檔案：準備一個包含一些線索註解的 Excel 檔案。對於本例，我們將使用一個名為`ThreadedCommentsSample.xlsx`.
現在我們已經滿足了先決條件，讓我們導入必要的套件。
## 導入包
要開始使用 Aspose.Cells，您需要匯入所需的命名空間。操作方法如下：
### 導入 Aspose.Cells 命名空間
在 Visual Studio 中開啟 C# 項目，然後在程式碼檔案頂部新增以下 using 指令：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
此命名空間可讓您存取 Aspose.Cells 庫提供的所有類別和方法。
現在我們已經做好了準備，讓我們將讀取線程評論的創建時間的過程分解為可管理的步驟。
## 第 1 步：定義來源目錄
首先，您需要指定 Excel 檔案所在的目錄。這很重要，因為程式需要知道在哪裡找到文件。
```csharp
//原始碼目錄
string sourceDir = "Your Document Directory";
```
代替`"Your Document Directory"`與 Excel 檔案的實際路徑。這可能是這樣的`"C:\\Documents\\"`.
## 第 2 步：載入工作簿
接下來，您將載入包含串連註解的 Excel 工作簿。操作方法如下：
```csharp
Workbook workbook = new Workbook(sourceDir + "ThreadedCommentsSample.xlsx");
```
這行程式碼創建了一個新的`Workbook`透過載入指定的 Excel 檔案來取得物件。如果找不到該文件，則會拋出異常，因此請確保路徑正確。
## 第 3 步：訪問工作表
載入工作簿後，下一步是存取包含註釋的特定工作表。在我們的例子中，我們將存取第一個工作表：
```csharp
//訪問第一個工作表
Worksheet worksheet = workbook.Worksheets[0];
```
此行會從工作簿中檢索第一個工作表（索引 0）。如果您的註解位於不同的工作表上，請相應地調整索引。
## 第 4 步：獲取線索評論
現在，是時候從特定單元格檢索線程註釋了。在此範例中，我們將從儲存格 A1 取得註解：
```csharp
//獲取線索評論
ThreadedCommentCollection threadedComments = worksheet.Comments.GetThreadedComments("A1");
```
此行取得與儲存格 A1 關聯的所有執行緒註解。如果沒有評論，集合將為空。
## 第 5 步：迭代評論
檢索線索評論後，我們現在可以循環它們並顯示詳細信息，包括創建時間：
```csharp
foreach (ThreadedComment comment in threadedComments)
{
    Console.WriteLine("Comment: " + comment.Notes);
    Console.WriteLine("Author: " + comment.Author.Name);
    Console.WriteLine("Created Time: " + comment.CreatedTime);
}
```
這個循環遍歷了中的每則評論`threadedComments`集合並列印出評論文字、作者姓名以及評論創建時間。
## 步驟6：確認訊息
最後，在執行評論閱讀邏輯後，提供確認訊息總是一個好主意。這有助於調試並確保程式碼已成功執行：
```csharp
Console.WriteLine("ReadThreadedCommentCreatedTime executed successfully.");
```
## 結論
恭喜！您已經成功學習如何使用 Aspose.Cells for .NET 讀取 Excel 工作表中串聯註解的建立時間。此功能對於追蹤 Excel 文件中的回饋和協作非常有用。只需幾行程式碼，您就可以提取有價值的信息，從而增強您的數據分析和報告流程。
## 常見問題解答
### 什麼是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一個功能強大的程式庫，可讓開發人員在 .NET 應用程式中建立、操作和轉換 Excel 檔案。
### 如何下載 Aspose.Cells for .NET？
您可以從[阿斯普斯網站](https://releases.aspose.com/cells/net/).
### 有免費試用嗎？
是的，您可以透過造訪免費試用 Aspose.Cells[免費試用頁面](https://releases.aspose.com/).
### 我可以訪問其他單元的評論嗎？
絕對地！您可以修改儲存格引用`GetThreadedComments`方法從任何單元格訪問評論。
### 我可以在哪裡獲得 Aspose.Cells 的支援？
如需支持，您可以訪問[Aspose論壇](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
