---
"description": "透過本詳細的分步教程，了解如何使用 Aspose.Cells for .NET 在 Excel 中對文字套用刪除線效果。"
"linktitle": "在 Excel 中建立文字刪除線效果"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 Excel 中建立文字刪除線效果"
"url": "/zh-hant/net/working-with-fonts-in-excel/creating-strike-out-effect/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中建立文字刪除線效果

## 介紹
對 Excel 來說，視覺元素與資料本身同樣重要。無論您突出顯示重要變更還是標記不再相關的項目，文字上的刪除線效果都是管理電子表格中視覺表示的經典方法。在本指南中，我們將引導您完成使用 Aspose.Cells for .NET 在 Excel 中對文字實現刪除線效果的過程。本教學不僅涵蓋必要的先決條件，還將提供逐步的方法來確保您可以輕鬆複製此效果。
## 先決條件
在深入學習本教程之前，請確保滿足以下先決條件：
1. 開發環境：您應該設定一個.NET 開發環境。這可以是 Visual Studio 或任何其他您喜歡的支援 .NET 開發的 IDE。
2. Aspose.Cells for .NET：請確保您的專案中安裝了 Aspose.Cells。您可以從以下鏈接下載： [下載 Aspose.Cells](https://releases。aspose.com/cells/net/).
3. C# 基礎知識：對 C# 程式設計的基本了解很有幫助，因為範例將以 C# 編碼。
4. .NET Framework：確保您的專案針對相容的 .NET Framework 版本，通常是 .NET Core 或 .NET Framework 4.5 及以上版本。
## 導入包
在編寫任何程式碼之前，您需要從 Aspose.Cells 匯入所需的命名空間。這對於訪問圖書館提供的各種功能至關重要。以下是導入必要命名空間的方法：
```csharp
using System.IO;
using Aspose.Cells;
```
透過這些匯入，您將可以存取本教學中將使用的 Workbook、Worksheet 和 Style 類別。
現在我們已經做好了準備，讓我們將流程分解為易於管理的步驟。每個步驟都會附有清晰的說明，指導您在 Excel 中建立文字的刪除線效果。
## 步驟1：定義文檔目錄
首先定義儲存 Excel 文件的路徑。這將是保存輸出文件的位置。
```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory";
```
代替 `"Your Document Directory"` 使用您想要儲存 Excel 檔案的實際目錄路徑。這將為您的輸出設定目錄。
## 第 2 步：建立目錄
接下來，您需要確保上一個步驟中指定的目錄存在。如果不存在，您可以透過程式設計方式建立它。
```csharp
// 如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
此程式碼檢查目錄是否存在，如果不存在則建立該目錄。這有助於避免您稍後嘗試儲存文件時出現錯誤。
## 步驟 3：實例化工作簿對象
現在，是時候建立一個新的 Workbook 物件了。這是 Excel 檔案的基礎，您可以在其中新增資料和應用程式格式。
```csharp
// 實例化 Workbook 物件
Workbook workbook = new Workbook();
```
這 `Workbook` 類別代表一個 Excel 文件。透過建立此類別的實例，您實際上正在建立一個新的 Excel 文件。
## 步驟 4：新增工作表
每個工作簿可以包含多個工作表。讓我們繼續在您的工作簿中建立一個新的工作表。
```csharp
// 向 Excel 物件新增工作表
int i = workbook.Worksheets.Add();
```
這 `Add` 方法 `Worksheets` 集合會向工作簿新增一個工作表並返回其索引。 
## 步驟5：取得新工作表的引用
建立工作表後，您需要參考它以進行將來的操作。
```csharp
// 透過傳遞工作表索引來取得新新增工作表的引用
Worksheet worksheet = workbook.Worksheets[i];
```
在這裡，您將使用其索引來獲取新建立的工作表（`i`）。這使您可以操作工作表。
## 步驟 6：訪問儲存格
您將需要存取工作表中將套用刪除線格式的特定儲存格。在這個例子中，我們使用單元格 `A1`。
```csharp
// 從工作表存取“A1”單元格
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
在 Excel 中，儲存格透過其列和行標識符來引用（例如「A1」）。我們正在獲取對單元格的引用 `A1` 以進行進一步的操作。
## 步驟 7：為儲存格新增值
接下來，讓我們在單元格中插入一些文字。我們將寫“Hello Aspose！”在細胞中 `A1`。
```csharp
// 在「A1」儲存格中加入一些值
cell.PutValue("Hello Aspose!");
```
這 `PutValue` 方法用於為單元格指派字串值。您可以將此字串修改為您想要顯示的任何內容。
## 步驟 8：取得儲存格的樣式
現在我們的單元格中已經有了文本，是時候訪問單元格的樣式來應用我們想要的格式，包括刪除線效果。
```csharp
// 取得單元格的樣式
Style style = cell.GetStyle();
```
這 `GetStyle` 方法會擷取儲存格的目前樣式，讓您可以修改字體類型、大小和效果等屬性。
## 步驟9：設定刪除線效果
讓我們將刪除線效果套用到儲存格中的文字。我們將修改單元格的字體樣式。
```csharp
// 開始：二傳三振
// 設定字體的刪除線效果
style.Font.IsStrikeout = true;
// ExEnd:設定三振出局
```
透過設定 `IsStrikeout` 為 true，則表示您指示 Excel 以視覺方式劃掉所選儲存格中的文字 - 就像以視覺方式從清單中標記某些內容一樣。
## 步驟 10：將樣式套用至儲存格
修改樣式後，需要將其套用回儲存格以反映變更。
```csharp
// 將樣式套用至儲存格
cell.SetStyle(style);
```
這 `SetStyle` 方法使用新樣式更新儲存格，現在包括刪除線格式。
## 步驟11：儲存Excel文件
最後，是時候將您的工作簿儲存到指定的目錄了。在此範例中，我們將使用以下名稱儲存文件 `book1。out.xls`.
```csharp
// 儲存 Excel 文件
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
這 `Save` 方法以 97-2003 Excel 格式將工作簿寫入磁碟。如果需要，您可以指定不同的格式。
## 結論
如果您逐步分解，使用 Aspose.Cells for .NET 在 Excel 中為文字建立刪除線效果是一個簡單的過程。透過遵循本指南，您現在掌握了使用視覺提示增強電子表格的技能，使您的資料不僅具有資訊量，而且具有視覺吸引力。
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的程式庫，用於在 .NET 應用程式中管理 Excel 文件，使您能夠以程式設計方式建立、操作和轉換 Excel 文件。
### 我可以免費使用 Aspose.Cells 嗎？
是的，您可以在試用期內免費使用它。免費試用版可訪問 [Aspose.Cells 免費試用](https://releases。aspose.com/).
### 如何購買 Aspose.Cells？
您可以透過其網站購買 Aspose.Cells 的許可證 [購買 Aspose.Cells](https://purchase。aspose.com/buy).
### 是否有使用 Aspose.Cells 的範例？
是的，你可以在 [Aspose.Cells文檔](https://reference。aspose.com/cells/net/).
### 我可以在哪裡獲得 Aspose.Cells 的支援？
您可以從 [Aspose 論壇](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}