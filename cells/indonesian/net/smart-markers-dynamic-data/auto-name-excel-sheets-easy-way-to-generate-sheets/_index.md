---
category: general
date: 2026-02-23
description: Beri nama otomatis pada lembar Excel dan pelajari cara menghasilkan lembar
  secara otomatis menggunakan SmartMarkers. Panduan C# langkah demi langkah untuk
  buku kerja dinamis.
draft: false
keywords:
- auto name excel sheets
- how to generate sheets
- Aspose.Cells SmartMarkers
- dynamic worksheet naming
- C# Excel automation
language: id
og_description: Beri nama lembar Excel secara otomatis dalam sekejap. Pelajari cara
  menghasilkan lembar dengan SmartMarkers di C# – contoh lengkap yang dapat dijalankan.
og_title: Penamaan Otomatis Lembar Excel – Tutorial C# Cepat
tags:
- C#
- Excel
- Aspose.Cells
title: Penamaan Otomatis Lembar Excel – Cara Mudah Membuat Lembar
url: /id/net/smart-markers-dynamic-data/auto-name-excel-sheets-easy-way-to-generate-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Penamaan Otomatis Lembar Excel – Tutorial Lengkap C#

Pernah bertanya-tanya bagaimana cara **auto name excel sheets** tanpa menulis loop yang secara manual mengganti nama setiap tab? Anda bukan satu-satunya. Dalam banyak proyek pelaporan, jumlah lembar bertambah saat runtime, dan menjaga nama tetap rapi menjadi masalah. Kabar baik? Dengan **SmartMarkers** Aspose.Cells Anda dapat membiarkan perpustakaan menangani penamaan untuk Anda, dan bahkan memungkinkan Anda **how to generate sheets** secara langsung.

Dalam panduan ini kami akan membahas skenario dunia nyata: membuat workbook, mengonfigurasi opsi SmartMarker sehingga lembar detail secara otomatis dinamai *Detail*, *Detail1*, *Detail2*, …, dan kemudian memverifikasi bahwa lembar muncul seperti yang diharapkan. Pada akhir panduan Anda akan memiliki solusi mandiri, siap salin‑tempel yang dapat Anda sesuaikan dengan proyek apa pun yang membutuhkan pembuatan worksheet dinamis.

---

## Apa yang Anda Butuhkan

- **.NET 6+** (atau .NET Framework 4.6.2+). Kode ini bekerja pada runtime terbaru apa pun.
- **Aspose.Cells for .NET** paket NuGet – `Install-Package Aspose.Cells`.
- Proyek C# dasar (Console App, WinForms, atau ASP.NET – kode yang sama bekerja di mana saja).
- Visual Studio, VS Code, atau IDE favorit Anda.

Tidak ada interop Excel tambahan, tidak ada COM, hanya kode terkelola murni.

---

## Langkah 1: Auto Name Excel Sheets dengan SmartMarkers

Hal pertama yang harus Anda lakukan adalah memberi tahu Aspose.Cells nama dasar apa yang Anda inginkan untuk lembar detail yang dibuat secara otomatis. Ini dilakukan melalui kelas `SmartMarkerOptions`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;   // for SmartMarkers
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook that will hold the master sheet.
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Master";

        // -----------------------------------------------------------
        // Step 1: Configure SmartMarker options – set the base name
        // -----------------------------------------------------------
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // This tells SmartMarkers to create sheets named Detail, Detail1, Detail2, …
            DetailSheetNewName = "Detail"
        };
```

**Mengapa ini penting:** Dengan mengatur `DetailSheetNewName`, Anda menyerahkan logika penamaan kepada perpustakaan. Tidak perlu menulis loop `for` yang memeriksa nama lembar yang ada dan menambah penghitung – API melakukannya untuk Anda, menjamin nama unik bahkan ketika sumber data berisi puluhan baris.

---

## Langkah 2: Siapkan Sumber Data

SmartMarkers bekerja dengan koleksi `IEnumerable` apa pun, `DataTable`, atau bahkan daftar objek sederhana. Untuk demo ini kami akan menggunakan daftar objek sederhana yang mewakili detail pesanan.

```csharp
        // -----------------------------------------------------------
        // Step 2: Build a sample data source
        // -----------------------------------------------------------
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop", Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",   Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard",Qty = 3, Price =  45.50 }
        };
```

**Mengapa ini penting:** Sumber data menentukan berapa banyak lembar detail yang akan dihasilkan. Setiap elemen dalam koleksi membuat lembar baru berdasarkan template SmartMarker yang akan kami tambahkan selanjutnya.

---

## Langkah 3: Sisipkan Template SmartMarker ke Lembar Master

Template SmartMarker hanyalah sebuah sel (atau rentang) yang berisi placeholder. Ketika metode `Apply` dijalankan, placeholder digantikan dengan data sebenarnya, dan untuk setiap baris sebuah lembar baru dibuat.

```csharp
        // -----------------------------------------------------------
        // Step 3: Add a SmartMarker template to the master sheet
        // -----------------------------------------------------------
        // Put a header row
        ws.Cells["A1"].PutValue("Order ID");
        ws.Cells["B1"].PutValue("Product");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["D1"].PutValue("Unit Price");

        // Insert SmartMarker placeholders starting at row 2
        ws.Cells["A2"].PutValue("&=orders.OrderId");
        ws.Cells["B2"].PutValue("&=orders.Product");
        ws.Cells["C2"].PutValue("&=orders.Qty");
        ws.Cells["D2"].PutValue("&=orders.Price");
```

**Mengapa ini penting:** Sintaks `&=` memberi tahu SmartMarkers “ambil nilai dari sumber data”. Ketika `Apply` dijalankan, Aspose.Cells akan menyalin baris ini ke lembar baru untuk setiap item dalam `orders`, secara otomatis menamai lembar berdasarkan opsi yang kami atur sebelumnya.

---

## Langkah 4: Terapkan Opsi SmartMarker – Di Sinilah Lembar Dinamai Otomatis

Sekarang tiba saatnya perpustakaan melakukan pekerjaan berat. Pemanggilan `Apply` membaca template, membuat lembar detail, dan menamainya sesuai `DetailSheetNewName`.

```csharp
        // -----------------------------------------------------------
        // Step 4: Apply SmartMarker – auto name excel sheets happens here
        // -----------------------------------------------------------
        ws.SmartMarkers.Apply(smartMarkerOptions, new { orders });

        // Save the workbook to verify the result
        wb.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Workbook saved. Open AutoNamedSheets.xlsx to see the result.");
    }
}
```

**Mengapa ini penting:** Metode `Apply` tidak hanya mengisi data tetapi juga menghormati pola penamaan yang kami berikan. Jika Anda membuka *AutoNamedSheets.xlsx* Anda akan melihat:

- **Detail** – berisi pesanan pertama.
- **Detail1** – pesanan kedua.
- **Detail2** – pesanan ketiga.

Tidak diperlukan penamaan manual.

---

## Langkah 5: Verifikasi Hasil – How to Generate Sheets dengan Benar

Setelah menjalankan program, buka file yang dihasilkan. Anda harus melihat tiga worksheet baru yang dinamai persis seperti yang dijelaskan di atas. Ini membuktikan bahwa Anda telah berhasil mempelajari **how to generate sheets** secara otomatis.

> **Tip pro:** Jika Anda membutuhkan akhiran khusus (mis., “_Report”), cukup atur `DetailSheetNewName = "Detail_Report"` dan perpustakaan akan menambahkan angka setelah string dasar.

---

## Kasus Tepi & Pertanyaan Umum

### Bagaimana jika nama dasar sudah ada?

Aspose.Cells memeriksa nama lembar yang ada dan menambahkan nomor inkremental hingga ditemukan nama unik. Jadi bahkan jika ada lembar bernama *Detail* yang sudah ada di workbook, lembar berikutnya yang dihasilkan akan menjadi *Detail1*.

### Bisakah saya mengontrol urutan lembar yang dihasilkan?

Ya. Urutan mengikuti urutan sumber data. Jika Anda membutuhkan urutan tertentu, urutkan koleksi sebelum mengirimkannya ke `Apply`.

### Apakah memungkinkan menghasilkan lembar di workbook yang berbeda?

Tentu saja. Buat instance `Workbook` kedua, tambahkan worksheet placeholder, dan panggil `Apply` pada worksheet tersebut. Logika penamaan yang sama berlaku.

### Bagaimana cara kerja ini dengan set data besar?

SmartMarkers dioptimalkan untuk kinerja. Bahkan dengan ribuan baris, perpustakaan mengalirkan data secara efisien. Pastikan Anda memiliki memori yang cukup untuk ukuran akhir workbook.

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah program lengkap yang dapat Anda masukkan ke dalam proyek console baru. Tidak ada bagian yang hilang – semua mulai dari direktif `using` hingga pemanggilan `Save` akhir disertakan.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System;

class AutoNameExcelSheetsDemo
{
    static void Main()
    {
        // 1️⃣ Create workbook and master worksheet
        Workbook workbook = new Workbook();
        Worksheet master = workbook.Worksheets[0];
        master.Name = "Master";

        // 2️⃣ Set up SmartMarker options – this is the key to auto‑naming
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"   // base name for generated sheets
        };

        // 3️⃣ Sample data source – each element will become a new sheet
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop",   Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",    Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard", Qty = 3, Price =  45.50 }
        };

        // 4️⃣ Build a simple template on the master sheet
        master.Cells["A1"].PutValue("Order ID");
        master.Cells["B1"].PutValue("Product");
        master.Cells["C1"].PutValue("Quantity");
        master.Cells["D1"].PutValue("Unit Price");

        master.Cells["A2"].PutValue("&=orders.OrderId");
        master.Cells["B2"].PutValue("&=orders.Product");
        master.Cells["C2"].PutValue("&=orders.Qty");
        master.Cells["D2"].PutValue("&=orders.Price");

        // 5️⃣ Apply SmartMarkers – this auto‑creates and auto‑names the sheets
        master.SmartMarkers.Apply(options, new { orders });

        // 6️⃣ Save and inform the user
        workbook.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Done! Open AutoNamedSheets.xlsx – you’ll see Detail, Detail1, Detail2 …");
    }
}
```

Jalankan program, buka *AutoNamedSheets.xlsx* yang dihasilkan, dan Anda akan melihat fitur **auto name excel sheets** beraksi.

---

## Pertanyaan Lanjutan yang Sering Diajukan

- **Bisakah saya menggunakan ini dengan file template yang sudah ada?**  
  Ya. Muat workbook dengan `new Workbook("Template.xlsx")` dan arahkan `master` ke lembar yang berisi placeholder SmartMarker Anda.

- **Bagaimana jika saya membutuhkan konvensi penamaan berbeda per jenis lembar?**  
  Buat beberapa objek `SmartMarkerOptions`, masing‑masing dengan `DetailSheetNewName` sendiri, dan terapkan ke lembar master yang berbeda.

- **Apakah ada cara untuk menyembunyikan lembar dasar (yang berisi template)?**  
  Setelah `Apply`, Anda cukup menghapus worksheet master: `workbook.Worksheets.RemoveAt(0);` – lembar detail tetap tidak tersentuh.

---

## Kesimpulan

Anda kini tahu **how to auto name excel sheets** menggunakan Aspose.Cells SmartMarkers, dan Anda juga telah melihat pola yang solid untuk **how to generate sheets** secara dinamis di C#. Ide dasarnya sederhana: konfigurasikan `SmartMarkerOptions.DetailSheetNewName`, berikan sebuah koleksi, dan biarkan perpustakaan melakukan sisanya. Pendekatan ini menghilangkan loop boilerplate, menjamin nama unik, dan skalabel dengan baik.

Siap untuk langkah selanjutnya? Cobalah mengganti sumber data dengan `Data

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}