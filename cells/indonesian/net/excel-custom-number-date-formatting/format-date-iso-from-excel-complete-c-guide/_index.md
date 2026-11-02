---
category: general
date: 2026-03-30
description: Pelajari cara memformat tanggal ISO saat Anda membaca nilai tanggal‑waktu
  Excel dan mengekstrak data tanggal‑waktu Excel menggunakan Aspose.Cells di C#.
draft: false
keywords:
- format date iso
- read excel datetime
- extract datetime excel
- Aspose.Cells date parsing
- Japanese era dates
language: id
og_description: Format tanggal ISO dari data Excel menggunakan Aspose.Cells. Panduan
  ini menunjukkan cara membaca datetime Excel, mengekstrak nilai datetime Excel, dan
  menghasilkan tanggal ISO.
og_title: Format Tanggal ISO dari Excel – Tutorial C# Langkah-demi-Langkah
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Format Tanggal ISO dari Excel – Panduan C# Lengkap
url: /id/net/excel-custom-number-date-formatting/format-date-iso-from-excel-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# format date iso dari Excel – Panduan Lengkap C#

Pernahkah Anda perlu **format date iso** saat mengambil tanggal dari lembar Excel? Mungkin Anda sedang menangani tanggal era Jepang, atau Anda hanya menginginkan string `yyyy‑MM‑dd` yang bersih untuk payload API. Dalam tutorial ini Anda akan melihat secara tepat cara **read Excel datetime** sel, **extract datetime Excel** nilai, dan mengubahnya menjadi format ISO‑8601—tanpa tebakan.

Kami akan menelusuri contoh dunia nyata yang menggunakan Aspose.Cells, menjelaskan mengapa setiap baris penting, dan menunjukkan output akhir yang dapat Anda salin‑tempel ke proyek Anda. Pada akhir tutorial, Anda akan dapat menangani string era aneh seperti “令和3年5月1日” dan menghasilkan tanggal ISO standar, siap untuk basis data, JSON, atau ke mana pun Anda membutuhkannya.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Framework)
- Aspose.Cells untuk .NET (versi percobaan gratis atau berlisensi)
- Familiaritas dasar dengan C# dan konsep Excel
- Visual Studio atau editor C# apa pun yang Anda suka

Tidak ada paket NuGet tambahan yang diperlukan selain Aspose.Cells, jadi penyiapannya cukup sederhana.

---

## Langkah 1: Buat Workbook dan Targetkan Worksheet Pertama

Hal pertama yang Anda lakukan adalah membuat objek `Workbook` baru. Ini memberi Anda representasi dalam memori dari file Excel, yang kemudian dapat Anda manipulasi atau baca.

```csharp
using Aspose.Cells;
using System.Globalization;

// Step 1: Initialize a new workbook and grab the first worksheet
Workbook workbook = new Workbook();                 // creates an empty .xlsx
Worksheet worksheet = workbook.Worksheets[0];      // the default sheet is "Sheet1"
```

*Mengapa ini penting:*  
Membuat workbook secara programatik memungkinkan Anda menghindari berkas fisik selama pengujian. Ini juga memastikan referensi worksheet selalu valid—tidak ada kejutan null‑reference nanti ketika Anda mencoba **read Excel datetime** nilai.

---

## Langkah 2: Tulis String Tanggal Era Jepang ke dalam Sel

Tujuan kami adalah mendemonstrasikan parsing tanggal non‑Gregorian. Kami akan menempatkan string era langsung ke sel **A1**.

```csharp
// Step 2: Insert a Japanese era date string into cell A1
worksheet.Cells["A1"].PutValue("令和3年5月1日");
```

*Tip pro:* Jika Anda mengambil data dari workbook yang sudah ada, Anda dapat melewatkan pemanggilan `PutValue` dan langsung merujuk ke sel yang sudah berisi tanggal. Kuncinya adalah sel tersebut memuat **string** yang mewakili tanggal dalam kalender lunisolar Jepang.

---

## Langkah 3: Konfigurasikan Kultur yang Memahami Kalender Lunisolar Jepang

Kelas `CultureInfo` .NET memungkinkan Anda menentukan bagaimana tanggal harus diinterpretasikan. Dengan menukar kalender Gregorian default ke `JapaneseLunisolarCalendar`, Anda memberi parser konteks yang dibutuhkan.

```csharp
// Step 3: Set up a culture using the Japanese lunisolar calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();
```

*Mengapa kita melakukan ini:*  
Jika Anda mencoba mem-parsing “令和3年5月1日” dengan kultur default, .NET akan melempar `FormatException`. Menukar ke kalender lunisolar memberi runtime petunjuk tepat bagaimana memetakan “令和3年” (tahun ke‑3 era Reiwa) ke tahun Gregorian 2021.

---

## Langkah 4: Parse Nilai Sel sebagai `DateTime` Menggunakan Kultur yang Dikonfigurasi

Sekarang masuk ke inti operasi—mengubah string era tersebut menjadi objek `DateTime` yang tepat. Aspose.Cells menyediakan overload `GetDateTime` yang menerima `CultureInfo`.

```csharp
// Step 4: Retrieve the cell value as a DateTime, respecting the Japanese culture
DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);
```

*Apa yang terjadi di balik layar:*  
`GetDateTime` membaca string mentah, menerapkan aturan kalender kultur yang diberikan, dan mengembalikan `DateTime` yang mewakili momen yang sama dalam kalender Gregorian. Inilah saat Anda **extract datetime Excel** data dalam bentuk yang dapat diproses di .NET.

---

## Langkah 5: Tampilkan Tanggal yang Telah Diparse dalam Format ISO 8601

Akhirnya, kami memformat `DateTime` sebagai string ISO—`yyyy‑MM‑dd`—yang diterima secara universal oleh API, basis data, dan kerangka kerja front‑end.

```csharp
// Step 5: Print the date in ISO format (e.g., 2021-05-01)
Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // Output: 2021-05-01
```

*Mengapa ISO?*  
ISO 8601 menghilangkan ambiguitas. “05/01/2021” bisa berarti 1 Mei atau 5 Januari tergantung locale. `2021-05-01` jelas sekali, itulah mengapa kami **format date iso** dalam hampir setiap skenario integrasi.

---

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap dijalankan. Salin ke proyek aplikasi konsol, tambahkan referensi Aspose.Cells, dan tekan **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and select the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // 3️⃣ Set up Japanese lunisolar culture
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();

        // 4️⃣ Parse the cell value as DateTime using the culture
        DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);

        // 5️⃣ Output the date in ISO format
        Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // 2021-05-01
    }
}
```

**Expected output**

```
2021-05-01
```

Jalankan sekali, dan Anda akan melihat tanggal berformat ISO tercetak ke konsol. Itulah seluruh alur dari **read Excel datetime** ke **format date iso**.

---

## Menangani Kasus Edge yang Umum

### 1. Sel yang Berisi Angka Tanggal Excel Nyata

Kadang Excel menyimpan tanggal sebagai nomor serial (mis., `44204`). Dalam kasus ini, Anda tidak memerlukan kultur; cukup panggil `GetDateTime()` tanpa parameter:

```csharp
DateTime serialDate = worksheet.Cells["B2"].GetDateTime(); // B2 holds a numeric date
Console.WriteLine(serialDate.ToString("yyyy-MM-dd"));
```

### 2. Sel Kosong atau Tidak Valid

Jika sel kosong atau berisi string yang tidak dapat diparse, `GetDateTime` akan melempar. Bungkus pemanggilan dalam `try/catch` atau periksa `IsDateTime` terlebih dahulu:

```csharp
if (worksheet.Cells["C3"].Type == CellValueType.IsDateTime)
{
    DateTime safeDate = worksheet.Cells["C3"].GetDateTime();
    Console.WriteLine(safeDate.ToString("yyyy-MM-dd"));
}
else
{
    Console.WriteLine("Cell C3 does not contain a valid date.");
}
```

### 3. Format Era yang Berbeda

Era Jepang lainnya (Heisei, Showa) mengikuti pola yang sama. `JapaneseLunisolarCalendar` yang sama akan menangani mereka secara otomatis, jadi Anda tidak memerlukan logika tambahan—cukup beri stringnya.

---

## Pro Tips & Gotchas

- **Performance:** Saat memproses spreadsheet besar, gunakan kembali satu instance `CultureInfo` alih‑alih membuat yang baru di dalam loop.
- **Thread Safety:** Objek `CultureInfo` bersifat read‑only setelah Anda mengatur kalender, sehingga aman dibagikan antar thread.
- **Aspose.Cells Licensing:** Jika Anda menggunakan versi percobaan gratis, ingat bahwa beberapa fitur mungkin terbatas setelah masa percobaan berakhir. Parsing tanggal yang ditunjukkan di sini berfungsi baik dalam mode percobaan maupun berlisensi.
- **Time Zones:** `DateTime` yang Anda dapatkan **unspecified** (tanpa zona waktu). Jika Anda memerlukan UTC, panggil `DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc)` atau konversi menggunakan `TimeZoneInfo`.

---

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **format date iso** dari workbook Excel menggunakan C#. Mulai dari string era Jepang mentah, kami **read Excel datetime**, menyiapkan kultur yang tepat, **extract datetime excel** data, dan akhirnya menghasilkan string ISO‑8601 yang bersih. Pendekatan ini bekerja untuk representasi tanggal apa pun yang mungkin dilemparkan Excel kepada Anda, baik itu nomor serial, string spesifik locale, atau format era tradisional.

Langkah selanjutnya? Coba iterasi seluruh kolom tanggal, tulis hasil ISO kembali ke sheet baru, atau kirimkan langsung ke payload JSON untuk layanan web. Jika Anda penasaran dengan sistem kalender lain (Ibrani, Islam), Aspose.Cells dan `CultureInfo` .NET membuat eksperimen tersebut sama mudahnya.

Ada pertanyaan atau format tanggal rumit yang belum terpecahkan? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}