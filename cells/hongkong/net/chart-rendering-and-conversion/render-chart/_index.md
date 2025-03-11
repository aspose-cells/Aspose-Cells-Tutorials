---
title: 渲染圖表
linktitle: 渲染圖表
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells 在 .NET 中渲染圖表。按照我們的逐步教學輕鬆創建令人驚嘆的視覺效果。
weight: 10
url: /zh-hant/net/chart-rendering-and-conversion/render-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 渲染圖表

## 介紹

圖表是數據呈現和分析的重要元素，使複雜的資訊易於理解。如果您使用 .NET 並需要以程式設計方式產生圖表，Aspose.Cells 是一個功能強大的程式庫，它提供了用於處理 Excel 檔案和圖表的直覺且進階的功能。在本指南中，我們將逐步介紹使用 Aspose.Cells for .NET 渲染圖表的過程。準備好深入學習這個詳細的教程，該教程旨在引人入勝且易於理解！

## 先決條件

在我們進入程式碼之前，讓我們確保您已準備好一切。這是您需要的：

1. .NET 環境：確保您已設定 .NET 開發環境。您可以使用 Visual Studio 或任何其他支援 .NET 的 IDE。
2.  Aspose.Cells for .NET：您需要安裝Aspose.Cells函式庫。您可以從以下位置下載：[Aspose的發布頁面](https://releases.aspose.com/cells/net/).
3. 基本 C# 知識：熟悉 C# 程式設計將幫助您更好地理解範例，但如果您是新手，請不要擔心 — 本指南將逐步解釋所有內容！

## 導入包

編碼之旅的第一步是導入必要的套件。在 IDE 中開啟專案並新增以下命名空間：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
```

這些命名空間將使您能夠存取 Aspose.Cells 庫提供的功能，從而允許您無縫地建立和操作圖表。


現在我們已經介紹了先決條件和匯入，讓我們深入了解渲染圖表的實質內容！我們將把它分解為清晰、可管理的步驟。

## 第 1 步：設定輸出目錄

在建立工作簿和圖表之前，我們需要確定輸出的保存位置。這樣，當我們的圖表生成時，您就會確切地知道在哪裡可以找到它。

```csharp
string outputDir = "Your Output Directory"; //在此指定輸出目錄。
```

確保將“您的輸出目錄”替換為您要儲存圖表影像的路徑。

## 第 2 步：建立工作簿

接下來，我們將建立一個新的工作簿。這就是所有魔法發生的地方！

```csharp
Workbook workbook = new Workbook();
```

該行創建了一個新實例`Workbook`類，它允許我們使用表格和圖表。

## 第 3 步：新增工作表

現在我們有了工作簿，是時候新增新的工作表了。將工作表視為筆記本中的不同頁面，您可以在其中組織資料。

```csharp
int sheetIndex = workbook.Worksheets.Add();
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```

在這裡，我們添加一個新工作表並獲取對其的引用。您將使用此工作表來輸入資料和圖表。

## 步驟 4：輸入樣本值

建立工作表後，我們將一些範例資料新增到儲存格中。該數據是您的圖表的基礎，因此請選擇對您的圖表類型有意義的值！

```csharp
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```

在此程式碼片段中，我們使用一些數值填充單元格“A1”到“A3”，並使用另一組值填充單元格“B1”到“B3”。請隨意自訂這些數字以滿足您的需求！

## 第 5 步：建立圖表

現在，是時候建立圖表了。我們將添加長條圖類型，這對於比較值非常有用。

```csharp
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

在這裡，我們透過定義其佈局在指定位置新增圖表：第一組數字表示圖表在網格上的位置。

## 第 6 步：將資料系列新增至圖表中

建立圖表後，我們現在需要將其綁定到我們在前面步驟中輸入的資料。

```csharp
chart.NSeries.Add("A1:B3", true);
```

此線將圖表的資料系列連接到儲存格「A1」到「B3」中的值。這意味著您的圖表將按預期直觀地表示數據。

## 第 7 步：將圖表另存為圖像

現在讓我們將圖表轉換為圖像格式，以便可以輕鬆分享和查看。

```csharp
chart.ToImage(outputDir + "outputChartRendering.emf", System.Drawing.Imaging.ImageFormat.Emf);
```

在此步驟中，我們將圖表作為 EMF（增強型圖元檔案）影像保存在指定的輸出目錄中。您也可以將其儲存為不同的格式，例如 BMP 或 PNG。

## 第 8 步：將圖表轉換為點陣圖

如果您喜歡使用點陣圖，請按照以下步驟將圖表轉換為點陣圖格式。

```csharp
System.Drawing.Bitmap bitmap = chart.ToImage();
bitmap.Save(outputDir + "outputChartRendering.bmp", System.Drawing.Imaging.ImageFormat.Bmp);
```

這會將您的圖表儲存為 BMP 影像。請記住，BMP 檔案往往較大，但品質非常高！

## 第 9 步：使用進階選項進行渲染

我們還可以使用一些進階影像選項來渲染圖表，以獲得更好的品質和解析度。讓我們設定幾個選項：

```csharp
ImageOrPrintOptions options = new ImageOrPrintOptions()
{
    VerticalResolution = 300,
    HorizontalResolution = 300,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.AntiAlias
};
```

這些選項有助於提高生成的圖像的視覺質量，對於簡報或出版物尤其有用。

## 步驟 10：使用進階選項將圖表轉換為影像

現在讓我們使用剛剛設定的進階選項來實際轉換圖表。

```csharp
chart.ToImage(outputDir + "outputChartRendering.png", options);
```

這會將您的圖表儲存為具有增強品質設定的 PNG 檔案。

## 第 11 步：將圖表匯出為 PDF

最後，如果您想要一個精美的、易於共享的文檔，您可以將圖表直接匯出為 PDF 格式。

```csharp
chart.ToPdf(outputDir + "outputChartRendering.pdf");
```

此步驟將建立一個包含您的圖表的 PDF，使其非常適合數位報告或與同事分享。

## 結論 

恭喜！您已使用 Aspose.Cells for .NET 成功渲染了圖表。這個功能強大的庫簡化了 Excel 文件和圖表的創建和操作，使您的資料更易於存取且更具視覺吸引力。無論您是準備報告、分析還是演示文稿，圖表都會產生重大影響，並且使用 Aspose，您可以輕鬆地以程式設計方式建立它們。

## 常見問題解答

### 我可以使用 Aspose.Cells for .NET 建立哪些類型的圖表？
您可以建立各種圖表，包括長條圖、折線圖、圓餅圖和長條圖等。

### 我可以自訂圖表的外觀嗎？
是的，Aspose.Cells 允許進行廣泛的自訂，包括顏色、樣式和圖表元素。

### 有免費試用嗎？
絕對地！您可以從以下位置下載免費試用版[這裡](https://releases.aspose.com/).

### 我可以在哪裡獲得 Aspose.Cells 的支援？
您可以在以下位置找到社區支持和資源：[Aspose 支援論壇](https://forum.aspose.com/c/cells/9).

### 我需要許可證才能使用 Aspose.Cells 嗎？
是的，試用期結束後繼續使用需要許可證，但您可以申請臨時許可證[這裡](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
