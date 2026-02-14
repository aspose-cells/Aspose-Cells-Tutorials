---
category: general
date: 2026-02-14
description: Buat objek data master di C# dan hasilkan lembar detail dengan mudah.
  Pelajari alur kerja SmartMarker secara lengkap dengan contoh kode praktis.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: id
og_description: Buat objek data master dalam C# dan hasilkan lembar detail dengan
  SmartMarker. Ikuti tutorial terperinci kami untuk solusi siap pakai.
og_title: Buat Objek Data Master – Panduan Lengkap
tags:
- C#
- SmartMarker
- Excel Automation
title: Buat Objek Data Master – Panduan Langkah-demi-Langkah untuk Menghasilkan Lembar
  Detail
url: /id/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

needed.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Objek Data Master – Tutorial Lengkap

Pernah perlu **membuat objek data master** untuk lembar kerja Excel tetapi tidak yakin bagaimana menghubungkannya ke lembar detail SmartMarker? Anda tidak sendirian. Dalam banyak skenario pelaporan, objek master menggerakkan lembar detail yang dinamis, dan mengatur sambungannya dapat terasa seperti menyusun puzzle tanpa gambar.  

Dalam panduan ini kami akan melangkah melalui seluruh proses—membangun objek data master, mengonfigurasi opsi SmartMarker untuk **menghasilkan lembar detail**, dan akhirnya menjalankan processor. Pada akhir panduan Anda akan memiliki potongan kode yang dapat dijalankan dan dapat ditempelkan ke proyek .NET apa pun yang menggunakan pustaka GrapeCity Documents for Excel (GcExcel).

## Apa yang Anda Butuhkan

- .NET 6+ (atau .NET Framework 4.7.2) dengan referensi ke `GcExcel.dll`
- Pemahaman dasar C# (variabel, tipe anonim, inisialisasi objek)
- Workbook Excel yang sudah berisi tag SmartMarker seperti `{{OrderId}}` dan tabel untuk item baris
- Visual Studio, Rider, atau editor apa pun yang Anda sukai

Itu saja—tidak ada paket NuGet tambahan selain distribusi inti GcExcel.

## Langkah 1: Buat Objek Data Master

Hal pertama yang harus Anda lakukan adalah **membuat objek data master** yang mencerminkan struktur yang diharapkan oleh tag SmartMarker. Anggaplah ini sebagai model laporan kecil dalam memori.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

Mengapa menggunakan tipe anonim di sini? Karena memungkinkan Anda mendefinisikan kontainer ringan tanpa mendeklarasikan kelas lengkap—sempurna untuk demo cepat atau ketika bentuknya tidak mungkin berubah. Jika Anda membutuhkan model yang dapat digunakan kembali nanti, cukup ganti `var` dengan POCO yang tepat.

> **Tip profesional:** Jaga nama properti (`OrderId`, `Product`, `Quantity`) tetap identik dengan placeholder di lembar kerja Anda; SmartMarker mencocokkannya tanpa memperhatikan huruf besar/kecil.

## Langkah 2: Konfigurasikan Opsi SmartMarker untuk Menghasilkan Lembar Detail

Sekarang kami memberi tahu SmartMarker bahwa kami menginginkan lembar kerja terpisah untuk tabel item baris. Di sinilah kata kunci **generate detail sheet** berperan.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

Polanya `DetailSheetNewName` menggunakan placeholder dalam kurung kurawal yang digantikan pada saat runtime. Dalam contoh kami, lembar akan disebut `Order_1`. Jika Anda kemudian melakukan iterasi pada beberapa pesanan, masing‑masing akan mendapatkan tabnya sendiri—tepat seperti yang diharapkan kebanyakan akuntan.

## Langkah 3: Jalankan Processor SmartMarker

Dengan data dan opsi siap, langkah terakhir adalah memanggil processor pada lembar kerja target.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

Di balik layar, SmartMarker memindai lembar kerja untuk tag, menyuntikkan nilai `orderData`, dan karena `DetailSheet` bernilai `true`, ia menggandakan templat ke lembar baru bernama `Order_1`. Semua item baris muncul di area detail, mempertahankan format apa pun yang Anda terapkan pada templat.

### Contoh Kerja Lengkap

Di bawah ini adalah program konsol mandiri yang membuka workbook templat (`Template.xlsx`), menjalankan tiga langkah, dan menyimpan hasilnya sebagai `Result.xlsx`. Anda dapat menyalin‑tempel ini ke proyek konsol baru dan menekan **F5**.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Output yang Diharapkan

- **Result.xlsx** berisi lembar yang disebut `Order_1`.
- Sel `A1` (atau di mana pun Anda menempatkan `{{OrderId}}`) kini menampilkan `1`.
- Sebuah tabel yang dimulai pada blok SmartMarker menampilkan dua baris:
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

Jika Anda membuka file, Anda akan melihat format dari templat tetap terjaga—batas, font, pemformatan bersyarat—semua tetap utuh.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya memiliki beberapa pesanan?

Bungkus objek master dalam koleksi dan biarkan SmartMarker mengiterasi secara otomatis:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

Setiap pesanan menghasilkan lembarnya sendiri (`Order_1`, `Order_2`, …). Processor memperlakukan array luar sebagai koleksi master.

### Bagaimana saya mengontrol posisi lembar?

Setel `smartMarkerOptions.DetailSheetInsertIndex = 2;` untuk menempatkan lembar baru setelah tab kedua, atau gunakan `DetailSheetInsertAfter = "Summary"` untuk menyisipkan setelah lembar bernama.

### Bisakah saya menonaktifkan lembar detail untuk satu run tertentu?

Cukup ubah `DetailSheet = false;`. SmartMarker kemudian akan menulis item baris ke lembar yang sama tempat tag master berada.

### Bagaimana dengan kumpulan data besar?

SmartMarker men‑stream data secara efisien, tetapi jika Anda melebihi beberapa ratus ribu baris, Anda mungkin mencapai batas 1.048.576 baris Excel. Dalam kasus itu, bagi data menjadi beberapa record master atau pertimbangkan mengekspor ke CSV.

## Ikhtisar Visual

![Diagram yang menggambarkan cara membuat objek data master dan menghasilkan lembar detail menggunakan SmartMarker](/images/smartmarker-flow.png)

*Ilustrasi menunjukkan alur dari objek master C# → opsi SmartMarker → pemrosesan lembar kerja → lembar detail baru.*

## Kesimpulan

Anda sekarang tahu cara **membuat objek data master** dalam C# dan mengonfigurasi SmartMarker untuk **menghasilkan lembar detail** secara otomatis. Pola tiga langkah—data, opsi, processor—mencakup mayoritas skenario otomatisasi Excel dengan GcExcel.  

Dari sini Anda dapat menjelajahi:

- Menambahkan data header/footer ke setiap lembar detail
- Menggunakan pemformatan bersyarat berdasarkan status pesanan
- Mengekspor workbook yang dihasilkan ke PDF dengan `workbook.SaveAsPdf(...)`

Silakan bereksperimen, memecahkan sesuatu, dan kemudian menyatukannya kembali. Itu cara tercepat untuk menguasai otomatisasi lembar kerja. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}