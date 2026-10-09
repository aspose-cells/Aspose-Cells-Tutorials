---
category: general
date: 2026-06-27
description: Cara menggunakan wrapcols dan wrap rows di Excel dengan C#. Pelajari
  cara membuat workbook Excel menggunakan C# dan menghitung ulang formula Excel dengan
  contoh langkah demi langkah.
draft: false
keywords:
- how to use wrapcols
- wrap rows excel
- wrap columns excel
- recalculate excel formulas
- create excel workbook c#
language: id
og_description: cara menggunakan wrapcols dan wrap rows excel dengan C#. panduan ini
  menunjukkan cara membuat workbook excel dengan C# dan menghitung ulang rumus excel
  dalam hitungan menit.
og_title: cara menggunakan wrapcols di C# – Tutorial Lengkap Pembungkus Excel
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  headline: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate
    Formulas
  type: TechArticle
- description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  name: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas
  steps:
  - name: Expected Result
    text: '| A | B | C | |---|---|---| | 1 | A | 2 | | 2 | B | 3 | | 3 | C | 4 | |
      4 | D | 5 | | 5 | E | 6 | | 6 | F | 7 | | 7 | G | 8 | | 8 | H | 9 | | 9 | I
      | |'
  - name: What if the source range is empty?
    text: Both `WRAPCOLS` and `WRAPROWS` will simply return an empty array, resulting
      in a blank cell. It’s safe to call the functions even when you’re not sure about
      data presence.
  - name: Can I wrap more than one range at a time?
    text: Yes—just place additional formulas in other cells. Each formula works independently,
      so you could have `WRAPCOLS` in D1, `WRAPROWS` in E1, etc.
  - name: How does this differ from a simple copy‑paste transpose?
    text: '`WRAPCOLS`/`WRAPROWS` handle *pagination* automatically. If you have 20
      items and ask for 3 columns, the function creates the necessary number of rows
      (7 in this case) without you calculating the dimensions manually.'
  - name: Does the library support dynamic array formulas (Excel 365)?
    text: Aspose.Cells fully supports dynamic array functions, including `WRAPCOLS`
      and `WRAPROWS`. The calculation engine will spill the results just like native
      Excel.
  - name: What about performance on large datasets?
    text: For millions of rows, consider batching the calculation (`workbook.CalculateFormula(FormulaCalculationOptions)`)
      or disabling automatic calculation while you insert formulas, then re‑enable
      it before saving.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Cara menggunakan wrapcols di C# – Panduan Lengkap dengan Excel WRAPROWS & Menghitung
  Ulang Rumus
url: /id/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara menggunakan wrapcols di C# – Panduan Lengkap dengan Excel WRAPROWS & Recalculate Formulas

Pernah bertanya-tanya **bagaimana cara menggunakan wrapcols** ketika Anda perlu mengubah daftar panjang menjadi kisi yang rapi? Mungkin Anda sudah mencoba trik salin‑tempel manual, tetapi itu lambat, rawan kesalahan, dan jujur saja, menyebalkan. Kabar baik? `WRAPCOLS` Excel (beserta saudaranya `WRAPROWS`) dapat melakukan pekerjaan berat untuk Anda—*dan* Anda dapat mengendalikan mereka dari kode C#.

Dalam tutorial ini kami akan membahas cara membuat workbook Excel di C#, menerapkan `WRAPCOLS` dan `WRAPROWS`, dan akhirnya **recalculate excel formulas** sehingga data yang dibungkus muncul secara instan. Pada akhir tutorial Anda akan memiliki potongan kode siap‑jalankan yang dapat Anda sisipkan ke proyek .NET mana pun.

## Apa yang Akan Anda Pelajari

- Bagaimana cara **create excel workbook c#** menggunakan library Aspose.Cells (tanpa memerlukan COM interop).  
- Sintaks tepat untuk fungsi `WRAPCOLS` dan bagaimana perbedaannya dengan `WRAPROWS`.  
- Mengapa Anda harus **recalculate excel formulas** setelah menyisipkan fungsi, dan cara melakukannya secara efisien.  
- Contoh lengkap yang dapat dijalankan yang dapat Anda copy‑paste dan melihat hasilnya dalam file `.xlsx`.

**Prerequisites** – Anda memerlukan .NET 6+ (atau .NET Framework 4.7+), Visual Studio 2022 atau IDE apa pun yang Anda suka, dan paket NuGet Aspose.Cells untuk .NET. Jika Anda baru dengan Aspose.Cells, jangan khawatir; langkah‑langkahnya sederhana dan dijelaskan sepenuhnya.

---

## Langkah 1: Siapkan Proyek dan Instal Aspose.Cells

Untuk memulai, buat proyek konsol baru:

```bash
dotnet new console -n WrapDemo
cd WrapDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** Jika Anda menggunakan Visual Studio, cukup klik kanan proyek → *Manage NuGet Packages* → cari **Aspose.Cells** dan instal.

Library ini memberikan kelas `Workbook`, `Worksheet`, dan `Cell` yang akan kita perlukan untuk sisa tutorial.

## Langkah 2: Buat Workbook Excel dan Isi Data Contoh

Sekarang kami akan membuat workbook, mengambil lembar kerja pertama, dan mengisi kolom **A** dan **B** dengan angka contoh. Data ini nanti akan dibungkus menjadi kolom dan baris.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 2‑1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2‑2: Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate A2:A10 with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate B2:B10 with letters A‑I (just for variety)
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // The rest of the steps follow…
```

> **Why this matters:** Memiliki data deterministik memungkinkan Anda memverifikasi bahwa `WRAPCOLS` dan `WRAPROWS` melakukan tepat apa yang Anda harapkan.

## Langkah 3: Terapkan Fungsi `WRAPCOLS` – **how to use wrapcols**

`WRAPCOLS` mengambil rentang satu‑dimensi dan menyebarkannya ke sejumlah kolom yang ditentukan, secara otomatis menambahkan baris baru bila diperlukan. Berikut adalah formula tepat yang akan kami sisipkan ke sel **A1**:

```csharp
        // Step 3: Insert WRAPCOLS formula – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";
```

> **Explanation:** Argumen kedua (`3`) memberi tahu Excel untuk membuat tiga kolom per baris. Jadi tiga nilai pertama (1, 2, 3) berada di A1:C1, tiga nilai berikutnya (4, 5, 6) berada di A2:C2, dan nilai yang tersisa mengisi baris berikutnya.

## Langkah 4: Terapkan Fungsi `WRAPROWS` – wrap rows excel

`WRAPROWS` melakukan hal sebaliknya: ia mengambil rentang vertikal dan menyusunnya menjadi sejumlah baris per kolom yang ditentukan. Kami akan menempatkan formula ini di **B1**:

```csharp
        // Step 4: Insert WRAPROWS formula – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";
```

> **Explanation:** Dengan `2` baris per kolom, nilai “A, B” masuk ke B1:B2, “C, D” ke C1:C2, dan seterusnya. Fungsi ini secara otomatis memperluas lembar secara horizontal.

## Langkah 5: Hitung Ulang Semua Formula – **recalculate excel formulas**

Ketika Anda menetapkan formula secara programatis, Excel tidak akan menghitung hasilnya sampai workbook dibuka atau Anda secara eksplisit memberi tahu library untuk mengevaluasinya. Di sinilah **recalculate excel formulas** berperan:

```csharp
        // Step 5: Force calculation so the wrapped data appears immediately
        workbook.CalculateFormula();
```

> **Why you need this:** Tanpa memanggil `CalculateFormula()`, sel akan menampilkan teks mentah `=WRAPCOLS(...)` saat Anda membuka file, yang mengalahkan tujuan tutorial.

## Langkah 6: Simpan Workbook dan Verifikasi Output

Akhirnya, tulis workbook ke disk. Anda dapat membuka file yang dihasilkan di Excel untuk melihat tata letak yang dibungkus.

```csharp
        // Step 6: Save the workbook (adjust the path as needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see wrapcols and wraprows in action.");
    }
}
```

### Hasil yang Diharapkan

| A | B | C |
|---|---|---|
| 1 | A | 2 |
| 2 | B | 3 |
| 3 | C | 4 |
| 4 | D | 5 |
| 5 | E | 6 |
| 6 | F | 7 |
| 7 | G | 8 |
| 8 | H | 9 |
| 9 | I |   |

- **Kolom A‑C** diisi oleh pemanggilan `WRAPCOLS` (tiga kolom per baris).  
- **Baris B‑I** diisi oleh pemanggilan `WRAPROWS` (dua baris per kolom).  

Buka `output.xlsx` dan Anda akan melihat tata letak persis seperti di atas. Jika angka tidak cocok, periksa kembali string formula dan pastikan `CalculateFormula()` telah dipanggil.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika rentang sumber kosong?
Baik `WRAPCOLS` maupun `WRAPROWS` akan mengembalikan array kosong, menghasilkan sel kosong. Aman memanggil fungsi tersebut bahkan ketika Anda tidak yakin ada data atau tidak.

### Bisakah saya membungkus lebih dari satu rentang sekaligus?
Ya—cukup letakkan formula tambahan di sel lain. Setiap formula bekerja secara independen, sehingga Anda dapat memiliki `WRAPCOLS` di D1, `WRAPROWS` di E1, dll.

### Bagaimana ini berbeda dari transpose salin‑tempel sederhana?
`WRAPCOLS`/`WRAPROWS` menangani *paginasi* secara otomatis. Jika Anda memiliki 20 item dan meminta 3 kolom, fungsi akan membuat jumlah baris yang diperlukan (7 dalam kasus ini) tanpa Anda menghitung dimensi secara manual.

### Apakah library mendukung formula array dinamis (Excel 365)?
Aspose.Cells sepenuhnya mendukung fungsi array dinamis, termasuk `WRAPCOLS` dan `WRAPROWS`. Mesin perhitungan akan menumpahkan hasil seperti Excel asli.

### Bagaimana dengan kinerja pada dataset besar?
Untuk jutaan baris, pertimbangkan memproses perhitungan secara batch (`workbook.CalculateFormula(FormulaCalculationOptions)`) atau menonaktifkan perhitungan otomatis saat Anda menyisipkan formula, lalu mengaktifkannya kembali sebelum menyimpan.

## Kode Sumber Lengkap (Siap Jalankan)

Berikut adalah program lengkap—salin ke `Program.cs` dan tekan **F5**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate column A (A2:A10) with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate column B (B2:B10) with letters A‑I
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // Apply WRAPCOLS – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";

        // Apply WRAPROWS – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";

        // Recalculate all formulas so the wrapped data appears
        workbook.CalculateFormula();

        // Save the workbook (adjust the folder if needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the wrapped results.");
    }
}
```

## Kesimpulan

Anda sekarang tahu **how to use wrapcols** (dan pasangannya `WRAPROWS`) dari C# untuk mengubah bentuk data dalam lembar Excel, dan Anda memahami mengapa **recalculate excel formulas** adalah langkah wajib. Pola ini—*create excel workbook c# → insert WRAP functions → recalculate*—adalah dasar yang kuat untuk setiap tugas pelaporan atau penyajian data yang memerlukan tata letak kolom atau baris dinamis.

Apa selanjutnya? Cobalah bereksperimen dengan:

- Jumlah kolom/baris yang berbeda (`WRAPCOLS(..., 5)` atau `WRAPROWS(..., 4)`).  
- Menggabungkan `WRAPCOLS` dengan fungsi array dinamis lain seperti `FILTER` atau `SORT`.  
- Mengekspor workbook ke PDF dengan `workbook.Save("report.pdf", SaveFormat.Pdf)`.

Silakan ubah contoh, tambahkan gaya, atau integrasikan ke dalam pipeline otomatisasi yang lebih besar. Jika Anda mengalami kendala, tinggalkan komentar di bawah—selamat coding!

![Diagram yang menunjukkan bagaimana wrapcols dan wraprows mengubah satu kolom menjadi grid – contoh how to use wrapcols](wrapcols-wraprows-diagram.png "contoh how to use wrapcols")

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menggunakan Aspose.Cells untuk .NET untuk Mengelompokkan Baris dan Kolom di Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [Cara Menyembunyikan Baris dan Kolom di Excel Menggunakan Aspose.Cells .NET: Panduan Komprehensif](/cells/english/net/range-management/aspose-cells-net-hide-rows-columns-excel/)
- [Cara Membuat dan Mengonfigurasi Workbook Excel dengan Aspose.Cells .NET: Panduan Langkah demi Langkah](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}