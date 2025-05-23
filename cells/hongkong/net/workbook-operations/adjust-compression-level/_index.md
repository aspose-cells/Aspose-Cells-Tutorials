---
"description": "透過本逐步指南了解如何使用 Aspose.Cells for .NET 調整 Excel 工作簿的壓縮等級。優化您的檔案管理。"
"linktitle": "調整工作簿中的壓縮等級"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "調整工作簿中的壓縮等級"
"url": "/zh-hant/net/workbook-operations/adjust-compression-level/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 調整工作簿中的壓縮等級

## 介紹
當談到管理大型 Excel 檔案時，壓縮可以改變遊戲規則。它不僅節省儲存空間，而且使檔案傳輸更快、更有效率。如果您使用 Aspose.Cells for .NET，您可以輕鬆調整工作簿的壓縮等級。在本指南中，我們將逐步引導您完成整個過程，確保您了解程式碼的每個部分及其工作原理。
## 先決條件
在深入研究程式碼之前，您需要滿足一些先決條件：
1. C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解程式碼片段。
2. Aspose.Cells 函式庫：您需要安裝 Aspose.Cells 函式庫。您可以從下載 [這裡](https://releases。aspose.com/cells/net/).
3. Visual Studio：執行程式碼需要像 Visual Studio 這樣的開發環境。
4. .NET Framework：確保您的專案設定了相容版本的 .NET Framework。
## 導入包
首先，您需要在 C# 專案中匯入必要的套件。您可以按照以下步驟操作：
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
這些套件對於使用 Aspose.Cells 庫處理 Excel 檔案至關重要。這 `Aspose.Cells` 命名空間包含操作 Excel 檔案所需的所有類，而 `Aspose.Cells.Xlsb` 提供以 XLSB 格式儲存檔案的選項。
現在，讓我們將調整工作簿中的壓縮等級的過程分解為易於管理的步驟。
## 步驟 1：定義來源和輸出目錄
首先，您需要指定原始檔案的位置以及要儲存輸出檔案的位置。這對於確保您的程式知道在哪裡找到需要處理的文件至關重要。
```csharp
// 來源目錄
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
代替 `"Your Document Directory"` 使用目錄的實際路徑。這將幫助程式找到您想要壓縮的檔案。
## 第 2 步：載入工作簿
接下來，您將載入要壓縮的工作簿。這就是魔法開始的地方！
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
在這一行中，我們創建了 `Workbook` 類別並載入現有的 Excel 文件。確保檔案名稱與來源目錄中的檔案名稱相符。
## 步驟 3：設定儲存選項
現在是時候配置儲存選項了。我們將設定輸出檔案的壓縮類型。 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
這 `XlsbSaveOptions` 類別可讓您在以 XLSB 格式儲存工作簿時指定各種選項，包括壓縮等級。
## 步驟 4：測量 1 級壓縮時間
讓我們從第一個壓縮等級開始。我們將測量使用此等級的壓縮保存工作簿需要多長時間。
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
這裡我們將壓縮類型設定為 1 級，儲存工作簿，然後測量經過的時間。這讓我們了解該過程需要多長時間。
## 步驟 5：測量第 6 級的壓縮時間
接下來我們來看看6級壓縮的表現如何。
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
這一步驟與上一步類似，但我們將壓縮等級變更為 6 級。您會注意到，所花費的時間可能會根據工作簿的複雜程度而有所不同。
## 步驟 6：測量第 9 級的壓縮時間
最後，我們來看看最高壓縮等級的效能。
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
在此步驟中，我們將壓縮等級設為 9 級。此時您通常會看到檔案大小最顯著的減少，但處理時間可能會更長。
## 步驟7：最終輸出
運行完所有壓縮等級後，可以輸出一條訊息，表示該過程已成功完成。
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
這行簡單的程式碼確認您的程式已順利完成執行。
## 結論
使用 Aspose.Cells for .NET 調整工作簿的壓縮等級是一個簡單的過程，可以在檔案大小和效能方面帶來顯著的益處。透過遵循本指南中概述的步驟，您可以輕鬆地在應用程式中實現壓縮並提高 Excel 文件管理的效率。
## 常見問題解答
### 什麼是 Aspose.Cells？  
Aspose.Cells 是一個強大的 .NET 程式庫，可讓開發人員建立、操作和轉換 Excel 文件，而無需 Microsoft Excel。
### 如何安裝 Aspose.Cells？  
您可以從 [Aspose 網站](https://releases。aspose.com/cells/net/).
### 有哪些壓縮等級可用？  
Aspose.Cells 支援多種壓縮級別，從 1 級（最低壓縮）到 9 級（最高壓縮）。
### 我可以免費測試 Aspose.Cells 嗎？  
是的！您可以免費試用 Aspose.Cells [這裡](https://releases。aspose.com/).
### 在哪裡可以找到對 Aspose.Cells 的支援？  
如有任何疑問或需要支持，您可以訪問 Aspose 支持論壇 [這裡](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}