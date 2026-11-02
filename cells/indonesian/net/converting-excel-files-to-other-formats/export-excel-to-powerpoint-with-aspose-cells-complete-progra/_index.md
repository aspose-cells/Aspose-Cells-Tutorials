---
category: general
date: 2026-08-14
description: Ekspor Excel ke PowerPoint menggunakan Aspose.Cells dan pelajari cara
  menghitung formula Excel dalam kode. Contoh C# langkah demi langkah dengan sumber
  lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: id
lastmod: 2026-08-14
og_description: Ekspor Excel ke PowerPoint dengan Aspose.Cells dan hitung rumus Excel
  dalam kode. Ikuti panduan lengkap ini untuk menghasilkan file PPTX yang dapat diedit
  dari buku kerja.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Ekspor Excel ke PowerPoint dengan Aspose.Cells – tutorial lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Ekspor Excel ke PowerPoint dengan Aspose.Cells – panduan pemrograman lengkap
url: /id/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel ke PowerPoint dengan Aspose.Cells – panduan pemrograman lengkap

Jika Anda perlu **mengekspor Excel ke PowerPoint** secara programatis, panduan ini menunjukkan secara tepat cara melakukannya dengan Aspose.Cells untuk .NET. Anda juga akan belajar cara **menghitung rumus Excel dalam kode**, menyalin tabel pivot tanpa kehilangan definisinya, dan menggunakan fungsi Office‑365 EXPAND yang baru untuk array dinamis.

Pada bagian berikut kami akan membahas contoh C# dunia nyata, menjelaskan mengapa setiap baris penting, dan menguraikan jebakan umum sehingga Anda dapat menyesuaikan solusi ini untuk proyek Anda sendiri.

## Apa yang dibahas dalam tutorial ini

* Memuat workbook yang ada (`input.xlsx`)  
* Menyalin rentang yang berisi tabel pivot sambil mempertahankan definisinya  
* Mengekspor workbook ke file PowerPoint (`.pptx`) dengan kotak teks dan bentuk yang dapat diedit  
* Mengekspor rentang sel sebagai string menggunakan logika khusus  
* Menghitung rumus Excel dalam kode, termasuk fungsi Office‑365 EXPAND  
* Menyimpan workbook akhir dengan semua perubahan diterapkan  

**Prasyarat**  
* .NET 6.0 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.7.2+)  
* Aspose.Cells untuk .NET v25.11 atau yang lebih baru (opsi `CopyPivotTable` diperkenalkan pada v25.11)  
* Pemahaman dasar tentang C# dan konsep Excel seperti rentang, tabel pivot, dan rumus  

> **Pro tip:** Instal Aspose.Cells melalui NuGet (`Install-Package Aspose.Cells`) untuk menjaga proyek Anda tetap terbaru dengan fitur-fitur terbaru.

## Mengekspor Excel ke PowerPoint dengan Aspose.Cells

Tugas utama pertama adalah mengonversi workbook menjadi presentasi PowerPoint sambil mempertahankan semua elemen visual dapat diedit. Ini penting ketika Anda ingin menghasilkan slide deck secara otomatis dari laporan keuangan atau dasbor.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### Mengapa ini berhasil

* **`Workbook`** memuat seluruh file Excel ke memori, memberi Anda akses API penuh.  
* **`CopyRange`** dengan `CopyPivotTable = true` memastikan sumber data, cache, dan tata letak tabel pivot diduplikasi secara tepat—sesuatu yang tidak dapat dilakukan oleh versi Aspose.Cells yang lebih lama.  
* Menambahkan worksheet baru (`Copy`) memungkinkan Anda menjaga sheet asli tidak tersentuh, yang berguna untuk jejak audit.

## Mengekspor workbook ke PowerPoint dengan objek yang dapat diedit

Sekarang kami mengubah workbook menjadi file PowerPoint. Dengan mengaktifkan `ExportEditableObjects`, setiap diagram, bentuk, atau kotak teks menjadi objek PowerPoint asli yang dapat diedit langsung oleh pengguna setelah ekspor.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### Penjelasan

* **`WorkbookDesigner`** adalah pembantu tingkat tinggi yang menyiapkan workbook untuk diekspor, menangani Smart Markers, named ranges, dan penyesuaian tata letak.  
* Menetapkan `ExportEditableObjects = true` memberi tahu Aspose.Cells untuk menerjemahkan gambar Excel menjadi bentuk PowerPoint alih-alih meratakannya menjadi gambar. Ini menghasilkan deck slide yang **sepenuhnya dapat diedit**.

> **Edge case:** Jika workbook Anda berisi diagram kompleks yang dibangun dari koneksi data eksternal, pastikan koneksi tersebut sudah diselesaikan sebelum memanggil `ExportToPptx`, jika tidak diagram mungkin muncul kosong.

## Mengekspor rentang sebagai string menggunakan logika khusus

Kadang-kadang Anda memerlukan nilai string mentah untuk pemrosesan lanjutan (mis., memberi masukan ke parser CSV). Kelas `ExportTableOptions` memungkinkan Anda mengontrol bagaimana setiap sel dikonversi.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### Mengapa Anda mungkin menggunakan ini

* **Tipe data seragam:** Mengekspor sebagai string menghindari kesalahan ketidakcocokan tipe ketika konsumen mengharapkan teks.  
* **Pemformatan khusus:** Ganti `value.ToString()` dengan pemformat khusus apa pun (mis., `value.ToString("yyyy-MM-dd")` untuk tanggal).  

## Menghitung rumus Excel dalam kode

Kebutuhan yang sering muncul adalah **menghitung rumus Excel dalam kode** tanpa membuka Excel. Aspose.Cells menyediakan mesin perhitungan bawaan yang bekerja secara offline dan mendukung fungsi Office‑365 terbaru, termasuk `EXPAND`.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### Cara kerja mesin perhitungan

* Properti `Formula` menyimpan ekspresi persis seperti yang Anda ketik di Excel.  
* `CalculateFormula()` memicu perhitungan ulang seluruh workbook, menghormati ketergantungan antar sel.  
* Fungsi `EXPAND` (tersedia di Excel 365) mengembalikan rentang spill berdasarkan sel sumber (`B1`) dan baris (`5`) serta kolom (`3`) yang ditentukan.  

> **Tip:** Jika Anda hanya perlu menghitung sebagian dari workbook, gunakan `Worksheet.CalculateFormula()` untuk membatasi ruang lingkup dan meningkatkan kinerja.

## Simpan workbook dengan semua perubahan diterapkan

Akhirnya, tulis kembali workbook yang telah dimodifikasi ke disk. Anda dapat menyimpan dalam format apa pun yang didukung (`.xlsx`, `.xls`, `.csv`, dll.) dengan mengubah ekstensi file.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### Apa yang harus diverifikasi

* Buka `result.xlsx` di Excel untuk memastikan salinan tabel pivot, hasil rumus `EXPAND`, dan string yang diekspor secara khusus.  
* Buka `output.pptx` di PowerPoint; Anda harus melihat slide yang mencerminkan tata letak Excel, dan semua diagram/kotak teks harus dapat diedit.

## Pertanyaan umum dan pemecahan masalah

| Question | Answer |
|----------|--------|
| **Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells?** | Ya. Versi percobaan dapat digunakan untuk evaluasi, tetapi lisensi penuh menghapus watermark evaluasi dan membuka fitur `CopyPivotTable`. |
| **Bagaimana jika PPTX yang diekspor menampilkan bentuk kosong?** | Pastikan objek gambar pada workbook tidak disembunyikan (`Visible = true`) dan bahwa semua tautan gambar eksternal telah disematkan sebelum ekspor. |
| **Bisakah saya mengekspor beberapa worksheet ke slide PPTX terpisah?** | Gunakan `WorkbookDesigner.ExportToPptx` dalam loop, menentukan `ExportOptions` yang berbeda untuk setiap worksheet, atau gabungkan menjadi satu presentasi dengan menambahkan slide secara manual melalui Aspose.Slides. |
| **Apakah `CalculateFormula` thread‑safe?** | Tidak. Lakukan perhitungan pada satu thread atau kloning workbook per thread untuk menghindari kondisi balapan. |

## Kesimpulan

Anda kini memiliki **solusi lengkap end‑to‑end untuk mengekspor Excel ke PowerPoint** menggunakan Aspose.Cells, dan Anda memahami cara **menghitung rumus Excel dalam kode**—termasuk fungsi modern `EXPAND`. Tutorial ini mencakup memuat workbook, menyalin tabel pivot, mengekspor ke PowerPoint yang dapat diedit, ekspor string khusus, perhitungan rumus, dan penyimpanan akhir.

Dari sini Anda dapat:

* Memperluas ekspor untuk menyertakan beberapa slide per worksheet (kata kunci sekunder: *calculate Excel formulas in code* dapat digunakan kembali saat menghasilkan data diagram).  
* Mengintegrasikan Aspose.Slides untuk menambahkan animasi atau tata letak master slide.  
* Mengganti delegate `CustomExport` sederhana dengan pemformatan yang memperhatikan lokal untuk proyek internasional.  

Silakan bereksperimen dengan rentang yang berbeda, menjelajahi fungsi Office‑365 lainnya (mis., `FILTER`, `SORT`), dan menggabungkan alur kerja ini dengan pengiriman email otomatis untuk pipeline pelaporan yang sepenuhnya otomatis.

---

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Otomatisasi Ekspor Data Excel Menggunakan Aspose.Cells untuk .NET: Panduan Langkah demi Langkah](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [Cara Mengekspor Diagram Excel ke PDF Menggunakan Aspose.Cells untuk .NET: Panduan Langkah demi Langkah](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Mengekspor Sel Excel ke Gambar Menggunakan Aspose.Cells .NET: Panduan Langkah demi Langkah](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}