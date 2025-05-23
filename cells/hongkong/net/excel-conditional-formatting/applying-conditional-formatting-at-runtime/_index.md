---
"description": "透過本全面的逐步指南了解如何使用 Aspose.Cells for .NET 在 Excel 執行階段套用條件格式。"
"linktitle": "在 Excel 中執行階段套用條件格式"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 Excel 中執行階段套用條件格式"
"url": "/zh-hant/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中執行階段套用條件格式

## 介紹

它們是數據分析和視覺化的強大工具。 Excel 的一個突出功能是條件格式，它允許使用者根據儲存格的值對儲存格套用特定的格式樣式。這可以更容易地識別趨勢，突出顯示重要數據點，或簡單地使數據更具可讀性。如果您希望以程式設計方式在 Excel 檔案中實現條件格式，那麼您來對地方了！在本指南中，我們將介紹如何使用 Aspose.Cells for .NET 在執行階段套用條件格式。

## 先決條件
在深入研究程式碼之前，請確保您已準備好開始所需的一切：

1. Visual Studio：確保您的機器上安裝了 Visual Studio。您可以使用任何支援.NET開發的版本。
2. Aspose.Cells for .NET：您需要安裝 Aspose.Cells for .NET。您可以從 [Aspose 網站](https://releases。aspose.com/cells/net/).
3. C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解程式碼片段。
4. .NET Framework：確保您的專案針對的是 .NET Framework 的相容版本。

現在我們已經滿足了先決條件，讓我們進入有趣的部分！

## 導入包
要開始使用 Aspose.Cells，您需要在 C# 專案中匯入必要的命名空間。您可以按照以下步驟操作：

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

這些命名空間將使您能夠存取操作 Excel 檔案和應用條件格式所需的類別和方法。

現在，讓我們將應用條件格式的流程分解為易於管理的步驟。

## 步驟 1：設定您的項目
首先，您需要在 Visual Studio 中建立一個新的 C# 專案。方法如下：

1. 開啟 Visual Studio 並選擇檔案 > 新建 > 專案。
2. 選擇控制台應用程式（.NET Framework）並為您的專案命名。
3. 按一下“建立”。

## 步驟2：新增Aspose.Cells引用
專案設定完成後，您需要新增 Aspose.Cells 庫的引用：

1. 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
2. 選擇管理 NuGet 套件。
3. 搜尋 Aspose.Cells 並安裝它。

這將允許您使用 Aspose.Cells 庫提供的所有功能。

## 步驟 3：建立工作簿對象
接下來，讓我們建立一個新的工作簿和一個工作表。這就是所有魔法發生的地方：

```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// 實例化 Workbook 物件
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

在此步驟中，我們定義儲存 Excel 檔案的目錄，建立一個新的工作簿，並存取第一個工作表。

## 步驟 4：新增條件格式
現在，讓我們來新增一些條件格式。我們先建立一個空的條件格式物件：

```csharp
// 新增空的條件格式
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

在這裡，我們為工作表新增一個新的條件格式集合，它將保存我們的格式規則。

## 步驟 5：定義格式範圍
接下來，我們需要指定應用條件格式的儲存格範圍。假設我們要格式化第一行和第二列：

```csharp
// 設定條件格式範圍。
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

在這段程式碼中，我們定義了兩個條件格式的區域。第一個區域針對的是 (0,0) 處的儲存格，第二個區域針對的是 (1,1) 處的儲存格。請根據您的具體需求隨意調整這些範圍！

## 步驟6：新增條件格式條件
現在是時候定義我們的格式化條件了。假設我們想根據單元格的值突出顯示單元格：

```csharp
// 新增條件。
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// 新增條件。
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

在此步驟中，我們新增兩個條件：一個條件是 `A2` 和 `100`，另一個用於介於 `50` 和 `100`。這使得您能夠根據單元格的值動態地突出顯示單元格。

## 步驟 7：設定格式樣式
有了條件之後，我們現在可以設定格式樣式。讓我們改變條件的背景顏色：

```csharp
// 設定背景顏色。
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

在這裡，我們將第一個條件的背景顏色設為紅色。您可以根據需要更改字體顏色、邊框和其他樣式來進一步自訂！

## 步驟8：儲存Excel文件
最後，是時候保存我們的工作了！我們將工作簿儲存到指定的目錄：

```csharp
// 儲存 Excel 文件
workbook.Save(dataDir + "output.xls");
```

這行程式碼保存了應用了條件格式的 Excel 檔案。確保檢查輸出檔案的指定目錄！

## 結論
就是這樣！您已成功使用 Aspose.Cells for .NET 在 Excel 運行時套用條件格式。這個強大的程式庫可以輕鬆地以程式設計方式操作 Excel 文件，讓您可以自動執行繁瑣的任務並增強資料呈現。無論您處理的是小型專案還是大型應用程序，Aspose.Cells 都可以幫助您簡化工作流程並提高工作效率。

## 常見問題解答

### 什麼是 Aspose.Cells？
Aspose.Cells 是一個 .NET 函式庫，可讓開發人員以程式設計方式建立、操作和轉換 Excel 檔案。

### 我可以將 Aspose.Cells 與其他程式語言一起使用嗎？
是的，Aspose.Cells 適用於多種程式語言，包括 Java、Python 等。

### Aspose.Cells 有免費試用版嗎？
是的，您可以從 [Aspose 網站](https://releases。aspose.com/).

### 我如何獲得 Aspose.Cells 的支援？
您可以透過訪問 [Aspose 支援論壇](https://forum。aspose.com/c/cells/9).

### 我需要許可證才能使用 Aspose.Cells 嗎？
是的，商業使用需要許可證，但您可以申請臨時許可證 [這裡](https://purchase。aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}