---
category: general
date: 2026-10-01
description: Pelajari cara menyematkan font dalam HTML saat mengonversi Excel ke HTML
  menggunakan Aspose.Cells. Ekspor Excel sebagai HTML dengan font yang disematkan
  dalam beberapa langkah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: id
lastmod: 2026-10-01
og_description: Cara menyematkan font dalam HTML saat mengekspor file Excel. Ikuti
  panduan langkah demi langkah ini untuk mengonversi Excel ke HTML dengan font yang
  disematkan.
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: Cara menyematkan font di HTML dari Excel – Panduan Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: Cara menyematkan font saat mengonversi Excel ke HTML dengan Aspose.Cells
url: /id/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyematkan font saat mengonversi Excel ke HTML dengan Aspose.Cells

Menyematkan font dalam HTML saat mengonversi workbook Excel sangat penting untuk mempertahankan tampilan asli di berbagai browser. Jika Anda perlu mengonversi Excel ke HTML sambil menjaga font khusus tetap utuh, panduan ini menunjukkan proses lengkapnya. Anda juga akan melihat cara mengekspor Excel sebagai HTML dan mengapa menyematkan font dalam HTML penting untuk rendering yang konsisten.

Tutorial ini mencakup semua yang perlu Anda ketahui: pustaka yang diperlukan, konfigurasi kode, dan verifikasi file HTML yang dihasilkan. Pada akhir tutorial, Anda akan dapat mengekspor Excel sebagai HTML dengan font yang disematkan hanya dengan beberapa baris C#.

## Apa yang Anda perlukan

Sebelum memulai, pastikan Anda memiliki:

* **.NET 6.0 atau yang lebih baru** – kode menargetkan .NET 6, tetapi versi .NET apa pun yang mendukung Aspose.Cells dapat digunakan.
* **Aspose.Cells untuk .NET** – dapatkan lisensi atau gunakan versi evaluasi gratis dari situs web Aspose.
* Lingkungan pengembangan **C#** (Visual Studio, Rider, atau VS Code) – IDE apa pun yang dapat mengompilasi proyek .NET.
* Sebuah workbook Excel (`Styled.xlsx`) yang menggunakan font khusus yang ingin Anda pertahankan.

## Langkah 1: Siapkan Aspose.Cells di proyek .NET Anda

Pertama, tambahkan paket NuGet Aspose.Cells ke proyek Anda:

```bash
dotnet add package Aspose.Cells
```

Kemudian sertakan namespace di bagian atas file C# Anda:

```csharp
using Aspose.Cells;
```

Menambahkan paket membuat kelas `Workbook`, `HtmlSaveOptions`, dan kelas terkait lainnya tersedia.

## Langkah 2: Muat workbook Excel

Memuat workbook adalah langkah konkret pertama dalam **cara mengekspor data Excel**. Konstruktor `Workbook` membaca file dari disk:

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*Mengapa ini penting:* Aspose.Cells mem-parsing workbook, termasuk gaya sel, formula, dan informasi font. Jika file tidak ditemukan, akan dilemparkan pengecualian, jadi pastikan jalurnya benar.

## Langkah 3: Konfigurasi opsi penyimpanan HTML untuk menyematkan font

Inti dari **menyematkan font dalam html** adalah kelas `HtmlSaveOptions`. Atur `EmbedFonts` ke `true` sehingga setiap font yang digunakan dalam workbook ditulis ke output HTML sebagai aturan `@font-face` yang dienkode Base64.

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*Mengapa ini penting:* Secara default Aspose.Cells merujuk ke file font eksternal, yang mungkin tidak tersedia di mesin klien. Mengaktifkan `EmbedFonts` menjamin bahwa HTML yang dirender terlihat identik dengan lembar Excel asli, terlepas dari font yang terpasang pada perangkat pengguna.

### Kasus khusus: font yang tidak didukung

Jika workbook menggunakan font yang tidak terpasang di server, Aspose.Cells akan beralih ke font sistem default. Untuk menghindari hal ini, pasang font yang diperlukan di server atau sematkan secara manual setelah ekspor.

## Langkah 4: Simpan workbook sebagai HTML menggunakan opsi yang telah dikonfigurasi

Sekarang Anda dapat menulis file HTML. Metode `Save` menerima jalur output dan instance `HtmlSaveOptions`:

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

Setelah dieksekusi, `Styled.html` berisi data spreadsheet dan blok `<style>` dengan definisi `@font-face` yang dienkode Base64 untuk setiap font khusus.

## Langkah 5: Verifikasi font yang disematkan

Buka `Styled.html` di browser. Periksa bagian `<head>`; Anda harus melihat sesuatu seperti:

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

Jika font muncul dengan benar di tabel yang dirender, penyematan berhasil. Jika Anda melihat glyph yang hilang, periksa kembali bahwa file font sumber terpasang di mesin yang menjalankan konversi.

## Variasi umum dan opsi tambahan

### Mengonversi beberapa lembar kerja

Jika Anda perlu **mengonversi Excel ke HTML** untuk semua lembar kerja, atur `ExportActiveWorksheetOnly = false` (nilai default). Aspose.Cells akan membuat file HTML terpisah untuk setiap lembar.

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### Mengontrol output CSS

Anda dapat mengurangi ukuran HTML dengan menonaktifkan CSS inline:

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### Menggunakan stream alih-alih file

Saat mengintegrasikan ke API web, tulis HTML ke `MemoryStream` dan kembalikan secara langsung:

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## Tips pro: Lisensikan produk untuk menghapus watermark evaluasi

Jika Anda menggunakan versi evaluasi, HTML yang dihasilkan mungkin berisi komentar watermark. Terapkan lisensi Aspose.Cells Anda sebelum memuat workbook untuk menghasilkan output bersih:

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat dijalankan yang mendemonstrasikan **cara menyematkan font**, **mengonversi excel ke html**, dan **mengekspor excel sebagai html** dalam satu langkah:

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**Output yang diharapkan:** Setelah menjalankan program, `Styled.html` muncul di `YOUR_DIRECTORY`. Membuka file tersebut di browser modern apa pun menampilkan spreadsheet dengan font yang sama seperti di file Excel asli, bahkan pada mesin yang tidak memiliki font tersebut.

## Kesimpulan

Anda kini tahu **cara menyematkan font** ketika **mengonversi Excel ke HTML** menggunakan Aspose.Cells, dan Anda telah melihat alur lengkap mulai dari memuat workbook hingga memverifikasi font yang disematkan. Pendekatan ini memastikan fidelitas visual file Excel Anda tetap terjaga dalam HTML yang dihasilkan, menjadikannya ideal untuk pelaporan web, buletin email, atau skenario apa pun di mana Anda harus **mengekspor Excel sebagai HTML** dengan tipografi khusus.

Selanjutnya, jelajahi topik terkait seperti **mengekspor Excel sebagai PDF**, **menata output HTML dengan CSS khusus**, atau **memproses batch beberapa workbook**. Semua ini dibangun di atas pola `HtmlSaveOptions` yang sama, sehingga Anda dapat menyesuaikan kode dengan perubahan minimal.

Selamat coding!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang sangat terkait dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Export Excel to HTML – Step‑by‑Step Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [How to Embed Fonts in HTML – Complete C# Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [How to embed fonts when converting Excel to PDF – Step‑by‑Step Guide](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}