---
title: 將分組框新增至 Excel 中的工作表
linktitle: 將分組框新增至 Excel 中的工作表
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 在 Excel 中新增群組框和單選按鈕。適合各級開發人員的分步指南。
weight: 24
url: /zh-hant/net/excel-shapes-controls/add-group-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將分組框新增至 Excel 中的工作表

## 介紹
當談到資料呈現時，Excel 是王者。添加分組框等互動元素可以使您的電子表格更具吸引力和用戶友好性。今天，我們將深入了解 Aspose.Cells for .NET 的世界，這是一個功能強大的程式庫，可協助您輕鬆操作 Excel 工作表。但如果您不是編碼專家，請不要擔心 - 本指南將所有內容分解為簡單的步驟。您準備好提升 Excel 技能了嗎？讓我們開始吧！
## 先決條件
在我們開始編寫程式碼之前，您需要做一些事情：
1. Visual Studio：確保您的電腦上安裝了 Visual Studio；您將在其中編寫 .NET 程式碼。
2.  Aspose.Cells for .NET：您需要下載此程式庫。你可以找到它[這裡](https://releases.aspose.com/cells/net/). 
3. C# 的基本知識：雖然我將逐步解釋所有內容，但對 C# 的一點了解將有助於您跟進。
## 導入包
對於任何項目，您首先需要匯入必要的套件。在這裡，Aspose.Cells 將是您的主要關注點。操作方法如下：
## 第 1 步：在 Visual Studio 中開啟您的專案
啟動 Visual Studio 並開啟現有專案或建立新專案。 
## 步驟2：新增對Aspose.Cells的引用
- 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
- 選擇“管理 NuGet 套件”。
- 搜尋“Aspose.Cells”並安裝它。這將允許您使用 Aspose.Cells 庫提供的所有類別和方法。
## 第 3 步：包含使用指令
在 C# 檔案的頂部，包含 Aspose.Cells 命名空間：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
這使您可以存取處理 Excel 文件所需的類別。
現在我們已完成設置，讓我們深入了解本教學的核心內容 - 將帶有單選按鈕的群組框新增至 Excel 工作表。為了清楚起見，我們將把這個過程分解為多個步驟。
## 第 1 步：設定您的文件目錄
在建立任何 Excel 檔案之前，您需要確定要將其儲存在何處。如果目錄尚不存在，我們就建立一個。
```csharp
//文檔目錄的路徑
string dataDir = "Your Document Directory"; //指定您想要的路徑
//如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
此程式碼檢查儲存 Excel 檔案的目錄是否存在。如果沒有，它會創建一個 - 就像在投入專案之前準備工作空間一樣！
## 第 2 步：實例化新工作簿
接下來，您需要建立一個 Excel 工作簿，在其中新增群組框。
```csharp
//實例化一個新的工作簿。
Workbook excelbook = new Workbook();
```
此行初始化工作簿的新實例。將此視為開啟一個新的空白 Excel 檔案以供修改。
## 第 3 步：新增組框
現在，讓我們新增該組框。 
```csharp
//將群組框新增至第一個工作表。
GroupBox box = excelbook.Worksheets[0].Shapes.AddGroupBox(1, 0, 1, 0, 300, 250);
```
在這裡，您將在第一個工作表中的指定座標處新增一個群組框。這些參數定義了盒子的位置和大小，就像在房間裡放置家具一樣！
## 第四步：設定組框的標題
現在，讓我們為您的群組框指定一個標題！
```csharp
//設定組框的標題。
box.Text = "Age Groups";
box.Placement = PlacementType.FreeFloating;
```
 “Age Groups”字串設定出現在群組框上的標籤。設定`Placement`作為`FreeFloating`允許盒子移動－靈活性是關鍵！
## 第 5 步：將分組框設為 2-D
雖然 3D 聽起來可能很花哨，但我們在這裡追求經典的外觀。
```csharp
//使其成為二維盒子。
box.Shadow = false;
```
此程式碼消除了陰影效果，使盒子具有平坦的外觀 - 就像一張簡單的紙一樣！
## 第 6 步：新增單選按鈕
讓我們透過添加一些用於用戶輸入的單選按鈕來使事情變得有趣。
## 步驟 6.1：新增第一個單選按鈕
```csharp
//新增一個單選按鈕。
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
//設定其文字字串。
radio1.Text = "20-29";
//將 A1 儲存格設定為單選按鈕的連結儲存格。
radio1.LinkedCell = "A1";
```
您為 20-29 歲年齡組建立一個單選按鈕，將其連結到工作表中的儲存格 A1。這表示當選擇此按鈕時，儲存格 A1 會反映該選擇！
## 步驟 6.2：自訂第一個單選按鈕
現在讓我們給它一些風格。
```csharp
//將單選按鈕設為 3D。
radio1.Shadow = true;
//設定單選按鈕的權重。
radio1.Line.Weight = 4;
//設定單選按鈕的破折號樣式。
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
透過添加陰影和調整線條樣式，我們增強了按鈕的可見性。這就像添加裝飾使其從頁面上脫穎而出！
## 步驟 6.3：重複更多單選按鈕
對其他年齡組重複此過程：
```csharp
//第二個單選按鈕
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
radio2.Text = "30-39";
radio2.LinkedCell = "A1";
radio2.Shadow = true;
radio2.Line.Weight = 4;
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
//第三個單選按鈕
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
radio3.Text = "40-49";
radio3.LinkedCell = "A1";
radio3.Shadow = true;
radio3.Line.Weight = 4;
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
每個單選按鈕都可以作為不同年齡範圍的選擇，連結回同一儲存格 A1。這允許簡單、用戶友好的選擇過程。
## 步驟7：將形狀分組
一切就緒後，讓我們透過對形狀進行分組來整理一切。 
```csharp
//取得形狀。
Aspose.Cells.Drawing.Shape[] shapeobjects = new Shape[] { box, radio1, radio2, radio3 };
//將形狀分組。
Aspose.Cells.Drawing.GroupShape group = excelbook.Worksheets[0].Shapes.Group(shapeobjects);
```
這一步驟將所有內容組合成一個有凝聚力的單元。這就像在你的藝術收藏周圍放置一個框架——它將它們完美地結合在一起！
## 步驟 8：儲存 Excel 文件
最後，讓我們來保存我們的傑作吧！
```csharp
//儲存 Excel 檔案。
excelbook.Save(dataDir + "book1.out.xls");
```
此行程式碼將變更寫入指定目錄中名為「book1.out.xls」的新 Excel 檔案。就像密封信封一樣，您的工作現在已安全存放！
## 結論
現在您已經擁有了使用 Aspose.Cells for .NET 將群組框和單選按鈕新增至 Excel 工作表的完整指南！透過每一步，您都學會如何以程式設計方式操作 Excel，為自訂報告、資料視覺化等的無限可能性打開了大門。程式設計的美妙之處在於您可以相對輕鬆地自動執行任務並創建用戶友好的介面 - 想像一下潛力！
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個 .NET 函式庫，用於管理 Excel 文件，支援以程式設計方式讀取、寫入和操作電子表格等任務。
### 使用 Aspose.Cells 需要編碼經驗嗎？
雖然一些程式設計知識很有幫助，但本教學將引導您完成基礎知識，讓初學者也能輕鬆掌握！
### 我可以自訂組框和按鈕的外觀嗎？
絕對地！ Aspose.Cells 提供了廣泛的形狀樣式選項，包括顏色、大小和 3D 效果。
### Aspose.Cells 是否有免費試用版？
是的！您可以存取免費試用[Aspose免費試用](https://releases.aspose.com/).
### 在哪裡可以找到有關 Aspose.Cells 的更多資源或支援？
這[Aspose 支援論壇](https://forum.aspose.com/c/cells/9)是尋求幫助和與社區分享知識的絕佳場所。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
