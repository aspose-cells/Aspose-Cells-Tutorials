---
category: general
date: 2026-10-10
description: Konversi Excel ke PowerPoint dan atur area cetak di C# dengan Aspose.Cells
  – pelajari cara mengekspor Excel, mengatur area cetak, dan menghasilkan file PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: id
lastmod: 2026-10-10
og_description: Konversi Excel ke PowerPoint dengan Aspose.Cells. Tutorial ini menunjukkan
  cara mengatur area cetak, mengekspor Excel, dan membuat file PPTX dalam C#.
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: Konversi Excel ke PowerPoint – panduan lengkap untuk pengembang C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Ubah Excel ke PowerPoint dan atur area cetak
url: /id/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengonversi Excel ke PowerPoint dan mengatur area cetak

Jika Anda perlu **convert Excel to PowerPoint**, panduan ini menunjukkan secara tepat cara melakukannya di C#. Dengan mendefinisikan area cetak terlebih dahulu, Anda mengontrol sel mana yang muncul di setiap slide, dan file PPTX akhir sesuai dengan harapan tata letak Anda. Solusi ini juga menjawab “how to export Excel” dan “how to set print area” menggunakan basis kode yang sama.

Dalam tutorial ini Anda akan:

* Muat workbook yang sudah ada.
* Atur area cetak untuk sebuah worksheet (langkah **set print area excel**).
* Konfigurasikan opsi konversi untuk output PowerPoint.
* Hasilkan file **convert excel to pptx** dalam satu pemanggilan metode.

Semua kode yang diperlukan sudah disertakan, sehingga Anda dapat menyalin, menempel, dan menjalankannya segera.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

| Persyaratan | Mengapa penting |
|-------------|----------------|
| **.NET 6.0 atau lebih baru** | Contoh ini menargetkan .NET 6+, tetapi versi .NET apa pun yang mendukung C# 10 dapat digunakan. |
| **Aspose.Cells for .NET** | Pustaka ini menyediakan `Workbook`, `ImageOrPrintOptions`, dan metode `ConvertToPdf` (digunakan untuk PPTX). Instal melalui NuGet: `dotnet add package Aspose.Cells` |
| **File Excel input** | Tutorial ini menggunakan `input.xlsx`. Letakkan di folder yang dapat Anda referensikan dari kode. |
| **Izin menulis ke folder output** | Program menulis `output.pptx`. Pastikan direktori ada dan dapat ditulisi. |

> **Tips Pro:** Jika Anda bekerja dengan beberapa worksheet, ulangi langkah area cetak untuk setiap sheet sebelum konversi.

## Langkah 1: Buat proyek konsol C# baru

Buka terminal atau jendela PowerShell dan jalankan:

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

Ini membuat proyek baru bernama **ExcelToPowerPointDemo** dan menambahkan paket Aspose.Cells, yang merupakan dependensi inti untuk **how to export Excel** ke format lain.

## Langkah 2: Tulis kode konversi

Ganti isi `Program.cs` dengan contoh lengkap di bawah ini. Kode tersebut mendemonstrasikan **convert excel to powerpoint**, menunjukkan **how to set print area**, dan menghasilkan file **convert excel to pptx**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### Mengapa setiap bagian penting

* **Memuat workbook** – Ini adalah langkah pertama dalam skenario **how to export Excel** apa pun. `Workbook` membaca file ke memori, memberi Anda akses penuh ke sheet, sel, dan format.
* **Mengatur area cetak** – Dengan menetapkan `PageSetup.PrintArea`, Anda memberi tahu Aspose.Cells sel mana yang akan dirender. Ini adalah inti dari **set print area excel**; tanpa itu, seluruh sheet akan diekspor, yang berpotensi menghasilkan slide yang sangat besar dan tidak dapat dibaca.
* **Memilih `SaveFormat.Pptx`** – Objek `ImageOrPrintOptions` memungkinkan Anda mengubah format output. Menetapkan `SaveFormat` ke `Pptx` memicu pipeline **convert excel to pptx**.
* **Memanggil `ConvertToPdf`** – Meskipun nama metodenya, ketika `SaveFormat` adalah `Pptx` pustaka menghasilkan file PowerPoint. Ini adalah cara yang direkomendasikan untuk **convert excel to powerpoint** dalam satu panggilan.

## Langkah 3: Jalankan program

Dari folder proyek, jalankan:

```bash
dotnet run
```

Jika semuanya dikonfigurasi dengan benar, Anda akan melihat output konsol yang mirip dengan:

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

Buka `output.pptx` di Microsoft PowerPoint atau penampil kompatibel lainnya. Setiap slide sesuai dengan halaman yang dicetak dari worksheet, dibatasi pada rentang yang Anda tentukan.

## Menangani beberapa worksheet

Jika workbook Anda berisi lebih dari satu sheet dan Anda menginginkan setiap sheet pada deck slide terpisah, lakukan loop melalui koleksi:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

Pola ini menunjukkan **how to export Excel** data sheet‑by‑sheet sambil tetap **setting print area** secara individual.

## Kasus tepi dan tips praktik terbaik

| Situasi | Pendekatan yang disarankan |
|-----------|----------------------|
| **Worksheet sangat besar** | Kurangi area cetak atau tingkatkan `HorizontalResolution`/`VerticalResolution` untuk menjaga ukuran PPTX tetap dapat dikelola. |
| **Orientasi halaman yang berbeda** | Setel `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` sebelum konversi. |
| **Ukuran slide khusus** | Gunakan `conversionOptions.OnePagePerSheet = false;` dan sesuaikan `conversionOptions.Width` / `conversionOptions.Height`. |
| **File input tidak ada** | Bungkus kode pemuatan dalam blok `try { … } catch (FileNotFoundException)` untuk memberikan pesan error yang jelas. |
| **Karakter non‑ASCII** | Pastikan workbook disimpan dengan encoding UTF‑8; Aspose.Cells menangani Unicode secara otomatis. |

## Kode sumber lengkap untuk referensi

Berikut adalah seluruh program, termasuk direktif `using` dan komentar. Simpan sebagai `Program.cs` di dalam proyek yang dibuat pada **Langkah 1**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## Output yang diharapkan

Menjalankan program menghasilkan file PowerPoint (`output.pptx`) yang berisi:

* Satu slide per halaman yang dicetak dari worksheet.
* Hanya sel dalam rentang **A1:G30** yang terlihat pada setiap slide.
* Pemformatan yang dipertahankan (font, warna, border) sebagaimana muncul di Excel.

Buka file di PowerPoint untuk memverifikasi bahwa tata letak sesuai dengan area cetak yang telah ditentukan.

## Kesimpulan

Anda sekarang tahu cara **convert Excel to PowerPoint** sambil secara tepat **set print area excel** menggunakan Aspose.Cells di C#. Tutorial ini mencakup **how to export Excel**, mendemonstrasikan **how to set print area**, dan menampilkan **convert excel to pptx** secara lengkap.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Mengatur Area Cetak di Excel Menggunakan Aspose.Cells untuk .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Atur Area Cetak di Excel dan Ekspor ke PowerPoint – Panduan Langkah‑per‑Langkah](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Atur Area Cetak Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}