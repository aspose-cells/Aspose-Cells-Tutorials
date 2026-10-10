---
category: general
date: 2026-10-10
description: Terapkan format angka di Excel dengan cepat dengan mengimpor DataTable,
  mengatur format tanggal dan mata uang, serta mempertahankan baris header Excel dalam
  satu langkah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: id
lastmod: 2026-10-10
og_description: Terapkan format angka Excel di C# menggunakan Aspose.Cells. Pelajari
  cara mengatur format tanggal Excel, mengatur format mata uang Excel, dan mempertahankan
  baris header Excel saat mengimpor DataTable.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: Terapkan format angka Excel di C# – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Cara menerapkan format angka di Excel dengan Aspose.Cells
url: /id/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menerapkan format angka excel dengan Aspose.Cells

Jika Anda perlu **apply number format excel** saat memuat data dari `DataTable`, panduan ini menunjukkan secara tepat caranya. Anda juga akan belajar cara **set date format excel**, **set currency format excel**, dan **preserve header row excel** selama impor, sehingga lembar kerja yang dihasilkan terlihat profesional tanpa pemrosesan lanjutan.

Kami akan membahas semuanya mulai dari pemasangan pustaka hingga menulis potongan kode lengkap yang dapat dijalankan. Pada akhir panduan, Anda akan dapat mengimpor `DataTable` apa pun ke dalam workbook Excel, secara otomatis memformat kolom numerik, dan menjaga baris header tetap utuh—semua dalam beberapa baris kode C#.

## Prasyarat

Sebelum Anda mulai, pastikan Anda memiliki:

* .NET 6.0 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.6+)
* Visual Studio 2022 (atau IDE C# lain yang Anda sukai)
* **Aspose.Cells for .NET** – install via NuGet:

```bash
dotnet add package Aspose.Cells
```

* Sumber `DataTable` – contoh menggunakan metode bantuan `GetTable()` yang mengembalikan data contoh.

> **Pro tip:** Aspose.Cells adalah pustaka komersial, tetapi menyediakan mode evaluasi gratis yang menonaktifkan watermark hingga 30 hari.

## Langkah 1: Buat workbook dan akses lembar kerja pertama

Objek workbook adalah titik masuk untuk semua operasi Excel. Membuat workbook baru memberi Anda lembar kerja default pada indeks 0.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Mengapa langkah ini?*  
`Workbook` mengelola format file, mesin perhitungan, dan repositori gaya. Mengakses `Worksheet` lebih awal memungkinkan kami mengirimkan lembar target ke metode impor nanti.

## Langkah 2: Ambil data sumber sebagai DataTable

Dalam proyek nyata data sering berasal dari kueri basis data, parser CSV, atau respons API. Untuk ilustrasi kami menghasilkan `DataTable` sederhana dengan tiga kolom: **Product**, **Price**, dan **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Mengapa langkah ini?*  
`DataTable` menyediakan representasi tabular dalam memori yang dapat diimpor langsung oleh Aspose.Cells, menjaga urutan kolom dan tipe data.

## Langkah 3: Siapkan array `Style` – satu gaya per kolom

Aspose.Cells memungkinkan Anda menerapkan gaya berbeda ke setiap kolom selama impor dengan mengirimkan array objek `Style`. Panjang array harus sesuai dengan jumlah kolom dalam tabel sumber.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Mengapa langkah ini?*  
Jika Anda melewatkan pembuatan eksplisit (`CreateStyle()`), upaya mengatur `Number` akan memunculkan `NullReferenceException`. Menginisialisasi setiap `Style` memastikan penugasan selanjutnya berhasil.

## Langkah 4: Tetapkan format angka – mata uang dan tanggal

Excel mengidentifikasi format angka bawaan dengan ID.

* **14** – Mata uang (mis., `$1,234.00`)
* **22** – Tanggal pendek (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Catatan:** Jika Anda memerlukan format khusus (mis., `"¥#,##0.00"`), gunakan `Style.Custom = "¥#,##0.00"` alih-alih ID bawaan.

*Mengapa langkah ini?*  
Menerapkan **number format** yang tepat saat impor menghilangkan kebutuhan proses kedua yang mengulang sel untuk mengubah format. Ini juga menjamin bahwa **format excel cells date** dan **set currency format excel** konsisten di semua baris.

## Langkah 5: Impor DataTable sambil mempertahankan baris header

Metode `ImportDataTable` dapat menyalin data, menjaga baris pertama sebagai header, dan menerapkan gaya kolom yang telah kami siapkan.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Output yang diharapkan** – Buka `FormattedReport.xlsx` dan Anda akan melihat:

| Product | Price (currency) | ReleaseDate (date) |
|---------|------------------|--------------------|
| Widget A| $12.99           | 05/01/2023         |
| Widget B| $23.50           | 06/15/2023         |
| Widget C| $7.75            | 07/30/2023         |

Baris header tetap utuh, kolom **Price** menampilkan simbol mata uang, dan kolom **ReleaseDate** menampilkan format tanggal pendek—semua tanpa kode styling tambahan.

### Menangani kasus tepi umum

| Situasi                               | Solusi |
|----------------------------------------|----------|
| **Lebih banyak kolom daripada gaya**           | Pastikan `columnStyles.Length` sama dengan `sourceTable.Columns.Count`. Entri yang hilang akan menggunakan gaya default workbook. |
| **Nilai null di kolom numerik**     | Excel memperlakukan `null` sebagai sel kosong; format angka tetap berlaku ketika nilai dimasukkan kemudian. |
| **Mata uang khusus sesuai locale**    | Gunakan `columnStyles[i].Custom = "\"€\"#,##0.00"` dan set `columnStyles[i].Number = -1` untuk menonaktifkan ID bawaan. |
| **Tabel besar ( > 100 000 baris )**    | Pertimbangkan menggunakan overload `ImportDataTable` dengan `ImportTableOptions` untuk streaming data dan mengurangi tekanan memori. |
| **Menerapkan gaya yang sama ke beberapa kolom** | Gunakan kembali instance `Style` yang sama dalam array (mis., `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Bonus: Menggunakan string format khusus

Jika ID bawaan tidak memenuhi kebutuhan Anda, Anda dapat mendefinisikan format angka khusus:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

Pendekatan ini memberi Anda kontrol penuh atas **format excel cells date** dan **set currency format excel** di luar ID yang telah ditentukan.

## Kesimpulan

Anda kini tahu cara **apply number format excel** secara efisien saat mengimpor `DataTable` dengan Aspose.Cells. Dengan membuat array `Style` per‑kolom, menetapkan ID angka bawaan atau khusus, dan menggunakan overload `ImportDataTable` yang **preserve header row excel**, Anda dapat menghasilkan lembar kerja siap terbit dalam satu operasi.

### Apa selanjutnya?

* Jelajahi **set date format excel** dengan pola khusus seperti `"dddd, mmmm dd, yyyy"`.
* Gabungkan teknik ini dengan **conditional formatting** untuk menyoroti nilai di luar jangkauan.
* Gunakan **format excel cells date** dalam tabel pivot atau diagram untuk pelaporan dinamis.

Silakan bereksperimen dengan ID angka atau string khusus yang berbeda untuk menyesuaikan panduan gaya organisasi Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [apply number format excel – Panduan Langkah‑per‑Langkah untuk Memformat Kolom](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Buat Excel Workbook C# – Terapkan Format Mata Uang dan Impor DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Set date format in Excel dengan C# – Panduan Lengkap Format Impor](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}