---
"description": "了解如何使用 Aspose.Cells for .NET 設定 PDF 儲存選項的預設字體，確保您的文件每次都看起來完美無缺。"
"linktitle": "設定 PDF 儲存選項的預設字體"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "設定 PDF 儲存選項的預設字體"
"url": "/zh-hant/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 設定 PDF 儲存選項的預設字體

## 介紹
當產生 PDF 格式的報告、發票或任何其他文件時，確保內容看起來正確是至關重要的。字體在保持文件的視覺吸引力和可讀性方面起著至關重要的作用。但是，當您在 Excel 文件中使用的字體在您產生 PDF 的系統上不可用時會發生什麼？這就是 Aspose.Cells for .NET 派上用場的地方。這個強大的程式庫可讓您為 PDF 儲存選項設定預設字體，確保您的文件無論在哪裡開啟都看起來專業且一致。
## 先決條件
在開始之前，請確保您具備以下條件：
1. Visual Studio：您需要一個像 Visual Studio 這樣的開發環境來編寫和執行您的程式碼。
2. Aspose.Cells for .NET：您可以從以下位置下載最新版本 [此連結](https://releases.aspose.com/cells/net/)。或者，您可以透過 Visual Studio 中的 NuGet 套件管理器來安裝它。
3. C# 基礎知識：了解 C# 的基礎知識將幫助您理解程式碼範例。
4. 範例 Excel 檔案：準備一個範例 Excel 檔案以供測試。您可以建立一個具有各種字體和樣式的字體，以查看 Aspose.Cells 如何處理遺失的字體。
## 導入包
在您的專案中使用 Aspose.Cells 之前，您需要匯入必要的套件。具體操作如下：
1. 開啟您的專案：啟動 Visual Studio 並開啟您現有的專案或建立新專案。
2. 新增參考：在解決方案資源管理器中右鍵點擊您的專案並選擇「管理 NuGet 套件」。
3. 安裝 Aspose.Cells：搜尋「Aspose.Cells」並點選「安裝」按鈕。
4. 新增使用指令：在 C# 檔案的頂部，包含以下命名空間：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## 步驟 1：設定目錄
在處理檔案之前，定義來源目錄和輸出目錄非常重要。這將使您更容易找到輸入的 Excel 檔案並保存產生的輸出檔案。
```csharp
// 來源目錄
string sourceDir = "Your Document Directory";
// 輸出目錄
string outputDir = "Your Document Directory";
```
代替 `"Your Document Directory"` 使用目錄的實際路徑。
## 步驟 2： 開啟 Excel 文件
現在我們已經設定了目錄，讓我們打開要處理的 Excel 檔案。這 `Workbook` Aspose.Cells 中的類別用於載入 Excel 文件。
```csharp
// 開啟 Excel 文件
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
確保將檔案名稱替換為您的實際檔案名稱。
## 步驟 3：設定影像渲染選項
接下來，我們需要配置渲染選項，將 Excel 表轉換為影像格式。我們將建立一個實例 `ImageOrPrintOptions`，指定圖像類型和預設字體。
```csharp
// 渲染為 PNG 檔案格式
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
在此程式碼片段中，我們設定 `CheckWorkbookDefaultFont` 財產 `false`，這意味著如果缺少任何字體，則將使用指定的預設字體（“Times New Roman”）。
## 步驟 4：將工作表渲染為影像
現在，讓我們將工作簿的第一張表渲染為 PNG 映像。我們將使用 `SheetRender` 類別來實現這一點。
```csharp
// 將第一個工作表渲染為圖像
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## 步驟5：更改影像類型並渲染為TIFF
如果你想將同一張表渲染為不同的影像格式，例如 TIFF，你可以簡單地改變 `ImageType` 屬性並重複渲染過程。
```csharp
// 設定為TIFF格式
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## 步驟6：配置PDF儲存選項
接下來，讓我們設定 PDF 儲存選項。我們將建立一個實例 `PdfSaveOptions`，設定預設字體，並指定我們要檢查缺少的字體。
```csharp
// 配置 PDF 儲存選項
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## 步驟 7：將工作簿儲存為 PDF
配置儲存選項後，就可以將我們的 Excel 工作簿儲存為 PDF 檔案了。 
```csharp
// 將工作簿儲存為 PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## 步驟8：確認執行
最後，讓使用者知道該過程已成功完成是一種很好的做法。您可以透過使用簡單的控制台訊息來實現這一點。
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## 結論
Aspose.Cells 提供了一種靈活且強大的方式來處理 Excel 文件操作，使開發人員可以更輕鬆地建立具有視覺吸引力且保持其格式的文件。無論您處理的是報告、財務文件或任何其他形式的資料演示，控製字體渲染都可以顯著提高輸出品質。
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的 .NET 程式庫，可讓開發人員無需安裝 Microsoft Excel 即可操作 Excel 檔案。它支援各種文件格式並提供豐富的電子表格處理功能。
### 如何為我的 Excel 檔案設定預設字體？
您可以使用 `PdfSaveOptions` 類別並指定所需的字體名稱。這可確保即使缺少字體，您的文件也會使用您指定的預設字體。
### 我可以將 Excel 檔案轉換為 PDF 以外的格式嗎？
絕對地！ Aspose.Cells 可讓您將 Excel 檔案轉換為各種格式，包括映像（PNG、TIFF）、HTML、CSV 等。
### Aspose.Cells 可以免費使用嗎？
Aspose.Cells 是一款商業產品，但您可以免費試用有限的試用版。要獲得全部功能，您需要購買許可證。
### 在哪裡可以找到對 Aspose.Cells 的支援？
您可以透過造訪以下網站取得 Aspose.Cells 的支持 [Aspose 論壇](https://forum.aspose.com/c/cells/9)，您可以在其中提出問題並與其他用戶和開發人員分享見解。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}