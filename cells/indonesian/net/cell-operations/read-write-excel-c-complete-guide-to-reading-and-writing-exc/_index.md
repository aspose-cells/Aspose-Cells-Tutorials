---
category: general
date: 2026-03-01
description: Tutorial membaca‑menulis Excel C# menunjukkan cara membaca nilai sel
  Excel dan menulis tanggal‑waktu ke Excel menggunakan C# serta Aspose.Cells dalam
  beberapa langkah mudah.
draft: false
keywords:
- read write excel c#
- read excel cell value
- write datetime to excel
- c# excel interop
- aspnet excel automation
language: id
og_description: Tutorial Read write Excel C# menjelaskan cara membaca nilai sel Excel
  dan menulis datetime ke Excel dengan contoh kode yang jelas serta praktik terbaik.
og_title: Baca Tulis Excel C# – Panduan Langkah demi Langkah
tags:
- C#
- Excel
- Aspose.Cells
title: Baca Tulis Excel C# – Panduan Lengkap Membaca dan Menulis Sel Excel
url: /id/net/cell-operations/read-write-excel-c-complete-guide-to-reading-and-writing-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Read Write Excel C# – Panduan Lengkap Membaca dan Menulis Sel Excel

Pernah mencoba **read write Excel C#** dan berakhir dengan pengecualian yang membingungkan atau tanggal yang tidak cocok? Anda tidak sendirian. Banyak pengembang mengalami kesulitan ketika mereka harus mengambil tanggal era Jepang dari lembar kerja dan kemudian menyimpan `DateTime` yang tepat kembali ke sel yang sama.  

Dalam panduan ini kami akan menjelaskan secara tepat cara **read excel cell value** dan **write datetime to excel** menggunakan C# dan pustaka Aspose.Cells yang kuat. Pada akhir tutorial Anda akan memiliki contoh yang berdiri sendiri dan dapat dijalankan yang dapat Anda masukkan ke proyek .NET mana pun.

## Apa yang Akan Anda Pelajari

- Cara menginstal dan mereferensikan Aspose.Cells dalam proyek .NET 6+.
- Kode tepat yang diperlukan untuk mengambil sel yang berisi string era Jepang seperti `"R3/5/12"`.
- Cara mengurai string tersebut menjadi `DateTime` menggunakan budaya `"ja-JP"`.
- Langkah-langkah untuk menempatkan `DateTime` yang dihasilkan kembali ke sel lembar kerja yang sama.
- Tips untuk menangani kasus tepi seperti sel kosong atau format era yang tidak terduga.

Tidak diperlukan pengalaman sebelumnya dengan interop Excel—hanya pemahaman dasar tentang C# dan .NET. Mari kita mulai.

![Tangkapan layar operasi read write Excel C# yang menampilkan sel B2 sebelum dan sesudah konversi](read-write-excel-csharp.png "contoh read write excel c#")

## Langkah 1: Siapkan Proyek – Dasar-dasar Read Write Excel C# Foundations

Sebelum kita menyelam ke kode, kita memerlukan fondasi yang kuat.

1. **Buat aplikasi console baru** (atau proyek .NET apa pun) yang menargetkan .NET 6 atau lebih baru:

   ```bash
   dotnet new console -n ExcelEraDemo
   cd ExcelEraDemo
   ```

2. **Tambahkan paket NuGet Aspose.Cells**. Ini adalah pustaka yang sepenuhnya dikelola dan berfungsi tanpa interop COM:

   ```bash
   dotnet add package Aspose.Cells
   ```

3. **Salin file Excel** (`EraDates.xlsx`) ke root proyek. Buku kerja ini harus berisi lembar bernama `"Sheet1"` dengan sel **B2** berisi nilai seperti `"R3/5/12"` (Reiwa 3, Mei 12).

Itulah semua kerangka yang Anda butuhkan. Sisanya tutorial berfokus pada logika **read excel cell value** dan **write datetime to excel** yang sebenarnya.

## Langkah 2: Baca Nilai Sel Excel dengan C#

Sekarang proyek sudah siap, mari ambil string dari lembar kerja. Potongan kode berikut menunjukkan rantai pemanggilan yang tepat:

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load the workbook (adjust the path as needed)
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // assumes the sheet is named Sheet1

        // Step 2: Get the cell that holds the Japanese era date string
        // B2 contains something like "R3/5/12"
        Cell dateCell = ws.Cells["B2"];  

        // Step 3: Read the string representation from the cell
        string eraDateString = dateCell.StringValue;  

        Console.WriteLine($"Original cell value: {eraDateString}");
        // -------------------------------------------------
        // From here we’ll convert the era string to a DateTime.
        // -------------------------------------------------
    }
}
```

**Mengapa ini berhasil:** `Cell.StringValue` selalu mengembalikan teks yang ditampilkan, terlepas dari format angka yang mendasarinya. Hal ini memastikan kita bekerja dengan string persis `"R3/5/12"` yang dilihat pengguna.

### Kesalahan Umum

- **Sel kosong** – `StringValue` mengembalikan string kosong. Lindungi terhadapnya sebelum mengurai.  
- **Format tidak terduga** – Jika sel berisi `"2023/05/12"` parser era akan melempar pengecualian; Anda mungkin memerlukan fallback.  

## Langkah 3: Tulis DateTime ke Excel dengan C#

Dengan string era di tangan, kini kita mengurai menggunakan `DateTime.ParseExact`. Format `"ggyy/MM/dd"` memberi tahu .NET untuk mengharapkan era Jepang (`gg`), tahun dua digit (`yy`), dan komponen bulan/hari.

Berikut potongan kode:

```csharp
        // Step 4: Convert the era date string to a DateTime using the Japanese culture
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The cell value does not match the expected Japanese era format.");
            return;
        }

        Console.WriteLine($"Parsed DateTime (UTC): {parsedDate:u}");

        // Step 5: Store the resulting DateTime back into the same cell
        dateCell.PutValue(parsedDate);

        // Optional: Apply a standard date format so Excel shows it nicely
        dateCell.SetStyle(new Style { Number = 14 }); // 14 = "m/d/yyyy"

        // Save the workbook to a new file so we don’t overwrite the original
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Workbook saved as EraDates_Converted.xlsx");
```

**Mengapa kami menggunakan `PutValue`**: Aspose.Cells secara otomatis mendeteksi tipe .NET dan menulis tipe sel Excel yang sesuai. Mengirimkan `DateTime` menghasilkan tanggal Excel yang sebenarnya, yang dapat diformat atau digunakan dalam formula selanjutnya.

### Kasus Tepi dan Tips

- **Zona waktu** – Objek `DateTime` disimpan tanpa info zona. Jika Anda memerlukan UTC, panggil `DateTime.SpecifyKind`.  
- **Fallback budaya** – Jika Anda mengantisipasi budaya lain, bungkus parsing dalam helper yang mencoba beberapa objek `CultureInfo`.  
- **Kinerja** – Saat memproses ribuan baris, gunakan kembali satu instance `CultureInfo` alih-alih membuat yang baru setiap iterasi.  

## Langkah 4: Contoh Lengkap yang Berjalan – Menggabungkan Semua

Berikut adalah program lengkap yang siap dijalankan. Salin‑tempel ke `Program.cs`, pastikan `EraDates.xlsx` berada di samping binary yang dikompilasi, dan jalankan `dotnet run`.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load workbook
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // Change if your sheet has a different name

        // -------------------------------------------------
        // 1️⃣ Read the Japanese era string from B2
        // -------------------------------------------------
        Cell dateCell = ws.Cells["B2"];
        string eraDateString = dateCell.StringValue?.Trim();

        if (string.IsNullOrEmpty(eraDateString))
        {
            Console.WriteLine("Cell B2 is empty. Nothing to convert.");
            return;
        }

        Console.WriteLine($"Original cell value: {eraDateString}");

        // -------------------------------------------------
        // 2️⃣ Parse the era string into a DateTime
        // -------------------------------------------------
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The value does not match the expected Japanese era format (ggyy/MM/dd).");
            return;
        }

        Console.WriteLine($"Parsed DateTime: {parsedDate:u}");

        // -------------------------------------------------
        // 3️⃣ Write the DateTime back into the same cell
        // -------------------------------------------------
        dateCell.PutValue(parsedDate);

        // Apply a friendly date format (e.g., 2023/05/12)
        Style style = wb.CreateStyle();
        style.Number = 14; // Built‑in date format
        dateCell.SetStyle(style);

        // Save the updated workbook
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Conversion complete – saved as EraDates_Converted.xlsx");
    }
}
```

**Output yang diharapkan**

```
Original cell value: R3/5/12
Parsed DateTime: 2021-05-12 00:00:00Z
Conversion complete – saved as EraDates_Converted.xlsx
```

Saat Anda membuka `EraDates_Converted.xlsx`, sel **B2** kini menampilkan tanggal biasa (misalnya, `5/12/2021`) dan dapat digunakan dalam perhitungan Excel seperti nilai tanggal lainnya.

## Pro Tips untuk Kode Read Write Excel C# yang Tangguh

- **Validasi sebelum menulis** – Gunakan `Cell.IsFormula` atau `Cell.Type` untuk menghindari menimpa formula secara tidak sengaja.  
- **Pemrosesan batch** – Jika Anda perlu mengonversi seluruh kolom, lakukan loop melalui `ws.Cells.Columns[1]` (kolom B) dan terapkan logika yang sama.  
- **Keamanan thread** – Objek Aspose.Cells tidak thread‑safe; buat instance `Workbook` terpisah per thread saat memparalelkan.  
- **Logging** – Untuk skrip produksi, ganti `Console.WriteLine` dengan logger yang tepat (mis., Serilog) untuk menangkap kegagalan parsing.  
- **Pengujian** – Tulis unit test yang memasukkan string era yang diketahui ke dalam metode helper dan memastikan nilai `DateTime` yang dihasilkan.  

## Kesimpulan

Anda baru saja menguasai **read write Excel C#** dengan mempelajari cara **read excel cell value**, mengurai string era Jepang, dan **write datetime to excel** dengan percaya diri. Contoh lengkap menunjukkan alur kerja bersih dari awal hingga akhir yang dapat Anda sesuaikan untuk operasi massal, budaya berbeda, atau bahkan pipeline Excel‑ke‑database.

Apa selanjutnya? Cobalah memperluas skrip untuk memproses seluruh kolom tanggal era, atau jelajahi opsi pemformatan kaya Aspose.Cells untuk menata sel output. Anda juga dapat bereksperimen dengan pustaka lain seperti EPPlus atau ClosedXML—sebagian besar logika tetap sama, hanya pemanggilan API yang berbeda.

Ada pertanyaan atau skenario Excel yang rumit? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}