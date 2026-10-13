---
category: general
date: 2026-03-22
description: Pelajari cara menduplikasi pivot di C# menggunakan Aspose.Cells. Panduan
  ini juga menunjukkan cara menyalin baris dan memuat workbook Excel dengan C# untuk
  otomatisasi Excel yang mulus dalam menyalin baris.
draft: false
keywords:
- how to duplicate pivot
- how to copy rows
- load excel workbook c#
- excel automation copy rows
language: id
og_description: Bagaimana cara menduplikasi pivot di C#? Ikuti tutorial singkat ini
  untuk memuat workbook Excel dengan C#, menyalin baris, dan menguasai otomatisasi
  Excel menyalin baris.
og_title: Cara Menggandakan Pivot di C# – Panduan Lengkap
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Cara Menggandakan Pivot di C# – Panduan Lengkap Langkah demi Langkah
url: /id/net/pivot-tables/how-to-duplicate-pivot-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggandakan Pivot di C# – Panduan Lengkap Langkah‑per‑Langkah

Pernah bertanya‑tanya **bagaimana cara menggandakan pivot** tabel secara programatis tanpa harus menyeretnya secara manual di Excel? Anda bukan satu‑satunya. Dalam banyak alur pelaporan, tata letak pivot yang sama diperlukan pada sekumpulan baris baru, dan melakukannya secara manual membuang waktu.  

Berita baik? Dengan beberapa baris C# Anda dapat memuat sebuah workbook Excel, menentukan area yang berisi pivot, dan **cara menyalin baris** sehingga pivot muncul di lokasi baru—semua dalam satu proses otomatis. Dalam tutorial ini kami juga akan membahas dasar‑dasar **load excel workbook c#** dan memberi Anda fondasi yang kuat untuk tugas **excel automation copy rows**.

> **Apa yang akan Anda dapatkan**  
> • Contoh lengkap yang dapat dijalankan yang menggandakan sebuah tabel pivot.  
> • Penjelasan mengapa setiap baris kode penting.  
> • Tips menangani kasus tepi seperti lembar kerja tersembunyi atau pivot ganda.

---

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- **.NET 6.0** (atau versi .NET terbaru) terpasang.  
- **Aspose.Cells for .NET** – perpustakaan yang akan kami gunakan untuk memanipulasi file Excel. Anda dapat mengunduhnya via NuGet:  

```bash
dotnet add package Aspose.Cells
```  

- Sebuah workbook sumber (`Source.xlsx`) yang sudah berisi tabel pivot pada rentang **A1:J20** (rentang yang akan kami gandakan).  
- Familiaritas dasar dengan sintaks C# – tidak ada yang rumit, hanya pernyataan `using` biasa dan metode `Main`.

Jika ada yang belum Anda kenal, jeda sejenak dan instal paketnya; sisanya mengasumsikan perpustakaan sudah siap pakai.

![Ilustrasi cara menggandakan pivot di C# menggunakan Aspose.Cells](https://example.com/duplicate-pivot.png "ilustrasi cara menggandakan pivot di C#")

*Teks alt gambar: "cara menggandakan pivot di C# contoh yang menunjukkan baris pivot sumber dan yang digandakan".*

---

## Langkah 1: Memuat Workbook Excel C# – Membuka File

Hal pertama yang harus Anda lakukan ketika ingin **load excel workbook c#** adalah membuat instance `Workbook` yang menunjuk ke file Anda. Objek ini memberi Anda akses ke setiap lembar kerja, sel, dan pivot di dalam file.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Load the source workbook
        string sourcePath = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // From here on we can work with worksheets, ranges, and pivots.
```

**Mengapa ini penting:**  
`Workbook` mengabstraksi seluruh file Excel menjadi model dalam memori. Tanpa memuatnya terlebih dahulu Anda tidak dapat memeriksa lokasi pivot atau menyalin baris. Selain itu, konstruktor secara otomatis mendeteksi format file (XLS, XLSX, CSV, dll.), sehingga Anda tidak memerlukan kode tambahan untuk deteksi format.

---

## Langkah 2: Cara Menyalin Baris – Menentukan Area Pivot

Setelah workbook berada di memori, kita perlu memberi tahu Aspose.Cells baris mana yang berisi pivot. Pada contoh ini pivot berada di **A1:J20**, yang diterjemahkan menjadi baris **0‑19** (indeks berbasis nol). Kita akan membungkusnya dalam struktur `CellArea`.

```csharp
        // Step 2: Define the cell area that contains the pivot table (A1:J20)
        // Row indices are zero‑based, column indices are also zero‑based.
        CellArea copyRange = new CellArea(startRow: 0, startColumn: 0, endRow: 19, endColumn: 9);
```

**Mengapa kami menggunakan `CellArea`:**  
Ini adalah cara ringan untuk mendeskripsikan blok persegi panjang. Ketika Anda kemudian memanggil `CopyRows`, metode tersebut membaca objek ini untuk mengetahui tepat baris mana yang harus digandakan. Jika Anda perlu menyesuaikan rentang (misalnya pivot berkembang ke kolom K), Anda hanya mengubah nilai `endColumn`.

---

## Langkah 3: Mengakses Lembar Kerja Target

Sebagian besar workbook hanya memiliki satu lembar, tetapi API bekerja sama untuk banyak lembar. Ambil lembar kerja pertama (indeks 0) – di situlah pivot asli berada.

```csharp
        // Step 3: Get the first worksheet from the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Pro tip:**  
Jika Anda memiliki lembar bernama, Anda juga dapat mengambilnya dengan nama: `workbook.Worksheets["Sheet1"]`. Ini membantu menghindari hard‑coding indeks ketika struktur workbook berubah.

---

## Langkah 4: Cara Menyalin Baris – Menggandakan Tabel Pivot

Berikut inti dari **bagaimana cara menggandakan pivot**: kami menyalin baris yang berisi pivot ke lokasi baru. Pada contoh ini kami mulai di baris 31 (indeks berbasis nol 30). Metode `CopyRows` menyalin *baik* data maupun cache pivot yang mendasarinya, sehingga baris baru berperilaku persis seperti yang asli.

```csharp
        // Step 4: Copy the rows of the defined range to a new location (starting at row 31)
        // The third argument is the destination start row (zero‑based).
        worksheet.Cells.CopyRows(copyRange.StartRow, copyRange.EndRow, destinationRow: 30);
```

**Apa yang terjadi di balik layar?**  
`CopyRows` menggandakan setiap baris, mempertahankan formula, gaya, dan definisi pivot. Karena cache pivot berada di tingkat workbook, pivot yang digandakan otomatis merujuk ke sumber data yang sama – tidak perlu konfigurasi tambahan.

**Kasus tepi – baris tersembunyi:**  
Jika ada baris dalam rentang sumber yang tersembunyi, mereka tetap tersembunyi setelah penyalinan. Jika Anda ingin menampilkannya, panggil `worksheet.Rows[destRow].IsHidden = false` setelah proses penyalinan.

---

## Langkah 5: Menyimpan Workbook – Memverifikasi Duplikat

Akhirnya, tulis perubahan kembali ke disk. Anda dapat menimpa file asli atau, lebih aman, menyimpan dengan nama baru agar dapat membandingkan sebelum/d sesudah.

```csharp
        // Step 5: Save the workbook – the pivot table is now duplicated in the new rows
        string outputPath = @"C:\Data\CopyWithPivot.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine("Pivot duplicated successfully! Check " + outputPath);
    }
}
```

**Hasil yang akan Anda lihat:**  
Buka `CopyWithPivot.xlsx`. Anda akan menemukan pivot asli di **A1:J20** dan salinan identik mulai dari **A31:J50**. Kedua pivot dapat disegarkan secara independen, dan slicer apa pun yang terhubung ke yang asli tetap berfungsi untuk salinan karena mereka berbagi cache yang sama.

---

## Pertanyaan Umum & Variasi

### Bisakah saya menggandakan beberapa pivot sekaligus?

Tentu saja. Loop melalui semua tabel pivot (`worksheet.PivotTables`) dan salin setiap rentang ke tujuan yang berbeda. Pastikan rentang tujuan tidak tumpang tindih.

### Bagaimana jika workbook sumber dilindungi kata sandi?

Aspose.Cells memungkinkan Anda membuka file yang dilindungi dengan memberikan kata sandi ke konstruktor `Workbook`:

```csharp
Workbook workbook = new Workbook(sourcePath, new LoadOptions { Password = "mySecret" });
```

### Bagaimana menyalin baris tanpa memengaruhi formula?

Jika Anda hanya membutuhkan *nilai* (tanpa formula), gunakan `CopyRows` dengan flag `CopyOptions`:

```csharp
worksheet.Cells.CopyRows(sourceStart, sourceEnd, destStart, new CopyOptions { CopyValues = true });
```

### Apakah ada cara menyalin baris ke *workbook* lain?

Ya. Setelah menyalin baris di lembar sumber, Anda dapat mengkloning lembar kerja ke instance `Workbook` lain via `targetWorkbook.Worksheets.AddCopy(worksheet)`.

---

## Tips Pro untuk Excel Automation Copy Rows yang Handal

- **Validasi rentang** sebelum menyalin. Pemeriksaan cepat `if (copyRange.EndRow >= worksheet.Cells.MaxDataRow)` mencegah error out‑of‑range.  
- **Matikan perhitungan** saat menyalin rentang besar: `workbook.Settings.CalcMode = CalcMode.Manual;` – ini mempercepat operasi secara signifikan.  
- **Dispose objek** (`workbook.Dispose()`) jika Anda memproses banyak file dalam loop untuk membebaskan sumber daya native.  
- **Log operasi** – terutama dalam pipeline produksi – sehingga Anda dapat melacak file mana yang diproses dan menangkap kegagalan lebih awal.

---

## Kesimpulan

Anda kini tahu **bagaimana cara menggandakan pivot** tabel di C# menggunakan Aspose.Cells, dan telah melihat alur kerja lengkap dari **load excel workbook c#** hingga **excel automation copy rows** serta akhirnya menyimpan hasilnya. Contoh ini berdiri sendiri, dapat dijalankan langsung, dan dapat diperluas untuk menangani pivot ganda, file terlindungi, atau penyalinan antar‑workbook.

Langkah selanjutnya? Coba sesuaikan skrip untuk:

- Menyegarkan pivot yang digandakan secara programatis (`pivotTable.RefreshData();`).  
- Mengekspor area yang digandakan ke CSV untuk pemrosesan lebih lanjut.  
- Mengintegrasikan kode ke dalam API ASP.NET Core sehingga pengguna dapat mengunggah file dan menerima versi dengan pivot yang digandakan secara instan.

Selamat coding, semoga otomatisasi Excel Anda selalu lancar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}