---
"description": "了解如何使用 Aspose.Cells for .NET 將列錶框新增至 Excel 工作表。按照我們簡單的逐步指南，讓您的 Excel 工作表具有互動性。"
"linktitle": "在 Excel 中將列錶框新增至工作表"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 Excel 中將列錶框新增至工作表"
"url": "/zh-hant/net/excel-shapes-controls/add-list-box-to-worksheet-excel/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中將列錶框新增至工作表

## 介紹
在 Excel 工作表中加入互動元素（如列錶框）可以顯著改善資料管理和呈現。無論您創建的是互動式表單還是自訂資料輸入工具，使用列錶框控制使用者輸入的能力都是非常寶貴的。 Aspose.Cells for .NET 提供了在 Excel 檔案中新增和管理這些控制項的有效方法。在本指南中，我們將引導您完成使用 Aspose.Cells for .NET 在工作表新增列錶框的過程。
## 先決條件
在深入編碼之前，請確保您已準備好以下工具和資源：
- Aspose.Cells for .NET Library：您可以從 [Aspose.Cells for .NET下載頁面](https://releases。aspose.com/cells/net/).
- 開發環境：任何支援.NET開發的IDE，例如Visual Studio。
- .NET Framework：確保您的專案針對的是支援的 .NET 框架版本。
另外，考慮購買 [臨時執照](https://purchase.aspose.com/temporary-license/) 如果您想不受限制地探索所有功能。
## 導入包
在開始之前，請確保您已匯入必要的 Aspose.Cells 命名空間。具體操作如下：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
在本教程中，我們將新增列錶框的過程分解為多個簡單的步驟。嚴格遵循每個步驟以確保一切按預期進行。
## 步驟 1：設定文檔目錄
在建立任何 Excel 檔案之前，您需要一個位置來儲存它。設定目錄的方法如下：
```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory";
// 如果目錄不存在，則建立目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
在此步驟中，您將定義檔案的儲存位置。程式碼檢查目錄是否存在，如果不存在，則為您建立一個。這可確保您以後不會遇到任何「找不到檔案」錯誤。
## 步驟 2：建立新工作簿並存取第一個工作表
接下來，我們將建立一個新的工作簿並存取我們將新增列錶框的第一個工作表。
```csharp
// 建立一個新的工作簿。
Workbook workbook = new Workbook();
// 取得第一張工作表。
Worksheet sheet = workbook.Worksheets[0];
```
工作簿本質上就是您的 Excel 文件。在這裡，我們建立一個新的工作簿並存取第一個工作表，我們將在其中放置列錶框。想像一下建立一個空白畫布，您將在其中繪製控制項。
## 步驟3：輸入列錶框的數據
在新增列錶框之前，我們需要填入列錶框將引用的一些資料。
```csharp
// 取得工作表單元格集合。
Cells cells = sheet.Cells;
// 輸入標籤的值。
cells["B3"].PutValue("Choose Dept:");
// 將標籤設定為粗體。
cells["B3"].GetStyle().Font.IsBold = true;
// 列錶框的輸入值。
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
在這裡，我們在工作表中添加一些文字。標籤「選擇部門：」放在儲存格 B3 中，並將其字體設定為粗體。在 A 欄中，我們插入將作為列錶框輸入範圍的值，代表不同的部門。此輸入範圍是使用者與列錶框互動時將要選擇的內容。
## 步驟 4：將列錶框新增至工作表
現在我們已經設定了數據，讓我們新增列錶框控製本身。
```csharp
// 新增一個新的列錶框。
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
此程式碼將列錶框新增至工作表。這些參數定義列錶框的位置和大小。列錶框位於第 2 行、第 0 列，寬度為 122，高度為 100。這些座標和大小決定了列錶框在工作表中的出現位置。
## 步驟 5：設定列錶框屬性
接下來，我們將設定列錶框的各種屬性，以使其充分發揮作用。
```csharp
// 設定放置類型。
listBox.Placement = PlacementType.FreeFloating;
// 設定連結的儲存格。
listBox.LinkedCell = "A1";
// 設定輸入範圍。
listBox.InputRange = "A2:A7";
// 設定選擇類型。
listBox.SelectionType = SelectionType.Single;
// 設定具有 3-D 陰影的列錶框。
listBox.Shadow = true;
```
- PlacementType.FreeFloating：此屬性可確保無論如何修改工作表，列錶框都保持在其位置。
- LinkedCell：設定一個儲存格（在本例中為 A1），其中將顯示從列錶框中選擇的值。
- InputRange：這告訴列錶框在哪裡尋找其選項清單（A2 到 A7，我們之前設定）。
- SelectionType.Single：這限制使用者只能從列錶框中選擇一個項目。
- 陰影：陰影效果使列錶框看起來更立體，更具視覺吸引力。
## 步驟6：儲存Excel文件
最後，讓我們儲存包含列錶框的工作簿。
```csharp
// 儲存工作簿。
workbook.Save(dataDir + "book1.out.xls");
```
這行程式碼將工作簿儲存到我們先前設定的目錄中。該檔案名稱為“book1.out.xls”，但您可以選擇任何適合您專案的名稱。
## 結論
就是這樣！您已成功使用 Aspose.Cells for .NET 將列錶框新增至 Excel 工作表。只需幾行程式碼，我們就創建了一個功能齊全的列錶框，使工作表更具互動性和動態性。本教學將為您提供堅實的基礎，以探索 Aspose.Cells for .NET 中的其他控制項和功能。繼續嘗試，很快您就會掌握該庫的豐富功能！
## 常見問題解答
### 我可以允許列錶框中的多項選擇嗎？  
是的，你可以更改 `SelectionType` 到 `SelectionType.Multi` 以允許多項選擇。
### 我可以改變列錶框的外觀嗎？  
絕對地！ Aspose.Cells 可讓您自訂列錶框的外觀，包括其大小、字體甚至顏色。
### 如果我稍後需要刪除列錶框怎麼辦？  
您可以從 `Shapes` 收集使用 `sheet。Shapes.RemoveAt(index)`.
### 我可以將列錶框連結到不同的單元格嗎？  
是的，只需更改 `LinkedCell` 屬性到您想要顯示所選值的任何其他儲存格。
### 如何為列錶框新增更多項目？  
只需透過在指定儲存格中插入更多值來更新輸入範圍，列錶框就會自動更新。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}