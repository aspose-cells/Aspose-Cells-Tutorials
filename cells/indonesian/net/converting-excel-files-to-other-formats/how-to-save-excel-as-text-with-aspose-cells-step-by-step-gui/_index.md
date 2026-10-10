---
category: general
date: 2026-10-10
description: Pelajari cara menyimpan Excel sebagai teks di C# menggunakan Aspose.Cells.
  Panduan ini mencakup mengonversi Excel ke txt, mengekspor XLSX ke txt, dan membuat
  txt dari Excel dengan kode lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as text
- convert excel to txt
- export xlsx to txt
- create txt from excel
language: id
lastmod: 2026-10-10
og_description: Simpan Excel sebagai teks menggunakan Aspose.Cells untuk .NET. Ikuti
  panduan ini untuk mengonversi Excel ke txt, mengekspor XLSX ke txt, dan membuat
  txt dari Excel dengan contoh kode.
og_image_alt: Screenshot of C# code that saves an Excel workbook as a plain‑text file
og_title: Simpan Excel sebagai teks di C# – tutorial lengkap Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to save Excel as text in C# using Aspose.Cells. This guide
    covers convert Excel to txt, export XLSX to txt, and create txt from Excel with
    full code.
  headline: How to save Excel as text with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to save Excel as text in C# using Aspose.Cells. This guide
    covers convert Excel to txt, export XLSX to txt, and create txt from Excel with
    full code.
  name: How to save Excel as text with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Prerequisites
    text: '* .NET 6.0 or later (the code also works with .NET Framework 4.7.2+). *
      Basic familiarity with C# and Visual Studio (or any .NET IDE). * An active Aspose.Cells
      for .NET license or a free evaluation key. * The Excel file you want to convert
      (`input.xlsx` in the examples).'
  - name: Full runnable program
    text: 'Putting the pieces together, here is a complete, self‑contained console
      application:'
  - name: Verify programmatically
    text: 'You can read the generated file back into memory to confirm that the export
      succeeded:'
  - name: Common edge cases
    text: '| Situation | What to watch for | Recommended fix | |----------------------------------------|---------------------------------------------------|-----------------|
      | Cells contain formulas | The exported value is the **calculated result**,
      not the formula text. | Ensure the workbook is fully calcul'
  - name: What’s next?
    text: '* Try exporting to CSV (`CsvSaveOptions`) for Excel‑compatible comma‑separated
      files. * Explore the `PdfSaveOptions` class to **export Excel to PDF** in a
      single line. * Combine multiple worksheets into one text file by iterating over
      `workbook.Worksheets`.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Text export
title: Cara menyimpan Excel sebagai teks dengan Aspose.Cells – panduan langkah demi
  langkah
url: /id/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyimpan Excel sebagai teks dengan Aspose.Cells – panduan langkah demi langkah

Jika Anda perlu **menyimpan Excel sebagai teks** dengan cepat, tutorial ini menunjukkan secara tepat cara melakukannya di C# dengan Aspose.Cells. Anda akan melihat cara **mengonversi Excel ke txt**, mengontrol presisi numerik, dan menangani kasus tepi umum—semua dalam satu contoh yang dapat dijalankan.

Di bagian-bagian berikut Anda akan mempelajari alur kerja lengkap, mulai dari menginstal pustaka hingga memverifikasi file output. Tidak diperlukan dokumentasi eksternal; semua yang Anda butuhkan sudah disertakan di sini.

## Apa yang akan Anda capai

* Memuat workbook `.xlsx` apa pun dari disk.  
* Mengonfigurasi `TxtSaveOptions` untuk membatasi jumlah digit signifikan.  
* **Mengekspor XLSX ke txt** dengan satu panggilan `Save`.  
* Memahami cara memecahkan masalah format ketika Anda **membuat txt dari Excel**.

### Prasyarat

* .NET 6.0 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.7.2+).  
* Familiaritas dasar dengan C# dan Visual Studio (atau IDE .NET apa pun).  
* Lisensi aktif Aspose.Cells untuk .NET atau kunci evaluasi gratis.  
* File Excel yang ingin Anda konversi (`input.xlsx` dalam contoh).

> **Pro tip:** Jika Anda berencana menjalankan ini di server, simpan file lisensi di lokasi yang aman dan muat sekali saat aplikasi dimulai.

## Langkah 1: Siapkan lingkungan pengembangan

1. Buat proyek konsol baru:

   ```bash
   dotnet new console -n ExcelToTxtDemo
   cd ExcelToTxtDemo
   ```

2. Tambahkan paket NuGet Aspose.Cells:

   ```bash
   dotnet add package Aspose.Cells
   ```

   Ini mengambil versi stabil terbaru (per 2026‑10‑10 versi 23.9).

3. (Opsional) Jika Anda memiliki file lisensi, letakkan `Aspose.Cells.lic` di root proyek dan tambahkan kode berikut di awal `Program.cs`:

   ```csharp
   // Load Aspose.Cells license (required for production use)
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Cells.lic");
   ```

   Memuat lisensi menghapus watermark evaluasi dan menonaktifkan batas ukuran.

## Langkah 2: Muat workbook Excel

Baris fungsional pertama membuat instance `Workbook` yang mewakili seluruh file Excel.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Load the workbook you want to convert
        var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
        // Continue with export logic...
    }
}
```

**Mengapa ini penting:** `Workbook` mengabstraksi lembar, sel, formula, dan format. Dengan memuat file sekali, Anda menjaga konversi tetap cepat dan efisien memori.

## Langkah 3: Konfigurasikan TxtSaveOptions untuk kontrol digit yang tepat

Saat Anda **mengonversi Excel ke txt**, nilai numerik dapat memiliki banyak tempat desimal. `TxtSaveOptions` memungkinkan Anda membatasi output ke jumlah digit signifikan tertentu, yang sering diperlukan untuk sistem hilir yang mengharapkan teks lebar tetap.

```csharp
// Step 3: Create and configure TxtSaveOptions
var txtOptions = new TxtSaveOptions
{
    // Keep only 5 significant digits (e.g., 123.45678 → 123.46)
    SignificantDigits = 5,

    // Optional: Use tab as the delimiter for column separation
    Separator = "\t",

    // Optional: Export only the first worksheet
    ExportActiveWorksheetOnly = true
};
```

**Penjelasan:**  
* `SignificantDigits` memotong noise floating‑point sambil mempertahankan presisi yang cukup untuk kebanyakan perhitungan bisnis.  
* `Separator` defaultnya spasi; mengaturnya ke `\t` (tab) membuat file yang dihasilkan lebih mudah diimpor ke basis data atau spreadsheet.  
* `ExportActiveWorksheetOnly` mencegah ekspor tidak sengaja lembar tersembunyi, yang dapat memperbesar file teks.

## Langkah 4: Ekspor XLSX ke txt dengan opsi yang dikonfigurasi

Sekarang Anda memiliki semua yang diperlukan untuk **menyimpan Excel sebagai teks**. Metode `Save` menulis representasi teks biasa ke jalur target.

```csharp
// Step 4: Save the workbook as a plain‑text file
workbook.Save(@"YOUR_DIRECTORY\output.txt", txtOptions);
Console.WriteLine("Export completed: output.txt");
```

File `output.txt` yang dihasilkan akan berisi baris nilai yang dipisahkan tab, setiap sel ditampilkan sebagai teks biasa sesuai opsi yang Anda atur.

### Program lengkap yang dapat dijalankan

Menggabungkan semua bagian, berikut adalah aplikasi konsol lengkap yang berdiri sendiri:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load license if you have one (remove comments if not needed)
        // var license = new License();
        // license.SetLicense("Aspose.Cells.lic");

        // 1️⃣ Load the Excel workbook
        var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Configure TxtSaveOptions
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5,
            Separator = "\t",
            ExportActiveWorksheetOnly = true
        };

        // 3️⃣ Export XLSX to TXT
        workbook.Save(@"YOUR_DIRECTORY\output.txt", txtOptions);

        Console.WriteLine("✅ Excel workbook successfully saved as text at: output.txt");
    }
}
```

**Expected output** (console):

```
✅ Excel workbook successfully saved as text at: output.txt
```

**Resulting `output.txt` sample** (first three rows):

```
Name    Age     Salary
Alice   30      55000
Bob     27      47000
```

Angka dibulatkan ke lima digit signifikan, dan kolom dipisahkan oleh tab.

## Langkah 5: Verifikasi output dan tangani kasus tepi

### Verifikasi secara programatik

Anda dapat membaca file yang dihasilkan kembali ke memori untuk memastikan bahwa ekspor berhasil:

```csharp
string[] lines = File.ReadAllLines(@"YOUR_DIRECTORY\output.txt");
if (lines.Length > 0)
{
    Console.WriteLine("First line of the txt file:");
    Console.WriteLine(lines[0]);
}
```

### Kasus tepi umum

| Situasi                               | Hal yang perlu diperhatikan                                 | Perbaikan yang disarankan |
|---------------------------------------|-------------------------------------------------------------|---------------------------|
| Sel berisi formula                    | Nilai yang diekspor adalah **hasil perhitungan**, bukan teks formula. | Pastikan workbook dihitung sepenuhnya (`workbook.CalculateFormula();`) sebelum menyimpan. |
| Tanggal muncul sebagai nomor seri     | Excel menyimpan tanggal sebagai angka; mereka mungkin terlihat seperti `44745`. | Atur `txtOptions.ConvertDateTime = true;` untuk memaksa format tanggal yang dapat dibaca manusia. |
| Lembar kerja besar (>10 000 baris)   | Konsumsi memori dapat meningkat tajam.                     | Gunakan `txtOptions.ExportAllSheets = false;` dan proses lembar kerja secara individual. |
| Karakter Unicode (mis., emoji)       | Encoding default adalah UTF‑8; sistem lama mungkin mengharapkan ANSI. | Atur `txtOptions.Encoding = Encoding.GetEncoding("windows-1252");` jika diperlukan. |

Dengan mengantisipasi skenario ini Anda dapat **membuat txt dari Excel** secara andal di berbagai set data.

## Kesimpulan

Anda sekarang tahu cara **menyimpan Excel sebagai teks** menggunakan Aspose.Cells untuk .NET, mulai dari memuat workbook hingga mengonfigurasi `TxtSaveOptions` dan akhirnya **mengekspor XLSX ke txt**. Contoh ini menunjukkan jalur kode lengkap, menjelaskan alasan di balik setiap pengaturan, dan mencakup jebakan umum saat Anda **mengonversi Excel ke txt**.

### Apa selanjutnya?

* Coba mengekspor ke CSV (`CsvSaveOptions`) untuk file yang kompatibel dengan Excel berformat koma‑dipisahkan.  
* Jelajahi kelas `PdfSaveOptions` untuk **mengekspor Excel ke PDF** dalam satu baris.  
* Gabungkan beberapa lembar kerja menjadi satu file teks dengan mengiterasi `workbook.Worksheets`.  

Silakan bereksperimen dengan opsi—mengubah pemisah, presisi, atau pemilihan lembar kerja—untuk menyesuaikan alur kerja spesifik Anda.

Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Menyimpan Excel sebagai File Teks dengan Pemisah Kustom menggunakan Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Menyimpan Excel sebagai txt – Panduan C# Lengkap untuk Mengekspor Angka dengan Digit Signifikan](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/)
- [Cara Menyimpan File Excel dalam Berbagai Format Menggunakan Aspose.Cells .NET (Panduan 2023)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}