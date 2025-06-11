---
"description": "了解如何使用 Aspose.Cells for .NET 在 Excel 圖表中設定類別資料。按照我們的逐步教學即可輕鬆實現。"
"linktitle": "設定類別數據"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "設定類別數據"
"url": "/zh-hant/net/advanced-chart-operations/setting-category-data/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 設定類別數據

## 介紹

當以程式方式管理和操作 Excel 檔案時，擁有正確的工具可以發揮重要作用。 Aspose.Cells for .NET 就是這樣一種工具，它允許開發人員毫不費力地建立、編輯和轉換 Excel 檔案。無論您是建立複雜的資料分析應用程式還是僅需要自動產生報告，Aspose.Cells 都能滿足您的需求。 

## 先決條件 

在深入探討細節之前，讓我們確保您已獲得所需的一切：

1. 開發環境：確保您已設定.NET 開發環境。建議使用 Visual Studio。
2. Aspose.Cells for .NET Library：從下載最新版本的函式庫 [Aspose.Cells 下載頁面](https://releases。aspose.com/cells/net/).
3. 對 C# 的基本了解：熟悉 C# 和 Excel 概念將幫助您更順利地掌握內容。
4. 存取文件：可以訪問 [Aspose.Cells文檔](https://reference.aspose.com/cells/net/) 如果你遇到困難，可以提供額外的見解。 

一切準備就緒後，讓我們逐步揭開 Excel 操作的魔力。

## 導入包 

在我們開始編碼之前，導入必要的套件至關重要。這使我們能夠存取 Aspose.Cells 提供的功能。

## 步驟 1：導入命名空間

首先，讓我們將 Aspose.Cells 命名空間匯入到您的 C# 檔案中。

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

透過在文件頂部包含此行，您可以存取 Aspose.Cells 庫中的所有相關類別和方法。

現在我們已經熟悉了先決條件並導入了必要的庫，讓我們探索如何在 Excel 圖表中設定類別資料。

## 第 2 步：定義輸出目錄

首先，您需要指定 Excel 檔案的儲存位置。為您的輸出目錄建立一個變數。 

```csharp
string outputDir = "Your Output Directory";
```

代替 `"Your Output Directory"` 使用您想要儲存輸出 Excel 檔案的位置的實際路徑。這可確保您確切地知道在哪裡找到您的成品！

## 步驟3：實例化工作簿對象

接下來，您將建立 Workbook 物件的新實例。該物件充當 Excel 文件的容器。

```csharp
Workbook workbook = new Workbook();
```

## 步驟 4：訪問第一個工作表

您需要使用工作簿中的第一個工作表。存取工作表非常簡單：

```csharp
Worksheet worksheet = workbook.Worksheets[0];
```

索引 `0` 指向第一個工作表。在 Excel 中，可以將其視為開啟工作簿中的第一個標籤。

## 步驟5：向儲存格新增範例值

讓我們填寫一些數據以供使用。您可以向前兩列新增數值。 

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

在此程式碼片段中，我們用不同的數值填入行 A1 至 A4，並填入列 B1 至 B4。這些數據將作為我們圖表的基礎。

## 步驟6：新增類別數據

現在，讓我們標記我們的資料類別。這是在第三列（C 列）中完成的：

```csharp
worksheet.Cells["C1"].PutValue("Q1");
worksheet.Cells["C2"].PutValue("Q2");
worksheet.Cells["C3"].PutValue("Y1");
worksheet.Cells["C4"].PutValue("Y2");
```

在這裡，我們用「Q1」和「Y1」等類別來表示每組數據，以便以後更容易解釋我們的圖表。

## 建立圖表

有了數據後，我們就可以加入圖表來直觀地表示這些數據了。

## 步驟 7：在工作表中新增圖表

現在，讓我們在工作表上新增一個「柱形」類型的圖表。

```csharp
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
```

此行從工作表的第 5 行和第 0 列開始建立一個新的長條圖。

## 步驟8：存取圖表實例

在我們用資料填充圖表之前，我們需要存取新建立的圖表的實例：

```csharp
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

透過此步驟，我們現在可以將資料系列新增至圖表。

## 步驟9：在圖表中新增資料系列

接下來，您將新增系列集合，它定義圖表將顯示的資料。 

```csharp
chart.NSeries.Add("A1:B4", true);
```

此行指定圖表應從 A1 到 B4 範圍取得數據，以便直觀地顯示這些值。

## 步驟10：設定類別數據

接下來是關鍵部分——定義我們的類別資料。這就是 x 軸上的資料點標籤。

```csharp
chart.NSeries.CategoryData = "C1:C4";
```

透過分配這個範圍，我們可以告訴圖表哪些單元格對應於我們的資料系列中的類別。如果沒有這一步，您的圖表就只是一組數字！

## 步驟11：儲存Excel文件

一切設定完畢後，就該保存我們的辛苦工作成果了。 

```csharp
workbook.Save(outputDir + "outputSettingCategoryData.xlsx");
```

此指令將您的工作簿以「outputSettingCategoryData.xlsx」名稱儲存在指定的輸出目錄中。 

## 步驟12：確認訊息

最後，我們可以加入一些回饋來確認一切順利進行：

```csharp
Console.WriteLine("SettingCategoryData executed successfully.");
```

這會在控制台中列印一條訊息，讓您知道該過程已完成。很簡單，對吧？

## 結論

就是這樣！您已成功使用 Aspose.Cells for .NET 為 Excel 工作簿中的圖表設定類別資料。這種方法的優點在於它允許您自動執行 Excel 檔案操作，而無需在電腦上安裝 Excel。 

## 常見問題解答

### 什麼是 Aspose.Cells？
Aspose.Cells 是一個無需 Microsoft Excel 即可管理 Excel 檔案的 .NET 程式庫。它允許以程式設計方式建立、編輯和轉換 Excel 文件。

### 我可以免費使用 Aspose.Cells 嗎？
是的，您可以免費試用 Aspose.Cells。他們提供免費試用版 [這裡](https://releases。aspose.com/).

### Aspose.Cells 適合大型資料集嗎？
絕對地！ Aspose.Cells 旨在有效處理大型資料集，使其成為資料密集型應用程式的可靠選擇。

### 如何使用 Aspose.Cells 新增圖表？
您可以透過建立新的圖表物件並將其連結到包含資料的儲存格範圍來新增圖表，如本教學所示。

### 在哪裡可以找到更多使用 Aspose.Cells 的範例？
您可以在以下位置探索更多範例和詳細文檔 [Aspose.Cells文件頁面](https://reference。aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}