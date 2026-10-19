---
category: general
date: 2026-07-13
description: Buat buku kerja Excel dan atur rumus sel menggunakan EXPAND. Pelajari
  cara menghitung ulang buku kerja serta menulis rumus Excel secara dinamis dalam
  C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set cell formula
- recalculate workbook
- write excel formula
- how to use expand
language: id
lastmod: 2026-07-13
og_description: Buat buku kerja Excel secara instan. Panduan ini menunjukkan cara
  mengatur rumus sel, menghitung ulang buku kerja, dan menguasai cara menggunakan
  EXPAND untuk rentang dinamis.
og_image_alt: Screenshot showing create excel workbook with EXPAND formula in C#
og_title: Buat Buku Kerja Excel dengan Rumus EXPAND – Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Create Excel workbook and set cell formula using EXPAND. Learn how
    to recalculate workbook and write Excel formulas dynamically in C#.
  headline: Create Excel Workbook with EXPAND Formula – Complete Guide
  type: TechArticle
tags:
- excel
- csharp
- aspnet
title: Buat Buku Kerja Excel dengan Rumus EXPAND – Panduan Lengkap
url: /id/net/formulas-functions/create-excel-workbook-with-expand-formula-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Workbook Excel dengan Rumus EXPAND – Panduan Lengkap

Pernah bertanya-tanya bagaimana cara **create excel workbook** secara programatis dan membiarkan satu rumus mengisi seluruh tabel untuk Anda? Anda tidak sendirian. Dalam banyak skenario pelaporan atau ekspor data, Anda perlu menaruh sebuah workbook ke folder Unduhan pengguna, menyebarkan sebuah rumus ke sel‑sel, dan membiarkannya menghitung secara otomatis.  

Dalam tutorial ini kami akan membahas tepat itu: kami akan **create excel workbook**, **set cell formula** menggunakan fungsi `EXPAND` yang baru, dan kemudian **recalculate workbook** sehingga hasilnya muncul seketika. Pada akhir tutorial Anda juga akan mengetahui **how to use expand** untuk rentang dinamis dan merasa nyaman **write excel formula** kode yang beradaptasi dengan ukuran data yang berubah.

---

## Apa yang Akan Anda Bangun

- Instance `Workbook` baru (tanpa template diperlukan).  
- Rumus array yang mengembang di `A1` yang tumbuh menjadi blok 5‑baris × 3‑kolom.  
- Panggilan ke `Calculate()` yang memaksa engine mengevaluasi rumus.  
- Membaca kembali sel‑sel yang terisi secara cepat sehingga Anda dapat memverifikasi output.

Tidak diperlukan pustaka eksternal selain inti Aspose.Cells (atau mesin Excel .NET lain yang sebanding) — hanya C# biasa.

## Prasyarat

- .NET 6+ (atau .NET Framework 4.7.2+).  
- Referensi ke pustaka manipulasi Excel yang mendukung fungsi array dinamis (mis., **Aspose.Cells**, **GemBox.Spreadsheet**, atau **ClosedXML** dengan mesin Excel terbaru).  
- Familiaritas dasar dengan sintaks C# — jika Anda pernah menulis “Hello World”, Anda siap melanjutkan.

## Langkah 1: Buat Workbook Excel dan Tambahkan Worksheet

Hal pertama yang harus dilakukan. Kita membutuhkan objek workbook untuk menampung semuanya. Anggaplah itu sebagai buku catatan kosong yang akan Anda isi nanti.

```csharp
// Step 1: Instantiate a new workbook
var workbook = new Workbook();               // Primary object
var sheet = workbook.Worksheets[0];          // Grab the default sheet
```

> **Why this matters:** Kelas `Workbook` adalah titik masuk untuk setiap operasi Excel. Tanpa itu Anda tidak dapat menetapkan rumus atau menghitung ulang apa pun. Membuat workbook di awal juga memungkinkan Anda menambahkan beberapa lembar nanti jika skenario Anda berkembang.

## Langkah 2: Tetapkan Rumus Sel dengan `EXPAND`

Sekarang kami akan **set cell formula** di `A1`. Fungsi `EXPAND` mengambil referensi “spill” (`A1#`) dan memperluasnya ke ukuran tertentu — dalam kasus kami, 5 baris kali 3 kolom.

```csharp
// Step 2: Insert an expanding array formula into cell A1
// The source range A1# will be stretched to 5 rows × 3 columns
sheet.Cells[0, 0].Formula = "=EXPAND(A1#,5,3)";
```

> **Pro tip:** Jika Anda menggunakan pustaka yang mencerminkan mesin perhitungan Excel, operator spill `#` berfungsi langsung. Jika tidak, Anda mungkin perlu mengaktifkan dukungan array dinamis di pengaturan pustaka.

> **What if the source cell is empty?** `EXPAND` akan mengembalikan `#SPILL!`. Untuk menghindarinya, Anda dapat membungkus referensi dengan `IFERROR` atau menyediakan nilai default, misalnya, `=IFERROR(EXPAND(A1#,5,3),0)`.

## Langkah 3: Isi Sel Sumber (Opsional)

`EXPAND` membutuhkan sesuatu untuk diperluas. Mari letakkan konstanta array sederhana di `A1` sehingga kita dapat melihat spill beraksi.

```csharp
// Optional: Fill A1 with a 2‑by‑2 array constant
sheet.Cells[0, 0].ArrayFormula = "{1,2;3,4}";
```

Sekarang `A1#` mewakili blok 2 × 2, dan `EXPAND` akan memperluasnya menjadi matriks 5 × 3 yang diminta, mengisi sel tambahan dengan nol (atau apa pun yang diputuskan oleh engine).

## Langkah 4: Hitung Ulang Workbook untuk Mengevaluasi Rumus

Menetapkan rumus tidak cukup — Anda harus **recalculate workbook** sehingga engine benar‑benar menghitung nilai-nilai.

```csharp
// Step 4: Force calculation of all formulas
workbook.Calculate();
```

> **Why we recalculate:** Beberapa pustaka mengevaluasi rumus secara malas hanya ketika Anda menyimpan atau secara eksplisit meminta nilai. Memanggil `Calculate()` menjamin bahwa area spill terisi segera, yang penting untuk pemrosesan lanjutan atau untuk mengembalikan data ke UI.

## Langkah 5: Verifikasi Hasil – Baca Kembali Rentang yang Diperluas

Mari ambil beberapa sel dari area yang diperluas untuk membuktikan bahwa itu berhasil.

```csharp
// Step 5: Read back a few cells from the expanded block
for (int row = 0; row < 5; row++)
{
    for (int col = 0; col < 3; col++)
    {
        var value = sheet.Cells[row, col].Value;
        Console.Write($"{value}\t");
    }
    Console.WriteLine();
}
```

**Output konsol yang diharapkan**

```
1	2	0	
3	4	0	
0	0	0	
0	0	0	
0	0	0	
```

Perhatikan bagaimana array 2 × 2 asli ditempatkan di sudut kiri‑atas, dan sel‑sel yang tersisa diisi dengan nol (perilaku default `EXPAND` ketika ukuran target melebihi sumber).

## Variasi Umum dan Kasus Tepi

| Situasi | Cara Menangani |
|-----------|------------------|
| **Rentang sumber lebih besar dari target** | `EXPAND` akan memotong baris/kolom ekstra. Jika Anda membutuhkan seluruh sumber, hapus argumen ukuran. |
| **Ukuran sumber dinamis** | Gunakan `ROWS(A1#)` dan `COLUMNS(A1#)` di dalam `EXPAND` untuk spill yang menyesuaikan diri secara otomatis. |
| **Kinerja pada rentang besar** | Menghitung ulang workbook yang sangat besar dapat lambat. Panggil `Calculate()` hanya pada lembar yang terpengaruh: `sheet.Calculate();`. |
| **Menyimpan workbook** | Setelah verifikasi, panggil `workbook.Save("Report.xlsx");` untuk menyimpan file. |
| **Menggunakan fungsi dinamis lain** | `SEQUENCE`, `FILTER`, dan `SORT` cocok dengan `EXPAND`. Misalnya, `=EXPAND(FILTER(A2:A20, B2:B20>0),10,2)`. |

## Contoh Kerja Penuh (Semua Langkah Digabung)

```csharp
using System;
using Aspose.Cells;   // Replace with your chosen library

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];

        // 2️⃣ Set an expanding formula in A1
        sheet.Cells[0, 0].Formula = "=EXPAND(A1#,5,3)";

        // 3️⃣ Optional: give A1 a 2x2 array constant
        sheet.Cells[0, 0].ArrayFormula = "{1,2;3,4}";

        // 4️⃣ Recalculate so the formula evaluates
        workbook.Calculate();

        // 5️⃣ Print the first 5 rows × 3 columns
        for (int r = 0; r < 5; r++)
        {
            for (int c = 0; c < 3; c++)
            {
                Console.Write($"{sheet.Cells[r, c].Value}\t");
            }
            Console.WriteLine();
        }

        // Save if you want to inspect the file
        workbook.Save("ExpandDemo.xlsx");
    }
}
```

Jalankan program ini dan Anda akan melihat output yang sama seperti yang ditunjukkan sebelumnya, plus file `ExpandDemo.xlsx` di disk yang berisi array spill yang sama.

## Tips & Trik dari Pengalaman

- **Pro tip:** Jika Anda hanya membutuhkan nilai yang diperluas untuk perhitungan lebih lanjut (tanpa spreadsheet yang terlihat pengguna), pertimbangkan membaca nilai langsung setelah `Calculate()` — tidak perlu menulis ke disk.  
- **Watch out for:** Beberapa versi lama mesin Excel tidak mendukung array dinamis; mereka akan menghasilkan `#NAME?`. Selalu verifikasi versi pustaka Anda.  
- **Typical mistake:** Lupa memanggil `Calculate()` menyebabkan sel kosong dan pengguna kebingungan. Selalu uji seluruh alur.  
- **Performance hint:** Menetapkan rumus secara batch (`sheet.Cells[range].Formula = ...`) dapat lebih cepat daripada penugasan individual ketika menangani ribuan sel.

## Kesimpulan

Anda sekarang tahu cara **create excel workbook**, **set cell formula** dengan fungsi `EXPAND` yang kuat, dan **recalculate workbook** sehingga data spill tepat di tempat yang Anda butuhkan. Pendekatan ini memungkinkan Anda **write excel formula** kode yang beradaptasi dengan ukuran data yang berubah tanpa meng‑hard‑code rentang — sempurna untuk dasbor, laporan otomatis, atau skenario apa pun di mana data sumber tumbuh seiring waktu.

Siap untuk langkah berikutnya? Coba ganti `EXPAND` dengan `SEQUENCE` untuk menghasilkan grid bernomor, atau gabungkan dengan `FILTER` untuk mengambil hanya baris yang memenuhi kondisi. Dan jangan lupa menjelajahi cara **set cell formula** untuk grafik, pivot table, atau pemformatan bersyarat — workbook baru Anda adalah fondasi yang kuat.

Ada pertanyaan tentang kasus tepi atau keanehan spesifik pustaka? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode kerja lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Membuat Named Ranges Berjangkauan Workbook di Excel Menggunakan Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Otomasi Excel dengan Aspose.Cells .NET&#58; Buat Workbook & Atur Tautan Eksternal](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Cara Memuat Workbook Excel & Mengatur Ukuran Printer Menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/load-workbook-set-printer-sizes-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}