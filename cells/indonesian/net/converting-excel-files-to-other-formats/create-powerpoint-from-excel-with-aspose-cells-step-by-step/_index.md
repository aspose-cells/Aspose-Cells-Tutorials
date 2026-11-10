---
category: general
date: 2026-10-01
description: Buat PowerPoint dari Excel menggunakan Aspose.Cells dalam C#. Ekspor
  Excel ke PowerPoint dan konversi XLSX ke PPTX dengan cepat menggunakan contoh kode
  lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PowerPoint from Excel
- export Excel to PowerPoint
- convert Excel to PPTX
- convert XLSX to PPTX
- generate PowerPoint from Excel
language: id
lastmod: 2026-10-01
og_description: Buat PowerPoint dari Excel menggunakan Aspose.Cells di C#. Pelajari
  cara mengekspor Excel ke PowerPoint dan mengonversi XLSX ke PPTX dalam beberapa
  baris kode.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel using Aspose.Cells
og_title: Buat PowerPoint dari Excel dengan Aspose.Cells – panduan singkat
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create PowerPoint from Excel using Aspose.Cells in C#. Export Excel
    to PowerPoint and convert XLSX to PPTX quickly with a complete code example.
  headline: Create PowerPoint from Excel with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Office automation
title: Buat PowerPoint dari Excel dengan Aspose.Cells – panduan langkah demi langkah
url: /id/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat PowerPoint dari Excel dengan Aspose.Cells – panduan langkah‑demi‑langkah

Jika Anda perlu **membuat PowerPoint dari Excel**, tutorial ini menunjukkan cara melakukannya dengan Aspose.Cells untuk .NET. Anda akan belajar **mengekspor Excel ke PowerPoint**, mengonversi workbook XLSX menjadi presentasi PPTX, dan menyesuaikan slide yang dihasilkan tanpa meninggalkan proyek C# Anda.

Panduan ini mencakup semua yang Anda perlukan untuk menjalankan kode pada .NET 6 atau yang lebih baru, termasuk penyiapan proyek, paket NuGet yang diperlukan, dan contoh lengkap yang dapat dijalankan. Pada akhir tutorial, Anda akan memiliki file PowerPoint yang berisi grafik Excel asli persis seperti yang muncul di workbook.

## Apa yang Anda perlukan

| Prasyarat | Alasan |
|---|---|
| .NET 6 SDK atau yang lebih baru | Menyediakan runtime untuk aplikasi konsol C# |
| Visual Studio 2022 (atau IDE apa pun) | Memungkinkan pembuatan proyek dan debugging yang mudah |
| Paket NuGet Aspose.Cells untuk .NET | Menyediakan kelas `Workbook` dan API ekspor |
| File Excel (`.xlsx`) yang berisi setidaknya satu grafik | Data sumber untuk slide PowerPoint |

> **Pro tip:** Aspose.Cells bekerja di Windows, Linux, dan macOS, sehingga Anda dapat menjalankan kode yang sama di dalam kontainer Docker atau pipeline CI.

## Langkah 1: Buat proyek konsol baru dan tambahkan Aspose.Cells

Buka terminal (atau Visual Studio Package Manager Console) dan jalankan:

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
dotnet add package Aspose.Cells
```

Perintah `dotnet add package` mengunduh versi stabil terbaru dari **Aspose.Cells**, yang mencakup metode `ExportPptx` yang akan digunakan nanti.

## Langkah 2: Tambahkan workbook Excel sumber

Letakkan file Excel yang ingin Anda konversi ke dalam folder proyek. Untuk tutorial ini kami menggunakan `ChartOle.xlsx`, yang berisi satu grafik pada lembar kerja pertama.

```
/ExcelToPptxDemo
│   Program.cs
│   ChartOle.xlsx   ← your source workbook
```

## Langkah 3: Tulis kode yang **membuat PowerPoint dari Excel**

Buka `Program.cs` dan ganti isinya dengan kode berikut. Contoh ini mendemonstrasikan operasi **ekspor inti** serta cara menangani kasus tepi umum seperti file yang hilang dan tipe grafik yang tidak didukung.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelToPptxDemo
{
    class Program
    {
        static void Main()
        {
            // Define input and output paths
            string inputPath = Path.Combine(AppContext.BaseDirectory, "ChartOle.xlsx");
            string outputPath = Path.Combine(AppContext.BaseDirectory, "Exported.pptx");

            // Verify that the source workbook exists
            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: The file '{inputPath}' was not found.");
                return;
            }

            try
            {
                // Load the Excel workbook that contains the chart
                var workbook = new Workbook(inputPath);

                // Export the first worksheet as a PowerPoint presentation
                // This call performs the **convert Excel to PPTX** operation.
                workbook.Worksheets[0].ExportPptx(outputPath);

                Console.WriteLine($"Success: PowerPoint file created at '{outputPath}'.");
            }
            catch (Exception ex)
            {
                // Catch any errors thrown by Aspose.Cells (e.g., unsupported chart)
                Console.WriteLine($"Export failed: {ex.Message}");
            }
        }
    }
}
```

### Mengapa ini berhasil

* `Workbook` membaca seluruh file Excel, termasuk grafik, tabel, dan pemformatan yang disematkan.
* `ExportPptx` mengonversi lembar kerja aktif menjadi dek slide PPTX. Metode ini secara otomatis mengubah grafik Excel menjadi bentuk PowerPoint, mempertahankan kesetiaan visual.
* Kode membungkus operasi dalam blok `try/catch` untuk menampilkan kesalahan seperti kegagalan **convert XLSX to PPTX** yang disebabkan oleh file korup.

## Langkah 4: Jalankan program dan verifikasi output

Eksekusi aplikasi:

```bash
dotnet run
```

Anda akan melihat pesan di konsol:

```
Success: PowerPoint file created at '.../Exported.pptx'.
```

Buka `Exported.pptx` di Microsoft PowerPoint atau penampil kompatibel lainnya. Slide pertama menampilkan grafik persis seperti yang muncul di `ChartOle.xlsx`. Ini menegaskan bahwa Anda telah berhasil **menghasilkan PowerPoint dari Excel**.

## Langkah 5: Lanjutan – mengekspor beberapa lembar kerja atau tata letak slide khusus

Contoh dasar hanya mengekspor lembar kerja pertama. Dalam skenario dunia nyata Anda mungkin perlu:

* **Mengekspor beberapa lembar kerja** ke slide terpisah.
* **Mengontrol ukuran slide** atau menambahkan placeholder judul.
* **Menyertakan lembar kerja tersembunyi** dalam konversi.

Berikut cuplikan singkat yang mengiterasi semua lembar kerja dan menambahkan masing‑masing sebagai slide terpisah:

```csharp
// Export each worksheet as a separate slide
var pptxPath = Path.Combine(AppContext.BaseDirectory, "FullExport.pptx");
var presentation = new Presentation(); // Aspose.Slides.Presentation, if you have the Slides library

foreach (Worksheet ws in workbook.Worksheets)
{
    // Convert worksheet to an image first (optional for custom layout)
    var imgStream = new MemoryStream();
    ws.PageSetup.PrintArea = ws.Cells.MaxDisplayRange; // ensure full content
    ws.Pictures[0].ToImage(imgStream, ImageFormat.Png);

    // Add a new slide and insert the image
    var slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
    slide.Shapes.AddPictureFrame(ShapeType.Rectangle, 0, 0, presentation.SlideSize.Size.Width, presentation.SlideSize.Size.Height, imgStream);
}

// Save the final presentation
presentation.Save(pptxPath, SaveFormat.Pptx);
```

> **Catatan:** Cuplikan lanjutan memerlukan pustaka **Aspose.Slides for .NET**. Jika Anda hanya membutuhkan konversi satu‑lembar sederhana, panggilan `ExportPptx` sebelumnya sudah cukup.

## Kesulitan umum dan cara menghindarinya

| Masalah | Penyebab | Solusi |
|---|---|---|
| Slide kosong setelah ekspor | Lembar kerja tidak berisi objek yang terlihat | Pastikan setidaknya ada satu grafik, tabel, atau bentuk sebelum memanggil `ExportPptx`. |
| Font hilang di PowerPoint | Font tidak terpasang pada mesin tempat PPTX dibuka | Sematkan font yang diperlukan dalam workbook Excel atau instal font tersebut pada sistem target. |
| Skala tidak terduga | Grafik besar melebihi dimensi slide | Sesuaikan properti `PageSetup.Zoom` pada lembar kerja sebelum ekspor. |
| `convert XLSX to PPTX` melempar `NotSupportedException` | Tipe grafik tidak didukung oleh Aspose.Cells (misalnya peta 3‑D) | Ganti grafik dengan tipe yang didukung atau ekspor lembar kerja sebagai gambar terlebih dahulu. |

Menangani kasus tepi ini memastikan alur kerja **ekspor Excel ke PowerPoint** yang andal dalam lingkungan produksi.

## Kesimpulan

Anda kini tahu cara **membuat PowerPoint dari Excel** menggunakan Aspose.Cells untuk .NET. Tutorial ini mencakup:

* Penyiapan proyek dan instalasi NuGet
* Memuat workbook Excel dan memanggil `ExportPptx`
* Menjalankan kode serta mengonfirmasi PPTX yang dihasilkan
* Memperluas solusi untuk menangani banyak lembar kerja dan tata letak khusus
* Tips praktis untuk menghindari masalah konversi umum

Dengan pengetahuan ini Anda dapat mengotomatisasi pembuatan laporan, membangun pipeline presentasi, atau mengintegrasikan konversi Excel‑ke‑PowerPoint ke dalam aplikasi C# apa pun. Bereksperimenlah dengan berbagai tipe grafik, tambahkan judul slide, atau gabungkan ekspor dengan Aspose.Slides untuk pembuatan presentasi berfitur lengkap.

--- 

*Siap menjelajah lebih jauh? Lihat topik terkait seperti **convert Excel to PDF**, **embed Excel data in Word**, atau **use Aspose.Slides to programmatically edit PPTX files**.*

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/spanish/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}