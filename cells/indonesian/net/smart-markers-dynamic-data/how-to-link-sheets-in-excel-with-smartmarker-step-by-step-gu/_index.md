---
category: general
date: 2026-06-08
description: Cara menghubungkan lembar kerja di Excel menggunakan SmartMarkerProcessor
  untuk laporan master‑detail. Isi lembar master dan hasilkan laporan Excel master‑detail
  dengan mudah.
draft: false
keywords:
- how to link sheets
- populate master sheet
- create master detail excel
- generate master detail report
language: id
og_description: Cara menghubungkan lembar kerja di Excel menggunakan SmartMarkerProcessor.
  Pelajari cara mengisi lembar master dan menghasilkan laporan master‑detail dalam
  hitungan menit.
og_title: Cara Menautkan Sheet di Excel dengan SmartMarker – Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  headline: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  type: TechArticle
- description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  name: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  steps:
  - name: Multiple Detail Rows per Master
    text: If a master row has several related details, SmartMarker repeats the master
      row once and then writes *all* matching detail rows beneath it. No extra code
      is needed—just ensure your `Details` collection contains every row.
  - name: Missing Details
    text: When a master entry has no matching detail rows, the detail sheet simply
      skips that section. If you need a placeholder (e.g., “No items”), you can add
      a calculated column in the template that uses an Excel formula like `=IF(COUNTA(A2:B2)=0,"No
      items","")`.
  - name: Large Datasets
    text: 'Processing tens of thousands of rows can be memory‑intensive. To keep performance
      snappy:'
  - name: Custom Column Mapping
    text: If your property names don’t line up (`MasterKey` vs `Id`), you can use
      the `SmartMarkerProcessor.Map` method to create an alias before processing.
  type: HowTo
tags:
- Excel
- SmartMarker
- C#
- master‑detail
title: Cara Menautkan Sheet di Excel dengan SmartMarker – Panduan Langkah demi Langkah
url: /id/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menautkan Sheet di Excel dengan SmartMarker – Panduan Langkah‑per‑Langkah

Pernah bertanya-tanya **bagaimana cara menautkan sheet** di Excel tanpa menyalin baris secara manual atau menulis loop VBA yang tak berujung? Anda tidak sendirian. Kebanyakan pengembang menemui kendala ketika mereka membutuhkan laporan master‑detail yang bersih dan tetap sinkron saat data berubah. Kabar baiknya? SmartMarkerProcessor melakukan pekerjaan berat untuk Anda, mengubah beberapa baris C# menjadi workbook master‑detail yang lengkap.

Dalam tutorial ini kami akan membahas langkah‑langkah tepat untuk **mengisi sheet master**, menyiapkan sheet detail, dan akhirnya **menghasilkan laporan master‑detail** yang memperbarui secara otomatis. Pada akhir tutorial Anda akan memiliki pola yang dapat digunakan kembali dan dapat dimasukkan ke proyek .NET mana pun.

> **Catatan prasyarat:** Anda memerlukan GrapeCity Documents for Excel (GcExcel) versi 2024 atau lebih baru, lingkungan pengembangan .NET (Visual Studio 2022 sangat cocok), dan pemahaman dasar C#. Tidak diperlukan paket NuGet tambahan selain GcExcel.

---

## Ikhtisar Solusi

Sebelum menyelam ke kode, mari kita uraikan apa arti “menautkan sheet” dalam konteks SmartMarker:

1. **Master sheet** – Menampung satu baris per entitas (misalnya, daftar pelanggan).
2. **Detail sheet** – Berisi baris yang terkait dengan baris master (misalnya, pesanan untuk setiap pelanggan).
3. **SmartMarker syntax** – Bahasa markup kecil (`{MasterSheet}#master;{DetailSheet}#detail`) yang memberi tahu processor cara mengikat dua tabel data.
4. **Processor options** – Mengaktifkan `MasterDetail` membuat mesin secara otomatis mengulangi baris master dan menyisipkan baris detail terkait di bawahnya.

Memahami bagian‑bagian ini membantu Anda menyesuaikan pendekatan nanti—mungkin Anda membutuhkan nesting tiga tingkat atau pemformatan bersyarat. Simpan model mental ini saat kita melangkah melalui implementasinya.

## Langkah 1: Siapkan Data Hierarkis untuk Pemrosesan Master‑Detail

Hal pertama yang Anda butuhkan adalah sumber data yang mencerminkan hubungan master‑detail. Dalam kebanyakan skenario dunia nyata ini berasal dari basis data, tetapi demi kejelasan kami akan menggunakan literal objek anonim.

```csharp
// Step 1: Prepare hierarchical data for master‑detail processing
var sampleData = new
{
    // Master collection – one row per category
    Master = new[]
    {
        new { Id = 1, Name = "A" },
        new { Id = 2, Name = "B" }
    },

    // Detail collection – rows reference MasterId
    Details = new[]
    {
        new { MasterId = 1, Item = "Item1" },
        new { MasterId = 2, Item = "Item2" }
    }
};
```

**Mengapa ini penting:** SmartMarker tidak secara ajaib menebak hubungan; ia mencari nama properti yang cocok (`MasterId` → `Id`). Dengan menyusun data seperti ini kami memberikan processor peta yang jelas, yang merupakan dasar dari **bagaimana cara menautkan sheet** secara efektif.

> **Pro tip:** Jika data Anda berada dalam objek `DataTable`, cukup expose mereka sebagai properti dengan nama yang sama—SmartMarker bekerja dengan koleksi enumerable apa pun.

## Langkah 2: Buat Workbook dan Muat Template

SmartMarker bekerja pada workbook Excel yang sudah ada, biasanya sebuah template yang sudah berisi nama sheet dan penanda placeholder. Mari kita buat workbook di memori dan tambahkan dua lembar kerja kosong bernama *MasterSheet* dan *DetailSheet*.

```csharp
using GrapeCity.Documents.Excel;

// Step 2: Create a workbook and add template sheets
IWorkbook wb = new Workbook();

// Create the master sheet and add a header row
IWorksheet masterSheet = wb.Worksheets.Add("MasterSheet");
masterSheet.Range["A1"].Value = "ID";
masterSheet.Range["B1"].Value = "Name";

// Create the detail sheet and add its header
IWorksheet detailSheet = wb.Worksheets.Add("DetailSheet");
detailSheet.Range["A1"].Value = "Master ID";
detailSheet.Range["B1"].Value = "Item";
```

Anda juga dapat memuat file `.xlsx` dari disk (`wb.Open("Template.xlsx")`) jika lebih suka merancang tata letak di Excel terlebih dahulu. Bagian pentingnya adalah nama sheet harus cocok dengan yang akan Anda referensikan dalam string SmartMarker.

## Langkah 3: Instansiasi SmartMarkerProcessor dan Aktifkan Mode Master‑Detail

Sekarang kita membawa engine yang akan membaca penanda dan menempelkan data. `SmartMarkerProcessor` menerima workbook sebagai argumen konstruktor, dan flag `Options.MasterDetail` memberi tahu untuk memperlakukan penanda `#master` dan `#detail` sebagai pasangan yang terhubung.

```csharp
// Step 3: Create a SmartMarkerProcessor for the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

// Enable master‑detail mode on the processor options
processor.Options.MasterDetail = true;
```

**Mengapa mengaktifkan `MasterDetail`?** Tanpa flag ini, processor akan memperlakukan `{MasterSheet}#master` dan `{DetailSheet}#detail` sebagai operasi independen, kehilangan hubungan penting antar baris. Menetapkan flag ini adalah satu baris kode yang membuat **bagaimana cara menautkan sheet** benar‑benar berfungsi.

## Langkah 4: Definisikan String SmartMarker dan Jalankan Processor

String penanda memberi tahu SmartMarker sheet mana yang menjadi master dan mana yang menjadi detail. Sintaksnya sederhana: `{SheetName}#master;{SheetName}#detail`. Anda juga dapat menambahkan penanda tambahan (misalnya `#header`) tetapi tidak diperlukan untuk laporan dasar.

```csharp
// Step 4: Execute the smart‑marker processing, linking master and detail sheets
string marker = "{MasterSheet}#master;{DetailSheet}#detail";
processor.Process(marker, sampleData);
```

Saat `Process` dijalankan, engine:

1. Menulis setiap baris master ke *MasterSheet* mulai dari baris kosong pertama setelah header.
2. Untuk setiap baris master, ia memindai koleksi `Details`, memilih baris di mana `MasterId` cocok dengan `Id` master, dan menuliskannya ke *DetailSheet* tepat di bawah entri master yang bersangkutan.

## Langkah 5: Simpan atau Ekspor Workbook yang Dihasilkan

Pada titik ini Anda memiliki workbook yang sepenuhnya terisi. Anda dapat menyimpannya ke disk, men-stream kembali ke klien web, atau bahkan mengonversinya ke PDF.

```csharp
// Save the workbook to a file (you could also stream it to a response)
wb.Save("MasterDetailReport.xlsx");
```

Buka file tersebut dan Anda akan melihat dua sheet: *MasterSheet* menampilkan `A` dan `B`, sementara *DetailSheet* menunjukkan `Item1` di bawah master `1` dan `Item2` di bawah master `2`. Itulah esensi dari **mengisi sheet master** dan **menghasilkan laporan master‑detail** dalam satu langkah.

## Ikhtisar Visual

![Diagram illustrating how to link sheets in Excel using SmartMarkerProcessor](https://example.com/diagram.png "How to link sheets diagram")

Diagram (teks alt mencakup kata kunci utama) menunjukkan alur data dari objek C# → SmartMarkerProcessor → sheet Excel yang terhubung.

## Menangani Kasus Tepi Umum

### Beberapa Baris Detail per Master

Jika satu baris master memiliki beberapa detail terkait, SmartMarker mengulangi baris master sekali lalu menulis *semua* baris detail yang cocok di bawahnya. Tidak diperlukan kode tambahan—pastikan saja koleksi `Details` Anda berisi setiap baris.

### Detail yang Hilang

Ketika entri master tidak memiliki baris detail yang cocok, sheet detail cukup melewatkan bagian tersebut. Jika Anda memerlukan placeholder (misalnya, “No items”), Anda dapat menambahkan kolom terhitung di template yang menggunakan rumus Excel seperti `=IF(COUNTA(A2:B2)=0,"No items","")`.

### Dataset Besar

Memproses puluhan ribu baris dapat memakan banyak memori. Agar performa tetap cepat:

- Gunakan `processor.Options.EnableStreaming = true` (tersedia di GcExcel 2025+).
- Bagi data menjadi potongan‑potongan dan proses tiap potongan secara terpisah, lalu gabungkan workbook.

### Pemetaan Kolom Kustom

Jika nama properti Anda tidak cocok (`MasterKey` vs `Id`), Anda dapat menggunakan metode `SmartMarkerProcessor.Map` untuk membuat alias sebelum pemrosesan.

```csharp
processor.Map("MasterId", "Id"); // tells the engine that MasterId maps to Id
```

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang siap disalin‑tempel dan dapat dijalankan segera.

```csharp
using System;
using GrapeCity.Documents.Excel;

namespace MasterDetailDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare hierarchical data
            var sampleData = new
            {
                Master = new[]
                {
                    new { Id = 1, Name = "A" },
                    new { Id = 2, Name = "B" }
                },
                Details = new[]
                {
                    new { MasterId = 1, Item = "Item1" },
                    new { MasterId = 1, Item = "Item1‑Extra" },
                    new { MasterId = 2, Item = "Item2" }
                }
            };

            // 2️⃣ Create workbook and template sheets
            IWorkbook wb = new Workbook();

            var master = wb.Worksheets.Add("MasterSheet");
            master.Range["A1"].Value


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Menguasai Rumus Tautan Eksternal di Excel Menggunakan Aspose.Cells untuk Java](/cells/english/java/formulas-functions/aspose-cells-java-external-link-formulas-excel/)
- [Menguasai Sheet Excel Dinamis di Java dengan Aspose.Cells: Panduan Komprehensif](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Menguasai Laporan Excel Dinamis Menggunakan Aspose.Cells Java: Named Ranges & Rumus Kompleks](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}