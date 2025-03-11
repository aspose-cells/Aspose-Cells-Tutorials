---
title: 在 .NET 中以程式設計方式自訂資料透視表排序
linktitle: 在 .NET 中以程式設計方式自訂資料透視表排序
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells 以程式設計方式對 .NET 中的資料透視表進行排序。逐步指南涵蓋設定、配置、排序以及將結果儲存為 Excel 和 PDF 檔案。
weight: 29
url: /zh-hant/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以程式設計方式自訂資料透視表排序

## 介紹
當談到在 .NET 環境中使用 Excel 時，有一個函式庫脫穎而出：Aspose.Cells。現在，當一個工具允許您以程式設計方式操作電子表格時，您不喜歡它嗎？這正是 Aspose.Cells 所做的！在今天的教學中，我們將深入了解資料透視表的世界，並向您展示如何使用這個多功能函式庫以程式設計方式實作自訂排序。
## 先決條件
在我們捲起袖子開始編寫程式碼之前，請確保您已經做好了一些準備工作：
1. Visual Studio：您需要 Visual Studio 的工作版本。這是所有魔法發生的遊樂場。
2. .NET Framework：熟悉 .NET 程式設計至關重要。無論您是 .NET Core 還是 .NET Framework 愛好者，都可以開始使用。
3.  Aspose.Cells 函式庫：您需要安裝Aspose.Cells 函式庫。您可以從[下載連結](https://releases.aspose.com/cells/net/)並將其添加到您的項目中。
4. 對資料透視表的基本了解：雖然您不需要成為專家，但在我們學習本教學時，了解一些有關資料透視表如何運作的知識將會很有幫助。
5. 範例 Excel 檔案：有一個名為`SamplePivotSort.xlsx`準備好在您的工作目錄中進行測試。
## 導入包
整理好所有先決條件後，第一步就是匯入必要的套件。為此，請在程式碼頂部添加以下行：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
該軟體包提供了使用 Aspose.Cells 操作 Excel 檔案所需的所有功能。

好了，讓我們進入有趣的部分吧！我們將把建立資料透視表和應用自訂排序的過程分解為可管理的步驟。
## 第 1 步：設定工作簿
首先，我們需要設定工作簿。操作方法如下：
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
在這一步驟中，我們初始化一個新的`Workbook`實例與我們的 Excel 檔案的路徑。這將充當我們的數據透視表的畫布。
## 第 2 步：訪問工作表
接下來，我們需要存取將在其中新增資料透視表的工作表。
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
在這裡，我們獲取工作簿中的第一個工作表並調用`PivotTableCollection`。該集合允許我們管理該工作表上的所有資料透視表。
## 第 3 步：建立您的第一個資料透視表
現在是時候建立我們的資料透視表了。
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
我們在工作表中新增一個新的資料透視表，指定資料範圍及其位置。 “E3”表示我們希望資料透視表開始的位置。然後，我們使用其索引來引用這個新的資料透視表。
## 步驟 4：配置資料透視表設置
讓我們配置我們的資料透視表！這意味著控制總計和現場安排等方面。
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
我們確保不顯示行和列的總計，這可以使資料更清晰。然後，我們將第一個欄位新增至行區域，啟用自動排序和升序排序。
## 第 5 步：新增列和資料字段
設定行後，讓我們新增列和資料欄位。
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
我們將第二個欄位新增為列並將其格式設為日期。再次，我們啟用自動排序和升序以保持事物井井有條。最後，我們需要將第三個欄位新增到我們的資料區域：
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## 步驟 6：刷新並計算資料透視表
在添加所有必要的欄位後，讓我們確保我們的資料透視表是新鮮且準備就緒的。
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
這些方法會刷新資料並重新計算，確保所有內容都是最新的並在我們的資料透視表中正確顯示。
## 步驟 7：根據行字段值自訂排序
讓我們根據特定值（例如“SeaFood”）對資料透視表進行排序來添加一些技巧。
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
我們透過建立另一個資料透視表並以與第一個資料透視表類似的方式對其進行設定來重複此過程。我們現在可以進一步定制它：
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## 步驟 8：其他排序自訂讓我們嘗試另一種基於特定日期的排序方法：
```csharp
//新增另一個資料透視表以按日期排序
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
//重複與先前步驟類似的行和列設置
```
您只需迭代相同的流程，建立第三個資料透視表，並根據您的需求自訂其排序標準。
## 步驟9：保存工作簿時間以節省我們所付出的所有努力！
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
在這裡，您將工作簿儲存為 Excel 檔案和 PDF。這`PdfSaveOptions`允許更好的格式設置，確保轉換時每個工作表都顯示在單獨的頁面上。
## 第 10 步：完成 讓使用者知道一切都很酷，從而結束一切。
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## 結論
到目前為止，您已經學習如何利用 Aspose.Cells 的強大功能在 .NET 應用程式中建立和自訂資料透視表。從初始設定到自訂排序，每個步驟結合以提供無縫體驗。無論您需要呈現年度銷售數據還是追蹤庫存統計數據，這些技能都將為您提供幫助！
## 常見問題解答
### 什麼是資料透視表？
資料透視表是 Excel 中的一種資料處理工具，可讓您匯總和分析數據，提供靈活的方式輕鬆提取見解。
### 如何安裝 Aspose.Cells？
您可以透過 Visual Studio 中的 NuGet 安裝它，或直接從[下載連結](https://releases.aspose.com/cells/net/).
### Aspose.Cells 有試用版嗎？
是的！您可以造訪以下網站免費試用[免費試用連結](https://releases.aspose.com/).
### 我可以對資料透視表中的多個欄位進行排序嗎？
絕對地！您可以根據需要新增多個欄位並對其進行排序。
### 在哪裡可以找到對 Aspose.Cells 的支援？
社群非常活躍，您可以在他們的論壇上提問[這裡](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
