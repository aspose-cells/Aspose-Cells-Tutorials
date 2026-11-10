---
category: general
date: 2026-10-13
description: Pelajari cara menyimpan Excel sebagai TXT dengan Aspose.Cells. Panduan
  ini mencakup mengekspor Excel ke TXT, menulis nilai ke sel, dan mengatur digit signifikan
  dalam beberapa langkah saja.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: id
lastmod: 2026-10-13
og_description: Simpan Excel sebagai TXT dengan Aspose.Cells. Pelajari cara mengekspor
  Excel ke TXT, menulis nilai ke sel, dan mengatur digit signifikan hanya dengan beberapa
  baris kode C#.
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: Simpan Excel sebagai TXT – panduan langkah demi langkah untuk pengembang
  .NET
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: Cara menyimpan Excel sebagai TXT menggunakan Aspose.Cells di C#
url: /id/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyimpan Excel sebagai TXT menggunakan Aspose.Cells di C#

Jika Anda perlu **save Excel as TXT** dengan cepat, tutorial ini menunjukkan proses lengkap dalam waktu kurang dari lima menit. Anda akan melihat cara mengekspor Excel ke TXT, menulis nilai ke sel, dan mengatur digit signifikan sehingga file teks berisi data persis seperti yang Anda harapkan.

Mengekspor spreadsheet sebagai TXT berguna ketika sistem hilir hanya menerima input teks biasa, ketika Anda perlu menghasilkan log, atau ketika Anda menginginkan dump perhitungan yang dapat dibaca manusia. Contoh di bawah ini bekerja dengan Aspose.Cells v25.10 atau yang lebih baru dan berjalan pada runtime .NET 6+ apa pun.

## Prasyarat

Sebelum Anda mulai, pastikan Anda memiliki:

* Salinan berlisensi **Aspose.Cells for .NET** (versi percobaan gratis dapat digunakan untuk pengujian).
* .NET 6 SDK atau yang lebih baru terpasang.
* IDE seperti Visual Studio 2022, VS Code, atau Rider.
* Pengetahuan dasar C#—tidak diperlukan pengalaman otomatisasi Excel tingkat lanjut.

Anda dapat menginstal paket NuGet Aspose.Cells dengan:

```bash
dotnet add package Aspose.Cells
```

## Langkah 1: Buat workbook dan akses worksheet pertama (save excel as txt)

Hal pertama yang Anda lakukan ketika ingin **save Excel as TXT** adalah membuat objek `Workbook`. Objek ini mewakili seluruh file Excel dalam memori.

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Mengapa ini penting:** Kelas `Workbook` adalah titik masuk untuk semua operasi spreadsheet. Dengan memulai dari workbook baru Anda menghindari format tersembunyi yang dapat memengaruhi output teks biasa.

## Langkah 2: Tulis angka presisi tinggi ke dalam sel (write value to cell)

Sekarang Anda perlu **write value to cell** A1. Metode `PutValue` secara otomatis mendeteksi tipe data dan menyimpannya sebagai nilai numerik.

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **Tip:** Jika Anda nanti perlu menulis string, tanggal, atau formula, metode `PutValue` yang sama tetap berfungsi—cukup berikan tipe .NET yang sesuai.

## Langkah 3: Konfigurasikan opsi ekspor untuk mempertahankan hanya presisi yang dibutuhkan (set significant digits)

Saat mengekspor ke file TXT, Anda sering ingin membatasi jumlah digit untuk menjaga ukuran file tetap kecil atau agar sesuai dengan spesifikasi hilir. Kelas `TxtSaveOptions` menyediakan properti `SignificantDigits` untuk tujuan ini.

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **Mengapa Anda harus mengatur digit signifikan:** Tanpa pengaturan ini, Aspose.Cells menulis nilai double‑precision penuh, yang dapat menghasilkan string panjang seperti `12345.6789012345`. Mengatur `SignificantDigits = 6` memotong output menjadi `12345.7`, yang cocok dengan sebagian besar kebutuhan pelaporan.

## Langkah 4: Ekspor workbook sebagai file TXT (export excel to txt)

Akhirnya, Anda **export Excel to TXT** dengan memanggil `Workbook.Save` menggunakan opsi yang telah dikonfigurasi sebelumnya.

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

Saat kode selesai, `LimitedDigits.txt` berisi:

```
12345.7
```

> **Verifikasi hasil:** Buka file di editor teks apa pun (Notepad, VS Code) untuk memastikan hanya enam digit signifikan yang ada dan tidak ada koma atau pemisah tab tambahan.

## Contoh lengkap yang dapat dijalankan

Berikut adalah aplikasi konsol mandiri yang dapat Anda salin, tempel, dan jalankan segera.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**Penjelasan setiap blok**

| Blok | Tujuan |
|------|--------|
| `using Aspose.Cells;` | Mengimpor namespace Aspose.Cells yang diperlukan untuk `Workbook`, `Worksheet`, dan `TxtSaveOptions`. |
| `Workbook workbook = new Workbook();` | Membuat instance workbook Excel kosong di memori. |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 dengan angka double‑precision. |
| `TxtSaveOptions` | Mengonfigurasi perilaku **set significant digits** untuk ekspor TXT. |
| `workbook.Save(..., txtOptions);` | Menjalankan operasi **export excel to txt**, membuat file teks biasa. |

## Kasus tepi dan tips tambahan

| Skenario | Cara menangani |
|----------|----------------|
| **Large worksheets** (banyak baris/kolom) | Gunakan `txtOptions.Encoding = Encoding.UTF8` jika Anda membutuhkan dukungan Unicode, dan pertimbangkan streaming file dengan `Workbook.Save(Stream, txtOptions)` untuk menghindari penggunaan memori yang tinggi. |
| **Custom delimiters** (nilai dipisahkan koma) | `TxtSaveOptions` juga menyediakan `Separator`—atur ke `','` untuk menghasilkan output gaya CSV sambil tetap menggunakan format TXT. |
| **Preserving formulas** | Atur `txtOptions.ExportFormulas = true` untuk menulis teks formula alih-alih nilai yang dihitung. |
| **Locale‑specific decimal separators** | Sesuaikan `txtOptions.DecimalSeparator` menjadi `','` untuk locale Eropa. |
| **Multiple worksheets** | Iterasi melalui `workbook.Worksheets` dan panggil `Save` untuk masing‑masing, menambahkan nama worksheet ke nama file. |

## Pertanyaan yang sering diajukan

**Q: Apakah `SignificantDigits` membulatkan atau memotong?**  
A: Itu membulatkan ke nilai terdekat berdasarkan jumlah digit signifikan yang ditentukan, memastikan output secara matematis akurat pada presisi tersebut.

**Q: Bisakah saya mengekspor langsung ke memory stream?**  
A: Ya. Ganti path file dengan instance `MemoryStream`: `workbook.Save(stream, txtOptions);`. Ini berguna untuk API web yang perlu mengembalikan konten TXT tanpa menyentuh sistem file.

**Q: Bagaimana jika saya perlu mempertahankan format asli (mis., tanggal)?**  
A: Gunakan `txtOptions.ExportFormattedValues = true`. Ini memaksa Aspose.Cells menulis teks yang ditampilkan sel alih‑alih nilai mentah.

## Kesimpulan

Anda kini tahu cara **save Excel as TXT** dengan kontrol penuh atas presisi, format, dan lokasi output. Dengan mengikuti empat langkah—membuat workbook, **write value to cell**, **set significant digits**, dan **export Excel to TXT**—Anda dapat mengintegrasikan ekspor teks biasa ke dalam aplikasi .NET apa pun.

Selanjutnya, jelajahi topik terkait seperti **export spreadsheet as TXT with custom delimiters**, **convert Excel to CSV**, atau **use Aspose.Cells to generate JSON reports**. Masing‑masing membangun pada konsep inti yang sama yang ditunjukkan di sini, memberi Anda toolkit serbaguna untuk pertukaran data lintas platform.

Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun pada teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Simpan Excel sebagai Teks – Panduan C# Lengkap untuk Mengekspor Excel ke TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Buat Workbook Baru dan Ekspor Excel ke TXT dengan Presisi](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Buat workbook baru – Ekspor Excel ke TXT dengan Presisi Penuh](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}