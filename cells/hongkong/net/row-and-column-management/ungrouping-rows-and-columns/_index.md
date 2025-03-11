---
title: 使用 Aspose.Cells 在 Excel 中取消行和列的分組
linktitle: 使用 Aspose.Cells 在 Excel 中取消行和列的分組
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過這份綜合指南，了解如何使用 Aspose.Cells for .NET 在 Excel 中取消行和列的分組。簡化 Excel 資料操作。
weight: 15
url: /zh-hant/net/row-and-column-management/ungrouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 在 Excel 中取消行和列的分組

## 介紹
在處理 Excel 檔案時，您可能會發現自己需要取消行和列的分組。無論您是清理電子表格還是重新格式化資料以實現更好的演示，Aspose.Cells for .NET 都是一款出色的工具，可以簡化流程。在本教學中，我將指導您完成使用 Aspose.Cells 在 Excel 中取消行和列分組的步驟。最後，您將深入了解如何以程式設計方式處理 Excel 檔案。
## 先決條件
在深入研究程式碼之前，讓我們確保您已完成所有設定。這是您需要的：
1.  Visual Studio：您的電腦上應該安裝有 Visual Studio 的工作版本。如果您還沒有，您可以從以下位置下載[Visual Studio 的網站](https://visualstudio.microsoft.com/).
2. Aspose.Cells for .NET：您需要下載 Aspose.Cells 函式庫。您可以從[Aspose 發佈頁面](https://releases.aspose.com/cells/net/)。確保您擁有必要的許可證，這些許可證可以透過購買或取得[臨時執照](https://purchase.aspose.com/temporary-license/).
3. C# 基礎知識：對 C# 程式設計的基本了解將幫助您更輕鬆地進行操作。
一旦一切準備就緒，我們就可以進入有趣的部分：程式碼！
## 導入包
首先，您需要在 C# 專案中匯入必要的套件。操作方法如下：
1. 在 Visual Studio 中開啟您的專案。
2. 新增對 Aspose.Cells 庫的引用。您可以透過右鍵單擊項目中的“引用”並選擇“新增引用”來完成此操作。瀏覽至儲存 Aspose.Cells DLL 的位置。
3. 在 C# 檔案的頂部，加入以下 using 指令：
```csharp
using System.IO;
using Aspose.Cells;
```
現在一切都已設定完畢，讓我們逐步完成在 Excel 工作表中取消行和列分組的步驟。 
## 第 1 步：定義文檔目錄
首先，您需要指定 Excel 檔案所在的目錄。您可以如下進行設定：
```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
```
代替`"Your Document Directory"`與您電腦上儲存 Excel 檔案的實際路徑。 
## 步驟2：建立檔案流
接下來，您需要建立文件流程來開啟 Excel 文件。您可以這樣做：
```csharp
//建立包含要開啟的 Excel 檔案的檔案流
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
在這裡，您將開啟名為的文件`book1.xls`。確保該檔案存在於您指定的目錄中，否則您將遇到檔案未找到的錯誤。
## 第 3 步：實例化工作簿對象
現在，讓我們將 Excel 檔案載入到 Workbook 物件中。這允許您以程式設計方式操作工作簿：
```csharp
//實例化 Workbook 物件
//透過檔案流程開啟Excel文件
Workbook workbook = new Workbook(fstream);
```
透過這行程式碼，您已成功將 Excel 檔案載入到記憶體中並準備好使用它。
## 第 4 步：訪問工作表
取得工作簿後，下一步是存取要取消行和列分組的特定工作表。具體做法如下：
```csharp
//存取 Excel 文件中的第一個工作表
Worksheet worksheet = workbook.Worksheets[0];
```
在本例中，我們正在存取第一個工作表。如果您的資料位於不同的工作表上，您可以相應地變更索引。
## 第 5 步：取消行分組
現在到了令人興奮的部分！讓我們取消前六行的分組（從第 0 行到第 5 行）。使用以下程式碼：
```csharp
//取消前六行的分組（從 0 到 5）
worksheet.Cells.UngroupRows(0, 5);
```
此方法刪除已套用於指定行的任何分組。就這麼簡單！
## 第 6 步：取消列分組
就像行一樣，您也可以取消列的分組。以下是取消前三列（從第 0 列到第 2 列）分組的方法：
```csharp
//取消前三列的分組（從 0 到 2）
worksheet.Cells.UngroupColumns(0, 2);
```
## 步驟7：儲存修改後的Excel文件
取消行和列的分組後，下一步是將變更儲存回 Excel 檔案。您可以使用`Save`方法：
```csharp
//儲存修改後的Excel文件
workbook.Save(dataDir + "output.xls");
```
在此範例中，我們將修改後的檔案另存為`output.xls`。您可以將檔案名稱變更為您喜歡的任何名稱。
## 步驟8：關閉文件流
最後，要釋放資源，您應該關閉文件流：
```csharp
//關閉文件流以釋放所有資源
fstream.Close();
```
這是一個很好的做法，可以確保您的應用程式保留檔案句柄的時間不會超過必要的時間。
## 結論
現在你就擁有了！您已成功學習如何使用 Aspose.Cells for .NET 在 Excel 檔案中取消行和列的分組。只需幾行程式碼，您就可以透過程式設計方式對 Excel 檔案進行重大變更。無論您是自動化報告還是準備分析數據，掌握這些技術都可以為您節省大量時間。
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的程式庫，用於在 .NET 應用程式中處理 Excel 文件，從而可以輕鬆操作、轉換和建立電子表格。
### 我可以使用其他庫在 Excel 中取消行和列的分組嗎？
是的，還有其他函式庫可用於 .NET 中的 Excel 操作，但 Aspose.Cells 提供了廣泛的功能和易用性。
### 儲存後有辦法撤銷更改嗎？
儲存 Excel 檔案後，除非您有原始檔案的備份，否則無法還原先前的狀態。
### 我如何獲得 Aspose.Cells 的支援？
您可以透過訪問尋求支持[Aspose 支援論壇](https://forum.aspose.com/c/cells/9)，您可以在其中提出問題並找到解決方案。
### 我可以在沒有許可證的情況下使用 Aspose.Cells 嗎？
是的，您可以免費使用 Aspose.Cells，但有一定的限制，並且您可以從[臨時執照](https://purchase.aspose.com/temporary-license/)以獲得完整的功能。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
