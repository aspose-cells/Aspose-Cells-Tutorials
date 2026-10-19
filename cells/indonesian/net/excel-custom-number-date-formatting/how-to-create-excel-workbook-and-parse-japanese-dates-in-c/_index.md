---
category: general
date: 2026-10-10
description: Buat buku kerja Excel di C# dan atur nilai sel dengan tanggal era Jepang,
  kemudian terapkan format khusus dan baca sel tanggal menggunakan Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set cell value
- apply custom format
- read date cell
- excel date parsing
language: id
lastmod: 2026-10-10
og_description: Buat workbook Excel di C# dan parsing tanggal era Jepang. Pelajari
  cara mengatur nilai sel, menerapkan format khusus, dan membaca sel tanggal dengan
  Aspose.Cells.
og_image_alt: Screenshot showing a C# program that creates an Excel workbook and parses
  a Japanese era date
og_title: Buat workbook Excel di C# – panduan lengkap untuk parsing tanggal
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and set cell value with a Japanese era
    date, then apply custom format and read date cell using Aspose.Cells.
  headline: How to create Excel workbook and parse Japanese dates in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Cara membuat workbook Excel dan mengurai tanggal Jepang di C#
url: /id/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat Excel workbook dan mengurai tanggal Jepang di C#

Jika Anda perlu **create Excel workbook** dari awal, panduan ini menunjukkan secara tepat cara melakukannya. Anda akan belajar **set cell value** dengan string tanggal era Jepang, **apply custom format** yang memahami era tersebut, dan akhirnya **read date cell** untuk memperoleh .NET `DateTime`. Contoh lengkap ini bekerja dengan Aspose.Cells untuk .NET versi terbaru, sehingga Anda dapat menyalin‑tempel kode ke proyek C# mana pun.

Bekerja dengan tanggal yang mencakup era Jepang dapat menjadi rumit karena parser Excel bawaan tidak mengenali simbol era. Dengan menggunakan custom number format (`[ja-JP-Era]`) Anda memberi tahu Excel cara menginterpretasikan string, memungkinkan **excel date parsing** yang dapat diandalkan. Langkah‑langkah di bawah ini mencakup seluruh alur kerja, dari pembuatan workbook hingga ekstraksi tanggal.

## Prasyarat

- .NET 6.0 atau lebih baru (kode juga dapat dijalankan pada .NET Framework 4.7+)
- Aspose.Cells untuk .NET (paket NuGet `Aspose.Cells`)
- Familiaritas dasar dengan C# dan Visual Studio atau IDE pilihan Anda

## Langkah 1: Buat Excel workbook dan tambahkan worksheet

Operasi pertama adalah **create Excel workbook** di memori. Aspose.Cells secara otomatis membuat worksheet default, tetapi Anda dapat menambahkan lebih banyak jika diperlukan.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Optional: rename the default worksheet for clarity
        workbook.Worksheets[0].Name = "Dates";
```

Membuat workbook mengalokasikan struktur internal yang nantinya menampung sel, gaya, dan formula. Tidak ada file yang ditulis pada tahap ini, sehingga operasi tetap cepat dan dapat diuji.

## Langkah 2: Set cell value dengan string tanggal era Jepang

Selanjutnya, **set cell value** ke representasi era Jepang `"R5-04-01"` (Reiwa 5, April 1). String tersebut mengikuti pola `EraYear-MM-DD`.

```csharp
        // Step 2: Reference cell A1 on the first worksheet
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Put the Japanese era date string into the cell
        dateCell.PutValue("R5-04-01");
```

Menggunakan `PutValue` menyimpan teks mentah. Excel akan memperlakukannya sebagai string sampai sebuah number format memberi tahu sebaliknya. Pendekatan ini bekerja untuk representasi kalender kustom apa pun, tidak hanya era Jepang.

## Langkah 3: Apply custom number format yang memahami era Jepang

Sekarang **apply custom format** agar Excel dapat menerjemahkan string era menjadi tanggal serial yang sebenarnya. Format `[ja-JP-Era]yyyy/MM/dd` memberi tahu mesin untuk menginterpretasikan karakter era di depan (`R` untuk Reiwa) dan menghitung tanggal Gregorian.

```csharp
        // Step 3: Apply a custom number format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";
```

Custom format disimpan dalam objek style sel. Aspose.Cells menghormati format ini selama proses rendering maupun konversi nilai, memungkinkan **excel date parsing** yang dapat diandalkan di kemudian hari dalam pipeline.

## Langkah 4: Ambil nilai DateTime yang diurai dari sel

Akhirnya, **read date cell** untuk memperoleh .NET `DateTime`. Properti `DateTimeValue` mengembalikan nilai yang telah dikonversi berdasarkan custom format yang diterapkan sebelumnya.

```csharp
        // Step 4: Retrieve the parsed DateTime value
        DateTime parsedDate = dateCell.DateTimeValue;

        // Output the result to the console for verification
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
```

Saat program dijalankan, konsol akan mencetak:

```
Parsed Gregorian date: 2023-04-01
```

Output tersebut mengonfirmasi bahwa string era Jepang `"R5-04-01"` telah diinterpretasikan dengan benar sebagai 1 April 2023.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua bagian menghasilkan program mandiri yang dapat Anda kompilasi dan jalankan segera.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Reference cell A1
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Insert Japanese era date string
        dateCell.PutValue("R5-04-01");

        // Apply custom format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";

        // Retrieve the parsed DateTime
        DateTime parsedDate = dateCell.DateTimeValue;

        // Show the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");

        // (Optional) Save the workbook to verify the visual format
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Menjalankan program membuat `JapaneseEraDate.xlsx` dengan sel A1 menampilkan `2023/04/01` sementara konsol menampilkan tanggal Gregorian yang sama. File tersebut dapat dibuka di Excel untuk melihat nilai yang diformat.

## Mengapa pendekatan ini berhasil

- **create excel workbook** – Menginstansiasi `Workbook` membangun struktur file Excel lengkap di memori tanpa menyentuh disk.
- **set cell value** – `PutValue` menyimpan teks mentah, yang diperlukan sebelum menerapkan format khusus budaya.
- **apply custom format** – Token `[ja-JP-Era]` menjembatani kesenjangan antara notasi era dan sistem tanggal serial internal Excel.
- **read date cell** – `DateTimeValue` secara otomatis menggunakan style sel untuk melakukan konversi, memberikan Anda `DateTime` native.
- **excel date parsing** – Dengan mendelegasikan parsing ke style sel, Anda menghindari manipulasi string manual, mengurangi bug dan meningkatkan dukungan lokal.

## Kasus tepi dan tips praktis

- **Different eras** – Gunakan `S` untuk Showa, `H` untuk Heisei, `R` untuk Reiwa. String format yang sama bekerja untuk semua era.
- **Invalid strings** – Jika sel berisi tanggal era yang tidak valid, `DateTimeValue` mengembalikan `DateTime.MinValue`. Periksa `dateCell.IsDate` sebelum membaca.
- **Multiple cells** – Terapkan custom format ke seluruh rentang (`range.ApplyStyle(style)`) ketika Anda perlu mengurai banyak tanggal.
- **Performance** – Menetapkan style sekali per kolom lebih cepat daripada per‑sel untuk lembar besar.
- **Saving options** – **Saving options** – Aspose.Cells dapat menghasilkan XLSX, XLS, CSV, atau PDF. Pilih format yang sesuai dengan proses selanjutnya.

## Pertanyaan yang sering diajukan

**Bisakah saya menggunakan budaya .NET bawaan alih-alih custom format?**  
Kelas .NET `CultureInfo` tidak memahami simbol era Jepang dengan cara yang sama seperti Excel. Menggunakan custom number format adalah metode paling dapat diandalkan untuk **excel date parsing** string era.

**Bagaimana jika saya perlu menulis kembali tanggal ke Excel dalam format era?**  
Set nilai sel ke `DateTime` dan terapkan custom format yang sama. Excel akan menampilkan era secara otomatis.

**Apakah ini bekerja pada versi Excel yang lebih lama?**  
Token `[ja-JP-Era]` didukung oleh Excel 2010 ke atas. Aspose.Cells meniru perilaku tersebut, sehingga workbook ditampilkan dengan benar bahkan ketika dibuka di versi Excel lama yang tidak memiliki dukungan era native.

## Kesimpulan

Anda kini tahu cara **create Excel workbook**, **set cell value** dengan string era Jepang, **apply custom format**, dan **read date cell** untuk mendapatkan `DateTime`. Pola ini menyediakan **excel date parsing** yang kuat tanpa penanganan string manual, menjadikan kode otomatisasi C# Anda ringkas dan dapat diandalkan.

Selanjutnya, jelajahi topik terkait seperti **formatting multiple date columns**, **working with other cultural calendars**, atau **exporting the workbook to PDF**. Setiap ekstensi dibangun di atas prinsip yang sama yang dibahas di sini, sehingga Anda dapat menyesuaikan solusi untuk berbagai skenario lokalisasi. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang dibangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Excel Workbook di C# – Terapkan Custom Number Format](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/)
- [Buat Excel Workbook dengan Custom Format – Panduan C#](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-custom-format-c-guide/)
- [Otomatisasi Excel dengan Aspose.Cells .NET: Buat Workbook & Atur Tautan Eksternal](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}