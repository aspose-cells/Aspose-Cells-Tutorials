---
category: general
date: 2026-05-30
description: Isi templat Excel dengan cepat dan pelajari cara mengisi Excel dengan
  data menggunakan Aspose.Cells SmartMarker. Panduan lengkap C# dengan kode yang dapat
  dijalankan.
draft: false
keywords:
- populate excel template
- fill excel with data
- Aspose.Cells SmartMarker
- automate Excel reporting
- C# Excel automation
language: id
og_description: Isi templat Excel dan mengisi Excel dengan data menggunakan Aspose.Cells
  SmartMarker. Ikuti tutorial C# langkah demi langkah ini untuk hasil instan.
og_title: Isi Template Excel – Isi Data Excel melalui SmartMarker
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  headline: Populate Excel Template – Fill Excel Data via SmartMarker
  type: TechArticle
- description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  name: Populate Excel Template – Fill Excel Data via SmartMarker
  steps:
  - name: Empty Collections
    text: 'If `Items` is empty, SmartMarker will leave the table header intact but
      won’t insert any rows. To avoid a blank space, you can add a conditional block:'
  - name: Custom Number Formats
    text: 'Sometimes you need currency symbols or thousands separators. After processing,
      you can apply a style programmatically:'
  - name: Large Data Sets
    text: 'For thousands of rows, enable the `UseFastMode` option to improve performance:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Isi Template Excel – Isi Data Excel melalui SmartMarker
url: /id/net/smart-markers-dynamic-data/populate-excel-template-fill-excel-data-via-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Isi Template Excel – Mengisi Data Excel melalui SmartMarker

Pernahkah Anda perlu **populate Excel template** tetapi tidak yakin bagaimana mengotomatiskan prosesnya? Dalam tutorial ini kami akan menunjukkan cara **fill Excel with data** menggunakan Aspose.Cells SmartMarker—sebuah alat yang mengubah workbook statis menjadi generator laporan dinamis.

Bayangkan Anda memiliki lembar faktur yang telah dirancang sebelumnya, dasbor penjualan, atau formulir berulang apa pun. Alih-alih mengetik nilai secara manual, Anda dapat memberikan objek C# dan biarkan SmartMarker melakukan pekerjaan berat. Pada akhir panduan ini Anda akan memiliki proyek yang dapat dijalankan sepenuhnya yang mengambil template, menyisipkan baris, total, dan bahkan pemformatan bersyarat—semua tanpa menyentuh UI.

## Apa yang Akan Anda Pelajari

- Cara menyiapkan sumber data yang cocok dengan penanda di template Excel Anda.  
- Cara menginstansiasi **SmartMarkerProcessor** dan mengaktifkan dukungan rentang.  
- Cara **populate Excel template** dengan koleksi bersarang, seperti item pesanan.  
- Tips untuk menangani kasus tepi seperti koleksi kosong atau format angka khusus.  

Tidak ada layanan eksternal, tidak ada makro VBA—hanya C# murni dan Aspose.Cells. Semua yang Anda butuhkan adalah .NET 6 (atau lebih baru) dan paket NuGet Aspose.Cells.

## Prasyarat

- Visual Studio 2022 (atau IDE apa pun yang Anda sukai).  
- .NET 6 SDK terpasang.  
- Aspose.Cells untuk .NET (Anda dapat mengambil versi percobaan gratis dari situs web Aspose).  
- Template Excel dasar dengan tag SmartMarker (kami akan membuatnya sebentar lagi).  

Jika ada yang terdengar tidak familiar, jangan panik; langkah-langkah di bawah ini akan memandu Anda melalui setiap persyaratan.

## Langkah 1: Rancang Template Excel dengan Tag SmartMarker

Pertama, buka workbook baru dan susun bagian statis—logo perusahaan, header, dll. Kemudian sisipkan placeholder SmartMarker di mana data dinamis harus muncul.

| Sel | Konten |
|------|---------|
| A1   | **Invoice** |
| A3   | `{{CompanyName}}` |
| A5   | **Order Details** |
| A7   | `{{Orders.Items.Name}}` |
| B7   | `{{Orders.Items.Qty}}` |
| C7   | `{{Orders.Items.Price}}` |
| D7   | `{{Orders.Items.Price * Orders.Items.Qty}}` |

**Mengapa ini penting:** SmartMarker membaca tanda kurung kurawal ganda dan memetakan mereka ke properti pada objek yang Anda berikan nanti. Koleksi `Orders.Items` memberi tahu engine untuk mengulang baris untuk setiap item dalam daftar.

> **Pro tip:** Gunakan opsi `RangeSmartMarker` (kami akan mengaktifkannya nanti) ketika Anda membutuhkan engine untuk memperluas rentang secara otomatis—sempurna untuk tabel yang bertambah atau menyusut.

Simpan file sebagai `InvoiceTemplate.xlsx` di folder `Resources` proyek Anda.

## Langkah 2: Siapkan Sumber Data yang Sesuai dengan Penanda Template

Sekarang kami membuat objek anonim C# (atau kelas yang kuat) yang nama propertinya cocok dengan penanda. Kuncinya adalah mencerminkan hierarki secara tepat.

```csharp
// Step 2: Prepare the data source that matches the template markers
var data = new
{
    CompanyName = "Acme Corp.",
    Orders = new[]
    {
        new
        {
            Items = new[]
            {
                new { Name = "Pen",   Qty = 2, Price = 1.5m },
                new { Name = "Notebook", Qty = 1, Price = 3.75m },
                new { Name = "Stapler",  Qty = 1, Price = 5.0m }
            }
        }
    }
};
```

**Mengapa ini penting:** Array `Orders` berisi satu pesanan, dan setiap pesanan memiliki array `Items`. SmartMarker akan mengiterasi `Items`, menggandakan baris untuk setiap elemen. Jika Anda kemudian membutuhkan beberapa pesanan, cukup tambahkan lebih banyak objek ke array `Orders`—tidak diperlukan perubahan kode.

## Langkah 3: Muat Template dan Buat Instance SmartMarkerProcessor

Dengan data siap, kami memuat workbook, membuat processor, dan memberi tahu untuk menghormati penanda rentang.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook
Workbook workbook = new Workbook("Resources/InvoiceTemplate.xlsx");

// Get the first worksheet (where our markers live)
Worksheet ws = workbook.Worksheets[0];

// Step 3: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

**Mengapa ini penting:** `SmartMarkerProcessor` adalah engine yang mem-parsing penanda, memperluas rentang, dan menulis nilai. Dengan memisahkan processor dari workbook, Anda menjaga kode tetap bersih dan dapat digunakan kembali.

## Langkah 4: Proses Worksheet dengan RangeSmartMarker Diaktifkan

Keajaiban terjadi ketika kami memanggil `Process`. Menetapkan `RangeSmartMarker = true` memberi tahu SmartMarker untuk memperlakukan seluruh rentang baris sebagai blok yang dapat diulang, secara otomatis menyisipkan atau menghapus baris sesuai kebutuhan.

```csharp
// Step 4: Process the worksheet using SmartMarker with range support enabled
processor.Process(ws, data, new SmartMarkerOptions { RangeSmartMarker = true });
```

Pada titik ini engine telah:

1. Memindai worksheet untuk tag `{{...}}`.  
2. Memetakan setiap tag ke properti pada `data`.  
3. Mendeteksi rentang tabel (A7:D7) dan menduplikasinya tiga kali—sekali per item.  
4. Menghitung ekspresi `Price * Qty` untuk kolom total.

## Langkah 5: Simpan Workbook Hasil

Akhirnya, tulis workbook yang telah diisi ke disk (atau alirkan kembali ke klien web).

```csharp
// Step 5: Save the populated workbook
workbook.Save("Output/InvoicePopulated.xlsx");
```

Buka `InvoicePopulated.xlsx` dan Anda akan melihat tabel yang terisi rapi:

| Nama      | Jumlah | Harga | Total |
|-----------|--------|-------|-------|
| Pen       | 2      | 1.5   | 3.00 |
| Notebook  | 1      | 3.75  | 3.75 |
| Stapler   | 1      | 5.00  | 5.00 |

Langkah **populate Excel template** kini selesai, dan Anda telah berhasil **filled Excel with data** untuk sejumlah baris apa pun.

## Menangani Kasus Tepi Umum

### Koleksi Kosong

Jika `Items` kosong, SmartMarker akan membiarkan header tabel tetap tetapi tidak menyisipkan baris apa pun. Untuk menghindari ruang kosong, Anda dapat menambahkan blok kondisional:

```csharp
{{#if Orders.Items.Length > 0}}
    ... table rows ...
{{else}}
    No items were ordered.
{{/if}}
```

### Format Angka Kustom

Kadang-kadang Anda memerlukan simbol mata uang atau pemisah ribuan. Setelah pemrosesan, Anda dapat menerapkan gaya secara programatik:

```csharp
Style style = workbook.CreateStyle();
style.Number = 164; // Built‑in currency format
StyleFlag flag = new StyleFlag { NumberFormat = true };

foreach (Cell cell in ws.Cells["C8:D12"])
{
    cell.SetStyle(style, flag);
}
```

### Set Data Besar

Untuk ribuan baris, aktifkan opsi `UseFastMode` untuk meningkatkan kinerja:

```csharp
processor.Process(ws, data, new SmartMarkerOptions { 
    RangeSmartMarker = true,
    UseFastMode = true
});
```

## Contoh Kerja Lengkap

Berikut adalah program lengkap yang berdiri sendiri yang dapat Anda salin‑tempel ke aplikasi konsol. Program ini mencakup semua direktif using, persiapan data, pemrosesan, dan penyimpanan.



## Apa yang Harus Anda Pelajari Selanjutnya?

- [Isi Excel dengan Data Menggunakan Aspose.Cells dan Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [Cara Mengisi Sel Excel dengan Aspose.Cells untuk .NET: Panduan Langkah demi Langkah](/cells/english/net/cell-operations/aspose-cells-dotnet-populate-excel-data/)
- [Otomatisasi Ekspor Data Excel Menggunakan Aspose.Cells untuk .NET: Panduan Langkah demi Langkah](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}