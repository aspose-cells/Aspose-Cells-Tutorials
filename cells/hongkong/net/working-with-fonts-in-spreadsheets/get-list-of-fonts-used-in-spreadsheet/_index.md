---
"description": "透過這個簡單易懂的教程，了解如何使用 Aspose.Cells for .NET 從 Excel 電子表格中取得和列出字體。"
"linktitle": "取得電子表格中使用的字體列表"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "取得電子表格中使用的字體列表"
"url": "/zh-hant/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 取得電子表格中使用的字體列表

## 介紹
您是否曾經發現自己在瀏覽 Excel 電子表格時，對其中各個單元格所使用的字體感到疑惑？也許您遇到過一份舊文檔，並想知道其排版選擇是什麼？嗯，你很幸運！使用 Aspose.Cells for .NET，就像擁有一個工具箱，可讓您篩選並發現電子表格中隱藏的字體秘密。在本指南中，我們將帶您了解如何輕鬆擷取 Excel 檔案中使用的所有字體的清單。繫好安全帶，讓我們進入電子表格的世界！
## 先決條件
在我們開始編寫程式碼之前，您需要做一些事情。別擔心，這真的很簡單。以下是您需要的物品清單：
1. Visual Studio：確保您的機器上安裝了某個版本的 Visual Studio。我們將在這裡編寫程式碼。
2. Aspose.Cells for .NET：您需要有 Aspose.Cells 函式庫可用。如果你還沒有下載，你可以從 [地點](https://releases。aspose.com/cells/net/).
3. C# 基礎知識：對 C# 程式設計有一點了解肯定會幫助您輕鬆瀏覽程式碼。
4. 範例 Excel 檔案：您將需要一個範例 Excel 檔案（如「sampleGetFonts.xlsx」）來使用。這就是我們應用字體探索的地方。
一旦一切準備就緒，您就可以開始編碼了！
## 導入包
首先，讓我們導入必要的命名空間。在 .NET 中，導入包就像邀請合適的客人參加您的聚會 - 沒有他們，事情就不會順利進行。
導入 Aspose.Cells 的方法如下：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
透過這行簡單的程式碼，我們將 Aspose.Cells 的核心功能引入我們的專案中。現在，讓我們繼續載入工作簿。
## 步驟1：設定文檔目錄
首先，在深入研究程式碼之前，您需要設定文檔目錄的路徑。這是您的 Excel 文件所在的位置。 
```csharp
string dataDir = "Your Document Directory";
```
您將用 Excel 檔案所在的實際路徑取代「您的文件目錄」。想像告訴程序，“嘿，這是我存放 Excel 文件的地方；去看看吧！”
## 步驟 2：載入來源工作簿
現在該載入 Excel 文件了。我們將建立一個新的實例 `Workbook` 類別並傳入檔案的路徑。 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
這裡發生了什麼事？我們基本上打開了電子表格的大門。這 `Workbook` 類別允許我們與 Excel 檔案的內容進行互動。 
## 步驟3：取得所有字體
現在到了神奇的時刻——讓我們真正檢索字體！這 `GetFonts()` 方法就是我們的黃金門票。
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
在這裡，我們要求工作簿透露其中使用的所有字體。這 `fnts` 陣列將保存我們的寶藏。
## 步驟4：列印字體
最後，讓我們把這些字體印出來。這將幫助我們驗證我們的發現。
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
這個循環遍歷我們 `fnts` 數組，並將它們逐一輸出到控制台。這就像炫耀您在 Excel 文件中擁有的所有酷炫的排版選擇！
## 結論
就是這樣！只需幾行程式碼，您就可以使用 Aspose.Cells for .NET 成功檢索並列印 Excel 電子表格中使用的字體清單。這不僅與字體有關；它是關於理解文件的細微之處、增強簡報以及掌握電子表格中的排版藝術。無論您是開發人員還是只是喜歡擺弄 Excel 的人，這個小片段都可能改變遊戲規則。 
## 常見問題解答
### 我需要單獨安裝 Aspose.Cells 嗎？
是的，您需要下載並在您的專案中引用該庫。 
### 我可以將 Aspose.Cells 用於其他格式嗎？
絕對地！ Aspose.Cells 適用於多種 Excel 格式，例如 XLSX、XLS 和 CSV。
### 有免費試用嗎？
是的，你可以從 [下載連結](https://releases。aspose.com/).
### 我如何獲得技術支援？
如果您需要協助， [Aspose 支援論壇](https://forum.aspose.com/c/cells/9) 是一項寶貴的資源。
### Aspose.Cells 與 .NET Core 相容嗎？
是的，Aspose.Cells 也與 .NET Core 專案相容。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}