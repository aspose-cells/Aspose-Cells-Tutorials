---
category: general
date: 2026-03-22
description: 在 Excel 設定列印範圍，並將 Excel 轉換為可編輯形狀的 PowerPoint。學習如何重複標題列、從 Excel 建立 PowerPoint
  以及將 Excel 匯出為 pptx。
draft: false
keywords:
- set print area
- convert excel to powerpoint
- repeat title row
- create powerpoint from excel
- export excel to pptx
language: zh-hant
og_description: 在 Excel 設定列印區域，並將其轉換為帶有可編輯形狀的 PowerPoint 投影片。按照本完整指南，重複標題列並將 Excel
  匯出為 pptx。
og_title: 在 Excel 中設定列印區域 – 匯出至 PowerPoint 教學
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint generation
title: 在 Excel 中設定列印範圍並匯出至 PowerPoint – 一步一步指南
url: /zh-hant/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中設定列印區域並匯出至 PowerPoint – 完整程式教學

有沒有曾經需要在 Excel 工作表中 **設定列印區域**，然後把那一部分轉成 PowerPoint 投影片？你並不是唯一有此需求的人。在許多報表流程中，同樣的資料既要列印得好看，也要出現在簡報裡，通常會把第一列重複作為標題。好消息是，只要幾行 C# 程式碼，你就可以 **convert excel to powerpoint**，保持所有文字方塊可編輯，甚至自動 **repeat title row**。

在本指南中，我們將逐步說明你需要了解的所有內容：從設定列印區域到建立可直接在 PowerPoint 中編輯的 PPTX 檔案。完成後，你將能夠 **create powerpoint from excel**，將結果 **export excel to pptx**，並在任何 .NET 專案中重複使用相同程式碼。沒有魔法，只有清晰的步驟與完整、可執行的範例。

## 需要的環境

- **.NET 6.0** 或更新版本（此 API 亦支援 .NET Framework）
- **Aspose.Cells for .NET**（提供 `Workbook`、`ImageOrPrintOptions` 等類別的函式庫）
- 基本的 C# IDE（Visual Studio、Rider，或安裝 C# 擴充功能的 VS Code）
- 一個 Excel 檔案（`input.xlsx`），內含你想匯出的資料

就這樣——除了 Aspose.Cells 之外不需要其他 NuGet 套件。如果尚未加入此函式庫，請執行：

```bash
dotnet add package Aspose.Cells
```

現在我們可以開始了。

## 步驟 1：載入活頁簿 – 匯出的起點

首先，你必須載入包含欲轉成投影片之工作表的活頁簿。把活頁簿想像成來源文件；沒有它，其他一切都無從談起。

```csharp
using Aspose.Cells;

// Load the workbook that contains the shapes and data
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

**為什麼這很重要：** 載入活頁簿後，你才能存取工作表集合、頁面設定選項，以及匯出引擎。如果跳過此步驟，就無法設定 **print area** 或重複任何列。

> **小技巧：** 測試時使用絕對路徑，之後再改為相對路徑或基於設定的路徑以供正式環境使用。

## 步驟 2：設定匯出選項 – 保持文字方塊與圖形可編輯

匯出至 PowerPoint 時，你可能希望最終的投影片是可編輯的。Aspose.Cells 允許你透過 `ImageOrPrintOptions` 進行控制。將 `ExportTextBoxes` 與 `ExportShapeObjects` 設為 `true`，即告訴函式庫保留這些物件為原生 PowerPoint 元素，而不是將它們平鋪成影像。

```csharp
// Configure export options for a PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // The target format – crucial for PowerPoint
    ExportTextBoxes = true,            // Keep text boxes editable
    ExportShapeObjects = true          // Keep shape objects editable
};
```

**為什麼這很重要：** 若你曾需要 **convert excel to powerpoint**，然後手動微調投影片，此設定可免除你重新建立文字方塊的麻煩。它同時確保任何圖形（例如箭頭或圖表）仍以向量物件存在，方便調整大小。

## 步驟 3：設定列印區域並重複標題列

現在進入本教學的核心：**set print area**，並讓第一列在每一頁列印時（或在我們的情況下，於匯出投影片時）重複。列印區域告訴 Excel 哪些儲存格需要列印——或在此情境下匯出。

```csharp
// Define the area of the sheet to export (A1:G20)
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G20";

// Repeat the first row as a title on each printed page
sheet.PageSetup.PrintTitleRows = "$1:$1";
```

**為什麼這很重要：** 將匯出範圍限制在 `A1:G20`，可避免拉入大量空白區域，提升轉換速度並保持投影片整潔。`PrintTitleRows` 這行則讓第一列如同標頭——正是你在簡報中 **repeat title row** 時所需要的效果。

> **特殊情況：** 若你的資料從第 2 列開始，請相應調整範圍（例如 `PrintTitleRows = "$2:$2"`）。

## 步驟 4：將工作表儲存為 PowerPoint 檔案

最後，我們將投影片寫入磁碟。`Save` 方法接受目標檔名以及先前設定的選項。產生的結果是一個 PPTX 檔案，內含可編輯的文字方塊與圖形，隨時可在 PowerPoint 中開啟。

```csharp
// Save the selected sheet as a PPTX file using the configured options
string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
workbook.Save(outputPath, exportOptions);
```

**你會看到的結果：** 在 PowerPoint 中開啟 `SheetWithEditableShapes.pptx`。第一列會顯示為標題，`A1:G20` 的所有儲存格皆被渲染，且在 Excel 中加入的任何圖形仍可移動與編輯。沒有點陣圖——只有原生 PowerPoint 物件。

## 完整範例 – 結合所有步驟

以下是完整、可直接複製貼上的程式碼。你可以將它作為主控台應用程式執行，或嵌入任何較大型的解決方案中。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the workbook
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Set export options for editable PPTX
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportTextBoxes = true,
                ExportShapeObjects = true
            };

            // Step 3: Define print area and repeat title row
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G20";
            sheet.PageSetup.PrintTitleRows = "$1:$1";

            // Step 4: Save as PowerPoint
            string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
            workbook.Save(outputPath, exportOptions);

            Console.WriteLine($"Successfully exported to {outputPath}");
        }
    }
}
```

**預期輸出：** 執行程式後，主控台會印出成功訊息，且 PPTX 檔案會出現在指定位置。開啟檔案時會看到一張投影片，顯示選取的範圍、可編輯的文字方塊，以及所有原始圖形。

## 常見問題與注意事項

| Question | Answer |
|----------|--------|
| **這能同時處理多個工作表嗎？** | 可以。遍歷 `workbook.Worksheets`，對每個工作表重複相同步驟，並每次更改輸出檔名。 |
| **如果需要匯出多於一張投影片該怎麼辦？** | 對不同的 `ImageOrPrintOptions` 物件呼叫 `workbook.Save` 多次，必要時為每個物件設定不同的 `PageSetup`。 |
| **我可以調整投影片尺寸嗎？** | 使用 `exportOptions.ImageFormat` 設定 DPI，或在儲存前調整 `sheet.PageSetup.PaperSize`。 |
| **Aspose.Cells 是免費的嗎？** | 提供帶有浮水印的免費評估版。正式環境需購買授權。 |
| **Excel 公式怎麼處理？** | 匯出的值是匯出時的 **計算結果**。若需要在 PowerPoint 中保留即時公式，則需採用其他方法。 |

## 工作流程順暢小技巧

- **小技巧：** 在匯出前設定 `Workbook.Settings.CalcMode = CalculationModeType.Automatic`，確保所有公式皆為最新計算結果。
- **注意：** 非常大的範圍可能導致記憶體壓力。請將列印區域裁減至最小必要範圍。
- **效能小技巧：** 若要匯出多張工作表，請重複使用同一個 `ImageOrPrintOptions` 實例；每次重新建立會增加額外開銷。
- **版本說明：** 上述程式碼以 Aspose.Cells 23.10（2023 年 11 月發佈）為目標。較新版本仍保留相同 API，但請務必檢查發佈說明以防止破壞性變更。

## 結論

我們已說明如何在 Excel 工作表中 **set print area**，將第一列重複為標題，並在 **export excel to pptx** 時保留可編輯的文字方塊與圖形。簡而言之，你現在掌握了只需幾行 C# 程式碼即可可靠地 **convert excel to powerpoint**、**repeat title row**，以及 **create powerpoint from excel** 的方法。

準備好進一步了嗎？試著自動化批次轉換數十份報表，或在匯出後使用 PowerPoint SDK 加入自訂投影片版面。沒有極限——盡情實驗、挑戰、享受程式化文件產生的威力。

如果你覺得本教學有幫助，請分享、留下你自己的調整建議，或探索我們其他關於 **export excel to pptx** 以及相關自動化主題的指南。祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}