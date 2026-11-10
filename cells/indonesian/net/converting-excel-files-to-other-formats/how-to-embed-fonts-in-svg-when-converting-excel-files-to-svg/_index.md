---
category: general
date: 2026-09-15
description: Pelajari cara menyematkan font dalam SVG dan mengekspor diagram Excel
  ke PowerPoint, mencakup mengonversi XLSX ke SVG dan mengonversi XLSX ke PPTX dengan
  contoh kode lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: id
lastmod: 2026-09-15
og_description: Sematkan font dalam SVG dan ekspor diagram Excel ke PowerPoint dengan
  kode C# langkah demi langkah. Konversi XLSX ke SVG dan XLSX ke PPTX dengan cepat
  dan andal.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: Menyematkan font dalam SVG dan mengekspor grafik Excel ke PowerPoint – panduan
  lengkap
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cara menyematkan font dalam SVG saat mengonversi file Excel ke SVG dan PowerPoint
url: /id/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyematkan font dalam SVG saat mengonversi file Excel ke SVG dan PowerPoint  

Jika Anda perlu **menyematkan font dalam SVG** saat mengonversi workbook Excel, panduan ini menunjukkan cara melakukannya secara tepat. Anda juga akan belajar cara **mengekspor diagram Excel ke PowerPoint**, serta cara **mengonversi XLSX ke SVG** dan **mengonversi XLSX ke PPTX** dengan diagram yang dapat diedit.  

Bekerja dengan data Excel secara programatik sering berarti Anda harus memindahkan konten visual yang sama antar format file yang berbeda. Membuat ulang diagram secara manual di PowerPoint atau menerapkan kembali font dalam SVG rawan kesalahan dan memakan waktu. Pada akhir tutorial ini Anda akan memiliki satu potongan kode C# yang dapat digunakan kembali yang:

* Menyimpan workbook sebagai file SVG dengan font yang disematkan dan selector variasi font.  
* Mengekspor workbook yang sama ke file PPTX di mana diagram tetap dapat diedit.  

Satu-satunya prasyarat adalah versi terbaru **Aspose.Cells for .NET** (2024‑x atau lebih baru) dan lingkungan pengembangan .NET seperti Visual Studio 2022.

---

## Apa yang Anda perlukan  

* .NET 6.0 atau lebih baru (kode juga berfungsi pada .NET Framework 4.8).  
* Paket NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  
* File Excel (`input.xlsx`) yang berisi setidaknya satu diagram.  
* Izin menulis ke direktori output.  

---

## Menyematkan font dalam SVG saat mengonversi XLSX ke SVG  

Menyematkan font memastikan bahwa SVG ditampilkan dengan benar pada perangkat apa pun, bahkan jika sistem target tidak memiliki jenis huruf asli. Kelas `SvgSaveOptions` menyediakan dua flag yang membuat ini memungkinkan: `EmbedFonts` dan `FontVariationSelectors`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**Mengapa ini berhasil:**  
* `EmbedFonts = true` menyalin file font ke dalam bagian `<defs>` SVG, menghilangkan ketergantungan eksternal.  
* `FontVariationSelectors = true` menambahkan selector yang diperlukan untuk font yang mendukung fitur OpenType, mempertahankan variasi glyph seperti ligatur.  

**Hasil yang diharapkan:** Buka `WithFonts.svg` di browser modern mana pun; teks di dalam diagram atau sel muncul dengan jenis huruf yang sama persis seperti di Excel, bahkan pada mesin yang tidak memiliki font tersebut terpasang.

---

## Mengekspor diagram Excel ke PowerPoint dengan diagram yang dapat diedit  

Ketika Anda perlu menyematkan diagram ke dalam slide PowerPoint tetapi tetap memungkinkan penerima mengedit data diagram, `PptxSaveOptions` milik Aspose.Cells menawarkan flag `ExportEditableChart`.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**Mengapa ini penting:**  
Menetapkan `ExportEditableChart` ke `true` menyimpan diagram sebagai objek diagram Office Open XML alih-alih gambar statis. Saat Anda membuka `EditableChart.pptx` di PowerPoint, Anda dapat klik kanan diagram → **Edit Data** dan memodifikasi seri seperti diagram PowerPoint asli.

**Langkah verifikasi:**  

1. Buka `EditableChart.pptx` di PowerPoint.  
2. Temukan slide yang berisi diagram.  
3. Pilih **Chart Tools → Design → Edit Data**.  
4. Pastikan grid data bergaya Excel muncul dan Anda dapat mengubah nilai.

---

## Mengonversi XLSX ke SVG – rangkuman alur kerja lengkap  

Berikut adalah versi ringkas yang menggabungkan pemuatan, manipulasi data opsional, dan penyimpanan sebagai SVG. Gunakan ini ketika Anda hanya memerlukan output SVG.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

Panggil metode tersebut seperti ini:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**Tips kasus tepi:** Jika workbook Anda berisi font khusus yang tidak terpasang di server, sematkan secara manual sebelum memanggil `Save`. Gunakan `FontInfoCollection` untuk menambahkan file font ke `SvgSaveOptions` melalui properti `CustomFonts` (tersedia pada rilis Aspose.Cells yang lebih baru).

---

## Mengonversi XLSX ke PPTX – mempertahankan kemampuan mengedit diagram  

Metode pembantu berikut menunjukkan jalur **convert XLSX to PPTX** sambil memastikan diagram tetap dapat diedit.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

Penggunaan:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**Pertanyaan umum:** *Bagaimana jika workbook saya memiliki beberapa lembar kerja dengan diagram?*  
**Jawaban:** Aspose.Cells mengekspor lembar kerja pertama secara default. Untuk menyertakan lembar tambahan, iterasi melalui `workbook.Worksheets`, salin setiap diagram ke slide baru, dan simpan setiap slide secara terpisah menggunakan objek `Presentation` dari Aspose.Slides. Skenario lanjutan ini berada di luar alur dasar “menyimpan workbook sebagai SVG” dan “mengekspor diagram Excel ke PowerPoint”, tetapi flag inti tetap sama.

---

## Tips praktis dan jebakan  

* **Kinerja:** Menyematkan font meningkatkan ukuran file SVG. Jika ukuran menjadi perhatian, setel `EmbedFonts = false` dan gunakan font web‑safe.  
* **Lisensi font:** Pastikan Anda memiliki hak untuk menyematkan font yang Anda gunakan; beberapa font komersial membatasi penyematan.  
* **Kompatibilitas diagram:** Diagram yang dapat diedit disimpan sebagai bagian `chart.xml` di dalam PPTX. Diagram yang sangat kompleks (misalnya, 3‑D atau diagram kombinasi) mungkin kehilangan sebagian styling saat diedit di PowerPoint. Uji tipe diagram paling umum yang Anda butuhkan.  
* **Ketidaksesuaian versi:** Flag `ExportEditableChart` memerlukan Aspose.Cells 20.10 atau lebih baru. Menggunakan versi yang lebih lama akan secara diam‑diam beralih ke gambar raster.  
* **Keamanan thread:** Objek Workbook tidak thread‑safe. Buat instance `Workbook` baru per permintaan dalam skenario layanan web.  

---

## Contoh lengkap end‑to‑end  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

Menjalankan program ini menghasilkan dua file:

* **WithFonts.svg** – SVG yang menampilkan persis seperti tampilan Excel, dengan font disertakan.  
* **EditableChart.pptx** – presentasi PowerPoint di mana diagram dapat diedit langsung.

---

## Kesimpulan  

Sekarang Anda tahu cara **menyematkan font dalam SVG** saat **mengonversi XLSX ke SVG**, dan cara **mengekspor diagram Excel ke PowerPoint** sambil mempertahankan kemampuan mengedit diagram. Kode yang sama juga menunjukkan cara **menyimpan workbook sebagai SVG** dan **mengonversi XLSX ke PPTX** dengan upaya minimal.  

Dari sini Anda dapat menjelajahi topik lebih lanjut seperti:

* Menambahkan font khusus secara programatik (`svgOptions.CustomFonts`).  
* Memproses batch banyak workbook dalam layanan latar belakang.  
* Menggunakan Aspose.Slides untuk membuat file PPTX multi‑slide yang menggabungkan beberapa diagram Excel.  

Cobalah opsi‑opsi tersebut, sesuaikan potongan kode dengan proyek Anda, dan nikmati konversi Excel‑to‑SVG/PPTX yang andal tanpa perlu pemrosesan manual. Selamat coding!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang berhubungan erat dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}