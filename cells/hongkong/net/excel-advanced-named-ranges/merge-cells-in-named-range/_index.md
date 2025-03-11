---
title: 合併 Excel 中命名範圍內的儲存格
linktitle: 合併 Excel 中命名範圍內的儲存格
second_title: Aspose.Cells .NET Excel 處理 API
description: 在此逐步教學中，了解如何使用 Aspose.Cells for .NET 合併命名範圍中的儲存格。了解如何設定 Excel 報表的格式、樣式和自動化。
weight: 11
url: /zh-hant/net/excel-advanced-named-ranges/merge-cells-in-named-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 合併 Excel 中命名範圍內的儲存格

## 介紹

以程式設計方式處理 Excel 檔案時，您可能遇到的常見任務之一是合併命名範圍內的儲存格。無論您是自動產生報表、建立儀表板還是只是管理大型資料集，合併儲存格都是一項重要技術。在本教學中，我們將探討如何使用 Aspose.Cells for .NET 合併命名範圍中的儲存格，這是一個功能強大的程式庫，可讓開發人員在無需安裝 Microsoft Excel 的情況下操作 Excel 檔案。

## 先決條件

在我們開始之前，請確保您已準備好以下內容：

-  Aspose.Cells for .NET：您可以從[Aspose.Cells 發佈頁面](https://releases.aspose.com/cells/net/).
- 您的電腦上已安裝 .NET Framework。
- 對 C# 的基本了解：熟悉類別、方法和物件等概念將會有所幫助。

## 導入包

在我們開始編碼之前，您需要匯入必要的名稱空間。這些命名空間將使您能夠存取 Aspose.Cells 庫的功能。

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

完成先決條件和軟體包後，讓我們進入有趣的部分：編碼！

以下詳細介紹如何使用 Aspose.Cells for .NET 合併 Excel 工作表中命名範圍內的儲存格。

## 第 1 步：建立新工作簿

我們首先需要的是一本工作簿。 Excel 術語中的工作簿相當於 Excel 檔案。讓我們創建一個。

```csharp
//實例化一個新的工作簿。
Workbook wb1 = new Workbook();
```

透過初始化一個新的工作簿，我們現在有一個空的 Excel 檔案可供操作。這就像從一張空白畫布開始！

## 第 2 步：存取第一個工作表

每個工作簿都包含工作表，在本例中，我們希望使用第一個工作表。讓我們抓住它吧！

```csharp
//取得工作簿中的第一個工作表。
Worksheet worksheet1 = wb1.Worksheets[0];
```

將工作表視為 Excel 檔案中實際資料所在的各個標籤。預設情況下，我們正在存取第一個選項卡。

## 第 3 步：建立儲存格範圍

現在我們有了工作表，是時候建立一個範圍了。範圍是指單元格區塊，可以跨越多行和多列。

```csharp
//建立一個範圍。
Range mrange = worksheet1.Cells.CreateRange("D6", "I12");
```

在這裡，我們選擇從 D6 到 I12 的儲存格——一個覆蓋多行和列的區塊。我們很快就會合併這個範圍！

## 第 4 步：命名範圍

命名範圍可以讓以後更容易引用，尤其是在處理大型資料集時。

```csharp
//命名範圍。
mrange.Name = "TestRange";
```

透過將此範圍命名為“TestRange”，我們可以稍後在程式碼中快速檢索它，而無需再次指定單元格座標。

## 第 5 步：合併儲存格範圍

現在我們來看看神奇之處——合併我們剛剛創建的範圍內的單元格！

```csharp
//合併該範圍的儲存格。
mrange.Merge();
```

此步驟將從 D6 到 I12 的所有儲存格合併為一個儲存格。非常適合標題或摘要等內容！

## 第 6 步：檢索命名範圍

合併儲存格後，我們可能需要套用一些格式。讓我們先檢索我們的命名範圍。

```csharp
//獲取範圍。
Range range1 = wb1.Worksheets.GetRangeByName("TestRange");
```

透過名稱檢索範圍允許我們執行進一步的操作，例如添加樣式或輸入資料。

## 步驟 7：定義合併儲存格的樣式

如果合併的單元格看起來不精美，那麼它有什麼用呢？讓我們建立一個樣式物件來對齊文字並應用背景顏色。

```csharp
//定義一個樣式物件。
Style style = wb1.CreateStyle();

//設定對齊方式。
style.HorizontalAlignment = TextAlignmentType.Center;
style.VerticalAlignment = TextAlignmentType.Center;
style.Pattern = BackgroundType.Solid;
style.ForegroundColor = System.Drawing.Color.Aqua;
```

在這裡，我們將文字水平和垂直居中對齊，並設定淺藍色（水綠色）背景色。時尚吧？

## 第 8 步：將樣式套用到範圍

定義樣式後，就可以將其套用到合併範圍了。

```csharp
//建立一個 StyleFlag 物件。
StyleFlag flag = new StyleFlag();

//啟用相對樣式屬性。
flag.HorizontalAlignment = true;
flag.VerticalAlignment = true;
flag.CellShading = true;

//將樣式套用到範圍。
range1.ApplyStyle(style, flag);
```

這`StyleFlag`告訴 Aspose.Cells 要套用哪些樣式屬性 - 對齊、陰影等。

## 第9步：將資料輸入到合併範圍中

什麼是沒有內容的格式化範圍？讓我們添加一些文字。

```csharp
//將資料輸入範圍。
range1[0, 0].PutValue("Welcome to Aspose APIs.");
```

這會將文字「歡迎使用 Aspose API」放入合併範圍的第一個儲存格中。合併儲存格後，此文字將跨越從 D6 到 I12 的所有儲存格。

## 步驟10：儲存Excel文件

最後，我們將工作簿儲存為 Excel 檔案。

```csharp
//儲存 Excel 檔案。
wb1.Save(dataDir + "outputMergeCellsInNamedRange.xlsx");
```

此處，工作簿以名稱「outputMergeCellsInNamedRange.xlsx」保存在指定目錄中。

## 結論

現在你就擁有了！您已經成功合併了命名範圍中的單元格，應用了一些漂亮的格式，甚至輸入了一些資料 - 所有這些都使用 Aspose.Cells for .NET。無論您是致力於自動化報告、操作 Excel 文件，還是只是學習新技術，本逐步指南都應該為您提供所需的基礎。

## 常見問題解答

### 我可以在 Aspose.Cells 中合併多個不連續的範圍嗎？  
不可以，您只能合併 Aspose.Cells 中的連續儲存格。

### 我可以透過程式撤銷合併操作嗎？  
合併儲存格後，您可以使用以下命令取消合併它們`UnMerge()`Aspose.Cells 中的方法。

### 合併儲存格會刪除其中的資料嗎？  
如果合併前儲存格中有任何數據，它將保留該範圍的第一個儲存格中的資料。

### 我可以對合併範圍內的各個單元格套用不同的樣式嗎？  
不可以，合併區域充當單一單元格，因此您不能將不同的樣式套用到其中的各個單元格。

### 合併後如何存取合併的儲存格？  
合併後，您仍然可以使用左上角的座標存取合併的儲存格。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
