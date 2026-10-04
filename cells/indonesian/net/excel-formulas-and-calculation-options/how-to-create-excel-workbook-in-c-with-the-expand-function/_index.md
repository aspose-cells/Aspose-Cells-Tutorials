---
category: general
date: 2026-10-04
description: Pelajari cara membuat workbook Excel di C# dan menggunakan EXPAND, memaksa
  perhitungan formula, serta menyimpan workbook sebagai XLSX sambil mengisi sebuah
  kolom dengan angka.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- how to use expand
- force formula calculation
- save workbook as xlsx
- populate column with numbers
language: id
lastmod: 2026-10-04
og_description: Buat buku kerja Excel di C# menggunakan Aspose.Cells. Tutorial ini
  menunjukkan cara menggunakan EXPAND, memaksa perhitungan rumus, dan menyimpan buku
  kerja sebagai XLSX sambil mengisi sebuah kolom dengan angka.
og_image_alt: Screenshot of a C# program that creates an Excel workbook and applies
  the EXPAND function
og_title: Membuat Workbook Excel di C# – panduan lengkap dengan EXPAND dan penyimpanan
  XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to create Excel workbook in C# and use EXPAND, force formula
    calculation, and save workbook as XLSX while populating a column with numbers.
  headline: How to create Excel workbook in C# with the EXPAND function
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Cara membuat workbook Excel di C# dengan fungsi EXPAND
url: /id/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-with-the-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Membuat Workbook Excel di C# dengan Fungsi EXPAND

Jika Anda perlu **membuat workbook Excel** secara programatis, panduan ini menunjukkan solusi lengkap yang siap dijalankan. Anda akan melihat cara **mengisi kolom dengan angka**, menerapkan fungsi **EXPAND** untuk menyebarkan data secara horizontal, **memaksa perhitungan formula**, dan akhirnya **menyimpan workbook sebagai XLSX**.  

Tutorial ini mencakup setiap langkah yang Anda perlukan, mulai dari inisialisasi workbook hingga verifikasi hasil. Tidak diperlukan dokumentasi eksternal—cukup salin kode, jalankan, dan Anda akan memiliki file Excel yang berfungsi penuh.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Framework 4.6+)
- Paket NuGet Aspose.Cells untuk .NET (`Install-Package Aspose.Cells`)
- Familiaritas dasar dengan sintaks C#
- IDE seperti Visual Studio atau VS Code

## Langkah 1: Buat workbook Excel dan akses lembar kerja pertama

Tindakan pertama adalah **membuat workbook Excel** dan mendapatkan referensi ke lembar kerja defaultnya. Aspose.Cells secara otomatis menambahkan lembar kerja pada indeks 0, sehingga Anda dapat langsung bekerja dengannya.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();          // create Excel workbook
        Worksheet sheet = workbook.Worksheets[0];   // first (default) worksheet
```

*Mengapa ini penting:* Menginstansiasi `Workbook` mengalokasikan struktur file internal, dan mengambil `Worksheets[0]` memberi Anda objek `Worksheet` konkret untuk memanipulasi baris, kolom, dan sel.

## Langkah 2: Isi kolom dengan angka

Selanjutnya, isi daftar vertikal di kolom A. Ini mendemonstrasikan **mengisi kolom dengan angka** dan menyediakan rentang sumber untuk fungsi EXPAND.

```csharp
        // Step 2: Fill a vertical list of values in column A
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);
```

*Tips profesional:* Gunakan `PutValue` untuk angka mentah, string, tanggal, atau primitif .NET apa pun. Metode ini secara otomatis menentukan tipe sel.

## Langkah 3: Cara menggunakan EXPAND – sebar daftar secara horizontal

Bagian **cara menggunakan expand** adalah inti dari tutorial ini. Fungsi `EXPAND` memperluas rentang sumber menjadi bentuk baru. Di sini kami memperluas rentang vertikal `A1:A3` menjadi satu baris yang mencakup tiga kolom, dimulai dari `B1`.

```csharp
        // Step 3: Apply the EXPAND function to spill the list horizontally starting at B1
        // The formula expands the range A1:A3 into 1 row and 3 columns (B1:D1)
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";
```

*Penjelasan:*  
- Argumen pertama (`A1:A3`) adalah rentang sumber.  
- Argumen kedua (`1`) memaksa hasil memiliki **1** baris.  
- Argumen ketiga (`3`) memaksa hasil memiliki **3** kolom.  

Saat workbook menghitung ulang, sel `B1`, `C1`, dan `D1` akan berisi `1`, `2`, dan `3` masing‑masing.

## Langkah 4: Paksa perhitungan formula

Aspose.Cells tidak secara otomatis mengevaluasi formula setelah Anda menetapkannya, sehingga Anda harus **memaksa perhitungan formula** sebelum menyimpan. Ini memastikan hasil EXPAND terwujud dalam file.

```csharp
        // Step 4: Force calculation of all formulas in the workbook
        workbook.CalculateFormula();   // triggers calculation engine
```

*Mengapa Anda membutuhkannya:* Tanpa memanggil `CalculateFormula`, file yang disimpan akan berisi string formula mentah, dan Excel hanya akan menghitung ulang saat file dibuka. Untuk pipeline otomatis, biasanya Anda menginginkan nilai ditulis segera.

## Langkah 5: Simpan workbook sebagai XLSX

Setelah workbook sepenuhnya siap, **simpan workbook sebagai XLSX** ke lokasi pilihan Anda. Ekstensi file menentukan format output; `.xlsx` menghasilkan workbook Office Open XML.

```csharp
        // Step 5: Save the workbook to a file
        string outputPath = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(outputPath);   // save workbook as XLSX
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

*Tips:* Jika Anda memerlukan format lain (CSV, PDF, dll.), cukup ubah ekstensi file atau gunakan `workbook.Save(outputPath, SaveFormat.Xls)` untuk versi Excel yang lebih lama.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua potongan kode memberikan program mandiri yang **membuat workbook Excel**, mengisi sebuah kolom, menggunakan **EXPAND**, memaksa perhitungan, dan **menyimpan workbook sebagai XLSX**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create Excel workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2. Populate column with numbers
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // 3. How to use EXPAND – spill horizontally
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";

        // 4. Force formula calculation
        workbook.CalculateFormula();

        // 5. Save workbook as XLSX
        string path = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(path);
        System.Console.WriteLine($"Workbook saved to {path}");
    }
}
```

### Output yang diharapkan

Setelah menjalankan program, buka `ExpandFunction.xlsx` di Excel. Anda akan melihat:

| A | B | C | D |
|---|---|---|---|
| 1 | 1 | 2 | 3 |
| 2 |   |   |   |
| 3 |   |   |   |

Nilai `1`, `2`, `3` pada sel `B1:D1` mengonfirmasi bahwa fungsi **EXPAND** berhasil dan langkah **memaksa perhitungan formula** berhasil menghasilkan nilai tersebut.

## Variasi umum dan kasus tepi

| Skenario | Penyesuaian |
|----------|------------|
| **Rentang sumber dinamis** | Gunakan `=EXPAND(A1:INDEX(A:A, COUNTA(A:A)), 1, 0)` untuk memperluas sebanyak baris yang terisi. |
| **Dimensi output berbeda** | Ubah argumen kedua dan ketiga dari `EXPAND` untuk mengontrol baris dan kolom. |
| **Beberapa lembar kerja** | Loop melalui `workbook.Worksheets` dan terapkan logika yang sama pada setiap lembar. |
| **Set data besar** | Panggil `workbook.CalculateFormula()` sekali setelah semua formula ditetapkan untuk menghindari perhitungan berulang. |
| **Menyimpan ke memory stream** | Ganti `workbook.Save(path)` dengan `workbook.Save(stream, SaveFormat.Xlsx)` ketika Anda memerlukan file dalam respons API web. |

## Daftar periksa pemecahan masalah

- **Formula tidak memperluas:** Pastikan `CalculateFormula()` dipanggil *setelah* menetapkan formula.  
- **File tidak ditemukan saat menyimpan:** Pastikan direktori target ada dan proses memiliki izin menulis.  
- **Tipe data tidak tepat:** Gunakan `PutValue` untuk angka; untuk tanggal, gunakan `PutValue(DateTime.Now)` atau `PutDateTime`.  
- **Versi tidak cocok:** Fungsi EXPAND memerlukan mesin perhitungan yang kompatibel dengan Excel 365; Aspose.Cells 23.9+ mendukungnya.

## Kesimpulan

Anda kini tahu cara **membuat workbook Excel** di C#, **mengisi kolom dengan angka**, menerapkan fungsi **EXPAND**, **memaksa perhitungan formula**, dan **menyimpan workbook sebagai XLSX**. Contoh ujung‑ke‑ujung ini dapat disesuaikan untuk pelaporan, transformasi data, atau skenario otomatisasi apa pun yang memerlukan output Excel dinamis.

### Langkah selanjutnya

- Jelajahi fungsi array dinamis lainnya seperti `FILTER`, `SORT`, dan `UNIQUE`.  
- Integrasikan pembuatan workbook ke dalam API ASP.NET Core untuk menyajikan file Excel secara on‑demand.  
- Ganti angka yang dikodekan secara tetap dengan data yang dibaca dari basis data atau file CSV untuk pelaporan dunia nyata.

Silakan bereksperimen dengan rentang, nama lembar, dan format output yang berbeda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menghitung Cotangent di Excel dengan C# – Buat Workbook, Gunakan EXPAND](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [Cara Menggunakan WRAPCOLS di C# – Buat Workbook Excel dengan Fungsi Wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Cara Membuat dan Menyimpan Workbook Excel sebagai ODS Menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}