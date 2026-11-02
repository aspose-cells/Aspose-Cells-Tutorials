---
category: general
date: 2026-06-05
description: Cara mengekspor grafik dari PowerPoint menggunakan C#. Termasuk mengekspor
  objek OLE dan membuat grafik dapat diedit dalam PPTX yang dihasilkan – langkah demi
  langkah.
draft: false
keywords:
- how to export charts
- export ole objects
- how to export ole
- make charts editable
language: id
og_description: Cara mengekspor grafik dari PowerPoint menggunakan C#. Pelajari cara
  mengekspor objek OLE dan membuat grafik dapat diedit dalam file PPTX yang disimpan
  – langkah demi langkah.
og_title: Cara Mengekspor Grafik – Panduan Lengkap PowerPoint C#
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  headline: How to Export Charts – Complete PowerPoint C# Guide
  type: TechArticle
- description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  name: How to Export Charts – Complete PowerPoint C# Guide
  steps:
  - name: Full Working Example
    text: Below is the complete, self‑contained program you can compile and run. It
      includes `using` statements, proper disposal, and comments that explain each
      line.
  - name: What if the source file has no charts?
    text: The code will still run; `ExportEditableCharts` simply has no effect because
      there’s nothing to convert. No error is thrown.
  - name: Can I export only specific charts?
    text: Yes. Instead of using the global `ExportEditableCharts` flag, you can iterate
      through `presentation.Slides` and set `Chart.IsEditable = true` on individual
      chart objects before saving. This gives you granular control.
  - name: Does enabling OLE export increase file size?
    text: A little. The binary OLE streams are stored verbatim, so the resulting PPTX
      can be a few kilobytes larger. In most business scenarios the trade‑off is worth
      it because you retain full editability.
  - name: Which PowerPoint versions can open the resulting file?
    text: Any version that supports the OOXML standard (PowerPoint 2007 and later).
      The editable chart feature relies on the native chart editor introduced in Office
      2007, so older binaries like `.ppt` won’t benefit.
  type: HowTo
tags:
- PowerPoint
- C#
- Aspose.Slides
- OLE
- Charts
title: Cara Mengekspor Grafik – Panduan Lengkap PowerPoint C#
url: /id/net/chart-rendering-and-conversion/how-to-export-charts-complete-powerpoint-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengekspor Grafik – Panduan Lengkap PowerPoint C# 

Pernah bertanya-tanya **cara mengekspor grafik** dari sebuah deck PowerPoint tanpa kehilangan kemampuan untuk mengeditnya nanti? Anda tidak sendirian. Dalam banyak alur pelaporan data grafik berada di dalam file PPTX, dan begitu Anda menyerahkan file tersebut, penerima sering perlu menyesuaikan nilai atau mengubah label. Kabar baiknya, dengan beberapa baris C# Anda dapat mempertahankan kemampuan mengedit, dan bahkan dapat mengekspor objek OLE yang disematkan secara bersamaan.

Dalam tutorial ini kami akan membahas contoh praktis yang siap dijalankan yang menunjukkan **cara mengekspor grafik**, cara **mengekspor objek OLE**, dan cara **membuat grafik dapat diedit** dalam file output. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat dimasukkan ke dalam proyek .NET apa pun yang menggunakan pustaka Aspose.Slides.

> **Pro tip:** Jika Anda baru mengenal Aspose.Slides, pastikan Anda telah menambahkan paket NuGet `Aspose.Slides.NET` ke proyek Anda—jika tidak, kode tidak akan dapat dikompilasi.

## Apa yang Anda Butuhkan

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6+ (or .NET Framework 4.7+) | Runtime modern memberikan kinerja yang lebih baik dan manajemen paket yang lebih mudah. |
| Aspose.Slides for .NET (latest version) | Pustaka ini menyediakan kelas `Presentation` dan `PptxSaveOptions` yang akan kami gunakan. |
| A sample PowerPoint file with at least one chart | Demo ini bekerja pada file `.pptx` apa pun yang berisi grafik; Anda akan melihat kemampuan mengedit setelah ekspor. |
| An IDE (Visual Studio, Rider, or VS Code) | Membantu untuk debugging cepat dan melihat file yang dihasilkan. |

Tidak diperlukan alat pihak ketiga tambahan—semua ditangani oleh API Aspose.

## Langkah 1 – Memuat Presentasi Sumber

Pertama, kita perlu memuat PPTX asli ke dalam memori. Anggap ini seperti membuka dokumen di Word sebelum mulai mengedit.

```csharp
using Aspose.Slides;

// Step 1: Load the source presentation
Presentation presentation = new Presentation(@"C:\MyProjects\input.pptx");
```

> **Mengapa ini penting:** Objek `Presentation` adalah titik masuk untuk semua operasi selanjutnya. Ia mem-parsing file, membangun model objek dari slide, shape, chart, dan objek OLE, serta menjaga semuanya dalam keadaan dapat diubah.

## Langkah 2 – Membuat Opsi Penyimpanan dan Mengaktifkan Grafik yang Dapat Diedit

Secara default, ketika Anda memanggil `Save` pustaka akan mengubah grafik menjadi gambar statis. Untuk mempertahankannya dapat diedit, Anda harus mengaktifkan flag `ExportEditableCharts`.

```csharp
// Step 2: Create PPTX save options and enable editable charts
PptxSaveOptions saveOptions = new PptxSaveOptions
{
    // This tells Aspose to keep chart data in a format PowerPoint can edit.
    ExportEditableCharts = true
};
```

> **Cara kerjanya:** Ketika `ExportEditableCharts` bernilai `true`, pustaka menulis definisi XML grafik (`chart.xml`) ke dalam PPTX alih-alih merasternya. PowerPoint kemudian membaca XML tersebut dan memungkinkan pengguna membuka editor grafik.

## Langkah 3 – Mengaktifkan Ekspor Objek OLE yang Disematkan

Banyak presentasi menyematkan lembar Excel, diagram Visio, atau bahkan file PDF sebagai objek OLE. Jika Anda ingin objek-objek tersebut tetap ada setelah proses ekspor‑impor, aktifkan `ExportOLEObjects`.

```csharp
// Step 3: Enable export of embedded OLE objects
saveOptions.ExportOLEObjects = true;
```

> **Apa arti sebenarnya dari “ekspor objek OLE”:** Paket OLE disimpan sebagai blob biner di dalam PPTX. Mengatur flag ini mempertahankan biner asli, memungkinkan penerima mengklik ganda objek dan membukanya di aplikasi aslinya (mis., Excel). Tanpa flag ini, objek OLE akan dihapus, memutus tautan dan kehilangan data.

## Langkah 4 – Menyimpan Presentasi dengan Opsi yang Dikonfigurasi

Sekarang setelah kami menyiapkan opsi, kami cukup memberi tahu Aspose untuk menulis file tersebut.

```csharp
// Step 4: Save the presentation with the configured options
presentation.Save(@"C:\MyProjects\editable.pptx", saveOptions);
```

> **Hasil:** `editable.pptx` berisi slide yang sama dengan `input.pptx`, tetapi setiap grafik dapat diedit langsung di PowerPoint, dan semua objek OLE yang disematkan tetap utuh.

### Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang berdiri sendiri yang dapat Anda kompilasi dan jalankan. Program ini mencakup pernyataan `using`, disposisi yang tepat, dan komentar yang menjelaskan setiap baris.

```csharp
using System;
using Aspose.Slides;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the source PPTX
            string sourcePath = @"C:\MyProjects\input.pptx";
            // Path where the edited PPTX will be saved
            string destPath = @"C:\MyProjects\editable.pptx";

            // Load the presentation
            using (Presentation presentation = new Presentation(sourcePath))
            {
                // Configure save options
                PptxSaveOptions options = new PptxSaveOptions
                {
                    ExportEditableCharts = true,   // make charts editable
                    ExportOLEObjects = true        // export OLE objects such as embedded Excel sheets
                };

                // Save the new file
                presentation.Save(destPath, options);
            }

            Console.WriteLine("Presentation saved with editable charts and OLE objects.");
        }
    }
}
```

**Output yang diharapkan:** Setelah menjalankan program, buka `editable.pptx` di PowerPoint. Klik kanan pada grafik apa pun → *Edit Data* → editor grafik terbuka, mengonfirmasi bahwa **membuat grafik dapat diedit** berhasil. Klik ganda pada lembar Excel yang disematkan, dan akan terbuka di Excel, membuktikan bahwa **ekspor objek OLE** berhasil.

![diagram cara mengekspor grafik](https://example.com/images/export-charts.png "cara mengekspor grafik – PowerPoint setelah ekspor")

*(Teks alternatif: cara mengekspor grafik – tangkapan layar PowerPoint dengan grafik yang dapat diedit dan objek OLE)*

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika file sumber tidak memiliki grafik?

Kode tetap akan berjalan; `ExportEditableCharts` tidak berpengaruh karena tidak ada yang perlu dikonversi. Tidak ada error yang dilempar.

### Bisakah saya mengekspor hanya grafik tertentu?

Ya. Alih-alih menggunakan flag global `ExportEditableCharts`, Anda dapat mengiterasi `presentation.Slides` dan mengatur `Chart.IsEditable = true` pada objek grafik individu sebelum menyimpan. Ini memberi Anda kontrol yang lebih detail.

```csharp
foreach (ISlide slide in presentation.Slides)
{
    foreach (IChart chart in slide.Shapes.OfType<IChart>())
    {
        chart.IsEditable = true; // enable editability only for this chart
    }
}
```

### Apakah mengaktifkan ekspor OLE meningkatkan ukuran file?

Sedikit. Stream OLE biner disimpan apa adanya, sehingga PPTX yang dihasilkan dapat berukuran beberapa kilobyte lebih besar. Dalam kebanyakan skenario bisnis, kompromi ini sepadan karena Anda mempertahankan kemampuan mengedit penuh.

### Versi PowerPoint mana yang dapat membuka file hasil?

Versi apa pun yang mendukung standar OOXML (PowerPoint 2007 ke atas). Fitur grafik yang dapat diedit bergantung pada editor grafik native yang diperkenalkan di Office 2007, sehingga file biner lama seperti `.ppt` tidak akan mendapat manfaat.

## Tips untuk Kode Siap Produksi

| Tip | Reason |
|-----|--------|
| Gunakan blok `using` (seperti yang ditunjukkan) untuk membuang objek `Presentation`. | Mencegah kebocoran memori, terutama saat memproses banyak file secara batch. |
| Validasi jalur file sebelum memuat. | Mencegah `FileNotFoundException` yang dapat menyebabkan layanan latar belakang crash. |
| Catat pengaturan `ExportEditableCharts` dan `ExportOLEObjects`. | Berguna untuk pemecahan masalah ketika pengguna melaporkan grafik yang tidak dapat diedit. |
| Tangkap `Aspose.Slides.Exception` secara terpisah. | Memberikan pesan error yang lebih jelas dari pustaka (mis., tipe grafik tidak didukung). |
| Pertimbangkan `PptxCompressionLevel` jika ukuran file penting. | Anda dapat mengompres output sambil tetap mempertahankan kemampuan mengedit. |

## Ringkasan – Apa yang Kami Capai

Kami memulai dengan pertanyaan jelas: **cara mengekspor grafik** dari file PowerPoint sambil mempertahankan kemampuan mengedit dan menyimpan objek OLE yang disematkan. Dengan memuat presentasi, mengkonfigurasi `PptxSaveOptions` (`ExportEditableCharts = true` dan `ExportOLEObjects = true`), dan menyimpan file, kini kami memiliki PPTX yang memenuhi kedua persyaratan. Pola yang sama dapat digunakan kembali untuk konversi batch, pipeline CI, atau alat pelaporan otomatis apa pun.

## Apa yang Bisa Dijelajahi Selanjutnya?

- **Ekspor grafik sebagai gambar** untuk laporan statis (`saveOptions.ExportEditableCharts = false`).  
- **Konversi PPTX ke PDF** sambil mempertahankan grafik vektor (`PdfSaveOptions`).  
- **Manipulasi data grafik secara programatis** (mis., memperbarui nilai seri sebelum ekspor).  
- **Integrasikan dengan Azure Functions** untuk menyediakan API ekspor grafik sesuai permintaan.

Silakan bereksperimen, dan beri tahu kami kasus tepi apa yang Anda temui. Selamat coding, dan semoga semua grafik Anda tetap dapat diedit!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengekspor Grafik Excel ke PDF Menggunakan Aspose.Cells untuk .NET: Panduan Langkah‑per‑Langkah](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Cara Mengonversi Grafik Excel ke SVG Menggunakan Aspose.Cells untuk .NET (Panduan Langkah‑per‑Langkah)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Cara Menerapkan Tema pada Grafik Excel Menggunakan Aspose.Cells .NET: Panduan Langkah‑per‑Langkah](/cells/english/net/charts-graphs/apply-themes-charts-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}