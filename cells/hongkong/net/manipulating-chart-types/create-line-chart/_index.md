---
title: 建立折線圖
linktitle: 建立折線圖
second_title: Aspose.Cells .NET Excel 處理 API
description: 使用 Aspose.Cells for .NET 建立令人驚嘆的折線圖。按照我們的逐步指南有效地視覺化您的資料。
weight: 11
url: /zh-hant/net/manipulating-chart-types/create-line-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立折線圖

## 介紹

您準備好以驚人的清晰度視覺化您的數據了嗎？折線圖是顯示隨時間變化的趨勢或兩個變數之間關係的絕佳方式。無論您是管理業務專案的資料還是分析個人指標，以程式設計方式建立折線圖的功能都可以節省您的時間並提供更大的靈活性。在本指南中，我們將引導您完成使用 Aspose.Cells for .NET 建立折線圖的每個步驟。準備好潛入了嗎？讓我們開始吧！

## 先決條件

在我們深入了解創建折線圖的細節之前，讓我們確保您有能力遵循以下步驟：

1. Visual Studio：確保您的電腦上安裝了 Visual Studio，因為它是最受歡迎的 .NET 開發 IDE 之一。
2.  Aspose.Cells for .NET Library：您需要 Aspose.Cells 函式庫，可以從以下位置下載：[這裡](https://releases.aspose.com/cells/net/).
3. C#基礎知識：熟悉C#程式語言將有助於您更好地理解範例和程式碼片段。
4. .NET Framework 或 .NET Core：任一框架的基本設置，因為這將成為我們應用程式的基礎。

一旦解決了這些先決條件，您就可以建立一些圖表了！

## 導入包

現在我們已經設定了環境，我們需要在 C# 程式碼中匯入必要的套件。就像在開始專案之前收集工具一樣，導入套件對於確保您擁有所需的一切至關重要。

操作方法如下：

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

該行導入`Aspose.Cells`命名空間，其中包含我們將用於建立折線圖的所有類別和方法。

現在，讓我們將整個過程分解為簡單易懂的步驟。每個步驟將引導您完成使用 Aspose.Cells for .NET 建立折線圖的邏輯流程。

## 第 1 步：設定輸出目錄

第一步是定義要儲存輸出檔案的位置。這就像在開始動手之前設定好工作空間一樣。 

```csharp
//輸出目錄
string outputDir = "Your Output Directory";
```
代替`"Your Output Directory"`與要儲存產生的 Excel 檔案的實際路徑。

## 第 2 步：實例化工作簿對象

接下來，我們需要建立一個新的工作簿實例。將工作簿視為發揮創意的畫布。 

```csharp
//實例化 Workbook 物件
Workbook workbook = new Workbook();
```
此行初始化一個新工作簿，其中將保存所有資料和視覺效果。

## 第 3 步：訪問工作表

在我們新建立的工作簿中，我們需要取得將輸入資料的工作表的參考。如果工作簿是我們的畫布，那麼工作表就是我們的調色盤。

```csharp
//透過傳遞工作表索引來取得新新增的工作表的引用
Worksheet worksheet = workbook.Worksheets[0];
```
在這裡，我們訪問第一個工作表（索引`0`）。

## 步驟 4：將範例值新增至儲存格

現在來了有趣的部分！我們將在工作表中輸入一些範例值。這些數據將作為我們折線圖的基礎。 

```csharp
//將樣本值新增至儲存格
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
在此程式碼片段中，我們將值新增至 A 列和 B 列中的儲存格。

## 步驟 5：將折線圖加入工作表中

接下來，我們將在工作表中引入折線圖。這才是您的數據真正變得栩栩如生的地方！

```csharp
//將圖表新增至工作表
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Line, 5, 0, 25, 10);
```
在這裡，我們在指定位置新增折線圖。參數 (5, 0, 25, 10) 定義圖表在工作表中的位置和大小。

## 第 6 步：存取新圖表實例

新增圖表後，就可以使用新建立的圖表物件了。 

```csharp
//存取新新增的圖表實例
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```
此程式碼將我們連接到圖表，以便我們可以進一步操作它。

## 第 7 步：將 SeriesCollection 加入圖表中

現在我們需要告訴圖表要顯示哪些數據。這是我們透過新增 SeriesCollection 來定義折線圖資料來源的地方。

```csharp
//將 SeriesCollection（圖表資料來源）新增至從「A1」儲存格到「B3」的圖表中
chart.NSeries.Add("A1:B3", true);
```
在此範例中，我們告訴圖表使用儲存格 A1 到 B3 中的值。

## 步驟 8：儲存 Excel 文件

大結局！完成所有辛勤工作後，是時候保存 Excel 文件並查看實際的折線圖了。

```csharp
//儲存 Excel 文件
workbook.Save(outputDir + "outputHowToCreateLineChart.xlsx");
```
此行將工作簿保存在指定的輸出目錄中，名稱為`outputHowToCreateLineChart.xlsx`.

## 步驟9：執行並驗證

最後，您現在可以運行程式碼並驗證折線圖是否已在輸出目錄中成功建立！ 

```csharp
Console.WriteLine("HowToCreateLineChart executed successfully.");
```
這將在您的控制台中輸出一條訊息，讓您知道一切運行順利。

## 結論

使用 Aspose.Cells for .NET 建立折線圖是讓資料栩栩如生的有效方法。透過遵循此逐步指南，您可以輕鬆地視覺化資料集中的趨勢和關係。無論您是經驗豐富的開發人員還是剛入門，Aspose.Cells 都能為您提供自動化資料視覺化任務的靈活性和功能。 

## 常見問題解答

### 什麼是 Aspose.Cells for .NET？  
Aspose.Cells for .NET 是一個功能強大的程式庫，旨在以程式設計方式管理和操作 Excel 文件，使開發人員能夠建立、編輯和轉換電子表格。

### Aspose.Cells 支援圖表嗎？  
是的，Aspose.Cells 為各種圖表類型提供了廣泛的支持，包括折線圖、餅圖、長條圖等。

### 我可以免費使用 Aspose.Cells 嗎？  
是的，您可以下載免費試用版來探索其功能。如需長期使用，請考慮購買授權。

### 有支援論壇嗎？  
絕對地！您可以在以下位置找到答案並提出問題[Aspose.Cells 論壇](https://forum.aspose.com/c/cells/9).

### 我如何購買許可證？  
可以透過以下方式輕鬆購買許可證[購買頁面](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
