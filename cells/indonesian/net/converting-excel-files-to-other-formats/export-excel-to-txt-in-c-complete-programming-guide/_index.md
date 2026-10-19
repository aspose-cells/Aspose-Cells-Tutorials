---
category: general
date: 2026-08-11
description: Ekspor Excel ke TXT di C# dengan panduan langkah demi langkah. Pelajari
  cara mengonversi xlsx ke teks biasa menggunakan Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: id
lastmod: 2026-08-11
og_description: Ekspor excel ke txt di C# dengan cepat. Tutorial ini menunjukkan cara
  mengonversi xlsx ke teks biasa, mengonfigurasi format, dan menangani lembar kerja
  besar.
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: Ekspor Excel ke TXT dalam C# – panduan langkah demi langkah untuk pengembang
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: Ekspor Excel ke TXT dalam C# – panduan pemrograman lengkap
url: /id/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengekspor excel ke txt di C# – panduan pemrograman lengkap

Jika Anda perlu **mengekspor excel ke txt** Anda dapat mencapai hasil tersebut dengan beberapa baris kode C#. Panduan ini menunjukkan cara mengonversi workbook `.xlsx` menjadi file teks biasa sambil mempertahankan format data yang Anda tentukan.

Mengekspor lembar kerja sebagai file teks adalah kebutuhan umum ketika sistem hilir hanya menerima data yang dipisahkan atau ketika Anda perlu mengaudit nilai sel mentah. Pada bagian berikut Anda akan belajar cara mengonfigurasi format tanggal dan angka, menangani lembar besar, dan menghindari jebakan umum.

## Prasyarat untuk mengonversi xlsx ke teks biasa

* .NET 6.0 (atau lebih baru) terpasang – kode menargetkan .NET Standard 2.0, sehingga juga berfungsi dengan .NET Framework 4.6+.
* Lisensi untuk **Aspose.Cells** (evaluasi gratis dapat digunakan untuk pengujian).
* IDE seperti Visual Studio 2022 atau Visual Studio Code.
* File Excel bernama `input.xlsx` ditempatkan di folder yang dapat Anda referensikan dari proyek Anda.

Item-item ini adalah satu-satunya persyaratan eksternal; tutorial ini tidak bergantung pada paket NuGet tambahan.

## Cara mengekspor excel ke txt menggunakan Aspose.Cells

Aspose.Cells menyediakan kelas `ExportTableOptions` yang memungkinkan Anda mengontrol bagaimana nilai sel dirender sebagai string. Dengan mengatur `ExportAsString` ke `true` Anda memaksa setiap sel ditulis sebagai teks, yang penting ketika Anda menginginkan output teks biasa yang deterministik.

### Langkah 1 – memuat workbook

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*Konstruktor `Workbook` membaca file Excel ke dalam memori. Jika file tidak ada, sebuah pengecualian akan dilempar, jadi Anda mungkin ingin membungkus pemanggilan ini dalam blok try‑catch untuk kode produksi.*

### Langkah 2 – mendapatkan lembar kerja pertama

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*Worksheets menggunakan indeks berbasis nol, sehingga indeks 0 mengacu pada tab pertama. Anda dapat mengganti indeks dengan nama lembar (`workbook.Worksheets["Sheet1"]`) ketika perlu menargetkan tab tertentu.*

### Langkah 3 – mendefinisikan opsi ekspor untuk konversi teks

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString` menjamin bahwa setiap sel, terlepas dari tipe aslinya, menjadi string dalam file output. Properti `DateTimeFormat` dan `NumberFormat` memungkinkan Anda mengontrol bagaimana tanggal dan angka ditampilkan, yang penting ketika Anda **mengonversi xlsx ke teks biasa** untuk sistem yang mengharapkan pola tertentu.*

### Langkah 4 – mengekspor lembar kerja sebagai file teks

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable` menulis konten lembar kerja ke file teks biasa menggunakan opsi yang Anda berikan. Pemisah default adalah karakter tab (`\t`). Jika Anda memerlukan pemisah lain, Anda dapat menggunakan overload yang menerima instance `ExportTableOptions` dan menentukan `ExportTableOptions.Separator`. File yang dihasilkan dapat dibuka di editor teks apa pun atau diimpor ke basis data.*

#### Output yang diharapkan

Assume `input.xlsx` contains:

| A            | B       | C            |
|--------------|---------|--------------|
| 2023‑05‑01   | 1234.5  | Teks contoh  |

With the options above the `Exported.txt` file will contain:

```
2023-05-01	1,234.50	Sample text
```

Setiap kolom dipisahkan oleh tab, tanggal mengikuti format `yyyy‑MM‑dd`, dan angka menggunakan koma sebagai pemisah ribuan serta dua tempat desimal.

## Kesalahan umum saat Anda mengekspor lembar kerja sebagai file teks

| Issue | Why it happens | How to avoid it |
|-------|----------------|-----------------|
| Pemformatan angka tergantung locale | Format default menghormati budaya OS, yang dapat menghasilkan koma atau titik secara tidak konsisten. | Setel `NumberFormat` secara eksplisit di `ExportTableOptions`. |
| Baris atau kolom tersembunyi muncul di output | Aspose.Cells mengekspor seluruh rentang yang digunakan, termasuk baris tersembunyi. | Setel `ExportTableOptions.ExportHiddenRows = false` dan `ExportHiddenColumns = false` jika ingin melewatkannya. |
| Lembar kerja besar menyebabkan tekanan memori | Seluruh workbook dimuat ke memori sebelum diekspor. | Gunakan `Workbook.LoadOptions` dengan `LoadDataOnly = true` untuk mengurangi penggunaan memori, atau proses file dalam potongan. |
| Sel tanggal disimpan sebagai teks dalam file sumber | Jika sebuah sel sudah berisi string yang diformat, exporter memperlakukannya sebagai teks dan mengabaikan `DateTimeFormat`. | Pastikan workbook sumber menyimpan tanggal sebagai tipe tanggal Excel yang tepat. |

Menangani masalah-masalah ini membuat proses **cara mengekspor lembar kerja excel sebagai teks** menjadi handal di berbagai lingkungan.

## Memperluas solusi – pemisah khusus dan ekspor streaming

Jika Anda memerlukan file nilai yang dipisahkan koma (CSV) alih-alih file yang dipisahkan tab, ubah opsi berikut:

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

Untuk file yang lebih besar dari 500 MB, streaming output mencegah aplikasi kehabisan RAM:

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

Overload yang menerima `Stream` menulis baris secara bertahap, yang ideal untuk pekerjaan batch atau layanan web yang mengembalikan file teks langsung ke klien.

## Verifikasi hasil secara programatik

Setelah ekspor selesai Anda dapat membaca baris pertama kembali ke memori untuk mengonfirmasi formatnya:

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

Menjalankan potongan kode ini seharusnya mencetak baris yang sama seperti yang ditunjukkan pada bagian *Output yang diharapkan*, memberi Anda keyakinan bahwa konversi berhasil.

## Ringkasan kode lengkap

Menggabungkan semua bagian menghasilkan program mandiri yang dapat Anda salin ke aplikasi konsol:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

Kompilasi dan jalankan program; file `Exported.txt` muncul di direktori yang sama dengan workbook sumber.

## Langkah selanjutnya dan topik terkait

* **Export worksheet as text file** – bereksperimen dengan pemisah yang berbeda, encoding (UTF‑8 vs. ASCII), dan gaya akhir baris untuk kompatibilitas lintas platform.
* **Bulk conversion** – lakukan loop melalui `workbook.Worksheets` untuk menghasilkan file teks terpisah untuk setiap tab.
* **Integration with databases** – alirkan teks yang dihasilkan langsung ke operasi bulk‑insert untuk SQL Server atau PostgreSQL.
* 

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Mengekspor File Excel di .NET Menggunakan Aspose.Cells: Panduan Komprehensif](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Cara Mengekspor Baris Excel yang Terlihat Menggunakan Aspose.Cells untuk .NET: Panduan Langkah demi Langkah](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Cara Mengekspor Diagram Excel ke PDF Menggunakan Aspose.Cells untuk .NET: Panduan Langkah demi Langkah](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}