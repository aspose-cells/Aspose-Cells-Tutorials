---
title: 將工作簿儲存為文字 CSV 格式
linktitle: 將工作簿儲存為文字 CSV 格式
second_title: Aspose.Cells .NET Excel 處理 API
description: 在這個專為 .NET 開發人員設計的綜合逐步教學中，了解如何使用 Aspose.Cells 輕鬆將 Excel 工作簿轉換為 CSV 格式。
weight: 17
url: /zh-hant/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將工作簿儲存為文字 CSV 格式

## 介紹
處理資料時，您選擇的格式確實可以決定您使用資料的難易度。處理表格資料最常見的格式是 CSV（逗號分隔值）。如果您是使用 Excel 檔案的開發人員並且需要將工作簿轉換為 CSV 格式，Aspose.Cells for .NET 是一個出色的程式庫，可以簡化此任務。在本教學中，我們將詳細介紹將 Excel 工作簿無縫轉換為文字 CSV 格式的步驟。
## 先決條件
在我們開始之前，讓我們確保您已準備好開始使用的一切：
1. C# 和 .NET 的基本知識：由於我們將使用 C# 編寫程式碼，因此熟悉該語言和 .NET 框架至關重要。
2. Aspose.Cells 函式庫：確保您的開發環境中安裝了 Aspose.Cells for .NET 函式庫。你可以下載它[這裡](https://releases.aspose.com/cells/net/).
3. Visual Studio 或任何 C# IDE：您將需要一個整合開發環境 (IDE) 來編寫和執行程式碼。 Visual Studio 是個受歡迎的選擇。
4. Excel 工作簿：準備一個範例 Excel 工作簿（例如「book1.xls」），其中包含一些用於測試轉換的資料。
## 導入包
現在我們已經滿足了先決條件，流程的第一步是匯入必要的套件。在您的 C# 專案中，您需要在程式碼檔案頂部包含以下命名空間：
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
這些命名空間將使您能夠存取處理 Excel 檔案和管理記憶體流所需的類別和方法。
## 第 1 步：定義文檔目錄的路徑
我們流程的第一步是定義文件（Excel 工作簿）的儲存位置。這是至關重要的，因為它允許我們的程式知道在哪裡可以找到它需要處理的文件。 
```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
```
確保更換`"Your Document Directory"`與「book1.xls」檔案所在的實際路徑。這可以是電腦上的目錄或伺服器的路徑。
## 第 2 步：載入來源工作簿
接下來，我們需要載入將轉換為 CSV 格式的 Excel 工作簿。
```csharp
//載入來源工作簿
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
這`Workbook` Aspose.Cells 庫中的類別允許操作和存取 Excel 工作簿。透過傳遞檔案路徑，我們載入指定的工作簿進行處理。
## 步驟 3：為工作簿資料初始化位元組數組
在開始將工作簿轉換為 CSV 之前，我們需要初始化一個空位元組數組，該數組最終將保存所有工作表資料。
```csharp
// 0 位元組數組
byte[] workbookData = new byte[0];
```
這個位元組數組會將每個工作表中的資料組合成一個結構，我們稍後可以將其寫入檔案。
## 第 4 步：設定文字儲存選項
現在，讓我們設定如何儲存文字格式的選項。您可以選擇自訂分隔符號或堅持使用製表符。
```csharp
//文字儲存選項。您可以使用任何類型的分隔符
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; //將製表符設定為分隔符
```
在此範例中，我們使用製表符作為分隔符號。您可以更換`'\t'`使用您想要的任何字符，例如逗號 (`,`)，取決於您希望 CSV 的格式如何。
## 第 5 步：迭代每個工作表
接下來，我們將迭代工作簿中的所有工作表，將每個工作表儲存到我們的`workbookData`數組，但您必須先選擇要處理的工作表。
```csharp
//以文字格式複製工作簿資料數組中的每個工作表數據
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    //將活動工作表儲存為文字格式
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
此循環遍歷工作簿中的每個工作表。`ActiveSheetIndex`設定為每次循環時我們都會儲存目前工作表。結果將使用保存到記憶體中`MemoryStream`.
## 第 6 步：檢索工作表數據
將工作表儲存到記憶體流後，下一步是檢索該資料並將其附加到我們的`workbookData`大批。
```csharp
    //將工作表資料儲存到工作表資料數組中
    ms.Position = 0; //重置記憶體流位置
    byte[] sheetData = ms.ToArray(); //取得位元組數組
```
`ms.Position = 0;`寫入後重置讀取位置。然後，我們使用`ToArray()`將記憶體流轉換為保存工作表資料的位元組數組。
## 第 7 步：合併工作表數據
現在，我們將把每個工作表中的資料組合成一個`workbookData`數組較早初始化。
```csharp
    //將此工作表資料合併到工作簿資料數組中
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
我們建立一個足夠大的新數組，足以容納現有工作簿資料和新工作表資料。然後，我們將現有資料和新資料複製到這個組合數組中以供以後使用。
## 步驟 8：將整個工作簿資料儲存到文件中
最後，將所有數據合併到我們的`workbookData`數組，我們可以將這個數組保存到指定的檔案路徑中。
```csharp
//將整個工作簿資料儲存到檔案中
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes`取得組合的位元組陣列並將其寫入指定目錄中名為「out.txt」的文字檔案中。
## 結論
現在你就擁有了！您已使用 Aspose.Cells for .NET 成功將 Excel 工作簿轉換為 CSV 格式。此流程不僅高效，而且可以輕鬆操作 Excel 資料以進行進一步分析或報告。現在，您可以自動化資料處理任務，甚至可以將此功能整合到更大的應用程式中。
## 常見問題解答
### 我可以對 CSV 檔案使用不同的分隔符號嗎？
是的，您可以更改`opts.Separator`任何您想要的字符，例如逗號或管道。
### Aspose.Cells 可以免費使用嗎？
 Aspose.Cells 不是免費的，但您可以免費試用[這裡](https://releases.aspose.com/).
### 除了 CSV 之外，我還可以儲存哪些類型的格式？
Aspose.Cells 允許儲存為多種格式，包括 XLSX、PDF 等。
### 我可以使用 Aspose.Cells 處理大型 Excel 檔案嗎？
是的，Aspose.Cells 旨在有效地處理大文件，但效能可能取決於系統資源。
### 在哪裡可以找到更詳細的文件？
您可以在其上找到全面的文檔和範例[參考站點](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
