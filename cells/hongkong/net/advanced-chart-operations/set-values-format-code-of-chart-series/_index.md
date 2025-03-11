---
title: 圖表系列設定值格式代碼
linktitle: 圖表系列設定值格式代碼
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過這個詳細的逐步教學，了解如何在 Aspose.Cells for .NET 中設定圖表系列的值格式代碼。非常適合初學者。
weight: 17
url: /zh-hant/net/advanced-chart-operations/set-values-format-code-of-chart-series/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 圖表系列設定值格式代碼

## 介紹

在當今數據驅動的世界中，複雜數據集的可視化表示對於決策至關重要。圖表是有效傳達見解的強大工具。 Aspose.Cells for .NET 簡化了這個過程，使開發人員能夠輕鬆操作 Excel 檔案並建立令人驚嘆的圖表。在本指南中，我們將探討如何使用 Aspose.Cells 設定圖表系列的值格式代碼。那麼，喝杯咖啡，讓我們一起踏上這段程式設計之旅吧！

## 先決條件

在深入討論細節之前，讓我們先確保您已做好成功的準備。這是您需要的：

1. 對 C# 的基本了解：熟悉 C# 將幫助您輕鬆掌握程式設計概念。
2.  Aspose.Cells for .NET：您需要 Aspose.Cells 函式庫。你可以下載它[這裡](https://releases.aspose.com/cells/net/).
3. Visual Studio：適合撰寫和執行 C# 程式碼的 IDE。任何支援 .NET 的版本都可以。
4.  Excel 檔案：在我們的示範中，我們將使用名為`sampleSeries_ValuesFormatCode.xlsx`。確保您已在工作目錄中準備好它。

## 導入包

首先，讓我們導入必要的套件。這一步至關重要，因為它允許我們利用 Aspose.Cells 提供的功能。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells;
using Aspose.Cells.Charts;
```

透過這些匯入，我們現在可以從 Aspose 庫存取操作 Excel 檔案所需的基本類別。

現在，讓我們將這個過程分解為簡單易懂的步驟。請跟隨我們概述如何在 Excel 檔案中設定圖表系列的值格式代碼。

## 第 1 步：設定來源目錄和輸出目錄

在操作 Excel 檔案之前，我們需要指定它的位置以及輸出的位置。 

將此視為為我們的表演奠定了基礎。如果您不知道輸入在哪裡以及輸出在哪裡，您的程式將迷失在檔案目錄的迷宮中！

```csharp
//原始碼目錄
string sourceDir = "Your Document Directory";

//輸出目錄
string outputDir = "Your Output Directory";
```

## 第 2 步：載入來源 Excel 文件

現在我們已經設定了目錄，是時候載入我們想要使用的 Excel 檔案了。

載入 Excel 檔案類似於在閱讀之前開啟一本書。如果不打開它，您就無法深入了解其內容。 

```csharp
//載入來源 Excel 文件
Workbook wb = new Workbook(sourceDir + "sampleSeries_ValuesFormatCode.xlsx");
```

## 第 3 步：訪問工作表

載入工作簿後，讓我們深入研究第一個工作表。

Excel 檔案中的每個工作表就像書中的一頁。您想要訪問正確的頁面來查找您感興趣的數據！

```csharp
//訪問第一個工作表
Worksheet worksheet = wb.Worksheets[0];
```

## 第 4 步：訪問圖表

接下來，我們需要存取要修改系列格式的圖表。

將圖表想像成一塊畫布，繪製您的數據視覺化傑作。訪問它可以讓我們利用它的力量！

```csharp
//訪問第一個圖表
Chart ch = worksheet.Charts[0];
```

## 第5步：新增資料系列

準備好圖表後，讓我們添加一些資料系列以進行視覺化。

添加系列就像為您的繪畫添加顏色一樣。色彩越豐富，藝術品越吸引人！

```csharp
//使用值數組新增系列
ch.NSeries.Add("{10000, 20000, 30000, 40000}", true);
```

## 步驟 6：設定值格式代碼

這就是奇蹟發生的地方。我們將為新新增的系列設定格式代碼。

設定格式代碼可將原始數字轉換為更具可讀性的內容，就像在向世界展示之前套用濾鏡來增強您的照片一樣！

```csharp
//訪問該系列並設定其值格式代碼
Series srs = ch.NSeries[0];
srs.ValuesFormatCode = "$#,##0"; //這將其設定為貨幣格式
```

## 第 7 步：儲存輸出 Excel 文件

最後，我們需要將所做的變更儲存到新的 Excel 檔案中。

節省你的辛苦工作讓人感覺很有意義，不是嗎？它保存您的努力並允許您隨時分享或回顧您的工作！

```csharp
//儲存輸出的 Excel 文件
wb.Save(outputDir + "outputSeries_ValuesFormatCode.xlsx");
```

## 第8步：確認訊息

最後，我們可以列印一條成功訊息。

就像表演結束時獲得掌聲一樣，這種確認會給你一種溫暖、模糊的成就感。

```csharp
Console.WriteLine("SetValuesFormatCodeOfChartSeries executed successfully.");
```

## 結論

在本教學中，我們詳細介紹了使用 Aspose.Cells for .NET 設定圖表系列的值格式程式碼的過程。從載入 Excel 檔案到儲存最終產品，每一步都讓我們更接近以有意義且有影響力的方式有效地視覺化資料。現在，您可以掌握這些技能並將其應用到您正在進行的專案中。

## 常見問題解答

### 什麼是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一個功能強大的程式庫，可讓開發人員使用 .NET 應用程式建立、操作和轉換 Excel 檔案。

### 我需要許可證才能使用 Aspose.Cells 嗎？
是的，Aspose.Cells 需要許可證才能在生產環境中使用。您可以選擇臨時許可證用於測試目的。

### 我可以使用 Aspose.Cells 從頭開始建立圖表嗎？
絕對地！ Aspose.Cells 提供了從頭開始建立和自訂圖表的強大功能。

### 在哪裡可以找到有關 Aspose.Cells 的更多文件？
您可以訪問[Aspose.Cells 文檔](https://reference.aspose.com/cells/net/)取得詳細指南和 API 參考。

### 儲存 Excel 檔案時支援哪些格式？
Aspose.Cells 支援多種格式，包括 XLSX、XLS、CSV、PDF 等。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
