---
category: general
date: 2026-08-07
description: Buat Excel dari JSON menggunakan Aspose.Cells Smart Marker – pelajari
  cara mengisi template Excel, menerapkan penamaan sheet dinamis, dan menghasilkan
  beberapa lembar kerja.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- populate excel template
- dynamic sheet naming
- generate multiple worksheets
- aspose.cells smart marker
language: id
lastmod: 2026-08-07
og_description: Buat Excel dari JSON dengan Aspose.Cells Smart Marker untuk dengan
  cepat mengisi templat, gunakan penamaan lembar dinamis, dan menghasilkan beberapa
  lembar kerja.
og_image_alt: Screenshot of generated Excel workbook with multiple dynamically named
  sheets
og_title: Buat Excel dari JSON – Panduan Smart Marker Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  headline: Create Excel from JSON with Aspose.Cells Smart Marker
  type: TechArticle
- description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  name: Create Excel from JSON with Aspose.Cells Smart Marker
  steps:
  - name: Define the JSON‑compatible source data
    text: '```csharp // Step 1: Define the source data that will be merged into the
      workbook var ordersData = new { Orders = new[] { new { Id = 1, Items = new[]
      { "Apple", "Banana" } }, new { Id = 2, Items = new[] { "Orange" } } } }; ```'
  - name: Prepare the workbook template and insert a Smart Marker
    text: '```csharp // Step 2: Create a new workbook and place a Smart Marker that
      references the data collection var workbook = new Workbook(); // creates an
      empty workbook workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}"); ```'
  - name: Configure dynamic sheet naming
    text: '```csharp // Step 3: Configure how duplicated detail sheets should be named
      during processing var smartMarkerOptions = new SmartMarkerOptions { // {0} will
      be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …) DetailSheetNewName
      = "DetailSheet_{0}" }; ```'
  - name: Process the template with the data and naming options
    text: '```csharp // Step 4: Process the workbook with the data and the naming
      options var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
      smartMarkerProcessor.Process(ordersData); ```'
  - name: Save the resulting workbook
    text: '```csharp // Step 5: Save the resulting workbook – the detail sheets are
      created automatically workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
      ```'
  - name: Populate Excel template with additional fields
    text: 'If your JSON includes more properties (e.g., `CustomerName`, `TotalAmount`),
      add corresponding markers to the template:'
  - name: Generate multiple worksheets from nested collections
    text: 'You can create a second level of duplication by placing a marker inside
      the detail sheet that references a nested collection, such as `Items`:'
  - name: Custom naming with data from the record
    text: '```csharp var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName
      = "Order_{Id}" }; ```'
  - name: Next steps
    text: '* Explore **conditional formatting** inside the detail sheet to highlight
      high‑value orders. * Replace the anonymous object with a strongly typed model
      deserialized via `System.Text.Json`. * Combine Smart Markers with **PivotTable**
      generation for advanced reporting.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Buat Excel dari JSON dengan Aspose.Cells Smart Marker
url: /id/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Excel dari JSON dengan Aspose.Cells Smart Marker

Jika Anda perlu **membuat Excel dari JSON**, tutorial ini menunjukkan solusi lengkap yang siap produksi. Anda akan melihat cara **mengisi template Excel**, mengonfigurasi **penamaan sheet dinamis**, dan **menghasilkan beberapa worksheet** secara otomatis dengan mesin **Aspose.Cells Smart Marker**.

Panduan ini membawa Anda melalui setiap langkah yang diperlukan, mulai dari mendefinisikan objek sumber bergaya JSON hingga menyimpan workbook akhir. Tidak diperlukan skrip eksternal, dan kode berjalan pada .NET 6 atau yang lebih baru.

## Apa yang akan Anda capai

* Muat objek data bergaya JSON ke dalam memori.  
* Sisipkan placeholder Smart Marker ke dalam template workbook.  
* Terapkan pola penamaan sehingga setiap sheet detail yang digandakan menerima nama unik.  
* Proses template untuk membuat worksheet terpisah untuk setiap order dalam koleksi.  
* Simpan hasil sebagai file `.xlsx` yang siap untuk konsumsi selanjutnya.

Prasyarat: Visual Studio 2022 (atau IDE C# apa pun), .NET 6+, dan paket NuGet **Aspose.Cells**. Contoh ini menggunakan C#; konsep yang sama berlaku untuk VB.NET atau bahasa .NET lainnya.

## Membuat Excel dari JSON – alur kerja keseluruhan

Bagian-bagian berikut membagi alur kerja menjadi lima langkah logis. Setiap langkah mencakup kode tepat yang Anda perlukan, penjelasan mengapa hal itu penting, dan tip untuk memperluas solusi.

### Langkah 1: Definisikan data sumber yang kompatibel dengan JSON

```csharp
// Step 1: Define the source data that will be merged into the workbook
var ordersData = new
{
    Orders = new[]
    {
        new { Id = 1, Items = new[] { "Apple", "Banana" } },
        new { Id = 2, Items = new[] { "Orange" } }
    }
};
```

**Why this matters** – Objek `ordersData` mencerminkan struktur yang akan Anda terima dari API JSON nyata. Aspose.Cells Smart Marker membaca properti publik, sehingga tipe anonim berfungsi selama nama properti cocok dengan tag marker (`{{Orders}}`). Ketika Anda kemudian mengganti tipe anonim dengan objek JSON yang telah dideserialisasi, tidak diperlukan perubahan kode.

### Langkah 2: Siapkan template workbook dan sisipkan Smart Marker

```csharp
// Step 2: Create a new workbook and place a Smart Marker that references the data collection
var workbook = new Workbook();                     // creates an empty workbook
workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");
```

**Why this matters** – Marker `{{Orders}}` memberi tahu processor untuk mengiterasi koleksi `Orders`. Menempatkan marker di sel `A1` pada sheet pertama menjadikan sheet tersebut sebagai sheet *master*. Processor akan menggandakan sheet ini untuk setiap order, mempertahankan semua format yang Anda tambahkan nanti.

> **Tip:** Jika Anda memiliki template yang sudah dirancang sebelumnya (mis., dengan header, formula, atau styling), muat dengan `new Workbook("Template.xlsx")` alih-alih membuat workbook kosong.

### Langkah 3: Konfigurasikan penamaan sheet dinamis

```csharp
// Step 3: Configure how duplicated detail sheets should be named during processing
var smartMarkerOptions = new SmartMarkerOptions
{
    // {0} will be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …)
    DetailSheetNewName = "DetailSheet_{0}"
};
```

**Why this matters** – Secara default Aspose.Cells menamai sheet yang digandakan `Sheet1`, `Sheet2`, dll. Pola `DetailSheetNewName` menyisipkan indeks inkremental (`{0}`) sehingga setiap sheet menerima nama yang bermakna. Anda dapat menyematkan placeholder tambahan (mis., `{Id}`) untuk menyertakan data dari record saat ini.

> **Pro tip:** Gunakan `DetailSheetNewName = "Order_{Id}"` untuk menamai sheet berdasarkan identifier order, yang memudahkan navigasi dalam workbook besar.

### Langkah 4: Proses template dengan data dan opsi penamaan

```csharp
// Step 4: Process the workbook with the data and the naming options
var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
smartMarkerProcessor.Process(ordersData);
```

**Why this matters** – `SmartMarkerProcessor` menggabungkan `ordersData` ke dalam workbook, membuat sheet baru untuk setiap elemen dalam `Orders`, dan menerapkan pola penamaan yang telah didefinisikan sebelumnya. Processor juga memperluas koleksi bersarang apa pun (mis., `Items`) jika Anda menambahkan marker tambahan di dalam sheet detail.

### Langkah 5: Simpan workbook yang dihasilkan

```csharp
// Step 5: Save the resulting workbook – the detail sheets are created automatically
workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
```

**Why this matters** – Metode `Save` menulis workbook yang sepenuhnya terisi ke disk. File kini berisi sheet master (yang dapat disembunyikan atau dihapus) dan serangkaian sheet detail bernama `DetailSheet_1`, `DetailSheet_2`, …, masing‑masing menyimpan data untuk satu order.

#### Output yang Diharapkan

| Nama sheet        | Konten (disederhanakan)                     |
|-------------------|------------------------------------------|
| DetailSheet_1     | Order Id = 1, Items: Apple, Banana       |
| DetailSheet_2     | Order Id = 2, Items: Orange              |

Semua sheet mempertahankan format apa pun yang Anda terapkan pada sheet master sebelum diproses.

## Variasi lanjutan

### Isi template Excel dengan bidang tambahan

Jika JSON Anda mencakup lebih banyak properti (mis., `CustomerName`, `TotalAmount`), tambahkan marker yang sesuai ke template:

```csharp
workbook.Worksheets[0].Cells["B1"].PutValue("{{CustomerName}}");
workbook.Worksheets[0].Cells["C1"].PutValue("{{TotalAmount}}");
```

Processor akan menggantikan setiap marker dengan nilai properti yang cocok.

### Hasilkan beberapa worksheet dari koleksi bersarang

Anda dapat membuat tingkat duplikasi kedua dengan menempatkan marker di dalam sheet detail yang merujuk pada koleksi bersarang, seperti `Items`:

```csharp
// Inside the detail sheet (e.g., cell A2)
workbook.Worksheets[0].Cells["A2"].PutValue("{{Items}}");

// Inside the same sheet, cell B2 will list each item
workbook.Worksheets[0].Cells["B2"].PutValue("{{Items}}");
```

Selama pemrosesan, Aspose.Cells membuat baris untuk setiap item dalam array `Items`, memungkinkan Anda menghasilkan daftar terperinci per order.

### Penamaan khusus dengan data dari record

```csharp
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheetNewName = "Order_{Id}"
};
```

Sekarang sheet dinamai `Order_1`, `Order_2`, yang menyelaraskan nama sheet dengan identifier bisnis.

## Kesalahan umum dan cara menghindarinya

| Jebakan                              | Solusi |
|--------------------------------------|----------|
| Teks marker tidak cocok dengan nama properti (case‑sensitive) | Pastikan marker (`{{Orders}}`) cocok dengan properti secara tepat, termasuk huruf besar/kecil. |
| Template berisi sel yang digabung yang melintasi wilayah marker | Lepaskan penggabungan sel atau tempatkan marker di sel tunggal yang tidak digabung untuk mencegah perubahan tata letak yang tidak terduga. |
| Koleksi JSON besar menyebabkan tekanan memori | Proses data dalam batch atau alirkan JSON ke dalam `DataTable` dan gunakan `SmartMarkerProcessor` dengan `DataSource`. |
| Path file yang disimpan tidak valid | Gunakan `Path.Combine(Environment.CurrentDirectory, "output.xlsx")` atau verifikasi izin menulis. |

## Contoh lengkap yang berfungsi

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // 1️⃣ Define JSON‑compatible data
        var ordersData = new
        {
            Orders = new[]
            {
                new { Id = 1, Items = new[] { "Apple", "Banana" } },
                new { Id = 2, Items = new[] { "Orange" } }
            }
        };

        // 2️⃣ Create workbook and add master Smart Marker
        var workbook = new Workbook();
        workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");

        // 3️⃣ Set up dynamic sheet naming
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "DetailSheet_{0}"
        };

        // 4️⃣ Process template with data
        var processor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
        processor.Process(ordersData);

        // 5️⃣ Save the result
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "SmartMarkerDupSheets.xlsx");
        workbook.Save(outputPath);
    }
}
```

Menjalankan program menghasilkan file Excel di desktop yang berisi dua sheet detail (`DetailSheet_1` dan `DetailSheet_2`). Setiap sheet mencerminkan record order yang bersangkutan.

## Kesimpulan

Anda kini tahu cara **membuat Excel dari JSON** menggunakan **Aspose.Cells Smart Marker**, cara **mengisi template Excel**, menerapkan **penamaan sheet dinamis**, dan **menghasilkan beberapa worksheet** secara otomatis. Pola yang sama dapat diskalakan ke puluhan atau ribuan record, mendukung koleksi bersarang, dan terintegrasi mulus dengan pustaka deserialisasi JSON .NET apa pun.

### Langkah selanjutnya

* Jelajahi **conditional formatting** di dalam sheet detail untuk menyoroti order bernilai tinggi.  
* Ganti objek anonim dengan model bertipe kuat yang dideserialisasi melalui `System.Text.Json`.  
* Gabungkan Smart Markers dengan pembuatan **PivotTable** untuk pelaporan lanjutan.  

Bereksperimenlah dengan pola penamaan, tambahkan lebih banyak marker, dan integrasikan alur kerja ini ke dalam pipeline ekspor data Anda yang sudah ada. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun pada teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Hasilkan Laporan Excel Dinamis Menggunakan Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Isi Excel dengan Data Menggunakan Aspose.Cells dan Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [Cara Membuat dan Menggabungkan Workbook Excel Menggunakan Aspose.Cells untuk Java | Panduan Lengkap](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}