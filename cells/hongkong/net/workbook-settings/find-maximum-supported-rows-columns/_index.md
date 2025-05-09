---
"description": "使用 Aspose.Cells for .NET 發現 XLS 和 XLSX 格式支援的最大行數和列數。透過本綜合教學最大化您的 Excel 資料管理能力。"
"linktitle": "尋找 XLS 和 XLSX 格式支援的最大行數和列數"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "尋找 XLS 和 XLSX 格式支援的最大行數和列數"
"url": "/zh-hant/net/workbook-settings/find-maximum-supported-rows-columns/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 尋找 XLS 和 XLSX 格式支援的最大行數和列數

## 介紹
在 Excel 的世界中，管理大型資料集可能是一項艱鉅的任務，尤其是在處理不同文件格式支援的最大行數和列數時。本教學將指導您使用 Aspose.Cells for .NET 函式庫來尋找 XLS 和 XLSX 格式支援的最大行數和列數。閱讀本文後，您將全面了解如何利用這個強大的工具有效地處理與 Excel 相關的任務。
## 先決條件
在深入學習本教程之前，請確保您已滿足以下先決條件：
1. [.NET 框架](https://dotnet.microsoft.com/en-us/download) 或者 [.NET 核心](https://dotnet.microsoft.com/en-us/download) 安裝在您的系統上。
2. [Aspose.Cells for .NET](https://releases.aspose.com/cells/net/) 下載並在專案中引用的庫。
如果您還沒有，您可以從 [網站](https://releases.aspose.com/cells/net/) 或透過以下方式安裝 [NuGet](https://www。nuget.org/packages/Aspose.Cells/).
## 導入包
首先，您需要從 Aspose.Cells for .NET 程式庫匯入必要的套件。在 C# 檔案的頂部加入以下使用語句：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## 步驟 1：找出 XLS 格式支援的最大行數和列數
讓我們先來探索 XLS（Excel 97-2003）格式支援的最大行數和列數。
```csharp
// 列印有關 XLS 格式的消息。
Console.WriteLine("Maximum Rows and Columns supported by XLS format.");
// 以 XLS 格式建立工作簿。
Workbook wb = new Workbook(FileFormatType.Excel97To2003);
// 列印XLS格式支援的最大行數和列數。
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
在此步驟中，我們：
1. 列印一條訊息以表示我們正在使用 XLS 格式。
2. 創建新的 `Workbook` 實例使用 `FileFormatType.Excel97To2003` 枚舉，代表 XLS 格式。
3. 使用以下方法檢索 XLS 格式支援的最大行數和列數 `Workbook.Settings.MaxRow` 和 `Workbook.Settings.MaxColumn` 屬性。我們將這些值加 1 以獲得實際的最大行數和列數（因為它們是從零開始的）。
4. 將最大行數和最大列數列印到控制台。
## 步驟 2：尋找 XLSX 格式支援的最大行數和列數
接下來，我們來探討XLSX（Excel 2007及更高版本）格式支援的最大行數和列數。
```csharp
// 列印有關 XLSX 格式的消息。
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// 以 XLSX 格式建立工作簿。
wb = new Workbook(FileFormatType.Xlsx);
// 列印 XLSX 格式支援的最大行數和列數。
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
在此步驟中，我們：
1. 列印一條訊息以表示我們正在使用 XLSX 格式。
2. 創建新的 `Workbook` 實例使用 `FileFormatType.Xlsx` 枚舉，代表 XLSX 格式。
3. 使用下列方法檢索 XLSX 格式支援的最大行數和列數 `Workbook.Settings.MaxRow` 和 `Workbook.Settings.MaxColumn` 屬性。我們將這些值加 1 以獲得實際的最大行數和列數（因為它們是從零開始的）。
4. 將最大行數和最大列數列印到控制台。
## 步驟 3：顯示成功訊息
最後，讓我們顯示一條成功訊息，表示「FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats」範例已成功執行。
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
此步驟只是將成功訊息列印到控制台。
## 結論
在本教學中，您學習如何使用 Aspose.Cells for .NET 函式庫來尋找 XLS 和 XLSX 檔案格式支援的最大行數和列數。透過了解這些格式的局限性，您可以更好地規劃和管理基於 Excel 的項目，確保您的資料符合支援的範圍。
## 常見問題解答
### XLS 格式支援的最大行數是多少？
XLS（Excel 97-2003）格式支援的最大行數為 65,536。
### XLS 格式最多支援多少列？
XLS（Excel 97-2003）格式支援的最大列數為256列。
### XLSX 格式支援的最大行數是多少？
XLSX（Excel 2007 及更高版本）格式支援的最大行數為 1,048,576。
### XLSX 格式支援的最大列數是多少？
XLSX（Excel 2007 及更高版本）格式支援的最大列數為 16,384。
### 我可以使用 Aspose.Cells for .NET 函式庫來處理其他 Excel 檔案格式嗎？
是的，Aspose.Cells for .NET 函式庫支援多種 Excel 檔案格式，包括 XLS、XLSX、ODS 等。您可以探索 [文件](https://reference.aspose.com/cells/net/) 了解可用的特性和功能。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}