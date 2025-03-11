---
title: 在 Excel 中使用自訂排序清單對列中的資料進行排序
linktitle: 在 Excel 中使用自訂排序清單對列中的資料進行排序
second_title: Aspose.Cells .NET Excel 處理 API
description: 在此綜合教學中，了解如何使用 Aspose.Cells for .NET 使用自訂排序清單對 Excel 中的資料進行排序。
weight: 10
url: /zh-hant/net/excel-data-sorting-exporting/sort-data-in-a-column-with-custom-sort-list-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中使用自訂排序清單對列中的資料進行排序

## 介紹

本教學將引導您完成設定項目、載入 Excel 檔案以及使用自訂排序順序對指定範圍內的資料進行排序的過程。透過遵循本指南，您將獲得實務經驗，從而增強您的資料管理技能和 Aspose.Cells 庫的可用性。

## 先決條件

在深入本教程之前，我們先概述一些確保順利學習體驗的先決條件。

### C#基礎知識

雖然本教學旨在引導您完成每個步驟，但對 C# 有基本的了解將使您更容易掌握所介紹的概念。

### .NET開發環境

確保您已設定有效的 .NET 開發環境。您可以使用 Visual Studio 或任何其他支援 .NET 開發的 IDE。

### Aspose.Cells for .NET NuGet 包

您需要在專案中安裝適用於 .NET 的 Aspose.Cells 程式庫。您可以透過 NuGet 套件管理器輕鬆新增它。 

操作方法如下：

1. 在 Visual Studio 中開啟您的專案。
2. 前往「工具」>「NuGet 套件管理器」>「管理解決方案的 NuGet 套件」。
3. 搜尋`Aspose.Cells`並安裝最新版本。

### 用於測試的基本 Excel 文件

您將需要一個範例 Excel 檔案來使用。您可以使用隨機國家/地區名稱及其程式碼建立一個簡單的 Excel 檔案。

## 導入包

首先，讓我們將必要的套件匯入到您的專案中。以下是如何設定程式碼的片段：

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

導入包後，我們就可以繼續前進了。

## 第 1 步：定義來源目錄和輸出目錄 

第一步是定義輸入檔案的位置以及輸出（排序檔案）的儲存位置。您需要指定兩個路徑：一個用於來源 Excel 文件，另一個用於儲存排序後的輸出。

```csharp
string sourceDir = "Your Document Directory\\";
string outputDir = "Your Document Directory\\";
```

## 第 2 步：載入來源 Excel 文件

接下來，我們將載入包含要排序的資料的 Excel 檔案。這是透過建立一個實例來完成的`Workbook`類別並傳遞來源檔案的路徑。

```csharp
Workbook wb = new Workbook(sourceDir + "sampleSortData_CustomSortList.xlsx");
```

## 第 3 步：存取第一個工作表 

載入文件後，我們需要存取包含我們要排序的資料的特定工作表。在本例中，我們的目標是第一個工作表。

```csharp
Worksheet ws = wb.Worksheets[0];
```

## 步驟 4：指定要排序的儲存格區域

我們需要確定要排序的單元格範圍。在此範例中，我們將對單元格從 A1 到 A40 進行排序。使用`CellArea.CreateCellArea`定義單元格區域的方法。

```csharp
CellArea ca = CellArea.CreateCellArea("A1", "A40");
```

## 第 5 步：建立自訂排序列表

在排序之前，我們需要建立用於自訂排序的標準。您可以將排序清單定義為字串陣列。自訂排序清單將決定排序順序。

```csharp
string[] customSortList = new string[] { "USA,US", "Brazil,BR", "China,CN", "Russia,RU", "Canada,CA" };
```

## 第 6 步：新增排序鍵並執行排序

現在是時候排序了！為此，我們將使用 DataSorter 類別。根據我們自訂的清單建立一個用於排序的鍵並執行排序操作。

```csharp
wb.DataSorter.AddKey(0, SortOrder.Ascending, customSortList);
wb.DataSorter.Sort(ws.Cells, ca);
```

## 第 7 步：儲存輸出 Excel 文件

排序完成後，最後一步是將變更儲存到新的 Excel 檔案。指定輸出檔名並儲存工作簿。

```csharp
wb.Save(outputDir + "outputSortData_CustomSortList.xlsx");
```

## 第8步：確認執行成功

為了確保一切順利進行，您可以將確認訊息列印到控制台。這有助於調試並使您對操作成功感到滿意。

```csharp
Console.WriteLine("SortDataInColumnWithCustomSortList executed successfully.\r\n");
```

## 結論

現在你就擁有了！您已使用 Aspose.Cells for .NET 使用自訂排序清單成功對 Excel 列中的資料進行排序。排序有助於使資料變得結構化和清晰，使其更易於分析和解釋。我希望本指南能夠將您的技能提升到一個新的水平，並幫助您認識到 Aspose.Cells 對於您的 Excel 相關任務有多強大。

## 常見問題解答

### 什麼是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一個綜合程式庫，可讓您在 .NET 應用程式中操作 Excel 文件，包括建立、編輯和轉換它們。

### 我可以使用自訂排序清單對多列進行排序嗎？
是的！如果需要，您可以新增其他按鍵以按多列排序，只需對每個鍵執行相同的過程即可。

### 我需要具備 C# 知識才能使用 Aspose.Cells 嗎？
雖然它很有幫助，但您可以按照本教程進行學習！對 C# 有一些基本的了解將增強您的學習體驗。

### 是否可以使用 Aspose.Cells 的臨時授權？
絕對地！如果您想不受限制地測試該程式庫的全部功能，您可以獲得臨時許可證。

### 我可以下載 Aspose.Cells 的範例或文件嗎？
是的！ Aspose 提供了大量的文件和範例項目，可以為您提供很大的幫助。查看[Aspose.Cells 文檔](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
