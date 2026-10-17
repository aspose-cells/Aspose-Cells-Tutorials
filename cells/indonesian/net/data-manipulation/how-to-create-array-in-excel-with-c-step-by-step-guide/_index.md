---
category: general
date: 2026-02-09
description: Cara membuat array di Excel dengan C# dijelaskan dalam hitungan menit
  – pelajari cara menghasilkan nomor urut, gunakan COT, dan simpan buku kerja sebagai
  XLSX.
draft: false
keywords:
- how to create array
- create excel workbook c#
- generate sequence numbers
- save workbook as xlsx
- how to use cot
language: id
og_description: Cara membuat array di Excel dengan C# dibahas langkah demi langkah,
  termasuk menghasilkan nomor urut, menggunakan COT, dan menyimpan buku kerja sebagai
  XLSX.
og_title: Cara membuat array di Excel dengan C# – Panduan Cepat
tags:
- C#
- Excel
- Aspose.Cells
title: Cara membuat array di Excel dengan C# – Panduan Langkah demi Langkah
url: /id/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat array di Excel dengan C# – Panduan Langkah demi Langkah

Pernah bertanya‑tanya **cara membuat array** di Excel menggunakan C# tanpa menghabiskan berjam‑jam menelusuri dokumentasi? Anda tidak sendirian. Banyak pengembang menemui kebuntuan ketika mereka membutuhkan rentang spill dinamis, nilai trigonometri cepat, atau sekadar file XLSX yang bersih disimpan ke disk. Pada tutorial ini kami akan menyelesaikan masalah itu langsung—dengan membangun sebuah workbook kecil yang menulis rumus array yang dapat berkembang, menyisipkan perhitungan kotangen, dan menyimpan semuanya sebagai file XLSX.  

Kami juga akan menambahkan beberapa trik tambahan: menghasilkan nomor urut, menguasai fungsi `COT`, dan memastikan file tersimpan di lokasi yang Anda inginkan. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat dipakai ulang dalam proyek .NET apa pun. Tanpa basa‑basi, hanya kode yang berfungsi.

> **Tip pro:** Contoh ini menggunakan pustaka **Aspose.Cells** yang populer, tetapi konsepnya dapat diterapkan pada paket otomasi Excel lainnya (EPPlus, ClosedXML) dengan hanya sedikit perubahan.

---

## Apa yang Anda Perlukan

- **.NET 6** atau lebih baru (kode ini juga dapat dikompilasi pada .NET Framework 4.7+ )  
- **Aspose.Cells untuk .NET** – dapat diunduh dari NuGet (`Install-Package Aspose.Cells`)  
- Editor teks atau IDE (Visual Studio, Rider, VS Code…)  
- Izin menulis ke folder tempat file output akan disimpan  

Itu saja—tanpa konfigurasi tambahan, tanpa COM interop, hanya assembly terkelola yang bersih.

---

## Langkah 1: Cara membuat array di Excel – Inisialisasi Workbook

Hal pertama yang harus dilakukan ketika Anda ingin **cara membuat array** di lembar Excel adalah membuat objek workbook. Anggap workbook sebagai kanvas kosong; worksheet adalah tempat Anda melukis rumus‑rumus.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // <- fresh workbook
        Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet

        // The rest of the steps follow...
```

Mengapa menggunakan `Workbook()` tanpa parameter? Itu memberi Anda workbook dalam memori dengan lembar default, yang sempurna untuk tugas cepat dan programatik. Jika Anda perlu membuka file yang sudah ada, cukup berikan jalur file ke konstruktor.

---

## Langkah 2: Menghasilkan nomor urut dengan EXPAND dan SEQUENCE

Sekarang kita sudah memiliki lembar, mari selesaikan bagian **menghasilkan nomor urut** dari teka‑teki ini. Fungsi array dinamis baru Excel (`SEQUENCE`, `EXPAND`) memungkinkan kita membuat daftar vertikal 3‑baris dan secara otomatis spill ke rentang 3 × 5.

```csharp
        // Write a dynamic array formula that expands a 3‑row sequence into a 3×5 spill range
        // EXPAND pads the result to 5 columns, SEQUENCE generates numbers 1‑3 vertically
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

**Apa yang terjadi di sini?**  
- `SEQUENCE(3,1,1,1)` → menghasilkan array vertikal `{1;2;3}`.  
- `EXPAND(...,5,1)` → mengambil kolom tiga‑baris itu dan memperluasnya menjadi lima kolom, mengisi sel‑sel tambahan dengan kosong.  

Saat Anda membuka `output.xlsx` yang dihasilkan, Anda akan melihat blok 3 × 5 dimulai dari **A1** dimana kolom pertama berisi 1, 2, 3 dan empat kolom berikutnya kosong. Teknik ini menjadi tulang punggung **cara membuat array**‑style spill range tanpa menulis setiap sel secara manual.

---

## Langkah 3: Cara menggunakan COT – Menambahkan Rumus Trigonometri

Jika Anda juga penasaran tentang **cara menggunakan COT** di dalam rumus Excel, fungsi `COT` adalah cara praktis untuk mendapatkan kotangen dari sudut yang dinyatakan dalam radian. Mari hitung `cot(π/4)`, yang seharusnya menghasilkan **1**.

```csharp
        // Write a simple trigonometric formula that calculates cotangent of 45° (π/4)
        // COT(π/4) evaluates to 1
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

Perhatikan kami menggunakan `PI()` untuk mendapatkan nilai radian 180°, lalu membaginya dengan 4 untuk mencapai 45°. Excel melakukan perhitungan berat, dan sel **B1** akan menampilkan `1` setelah workbook dibuka. Ini mendemonstrasikan **cara menggunakan COT** untuk perhitungan teknik atau keuangan cepat tanpa harus menambahkan pustaka matematika terpisah.

---

## Langkah 4: Simpan workbook sebagai XLSX – Menyimpan File

Semua kesenangan membuat array dan menyisipkan rumus akan sia‑sia jika Anda tidak menulis file ke disk. Berikut cara sederhana untuk **menyimpan workbook sebagai xlsx** menggunakan Aspose.Cells:

```csharp
        // Save the workbook to verify the formulas (optional)
        string outputPath = @"C:\Temp\output.xlsx";   // adjust to your folder
        workbook.Save(outputPath, SaveFormat.Xlsx);

        // Let the user know we’re done
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Mengapa menentukan `SaveFormat.Xlsx`? Itu menjamin format OpenXML modern, yang dapat dibaca secara universal (Excel, LibreOffice, Google Sheets). Jika Anda memerlukan file `.xls` lama, cukup ganti enum‑nya.

---

## Contoh Kerja Penuh (Semua Langkah Digabungkan)

Berikut adalah program lengkap yang siap dijalankan. Salin‑tempel ke proyek konsol, pulihkan paket NuGet Aspose.Cells, dan tekan **F5**.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Create a dynamic spill range (how to create array)
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";

        // Step 3: Calculate cotangent (how to use cot)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";

        // Step 4: Persist the file (save workbook as xlsx)
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Hasil yang diharapkan** setelah membuka `output.xlsx`:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 |   |   |   |
| 2 |   |   |   |   |
| 3 |   |   |   |   |

- Kolom A menampilkan angka 1‑3 yang dihasilkan oleh `SEQUENCE`.  
- Kolom B berisi nilai **1** dari rumus `COT`.  
- Kolom C‑E kosong, menggambarkan efek padding dari `EXPAND`.

---

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya membutuhkan lebih banyak baris atau kolom?

Cukup ubah argumen `SEQUENCE` dan `EXPAND`.  
- `SEQUENCE(10,2,5,2)` akan menghasilkan matriks 10‑baris × 2‑kolom dimulai dari 5 dan bertambah 2.  
- `EXPAND(...,10,5)` akan menambah hasil menjadi 10 kolom dan 5 baris.

### Apakah ini bekerja dengan versi Excel yang lebih lama?

Fungsi array dinamis (`SEQUENCE`, `EXPAND`) memerlukan Excel 365 atau 2019+. Untuk file legacy, Anda dapat kembali ke rumus klasik atau menulis nilai secara langsung lewat `Cells[row, col].PutValue(value)`.

### Bisakah saya menulis rumus dalam gaya R1C1?

Tentu saja. Ganti `A1` dengan `Cells[0, 0]` dan gunakan properti `FormulaR1C1`:

```csharp
worksheet.Cells[0, 0].FormulaR1C1 = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

### Bagaimana dengan pemisah desimal yang spesifik budaya?

Aspose.Cells menghormati locale workbook. Jika Anda memerlukan budaya tertentu, atur `workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");` sebelum menulis rumus.

---

## Ringkasan Visual

![cara membuat array di Excel menggunakan C#](/images/how-to-create-array-excel-csharp.png "cara membuat array di Excel menggunakan C#")

*Cuplikan layar menunjukkan rentang spill akhir dan hasil kotangen.*

---

## Kesimpulan

Itulah dia—**cara membuat array** di Excel dengan C# dari awal, menghasilkan nomor urut, memanfaatkan fungsi `COT`, dan **menyimpan workbook sebagai XLSX** dalam satu program yang rapi. Poin penting yang dapat diambil:

1. Gunakan objek `Workbook` dan `Worksheet` untuk memulai otomasi Excel Anda.  
2. Manfaatkan fungsi array dinamis (`SEQUENCE`, `EXPAND`) untuk rentang spill yang fleksibel.  
3. Sisipkan fungsi trigonometri seperti `COT` untuk perhitungan cepat tanpa pustaka tambahan.  
4. Simpan hasil dengan `SaveFormat.Xlsx` untuk mendapatkan file yang dapat dibaca secara universal.

Siap untuk langkah selanjutnya? Coba ganti `COT(PI()/4)`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}