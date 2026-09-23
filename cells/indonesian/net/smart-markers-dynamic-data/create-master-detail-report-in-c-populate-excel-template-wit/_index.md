---
category: general
date: 2026-02-28
description: Buat laporan master‑detail dalam C# dan pelajari cara mengisi templat
  Excel, menggabungkan data ke dalam Excel, serta memuat workbook Excel dengan C#
  dalam beberapa langkah saja.
draft: false
keywords:
- create master detail report
- populate excel template
- merge data into excel
- load excel workbook c#
- how to create master detail
language: id
og_description: Buat laporan master‑detail di C# menggunakan Aspose.Cells SmartMarker.
  Pelajari cara memuat workbook Excel di C#, menggabungkan data ke dalam Excel, dan
  mengisi template Excel.
og_title: Buat laporan master‑detail di C# – Isi templat Excel
tags:
- C#
- Aspose.Cells
- Excel automation
- SmartMarker
title: Buat laporan master-detail di C# – Isi templat Excel dengan SmartMarker
url: /id/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat laporan master detail di C# – Isi templat Excel dengan SmartMarker

Pernah perlu **create master detail report** di C# tetapi tidak yakin bagaimana cara memasukkan data ke dalam file Excel? Anda tidak sendirian. Dalam panduan ini kami akan menjelaskan langkah‑langkah tepat untuk **populate Excel template**, **merge data into Excel**, dan **load Excel workbook C#**‑style sehingga Anda mendapatkan laporan master‑detail yang rapi siap didistribusikan.

Kami akan menggunakan Aspose.Cells SmartMarker, sebuah mesin kuat yang memahami hubungan master‑detail secara otomatis. Pada akhir tutorial Anda akan memiliki contoh lengkap yang dapat dijalankan yang dapat Anda masukkan ke proyek .NET mana pun. Tidak ada jalan pintas “lihat dokumen” yang samar—hanya solusi mandiri yang dapat Anda salin‑tempel dan jalankan.

## Apa yang akan Anda pelajari

- Cara **create master detail** struktur data di C# yang langsung dipetakan ke templat Excel.
- Cara tepat untuk **load Excel workbook C#** kode yang membuka file `.xlsx` yang berisi tag SmartMarker.
- Proses **populate Excel template** dengan menjalankan `SmartMarkerProcessor`.
- Tips menangani kasus tepi, seperti tag yang hilang atau kumpulan data besar.
- Cara memverifikasi hasil dan seperti apa **master detail report** akhir.

### Prasyarat

- .NET 6.0 atau lebih baru (kode juga berfungsi pada .NET Framework 4.8).
- Aspose.Cells untuk .NET (Anda dapat mengunduh paket percobaan gratis NuGet: `Install-Package Aspose.Cells`).
- File Excel dasar (`template.xlsx`) yang berisi tag SmartMarker (kami akan menunjukkan markup minimal yang Anda perlukan).

Jika Anda sudah menyiapkannya, mari kita mulai.

## Langkah 1 – Buat sumber data master‑detail *(cara membuat master detail)*

Hal pertama yang Anda perlukan adalah objek C# yang mewakili baris master (orders) dan baris anaknya (order items). SmartMarker akan membaca hierarki ini secara otomatis ketika `MasterDetail` diatur ke `true`.

```csharp
using System;

// Step 1: Build the master‑detail data object
var orderData = new
{
    // Master collection – each order is a row in the master table
    Orders = new[]
    {
        new
        {
            Id = 1,
            // Detail collection – items belonging to order 1
            Items = new[] { new { Sku = 101, Qty = 2 }, new { Sku = 102, Qty = 1 } }
        },
        new
        {
            Id = 2,
            Items = new[] { new { Sku = 202, Qty = 1 } }
        }
    }
};
```

**Mengapa ini penting:**  
SmartMarker mencari properti bernama `Orders` (master) dan kemudian untuk setiap order mencari koleksi bernama `Items`. Dengan mencocokkan nama-nama tersebut Anda secara otomatis mendapatkan **master‑detail report** tanpa menulis loop apa pun.

> **Pro tip:** Jaga nama properti tetap singkat dan bermakna; mereka menjadi placeholder di templat Excel Anda.

## Langkah 2 – Konfigurasikan opsi SmartMarker untuk pemrosesan master‑detail

Beritahu mesin bahwa Anda sedang menangani skenario master‑detail dan berikan nama sheet detail yang akan menerima baris anak.

```csharp
using Aspose.Cells;

// Step 2: Set up SmartMarker options
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Enables master‑detail processing
    MasterDetail = true,
    // The sheet in the template that holds the detail rows
    DetailSheetName = "OrderDetail"
};
```

**Mengapa ini penting:**  
Jika Anda menghilangkan `MasterDetail = true`, SmartMarker akan memperlakukan data sebagai daftar datar dan baris detail tidak akan pernah muncul. `DetailSheetName` harus cocok dengan nama sheet yang Anda buat di templat (case‑sensitive).

## Langkah 3 – Muat workbook Excel dengan gaya C#

Sekarang kita membuka templat yang berisi tag SmartMarker. Ini adalah langkah **load Excel workbook C#** yang banyak pengembang tersandung karena lupa menggunakan jalur file yang benar atau membuang workbook dengan tepat.

```csharp
using System.IO;

// Step 3: Load the workbook that holds the SmartMarker tags
string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
Workbook workbook = new Workbook(templatePath);
```

**Mengapa ini penting:**  
Aspose.Cells membaca seluruh workbook ke dalam memori, sehingga file dapat berada di disk, disematkan sebagai sumber daya, atau bahkan di‑stream dari layanan web. Pastikan jalur mengarah ke file `.xlsx` yang valid yang berisi tag yang akan kami bahas selanjutnya.

## Langkah 4 – Sisipkan tag SmartMarker ke dalam templat (populate Excel template)

Jika Anda membuka `template.xlsx` sekarang, Anda akan melihat dua sheet:

- **Orders** – sheet master dengan baris seperti `&=Orders.Id`.
- **OrderDetail** – sheet detail dengan baris seperti `&=Items.Sku` dan `&=Items.Qty`.

Berikut tampilan minimal markup:

| Sheet | Cell A1 | Cell B1 |
|-------|---------|---------|
| Orders | `&=Orders.Id` | *(empty)* |
| OrderDetail | `&=Items.Sku` | `&=Items.Qty` |

Anda tidak perlu menulis kode apa pun untuk tag—mereka berada di file Excel. Langkah **populate Excel template** hanyalah memanggil processor:

```csharp
// Step 4: Run SmartMarker to merge data into Excel
new SmartMarkerProcessor().Process(workbook, orderData, options);
```

**Mengapa ini penting:**  
Processor memindai setiap sheet, mengganti placeholder `&=` dengan nilai sebenarnya, dan memperluas baris untuk setiap record master dan detail. Karena `MasterDetail` diaktifkan, secara otomatis dibuat baris baru untuk setiap item di bawah order yang sesuai.

## Langkah 5 – Simpan laporan master detail

Akhirnya, tulis workbook yang telah diisi ke disk. Ini adalah momen Anda mendapatkan **master detail report** yang siap dibagikan.

```csharp
// Step 5: Save the populated workbook
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);

// Optional: open the file automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Output yang diharapkan:**  

- Sheet **Orders** menampilkan dua baris: `1` dan `2` (ID order).  
- Sheet **OrderDetail** menampilkan tiga baris:  
  - SKU 101 Qty 2  
  - SKU 102 Qty 1  
  - SKU 202 Qty 1  

Itu adalah **create master detail report** yang berfungsi penuh yang dapat Anda email, cetak, atau masukkan ke sistem lain.

## Kasus tepi & pertanyaan umum

### Bagaimana jika templat tidak memiliki tag?

SmartMarker secara diam-diam mengabaikan tag yang tidak dikenal, tetapi Anda akan mendapatkan sel kosong. Periksa kembali ejaan tag dan pastikan nama properti di objek C# Anda cocok persis.

### Bagaimana cara menangani kumpulan data besar?

Processor melakukan streaming baris, sehingga bahkan ribuan record detail tidak akan membebani memori. Namun, untuk file yang sangat besar Anda mungkin ingin meningkatkan `MemorySetting` di `LoadOptions`.

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeWorkbook = new Workbook(templatePath, loadOptions);
```

### Bisakah saya menggunakan nama sheet berbeda untuk master?

Ya—cukup ganti nama sheet di templat dan sesuaikan `DetailSheetName` jika Anda memiliki sheet detail. Nama sheet master diambil dari placeholder (`&=Orders.Id`).

### Bagaimana jika saya perlu menambahkan baris total?

Tambahkan formula Excel biasa di templat (misalnya, `=SUM(B2:B{#})`). SmartMarker akan mempertahankan formula setelah penyisipan data.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke aplikasi console. Ini mencakup semua direktif `using`, model data, opsi, dan penanganan file.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace MasterDetailReportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Create master‑detail data ----------
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Sku = 101, Qty = 2 },
                            new { Sku = 102, Qty = 1 }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Sku = 202, Qty = 1 }
                        }
                    }
                }
            };

            // ---------- Step 2: SmartMarker options ----------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                MasterDetail = true,
                DetailSheetName = "OrderDetail"
            };

            // ---------- Step 3: Load the template ----------
            string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
            Workbook workbook = new Workbook(templatePath);

            // ---------- Step 4: Process the template ----------
            new SmartMarkerProcessor().Process(workbook, orderData, options);

            // ---------- Step 5: Save the result ----------
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Master detail report generated at: {outputPath}");
        }
    }
}
```

Jalankan program, buka `output.xlsx`, dan Anda akan melihat data master‑detail terisi dengan indah.

## Referensi visual

![Tangkapan layar output laporan master detail](https://example.com/images/master-detail-report.png "Contoh laporan master detail")

*Gambar ini menunjukkan sheet Orders dengan ID 1 dan 2, serta sheet OrderDetail dengan tiga baris SKU‑Qty.*

## Kesimpulan

Anda sekarang tahu **how to create master detail report** di C# menggunakan Aspose.Cells SmartMarker, mulai dari membangun sumber data hingga **loading Excel workbook C#**, **populating Excel template**, dan akhirnya

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}