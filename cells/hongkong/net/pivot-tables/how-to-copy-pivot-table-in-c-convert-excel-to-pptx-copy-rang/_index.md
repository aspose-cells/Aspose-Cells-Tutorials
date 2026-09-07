---
category: general
date: 2026-01-14
description: 如何使用 Aspose.Cells 複製樞紐分析表，並在同一教程中學習將 Excel 轉換為 PPTX、將範圍複製到其他工作簿，以及製作可編輯文字方塊的
  PPTX。
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: zh-hant
og_description: 如何複製樞紐分析表，然後將 Excel 轉換為 PPTX，將範圍複製到另一個工作簿，並使 PPTX 中的文字方塊可編輯——全部使用
  Aspose.Cells。
og_title: 如何在 C# 中複製樞紐分析表 – 完整的 Excel 到 PPTX 指南
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: 如何在 C# 中複製樞紐分析表 – 將 Excel 轉換為 PPTX、複製範圍並使文字方塊可編輯
url: /zh-hant/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中複製樞紐分析表 – 完整的 Excel 轉 PPTX 指南

從一個工作簿複製樞紐分析表到另一個工作簿是自動化 Excel 報表時常見的問題。在本教學中，我們將使用 **Aspose.Cells for .NET** 逐步說明三個實務情境：複製樞紐分析表範圍、將工作表匯出為可編輯文字方塊的 PPTX 檔案，以及透過 Smart Markers 將 JSON 陣列填入單一儲存格。  

您還會看到如何 **將 Excel 轉換為 PPTX**、**將範圍複製到另一個工作簿**，以及 **使 PPTX 文字方塊可編輯**，且不會破壞任何格式。完成後，您將擁有一套可直接放入任何 .NET 專案的即用程式碼。

> **專業提示：** 所有範例皆以 Aspose.Cells 23.12 為目標，但相同概念也適用於較早的版本，只需稍作 API 調整。

![顯示樞紐分析表複製、工作表匯出至 PPTX、以及插入 JSON 陣列的流程圖 – 複製樞紐分析表工作流程](how-to-copy-pivot-table-diagram.png)

---

## 您需要的環境

- Visual Studio 2022（或任何 C# IDE）
- .NET 6.0 或更新的執行環境
- Aspose.Cells for .NET NuGet 套件  
  ```bash
  dotnet add package Aspose.Cells
  ```
- 兩個範例 Excel 檔案（`source.xlsx`、`chartWithTextbox.xlsx`），放置於您自行管理的資料夾中（將 `YOUR_DIRECTORY` 替換為實際路徑）。

不需要其他函式庫；同一個 `Aspose.Cells` 程式集即可處理 Excel、PPTX 與 Smart Markers。

## 如何複製樞紐分析表並保留其資料

當您複製包含樞紐分析表的範圍時，預設行為僅貼上 **值**。若要保留樞紐分析表的定義，必須啟用 `CopyPivotTable` 旗標。

### 步驟說明

1. **載入包含樞紐分析表的來源工作簿**。  
2. **建立空的目標工作簿** – 用於接收複製的範圍。  
3. **使用 `CopyRange` 並將 `CopyPivotTable = true`**，讓樞紐定義隨資料一起傳遞。  
4. **將目標檔案儲存**至您需要的位置。

#### 完整程式碼範例

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**為什麼這樣有效：**  
`CopyOptions.CopyPivotTable` 告訴 Aspose.Cells 複製底層的 `PivotTable` 物件，而非僅其呈現的值。目標工作簿現在包含一個完整功能的樞紐分析表，您可以以程式方式重新整理或修改。

**邊緣情況：** 若來源工作簿使用外部資料來源，您可能需要在複製後嵌入資料或調整連線字串，否則樞紐分析表會顯示 “#REF!”。

## 將 Excel 轉換為 PPTX 並使文字方塊可編輯

將工作表匯出至 PowerPoint 可直接從資料建立投影片組合，十分方便。預設情況下，匯出的文字方塊會變成靜態圖形，但設定 `IsTextBoxEditable` 後即可改變此行為。

### 步驟說明

1. **開啟包含欲匯出圖表與文字方塊的工作簿**。  
2. **設定 `ImageOrPrintOptions`**，將 `SaveFormat = SaveFormat.Pptx`。  
3. **定義包含文字方塊的列印區域**。  
4. **啟用 `IsTextBoxEditable`**，使 PPTX 開啟後文字可編輯。  
5. **儲存 PPTX 檔案**。

#### 完整程式碼範例

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**結果：** 在 PowerPoint 中開啟 `result.pptx` – 您在 Excel 中放置的文字方塊現在會變成可直接輸入文字的普通文字方塊，無需手動重新建立。

**常見陷阱：** 若工作表含有與列印區域相交的合併儲存格，產生的投影片可能會偏移。請在匯出前調整列印區域或取消合併儲存格。

## 使用 Smart Markers 複製範圍至另一工作簿（JSON → 單一儲存格）

有時需要將 JSON 陣列嵌入單一 Excel 儲存格，例如在傳遞資料給期望 JSON 字串的下游系統時。Aspose.Cells 的 Smart Markers 在設定 `ArrayAsSingle = true` 時，可將陣列序列化為單一儲存格。

### 步驟說明

1. **載入包含 Smart Marker 佔位符（例如 `&=Items.Name`）的範本工作簿**。  
2. **準備資料物件** – 具備 `Items` 陣列的匿名型別。  
3. **建立 `SmartMarkerProcessor`**，並以 `ArrayAsSingle` 套用資料。  
4. **儲存已填充的工作簿**。

#### 完整程式碼範例

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**說明：**  
當 `ArrayAsSingle` 為 true 時，Aspose.Cells 會將 `Items.Name` 的每個元素串接成 JSON 風格的字串（`["A","B"]`），並寫入原本放置 Smart Marker 的儲存格。這樣可避免為每個陣列元素建立單獨的列。

**使用時機：** 適用於匯出設定表、API 載荷，或任何消費端期望緊湊 JSON 字串而非表格布局的情境。

## 其他提示與邊緣案例處理

| Scenario | What to Watch For | Suggested Fix |
|----------|-------------------|---------------|
| **大型樞紐分析表** | 複製大型樞紐快取時記憶體使用量激增。 | 在載入前使用 `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference`。 |
| **匯出至 PPTX 時包含影像** | 影像可能以低 DPI 轉為點陣圖。 | 將 `pptxOptions.ImageResolution = 300` 設定為較高解析度，以獲得更清晰的投影片。 |
| **Smart Marker JSON 格式化** | 特殊字元（`"`、`\`）會破壞 JSON。 | 手動轉義這些字元，或在提供給 Smart Markers 前使用 `JsonSerializer` 先行序列化。 |
| **跨不同 Excel 版本複製範圍** | 較舊的 `.xls` 檔案可能會遺失格式。 | 將目標儲存為 `.xlsx` 以保留現代功能。 |

## 重點回顧 – 如何複製樞紐分析表及更多操作

我們首先說明了 **如何複製樞紐分析表** 並保留其功能，接著示範了 **將 Excel 轉換為 PPTX**、**使 PPTX 文字方塊可編輯**，最後說明了使用 Smart Markers 將 JSON 陣列嵌入單一儲存格的 **如何將範圍複製到另一工作簿**。  

這三段程式碼皆為獨立可執行的範例；您只需將其貼入全新的主控台應用程式，調整檔案路徑，即可立即執行。

## 接下來可以做什麼？

- **探索其他匯出格式** – Aspose.Cells 亦支援 PDF、XPS 與 HTML。  
- **以程式方式重新整理樞紐分析表**，在複製後使用 `PivotTable.RefreshData()`。  
- **將 Smart Markers 與圖表結合**，產生可自動更新的動態儀表板。  

如果您有興趣 **以自訂投影片版面將工作簿儲存為 PPTX**，請參閱 Aspose.Cells 關於 `SlideOptions` 的文件。  

歡迎自行嘗試——更換列印區域、嘗試不同的 `CopyOptions`，或提供更複雜的 JSON 資料。此 API 足夠彈性，能應付大多數報表流程。

### 常見問答

**Q: `CopyPivotTable` 也會複製 slicer 嗎？**  
A: 不會直接複製。Slicer 是獨立的物件，複製後需要重新建立，或透過 `Worksheet.Shapes` 集合複製它們。

**Q: 能否將多個工作表匯出成單一 PPTX 投影片組合？**  
A: 可以。對每個工作表迴圈，使用相同的 `ImageOrPrintOptions` 呼叫 `Save`，並設定 `pptxOptions.StartSlideNumber` 以持續編號。

**Q: 若我的 JSON 陣列包含巢狀物件該怎麼辦？**  
A: 將 `ArrayAsSingle = false`，並使用自訂模板來迭代

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}