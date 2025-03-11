---
title: 在 Excel 中將形狀傳送到正面或背面
linktitle: 在 Excel 中將形狀傳送到正面或背面
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 在 Excel 中將形狀傳送到前面或後面。本指南提供了帶有提示的分步教程。
weight: 16
url: /zh-hant/net/excel-shape-text-modifications/send-shape-front-back-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中將形狀傳送到正面或背面

## 介紹
使用 Excel 檔案時，您可能會發現自己需要對電子表格中的視覺元素進行更多控制。形狀（如影像和圖形）可以增強資料的呈現效果。但是當這些形狀重疊或需要重新排序時會發生什麼？這就是 Aspose.Cells for .NET 的閃光點。在本教學中，我們將引導您完成在 Excel 工作表中操作形狀的步驟，特別是將形狀傳送到其他形狀的前面或後面。如果您已準備好增強您的 Excel 遊戲能力，那麼就讓我們開始吧！
## 先決條件
在我們開始之前，您需要準備好一些東西：
1.  Aspose.Cells 函式庫的安裝：確保您已安裝適用於.NET 的Aspose.Cells 函式庫。你可以找到它[這裡](https://releases.aspose.com/cells/net/).
2. 開發環境：確保您設定了支援 .NET 的開發環境，例如 Visual Studio。
3. C# 基礎知識：熟悉 C# 程式設計將有助於您更好地理解程式碼片段。
好的，您已經勾選了先決條件清單上的所有方塊嗎？偉大的！讓我們繼續有趣的部分——編寫一些程式碼！
## 導入包
在我們深入實際編碼之前，讓我們先導入必要的套件。只需在 C# 檔案頂部添加以下 using 指令：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
這些命名空間至關重要，因為它們包含我們將用來操作 Excel 檔案和形狀的類別和方法。
## 第 1 步：定義檔路徑
在第一步中，我們需要建立來源目錄和輸出目錄。這是 Excel 檔案所在的位置，也是您要儲存修改後的檔案的位置。
```csharp
//原始碼目錄
string sourceDir = "Your Document Directory";
//輸出目錄
string outputDir = "Your Document Directory";
```
代替`"Your Document Directory"`與儲存 Excel 檔案的實際路徑。
## 第 2 步：載入工作簿
現在我們已經設定了目錄，讓我們載入包含我們要操作的形狀的工作簿（Excel 檔案）。
```csharp
//載入來源 Excel 文件
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
這行程式碼初始化一個新的`Workbook`對象，將指定的 Excel 檔案載入到記憶體中，以便我們可以使用它。
## 第 3 步：訪問工作表 
接下來，我們需要存取形狀所在的特定工作表。對於本範例，我們將使用第一個工作表。
```csharp
//訪問第一個工作表
Worksheet ws = wb.Worksheets[0];
```
透過引用`Worksheets[0]`，我們的目標是工作簿的第一張工作表。如果您的形狀位於不同的紙張上，請相應地調整索引。
## 第 4 步：存取形狀
準備好存取工作表後，讓我們取得我們感興趣的形狀。
```csharp
//訪問第一個和第四個形狀
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
這些線根據其索引從工作表中取得特定形狀。
## 步驟 5：列印形狀的 Z 順序位置
在移動任何形狀之前，讓我們先列印它們目前的 Z 順序位置。這有助於我們在做出改變之前追蹤他們的定位。
```csharp
//列印形狀的 Z 順序位置
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
透過致電`ZOrderPosition`，我們可以看到每個形狀在繪製順序中的位置。
## 第 6 步：將第一個形狀送到前面
現在是採取行動的時候了！讓我們將第一個形狀送到 Z 順序的前面。
```csharp
//將此形狀發送到前面
sh1.ToFrontOrBack(2);
```
透過`2`到`ToFrontOrBack`，我們指示 Aspose.Cells 將此形狀置於前面。 
## 步驟 7：列印第二個形狀的 Z 順序位置
在我們將第二個形狀發送到後面之前，讓我們檢查一下它的位置。
```csharp
//列印形狀的 Z 順序位置
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
這使我們可以在進行任何更改之前了解第四個形狀的位置。
## 步驟8：將第四個形狀放在後面
最後，我們將把第四個形狀送到 Z 順序堆疊的後面。
```csharp
//將此形狀發送到後面
sh4.ToFrontOrBack(-2);
```
使用`-2`當參數將形狀發送到堆疊的後面時，請確保它不會阻礙其他形狀或文字。
## 第 9 步：儲存工作簿 
最後一步是使用新定位的形狀來儲存工作簿。
```csharp
//儲存輸出的 Excel 文件
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
此指令將修改後的工作簿儲存到指定的輸出目錄。
## 第10步：確認訊息
最後，讓我們提供一個簡單的確認，讓我們知道我們的任務已成功完成。
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
這就是我們教學的程式碼了！
## 結論
使用 Aspose.Cells for .NET 在 Excel 中操作形狀不僅簡單且功能強大。透過遵循本指南，您現在應該能夠輕鬆地將形狀發送到前面或後面，從而更好地控制您的 Excel 簡報。有了這些可用的工具，您就可以增強電子表格的視覺吸引力。
## 常見問題解答
### Aspose.Cells 需要什麼程式語言？  
您需要使用 C# 或任何 .NET 支援的語言才能使用 Aspose.Cells。
### 可以免費試用 Aspose.Cells 嗎？  
是的，您可以從免費試用 Aspose.Cells 開始[這裡](https://releases.aspose.com/).
### 我可以在 Excel 中操作哪些形狀？  
您可以操縱各種形狀，例如矩形、圓形、線條和圖像。
### 我如何獲得 Aspose.Cells 的支援？  
您可以訪問他們的社區論壇以獲得任何支持或疑問[這裡](https://forum.aspose.com/c/cells/9).
### Aspose.Cells 是否有可用的臨時許可證？  
是的，您可以申請臨時許可證[這裡](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
