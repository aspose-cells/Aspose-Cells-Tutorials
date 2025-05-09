---
"description": "在本詳細教學中了解如何使用 Aspose.Cells for .NET 讀取 Numbers 電子表格並將其轉換為 PDF。"
"linktitle": "在 .NET 中以程式設計方式讀取數位電子表格"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 .NET 中以程式設計方式讀取數位電子表格"
"url": "/zh-hant/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以程式設計方式讀取數位電子表格

## 介紹
在當今的數位世界中，資料管理是一項至關重要的技能，而電子表格則處於資料組織的最前線。但是如果您需要使用 .NET 來處理 Numbers 電子表格（由 Apple 的 Numbers 應用程式建立的檔案）該怎麼辦？不用擔心;你並不孤單！在本教程中，我們將介紹使用 Aspose.Cells for .NET 以程式設計方式讀取 Numbers 電子表格的過程。您將學習如何載入 Numbers 檔案並將其轉換為 PDF。
## 先決條件
在我們開始之前，您需要做好以下幾點：
1. Aspose.Cells for .NET：請確保您已安裝 Aspose.Cells 函式庫。你可以下載它 [這裡](https://releases。aspose.com/cells/net/).
2. Visual Studio：建議在您的機器上安裝 Visual Studio（或任何其他與 .NET 相容的 IDE）。
3. C# 基礎：稍微熟悉一下 C# 程式設計將有助於您順利完成學習。
4. 您的文件目錄：您需要一個儲存 Numbers 檔案的目錄，以及一個儲存轉換後的 PDF 的位置。
一旦滿足了這些先決條件，您就可以開始了！
## 導入包
首先，我們需要將必要的套件匯入到我們的 C# 專案中。這是至關重要的一步，因為它使我們能夠利用 Aspose.Cells 庫提供的功能。
1. 在 Visual Studio 中開啟您的 C# 專案。
2. 新增對 Aspose.Cells 庫的引用：
   - 如果您使用 NuGet，只需在套件管理器控制台中執行以下命令：
```
 Install-Package Aspose.Cells
 ```
3. 在程式碼中匯入必要的命名空間：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
現在我們已經匯入了必要的套件，讓我們繼續逐步指導如何讀取 Numbers 電子表格。
## 步驟 1：指定來源目錄和輸出目錄
在此步驟中，我們將設定來源 Numbers 檔案所在的目錄以及您想要儲存輸出 PDF 的位置。
```csharp
// 來源目錄
string sourceDir = "Your Document Directory"; // 將其更新為您的實際目錄
// 輸出目錄
string outputDir = "Your Document Directory"; // 將其更新為您的實際目錄
```
這裡我們定義了兩個字串變量， `sourceDir` 和 `outputDir`，指定輸入和輸出檔案的位置。確保更換 `"Your Document Directory"` 使用系統上的實際路徑。
## 步驟 2：設定數字格式的載入選項
接下來，我們將指定讀取 Numbers 電子表格的載入選項。此步驟至關重要，因為它告訴 Aspose 如何解釋 Numbers 檔案。
```csharp
// 指定載入選項；我們要載入 Numbers 電子表格
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
我們創建了一個 `LoadOptions` 物件並指定格式為 `LoadFormat.Numbers`。這告訴 Aspose.Cells 庫我們正在處理 Numbers 檔案。 
## 步驟 3：將 Numbers 電子表格載入到工作簿中
現在，是時候將實際的 Numbers 電子表格載入到 `Workbook` 目的。
```csharp
// 使用上述載入選項將 Numbers 電子表格載入到工作簿中
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
我們實例化一個 `Workbook` 物件並傳遞 Numbers 檔案的檔案路徑以及我們的載入選項。確保檔案名稱（`sampleNumbersByAppleInc.numbers`) 與 Numbers 檔案的實際名稱相符。
## 步驟 4：將工作簿儲存為 PDF
一旦 Numbers 檔案成功加載，下一步就是將其儲存為不同的格式 - 具體來說，是 PDF。
```csharp
// 將工作簿儲存為 PDF 格式
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
在這裡，我們稱 `Save` 方法 `Workbook` 對象，指定輸出檔案路徑和我們想要儲存的格式。在本例中，我們將其儲存為 PDF。確保輸出檔名（`outputNumbersByAppleInc.pdf`) 是唯一的，並且不會覆蓋任何現有文件。
## 步驟5：確認成功
最後，讓我們添加一條訊息來確認我們的操作成功。
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
一旦一切完成，這行程式碼將會在控制台上列印一條成功訊息。得到回饋總是好的，對吧？
## 結論
就是這樣！您已成功讀取 Numbers 電子表格並使用 Aspose.Cells for .NET 將其轉換為 PDF。這個強大的庫可以讓您毫不費力地操作電子表格，讓您的資料管理任務變得輕而易舉。無論您是在開發應用程式還是只需要更有效地處理電子表格，Aspose.Cells 都是您工具包中必備的絕佳工具。
## 常見問題解答
### Aspose.Cells 可以讀取哪些類型的檔案？  
Aspose.Cells 可以讀取多種檔案格式，包括 XLS、XLSX、CSV 和 Numbers 檔案。 
### 我可以使用 Aspose.Cells 編輯 Numbers 檔案嗎？  
是的，您可以使用 Aspose.Cells 讀取、操作和儲存 Numbers 檔案。
### Aspose.Cells 可以免費使用嗎？  
Aspose.Cells 提供免費試用，但您需要許可證才能延長使用時間。查看價格 [這裡](https://purchase。aspose.com/buy).
### 如果在載入 Numbers 檔案時遇到錯誤，該怎麼辦？  
確保您使用正確的載入選項並且檔案路徑準確。如需更多支持，請訪問 [Aspose 支援論壇](https://forum。aspose.com/c/cells/9).
### 如何取得 Aspose.Cells 的臨時授權？  
您可以申請臨時駕照 [這裡](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}