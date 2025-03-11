---
title: 將單選按鈕新增至 Excel 中的工作表
linktitle: 將單選按鈕新增至 Excel 中的工作表
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過這個簡單的逐步指南，了解如何使用 Aspose.Cells for .NET 將單選按鈕新增至 Excel 工作表。非常適合建立互動式 Excel 表單。
weight: 19
url: /zh-hant/net/excel-shapes-controls/add-radio-button-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將單選按鈕新增至 Excel 中的工作表

## 介紹
有沒有想過如何使用單選按鈕等互動式元素為您的 Excel 工作表增添趣味？無論您是要建立調查、表單還是分析工具，新增單選按鈕都可以真正增強使用者互動。在本教學中，我們將引導您完成使用 Aspose.Cells for .NET 將單選按鈕新增至 Excel 工作表的過程。我們將把所有內容分解為易於遵循的步驟，確保您在本文結束時成為專業人士。準備好潛入了嗎？讓我們開始吧！
## 先決條件
在我們開始新增單選按鈕的有趣部分之前，讓我們確保您已完成開始的所有設定。
1.  Aspose.Cells for .NET：首先，請確保您已經下載並安裝了[Aspose.Cells for .NET](https://releases.aspose.com/cells/net/)圖書館.您可以透過 Visual Studio 中的 NuGet 或從下載頁面取得它。
2. IDE（整合開發環境）：您需要像 Visual Studio 這樣的 IDE 來編寫和執行 C# 程式碼。
3. .NET Framework：確保您的電腦上安裝了 .NET Framework 4.0 或更高版本。 Aspose.Cells 需要這個才能工作。
4. 對 C# 的基本了解：熟悉 C# 語法和 .NET 程式設計將使事情變得更容易。
一旦一切準備就緒，我們就可以開始了！
## 導入包
在編碼之前，必須匯入必要的名稱空間，以避免日後出現任何錯誤。將以下內容加入您的程式碼：
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Drawing;
```
這些匯入對於存取工作簿功能、新增單選按鈕和處理文件操作至關重要。
## 第 1 步：設定工作簿
首先，讓我們建立一個新的 Excel 工作簿。
首先，您需要實例化一個新的`Workbook`目的。這將以程式碼形式表示您的 Excel 檔案。
```csharp
//實例化一個新的工作簿。
Workbook excelbook = new Workbook();
```
在此步驟中，您將建立一個空白工作簿。將其想像為空白畫布，您將在後續步驟中新增單選按鈕。
## 步驟 2：新增儲存格值並設定其格式
接下來，讓我們為工作表新增標題。我們將向單元格添加一些文本`C2`並將其格式化為粗體。此步驟為您的單選按鈕新增上下文。
### 在儲存格中插入文字
```csharp
//在儲存格 C2 中插入一個值。
excelbook.Worksheets[0].Cells["C2"].PutValue("Age Groups");
```
### 將文字設為粗體
```csharp
//將儲存格 C2 中的字型文字設定為粗體。
excelbook.Worksheets[0].Cells["C2"].GetStyle().Font.IsBold = true;
```
在這裡，我們在單元格中添加了一個簡單的標題“年齡組”`C2`，並將其加粗以使其脫穎而出。容易，對吧？
## 第 3 步：新增第一個單選按鈕
現在是令人興奮的部分：將您的第一個單選按鈕添加到工作表中！
### 新增單選按鈕
```csharp
//將單選按鈕新增至第一個工作表。
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
```
此行將單選按鈕新增至工作表上的特定位置。數字代表其位置和大小。可以將其想像為設定按鈕的 X 和 Y 座標。
### 設定單選按鈕文字
```csharp
//設定其文字字串。
radio1.Text = "20-29";
```
在這裡，我們為單選按鈕指定了一個標籤“20-29”，代表一個年齡組。
### 將單選按鈕連結到儲存格
```csharp
//將 A1 儲存格設定為單選按鈕的連結儲存格。
radio1.LinkedCell = "A1";
```
這將單選按鈕連結到單元格`A1`，這意味著按鈕選擇的結果將儲存在該儲存格中。
### 加入 3D 效果
```csharp
//將單選按鈕設為 3D。
radio1.Shadow = true;
```
因為我們希望這個單選按鈕彈出，所以我們添加了 3D 效果。
### 自訂單選按鈕的行
```csharp
//設定單選按鈕線的粗細。
radio1.Line.Weight = 4;
//設定單選按鈕線的破折號樣式。
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
這些程式碼行調整單選按鈕邊框的粗細和破折號樣式，使其更具視覺吸引力。
## 第 4 步：新增其他單選按鈕
讓我們為剩餘的年齡組添加兩個單選按鈕：「30-39」和「40-49」。步驟是相同的，只是座標和標籤略有不同。
### 新增第二個單選按鈕
```csharp
//將另一個單選按鈕新增到第一個工作表。
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
//設定其文字字串。
radio2.Text = "30-39";
//將 A1 儲存格設定為單選按鈕的連結儲存格。
radio2.LinkedCell = "A1";
//將單選按鈕設為 3D。
radio2.Shadow = true;
//設定單選按鈕的權重。
radio2.Line.Weight = 4;
//設定單選按鈕的破折號樣式。
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
```
### 新增第三個單選按鈕
```csharp
//將另一個單選按鈕新增到第一個工作表。
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
//設定其文字字串。
radio3.Text = "40-49";
//將 A1 儲存格設定為單選按鈕的連結儲存格。
radio3.LinkedCell = "A1";
//將單選按鈕設為 3D。
radio3.Shadow = true;
//設定單選按鈕的權重。
radio3.Line.Weight = 4;
//設定單選按鈕的破折號樣式。
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
## 第 5 步：儲存 Excel 文件
新增所有單選按鈕並設定格式後，就可以儲存檔案了。
```csharp
//儲存 Excel 檔案。
string dataDir = "Your Document Directory";
excelbook.Save(dataDir + "book1.out.xls");
```
在此步驟中，工作簿將會儲存到您指定的目錄中。就是這麼簡單 - 您的互動式工作表現已準備就緒！
## 結論
給你了！您剛剛使用 Aspose.Cells for .NET 將單選按鈕新增至 Excel 工作表。本教學涵蓋了從設定工作簿、插入和格式化值、新增多個單選按鈕以及將它們連結到儲存格的所有內容。現在，您已準備好建立互動式 Excel 工作表，它們不僅看起來很棒，而且還提供增強的使用者體驗。祝您使用 Aspose.Cells 探索更多可能性！
## 常見問題解答
### 我可以為不同的工作表添加更多單選按鈕嗎？  
絕對地！您可以透過指定正確的工作表索引在工作簿中的任何工作表上重複此程序。
### 我可以進一步自訂單選按鈕的外觀嗎？  
是的，Aspose.Cells 提供了多種自訂選項，包括更改顏色、大小和其他格式屬性。
### 如何偵測選擇了哪個單選按鈕？  
連結的儲存格（例如，A1）將顯示所選單選按鈕的索引。您可以檢查連結儲存格的值以了解選擇了哪一個儲存格。
### 我可以新增的單選按鈕數量有限制嗎？  
不，您可以新增的單選按鈕的數量沒有硬性限制。然而，保持介面用戶友好是件好事。
### 我可以將 Aspose.Cells 與其他程式語言一起使用嗎？  
是的，Aspose.Cells 支援多種程式語言，包括 Java。但本教學特別關注 .NET。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
