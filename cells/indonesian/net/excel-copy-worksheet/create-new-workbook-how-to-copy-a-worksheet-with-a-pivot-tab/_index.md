---
category: general
date: 2026-03-01
description: Buat buku kerja baru dan salin lembar kerja ke buku kerja dengan tabel
  pivot. Pelajari cara mengekspor tabel pivot, menyalin lembar, dan menyalin pivot
  di C#.
draft: false
keywords:
- create new workbook
- copy worksheet to workbook
- export pivot table
- how to copy sheet
- how to copy pivot
language: id
og_description: Buat buku kerja baru di C# dan salin lembar kerja ke buku kerja sambil
  mempertahankan tabel pivot. Panduan langkah demi langkah dengan kode lengkap.
og_title: Buat Buku Kerja Baru – Salin Lembar Kerja & Tabel Pivot di C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Buat Buku Kerja Baru – Cara Menyalin Lembar Kerja dengan Tabel Pivot
url: /id/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Workbook Baru – Salin Worksheet & Pivot Table di C#

Pernah membutuhkan **create new workbook** yang berisi pivot table siap pakai tanpa harus membangunnya dari awal? Anda bukan satu-satunya. Dalam banyak skenario pelaporan Anda memiliki file master (`src.xlsx`) dengan pivot yang kompleks, dan Anda ingin mengirim salinan bersih (`dest.xlsx`) ke klien atau sistem lain. Kabar baiknya? Anda dapat melakukannya hanya dengan dua baris C#—dan panduan ini akan menunjukkan cara tepatnya.

Kami akan membahas seluruh proses: memuat workbook sumber, menyalin worksheet pertama (yang berisi pivot), dan menyimpannya sebagai workbook baru. Pada akhir Anda akan mengetahui **how to copy sheet** yang berisi pivot, cara **export pivot table** data jika Anda membutuhkannya, dan bahkan beberapa trik untuk kasus tepi seperti menyalin ke file yang sudah ada.

## Prasyarat

- .NET 6.0 atau lebih baru (versi terbaru apa pun dapat digunakan)
- Aspose.Cells untuk .NET (versi percobaan gratis atau berlisensi) – pustaka ini menyediakan kelas `Workbook` yang digunakan di bawah.
- File Excel sumber (`src.xlsx`) yang sudah berisi pivot table pada worksheet pertama.

Jika Anda belum memiliki Aspose.Cells, tambahkan melalui NuGet:

```bash
dotnet add package Aspose.Cells
```

Itu saja—tanpa interop COM tambahan, tanpa Excel terpasang di server.

## Apa yang Dibahas Tutorial Ini

- **Create new workbook** dari worksheet yang sudah ada yang berisi pivot.
- **Copy worksheet to workbook** sambil mempertahankan semua definisi pivot.
- **Export pivot table** data ke DataTable (opsional).
- Jebakan umum saat menggunakan **how to copy pivot** di lingkungan yang berbeda.
- Contoh lengkap yang dapat dijalankan yang dapat Anda masukkan ke aplikasi console.

---

## Langkah 1: Muat Workbook Sumber (How to Copy Sheet)

Hal pertama yang Anda lakukan adalah membuka workbook yang berisi pivot table. Menggunakan Aspose.Cells membuat ini mudah karena membaca file ke memori tanpa meluncurkan Excel.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the pivot
        string srcPath = @"YOUR_DIRECTORY\src.xlsx";

        // Load the workbook – this is where we **create new workbook** later
        Workbook sourceWorkbook = new Workbook(srcPath);
```

> **Mengapa ini penting:** Memuat file memvalidasi bahwa pivot ada dan memberi Anda akses ke koleksi worksheet. Jika file rusak, `Workbook` melemparkan pengecualian yang jelas, menyelamatkan Anda dari output misterius nanti.

## Langkah 2: Salin Worksheet ke Workbook Baru (Copy Worksheet to Workbook)

Sekarang kita benar‑benarnya **copy worksheet to workbook**. Metode `CopyTo` milik Aspose.Cells menyalin seluruh sheet—termasuk formula, format, dan pivot cache—ke file baru.

```csharp
        // Destination path for the new workbook
        string destPath = @"YOUR_DIRECTORY\dest.xlsx";

        // Copy the first worksheet (index 0) which contains the pivot
        sourceWorkbook.Worksheets[0].CopyTo(destPath);
```

> **Tips pro:** `CopyTo` membuat workbook baru di balik layar, sehingga Anda tidak perlu menginstansiasi objek `Workbook` lain. Ini menjaga penggunaan memori tetap rendah dan memastikan definisi pivot tetap utuh.

## Langkah 3: Verifikasi Pivot yang Disalin (How to Copy Pivot)

Setelah penyalinan selesai, ada baiknya membuka file baru dan memastikan pivot masih berfungsi. Anda dapat melakukannya secara programatis atau cukup membukanya di Excel.

```csharp
        // Optional: Load the destination workbook to verify
        Workbook destWorkbook = new Workbook(destPath);
        Worksheet copiedSheet = destWorkbook.Worksheets[0];

        // Find the first pivot table on the copied sheet
        PivotTable pivot = copiedSheet.PivotTables[0];

        Console.WriteLine($"Pivot name: {pivot.Name}");
        Console.WriteLine($"Data source range: {pivot.DataSource}");
        Console.WriteLine($"Number of rows in pivot cache: {pivot.CacheDefinition.RecordCount}");
    }
}
```

Menjalankan program mencetak sesuatu seperti:

```
Pivot name: PivotTable1
Data source range: A1:D100
Number of rows in pivot cache: 100
```

Jika Anda melihat nilai‑nilai tersebut, langkah **how to copy pivot** berhasil.

## Langkah 4: (Opsional) Export Pivot Table Data ke DataTable

Kadang Anda membutuhkan angka mentah dari pivot tanpa membuka Excel. Aspose.Cells memungkinkan Anda menarik data pivot ke dalam `DataTable`—sempurna untuk pemrosesan lanjutan atau respons API.

```csharp
        // Export pivot data to a DataTable
        DataTable pivotData = pivot.ExportDataTable(pivot.RowFields[0].Name, 
                                                   pivot.ColumnFields[0].Name,
                                                   true);

        // Display a few rows in the console
        foreach (DataRow row in pivotData.Rows)
        {
            Console.WriteLine(string.Join("\t", row.ItemArray));
        }
```

> **Mengapa Anda mungkin menginginkannya:** Mengekspor memungkinkan Anda **export pivot table** isi ke basis data, payload JSON, atau format lain tanpa menyalin‑tempel manual.

## Langkah 5: Kasus Tepi & Gotchas Umum

### Menyalin ke Workbook yang Sudah Ada

Jika Anda perlu **copy worksheet to workbook** yang sudah berisi sheet lain, gunakan overload yang menerima instance `Workbook` target:

```csharp
        Workbook targetWorkbook = new Workbook(); // empty workbook
        sourceWorkbook.Worksheets[0].CopyTo(targetWorkbook);
        targetWorkbook.Save(@"YOUR_DIRECTORY\combined.xlsx");
```

### Mempertahankan Sumber Data Eksternal

Pivot table yang menarik data dari koneksi eksternal (mis., Power Query) dapat kehilangan tautannya setelah disalin. Dalam kasus seperti itu, setel `pivot.RefreshDataOnOpen = true` sebelum menyimpan:

```csharp
        pivot.RefreshDataOnOpen = true;
```

### File Besar & Kinerja

Untuk file yang lebih besar dari 50 MB, pertimbangkan mengaktifkan `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` untuk mengurangi tekanan memori.

---

![Contoh membuat workbook baru](https://example.com/images/create-new-workbook.png "Buat workbook baru")

*Image alt text: create new workbook – menyalin worksheet dengan pivot table*

---

## Contoh Kerja Lengkap (Semua Langkah Digabung)

Berikut adalah aplikasi console lengkap yang siap dijalankan. Salin‑tempel ke `.csproj` baru dan tekan **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace CopyPivotDemo
{
    class Program
    {
        static void Main()
        {
            // ==============================
            // 1️⃣ Load the source workbook
            // ==============================
            string srcPath = @"YOUR_DIRECTORY\src.xlsx";
            Workbook sourceWorkbook = new Workbook(srcPath);

            // ==============================
            // 2️⃣ Copy the first worksheet (pivot) to a new workbook
            // ==============================
            string destPath = @"YOUR_DIRECTORY\dest.xlsx";
            sourceWorkbook.Worksheets[0].CopyTo(destPath);

            // ==============================
            // 3️⃣ Verify the copied pivot (how to copy pivot)
            // ==============================
            Workbook destWorkbook = new Workbook(destPath);
            Worksheet copiedSheet = destWorkbook.Worksheets[0];
            PivotTable pivot = copiedSheet.PivotTables[0];

            Console.WriteLine($"Pivot name: {pivot.Name}");
            Console.WriteLine($"Data source range: {pivot.DataSource}");
            Console.WriteLine($"Cache rows: {pivot.CacheDefinition.RecordCount}");

            // ==============================
            // 4️⃣ (Optional) Export pivot data
            // ==============================
            if (pivot.RowFields.Count > 0 && pivot.ColumnFields.Count > 0)
            {
                DataTable dt = pivot.ExportDataTable(
                    pivot.RowFields[0].Name,
                    pivot.ColumnFields[0].Name,
                    true);

                Console.WriteLine("\n--- Pivot Data Preview ---");
                foreach (DataRow row in dt.Rows)
                {
                    Console.WriteLine(string.Join("\t", row.ItemArray));
                }
            }

            Console.WriteLine("\nDone! New workbook created at: " + destPath);
        }
    }
}
```

### Hasil yang Diharapkan

- `dest.xlsx` muncul di `YOUR_DIRECTORY`.
- Sheet pertama terlihat persis seperti aslinya, lengkap dengan pivot table.
- Menjalankan console mencetak metadata pivot dan pratinjau data kecil, mengonfirmasi penyalinan berhasil.

---

## Kesimpulan

Anda sekarang tahu cara **create new workbook** dengan menyalin worksheet yang berisi pivot table, cara **copy worksheet to workbook**, dan bahkan cara **export pivot table** data untuk pemrosesan lanjutan. Baik Anda membangun layanan pelaporan, mengotomatisasi distribusi Excel, atau hanya membutuhkan cara cepat untuk menduplikasi pivot, langkah‑langkah di atas memberikan solusi yang andal dan siap produksi.

**Langkah selanjutnya** yang mungkin Anda jelajahi:

- Gabungkan beberapa sheet (gunakan `CopyTo` berulang kali) – sempurna untuk mengemas laporan lengkap.
- Sesuaikan pengaturan refresh cache pivot ketika data sumber berubah.
- Gunakan teknik **how to copy sheet** untuk menduplikasi chart, gambar, atau modul VBA.
- Menyelami `WorkbookDesigner` milik Aspose.Cells untuk pembuatan laporan berbasis templat.

Cobalah, sesuaikan jalur, dan lihat betapa mudahnya mengirim workbook bersih yang siap pivot. Ada pertanyaan tentang kasus tepi atau lisensi? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}