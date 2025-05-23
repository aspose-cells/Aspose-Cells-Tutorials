---
"description": "透過我們全面的逐步教學學習如何使用 Aspose.Cells for .NET 以程式設計方式變更資料透視表來源資料。"
"linktitle": "在 .NET 中以程式設計方式變更資料透視表的來源數據"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 .NET 中以程式設計方式變更資料透視表的來源數據"
"url": "/zh-hant/net/creating-and-configuring-pivot-tables/changing-source-data/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以程式設計方式變更資料透視表的來源數據

## 介紹
在資料分析領域，很少有工具能像 Microsoft Excel 一樣閃耀。每天，無數用戶依靠 Excel 來管理和分析數據，但在幕後，它比簡單的點擊和拖曳要複雜得多。如果您曾經想以程式設計方式操作 Excel 檔案（具體來說，更改資料透視表的來源資料），那麼您來對地方了！在本指南中，我們將探討如何使用 Aspose.Cells for .NET 來實現這一點。無論您是經驗豐富的開發人員還是剛剛涉足程式設計領域，您都會發現本教學包含大量易於理解的寶貴資訊。
## 先決條件
在我們開始更改資料透視表的來源資料之前，讓我們確保您已完成所有設定並準備就緒：
1. Visual Studio：確保您已安裝 Microsoft Visual Studio 的副本，因為我們將在這裡編寫程式碼。
2. Aspose.Cells 庫：您需要下載 Aspose.Cells 庫並在專案中引用。你可以下載它 [這裡](https://releases。aspose.com/cells/net/).
3. C# 基礎知識：雖然本教學比較簡化，但掌握 C# 將幫助您更好地理解程式碼。
4. Excel 檔案：您應該有一個範例 Excel 檔案（如「Book1.xlsx」），其中包含我們可以操作的資料透視表。
好了，檢查完這些先決條件後，我們可以繼續導入必要的套件並開始編碼！
## 導入包
首先，讓我們導入我們需要的套件。在 Visual Studio 中開啟您的 C# 項目，並在程式碼檔案頂部新增以下使用指令：
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
這些命名空間將使您能夠存取處理 Excel 檔案和使用 Aspose.Cells 操作其內容所需的基本類別。

現在，讓我們將這個過程分解為易於管理的步驟。我們將逐步介紹如何開啟 Excel 檔案、修改工作表、變更資料透視表的資料來源以及儲存結果。
## 步驟 1：定義文件目錄
首先，您需要指定 Excel 檔案的位置。修改 `dataDir` 變數指向包含“Book1.xlsx”的資料夾。
```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory";
```
此行設定了儲存 Excel 檔案的目錄，以便日後更容易存取。
## 步驟2：指定輸入路徑
接下來，讓我們建立一個字串來指定輸入 Excel 檔案的完整路徑：
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
這有助於簡化您的文件存取；您不必在整個程式碼中多次輸入相同的路徑。
## 步驟3：建立文件流
現在是時候開啟 Excel 文件了。我們將創建一個 `FileStream` 它可以讓你讀取 Excel 檔案的內容：
```csharp
// 建立包含要開啟的 Excel 檔案的檔案流
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
此行以讀取模式開啟文件，允許我們存取其資料。
## 步驟 4：載入工作簿
有了文件流後，下一步就是載入工作簿：
```csharp
// 透過檔案流程開啟Excel文件
Workbook workbook = new Workbook(fstream);
```
此命令獲取您的 Excel 文件並將其加載到 `Workbook` 目的。加載後，您可以根據需要操作該文件。
## 步驟 5：訪問工作表
是時候深入探討細節了。我們將存取工作簿中的第一個工作表：
```csharp
// 存取 Excel 文件中的第一個工作表
Worksheet worksheet = workbook.Worksheets[0];
```
這使您可以直接存取第一個工作表中的數據，從而輕鬆進行修改。
## 步驟 6：填入新數據
接下來，我們要將新資料插入儲存格。在此範例中，我們將添加一些範例資料：
```csharp
// 將新資料填入工作表儲存格
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
在這裡，我們輸入值「Golf」、「Qtr4」和 `7000` 進入特定的細胞。您可以根據自己的需求變更這些值。
## 步驟 7：更改命名範圍
現在，我們將更改資料透視表所引用的命名範圍。這涉及創建或更新範圍：
```csharp
// 更改命名範圍“DataSource”
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
透過定義新的範圍，我們確保資料透視表在刷新時使用這些新資料。
## 步驟8：儲存修改後的Excel文件
完成所有更改後，保存您的工作至關重要！讓我們儲存修改後的工作簿：
```csharp
// 儲存修改後的 Excel 文件
workbook.Save(dataDir + "output.xls");
```
此命令將工作簿儲存到新文件，因此除非您願意，否則不會覆蓋原始文件！
## 步驟9：關閉文件流
最後，必須關閉文件流以釋放正在使用的任何資源：
```csharp
// 關閉文件流以釋放所有資源
fstream.Close();
```
此步驟可確保您的應用程式不會洩漏記憶體並保持高效率。
## 結論
恭喜！您剛剛使用 Aspose.Cells 在 .NET 中以程式設計方式成功變更了資料透視表的來源資料。此功能為自動化 Excel 任務和改進工作流程開啟了許多可能性。無論您是在更新財務報告、追蹤銷售數據，還是只是處理數據集，以程式設計方式執行這些操作的能力都可以為您節省大量時間並降低出錯的風險。

## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的 .NET 程式庫，用於處理 Excel 文件，允許使用者以程式設計方式建立、修改和操作 Excel 文件。
### 我可以使用此方法更改現有資料透視表的來源資料嗎？
絕對地！此方法可讓您更新 Excel 工作簿中現有資料透視表的資料來源。
### 我需要安裝 Office 使用 Aspose.Cells 嗎？
沒有！ Aspose.Cells 是一個獨立的函式庫，這表示您不需要安裝 Microsoft Office 即可處理 Excel 檔案。
### Aspose.Cells 可以免費使用嗎？
Aspose.Cells 提供免費試用版，但要獲得完整功能，您必須購買授權。您可以找到詳細信息 [這裡](https://purchase。aspose.com/buy).
### 在哪裡可以找到更多範例和支援？
如需更多範例和支持，請查看 [Aspose.Cells 文檔](https://reference.aspose.com/cells/net/) 以及他們的社群論壇 [這裡](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}