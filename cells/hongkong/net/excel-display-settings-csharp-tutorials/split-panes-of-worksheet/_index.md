---
title: 工作表的分割窗格
linktitle: 工作表的分割窗格
second_title: Aspose.Cells for .NET API 參考
description: 透過我們的逐步指南了解如何在 Aspose.Cells for .NET 中分割工作表窗格。透過這個簡單的教學來改進 Excel 檔案導航。
weight: 130
url: /zh-hant/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 工作表的分割窗格

## 介紹

您準備好使用 Aspose.Cells for .NET 分割 Excel 工作表的窗格了嗎？想像一下：您有一個巨大的 Excel 工作表，並且您厭倦了不斷滾動回標題只是為了記住您正在使用哪一列。輸入「分割窗格」。這個方便的功能可讓您凍結工作表的一部分，使其更容易導航。無論您正在處理財務資料、庫存管理或大量資料集，分割窗格都可以將您的工作效率提高十倍。 

## 先決條件

在我們開始像電子表格精靈一樣分割窗格之前，讓我們先進行正確的設定。這是您需要的：

-  Aspose.Cells for .NET：請確保您已下載並安裝它。如果你還沒有，那就抓住它吧[這裡](https://releases.aspose.com/cells/net/).
- .NET Framework：本指南假設您在 .NET 環境中工作。
- Excel 工作簿：我們將使用範例 Excel 檔案來展示此功能的工作原理。
- 臨時或完整許可證：Aspose.Cells 需要許可證。如果您只是想嘗試一下，請獲取[免費臨時許可證](https://purchase.aspose.com/temporary-license/)以避免評估限制。

## 導入包

在深入研究程式碼之前，我們首先導入必要的名稱空間。如果不包含這些，你就無法真正在 Aspose.Cells 中執行任何操作。

```csharp
using System.IO;
using Aspose.Cells;
```

現在我們已經掌握了要點，讓我們繼續令人興奮的部分——分割窗格！

## 第 1 步：實例化工作簿

此過程的第一步是創建一個`Workbook`對象，它將代表您要修改的 Excel 檔案。在本例中，我們將從目錄載入檔案。這是您的畫布，是您可以施展魔法的 Excel 工作表。

在分割窗格之前，我們需要一個工作簿來使用！這一步就像在開始閱讀之前打開一本書一樣重要。

```csharp
//文檔目錄的路徑
string dataDir = "YOUR DOCUMENT DIRECTORY";

//實例化一個新工作簿並開啟範本文件
Workbook book = new Workbook(dataDir + "Book1.xls");
```

在上面的程式碼中，替換`"YOUR DOCUMENT DIRECTORY"`與 Excel 檔案所在的實際路徑。這`Workbook`類別將 Excel 檔案載入到記憶體中。

## 第 2 步：設定活動儲存格

載入工作簿後，就可以設定活動儲存格了。在 Excel 術語中，活動儲存格是目前選取或處於焦點的儲存格。在本教程中，我們將選擇單元格`A20`在第一個工作表中。

設定活動儲存格至關重要，因為窗格分割是從該活動儲存格開始的。這就像選擇在哪裡切第一塊披薩——選擇你的切片！

```csharp
//設定活動儲存格
book.Worksheets[0].ActiveCell = "A20";
```

這段程式碼使得`A20`活動單元格。這很重要，因為分割發生在這一點附近，就像 Excel 中的導航通常以特定單元格為中心一樣。

## 第 3 步：拆分工作表

現在活動單元格已設置，讓我們轉到有趣的部分 - 拆分工作表！這一步就是神奇發生的地方。您將能夠將工作表分為多個窗格，以便於檢視和導覽。

這是整個教程的核心。透過分割工作表，您可以建立單獨的窗格，讓您可以捲動 Excel 工作表的不同部分，而不會忽略標題或其他重要區域。

```csharp
//分割工作表視窗
book.Worksheets[0].Split();
```

隨著`Split()`方法，您告訴 Aspose.Cells 在活動儲存格處分割工作表（`A20`在這種情況下）。從此時起，Excel 在工作表中建立一個分割區，將各個窗格分開，以便您可以獨立導覽。

## 步驟 4：儲存工作簿

分割窗格後，剩下的就是儲存您的工作。最後一步將確保您的變更保存在指定的輸出檔案中。

如果你不保存的話，你所有的努力又有什麼用呢？儲存可確保您美麗的分割窗格保持完整以供將來使用。

```csharp
//儲存 Excel 文件
book.Save(dataDir + "output.xls");
```

在這裡，`Save()`方法將包含新分割的窗格的工作簿儲存到輸出 Excel 檔案。您所做的更改現在可供您或其他任何人使用。

## 結論

現在你就擁有了！您剛剛學習如何使用 Aspose.Cells for .NET 在 Excel 工作表中分割窗格。不再有無休止的滾動或丟失資料。此方法使處理大型 Excel 檔案不再那麼困難，而且效率更高。借助分割窗格的功能，您現在可以在處理複雜的電子表格時追蹤關鍵資料點。

## 常見問題解答

### 我可以分割兩個以上的窗格嗎？  
是的，您可以透過指定不同的活動儲存格並調用`Split()`方法。

### 分割窗格和凍結窗格有什麼區別？  
分割窗格可讓您在兩個窗格中獨立捲動。凍結窗格會鎖定標題或特定行/列，以便它們在捲動時保持可見。

### 套用後我可以刪除分割嗎？  
是的，您可以透過關閉並重新開啟工作簿或以程式方式重置它來刪除分割。

### 對於不同的 Excel 檔案格式（XLS、XLSX），分割窗格的運作方式是否相同？  
是的，`Split()`此方法適用於 XLS 和 XLSX 格式。

### 我可以在沒有許可證的情況下使用 Aspose.Cells 嗎？  
是的，但它有限制。為了獲得完整的體驗，最好使用[暫時的](https://purchase.aspose.com/temporary-license/)或者[付費許可](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
