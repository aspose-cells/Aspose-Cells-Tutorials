---
"description": "了解如何使用 Aspose.Cells for .NET 在 Excel 中建立帶有資料標記的線圖。按照本逐步指南輕鬆生成和自訂圖表。"
"linktitle": "建立帶有資料標記的線條圖"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "建立帶有資料標記的線條圖"
"url": "/zh-hant/net/working-with-chart-data/create-line-with-data-marker-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 建立帶有資料標記的線條圖

## 介紹

您是否想過如何以程式設計方式在 Excel 中創建令人驚嘆的圖表？好吧，請繫好安全帶，因為今天我們將深入研究使用 Aspose.Cells for .NET 建立帶有資料標記圖表的線條。本教學將引導您完成每個步驟，確保您牢牢掌握圖表生成，即使您剛開始使用 Aspose.Cells。

## 先決條件

在我們開始之前，請確保一切準備就緒，以便順利進行。

1. Aspose.Cells for .NET Library – 您需要安裝它。你可以抓住它 [這裡](https://releases。aspose.com/cells/net/).
2. .NET Framework – 確保您的開發環境設定了最新版本的 .NET。
3. IDE（整合開發環境）－建議使用 Visual Studio。
4. 有效的 Aspose.Cells 許可證 – 如果您沒有，您可以申請 [臨時執照](https://purchase.aspose.com/temporary-license/) 或查看他們的 [免費試用](https://releases。aspose.com/).

準備出發了嗎？讓我們來分解一下！

## 導入必要的套件

首先，請確保將以下命名空間匯入到您的專案中。這些將提供創建圖表所需的類別和方法。

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

一旦你搞定了這些，我們就可以開始編碼了！

## 步驟 1：設定工作簿和工作表

首先，您需要建立一個新的工作簿並存取第一個工作表。

```csharp
//輸出目錄
static string outputDir = "Your Document Directory";
		
// 實例化工作簿
Workbook workbook = new Workbook();

// 訪問第一個工作表
Worksheet worksheet = workbook.Worksheets[0];
```

將工作簿視為 Excel 文件，並將工作表視為其中的特定工作表。在這種情況下，我們正在處理第一張表。

## 步驟 2：用資料填入工作表

現在我們有了工作表，讓我們用一些資料填入它。我們正在為兩個系列的值創建隨機數據點。

```csharp
// 設定列標題
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// 用於產生圖表的隨機數據
Random R = new Random();

// 創建隨機資料並保存在儲存格中
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

在這裡，我們使用隨機數字來模擬數據，但在實際應用中，您可以使用資料集中的實際值來填充它。

## 步驟 3：將圖表新增至工作表

接下來，我們將圖表新增至工作表並選擇類型 - 在本例中為帶有資料標記的折線圖。

```csharp
// 在工作表中新增圖表
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// 存取新建立的圖表
Chart chart = worksheet.Charts[idx];
```

此程式碼片段將帶有資料標記的折線圖新增至工作表，並將其放置在特定範圍內（1,3 到 20,20）。很簡單，對吧？

## 步驟 4：自訂圖表的外觀

建立圖表後，您可以根據自己的喜好設定其樣式。讓我們改變背景、標題和圖表樣式。

```csharp
// 設定圖表樣式
chart.Style = 3;

// 將自動縮放值設為 true
chart.AutoScaling = true;

// 將前景色設定為白色
chart.PlotArea.Area.ForegroundColor = Color.White;

// 設定圖表標題屬性
chart.Title.Text = "Sample Chart";

// 設定圖表類型
chart.Type = ChartType.LineWithDataMarkers;
```

在這裡，我們透過設定白色背景、自動縮放並賦予其有意義的標題來使圖表看起來整潔。

## 步驟 5：定義序列並繪製資料點

現在我們的圖表看起來不錯，我們需要定義將要繪製的資料系列。

```csharp
// 設定分類軸標題的屬性
chart.CategoryAxis.Title.Text = "Units";

// 為圖表定義兩個系列
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

這些系列對應於我們先前填入的資料點範圍。

## 步驟 6：新增顏色並自訂系列標記

讓我們透過向資料標記添加自訂顏色來使該圖表更具吸引力。

```csharp
// 客製第一個系列
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// 客製化第二系列
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

透過自訂顏色，您可以使圖表不僅具有功能性，而且具有視覺吸引力！

## 步驟 7：設定每個系列的 X 和 Y 值

最後，讓我們為每個系列分配 X 和 Y 值。

```csharp
// 設定第一個系列的 X 和 Y 值
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// 設定第二個系列的 X 和 Y 值
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

這些值是基於我們在步驟 2 中填充的資料。

## 步驟 8：儲存工作簿

現在一切都已設定好，讓我們儲存工作簿，以便我們可以看到圖表的運作情況。

```csharp
// 儲存工作簿
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

就是這樣！您剛剛使用 Aspose.Cells for .NET 建立了帶有資料標記的折線圖。

## 結論

在 Excel 中以程式設計方式建立圖表可能看起來很困難，但使用 Aspose.Cells for .NET，它就像按照逐步食譜一樣簡單。從設定工作簿到自訂圖表外觀，這個強大的庫可以處理一切。無論您是建立報表、儀表板還是資料視覺化，Aspose.Cells 都能讓您輕鬆完成。

## 常見問題解答

### 我可以進一步自訂圖表嗎？  
絕對地！ Aspose.Cells 提供了大量自訂選項，從字體到網格線等等。

### 我需要許可證才能使用 Aspose.Cells 嗎？  
是的，需要許可證才能使用全部功能。您可以獲得 [臨時執照](https://purchase.aspose.com/temporary-license/) 或者從 [免費試用](https://releases。aspose.com/).

### 我如何添加更多數據系列？  
只需使用 `NSeries.Add` 方法，指定新資料的單元格範圍。

### 我可以將圖表匯出為圖像嗎？  
是的，您可以使用 `Chart.ToImage` 方法。

### Aspose.Cells 支援 3D 圖表嗎？  
是的，Aspose.Cells 支援多種圖表類型，包括 3D 圖表。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}