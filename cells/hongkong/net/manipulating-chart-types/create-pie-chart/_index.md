---
title: 創建圓餅圖
linktitle: 創建圓餅圖
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過此逐步指南，了解如何使用 Aspose.Cells for .NET 在 Excel 中建立圓餅圖。輕鬆視覺化您的數據。
weight: 12
url: /zh-hant/net/manipulating-chart-types/create-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 創建圓餅圖

## 介紹

創建圖表對於直觀地表示數據至關重要，餅圖是說明各個部分如何構成整體的最受歡迎的方法之一。使用 Aspose.Cells for .NET，您可以輕鬆地在 Excel 檔案中自動產生圓餅圖。在本教程中，我們將深入探討如何使用 Aspose.Cells for .NET 從頭開始建立圓餅圖，並提供逐步指南，使過程順利且簡單。無論您是該工具的新手還是希望提高 Excel 自動化技能，本指南都能滿足您的需求！

## 先決條件

在深入研究程式碼之前，請確保您已進行以下設定：

1.  Aspose.Cells for .NET Library：請確保您的專案中安裝了 Aspose.Cells。如果您還沒有安裝，可以從以下位置下載[這裡](https://releases.aspose.com/cells/net/).
2. .NET 開發環境：確保您的專案設定為使用 .NET Framework 或 .NET Core。
3. C# 基礎知識：您應該熟悉 C# 編程，特別是物件導向編程 (OOP)。

對於高級用戶，可以應用臨時許可證來解鎖 Aspose.Cells 的所有功能。您可以從以下位置索取一份[這裡](https://purchase.aspose.com/temporary-license/).

## 導入包

首先，匯入本教學所需的必要命名空間和套件。其中包括基本的 I/O 操作和 Aspose.Cells 包。

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## 第 1 步：建立新工作簿

首先，我們需要建立一個實例`Workbook`類，代表 Excel 文件。工作簿包含多個工作表，對於我們的範例，我們將使用兩張工作表 - 一張用於數據，一張用於餅圖。

```csharp
Workbook workbook = new Workbook();
```

這將初始化一個新的 Excel 工作簿。但數據去哪了？讓我們在下一步中解決這個問題。

## 第 2 步：將資料新增至工作表

建立工作簿後，我們需要存取第一個工作表並為其命名。我們將在此輸入餅圖所需的資料。

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

現在，我們可以輸入一些代表不同地區的虛擬銷售資料：

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

在這裡，我們新增兩列：一列用於區域，另一列用於銷售資料。該數據將顯示在餅圖中。

## 第 3 步：新增圖表表

接下來，我們新增一個單獨的工作表來儲存圓餅圖。

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

這個新工作表將託管餅圖。為其指定一個名稱（例如「圖表」）可確保使用者知道開啟檔案時會發生什麼。

## 第 4 步：建立餅圖

現在是時候創建實際的圖表了。我們將指定需要一個圓餅圖，並定義它在工作表上的位置。

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

方法`Add()`接受圖表類型的參數（在本例中，`ChartType.Pie`) 及其在工作表上的位置。這些數字代表行和列的位置。

## 第 5 步：自訂圖表外觀

如果沒有一些定制，餅圖就不完整！讓我們透過調整顏色、標籤和標題來使圖表在視覺上更具吸引力。

### 設定圖表標題
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### 自訂繪圖區域
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

我們為繪圖區域設定漸層填滿並隱藏邊框以獲得更清晰的外觀。

## 第 6 步：定義圖表數據

是時候將圖表連結到我們的數據了。這`NSeries`圖表的屬性將銷售數字和區域綁定到圓餅圖。

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

第一行指定我們正在使用儲存格中的銷售數據`B2:B8`。我們也告訴圖表使用來自的區域名稱`A2:A8`作為類別標籤。

## 第 7 步：新增資料標籤

直接向圖表段添加標籤可以使其更易於理解。讓我們在餅圖切片中包含區域名稱和銷售值。

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## 第 8 步：自訂圖表區域和圖例

最後，讓我們對圖表區域和圖例進行最後的修改。這增強了圖表的整體呈現。

### 圖表區
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### 傳奇
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## 第 9 步：儲存工作簿

最後，我們將工作簿儲存到 Excel 檔案。您可以根據需要指定輸出目錄和檔案名稱。

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## 結論

使用 Aspose.Cells for .NET 建立圓餅圖是一個簡單且可自訂的過程。透過遵循本指南，您只需幾個步驟即可產生具有專業外觀的圖表，該圖表可以傳達有價值的見解。無論是用於商業報告還是教育目的，掌握圖表創建都將提高您的 Excel 自動化技能。請記住，Aspose.Cells 提供了您輕鬆建立令人驚嘆的資料驅動 Excel 檔案所需的靈活性。

## 常見問題解答

### 我可以使用 Aspose.Cells for .NET 建立其他類型的圖表嗎？
是的！ Aspose.Cells支援各種圖表類型，包括長條圖、折線圖和散點圖。

### 我需要付費許可證才能使用 Aspose.Cells for .NET 嗎？
您可以使用免費版本，但有一些限制。要獲得完整功能，您需要一個許可證，您可以購買該許可證[這裡](https://purchase.aspose.com/buy).

### 我可以將圖表匯出為 PDF 或圖像等格式嗎？
絕對地！ Aspose.Cells 可讓您將圖表匯出為各種格式，包括 PDF 和 PNG。

### 是否可以為每個餅圖設定不同的顏色？
是的，您可以透過設定為每個切片應用不同的顏色`IsColorVaried`財產給`true`，如教程所示。

### 我可以在單一工作簿中自動產生多個圖表嗎？
是的，您可以在單一 Excel 檔案中根據需要建立和自訂任意數量的圖表。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
