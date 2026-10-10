---
category: general
date: 2026-10-10
description: Buat data smart marker dan isi data templat Excel menggunakan smart marker
  Aspose.Cells. Ikuti panduan langkah demi langkah ini untuk mengotomatiskan laporan
  Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create smart marker data
- fill excel template data
- use aspose.cells smart markers
language: id
lastmod: 2026-10-10
og_description: Buat data smart marker dengan smart marker Aspose.Cells dan isi data
  templat Excel dalam hitungan menit. Panduan ini membawa Anda melalui contoh lengkap
  yang dapat dijalankan.
og_image_alt: Screenshot showing the process of creating smart marker data in an Excel
  worksheet
og_title: Buat data smart marker dan isi data templat Excel
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create smart marker data and fill Excel template data using Aspose.Cells
    smart markers. Follow this step‑by‑step guide to automate Excel reports.
  headline: How to create smart marker data and fill Excel template data
  type: TechArticle
- description: Create smart marker data and fill Excel template data using Aspose.Cells
    smart markers. Follow this step‑by‑step guide to automate Excel reports.
  name: How to create smart marker data and fill Excel template data
  steps:
  - name: '**Loading the workbook** gives the processor a concrete file to work on.'
    text: '**Loading the workbook** gives the processor a concrete file to work on.'
  - name: '**Selecting the worksheet** ensures the processor scans the correct sheet;
      you can target any sheet by index or name.'
    text: '**Selecting the worksheet** ensures the processor scans the correct sheet;
      you can target any sheet by index or name.'
  - name: '**The data source** is an array of anonymous objects. Each property name
      (`fieldName`) must match the marker name inside `${Comment:fieldName}`.'
    text: '**The data source** is an array of anonymous objects. Each property name
      (`fieldName`) must match the marker name inside `${Comment:fieldName}`.'
  - name: '**`SmartMarkerProcessor`** is the engine that parses tags and performs
      the replacement.'
    text: '**`SmartMarkerProcessor`** is the engine that parses tags and performs
      the replacement.'
  - name: '**`Process`** performs the heavy lifting: it reads every `${...}` tag,
      looks up the matching property in the data source, and writes the value into
      the cell.'
    text: '**`Process`** performs the heavy lifting: it reads every `${...}` tag,
      looks up the matching property in the data source, and writes the value into
      the cell.'
  - name: '**Saving the workbook** writes the updated file to disk, ready for downstream
      consumption.'
    text: '**Saving the workbook** writes the updated file to disk, ready for downstream
      consumption.'
  - name: Open a new Excel workbook.
    text: Open a new Excel workbook.
  - name: 'In any cell where you want dynamic content, type a Smart Marker tag, for
      example:'
    text: 'In any cell where you want dynamic content, type a Smart Marker tag, for
      example:'
  - name: Save the file as `Template.xlsx`.
    text: Save the file as `Template.xlsx`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cara membuat data smart marker dan mengisi data templat Excel
url: /id/net/smart-markers-dynamic-data/how-to-create-smart-marker-data-and-fill-excel-template-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat data smart marker dan mengisi data template Excel

Jika Anda perlu **membuat data smart marker** untuk sebuah workbook Excel, smart marker Aspose.Cells membuatnya menjadi mudah. Tutorial ini menunjukkan cara **mengisi data template Excel** menggunakan smart marker dalam beberapa baris kode C#.

Anda akan belajar cara menyisipkan tag Smart Marker dalam sebuah template, menyediakan sumber data, menjalankan processor, dan menyimpan file yang telah terisi. Tidak diperlukan alat eksternal—hanya Aspose.Cells untuk .NET dan proyek C# dasar.

## Apa yang Anda butuhkan

- .NET 6.0 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.7+)
- Aspose.Cells untuk .NET (paket NuGet `Aspose.Cells`)
- Sebuah workbook Excel yang berisi tag Smart Marker seperti `${Comment:fieldName}`
- IDE C# (Visual Studio, Rider, atau VS Code)

> **Pro tip:** Simpan workbook di folder yang sama dengan proyek atau gunakan path absolut untuk menghindari kesalahan file‑tidak‑ditemukan.

## Cara membuat data smart marker dengan Aspose.Cells

Inti dari solusi ini adalah `SmartMarkerProcessor`. Ia memindai worksheet untuk tag, mengambil nilai yang cocok dari sumber data, dan menulis hasilnya kembali ke lembar.

```csharp
using Aspose.Cells;
using System;

// 1️⃣ Load the workbook that contains Smart Marker tags.
Workbook workbook = new Workbook("Template.xlsx");

// 2️⃣ Get the worksheet where the tags reside.
Worksheet ws = workbook.Worksheets[0];

// 3️⃣ Prepare the data source that supplies values for the markers.
var dataSource = new[]
{
    new { fieldName = "Sample comment text generated by C#." }
};

// 4️⃣ Create a SmartMarkerProcessor instance.
SmartMarkerProcessor processor = new SmartMarkerProcessor();

// 5️⃣ Process the worksheet, replacing Smart Marker tags with data from the source.
processor.Process(ws, dataSource);

// 6️⃣ Save the populated workbook.
workbook.Save("Result.xlsx");
```

### Mengapa setiap baris penting

1. **Memuat workbook** memberikan processor file konkret untuk diproses.  
2. **Memilih worksheet** memastikan processor memindai lembar yang tepat; Anda dapat menargetkan lembar apa pun dengan indeks atau nama.  
3. **Sumber data** adalah array objek anonim. Setiap nama properti (`fieldName`) harus cocok dengan nama marker di dalam `${Comment:fieldName}`.  
4. `SmartMarkerProcessor` adalah mesin yang mengurai tag dan melakukan penggantian.  
5. `Process` melakukan pekerjaan berat: ia membaca setiap tag `${...}`, mencari properti yang cocok di sumber data, dan menulis nilai ke sel.  
6. **Menyimpan workbook** menulis file yang diperbarui ke disk, siap untuk penggunaan selanjutnya.

## Menyiapkan template Excel untuk **mengisi data template Excel**

1. Buka workbook Excel baru.  
2. Di sel mana pun yang Anda inginkan konten dinamis, ketik tag Smart Marker, misalnya:

   ```
   ${Comment:fieldName}
   ```

3. Simpan file sebagai `Template.xlsx`.  

Sintaks tag mengikuti pola `${<CollectionName>:<PropertyName>}`. Dalam contoh sederhana ini kami menghilangkan nama koleksi dan mengandalkan koleksi default, yaitu sumber data yang diberikan ke `Process`.

> **Edge case:** Jika tag merujuk pada properti yang tidak ada dalam sumber data, Aspose.Cells membiarkan sel tidak berubah. Selalu pastikan bahwa nama properti cocok persis, termasuk sensitivitas huruf.

## Membuat sumber data untuk **menggunakan smart marker Aspose.Cells**

Anda dapat menyediakan koleksi enumerable apa pun—array, `List<T>`, `DataTable`, atau bahkan objek kustom. Processor mengiterasi koleksi dan mengulang baris untuk setiap item ketika marker bergaya tabel digunakan.

```csharp
// Example with a List<T>
var comments = new List<Comment>
{
    new Comment { fieldName = "First comment." },
    new Comment { fieldName = "Second comment." }
};

processor.Process(ws, comments);
```

```csharp
public class Comment
{
    public string fieldName { get; set; }
}
```

Ketika Anda menyediakan beberapa baris, Aspose.Cells secara otomatis memperluas wilayah template untuk menampung semua item, yang berguna untuk menghasilkan laporan, faktur, atau tabel berbasis data.

## Memproses worksheet menggunakan **smart marker Aspose.Cells**

Metode `Process` dapat menerima pengaturan opsional, seperti:

- `SmartMarkerOptions` untuk mengontrol cara sel kosong ditangani.
- `DataSourceOptions` untuk menentukan nama koleksi yang berbeda.

```csharp
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Preserve empty cells as blanks instead of removing them.
    PreserveEmptyCells = true
};

processor.Process(ws, dataSource, options);
```

Opsi-opsi ini memberi Anda kontrol detail atas operasi **mengisi data template Excel**, memastikan output sesuai dengan kebutuhan format Anda.

## Menyimpan hasil dan memverifikasi output

Setelah diproses, Anda dapat menyimpan workbook dalam format apa pun yang didukung oleh Aspose.Cells, seperti XLSX, CSV, atau PDF.

```csharp
workbook.Save("Result.pdf", SaveFormat.Pdf);
```

Buka `Result.xlsx` (atau `Result.pdf`) untuk memverifikasi bahwa placeholder `${Comment:fieldName}` telah diganti dengan **Sample comment text generated by C#**. Jika sel masih menampilkan tag asli, periksa kembali nama properti di sumber data.

## Kesalahan umum dan cara menghindarinya

| Masalah | Penyebab | Solusi |
|-------|-------|-----|
| Tag tidak diganti | Nama properti tidak cocok (mis., `fieldname` vs `fieldName`) | Pastikan cocok persis dengan sensitivitas huruf |
| Baris tidak diduplikasi | Sumber data hanya berisi satu objek sementara template mengharapkan tabel | Sediakan koleksi dengan beberapa item |
| Workbook crash saat menyimpan | Menggunakan versi Aspose.Cells yang usang | Upgrade ke paket NuGet terbaru |
| Format hilang | Processor menimpa gaya sel | Pertahankan gaya dengan `SmartMarkerOptions.PreserveCellFormatting = true` |

## Contoh lengkap yang berfungsi

Berikut adalah program mandiri yang dapat Anda salin, tempel, dan jalankan.

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Load the template that contains the Smart Marker tag ${Comment:fieldName}
            Workbook workbook = new Workbook("Template.xlsx");
            Worksheet ws = workbook.Worksheets[0];

            // Create a list of data objects – each object maps to the marker property.
            var data = new List<Comment>
            {
                new Comment { fieldName = "First generated comment." },
                new Comment { fieldName = "Second generated comment." },
                new Comment { fieldName = "Third generated comment." }
            };

            // Initialise the processor and run it.
            SmartMarkerProcessor processor = new SmartMarkerProcessor();
            processor.Process(ws, data);

            // Save the populated workbook.
            workbook.Save("Result.xlsx");
            Console.WriteLine("Smart marker processing complete. Check Result.xlsx.");
        }
    }

    public class Comment
    {
        public string fieldName { get; set; }
    }
}
```

**Hasil yang diharapkan:** Di `Result.xlsx`, sel yang awalnya berisi `${Comment:fieldName}` berkembang menjadi tiga baris, masing‑masing diisi dengan teks komentar yang sesuai dari daftar `data`.

## Kesimpulan

Anda kini tahu cara **membuat data smart marker**, **mengisi data template Excel**, dan **menggunakan smart marker Aspose.Cells** untuk mengotomatisasi pembuatan laporan Excel. Proses ini dapat diringkas menjadi tiga tindakan: menyisipkan tag Smart Marker, menyediakan sumber data yang cocok, dan memanggil `SmartMarkerProcessor.Process`. Dari sini Anda dapat menjelajahi skenario yang lebih maju seperti koleksi bersarang, format bersyarat, atau mengekspor ke PDF.

### Langkah selanjutnya

- Bereksperimen dengan **smart marker bergaya tabel** untuk menghasilkan tabel multi‑baris secara otomatis.  
- Menggabungkan smart marker dengan **format bersyarat** untuk menyorot baris yang memenuhi kriteria tertentu.  
- Tinjau dokumentasi Aspose.Cells tentang **opsi Smart Marker** untuk penyetelan kinerja.

Selamat coding, dan nikmati waktu yang dihemat dengan mengotomatisasi alur kerja Excel Anda!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Automate Excel Workbooks with Aspose.Cells .NET: Utilize Smart Markers for Efficient Data Processing](/cells/english/net/automation-batch-processing/automate-excel-aspose-cells-workbook-smart-markers/)
- [Master Aspose.Cells .NET Smart Markers & DataTable Integration for Efficient Data Management in Excel](/cells/english/net/import-export/aspose-cells-net-smart-markers-data-table-integration/)
- [excel data merging in C# – Complete Smart Marker Guide](/cells/english/net/smart-markers-dynamic-data/excel-data-merging-in-c-complete-smart-marker-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}