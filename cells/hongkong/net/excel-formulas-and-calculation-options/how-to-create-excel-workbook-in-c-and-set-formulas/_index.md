---
category: general
date: 2026-10-01
description: 快速在 C# 中建立 Excel 工作簿，學習如何設定公式、計算餘切，並在 Aspose.Cells 中使用 PI 函數。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- how to calculate cot
- set formula in cell
- write formula to cell
- how to use pi function
language: zh-hant
lastmod: 2026-10-01
og_description: 使用 Aspose.Cells 在 C# 中建立 Excel 工作簿。學習如何設定公式、使用 PI 函數，以及計算餘切，只需幾個步驟。
og_image_alt: Diagram showing an Excel workbook created in C# with a formula in cell
  A1
og_title: 在 C# 中建立 Excel 工作簿 – 設定公式並計算餘切
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook in C# quickly, learn how to set a formula, calculate
    cotangent, and use the PI function in Aspose.Cells.
  headline: How to create Excel workbook in C# and set formulas
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何在 C# 中建立 Excel 工作簿並設定公式
url: /zh-hant/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-and-set-formulas/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中建立 Excel 工作簿並設定公式

如果您需要 **在 C# 中建立 Excel 工作簿** 的程式碼，並將公式寫入儲存格，本指南將一步一步示範。您將看到如何在工作表中設定公式、使用內建的 PI 函數，以及計算角度的餘切——全部使用 Aspose.Cells。

本教學涵蓋從初始化工作簿到取得計算結果的所有步驟，您可以直接將完整範例複製到自己的專案中，且不會遺漏任何部份。

## 前置條件

在開始之前，請確保您已具備：

* 已安裝 .NET 6.0 或更新版本  
* 有效的 Aspose.Cells 授權（或暫時的評估金鑰）  
* Visual Studio 2022 或您慣用的任何 C# IDE  

除 `Aspose.Cells` 之外，無需額外的 NuGet 套件。

## 在 C# 中建立 Excel 工作簿

第一步是實例化一個新的 `Workbook` 物件。此物件代表記憶體中的整個 Excel 檔案，並讓您存取其工作表。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                 // creates an empty .xlsx file
        var worksheet = workbook.Worksheets[0];        // the default first sheet

        // Continue with the rest of the steps...
```

以此方式建立工作簿可確保檔案已準備好進行後續操作，例如加入資料、設定儲存格樣式或寫入公式。

## 使用 PI 函數在儲存格設定公式

現在您將 **將公式寫入儲存格** A1。此公式使用 `PI()` 函數提供圓周率 π，並使用 `COT` 函數計算其餘切。

```csharp
        // Step 2: Set a formula in cell A1 (row 0, column 0)
        // The formula calculates the cotangent of π/4, which equals 1
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Continue with calculation...
```

*為什麼這很重要*：`PI()` 是 Excel 內建函數，會回傳 π 的值。將它除以 4 即得到 45°，而 `COT` 會回傳該角度的餘切。這示範了 **如何在 C# 中的 Excel 公式裡使用 pi 函數**。

## 如何使用 Aspose.Cells 計算 cot

如果您想知道 **如何計算 cot** 而不必手動換算角度，`COT` 函數會自行處理。它接受弧度制的角度，因此您可以將它與 `PI()` 結合以取得常見角度。

```csharp
        // Step 3: Recalculate the workbook so the formula is evaluated
        workbook.Calculate();

        // Step 4: Retrieve and display the calculated result
        double result = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {result}");
    }
}
```

執行程式後會輸出：

```
Cotangent of PI/4 = 1
```

因為 `COT(π/4)` 等於 1，輸出結果證實公式已正確 **設定儲存格公式** 並完成計算。

## 寫入公式到儲存格 – 其他提示

* **多重公式**：您可以使用相同的 `Formula` 屬性將公式指派給任意儲存格，例如 `worksheet.Cells["B2"].Formula = "=SIN(PI()/2)";`。
* **國際化設定**：Aspose.Cells 會遵循工作簿的語系設定，函數名稱始終保留英文 (`PI`, `COT`)，不受使用者區域設定影響。
* **效能**：若需設定數千筆公式，請批次處理後於最後一次呼叫 `workbook.Calculate()`，以避免重複重新計算。

## 完整可執行範例

以下是可直接貼到 Console 專案的完整程式碼。它包含所有必要的 `using` 陳述式，示範從工作簿建立到結果輸出的完整流程。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and obtain the first worksheet
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // Write a formula that uses the PI function and calculates cotangent
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Force calculation so the formula value is materialized
        workbook.Calculate();

        // Read the calculated value and display it
        double cotValue = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {cotValue}");

        // Optional: save the workbook to verify the formula visually
        workbook.Save("CotExample.xlsx");
    }
}
```

**預期輸出**（執行程式時）：

```
Cotangent of PI/4 = 1
```

產生的 `CotExample.xlsx` 檔案在 A1 儲存格內包含公式，您可在 Excel 中開啟並看到相同結果。

## 結論

現在您已瞭解如何撰寫 **在 C# 中建立 Excel 工作簿** 的程式碼，寫入公式、使用 `PI` 函數，並使用 Aspose.Cells **計算 cot**。此範例涵蓋了整個生命週期：工作簿建立、**設定儲存格公式**、重新計算與取得結果。

接下來您可以探索：

* 為更複雜的計算（如財務模型）**寫入公式到儲存格**。  
* 結合 **設定儲存格公式** 與條件格式，以突顯結果。  
* 將 **如何使用 pi 函數** 與三角函數圖表結合，用於科學報告。

歡迎嘗試不同的角度、函數與工作表版面配置。掌握 C# 中的公式處理，將為您開啟全自動化 Excel 報表管線的大門。祝開發順利！

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步擴充您在本章節中學到的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在自己的專案中探索其他實作方式。

- [How to Calculate Cotangent in Excel with C# – Create Workbook, Use EXPAND](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}