---
title: 以程式設計方式使用 Excel 內建的數位格式
linktitle: 以程式設計方式使用 Excel 內建的數位格式
second_title: Aspose.Cells .NET Excel 處理 API
description: 使用 Aspose.Cells for .NET 在 Excel 中自動設定數字格式。了解如何以程式設計方式套用日期、百分比和貨幣格式。
weight: 10
url: /zh-hant/net/number-and-display-formats-in-excel/using-built-in-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 以程式設計方式使用 Excel 內建的數位格式

## 介紹
在本教學中，我們將引導您了解如何使用 Aspose.Cells for .NET 在 Excel 中使用內建數位格式。我們將涵蓋從設定環境到套用不同格式（例如日期、百分比和貨幣）的所有內容。無論您是經驗豐富的專業人士還是剛涉足 .NET 生態系統，本指南都將幫助您輕鬆設定 Excel 儲存格格式。
## 先決條件
在投入之前，請確保您具備以下條件：
- 安裝了 Aspose.Cells for .NET 函式庫。你可以[在這裡下載](https://releases.aspose.com/cells/net/).
- 具備 C# 和基本 .NET 程式設計的應用知識。
- Visual Studio 或電腦上安裝的任何 .NET IDE。
- 有效的 Aspose 許可證或[臨時執照](https://purchase.aspose.com/temporary-license/).
- 已安裝 .NET Framework（版本 4.0 或更高版本）。
  
如果您缺少上述任何一項，請按照提供的連結進行所有設定。準備好？讓我們進入有趣的部分吧！
## 導入包
在開始學習本教學之前，請確保導入使用 Aspose.Cells for .NET 所需的命名空間：
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
匯入這些檔案後，您就可以以程式方式操作 Excel 檔案了。現在，讓我們深入了解逐步指南！
## 第 1 步：建立或存取您的 Excel 工作簿
在此步驟中，您將建立一個新工作簿。將此視為開啟一個新的 Excel 文件，只不過您是透過程式碼執行此操作！
```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
//如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
//實例化 Workbook 物件
Workbook workbook = new Workbook();
```
在這裡，我們只是實例化一個新的`Workbook`目的。這充當您的 Excel 文件，準備好進行資料操作。您也可以透過提供現有文件的路徑來載入該文件。
## 第 2 步：訪問工作表
Excel 工作簿可以包含多個工作表。在此步驟中，我們將存取工作簿中的第一個工作表：
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
我們現在正在存取工作簿中的第一個工作表。如果您需要操作其他工作表，您可以使用它們的索引或名稱來引用它們。
## 第 3 步：將資料新增至儲存格
讓我們開始在特定單元格上添加一些資料。首先，我們將目前系統日期插入儲存格「A1」：
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
此行將目前日期插入儲存格 A1。很酷，對吧？想像一下對數百個單元手動執行此操作 - 這將是一場噩夢。現在，我們將繼續格式化！
## 步驟 4：設定儲存格「A1」中的日期格式
接下來，讓我們將該日期設定為更易讀的格式，例如「15-Oct-24」。這就是 Aspose.Cells 真正閃光的地方：
1. 檢索單元格的樣式：
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
在這裡，我們取得儲存格 A1 的樣式。可以將其視為在進行任何調整之前抓住細胞的“時尚”。
2. 設定日期格式：
```csharp
style.Number = 15;
```
設定`Number`屬性設定為 15 應用所需的日期格式。這是一個內建的數字格式代碼，用於以“d-mmm-yy”格式顯示日期。
3. 將樣式套用到儲存格：
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
此行將樣式變更套用至儲存格。現在，您將看到更用戶友好的格式，例如“15-Oct-24”，而不是預設的日期格式。
## 步驟 5：在儲存格「A2」中新增百分比並設定其格式
讓我們繼續格式化百分比。想像一下您想要插入一個值並將其顯示為百分比。在此步驟中，我們將向儲存格「A2」新增一個數值並將其格式化為百分比：
1. 插入數值：
```csharp
worksheet.Cells["A2"].PutValue(20);
```
這會將數字 20 插入儲存格 A2 中。您可能會想，“這只是一個簡單的數字——我如何將其轉換為百分比？”好吧，我們即將談到這一點。
2. 檢索樣式並設定百分比格式：
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  //格式為百分比
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
style.Number = 6;  //格式為貨幣
worksheet.Cells["A3"].SetStyle(style);
```
設定`Number`屬性 6 應用貨幣格式。現在，儲存格 A3 中的值將顯示為“2,546.00”，包含逗號和兩位小數。
## 步驟 7：儲存 Excel 文件
現在我們已經應用了所有格式化魔法，是時候儲存檔案了：
```csharp
//儲存 Excel 文件
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
此行以 Excel 97-2003 格式儲存 Excel 檔案。您可以更改`SaveFormat`以滿足您的需求。就像這樣，您已經以程式設計方式建立並格式化了 Excel 檔案！
## 結論
恭喜！您已成功學習如何使用 Aspose.Cells for .NET 將內建數位格式套用到 Excel 檔案中的儲存格。從日期到百分比和貨幣，我們介紹了 Excel 資料處理的一些最常見的格式設定需求。現在，您可以自動化整個過程，而不是手動設定單元格格式，從而節省時間並減少錯誤。
## 常見問題解答
### 我可以使用 Aspose.Cells for .NET 應用自訂數字格式嗎？
是的！除了內建格式之外，Aspose.Cells 還支援自訂數位格式。您可以使用以下命令建立高度特定的格式`Custom`財產在`Style`班級。
### 如何將儲存格格式化為具有特定符號的貨幣？
若要套用特定的貨幣符號，您可以透過設定來使用自訂格式`Style.Custom`財產。
### 我可以格式化整行或整列嗎？
絕對地！您可以使用下列命令將樣式套用至整行或整列`Rows`或者`Columns`收藏於`Worksheet`目的。
### 如何一次格式化多個儲存格？
您可以使用`Range`物件選擇多個單元格並一次將樣式應用於它們。
### 我需要安裝 Microsoft Excel 才能使用 Aspose.Cells 嗎？
不需要，Aspose.Cells 獨立於 Microsoft Excel 工作，因此您不需要在電腦上安裝 Excel。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
