---
"description": "了解如何使用 Aspose.Cells for .NET 在 Excel 中新增群組框和單選按鈕。針對各個層級開發人員的分步指南。"
"linktitle": "在 Excel 中將群組框新增至工作表"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 Excel 中將群組框新增至工作表"
"url": "/zh-hant/net/excel-shapes-controls/add-group-box-to-worksheet-excel/"
"weight": 24
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中將群組框新增至工作表

## 介紹
說到資料呈現，Excel 是王者。添加組框等互動元素可以使您的電子表格更具吸引力和用戶友好性。今天，我們將深入研究 Aspose.Cells for .NET 的世界，這是一個強大的程式庫，可幫助您輕鬆操作 Excel 表。但如果您不是編碼專家，也不用擔心——本指南將所有內容分解為簡單的步驟。您準備好提升您的 Excel 技能了嗎？讓我們開始吧！
## 先決條件
在我們進入程式碼之前，您需要做幾件事：
1. Visual Studio：確保您的機器上安裝了 Visual Studio；這是您編寫 .NET 程式碼的地方。
2. Aspose.Cells for .NET：您需要下載此程式庫。你可以找到它 [這裡](https://releases。aspose.com/cells/net/). 
3. C# 基礎知識：雖然我會逐步解釋所有內容，但對 C# 有一點了解將有助於您跟上。
## 導入包
對於任何項目，您首先需要匯入必要的套件。在這裡，Aspose.Cells 將是您的主要關注點。具體操作如下：
## 步驟 1：在 Visual Studio 中開啟項目
啟動 Visual Studio 並開啟現有專案或建立新專案。 
## 步驟 2： 新增 Aspose.Cells 的引用
- 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
- 選擇“管理 NuGet 套件”。
- 搜尋“Aspose.Cells”並安裝它。這將允許您使用 Aspose.Cells 庫提供的所有類別和方法。
## 步驟 3：包含 Using 指令
在 C# 檔案的頂部，包含 Aspose.Cells 命名空間：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
這使您可以存取處理 Excel 文件所需的類別。
現在我們已經完成設置，讓我們深入了解本教程的核心 - 向 Excel 工作表添加帶有單選按鈕的組合框。為了清楚起見，我們將把這個過程分解為多個步驟。
## 步驟 1：設定文檔目錄
在建立任何 Excel 檔案之前，您需要確定要將其儲存在何處。如果目錄不存在，我們就建立一個。
```csharp
// 文檔目錄的路徑
string dataDir = "Your Document Directory"; // 指定您想要的路徑
// 如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
此程式碼檢查儲存 Excel 檔案的目錄是否存在。如果沒有，它會創建一個 - 這就像在深入專案之前準備好工作區一樣！
## 步驟 2：實例化新工作簿
接下來，您需要建立一個 Excel 工作簿，在其中新增群組框。
```csharp
// 實例化一個新的工作簿。
Workbook excelbook = new Workbook();
```
此行初始化工作簿的新實例。可以將其視為開啟一個全新的、空白的 Excel 文件，準備進行修改。
## 步驟 3：新增群組框
現在，讓我們新增該組框。 
```csharp
// 在第一個工作表新增一個群組框。
GroupBox box = excelbook.Worksheets[0].Shapes.AddGroupBox(1, 0, 1, 0, 300, 250);
```
在這裡，您將在第一個工作表中的指定座標處新增一個群組框。這些參數定義了盒子的位置和大小，就像在房間裡定位家具一樣！
## 步驟4：設定群組框的標題
現在，讓我們為你的組框添加一個標題！
```csharp
// 設定組框的標題。
box.Text = "Age Groups";
box.Placement = PlacementType.FreeFloating;
```
「年齡組」字串設定了群組框上顯示的標籤。設定 `Placement` 作為 `FreeFloating` 允許盒子移動－靈活性是關鍵！
## 步驟 5：將群組框變為二維
儘管 3D 聽起來很花哨，但我們在這裡追求的是經典的外觀。
```csharp
// 使其成為二維盒子。
box.Shadow = false;
```
此程式碼消除了陰影效果，使盒子呈現平面外觀 - 就像一張簡單的紙！
## 步驟 6：新增單選按鈕
讓我們添加一些供用戶輸入的單選按鈕來讓事情變得更加有趣。
## 步驟 6.1：新增第一個單選按鈕
```csharp
// 新增單選按鈕。
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
// 設定其文字字串。
radio1.Text = "20-29";
// 將 A1 儲存格設定為單選按鈕的連結儲存格。
radio1.LinkedCell = "A1";
```
您為年齡組 20-29 建立一個單選按鈕，並將其連結到工作表中的儲存格 A1。這表示當選擇此按鈕時，儲存格 A1 會反映該選擇！
## 步驟 6.2：自訂第一個單選按鈕
現在讓我們為它添加一些風格。
```csharp
// 使單選按鈕成為 3-D 的。
radio1.Shadow = true;
// 設定單選按鈕的權重。
radio1.Line.Weight = 4;
// 設定單選按鈕的破折號樣式。
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
透過添加陰影和調整線條樣式，我們增強了按鈕的可見性。這就像添加裝飾，讓它從頁面上彈出！
## 步驟 6.3：重複操作以新增更多單選按鈕
針對其他年齡層重複此過程：
```csharp
// 第二個單選按鈕
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
radio2.Text = "30-39";
radio2.LinkedCell = "A1";
radio2.Shadow = true;
radio2.Line.Weight = 4;
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
// 第三個單選按鈕
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
radio3.Text = "40-49";
radio3.LinkedCell = "A1";
radio3.Shadow = true;
radio3.Line.Weight = 4;
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
每個單選按鈕代表不同年齡範圍的選項，並連結回同一個儲存格 A1。這使得選擇過程變得簡單且用戶友好。
## 步驟 7：將形狀進行分組
一切準備就緒後，讓我們透過對形狀進行分組來整理一下。 
```csharp
// 取得形狀。
Aspose.Cells.Drawing.Shape[] shapeobjects = new Shape[] { box, radio1, radio2, radio3 };
// 將形狀分組。
Aspose.Cells.Drawing.GroupShape group = excelbook.Worksheets[0].Shapes.Group(shapeobjects);
```
此步驟將所有內容組合成一個有凝聚力的單元。這就像在您的藝術收藏品周圍放置一個框架 - 它將它們完美地結合在一起！
## 步驟8：儲存Excel文件
最後，讓我們保存我們的傑作！
```csharp
// 儲存 Excel 檔案。
excelbook.Save(dataDir + "book1.out.xls");
```
這行程式碼將您的變更寫入指定目錄中名為「book1.out.xls」的新 Excel 檔案。就像密封信封一樣，您的工作現在可以安全地存放了！
## 結論
以上就是使用 Aspose.Cells for .NET 為 Excel 工作表新增群組框和單選按鈕的完整指南！透過每一步，您學會如何以程式設計方式操作 Excel，為自訂報告、資料視覺化等開啟了無限的可能性。程式設計的魅力在於您可以相對輕鬆地自動執行任務並創建用戶友好的介面 - 想像一下它的潛力！
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個用於管理 Excel 檔案的 .NET 程式庫，支援以程式設計方式讀取、寫入和操作電子表格等任務。
### 我需要編碼經驗才能使用 Aspose.Cells 嗎？
雖然一些程式設計知識很有幫助，但本教學將引導您了解基礎知識，讓初學者也能輕鬆掌握！
### 我可以自訂組框和按鈕的外觀嗎？
絕對地！ Aspose.Cells 提供了豐富的形狀樣式選項，包括顏色、大小和 3D 效果。
### Aspose.Cells 有免費試用版嗎？
是的！您可以存取以下網址免費試用 [Aspose 免費試用](https://releases。aspose.com/).
### 在哪裡可以找到有關 Aspose.Cells 的更多資源或支援？
這 [Aspose 支援論壇](https://forum.aspose.com/c/cells/9) 是尋求幫助和與社區分享知識的絕佳場所。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}