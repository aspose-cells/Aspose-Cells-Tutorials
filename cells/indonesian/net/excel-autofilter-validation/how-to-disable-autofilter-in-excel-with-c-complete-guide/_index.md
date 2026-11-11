---
category: general
date: 2026-10-26
description: nonaktifkan autofilter di Excel menggunakan C#. Tutorial ini menunjukkan
  cara menghapus autofilter dari tabel Excel secara programatis dan menyertakan contoh
  kerja lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- disable autofilter in excel
- remove autofilter from excel table
- Excel automation C#
- Aspose.Cells filter handling
- programmatic Excel editing
language: id
lastmod: 2026-10-26
og_description: nonaktifkan autofilter di Excel dengan cepat. Ikuti panduan ini untuk
  menghapus autofilter dari tabel Excel menggunakan C# dan Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet where the autofilter has been disabled
og_title: Nonaktifkan autofilter di Excel dengan C# – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  headline: How to disable autofilter in Excel with C# – complete guide
  type: TechArticle
- description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  name: How to disable autofilter in Excel with C# – complete guide
  steps:
  - name: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
    text: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
  - name: Click any column header – you should **not** see the drop‑down filter arrow.
    text: Click any column header – you should **not** see the drop‑down filter arrow.
  - name: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
    text: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Cara menonaktifkan autofilter di Excel dengan C# – panduan lengkap
url: /id/net/excel-autofilter-validation/how-to-disable-autofilter-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menonaktifkan autofilter di Excel dengan C# – panduan lengkap

Jika Anda perlu **menonaktifkan autofilter di Excel**, panduan ini menunjukkan secara tepat cara melakukannya dari C#. Baik Anda sedang membersihkan laporan sebelum dipublikasikan atau mengotomatiskan pipeline ekspor data, menghapus filter memastikan lembar kerja menampilkan setiap baris. Anda juga akan belajar cara **menghapus autofilter dari tabel Excel** dalam satu panggilan yang andal.

Kami akan menggunakan pustaka **Aspose.Cells for .NET** yang populer karena dapat bekerja tanpa memerlukan Excel terinstal di server. Pada akhir tutorial ini Anda akan memiliki aplikasi konsol mandiri yang memuat workbook, menemukan tabel pertama, dan menonaktifkan autofilter-nya. Solusi ini bekerja dengan file .xlsx yang dibuat oleh Excel 2007 atau yang lebih baru.

## Apa yang Anda butuhkan

| Prerequisite | Why it matters |
|--------------|----------------|
| .NET 6.0 or later | Menyediakan runtime untuk kode C#. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Memberikan akses programatik ke lembar kerja, tabel, dan autofilter. |
| A sample Excel file (`Sample.xlsx`) that contains at least one table with an autofilter applied | Kode beroperasi pada tabel pertama; memiliki tabel memungkinkan kami mendemonstrasikan penonaktifan filter. |
| Visual Studio 2022 (or any C# IDE) | Mempermudah pembuatan dan debugging aplikasi konsol. |

> **Pro tip:** Jika Anda lebih suka alternatif gratis, Anda dapat menyesuaikan kode untuk menggunakan **ClosedXML** atau **EPPlus**; ide inti—menetapkan properti `AutoFilter` tabel ke `null`—tetap sama.

## Langkah 1: Buat proyek konsol baru

Buka terminal atau command prompt Visual Studio dan jalankan:

```bash
dotnet new console -n ExcelFilterDemo
cd ExcelFilterDemo
dotnet add package Aspose.Cells
```

Ini membuat proyek baru bernama `ExcelFilterDemo` dan menambahkan pustaka Aspose.Cells.

## Langkah 2: Muat workbook dan temukan lembar kerja pertama

Operasi logis pertama adalah membuka file workbook. Aspose.Cells membaca file ke dalam objek `Workbook` yang memberi Anda akses langsung ke lembar kerja dan tabel.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the Excel file you want to modify
        const string inputPath = "Sample.xlsx";

        // Load the workbook into memory
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Mengapa langkah ini?** Memuat workbook diperlukan sebelum Anda dapat memanipulasi objek Excel apa pun. Menggunakan lembar kerja pertama (`Worksheets[0]`) mencerminkan skenario umum di mana data utama berada di lembar pertama.

## Langkah 3: Dapatkan tabel pertama yang didefinisikan pada lembar kerja

Tabel Excel (juga disebut ListObjects) adalah kontainer yang menyimpan data terstruktur. Setiap tabel dapat memiliki autofilter masing-masing. Untuk menghapus filter kita pertama-tama memerlukan referensi ke objek tabel.

```csharp
        // Get the first table on the worksheet.
        // If the worksheet has no tables, this will throw an IndexOutOfRangeException.
        Table table = worksheet.Tables[0];
```

> **Kasus tepi:** Jika workbook mungkin berisi lembar kerja tanpa tabel, bungkus akses dengan pemeriksaan `if (worksheet.Tables.Count > 0)`. Ini mencegah error runtime dan membuat solusi lebih kuat.

## Langkah 4: Nonaktifkan autofilter untuk tabel

Penonaktifan sebenarnya hanya satu baris: tetapkan `null` ke properti `AutoFilter` dari objek `Table`. Ini menghapus semua kriteria filter dan menghilangkan panah dropdown dari baris header.

```csharp
        // Disable the autofilter – this clears any applied filter.
        table.AutoFilter = null;
```

Setelah baris ini dijalankan, tabel berperilaku seperti rentang biasa tanpa UI filter.

## Langkah 5: Simpan workbook yang telah dimodifikasi

Akhirnya, tulis perubahan kembali ke disk. Anda dapat menimpa file asli atau membuat file baru untuk menjaga sumber tetap utuh.

```csharp
        // Save the workbook. Use a new file name to avoid overwriting the original.
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

### Kode sumber lengkap

Menggabungkan semua bagian, program lengkap terlihat seperti ini:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the original Excel file
        const string inputPath = "Sample.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (worksheet.Tables.Count == 0)
        {
            System.Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Get the first table
        Table table = worksheet.Tables[0];

        // Disable the autofilter – clears any applied filter
        table.AutoFilter = null;

        // Save the modified workbook
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

Jalankan program dengan `dotnet run`. Setelah eksekusi, buka `Sample_NoFilter.xlsx` di Excel; Anda akan melihat panah filter telah menghilang dan semua baris terlihat.

## Verifikasi bahwa autofilter benar‑benar telah hilang

1. Buka file yang disimpan (`Sample_NoFilter.xlsx`) di Microsoft Excel.  
2. Klik header kolom mana saja – Anda **tidak** harus melihat panah filter dropdown.  
3. Jika masih melihat panah, periksa kembali bahwa tabel yang Anda targetkan memang tabel dengan filter. Anda dapat menampilkan semua tabel dengan:

```csharp
foreach (var tbl in worksheet.Tables)
{
    System.Console.WriteLine($"Table name: {tbl.Name}, Has AutoFilter: {tbl.AutoFilter != null}");
}
```

Output konsol seharusnya melaporkan `Has AutoFilter: False` untuk tabel yang Anda modifikasi.

## Kesalahan umum dan cara menghindarinya

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| `IndexOutOfRangeException` at `worksheet.Tables[0]` | Lembar kerja tidak memiliki tabel. | Tambahkan pengecekan `if (worksheet.Tables.Count == 0)` sebelum mengakses. |
| Saved file still shows filters | Anda mengedit lembar kerja atau tabel yang salah. | Gunakan `wb.Worksheets["SheetName"]` atau iterasi melalui `wb.Worksheets` untuk menemukan tabel yang tepat. |
| The program crashes on older .NET versions | Aspose.Cells memerlukan .NET 6.0+ untuk paket terbaru. | Upgrade target framework di file `.csproj`. |
| NullReferenceException when `table.AutoFilter` is already null | Anda memanggil kode dua kali pada file yang sama tanpa memuat ulang. | Muat ulang workbook atau periksa `if (table.AutoFilter != null)` sebelum menetapkan. |

## Memperluas solusi

Sekarang Anda tahu cara **menonaktifkan autofilter di Excel**, Anda mungkin ingin:

* **Hapus autofilter dari tabel Excel** hanya ketika kondisi tertentu terpenuhi (mis., ketika flag pengguna diatur). Tambahkan pernyataan `if` di sekitar `table.AutoFilter = null;`.
* **Terapkan filter baru** secara programatik setelah menghapus yang lama, menggunakan `table.AutoFilter.Range` dan `table.AutoFilter.AddFilterColumn(...)`.
* **Proses beberapa tabel** dalam workbook yang sama dengan melakukan loop melalui `worksheet.Tables` dan menonaktifkan setiap filter.

Ekstensi ini mengikuti pola yang sama seperti yang ditunjukkan di atas dan menjaga basis kode tetap bersih.

## Kesimpulan

Anda kini memiliki metode yang ringkas dan siap produksi untuk **menonaktifkan autofilter di Excel** menggunakan C#. Dengan memuat workbook, mengakses tabel pertama, dan menetapkan `table.AutoFilter = null`, Anda secara efektif **menghapus autofilter dari tabel Excel** tanpa interaksi manual. Contoh lengkap ini dapat dikompilasi, dijalankan, dan menghasilkan file bersih yang siap untuk otomatisasi atau distribusi lebih lanjut.

Silakan bereksperimen dengan tabel tambahan, logika bersyarat, atau pustaka alternatif. Jika Anda menemukan kasus tepi, kembali ke bagian pemecahan masalah atau jelajahi dokumentasi lengkap Aspose.Cells untuk penanganan filter lanjutan. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara menghapus autofilter dari tabel Excel menggunakan C#](/cells/english/net/excel-autofilter-validation/how-to-remove-autofilter-from-excel-tables-using-c/)
- [Bersihkan UI filter di Excel dengan C# – Hapus Tombol AutoFilter](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [Cara Menggunakan AutoFilter dalam Otomasi Excel C# – Panduan Langkah‑per‑Langkah Lengkap](/cells/english/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}