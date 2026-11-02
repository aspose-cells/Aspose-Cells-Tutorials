---
category: general
date: 2026-03-22
description: Cara mengekspor Excel dengan format dan mempertahankan format angka.
  Pelajari cara mengonversi rentang Excel, mendapatkan hasil formula, dan mengekspor
  Excel dengan format menggunakan Aspose.Cells.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: id
og_description: Cara mengekspor Excel dengan pemformatan dan mempertahankan format
  angka. Panduan langkah demi langkah untuk mengonversi rentang Excel, mendapatkan
  hasil formula, dan mengekspor Excel dengan pemformatan di C#.
og_title: Cara Mengekspor Excel dengan Pemformatan – Pertahankan Format Angka
tags:
- C#
- Aspose.Cells
- Excel automation
title: Cara Mengekspor Excel dengan Pemformatan – Pertahankan Format Angka
url: /id/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengekspor Excel dengan Pemformatan – Mempertahankan Format Angka

Pernah bertanya-tanya **bagaimana cara mengekspor data Excel** sambil mempertahankan tampilan setiap sel persis seperti yang Anda lihat di workbook? Mungkin Anda perlu mengirimkan laporan ke klien, mengisi kontrol grid, atau sekadar menyimpan nilai-nilai ke dalam basis data. Masalah yang sering muncul adalah hilangnya pemformatan angka atau rumus yang berubah menjadi string mentah.  

Dalam tutorial ini kami akan membahas contoh C# lengkap yang siap‑jalankan yang **mempertahankan format angka**, **mengonversi rentang Excel** menjadi `DataTable`, **mengambil hasil rumus**, dan akhirnya **mengekspor Excel dengan pemformatan** menggunakan Aspose.Cells. Pada akhir tutorial Anda akan memiliki satu metode yang dapat Anda sisipkan ke proyek mana pun dan panggil dengan referensi worksheet.

> **Pratinjau cepat:** kode membuat sebuah workbook, menulis nilai dan sebuah rumus, memberi tahu Aspose.Cells untuk mengekspor sel sebagai string yang diformat, dan mencetak `123.456 | 246.912` – persis seperti yang Anda harapkan di Excel.

---

## Apa yang Anda Butuhkan

- **Aspose.Cells for .NET** (versi percobaan gratis sudah cukup untuk belajar)
- .NET 6.0 atau lebih baru (API-nya sama pada .NET Framework)
- Lingkungan pengembangan C# dasar (Visual Studio, VS Code, Rider… pilih sesuai kebutuhan)

Tidak diperlukan paket NuGet tambahan selain Aspose.Cells. Jika Anda belum menginstalnya, jalankan:

```bash
dotnet add package Aspose.Cells
```

---

## Langkah 1 – Membuat Workbook dan Menulis Nilai (termasuk sebuah rumus)

Pertama kami membuat workbook baru dan menaruh nilai numerik ke **A1**. Kemudian kami menambahkan rumus sederhana di **B1** yang mengalikan sel pertama dengan dua. Ini menyiapkan panggung untuk mendemonstrasikan **mengambil hasil rumus** nanti.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**Mengapa ini penting:**  
- `PutValue` menyimpan angka mentah, sedangkan `PutFormula` menyimpan perhitungan.  
- Aspose.Cells menjaga rumus tetap **aktif**, sehingga ketika kami kemudian meminta nilai sel, kami akan mendapatkan `246.912`, bukan string `"=A1*2"`.

---

## Langkah 2 – Meminta Aspose.Cells untuk Mengekspor Nilai sebagai String yang Diformat

Jika Anda hanya memanggil `ExportDataTable` dengan pengaturan default, sel numerik akan dikembalikan sebagai nilai `double` dasarnya. Itu menghilangkan pemisah ribuan, simbol mata uang, atau tempat desimal khusus yang mungkin Anda atur. Kelas `ExportTableOptions` memungkinkan kita **mempertahankan format angka** dan **mengekspor sebagai string**.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**Poin utama:** `ExportNumberFormat = true` adalah flag yang membuat **mempertahankan format angka** berfungsi. Tanpanya Anda akan melihat `"123.456"` dan `"246.912"` sebagai angka mentah, yang mungkin terlihat baik dalam kode tetapi tidak ketika Anda menempelkan data ke UI yang mengharapkan pemformatan yang sama seperti di Excel.

---

## Langkah 3 – Mencetak Data yang Diekspor (Verifikasi)

Sekarang kami memiliki `DataTable` penuh dengan string yang diformat, mari kita cetak isinya ke konsol. Ini juga menunjukkan bahwa kami berhasil **mengambil hasil rumus** tanpa harus mengevaluasi rumus secara manual.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

Menjalankan program mencetak:

```
123.456 | 246.912
```

Perhatikan bagaimana kolom kedua menampilkan **hasil rumus**, bukan teks rumus. Itulah yang Anda butuhkan saat **mengekspor Excel dengan pemformatan** untuk pemrosesan selanjutnya.

---

## Langkah 4 – Mengonversi Rentang Excel yang Lebih Besar (Opsional)

Contoh di atas menangani potongan kecil `A1:B1`, tetapi skenario dunia nyata sering memerlukan pengeksporan seluruh tabel. Metode yang sama bekerja untuk blok persegi panjang apa pun – cukup sesuaikan argumen `firstRow`, `firstColumn`, `totalRows`, dan `totalColumns`.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**Tips pro:** Jika lembar Anda sudah memiliki baris header, atur `includeColumnNames` menjadi `true`. Aspose.Cells akan menggunakan baris pertama dari rentang sebagai nama kolom, yang berguna ketika Anda nanti mengikat `DataTable` ke grid UI.

---

## Langkah 5 – Kesalahan Umum & Cara Menghindarinya

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| **Angka kehilangan koma atau simbol mata uang** | `ExportAsString` bernilai `false` atau `ExportNumberFormat` tidak disertakan | Atur keduanya `ExportAsString = true` **dan** `ExportNumberFormat = true`. |
| **Sel rumus mengembalikan teks rumus** | Anda tidak memanggil `CalculateFormula` sebelum mengekspor (hanya diperlukan jika workbook tidak diatur untuk auto‑calculate) | Aktifkan auto‑calculate (`workbook.CalculateFormula()`) atau gunakan `ExportAsString` yang memaksa evaluasi. |
| **Header muncul sebagai baris data** | `includeColumnNames` diatur ke `false` padahal rentang Anda mencakup baris header | Atur `includeColumnNames = true` untuk memperlakukan baris pertama sebagai nama kolom. |
| **Rentang besar menyebabkan tekanan memori** | Mengekspor seluruh lembar sekaligus memuat semua data ke memori | Ekspor dalam potongan (misalnya 500 baris sekaligus) dan gabungkan `DataTable` bila diperlukan. |

---

## Langkah 6 – Contoh Kerja Lengkap (Siap Salin‑Tempel)

Berikut adalah seluruh program, mulai dari pernyataan `using` hingga `Main`. Tempelkan ke aplikasi console dan tekan **F5** – Anda akan melihat output yang diformat secara langsung.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Output yang diharapkan**

```
123.456 | 246.912

Press any key to exit...
```

Itulah seluruh alur kerja **cara mengekspor excel**, dengan pemformatan tetap, hasil rumus dievaluasi, dan `DataTable` bersih siap untuk konsumen .NET apa pun.

---

## Kesimpulan

Kami telah membahas semua yang perlu Anda ketahui tentang **cara mengekspor data Excel** sambil **mempertahankan format angka**, **mengonversi rentang Excel** menjadi `DataTable`, dan **mengambil hasil rumus** tanpa parsing tambahan. Kuncinya adalah konfigurasi `ExportTableOptions` – setelah Anda mengatur `ExportAsString` dan `ExportNumberFormat` menjadi `true`, Aspose.Cells akan melakukan pekerjaan berat untuk Anda.

Dari sini Anda dapat:

- Sambungkan `DataTable` ke `DataGrid` WPF atau tampilan ASP.NET MVC.
- Tulis tabel ke file CSV sambil mempertahankan representasi visual yang persis.
- Perluas pendekatan ke beberapa lembar atau rentang dinamis.

Silakan bereksperimen dengan format berbeda (mata uang, persentase) dan blok data yang lebih besar. Jika Anda menemukan kejanggalan, kembali ke tabel **kesalahan umum** – tabel tersebut mencakup masalah paling sering terjadi saat Anda **mengekspor excel dengan pemformatan**.

Selamat coding, semoga spreadsheet yang Anda ekspor selalu tampak sehalus aslinya!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}