---
title: 建立具有所需頁面大小的圖表 PDF
linktitle: 建立具有所需頁面大小的圖表 PDF
second_title: Aspose.Cells .NET Excel 處理 API
description: 使用 Aspose.Cells for .NET 使用 Excel 圖表建立 PDF。透過此逐步指南了解具體操作方法。
weight: 12
url: /zh-hant/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立具有所需頁面大小的圖表 PDF

## 介紹

創建具有視覺吸引力和資訊豐富的圖表對於各個領域的數據表示至關重要。無論您是處理銷售數據、績效指標還是任何其他類型的信息，能夠產生高品質的圖表都可以讓您的發現更加深入和清晰。如果您使用 .NET 應用程序，Aspose.Cells 是一個功能強大的庫，它使處理 Excel 文件和生成圖表變得輕而易舉。在本教學中，我們將引導您完成從具有所需頁面大小的 Excel 檔案建立圖表 PDF 的過程。

## 先決條件

在深入研究程式碼之前，您必須滿足一些先決條件才能確保流暢的體驗：

### C# 和 .NET 基礎知識

您需要對 C# 程式設計和 .NET 框架有基本的了解。這將幫助您掌握本指南中將遇到的程式碼的結構。

### Aspose.Cells for .NET

請確定您已安裝 Aspose.Cells for .NET。您可以在以下位置找到所有詳細信息[Aspose.Cells 文檔](https://reference.aspose.com/cells/net/). 

### 開發環境

設定您的開發環境。這可以是 Visual Studio 或任何其他支援 C# 的 IDE。從以下位置下載並安裝 Aspose.Cells 庫[下載頁面](https://releases.aspose.com/cells/net/).

### Excel 檔案範例

您將需要一個至少包含一個圖表的範例 Excel 檔案。您可以建立一個範例文件或下載一個範例文件以在本教程中使用。

## 導入包

要開始使用 Aspose.Cells，您需要在 C# 應用程式中匯入必要的命名空間。操作方法如下：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

這些命名空間可讓您存取操作 Excel 工作簿及其內容所需的類別和方法。

現在我們已經解決了所有先決條件，讓我們將該過程分解為詳細的步驟。

## 第 1 步：設定輸出和來源目錄

首先，您需要定義輸出 PDF 的儲存位置以及來源 Excel 文件的位置。

```csharp
//輸出目錄
string outputDir = "Your Output Directory";

//原始碼目錄
string sourceDir = "Your Document Directory";
```

確保將“您的輸出目錄”和“您的文件目錄”替換為系統上的實際路徑。這決定了 Aspose 將保存生成的 PDF 以及在何處找到 Excel 檔案。

## 第 2 步：載入範例 Excel 文件

接下來，您需要載入包含圖表的 Excel 檔案。方法如下：

```csharp
//載入包含圖表的範例 Excel 檔案。
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

這`Workbook`類別是與 Excel 文件互動的核心。確保路徑正確指向您的 Excel 檔案 - 此處的錯誤將阻止其餘程式碼的執行。

## 第 3 步：存取第一個工作表

載入工作簿後，下一步是存取包含所需圖表的工作表。

```csharp
//訪問第一個工作表。
Worksheet ws = wb.Worksheets[0];
```

在 Aspose.Cells 中，工作表從零開始索引，因此`Worksheets[0]`指第一張紙。

## 第 4 步：訪問第一個圖表

現在，讓我們存取要匯出為 PDF 的圖表。此步驟假設您的工作表至少包含一個圖表。

```csharp
//訪問工作表內的第一個圖表。
Chart ch = ws.Charts[0];
```

同樣，這將訪問工作表中的第一個圖表；確保您的工作表結構適合這種方法。

## 第 5 步：建立具有所需頁面尺寸的 PDF

最後，是時候根據具有指定頁面大小的圖表建立 PDF 了。這是完成這一切的神奇程式碼行：

```csharp
//建立具有所需頁面大小的圖表 pdf。
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

在此程式碼中：
- PDF 將會儲存到您先前指定的輸出目錄。
- 數位`7, 7`分別表示所需頁面尺寸的寬度和高度。
- PageLayoutAlignmentType.Center 確保圖表在頁面上居中。

## 步驟6：確認訊息

為了讓自己（和其他人）知道一切順利，請在程式碼末尾添加確認訊息：

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

過程完成後，此訊息將出現在控制台視窗中，表示您的 PDF 已順利建立。

## 結論

恭喜！您剛剛學習如何利用 Aspose.Cells for .NET 從 Excel 檔案中包含的圖表建立 PDF。這個功能強大的程式庫簡化了操作 Excel 文件和產生資料視覺化表示的過程，從而節省您數小時的手動格式化時間。請務必探索 Aspose.Cells 提供的眾多其他功能，而不僅僅是 PDF 生成——您永遠不知道什麼可以進一步增強您的專案！

## 常見問題解答

### Aspose.Cells for .NET 的用途是什麼？  
Aspose.Cells for .NET 用於在 .NET 應用程式中以程式設計方式建立、編輯和轉換 Excel 文件。

### 我可以免費使用 Aspose.Cells 嗎？  
是的，Aspose.Cells 提供了[免費試用](https://releases.aspose.com/)出於評估目的。

### 有沒有辦法將我的試用期延長到初始期限之後？  
你可以申請一個[臨時執照](https://purchase.aspose.com/temporary-license/)用於擴展測試。

### 如果我遇到問題或有疑問怎麼辦？  
您可以向 Aspose 社群尋求協助[支援論壇](https://forum.aspose.com/c/cells/9).

### 如何購買 Aspose.Cells？  
您可以從以下網站購買 Aspose.Cells[購買頁面](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
