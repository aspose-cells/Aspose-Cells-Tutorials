---
"description": "了解如何使用 Aspose.Cells for .NET 將 HTML 載入到 Excel 時自動調整列和行。包含逐步指南。"
"linktitle": "在工作簿中載入 HTML 時自動調整列和行"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在工作簿中載入 HTML 時自動調整列和行"
"url": "/zh-hant/net/loading-and-saving-excel-files-with-options/auto-fitting-columns-and-rows/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在工作簿中載入 HTML 時自動調整列和行

## 介紹
有沒有想過如何在使用 Aspose.Cells for .NET 將 HTML 內容載入到 Excel 工作簿時自動調整列和行的大小？嗯，您來對地方了！在本教學中，我們將深入探討如何將 HTML 表載入到工作簿中，並確保列和行自動調整以符合內容。如果您處理的是經常變化的動態數據，本指南將協助您從 HTML 建立格式良好的 Excel 工作表。
### 先決條件
在進入代碼之前，您需要在系統上設定一些東西。別擔心，它簡單又直接！
1. 已安裝 Visual Studio：您需要 Visual Studio 或任何其他 .NET 開發環境。
2. Aspose.Cells for .NET：您可以 [下載最新版本](https://releases.aspose.com/cells/net/) 或使用 NuGet 套件管理器來安裝它。
3. .NET Framework：確保您已安裝 .NET Framework 4.0 或更高版本。
4. 對 C# 的基本了解：對 C# 有一些了解將使本教學對您來說更加順利。
5. HTML 表格資料：準備一些您想要載入到 Excel 中的 HTML 內容（甚至是基本表格）。
## 導入包
首先，讓我們匯入必要的命名空間以開始。以下是您需要匯入的內容的簡單清單：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
這些套件可讓您處理工作簿、操作 HTML 資料並將其無縫載入到 Excel 中。
讓我們將這個過程分解成易於管理的部分，以便您可以輕鬆跟進。最後，您將獲得一個工作範例，說明如何在使用 Aspose.Cells for .NET 將 HTML 載入到工作簿時自動調整列和行。
## 步驟 1：設定文檔目錄
為了輕鬆保存和檢索文件，我們將指定儲存文件的路徑。您可以用自己的資料夾位置替換目錄路徑。
```csharp
string dataDir = "Your Document Directory";
```
此行設定了儲存 Excel 檔案的目錄。在處理多個項目時，正確組織文件非常重要。想像一下這是您專案的文件櫃！
## 步驟 2：將 HTML 資料建立為字串
接下來，我們將定義一些基本的 HTML 內容。為了本例，我們將使用一個簡單的 HTML 表格。您可以根據專案的需要進行客製化。
```csharp
string sampleHtml = "<html><body><table><tr><td>This is sample text.</td><td>Some text.</td></tr><tr><td>This is another sample text.</td><td>Some text.</td></tr></table></body></html>";
```
我們在這裡定義一個非常基本的 HTML 字串。它包含一個有幾行和幾列的表格。您可以根據需要新增更多行或列。想像一下煮飯前準備食材的過程！
## 步驟3：將HTML字串載入到MemoryStream中
現在我們已經準備好 HTML 內容，下一步是使用 `MemoryStream`。這使得我們可以在記憶體中操作 HTML 內容，而無需先將其儲存到磁碟。
```csharp
MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(sampleHtml));
```
透過將 HTML 字串轉換為位元組數組並將其輸入到 `MemoryStream`，我們可以處理記憶體中的 HTML 資料。想像一下，這一步就像在將菜餚放入烤箱之前先在鍋中準備菜餚！
## 步驟 4：將 MemoryStream 載入到工作簿中（不自動調整）
一旦我們將 HTML 內容放入記憶體中，我們就會將其載入到 Aspose `Workbook`。此時，我們還不能自動調整列和行。這是我們的“之前”場景，以便與稍後自動調整的版本進行比較。
```csharp
Workbook wb = new Workbook(ms);
wb.Save(dataDir + "outputWithout_AutoFitColsAndRows.xlsx");
```
工作簿已載入 HTML 內容，但列和行尚未自動適應文字。想像一下，就像烤蛋糕但忘記檢查溫度一樣——雖然可以，但可能並不完美！
## 步驟 5：啟用自動調整功能，指定 HTML 載入選項
現在，魔術就在這裡！我們建立一個實例 `HtmlLoadOptions` 並啟用 `AutoFitColsAndRows` 財產。這確保了當載入 HTML 內容時，列和行會進行調整以適應其中的內容。
```csharp
HtmlLoadOptions opts = new HtmlLoadOptions();
opts.AutoFitColsAndRows = true;
```
透過設定此選項，我們告訴 Aspose.Cells 自動調整行和列的大小。想像一下將烤箱設定到完美的溫度，以便蛋糕剛好膨脹！
## 步驟 6：將 HTML 載入到工作簿中並啟用自動調整
現在我們再次載入 HTML 內容，但這次使用 `AutoFitColsAndRows` 選項已啟用。這將根據列寬和行高的內容調整列寬和行高。
```csharp
wb = new Workbook(ms, opts);
wb.Save(dataDir + "outputWith_AutoFitColsAndRows.xlsx");
```
此步驟將 HTML 內容載入到新的工作簿中並將其儲存為 Excel 文件，但現在列和行已自動調整！想像一下，這就像一個完美烘焙的蛋糕，所有東西的尺寸都恰到好處。
## 結論
透過遵循這些簡單的步驟，您已經了解如何使用 Aspose.Cells for .NET 將 HTML 內容載入到工作簿中並自動調整列和行。無論內容多麼動態，這都可以確保您的 Excel 表始終看起來整潔。它是一個簡單但功能強大的功能，可以為您節省大量格式化和組織 Excel 資料的時間。
現在您已經掌握了這些知識，您可以嘗試更複雜的 HTML 內容，新增樣式，甚至從網頁建立整個 Excel 工作簿！
## 常見問題解答
### 我可以使用此方法來載入大型 HTML 表格嗎？
是的，Aspose.Cells 可以有效地處理大型 HTML 表，但為了獲得最佳效能，建議使用您的資料大小進行測試。
### 自動調整後我可以手動套用特定的列寬和行高嗎？
絕對地！即使使用自動調整功能後，您仍然可以自訂單一列和行。
### 載入 HTML 後如何設定表格樣式？
載入 HTML 後，您可以使用 Aspose.Cells 的廣泛樣式選項套用樣式。
### Aspose.Cells for .NET 是否與舊版的 .NET Framework 相容？
是的，Aspose.Cells for .NET 支援 .NET Framework 4.0 及更高版本。
### 我可以使用 Aspose.Cells 將 HTML 以外的其他類型的內容載入到 Excel 中嗎？
是的，Aspose.Cells 支援將各種格式（如 CSV、JSON 和 XML）載入到 Excel 中。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}