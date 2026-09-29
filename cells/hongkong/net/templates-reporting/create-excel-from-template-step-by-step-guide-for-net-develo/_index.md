---
category: general
date: 2026-05-04
description: 從範本建立 Excel，並將 JSON 映射至 Excel，支援動態工作表命名。了解如何從 JSON 填充 Excel，並在數分鐘內使用
  JSON 生成 Excel。
draft: false
keywords:
- create excel from template
- map json to excel
- populate excel from json
- dynamic worksheet naming excel
- generate excel using json
language: zh-hant
og_description: 快速從範本建立 Excel。本指南說明如何將 JSON 映射至 Excel、從 JSON 填充 Excel、使用動態工作表命名，以及使用
  JSON 產生 Excel。
og_title: 從範本建立 Excel – 完整 .NET 教學
tags:
- C#
- Aspose.Cells
- SmartMarker
- JSON
title: 從範本建立 Excel – .NET 開發人員逐步指南
url: /zh-hant/net/templates-reporting/create-excel-from-template-step-by-step-guide-for-net-develo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從範本建立 Excel – 完整 .NET 教程

曾經需要**從範本建立 Excel**，卻因為要同時處理 JSON 資料與工作表名稱而卡住嗎？你並不孤單。在許多報表專案中，範本負責版面配置，而 JSON 負載則提供實際的數值，讓兩者協同往往是一大難題。  

好消息是？只要幾行 C# 程式碼加上 Aspose Cells 的 SmartMarker 引擎，你就能**從 JSON 填充 Excel**、即時重新命名明細工作表，最後**使用 JSON 產生 Excel**，完全不需要操作介面。  

在本教學中，我們將逐步說明完整流程：載入範本、將 JSON 對映至 Excel、設定動態工作表命名，並儲存最終活頁簿。完成後，你將擁有一段可直接嵌入任何 .NET 服務的可重用程式碼。全程不需外部工具，純粹靠程式碼。

---

## 需求環境

- **Aspose.Cells for .NET**（v24.10 或更新版本）– 為 SmartMarker 提供功能的函式庫。
- 一個包含 SmartMarker 標籤（如 `{Master:Name}`、`{Detail:Item}`）的 **template.xlsx** 檔案。
- 一個符合主從結構的 **data.json** 檔案。
- Visual Studio 2022（或任何你偏好的 IDE），目標為 .NET 6 或更新版本。

就這樣。如果你已經備妥上述項目，就可以開始了。

---

## 從範本建立 Excel – 概觀

核心概念很簡單：將 Excel 檔案視為*範本*，讓 SmartMarker 用 JSON 中的值取代佔位符。此函式庫亦支援依據主欄位重新命名明細工作表，這正是 **dynamic worksheet naming excel** 發揮威力的地方。

以下是完整、可直接執行的程式碼。請隨意複製貼上至 Console 應用程式，並將路徑指向自己的檔案。

```csharp
// ------------------------------------------------------------
// Full example: create Excel from template using JSON data
// ------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains SmartMarker tags
            //    (e.g., {Master:Name} in the master sheet and {Detail:Item} in the detail sheet)
            string templatePath = @"C:\MyProject\Templates\template.xlsx";
            Workbook wb = new Workbook(templatePath);

            // 2️⃣ Read the JSON data that will populate the markers
            //    The JSON should match the structure expected by the template.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // 3️⃣ Configure the SmartMarker processor to rename the detail sheet
            //    dynamically based on the master record’s Name field.
            //    This demonstrates dynamic worksheet naming excel.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // 4️⃣ Execute the SmartMarker processing using the JSON data.
            //    This step maps JSON to Excel and populates every marker.
            wb.SmartMarkerProcessor.Execute(json);

            // 5️⃣ Save the processed workbook – now it’s a brand‑new file.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Excel file generated successfully at: " + outputPath);
        }
    }
}
```

> **預期結果：**  
> - 主工作表會顯示來自 `Master.Name` 的名稱。  
> - 明細工作表將重新命名為類似 `Detail_JohnDoe` 的名稱。  
> - 所有 `{Detail:Item}` 列將填入 JSON 中的 items 陣列。

---

## 將 JSON 對映至 Excel – 載入資料

在 SmartMarker 引擎發揮作用之前，JSON 必須**格式正確**且符合範本所使用的層級結構。典型的主從 JSON 如下所示：

```json
{
  "Master": {
    "Name": "John Doe",
    "Date": "2026-05-04"
  },
  "Detail": [
    { "Item": "Widget A", "Qty": 10, "Price": 2.5 },
    { "Item": "Widget B", "Qty": 5,  "Price": 5.0 }
  ]
}
```

**為什麼這很重要：**  
- 鍵 `Master` 與 `Detail` 直接對應到 `{Master:…}` 與 `{Detail:…}` 標籤。  
- 若 JSON 結構不符，SmartMarker 將找不到對應，儲存格將保持空白。  

**小技巧：** 使用線上驗證工具或 `System.Text.Json.JsonDocument.Parse(json)` 來驗證 JSON，及早發現語法錯誤。

---

## 從 JSON 填充 Excel – SmartMarker 設定

SmartMarker 會掃描活頁簿中的標籤，然後注入資料。**populate excel from json** 步驟實質上就是前面提到的 `Execute` 呼叫，但還有幾個可選設定值得說明：

| Setting | 功能說明 | 使用時機 |
|---------|----------|----------|
| `Options.CaseSensitive` | 將標籤名稱視為大小寫敏感。 | 當範本的大小寫混雜且需要嚴格匹配時。 |
| `Options.RemoveEmptyRows` | 刪除未收到資料的列。 | 當某些明細項目為可選，需保持最終工作表整潔時。 |
| `Options.EnableHyperlink` | 允許 JSON 中的超連結變為可點擊。 | 需要在報表中提供可點擊的 URL 時。 |

你可以這樣串接設定：

```csharp
wb.SmartMarkerProcessor.Options.CaseSensitive = true;
wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;
```

---

## 動態工作表命名 Excel – 設定明細工作表名稱

許多專案常見的較為複雜需求是 **dynamic worksheet naming excel**。與其使用固定的「Detail」工作表，你可能希望每份報表都帶有客戶名稱或訂單編號。

以下程式碼：

```csharp
wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";
```

正好達成此目的。占位符 `{Master.Name}` 會在 JSON 處理完畢後*替換*，因此新工作表名稱會變成 `Detail_JohnDoe`。  

**邊緣情況：** 若名稱包含工作表名稱不允許的字元（`:`、`\`、`/`、`?`、`*`、`[`、`]`），Aspose 會自動清理，但若需特定格式，可在 JSON 中先行清理字串。

---

## 使用 JSON 產生 Excel – 執行與儲存

程式碼最後兩行（`Execute` 與 `Save`）即是 **generate excel using json** 魔法發生的地方。底層上，Aspose 會將 JSON 解析成資料表，遍歷範本，並寫入輸出檔案。

若需在迴圈中產生多本活頁簿（例如每位客戶一份），只要將 `Workbook` 的實例化搬到迴圈內，並依需求更改輸出檔名：

```csharp
foreach (var customerJson in customers)
{
    Workbook wb = new Workbook(templatePath);
    wb.SmartMarkerProcessor.Options.DetailSheetNewName = $"Detail_{customerJson.Master.Name}";
    wb.SmartMarkerProcessor.Execute(customerJson);
    wb.Save($@"C:\Reports\Report_{customerJson.Master.Name}.xlsx");
}
```

此模式在批次報表服務中相當常見。

---

## 常見陷阱與專業技巧

- **缺少標籤：** 若儲存格仍顯示 `{Master:Name}`，表示標籤未被識別。請再次確認拼寫，且標籤必須位於儲存格內，而非註解中。
- **大型 JSON 負載：** 面對龐大資料集時，建議以串流方式讀取 JSON，或改用 `DataTable` 取代純字串，以降低記憶體壓力。
- **執行緒安全性：** `Workbook` 實例非執行緒安全。若執行平行作業，請為每個執行緒建立新實例。
- **檔案鎖定：** 確保範本未在 Excel 中開啟，否則程式執行時會拋出 `IOException`。

> **專業小技巧：** 將原始範本放在唯讀資料夾中保存副本，避免除錯時不小心覆寫。

---

## 完整範例回顧

以下再次呈現完整程式碼，並為每一行不明顯的部分加入內嵌註解：

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Path to the Excel template that contains SmartMarker tags.
            string templatePath = @"C:\MyProject\Templates\template.xlsx";

            // Load the workbook – this is the "create excel from template" step.
            Workbook wb = new Workbook(templatePath);

            // Read JSON data that maps directly to the template's tags.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // OPTIONAL: tweak SmartMarker behavior (case‑sensitivity, empty rows, etc.).
            wb.SmartMarkerProcessor.Options.CaseSensitive = false;
            wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;

            // Set up dynamic worksheet naming based on the master record's Name field.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // Run the SmartMarker engine – this is where we "populate excel from json".
            wb.SmartMarkerProcessor.Execute(json);

            // Save the newly generated workbook – the final "generate excel using json" step.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Workbook created at: " + outputPath);
        }
    }
}
```

執行此 Console 應用程式後，會產生 `output.xlsx`，其中明細工作表已重新命名，且所有資料皆已填入。

---

## 後續步驟與相關主題

- **匯出為 PDF：** 產生活頁簿後，可呼叫 `wb.Save("report.pdf", SaveFormat.Pdf);` 以提供 PDF 版。
- **圖表填充：** SmartMarker 亦支援圖表資料來源，只需將 JSON 陣列綁定至圖表的系列範圍。
- **條件格式化：** 在範本中使用 Excel 內建的規則，SmartMarker 替換後仍會保留。
- **效能調校：** 在高量情境下，可使用 `Clone` 重複利用單一 `Workbook` 實例，以避免重複的檔案 I/O。

歡迎嘗試不同的 JSON 結構、重新命名模式，甚至在一次執行中結合多個範本。使用 Aspose.Cells 的 **create excel from template** 具備高度彈性，能夠套用於發票、儀表板或任何報表需求。

---

## 視覺摘要

![從範本建立 Excel 工作流程，顯示 JSON → SmartMarker → 動態工作表命名](/images/create-excel-from-template-workflow.png "從範本建立 Excel 工作流程圖")

*(替代文字包含主要關鍵字以利 SEO)*

---

### 結語

我們已說明如何**從範本建立 Excel**、**將 JSON 對映至 Excel**、**從 JSON 填充 Excel**、使用**dynamic worksheet naming excel**，以及最終**使用 JSON 產生 Excel**。程式碼已完整，說明也闡述了每行程式碼的*原因*，讓你具備堅實基礎以建構更大型的報表管線。

有想實作的變化嗎？在下方留下評論，我們一起排除問題。祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}