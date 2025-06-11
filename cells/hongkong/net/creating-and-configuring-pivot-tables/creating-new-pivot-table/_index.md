---
"description": "透過我們的逐步指南，學習如何使用 Aspose.Cells 在 .NET 中以程式設計方式建立資料透視表。有效地分析您的數據。"
"linktitle": "在 .NET 中以程式設計方式建立新的資料透視表"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 .NET 中以程式設計方式建立新的資料透視表"
"url": "/zh-hant/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以程式設計方式建立新的資料透視表

## 介紹
建立資料透視表似乎是一項艱鉅的任務，尤其是當您以程式設計方式執行時。但不要害怕！使用 Aspose.Cells for .NET，組合資料透視表不僅簡單，而且對於資料分析來說也非常強大。在本教學中，我們將逐步指導您如何在 .NET 應用程式中建立新的資料透視表。無論您新增的是銷售、體育或任何其他業務指標的數據，本指南都將協助您立即啟動並執行資料透視表。

## 先決條件
在深入研究之前，請確保您已做好一切準備。您需要執行以下操作：

1. 安裝 .NET Framework：確保您的機器上安裝了 .NET Framework。 Aspose.Cells 支援各種版本，但最好堅持使用最新版本。
2. Aspose.Cells 函式庫：您需要有 Aspose.Cells 函式庫。你可以 [點此下載](https://releases.aspose.com/cells/net/) 或得到 [臨時執照](https://purchase.aspose.com/temporary-license/) 以供評估。
3. IDE 設定：準備好與 C# 相容的 IDE，例如 Visual Studio，您可以在其中啟動新專案。
4. C# 基礎：熟悉 C# 程式設計將幫助您順利完成學習，而不會陷入困境。

你準備好了嗎？偉大的！讓我們開始導入必要的套件。

## 導入包
首先，您需要將所需的命名空間匯入到您的 C# 專案中。開啟 C# 檔案並新增以下使用指令：

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

這些命名空間可讓您存取我們將在本教學課程中使用的工作簿、工作表和資料透視表功能。

## 步驟 1：建立工作簿對象
建立工作簿是您的旅程的開始。讓我們先實例化一個新的工作簿並存取第一個工作表。

```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory";
// 實例化 Workbook 物件
Workbook workbook = new Workbook();

// 取得新新增工作表的引用
Worksheet sheet = workbook.Worksheets[0];
```

在此步驟中，我們建立一個 `Workbook` 代表我們的 Excel 檔案的實例並抓取第一個工作表，這將是我們的資料透視表的遊樂場。

## 步驟 2：將資料插入儲存格
接下來，讓我們用一些範例資料填入我們的工作表。我們將輸入不同運動、季度和銷售資料的行，以便我們的資料透視表能夠進行匯總。

```csharp
Cells cells = sheet.Cells;

// 設定單元格的值
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// 填充資料單元 = 儲存格["A2"];
cell.PutValue("Golf");
// ....更多數據條目
```

在這裡，我們定義列標題並在每個標題下插入值。這些數據將作為我們的數據透視表的來源，因此請確保它是有組織的！按照這個步驟，您將建立一個全面的資料集。

## 步驟3：新增資料透視表
資料準備好後，就可以建立資料透視表了。我們將使用工作表中的透視表集合來新增新的透視表。

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// 向工作表新增資料透視表
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

在此程式碼片段中，我們為工作表新增了一個引用資料範圍（在本例中為儲存格 A1 至 C8）的資料透視表。我們將資料透視表放置在儲存格 E3 的起始位置，並將其命名為「PivotTable2」。很簡單，對吧？

## 步驟 4：自訂資料透視表
現在我們有了資料透視表，讓我們對其進行自訂以顯示有意義的摘要。我們可以控制資料透視表的行、列和資料區域中顯示的內容。

```csharp
// 存取新新增的資料透視表實例
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// 不顯示行的總計。
pivotTable.RowGrand = false;

// 將第一個字段拖曳到行區域。
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// 將第二個字段拖曳到列區域。
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// 將第三個欄位拖曳到資料區域。
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

在此步驟中，我們告訴資料透視表隱藏行的總計，然後指定哪些欄位進入行、列和資料區域。體育項目名稱將填入行，季度將填入列，銷售數字將提供摘要。

## 步驟 5：儲存工作簿
最後，我們要儲存新建立的工作簿來查看我們的勞動成果。

```csharp
// 儲存 Excel 文件
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

只需提供正確的路徑，即可將資料透視表輸出儲存到您可以開啟和檢視的 Excel 檔案。

## 結論
使用 Aspose.Cells for .NET 以程式設計方式建立資料透視表可以顯著節省您的時間，尤其是在處理大型資料集時。您已經學習如何設定專案、匯入必要的套件、填充資料以及從頭開始建立可自訂的資料透視表。因此，下次您被數字淹沒時，請記住本教程，讓 Aspose.Cells 為您完成繁重的工作。

## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的 .NET 程式庫，用於以程式設計方式建立和管理 Excel 電子表格。

### Aspose.Cells 有免費試用版嗎？
是的，您可以免費試用 [這裡](https://releases。aspose.com/).

### 我可以自訂資料透視表的外觀嗎？
絕對地！您可以根據需要自訂資料透視表的格式、佈局甚至樣式。

### 在哪裡可以找到有關 Aspose.Cells 的更多範例和文件？
您可以檢查 [文件](https://reference.aspose.com/cells/net/) 以獲得全面的指南和範例。

### 如何獲得 Aspose.Cells 的支援？
您可以透過 [Aspose 論壇](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}