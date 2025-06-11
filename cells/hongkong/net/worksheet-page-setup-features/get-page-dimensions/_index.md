---
"description": "了解如何使用 Aspose.Cells for .NET 取得 Excel 工作表中的頁面尺寸。自訂 A2、A3、A4 和 Letter 紙張尺寸的逐步指南。"
"linktitle": "取得工作表的頁面尺寸"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "取得工作表的頁面尺寸"
"url": "/zh-hant/net/worksheet-page-setup-features/get-page-dimensions/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 取得工作表的頁面尺寸

## 介紹
如果您使用 Aspose.Cells for .NET 以程式設計方式處理 Excel 文件，有時可能需要存取和設定工作表的頁面尺寸。了解尺寸有助於佈局、列印和自訂 Excel 工作表以用於特定目的。在本文中，我們將探討如何使用 Aspose.Cells for .NET 在 Excel 中擷取和顯示各種頁面尺寸。我們將透過逐步教學確保您掌握所有詳細信息，從而自信地開始操作。
## 先決條件
在深入研究之前，請確保您已準備好完成本教學所需的一切。
1. Aspose.Cells for .NET：請確定您已安裝 Aspose.Cells for .NET。你可以 [在此下載庫](https://releases.aspose.com/cells/net/) 或透過 NuGet 在您的 .NET 專案中安裝它。
2. .NET 環境：相容的 .NET 開發環境（例如，Visual Studio）。
3. 許可證設定：若要使用 Aspose.Cells 的全部功能，請申請許可證。你可以 [申請免費臨時許可證](https://purchase.aspose.com/temporary-license/) 用於評估目的。
如果您是第一次評估，請從 Aspose.Cells 的免費試用版開始。
## 導入包
在我們進入程式碼之前，您需要將 Aspose.Cells 命名空間匯入到您的專案中以存取所有必要的類別和方法。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
讓我們將這個過程分解為簡單的步驟。在這裡，我們將存取不同的紙張尺寸，將它們應用到工作表，並列印每種尺寸。
## 步驟 1：建立工作簿實例
第一步是創建 `Workbook` 班級。該物件將作為我們的主要工作簿，其中包含我們可以操作的工作表。
```csharp
Workbook book = new Workbook();
```
想想 `Workbook` 作為 Excel 文件的主要容器。我們需要它來存取和控制單一工作表。
## 第 2 步：存取第一個工作表
接下來，讓我們訪問工作簿中的第一個工作表。預設情況下，新工作簿附帶一張工作表，因此我們可以使用索引直接引用它 `0`。
```csharp
Worksheet sheet = book.Worksheets[0];
```
這 `Worksheets` 收藏於 `Workbook` 允許我們透過索引存取每個工作表。在這裡，我們抓住第一張表來開始設定頁面尺寸。
## 步驟 3：將紙張尺寸設定為 A2 並顯示尺寸
現在我們可以訪問我們的工作表，讓我們將其紙張尺寸設為 A2。設定紙張尺寸對於在列印或匯出頁面之前格式化頁面很有用。一旦我們設定了紙張尺寸，我們將以英吋為單位列印頁面尺寸。
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
在這裡，我們改變 `PaperSize` 財產 `PaperA2`。設定尺寸後， `PageSetup.PaperWidth` 和 `PageSetup.PaperHeight` 檢索紙張的寬度和高度（以英吋為單位）。這讓我們快速了解頁面尺寸。
## 步驟 4：將紙張尺寸設定為 A3 並顯示尺寸
按照與上述相同的步驟，我們將頁面尺寸調整為 A3 尺寸。此變更對於稍大的列印件或在一頁上容納更多內容很有用。
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
A3 尺寸是 A4 尺寸的兩倍，因此非常適合用於大型表格或詳細圖表。更改紙張尺寸有助於相應地調整工作表佈局。
## 步驟 5：將紙張大小設定為 A4 並顯示尺寸
現在，我們將紙張尺寸設定為 A4。這是列印文件最常用的頁面尺寸。隨後我們將顯示更新後的尺寸。
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
如果您的目標是標準文件格式，A4 通常是最合適的尺寸。了解尺寸有助於調整內容佈局以避免列印問題。
## 步驟 6：將紙張大小設定為信紙並顯示尺寸
最後，我們將紙張尺寸設定為北美常用的 Letter 格式。讓我們最後一次列印尺寸。
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
北美的文件廣泛使用 Letter 尺寸，因此設定此尺寸有助於與那裡的團隊或客戶合作。
## 結論
在本教學中，我們介紹如何使用 Aspose.Cells for .NET 設定和擷取不同紙張尺寸的頁面尺寸。透過配置 A2、A3、A4 和 Letter 等頁面大小，您可以格式化 Excel 工作表以滿足特定的列印和佈局需求。這種對頁面尺寸的控制對於專業報告和簡報尤其有價值，因為它可以確保您的內容完美地適合每個頁面尺寸。
## 常見問題解答
### 如何在 Aspose.Cells 中更改頁面的方向？  
您可以使用 `PageSetup.Orientation` 屬性，將其設為 `PageOrientationType.P或者trait` or `PageOrientationType。Landscape`.
### 我可以在 Aspose.Cells 中設定自訂頁面尺寸嗎？  
是的，您可以透過調整頁邊距和縮放選項來設定自訂頁面尺寸 `PageSetup` 以獲得更好的控制。
### Aspose.Cells 中的預設紙張尺寸是多少？  
預設紙張尺寸通常為 A4。但是，這可能取決於區域設置，並且可以根據需要進行調整。
### 是否可以在 Aspose.Cells 中預覽頁面佈局？  
雖然 Aspose.Cells 不提供圖形預覽，但您可以以程式設計方式設定佈局並在 Excel 中使用列印預覽。
### 如何安裝 Aspose.Cells for .NET？  
您可以使用 Visual Studio 中的 NuGet 套件管理器安裝 Aspose.Cells，或從 [Aspose.Cells下載頁面](https://releases。aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}