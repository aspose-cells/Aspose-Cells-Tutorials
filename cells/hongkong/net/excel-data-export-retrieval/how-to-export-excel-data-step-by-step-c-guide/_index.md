---
category: general
date: 2026-03-29
description: 學習如何將 Excel 表格匯出為純文字、將字串寫入檔案，以及使用 C# 將 Excel 表格轉換為 CSV 或 TXT。包括完整程式碼與技巧。
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: zh-hant
og_description: 如何在 C# 中將 Excel 表格匯出為文字檔。取得完整解決方案、程式碼及最佳實踐，將 Excel 表格轉換並儲存為 TXT 檔。
og_title: 如何匯出 Excel 資料 – 完整 C# 教學
tags:
- C#
- Excel
- File I/O
title: 如何匯出 Excel 資料 – C# 步驟教學
url: /zh-hant/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何匯出 Excel 資料 – 完整 C# 指南

有沒有想過 **如何在不手動開啟試算表的情況下匯出 Excel** 資料？也許你需要把資料表丟到一個簡單的文字檔給舊系統使用，或是想快速產生 CSV 供資料分析管線使用。在本教學中，我們將一步步示範一個實用的端對端解決方案，**將字串寫入檔案**，並說明如何 **將 Excel 表格** 資料轉換成分隔文字格式（使用 C#）。

我們會涵蓋從載入活頁簿、挑選正確的表格、設定匯出選項，到最後將結果儲存為 `.txt` 檔案的全部流程。完成後，你就能 **將表格匯出為 CSV**（或任何你想要的分隔符），同時學會幾個 **saving txt file C#** 的小技巧。全程不需要外部工具——只要幾個 NuGet 套件與少量程式碼即可。

---

## 你需要的環境

- **.NET 6.0+**（或如果你偏好傳統版，使用 .NET Framework 4.7.2）
- **Syncfusion.XlsIO** NuGet 套件（`ExportTableOptions` 類別就在這裡）
- 基本的 C# IDE（Visual Studio、VS Code、Rider 任一皆可）
- 一個包含至少一個表格的 Excel 活頁簿（範例中會使用 `ws.Tables[0]`）

> Pro tip: If you don’t already have the Syncfusion library, run  
> `dotnet add package Syncfusion.XlsIO.Net.Core` from the command line.

---

## Step 1 – Open the Workbook and Grab the First Table  

首先要載入 Excel 檔案，並取得包含表格的工作表參考。這一步很重要，因為 **convert excel table** 的操作是針對 `ITable` 物件，而不是原始儲存格範圍。

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*Why this matters:* Opening the workbook with `using` ensures all unmanaged resources are released, preventing file‑lock issues later when you try to **write string to file**.

---

## Step 2 – Configure Export Options (Plain Text, No Headers, Semicolon Delimiter)  

接著告訴 Syncfusion 我們希望如何序列化表格。`ExportTableOptions` 讓你可以切換是否包含標頭、選擇分隔符，並決定是取得字串還是位元組陣列。

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*Why this matters:* Setting `IncludeHeaders = false` often matches the expectations of downstream systems that already know the column order. Changing the delimiter is how you **export table as CSV** with a custom separator.

---

## Step 3 – Export the Table to a String  

設定好選項後，呼叫 `ExportToString`。此方法會抓取整個表格（包括所有列），並回傳一個可直接寫入檔案的單一字串。

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*Why this matters:* The `ExportToString` call does the heavy lifting of converting the Excel grid into a delimited format. It respects the `Delimiter` you set, so you get a clean **export table as csv** result without extra processing.

---

## Step 4 – Write the Exported Text to a File  

最後，把字串寫入磁碟。`File.WriteAllText` 是最簡單的 **save txt file C#** 方法；它會在檔案不存在時自動建立，若已存在則直接覆寫。

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*Why this matters:* By writing the string directly, you avoid an extra conversion step. The file now contains rows like `Value1;Value2;Value3`, ready for any downstream parser.

---

## Full Working Example (All Steps in One Place)  

以下是完整、可直接複製貼上的程式碼，將前面討論的所有步驟整合在一起，並加入錯誤處理與說明註解。

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**Expected output** (the content of `ExportedTable.txt`):

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

每一行對應原始 Excel 表格中的一列，欄位以分號分隔。如果將 `Delimiter = ","` 改成逗號，就會得到傳統的 CSV 檔案。

---

## Common Questions & Edge Cases  

### What if My Workbook Has Multiple Tables?  
You can simply change `ws.Tables[0]` to the appropriate index, or loop through `ws.Tables`:

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### How Do I Include Column Headers?  
Set `IncludeHeaders = true` in `ExportTableOptions`. This is useful when the downstream system expects a header row.

### Can I Export to a Different Folder Dynamically?  
Absolutely. Use `Path.Combine` with `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` or any user‑provided path to make the solution more flexible.

### What About Large Files?  
For massive tables, consider streaming the output instead of loading the whole string into memory:

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### Does This Work on .NET Core?  
Yes—Syncfusion.XlsIO supports .NET 5/6/7. Just reference the appropriate NuGet package and you’re good to go.

---

## Pro Tips for Reliable Exports  

- **Validate the file path** before writing. A missing directory will throw `DirectoryNotFoundException`.  
- **Check `ExportAsString`** only when the table fits comfortably in memory; otherwise, use `ExportToStream` for huge datasets.  
- **Mind the culture**: if your data contains commas as decimal separators, choose a semicolon (`;`) or tab (`\t`) delimiter to avoid CSV parsing errors.  
- **Version lock**: Syncfusion occasionally changes API signatures. Pin the NuGet version (`<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`) to keep your build reproducible.

---

## Conclusion  

In this guide we demonstrated **how to export Excel** tables to plain‑text files using C#. By loading the workbook, configuring `ExportTableOptions`, exporting the table to a string, and finally **writing the string to file**, you now have a robust pattern for **convert excel table** data, **export table as csv**, and **save txt file C#** tasks.  

Feel free to experiment—swap the delimiter, include headers, or loop over multiple tables. The same approach works for generating CSV reports, feeding data into legacy parsers, or simply archiving spreadsheet contents as lightweight text files.

Got more scenarios you’d like to tackle? Maybe you need to **write string to file** asynchronously, or you want to zip the output on the fly. Check out our next tutorials on *asynchronous file I/O in C#* and *zipping files with .NET* to keep the momentum going.

Happy coding! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}