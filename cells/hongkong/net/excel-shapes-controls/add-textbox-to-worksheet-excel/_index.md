---
title: 將文字方塊新增至 Excel 中的工作表
linktitle: 將文字方塊新增至 Excel 中的工作表
second_title: Aspose.Cells .NET Excel 處理 API
description: 在此逐步教學中，了解如何使用 Aspose.Cells for .NET 將可自訂文字方塊新增至 Excel。
weight: 14
url: /zh-hant/net/excel-shapes-controls/add-textbox-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將文字方塊新增至 Excel 中的工作表

## 介紹
您是否熱衷於透過吸引受眾的獨特視覺效果來增強您的 Excel 試算表？添加文字框是實現此目的的好方法！透過 Aspose.Cells for .NET，您可以輕鬆地將文字方塊整合到 Excel 工作表中，讓您的文件資訊更豐富且更具視覺吸引力。本逐步指南將引導您完成使用 Aspose.Cells 新增文字方塊的簡單流程，展示如何使用文字、顏色、超連結等對其進行個人化！
## 先決條件
在我們深入研究編碼奇蹟之前，以下是確保順利航行體驗的基本先決條件：
1. .NET 開發環境：您需要一個可用的 .NET 框架以及 Visual Studio 等 IDE。確保已更新至最新版本！
2.  Aspose.Cells for .NET：請確定您已下載 Aspose.Cells 庫。您可以從以下位置取得最新版本[這裡](https://releases.aspose.com/cells/net/).
3. 基本程式設計知識：熟悉 C# 和處理 Excel 檔案的一些一般概念將使本教學變得更容易！
## 導入包
確保在 C# 檔案的開頭導入必要的套件。您可以按照以下方法執行此操作：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## 安裝 Aspose.Cells
如果您還沒有這樣做，您可以透過 Visual Studio 中的 NuGet 套件管理器新增 Aspose.Cells：
1. 打開視覺工作室。
2. 前往`Tools` ->`NuGet Package Manager` ->`Manage NuGet Packages for Solution`.
3. 搜尋“Aspose.Cells”並為您的專案安裝它。
現在我們已經奠定了基礎，讓我們進入有趣的部分！
## 第 1 步：設定您的文件目錄
首先，讓我們設定儲存所有 Excel 文件的目錄。在我們開始建立工作簿之前，必須確保該目錄存在。
```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory"; 
//如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists) 
    System.IO.Directory.CreateDirectory(dataDir);
```
此程式碼片段將建立一個名為的目錄`Your Document Directory`（請將其替換為您的實際路徑）如果它尚不存在。簡單易行，對吧？
## 第 2 步：實例化新工作簿
接下來，我們需要建立一個新的工作簿，在其中新增文字方塊。這可以透過幾行程式碼輕鬆完成：
```csharp
//實例化一個新的工作簿。
Workbook workbook = new Workbook();
```
這行程式碼會建立一個新的 Excel 工作簿。簡單明了！
## 第 3 步：存取第一個工作表
現在我們已經準備好了工作簿，讓我們取得第一個工作表，我們將在其中新增文字方塊：
```csharp
//取得本書中的第一個工作表。
Worksheet worksheet = workbook.Worksheets[0];
```
就像這樣，您現在可以訪問第一個名為`worksheet`。是時候讓它發光了！
## 第四步：新增文字框
好吧，是時候添加我們的第一個文字框了！操作方法如下：
```csharp
//將新文字方塊新增至集合。
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
在這一行中，我們指定文字方塊將放置的行和列，並設定其寬度和高度（分別為 160 和 200）。請根據您的佈局隨意調整這些數字！
## 步驟5：取得TextBox對象
在新增文字方塊後，我們需要取得對其的引用，以便自訂其內容：
```csharp
//取得文字方塊物件。
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[textboxIndex];
```
現在，`textbox0`是您修改此文字方塊的金票！
## 第 6 步：用內容填滿文字框
接下來，我們為文字方塊提供一些文字：
```csharp
//填寫文字。
textbox0.Text = "ASPOSE______The .NET & JAVA Component Publisher!";
```
將文字插入文字方塊就是這麼簡單！ 
## 第7步：自訂文字方塊外觀
我們稍微修飾一下怎麼樣？您可以調整字體顏色、樣式等等！
```csharp
//設定字體顏色。
textbox0.Font.Color = Color.Blue;
//將字體設定為粗體。
textbox0.Font.IsBold = true;
//設定字體大小。
textbox0.Font.Size = 14;
//將字體屬性設定為斜體。
textbox0.Font.IsItalic = true;
```
隨意嘗試不同的顏色和款式，看看什麼在視覺上最受歡迎！
## 步驟 8：新增超鏈接
想要將文字方塊變成可點擊的連結嗎？讓我們這樣做：
```csharp
//將超連結新增至文字方塊。
textbox0.AddHyperlink("http://www.aspose.com/");
```
現在，任何點擊您的文字方塊的人都會被轉到 Aspose 網站。就像魔法一樣！
## 步驟9：設定文字方塊放置類型
對於文字方塊相對於工作表的行為方式，您有不同的選擇。以下是如何將其設定為自由浮動的範例：
```csharp
//設定放置位置。
textbox0.Placement = PlacementType.FreeFloating;
```
或者，如果您希望它調整大小並隨單元格移動，您可以這樣設定：
```csharp
//設定放置類型，因為文字方塊將隨單元格移動並調整大小。
textbox1.Placement = PlacementType.MoveAndSize;
```
## 第10步：自訂線條和填滿格式
以下是更改文字方塊邊框和填滿的外觀的方法：
```csharp
//取得文字方塊的填滿格式。
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;            
//取得文字方塊的行格式類型。
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;           
//設定線寬。
lineformat.Weight = 6;
//將破折號樣式設定為方點。
lineformat.DashStyle = MsoLineDashStyle.SquareDot;
```
這樣，您可以進一步自訂文字框，添加適合您風格的視覺效果。
## 第11步：新增另一個文字框
沒有人說我們只能添加一個文字框！讓我們放入另一張有不同文字的圖片：
```csharp
//新增另一個文字框。
textboxIndex = worksheet.TextBoxes.Add(15, 4, 85, 120);
//取得第二個文字方塊。
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[textboxIndex];
//向其中輸入一些文字。
textbox1.Text = "This is another simple text box";
```
現在，您確實可以使用多個文字方塊讓您的 Excel 工作表變得更加生動活潑！
## 第 12 步：儲存工作簿
最後，是時候拯救我們的傑作了！這是當天的最後一行程式碼：
```csharp
//儲存 Excel 檔案。
workbook.Save(dataDir + "book1.out.xls");
```
僅用這一行程式碼，您就建立並修改了帶有可自訂文字方塊的 Excel 檔案！
## 結論
恭喜！您已使用 Aspose.Cells for .NET 成功地瀏覽了 Excel 中的文字方塊世界。您不僅學習如何新增文字框，還學習如何自訂文字方塊以使電子表格更具吸引力。從改變顏色和樣式到甚至添加超鏈接，可能性幾乎是無限的！ 
您準備好開始轉換您的 Excel 文件了嗎？發揮您的創造力，嘗試不同的佈局！
## 常見問題解答
### 什麼是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一個功能強大的程式庫，可讓開發人員輕鬆建立、操作和轉換 Excel 檔案。
### 購買前我可以試用 Aspose.Cells 嗎？
是的！您可以下載並使用免費試用版[這裡](https://releases.aspose.com/).
### 在哪裡可以找到 Aspose.Cells 的文件？
您可以存取全面的文件：[Aspose.Cells 文檔](https://reference.aspose.com/cells/net/).
### 如果我遇到問題，可以獲得支援嗎？
絕對地！如果您需要協助，請前往[Aspose論壇](https://forum.aspose.com/c/cells/9)尋求幫助。
### 我可以在沒有許可證的情況下使用 Aspose.Cells 嗎？
雖然您可以使用免費試用版，但要存取完整功能，您需要購買授權。查看定價[這裡](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
