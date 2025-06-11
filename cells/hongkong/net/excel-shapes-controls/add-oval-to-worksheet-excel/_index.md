---
"description": "了解如何使用 Aspose.Cells for .NET 將橢圓形新增至 Excel 工作表。帶有詳細程式碼解釋的分步指南。"
"linktitle": "在 Excel 中將橢圓形新增至工作表"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 Excel 中將橢圓形新增至工作表"
"url": "/zh-hant/net/excel-shapes-controls/add-oval-to-worksheet-excel/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中將橢圓形新增至工作表

## 介紹
創建令人驚嘆的互動式 Excel 檔案不僅僅涉及數字和公式。橢圓形等形狀可以增加視覺吸引力或在工作表中提供功能元素。在本教學中，我們將探討如何使用 Aspose.Cells for .NET 以程式設計方式將橢圓形新增至 Excel 工作表。無論您想添加一些特色還是功能，我們都會為您提供逐步指南，分解所有內容。
## 先決條件
在深入研究程式碼之前，您需要做好以下幾點：
1. Aspose.Cells for .NET Library：您可以從 [這裡](https://releases.aspose.com/cells/net/) 或使用 Visual Studio 中的 NuGet 安裝它。
2. 開發環境：類似 Visual Studio 的 C# IDE。
3. 對 C# 的基本了解：您應該熟悉 C# 中的基本編碼概念。
另外，請記得透過安裝 Aspose.Cells for .NET 函式庫來設定您的專案。如果你還沒有執照，你可以申請 [臨時執照](https://purchase.aspose.com/temporary-license/) 或使用 [免費試用](https://releases.aspose.com/) 版本。
## 導入包
在編寫任何程式碼之前，請確保已包含所需的命名空間。以下是 C# 程式碼片段，可確保您使用正確的程式庫：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## 步驟 1：設定目錄
在 Excel 工作表中新增橢圓的第一步是指定 Excel 檔案的儲存位置。讓我們定義目錄路徑並確保在儲存工作之前該目錄存在。

我們將建立一個目錄路徑並驗證它是否存在。如果該資料夾不存在，則會建立該資料夾。
```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory";
// 如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
此步驟至關重要，因為它可以確保您的文件保存在正確的位置，並且您以後不會遇到文件路徑問題。
## 步驟 2：初始化新工作簿
接下來，我們需要建立一個新的工作簿，在其中新增橢圓形。工作簿代表一個Excel文件，我們可以在其中添加內容或形狀。

在此步驟中，我們實例化一個新的 `Workbook` 該物件將作為我們的 Excel 文件容器。
```csharp
// 實例化一個新的工作簿。
Workbook excelbook = new Workbook();
```
## 步驟 3：新增第一個橢圓形
現在到了有趣的部分——在工作表中添加橢圓形。這個橢圓可以代表一個視覺元素，例如按鈕或高亮。我們首先將第一個橢圓形加入到工作簿的第一個工作表中。

在這裡，我們使用 `Shapes.AddOval()` 方法在工作表上的特定行和列建立橢圓。
```csharp
// 加入橢圓形。
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
裡面的參數 `AddOval()` 如下：
- 前兩個數字代表橢圓左上角的行和列。
- 接下來的兩個數字代表橢圓的高度和寬度。
## 步驟 4：設定橢圓的位置和樣式
建立橢圓後，我們可以設定它的位置、線條粗細和虛線樣式。這 `Placement` 屬性決定了在工作表中調整大小或移動儲存格時橢圓的行為。

我們使橢圓自由浮動並調整其外觀。
```csharp
// 設定橢圓的位置。
oval1.Placement = PlacementType.FreeFloating;
// 設定線條粗細。
oval1.Line.Weight = 1;
// 設定橢圓的虛線樣式。
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
這使得橢圓可以在工作表內自由移動，並且其線條粗細和樣式設定以實現視覺一致性。
## 步驟5：新增另一個橢圓（圓形）形狀
為什麼只停留在一個地方？在此步驟中，我們將添加另一個橢圓形，這次透過使高度和寬度相同來創建一個完美的圓形。

我們創建另一個橢圓，將其放置在不同的位置，並透過設定相等的高度和寬度確保它具有圓形。
```csharp
// 增加另一個橢圓形（圓形）。
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## 步驟 6：設計第二個橢圓
就像之前一樣，我們將調整第二個橢圓（或圓形）的位置、粗細和虛線樣式。

我們將類似的屬性應用於第二個橢圓，以符合第一個橢圓的風格。
```csharp
// 設定橢圓的位置。
oval2.Placement = PlacementType.FreeFloating;
// 設定線條粗細。
oval2.Line.Weight = 1;
// 設定橢圓的虛線樣式。
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## 步驟 7：儲存工作簿
最後，我們需要保存剛剛新增的橢圓的工作簿。儲存檔案可確保儲存所有變更。

我們將工作簿儲存到我們之前定義的目錄路徑。
```csharp
// 儲存 Excel 檔案。
excelbook.Save(dataDir + "book1.out.xls");
```
就是這樣！您已成功將橢圓形新增至 Excel 工作表並儲存了檔案。
## 結論
使用 Aspose.Cells for .NET 將橢圓形等形狀新增至 Excel 工作表不僅簡單，而且還是一種使用附加視覺元素增強電子表格的有趣方式。無論是為了設計目的還是添加可點擊元素，形狀都可以在 Excel 檔案的外觀和功能中發揮重要作用。因此，下次您處理需要互動式或視覺上吸引人的 Excel 表的項目時，您就會知道如何添加那些完美的橢圓形！
## 常見問題解答
### 我可以使用 Aspose.Cells for .NET 添加其他形狀，例如矩形或線條嗎？
是的，你可以使用 `Shapes` Aspose.Cells 中的集合。
### 添加橢圓後可以調整大小嗎？
絕對地！新增橢圓後，您可以修改其高度和寬度屬性。
### 除了 XLS 之外，我還可以將工作簿儲存為哪些文件格式？
Aspose.Cells 支援多種格式，例如 XLSX、CSV 和 PDF 等。
### 我可以修改橢圓輪廓的顏色嗎？
是的，你可以使用 `Line.Color` 財產。
### Aspose.Cells 需要許可證嗎？
雖然您可以免費試用 Aspose.Cells，但您需要 [執照](https://purchase.aspose.com/buy) 適合長期使用或存取高級功能。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}