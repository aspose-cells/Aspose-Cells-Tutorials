---
category: general
date: 2026-03-30
description: Pelajari cara menggunakan WRAPCOLS dalam C# untuk membuat buku kerja
  Excel, menambahkan data ke Excel, dan memaksa perhitungan formula sambil juga menggunakan
  WRAPROWS.
draft: false
keywords:
- how to use wrapcols
- create excel workbook c#
- add data to excel
- force formula calculation
- how to use wraprows
language: id
og_description: Temukan cara menggunakan WRAPCOLS dalam C# untuk membuat workbook
  Excel, menambahkan data, memaksa perhitungan rumus, dan memanfaatkan WRAPROWS untuk
  rumus array.
og_title: Cara Menggunakan WRAPCOLS di C# – Panduan Lengkap
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Cara Menggunakan WRAPCOLS di C# – Membuat Workbook Excel dengan Fungsi Wrap
url: /id/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan WRAPCOLS di C# – Membuat Workbook Excel dengan Fungsi Wrap

Pernah bertanya-tanya **bagaimana cara menggunakan WRAPCOLS** saat Anda mengotomatisasi Excel dengan C#? Anda tidak sendirian—banyak pengembang mengalami kebuntuan ketika mereka perlu mengubah rentang horizontal menjadi array vertikal tanpa menulis banyak kode. Kabar baiknya, Aspose.Cells membuatnya sangat mudah.

Dalam tutorial ini kami akan menelusuri contoh lengkap yang dapat dijalankan yang menunjukkan **cara menggunakan WRAPCOLS**, cara **membuat workbook Excel C#**‑style, cara **menambahkan data ke Excel**, dan bahkan cara **memaksa perhitungan formula** sehingga hasilnya muncul secara langsung. Kami juga akan menambahkan **cara menggunakan WRAPROWS** untuk transformasi sebaliknya. Pada akhir tutorial Anda akan memiliki program siap‑jalankan dan pemahaman jelas mengapa setiap langkah penting.

---

![How to use WRAPCOLS in C# example](alt="Screenshot showing Excel workbook after using WRAPCOLS in C#")

## Apa yang Dibahas dalam Panduan Ini

* Menyiapkan workbook baru dengan Aspose.Cells.
* Mengisi sel secara programatis (**menambahkan data ke Excel**).
* Menerapkan fungsi `WRAPCOLS` untuk mengubah baris menjadi kolom.
* Menggunakan `WRAPROWS` untuk mengubah kolom kembali menjadi baris (**cara menggunakan wraprows**).
* Memaksa mesin mengevaluasi formula secara langsung (**memaksa perhitungan formula**).
* Menyimpan file dan memeriksa output.

Tidak ada dokumentasi eksternal yang diperlukan—semua yang Anda butuhkan ada di sini.

---

## Cara Menggunakan WRAPCOLS di C# – Implementasi Langkah‑per‑Langkah

Di bawah ini adalah file sumber lengkap. Silakan salin‑tempel ke proyek konsol baru, tambahkan paket NuGet Aspose.Cells, dan tekan **F5**.

```csharp
// ------------------------------------------------------------
// How to Use WRAPCOLS in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.Cells;

namespace WrapFunctionsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh workbook (this is how we **create excel workbook c#** style)
            Workbook workbook = new Workbook();

            // 2️⃣ Grab the first worksheet – it's created by default
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ **Add data to Excel**: place two numbers side‑by‑side
            sheet.Cells["A1"].PutValue(1);   // first value
            sheet.Cells["B1"].PutValue(2);   // second value

            // 4️⃣ **How to use WRAPCOLS** – turn the horizontal range A1:B1 into a vertical array
            //    The second argument (1) tells WRAPCOLS to create 1 column per element.
            sheet["C1"].Formula = "WRAPCOLS(A1:B1, 1)";

            // 5️⃣ **How to use WRAPROWS** – the opposite; turn the same range into a horizontal array
            //    Here we ask for 2 rows per element, which produces a single row with both values.
            sheet["C2"].Formula = "WRAPROWS(A1:B1, 2)";

            // 6️⃣ **Force formula calculation** so the workbook reflects the results immediately
            workbook.CalculateFormula();

            // 7️⃣ Save the workbook to disk – change the path to a folder you own
            string outputPath = @"WrapFunctions.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
            Console.WriteLine("Check cells C1 and C2 for the WRAPCOLS / WRAPROWS results.");
        }
    }
}
```

### Mengapa Setiap Baris Penting

| Langkah | Penjelasan |
|------|-------------|
| **1️⃣ Buat workbook baru** | Ini adalah dasar. Aspose.Cells memperlakukan objek `Workbook` sebagai seluruh file Excel, sehingga Anda secara efektif **membuat workbook Excel C#**. |
| **2️⃣ Ambil worksheet pertama** | Workbook baru selalu berisi setidaknya satu worksheet (`Worksheets[0]`). Mengaksesnya lebih awal menghindari kejutan null‑reference. |
| **3️⃣ Tambahkan data ke Excel** | Dengan menggunakan `PutValue` kami **menambahkan data ke Excel** tanpa harus khawatir tentang pemformatan sel. Angka `1` dan `2` adalah data uji untuk fungsi wrap. |
| **4️⃣ Cara menggunakan WRAPCOLS** | `WRAPCOLS(A1:B1, 1)` memberi tahu Excel untuk mengambil rentang `A1:B1` dan menumpahkan nilainya secara vertikal, satu per baris. Hasilnya berada di `C1` dan menumpah ke bawah (`C1`, `C2`, …). |
| **5️⃣ Cara menggunakan WRAPROWS** | `WRAPROWS(A1:B1, 2)` melakukan hal sebaliknya: membuat tumpahan horizontal, menempatkan dua nilai ke dalam satu baris yang dimulai dari `C2`. |
| **6️⃣ Paksa perhitungan formula** | Secara default, Aspose.Cells mungkin menunda perhitungan hingga file dibuka di Excel. Memanggil `CalculateFormula()` **memaksa perhitungan formula** sehingga Anda dapat membaca hasilnya segera setelah menyimpan. |
| **7️⃣ Simpan workbook** | Langkah akhir menulis semuanya ke disk. Buka `WrapFunctions.xlsx` yang dihasilkan untuk melihat hasilnya. |

---

## Membuat Workbook Excel C# – Menyiapkan Lingkungan

Sebelum menjalankan kode, pastikan Anda memiliki alat yang tepat:

1. **.NET 6.0+** – Versi LTS terbaru bekerja paling baik.
2. **Visual Studio 2022** (atau VS Code dengan ekstensi C#).
3. **Aspose.Cells untuk .NET** – Instal melalui NuGet:  
   ```bash
   dotnet add package Aspose.Cells
   ```
4. Folder yang dapat ditulisi untuk file output.

Prasyarat ini minimal; tidak diperlukan interop COM atau instalasi Office, itulah mengapa Aspose.Cells menjadi pilihan populer untuk pembuatan Excel sisi‑server.

---

## Menambahkan Data ke Excel – Praktik Terbaik

Saat Anda **menambahkan data ke Excel** secara programatis, pertimbangkan tips berikut:

* **Gunakan `PutValue`** untuk angka mentah atau string; secara otomatis mendeteksi tipe data.
* **Hindari hard‑coding alamat sel** dalam proyek besar—gunakan loop atau named range untuk skalabilitas.
* **Terapkan gaya sel secara hemat**; setiap perubahan gaya menambah beban. Jika memerlukan pemformatan, buat satu objek gaya dan terapkan ke banyak sel.

Dalam contoh kecil kami hanya menyisipkan dua angka, tetapi pola yang sama dapat diskalakan ke ribuan baris.

---

## Cara Menggunakan WRAPROWS – Contoh Array Horizontal

Jika Anda membutuhkan kebalikan dari `WRAPCOLS`, `WRAPROWS` adalah pilihan utama. Sintaksnya adalah:

```
WRAPROWS(source_range, [rows_per_item])
```

* `source_range` – rentang yang ingin Anda transformasikan.
* `rows_per_item` – opsional; memberi tahu Excel berapa banyak baris yang ditempati setiap elemen. Dalam demo kami menggunakan `2` untuk memaksa kedua nilai berada pada satu baris.

Anda dapat bereksperimen dengan mengubah argumen kedua:

```csharp
// Example: split each value into its own column, three rows per item
sheet["D1"].Formula = "WRAPROWS(A1:B1, 3)";
```

Buka workbook dan Anda akan melihat nilai‑nilai menumpah melintasi tiga kolom, masing‑masing kolom berisi angka asli yang diulang sesuai kebutuhan.

---

## Memaksa Perhitungan Formula – Kapan dan Mengapa

Anda mungkin bertanya, “Apakah saya benar‑benar perlu memanggil `CalculateFormula()`?” Jawabannya **ya**, jika:

* Anda berencana membaca nilai yang dihitung **secara programatis** setelah menyimpan.
* Anda ingin memastikan file terbuka di Excel dengan hasil yang sudah ditampilkan.
* Anda menjalankan di **lingkungan headless** (misalnya, API web) di mana tidak ada pengguna yang secara manual memicu perhitungan ulang.

Melewatkan langkah ini tidak akan merusak workbook, tetapi sel akan menampilkan teks formula (`=WRAPCOLS(...)`) alih‑alih nilai yang dihitung sampai Excel melakukan perhitungan ulang.

---

## Output yang Diharapkan – Apa yang Harus Dilihat

Setelah menjalankan program dan membuka `WrapFunctions.xlsx`:

| Sel | Formula | Nilai yang Ditampilkan |
|------|---------|------------------------|
| **C1** | `=WRAPCOLS(A1:B1, 1)` | `1` (di C1) dan `2` (di C2) – daftar vertikal |
| **C2** | `=WRAPROWS(A1:B1, 2)` | `1` di C2 dan `2` di D2 – daftar horizontal |

Jadi Anda akan melihat kolom nilai yang dimulai dari **C1** dan baris nilai yang dimulai dari **C2**. Ini mengonfirmasi kedua fungsi wrap berperilaku sesuai harapan.

---

## Kasus Edge & Variasi

| Skenario | Apa yang berubah? | Saran penyesuaian |
|----------|-------------------|-------------------|
| **Rentang besar (A1:Z1)** | Lebih banyak nilai yang ditumpahkan secara vertikal | Tingkatkan argumen kedua `WRAPCOLS` jika Anda menginginkan beberapa kolom per grup. |
| **Data non‑numeric** | String diperlakukan sama | Tidak ada perubahan kode; `PutValue` menerima objek apa pun. |
| **Rentang dinamis** | Anda tidak mengetahui ukuran pada waktu kompilasi | Gunakan `sheet.Cells.MaxDataColumn` dan `MaxDataRow` untuk membangun string alamat. |
| **Beberapa worksheet** | Perlu menerapkan fungsi wrap pada sheet berbeda | Referensikan worksheet yang tepat (`workbook.Worksheets["Sheet2"]`). |

Dengan mengantisipasi variasi ini, Anda dapat menyesuaikan pola inti untuk hampir semua skenario otomasi.

---

## Pro Tips dari Lapangan

* **Pro tip:** Bungkus pembuatan workbook dalam blok `using` jika Anda menargetkan .NET Core 3.1+ untuk memastikan semua sumber daya dilepaskan dengan cepat.
* **Waspadai:** Menetapkan formula yang sama pada rentang besar tanpa memanggil `CalculateFormula()` dapat menyebabkan bottleneck kinerja. Proses formula secara batch bila memungkinkan.
* **Tip:** Jika Anda perlu membaca kembali nilai yang dihitung dalam kode, panggil `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}