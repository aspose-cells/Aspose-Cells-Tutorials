---
category: general
date: 2026-08-07
description: Hapus autofilter dari Excel di C# dengan cepat. Pelajari cara mematikan
  filter Excel, menghapus filter tabel Excel, dan membersihkan autofilter tabel Excel
  dengan Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- remove autofilter from excel
- how to turn off excel filter
- delete excel table filter
- clear excel table autofilter
language: id
lastmod: 2026-08-07
og_description: Hapus autofilter dari Excel di C# dan pelajari cara mematikan filter
  Excel, menghapus filter tabel Excel, serta membersihkan autofilter tabel Excel menggunakan
  Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet after remove autofilter from excel
og_title: Menghapus autofilter dari Excel dengan C# – tutorial langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Remove autofilter from Excel in C# quickly. Learn how to turn off Excel
    filter, delete Excel table filter, and clear Excel table autofilter with Aspose.Cells.
  headline: Remove autofilter from Excel in C# – complete guide
  type: TechArticle
- description: Remove autofilter from Excel in C# quickly. Learn how to turn off Excel
    filter, delete Excel table filter, and clear Excel table autofilter with Aspose.Cells.
  name: Remove autofilter from Excel in C# – complete guide
  steps:
  - name: Expected output
    text: 'Open `output.xlsx` in Excel:'
  - name: Multiple tables in the same worksheet
    text: 'If the worksheet contains more than one table, iterate over the collection:'
  - name: Removing filter from a specific column only
    text: 'Aspose.Cells does not expose a column‑level `AutoFilter` removal, but you
      can recreate the table without the filter:'
  - name: Working with older Excel formats (*.xls)
    text: Aspose.Cells supports the legacy binary format automatically. The same code
      works; just ensure the file extension matches the input file.
  - name: Handling large workbooks
    text: For files larger than 100 MB, enable the **LoadOptions** to use the **MemoryOptimized**
      mode, which reduces memory pressure while still allowing table manipulation.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Hapus autofilter dari Excel di C# – panduan lengkap
url: /id/net/excel-autofilter-validation/remove-autofilter-from-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hapus autofilter dari Excel di C# – panduan lengkap

Jika Anda perlu **menghapus autofilter dari Excel** saat memproses file secara programatik, panduan ini menunjukkan cara melakukannya secara tepat. Anda akan mempelajari cara tercepat untuk mematikan filter Excel, menghapus filter tabel Excel, dan membersihkan autofilter tabel Excel menggunakan pustaka Aspose.Cells.

Tutorial ini mencakup semuanya mulai dari menyiapkan proyek hingga memverifikasi bahwa workbook output tidak lagi menampilkan panah filter. Tidak ada langkah manual yang diperlukan, dan kode ini bekerja dengan file .xlsx apa pun yang berisi tabel dengan AutoFilter.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

- .NET 6.0 atau yang lebih baru terpasang  
- Visual Studio 2022 (atau IDE C# apa saja)  
- Lisensi untuk **Aspose.Cells for .NET** (evaluasi gratis dapat digunakan untuk pengujian)  
- File Excel (`input.xlsx`) yang berisi setidaknya satu tabel dengan AutoFilter yang diterapkan  

Anda juga perlu menambahkan paket NuGet Aspose.Cells ke proyek Anda:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Simpan workbook di folder yang dapat dibaca/ditulis oleh aplikasi Anda tanpa hak istimewa tambahan untuk menghindari `UnauthorizedAccessException`.

![hapus autofilter dari excel](/assets/remove-autofilter.png "hapus autofilter dari excel – Lembar Excel tanpa panah filter")

## Hapus autofilter dari Excel – langkah 1: muat workbook

Operasi pertama adalah membuka workbook sumber. Memuat file ke memori memberi Anda akses penuh ke lembar kerja, tabel, dan properti mereka.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook containing a table with an AutoFilter
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Mengapa ini penting:* `Workbook` adalah objek pusat di Aspose.Cells. Ia mem-parsing paket XLSX dan membangun model objek yang mencerminkan struktur internal Excel, memungkinkan Anda memanipulasi tabel secara langsung.

## Cara mematikan filter Excel – langkah 2: akses lembar kerja target

File Excel dapat memiliki banyak lembar kerja, tetapi contoh ini fokus pada lembar pertama. Sesuaikan indeks jika data Anda berada di tempat lain.

```csharp
// Step 2: Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Mengapa ini penting:* Setiap `Worksheet` memiliki koleksi tabelnya sendiri. Dengan mengambil lembar yang tepat, Anda memastikan bahwa tabel yang dimodifikasi adalah yang diinginkan.

## Hapus filter tabel Excel – langkah 3: temukan tabel pertama

Tabel disimpan dalam koleksi `Tables` pada sebuah worksheet. Anda dapat mengiterasinya, tetapi untuk kesederhanaan kami mengambil tabel pertama.

```csharp
// Step 3: Retrieve the first table on the worksheet
Table table = worksheet.Tables[0];
```

*Mengapa ini penting:* Objek `Table` menyimpan properti `AutoFilter` yang mengontrol UI filter. Mengakses tabel merupakan prasyarat untuk menghapus filter.

## Bersihkan autofilter tabel Excel – langkah 4: hapus AutoFilter

Menetapkan properti `AutoFilter` ke `null` menghapus UI filter sepenuhnya. Data yang mendasarinya tetap tidak berubah.

```csharp
// Step 4: Remove the AutoFilter by setting it to null
table.AutoFilter = null;
```

*Mengapa ini penting:* Ketika `AutoFilter` bernilai `null`, Excel tidak lagi menampilkan panah drop‑down, dan semua kriteria filter yang sebelumnya diterapkan dihapus. Ini adalah operasi inti untuk **menghapus filter tabel excel**.

## Simpan workbook – langkah 5: verifikasi hasilnya

Akhirnya, tulis workbook yang telah dimodifikasi ke disk. File yang disimpan akan dibuka di Excel tanpa panah filter apa pun.

```csharp
// Step 5: Save the workbook; the table is now a plain data table without filter UI
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

### Output yang diharapkan

Buka `output.xlsx` di Excel:

- Tabel ditampilkan sebagai data biasa—tidak ada panah filter yang muncul di baris header.  
- Semua baris terlihat, menegaskan bahwa filter telah dibersihkan.  

Jika Anda masih melihat panah, periksa kembali bahwa file sumber memang berisi AutoFilter dan Anda menargetkan indeks tabel yang tepat.

## Variasi umum dan kasus tepi

### Beberapa tabel dalam satu worksheet

Jika worksheet berisi lebih dari satu tabel, iterasikan koleksinya:

```csharp
foreach (Table tbl in worksheet.Tables)
{
    tbl.AutoFilter = null; // clear filter for each table
}
```

### Menghapus filter hanya pada kolom tertentu

Aspose.Cells tidak menyediakan penghapusan `AutoFilter` tingkat kolom, tetapi Anda dapat membuat ulang tabel tanpa filter:

```csharp
// Capture existing data range
CellArea range = table.DisplayRange;

// Remove the table (including filter)
worksheet.Tables.RemoveAt(table.Index);

// Re‑add the table without AutoFilter
Table newTable = worksheet.Tables[worksheet.Tables.Add(range.StartRow, range.StartColumn, range.EndRow, range.EndColumn, true)];
```

### Bekerja dengan format Excel lama (*.xls)

Aspose.Cells secara otomatis mendukung format biner legacy. Kode yang sama berfungsi; pastikan ekstensi file sesuai dengan file input.

### Menangani workbook besar

Untuk file yang lebih besar dari 100 MB, aktifkan **LoadOptions** untuk menggunakan mode **MemoryOptimized**, yang mengurangi tekanan memori sambil tetap memungkinkan manipulasi tabel.

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx) { MemoryOptimization = true };
Workbook largeWorkbook = new Workbook("large_input.xlsx", options);
```

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin, tempel, dan jalankan sebagai aplikasi konsol.

```csharp
using System;
using Aspose.Cells;

namespace RemoveExcelAutoFilter
{
    class Program
    {
        static void Main()
        {
            // Define file paths
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\output.xlsx";

            // Load the workbook
            Workbook workbook = new Workbook(inputPath);

            // Access the first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Ensure the worksheet contains at least one table
            if (worksheet.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }

            // Retrieve the first table and clear its AutoFilter
            Table table = worksheet.Tables[0];
            table.AutoFilter = null;

            // Save the modified workbook
            workbook.Save(outputPath);

            Console.WriteLine($"AutoFilter removed. Saved to {outputPath}");
        }
    }
}
```

Jalankan program, lalu buka `output.xlsx`. Anda akan melihat bahwa operasi **menghapus autofilter dari excel** berhasil dan lembar menampilkan tabel data biasa.

## Kesimpulan

Sekarang Anda tahu cara **menghapus autofilter dari Excel** menggunakan C#. Dengan memuat workbook, mengakses tabel target, dan menetapkan `AutoFilter` ke `null`, Anda dapat **mematikan filter Excel**, **menghapus filter tabel Excel**, dan **membersihkan autofilter tabel Excel** dalam satu langkah yang andal.  

Selanjutnya, pertimbangkan untuk menjelajahi topik terkait seperti **memformat tabel Excel dengan Aspose.Cells**, **mengekspor data yang difilter ke CSV**, atau **menerapkan pemformatan bersyarat secara programatik**. Semua ini dibangun di atas model objek yang baru saja Anda kuasai.

Jangan ragu bereksperimen dengan banyak tabel, workbook besar, atau format file yang berbeda—keahlian baru Anda akan membuat otomatisasi Excel menjadi lebih lancar dan dapat diprediksi. Selamat coding!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Bersihkan UI filter di Excel dengan C# – Hapus Tombol AutoFilter](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [Cara Mengimplementasikan AutoFilter di Excel menggunakan Aspose.Cells for .NET (Panduan Analisis Data)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [Cara Mengimplementasikan Autofilter Excel 'EndsWith' Menggunakan Aspose.Cells for .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}