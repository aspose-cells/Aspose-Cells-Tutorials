---
title: 將 Spinner 控制項新增至 Excel 中的工作表
linktitle: 將 Spinner 控制項新增至 Excel 中的工作表
second_title: Aspose.Cells .NET Excel 處理 API
description: 在此逐步教學中，了解如何使用 Aspose.Cells for .NET 將 Spinner 控制項新增至 Excel 工作表。
weight: 23
url: /zh-hant/net/excel-shapes-controls/add-spinner-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將 Spinner 控制項新增至 Excel 中的工作表

## 介紹
如果您正在使用 .NET 深入研究 Excel 自動化的世界，您可能會發現電子表格中需要更多的互動式控制項。 Spinner 就是此類控制項之一，它允許使用者輕鬆增加或減少值。在本教學中，我們將探討如何使用 Aspose.Cells for .NET 將 Spinner 控制項新增至 Excel 工作表。我們會將其分解為易於理解的步驟，以便您可以無縫地遵循。 
## 先決條件
在我們進入程式碼之前，讓我們確保您已完成一切設定以獲得流暢的體驗：
1.  Aspose.Cells for .NET：請確保您擁有 Aspose.Cells 函式庫。如果您尚未安裝，可以從以下位置取得最新版本[下載連結](https://releases.aspose.com/cells/net/).
2. Visual Studio：您應該安裝了可以正常運作的 Visual Studio 或您喜歡的任何其他 .NET IDE。
3. C#基礎知識：熟悉C#程式設計將有助於您輕鬆理解程式碼片段。如果您剛開始，請不要擔心！我將引導您完成每個部分。
## 導入包
若要在專案中使用 Aspose.Cells，您需要匯入必要的命名空間。設定環境的方法如下：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
這些命名空間可讓您存取 Aspose.Cells 的核心功能，包括工作簿操作和 Spinner 等形狀的繪圖功能。
現在我們已經介紹了先決條件並導入了必要的包，讓我們深入了解逐步指南。每個步驟都設計得清晰簡潔，以便您可以輕鬆實施。
## 第 1 步：設定您的專案目錄
在開始編碼之前，組織文件是一個很好的做法。讓我們為 Excel 檔案建立一個目錄。
```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
//如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
在這裡，我們指定文檔目錄的路徑。如果該目錄不存在，我們將建立它。這確保了我們產生的所有文件都有一個指定的目錄。
## 第 2 步：建立新工作簿
現在是時候建立一個 Excel 工作簿，我們將在其中新增 Spinner 控制項。
```csharp
//實例化一個新的工作簿。
Workbook excelbook = new Workbook();
```
這`Workbook`類別代表一個 Excel 文件。透過實例化它，我們創建了一個可供修改的新工作簿。
## 第 3 步：存取第一個工作表
我們將把 Spinner 加入工作簿中的第一個工作表。
```csharp
//取得第一個工作表。
Worksheet worksheet = excelbook.Worksheets[0];
```
該行存取工作簿中的第一個工作表（索引 0）。您可以有多個工作表，但對於本範例，我們將保持簡單。
## 第 4 步：使用細胞
接下來，讓我們處理工作表中的儲存格。我們將設定一些價值觀和風格。
```csharp
//取得工作表單元格。
Cells cells = worksheet.Cells;
//在 A1 儲存格中輸入字串值。
cells["A1"].PutValue("Select Value:");
//設定單元格的字體顏色。
cells["A1"].GetStyle().Font.Color = Color.Red;
//將字體文字設定為粗體。
cells["A1"].GetStyle().Font.IsBold = true;
//將數值輸入 A2 儲存格。
cells["A2"].PutValue(0);
```
在這裡，我們使用提示填充單元格 A1，應用紅色並將文字設定為粗體。我們還將單元格 A2 設定為初始值 0，它將連結到我們的微調器。
## 第 5 步：設定 A2 單元格的樣式
接下來，讓我們對 A2 單元格應用一些樣式，使其在視覺上更具吸引力。
```csharp
//將底紋顏色設定為純色背景的黑色。
cells["A2"].GetStyle().ForegroundColor = Color.Black;
cells["A2"].GetStyle().Pattern = BackgroundType.Solid;
//設定單元格的字體顏色。
cells["A2"].GetStyle().Font.Color = Color.White;
//將字體文字設定為粗體。
cells["A2"].GetStyle().Font.IsBold = true;
```
我們為儲存格 A2 添加帶有純色圖案的黑色背景，並將字體顏色設為白色。這種對比將使其在工作表上脫穎而出。
## 第 6 步：新增微調控件
現在，我們準備將 Spinner 控制項新增到我們的工作表中。
```csharp
//新增微調控制。
Aspose.Cells.Drawing.Spinner spinner = excelbook.Worksheets[0].Shapes.AddSpinner(1, 0, 1, 0, 20, 18);
```
此行將 Spinner 控制項新增至工作表。這些參數指定 Spinner 的位置和大小（行、列、寬度、高度）。
## 第 7 步：配置微調器屬性
讓我們自訂 Spinner 的行為來滿足我們的需求。
```csharp
//設定微調器的放置類型。
spinner.Placement = PlacementType.FreeFloating;
//設定控制項的連結單元格。
spinner.LinkedCell = "A2";
//設定最大值。
spinner.Max = 10;
//設定最小值。
spinner.Min = 0;
//設定控制項的增量變化。
spinner.IncrementalChange = 2;
//將其設定為 3-D 著色。
spinner.Shadow = true;
```
在這裡，我們設定 Spinner 的屬性。我們將其連結到單元格 A2，使其能夠控制此處顯示的值。最小值和最大值定義了微調器可以工作的範圍，而增量變更設定了每次點擊時值的變化量。添加 3D 陰影使其具有拋光的外觀。
## 步驟 8：儲存 Excel 文件
最後，讓我們儲存包含 Spinner 的 Excel 工作簿。
```csharp
//儲存 Excel 檔案。
excelbook.Save(dataDir + "book1.out.xls");
```
此指令將工作簿儲存到指定目錄。您可以根據需要更改檔案名稱。
## 結論
現在你就擁有了！您已使用 Aspose.Cells for .NET 成功將 Spinner 控制項新增至 Excel 工作表。此交互元素透過允許快速調整值來增強使用者體驗。無論您是建立動態報告工具還是資料輸入表單，Spinner 控制項都是有價值的補充。 
## 常見問題解答
### Excel 中的 Spinner 控制項是什麼？
Spinner 控制項可讓使用者輕鬆增加或減少數值，從而提供直覺的選擇方式。
### 我可以自訂 Spinner 的外觀嗎？
是的，您可以修改其大小、位置，甚至 3D 陰影以獲得更精美的外觀。
### 我需要許可證才能使用 Aspose.Cells 嗎？
 Aspose.Cells 提供免費試用，但生產使用需要付費許可證。查看[購買選擇權](https://purchase.aspose.com/buy).
### 我如何獲得 Aspose.Cells 的協助？
如需支持，請訪問[Aspose論壇](https://forum.aspose.com/c/cells/9)您可以在這裡提出問題並找到答案。
### 是否可以將多個 Spinner 加入同一個工作表中？
絕對地！您可以根據需要添加任意數量的微調器，方法是對每個控制執行相同的步驟。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
