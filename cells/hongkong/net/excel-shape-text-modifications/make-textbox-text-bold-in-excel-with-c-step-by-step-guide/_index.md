---
category: general
date: 2026-02-21
description: 學習如何將 TextBox 文字設為粗體、變更 TextBox 字型大小，以及使用 Aspose.Cells 在 C# 中載入 Excel
  工作簿，並提供完整可執行的範例。
draft: false
keywords:
- make textbox text bold
- change textbox font size
- load excel workbook c#
- format excel shape text
language: zh-hant
og_description: 將 TextBox 文字設為粗體（使用 C#）。本教學亦示範如何更改 TextBox 字型大小，以及使用 Aspose.Cells
  於 C# 載入 Excel 工作簿。
og_title: 使用 C# 在 Excel 中將 TextBox 文字加粗 – 完整指南
tags:
- C#
- Aspose.Cells
- Excel automation
title: 使用 C# 在 Excel 中將文字方塊文字設為粗體 – 步驟指南
url: /zh-hant/net/excel-shape-text-modifications/make-textbox-text-bold-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中使用 C# 使 TextBox 文字加粗 – 步驟教學指南

需要在 Excel 檔案中使用 C# **將 TextBox 文字加粗** 嗎？本教學將會示範如何*載入 Excel 工作簿*、**更改 TextBox 字型大小**，以及使用 Aspose.Cells 來格式化圖形文字。  
如果你曾盯著一張平淡的試算表，心想「我的 TextBox 應該更突出」，那麼你來對地方了。

我們會逐行說明程式碼，解釋每個呼叫的意義，甚至討論當工作表根本沒有任何 TextBox 時該怎麼處理。完成後，你將擁有一段可重複使用的程式碼片段，直接放入任何 .NET 專案中——不需要再去找「請參考文件」的神祕連結。

## 您需要的條件

- **Aspose.Cells for .NET**（免費試用或授權版）– 我們用來操作 Excel 圖形的 API。  
- .NET 6 或更新版本（此程式碼同樣支援 .NET Framework 4.7+）。  
- 一個簡單的 Excel 檔案（`input.xlsx`），其中第一張工作表已至少包含一個 TextBox。  

就這樣。沒有額外的 NuGet 套件，沒有 COM interop，純粹的 C#。

## 使 TextBox 文字加粗 – 載入工作簿並存取 Shape

第一步是開啟工作簿並取得要編輯的 TextBox。  
我們同時會做一次快速的安全檢查，避免在工作表為空時程式當機。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook (load excel workbook c#)
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];

        // Verify that at least one TextBox exists
        if (worksheet.TextBoxes.Count == 0)
        {
            Console.WriteLine("No TextBoxes found on the first sheet.");
            return;
        }

        // Step 3: Access the first TextBox shape
        Shape textBox = worksheet.TextBoxes[0];

        // From here on we can format the shape's text
```

**為什麼這很重要：**  
*載入工作簿* 會給我們一個代表整個檔案於記憶體中的 `Workbook` 物件。存取 `Worksheets[0]` 是安全的，因為每個 Excel 檔案至少都有一張工作表。防護條件 (`if (worksheet.TextBoxes.Count == 0)`) 可防止 `IndexOutOfRangeException`——這是自動化既有檔案時常見的陷阱。

## 更改 TextBox 字型大小

在加粗文字之前，先確保字型大小正好符合需求。  
只要調整 `Font.Size` 屬性即可輕鬆變更大小。

```csharp
        // Step 4: Set the font name (optional but often useful)
        textBox.Font.Name = "Calibri";

        // Step 5: Change the font size (change textbox font size)
        textBox.Font.Size = 12; // 12 points is a comfortable default
```

**小技巧：**  
如果需要根據使用者輸入動態決定大小，只要把 `12` 換成變數即可。`Font` 物件是整個 Shape 共享的，所以大小變更會即時影響 TextBox 內的所有字元。

## 使 TextBox 文字加粗 – 核心操作

現在來到重點功能：將文字加粗。  
`IsBold` 旗標會改變字型的粗細，而不會影響其他樣式。

```csharp
        // Step 6: Make the text bold (make textbox text bold)
        textBox.Font.IsBold = true;
```

**底層發生了什麼？**  
Aspose.Cells 會將文字格式儲存在附加於 Shape 的 `Font` 物件中。設定 `IsBold = true` 會更新底層 XML（`<b>1</b>`），Excel 在渲染工作表時會讀取此資訊。這是一個**非破壞性**的操作——若之後將 `IsBold = false`，文字會回復成正常粗細。

## 儲存已修改的工作簿

完成格式設定後，我們將變更寫回磁碟。  
你可以直接覆寫原始檔，或如範例所示，產生新檔以保留來源檔不受影響。

```csharp
        // Step 7: Save the modified workbook
        var outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved. TextBox is now bold and 12pt Calibri in '{outputPath}'.");
    }
}
```

**預期結果：**  
在 Excel 中開啟 `output.xlsx`。第一張工作表的第一個 TextBox 應顯示 **Calibri 12 pt、加粗** 的文字。其他圖形不受影響。

## 格式化 Excel Shape 文字 – 其他樣式選項（可選）

雖然主要目標是**將 TextBox 文字加粗**，你可能還想要：

| 選項 | 程式碼片段 | 使用時機 |
|------|------------|----------|
| 斜體 | `textBox.Font.IsItalic = true;` | 強調副標題 |
| 文字顏色 | `textBox.Font.Color = System.Drawing.Color.DarkBlue;` | 品牌色彩 |
| 對齊方式 | `textBox.AlignmentHorizontal = TextAlignmentType.Center;` | 置中標題 |
| 多個 TextBox | Loop through `worksheet.TextBoxes` | 批次格式化 |

```csharp
// Example: Apply a blue color and center alignment to all textboxes
foreach (Shape tb in worksheet.TextBoxes)
{
    tb.Font.Color = System.Drawing.Color.Blue;
    tb.AlignmentHorizontal = TextAlignmentType.Center;
}
```

這些額外的調整說明了 *format excel shape text* 如何超越單純加粗的應用。

## 邊緣情況與常見陷阱

1. **工作表上沒有 TextBox** – 我們加入的防護條件 (`if (worksheet.TextBoxes.Count == 0)`) 會優雅地退出並提示使用者。  
2. **隱藏的工作表** – 隱藏的工作表仍可透過 `Worksheets` 集合存取，只要確保引用正確的索引。  
3. **大型檔案** – 載入巨大的工作簿會佔用大量記憶體。可考慮使用 `Workbook.LoadOptions` 只載入必要的部分。  
4. **不同的 Excel 版本** – Aspose.Cells 支援 `.xls`、`.xlsx` 甚至 `.xlsb`。相同程式碼可跨版本使用，但較舊的 Excel 可能會忽略某些較新的字型功能。

## 完整可執行範例（直接複製貼上）

```csharp
using System;
using Aspose.Cells;

class MakeTextboxBoldDemo
{
    static void Main()
    {
        // Load the workbook (load excel workbook c#)
        var inputFile = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputFile);

        // Get the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // Ensure a textbox exists
        if (sheet.TextBoxes.Count == 0)
        {
            Console.WriteLine("No textbox found on the first sheet.");
            return;
        }

        // Access the first textbox
        Shape txtBox = sheet.TextBoxes[0];

        // Set font name and size (change textbox font size)
        txtBox.Font.Name = "Calibri";
        txtBox.Font.Size = 12;

        // Make the text bold (make textbox text bold)
        txtBox.Font.IsBold = true;

        // Optional: extra styling (format excel shape text)
        txtBox.Font.Color = System.Drawing.Color.DarkGreen;
        txtBox.AlignmentHorizontal = TextAlignmentType.Center;

        // Save the result
        var outputFile = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputFile);

        Console.WriteLine($"Saved: {outputFile}");
    }
}
```

執行程式，開啟產生的 `output.xlsx`，你會看到 TextBox 內的文字已變成加粗、12 pt Calibri。簡單吧？

## 結論

現在你已掌握 **如何在 Excel 工作簿中使用 C# 使 TextBox 文字加粗**、**如何更改 TextBox 字型大小**，以及使用 Aspose.Cells **載入 Excel 工作簿 C#** 的基本概念。上方的完整範例可直接放入任何專案，同時也示範了 **格式化 Excel shape 文字** 的更多可能。

接下來可以嘗試遍歷每張工作表，將所有 TextBox 加粗，或結合資料驅動的內容產生——例如從資料庫取值填入 TextBox。原理相同，程式碼依舊保持簡潔。

有任何想法想分享，或遇到意外錯誤嗎？留下評論，我們一起討論。祝編程愉快！

![在 Excel 中使用 C# 使 TextBox 文字加粗](/images/make-textbox-text-bold-csharp.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}