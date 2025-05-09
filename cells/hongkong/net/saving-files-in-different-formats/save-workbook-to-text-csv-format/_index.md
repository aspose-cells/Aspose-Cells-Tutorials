---
"description": "透過這個專為 .NET 開發人員設計的全面、循序漸進的教程，了解如何使用 Aspose.Cells 輕鬆地將 Excel 工作簿轉換為 CSV 格式。"
"linktitle": "將工作簿儲存為文字 CSV 格式"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "將工作簿儲存為文字 CSV 格式"
"url": "/zh-hant/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 將工作簿儲存為文字 CSV 格式

## 介紹
處理資料時，您選擇的格式實際上可以決定您處理資料的難易程度。處理表格資料最常見的格式之一是 CSV（逗號分隔值）。如果您是使用 Excel 檔案的開發人員，並且需要將工作簿轉換為 CSV 格式，Aspose.Cells for .NET 是一個可以簡化此任務的絕佳程式庫。在本教程中，我們將分解將 Excel 工作簿無縫轉換為文字 CSV 格式的步驟。
## 先決條件
在我們深入研究之前，請確保您已準備好一切可以開始：
1. C# 和 .NET 的基礎知識：由於我們將使用 C# 編寫程式碼，因此熟悉該語言和 .NET 框架至關重要。
2. Aspose.Cells 函式庫：確保您的開發環境中安裝了 Aspose.Cells for .NET 函式庫。你可以下載它 [這裡](https://releases。aspose.com/cells/net/).
3. Visual Studio 或任何 C# IDE：您將需要一個整合開發環境 (IDE) 來編寫和執行您的程式碼。 Visual Studio 是個受歡迎的選擇。
4. Excel 工作簿：準備一個包含一些資料的範例 Excel 工作簿（例如「book1.xls」）來測試轉換。
## 導入包
現在我們已經滿足了先決條件，接下來的第一步就是匯入必要的套件。在您的 C# 專案中，您需要在程式碼檔案的頂部包含以下命名空間：
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
這些命名空間將使您能夠存取處理 Excel 檔案和管理記憶體流所需的類別和方法。
## 步驟 1：定義文檔目錄的路徑
我們流程的第一步是定義我們的文件（Excel 工作簿）的儲存位置。這很重要，因為它使我們的程式知道在哪裡可以找到需要處理的文件。 
```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory";
```
確保更換 `"Your Document Directory"` 使用“book1.xls”檔案所在的實際路徑。這可能是您電腦上的目錄或伺服器的路徑。
## 第 2 步：載入來源工作簿
接下來，我們需要載入將轉換為 CSV 格式的 Excel 工作簿。
```csharp
// 載入來源工作簿
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
這 `Workbook` Aspose.Cells 庫中的類別允許操作和存取 Excel 工作簿。透過傳遞檔案路徑，我們正在載入指定的工作簿進行處理。
## 步驟 3：初始化工作簿資料的位元組數組
在開始將工作簿轉換為 CSV 之前，我們需要初始化一個空位元組數組，該數組最終將保存所有工作表資料。
```csharp
// 0位元組數組
byte[] workbookData = new byte[0];
```
這個位元組數組將把每個工作表的資料組合成一個單一的結構，我們稍後可以將其寫入文件。
## 步驟 4：設定文字儲存選項
現在，讓我們設定如何儲存文字格式的選項。您可以選擇自訂分隔符號或堅持使用製表符。
```csharp
// 文字儲存選項。您可以使用任何類型的分隔符
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // 將製表符設定為分隔符
```
在此範例中，我們使用製表符作為分隔符號。您可以替換 `'\t'` 任何你想要的字符，例如逗號 (`,`)，取決於您希望 CSV 如何格式化。
## 步驟 5：遍歷每個工作表
接下來，我們將遍歷工作簿中的所有工作表，並將每個工作表儲存到我們的 `workbookData` 數組，但您必須先選擇要處理的工作表。
```csharp
// 將每個工作表資料以文字格式複製到工作簿資料數組中
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // 將活動工作表儲存為文字格式
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
循環遍歷工作簿中的每個工作表。 `ActiveSheetIndex` 設定這樣，每次循環時，我們都會儲存目前工作表。結果將使用 `MemoryStream`。
## 步驟 6：檢索工作表數據
將工作表儲存到記憶體流後，下一步是檢索此資料並將其附加到我們的 `workbookData` 大批。
```csharp
    // 將工作表資料儲存到工作表資料數組中
    ms.Position = 0; // 記憶體流的重置位置
    byte[] sheetData = ms.ToArray(); // 取得位元組數組
```
`ms.Position = 0;` 寫入後重置讀取位置。然後我們使用 `ToArray()` 將記憶體流轉換為保存工作表資料的位元組數組。
## 步驟 7：合併工作表數據
現在，我們將每個工作表中的資料合併到單一 `workbookData` 數組先前已初始化。
```csharp
    // 將此工作表資料合併到工作簿資料數組中
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
我們建立一個足夠大的新數組來容納現有工作簿資料和新工作表資料。然後我們將現有資料和新資料複製到這個組合數組中以供以後使用。
## 步驟 8：將整個工作簿資料儲存到文件中
最後，將所有數據合併到我們的 `workbookData` 數組，我們可以將這個數組保存到指定的檔案路徑下。
```csharp
// 將整個工作簿資料儲存到檔案中
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` 取得組合的位元組陣列並將其寫入指定目錄中名為「out.txt」的文字檔案中。
## 結論
就是這樣！您已成功使用 Aspose.Cells for .NET 將 Excel 工作簿轉換為 CSV 格式。這個過程不僅高效，而且還可以輕鬆操作 Excel 資料以進行進一步分析或報告。現在您可以自動執行資料處理任務，甚至可以將此功能整合到更大的應用程式中。
## 常見問題解答
### 我可以對 CSV 檔案使用不同的分隔符號嗎？
是的，你可以更改 `opts.Separator` 為您想要的任何字符，例如逗號或豎線。
### Aspose.Cells 可以免費使用嗎？
Aspose.Cells 不是免費的，但您可以免費試用 [這裡](https://releases。aspose.com/).
### 除了 CSV 之外，我還可以儲存哪些格式？
Aspose.Cells 允許儲存為多種格式，包括 XLSX、PDF 等。
### 我可以使用 Aspose.Cells 處理大型 Excel 檔案嗎？
是的，Aspose.Cells 旨在有效處理大文件，但效能可能取決於系統資源。
### 在哪裡可以找到更詳細的文件？
您可以在其網站上找到全面的文件和範例 [參考站點](https://reference。aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}