---
category: general
date: 2026-03-22
description: Tetapkan area cetak di Excel dan konversi Excel ke PowerPoint dengan
  bentuk yang dapat diedit. Pelajari cara mengulang baris judul, membuat PowerPoint
  dari Excel, dan mengekspor Excel ke PPTX.
draft: false
keywords:
- set print area
- convert excel to powerpoint
- repeat title row
- create powerpoint from excel
- export excel to pptx
language: id
og_description: Atur area cetak di Excel dan konversi menjadi slide PowerPoint dengan
  bentuk yang dapat diedit. Ikuti panduan lengkap ini untuk mengulang baris judul
  dan mengekspor Excel ke pptx.
og_title: Atur Area Cetak di Excel – Tutorial Ekspor ke PowerPoint
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint generation
title: Atur Area Cetak di Excel dan Ekspor ke PowerPoint – Panduan Langkah demi Langkah
url: /id/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Atur Area Cetak di Excel dan Ekspor ke PowerPoint – Tutorial Pemrograman Lengkap

Pernahkah Anda perlu **set print area** di lembar kerja Excel dan kemudian mengubah bagian itu menjadi slide PowerPoint? Anda tidak sendirian. Dalam banyak alur pelaporan, data yang dicetak dengan rapi juga harus muncul dalam presentasi, seringkali dengan baris pertama diulang sebagai judul. Kabar baik? Dengan beberapa baris C# Anda dapat **convert excel to powerpoint**, menjaga semua kotak teks dapat diedit, dan bahkan **repeat title row** secara otomatis.

Dalam panduan ini kami akan membahas semua yang perlu Anda ketahui: mulai dari mengonfigurasi area cetak hingga membuat file PPTX yang dapat Anda edit langsung di PowerPoint. Pada akhir tutorial Anda akan dapat **create powerpoint from excel**, mengekspor hasilnya sebagai **export excel to pptx**, dan menggunakan kembali kode yang sama di proyek .NET mana pun. Tanpa sulap, hanya langkah‑langkah jelas dan contoh lengkap yang dapat dijalankan.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki:

- **.NET 6.0** atau lebih baru (API ini juga berfungsi dengan .NET Framework)
- **Aspose.Cells for .NET** (perpustakaan yang menyediakan `Workbook`, `ImageOrPrintOptions`, dll.)
- IDE C# dasar (Visual Studio, Rider, atau VS Code dengan ekstensi C#)
- File Excel (`input.xlsx`) yang berisi data yang ingin Anda ekspor

Itu saja—tidak ada paket NuGet tambahan selain Aspose.Cells. Jika Anda belum menambahkan perpustakaan tersebut, jalankan:

```bash
dotnet add package Aspose.Cells
```

Sekarang kita siap meluncur.

## Langkah 1: Muat Workbook – Titik Awal untuk Ekspor

Hal pertama yang harus Anda lakukan adalah memuat workbook yang berisi sheet yang ingin Anda ubah menjadi slide. Anggap workbook sebagai dokumen sumber; tanpa itu tidak ada yang penting.

```csharp
using Aspose.Cells;

// Load the workbook that contains the shapes and data
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

**Mengapa ini penting:** Memuat workbook memberi Anda akses ke koleksi worksheet, opsi pengaturan halaman, dan mesin ekspor. Jika Anda melewatkan langkah ini, Anda tidak akan dapat mengatur **print area** atau mengulang baris apa pun.

> **Pro tip:** Gunakan path absolut saat pengujian, lalu beralih ke path relatif atau path berbasis konfigurasi untuk produksi.

## Langkah 2: Konfigurasikan Opsi Ekspor – Jaga Kotak Teks dan Bentuk Dapat Diedit

Saat Anda mengekspor ke PowerPoint, biasanya Anda ingin slide yang dihasilkan dapat diedit. Aspose.Cells memungkinkan Anda mengontrol hal ini dengan `ImageOrPrintOptions`. Menetapkan `ExportTextBoxes` dan `ExportShapeObjects` ke `true` memberi tahu perpustakaan untuk mempertahankan objek‑objek tersebut sebagai elemen PowerPoint asli, bukan mengubahnya menjadi gambar.

```csharp
// Configure export options for a PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // The target format – crucial for PowerPoint
    ExportTextBoxes = true,            // Keep text boxes editable
    ExportShapeObjects = true          // Keep shape objects editable
};
```

**Mengapa ini penting:** Jika Anda pernah perlu **convert excel to powerpoint** dan kemudian menyempurnakan slide secara manual, pengaturan ini menyelamatkan Anda dari harus membuat ulang kotak teks dari awal. Ini juga memastikan semua bentuk (seperti panah atau diagram) tetap sebagai objek vektor yang dapat Anda ubah ukurannya.

## Langkah 3: Atur Area Cetak dan Ulangi Baris Judul

Sekarang kita sampai pada inti tutorial: **set print area** dan membuat baris pertama diulang pada setiap halaman yang dicetak (atau, dalam kasus kita, pada slide yang diekspor). Area cetak memberi tahu Excel sel‑sel mana yang akan dipertimbangkan untuk pencetakan—atau dalam skenario ini, untuk ekspor.

```csharp
// Define the area of the sheet to export (A1:G20)
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G20";

// Repeat the first row as a title on each printed page
sheet.PageSetup.PrintTitleRows = "$1:$1";
```

**Mengapa ini penting:** Dengan membatasi ekspor ke `A1:G20` Anda menghindari penarikan rentang kosong yang sangat besar, yang mempercepat konversi dan membuat slide tetap rapi. Baris `PrintTitleRows` membuat baris pertama berperan sebagai header—tepat apa yang Anda inginkan ketika **repeat title row** dalam presentasi.

> **Edge case:** Jika data Anda dimulai pada baris 2, sesuaikan rentangnya (misalnya, `PrintTitleRows = "$2:$2"`).

## Langkah 4: Simpan Worksheet sebagai File PowerPoint

Akhirnya, kami menulis slide ke disk. Metode `Save` menerima nama file target dan opsi yang telah kami konfigurasikan sebelumnya. Hasilnya adalah file PPTX dengan kotak teks dan bentuk yang dapat diedit, siap dibuka di PowerPoint.

```csharp
// Save the selected sheet as a PPTX file using the configured options
string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
workbook.Save(outputPath, exportOptions);
```

**Apa yang akan Anda lihat:** Buka `SheetWithEditableShapes.pptx` di PowerPoint. Baris pertama muncul sebagai judul, semua sel dari `A1:G20` dirender, dan semua bentuk yang Anda tambahkan di Excel tetap dapat dipindahkan dan diedit. Tidak ada gambar raster—hanya objek PowerPoint asli.

## Contoh Kerja Penuh – Semua Langkah Digabungkan

Berikut adalah program lengkap yang siap disalin‑tempel. Jalankan sebagai aplikasi konsol atau sematkan dalam solusi yang lebih besar.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the workbook
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Set export options for editable PPTX
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportTextBoxes = true,
                ExportShapeObjects = true
            };

            // Step 3: Define print area and repeat title row
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G20";
            sheet.PageSetup.PrintTitleRows = "$1:$1";

            // Step 4: Save as PowerPoint
            string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
            workbook.Save(outputPath, exportOptions);

            Console.WriteLine($"Successfully exported to {outputPath}");
        }
    }
}
```

**Output yang diharapkan:** Setelah menjalankan program, konsol menampilkan pesan keberhasilan, dan file PPTX muncul di lokasi yang ditentukan. Membuka file tersebut menampilkan satu slide dengan rentang yang dipilih, kotak teks yang dapat diedit, dan semua bentuk asli.

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

| Question | Answer |
|----------|--------|
| **Does this work with multiple worksheets?** | Ya. Loop melalui `workbook.Worksheets` dan ulangi langkah yang sama untuk setiap sheet, ubah nama file output setiap kali. |
| **What if I need to export more than one slide?** | Panggil `workbook.Save` beberapa kali dengan objek `ImageOrPrintOptions` yang berbeda, masing‑masing dikonfigurasikan dengan `PageSetup` yang berbeda bila diperlukan. |
| **Can I change the slide size?** | Gunakan `exportOptions.ImageFormat` untuk mengatur DPI, atau sesuaikan `sheet.PageSetup.PaperSize` sebelum menyimpan. |
| **Is Aspose.Cells free?** | Ia menawarkan evaluasi gratis dengan watermark. Untuk produksi, lisensi diperlukan. |
| **What about Excel formulas?** | Nilai yang diekspor adalah **calculated results** pada saat ekspor. Jika Anda memerlukan formula hidup di PowerPoint, Anda memerlukan pendekatan lain. |

## Tips untuk Alur Kerja yang Lancar

- **Pro tip:** Set `Workbook.Settings.CalcMode = CalculationModeType.Automatic` sebelum ekspor untuk menjamin semua formula terbaru.
- **Watch out for:** Rentang yang sangat besar dapat menyebabkan tekanan memori. Potong area cetak ke rentang terkecil yang diperlukan.
- **Performance tip:** Gunakan satu instance `ImageOrPrintOptions` jika Anda mengekspor banyak sheet; membuat instance baru setiap kali menambah beban.
- **Version note:** Kode di atas menargetkan Aspose.Cells 23.10 (dirilis November 2023). Versi selanjutnya tetap menggunakan API yang sama, tetapi selalu periksa catatan rilis untuk perubahan yang dapat memengaruhi.

## Kesimpulan

Kami telah membahas cara **set print area** di worksheet Excel, mengulang baris pertama sebagai judul, dan kemudian **export excel to pptx** sambil mempertahankan kotak teks serta bentuk yang dapat diedit. Singkatnya, Anda kini mengetahui cara andal untuk **convert excel to powerpoint**, **repeat title row**, dan **create powerpoint from excel** hanya dengan beberapa baris C#.

Siap untuk langkah berikutnya? Cobalah mengotomatisasi konversi batch puluhan laporan, atau tambahkan tata letak slide khusus menggunakan PowerPoint SDK setelah ekspor. Langit adalah batasnya—bereksperimen, pecahkan masalah, dan nikmati kekuatan pembuatan dokumen secara programatik.

Jika tutorial ini berguna bagi Anda, bagikan, tinggalkan komentar dengan modifikasi Anda, atau jelajahi panduan lain kami tentang **export excel to pptx** dan topik otomasi terkait. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}