---
category: general
date: 2026-03-22
description: Pelajari cara memformat datetime ke ISO saat mengekstrak tanggal dari
  Excel dan menampilkan tanggal ISO menggunakan Aspose.Cells dalam C#.
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: id
og_description: Memformat datetime ke ISO menjadi mudah. Panduan ini menunjukkan cara
  mengekstrak tanggal dari Excel dan menampilkan tanggal ISO dengan Aspose.Cells.
og_title: Format datetime ke ISO di C# – Tutorial Langkah demi Langkah
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: Format datetime ke ISO di C# – Panduan Lengkap
url: /id/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# format datetime ke iso di C# – Panduan Lengkap

Pernah perlu **format datetime ke iso** tetapi sumbernya berada di dalam workbook Excel? Mungkin sel tersebut berisi era Jepang seperti “令和3年5月1日” dan Anda kebingungan bagaimana mengubahnya menjadi string bersih `2021‑05‑01`. Anda tidak sendirian. Dalam tutorial ini kami akan **mengekstrak tanggal dari excel**, mengurai era Jepang, dan kemudian **menampilkan tanggal iso** di konsol—semua dengan beberapa baris C# dan Aspose.Cells.

Kami akan membahas semua yang Anda perlukan: paket NuGet yang diperlukan, kode tepat yang dapat Anda salin‑tempel, mengapa setiap baris penting, dan beberapa tips untuk kasus tepi. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali untuk memformat datetime ke iso tidak peduli seberapa unik nilai Excel aslinya.

## Apa yang Anda Butuhkan

- .NET 6.0 atau lebih baru (kode ini juga dapat dikompilasi pada .NET Framework 4.6+)
- Visual Studio 2022 (atau editor lain yang Anda sukai)
- Paket NuGet **Aspose.Cells for .NET** – `Install-Package Aspose.Cells`
- File Excel (atau workbook baru) yang berisi tanggal dalam format era Jepang

Itu saja. Tanpa pustaka tambahan, tanpa interop COM, hanya satu metode yang terdokumentasi dengan baik.

## Langkah 1: Buat Workbook dan Tulis Tanggal Era Jepang  

Pertama, kita memerlukan workbook untuk bekerja. Jika Anda sudah memiliki file Excel, Anda dapat memuatnya dengan `new Workbook("path")`. Untuk contoh ini kami akan membuat workbook baru di memori dan menaruh string era Jepang ke sel **A1**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **Mengapa kami melakukan ini:** Aspose.Cells memperlakukan nilai sel sebagai string secara default. Dengan menyisipkan teks era mentah kami mensimulasikan skenario dunia nyata di mana klien Jepang memasukkan tanggal menggunakan kalender asli mereka.

## Langkah 2: Aktifkan Penguraian Era Jepang dan Ekstrak Tanggal  

Aspose.Cells dapat secara otomatis menerjemahkan string era Jepang menjadi objek .NET `DateTime`—asalkan Anda memberi tahu. Flag `DateTimeParseOptions.EnableJapaneseEra` melakukan pekerjaan berat tersebut.

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **Pro tip:** Jika Anda lupa menambahkan opsi `EnableJapaneseEra`, pustaka akan mengembalikan string asli, dan konversi selanjutnya akan gagal. Selalu periksa `parsed.Type` jika Anda menangani konten campuran.

## Langkah 3: Konversi DateTime yang Telah Diurai ke ISO 8601  

Setelah kita memiliki `DateTime` yang tepat, mengubahnya menjadi string berformat ISO sangat mudah. Pola `"yyyy-MM-dd"` mematuhi bagian tanggal ISO 8601, yang merupakan format yang paling banyak diharapkan oleh API.

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

Menjalankan program akan mencetak:

```
ISO date: 2021-05-01
```

Itulah **menampilkan tanggal iso** yang Anda cari.

## Contoh Lengkap yang Dapat Dijalankan  

Berikut adalah blok kode lengkap yang dapat Anda salin langsung ke proyek console. Tanpa dependensi tersembunyi, tanpa konfigurasi tambahan.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **Output yang diharapkan:** `ISO date: 2021-05-01`

## Penjabaran Langkah‑per‑Langkah (Mengapa Setiap Bagian Penting)

| Langkah | Apa yang Terjadi | Mengapa Penting |
|------|--------------|--------------------|
| **Buat workbook** | Menginisialisasi kontainer Excel dalam memori. | Memberikan sandbox untuk menguji tanpa menyentuh sistem file. |
| **PutValue** | Menyimpan string era Jepang mentah ke **A1**. | Meniru entri data nyata; memastikan parser melihat teks persis. |
| **GetValue dengan `EnableJapaneseEra`** | Mengubah string era menjadi .NET `DateTime`. | Menangani konversi kalender secara otomatis—tanpa tabel lookup manual. |
| **`ToString("yyyy-MM-dd")`** | Memformat `DateTime` ke ISO 8601. | Menjamin string tanggal yang tidak bergantung pada budaya, dapat diurutkan, dan diterima oleh REST API, basis data, dll. |
| **Console.WriteLine** | Menampilkan tanggal ISO akhir. | Mengonfirmasi seluruh alur kerja berfungsi dari ujung ke ujung. |

## Menangani Variasi Umum  

### 1. Lokasi Sel yang Berbeda  

Jika tanggal Anda berada di **B2** atau rentang bernama, cukup ganti `"A1"` dengan alamat yang sesuai:

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. Banyak Tanggal dalam Satu Kolom  

Ketika Anda perlu **mengekstrak tanggal dari excel** untuk banyak baris, lakukan loop melalui range yang digunakan:

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. Cadangan untuk Tanggal Bukan Era  

Jika sel sudah berisi string tanggal standar, parser tetap berfungsi, tetapi Anda mungkin menginginkan jaring pengaman:

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

Flag `TryParse` mencegah pengecualian dan mengembalikan nilai asli bila konversi gagal.

### 4. Komponen Waktu  

Jika Anda juga memerlukan bagian waktu, gunakan `"yyyy-MM-ddTHH:mm:ss"`:

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

Itu menghasilkan timestamp ISO 8601 lengkap (`2021-05-01T00:00:00`).

## Bantuan Visual  

![contoh format datetime ke iso](image.png "Contoh format datetime ke iso dalam C#")

*Alt text:* *contoh format datetime ke iso menampilkan output konsol*

## Pertanyaan yang Sering Diajukan  

- **Apakah saya dapat menggunakan ini dengan file .xls?**  
  Ya. Aspose.Cells mendukung `.xls`, `.xlsx`, `.csv`, dan banyak format lain secara bawaan.

- **Bagaimana jika workbook diproteksi password?**  
  Muat dengan `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })`.

- **Apakah format ISO tergantung locale?**  
  Tidak. Pola `"yyyy-MM-dd"` tidak bergantung pada budaya, menjamin string yang sama di mesin mana pun.

- **Apakah ini bekerja di .NET Core?**  
  Tentu—Aspose.Cells kompatibel dengan .NET Standard 2.0.

## Penutup  

Kami telah membahas cara **format datetime ke iso** dengan **mengekstrak tanggal dari excel**, mengurai string era Jepang, dan akhirnya **menampilkan tanggal iso** di konsol. Langkah inti—membuat workbook, menulis atau memuat teks era, mengaktifkan penguraian era Jepang, dan memformat dengan `ToString("yyyy-MM-dd")`—adalah semua yang Anda perlukan untuk kebanyakan skenario.

Selanjutnya, Anda mungkin ingin:

- Menulis kembali tanggal ISO ke kolom lain untuk pemrosesan lebih lanjut.
- Mengekspor workbook yang telah diubah ke CSV untuk impor massal.
- Menggabungkan logika ini dengan API web yang menerima unggahan Excel dan mengembalikan tanggal ISO dalam format JSON.

Silakan bereksperimen dengan format tanggal lain, zona waktu, atau bahkan kalender khusus. Fleksibilitas Aspose.Cells berarti Anda jarang menemui batas.

Selamat coding, semoga semua tanggal Anda selalu sesuai ISO!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}