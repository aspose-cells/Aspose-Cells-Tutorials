---
category: general
date: 2026-10-13
description: Buat workbook Excel di C# dan tulis tanggal ke Excel menggunakan Aspose.Cells.
  Pelajari cara menyimpan file Excel sebagai xlsx dan menambahkan tanggal ke lembar
  kerja dengan kode lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save excel file
- write date to excel
- save workbook as xlsx
- add date to worksheet
language: id
lastmod: 2026-10-13
og_description: Buat buku kerja Excel di C# dan tulis tanggal ke Excel. Ikuti panduan
  lengkap ini untuk menyimpan file Excel sebagai xlsx dan menambahkan tanggal ke lembar
  kerja dengan Aspose.Cells.
og_image_alt: Excel workbook screenshot showing a Japanese imperial date in cell A1
og_title: Buat buku kerja Excel dan tambahkan tanggal ke lembar kerja – C# langkah
  demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Create excel workbook in C# and write date to excel using Aspose.Cells.
    Learn to save excel file as xlsx and add date to worksheet with full code.
  headline: Create excel workbook and add date to worksheet in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Buat buku kerja Excel dan tambahkan tanggal ke lembar kerja di C#
url: /id/net/excel-workbook/create-excel-workbook-and-add-date-to-worksheet-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat workbook Excel dan tambahkan tanggal ke worksheet di C#

Jika Anda perlu **create excel workbook** secara programatis, panduan ini menunjukkan cara **write date to excel** dan **save excel file** sebagai workbook *.xlsx*. Anda akan melihat contoh lengkap yang dapat dijalankan yang mem‑parsing string era kekaisaran Jepang dan menyimpan `DateTime` yang dihasilkan di sel A1.

Bekerja dengan Excel dari C# sering memerlukan tiga langkah: menginstansiasi workbook, menaruh data ke worksheet, dan akhirnya menyimpan file. Tutorial ini mencakup setiap langkah, menjelaskan mengapa kode ditulis seperti itu, dan menyoroti jebakan umum seperti parsing yang spesifik budaya dan izin sistem file. Pada akhir Anda dapat **add date to worksheet**, **save workbook as xlsx**, dan mengadaptasi pola ini untuk tipe data apa pun.

> **Prasyarat** – Contoh ini menggunakan pustaka **Aspose.Cells for .NET** (versi 23.10 atau lebih baru). Instal melalui NuGet:

```bash
dotnet add package Aspose.Cells
```

Anda juga memerlukan SDK .NET 6+ dan direktori yang dapat ditulisi untuk file output.

---

## Buat workbook Excel dan konfigurasikan worksheet

Langkah pertama adalah menginstansiasi workbook kosong dan mengambil worksheet defaultnya. Aspose.Cells secara otomatis membuat workbook dengan satu lembar bernama “Sheet1”.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

// Step 1: Create a new workbook
Workbook workbook = new Workbook();

// Step 2: Get the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];
```

**Mengapa ini penting** – `Workbook` adalah titik masuk untuk semua operasi Excel. Dengan membuatnya tanpa parameter Anda mendapatkan workbook bersih yang kemudian dapat **save excel file** dalam format apa pun yang Anda pilih.

## Parse tanggal kekaisaran Jepang

Tanggal kekaisaran Jepang menggunakan simbol era (misalnya, “R” untuk Reiwa) diikuti oleh tahun dua digit. Metode .NET `DateTime.ParseExact` dapat menangani format ini ketika Anda menyediakan objek `DateTimeParseOptions` khusus yang memberi tahu parser untuk menggunakan kalender Kaisar Jepang.

```csharp
// Step 3: Define a date string in the Japanese imperial era
string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

// Step 4: Configure parsing options for the Japanese Emperor calendar
var parseOptions = new DateTimeParseOptions
{
    Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
};

// Step 5: Parse the string into a .NET DateTime
DateTime parsedDate = DateTime.ParseExact(
    imperialDate,
    "ggyy/MM/dd",
    CultureInfo.InvariantCulture,
    DateTimeStyles.None,
    parseOptions);
```

**Penjelasan** –  
* `gg` membaca penanda era (`R` untuk Reiwa).  
* `yy` membaca tahun dua digit dalam era tersebut.  
* `MM/dd` membaca bulan dan hari.  

Jika Anda menghilangkan `parseOptions`, parser mengasumsikan kalender Gregorian dan melempar `FormatException`. Ini adalah kasus tepi umum saat berurusan dengan kalender non‑Gregorian.

## Tulis tanggal ke worksheet

Sekarang Anda memiliki nilai `DateTime`, Anda dapat menempatkannya ke dalam sel. Aspose.Cells secara otomatis memformat sel berdasarkan tipe nilai.

```csharp
// Step 6: Write the parsed date into cell A1
sheet.Cells["A1"].PutValue(parsedDate);

// Optional: Apply a date format for better readability
Style style = workbook.CreateStyle();
style.Custom = "yyyy-mm-dd";
sheet.Cells["A1"].SetStyle(style);
```

**Mengapa mengatur gaya?** – Tanpa gaya, Excel mungkin menampilkan tanggal menggunakan format default sistem, yang dapat membingungkan pengguna di locale lain. Menetapkan secara eksplisit `"yyyy-mm-dd"` memastikan tampilan yang konsisten.

## Simpan file excel sebagai xlsx

Akhirnya, simpan workbook ke disk. Metode `Save` menentukan format output dari ekstensi file, sehingga menggunakan “.xlsx” secara otomatis memicu format Office Open XML.

```csharp
// Step 7: Define the output path (adjust to your environment)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "JapaneseDate.xlsx");

// Step 8: Save the workbook
workbook.Save(outputPath, SaveFormat.Xlsx);
```

**Tip** – Jika direktori target tidak ada atau Anda tidak memiliki izin menulis, `Save` akan melempar `IOException`. Selalu verifikasi path sebelum memanggil `Save`.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin, tempel, dan jalankan. Program ini mencakup semua direktif `using`, penanganan error, dan komentar yang menjelaskan setiap operasi.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;
using System.IO;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Define the Japanese imperial date string
            string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

            // 3️⃣ Set up parsing options for the Japanese Emperor calendar
            var parseOptions = new DateTimeParseOptions
            {
                Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
            };

            // 4️⃣ Parse the string into a .NET DateTime
            DateTime parsedDate = DateTime.ParseExact(
                imperialDate,
                "ggyy/MM/dd",
                CultureInfo.InvariantCulture,
                DateTimeStyles.None,
                parseOptions);

            // 5️⃣ Write the date to cell A1
            sheet.Cells["A1"].PutValue(parsedDate);

            // Apply a consistent date format
            Style dateStyle = workbook.CreateStyle();
            dateStyle.Custom = "yyyy-mm-dd";
            sheet.Cells["A1"].SetStyle(dateStyle);

            // 6️⃣ Determine the output file location
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "JapaneseDate.xlsx");

            // 7️⃣ Save the workbook as an .xlsx file
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved successfully to: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

**Hasil yang diharapkan**

Saat Anda membuka `JapaneseDate.xlsx`, sel A1 berisi tanggal **2021‑04‑01** (setara Gregorian dari Reiwa 3 / 04 / 01) yang ditampilkan dalam format `yyyy‑mm‑dd`.

![Excel workbook with date in cell A1](excel-date-screenshot.png){alt="Tangkapan layar workbook Excel yang menampilkan tanggal kekaisaran Jepang di sel A1"}

---

## Pertanyaan umum dan kasus tepi

| Question | Answer |
|----------|--------|
| *Bagaimana jika era berubah (mis., Heisei ke Reiwa)?* | Kalender `JapaneseEmperor` secara otomatis memetakan simbol era (`H`, `R`, dll.) ke rentang Gregorian yang tepat, sehingga Anda hanya perlu memperbarui string input. |
| *Bisakah saya menulis banyak tanggal dalam satu kolom?* | Ya. Lakukan loop pada data Anda dan panggil `sheet.Cells[row, column].PutValue(dateValue)` untuk setiap baris. |
| *Bagaimana jika saya membutuhkan format tanggal yang berbeda?* | Ubah `dateStyle.Custom` ke string format tanggal Excel apa pun, seperti `"dd-mmm-yyyy"` atau `"mm/dd/yyyy"`. |
| *Apakah ada cara untuk melindungi sheet setelah menulis tanggal?* | Gunakan `sheet.Protect(ProtectOptions.All, "password")` sebelum menyimpan. |
| *Bagaimana cara menangani zona waktu?* | `DateTime` menyimpan waktu UTC atau lokal. Konversi menggunakan `DateTime.SpecifyKind` atau `TimeZoneInfo.ConvertTime` sebelum memanggil `PutValue`. |

## Kesimpulan

Anda sekarang tahu cara **create excel workbook**, **write date to excel**, **add date to worksheet**, dan **save workbook as xlsx** menggunakan Aspose.Cells di C#. Contoh lengkap menunjukkan cara mem‑parsing string kalender kekaisaran Jepang, menerapkan gaya konsisten, dan menangani masalah sistem file.  

Dari sini Anda dapat

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Workbook Excel C# – Tambahkan Komentar & Simpan sebagai XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Buat Workbook Baru di C# – Tambahkan Rumus dan Simpan File Excel](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Buat Workbook Excel – Bungkus Kolom dan Simpan sebagai XLSX](/cells/english/net/formatting-rows-and-columns-in-excel/create-excel-workbook-wrap-columns-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}