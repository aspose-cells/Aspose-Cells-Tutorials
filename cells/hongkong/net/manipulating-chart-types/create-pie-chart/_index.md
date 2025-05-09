---
"description": "透過本逐步指南了解如何使用 Aspose.Cells for .NET 在 Excel 中建立圓餅圖。輕鬆實現數據視覺化。"
"linktitle": "創建圓餅圖"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "創建圓餅圖"
"url": "/zh-hant/net/manipulating-chart-types/create-pie-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 創建圓餅圖

## 介紹

建立圖表對於直觀地呈現資料至關重要，而圓餅圖是說明各部分如何組成整體的最受歡迎方式之一。使用 Aspose.Cells for .NET，您可以輕鬆地自動產生 Excel 檔案中的圓餅圖。在本教程中，我們將深入探討如何使用 Aspose.Cells for .NET 從頭開始建立圓餅圖，並提供逐步指南以使該過程順暢而直接。無論您是剛使用該工具還是希望提高您的 Excel 自動化技能，本指南都能滿足您的需求！

## 先決條件

在深入研究程式碼之前，請確保已進行以下設定：

1. Aspose.Cells for .NET Library：請確保您的專案中安裝了 Aspose.Cells。如果你還沒有安裝，你可以從 [這裡](https://releases。aspose.com/cells/net/).
2. .NET 開發環境：確保您的專案設定為使用 .NET Framework 或 .NET Core。
3. C# 基礎知識：您應該熟悉 C# 編程，尤其是物件導向編程 (OOP)。

對於高級用戶，可以申請臨時許可證來解鎖 Aspose.Cells 的所有功能。您可以從 [這裡](https://purchase。aspose.com/temporary-license/).

## 導入包

首先，匯入本教學所需的必要命名空間和套件。這些包括基本的 I/O 操作和 Aspose.Cells 包。

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## 步驟 1：建立新工作簿

首先，我們需要創建一個 `Workbook` 類，代表 Excel 文件。一個工作簿包含多個工作表，在我們的範例中，我們將使用兩個工作表 - 一個用於數據，一個用於餅圖。

```csharp
Workbook workbook = new Workbook();
```

這將初始化一個新的 Excel 工作簿。但數據去了哪裡？讓我們在下一步中處理這個問題。

## 步驟 2：向工作表新增數據

一旦創建了工作簿，我們需要訪問第一個工作表並為其命名。我們將在這裡輸入餅圖所需的資料。

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

在這裡，我們新增兩列：一列用於地區，另一列用於銷售資料。此數據將以餅圖形式表示。

## 步驟 3：新增圖表表

接下來，讓我們新增一個單獨的工作表來儲存圓餅圖。

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

這張新表將包含圓餅圖。給它一個諸如“圖表”之類的名稱可以確保用戶知道打開文件時會發生什麼。

## 步驟 4：建立圓餅圖

現在是時候建立實際圖表了。我們將指定我們想要一個圓餅圖，並定義它在工作表上的位置。

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

方法 `Add()` 接受圖表類型的參數（在本例中， `ChartType.Pie`) 及其在工作表上的位置。數字代表行和列的位置。

## 步驟 5：自訂圖表外觀

如果沒有一些定制，餅圖就不完整！讓我們透過調整顏色、標籤和標題來使我們的圖表更具視覺吸引力。

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

我們為繪圖區域設定漸層填充，並隱藏邊框以獲得更整潔的外觀。

## 步驟 6：定義圖表數據

現在是時候將圖表連結到我們的數據了。這 `NSeries` 圖表的屬性將銷售數字和地區綁定到圓餅圖。

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

第一行指定我們使用儲存格中的銷售數據 `B2:B8`。我們也告訴圖表使用來自 `A2:A8` 作為類別標籤。

## 步驟 7：新增資料標籤

直接在圖表片段上添加標籤可以使其更容易理解。讓我們在餅圖切片中包含區域名稱和銷售價值。

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## 步驟 8：自訂圖表區域和圖例

最後，讓我們對圖表區域和圖例進行一些最後的修飾。這增強了圖表的整體呈現效果。

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

## 步驟 9：儲存工作簿

最後，我們將工作簿儲存為 Excel 檔案。您可以根據需要指定輸出目錄和檔案名稱。

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## 結論

使用 Aspose.Cells for .NET 建立圓餅圖是一個簡單且可自訂的過程。按照本指南，您只需幾個步驟即可產生傳達寶貴見解的專業圖表。無論是出於商業報告還是教育目的，掌握圖表創建都會提升您的 Excel 自動化技能。請記住，Aspose.Cells 提供了您所需的靈活性，讓您輕鬆建立令人驚嘆的、數據驅動的 Excel 檔案。

## 常見問題解答

### 我可以使用 Aspose.Cells for .NET 建立其他類型的圖表嗎？
是的！ Aspose.Cells 支援各種圖表類型，包括長條圖、折線圖和散點圖。

### 我需要付費許可證才能使用 Aspose.Cells for .NET 嗎？
您可以使用免費版本，但有一些限制。要獲得完整功能，您需要許可證，您可以購買 [這裡](https://purchase。aspose.com/buy).

### 我可以將圖表匯出為 PDF 或圖像等格式嗎？
絕對地！ Aspose.Cells 可讓您將圖表匯出為各種格式，包括 PDF 和 PNG。

### 是否可以為每個餅圖切片設定不同的顏色？
是的，您可以透過設定為每個切片應用不同的顏色 `IsColorVaried` 財產 `true`，如教程所示。

### 我可以在單一工作簿中自動產生多個圖表嗎？
是的，您可以在單一 Excel 檔案中建立和自訂所需數量的圖表。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}