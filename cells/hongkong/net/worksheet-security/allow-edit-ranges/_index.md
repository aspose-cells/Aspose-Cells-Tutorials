---
title: 允許使用者使用 Aspose.Cells 編輯工作表中的範圍
linktitle: 允許使用者使用 Aspose.Cells 編輯工作表中的範圍
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解使用 Aspose.Cells for .NET 在 Excel 工作表中建立可編輯範圍，允許特定儲存格可編輯，同時透過工作表保護其餘儲存格。
weight: 10
url: /zh-hant/net/worksheet-security/allow-edit-ranges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 允許使用者使用 Aspose.Cells 編輯工作表中的範圍

## 介紹
Excel 文件通常包含敏感資料或結構化內容，您希望保護它們免受不必要的編輯。但是，您可能希望使某些特定儲存格或範圍可供某些使用者編輯。這就是 Aspose.Cells for .NET 作為一個強大的工具發揮作用的地方，它允許您保護整個工作表，同時仍授予指定範圍的編輯權限。想像一下共享一個預算電子表格，其中只有某些單元格可編輯，而其他單元格保持安全 - Aspose.Cells 使這變得簡單而高效。
## 先決條件
在深入編碼部分之前，讓我們確保您擁有所需的一切：
-  Aspose.Cells for .NET：請確定您已安裝 Aspose.Cells for .NET 程式庫。你可以下載它[這裡](https://releases.aspose.com/cells/net/).
- 開發環境：Visual Studio 或任何與 C# 相容的 IDE。
- .NET Framework：4.0 或更高版本。
- 許可證：考慮取得許可證以避免試用限制。您可以獲得[臨時許可證在這裡](https://purchase.aspose.com/temporary-license/).
## 導入包
確保在程式碼開頭包含必要的 Aspose.Cells 命名空間：
```csharp
using System.IO;
using Aspose.Cells;
```
這將確保您可以存取在 Excel 檔案中設定受保護範圍所需的所有類別和方法。
現在基礎工作已經就位，讓我們一步一步地詳細瀏覽程式碼。
## 第 1 步：設定目錄
在處理檔案之前，您需要設定儲存 Excel 檔案的目錄。這可確保您的文件組織良好並安全儲存。
```csharp
//定義文檔目錄的路徑
string dataDir = "Your Document Directory";
//檢查目錄是否存在，如果不存在則建立
bool isExists = Directory.Exists(dataDir);
if (!isExists)
{
    Directory.CreateDirectory(dataDir);
}
```
這部分程式碼確保您的目錄已準備好進行檔案操作。將其視為為接下來的一切奠定基礎。
## 步驟2：初始化工作簿和工作表
現在，讓我們繼續建立一個新工作簿並存取其預設工作表。
```csharp
//初始化一個新的工作簿
Workbook book = new Workbook();
//訪問工作簿中的第一個工作表
Worksheet sheet = book.Worksheets[0];
```
在這裡，我們初始化一個 Excel 工作簿並選擇其中的第一個工作表。此工作表將成為我們套用保護設定並定義可編輯範圍的畫布。
## 步驟 3：存取允許編輯範圍集合
Aspose.Cells 有一個功能叫做`AllowEditRanges`，它是可編輯的範圍的集合，即使工作表受到保護也是如此。
```csharp
//存取允許編輯範圍集合
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
此行設定對可編輯的特殊範圍集合的存取。將其視為工作表中的“VIP”區域，其中僅允許特定範圍繞過保護。
## 第 4 步：定義並建立保護範圍
現在，讓我們在工作表中定義並建立受保護的範圍。我們將指定該範圍的開始和結束儲存格。
```csharp
//定義 ProtectedRange 變數
ProtectedRange protectedRange;
//在集合中新增具有特定名稱和儲存格位置的新範圍
int idx = allowRanges.Add("EditableRange", 1, 1, 3, 3);
protectedRange = allowRanges[idx];
```
在此程式碼區塊中：
- `EditableRange`是分配給該範圍的名稱。
- 數字 (1, 1, 3, 3) 定義範圍座標，這表示它從儲存格 B2（第 1 行，第 1 列）開始到儲存格 D4（第 3 行，第 3 列）。
## 步驟5：為保護範圍設定密碼
為了增加安全性，您可以為受保護的範圍設定密碼。此步驟新增了額外的保護層，以確保只有授權使用者才能編輯範圍。
```csharp
//為可編輯範圍設定密碼
protectedRange.Password = "123";
```
在這裡，我們添加了一個密碼（`"123"`) 到保護範圍。此密碼要求提供了對誰可以進行更改的額外控制。
## 步驟 6：保護工作表
建立可編輯範圍後，下一步就是保護整個工作表。此保護設定將確保定義範圍之外的所有儲存格都已鎖定且無法編輯。
```csharp
//對工作表套用保護，使所有其他儲存格不可編輯
sheet.Protect(ProtectionType.All);
```
這`Protect`方法鎖定整個工作表，除了我們定義為可編輯的範圍。此步驟本質上創建了一個安全的「唯讀」環境，可以根據需要存取特定單元。
## 第 7 步：儲存工作簿
最後一步是保存工作簿，以便應用並儲存您的設定。
```csharp
//將Excel檔案儲存到指定目錄
book.Save(dataDir + "protectedrange.out.xls");
```
在此步驟中，我們將工作簿另存為“protectedrange.out.xls”，保存在我們在步驟1 中設定的目錄中。 ！
## 結論
Aspose.Cells for .NET 提供了一個管理 Excel 檔案內的保護和權限的絕佳方法。透過建立可編輯範圍，您可以保護工作表，同時仍允許存取特定區域。此功能對於協作文件特別有用，其中只有少數單元格應打開進行編輯，而其他單元格保持鎖定狀態。
## 常見問題解答
### 我可以為工作表新增多個可編輯範圍嗎？
是的，您可以透過簡單地重複以下操作來新增多個範圍`allowRanges.Add()`每個新範圍的方法。
### 如果我想稍後刪除受保護的範圍怎麼辦？
使用`allowRanges.RemoveAt()`方法與您要刪除的範圍的索引。
### 我可以為每個範圍設定不同的密碼嗎？
絕對地。每個`ProtectedRange`可以擁有自己獨特的密碼，為您提供精細的控制。
### 如果我保護工作表而沒有任何可編輯範圍，會發生什麼情況？
如果您不定義可編輯範圍，則整個工作表在受保護後將無法編輯。
### 受保護的範圍對其他使用者可見嗎？
不，保護是內部的。只有當使用者嘗試編輯受保護區域時，系統才會提示他們輸入密碼。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
