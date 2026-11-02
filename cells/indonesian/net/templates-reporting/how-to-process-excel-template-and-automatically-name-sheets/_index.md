---
category: general
date: 2026-10-10
description: Pelajari cara memproses templat Excel di C# sambil secara otomatis memberi
  nama sheet. Panduan langkah demi langkah dengan kode SmartMarkerProcessor dan praktik
  terbaik.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- process excel template
- automatically name sheets
- SmartMarkerProcessor
- Excel automation C#
- worksheet data binding
language: id
lastmod: 2026-10-10
og_description: Proses templat Excel di C# dan secara otomatis beri nama sheet dengan
  SmartMarkerProcessor. Ikuti tutorial terperinci ini untuk menghasilkan workbook
  dinamis.
og_image_alt: Screenshot showing process excel template with automatically named sheets
  in a C# application
og_title: Proses templat Excel dan secara otomatis beri nama sheet di C# – panduan
  lengkap
schemas:
- author: GroupDocs
  dateModified: '2026-10-10'
  description: Learn how to process Excel template in C# while automatically name
    sheets. Step‑by‑step guide with SmartMarkerProcessor code and best practices.
  headline: How to process Excel template and automatically name sheets in C#
  type: TechArticle
- description: Learn how to process Excel template in C# while automatically name
    sheets. Step‑by‑step guide with SmartMarkerProcessor code and best practices.
  name: How to process Excel template and automatically name sheets in C#
  steps:
  - name: Large data sets
    text: 'When the data source contains hundreds of rows, the processor creates a
      separate sheet for each row by default. To keep the workbook from exploding,
      you can:'
  - name: Existing sheet name conflicts
    text: If the template already contains a sheet named `Detail`, the processor appends
      a numeric suffix to avoid collision (`Detail_0`, `Detail_1`, …). To enforce
      a custom conflict‑resolution strategy, inspect `Worksheet.Sheets` before processing
      and rename any conflicting sheets.
  - name: Non‑Excel templates
    text: The same `SmartMarkerProcessor` can process Word, PowerPoint, or PDF templates.
      The only change is the class you instantiate (`Document`, `Presentation`, etc.).
      The **process excel template** pattern stays identical, which means you can
      reuse the code with minimal adjustments.
  type: HowTo
tags:
- Excel
- C#
- SmartMarker
- Automation
title: Cara memproses templat Excel dan secara otomatis menamai lembar kerja di C#
url: /id/net/templates-reporting/how-to-process-excel-template-and-automatically-name-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara memproses template Excel dan secara otomatis menamai sheet di C#

Jika Anda perlu **memproses template Excel** dalam aplikasi .NET, panduan ini menunjukkan cara yang andal untuk menghasilkan workbook dan **secara otomatis menamai sheet**. Dengan menggunakan `SmartMarkerProcessor` dari GroupDocs.Parser Anda dapat mengikat data ke template, membuat sheet detail secara dinamis, dan menjaga workbook tetap rapi tanpa harus menamai ulang secara manual.

Anda akan menyelesaikan tutorial dengan contoh yang dapat dijalankan sepenuhnya yang membaca template, menerapkan sumber data, dan menghasilkan sheet dengan nama `Detail`, `Detail_1`, `Detail_2`, … Semua namespace yang diperlukan, langkah konfigurasi, dan jebakan umum dibahas, sehingga Anda dapat menyalin kode ke dalam proyek Anda dengan percaya diri.

## Prasyarat

* .NET 6.0 atau lebih baru (kode ini bekerja dengan .NET Core dan .NET Framework)
* Referensi ke paket NuGet **GroupDocs.Parser** (versi 23.5 atau lebih baru)
* Template Excel (`Template.xlsx`) yang berisi tag SmartMarker seperti `{{Table}}` untuk data master‑detail
* Model data sederhana (misalnya, `DataTable` atau daftar objek) yang cocok dengan marker di template

Jika salah satu dari item ini belum ada, instal paket NuGet dengan:

```bash
dotnet add package GroupDocs.Parser
```

## Gambaran Solusi

Solusi ini mengikuti tiga fase logis:

1. **Membuat instance `SmartMarkerProcessor`** – objek ini mengendalikan seluruh mesin templating.
2. **Mengonfigurasi processor untuk secara otomatis menamai sheet detail** – opsi `DetailSheetNewName` menentukan nama dasar dan perpustakaan menambahkan sufiks inkremental.
3. **Menjalankan `Process`** – metode ini membaca template, menggabungkan sumber data, dan menulis hasil ke workbook baru.

Setiap fase dijelaskan di bawah ini, bersama dengan kode tepat yang Anda perlukan.

## Langkah 1: Membuat instance SmartMarkerProcessor

Processor adalah titik masuk untuk semua operasi SmartMarker. Ia tidak memerlukan argumen konstruktor, tetapi Anda dapat memberikan objek `SmartMarkerOptions` khusus nanti jika memerlukan pengaturan lanjutan.

```csharp
using GroupDocs.Parser;
using GroupDocs.Parser.Options;

// ...

// Step 1: Instantiate the processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

*Mengapa ini penting*: Membuat instance processor satu kali per operasi menjaga penggunaan memori tetap rendah dan memungkinkan Anda menggunakan kembali objek yang sama untuk beberapa template jika diperlukan.

## Langkah 2: Mengonfigurasi penamaan sheet otomatis

Ketika tabel master‑detail berkembang menjadi lembar kerja terpisah, perpustakaan secara otomatis membuat sheet baru. Dengan mengatur `DetailSheetNewName`, Anda mengendalikan nama dasar yang digunakan mesin. Perpustakaan menambahkan garis bawah dan nomor yang meningkat untuk setiap sheet tambahan.

```csharp
// Step 2: Define the base name for automatically created detail sheets
processor.Options.DetailSheetNewName = "Detail"; // Sheets become Detail, Detail_1, Detail_2, …
```

*Tips*:

* Pilih nama dasar yang tidak bentrok dengan nama sheet yang sudah ada di template.
* Skema penamaan bekerja untuk jumlah baris detail berapa pun; perpustakaan berhenti menambahkan sufiks ketika sheet terakhir dibuat.
* Jika Anda memerlukan pola penamaan yang berbeda (mis., prefiks alih‑alih sufiks), Anda dapat memanipulasi `processor.Options.DetailSheetNewName` sebelum setiap pemanggilan.

## Langkah 3: Memproses worksheet dengan sumber data

Metode `Process` menerima tiga argumen:

* **worksheet sumber** (`Worksheet` object) – Anda mendapatkannya dengan memuat file template.
* **stream target** – tempat workbook yang telah diproses akan ditulis.
* **sumber data** – objek apa pun yang mengimplementasikan `IDataSource` (mis., `DataTable`, `IEnumerable<T>`).

Berikut contoh lengkap yang memuat `Template.xlsx`, mengikat `DataTable`, dan menyimpan hasil ke `Result.xlsx`.

```csharp
using System.Data;
using System.IO;
using GroupDocs.Parser;
using GroupDocs.Parser.Data;
using GroupDocs.Parser.Options;

// ...

// Load the Excel template into a Worksheet object
using (FileStream templateStream = File.OpenRead("Template.xlsx"))
{
    // Create a Worksheet instance from the template
    Worksheet ws = new Worksheet(templateStream);

    // Prepare a simple DataTable as the data source
    DataTable dt = new DataTable("Employees");
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    // Populate the table with sample rows
    dt.Rows.Add("Alice", "Engineering", 95000);
    dt.Rows.Add("Bob", "Marketing", 72000);
    dt.Rows.Add("Charlie", "Sales", 68000);

    // Wrap the DataTable in a DataSource object required by SmartMarker
    IDataSource dataSource = new DataTableSource(dt);

    // Step 1 and Step 2 have already been performed earlier
    // Now process the worksheet
    using (MemoryStream resultStream = new MemoryStream())
    {
        processor.Process(ws, dataSource, resultStream);

        // Write the processed workbook to a physical file
        File.WriteAllBytes("Result.xlsx", resultStream.ToArray());
    }
}
```

*Penjelasan baris kunci*:

* `new Worksheet(templateStream)` membaca file Excel dan membuat representasi dalam memori yang dapat dimanipulasi oleh SmartMarker.
* `DataTableSource` mengimplementasikan `IDataSource`, memungkinkan processor untuk mengiterasi baris dan mengganti marker seperti `{{Employees.Name}}`.
* `processor.Process(ws, dataSource, resultStream)` menggabungkan data dan menulis workbook akhir ke `resultStream`. Metode ini secara otomatis membuat sheet detail bernama `Detail`, `Detail_1`, dll., karena opsi yang diatur pada Langkah 2.
* Setelah diproses, hasil disimpan sebagai `Result.xlsx`. Buka file tersebut di Excel untuk memverifikasi bahwa tiga sheet detail ada, masing‑masing berisi baris dari tabel `Employees`.

## Verifikasi output

Buka `Result.xlsx` dan periksa hal berikut:

| Nama sheet | Konten yang diharapkan |
|------------|------------------------|
| Detail | Baris header (`Name`, `Department`, `Salary`) dan baris data pertama (`Alice`) |
| Detail_1 | Baris data kedua (`Bob`) |
| Detail_2 | Baris data ketiga (`Charlie`) |

Jika sheet muncul dengan nama dasar dan sufiks inkremental yang benar, alur kerja **process excel template** berhasil dan fitur **automatically name sheets** berfungsi sebagaimana mestinya.

## Menangani kasus tepi

### Set data besar

Ketika sumber data berisi ratusan baris, processor secara default membuat sheet terpisah untuk setiap baris. Untuk mencegah workbook menjadi terlalu besar, Anda dapat:

* **Mengelompokkan baris**: ubah template untuk menggunakan marker tabel yang mengulang dalam satu sheet alih‑alih membuat sheet baru per baris.
* **Membatasi pembuatan sheet**: atur `processor.Options.MaxDetailSheets` ke angka yang wajar (mis., 50) dan tangani kelebihan secara manual.

```csharp
processor.Options.MaxDetailSheets = 50; // Prevent more than 50 auto‑generated sheets
```

### Konflik nama sheet yang sudah ada

Jika template sudah berisi sheet bernama `Detail`, processor menambahkan sufiks numerik untuk menghindari bentrok (`Detail_0`, `Detail_1`, …). Untuk menerapkan strategi penyelesaian konflik khusus, periksa `Worksheet.Sheets` sebelum pemrosesan dan ganti nama sheet yang konflik.

```csharp
foreach (var sheet in ws.Sheets)
{
    if (sheet.Name.Equals("Detail", StringComparison.OrdinalIgnoreCase))
    {
        sheet.Name = "BaseDetail";
    }
}
```

### Template non‑Excel

`SmartMarkerProcessor` yang sama dapat memproses template Word, PowerPoint, atau PDF. Satu‑satunya perubahan adalah kelas yang Anda instantiate (`Document`, `Presentation`, dll.). Pola **process excel template** tetap sama, yang berarti Anda dapat menggunakan kembali kode dengan penyesuaian minimal.

## Tips profesional untuk penggunaan produksi

* **Gunakan kembali processor**: Buat singleton `SmartMarkerProcessor` jika Anda memproses banyak template dalam layanan web. Ini mengurangi beban alokasi.
* **Gunakan stream alih‑alih file**: Dalam skenario throughput tinggi, simpan template dan hasil dalam memory stream untuk menghindari I/O disk.
* **Dispose objek**: Semua instance `Worksheet`, `FileStream`, dan `MemoryStream` mengimplementasikan `IDisposable`. Menggunakan blok `using`, seperti yang ditunjukkan, menjamin pelepasan sumber daya yang tepat.
* **Logging**: Aktifkan `processor.Options.Logging` untuk menangkap informasi pemrosesan yang detail, yang membantu mendiagnosa kesalahan template dengan cepat.

## Contoh lengkap yang dapat dijalankan

Berikut seluruh program yang dikompilasi menjadi satu file. Salin ke proyek konsol dan jalankan; workbook output akan muncul di folder proyek.

```csharp
using System;
using System.Data;
using System.IO;
using GroupDocs.Parser;
using GroupDocs.Parser.Data;
using GroupDocs.Parser.Options;

class ExcelTemplateProcessor
{
    static void Main()
    {
        // 1️⃣ Create the processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Set automatic sheet naming
        processor.Options.DetailSheetNewName = "Detail";

        // Load the template
        using (FileStream templateStream = File.OpenRead("Template.xlsx"))
        {
            Worksheet ws = new Worksheet(templateStream);

            // Build a sample data source
            DataTable dt = new DataTable("Employees");
            dt.Columns.Add("Name", typeof(string));
            dt.Columns.Add("Department", typeof(string));
            dt.Columns.Add("Salary", typeof(decimal));
            dt.Rows.Add("Alice", "Engineering", 95000);
            dt.Rows.Add("Bob", "Marketing", 72000);
            dt.Rows.Add("Charlie", "Sales", 68000);
            IDataSource dataSource = new DataTableSource(dt);

            // 3️⃣ Process the worksheet
            using (MemoryStream resultStream = new MemoryStream())
            {
                processor.Process(ws, dataSource, resultStream);
                File.WriteAllBytes("Result.xlsx", resultStream.ToArray());
            }
        }

        Console.WriteLine("Processing complete. Check Result.xlsx.");
    }
}
```

Menjalankan program mencetak “Processing complete. Check Result.xlsx.” dan membuat file Excel yang menunjukkan alur kerja **process excel template** dengan **automatically name sheets**.

## Kesimpulan

Sekarang Anda tahu cara **process Excel template** file di C# sambil membiarkan perpustakaan **automatically name sheets** berdasarkan nama dasar khusus. Tutorial ini mencakup pembuatan processor, konfigurasi opsi, pengikatan data, dan langkah verifikasi, serta penanganan kasus tepi dan tips produksi. Terapkan pola yang sama ke proyek yang lebih besar, integrasikan ke API web, atau perluas ke format Office lainnya.

**Langkah selanjutnya** yang dapat Anda jelajahi:

* Gunakan `processor.Options.DetailSheetNewName` dengan nilai dinamis (mis., menyertakan tanggal atau ID pengguna).
* Gabungkan beberapa sumber data untuk menghasilkan hierarki master‑detail di beberapa worksheet.
* Bereksperimen dengan styling tag SmartMarker untuk mengontrol font, warna, dan format angka langsung dari template.

Selamat coding, dan nikmati otomatisasi Excel yang lebih sederhana!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Create Excel from Template – Step‑by‑Step Guide for .NET Developers](/cells/english/net/templates-reporting/create-excel-from-template-step-by-step-guide-for-net-develo/)
- [How to Merge and Rename Excel Sheets Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/worksheet-management/merge-rename-excel-sheets-aspose-cells-net/)
- [How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide](/cells/english/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}