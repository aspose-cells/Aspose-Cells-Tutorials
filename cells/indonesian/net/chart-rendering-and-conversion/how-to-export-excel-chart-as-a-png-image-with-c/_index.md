---
category: general
date: 2026-11-19
description: Cara mengekspor grafik Excel sebagai gambar PNG menggunakan Aspose.Cells.
  Pelajari cara menyimpan gambar grafik Excel dan mengatur format gambar PNG dalam
  beberapa langkah saja.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: id
lastmod: 2026-11-19
og_description: Cara mengekspor diagram Excel sebagai gambar PNG dengan Aspose.Cells.
  Ikuti panduan langkah demi langkah ini untuk menyimpan gambar diagram Excel dan
  mengatur format gambar PNG secara efisien.
og_image_alt: How to export Excel chart as a PNG image
og_title: Cara mengekspor diagram Excel sebagai gambar PNG – panduan C# cepat
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: Cara mengekspor grafik Excel sebagai gambar PNG dengan C#
url: /id/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengekspor chart Excel sebagai gambar PNG dengan C#

Jika Anda perlu **how to export Excel chart** ke dalam gambar portabel, panduan ini menunjukkan solusi lengkap yang siap dijalankan. Menggunakan Aspose.Cells Anda dapat **save Excel chart image** dalam format PNG dengan hanya tiga baris kode, dan tutorial ini juga menjelaskan cara **set image format png** dan **save Excel picture file** dengan aman.

Anda akan menyelesaikan artikel ini dengan program yang dapat dijalankan yang memuat workbook, merender chart pertama, dan menulis file `pivot.png` ke disk. Tanpa alat tambahan, tanpa menyalin‑tempel manual—hanya kode C# bersih yang dapat Anda masukkan ke proyek .NET apa pun.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* .NET 6.0 SDK atau yang lebih baru (kode juga berfungsi dengan .NET Framework 4.6+)
* Visual Studio 2022 atau editor C# apa pun
* Lisensi Aspose.Cells untuk .NET (atau kunci evaluasi sementara)
* File Excel (`pivot.xlsx`) yang berisi setidaknya satu chart pada lembar kerja pertama

Item-item ini adalah satu‑satunya dependensi eksternal; tutorial tidak memerlukan Office terpasang di mesin.

## Langkah 1: Instal Aspose.Cells

Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.Cells
```

Paket ini menambahkan namespace `Aspose.Cells`, yang menyediakan kelas `Workbook`, `ImageOrPrintOptions`, dan kelas lain yang diperlukan untuk **save Excel chart image**.

## Langkah 2: Buat program konsol minimal

Buat aplikasi konsol baru (`dotnet new console -n ExportChartDemo`) dan ganti `Program.cs` yang dihasilkan secara otomatis dengan kode berikut. Program ini menunjukkan **how to export Excel chart** dan menyertakan komentar yang menjelaskan setiap keputusan.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### Mengapa setiap bagian penting

* **Loading the workbook** – `Workbook` mem-parsing file `.xlsx` tanpa memerlukan Microsoft Excel terpasang.
* **ImageOrPrintOptions** – Objek ini mengontrol format output. Menetapkan `ImageFormat = ImageFormat.Png` **sets image format png**, yang lossless dan didukung luas.
* **RenderToImage** – Metode `RenderToImage` mengonversi chart (objek `Picture`) menjadi file gambar. Metode ini juga menangani skala, DPI, dan transparansi secara otomatis.
* **Error handling** – Pemeriksaan `sheet.Pictures.Count == 0` mencegah pengecualian runtime jika lembar kerja tidak memiliki chart, kasus tepi umum ketika pengguna menunjuk ke lembar yang salah.

## Langkah 3: Jalankan program dan verifikasi hasilnya

1. Bangun proyek: `dotnet build`.
2. Jalankan: `dotnet run --project ExportChartDemo`.

Jika semuanya dikonfigurasi dengan benar, Anda akan melihat:

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

Buka `pivot.png` dengan penampil gambar apa pun. Anda harus melihat representasi visual yang tepat dari chart Excel, mengonfirmasi bahwa Anda telah berhasil **saved Excel picture file**.

### Output yang diharapkan

Berikut adalah contoh tampilan PNG yang diekspor; chart sebenarnya tergantung pada file sumber Anda.

![Chart Excel yang diekspor disimpan sebagai gambar PNG](images/exported-chart.png){: .center alt="Bagaimana mengekspor chart Excel sebagai gambar PNG"}

## Langkah 4: Opsi lanjutan – mengekspor beberapa chart

Jika workbook Anda berisi lebih dari satu chart, Anda dapat melakukan loop melalui koleksi `Pictures`:

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

Pola ini memungkinkan Anda **save Excel chart image** untuk setiap chart pada lembar, yang berguna untuk pipeline pelaporan.

## Kesalahan umum dan cara menghindarinya

| Gejala | Penyebab kemungkinan | Solusi |
|--------|----------------------|--------|
| `ArgumentOutOfRangeException` pada `Pictures[0]` | Lembar kerja tidak memiliki chart atau chart berada di lembar lain. | Verifikasi indeks lembar (`Worksheets[0]`) dan pastikan chart ada. Gunakan `Worksheets["SheetName"]` jika diperlukan. |
| Gambar yang diekspor buram | DPI diatur terlalu rendah (default 96). | Tingkatkan `HorizontalResolution` dan `VerticalResolution` dalam `ImageOrPrintOptions`. |
| File PNG kosong atau rusak | Lisensi hilang menyebabkan pembatasan evaluasi. | Terapkan lisensi Aspose.Cells yang valid sebelum memuat workbook (`License license = new License(); license.SetLicense("Aspose.Total.lic");`). |
| Kesalahan jalur file (`FileNotFoundException`) | Placeholder `YOUR_DIRECTORY` tidak tepat. | Gunakan jalur absolut atau `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")`. |

Menangani masalah ini memastikan pengalaman **save excel picture file** yang lancar.

## Tips pro: Ekspor langsung ke memory stream

Kadang-kadang Anda memerlukan gambar di memori (mis., untuk mengunggah ke API web) alih-alih menulis ke disk:

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

Logika **set image format png** yang sama berlaku; Anda hanya mengganti jalur file dengan stream.

## Kesimpulan

Sekarang Anda tahu **how to export Excel chart** sebagai file PNG menggunakan Aspose.Cells untuk .NET. Tutorial ini mencakup:

* Menginstal pustaka
* Memuat workbook
* **Setting image format png**
* **Saving Excel chart image** ke disk
* Menangani beberapa chart dan kesalahan umum

Dengan fondasi ini Anda dapat mengintegrasikan ekspor chart ke dalam pelaporan otomatis, layanan web, atau utilitas desktop. Selanjutnya, jelajahi topik terkait seperti **save excel picture file** sebagai JPEG (`ImageFormat.Jpeg`) atau mengonversi chart ke PDF untuk laporan yang dapat dicetak.

Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Konversi Chart Pie Excel ke Gambar Menggunakan Aspose.Cells .NET: Panduan Langkah demi Langkah](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [Ekspor Chart sebagai PNG – Panduan Lengkap Mengonversi Excel ke HTML dengan Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [Ekspor Sel Excel ke Gambar Menggunakan Aspose.Cells .NET: Panduan Langkah demi Langkah](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}