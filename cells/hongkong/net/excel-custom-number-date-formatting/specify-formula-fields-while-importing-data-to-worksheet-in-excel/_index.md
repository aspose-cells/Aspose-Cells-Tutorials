---
title: 將資料匯入 Excel 工作表時指定公式字段
linktitle: 將資料匯入 Excel 工作表時指定公式字段
second_title: Aspose.Cells .NET Excel 處理 API
description: 在此詳細教學中，了解如何使用 Aspose.Cells for .NET 將資料匯入具有指定公式欄位的 Excel 工作表。
weight: 11
url: /zh-hant/net/excel-custom-number-date-formatting/specify-formula-fields-while-importing-data-to-worksheet-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將資料匯入 Excel 工作表時指定公式字段

## 介紹

當涉及到以程式設計方式處理 Excel 檔案時，Aspose.Cells for .NET 是一個非常寶貴的工具。它提供了強大的功能，可以輕鬆建立、修改和操作 Excel 電子表格。它提供的有趣功能之一是能夠在將資料匯入 Excel 工作表時指定公式欄位。假設您正在編寫財務報告，並且需要根據使用者輸入自動計算總計。本教程將引導您透過簡潔明了的方法逐步實現這一目標。

## 先決條件

在深入研究程式碼之前，讓我們確保您擁有所需的一切。 

1. Visual Studio 或任何 .NET 整合開發環境 (IDE)：確保您有合適的 IDE 來編寫和執行 C# 程式碼。
2.  Aspose.Cells for .NET：您需要下載並在專案中引用 Aspose.Cells 函式庫。您可以從[Aspose 版本](https://releases.aspose.com/cells/net/).
3. 基礎 C# 知識：熟悉 C# 和物件導向程式設計概念將有助於您更好地理解範例。
4. .NET Framework：本教學假設您使用的是 .NET Framework 4.5 或更高版本。

解決了先決條件後，我們就可以繼續將一些資料匯入到具有指定公式欄位的 Excel 工作表中。

## 導入包

在開始編寫程式碼之前，您需要匯入必要的 Aspose.Cells 命名空間。這通常在 C# 文件的頂部完成：

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;
```

這允許您使用 Aspose.Cells 庫提供的類別和方法，而無需每次都使用命名空間作為前綴。

讓我們將整個過程分解為可管理的步驟：

## 第 1 步：定義輸出目錄

首先，您需要確定 Excel 檔案的儲存位置。您可以這樣做：

```csharp
static string outputDir = "Your Document Directory"; //在此指定您的文件目錄
```

代替`"Your Document Directory"`與您的實際文件路徑。這是產生的 Excel 檔案的儲存位置。

## 步驟 2：為資料項建立使用者定義的類

接下來，我們將定義一個類別來建立我們計劃導入的資料。

```csharp
class DataItems
{
    public int Number1 { get; set; }
    public int Number2 { get; set; }
    public string Formula1 { get; set; }
    public string Formula2 { get; set; }
}
```

這`DataItems`類別將保存原始整數和我們將寫入 Excel 工作表的公式。 

## 步驟 3：初始化一個清單來保存資料項

我們將使用一個清單來保存我們的多個實例`DataItems`班級。

```csharp
List<DataItems> dis = new List<DataItems>();
```

## 步驟 4：將資料項新增至清單中

現在，讓我們為清單中新增一些條目。每個條目將包含兩個數字和兩個公式。

```csharp
//定義並新增每個資料項
DataItems di = new DataItems();
di.Number1 = 2002;
di.Number2 = 3502;
di.Formula1 = "=SUM(A2,B2)";
di.Formula2 = "=HYPERLINK(\"https://www.aspose.com\",\"Aspose 網站\")";
dis.Add(di);

//對其他資料項目重複此操作
```

確保自訂每個`DataItems`具有唯一值和公式的實例。

## 第 5 步：建立工作簿並存取工作表

接下來，建立工作簿並存取我們最終將在其中匯入資料的第一個工作表。

```csharp
Workbook wb = new Workbook(); //建立一個新工作簿
Worksheet ws = wb.Worksheets[0]; //訪問第一個工作表
```

## 步驟 6：指定匯入表選項

這就是奇蹟發生的地方。您需要指定資料中的哪些欄位對應於公式。 

```csharp
ImportTableOptions opts = new ImportTableOptions();
opts.IsFormulas = new bool[] { false, false, true, true };
```

在此範例中，最後兩個欄位包含公式，由下式表示`true`，而前兩個字段設定為`false`.

## 第 7 步：匯入自訂對象

現在一切都已設定完畢，讓我們將資料項目清單匯入工作表中。

```csharp
ws.Cells.ImportCustomObjects(dis, 0, 0, opts);
```

該行有效地匯入從儲存格 A1 開始的資料。

## 第8步：計算公式

由於我們已經導入了一些公式，因此計算它們至關重要。

```csharp
wb.CalculateFormula();
```

此方法可確保您的公式根據其依賴性進行評估。

## 第 9 步：自動調整列

為了確保您的數據易於顯示，您可以根據內容自動調整列。

```csharp
ws.AutoFitColumns();
```

此步驟優化 Excel 檔案的佈局。 

## 第 10 步：儲存 Excel 文件

最後，是時候儲存新建立的 Excel 檔案了。 

```csharp
wb.Save(outputDir + "outputSpecifyFormulaFieldsWhileImportingDataToWorksheet.xlsx");
```

確保您的輸出檔案名稱相關且具有描述性！

## 第11步：檢查執行狀況

作為確認一切正常運作的簡單方法，您可能需要列印一條訊息。

```csharp
Console.WriteLine("SpecifyFormulaFieldsWhileImportingDataToWorksheet executed successfully.");
```

這會立即向您提供程式碼運行正常且沒有任何問題的回饋。

## 結論

現在你就擁有了！您已使用 Aspose.Cells for .NET 和指定的公式欄位成功將資料匯入到 Excel 工作表中。透過執行這些步驟，您可以應用類似的技術來自動執行根據您的需求量身定制的資料處理任務。無論您是要處理報告中的數字還是只是維護數據，掌握使用 Aspose 進行 Excel 操作的藝術都是值得擁有的技能。

## 常見問題解答

### 什麼是 Aspose.Cells？
Aspose.Cells 是一個 .NET 函式庫，旨在以程式設計方式建立、操作和轉換 Excel 檔案。

### 如何安裝 Aspose.Cells for .NET？
您可以從[Aspose 版本](https://releases.aspose.com/cells/net/)並在您的項目中引用它。

### 我可以免費使用 Aspose.Cells 嗎？
是的，Aspose 提供免費試用，網址為[這個連結](https://releases.aspose.com/).

### 我在哪裡可以找到更多範例？
其他範例和文件可以在以下位置找到：[Aspose 文件頁面](https://reference.aspose.com/cells/net/).

### 如果我在使用 Aspose 時遇到問題怎麼辦？
您可以從 Aspose 支援論壇尋求協助[這裡](https://forum.aspose.com/c/cells/9).
 
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
