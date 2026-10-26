---
category: general
date: 2026-10-26
description: 學習如何使用 C# 將 Excel 圖表匯出至 PowerPoint。保持圖形可編輯，僅需幾行程式碼即可儲存為 PPTX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: zh-hant
lastmod: 2026-10-26
og_description: 使用 C# 將 Excel 圖表匯出至 PowerPoint。本指南示範如何保留可編輯的形狀，並使用 Aspose.Cells 儲存為
  PPTX。
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: 使用 C# 將 Excel 圖表匯出至 PowerPoint – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: 如何使用 C# 將 Excel 圖表匯出至 PowerPoint
url: /zh-hant/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# 將 Excel 圖表匯出至 PowerPoint

如果您需要 **將 Excel 圖表匯出至 PowerPoint**，本指南將帶您完成一個完整、可直接執行的解決方案。無論您是在建立報告儀表板或自動化投影片組合，您都會看到僅需幾行 C# 程式碼即可在轉換後保持圖表形狀完全可編輯。

在本教學中您將學會：

* 載入包含圖表的現有 Excel 活頁簿。  
* （可選）在轉換前微調活頁簿設定。  
* 將活頁簿儲存為 PowerPoint 檔案，同時保留形狀可編輯性。  

所有這些皆透過 **Aspose.Cells for .NET** 完成，該函式庫可在伺服器上執行 Excel 到 PowerPoint 的轉換，且不需安裝 Microsoft Office。

## 您需要的條件

| 需求 | 原因 |
|------|------|
| .NET 6.0 或更新版本 | 具備完整語言功能的現代執行環境 |
| Visual Studio 2022（或任何 IDE） | 方便的編輯器與除錯器 |
| **Aspose.Cells for .NET** NuGet 套件 | 提供 `Workbook` 類別與 `SaveFormat.Pptx` 支援 |
| 一個 Excel 檔案（`ChartAndShapes.xlsx`），內含至少一個圖表 | 作為您要匯出的圖表來源 |

> **專業提示：** 使用免費的 **Aspose.Cells Evaluation** 版本來測試程式碼；授權金鑰可移除評估水印。

```bash
dotnet add package Aspose.Cells
```

## 匯出 Excel 圖表至 PowerPoint – 完整工作流程

以下為端對端程式碼，完成匯出同時 **保留形狀可編輯性**。每一步都會詳細說明。

### 步驟 1：載入 Excel 活頁簿

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

`Workbook` 類別代表整個 Excel 檔案。載入檔案會將所有工作表、圖表與形狀讀入記憶體，這是進一步操作所必需的。

### 步驟 2：（可選）調整活頁簿設定

在大多數情況下，預設設定已足以產生乾淨的匯出結果。但若您需要變更計算模式、頁面設定，或隱藏特定工作表，可於此處處理。

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **為什麼重要：** 在轉換前調整設定可確保產生的投影片正確反映您想要的狀態，特別是當公式或隱藏工作表可能影響圖表資料時。

### 步驟 3：將活頁簿儲存為 PowerPoint 檔案

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

`SaveFormat.Pptx` 常數告訴 Aspose.Cells 輸出為 PowerPoint 簡報。函式庫會在內部將每個 Excel 圖表轉換為 PowerPoint 形狀，且在 Microsoft PowerPoint 中仍可完整編輯。

### 步驟 4：驗證結果

在 PowerPoint 中開啟 `Shapes.pptx`，然後：

1. 在任意投影片上選取圖表。  
2. 右鍵 → **Edit Data**。  
3. 確認圖表資料表出現，且您可以修改數值。

如果圖表開啟了 **Edit Data** 面板，表示轉換成功且 **形狀可編輯性** 已被保留。

![Export Excel charts to PowerPoint example](export-excel-charts-to-powerpoint.png){.img-fluid alt="匯出 Excel 圖表至 PowerPoint 範例"}

## 常見陷阱與避免方法

| 問題 | 原因 | 解決方案 |
|------|------|----------|
| 圖表顯示為靜態影像 | 使用不支援 PPTX 匯出的舊版 Aspose.Cells | 升級至最新的 Aspose.Cells 23.x 或更新版本 |
| PowerPoint 圖表資料遺失 | 匯出前活頁簿未完整計算 | 在 `Save` 前呼叫 `workbook.CalculateFormula()` |
| 形狀無法編輯 | 使用 `SaveFormat.Xlsx` 而非 `SaveFormat.Pptx` 進行儲存 | 確保在 `Workbook.Save` 時傳入 `SaveFormat.Pptx` |
| 執行時授權例外 | 未註冊授權的評估版 | 使用 `License license = new License(); license.SetLicense("Aspose.Cells.lic");` 註冊授權 |

### 邊緣案例：匯出多個工作表的獨立圖表

如果您的 Excel 檔案包含多個工作表，且每個工作表都有自己的圖表，Aspose.Cells 會自動為每個圖表建立一張獨立投影片。您可在儲存前重新排列工作表順序，以控制投影片的排列順序。

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### 效能提示：使用串流輸出而非寫入磁碟

在 Web API 中產生 PowerPoint 檔案時，請避免使用暫存檔，改以寫入 `MemoryStream` 的方式處理。

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## 完整、可執行範例

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**預期輸出：** 主控台會印出確認訊息，且 `Shapes.pptx` 於 PowerPoint 開啟時，每個 Excel 圖表皆會出現在各自的投影片上。選取圖表後即可編輯其資料，證明 **形狀可編輯性** 已被保留。

## 重點回顧與後續步驟

您現在已掌握如何使用 C# **將 Excel 圖表匯出至 PowerPoint**，同時保持圖表完全可編輯。此解決方案的核心在於使用 `Workbook.Save` 搭配 `SaveFormat.Pptx`，這是 **Aspose.Cells 匯出** 功能，讓您免除繁雜的 Open XML 處理。

接下來您可以探索：

* 使用 **Aspose.Slides** API 為投影片加入自訂標題或備註。  
* 同時匯出其他 Excel 物件（表格、圖片）與圖表。  
* 在背景服務中自動批次處理多個活頁簿。

歡迎自行嘗試上述可選設定，並將此模式整合至您的報告管線，以實現快速且可靠的 PowerPoint 產生。

## 接下來該學什麼？

以下教學與本指南所示技術緊密相關，能進一步深化您的應用：

- [Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [How to Export Excel to PowerPoint with C# – Complete Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [How to Export Shapes from Excel to PowerPoint – Complete Guide](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}