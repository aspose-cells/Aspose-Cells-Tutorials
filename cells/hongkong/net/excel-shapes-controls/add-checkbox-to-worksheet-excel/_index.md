---
title: 將複選框新增至 Excel 中的工作表
linktitle: 將複選框新增至 Excel 中的工作表
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過我們的逐步教學（包含程式碼範例和說明）了解如何使用 Aspose.Cells for .NET 輕鬆地將複選框新增至 Excel 工作表。
weight: 18
url: /zh-hant/net/excel-shapes-controls/add-checkbox-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將複選框新增至 Excel 中的工作表

## 介紹
當談到在 Excel 中管理資料時，有無數的函數和方法可以簡化您的任務並增強您的電子表格。其中一個功能是複選框 - 一個漂亮的小工具，可讓使用者直接在 Excel 工作表中進行二元選擇。在本指南中，我們將引導您完成使用 .NET 的 Aspose.Cells 庫為 Excel 工作表新增複選框的過程。因此，請繫好安全帶，準備好進入 Excel 自動化世界的令人興奮的旅程吧！
## 先決條件
在我們深入研究編碼的細節之前，讓我們確保您擁有開始使用所需的一切。以下是先決條件：
- 視覺工作室：我們假設您已經使用 Visual Studio 設定了工作環境。如果沒有，您可以輕鬆地從以下位置下載[Visual Studio](https://visualstudio.microsoft.com/vs/).
- .NET Framework：確保您的系統上安裝了 .NET Framework。檢查 Aspose.Cells 與您的 .NET 版本的相容性。
-  Aspose.Cells for .NET：您需要下載 Aspose.Cells 函式庫並在專案中引用。您可以從以下位置下載：[這裡](https://releases.aspose.com/cells/net/).
- 對 C# 的基本了解：對 C# 程式設計的基本掌握將幫助您更輕鬆地理解範例。
在核對清單中的這些先決條件後，讓我們開始吧！
## 導入包
在開始編碼之前，我們需要將必要的套件匯入到我們的 C# 專案中。 Aspose.Cells 函式庫對於我們的任務至關重要，導入它是一件輕而易舉的事。只需按照以下步驟操作：
### 建立一個新的 C# 項目
- 開啟 Visual Studio 並建立一個新的 C# 控制台應用程式。
### 新增對 Aspose.Cells 的引用
- 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
- 選擇“管理 NuGet 套件”。
- 在 NuGet 套件管理器中，搜尋「Aspose.Cells」並安裝它。
### 導入命名空間
在 Program.cs 檔案的頂部，包含對 Aspose.Cells 命名空間的以下引用：
```csharp
using System.IO;
using Aspose.Cells;
```
現在，您已準備好開始編碼！

現在我們開始談正事吧。以下是如何使用 Aspose.Cells 將複選框新增至 Excel 工作表的逐步說明。
## 第 1 步：設定目錄
首先，我們需要確保保存 Excel 檔案的目錄存在。這是至關重要的一步，因為它可以防止我們嘗試儲存檔案時出現執行階段錯誤。
```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
//如果目錄尚不存在，則建立該目錄。
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
## 第 2 步：實例化新工作簿
接下來，我們需要建立一個新的工作簿實例。這將作為我們整個 Excel 文件的基礎。
```csharp
//實例化一個新的工作簿。
Workbook excelBook = new Workbook();
```
## 步驟 3：將複選框新增至工作表
現在，讓我們在工作簿的第一個工作表中新增一個複選框。您可以使用以下命令指定複選框的位置和大小`Add`方法：
```csharp
//將複選框新增至工作簿中的第一個工作表。
int index = excelBook.Worksheets[0].CheckBoxes.Add(5, 5, 100, 120);
```
## 第四步：取得複選框對象
新增複選框後，我們需要檢索複選框物件以進行進一步的自訂。
```csharp
//取得複選框物件。
Aspose.Cells.Drawing.CheckBox checkbox = excelBook.Worksheets[0].CheckBoxes[index];
```
## 第 5 步：設定複選框文本
什麼是沒有標籤的複選框？讓我們為複選框提供一些文本，以便用戶知道它的全部內容！
```csharp
//設定其文字字串。
checkbox.Text = "Click it!";
```
## 第 6 步：將複選框連結到儲存格
將複選框連結到特定單元格可以讓我們輕鬆追蹤其狀態。在本例中，我們將其連結到儲存格 B1。
```csharp
//將數值放入 B1 儲存格中。
excelBook.Worksheets[0].Cells["B1"].PutValue("LnkCell");
//將 B1 儲存格設定為複選框的連結儲存格。
checkbox.LinkedCell = "B1";
```
## 第 7 步：設定預設複選框值
如果您希望在開啟檔案時預設選取該複選框，您也可以輕鬆做到！
```csharp
//預設選取該複選框。
checkbox.Value = true;
```
## 步驟 8：儲存 Excel 文件
最後，完成所有這些步驟後，是時候將我們的傑作保存到指定目錄了。 
```csharp
//儲存 Excel 檔案。
excelBook.Save(dataDir + "book1.out.xls");
```
就像這樣，您已經建立了一個帶有功能複選框的 Excel 檔案！
## 結論
恭喜！您剛剛使用 Aspose.Cells for .NET 在 Excel 工作表中新增了一個複選框。這個功能強大的庫允許進行多種電子表格操作，而添加複選框只是冰山一角。現在，您可以使用互動式元素自訂 Excel 文檔，以增強使用者體驗。那麼，你還在等什麼？深入 Excel 自動化的世界，探索 Aspose.Cells 提供的所有可能性！
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的.NET 程式庫，可讓開發人員以程式設計方式建立、操作和管理 Excel 檔案。
### 我可以免費使用 Aspose.Cells 嗎？
是的，Aspose 提供 Aspose.Cells 的免費試用版。您可以從以下位置下載：[這裡](https://releases.aspose.com/).
### 我需要許可證才能使用 Aspose.Cells 嗎？
雖然您可以免費使用試用版，但需要付費許可證才能繼續使用並存取完整功能。您可以購買[這裡](https://purchase.aspose.com/buy).
### 在哪裡可以找到 Aspose.Cells 的文件？
完整的文檔可用[這裡](https://reference.aspose.com/cells/net/).
### 我如何獲得 Aspose.Cells 的支援？
如果您有任何疑問或需要協助，可以造訪 Aspose 支援論壇[這裡](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
