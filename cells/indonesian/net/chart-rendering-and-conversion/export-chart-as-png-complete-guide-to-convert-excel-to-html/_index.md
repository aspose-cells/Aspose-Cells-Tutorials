---
category: general
date: 2026-06-30
description: Ekspor diagram sebagai PNG saat Anda mengonversi Excel ke HTML menggunakan
  Aspose.Cells. Pelajari cara menyematkan gambar sebagai Base64 dan menyimpan buku
  kerja sebagai HTML dalam hitungan menit.
draft: false
keywords:
- export chart as png
- convert excel to html
- embed images as base64
- save workbook as html
- export excel chart to png
language: id
og_description: Ekspor diagram sebagai PNG dan sematkan gambar sebagai Base64 saat
  mengonversi Excel ke HTML. Ikuti tutorial C# langkah demi langkah ini untuk menyimpan
  workbook sebagai HTML dengan mudah.
og_title: Ekspor Grafik sebagai PNG – Konversi Excel ke HTML dengan Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  headline: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  name: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  steps:
  - name: Open Visual Studio and create a new **Console App** (`dotnet new console`).
    text: Open Visual Studio and create a new **Console App** (`dotnet new console`).
  - name: 'Add the Aspose.Cells NuGet package:'
    text: 'Add the Aspose.Cells NuGet package:'
  - name: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
    text: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
  - name: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
    text: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
  - name: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
    text: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
  - name: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
    text: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Ekspor Grafik sebagai PNG – Panduan Lengkap Mengonversi Excel ke HTML dengan
  Aspose.Cells
url: /id/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor Diagram sebagai PNG – Panduan Lengkap Mengonversi Excel ke HTML dengan Aspose.Cells

Pernah bertanya-tanya bagaimana cara **export chart as PNG** langsung dari workbook Excel sekaligus mengubah seluruh lembar menjadi HTML yang bersih dan responsif? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan ketika mereka membutuhkan laporan siap web yang menampilkan diagram tanpa harus mengelola file gambar terpisah. Kabar baiknya, Aspose.Cells membuat ini menjadi sangat mudah.

Dalam tutorial ini kami akan memandu Anda melalui langkah‑langkah tepat untuk **convert Excel to HTML**, **embed images as Base64**, dan akhirnya **save workbook as HTML**—semua sambil memastikan setiap diagram disimpan sebagai gambar PNG. Pada akhir tutorial, Anda akan memiliki satu file HTML yang dapat Anda sisipkan ke halaman web mana pun, dan setiap diagram akan muncul secara langsung, tanpa memerlukan aset tambahan.

## Apa yang Akan Anda Pelajari

- Cara memuat workbook yang sudah ada dan sudah berisi diagram.  
- Flag `HtmlSaveOptions` mana yang mengontrol ekspor gambar, format diagram, dan responsivitas.  
- Kode tepat yang diperlukan untuk **export chart as PNG** dan menyematkan PNG tersebut sebagai string Base64.  
- Cara **save workbook as HTML** dengan satu pemanggilan metode.  
- Tips untuk memecahkan masalah umum, seperti gambar diagram yang hilang atau string Base64 yang terlalu besar.  

**Prasyarat:**  
- .NET 6+ (atau .NET Framework 4.6+) terinstal.  
- Lisensi Aspose.Cells yang valid (atau kunci evaluasi sementara).  
- Pemahaman dasar tentang C# dan Visual Studio (atau IDE favorit Anda).  

Jika ada yang belum familiar, berhentilah sejenak dan siapkan dulu; sisanya panduan mengasumsikan semuanya sudah siap.

---

## Langkah 1: Siapkan Proyek Anda dan Instal Aspose.Cells

Sebelum kita dapat **export chart as PNG**, kita memerlukan proyek C# yang mereferensikan pustaka Aspose.Cells.

1. Buka Visual Studio dan buat **Console App** baru (`dotnet new console`).  
2. Tambahkan paket NuGet Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

3. (Opsional) Jika Anda memiliki file lisensi, letakkan di root proyek dan aktifkan pada runtime:

```csharp
// Activate license – skip this line if you’re using the trial version
Aspose.Cells.License license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

> **Pro tip:** Simpan file lisensi di luar kontrol sumber. Gunakan variabel lingkungan atau penyimpanan rahasia yang aman untuk produksi.

---

## Langkah 2: Muat Workbook yang Berisi Diagram

Sekarang kami akan memuat file Excel yang sudah memiliki diagram yang ingin kami **export chart as PNG**.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;   // Needed for ImageFormat enum

// Path to the source workbook – change this to your actual file location
string sourcePath = @"C:\Reports\ReportWithChart.xlsx";

// Load the workbook
Workbook workbook = new Workbook(sourcePath);
```

> **Mengapa ini penting:** Memuat workbook lebih awal memberi kami akses ke semua lembar kerja, diagram, dan objek yang disematkan. Jika workbook gagal dimuat, langkah **export chart to PNG** berikutnya tidak akan pernah dijalankan.

---

## Langkah 3: Konfigurasikan HTML Save Options

The heart of the solution lives in `HtmlSaveOptions`. By toggling a few properties we can:

- **ExportChartImageFormat = ImageFormat.Png** → memastikan setiap diagram menjadi PNG.  
- **ExportImagesAsBase64 = true** → menyematkan data PNG langsung ke dalam HTML, menghilangkan file eksternal.  
- **IsResponsive = true** → membuat tabel yang dihasilkan menyesuaikan diri dengan layar ponsel.  
- **ExportPrintingHeadersFooters = false** → menghapus metadata printer yang tidak diperlukan.  

Here’s the full configuration:

```csharp
// Create HTML save options and fine‑tune them
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // 1️⃣ Embed PNG/JPEG images directly as Base64 strings
    ExportImagesAsBase64 = true,

    // 2️⃣ Force chart images to be saved as PNG files
    ExportChartImageFormat = ImageFormat.Png,

    // 3️⃣ Omit printing headers/footers for a cleaner web view
    ExportPrintingHeadersFooters = false,

    // 4️⃣ Generate responsive tables for mobile friendliness
    IsResponsive = true,

    // 5️⃣ Target modern browsers with HTML5
    HtmlVersion = HtmlVersion.Html5
};
```

### Mengapa Pengaturan Ini?

- **ExportChartImageFormat = ImageFormat.Png** adalah satu‑satunya cara untuk menjamin gambar diagram yang lossless dan aman untuk web.  
- **ExportImagesAsBase64 = true** berarti Anda dapat **embed images as Base64**, yang sempurna untuk laporan email atau penyebaran satu‑file.  
- **IsResponsive = true** menyelesaikan keluhan umum: tabel yang meluap pada smartphone.  
- **ExportPrintingHeadersFooters = false** membuat HTML ringan—tanpa info printer tersembunyi yang tidak pernah dipakai di web.  

---

## Langkah 4: Simpan Workbook sebagai HTML

Dengan opsi yang sudah diatur, baris terakhir adalah satu pemanggilan yang sekaligus **convert excel to html** dan **export chart as PNG** di balik layar.

```csharp
// Destination HTML file – adjust the folder as needed
string outputPath = @"C:\Reports\Report.html";

// Save the workbook using the configured options
workbook.Save(outputPath, htmlOptions);
```

When this line finishes, you’ll have a file called `Report.html`. Open it in any browser, and you’ll see:

- Semua data lembar kerja ditampilkan sebagai tabel HTML yang bersih.  
- Setiap diagram ditampilkan sebagai gambar PNG inline (berkat penyematan Base64).  
- Tidak ada file gambar tambahan yang berada di samping HTML.  

### Output yang Diharapkan

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Report</title>
    <style>
        /* Aspose.Cells generated responsive CSS */
    </style>
</head>
<body>
    <table class="aspose">
        <!-- Table rows here -->
    </table>

    <!-- Example of an embedded chart image -->
    <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA..." alt="Chart 1" />
</body>
</html>
```

Perhatikan atribut `src="data:image/png;base64,..."`—itu adalah keajaiban **embed images as base64** yang bekerja. Tidak ada file `.png` terpisah yang dibuat di disk.

---

## Langkah 5: Verifikasi Ekspor PNG dan Sesuaikan Jika Diperlukan

Kadang-kadang diagram dapat terlihat agak tidak tepat setelah konversi, terutama jika menggunakan font khusus atau gradien kompleks. Berikut cara memeriksanya dua kali:

1. Buka HTML yang dihasilkan di Chrome. Klik kanan gambar diagram dan pilih **Open image in new tab**. URL masih akan dimulai dengan `data:image/png;base64,`.  
2. Jika gambar terlihat buram, pertimbangkan meningkatkan resolusi diagram sebelum menyimpan:

```csharp
htmlOptions.ImageResolution = 300; // DPI – higher values = sharper PNGs
```

3. Untuk diagram yang bergantung pada sumber data eksternal, pastikan workbook sudah sepenuhnya diperbarui sebelum menyimpan:

```csharp
workbook.CalculateFormula(); // Force recalculation
```

Penyesuaian ini memastikan bahwa langkah **export excel chart to png** menghasilkan grafik yang tajam dan siap produksi.

---

## Langkah 6: Sebarkan HTML ke Mana Saja

Karena semua gambar disematkan, Anda dapat sekarang:

- Kirim HTML lewat email sebagai satu lampiran.  
- Tempel HTML ke dalam CMS yang menerima kode mentah.  
- Host di situs statis tanpa khawatir file PNG yang hilang.  

Jika Anda pernah membutuhkan file PNG sebagai aset terpisah (mungkin untuk PDF nanti), Anda dapat mengubah `ExportImagesAsBase64` menjadi `false` dan mengarahkan `HtmlSaveOptions` ke folder output untuk gambar.

```csharp
htmlOptions.ExportImagesAsBase64 = false;
htmlOptions.ImageFolder = @"C:\Reports\Images";
```

Sekarang HTML akan merujuk ke file PNG eksternal, tetap memastikan **export chart as png** tetapi memberi Anda file gambar terpisah untuk penggunaan lain.

---

## Kesulitan Umum & Cara Menghindarinya

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| Chart missing from HTML | `ExportChartImageFormat` dibiarkan default (`Jpeg`) dan browser memblokir konten campuran. | Set `ExportChartImageFormat = ImageFormat.Png`. |
| File HTML sangat besar (beberapa MB) | Diagram besar atau banyak gambar resolusi tinggi yang disematkan sebagai Base64. | Kurangi `htmlOptions.ImageResolution` atau kompres diagram di Excel sebelum konversi. |
| Tabel meluap di ponsel | `IsResponsive` tidak diaktifkan. | Pastikan `IsResponsive = true` di `HtmlSaveOptions`. |
| String Base64 mengandung karakter newline | Versi .NET lama dapat membungkus string panjang. | Tingkatkan ke .NET 6+ atau set `htmlOptions.ExportBase64StringInOneLine = true`. |

---

## Bonus: Bungkus Semua dalam Metode yang Dapat Digunakan Kembali

Jika Anda akan melakukan konversi ini berulang kali, enkapsulasi logikanya:

```csharp
public static void ConvertExcelToHtmlWithPngCharts(string excelPath, string htmlPath)
{
    // Load workbook
    Workbook wb = new Workbook(excelPath);

    // Prepare options
    HtmlSaveOptions opts = new HtmlSaveOptions
    {
        ExportImagesAsBase64 = true,
        ExportChartImageFormat = ImageFormat.Png,
        ExportPrintingHeadersFooters = false,
        IsResponsive = true,
        HtmlVersion = HtmlVersion.Html5,
        ImageResolution = 150 // reasonable default DPI
    };

    // Force recalculation for up‑to‑date charts
    wb.CalculateFormula();

    // Save as HTML
    wb.Save(htmlPath, opts);
}
```

Sekarang Anda dapat memanggil `ConvertExcelToHtmlWithPngCharts(@"C:\Reports\MyFile.xlsx", @"C:\Reports\MyFile.html");` dari mana saja dalam basis kode Anda.

---

## Kesimpulan

Anda baru saja menguasai cara **export chart as PNG** sambil **convert Excel to HTML**, **embed images as Base64**, dan **save workbook as HTML** menggunakan Aspose.Cells. Inti pentingnya adalah beberapa pengaturan `HtmlSaveOptions` yang dipilih dengan tepat memberi Anda satu file HTML yang mandiri dan berisi semua yang berfungsi di perangkat apa pun—tanpa file PNG tambahan, tanpa folder berantakan.

Siap untuk tantangan berikutnya? Cobalah menggabungkan pendekatan ini dengan **export excel chart to PNG** untuk pembuatan PDF, atau bereksperimen dengan CSS khusus untuk menata tabel lebih lanjut. Langit adalah batasnya ketika Anda mengendalikan data dan presentasi secara programatis.

Jangan ragu meninggalkan komentar jika Anda mengalami kendala, atau bagikan bagaimana Anda menyesuaikan pola ini dalam proyek Anda sendiri. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Ekspor Excel ke HTML Menggunakan Aspose.Cells untuk .NET: Panduan Lengkap](/cells/english/net/workbook-operations/export-excel-html-aspose-cells-net/)
- [Ekspor Excel ke HTML Tanpa Skrip Frame Menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/export-excel-to-html-aspose-cells-net/)
- [Cara Mengekspor Worksheet Excel ke PNG Menggunakan Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}