---
category: general
date: 2026-09-18
description: Pelajari cara memperluas array di Excel menggunakan fungsi EXPAND, mengisi
  template Excel, dan membuat lembar kerja Excel dengan rentang dinamis menggunakan
  C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- populate excel template
- dynamic range excel
- use expand function
- expand array formula
language: id
lastmod: 2026-09-18
og_description: Cara memperluas array di Excel dengan fungsi EXPAND, mengisi template
  Excel, dan membangun solusi Excel dengan rentang dinamis menggunakan kode C#.
og_image_alt: Excel worksheet showing expanded 5x5 array and Smart Markers result
og_title: Cara memperluas array di Excel dan mengisi templat
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to expand array in Excel using the EXPAND function, populate
    an Excel template, and create a dynamic range Excel worksheet with C#.
  headline: How to expand array in Excel and populate a template
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Cara memperluas array di Excel dan mengisi template
url: /id/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara memperluas array di Excel dan mengisi template

Jika Anda perlu **cara memperluas array** di Excel sambil mengisi template yang telah dirancang sebelumnya, panduan ini menunjukkan solusi lengkap dari awal hingga akhir. Dengan menggunakan fungsi `EXPAND` bersama Smart Markers dari Aspose.Cells, Anda dapat mengubah referensi satu sel menjadi rentang 5 × 5 dan secara otomatis mengganti penanda seperti `{IsActive}` dengan data nyata.

Anda akan melihat cara **mengisi template excel**, membuat **rentang dinamis excel**, dan menggunakan **fungsi expand** dengan benar dalam proyek C#. Pada akhir tutorial, Anda akan memiliki program yang dapat dijalankan yang memuat file `.xlsx`, memperluas formula array, menerapkan Smart Markers, dan menyimpan hasilnya.

## Prasyarat

* .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Core 3.1+)
* Aspose.Cells untuk .NET (paket NuGet `Aspose.Cells`)
* Sebuah workbook Excel yang berisi sel formula placeholder (misalnya `B2`) dan Smart Marker seperti `{IsActive}`
* Familiaritas dasar dengan C# dan formula Excel

> **Tips profesional:** Fungsi `EXPAND` hanya tersedia di Excel untuk Microsoft 365 dan Excel 2021+. Versi lama akan mengembalikan error `#NAME?`.

## Langkah 1: Cara memperluas array dengan fungsi EXPAND

Langkah pertama adalah memuat workbook dan menulis formula `EXPAND` yang mengubah satu sel sumber menjadi matriks yang lebih besar.  

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the template layout
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Apply the EXPAND function to cell B2.
        // =EXPAND(A2,5,5) expands the array that starts at A2 into a 5‑row by 5‑column range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";
```

Mengapa ini penting: `EXPAND` menghilangkan kebutuhan menyalin formula secara manual ke baris dan kolom. Ketika sel sumber (`A2`) berubah, seluruh blok 5 × 5 diperbarui secara otomatis, memberi Anda **rentang dinamis excel** yang merespons perubahan data.

## Langkah 2: Mengisi template Excel menggunakan Smart Markers

Smart Markers memungkinkan Anda menyisipkan placeholder di dalam template yang digantikan dengan nilai dari objek C#. Ini adalah cara paling nyaman untuk **mengisi template excel** tanpa menulis kode sel‑per‑sel.

```csharp
        // Prepare an anonymous object that matches the marker names in the template.
        var data = new { IsActive = true };

        // Apply Smart Markers. The marker {IsActive} inside a formula like
        // =IF({IsActive}, "Active", "Inactive") will be replaced with the value from the object.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);
```

Pemanggilan `SmartMarkersProcessor().Apply` memindai seluruh lembar, menemukan `{IsActive}`, dan menyuntikkan nilai boolean. Formula kemudian secara otomatis mengevaluasi menjadi `"Active"` atau `"Inactive"`.

## Langkah 3: Verifikasi rentang yang diperluas dan hasil yang terisi

Setelah menerapkan baik formula `EXPAND` maupun Smart Markers, Anda dapat secara programatis membaca beberapa sel untuk memastikan semuanya berfungsi seperti yang diharapkan.

```csharp
        // Optional: read a cell from the expanded block to confirm the value.
        var sampleValue = ws.Cells["B2"].Value; // top‑left cell of the expanded range
        Console.WriteLine($"Top‑left of expanded range: {sampleValue}");

        // Read the marker result cell (assume it is C2)
        var status = ws.Cells["C2"].StringValue;
        Console.WriteLine($"Status from Smart Marker: {status}");
```

Menjalankan program seharusnya mencetak nilai asli dari `A2` (atau hasil array) dan baik **Active** maupun **Inactive** tergantung pada flag `IsActive`.

## Langkah 4: Simpan workbook – output akhir

Akhirnya, tulis workbook yang telah dimodifikasi ke disk. Langkah ini menunjukkan alur lengkap dari memuat, memperluas, mengisi, hingga menyimpan file.

```csharp
        // Save the workbook with the expanded array and populated markers.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

File `output.xlsx` yang disimpan kini berisi matriks 5 × 5 yang dihasilkan oleh formula `EXPAND` dan sel yang mencerminkan nilai `{IsActive}`. Buka file tersebut di Excel untuk melihat rentang dinamis beraksi.

## Kasus tepi dan praktik terbaik

| Situasi                              | Rekomendasi                                                                 |
|--------------------------------------|------------------------------------------------------------------------------|
| Versi Excel tidak mendukung `EXPAND`| Kembali ke formula klasik `=OFFSET` atau `=INDEX`, atau tingkatkan ke Office 365. |
| Perlu memperluas ke ukuran variabel  | Gunakan `ROWS(source)` dan `COLUMNS(source)` di dalam `EXPAND` untuk dinamisme sejati.   |
| Banyak Smart Markers dalam lembar yang sama| Panggil `SmartMarkersProcessor().Apply` sekali dengan objek data komposit.      |
| Workbook besar ( > 10 000 baris)     | Nonaktifkan perhitungan saat menulis formula (`workbook.Settings.CheckFormula = false`). |

## Contoh lengkap yang berfungsi

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke proyek konsol baru.

```csharp
using System;
using Aspose.Cells;

class ExpandArrayDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that serves as the template.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Write the EXPAND formula to create a 5x5 dynamic range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";

        // 3️⃣ Prepare data for Smart Markers.
        var data = new { IsActive = true };

        // 4️⃣ Apply Smart Markers – replaces {IsActive} in any formula or text.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);

        // 5️⃣ (Optional) Verify a couple of cells.
        Console.WriteLine($"Expanded top‑left: {ws.Cells["B2"].Value}");
        Console.WriteLine($"Marker result: {ws.Cells["C2"].StringValue}");

        // 6️⃣ Save the final workbook.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
        Console.WriteLine("Workbook saved successfully.");
    }
}
```

**Output yang diharapkan saat Anda menjalankan program** (asumsikan `A2` berisi angka `42`):

```
Expanded top‑left: 42
Marker result: Active
Workbook saved successfully.
```

Membuka `output.xlsx` menampilkan blok 5 × 5 yang terisi dengan nilai yang diambil dari `A2` dan sel yang menampilkan **Active**.

## Kesimpulan

Anda kini tahu **cara memperluas array** di Excel menggunakan fungsi `EXPAND`, cara **mengisi template excel** dengan Smart Markers, dan cara membangun **rentang dinamis excel** yang secara otomatis menyesuaikan diri dengan data sumber. Contoh ini juga memperlihatkan cara yang tepat untuk **menggunakan fungsi expand** dan **formula array expand** dalam skenario otomasi C# dunia nyata.

Selanjutnya, pertimbangkan untuk memperluas solusi:

* Ganti dimensi tetap `5,5` dengan `ROWS(A2:A10), COLUMNS(A2:E2)` untuk rentang yang benar-benar variabel.
* Gabungkan beberapa Smart Markers untuk menghasilkan laporan lengkap (misalnya, daftar karyawan, tabel penjualan).
* Jelajahi API styling Aspose.Cells untuk memformat blok yang diperluas secara otomatis.

Silakan bereksperimen dengan berbagai array sumber, nama penanda, dan tata letak workbook. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Ekspor Data ke Excel: Isi Template dari Array dalam C#](/cells/english/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/)
- [Cara membuat array di Excel dengan C# – Panduan Langkah demi Langkah](/cells/english/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/)
- [Memproses Data Menggunakan Fungsi Array di Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}