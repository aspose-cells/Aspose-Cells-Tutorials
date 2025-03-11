---
title: 在 .NET 中以程式設計方式建立新的資料透視表
linktitle: 在 .NET 中以程式設計方式建立新的資料透視表
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過我們的逐步指南，學習如何使用 Aspose.Cells 在 .NET 中以程式設計方式建立資料透視表。有效分析您的數據。
weight: 13
url: /zh-hant/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以程式設計方式建立新的資料透視表

## 介紹
建立資料透視表似乎是一項令人生畏的任務，尤其是當您以程式設計方式執行此操作時。但不要害怕！使用 Aspose.Cells for .NET，組合資料透視表不僅簡單，而且對於資料分析也非常強大。在本教學中，我們將逐步指導您如何在 .NET 應用程式中建立新的資料透視表。無論您是新增銷售、體育或任何其他業務指標的數據，本指南都將協助您立即啟動並執行數據透視表。

## 先決條件
在開始之前，讓我們確保一切準備就緒。您需要執行以下操作：

1. 安裝 .NET Framework：確保您的電腦上安裝了 .NET Framework。 Aspose.Cells 支援各種版本，但最好堅持使用最新版本。
2.  Aspose.Cells 函式庫：您需要擁有 Aspose.Cells 函式庫。你可以[在這裡下載](https://releases.aspose.com/cells/net/)或得到一個[臨時執照](https://purchase.aspose.com/temporary-license/)進行評估。
3. IDE 設定：準備好一個與 C# 相容的 IDE，例如 Visual Studio，您可以在其中啟動新專案。
4. C# 基礎：熟悉 C# 程式設計將幫助您順利進行操作，而不會陷入太大的困境。

你都準備好了嗎？偉大的！讓我們開始導入必要的套件。

## 導入包
首先，您需要將所需的命名空間匯入到您的 C# 專案中。開啟 C# 檔案並新增以下 using 指令：

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

這些命名空間可讓您存取我們將在本教學課程中使用的工作簿、工作表和資料透視表功能。

## 第 1 步：建立工作簿對象
建立工作簿是您旅程的開始。讓我們先實例化一個新工作簿並存取第一個工作表。

```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
//實例化 Workbook 物件
Workbook workbook = new Workbook();

//取得新增工作表的引用
Worksheet sheet = workbook.Worksheets[0];
```

在這一步中，我們創建一個`Workbook`代表我們的 Excel 檔案的實例並取得第一個工作表，這將是我們的資料透視表的遊樂場。

## 第 2 步：將資料插入儲存格
接下來，讓我們用一些範例資料填入工作表。我們將輸入不同運動項目、季度和銷售數據的行，以便為我們的數據透視表提供一些總結資訊。

```csharp
Cells cells = sheet.Cells;

//將值設為儲存格
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

//填充資料單元 = cells["A2"];
cell.PutValue("Golf");
// ....更多數據條目
```

在這裡，我們定義列標題並在每個標題下插入值。該數據將作為我們的數據透視表的來源，因此請確保它是有組織的！完成此區塊後，您將建立一個全面的資料集。

## 步驟 3：新增資料透視表
資料準備就緒後，就可以建立資料透視表了。我們將使用工作表中的資料透視表集合來新增新的資料透視表。

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

//將資料透視表新增至工作表
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

在此程式碼片段中，我們將一個資料透視表新增至引用我們的資料範圍（在本例中為儲存格 A1 到 C8）的工作表中。我們將資料透視表從儲存格 E3 開始放置，並將其命名為「PivotTable2」。很簡單，對吧？

## 步驟 4：自訂資料透視表
現在我們有了資料透視表，讓我們對其進行自訂以顯示有意義的摘要。我們可以控制資料透視表的行、列和資料區域中顯示的內容。

```csharp
//存取新新增的資料透視表的實例
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

//不顯示行的總計。
pivotTable.RowGrand = false;

//將第一個欄位拖曳到行區域。
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

//將第二個欄位拖曳至列區域。
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

//將第三個欄位拖曳至資料區域。
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

在此步驟中，我們告訴資料透視表隱藏行的總計，然後指定哪些欄位進入行、列和資料區域。運動名稱將填充行，季度將填充列，銷售資料將提供摘要。

## 第 5 步：儲存工作簿
最後，我們想要儲存新建立的工作簿以查看我們的勞動成果。

```csharp
//儲存 Excel 文件
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

只需提供正確的路徑，您就會將資料透視表輸出儲存到可以開啟和檢視的 Excel 檔案。

## 結論
使用 Aspose.Cells for .NET 以程式設計方式建立資料透視表可以顯著節省您的時間，尤其是在處理大型資料集時。您已經學習如何設定專案、匯入必要的套件、填充資料以及從頭開始建立可自訂的資料透視表。因此，下次當您被數字淹沒時，請記住本教程，讓 Aspose.Cells 為您完成繁重的工作。

## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的 .NET 程式庫，用於以程式設計方式建立和管理 Excel 電子表格。

### Aspose.Cells 是否有免費試用版？
是的，您可以獲得免費試用[這裡](https://releases.aspose.com/).

### 我可以自訂資料透視表的外觀嗎？
絕對地！您可以根據需要自訂資料透視表的格式、佈局甚至樣式。

### 在哪裡可以找到有關 Aspose.Cells 的更多範例和文件？
您可以檢查[文件](https://reference.aspose.com/cells/net/)取得全面的指南和範例。

### 我如何獲得 Aspose.Cells 的支援？
您可以透過以下方式獲得支持[Aspose論壇](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
