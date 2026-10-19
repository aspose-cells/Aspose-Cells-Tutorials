---
category: general
date: 2026-08-04
description: Ekspor diagram Excel ke PowerPoint menggunakan Aspose.Cells dalam C#.
  Ikuti panduan konversi Excel ke PowerPoint langkah demi langkah ini dan pertahankan
  bentuk tetap dapat diedit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: id
lastmod: 2026-08-04
og_description: Ekspor diagram Excel ke PowerPoint dengan Aspose.Cells dalam C#. Pelajari
  cara membuat PPTX yang dapat diedit, mempertahankan data diagram, dan mengotomatiskan
  konversi Excel ke PowerPoint.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: Ekspor diagram Excel ke PowerPoint dengan C# – tutorial lengkap Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: Ekspor diagram Excel ke PowerPoint dengan C# – panduan lengkap Aspose.Cells
url: /id/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor diagram Excel ke PowerPoint dengan C# – panduan lengkap Aspose.Cells

Jika Anda perlu **mengekspor diagram Excel ke PowerPoint**, tutorial ini menunjukkan cara melakukannya dengan Aspose.Cells dan Aspose.Slides di C#. Anda akan mendapatkan file PPTX yang dapat diedit sepenuhnya, yang mempertahankan data dan bentuk diagram, sehingga konversi siap untuk pekerjaan desain lebih lanjut.

Mengekspor diagram dari Excel ke PowerPoint adalah kebutuhan umum saat membangun pipeline pelaporan otomatis, deck penjualan, atau materi pelatihan. Dalam panduan ini Anda akan mempelajari langkah‑langkah tepat untuk melakukan **konversi Excel ke PowerPoint** yang menjaga semua elemen diagram dapat diedit. Tidak diperlukan penyalinan‑tempel manual, dan kode berfungsi dengan .NET 6+ serta .NET Framework klasik.

## Prasyarat

- Lisensi Aspose.Cells yang valid (atau kunci evaluasi gratis)  
- Aspose.Slides untuk .NET ditambahkan ke proyek (perpustakaan menangani output PPTX)  
- .NET 6 SDK atau yang lebih baru terpasang  
- Buku kerja Excel yang berisi setidaknya satu diagram (untuk contoh ini kami menggunakan `Shapes.xlsx`)  

Anda dapat menginstal paket NuGet dengan perintah berikut:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## Langkah 1: Muat buku kerja Excel

Operasi pertama adalah membuka buku kerja yang berisi diagram yang ingin Anda ekspor. Kelas `Workbook` mewakili seluruh file Excel.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**Mengapa ini penting:** Memuat buku kerja memberi Anda akses ke lembar kerja, diagram, dan formatnya. Aspose.Cells membaca file tanpa memerlukan Microsoft Office terpasang, sehingga solusi tetap ringan dan ramah server.

## Langkah 2: Pilih lembar kerja dan tentukan area cetak

Sebuah lembar kerja dapat berisi banyak diagram, tetapi biasanya Anda mengekspor wilayah tertentu. Menetapkan `PrintArea` memberi tahu Aspose.Cells sel mana (termasuk diagram) yang harus dirender.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**Mengapa ini penting:** Dengan membatasi ekspor ke area cetak yang ditentukan, Anda menghindari slide kosong yang tidak perlu dan menjaga ukuran file PPTX tetap kecil. Area tersebut dapat disesuaikan agar cocok dengan rentang diagram Anda.

## Langkah 3: Konfigurasikan opsi ekspor untuk PPTX yang dapat diedit

Aspose.Cells menggunakan kelas `ImageOrPrintOptions` untuk mengontrol format output dan kemampuan edit. Menetapkan `ImageFormat` ke `ImageFormat.Pptx` membuat file PowerPoint, sementara `ExportEditableShapes = true` mempertahankan objek diagram sebagai bentuk yang dapat diedit.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**Mengapa ini penting:** Flag `ExportEditableShapes` adalah kunci untuk menghasilkan **bentuk yang dapat diedit di PowerPoint**. Tanpanya, diagram akan dirasterkan menjadi gambar, sehingga kehilangan kemampuan untuk memodifikasi titik data atau gaya nanti.

## Langkah 4: Simpan lembar kerja sebagai presentasi PowerPoint

Akhirnya, panggil metode `Save` pada objek `Workbook`. Enum `SaveFormat.Pptx` memberi tahu Aspose.Cells untuk menghasilkan file PowerPoint.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

Setelah kode selesai, buka `ShapesExport.pptx` di PowerPoint. Anda akan melihat slide yang berisi diagram Excel asli sebagai objek diagram PowerPoint asli. Klik ganda pada diagram untuk mengedit data, mengubah warna, atau menambahkan animasi—seperti seolah‑olah Anda membuat diagram tersebut langsung di PowerPoint.

### Output yang diharapkan

| Nama file                | Konten pada slide                         |
|--------------------------|------------------------------------------|
| `ShapesExport.pptx`      | Diagram dari `Shapes.xlsx` ditampilkan sebagai diagram PowerPoint yang dapat diedit, dengan label sumbu, legenda, dan seri data tetap utuh. |

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin, tempel, dan jalankan. Program ini mencakup semua pernyataan `using` yang diperlukan, penanganan kesalahan, dan komentar.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Penjelasan setiap blok**

| Blok | Tujuan |
|------|--------|
| `using` directives | Menyertakan namespace Aspose.Cells dan Aspose.Slides. |
| `Workbook workbook = new Workbook(excelPath);` | Muat file Excel tanpa memerlukan Office terpasang. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | Membatasi ekspor ke wilayah yang berisi diagram. |
| `ImageOrPrintOptions` | Mengonfigurasi output PPTX dan mengaktifkan **Ekspor PPTX Aspose.Cells** dengan bentuk yang dapat diedit. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | Menulis file PowerPoint ke disk. |
| `try / catch` | Memberikan penanganan kesalahan dasar untuk file yang hilang atau masalah lisensi. |

Menjalankan program ini menghasilkan slide PowerPoint yang dapat Anda buka di Microsoft PowerPoint, Google Slides (setelah konversi), atau penampil kompatibel lainnya.

## Variasi umum dan kasus tepi

### Mengekspor beberapa lembar kerja

Jika Anda memerlukan slide untuk setiap lembar kerja, lakukan iterasi melalui `workbook.Worksheets` dan panggil `Save` dengan nama file unik untuk setiap iterasi.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### Mengontrol tata letak slide

Aspose.Slides memungkinkan Anda menambahkan tata letak slide khusus setelah ekspor. Buat presentasi baru, impor slide yang dihasilkan, lalu terapkan tema master.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### Menangani diagram dengan sumber data eksternal

Jika sebuah diagram merujuk pada rentang data di luar area cetak yang ditentukan, perpanjang `PrintArea` untuk menyertakan sel tersebut. Jika tidak, diagram dapat kehilangan seri data selama ekspor.

### Pertimbangan lisensi

Perpustakaan Aspose berfungsi dalam mode evaluasi dengan watermark. Untuk menghapus watermark, tetapkan lisensi sebelum panggilan API apa pun:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Lakukan hal yang sama untuk Aspose.Slides jika Anda menggunakan fitur lanjutan.

## Tips profesional

- **Gunakan kembali opsi ekspor:** Buat satu instance `ImageOrPrintOptions` dan tetapkan ke setiap lembar kerja untuk menjaga kode tetap DRY.  
- **Pemrosesan batch:** Untuk pelaporan skala besar, gabungkan logika ekspor ini dengan background worker atau Azure Function untuk menghasilkan file PPTX sesuai permintaan.  
- **Kinerja:** Jika Anda hanya membutuhkan gambar diagram (tidak dapat diedit), setel `ExportEditableShapes = false`. Ini mengurangi penggunaan memori dan mempercepat konversi.  
- **Pengujian:** Verifikasi PPTX yang dihasilkan pada instalasi PowerPoint Windows dan macOS, karena beberapa keanehan rendering berbeda antar platform.

## Kesimpulan

Anda kini memiliki solusi lengkap end‑to‑end untuk **mengekspor diagram Excel ke PowerPoint** menggunakan C#. Tutorial ini mencakup memuat buku kerja, memilih area cetak, mengonfigurasi **Ekspor PPTX Aspose.Cells** dengan **bentuk yang dapat diedit di PowerPoint**, dan menyimpan hasilnya sebagai file PPTX yang sepenuhnya dapat diedit.  

Dari sini Anda dapat menjelajahi skenario **konversi Excel ke PowerPoint** tambahan seperti ekspor batch, tata letak slide khusus, atau mengintegrasikan proses ke dalam API web. Bereksperimenlah dengan berbagai jenis diagram, tambahkan gambar, atau gabungkan beberapa lembar kerja menjadi satu presentasi untuk menyesuaikan output dengan kebutuhan bisnis Anda.

Siap mengotomatisasi alur kerja pelaporan Anda? Cobalah mengganti file sumber, menyesuaikan area cetak, dan mengintegrasikan kode ke dalam layanan .NET Anda yang ada. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengonversi Excel ke PowerPoint Menggunakan Aspose.Cells untuk .NET: Panduan Lengkap](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Cara Mengekspor Diagram Excel ke PDF Menggunakan Aspose.Cells untuk .NET: Panduan Langkah demi Langkah](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Mengekspor Sel Excel ke Gambar Menggunakan Aspose.Cells .NET: Panduan Langkah demi Langkah](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}