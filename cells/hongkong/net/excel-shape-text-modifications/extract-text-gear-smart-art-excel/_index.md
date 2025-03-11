---
title: 從 Excel 中的齒輪類型智慧藝術中提取文本
linktitle: 從 Excel 中的齒輪類型智慧藝術中提取文本
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 從 Excel 中的齒輪型 SmartArt 中擷取文字。包含逐步指南和程式碼範例。
weight: 10
url: /zh-hant/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 Excel 中的齒輪類型智慧藝術中提取文本

## 介紹
使用 Excel 時，您可能會遇到 SmartArt 圖形，它們有助於以視覺上吸引人的方式傳達訊息。在這些圖形中，齒輪型 SmartArt 因其分層和定向流程而受到喜愛，通常用於專案管理或系統建模。但是，如果您需要以程式設計方式從這些形狀中提取文字怎麼辦？這就是 Aspose.Cells for .NET 派上用場的地方！在這篇文章中，我們將引導您逐步了解如何使用 Aspose.Cells for .NET 從 Excel 中的齒輪型 SmartArt 形狀中提取文字。
## 先決條件
在我們深入研究之前，您需要滿足一些基本的先決條件。不用擔心;這很簡單，我將指導您完成它。
### .NET環境
確保您的電腦上設定了 .NET 開發環境。這可以是 Visual Studio 或您選擇的任何支援 .NET 開發的 IDE。
### Aspose.Cells for .NET
接下來，您需要安裝 Aspose.Cells 函式庫。這是使您能夠無縫操作 Excel 文件的強大功能。您可以從[Aspose 發佈頁面](https://releases.aspose.com/cells/net/)。如果您想先探索它，請利用[免費試用](https://releases.aspose.com/).
### C#基礎知識
您需要遵循本教程，對 C# 程式設計有基本的了解。如果您是新手，不用擔心 - 我將設計盡可能適合初學者的步驟。
### Excel 檔案範例
對於本教學課程，您還需要一個包含齒輪型 SmartArt 形狀的範例 Excel 檔案。您可以輕鬆建立一個或在線查找模板。只需確保 SmartArt 至少包含一種齒輪形狀即可。
## 導入包
要開始編碼，您需要匯入必要的套件。操作方法如下：
### 建立一個新項目
1. 開啟您的 .NET IDE。
2. 建立一個新專案。例如，選擇 .NET 選項下的「控制台應用程式」。
3. 為您的專案命名並設定所需的框架。 
### 新增參考文獻
要使用 Aspose.Cells，您需要將庫引用新增到您的專案中：
1. 在解決方案資源管理器中以滑鼠右鍵按一下您的專案名稱。
2. 選擇“管理 NuGet 套件”。
3. 搜尋“Aspose.Cells”並安裝它。
安裝完成後，您就可以開始編碼了！
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
現在，讓我們分解一下用於提取文字的程式碼。我們將一步一步地做到這一點。
## 第 1 步：設定來源目錄
首先定義 Excel 檔案所在的目錄：
```csharp
//原始碼目錄
string sourceDir = "Your Document Directory";
```
確保更換`"Your Document Directory"`與 Excel 檔案的實際路徑。
## 第 2 步：載入 Excel 工作簿
接下來，我們將載入 Excel 工作簿。這是我們訪問其內容的方式：
```csharp
//載入包含齒輪類型智慧藝術形狀的範例 Excel 檔案。
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
這一部分將載入您的範例 Excel 工作簿。
## 第 3 步：存取第一個工作表
現在我們已經載入了工作簿，讓我們可以存取 SmartArt 所在的第一個工作表：
```csharp
//訪問第一個工作表。
Worksheet ws = wb.Worksheets[0];
```
這將檢索第一個工作表以進行進一步操作。
## 第 4 步：訪問第一個形狀
接下來，我們需要存取工作表中的第一個形狀。透過這樣做，我們可以瀏覽 SmartArt 圖形：
```csharp
//存取第一個形狀。
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
在這裡，我們專注於第一個形狀，我們假設它是我們需要的 SmartArt。
## 第 5 步：取得群組形狀
一旦我們有了形狀，就可以得到 SmartArt 所表示的結果了：
```csharp
//以組形狀的形式得到齒輪型智能藝術形狀的結果。
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
這將檢索我們的齒輪型 SmartArt 作為分組形狀。
## 第 6 步：提取單一形狀
現在，讓我們來擷取組成 SmartArt 的各個造型：
```csharp
//取得由群組形狀組成的單一形狀的清單。
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
該數組將保存我們需要循環遍歷的所有單一形狀。
## 第 7 步：提取並列印文本
最後，我們可以循環遍歷形狀數組並從任何齒輪類型形狀中提取文字：
```csharp
//提取齒輪類型形狀的文字並將其列印在控制台上。
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
在此循環中，我們檢查形狀的類型，如果是齒輪型形狀，則列印文字。
## 第8步：執行確認
最後，一旦該過程成功完成，您可能需要添加一條確認訊息：
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
這樣，您的提取就完成了，您應該在控制台中看到文字輸出！
## 結論
恭喜！您剛剛學習如何使用 Aspose.Cells for .NET 從 Excel 中的齒輪型 SmartArt 形狀中提取文字。這種方便的技術為依賴可視化資料表示的自動化報告或文件打開了大門。無論您是經驗豐富的開發人員還是新手，從 SmartArt 控制和提取資訊都可以簡化您的工作流程並提高效率。別忘了探索細節[Aspose.Cells 文檔](https://reference.aspose.com/cells/net/)以獲得更多功能。
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個 .NET 函式庫，可讓開發人員輕鬆建立和操作 Excel 檔案。
### 我可以將 Aspose.Cells 與其他語言一起使用嗎？
是的！ Aspose.Cells 可用於多種程式語言，包括 Java 和 Python。
### 我需要購買 Aspose.Cells for .NET 嗎？
 Aspose.Cells 提供免費試用，但要長期使用，則需要購買。您可以找到購買選項[這裡](https://purchase.aspose.com/buy).
### 是否為 Aspose.Cells 用戶提供支援？
絕對地！您可以在以下位置找到社區支持：[Aspose.Cells 論壇](https://forum.aspose.com/c/cells/9).
### 我可以使用此方法提取其他 SmartArt 類型嗎？
是的，只需稍加修改，您就可以透過更改程式碼中的條件從各種 SmartArt 形狀中提取文字。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
