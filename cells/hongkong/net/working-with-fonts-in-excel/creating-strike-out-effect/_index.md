---
title: 在 Excel 中的文字上建立刪除線效果
linktitle: 在 Excel 中的文字上建立刪除線效果
second_title: Aspose.Cells .NET Excel 處理 API
description: 在此詳細的逐步教學中，了解如何使用 Aspose.Cells for .NET 對 Excel 中的文字套用刪除線效果。
weight: 15
url: /zh-hant/net/working-with-fonts-in-excel/creating-strike-out-effect/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中的文字上建立刪除線效果

## 介紹
對於 Excel，視覺元素與資料本身同樣重要。無論您是突出顯示重要變更還是標記不再相關的項目，文字上的刪除線效果都是管理電子表格中視覺表示的經典方法。在本指南中，我們將引導您完成使用 Aspose.Cells for .NET 在 Excel 中的文字上實作刪除線效果的過程。本教學不僅涵蓋必要的先決條件，還將提供逐步方法，以確保您可以輕鬆複製此效果。
## 先決條件
在深入學習本教程之前，請確保您符合以下先決條件：
1. 開發環境：您應該設定一個.NET 開發環境。這可以是 Visual Studio 或您喜歡的任何其他支援 .NET 開發的 IDE。
2. Aspose.Cells for .NET：請確保您的專案中安裝了 Aspose.Cells。您可以從以下鏈接下載：[下載 Aspose.Cells](https://releases.aspose.com/cells/net/).
3. C# 基礎知識：對 C# 程式設計的基本了解很有幫助，因為範例將使用 C# 進行編碼。
4. .NET Framework：確保您的專案是針對相容的 .NET Framework 版本，通常是 .NET Core 或 .NET Framework 4.5 及更高版本。
## 導入包
在編寫任何程式碼之前，您需要從 Aspose.Cells 匯入所需的命名空間。這對於存取庫提供的各種功能至關重要。以下是導入必要的命名空間的方法：
```csharp
using System.IO;
using Aspose.Cells;
```
透過這些匯入，您將可以存取本教學中將使用的 Workbook、Worksheet 和 Style 類別。
現在我們已經做好了準備，讓我們將流程分解為可管理的步驟。每個步驟都附有清晰的說明，指導您在 Excel 中的文字上建立刪除線效果。
## 第 1 步：定義文檔目錄
首先定義 Excel 文檔的儲存路徑。這將是保存輸出文件的位置。
```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
```
代替`"Your Document Directory"`與您要儲存 Excel 檔案的實際目錄路徑。這將為您的輸出設定目錄。
## 步驟2：建立目錄
接下來，您需要確保您在上一個步驟中指定的目錄存在。如果它不存在，您可以透過程式設計方式建立它。
```csharp
//如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
此程式碼檢查該目錄是否存在，如果不存在則建立它。這有助於避免您稍後嘗試儲存文件時出現錯誤。
## 第 3 步：實例化工作簿對象
現在，是時候建立一個新的 Workbook 物件了。這是 Excel 檔案的基礎，您將在其中新增資料和應用程式格式。
```csharp
//實例化 Workbook 物件
Workbook workbook = new Workbook();
```
這`Workbook`類別代表一個 Excel 文件。透過建立此類別的實例，您實際上正在建立一個新的 Excel 文件。
## 第 4 步：新增工作表
每個工作簿可以包含多個工作表。讓我們繼續在工作簿中建立一個新工作表。
```csharp
//將新工作表新增至 Excel 對象
int i = workbook.Worksheets.Add();
```
這`Add`的方法`Worksheets`集合將新工作表新增至工作簿並返回其索引。 
## 步驟5：取得新工作表的引用
建立工作表後，您需要在以後的操作中引用它。
```csharp
//透過傳遞工作表索引來取得新新增的工作表的引用
Worksheet worksheet = workbook.Worksheets[i];
```
在這裡，您將使用其索引來獲取新建立的工作表（`i`）。這使您可以操作工作表。
## 第 6 步：訪問儲存格
您需要存取工作表中的特定儲存格，在其中套用刪除線格式。在此範例中，我們使用單元格`A1`.
```csharp
//從工作表存取“A1”單元格
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
在 Excel 中，儲存格透過其列標識符和行標識符（例如「A1」）來引用。我們正在獲取對單元格的引用`A1`以便進一步操縱。
## 第 7 步：為單元添加價值
接下來，讓我們在單元格中插入一些文字。我們會寫“Hello Aspose！”在細胞內`A1`.
```csharp
//在「A1」儲存格中加入一些值
cell.PutValue("Hello Aspose!");
```
這`PutValue`方法用於將字串值指派給單元格。您可以將此字串修改為您想要顯示的任何內容。
## 步驟8：取得儲存格的樣式
現在我們的單元格中有文本，是時候訪問單元格的樣式以應用我們所需的格式，包括刪除線效果。
```csharp
//取得單元格的樣式
Style style = cell.GetStyle();
```
這`GetStyle`方法會擷取儲存格的目前樣式，讓您可以修改字體類型、大小和效果等屬性。
## 第9步：設定三振效果
讓我們對儲存格中的文字套用刪除線效果。我們將修改單元格的字體樣式。
```csharp
// ExStart:設定刪除線
//設定字體的刪除線效果
style.Font.IsStrikeout = true;
//ExEnd:設定刪除線
```
透過設定`IsStrikeout`為 true 時，您將指示 Excel 以視覺方式劃掉所選儲存格中的文字刪除線 - 非常類似於直觀地從清單中標記某些內容。
## 第 10 步：將樣式套用到儲存格
修改樣式後，您需要將其套用回儲存格以反映變更。
```csharp
//將樣式套用到儲存格
cell.SetStyle(style);
```
這`SetStyle`方法使用新樣式更新儲存格，其中現在包括刪除線格式。
## 第11步：儲存Excel文件
最後，是時候將工作簿儲存到指定的目錄了。在此範例中，我們使用名稱儲存文件`book1.out.xls`.
```csharp
//儲存 Excel 文件
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
這`Save`方法以 97-2003 Excel 格式將工作簿寫入磁碟。如果需要，您可以指定不同的格式。
## 結論
當您逐步分解時，使用 Aspose.Cells for .NET 在 Excel 中的文字上建立刪除線效果是一個簡單的過程。透過遵循本指南，您現在掌握了透過視覺提示增強電子表格的技能，使您的數據不僅資訊豐富，而且具有視覺吸引力。
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的程式庫，用於在 .NET 應用程式中管理 Excel 文件，使您能夠以程式設計方式建立、操作和轉換 Excel 文件。
### 我可以免費使用 Aspose.Cells 嗎？
是的，您可以在試用期內免費使用它。免費試用可在[Aspose.Cells 免費試用版](https://releases.aspose.com/).
### 如何購買 Aspose.Cells？
您可以透過 Aspose.Cells 網站購買許可證[購買 Aspose.Cells](https://purchase.aspose.com/buy).
### 有使用 Aspose.Cells 的範例嗎？
是的，您可以在中找到大量範例和程式碼片段[Aspose.Cells 文檔](https://reference.aspose.com/cells/net/).
### 我可以在哪裡獲得 Aspose.Cells 的支援？
您可以從以下方面獲得社區支持和幫助[Aspose論壇](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
