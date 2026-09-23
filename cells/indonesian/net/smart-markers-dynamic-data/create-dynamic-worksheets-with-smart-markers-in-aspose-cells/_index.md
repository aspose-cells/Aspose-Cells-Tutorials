---
category: general
date: 2026-03-25
description: Pelajari cara membuat lembar kerja dinamis menggunakan smart markers
  aspose.cells. Panduan langkah demi langkah dengan kode C# lengkap, tips, dan penanganan
  kasus tepi.
draft: false
keywords:
- create dynamic worksheets
- smart markers aspose.cells
language: id
og_description: Buat lembar kerja dinamis dengan mudah menggunakan smart markers aspose.cells.
  Ikuti tutorial lengkap ini untuk menguasai pembuatan Excel dinamis dalam C#.
og_title: Buat Lembar Kerja Dinamis – Panduan Smart Markers Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel automation
title: Buat Lembar Kerja Dinamis dengan Smart Markers di Aspose.Cells
url: /id/net/smart-markers-dynamic-data/create-dynamic-worksheets-with-smart-markers-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Worksheet Dinamis dengan Smart Markers di Aspose.Cells

Pernah bertanya-tanya bagaimana **membuat worksheet dinamis** yang secara otomatis memperluas sesuai data Anda? Mungkin Anda pernah menatap template Excel statis dan berpikir, “Harusnya ada cara yang lebih pintar.” Kabar baiknya, Anda dapat **membuat worksheet dinamis** dalam sekejap dengan memanfaatkan **smart markers aspose.cells**.  

Dalam tutorial ini kami akan membahas semua yang perlu Anda ketahui: mulai dari menyiapkan sumber data hingga mengonfigurasi processor SmartMarker, sambil memastikan kode dapat dijalankan dan penjelasannya jelas. Pada akhir tutorial Anda akan dapat menambahkan beberapa baris kode ke proyek Anda dan melihat Aspose.Cells menghasilkan lembar detail yang sempurna secara otomatis.

## Apa yang Akan Anda Pelajari

- Cara **membuat worksheet dinamis** yang bertambah atau berkurang berdasarkan `DataTable`, `List<T>`, atau sumber enumerable apa pun.  
- Mengapa **smart markers aspose.cells** adalah rahasia utama untuk pembuatan Excel berbasis template.  
- Kesalahan umum (data null, tabrakan nama) dan cara menghindarinya.  
- Kode C# tepat yang dapat Anda salin‑tempel ke Visual Studio 2022 dan jalankan langsung.  

> **Prasyarat:** Visual Studio 2022 (atau lebih baru) dengan .NET 6+, dan lisensi Aspose.Cells yang valid (atau evaluasi gratis). Tidak ada pustaka pihak ketiga lain yang diperlukan.

![Create dynamic worksheets example](image.png "Screenshot showing dynamic worksheets generated with smart markers aspose.cells")

## Langkah 1 – Siapkan Sumber Data untuk Worksheet Dinamis Anda

Hal pertama yang Anda perlukan adalah sumber data yang dapat digabungkan Aspose.Cells ke dalam template. Apa pun yang mengimplementasikan `IEnumerable` dapat digunakan, tetapi pilihan paling umum adalah `DataTable` dan `List<T>`.

```csharp
using System;
using System.Data;
using System.Collections.Generic;
using Aspose.Cells;

namespace ExcelDynamicDemo
{
    class Program
    {
        static void Main()
        {
            // Example 1: DataTable
            DataTable table = new DataTable("Orders");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Price", typeof(double));

            table.Rows.Add("Apple", 10, 0.5);
            table.Rows.Add("Banana", 5, 0.3);
            table.Rows.Add("Cherry", 20, 0.2);

            // Example 2: List<T>
            var orders = new List<Order>
            {
                new Order { Product = "Desk", Quantity = 2, Price = 150.0 },
                new Order { Product = "Chair", Quantity = 5, Price = 45.0 }
            };

            // Choose which one to feed into the processor
            object data = table; // or: object data = orders;
```

**Mengapa ini penting:**  
Jika Anda memberikan referensi `null`, processor akan melemparkan exception dan upaya Anda **membuat worksheet dinamis** akan gagal secara diam‑diam. Selalu validasi sumber Anda sebelum melanjutkan.

## Langkah 2 – Muat Worksheet Template yang Memuat Smart Markers

Selanjutnya, ambil workbook yang berisi smart markers. Biasanya Anda memulai dari file `.xlsx` yang sudah Anda desain di Excel.

```csharp
            // Load the template workbook (ensure the file exists)
            string templatePath = @"Templates\DynamicTemplate.xlsx";
            Workbook workbook = new Workbook(templatePath);

            // Assume the first worksheet contains the smart markers
            Worksheet ws = workbook.Worksheets[0];
```

**Tip:**  
Simpan template Anda di folder `Templates` dalam proyek. Ini membuat jalur tetap stabil di semua lingkungan dan membantu Anda **membuat worksheet dinamis** tanpa harus menuliskan lokasi absolut.

## Langkah 3 – Konfigurasikan SmartMarkerOptions untuk Kontrol Detail

`SmartMarkerOptions` memungkinkan Anda menyesuaikan cara Aspose.Cells memperlakukan marker. Untuk pembuatan sheet dinamis Anda ingin mengontrol pola penamaan sheet detail.

```csharp
            // Create options object
            SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();

            // Optional: turn on advanced processing if you have nested collections
            smartMarkerOptions.Advanced = true;
```

**Penjelasan:**  
Menetapkan `Advanced = true` mengaktifkan processor untuk menangani skenario kompleks seperti loop bersarang, yang sering diperlukan ketika Anda **membuat worksheet dinamis** yang memiliki hubungan master‑detail.

## Langkah 4 – Tentukan Pola Penamaan untuk Sheet Detail

Properti `DetailSheetNewName` menentukan bagaimana sheet yang baru dibuat dinamai. Aspose.Cells akan menambahkan nomor inkremental secara otomatis.

```csharp
            // Define the base name for each generated detail sheet
            smartMarkerOptions.DetailSheetNewName = "Detail"; // → Detail1, Detail2, …
```

**Pro tip:**  
Jika Anda memperkirakan banyak sheet detail, gunakan nama dasar yang deskriptif seperti `"OrderDetail"` sehingga tab yang dihasilkan menjadi mudah dipahami.

## Langkah 5 – Jalankan SmartMarker Processor untuk **Membuat Worksheet Dinamis**

Sekarang keajaiban terjadi. Processor menggabungkan data Anda ke dalam template, menghasilkan sebanyak yang diperlukan sheet.

```csharp
            // Run the processor
            ws.SmartMarkerProcessor.Process(data, smartMarkerOptions);

            // Save the result
            string outputPath = @"Output\DynamicReport.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Dynamic workbook saved to {outputPath}");
        }
    }

    // Simple POCO for List<T> example
    public class Order
    {
        public string Product { get; set; }
        public int Quantity { get; set; }
        public double Price { get; set; }
    }
}
```

**Apa yang akan Anda lihat:**  
Jika `data` berisi tiga baris, Aspose.Cells akan menghasilkan tiga worksheet baru bernama `Detail1`, `Detail2`, dan `Detail3`. Setiap sheet akan terisi dengan smart markers yang Anda letakkan di template (misalnya `&=Product`, `&=Quantity`, `&=Price`). Inilah inti cara **membuat worksheet dinamis** tanpa menulis logika loop sendiri.

## Kasus Khusus & Pertanyaan Umum

### Bagaimana jika sumber data kosong?

Jika `data` merupakan koleksi kosong, processor tetap akan membuat satu sheet detail (dengan nama `Detail1`) tetapi hanya berisi bagian statis dari template Anda. Untuk menghindari sheet yang tidak diperlukan, periksa jumlah koleksi sebelum memanggil `Process`.

```csharp
if ((data as IEnumerable<object>)?.Cast<object>().Any() == true)
{
    ws.SmartMarkerProcessor.Process(data, smartMarkerOptions);
}
else
{
    Console.WriteLine("No data to merge – skipping dynamic sheet creation.");
}
```

### Bisakah saya mengontrol urutan sheet yang dihasilkan?

Ya. Sheet dibuat sesuai urutan data muncul. Jika Anda memerlukan urutan khusus, urutkan `DataTable` atau `List<T>` Anda sebelum mengirimkannya ke processor.

### Bagaimana **smart markers aspose.cells** berbeda dari formula sel biasa?

Smart markers adalah placeholder yang digantikan oleh engine Aspose.Cells pada runtime, sedangkan formula dievaluasi oleh Excel itu sendiri. Smart markers memungkinkan Anda menyisipkan loop, kondisi, bahkan sub‑template langsung di dalam workbook—sempurna untuk **membuat worksheet dinamis**.

## Ringkasan Contoh Kerja Lengkap

Berikut adalah program lengkap yang siap disalin‑tempel dan menunjukkan seluruh alur kerja:

```csharp
using System;
using System.Data;
using System.Collections.Generic;
using Aspose.Cells;

namespace ExcelDynamicDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Prepare data ----------
            DataTable table = new DataTable("Orders");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Price", typeof(double));
            table.Rows.Add("Apple", 10, 0.5);
            table.Rows.Add("Banana", 5, 0.3);
            table.Rows.Add("Cherry", 20, 0.2);
            object data = table; // Or use a List<Order> instead

            // ---------- Step 2: Load template ----------
            string templatePath = @"Templates\DynamicTemplate.xlsx";
            Workbook workbook = new Workbook(templatePath);
            Worksheet ws = workbook.Worksheets[0];

            // ---------- Step 3: Set options ----------
            SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
            {
                Advanced = true,
                DetailSheetNewName = "Detail"
            };

            // ---------- Step 4: Process and save ----------
            ws.SmartMarkerProcessor.Process(data, smartMarkerOptions);
            string outputPath = @"Output\DynamicReport.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Dynamic workbook saved to {outputPath}");
        }
    }

    public class Order
    {
        public string Product { get; set; }
        public int Quantity { get; set; }
        public double Price { get; set; }
    }
}
```

Menjalankan program ini akan menghasilkan file `Output\DynamicReport.xlsx` dengan sheet `Detail` terpisah untuk setiap baris di tabel sumber Anda—tepat seperti cara Anda **membuat worksheet dinamis** menggunakan **smart markers aspose.cells**.

## Kesimpulan

Anda kini memiliki resep end‑to‑end yang solid untuk **membuat worksheet dinamis** dengan smart markers Aspose.Cells. Dengan menyiapkan sumber data, memuat template yang kaya marker, menyesuaikan `SmartMarkerOptions`, dan memanggil processor, Anda membiarkan pustaka menangani semua pekerjaan berat.  

Dari sini

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}