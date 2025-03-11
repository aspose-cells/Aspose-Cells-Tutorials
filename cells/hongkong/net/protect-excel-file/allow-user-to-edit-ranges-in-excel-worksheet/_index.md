---
title: 允許使用者編輯 Excel 工作表中的範圍
linktitle: 允許使用者編輯 Excel 工作表中的範圍
second_title: Aspose.Cells for .NET API 參考
description: 允許使用者使用 Aspose.Cells for .NET 編輯 Excel 電子表格中的特定範圍。帶有 C# 原始程式碼的逐步指南。
weight: 10
url: /zh-hant/net/protect-excel-file/allow-user-to-edit-ranges-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 允許使用者編輯 Excel 工作表中的範圍

## 介紹

在使用 Excel 工作表時，靈活性通常是關鍵，尤其是當多個使用者需要存取權限來編輯特定區域而不影響整個工作表的資料完整性時。這就是 Aspose.Cells for .NET 的閃光點！在本教程中，我們將深入探討如何允許使用者編輯 Excel 工作表中的某些範圍，同時保護文件的其餘部分。讀完本文後，您不僅會掌握這些概念，還會有一個實際的範例可供使用。 

## 先決條件

在我們深入討論細節之前，讓我們確保您已具備開始使用所需的一切：

1. .NET 開發環境：您應該設定一個正常運作的 .NET 開發環境（可以是 Visual Studio 或您選擇的任何其他 IDE）。
2.  Aspose.Cells for .NET 函式庫：下載並安裝 Aspose.Cells 函式庫。你可以找到它[這裡](https://releases.aspose.com/cells/net/).
3. C# 基礎知識：熟悉 C# 程式設計將幫助您輕鬆瀏覽程式碼範例。
4. 了解 Excel 基礎：了解 Excel 的工作原理將為我們將要討論的功能奠定基礎。

一旦滿足了這些先決條件，您就可以開始了！

## 導入包

在開始編碼之前，我們需要確保我們的專案能夠識別 Aspose.Cells 命名空間。以下是導入必要包的方法：

```csharp
using System.IO;
using Aspose.Cells;
```

現在我們已經導入了所需的內容，讓我們逐步深入了解我們的教學。

## 第 1 步：設定文檔目錄

對於任何文件操作，定義保存文件的位置至關重要。讓我們設定工作目錄來儲存 Excel 檔案。

```csharp
//文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";

//如果目錄尚不存在，則建立該目錄。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

首先，更換`"YOUR DOCUMENT DIRECTORY"`以及您想要儲存檔案的路徑。此程式碼檢查目錄是否存在；如果沒有，它就會創建一個。

## 第 2 步：實例化新工作簿

工作目錄準備就緒後，就可以建立 Excel 工作簿了。 

```csharp
//實例化一個新的工作簿
Workbook book = new Workbook();
```

在這裡，我們建立一個新的實例`Workbook` Aspose.Cells提供的類，它允許我們操作Excel檔案。

## 第 3 步：存取預設工作表

每個新建立的工作簿都至少附帶一個工作表。讓我們訪問它。

```csharp
//取得第一個（預設）工作表
Worksheet sheet = book.Worksheets[0];
```

在此程式碼片段中，我們訪問工作簿的第一個工作表，我們將在後續步驟中對其進行操作。

## 第 4 步：取得允許編輯範圍

要啟用工作表的特定範圍進行編輯，我們需要訪問`AllowEditRanges`財產。

```csharp
//取得允許編輯範圍
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

此集合將使我們能夠管理工作表中可編輯的範圍。

## 步驟 5：定義保護範圍

接下來，讓我們定義要保護工作表的哪一部分，同時允許對指定範圍進行編輯。

```csharp
//定義保護範圍
ProtectedRange proteced_range;

//建立範圍
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];

//指定密碼
proteced_range.Password = "123";
```

在此步驟中，我們新增一個名為「r2」的新可編輯範圍，允許在從第1 行第1 列到第3 行第3 列的儲存格中進行編輯。範圍，確保只有授權使用者才能編輯修改它。

## 步驟 6：保護工作表

現在我們已經設定了可編輯範圍，我們需要保護工作表。

```csharp
//保護板材
sheet.Protect(ProtectionType.All);
```

此程式碼將保護整個工作表免受任何不必要的更改（我們剛剛指定的範圍除外）。

## 步驟 7：儲存 Excel 文件

讓我們儲存工作簿，以便我們可以看到 Excel 文件中反映的變更。

```csharp
//儲存 Excel 文件
book.Save(dataDir + "protectedrange.out.xls");
```

確保根據需要調整檔案名稱。這將使用我們配置的設定在您指定的目錄中建立一個 Excel 檔案。

## 結論

給你了！您已成功建立了 Excel 工作表，該工作表將編輯限制在指定範圍內，同時保護工作表的其餘部分。使用 Aspose.Cells for .NET 讓管理此類任務變得更加簡單和有效率。無論您是在開發複雜的應用程式還是只需要安全地管理數據，這些功能都可以顯著增強您的工作流程。

## 常見問題解答

### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的 .NET 函式庫，用於處理 Excel 文件，提供以程式設計方式建立、編輯和轉換電子表格等功能。

### 我可以套用多個可編輯範圍嗎？
絕對地！您可以致電`Add`方法上的`allowRanges`多次集合以指定多個可編輯範圍。

### 如果我忘記密碼會怎樣？
不幸的是，如果您忘記了可編輯範圍的密碼，則需要刪除保護或以可能涉及憑證的預定義方式存取檔案。

### Aspose.Cells 有免費版本嗎？
是的，Aspose 提供免費試用版，您可以在購買前探索其功能。

### 在哪裡可以找到有關 Aspose.Cells 的更多資訊？
您可以檢查[文件](https://reference.aspose.com/cells/net/)取得詳細指南和參考。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
