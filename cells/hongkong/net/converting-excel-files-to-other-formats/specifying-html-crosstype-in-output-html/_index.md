---
"description": "了解如何在 Aspose.Cells for .NET 中指定 HTML CrossType。按照我們的逐步教程，將 Excel 檔案精確地轉換為 HTML。"
"linktitle": "在 .NET 中以程式設計方式在輸出 HTML 中指定 HTML CrossType"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 .NET 中以程式設計方式在輸出 HTML 中指定 HTML CrossType"
"url": "/zh-hant/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以程式設計方式在輸出 HTML 中指定 HTML CrossType

## 介紹
當在 .NET 應用程式中將 Excel 檔案轉換為 HTML 時，您可能會發現需要指定如何在輸出中處理交叉引用。 Aspose.Cells for .NET 中的 HtmlSaveOptions 類別提供了各種設定來控制轉換過程，其中一個選項是 HtmlCrossType。在本教學中，我們將介紹如何在將 Excel 檔案匯出為 HTML 格式時以程式設計方式指定 HTML 交叉類型。 
## 先決條件
在深入研究程式碼之前，請確保您已具備以下條件：
- Aspose.Cells for .NET：請確定您的專案中安裝了 Aspose.Cells 函式庫。您可以從 [Aspose 網站](https://releases。aspose.com/cells/net/).
- Visual Studio：Visual Studio 或任何其他 .NET 開發環境的工作安裝。
- C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解範例。
- 範例 Excel 檔案：準備好一個範例 Excel 檔案以供使用。對於這個例子，我們將使用 `sampleHtmlCrossStringType。xlsx`.
## 導入包
首先，您需要匯入必要的 Aspose.Cells 命名空間。您可以按照以下步驟操作：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
讓我們逐步分解它，以便您可以輕鬆地跟隨並在自己的專案中實現此功能。
## 步驟 1：定義來源目錄和輸出目錄
首先，您需要設定來源 Excel 檔案的目錄以及要儲存輸出 HTML 檔案的目錄。
```csharp
// 來源目錄
string sourceDir = "Your Document Directory";
// 輸出目錄
string outputDir = "Your Document Directory";
```
## 步驟 2：載入範例 Excel 文件
接下來，將範例 Excel 檔案載入到 `Workbook` 目的。一切魔法都從這裡開始。
```csharp
// 載入範例 Excel 文件
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
在這裡，替換 `"Your Document Directory"` 使用您的 Excel 檔案所在的實際路徑。此行將 Excel 檔案讀入內存，以便您可以對其進行操作。
## 步驟 3：指定 HTML 儲存選項
現在，我們將創建一個 `HtmlSaveOptions`，它允許您配置如何將 Excel 文件轉換為 HTML。
```csharp
// 指定 HTML 交叉類型
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
在此步驟中，我們設定了 `HtmlCrossStringType` 到 `HtmlCrossType.Default`，這是處理輸出 HTML 中的交叉引用可用的選項之一。
## 步驟 4：根據需要更改十字架類型
您可以指定不同的類型 `HtmlCrossStringType` 根據您的要求。以下是您可以使用的各種選項：
- `HtmlCrossType.Default`：預設十字類型。
- `HtmlCrossType.MSExport`：以類似 MS Excel 的行為匯出 HTML。
- `HtmlCrossType.Cross`：建立交叉引用。
- `HtmlCrossType.FitToCell`：使交叉引用適合單元格尺寸。
您可以修改 `HtmlCrossStringType` 像這樣：
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExp或者t;
// 或者 
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// or
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## 步驟5：儲存輸出HTML文件
配置完選項後，就可以儲存轉換後的 HTML 檔案了。使用 `Save` 方法 `Workbook` 目的：
```csharp
// 輸出 HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
在這裡，我們根據 `HtmlCrossStringType` 我們已經設定了。這樣，您可以輕鬆識別轉換中使用了哪種交叉類型。
## 步驟6：確認執行成功
最後，確認操作成功始終是個好的做法。您可以將訊息列印到控制台：
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
這將讓您知道該過程已完成且沒有任何錯誤。
## 結論
就是這樣！您已成功使用 Aspose.Cells 在 .NET 中為 Excel 匯出指定 HTML 交叉類型。當您需要在 HTML 輸出中保留特定格式或引用時，此功能特別有用，可確保轉換後的文件符合您的要求。
## 常見問題解答
### Aspose.Cells 中的 HtmlCrossType 是什麼？  
HtmlCrossType 定義在 HTML 轉換期間如何處理 Excel 檔案中的交叉引用。您可以選擇預設、MSExport、Cross 和 FitToCell 等選項。
### 我可以免費使用 Aspose.Cells 嗎？  
Aspose.Cells 提供免費試用版。您可以從他們的網站下載 [網站](https://releases。aspose.com/).
### 如何在我的.NET專案中安裝Aspose.Cells？  
您可以透過執行以下命令在 Visual Studio 中透過 NuGet 套件管理器安裝 Aspose.Cells： `Install-Package Aspose。Cells`.
### 在哪裡可以找到 Aspose.Cells 的文件？  
您可以在 Aspose.Cells 上找到全面的文檔 [這裡](https://reference。aspose.com/cells/net/).
### 如果儲存 HTML 檔案時遇到錯誤，該怎麼辦？  
確保目錄路徑正確並且您對輸出目錄具有寫入權限。如果問題仍然存在，請查看 Aspose 支援論壇以獲取協助。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}