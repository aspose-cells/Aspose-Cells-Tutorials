---
category: general
date: 2026-11-19
description: Cara mengulang lembar kerja saat mengisi Excel dengan data array. Pelajari
  cara membuat beberapa lembar kerja dan mengisi lembar kerja dari daftar dalam beberapa
  langkah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: id
lastmod: 2026-11-19
og_description: Cara mengulang lembar kerja menggunakan SmartMarkerProcessor. Ikuti
  panduan ini untuk mengisi Excel dengan data array, menghasilkan beberapa lembar
  kerja, dan mengisi lembar kerja dari daftar.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Cara Mengulang Worksheet di Excel – Panduan Langkah demi Langkah
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: Cara mengulang lembar kerja di Excel dengan SmartMarkerProcessor
url: /id/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengulang worksheet di Excel dengan SmartMarkerProcessor

Jika Anda perlu **how to repeat worksheet** saat menghasilkan laporan Excel, panduan ini menunjukkan solusi lengkap yang dapat dijalankan. Pada akhir tutorial Anda akan dapat **populate Excel with array** data, **generate multiple worksheets**, dan **populate worksheet from list** menggunakan pustaka SmartMarkerProcessor.

Mengulang sebuah worksheet adalah kebutuhan umum ketika setiap departemen, wilayah, atau periode waktu memerlukan tab masing‑masing. Contoh di bawah menunjukkan langkah‑langkah tepat, menjelaskan mengapa setiap pengaturan penting, dan mencakup kasus tepi seperti daftar kosong atau penamaan khusus.

## Prasyarat

- .NET 6.0 atau yang lebih baru terpasang
- Referensi ke paket NuGet **GroupDocs.Viewer** (atau setara) yang berisi `SmartMarkerProcessor`
- Workbook templat Excel (`.xlsx`) dengan penanda seperti `${repeat:Dept}` ditempatkan pada baris yang ingin Anda ulang
- Familiaritas dasar dengan C# dan LINQ (opsional tetapi membantu)

Tidak diperlukan pustaka pihak ketiga tambahan.

## Langkah 1: Buat instance SmartMarkerProcessor

Processor mengatur penggantian penanda dan duplikasi worksheet. Membuat instance tanpa argumen menggunakan opsi default.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Membuat processor lebih awal memungkinkan Anda mengonfigurasi opsi global sebelum data apa pun diterapkan. Ini adalah dasar untuk **how to repeat worksheet** dengan benar.

## Langkah 2: Aktifkan pengulangan worksheet

Secara default processor menggantikan penanda hanya pada sheet saat ini. Menetapkan `RepeatWorksheet` ke `true` memberi tahu engine untuk menggandakan seluruh worksheet untuk setiap item dalam koleksi data.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

Mengaktifkan opsi ini adalah kunci untuk **generate multiple worksheets**—processor akan membuat tab baru untuk setiap elemen dalam array `Dept` dan mempertahankan format asli.

## Langkah 3: Siapkan sumber data sebagai array atau list

SmartMarkerProcessor bekerja dengan enumerable apa pun, tetapi menggunakan array membuat maksud lebih jelas ketika Anda ingin **populate worksheet from list**. Di sini kami membuat objek anonim yang berisi properti `Dept` yang menyimpan array string.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

Jika Anda sudah memiliki `List<string>` Anda dapat melewatkannya langsung; processor akan memperlakukannya dengan cara yang sama. Bagian pentingnya adalah nama properti (`Dept`) harus cocok dengan penanda `${repeat:Dept}` dalam templat.

## Langkah 4: Muat worksheet templat

Dengan asumsi Anda memiliki `ExcelPackage` (dari EPPlus) atau objek `Workbook`, ambil worksheet yang ingin Anda ulang. Variabel `ws` mewakili sheet tersebut.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

Jika Anda lebih suka pustaka lain (misalnya, ClosedXML), prinsip yang sama berlaku: dapatkan objek worksheet yang mengimplementasikan antarmuka yang diperlukan.

## Langkah 5: Proses worksheet dengan data

Sekarang terapkan data ke templat. Processor menggandakan worksheet untuk setiap departemen, mengganti penanda `${repeat:Dept}` dengan nama departemen yang sebenarnya, dan membiarkan sisanya tidak berubah.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

Setelah `Process` selesai, `ws` menjadi yang pertama dari beberapa worksheet—satu per departemen. Nama sheet asli dipertahankan, sementara duplikat menerima sufiks inkremental (misalnya, “Sheet1 (1)”, “Sheet1 (2)”). Anda dapat mengganti nama mereka setelahnya jika memerlukan skema penamaan khusus.

### Output yang diharapkan

Saat Anda membuka workbook hasil, Anda akan melihat:

- **Sheet1** – templat asli (sering dibiarkan kosong atau digunakan sebagai master)
- **Sheet1 (1)** – terisi dengan “HR”
- **Sheet1 (2)** – terisi dengan “IT”
- **Sheet1 (3)** – terisi dengan “Finance”

Setiap sheet berisi tata letak yang sama tetapi dengan nama departemen yang diganti di tempat `${repeat:Dept}` muncul.

## Menangani kasus tepi

### Array kosong atau null

Jika `Dept` null atau kosong, processor tidak akan membuat worksheet tambahan. Untuk menghindari workbook yang sepenuhnya kosong, Anda dapat menambahkan pengecekan:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Nama worksheet khusus

Skema penamaan default mungkin tidak cocok untuk setiap kebutuhan pelaporan. Setelah proses, ganti nama setiap sheet menggunakan loop:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### Mengisi kolom tambahan

Jika Anda perlu **populate excel with array** nilai lebih dari satu penanda, perpanjang objek data:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

Kemudian sesuaikan penanda templat menjadi `${repeat:Dept.Name}` dan `${repeat:Dept.Headcount}`. Processor akan mengulang baris untuk setiap departemen dan mengisi kedua kolom.

## Contoh lengkap yang berfungsi

Berikut adalah aplikasi konsol mandiri yang menunjukkan alur lengkap dari pemuatan templat hingga menyimpan workbook akhir.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Penjelasan bagian kunci**

- **Processor creation** – menetapkan engine yang akan menginterpretasikan penanda.
- **RepeatWorksheet option** – mengaktifkan fitur inti yang menjawab *how to repeat worksheet*.
- **Data source** – menggunakan array (`new[]`) untuk memenuhi **populate excel with array**.
- **Template loading** – menunjukkan cara umum untuk memperoleh objek worksheet.
- **Processing** – melakukan duplikasi dan penyisipan data dalam satu panggilan.
- **Renaming** – menunjukkan cara mengubah nama generik “(1)”, “(2)” menjadi judul yang bermakna, kebutuhan tipikal setelah **generate multiple worksheets**.

Menjalankan program ini menghasilkan `Result.xlsx` dengan tiga tab khusus departemen, masing‑masing terisi dari array.

## Kesalahan umum dan tips profesional

- **Marker spelling** – penanda harus cocok persis dengan nama properti (`${repeat:Dept}`). Kesalahan ketik mencegah pengulangan.
- **Worksheet index** – setelah proses, sheet asli tetap pada indeks 0; sheet yang dihasilkan mengikuti secara berurutan. Kesalahan indeks dapat menyebabkan penamaan ulang tab yang salah.
- **Large data sets** – menghasilkan ratusan worksheet dapat meningkatkan ukuran file secara dramatis. Pertimbangkan membagi laporan atau menggunakan satu sheet dengan bagian yang dikelompokkan jika kinerja menjadi masalah.
- **Thread safety** – `SmartMarkerProcessor` tidak thread‑safe. Buat instance terpisah per thread jika Anda memproses beberapa workbook secara paralel.

## Kesimpulan

Anda kini tahu **how to repeat worksheet** di Excel menggunakan SmartMarkerProcessor, cara **populate excel with array** data, cara **generate multiple worksheets**, dan cara **populate worksheet from list** secara efisien. Contoh lengkap menggabungkan semua konsep, dan langkah penamaan ulang opsional memungkinkan Anda menghasilkan nama tab yang bersih dan ramah pengguna.

Selanjutnya, Anda mungkin ingin menjelajahi:

Berikut tutorial yang mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Repeat Worksheets – Complete Guide for Excel Automation](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Create Worksheet Per Item – How to Repeat Worksheet in C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}