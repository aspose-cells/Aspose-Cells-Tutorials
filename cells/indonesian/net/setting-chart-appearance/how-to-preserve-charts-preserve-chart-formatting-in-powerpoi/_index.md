---
category: general
date: 2026-07-03
description: Cara mempertahankan diagram sambil menjaga pemformatan diagram menggunakan
  Aspose.Slides di C#. Ikuti panduan langkah demi langkah ini.
draft: false
keywords:
- how to preserve charts
- preserve chart formatting
language: id
og_description: cara mempertahankan diagram dan format diagram dengan Aspose.Slides
  di C#. Panduan lengkap dengan kode.
og_title: Cara mempertahankan grafik – mempertahankan format grafik di PowerPoint
  (C#)
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  headline: how to preserve charts – preserve chart formatting in PowerPoint C#
  type: TechArticle
- description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  name: how to preserve charts – preserve chart formatting in PowerPoint C#
  steps:
  - name: Open `EditableCharts.pptx` in PowerPoint.
    text: Open `EditableCharts.pptx` in PowerPoint.
  - name: Click any chart → “Edit Data”.
    text: Click any chart → “Edit Data”.
  - name: The Excel‑like data sheet should appear, letting you modify series values.
    text: The Excel‑like data sheet should appear, letting you modify series values.
  type: HowTo
- questions:
  - answer: Directly no—`ExportEditableObjects` only applies to the PPTX format. Convert
      first, then export.
    question: Does this work with PowerPoint 2003 (PPT) files?
  - answer: Absolutely. The same `ExportEditableObjects` flag keeps SmartArt, tables,
      and diagrams editable.
    question: Can I preserve other objects like SmartArt?
  - answer: 'The slide size is stored in the presentation metadata and isn’t affected
      by these options. No extra code needed. --- ## Next steps – keep the momentum
      Now that you’ve nailed **how to preserve charts**, try exploring: - **preserve
      chart formatting** for specific chart types (e.g., stacked bar vs. rad'
    question: What if I need to keep the original slide size?
  type: FAQPage
tags:
- Aspose.Slides
- C#
- PowerPoint
- chart automation
title: Cara Mempertahankan Grafik – Mempertahankan Format Grafik di PowerPoint C#
url: /id/net/setting-chart-appearance/how-to-preserve-charts-preserve-chart-formatting-in-powerpoi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara mempertahankan charts – preserve chart formatting in PowerPoint C#

Pernah bertanya-tanya **bagaimana cara mempertahankan charts** ketika Anda perlu mengekspor atau memanipulasi file PowerPoint secara programatis? Mungkin Anda sudah mencoba menyimpan cepat dan chart berubah menjadi gambar statis, menghilangkan kemampuan mengedit yang Anda harapkan.  

Dalam tutorial ini kami akan menunjukkan **bagaimana cara mempertahankan charts** **dan** menjaga **preserve chart formatting** mereka tetap utuh menggunakan Aspose.Slides untuk .NET. Pada akhir tutorial Anda akan memiliki potongan kode C# yang siap dijalankan yang menghasilkan PPTX dimana setiap chart tetap menjadi objek OOXML yang dapat diedit—tidak ada lagi gambar yang diratakan.

## Apa yang akan Anda pelajari

- Langkah-langkah tepat untuk memuat presentasi, mengonfigurasi opsi ekspor, dan menyimpan sambil **preserving chart formatting**.  
- Mengapa flag `ExportEditableObjects` penting dan bagaimana ia menghentikan chart dari rasterisasi.  
- Jebakan umum (mis., format PPT lama, font yang hilang) dan perbaikan cepat.  

Tidak diperlukan pengalaman Aspose sebelumnya; cukup dengan setup C# dasar dan file PowerPoint yang ingin Anda pertahankan agar ramah chart.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Framework 4.7+).  
- Paket NuGet Aspose.Slides untuk .NET (`Install-Package Aspose.Slides.NET`).  
- Sebuah contoh `input.pptx` yang berisi setidaknya satu chart.  
- Visual Studio, Rider, atau editor apa pun yang Anda suka.

---

## Langkah 1: Instal Aspose.Slides dan buat proyek konsol baru

Untuk memulai, buat aplikasi konsol baru dan tambahkan pustaka:

```bash
dotnet new console -n PreserveChartsDemo
cd PreserveChartsDemo
dotnet add package Aspose.Slides.NET
```

> **Pro tip:** Jika Anda berada di belakang proxy perusahaan, tambahkan flag `--no-restore` dan lakukan restore nanti dengan pengaturan proxy Anda.

## Langkah 2: Muat presentasi sumber – tempat pertama untuk menerapkan **how to preserve charts**

Buka file PPTX Anda menggunakan kelas `Presentation`. Di sinilah perjalanan menuju **how to preserve charts** benar‑benar dimulai.

```csharp
using Aspose.Slides;
using Aspose.Slides.Export;

namespace PreserveChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Load the source presentation
            // Replace the path with the location of your PPTX that contains charts.
            Presentation pres = new Presentation(@"YOUR_DIRECTORY\input.pptx");
```

Perhatikan bahwa kami belum menyentuh objek chart apa pun—itu disengaja. Memuat file apa adanya memastikan kami mempertahankan struktur XML asli, yang penting untuk **preserve chart formatting** nanti.

## Langkah 3: Konfigurasikan opsi ekspor – inti dari **how to preserve charts**

Aspose.Slides menyediakan kelas `PresentationExportOptions`. Menetapkan `ExportEditableObjects` ke `true` memberi tahu mesin untuk mempertahankan chart, tabel, dan SmartArt sebagai bagian OOXML asli alih‑alih meratakannya.

```csharp
            // Step 3: Configure export options to keep objects editable
            PresentationExportOptions exportOptions = new PresentationExportOptions
            {
                // This flag is the key to how to preserve charts.
                ExportEditableObjects = true
            };
```

Mengapa ini berhasil? Ketika `ExportEditableObjects` bernilai `false` (default), pustaka merasterisasi objek kompleks untuk kompatibilitas, yang menghancurkan **preserve chart formatting**. Mengaktifkannya mempertahankan XML chart asli, memungkinkan pengguna akhir membuka PPTX dan tetap dapat mengedit data chart.

## Langkah 4: Simpan presentasi menggunakan opsi yang telah dikonfigurasi

Sekarang kami menulis file output. Overload `Save` yang sama yang menerima `SaveFormat` dan `exportOptions` menjamin chart tetap dapat diedit.

```csharp
            // Step 4: Save the presentation with the configured options
            pres.Save(@"YOUR_DIRECTORY\EditableCharts.pptx", SaveFormat.Pptx, exportOptions);

            // Optional: Inform the user
            Console.WriteLine("Presentation saved with editable charts at: YOUR_DIRECTORY\\EditableCharts.pptx");
        }
    }
}
```

Menjalankan program ini menghasilkan `EditableCharts.pptx`. Buka di PowerPoint, klik kanan pada chart, dan Anda akan melihat opsi “Edit Data” yang biasa—bukti bahwa kami berhasil menguasai **how to preserve charts** dan **preserve chart formatting**.

## Langkah 5: Verifikasi hasil dan selesaikan masalah umum

### Verifikasi

1. Buka `EditableCharts.pptx` di PowerPoint.  
2. Klik chart mana pun → “Edit Data”.  
3. Lembar data mirip Excel harus muncul, memungkinkan Anda mengubah nilai seri.

Jika Anda hanya melihat gambar statis, periksa kembali bahwa:

- Anda menggunakan versi terbaru Aspose.Slides (build lama memiliki bug dengan `ExportEditableObjects`).  
- PPTX sumber memang berisi objek chart (bukan gambar chart).  
- Tidak ada tema khusus atau substitusi font yang menyebabkan chart dirender sebagai gambar.

### Kasus Tepi

- **File PPT (biner) lama:** Konversi terlebih dahulu ke PPTX (`pres.Save("temp.pptx", SaveFormat.Pptx)`) sebelum menerapkan opsi ekspor.  
- **Presentasi besar:** Penggunaan memori dapat melonjak; pertimbangkan pola `Dispose` pada `Presentation` atau API streaming untuk file yang sangat besar.  
- **Font tersemat:** Jika lingkungan target tidak memiliki font asli, PowerPoint dapat beralih dan merender chart sebagai gambar. Sematkan font dalam file sumber atau kirimkan bersama aplikasi Anda.

## Pertanyaan yang Sering Diajukan (FAQ)

**Q: Apakah ini bekerja dengan file PowerPoint 2003 (PPT)?**  
A: Tidak secara langsung—`ExportEditableObjects` hanya berlaku untuk format PPTX. Konversi dulu, lalu ekspor.

**Q: Bisakah saya mempertahankan objek lain seperti SmartArt?**  
A: Tentu saja. Flag `ExportEditableObjects` yang sama menjaga SmartArt, tabel, dan diagram tetap dapat diedit.

**Q: Bagaimana jika saya perlu mempertahankan ukuran slide asli?**  
A: Ukuran slide disimpan dalam metadata presentasi dan tidak terpengaruh oleh opsi ini. Tidak diperlukan kode tambahan.

## Langkah Selanjutnya – pertahankan momentum

Sekarang Anda telah menguasai **how to preserve charts**, cobalah menjelajahi:

- **preserve chart formatting** untuk tipe chart tertentu (mis., stacked bar vs. radar).  
- Menggunakan API `Chart` untuk memodifikasi data secara programatis sebelum menyimpan.  
- Mengekspor ke format lain (PDF, HTML) sambil tetap menjaga chart dapat diedit di PPTX sumber.  

Masing‑masing hal ini dibangun di atas prinsip yang sama: menjaga OOXML yang mendasari tetap utuh.

## Kesimpulan

Kami telah membahas **how to preserve charts** dalam file PowerPoint menggunakan Aspose.Slides untuk .NET, dan kami telah menunjukkan langkah‑langkah **preserve chart formatting** yang tepat untuk menjaga chart tetap dapat diedit sepenuhnya. Potongan kode lengkap di atas siap dimasukkan ke dalam proyek C# mana pun, dan penjelasan mencakup *mengapa* di balik setiap baris—sehingga Anda tidak hanya menyalin‑tempel, tetapi juga memahami.

Cobalah, sesuaikan opsi ekspor, dan segera Anda akan mengotomatisasi pembaruan presentasi tanpa pernah kehilangan kemampuan untuk menyempurnakan data chart. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengekspor Diagram Excel ke PDF Menggunakan Aspose.Cells untuk .NET: Panduan Langkah demi Langkah](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Cara Mengonversi Diagram Excel ke SVG Menggunakan Aspose.Cells untuk .NET (Panduan Langkah demi Langkah)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Cara Membuat Diagram di Excel Menggunakan Aspose.Cells untuk .NET: Panduan Pengembang](/cells/english/net/charts-graphs/create-charts-excel-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}