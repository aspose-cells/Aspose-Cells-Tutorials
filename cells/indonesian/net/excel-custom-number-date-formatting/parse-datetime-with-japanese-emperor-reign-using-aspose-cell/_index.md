---
category: general
date: 2026-09-24
description: Mengurai DateTime dengan masa pemerintahan kaisar Jepang menggunakan
  Aspose.Cells di C#. Aktifkan kalender era Jepang, tulis string era, dan dapatkan
  nilai DateTime yang akurat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: id
lastmod: 2026-09-24
og_description: Mengurai DateTime dengan Masa Pemerintahan Kaisar Jepang menggunakan
  Aspose.Cells dalam C#. Tutorial ini menunjukkan cara mengaktifkan kalender era Jepang,
  menulis string era, dan membaca kembali DateTime yang benar.
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: Mengurai DateTime dengan Masa Pemerintahan Kaisar Jepang menggunakan Aspose.Cells
  – Panduan C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: Mengurai DateTime dengan Masa Pemerintahan Kaisar Jepang menggunakan Aspose.Cells
url: /id/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengurai DateTime dengan Masa Pemerintahan Kaisar Jepang menggunakan Aspose.Cells

Jika Anda perlu **mengurai DateTime dengan Masa Pemerintahan Kaisar Jepang** dalam aplikasi .NET, panduan ini menunjukkan secara tepat cara melakukannya dengan Aspose.Cells. Dengan mengaktifkan kalender era Jepang, menulis string berbasis era, dan membaca nilai `DateTime` yang dihasilkan, Anda mendapatkan tanggal yang andal dan sensitif budaya tanpa manipulasi string manual.

Bekerja dengan tanggal era Jepang umum dalam keuangan, pemerintahan, dan sistem warisan yang masih menyimpan tanggal seperti “令和3年5月10日”. Tutorial ini mencakup alur kerja lengkap, mulai dari penyiapan proyek hingga memperoleh objek `DateTime` yang dapat Anda gunakan dalam perhitungan, pencatatan, atau tampilan UI.

## Apa yang akan Anda pelajari

- Cara menambahkan paket NuGet Aspose.Cells ke proyek C#.  
- Cara mengaktifkan **kalender era Jepang** melalui `Workbook.Settings`.  
- Cara menulis string tanggal era Jepang ke dalam sel dan membiarkan Aspose.Cells mengurai secara otomatis.  
- Cara membaca `DateTime` yang telah diurai menggunakan properti `DateTimeValue`.  

**Prasyarat**  
- .NET 6.0 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.7+).  
- Familiaritas dasar dengan C# dan Visual Studio (atau IDE apa pun).  
- Akses internet untuk mengunduh paket Aspose.Cells.

---

## Langkah 1: Instal Aspose.Cells

Buka folder proyek Anda di terminal atau NuGet Package Manager Console dan jalankan:

```bash
dotnet add package Aspose.Cells
```

Atau, di Visual Studio, klik kanan proyek → **Manage NuGet Packages** → cari **Aspose.Cells** dan klik **Install**.  
Ini menambahkan assembly `Aspose.Cells`, yang menyediakan `Workbook`, `Worksheet`, dan kemampuan penguraian yang kita perlukan.

## Langkah 2: Aktifkan kalender era Jepang

Aspose.Cells menonaktifkan penguraian era Jepang secara default. Anda harus mengaktifkannya melalui flag `Workbook.Settings.UseJapaneseEraCalendar`.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

Menetapkan `UseJapaneseEraCalendar` ke `true` memberi tahu perpustakaan untuk menafsirkan string yang berisi nama era (`令和`, `平成`, `昭和`, dll.) sesuai dengan aturan kalender resmi Jepang.

## Langkah 3: Tulis string tanggal era Jepang ke sebuah sel

Selanjutnya, dapatkan worksheet pertama dan letakkan string tanggal era Jepang ke sel **A1**.

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**Mengapa ini berhasil:**  
Ketika `UseJapaneseEraCalendar` aktif, `PutValue` memeriksa string, mendeteksi awalan era (`令和`), dan secara internal mengonversinya ke tahun Gregorian yang bersesuaian (2021). Perpustakaan kemudian menyimpan nilai tersebut sebagai objek `DateTime` yang sebenarnya, bukan sekadar teks.

## Langkah 4: Ambil nilai `DateTime` yang telah diurai

Sekarang baca `DateTimeValue` sel tersebut. Aspose.Cells secara otomatis mengembalikan tanggal Gregorian.

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

Menjalankan program mencetak:

```
Parsed Gregorian date: 2021-05-10
```

Output mengonfirmasi bahwa **Parse DateTime with Japanese Emperor Reign** berhasil mengonversi “令和3年5月10日” menjadi 10 Mei 2021.

## Langkah 5: Menangani kasus tepi dan variasi umum

### Berbagai format era
Aspose.Cells mengenali beberapa representasi era:

| Era (Jepang) | Rentang tahun Gregorian |
|--------------|--------------------------|
| 明治 (Meiji) | 1868‑1912                |
| 大正 (Taishō) | 1912‑1926                |
| 昭和 (Shōwa) | 1926‑1989                |
| 平成 (Heisei) | 1989‑2019                |
| 令和 (Reiwa) | 2019‑sekarang            |

Jika data sumber Anda mencampur karakter lebar penuh, spasi, atau menggunakan kanji “年”, “月”, “日”, parser tetap berhasil. Misalnya, `"平成31年4月30日"` menjadi `2019-04-30`.

### String tidak valid
Ketika string tidak dapat diurai (mis., `"令和99年13月40日"`), `DateTimeValue` mengembalikan `DateTime.MinValue`. Anda dapat memeriksa kondisi ini:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### Menonaktifkan fitur
Jika kemudian Anda perlu menyimpan string era mentah tanpa konversi, setel flag kembali ke `false`:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### Tips kinerja
Mengaktifkan kalender era menambah overhead kecil pada setiap pemanggilan `PutValue` yang melibatkan string. Jika Anda hanya mengurai beberapa sel, aktifkan flag tepat sebelum operasi dan nonaktifkan setelahnya untuk meminimalkan dampak.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin, tempel, dan jalankan secara langsung.

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**Output yang diharapkan**

```
Parsed Gregorian date: 2021-05-10
```

Program ini mendemonstrasikan alur end‑to‑end untuk **Parse DateTime with Japanese Emperor Reign** menggunakan Aspose.Cells, mulai dari pembuatan workbook hingga memperoleh objek `DateTime` yang dapat dipakai.

---

## Kesimpulan

Anda kini tahu cara **Mengurai DateTime dengan Masa Pemerintahan Kaisar Jepang** di C# dengan:

1. Menginstal **Aspose.Cells**.  
2. Mengaktifkan **kalender era Jepang** melalui `Workbook.Settings`.  
3. Menulis string berbasis era ke sel.  
4. Membaca `DateTimeValue` yang dihasilkan.  

Pendekatan ini menghilangkan logika penguraian manual, menghormati batas era resmi, dan terintegrasi mulus dengan kode penanganan tanggal .NET yang ada.  

**Langkah selanjutnya**  
- Jelajahi fitur budaya‑spesifik lain dari Aspose.Cells, seperti **C# date parsing** untuk kalender Hijriah atau Buddha Thailand.  
- Gabungkan teknik ini dengan **Workbook Settings** seperti `CalcEngine` untuk mengevaluasi formula yang merujuk pada tanggal era.  
- Gunakan `DateTime` yang telah diurai dalam pelaporan, penyimpanan basis data, atau komponen UI yang memerlukan tanggal Gregorian.

Silakan bereksperimen dengan berbagai string era, tangani input tidak valid, dan integrasikan solusi ini ke dalam pipeline impor data yang lebih besar. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to Parse Japanese Dates in C# – Complete Guide](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}