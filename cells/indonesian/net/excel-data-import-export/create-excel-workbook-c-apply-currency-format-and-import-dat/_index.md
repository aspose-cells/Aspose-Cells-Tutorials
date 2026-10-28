---
category: general
date: 2026-03-30
description: Buat workbook Excel C# dengan format mata uang. Pelajari cara mengimpor
  DataTable, menambahkan format angka di Excel, dan menerapkan format mata uang pada
  kolom dalam hitungan menit.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: id
og_description: Buat workbook Excel dengan C# dan langsung format sel sebagai mata
  uang. Tutorial langkah demi langkah ini menunjukkan cara mengimpor DataTable ke
  Excel dan menambahkan format angka Excel untuk sebuah kolom.
og_title: Buat Workbook Excel C# – Panduan Pemformatan Mata Uang
tags:
- Aspose.Cells
- C#
- Excel automation
title: Buat Workbook Excel C# – Terapkan Format Mata Uang dan Impor DataTable
url: /id/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Workbook Excel C# – Terapkan Format Mata Uang dan Impor DataTable

Pernahkah Anda perlu **create Excel workbook C#** yang sudah terlihat seperti laporan yang rapi? Mungkin Anda menarik angka penjualan dari basis data dan ingin kolom harga ditampilkan dalam dolar tanpa harus mengutak‑atik Excel secara manual. Kedengarannya familiar? Anda tidak sendiri—banyak pengembang mengalami masalah ini saat pertama kali mengotomatisasi ekspor Excel.

Dalam panduan ini kami akan membahas solusi lengkap yang siap dijalankan yang **creates an Excel workbook C#**, mengimpor `DataTable`, dan **formats the Price column as currency**. Pada akhir panduan Anda akan memiliki file bernama `StyledTable.xlsx` yang dapat Anda buka dan melihat angka yang diformat dengan rapi. Tidak diperlukan pemrosesan tambahan.

> **What you’ll learn**
> - Cara menyiapkan Aspose.Cells dalam proyek .NET  
> - Cara **import datatable to excel** dengan array gaya  
> - Cara **add number format excel** untuk kolom tertentu  
> - Tips menangani lebih banyak kolom atau lokal yang berbeda  

> **Prasyarat**  
> - .NET 6+ (atau .NET Framework 4.6+) terinstal  
> - Paket NuGet Aspose.Cells untuk .NET (`Install-Package Aspose.Cells`)  
> - Familiaritas dasar dengan C# dan DataTables  

---

## Langkah 1: Siapkan DataTable (import datatable to excel)

First, we need some sample data. In a real‑world app you’d likely fill this table from a DB query, but a hard‑coded example keeps things simple.

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*Mengapa ini penting*: The `DataTable` is the bridge between your business data and the Excel file. Aspose.Cells can import it directly, preserving column names and data types.

---

## Langkah 2: Buat Workbook Baru (create excel workbook c#)

Now we create the actual Excel file object. Think of it as the blank canvas you’ll paint on.

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** If you need multiple sheets, call `workbook.Worksheets.Add()` and give each a meaningful name.

---

## Langkah 3: Definisikan Gaya Mata Uang (format cells currency)

Aspose.Cells lets you craft a `Style` object that describes how cells should look. For currency we use the built‑in number format ID 164 (`"$#,##0.00"`).

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*Why not just set the format string?* Using the built‑in ID ensures compatibility across Excel versions and avoids locale‑specific quirks.

---

## Langkah 4: Bangun Array Gaya (apply currency format column)

When importing a `DataTable`, you can pass an array of `Style` objects—one per column. `null` means “use the default style”. Here we apply `priceStyle` only to the second column.

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

If you later add more columns, just extend the array accordingly. The length of `columnStyles` must match the number of columns you’re importing, otherwise Aspose will throw an exception.

---

## Langkah 5: Impor DataTable dengan Gaya (import datatable to excel)

Now the magic happens—our `DataTable` lands in the worksheet, and the price column instantly shows as currency.

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*What if you have more than two columns?* Just expand `columnStyles` so each column gets the appropriate style (or `null` for default). This is the cleanest way to **add number format excel** selectively.

---

## Langkah 6: Simpan Workbook (create excel workbook c#)

Finally, we write the file to disk. Choose any folder you have write access to.

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

Open `StyledTable.xlsx` in Excel and you should see:

| Product | Price |
|---------|-------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

The **Price** column is already formatted as currency—no extra steps needed.

---

## Kasus Tepi & Variasi

### Lebih Banyak Kolom, Format Berbeda

If you need to **format cells currency** for several columns (e.g., Cost, Tax, Total), create a separate `Style` for each and populate `columnStyles` accordingly:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Mata Uang Spesifik Lokal

For Euro or British Pound, use different built‑in IDs (e.g., 165 for `€#,##0.00`). Alternatively, set a custom format string:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Set Data Besar

Aspose.Cells can handle millions of rows, but memory consumption grows with style objects. Reuse a single `Style` instance for all currency columns to keep the footprint low.

### Gaya yang Hilang

If `columnStyles` is shorter than the number of columns, Aspose will apply the default style to the remaining columns. This is handy when you only care about a few columns.

---

## Contoh Kerja Penuh (Semua Langkah Digabung)

Below is the complete program you can copy‑paste into a console app. It includes all the pieces we discussed, plus a few helpful comments.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Expected result:** Opening `StyledTable.xlsx` shows the `Price` column with a dollar sign and two decimal places, exactly as the `format cells currency` instruction demanded.

---

## Pertanyaan yang Sering Diajukan

**Q: Does this work with .NET Core?**  
A: Absolutely. Aspose.Cells is .NET‑standard compliant, so you can target .NET 5, .NET 6, or later without changes.

**Q: What if my DataTable has 10 columns but I only want to format column 5?**  
A: Create a `Style[]` of length 10, fill positions 0‑4 and 6‑9 with `null`, and put your custom style at index 4 (zero‑based). Aspose will respect each entry.

**Q: Can I hide the header row?**  
A: After import, set `worksheet.Cells.Rows[0].Hidden = true;` or simply pass `false` for the `includeColumnNames` parameter in `ImportDataTable`.

---

## Kesimpulan

We’ve just **created an Excel workbook C#**, imported a `DataTable`, and **applied a currency format column** using Aspose.Cells. The primary steps—preparing data, defining a style, building a style array, importing with `ImportDataTable`, and saving—cover the core of most Excel‑automation tasks.

From here you might explore:

- **add number format excel** for dates or percentages  
- Exporting multiple worksheets in a single file  
- Using **format cells currency** with locale‑specific symbols  
- Automating chart creation based on the same data  

Give those a try, and you’ll quickly become the go‑to person for Excel reporting in your team. Got a twist you’d like to share? Drop a comment below—happy coding!  

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}