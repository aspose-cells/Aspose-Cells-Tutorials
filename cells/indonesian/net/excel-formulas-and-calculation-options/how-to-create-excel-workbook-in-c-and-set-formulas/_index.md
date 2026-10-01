---
category: general
date: 2026-10-01
description: Buat workbook Excel di C# dengan cepat, pelajari cara mengatur formula,
  menghitung kotangen, dan menggunakan fungsi PI di Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- how to calculate cot
- set formula in cell
- write formula to cell
- how to use pi function
language: id
lastmod: 2026-10-01
og_description: Buat workbook Excel di C# dengan Aspose.Cells. Pelajari cara mengatur
  formula, menggunakan fungsi PI, dan menghitung kotangen dalam beberapa langkah saja.
og_image_alt: Diagram showing an Excel workbook created in C# with a formula in cell
  A1
og_title: Buat workbook Excel di C# – atur rumus dan hitung cot
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook in C# quickly, learn how to set a formula, calculate
    cotangent, and use the PI function in Aspose.Cells.
  headline: How to create Excel workbook in C# and set formulas
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cara membuat workbook Excel di C# dan mengatur rumus
url: /id/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-and-set-formulas/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat workbook Excel di C# dan mengatur formula

Jika Anda perlu **create Excel workbook C#** kode yang menulis formula ke dalam sel, panduan ini menunjukkan secara tepat cara melakukannya. Anda akan melihat cara mengatur formula di worksheet, menggunakan fungsi PI bawaan, dan menghitung kotangen dari sebuah sudut—semua dengan Aspose.Cells.

Tutorial ini mencakup semua hal mulai dari menginisialisasi workbook hingga mengambil hasil perhitungan, sehingga Anda dapat menyalin contoh lengkap ke dalam proyek Anda sendiri tanpa ada bagian yang hilang.

## Prasyarat

* .NET 6.0 atau yang lebih baru terinstal  
* Lisensi Aspose.Cells yang valid (atau kunci evaluasi sementara)  
* Visual Studio 2022 atau IDE C# apa pun yang Anda sukai  

Tidak ada paket NuGet tambahan yang diperlukan selain `Aspose.Cells`.

## Membuat workbook Excel di C#

Langkah pertama adalah menginstansiasi objek `Workbook` baru. Objek ini mewakili seluruh file Excel dalam memori dan memberi Anda akses ke worksheet-nya.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                 // creates an empty .xlsx file
        var worksheet = workbook.Worksheets[0];        // the default first sheet

        // Continue with the rest of the steps...
```

Membuat workbook dengan cara ini memastikan file siap untuk manipulasi lebih lanjut, seperti menambahkan data, memberi gaya pada sel, atau menulis formula.

## Mengatur formula di sel menggunakan fungsi PI

Sekarang Anda akan **write formula to cell** A1. Formula ini menggunakan fungsi `PI()` untuk menyediakan konstanta π dan fungsi `COT` untuk menghitung kotangennya.

```csharp
        // Step 2: Set a formula in cell A1 (row 0, column 0)
        // The formula calculates the cotangent of π/4, which equals 1
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Continue with calculation...
```

*Mengapa ini penting*: `PI()` adalah fungsi bawaan Excel yang mengembalikan nilai π. Dengan membaginya dengan 4 Anda mendapatkan 45°, dan `COT` mengembalikan kotangen dari sudut tersebut. Ini menunjukkan **how to use pi function** di dalam formula Excel dari C#.

## Cara menghitung cot dengan Aspose.Cells

Jika Anda bertanya-tanya **how to calculate cot** tanpa mengonversi sudut secara manual, fungsi `COT` melakukan pekerjaan berat. Ia menerima sudut dalam radian, sehingga Anda dapat menggabungkannya dengan `PI()` untuk sudut umum.

```csharp
        // Step 3: Recalculate the workbook so the formula is evaluated
        workbook.Calculate();

        // Step 4: Retrieve and display the calculated result
        double result = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {result}");
    }
}
```

Menjalankan program mencetak:

```
Cotangent of PI/4 = 1
```

Karena `COT(π/4)` sama dengan 1, output mengonfirmasi bahwa formula telah berhasil **set formula in cell** dan dievaluasi.

## Menulis formula ke sel – tips tambahan

* **Multiple formulas**: Anda dapat menetapkan formula ke sel mana pun menggunakan properti `Formula` yang sama, misalnya, `worksheet.Cells["B2"].Formula = "=SIN(PI()/2)";`.
* **International settings**: Aspose.Cells menghormati locale workbook, sehingga nama fungsi tetap dalam bahasa Inggris (`PI`, `COT`) terlepas dari pengaturan regional pengguna.
* **Performance**: Jika Anda perlu mengatur ribuan formula, kumpulkan dalam batch dan panggil `workbook.Calculate()` sekali di akhir untuk menghindari perhitungan ulang berulang.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke dalam proyek konsol. Program ini mencakup semua pernyataan `using` yang diperlukan dan menunjukkan alur kerja lengkap dari pembuatan workbook hingga output hasil.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and obtain the first worksheet
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // Write a formula that uses the PI function and calculates cotangent
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Force calculation so the formula value is materialized
        workbook.Calculate();

        // Read the calculated value and display it
        double cotValue = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {cotValue}");

        // Optional: save the workbook to verify the formula visually
        workbook.Save("CotExample.xlsx");
    }
}
```

**Output yang diharapkan** ketika Anda menjalankan program:

```
Cotangent of PI/4 = 1
```

File `CotExample.xlsx` yang dihasilkan berisi formula di sel A1, memungkinkan Anda membuka file tersebut di Excel dan melihat hasil yang sama.

## Kesimpulan

Anda sekarang tahu cara **create Excel workbook C#** kode yang menulis formula, menggunakan fungsi `PI`, dan **calculates cot** dengan Aspose.Cells. Contoh ini mencakup seluruh siklus hidup: pembuatan workbook, **set formula in cell**, perhitungan ulang, dan pengambilan hasil.

Langkah selanjutnya yang dapat Anda jelajahi:

* Terapkan **write formula to cell** untuk perhitungan yang lebih kompleks seperti model keuangan.  
* Gunakan **set formula in cell** bersama dengan pemformatan bersyarat untuk menyoroti hasil.  
* Gabungkan **how to use pi function** dengan diagram trigonometri untuk pelaporan ilmiah.

Silakan bereksperimen dengan berbagai sudut, fungsi, dan tata letak worksheet. Menguasai penanganan formula di C# membuka pintu ke pipeline pelaporan Excel yang sepenuhnya otomatis. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Calculate Cotangent in Excel with C# – Create Workbook, Use EXPAND](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}