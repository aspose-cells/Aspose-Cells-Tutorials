---
category: general
date: 2026-11-19
description: Pelajari cara menyalin rentang menggunakan CopyOptions di Aspose.Cells,
  mempertahankan pemformatan dan tabel pivot saat menyalin rentang Excel dengan pemformatan.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: id
lastmod: 2026-11-19
og_description: Menyalin rentang menggunakan CopyOptions di Aspose.Cells memungkinkan
  Anda menggandakan data Excel dengan format lengkap dan tabel pivot yang dipertahankan,
  sehingga manipulasi workbook menjadi andal.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Salin rentang menggunakan CopyOptions di Aspose.Cells – panduan langkah
  demi langkah
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cara menyalin rentang menggunakan CopyOptions di Aspose.Cells
url: /id/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin rentang menggunakan CopyOptions di Aspose.Cells

Jika Anda perlu **copy range using CopyOptions** di Aspose.Cells, panduan ini menunjukkan secara tepat cara menduplikasi blok sel sambil mempertahankan semua pemformatan dan tabel pivot yang tertanam. Banyak pengembang mengalami kesulitan dalam mempertahankan gaya saat memindahkan data antar lembar kerja, dan kelas `CopyOptions` menyelesaikan masalah tersebut tanpa langkah manual tambahan.

Di tutorial ini Anda akan belajar untuk:

* Menentukan area sumber dan tujuan dalam sebuah workbook Excel.  
* Menggunakan `CopyOptions` untuk mempertahankan pemformatan sel, lebar kolom, dan tabel pivot.  
* Menyimpan hasil ke file baru yang siap untuk pemrosesan lanjutan.

Contoh ini bekerja dengan file `.xlsx` apa pun dan hanya memerlukan pustaka Aspose.Cells untuk .NET.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* .NET 6.0 atau yang lebih baru terpasang.  
* Lisensi Aspose.Cells untuk .NET yang valid (atau kunci evaluasi gratis).  
* Visual Studio 2022 atau IDE C# apa pun yang Anda sukai.  

Tidak ada paket NuGet tambahan yang diperlukan selain `Aspose.Cells`.

## Langkah 1: Siapkan proyek dan impor namespace

Buat aplikasi konsol baru dan tambahkan referensi Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

Direktif `using Aspose.Cells;` memberi Anda akses ke `Workbook`, `CellArea`, dan `CopyOptions`.

## Langkah 2: Muat workbook yang ingin Anda modifikasi

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` mewakili seluruh file Excel. Ganti `YOUR_DIRECTORY` dengan folder yang berisi file sumber Anda.

## Langkah 3: Tentukan rentang sumber dan tujuan

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` membangun area persegi panjang berdasarkan alamat sel kiri‑atas dan kanan‑bawah. Anda dapat menyesuaikan koordinat untuk mencocokkan ukuran blok yang ingin disalin.

## Langkah 4: Salin rentang sambil mempertahankan pemformatan dan tabel pivot

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

Objek `CopyOptions` memberi tahu Aspose.Cells secara tepat apa yang harus dipertahankan. Menetapkan `CopyPivotTables = true` adalah kunci untuk **copy range using CopyOptions** ketika sumber Anda mencakup tabel pivot. Flag lainnya memastikan bahwa **copy excel range with formatting** tercapai secara otomatis—tidak ada kode tambahan yang diperlukan untuk menerapkan kembali gaya setelah penyalinan.

### Mengapa `CopyOptions` penting

* **Performance** – Perpustakaan melakukan satu operasi internal tunggal alih-alih menyalin sel satu‑per‑satu.  
* **Accuracy** – Semua aspek visual (font, warna, batas) tetap ada setelah pemindahan, yang menghilangkan pergeseran visual dalam laporan yang dihasilkan.  
* **Reliability** – Tabel pivot tetap berfungsi karena cache dan referensi sumbernya diduplikasi.

## Langkah 5: Simpan workbook yang telah dimodifikasi

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

Setelah memanggil `Save`, file `output.xlsx` berisi data asli ditambah blok yang diduplikasi di lokasi tujuan, lengkap dengan pemformatan dan tabel pivot.

## Kode sumber lengkap untuk referensi

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

Running this program prints:

```
Range copied successfully. Output saved to output.xlsx
```

Buka `output.xlsx` di Excel – Anda akan melihat blok A1:H30 diduplikasi ke A35:H64, dengan semua warna sel, batas, format angka, dan semua tabel pivot tetap utuh.

## Pertanyaan umum dan penanganan kasus tepi

### Bagaimana jika area tujuan tumpang tindih dengan sumber?

Aspose.Cells akan melempar `ArgumentException`. Untuk menghindarinya, hitung tujuan yang tidak berpotongan dengan sumber, atau salin ke lembar kerja yang berbeda:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### Cara menyalin antar workbook yang berbeda?

Buat instance `Workbook` kedua untuk file target dan gunakan objek `CopyOptions` yang sama:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### Apakah `CopyOptions` juga menyalin sel yang digabungkan?

Ya. Flag `CopyStyle` mencakup informasi sel yang digabungkan. Jika Anda memerlukan kontrol yang lebih halus, setel `options.CopyMergedCells = true` (tersedia di versi terbaru).

### Bagaimana dengan rentang besar (ribuan baris)?

Operasi ini efisien memori, tetapi Anda mungkin ingin meningkatkan `WorkbookSettings` `MemorySetting` menjadi `MemorySetting.MemoryPreference` untuk file yang sangat besar.

## Tips profesional

* **Gunakan kembali instance `CopyOptions` yang sama** untuk beberapa operasi penyalinan – ini mengurangi beban alokasi objek.  
* **Validasi rentang** sebelum menyalin: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` membantu menangkap kesalahan ketik lebih awal.  
* **Matikan perhitungan** (`workbook.Settings.CalcMode = CalculationMode.Manual`) saat menyalin kumpulan data besar untuk mempercepat proses, kemudian panggil `workbook.CalculateFormula()` setelah penyalinan jika Anda memerlukan hasil yang diperbarui.

## Kesimpulan

Anda sekarang tahu cara **copy range using CopyOptions** di Aspose.Cells, mencapai **copy excel range with formatting** secara lengkap sambil mempertahankan tabel pivot dan fitur lanjutan lainnya. Pendekatan ini menghilangkan penerapan ulang gaya secara manual dan memastikan otomatisasi Excel Anda tetap kuat dan dapat dipelihara.

Langkah selanjutnya yang dapat Anda jelajahi:

* Gunakan `CopyOptions` untuk menduplikasi seluruh lembar kerja.  
* Gabungkan operasi penyalinan dengan `WorksheetCollection.AddCopy` untuk pembuatan laporan berbasis templat.  
* Integrasikan kode ke dalam API ASP.NET Core untuk menyediakan transformasi Excel secara real‑time.

Silakan bereksperimen dengan koordinat sumber/tujuan yang berbeda, dan bagikan hasil Anda di komentar!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}