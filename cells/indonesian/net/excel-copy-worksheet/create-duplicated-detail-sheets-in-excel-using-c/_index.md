---
category: general
date: 2026-10-07
description: Buat lembar detail duplikat di Excel menggunakan C#. Pelajari cara menghasilkan
  beberapa lembar kerja dan membangun laporan dari tabel dalam satu kali proses.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: id
lastmod: 2026-10-07
og_description: Buat lembar detail duplikat di Excel dengan C#. Tutorial ini menunjukkan
  cara menghasilkan beberapa lembar kerja dan membuat laporan Excel lengkap dari tabel.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: Buat lembar detail duplikat di Excel – panduan C# langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  headline: Create duplicated detail sheets in Excel using C#
  type: TechArticle
- description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  name: Create duplicated detail sheets in Excel using C#
  steps:
  - name: '**Obtain the data source** that contains a master table and two detail
      tables.'
    text: '**Obtain the data source** that contains a master table and two detail
      tables.'
  - name: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
    text: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
  - name: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
    text: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
  - name: '**Run the processor** to generate the master sheet and all detail sheets.'
    text: '**Run the processor** to generate the master sheet and all detail sheets.'
  - name: '**Save the workbook** – each detail sheet now has a distinct name.'
    text: '**Save the workbook** – each detail sheet now has a distinct name.'
  type: HowTo
tags:
- C#
- Excel automation
- Aspose.Cells
title: Buat lembar detail duplikat di Excel menggunakan C#
url: /id/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat lembar detail duplikat di Excel menggunakan C#

Jika Anda perlu **membuat lembar detail duplikat** dalam sebuah workbook Excel, panduan ini akan membawa Anda melalui seluruh proses. Anda akan melihat cara **menghasilkan beberapa worksheet** dari kumpulan data master‑detail dan menghasilkan laporan Excel yang rapi langsung dari tabel.

Menghasilkan laporan Excel dari tabel adalah kebutuhan umum untuk sistem penagihan, dasbor inventaris, atau skenario apa pun di mana satu catatan master memiliki beberapa baris detail terkait. Pada akhir tutorial ini Anda akan memiliki program C# yang dapat dijalankan yang membuat workbook dengan lembar master dan lembar yang diberi nama unik untuk setiap grup detail.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* .NET 6.0 (atau lebih baru) terpasang  
* Visual Studio 2022 atau IDE yang kompatibel dengan C#  
* Paket NuGet **Aspose.Cells for .NET** (menyediakan `SmartMarkerProcessor`)  

Anda dapat menambahkan paket dengan perintah berikut:

```bash
dotnet add package Aspose.Cells
```

## Gambaran umum solusi

Solusi ini mengikuti lima langkah berikut:

1. **Mendapatkan sumber data** yang berisi tabel master dan dua tabel detail.  
2. **Mengonfigurasi processor Smart‑marker** sehingga setiap lembar detail duplikat menerima nama yang unik.  
3. **Membuat workbook baru** dan menempatkan smart‑marker yang merujuk ke tabel master.  
4. **Menjalankan processor** untuk menghasilkan lembar master dan semua lembar detail.  
5. **Menyimpan workbook** – setiap lembar detail kini memiliki nama yang berbeda.

Setiap langkah dijelaskan secara rinci di bawah ini, lengkap dengan kode dan penjelasan.

## Langkah 1: Dapatkan sumber data yang berisi tabel master dan dua tabel detail

Tugas pertama adalah membangun sebuah `DataSet` yang meniru data yang biasanya Anda ambil dari basis data. `DataSet` harus berisi tabel bernama **Master** dan satu atau lebih tabel bernama **Detail**. Mesin Smart‑marker menggunakan nama tabel ini untuk mengisi workbook.

```csharp
using System.Data;

/// <summary>
/// Returns a DataSet with a master table and two detail tables.
/// In a real application you would fill these tables from a database.
/// </summary>
static DataSet GetReportDataSet()
{
    var ds = new DataSet();

    // Master table – one row per invoice
    var master = new DataTable("Master");
    master.Columns.Add("InvoiceId", typeof(int));
    master.Columns.Add("CustomerName", typeof(string));
    master.Columns.Add("InvoiceDate", typeof(DateTime));
    master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
    master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
    ds.Tables.Add(master);

    // Detail table – multiple rows per invoice
    var detail = new DataTable("Detail");
    detail.Columns.Add("InvoiceId", typeof(int));
    detail.Columns.Add("Product", typeof(string));
    detail.Columns.Add("Quantity", typeof(int));
    detail.Columns.Add("Price", typeof(decimal));

    // Detail rows for Invoice 101
    detail.Rows.Add(101, "Widget A", 5, 9.99m);
    detail.Rows.Add(101, "Widget B", 2, 19.95m);

    // Detail rows for Invoice 102
    detail.Rows.Add(102, "Gadget X", 1, 99.00m);
    detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
    ds.Tables.Add(detail);

    return ds;
}
```

**Mengapa ini penting:**  
*Smart‑marker* bekerja dengan objek `DataSet`; setiap nama tabel menjadi marker yang dapat digantikan oleh mesin. Dengan menstrukturkan data seperti ini Anda memungkinkan processor secara otomatis menduplikasi lembar detail untuk setiap `InvoiceId` yang berbeda.

## Langkah 2: Konfigurasikan processor Smart‑marker untuk memberi setiap lembar detail duplikat nama yang unik

Ketika processor menemukan marker detail, ia membuat worksheet baru untuk setiap grup baris. Secara default, lembar baru memiliki nama yang sama, yang menyebabkan konflik penamaan. Menetapkan `DetailSheetNewName` memberi tahu mesin cara menamai ulang setiap salinan.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

/// <summary>
/// Configures the SmartMarkerProcessor to rename duplicated detail sheets.
/// The placeholder {0} is replaced with a sequential number (1, 2, …).
/// </summary>
static SmartMarkerProcessor ConfigureProcessor()
{
    var processor = new SmartMarkerProcessor();

    // The pattern "Detail_{0}" becomes Detail_1, Detail_2, …
    processor.Options.DetailSheetNewName = "Detail_{0}";

    // Optional: keep the original sheet as a template (if you have one)
    processor.Options.KeepTemplateSheet = false;

    return processor;
}
```

**Mengapa ini penting:**  
Tanpa pola penamaan yang unik, workbook akan melempar pengecualian ketika processor mencoba menambahkan lembar detail kedua. Placeholder `{0}` memastikan setiap lembar menerima nama yang berbeda dan dapat diprediksi.

## Langkah 3: Buat workbook baru dan tempatkan smart‑marker yang merujuk ke tabel master

Sekarang Anda membuat `Workbook` baru, menambahkan marker yang menunjuk ke tabel **Master**, dan secara opsional memformat baris header.

```csharp
/// <summary>
/// Creates a workbook with a single cell that contains the master smart‑marker.
/// </summary>
static Workbook CreateTemplateWorkbook()
{
    var workbook = new Workbook();
    var sheet = workbook.Worksheets[0];

    // Put the master smart‑marker in cell A1.
    // The double braces {{ }} tell SmartMarker to replace the content with the Master table.
    sheet.Cells["A1"].PutValue("{{Master}}");

    // Optional: add a header row for visual clarity.
    sheet.Cells["A2"].PutValue("Invoice ID");
    sheet.Cells["B2"].PutValue("Customer");
    sheet.Cells["C2"].PutValue("Date");
    sheet.Cells["A2:C2"].Style.Font.IsBold = true;

    return workbook;
}
```

**Mengapa ini penting:**  
Marker `{{Master}}` memberi instruksi kepada processor untuk memperluas tabel master mulai dari `A1`. Baris‑baris berikutnya menjadi baris data untuk setiap catatan master. Ini adalah titik masuk untuk **generate excel report from tables**.

## Langkah 4: Jalankan processor smart‑marker untuk menghasilkan lembar master dan lembar detail

Dengan sumber data, processor, dan templat siap, Anda memanggil `Process`. Mesin memperluas marker master, kemudian membuat lembar detail terpisah untuk setiap `InvoiceId` yang unik.

```csharp
static void GenerateReport()
{
    // 1️⃣ Obtain data
    DataSet reportData = GetReportDataSet();

    // 2️⃣ Configure processor
    SmartMarkerProcessor processor = ConfigureProcessor();

    // 3️⃣ Create template workbook
    Workbook workbook = CreateTemplateWorkbook();

    // 4️⃣ Process the smart‑markers – this creates the master sheet and duplicated detail sheets
    processor.Process(workbook, reportData);

    // 5️⃣ Save the file
    string outputPath = Path.Combine(
        Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
        "DuplicatedDetailSheets.xlsx");
    workbook.Save(outputPath);

    Console.WriteLine($"Report generated successfully: {outputPath}");
}
```

**Mengapa ini penting:**  
`processor.Process` melakukan pekerjaan berat: membaca baris master, membuat lembar detail untuk setiap kunci unik, dan menamai ulang lembar‑lembar tersebut sesuai pola yang telah ditentukan sebelumnya. Hasilnya adalah workbook yang memenuhi kebutuhan **how to generate multiple worksheets**.

## Langkah 5: Simpan workbook yang dihasilkan – setiap lembar detail kini memiliki nama yang berbeda

Pemanggilan `Save` menulis file ke disk. Saat Anda membuka workbook, Anda akan melihat:

* **Sheet1** – lembar master yang berisi header faktur.  
* **Detail_1**, **Detail_2**, … – setiap lembar berisi baris dari tabel **Detail** yang terkait dengan faktur tertentu.

Berikut adalah contoh tampilan layout workbook yang diharapkan (gambar bersifat ilustratif; Anda dapat menggantinya dengan screenshot nyata jika diinginkan).

![Screenshot of an Excel file that has create duplicated detail sheets output](https://example.com/images/duplicated-detail-sheets.png)

### Output yang diharapkan

| Nama Lembar | Deskripsi Konten |
|------------|------------------|
| **Sheet1** | Baris Master: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | Baris Detail dimana `InvoiceId = 101` |
| **Detail_2** | Baris Detail dimana `InvoiceId = 102` |

Membuka `DuplicatedDetailSheets.xlsx` harus menampilkan struktur persis seperti ini.

## Kode sumber lengkap (siap disalin)



## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menamai Lembar Secara Otomatis – Generate Multiple Sheets in C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [Cara Membuat Worksheet – Panduan Langkah‑per‑Langkah untuk Generasi Excel Dinamis](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [Cara Menghasilkan Laporan Excel di C# – Panduan Lengkap Menggunakan SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}