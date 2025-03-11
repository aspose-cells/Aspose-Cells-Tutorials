---
title: .NET 中的圖表到影像轉換
linktitle: .NET 中的圖表到影像轉換
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過此逐步指南，了解如何使用 Aspose.Cells 將圖表轉換為 .NET 中的圖像。輕鬆將 Excel 圖表轉換為高品質影像。
weight: 10
url: /zh-hant/net/image-and-chart-operations/chart-to-image-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET 中的圖表到影像轉換

## 介紹
在建立報告系統或共享視覺化資料表示時，將 Excel 圖表轉換為圖像可能是關鍵要求。幸運的是，有了 Aspose.Cells for .NET，這個過程就變得非常簡單！無論您是產生報告還是只是將 Excel 圖表轉換為圖像以更好地顯示，本指南都將引導您逐步完成該過程。
## 先決條件
在開始之前，讓我們確保您已準備好遵循本教學的所有內容。
### Aspose.Cells for .NET 函式庫
首先，您需要在專案中下載並引用 Aspose.Cells for .NET 函式庫。您可以在這裡獲取最新版本：
- [下載 .NET 版 Aspose.Cells](https://releases.aspose.com/cells/net/)
### .NET環境
確保您的系統上安裝了 .NET Framework。您可以使用 Visual Studio 或任何其他 .NET 開發環境來執行此範例。
### 許可證設定（可選）
雖然您可以免費試用 Aspose.Cells，但要獲得完整的功能且不受任何限制，請考慮申請[臨時執照](https://purchase.aspose.com/temporary-license/)或從以下網站購買一份[這裡](https://purchase.aspose.com/buy).

## 導入包
首先，讓我們匯入必要的命名空間以使用 Aspose.Cells 函式庫。這將使我們能夠操作 Excel 檔案並產生圖像。
```csharp
using System.IO;
using System.Drawing;
using Aspose.Cells;
```
在開始編碼部分之前，請確保您已準備好這些包。

現在，讓我們將圖表轉換為圖像的過程分解為簡單的步驟。
## 第 1 步：設定您的專案目錄
您需要一個地方來保存生成的圖像，對嗎？我們首先建立一個用於保存輸出影像的目錄。

我們首先定義文檔目錄的路徑並確保該資料夾存在。如果沒有，我們將創建一個。
```csharp
//定義保存圖片的目錄
string dataDir = "Your Document Directory";
//檢查目錄是否存在
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
透過此步驟，您就可以產生圖表影像並將其儲存到此目錄。
## 第 2 步：建立新工作簿
在這裡，我們將實例化一個 Workbook 物件。這將代表我們將在其中嵌入圖表的 Excel 文件。

工作簿就像包含工作表的 Excel 檔案。透過建立新的工作簿，我們從一個空的 Excel 檔案開始。
```csharp
//建立一個新的工作簿對象
Workbook workbook = new Workbook();
```
## 第 3 步：新增工作表
每個 Excel 檔案都有工作表（或選項卡）。讓我們在工作簿中新增一個。

新增工作表至關重要，因為我們將把資料和圖表插入到該工作表中。新增工作表後，我們檢索其參考。
```csharp
//將新工作表新增至工作簿
int sheetIndex = workbook.Worksheets.Add();
//檢索新新增的工作表
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
## 步驟 4：用資料填入工作表
要創建有意義的圖表，我們需要一些數據，對吧？讓我們用範例值填充幾個單元格。

我們將資料新增至工作表上的特定儲存格。該數據稍後將用於生成我們的圖表。
```csharp
//將範例資料新增至儲存格
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
## 第 5 步：將圖表新增至工作表
現在，讓我們建立一個長條圖來視覺化我們剛剛新增的資料。

我們指定圖表的類型（長條圖）並定義其大小和在工作表中的位置。
```csharp
//將長條圖加入工作表
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
```
## 步驟 6：定義圖表資料來源
這就是神奇發生的地方：將圖表連結到工作表中的資料！

我們將圖表連結到 A1 至 B3 欄的資料。這告訴圖表從哪裡提取數據。
```csharp
//將圖表連結到 A1 到 B3 範圍內的數據
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("A1:B3", true);
```
## 第 7 步：將圖表轉換為影像
關鍵時刻：我們要將此圖表轉換為圖像檔案！

在這裡，我們使用`ToImage`將圖表轉換為您選擇的圖像格式的方法。在本例中，我們將其轉換為 EMF（增強型圖元檔案）格式。
```csharp
//將圖表轉換為圖像並儲存到目錄中
chart.ToImage(dataDir + "Chart.emf", ImageFormat.Emf);
```
就是這樣！您的圖表現已儲存為影像。是時候拍拍自己的背了。
## 步驟8：顯示成功訊息
最後，讓我們顯示一條確認圖像產生的訊息。
```csharp
//顯示一則訊息表示成功
System.Console.WriteLine("Image generated successfully.");
```
## 結論
繁榮！使用 Aspose.Cells for .NET 將圖表從 Excel 轉換為圖像是如此簡單。此過程不僅簡化了資料的呈現，還增強了報表或儀表板的靈活性，其中影像優於嵌入圖表。
透過遵循本指南中概述的步驟，您現在可以將任何 Excel 圖表轉換為圖像，從而使您可以將視覺資料無縫整合到各種應用程式中。
## 常見問題解答
### 我可以使用此方法轉換不同類型的圖表嗎？
是的，您可以轉換 Aspose.Cells 支援的任何圖表類型，包括餅圖、長條圖、折線圖等等！
### 是否可以更改圖像格式？
絕對地！雖然我們在本例中使用了 EMF，但您只需修改以下內容即可將影像格式變更為 PNG、JPEG、BMP 等`ImageFormat`範圍。
### Aspose.Cells 支援高解析度影像嗎？
是的，Aspose.Cells 可讓您在將圖表匯出到影像時控制影像解析度和品質設定。
### 我可以一次將多個圖表轉換為圖像嗎？
是的，您可以循環瀏覽工作簿中的多個圖表，並只需幾行程式碼即可將它們全部轉換為圖像。
### 我可以轉換的圖表數量有限制嗎？
Aspose.Cells 沒有固有的限制，但處理大量資料可能取決於系統的記憶體和效能。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
