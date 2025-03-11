---
title: 從 Excel 儲存格中擷取數據
linktitle: 從 Excel 儲存格中擷取數據
second_title: Aspose.Cells .NET Excel 處理 API
description: 在此逐步教程中，了解如何使用 Aspose.Cells for .NET 從 Excel 單元格檢索數據，非常適合初學者和經驗豐富的開發人員。
weight: 10
url: /zh-hant/net/excel-data-export-retrieval/retrieve-data-from-cells-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 Excel 儲存格中擷取數據

## 介紹

當涉及在 Excel 中管理資料時，從單元格中讀取和檢索資訊的能力至關重要。 Aspose.Cells for .NET 是一個功能強大的程式庫，可讓開發人員無縫地操作 Excel 檔案。在本教學中，我們將深入研究如何使用 Aspose.Cells 從 Excel 工作簿中的儲存格擷取資料。無論您是經驗豐富的開發人員還是剛入門，本指南都將逐步引導您完成整個過程。

## 先決條件

在我們開始編寫程式碼之前，您需要滿足一些先決條件：

1. Visual Studio：確保您的電腦上安裝了 Visual Studio。這是我們將用來編寫和執行程式碼的 IDE。
2.  Aspose.Cells for .NET：您需要擁有 Aspose.Cells 函式庫。您可以從[阿斯普斯網站](https://releases.aspose.com/cells/net/).
3. C#基礎知識：熟悉C#程式設計將有助於您更好地理解範例。
4. Excel 檔案：準備一個 Excel 檔案（例如，`book1.xls`）您將在本教程中使用它。

一旦滿足了這些先決條件，我們就可以開始探索如何從 Excel 儲存格中擷取資料。

## 導入包

首先，您需要在 C# 專案中匯入必要的命名空間。這將允許您利用 Aspose.Cells 提供的類別和方法。

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

匯入這些命名空間後，您就可以開始編碼了。讓我們將這個過程分解為可管理的步驟。

## 第 1 步：設定您的文件目錄

第一步是定義 Excel 檔案所在文件目錄的路徑。這很重要，因為它告訴應用程式在哪裡可以找到您想要使用的檔案。


```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
```

代替`"Your Document Directory"`與您的實際路徑`book1.xls`文件已儲存。當您嘗試開啟檔案時，Aspose.Cells 將在該路徑中尋找該檔案。

## 第 2 步：開啟現有工作簿

現在您已經設定了文件目錄，下一步是開啟您要使用的工作簿（Excel 檔案）。


```csharp
//開啟現有工作簿
Workbook workbook = new Workbook(dataDir + "book1.xls");
```

在這裡，我們創建一個`Workbook`透過傳遞 Excel 檔案的完整路徑來取得物件。此步驟將初始化工作簿並使其做好資料檢索的準備。

## 第 3 步：存取第一個工作表

開啟工作簿後，您將需要存取要從中擷取資料的特定工作表。在本例中，我們將存取第一個工作表。


```csharp
//訪問第一個工作表
Worksheet worksheet = workbook.Worksheets[0];
```

這`Worksheets`集合可讓您存取工作簿中的不同工作表。指數`[0]`指第一個工作表。如果要存取後續工作表，可以相應地變更索引。

## 第 4 步：循環單元格

現在您已經有了工作表，是時候循環遍歷每個單元格來檢索資料了。這就是魔法發生的地方！


```csharp
foreach (Cell cell1 in worksheet.Cells)
{
    //用於儲存不同資料類型的值的變數
    string stringValue;
    double doubleValue;
    bool boolValue;
    DateTime dateTimeValue;

    //傳遞儲存格中包含的資料類型進行評估
    switch (cell1.Type)
    {
        //評估字串值的單元格資料的資料類型
        case CellValueType.IsString:
            stringValue = cell1.StringValue;
            Console.WriteLine("String Value: " + stringValue);
            break;

        //評估雙值單元格資料的資料類型
        case CellValueType.IsNumeric:
            doubleValue = cell1.DoubleValue;
            Console.WriteLine("Double Value: " + doubleValue);
            break;

        //評估單元格資料的資料類型以獲得布林值
        case CellValueType.IsBool:
            boolValue = cell1.BoolValue;
            Console.WriteLine("Bool Value: " + boolValue);
            break;

        //評估日期/時間值的儲存格資料的資料類型
        case CellValueType.IsDateTime:
            dateTimeValue = cell1.DateTimeValue;
            Console.WriteLine("DateTime Value: " + dateTimeValue);
            break;

        //評估單元格資料的未知資料類型
        case CellValueType.IsUnknown:
            stringValue = cell1.StringValue;
            Console.WriteLine("Unknown Value: " + stringValue);
            break;

        //終止單元格資料類型為null的類型檢查
        case CellValueType.IsNull:
            break;
    }
}
```

在此步驟中，我們循環遍歷工作表中的每個儲存格。對於每個單元格，我們使用`switch`陳述。根據類型，我們檢索值並將其列印到控制台。以下是案件的詳細情況：

-  IsString：如果單元格包含字串，我們使用以下方法檢索它`StringValue`.
- IsNumeric：對於數值，我們使用`DoubleValue`.
- IsBool：如果儲存格包含布林值，我們可以使用`BoolValue`.
- IsDateTime：對於日期和時間值，我們使用`DateTimeValue`.
- IsUnknown：如果資料類型未知，我們仍然會擷取字串表示形式。
- IsNull：如果單元格為空，我們只需跳過它。

## 結論

使用 Aspose.Cells for .NET 從 Excel 儲存格檢索資料是一個簡單的過程。透過執行以下步驟，您可以有效地從 Excel 檔案中提取各種資料類型。無論您是建立報告工具、自動化數據輸入，還是只需要分析數據，Aspose.Cells 都能提供完成工作所需的靈活性和強大功能。

## 常見問題解答

### 什麼是 Aspose.Cells？  
Aspose.Cells 是一個 .NET 函式庫，可讓開發人員建立、操作和轉換 Excel 文件，而無需安裝 Microsoft Excel。

### 我可以免費使用 Aspose.Cells 嗎？  
是的，Aspose.Cells 提供免費試用版，您可以用它來測試其功能。你可以下載它[這裡](https://releases.aspose.com/).

### 我可以從 Excel 儲存格檢索哪些類型的資料？  
您可以檢索各種資料類型，包括字串、數字、布林值和日期/時間值。

### 我如何獲得 Aspose.Cells 的支援？  
您可以透過訪問獲得支持[Aspose論壇](https://forum.aspose.com/c/cells/9)您可以在其中提出問題並從社區獲得幫助。

### 有臨時許可證嗎？  
是的，Aspose 提供用於評估目的的臨時許可證。您可以找到更多信息[這裡](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
