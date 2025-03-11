---
title: 使用迷你圖
linktitle: 使用迷你圖
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何透過 Aspose.Cells for .NET 在 Excel 中有效使用迷你圖。包含逐步指南，可帶來流暢的體驗。
weight: 18
url: /zh-hant/net/advanced-chart-operations/using-sparklines/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用迷你圖

## 介紹

在當今快節奏的數據分析和視覺化世界中，我們經常尋求快速有效的方式來呈現資訊。迷你圖是一種巧妙的解決方案 - 一種小型、簡單的圖形或圖表，以緊湊的格式概述數據趨勢和變化。無論您是分析師、開發人員還是僅僅熱愛數據的人，學習如何使用 Aspose.Cells for .NET 在 Excel 文件中使用迷你圖都可以提升資訊的呈現效果。在本指南中，我們將逐步探索實現迷你圖的過程，確保您可以有效地利用這項令人驚嘆的功能的強大功能。

## 先決條件

在我們深入了解迷你圖的世界之前，讓我們先介紹一些為我們的旅程奠定基礎的先決條件：

1. 熟悉C#：C#程式設計的基礎知識將幫助您更好地理解編碼部分。
2. 已安裝 .NET Framework：請確保您的系統上安裝了 .NET Framework。
3. Aspose.Cells for .NET：您的專案中需要有 Aspose.Cells 函式庫。您可以從以下位置下載：[這裡](https://releases.aspose.com/cells/net/).
4.  Excel 範本：我們將使用一個名為`sampleUsingSparklines.xlsx`。將其保存在工作目錄中。

現在我們已經有了必要的設置，讓我們分解實施迷你圖的步驟！

## 導入包

在編寫程式碼之前，我們需要導入必要的套件。在您的 C# 檔案中，包含以下 using 語句：

```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System;
using System.Drawing;
```

匯入這些套件將使您能夠存取 Aspose.Cells 庫、渲染功能以及用於處理顏色和控制台操作的基本系統庫。

## 第 1 步：初始化輸出與來源目錄

在第一步中，我們將定義儲存輸出和來源檔案的目錄。 

```csharp
//輸出目錄
string outputDir = "Your Output Directory"; //指定路徑

//原始碼目錄
string sourceDir = "Your Document Directory"; //指定路徑
```

在這裡，替換`Your Output Directory`和`Your Document Directory`與系統上的實際路徑。

## 第 2 步：建立並開啟工作簿

現在，讓我們建立一個工作簿並開啟 Excel 範本檔案。

```csharp
//實例化工作簿
//開啟模板文件
Workbook book = new Workbook(sourceDir + "sampleUsingSparklines.xlsx");
```

這段程式碼實例化了`Workbook`class 並從來源目錄載入指定的模板檔案。

## 第 3 步：存取第一個工作表

接下來，我們將存取工作簿中的第一個工作表。 

```csharp
//取得第一個工作表
Worksheet sheet = book.Worksheets[0];
```

透過存取第一個工作表，我們可以開始操作其中的資料和特徵。

## 步驟 4：讀取現有迷你圖（如果有）

如果您希望檢查工作表中是否存在任何現有迷你圖，可以使用下列程式碼來執行此操作：

```csharp
//從模板檔案中讀取迷你圖（如果有）
foreach (SparklineGroup g in sheet.SparklineGroupCollection)
{
    //顯示迷你圖組訊息
    Console.WriteLine("sparkline group: type:" + g.Type + ", sparkline items count:" + g.SparklineCollection.Count);
    
    foreach (Sparkline s in g.SparklineCollection)
    {
        //顯示單一迷你圖及其資料範圍
        Console.WriteLine("sparkline: row:" + s.Row + ", col:" + s.Column + ", dataRange:" + s.DataRange);
    }
}
```

執行此命令將顯示有關 Excel 檔案中已存在的任何迷你圖的資訊 - 這是查看已視覺化的資料趨勢的有用方法！

## 步驟 5：定義新迷你圖的單元格區域

接下來，我們要定義新迷你圖在工作表中的放置位置。 

```csharp
//定義單元格區域 D2:D10
CellArea ca = new CellArea();
ca.StartColumn = 4; //乙
ca.EndColumn = 4;   //乙
ca.StartRow = 1;    //2
ca.EndRow = 7;      // 8
```

在此程式碼片段中，我們在工作表中設定一個標記為 D2:D10 的區域，將在其中建立新的迷你圖。根據您希望迷你圖顯示的位置調整儲存格引用。

## 步驟 6：將迷你圖新增至工作表

有了我們定義的單元格區域，就可以建立並添加迷你圖了！

```csharp
//將資料範圍的新迷你圖新增至儲存格區域
int idx = sheet.SparklineGroupCollection.Add(SparklineType.Column, "Sheet1!B2:D8", false, ca);
SparklineGroup group = sheet.SparklineGroupCollection[idx];
```

在這裡，我們為跨越的資料新增列類型迷你圖`Sheet1!B2:D8`進入先前定義的儲存格區域。不要忘記根據您的要求修改資料範圍。

## 第 7 步：自訂迷你圖顏色

當你可以有一些天賦時，為什麼還要堅持使用預設顏色呢？讓我們自訂迷你圖顏色！

```csharp
//建立單元格顏色
CellsColor clr = book.CreateCellsColor();
clr.Color = Color.Orange; //選擇您想要的顏色
group.SeriesColor = clr;
```

在此程式碼中，我們建立一個新的`CellsColor`例如，將其設為橙色，並將其套用到我們剛剛建立的迷你圖系列。

## 步驟8：儲存修改後的工作簿

最後，讓我們儲存工作簿的更改並結束它！

```csharp
//儲存 Excel 文件
book.Save(outputDir + "outputUsingSparklines.xlsx");

Console.WriteLine("UsingSparklines executed successfully.");
```

此段程式碼將修改後的工作簿儲存到指定的輸出目錄。您將看到一條成功訊息，確認一切順利。

## 結論

這就是使用 Aspose.Cells for .NET 在 Excel 工作表中建立和使用迷你圖的全面逐步指南。迷你圖是提供具有視覺吸引力且易於理解的數據見解的絕佳方式。無論是報告、演示文稿，甚至是內部文檔，這種動態功能都可以使您的資料更具影響力。

## 常見問題解答

### 什麼是迷你圖？
迷你圖是適合單一單元格的微型圖，提供緊湊而簡單的資料趨勢視覺化。

### 我需要許可證才能使用 Aspose.Cells 嗎？
是的，您需要有效的許可證才能使用 Aspose.Cells 的所有功能。你可以獲得一個[臨時執照](https://purchase.aspose.com/temporary-license/)如果你剛開始。

### 我可以建立不同類型的迷你圖嗎？
絕對地！ Aspose.Cells 支援各種迷你圖類型，包括行、列和贏/輸迷你圖。

### 在哪裡可以找到更多文件？
您可以存取 Aspose.Cells for .NET 的詳細文件和範例[這裡](https://reference.aspose.com/cells/net/).

### 有免費試用嗎？
是的，您可以下載 Aspose.Cells 的免費試用版[這裡](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
