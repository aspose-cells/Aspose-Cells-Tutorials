---
title: 將文字方塊控制項新增至圖表
linktitle: 將文字方塊控制項新增至圖表
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 將文字方塊新增至 Excel 中的圖表。輕鬆增強您的數據視覺化。
weight: 12
url: /zh-hant/net/inserting-controls-in-charts/add-textbox-control-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將文字方塊控制項新增至圖表

## 介紹

在 Excel 中建立動態且具有視覺吸引力的圖表是有效表示資料的絕佳方式。您可以使用的一項實用功能是將文字方塊新增至圖表。有了 Aspose.Cells for .NET，這個任務變得簡單又有趣！在本指南中，我們將引導您逐步完成將文字方塊整合到圖表中的過程。無論您是經驗豐富的開發人員還是新手，本教學都將為您提供增強 Excel 圖表所需的所有工具。那麼，您準備好潛入其中了嗎？

## 先決條件

在我們開始編碼之前，您應該先做好以下幾件事：

- 對 C# 的基本了解：對 C# 程式設計的基本掌握將會有所幫助。不用擔心;您不需要成為專家，只需輕鬆掌握文法即可。
- 安裝的 Aspose.Cells 函式庫：確保您已安裝 Aspose.Cells for .NET 函式庫。您可以從以下位置下載：[這裡](https://releases.aspose.com/cells/net/)如果你還沒有。
- Visual Studio：熟悉 Visual Studio 或您喜歡用於 .NET 框架的任何 IDE 至關重要。
- 現有 Excel 檔案：在此範例中，我們將使用名為「sampleAddingTextBoxControlInChart.xls」的現有 Excel 檔案。您可以建立一個或下載範例。

現在我們已經完成了所有工作，讓我們開始編碼部分！

## 導入包

首先，我們需要將必要的 Aspose.Cells 命名空間匯入到我們的 C# 專案中。您可以透過在程式碼檔案頂部新增以下行來輕鬆完成此操作：

```csharp
using System;
using System.IO;

using Aspose.Cells;
using System.Drawing;
```

## 第 1 步：定義來源目錄和輸出目錄

在開始使用 Excel 檔案之前，定義輸入檔案的位置以及輸出檔案的儲存位置非常重要。這有助於讓您的專案井井有條。

```csharp
//原始碼目錄
string sourceDir = "Your Document Directory";

//輸出目錄
string outputDir = "Your Output Directory";
```
代替`"Your Document Directory"`和`"Your Output Directory"`與系統上的實際路徑。

## 步驟 2： 開啟現有 Excel 文件

接下來，我們需要開啟包含要修改的圖表的 Excel 檔案。這將使我們能夠獲取圖表並進行更改。

```csharp
//開啟現有文件。
Workbook workbook = new Workbook(sourceDir + "sampleAddingTextBoxControlInChart.xls");
```
此行使用我們指定的檔案初始化一個新的 Workbook 物件。

## 第 3 步：存取工作表中的圖表

由於Excel中的圖表儲存在工作表中，因此我們需要先存取工作表，然後取得所需的圖表。在此範例中，我們將存取第一個工作表中的第一個圖表。

```csharp
//在第一張紙中取得設計師圖表。
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```
透過變更索引值，如果您的檔案有更多工作表或圖表，您可以選擇不同的工作表或圖表。

## 第 4 步：在圖表中新增文字框

現在，我們準備好新增文字方塊。我們將在創建它時指定它的位置和大小。

```csharp
//將新文字方塊新增至圖表。
Aspose.Cells.Drawing.TextBox textbox0 = chart.Shapes.AddTextBoxInChart(400, 1100, 350, 2550);
```
在此指令中，參數定義圖表中文字方塊的位置（x，y）和大小（寬度，高度）。根據您的特定佈局需求調整這些數值。

## 第 5 步：設定文本框的文本

一旦文字方塊就位，就可以用內容填滿它了。您可以添加您認為圖表所需的任何文字。

```csharp
//填寫文字。
textbox0.Text = "Sales By Region";
```
請隨意將“Sales By Region”替換為與您的資料相關的任何文字。

## 步驟6：調整文字方塊屬性

現在，讓我們的 TextBox 看起來更漂亮！您可以自訂各種屬性，例如字體顏色、大小和樣式。

```csharp
//設定字體顏色。
textbox0.Font.Color = Color.Maroon; //更改為您想要的顏色

//將字體設定為粗體。
textbox0.Font.IsBold = true;

//設定字體大小。
textbox0.Font.Size = 14;

//將字體屬性設定為斜體。
textbox0.Font.IsItalic = true;
```

其中每一行都會修改 TextBox 內文字的外觀，從而增強可見性和吸引力。

## 第 7 步：設定文字方塊外觀格式

設定文字方塊背景和邊框的格式也很重要。這使它在圖表上脫穎而出。

```csharp
//取得文字方塊的填滿格式。
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;

//取得文字方塊的行格式類型。
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;

//設定線寬。
lineformat.Weight = 2;

//將破折號樣式設定為實線。
lineformat.DashStyle = Aspose.Cells.Drawing.MsoLineDashStyle.Solid;
```

這些選項可讓您設定文字方塊的背景填入並自訂其邊框。

## 步驟8：儲存修改後的Excel文件

最後一步是將所做的變更儲存到新的 Excel 檔案。這將確保您的原始文件保持不變。

```csharp
//儲存 Excel 檔案。
workbook.Save(outputDir + "outputAddingTextBoxControlInChart.xls");
```
代替`"outputAddingTextBoxControlInChart.xls"`使用您喜歡的檔案名稱。

## 結論

恭喜！您已使用 Aspose.Cells for .NET 成功將 TextBox 控制項新增至圖表。這種簡單而有效的更改可以使您的圖表資訊更豐富且更具視覺吸引力。資料表示是有效溝通的關鍵，使用 Aspose 這樣的工具，您可以以最少的努力增強簡報效果。

## 常見問題解答

### 什麼是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一個功能強大的程式庫，用於建立、操作和轉換 Excel 文件，而無需依賴 Microsoft Excel。

### 我可以將多個文字方塊新增到單一圖表中嗎？
是的！您可以透過在不同位置重複文字方塊建立步驟來新增所需數量的文字方塊。

### Aspose.Cells 可以免費使用嗎？
Aspose.Cells 是一個付費庫，但您可以從以下位置下載免費試用版：[這裡](https://releases.aspose.com/).

### 在哪裡可以找到有關 Aspose.Cells 的更多文件？
您可以存取全面的文檔[這裡](https://reference.aspose.com/cells/net/).

### 如果遇到問題，我該如何獲得支援？
您可以透過 Aspose 支援論壇尋求協助[這裡](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
