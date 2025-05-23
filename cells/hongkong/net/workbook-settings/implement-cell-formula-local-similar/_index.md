---
"description": "了解如何實作與 Aspose.Cells for .NET 中的範圍公式本機功能類似的儲存格公式。學習自訂內建 Excel 函數名稱等。"
"linktitle": "實現類似於本地範圍公式的本機單元格公式"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "實現類似於本地範圍公式的本機單元格公式"
"url": "/zh-hant/net/workbook-settings/implement-cell-formula-local-similar/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 實現類似於本地範圍公式的本機單元格公式

## 介紹
Aspose.Cells for .NET 是一個強大且靈活的電子表格操作 API，可讓您以程式設計方式建立、操作和轉換 Excel 檔案。 Aspose.Cells 提供的眾多功能之一是能夠自訂內建 Excel 函數的行為，包括建立您自己的本機函數名稱的能力。在本教學中，我們將引導您完成實作類似 Aspose.Cells for .NET 中的範圍公式本機功能的儲存格公式的步驟。
## 先決條件
在開始之前，請確保您已具備以下條件：
1. 您的系統上安裝了 Microsoft Visual Studio 2010 或更高版本。
2. 您的專案中安裝了最新版本的 Aspose.Cells for .NET 程式庫。您可以從 [Aspose.Cells for .NET下載頁面](https://releases。aspose.com/cells/net/).
## 導入包
首先，您需要在 C# 專案中匯入必要的套件。在程式碼檔案頂部新增以下使用語句：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## 步驟 1：建立自訂全球化設定類
第一步是建立自訂 `GlobalizationSettings` 該類別將允許您覆寫 Excel 函數的預設行為。在這個例子中，我們將更改 `SUM` 和 `AVERAGE` 功能 `UserFormulaLocal_SUM` 和 `UserFormulaLocal_AVERAGE`， 分別。
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //根據您的需求變更 SUM 函數名稱。
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //根據您的需求變更 AVERAGE 函數名稱。
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## 步驟 2：建立新工作簿並指派自訂全球化設置
接下來，建立一個新的 Workbook 實例並指派自訂 `GlobalizationSettings` 工作簿的實作類 `Settings.GlobalizationSettings` 財產。
```csharp
//建立工作簿
Workbook wb = new Workbook();
//分配 GlobalizationSettings 實作類
wb.Settings.GlobalizationSettings = new GS();
```
## 步驟 3：存取第一個工作表和儲存格
現在，讓我們存取工作簿中的第一個工作表和該工作表中的特定儲存格。
```csharp
//訪問第一個工作表
Worksheet ws = wb.Worksheets[0];
//存取某些儲存格
Cell cell = ws.Cells["C4"];
```
## 步驟 4：分配公式並列印 FormulaLocal
最後，讓我們分配 `SUM` 和 `AVERAGE` 公式到單元格並列印結果 `FormulaLocal` 值。
```csharp
//指派 SUM 公式並列印其 FormulaLocal
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//分配 AVERAGE 公式並列印其 FormulaLocal
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## 結論
在本教學中，您學習如何實作與 Aspose.Cells for .NET 中的範圍公式本機功能類似的儲存格公式。透過建立自訂 `GlobalizationSettings` 類，您可以覆寫 Excel 函數的預設行為並自訂本地函數名稱以滿足您的需求。這在處理本地化或國際化的 Excel 文件時特別有用。
## 常見問題解答
### 的目的是什麼 `GlobalizationSettings` Aspose.Cells 中的類別？
這 `GlobalizationSettings` Aspose.Cells 中的類別可讓您自訂內建 Excel 函數的行為，包括變更本機函數名稱的能力。
### 我可以覆蓋除 `SUM` 和 `AVERAGE`？
是的，您可以透過修改 `GetLocalFunctionName` 您的自訂方法 `GlobalizationSettings` 班級。
### 有沒有辦法將函數名稱重設為其預設值？
是的，您可以透過刪除自訂 `GlobalizationSettings` 類或透過從 `GetLocalFunctionName` 方法。
### 我可以使用此功能在 Aspose.Cells 中建立自訂函數嗎？
不， `GlobalizationSettings` 該類別旨在覆蓋內建 Excel 函數的行為，而不是建立自訂函數。如果需要建立自訂函數，可以使用 `UserDefinedFunction` Aspose.Cells 中的類別。
### 所有版本的 Aspose.Cells for .NET 都提供此功能嗎？
是的， `GlobalizationSettings` 類別和自訂函數名稱的功能在 Aspose.Cells for .NET 的所有版本中均可使用。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}