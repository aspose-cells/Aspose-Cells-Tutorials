---
title: 將矩形控制項新增至 Excel 中的工作表
linktitle: 將矩形控制項新增至 Excel 中的工作表
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過詳細的逐步指南，了解如何使用 Aspose.Cells for .NET 將矩形控制項新增至 Excel 工作表。
weight: 25
url: /zh-hant/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將矩形控制項新增至 Excel 中的工作表

## 介紹
當涉及自動化 Excel 任務時，Aspose.Cells for .NET 是一款功能強大的工具，可以幫助您實現各種目標，其中之一就是在工作表中添加矩形等形狀。在本指南中，我們將探討如何使用 Aspose.Cells for .NET 將矩形控制項新增至 Excel 工作表。最後，您將能夠建立、自訂和儲存嵌入了矩形控制項的工作表。
但在深入討論之前，讓我們先討論一下先決條件。
## 先決條件
要學習本教程，請確保您具備以下先決條件：
1.  Aspose.Cells for .NET 函式庫：如果您還沒有，[下載庫](https://releases.aspose.com/cells/net/)或在 Visual Studio 中使用 NuGet 安裝它。
2. .NET Framework：您需要在電腦上設定.NET 開發環境。
3. C# 的基礎知識：雖然我們將逐步指導您，但對 C# 和物件導向程式設計的基本熟悉是有益的。
4. 許可證：在評估模式下使用 Aspose.Cells 可以很好地完成基本任務，但要獲得完整功能，請考慮獲取[臨時執照](https://purchase.aspose.com/temporary-license/)或從以下網站購買一個[這裡](https://purchase.aspose.com/buy).
現在，讓我們深入研究程式碼！
## 導入包
若要開始使用 Aspose.Cells，請確保您已將必要的命名空間匯入到您的專案中。這些匯入將允許存取與 Excel 檔案互動所需的各種類別和方法。
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
這些行確保您的項目可以與文件目錄互動（`System.IO`), Excel 工作簿 (`Aspose.Cells`) 和形狀繪製 (`Aspose.Cells.Drawing`）。
現在，讓我們將該過程分解為簡單的步驟，以便您可以輕鬆地在自己的專案中遵循並複製該過程。
## 第1步：設定目錄路徑
您需要做的第一件事是定義儲存 Excel 檔案的目錄。此步驟可確保您的專案知道在哪裡建立和儲存輸出檔案。
### 定義資料目錄
```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
```
在這裡，您指定將儲存 Excel 檔案的目錄路徑。您可以更換`"Your Document Directory"`使用電腦上的實際路徑，或動態建立一個資料夾（如果不存在）。
### 檢查並建立目錄
```csharp
//如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
該塊檢查目錄是否存在。如果沒有，它就會創建一個。可以將其想像為在儲存任何文件之前準備好文件櫃。
## 第 2 步：實例化新工作簿
在此步驟中，您將使用下列命令建立新的 Excel 工作簿`Aspose.Cells.Workbook`班級。這將用作工作表和形狀的容器。
```csharp
//實例化一個新的工作簿。
Workbook excelbook = new Workbook();
```
透過致電`Workbook`在建構函式中，您現在有一個空白的 Excel 工作簿可供自訂。
## 第三步：新增矩形控件
這就是奇蹟發生的地方。您將向工作簿的第一個工作表新增一個矩形形狀。
```csharp
//新增一個矩形控制項。
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
讓我們來分解一下：
- `excelbook.Worksheets[0]`：這將存取工作簿中的第一個工作表。
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`：這會在工作表中新增一個矩形形狀。這裡的參數定義了矩形的位置（行和列）以及寬度和高度。
## 第四步：自訂矩形
僅僅添加一個矩形是不夠的——您需要自訂它。在此步驟中，我們將設定矩形的位置、線寬和虛線樣式。
### 設定放置位置
```csharp
//設定矩形的位置。
rectangle.Placement = PlacementType.FreeFloating;
```
這指定矩形是自由浮動的，這意味著它不會受到單元尺寸的限制。
### 設定線寬
```csharp
//設定線寬。
rectangle.Line.Weight = 4;
```
這裡，我們將矩形的線條粗細設定為 4 點。數字越高，線條越粗。
### 設定破折號樣式
```csharp
//設定矩形的虛線樣式。
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
該行將矩形邊框的虛線樣式設定為實線。您可以嘗試不同的風格，例如`Dash`或者`Dot`根據您的要求。
## 第 5 步：儲存工作簿
新增並自訂矩形後，最後一步是將工作簿儲存到指定目錄。
```csharp
//儲存 Excel 檔案。
excelbook.Save(dataDir + "book1.out.xls");
```
這會將工作簿另存為`.xls`文件位於您先前定義的資料夾中。可以透過更改副檔名來修改檔案格式，例如`.xlsx`如果您喜歡較新的 Excel 格式。
## 結論
現在你就擁有了！一旦您逐步分解，使用 Aspose.Cells for .NET 將矩形控制項新增至 Excel 工作表是一個簡單的流程。無論您需要添加形狀以增強視覺吸引力、突出顯示資料部分還是自訂報告，Aspose.Cells 都可以讓您靈活地以程式設計方式執行此操作。
本指南應該已經為您提供了開始使用 Aspose.Cells 將矩形等形狀新增至 Excel 工作表所需的所有知識。現在是時候進行實驗，看看您還可以使用這個強大的程式庫實現什麼目標！
## 常見問題解答
### 我可以使用 Aspose.Cells for .NET 添加其他形狀，例如圓形或線條嗎？  
是的，Aspose.Cells 允許您添加各種形狀，包括圓形、線條、箭頭等。
### 我還可以為矩形控制項設定哪些其他屬性？  
您可以自訂填滿顏色、線條顏色、透明度，甚至可以在矩形內添加文字。
### Aspose.Cells 與 .NET Core 相容嗎？  
是的，Aspose.Cells 支援 .NET Core、.NET Framework 和其他基於 .NET 的平台。
### 我可以相對於特定單元格定位矩形嗎？  
是的，您可以將矩形放置在特定的行和列中，或使用`PlacementType`來控制它的錨定方式。
### Aspose.Cells 是否有免費試用版？  
是的，您可以獲得[免費試用](https://releases.aspose.com/)在購買之前從網站上測試圖書館的功能。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
