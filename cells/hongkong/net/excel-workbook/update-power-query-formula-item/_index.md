---
"description": "使用 Aspose.Cells for .NET 輕鬆更新 Excel 中的 Power Query 公式項目。逐步指導您簡化資料操作流程。"
"linktitle": "更新 Power Query 公式項"
"second_title": "Aspose.Cells for .NET API參考"
"title": "更新 Power Query 公式項"
"url": "/zh-hant/net/excel-workbook/update-power-query-formula-item/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 更新 Power Query 公式項

## 介紹

如果您曾經使用過 Excel，您就會知道它有多強大 - 尤其是當您開始深入研究 Power Queries 時。這些都是讓您輕鬆轉換、清理和分析資料的秘訣。在 Excel 中操作 Power Query 公式的一個巧妙方法是透過 Aspose.Cells for .NET。今天，我們將指導您逐步更新 Power Query 公式項目。那麼，戴上你的編碼帽，讓我們開始吧！

## 先決條件

在深入研究程式碼之前，您需要設定一些內容：

1. Visual Studio：您需要一個整合開發環境 (IDE) 來編寫和執行您的 .NET 程式碼。 Visual Studio 是首選。
2. Aspose.Cells 庫：確保您的專案中擁有 Aspose.Cells 庫。您可以從 [地點](https://releases。aspose.com/cells/net/).
3. C# 基礎知識：雖然我們將一起完成這個過程，但對 C# 有一些基礎知識的了解肯定會有所幫助，尤其是在瀏覽不同的類別和方法時。
4. 範例 Excel 檔案：您需要程式碼片段中提到的 Excel 檔案。確保您擁有：
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework：確保您的專案針對的是 .NET Framework 的相容版本。

現在我們已經準備好了工具包，我們可以繼續進行有趣的部分：編寫程式碼！

## 導入包

首先，您需要匯入必要的命名空間。具體操作如下：

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

透過新增這些命名空間，您可以讓編譯器知道您打算使用 Aspose.Cells 庫中的類別和方法。這一步至關重要，因為它為後面的程式碼奠定了基礎。

讓我們分解一下您提供的程式碼片段。本教學將引導您完成每個部分，確保您了解正在發生的事情。

## 步驟 1：設定工作目錄

在此步驟中，我們將定義來源檔案和輸出檔案的位置。這可確保 Aspose 知道在哪裡找到您的 Excel 檔案。

```csharp
// 工作目錄
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## 第 2 步：載入工作簿

現在，讓我們載入 Power Query 所在的 Excel 檔案。

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
這 `Workbook` 類別是您進入 Excel 檔案的入口點。透過傳遞來源檔案的路徑，我們建立了一個允許我們操作它的實例。您可以將其想像為打開一本書 - 您正準備閱讀（或編輯）其內容。

## 步驟 3：存取資料混搭

接下來，我們將存取儲存在工作簿的資料混搭中的 Power Query 公式。

```csharp
DataMashup mashupData = workbook.DataMashup;
```
這 `DataMashup` 類別包含與您的工作簿相關的所有 Power Query 公式。這是我們進行繁重工作的地方，就像打開工具箱進行維修一樣。

## 步驟 4：循環遍歷 Power Query 公式

現在我們遍歷 Power Query 公式來找到我們想要更新的特定公式。

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

- 我們循環遍歷每一個 `PowerQueryFormula` 在 `mashupData`。
- 在這個循環中，我們深入研究每一個 `PowerQueryFormulaItem`。
- 我們檢查該項目的名稱是否與「來源」相符。如果是，我們就更新它的值以連結到我們的新來源檔案。

這類似於在手冊中找到正確的頁面，然後進行必要的更新——這是一個簡單而細緻的過程。

## 步驟 5：儲存更新的工作簿

完成更新後，就該儲存我們的變更了。

```csharp
// 儲存輸出工作簿。
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
這 `Save` 方法將更新的工作簿寫入指定的輸出目錄。這就像將您的編輯密封在新版本的手冊中，以供其他人使用！

## 結論

恭喜！您已成功使用 Aspose.Cells for .NET 更新 Power Query 公式項目。透過這種方法，您可以自動修改 Excel 檔案中的 Power Query 公式，從而節省寶貴的時間和精力。

## 常見問題解答

### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的程式庫，用於在 .NET 應用程式中操作 Excel 文件，而無需安裝 Microsoft Excel。

### 我需要 Microsoft Excel 來執行 Aspose.Cells 嗎？
不，Aspose.Cells 使您能夠以程式設計方式建立和編輯 Excel 文件，而無需在伺服器或開發機器上安裝 Excel。

### 我可以使用 Aspose.Cells 處理哪些類型的 Excel 檔案？
您可以使用 Aspose.Cells 處理 .xlsx、.xls、.xlsm 和其他幾種 Excel 格式。

### Aspose.Cells 有試用版嗎？
是的，您可以從 [Aspose Cells發佈頁面](https://releases。aspose.com/).

### 我如何獲得 Aspose.Cells 的支援？
您可以透過以下方式獲得支持 [Aspose 論壇](https://forum.aspose.com/c/cells/9)，您可以在這裡提出問題並從社區和 Aspose 團隊中找到答案。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}