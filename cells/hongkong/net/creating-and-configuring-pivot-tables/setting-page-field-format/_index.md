---
"description": "了解如何使用 Aspose.Cells for .NET 以程式設計方式設定資料透視表中的頁面欄位格式。按照我們的分步教程實現無縫資料管理。"
"linktitle": "在 .NET 中以程式設計方式設定頁面欄位格式"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 .NET 中以程式設計方式設定頁面欄位格式"
"url": "/zh-hant/net/creating-and-configuring-pivot-tables/setting-page-field-format/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以程式設計方式設定頁面欄位格式

## 介紹
透過程式碼建立和操作 Excel 檔案可以非常強大，尤其是當您需要分析大型資料集時。您的工具庫中有一個非常棒的工具，那就是 Aspose.Cells for .NET，它允許您以程式設計方式與 Excel 檔案互動並建立複雜的報表結構。在本教程中，我們將深入研究如何使用這個強大的庫在資料透視表中設定頁面欄位格式。無論您是經驗豐富的開發人員還是初學者，在本指南結束時，您都將掌握如何在 .NET 中使用資料透視表及其各種設定。
## 先決條件
在我們深入編碼之前，讓我們確保您已正確設定了所有內容。您需要以下物品：
- Visual Studio：一個可以編寫和執行 .NET 程式碼的工作環境。
- Aspose.Cells：您可以下載資料庫 [這裡](https://releases。aspose.com/cells/net/).
- C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解程式碼片段。
- Excel 檔案：準備好 Excel 檔案（例如 `Book1.xls`）包含適合建立資料透視表的資料。 
如果您還沒有，請取得 Aspose.Cells 的免費試用版 [這裡](https://releases。aspose.com/).
## 導入包
首先，您需要在專案中匯入正確的套件。首先在 C# 專案中加入 Aspose.Cells 函式庫的參考。具體操作如下：
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
這將引入使用 Aspose.Cells 操作 Excel 檔案所需的所有必要類別和方法。
## 步驟 1：設定您的工作區
首先定義儲存 Excel 檔案的工作目錄。例如，您可以像這樣宣告一個變數：
```csharp
string dataDir = "Your Document Directory";
```
## 載入工作簿
接下來，我們需要載入我們的 Excel 範本。這是至關重要的一步，因為它為我們的營運奠定了基礎：
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
此行從指定目錄載入現有工作簿。
## 第 2 步：訪問工作表
工作簿載入完成後，就可以存取包含資料透視表或要分析的資料的工作表了。您可以按照以下步驟操作：
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
這將抓取已載入工作簿的第一個工作表。如果您使用多張工作表，您可以輕鬆修改索引。
## 步驟 3：存取資料透視表
繼續，讓我們存取所選工作表中的資料透視表。如果您使用單一資料透視表，則可以將其索引設為 `0`：
```csharp
int pivotindex = 0;
// 存取資料透視表
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
此程式碼片段選擇工作表中的第一個資料透視表。 
## 步驟 4：設定資料透視表
現在到了令人興奮的部分！讓我們設定資料透視表來顯示各行的總計：
```csharp
pivotTable.RowGrand = true;
```
此行確保您的報告將顯示總計，這可以作為數據分析的有用摘要。
## 步驟 5：存取和設定行字段
接下來，我們需要存取資料透視表的行字段：
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.RowFields;
```
此集合允許我們根據需要操作欄位。
## 配置第一行字段
想要設定特定的小計類型嗎？讓我們存取集合中的第一個欄位並對其進行配置：
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
// 設定小計。
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
透過啟用 `Sum` 和 `Count` 小計，我們可以快速匯總報告中的數據。
## 步驟 6：設定自動排序選項
接下來，讓我們進行一些智慧排序。這樣，您的資料透視表將按照有意義的順序排列資料：
```csharp
// 設定自動排序選項。
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; // 使用預定義的排序欄位。
```
此程式碼片段可實現自動排序並指定升序。 
## 步驟 7：設定自動顯示選項
您想進一步過濾資料嗎？自動顯示選項有助於在定義的條件下顯示特定的資料點：
```csharp
// 設定自動顯示選項。
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; // 指定要自動顯示的欄位。
```
這可確保您的數據透視表僅顯示相關數據，從而增強清晰度和重點。
## 步驟8：儲存您的工作
完成所有這些配置後，您肯定不想失去自己的工作成果！像這樣儲存修改後的工作簿：
```csharp
workbook.Save(dataDir + "output.xls");
```
現在，您可以在文件目錄中找到新建立的 Excel 檔案。
## 結論
就是這樣！我們已經介紹了一種使用 Aspose.Cells for .NET 在資料透視表中以程式設計方式設定頁面欄位格式的全面且實用的方法。透過提供的簡單步驟，您可以自信地修改 Excel 資料以滿足您的報告需求。當您將 C# 的強大功能與 Aspose.Cells 結合時，您可以取得令人難以置信的成就。
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個 .NET 函式庫，可讓開發人員以程式設計方式建立、操作和轉換 Excel 檔案。
### 如何安裝 Aspose.Cells？
您可以直接從 [Aspose 網站](https://releases。aspose.com/cells/net/).
### 我可以在沒有安裝 Excel 的情況下使用 Aspose.Cells 嗎？
是的，Aspose.Cells 是一個獨立的函式庫，不需要安裝 Microsoft Excel。
### 在哪裡可以找到詳細的支援？
您可以在以下位置存取詳細的支援和論壇 [Aspose 支援](https://forum。aspose.com/c/cells/9).
### 我怎樣才能獲得臨時駕照？
您可以從 [這裡](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}