---
title: 管理工作表的紙張尺寸
linktitle: 管理工作表的紙張尺寸
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過這個簡單的逐步指南，了解如何使用 Aspose.Cells for .NET 在 Excel 中設定自訂紙張尺寸。
weight: 16
url: /zh-hant/net/worksheet-page-setup-features/manage-paper-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 管理工作表的紙張尺寸

## 介紹
管理 Excel 工作表中的紙張尺寸至關重要，尤其是當您需要將文件列印為特定尺寸或以通用格式佈局共用文件時。在本指南中，我們將引導您使用 Aspose.Cells for .NET 在 Excel 中輕鬆設定工作表的紙張大小。我們將涵蓋您所需的一切，從先決條件和導入包到以易於遵循的步驟對程式碼進行完整分解。
## 先決條件
在開始之前，需要準備一些東西：
-  Aspose.Cells for .NET Library：確保您已下載並安裝[Aspose.Cells for .NET](https://releases.aspose.com/cells/net/)。這是我們將用來以程式設計方式操作 Excel 檔案的核心庫。
- .NET 環境：您的電腦上應該安裝有 .NET。任何最新版本都應該可以工作。
- 編輯器或 IDE：用於編寫和執行程式碼的程式碼編輯器（例如 Visual Studio、Visual Studio Code 或 JetBrains Rider）。
- C# 的基本知識：雖然我們將逐步指導您，但熟悉 C# 會有所幫助。
## 導入包
讓我們先導入 Aspose.Cells 所需的套件。
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
此行導入基本的 Aspose.Cells 包，它提供了 Excel 文件操作所需的所有類別和方法。
現在，讓我們深入了解核心步驟！我們將仔細檢查每一行程式碼，解釋它的作用以及為什麼它很重要。
## 第 1 步：設定文檔目錄
首先，我們需要一個地方來儲存 Excel 檔案。設定目錄路徑可確保我們的檔案保存在定義的位置。
```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
```
代替`"Your Document Directory"`與您要儲存檔案的路徑。這可能是您電腦上的特定資料夾，例如`"C:\\Documents\\ExcelFiles\\"`.
## 第 2 步：初始化新工作簿
我們需要建立一個新的工作簿（Excel 檔案），我們將在其中套用紙張尺寸變更。
```csharp
//實例化 Workbook 物件
Workbook workbook = new Workbook();
```
這`Workbook`類別代表一個 Excel 文件。透過建立此類別的實例，我們實際上正在建立一個空白的 Excel 工作簿，我們可以根據需要對其進行操作。
## 第 3 步：存取第一個工作表
每個工作簿都包含多個工作表。在這裡，我們將訪問第一個工作表來應用我們的設定。
```csharp
//存取 Excel 文件中的第一個工作表
Worksheet worksheet = workbook.Worksheets[0];
```
這`Worksheets`集合包含工作簿中的所有工作表。透過使用`workbook.Worksheets[0]`，我們選擇第一張紙。您也可以修改此索引以選擇其他工作表。
## 步驟 4：將紙張尺寸設定為 A4
現在是我們任務的核心——將紙張尺寸設為 A4。
```csharp
//將紙張尺寸設定為 A4
worksheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
```
這`PageSetup`的財產`Worksheet`類別允許我們存取頁面佈局設定。`PaperSizeType.PaperA4`將頁面尺寸設定為 A4，這是全球通用的標準紙張尺寸之一。
想要使用其他紙張尺寸嗎？ Aspose.Cells 提供了各種選項，例如`PaperSizeType.PaperLetter`, `PaperSizeType.PaperLegal`，等等。只需更換`PaperA4`與您喜歡的尺寸！
## 第 5 步：儲存工作簿
最後，我們將儲存調整紙張尺寸的工作簿。
```csharp
//儲存工作簿。
workbook.Save(dataDir + "ManagePaperSize_out.xls");
```
這`Save`方法將工作簿儲存到您指定的路徑。檔案名稱`"ManagePaperSize_out.xls"`可以根據您的喜好進行客製化。在這裡，它保存為 Excel 文件`.xls`格式，但您可以將其儲存為`.xlsx`或其他支援的格式（透過更改檔案副檔名）。
## 結論
現在你就擁有了！透過執行這些簡單的步驟，您已使用 Aspose.Cells for .NET 將 Excel 工作表的紙張尺寸設為 A4。當您需要確保文件保持一致的紙張尺寸時，尤其是列印或分享時，這種方法非常有用。 
使用 Aspose.Cells，您不僅限於 A4 — 您可以從多種紙張尺寸中進行選擇，並進一步自訂頁面設置，使其成為自動化和自訂 Excel 文件的強大工具。
## 常見問題解答
### 我可以為每個工作表設定不同的紙張尺寸嗎？
是的，絕對！只需單獨訪問每個工作表並使用以下命令設定唯一的紙張尺寸`worksheet.PageSetup.PaperSize`.
### Aspose.Cells 與 .NET Core 相容嗎？
是的，Aspose.Cells 與 .NET Framework 和 .NET Core 相容，使其適用於不同的 .NET 專案。
### 如何將工作簿儲存為 PDF 格式？
只需更換`.Save(dataDir + "ManagePaperSize_out.xls")`和`.Save(dataDir + "ManagePaperSize_out.pdf", SaveFormat.Pdf)`，Aspose.Cells 會將其儲存為 PDF。
### 我可以使用 Aspose.Cells 自訂其他頁面設定嗎？
是的，Aspose.Cells 允許您透過以下方式調整許多設置，例如方向、縮放、邊距和頁首/頁腳`worksheet.PageSetup`.
### 如何獲得 Aspose.Cells 的免費試用版？
您可以從以下位置下載免費試用版[Aspose.Cells 下載頁面](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
