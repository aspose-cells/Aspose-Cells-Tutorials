---
title: 將圓弧新增至 Excel 中的工作表
linktitle: 將圓弧新增至 Excel 中的工作表
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解使用 Aspose.Cells for .NET 將弧新增至 Excel 工作表。請按照我們的逐步指南來增強您的電子表格設計。
weight: 16
url: /zh-hant/net/excel-shapes-controls/add-arc-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將圓弧新增至 Excel 中的工作表

## 介紹
建立具有視覺吸引力的 Excel 電子表格對於資料呈現至關重要，Aspose.Cells 庫為開發人員提供了完成此任務的強大工具。您可能想要將其合併到 Excel 文件中的一項有趣功能是新增形狀（例如圓弧）的能力。在本教學中，我們將逐步介紹如何使用 Aspose.Cells for .NET 將弧新增至 Excel 工作表。在本文結束時，您不僅將學習如何添加圓弧，還將深入了解一般形狀的管理。
## 先決條件
在我們深入研究為工作表添加弧的複雜性之前，必須確保您已做好一些準備。以下是您開始使用所需的先決條件：
1. Visual Studio：您需要在電腦上安裝 Visual Studio，因為我們將使用 C# 作為程式語言。
2. .NET Framework：確保已安裝 .NET Framework 或 .NET Core。 Aspose.Cells 兩者都支援。
3. Aspose.Cells for .NET：您必須擁有 Aspose.Cells 函式庫。您可以從[Aspose.Cells 下載](https://releases.aspose.com/cells/net/)頁。
4. 對 C# 的基本了解：熟悉 C# 將幫助您輕鬆理解程式碼片段。
## 導入包
要開始在專案中使用 Aspose.Cells，您需要匯入必要的套件。操作方法如下：
### 建立一個新項目
- 打開視覺工作室。
- 選擇“建立新項目”。
- 選擇適用於 .NET 的範本（例如控制台應用程式）。
  
### 新增 Aspose.Cells 引用
- 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
- 選擇“管理 NuGet 套件”。
- 搜尋“Aspose.Cells”並安裝它。
現在您已準備好開始編寫圓弧加法的程式碼。
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
以下是程式碼的分步細分，示範如何將圓弧新增至 Excel 中的工作表。
## 第 1 步：設定目錄
第一步是設定一個用於儲存 Excel 檔案的目錄。這有助於輕鬆管理輸出檔案。
```csharp
string dataDir = "Your Document Directory";
//如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
在此程式碼片段中，我們指定文檔目錄的路徑。我們也檢查該目錄是否存在；如果沒有，我們就創建它。這為我們的輸出奠定了基礎。
## 第 2 步：實例化工作簿
接下來，讓我們建立一個新的工作簿實例。
```csharp
//實例化一個新的工作簿。
Workbook excelbook = new Workbook();
```
此行建立一個新的 Excel 工作簿。將其視為空白畫布，我們可以在其中添加形狀、數據等。
## 第 3 步：新增第一個弧形
現在，讓我們將第一個圓弧形狀新增到工作表中。
```csharp
//添加弧形。
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
在這裡，我們為第一個工作表新增一條弧。參數定義圓弧的位置和大小：`(left, top, width, height, startAngle, endAngle)`。這就像繪製圓的一部分！
## 第 4 步：自訂第一條弧線
添加弧線後，您可能想要自訂其外觀。
```csharp
//設定填滿形狀顏色
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
//設定圓弧的位置。
arc1.Placement = PlacementType.FreeFloating;           
//設定線寬。
arc1.Line.Weight = 1;      
//設定圓弧的虛線樣式。
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
在本節中，我們將自訂弧線。我們將其填滿類型設為純色（在本例中為藍色），定義其放置方式，建立線寬，並選擇虛線樣式。基本上，我們正在修飾我們的弧線，使其在視覺上更有吸引力！
## 第 5 步：新增第二個弧形
讓我們添加另一個弧形以提供更多上下文。
```csharp
//添加另一個弧形。
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
與第一條弧類似，我們在同一工作表上新增第二個弧。這裡的座標稍微移動了一點，以不同的方式定位它。
## 第 6 步：自訂第二條弧線
就像我們對第一個弧線所做的那樣，我們也將自訂第二個弧線。
```csharp
//設定線條顏色
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
//設定圓弧的位置。
arc2.Placement = PlacementType.FreeFloating;          
//設定線寬。
arc2.Line.Weight = 1;           
//設定圓弧的虛線樣式。
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
在這裡，我們為第二條弧線賦予與第一條弧線相同的樣式。您可以根據需要更改顏色或樣式，以實現獨特性或主題目的。
## 第 7 步：儲存工作簿
最後，是時候儲存新建立的帶有弧線的工作簿了。
```csharp
//儲存 Excel 檔案。
excelbook.Save(dataDir + "book1.out.xls");
```
這行程式碼的作用就像點擊儲存按鈕一樣。我們正在使用指定的檔案名稱將工作儲存到指定位置。請務必檢查您的目錄以查看 Excel 格式的傑作！
## 結論
在本教學中，我們探索了使用 Aspose.Cells for .NET 將弧形新增至 Excel 工作表的流程。透過簡單的逐步指南，您已經了解如何建立新工作簿、新增弧線、自訂其外觀以及儲存文件。此功能不僅增強了電子表格的視覺吸引力，還使您的數據演示更加豐富。無論您是要建立圖表、報告還是只是進行試驗，使用弧形等形狀都可以為您的專案增添創意。
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的程式庫，可讓開發人員以程式設計方式建立、操作和轉換 Excel 文件，而無需 Microsoft Excel。
### 我需要安裝 Microsoft Excel 才能使用 Aspose.Cells 嗎？
不需要，Aspose.Cells 是完全獨立的，不需要安裝 Microsoft Excel。
### 可以免費試用 Aspose.Cells 嗎？
是的，您可以使用 Aspose.Cells 來嘗試[免費試用](https://releases.aspose.com/).
### Aspose.Cells 支援哪些程式語言？
Aspose.Cells支援多種語言，包括C#、VB.NET等。
### 我可以在哪裡獲得 Aspose.Cells 的支援？
您可以透過以下方式獲得支持[Aspose論壇](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
