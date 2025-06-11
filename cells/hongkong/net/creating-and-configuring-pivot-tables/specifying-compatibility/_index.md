---
"description": "學習使用 Aspose.Cells for .NET 操作 Excel 資料透視表，包括資料更新、相容性設定和儲存格格式。"
"linktitle": "在 .NET 中以程式設計方式指定 Excel 檔案的兼容性"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 .NET 中以程式設計方式指定 Excel 檔案的兼容性"
"url": "/zh-hant/net/creating-and-configuring-pivot-tables/specifying-compatibility/"
"weight": 23
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以程式設計方式指定 Excel 檔案的兼容性

## 介紹

在當今數據驅動的世界中，以程式設計方式管理和操作 Excel 檔案對於許多開發人員來說已變得至關重要。如果您在 .NET 中使用 Excel，Aspose.Cells 是一個功能強大的程式庫，可讓您輕鬆建立、讀取、修改和儲存 Excel 檔案。該程式庫的一個重要功能可讓您以程式設計方式指定 Excel 檔案的兼容性。在本教程中，我們將探討如何操作 Excel 文件，特別是重點介紹如何使用 Aspose.Cells for .NET 管理相容性。最後，您將了解如何在刷新和管理資料時設定 Excel 檔案（尤其是資料透視表）的兼容性。

## 先決條件

在進入編碼階段之前，請確保您已具備以下條件：

1. C# 基礎知識：由於我們將使用 C# 編寫程式碼，因此熟悉語言將幫助您更好地理解本教學。
2. Aspose.Cells for .NET 函式庫：您可以從 [Aspose Cells 發佈頁面](https://releases.aspose.com/cells/net/)。如果您還沒有，請考慮先免費試用以了解其功能。
3. Visual Studio：一個可以有效地編寫和測試 C# 程式碼的 IDE。
4. 範例 Excel 文件：確保您有一個範例 Excel 文件，最好是包含用於演示的資料透視表的文件。對於我們的例子，我們將使用 `sample-pivot-table。xlsx`.

有了這些先決條件，我們就可以開始編碼過程了。

## 導入包

在開始編寫應用程式之前，您需要在程式碼中包含必要的命名空間，以有效地利用 Aspose.Cells 函式庫。以下是操作方法。

### 導入 Aspose.Cells 命名空間

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

這行程式碼確保您可以存取 Aspose.Cells 庫中的所有類別和方法。

現在，讓我們詳細分解這個過程以確保一切都清晰易懂。

## 步驟 1：設定目錄

首先，設定 Excel 檔案所在的目錄。提供正確的檔案路徑很重要。

```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory";
```

在這裡，替換 `"Your Document Directory"` 使用您的 Excel 檔案的實際路徑。這是您的範例資料透視表檔案應該駐留的位置。

## 步驟 2：載入來源 Excel 文件

接下來，我們需要載入包含範例資料透視表的 Excel 檔案。 

```csharp
// 載入包含範例資料透視表的來源 Excel 文件
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

在此步驟中，我們建立 `Workbook` 類，載入指定的Excel文件。 

## 步驟 3：存取工作表

現在工作簿已加載，您必須訪問包含資料透視表資料的工作表。

```csharp
// 存取包含資料透視表資料的第一個工作表
Worksheet dataSheet = wb.Worksheets[0];
```

在這裡，我們存取資料透視表所在的第一個工作表。您也可以根據 Excel 結構循環或指定其他工作表。

## 步驟 4：處理單元格數據

接下來，您將修改工作表中的某些儲存格值。 

### 步驟 4.1：修改儲存格 A3

讓我們先訪問單元格 A3 並設定其值。

```csharp
// 存取儲存格 A3 並設定其數據
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

此程式碼片段使用值“FooBar”更新儲存格 A3。

### 步驟 4.2：使用長字串修改儲存格 B3

現在，讓我們在儲存格 B3 中設定一個較長的字串，它超出了 Excel 的標準字元限制。

```csharp
// 存取儲存格 B3，設定其數據
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

此程式碼很重要，因為它設定了您對資料限制的期望，尤其是在使用 Excel 中的相容性設定時。

## 步驟 5：檢查儲存格 B3 的長度

確認我們輸入的字串的長度也很重要。

```csharp
// 列印儲存格B3字串的長度
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

這只是為了驗證您的儲存格中有多少個字元。

## 步驟 6：設定其他儲存格值

現在我們將訪問更多單元格並設定一些值。

```csharp
// 存取儲存格 C3 並設定其數據
cell = cells["C3"];
cell.PutValue("closed");

// 存取儲存格 D3 並設定其數據
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

每個程式碼片段都會更新工作表中的幾個附加儲存格。

## 步驟 7：存取資料透視表

接下來，您將存取第二張工作表，其中包含資料透視表資料。

```csharp
// 存取包含資料透視表的第二個工作表
Worksheet pivotSheet = wb.Worksheets[1];

// 存取資料透視表
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

此程式碼片段可讓您操作資料透視表以進行相容性設定。

## 步驟 8：設定 Excel 2003 相容性

設定資料透視表是否與 Excel 2003 相容至關重要。 

```csharp
// IsExcel2003Compatible 屬性指示在重新整理資料透視表時資料透視表是否與 Excel2003 相容
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

真正的轉變從這裡開始。透過設定 `IsExcel2003Compatible` 到 `true`，刷新時將字元長度限制為 255。

## 步驟9：相容性設定後檢查長度

設定完相容性之後我們來看看對資料有什麼影響。

```csharp
// 檢查資料透視表的儲存格 B5 的值。
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

如果初始資料超過 255 個字符，您可能會看到確認截斷效果的輸出。

## 步驟 10：更改相容性設置

現在，讓我們更改相容性設定並再次檢查。

```csharp
// 現在將 IsExcel2003Compatible 屬性設為 false 並再次刷新
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

這使得您的資料能夠反映其原始長度，而不受先前的限制。

## 步驟11：再次驗證長度 

讓我們驗證一下數據現在是否準確反映了其實際長度。

```csharp
// 現在它將列印單元格資料的原始長度。現在數據還沒有被截斷。
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

您應該會看到輸出確認已刪除截斷。

## 步驟 12：設定儲存格格式

為了增強視覺體驗，您可能需要設定儲存格的格式。 

```csharp
// 設定儲存格 B5 的行高和列寬，並設定其文字的換行
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

這些程式碼行透過調整儲存格尺寸和啟用文字換行使資料更易於閱讀。

## 步驟 13：儲存工作簿

最後，儲存包含所做變更的工作簿。

```csharp
// 將工作簿儲存為 xlsx 格式
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

儲存 Excel 檔案時，選擇合適的文件格式至關重要。這 `Xlsx` 格式應用廣泛，並且與許多 Excel 版本相容。

## 結論

恭喜！現在，您已經使用 Aspose.Cells for .NET 編寫了 Excel 檔案相容性設定。本教學概述了從設定環境到更改資料透視表的兼容性設定的每個步驟。如果您曾經處理過需要特定限製或相容性的數據，那麼這是一項您不想忽視的技能。

## 常見問題解答

### 什麼是 Aspose.Cells？  
Aspose.Cells 是一個 .NET 函式庫，旨在幫助開發人員無縫建立、操作和轉換 Excel 檔案。

### 為什麼 Excel 相容性很重要？  
Excel 相容性對於確保文件可以在目標版本的 Excel 中開啟和使用至關重要，特別是當文件包含早期版本不支援的功能或格式時。

### 我可以使用 Aspose.Cells 以程式設計方式建立資料透視表嗎？  
是的，您可以使用 Aspose.Cells 以程式設計方式建立和操作資料透視表。該程式庫提供了各種方法來新增與資料透視表相關的資料來源、欄位和功能。

### 如何檢查 Excel 儲存格中字串的長度？  
您可以使用 `StringValue` 的財產 `Cell` 物件來取得單元格的內容，然後調用 `.Length` 屬性來找出字串的長度。

### 除了行高和行寬之外，我還可以自訂儲存格格式嗎？  
絕對地！ Aspose.Cells 允許進行廣泛的單元格格式化。您可以透過 `Style` 班級。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}