---
title: 取得電子表格中使用的字體列表
linktitle: 取得電子表格中使用的字體列表
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過這個易於理解的教程，了解如何使用 Aspose.Cells for .NET 從 Excel 電子表格中取得和列出字體。
weight: 10
url: /zh-hant/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 取得電子表格中使用的字體列表

## 介紹
您是否曾經發現自己滾動瀏覽 Excel 電子表格，想知道其各個單元格中使用的字體？也許您遇到過一份舊文檔，並想知道做出了哪些排版選擇？嗯，你很幸運！使用 Aspose.Cells for .NET，它就像擁有一個工具箱，可讓您篩選並發現隱藏在電子表格中的字體秘密。在本指南中，我們將引導您了解如何輕鬆擷取 Excel 檔案中使用的所有字體的清單。繫好安全帶，讓我們深入電子表格的世界吧！
## 先決條件
在我們開始編寫程式碼之前，您需要先做一些事情。別擔心，這真的很簡單。這是您需要的清單：
1. Visual Studio：確保您的電腦上安裝了 Visual Studio 版本。這是我們編寫程式碼的地方。
2. Aspose.Cells for .NET：您需要有可用的 Aspose.Cells 函式庫。如果您還沒有下載，可以從[地點](https://releases.aspose.com/cells/net/).
3. C# 基礎知識：對 C# 程式設計有一點了解肯定會幫助您輕鬆瀏覽程式碼。
4. 範例 Excel 檔案：您需要使用範例 Excel 文件，例如「sampleGetFonts.xlsx」。這是我們應用字體探索的地方。
一旦一切準備就緒，您就可以開始編碼了！
## 導入包
首先，讓我們導入必要的命名空間。在 .NET 中，導入包類似於邀請合適的客人參加您的聚會 - 沒有他們，事情就不會順利進行。
以下是導入 Aspose.Cells 的方法：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
透過這簡單的線條，我們將 Aspose.Cells 的核心功能引入我們的專案中。現在，讓我們繼續載入工作簿。
## 步驟1：設定文檔目錄
首先，在我們深入程式碼之前，您需要設定文檔目錄的路徑。這是您的 Excel 文件所在的位置。 
```csharp
string dataDir = "Your Document Directory";
```
您將用 Excel 檔案所在的實際路徑取代「您的文件目錄」。可以將其視為告訴程式：「嘿，這是我存放 Excel 文件的地方；快去看看吧！
## 第 2 步：載入來源工作簿
是時候載入 Excel 文件了。我們將建立一個新實例`Workbook`類別並傳入檔案的路徑。 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
這裡發生了什麼事？我們基本上打開了電子表格的大門。這`Workbook`類別允許我們與 Excel 檔案的內容進行互動。 
## 第三步：取得所有字體
現在神奇的時刻到來了——讓我們實際檢索字體！這`GetFonts()`方法是我們的金票。
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
在這裡，我們要求工作簿透露其中使用的所有字體。這`fnts`陣列將保存我們的寶藏。
## 第四步：列印字體
最後，讓我們將這些字體列印出來。這將幫助我們驗證我們的發現。
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
這個循環貫穿我們的每個字體`fnts`array，將它們一一輸出到控制台。這就像展示 Excel 文件中所有很酷的排版選擇！
## 結論
現在你就擁有了！只需幾行程式碼，您就可以使用 Aspose.Cells for .NET 成功檢索並列印 Excel 電子表格中使用的字體清單。這不僅僅是字體的問題；它涉及理解文件的微妙之處、增強簡報以及掌握電子表格中的排版藝術。無論您是開發人員還是只是喜歡擺弄 Excel 的人，這個小片段都可能會改變遊戲規則。 
## 常見問題解答
### 我需要單獨安裝Aspose.Cells嗎？
是的，您需要下載並在專案中引用該庫。 
### 我可以將 Aspose.Cells 用於其他格式嗎？
絕對地！ Aspose.Cells 適用於多種 Excel 格式，例如 XLSX、XLS 和 CSV。
### 有免費試用嗎？
是的，您可以從[下載連結](https://releases.aspose.com/).
### 我如何獲得技術支援？
如果您需要協助，[Aspose 支援論壇](https://forum.aspose.com/c/cells/9)是一個很好的資源。
### Aspose.Cells 與 .NET Core 相容嗎？
是的，Aspose.Cells 也與 .NET Core 專案相容。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
