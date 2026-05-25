---
category: general
date: 2026-03-18
description: Buat buku kerja baru dan ekspor Excel ke TXT sambil mempertahankan presisi
  numerik. Pelajari cara menyimpan lembar kerja sebagai TXT dan mengonversi lembar
  kerja ke TXT secara efisien.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: id
og_description: Buat buku kerja baru dan ekspor Excel ke TXT dengan presisi. Tutorial
  ini menunjukkan cara menyimpan lembar kerja sebagai TXT dan mengonversi lembar kerja
  ke TXT menggunakan C#.
og_title: Buat buku kerja baru – Panduan Ekspor Excel ke TXT
tags:
- Aspose.Cells
- C#
- Excel automation
title: Buat buku kerja baru – Ekspor Excel ke TXT dengan Presisi Penuh
url: /id/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat workbook baru – Ekspor Excel ke TXT dengan Presisi Penuh

Pernahkah Anda perlu **create new workbook** di C# hanya untuk menuliskan beberapa data ke file teks biasa? Mungkin Anda menarik laporan dari sistem legacy dan alat hilir hanya menerima umpan `.txt`. Kabar baiknya? Anda tidak perlu mengorbankan presisi numerik, dan tentu saja tidak perlu membuat string CSV secara manual.

Dalam panduan ini kami akan membahas seluruh proses **export excel to txt**, mulai dari menginisialisasi workbook hingga mempertahankan nol di akhir ketika Anda **save worksheet as txt**. Pada akhir tutorial Anda akan memiliki potongan kode siap‑jalankan yang dapat Anda sisipkan ke proyek .NET mana pun—tanpa utilitas tambahan.

## Apa yang Anda Butuhkan

- **ASP.NET/ .NET 6+** (kode ini juga berfungsi pada .NET Framework 4.6+)
- **Aspose.Cells for .NET** – perpustakaan yang menyediakan kelas `Workbook`, `Worksheet`, dan `TxtSaveOptions`. Anda dapat mengunduhnya dari NuGet dengan `Install-Package Aspose.Cells`.
- Pemahaman dasar tentang C# (jika Anda nyaman dengan pernyataan `using`, Anda sudah siap).

Itu saja—tidak ada interop Excel, tidak ada objek COM, dan tentu saja tidak ada penggabungan string manual.  

---

## Langkah 1: Inisialisasi Workbook Baru (Kata Kunci Utama)

Hal pertama yang harus Anda lakukan adalah **create new workbook**. Anggap workbook sebagai kanvas kosong tempat Anda nanti menempelkan angka, teks, atau formula.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **Mengapa ini penting:** Menginstansiasi `Workbook` tanpa memuat file memberi Anda lembar kerja bersih. Anda kemudian dapat menambahkan data secara programatik, yang sangat cocok untuk skenario **convert worksheet to txt** di mana Anda tidak memiliki file `.xlsx` yang sudah ada.

---

## Langkah 2: Isi Sel – Pertahankan Nol di Akhir

Kesalahan umum saat menuliskan angka ke teks adalah kehilangan nol di akhir (`123.45000` menjadi `123.45`). Jika sistem hilir mengandalkan bidang lebar tetap, kehilangan ini dapat merusak semuanya.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **Pro tip:** `PutValue` secara otomatis menebak tipe data. Jika Anda membutuhkan string yang terlihat seperti angka, gunakan `PutValue("123.45000")` sebagai gantinya.

---

## Langkah 3: Konfigurasikan Opsi Penyimpanan TXT – Pertahankan Presisi Numerik

Di sinilah keajaiban terjadi. Dengan mengaktifkan `PreserveNumericPrecision`, Anda memberi tahu Aspose.Cells untuk menulis nilai persis yang Anda masukkan, termasuk nol tak signifikan di akhir.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **Mengapa mengaktifkannya?** Saat Anda **save excel as txt**, perilaku default memotong desimal yang tidak diperlukan. Menetapkan `PreserveNumericPrecision = true` menjamin output mencerminkan nilai yang ditampilkan di sel, yang sangat penting untuk laporan keuangan atau data ilmiah.

---

## Langkah 4: Simpan Worksheet sebagai TXT – Ekspor Akhir

Sekarang kita benar‑benar **save worksheet as txt**. Anda dapat menentukan jalur ke mana saja yang memiliki izin menulis; contoh ini menggunakan folder relatif bernama `output`.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **Output yang diharapkan** (`num-preserve.txt`):

```
123.45000
```

Perhatikan nol di akhir tetap utuh—tepat seperti yang Anda minta.

---

## Langkah 5: Verifikasi Hasil – Pemeriksaan Cepat

Setelah program dijalankan, buka `num-preserve.txt` di editor teks apa pun. Anda harus melihat satu baris `123.45000`. Jika yang muncul `123.45`, periksa kembali bahwa `PreserveNumericPrecision` diset ke `true` dan Anda menggunakan versi terbaru Aspose.Cells (v23.10+).

---

## Variasi Umum & Kasus Tepi

### Mengekspor Beberapa Sel atau Rentang

Jika Anda perlu **export excel to txt** untuk seluruh rentang, cukup isi lebih banyak sel sebelum menyimpan:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Aspose akan menuliskan setiap sel pada baris baru secara default. Anda juga dapat mengubah pemisah (tab, koma) melalui `txtSaveOptions.Separator`.

### Mengonversi Worksheet ke TXT dengan Encoding Berbeda

Kadang‑kadang sistem hilir memerlukan UTF‑8 BOM atau ASCII. Sesuaikan encoding seperti ini:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### Menangani Workbook Besar

Saat berurusan dengan lembar kerja raksasa (ratusan ribu baris), pertimbangkan untuk streaming output:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

---

## Tips Pro & Hal-hal yang Perlu Diwaspadai

- **Jangan lupa membuat direktori output** sebelum memanggil `Save`, jika tidak Anda akan mendapatkan `DirectoryNotFoundException`.
- **Waspadai pemisah desimal yang bergantung pada locale**. Jika lingkungan Anda menggunakan koma (`1,23`), setel `txtSaveOptions.DecimalSeparator = '.'` untuk memaksa titik.
- **Kompatibilitas versi**: Flag `PreserveNumericPrecision` diperkenalkan pada Aspose.Cells 20.6. Jika Anda menggunakan versi lebih lama, flag tersebut tidak ada dan Anda harus memformat sel sebagai teks sebelum menyimpan.

---

![Create new workbook example](excel-to-txt.png "Create new workbook")

*Image alt text: "Create new workbook and export Excel to TXT with numeric precision preserved"*

---

## Ringkasan – Apa yang Telah Dibahas

- **Create new workbook** menggunakan Aspose.Cells.  
- Isi sel dengan angka yang memiliki nol di akhir.  
- Setel `TxtSaveOptions.PreserveNumericPrecision = true` untuk **save excel as txt** tanpa kehilangan presisi.  
- Tulis file ke disk, lalu verifikasi bahwa output sesuai dengan nilai asli.  

Itulah alur kerja lengkap **convert worksheet to txt** dalam kurang dari 50 baris C#.

---

## Langkah Selanjutnya & Topik Terkait

Setelah Anda dapat **export excel to txt** dengan presisi sempurna, Anda mungkin ingin menjelajahi:

- **Ekspor ke CSV** dengan pemisah khusus (`TxtSaveOptions.Separator`).  
- **Menyimpan sebagai format teks lain** seperti TSV (`SaveFormat.TabDelimited`).  
- **Pemrosesan batch** banyak workbook dalam sebuah folder menggunakan `Directory.GetFiles`.  
- **Integrasi dengan Azure Functions** untuk konversi on‑demand di cloud.

Masing‑masing topik ini dibangun di atas pola yang sama `Workbook` → `Worksheet` → `TxtSaveOptions`, sehingga Anda akan merasa sangat familiar.

---

### Pemikiran Akhir

Jika Anda telah mengikuti langkah‑langkah di atas, kini Anda tahu persis cara **create new workbook**, mengisinya, dan **save worksheet as txt** sambil mempertahankan setiap digit desimal yang penting. Ini hanyalah potongan kode kecil, namun menyelesaikan masalah yang cukup umum ketika pipeline legacy menuntut input teks biasa.

Cobalah, sesuaikan opsi‑opsinya, dan biarkan data mengalir persis seperti yang Anda inginkan. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}