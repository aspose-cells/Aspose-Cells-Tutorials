---
category: general
date: 2026-08-17
description: Simpan Excel sebagai PowerPoint dengan C# – panduan langkah demi langkah
  untuk mengonversi file XLSX, membuat kotak teks yang dapat diedit, dan menghasilkan
  output PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: id
lastmod: 2026-08-17
og_description: Simpan Excel sebagai PowerPoint di C# dengan contoh kode lengkap.
  Pelajari cara mengonversi XLSX, membuat kotak teks dapat diedit, dan mengekspor
  ke PPTX.
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: Simpan Excel sebagai PowerPoint di C# – panduan konversi lengkap
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: Cara menyimpan Excel sebagai PowerPoint menggunakan C# dan Aspose.Cells
url: /id/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyimpan Excel sebagai PowerPoint menggunakan C# dan Aspose.Cells

Jika Anda perlu **menyimpan Excel sebagai PowerPoint** dalam proyek .NET, panduan ini menunjukkan solusi lengkap yang siap dijalankan. Anda akan melihat cara memuat workbook XLSX, membuat setiap textbox pada lembar dapat diedit, dan mengekspor hasilnya ke file PPTX—semua dengan hanya beberapa baris C#.

Mengonversi Excel ke PowerPoint adalah kebutuhan umum untuk dasbor pelaporan, deck slide, atau pembuatan presentasi otomatis. Tutorial ini juga mencakup **cara mengedit textbox** secara programatis, sehingga Anda dapat menyesuaikan konten slide sebelum menyimpan.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* .NET 6.0 (atau lebih baru) SDK terpasang  
* Lingkungan pengembangan seperti Visual Studio 2022 atau VS Code  
* Lisensi Aspose.Cells untuk .NET (atau kunci evaluasi gratis) – unduh dari [Aspose website](https://products.aspose.com/cells/net/)  
* File `input.xlsx` yang ingin Anda konversi  

> **Pro tip:** Jika Anda menggunakan versi evaluasi gratis, file PPTX output akan berisi watermark. Versi berlisensi akan menghilangkannya.

## Langkah 1: Instal paket NuGet Aspose.Cells

Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package Aspose.Cells
```

Ini menambahkan assembly `Aspose.Cells`, yang menyediakan kelas `Workbook`, `Worksheet`, dan `Shape` yang diperlukan untuk konversi.

## Langkah 2: Buat kerangka aplikasi konsol

Buat proyek konsol baru (jika Anda belum memilikinya):

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

Ganti `Program.cs` yang dihasilkan dengan kode yang ditunjukkan pada langkah berikutnya.

## Langkah 3: Muat workbook dan pilih lembar kerja pertama

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Mengapa ini penting:**  
`Workbook` membaca file Excel ke dalam memori, sementara `Worksheet` memberi Anda akses ke sel, diagram, dan bentuk pada lembar. Lembar kerja pertama biasanya merupakan laporan default yang ingin Anda tampilkan.

## Langkah 4: Buat setiap textbox pada lembar dapat diedit

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**Mengapa Anda membutuhkan ini:**  
Secara default, textbox yang diimpor dari Excel bersifat read‑only saat ditampilkan di PowerPoint. Menetapkan `IsEditable = true` memungkinkan Anda (atau pengguna PowerPoint nanti) mengubah teks secara langsung pada slide.

## Langkah 5: Simpan workbook sebagai presentasi PowerPoint

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**Apa yang terjadi di balik layar:**  
`Workbook.Save` mendeteksi nilai enum `SaveFormat.Pptx` dan menerjemahkan tata letak lembar Excel—termasuk baris, kolom, diagram, dan textbox yang kini dapat diedit—menjadi objek slide PowerPoint.

## Kode sumber lengkap (dapat dijalankan)

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### Output yang diharapkan

Saat Anda menjalankan program (`dotnet run`), Anda akan melihat:

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

Membuka `output.pptx` di Microsoft PowerPoint akan menampilkan slide yang mencerminkan lembar Excel asli. Semua textbox dapat diedit langsung dengan mengklik ganda mereka.

## Pertanyaan umum dan kasus tepi

| Pertanyaan | Jawaban |
|------------|---------|
| **Apakah saya dapat mengonversi lembar kerja tertentu selain yang pertama?** | Ya. Ganti `workbook.Worksheets[0]` dengan `workbook.Worksheets["SheetName"]` atau indeks apa pun yang Anda perlukan. |
| **Bagaimana jika workbook berisi beberapa lembar?** | Panggil `workbook.Save` sekali per lembar kerja, berikan nama file PPTX yang berbeda untuk masing‑masing, atau gabungkan mereka menjadi satu presentasi dengan menggunakan objek `Presentation` dari Aspose.Slides. |
| **Apakah diagram akan tetap dipertahankan?** | Aspose.Cells secara otomatis mengonversi diagram Excel menjadi objek diagram PowerPoint. Tidak diperlukan kode tambahan. |
| **Bagaimana cara mengubah ukuran slide?** | Setelah `workbook.Save`, Anda dapat memuat PPTX yang dihasilkan dengan Aspose.Slides dan menyesuaikan `Presentation.SlideSize`. |
| **Bagaimana jika saya perlu mengedit teks textbox sebelum menyimpan?** | Akses `shapeItem.TextBox.Text` di dalam loop, ubah teksnya, lalu setel `IsEditable = true`. Contoh: `shapeItem.TextBox.Text = "Judul baru";` |

## Tips pemecahan masalah

* **“ShapeType.TextBox” tidak ditemukan** – Pastikan Anda menggunakan Aspose.Cells versi 25.11 atau lebih baru; versi sebelumnya tidak memiliki properti `IsEditable`.  
* **Kesalahan file tidak ditemukan** – Verifikasi bahwa `YOUR_DIRECTORY` adalah jalur absolut atau bahwa jalur relatif mengarah ke lokasi yang tepat.  
* **Lisensi tidak diterapkan** – Panggil `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` sebelum memuat workbook untuk menghilangkan watermark evaluasi.

## Kesimpulan

Anda kini tahu cara **menyimpan Excel sebagai PowerPoint** dengan C# dengan memuat workbook XLSX, membuat setiap textbox dapat diedit, dan mengekspor ke PPTX. Metode ini menangani diagram, gambar, dan pemformatan sel secara otomatis, memberikan Anda deck slide yang siap dipresentasikan.

Selanjutnya, jelajahi topik terkait seperti **mengonversi Excel ke PowerPoint dengan Aspose.Slides**, **cara mengedit textbox secara programatis setelah konversi**, atau **memproses batch banyak workbook**. Masing‑masing topik ini membangun di atas langkah‑langkah inti yang dibahas di sini dan dapat lebih mengotomatisasi alur kerja pelaporan Anda.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Mengonversi Excel ke PowerPoint Menggunakan Aspose.Cells untuk .NET: Panduan Lengkap](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Cara Menyalin Pivot Table di C# – Mengonversi Excel ke PPTX, Menyalin Rentang & Membuat Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Cara Menyimpan File Excel dalam Berbagai Format Menggunakan Aspose.Cells .NET (Panduan 2023)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}