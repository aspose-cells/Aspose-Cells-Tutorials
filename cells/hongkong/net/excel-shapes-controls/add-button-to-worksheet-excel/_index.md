---
"description": "透過本逐步教學學習如何使用 Aspose.Cells for .NET 在 Excel 工作表中新增按鈕。使用互動式按鈕增強 Excel 電子表格。"
"linktitle": "在 Excel 中為工作表新增按鈕"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 Excel 中為工作表新增按鈕"
"url": "/zh-hant/net/excel-shapes-controls/add-button-to-worksheet-excel/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中為工作表新增按鈕

## 介紹
Excel 電子表格功能多樣，常用於管理數據，但有時需要額外的互動性。增強使用者體驗的最佳方法之一是為工作表新增按鈕。這些按鈕可以觸發巨集或引導用戶找到有用的連結。如果您是使用 Excel 檔案的 .NET 開發人員，Aspose.Cells for .NET 提供了一種以程式設計方式操作 Excel 工作簿的簡單方法，包括新增按鈕。
在本教學中，我們將引導您完成使用 Aspose.Cells for .NET 為 Excel 工作表新增按鈕的過程。我們將涵蓋每一個細節，從設定先決條件到逐步說明。讓我們開始吧！
## 先決條件
在學習本教學之前，請確保已安裝以下工具和軟體包：
- Aspose.Cells for .NET Library：您可以從 [這裡](https://releases。aspose.com/cells/net/).
- .NET 開發環境：確保您已安裝可執行的 .NET 環境（如 Visual Studio）。
- 對 C# 的基本了解：您應該熟悉 C# 程式設計的基礎知識。
- 許可證：您需要有效的許可證。如果你沒有，你可以獲得 [免費試用](https://releases.aspose.com/) 或申請 [臨時執照](https://purchase。aspose.com/temporary-license/).
讓我們繼續導入必要的套件。
## 導入包
在開始編碼之前，您需要將所需的套件匯入到您的 .NET 專案中。以下是一個簡單的程式碼片段，可協助您將 Aspose.Cells 匯入到您的專案中：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
現在我們已經導入了必要的套件，讓我們將範例分解為詳細的逐步指南。
## 步驟 1：設定工作簿和工作表
在第一步中，我們將建立一個新的 Excel 工作簿並取得第一個工作表的參考。
```csharp
// 定義文檔目錄的路徑。
string dataDir = "Your Document Directory";
// 如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// 建立一個新的工作簿。
Workbook workbook = new Workbook();
// 取得工作簿中的第一個工作表。
Worksheet sheet = workbook.Worksheets[0];
```

- 工作簿建立：我們首先建立一個新的 `Workbook` 對象，代表一個 Excel 檔案。
- 工作表參考： `Worksheets[0]` 命令檢索工作簿中的第一個工作表，我們將對其進行修改。
此步驟透過建立包含單一工作表的空白 Excel 檔案奠定基礎。
## 步驟 2：為工作表新增按鈕
接下來，我們將向工作表新增一個按鈕。這就是奇蹟發生的地方！
```csharp
// 在工作表中新增一個按鈕。
Aspose.Cells.Drawing.Button button = sheet.Shapes.AddButton(2, 0, 2, 0, 28, 80);
```

- AddButton 方法：此方法在工作表中指定的位置新增一個按鈕。參數定義按鈕的位置（行、列、x 偏移、y 偏移）和大小（高度、寬度）。
- 行和列：按鈕放置在第 2 行和第 0 列，沒有額外的偏移。
- 尺寸：按鈕的高度設定為28，寬度設定為80。
此步驟成功地向工作表添加了一個按鈕，但我們還沒有完成 - 讓我們對其進行自訂。
## 步驟3：設定按鈕屬性
現在是時候透過設定按鈕的文字、字體和位置來自訂按鈕的外觀了。
```csharp
// 設定按鈕的標題。
button.Text = "Aspose";
// 設定放置類型，即按鈕附加到儲存格的方式。
button.Placement = PlacementType.FreeFloating;
```

- 文字：我們將按鈕的標題設為「Aspose」。
- 位置：我們定義按鈕相對於工作表單元格的位置。 `FreeFloating` 允許按鈕獨立於單元格移動。
此步驟可個性化按鈕的標題和位置。
## 步驟 4：自訂按鈕字體
讓我們透過自訂字體屬性來為按鈕增添一些特色。
```csharp
// 設定字體名稱。
button.Font.Name = "Tahoma";
// 將標題字串設為粗體。
button.Font.IsBold = true;
// 將顏色設定為藍色。
button.Font.Color = Color.Blue;
```

- 字體名稱：我們將字體更改為“Tahoma”，這是一種簡潔而現代的字體。
- 粗體：我們將按鈕文字加粗以強調。
- 顏色：字體顏色設定為藍色，使按鈕文字突出。
此步驟增強了按鈕的外觀，確保其實既實用又美觀。
## 步驟 5：向按鈕新增超連結
您可以透過新增超連結使按鈕更加有用。
```csharp
// 設定按鈕的超連結。
button.AddHyperlink("https://www.aspose.com/”);
```

- AddHyperlink：我們使用此方法為按鈕新增可點擊的超連結。點擊後，該按鈕將導航至 Aspose 網站。
這一步驟增加了按鈕的互動性，使其不僅具有美觀性，還具有實用性。
## 步驟6：儲存Excel文件
一旦一切設定完畢，不要忘記儲存您的變更！
```csharp
// 儲存文件。
workbook.Save(dataDir + "book1.out.xls");
```

- 保存方法：我們使用 `Save` 方法將修改後的工作簿寫入新文件。該檔案將保存在指定的目錄中。
恭喜！現在，您已向 Excel 工作表新增了完全自訂的按鈕。
## 結論
在 Excel 工作表中新增按鈕可以大大增強電子表格的功能，使其更具互動性和使用者友善性。使用 Aspose.Cells for .NET，您只需幾行程式碼即可實現這一點，正如我們在本教程中所示。
Aspose.Cells for .NET 是一個功能強大的函式庫，為 Excel 操作提供了無限的可能性。無論您是自動執行任務還是為電子表格新增功能，此程式庫都是您的首選解決方案。
如果你還沒有， [下載 Aspose.Cells for .NET 函式庫](https://releases.aspose.com/cells/net/) 並開始增強您的 Excel 文件。
## 常見問題解答
### 除了按鈕之外，我還可以在 Aspose.Cells for .NET 中使用其他形狀嗎？
是的，Aspose.Cells 允許您新增各種形狀，包括複選框、單選按鈕等。
### 我可以透過 Aspose.Cells 新增的按鈕觸發巨集嗎？
是的，您可以將按鈕連結到宏，但您需要在 Excel 中單獨處理宏程式碼。
### 如何讓按鈕隨儲存格自動調整大小？
使用 `PlacementType.Move` 屬性允許按鈕隨單元格調整大小。
### 是否可以在單一工作表上新增多個按鈕？
絕對地！您可以透過調用 `AddButton` 方法多次。
### 我可以進一步自訂按鈕外觀嗎？
是的，您可以修改許多屬性，包括背景顏色、邊框樣式等等。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}