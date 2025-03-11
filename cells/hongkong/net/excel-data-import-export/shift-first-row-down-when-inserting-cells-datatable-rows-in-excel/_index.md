---
title: 在 Excel 中插入資料表行時將第一行向下移動
linktitle: 在 Excel 中插入資料表行時將第一行向下移動
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解使用 Aspose.Cells for .NET 在 Excel 中插入 DataTable 行而不將第一行向下移動。輕鬆實現自動化的分步指南。
weight: 11
url: /zh-hant/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中插入資料表行時將第一行向下移動

## 介紹

您是否厭倦了在 Excel 電子表格中插入新資料時手動移動行？嗯，你很幸運！在本文中，我們將深入探討如何使用 Aspose.Cells for .NET 自動化此流程。在本教程結束時，您不僅將學習如何在 Excel 中使用資料表，還將了解如何自訂匯入選項以更好地滿足您的需求。相信我；這可以為您節省大量時間和麻煩！那麼，喝杯咖啡，讓我們開始吧！

## 先決條件

在我們開始編碼之前，讓我們確保您已完成所有設定：

1. Visual Studio：確保安裝了 Visual Studio（2017 或更高版本應該可以正常運作）。
2.  Aspose.Cells for .NET：您需要擁有 Aspose.Cells 函式庫。如果您還沒有這樣做，您可以下載它[這裡](https://releases.aspose.com/cells/net/).
3. 對 C# 和 Excel 的基本了解：對 C# 程式設計和 Excel 工作原理的基本掌握肯定會幫助您更有效地進行操作。

您還需要手邊有一個範例 Excel 檔案。在本指南中，我們將使用一個名為`sampleImportTableOptionsShiftFirstRowDown.xlsx`。您可以建立此文件或尋找適合您需求的範本。

## 導入包

在我們深入編碼之前，我們需要確保導入必要的套件。在您的 C# 專案中，包含以下命名空間：

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

這些套件對於使用工作簿、工作表和表格至關重要。

## 第 1 步：設定您的項目

### 建立一個新的 C# 項目

首先在 Visual Studio 中建立一個新的 C# 控制台應用程式。為您的專案指定一個適當的名稱，例如「ExcelDataImport」。

### 加入 Aspose.Cells NuGet 包

若要新增 Aspose.Cells 套件，請在解決方案資源管理器中以滑鼠右鍵按一下您的項目，選擇管理 NuGet 套件，然後搜尋「Aspose.Cells」。安裝該軟體包以確保您可以存取我們需要的所有功能。

## 步驟 2：定義資料表

接下來，我們將實現`ICellsDataTable`介面來建立一個提供要導入的資料的類別。以下是您可以如何構建`CellsDataTable`班級：

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
    
    // ...實施其他成員...
}
```

在這裡，我們定義列名和每列的數據，這將有助於我們匯入表的結構。

## 步驟 3：實作 ICellsDataTable 介面成員

內`CellsDataTable`類，你需要實現的成員`ICellsDataTable`介面.這是所需的實作：

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

類別的這一部分處理資料檢索，定義有多少行和列，並管理目前索引狀態。

## 第四步：編寫主函數

現在，讓我們創建`Run`編排整個表格匯入過程的方法：

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## 第 5 步：設定導入選項

若要控制匯入行為，您應該建立一個實例`ImportTableOptions`並相應地設定屬性。具體來說，我們要設定`ShiftFirstRowDown`到`false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; //我們不想將第一行向下移動
```

## 第6步：匯入資料表

現在我們可以從我們的資料導入`CellsDataTable`到工作表中。

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

該命令將直接從指定的行和列開始插入資料表。

## 第 7 步：儲存工作簿

最後，我們將修改後的工作簿儲存回文件中：

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## 結論

現在你就擁有了！您已經了解如何使用 Aspose.Cells for .NET 將 DataTable 行插入到 Excel 工作表中，而無需移動第一行。此過程不僅簡化了 Excel 中的資料操作，而且還透過自動執行通常繁瑣的任務來增強應用程式的效能。有了工具包中的這些知識，您就可以更好地處理 Excel 自動化任務，從而節省時間和精力。

## 常見問題解答

### 什麼是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一個程式庫，可讓開發人員在 .NET 應用程式中建立、操作和轉換 Excel 檔案。

### 我需要許可證才能使用 Aspose.Cells 嗎？
是的，您需要有效的許可證才能使用全部功能。但是，可以免費試用以進行初始測試。

### 我可以在 Web 應用程式中使用 Aspose.Cells 嗎？
絕對地！ Aspose.Cells 非常適合在 .NET 中開發的桌面、Web 和基於雲端的應用程式。

### 我可以使用 Aspose.Cells 建立哪些類型的 Excel 檔案？
您可以建立多種 Excel 檔案格式，包括 XLSX、XLS、CSV 等。

### 我可以在哪裡獲得 Aspose.Cells 的支援？
您可以在以下位置提問或尋求協助[Aspose 論壇](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
