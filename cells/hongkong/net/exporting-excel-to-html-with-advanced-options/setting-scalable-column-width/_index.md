---
title: 在 Excel 中以程式設定可縮放列寬
linktitle: 在 Excel 中以程式設定可縮放列寬
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 以程式設計方式設定 Excel 檔案中的可縮放列寬。非常適合高效率的數據呈現。
weight: 20
url: /zh-hant/net/exporting-excel-to-html-with-advanced-options/setting-scalable-column-width/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中以程式設定可縮放列寬

## 介紹
Excel 是一個令人驚嘆的工具，有助於簡化資料管理、分析和報表。然而，有時完美地對齊所有東西可能會讓人感覺就像你試圖將方釘裝入一個圓孔中。值得慶幸的是，使用 Aspose.Cells for .NET，您不僅可以處理電子表格需求，還可以透過程式設計自訂列寬等方面。在本文中，我們將詳細指導您如何使用 C# 在 Excel 檔案中設定可縮放的列寬。準備好潛入了嗎？我們走吧！
## 先決條件
在我們開始編碼之前，您需要設定一些東西。將此視為在開始 DIY 專案之前收集工具。這是您需要的：
1. Visual Studio：確保您的電腦上安裝了 Visual Studio。這是我們用於 .NET 應用程式的主要環境。
2.  Aspose.Cells 函式庫：您需要安裝 Aspose.Cells for .NET。這可以從以下位置下載[Aspose 發布](https://releases.aspose.com/cells/net/)頁。 
3. C# 基礎知識：掌握 C# 程式設計將很有幫助，因為我們將用這種語言編寫程式碼。如果您是初學者，請不要擔心。我們會邊走邊解釋事情。
4.  Excel 檔案：為了進行測試，請確保您有一個 Excel 檔案（假設`sampleForScalableColumns.xlsx`） 準備好。這將是我們修改的文件。
現在您已經準備好了，讓我們逐步分解這個過程。
## 導入包
要開始使用我們的程式碼，我們需要導入必要的庫。確保您的項目中包含 Aspose.Cells。您可以這樣做：
## 第 1 步：設定您的項目
- 開啟 Visual Studio 並建立一個新的控制台應用程式。
- 在解決方案資源管理器中，右鍵單擊您的專案並選擇`Manage NuGet Packages`.
- 搜尋`Aspose.Cells`並安裝它。這確保我們可以存取 Aspose.Cells 的所有功能。
## 第 2 步：新增 using 指令
在 C# 檔案的頂部，您需要匯入所需的 Aspose.Cells 命名空間：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
這使得 Aspose.Cells 庫中的類別可供使用。
現在您已經完成了所有設置，讓我們開始實際編碼。我們將詳細介紹每個部分，確保您了解正在發生的事情。
## 第 1 步：定義輸入和輸出目錄
在此初始步驟中，您將指定輸入檔案的位置以及輸出檔案的儲存位置。 
```csharp
//輸入目錄
string sourceDir = "Your Document Directory"; 
//輸出目錄
string outputDir = "Your Document Directory"; 
```
確保更換`"Your Document Directory"`與目錄的實際路徑。這很重要，因為如果路徑不正確，程式將找不到 Excel 檔案。
## 第 2 步：載入範例 Excel 文件
接下來，您將把 Excel 檔案載入到 Workbook 物件中。該物件允許您以程式設計方式操作檔案的資料和屬性。
```csharp
//載入範例來源文件
Workbook wb = new Workbook(sourceDir + "sampleForScalableColumns.xlsx");
```
在此程式碼中，我們建立一個新的`Workbook`例如，傳入 Excel 檔案的路徑。如果該文件不存在，您將收到錯誤訊息。
## 步驟 3：指定 HTML 儲存選項
選擇保存修改後的工作簿的方式至關重要。在本範例中，我們選擇將其儲存為 HTML 文件，但您也可以根據需要將其儲存為 Excel 格式。
```csharp
//指定 Html 儲存選項
HtmlSaveOptions options = new HtmlSaveOptions();
```
在這裡，我們實例化一個新的`HtmlSaveOptions`將用於設定檔案的保存特性的物件。
## 步驟 4：設定可縮放寬度的屬性
這是我們任務的核心。透過此步驟，您將允許 HTML 輸出中的列具有可縮放的寬度：
```csharp
//設定可縮放寬度的屬性
options.WidthScalable = true;
```
透過設定`WidthScalable`到`true`，您可以確保列寬動態調整，使您的 HTML 輸出在不同的裝置和螢幕尺寸上看起來不錯。
## 步驟5：指定影像儲存格式 
在此步驟中，您將決定在轉換文件時如何處理影像。具體做法如下：
```csharp
//指定影像保存格式
options.ExportImagesAsBase64 = true;
```
透過將圖像匯出為 Base64，您可以將它們直接嵌入到 HTML 中，如果您想要一個沒有單獨圖像文件的獨立 HTML 文件，這會很有幫助。
## 第 6 步：儲存工作簿 
最後，到了壓軸戲——保存修改後的工作簿。 
```csharp
//使用指定的 Html 儲存選項將工作簿儲存為 Html 格式
wb.Save(outputDir + "outsampleForScalableColumns.html", options);
```
這條線可以保存你的`Workbook`到之前使用定義的選項指定的輸出目錄。 
## 步驟7：確認訊息
為了整齊地總結一切，讓我們列印一條成功訊息：
```csharp
Console.WriteLine("SetScalableColumnWidth executed successfully.\r\n");
```
這條簡單的線確保您知道該過程已完成。
## 結論
就這樣吧！您剛剛使用 Aspose.Cells for .NET 以程式設計方式為 Excel 檔案設定了可縮放列寬。這可以顯著改善資料以 HTML 格式呈現的方式，尤其是跨不同裝置的可用性。無論您是經驗豐富的開發人員還是剛剛涉足編碼，Aspose.Cells 都提供了一個強大的工具集，可以簡化 Excel 文件操作。
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個用於在 .NET 應用程式中管理 Excel 檔案的綜合庫，可讓您建立、修改和轉換電子表格。
### 我可以免費使用 Aspose.Cells 嗎？
是的！ Aspose 提供免費試用；一探究竟[這裡](https://releases.aspose.com/).
### 在哪裡可以購買 Aspose.Cells 的許可證？
您可以直接從 Aspose 購買許可證[購買頁面](https://purchase.aspose.com/buy).
### 使用 Aspose.Cells 可以轉換為哪些檔案格式？
除了 HTML 之外，您還可以將 Excel 檔案轉換為 XLSX、CSV、PDF 等格式！
### 我如何獲得 Aspose.Cells 的支援？
您可以透過造訪 Aspose 獲得支持[論壇](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
