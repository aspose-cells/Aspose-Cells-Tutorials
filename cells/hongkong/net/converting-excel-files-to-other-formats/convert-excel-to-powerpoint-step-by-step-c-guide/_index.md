---
category: general
date: 2026-03-01
description: 使用 C# 快速將 Excel 轉換為 PowerPoint。了解如何僅用幾行程式碼，使用 Aspose.Cells 從 Excel 工作簿產生
  PowerPoint。
draft: false
keywords:
- convert excel to powerpoint
- generate powerpoint from excel
- convert xlsx to pptx
- how to convert excel
- create pptx from excel
language: zh-hant
og_description: 在 C# 中將 Excel 轉換為 PowerPoint。本指南示範如何使用 Aspose.Cells 從 Excel 檔案產生 PowerPoint，並提供完整程式碼與技巧。
og_title: 將 Excel 轉換為 PowerPoint – 完整 C# 教學
tags:
- C#
- Aspose.Cells
- Excel
- PowerPoint
title: 將 Excel 轉換為 PowerPoint – C# 逐步指南
url: /zh-hant/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 轉換 Excel 為 PowerPoint – 步驟說明 C# 教學

有沒有曾經想要 **將 Excel 轉換成 PowerPoint**，卻不知從何下手？你並不孤單——許多開發者在嘗試把資料豐富的試算表變成可直接使用的簡報時，都會卡在這裡。

好消息是，只要幾行 C# 程式碼，就能 **自動從 Excel 產生 PowerPoint**，不需要手動複製貼上。在本教學中，我們會一步步說明整個流程，從載入 `.xlsx` 檔案到儲存一個可在 Microsoft PowerPoint 或任何相容檢視器開啟的精緻 `.pptx`。

> **你將得到：** 一個可執行的程式，能載入 Excel 活頁簿、設定 PowerPoint 儲存選項，並寫出 PowerPoint 檔案——全部使用 Aspose.Cells 函式庫。

## 需求

- **.NET 6.0** 或更新版本（程式碼同樣支援 .NET Framework 4.7 以上）  
- **Aspose.Cells for .NET** – 可從 NuGet 取得 (`Install-Package Aspose.Cells`)  
- 基本的 C# 知識（只要會使用 `using` 陳述式即可）  
- 一個想要轉成簡報的 Excel 檔案（`input.xlsx`）  

就這麼簡單。無需額外第三方工具、無需 COM interop、也不需要繁雜的 PowerPoint 自動化。現在就開始吧。

![Convert Excel to PowerPoint workflow](convert-excel-to-powerpoint.png "轉換 Excel 為 PowerPoint 工作流程圖")

*Alt text: 轉換 Excel 為 PowerPoint 工作流程圖*

## 使用 Aspose.Cells 轉換 Excel 為 PowerPoint

### 步驟 1 – 載入 Excel 活頁簿

首先要把試算表載入記憶體。Aspose.Cells 只要呼叫 `Workbook` 建構子並傳入檔案路徑，就能輕鬆完成。

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the Excel workbook
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
```

**為什麼重要：** 載入活頁簿後，我們就能存取每張工作表、圖表，甚至內嵌圖片。接下來就可以決定哪些要保留、哪些要捨棄，再進行轉換。

### 步驟 2 – 設定簡報儲存選項

Aspose.Cells 支援多種輸出格式，對於 PowerPoint 我們使用 `PresentationSaveOptions`。此物件讓我們指定目標 `SaveFormat.Pptx`，並調整一些實用設定，例如是否嵌入巨集或保留原始欄寬。

```csharp
            // Step 2: Set up presentation save options for PowerPoint format
            PresentationSaveOptions saveOptions = new PresentationSaveOptions(SaveFormat.Pptx)
            {
                // Optional: keep the original Excel formatting as much as possible
                // (true by default, but we set it explicitly for clarity)
                KeepOriginalFormatting = true
            };
```

**為什麼重要：** 若未正確設定，產生的投影片可能會被壓縮或失去樣式。告訴 Aspose.Cells 我們需要真正的 PPTX 檔案，就能確保轉換時保留 Excel 版面的排版。

### 步驟 3 – 將活頁簿儲存為 PowerPoint 簡報

魔法發生的時刻。只要一次 `Save` 呼叫，就會寫出一個 `.pptx`，其內容映射活頁簿的第一張工作表（或全部工作表，視函式庫版本而定）。對大多數情境而言，第一張工作表已足夠，之後你也可以自行實驗。

```csharp
            // Step 3: Save the workbook as a PowerPoint presentation
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            workbook.Save(outputPath, saveOptions);

            Console.WriteLine($"Success! '{outputPath}' has been created.");
        }
    }
}
```

**你會看到的結果：** 在 PowerPoint 開啟 `output.pptx`，每張工作表都會變成一張投影片。文字儲存格會變成文字方塊，圖表會變成原生 PowerPoint 圖表，甚至圖片也會保留原始解析度。

## 從 Excel 產生 PowerPoint – 專案設定小技巧

- **NuGet 安裝：** 在專案資料夾執行 `dotnet add package Aspose.Cells`。這會取得最新穩定版（截至 2026 年 3 月，版本 23.10）。  
- **目標平台：** 若使用 .NET Core，請確保 `csproj` 中包含 `<TargetFramework>net6.0</TargetFramework>`。  
- **檔案路徑：** 使用 `Path.Combine` 以確保跨平台安全，特別是程式在 Linux 容器中執行時。

```csharp
using System.IO;

// Example of safe path building
string baseDir = AppDomain.CurrentDomain.BaseDirectory;
string inputPath = Path.Combine(baseDir, "input.xlsx");
string outputPath = Path.Combine(baseDir, "output.pptx");
```

## 轉換 Xlsx 為 Pptx – 處理多張工作表

預設情況下 Aspose.Cells 只會轉換 **目前作用中的工作表**。如果需要每張工作表對應一張投影片，可以遍歷集合並分別儲存：

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet sheet = workbook.Worksheets[i];
    sheet.IsSelected = true; // Make this sheet the active one
    string slidePath = Path.Combine(baseDir, $"Slide_{i + 1}.pptx");
    workbook.Save(slidePath, saveOptions);
}
```

**小技巧：** 每次迭代後，若打算再次使用同一個 `Workbook` 物件執行其他操作，請呼叫 `workbook.Worksheets[i].IsSelected = false`。

## 如何轉換 Excel – 處理大型檔案

大型活頁簿（數百 MB）可能會耗盡記憶體。以下幾個技巧可讓流程更順暢：

1. **啟用串流：** `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` 會讓 Aspose.Cells 使用暫存檔，而非全部載入記憶體。  
2. **跳過空白列/欄：** 設定 `saveOptions.IgnoreEmptyRows = true` 可減少投影片雜訊。  
3. **調整圖片大小：** 若 Excel 含有高解析度圖片，可在轉換前使用 `ImageResizeOptions` 進行縮小。

```csharp
workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;
saveOptions.IgnoreEmptyRows = true;
saveOptions.ImageResizeOptions = new ImageResizeOptions
{
    Width = 1024,
    Height = 768,
    ResizeMode = ResizeMode.Proportional
};
```

## 從 Excel 建立 Pptx – 驗證結果

`Save` 完成後，你會想確認檔案是否可用：

```csharp
if (File.Exists(outputPath))
{
    var fileInfo = new FileInfo(outputPath);
    Console.WriteLine($"File size: {fileInfo.Length / 1024} KB");
    // Optionally launch PowerPoint automatically (Windows only)
    System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
    {
        FileName = outputPath,
        UseShellExecute = true
    });
}
else
{
    Console.Error.WriteLine("Something went wrong – the PPTX was not created.");
}
```

開啟檔案後，應會看到一套與原始試算表版面相同的投影片，包含圖表、表格以及任何內嵌圖片。

## 常見問題與特殊情況

| 問題 | 解答 |
|----------|--------|
| *可以保留 Excel 巨集嗎？* | 不行。PowerPoint 不支援來自 Excel 的 VBA 巨集。需要自行在 PowerPoint 中重新建立相關自動化。 |
| *儲存格註解會怎樣處理？* | 會變成投影片上的獨立文字方塊，若想隱藏可設定 `saveOptions.IncludeCellComments = false`。 |
| *公式會被計算嗎？* | 會——Aspose.Cells 會在轉換前先計算公式，投影片上顯示的是計算後的值，而非公式本身。 |
| *有沒有辦法自訂投影片設計？* | 轉換後可使用 Aspose.Slides 的 `Presentation` 類別套用 PowerPoint 範本，然後把產生的投影片複製進去。 |

## 完整範例（所有程式碼一次呈現）

```csharp
using Aspose.Cells;
using System;
using System.IO;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Build safe file paths
            string baseDir = AppDomain.CurrentDomain.BaseDirectory;
            string inputPath = Path.Combine(baseDir, "input.xlsx");
            string outputPath = Path.Combine(baseDir, "output.pptx");

            // Load the Excel workbook
            Workbook workbook = new Workbook(inputPath);

            // Optional: improve memory usage for huge files
            workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;

            // Configure PowerPoint save options
            PresentationSaveOptions saveOptions = new PresentationSaveOptions(SaveFormat.Pptx)
            {
                KeepOriginalFormatting = true,
                IgnoreEmptyRows = true,
                ImageResizeOptions = new ImageResizeOptions
                {
                    Width = 1024,
                    Height = 768,
                    ResizeMode = ResizeMode.Proportional
                }
            };

            // Save as PowerPoint
            workbook.Save(outputPath, saveOptions);

            // Verify the result
            if (File.Exists(outputPath))
            {
                Console.WriteLine($"Success! '{outputPath}' created ({new FileInfo(outputPath).Length / 1024} KB).");
                // Open the file automatically (Windows only)
                System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            else
            {
                Console.Error.WriteLine("Failed to create the PowerPoint file.");
            }
        }
    }
}
```

執行程式，即可得到全新 `.pptx`，適合下次客戶會議、董事會簡報或內部說明會使用。

## 結論

現在你已掌握 **如何使用 C# 與 Aspose.Cells 將 Excel 轉換成 PowerPoint**。核心步驟——載入活頁簿、設定 `PresentationSaveOptions`、呼叫 `Save`——相當直接，且本教學同時說明了 **從 Excel 產生 PowerPoint** 時的記憶體處理等細節。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}