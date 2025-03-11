---
title: 將列錶框新增至 Excel 中的工作表
linktitle: 將列錶框新增至 Excel 中的工作表
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 將列錶框新增至 Excel 工作表。遵循我們簡單的逐步指南，使您的 Excel 工作表具有互動性。
weight: 20
url: /zh-hant/net/excel-shapes-controls/add-list-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將列錶框新增至 Excel 中的工作表

## 介紹
在 Excel 工作表中新增互動式元素（例如列錶框）可以顯著改善資料管理和示範。無論您是建立互動式表單還是自訂資料輸入工具，使用列錶框控制使用者輸入的能力都是非常寶貴的。 Aspose.Cells for .NET 提供了在 Excel 檔案中新增和管理這些控制項的有效方法。在本指南中，我們將引導您完成使用 Aspose.Cells for .NET 將列錶框新增至工作表的過程。
## 先決條件
在深入編碼之前，請確保您擁有以下工具和資源：
-  Aspose.Cells for .NET Library：您可以從[Aspose.Cells for .NET 下載頁面](https://releases.aspose.com/cells/net/).
- 開發環境：任何支援.NET開發的IDE，例如Visual Studio。
- .NET Framework：確保您的專案是針對支援的 .NET Framework 版本。
另外，考慮獲得[臨時執照](https://purchase.aspose.com/temporary-license/)如果您想不受限制地探索所有功能。
## 導入包
在開始之前，請確保您已匯入必要的 Aspose.Cells 命名空間。具體做法如下：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
在本教程中，我們將把新增列錶框的過程分解為多個簡單的步驟。密切注意每一步，確保一切按預期進行。
## 第 1 步：設定您的文件目錄
在建立任何 Excel 檔案之前，您需要一個儲存位置。設定目錄的方法如下：
```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
//如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
在此步驟中，您將定義檔案的儲存位置。程式碼會檢查該目錄是否存在，如果不存在，則會為您建立一個目錄。這可以確保您以後不會遇到任何“文件未找到”錯誤。
## 步驟 2：建立新工作簿並存取第一個工作表
接下來，我們將建立一個新工作簿並存取第一個工作表，我們將在其中新增列錶框。
```csharp
//建立一個新的工作簿。
Workbook workbook = new Workbook();
//取得第一個工作表。
Worksheet sheet = workbook.Worksheets[0];
```
工作簿本質上就是 Excel 文件。在這裡，我們將建立一個新工作簿並存取第一個工作表，這是我們放置列錶框的位置。將此視為建立一個空白畫布，您將在其中繪製控制項。
## 步驟 3：為列錶框輸入數據
在新增列錶框之前，我們需要填入列錶框將引用的一些資料。
```csharp
//取得工作表單元格集合。
Cells cells = sheet.Cells;
//輸入標籤的值。
cells["B3"].PutValue("Choose Dept:");
//將標籤設定為粗體。
cells["B3"].GetStyle().Font.IsBold = true;
//輸入列錶框的值。
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
在這裡，我們將一些文字添加到工作表中。標籤「選擇部門：」放置在儲存格 B3 中，並將其字體設定為粗體。在 A 欄中，我們插入的值將作為列錶框的輸入範圍，代表不同的部門。使用者在與列錶框互動時將選擇此輸入範圍。
## 步驟 4：將列錶框新增至工作表中
現在我們已經設定了數據，讓我們新增列錶框控製本身。
```csharp
//新增的列錶框。
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
此程式碼將列錶框新增至工作表。這些參數定義列錶框的位置和大小。此列錶框位於第 2 行、第 0 列，寬度為 122，高度為 100。
## 第 5 步：設定列錶框屬性
接下來，我們將為列錶框設定各種屬性以使其功能齊全。
```csharp
//設定放置類型。
listBox.Placement = PlacementType.FreeFloating;
//設定連結的儲存格。
listBox.LinkedCell = "A1";
//設定輸入範圍。
listBox.InputRange = "A2:A7";
//設定選擇類型。
listBox.SelectionType = SelectionType.Single;
//設定具有 3D 陰影的列錶框。
listBox.Shadow = true;
```
- PlacementType.FreeFloating：此屬性可確保無論工作表如何修改，列錶框都會保持在其位置。
- LinkedCell：這設定一個儲存格（在本例中為 A1），其中將顯示從列錶框中選擇的值。
- 輸入範圍：這告訴列錶框在哪裡尋找其選項清單（A2 到 A7，我們之前設定的）。
- SelectionType.Single：這限制使用者只能從列錶框中選擇一項。
- 陰影：陰影效果使列錶框具有更立體的外觀，使其具有視覺吸引力。
## 第 6 步：儲存 Excel 文件
最後，讓我們儲存包含列錶框的工作簿。
```csharp
//儲存工作簿。
workbook.Save(dataDir + "book1.out.xls");
```
這行程式碼將工作簿儲存到我們先前設定的目錄中。該檔案名稱為“book1.out.xls”，但您可以選擇適合您的專案的任何名稱。
## 結論
現在你就擁有了！您已使用 Aspose.Cells for .NET 成功將列錶框新增至 Excel 工作表。只需幾行程式碼，我們就創建了一個功能齊全的列錶框，使工作表更具互動性和動態性。本教學將為您探索 Aspose.Cells for .NET 中的其他控制項和功能奠定堅實的基礎。繼續嘗試，很快您就會掌握該庫的豐富功能！
## 常見問題解答
### 我可以允許在列錶框中進行多項選擇嗎？  
是的，您可以更改`SelectionType`到`SelectionType.Multi`允許多項選擇。
### 我可以更改列錶框的外觀嗎？  
絕對地！ Aspose.Cells 可讓您自訂列錶框的外觀，包括其大小、字體甚至顏色。
### 如果我稍後需要刪除列錶框怎麼辦？  
您可以從列錶框存取和刪除列錶框`Shapes`收集使用`sheet.Shapes.RemoveAt(index)`.
### 我可以將列錶框連結到不同的單元格嗎？  
是的，只需更改`LinkedCell`屬性到要顯示所選值的任何其他單元格。
### 如何在列錶框中新增更多項目？  
只需透過在指定儲存格中插入更多值來更新輸入範圍，列錶框就會自動更新。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
