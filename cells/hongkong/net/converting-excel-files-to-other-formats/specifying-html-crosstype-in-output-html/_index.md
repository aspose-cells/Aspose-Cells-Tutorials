---
title: 在 .NET 中以程式設計方式指定輸出 HTML 中的 HTML CrossType
linktitle: 在 .NET 中以程式設計方式指定輸出 HTML 中的 HTML CrossType
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何在 Aspose.Cells for .NET 中指定 HTML CrossType。按照我們的逐步教學將 Excel 檔案精確轉換為 HTML。
weight: 17
url: /zh-hant/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以程式設計方式指定輸出 HTML 中的 HTML CrossType

## 介紹
在 .NET 應用程式中將 Excel 檔案轉換為 HTML 時，您可能會發現自己需要指定如何在輸出中處理交叉引用。 Aspose.Cells for .NET 中的 HtmlSaveOptions 類別提供了各種設定來控制轉換過程，其中之一是 HtmlCrossType。在本教學中，我們將介紹如何在將 Excel 檔案匯出為 HTML 格式時以程式設計方式指定 HTML 交叉類型。 
## 先決條件
在深入研究程式碼之前，請確保您具備以下條件：
-  Aspose.Cells for .NET：請確定您的專案中安裝了 Aspose.Cells 函式庫。您可以從[阿斯普斯網站](https://releases.aspose.com/cells/net/).
- Visual Studio：Visual Studio 或任何其他 .NET 開發環境的有效安裝。
- C#基礎知識：熟悉C#程式設計將有助於您更好地理解範例。
- 範例 Excel 檔案：準備好一個範例 Excel 檔案以供使用。對於這個例子，我們將使用`sampleHtmlCrossStringType.xlsx`.
## 導入包
首先，您需要匯入必要的 Aspose.Cells 命名空間。您可以這樣做：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
讓我們逐步分解這一點，以便您可以輕鬆地在自己的專案中遵循並實現此功能。
## 第 1 步：定義來源目錄和輸出目錄
首先，您需要設定來源 Excel 檔案的目錄以及要儲存輸出 HTML 檔案的位置。
```csharp
//原始碼目錄
string sourceDir = "Your Document Directory";
//輸出目錄
string outputDir = "Your Document Directory";
```
## 第 2 步：載入範例 Excel 文件
接下來，將範例 Excel 檔案載入到`Workbook`目的。這就是所有魔法的開始。
```csharp
//載入範例 Excel 文件
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
在這裡，替換`"Your Document Directory"`與 Excel 檔案所在的實際路徑。此行將 Excel 檔案讀取到記憶體中，以便您可以對其進行操作。
## 步驟 3：指定 HTML 儲存選項
現在，我們將建立一個實例`HtmlSaveOptions`，它允許您配置如何將 Excel 文件轉換為 HTML。
```csharp
//指定 HTML 交叉類型
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
在這一步中，我們設定了`HtmlCrossStringType`到`HtmlCrossType.Default`，這是可用於處理輸出 HTML 中的交叉引用的選項之一。
## 步驟 4：根據需要更改交叉類型
您可以指定不同的類型`HtmlCrossStringType`根據您的要求。以下是您可以使用的各種選項：
- `HtmlCrossType.Default`：預設十字類型。
- `HtmlCrossType.MSExport`：以類似 MS Excel 的行為匯出 HTML。
- `HtmlCrossType.Cross`：建立交叉引用。
- `HtmlCrossType.FitToCell`：使交叉引用適合單元格尺寸。
您可以修改`HtmlCrossStringType`像這樣：
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExport;
//或者
opts.HtmlCrossStringType = HtmlCrossType.Cross;
//或者
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## 第 5 步：儲存輸出 HTML 文件
配置完選項後，就可以儲存轉換後的 HTML 檔案了。使用`Save`方法對你的`Workbook`目的：
```csharp
//輸出HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
在這裡，我們根據以下內容命名輸出文件`HtmlCrossStringType`我們已經設定了。這樣，您可以輕鬆識別轉換中使用的交叉類型。
## 第六步：確認執行成功
最後，確認您的操作是否成功始終是一個很好的做法。您可以將訊息列印到控制台：
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
這會讓您知道該過程已完成，沒有任何錯誤。
## 結論
現在你就擁有了！您已使用 Aspose.Cells 成功為 .NET 中的 Excel 匯出指定了 HTML 交叉類型。當您需要在 HTML 輸出中維護特定格式或引用時，此功能特別有用，以確保轉換後的文件符合您的要求。
## 常見問題解答
### Aspose.Cells 中的 HtmlCrossType 是什麼？  
HtmlCrossType 定義在 HTML 轉換期間如何處理 Excel 檔案中的交叉引用。您可以選擇「預設」、「MSExport」、「交叉」和「FitToCell」等選項。
### 我可以免費使用 Aspose.Cells 嗎？  
 Aspose.Cells 提供免費試用版。你可以從他們那裡下載[網站](https://releases.aspose.com/).
### 如何在我的 .NET 專案中安裝 Aspose.Cells？  
您可以透過 Visual Studio 中的 NuGet 套件管理器執行以下命令來安裝 Aspose.Cells：`Install-Package Aspose.Cells`.
### 在哪裡可以找到 Aspose.Cells 的文件？  
您可以找到有關 Aspose.Cells 的綜合文檔[這裡](https://reference.aspose.com/cells/net/).
### 如果儲存 HTML 檔案時遇到錯誤，該怎麼辦？  
確保目錄路徑正確且您對輸出目錄具有寫入權限。如果問題仍然存在，請查看 Aspose 支援論壇尋求協助。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
