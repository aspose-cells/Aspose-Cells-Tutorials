---
title: 在 .NET 中以程式設計方式儲存 ODS 格式的資料透視表
linktitle: 在 .NET 中以程式設計方式儲存 ODS 格式的資料透視表
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過此逐步指南，了解如何使用 Aspose.Cells for .NET 以 ODS 格式儲存資料透視表。
weight: 25
url: /zh-hant/net/creating-and-configuring-pivot-tables/saving-in-ods-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以程式設計方式儲存 ODS 格式的資料透視表

## 介紹
在管理電子表格中的資料時，沒有什麼能與資料透視表的功能相提並論。它們是總結、分析和呈現複雜資料集的首選工具。今天，我們將深入研究如何使用 Aspose.Cells for .NET 以 ODS 格式儲存資料透視表。無論您是經驗豐富的開發人員還是剛接觸 .NET，您都會發現本指南非常簡單。 
讓我們開始吧！
## 先決條件
在我們開始編寫程式碼之前，您需要滿足一些要點：
### 1..NET基礎知識
對 .NET 及其程式設計概念有基本的了解將有助於您輕鬆地進行操作。
### 2..NET 的 Aspose.Cells
您需要安裝 Aspose.Cells for .NET。您可以從[Aspose 發佈頁面](https://releases.aspose.com/cells/net/)。還提供試用版[這裡](https://releases.aspose.com/).
### 三、開發環境
確保您有一個像 Visual Studio 這樣的 IDE，您可以在其中編寫和測試 .NET 程式碼。
### 4. 一點耐心
與任何編碼工作一樣，耐心是關鍵。如果第一次工作不順利，請不要擔心；調試是該過程的一部分。
## 導入包
要使用 Aspose.Cells，您需要匯入必要的命名空間。在程式碼檔案的開頭加入以下 using 指令：
```csharp
using System;
using Aspose.Cells.Pivot;
```
該行可讓您存取 Aspose.Cells 庫中的所有功能，讓您的編碼過程變得輕而易舉。
現在，讓我們將該流程分解為可管理的步驟。
## 第 1 步：設定輸出目錄
首先，您需要定義 ODS 檔案的儲存位置。這是目錄路徑的簡單分配。
```csharp
string outputDir = "Your Document Directory";
```
在此行中，替換`"Your Document Directory"`以及您要儲存檔案的路徑。
## 第 2 步：建立新工作簿
接下來，您將實例化一個新的 Workbook 對象，它將保存所有資料和結構，包括資料透視表。
```csharp
Workbook workbook = new Workbook();
```
在這裡，您基本上可以重新開始 - 將其視為一塊空白畫布，您將在其中創建您的傑作。
## 第 3 步：訪問工作表
現在我們有了工作簿，我們需要開始處理我們的工作表。 Aspose.Cells 讓您可以輕鬆存取第一個可用的工作表。
```csharp
Worksheet sheet = workbook.Worksheets[0];
```
該行將我們帶到第一個工作表，準備好資料輸入。
## 第 4 步：用資料填滿儲存格
是時候用一些數據填充我們的工作表了。我們將使用一個簡單的體育銷售數據範例。 
以下是在各個單元格中設定值的方法：
```csharp
Cells cells = sheet.Cells;
cells["A1"].PutValue("Sport");
cells["B1"].PutValue("Quarter");
cells["C1"].PutValue("Sales");
cells["A2"].PutValue("Golf");
cells["A3"].PutValue("Golf");
cells["A4"].PutValue("Tennis");
cells["A5"].PutValue("Tennis");
cells["A6"].PutValue("Tennis");
cells["A7"].PutValue("Tennis");
cells["A8"].PutValue("Golf");
cells["B2"].PutValue("Qtr3");
cells["B3"].PutValue("Qtr4");
cells["B4"].PutValue("Qtr3");
cells["B5"].PutValue("Qtr4");
cells["B6"].PutValue("Qtr3");
cells["B7"].PutValue("Qtr4");
cells["B8"].PutValue("Qtr3");
cells["C2"].PutValue(1500);
cells["C3"].PutValue(2000);
cells["C4"].PutValue(600);
cells["C5"].PutValue(1500);
cells["C6"].PutValue(4070);
cells["C7"].PutValue(5000);
cells["C8"].PutValue(6430);
```
在這些行中，我們定義標題並填入銷售資料。將此步驟想像成煮飯前先在食品儲藏室備貨；您的成分（數據）越好，您的膳食（分析）就越好。
## 第 5 步：建立資料透視表
現在到了有趣的部分——創建數據透視表！以下是將其新增至工作表中的方法：
```csharp
PivotTableCollection pivotTables = sheet.PivotTables;
//將資料透視表新增至工作表
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```
在此程式碼片段中，我們指定資料透視表的資料範圍以及將其放置在工作表上的位置。數據範圍`=A1:C8`覆蓋我們資料所在的區域。
## 第 6 步：自訂您的資料透視表
接下來，您需要自訂資料透視表以滿足您的需求。這涉及控制顯示內容、分類方式以及計算資料的方式。
```csharp
PivotTable pivotTable = pivotTables[index];
//不顯示行的總計。
pivotTable.RowGrand = false;
//將第一個欄位拖曳到行區域。
pivotTable.AddFieldToArea(PivotFieldType.Row, 0);
//將第二個欄位拖曳至列區域。
pivotTable.AddFieldToArea(PivotFieldType.Column, 1);
//將第三個欄位拖曳至資料區域。
pivotTable.AddFieldToArea(PivotFieldType.Data, 2);
pivotTable.CalculateData();
```
在這裡，您要決定要匯總哪些資料欄位以及如何表示它們。這就像為你的晚餐佈置餐桌一樣；您可以決定什麼最適合以及如何呈現它。
## 第 7 步：儲存您的工作簿
最後，您可以將工作儲存為所需的 ODS 格式。操作方法如下：
```csharp
workbook.Save(outputDir + "PivotTableSaveInODS_out.ods");
```
透過此步驟，您將完成您的專案並將其保護在您選擇的目錄中 - 一個令人滿意的完成！
## 第 8 步：驗證您的輸出
最後，檢查該過程是否成功完成總是一個好主意。您可以新增一條簡單的控制台訊息：
```csharp
Console.WriteLine("PivotTableSaveInODS executed successfully.");
```
此訊息將出現在您的控制台中，以確認一切順利。就像廚師在上菜前檢查所有東西是否煮得完美一樣！
## 結論 
現在你就擁有了！您不僅使用 Aspose.Cells 建立了資料透視表，而且還以 ODS 格式儲存了它。本指南將引導您完成每一步，確保您具備應對未來類似任務的知識和信心。
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個複雜的程式庫，可讓您在 .NET 應用程式中建立和操作 Excel 檔案。
### 我可以免費使用 Aspose.Cells 嗎？
是的，您可以從以下位置下載免費試用版[阿斯普斯網站](https://releases.aspose.com/).
### Aspose.Cells 支援哪些格式？
它支援多種格式，包括 XLSX、XLS、ODS、PDF 等。
### 我如何獲得 Aspose.Cells 的支援？
您可以在以下位置找到幫助[Aspose 支援論壇](https://forum.aspose.com/c/cells/9).
### 有臨時許可證嗎？
是的，您可以透過 Aspose 網站申請臨時許可證[這裡](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
