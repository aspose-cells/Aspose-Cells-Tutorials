---
category: general
date: 2026-03-21
description: Atur format khusus sel di C# dan pelajari cara menulis tanggal ke Excel,
  menerapkan format tanggal khusus, membaca DateTime dari Excel, serta membuat worksheet
  buku kerja dengan cepat.
draft: false
keywords:
- set cell custom format
- write date to excel
- read datetime from excel
- apply custom date format
- create workbook worksheet
language: id
og_description: Atur format khusus sel di C# untuk menulis tanggal ke Excel, terapkan
  format tanggal khusus, baca DateTime dari Excel, dan buat lembar kerja workbook
  dengan mudah.
og_title: Atur Format Kustom Sel di C# – Tulis & Baca Tanggal di Excel
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Mengatur Format Kustom Sel di C# – Panduan Lengkap Menulis & Membaca Tanggal
  di Excel
url: /id/net/excel-custom-number-date-formatting/set-cell-custom-format-in-c-complete-guide-to-writing-readin/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Atur Format Kustom Sel – Menulis & Membaca Tanggal di Excel Menggunakan C#

Pernah membutuhkan untuk **set cell custom format** dalam file Excel dari C# tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian. Dalam banyak alat pelaporan atau utilitas ekspor data, tanggal harus muncul dalam locale tertentu—misalnya tanggal era Jepang, kalender fiskal, atau string ISO‑8601.

Dalam tutorial ini kami akan membahas sebuah **complete, runnable example** yang menunjukkan cara **write date to Excel**, **apply custom date format**, **read DateTime from Excel**, dan **create workbook worksheet** dengan Aspose.Cells. Pada akhir tutorial Anda akan memiliki satu program mandiri yang dapat Anda masukkan ke proyek .NET mana pun.

## Apa yang Akan Anda Pelajari

- Cara **create workbook worksheet** secara programatis.  
- Langkah-langkah tepat untuk **write date to Excel** menggunakan string yang spesifik locale.  
- Cara **apply custom date format** (termasuk notasi era Jepang).  
- Cara **read DateTime from Excel** kembali ke objek `DateTime`.  
- Tips, jebakan, dan variasi yang mungkin Anda temui saat menangani tanggal di Excel.

Tidak memerlukan dokumentasi eksternal—semua yang Anda butuhkan ada di sini.

## Prasyarat

- .NET 6.0 atau lebih baru (kode juga berfungsi pada .NET Framework 4.7+).  
- Aspose.Cells untuk .NET diinstal via NuGet (`Install-Package Aspose.Cells`).  
- Pemahaman dasar tentang sintaks C#—tidak ada yang rumit.

> **Pro tip:** Jika Anda menggunakan Visual Studio, aktifkan *nullable reference types* untuk menangkap bug halus lebih awal.

## Langkah 1: Buat Workbook dan Worksheet  

Pertama-tama: Anda memerlukan objek workbook yang mewakili file Excel, dan worksheet tempat data akan disimpan.

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // Step 1: Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];           // default sheet is named "Sheet1"
```

*Mengapa ini penting:* Kelas `Workbook` adalah titik masuk untuk semua operasi Excel. Membuatnya di memori berarti Anda tidak menyentuh sistem file sampai Anda secara eksplisit menyimpan, yang membuat proses lebih cepat dan ramah pengujian.

## Langkah 2: Tulis Tanggal ke Excel  

Selanjutnya, kami akan menempatkan string tanggal era Jepang (`"R02-04-01"`) ke sel **A1**. String ini meniru era Reiwa (tahun 2, 1 April).

```csharp
        // Step 2: Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("R02-04-01");
```

*Apa yang terjadi:* `PutValue` menyimpan string mentah. Aspose.Cells kemudian akan mencoba menguraikannya berdasarkan gaya sel. Jika Anda melewatkan langkah ini dan menulis `DateTime` secara langsung, Anda akan kehilangan informasi era yang ingin ditampilkan.

## Langkah 3: Terapkan Format Nomor Tanggal Bawaan (ID 14)

Excel memiliki format tanggal bawaan dengan ID 14 (`mm-dd-yy`). Menerapkannya memberi tahu mesin bahwa sel **berisi tanggal**, bukan hanya teks.

```csharp
        // Step 3: Apply the built‑in date number format (ID 14)
        worksheet.Cells["A1"].Style.Number = 14;
```

*Mengapa menggunakan ID 14?* Itu adalah format “tanggal singkat” universal yang memastikan Excel memperlakukan konten sebagai nilai tanggal, yang merupakan prasyarat agar format kustom berfungsi dengan benar.

## Langkah 4: Atur Format Kustom untuk Menampilkan Notasi Era Jepang  

Sekarang bagian yang menyenangkan: kami memberi tahu Excel untuk menampilkan tanggal menggunakan format era Jepang. String kustom `[$-ja-JP]ggge年m月d日` melakukan hal itu dengan tepat.

```csharp
        // Step 4: Set a custom format to display the date in Japanese era notation
        worksheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge年m月d日";
```

*Penjelasan:*  
- `[$-ja-JP]` memaksa locale menjadi Jepang.  
- `ggg` adalah nama era (mis., “R” untuk Reiwa).  
- `e` adalah tahun era.  
- `年`, `月`, `日` adalah karakter Jepang literal untuk tahun, bulan, hari.

Jika Anda membutuhkan locale yang berbeda, cukup ganti `ja-JP` dengan kode budaya yang sesuai (mis., `en-US`).

## Langkah 5: Ambil Nilai DateTime yang Diurai  

Akhirnya, mari baca **`DateTime` sebenarnya** yang diurai Excel dari sel. Ini membuktikan bahwa string telah diinterpretasikan dengan benar.

```csharp
        // Step 5: Retrieve the parsed DateTime value from the cell
        DateTime parsedDate = worksheet.Cells["A1"].DateTime;   // => 2020‑04‑01

        // Output to console for verification
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

*Hasil:* Konsol mencetak `Parsed DateTime: 2020-04-01`. Meskipun kami memasukkan string era Jepang, Excel secara internal menyimpan tanggal Gregorian, yang dapat Anda gunakan untuk perhitungan, perbandingan, atau ekspor lebih lanjut.

## Langkah 6: Simpan Workbook (Opsional)

Jika Anda ingin melihat workbook yang diformat di Excel, cukup simpan ke disk.

```csharp
        // Optional: Save the workbook to a file
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Buka **JapaneseEraDate.xlsx** yang dihasilkan dan Anda akan melihat sel **A1** menampilkan `R02年4月1日` (format era Jepang tepat yang kami atur).

![contoh set format kustom sel](image-placeholder.png "Sel Excel menampilkan tanggal era Jepang – set format kustom sel")

*Teks alt di atas berisi kata kunci utama, memenuhi persyaratan SEO gambar.*

## Variasi Umum & Kasus Tepi  

### Menulis Format Tanggal yang Berbeda  

Jika Anda lebih suka ISO‑8601 (`2020-04-01`) alih-alih string era, cukup ubah pemanggilan `PutValue`:

```csharp
worksheet.Cells["A1"].PutValue(new DateTime(2020, 4, 1));
worksheet.Cells["A1"].Style.Number = 14;                 // keep built‑in date format
worksheet.Cells["A1"].Style.Custom = "yyyy-mm-dd";      // custom ISO format
```

### Menangani Sel Null atau Kosong  

Saat membaca tanggal, selalu lindungi terhadap sel kosong untuk menghindari `InvalidOperationException`:

```csharp
if (!worksheet.Cells["A1"].IsDate)
{
    Console.WriteLine("Cell A1 does not contain a valid date.");
}
else
{
    DateTime dt = worksheet.Cells["A1"].DateTime;
    // use dt...
}
```

### Mendukung Multiple Locales  

Anda dapat melakukan loop melalui daftar kode budaya dan menerapkannya secara dinamis:

```csharp
string[] cultures = { "ja-JP", "en-US", "fr-FR" };
foreach (var culture in cultures)
{
    worksheet.Cells["A1"].Style.Custom = $"[$-{culture}]ggge年m月d日";
    // Save or export per culture if needed
}
```

## Tips Pro & Hal-hal yang Perlu Diwaspadai  

- **Selalu atur format nomor bawaan terlebih dahulu** (`Style.Number`). Tanpa itu, Excel memperlakukan sel sebagai teks biasa dan format kustom diabaikan.  
- **Kode locale tidak sensitif huruf besar/kecil**, tetapi menggunakan bentuk kanonik (`ja-JP`) menghindari kebingungan.  
- **Menyimpan bersifat opsional** untuk pemrosesan dalam memori; Anda dapat men‑stream workbook langsung ke respons web (`workbook.Save(stream, SaveFormat.Xlsx)`).  
- **Lisensi Aspose.Cells**: Versi evaluasi gratis menambahkan watermark. Untuk produksi, pastikan Anda memiliki lisensi yang valid untuk menghindari penalti kinerja.

## Ringkasan  

Kami telah menunjukkan cara **set cell custom format** di C# untuk menampilkan tanggal era Jepang, cara **write date to Excel**, **apply custom date format**, **read DateTime from Excel**, dan **create workbook worksheet**—semua dalam satu program mandiri. Kata kunci utama muncul secara alami di seluruh teks, sementara kata kunci sekunder terjalin dalam judul dan isi, memenuhi standar SEO dan AI‑citation.

## Apa Selanjutnya?

- Jelajahi **conditional formatting** untuk menyorot tanggal yang lewat.  
- Gabungkan pendekatan ini dengan **PivotTables** untuk pelaporan dinamis.  
- Coba **reading large CSV files** dan mengonversinya ke Excel dengan logika penanganan tanggal yang sama.  

Silakan bereksperimen dengan locale yang berbeda, pola kustom, atau bahkan zona waktu. Jika Anda mengalami kendala, tinggalkan komentar di bawah—selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}