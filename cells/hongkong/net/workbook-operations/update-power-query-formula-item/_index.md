---
title: 更新工作簿中的 Power Query 公式項
linktitle: 更新工作簿中的 Power Query 公式項
second_title: Aspose.Cells .NET Excel 處理 API
description: 在這份全面的逐步指南中了解如何使用 Aspose.Cells for .NET 更新 Excel 中的 Power Query 公式。
weight: 27
url: /zh-hant/net/workbook-operations/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 更新工作簿中的 Power Query 公式項

## 介紹
了解如何使用 Excel 中的 Power Query 有效管理資料對於任何資料分析師或 Excel 愛好者來說都是至關重要的。如果您曾經需要更新 Power Query 工作簿中的公式項目，那麼您來對地方了。本指南旨在協助您了解如何使用 Aspose.Cells for .NET 無縫更新 Excel 工作簿中的 Power Query 公式。透過幾個簡單的步驟，您將能夠操縱和簡化數據，確保您的工作簿保持動態和集中。
## 先決條件
在開始深入研究範例程式碼和步驟之前，讓我們先回顧一下您需要什麼：
1. 對 C# 和 .NET 的基本了解：熟悉 C# 中的程式設計概念將很有幫助，因為我們將編寫一些程式碼。
2. 安裝 Aspose.Cells for .NET：您需要將 Aspose.Cells 函式庫整合到您的 .NET 專案中。你可以下載它[這裡](https://releases.aspose.com/cells/net/).
3. 準備修改的 Excel 檔案：確保您有一個包含要更新的 Power Query 的 Excel 檔案。您需要有一個範例工作簿，例如`SamplePowerQueryFormula.xlsx`任您支配。
## 導入包
首先，請確保 C# 檔案中包含以下命名空間：
```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```
這將允許您存取 Aspose.Cells 庫提供的功能，特別是處理工作簿和 Power Query 資料。
## 第 1 步：設定您的工作目錄
首先，您需要定義原始檔案和輸出檔案的位置。 
```csharp
string SourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
```
在此步驟中，您指定目錄路徑。代替`"Your Document Directory"`與儲存 Excel 檔案的實際路徑。這告訴程式在哪裡查找原始檔案以及在哪裡保存更新的檔案。
## 第 2 步：載入工作簿
現在您已經設定了工作目錄，下一步是將 Excel 檔案載入到程式中。
```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
在這裡，您創建一個`Workbook`載入指定 Excel 檔案的物件。這`Workbook`類別是 Aspose.Cells 庫的一部分，對於您對該 Excel 檔案執行的任何操作都是必不可少的。
## 第 3 步：存取 Power Query 數據
載入工作簿後，就可以存取其中儲存的 Power Query 公式了。
```csharp
DataMashup mashupData = workbook.DataMashup;
```
在這一行中，`DataMashup`屬性有助於存取工作簿中的 Power Query 資料結構。此屬性可讓您與 Excel 檔案中包含的 Power Query 資料的各個方面進行互動。
## 步驟 4： 循環存取 Power Query 公式
在可存取 Power Query 資料後，下一步是迭代現有的每個公式。
```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```
這就是奇蹟發生的地方。我們循環遍歷每個`PowerQueryFormula`然後透過每個`PowerQueryFormulaItem`。這`if`語句尋找名為「Source」的公式項，並將其值更新為您希望 Power Query 引用的來源檔案的路徑。
## 步驟 5：儲存更新的工作簿
更新必要的公式項目後，最後一步是儲存工作簿。
```csharp
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
```
此行將修改後的工作簿儲存到新文件中，從而保留原始工作簿，同時允許您使用更新的版本。
## 步驟6：確認訊息
最後，檢查程式碼是否正確執行是一個很好的做法。
```csharp
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
這個簡單的訊息將在控制台中向您確認您的操作已成功，從而為該過程提供一個令人放心的結束。
## 結論
現在你就擁有了！只需幾個簡單的步驟即可使用 Aspose.Cells for .NET 更新 Excel 中的 Power Query 公式項目。透過遵循本指南，您可以有效管理 Excel 資料連線並保持工作簿順利運作。無論您是經驗豐富的專業人士還是剛開始資料操作，Aspose.Cells 都提供了一種強大的方法來自動化和增強 Excel 工作流程。 
## 常見問題解答
### 我可以將 Aspose.Cells 與任何版本的 .NET 一起使用嗎？
Aspose.Cells 與多個版本的 .NET 相容，包括 .NET Framework 和 .NET Core。
### Aspose.Cells 可以免費使用嗎？
 Aspose.Cells 提供免費試用，但要持續使用，需要許可證。您可以獲得臨時許可證[這裡](https://purchase.aspose.com/temporary-license/).
### 如果我現有的 Excel 檔案沒有 Power Query 怎麼辦？
所描述的流程重點是更新 Power Query 項目，因此如果您的文件缺少它們，您需要先合併 Power Queries。
### 在哪裡可以找到有關 Aspose.Cells 的更多資訊？
查看文件以獲取全面的指導和範例。參觀[文件](https://reference.aspose.com/cells/net/).
### 如何回報 Aspose.Cells 的錯誤或問題？
您可以聯絡他們支援的論壇，尋求有關您遇到的任何問題的協助。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
