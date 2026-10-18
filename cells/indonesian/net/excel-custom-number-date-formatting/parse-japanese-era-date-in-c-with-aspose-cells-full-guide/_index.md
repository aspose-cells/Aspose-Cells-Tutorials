---
category: general
date: 2026-06-08
description: Mengurai tanggal era Jepang di C# menggunakan Aspose.Cells. Pelajari
  bagaimana CultureInfo ja-JP dan format era Jepang memungkinkan konversi tanggal
  Excel yang akurat.
draft: false
keywords:
- parse japanese era date
- Aspose.Cells
- CultureInfo ja-JP
- Japanese era format
- Excel date conversion
- C# DateTime parsing
language: id
og_description: Mengurai tanggal era Jepang di C# dengan cepat. Tutorial ini menunjukkan
  bagaimana CultureInfo ja-JP dan Aspose.Cells mengubah string era menjadi objek DateTime
  yang tepat.
og_title: Mengurai Tanggal Era Jepang di C# – Panduan Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  headline: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  type: TechArticle
- description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  name: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  steps:
  - name: 5.1 Invalid or Empty Strings
    text: '```csharp string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString();
      // could be empty if (string.IsNullOrWhiteSpace(maybeDate)) { Console.WriteLine("Cell
      B1 is empty – skipping."); } else { // Attempt to parse; catch format exceptions
      try { DateTime dt = DateTime.Parse(maybeDate, new Cultur'
  - name: 5.2 Older Eras (Showa, Taisho)
    text: 'The same `CultureInfo ja-JP` works for older eras automatically:'
  - name: 5.3 Using `DateTime.ParseExact` for Strict Validation
    text: 'If you want to enforce the exact Japanese era pattern, use a custom format
      string:'
  type: HowTo
- questions:
  - answer: Yes. As long as the workbook’s `Settings.CultureInfo` is set to `ja-JP`
      *before* you call `GetDateTime()`, Aspose.Cells will interpret the existing
      strings correctly.
    question: Does this work with .xlsx files that already contain era dates?
  - answer: The parsing returns a `DateTime` with `Kind = Unspecified`. If you need
      UTC or local time, apply `DateTime.SpecifyKind` or convert after parsing.
    question: What about time zones?
  - answer: Absolutely. Loop through the desired range and call `GetDateTime()` on
      each cell—just remember to handle exceptions for malformed entries.
    question: Can I parse multiple cells at once?
  type: FAQPage
tags:
- C#
- Excel
- DateTime
- Localization
title: Mengurai Tanggal Era Jepang di C# dengan Aspose.Cells – Panduan Lengkap
url: /id/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengurai Tanggal Era Jepang di C# dengan Aspose.Cells – Panduan Lengkap

Pernahkah Anda perlu **mengurai tanggal era Jepang** langsung dari lembar Excel? Mungkin Anda menarik data dari sistem warisan yang masih menggunakan “令和3年5月12日” dan Anda menginginkan `DateTime` yang bersih untuk menjalankan laporan. Dalam tutorial ini kami akan membahas contoh lengkap yang siap dijalankan yang mengubah string bergaya era tersebut menjadi tanggal C# yang tepat—tanpa tebak‑tebakan.

Kami akan menggunakan **Aspose.Cells**, perpustakaan .NET yang kuat untuk manipulasi Excel, bersama dengan pengaturan **CultureInfo ja-JP** yang dapat membaca era Jepang. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali untuk menangani “令和”, “平成”, dan bahkan era yang lebih lama tanpa kesulitan.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga berfungsi pada .NET Framework 4.6+ )  
- Aspose.Cells untuk .NET (Anda dapat mengunduh paket NuGet trial gratis: `Install-Package Aspose.Cells`)  
- Familiaritas dasar C#—tidak perlu hal yang rumit, cukup aplikasi console saja  
- IDE pilihan Anda (Visual Studio, Rider, VS Code, dll.)

Itu saja. Tidak ada layanan tambahan, tidak ada parser pihak ketiga yang obscure.

## Langkah 1: Siapkan Proyek dan Tambahkan Aspose.Cells

Pertama, buat proyek console baru:

```bash
dotnet new console -n JapaneseEraParser
cd JapaneseEraParser
dotnet add package Aspose.Cells
```

Sekarang buka **Program.cs** dan tambahkan namespace yang diperlukan:

```csharp
using System;
using System.Globalization;
using Aspose.Cells;
```

> **Pro tip:** Jika Anda menggunakan Visual Studio, IDE akan menyarankan penambahan pernyataan `using` secara otomatis setelah Anda mengetik nama kelas.

## Langkah 2: Buat Workbook dan Terapkan Budaya Jepang

Kunci untuk **mengurai tanggal era Jepang** dengan benar adalah memberi tahu Aspose.Cells budaya apa yang akan digunakan. Menetapkan `CultureInfo` ke `ja-JP` mengaktifkan penguraian yang sadar era.

```csharp
// Step 2: Initialize a new workbook and set Japanese culture
Workbook workbook = new Workbook();
workbook.Settings.CultureInfo = new CultureInfo("ja-JP");
```

Mengapa ini penting? Kalender Jepang memiliki banyak era (misalnya *Reiwa* (令和), *Heisei* (平成)). Objek `CultureInfo` berisi `JapaneseCalendar` yang mengetahui tanggal mulai setiap era, sehingga string apa pun yang mengikuti format era Jepang dapat diinterpretasikan dengan tepat.

## Langkah 3: Tulis String Tanggal Era Jepang ke Sel

Mari masukkan contoh tanggal era ke sel **A1**. Anda bebas mengubah string untuk menguji era yang berbeda.

```csharp
// Step 3: Put a Japanese era date string into A1
string japaneseDate = "令和3年5月12日"; // Reiwa 3, May 12, 2021
workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);
```

Jika Anda lebih suka bekerja dengan workbook yang sudah ada, Anda dapat memuatnya dengan `new Workbook("path/to/file.xlsx")` dan melewati langkah pembuatan.

## Langkah 4: Ambil Nilai sebagai Objek DateTime C#

Sekarang keajaiban terjadi. Dengan memanggil `GetDateTime()`, Aspose.Cells membaca sel menggunakan `CultureInfo` yang telah diset sebelumnya dan mengembalikan `DateTime` yang tepat.

```csharp
// Step 4: Parse the cell value into a DateTime
DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

**Output yang diharapkan**

```
Parsed DateTime: 2021-05-12
```

Itulah seluruh alur **mengurai tanggal era Jepang**—empat baris kode yang singkat.

## Langkah 5: Menangani Kasus Tepi dan Era Alternatif

Data dunia nyata tidak selalu bersih. Berikut beberapa skenario yang mungkin Anda temui dan cara menanganinya.

### 5.1 String Tidak Valid atau Kosong

```csharp
string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString(); // could be empty
if (string.IsNullOrWhiteSpace(maybeDate))
{
    Console.WriteLine("Cell B1 is empty – skipping.");
}
else
{
    // Attempt to parse; catch format exceptions
    try
    {
        DateTime dt = DateTime.Parse(maybeDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"B1 parsed as {dt:yyyy-MM-dd}");
    }
    catch (FormatException)
    {
        Console.WriteLine($"Unable to parse '{maybeDate}' as a Japanese era date.");
    }
}
```

### 5.2 Era Lebih Lama (Showa, Taisho)

`CultureInfo ja-JP` yang sama bekerja otomatis untuk era yang lebih lama:

```csharp
string showaDate = "昭和45年12月31日"; // Showa 45 = 1970-12-31
DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
Console.WriteLine(showaParsed.ToString("yyyy-MM-dd")); // 1970-12-31
```

### 5.3 Menggunakan `DateTime.ParseExact` untuk Validasi Ketat

Jika Anda ingin menegakkan pola era Jepang yang tepat, gunakan string format khusus:

```csharp
string pattern = "ggggy年M月d日"; // gggg = era name, y = year in era
DateTime strictDate = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
Console.WriteLine(strictDate); // 2021-05-12 00:00:00
```

Pendekatan ini akan melempar `FormatException` ketika string menyimpang, yang berguna untuk pemeriksaan kualitas data.

## Contoh Kerja Lengkap

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke **Program.cs** dan jalankan.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and set Japanese culture
        Workbook workbook = new Workbook();
        workbook.Settings.CultureInfo = new CultureInfo("ja-JP");

        // 2️⃣ Insert a Japanese era date string
        string japaneseDate = "令和3年5月12日";
        workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);

        // 3️⃣ Parse the cell value into DateTime
        DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");

        // 4️⃣ Demonstrate handling an older era
        string showaDate = "昭和45年12月31日";
        DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"Showa parsed: {showaParsed:yyyy-MM-dd}");

        // 5️⃣ Strict parsing with ParseExact
        string pattern = "gggy年M月d日";
        try
        {
            DateTime strict = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
            Console.WriteLine($"Strict parse: {strict:yyyy-MM-dd}");
        }
        catch (FormatException ex)
        {
            Console.WriteLine($"Strict parse failed: {ex.Message}");
        }
    }
}
```

Jalankan dengan `dotnet run` dan Anda akan melihat:

```
Parsed DateTime: 2021-05-12
Showa parsed: 1970-12-31
Strict parse: 2021-05-12
```

Boom—**mengurai tanggal era Jepang** selesai, dan Anda memiliki templat untuk era apa pun yang mungkin Anda temui.

![Alur kerja Mengurai Tanggal Era Jepang – menampilkan pembuatan workbook, pengaturan budaya, penulisan sel, dan pemanggilan GetDateTime](parse-japanese-era-date.png "Diagram yang menggambarkan cara mengurai tanggal era Jepang menggunakan Aspose.Cells dan CultureInfo ja-JP")

## Pertanyaan Umum yang Dijawab

- **Apakah ini bekerja dengan file .xlsx yang sudah berisi tanggal era?**  
  Ya. Selama `Settings.CultureInfo` workbook diatur ke `ja-JP` *sebelum* Anda memanggil `GetDateTime()`, Aspose.Cells akan menginterpretasikan string yang ada dengan benar.

- **Bagaimana dengan zona waktu?**  
  Penguraian mengembalikan `DateTime` dengan `Kind = Unspecified`. Jika Anda memerlukan UTC atau waktu lokal, gunakan `DateTime.SpecifyKind` atau konversi setelah penguraian.

- **Bisakah saya mengurai beberapa sel sekaligus?**  
  Tentu saja. Loop melalui rentang yang diinginkan dan panggil `GetDateTime()` pada setiap sel—hanya ingat untuk menangani pengecualian pada entri yang tidak sesuai format.

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **mengurai tanggal era Jepang** dalam C# menggunakan Aspose.Cells dan `CultureInfo ja-JP` bawaan. Dari menyiapkan workbook, menulis string berformat era, mengambil `DateTime` yang bersih, hingga menangani kasus tepi seperti era lama dan validasi ketat—panduan ini memberikan solusi siap produksi.

Selanjutnya, Anda dapat menjelajahi **konversi tanggal Excel** untuk tanggal serial numerik, atau menyelami **penguraian DateTime C#** dengan kalender khusus untuk locale lain. Pola yang sama berlaku untuk kalender Buddha Thailand, kalender Ibrani, dan lainnya—cukup ganti `CultureInfo`.

Ada tantangan khusus yang Anda hadapi? Tinggalkan komentar, dan mari kita selesaikan bersama. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang berhubungan erat dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menerapkan Validasi Tanggal di .NET Menggunakan Aspose.Cells: Panduan Komprehensif](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Ubah Sistem Tanggal Excel ke 1904 menggunakan Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Konversi Excel ke PDF secara Efisien dengan Format Tanggal Kustom Menggunakan Aspose.Cells untuk Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}