---
category: general
date: 2026-03-18
description: Cara mengekspor data Excel ke DataTable dalam C# dengan kode yang menangani
  sel tertentu, mengonversi Excel ke DataTable, dan memformat angka. Pelajari cara
  mengekspor sel tertentu dan lainnya.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: id
og_description: Cara mengekspor data Excel ke DataTable di C#. Tutorial ini menunjukkan
  cara mengekspor sel tertentu, mengonversi Excel ke DataTable, dan memformat angka
  dengan mudah.
og_title: Cara Mengekspor Excel ke DataTable di C# – Panduan Lengkap
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Cara Mengekspor Excel ke DataTable di C# – Panduan Langkah demi Langkah
url: /id/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengekspor Excel ke DataTable di C# – Panduan Langkah‑per‑Langkah

Pernah bertanya-tanya **bagaimana cara mengekspor data Excel** ke dalam `DataTable` tanpa kehilangan format? Anda bukan satu-satunya—para pengembang terus-menerus perlu mengambil sebagian lembar kerja ke memori untuk pelaporan, validasi, atau operasi bulk‑insert. Kabar baiknya? Dengan beberapa baris C# Anda dapat mengekspor rentang yang tepat (misalnya *A1:F11*), memaksa setiap sel diperlakukan sebagai string, dan bahkan menerapkan format angka khusus.

Dalam tutorial ini kami akan membahas semua yang perlu Anda ketahui: mulai dari memuat workbook, mengonfigurasi **export specific cells**, mengonversi rentang ke `DataTable`, dan menangani kasus tepi seperti baris kosong atau angka yang bergantung pada locale. Pada akhir tutorial Anda akan memiliki metode yang dapat digunakan kembali yang bekerja dengan skenario **excel to datatable c#** dalam kode produksi.

> **Prasyarat** – Anda memerlukan library Aspose.Cells untuk .NET (atau API serupa yang menyediakan `ExportDataTable`). Contoh ini mengasumsikan .NET 6+, tetapi konsepnya juga berlaku untuk versi sebelumnya.

## Apa yang Akan Anda Pelajari

- Cara **mengonversi Excel ke DataTable** menggunakan Aspose.Cells.
- Mengekspor rentang khusus (`excel range to datatable`) sambil memperlakukan semua nilai sebagai string.
- Menerapkan format angka dua desimal (`#,#00.00`) saat mengekspor.
- Kesalahan umum (baris null, kolom tersembunyi) dan cara menghindarinya.
- Contoh kode siap‑salin, yang dapat dijalankan sepenuhnya.

## Prasyarat dan Penyiapan

Sebelum kita masuk ke kode, pastikan Anda memiliki:

1. **Aspose.Cells untuk .NET** terpasang via NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. File Excel (`input.xlsx`) ditempatkan di folder yang dapat Anda referensikan, misalnya `YOUR_DIRECTORY/input.xlsx`.
3. Proyek yang menargetkan .NET 6 atau lebih baru (pernyataan `using` di bawah ini bekerja langsung).

> **Tips Pro:** Jika Anda menggunakan library lain (mis., EPPlus atau ClosedXML), konsepnya tetap sama—muat workbook, pilih rentang, dan panggil metode yang mengembalikan `DataTable`.

## Langkah 1: Muat Workbook dan Ambil Worksheet Pertama

Hal pertama yang Anda butuhkan adalah objek `Workbook` yang mewakili file Excel Anda. Setelah Anda memilikinya, Anda dapat mengakses worksheet mana pun dengan indeks atau nama.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**Mengapa ini penting:** Memuat workbook lebih awal memungkinkan Anda memeriksa strukturnya (sheet tersembunyi, proteksi) sebelum memutuskan sel mana yang akan diekspor. Jika file besar, pertimbangkan menggunakan `LoadOptions` untuk men-stream hanya bagian yang diperlukan.

## Langkah 2: Konfigurasikan Opsi Ekspor – Perlakukan Semua Nilai sebagai String

Saat Anda mengekspor data untuk pemrosesan selanjutnya (mis., bulk insert ke SQL), Anda sering menginginkan **representasi string yang konsisten**. Ini menghindari kesalahan ketidakcocokan tipe di kemudian hari.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Penjelasan:**  
- `ExportAsString = true` memberi tahu Aspose.Cells untuk mengabaikan tipe sel asli dan mengembalikan teks yang diformat.  
- `NumberFormat = "#,##0.00"` memastikan angka seperti `1234.5` menjadi `"1,234.50"`—berguna untuk laporan keuangan.

Jika Anda membutuhkan tipe data asli, cukup set `ExportAsString` ke `false` dan tangani konversinya sendiri.

## Langkah 3: Ekspor Rentang Spesifik (A1:F11) ke DataTable

Sekarang masuk ke inti **export specific cells**. Metode `ExportDataTable` menerima indeks baris/kolom mulai/akhir (berbasis nol) serta sebuah flag untuk inklusi header.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**Apa yang Anda dapatkan:** Sebuah `DataTable` dengan 11 baris (termasuk header) dan 6 kolom (`A`‑`F`). Semua nilai adalah string yang diformat sesuai `exportOptions`.

## Langkah 4: Verifikasi Hasil – Cetak ke Konsol

Selalu merupakan ide yang baik untuk memeriksa keabsahan output sebelum Anda menyerahkan tabel ke komponen lain.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

Anda seharusnya melihat sesuatu seperti:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

Perhatikan bagaimana kolom numerik menampilkan dua tempat desimal, persis seperti yang kami tentukan.

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Di bawah ini adalah program lengkap yang menggabungkan semuanya. Letakkan ke dalam proyek konsol baru, sesuaikan jalur file, dan jalankan—tidak diperlukan konfigurasi tambahan.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Poin penting dari kode:**

- Objek `ExportTableOptions` dapat digunakan kembali; Anda dapat meneruskannya ke beberapa panggilan `ExportDataTable` jika perlu mengekspor beberapa rentang.
- Pengindeksan dimulai dari **0**, sehingga `A1` berkorespondensi dengan `(0,0)`.
- Menetapkan `includeColumnNames` ke `true` secara otomatis menggunakan baris pertama sebagai header kolom—bagus untuk operasi `DataTable` selanjutnya.

## Menangani Kasus Tepi & Pertanyaan Umum

### Bagaimana jika worksheet memiliki baris atau kolom tersembunyi?

Aspose.Cells menghormati visibilitas secara default. Jika Anda perlu mengekspor data tersembunyi, set `exportOptions.ExportHiddenRows = true` dan `ExportHiddenColumns = true`.

### File Excel saya berisi formula—apakah saya akan mendapatkan nilai yang dihitung?

Ya. Secara default `ExportDataTable` mengembalikan **nilai yang ditampilkan** (hasil dari formula). Jika Anda menginginkan teks formula mentah, set `exportOptions.ExportFormulas = true`.

### Bagaimana cara melewatkan baris yang sepenuhnya kosong?

Setelah ekspor, Anda dapat memangkas `DataTable`:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### Bisakah saya mengekspor rentang tidak berurutan (mis., A1:B5 dan D1:E5)?

Aspose.Cells tidak mendukung rentang terpisah dalam satu panggilan. Sebagai gantinya, ekspor setiap blok secara terpisah lalu gabungkan `DataTable` yang dihasilkan secara manual.

## Tips Kinerja

- **Gunakan kembali `ExportTableOptions`** untuk beberapa ekspor; membuat instance baru setiap kali menambah overhead yang dapat diabaikan tetapi membuat kode berantakan.
- **Stream file besar** dengan `LoadOptions` untuk menghindari memuat seluruh workbook ke memori.
- **Hindari `DataTable`** jika Anda hanya membutuhkan ekspor CSV cepat—`ExportDataTable` nyaman tetapi bukan yang paling efisien memori untuk sheet yang sangat besar.

## Kesimpulan

Kami telah membahas **cara mengekspor data Excel** ke dalam `DataTable` sambil mengontrol format, menangani rentang sel spesifik, dan memastikan setiap nilai datang sebagai string. Contoh lengkap menunjukkan pendekatan bersih yang siap produksi yang dapat Anda sesuaikan untuk **convert excel to datatable**, **export specific cells**, atau skenario **excel range to datatable** apa pun yang Anda temui.

Silakan bereksperimen: ubah rentang, alihkan `ExportAsString`, atau alirkan `DataTable` langsung ke Entity Framework untuk bulk insert. Kemungkinannya tidak terbatas setelah Anda memiliki fondasi yang kuat ini.

### Langkah Selanjutnya & Topik Terkait

- **Mengimpor DataTable kembali ke Excel** – pelajari operasi sebaliknya dengan `ImportDataTable`.
- **Bulk insert DataTable ke SQL Server** – gunakan `SqlBulkCopy` untuk pemuatan super cepat.
- **Bekerja dengan EPPlus atau ClosedXML** – lihat bagaimana tugas yang sama terlihat dengan library alternatif.
- **Memformat sel saat ekspor** – jelajahi lebih jauh `ExportTableOptions` untuk format tanggal, pengaturan budaya khusus, dan lainnya.

Punya pertanyaan atau kasus penggunaan yang berbeda? Tinggalkan komentar, dan mari teruskan diskusinya. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}