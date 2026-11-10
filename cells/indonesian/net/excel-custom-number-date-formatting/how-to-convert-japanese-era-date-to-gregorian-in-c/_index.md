---
category: general
date: 2026-10-01
description: Konversi tanggal era Jepang ke DateTime Gregorian menggunakan Aspose.Cells
  dalam C#. Pelajari cara mengonversi kalender Jepang dengan cepat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: id
lastmod: 2026-10-01
og_description: Mengonversi tanggal era Jepang ke DateTime Gregorian dalam C#. Tutorial
  ini menjelaskan cara mengonversi kalender Jepang secara akurat dengan Aspose.Cells.
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: Mengonversi tanggal era Jepang ke Gregorian dalam C# – panduan langkah demi
  langkah
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: Cara mengonversi tanggal era Jepang ke Gregorian di C#
url: /id/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengonversi tanggal era Jepang ke Gregorian dalam C#

Jika Anda perlu **mengonversi tanggal era Jepang** menjadi tanggal Gregorian dalam C#, panduan ini menunjukkan cara tepatnya. Baik Anda memproses data warisan, membaca input pengguna, atau menghasilkan laporan, perpustakaan Aspose.Cells membuat konversi menjadi sederhana. Selain itu, Anda akan menemukan cara terbaik untuk **cara mengonversi kalender Jepang** saat bekerja dengan spreadsheet.

Tutorial ini mencakup setiap langkah—dari membuat workbook hingga mengambil nilai `DateTime`—sehingga Anda dapat menyalin‑tempel program lengkap yang dapat dijalankan. Tidak diperlukan dokumentasi eksternal; cukup ikuti kode dan penjelasan di bawah ini.

## Prasyarat

* .NET 6.0 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.6+)
* Lisensi untuk **Aspose.Cells** (versi percobaan gratis dapat digunakan untuk pengujian)
* Lingkungan pengembangan seperti Visual Studio 2022 atau VS Code
* Familiaritas dasar dengan aplikasi konsol C#

## Mengonversi tanggal era Jepang dengan Aspose.Cells

Inti konversi berada pada beberapa panggilan API sederhana. Aspose.Cells secara otomatis menafsirkan string era Jepang (misalnya “Reiwa 2/04/01”) dan menampilkan hasilnya sebagai objek `DateTime` setelah lembar kerja dihitung ulang.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### Mengapa setiap langkah penting

| Step | Purpose | How it helps the conversion |
|------|---------|-----------------------------|
| **Create workbook** | Menyediakan kontainer yang memahami rumus Excel dan sistem tanggal. | Mesin tanggal internal perpustakaan diaktifkan hanya di dalam workbook. |
| **Insert era string** | Menyediakan teks kalender Jepang mentah yang ingin Anda terjemahkan. | Aspose.Cells mengenali nama era seperti *Reiwa*, *Heisei*, *Showa*, dll. |
| **Set style** | Memaksa sel diperlakukan sebagai sel nilai bukan string literal. | Tanpa style, metode `Calculate` mungkin mengabaikan sel, meninggalkan teks tidak berubah. |
| **Calculate** | Memicu parsing string era dan konversi ke nomor tanggal serial internal. | Perpustakaan mengonversi “Reiwa 2/04/01” → nomor serial → Gregorian `DateTime`. |
| **Read `DateTimeValue`** | Mengembalikan objek .NET `DateTime` yang telah dikonversi. | Anda kini memiliki `DateTime` standar yang dapat digunakan di API .NET mana pun. |

## Cara mengonversi kalender Jepang dalam skenario lain

Pendekatan yang sama berlaku untuk setiap nama era Jepang yang didukung oleh Aspose.Cells:

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### Menangani string tidak valid atau ambigu

* **Invalid era name** – Aspose.Cells melempar `FormatException`. Bungkus konversi dalam `try/catch` untuk memberikan pesan error yang ramah.
* **Missing year/month/day** – Perpustakaan mengharapkan pola lengkap “Era Year/Month/Day”. Jika Anda menerima data parsial, tambahkan bagian yang hilang atau tolak input tersebut lebih awal.
* **Different locale settings** – Konversi **tidak** bergantung pada budaya (culture) thread saat ini; selalu menggunakan peta era Jepang yang dibangun dalam Aspose.Cells. Hal ini membuat metode aman untuk pemrosesan sisi‑server.

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## Tips praktis dan jebakan umum

* **Always call `SetStyle`** sebelum `Calculate`. Melewatkan langkah ini sering menjadi sumber bug karena sel tetap menjadi penampung teks biasa.
* **Reuse the same workbook** jika Anda perlu mengonversi banyak tanggal. Membuat workbook baru untuk setiap konversi menambah beban yang tidak perlu.
* **Batch conversion** – Isi sebuah kolom dengan string era, panggil `worksheet.Calculate()` sekali, kemudian baca seluruh kolom `DateTimeValue`. Ini jauh lebih efisien dibanding menghitung ulang per sel.
* **Version compatibility** – Logika konversi era diperkenalkan di Aspose.Cells 22.9. Pastikan Anda menggunakan versi tersebut atau lebih baru; rilis lama memperlakukan string sebagai teks biasa.

## Contoh lengkap yang dapat dijalankan (aplikasi konsol)

Berikut adalah program mandiri yang dapat Anda kompilasi dan jalankan segera. Program ini memperlihatkan konversi Reiwa dan Heisei, serta menangani error dengan elegan.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**Output konsol yang diharapkan**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

Menjalankan program ini mengonfirmasi bahwa perpustakaan dengan benar **mengonversi tanggal era Jepang** dan melaporkan nilai yang tidak didukung dengan elegan.

## Kesimpulan

Anda sekarang tahu cara **mengonversi tanggal era Jepang** menjadi objek `DateTime` Gregorian standar menggunakan Aspose.Cells dalam C#. Prosesnya melibatkan memasukkan teks era, menerapkan style, menghitung ulang lembar kerja, dan membaca `DateTimeValue`. Dengan mengikuti langkah-langkah di atas Anda juga dapat menjawab pertanyaan lebih luas tentang **cara mengonversi kalender Jepang** secara massal, menangani error, dan mengoptimalkan kinerja.

### Langkah selanjutnya

* Jelajahi **formatting options** untuk menulis tanggal Gregorian kembali ke lembar kerja dengan format angka khusus.
* Gabungkan konversi ini dengan **data import pipelines** (misalnya, membaca file CSV yang berisi tanggal era).
* Tinjau fitur Aspose.Cells lain seperti **date arithmetic** dan **regional settings** untuk skenario kalender yang lebih kompleks.

Selamat coding, dan silakan sesuaikan contoh ini dengan alur kerja pemrosesan data Anda!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Mengurai Tanggal Era Jepang dalam C# dengan Aspose.Cells – Panduan Lengkap](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [Mengaktifkan Parsing Era Jepang dalam C# dengan Aspose.Cells](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [Cara membuat workbook dan mengonversi string ke tanggal dalam C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}