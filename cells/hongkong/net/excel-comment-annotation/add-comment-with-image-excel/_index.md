---
"description": "了解如何使用 Aspose.Cells for .NET 在 Excel 中新增帶有影像的註解。使用個人化註解增強您的電子表格。"
"linktitle": "在 Excel 中新增帶有圖像的註釋"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 Excel 中新增帶有圖像的註釋"
"url": "/zh-hant/net/excel-comment-annotation/add-comment-with-image-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中新增帶有圖像的註釋

## 介紹
Excel 是用於資料管理和分析的強大工具，但有時您需要為電子表格添加個人化內容，對嗎？也許您想註釋數據、提供回饋，甚至用圖像添加一點特色。這就是評論派上用場的地方！在本教學中，我們將探討如何使用 .NET 的 Aspose.Cells 函式庫在 Excel 中新增帶有影像的註解。這種方法對於創建更具互動性和視覺吸引力的電子表格特別有用。
## 先決條件
在我們深入探討在 Excel 中新增帶有圖像的註釋的細節之前，讓我們確保您已準備好開始操作所需的一切：
1. Visual Studio：確保您的電腦上安裝了 Visual Studio。這是您編寫和執行程式碼的地方。
2. Aspose.Cells for .NET：您需要有 Aspose.Cells 函式庫。如果你還沒有安裝，你可以從 [這裡](https://releases。aspose.com/cells/net/).
3. C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解程式碼片段。
4. 圖片檔案：準備好要嵌入到 Excel 註解中的圖片檔案（如標誌）。在本教程中，我們假設您有一個名為 `logo。jpg`.
5. .NET Framework：確保您已安裝 .NET Framework，因為 Aspose.Cells 需要它才能正常運作。
現在我們已經滿足了先決條件，讓我們繼續進行實際的編碼！
## 導入包
首先，我們需要導入必要的套件。在您的 C# 專案中，請確保新增對 Aspose.Cells 庫的引用。您可以使用 Visual Studio 中的 NuGet 套件管理器來執行此操作。方法如下：
1. 開啟 Visual Studio。
2. 建立新項目或開啟現有項目。
3. 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
4. 選擇管理 NuGet 套件。
5. 搜尋 Aspose.Cells 並安裝它。

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

一旦安裝了庫，您就可以開始編寫程式碼。以下是逐步操作的方法。
## 步驟 1：設定文檔目錄
首先，我們需要設定一個可以儲存 Excel 檔案的目錄。這是至關重要的一步，因為我們希望保持工作井然有序。
```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory";
// 如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir：此變數保存您的文件目錄的路徑。代替 `"Your Document Directory"` 使用您想要儲存 Excel 檔案的實際路徑。
- Directory.Exists：檢查目錄是否已經存在。
- Directory.CreateDirectory：如果目錄不存在，則建立它。
## 步驟 2：實例化工作簿
接下來，我們需要建立一個 `Workbook` 班級。此類代表記憶體中的 Excel 工作簿。
```csharp
// 實例化工作簿
Workbook workbook = new Workbook();
```
- 工作簿：這是 Aspose.Cells 中的主要類，可讓您建立和操作 Excel 檔案。透過實例化它，您實際上正在建立一個新的 Excel 工作簿。
## 步驟3：取得評論集合
現在我們有了工作簿，讓我們訪問第一個工作表的評論集。
```csharp
// 獲取第一張表的評論集合的引用
CommentCollection comments = workbook.Worksheets[0].Comments;
```
- 工作表[0]：存取工作簿中的第一個工作表。請記住，索引是從零開始的，所以 `[0]` 指的是第一張表。
- 評論：此屬性使我們能夠存取該工作表上的評論集合。
## 步驟 4：為儲存格新增註釋
讓我們為特定單元格添加評論。在這種情況下，我們將向儲存格 A1 新增註解。
```csharp
// 在儲存格 A1 中新增註釋
int commentIndex = comments.Add(0, 0);
Comment comment = comments[commentIndex];
comment.Note = "First note.";
comment.Font.Name = "Times New Roman";
```
- comments.Add(0, 0)：此方法為儲存格 A1（第 0 行，第 0 列）新增註解。
- comment.Note：在這裡，我們設定評論的文字。
- comment.Font.Name：設定評論文字的字體。
## 步驟 5：將圖像載入到流中
現在是時候加載我們想要嵌入到評論中的圖像了。我們將使用 `MemoryStream` 儲存影像資料。
```csharp
// 將圖像載入到流中
Bitmap bmp = new Bitmap(dataDir + "logo.jpg");
MemoryStream ms = new MemoryStream();
bmp.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
```
- Bitmap：此類別用於載入映像檔。確保路徑正確。
- MemoryStream：這是我們用來將圖像保存在記憶體中的流。
- bmp.Save：將點陣圖影像以 PNG 格式儲存到記憶體流中。
## 步驟 6：將影像資料設定為註解形狀
現在我們需要將圖像資料設定為與我們先前建立的評論相關的形狀。
```csharp
// 將圖像資料設定為與評論相關的形狀
comment.CommentShape.Fill.ImageData = ms.ToArray();
```
- comment.CommentShape.Fill.ImageData：此屬性可讓您設定評論形狀的圖像。我們將 `MemoryStream` 轉換為位元組數組 `ms。ToArray()`.
## 步驟 7：儲存工作簿
最後，讓我們保存包含註釋和圖像的工作簿。
```csharp
// 儲存工作簿
workbook.Save(dataDir + "book1.out.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
- workbook.Save：此方法將工作簿儲存到指定路徑。我們將其保存為 XLSX 檔案。
## 結論
就是這樣！您已成功使用 Aspose.Cells for .NET 為 Excel 檔案新增帶有影像的註解。此功能可讓您的電子表格更具資訊性和視覺吸引力。無論您是註釋資料、提供回饋還是僅僅添加個人風格，帶有圖像的評論都可以顯著增強使用者體驗。
## 常見問題解答
### 我可以為同一個單元格添加多個評論嗎？
不可以，Excel 不允許在同一個儲存格上新增多個註解。每個單元格只能有一個註解。
### 支援哪些圖像格式？
Aspose.Cells 支援各種圖片格式，包括 PNG、JPEG 和 BMP。
### 我需要許可證才能使用 Aspose.Cells 嗎？
Aspose.Cells 提供免費試用，但要獲得完整功能，您需要購買許可證。
### 我可以自訂評論的外觀嗎？
是的，您可以自訂評論文字的字體、大小和顏色，也可以變更評論本身的形狀和大小。
### 在哪裡可以找到有關 Aspose.Cells 的更多文件？
您可以在 Aspose.Cells 上找到全面的文檔 [這裡](https://reference。aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}