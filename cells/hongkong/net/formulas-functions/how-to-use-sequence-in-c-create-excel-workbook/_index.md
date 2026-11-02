---
category: general
date: 2026-07-03
description: 如何在 C# 中使用 SEQUENCE 於 Excel 產生遞增數字。學習只需幾行程式碼，即可使用 C# 與 ASP.NET 建立 Excel
  工作簿。
draft: false
keywords:
- how to use sequence
- create excel workbook c#
- asp.net create excel file
- generate incremental numbers excel
language: zh-hant
og_description: 如何在 C# 中使用 SEQUENCE 於 Excel 產生遞增數字。逐步指南教你使用 C# 及 ASP.NET 建立 Excel
  工作簿與 Excel 檔案。
og_title: 如何在 C# 中使用 SEQUENCE – 建立 Excel 活頁簿
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  headline: How to Use SEQUENCE in C# – Create Excel Workbook
  type: TechArticle
- description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  name: How to Use SEQUENCE in C# – Create Excel Workbook
  steps:
  - name: Why Use SEQUENCE Instead of a Loop?
    text: '- **Performance** – Excel does the math on its own engine, which is highly
      optimized. - **Maintainability** – The formula is self‑documenting; anyone opening
      the sheet instantly knows the intent. - **Dynamic resizing** – Change the `rows`
      argument and the spill range expands automatically.'
  - name: Pro Tip
    text: 'If you need the workbook in memory (e.g., to send it over a web API), use
      a `MemoryStream`:'
  - name: What If the Client Uses an Older Excel Version?
    text: 'Dynamic arrays (including `SEQUENCE`) were introduced in Excel 365/2019.
      If you need backward compatibility, fall back to a manual fill:'
  type: HowTo
- questions:
  - answer: No. `SEQUENCE` is a non‑iterative function; a simple `CalculateFormula()`
      call is enough.
    question: Do I need to enable iterative calculation?
  - answer: 'Change the second argument: `=SEQUENCE(1,5,10,2)` spills across B1:F1.'
    question: What if I want a horizontal spill?
  - answer: Absolutely. For example, `=INDEX(A:A, SEQUENCE(5,1,10,2))` can pull rows
      from another column.
    question: Can I combine SEQUENCE with other functions?
  - answer: The file size impact of a formula is negligible. Only when you start populating
      millions of cells manually does size become an issue.
    question: Is the workbook size a concern?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- ASP.NET
title: 如何在 C# 中使用 SEQUENCE – 建立 Excel 工作簿
url: /zh-hant/net/formulas-functions/how-to-use-sequence-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 SEQUENCE – 建立 Excel 工作簿

有沒有想過 **如何使用 SEQUENCE** 從 C# 輸出一系列數字到 Excel 工作表？你並不是唯一有此疑問的人。無論你是在建立報表儀表板、為資料格提供資料，或只是需要快速產生 ID，掌握這個技巧都能讓你免於手動撰寫迴圈。

在本教學中，我們將 **在 C# 中建立 Excel 工作簿**，在 A1 儲存格插入 `SEQUENCE` 動態陣列公式，最終得到一欄遞增的數字。我們還會示範如何從 ASP.NET 控制器提供該檔案下載——是的，**ASP.NET 建立 Excel 檔案** 也會涵蓋。完成後，你將能以單行程式碼 **產生 Excel 風格的遞增數字**。

## 需要的環境

- .NET 6+（此程式碼亦可在 .NET Framework 4.6+ 上執行）  
- **Aspose.Cells for .NET** NuGet 套件（或任何提供 `Workbook`/`Worksheet` 物件的函式庫）  
- 若想嘗試網頁下載功能，請準備一個基本的 ASP.NET Core 或 MVC 專案  

就這樣。無需額外的 COM 互操作，也不需要安裝 Office。

---

## 如何使用 SEQUENCE 產生遞增數字

Excel 的 `SEQUENCE(rows, [columns], [start], [step])` 函式會回傳一個 **spill** 範圍。在本例中，我們需要 5 列、1 欄，起始值為 10，步長為 2。公式如下：

```excel
=SEQUENCE(5,1,10,2)
```

當 Excel 計算此公式時，A1:A5 儲存格會分別顯示 **10、12、14、16、18**。最棒的是，我們不需要撰寫任何 C# 迴圈——公式會自行完成計算。

以下是完整的 C# 程式碼片段，會建立工作簿、插入公式、強制計算，並儲存檔案。

```csharp
using Aspose.Cells;
using System.IO;

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 2️⃣ Grab the first worksheet (Aspose creates one by default)
Worksheet sheet = workbook.Worksheets[0];

// 3️⃣ Insert the SEQUENCE formula – this will spill a 5‑row column starting at 10, step 2
sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";

// 4️⃣ Force calculation so the spilled range is materialized
workbook.CalculateFormula();

// 5️⃣ Save to disk (you can change the path as needed)
workbook.Save("DynamicArray.xlsx");
```

**預期輸出** – 開啟 *DynamicArray.xlsx* 後會看到：

| A |
|---|
| 10 |
| 12 |
| 14 |
| 16 |
| 18 |

這就是在 C# 中 **如何使用 SEQUENCE** 的完整說明。簡單吧？但讓我們再深入探討一下。

### 為何使用 SEQUENCE 而非迴圈？

- **效能** – Excel 使用自身的運算引擎執行計算，效能高度最佳化。  
- **可維護性** – 公式本身即具說明性，任何開啟工作表的人都能立即了解意圖。  
- **動態調整大小** – 只要變更 `rows` 參數，spill 範圍會自動擴展。

---

## 建立 Excel 工作簿 C# – 步驟說明

如果你是 **create excel workbook c#** 的新手，以下檢查清單可協助你避免常見的陷阱。

1. **加入 Aspose.Cells 套件**  
   ```bash
   dotnet add package Aspose.Cells
   ```
   （你也可以使用 ClosedXML 或 EPPlus，但此處示範的 API 與上述程式碼相符。）
2. **設定授權**（試用版可選）。  
   ```csharp
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Total.NET.lic");
   ```
3. **實例化 `Workbook`** – 取得一個全新的空白工作簿。
4. **參照工作表** – `workbook.Worksheets[0]` 為預設名稱為 *Sheet1* 的工作表。
5. **套用 SEQUENCE 公式** – 如前所示。
6. **計算** – `workbook.CalculateFormula()` 會強制執行 spill；否則檔案中只會留下公式。
7. **儲存** – 你可以寫入磁碟、`MemoryStream`，或直接回傳至 HTTP 回應。

### 小技巧

如果需要在記憶體中保留工作簿（例如透過 Web API 傳送），請使用 `MemoryStream`：

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
byte[] excelBytes = ms.ToArray(); // ready to return or attach
```

---

## ASP.NET 建立 Excel 檔案 – 串流至瀏覽器

既然我們已了解 **create excel workbook c#**，接下來將它整合到 ASP.NET Core 控制器，讓使用者即時下載檔案。

```csharp
using Aspose.Cells;
using Microsoft.AspNetCore.Mvc;
using System.IO;

[Route("api/[controller]")]
public class ExcelController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult Download()
    {
        // 1️⃣ Build the workbook (same steps as before)
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";
        workbook.CalculateFormula();

        // 2️⃣ Save to a memory stream
        using var ms = new MemoryStream();
        workbook.Save(ms, SaveFormat.Xlsx);
        ms.Position = 0; // reset stream position

        // 3️⃣ Return the file as a download
        const string fileName = "DynamicArray.xlsx";
        return File(ms, 
                    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", 
                    fileName);
    }
}
```

當使用者存取 `/api/excel/download` 時，瀏覽器會提示下載 *DynamicArray.xlsx*。該檔案已因 `SEQUENCE` 公式而包含 **generated incremental numbers excel** 欄位。

### 若客戶端使用較舊的 Excel 版本，該怎麼辦？

動態陣列（包括 `SEQUENCE`）於 Excel 365/2019 之後才推出。若需相容舊版，請改用手動填入：

```csharp
// Alternative for older Excel: write numbers directly
for (int i = 0; i < 5; i++)
{
    sheet.Cells[i, 0].PutValue(10 + i * 2); // column 0 = A
}
```

上述程式碼示範了不依賴新函式的傳統 **generate incremental numbers excel** 方法。

---

## 常見問題與邊緣案例

- **是否需要啟用迭代計算？**  
  不需要。`SEQUENCE` 為非迭代函式，只要呼叫 `CalculateFormula()` 即可。
- **如果想要水平 spill 該怎麼做？**  
  只需變更第二個參數：`=SEQUENCE(1,5,10,2)` 會在 B1:F1 之間水平展開。
- **能否將 SEQUENCE 與其他函式結合使用？**  
  當然可以。例如，`=INDEX(A:A, SEQUENCE(5,1,10,2))` 能從另一欄位取出相應列。
- **工作簿大小會是問題嗎？**  
  公式本身對檔案大小的影響可以忽略不計。只有在手動填入數百萬儲存格時，檔案大小才會成為問題。

---

## 結論

我們已示範如何在 C# 中 **how to use sequence** 以 **create excel workbook c#**，並透過 **ASP.NET create excel file** 服務該工作簿，展示了不撰寫迴圈即可 **generate incremental numbers excel** 的簡潔方法。關鍵在於：讓 Excel 自身的動態陣列引擎負責計數，讓 .NET 程式碼專注於協調。

歡迎自行實驗——更換 `rows`、`start` 或 `step` 參數、水平 spill，或將公式與 `IF`、`FILTER` 結合，以產生更進階的報表。準備好後，可嘗試串接多個工作表，或將工作簿匯出為 CSV 供下游系統使用。

有任何想法想分享嗎？在下方留言，或在 GitHub 上私訊我。祝編程愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上延伸技術。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索其他實作方式。

- [如何使用 Aspose.Cells .NET 建立與設定 Excel 工作簿：一步步指南](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [如何使用 Aspose.Cells for .NET 建立與儲存 Excel 檔案：完整指南](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [如何使用 Aspose.Cells for .NET 建立與樣式化 Excel 工作簿（2023 指南）](/cells/english/net/formatting/create-style-excel-workbooks-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}