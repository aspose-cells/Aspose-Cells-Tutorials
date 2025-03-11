---
title: 使用數據標記圖表建立線條
linktitle: 使用數據標記圖表建立線條
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 在 Excel 中建立帶有資料標記的線條圖表。請按照此逐步指南輕鬆生成和自訂圖表。
weight: 10
url: /zh-hant/net/working-with-chart-data/create-line-with-data-marker-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用數據標記圖表建立線條

## 介紹

您是否想過如何在 Excel 中以程式設計方式建立令人驚嘆的圖表？好吧，請繫好安全帶，因為今天我們將深入研究使用 Aspose.Cells for .NET 建立帶有資料標記圖表的線條。本教學將引導您完成每個步驟，確保您牢牢掌握圖表生成，即使您剛開始使用 Aspose.Cells。

## 先決條件

在我們開始之前，請確保您已準備好一切以便順利進行。

1. Aspose.Cells for .NET Library – 您需要安裝它。你可以抓住它[這裡](https://releases.aspose.com/cells/net/).
2. .NET Framework – 確保您的開發環境設定為最新版本的 .NET。
3. IDE（整合開發環境）- 推薦使用 Visual Studio。
4. 有效的 Aspose.Cells 許可證 – 如果您沒有許可證，您可以申請一份[臨時執照](https://purchase.aspose.com/temporary-license/)或查看他們的[免費試用](https://releases.aspose.com/).

準備好了嗎？讓我們來分解一下吧！

## 導入必要的套件

首先，請確保將以下命名空間匯入到您的專案中。這些將提供創建圖表所需的類別和方法。

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

一旦你把它記下來，我們就可以開始編碼了！

## 第 1 步：設定您的工作簿和工作表

首先，您需要建立一個新工作簿並存取第一個工作表。

```csharp
//輸出目錄
static string outputDir = "Your Document Directory";
		
//實例化工作簿
Workbook workbook = new Workbook();

//訪問第一個工作表
Worksheet worksheet = workbook.Worksheets[0];
```

將工作簿視為 Excel 文件，並將工作表視為其中的特定工作表。在本例中，我們正在處理第一張工作表。

## 步驟 2：用資料填入工作表

現在我們有了工作表，讓我們填入一些資料。我們正在為兩個值系列創建隨機數據點。

```csharp
//設定列標題
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

//用於產生圖表的隨機數據
Random R = new Random();

//創建隨機資料並保存在儲存格中
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

在這裡，我們使用隨機數字來模擬數據，但在現實應用程式中，您可以使用資料集中的實際值來填充它。

## 第 3 步：將圖表新增到工作表中

接下來，我們將圖表新增到工作表中並選擇類型 - 在本例中為帶有資料標記的線條圖表。

```csharp
//將圖表新增至工作表
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

//存取新建立的圖表
Chart chart = worksheet.Charts[idx];
```

此程式碼片段將帶有資料標記的折線圖新增至工作表中，並將其放置在特定範圍（1,3 到 20,20）中。很簡單，對吧？

## 第 4 步：自訂圖表的外觀

建立圖表後，您可以根據自己的喜好設定其樣式。讓我們更改背景、標題和圖表樣式。

```csharp
//設定圖表樣式
chart.Style = 3;

//將自動縮放值設為 true
chart.AutoScaling = true;

//將前景色設定為白色
chart.PlotArea.Area.ForegroundColor = Color.White;

//設定圖表標題屬性
chart.Title.Text = "Sample Chart";

//設定圖表類型
chart.Type = ChartType.LineWithDataMarkers;
```

在這裡，我們透過設定白色背景、自動縮放並賦予其有意義的標題來使圖表看起來乾淨。

## 第 5 步：定義系列並繪製資料點

現在我們的圖表看起來不錯，我們需要定義要繪製的資料系列。

```csharp
//設定類別軸標題的屬性
chart.CategoryAxis.Title.Text = "Units";

//為圖表定義兩個系列
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

這些系列對應於我們先前填入的資料點範圍。

## 第 6 步：新增顏色並自訂系列標記

讓我們透過向資料標記添加自訂顏色來使該圖表更具吸引力。

```csharp
//客製第一個系列
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

//客製化第二系列
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

透過自訂顏色，您可以使圖表不僅具有功能性，而且具有視覺吸引力！

## 步驟 7：為每個系列設定 X 和 Y 值

最後，讓我們為每個系列分配 X 和 Y 值。

```csharp
//設定第一個系列的 X 和 Y 值
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

//設定第二個系列的 X 和 Y 值
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

這些值是基於我們在步驟 2 中填充的資料。

## 第 8 步：儲存工作簿

現在一切都已設定完畢，讓我們儲存工作簿，以便我們可以看到正在運行的圖表。

```csharp
//儲存工作簿
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

就是這樣！您剛剛使用 Aspose.Cells for .NET 建立了一個帶有資料標記的折線圖。

## 結論

在 Excel 中以程式設計方式建立圖表可能看起來令人畏懼，但使用 Aspose.Cells for .NET，這就像遵循逐步食譜一樣簡單。從設定工作簿到自訂圖表外觀，這個強大的庫可以處理這一切。無論您是建立報表、儀表板還是資料視覺化，Aspose.Cells 都可以讓您輕鬆完成。

## 常見問題解答

### 我可以進一步自訂圖表嗎？  
絕對地！ Aspose.Cells 提供了大量的自訂選項，從字體到網格線等等。

### 我需要許可證才能使用 Aspose.Cells 嗎？  
是的，完整功能需要許可證。你可以獲得一個[臨時執照](https://purchase.aspose.com/temporary-license/)或從一個開始[免費試用](https://releases.aspose.com/).

### 如何新增更多數據系列？  
只需使用以下命令添加其他系列`NSeries.Add`方法，指定新資料的單元格範圍。

### 我可以將圖表匯出為圖像嗎？  
是的，您可以使用以下命令將圖表直接匯出為圖像`Chart.ToImage`方法。

### Aspose.Cells 支援 3D 圖表嗎？  
是的，Aspose.Cells 支援多種圖表類型，包括 3D 圖表。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
