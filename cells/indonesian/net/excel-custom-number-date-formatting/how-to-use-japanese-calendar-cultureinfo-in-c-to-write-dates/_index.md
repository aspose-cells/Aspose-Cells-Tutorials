---
category: general
date: 2026-10-26
description: Pelajari cara menggunakan CultureInfo kalender Jepang dalam C# saat mem-parsing
  tanggal era dan memasukkannya ke dalam lembar kerja Excel dengan NPOI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: id
lastmod: 2026-10-26
og_description: Gunakan CultureInfo kalender Jepang di C# untuk mengurai tanggal era
  Reiwa dan menuliskannya ke lembar kerja Excel. Kode lengkap yang dapat dijalankan
  dengan penjelasan.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: Gunakan CultureInfo Kalender Jepang di C# – contoh lengkap Excel
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: Cara menggunakan CultureInfo kalender Jepang di C# untuk menulis tanggal ke
  Excel
url: /id/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menggunakan Japanese calendar CultureInfo di C# untuk menulis tanggal ke Excel

Jika Anda perlu **menggunakan Japanese calendar CultureInfo** saat bekerja dengan tanggal di C#, panduan ini menunjukkan cara melakukannya secara tepat. Anda akan belajar cara mengurai string tanggal yang berisi nama era Jepang (misalnya, *Reiwa 2/5/1*) dan kemudian menulis `DateTime` yang dihasilkan ke sel pertama lembar kerja Excel menggunakan pustaka NPOI.

Mengurai tanggal berbasis era tanpa `CultureInfo` yang tepat dapat menyebabkan `FormatException` atau nilai bulan/hari yang salah. Dengan mengonfigurasi `CultureInfo` ke kalender Jepang, Anda memastikan runtime .NET menginterpretasikan era dengan benar dan nilai yang Anda simpan di Excel cocok dengan notasi Jepang asli.

Dalam tutorial ini Anda akan:

* Membuat objek `CultureInfo` yang menggunakan kalender Jepang.
* Mengurai string tanggal era Jepang dengan `DateTime.Parse`.
* Menyisipkan `DateTime` yang diurai ke sel lembar kerja NPOI.
* Melihat program lengkap yang dapat dijalankan serta output yang diharapkan.

> **Prerequisites** – .NET 6.0+ (atau .NET Core 3.1+), paket **NPOI** NuGet, dan pemahaman dasar tentang C# serta penanganan file Excel.

---

## Apa yang Anda perlukan

| Item | Alasan |
|------|--------|
| **.NET SDK** (6.0 atau lebih baru) | Menyediakan runtime dan pustaka untuk `CultureInfo`. |
| **NPOI** (`NPOI` NuGet package) | Memungkinkan Anda membuat dan memanipulasi file Excel tanpa harus menginstal Office. |
| **Visual Studio Code**, **Visual Studio**, atau IDE C# apa pun | Untuk mengompilasi dan menjalankan contoh. |
| **Japanese era date string** (mis., `"Reiwa 2/5/1"`) | Menunjukkan penggunaan kalender Jepang. |

---

## Langkah 1: Instal NPOI

Buka terminal di folder proyek Anda dan jalankan:

```bash
dotnet add package NPOI --version 2.6.1
```

Paket ini menyediakan tipe `IWorkbook`, `ISheet`, dan `ICell` yang akan digunakan nanti.

---

## Langkah 2: Buat CultureInfo yang menggunakan kalender Jepang

Kalender Jepang adalah kalender berbasis era. Anda harus meminta varian *Japanese* dari locale `ja-JP` dan secara eksplisit mengatur kalender ke `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Mengapa ini penting** – Budaya default `ja-JP` menggunakan kalender Gregorian. Menetapkan kembali properti `Calendar` memastikan bahwa nama era seperti *Reiwa* dikenali selama penguraian.

---

## Langkah 3: Mengurai string tanggal era Jepang

Setelah `CultureInfo` dikonfigurasi, Anda dapat dengan aman mengurai string yang berisi nama era.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Output**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

Metode `Parse` menginterpretasikan *Reiwa 2* sebagai tahun Gregorian 2020, bulan 5, hari 1.

### Kasus tepi: menangani era yang tidak valid

Jika pengguna memberikan era yang tidak didukung (misalnya, `"Heisei 31/4/30"` setelah era Heisei berakhir), `DateTime.Parse` akan melempar `FormatException`. Bungkus pemanggilan tersebut dalam blok try‑catch untuk memberikan pesan kesalahan yang ramah:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## Langkah 4: Menulis DateTime yang diurai ke dalam lembar kerja Excel

Dengan objek `DateTime` siap, Anda dapat menyimpannya di sel Excel. NPOI secara otomatis memformat nilai `DateTime` sebagai tanggal Excel.

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Hasil** – Membuka *JapaneseEraDate.xlsx* menampilkan tanggal **2020‑05‑01** di sel A1.

### Mengapa menggunakan NPOI?

*Berfungsi di semua platform* (Windows, Linux, macOS) dan **tidak** memerlukan Microsoft Office. Hal ini membuat solusi cocok untuk pipeline CI, kontainer Docker, atau pemrosesan sisi server.

---

## Langkah 5: Program lengkap yang dapat dijalankan

Menggabungkan semuanya, berikut adalah aplikasi konsol lengkap yang mendemonstrasikan seluruh alur:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**Cara menjalankan**

```bash
dotnet run
```

Setelah dijalankan, Anda akan menemukan `JapaneseEraDate.xlsx` di folder proyek dengan tanggal yang telah diurai dengan benar.

---

## Kesalahan umum dan tips praktik terbaik

| Kesalahan | Perbaikan / Rekomendasi |
|-----------|--------------------------|
| Lupa mengatur `japaneseCulture.DateTimeFormat.Calendar` | Selalu tetapkan instance `JapaneseCalendar`; jika tidak, nama era tidak akan dikenali. |
| Menggunakan `DateTime.TryParse` tanpa `CultureInfo` khusus | Berikan `japaneseCulture` yang sama ke `TryParse` untuk menjaga konsistensi perilaku. |
| Mengharapkan Excel menampilkan nama era | Format tanggal bawaan Excel hanya Gregorian. Jika Anda membutuhkan era ditampilkan, simpan string asli di kolom terpisah atau buat format teks khusus. |
| Tidak menutup `FileStream` | Gunakan blok `using` (seperti yang ditunjukkan) untuk memastikan handle file segera dilepaskan. |
| Mencampur objek `CultureInfo` antar thread | `CultureInfo` aman untuk operasi baca‑saja di banyak thread, tetapi hindari mengubah properti `Calendar` setelah pengaturan awal. |

---

## Kesimpulan

Anda kini tahu cara **menggunakan Japanese calendar CultureInfo** di C# untuk secara akurat mengurai tanggal era Jepang dan menulis `DateTime` yang dihasilkan ke lembar kerja Excel dengan NPOI. Contoh lengkap mencakup konfigurasi, penguraian, penanganan kesalahan, dan output Excel, memberikan fondasi yang kuat untuk skenario pelaporan atau pertukaran data internasional apa pun.

Selanjutnya, Anda mungkin ingin mengeksplorasi:

* **Memformat tanggal dengan teks khusus** untuk mempertahankan nama era di dalam Excel.  
* **Membaca tanggal dari Excel** menggunakan `cell.DateCellValue` sambil menghormati kalender Jepang.  
* **Menerapkan teknik yang sama** untuk kalender berbasis era lainnya (mis., kalender Buddha Thailand) dengan mengganti `JapaneseCalendar` dengan subclass `Calendar` yang sesuai.

Silakan bereksperimen dengan string era yang berbeda, kumpulan data yang lebih besar, atau mengintegrasikan logika ini ke dalam API ASP.NET Core yang menghasilkan laporan Excel secara dinamis. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Create Excel Workbook with Japanese Calendar Dates – Full Guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to create Excel workbook and parse Japanese dates in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}