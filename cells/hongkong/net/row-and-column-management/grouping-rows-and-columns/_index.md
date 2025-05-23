---
"description": "透過本逐步指南了解如何使用 Aspose.Cells for .NET 對 Excel 中的行和列進行分組。"
"linktitle": "使用 Aspose.Cells 在 Excel 中對行和列進行分組"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "使用 Aspose.Cells 在 Excel 中對行和列進行分組"
"url": "/zh-hant/net/row-and-column-management/grouping-rows-and-columns/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 在 Excel 中對行和列進行分組

## 介紹
如果您使用大型 Excel 表，您就會知道保持一切井然有序且用戶友好是多麼重要。將行和列分組可以幫助您建立部分，使資料導航更加順暢。使用 Aspose.Cells for .NET，您可以輕鬆地以程式設計方式對 Excel 中的行和列進行分組，從而完全控製文件的佈局。
在本教學中，我們將介紹使用 Aspose.Cells for .NET 在 Excel 表中設定、分組和隱藏行和列所需了解的所有內容。最後，您將能夠像專業人士一樣操作 Excel 文件，甚至無需開啟 Excel 本身。準備好了嗎？
## 先決條件
在我們進入程式碼之前，讓我們確保您已設定好一切並準備就緒：
1. Aspose.Cells for .NET Library：您需要此程式庫來處理 Excel 檔案。你可以下載它 [這裡](https://releases。aspose.com/cells/net/).
2. Visual Studio：本教學課程使用 Visual Studio 作為程式碼範例。
3. 基本 C# 知識：熟悉 C# 和 .NET 會很有幫助。
4. Aspose 許可證：需要付費或臨時許可證以避免評估限制。取得臨時執照 [這裡](https://purchase。aspose.com/temporary-license/).
## 導入包
首先，導入必要的 Aspose.Cells 命名空間以及檔案處理所需的基本 .NET 函式庫。 
```csharp
using System.IO;
using Aspose.Cells;
```
讓我們分解程式碼的每個部分，以便您更輕鬆地跟進和理解。
## 步驟 1：設定資料目錄
首先，我們需要定義要使用的 Excel 檔案的路徑。這通常是本地路徑，但也可能是網路上的路徑。
```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory";
```
在這裡，替換 `"Your Document Directory"` 使用您的 Excel 檔案的實際路徑。此設定可協助您的程式碼找到需要處理的檔案。
## 步驟2：建立文件流程以存取 Excel 文件
Aspose.Cells 要求您透過檔案流開啟檔案。該流讀取並加載文件的內容以進行處理。
```csharp
// 建立包含要開啟的 Excel 檔案的檔案流
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
上面的程式碼打開 `book1.xls` 來自您指定的目錄。如果該檔案不存在，請務必建立它或更改檔案名稱。
## 步驟3：使用Aspose.Cells載入工作簿
現在，讓我們透過 Aspose.Cells 初始化工作簿。此步驟使我們能夠存取 Excel 文件，從而輕鬆進行操作。
```csharp
// 透過檔案流程開啟Excel文件
Workbook workbook = new Workbook(fstream);
```
在這一行之後， `workbook` 物件將包含 Excel 檔案中的所有資料和結構。可以將其想像為將整個電子表格載入到記憶體中。
## 步驟 4：存取要修改的工作表
Aspose.Cells 將工作簿中的每個工作表作為單獨的物件儲存。在這裡，我們選擇第一個工作表。
```csharp
// 存取 Excel 文件中的第一個工作表
Worksheet worksheet = workbook.Worksheets[0];
```
如果您需要特定的工作表，您可以修改此行以透過名稱或索引存取它。
## 步驟 5：將工作表中的行進行分組
現在到了最有趣的部分——分組行！我們將前六行分組並隱藏它們。
```csharp
// 將前六行（從 0 到 5）分組，並透過傳遞 true 使其隱藏
worksheet.Cells.GroupRows(0, 5, true);
```
每個參數的作用如下：
- 0, 5：要分組的行的起始和結束索引。在 Excel 中，行索引從 0 開始。
- true：將其設為 true 會隱藏分組行。
一旦執行，從 0 到 5 的行將被分組並隱藏。
## 步驟 6：將工作表中的欄位進行分組
就像行一樣，您可以對列進行分組以建立更清晰、更有條理的佈局。以下是將前三列分組的方法。
```csharp
// 將前三列（從 0 到 2）分組，並透過傳遞 true 使其隱藏
worksheet.Cells.GroupColumns(0, 2, true);
```
此函數的參數為：
- 0, 2：要分組的列的範圍，其中索引從 0 開始。
- true：此參數隱藏分組的欄位。
您選擇的列（0 到 2）現在將在 Excel 文件中分組顯示並隱藏。
## 步驟7：儲存修改後的Excel文件
進行更改後，讓我們用新名稱儲存檔案以避免覆蓋原始檔案。
```csharp
// 儲存修改後的 Excel 文件
workbook.Save(dataDir + "output.xls");
```
現在您已成功將分組的行和列保存到 `output.xls`。您可以根據需要調整檔案名稱。
## 步驟8：關閉文件流以釋放資源
最後，關閉文件流以釋放所有資源。如果您需要再次存取或修改該文件，則不這樣做可能會導致問題。
```csharp
// 關閉文件流以釋放所有資源
fstream.Close();
```
就是這樣！現在，您已使用 Aspose.Cells for .NET 對 Excel 檔案中的行和列進行分組。
## 結論
使用 Aspose.Cells for .NET 對 Excel 中的行和列進行分組是一個簡單的過程，可以使您的電子表格更加用戶友好且井然有序。只需幾行程式碼，您就掌握了一項強大的功能，如果在 Excel 中手動完成則需要更多步驟。此外，您可以跨多個文件自動執行此過程，從而節省時間並減少錯誤。本指南向您展示了以程式方式控制 Excel 檔案所需的所有步驟。
## 常見問題解答
### 我可以對行和列進行分組而不隱藏它們嗎？  
是的！只需通過 `false` 作為第三個參數 `GroupRows` 或者 `GroupColumns` 方法。
### 如果我想取消分組行或列怎麼辦？  
使用 `w或者ksheet.Cells.UngroupRows(startRow, endRow)` or `worksheet.Cells.UngroupColumns(startColumn, endColumn)` 取消組合。
### 我可以在同一個工作表中將多個範圍分組嗎？  
絕對地。致電 `GroupRows` 或者 `GroupColumns` 對要分組的每個範圍的方法。
### 我需要許可證才能使用 Aspose.Cells for .NET 嗎？  
是的，雖然有試用版，但您需要許可證才能解鎖全部功能。您可以獲得臨時駕照 [這裡](https://purchase。aspose.com/temporary-license/).
### 我可以使用條件邏輯對行和列進行分組嗎？  
是的！您可以根據每行或每列中的數據，在分組之前將邏輯合併到程式碼中，從而建立條件分組。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}