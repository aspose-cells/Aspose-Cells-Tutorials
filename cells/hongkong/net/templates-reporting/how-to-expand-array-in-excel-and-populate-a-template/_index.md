---
category: general
date: 2026-09-18
description: 學習如何使用 EXPAND 函數在 Excel 中展開陣列、填充 Excel 範本，並使用 C# 建立動態範圍的 Excel 工作表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- populate excel template
- dynamic range excel
- use expand function
- expand array formula
language: zh-hant
lastmod: 2026-09-18
og_description: 如何使用 EXPAND 函數在 Excel 中展開陣列、填充 Excel 範本，並使用 C# 程式碼建立動態範圍的 Excel 解決方案。
og_image_alt: Excel worksheet showing expanded 5x5 array and Smart Markers result
og_title: 如何在 Excel 中擴充陣列並填入範本
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to expand array in Excel using the EXPAND function, populate
    an Excel template, and create a dynamic range Excel worksheet with C#.
  headline: How to expand array in Excel and populate a template
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: 如何在 Excel 中展開陣列並填充範本
url: /zh-hant/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中展開陣列並填充範本

如果你需要在 Excel 中 **展開陣列** 同時填寫預先設計好的範本，本指南將提供完整、端對端的解決方案。結合 `EXPAND` 函數與 Aspose.Cells 的 Smart Markers，你可以將單一儲存格參照轉換為 5 × 5 的範圍，並自動將 `{IsActive}` 等標記替換為即時資料。

你將會看到如何 **populate excel template**、建立 **dynamic range excel**，以及在 C# 專案中正確 **use expand function**。完成本教學後，你將擁有一個可執行的程式，能載入 `.xlsx` 檔案、展開陣列公式、套用 Smart Markers，並儲存結果。

## 前置條件

* .NET 6.0 或更新版本（程式碼亦可在 .NET Core 3.1+ 上執行）
* Aspose.Cells for .NET（NuGet 套件 `Aspose.Cells`）
* 包含佔位公式儲存格（例如 `B2`）與 Smart Marker（如 `{IsActive}`）的 Excel 活頁簿
* 具備 C# 與 Excel 公式的基本知識

> **專業提示：** `EXPAND` 函數僅在 Microsoft 365 版 Excel 與 Excel 2021+ 中可用。舊版 Excel 會回傳 `#NAME?` 錯誤。

## 步驟 1：使用 EXPAND 函數展開陣列

第一步是載入活頁簿，並寫入 `EXPAND` 公式，將單一來源儲存格轉換為更大的矩陣。  

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the template layout
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Apply the EXPAND function to cell B2.
        // =EXPAND(A2,5,5) expands the array that starts at A2 into a 5‑row by 5‑column range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";
```

為什麼這很重要：`EXPAND` 免除手動在列與欄之間複製公式的需求。當來源儲存格（`A2`）變更時，整個 5 × 5 區塊會自動更新，為你提供一個會隨資料變動的 **dynamic range excel**。

## 步驟 2：使用 Smart Markers 填充 Excel 範本

Smart Markers 讓你在範本中嵌入佔位符，這些佔位符會被 C# 物件的值取代。這是 **populate excel template** 的最便利方式，無需逐格撰寫程式碼。

```csharp
        // Prepare an anonymous object that matches the marker names in the template.
        var data = new { IsActive = true };

        // Apply Smart Markers. The marker {IsActive} inside a formula like
        // =IF({IsActive}, "Active", "Inactive") will be replaced with the value from the object.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);
```

`SmartMarkersProcessor().Apply` 會掃描整張工作表，找到 `{IsActive}`，並注入布林值。公式隨即自動計算為 `"Active"` 或 `"Inactive"`。

## 步驟 3：驗證展開的範圍與填充結果

在套用 `EXPAND` 公式與 Smart Markers 後，你可以以程式方式讀取幾個儲存格，以確認所有操作如預期般執行。

```csharp
        // Optional: read a cell from the expanded block to confirm the value.
        var sampleValue = ws.Cells["B2"].Value; // top‑left cell of the expanded range
        Console.WriteLine($"Top‑left of expanded range: {sampleValue}");

        // Read the marker result cell (assume it is C2)
        var status = ws.Cells["C2"].StringValue;
        Console.WriteLine($"Status from Smart Marker: {status}");
```

執行程式時應會印出 `A2` 的原始值（或陣列結果），以及根據 `IsActive` 旗標顯示 **Active** 或 **Inactive**。

## 步驟 4：儲存活頁簿 – 最終輸出

最後，將修改過的活頁簿寫入磁碟。此步驟示範了從載入、展開、填充到持久化檔案的完整流程。

```csharp
        // Save the workbook with the expanded array and populated markers.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

儲存的 `output.xlsx` 現在包含由 `EXPAND` 公式產生的 5 × 5 矩陣，以及顯示 `{IsActive}` 值的儲存格。於 Excel 中開啟該檔案，即可看到動態範圍的運作。

## 邊緣情況與最佳實踐

| 情況 | 建議 |
|------|------|
| Excel 版本不支援 `EXPAND` | 改用傳統的 `=OFFSET` 或 `=INDEX` 公式，或升級至 Office 365。 |
| 需要展開至可變大小 | 在 `EXPAND` 中使用 `ROWS(source)` 與 `COLUMNS(source)` 以實現真正的動態性。 |
| 同一工作表中有多個 Smart Markers | 只呼叫一次 `SmartMarkersProcessor().Apply`，並傳入複合資料物件。 |
| 大型活頁簿（> 10 000 列） | 在寫入公式時停用計算 (`workbook.Settings.CheckFormula = false`)。 |

## 完整範例程式

以下是完整、獨立的程式碼，你可以直接複製貼上至新的 Console 專案中。

```csharp
using System;
using Aspose.Cells;

class ExpandArrayDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that serves as the template.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Write the EXPAND formula to create a 5x5 dynamic range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";

        // 3️⃣ Prepare data for Smart Markers.
        var data = new { IsActive = true };

        // 4️⃣ Apply Smart Markers – replaces {IsActive} in any formula or text.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);

        // 5️⃣ (Optional) Verify a couple of cells.
        Console.WriteLine($"Expanded top‑left: {ws.Cells["B2"].Value}");
        Console.WriteLine($"Marker result: {ws.Cells["C2"].StringValue}");

        // 6️⃣ Save the final workbook.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
        Console.WriteLine("Workbook saved successfully.");
    }
}
```

**執行程式時的預期輸出**（假設 `A2` 包含數字 `42`）：

```
Expanded top‑left: 42
Marker result: Active
Workbook saved successfully.
```

開啟 `output.xlsx` 後會看到一個由 `A2` 衍生值填滿的 5 × 5 區塊，以及顯示 **Active** 的儲存格。

## 結論

現在你已了解如何在 Excel 中使用 `EXPAND` 函數 **how to expand array**，如何使用 Smart Markers **populate excel template**，以及如何建立會自動依來源資料調整的 **dynamic range excel**。此範例亦示範了在實務 C# 自動化情境中正確使用 **use expand function** 與 **expand array formula** 的方式。

接下來，考慮擴充此解決方案：

* 將固定的 `5,5` 維度改為 `ROWS(A2:A10), COLUMNS(A2:E2)`，以實現真正的可變範圍。
* 結合多個 Smart Markers 產生完整報表（例如員工清單、銷售表格）。
* 探索 Aspose.Cells 的樣式 API，讓展開的區塊自動套用格式。

歡迎嘗試不同的來源陣列、標記名稱與活頁簿版面配置。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上進一步說明。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [Export Data to Excel: Populate a Template from an Array in C#](/cells/english/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/)
- [How to create array in Excel with C# – Step-by-Step Guide](/cells/english/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/)
- [Processing Data Using Array Function in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}