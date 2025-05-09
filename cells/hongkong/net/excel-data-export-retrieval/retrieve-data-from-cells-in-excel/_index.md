---
"description": "透過本逐步教學學習如何使用 Aspose.Cells for .NET 從 Excel 儲存格中擷取數據，非常適合初學者和經驗豐富的開發人員。"
"linktitle": "從 Excel 儲存格中擷取數據"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "從 Excel 儲存格中擷取數據"
"url": "/zh-hant/net/excel-data-export-retrieval/retrieve-data-from-cells-in-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 從 Excel 儲存格中擷取數據

## 介紹

在 Excel 中管理資料時，從單元格讀取和檢索資訊的能力至關重要。 Aspose.Cells for .NET 是一個功能強大的程式庫，可讓開發人員無縫地操作 Excel 檔案。在本教學中，我們將深入研究如何使用 Aspose.Cells 從 Excel 工作簿中的儲存格擷取資料。無論您是經驗豐富的開發人員還是剛起步，本指南都會逐步引導您完成整個過程。

## 先決條件

在我們進入程式碼之前，您需要滿足一些先決條件：

1. Visual Studio：確保您的機器上安裝了 Visual Studio。它是我們用來編寫和執行程式碼的 IDE。
2. Aspose.Cells for .NET：您需要有 Aspose.Cells 函式庫。您可以從 [Aspose 網站](https://releases。aspose.com/cells/net/).
3. C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解範例。
4. Excel 檔案：準備好一個 Excel 檔案（例如， `book1.xls`) 您將在本教程中使用它。

一旦滿足了這些先決條件，我們就可以開始探索如何從 Excel 儲存格中擷取資料。

## 導入包

首先，您需要在 C# 專案中匯入必要的命名空間。這將允許您使用 Aspose.Cells 提供的類別和方法。

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

匯入這些命名空間後，您就可以開始編碼了。讓我們將這個過程分解為易於管理的步驟。

## 步驟 1：設定文檔目錄

第一步是定義 Excel 檔案所在的文件目錄的路徑。這很關鍵，因為它告訴應用程式在哪裡可以找到您想要使用的檔案。


```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory";
```

代替 `"Your Document Directory"` 實際路徑 `book1.xls` 文件已儲存。當您嘗試開啟檔案時，Aspose.Cells 將在此路徑中尋找該檔案。

## 步驟 2：開啟現有工作簿

現在您已經設定了文件目錄，下一步是開啟您想要使用的工作簿（Excel 檔案）。


```csharp
// 開啟現有工作簿
Workbook workbook = new Workbook(dataDir + "book1.xls");
```

在這裡，我們創建一個 `Workbook` 透過傳遞 Excel 檔案的完整路徑來取得物件。此步驟初始化工作簿並使其準備好進行資料檢索。

## 步驟 3：存取第一個工作表

開啟工作簿後，您將需要存取要從中擷取資料的特定工作表。在這種情況下，我們將存取第一個工作表。


```csharp
// 訪問第一個工作表
Worksheet worksheet = workbook.Worksheets[0];
```

這 `Worksheets` 集合可讓您存取工作簿中的不同工作表。索引 `[0]` 指的是第一個工作表。如果您想存取後續工作表，您可以相應地更改索引。

## 步驟 4：循環遍歷單元格

現在您有了工作表，是時候循環遍歷每個單元格來檢索資料了。這就是奇蹟發生的地方！


```csharp
foreach (Cell cell1 in worksheet.Cells)
{
    // 用於儲存不同資料類型值的變數
    string stringValue;
    double doubleValue;
    bool boolValue;
    DateTime dateTimeValue;

    // 傳遞儲存格中包含的資料類型以供評估
    switch (cell1.Type)
    {
        // 評估單元格資料的字串值類型
        case CellValueType.IsString:
            stringValue = cell1.StringValue;
            Console.WriteLine("String Value: " + stringValue);
            break;

        // 評估單元格資料的雙精度資料類型
        case CellValueType.IsNumeric:
            doubleValue = cell1.DoubleValue;
            Console.WriteLine("Double Value: " + doubleValue);
            break;

        // 評估單元格資料的布林值類型
        case CellValueType.IsBool:
            boolValue = cell1.BoolValue;
            Console.WriteLine("Bool Value: " + boolValue);
            break;

        // 評估單元格資料的日期/時間值資料類型
        case CellValueType.IsDateTime:
            dateTimeValue = cell1.DateTimeValue;
            Console.WriteLine("DateTime Value: " + dateTimeValue);
            break;

        // 評估單元格資料的未知資料類型
        case CellValueType.IsUnknown:
            stringValue = cell1.StringValue;
            Console.WriteLine("Unknown Value: " + stringValue);
            break;

        // 終止單元格資料類型為空的類型檢查
        case CellValueType.IsNull:
            break;
    }
}
```

在此步驟中，我們循環遍歷工作表中的每個儲存格。對於每個單元格，我們使用 `switch` 陳述。根據類型，我們檢索值並將其列印到控制台。以下是案件的詳細情況：

- IsString：如果單元格包含字串，我們使用 `StringValue`。
- IsNumeric：對於數值，我們使用 `DoubleValue`。
- IsBool：如果儲存格包含布林值，我們可以使用 `BoolValue`。
- IsDateTime：對於日期和時間值，我們使用 `DateTimeValue`。
- IsUnknown：如果資料類型未知，我們仍然會擷取字串表示形式。
- IsNull：如果單元格為空，我們就跳過它。

## 結論

使用 Aspose.Cells for .NET 從 Excel 儲存格檢索資料是一個簡單的過程。透過遵循這些步驟，您可以有效地從 Excel 檔案中提取各種資料類型。無論您是建立報告工具、自動化數據輸入，還是只需要分析數據，Aspose.Cells 都能提供完成工作所需的靈活性和強大功能。

## 常見問題解答

### 什麼是 Aspose.Cells？  
Aspose.Cells 是一個 .NET 函式庫，可讓開發人員建立、操作和轉換 Excel 文件，而無需安裝 Microsoft Excel。

### 我可以免費使用 Aspose.Cells 嗎？  
是的，Aspose.Cells 提供免費試用版，您可以用來測試其功能。你可以下載它 [這裡](https://releases。aspose.com/).

### 我可以從 Excel 儲存格中檢索哪些類型的資料？  
您可以檢索各種資料類型，包括字串、數字、布林值和日期/時間值。

### 如何獲得 Aspose.Cells 的支援？  
您可以透過訪問 [Aspose 論壇](https://forum.aspose.com/c/cells/9) 您可以在這裡提出問題並獲得社區的幫助。

### 有臨時執照嗎？  
是的，Aspose 提供臨時許可證以供評估。您可以找到更多信息 [這裡](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}