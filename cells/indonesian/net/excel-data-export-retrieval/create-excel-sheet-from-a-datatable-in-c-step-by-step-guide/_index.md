---
category: general
date: 2026-08-11
description: Buat lembar excel dari DataTable di C# dan ekspor datatable ke excel
  dengan penamaan lembar otomatis. Pelajari cara menambahkan baris ke datatable dan
  menyimpan workbook sebagai xlsx.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: id
lastmod: 2026-08-11
og_description: Buat lembar Excel dari DataTable di C#. Tutorial ini menunjukkan cara
  mengekspor DataTable ke Excel, menambahkan baris ke DataTable, menghasilkan beberapa
  lembar Excel, dan menyimpan buku kerja sebagai file xlsx.
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: Buat lembar Excel dari DataTable di C# – panduan pemrograman lengkap
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Buat lembar excel dari DataTable di C# – panduan langkah demi langkah
url: /id/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat lembar excel dari DataTable di C# – panduan langkah demi langkah

Jika Anda perlu **create excel sheet** dari `DataTable` di C#, panduan ini menunjukkan secara tepat cara melakukannya. Anda akan melihat cara **export datatable to excel**, menambahkan baris, menangani nama lembar duplikat, dan akhirnya **save workbook as xlsx**.

Contoh ini menggunakan Aspose.Cells, perpustakaan .NET yang banyak digunakan untuk otomatisasi Excel. Konsep yang sama berlaku untuk perpustakaan lain yang mendukung pemrosesan gaya SmartMarker, tetapi kode di bawah ini dapat langsung digunakan dengan Aspose.Cells 22.12 atau yang lebih baru.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* .NET 6.0 SDK atau yang lebih baru terpasang  
* Referensi ke paket NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`)  
* Pemahaman dasar tentang `DataTable` dan aplikasi konsol C#  

Persyaratan ini menjaga tutorial tetap mandiri dan menghindari penggunaan alat eksternal.

## Langkah 1: Buat DataTable yang akan diekspor ke Excel

Langkah pertama adalah membuat `DataTable` yang mencerminkan data yang Anda inginkan di lembar kerja. Di sini kami membuat tabel bernama **Sheet1**, menambahkan kolom `Id`, dan menyisipkan dua baris.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**Mengapa ini penting:**  
`DataTable` adalah representasi data tabular dalam memori yang nyaman. Menamai tabel dengan `"Sheet1"` memberi tahu Aspose.Cells lembar mana yang menjadi target saat memproses SmartMarkers.

## Langkah 2: Tambahkan baris ke DataTable (ekspansi opsional)

Jika data sumber Anda bersifat dinamis, Anda sering perlu menambahkan baris dalam sebuah loop. Potongan kode berikut menunjukkan pola umum:

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**Tip:** Saat menambahkan banyak baris, pertimbangkan untuk menonaktifkan constraints (`dataTable.Constraints.Clear()`) untuk meningkatkan kinerja.

## Langkah 3: Konfigurasikan opsi SmartMarker untuk membuat beberapa lembar excel secara otomatis

Opsi SmartMarker memungkinkan Anda mengontrol cara penanganan nama lembar duplikat. Menetapkan `DetailSheetNewName` ke `"Sheet1_{0}"` memberi tahu Aspose.Cells untuk mengganti nama lembar berikutnya menjadi `Sheet1_1`, `Sheet1_2`, dan seterusnya.

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**Mengapa ini penting:**  
Ketika Anda memproses beberapa objek `DataTable` yang memiliki nama sama, Excel biasanya akan menghasilkan error karena nama lembar harus unik. Pola `DetailSheetNewName` secara otomatis menghilangkan konflik tersebut.

## Langkah 4: Proses SmartMarkers dan ekspor datatable ke excel

Sekarang kami membuat `Workbook` baru, menjalankan `ProcessSmartMarkers`, dan membiarkan Aspose.Cells mengisi lembar kerja berdasarkan `DataTable`.

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**Penjelasan:**  
`ProcessSmartMarkers` memindai workbook untuk penanda seperti `&=Sheet1!A1` (tidak ditampilkan di sini) dan menggantinya dengan data dari `dataTable`. Karena kami memulai dengan workbook kosong, Aspose.Cells membuat lembar baru yang cocok dengan nama tabel dan mengisinya dengan baris yang kami tambahkan.

## Langkah 5: Simpan workbook sebagai xlsx

Akhirnya, tulis workbook ke disk dengan format OpenXML modern (`.xlsx`). Anda dapat mengubah path sesuai lingkungan Anda.

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Hasil:**  

| Nama lembar | Baris |
|------------|------|
| Sheet1     | 1, 2, 3, 4, 5 |
| Sheet1_1   | (jika DataTable lain dengan nama yang sama diproses) |

Logika penggantian nama lembar memastikan **create multiple excel sheets** tanpa pengelolaan nama manual.

## Variasi umum dan kasus tepi

| Situasi | Cara menanganinya |
|-----------|------------------|
| **Tabel sangat besar** (≥ 100 000 baris) | Gunakan `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` sebelum memproses untuk menjaga penggunaan memori tetap rendah. |
| **Urutan kolom khusus** | Urutkan kembali objek `DataColumn` dalam `DataTable` sebelum memanggil `ProcessSmartMarkers`. |
| **Beberapa DataTable dengan nama berbeda** | Panggil `ProcessSmartMarkers` untuk setiap tabel; Aspose.Cells akan membuat lembar terpisah untuk setiap nama secara otomatis. |
| **Butuh baris header dengan styling** | Setelah pemrosesan, akses `Worksheet.Cells["A1"]` dan terapkan properti `Style` (font, latar belakang). |
| **Menyimpan ke stream alih-alih file** | Ganti `workbook.Save(outputPath, SaveFormat.Xlsx)` dengan `workbook.Save(stream, SaveFormat.Xlsx)`. |

**Pro tip:** Selalu bungkus operasi sistem file dalam blok `try…catch` untuk menampilkan masalah izin lebih awal.

## Kode sumber lengkap (siap disalin)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Output yang diharapkan

Menjalankan program mencetak:

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

Membuka `DuplicateSheets.xlsx` menampilkan lembar bernama **Sheet1** dengan kolom `Id` berisi nilai `1, 2, 3, 4, 5`. Jika Anda kemudian memproses `DataTable` lain bernama `"Sheet1"` dalam workbook yang sama, Aspose.Cells akan secara otomatis membuat **Sheet1_1**, **Sheet1_2**, dll.

## Kesimpulan

Anda sekarang tahu cara **create excel sheet** dari `DataTable` di C#, **export datatable to excel**, **add rows to datatable**, menghasilkan **create multiple excel sheets** dengan penamaan otomatis, dan **save workbook as xlsx**. Contoh lengkap yang dapat dijalankan ini menunjukkan alur kerja end‑to-end dan memberikan tip praktis untuk set data besar serta styling khusus.

### Apa selanjutnya?

* Jelajahi **cell formatting** (font, warna, border) dengan mengakses `Worksheet.Cells` setelah `ProcessSmartMarkers`.  
* Gunakan **SmartMarker loops** untuk menghasilkan laporan master‑detail dalam satu workbook.  
* Beralih ke **CSV export** dengan mengubah `SaveFormat.Csv` jika Anda membutuhkan representasi teks biasa.  

Silakan sesuaikan kode dengan sumber data Anda sendiri—baik itu query basis data, respons API, atau koleksi dalam memori. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Membuat dan Menyimpan Workbook Excel sebagai ODS Menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Cara Membuat dan Menyimpan Workbook Excel sebagai SVG menggunakan Aspose.Cells untuk Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Cara Membuat dan Mengekspor Excel ke HTML Menggunakan Aspose.Cells Java | Panduan Operasi Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}