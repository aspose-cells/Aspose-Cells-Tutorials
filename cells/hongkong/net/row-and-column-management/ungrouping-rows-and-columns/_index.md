---
"description": "透過本綜合指南了解如何使用 Aspose.Cells for .NET 取消 Excel 中的行和列的組合。簡化您的 Excel 資料操作。"
"linktitle": "使用 Aspose.Cells 在 Excel 中取消行和列的分組"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "使用 Aspose.Cells 在 Excel 中取消行和列的分組"
"url": "/zh-hant/net/row-and-column-management/ungrouping-rows-and-columns/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 在 Excel 中取消行和列的分組

## 介紹
在處理 Excel 檔案時，您可能會遇到需要取消組合行和列的情況。無論您是清理電子表格還是重新格式化資料以獲得更好的呈現效果，Aspose.Cells for .NET 都是一款可以簡化流程的出色工具。在本教學中，我將指導您完成使用 Aspose.Cells 在 Excel 中取消分組行和列的步驟。最後，您將對如何以程式設計方式處理 Excel 文件有深入的了解。
## 先決條件
在深入研究程式碼之前，請確保您已完成所有設定。您需要準備以下物品：
1. Visual Studio：您的機器上應該安裝了 Visual Studio 的工作版本。如果你還沒有，你可以從 [Visual Studio 的網站](https://visualstudio。microsoft.com/).
2. Aspose.Cells for .NET：您需要下載 Aspose.Cells 函式庫。您可以從 [Aspose 發佈頁面](https://releases.aspose.com/cells/net/)。確保您擁有必要的許可證，這些許可證可以購買或透過 [臨時執照](https://purchase。aspose.com/temporary-license/).
3. C# 基礎知識：對 C# 程式設計的基本了解將幫助您更輕鬆地跟上進度。
一旦一切準備就緒，我們就可以進入有趣的部分：程式碼！
## 導入包
首先，您需要在 C# 專案中匯入必要的套件。以下是操作方法：
1. 在 Visual Studio 中開啟您的專案。
2. 新增對 Aspose.Cells 庫的引用。您可以透過右鍵單擊項目中的引用並選擇新增引用來執行此操作。瀏覽至儲存 Aspose.Cells DLL 的位置。
3. 在 C# 檔案的頂部，新增以下使用指令：
```csharp
using System.IO;
using Aspose.Cells;
```
現在一切都已設定完畢，讓我們逐步了解在 Excel 表中取消分組行和列的步驟。 
## 步驟1：定義文檔目錄
首先，您需要指定 Excel 檔案所在的目錄。您可以如下進行設定：
```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory";
```
代替 `"Your Document Directory"` 使用計算機上儲存 Excel 檔案的實際路徑。 
## 步驟2：建立檔案流
接下來，您需要建立一個文件流程來開啟 Excel 文件。你可以這樣做：
```csharp
// 建立包含要開啟的 Excel 檔案的檔案流
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
在這裡，你打開的是名為 `book1.xls`。確保此文件存在於您指定的目錄中，否則您將遇到文件未找到錯誤。
## 步驟 3：實例化工作簿對象
現在，讓我們將 Excel 檔案載入到 Workbook 物件中。這允許您以程式設計方式操作工作簿：
```csharp
// 實例化 Workbook 物件
// 透過檔案流程開啟Excel文件
Workbook workbook = new Workbook(fstream);
```
透過這行程式碼，您已成功將 Excel 檔案載入到記憶體中並準備使用它。
## 步驟 4：訪問工作表
有了工作簿之後，下一步就是存取您想要取消行和列分組的特定工作表。具體操作如下：
```csharp
// 存取 Excel 文件中的第一個工作表
Worksheet worksheet = workbook.Worksheets[0];
```
在這種情況下，我們正在存取第一個工作表。如果您的資料位於不同的工作表上，您可以相應地變更索引。
## 步驟 5：取消行分組
現在到了令人興奮的部分！讓我們取消組合前六行（從第 0 行到第 5 行）。使用以下程式碼：
```csharp
// 取消分組前六行（從 0 到 5）
worksheet.Cells.UngroupRows(0, 5);
```
此方法刪除已套用於指定行的任何分組。就這麼簡單！
## 步驟 6：取消列分組
就像行一樣，您也可以取消列的組合。以下是取消組合前三列（從第 0 列到第 2 列）的方法：
```csharp
// 取消分組前三列（從 0 到 2）
worksheet.Cells.UngroupColumns(0, 2);
```
## 步驟7：儲存修改後的Excel文件
取消分組行和列後，下一步是將變更儲存回 Excel 檔案。您可以使用 `Save` 方法：
```csharp
// 儲存修改後的 Excel 文件
workbook.Save(dataDir + "output.xls");
```
在此範例中，我們將修改後的檔案儲存為 `output.xls`。您可以將檔案名稱變更為您喜歡的任何名稱。
## 步驟8：關閉文件流
最後，為了釋放資源，您應該關閉文件流：
```csharp
// 關閉文件流以釋放所有資源
fstream.Close();
```
這是一個很好的做法，可以確保您的應用程式不會佔用檔案句柄超過必要的時間。
## 結論
就是這樣！您已成功學習如何使用 Aspose.Cells for .NET 取消 Excel 檔案中行和列的分組。只需幾行程式碼，您就可以以程式設計方式對 Excel 檔案進行重大更改。無論您是自動產生報告還是準備分析數據，掌握這些技術都可以為您節省大量時間。
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的程式庫，用於在 .NET 應用程式中處理 Excel 文件，可輕鬆操作、轉換和建立電子表格。
### 我可以使用其他庫取消 Excel 中的行和列的分組嗎？
是的，.NET 中還有其他可用於 Excel 操作的程式庫，但 Aspose.Cells 提供了廣泛的功能和易用性。
### 儲存後有沒有辦法撤銷更改？
一旦儲存了 Excel 文件，除非您有原始文件的備份，否則無法還原到先前的狀態。
### 如何獲得 Aspose.Cells 的支援？
您可以透過造訪以下方式獲得支持 [Aspose 支援論壇](https://forum.aspose.com/c/cells/9)，您可以在這裡提出問題並找到解決方案。
### 我可以在沒有許可證的情況下使用 Aspose.Cells 嗎？
是的，您可以免費使用 Aspose.Cells，但有一定的限制，您可以從 [臨時執照](https://purchase.aspose.com/temporary-license/) 以實現全部功能。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}