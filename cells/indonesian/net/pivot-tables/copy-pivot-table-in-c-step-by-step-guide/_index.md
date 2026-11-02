---
category: general
date: 2026-03-18
description: Salin tabel pivot di C# dengan Aspose.Cells. Pelajari cara menyalin rentang
  Excel, menduplikasi pivot Excel, menyalin rentang ke lembar baru, dan menyalin pivot
  ke lembar dalam hitungan menit.
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: id
og_description: Salin tabel pivot di C# menggunakan Aspose.Cells. Pelajari cara menduplikasi
  pivot Excel, menyalin rentang Excel ke lokasi baru, dan menyalin pivot ke lembar
  dengan contoh kode lengkap.
og_title: Menyalin tabel pivot di C# – Panduan Pemrograman Lengkap
tags:
- Aspose.Cells
- C#
- Excel automation
title: Salin tabel pivot di C# – Panduan Langkah demi Langkah
url: /id/net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salin tabel pivot di C# – Panduan Pemrograman Lengkap

Pernahkah Anda perlu **menyalin tabel pivot** dari satu bagian workbook ke bagian lain, tetapi tidak yakin cara melakukannya tanpa kehilangan koneksi data yang mendasarinya? Anda tidak sendirian. Banyak pengembang mengalami kendala ini saat mengotomatisasi laporan Excel, terutama ketika pivot berada di dalam blok data yang lebih besar. Kabar baiknya? Dengan Aspose.Cells Anda dapat menyalin tabel pivot **tepat seperti tampilannya**, dan Anda juga akan belajar cara **menyalin rentang excel**, **menggandakan pivot excel**, serta bahkan **menyalin pivot ke sheet** hanya dengan beberapa baris kode C#.

Dalam tutorial ini kami akan membahas skenario dunia nyata: memindahkan pivot yang menempati *A1:J20* ke area baru *M1:V20* pada lembar kerja yang sama. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan, memahami mengapa setiap langkah penting, dan tahu cara menyesuaikan kode untuk rentang lain atau bahkan lembar kerja terpisah. Tidak perlu dokumen eksternal—semuanya ada di sini.

---

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- **Aspose.Cells for .NET** (versi 23.9 atau lebih baru). Anda dapat mengunduhnya via NuGet: `Install-Package Aspose.Cells`.
- Lingkungan pengembangan C# dasar (Visual Studio 2022, Rider, atau VS Code dengan ekstensi C#).
- File Excel (`source.xlsx`) yang berisi tabel pivot dalam rentang *A1:J20*.

Itu saja. Jika Anda nyaman membuat aplikasi konsol, Anda siap melanjutkan.

---

## Cara menyalin tabel pivot di Aspose.Cells

Inti solusi adalah satu panggilan ke `Worksheet.Cells.CopyRange`. Metode ini tidak hanya menyalin nilai sel mentah tetapi juga mempertahankan tabel pivot, diagram, dan objek kaya lainnya secara otomatis. Mari kita uraikan.

### Langkah 1: Muat workbook sumber

Pertama kita perlu membawa workbook ke memori.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Mengapa ini penting:** Memuat workbook membuat representasi dalam memori yang dapat dimanipulasi Aspose.Cells tanpa meluncurkan Excel. Prosesnya cepat, thread‑safe, dan dapat dijalankan di server.

### Langkah 2: Ambil lembar kerja pertama

Sebagian besar contoh menggunakan lembar pertama, tetapi Anda dapat menargetkan indeks atau nama apa pun.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **Tip:** Jika Anda perlu **menyalin pivot ke sheet** bukan ke lembar yang sama, cukup ubah referensi `worksheet` ke objek `Worksheet` lain.

### Langkah 3: Definisikan rentang sumber dan target

Kita akan menggunakan struktur `CellArea` untuk mendeskripsikan blok yang akan dipindahkan.

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **Penjelasan:** Indeks baris dan kolom dimulai dari nol. Kolom 0 = **A**, kolom 12 = **M**, dan seterusnya. Sesuaikan angka-angka ini jika pivot Anda berada di tempat lain.

### Langkah 4: Lakukan operasi penyalinan

Sekarang magis terjadi. Menetapkan parameter boolean terakhir ke `true` memberi tahu Aspose.Cells untuk menyalin semua objek—termasuk pivot.

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **Mengapa `true`?** Flag tersebut menunjukkan “salin semua objek”. Jika Anda mengaturnya ke `false`, hanya nilai sel biasa yang akan dipindahkan, dan pivot akan hilang.

### Langkah 5: Simpan workbook

Akhirnya, tulis workbook yang telah dimodifikasi kembali ke disk.

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **Hasil:** `copy-pivot.xlsx` kini berisi pivot asli di *A1:J20* **dan** salinan identik di *M1:V20*. Buka file tersebut di Excel untuk memverifikasi bahwa kedua pivot berfungsi dan mempertahankan koneksi data mereka.

---

## Menyalin rentang Excel ke lokasi baru – variasi cepat

Terkadang Anda hanya perlu **menyalin rentang excel** tanpa memperhatikan pivot. Metode `CopyRange` yang sama dapat melakukannya; cukup set argumen terakhir ke `false`.

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **Kapan digunakan:** Jika Anda memindahkan data mentah untuk lembar perhitungan sementara, menonaktifkan penyalinan objek menghemat memori dan mempercepat proses.

---

## Menggandakan pivot excel di beberapa lembar

Bagaimana jika Anda ingin **menggandakan pivot excel** pada lembar kerja yang berbeda? Polanya tetap sama; Anda hanya perlu merujuk ke `Worksheet` lain untuk tujuan.

```csharp
// Assume we have a second sheet already created
Worksheet destSheet = sourceWorkbook.Worksheets.Add("PivotCopy");

// Copy the pivot (and its data source) to the new sheet starting at A1
destSheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    0, 0, // destination at A1
    true);
```

> **Kasus tepi:** Jika pivot sumber menggunakan tabel yang berada di lembar asal, Aspose.Cells juga akan menyalin definisi tabel tersebut, memastikan pivot baru berfungsi langsung.

---

## Kesalahan umum dan cara menghindarinya

| Kesalahan | Mengapa terjadi | Solusi |
|-----------|----------------|--------|
| **Pivot kehilangan cache-nya** | Menggunakan `CopyRange` dengan `false` atau rutinitas salin khusus yang mengabaikan objek. | Selalu berikan `true` ketika Anda memerlukan pivot itu sendiri. |
| **Sel target sudah berisi data** | Menimpa secara diam‑diam, berpotensi merusak formula yang ada. | Bersihkan area target terlebih dahulu: `worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **Rentang sumber tidak mencakup seluruh pivot** | Tabel pivot mencakup baris/kolom lebih banyak dari yang Anda duga (misalnya baris tersembunyi). | Gunakan `worksheet.PivotTables[0].DataRange` untuk secara programatis mengambil batas yang tepat. |
| **Menyalin antar workbook** | `CopyRange` hanya berfungsi dalam workbook yang sama. | Gunakan `sourceWorksheet.Cells.CopyRange` ke rentang sementara, lalu `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` |

---

## Output yang diharapkan & verifikasi

Setelah menjalankan program:

1. Buka `copy-pivot.xlsx`.
2. Anda akan melihat dua tabel pivot identik—satu di **A1:J20**, lainnya di **M1:V20**.
3. Refresh salah satu pivot; keduanya harus mencerminkan data dasar yang sama.
4. Jika Anda menggandakan ke lembar lain, lembar baru akan berisi salinan yang berfungsi.

Cara cepat memverifikasi lewat kode:

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

---

## Pro tip: Otomatisasi deteksi rentang

Menuliskan `CellArea` secara manual cocok untuk laporan statis, tetapi kode produksi sering memerlukan pencarian pivot secara dinamis.

```csharp
// Find the first pivot table on the sheet
PivotTable pt = worksheet.PivotTables[0];
CellArea ptRange = pt.DataRange;

// Use the detected range for copying
worksheet.Cells.CopyRange(
    ptRange.StartRow, ptRange.StartColumn,
    ptRange.EndRow, ptRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    true);
```

> **Mengapa repotkan?** Ini membuat solusi Anda tahan terhadap perubahan tata letak—tidak ada lagi error “Ups, pivot pindah ke B2”.

---

![copy pivot table example](copy-pivot.png){alt="copy pivot table example"}

*Screenshot (placeholder) menampilkan pivot asli di sebelah kiri dan yang digandakan di sebelah kanan.*

---

## Ringkasan

Kami baru saja membahas cara **menyalin tabel pivot** di C# menggunakan Aspose.Cells, mengeksplorasi cara **menyalin rentang excel**, **menggandakan pivot excel**, dan bahkan **menyalin pivot ke sheet** lintas lembar kerja. Poin penting yang harus diingat:

- Gunakan `Worksheet.Cells.CopyRange` dengan flag `true` untuk mempertahankan objek kaya.
- Definisikan objek `CellArea` sumber dan target dengan indeks berbasis nol.
- Sesuaikan lembar kerja tujuan jika Anda perlu **menyalin pivot ke sheet**.
- Perhatikan kasus tepi seperti data yang sudah ada, baris tersembunyi, dan skenario lintas workbook.

---

## Apa selanjutnya?

- **Penemuan pivot dinamis**: Buat helper yang memindai workbook untuk semua pivot dan menyalinnya secara otomatis.
- **Ekspor ke PDF/HTML**: Setelah menyalin, Anda mungkin ingin merender lembar ke format laporan—Aspose.Cells juga mendukungnya.
- **Optimasi performa**: Untuk workbook besar, pertimbangkan menonaktifkan perhitungan sebelum menyalin dan mengaktifkannya kembali setelahnya.

Silakan bereksperimen: ubah koordinat target, salin ke workbook baru, atau bahkan loop melalui beberapa lembar kerja untuk membuat laporan terpusat. Kemungkinannya tak terbatas, dan dengan fondasi yang kini Anda miliki, Anda dapat menyesuaikan kode untuk hampir semua tugas otomasi Excel.

Selamat coding, semoga pivot Anda selalu sinkron dengan sempurna!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}