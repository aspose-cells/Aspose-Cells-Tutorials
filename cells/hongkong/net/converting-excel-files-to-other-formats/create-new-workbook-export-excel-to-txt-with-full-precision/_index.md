---
category: general
date: 2026-03-18
description: 建立新工作簿並將 Excel 匯出為 TXT，同時保留數字精度。學習如何將工作表另存為 txt，並有效率地將工作表轉換為 txt。
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: zh-hant
og_description: 建立新工作簿並精確匯出 Excel 為 TXT。本教學示範如何將工作表另存為 txt，以及使用 C# 將工作表轉換為 txt。
og_title: 建立新工作簿 – Excel 匯出為 TXT 指南
tags:
- Aspose.Cells
- C#
- Excel automation
title: 建立新工作簿 – 匯出 Excel 為 TXT（完整精度）
url: /zh-hant/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立新工作簿 – 以完整精度匯出 Excel 為 TXT

有沒有曾經需要在 C# 中 **create new workbook**，只為了把資料匯出成純文字檔？也許你正從舊系統擷取報表，而下游工具只能接受 `.txt` 檔案。好消息是？你不必犧牲數值精度，也絕對不需要手動編寫 CSV 字串。

在本指南中，我們將逐步說明 **export excel to txt** 的完整流程，涵蓋從初始化工作簿到在 **save worksheet as txt** 時保留尾端零的所有步驟。完成後，你將擁有一段可直接放入任何 .NET 專案的即用程式碼——不需要額外工具。

## 需要的條件

- **ASP.NET/.NET 6+**（此程式碼亦可在 .NET Framework 4.6+ 上執行）  
- **Aspose.Cells for .NET** – 提供 `Workbook`、`Worksheet` 與 `TxtSaveOptions` 類別的函式庫。可透過 NuGet 使用 `Install-Package Aspose.Cells` 取得。  
- 具備基本的 C# 知識（只要熟悉 `using` 陳述式，即可順利使用）。  

就是這樣——不需要 Excel interop、不需要 COM 物件，絕對不需要手動字串串接。  

---

## 步驟 1：初始化新工作簿（主要關鍵字）

首先要做的事就是 **create new workbook**。可以把工作簿想像成空白畫布，之後會在上面貼上數字、文字或公式。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **為什麼這很重要：** 未載入檔案就實例化 `Workbook`，即可得到一張全新白紙。之後可程式化加入資料，這對於沒有現有 `.xlsx` 檔案的 **convert worksheet to txt** 情境非常適合。

## 步驟 2：填入儲存格 – 保留尾端零

將數字匯出為文字時常見的陷阱是會遺失尾端零（`123.45000` 變成 `123.45`）。若下游系統依賴固定寬度欄位，這種遺失會導致全部失效。

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **小技巧：** `PutValue` 會自動推斷資料類型。如果需要看起來像數字的字串，請改用 `PutValue("123.45000")`。

## 步驟 3：設定 TXT 儲存選項 – 保留數值精度

這裡就是魔法發生的地方。透過切換 `PreserveNumericPrecision`，可指示 Aspose.Cells 寫入你輸入的精確值，包含任何不顯著的尾端零。

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **為什麼要啟用？** 當你 **save excel as txt** 時，預設會去除不必要的小數位。將 `PreserveNumericPrecision = true` 設為 true 可確保輸出與儲存格顯示的值相同，這對於財務報表或科學資料尤為重要。

## 步驟 4：將工作表儲存為 TXT – 最終匯出

現在我們真正執行 **save worksheet as txt**。你可以將路徑指向任何有寫入權限的地方；範例使用名為 `output` 的相對資料夾。

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **預期輸出**（`num-preserve.txt`）：

```
123.45000
```

請注意尾端零仍然完整保留——正是你所要求的。

## 步驟 5：驗證結果 – 快速檢查

程式執行完畢後，使用任何文字編輯器開啟 `num-preserve.txt`。你應該會看到單行 `123.45000`。若看到 `123.45`，請再次確認 `PreserveNumericPrecision` 已設為 `true`，且使用的是較新版本的 Aspose.Cells（v23.10 以上）。

## 常見變形與邊緣情況

### 匯出多個儲存格或範圍

如果需要對整個範圍執行 **export excel to txt**，只要在儲存前填入更多儲存格即可：

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Aspose 預設會將每個儲存格寫在新的一行。你也可以透過 `txtSaveOptions.Separator` 變更分隔符（如 Tab、逗號）。

### 以不同編碼將工作表轉換為 TXT

有時下游系統需要 UTF‑8 BOM 或 ASCII 編碼。可這樣調整編碼：

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### 處理大型工作簿

面對巨量工作表（數十萬列）時，建議使用串流輸出：

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

## 專業技巧與注意事項

- **不要忘記在呼叫 `Save` 前先建立輸出目錄**，否則會拋出 `DirectoryNotFoundException`。  
- **留意區域設定特定的小數分隔符**。若你的環境使用逗號（`1,23`），請設定 `txtSaveOptions.DecimalSeparator = '.'` 以強制使用點號。  
- **版本相容性**：`PreserveNumericPrecision` 旗標於 Aspose.Cells 20.6 版首次加入。若使用較舊版本，該旗標不存在，必須在儲存前將儲存格格式化為文字。

![建立新工作簿範例](excel-to-txt.png "建立新工作簿")

*圖片替代文字：「建立新工作簿並以保留數值精度匯出 Excel 為 TXT」*

## 重點回顧 – 我們涵蓋的內容

- **Create new workbook** 使用 Aspose.Cells。  
- 填入包含尾端零的數字至儲存格。  
- 將 `TxtSaveOptions.PreserveNumericPrecision = true` 設為 true，以 **save excel as txt** 而不失去精度。  
- 將檔案寫入磁碟，並驗證輸出與原始值相符。  

這就是完整的 **convert worksheet to txt** 工作流程，程式碼不超過 50 行 C#。

## 往後步驟與相關主題

既然你已能以完美精度 **export excel to txt**，接下來可以探索以下主題：

- **Exporting to CSV** 使用自訂分隔符（`TxtSaveOptions.Separator`）。  
- **Saving as other plain‑text formats** 如 TSV（`SaveFormat.TabDelimited`）。  
- **Batch processing** 資料夾中多個工作簿，使用 `Directory.GetFiles`。  
- **Integrating with Azure Functions** 於雲端即時轉換。  

上述每項皆基於相同的 `Workbook` → `Worksheet` → `TxtSaveOptions` 流程，讓你感到如沐春風。

### 最後的想法

如果你已跟隨操作，現在你已清楚知道如何 **create new workbook**、填入資料，並 **save worksheet as txt**，同時保留所有關鍵的小數位。這段程式碼雖小，卻能解決舊有流程要求純文字輸入時常見的頭痛問題。

試試看，微調選項，讓資料以你想要的方式流動。祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}