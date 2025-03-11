---
title: 使用使用者定義的數字自訂顯示格式
linktitle: 使用使用者定義的數字自訂顯示格式
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 自訂顯示格式。使用此逐步指南設定日期、百分比和貨幣的格式。
weight: 11
url: /zh-hant/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用使用者定義的數字自訂顯示格式

## 介紹
使用 Excel 檔案通常需要自訂儲存格格式，以便以更有意義和使用者友好的方式呈現資料。假設您正在為報表建立 Excel 檔案。您不僅僅想要原始數字。您希望日期、百分比和貨幣看起來時尚而專業，對嗎？這就是自訂顯示格式發揮作用的地方。在本教學中，我們將深入研究 Aspose.Cells for .NET，向您展示如何使用使用者定義的設定自訂數字的顯示格式。
## 先決條件
在開始之前，請確保您已準備好學習本教學所需的一切。這是您需要的：
- 安裝了 Aspose.Cells for .NET。[在這裡下載](https://releases.aspose.com/cells/net/).
- C# 和 .NET 架構的基礎知識。
-  Aspose.Cells 的有效許可證。如果你沒有，請拿一個[免費試用](https://releases.aspose.com/)或請求[臨時執照](https://purchase.aspose.com/temporary-license/).
- 像 Visual Studio 這樣的 IDE。
- .NET Framework 4.0 或更高版本。
如果您缺少任何東西，請不要擔心。您可以隨時重新造訪這些連結來下載必要的文件或尋求協助[Aspose 支援論壇](https://forum.aspose.com/c/cells/9).
## 導入命名空間
在進入程式碼之前，您需要匯入所需的命名空間以存取所有必要的 Aspose.Cells 功能。
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
這兩個命名空間將是本教學中的核心工具。現在，讓我們繼續有趣的部分：
## 第1步：設定項目目錄
首先，您需要一個儲存檔案的地方，對嗎？讓我們建立一個目錄來保存輸出的 Excel 檔案。在此步驟中，我們還將在保存任何內容之前確保該目錄存在。
```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
//如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- 我們定義一個`dataDir`變數來儲存輸出 Excel 檔案的路徑。
- 然後我們使用以下命令檢查目錄是否存在`System.IO.Directory.Exists()`.
- 如果該目錄不存在，將使用以下命令建立該目錄`System.IO.Directory.CreateDirectory()`.
## 步驟 2：建立新工作簿並新增工作表
現在我們已經獲得了目錄，讓我們建立一個新的 Excel 工作簿並向其中新增一個工作表。
```csharp
//實例化 Workbook 物件
Workbook workbook = new Workbook();
//將新工作表新增至 Excel 對象
int i = workbook.Worksheets.Add();
//透過傳遞工作表索引來取得新新增的工作表的引用
Worksheet worksheet = workbook.Worksheets[i];
```
- 首先，我們創建一個新的`Workbook`目的。將此視為您的 Excel 文件。
- 我們使用以下命令向該工作簿新增一個新工作表`Add()`方法並將索引儲存在變數中`i`.
- 我們使用該工作表來引用`workbook.Worksheets[i]`.
## 步驟 3：向儲存格新增日期並自訂其格式
現在，讓我們將當前日期插入到儲存格中，並將其格式化為以自訂方式顯示。我們將設定自訂格式，而不是預設的日期格式`d-mmm-yy`.
```csharp
//將目前系統日期新增至「A1」儲存格
worksheet.Cells["A1"].PutValue(DateTime.Now);
//取得A1單元格的樣式
Style style = worksheet.Cells["A1"].GetStyle();
//設定自訂顯示格式以將日期顯示為“d-mmm-yy”
style.Custom = "d-mmm-yy";
//將樣式套用到 A1 儲存格
worksheet.Cells["A1"].SetStyle(style);
```
- 我們將目前系統日期新增到儲存格中`A1`使用`PutValue(DateTime.Now)`.
- 我們檢索單元格的目前樣式`A1`使用`GetStyle()`.
- 我們透過設定來修改單元格的樣式`style.Custom = "d-mmm-yy"`，它格式化日期以顯示日期、縮寫月份和年份。
- 最後，我們將新樣式套用到儲存格`SetStyle()`.
## 步驟 4：將儲存格格式設定為百分比
接下來，讓我們處理數字。我們將向另一個單元格添加一個數值，例如`A2`，並將其格式化為百分比。
```csharp
//將數值新增至「A2」儲存格
worksheet.Cells["A2"].PutValue(20);
//取得A2單元格的樣式
style = worksheet.Cells["A2"].GetStyle();
//設定自訂顯示格式以將值顯示為百分比
style.Custom = "0.0%";
//將樣式套用到 A2 儲存格
worksheet.Cells["A2"].SetStyle(style);
```
- 我們增加價值`20`到細胞`A2`.
- 我們檢索單元格的樣式`A2`並將自訂格式設為`0.0%`將數值顯示為百分比（即 20%）。
- 最後，我們使用以下命令將樣式套用至儲存格`SetStyle()`.
## 步驟 5：將儲存格格式設定為貨幣
讓我們新增另一個值，例如儲存格`A3`，並將其格式化以顯示為貨幣。為了讓事情變得更有趣，我們將使用一種格式，將正值顯示為英鎊貨幣，將負值顯示為美元。
```csharp
//將數值新增至「A3」儲存格
worksheet.Cells["A3"].PutValue(2546);
//取得A3單元格的樣式
style = worksheet.Cells["A3"].GetStyle();
//設定自訂顯示格式以將數值顯示為貨幣
style.Custom = "£#,##0;[Red]$-#,##0";
//將樣式套用到 A3 儲存格
worksheet.Cells["A3"].SetStyle(style);
```
- 我們增加價值`2546`到細胞`A3`.
- 我們設定自訂格式`£#,##0;[Red]$-#,##0`，它顯示帶井號的正值和帶有美元符號的紅色負值。
- 我們使用以下方法將樣式套用至儲存格`SetStyle()`.
## 第 6 步：儲存工作簿
最後一步是將工作簿儲存為 Excel 檔案。在本教學中，我們將使用 Excel 97-2003 格式。
```csharp
//儲存 Excel 文件
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
- 這`Save()`方法將工作簿保存在指定目錄中。
- 我們選擇`SaveFormat.Excel97To2003`以確保與舊版 Excel 的兼容性。
## 結論
給你了！我們剛剛建立了一個 Excel 文件，使用 Aspose.Cells for .NET 將自訂日期、百分比和貨幣格式新增至特定儲存格，並儲存了該文件。自訂格式使您的 Excel 檔案更具可讀性和專業性。不要忘記探索 Aspose.Cells 中的其他格式選項，例如條件格式，以便更好地控制資料的外觀。
## 常見問題解答
### 如何在 Aspose.Cells 中套用更複雜的格式選項？
您可以將不同的格式樣式（例如字體顏色、邊框和背景顏色）與自訂數字格式結合。
### 我可以將自訂數字格式應用於一系列單元格嗎？
是的，Aspose.Cells 允許您使用以下命令將樣式套用到一系列儲存格：`Range.SetStyle()`方法。
### 我還可以將工作簿儲存為哪些其他文件格式？
 Aspose.Cells 支援多種格式，包括 XLSX、CSV 和 PDF。只需更改`SaveFormat`在`Save()`方法。
### 我可以用不同的方式格式化負數嗎？
絕對地！您可以使用自訂數字格式以不同的顏色或符號顯示負數。
### Aspose.Cells for .NET 是免費的嗎？
 Aspose.Cells 提供免費試用版，但要獲得完整功能，您需要有效的授權。你可以獲得一個[臨時許可證在這裡](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
