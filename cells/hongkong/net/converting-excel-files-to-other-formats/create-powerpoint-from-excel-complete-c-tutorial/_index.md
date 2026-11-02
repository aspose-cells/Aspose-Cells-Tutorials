---
category: general
date: 2026-02-21
description: 快速從 Excel 建立 PowerPoint。了解如何使用 Aspose.Cells 只需幾行 C# 程式碼，即可將 Excel 匯出為可編輯文字與圖表的
  PowerPoint。
draft: false
keywords:
- create powerpoint from excel
- export excel to powerpoint
- export editable text
- export excel chart powerpoint
- convert excel chart powerpoint
language: zh-hant
og_description: 從 Excel 建立可編輯文字和圖表的 PowerPoint。請參考本詳細指南，使用 Aspose.Cells 將 Excel 匯出至
  PowerPoint。
og_title: 從 Excel 建立 PowerPoint – 逐步 C# 教學
tags:
- C#
- Aspose.Cells
- PowerPoint
- Excel Automation
title: 從 Excel 建立 PowerPoint – 完整 C# 教學
url: /zh-hant/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-complete-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 Excel 建立 PowerPoint – 完整 C# 教程

是否曾經需要 **從 Excel 建立 PowerPoint**，卻不確定該使用哪個 API？你並不孤單。許多開發者在想把資料豐富的工作表轉換成精緻投影片時會卡關，尤其是當他們希望轉換後的文字方塊仍能在 PowerPoint 中編輯時。

在本指南中，我們將示範如何 **將 Excel 匯出至 PowerPoint**，同時保留可編輯的文字、圖表品質與版面配置——只需幾行 C# 程式碼。完成後，你將得到一個可直接在 PowerPoint 中調整的 PPTX 檔案，彷彿是手動製作的投影片。

## 你將學會

- 如何載入包含圖表與圖形的 Excel 活頁簿。  
- 如何設定 `PresentationExportOptions` 讓文字方塊保持可編輯（`export editable text`）。  
- 如何實際 **匯出 Excel 圖表至 PowerPoint**，取得乾淨的投影片檔。  
- 在不同頁面設定或多個工作表的情況下，如何套用小變化以 **轉換 Excel 圖表 PowerPoint**。

### 前置條件

- .NET 開發環境（Visual Studio 2022 或更新版本）。  
- Aspose.Cells for .NET（免費試用版或正式授權版）。  
- 一個 Excel 檔案（`ChartWithShape.xlsx`），內含至少一個圖表與一個你想保留可編輯的圖形。  

如果以上條件都具備，讓我們直接進入實作——不囉嗦，只提供可直接執行的解決方案。

## 從 Excel 建立 PowerPoint – 步驟說明

以下每個步驟都會附上簡潔的程式碼片段，說明 **為何** 這麼做，並提醒常見的陷阱。完整範例可於頁面底部直接複製貼上。

### 步驟 1：載入 Excel 活頁簿

首先必須將來源活頁簿載入記憶體。Aspose.Cells 會讀取檔案並建立可供操作的豐富物件模型。

```csharp
// Step 1: Load the Excel workbook that contains the chart and shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");

// Quick sanity check – make sure the workbook actually loaded
if (workbook.Worksheets.Count == 0)
    throw new InvalidOperationException("The workbook appears to be empty.");
```

**為何重要：**  
載入活頁簿是基礎。若檔案路徑錯誤或活頁簿損毀，所有後續的 `export excel to powerpoint` 步驟都會失敗。此處的健全性檢查能在早期提供回饋，避免之後出現「找不到檔案」的模糊錯誤。

### 步驟 2：準備匯出選項

Aspose.Cells 提供 `PresentationExportOptions` 物件，讓你控制 PPTX 的外觀。此處決定文字是否保持可編輯。

```csharp
// Step 2: Create export options for PowerPoint conversion
PresentationExportOptions exportOptions = new PresentationExportOptions();

// Optional: tweak the slide size (default is 10in x 7.5in)
exportOptions.SlideSize = new SizeF(10, 7.5f);
```

**為何重要：**  
若不自行設定 `PresentationExportOptions`，函式庫會使用預設值，可能與你的企業投影片範本不符。提前調整投影片尺寸可避免之後手動調整的麻煩。

### 步驟 3：啟用可編輯文字方塊

魔法旗標 `ExportEditableTextBoxes` 告訴 Aspose.Cells 將任何文字圖形保留為 PowerPoint 文字方塊，而非靜態影像。

```csharp
// Step 3: Enable editability of text boxes in the resulting presentation
exportOptions.ExportEditableTextBoxes = true;
```

**為何重要：**  
若省略此行，產生的 PPTX 會將文字點陣化——在 PowerPoint 中無法編輯標籤或說明。設定 `export editable text` 才是讓投影片真正可重複使用的關鍵。

### 步驟 4：將工作表匯出為 PPTX

現在正式寫入 PPTX 檔案。你可以選擇任意工作表；此例使用第一張工作表（`Worksheets[0]`）。

```csharp
// Step 4: Export the first worksheet's page setup to a PPTX file
workbook.Worksheets[0].PageSetup.SaveToPptx("YOUR_DIRECTORY/Result.pptx", exportOptions);
```

**為何重要：**  
`SaveToPptx` 會遵循你在 Excel 中設定的頁面配置（邊界、方向），因此投影片會完整映射你已設計好的版面。這正是 **export excel chart powerpoint** 的核心。

### 步驟 5：驗證輸出（可選但建議執行）

轉換完成後，於 PowerPoint 開啟產生的 `Result.pptx`，檢查：

1. 圖表是否清晰且保留資料系列。  
2. 文字方塊是否可選取且可編輯。  
3. 投影片尺寸是否符合預期。

若有異常，請回到 `exportOptions` 再次調整——例如可設定 `exportOptions.IncludePrintArea = true` 以遵循已命名的列印區域。

```csharp
// Optional: open the PPTX automatically (requires System.Diagnostics)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/Result.pptx",
    UseShellExecute = true
});
```

### 步驟 6：進階變形（匯出多張工作表）

通常你會想一次 **轉換 excel chart powerpoint** 多個工作表。只要遍歷集合，為每張投影片指定唯一名稱即可：

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outputPath = $"YOUR_DIRECTORY/Result_Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(outputPath, exportOptions);
}
```

**小技巧：** 若需要將所有工作表匯入同一個 PPTX，先建立新的 `Presentation` 物件，將每張投影片匯入後一次儲存。雖稍微複雜，但可避免產生大量檔案。

## 完整範例程式

以下提供完整程式碼，直接貼到 Console App 即可執行。

```csharp
using System;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Export;

class Program
{
    static void Main()
    {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");
        if (workbook.Worksheets.Count == 0)
        {
            Console.WriteLine("Workbook is empty – aborting.");
            return;
        }

        // 2️⃣ Set up export options
        PresentationExportOptions exportOptions = new PresentationExportOptions
        {
            SlideSize = new SizeF(10, 7.5f),          // optional custom size
            ExportEditableTextBoxes = true           // <‑‑ keep text boxes editable
        };

        // 3️⃣ Export first worksheet
        string outputPath = "YOUR_DIRECTORY/Result.pptx";
        workbook.Worksheets[0].PageSetup.SaveToPptx(outputPath, exportOptions);
        Console.WriteLine($"PowerPoint created at: {outputPath}");

        // 4️⃣ Open the result automatically (Windows only)
        try
        {
            System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
            {
                FileName = outputPath,
                UseShellExecute = true
            });
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not open PPTX automatically: {ex.Message}");
        }
    }
}
```

**預期結果：**  
開啟 `Result.pptx` 後，你會看到一張與 Excel 工作表版面相同的投影片。Excel 中的圖表會以原生 PowerPoint 圖表形式呈現，先前在 Excel 加入的圖形則變成可完全編輯的文字方塊。

## 常見問題與邊緣情況

- **這能處理含巨集的活頁簿（`.xlsm`）嗎？**  
  可以。Aspose.Cells 會讀取巨集，但不會執行它們。轉換過程會忽略 VBA，仍會取得視覺內容。

- **如果工作表內有多個圖表怎麼辦？**  
  所有可見圖表都會轉移到同一張投影片。若需要每個圖表各佔一張投影片，可將工作表拆分或使用第 6 步的迴圈方式。

- **能保留自訂的 PowerPoint 主題嗎？**  
  匯出時無法直接保留。轉換後可在 PowerPoint 手動套用主題，或使用 Aspose.Slides 以程式方式套用。

- **能只匯出選取的範圍嗎？**  
  在 Excel 設定命名列印區（`Page Layout → Print Area`），並啟用 `exportOptions.IncludePrintArea = true`。

## 結語

現在你已掌握如何使用 Aspose.Cells **從 Excel 建立 PowerPoint**，完整控制可編輯文字、圖表品質與投影片尺寸。本文提供的簡短程式碼涵蓋最常見情境，而額外的技巧則讓你在需要 **export excel to powerpoint** 多工作表或自訂版面時更具彈性。

準備好迎接下一個挑戰了嗎？試著結合 **Aspose.Slides**，以程式方式加入轉場、講者備註，甚至將產生的投影片嵌入更大的簡報中。或是嘗試將整本活頁簿一次轉成多張投影片——非常適合自動化報表流程。

有任何問題或發現巧妙的調整方法嗎？歡迎在下方留言，祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}