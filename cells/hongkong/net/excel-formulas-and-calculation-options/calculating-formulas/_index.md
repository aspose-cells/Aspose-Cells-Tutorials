---
title: 以程式設計方式計算 Excel 中的公式
linktitle: 以程式設計方式計算 Excel 中的公式
second_title: Aspose.Cells .NET Excel 處理 API
description: 使用 Aspose.Cells for .NET 自動執行 Excel 任務。在這個綜合教程中學習以程式設計計算公式。
weight: 11
url: /zh-hant/net/excel-formulas-and-calculation-options/calculating-formulas/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 以程式設計方式計算 Excel 中的公式

## 介紹
在當今數據驅動的世界中，自動化任務可以節省時間並提高效率，尤其是在處理電子表格時。如果您曾經在 Excel 中處理過複雜的公式，您就會知道正確處理它是多麼重要。透過使用 Aspose.Cells for .NET，您可以以程式設計方式計算公式並輕鬆管理您的 Excel 檔案。在本教程中，我們將逐步介紹建立 Excel 檔案、新增值和公式，然後使用一些 C# 計算這些公式所涉及的每個步驟。讓我們深入了解一下吧！
## 先決條件
在我們開始之前，您需要確保準備好以下幾件事：
1. 開發環境：確保您擁有 Visual Studio 或任何其他可以執行 .NET 應用程式的 C# 環境。
2.  Aspose.Cells for .NET：下載並安裝 Aspose.Cells 函式庫。您可以從[阿斯普斯網站](https://releases.aspose.com/cells/net/).
3. C# 的基本了解：C# 的基礎知識將幫助您掌握我們將使用的概念和程式碼片段。
4. .NET Framework：確保您的電腦上安裝了適當版本的 .NET Framework。
5.  Aspose.Cells 許可證：如果您想在免費試用期之外使用它，請考慮獲取[臨時執照](https://purchase.aspose.com/temporary-license/).
現在我們已經準備好了一切，讓我們進入程式碼並逐步分解它！
## 導入包
在編寫任何程式碼之前，請確保在 C# 檔案中匯入 Aspose.Cells 所需的命名空間：
```csharp
using System.IO;
using Aspose.Cells;
```
這允許您存取 Aspose.Cells 庫提供的功能來操作 Excel 檔案。
## 步驟1：設定文檔目錄
首先定義要儲存 Excel 文件的路徑。必須確保該目錄存在，如果不存在則建立它。
```csharp
//文檔目錄的路徑
string dataDir = "Your Document Directory";
//建立目錄（如果尚不存在）
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
在此步驟中，您將檢查該目錄是否存在。如果沒有，那麼您正在創建它。這個簡單的步驟有助於避免稍後嘗試儲存 Excel 檔案時發生錯誤。
## 第 2 步：實例化工作簿對象
## 建立新工作簿
現在您的目錄已設置，讓我們建立一個代表您的 Excel 檔案的 Workbook 物件：
```csharp
//實例化 Workbook 物件
Workbook workbook = new Workbook();
```
該行只是在記憶體中建立一個新的工作簿。將其視為開啟一個空白 Excel 文件，您可以在其中開始新增資料和公式。
## 第 3 步：新增工作表
## 使用工作表
在我們的工作簿中，我們想要新增一個新的工作表，我們可以在其中操作資料。其操作方法如下：
```csharp
//將新工作表新增至 Excel 對象
int sheetIndex = workbook.Worksheets.Add();
//透過傳遞工作表索引來取得新新增的工作表的引用
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
首先，新增一個工作表，它將自動為您提供該工作表的索引。接下來，您透過索引檢索該工作表。這就像在 Excel 工作簿中開啟一個新分頁！
## 第 4 步：將值插入儲存格
## 填充數據
現在我們已經建立了工作表，我們需要在其中添加一些資料：
```csharp
//為「A1」儲存格新增值
worksheet.Cells["A1"].PutValue(1);
//在「A2」儲存格中新增值
worksheet.Cells["A2"].PutValue(2);
//在「A3」儲存格中新增值
worksheet.Cells["A3"].PutValue(3);
```
在此步驟中，您將向工作表的前三個儲存格（A1、A2、A3）插入值。此操作類似於直接在 Excel 工作表中鍵入值。 
## 第 5 步：新增公式
## 對值求和
輸入值後，需要新增一個公式來計算這些儲存格的總和。方法如下：
```csharp
//將 SUM 公式新增至「A4」儲存格
worksheet.Cells["A4"].Formula = "=SUM(A1:A3)";
```
此行程式碼將 SUM 公式附加到儲存格 A4，該公式將對 A1 到 A3 的值求和。這就像在 Excel 中編寫公式一樣，但是以程式設計方式編寫！
## 第6步：計算公式
## 執行計算
現在到了關鍵時刻！我們需要計算輸入公式的結果：
```csharp
//計算公式的結果
workbook.CalculateFormula();
```
透過致電`CalculateFormula()`，您告訴工作簿處理其中的所有公式。這類似於在 Excel 儲存格中鍵入公式後按下「Enter」鍵。
## 步驟 7：檢索計算值
## 讀取結果
公式計算完成後，我們可以從 A4 擷取值：
```csharp
//取得單元格的計算值
string value = worksheet.Cells["A4"].Value.ToString();
```
在此步驟中，您將取得 SUM 公式的結果。這將為您提供 1 + 2 + 3 的總和，即 6！
## 步驟 8：儲存 Excel 文件
## 寫入磁碟
最後，將工作簿儲存到指定目錄，以便稍後存取：
```csharp
//儲存 Excel 文件
workbook.Save(dataDir + "output.xls");
```
此程式碼將您的 Excel 檔案保存在您指定的目錄中，名稱為「output.xls」。這就像在 Excel 中點擊「另存為」並選擇檔案的儲存位置。
## 結論
在本教學中，我們介紹如何使用 Aspose.Cells for .NET 以程式設計方式建立 Excel 檔案。從新增值和公式到計算和保存最終輸出，我們逐步完成了每個關鍵步驟，確保您為未來的自動化奠定堅實的基礎。
## 常見問題解答
### 什麼是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一個函式庫，可讓開發人員以程式設計方式操作 .NET 應用程式中的 Excel 文件。
### 我可以使用 Aspose.Cells 計算 Excel 中的公式嗎？
是的！您可以使用 Aspose.Cells 來計算和評估公式，就像在 Excel 中一樣。
### Aspose.Cells 是否有免費試用版？
絕對地！您可以獲得免費試用[這裡](https://releases.aspose.com/).
### 我可以使用 Aspose.Cells 操作現有的 Excel 檔案嗎？
是的，Aspose.Cells 允許您載入現有的 Excel 檔案並根據需要修改它們。
### 在哪裡可以找到有關 Aspose.Cells for .NET 的更多文件？
您可以找到全面的文檔[這裡](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
