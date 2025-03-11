---
title: 設定類別數據
linktitle: 設定類別數據
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 在 Excel 圖表中設定類別資料。請按照我們的逐步教學輕鬆實施。
weight: 15
url: /zh-hant/net/advanced-chart-operations/setting-category-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 設定類別數據

## 介紹

以程式設計方式管理和操作 Excel 檔案時，擁有正確的工具可以發揮重要作用。 Aspose.Cells for .NET 就是這樣一款脫穎而出的工具，它允許開發人員輕鬆建立、編輯和轉換 Excel 檔案。無論您是建立複雜的資料分析應用程式還是僅需要自動產生報告，Aspose.Cells 都能滿足您的需求。 

## 先決條件 

在我們深入了解具體細節之前，讓我們確保您已擁有所需的一切：

1. 開發環境：確保您已設定 .NET 開發環境。推薦使用 Visual Studio。
2.  Aspose.Cells for .NET Library：從以下位置下載庫的最新版本[Aspose.Cells 下載頁面](https://releases.aspose.com/cells/net/).
3. C# 的基本了解：熟悉 C# 和 Excel 概念將有助於您更順利地掌握內容。
4. 存取文件：可以訪問[Aspose.Cells 文檔](https://reference.aspose.com/cells/net/)如果您遇到困難，可以提供額外的見解。 

一切就緒後，讓我們逐步解鎖 Excel 操作的魔力。

## 導入包 

在我們開始編碼之前，導入必要的套件至關重要。這使我們能夠存取 Aspose.Cells 提供的功能。

## 步驟1：導入命名空間

首先，讓我們將 Aspose.Cells 命名空間匯入到您的 C# 檔案中。

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

透過在文件頂部包含此行，您可以存取 Aspose.Cells 庫中的所有相關類別和方法。

現在我們已經熟悉了先決條件並匯入了必要的庫，讓我們探討如何在 Excel 圖表中設定類別資料。

## 第 2 步：定義輸出目錄

首先，您需要指定 Excel 檔案的儲存位置。為輸出目錄建立一個變數。 

```csharp
string outputDir = "Your Output Directory";
```

代替`"Your Output Directory"`以及要儲存輸出 Excel 檔案的位置的實際路徑。這可以確保您準確地知道在哪裡可以找到您的成品！

## 第 3 步：實例化工作簿對象

接下來，您將建立 Workbook 物件的新實例。該物件充當 Excel 文件的容器。

```csharp
Workbook workbook = new Workbook();
```

## 第 4 步：存取第一個工作表

您需要使用工作簿中的第一個工作表。存取工作表非常簡單：

```csharp
Worksheet worksheet = workbook.Worksheets[0];
```

指數`0`指向第一個工作表。在 Excel 中，將其視為開啟工作簿中的第一個標籤。

## 第 5 步：將範例值新增至儲存格

讓我們填寫一些要使用的數據。您可以向前兩列新增數值。 

```csharp
worksheet.Cells["A1"].PutValue(10);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(170);
worksheet.Cells["A4"].PutValue(200);
worksheet.Cells["B1"].PutValue(120);
worksheet.Cells["B2"].PutValue(320);
worksheet.Cells["B3"].PutValue(50);
worksheet.Cells["B4"].PutValue(40);
```

在此程式碼片段中，我們使用不同的數值填充行 A1 到 A4，並填入列 B1 到 B4。該數據將作為我們圖表的基礎。

## 第6步：新增類別數據

現在，讓我們標記我們的資料類別。這是在第三列（C 列）中完成的：

```csharp
worksheet.Cells["C1"].PutValue("Q1");
worksheet.Cells["C2"].PutValue("Q2");
worksheet.Cells["C3"].PutValue("Y1");
worksheet.Cells["C4"].PutValue("Y2");
```

在這裡，我們用「Q1」和「Y1」等類別表示每組數據，以便以後更容易解釋我們的圖表。

## 建立圖表

資料準備就緒後，我們就可以新增圖表來直觀地表示這些資料。

## 步驟 7：將圖表新增至工作表

現在，讓我們在工作表上新增一個「柱形」類型的圖表。

```csharp
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
```

此行從工作表的第 5 行和第 0 列開始建立一個新的長條圖。

## 第 8 步：存取圖表實例

在用資料填充圖表之前，我們需要存取新建立的圖表的實例：

```csharp
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

透過這一步，我們現在就可以將資料系列新增到圖表中了。

## 第 9 步：將資料系列新增至圖表中

接下來，您將新增系列集合，它定義圖表將顯示的資料。 

```csharp
chart.NSeries.Add("A1:B4", true);
```

此行指定圖表應取得 A1 到 B4 範圍內的數據，使其能夠直觀地顯示這些值。

## 第10步：設定類別數據

這是關鍵部分——定義我們的類別資料。這就是在 x 軸上標記我們的數據點的內容。

```csharp
chart.NSeries.CategoryData = "C1:C4";
```

透過分配此範圍，我們告訴圖表哪些單元格對應於我們的資料系列中的類別。如果沒有這一步，您的圖表將只是一組數字！

## 第11步：儲存Excel文件

一切準備就緒，是時候保存我們的辛苦工作了。 

```csharp
workbook.Save(outputDir + "outputSettingCategoryData.xlsx");
```

此指令將工作簿保存在指定的輸出目錄中，名稱為「outputSettingCategoryData.xlsx」。 

## 第12步：確認訊息

最後，我們可以加入一些回饋來確認一切順利進行：

```csharp
Console.WriteLine("SettingCategoryData executed successfully.");
```

這會在控制台中列印一條訊息，讓您知道該過程已完成。很簡單，對吧？

## 結論

現在你就擁有了！您已使用 Aspose.Cells for .NET 成功為 Excel 工作簿中的圖表設定類別資料。這種方法的優點在於它允許您自動操作 Excel 文件，而無需在電腦上安裝 Excel。 

## 常見問題解答

### 什麼是 Aspose.Cells？
Aspose.Cells 是一個 .NET 函式庫，用於管理 Excel 文件，而無需 Microsoft Excel。它允許以程式設計方式建立、編輯和轉換 Excel 文件。

### 我可以免費使用 Aspose.Cells 嗎？
是的，您可以免費試用 Aspose.Cells。他們提供免費試用版[這裡](https://releases.aspose.com/).

### Aspose.Cells 適合大型資料集嗎？
絕對地！ Aspose.Cells 旨在有效處理大型資料集，使其成為資料密集型應用程式的可靠選擇。

### 如何使用 Aspose.Cells 新增圖表？
您可以透過建立新的圖表物件並將其連結到包含資料的儲存格區域來新增圖表，如本教學所示。

### 在哪裡可以找到更多使用 Aspose.Cells 的範例？
您可以在以下位置探索更多範例和詳細文檔[Aspose.Cells 文件頁面](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
