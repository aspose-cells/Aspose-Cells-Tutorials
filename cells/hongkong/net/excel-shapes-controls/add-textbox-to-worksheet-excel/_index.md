---
"description": "在本逐步教學中了解如何使用 Aspose.Cells for .NET 為 Excel 新增可自訂的文字方塊。"
"linktitle": "在 Excel 中為工作表新增文字框"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 Excel 中為工作表新增文字框"
"url": "/zh-hant/net/excel-shapes-controls/add-textbox-to-worksheet-excel/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中為工作表新增文字框

## 介紹
您是否渴望透過獨特的視覺效果來增強您的 Excel 電子表格，以吸引觀眾？添加文字框是實現此目的的好方法！使用 Aspose.Cells for .NET，您可以輕鬆地將文字方塊整合到您的 Excel 工作表中，使您的文件更具資訊量和視覺吸引力。本逐步指南將引導您完成使用 Aspose.Cells 新增文字方塊的簡單流程，展示如何使用文字、顏色、超連結等對其進行個人化設定！
## 先決條件
在我們深入研究編碼奇蹟之前，以下是確保順利航行體驗的基本先決條件：
1. .NET 開發環境：您需要一個可運行的 .NET 框架以及像 Visual Studio 這樣的 IDE。確保它已更新至最新版本！
2. Aspose.Cells for .NET：請確定您已下載 Aspose.Cells 庫。您可以從 [這裡](https://releases。aspose.com/cells/net/).
3. 基本程式設計知識：熟悉 C# 和一些處理 Excel 檔案的一般概念將使本教學更容易！
## 導入包
確保在 C# 檔案的開頭導入必要的套件。您可以按照以下步驟操作：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## 安裝 Aspose.Cells
如果您還沒有這樣做，您可以透過 Visual Studio 中的 NuGet 套件管理器新增 Aspose.Cells：
1. 開啟 Visual Studio。
2. 前往 `Tools` -> `NuGet Package Manager` -> `Manage NuGet Packages for Solution`。
3. 搜尋“Aspose.Cells”並將其安裝到您的專案中。
現在我們已經打好了基礎，讓我們進入有趣的部分吧！
## 步驟 1：設定文檔目錄
首先，讓我們設定儲存所有 Excel 文件的目錄。在我們開始建立工作簿之前，必須確保該目錄存在。
```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory"; 
// 如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists) 
    System.IO.Directory.CreateDirectory(dataDir);
```
此程式碼片段將建立一個名為 `Your Document Directory` （如果它不存在，請用您的實際路徑替換它）。非常簡單，對吧？
## 步驟 2：實例化新工作簿
接下來，我們需要建立一個新的工作簿，在其中新增文字方塊。只需幾行程式碼即可輕鬆完成：
```csharp
// 實例化一個新的工作簿。
Workbook workbook = new Workbook();
```
這行程式碼會建立一個新的 Excel 工作簿。簡單又直接！
## 步驟 3：存取第一個工作表
現在我們已經準備好工作簿，讓我們取得第一個工作表，在其中新增文字方塊：
```csharp
// 取得書中的第一個工作表。
Worksheet worksheet = workbook.Worksheets[0];
```
就這樣，您現在可以訪問名為 `worksheet`。是時候讓它閃耀了！
## 步驟 4：新增文字框
好了，現在是時候添加我們的第一個文字方塊了！具體操作如下：
```csharp
// 在集合中新增一個新的文字方塊。
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
在這一行中，我們指定了文字方塊所在的行和列，並設定了它的寬度和高度（分別為 160 和 200）。請根據您的佈局隨意調整這些數字！
## 步驟5：取得TextBox對象
在新增文字方塊後，我們需要取得對它的引用，以便我們可以自訂其內容：
```csharp
// 取得文字方塊物件。
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[textboxIndex];
```
現在， `textbox0` 是您修改此文字方塊的黃金門票！
## 步驟6：用內容填滿文字框
接下來，讓我們為文字方塊提供一些文字：
```csharp
// 填充文字。
textbox0.Text = "ASPOSE______The .NET & JAVA Component Publisher!";
```
將文字插入文字方塊就是這麼簡單！ 
## 步驟 7：自訂文字方塊外觀
我們把它修飾一下怎麼樣？您可以調整字體顏色、樣式等！
```csharp
// 設定字體顏色。
textbox0.Font.Color = Color.Blue;
// 將字體設定為粗體。
textbox0.Font.IsBold = true;
// 設定字體大小。
textbox0.Font.Size = 14;
// 將字體屬性設定為斜體。
textbox0.Font.IsItalic = true;
```
隨意嘗試不同的顏色和風格，看看哪種視覺效果最好！
## 步驟8：新增超鏈接
想要將您的文字方塊變成可點擊的連結嗎？讓我們這樣做：
```csharp
// 在文字方塊中新增超連結。
textbox0.AddHyperlink("http://www.aspose.com/”);
```
現在，任何點擊您的文字方塊的人都會被帶到 Aspose 網站。就像魔術一樣！
## 步驟9：設定文字方塊放置類型
對於文字方塊相對於工作表的行為方式，您可以有不同的選擇。以下是如何將其設定為自由浮動的範例：
```csharp
// 設定位置。
textbox0.Placement = PlacementType.FreeFloating;
```
或者，如果您希望它調整大小並隨單元格移動，您可以像這樣設定：
```csharp
// 設定放置類型，因為文字方塊將隨單元格移動並調整大小。
textbox1.Placement = PlacementType.MoveAndSize;
```
## 步驟10：自訂線條和填滿格式
您可以透過以下方式變更文字方塊邊框和填滿的外觀：
```csharp
// 取得文字方塊的填滿格式。
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;            
// 取得文字方塊的行格式類型。
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;           
// 設定線條粗細。
lineformat.Weight = 6;
// 將虛線樣式設定為方點。
lineformat.DashStyle = MsoLineDashStyle.SquareDot;
```
透過它，您可以進一步自訂文字框，添加適合您風格的視覺效果。
## 步驟11：新增另一個文字框
沒有人說我們只能添加一個文字框！讓我們再補充一些不同的文字：
```csharp
// 新增另一個文字框。
textboxIndex = worksheet.TextBoxes.Add(15, 4, 85, 120);
// 取得第二個文字方塊。
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[textboxIndex];
// 輸入一些文字。
textbox1.Text = "This is another simple text box";
```
現在，您確實可以使用多個文字方塊來使您的 Excel 工作表更加生動有趣！
## 步驟12：儲存工作簿
最後，是時候保存我們的傑作了！這是當天的最後一行程式碼：
```csharp
// 儲存 Excel 檔案。
workbook.Save(dataDir + "book1.out.xls");
```
只需這一行程式碼，您就建立並修改了一個帶有可自訂文字方塊的 Excel 檔案！
## 結論
恭喜！您已成功使用 Aspose.Cells for .NET 瀏覽 Excel 中的文字方塊世界。您不僅學習如何新增文字框，還學習如何自訂文字框以使您的電子表格更具吸引力。從改變顏色和样式到添加超鏈接，可能性幾乎是無窮無盡的！ 
您準備好開始轉換您的 Excel 文件了嗎？發揮您的創造力，嘗試不同的佈局！
## 常見問題解答
### 什麼是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一個功能強大的程式庫，可讓開發人員輕鬆建立、操作和轉換 Excel 檔案。
### 購買前我可以試用 Aspose.Cells 嗎？
是的！您可以下載並使用免費試用版 [這裡](https://releases。aspose.com/).
### 在哪裡可以找到 Aspose.Cells 的文件？
您可以在以下位置存取綜合文檔 [Aspose.Cells文檔](https://reference。aspose.com/cells/net/).
### 如果我遇到問題，可以獲得支援嗎？
絕對地！如果您需要協助，請前往 [Aspose 論壇](https://forum.aspose.com/c/cells/9) 尋求幫助。
### 我可以在沒有許可證的情況下使用 Aspose.Cells 嗎？
雖然您可以使用免費試用版，但要存取全部功能，您需要購買授權。查看價格 [這裡](https://purchase。aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}