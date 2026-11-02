---
category: general
date: 2026-06-05
description: Aktifkan opsi rentang bersarang pada Aspose.Cells SmartMarkerProcessor
  untuk menangani data Excel hierarkis dengan mudah. Pelajari smart marker, rentang
  bersarang, dan praktik terbaik.
draft: false
keywords:
- enable nested range option
- SmartMarkerProcessor
- nested range handling
- Excel smart markers
- Aspose.Cells
language: id
og_description: Aktifkan opsi rentang bersarang di Aspose.Cells SmartMarkerProcessor
  untuk bekerja dengan data hierarkis. Panduan lengkap dengan kode, tips, dan jebakan.
og_title: Aktifkan Opsi Rentang Bersarang di Aspose.Cells SmartMarker
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Enable nested range option in Aspose.Cells SmartMarkerProcessor to
    handle hierarchical Excel data effortlessly. Learn smart markers, nested ranges,
    and best practices.
  headline: Enable Nested Range Option in Aspose.Cells SmartMarker
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Smart Markers
title: Aktifkan Opsi Rentang Bersarang di Aspose.Cells SmartMarker
url: /id/net/smart-markers-dynamic-data/enable-nested-range-option-in-aspose-cells-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aktifkan Opsi Nested Range di Aspose.Cells SmartMarker

Pernah bertanya-tanya bagaimana **mengaktifkan opsi nested range** di Aspose.Cells SmartMarkerProcessor? Mengaktifkan fitur ini memungkinkan Anda bekerja dengan data hierarkis seperti pesanan dan item baris tanpa hambatan.  

Dalam tutorial ini kami akan membahas skenario dunia nyata: mengisi daftar pesanan dengan item bersarang ke dalam templat Excel menggunakan smart markers. Pada akhir tutorial Anda akan memiliki workbook yang berfungsi penuh, memahami **SmartMarkerProcessor**, dan mengetahui mengapa flag **nested range handling** penting.

Kami akan membahas:

* Menyiapkan objek anonim C# yang meniru data master‑detail.  
* Mengaktifkan flag **nested range** pada processor.  
* Menjalankan processor terhadap workbook dan memverifikasi hasilnya.  

Tidak memerlukan kerangka kerja khusus—hanya .NET 6+ dan pustaka Aspose.Cells untuk .NET. Jika Anda pernah mengalami kesulitan dengan baris berulang di dalam baris berulang, panduan ini untuk Anda.

---

## Siapkan Data Hierarkis untuk Excel Smart Markers

Pertama, kita memerlukan sumber data yang mencerminkan hubungan orang‑tua‑anak. Contoh di bawah ini membuat objek anonim dengan satu pesanan yang berisi dua item.

```csharp
// Step 1: Define hierarchical data with orders and their items
var orderData = new
{
    Orders = new[]
    {
        new
        {
            Id = 1,
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        }
    }
};
```

**Mengapa bentuk ini?**  
Smart markers membaca nama properti (`Orders`, `Items`) dan secara otomatis menghasilkan nested range ketika processor dikonfigurasi dengan benar. Anggap saja ini sebagai mini‑database yang akan di‑iterasi oleh templat Excel.

> **Pro tip:** Gunakan nama properti yang bermakna dan cocok dengan marker yang Anda letakkan di templat (misalnya `&=Orders.Id&`, `&=Items.Name&`). Nama yang tidak cocok adalah penyebab umum kesalahan “no data”.

---

## Konfigurasi SmartMarkerProcessor dan Aktifkan Nested Range

Sekarang kita buat processor dan mengaktifkan saklar **NestedRange**. Satu baris ini memberi tahu Aspose.Cells untuk memperlakukan koleksi anak sebagai tabel dalam.

```csharp
// Step 2: Create a SmartMarkerProcessor and enable nested range handling
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.Options.NestedRange = true;   // <‑‑ enable nested range option
```

**Apa yang sebenarnya dilakukan `NestedRange = true`?**  
Ketika diaktifkan, processor membuat range terpisah untuk setiap koleksi anak dan menempatkannya di dalam range orang‑tua. Tanpa flag ini, hanya koleksi tingkat atas (`Orders`) yang akan dirender, dan baris `Items` di dalamnya akan diabaikan.

> **Waspada:** Jika Anda mengaktifkan nested range tetapi lupa menandai range anak di templat (menggunakan `&=Items.Start&` / `&=Items.End&`), processor akan melempar `SmartMarkerException`. Selalu periksa kembali sintaks marker Anda.

---

## Muat atau Buat Templat Workbook

Untuk demo kami akan menghasilkan workbook sederhana secara dinamis, tetapi dalam produksi Anda biasanya memulai dari file `.xlsx` yang sudah ada dan berisi smart markers.

```csharp
// Step 3: Create a workbook with a simple template
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Header row
ws.Cells["A1"].PutValue("Order ID");
ws.Cells["B1"].PutValue("Item Name");

// Smart marker row for Orders (parent)
//   &amp;=Orders.Start&amp; and &amp;=Orders.End&amp; define the range for each order.
ws.Cells["A2"].PutValue("&=Orders.Start&");
ws.Cells["A2"].PutValue("&=Orders.Id&");
ws.Cells["B2"].PutValue("&=Orders.End&");

// Smart marker row for Items (child)
//   Nested inside the Orders range.
ws.Cells["A3"].PutValue("&=Items.Start&");
ws.Cells["A3"].PutValue("&=Items.Name&");
ws.Cells["B3"].PutValue("&=Items.End&");
```

Perhatikan marker `&=Orders.Start&` / `&=Orders.End&`—marker ini memberi tahu processor di mana setiap blok pesanan dimulai dan berakhir. Pola yang sama berlaku untuk range anak `Items`.

---

## Proses Workbook dengan Smart Markers

Dengan data dan processor siap, langkah terakhir adalah satu baris kode yang menggabungkan semuanya.

```csharp
// Step 4: Apply the data to the workbook using smart markers
processor.Process(wb, orderData);
```

Setelah pemanggilan ini, workbook akan berisi:

| Order ID | Item Name |
|----------|-----------|
| 1        | A         |
| 1        | B         |

Anda dapat menyimpan hasilnya ke disk atau mengirimnya kembali ke klien:

```csharp
wb.Save("NestedRangeResult.xlsx");
```

---

## Verifikasi Output dan Tangani Kendala Umum

### Hasil yang Diharapkan

Buka `NestedRangeResult.xlsx` dan Anda akan melihat dua baris di bawah header pesanan tunggal, masing‑masing menampilkan nama item (`A` dan `B`). ID pesanan diulang untuk setiap baris anak—tepat seperti yang dirancang oleh nested range.

### Masalah Umum

| Gejala | Penyebab Kemungkinan | Solusi |
|--------|----------------------|--------|
| Tidak ada baris anak yang muncul | `NestedRange` tetap `false` | Setel `processor.Options.NestedRange = true`. |
| Marker muncul sebagai teks biasa | Typo sintaks marker (`&=Orders.Start&` vs `&=Orders.Start`) | Pastikan kedua `&=` dan `&` penutup ada. |
| Baris duplikat untuk setiap pesanan | Marker penutup `&=Orders.End&` hilang | Tambahkan marker penutup untuk membatasi range orang‑tua. |

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Define hierarchical data
        var orderData = new
        {
            Orders = new[]
            {
                new
                {
                    Id = 1,
                    Items = new[]
                    {
                        new { Name = "A" },
                        new { Name = "B" }
                    }
                }
            }
        };

        // 2️⃣ Create processor and enable nested range option
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Options.NestedRange = true;   // enable nested range option

        // 3️⃣ Build a simple workbook template with smart markers
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("Order ID");
        ws.Cells["B1"].PutValue("Item Name");

        // Parent range markers
        ws.Cells["A2"].PutValue("&=Orders.Start&");
        ws.Cells["A2"].PutValue("&=Orders.Id&");
        ws.Cells["B2"].PutValue("&=Orders.End&");

        // Child range markers (nested)
        ws.Cells["A3"].PutValue("&=Items.Start&");
        ws.Cells["A3"].PutValue("&=Items.Name&");
        ws.Cells["B3"].PutValue("&=Items.End&");

        // 4️⃣ Process the workbook
        processor.Process(wb, orderData);

        // 5️⃣ Save the result
        wb.Save("NestedRangeResult.xlsx");
        Console.WriteLine("Workbook generated – check NestedRangeResult.xlsx");
    }
}
```

Jalankan program, buka file yang dihasilkan, dan Anda akan melihat baris bersarang terisi persis seperti yang ditunjukkan pada tabel di atas.

---

## Kesimpulan

Anda baru saja mempelajari cara **mengaktifkan opsi nested range** di Aspose.Cells SmartMarkerProcessor, mengubah templat Excel datar menjadi generator laporan master‑detail yang kuat. Dengan mengatur `processor.Options.NestedRange = true`, pustaka secara otomatis membuat tabel dalam untuk koleksi anak, menghemat Anda dari penulisan loop penyisipan baris manual.

Apa selanjutnya? Coba tambahkan tingkat nesting kedua (misalnya, pesanan → item → sub‑komponen), bereksperimen dengan styling baris yang dihasilkan, atau beralih ke templat yang sudah dirancang dengan grafik dan formula. Kombinasi **Excel smart markers** dan **nested range handling** merupakan fondasi solid untuk solusi pelaporan otomatis apa pun.

Punya pertanyaan atau skenario rumit? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Handle Nested Objects with Smart Markers Aspose.Cells](/cells/english/net/smart-markers-dynamic-data/nested-objects-smart-markers/)
- [Populate Excel with Nested Data Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)
- [Populate Excel Nested Data Aspose Cells Java](/cells/german/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}