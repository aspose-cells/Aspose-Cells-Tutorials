---
category: general
date: 2026-10-10
description: Konversi Excel ke PNG dengan cepat menggunakan Aspose.Cells di C#. Pelajari
  cara mengekspor rentang Excel, menyimpan Excel sebagai PNG, dan mengubah lembar
  kerja menjadi gambar dalam hitungan menit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to png
- export excel range
- save excel as png
- how to export excel
- convert worksheet to image
language: id
lastmod: 2026-10-10
og_description: konversi excel ke png secara instan dengan Aspose.Cells. tutorial
  ini menunjukkan cara mengekspor rentang excel, menyimpan excel sebagai png, dan
  mengonversi lembar kerja menjadi gambar.
og_image_alt: Screenshot of C# code that converts an Excel worksheet to a PNG image
og_title: Mengonversi Excel ke PNG dengan C# – panduan pemrograman lengkap
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: convert excel to png quickly using Aspose.Cells in C#. Learn to export
    excel range, save excel as png, and convert worksheet to image in minutes.
  headline: How to convert Excel to PNG with C# – step‑by‑step guide
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Image export
- Automation
title: Cara mengonversi Excel ke PNG dengan C# – panduan langkah demi langkah
url: /id/net/converting-excel-files-to-other-formats/how-to-convert-excel-to-png-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengonversi Excel ke PNG dengan C# – panduan langkah demi langkah

Jika Anda perlu **convert Excel to PNG** secara programatis, panduan ini menunjukkan secara tepat cara melakukannya menggunakan Aspose.Cells for .NET. Baik Anda sedang membangun layanan pelaporan atau dasbor otomatis, Anda akan belajar mengekspor rentang Excel, menyimpan hasilnya sebagai file PNG, dan menangani kasus tepi umum.

Anda akan melalui setiap langkah yang diperlukan—dari menambahkan paket NuGet hingga merender area lembar kerja tertentu—sehingga Anda dapat mengintegrasikan solusi ini ke dalam proyek C# apa pun tanpa harus mencari sumber tambahan.

## Prasyarat

* .NET 6.0 SDK atau yang lebih baru (kode juga berfungsi dengan .NET Framework 4.6+)
* Visual Studio 2022 (atau IDE apa pun yang mendukung C#)
* Lisensi Aspose.Cells for .NET yang valid (versi percobaan gratis dapat digunakan untuk evaluasi)
* File Excel bernama **Pivot.xlsx** yang berada di folder yang dapat Anda referensikan (tutorial menggunakan `YOUR_DIRECTORY` sebagai placeholder)

> **Tips pro:** Install paket Aspose.Cells melalui NuGet Package Manager Console:  
> `Install-Package Aspose.Cells`

## Mengonversi Excel ke PNG – penjelasan kode lengkap

Program lengkap berikut memuat workbook, mengonfigurasi opsi gambar, dan merender rentang sel yang ditentukan ke file PNG. Semua direktif `using` yang diperlukan sudah disertakan, sehingga Anda dapat menyalin kode ke dalam proyek konsol baru dan menjalankannya segera.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the workbook (convert excel to png starts here)
            // -------------------------------------------------
            string workbookPath = @"YOUR_DIRECTORY\Pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -------------------------------------------------
            // Step 2: Configure image options (PNG format)
            // -------------------------------------------------
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                // Export format – PNG ensures lossless quality
                ImageFormat = ImageFormat.Png,

                // Optional: set resolution (default is 96 DPI)
                // HorizontalResolution = 150,
                // VerticalResolution = 150
            };

            // -------------------------------------------------
            // Step 3: Define the range you want to export
            // -------------------------------------------------
            // Example range A1:H30 – you can change this to any valid Excel range
            string range = "A1:H30";

            // -------------------------------------------------
            // Step 4: Render the range to an image file
            // -------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\Pivot.png";
            workbook.Worksheets[0].RenderRangeToImage(range, outputPath, imgOptions);

            Console.WriteLine($"Excel range {range} has been exported to PNG at: {outputPath}");
        }
    }
}
```

### Cara kerja kode

* **Loading the workbook** – `Workbook` membaca file `.xlsx` ke memori, memberi Anda akses ke semua lembar kerja.
* **ImageOrPrintOptions** – Objek ini memberi tahu Aspose.Cells untuk menghasilkan PNG (`ImageFormat.Png`). Anda juga dapat menyesuaikan DPI, skala, atau warna latar belakang jika diperlukan.
* **RenderRangeToImage** – Metode `RenderRangeToImage` menerima tiga argumen: rentang sel (`"A1:H30"`), jalur file tujuan, dan opsi gambar. Ini adalah operasi inti yang **export excel range** ke gambar PNG.
* **Result** – Setelah dijalankan, Anda akan menemukan `Pivot.png` di folder yang ditentukan, berisi representasi visual yang tepat dari sel yang dipilih.

## Mengekspor rentang excel ke PNG – menyesuaikan output

Jika Anda perlu **export excel range** selain `A1:H30`, cukup ubah variabel `range`. Metode ini menerima alamat gaya Excel apa pun, termasuk rentang bernama:

```csharp
// Export a named range called "ReportArea"
string range = "ReportArea";
```

Anda juga dapat mengekspor seluruh lembar kerja dengan menggunakan "A1:Z1000" (atau alamat yang lebih besar) atau dengan memanggil `RenderToImage` tanpa parameter rentang.

## Menyimpan excel sebagai png dengan pengaturan tambahan

Terkadang Anda menginginkan PNG dengan resolusi tertentu untuk pencetakan atau penggunaan web. Sesuaikan `ImageOrPrintOptions` seperti berikut:

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    HorizontalResolution = 300,   // 300 DPI for high‑quality print
    VerticalResolution = 300,
    Transparent = true           // Makes the background transparent
};
```

Pengaturan ini menggambarkan cara **save excel as png** dengan DPI dan transparansi khusus, memberi Anda kontrol penuh atas kualitas gambar akhir.

## Cara mengekspor excel – menangani banyak lembar kerja

Contoh ini menargetkan lembar kerja pertama (`Worksheets[0]`). Untuk **convert worksheet to image** pada lembar lain, referensikan dengan indeks atau nama:

```csharp
// By index (second sheet)
Worksheet sheet = workbook.Worksheets[1];

// By name
Worksheet sheet = workbook.Worksheets["DataSheet"];
sheet.RenderRangeToImage(range, outputPath, imgOptions);
```

Memproses setiap lembar dalam loop sangat sederhana:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string sheetPath = $@"YOUR_DIRECTORY\Sheet{i + 1}.png";
    workbook.Worksheets[i].RenderRangeToImage(range, sheetPath, imgOptions);
    Console.WriteLine($"Sheet {i + 1} exported to {sheetPath}");
}
```

## Kasus tepi dan pemecahan masalah

| Situation | Recommended approach |
|-----------|----------------------|
| **Rentang sangat besar** (mis., seluruh workbook) | Tingkatkan `HorizontalResolution`/`VerticalResolution` secara bertahap untuk menghindari `OutOfMemoryException`. Pertimbangkan mengekspor setiap lembar secara terpisah. |
| **Sel yang digabung** | Aspose.Cells secara otomatis mempertahankan visual sel yang digabung, tetapi verifikasi output jika Anda bergantung pada lebar kolom yang tepat. |
| **Formula yang merujuk ke file eksternal** | Pastikan file tersebut dapat diakses sebelum memuat workbook; jika tidak, gambar yang dirender mungkin menampilkan nilai yang sudah usang. |
| **Lisensi tidak ada** | Versi percobaan menambahkan watermark. Terapkan lisensi yang valid (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`) sebelum merender untuk menghasilkan PNG bersih. |

## Contoh kerja lengkap

Berikut adalah program mandiri yang dapat Anda kompilasi dan jalankan. Ganti `YOUR_DIRECTORY` dengan jalur folder yang sebenarnya di mesin Anda.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main()
        {
            // Load workbook
            var workbook = new Workbook(@"C:\Temp\Pivot.xlsx");

            // Set PNG options
            var options = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 150,
                VerticalResolution = 150
            };

            // Define range and output file
            string range = "A1:H30";
            string output = @"C:\Temp\Pivot.png";

            // Export the range as a PNG image
            workbook.Worksheets[0].RenderRangeToImage(range, output, options);

            Console.WriteLine($"Successfully converted Excel to PNG: {output}");
        }
    }
}
```

**Output yang diharapkan**

```
Successfully converted Excel to PNG: C:\Temp\Pivot.png
```

Buka `Pivot.png` dengan penampil gambar apa pun—Anda akan melihat tata letak visual yang tepat dari sel A1 hingga H30, termasuk pemformatan, warna, dan batas.

## Kesimpulan

Anda kini memiliki metode yang handal untuk **convert Excel to PNG** menggunakan C#. Tutorial ini mencakup cara **export excel range**, **save excel as png**, dan **convert worksheet to image** dengan opsi yang dapat disesuaikan serta tips praktik terbaik.  

Dari sini Anda dapat:

* Mengintegrasikan kode ke dalam API web untuk menghasilkan gambar sesuai permintaan.  
* Menggabungkan output PNG dengan pembuatan PDF untuk laporan multi‑format.  
* Menjelajahi format gambar lain (`ImageFormat.Jpeg`, `ImageFormat.Bmp`) dengan menyesuaikan properti `ImageFormat`.

Silakan bereksperimen dengan rentang, resolusi, dan pilihan lembar kerja yang berbeda untuk menyesuaikan skenario otomatisasi spesifik Anda.

---

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode kerja lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengekspor Lembar Kerja Excel ke PNG Menggunakan Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Mengonversi Excel ke PNG, TIFF, dan PDF di Java menggunakan Aspose.Cells](/cells/english/java/workbook-operations/render-excel-as-png-tiff-pdf-aspose-cells-java/)
- [Menguasai Aspose.Cells Java: Mengonversi Excel ke PNG dengan Penyedia Stream Kustom](/cells/english/java/advanced-features/aspose-cells-java-custom-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}