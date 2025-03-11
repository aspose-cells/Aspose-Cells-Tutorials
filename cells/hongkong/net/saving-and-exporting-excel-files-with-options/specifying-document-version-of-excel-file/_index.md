---
title: 在 .NET 中以程式設計方式指定 Excel 檔案的文件版本
linktitle: 在 .NET 中以程式設計方式指定 Excel 檔案的文件版本
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 透過逐步說明以程式設計方式在 Excel 檔案中指定版本、作者和標題等文件屬性。
weight: 12
url: /zh-hant/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以程式設計方式指定 Excel 檔案的文件版本

## 介紹
Aspose.Cells for .NET 是一個功能強大的程式庫，可讓開發人員以程式設計方式輕鬆操作 Excel 檔案。無論您是想從頭開始建立 Excel 文件還是修改現有文件，Aspose.Cells 都可以提供全面的 API 來實現您的目標。其中一項功能是指定文件屬性，例如版本、作者或標題。本教學將引導您了解如何使用 Aspose.Cells for .NET 以程式設計方式指定 Excel 檔案的文件版本。
## 先決條件
在我們深入了解細節之前，讓我們確保您已掌握本教學所需的一切：
1. Aspose.Cells for .NET：您可以下載最新版本[這裡](https://releases.aspose.com/cells/net/)。如果您尚未購買許可證，您可以選擇[臨時執照](https://purchase.aspose.com/temporary-license/)探索功能。
2. .NET 開發環境：您可以使用 Visual Studio 或任何與 .NET 相容的 IDE。
3. C# 基礎知識：了解 C# 程式設計將使您更容易遵循。
## 導入包
在開始編碼之前，您需要從 Aspose.Cells 庫匯入必要的命名空間。這將使您能夠存取 Excel 文件操作所需的類別和方法。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
這兩個命名空間對於與工作簿及其內建文件屬性進行互動至關重要。
現在，讓我們分解一下在 Excel 文件中指定文件屬性（包括版本、標題和作者）的過程。
## 第 1 步：初始化工作簿對象
第一步是建立一個新的實例`Workbook`目的。該物件代表您將使用的整個 Excel 檔案。
```csharp
Workbook wb = new Workbook();
```
這`Workbook`類別提供 Excel 檔案的表示形式。透過實例化它，我們創建了一個可以操作的空白 Excel 工作簿。
## 第 2 步：存取內建文件屬性
Aspose.Cells 提供內建文件屬性，其中包括標題、作者和文件版本等欄位。您可以透過以下方式存取這些屬性`BuiltInDocumentProperties`收藏。
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
這`BuiltInDocumentPropertyCollection`類別提供對內建文件屬性集合的訪問，例如標題、作者以及通常與文件關聯的其他元資料。
## 步驟3：設定Excel文檔的標題
接下來，我們將設定 Excel 文件的標題。此元資料有助於稍後識別和管理文件。
```csharp
bdpc.Title = "Aspose File Format APIs";
```
設定標題對於文件組織很重要。這些元資料可以在文件屬性中看到，並且可以被外部系統用來更有效地編目或識別文件。
## 第 4 步：指定作者
也可以指定文件的作者以反映建立或修改該文件的人。
```csharp
bdpc.Author = "Aspose APIs Developers";
```
此步驟有助於將文件歸因於其創建者，為文件管理或協作場景提供附加元資料。
## 步驟 5：指定文件版本
我們在本教程中討論的最重要的屬性之一是文件版本。此步驟可讓您指定文件的版本，這在需要版本控制的環境中運作時非常有用。
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
設定文件版本可以清楚地了解用於建立文件的文件或庫的版本。這在需要追蹤文件修訂或與不同庫版本的兼容性的環境中尤其重要。
## 第 6 步：儲存 Excel 文件
最後，您可以使用剛剛設定的所有屬性來儲存 Excel 檔案。 Aspose.Cells 允許您以各種格式儲存文件，但對於本例，我們將堅持使用`.xlsx`格式。
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
這`Save`方法用於將檔案儲存到您指定的目錄。在這裡，我們將其儲存為 Excel 文件`.xlsx`格式。如果需要，Aspose.Cells 也支援以下格式`.xls`, `.csv` ， 和`.pdf`，根據您的專案需求提供靈活性。
## 結論
在本教學中，我們演練如何使用 Aspose.Cells for .NET 在 Excel 文件中指定文件屬性，特別是文件版本。 Aspose.Cells 是一個極其靈活且功能強大的工具，可讓您以程式設計方式操作 Excel 文件，這使其成為任何使用電子表格的 .NET 開發人員的寶貴資產。
## 常見問題解答
### 我可以使用 Aspose.Cells 修改其他內建屬性嗎？  
是的，您可以修改其他內建屬性，例如主題、關鍵字和評論等。
### Aspose.Cells 支援哪些檔案格式？  
 Aspose.Cells 支援多種格式，包括`.xls`, `.xlsx`, `.csv`, `.pdf`，等等。
### 我需要許可證才能使用 Aspose.Cells for .NET 嗎？  
您可以透過以下方式探索 Aspose.Cells[免費試用](https://releases.aspose.com/)或申請[臨時執照](https://purchase.aspose.com/temporary-license/)用於擴展測試。
### 我可以在 Web 應用程式中使用 Aspose.Cells 嗎？  
是的，Aspose.Cells 可以在桌面和 Web 應用程式中使用。它具有高度通用性，並且與 .NET Web 框架整合良好。
### 我可以在哪裡獲得 Aspose.Cells 的支援？  
您可以透過以下方式訪問社區和支持[Aspose.Cells 支援論壇](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
