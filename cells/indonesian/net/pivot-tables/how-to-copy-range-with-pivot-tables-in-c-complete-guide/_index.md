---
category: general
date: 2026-03-29
description: Pelajari cara menyalin rentang, menyalin tabel pivot, cara menyimpan
  workbook, dan cara memuat workbook di C#. Pindahkan tabel pivot dengan mudah menggunakan
  kode langkah demi langkah.
draft: false
keywords:
- how to copy range
- copy pivot tables
- how to save workbook
- how to load workbook
- move pivot table
language: id
og_description: Cara menyalin rentang, menyalin tabel pivot, cara menyimpan workbook,
  dan cara memuat workbook dalam C#. Pindahkan tabel pivot dengan mudah menggunakan
  kode yang jelas.
og_title: Cara menyalin rentang dengan tabel pivot di C# – Panduan Lengkap
tags:
- C#
- Aspose.Cells
- Excel automation
title: Cara menyalin rentang dengan tabel pivot di C# – Panduan Lengkap
url: /id/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin rentang dengan tabel pivot di C# – Panduan Lengkap

Pernah bertanya-tanya **cara menyalin rentang** yang berisi tabel pivot tanpa memutus tautan ke data sumbernya? Anda bukan satu-satunya. Dalam banyak proyek dunia nyata saya pernah mengalami masalah ini—file Excel datang dengan tabel pivot yang canggih, dan kebutuhannya adalah memindahkannya atau menduplikasi data ke tempat lain.  

Berita baiknya? Solusinya cukup sederhana setelah Anda mengetahui **cara memuat workbook**, membuat salinan, dan kemudian **cara menyimpan workbook** lagi. Dalam tutorial ini kami akan membahas seluruh proses, termasuk cara **menyalin tabel pivot**, dan bahkan tip cepat tentang **memindahkan tabel pivot** jika Anda membutuhkannya di tempat lain dalam lembar yang sama.

Pada akhir panduan ini Anda akan memiliki potongan kode C# yang berfungsi penuh yang:

1. Memuat file Excel yang sudah ada.  
2. Menyalin sebuah rentang (termasuk tabel pivot) ke lokasi baru.  
3. Menyimpan workbook yang telah dimodifikasi ke file baru.

Tanpa skrip eksternal, tanpa pengaturan manual—hanya kode yang bersih dan dapat diulang.

---

## Prasyarat

- **.NET 6+** (versi terbaru apa pun dapat digunakan).  
- **Aspose.Cells for .NET** – perpustakaan yang menyediakan `Workbook`, `WorksheetCopyOptions`, dll. Anda dapat menginstalnya melalui NuGet:

```bash
dotnet add package Aspose.Cells
```

- Workbook input (`input.xlsx`) yang sudah berisi tabel pivot pada rentang `A1:G20`.  
- Pemahaman dasar tentang C# dan Visual Studio (atau IDE favorit Anda).

> **Pro tip:** Jika Anda menggunakan perpustakaan Excel yang berbeda (mis., EPPlus), konsepnya tetap sama—cukup ganti panggilan API.

---

## Langkah 1 – Cara memuat workbook (Pengaturan Utama)

Sebelum kita dapat menyalin apa pun, kita perlu memuat file Excel ke dalam memori.

```csharp
using Aspose.Cells;

// Step 1: Load the source workbook
var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// Grab the first worksheet – this is where our pivot lives
var sourceWorksheet = sourceWorkbook.Worksheets[0];
```

**Mengapa ini penting:**  
Memuat workbook memberi Anda model objek yang dapat dimanipulasi. Tanpa `cara memuat workbook` dengan benar, operasi penyalinan selanjutnya akan melemparkan pengecualian *FileNotFound* atau *InvalidOperation*.

> **Watch out:** Jika file besar, pertimbangkan menggunakan `LoadOptions` dengan `MemorySetting` untuk mengontrol penggunaan memori.

---

## Langkah 2 – Cara menyalin rentang (termasuk pivot)

Sekarang hadir bintang utama: menyalin rentang yang berisi tabel pivot. Metode `CopyRange`, dikombinasikan dengan `WorksheetCopyOptions`, melakukan pekerjaan berat.

```csharp
// Step 2: Copy a range that includes a pivot table to a new location
sourceWorksheet.CopyRange(
    "A1:G20",                                   // Source range
    new WorksheetCopyOptions { CopyPivotTables = true }, // Ensure pivot tables travel with the data
    sourceWorksheet,                           // Destination worksheet (same sheet in this case)
    "A25");                                     // Upper‑left corner of the destination
```

**Mengapa kami mengatur `CopyPivotTables = true`:**  
Secara default, menyalin rentang hanya memindahkan sel mentah. Cache pivot tetap di belakang, dan pivot yang disalin menjadi tabel statis. Mengatur `CopyPivotTables` mempertahankan koneksi langsung, sehingga pivot yang diduplikasi tetap dapat menyegarkan ketika data sumbernya berubah.

**Kasus tepi:**  
Jika rentang tujuan tumpang tindih dengan sumber, Aspose.Cells akan melempar `ArgumentException`. Selalu pilih target yang tidak tumpang tindih, atau buat lembar kerja baru terlebih dahulu.

---

## Langkah 3 – Cara menyimpan workbook (Menyimpan perubahan)

Setelah penyalinan, Anda ingin menulis perubahan kembali ke disk. Di sinilah **cara menyimpan workbook** berperan.

```csharp
// Step 3: Save the modified workbook to a new file
sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

**Apa yang terjadi di balik layar:**  
`Save` menyerialisasi workbook dalam memori, termasuk tabel pivot yang baru disalin, ke dalam paket `.xlsx` standar. Jika Anda membutuhkan format lain (CSV, PDF, dll.), cukup ubah ekstensi file atau gunakan overload yang menerima `SaveFormat`.

> **Tip:** Gunakan `Workbook.Save(string, SaveOptions)` jika Anda perlu melindungi file dengan kata sandi atau mengatur opsi ekspor lainnya.

---

## Contoh Kerja Lengkap

Menggabungkan semuanya, berikut program lengkap yang siap dijalankan:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ How to load workbook
        var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
        var sourceWorksheet = sourceWorkbook.Worksheets[0];

        // 2️⃣ How to copy range (including pivot tables)
        sourceWorksheet.CopyRange(
            "A1:G20",
            new WorksheetCopyOptions { CopyPivotTables = true },
            sourceWorksheet,
            "A25");

        // 3️⃣ How to save workbook
        sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");

        Console.WriteLine("✅ Range copied and workbook saved successfully!");
    }
}
```

**Hasil yang diharapkan:**  
Buka `output.xlsx`. Anda akan melihat tabel pivot asli masih berada di `A1:G20`, dan salinan identik yang berfungsi penuh mulai dari `A25`. Kedua pivot mengacu pada data sumber yang sama, sehingga menyegarkan salah satu akan memperbarui yang lainnya.

---

## Pertanyaan yang Sering Diajukan & Variasi

### Apakah saya dapat **memindahkan tabel pivot** alih-alih menyalinnya?

Tentu saja. Setelah menyalin, cukup bersihkan rentang asli (atau gunakan `sourceWorksheet.Cells.ClearRange(0, 0, 19, 6)`) dan kemudian ganti nama rentang tujuan jika diperlukan. Ini secara efektif “memindahkan” pivot.

### Bagaimana jika pivot menggunakan sumber data eksternal?

`CopyPivotTables = true` hanya menyalin definisi pivot, bukan koneksi eksternal itu sendiri. Pastikan workbook target memiliki akses ke sumber data yang sama, atau buat kembali koneksi setelah penyalinan.

### Bagaimana cara menyalin ke **lembar kerja yang berbeda**?

Cukup berikan objek lembar kerja tujuan alih-alih `sourceWorksheet`:

```csharp
var destWorksheet = sourceWorkbook.Worksheets.Add("CopiedPivot");
sourceWorksheet.CopyRange("A1:G20", new WorksheetCopyOptions { CopyPivotTables = true }, destWorksheet, "A1");
```

### Apakah ada cara menyalin **beberapa rentang** sekaligus?

Anda dapat memanggil `CopyRange` berulang kali atau menggunakan `CopyRows`/`CopyColumns` untuk blok yang lebih besar. Melakukan loop atas daftar string alamat merupakan pendekatan yang bersih.

---

## Kesalahan Umum & Tips Pro

- **Ukuran cache pivot:** Cache pivot yang besar dapat memperbesar ukuran workbook. Jika Anda hanya membutuhkan data yang ditampilkan, pertimbangkan `CopyPivotTables = false` dan kemudian gunakan `PivotTable.RefreshData()` pada tujuan.  
- **Path file:** Gunakan `Path.Combine` untuk menghindari pemisah yang ditulis keras, terutama pada .NET lintas platform.  
- **Kinerja:** Untuk workbook yang sangat besar, bungkus penyalinan dalam `using (var stream = new MemoryStream())` dan simpan ke stream terlebih dahulu, kemudian tulis ke disk. Ini mengurangi beban I/O.

---

## Kesimpulan

Anda kini tahu **cara menyalin rentang** yang berisi tabel pivot, cara **menyalin tabel pivot**, dan langkah tepat untuk **cara memuat workbook** serta **cara menyimpan workbook** setelah operasi. Baik Anda perlu **memindahkan tabel pivot** dalam lembar yang sama atau ke lembar kerja lain, pola tetap sama—muat, salin dengan opsi yang tepat, dan simpan.

Cobalah dengan file Anda sendiri, ubah alamat tujuan, dan bereksperimen dengan konfigurasi pivot yang berbeda. Semakin banyak Anda mencoba, semakin percaya diri Anda dalam mengotomatisasi tugas Excel di C#.

---

![Diagram yang menunjukkan rentang sumber A1:G20 disalin ke A25 dalam lembar kerja yang sama – cara menyalin rentang dengan tabel pivot](/images/how-to-copy-range-diagram.png "cara menyalin rentang dengan tabel pivot")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}