---
category: general
date: 2026-06-27
description: Salin tabel pivot ke lembar lain di C# menggunakan Aspose.Cells. Pelajari
  langkah demi langkah cara mempertahankan data dan format pivot.
draft: false
keywords:
- copy pivot table to another sheet
- Aspose.Cells copy pivot
- Excel pivot duplication
- preserve pivot formatting
- copy range with pivot
language: id
og_description: Salin tabel pivot ke lembar lain di C# dengan Aspose.Cells. Tutorial
  ini menunjukkan secara tepat cara menduplikasi pivot sambil mempertahankan formatnya
  tetap utuh.
og_title: Salin Tabel Pivot ke Lembar Lain – Panduan Lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table to another sheet in C# using Aspose.Cells. Learn step‑by‑step
    how to preserve pivot data and formatting.
  headline: Copy Pivot Table to Another Sheet – Complete C# Guide
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Salin Tabel Pivot ke Lembar Lain – Panduan Lengkap C#
url: /id/net/pivot-tables/copy-pivot-table-to-another-sheet-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salin Tabel Pivot ke Lembar Lain – Panduan Lengkap C# 

Pernah perlu **menyalin tabel pivot ke lembar lain** tetapi khawatir Anda akan kehilangan slicer, bidang terhitung, atau pemformatan? Anda tidak sendirian. Banyak pengembang mengalami masalah ini saat mengotomatiskan laporan Excel, dan frustrasinya nyata. Dalam panduan ini kami akan membahas solusi bersih, end‑to‑end yang **mempertahankan tabel pivot** persis seperti yang terlihat.

Kami akan menggunakan **Aspose.Cells for .NET**, sebuah perpustakaan kuat yang memungkinkan Anda memanipulasi file Excel tanpa harus membuka Excel itu sendiri. Pada akhir tutorial ini Anda akan memiliki potongan kode C# siap‑jalankan yang menyalin tabel pivot dari satu lembar kerja ke lembar lain, menjaga semua koneksi data yang mendasarinya tetap utuh.

## Apa yang Dibahas dalam Tutorial Ini

- Menyiapkan proyek .NET dan menambahkan paket NuGet Aspose.Cells.  
- Memuat workbook yang sudah ada yang sudah berisi tabel pivot.  
- Mendefinisikan baik rentang sumber (pivot asli) maupun rentang tujuan pada lembar yang berbeda.  
- Menggunakan `CopyOptions` untuk **mempertahankan tabel pivot** saat menyalin.  
- Menyimpan hasil dan memverifikasi bahwa pivot berfungsi di lokasi barunya.  

Tanpa alat eksternal, tanpa salin‑tempel manual, dan tanpa sihir tersembunyi—hanya kode sederhana yang dapat Anda masukkan ke dalam aplikasi konsol C# apa pun atau layanan.

> **Mengapa Anda harus peduli:** Mengotomatiskan duplikasi pivot menghemat jam kerja manual, terutama dalam pipeline pelaporan malam hari di mana puluhan workbook membutuhkan struktur pivot yang identik di beberapa lembar.

---

## Langkah 1: Siapkan Proyek dan Tambahkan Aspose.Cells

Hal pertama yang harus dilakukan. Jika Anda belum melakukannya, buat proyek konsol .NET baru:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
```

Sekarang tambahkan paket Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

> **Tip pro:** Gunakan versi stabil terbaru (per Juni 2026 v23.12). Versi ini mencakup perbaikan bug untuk penanganan `CopyPivotTable`.

## Langkah 2: Muat Workbook dan Akses Worksheet

Buka workbook yang berisi tabel pivot sumber. Dalam kebanyakan skenario dunia nyata file berada di drive bersama, tetapi untuk demo ini kami mengasumsikan berada di folder lokal bernama `YOUR_DIRECTORY`.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook containing the source pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Step 2: Access the first worksheet (source sheet)
        Worksheet sourceSheet = workbook.Worksheets[0];

        // We'll also create (or reference) a destination sheet
        Worksheet destSheet = workbook.Worksheets.Add("CopyDestination");
```

Di sini kami membuat lembar baru bernama **CopyDestination** tempat pivot akan ditempatkan. Jika Anda sudah memiliki lembar target, cukup ambil dengan indeks atau nama.

## Langkah 3: Definisikan Rentang Sumber dan Tujuan

Tabel pivot berada di dalam blok persegi panjang sel. Anda harus memberi tahu Aspose.Cells blok mana yang akan disalin. Dalam contoh ini pivot menempati baris 0‑20 dan kolom 0‑10 (indeks berbasis nol).

```csharp
        // Step 3: Define the source range that includes the pivot table (rows 0‑20, columns 0‑10)
        CellArea sourceRange = new CellArea(0, 0, 20, 10);

        // Step 4: Define the destination start cell (row 30, column 0) on the destination sheet
        // and calculate the target area size to match the source dimensions
        CellArea destinationRange = new CellArea(
            30,                                 // start row on destination sheet
            0,                                  // start column
            30 + sourceRange.RowCount - 1,     // end row (same height as source)
            sourceRange.ColumnCount - 1        // end column (same width as source)
        );
```

Perhatikan bagaimana kami menghitung baris akhir dan kolom secara dinamis. Dengan cara ini, bahkan jika Anda kemudian mengubah ukuran rentang sumber, tujuan akan menyesuaikan secara otomatis.

## Langkah 4: Lakukan Penyalinan Sambil Mempertahankan Pivot

Sekarang keajaiban terjadi. Dengan mengirimkan objek `CopyOptions` dengan `CopyPivotTable = true`, Aspose.Cells tahu untuk menjaga definisi tabel pivot tetap utuh.

```csharp
        // Step 5: Copy the range, preserving the pivot table
        destSheet.Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTable = true }
        );
```

Di balik layar, Aspose.Cells membuat ulang cache pivot, menyegarkan referensi sumber data, dan menerapkan kembali semua pemformatan. Ini adalah **duplikasi pivot Excel** yang Anda cari.

## Langkah 5: Simpan dan Verifikasi Hasil

Akhirnya, tulis kembali workbook ke disk. Anda dapat menjaga file asli tetap tidak tersentuh dengan menyimpan ke nama baru.

```csharp
        // Step 6: Save the workbook with the copied pivot table
        workbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

        // Optional: open the file automatically (Windows only)
        System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
        {
            FileName = "YOUR_DIRECTORY/copy-pivot.xlsx",
            UseShellExecute = true
        });
    }
}
```

Buka `copy-pivot.xlsx` yang dihasilkan dan Anda akan melihat tabel pivot terduplikasi dengan sempurna pada lembar **CopyDestination**, lengkap dengan slicer, bidang terhitung, dan pemformatan. Sumber data yang mendasarinya masih mengarah ke tabel asli, sehingga penyegaran berfungsi persis seperti sebelumnya.

> **Bagaimana jika pivot sumber mencakup rentang dinamis?**  
> Gunakan `Worksheet.PivotTables[0].CacheDefinition.SourceData` untuk mengambil batas sebenarnya, lalu bangun `sourceRange` dari informasi tersebut. Ini menangani kasus di mana baris atau kolom dapat berkembang seiring waktu.

## Bonus: Pertahankan Pemformatan Pivot di Seluruh Penyalinan

Kadang penyalinan default kehilangan pemformatan bersyarat atau format angka khusus. Untuk menghindari hal itu, perpanjang `CopyOptions`:

```csharp
        var options = new CopyOptions
        {
            CopyPivotTable = true,
            CopyFormatting = true,      // copies cell styles, colors, fonts
            CopyConditionalFormatting = true
        };
        destSheet.Cells.CopyRange(sourceRange, destinationRange, options);
```

Mengaktifkan `CopyFormatting` memastikan kebutuhan **mempertahankan pemformatan pivot** terpenuhi, memberikan Anda duplikat yang pixel‑perfect.

## Output yang Diharapkan

Saat Anda menjalankan program, konsol akan keluar tanpa pesan (kecuali Anda menambahkan logging). Membuka `copy-pivot.xlsx` harus menampilkan:

- Sheet 1: Data asli dan tabel pivot tidak berubah.  
- **CopyDestination**: Replika persis dari pivot, ditempatkan mulai baris 31 (karena baris di UI Excel berbasis 1).  
- Semua slicer dan filter berfungsi; mengklik “Refresh” memperbarui kedua pivot secara bersamaan.

## Kesimpulan

Kami baru saja mendemonstrasikan cara **menyalin tabel pivot ke lembar lain** menggunakan Aspose.Cells dalam C#. Langkah‑langkah—menyiapkan proyek, memuat workbook, mendefinisikan rentang, menyalin dengan `CopyPivotTable = true`, dan menyimpan—membentuk pola andal yang dapat Anda gunakan kembali dalam pipeline otomatisasi apa pun.

Jika Anda ingin melangkah lebih jauh, pertimbangkan:

- **Duplikasi pivot Excel** di beberapa workbook (loop melalui file).  
- Menggunakan opsi **Aspose.Cells copy range with pivot** untuk memindahkan pivot antar workbook yang berbeda.  
- Mengotomatiskan penyegaran dengan `PivotTable.RefreshData()` setelah menyalin.

Silakan bereksperimen dengan rentang sumber yang berbeda, atau gabungkan teknik ini dengan pembuatan diagram untuk dasbor pelaporan yang sepenuhnya otomatis. Ada pertanyaan? Tinggalkan komentar, dan selamat coding!

![Screenshot showing copied pivot table in new sheet](copy-pivot-screenshot.png "copy pivot table to another sheet example")

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Mengubah Sumber Data Tabel Pivot Menggunakan Aspose.Cells untuk .NET | Panduan Analisis Data](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Menguasai Pemformatan Tabel Pivot di .NET Menggunakan Aspose.Cells](/cells/english/net/formatting/format-pivot-tables-dotnet-aspose-cells/)
- [Mengakses Sumber Data Eksternal Tabel Pivot di .NET menggunakan Aspose.Cells](/cells/english/net/data-analysis/access-pivot-table-data-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}