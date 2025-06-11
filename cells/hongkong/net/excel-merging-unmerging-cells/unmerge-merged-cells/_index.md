---
"description": "使用 Aspose.Cells for .NET 輕鬆取消合併 Excel 中的儲存格。按照我們的逐步指南創建更好的電子表格。"
"linktitle": "在 Excel 中取消合併儲存格"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 Excel 中取消合併儲存格"
"url": "/zh-hant/net/excel-merging-unmerging-cells/unmerge-merged-cells/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中取消合併儲存格

## 介紹

您是否厭倦了處理 Excel 電子表格中的合併儲存格？你並不孤單！合併儲存格對於格式化來說可能是一個方便的功能，但在資料操作和分析時，它們往往會導致麻煩。但你猜怎麼著？取消合併這些討厭的單元格比您想像的要容易 - 尤其是當您使用 Aspose.Cells for .NET 時。在本文中，我將逐步引導您完成如何取消合併儲存格，確保您的資料整潔、有序且可立即操作！所以，戴上你的編碼帽，讓我們深入了解 Aspose.Cells 的世界。

## 先決條件

在我們開始之前，您需要準備好一些必需品：

### C# 和 .NET Framework 的基礎知識
如果您熟悉 C# 程式設計並對 .NET 框架有基本的了解，那麼您已經有了一個很好的開始。如果沒有，別擔心！本教程設計得非常簡單，因此您可以在學習過程中掌握必要的概念。

### Aspose.Cells 庫
確保您的.NET環境中安裝了Aspose.Cells庫。您可以透過訪問 [Aspose.Cells下載頁面](https://releases。aspose.com/cells/net/).

### IDE 設定
您應該設定一個開發環境，例如 Visual Studio，您可以在其中編寫和執行 C# 程式碼。

### 範例 Excel 文件
取得包含一些合併儲存格的範例 Excel 檔案 - 您將使用此檔案來練習取消合併。

滿足了所有這些先決條件後，我們現在可以進入令人興奮的部分 - 編寫解決方案！

## 導入包

首先，讓我們導入必要的套件。使用 Aspose.Cells，您將與各種類別進行互動以有效地管理您的 Excel 檔案。以下是您需要在 C# 檔案頂部包含的內容：

```csharp
using System;
using System.IO;

using Aspose.Cells;
```

透過包含此包，您將可以存取 Aspose.Cells 提供的所有功能。

讓我們將拆分過程分解為易於管理的步驟。每個步驟都將被清晰地定義，以便您可以輕鬆遵循。

## 步驟 1：定義目錄

第一步是定義輸入 Excel 檔案（包含合併儲存格的檔案）和輸出檔案（儲存未合併資料的檔案）所在的目錄。設定方法如下：

```csharp
// 來源目錄
string sourceDir = "Your Document Directory"; 

// 輸出目錄
string outputDir = "Your Document Directory"; 
```

確保更換 `"Your Document Directory"` 使用文件的實際路徑。

## 步驟 2：建立工作簿

現在您已經設定了目錄，接下來該建立 Workbook 物件了。該物件將允許您操作 Excel 檔案。您可以使用以下程式碼執行此操作：

```csharp
// 建立工作簿
Workbook wbk = new Aspose.Cells.Workbook(sourceDir + "sampleUnMergingtheMergedCells.xlsx");
```

這行程式碼讀取您的範例 Excel 檔案並準備進行處理。 

## 步驟 3：存取工作表

每個工作簿都由工作表組成。您需要存取想要取消合併儲存格的特定工作表。具體操作如下：

```csharp
// 建立工作表並取得第一張工作表
Worksheet worksheet = wbk.Worksheets[0];
```

此程式碼抓取第一個工作表。如果合併的儲存格位於不同的工作表上，請相應地更新索引。

## 步驟 4：存取工作表中的儲存格

接下來，您需要取得工作表中儲存格的參考。這可以透過以下方式實現：

```csharp
// 建立一個 Cells 物件來取得所有儲存格
Cells cells = worksheet.Cells;
```

透過此行，您現在可以存取工作表上的所有儲存格，並可以根據需要進行操作。

## 步驟 5：取消合併儲存格

接下來是關鍵的一步－分離細胞！您需要指定要取消合併的合併儲存格的範圍。使用以下程式碼：

```csharp
// 取消合併儲存格
cells.UnMerge(5, 2, 2, 3);
```

在此範例中， `UnMerge` 方法採用四個參數：起始行索引 (5)、起始列索引 (2)、要取消合併的行數 (2) 和要取消合併的列數 (3)。調整這些參數以符合 Excel 檔案中的特定合併儲存格。

## 步驟 6：儲存工作簿

取消合併後，您需要將變更儲存到新的 Excel 檔案。具體操作如下：

```csharp
// 儲存檔案
wbk.Save(outputDir + "outputUnMergingtheMergedCells.xlsx");
```

此行將未合併的資料保存在指定的輸出目錄中。就這麼簡單！

## 步驟7：確認流程

最後，最好確認一切進展順利。您可以向控制台列印一則訊息，讓您知道操作已成功執行：

```csharp
Console.WriteLine("UnMerging the Cells executed successfully.");
```

就是這樣！您已成功使用 Aspose.Cells for .NET 取消合併 Excel 檔案中的儲存格。

## 結論

取消合併單元格可能看起來很繁瑣，特別是在處理大型電子表格時，但使用 Aspose.Cells for .NET，這一切都變得輕而易舉！本教學將引導您完成從設定環境到執行有效取消合併儲存格所需的程式碼的所有內容。 Aspose.Cells 庫提供的靈活性使您能夠有效地處理電子表格，使其成為使用 Excel 文件的開發人員的理想選擇。因此，深入研究並開始享受更清晰、更易於管理的電子表格。

## 常見問題解答

### 什麼是 Aspose.Cells？  
Aspose.Cells 是一個功能強大的程式庫，用於在 .NET 應用程式中建立、操作和轉換 Excel 文件。

### 我需要許可證才能使用 Aspose.Cells 嗎？  
雖然 Aspose.Cells 提供免費試用，但需要許可證才能完全使用。您可以獲得 [此處為臨時駕照](https://purchase。aspose.com/temporary-license/).

### 我可以一次取消合併多張工作表中的儲存格嗎？  
是的，您可以循環遍歷工作簿中的多個工作表並根據需要取消合併儲存格。

### Aspose.Cells 與 .NET Core 相容嗎？  
是的，Aspose.Cells 與 .NET Core 相容，使其適用於各種 .NET 應用程式。

### 在哪裡可以找到有關 Aspose.Cells 的更多文件？  
您可以在 [Aspose.Cells 參考頁面](https://reference。aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}