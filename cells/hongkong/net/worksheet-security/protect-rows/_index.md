---
title: 使用 Aspose.Cells 保護工作表中的行
linktitle: 使用 Aspose.Cells 保護工作表中的行
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 保護 Excel 工作表中的資料列。透過行級保護保護您的資料並防止意外變更。
weight: 18
url: /zh-hant/net/worksheet-security/protect-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 保護工作表中的行

## 介紹
以程式設計方式處理 Excel 檔案通常是一項不僅需要資料操作還需要資料保護的任務。無論您需要保護敏感資料還是防止意外編輯，保護工作表中的行都是至關重要的一步。在本教學中，我們將深入探討如何使用 Aspose.Cells for .NET 來保護 Excel 工作表中的特定行。我們將逐步完成所有必要的步驟，從準備環境到以簡單易懂的方式實施保護功能。
## 先決條件
在開始保護工作表中的行之前，您需要做好以下幾件事：
1.  Aspose.Cells for .NET：請確保您的開發電腦上安裝了 Aspose.Cells for .NET。如果您還沒有這樣做，您可以輕鬆地從[Aspose Cells 下載頁面](https://releases.aspose.com/cells/net/).
2. Visual Studio 或任何 .NET IDE：要實作此解決方案，您需要設定一個開發環境。 Visual Studio 是不錯的選擇，但任何相容 .NET 的 IDE 都可以使用。
3. 基本 C# 知識：了解 C# 程式設計基礎將幫助您按照教學進行操作並修改範例程式碼以滿足您的需求。
4.  Aspose.Cells API 文件：熟悉[Aspose.Cells for .NET 文檔](https://reference.aspose.com/cells/net/)取得庫中使用的類別結構和方法的概述。
如果您已滿足先決條件，我們就可以直接開始實施。
## 導入包
首先，您需要匯入所需的套件。這些函式庫對於與 C# 專案中的 Excel 檔案進行互動至關重要。
```csharp
using System.IO;
using Aspose.Cells;
```
匯入必要的套件後，您就可以開始編碼了。 
現在，讓我們將該過程分解為更小的步驟，以便您輕鬆遵循。每個步驟都將專注於實施的特定部分，確保您可以快速理解並應用它。 
## 第 1 步：建立新工作簿和工作表
在套用任何保護設定之前，您需要建立新工作簿並選擇要使用的工作表。這將是您的工作文件。
```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
//如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
//建立一個新工作簿。
Workbook wb = new Workbook();
//建立一個工作表物件並取得第一個工作表。
Worksheet sheet = wb.Worksheets[0];
```
在此範例中，我們將使用單一工作表建立新工作簿（這是使用 Aspose.Cells 建立新工作簿時的預設設定）。然後，我們取得工作簿中的第一個工作表，它將作為行保護的目標。
## 第 2 步：定義 Style 和 StyleFlag 對象
下一步是定義樣式和樣式標誌物件。這些物件允許您修改單元格的屬性，例如它是鎖定還是解鎖。
```csharp
//定義樣式物件。
Style style;
//定義 styleflag 物件。
StyleFlag flag;
```
您將在後面的步驟中使用這些物件來自訂儲存格屬性並將其套用到您的工作表。
## 步驟 3：解鎖工作表中的所有列
預設情況下，Excel 工作表中的所有儲存格都會被鎖定。但是，當您保護工作表時，會強制執行鎖定狀態。為了確保只有特定的行或儲存格受到保護，您可以先解鎖所有列。如果您只想保護某些行，則此步驟至關重要。
```csharp
//循環遍歷工作表中的所有列並解鎖它們。
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
在此程式碼中，我們循環遍歷工作表中的所有 256 列（Excel 工作表最多有 256 列，索引從 0 到 255）並設定它們`IsLocked`財產給`false`。此操作可確保所有列均已解鎖，但稍後我們仍會鎖定特定行。
## 第四步：鎖定第一行
解鎖列後，下一步是鎖定要保護的特定行。在此範例中，我們將鎖定第一行。這可確保使用者無法在其他行保持解鎖狀態時對其進行修改。
```csharp
//取得第一行樣式。
style = sheet.Cells.Rows[0].Style;
//鎖定它。
style.IsLocked = true;
//實例化標誌。
flag = new StyleFlag();
//設定鎖定設定。
flag.Locked = true;
//將樣式套用到第一行。
sheet.Cells.ApplyRowStyle(0, style, flag);
```
在這裡，我們訪問第一行的樣式並設定其`IsLocked`財產給`true`。之後，我們使用`ApplyRowStyle()`方法將鎖定樣式套用至整行。您可以重複此步驟來鎖定您想要保護的任何其他行。
## 第 5 步：保護紙張
現在我們已經解鎖並鎖定了必要的行，是時候保護工作表了。此保護可確保任何人都無法修改已鎖定的行或儲存格，除非刪除保護密碼（如果提供）。
```csharp
//保護板材。
sheet.Protect(ProtectionType.All);
```
在此步驟中，我們使用以下方法對整個工作表套用保護`ProtectionType.All`。這種類型的保護意味著工作表的所有方面（包括鎖定的行和儲存格）都受到保護。如果需要，您也可以透過指定不同的保護類型來自訂此保護。
## 第 6 步：儲存工作簿
最後，我們需要在套用必要的樣式和保護後儲存工作簿。工作簿可以儲存為多種格式，例如Excel 97-2003、Excel 2010等。
```csharp
//儲存 Excel 檔案。
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
此程式碼行將工作簿儲存為 Excel 97-2003 格式並套用了變更。您可以根據需要從各種選擇中更改文件格式`SaveFormat`選項。
## 結論
現在你就擁有了！您已成功學習如何使用 Aspose.Cells for .NET 保護工作表中的資料列。透過執行上述步驟，您可以根據需要解鎖或鎖定任何行或列，並套用保護以確保資料的完整性。
## 常見問題解答
### 如何同時保護多行？  
您可以循環遍歷多行並將鎖定樣式單獨套用到每一行。只需更換`0`與您想要鎖定的行索引。
### 我可以為工作表保護設定密碼嗎？  
是的！您可以將密碼傳遞給`sheet.Protect()`強制密碼保護的方法。
### 我可以解鎖單元格而不是整列嗎？  
是的！您可以透過修改儲存格的樣式屬性來解鎖各個儲存格，而不是解鎖欄位。
### 如果我嘗試編輯受保護的行會發生什麼？  
當一行受到保護時，Excel 將阻止對鎖定的儲存格進行任何編輯，除非您取消保護工作表。
### 我可以連續保護特定範圍嗎？  
是的！您可以透過設定來鎖定連續的各個範圍`IsLocked`範圍內特定單元格的屬性。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
