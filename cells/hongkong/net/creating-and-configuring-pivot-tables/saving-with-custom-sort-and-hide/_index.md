---
title: 在 .NET 中使用自訂排序和隱藏保存資料透視表
linktitle: 在 .NET 中使用自訂排序和隱藏保存資料透視表
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 儲存具有自訂排序和隱藏行的資料透視表。包含實際範例的分步指南。
weight: 26
url: /zh-hant/net/creating-and-configuring-pivot-tables/saving-with-custom-sort-and-hide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中使用自訂排序和隱藏保存資料透視表

## 介紹
在資料分析領域，資料透視表是最強大的工具之一，用於以易於理解的格式匯總、分析和呈現資料。如果您正在使用 .NET 並尋找一種簡單的方法來操作資料透視表（具體來說，透過自訂排序和隱藏特定行來保存資料透視表），那麼您來對地方了！今天，我們將解開使用 Aspose.Cells for .NET 儲存資料透視表的技術。本指南將引導您完成從先決條件到實踐範例的所有內容，確保您有能力自行解決類似的任務。那麼，讓我們立即開始吧！
## 先決條件
在深入研究編碼的本質之前，請確保滿足以下先決條件：
1. Visual Studio：理想情況下，您需要一個可靠的 IDE 來處理您的 .NET 專案。 Visual Studio 是不錯的選擇。
2.  Aspose.Cells for .NET：您需要存取 Aspose 的程式庫以程式設計方式管理 Excel 檔案。你可以[在此下載 Aspose.Cells for .NET](https://releases.aspose.com/cells/net/).
3. C# 基礎知識：熟悉 C# 中的基本程式設計概念和語法將使過程更加順利。
4. 範例 Excel 檔案：我們將使用名為`PivotTableHideAndSortSample.xlsx`。確保您指定的文件目錄中有此文件。
設定好開發環境並準備好範例文件後，一切都準備好了！
## 導入包
現在我們已經檢查了先決條件，讓我們匯入必要的套件。在您的 C# 檔案中，使用以下指令來包含 Aspose.Cells：
```csharp
using System;
using Aspose.Cells.Pivot;
```
該指令可讓您存取 Aspose.Cells 庫提供的類別和方法。確保您已將 Aspose.Cells.dll 新增至專案參考。
## 第 1 步：設定工作簿
首先，我們需要載入工作簿。下面的程式碼片段實現了這一點：
```csharp
//原始檔和輸出檔的目錄
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
//載入工作簿
Workbook workbook = new Workbook(sourceDir + "PivotTableHideAndSortSample.xlsx");
```
在此步驟中，您定義儲存來源檔案和輸出檔案的目錄。這`Workbook`建構函數將載入現有的 Excel 文件，使其準備好進行操作。
## 第 2 步：存取工作表和資料透視表
現在，讓我們存取工作簿中的特定工作表並選擇我們要使用的資料透視表。
```csharp
//訪問第一個工作表
Worksheet worksheet = workbook.Worksheets[0];
//存取工作表中的第一個資料透視表
var pivotTable = worksheet.PivotTables[0];
```
在這個片段中，`Worksheets[0]`選擇 Excel 文件中的第一個工作表，然後`PivotTables[0]`檢索第一個資料透視表。這使您可以準確定位要修改的資料透視表。
## 步驟 3：對資料透視表行進行排序
接下來，我們將實作自訂排序來組織資料。具體來說，我們將按降序對分數進行排序。
```csharp
//按降序對第一行欄位進行排序
PivotField field = pivotTable.RowFields[0];
field.IsAutoSort = true;
field.IsAscendSort = false;  //下降為 false
field.AutoSortField = 0;     //根據第一列排序
```
在這裡，我們使用的是`PivotField`設定排序參數。這告訴資料透視表根據第一列對指定的行字段進行排序，並按降序排列。 
## 步驟 4：刷新並計算數據
應用排序後，刷新資料透視表的資料以確保它反映我們的修改至關重要。
```csharp
//刷新並計算數據透視表數據
pivotTable.RefreshData();
pivotTable.CalculateData();
```
此步驟將資料透視表與您目前的資料同步，套用您迄今為止所做的任何排序或過濾變更。將其視為點擊「刷新」即可查看資料的新組織！
## 第 5 步：隱藏特定行
現在，讓我們隱藏分數低於特定閾值（例如小於 60）的行。
```csharp
//指定檢查分數的起始行
int currentRow = 3;
int rowsUsed = pivotTable.DataBodyRange.EndRow;
//隱藏分數低於 60 的行
while (currentRow < rowsUsed)
{
    Cell cell = worksheet.Cells[currentRow, 1]; //假設分數在第一列
    double score = Convert.ToDouble(cell.Value);
    if (score < 60)
    {
        worksheet.Cells.HideRow(currentRow);  //如果分數低於 60，則隱藏該行
    }
    currentRow++;
}
```
在此循環中，我們檢查資料透視表資料主體範圍內的每一行。如果分數低於 60，我們會隱藏該行。這就像清理你的工作空間一樣——清除那些無助於你了解全局的雜物！
## 第 6 步：最終刷新並儲存工作簿
在結束之前，我們對資料透視表進行最後一次刷新，以確保行隱藏生效，然後將工作簿儲存到新文件中。
```csharp
//最後一次刷新併計算數據
pivotTable.RefreshData();
pivotTable.CalculateData();
//儲存修改後的工作簿
workbook.Save(outputDir + "PivotTableHideAndSort_out.xlsx");
```
最後的刷新可確保所有內容都是最新的，並且透過儲存工作簿，您可以建立一個反映我們所做的所有變更的新檔案。
## 第7步：確認成功
最後，我們將列印一條成功訊息，以確認我們的操作順利完成。
```csharp
Console.WriteLine("PivotTableSortAndHide executed successfully.");
```
該行具有確認成功和在控制台中提供反饋的雙重目的，使該過程更具互動性和用戶友好性。
## 結論
現在你就擁有了！您已經成功學習如何使用 Aspose.Cells for .NET 儲存具有自訂排序和隱藏功能的資料透視表。從載入工作簿到對資料進行排序和隱藏不必要的詳細信息，這些步驟提供了一種以程式設計方式管理資料透視表的結構化方法。無論您是在分析銷售數據、追蹤團隊績效，還是只是組織信息，使用 Aspose.Cells 掌握這些技能都可以節省您寶貴的時間並改進您的數據分析工作流程。
## 常見問題解答
### 什麼是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一個 .NET 函式庫，可讓開發人員在不依賴 Microsoft Excel 的情況下建立、操作和轉換 Excel 電子表格。它非常適合自動化 Excel 文件中的任務。
### 我可以在未安裝 Microsoft Office 的情況下使用 Aspose.Cells 嗎？
絕對地！ Aspose.Cells 是一個獨立的函式庫，因此您無需在系統上安裝 Microsoft Office 即可處理 Excel 檔案。
### 我如何獲得 Aspose.Cells 的臨時許可證？
您可以透過以下方式申請臨時許可證[臨時許可證頁面](https://purchase.aspose.com/temporary-license/).
### 在哪裡可以找到 Aspose.Cells 問題的支援？
如有任何疑問或問題，您可以訪問[Aspose論壇](https://forum.aspose.com/c/cells/9)，您可以在這裡找到社區和 Aspose 團隊的支持。
### Aspose.Cells 是否有免費試用版？
是的！您可以在購買之前下載 Aspose.Cells 的免費試用版來測試其功能。參觀[免費試用頁面](https://releases.aspose.com/)開始吧。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
