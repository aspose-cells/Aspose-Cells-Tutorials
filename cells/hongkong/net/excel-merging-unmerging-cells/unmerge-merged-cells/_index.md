---
title: 在 Excel 中取消合併合併的儲存格
linktitle: 在 Excel 中取消合併合併的儲存格
second_title: Aspose.Cells .NET Excel 處理 API
description: 使用 Aspose.Cells for .NET 輕鬆取消合併 Excel 中的合併儲存格。按照我們的逐步指南創建更好的電子表格。
weight: 10
url: /zh-hant/net/excel-merging-unmerging-cells/unmerge-merged-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中取消合併合併的儲存格

## 介紹

您是否厭倦了處理 Excel 電子表格中的合併儲存格？你並不孤單！合併單元格對於格式化來說是一個方便的功能，但在資料操作和分析方面它們通常會帶來麻煩。但你猜怎麼著？取消合併那些討厭的單元格比您想像的要容易，尤其是當您使用 Aspose.Cells for .NET 時。在本文中，我將引導您逐步了解如何取消合併合併的儲存格，確保您的資料整齊、整潔並準備好採取行動！所以，拿起你的編碼帽，讓我們深入 Aspose.Cells 的世界。

## 先決條件

在我們開始動手之前，您需要準備好一些必需品：

### C# 和 .NET Framework 的基礎知識
如果您熟悉 C# 程式設計並對 .NET 框架有基本的了解，那麼您已經有了一個很好的開始。如果沒有，別擔心！本教程旨在簡單明了，因此您將在過程中掌握必要的概念。

### Aspose.Cells 庫
確保您的 .NET 環境中安裝了 Aspose.Cells 函式庫。您可以通過訪問輕鬆獲得此信息[Aspose.Cells 下載頁面](https://releases.aspose.com/cells/net/).

### IDE設定
您應該設定一個開發環境，例如 Visual Studio，您可以在其中編寫和執行 C# 程式碼。

### Excel 檔案範例
取得包含一些合併儲存格的範例 Excel 檔案 - 您將使用此檔案來練習取消合併。

解決完所有這些先決條件後，我們現在可以進入令人興奮的部分——編寫我們的解決方案！

## 導入包

首先，讓我們導入必要的套件。使用 Aspose.Cells，您將與各種類別進行交互，以有效地管理您的 Excel 檔案。以下是您需要在 C# 檔案頂部包含的內容：

```csharp
using System;
using System.IO;

using Aspose.Cells;
```

透過包含此軟體包，您將可以存取 Aspose.Cells 提供的所有功能。

讓我們將取消合併過程分解為可管理的步驟。每個步驟都將被明確定義，以便您可以輕鬆遵循。

## 第 1 步：定義目錄

第一步是定義輸入 Excel 檔案（包含合併儲存格的檔案）和輸出檔案（將儲存未合併資料的檔案）所在的目錄。設定方法如下：

```csharp
//原始碼目錄
string sourceDir = "Your Document Directory"; 

//輸出目錄
string outputDir = "Your Document Directory"; 
```

確保更換`"Your Document Directory"`與文件的實際路徑。

## 第 2 步：建立工作簿

現在您已經設定了目錄，是時候建立 Workbook 物件了。該物件將允許您操作 Excel 檔案。您可以使用以下程式碼來執行此操作：

```csharp
//建立工作簿
Workbook wbk = new Aspose.Cells.Workbook(sourceDir + "sampleUnMergingtheMergedCells.xlsx");
```

此行程式碼讀取範例 Excel 檔案並準備對其進行處理。 

## 第 3 步：訪問工作表

每個工作簿都由工作表組成。您需要存取要取消合併儲存格的特定工作表。具體做法如下：

```csharp
//建立一個工作表並取得第一個工作表
Worksheet worksheet = wbk.Worksheets[0];
```

此程式碼取得第一個工作表。如果合併的儲存格位於不同的工作表上，請相應地更新索引。

## 步驟 4：存取工作表中的儲存格

接下來，您需要取得工作表中儲存格的參考。這可以使用以下方法來完成：

```csharp
//建立一個 Cells 物件來取得所有儲存格
Cells cells = worksheet.Cells;
```

透過這一行，您現在可以存取工作表上的所有儲存格，從而可以根據需要操作它們。

## 第 5 步：取消合併儲存格

關鍵的一步來了－取消細胞合併！您需要指定要取消合併的合併儲存格的範圍。使用以下程式碼：

```csharp
//取消合併儲存格
cells.UnMerge(5, 2, 2, 3);
```

在此範例中，`UnMerge`方法採用四個參數：起始行索引 (5)、起始列索引 (2)、要取消合併的行數 (2) 和要取消合併的列數 (3)。調整這些參數以符合 Excel 檔案中的特定合併儲存格。

## 第 6 步：儲存工作簿

取消合併後，您需要將變更儲存到新的 Excel 檔案。具體做法如下：

```csharp
//儲存檔案
wbk.Save(outputDir + "outputUnMergingtheMergedCells.xlsx");
```

此行將未合併的資料保存在指定的輸出目錄中。就這麼簡單！

## 第7步：確認流程

最後，確認一切順利是個好主意。您可以在控制台列印一則訊息，讓您知道操作執行成功：

```csharp
Console.WriteLine("UnMerging the Cells executed successfully.");
```

現在你就擁有了！您已使用 Aspose.Cells for .NET 成功取消合併 Excel 檔案中的儲存格。

## 結論

取消合併儲存格可能看起來很乏味，尤其是在處理大型電子表格時，但使用 Aspose.Cells for .NET，這一切變得輕而易舉！本教學將引導您完成從設定環境到執行有效取消合併單元所需的程式碼的所有內容。 Aspose.Cells 庫提供的靈活性使您能夠有效地處理電子表格，使其成為處理 Excel 文件的開發人員的理想選擇。因此，潛入並開始享受更乾淨、更易於管理的電子表格。

## 常見問題解答

### 什麼是 Aspose.Cells？  
Aspose.Cells 是一個功能強大的程式庫，用於在 .NET 應用程式中建立、操作和轉換 Excel 文件。

### 我需要許可證才能使用 Aspose.Cells 嗎？  
雖然 Aspose.Cells 提供免費試用，但完整使用需要授權。你可以獲得一個[臨時許可證在這裡](https://purchase.aspose.com/temporary-license/).

### 我可以一次取消合併多個工作表中的儲存格嗎？  
是的，您可以循環瀏覽工作簿中的多個工作表並根據需要取消合併儲存格。

### Aspose.Cells 與 .NET Core 相容嗎？  
是的，Aspose.Cells 與 .NET Core 相容，使其適用於各種 .NET 應用程式。

### 在哪裡可以找到有關 Aspose.Cells 的更多文件？  
您可以瀏覽完整的文檔[Aspose.Cells 參考頁](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
