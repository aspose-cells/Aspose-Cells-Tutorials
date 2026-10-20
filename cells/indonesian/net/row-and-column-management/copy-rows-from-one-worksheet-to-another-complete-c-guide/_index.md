---
category: general
date: 2026-07-29
description: Salin baris dari satu lembar kerja ke lembar kerja lain dan pelajari
  cara memuat buku kerja Excel secara programatis menggunakan Aspose.Cells dalam tutorial
  langkah demi langkah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy rows from one worksheet to another
- load excel workbook programmatically
- Aspose.Cells copy rows
- C# Excel automation
- worksheet data transfer
language: id
lastmod: 2026-07-29
og_description: Salin baris dari satu lembar kerja ke lembar kerja lain menggunakan
  Aspose.Cells. Pelajari cara memuat buku kerja Excel secara programatik dan mempertahankan
  tabel pivot hanya dalam beberapa baris kode C#.
og_image_alt: Screenshot showing C# code that copies rows from one worksheet to another
  while preserving pivot tables
og_title: Salin baris dari satu lembar kerja ke lembar kerja lain – Panduan Otomatisasi
  Excel C#
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Copy rows from one worksheet to another and learn how to load Excel
    workbook programmatically using Aspose.Cells in a step‑by‑step tutorial.
  headline: Copy rows from one worksheet to another – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Replace `destinationWorkbook.Worksheets[0]` with `destinationWorkbook.Worksheets["TargetSheet"]`
      (create the sheet first if it doesn’t exist).
    question: Can I copy to a specific worksheet instead of the first one?
  - answer: Use `CopyRows` with the overload that accepts a `CopyRowsOptions` object
      and set `PasteType` to `PasteType.Values`.
    question: What if I need to copy only values, not formulas?
  - answer: Aspose.Cells supports **streaming** via `LoadOptions` with `MemorySetting.MemoryPreference`.
      Load the source workbook with a lower memory footprint and the copy operation
      will still be efficient.
    question: How do I handle large files without exhausting memory?
  - answer: When you set the `true` flag, the pivot cache is duplicated, so the new
      workbook’s pivots reference the copied data, not the original file.
    question: Do pivot tables stay linked to the original data source?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Salin baris dari satu lembar kerja ke lembar kerja lain – Panduan Lengkap C#
url: /id/net/row-and-column-management/copy-rows-from-one-worksheet-to-another-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salin baris dari satu lembar kerja ke lembar kerja lain – Panduan Lengkap C#

Pernah perlu **menyalin baris dari satu lembar kerja ke lembar kerja lain** tetapi tidak yakin bagaimana cara menjaga formula dan pivot table tetap utuh? Anda tidak sendirian. Dalam banyak pipeline pelaporan kami harus mengambil potongan data dari lembar master dan menaruhnya ke workbook baru untuk proses selanjutnya. Kabar baiknya? Dengan Aspose.Cells Anda dapat melakukannya secara programatis, dan seluruh operasi hanya membutuhkan beberapa baris kode.

Dalam tutorial ini kami akan menuntun Anda memuat workbook Excel secara programatis, memilih rentang, dan kemudian menyalin baris‑baris tersebut ke workbook baru sambil mempertahankan pivot table yang ada. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat dipakai ulang dan dapat disisipkan ke proyek C# mana pun—tanpa perlu menyalin‑tempel secara manual.

## Apa yang Akan Anda Capai

- **Muat workbook Excel secara programatis** menggunakan kelas `Workbook` dari Aspose.Cells.  
- Tentukan **area sel** yang berisi baris‑baris yang ingin dipindahkan.  
- **Salin baris dari satu lembar kerja ke lembar kerja lain** dengan satu pemanggilan metode yang tetap menjaga pivot table tetap hidup.  
- Simpan hasilnya ke file baru siap didistribusikan atau diproses lebih lanjut.

### Prasyarat

- .NET 6.0 atau lebih baru (kode ini bekerja pada .NET Core dan .NET Framework).  
- Lisensi Aspose.Cells yang valid (atau kunci evaluasi sementara).  
- Dua folder di disk: satu untuk workbook sumber (`Source.xlsx`) dan satu untuk tujuan (`Destination.xlsx`).  

Jika Anda sudah menyiapkan semua itu, mari kita mulai.

## Langkah 1: Muat workbook Excel secara programatis

Hal pertama—sebelum Anda dapat menyalin apa pun, Anda harus memuat file sumber ke memori. Aspose.Cells membuat ini sangat mudah:

```csharp
using Aspose.Cells;

// Load the source workbook from disk
Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");
```

> **Mengapa ini penting:** Memuat workbook secara programatis memberi Anda kontrol penuh atas isi file tanpa harus membuka Excel di server. Ini juga menghindari masalah interop COM dan bekerja di lingkungan tanpa UI seperti pipeline CI.

## Langkah 2: Tentukan rentang sumber yang berisi baris‑baris tersebut

Selanjutnya, tentukan secara tepat baris‑baris mana yang ingin Anda transfer. Objek `CellArea` memungkinkan Anda menentukan blok persegi panjang menggunakan alamat sel kiri‑atas dan kanan‑bawah:

```csharp
// Define the area A1:H20 – adjust as needed
CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");
```

> **Tips profesional:** Jika ukuran data Anda berubah secara dinamis, Anda dapat menghitung `EndRow` dengan `sourceWorksheet.Cells.MaxDataRow` untuk selalu menangkap seluruh tabel.

## Langkah 3: Buat workbook baru untuk tujuan

Sekarang buat workbook kosong yang akan menerima baris‑baris yang disalin. Secara default workbook ini dimulai dengan satu lembar kerja:

```csharp
// Create a new, empty workbook
Workbook destinationWorkbook = new Workbook();
```

> **Mengapa workbook baru?** Memulai dari nol memastikan Anda tidak secara tidak sengaja menimpa data yang sudah ada dan memberi Anda lingkungan yang dapat diprediksi untuk pengujian.

## Langkah 4: Salin baris dari satu lembar kerja ke lembar kerja lain (mempertahankan pivot table)

Berikut inti dari tutorial. Metode `CopyRows` menyalin baris‑baris yang dipilih dan, ketika Anda memberikan `true` sebagai argumen terakhir, juga menyalin pivot table yang berada di dalam rentang tersebut:

```csharp
// Perform the copy operation
destinationWorkbook.Worksheets[0].Cells.CopyRows(
    sourceWorkbook.Worksheets[0],      // source worksheet
    sourceRange.StartRow,              // first row to copy (0‑based)
    sourceRange.EndRow,                // last row to copy (inclusive)
    destinationWorkbook.Worksheets[0].Cells, // target worksheet
    0,                                 // target start row (top of sheet)
    true);                             // preserve pivot tables
```

### Apa yang terjadi di balik layar?

- **Lembar kerja sumber**: `sourceWorkbook.Worksheets[0]` menunjuk ke lembar pertama di file sumber.  
- **Indeks baris**: Aspose.Cells menggunakan indeks berbasis nol, sehingga `StartRow` dan `EndRow` sesuai dengan baris‑baris yang Anda definisikan di `sourceRange`.  
- **Baris mulai tujuan**: Kami memulai di baris 0 pada lembar baru, sehingga blok yang disalin ditempatkan tepat di atas.  
- **Flag `true`**: Inilah saklar ajaib yang memberi tahu Aspose.Cells untuk menggandakan semua pivot table yang berada di dalam baris yang disalin, mempertahankan cache dan koneksinya.

> **Peringatan kasus tepi:** Jika rentang sumber berisi sel yang digabung yang meluas di luar area yang didefinisikan, penggabungan tersebut akan terpotong. Untuk mempertahankannya, perlebarilah rentang sehingga mencakup seluruh wilayah yang digabung.

## Langkah 5: Simpan workbook tujuan

Akhirnya, tulis file baru ke disk. Anda dapat memilih folder mana saja; pastikan proses memiliki izin menulis:

```csharp
// Save the result
destinationWorkbook.Save(@"C:\Data\Destination.xlsx");
```

Saat Anda membuka `Destination.xlsx` Anda akan melihat baris A1‑H20 terduplikasi, lengkap dengan pivot table yang semula tertanam. Sisanya tetap kosong, siap bagi Anda menambahkan lembar kerja atau data lain nanti.

## Contoh Lengkap yang Dapat Dijalankan

Menggabungkan semuanya, berikut program lengkap yang dapat dijalankan:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook programmatically
        Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");

        // 2️⃣ Define the source range (adjust as needed)
        CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");

        // 3️⃣ Create a new destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 4️⃣ Copy rows from one worksheet to another, preserving pivot tables
        destinationWorkbook.Worksheets[0].Cells.CopyRows(
            sourceWorkbook.Worksheets[0],
            sourceRange.StartRow,
            sourceRange.EndRow,
            destinationWorkbook.Worksheets[0].Cells,
            0,
            true);

        // 5️⃣ Save the result
        destinationWorkbook.Save(@"C:\Data\Destination.xlsx");

        Console.WriteLine("Rows successfully copied! Check C:\\Data\\Destination.xlsx");
    }
}
```

**Output yang diharapkan** (console):

```
Rows successfully copied! Check C:\Data\Destination.xlsx
```

Buka file tujuan dan verifikasi bahwa data, format, serta pivot table terlihat persis seperti di sumber. Jika ada data yang hilang, periksa kembali bahwa `sourceRange` benar‑benar meliputi semua baris yang relevan.

## Pertanyaan Umum & Tips

- **Bisakah saya menyalin ke lembar kerja tertentu selain yang pertama?**  
  Tentu saja. Ganti `destinationWorkbook.Worksheets[0]` dengan `destinationWorkbook.Worksheets["TargetSheet"]` (buat lembar tersebut terlebih dahulu jika belum ada).

- **Bagaimana jika saya hanya ingin menyalin nilai, bukan formula?**  
  Gunakan `CopyRows` dengan overload yang menerima objek `CopyRowsOptions` dan atur `PasteType` menjadi `PasteType.Values`.

- **Bagaimana cara menangani file besar tanpa kehabisan memori?**  
  Aspose.Cells mendukung **streaming** melalui `LoadOptions` dengan `MemorySetting.MemoryPreference`. Muat workbook sumber dengan jejak memori yang lebih kecil dan operasi penyalinan tetap efisien.

- **Apakah pivot table tetap terhubung ke sumber data asli?**  
  Ketika Anda mengatur flag `true`, cache pivot digandakan, sehingga pivot di workbook baru merujuk ke data yang disalin, bukan ke file asli.

## Penutup

Sekarang Anda tahu cara **menyalin baris dari satu lembar kerja ke lembar kerja lain** sambil menjaga semua pivot table tetap utuh, dan Anda telah melihat cara **memuat workbook Excel secara programatis** menggunakan Aspose.Cells. Pola ini menjadi dasar yang kuat untuk membangun pipeline pelaporan otomatis, skrip migrasi data, atau skenario apa pun yang memerlukan pemotongan data Excel secara dinamis.

Apa selanjutnya? Cobalah memperluas potongan kode ini untuk:

- Mengulang beberapa rentang sumber dan menggabungkannya ke dalam satu file tujuan.  
- Menerapkan pemformatan bersyarat setelah penyalinan untuk menyoroti metrik penting.  
- Mengekspor workbook akhir ke PDF atau CSV untuk konsumsi selanjutnya.

Silakan bereksperimen, dan jika Anda menemui kendala, tinggalkan komentar di bawah. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang memperluas teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Copy Rows in Excel Using Aspose.Cells for .NET&#58; A C# Guide](/cells/english/net/worksheet-management/copy-rows-excel-aspose-cells-net-guide/)
- [Copy Worksheet from One Workbook to Another using Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}