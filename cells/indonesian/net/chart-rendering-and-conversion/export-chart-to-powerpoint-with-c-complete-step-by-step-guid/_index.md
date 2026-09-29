---
category: general
date: 2026-02-26
description: Ekspor diagram ke PowerPoint dari Excel menggunakan C#. Pelajari cara
  mengonversi Excel ke PowerPoint, menyimpan Excel sebagai PowerPoint, dan menjaga
  bentuk tetap dapat diedit.
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: id
og_description: Ekspor grafik ke PowerPoint dari Excel menggunakan C#. Panduan ini
  menunjukkan cara mengonversi Excel ke PowerPoint, menyimpan buku kerja sebagai PPTX,
  dan menjaga bentuk tetap dapat diedit.
og_title: Ekspor Diagram ke PowerPoint dengan C# – Tutorial Pemrograman Lengkap
tags:
- Aspose.Cells
- C#
- Office Automation
title: Ekspor Grafik ke PowerPoint dengan C# – Panduan Lengkap Langkah demi Langkah
url: /id/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Chart to PowerPoint – Tutorial Pemrograman Lengkap

Pernah bertanya-tanya bagaimana cara **mengekspor chart ke PowerPoint** tanpa kehilangan kemampuan edit? Dalam banyak skenario pelaporan Anda memerlukan chart hidup di dalam slide deck, namun menyalin‑tempel secara manual sangat merepotkan. Kabar baiknya, Anda dapat melakukannya secara programatis dengan beberapa baris C#.

Dalam panduan ini kami akan membahas seluruh proses: mulai dari memuat workbook Excel yang berisi chart dengan textbox, mengonfigurasi ekspor sehingga textbox dan shape tetap dapat diedit, dan akhirnya menyimpan hasilnya sebagai file **PowerPoint**. Pada akhir tutorial Anda juga akan tahu cara **mengonversi Excel ke PowerPoint**, **menyimpan Excel sebagai PowerPoint**, serta menyesuaikan opsi untuk skenario kasus tepi.

## Apa yang Anda Butuhkan

- **Aspose.Cells for .NET** (versi 23.10 atau lebih baru). Ini adalah pustaka yang membuat konversi menjadi mudah.
- Runtime **.NET 6+** – SDK terbaru apa pun dapat digunakan.
- File Excel sederhana (`ChartWithTextbox.xlsx`) yang berisi setidaknya satu chart dan sebuah textbox.
- Visual Studio atau IDE favorit Anda.

Tidak ada paket NuGet tambahan yang diperlukan selain Aspose.Cells, namun memiliki pemahaman dasar tentang sintaks C# tentu membantu.

## Export Chart to PowerPoint – Langkah‑per‑Langkah

Berikut kami membagi solusi menjadi langkah‑langkah terpisah yang mudah diikuti. Setiap langkah menyertakan kode tepat yang Anda perlukan, plus paragraf singkat “mengapa” yang menjelaskan alasan di baliknya.

### Langkah 1: Muat Excel Workbook yang Memuat Chart

Pertama kita harus membawa file sumber ke memori. Menggunakan `Workbook` dari Aspose.Cells membaca seluruh spreadsheet, termasuk chart, gambar, dan objek tersemat.

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*Mengapa ini penting:* Jika workbook dibuka tanpa menentukan path dengan benar, Anda akan mendapatkan `FileNotFoundException`. Pemeriksaan cepat ini mencegah Anda mengekspor slide kosong di kemudian hari.

### Langkah 2: Siapkan Presentation Options agar Shape Tetap Dapat Diedit

Aspose.Cells memungkinkan Anda menentukan apakah textbox, shape, bahkan chart itu sendiri tetap **dapat diedit** setelah ekspor. Menetapkan `ExportTextBoxes` dan `ExportShapes` ke `true` mempertahankan objek‑objek tersebut sebagai elemen PowerPoint native alih‑alih meratakannya menjadi gambar statis.

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*Mengapa ini penting:* Jika Anda membiarkan flag ini pada nilai default (`false`), slide yang dihasilkan akan berisi bitmap chart, sehingga tidak mungkin mengedit seri atau mengubah caption nanti. Mengaktifkan kedua opsi memberi Anda chart PowerPoint sejati yang berperilaku persis seperti yang Anda gambar secara manual.

### Langkah 3: Konversi Excel ke PowerPoint dan Simpan File

Sekarang kita panggil metode `Save`, menyertakan enum `SaveFormat.Pptx` dan opsi yang baru saja dikonfigurasi. Pustaka akan menangani penerjemahan objek chart Excel menjadi shape chart PowerPoint.

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*Mengapa ini penting:* Pemanggilan `Save` melakukan semua pekerjaan berat—memetakan seri Excel ke seri PowerPoint, mempertahankan format sumbu, dan menyalin semua textbox yang terhubung. Setelah baris ini dijalankan, Anda akan memiliki file `.pptx` yang sepenuhnya dapat diedit dan siap dibuka di Microsoft PowerPoint.

### Verifikasi Hasil

Buka `Result.pptx` di PowerPoint. Anda seharusnya melihat slide yang berisi:

- Chart asli, masih terhubung ke datanya (Anda dapat double‑click untuk mengedit seri).
- Setiap textbox yang ada di lembar Excel, kini menjadi textbox PowerPoint native.
- Layout slide dipilih secara otomatis (biasanya slide kosong).

Jika ada elemen yang hilang, periksa kembali bahwa workbook sumber memang memiliki objek yang terlihat dan bahwa `ExportTextBoxes` / `ExportShapes` telah diset ke `true`.

### Mengonversi Excel ke PowerPoint: Menangani Banyak Worksheet

Seringkali sebuah workbook berisi lebih dari satu sheet, masing‑masing dengan chartnya. Secara default Aspose.Cells akan mengekspor **semua** chart dari **semua** worksheet ke slide terpisah. Jika Anda hanya membutuhkan sebagian, Anda dapat memfilter chart sebelum menyimpan:

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*Tips profesional:* Menetapkan `chart.IsVisible = false` lebih ringan daripada menghapus chart sepenuhnya, dan memungkinkan Anda men-toggle inklusi tanpa mengubah file sumber.

### Simpan Excel sebagai PowerPoint – Menyesuaikan Ukuran Slide

PowerPoint secara default menggunakan slide berukuran 10‑inch × 5.63‑inch. Jika chart Anda terasa sempit, Anda dapat mengubah dimensi slide melalui objek `PresentationOptions`:

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

Sekarang chart yang diekspor akan memiliki ruang lebih, dan semua textbox akan mempertahankan tata letak aslinya.

### Cara Mengonversi Excel ke PPT: Menangani Objek Tersembunyi

Baris, kolom, atau shape yang disembunyikan kadang‑kadang ikut masuk ke dalam ekspor. Untuk menghilangkannya, lakukan pembersihan cepat sebelum menyimpan:

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

Langkah ini tidak selalu diperlukan, tetapi dapat mencegah celah tak terduga di deck slide akhir Anda.

### Simpan Workbook sebagai PPTX – Contoh Lengkap yang Siap Jalan

Menggabungkan semuanya, berikut program konsol siap‑jalankan yang mendemonstrasikan alur lengkap:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

Menjalankan program ini akan membuat `Result.pptx` dengan chart dan textbox yang dapat diedit, persis seperti yang Anda harapkan ketika **menyimpan workbook sebagai pptx** secara manual.

![Export chart to PowerPoint example](/images/export-chart-to-powerpoint.png "Export chart to PowerPoint – editable slide")

## Pertanyaan Umum & Kasus Tepi

**Bagaimana jika file Excel berisi chart dengan sumber data eksternal yang terhubung?**  
Aspose.Cells menyalin nilai data *saat ini* ke chart PowerPoint. Ia **tidak** mempertahankan tautan eksternal, karena PowerPoint tidak dapat merujuk koneksi data Excel dengan cara yang sama. Jika Anda memerlukan pembaruan langsung, pertimbangkan menyematkan file Excel asli ke dalam PPTX sebagai objek OLE.

**Apakah saya dapat mengekspor chart yang menggunakan tema khusus?**  
Ya. Pustaka berusaha memetakan warna tema Excel ke slot tema PowerPoint. Untuk palet yang sangat khusus, Anda mungkin perlu menyesuaikan warna setelah ekspor menggunakan API PowerPoint sendiri (misalnya, Aspose.Slides).

**Apakah ada batasan jumlah chart?**  
Secara praktis tidak ada—Aspose.Cells melakukan streaming data, sehingga bahkan workbook dengan puluhan chart dapat diekspor, meskipun ukuran PPTX yang dihasilkan akan bertambah secara linear.

**Apakah saya memerlukan lisensi untuk Aspose.Cells?**  
Evaluasi gratis dapat digunakan, tetapi akan menambahkan watermark pada slide pertama. Untuk penggunaan produksi, dapatkan lisensi resmi untuk menghilangkan watermark dan membuka kinerja penuh.

## Ringkasan

Kami telah membahas cara **mengekspor chart ke PowerPoint** menggunakan C#, memperlihatkan kode tepat untuk memuat workbook Excel, mengonfigurasi `PresentationOptions` agar textbox dan shape tetap dapat diedit, dan akhirnya menyimpan hasilnya sebagai `.pptx`. Anda juga belajar cara **mengonversi Excel ke PowerPoint**, **menyimpan Excel sebagai PowerPoint**, serta menjawab pertanyaan “**bagaimana mengonversi Excel ke ppt**” dengan contoh lengkap yang dapat dijalankan.

## Apa Selanjutnya?

- **Simpan workbook sebagai PPTX** dengan banyak slide: loop melalui setiap worksheet dan panggil `Save` dengan `PresentationOptions` untuk masing‑masing.
- Jelajahi **Aspose.Slides** jika Anda perlu memodifikasi PPTX yang dihasilkan secara programatis (menambah transisi, catatan pembicara, dll.).
- Coba mengekspor **pivot chart** atau **chart 3‑D**—opsi yang sama berlaku, namun Anda mungkin perlu menyesuaikan format sumbu setelahnya.

Jika Anda mengalami kendala, tinggalkan komentar di bawah atau periksa dokumentasi resmi Aspose.Cells untuk perubahan API terbaru. Selamat coding, dan nikmati mengubah chart Excel menjadi presentasi PowerPoint yang elegan hanya dengan beberapa baris C#!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}