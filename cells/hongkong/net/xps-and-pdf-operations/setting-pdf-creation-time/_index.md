---
title: 在 .NET 中設定 PDF 建立時間
linktitle: 在 .NET 中設定 PDF 建立時間
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells 在 .NET 中設定 PDF 建立時間。請按照我們的逐步指南進行 Excel 到 PDF 的無縫轉換。
weight: 11
url: /zh-hant/net/xps-and-pdf-operations/setting-pdf-creation-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中設定 PDF 建立時間

## 介紹
在當今的數位時代，將文件轉換為不同格式的能力對於許多應用程式至關重要。一個常見的需求是將 Excel 電子表格轉換為 PDF 檔案。這不僅保留了格式，而且還使共享和列印變得更加容易。如果您是使用 .NET 的開發人員，Aspose.Cells 是一個很棒的程式庫，可以簡化此流程。在本教學中，我們將深入探討如何使用 Aspose.Cells for .NET 將 Excel 檔案轉換為 PDF 時設定 PDF 建立時間。
## 先決條件
在我們深入了解程式碼的細節之前，讓我們確保您擁有開始使用所需的一切。
### 你需要什麼
1. Visual Studio：確保您的電腦上安裝了 Visual Studio。這將是您的開發環境。
2. Aspose.Cells for .NET：從下列位置下載 Aspose.Cells 函式庫：[網站](https://releases.aspose.com/cells/net/)。您也可以從免費試用開始測試其功能。
3. C# 基礎知識：熟悉 C# 程式設計將有助於您更好地理解程式碼片段。
4.  Excel 檔案：準備好轉換的 Excel 檔案。對於本例，我們將使用一個名為`Book1.xlsx`.
現在您已經滿足了先決條件，讓我們進入有趣的部分 - 匯入必要的套件並編寫程式碼！
## 導入包
首先，您需要在 C# 檔案中匯入所需的命名空間。這很重要，因為它允許您存取 Aspose.Cells 庫提供的類別和方法。
### 打開您的 C# 項目
開啟 Visual Studio，然後建立新專案或開啟要在其中實作 PDF 轉換功能的現有專案。
### 加入 Aspose.Cells 參考
您可以透過在解決方案資源管理器中右鍵點擊您的項目，選擇“管理 NuGet 套件”並搜尋“Aspose.Cells”，將 Aspose.Cells 庫新增到您的專案中。安裝軟體包。
### 導入命名空間
在 C# 檔案的頂部，包含以下命名空間：
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
這些命名空間將使您能夠存取 Workbook 類別和其他基本功能。

現在我們已經匯入了套件，讓我們分解一下將 Excel 檔案轉換為 PDF 並設定建立時間的過程。
## 第 1 步：定義文檔目錄
首先，您需要指定儲存文件的目錄。這是 Excel 檔案所在的位置以及輸出 PDF 的儲存位置。
```csharp
string dataDir = "Your Document Directory"; //指定您的文件目錄
```
代替`"Your Document Directory"`與您的實際路徑`Book1.xlsx`文件位於。該路徑將幫助應用程式找到要處理的文件。
## 第 2 步：載入 Excel 文件
接下來，您將把 Excel 文件載入到`Workbook`目的。這就是 Aspose.Cells 的閃光點，因為它可以讓您輕鬆處理 Excel 檔案。
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Excel 檔案的路徑
Workbook workbook = new Workbook(inputPath); //載入 Excel 文件
```
這`Workbook`類別用於載入和操作 Excel 檔案。透過傳遞輸入路徑，您可以告訴應用程式要使用哪個檔案。
## 第 3 步：建立 PdfSaveOptions
現在，是時候建立一個實例了`PdfSaveOptions`。此類別可讓您指定將工作簿儲存為 PDF 的各種選項，包括建立時間。
```csharp
PdfSaveOptions options = new PdfSaveOptions(); //建立 PdfSaveOptions 實例
options.CreatedTime = DateTime.Now; //將創建時間設定為現在
```
透過設定`options.CreatedTime`到`DateTime.Now`，您要確保 PDF 將反映創建時的當前日期和時間。
## 步驟 4：將工作簿另存為 PDF
最後，您將使用剛剛定義的選項將工作簿儲存為 PDF 檔案。
```csharp
workbook.Save(dataDir + "output.pdf", options); //另存為 PDF
```
此行程式碼會取得工作簿並將其以 PDF 格式儲存在指定位置。這`options`傳遞參數以將建立時間包含在 PDF 元資料中。

## 結論
現在你就擁有了！您已使用 Aspose.Cells for .NET 成功將 Excel 檔案轉換為 PDF，並附有建立時間戳記。當您需要追蹤文件版本或想要向收件人提供有關文件建立時間的資訊時，此功能非常有用。
如果您想探索 Aspose.Cells 的更多功能，請隨時查看[文件](https://reference.aspose.com/cells/net/).
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個強大的 .NET 程式庫，可讓開發人員建立、操作和轉換 Excel 檔案。
### 我可以免費使用 Aspose.Cells 嗎？
是的，您可以從以下網站上的免費試用開始[阿斯普斯網站](https://releases.aspose.com/).
### 如何設定其他 PDF 屬性？
您可以使用以下命令設定各種 PDF 屬性`PdfSaveOptions`類，例如頁面大小、壓縮等等。
### 是否可以同時轉換多個 Excel 檔案？
是的，您可以循環瀏覽文件列表並對每個文件應用相同的轉換過程。
### 我可以在哪裡獲得 Aspose.Cells 的支援？
您可以從 Aspose 社區獲得支持[支援論壇](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
