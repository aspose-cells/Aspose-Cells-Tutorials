---
category: general
date: 2026-10-10
description: 使用 Aspose.Cells 於 C# 將 Excel 轉換為 PowerPoint 並設定列印範圍 – 學習如何匯出 Excel、設定列印範圍，以及產生
  PPTX 檔案。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: zh-hant
lastmod: 2026-10-10
og_description: 使用 Aspose.Cells 將 Excel 轉換為 PowerPoint。本教學示範如何設定列印區域、匯出 Excel，並在 C#
  中建立 PPTX 檔案。
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: 將 Excel 轉換為 PowerPoint – C# 開發者完整指南
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: 將 Excel 轉換為 PowerPoint 並設定列印範圍
url: /zh-hant/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將 Excel 轉換為 PowerPoint 並設定列印區域

如果您需要 **convert Excel to PowerPoint**，本指南會精確說明如何在 C# 中完成。先定義列印區域，即可控制每張投影片顯示的儲存格，最終的 PPTX 檔案會符合您的版面配置預期。此解決方案同時也回答了「how to export Excel」與「how to set print area」的問題，且使用相同的程式碼基礎。

在本教學中，您將會：

* 載入現有的工作簿。
* 為工作表設定列印區域（**set print area excel** 步驟）。
* 設定 PowerPoint 輸出的轉換選項。
* 在單一方法呼叫中產生 **convert excel to pptx** 檔案。

已提供所有必要的程式碼，您可以直接複製、貼上並立即執行。

## 前置條件

在開始之前，請確保您已具備以下條件：

| 前置條件 | 為何重要 |
|----------|----------|
| **.NET 6.0 或更新版本** | 此範例以 .NET 6+ 為目標，但任何支援 C# 10 的 .NET 版本皆可使用。 |
| **Aspose.Cells for .NET** | 此函式庫提供 `Workbook`、`ImageOrPrintOptions` 以及 `ConvertToPdf`（用於 PPTX）方法。請透過 NuGet 安裝：`dotnet add package Aspose.Cells` |
| **輸入的 Excel 檔案** | 本教學使用 `input.xlsx`。請將其放置於程式碼可參考的資料夾中。 |
| **輸出資料夾的寫入權限** | 程式會寫入 `output.pptx`。請確保該目錄已存在且具備寫入權限。 |

> **專業提示：** 若您處理多個工作表，請在轉換前為每個工作表重複列印區域的設定步驟。

## 步驟 1：建立新的 C# 主控台專案

在終端機或 PowerShell 視窗中執行以下指令：

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

此指令會建立一個名為 **ExcelToPowerPointDemo** 的新專案，並加入 Aspose.Cells 套件，該套件是 **how to export Excel** 至其他格式的核心相依性。

## 步驟 2：撰寫轉換程式碼

將 `Program.cs` 的內容取代為下方完整範例。程式碼示範 **convert excel to powerpoint**、說明 **how to set print area**，並產生 **convert excel to pptx** 檔案。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### 為何每個部分都很重要

* **載入工作簿** – 這是任何 **how to export Excel** 情境的第一步。`Workbook` 會將檔案讀入記憶體，讓您完整存取工作表、儲存格與格式設定。
* **設定列印區域** – 透過指定 `PageSetup.PrintArea`，您告訴 Aspose.Cells 要渲染哪些儲存格。這是 **set print area excel** 的核心；若未設定，整張工作表都會被匯出，可能產生巨大的、難以閱讀的投影片。
* **選擇 `SaveFormat.Pptx`** – `ImageOrPrintOptions` 物件允許您切換輸出格式。將 `SaveFormat` 設為 `Pptx` 即會啟動 **convert excel to pptx** 流程。
* **呼叫 `ConvertToPdf`** – 雖然方法名稱為 ConvertToPdf，但當 `SaveFormat` 為 `Pptx` 時，函式庫會輸出 PowerPoint 檔案。這是以單一呼叫 **convert excel to powerpoint** 的推薦方式。

## 步驟 3：執行程式

在專案資料夾中執行以下指令：

```bash
dotnet run
```

若設定皆正確，您應該會看到類似以下的主控台輸出：

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

在 Microsoft PowerPoint 或任何相容的檢視器中開啟 `output.pptx`。每張投影片對應工作表的列印頁面，且僅限於您所定義的範圍。

## 處理多個工作表

若您的工作簿包含多於一張工作表且希望每張工作表都有自己的投影片組，請遍歷集合：

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

此模式示範 **how to export Excel** 資料逐工作表匯出，同時為每張工作表 **setting print area**。

## 邊緣情況與最佳實踐建議

| 情況 | 建議做法 |
|------|----------|
| **非常大的工作表** | 縮小列印區域或提升 `HorizontalResolution`/`VerticalResolution`，以維持 PPTX 檔案大小在可接受範圍。 |
| **不同的頁面方向** | 在轉換前設定 `sheet.PageSetup.Orientation = PageOrientationType.Landscape;`。 |
| **自訂投影片尺寸** | 使用 `conversionOptions.OnePagePerSheet = false;`，並調整 `conversionOptions.Width` / `conversionOptions.Height`。 |
| **缺少輸入檔案** | 將載入程式碼包在 `try { … } catch (FileNotFoundException)` 區塊，以提供清晰的錯誤訊息。 |
| **非 ASCII 字元** | 確保工作簿以 UTF‑8 編碼儲存；Aspose.Cells 會自動處理 Unicode。 |

## 完整原始碼供參考

以下為完整程式碼，包含 `using` 指令與註解。請將其儲存為 `Program.cs`，放置於 **步驟 1** 所建立的專案內。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## 預期輸出

執行程式會產生一個 PowerPoint 檔案（`output.pptx`），其內容如下：

* 每個工作表的列印頁面對應一張投影片。
* 每張投影片僅顯示 **A1:G30** 內的儲存格。
* 保留 Excel 中的格式（字型、顏色、邊框）。

在 PowerPoint 中開啟檔案，以驗證版面配置與已定義的列印區域相符。

## 結論

您現在已了解如何使用 Aspose.Cells 在 C# 中 **convert Excel to PowerPoint**，同時精確 **set print area excel**。本教學涵蓋了 **how to export Excel**、示範了 **how to set print area**，並展示完整的 **convert excel to pptx**。

## 接下來您可以學習什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎延伸技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}