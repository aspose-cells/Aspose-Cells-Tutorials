---
category: general
date: 2026-10-26
description: 學習如何在 C# 中使用 WRAPCOLS 將範圍拆分為列，套用 WRAPROWS 以拆分為行，並以程式方式將工作簿儲存為 XLSX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: zh-hant
lastmod: 2026-10-26
og_description: 如何在 C# 中使用 WRAPCOLS 將資料分割成欄位，使用 WRAPROWS 進行列分割，並將活頁簿儲存為 XLSX。跟隨完整的逐步指南。
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: 如何在 C# 中使用 WRAPCOLS – 分割範圍並另存為 XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何在 C# 中使用 WRAPCOLS 並將工作簿另存為 XLSX
url: /zh-hant/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 WRAPCOLS 並將活頁簿儲存為 XLSX

如果你需要 **如何使用 WRAPCOLS** 來重新排列 Excel 檔案中的資料，本指南將提供完整、可執行的解決方案。你將看到 **excel wrapcols 範例**、學習如何使用 **WRAPROWS 將範圍拆分為列**，最後完成 **將活頁簿儲存為 XLSX**——全部以 **程式方式** 完成。

在 C# 中操作 Excel 通常意味著建立活頁簿、套用公式，並將檔案寫入磁碟。以下程式碼使用 Aspose.Cells 函式庫，讓你在未安裝 Microsoft Office 的環境下也能操作 Excel 檔案。完成本教學後，你將能 **以程式方式建立 excel 活頁簿**、水平與垂直拆分資料，並產生乾淨的 `.xlsx` 檔案供後續處理使用。

## 前置條件

開始之前，請確保你已具備：

* .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.7+）
* 參考 **Aspose.Cells** NuGet 套件  
  ```bash
  dotnet add package Aspose.Cells
  ```
* 基本的 C# 與 Excel 公式概念

## 步驟 1：如何使用 WRAPCOLS 將範圍拆分為欄

**WRAPCOLS** 函式會將一維範圍的值依指定的欄數展開。在此範例中，我們從 `A1:A10` 取得值，並要求 WRAPCOLS 產生三欄。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **結果：** `C1:E4` 儲存格現在包含原本的十筆資料，排列成三欄（最後一欄保留剩餘的項目）。

![說明如何使用 WRAPCOLS 將範圍拆分為 Excel 中的欄位的螢幕截圖](image-url.png)

## 步驟 2：使用 WRAPROWS 將範圍拆分為列

**WRAPCOLS** 以水平方式展開，而 **WRAPROWS** 則相反：它會將範圍依指定的列數展開。此處我們取 `B1:B10` 的值，並在 `F1` 起始位置排列成兩列。

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **結果：** 公式將十筆值分佈於兩列，填滿 `F1:K2` 儲存格。

## 步驟 3：將活頁簿儲存為 XLSX

套用公式後，最後一步是將檔案寫入磁碟。**將活頁簿儲存為 xlsx** 的操作會把記憶體中的活頁簿以現代 OpenXML 格式寫出。

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### 儲存後檔案的樣子

在 Excel 開啟 `wrapcols_wraprows_output.xlsx` 後，你會看到：

| C | D | E |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
|        |        | Item 10 |

以及

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Value 1 | Value 3 | Value 5 | Value 7 | Value 9 | |
| Value 2 | Value 4 | Value 6 | Value 8 | Value 10 | |

公式仍保留在儲存格中，之後若變更來源範圍，結果會自動更新。

## 步驟 4：常見變形與例外情況

### 更改欄數或列數

* **更多欄位：** 增加 `WRAPCOLS` 的第二個參數。  
  範例：`=WRAPCOLS(A1:A10,5)` 會產生五欄，資料不足的格子會留空。
* **動態欄數：** 使用儲存格參考取代硬編碼數字。  
  `=WRAPCOLS(A1:A10, G1)` 其中 `G1` 含有欲設定的欄數。

### 處理空白或非數值儲存格

WRAPCOLS 與 WRAPROWS 預設會忽略空白儲存格，但仍會保留非空值的順序。若需保留空白，可在套用 WRAPCOLS 前先以 `IFERROR` 或 `TEXT` 函式包住來源範圍。

### 儲存為其他格式

雖然本教學聚焦於 **將活頁簿儲存為 xlsx**，Aspose.Cells 亦支援多種格式（`.xls`、`.csv`、`.pdf` 等）：

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## 專業技巧與常見陷阱

* **專業技巧：** 若要在儲存後立即評估公式，請設定 `Workbook.Settings.CalcEngineEnabled = true`。
* **注意事項：** 大範圍來源可能產生巨大的溢位區域，影響效能。建議限制範圍大小或將操作分散至多個工作表。
* **執行緒安全性：** Aspose.Cells 物件 **不** 具備執行緒安全性。若在平行處理檔案，請為每個執行緒建立獨立的 `Workbook` 實例。

## 結論

現在你已掌握 **如何使用 WRAPCOLS** 將垂直範圍拆分為多欄、**如何使用 WRAPROWS 將範圍拆分為列**，以及 **如何在完成轉換後將活頁簿儲存為 XLSX**。依照上述步驟，你可以 **以程式方式建立 excel 活頁簿**、套用強大的溢位公式，並自動產生可直接分享的 Excel 檔案，省去手動操作的麻煩。

### 接下來該做什麼？

* 探索 **條件格式** 以突顯溢位資料。
* 結合 **WRAPCOLS** 與 **SORT** 或 **FILTER** 建立動態儀表板。
* 使用 Aspose.Cells 的 **圖表 API**，直接從程式碼視覺化重新排列的資料。

祝開發順利，盡情自動化你的 Excel 工作流程！

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化你所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在專案中探索其他實作方式。

- [how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [How to Use WRAPCOLS – Complete Guide for C# Excel Automation](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}