---
title: 加入連接點的弧控制
linktitle: 加入連接點的弧控制
second_title: Aspose.Cells .NET Excel 處理 API
description: 在此詳細指南中了解如何使用 Aspose.Cells for .NET 新增帶有連接點的弧形控制項。
weight: 27
url: /zh-hant/net/excel-shapes-controls/add-arc-control-with-connection-points/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 加入連接點的弧控制

## 介紹
在創建具有視覺吸引力的 Excel 報告時，插圖起著至關重要的作用。無論您是在製作財務報告還是專案分解，使用弧線等形狀都可以增加資料簡報的深度和清晰度。今天，我們將深入探討如何利用 Aspose.Cells for .NET 在 Excel 工作表中新增帶有連接點的弧形控制項。因此，如果您想知道如何為電子表格增添趣味或讓數據動起來，請繼續閱讀！
## 先決條件
在我們開始激動人心的編碼之前，讓我們先確保您已做好準備。這是您需要的：
1. .NET Framework：確保您安裝了相容版本。 Aspose.Cells 適用於多個版本，包括 .NET Core。
2.  Aspose.Cells for .NET：您需要下載並安裝 Aspose.Cells 函式庫。您可以輕鬆地從[下載連結](https://releases.aspose.com/cells/net/).
3. 一個好的 IDE：Visual Studio 是任何 .NET 開發人員的忠實夥伴，將幫助簡化您的程式設計體驗。
4. C# 基礎：如果您熟悉 C#，您會發現本教學很順利。
5. 存取文件目錄：了解 Excel 檔案的儲存位置。這對於有效組織輸出至關重要。
## 導入包
下一步是確保您將正確的套件匯入到您的專案中。 Aspose.Cells for .NET 具有多種功能，因此我們將保持簡單。以下是您需要包含的內容：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
這些命名空間將使您能夠存取本指南中將使用的所有繪圖功能和儲存格管理功能。
## 第 1 步：設定您的文件目錄
首先，讓我們建立一個目錄來保存這些閃亮的新 Excel 檔案。我們是這樣做的：
```csharp
string dataDir = "Your Document Directory";
//如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
這段程式碼檢查您指定的資料夾是否存在。如果沒有，它就會創建一個。很簡單，對吧？為文件指定一個特定的位置以避免混亂總是好的。
## 第 2 步：實例化工作簿
現在我們已經準備好了目錄，讓我們建立一個新的 Excel 工作簿。
```csharp
Workbook excelbook = new Workbook();
```
透過致電`Workbook`建構函數，您實際上是在說：“嘿，讓我們開始一個新的 Excel 文件！”這將是所有形狀和數據的畫布。
## 第 3 步：新增第一個圓弧形狀
這就是樂趣的開始！讓我們加入第一個弧形。
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
這行程式碼在第一個工作表新增了一個圓弧形狀。這些參數指定圓弧的座標和定義其曲率的角度。 
## 第 4 步：自訂圓弧的外觀
空白的弧形就像沒有油漆的畫布一樣——它需要一點天賦！
### 設定圓弧填滿顏色
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
這使得弧線變成純藍色。您可以透過交換將顏色變更為您喜歡的任何色調`Color.Blue`換另一種顏色。
### 設定圓弧放置
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
將放置設定為“FreeFloating”允許圓弧獨立於單元格邊界移動，從而使您可以靈活定位。
### 調整線寬和样式
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
在這裡，您可以定義線條的粗細和樣式，使其更加突出且更具視覺吸引力。
## 第 5 步：新增另一個弧形
為什麼停在一個？讓我們加入另一個弧形來豐富我們的 Excel 視覺效果。
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
與第一個弧線一樣，這條弧線被添加到不同的位置——這就是設計的魔力發生的地方！
## 第 6 步：自訂第二條弧線
讓我們也給我們的第二條弧線一些個性吧！
### 改變弧線顏色
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
我們將其與藍色保持一致，但您可以隨時混合搭配，看看什麼最適合您的設計！
### 設定與第一條弧類似的屬性
確保複製這些美學選擇：
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
在這裡，您只需確保第二個弧與第一個弧匹配，從而在整個工作表中創建一個有凝聚力的外觀。
## 第 7 步：儲存您的工作簿
沒有保存下來的傑作是不完整的，對嗎？是時候將弧寫入 Excel 檔案了。
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
此行將新建立的弧儲存到指定目錄中名為「book1.out.xls」的 Excel 檔案。
## 結論
恭喜！您剛剛掌握了使用 Aspose.Cells for .NET 在 Excel 工作表中新增帶有連接點的弧形控制項的基礎知識。此功能不僅可以美化您的電子表格，還可以使複雜的數據更易於理解。無論您是經驗豐富的開發人員還是新手，這些視覺元素都可以將您的報告從平淡無奇變為宏偉。
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的.NET 程式庫，可讓開發人員以程式設計方式建立和操作 Excel 檔案。
### 我可以免費使用 Aspose.Cells 嗎？
是的！您可以嘗試免費試用。訪問[這個連結](https://releases.aspose.com/)開始。
### 除了圓弧之外，如何添加其他形狀？
您可以使用 Aspose.Cells.Drawing 命名空間中提供的不同類別來新增各種形狀，例如矩形、圓形等。
### 我可以使用 Aspose.Cells 建立什麼類型的檔案？
您可以建立和操作各種 Excel 格式，包括 XLS、XLSX、CSV 等。
### Aspose.Cells 是否提供技術支援？
絕對地！您可以訪問[Aspose 支援論壇](https://forum.aspose.com/c/cells/9)尋求幫助。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
