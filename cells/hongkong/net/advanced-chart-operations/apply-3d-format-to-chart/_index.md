---
title: 將 3D 格式應用於圖表
linktitle: 將 3D 格式應用於圖表
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 在 Excel 中建立令人驚嘆的 3D 圖表。請遵循我們簡單的逐步指南。
weight: 10
url: /zh-hant/net/advanced-chart-operations/apply-3d-format-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將 3D 格式應用於圖表

## 介紹

在資料視覺化至關重要的時代，我們呈現資料的方式超越了基本的圖形和圖表。透過 Aspose.Cells for .NET 等工具，您可以使用令人驚嘆的 3D 圖表來提升數據演示，這些圖表不僅能吸引註意力，還能有效地傳達訊息。本指南將引導您使用 Aspose.Cells 將 3D 格式應用於圖表的步驟，將原始資料轉換為引人入勝的顯示。

## 先決條件

在我們深入研究將 3D 格式應用於圖表的細節之前，讓我們確保您擁有所需的一切。

### 軟體需求

- Visual Studio：確保安裝了 Visual Studio 以使用 .NET 應用程式。
-  Aspose.Cells for .NET：如果您還沒有安裝 Aspose.Cells，請從[這裡](https://releases.aspose.com/cells/net/).

### 編碼環境設定

1. 建立新的 .NET 專案：開啟 Visual Studio，選擇“建立新專案”，然後選擇控制台應用程式。
2. 新增 Aspose.Cells 參考：透過 NuGet Package Manager，透過搜尋或透過 Package Manager Console 新增 Aspose.Cells：

```bash
Install-Package Aspose.Cells
```

3. 設定輸出目錄：指定將儲存產生的檔案的輸出目錄 - 這就像在桌面上建立資料夾一樣簡單。

現在您已完成所有設置，是時候開始編寫程式碼並創建一些令人眼花繚亂的 3D 圖表了！

## 導入包

首先，您需要匯入必要的命名空間。這將幫助您存取 Aspose.Cells 提供的類別和方法。操作方法如下：

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

本節將把該流程分解為可管理的步驟，讓您清楚地了解每個階段。

## 第 1 步：初始化您的工作簿

首先，您需要建立一個實例`Workbook`班級。該物件將作為 Excel 文件的基礎。

```csharp
//輸出目錄
string outputDir = "Your Document Directory";
Workbook book = new Workbook();
```
想想這個`Workbook`作為一塊空白畫布，您可以用豐富多彩的數據和有影響力的視覺化來填充它。

## 第 2 步：重新命名第一個工作表

接下來，讓我們重新命名第一個工作表。這讓我們清楚地了解我們正在使用哪些數據。

```csharp
book.Worksheets[0].Name = "DataSheet";
```

名稱應該直觀。在本例中，我們將其命名為“DataSheet”，以便我們知道資料所在的位置。

## 第 3 步：為圖表建立數據

現在，我們將向「數據表」添加一些數據。讓我們用圖表將使用的值填充它。

```csharp
Worksheet dataSheet = book.Worksheets["DataSheet"];
dataSheet.Cells["B1"].PutValue(1);
dataSheet.Cells["B2"].PutValue(2);
dataSheet.Cells["B3"].PutValue(3);
dataSheet.Cells["A1"].PutValue("A");
dataSheet.Cells["A2"].PutValue("B");
dataSheet.Cells["A3"].PutValue("C");
```

就像食譜取決於成分一樣，圖表的有效性也取決於輸入資料的品質和組織。

## 第 4 步：設定新的圖表工作表

是時候為圖表本身建立一個新的工作表了。這有助於讓您的資料視覺化井井有條。

```csharp
Worksheet sheet = book.Worksheets.Add("MyChart");
```

將此工作表視為您的舞台－數據表現在此展現。

## 第 5 步：新增圖表

在這裡，我們將向新建立的工作表添加長條圖。  

```csharp
ChartCollection charts = sheet.Charts;
int chartSheetIdx = charts.Add(ChartType.Column, 5, 0, 25, 15);
```

我們正在為圖表定義一個空間並指定它的類型。只需將其視為為您的藝術品選擇框架類型即可。

## 第 6 步：自訂圖表外觀

現在，讓我們透過設定背景顏色來自訂圖表的外觀。 

```csharp
Aspose.Cells.Charts.Chart chart = book.Worksheets["MyChart"].Charts[0];
chart.PlotArea.Area.BackgroundColor = Color.White;
chart.ChartArea.Area.BackgroundColor = Color.White;
chart.PlotArea.Area.ForegroundColor = Color.White;
chart.ChartArea.Area.ForegroundColor = Color.White;
chart.ShowLegend = false;
```

乾淨的白色背景通常會使數據的顏色脫穎而出，從而提高可視性。

## 第 7 步：將資料系列新增至圖表中

是時候為我們的圖表提供數據了。我們將從「資料表」中新增一個資料系列，以確保我們的圖表反映我們需要的資料。

```csharp
chart.NSeries.Add("DataSheet!B1:B3", true);
chart.NSeries.CategoryData = "DataSheet!A1:A3";
```

這類似於廚師用特定食材準備菜餚。每個數據點都很重要！

## 步驟 8：存取並格式化資料系列

現在我們已經連結了數據，讓我們取得數據系列並開始應用一些 3D 效果。

```csharp
Aspose.Cells.Charts.Series ser = chart.NSeries[0];
ShapePropertyCollection spPr = ser.ShapeProperties;
Format3D fmt3d = spPr.Format3D;
```

我們正準備為我們的菜餚添加一些風味——將其視為增強整體風味的調味料。

## 第 9 步：應用 3D 斜角效果

接下來，我們將添加斜角效果以使圖表具有一定的尺寸。

```csharp
Bevel bevel = fmt3d.TopBevel;
bevel.Type = BevelPresetType.Circle;
bevel.Height = 2;
bevel.Width = 5;
```

就像雕刻家塑造石頭一樣，我們正在創造深度，使我們的圖表變得生動！

## 第10步：定製表面材質和燈光

讓我們的圖表閃閃發光！我們將調整表面材質和照明設定。

```csharp
fmt3d.SurfaceMaterialType = PresetMaterialType.WarmMatte;
fmt3d.SurfaceLightingType = LightRigType.ThreePoint;
fmt3d.LightingAngle = 20;
```

適當的照明和材料可以將平面物體轉變成迷人的視覺效果。想像一下經過專業照明以增強每個場景的電影佈景。

## 第11步：系列外觀的最後潤飾

現在透過調整顏色來最終確定資料系列的外觀。

```csharp
ser.Area.BackgroundColor = Color.Maroon;
ser.Area.ForegroundColor = Color.Maroon;
ser.Border.Color = Color.Maroon;
```

正確的顏色可以喚起一定的感覺和反應——栗色增添了一絲優雅和精緻。

## 第 12 步：儲存您的工作簿

最後，是時候保存你的傑作了！不要忘記指定要儲存它的目的地。

```csharp
book.Save(outputDir + "outputApplying3DFormat.xlsx");
Console.WriteLine("Applying3DFormat executed successfully.");
```

保存您的作品就像將您的藝術品放入畫廊一樣；這是一個值得珍惜與分享的時刻。

## 結論

恭喜！您已使用 Aspose.Cells for .NET 成功建立了具有視覺吸引力的 3D 圖表。透過執行這些步驟，您現在擁有了一個強大的工具來增強您的數據演示，使其不僅資訊豐富，而且在視覺上引人入勝。當您完善圖表時，請記住每個視覺化都是一個故事 - 使其引人入勝、清晰且具有影響力！

## 常見問題解答

### 什麼是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一個功能強大的函式庫，可讓開發人員以程式設計方式操作 Excel 文檔，包括建立圖表和圖表。

### 我可以在 Aspose.Cells 中自訂圖表類型嗎？
是的！ Aspose.Cells 支援各種圖表類型，如長條圖、折線圖、圓餅圖等，可以輕鬆自訂。

### Aspose.Cells 是否有免費試用版？
絕對地！您可以從以下位置下載免費試用版[這裡](https://releases.aspose.com/).

### 除了 3D 格式之外，我還可以對圖表套用其他效果嗎？
是的，您可以套用陰影、漸層和不同樣式等各種效果來增強 3D 以外的圖表。

### 在哪裡可以找到對 Aspose.Cells 的支援？
如需支持，您可以訪問[Aspose論壇](https://forum.aspose.com/c/cells/9)尋求社區的幫助和幫助。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
