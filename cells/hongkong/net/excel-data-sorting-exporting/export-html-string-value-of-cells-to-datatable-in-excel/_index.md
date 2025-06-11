---
"description": "透過簡單的逐步教學來了解如何使用 Aspose.Cells for .NET 將 HTML 字串值從 Excel 儲存格匯出到 DataTable。"
"linktitle": "將儲存格的 HTML 字串值匯出到 Excel 中的資料表"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "將儲存格的 HTML 字串值匯出到 Excel 中的資料表"
"url": "/zh-hant/net/excel-data-sorting-exporting/export-html-string-value-of-cells-to-datatable-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 將儲存格的 HTML 字串值匯出到 Excel 中的資料表

## 介紹

在 .NET 環境中使用 Excel 文件時，您可能會發現自己需要從單元格中提取信息，不僅是純文本，而是 HTML 字串。當您處理富文本資料或想要維護格式時，這會非常方便。在本指南中，我將引導您使用 Aspose.Cells for .NET 將單元格的 HTML 字串值匯出到 DataTable。 

## 先決條件

在深入研究程式碼之前，請確保您已準備好所需的一切。以下是一份快速清單：

1. C# 和 .NET 的基礎知識：在開始程式設計之前，請確保您熟悉 C# 程式設計和 .NET 框架的基礎知識。
2. Aspose.Cells for .NET：如果您還沒有安裝，您需要安裝 Aspose.Cells for .NET。您可以從下載免費試用版 [這裡](https://releases。aspose.com/).
3. Visual Studio 或您選擇的 IDE：設定您的環境來編寫 C# 程式碼。推薦使用 Visual Studio，因為它功能廣泛且易於使用。
4. 範例 Excel 檔案：您需要一個範例 Excel 檔案 (`sampleExportTableAsHtmlString.xlsx`) 來合作。確保它位於可訪問的目錄中。
5. NuGet 套件管理器：確保您可以在專案中存取 NuGet 套件管理器，以便輕鬆新增 Aspose.Cells 庫。

滿足這些先決條件後，讓我們開始寫一些程式碼吧！

## 導入包

在我們開始使用 Aspose.Cells 之前，我們需要導入必要的套件。這通常涉及將 Aspose.Cells NuGet 套件添加到您的專案中。具體操作如下：

### 開啟 NuGet 套件管理器

在 Visual Studio 中，以滑鼠右鍵按一下解決方案資源管理器中的項目，然後選擇管理 NuGet 套件。

### 搜尋 Aspose.Cells

在 NuGet 套件管理器中，輸入 `Aspose.Cells` 在搜尋欄中。

### 安裝軟體包

找到 Aspose.Cells 後，按一下「安裝」按鈕。這會將庫添加到您的專案中並允許您將其導入到您的程式碼中。

### 導入命名空間

在程式碼檔案頂部新增以下使用指令：

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Data;
```

現在我們已經設定好了一切，讓我們深入了解將 HTML 字串值從 Excel 檔案匯出到 DataTable 的逐步流程。 

## 步驟 1：定義來源目錄

首先定義儲存範例 Excel 檔案的目錄。這很關鍵，因為它告訴您的應用程式在哪裡可以找到該檔案。下面是程式碼：

```csharp
string sourceDir = "Your Document Directory";
```

確保更換 `"Your Document Directory"` 使用您的 Excel 檔案的實際路徑。

## 步驟 2：載入範例 Excel 文件

下一步是載入 Excel 工作簿。您將使用 `Workbook` 來自 Aspose.Cells 的類別來執行此操作。載入檔案的方法如下：

```csharp
Workbook wb = new Workbook(sourceDir + "sampleExportTableAsHtmlString.xlsx");
```

這行簡單的程式碼初始化工作簿並載入指定的 Excel 檔案。

## 步驟 3：存取第一個工作表

工作簿載入完成後，您將需要存取包含您感興趣的資料的特定工作表。通常，您將從第一個工作表開始：

```csharp
Worksheet ws = wb.Worksheets[0];
```

這裡，我們正在處理第一個工作表（索引 0）。確保您的數據在正確的表格上。

## 步驟 4：指定匯出表選項

要控制資料的匯出方式，您需要設定 `ExportTableOptions`。在這種情況下，您要確保不匯出列名，並且希望將儲存格資料匯出為 HTML 字串：

```csharp
ExportTableOptions opts = new ExportTableOptions();
opts.ExportColumnName = false;
opts.ExportAsHtmlString = true;
```

此配置可讓您在匯出時保持儲存格資料的豐富格式。

## 步驟 5：將儲存格匯出到資料表

現在到了實際導出資料的關鍵部分。使用 `ExportDataTable` 方法，您可以將資料從工作表拉入 `DataTable`。具體操作如下：

```csharp
DataTable dt = ws.Cells.ExportDataTable(0, 0, 3, 3, opts);
```

此程式碼使用先前指定的選項將指定範圍的儲存格（從第 0 行、第 0 列到第 3 行、第 3 列）匯出到 DataTable 中。

## 步驟 6：列印 HTML 字串值

最後，讓我們從 DataTable 中的特定單元格列印出 HTML 字串值，以查看我們成功匯出的內容。例如，如果您想要列印第三行第二列的值，您可以執行以下操作：

```csharp
Console.WriteLine(dt.Rows[2][1].ToString());
```

此行將 DataTable 中所需的 HTML 字串列印到控制台。 

## 結論 

就是這樣！您已成功使用 Aspose.Cells for .NET 將 Excel 檔案儲存格中的 HTML 字串值匯出到 DataTable。此功能不僅豐富了您的資料處理技能，而且還拓寬了您直接從 Excel 檔案處理格式化內容時的選擇。 

## 常見問題解答

### 除了 Excel 之外，我可以將 Aspose.Cells 用於其他文件格式嗎？  
是的，Aspose.Cells 主要用於 Excel，但 Aspose 也為不同格式提供了其他函式庫。

### 我需要 Aspose.Cells 的許可證嗎？  
是的，生產使用需要有效的許可證。您可以獲得臨時駕照 [這裡](https://purchase。aspose.com/temporary-license/).

### 如果我的 Excel 檔案包含公式怎麼辦？它們能正確出口嗎？  
是的，Aspose.Cells 可以處理公式，並且在導出時，它們將被評估為結果值。

### 可以更改匯出選項嗎？  
絕對地！您可以自訂 `ExportTableOptions` 以滿足您的特定需求。

### 在哪裡可以找到有關 Aspose.Cells 的更詳細文件？  
您可以找到大量文檔 [這裡](https://reference。aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}