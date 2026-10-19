---
category: general
date: 2026-07-03
description: Tuliskan formula array dalam C# untuk membuat array 2‑kolom, menghitung
  sel Excel, dan membungkus daftar ke dalam kolom. Ikuti contoh langkah demi langkah
  ini menggunakan Aspose.Cells.
draft: false
keywords:
- write array formula
- calculate excel cell
- wrap list into columns
- create 2‑column array
- generate excel array
language: id
og_description: Tuliskan formula array di C# untuk membangun array 2‑kolom, menghitung
  sel Excel, dan membungkus daftar ke dalam kolom. Pelajari proses lengkapnya dengan
  kode yang dapat dijalankan.
og_title: Menulis rumus array di C# – Panduan Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Write array formula in C# to create a 2‑column array, calculate Excel
    cell and wrap list into columns. Follow this step‑by‑step example using Aspose.Cells.
  headline: Write array formula in C# – Complete Programming Guide
  type: TechArticle
- description: Write array formula in C# to create a 2‑column array, calculate Excel
    cell and wrap list into columns. Follow this step‑by‑step example using Aspose.Cells.
  name: Write array formula in C# – Complete Programming Guide
  steps:
  - name: What if I need a dynamic range rather than a hard‑coded list?
    text: 'You can construct the list part of the formula at runtime:'
  - name: Does `WRAPCOLS` work on older Excel versions?
    text: '`WRAPCOLS` is available starting with Excel 365/2019. If you target older
      versions, you’ll need to simulate the behavior with `INDEX` and `MOD` tricks,
      but that quickly becomes messy. Using Aspose.Cells lets you keep the modern
      formula and still produce a compatible file for most users.'
  - name: Can I write the formula to a range instead of a single cell?
    text: 'Yes—assign the same formula to the top‑left cell of the range, then call
      `Calculate()` on the range object:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- automation
title: Menulis formula array di C# – Panduan Pemrograman Lengkap
url: /id/net/formulas-functions/write-array-formula-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menulis formula array di C# – Panduan Pemrograman Lengkap

Pernah membutuhkan untuk **menulis formula array** di C# tetapi tidak yakin bagaimana cara membuat Excel menghasilkan daftar yang terbungkus rapi? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan ketika mereka mencoba *menghasilkan array Excel* tanpa membuka UI. Dalam tutorial ini kami akan membahas contoh singkat, end‑to‑end yang **menulis formula array**, **menghitung sel Excel**, dan **membungkus daftar ke dalam kolom** untuk **membuat array 2‑kolom** yang dapat Anda simpan dan periksa.

Kami akan menggunakan pustaka Aspose.Cells yang populer karena memungkinkan Anda memanipulasi workbook sepenuhnya dalam kode. Pada akhir tutorial Anda akan memiliki potongan kode yang siap dijalankan, penjelasan jelas untuk setiap baris, dan ide-ide untuk memperluas pola ini ke dataset yang lebih besar. Tanpa basa‑basi—hanya bagian praktis yang dapat Anda salin‑tempel hari ini.

## Apa yang Anda Butuhkan

* .NET 6.0 atau lebih baru (kode ini juga berfungsi di .NET Core)  
* Referensi ke **Aspose.Cells** (Anda dapat mengunduhnya dari NuGet: `Install-Package Aspose.Cells`)  
* Folder yang dapat Anda baca/tulis file Excel – kami akan menyebutnya `YOUR_DIRECTORY` dalam contoh  

Itu saja. Tidak ada interop Excel tambahan, tidak ada COM, hanya kode terkelola murni.

![Contoh menulis formula array di C#](write-array-formula.png "Tangkapan layar yang menunjukkan array 2‑kolom yang dihasilkan di Excel – menulis formula array di C#")

## Langkah 1: Menulis formula array dengan Aspose.Cells

Hal pertama yang harus kita lakukan adalah **menulis formula array** ke dalam sebuah sel. Dalam sintaks Excel fungsi `WRAPCOLS` mengambil daftar datar dan mengubahnya menjadi matriks. Berikut cara melakukannya secara programatis:

```csharp
// Step 1: Load the workbook (or create a new one)
var workbook = new Aspose.Cells.Workbook(); // creates a blank workbook

// Access the first worksheet – this is where we’ll work
var worksheet = workbook.Worksheets[0];

// Write array formula into A1 that wraps {1,2,3,4} into 2 columns
worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";
```

**Mengapa ini penting:** Properti `Formula` menyimpan string formula Excel secara literal. Dengan menggunakan `WRAPCOLS` kita memberi tahu Excel untuk mengambil array linear `{1,2,3,4}` dan menyusunnya menjadi tata letak 2‑kolom, secara efektif **membuat array 2‑kolom**. Formula itu sendiri adalah *formula array*—Anda akan melihat kurung kurawal di sekitar angka-angka.

## Langkah 2: Menghitung sel Excel sehingga formula dievaluasi

Menulis formula saja tidak cukup; kita perlu **menghitung sel Excel** agar mesin mengevaluasinya. Aspose.Cells tidak akan secara otomatis menghitung ulang kecuali Anda memintanya:

```csharp
// Step 2: Force calculation of the cell containing the array formula
worksheet.Cells["A1"].Calculate();
```

**Mengapa langkah ini penting:** Tanpa memanggil `Calculate()`, sel tetap dalam keadaan “tertunda” dan workbook yang Anda simpan akan berisi formula mentah, bukan nilai yang dihitung. Dengan secara eksplisit menghitung ulang, kita memastikan array output terwujud dalam file.

## Langkah 3: Membungkus daftar ke dalam kolom – lihat hasilnya

Pada titik ini lembar kerja berisi blok 2‑kolom yang dimulai dari `A1`. Jika Anda membuka file, Anda akan melihat:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |

Itu adalah representasi visual dari **membungkus daftar ke dalam kolom** menggunakan fungsi `WRAPCOLS`. Jika Anda menginginkan jumlah kolom yang berbeda, cukup ubah argumen kedua:

```csharp
worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)"; // creates 3 columns
worksheet.Cells["A1"].Calculate();
```

Sekarang array terlihat seperti:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

**Tips pro:** Saat menangani dataset yang lebih besar, bangun string daftar secara dinamis (mis., menggunakan `string.Join(",", myNumbers)`) untuk menghindari nilai yang dikodekan secara tetap.

## Langkah 4: Menyimpan workbook dan memverifikasi output

Terakhir, kami menyimpan workbook ke disk sehingga Anda dapat membukanya di Excel dan mengonfirmasi pekerjaan **menghasilkan array Excel**:

```csharp
// Step 4: Save the workbook – you’ll see the calculated array in Excel
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Buka `output.xlsx` dan Anda akan melihat array 2‑kolom persis seperti yang dijelaskan. Jika Anda mengubah formula dan menghitung ulang, file yang disimpan akan diperbarui secara otomatis—tidak perlu penyegaran manual.

## Contoh Lengkap yang Dapat Dijalankan

Menggabungkan semuanya, berikut program lengkap yang dapat Anda masukkan ke dalam aplikasi console:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load (or create) a workbook
        var workbook = new Workbook(); // blank workbook

        // 2️⃣ Access the first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3️⃣ Write the array formula that wraps a list into 2 columns
        worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";

        // 4️⃣ Calculate the cell so the formula is evaluated
        worksheet.Cells["A1"].Calculate();

        // 5️⃣ (Optional) Save the workbook to view the result
        workbook.Save("YOUR_DIRECTORY/output.xlsx");

        Console.WriteLine("Workbook saved – check output.xlsx to see the 2‑column array.");
    }
}
```

**Output yang diharapkan:** Saat Anda membuka `output.xlsx`, sel `A1:B2` berisi angka 1‑4 yang disusun dalam dua kolom. Konsol mencetak konfirmasi yang ramah.

## Kasus Tepi & Pertanyaan Umum

### Bagaimana jika saya membutuhkan rentang dinamis bukan daftar yang dikodekan secara tetap?

Anda dapat membangun bagian daftar dari formula pada waktu runtime:

```csharp
int[] values = { 10, 20, 30, 40, 50, 60 };
string list = "{" + string.Join(",", values) + "}";
worksheet.Cells["A1"].Formula = $"=WRAPCOLS({list},3)";
worksheet.Cells["A1"].Calculate();
```

Ini masih menghasilkan output **menghasilkan array Excel**, tetapi kini data sumber berasal dari logika aplikasi Anda.

### Apakah `WRAPCOLS` bekerja pada versi Excel yang lebih lama?

`WRAPCOLS` tersedia mulai dari Excel 365/2019. Jika Anda menargetkan versi yang lebih lama, Anda harus mensimulasikan perilakunya dengan trik `INDEX` dan `MOD`, tetapi hal itu dengan cepat menjadi rumit. Menggunakan Aspose.Cells memungkinkan Anda mempertahankan formula modern dan tetap menghasilkan file yang kompatibel untuk kebanyakan pengguna.

### Bisakah saya menulis formula ke rentang alih-alih satu sel?

Ya—tetapkan formula yang sama ke sel paling kiri atas dari rentang, lalu panggil `Calculate()` pada objek rentang:

```csharp
var range = worksheet.Cells.CreateRange("A1", 2, 2); // 2x2 block
range.Formula = "=WRAPCOLS({1,2,3,4},2)";
range.Calculate();
```

Hasilnya identik, tetapi Anda memiliki kontrol lebih besar atas lokasi array.

## Pertimbangan Kinerja

Ketika Anda **menghitung sel Excel** untuk banyak formula, Aspose.Cells dapat melakukan perhitungan batch untuk kecepatan. Jika Anda menghasilkan ribuan array, panggil `workbook.CalculateFormula()` sekali setelah semua formula diatur, alih-alih `Calculate()` pada setiap sel. Ini secara dramatis mengurangi overhead.

## Langkah Selanjutnya

Sekarang Anda tahu cara **menulis formula array**, **menghitung sel Excel**, dan **membungkus daftar ke dalam kolom** untuk **membuat array 2‑kolom**, Anda dapat menjelajahi:

* **Generate Excel array** untuk laporan multi‑sheet  
* Terapkan styling (batas, format angka) pada rentang hasil  
* Ekspor workbook ke PDF atau CSV untuk pemrosesan lanjutan  
* Gabungkan dengan aturan validasi data untuk membuat spreadsheet interaktif  

Setiap hal ini dibangun di atas teknik inti yang kami bahas, memungkinkan Anda mengotomatisasi alur kerja Excel yang kompleks sepenuhnya dari C#.

---

**Singkatnya**, panduan ini menunjukkan cara **menulis formula array** di C# menggunakan Aspose.Cells, memaksa langkah **menghitung sel Excel**, dan **membungkus daftar ke dalam kolom** untuk **membuat array 2‑kolom** yang dapat Anda **menghasilkan array Excel**. Kode sepenuhnya dapat dijalankan, penjelasan mencakup *mengapa* di balik setiap baris, dan Anda memiliki tips untuk skala serta menangani kasus tepi.

Cobalah, ubah jumlah kolom, sambungkan data Anda sendiri, dan biarkan Excel melakukan pekerjaan berat untuk Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Menguasai Formula Array Excel dengan Aspose.Cells Java: Mempercepat Perhitungan dan Pemformatan](/cells/english/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/)
- [Membuat Objek Daftar Excel Menggunakan Aspose.Cells .NET: Panduan Langkah demi Langkah](/cells/english/net/tables-structured-references/create-excel-list-objects-aspose-cells-net/)
- [Mengimpor Array Multi Dimensi Excel dengan Aspose Cells Java](/cells/german/java/import-export/import-multi-dimensional-array-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}