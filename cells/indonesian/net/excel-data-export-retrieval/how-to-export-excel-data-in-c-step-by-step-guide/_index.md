---
category: general
date: 2026-03-21
description: Cara mengekspor data Excel dengan nama kolom, mempertahankan format angka,
  dan membaca baris tertentu menggunakan Aspose.Cells dalam C#. Pelajari cara membaca
  lembar kerja Excel dan mengekspor baris tertentu secara efisien.
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: id
og_description: Cara mengekspor data Excel dengan nama kolom, mempertahankan format
  angka, dan membaca baris tertentu menggunakan Aspose.Cells. Contoh lengkap yang
  dapat dijalankan untuk pengembang C#.
og_title: Cara Mengekspor Data Excel di C# – Panduan Pemrograman Lengkap
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Cara Mengekspor Data Excel di C# – Panduan Langkah demi Langkah
url: /id/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengekspor Data Excel di C# – Panduan Pemrograman Lengkap

Pernah bertanya-tanya **how to export excel** data tanpa kehilangan format aslinya? Mungkin Anda sudah mencoba copy‑paste cepat dan berakhir dengan tanggal yang terlihat seperti “44728” atau header kolom yang hilang. Itu membuat frustrasi, bukan? Dalam tutorial ini Anda akan melihat cara bersih, end‑to‑end untuk membaca sebuah lembar kerja Excel, mempertahankan format angka, mengekspor dengan nama kolom, dan bahkan memilih hanya baris yang Anda butuhkan.

Kami akan menggunakan library Aspose.Cells karena memberikan kontrol detail atas opsi ekspor. Pada akhir panduan ini Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat dimasukkan ke proyek .NET apa pun, serta Anda akan memahami mengapa setiap opsi penting. Tidak diperlukan dokumen eksternal—semua yang Anda butuhkan ada di sini.

---

## Apa yang Akan Anda Pelajari

- **Read Excel worksheet** ke memori dengan Aspose.Cells.
- **Export specific rows** (misalnya baris 0‑49) sambil mempertahankan nama kolom.
- **Preserve number format** sehingga mata uang, tanggal, dan persentase tetap utuh.
- Cara **export with column names** dan menyertakan komentar sel jika Anda membutuhkannya.
- Contoh C# lengkap, siap‑jalankan plus tips untuk jebakan umum.

### Prasyarat

- .NET 6.0 atau lebih baru (kode berfungsi dengan .NET Framework 4.6+ juga).
- Aspose.Cells for .NET terinstal via NuGet (`Install-Package Aspose.Cells`).
- Sebuah file Excel (`input.xlsx`) ditempatkan di folder yang dapat Anda referensikan.

> **Pro tip:** Jika Anda berada di pipeline CI, pertimbangkan untuk menarik paket NuGet dari feed pribadi untuk menghindari kejutan lisensi.

---

## Langkah 1 – Instal Aspose.Cells dan Tambahkan Namespace

Pertama, pastikan paket Aspose.Cells ada di proyek Anda. Buka Package Manager Console dan jalankan:

```powershell
Install-Package Aspose.Cells
```

Kemudian tambahkan direktif `using` yang diperlukan di bagian atas file C# Anda:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

Import ini memberi Anda akses ke `Workbook`, `Worksheet`, `ExportTableOptions`, dan `DataTable`—bagian inti untuk **reading an Excel worksheet** dan mengekspor data.

---

## Langkah 2 – Muat Workbook (Baca File Excel)

Sekarang kita benar‑benarnya **read the Excel worksheet**. Konstruktor `Workbook` menerima path ke file, dan Aspose.Cells akan menangani format `.xlsx` maupun `.xls` yang lebih lama.

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Mengapa ini penting:** Memuat workbook sekali dan menggunakan kembali objek `Worksheet` yang sama jauh lebih efisien daripada membuka file berulang‑ulang, terutama untuk spreadsheet besar.

---

## Langkah 3 – Konfigurasi Opsi Ekspor (Preserve Number Format & Column Names)

Di sinilah kami memberi tahu Aspose.Cells *bagaimana* mengekspor. Kelas `ExportTableOptions` memungkinkan kami menyesuaikan output secara detail. Kami akan mengaktifkan tiga flag:

1. `ExportAsString = true` – memaksa setiap sel menjadi string, yang menjamin angka tetap mempertahankan representasi visualnya.
2. `IncludeCellComments = true` – menyalin semua komentar yang terlampir pada sel (berguna untuk dokumentasi).
3. `PreserveNumberFormat = true` – mempertahankan format angka asli (simbol mata uang, pola tanggal, dll).

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Kasus tepi:** Jika Anda mengatur `ExportAsString` ke `false` tetapi masih ingin mempertahankan format angka, Anda mungkin mendapatkan nilai numerik mentah (mis., 44728 untuk tanggal). Menjaga kedua flag tetap aktif menghindari kejutan tersebut.

---

## Langkah 4 – Ambil Worksheet Pertama (Read Excel Worksheet)

Sebagian besar file sederhana memiliki data yang Anda butuhkan pada sheet pertama, jadi kami akan mengambilnya berdasarkan indeks. Jika Anda memerlukan sheet lain, cukup ganti `0` dengan indeks berbasis nol yang sesuai atau gunakan `workbook.Worksheets["SheetName"]`.

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Mengapa ini berguna:** Mengakses objek worksheet secara langsung memberi Anda kontrol penuh atas koleksi `Cells`‑nya, yang penting untuk **export specific rows** nanti.

---

## Langkah 5 – Ekspor Rentang Sel (Export Specific Rows)

Sekarang inti tutorial: mengekspor baris 0‑49 dan kolom 0‑4 (yaitu 50 baris pertama dan lima kolom pertama) ke dalam `DataTable`. Kami juga akan meminta Aspose.Cells menyertakan nama kolom sebagai baris pertama `DataTable`.

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### Apa yang Dilakukan Ini

- **`startRow: 0`** – memulai di bagian paling atas sheet.
- **`totalRows: 50`** – mengambil 50 baris pertama (yaitu **export specific rows**).
- **`totalColumns: 5`** – membatasi ekspor ke lima kolom pertama.
- **`includeColumnNames: true`** – memastikan header kolom `DataTable` cocok dengan baris header Excel, memenuhi persyaratan **export with column names**.
- **`exportOptions`** – menerapkan pengaturan dari Langkah 3, sehingga nilai numerik Anda tetap terlihat seperti “$1,234.56” bukan “1234.56”.

---

## Langkah 6 – Verifikasi Ekspor (Bagaimana Hasilnya Terlihat)

Mari cetak beberapa baris pertama ke konsol sehingga Anda dapat melihat bahwa format tetap terjaga.

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**Output yang diharapkan (contoh):**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

Perhatikan bagaimana tanggal muncul dalam format `MM/dd/yyyy` dan mata uang mempertahankan simbol `$`—berkat **preserve number format**.

---

## Kesalahan Umum & Cara Menghindarinya

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Tanggal berubah menjadi angka besar | `ExportAsString` dibiarkan `false` | Pertahankan `ExportAsString = true` atau konversi sel secara manual |
| Header kolom hilang | `includeColumnNames` diset ke `false` | Setel ke `true` ketika Anda membutuhkan **export with column names** |
| Komentar menghilang | `IncludeCellComments` tidak diaktifkan | Aktifkan `IncludeCellComments` di `ExportTableOptions` |
| Mengekspor sheet yang salah | Menggunakan `Worksheets[0]` pada file multi‑sheet | Tentukan nama sheet: `workbook.Worksheets["Data"]` |
| Exception out‑of‑range | `totalRows` melebihi jumlah baris sebenarnya | Gunakan `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

---

## Bonus: Mengekspor Seluruh Sheet Sambil Tetap Mempertahankan Format

Jika nanti Anda memutuskan membutuhkan seluruh sheet, cukup ganti `totalRows` dan `totalColumns` dengan dimensi maksimum sheet:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

Sekarang Anda memiliki rutinitas **read excel worksheet** yang bekerja untuk ukuran apa pun, sambil tetap **preserving number format** dan **exporting with column names**.

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah program lengkap yang dapat Anda masukkan ke aplikasi console. Program ini mencakup semua langkah, import, dan cetakan verifikasi sederhana.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

Simpan ini sebagai `Program.cs`, jalankan `dotnet run`, dan Anda akan melihat pratinjau terformat di terminal Anda.

---

## Kesimpulan

Kami baru saja membahas **how to export excel** data menggunakan Aspose.Cells, mencakup semua hal mulai dari memuat workbook hingga mempertahankan format angka, mengekspor dengan nama kolom, dan membatasi ekspor ke baris tertentu. Kode ini mandiri, dapat dijalankan sepenuhnya, dan menyertakan perlindungan praktis untuk kasus tepi yang paling umum.

Siap untuk tantangan berikutnya? Cobalah mengekspor langsung ke CSV sambil tetap mempertahankan format angka asli, atau dorong `DataTable` ke konteks Entity Framework Core untuk penyisipan basis data massal. Kedua skenario dibangun di atas dasar yang sama yang kami bahas di sini.

Jika Anda menemukan panduan ini bermanfaat

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}