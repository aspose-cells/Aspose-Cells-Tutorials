---
"description": "了解如何使用 Aspose.Cells 以程式設計方式對 .NET 中的資料透視表進行排序。逐步指南涵蓋設定、配置、排序以及將結果儲存為 Excel 和 PDF 檔案。"
"linktitle": "在 .NET 中以程式設計方式對資料透視表進行自訂排序"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 .NET 中以程式設計方式對資料透視表進行自訂排序"
"url": "/zh-hant/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/"
"weight": 29
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以程式設計方式對資料透視表進行自訂排序

## 介紹
當談到在 .NET 環境中使用 Excel 時，有一個函式庫脫穎而出：Aspose.Cells。現在，當一個工具允許您以程式設計方式操作電子表格時，您不喜歡它嗎？這正是 Aspose.Cells 所做的！在今天的教學中，我們將深入探討資料透視表的世界，並向您展示如何使用這個多功能函式庫以程式設計方式實作自訂排序。
## 先決條件
在我們捲起袖子開始編寫程式碼之前，請確保您已準備好以下幾件事：
1. Visual Studio：您需要一個可運行的 Visual Studio 版本。這是發生一切奇蹟的遊樂場。
2. .NET Framework：熟悉.NET 程式設計至關重要。無論您是 .NET Core 還是 .NET Framework 愛好者，都可以開始了。
3. Aspose.Cells 函式庫：您需要安裝 Aspose.Cells 函式庫。您可以從 [下載連結](https://releases.aspose.com/cells/net/) 並將其添加到您的項目中。
4. 對資料透視表的基本了解：雖然您不需要成為專家，但在學習本教學課程時，了解一些有關資料透視表工作原理的知識將會很有幫助。
5. 範例 Excel 文件：有一個名為的範例 Excel 文件 `SamplePivotSort.xlsx` 已準備好在您的工作目錄中進行測試。
## 導入包
一旦滿足了所有先決條件，第一步就是匯入必要的套件。為此，請在程式碼頂部包含以下幾行：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
該軟體包提供了使用 Aspose.Cells 操作 Excel 檔案所需的所有功能。

好吧，讓我們進入有趣的部分！我們將把建立資料透視表和應用自訂排序的過程分解為可管理的步驟。
## 步驟 1：設定工作簿
首先，我們需要設定我們的工作簿。以下是操作方法：
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
在此步驟中，我們初始化一個新的 `Workbook` 實例與我們的 Excel 檔案的路徑。這充當了我們的數據透視表生動呈現的畫布。
## 第 2 步：訪問工作表
接下來，我們需要存取將新增資料透視表的工作表。
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
在這裡，我們抓取工作簿中的第一個工作表並調用 `PivotTableCollection`。此集合允許我們管理此工作表上的所有資料透視表。
## 步驟3：建立您的第一個資料透視表
現在是時候建立我們的資料透視表了。
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
我們在工作表中新增一個新的資料透視表，指定資料範圍及其位置。 “E3”表示我們希望資料透視表開始的位置。然後我們使用其索引來引用這個新的資料透視表。
## 步驟 4：配置資料透視表設置
讓我們配置我們的資料透視表！這意味著控制總數和現場安排等方面。
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
我們確保不顯示行和列的總計，這可以使資料更乾淨。然後我們將第一個欄位新增到行區域，啟用自動排序和升序排序。
## 步驟 5：新增列和資料字段
設定好行之後，我們來新增列和資料欄位。
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
我們將第二個欄位新增為一列並將其格式化為日期。再次，我們啟用自動排序和升序排列來保持內容井然有序。最後，我們需要將第三個欄位新增到我們的資料區域：
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## 步驟 6：刷新並計算資料透視表
在新增所有必要的欄位後，請確保我們的資料透視表是最新的並且已準備就緒。
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
這些方法會刷新資料並重新計算，確保所有內容都是最新的並正確顯示在資料透視表中。
## 步驟 7：根據行字段值進行自訂排序
讓我們透過根據特定值（例如“海鮮”）對資料透視表進行排序來添加一些特色。
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
我們透過建立另一個資料透視表並進行與第一個類似的設定來重複此過程。我們現在可以進一步定制它：
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## 步驟 8：額外的排序自訂讓我們嘗試另一種基於特定日期的排序方法：
```csharp
// 新增另一個資料透視表以按日期排序
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// 重複與前面步驟類似的行和列設置
```
您只需重複相同的過程，創建第三個資料透視表，並根據您的需求自訂其排序標準。
## 步驟 9：保存工作簿時間來保存我們投入的所有辛勤工作！
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
在這裡，您可以將工作簿儲存為 Excel 檔案和 PDF。這 `PdfSaveOptions` 允許更好的格式化，確保轉換時每張表都出現在單獨的頁面上。
## 步驟 10：完成，讓使用者知道一切都很酷。
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## 結論
到目前為止，您已經了解如何利用 Aspose.Cells 的強大功能在 .NET 應用程式中建立和自訂資料透視表。從初始設定到自訂排序，每個步驟結合提供無縫體驗。無論您需要展示年度銷售數據還是追蹤庫存統計數據，這些技能都會為您提供幫助！
## 常見問題解答
### 什麼是資料透視表？
資料透視表是 Excel 中的一種資料處理工具，可讓您匯總和分析數據，從而提供一種靈活的方式來輕鬆提取見解。
### 如何安裝 Aspose.Cells？
您可以透過 Visual Studio 中的 NuGet 安裝它，或直接從 [下載連結](https://releases。aspose.com/cells/net/).
### Aspose.Cells 有試用版嗎？
是的！您可以存取以下網址免費試用 [免費試用連結](https://releases。aspose.com/).
### 我可以對資料透視表中的多個欄位進行排序嗎？
絕對地！您可以根據需要新增和排序多個欄位。
### 在哪裡可以找到對 Aspose.Cells 的支援？
社群非常活躍，您可以在他們的論壇上提問 [這裡](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}