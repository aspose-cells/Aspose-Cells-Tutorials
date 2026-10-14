---
category: general
date: 2026-02-21
description: 快速在 C# 中建立儲存格樣式。學習如何套用樣式至儲存格、將文字置中、設定儲存格對齊方式，並精通儲存格格式設定。
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: zh-hant
og_description: 在 C# 中建立儲存格樣式，並學習如何將樣式套用至儲存格、將文字置中以及設定儲存格對齊方式，提供清晰的逐步指南。
og_title: 在 C# 中建立儲存格樣式 – 為儲存格套用樣式並置中文字
tags:
- C#
- Aspose.Cells
- Excel automation
title: 在 C# 中建立儲存格樣式 – 如何套用樣式至儲存格並置中文字
url: /zh-hant/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中建立儲存格樣式 – 完整指南：套用樣式與文字置中

是否曾需要在 Excel 工作表中 **create cell style**，卻不知從何下手？你並不孤單。在許多自動化專案中，**apply style to cell** 物件的能力是讓試算表從平淡無奇變成精緻報告的關鍵。

在本教學中，我們將逐步示範一個完整、可執行的範例，說明如何在儲存格內 **center text**、設定對齊方式，並加入細線框線——只需幾行 C# 程式碼。完成後，你將清楚了解每個步驟的意義，並能依需求自行調整。

## 你將學會什麼

- 透過 Aspose.Cells（或任何類似函式庫）完整的 **create cell style** 工作流程。
- 可直接複製貼上到 Console 應用程式的 **apply style to cell** 程式碼。
- 了解 **center text in cell**、**set cell alignment**，以及合併儲存格或自訂數字格式等邊緣情況的處理方式。
- 延伸樣式的技巧——不同字型、背景色或條件格式化。

> **先決條件：** Visual Studio 2022（或任何 C# IDE）以及 Aspose.Cells for .NET NuGet 套件。無需其他相依性。

---

## 第一步：設定專案並匯入命名空間

在 **create cell style** 之前，我們需要一個參考 Excel 函式庫的專案。

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*為什麼這很重要：* 匯入 `Aspose.Cells` 後，我們即可使用 `Workbook`、`Worksheet`、`Style` 與 `Border` 等類別。若改用其他函式庫（例如 EPPlus），類別名稱會不同，但概念相同。

---

## 第二步：建立 Workbook 並取得第一個儲存格

現在我們先取得要格式化的儲存格，進而 **create cell style**。

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

請注意我們使用 `Cell` 而非通用的 `var`——明確的型別讓新手更易讀。`PutValue` 會寫入字串，方便之後觀察樣式效果。

---

## 第三步：定義樣式 – 文字置中、加入細框線

以下是 **create cell style** 的核心。我們會設定水平對齊、細框線，以及幾項可選的細節。

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*為什麼這樣做：*  
- **HorizontalAlignment** 與 **VerticalAlignment** 共同回答「**how to center text** in a cell？」的問題。  
- 加上四側框線讓儲存格看起來像一個盒狀標籤，常用於標題列。  
- 背景色不是必須的，但可示範日後如何擴充樣式。

---

## 第四步：將定義好的樣式套用到選取的儲存格

樣式已建立，接著使用單一方法 **apply style to cell**。

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

就這樣——Aspose.Cells 會自動將樣式複製到儲存格的內部樣式集合。若需對整個區域套用相同格式，可使用 `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });`。

---

## 第五步：儲存 Workbook 並驗證結果

快速儲存後，即可在 Excel 中開啟檔案，確認文字是否真的置中且框線是否正確顯示。

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*預期輸出：* 開啟 **StyledCell.xlsx** 後，儲存格 **A1** 會顯示「Hello, styled world!」且文字水平與垂直置中，四周有細灰框線，背景為淡灰色。

---

## 常見變化與邊緣情況

### 1. 合併區域內的文字置中

若將儲存格 **A1:C1** 合併，仍想讓文字置中，必須在合併 **之後** 將樣式套用至左上角儲存格：

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. 使用數字格式

有時需要 **set cell alignment** 同時以特定格式顯示數字：

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

對齊仍保持置中，數字則顯示為 `12,345.68`。

### 3. 高效重複使用樣式

為每個儲存格都建立新 `Style` 會影響效能。建議建立一次樣式物件，於多個儲存格或區域重複使用。`StyleFlag` 類別允許只套用需要的部分，減少記憶體使用。

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## 專業小技巧與常見陷阱

- **別忘了垂直對齊**——僅水平置中在較高的列上會顯得不自然。  
- **框線類型**：`CellBorderType.Thin` 適用大多數報表，若需層次感可改用 `Medium` 或 `Dashed`。  
- **顏色處理**：在 .NET Core 環境下，請使用 `System.Drawing.Color`（需安裝 `System.Drawing.Common` 套件），否則會發生執行時錯誤。  
- **儲存格式**：若需相容舊版 Excel，將 `SaveFormat.Xlsx` 改為 `SaveFormat.Xls`。

---

![Create cell style example](https://example.com/images/create-cell-style.png "Create cell style in C#")

*Alt text: 顯示已建立儲存格樣式的螢幕截圖，文字置中且有細框線。*

---

## 完整可執行範例（直接複製貼上）

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

執行此程式，開啟 **StyledCell.xlsx**，即可看到前述的結果。隨意更改文字、框線樣式或背景色，以符合你的品牌需求。

---

## 結論

我們已從頭 **create cell style**、**apply style to cell**，並示範如何 **center text** 於水平與垂直方向。掌握這些基礎後，你可以格式化標題、突顯總計，或建立完整的報表樣板，而不必離開 C#。

接下來可以嘗試：

- **將相同樣式套用至整列**（`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`）。  
- **加入條件格式化**，依儲存格值變更背景色。  
- **匯出為 PDF**，同時保留樣式。

記住，樣式不只關乎美觀，更影響可讀性。多實驗、多迭代，你的試算表將如同程式碼般專業。

*Happy coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}