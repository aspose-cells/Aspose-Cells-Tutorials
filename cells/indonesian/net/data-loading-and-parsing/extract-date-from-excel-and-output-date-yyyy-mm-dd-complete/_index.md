---
category: general
date: 2026-03-18
description: Ekstrak tanggal dari Excel dan keluarkan tanggal yyyy‑mm‑dd dalam format
  ISO. Pelajari cara membaca tanggal era Jepang, mengonversinya, dan menampilkan tanggal
  ISO di C#.
draft: false
keywords:
- extract date from excel
- output date yyyy-mm-dd
- display date iso format
language: id
og_description: Ekstrak tanggal dari Excel dan keluarkan tanggal dalam format yyyy‑mm‑dd
  ISO. Tutorial C# langkah demi langkah dengan kode lengkap dan penjelasan.
og_title: Ekstrak tanggal dari Excel – Output tanggal yyyy‑mm‑dd di C#
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Ekstrak tanggal dari Excel dan output tanggal yyyy‑mm‑dd – Panduan Lengkap
  C#
url: /id/net/data-loading-and-parsing/extract-date-from-excel-and-output-date-yyyy-mm-dd-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekstrak tanggal dari Excel – Cara Mengoutput Tanggal yyyy‑mm‑dd dalam Format ISO

Pernah perlu **extract date from Excel** tetapi tidak yakin cara menangani tanggal era Jepang atau mendapatkan string `yyyy‑mm‑dd` yang bersih? Anda tidak sendirian. Dalam banyak proyek migrasi data, workbook sumber menyimpan tanggal menggunakan kalender Kaisar Jepang, dan sistem hilir mengharapkan tanggal yang sesuai ISO seperti `2024-04-01`.  

Dalam panduan ini kami akan membahas solusi lengkap yang dapat dijalankan yang membaca sebuah sel, menginterpretasikan era Jepang, dan **outputs the date yyyy‑mm‑dd**. Pada akhir panduan Anda akan tahu persis cara **display date ISO format** di aplikasi .NET apa pun, dan Anda akan memiliki potongan kode yang dapat digunakan kembali yang dapat Anda sisipkan ke dalam proyek Anda.

## Apa yang Anda Butuhkan

- **.NET 6+** (or .NET Framework 4.7.2+).  
- **Aspose.Cells for .NET** – perpustakaan yang memungkinkan kami mengatur kalender khusus saat memuat workbook.  
- Sebuah file Excel (`japan-date.xlsx`) yang berisi tanggal yang disimpan dalam sel era Jepang (misalnya `令和3年4月1日`).  
- Sebuah IDE favorit – Visual Studio, Rider, atau bahkan VS Code sudah cukup.

Tidak ada paket NuGet tambahan yang diperlukan selain Aspose.Cells, dan kode ini bekerja di Windows, Linux, atau macOS.

## Langkah 1: Siapkan Proyek dan Instal Aspose.Cells

Pertama, buat aplikasi console:

```bash
dotnet new console -n ExcelDateDemo
cd ExcelDateDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** Jika Anda berada di server CI, kunci versi paket (`Aspose.Cells 23.12`) untuk menjamin build yang dapat direproduksi.

## Langkah 2: Muat Workbook dengan Kalender Kaisar Jepang

Kunci untuk **extract date from Excel** ketika sumber menggunakan kalender non‑Gregorian adalah memberi tahu Aspose.Cells kalender mana yang harus diterapkan saat memuat. Kami melakukannya dengan `LoadOptions.Calendar`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create load options and set the Japanese Emperor calendar
        LoadOptions loadOptions = new LoadOptions
        {
            // This tells Aspose.Cells to interpret era dates correctly
            Calendar = new JapaneseEmperorCalendar()
        };

        // Step 3: Open the workbook that contains Japanese era dates
        // Replace the path with the actual location of your Excel file
        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);
```

**Why this matters:** Tanpa kalender khusus, Aspose.Cells akan memperlakukan sel sebagai string biasa, dan Anda akan kehilangan informasi era. Dengan menetapkan `JapaneseEmperorCalendar`, perpustakaan secara otomatis mengonversi `令和3年4月1日` menjadi `2021‑04‑01` di belakang layar.

## Langkah 3: Ambil Tanggal dari Sel Tertentu

Sekarang workbook tahu cara menginterpretasikan era, kita dapat membaca sel sebagai `DateTime`. Mari asumsikan tanggal berada di lembar kerja pertama, sel **A1** (baris 0, kolom 0).

```csharp
        // Step 4: Retrieve the date value from the first worksheet, first cell
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0]; // A1

        // GetDateTime() returns a System.DateTime object
        DateTime extractedDate = dateCell.GetDateTime();
```

Jika sel kosong atau berisi nilai non‑date, `GetDateTime()` akan melemparkan pengecualian. Pendekatan defensif terlihat seperti ini:

```csharp
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        DateTime extractedDate = dateCell.GetDateTime();
```

**Edge case:** Beberapa file Excel lama menyimpan tanggal sebagai angka (tanggal serial). Aspose.Cells menangani itu secara otomatis, tetapi Anda tetap harus memverifikasi tipe sel jika mengharapkan konten campuran.

## Langkah 4: Output Tanggal yyyy‑mm‑dd (ISO) dan Verifikasi

Dengan `DateTime` di tangan, memformatnya sebagai **output date yyyy‑mm‑dd** cukup satu baris:

```csharp
        // Step 5: Output the date in ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

Menjalankan program terhadap file yang berisi `令和3年4月1日` akan mencetak:

```
Extracted date (ISO): 2021-04-01
```

Itulah **display date iso format** yang tepat yang dibutuhkan banyak API.

## Contoh Lengkap yang Berfungsi

Menggabungkan semua bagian, berikut program lengkap yang siap disalin‑tempel:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook with Japanese era support
        LoadOptions loadOptions = new LoadOptions
        {
            Calendar = new JapaneseEmperorCalendar()
        };

        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);

        // Access the cell that holds the date (A1)
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0];

        // Validate the cell contains a date
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        // Extract the DateTime value
        DateTime extractedDate = dateCell.GetDateTime();

        // Convert to ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

> **Note:** Ganti `YOUR_DIRECTORY` dengan folder sebenarnya yang berisi `japan-date.xlsx`. Kode ini bekerja dengan lembar apa pun dan sel apa pun – cukup sesuaikan indeksnya.

## Menangani Kalender Lain (Opsional)

Jika Anda pernah perlu **extract date from Excel** yang menggunakan kalender Thai Buddhist atau kalender Ibrani, cukup ganti instance kalender:

```csharp
loadOptions.Calendar = new ThaiBuddhistCalendar();   // for Thai dates
// or
loadOptions.Calendar = new HebrewCalendar();         // for Hebrew dates
```

Sisa logika tetap tidak berubah, yang menunjukkan fleksibilitas pendekatan ini.

## Kesalahan Umum dan Cara Menghindarinya

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| `GetDateTime()` throws `InvalidCastException` | Sel bukan tanggal (mungkin string) | Periksa `Cell.Type` sebelum memanggil, atau gunakan `DateTime.TryParse` pada `Cell.StringValue`. |
| Tahun salah setelah konversi | Workbook dimuat tanpa mengatur `Calendar` | Selalu buat `LoadOptions` dengan kalender yang sesuai **sebelum** membuka file. |
| Output ISO menampilkan bagian waktu (`2021-04-01 00:00:00`) | Menggunakan `ToString()` tanpa string format | Gunakan specifier format `"yyyy-MM-dd"` untuk memaksa **output date yyyy‑mm‑dd**. |
| File tidak ditemukan | Path relatif mengarah ke folder yang salah | Gunakan `Path.Combine(Environment.CurrentDirectory, "japan-date.xlsx")` atau berikan path absolut. |

## Pro Tips untuk Kode Siap Produksi

1. **Cache workbook** jika Anda perlu membaca banyak tanggal dari file yang sama – membuka workbook relatif mahal.  
2. **Wrap extraction logic** dalam metode yang dapat digunakan kembali:

   ```csharp
   static string ExtractIsoDate(string file, int sheetIdx, int row, int col)
   {
       var opts = new LoadOptions { Calendar = new JapaneseEmperorCalendar() };
       var wb = new Workbook(file, opts);
       var cell = wb.Worksheets[sheetIdx].Cells[row, col];
       if (cell.Type != CellValueType.IsDateTime) return null;
       return cell.GetDateTime().ToString("yyyy-MM-dd");
   }
   ```

3. **Log string era asli** (`cell.StringValue`) bersamaan dengan output ISO untuk jejak audit.  
4. **Unit test** metode dengan beberapa file Excel yang dikodekan keras yang mencakup era berbeda (Heisei, Reiwa) untuk menjamin keakuratan.

## Gambaran Visual

Di bawah ini diagram cepat yang menggambarkan alur data—dari sel Excel ke string ISO.  

![Contoh ekstrak tanggal dari Excel yang menampilkan Excel → LoadOptions → DateTime → string ISO]  

*Teks alt: “ekstrak tanggal dari excel” diagram yang menampilkan alur konversi.*

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **extract date from Excel**, menangani nilai era Jepang, dan **output date yyyy‑mm‑dd** sehingga sesuai dengan **display date iso format** yang disukai API modern. Solusinya mandiri, bekerja dengan versi .NET apa pun yang mendukung Aspose.Cells, dan dapat diperluas ke kalender lain dengan satu baris perubahan.

Memiliki kalender lain dalam pikiran? Atau mungkin Anda mengambil tanggal dari beberapa kolom? Jangan ragu untuk menyesuaikan helper `ExtractIsoDate` atau tinggalkan komentar di bawah. Selamat coding, dan semoga tanggal Anda selalu sinkron dengan ISO!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}