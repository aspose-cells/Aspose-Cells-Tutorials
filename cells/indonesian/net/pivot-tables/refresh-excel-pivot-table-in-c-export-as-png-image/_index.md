---
category: general
date: 2026-02-23
description: Segarkan tabel pivot Excel di C# dan ekspor sebagai gambar PNG. Pelajari
  cara memuat workbook Excel di C#, menyegarkan pivot, dan menyimpan hasilnya.
draft: false
keywords:
- refresh excel pivot table
- load excel workbook c#
- export pivot as image
- export excel pivot image
language: id
og_description: Segarkan tabel pivot Excel di C# dan ekspor sebagai gambar PNG. Panduan
  langkah demi langkah dengan kode lengkap dan tips praktis.
og_title: Segarkan Tabel Pivot Excel di C# – Ekspor sebagai Gambar PNG
tags:
- C#
- Excel
- Aspose.Cells
- Data Automation
title: Segarkan Tabel Pivot Excel di C# – Ekspor sebagai Gambar PNG
url: /id/net/pivot-tables/refresh-excel-pivot-table-in-c-export-as-png-image/
---

output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Refresh Excel Pivot Table in C# – Export as PNG Image

Pernah perlu **menyegarkan tabel pivot Excel** dari aplikasi C# dan kemudian mengubahnya menjadi gambar? Anda bukan satu‑satunya yang kebingungan tentang hal itu. Pada tutorial ini kami akan menjelaskan langkah demi langkah cara **refresh Excel pivot table**, **load Excel workbook C#**, dan akhirnya **export pivot as image**—semua dalam potongan kode yang bersih dan dapat dijalankan.

Apa yang akan Anda dapatkan pada akhir tutorial adalah file PNG yang tampak persis seperti pivot yang Anda lihat di Excel, siap disisipkan ke dalam laporan, email, atau dasbor. Tanpa menyalin‑tempel manual, tanpa interop COM yang rumit, hanya kode .NET yang langsung.

## Prerequisites

- .NET 6+ (atau .NET Framework 4.7+)
- Aspose.Cells for .NET (versi percobaan gratis atau berlisensi) – Anda dapat mengunduhnya dari NuGet dengan `Install-Package Aspose.Cells`.
- Sebuah file `input.xlsx` yang berisi setidaknya satu tabel pivot.
- Sebuah folder di mana Anda memiliki izin menulis untuk gambar output.

> **Tip pro:** Jika Anda menggunakan Visual Studio, aktifkan **nullable reference types** (`<Nullable>enable</Nullable>`) untuk menangkap bug terkait null lebih awal.

---

## Step 1: Load Excel Workbook in C#

Hal pertama yang kita perlukan adalah objek `Workbook` yang menunjuk ke file sumber kita. Anggap ini seperti membuka file Excel secara programatik.

```csharp
using System;
using Aspose.Cells;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // The rest of the steps follow…
```

**Mengapa ini penting:** Memuat workbook memberi kita akses ke lembar kerja, sel, dan—yang paling penting—tabel pivot yang telah Anda buat. Jika file tidak ditemukan, Aspose akan melempar `FileNotFoundException` yang jelas, yang dapat Anda tangkap untuk penanganan yang lebih baik.

---

## Step 2: Configure Image Export Options (Export Pivot as Image)

Aspose.Cells memungkinkan Anda menentukan bagaimana pivot harus dirender. Di sini kami meminta PNG karena tidak kehilangan kualitas dan didukung secara luas.

```csharp
        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Optional: set resolution for sharper output
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

**Mengapa PNG?** Tidak seperti JPEG, PNG mempertahankan garis kisi yang tajam dan bayangan teks yang menjadi andalan tabel pivot. Jika Anda membutuhkan file yang lebih kecil, Anda dapat beralih ke `ImageFormat.Jpeg` dan menyesuaikan kualitas, tetapi Anda akan kehilangan sedikit kejernihan.

---

## Step 3: Refresh the Pivot Table

Sebelum kami menangkap visualnya, kami harus memastikan pivot mencerminkan data terbaru. Inilah inti dari **refresh excel pivot table**.

```csharp
        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();
```

**Apa yang terjadi di balik layar?** `Refresh()` menghitung ulang pivot berdasarkan rentang sumber. Jika Anda menambahkan baris ke data sumber setelah workbook disimpan, pemanggilan ini akan menarik data baru tersebut. Melewatkan langkah ini menghasilkan gambar usang yang tidak cocok dengan data saat ini.

---

## Step 4: Render the Pivot Table to PNG (Export Excel Pivot Image)

Sekarang semuanya sudah mutakhir, kami dapat merender pivot langsung ke file gambar.

```csharp
        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

**Hasil:** Buka `pivot.png` dan Anda akan melihat snapshot pixel‑perfect dari pivot yang telah disegarkan. File ini dapat dilampirkan ke email, disisipkan dalam halaman web, atau dimasukkan ke dalam mesin pelaporan.

### Expected Output

```
Pivot table exported successfully to: YOUR_DIRECTORY\pivot.png
```

Jika Anda menelusuri folder tersebut, PNG akan menampilkan baris, kolom, dan filter yang sama seperti yang Anda lihat di Excel.

---

## Handling Common Edge Cases

| Situation | What to Do |
|-----------|------------|
| **Multiple pivot tables** | Loop melalui `worksheet.PivotTables` dan panggil `Refresh()` / `RenderToImage()` untuk masing‑masing. |
| **Dynamic sheet names** | Gunakan `wb.Worksheets[wb.Worksheets.IndexOf("SheetName")]` atau cari berdasarkan `worksheet.Name`. |
| **Large datasets** | Tingkatkan `imgOptions.OnePagePerSheet = false` dan atur `imgOptions.PageWidth`/`PageHeight` untuk mengontrol pagination. |
| **Missing Aspose.Cells license** | Versi percobaan gratis menambahkan watermark. Dapatkan lisensi dan panggil `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` sebelum memuat workbook. |
| **File‑path issues** | Gunakan `Path.Combine(Environment.CurrentDirectory, "input.xlsx")` untuk menghindari pemisah yang ditulis keras. |

---

## Pro Tips & Best Practices

- **Dispose properly** – Bungkus `Workbook` dalam blok `using` atau panggil `wb.Dispose()` setelah selesai untuk membebaskan sumber daya native.
- **Cache rendered images** – Jika Anda membutuhkan gambar pivot yang sama berulang kali, simpan PNG di disk dan gunakan kembali alih‑alih merender setiap kali.
- **Thread safety** – Setiap thread harus bekerja dengan instance `Workbook` masing‑masing; objek Aspose.Cells tidak thread‑safe.
- **Performance** – Merender pivot besar dapat memakan memori. Ubah `imgOptions.ImageFormat` menjadi `Bmp` untuk proses lebih cepat namun file lebih besar, atau turunkan DPI untuk render yang lebih cepat.

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.xlsx");
        if (!File.Exists(inputPath))
        {
            Console.Error.WriteLine($"File not found: {inputPath}");
            return;
        }

        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        if (worksheet.PivotTables.Count == 0)
        {
            Console.Error.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();

        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = Path.Combine(Environment.CurrentDirectory, "pivot.png");
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");

        // Clean up
        wb.Dispose();
    }
}
```

Jalankan program, buka `pivot.png`, dan Anda akan melihat tabel pivot yang telah disegarkan persis seperti yang muncul di Excel.

---

## Frequently Asked Questions

**Q: Does this work with .xlsx files created by LibreOffice?**  
A: Yes. Aspose.Cells membaca format Open XML terlepas dari aplikasi asalnya, jadi Anda dapat **load excel workbook c#** dari LibreOffice, ekspor Google Sheets, atau sumber lain mana pun.

**Q: Can I export multiple worksheets at once?**  
A: Absolutely. Loop over `wb.Worksheets` dan terapkan logika `RenderToImage` yang sama per lembar. Pastikan memberi setiap output nama file yang unik.

**Q: What if the pivot uses an external data source?**  
A: Aspose.Cells dapat menyegarkan koneksi eksternal jika tersemat dalam file, tetapi Anda harus menyediakan string koneksi dan kredensial secara programatik. Lihat dokumentasi Aspose untuk `DataSourceOptions`.

---

## Conclusion

Anda kini memiliki solusi menyeluruh, dari awal hingga akhir, untuk **refresh excel pivot table** dari C# dan **export excel pivot image** sebagai PNG. Kode tersebut menunjukkan cara **load excel workbook c#**, mengatur opsi gambar, memastikan pivot mencerminkan data terbaru, dan akhirnya merendernya ke file.

Selanjutnya, Anda dapat menjelajahi **export pivot as image** dalam format lain (PDF, SVG) atau mengotomatiskan proses untuk banyak workbook dalam pekerjaan batch. Ingin menyisipkan PNG ke dalam laporan Word? Kelas `ImageOrPrintOptions` yang sama bekerja dengan Aspose.Words.

Silakan bereksperimen, coba hal baru, dan ajukan pertanyaan di kolom komentar—selamat coding! 

![Tangkapan layar refresh tabel pivot Excel](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}