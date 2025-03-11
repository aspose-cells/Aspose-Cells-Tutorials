---
title: .NET 中的工作表到影像轉換
linktitle: .NET 中的工作表到影像轉換
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過我們的逐步指南，了解如何使用 Aspose.Cells 將 Excel 工作表轉換為 .NET 中的映像。簡化您的資料視覺化。
weight: 11
url: /zh-hant/net/image-and-chart-operations/worksheet-to-image-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET 中的工作表到影像轉換

## 介紹
當談到在 .NET 中操作 Excel 檔案時，Aspose.Cells 是一個可靠且強大的程式庫。您可能遇到的常見任務之一是將 Excel 工作表轉換為影像。無論您是想在網頁上顯示工作表、將其包含在報告中，還是只是以視覺方式共享數據，本逐步指南都將引導您完成整個過程。最後，您將具備將工作表無縫轉換為影像所需的一切。那麼就讓我們深入了解吧！
## 先決條件
在開始轉換之前，必須確保一切都設定正確。以下是您需要的先決條件：
1. Visual Studio：確保您的電腦上安裝了 Visual Studio。該 IDE 將協助您順利執行 .NET 專案。
2.  Aspose.Cells for .NET Library：您需要取得此程式庫。你可以[在這裡下載](https://releases.aspose.com/cells/net/)或從一個開始[免費試用](https://releases.aspose.com/).
3. C# 基礎知識：熟悉 C# 程式設計將會很有幫助，因為我們的範例和解釋將用這種語言編寫。
4.  Excel 檔案範例：為了演示，請建立或下載 Excel 檔案。另存為`MyTestBook1.xls`在你的專案目錄中。
5. 對 .NET 專案的基本了解：了解如何建立簡單的 .NET 專案將使這變得更容易，但不用擔心 - 我們將引導您完成這些步驟。
## 導入包
我們旅程的第一步是將必要的 Aspose.Cells 套件匯入到我們的專案中。這是至關重要的，因為它允許我們利用 Aspose.Cells 提供的所有功能。
## 第 1 步：建立一個新項目 
首先，在 Visual Studio 中建立一個新的 .NET 專案：
- 打開視覺工作室。
- 按一下“建立新專案”。
- 根據您的喜好選擇「控制台應用程式（.NET Framework）」或「控制台應用程式（.NET Core）」。
- 為您的專案命名（例如，WorksheetToImage）並按一下「建立」。
## 步驟2：新增Aspose.Cells引用
現在我們有了項目，我們需要加入 Aspose.Cells：
- 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
- 選擇“管理 NuGet 套件”。
- 搜尋“Aspose.Cells”並安裝最新版本。
```csharp
using System.IO;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```
您已準備好進行編碼部分！

現在，讓我們逐步分解實際的轉換過程。我們將使用一個簡單的 C# 程式來開啟 Excel 檔案、將工作表轉換為映像並將該映像儲存到指定目錄。
## 第三步：設定環境
首先，透過定義文檔目錄的路徑來設定環境：
```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
```
在這裡，我們定義了一個變量，名為`dataDir`它保存我們的檔案儲存目錄的路徑。代替`"Your Document Directory"`與系統上的實際路徑（例如，「C:\\我的文件\\”）。
## 步驟 4：開啟 Excel 工作簿
接下來，我們將使用以下命令開啟 Excel 文件`Workbook`Aspose.Cells 中的類別：
```csharp
//開啟 Excel 範本檔案。
Workbook book = new Workbook(dataDir + "MyTestBook1.xls");
```
在這一步驟中，我們建立一個實例`Workbook`類別並將路徑傳遞給我們的 Excel 檔案。這使我們能夠以程式設計方式與文件的內容進行互動。
## 第 5 步：訪問工作表
現在我們已經打開了工作簿，讓我們可以訪問第一個工作表：
```csharp
//取得第一個工作表。
Worksheet sheet = book.Worksheets[0];
```
在這裡，我們檢索第一個工作表（索引`0`）來自工作簿。 Aspose.Cells 陣列是零索引的，這表示第一張紙是`0`.
## 第 6 步：定義影像或列印選項
在渲染圖像之前，我們需要使用以下命令指定我們希望它的外觀`ImageOrPrintOptions`：
```csharp
//定義影像或列印選項
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
//指定影像格式
imgOptions.ImageType = Drawing.ImageType.Jpeg;
//整張紙僅渲染一頁
imgOptions.OnePagePerSheet = true;
```
在這一步驟中，我們建立一個實例`ImageOrPrintOptions`。我們指定要將輸出儲存為 JPEG 影像並設定`OnePagePerSheet`到`true`以確保整張紙被捕獲在一張影像中。
## 第 7 步：渲染工作表
選項到位後，我們現在可以渲染工作表：
```csharp
//根據指定的圖像/列印選項渲染圖紙
SheetRender sr = new SheetRender(sheet, imgOptions);
//渲染工作表的圖像
Bitmap bitmap = sr.ToImage(0);
```
這`SheetRender`類別有助於將工作表渲染為點陣圖影像。我們打電話`ToImage(0)`將第零頁（我們的第一張紙）渲染為點陣圖。
## 第 8 步：儲存影像
渲染完成後，我們需要將圖像保存到指定目錄中：
```csharp
//儲存指定影像格式的影像檔案。
bitmap.Save(dataDir + "SheetImage.out.jpg");
```
在這裡，我們保存生成的點陣圖影像。該行將圖像寫入`dataDir`帶有檔案名稱的位置`SheetImage.out.jpg`.
## 第 9 步：完成通知
為了確保過程完成，讓我們添加一個簡單的控制台訊息：
```csharp
//顯示結果，以便使用者知道處理已完成。
System.Console.WriteLine("Conversion to Image(s) completed.");
```
該行向控制台輸出一條確認訊息，讓使用者知道轉換成功。
## 結論
現在你就擁有了！只需幾個簡單的步驟，您就學會如何使用 Aspose.Cells for .NET 將 Excel 工作表轉換為映像。此過程不僅快速且功能強大，使您能夠輕鬆建立電子表格資料的視覺化表示。
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個 .NET 函式庫，可讓開發人員以程式設計方式建立、操作、轉換和處理 Excel 檔案。
### 我可以免費使用 Aspose.Cells 嗎？
是的，您可以從他們的網站下載免費試用版來開始使用 Aspose.Cells[網站](https://releases.aspose.com/).
### Aspose.Cells 支援要匯出哪些影像格式？
Aspose.Cells 支援各種圖片格式，包括 JPEG、PNG、BMP 和 GIF。
### 在哪裡可以找到 Aspose.Cells 的額外支援？
您可以造訪 Aspose.Cells 的支援論壇[這裡](https://forum.aspose.com/c/cells/9).
### 如何取得 Aspose.Cells 的臨時授權？
可以透過造訪他們的網站來獲得臨時許可證[臨時許可證頁面](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
