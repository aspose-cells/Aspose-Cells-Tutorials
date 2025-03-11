---
title: Excel中的位置圖片（比例）
linktitle: Excel中的位置圖片（比例）
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 在 Excel 中按比例定位影像。讓您的電子表格在視覺上更具吸引力。
weight: 14
url: /zh-hant/net/excel-ole-picture-objects/position-picture-proportional-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel中的位置圖片（比例）

## 介紹
您是否厭倦了那些似乎永遠不適合 Excel 電子表格的像素化影像？想像一下：您有一個漂亮的徽標，需要在 Excel 工作表中突出顯示，但最終它被壓扁、拉伸或放置不當。沒有人想要這樣！好吧，請坐好，因為今天您將學習如何使用 .NET 的 Aspose.Cells 庫在 Excel 中按比例定位圖像。這個強大的函式庫讓操作 Excel 檔案變得輕而易舉，無論是用於報表、資料分析，還是只是修飾簡報。讓我們深入探討完美對齊照片的細節！
## 先決條件
在我們深入實際編碼之前，您需要在電腦上設定一些內容：
1. Visual Studio：確保安裝了 Visual Studio，因為它將為您的 .NET 專案提供方便的環境。
2.  Aspose.Cells 函式庫：您需要 Aspose.Cells 函式庫。您可以免費試用或從[阿斯普斯網站](https://purchase.aspose.com/buy).
3. C# 基礎知識：稍微熟悉一下 C# 程式設計將對理解我們將要討論的範例大有幫助。
4. 圖像檔案：準備好要插入 Excel 工作表的圖像（例如徽標）。
現在一切準備就緒，讓我們開始編碼吧！
## 導入包
要開始在專案中使用 Aspose.Cells，您需要匯入特定的命名空間。具體做法如下：
### 建立一個新項目
在 Visual Studio 中，建立一個新專案：
- 打開視覺工作室。
- 按一下“建立新專案”。
- 根據您的喜好選擇“類別庫（.NET Framework）”或“控制台應用程式”。
### 安裝 Aspose.Cells
您可以透過 NuGet 將 Aspose.Cells 套件新增至您的專案。方法如下：
- 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
- 選擇“管理 NuGet 套件”。
- 搜尋“Aspose.Cells”並點擊“安裝”。
### 新增使用指令
在程式碼檔案的頂部包含以下指令：
```csharp
using System.IO;
using Aspose.Cells;
```
這些指令將使您能夠存取操作 Excel 檔案所需的類別。
現在，讓我們將其分解為在 Excel 中成功按比例定位影像的詳細步驟。
## 第 1 步：設定您的目錄
首先，請確保您有一個指定的文件資料夾。如果目錄不存在，則建立方法如下：
```csharp
string dataDir = "Your Document Directory";
//如果目錄尚不存在，則建立該目錄。
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
此程式碼片段會建立一個新目錄（如果不存在）來儲存 Excel 檔案。只需更換`"Your Document Directory"`與您想要儲存檔案的實際路徑。
## 第 2 步：實例化工作簿
接下來，讓我們建立一個新的工作簿：
```csharp
Workbook workbook = new Workbook();
```
此行初始化一個新的工作簿對象，為您提供一個空白畫布來進行操作。
## 第 3 步：新增工作表
現在我們已經設定了工作簿，讓我們在其中新增一個工作表：
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
這將會新增一個新的工作表並傳回該工作表的索引，我們稍後可以用它來操作它。
## 第 4 步：存取新工作表
要操作新新增的工作表，您需要存取它：
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
現在，`worksheet`將允許我們向該特定工作表添加內容和圖像。
## 第5步：插入圖片
現在到了令人興奮的部分！讓我們添加您的美麗圖像。代替`"logo.jpg"`與您的映像檔的名稱：
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
此行在儲存格 F6 處新增映像（因為行和列的索引為零，`5`指第六個單元格）。
## 第6步：訪問新增的圖片
插入圖像後，您可以像這樣存取它：
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
這使您能夠操縱圖片屬性。
## 第7步：按比例放置圖片
現在，讓我們按比例放置圖片：
```csharp
picture.UpperDeltaX = 200;
picture.UpperDeltaY = 200;
```
這裡，`UpperDeltaX`和`UpperDeltaY`調整影像相對於儲存格尺寸的位置。您可以調整這些值以使影像恰到好處。
## 第 8 步：儲存您的更改
最後，儲存工作簿以保留所有變更：
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
此行將您的工作簿另存為`book1.out.xls`到指定目錄下。
## 結論
現在你就擁有了！您剛剛學習如何使用 Aspose.Cells for .NET 在 Excel 中按比例放置圖片。這不僅僅是插入圖像；這是為了讓它們在電子表格中看起來完美。請記住：放置得當的圖片可以顯著提升您的資料呈現效果。
嘗試不同的圖像和位置，享受樂趣，並毫不猶豫地深入了解 Aspose.Cells 提供的豐富功能。您的 Excel 工作表即將徹底改造！
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個強大的 .NET 程式庫，使用戶能夠建立、操作和轉換 Excel 文件，而無需安裝 Microsoft Excel。
### 我可以免費使用 Aspose.Cells 嗎？
是的，Aspose.Cells 提供免費試用版，您可以下載[這裡](https://releases.aspose.com/).
### 我在哪裡可以找到文件？
您可以訪問全面的[文件](https://reference.aspose.com/cells/net/)對於 Aspose.Cells。
### Aspose.Cells 支援所有圖片格式嗎？
Aspose.Cells 支援多種格式，包括 JPEG、PNG、BMP、GIF 和 TIFF。
### 我如何獲得 Aspose.Cells 的支援？
如有任何疑問，請隨時訪問[支援論壇](https://forum.aspose.com/c/cells/9)您可以在哪裡提問。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
