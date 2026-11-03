---
category: general
date: 2026-09-27
description: Atur area cetak di Excel dan pelajari cara mengekspor gambar PNG dari
  sel yang dipilih. Panduan ini juga mencakup menyimpan rentang sebagai gambar dan
  menambahkan gambar ke lembar kerja.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: id
lastmod: 2026-09-27
og_description: Atur area cetak di Excel dan ekspor PNG dengan Aspose.Cells. Ikuti
  panduan langkah demi langkah ini untuk menyimpan rentang sebagai gambar dan menambahkan
  gambar ke lembar kerja.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Atur area cetak di Excel – ekspor PNG dalam C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Cara mengatur area cetak di Excel dan mengekspor PNG
url: /id/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengatur area cetak di Excel dan mengekspor PNG

Jika Anda perlu **set print area excel** sebelum membuat gambar, panduan ini menunjukkan secara tepat cara melakukannya. Anda juga akan belajar **how to export png** file dari rentang tertentu, **save range as image**, dan **add picture to worksheet** dalam satu alur kerja yang dapat diulang.

Bekerja dengan Excel secara programatik sering berarti Anda hanya menginginkan sebagian sel—misalnya tabel pivot atau diagram—menjadi gambar. Dengan mendefinisikan area cetak terlebih dahulu, Anda menjamin bahwa PNG yang diekspor berisi tepat sel yang Anda harapkan, tidak lebih dan tidak kurang. Tutorial ini memandu Anda melalui setiap langkah, mulai dari memuat workbook hingga menyimpan file PNG akhir, dan menjelaskan mengapa setiap pengaturan penting.

## Prasyarat

* .NET 6.0 atau yang lebih baru terinstal  
* Visual Studio 2022 (atau IDE C# apa pun)  
* Paket NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`)  
* File Excel (`input.xlsx`) yang berada di direktori yang diketahui  

Persyaratan ini memastikan kode berjalan tanpa konfigurasi tambahan.

## Langkah 1: Muat workbook yang ingin Anda kerjakan

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

Kelas `Workbook` mewakili seluruh file Excel. Memuatnya terlebih dahulu memberi Anda akses ke lembar kerja, sel, dan opsi pengaturan halaman.

## Langkah 2: **Set print area excel** untuk rentang target

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

Menetapkan **print area** memberi tahu Excel (dan Aspose.Cells) sel mana yang termasuk dalam halaman yang dapat dicetak. Ketika Anda kemudian mengekspor lembar sebagai gambar, hanya area ini yang dirender, yang penting untuk **export selected cells image** yang bersih.

## Langkah 3: Konfigurasikan opsi ekspor gambar – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` mengontrol format output. Dengan memilih `ImageFormat.Png`, Anda menjamin gambar beresolusi tinggi dengan latar belakang transparan yang bekerja baik di konteks web maupun desktop.

## Langkah 4: Buat gambar dari rentang yang ditentukan dan **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

Metode `Pictures.Add` menyisipkan gambar baru ke dalam lembar kerja. Dengan memberikan rentang yang dibuat pada Langkah 2, Anda **save range as image** langsung ke lembar, yang berguna jika Anda kemudian perlu merujuk gambar tersebut di bagian lain workbook.

## Langkah 5: **Save the picture as an image file** – menyelesaikan alur kerja **export selected cells image**

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

Memanggil `Save` menulis gambar ke sistem file menggunakan opsi yang didefinisikan pada Langkah 3. `selected_range.png` yang dihasilkan berisi tepat sel yang didefinisikan oleh perintah **set print area excel**.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua bagian memberikan Anda program ringkas yang dapat Anda masukkan ke dalam aplikasi konsol apa pun:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### Output yang diharapkan

Running the program prints:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

Dan Anda akan menemukan file `selected_range.png` yang hanya menampilkan sel A1 hingga G20 dari `input.xlsx`.

## Kesalahan umum dan cara menghindarinya

| Masalah | Mengapa terjadi | Solusi |
|---------|----------------|--------|
| Gambar yang diekspor berisi seluruh lembar | Tidak ada area cetak yang didefinisikan | Pastikan Anda **set print area excel** sebelum membuat gambar |
| PNG buram | DPI default terlalu rendah | Set `imageOptions.DpiX` dan `imageOptions.DpiY` ke nilai yang lebih tinggi (misalnya, 300) |
| Kesalahan file tidak ditemukan | Path direktori salah | Gunakan `Path.Combine` atau periksa kembali folder ada |
| Gambar muncul bergeser | Indeks baris/kolom tidak tepat | Dua parameter pertama `Pictures.Add` adalah sel kiri‑atas tempat gambar ditempatkan; pertahankan pada `0,0` untuk ekspor bersih |

## Tips profesional: Ekspor beberapa rentang dalam satu proses

Jika Anda perlu **export selected cells image** untuk beberapa area, ulangi Langkah 2‑5 di dalam loop, mengubah `printArea` setiap iterasi. Ingat untuk memberi setiap gambar nama file yang unik, jika tidak penyimpanan berikutnya akan menimpa file sebelumnya.

## Kesimpulan

Anda sekarang tahu cara **set print area excel**, mengonfigurasi **how to export png**, **save range as image**, dan **add picture to worksheet** menggunakan Aspose.Cells. Solusi menyeluruh ini memungkinkan Anda mengubah blok sel apa pun menjadi PNG berkualitas tinggi dengan hanya beberapa baris kode C#.

Selanjutnya, Anda mungkin ingin menjelajahi:

* Menambahkan border atau watermark ke PNG yang diekspor (cari *add picture to worksheet* dengan styling)  
* Mengekspor langsung ke PDF untuk laporan yang dapat dicetak (*export selected cells image* → alur kerja PDF)  
* Mengotomatiskan proses untuk beberapa workbook dalam pekerjaan batch  

Silakan bereksperimen dengan rentang yang berbeda, pengaturan DPI, atau format gambar untuk menyesuaikan kebutuhan proyek Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Mengatur Area Cetak di Excel dan Mengekspor ke PowerPoint – Panduan Langkah‑per‑Langkah](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Mengekspor Area Cetak Excel ke HTML dengan Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [Cara Mengatur Area Cetak di Excel Menggunakan Aspose.Cells untuk .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}