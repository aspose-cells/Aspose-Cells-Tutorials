---
category: general
date: 2026-10-01
description: 學習如何使用 C# 建立 Excel 工作簿、套用自訂數字格式、設定儲存格小數位數，並將工作簿另存為 XLSX，完整逐步教學。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: zh-hant
lastmod: 2026-10-01
og_description: 使用 C# 建立 Excel 工作簿，設定自訂數字格式、設定儲存格小數位，並將工作簿儲存為 XLSX。遵循此完整指南，以獲得精確的數值輸出。
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: 使用 C# 建立 Excel 活頁簿 – 自訂數字格式與 XLSX 匯出
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: 如何使用 C# 建立具自訂數字格式的 Excel 活頁簿
url: /zh-hant/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用自訂數字格式建立 Excel 工作簿

如果你需要 **create excel workbook c#** 以精確顯示數字，本指南將一步步說明如何完成。你將學會套用自訂數字格式、設定儲存格小數位，最後 **save workbook as xlsx** 供後續使用。

處理數值資料時常需要在精確度與可讀性之間取得平衡。完成本教學後，你將擁有一套可重複使用的模式，將顯示的位數限制在特定的有效數字位數，同時在檔案中保留原始值。無需外部腳本——只要 C# 與 Aspose.Cells 函式庫即可。

## 前置條件

在開始之前，請確保你已具備：

* .NET 6.0 SDK 或更新版本  
* Visual Studio 2022（或任何 C# IDE）  
* **Aspose.Cells for .NET** NuGet 套件 (`Install-Package Aspose.Cells`) – 此函式庫提供本範例中使用的 `Workbook`、`Worksheet` 與 `ExportTableOptions` 類別  

這些需求相當簡潔；相同程式碼可在 .NET Core、.NET Framework，甚至 Azure Functions 中執行。

## 第一步：Create Excel workbook C# – 初始化檔案

第一個動作是實例化一個新的 `Workbook` 物件。此物件在記憶體中代表整個 Excel 檔案，並自動包含一個預設工作表。

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**為什麼這很重要：**  
先建立工作簿可讓你擁有乾淨的畫布。預設工作表 (`Worksheets[0]`) 已可直接寫入資料，除非你的情境需要多個分頁，否則不必額外新增工作表。

## 第二步：將數值寫入儲存格

現在將範例數字寫入 **A1**。我們使用的值 (`123.456789`) 小數位數多於最終想要顯示的位數，這樣才能稍後示範四捨五入。

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**提示：** `PutValue` 會自動偵測資料型別，無需先將數字轉成字串。

## 第三步：Apply custom number format – 限制可見小數位

為了控制 Excel 顯示的方式，我們建立一個帶有 **custom number format** 的 `Style`。模式 `"0.######"` 告訴 Excel 最多顯示六位小數，但會省略尾端的零。

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**運作方式：**  
格式字串遵循 Excel 的自訂格式語法。`0` 代表必須顯示的數字，`#` 只在有意義時才顯示。結合兩者即可在保留原始精度的同時提供彈性的顯示方式。

## 第四步：Set cell decimal places – 使用 ExportTableOptions

如果你需要 **set cell decimal places** 於匯出資料（例如轉成 DataTable）時，Aspose.Cells 允許你指定 **significant digits** 的數量。此步驟確保匯出的 CSV 或 DataTable 會遵循工作簿中設定的四捨五入規則。

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**為什麼使用 `SignificantDigits`？**  
與固定小數位數不同，有效位數會在保留數值大小的同時限制精度，這正是分析師在彙總資料時常見的需求。

## 第五步：Export the worksheet data and **save workbook as xlsx**

最後，匯出資料（若需要 DataTable）並將工作簿寫入磁碟。`ExportDataTable` 會遵循先前設定的 `ExportTableOptions`，而 `workbook.Save` 則會產生標準的 XLSX 檔案。

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**預期結果：**  
當你在 Excel 開啟 *SigDigits.xlsx* 時，儲存格 **A1** 會顯示 `123.5`。底層值仍為 `123.456789`，但顯示的數字遵循 4 位有效數字的規則。若將工作表匯出為 DataTable，表格中的值同樣會四捨五入為 `123.5`。

---

## Apply custom number format to additional cells

如果你需要對一個範圍而非單一儲存格套用格式，只要重複使用同一個 `Style` 物件：

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**專業提示：** 重複使用樣式物件可減少記憶體開銷，並確保整張工作表的格式保持一致。

## How to format numbers Excel using C# – 常見變化

| 情境 | 格式字串 | 結果 |
|----------|---------------|--------|
| 固定兩位小數 | `"0.00"` | `123.46` |
| 貨幣（美國） | `"$#,##0.00"` | `$123.46` |
| 百分比（保留一位小數） | `"0.0%"` | `12,346.0%` |
| 科學記號 | `"0.00E+00"` | `1.23E+02` |

選擇符合你報表需求的格式字串。所有模式皆相容於前述 `Style.Custom` 屬性。

## Set cell decimal places dynamically based on user input

有時所需的精度在編譯時無法確定。你可以在執行時動態組合格式字串：

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**邊緣情況：** 若 `decimals` 為 0，格式會變成 `"0"`（整數顯示）。務必驗證使用者輸入，以免產生不合法的格式字串。

## Save workbook as XLSX – 最佳實踐

* **使用絕對路徑** 寫入已知目錄時（例如 `Path.Combine(Environment.CurrentDirectory, "output.xlsx")`）。  
* **Dispose** `Workbook`，若將其包在 `using` 陳述式中，可即時釋放非受控資源：

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **版本相容性：** Aspose.Cells 產生的檔案相容於 Excel 2010‑2023，後續使用者不會遇到格式問題。

---

## Full working example

以下是完整程式碼，你可以直接複製、貼上並立即執行。程式碼已包含所有必要的 `using` 指示、註解與錯誤處理。

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**驗證步驟**

1. 執行程式 (`dotnet run`)。  
2. 開啟 `SigDigits.xlsx`。  
3. 確認 **A1** 讀取為 `123.5`。  
4. 若解壓縮檔案的 XML（`.xlsx` 為 zip 壓縮檔），可在 `<c>` 元素的 `s` 屬性中看到自訂格式 `"0.######"`。

---

## Conclusion

在本教學中，你學會了如何 **create excel workbook c#**、**apply custom number format**、**set cell decimal places**，以及使用 Aspose.Cells **save workbook as xlsx**。此解決方案同時示範了 Excel 內的視覺格式化與透過 `ExportTableOptions` 進行資料匯出時的四捨五入。

從此你可以：

* 將此方法擴展至整個範圍或資料表。  
* 結合多種樣式（字型、邊框）使用 `StyleFlag`。  
* 透過迴圈資料來源，自動化報表產生並套用相同的格式化邏輯。  

歡迎自行嘗試不同的格式字串、小數位數或匯出選項，以符合你的特定報表需求。祝開發順利！

## What Should You Learn Next?

以下教學與本篇內容緊密相關，能進一步深化你所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，或在自己的專案中探索其他實作方式。

- [建立 Excel 工作簿 C# – 套用貨幣格式並匯入 DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [建立 Excel 工作簿 C# – 逐步指南與條件格式化](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [建立 Excel 工作簿 C# – 新增註解並另存為 XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}