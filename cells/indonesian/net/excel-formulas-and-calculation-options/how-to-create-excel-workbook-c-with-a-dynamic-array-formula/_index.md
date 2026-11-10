---
category: general
date: 2026-10-01
description: Buat workbook Excel dengan C# secara cepat dan pelajari contoh formula
  array dinamis untuk menulis formula Excel C# di Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- dynamic array formula example
- write excel formula c#
language: id
lastmod: 2026-10-01
og_description: Buat buku kerja Excel dengan C# secara cepat dan lihat contoh rumus
  array dinamis yang menunjukkan cara menulis rumus Excel C# menggunakan Aspose.Cells.
  Ikuti panduan langkah demi langkah untuk menghasilkan, menghitung, dan menyimpan
  file.
og_image_alt: Screenshot of C# code creating an Excel workbook and applying a SORT
  dynamic array formula
og_title: Buat buku kerja Excel C# dengan rumus array dinamis
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook C# quickly and learn a dynamic array formula
    example to write Excel formula C# in Aspose.Cells.
  headline: How to create Excel workbook C# with a dynamic array formula
  type: TechArticle
- description: Create Excel workbook C# quickly and learn a dynamic array formula
    example to write Excel formula C# in Aspose.Cells.
  name: How to create Excel workbook C# with a dynamic array formula
  steps:
  - name: Verifying the result (expected output)
    text: 'You can print the spilled values to the console to confirm the calculation
      succeeded:'
  - name: What if I need to use a different dynamic array function?
    text: 'Replace the formula string with any other dynamic array function, such
      as `=FILTER(A2:A10, B2:B10>10)` or `=UNIQUE(A2:A10)`. The same **write Excel
      formula C#** pattern applies:'
  - name: How do I handle formulas that reference other worksheets?
    text: 'Reference another sheet by its name:'
  - name: Can I suppress automatic calculation and calculate later?
    text: 'Yes. Set the workbook’s calculation mode to manual:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cara membuat workbook Excel C# dengan rumus array dinamis
url: /id/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat workbook Excel C# dengan formula array dinamis

Jika Anda perlu **membuat workbook Excel C#** secara programatis, panduan ini menunjukkan secara tepat cara melakukannya menggunakan Aspose.Cells. Anda juga akan mendapatkan **contoh formula array dinamis** yang memperlihatkan cara terbaik untuk **menulis formula Excel C#** bagi fungsi Excel modern seperti `SORT`.

Membuat file Excel dari C# dulu memerlukan interop COM atau pembuatan XML manual, keduanya rapuh dan sulit dipelihara. Pada akhir tutorial ini Anda akan memiliki workbook yang berfungsi penuh yang secara otomatis menghitung array dinamis, dan Anda akan memahami mengapa pendekatan ini dapat diandalkan untuk otomasi tingkat produksi.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

- .NET 6.0 atau yang lebih baru terpasang (kode ini juga bekerja dengan .NET Core dan .NET Framework)
- Lisensi Aspose.Cells yang valid atau kunci evaluasi gratis
- Visual Studio 2022 (atau IDE apa pun yang mendukung C#)
- Familiaritas dasar dengan sintaks C# dan formula Excel

Tidak ada paket NuGet tambahan yang diperlukan selain `Aspose.Cells`, yang dapat Anda tambahkan dengan:

```bash
dotnet add package Aspose.Cells
```

## Langkah 1: Siapkan proyek C# dan referensikan Aspose.Cells

Buat aplikasi console baru dan tambahkan referensi Aspose.Cells. Langkah ini penting karena perpustakaan menyediakan `Workbook`, `Worksheet`, dan mesin perhitungan yang Anda perlukan untuk **menulis formula Excel C#**.

```csharp
// Program.cs
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // The rest of the tutorial code lives inside this method.
    }
}
```

> **Mengapa ini penting:** Aspose.Cells menyembunyikan detail OpenXML tingkat rendah, memungkinkan Anda fokus pada logika bisnis daripada keanehan format file.

## Langkah 2: Buat workbook Excel dan dapatkan worksheet pertama

Sekarang kita **membuat workbook Excel C#** dengan menginstansiasi objek `Workbook`. Workbook default berisi satu worksheet, yang kita ambil untuk operasi selanjutnya.

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates a blank .xlsx file in memory
Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet by default
```

> **Tip profesional:** Jika Anda memerlukan beberapa sheet, panggil `workbook.Worksheets.Add()` sebelum mengaksesnya.

## Langkah 3: Isi data sumber untuk array dinamis

Fungsi array dinamis seperti `SORT` memerlukan rentang sumber. Mari isi sel *A2:A10* dengan angka yang belum terurut sehingga formula `SORT` dapat memperlihatkan perilakunya.

```csharp
// Step 3: Fill A2:A10 with sample data
int[] numbers = { 42, 7, 19, 33, 5, 27, 14, 8, 21 };
for (int i = 0; i < numbers.Length; i++)
{
    worksheet.Cells[i + 1, 0].PutValue(numbers[i]); // Row i+2, Column A (0‑based index)
}
```

> **Mengapa kita melakukan ini:** Menyediakan data konkret memungkinkan Anda melihat **contoh formula array dinamis** beraksi tanpa memerlukan file input eksternal.

## Langkah 4: Tulis formula array dinamis ke sel A1

Berikut inti dari bagian **menulis formula Excel C#**. Kami menetapkan formula `SORT` ke sel *A1*. Karena `SORT` adalah fungsi array dinamis, Excel secara otomatis akan “spill” hasil yang terurut ke sel‑sel di bawahnya.

```csharp
// Step 4: Insert a dynamic array formula (SORT) into cell A1
worksheet.Cells[0, 0].Formula = "=SORT(A2:A10)";
```

> **Penjelasan:**  
> - `worksheet.Cells[0, 0]` menargetkan sel **A1** (baris 0, kolom 0).  
> - String `=SORT(A2:A10)` adalah formula Excel standar. Aspose.Cells mem‑parsenya sama seperti Excel, sehingga mendukung penuh fungsi array dinamis modern.

## Langkah 5: Hitung ulang workbook agar formula terisi secara otomatis

Aspose.Cells tidak menghitung ulang formula secara otomatis saat menulis. Anda harus secara eksplisit memicu perhitungan untuk melihat hasil yang “spill”.

```csharp
// Step 5: Recalculate the workbook so the formula evaluates
workbook.Calculate();   // runs the calculation engine once
```

Setelah pemanggilan ini, sel **A1:A9** akan berisi daftar terurut: 5, 7, 8, 14, 19, 21, 27, 33, 42.

### Memverifikasi hasil (output yang diharapkan)

Anda dapat mencetak nilai yang “spill” ke konsol untuk memastikan perhitungan berhasil:

```csharp
Console.WriteLine("Sorted values from A1 down:");
for (int row = 0; row < 9; row++)
{
    Console.WriteLine(worksheet.Cells[row, 0].StringValue);
}
```

**Output konsol yang diharapkan**

```
Sorted values from A1 down:
5
7
8
14
19
21
27
33
42
```

> **Catatan kasus tepi:** Jika rentang sumber berisi data non‑numerik, `SORT` akan mengurutkan secara leksikografis. Selalu validasi tipe data sebelum menerapkan fungsi yang hanya untuk angka.

## Langkah 6: Simpan workbook ke disk (opsional)

Menyimpan file memungkinkan Anda membukanya di Excel dan melihat array dinamis secara visual. Langkah ini tidak diperlukan untuk perhitungan itu sendiri, tetapi berguna untuk debugging dan distribusi.

```csharp
// Step 6: Save the workbook as an .xlsx file
string outputPath = "SortedNumbers.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Saat Anda membuka *SortedNumbers.xlsx* di Excel 365 atau versi lebih baru, Anda akan melihat daftar terurut secara otomatis “spill” dari **A1** ke bawah—tepat seperti yang dihasilkan oleh **contoh formula array dinamis** dari C#.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua bagian, berikut program lengkap yang dapat dijalankan:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2. Fill source data (A2:A10)
        int[] numbers = { 42, 7, 19, 33, 5, 27, 14, 8, 21 };
        for (int i = 0; i < numbers.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(numbers[i]); // A2:A10
        }

        // 3. Write dynamic array formula (SORT) into A1
        worksheet.Cells[0, 0].Formula = "=SORT(A2:A10)";

        // 4. Force calculation so the array spills
        workbook.Calculate();

        // 5. Display the spilled values in the console
        Console.WriteLine("Sorted values from A1 down:");
        for (int row = 0; row < 9; row++)
        {
            Console.WriteLine(worksheet.Cells[row, 0].StringValue);
        }

        // 6. Save the workbook (optional)
        string outputPath = "SortedNumbers.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Jalankan program (`dotnet run`) dan Anda akan melihat angka terurut tercetak, diikuti konfirmasi bahwa file telah disimpan.

## Pertanyaan umum dan variasi

### Bagaimana jika saya perlu menggunakan fungsi array dinamis yang berbeda?

Ganti string formula dengan fungsi array dinamis lain, seperti `=FILTER(A2:A10, B2:B10>10)` atau `=UNIQUE(A2:A10)`. Pola **menulis formula Excel C#** tetap sama:

```csharp
worksheet.Cells[0, 0].Formula = "=UNIQUE(A2:A10)";
```

### Bagaimana cara menangani formula yang merujuk ke worksheet lain?

Rujuk sheet lain dengan namanya:

```csharp
worksheet.Cells[0, 0].Formula = "=SORT('Sheet2'!A2:A10)";
```

Aspose.Cells menyelesaikan referensi lintas sheet secara otomatis selama `workbook.Calculate()`.

### Bisakah saya menonaktifkan perhitungan otomatis dan menghitung nanti?

Ya. Atur mode perhitungan workbook ke manual:

```csharp
workbook.Settings.CalcMode = CalcMode.Manual;
// ... make many changes ...
workbook.Calculate(); // call once when ready
```

Ini meningkatkan kinerja ketika Anda memperbarui ribuan sel sebelum perhitungan akhir.

## Kesimpulan

Anda kini tahu cara **membuat workbook Excel C#** menggunakan Aspose.Cells, menyisipkan **contoh formula array dinamis**, dan **menulis formula Excel C#** yang secara otomatis “spill” hasilnya. Solusi lengkap mencakup penyiapan proyek, persiapan data, penyisipan formula, pemaksaan perhitungan, verifikasi, dan penyimpanan file opsional.

Dari sini Anda dapat menjelajahi skenario yang lebih maju: menggabungkan beberapa fungsi array dinamis, menerapkan format angka khusus, atau mengintegrasikan pembuatan workbook ke dalam API web. Selalu validasi data masukan sebelum menerapkan formula, dan manfaatkan mesin perhitungan Aspose.Cells yang kaya untuk pemrosesan Excel sisi‑server yang andal. Selamat coding!


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Excel Automation with Aspose.Cells .NET: Mastering Workbook & Formula Calculations](/cells/english/net/formulas-functions/excel-automation-aspose-cells-net-workbook-formulas/)
- [Create Excel Workbook C# – Complete Guide with Aspose.Cells](/cells/english/net/excel-workbook/create-excel-workbook-c-complete-guide-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}