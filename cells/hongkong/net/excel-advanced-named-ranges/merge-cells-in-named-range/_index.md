---
"description": "在本逐步教學中了解如何使用 Aspose.Cells for .NET 合併命名範圍內的儲存格。了解如何格式化、設定樣式以及自動化 Excel 報表。"
"linktitle": "在 Excel 中合併命名範圍內的儲存格"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 Excel 中合併命名範圍內的儲存格"
"url": "/zh-hant/net/excel-advanced-named-ranges/merge-cells-in-named-range/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中合併命名範圍內的儲存格

## 介紹

以程式設計方式處理 Excel 檔案時，您可能會遇到的常見任務之一是合併命名範圍內的儲存格。無論您是自動產生報表、建立儀表板還是僅管理大型資料集，合併儲存格都是一項不可或缺的技術。在本教學中，我們將探討如何使用 Aspose.Cells for .NET 合併命名範圍內的儲存格 - 這是一個功能強大的函式庫，讓開發人員無需安裝 Microsoft Excel 即可操作 Excel 檔案。

## 先決條件

在我們開始之前，請確保您已準備好以下內容：

- Aspose.Cells for .NET：您可以從 [Aspose.Cells 發佈頁面](https://releases。aspose.com/cells/net/).
- 您的機器上安裝了 .NET Framework。
- 對 C# 的基本了解：熟悉類別、方法和物件等概念會有所幫助。

## 導入包

在我們開始編碼之前，您需要匯入必要的命名空間。這些命名空間將允許您存取 Aspose.Cells 庫的功能。

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

解決了先決條件和軟體包後，讓我們進入有趣的部分：編碼！

以下是如何使用 Aspose.Cells for .NET 合併 Excel 工作表中指定範圍內的儲存格的詳細說明。

## 步驟 1：建立新工作簿

我們首先需要的是一本工作簿。 Excel 術語中的工作簿相當於 Excel 檔案。讓我們創建一個。

```csharp
// 實例化一個新的工作簿。
Workbook wb1 = new Workbook();
```

透過初始化新的工作簿，我們現在有一個可供操作的空白 Excel 檔案。這就像從一張空白的畫布開始！

## 第 2 步：存取第一個工作表

每個工作簿都包含工作表，在這種情況下，我們要使用第一個工作簿。我們抓住它吧！

```csharp
// 取得工作簿中的第一個工作表。
Worksheet worksheet1 = wb1.Worksheets[0];
```

可以將工作表視為 Excel 檔案中存放實際資料的單獨標籤。預設情況下，我們訪問第一個選項卡。

## 步驟 3：建立儲存格區域

現在我們有了工作表，是時候建立一個範圍了。範圍是指一個單元格區塊，可以跨越多行和多列。

```csharp
// 建立一個範圍。
Range mrange = worksheet1.Cells.CreateRange("D6", "I12");
```

在這裡，我們選擇從 D6 到 I12 的儲存格 - 一個覆蓋多行和多列的區塊。我們很快就會合併這個範圍！

## 步驟 4：命名範圍

命名範圍使得以後引用更容易，特別是在處理大型資料集時。

```csharp
// 命名範圍。
mrange.Name = "TestRange";
```

透過將此範圍命名為“TestRange”，我們可以在程式碼中快速檢索它，而無需再次指定單元格座標。

## 步驟 5：合併儲存格區域

現在來看看魔術——合併我們剛剛創建的範圍內的單元格！

```csharp
// 合併該範圍的儲存格。
mrange.Merge();
```

此步驟將從 D6 到 I12 的所有儲存格合併為一個儲存格。非常適合標題或摘要之類的內容！

## 步驟 6：檢索命名範圍

一旦單元格合併，我們可能想要套用一些格式。讓我們先檢索我們的命名範圍。

```csharp
// 獲取範圍。
Range range1 = wb1.Worksheets.GetRangeByName("TestRange");
```

透過名稱檢索範圍可以讓我們執行進一步的操作，例如新增樣式或輸入資料。

## 步驟 7：為合併儲存格定義樣式

如果合併的單元格看起來不夠精緻，那還有什麼用呢？讓我們建立一個樣式物件來對齊文字並應用背景顏色。

```csharp
// 定義樣式物件。
Style style = wb1.CreateStyle();

// 設定對齊方式。
style.HorizontalAlignment = TextAlignmentType.Center;
style.VerticalAlignment = TextAlignmentType.Center;
style.Pattern = BackgroundType.Solid;
style.ForegroundColor = System.Drawing.Color.Aqua;
```

在這裡，我們將文字水平和垂直對齊在中心，並設定淺藍色（水綠色）背景顏色。很時尚吧？

## 步驟 8：將樣式套用至範圍

定義樣式後，就可以將其套用到合併範圍了。

```csharp
// 建立一個 StyleFlag 物件。
StyleFlag flag = new StyleFlag();

// 使相對樣式屬性處於開啟狀態。
flag.HorizontalAlignment = true;
flag.VerticalAlignment = true;
flag.CellShading = true;

// 將樣式套用到範圍。
range1.ApplyStyle(style, flag);
```

這 `StyleFlag` 告訴 Aspose.Cells 要套用哪些樣式屬性 - 對齊、陰影等。這使您可以精細地控制樣式的應用方式。

## 步驟 9：將資料輸入合併範圍

沒有內容的格式化範圍是？讓我們添加一些文字。

```csharp
// 將資料輸入到範圍內。
range1[0, 0].PutValue("Welcome to Aspose APIs.");
```

這會將文字「歡迎使用 Aspose API」放入合併範圍的第一個儲存格中。隨著單元格的合併，該文字將跨越從 D6 到 I12 的所有單元格。

## 步驟10：儲存Excel文件

最後，讓我們將工作簿儲存為 Excel 檔案。

```csharp
// 儲存 Excel 檔案。
wb1.Save(dataDir + "outputMergeCellsInNamedRange.xlsx");
```

在這裡，工作簿以名稱「outputMergeCellsInNamedRange.xlsx」保存在您指定的目錄中。

## 結論

就是這樣！您已成功合併命名範圍內的儲存格、套用一些漂亮的格式，甚至輸入一些資料 - 所有這些都使用 Aspose.Cells for .NET 完成。無論您是在進行報告自動化、Excel 文件操作還是僅僅學習新技術，本逐步指南都應為您提供所需的基礎知識。

## 常見問題解答

### 我可以在 Aspose.Cells 中合併多個不連續的範圍嗎？  
不可以，您只能在 Aspose.Cells 中合併連續的儲存格。

### 我可以透過程式設計撤銷合併操作嗎？  
儲存格合併後，您可以使用 `UnMerge()` Aspose.Cells 中的方法。

### 合併儲存格會刪除其中的資料嗎？  
如果合併之前儲存格中有任何數據，它將保留範圍第一個儲存格的資料。

### 我可以對合併範圍內的單一儲存格套用不同的樣式嗎？  
不可以，合併範圍將充當單一儲存格，因此您無法將不同的樣式套用於其中的個別儲存格。

### 合併後如何存取合併的儲存格？  
合併後，您仍然可以使用合併儲存格的左上角座標存取該儲存格。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}