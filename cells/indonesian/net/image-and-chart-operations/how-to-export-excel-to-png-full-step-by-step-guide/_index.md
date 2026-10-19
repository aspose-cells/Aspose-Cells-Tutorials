---
category: general
date: 2026-08-11
description: Cara mengekspor Excel ke PNG dan menyimpan rentang Excel sebagai gambar
  menggunakan Aspose.Cells. Pelajari cara menyimpan gambar lembar Excel dan mengekspor
  gambar tabel pivot dalam hitungan menit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel to png
- save excel range as image
- save excel sheet picture
- export pivot table image
language: id
lastmod: 2026-08-11
og_description: Cara mengekspor Excel ke PNG dengan cepat. Tutorial ini menunjukkan
  cara menyimpan rentang Excel sebagai gambar, menyimpan gambar lembar Excel, dan
  mengekspor gambar tabel pivot dengan Aspose.Cells.
og_image_alt: Screenshot of C# code exporting an Excel worksheet to a PNG file
og_title: Cara mengekspor Excel ke PNG – panduan pemrograman lengkap
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to export Excel to PNG and save Excel range as image using Aspose.Cells.
    Learn to save Excel sheet picture and export pivot table image in minutes.
  headline: How to export Excel to PNG – full step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Excel automation
- C#
- image export
title: Cara mengekspor Excel ke PNG – panduan langkah demi langkah lengkap
url: /id/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengekspor Excel ke PNG – panduan lengkap langkah demi langkah

Jika Anda perlu **mengekspor Excel ke PNG**, panduan ini akan memandu Anda melalui seluruh proses menggunakan Aspose.Cells untuk .NET. Baik Anda ingin **menyimpan rentang Excel sebagai gambar**, menyematkan gambar lembar kerja dalam laporan, atau **mengekspor gambar tabel pivot** untuk dasbor, langkah‑langkah di bawah ini memberikan solusi siap‑jalankan.

Anda akan belajar cara memuat workbook, menyegarkan tabel pivot, mengonfigurasi opsi gambar, dan akhirnya menulis file PNG yang mempertahankan tampilan bergaya dari data sumber. Tidak diperlukan alat eksternal atau tangkapan layar manual.

## Prasyarat

* .NET 6.0 SDK atau yang lebih baru terpasang  
* Visual Studio 2022 (atau IDE C# apa pun)  
* Lisensi Aspose.Cells untuk .NET atau salinan evaluasi gratis – unduh dari [Aspose.Cells website](https://products.aspose.com/cells/net)  
* File Excel contoh (`PivotTable.xlsx`) yang berisi setidaknya satu tabel pivot  

Kode ini bekerja di Windows, macOS, dan Linux karena Aspose.Cells bersifat platform‑agnostik.

## Langkah 1: Instal Aspose.Cells via NuGet

Buka folder proyek Anda di terminal dan jalankan:

```bash
dotnet add package Aspose.Cells
```

## Langkah 2: Muat workbook yang berisi tabel pivot

```csharp
using Aspose.Cells;
using System;

// Load the Excel file – replace the path with your actual location
string sourcePath = @"YOUR_DIRECTORY\PivotTable.xlsx";
Workbook workbook = new Workbook(sourcePath);
```

*Mengapa ini penting:*  
Memuat workbook memberi Anda akses ke semua lembar kerja, sel, dan objek tersemat. Kelas `Workbook` mengabstraksi format file, sehingga Anda dapat bekerja dengan `.xlsx`, `.xls`, atau bahkan `.csv` tanpa kode parsing tambahan.

## Langkah 3: Pilih lembar kerja dan segarkan tabel pivot

```csharp
// Get the first worksheet where the pivot table resides
Worksheet sheet = workbook.Worksheets[0];

// Refresh the pivot table so it reflects the latest source data
if (sheet.PivotTables.Count > 0)
{
    sheet.PivotTables[0].Refresh();
}
else
{
    Console.WriteLine("No pivot tables found on the selected worksheet.");
}
```

*Mengapa ini penting:*  
Tabel pivot menyimpan cache data sumber mereka. Memanggil `Refresh()` memastikan representasi visual cocok dengan perubahan terbaru, yang penting ketika Anda kemudian **mengekspor gambar tabel pivot**.

## Langkah 4: Konfigurasikan opsi ekspor gambar (format PNG, pelestarian gaya)

```csharp
// Set up export options – PNG keeps lossless quality and supports transparency
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Png,
    // Preserve the pivot table’s style (fonts, colors, borders)
    CalculatePivotTableStyle = true,
    // Optional: set image resolution (DPI) for higher quality
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

*Mengapa ini penting:*  
`CalculatePivotTableStyle = true` memberi tahu Aspose.Cells untuk merender tabel pivot persis seperti yang terlihat di Excel, termasuk pemformatan bersyarat. Menyesuaikan DPI dapat berguna untuk pencetakan atau layar beresolusi tinggi.

## Langkah 5: Tangkap rentang yang digunakan (termasuk tabel pivot) sebagai gambar

```csharp
// Determine the range that contains data – MaxDisplayRange covers the whole used area
CellArea usedRange = sheet.Cells.MaxDisplayRange;

// Add a picture of the used range to the worksheet (position 0,0) and save it
Picture pic = sheet.Pictures.Add(0, 0, usedRange);
pic.Save(@"YOUR_DIRECTORY\PivotImage.png", imgOptions);
```

*Mengapa ini penting:*  
`MaxDisplayRange` secara otomatis memperluas ke sel terjauh yang berisi data, rumus, atau pemformatan, memastikan seluruh tabel pivot dan sel di sekitarnya termasuk. Metode `Pictures.Add` membuat gambar dalam memori yang langsung kami tulis ke disk sebagai file PNG.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semuanya, berikut program konsol mandiri yang dapat Anda salin, tempel, dan jalankan:

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPngExport
{
    class Program
    {
        static void Main()
        {
            // ---------- 1. Load workbook ----------
            string sourcePath = @"YOUR_DIRECTORY\PivotTable.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // ---------- 2. Get first worksheet ----------
            Worksheet sheet = workbook.Worksheets[0];

            // ---------- 3. Refresh pivot table ----------
            if (sheet.PivotTables.Count > 0)
            {
                sheet.PivotTables[0].Refresh();
            }
            else
            {
                Console.WriteLine("No pivot tables found on the selected worksheet.");
                return;
            }

            // ---------- 4. Set image export options ----------
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Png,
                CalculatePivotTableStyle = true,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // ---------- 5. Export used range as PNG ----------
            CellArea usedRange = sheet.Cells.MaxDisplayRange;
            Picture pic = sheet.Pictures.Add(0, 0, usedRange);
            string outputPath = @"YOUR_DIRECTORY\PivotImage.png";
            pic.Save(outputPath, imgOptions);

            Console.WriteLine($"Pivot table image saved to: {outputPath}");
        }
    }
}
```

### Output yang diharapkan

Saat Anda menjalankan program, konsol akan mencetak:

```
Pivot table image saved to: YOUR_DIRECTORY\PivotImage.png
```

Dan file `PivotImage.png` muncul di folder target. Buka dengan penampil gambar apa pun—Anda akan melihat representasi visual persis dari lembar kerja Excel, termasuk tabel pivot yang bergaya, header kolom, dan data di sekitarnya.

## Variasi umum dan kasus tepi

| Skenario | Penyesuaian |
|----------|------------|
| **Export only a specific cell range** (e.g., `A1:D20`) | Ganti `sheet.Cells.MaxDisplayRange` dengan `new CellArea { StartRow = 0, StartColumn = 0, EndRow = 19, EndColumn = 3 }`. |
| **Multiple worksheets** | Loop melalui `workbook.Worksheets` dan ulangi langkah 3‑5 untuk setiap lembar yang ingin Anda ekspor. |
| **Different image format** (JPEG, BMP) | Ubah `SaveFormat = SaveFormat.Jpeg` (atau `Bmp`). PNG direkomendasikan untuk kualitas tanpa kehilangan. |
| **Large worksheets** causing memory pressure | Gunakan `sheet.Pictures.Add` dengan `CellArea` yang lebih kecil atau bagi ekspor menjadi beberapa gambar. |
| **No pivot table present** | Lindungi dengan `if (sheet.PivotTables.Count == 0)` seperti ditunjukkan; Anda masih dapat mengekspor rentang biasa. |

## Tips profesional

* **License early** – Daftarkan lisensi Aspose.Cells Anda sebelum memuat workbook untuk menghindari watermark evaluasi.  
  ```csharp
  var license = new License();
  license.SetLicense(@"YOUR_DIRECTORY\Aspose.Total.NET.lic");
  ```
* **Batch export** – Untuk pipeline pelaporan, bungkus logika ekspor dalam metode yang mengembalikan `byte[]`. Ini memungkinkan Anda mengirim PNG langsung ke API web tanpa menyentuh sistem file.  
* **Transparent background** – PNG sudah mendukung transparansi. Jika Anda menginginkan latar belakang putih, setel `imgOptions.Transparent = false;`.  

## Kesimpulan

Anda sekarang tahu **cara mengekspor Excel ke PNG** menggunakan Aspose.Cells, mencakup alur kerja lengkap dari memuat workbook hingga **menyimpan rentang Excel sebagai gambar**, **menyimpan gambar lembar Excel**, dan **mengekspor gambar tabel pivot**. Kode yang disediakan lengkap, dapat dijalankan, dan dapat disesuaikan untuk skenario dunia nyata seperti pelaporan otomatis atau pembuatan dasbor.

Siap untuk langkah berikutnya? Jelajahi cara **mengonversi PNG ke PDF** untuk laporan yang dapat dicetak, atau integrasikan gambar ke layanan web yang menyajikan visualisasi Excel secara langsung. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Mengekspor Lembar Kerja Excel ke PNG Menggunakan Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Mengekspor Workbook Excel sebagai Gambar Menggunakan Aspose.Cells untuk Java: Panduan Langkah demi Langkah](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Cara Mengekspor Sel Excel sebagai Gambar Menggunakan Aspose.Cells untuk Java](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}