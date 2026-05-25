---
category: general
date: 2026-02-15
description: 如何在 C# 中複製字型並套用儲存格樣式（簡單範例）。了解如何取得儲存格樣式，並使用儲存格格式設定文字方塊的字型大小。
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: zh-hant
og_description: 如何從工作表儲存格複製字型並套用儲存格樣式至文字方塊。本指南說明如何取得儲存格樣式、使用儲存格格式設定，以及設定文字方塊的字型大小。
og_title: 如何從 Excel 儲存格複製字型 – 完整 C# 教學
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: 如何將 Excel 儲存格的字型複製到文字方塊 – 逐步指南
url: /zh-hant/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

? Actually they are placeholders not code fences. In original, they appear as separate lines, not inside fences. So we keep them unchanged.

Also keep markdown formatting.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何從 Excel 儲存格複製字型到 TextBox – 完整 C# 教學

有沒有曾經需要 **複製字型** 從試算表儲存格，並讓 UI 文字方塊看起來完全相同？你並不是唯一遇到這種情況的人。在許多報表工具或自訂儀表板中，你會發現自己從 Excel 抽取資料，然後嘗試保持視覺一致性——字型系列、大小與顏色——完整不變。  

好消息是，只要幾行 C# 程式碼，你就可以 **取得儲存格樣式**、讀取其字型屬性，並 **套用儲存格樣式** 到任何文字方塊控制項。在本教學中，我們將一步步示範完整、可執行的範例，說明如何 **使用儲存格格式化**，甚至 **程式化設定文字方塊字型大小**。

---

## 你將學會

- 如何從網格元件（範例中的 `gridJs`）取得 `TextBox` 物件  
- 如何從特定的 Excel 儲存格（`B2`）讀取字型系列、大小與顏色  
- 如何將這些字型屬性複製到文字方塊，使 UI 與試算表鏡像相同  
- 常見陷阱（例如顏色轉換）以及一些 **專業技巧**，讓你的程式碼更健全  
- 一段可直接執行的程式碼片段，您可以直接放入 console 應用程式或 WinForms 專案中  

**Prerequisites**  
你應該具備：

1. 已安裝 .NET 6+（或 .NET Framework 4.8）  
2. EPPlus NuGet 套件（用於 Excel 處理）  
3. 一個能夠公開 `TextBoxes` 字典的網格控制項（範例使用虛構的 `gridJs`，但概念適用於任何 UI 函式庫）  

現在，讓我們動手實作。

---

## Step 1: Set Up the Project and Load the Worksheet

首先，建立一個新的 console 或 WinForms 專案，並加入 EPPlus：

```bash
dotnet add package EPPlus --version 6.*
```

接著，載入活頁簿並取得想要複製樣式的儲存格。

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**Why this matters:** EPPlus 讓你直接存取 `Style` 物件，該物件內含 `Font` 子物件。從中你可以讀取 `Name`、`Size` 與 `Color`。這正是 **取得儲存格樣式** 操作的核心。

---

## Step 2: Grab the Target TextBox from Your Grid

假設你的 UI 網格（`gridJs`）以欄位名稱為鍵，將文字方塊存放於字典中，你可以這樣取得目標物件：

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

如果你使用 WinForms，`notesTextBox` 可能是 `TextBox` 控制項；在 WPF 中可能是 `TextBox` 元素；而在基於 Web 的網格中則可能是 JavaScript interop 物件。關鍵是你已取得可操作的參考。

---

## Step 3: Transfer the Font Family

現在我們同時擁有來源樣式與目標控制項，開始複製字型系列。

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Pro tip:** 並非所有 UI 框架都提供接受純字串的 `FontFamily` 屬性。於 WinForms 中，你會這樣寫 `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`，請依實際情況調整。

---

## Step 4: Transfer the Font Size

EPPlus 以 `float` 儲存字型大小，直接套用即可：

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

如果你的控制項使用點數（大多數情況如此），可以直接指派該值而不需轉換。對於基於 CSS 的網格，可能需要在數值後加上 `"pt"`。

---

## Step 5: Transfer the Font Colour

顏色轉換是最具挑戰性的部分，因為 EPPlus 以 ARGB 整數儲存顏色，而許多 UI 框架則期待 `System.Drawing.Color` 或 CSS 十六進位字串。

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Why this works:** `GetColor()` 會解析以佈景主題為基礎的顏色，並回傳具體的 `System.Drawing.Color`。若儲存格使用預設顏色（未明確設定），我們會預設為黑色，以避免 null 參考例外。

---

## Full Working Example

把前面的步驟整合起來，以下是一個最小化的 console 應用程式範例，會讀取 Excel 檔案、擷取 **B2** 的字型，並套用到模擬的文字方塊。

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Expected output (assuming B2 uses Arial, 12 pt, blue):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

執行程式、開啟 UI，你會看到「Notes」文字方塊現在正確映射 **B2** 的字型樣式，無需手動調整。

---

## Frequently Asked Questions & Edge Cases

### 如果儲存格使用佈景主題顏色而非明確的 RGB 值，該怎麼辦？

EPPlus 的 `GetColor()` 會自動將佈景主題顏色解析為具體的 `System.Drawing.Color`。然而，若你使用的舊版函式庫僅回傳佈景主題索引，則需要自行將索引對映到顏色調色盤。

### 我可以複製其他樣式屬性嗎（例如粗體、斜體）？

當然可以。`ExcelStyle.Font` 物件同時提供 `Bold`、`Italic`、`Underline` 與 `Strike`。只要在 UI 控制項上設定對應屬性即可：

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### 如果網格控制項沒有 `FontColor` 屬性怎麼處理？

大多數現代 UI 框架都有此屬性，但若你的控制項僅接受 CSS 字串，請將 `Color` 轉換為十六進位表示：

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### 若要一次處理多個儲存格該怎麼做？

遍歷目標範圍，逐一取得每個儲存格的樣式，並套用到相對應的文字方塊。若處理大量列時，請記得快取樣式物件，以免影響效能。

---

## Pro Tips & Common Pitfalls

- **Cache the ExcelPackage** – 為每個儲存格都開關檔案的成本相當高。請一次載入活頁簿，之後重複使用 `ExcelWorksheet` 物件。  
- **Watch out for null colours** – 繼承預設顏色的儲存格會回傳 `null`。務必提供備援（例如黑色或控制項的預設顏色）。  
- **Mind DPI scaling** – 若目標是高 DPI 螢幕，字型大小可能會顯得較大。必要時可使用 `Graphics.DpiX` 進行調整。  
- **Thread safety** – EPPlus 並非執行緒安全。若要平行處理多張工作表，請為每個執行緒建立獨立的 `ExcelPackage`。

---

## Conclusion

你現在已掌握 **如何從 Excel 儲存格複製字型**，以及 **如何將儲存格樣式套用** 到任何文字方塊控制項的完整流程。透過取得儲存格的 `Style`、擷取其 `Font` 屬性，並指派給 UI 元件，即可在不需手動調整的情況下保持視覺一致性。  

完整解決方案——載入活頁簿、取得儲存格樣式、設定文字方塊的字型系列、大小與顏色——涵蓋了 **使用儲存格格式化** 的核心，同時示範了 **正確設定文字方塊字型大小** 的方法。  

接下來，你可以嘗試擴充範例，複製背景顏色、邊框，甚至整個儲存格內容。若你使用的資料網格函式庫支援豐富的儲存格渲染，現在就能將從 Excel 抽取的完整樣式資訊餵入，讓 UI 與報表徹底同步。  

還有其他問題嗎？歡迎留言或探索相關主題，例如「動態 Excel‑to‑UI 綁定」與「支援佈景主題的顏色轉換」。祝開發順利！

---

![字型複製範例](placeholder-image.jpg "從 Excel 儲存格複製字型到 TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}