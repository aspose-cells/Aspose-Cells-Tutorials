---
category: general
date: 2026-05-23
description: Cara menggunakan penanda dengan Aspose.Cells untuk mencapai penamaan
  lembar dinamis dalam otomatisasi Excel. Pelajari smart markers, pengikatan data
  JSON, dan pembuatan lembar dalam hitungan menit.
draft: false
keywords:
- how to use markers
- dynamic sheet naming excel
- aspose.cells smart markers
language: id
og_description: Cara menggunakan penanda di Aspose.Cells untuk menghasilkan file Excel
  dengan penamaan sheet dinamis. Panduan lengkap langkah demi langkah dengan contoh
  C# lengkap.
og_title: Cara Menggunakan Penanda – Penamaan Lembar Kerja Dinamis di Excel dengan
  Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  headline: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  type: TechArticle
- description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  name: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  steps:
  - name: What Happens Under the Hood?
    text: 1. The processor reads the `Orders` array. 2. For each order it creates
      a **master sheet** (using `${Orders.MasterSheetName}`) and a **detail sheet**
      (using the `DetailSheetNewName` pattern). 3. Cell values are replaced with the
      corresponding JSON fields, so the master sheet’s first cell ends up con
  - name: What if I need more than two levels of hierarchy?
    text: You can nest markers inside the newly created detail sheets. Just place
      additional `${...}` tags in the template sheet before processing. The processor
      will cascade through each level automatically.
  - name: Can I use a DataTable instead of JSON?
    text: Absolutely. `SmartMarkerProcessor` has overloads for `DataSet`, `DataTable`,
      and even custom objects. The only change is the call to `ApplyJson` – you’d
      use `ApplyDataSet(myDataSet)` instead.
  - name: How do I control the order of sheet creation?
    text: The order follows the sequence of the source collection. If you need a custom
      sort, simply sort the JSON array (or DataTable) before passing it to the processor.
  - name: Is there a way to hide the template sheet after processing?
    text: Yes. Set `sm.Options.RemoveTemplateSheets = true;` before calling `ApplyJson`.
      The original sheet (index 0) will be removed from the final workbook.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cara Menggunakan Penanda di Aspose.Cells untuk Penamaan Lembar Dinamis di Excel
url: /id/net/smart-markers-dynamic-data/how-to-use-markers-in-aspose-cells-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan Marker di Aspose.Cells untuk Penamaan Sheet Dinamis di Excel

Pernah bertanya-tanya **bagaimana cara menggunakan marker** untuk mengubah templat Excel statis menjadi workbook master‑detail yang lengkap? Anda tidak sendirian. Banyak pengembang menemui kendala ketika mereka membutuhkan kemampuan *dynamic sheet naming excel*, terutama ketika nama sheet harus mencerminkan nilai data yang berasal dari JSON atau basis data.  

Dalam tutorial ini kami akan membahas contoh C# lengkap yang siap dijalankan yang menunjukkan **bagaimana cara menggunakan marker** dengan **Aspose.Cells** smart markers, mengikat data JSON, dan membiarkan processor membuat sheet yang namanya berubah secara dinamis. Tanpa basa‑basi, hanya kode tepat yang dapat Anda salin ke Visual Studio dan langsung melihat hasilnya.

## Apa yang Akan Anda Pelajari

- Konsep **smart markers** dan mengapa mereka sempurna untuk skenario master‑detail.  
- Cara menyisipkan tag marker dalam workbook yang nantinya akan digantikan dengan nama sheet yang sebenarnya.  
- Menyiapkan **dynamic sheet naming excel** menggunakan opsi `DetailSheetNewName`.  
- Menjalankan `SmartMarkerProcessor` dengan data JSON untuk menghasilkan beberapa sheet secara otomatis.  
- Memverifikasi output dan beberapa tip berguna untuk menghindari jebakan umum.

> **Prasyarat** – Anda memerlukan runtime .NET terbaru (≥ .NET 6 sudah cukup), pustaka Aspose.Cells untuk .NET (Anda dapat mengunduh trial gratis dari Aspose), dan pemahaman dasar tentang C#.  

---

![contoh penggunaan marker di Aspose.Cells](example.png "contoh penggunaan marker di Aspose.Cells")

## Cara Menggunakan Marker untuk Membuat Penamaan Sheet Dinamis (Langkah 1)

Hal pertama yang kita butuhkan adalah workbook kosong yang akan berfungsi sebagai templat kita. Dalam proyek nyata Anda mungkin akan memulai dari file `.xlsx` yang sudah ada yang berisi tata letak, pemformatan, dan sel placeholder. Untuk kejelasan, kami akan membuat semuanya secara programatis.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

// Step 1: Create a new workbook and get the first worksheet
Workbook wb = new Workbook();                // fresh workbook, no sheets yet
Worksheet ws = wb.Worksheets[0];             // default first sheet
```

*Mengapa ini penting*: Objek `Worksheet` adalah tempat kami menempatkan tag **smart marker** kami. Anggap tag tersebut sebagai placeholder kecil yang nanti akan digantikan oleh processor dengan nilai sebenarnya dari JSON.  

## Sisipkan Tag Smart Marker (Langkah 2)

Sekarang kami menempatkan tag marker langsung ke dalam sel. Sintaks `${...}` memberi tahu Aspose.Cells “ini adalah sebuah marker”. Dalam contoh kami kami membutuhkan dua marker: satu untuk nama sheet master dan satu lagi untuk nama sheet detail.

```csharp
// Step 2: Insert Smart Marker tags that will be replaced with sheet names
ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");   // master sheet placeholder
ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");   // detail sheet placeholder
```

> **Tip pro** – Jaga nama marker tetap singkat dan bermakna; mereka menjadi kunci yang akan Anda gunakan dalam payload JSON Anda.

## Siapkan Data JSON (Langkah 3)

Processor bekerja dengan sumber data apa pun yang dapat direpresentasikan sebagai JSON, `DataSet`, atau bahkan objek biasa. Berikut adalah string JSON minimal yang berisi koleksi master‑detail. Perhatikan bahwa setiap order memiliki baik `MasterSheetName` maupun `DetailSheetName`.

```csharp
// Step 3: Prepare the JSON data that contains the master‑detail information
string jsonOrders = @"{
    ""Orders"": [
        {
            ""OrderId"": 1,
            ""MasterSheetName"": ""Master_1"",
            ""DetailSheetName"": ""Detail_1""
        },
        {
            ""OrderId"": 2,
            ""MasterSheetName"": ""Master_2"",
            ""DetailSheetName"": ""Detail_2""
        }
    ]
}";
```

*Mengapa JSON?* JSON ringan, mudah dibaca manusia, dan bekerja dengan baik bersama API web. Anda juga dapat menarik data ini dari query SQL dan menyerialisasikannya dengan `Newtonsoft.Json`.

## Inisialisasi SmartMarkerProcessor (Langkah 4)

`SmartMarkerProcessor` adalah mesin yang memindai workbook, menemukan marker, dan melakukan binding data. Membuat instansinya hanya satu baris kode.

```csharp
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);
```

## Definisikan Penamaan Sheet Dinamis (Langkah 5)

Di sinilah **dynamic sheet naming excel** benar‑benar bersinar. Dengan mengatur `DetailSheetNewName`, kami memberi tahu processor untuk membuat sheet detail baru untuk setiap order dan menamainya berdasarkan `OrderId`. Placeholder `${OrderId}` diambil dari record saat ini selama proses.

```csharp
// Step 5: Define how new detail sheets should be named during processing
sm.Options.DetailSheetNewName = "Detail_${OrderId}";
```

> **Waspada** – Jika Anda lupa menyertakan sintaks `${}`, sheet akan secara harfiah dinamai “Detail_${OrderId}” alih‑alih “Detail_1”, “Detail_2”, dll.

## Terapkan JSON dan Hasilkan Sheet (Langkah 6)

Sekarang kami membiarkan processor melakukan pekerjaan berat. Ia akan membaca JSON, mengganti marker, dan membuat worksheet baru sesuai kebutuhan.

```csharp
// Step 6: Apply the JSON data to populate the smart markers and generate sheets
sm.ApplyJson(jsonOrders);
```

### Apa yang Terjadi di Balik Layar?

1. Processor membaca array `Orders`.  
2. Untuk setiap order, ia membuat **sheet master** (menggunakan `${Orders.MasterSheetName}`) dan **sheet detail** (menggunakan pola `DetailSheetNewName`).  
3. Nilai sel diganti dengan bidang JSON yang sesuai, sehingga sel pertama pada sheet master berisi “Master_1”, “Master_2”, dll.  

## Simpan dan Verifikasi Hasil (Opsional)

Akhirnya, tulis workbook ke disk. Buka file di Excel dan Anda akan melihat dua sheet master (`Master_1`, `Master_2`) dan dua sheet detail dengan nama dinamis (`Detail_1`, `Detail_2`).  

```csharp
// (Optional) Save the result to verify the output
wb.Save("output.xlsx");
```

**Output yang diharapkan** – Setelah membuka `output.xlsx` Anda akan melihat:

- Sheet **Master_1** dengan sel A1 = “Master_1”.  
- Sheet **Detail_1** dengan sel A1 = “Detail_1”.  
- Sheet **Master_2** dengan sel A1 = “Master_2”.  
- Sheet **Detail_2** dengan sel A1 = “Detail_2”.  

Itulah siklus lengkap **bagaimana cara menggunakan marker** untuk mencapai **dynamic sheet naming excel** dengan **Aspose.Cells smart markers**.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya membutuhkan lebih dari dua tingkat hierarki?

Anda dapat menumpuk marker di dalam sheet detail yang baru dibuat. Cukup letakkan tag `${...}` tambahan di sheet templat sebelum diproses. Processor akan menurunkan secara otomatis melalui setiap tingkat.

### Bisakah saya menggunakan DataTable alih‑alih JSON?

Tentu saja. `SmartMarkerProcessor` memiliki overload untuk `DataSet`, `DataTable`, dan bahkan objek kustom. Satu‑satunya perubahan adalah pemanggilan `ApplyJson` – Anda akan menggunakan `ApplyDataSet(myDataSet)` sebagai gantinya.

### Bagaimana saya mengontrol urutan pembuatan sheet?

Urutan mengikuti urutan koleksi sumber. Jika Anda memerlukan urutan khusus, cukup urutkan array JSON (atau DataTable) sebelum mengirimkannya ke processor.

### Apakah ada cara untuk menyembunyikan sheet templat setelah proses?

Ya. Setel `sm.Options.RemoveTemplateSheets = true;` sebelum memanggil `ApplyJson`. Sheet asli (indeks 0) akan dihapus dari workbook akhir.

---

## Contoh Kerja Lengkap (Semua Langkah Digabungkan)

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke proyek konsol C# baru. Pastikan Anda telah menambahkan referensi paket NuGet `Aspose.Cells`.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace DynamicSheetNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Step 2: Insert Smart Marker tags that will be replaced with sheet names
            ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");
            ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");

            // Step 3: Prepare the JSON data that contains the master‑detail information
            string jsonOrders = @"{
                ""Orders"": [
                    {
                        ""OrderId"": 1,
                        ""MasterSheetName"": ""Master_1"",
                        ""DetailSheetName"": ""Detail_1""
                    },
                    {
                        ""OrderId"": 2,
                        ""MasterSheetName"": ""Master_2"",
                        ""DetailSheetName"": ""Detail_2""
                    }
                ]
            }";

            // Step 4: Initialise the SmartMarkerProcessor with the workbook
            SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);

            // Step 5: Define how new detail sheets should be named during processing
            sm.Options.DetailSheetNewName = "Detail_${OrderId}";

            // (Optional) Remove the original template sheet after processing
            // sm.Options.RemoveTemplateSheets = true;

            // Step 6: Apply the JSON data to populate the smart markers and generate sheets
            sm.ApplyJson(jsonOrders);

            // Save the result
            wb.Save("output.xlsx");
            Console.WriteLine("Workbook generated successfully. Check output.xlsx.");
        }
    }
}
```

Jalankan program, buka `output.xlsx`, dan Anda akan melihat sheet dinamis persis seperti yang dijelaskan sebelumnya.

---

## Kesimpulan

Kami baru saja membahas **bagaimana cara menggunakan marker** di Aspose.Cells untuk mengubah workbook biasa menjadi solusi master‑detail dengan **dynamic sheet naming excel**. Poin pentingnya adalah:

1. Letakkan smart marker `${...}` di tempat Anda ingin data muncul.  
2. Berikan JSON (atau sumber data lain yang didukung) ke `SmartMarkerProcessor`.  
3. Gunakan `DetailSheetNewName` agar processor menamai sheet baru secara dinamis.  

Dari sini Anda dapat menjelajahi skenario yang lebih maju—menambahkan tabel, menata sel, atau bahkan menyisipkan diagram—semuanya didorong

## Tutorial Terkait

- [Cara Menerapkan Aspose.Cells Smart Markers di C# untuk Pelaporan Excel Dinamis](/cells/english/net/automation-batch-processing/implement-aspose-cells-smart-markers-with-csharp/)
- [Hasilkan Laporan Excel Dinamis Menggunakan Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Menguasai Aspose.Cells .NET: Menerapkan Smart Markers dan Label Kustom untuk Laporan Excel Dinamis](/cells/english/net/advanced-features/aspose-cells-net-smart-markers-custom-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}