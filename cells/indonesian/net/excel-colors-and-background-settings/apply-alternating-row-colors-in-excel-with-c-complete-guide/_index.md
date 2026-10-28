---
category: general
date: 2026-07-03
description: Terapkan warna baris bergantian saat Anda mengimpor datatable ke Excel
  menggunakan C#. Pelajari cara mengekspor datatable C# ke Excel, menyimpan tabel
  berformat di Excel, dan mempertahankan format workbook.
draft: false
keywords:
- apply alternating row colors
- import datatable to excel
- export c# datatable to excel
- save styled table excel
- save workbook with formatting
language: id
og_description: Terapkan warna baris bergantian di Excel menggunakan C#. Tutorial
  ini menunjukkan cara mengimpor datatable ke Excel, mengekspor datatable C# ke Excel,
  dan menyimpan workbook dengan pemformatan.
og_title: Terapkan Warna Baris Bergantian di Excel dengan C# – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  headline: Apply Alternating Row Colors in Excel with C# – Complete Guide
  type: TechArticle
- description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  name: Apply Alternating Row Colors in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: '| ID | Name | Department | HireDate | |----|---------|------------|------------|
      | 1 | Alice | Finance | 15‑01‑2020 | | 2 | Bob | HR | 23‑06‑2019 | | 3 | Charlie
      | IT | 10‑03‑2021 | | 4 | Diana | Marketing | 05‑11‑2018 |'
  - name: What if my DataTable has thousands of rows?
    text: The `ImportDataTable` method streams data efficiently, but you might hit
      memory limits on very large tables. In such cases, consider splitting the export
      into multiple worksheets or using the `ImportDataTable` overload that lets you
      specify a start row and column.
  - name: Can I use custom colors instead of the built‑in ones?
    text: Absolutely. Just replace the `ForegroundColor` assignments in `styleWhite`
      and `styleGray` with any `System.Drawing.Color` you prefer—think pastel blues
      or corporate brand colors.
  - name: How do I ensure the alternating style works when the user adds rows later?
    text: If users edit the file manually, the original style array won’t automatically
      extend. A quick workaround is to convert the range into an Excel Table (`ListObject`)
      after import; Excel then repeats the pattern for new rows.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataExport
title: Terapkan Warna Baris Bergantian di Excel dengan C# – Panduan Lengkap
url: /id/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Terapkan Warna Baris Bergantian di Excel dengan C# – Panduan Lengkap

Pernahkah Anda perlu **apply alternating row colors** saat mengekspor `DataTable` C# ke Excel? Anda bukan satu-satunya—para pengembang terus menanyakan cara membuat spreadsheet tersebut tampak rapi tanpa harus mengutak‑atik Excel secara manual setelahnya. Kabar baiknya? Anda dapat melakukannya secara programatis hanya dengan beberapa baris kode.

Dalam tutorial ini kami akan membahas **import datatable to excel**, menunjukkan cara **export c# datatable to excel** dengan tabel yang bergaya, dan akhirnya **save styled table excel** sambil mempertahankan formatnya. Pada akhir tutorial Anda akan dapat **save workbook with formatting** yang tampak siap untuk pertemuan dengan klien.

## Prasyarat

- .NET 6.0 atau lebih baru (contoh menggunakan .NET 6, tetapi versi terbaru apa pun dapat digunakan)
- Aspose.Cells untuk .NET (versi trial gratis atau berlisensi) – perpustakaan ini memudahkan styling
- Sumber `DataTable` (bisa berasal dari basis data, CSV, atau koleksi dalam memori)

> **Pro tip:** Jika Anda belum memiliki Aspose.Cells, Anda dapat mengunduhnya dari NuGet dengan `dotnet add package Aspose.Cells`.

## Langkah 1: Siapkan Proyek dan Muat Data Anda

Pertama, buat aplikasi console (atau proyek C# apa pun) dan tambahkan pernyataan `using` yang diperlukan. Kemudian ambil data ke dalam `DataTable`. Untuk ilustrasi kami akan menghasilkan tabel sederhana secara langsung.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Retrieve the source data as a DataTable
        DataTable sourceTable = GetSampleData();

        // The rest of the steps follow...
    }

    // Helper that creates a dummy DataTable
    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

**Mengapa ini penting:** Memiliki `DataTable` yang siap berarti Anda dapat **import datatable to excel** dalam satu panggilan, menghilangkan kebutuhan penyisipan sel‑per‑sel secara manual.

## Langkah 2: Buat Workbook dan Tentukan Gaya Baris Bergantian

Sekarang kami akan menginstansiasi `Workbook` baru. Trik untuk **apply alternating row colors** terletak pada `ImportTableOptions.StyleArray`. Kami akan menggunakan dua gaya bawaan pertama (biasanya putih dan abu‑abu muda) tetapi Anda dapat menyesuaikannya nanti.

```csharp
// Step 2: Create a new workbook
Workbook workbook = new Workbook();

// Define two simple styles: white (default) and light gray
Style styleWhite = workbook.Styles[workbook.Styles.Add()];
styleWhite.ForegroundColor = System.Drawing.Color.White;
styleWhite.Pattern = BackgroundType.Solid;

Style styleGray = workbook.Styles[workbook.Styles.Add()];
styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242); // light gray
styleGray.Pattern = BackgroundType.Solid;

// Step 3: Set up ImportTableOptions with the alternating styles
ImportTableOptions importOptions = new ImportTableOptions
{
    // The array alternates between the two styles for each row
    StyleArray = new Style[] { styleWhite, styleGray }
};
```

**Penjelasan:** `ImportTableOptions` memberi tahu Aspose.Cells cara memperlakukan setiap baris selama impor. Dengan menyediakan `StyleArray` berisi dua entri, perpustakaan secara otomatis memberi warna pada setiap baris ganjil dengan gaya pertama dan setiap baris genap dengan gaya kedua—tepat apa yang Anda butuhkan untuk **apply alternating row colors**.

## Langkah 3: Tarik DataTable ke Worksheet (Termasuk Header)

Dengan workbook dan gaya yang siap, kini kami **import datatable to excel**. Metode `ImportDataTable` melakukan pekerjaan berat: menulis header kolom, menghormati style array, dan menempatkan data mulai dari sel A1.

```csharp
// Step 4: Import the DataTable into the first worksheet (include column headers)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells.ImportDataTable(sourceTable, true, importOptions);
```

**Mengapa kami menyertakan `true` untuk argumen kedua:** Ini memberi tahu metode untuk menulis nama kolom sebagai baris pertama, yang penting untuk laporan yang tampak profesional.

## Langkah 4: Sesuaikan Tabel (Opsional namun Berguna)

Jika Anda ingin tabel menyesuaikan lebar kolom secara otomatis atau menambahkan baris filter, beberapa baris tambahan akan membuatnya bersinar.

```csharp
// Auto‑fit all columns for readability
sheet.AutoFitColumns();

// Add a filter to the header row
sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";
```

Penyesuaian ini tidak memengaruhi warna bergantian tetapi meningkatkan pengalaman pengguna secara keseluruhan pada file **save styled table excel**.

## Langkah 5: Simpan Workbook Sambil Menjaga Semua Formatting

Akhirnya, kami menulis file ke disk. Metode `Save` mempertahankan setiap gaya yang kami tetapkan, memastikan baris bergantian tetap utuh.

```csharp
// Step 5: Save the workbook with the styled table
string outputPath = @"C:\Temp\StyledEmployees.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Saat Anda membuka `StyledEmployees.xlsx`, Anda akan melihat tabel bersih di mana baris bergantian antara putih dan abu‑abu muda—tepat petunjuk visual yang banyak pengguna andalkan untuk keterbacaan.

### Output yang Diharapkan

| ID | Name    | Department | HireDate   |
|----|---------|------------|------------|
| 1  | Alice   | Finance    | 15‑01‑2020 |
| 2  | Bob     | HR         | 23‑06‑2019 |
| 3  | Charlie | IT         | 10‑03‑2021 |
| 4  | Diana   | Marketing  | 05‑11‑2018 |

- Baris 1, 3 … → latar belakang putih  
- Baris 2, 4 … → latar belakang abu‑abu muda  

Itulah seluruh proses **save workbook with formatting**.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika DataTable saya memiliki ribuan baris?

Metode `ImportDataTable` mengalirkan data secara efisien, tetapi Anda mungkin mencapai batas memori pada tabel yang sangat besar. Dalam kasus tersebut, pertimbangkan untuk membagi ekspor ke beberapa worksheet atau menggunakan overload `ImportDataTable` yang memungkinkan Anda menentukan baris dan kolom mulai.

### Bisakah saya menggunakan warna kustom alih-alih yang bawaan?

Tentu saja. Cukup ganti penugasan `ForegroundColor` pada `styleWhite` dan `styleGray` dengan `System.Drawing.Color` apa pun yang Anda sukai—misalnya biru pastel atau warna merek perusahaan.

```csharp
styleWhite.ForegroundColor = System.Drawing.Color.LightBlue;
styleGray.ForegroundColor = System.Drawing.Color.LightCyan;
```

### Bagaimana saya memastikan gaya bergantian tetap berfungsi ketika pengguna menambahkan baris nanti?

Jika pengguna mengedit file secara manual, style array asli tidak akan otomatis memperluas. Solusi cepat adalah mengonversi rentang menjadi Tabel Excel (`ListObject`) setelah impor; Excel kemudian mengulangi pola untuk baris baru.

```csharp
int lastRow = sheet.Cells.MaxDataRow;
int lastCol = sheet.Cells.MaxDataColumn;
string tableRange = $"A1:{CellsHelper.ColumnIndexToName(lastCol)}{lastRow + 1}";
ListObject table = sheet.ListObjects[sheet.ListObjects.Add(tableRange, true)];
```

Sekarang setiap baris baru mewarisi warna bergantian.

## Contoh Lengkap yang Berfungsi (Semua Langkah dalam Satu Tempat)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve source data
        DataTable sourceTable = GetSampleData();

        // 2️⃣ Create workbook and define alternating styles
        Workbook workbook = new Workbook();

        Style styleWhite = workbook.Styles[workbook.Styles.Add()];
        styleWhite.ForegroundColor = System.Drawing.Color.White;
        styleWhite.Pattern = BackgroundType.Solid;

        Style styleGray = workbook.Styles[workbook.Styles.Add()];
        styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242);
        styleGray.Pattern = BackgroundType.Solid;

        ImportTableOptions importOptions = new ImportTableOptions
        {
            StyleArray = new Style[] { styleWhite, styleGray }
        };

        // 3️⃣ Import DataTable (including headers)
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(sourceTable, true, importOptions);

        // 4️⃣ Optional polish
        sheet.AutoFitColumns();
        sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";

        // 5️⃣ Save the styled workbook
        string outputPath = @"C:\Temp\StyledEmployees.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

Jalankan program, buka file yang dihasilkan, dan Anda akan langsung melihat warna bergantian diterapkan—tanpa perlu format manual.

## Kesimpulan

Kami baru saja menunjukkan cara **apply alternating row colors** saat Anda **import datatable to excel** menggunakan C#. Proses ini mencakup semua yang Anda butuhkan untuk **export c# datatable to excel**, **save styled table excel**, dan **save workbook with formatting** yang tampak profesional langsung dari awal.

Langkah selanjutnya? Coba tukar dua gaya untuk tema kustom, atau ubah rentang menjadi Tabel Excel sehingga pengguna dapat menyortir dan memfilter sambil mempertahankan pola warna. Anda juga dapat menjelajahi conditional formatting melalui `ConditionalFormattingCollection` untuk petunjuk visual yang lebih dinamis.

Ada tantangan lain

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Apply Colors & Backgrounds in Excel using Aspose.Cells for .NET](/cells/english/net/formatting/colors-and-background/)
- [Automate Excel Theme Colors Using Aspose.Cells .NET for Efficient Formatting](/cells/english/net/formatting/automate-excel-theme-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}