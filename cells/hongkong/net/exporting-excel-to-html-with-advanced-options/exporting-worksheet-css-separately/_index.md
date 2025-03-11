---
title: 在輸出 HTML 中單獨匯出工作表 CSS
linktitle: 在輸出 HTML 中單獨匯出工作表 CSS
second_title: Aspose.Cells .NET Excel 處理 API
description: 在此全面的逐步教學中，了解如何使用 Aspose.Cells for .NET 透過單獨的 CSS 將 Excel 工作表有效匯出為 HTML。
weight: 14
url: /zh-hant/net/exporting-excel-to-html-with-advanced-options/exporting-worksheet-css-separately/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在輸出 HTML 中單獨匯出工作表 CSS

## 介紹
在本指南中，您將學習如何將 Excel 工作表匯出為 HTML，特別注意單獨匯出 CSS。這不僅提高了樣式的可維護性，也提高了工作流程效率。現在，讓我們深入了解先決條件並親自動手！
## 先決條件
在我們開始編寫程式碼之前，為了讓本教學順利進行，您需要執行以下操作：
1. Aspose.Cells for .NET 授權：您需要授權才能充分利用 Aspose.Cells 的功能。你可以[下載最新版本](https://releases.aspose.com/cells/net/)或得到一個[臨時執照](https://purchase.aspose.com/temporary-license/)如果你只是試水溫。
2. 開發環境：理想情況下，您應該安裝 Visual Studio 才能無縫執行 .NET 專案。
3. C# 基礎知識：具備一點 C# 程式設計基礎將有助於您更好地理解程式碼片段。
4. 參考文件：熟悉[Aspose.Cells 文檔](https://reference.aspose.com/cells/net/)了解更多特性和功能。
一旦您從清單中勾選了這些先決條件，我們就準備好開始令人興奮的部分了！
## 導入包
首先，您需要從 Aspose.Cells 匯入相關的命名空間。設定方法如下：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Drawing;
```
此設定將為您提供建立工作簿、操作工作表和管理樣式所需的所有工具。

讓我們將其分解為可管理的區塊，每一步都讓您更接近將充滿活力的 Excel 工作表匯出到 HTML 文件中的目標，並將所有 CSS 內容分開！
## 第1步：設定輸出目錄
您需要做的第一件事是決定要儲存匯出的 HTML 檔案的位置。這一點至關重要，因為如果你犯了這個錯誤，你可能最終會到處搜尋你的文件！
```csharp
string outputDir = "Your Document Directory";
```
只需更換`"Your Document Directory"`以及您想要儲存檔案的路徑。例如：`string outputDir = @"C:\MyExports\";`.
## 第 2 步：建立工作簿對象
接下來，我們需要建立一個新的工作簿物件。將工作簿視為您的空白畫布，所有魔法都發生在其中！
```csharp
Workbook wb = new Workbook();
```
透過這樣做，我們初始化了 Workbook 類別的一個新實例。這個變數`wb`現在將儲存我們的整個 Excel 工作表。
## 第 3 步：存取第一個工作表
現在是時候深入畫布並獲得第一個工作表了。這部分很簡單，因為我們只需要本教學的第一張紙。
```csharp
Worksheet ws = wb.Worksheets[0];
```
此行取得工作簿中的第一個工作表，準備進行操作。
## 第 4 步：操作單元格的值
現在進入有趣的部分 - 讓我們將一些資料放入單元格中！您可以選擇任何儲存格，但在本例中，我們將使用儲存格「B5」。
```csharp
Cell cell = ws.Cells["B5"];
cell.PutValue("This is some text.");
```
在這一行中，我們插入了文字「This is some text」。進入儲存格 B5。很簡單，對吧？ 
## 步驟5：設定單元格樣式
讓我們加入一點天份吧！我們將透過將字體顏色變更為紅色來設定文字樣式。 
```csharp
Style st = cell.GetStyle();
st.Font.Color = Color.Red;
cell.SetStyle(st);
```
此步驟會擷取儲存格 B5 的現有樣式，將字體顏色變更為紅色，然後重新套用新樣式。現在您的儲存格不再只是另一個純文字方塊！
## 步驟 6：指定 HTML 儲存選項
在此階段，我們將準備 HTML 儲存選項。這對於確保您的 CSS 單獨匯出至關重要。
```csharp
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.ExportWorksheetCSSSeparately = true;
```
隨著`ExportWorksheetCSSSeparately`選項設為 true，您將告訴庫明確處理 CSS 樣式，而不是將它們直接嵌入到 HTML 文件中。
## 步驟 7：將工作簿另存為 HTML
最後，是時候省掉所有的辛苦了！此行將工作簿作為 HTML 檔案保存在指定的輸出目錄中。
```csharp
wb.Save(outputDir + "outputExportWorksheetCSSSeparately.html", opts);
```
在這裡，我們命名我們的輸出文件`outputExportWorksheetCSSSeparately.html`。瞧——你成功了！
## 第8步：確認執行
要知道一切順利，輸出確認訊息始終是個好習慣。
```csharp
Console.WriteLine("ExportWorksheetCSSSeparatelyInOutputHTML executed successfully.");
```
現在您可以運行程式碼，如果您看到確認訊息，那麼恭喜您已成功使用單獨的 CSS 匯出 Excel 工作表！
## 結論
這就是您自己的指南，將 Excel 工作表匯出為 HTML，同時保持 CSS 獨立，這要歸功於 Aspose.Cells for .NET。這不僅可以使您的樣式保持井井有條，而且還可以在您將來需要進行更改時提供更大的靈活性。 
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的 .NET 程式庫，可讓您建立、修改和轉換 Excel 電子表格，而無需 Microsoft Excel。
### 如何獲得 Aspose.Cells 的免費試用版？
您可以從以下位置下載免費試用版：[Aspose.Cells 發佈頁面](https://releases.aspose.com/).
### 我可以進一步自訂 HTML 輸出嗎？
是的，Aspose.Cells 提供了各種選項來根據您的需求自訂 HTML 輸出。
### 是否可以使用 Aspose.Cells 操作其他工作表元素？
絕對地！ Aspose.Cells 可讓您操作電子表格中的圖表、圖像和許多其他元素。
### 我可以在哪裡找到其他資源？
查看[Aspose.Cells 文檔](https://reference.aspose.com/cells/net/)取得詳細指南和 API 參考。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
