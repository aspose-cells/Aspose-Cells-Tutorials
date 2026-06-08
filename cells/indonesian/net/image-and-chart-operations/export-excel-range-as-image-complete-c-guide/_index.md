---
category: general
date: 2026-06-08
description: Ekspor rentang Excel sebagai gambar menggunakan C# dan Aspose.Cells.
  Pelajari cara menyimpan lembar kerja Excel sebagai gambar dalam beberapa langkah
  sederhana.
draft: false
keywords:
- export excel range as image
- save excel worksheet as image
- Aspose.Cells image export
- C# Excel automation
- pivot table to image
language: id
og_description: Ekspor rentang Excel sebagai gambar dengan C#. Tutorial ini menunjukkan
  cara menyimpan lembar kerja Excel sebagai gambar dengan cepat dan andal.
og_title: Ekspor Rentang Excel sebagai Gambar – Panduan Lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  headline: Export Excel Range as Image – Complete C# Guide
  type: TechArticle
- description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  name: Export Excel Range as Image – Complete C# Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - Aspose.Cells
      for .NET ≥ 23.9 (you can grab a free trial from the Aspose website). - A basic
      understanding of C# and file I/O.'
  - name: What the code does
    text: '- `exportRange.ToImage` captures only the cells inside the range (pivot
      table or custom block). - `worksheet.ToImage` captures the *entire* visible
      area of the worksheet, effectively **save excel worksheet as image**.'
  - name: Multiple Pivot Tables
    text: 'If your workbook contains more than one pivot table, you can loop through
      them:'
  - name: Very Large Ranges
    text: 'Exporting a massive range (e.g., thousands of rows) can consume a lot of
      memory. Mitigate this by:'
  - name: Transparent Backgrounds
    text: 'If you need a transparent background (useful for overlaying on web pages),
      set the background color to `Color.Transparent` before export:'
  - name: File Permissions
    text: Make sure the target directory exists and your process has write permission.
      Otherwise `ToImage` throws an `IOException`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- ImageExport
title: Ekspor Rentang Excel sebagai Gambar – Panduan Lengkap C#
url: /id/net/image-and-chart-operations/export-excel-range-as-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor Rentang Excel sebagai Gambar – Panduan Lengkap C#

Pernah perlu **mengekspor rentang Excel sebagai gambar** tetapi tidak yakin panggilan API mana yang harus digunakan? Anda tidak sendirian. Baik Anda sedang membangun dasbor pelaporan atau membutuhkan snapshot tabel pivot untuk slide PowerPoint, mengubah blok sel menjadi PNG adalah trik yang berguna.

Dalam panduan ini kami akan membahas contoh mandiri yang tidak hanya **mengekspor rentang Excel sebagai gambar** tetapi juga menunjukkan cara **menyimpan lembar kerja Excel sebagai gambar** untuk seluruh sheet. Tanpa skrip eksternal, hanya C# murni dan Aspose.Cells, sehingga Anda dapat menyalin‑tempel kode dan melihatnya bekerja secara instan.

## Apa yang Akan Anda Pelajari

- Memuat workbook yang ada dan menemukan rentang tertentu (tabel pivot atau blok sel apa pun).  
- Mengonfigurasi opsi ekspor gambar seperti format, resolusi, dan skala.  
- Mengekspor satu rentang ke PNG, JPEG, atau BMP.  
- Memperluas logika yang sama untuk **menyimpan lembar kerja Excel sebagai gambar** dalam satu baris.  
- Tips untuk menangani banyak tabel pivot, rentang besar, dan jebakan umum.

### Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga bekerja pada .NET Framework 4.7+).  
- Aspose.Cells untuk .NET ≥ 23.9 (Anda dapat mengambil trial gratis dari situs web Aspose).  
- Pemahaman dasar tentang C# dan I/O file.  

Jika Anda sudah memiliki semua itu, mari kita mulai.

## Langkah 1: Siapkan Proyek dan Impor Namespace

Pertama, buat aplikasi console baru (atau integrasikan kode ke dalam proyek yang sudah ada). Tambahkan paket NuGet Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

Kemudian bawa namespace yang diperlukan ke dalam ruang lingkup:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // For ImageOrPrintOptions
using System.Drawing.Imaging; // For ImageFormat enum
```

> **Pro tip:** Letakkan pernyataan `using` Anda di bagian atas file; ini membuat kode lebih mudah dipindai—terutama ketika Anda menambahkan lebih banyak fitur Aspose nanti.

## Langkah 2: Muat Workbook yang Memuat Rentang Target

Anda memerlukan workbook di disk. Ganti `YOUR_DIRECTORY/input.xlsx` dengan jalur sebenarnya ke file Anda.

```csharp
// Step 2: Load the workbook containing the data you want to capture
Workbook workbook = new Workbook(@"YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – make sure the file loaded correctly
if (workbook == null)
{
    Console.WriteLine("Failed to load workbook. Check the file path.");
    return;
}
```

Mengapa langkah ini penting: objek `Workbook` adalah titik masuk untuk setiap operasi Aspose.Cells. Tanpa itu Anda tidak dapat merujuk ke lembar kerja, rentang, atau tabel pivot.

## Langkah 3: Identifikasi Rentang yang Akan Diekspor

Anda memiliki dua skenario umum:

1. **Tabel pivot tertentu** – kode yang Anda posting menggunakan `PivotTables[0].PivotTableRange`.  
2. **Blok sel arbitrer** – Anda dapat menggunakan `worksheet.Cells.CreateRange("B2:D10")`.

Di bawah ini kami menangani keduanya, sehingga Anda dapat memilih yang paling sesuai dengan kasus Anda.

```csharp
// Step 3a: Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Option A: Export the first pivot table's range
Range exportRange;
if (worksheet.PivotTables.Count > 0)
{
    exportRange = worksheet.PivotTables[0].PivotTableRange;
}
else
{
    // Option B: Fallback to a manual range (e.g., B2:D10)
    exportRange = worksheet.Cells.CreateRange("B2:D10");
}
```

> **Mengapa kami memeriksa tabel pivot terlebih dahulu:** Banyak file pelaporan mengandalkan data pivot dinamis. Jika tidak ada, fallback memastikan tutorial tetap berfungsi.

## Langkah 4: Konfigurasikan Opsi Ekspor Gambar

Aspose.Cells memberi Anda kontrol detail atas gambar output. Pengaturan paling umum adalah format, resolusi (DPI), dan apakah menyertakan garis kisi.

```csharp
// Step 4: Set up image export options
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG works well for lossless quality
    HorizontalResolution = 300,      // 300 DPI for crisp prints
    VerticalResolution = 300,
    // Optional: uncomment to hide gridlines
    // IsGridlinesVisible = false
};
```

Anda dapat mengganti ke `ImageFormat.Jpeg` atau `ImageFormat.Bmp` jika sistem downstream Anda lebih menyukai tipe tersebut. Pengaturan DPI penting ketika Anda menyematkan gambar dalam PDF beresolusi tinggi atau deck slide.

## Langkah 5: Ekspor Rentang (atau Seluruh Lembar Kerja) sebagai Gambar

Sekarang keajaiban terjadi. Metode `ToImage` menulis representasi visual dari rentang langsung ke disk.

```csharp
// Step 5a: Export the selected range to an image file
string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
exportRange.ToImage(rangeImagePath, imgOptions);
Console.WriteLine($"Range exported to: {rangeImagePath}");

// Step 5b: If you need to **save excel worksheet as image**, use the worksheet's ToImage overload
string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";
worksheet.ToImage(sheetImagePath, imgOptions);
Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
```

### Apa yang Dilakukan Kode Ini

- `exportRange.ToImage` menangkap hanya sel‑sel di dalam rentang (tabel pivot atau blok khusus).  
- `worksheet.ToImage` menangkap *seluruh* area yang terlihat pada lembar kerja, secara efektif **menyimpan lembar kerja Excel sebagai gambar**.  

Kedua pemanggilan menghormati opsi yang Anda tetapkan sebelumnya—sehingga Anda akan mendapatkan file PNG dengan resolusi 300 DPI.

## Menangani Kasus Tepi & Pertanyaan Umum

### Banyak Tabel Pivot

Jika workbook Anda berisi lebih dari satu tabel pivot, Anda dapat melakukan loop melalui mereka:

```csharp
for (int i = 0; i < worksheet.PivotTables.Count; i++)
{
    Range ptRange = worksheet.PivotTables[i].PivotTableRange;
    string outPath = $@"YOUR_DIRECTORY/Pivot_{i}.png";
    ptRange.ToImage(outPath, imgOptions);
    Console.WriteLine($"Pivot {i} saved to {outPath}");
}
```

### Rentang Sangat Besar

Mengekspor rentang yang sangat besar (misalnya ribuan baris) dapat mengonsumsi banyak memori. Kurangi hal ini dengan:

- Mengurangi `HorizontalResolution` / `VerticalResolution`.  
- Mengekspor dalam bagian‑bagian (bagi rentang menjadi blok‑blok yang lebih kecil).  

### Latar Belakang Transparan

Jika Anda memerlukan latar belakang transparan (berguna untuk overlay pada halaman web), atur warna latar belakang ke `Color.Transparent` sebelum mengekspor:

```csharp
imgOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### Izin File

Pastikan direktori target ada dan proses Anda memiliki izin menulis. Jika tidak, `ToImage` akan melempar `IOException`.

## Contoh Lengkap yang Siap Jalan

Menggabungkan semuanya, berikut program console yang siap dijalankan:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing.Imaging;

namespace ExcelImageExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths for your environment
            string inputPath = @"YOUR_DIRECTORY/input.xlsx";
            string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
            string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";

            // Load workbook
            Workbook workbook = new Workbook(inputPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // Determine which range to export
            Range exportRange;
            if (worksheet.PivotTables.Count > 0)
            {
                exportRange = worksheet.PivotTables[0].PivotTableRange;
            }
            else
            {
                exportRange = worksheet.Cells.CreateRange("B2:D10");
            }

            // Configure image options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // Export range as image
            exportRange.ToImage(rangeImagePath, imgOptions);
            Console.WriteLine($"Range exported to: {rangeImagePath}");

            // Export entire worksheet as image
            worksheet.ToImage(sheetImagePath, imgOptions);
            Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
        }
    }
}
```

**Output yang diharapkan** (console):

```
Range exported to: YOUR_DIRECTORY/PivotRange.png
Worksheet exported to: YOUR_DIRECTORY/FullSheet.png
```

Buka file PNG yang dihasilkan dan Anda akan melihat snapshot pixel‑perfect dari rentang yang dipilih dan seluruh sheet, masing‑masing.

## Kesimpulan

Kami baru saja membahas semua yang Anda perlukan untuk **mengekspor rentang Excel sebagai gambar** serta cara **menyimpan lembar kerja Excel sebagai gambar** menggunakan Aspose.Cells dan C#. Dari memuat workbook hingga menyetel opsi gambar dan menangani banyak pivot, langkah‑langkahnya sederhana dan dapat direproduksi sepenuhnya.

Selanjutnya, Anda mungkin ingin:

- Bereksperimen dengan nilai `ImageFormat` yang berbeda (JPEG, BMP).  
- Menggabungkan gambar dengan PDF menggunakan kelas `Document` untuk pembuatan laporan.  
- Mengotomatiskan proses untuk sekumpulan file dalam sebuah folder.

Silakan sesuaikan potongan kode dengan alur kerja Anda—apakah Anda mengirim gambar ke API web, menyematkannya dalam email, atau menghasilkan laporan yang dapat dicetak. Selamat coding, dan biarkan gambar berbicara untuk data Excel Anda!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekspor Sel Excel ke Gambar Menggunakan Aspose.Cells .NET: Panduan Langkah demi Langkah](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Ekspor Workbook Excel sebagai Gambar Menggunakan Aspose.Cells untuk Java: Panduan Langkah demi Langkah](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Ekspor Workbook Excel sebagai Gambar Menggunakan Aspose Cells untuk Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}