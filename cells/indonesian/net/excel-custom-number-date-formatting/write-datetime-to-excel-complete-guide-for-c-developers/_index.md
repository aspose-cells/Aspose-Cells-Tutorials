---
category: general
date: 2026-04-07
description: Tuliskan datetime ke Excel menggunakan C#. Pelajari cara menyisipkan
  tanggal ke dalam lembar kerja, menangani nilai tanggal sel Excel, dan mengonversi
  tanggal kalender Jepang dalam beberapa langkah saja.
draft: false
keywords:
- write datetime to excel
- excel cell date value
- insert date into worksheet
- convert japanese calendar date
language: id
og_description: Tulis datetime ke Excel dengan cepat. Panduan ini menunjukkan cara
  menyisipkan tanggal ke dalam lembar kerja, mengelola nilai tanggal sel Excel, dan
  mengonversi tanggal kalender Jepang dengan C#.
og_title: Menulis tanggal dan waktu ke Excel – Tutorial C# Langkah demi Langkah
tags:
- C#
- Excel automation
- Aspose.Cells
title: Menulis datetime ke Excel – Panduan Lengkap untuk Pengembang C#
url: /id/net/excel-custom-number-date-formatting/write-datetime-to-excel-complete-guide-for-c-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menulis datetime ke Excel – Panduan Lengkap untuk Pengembang C#

Pernah perlu **menulis datetime ke Excel** tetapi tidak yakin panggilan API mana yang sebenarnya menyimpan tanggal Excel yang tepat? Anda tidak sendirian. Dalam banyak alat perusahaan kita harus menaruh `DateTime` C# ke dalam spreadsheet, dan hasilnya harus berperilaku seperti tanggal Excel yang sesungguhnya—dapat diurutkan, difilter, dan siap untuk pivot table.  

Dalam tutorial ini kami akan memandu langkah‑langkah *menyisipkan tanggal ke worksheet* menggunakan Aspose.Cells, menjelaskan mengapa pengaturan budaya penting, dan bahkan menunjukkan cara **mengonversi tanggal kalender Jepang** menjadi `DateTime` biasa sebelum menuliskannya. Pada akhir tutorial Anda akan memiliki potongan kode mandiri yang dapat disalin‑tempel ke proyek .NET mana pun.

## Apa yang Anda Butuhkan

- **.NET 6+** (atau versi .NET terbaru; kode ini juga bekerja di .NET Framework)  
- **Aspose.Cells for .NET** – paket NuGet yang memungkinkan Anda memanipulasi file Excel tanpa harus menginstal Office.  
- Pemahaman dasar tentang `DateTime` C# dan budaya (culture).  

Tidak ada pustaka tambahan, tidak ada interop COM, dan tidak memerlukan instalasi Excel. Jika Anda sudah memiliki instance worksheet (`ws`), Anda siap melanjutkan.

## Langkah 1: Siapkan Budaya Jepang (Konversi Tanggal Kalender Jepang)

Ketika Anda menerima tanggal seperti `"R02/05/01"` (Reiwa 2, 1 Mei) Anda harus memberi tahu .NET cara menafsirkan simbol era. Kalender Jepang bukan kalender Gregorian default, jadi kita buat `CultureInfo` yang mengganti kalendernya dengan `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;   // Make sure Aspose.Cells is referenced

// Assume you already have a worksheet instance named "ws"
Worksheet ws = /* your worksheet instance */;

// 1️⃣ Configure a Japanese culture that uses the Japanese calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

**Mengapa ini penting:**  
Jika Anda mem‑parse string dengan budaya default, .NET akan melempar pengecualian format karena tidak dapat memetakan `R` (era Reiwa) ke tahun. Dengan menukar ke `JapaneseCalendar`, parser memahami simbol era dan menerjemahkannya ke tahun Gregorian yang benar.

## Langkah 2: Parse String Berbasis Era menjadi `DateTime`

Setelah budaya siap, kita dapat dengan aman memanggil `DateTime.ParseExact`. String format `"ggyy/MM/dd"` memberi tahu parser:

- `gg` – penanda era (misalnya `R` untuk Reiwa)  
- `yy` – dua digit tahun dalam era tersebut  
- `MM/dd` – bulan dan hari.

```csharp
// 2️⃣ Parse a date string in the Japanese era format (ggyy/MM/dd)
string japaneseDate = "R02/05/01";          // Reiwa 2, May 1st
DateTime parsedDate = DateTime.ParseExact(
    japaneseDate,
    "ggyy/MM/dd",
    japaneseCulture,
    DateTimeStyles.None
);
```

**Tips profesional:** Jika Anda mungkin menerima tanggal dalam format lain (misalnya `"Heisei 30/12/31"`), bungkus parsing dalam `try/catch` dan gunakan fallback ke `DateTime.TryParseExact`. Itu mencegah seluruh proses impor Anda crash karena satu baris yang buruk.

## Langkah 3: Tulis `DateTime` ke Sel Excel (Nilai Tanggal Sel Excel)

Aspose.Cells memperlakukan `DateTime` .NET sebagai tanggal Excel native ketika Anda menggunakan `PutValue`. Pustaka secara otomatis mengonversi ticks menjadi nomor seri Excel (jumlah hari sejak 1900‑01‑00). Ini berarti sel akan menampilkan **nilai tanggal sel Excel** yang tepat dan Anda dapat memformatnya nanti menggunakan gaya tanggal bawaan Excel.

```csharp
// 3️⃣ Write the resulting DateTime value into cell C1 of the worksheet
Cell targetCell = ws.Cells["C1"];
targetCell.PutValue(parsedDate);

// Optional: apply a standard date format so users see "yyyy-MM-dd"
targetCell.Style.Number = 14;   // built‑in Excel format ID for "m/d/yy"
```

**Apa yang akan Anda lihat di Excel:**  
Sel C1 kini berisi nomor seri `44796`, yang Excel menampilkan sebagai `2020‑05‑01` (atau format apa pun yang Anda terapkan). Nilai dasarnya adalah tanggal sesungguhnya, bukan string, sehingga penyortiran berfungsi sebagaimana mestinya.

## Langkah 4: Simpan Workbook (Penutup)

Jika Anda belum menyimpan workbook, lakukan sekarang. Langkah ini tidak secara langsung berhubungan dengan menulis datetime, tetapi melengkapi alur kerja.

```csharp
// Save the workbook to a file (or a MemoryStream if you need it in‑memory)
Workbook workbook = ws.Workbook;   // get the parent workbook
workbook.Save("Output.xlsx", SaveFormat.Xlsx);
```

Itu saja—empat langkah singkat, dan Anda telah berhasil **menulis datetime ke Excel**, sekaligus menangani tanggal era Jepang.

---

![contoh menulis datetime ke excel](/images/write-datetime-to-excel.png "Tangkapan layar yang menunjukkan proyek C# menulis DateTime ke sel Excel C1")

*Gambar di atas menggambarkan file Excel akhir dengan tanggal yang ditampilkan dengan benar di sel C1.*

## Pertanyaan Umum & Kasus Pojok

### Bagaimana jika variabel worksheet belum siap?

Anda dapat membuat workbook baru secara langsung:

```csharp
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];   // default first sheet
```

### Bagaimana cara mempertahankan string era Jepang asli di sheet?

Jika Anda membutuhkan kedua string asli dan tanggal yang sudah diparse, tulis keduanya ke sel yang berdekatan:

```csharp
ws.Cells["B1"].PutValue(japaneseDate);   // original text
ws.Cells["C1"].PutValue(parsedDate);     // parsed DateTime
```

### Apakah ini bekerja dengan versi .NET yang lebih lama?

Ya. `JapaneseCalendar` sudah ada sejak .NET 2.0, dan Aspose.Cells mendukung .NET Framework 4.5+. Pastikan Anda merujuk ke assembly yang tepat.

### Bagaimana dengan zona waktu?

`DateTime.ParseExact` mengembalikan **Kind** `Unspecified`. Jika tanggal sumber Anda dalam UTC, konversikan terlebih dahulu:

```csharp
DateTime utcDate = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
DateTime localDate = utcDate.ToLocalTime();
targetCell.PutValue(localDate);
```

### Bisakah saya mengatur format tanggal khusus (misalnya “yyyy年MM月dd日”)?

Tentu. Gunakan properti `Style.Custom`:

```csharp
targetCell.Style.Custom = "yyyy\"年\"mm\"月\"dd\"日\"";
```

Sekarang Excel akan menampilkan `2020年05月01日` sambil tetap menyimpan nilai tanggal yang sesungguhnya.

## Ringkasan

Kami telah membahas semua yang Anda perlukan untuk **menulis datetime ke Excel** dari C#:

1. **Konfigurasikan** budaya Jepang dengan `JapaneseCalendar` untuk **mengonversi tanggal kalender Jepang**.  
2. **Parse** string berbasis era menggunakan `DateTime.ParseExact`.  
3. **Sisipkan** `DateTime` yang dihasilkan ke dalam sel, memastikan **nilai tanggal sel Excel** yang tepat.  
4. **Simpan** workbook agar data tetap tersimpan.

Dengan empat langkah ini Anda dapat dengan aman **menyisipkan tanggal ke worksheet** terlepas dari format sumber. Kode ini sepenuhnya dapat dijalankan, hanya memerlukan Aspose.Cells, dan berfungsi pada runtime .NET modern mana pun.

## Apa Selanjutnya?

- **Impor massal:** Loop baris dalam CSV, parse setiap tanggal Jepang, dan tulis ke sel berurutan.  
- **Styling:** Terapkan conditional formatting untuk menyorot tanggal jatuh tempo.  
- **Performa:** Gunakan `WorkbookDesigner` atau caching `CellStyle` saat menangani ribuan baris.  

Silakan bereksperimen—ganti era Jepang dengan kalender Gregorian, ubah sel target, atau output ke format file lain (CSV, ODS). Ide dasarnya tetap sama: parse, konversi, dan **menulis datetime ke Excel** dengan percaya diri.

Selamat coding, semoga spreadsheet Anda selalu dapat diurutkan dengan benar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}