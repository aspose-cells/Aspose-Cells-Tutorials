---
title: 實現局部單元格公式與局部範圍公式類似
linktitle: 實現局部單元格公式與局部範圍公式類似
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何實作與 Aspose.Cells for .NET 中的範圍公式本機功能類似的儲存格公式。了解自訂內建 Excel 函數名稱等。
weight: 13
url: /zh-hant/net/workbook-settings/implement-cell-formula-local-similar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 實現局部單元格公式與局部範圍公式類似

## 介紹
Aspose.Cells for .NET 是一個強大且靈活的電子表格操作 API，可讓您以程式設計方式建立、操作和轉換 Excel 檔案。 Aspose.Cells 提供的眾多功能之一是能夠自訂內建 Excel 函數的行為，包括建立您自己的本機函數名稱的能力。在本教學中，我們將引導您完成實作儲存格公式的步驟，該公式類似於 Aspose.Cells for .NET 中的範圍公式本機功能。
## 先決條件
在開始之前，請確保您具備以下條件：
1. 您的系統上安裝了 Microsoft Visual Studio 2010 或更高版本。
2. 專案中安裝的最新版本的 Aspose.Cells for .NET 函式庫。您可以從以下位置下載該程式庫[Aspose.Cells for .NET 下載頁面](https://releases.aspose.com/cells/net/).
## 導入包
首先，您需要在 C# 專案中匯入必要的套件。在程式碼檔案頂部加入以下 using 語句：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## 第 1 步：建立自訂全球化設定類
第一步是建立自訂`GlobalizationSettings`類別將允許您覆寫 Excel 函數的預設行為。在此範例中，我們將更改`SUM`和`AVERAGE`功能`UserFormulaLocal_SUM`和`UserFormulaLocal_AVERAGE`， 分別。
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
接下來，建立一個新的 Workbook 實例並指派自訂`GlobalizationSettings`工作簿的實作類`Settings.GlobalizationSettings`財產。
```csharp
//建立工作簿
Workbook wb = new Workbook();
//分配 GlobalizationSettings 實作類
wb.Settings.GlobalizationSettings = new GS();
```
## 步驟 3：存取第一個工作表和儲存格
現在，讓我們存取工作簿中的第一個工作表以及該工作表中的特定儲存格。
```csharp
//訪問第一個工作表
Worksheet ws = wb.Worksheets[0];
//存取某些儲存格
Cell cell = ws.Cells["C4"];
```
## 步驟 4： 分配公式並列印 FormulaLocal
最後，讓我們分配`SUM`和`AVERAGE`將公式寫入儲存格並列印結果`FormulaLocal`價值觀。
```csharp
//指派 SUM 公式並列印其 FormulaLocal
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//分配 AVERAGE 公式並列印其 FormulaLocal
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## 結論
在本教學中，您學習如何實作與 Aspose.Cells for .NET 中的範圍公式本機功能類似的儲存格公式。透過建立自訂`GlobalizationSettings`在類別中，您可以覆寫 Excel 函數的預設行為並自訂本機函數名稱以滿足您的需求。這在處理本地化或國際化 Excel 文件時特別有用。
## 常見問題解答
### 目的是什麼`GlobalizationSettings` class in Aspose.Cells?
這`GlobalizationSettings` Aspose.Cells 中的類別可讓您自訂內建 Excel 函數的行為，包括變更本機函數名稱的功能。
### 我可以覆寫除以下函數之外的函數的行為嗎`SUM` and `AVERAGE`?
是的，您可以透過修改以下內容來覆寫任何內建 Excel 函數的行為`GetLocalFunctionName`您自訂的方法`GlobalizationSettings`班級。
### 有沒有辦法將函數名稱重回預設值？
是的，您可以透過刪除自訂函數來重置函數名稱`GlobalizationSettings`類別或透過傳回一個空字串`GetLocalFunctionName`方法。
### 我可以使用此功能在 Aspose.Cells 中建立自訂函數嗎？
不，該`GlobalizationSettings`類別旨在覆蓋內建 Excel 函數的行為，而不是建立自訂函數。如果您需要建立自訂函數，您可以使用`UserDefinedFunction`Aspose.Cells 中的類別。
### 此功能在 Aspose.Cells for .NET 的所有版本中都可用嗎？
是的，`GlobalizationSettings`類別和自訂函數名稱的功能在 Aspose.Cells for .NET 的所有版本中均可使用。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
