---
category: general
date: 2026-10-01
description: 學習如何使用 Aspose.Cells 為 Excel 工作簿添加自訂屬性。本指南亦示範如何加入專案 ID 以及讀取自訂屬性。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: zh-hant
lastmod: 2026-10-01
og_description: 使用 Aspose.Cells 為 Excel 工作簿新增自訂屬性。請參考本完整教學，了解如何新增專案 ID、設定審閱者資訊，以及以程式方式讀取自訂屬性。
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: 為 Excel 工作簿新增自訂屬性 – 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何向 Excel 工作簿添加自訂屬性
url: /zh-hant/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何向 Excel 工作簿加入自訂屬性

如果您需要 **加入自訂屬性** 到 Excel 工作簿，本指南將示範如何使用 Aspose.Cells for .NET 完成此操作。您還會學會如何加入專案 ID、設定審閱者名稱，並在之後 **讀取自訂屬性**。

使用自訂中繼資料可將特定業務資訊直接嵌入試算表，讓您輕鬆追蹤擁有者、版本或其他情境，而無需維護額外的資料庫。以下步驟涵蓋完整的端對端工作流程，從建立工作簿到持久化新屬性。

## 前置條件

開始之前，請確保您已具備：

* 已安裝 .NET 6.0 或更新版本  
* 有效的 Aspose.Cells for .NET 授權（或免費試用）  
* Visual Studio 2022（或任何 C# IDE）  

除 `Aspose.Cells` 之外，無需其他 NuGet 套件。

## 步驟 1：設定專案並匯入命名空間

建立一個新的主控台應用程式，並加入 Aspose.Cells 參考：

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

`Aspose.Cells` 命名空間包含 `Workbook`、`Worksheet` 與 `CustomPropertyCollection` 類別，我們將會使用它們。

## 步驟 2：載入既有工作簿（或建立新工作簿）

您可以從既有的 `.xlsb` 檔案開始，或產生全新的工作簿。以下範例載入位於 `YOUR_DIRECTORY` 資料夾下的 **Data.xlsb** 檔案。

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

若檔案不存在，請將程式碼改為 `new Workbook();` 以建立空白工作簿。

## 步驟 3：向第一個工作表加入自訂屬性

主要操作是 **加入自訂屬性** 到工作表。Aspose.Cells 會將自訂屬性儲存在類似字典的集合中。

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

我們使用 `CustomProperties.Add` 而非 `CustomProperties["Name"] = value` 的原因在於，`Add` 方法會在屬性不存在時建立條目，且保證儲存正確的資料類型。此做法可防止因類型不符而在之後讀取時發生執行時錯誤。

## 步驟 4：以新屬性儲存工作簿

將中繼資料寫入後，將變更保存為新檔案，讓原始檔案保持不變。

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

此時 Excel 檔案已包含您定義的自訂中繼資料。您可以依照下一節的步驟驗證這些屬性。

## 步驟 5：從工作簿讀取自訂屬性

讀取 **Excel 自訂屬性** 的方式與前面的集合操作相同。以下程式碼示範如何取得剛才儲存的值。

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

`CustomPropertyCollection` 的索引子會回傳 `CustomProperty` 物件；存取其 `Value` 屬性即可取得原始類型的資料。先檢查 `null` 再進行型別轉換，可避免屬性缺失時拋出 `NullReferenceException`。

### 預期的主控台輸出

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

時間戳記會顯示您在第 3 步呼叫 `Add` 的確切時刻。

## 小技巧：更新既有的自訂屬性

若日後需要 **加入自訂** 資訊（例如變更審閱者），可使用 `CustomPropertyCollection` 的設定子：

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

此模式確保屬性會被更新或建立，適合自動化報表產生等迭代工作流程。

## 步驟 6：在 Excel 中驗證屬性（可選）

您也可以直接在 Excel 內檢視自訂屬性：

1. 開啟已儲存的 `DataWithProps.xlsb` 檔案。  
2. 前往 **檔案 → 資訊 → 屬性 → 進階屬性**。  
3. 點選 **自訂** 分頁。  

即可看到 `ProjectId`、`Reviewer` 與 `CreatedOn` 及其對應值。

## 完整範例程式

以下為結合前述所有片段的完整自包含程式。將其複製到 `Program.cs` 後執行，主控台會顯示取得的值。

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

執行此程式會產生前面示範的主控台輸出，並建立包含嵌入中繼資料的 `DataWithProps.xlsb`。

## 常見問題與邊緣情況

| 問題 | 解答 |
|---|---|
| **可以儲存非基本類型嗎？** | Aspose.Cells 支援 `string`、`int`、`double`、`DateTime` 與 `bool`。若需儲存複雜物件，請先序列化為 JSON 或 XML，再以字串形式存放。 |
| **如果工作簿有密碼保護該怎麼辦？** | 在存取 `CustomProperties` 前，以密碼開啟工作簿（`new Workbook(path, password)`）。解密後仍可存取屬性。 |
| **自訂屬性在格式轉換後會保留嗎？** | 轉存為其他格式（例如 `.xlsx`）時，只要目標格式支援，自訂屬性會被保留。 |
| **如何刪除自訂屬性？** | 使用 `worksheet.CustomProperties.Remove("PropertyName");` 即可將該條目從集合中移除。 |

## 往後的步驟

既然您已掌握 **加入自訂屬性**，可以進一步探索以下相關主題：

* **excel custom properties** 用於文件版本管理  
* **read custom properties** 從單一工作簿的多個工作表中讀取  
* 使用 **Aspose.Cells** 建立參考自訂中繼資料的樞紐分析表  
* 匯出工作簿為 PDF 同時保留自訂屬性  

試著使用不同的資料類型，將自訂屬性與儲存格註解結合，或將中繼資料整合至更大的文件管理系統。

---

**準備好自動化您的 Excel 報表了嗎？** 將上述程式碼加入您的專案，依需求調整屬性名稱，即可擁有具備自我說明功能的試算表，供後續處理使用。

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化您所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在專案中探索替代實作方式。

- [建立 Excel 工作簿 – 新增自訂屬性並儲存為 XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [使用 Aspose.Cells for .NET 讀取 Excel 自訂文件屬性](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [精通 Aspose.Cells .NET 的 Excel 自訂屬性以提升資料管理](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}