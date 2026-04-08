---
category: general
date: 2026-04-07
description: Pelajari cara memperluas array di C# menggunakan Aspose.Cells. Tutorial
  ini menunjukkan cara membuat workbook C#, menulis formula Excel C#, dan mengatur
  formula sel C# dengan mudah.
draft: false
keywords:
- how to expand array
- create workbook c#
- use aspose cells
- write excel formula c#
- set cell formula c#
language: id
og_description: Temukan cara memperluas array di C# menggunakan Aspose.Cells. Ikuti
  langkah‑langkah jelas kami untuk membuat workbook C#, menulis formula Excel C#,
  dan mengatur formula sel C#.
og_title: Cara Memperluas Array di C# dengan Aspose.Cells – Panduan Lengkap
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Cara Memperluas Array di C# dengan Aspose.Cells – Panduan Langkah demi Langkah
url: /id/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Memperluas Array di C# dengan Aspose.Cells – Panduan Langkah‑per‑Langkah

Pernah bertanya-tanya **how to expand array** di dalam lembar Excel dari C# tanpa harus berurusan dengan loop yang berantakan? Anda tidak sendirian. Banyak pengembang menemui kebuntuan ketika mereka perlu mengubah array konstan kecil menjadi kolom atau baris yang lebih besar untuk perhitungan selanjutnya. Kabar baik? Aspose.Cells membuatnya sangat mudah, dan Anda dapat melakukannya dengan satu formula Excel.

Dalam tutorial ini kami akan membahas seluruh proses: membuat workbook C#, menggunakan Aspose.Cells, menulis formula Excel C#, dan akhirnya mengatur cell formula C# sehingga array diperluas persis seperti yang Anda harapkan. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat dijalankan yang mencetak nilai yang diperluas ke konsol, dan Anda akan memahami mengapa pendekatan ini bersih dan berperforma tinggi.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini bekerja di .NET Core dan .NET Framework)  
- Aspose.Cells untuk .NET ≥ 23.12 (versi terbaru pada saat penulisan)  
- Pemahaman dasar tentang sintaks C#—tidak memerlukan pengalaman mendalam dalam otomatisasi Excel  

Jika Anda sudah memiliki semua itu, bagus—mari kita mulai.

## Langkah 1: Buat Workbook C# dengan Aspose.Cells

Pertama, kita membutuhkan objek workbook baru. Anggaplah ini sebagai file Excel kosong yang hidup sepenuhnya di memori sampai Anda memutuskan untuk menyimpannya.

```csharp
using Aspose.Cells;
using System;

namespace ExpandArrayDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize a new workbook – this is the canvas for our work.
            Workbook workbook = new Workbook();

            // Grab the first worksheet (index 0). Most demos start here.
            Worksheet ws = workbook.Worksheets[0];
```

> **Pro tip:** Jika Anda berencana bekerja dengan beberapa lembar, Anda dapat menambahkannya melalui `workbook.Worksheets.Add()` dan merujuknya dengan nama atau indeks.

## Langkah 2: Tulis Formula Excel C# untuk Memperluas Array

Sekarang masuk ke inti masalah—how to expand array. Fungsi `EXPAND` (tersedia di versi Excel terbaru) mengambil array sumber dan memperluasnya ke ukuran yang ditentukan. Di C# kita cukup menetapkan formula itu ke sebuah sel.

```csharp
            // Set a formula that expands a 3‑element array into a 5‑row column.
            // The syntax mirrors what you'd type in Excel: =EXPAND({1,2,3},5,1)
            ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";
```

Mengapa menggunakan `EXPAND`? Fungsi ini menghindari loop manual, menjaga workbook tetap ringan, dan memungkinkan Excel menghitung ulang secara otomatis jika Anda kemudian mengubah array sumber. Ini adalah cara paling bersih untuk menjawab pertanyaan **how to expand array** tanpa menulis kode C# tambahan.

## Langkah 3: Hitung Workbook Agar Formula Dieksekusi

Aspose.Cells tidak secara otomatis mengevaluasi formula sampai Anda memintanya. Memanggil `Calculate` memaksa mesin menjalankan fungsi `EXPAND` dan mengisi rentang target.

```csharp
            // Force calculation so the formula result becomes available.
            workbook.Calculate();
```

Jika Anda melewatkan langkah ini, membaca nilai sel akan mengembalikan teks formula alih-alih angka yang telah dihitung.

## Langkah 4: Baca Nilai yang Diperluas – Set Cell Formula C# dan Ambil Hasil

Dengan lembar kerja yang sudah dihitung, kita kini dapat membaca lima sel yang diisi oleh `EXPAND`. Ini mendemonstrasikan **set cell formula c#** dalam aksi dan juga menunjukkan cara menarik data kembali ke aplikasi Anda.

```csharp
            // Loop through the first 5 rows of column A and print each value.
            for (int row = 0; row < 5; row++)
            {
                // Cells[row, 0] corresponds to column A (zero‑based index).
                Console.WriteLine(ws.Cells[row, 0].Value);
            }

            // Optional: keep the console window open when debugging.
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

### Output yang Diharapkan

Menjalankan program akan mencetak hal berikut ke konsol:

```
1
2
3
0
0
```

Tiga angka pertama berasal dari array asli `{1,2,3}`. Dua baris terakhir diisi dengan nol karena `EXPAND` menambahkan nilai default (nol untuk array numerik) pada ukuran target. Jika Anda menginginkan nilai padding yang berbeda, Anda dapat membungkus pemanggilan `EXPAND` dengan `IFERROR` atau menggabungkannya dengan `CHOOSE`.

## Langkah 5: Simpan Workbook (Opsional)

Jika Anda ingin memeriksa file Excel yang dihasilkan, cukup tambahkan pemanggilan `Save` sebelum program berakhir:

```csharp
            // Save the workbook to disk for verification.
            workbook.Save("ExpandedArray.xlsx");
```

Membuka `ExpandedArray.xlsx` akan menampilkan kolom lima baris yang sama di sel A1:A5, mengonfirmasi bahwa formula telah dievaluasi dengan benar.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika saya membutuhkan ekspansi horizontal alih-alih vertikal?

Ubah argumen ketiga `EXPAND` dari `1` (baris) menjadi `0` (kolom) dan sesuaikan loopnya:

```csharp
ws.Cells["A1"].Formula = "=EXPAND({1,2,3},1,5)"; // expands to a 1‑row, 5‑column range
```

### Bisakah saya memperluas rentang dinamis alih-alih array yang ditulis keras?

Tentu saja. Ganti literal `{1,2,3}` dengan referensi ke rentang sel lain, misalnya `A10:C10`. Formula menjadi:

```csharp
ws.Cells["A1"].Formula = "=EXPAND(A10:C10,5,1)";
```

Pastikan rentang sumber ada sebelum Anda memicu perhitungan.

### Bagaimana pendekatan ini dibandingkan dengan looping di C#?

Looping memerlukan Anda menulis setiap nilai secara manual:

```csharp
for (int i = 0; i < 5; i++) ws.Cells[i, 0].PutValue(i < 3 ? i + 1 : 0);
```

Meskipun cara itu berhasil, menggunakan `EXPAND` menjaga logika di dalam Excel, yang menguntungkan ketika workbook nantinya diedit oleh non‑developer atau ketika Anda ingin mesin perhitungan native Excel menangani perubahan secara otomatis.

## Ringkasan Contoh Kerja Penuh

Berikut adalah program lengkap yang siap disalin‑tempel dan mendemonstrasikan **how to expand array** menggunakan Aspose.Cells. Tidak ada dependensi tersembunyi, hanya pernyataan `using` yang Anda perlukan.

```csharp
using Aspose.Cells;
using System;

namespace ExpandArrayDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook.
            Workbook workbook = new Workbook();

            // 2️⃣ Access the first worksheet.
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Write the EXPAND formula – this is the core of how to expand array.
            ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

            // 4️⃣ Calculate so the formula resolves.
            workbook.Calculate();

            // 5️⃣ Read and display the expanded values.
            for (int row = 0; row < 5; row++)
            {
                Console.WriteLine(ws.Cells[row, 0].Value);
            }

            // Optional: Save the workbook for visual verification.
            workbook.Save("ExpandedArray.xlsx");

            Console.WriteLine("Done – press any key to close.");
            Console.ReadKey();
        }
    }
}
```

Jalankan ini di Visual Studio, Rider, atau CLI `dotnet run` dan Anda akan melihat array diperluas persis seperti yang dijelaskan.

## Kesimpulan

Kami telah membahas **how to expand array** di dalam lembar kerja Excel menggunakan C# dan Aspose.Cells, mulai dari membuat workbook C# hingga menulis formula Excel C# dan akhirnya mengatur cell formula C# untuk mengambil hasilnya. Teknik ini mengandalkan fungsi native `EXPAND`, menjaga kode Anda tetap rapi dan spreadsheet Anda dinamis.

Langkah selanjutnya? Coba ganti array sumber dengan named range, bereksperimen dengan nilai padding yang berbeda, atau rangkaikan beberapa pemanggilan `EXPAND` untuk membangun tabel data yang lebih besar. Anda juga dapat menjelajahi fungsi kuat lainnya seperti `SEQUENCE` atau `LET` untuk otomasi berbasis formula yang lebih kaya.

Ada pertanyaan tentang penggunaan Aspose.Cells untuk skenario yang lebih kompleks? Tinggalkan komentar di bawah atau lihat dokumentasi resmi Aspose.Cells untuk pendalaman lebih lanjut tentang penanganan formula, penyetelan performa, dan dukungan lintas platform.

Selamat coding, dan nikmati mengubah array kecil menjadi kolom yang kuat! 

![Diagram yang menunjukkan program C# membuat workbook, menerapkan formula EXPAND, dan mencetak hasil – mengilustrasikan cara memperluas array dengan Aspose.Cells](https://example.com/expand-array-diagram.png "Diagram cara memperluas array menggunakan Aspose.Cells di C#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}