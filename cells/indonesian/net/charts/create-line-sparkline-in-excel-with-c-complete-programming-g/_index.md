---
category: general
date: 2026-06-30
description: Buat sparkline garis di Excel dengan C# secara cepat. Pelajari cara menambahkan
  sparkline, membuat workbook Excel dengan C#, dan menambahkan sparkline ke sel dalam
  beberapa langkah.
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: id
og_description: Buat sparkline garis di Excel dengan C#. Tutorial ini menunjukkan
  cara menambahkan sparkline, membuat workbook Excel dengan C#, dan menyematkan sparkline
  ke dalam sel.
og_title: Buat Sparkline Garis di Excel dengan C# – Panduan Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Buat sparkline garis di Excel dengan C# – Panduan Pemrograman Lengkap
url: /id/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat line sparkline di Excel dengan C# – Panduan Pemrograman Lengkap

Pernah bertanya-tanya bagaimana cara **membuat line sparkline** dalam file Excel menggunakan C#? Anda tidak sendirian—para pengembang terus bertanya, “bagaimana cara menambahkan sparkline ke laporan tanpa membuka Excel secara manual?” Kabar baiknya, dengan beberapa baris kode Anda dapat menghasilkan line sparkline yang ramping langsung di dalam workbook, tanpa UI.

Dalam tutorial ini kami akan membahas semua yang perlu Anda ketahui: mulai dari dasar **create Excel workbook C#**, mengisi data, hingga langkah‑langkah tepat untuk **add line sparkline** dan **add sparkline to cell**. Pada akhir tutorial Anda akan memiliki file *.xlsx* siap pakai yang menampilkan tren penjualan bulanan sekilas. Tanpa basa‑basi, hanya solusi praktis yang dapat dijalankan.

---

## Apa yang Akan Anda Bangun

- Sebuah workbook Excel baru bernama *KPI_Sparklines.xlsx*  
- Sebuah worksheet bernama **KPI** yang berisi contoh angka penjualan  
- Sebuah **line sparkline** yang ditempatkan di sel **D2** dan merujuk ke rentang data **B2:B13**  
- Pemformatan dasar (warna, ketebalan garis) agar sparkline terlihat menonjol  

Prasyarat? Hanya .NET SDK (3.1+ atau .NET 6) dan perpustakaan gratis Aspose.Cells untuk .NET (tersedia via NuGet). Jika Anda belum pernah menggunakan Aspose.Cells, anggaplah sebagai mesin Excel yang kuat yang dapat dipanggil dari kode—tanpa interop COM, tanpa instalasi Excel.

---

![Create line sparkline in Excel using C#](https://example.com/images/create-line-sparkline.png "Create line sparkline in Excel with C#")

*Image alt text: create line sparkline in Excel using C# code example*

---

## Langkah 1: **Create Excel workbook C#** – Siapkan file dan worksheet

Hal pertama yang harus dilakukan adalah membuat objek workbook dan worksheet tempat data akan disimpan. Ini adalah fondasi untuk semua otomatisasi Excel, baik Anda nanti **add line sparkline** maupun menulis rumus.

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **Mengapa ini penting:** Kelas `Workbook` mewakili seluruh file, sedangkan `Worksheet` adalah kanvas untuk baris, kolom, dan nantinya sparkline kita. Menamai sheet di awal membuat file lebih rapi dan mudah dipahami.

---

## Langkah 2: Isi data – Rentang sumber untuk sparkline

Sebuah sparkline membutuhkan data untuk digambarkan. Mari kita simulasi 12 bulan angka penjualan. Anda bisa mengambil data ini dari basis data, tetapi demi kejelasan kami akan menghasilkan secara langsung.

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **Tip:** `PutValue` secara otomatis mendeteksi tipe data, jadi Anda tidak perlu meng‑cast ke `double` atau `int`. Jika Anda perlu memformat sel (mata uang, pemisah ribuan), Anda dapat menerapkan objek `Style` nanti.

---

## Langkah 3: **Create line sparkline** – Tambahkan sparkline ke sel tertentu

Sekarang saatnya menampilkan bintang utama: **line sparkline**. Aspose.Cells mengelompokkan sparkline, jadi pertama‑tama kita buat `SparklineGroup` dengan tipe `Line`, lalu tentukan di mana visualnya akan ditempatkan.

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **Cara kerjanya:**  
> - `firstRow/firstColumn` dan `lastRow/lastColumn` menentukan *sel target* (tempat sparkline muncul).  
> - `firstDataRow/lastDataRow` menunjuk ke rentang sumber.  
> Karena kita menggunakan **line sparkline**, visualnya akan berupa garis tipis sederhana yang mengikuti tren angka.

### Opsional: **How to add sparkline** dengan gaya khusus

Jika Anda ingin sparkline lebih menonjol, sesuaikan beberapa properti:

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **Mengapa memberi gaya?** Garis biru tua di atas latar putih nyaman dipandang, sementara penanda memberi petunjuk cepat tentang titik data individu—berguna untuk presentasi.

---

## Langkah 4: Simpan workbook – Verifikasi hasilnya

Setelah sparkline ditempatkan, cukup tulis file ke disk. Pilih folder yang Anda miliki hak tulisnya; contoh ini menggunakan path placeholder yang harus Anda ganti.

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **Verifikasi:** Buka file yang dihasilkan di Excel (atau penampil lain yang mendukung .xlsx). Anda akan melihat **line sparkline** di sel **D2** yang mencerminkan peningkatan angka penjualan di kolom **B**. Mengarahkan kursor ke sparkline akan menampilkan tooltip dengan nilai‑nilai dasarnya.

---

## Langkah 5: Kesulitan umum saat Anda **add sparkline to cell**

Bahkan contoh yang sederhana sekalipun dapat menimbulkan masalah bagi pemula. Berikut beberapa hal yang perlu diwaspadai:

| Masalah | Mengapa terjadi | Solusi |
|-------|----------------|-----|
| Koordinat sel salah | Target sparkline menggunakan indeks kolom berbasis nol tetapi indeks baris berbasis satu. | Ingat `Cells[row, column]` dimana `row` berbasis nol, `column` juga berbasis nol. Pada `SparklineGroup.Add`, baris dan kolom **berbasis satu**. |
| Tidak ada data yang ditampilkan | Rentang sumber kosong atau berisi nilai non‑numerik. | Pastikan rentang (misalnya `B2:B13`) berisi angka. Gunakan `PutValue` dengan tipe numerik. |
| Sparkline menghilang setelah disimpan | Versi perpustakaan tidak cocok atau lisensi hilang. | Gunakan paket Aspose.Cells terbaru dan berikan lisensi yang valid jika Anda melewati batas evaluasi. |
| Pemformatan tidak diterapkan | Perubahan gaya dilakukan sebelum menambahkan sparkline. | Tetapkan gaya **setelah** Anda membuat grup, seperti yang ditunjukkan di atas. |

---

## Kode Sumber Lengkap – Salin‑tempel sekali pakai

Berikut adalah program lengkap yang siap dijalankan. Tempelkan ke proyek konsol baru, tambahkan paket NuGet Aspose.Cells, dan tekan **F5**.

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Output yang diharapkan:** Saat Anda membuka *KPI_Sparklines.xlsx*, kolom **B** menampilkan dua belas angka (5.000 → 13.250) dan sel **D2** berisi line sparkline biru tua yang halus dan naik secara bertahap. Penanda muncul sebagai titik oranye‑merah kecil jika Anda mengaktifkan `ShowMarkers`.

---

## Apa Selanjutnya? Memperluas Keterampilan Sparkline Anda

Setelah menguasai **create line sparkline** dengan Aspose.Cells, pertimbangkan untuk mengeksplorasi topik terkait berikut:

- **Add column sparkline** – cocok untuk menampilkan data bertumpuk.  
- **Create multi‑sparkline groups** pada lembar yang sama untuk perbandingan berdampingan.  
- **Export to PDF** sambil mempertahankan sparkline (Aspose.Cells mendukung konversi PDF).  
- **Dynamic data sources** – tarik data penjualan nyata dari basis data SQL alih‑alih nilai yang ditulis keras.  

Masing‑masing topik ini membangun pada konsep inti yang sama: **create Excel workbook C#**, mengisi data, dan **add sparkline to cell** dengan gaya yang diinginkan.

---

### TL;DR

Kami menunjukkan cara **membuat line sparkline** dalam workbook Excel menggunakan C#. Langkah‑langkah—*buat workbook, isi data, tambahkan sparkline, beri gaya, dan simpan*—semuanya dibungkus dalam satu program mandiri. Silakan ubah warna, ketebalan garis, atau rentang sumber agar sesuai dengan kebutuhan pelaporan Anda.

Ada trik yang ingin Anda bagikan? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Automasi Excel: Buat Workbook dan Tambahkan ListBox Menggunakan Aspose.Cells untuk .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Automasi Excel: Buat Workbook Tambahkan ListBox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Automasi Excel: Buat Workbook Tambahkan ListBox Aspose Cells](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}