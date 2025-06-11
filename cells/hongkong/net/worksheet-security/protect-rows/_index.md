---
"description": "了解如何使用 Aspose.Cells for .NET 保護 Excel 工作表中的資料列。使用行級保護來保護您的資料並防止意外變更。"
"linktitle": "使用 Aspose.Cells 保護工作表中的行"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "使用 Aspose.Cells 保護工作表中的行"
"url": "/zh-hant/net/worksheet-security/protect-rows/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 保護工作表中的行

## 介紹
以程式設計方式處理 Excel 檔案通常是一項不僅需要資料操作而且還需要資料保護的任務。無論您需要保護敏感資料還是防止意外編輯，保護工作表中的行都是至關重要的一步。在本教程中，我們將深入研究如何使用 Aspose.Cells for .NET 保護 Excel 工作表中的特定行。我們將以簡單易懂的方式介紹所有必要的步驟，從準備環境到實作保護功能。
## 先決條件
在開始保護工作表中的行之前，您需要先做好以下幾點：
1. Aspose.Cells for .NET：請確保您的開發機器上安裝了 Aspose.Cells for .NET。如果你還沒有這樣做，你可以從 [Aspose Cells下載頁面](https://releases。aspose.com/cells/net/).
2. Visual Studio 或任何 .NET IDE：要實作此解決方案，您需要建立一個開發環境。 Visual Studio 是一個很好的選擇，但任何與 .NET 相容的 IDE 都可以。
3. 基本 C# 知識：了解 C# 程式設計的基礎知識將幫助您跟隨教學課程並修改範例程式碼以滿足您的需求。
4. Aspose.Cells API 文件：熟悉 [Aspose.Cells for .NET 文檔](https://reference.aspose.com/cells/net/) 獲得庫中使用的類別結構和方法的概述。
如果您已滿足所有先決條件，我們就可以直接開始實施。
## 導入包
首先，您需要匯入所需的套件。這些程式庫對於在 C# 專案中與 Excel 檔案互動至關重要。
```csharp
using System.IO;
using Aspose.Cells;
```
一旦導入了必要的包，就可以開始編碼。 
現在，讓我們將這個過程分解成更小的步驟，以便您可以輕鬆遵循。每個步驟都將集中在實施的特定部分，確保您能夠快速理解和應用它。 
## 步驟 1：建立新的工作簿和工作表
在套用任何保護設定之前，您需要建立新的工作簿並選擇要使用的工作表。這將是您的工作文件。
```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory";
// 如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// 建立新工作簿。
Workbook wb = new Workbook();
// 建立一個工作表物件並取得第一個工作表。
Worksheet sheet = wb.Worksheets[0];
```
在此範例中，我們將建立一個包含單一工作表的新工作簿（這是使用 Aspose.Cells 建立新工作簿時的預設設定）。然後，我們抓取工作簿中的第一個工作表，這將是我們行保護的目標。
## 步驟 2：定義 Style 和 StyleFlag 對象
下一步是定義樣式和樣式標誌物件。這些物件可讓您修改儲存格的屬性，例如是否已鎖定或解鎖。
```csharp
// 定義樣式物件。
Style style;
// 定義 styleflag 物件。
StyleFlag flag;
```
您將在後續步驟中使用這些物件來自訂儲存格屬性並將其套用到您的工作表。
## 步驟 3：解鎖工作表中的所有列
預設情況下，Excel 工作表中的所有儲存格都會被鎖定。但是，當您保護工作表時，將強制執行鎖定狀態。為了確保只有特定的行或儲存格受到保護，您可以先解鎖所有列。如果您只想保護某些行，則此步驟至關重要。
```csharp
// 循環遍歷工作表中的所有列並將其解鎖。
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
在此程式碼中，我們循環遍歷工作表中的所有 256 列（Excel 工作表最多有 256 列，索引從 0 到 255），並設定它們的 `IsLocked` 財產 `false`。此操作可確保所有列都已解鎖，但我們稍後仍會鎖定特定的行。
## 步驟 4：鎖定第一行
解鎖列後，下一步是鎖定要保護的特定行。在這個例子中，我們將鎖定第一行。這確保了當其他行處於解鎖狀態時用戶無法修改它。
```csharp
// 取得第一行樣式。
style = sheet.Cells.Rows[0].Style;
// 鎖上。
style.IsLocked = true;
// 實例化標誌。
flag = new StyleFlag();
// 設定鎖定設定。
flag.Locked = true;
// 將樣式套用到第一行。
sheet.Cells.ApplyRowStyle(0, style, flag);
```
在這裡，我們訪問第一行的樣式並設定其 `IsLocked` 財產 `true`。之後，我們使用 `ApplyRowStyle()` 方法將鎖定樣式套用至整行。您可以重複此步驟來鎖定您想要保護的任何其他行。
## 步驟5：保護工作表
現在我們已經解鎖並鎖定了必要的行，是時候保護工作表了。這種保護可確保沒有人可以修改已鎖定的行或儲存格，除非他們刪除保護密碼（如果提供）。
```csharp
// 保護床單。
sheet.Protect(ProtectionType.All);
```
在此步驟中，我們使用 `ProtectionType.All`。這種保護意味著工作表的所有方面，包括鎖定的行和儲存格，都受到保護。如果需要，您也可以透過指定不同的保護類型來自訂此保護。
## 步驟 6：儲存工作簿
最後，我們需要在套用必要的樣式和保護後儲存工作簿。工作簿可以儲存為多種格式，例如Excel 97-2003，Excel 2010等。
```csharp
// 儲存 Excel 檔案。
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
此行程式碼將套用變更的工作簿儲存為 Excel 97-2003 格式。您可以根據需要選擇多種文件格式來變更文件格式 `SaveFormat` 選項。
## 結論
就是這樣！您已成功學習如何使用 Aspose.Cells for .NET 保護工作表中的資料列。按照上述步驟，您可以根據需要解鎖或鎖定任何行或列，並套用保護以確保資料的完整性。
## 常見問題解答
### 我怎樣才能同時保護多行？  
您可以循環遍歷多行並將鎖定樣式單獨套用到每一行。只需更換 `0` 使用您想要鎖定的行索引。
### 我可以為工作表保護設定密碼嗎？  
是的！您可以將密碼傳遞給 `sheet.Protect()` 強制密碼保護的方法。
### 我可以解鎖單元格而不是整個列嗎？  
是的！您無需解鎖列，而是可以透過修改樣式屬性來解鎖單一儲存格。
### 如果我嘗試編輯受保護的行會發生什麼？  
當某一行受到保護時，Excel 將阻止對鎖定的儲存格進行任何編輯，除非您取消對工作表的保護。
### 我可以連續保護特定範圍嗎？  
是的！您可以透過設定 `IsLocked` 範圍內特定單元格的屬性。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}