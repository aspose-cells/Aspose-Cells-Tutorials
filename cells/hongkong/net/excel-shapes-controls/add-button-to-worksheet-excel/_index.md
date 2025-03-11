---
title: 將按鈕新增至 Excel 中的工作表
linktitle: 將按鈕新增至 Excel 中的工作表
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過此逐步教學課程，了解如何使用 Aspose.Cells for .NET 將按鈕新增至 Excel 工作表。使用互動式按鈕增強 Excel 電子表格。
weight: 12
url: /zh-hant/net/excel-shapes-controls/add-button-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將按鈕新增至 Excel 中的工作表

## 介紹
Excel 電子表格用途廣泛，通常用於管理數據，但有時它們需要額外的互動性。增強使用者體驗的最佳方法之一是為工作表新增按鈕。這些按鈕可以觸發巨集或將使用者導航到有用的連結。如果您是使用 Excel 檔案的 .NET 開發人員，Aspose.Cells for .NET 提供了一種以程式設計方式操作 Excel 工作簿的簡單方法，包括新增按鈕。
在本教學中，我們將引導您完成使用 Aspose.Cells for .NET 在 Excel 中的工作表中新增按鈕的過程。我們將介紹從設定先決條件到逐步說明的所有細節。讓我們深入了解一下吧！
## 先決條件
在學習本教學之前，請確保已安裝以下工具和軟體包：
-  Aspose.Cells for .NET Library：您可以從以下位置下載它[這裡](https://releases.aspose.com/cells/net/).
- .NET 開發環境：確保您安裝了有效的 .NET 環境，例如 Visual Studio。
- 對 C# 的基本了解：您應該熟悉 C# 程式設計的基礎知識。
- 許可證：您需要有效的許可證。如果您沒有，您可以獲得一個[免費試用](https://releases.aspose.com/)或申請[臨時執照](https://purchase.aspose.com/temporary-license/).
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
## 第 1 步：設定工作簿和工作表
在第一步中，我們將建立一個新的 Excel 工作簿並取得第一個工作表的參考。
```csharp
//定義文檔目錄的路徑。
string dataDir = "Your Document Directory";
//如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
//建立一個新的工作簿。
Workbook workbook = new Workbook();
//取得工作簿中的第一個工作表。
Worksheet sheet = workbook.Worksheets[0];
```

- 建立工作簿：我們先建立一個新的工作簿`Workbook`對象，代表一個 Excel 檔案。
- 工作表參考：`Worksheets[0]`命令檢索工作簿中的第一個工作表，我們將對其進行修改。
此步驟透過使用單一工作表建立空白 Excel 檔案來奠定基礎。
## 第 2 步：向工作表新增按鈕
接下來，我們將向工作表新增一個按鈕。這就是魔法發生的地方！
```csharp
//將新按鈕新增至工作表。
Aspose.Cells.Drawing.Button button = sheet.Shapes.AddButton(2, 0, 2, 0, 28, 80);
```

- AddButton 方法：此方法在工作表中的指定位置新增一個按鈕。這些參數定義按鈕的位置（行、列、x 偏移、y 偏移）和大小（高度、寬度）。
- 行和列：按鈕放置在第 2 行第 0 列，沒有額外的偏移。
- 大小：按鈕的高度設定為 28，寬度設定為 80。
此步驟成功地向工作表添加了一個按鈕，但我們還沒有完成，讓我們自訂它。
## 步驟 3：設定按鈕屬性
現在是時候透過設定按鈕的文字、字體和位置來自訂按鈕的外觀了。
```csharp
//設定按鈕的標題。
button.Text = "Aspose";
//設定放置類型，即按鈕附加到儲存格的方式。
button.Placement = PlacementType.FreeFloating;
```

- 文字：我們將按鈕的標題設為「Aspose」。
- 放置：我們定義按鈕相對於工作表單元格的位置。`FreeFloating`允許按鈕獨立於單元格移動。
此步驟個人化按鈕的標題和位置。
## 第 4 步：自訂按鈕的字體
讓我們透過自訂字體屬性來為按鈕添加一些風格。
```csharp
//設定字體名稱。
button.Font.Name = "Tahoma";
//將標題字串設為粗體。
button.Font.IsBold = true;
//將顏色設定為藍色。
button.Font.Color = Color.Blue;
```

- 字體名稱：我們將字體更改為“Tahoma”，這是一種乾淨而現代的字體。
- 粗體：我們將按鈕文字設為粗體以強調。
- 顏色：字體顏色設定為藍色，使按鈕文字突出。
此步驟增強了按鈕的外觀，確保其功能性和視覺吸引力。
## 第 5 步：向按鈕新增超連結
您可以透過新增超連結使該按鈕更加有用。
```csharp
//設定按鈕的超連結。
button.AddHyperlink("https://www.aspose.com/");
```

- AddHyperlink：我們使用此方法為按鈕新增可點擊的超連結。點擊後，該按鈕將導航至 Aspose 網站。
此步驟增加了按鈕的互動性，使其功能超越了美觀。
## 第 6 步：儲存 Excel 文件
一切設定完畢後，不要忘記儲存變更！
```csharp
//儲存文件。
workbook.Save(dataDir + "book1.out.xls");
```

- 保存方法：我們使用`Save`方法將修改後的工作簿寫入新文件。文件將保存在指定目錄中。
恭喜！現在您已向 Excel 工作表新增了完全自訂的按鈕。
## 結論
在 Excel 工作表中新增按鈕可以大幅增強電子表格的功能，使其更具互動性和使用者友善性。使用 Aspose.Cells for .NET，您只需幾行程式碼即可實現此目的，如我們在本教程中所示。
Aspose.Cells for .NET 是一個功能強大的函式庫，為 Excel 操作提供了無限的可能性。無論您是自動化任務還是為電子表格新增功能，此程式庫都是您的首選解決方案。
如果你還沒有，[下載 Aspose.Cells for .NET 函式庫](https://releases.aspose.com/cells/net/)並開始增強您的 Excel 文件。
## 常見問題解答
### 除了 Aspose.Cells for .NET 中的按鈕之外，還可以使用其他形狀嗎？
是的，Aspose.Cells 允許您新增各種形狀，包括複選框、單選按鈕等。
### 我可以透過 Aspose.Cells 新增的按鈕觸發巨集嗎？
是的，您可以將按鈕連結到宏，但您需要在 Excel 中單獨處理宏程式碼。
### 如何讓按鈕隨儲存格自動調整大小？
使用`PlacementType.Move`屬性允許按鈕隨單元格調整大小。
### 是否可以在單一工作表上新增多個按鈕？
絕對地！您可以透過呼叫添加任意數量的按鈕`AddButton`方法多次。
### 我可以進一步自訂按鈕外觀嗎？
是的，您可以修改許多屬性，包括背景顏色、邊框樣式等等。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
