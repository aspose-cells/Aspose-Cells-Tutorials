---
category: general
date: 2026-02-26
description: Ekspor buku kerja ke PDF dengan font yang disematkan dan juga ekspor
  grafik ke PowerPoint dalam C#. Pelajari cara menyalin lembar kerja tabel pivot dan
  menyimpan buku kerja sebagai PPTX.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: id
og_description: Ekspor workbook ke PDF dengan font tersemat dan juga ekspor diagram
  ke PowerPoint dalam C#. Ikuti panduan langkah demi langkah untuk menyalin tabel
  pivot dan menyimpan sebagai PPTX.
og_title: Ekspor Buku Kerja ke PDF – Panduan Lengkap C#
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: Ekspor Buku Kerja ke PDF – Panduan Lengkap C#
url: /id/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor Workbook ke PDF – Panduan Lengkap C#

Ekspor workbook ke PDF adalah kebutuhan umum ketika Anda perlu berbagi laporan dengan pemangku kepentingan yang mungkin tidak memiliki Excel terpasang. Dalam tutorial ini kami juga akan menunjukkan cara **mengekspor diagram ke PowerPoint**, menyalin **lembar kerja pivot table**, dan menyematkan font sehingga PDF terlihat persis seperti desain di layar Anda.  

Pernah bertanya-tanya mengapa beberapa PDF kehilangan tata letak asli atau mengapa slide PowerPoint berakhir dengan bentuk yang hilang? Jawabannya biasanya terletak pada opsi yang terlewat selama proses ekspor. Pada akhir panduan ini Anda akan memiliki satu metode C# yang dapat digunakan kembali yang menangani semua masalah tersebut—tidak lagi menyalin‑tempel secara manual atau mengutak‑atik pengaturan ekspor.

## Apa yang Akan Anda Pelajari

- Cara membuat workbook, menambahkan ekspresi Smart Marker, dan memprosesnya.  
- Cara **menyalin lembar kerja pivot table** tanpa merusak sumber data.  
- Cara **mengekspor diagram, bentuk, dan kotak teks** ke presentasi PowerPoint sambil tetap dapat diedit.  
- Cara **menyematkan font standar** selama ekspor PDF untuk rendering yang konsisten pada mesin apa pun.  
- Cara **menyimpan workbook sebagai PPTX** menggunakan pendekatan `save workbook as pptx`.  

Semua ini bekerja dengan pustaka Aspose.Cells dan Aspose.Slides .NET terbaru (versi 23.11 pada saat penulisan). Tanpa alat eksternal, tanpa skrip pasca‑pemrosesan—hanya C# murni.

> **Pro tip:** Jika Anda sudah menggunakan Aspose dalam proyek Anda, Anda dapat langsung menggunakan potongan kode apa adanya; jika tidak, tambahkan paket NuGet `Aspose.Cells` dan `Aspose.Slides` terlebih dahulu.

## Prasyarat

- .NET 6.0 atau lebih baru (kode juga dapat dijalankan pada .NET Framework 4.7.2).  
- Visual Studio 2022 (atau IDE apa pun yang Anda sukai).  
- Aspose.Cells .NET dan Aspose.Slides .NET terpasang melalui NuGet.  
- Familiaritas dasar dengan C# dan konsep Excel seperti Smart Markers dan PivotTables.

---

![Diagram ekspor workbook ke PDF](export-workbook-to-pdf.png "Alur kerja ekspor workbook ke PDF yang menampilkan output PDF dan PPTX")

## Ekspor Workbook ke PDF – Implementasi Langkah‑per‑Langkah

Berikut adalah contoh lengkap yang siap dijalankan. Contoh ini membuat workbook, menyisipkan ekspresi Smart Marker, memprosesnya, menyalin rentang pivot table, dan akhirnya menyimpan baik file PDF maupun PowerPoint.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Mengapa Ini Berfungsi

1. **Pemrosesan Smart Marker** memungkinkan Anda mengisi workbook dari sumber data apa pun (JSON, DataTables, dll.) tanpa menulis loop.  
2. **DetailSheetNewName** membuat lembar terpisah untuk setiap departemen, memberikan Anda tab yang bersih per‑departemen.  
3. **Menyalin rentang** (`sourceRange.Copy`) menggandakan pivot table *termasuk* cache-nya, sehingga lembar yang disalin berperilaku persis seperti aslinya.  
4. **PresentationOptions** dengan `ExportCharts`, `ExportShapes`, dan `ExportTextBoxes` memberi tahu Aspose untuk merender objek tersebut sebagai elemen PowerPoint asli, menjaga kemampuan edit.  
5. **PdfSaveOptions.EmbedStandardFonts** memastikan PDF terlihat identik pada mesin yang tidak memiliki font asli terpasang.

Hasilnya adalah dua file—`FinalReport.pdf` dan `FinalPresentation.pptx`—yang dapat dikirim via email, diarsipkan, atau ditampilkan di viewer apa pun tanpa kehilangan keakuratan.

## Ekspor Diagram ke PowerPoint (Simpan Workbook sebagai PPTX)

Jika laporan Anda berisi diagram, Anda kemungkinan ingin diagram tersebut dapat diedit di PowerPoint. Kelas `PresentationOptions` adalah kuncinya. Berikut cuplikan terfokus yang hanya menampilkan bagian ekspor diagram:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**Apa yang terjadi di balik layar?** Aspose menerjemahkan setiap diagram Excel menjadi diagram PowerPoint asli, mempertahankan seri, judul sumbu, dan pemformatan. Ini jauh lebih baik daripada mengekspor diagram sebagai gambar statis, karena audiens Anda dapat mengubah titik data nanti.

## Salin Lembar Kerja Pivot Table Tanpa Kehilangan Data

Pivot table sering menjadi bagian tersulit dalam ekspor karena mereka bergantung pada cache tersembunyi. Metode `Copy` sederhana bekerja karena Aspose menyalin baik rentang yang terlihat **dan** objek cache yang mendasarinya.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Catatan:** Jika Anda hanya membutuhkan pivot table pada lembar baru dalam workbook yang sama, pendekatan `sourceRange.Copy` sebelumnya lebih ringan dan menghindari pembuatan workbook baru seluruhnya.

## Menyematkan Font untuk Ekspor PDF – Mengapa Ini Penting

Saat Anda membuka PDF pada mesin yang tidak memiliki font asli, teks dapat bergeser, pemenggalan baris berubah, atau karakter menghilang. Mengatur `EmbedStandardFonts = true` memberi tahu Aspose untuk menyematkan font paling umum (Arial, Times New Roman, dll.) langsung ke dalam aliran PDF.

Jika Anda menggunakan font khusus, beralihlah ke `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`. Berikut contoh:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

Sekarang setiap penerima melihat tata letak yang persis sama dengan yang Anda rancang—tanpa kejutan.

## Ringkasan Contoh Kerja Lengkap

Menggabungkan semuanya, program lengkap (ditunjukkan sebelumnya) melakukan hal berikut:

1. **Membuat** workbook dengan placeholder Smart Marker.  
2. **Memproses** penanda, menghasilkan lembar detail yang dinamai sesuai departemen.  
3. **Menyalin** rentang yang berisi pivot table ke lembar kerja baru, mempertahankan fungsionalitasnya.  
4. **Mengekspor** workbook ke PowerPoint, menjaga diagram, bentuk, dan kotak teks tetap dapat diedit.  
5. **Mengekspor** workbook yang sama ke PDF sambil menyematkan font standar untuk rendering yang dapat diandalkan.

Jalankan program, buka file yang dihasilkan, dan Anda akan melihat:

- **PDF**: Tabel yang tajam, font yang disematkan, dan gaya visual yang sama seperti sumber Excel.  
- **PowerPoint**: Diagram yang dapat diedit yang dapat Anda klik kanan → *Edit Data* di PowerPoint, dan bentuk yang tetap sepenuhnya dapat dimanipulasi.

---

## Pertanyaan yang Sering Diajukan (FAQ)

**Q: Apakah ini bekerja dengan .NET Core?**  
Ya—Aspose.Cells dan Aspose.Slides bersifat lintas‑platform. Cukup target .NET 6 atau lebih baru dan kode yang sama berjalan di Windows, Linux, atau macOS.

**Q: Bagaimana jika saya hanya perlu mengekspor sebagian lembar?**  
Gunakan `Workbook.Save` dengan `SaveOptions` yang memungkinkan Anda menentukan `SheetNames`. Contoh: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**Q: Bisakah saya mengenkripsi PDF?**  
Tentu saja. Atur `PdfSaveOptions.EncryptionDetails` dengan kata sandi sebelum memanggil `Save`.

**Q: Pivot table saya menggunakan sumber data eksternal—apakah penyalinan akan memutus tautan?**  
Operasi penyalinan mencakup cache, bukan koneksi eksternal. Pivot akan tetap berfungsi secara offline, tetapi tidak akan menyegarkan terhadap sumber asli. Jika Anda membutuhkan penyegaran langsung, ekspor data sumber bersama dengan workbook.

## Langkah Selanjutnya & Topik Terkait

- **Sumber Data Dinamis** – Pelajari cara memberi JSON atau DataTable ke Smart Markers untuk pelaporan waktu‑nyata.  
- **Pemformatan PDF Lanjutan** – Jelajahi `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}