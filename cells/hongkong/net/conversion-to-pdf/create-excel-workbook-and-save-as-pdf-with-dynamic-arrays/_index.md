---
category: general
date: 2026-09-15
description: 在 C# 中建立 Excel 活頁簿，並學習如何在使用 EXPAND 函數展開動態陣列時，將活頁簿另存為 PDF。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: zh-hant
lastmod: 2026-09-15
og_description: 在 C# 中建立 Excel 活頁簿，並快速將活頁簿儲存為 PDF，同時使用 EXPAND 函數溢出動態陣列。
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: 建立 Excel 工作簿並以動態陣列儲存為 PDF
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: 建立 Excel 工作簿並以動態陣列儲存為 PDF
url: /zh-hant/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 Excel 活頁簿並以動態陣列儲存為 PDF

如果您需要以程式方式 **create Excel workbook**，然後 **save workbook as PDF**，本指南將向您展示在 C# 中的完整端到端解決方案。您還將看到如何使用 **EXPAND function** 來 **spill dynamic array** 結果，這是生成陣列的現代方法，無需 VBA。

無論您是在構建報告服務、ERP 系統的匯出功能，還是資料驅動的儀表板，以下步驟都能讓您產生活頁簿、以 smart‑marker 資料填充，並產生保留進階字型功能的 PDF。

## 前置條件

* .NET 6.0 或更新版本（此程式碼亦可在 .NET Framework 4.8 上執行）
* 最近版本的 **Aspose.Cells for .NET**（v25.8 或更新）——它提供 `Workbook`、`PdfSaveOptions` 和 `SmartMarkerProcessor`。
* 如 Visual Studio 2022 等 IDE（任何能編譯 C# 的編輯器皆可）。

將 NuGet 套件加入您的專案：

```bash
dotnet add package Aspose.Cells --version 25.8
```

## 步驟 1：建立 Excel 活頁簿並設定第一個工作表

第一個任務是 **create Excel workbook**，並取得預設工作表的參考。此工作表將承載動態陣列與 Smart Marker 範本。

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*為什麼這很重要*：實例化 `Workbook` 會分配內部活頁簿結構，而存取 `Worksheets[0]` 則可直接取得可使用的工作表，無需手動新增。

## 步驟 2：使用 EXPAND 函數 **spill dynamic array**

Excel 的 **EXPAND function** 能將靜態陣列常值轉換為任意大小的溢位範圍。此處我們請 Excel 將 `{1,2,3}` 展開為從 `A1` 開始的 5 行 × 1 列範圍。

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*為什麼這很重要*：使用 `EXPAND` 可避免在 C# 中手動迴圈。引擎會計算溢位範圍並直接將值寫入工作表，之後會出現在 PDF 中。

## 步驟 3：儲存活頁簿為 PDF 同時保留字型變體選擇器

當您需要 **save workbook as PDF** 時，亦可啟用進階排版功能，例如字型變體選擇器（自 Aspose.Cells v25.8 起提供）。這可確保 PDF 正確呈現複雜文字。

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*為什麼這很重要*：將 `FontVariationSelectors` 設為 `true` 對依賴字形變體的語言（如中文、日文、表情符號）至關重要。產生的 PDF 會與螢幕上的 Excel 觀感相同。

## 步驟 4：插入參照巢狀資料來源的 Smart Marker 範本

Smart Markers 允許您直接在工作表中嵌入佔位符。以下範本將產生訂單及其項目的清單。

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*為什麼這很重要*：將範本放在 `A1`，即告訴 Aspose.Cells 從此處開始展開資料。`:` 語法（`Items:ItemName`）指示處理器遍歷巢狀集合。

## 步驟 5：定義巢狀資料來源（包含項目的訂單）

我們建立一個匿名的訂單陣列，每筆訂單皆包含自己的項目物件集合。這類似典型的主從情境。

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*為什麼這很重要*：此巢狀結構示範了透過 Smart Markers **how to create dynamic array in Excel**，無需撰寫 VBA 或手動儲存格迴圈。

## 步驟 6：處理 Smart Markers 並儲存最終的 Excel 檔案

現在我們將活頁簿與資料來源交給 `SmartMarkerProcessor`。處理完畢後，佔位符會被實際列取代，我們將結果儲存為一般的 `.xlsx` 檔案。

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*為什麼這很重要*：`SmartMarkerProcessor` 會自動展開範本、建立所需列，並填入資料。最終的活頁簿可在 Excel 中開啟，以驗證每筆訂單及其項目正確顯示。

## 預期輸出

* **VarSelector.pdf** – 顯示數字 1‑3 向下溢位至五行的 PDF 檔案，使用您啟用的任何 OpenType 字型變體呈現。
* **NestedSmartMarker.xlsx** – 具有以下列的 Excel 檔案（從 `A1` 開始）：

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

PDF 版本保留相同的數字溢位，因為工作表狀態在 Smart Marker 處理之前已儲存；若需要最終資料的 PDF，可在處理後再次儲存 PDF。

## 專業提示與常見陷阱

| Tip | Explanation |
|-----|-------------|
| **Reuse the same `PdfSaveOptions`** | 一次建立選項物件並重複使用，可避免渲染上細微差異（例如缺少變體選擇器）。 |
| **Call `ws.Calculate()` after setting formulas** | 若未明確計算，檢查程式化時溢位範圍可能保持空白。 |
| **Place Smart Marker templates on a clean sheet** | 將範本與現有資料混合可能導致意外的列插入。盡可能使用專用工作表。 |
| **Mind the file paths** | 使用 `Path.Combine(Environment.CurrentDirectory, "output.pdf")` 可避免在不同機器上硬編碼目錄。 |
| **Version check** | `FontVariationSelectors` 僅在 25.8 版以上可用；舊版會忽略此屬性且不拋出例外。 |

## 後續步驟

既然您已了解如何 **create Excel workbook**、**spill dynamic array**，以及 **save workbook as PDF**，接下來可以探索：

- 在 PDF 轉換前加入圖表或圖片。
- 使用 `Save` 重載將相同活頁簿匯出為其他格式（例如 HTML、CSV）。
- 使用 **Smart Marker expressions** (`${Orders.Total:SUM(Items.Price)}`) 即時計算彙總。
- 將此程式碼整合至 ASP.NET Core API，讓使用者可直接從 Web 端點下載產生的 PDF。

---

**Summary** – 本教學示範了如何 **create Excel workbook**、使用 **EXPAND function** 來 **spill dynamic array**、嵌入可處理巢狀資料來源的 **Smart Marker**，最後 **save workbook as PDF** 並保留進階字型功能。完整可執行的範例可直接複製到任何 C# 專案，並依您的資料結構進行調整。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在此處示範的技巧之上。每個資源皆提供完整可運作的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}