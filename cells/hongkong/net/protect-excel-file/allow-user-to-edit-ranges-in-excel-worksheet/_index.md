---
"description": "允許使用者使用 Aspose.Cells for .NET 編輯 Excel 電子表格中的特定範圍。使用 C# 原始碼進行逐步指導。"
"linktitle": "允許使用者編輯 Excel 工作表中的範圍"
"second_title": "Aspose.Cells for .NET API參考"
"title": "允許使用者編輯 Excel 工作表中的範圍"
"url": "/zh-hant/net/protect-excel-file/allow-user-to-edit-ranges-in-excel-worksheet/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 允許使用者編輯 Excel 工作表中的範圍

## 介紹

在使用 Excel 工作表時，靈活性通常是關鍵——尤其是當多個使用者需要存取編輯特定區域而不損害整個工作表的資料完整性時。這就是 Aspose.Cells for .NET 閃耀的地方！在本教程中，我們將深入探討如何允許使用者編輯 Excel 工作表中的某些範圍，同時保護文件的其餘部分。讀完本文後，您不僅會掌握概念，而且還會有一個切實的例子可供參考。 

## 先決條件

在我們討論細節之前，讓我們確保您已準備好開始所需的一切：

1. .NET 開發環境：您應該設定一個可運行的 .NET 開發環境（可以是 Visual Studio 或您選擇的任何其他 IDE）。
2. Aspose.Cells for .NET Library：下載並安裝 Aspose.Cells 函式庫。你可以找到它 [這裡](https://releases。aspose.com/cells/net/).
3. C# 基礎知識：熟悉 C# 程式設計將幫助您輕鬆瀏覽程式碼範例。
4. 了解 Excel 基礎：了解 Excel 的工作原理將為我們將要討論的功能奠定基礎。

一旦滿足了這些先決條件，您就可以開始了！

## 導入包

在開始編碼之前，我們需要確保我們的專案識別 Aspose.Cells 命名空間。以下是導入必要包的方法：

```csharp
using System.IO;
using Aspose.Cells;
```

現在我們已經導入了我們需要的內容，讓我們逐步深入了解我們的教學。

## 步驟 1：設定文檔目錄

對於任何文件操作，確定保存文件的明確位置至關重要。讓我們設定工作目錄來儲存 Excel 檔案。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

首先，更換 `"YOUR DOCUMENT DIRECTORY"` 使用您想要儲存檔案的路徑。此程式碼檢查目錄是否存在；如果沒有，它會建立一個。

## 步驟 2：實例化新工作簿

工作目錄準備好後，就可以建立 Excel 工作簿了。 

```csharp
// 實例化新的工作簿
Workbook book = new Workbook();
```

在這裡，我們正在建立一個新的實例 `Workbook` Aspose.Cells 提供的類，它允許我們操作 Excel 檔案。

## 步驟 3：存取預設工作表

每個新建立的工作簿都至少附帶一個工作表。讓我們訪問它。

```csharp
// 取得第一個（預設）工作表
Worksheet sheet = book.Worksheets[0];
```

在此程式碼片段中，我們訪問工作簿的第一個工作表，我們將在後續步驟中對其進行操作。

## 步驟 4：取得允許編輯範圍

為了能夠編輯工作表的特定範圍，我們需要訪問 `AllowEditRanges` 財產。

```csharp
// 取得允許編輯範圍
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

該集合將允許我們管理工作表中哪些範圍是可編輯的。

## 步驟5：定義保護範圍

接下來，讓我們定義想要保護工作表的哪一部分，同時允許對指定範圍進行編輯。

```csharp
// 定義 ProtectedRange
ProtectedRange proteced_range;

// 建立範圍
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];

// 指定密碼
proteced_range.Password = "123";
```

在此步驟中，我們新增一個名為「r2」的新可編輯範圍，允許編輯從第 1 行第 1 列到第 3 行第 3 列的儲存格。此外，我們設定密碼來保護此範圍，確保只有授權使用者才能修改它。

## 步驟 6：保護工作表

現在我們已經設定了可編輯範圍，我們需要保護工作表。

```csharp
// 保護工作表
sheet.Protect(ProtectionType.All);
```

此程式碼將保護整個工作表免受任何不必要的更改，除了我們剛剛指定的範圍之外。

## 步驟 7：儲存 Excel 文件

讓我們儲存工作簿，以便我們可以在 Excel 文件中看到我們的變更。

```csharp
// 儲存 Excel 文件
book.Save(dataDir + "protectedrange.out.xls");
```

確保根據需要調整檔案名稱。這將使用我們配置的設定在指定的目錄中建立一個 Excel 檔案。

## 結論

就是這樣！您已成功建立了 Excel 工作表，該工作表將編輯限制在指定範圍內，同時保護工作表的其餘部分。使用 Aspose.Cells for .NET 使得管理這些類型的任務變得更加直接和有效率。無論您是開發複雜的應用程式還是只需要安全地管理數據，這些功能都可以顯著增強您的工作流程。

## 常見問題解答

### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的 .NET 程式庫，用於處理 Excel 文件，提供以程式設計方式建立、編輯和轉換電子表格等功能。

### 我可以套用多個可編輯範圍嗎？
絕對地！您可以致電 `Add` 方法 `allowRanges` 多次收集以指定多個可編輯範圍。

### 如果我忘了密碼怎麼辦？
不幸的是，如果您忘記了可編輯範圍的密碼，則需要刪除保護或以可能涉及憑證的預定義方式存取檔案。

### Aspose.Cells 有免費版本嗎？
是的，Aspose 提供免費試用，您可以在購買前利用它來探索其功能。

### 在哪裡可以找到有關 Aspose.Cells 的更多資訊？
您可以檢查 [文件](https://reference.aspose.com/cells/net/) 以獲得詳細的指南和參考。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}