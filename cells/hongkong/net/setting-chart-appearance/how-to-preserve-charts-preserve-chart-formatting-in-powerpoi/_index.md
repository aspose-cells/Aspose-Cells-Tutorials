---
category: general
date: 2026-07-03
description: 如何在 C# 中使用 Aspose.Slides 保留圖表，同時保持圖表格式。請遵循此一步一步的指南。
draft: false
keywords:
- how to preserve charts
- preserve chart formatting
language: zh-hant
og_description: 如何在 C# 中使用 Aspose.Slides 保留圖表及其格式。完整指南與程式碼。
og_title: 如何保留圖表 – 在 PowerPoint 中保留圖表格式 (C#)
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  headline: how to preserve charts – preserve chart formatting in PowerPoint C#
  type: TechArticle
- description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  name: how to preserve charts – preserve chart formatting in PowerPoint C#
  steps:
  - name: Open `EditableCharts.pptx` in PowerPoint.
    text: Open `EditableCharts.pptx` in PowerPoint.
  - name: Click any chart → “Edit Data”.
    text: Click any chart → “Edit Data”.
  - name: The Excel‑like data sheet should appear, letting you modify series values.
    text: The Excel‑like data sheet should appear, letting you modify series values.
  type: HowTo
- questions:
  - answer: Directly no—`ExportEditableObjects` only applies to the PPTX format. Convert
      first, then export.
    question: Does this work with PowerPoint 2003 (PPT) files?
  - answer: Absolutely. The same `ExportEditableObjects` flag keeps SmartArt, tables,
      and diagrams editable.
    question: Can I preserve other objects like SmartArt?
  - answer: 'The slide size is stored in the presentation metadata and isn’t affected
      by these options. No extra code needed. --- ## Next steps – keep the momentum
      Now that you’ve nailed **how to preserve charts**, try exploring: - **preserve
      chart formatting** for specific chart types (e.g., stacked bar vs. rad'
    question: What if I need to keep the original slide size?
  type: FAQPage
tags:
- Aspose.Slides
- C#
- PowerPoint
- chart automation
title: 如何保留圖表 – 在 PowerPoint C# 中保留圖表格式
url: /zh-hant/net/setting-chart-appearance/how-to-preserve-charts-preserve-chart-formatting-in-powerpoi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何保留圖表 – 在 PowerPoint C# 中保留圖表格式

有沒有想過在需要以程式方式匯出或操作 PowerPoint 檔案時，**如何保留圖表**？也許你曾嘗試快速儲存，結果圖表變成靜態圖片，失去了原本的可編輯性。  

在本教學中，我們將示範如何 **保留圖表** **以及** 使用 Aspose.Slides for .NET 保持其 **保留圖表格式** 完好。完成後，你將擁有一段可直接執行的 C# 程式碼，產生的 PPTX 中每個圖表皆為可編輯的 OOXML 物件——不再是平面化的圖片。

## 你將學到什麼

- 載入簡報、設定匯出選項並儲存，同時 **保留圖表格式** 的完整步驟。  
- `ExportEditableObjects` 旗標的重要性以及它如何防止圖表被光柵化。  
- 常見陷阱（例如舊版 PPT 格式、缺少字型）與快速解決方法。  

不需要任何 Aspose 的先前經驗；只要具備基本的 C# 環境以及一個你希望保持圖表可編輯性的 PowerPoint 檔案即可。

## 前置條件

- .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.7+）。  
- Aspose.Slides for .NET NuGet 套件（`Install-Package Aspose.Slides.NET`）。  
- 一個包含至少一個圖表的範例 `input.pptx`。  
- Visual Studio、Rider，或任何你喜歡的編輯器。  

---

## 步驟 1：安裝 Aspose.Slides 並建立新的主控台專案

首先，建立一個全新的主控台應用程式並加入此函式庫：

```bash
dotnet new console -n PreserveChartsDemo
cd PreserveChartsDemo
dotnet add package Aspose.Slides.NET
```

> **專業提示：** 若你位於企業代理伺服器之後，請加入 `--no-restore` 參數，之後再使用你的代理設定還原套件。

## 步驟 2：載入來源簡報 – 首個應用 **如何保留圖表** 的位置

使用 `Presentation` 類別開啟你的 PPTX 檔案。這正是 **如何保留圖表** 真正開始的地方。

```csharp
using Aspose.Slides;
using Aspose.Slides.Export;

namespace PreserveChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Load the source presentation
            // Replace the path with the location of your PPTX that contains charts.
            Presentation pres = new Presentation(@"YOUR_DIRECTORY\input.pptx");
```

請注意，我們尚未觸碰任何圖表物件——這是有意為之。以原始方式載入檔案可確保保留原始 XML 結構，這對於之後的 **保留圖表格式** 至關重要。

## 步驟 3：設定匯出選項 – **如何保留圖表** 的核心

Aspose.Slides 提供 `PresentationExportOptions` 類別。將 `ExportEditableObjects` 設為 `true` 會指示引擎保留圖表、表格與 SmartArt 為原生 OOXML 部分，而非將其平面化。

```csharp
            // Step 3: Configure export options to keep objects editable
            PresentationExportOptions exportOptions = new PresentationExportOptions
            {
                // This flag is the key to how to preserve charts.
                ExportEditableObjects = true
            };
```

為什麼會這樣運作？當 `ExportEditableObjects` 為 `false`（預設值）時，函式庫會為相容性將複雜物件光柵化，從而破壞 **保留圖表格式**。開啟此設定即可保留原始圖表 XML，讓最終使用者開啟 PPTX 時仍能編輯圖表資料。

## 步驟 4：使用已設定的選項儲存簡報

現在寫入輸出檔案。使用接受 `SaveFormat` 與 `exportOptions` 的同一個 `Save` 重載，可確保圖表保持可編輯。

```csharp
            // Step 4: Save the presentation with the configured options
            pres.Save(@"YOUR_DIRECTORY\EditableCharts.pptx", SaveFormat.Pptx, exportOptions);

            // Optional: Inform the user
            Console.WriteLine("Presentation saved with editable charts at: YOUR_DIRECTORY\\EditableCharts.pptx");
        }
    }
}
```

執行此程式會產生 `EditableCharts.pptx`。在 PowerPoint 中開啟，右鍵點擊圖表，即可看到常見的「Edit Data」選項——證明我們已成功掌握 **如何保留圖表** 與 **保留圖表格式**。

## 步驟 5：驗證結果並排除常見問題

### 驗證

1. 在 PowerPoint 中開啟 `EditableCharts.pptx`。  
2. 點擊任意圖表 → 「Edit Data」。  
3. 應會出現類似 Excel 的資料工作表，讓你修改系列數值。  

如果只看到靜態圖片，請再次確認：

- 你使用的是最新版本的 Aspose.Slides（較舊版本在 `ExportEditableObjects` 上有錯誤）。  
- 來源 PPTX 確實包含圖表物件（而非圖表的圖片）。  
- 沒有自訂佈景主題或字型替換導致圖表被渲染成圖片。  

### 邊緣情況

- **舊版 PPT（二進位）檔案：** 在套用匯出選項前先將其轉換為 PPTX（`pres.Save("temp.pptx", SaveFormat.Pptx)`）。  
- **大型簡報：** 記憶體使用量可能激增；請考慮使用 `Presentation` 的 `Dispose` 模式或串流 API 來處理巨型檔案。  
- **嵌入字型：** 若目標環境缺少原始字型，PowerPoint 可能會回退並將圖表渲染為圖片。請在來源檔案中嵌入字型或隨應用程式一起提供。  

---

## 常見問題 (FAQ)

**Q: 這能適用於 PowerPoint 2003（PPT）檔案嗎？**  
A: 直接不行——`ExportEditableObjects` 只適用於 PPTX 格式。需先轉換，再匯出。

**Q: 我可以保留其他物件，例如 SmartArt 嗎？**  
A: 當然可以。同樣的 `ExportEditableObjects` 旗標會讓 SmartArt、表格與圖表保持可編輯。

**Q: 如果需要保留原始投影片尺寸怎麼辦？**  
A: 投影片尺寸儲存在簡報的中繼資料中，不會受到這些選項的影響。無需額外程式碼。

---

## 下一步 – 持續前進

既然你已掌握 **如何保留圖表**，不妨進一步探索：

- 針對特定圖表類型（例如堆疊長條圖與雷達圖）進行 **保留圖表格式**。  
- 使用 `Chart` API 在儲存前以程式方式修改資料。  
- 匯出至其他格式（PDF、HTML），同時保持來源 PPTX 中的圖表可編輯。  

以上每項皆基於相同原則：保留底層 OOXML 完整性。

---

## 結論

我們已示範如何使用 Aspose.Slides for .NET 在 PowerPoint 檔案中 **保留圖表**，並展示了保持圖表完全可編輯所需的 **保留圖表格式** 步驟。上方完整的程式碼片段可直接嵌入任何 C# 專案，說明亦闡述了每行程式背後的 *原因*——讓你不僅僅是複製貼上，而是真正了解。

試著執行看看，調整匯出選項，很快你就能自動化簡報更新，同時永不失去微調圖表資料的能力。祝編程愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在本教學所示技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [如何使用 Aspose.Cells for .NET 將 Excel 圖表匯出為 PDF：逐步指南](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [如何使用 Aspose.Cells for .NET 將 Excel 圖表轉換為 SVG（逐步指南）](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [如何使用 Aspose.Cells for .NET 在 Excel 中建立圖表：開發者指南](/cells/english/net/charts-graphs/create-charts-excel-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}