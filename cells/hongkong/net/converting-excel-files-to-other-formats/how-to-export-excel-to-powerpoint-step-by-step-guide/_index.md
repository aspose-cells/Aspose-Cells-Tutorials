---
category: general
date: 2026-02-21
description: 學習如何將 Excel 匯出至 PowerPoint，並保留可編輯的圖表。只需幾行 C# 程式碼，即可將 Excel 轉換為 PowerPoint，或從
  Excel 建立 PowerPoint。
draft: false
keywords:
- how to export excel
- convert excel to powerpoint
- create powerpoint from excel
- save excel as powerpoint
- how to export charts
language: zh-hant
og_description: 如何將 Excel 匯出至 PowerPoint 並保留可編輯的圖表。跟隨本指南，即可輕鬆將 Excel 轉換為 PowerPoint、從
  Excel 建立 PowerPoint，並將 Excel 儲存為 PowerPoint。
og_title: 如何將 Excel 匯出至 PowerPoint – 完整教學
tags:
- C#
- Aspose.Cells
- PowerPoint
title: 如何將 Excel 匯出至 PowerPoint – 步驟教學
url: /zh-hant/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何將 Excel 匯出至 PowerPoint – 完整教學

有沒有想過 **如何將 Excel 匯出** 到 PowerPoint 而不把您精美的圖表變成靜態圖片？您並不是唯一有此疑問的人。在許多報告流程中，每天都會需要 **將 Excel 轉換為 PowerPoint**，而常見的複製‑貼上技巧要麼會破壞版面配置，要麼會鎖定圖表資料。  

在本指南中，我們將逐步說明一個乾淨、程式化的解決方案，該方案 **從 Excel 建立 PowerPoint**，同時保持圖表可完全編輯。完成後，您將能夠在一次方法呼叫中 **將 Excel 儲存為 PowerPoint**，並清楚了解每一行程式碼的意義。

## 您將學到的內容

- 所需的完整 C# 程式碼，以 **匯出 Excel** 為 PPTX 檔案。
- 如何使用 `PresentationExportOptions` 讓圖表保持可編輯。
- 何時應優先使用此方法，而非手動匯出或第三方轉換工具。
- 前置條件、常見陷阱，以及幾個讓流程萬無一失的專業提示。

> **專業提示：** 如果您已在專案的其他地方使用 Aspose.Cells，這個方法幾乎不會增加任何負擔。

### 前置條件

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 或更新版本 | 現代執行環境，效能更佳，且完整支援 Aspose.Cells。 |
| Aspose.Cells for .NET (NuGet 套件) | 提供我們依賴的 `Workbook`、`PresentationExportOptions` 與 `SaveToPptx` API。 |
| 基本的 Excel 檔案，且至少包含一個圖表 | 只有在工作表中存在圖表物件時匯出才會生效，否則 PPTX 會是空白。 |
| Visual Studio 2022（或您喜歡的任何 IDE） | 讓除錯與套件管理更為便利。 |

如果您已備妥上述項目，讓我們開始吧。

## 如何將 Excel 匯出至 PowerPoint（圖表可編輯）

以下是 **完整、可執行** 的範例，展示整個流程。每個程式碼區塊之後都有說明，您可以直接複製貼上並依需求調整，無需在文件中搜尋。

### 步驟 1：安裝 Aspose.Cells

在專案資料夾中開啟終端機，執行以下指令：

```bash
dotnet add package Aspose.Cells
```

### 步驟 2：載入 Excel 活頁簿

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Step 2: Load the Excel workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

> **為何重要：** `Workbook` 是任何 Excel 操作的入口點。先載入檔案即可確保後續匯出使用您在 Excel 中看到的相同資料與格式。

### 步驟 3：設定 PPTX 匯出選項以保持圖表可編輯

```csharp
// Step 3: Configure PPTX export options to keep charts editable
PresentationExportOptions exportOptions = new PresentationExportOptions
{
    ExportEditableCharts = true   // This flag ensures charts stay editable in PowerPoint
};
```

如果省略 `ExportEditableCharts`，Aspose 會將圖表光柵化，變成平面圖片。這樣就失去了 **如何以可編輯形式匯出圖表** 的目的。

### 步驟 4：將第一個工作表儲存為 PPTX 檔案

```csharp
// Step 4: Export the first worksheet as a PPTX file using the options
workbook.Worksheets[0].PageSetup.SaveToPptx(@"YOUR_DIRECTORY\Editable.pptx", exportOptions);
```

`SaveToPptx` 方法會產生 PowerPoint 檔案，將每個 Excel 儲存格轉為文字方塊，將每個圖表轉為原生 PowerPoint 圖表物件。現在您可以在 PowerPoint 中開啟 `Editable.pptx`，雙擊任意圖表即可編輯其系列、座標軸或樣式。

### 步驟 5：驗證結果

1. 在 Microsoft PowerPoint 中開啟 `Editable.pptx`。
2. 找到對應於已匯出工作表的投影片。
3. 點擊圖表 → 選擇 **Edit Data** → 您應該會看到 Excel 風格的資料格。

如果圖表仍然是圖片，請再次確認 `ExportEditableCharts` 已設為 `true`，且來源工作表確實包含圖表物件。

![Diagram showing the flow from Excel to PowerPoint – how to export excel](/images/excel-to-pptx-flow.png "how to export excel example")

## 將 Excel 轉換為 PowerPoint – 常見陷阱與技巧

即使程式碼正確，開發者仍可能遇到問題。以下列出最常見的問題以及避免方式。

| Issue | Explanation | Fix |
|-------|-------------|-----|
| **No charts appear** | 工作簿可能沒有任何圖表物件，或圖表被隱藏。 | 確認圖表可見且未放在隱藏的工作表上。 |
| **Charts become images** | `ExportEditableCharts` 保持預設的 `false`。 | 如步驟 3 所示，明確設定 `ExportEditableCharts = true`。 |
| **File path errors** | 使用相對路徑卻未正確使用 `Path.Combine`。 | 建議使用 `Path.Combine(Environment.CurrentDirectory, "input.xlsx")`。 |
| **Large files cause OutOfMemory** | 匯出包含數千列與大量圖表的活頁簿會佔用大量記憶體。 | 在載入前使用 `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;`。 |
| **Version mismatch** | 使用較舊的 Aspose.Cells 版本，缺少 `PresentationExportOptions`。 | 升級至最新的 NuGet 套件。 |

### 加分項目：匯出多個工作表

如果您需要為多於一個工作表 **從 Excel 建立 PowerPoint**，可遍歷集合：

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string pptxPath = $@"YOUR_DIRECTORY\Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(pptxPath, exportOptions);
}
```

## 將 Excel 儲存為 PowerPoint – 進階情境

### 圖片與圖表並存

有時報告會同時包含圖表與公司標誌。Aspose 會將圖片視為一般圖形，因此會自動出現在 PPTX 中。若需控制層級順序，可在匯出前透過 `Shape` 屬性調整 Z‑index。

### 自訂投影片版面配置

PowerPoint 支援母片投影片。雖然 `SaveToPptx` 會建立預設版面，但您之後可以套用母片範本：

```csharp
using Aspose.Slides;

// Load the generated PPTX
Presentation pres = new Presentation(@"YOUR_DIRECTORY\Editable.pptx");

// Apply a master template (must be a .pptx file)
pres.Masters.AddFromFile(@"TEMPLATES\CorporateTemplate.pptx");

// Save the final version
pres.Save(@"YOUR_DIRECTORY\FinalPresentation.pptx", SaveFormat.Pptx);
```

此步驟讓您在 **將 Excel 轉換為 PowerPoint** 時，仍能保留企業品牌形象。

### 處理不同類型的圖表

大多數常見圖表類型（長條圖、柱狀圖、折線圖、圓餅圖）均能完美匯出。然而，對於 **如何匯出圖表** 如雷達圖或股票圖，可能需要在匯入後進行額外樣式調整。此時，您可以：

1. 如前所述匯出。
2. 使用 Aspose.Slides 以程式方式開啟 PPTX。
3. 調整圖表屬性（例如 `Chart.Type = ChartType.Radar`）。

## 重點回顧與後續步驟

我們已說明所有關於 **如何將 Excel 匯出** 為 PowerPoint 簡報且保留圖表可編輯性的知識。核心步驟——安裝 Aspose.Cells、載入活頁簿、設定 `PresentationExportOptions`，以及呼叫 `SaveToPptx`——只需幾行 C# 程式碼，即可取代整個手動流程。

### 接下來可以嘗試的項目

- 使用迴圈範例，將整個活頁簿 **轉換為 PowerPoint**。
- 嘗試 **從 Excel 建立 PowerPoint**，用於每晚自動更新的動態儀表板。
- 結合此匯出與 **Aspose.Slides**，套用自訂投影片母片並自動化品牌設定。
- 若想要單一 PPTX 包含多個工作表，可探索 `ExportAllSheetsAsPptx` 方法。

歡迎自行調整路徑、匯出選項，或將此邏輯嵌入更大型的報告服務中。唯一的限制就是您在資料視覺化上的創意。

*祝程式開發愉快！若在嘗試 **將 Excel 儲存為 PowerPoint** 時遇到任何問題，歡迎在下方留言或查閱 Aspose.Cells 文件以取得最新資訊。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}