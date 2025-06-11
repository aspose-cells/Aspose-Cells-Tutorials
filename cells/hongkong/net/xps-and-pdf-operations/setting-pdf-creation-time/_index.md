---
"description": "了解如何使用 Aspose.Cells 在 .NET 中設定 PDF 建立時間。按照我們的逐步指南，實現 Excel 到 PDF 的無縫轉換。"
"linktitle": "在 .NET 中設定 PDF 建立時間"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 .NET 中設定 PDF 建立時間"
"url": "/zh-hant/net/xps-and-pdf-operations/setting-pdf-creation-time/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中設定 PDF 建立時間

## 介紹
在當今數位時代，將文件轉換為不同格式的能力對於許多應用程式來說至關重要。一個常見的需求是將 Excel 電子表格轉換為 PDF 檔案。這不僅可以保留格式，而且還可以使得共享和列印變得更加容易。如果您是使用 .NET 的開發人員，Aspose.Cells 是一個可以簡化此過程的出色程式庫。在本教學中，我們將深入研究如何在使用 Aspose.Cells for .NET 將 Excel 檔案轉換為 PDF 時設定 PDF 建立時間。
## 先決條件
在我們深入研究程式碼細節之前，讓我們確保您擁有開始所需的一切。
### 你需要什麼
1. Visual Studio：確保您的機器上安裝了 Visual Studio。這將是您的開發環境。
2. Aspose.Cells for .NET：從下載 Aspose.Cells 庫 [網站](https://releases.aspose.com/cells/net/)。您也可以從免費試用開始測試其功能。
3. C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解程式碼片段。
4. Excel 檔案：準備好要轉換的 Excel 檔案。對於此範例，我們將使用名為 `Book1。xlsx`.
現在您已經滿足了先決條件，讓我們進入有趣的部分 - 匯入必要的套件並編寫程式碼！
## 導入包
首先，您需要在 C# 檔案中匯入所需的命名空間。這至關重要，因為它允許您存取 Aspose.Cells 庫提供的類別和方法。
### 打開你的 C# 項目
開啟 Visual Studio 並建立一個新專案或開啟一個現有項目，在其中實作 PDF 轉換功能。
### 新增 Aspose.Cells 引用
您可以透過在解決方案資源管理器中右鍵單擊您的項目，選擇“管理 NuGet 套件”，然後搜尋“Aspose.Cells”來將 Aspose.Cells 庫新增到您的專案中。安裝該包。
### 導入命名空間
在 C# 檔案的頂部，包含以下命名空間：
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
這些命名空間將允許您存取 Workbook 類別和其他基本功能。

現在我們已經導入了包，讓我們在設定創建時間的同時分解將 Excel 文件轉換為 PDF 的過程。
## 步驟1：定義文檔目錄
首先，您需要指定儲存文件的目錄。這是您的 Excel 檔案所在的位置，也是輸出 PDF 的儲存位置。
```csharp
string dataDir = "Your Document Directory"; // 指定您的文件目錄
```
代替 `"Your Document Directory"` 實際路徑 `Book1.xlsx` 文件所在位置。此路徑將幫助應用程式定位要處理的檔案。
## 步驟2：載入Excel文件
接下來，將 Excel 文件載入到 `Workbook` 目的。這就是 Aspose.Cells 的優勢所在，因為它可以讓您毫不費力地處理 Excel 檔案。
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Excel 檔案的路徑
Workbook workbook = new Workbook(inputPath); // 載入 Excel 文件
```
這 `Workbook` 類別用於載入和操作 Excel 檔案。透過傳遞輸入路徑，您可以告訴應用程式要處理哪個檔案。
## 步驟 3：建立 PdfSaveOptions
現在，是時候建立一個實例了 `PdfSaveOptions`。此類別可讓您指定將工作簿儲存為 PDF 的各種選項，包括建立時間。
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // 建立 PdfSaveOptions 實例
options.CreatedTime = DateTime.Now; // 將創建時間設定為現在
```
透過設定 `options.CreatedTime` 到 `DateTime.Now`，您要確保 PDF 將反映其建立的當前日期和時間。
## 步驟 4：將工作簿儲存為 PDF
最後，您將使用剛剛定義的選項將工作簿儲存為 PDF 檔案。
```csharp
workbook.Save(dataDir + "output.pdf", options); // 另存為 PDF
```
這行程式碼會取得工作簿並以 PDF 格式儲存在指定位置。這 `options` 傳遞參數以將建立時間包含在 PDF 元資料中。

## 結論
就是這樣！您已成功使用 Aspose.Cells for .NET 將 Excel 檔案轉換為 PDF，並附有建立時間戳記。當您需要追蹤文件版本或想要向收件人提供有關文件建立時間的資訊時，此功能非常有用。
如果您想了解 Aspose.Cells 的更多功能，請隨時查看 [文件](https://reference。aspose.com/cells/net/).
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個強大的 .NET 程式庫，可讓開發人員建立、操作和轉換 Excel 檔案。
### 我可以免費使用 Aspose.Cells 嗎？
是的，你可以先免費試用一下 [Aspose 網站](https://releases。aspose.com/).
### 如何設定其他 PDF 屬性？
您可以使用 `PdfSaveOptions` 類，例如頁面大小、壓縮等等。
### 是否可以一次轉換多個 Excel 檔案？
是的，您可以循環遍歷文件列表並對每個文件應用相同的轉換過程。
### 我可以在哪裡獲得 Aspose.Cells 的支援？
您可以從 Aspose 社區獲得支持 [支援論壇](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}