---
title: 將儲存格的 HTML 字串值匯出到 Excel 中的資料表
linktitle: 將儲存格的 HTML 字串值匯出到 Excel 中的資料表
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過簡單的逐步教學，了解如何使用 Aspose.Cells for .NET 將 HTML 字串值從 Excel 儲存格匯出到 DataTable。
weight: 11
url: /zh-hant/net/excel-data-sorting-exporting/export-html-string-value-of-cells-to-datatable-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將儲存格的 HTML 字串值匯出到 Excel 中的資料表

## 介紹

在 .NET 環境中使用 Excel 文件時，您可能會發現自己需要從單元格中提取信息，不僅是純文本，而且是 HTML 字串。當您處理富文本資料或想要保持格式時，這會非常方便。在本指南中，我將引導您使用 Aspose.Cells for .NET 將單元格的 HTML 字串值匯出到 DataTable。 

## 先決條件

在深入研究程式碼之前，讓我們確保您已準備好所需的一切。這是一個快速清單：

1. C# 和 .NET 的基本知識：在開始程式設計之前，請確保您熟悉 C# 程式設計和 .NET 框架的基礎知識。
2.  Aspose.Cells for .NET：如果您尚未安裝，則需要安裝 Aspose.Cells for .NET。您可以從以下位置下載免費試用版[這裡](https://releases.aspose.com/).
3. 您選擇的 Visual Studio 或 IDE：設定您的環境來編寫 C# 程式碼。 Visual Studio 因其廣泛的功能和易用性而受到推薦。
4. 範例 Excel 檔案：您將需要一個範例 Excel 檔案（`sampleExportTableAsHtmlString.xlsx`）一起工作。確保它位於可訪問的目錄中。
5. NuGet 套件管理器：確保您可以存取專案中的 NuGet 套件管理器，以輕鬆新增 Aspose.Cells 庫。

檢查完這些先決條件後，讓我們開始寫一些程式碼吧！

## 導入包

在開始使用 Aspose.Cells 之前，我們需要導入必要的套件。這通常涉及將 Aspose.Cells NuGet 套件添加到您的專案中。操作方法如下：

### 開啟 NuGet 套件管理器

在 Visual Studio 中，在解決方案資源管理器中以滑鼠右鍵按一下您的項目，然後選擇「管理 NuGet 套件」。

### 搜尋 Aspose.Cells

在 NuGet 套件管理員中，鍵入`Aspose.Cells`在搜尋欄中。

### 安裝包

找到 Aspose.Cells 後，按一下「安裝」按鈕。這會將庫添加到您的專案中，並允許您將其匯入到程式碼中。

### 導入命名空間

在程式碼檔案頂部新增以下 using 指令：

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Data;
```

現在我們已經完成所有設置，讓我們深入了解將 HTML 字串值從 Excel 文件匯出到 DataTable 的逐步過程。 

## 第 1 步：定義來源目錄

首先，您將定義儲存範例 Excel 檔案的目錄。這很重要，因為它告訴您的應用程式在哪裡可以找到該檔案。這是代碼：

```csharp
string sourceDir = "Your Document Directory";
```

確保更換`"Your Document Directory"`與 Excel 檔案的實際路徑。

## 第 2 步：載入範例 Excel 文件

下一步是載入 Excel 工作簿。您將使用`Workbook`Aspose.Cells 中的類別來執行此操作。以下是載入檔案的方法：

```csharp
Workbook wb = new Workbook(sourceDir + "sampleExportTableAsHtmlString.xlsx");
```

這行簡單的程式碼將初始化工作簿並載入指定的 Excel 檔案。

## 第 3 步：存取第一個工作表

載入工作簿後，您將需要存取包含您感興趣的資料的特定工作表。

```csharp
Worksheet ws = wb.Worksheets[0];
```

在這裡，我們正在處理第一個工作表（索引 0）。確保您的資料位於正確的表格上。

## 步驟 4：指定匯出表選項

要控制資料匯出的方式，您需要設定`ExportTableOptions`。在這種情況下，您需要確保不匯出列名稱，並且希望將單元格資料匯出為 HTML 字串：

```csharp
ExportTableOptions opts = new ExportTableOptions();
opts.ExportColumnName = false;
opts.ExportAsHtmlString = true;
```

此配置可讓您在匯出時保持儲存格資料的豐富格式。

## 步驟5：將儲存格匯出到資料表

現在是實際導出資料的關鍵部分。使用`ExportDataTable`方法，您可以將工作表中的資料提取到`DataTable`。具體做法如下：

```csharp
DataTable dt = ws.Cells.ExportDataTable(0, 0, 3, 3, opts);
```

此程式碼使用前面指定的選項將指定的儲存格範圍（從第 0 行第 0 列到第 3 行第 3 列）匯出到 DataTable 中。

## 第 6 步：列印 HTML 字串值

最後，讓我們從 DataTable 中的特定單元格列印出 HTML 字串值，以查看我們已成功匯出的內容。例如，如果您想要列印第三行第二列的值，您將執行以下操作：

```csharp
Console.WriteLine(dt.Rows[2][1].ToString());
```

此行將所需的 HTML 字串從 DataTable 列印到控制台中。 

## 結論 

現在你就擁有了！您已使用 Aspose.Cells for .NET 成功將 HTML 字串值從 Excel 檔案中的儲存格匯出到 DataTable。此功能不僅豐富了您的資料操作技能，而且還拓寬了您在直接處理 Excel 文件中的格式化內容時的選擇。 

## 常見問題解答

### 我可以將 Aspose.Cells 用於 Excel 以外的其他文件格式嗎？  
是的，Aspose.Cells 主要用於 Excel，但 Aspose 也提供了針對不同格式的其他函式庫。

### 我需要 Aspose.Cells 許可證嗎？  
是的，生產使用需要有效的許可證。您可以獲得臨時許可證[這裡](https://purchase.aspose.com/temporary-license/).

### 如果我的 Excel 檔案包含公式怎麼辦？他們會正確導出嗎？  
是的，Aspose.Cells 可以處理公式，並且在導出時，它們將被評估為結果值。

### 是否可以更改匯出選項？  
絕對地！您可以自訂`ExportTableOptions`以滿足您的特定需求。

### 在哪裡可以找到有關 Aspose.Cells 的更詳細文件？  
您可以找到大量文檔[這裡](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
