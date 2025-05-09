---
"description": "在本簡單易懂的教學中，學習如何使用 Aspose.Cells for .NET 將自訂 DB Num 格式的資料匯入 Excel。"
"linktitle": "使用自訂資料庫編號模式格式將資料匯入 Excel"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "使用自訂資料庫編號模式格式將資料匯入 Excel"
"url": "/zh-hant/net/excel-data-import-export/import-data-to-worksheet-in-excel-with-specified-db-num-custom-pattern-formatting/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用自訂資料庫編號模式格式將資料匯入 Excel

## 介紹

當涉及到電子表格操作時，將資料匯入 Excel 並正確格式化似乎是一項艱鉅的任務，尤其是當您想要使用特定的基於文化的格式（例如 DB Num 模式）時。如果您曾經因 Excel 格式的技術細節而感到困惑，那麼您來對地方了！在本指南中，我們將使用 Aspose.Cells for .NET 將事情分解為簡單的步驟，使您的資料匯入不僅簡單而且美觀。所以，請堅持住，因為我們將輕鬆進入 .NET 編程、格式化和匯出 Excel 檔案的世界！

## 先決條件

在我們討論細節之前，讓我們先確保您已準備好所需的一切。以下是幫助您取得成功的先決條件的快速清單：

1. .NET Framework：確保您的機器上安裝了 .NET Framework。 Aspose.Cells 可與各種 .NET 版本無縫合作。
2. Aspose.Cells for .NET：您需要下載並安裝 Aspose.Cells 函式庫。您可以從 [下載連結](https://releases。aspose.com/cells/net/).
3. 整合開發環境 (IDE)：使用像 Visual Studio 這樣的 IDE，您可以在其中編寫和執行 C# 程式碼。
4. C# 基礎知識：對 C# 有基本的了解將有助於您遵循本指南中使用的編碼實踐。

都拿到了嗎？偉大的！讓我們繼續導入必要的套件。

## 導入包

為了有效地使用 Aspose.Cells，您需要在 C# 檔案的開頭匯入所需的命名空間。讓我們一步一步地分解一下。

### 建立您的 C# 文件

開啟您的 IDE（建議使用 Visual Studio）並建立新的 C# 專案。將其命名為相關名稱，例如 `ExcelDataImport`。

### 參考 Aspose.Cells

您必須在專案中包含 Aspose.Cells 函式庫。在解決方案資源管理器中右鍵單擊您的專案並選擇“新增參考”。瀏覽到您安裝 Aspose.Cells 的位置並選擇它。

### 導入必要的命名空間

在 C# 檔案的頂部，匯入以下命名空間：

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

這條簡單的線路是您獲得 Aspose.Cells 所提供的所有功能的入口。 

現在我們已經滿足了所有先決條件並匯入了必要的套件，讓我們深入了解將資料匯入 Excel 並套用自訂 DB Num 模式格式的逐步流程。我們將有條不紊地進行此事，以確保清晰度和理解力。

## 步驟1：設定資料目錄

首先，您需要指定已儲存輸出的文件目錄的路徑。根據您的文件結構進行調整。

```csharp
string dataDir = "Your Document Directory";
```

在此範例中，替換 `Your Document Directory` 與您的實際路徑，例如 `C:\\Users\\YourName\\Documents\\`。

## 步驟 2：建立工作簿

接下來，您將建立一個新的工作簿，它本質上是您的 Excel 檔案。

```csharp
Workbook wb = new Workbook();
```

在這裡，我們實例化一個新的 `Workbook` 目的。這是您的空白畫布！

## 步驟 3：存取第一個工作表

每個工作簿包含多個工作表。您將需要存取第一個工作表來開始輸入資料。

```csharp
Worksheet ws = wb.Worksheets[0];
```

就像翻開一本書的第一頁一樣，您正在存取第一個工作表來新增資料。

## 步驟 4：將資料輸入儲存格

現在，讓我們用一些資料填充單元格。對於此範例，我們將輸入值 `123` 到單元格 A1。

```csharp
Cell cell = ws.Cells["A1"];
cell.PutValue(123);
```

您在這裡直接與 Excel 對話 — — 將資料直接放入儲存格 A1！ 

## 步驟 5：存取儲存格樣式

每個單元格都有一種樣式，您可以自訂它的外觀。要套用自訂格式，首先，您需要存取儲存格的樣式。

```csharp
Style st = cell.GetStyle();
```

透過抓住單元格的風格，您正準備添加自己獨特的風格！

## 步驟 6：指定 DBNum 自訂模式格式

這就是奇蹟發生的地方。您可以使用 DBNum 格式樣式指定自訂格式模式。

```csharp
st.Custom = "[DBNum2][$-804]General";
```

這行告訴 Excel 格式化數字 `123` 依照中文對應的DBNum模式。非常整潔，對吧？

## 步驟 7：設定更新的儲存格樣式

現在您已經定義了自訂樣式，是時候將其套用到儲存格了。

```csharp
cell.SetStyle(st);
```

這就像是給你的手機穿上一件時尚的新衣服！

## 步驟8：調整列寬

讓我們確保一切看起來漂亮又整潔。您可以調整第一列的寬度以更好地適合您的資料。

```csharp
ws.Cells.SetColumnWidth(0, 30);
```

在這裡，我們擴大了列寬，這樣您的資料就不會顯得擁擠。想像一下給你的數據提供呼吸的空間！

## 步驟 9：儲存工作簿

最後，讓我們將這個傑作儲存為PDF格式。這就是大結局！

```csharp
wb.Save(dataDir + "outputDBNumCustomFormatting.pdf", SaveFormat.Pdf);
```

恭喜！您剛剛建立了一個 PDF 文件，其中展示了使用 DB Num 樣式格式化的號碼。

## 結論

就是這樣！您已成功將資料匯入 Excel，套用自訂 DB Num 格式，並將其儲存為 PDF 格式。透過 Aspose.Cells for .NET，這個過程不僅變得更容易，而且更靈活和更強大。不再需要為 Excel 的內建格式選項而苦惱 - 現在您可以透過程式碼直接控制！

無論您是準備數據報告還是建立財務報表，利用 Aspose.Cells 的強大功能都會將您的電子表格遊戲提升到一個全新的水平。那麼，您還在等什麼呢？滿懷信心地投入您的專案中，讓您的數據大放異彩！

## 常見問題解答

### 什麼是 Aspose.Cells？  
Aspose.Cells 是一個強大的 .NET 程式庫，可讓開發人員以程式設計方式建立、操作和轉換 Excel 檔案。

### 我可以格式化其他類型的儲存格嗎？  
是的！您可以將不同的樣式、格式甚至公式套用到工作表中的任何儲存格。

### 有免費試用嗎？  
絕對地！您可以查看免費試用版 [這裡](https://releases。aspose.com/).

### 我可以將 Excel 檔案儲存為哪些格式？  
Aspose.Cells 支援多種格式，包括 XLSX、XLS、CSV、PDF 等。

### 我可以在哪裡找到更多支援？  
如果您需要幫助，請訪問他們的 [支援論壇](https://forum.aspose.com/c/cells/9) 尋求社區和專家的幫助。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}