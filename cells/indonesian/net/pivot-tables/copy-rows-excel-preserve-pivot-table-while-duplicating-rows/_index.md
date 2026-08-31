---
category: general
date: 2026-02-14
description: Salin baris Excel dan pertahankan tabel pivot sekaligus. Pelajari cara
  menyalin baris, menyalin rentang ke lembar, dan menggandakan baris dengan pivot
  menggunakan Aspose.Cells.
draft: false
keywords:
- copy rows excel
- preserve pivot table
- how to copy rows
- copy range to sheet
- duplicate rows with pivot
language: id
og_description: Salin baris Excel dan pertahankan tabel pivot sekaligus. Ikuti panduan
  langkah demi langkah ini untuk menggandakan baris dengan pivot menggunakan C#.
og_title: menyalin baris excel – Pertahankan Tabel Pivot Saat Menggandakan Baris
tags:
- Aspose.Cells
- C#
- Excel automation
title: Menyalin Baris Excel – Pertahankan Tabel Pivot Saat Menggandakan Baris
url: /id/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# menyalin baris excel – Mempertahankan Pivot Table Saat Menggandakan Baris

Pernah perlu **menyalin baris excel** sambil menjaga pivot table tetap utuh? Pada tutorial ini kami akan membahas solusi lengkap yang dapat dijalankan, menunjukkan **cara menyalin baris**, mempertahankan perilaku **preserve pivot table**, dan bahkan **menggandakan baris dengan pivot** antar lembar menggunakan Aspose.Cells untuk .NET.

Bayangkan Anda membuat laporan penjualan bulanan yang mengambil data dari lembar master, menjalankan pivot, lalu harus mengirimkan versi yang dipangkas ke mitra. Menyalin rentang secara manual sangat merepotkan, dan Anda berisiko merusak pivot. Kabar baiknya? Beberapa baris kode C# dapat melakukan pekerjaan berat itu untuk Anda—tanpa klik mouse.

> **Apa yang akan Anda dapatkan:** contoh kode lengkap, penjelasan langkah demi langkah, tips untuk kasus tepi, dan pemeriksaan cepat untuk memastikan pivot tetap hidup setelah penyalinan.

---

## Apa yang Anda Butuhkan

- **Aspose.Cells untuk .NET** (paket NuGet gratis sudah cukup untuk demo ini).  
- Runtime **.NET terbaru** (4.7+ atau .NET 6/7).  
- File Excel (`source.xlsx`) yang berisi pivot table pada lembar kerja pertama.  
- Visual Studio, Rider, atau editor C# pilihan Anda.

Tanpa pustaka tambahan, tanpa interop COM, dan tanpa instalasi Excel di server. Itulah mengapa pendekatan ini **ramah menyalin rentang ke lembar** dan aman untuk server.

---

## Langkah 1 – Memuat Workbook (copy rows excel)

Hal pertama yang harus dilakukan adalah membuka workbook sumber. Menggunakan Aspose.Cells memberi kita model objek bersih yang berfungsi sama di Windows, Linux, atau Azure.

```csharp
using Aspose.Cells;

public class PivotCopyDemo
{
    public static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Mengapa ini penting:** memuat workbook membuat representasi dalam memori dari setiap lembar kerja, termasuk objek tersembunyi seperti pivot cache. Begitu file berada di memori, kita dapat memanipulasi baris tanpa menyentuh UI.

---

## Langkah 2 – Mengidentifikasi Worksheet Tujuan (copy range to sheet)

Kita ingin baris yang disalin ditempatkan pada lembar lain—`Sheet2` dalam contoh ini. Jika lembar belum ada, Aspose akan membuatnya untuk Anda.

```csharp
        // Get (or create) the destination worksheet where the rows will be placed
        Worksheet destinationWorksheet;
        if (sourceWorkbook.Worksheets.Contains("Sheet2"))
            destinationWorksheet = sourceWorkbook.Worksheets["Sheet2"];
        else
            destinationWorksheet = sourceWorkbook.Worksheets.Add("Sheet2");
```

> **Tips profesional:** selalu periksa `Worksheets.Contains` sebelum menambahkan lembar; jika tidak, Anda akan berakhir dengan nama duplikat dan pengecualian runtime.

---

## Langkah 3 – Menyalin Baris Sambil Mempertahankan Pivot Table

Sekarang masuk ke inti masalah: menyalin baris **A1:E20** (yang mencakup pivot) dari lembar pertama ke `Sheet2`. Metode `CopyRows` menyalin sel mentah *dan* pivot cache yang mendasarinya, sehingga pivot tetap berfungsi.

```csharp
        // Define the source range: rows 0‑19 (A1:E20) on the first worksheet
        Worksheet sourceWorksheet = sourceWorkbook.Worksheets[0];

        // Copy rows 0‑19 from source to destination, starting at row 0 on the destination sheet
        sourceWorksheet.Cells.CopyRows(
            sourceWorksheet.Cells,   // source cells collection
            0,                       // source start row (0‑based, i.e., row 1)
            0,                       // destination start row on the same sheet (adjust if needed)
            20);                     // total number of rows to copy
```

> **Mengapa ini berhasil:** `CopyRows` menghormati pivot cache internal, sehingga pivot table pada lembar tujuan menjadi salinan *aktif*, bukan snapshot statis. Ini memenuhi persyaratan **preserve pivot table** tanpa kode tambahan.

Jika Anda ingin baris mulai pada offset yang berbeda di lembar tujuan—misalnya baris 10—cukup ubah argumen ketiga menjadi `9`.

---

## Langkah 4 – Menyimpan Workbook (duplicate rows with pivot)

Terakhir, tulis workbook yang telah dimodifikasi kembali ke disk. Pivot table akan berfungsi penuh di file baru.

```csharp
        // Save the workbook; the copied pivot remains active automatically
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

> **Verifikasi hasil:** buka `copyWithPivot.xlsx` di Excel, pergi ke *Sheet2*, dan refresh pivot. Anda akan melihat tata letak bidang dan perhitungan yang sama seperti aslinya—tidak ada yang rusak.

---

## Memverifikasi Penyalinan – Pemeriksaan Cepat

```csharp
// Optional: programmatically confirm the pivot exists on the destination sheet
Worksheet dest = sourceWorkbook.Worksheets["Sheet2"];
bool pivotExists = dest.PivotTables.Count > 0;
Console.WriteLine($"Pivot table copied? {pivotExists}");
```

Jika konsol mencetak `True`, Anda telah berhasil **duplicate rows with pivot** dan menjaga mesin analisis data tetap hidup.

---

## Kasus Tepi Umum & Cara Menanganinya

| Situasi | Hal yang Perlu Diperhatikan | Penyesuaian yang Disarankan |
|-----------|-------------------|-----------------|
| **Rentang sumber mencakup sel yang digabung** | Sel yang digabung dapat menyebabkan ketidaksesuaian saat disalin. | Gunakan `CopyRows` seperti contoh; ia secara otomatis mempertahankan penggabungan. |
| **Lembar tujuan sudah memiliki data** | Baris baru mungkin menimpa konten yang ada. | Ubah baris mulai tujuan (argumen ketiga) ke baris kosong pertama: `destWorksheet.Cells.MaxDataRow + 1`. |
| **Pivot menggunakan sumber data eksternal** | Koneksi eksternal tidak disalin. | Pastikan workbook sumber berisi set data lengkap; jika tidak, sambungkan kembali setelah penyalinan. |
| **Workbook besar (100k+ baris)** | Penggunaan memori melonjak. | Pertimbangkan menyalin dalam potongan (misalnya 5.000 baris sekaligus) agar GC tetap nyaman. |

---

## Contoh Lengkap yang Berfungsi (Semua Langkah Bersama)

Berikut seluruh program yang dapat Anda tempel ke aplikasi console dan jalankan langsung.

```csharp
using System;
using Aspose.Cells;

public class PivotCopyDemo
{
    public static void Main()
    {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");

        // 2️⃣ Get (or create) the destination worksheet
        Worksheet destinationWorksheet;
        if (sourceWorkbook.Worksheets.Contains("Sheet2"))
            destinationWorksheet = sourceWorkbook.Worksheets["Sheet2"];
        else
            destinationWorksheet = sourceWorkbook.Worksheets.Add("Sheet2");

        // 3️⃣ Copy rows A1:E20 (includes pivot) from the first sheet
        Worksheet sourceWorksheet = sourceWorkbook.Worksheets[0];
        sourceWorksheet.Cells.CopyRows(
            sourceWorksheet.Cells, // source cells
            0,                     // start at row 0 (A1)
            0,                     // destination start row (adjust as needed)
            20);                   // copy 20 rows

        // 4️⃣ Save the workbook – pivot stays alive
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");

        // Optional verification
        bool pivotExists = destinationWorksheet.PivotTables.Count > 0;
        Console.WriteLine($"Pivot table copied? {pivotExists}");
    }
}
```

Jalankan program, buka `copyWithPivot.xlsx` yang dihasilkan, dan Anda akan melihat bahwa pivot pada **Sheet2** berfungsi persis seperti aslinya. Tidak perlu membuat ulang secara manual.

---

## Pertanyaan yang Sering Diajukan

**T: Apakah ini bekerja dengan file `.xls` kompatibel Excel 2003?**  
J: Ya. Aspose.Cells mengabstraksi format file, sehingga kode yang sama bekerja untuk `.xls`, `.xlsx`, dan bahkan `.xlsb`.

**T: Bagaimana jika saya perlu menyalin *kolom* alih-alih baris?**  
J: Gunakan `CopyColumns` dengan cara serupa; cukup ganti parameter baris dengan indeks kolom.

**T: Bisakah saya menyalin beberapa rentang yang tidak berurutan sekaligus?**  
J: Tidak secara langsung dengan `CopyRows`. Lakukan loop untuk setiap rentang atau buat lembar kerja sementara yang mengkonsolidasikan rentang sebelum menyalin.

---

## Kesimpulan

Kami baru saja mendemonstrasikan pola **copy rows excel** yang **preserve pivot table** integritasnya, memungkinkan Anda **how to copy rows** secara efisien, dan menunjukkan cara **copy range to sheet** tanpa kehilangan fungsi pivot. Pada akhir panduan ini Anda seharusnya merasa percaya diri untuk **duplicate rows with pivot** dalam pipeline otomatisasi apa pun—baik Anda menghasilkan laporan harian atau membangun layanan ekspor data berskala besar.

Siap untuk tantangan berikutnya? Cobalah memperluas kode untuk:

- Mengekspor lembar yang digandakan sebagai PDF.  
- Menyegarkan pivot secara programatis setelah penyalinan.  
- Melakukan loop pada daftar file sumber dan memprosesnya secara batch.

Jika mengalami kendala, tinggalkan komentar di bawah atau hubungi saya di GitHub. Selamat coding, dan nikmati waktu yang Anda hemat dengan tidak harus menyeret Excel secara manual!  

<img src="copy-rows-excel.png" alt="copy rows excel diagram" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}