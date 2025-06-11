---
"description": "學習使用 Aspose.Cells for .NET 在 Excel 中插入 DataTable 行，而無需向下移動第一行。輕鬆實現自動化的分步指南。"
"linktitle": "在 Excel 中插入資料表行時將第一行向下移動"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 Excel 中插入資料表行時將第一行向下移動"
"url": "/zh-hant/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中插入資料表行時將第一行向下移動

## 介紹

在向 Excel 電子表格中插入新資料時，您是否厭倦了手動移動行？嗯，你很幸運！在本文中，我們將深入探討如何使用 Aspose.Cells for .NET 自動執行此程序。在本教程結束時，您不僅將學習如何使用 Excel 中的資料表，還將學習如何自訂匯入選項以更好地滿足您的需求。相信我；這可以為您節省大量時間和麻煩！那麼，喝杯咖啡，我們開始吧！

## 先決條件

在開始編碼之前，請確保已完成所有設定：

1. Visual Studio：確保您已安裝 Visual Studio（2017 或更高版本應該可以正常運作）。
2. Aspose.Cells for .NET：您需要有 Aspose.Cells 函式庫。如果你還沒有這樣做，你可以下載 [這裡](https://releases。aspose.com/cells/net/).
3. 對 C# 和 Excel 的基本了解：對 C# 程式設計和 Excel 工作原理的基本掌握肯定會幫助您更有效地跟進。

您還需要準備一個範例 Excel 檔案。在本指南中，我們將使用一個名為 `sampleImportTableOptionsShiftFirstRowDown.xlsx`。您可以建立此文件或找到適合您需求的範本。

## 導入包

在深入編碼之前，我們需要確保導入必要的套件。在您的 C# 專案中，包括以下命名空間：

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

這些包對於處理工作簿、工作表和表格至關重要。

## 步驟 1：設定您的項目

### 建立新的 C# 項目

首先在 Visual Studio 中建立一個新的 C# 控制台應用程式。給你的專案一個合適的名字，例如「ExcelDataImport」。

### 加入 Aspose.Cells NuGet 包

若要新增 Aspose.Cells 套件，請在解決方案資源管理器中以滑鼠右鍵按一下您的項目，選擇管理 NuGet 套件，然後搜尋「Aspose.Cells」。安裝該軟體包以確保您可以存取我們需要的所有功能。

## 第 2 步：定義資料表

接下來，我們將實現 `ICellsDataTable` 介面來建立一個提供要導入的資料的類別。以下是如何構建 `CellsDataTable` 班級：

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... 實現其他成員...
}
```

在這裡，我們定義列名和每列的數據，這將有助於我們匯入表的結構。

## 步驟3：實作ICellsDataTable介面成員

在 `CellsDataTable` 類，你需要實現 `ICellsDataTable` 介面.以下是所需的實作：

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

該類別的這一部分處理資料檢索，定義有多少行和多少列，以及管理目前索引狀態。

## 步驟4：編寫主函數

現在，讓我們創建 `Run` 方法來編排整個表格導入過程：

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## 步驟 5：設定導入選項

為了控制導入行為，您應該建立一個 `ImportTableOptions` 並相應地設定屬性。具體來說，我們想要設定 `ShiftFirstRowDown` 到 `false`。

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // 我們不想將第一行向下移動
```

## 步驟 6：匯入資料表

現在我們可以從我們的 `CellsDataTable` 到工作表中。

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

此命令將直接從指定的行和列開始插入資料表。

## 步驟 7：儲存工作簿

最後，我們將修改後的工作簿儲存回檔案：

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## 結論

就是這樣！您已經了解如何使用 Aspose.Cells for .NET 將 DataTable 行插入 Excel 工作表而不移動第一行。此過程不僅簡化了 Excel 內的資料操作，而且還透過自動執行通常繁瑣的任務來提高應用程式的效能。有了這些知識，您就可以更好地處理 Excel 自動化任務，從而節省您的時間和精力。

## 常見問題解答

### 什麼是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一個程式庫，可讓開發人員在 .NET 應用程式中建立、操作和轉換 Excel 檔案。

### 我需要許可證才能使用 Aspose.Cells 嗎？
是的，您需要有效的許可證才能使用全部功能。不過，可以免費試用進行初步測試。

### 我可以在 Web 應用程式中使用 Aspose.Cells 嗎？
絕對地！ Aspose.Cells 非常適合使用 .NET 開發的桌面、Web 和基於雲端的應用程式。

### 我可以使用 Aspose.Cells 建立哪些類型的 Excel 檔案？
您可以建立多種 Excel 檔案格式，包括 XLSX、XLS、CSV 等。

### 我可以在哪裡獲得 Aspose.Cells 的支援？
您可以在 [Aspose 論壇](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}