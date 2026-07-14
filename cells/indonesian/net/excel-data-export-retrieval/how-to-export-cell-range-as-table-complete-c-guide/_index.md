---
category: general
date: 2026-07-13
description: Cara mengekspor rentang sel sebagai tabel menggunakan C# dan ExportTableOptions.
  Pelajari langkah demi langkah penyiapan workbook, pemformatan, dan ekspor tabel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export cell range as table
- ExportTableOptions usage
- Workbook and Worksheet handling
- cell value formatting C#
- scientific notation export
language: id
lastmod: 2026-07-13
og_description: Cara mengekspor rentang sel sebagai tabel di C# dengan ExportTableOptions.
  Ikuti panduan ini untuk memformat sel, membuat workbook, dan mengekspor tabel dengan
  mudah.
og_image_alt: Diagram illustrating a C# code snippet that exports a single cell range
  as a formatted table
og_title: Cara Mengekspor Rentang Sel sebagai Tabel – Panduan Lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to export cell range as table using C# and ExportTableOptions.
    Learn step‑by‑step workbook setup, formatting, and table export.
  headline: How to Export Cell Range as Table – Complete C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
- data export
title: Cara Mengekspor Rentang Sel sebagai Tabel – Panduan Lengkap C#
url: /id/net/excel-data-export-retrieval/how-to-export-cell-range-as-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengekspor Rentang Sel sebagai Tabel – Panduan Lengkap C#

Pernah bertanya‑tanya **bagaimana cara mengekspor rentang sel sebagai tabel** tanpa membuat rambut Anda rontok karena keanehan format? Anda bukan satu‑satunya. Baik Anda memasukkan data ke dalam pipeline pelaporan atau hanya membutuhkan dump cepat bergaya CSV, menguasai proses ekspor dapat menghemat Anda berjam‑jam penyalinan‑tempel manual.

Dalam tutorial ini kami akan memandu Anda langkah demi langkah untuk mengambil sel numerik, menerapkan notasi ilmiah, dan mengekspornya sebagai tabel menggunakan **ExportTableOptions**. Pada akhir tutorial Anda akan memiliki cuplikan kode yang dapat dijalankan, memahami *mengapa* di balik setiap pemanggilan, dan mengetahui cara menyesuaikan kode untuk rentang yang lebih besar atau format yang berbeda.

## Prasyarat

- .NET 6 atau lebih baru (API berfungsi sama pada .NET Framework 4.7+)
- Aspose.Cells untuk .NET terpasang (`Install-Package Aspose.Cells`)
- Pemahaman dasar tentang sintaks C#; tidak memerlukan pengetahuan mendalam tentang internals Excel

Sudah ada? Bagus—mari kita mulai.

## Langkah 1: Siapkan Opsi Ekspor – Cara Mengekspor Rentang Sel sebagai Tabel

Hal pertama yang Anda butuhkan adalah instance **ExportTableOptions** yang memberi tahu perpustakaan cara memperlakukan isi sel. Tanpa ini, ekspor akan menggunakan nilai numerik mentah, yang dapat merusak konsumen hilir yang mengharapkan teks.

```csharp
// Step 1: Define export options – export the cell value as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Return the cell content as text
    CustomFormat = "0.00E+00"       // Apply scientific notation format
};
```

**Mengapa ini penting:**  
- `ExportAsString = true` memaksa perpustakaan menulis teks yang ditampilkan pada sel, bukan nilai double yang mendasarinya.  
- `CustomFormat` memungkinkan Anda menerapkan **ekspor notasi ilmiah**, berguna saat menangani angka yang sangat besar atau sangat kecil.

> **Pro tip:** Jika Anda memerlukan format tanggal atau mata uang, ganti `"0.00E+00"` dengan `"yyyy‑MM‑dd"` atau `"$#,##0.00"` masing‑masing.

## Langkah 2: Buat Workbook dan Ambil Worksheet Pertama – Penanganan Workbook dan Worksheet

Sebuah **Workbook** mewakili seluruh file Excel, sementara **Worksheet** adalah satu tab. Untuk ekspor sederhana kita akan tetap pada lembar pertama, yang selalu ada pada indeks 0.

```csharp
// Step 2: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

**Mengapa ini penting:**  
Membuat `Workbook` baru memastikan kanvas bersih—tidak ada gaya tersembunyi atau data sisa yang dapat mengganggu Anda. Mengakses `Worksheets[0]` adalah cara tercepat untuk mendapatkan pegangan pada lembar aktif tanpa harus memikirkan nama lembar.

## Langkah 3: Isi Sel Target – Pemformatan Nilai Sel C#

Sekarang kita memasukkan nilai numerik ke sel **A1** (baris 0, kolom 0). Nilai yang kami pilih sengaja memiliki desimal panjang agar Anda dapat melihat notasi ilmiah beraksi.

```csharp
// Step 3: Insert a numeric value into cell A1 (row 0, column 0)
sheet.Cells[0, 0].PutValue(12345.6789);
```

**Mengapa ini penting:**  
Pemanggilan `PutValue` secara otomatis menebak tipe data sel. Karena kami kemudian mengekspor sebagai string, double mentah akan dikonversi menggunakan format yang kami tetapkan sebelumnya, menghasilkan output yang rapi seperti `"1.23E+04"`.

## Langkah 4: Ekspor Rentang Sel yang Didefinisikan sebagai Tabel – Mengekspor Rentang Sel sebagai Tabel

Dengan opsi dan data yang sudah siap, langkah terakhir adalah memberi tahu Aspose.Cells untuk menulis rentang tersebut. Metode `ExportTable` mengharapkan baris/kolom mulai, ukuran rentang, dan objek opsi yang telah kami buat.

```csharp
// Step 4: Export the defined cell range as a table using the options above
// Parameters: startRow, startColumn, totalRows, totalColumns, options
sheet.ExportTable(0, 0, 1, 1, exportOptions);
```

**Mengapa ini penting:**  
- `totalRows = 1` dan `totalColumns = 1` membatasi ekspor ke satu sel saja, tetapi Anda dapat memperluas angka‑angka ini untuk mencakup blok yang lebih besar (misalnya `5, 3` untuk rentang 5‑baris × 3‑kolom).  
- Metode ini menulis data ke struktur tabel internal yang dapat disimpan sebagai CSV, HTML, atau bahkan langsung di‑stream ke klien.

### Menyimpan Hasil (Opsional)

Jika Anda ingin menyimpan tabel yang diekspor ke disk, Anda dapat menuliskannya ke file CSV:

```csharp
// Optional: Save the exported table as CSV for verification
using (var stream = new MemoryStream())
{
    sheet.ExportTableToCSV(stream, exportOptions);
    File.WriteAllBytes("ExportedTable.csv", stream.ToArray());
}
```

Menjalankan kode di atas akan menghasilkan file yang berisi:

```
1.23E+04
```

## Kasus Tepi & Variasi Umum

| Situasi | Apa yang Diubah | Alasan |
|-----------|----------------|--------|
| **Mengekspor beberapa baris** | Sesuaikan `totalRows` dan lakukan loop pada baris bila diperlukan | Memungkinkan ekspor batch tanpa memanggil `ExportTable` berulang kali |
| **Mempertahankan formula** | Set `ExportAsString = false` | Menjaga formula asli alih‑alih nilai yang ditampilkan |
| **Delimiter yang berbeda** | Gunakan overload `ExportTableToCSV(..., ',', ...)` | Berpindah dari nilai dipisahkan koma ke nilai dipisahkan tab atau pipa |
| **Worksheet besar** | Stream ekspor untuk menghindari `OutOfMemoryException` | Berfungsi baik untuk >10 000 baris |

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap disalin‑tempel. Program ini dapat dikompilasi pada proyek konsol .NET apa pun yang merujuk ke Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class ExportCellRangeDemo
{
    static void Main()
    {
        // 1️⃣ Define export options – how to export cell range as table
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            CustomFormat = "0.00E+00"
        };

        // 2️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Put a numeric value into A1
        sheet.Cells[0, 0].PutValue(12345.6789);

        // 4️⃣ Export the single‑cell range as a table
        sheet.ExportTable(0, 0, 1, 1, exportOptions);

        // Optional: write to CSV to see the result
        using (var ms = new MemoryStream())
        {
            sheet.ExportTableToCSV(ms, exportOptions);
            File.WriteAllBytes("ExportedTable.csv", ms.ToArray());
        }

        Console.WriteLine("Export complete! Check ExportedTable.csv");
    }
}
```

**Output yang diharapkan:**  
Sebuah file bernama `ExportedTable.csv` yang berisi satu baris:

```
1.23E+04
```

Jika Anda membuka CSV tersebut di editor teks, Anda akan melihat notasi ilmiah diterapkan persis seperti yang didefinisikan.

## Kesimpulan

Kami telah membahas **cara mengekspor rentang sel sebagai tabel** dari awal hingga akhir: menyiapkan `ExportTableOptions`, membuat `Workbook`, memasukkan data, dan akhirnya memanggil `ExportTable`. Dengan memahami setiap bagian, Anda kini dapat memperluas pendekatan ini ke rentang yang lebih besar, format yang berbeda, atau bahkan mengintegrasikannya ke dalam API web yang menyajikan data hasil Excel secara langsung.

Ke depan, Anda mungkin ingin menjelajahi:

- **ExportTableToHTML** untuk pratinjau siap web  
- **ExportTableToDataTable** untuk memberi makan langsung ke pipeline ADO.NET  
- **Format khusus lanjutan** untuk tanggal, mata uang, atau persentase  

Cobalah hal‑hal tersebut, dan Anda akan mengubah ekspor sel sederhana menjadi mesin penyampaian data yang serbaguna. Ada pertanyaan atau kasus penggunaan yang unik? Tinggalkan komentar di bawah—selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengekspor Baris Excel yang Terlihat Menggunakan Aspose.Cells untuk .NET: Panduan Langkah demi Langkah](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Cara Mengekspor File Excel di .NET Menggunakan Aspose.Cells: Panduan Komprehensif](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Cara Mengakses Sel Excel berdasarkan Nama Menggunakan Aspose.Cells untuk .NET: Panduan Langkah demi Langkah](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}