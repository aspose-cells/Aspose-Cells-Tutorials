---
title: 在 .NET 中以程式設計方式設定頁面欄位格式
linktitle: 在 .NET 中以程式設計方式設定頁面欄位格式
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 以程式設計方式設定資料透視表中的頁面欄位格式。按照我們的逐步教學進行無縫資料管理。
weight: 21
url: /zh-hant/net/creating-and-configuring-pivot-tables/setting-page-field-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以程式設計方式設定頁面欄位格式

## 介紹
透過程式碼建立和操作 Excel 檔案非常有用，尤其是當您需要分析大型資料集時。 Aspose.Cells for .NET 是您武器庫中最出色的工具之一，它允許您以程式設計方式與 Excel 檔案互動並建立複雜的報表結構。在本教程中，我們將深入研究如何使用這個強大的庫在資料透視表中設定頁面欄位格式。無論您是經驗豐富的開發人員還是初學者，在本指南結束時，您都將深入掌握如何在 .NET 中使用資料透視表及其各種設定。
## 先決條件
在我們開始編碼之前，讓我們確保一切都設定正確。您將需要以下內容：
- Visual Studio：一個可以編寫和執行 .NET 程式碼的工作環境。
-  Aspose.Cells：您可以下載資料庫[這裡](https://releases.aspose.com/cells/net/).
- C# 基礎知識：熟悉 C# 程式設計將有助於您更好地理解程式碼片段。
-  Excel 檔案：準備好 Excel 檔案（例如`Book1.xls`）包含適合建立資料透視表的資料。 
如果您還沒有，請免費試用 Aspose.Cells[這裡](https://releases.aspose.com/).
## 導入包
首先，您需要在專案中匯入正確的套件。首先在 C# 專案中加入 Aspose.Cells 函式庫的參考。操作方法如下：
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
這將引入使用 Aspose.Cells 操作 Excel 檔案所需的所有必要的類別和方法。
## 第 1 步：設定您的工作區
首先定義將儲存 Excel 檔案的工作目錄。例如，您可以像這樣宣告一個變數：
```csharp
string dataDir = "Your Document Directory";
```
## 載入工作簿
接下來，我們需要載入 Excel 範本。這是一個重要的步驟，因為它為我們的操作建立了背景：
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
此行從指定目錄載入現有工作簿。
## 第 2 步：訪問工作表
載入工作簿後，就可以存取包含資料透視表或要分析的資料的工作表了。您可以按照以下方法執行此操作：
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
這將取得已載入工作簿的第一個工作表。如果您正在使用多個工作表，則可以輕鬆修改索引。
## 第 3 步：存取資料透視表
繼續，讓我們存取所選工作表中的資料透視表。如果您使用單一資料透視表，則可以將其索引設為`0`：
```csharp
int pivotindex = 0;
//存取資料透視表
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
此程式碼片段選擇工作表中的第一個資料透視表。 
## 步驟 4：設定資料透視表
現在到了令人興奮的部分！讓我們設定資料透視表以顯示行的總計：
```csharp
pivotTable.RowGrand = true;
```
該行確保您的報告將顯示總計，這對於數據分析來說是有用的摘要。
## 第 5 步：存取和配置行字段
接下來，我們需要存取資料透視表的行字段：
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.RowFields;
```
此集合允許我們根據需要操作欄位。
## 配置第一行字段
想要設定特定的小計類型？讓我們訪問集合中的第一個字段並配置它：
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
//設定小計。
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
透過啟用`Sum`和`Count`小計，我們可以快速總結報告中的數據。
## 第 6 步：設定自動排序選項
接下來，讓我們進行一些智慧排序。這樣，您的資料透視表將以有意義的順序排列資料：
```csharp
//設定自動排序選項。
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; //使用預定義的排序欄位。
```
此程式碼片段啟用自動排序並指定升序。 
## 第 7 步：設定自動顯示選項
您想進一步過濾您的資料嗎？自動顯示選項有助於在定義的條件下顯示特定的資料點：
```csharp
//設定自動顯示選項。
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; //指定要自動顯示的欄位。
```
這可確保您的數據透視表僅顯示相關數據，從而增強清晰度和焦點。
## 第 8 步：儲存您的工作
完成所有這些配置後，您不想丟失您的工作！像這樣儲存修改後的工作簿：
```csharp
workbook.Save(dataDir + "output.xls");
```
現在，您可以在文件目錄中找到新建立的 Excel 檔案。
## 結論
現在你就擁有了！我們已經介紹了使用 Aspose.Cells for .NET 在資料透視表中以程式設計方式設定頁面欄位格式的全面且實用的方法。透過提供的簡單步驟，您應該可以放心地修改 Excel 資料以滿足您的報表需求。當您將 C# 的強大功能與 Aspose.Cells 結合時，您所取得的成就令人難以置信。
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個 .NET 函式庫，可讓開發人員以程式設計方式建立、操作和轉換 Excel 檔案。
### 如何安裝 Aspose.Cells？
您可以直接從[阿斯普斯網站](https://releases.aspose.com/cells/net/).
### 我可以在沒有安裝 Excel 的情況下使用 Aspose.Cells 嗎？
是的，Aspose.Cells 是一個獨立的函式庫，不需要安裝 Microsoft Excel。
### 在哪裡可以找到詳細的支援？
您可以訪問詳細的支援和論壇：[阿斯普斯支持](https://forum.aspose.com/c/cells/9).
### 我怎麼才能獲得臨時許可證？
您可以從以下位置取得臨時許可證[這裡](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
