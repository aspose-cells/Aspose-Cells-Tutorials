---
"description": "透過詳細的逐步指南了解如何使用 Aspose.Cells for .NET 在 Excel 工作表中新增矩形控制項。"
"linktitle": "在 Excel 中為工作表新增矩形控件"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 Excel 中為工作表新增矩形控件"
"url": "/zh-hant/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/"
"weight": 25
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中為工作表新增矩形控件

## 介紹
在自動化 Excel 任務方面，Aspose.Cells for .NET 是一個強大的工具，可以幫助您實現各種目標，其中之一就是在工作表中新增矩形等形狀。在本指南中，我們將探討如何使用 Aspose.Cells for .NET 在 Excel 工作表中新增矩形控制項。最後，您將能夠建立、自訂和儲存嵌入矩形控制項的工作表。
但在深入探討之前，讓我們先討論先決條件。
## 先決條件
要遵循本教程，請確保您已滿足以下先決條件：
1. Aspose.Cells for .NET 函式庫：如果您還沒有， [下載庫](https://releases.aspose.com/cells/net/) 或使用 Visual Studio 中的 NuGet 安裝它。
2. .NET Framework：您需要在您的機器上設定.NET 開發環境。
3. C# 基礎知識：雖然我們會逐步指導您，但熟悉 C# 和物件導向程式設計的基本知識還是有益的。
4. 許可證：在評估模式下使用 Aspose.Cells 可以完成基本任務，但要獲得完整功能，請考慮獲取 [臨時執照](https://purchase.aspose.com/temporary-license/) 或從 [這裡](https://purchase。aspose.com/buy).
現在，讓我們深入研究程式碼！
## 導入包
若要開始使用 Aspose.Cells，請確保已將必要的命名空間匯入到專案中。這些匯入將允許存取與 Excel 檔案互動所需的各種類別和方法。
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
這些行確保您的項目可以與文件目錄進行互動（`System.IO`)、Excel 工作簿（`Aspose.Cells`) 和形狀繪製 (`Aspose.Cells.Drawing`）。
現在，讓我們將這個過程分解成簡單的步驟，以便您可以輕鬆地跟隨並在自己的專案中複製它。
## 步驟 1：設定目錄路徑
您需要做的第一件事是定義儲存 Excel 檔案的目錄。此步驟可確保您的專案知道在哪裡建立和儲存輸出檔案。
### 定義資料目錄
```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory";
```
在這裡，您可以指定儲存 Excel 檔案的目錄路徑。您可以替換 `"Your Document Directory"` 使用您機器上的實際路徑，如果不存在則動態建立一個資料夾。
### 檢查並建立目錄
```csharp
// 如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
該塊檢查目錄是否存在。如果沒有，它會創建一個。想像一下，在儲存任何文件之前，先準備好文件櫃。
## 步驟 2：實例化新工作簿
在此步驟中，您將使用 `Aspose.Cells.Workbook` 班級。這將作為您的工作表和形狀的容器。
```csharp
// 實例化一個新的工作簿。
Workbook excelbook = new Workbook();
```
透過調用 `Workbook` 建構函數後，現在您就有了一個可供自訂的空白 Excel 工作簿。
## 步驟3：新增矩形控件
這就是奇蹟發生的地方。您將向工作簿的第一個工作表新增一個矩形形狀。
```csharp
// 新增一個矩形控制項。
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
讓我們來分析一下：
- `excelbook.Worksheets[0]`：這將存取工作簿中的第一個工作表。
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`：這會在工作表中新增一個矩形形狀。這裡的參數定義了矩形的位置（行和列）以及寬度和高度。
## 步驟4：自訂矩形
僅添加一個矩形是不夠的——您需要對其進行自訂。在此步驟中，我們將設定矩形的位置、線條粗細和虛線樣式。
### 設定位置
```csharp
// 設定矩形的位置。
rectangle.Placement = PlacementType.FreeFloating;
```
這指定矩形是自由浮動的，這意味著它不會受到單元格尺寸的限制。
### 設定線寬
```csharp
// 設定線條粗細。
rectangle.Line.Weight = 4;
```
這裡，我們將矩形的線條粗細設定為4磅。數字越高，線越粗。
### 設定虛線樣式
```csharp
// 設定矩形的虛線樣式。
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
此行將矩形邊框的虛線樣式設定為實線。您可以嘗試不同的風格，例如 `Dash` 或者 `Dot` 取決於您的要求。
## 步驟 5：儲存工作簿
新增並自訂矩形後，最後一步是將工作簿儲存到指定的目錄。
```csharp
// 儲存 Excel 檔案。
excelbook.Save(dataDir + "book1.out.xls");
```
這會將工作簿儲存為 `.xls` 您之前定義的資料夾中的檔案。您可以透過更改副檔名來修改檔案格式，例如 `.xlsx` 如果您喜歡較新的 Excel 格式。
## 結論
就是這樣！一旦逐步分解，使用 Aspose.Cells for .NET 為 Excel 工作表新增矩形控制項是一個簡單的過程。無論您需要添加形狀以增強視覺吸引力、突出顯示資料部分還是自訂報告，Aspose.Cells 都可以讓您靈活地以程式設計方式進行操作。
本指南應該為您提供使用 Aspose.Cells 為 Excel 工作表新增矩形等形狀所需的所有知識。現在是時候進行實驗並看看您還可以使用這個強大的程式庫實現什麼！
## 常見問題解答
### 我可以使用 Aspose.Cells for .NET 添加其他形狀，例如圓形或線條嗎？  
是的，Aspose.Cells 允許您添加各種形狀，包括圓形、線條、箭頭等。
### 我可以為矩形控制項設定哪些其他屬性？  
您可以自訂填滿顏色、線條顏色、透明度，甚至在矩形內添加文字。
### Aspose.Cells 與 .NET Core 相容嗎？  
是的，Aspose.Cells 支援 .NET Core，以及 .NET Framework 和其他基於 .NET 的平台。
### 我可以將矩形定位到特定單元格嗎？  
是的，您可以將矩形放置在特定的行和列中，或使用 `PlacementType` 來控制它的錨定方式。
### Aspose.Cells 有免費試用版嗎？  
是的，你可以得到 [免費試用](https://releases.aspose.com/) 從網站上測試圖書館的功能，然後再購買。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}