---
title: 在 Excel 中以程式設計方式使用複製方法
linktitle: 在 Excel 中以程式設計方式使用複製方法
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 中的複製方法有效地操作 Excel 檔案。包括逐步指南。
weight: 10
url: /zh-hant/net/excel-formatting-methods-and-options/using-copy-method/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中以程式設計方式使用複製方法

## 介紹
當談到以程式方式管理和操作電子表格時，Aspose.Cells for .NET 是一個強大的工具，可以節省您的時間並簡化您的工作流程。開發人員面臨的常見任務之一是需要將 Excel 工作簿中的一個工作表的範圍複製到另一個工作表。在本教程中，我們將引導您使用 Aspose.Cells 中的 Copy 方法，透過清晰的解釋和程式碼範例引導您完成每個步驟。
## 先決條件
在我們深入了解使用複製方法的步驟之前，您需要確保滿足以下先決條件：
1. .NET Framework：請確定您的電腦上安裝了 .NET Framework。 Aspose.Cells 與各種版本相容，因此請檢查它們[文件](https://reference.aspose.com/cells/net/)了解具體情況。
2. Visual Studio：為 .NET 開發設定 Visual Studio 或任何相容的 IDE 至關重要。這將幫助您輕鬆建立和管理專案。
3.  Aspose.Cells 庫：從以下位置下載 Aspose.Cells 庫：[發布頁面](https://releases.aspose.com/cells/net/)並在您的項目中添加對它的引用。
4.  Excel 檔案範例：建立或準備好 Excel 檔案（例如，`Book1.xlsx`）您將在本教程中使用它。
5. 基本 C# 知識：熟悉 C# 語言概念和文法。
滿足這些先決條件後，您就可以開始編碼了！
## 導入包
要使用Aspose.Cells提供的功能，您需要匯入必要的套件。在您的 C# 專案中，請確保在程式碼檔案頂部包含以下 using 指令：
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
這使您可以存取輕鬆操作 Excel 文件所需的類別和方法。
現在一切都已就緒，讓我們將使用 Copy 方法的流程分解為可管理的步驟。我們首先載入 Excel 文件，然後繼續複製所需的範圍。
## 第 1 步：設定檔案流
第一步是建立一個文件流，允許我們打開並使用 Excel 文件。操作方法如下：
```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
//建立包含要開啟的 Excel 檔案的檔案流
FileStream fstream = new FileStream(dataDir + "Book1.xlsx", FileMode.Open);
```
在此程式碼中，您需要指定您的路徑`Book1.xlsx`文件位於。這`FileMode.Open`參數表示我們要開啟一個現有文件。
## 第 2 步：開啟工作簿
接下來，我們將使用剛剛設定的檔案流建立一個 Workbook 物件。這使我們能夠存取 Excel 文件的內容。
```csharp
//透過檔案流程開啟Excel文件
Workbook workbook = new Workbook(fstream);
```
此時，我們已開啟工作簿並可以開始處理其內容。
## 第 3 步：訪問工作表
載入工作簿後，我們需要存取要使用的特定工作表。通常，這將是工作簿中的第一個工作表。
```csharp
//存取 Excel 文件中的第一個工作表
Worksheet worksheet = workbook.Worksheets[0];
```
這裡，`Worksheets[0]`抓住第一張紙。如果您想存取任何其他工作表，只需更改索引即可。
## 第 4 步：複製範圍
現在是主要部分－複製儲存格範圍。在本教學中，我們將示範如何將條件格式設定從一個儲存格複製到另一個儲存格，以及如何複製 Excel 工作表的整個範圍。
### 複製條件格式（範例）
```csharp
//將條件格式設定從儲存格“A1”複製到儲存格“B1”
//工作表.CopyConditionalFormatting(0, 0, 0, 1);
```
此行在原始程式碼中被註解掉，但它向您展示如何在同一工作表上將條件格式從儲存格 A1 複製到儲存格 B1。這些參數表示來源單元格和目標單元格的行索引和列索引。如果需要此功能，可以取消註解。
### 複製整個範圍（範例）
我們可以進一步擴展複製功能以包括複製整個範圍，為此我們將使用循環來遍歷所有工作表。
```csharp
int TotalRowCount = 0;
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    //存取每個工作表
    Worksheet sourceSheet = workbook.Worksheets[i];
    //取得工作表中的顯示範圍
    Range sourceRange = sourceSheet.Cells.MaxDisplayRange;
    //在目標工作表中建立範圍
    Range destRange = worksheet.Cells.CreateRange(
        sourceRange.FirstRow + TotalRowCount,
        sourceRange.FirstColumn,
        sourceRange.RowCount,
        sourceRange.ColumnCount);
    //將來源範圍複製到目標範圍
    destRange.Copy(sourceRange);
    //更新下一次循環迭代的總行數
    TotalRowCount += sourceRange.RowCount; 
}
```
## 步驟5：儲存修改後的工作簿
複製所需範圍後，您需要儲存修改後的工作簿以保留變更。方法如下：
```csharp
//儲存修改後的Excel文件
workbook.Save(dataDir + "output.xls");
```
此程式碼會將修改後的工作簿儲存為`output.xls`在您指定的目錄中。確保選擇適合您需求的適當格式。 
## 第6步：關閉檔案流
最後，為了確保釋放系統資源，我們需要關閉最初開啟的檔案流。
```csharp
//關閉文件流以釋放所有資源
fstream.Close();
```
就這樣，您已成功完成複製範圍並儲存更新的 Excel 檔案的過程！
## 結論
使用 Aspose.Cells for .NET 中的 Copy 方法為您提供了輕鬆操作 Excel 檔案的強大功能。透過遵循此逐步指南，您可以有效地將儲存格範圍和條件格式從一個工作表複製到另一個工作表，從而簡化資料管理任務。 
## 常見問題解答
### 什麼是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一個函式庫，可讓開發人員在 .NET 應用程式中以程式設計方式建立、操作和管理 Excel 檔案。
### 我可以使用 Aspose.Cells 複製格式、公式和值嗎？
是的，Aspose.Cells 不僅允許您複製值，還允許您複製範圍之間的格式和公式。
### Aspose.Cells 可以免費使用嗎？
 Aspose.Cells 提供免費試用，但要繼續使用，必須購買許可證。您可以找到更多信息[這裡](https://purchase.aspose.com/buy).
### 如果遇到問題，我該如何獲得支援？
您可以透過 Aspose 支援論壇尋求協助[這裡](https://forum.aspose.com/c/cells/9).
### 哪裡可以下載 Aspose.Cells 函式庫？
您可以從發布頁面下載該程式庫[這裡](https://releases.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
