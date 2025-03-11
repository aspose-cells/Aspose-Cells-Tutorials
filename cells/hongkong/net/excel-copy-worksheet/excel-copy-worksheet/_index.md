---
title: Excel 複製工作表
linktitle: Excel 複製工作表
second_title: Aspose.Cells for .NET API 參考
description: 透過這個易於遵循的分步指南，了解如何使用 Aspose.Cells for .NET 複製 Excel 工作表。非常適合希望自動化 Excel 任務的 .NET 開發人員。
weight: 20
url: /zh-hant/net/excel-copy-worksheet/excel-copy-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 複製工作表

## 介紹

在數據處理領域，從管理銷售數據到組織項目數據，電子表格無所不在。但是，當需要自動化時，如何管理這些文件？那麼，如果您使用 .NET，Aspose.Cells 是一個以程式設計方式操作 Excel 檔案的絕佳工具。在本文中，我們將指導您使用 Aspose.Cells for .NET 在 Excel 檔案中複製工作表。當您需要在新工作表中複製資料而無需從頭開始時，這是一項常見任務。

所以，係好安全帶！我們將深入探討這個過程，但要以簡單、對話式且清晰的方式進行。

## 先決條件

在開始享受樂趣之前，讓我們確保您擁有開始學習本教程所需的一切。

### 安裝 Aspose.Cells for .NET
首先，如果您尚未安裝 Aspose.Cells for .NET，則需要下載並安裝它。您可以從他們的發布頁面獲取最新版本。

- [下載 .NET 版 Aspose.Cells](https://releases.aspose.com/cells/net/)

您可以在 Visual Studio 中使用 NuGet 或手動下載。如果您喜歡 NuGet 路線，只需執行以下命令：

```bash
Install-Package Aspose.Cells
```

### 獲得許可證
要完全解鎖 Aspose.Cells 的功能，最好獲得許可證。

- [購買許可證](https://purchase.aspose.com/buy)或者[申請臨時許可證](https://purchase.aspose.com/temporary-license/)

在沒有許可證的情況下使用該庫會將浮水印套用到您的輸出文件，因此請確保已準備好許可證！

### 設定您的開發環境
請確定您已安裝以下軟體：
- Visual Studio（或任何與 .NET 相容的 IDE）
- .NET Framework 或 .NET Core

一切安裝完畢後，讓我們開始編碼吧！

## 導入包

要使用 Aspose.Cells，您首先需要在專案中匯入所需的命名空間。以下是確保您擁有正確引用的程式碼片段：

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

現在我們已經完成了日常工作，讓我們開始真正的工作——在 Excel 工作簿中複製工作表。

## 第 1 步：定義您的目錄路徑
您需要做的第一件事是指定 Excel 檔案所在的目錄。這是將文件載入到專案中並保存修改後的工作簿的關鍵。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string InputPath = dataDir + "book1.xls";
```

- 這`dataDir`變數保存 Excel 檔案所在的目錄路徑。改變`"YOUR DOCUMENT DIRECTORY"`到實際的資料夾路徑。
- `InputPath`儲存我們將要處理的 Excel 檔案的位置（在本例中為「book1.xls」）。

使用動態路徑是一個好主意，這樣您就可以輕鬆地在環境（開發、暫存、生產）之間切換。

## 步驟 2：開啟 Excel 工作簿
接下來，讓我們使用 Workbook 類別來載入 Excel 文件，該類別代表整個 Excel 文件。

```csharp
Workbook wb = new Workbook(InputPath);
```

- 這`Workbook`物件載入位於以下位置的 Excel 文件`InputPath`。 Aspose.Cells 負責解析文件，因此您不必擔心 Excel 格式的複雜性。

## 第 3 步：存取工作表集合
每個工作簿都有多個工作表（將它們視為 Excel 文件中的選項卡）。要複製工作表，您首先需要存取這些工作表。

```csharp
WorksheetCollection sheets = wb.Worksheets;
```

- `WorksheetCollection`本質上是工作簿中所有工作表的清單。這就是我們將用來複製工作表的內容。

## 步驟 4：複製現有工作表
現在是令人興奮的部分——複製工作表！在這裡，我們將「Sheet1」的內容複製到新工作表中。

```csharp
sheets.AddCopy("Sheet1");
```

- 這`AddCopy`方法複製現有工作表（在本例中為「Sheet1」）並將新工作表新增至工作簿。
- 您可以更換`"Sheet1"`與您要複製的任何工作表名稱。

## 第 5 步：儲存工作簿
最後，複製工作表後，需要儲存更新的 Excel 檔案。我們將使用 Save 方法將變更儲存到新檔案。

```csharp
wb.Save(dataDir + "CopyWithinWorkbook_out.xls");
```

- 這`Save`方法將更新的工作簿寫入新文件（`CopyWithinWorkbook_out.xls` ）。您可以為輸出檔案選擇任何名稱，但請記住以適當的格式儲存它（例如，`.xls`, `.xlsx`）。

就是這樣！您已成功複製 Excel 檔案中的工作表。

## 結論

在 Aspose.Cells for .NET 中複製工作表不僅簡單而且有效率。只需幾行程式碼，您就可以自動執行重複的 Excel 任務，讓您在處理大型資料集或範本化報表時變得更加輕鬆。無論您是自動化財務報告、庫存日誌或其他需要 Excel 的內容，Aspose.Cells 都是您的首選解決方案。

## 常見問題解答

### 我可以使用 Aspose.Cells for .NET 一次複製多個工作表嗎？
不，您需要使用以下命令將它們一一複製`AddCopy`方法。但是，您可以輕鬆地循環瀏覽多張紙並按順序複製它們。

### Aspose.Cells for .NET 支援在不同工作簿之間複製工作表嗎？
是的，您可以透過開啟兩個工作簿並使用`AddCopy`他們之間的方法。

### Aspose.Cells 支援哪些 Excel 格式？
Aspose.Cells 支援多種 Excel 格式，包括`.xls`, `.xlsx`, `.csv`, `.html`，等等。

### 我需要許可證才能使用 Aspose.Cells for .NET 嗎？
是的，為了避免水印並釋放庫的全部潛力，您需要有效的許可證。但是，您可以請求[免費臨時許可證](https://purchase.aspose.com/temporary-license)購買前先試用。

### 我可以在 .NET Core 上執行 Aspose.Cells 嗎？
是的，Aspose.Cells 與 .NET Framework 和 .NET Core 完全相容，使其適用於跨平台應用程式。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
