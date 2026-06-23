---
category: general
date: 2026-03-25
description: Pelajari cara mengekspor Excel ke DataTable dalam C# dengan cepat. Tutorial
  ini mencakup mengekspor Excel dengan nama kolom dan mengekspor data Excel sebagai
  string untuk penanganan data yang andal.
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: id
og_description: Ekspor Excel ke DataTable dalam C# dengan nama kolom dan konversi
  string. Ikuti tutorial singkat ini untuk solusi siap pakai.
og_title: Ekspor Excel ke DataTable di C# – Panduan Lengkap
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: Ekspor Excel ke DataTable di C# – Panduan Langkah demi Langkah
url: /id/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel ke DataTable di C# – Panduan Langkah‑per‑Langkah

Pernah perlu **mengekspor Excel ke DataTable** tapi tidak yakin flag mana yang harus diaktifkan? Anda tidak sendirian—banyak pengembang mengalami hal yang sama saat pertama kali mencoba mengambil data spreadsheet ke dalam `DataTable`.  

Kabar baiknya? Dalam beberapa baris kode saja Anda dapat **mengekspor Excel dengan nama kolom** dan bahkan **mengekspor data Excel sebagai string** untuk menghindari masalah ketidaksesuaian tipe. Di bawah ini Anda akan menemukan contoh lengkap yang dapat dijalankan serta penjelasan “mengapa” di balik setiap pengaturan, sehingga Anda dapat menyesuaikannya dengan proyek apa pun tanpa menebak‑nebak.

## Apa yang Dibahas dalam Tutorial Ini

* Cara membuat workbook di memori (tanpa file fisik).  
* Mengisi beberapa baris contoh agar Anda dapat melihat hasilnya secara langsung.  
* Mengonfigurasi `ExportTableOptions` sehingga setiap sel diperlakukan sebagai string.  
* Mengekspor rentang persegi panjang ke `DataTable` sambil mempertahankan baris pertama sebagai header kolom.  
* Memverifikasi output dan mencetak baris pertama ke konsol.  

Tidak ada tautan dokumentasi eksternal yang diperlukan—semua yang Anda butuhkan ada di sini. Jika Anda sudah memiliki file Excel di disk, cukup ganti baris pembuatan workbook dengan `new Workbook("path/to/file.xlsx")` dan Anda siap melanjutkan.

---

## Langkah 1: Siapkan Proyek dan Tambahkan Paket NuGet Aspose.Cells

Sebelum menulis kode apa pun, pastikan proyek Anda mereferensikan **Aspose.Cells for .NET** (perpustakaan yang menyediakan kelas `Workbook`). Anda dapat menambahkannya melalui NuGet Package Manager:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Gunakan versi stabil terbaru (per Maret 2026, versi 22.12) untuk mendapatkan perbaikan bug dan peningkatan performa terbaru.

---

## Langkah 2: Buat Workbook dan Isi dengan Data Contoh

Kita akan mulai dengan `Workbook` baru dan menulis beberapa baris sehingga Anda dapat melihat proses ekspor secara langsung. Langkah ini juga mendemonstrasikan **cara mengekspor excel ke datatable** ketika data sumber hanya berada di memori.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*Mengapa ini penting:* Dengan menyisipkan baris header terlebih dahulu (`A1` & `B1`), kita dapat memberi tahu exporter untuk memperlakukan baris pertama sebagai nama kolom—tepat seperti yang dimaksud dengan **export excel with column names**.

---

## Langkah 3: Beri Tahu Aspose.Cells untuk Memperlakukan Setiap Sel sebagai String

Saat Anda mengekspor sel numerik atau tanggal, Aspose berusaha menebak tipe .NET. Hal ini dapat menimbulkan bug halus jika kode downstream Anda mengharapkan string. Flag `ExportTableOptions.ExportAsString` memaksa konversi seragam ke string.

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*Mengapa menggunakan ini?* Bayangkan sebuah kolom yang kadang berisi angka dan kadang teks (misalnya “00123” vs. “ABC”). Dengan mengekspor semuanya sebagai string, Anda menghindari kehilangan nol di depan atau munculnya pengecualian konversi tipe.

---

## Langkah 4: Ekspor Rentang yang Diinginkan ke DataTable

Sekarang kita benar‑benar **mengekspor excel ke datatable**. Metode `ExportDataTable` menerima baris/kolom awal, jumlah baris/kolom, flag untuk ekstraksi nama kolom, dan opsi yang baru saja kita buat.

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*Apa yang terjadi di balik layar?*  
- `startRow: 0` menunjuk pada baris Excel pertama (baris header).  
- `exportColumnNames: true` memberi tahu Aspose untuk mengangkat “Name” dan “Age” ke dalam koleksi kolom `DataTable`.  
- `totalRows`/`totalColumns` dapat lebih besar dari data sebenarnya; sel berlebih menjadi string kosong karena `ExportAsString`.

---

## Langkah 5: Verifikasi Hasil – Cetak Baris Pertama

Dump cepat ke konsol membuktikan bahwa konversi berhasil dan nama kolom tetap utuh.

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**Output yang diharapkan**

```
First row: Alice, 30
```

Jika Anda mengubah data contoh, konsol akan menampilkan perubahan tersebut secara otomatis—tanpa kode tambahan.

---

## Pertanyaan yang Sering Diajukan & Kasus Pinggir

| Pertanyaan | Jawaban |
|------------|---------|
| **Apakah saya bisa mengekspor sheet yang sudah ada di disk?** | Ya—ganti `new Workbook()` dengan `new Workbook("myFile.xlsx")`. Langkah‑langkah selanjutnya tetap sama. |
| **Bagaimana jika file Excel saya memiliki sel yang digabung?** | Sel yang digabung akan di‑unwrap; nilai sel paling kiri‑atas digunakan untuk seluruh rentang yang digabung. |
| **Apakah saya perlu khawatir tentang format angka yang spesifik budaya?** | Tidak ketika `ExportAsString = true`; semuanya datang sebagai string mentah yang ditampilkan di Excel. |
| **Berapa banyak baris yang dapat saya ekspor sekaligus?** | Aspose.Cells dapat menangani jutaan baris, tetapi konsumsi memori meningkat seiring ukuran `DataTable`. Pertimbangkan paging jika Anda mencapai batas. |
| **Bagaimana dengan kolom yang disembunyikan?** | Kolom tersembunyi akan diekspor kecuali Anda mengatur `ExportHiddenColumns = false` pada `ExportTableOptions`. |

---

## Bonus: Mengekspor ke CSV Alih‑Alih DataTable

Kadang Anda mungkin lebih suka file datar. `ExportTableOptions` yang sama dapat dipakai kembali dengan `ExportDataTableToCSV`:

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

Satu baris kode itu memberi Anda CSV siap impor sambil tetap **mengekspor data excel sebagai string**.

---

## Contoh Lengkap yang Siap Dijalankan (Copy‑Paste)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

Jalankan program (`dotnet run`) dan Anda akan melihat hasil **export excel to datatable** tercetak di konsol. Ganti data contoh, ubah `totalRows`/`totalColumns`, atau arahkan workbook ke file nyata—semua akan tetap berfungsi.

---

## Kesimpulan

Anda kini memiliki **solusi lengkap dan mandiri untuk mengekspor Excel ke DataTable** di C#. Dengan mengonfigurasi `ExportTableOptions.ExportAsString` Anda menjamin bahwa **export excel data as string**, dan dengan mengatur `exportColumnNames: true` Anda mendapatkan header kolom yang familiar saat **export excel with column names**.  

Dari sini Anda dapat:

* Memasukkan `DataTable` ke Entity Framework atau Dapper untuk bulk insert.  
* Mengirimkannya ke mesin pelaporan seperti **FastReport** atau **RDLC**.  
* Mengonversinya ke JSON untuk respons API (`JsonConvert.SerializeObject(table)`).

Silakan bereksperimen—mungkin coba mengekspor sheet yang lebih besar, atau gabungkan ini dengan **cara mengekspor excel ke datatable** dari share jaringan. Polanya tetap sama, dan kodenya siap untuk produksi.

---

![Diagram of Excel → DataTable conversion flow – export excel to datatable](https://example.com/placeholder.png "export excel to datatable diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}