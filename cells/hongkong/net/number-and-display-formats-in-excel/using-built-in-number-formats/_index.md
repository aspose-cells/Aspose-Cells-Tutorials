---
"description": "使用 Aspose.Cells for .NET 自動執行 Excel 中的數字格式化。了解如何以程式設計方式套用日期、百分比和貨幣格式。"
"linktitle": "以程式設計方式使用 Excel 內建的數位格式"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "以程式設計方式使用 Excel 內建的數位格式"
"url": "/zh-hant/net/number-and-display-formats-in-excel/using-built-in-number-formats/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 以程式設計方式使用 Excel 內建的數位格式

## 介紹
在本教學中，我們將引導您了解如何使用 Aspose.Cells for .NET 在 Excel 中使用內建數位格式。我們將涵蓋從設定環境到應用不同格式（如日期、百分比和貨幣）的所有內容。無論您是經驗豐富的專業人士還是剛剛涉足 .NET 生態系統，本指南都將幫助您輕鬆格式化 Excel 單元格。
## 先決條件
在深入研究之前，請確保您已具備以下條件：
- 已安裝 Aspose.Cells for .NET 函式庫。你可以 [點此下載](https://releases。aspose.com/cells/net/).
- 具備 C# 和基本 .NET 程式設計的工作知識。
- 您的機器上安裝了 Visual Studio 或任何 .NET IDE。
- 有效的 Aspose 許可證或 [臨時執照](https://purchase。aspose.com/temporary-license/).
- 安裝了.NET框架（4.0或更高版本）。
  
如果您缺少上述任何內容，請按照提供的連結進行設定。準備好？讓我們進入有趣的部分吧！
## 導入包
在開始本教學之前，請確保匯入使用 Aspose.Cells for .NET 所需的命名空間：
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
一旦匯入了這些內容，您就可以以程式方式操作 Excel 檔案了。現在，讓我們深入了解逐步指南！
## 步驟 1：建立或存取您的 Excel 工作簿
在此步驟中，您將建立一個新的工作簿。將其視為開啟一個新的 Excel 文件，只不過您是透過程式碼來完成的！
```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory";
// 如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// 實例化 Workbook 物件
Workbook workbook = new Workbook();
```
這裡我們只是實例化了一個新的 `Workbook` 目的。這充當您的 Excel 文件，可供進行資料操作。您也可以透過提供其路徑來載入現有文件。
## 第 2 步：訪問工作表
Excel 工作簿可以包含多個工作表。在此步驟中，我們將存取工作簿中的第一個工作表：
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
我們現在正在存取工作簿中的第一個工作表。如果您需要操作其他工作表，則可以使用它們的索引或名稱來引用它們。
## 步驟 3：向單元格新增數據
讓我們開始在特定單元格上添加一些資料。首先，我們將目前系統日期插入儲存格「A1」：
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
此行將目前日期插入儲存格 A1。很酷吧？想像一下手動對數百個單元格執行此操作 - 這將是一場噩夢。現在，我們繼續進行格式化！
## 步驟 4：在儲存格「A1」中設定日期格式
接下來，讓我們以更易讀的格式格式化該日期，例如「15-Oct-24」。這就是 Aspose.Cells 真正閃耀的地方：
1. 檢索單元格的樣式：
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
在這裡，我們取得儲存格 A1 的樣式。可以將其視為在進行任何調整之前掌握細胞的“時尚”。
2.設定日期格式：
```csharp
style.Number = 15;
```
設定 `Number` 屬性設定為 15 則套用所需的日期格式。這是一個內建的數字格式代碼，用於以“d-mmm-yy”格式顯示日期。
3. 將樣式套用至儲存格：
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
此行將樣式變更套用至儲存格。現在，您將看到更用戶友好的日期格式，而不是預設的日期格式，例如「15-Oct-24」。
## 步驟 5：在儲存格「A2」中新增並設定百分比格式
讓我們繼續討論百分比的格式化。假設您想要插入一個值並將其顯示為百分比。在此步驟中，我們將向儲存格「A2」新增一個數值並將其格式化為百分比：
1. 插入數值：
```csharp
worksheet.Cells["A2"].PutValue(20);
```
這會將數字 20 插入到儲存格 A2 中。您可能會想，「這只是一個簡單的數字——我怎麼才能將其轉換為百分比？」好吧，我們即將談到這一點。
2. 檢索樣式並設定百分比格式：
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // 格式為百分比
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
在這裡，我們將 2546 新增到儲存格 A3。接下來，我們將格式化該數字以顯示為貨幣。
2. 檢索樣式並設定貨幣格式：
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // 格式化為貨幣
worksheet.Cells["A3"].SetStyle(style);
```
設定 `Number` 屬性為 6 應用貨幣格式。現在，儲存格 A3 中的值將顯示為“2,546.00”，帶有逗號和兩位小數。
## 步驟 7：儲存 Excel 文件
現在我們已經套用了所有的格式化魔法，是時候儲存檔案了：
```csharp
// 儲存 Excel 文件
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
此行將 Excel 檔案儲存為 Excel 97-2003 格式。您可以更改 `SaveFormat` 以滿足您的需求。就這樣，您已經以程式設計方式建立並格式化了 Excel 檔案！
## 結論
恭喜！您已成功學習如何使用 Aspose.Cells for .NET 將內建數位格式套用至 Excel 檔案中的儲存格。從日期到百分比和貨幣，我們涵蓋了 Excel 資料處理中一些最常見的格式需求。現在，您無需手動設定儲存格格式，而是可以自動執行整個過程，從而節省時間並減少錯誤。
## 常見問題解答
### 我可以使用 Aspose.Cells for .NET 應用自訂數字格式嗎？
是的！除了內建格式外，Aspose.Cells 還支援自訂數位格式。您可以使用 `Custom` 財產 `Style` 班級。
### 如何將儲存格格式化為具有特定符號的貨幣？
要套用特定的貨幣符號，您可以透過設定 `Style.Custom` 財產。
### 我可以格式化整行或整列嗎？
絕對地！您可以使用 `Rows` 或者 `Columns` 收藏品 `Worksheet` 目的。
### 如何一次格式化多個儲存格？
您可以使用 `Range` 物件來選擇多個單元格並一次將樣式應用於它們。
### 我需要安裝 Microsoft Excel 才能使用 Aspose.Cells 嗎？
不，Aspose.Cells 獨立於 Microsoft Excel 運行，因此您不需要在機器上安裝 Excel。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}