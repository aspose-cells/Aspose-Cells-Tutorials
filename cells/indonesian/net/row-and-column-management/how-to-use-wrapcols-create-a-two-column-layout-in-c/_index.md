---
category: general
date: 2026-02-15
description: Cara menggunakan WRAPCOLS untuk membuat tata letak dua kolom, menambahkan
  formula, dan menghasilkan array urutan di lembar kerja C# – panduan langkah demi
  langkah.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: id
og_description: Cara menggunakan WRAPCOLS untuk membuat tata letak dua kolom, menambahkan
  rumus, dan menghasilkan array urutan dalam lembar kerja C# – panduan lengkap.
og_title: 'Cara Menggunakan WRAPCOLS: Tata Letak Dua Kolom di C#'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'Cara Menggunakan WRAPCOLS: Membuat Tata Letak Dua Kolom di C#'
url: /id/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan WRAPCOLS: Membuat Tata Letak Dua‑Kolom di C#

Pernah bertanya-tanya **bagaimana cara menggunakan WRAPCOLS** ketika Anda membutuhkan tampilan dua kolom cepat di dalam lembar kerja bergaya Excel? Anda tidak sendirian. Banyak pengembang menemui kendala ketika mencoba membagi daftar yang dihasilkan menjadi kolom rapi tanpa menulis loop untuk setiap sel. Kabar baiknya? Dengan fungsi `WRAPCOLS` Anda dapat menaruh satu formula di `A1` dan membiarkan Excel (atau mesin yang kompatibel) melakukan pekerjaan berat.

Di tutorial ini kami akan menjelaskan **cara menambahkan formula** yang membuat **tata letak dua kolom**, menunjukkan **cara membuat kolom** secara dinamis, dan bahkan **menghasilkan array urutan** secara langsung. Pada akhir tutorial Anda akan memiliki cuplikan kode C# yang dapat dijalankan sepenuhnya, yang dapat Anda tempelkan ke proyek Anda, jalankan, dan melihat blok dua kolom yang rapi muncul secara instan.

## Apa yang Akan Anda Pelajari

- Tujuan `WRAPCOLS` dan mengapa itu merupakan alternatif yang lebih baik dibandingkan loop manual.  
- Cara **menambahkan formula** ke sel lembar kerja menggunakan C#.  
- Cara menghasilkan array urutan dengan `SEQUENCE` dan memasukkannya ke dalam `WRAPCOLS`.  
- Tips untuk menghitung ulang lembar sehingga formula langsung terpecahkan.  
- Penanganan kasus tepi (mis., lembar kerja kosong, jumlah kolom khusus).

Tidak diperlukan pustaka eksternal selain paket pemrosesan Excel standar – kami akan menggunakan **ClosedXML** untuk API-nya yang sederhana, namun konsepnya dapat diterapkan pada EPPlus, SpreadsheetGear, atau bahkan Google Sheets melalui API-nya.

---

## Prasyarat

- .NET 6.0 atau lebih baru (kode dapat dikompilasi pada .NET Core dan .NET Framework).  
- Referensi ke **ClosedXML** (`dotnet add package ClosedXML`).  
- Pengetahuan dasar C# – Anda harus nyaman dengan pernyataan `using` dan inisialisasi objek.  

Jika Anda sudah memiliki workbook terbuka, Anda dapat melewati bagian pembuatan file dan langsung ke bagian formula.

---

## Langkah 1: Menyiapkan Worksheet (Cara Membuat Kolom)

Pertama kita membutuhkan objek `Worksheet` untuk bekerja. Di ClosedXML Anda mendapatkannya dari `XLWorkbook`. Cuplikan kode di bawah membuat workbook baru, menambahkan sheet bernama *Demo*, dan mengambil referensi bernama `worksheet` untuk kejelasan.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **Mengapa mengganti nama?**  
> Menjaga nama variabel tetap pendek (`worksheet`) membuat kode selanjutnya lebih mudah dibaca, terutama ketika Anda menautkan banyak operasi. Ini juga mencerminkan gaya penamaan yang Anda temukan di sebagian besar dokumentasi, mengurangi beban kognitif.

---

## Langkah 2: Menulis Formula (Cara Menambahkan Formula + Menghasilkan Array Urutan)

Berikutnya baris ajaib. Kami akan menempatkan formula di sel **A1** yang melakukan dua hal:

1. **Menghasilkan array urutan** dari enam angka (`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **Membungkus angka-angka tersebut ke dalam dua kolom** (`WRAPCOLS(..., 2)`).

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **Apa yang terjadi?**  
> `SEQUENCE(6)` membuat array vertikal `{1;2;3;4;5;6}`. `WRAPCOLS` kemudian mengambil array tersebut dan “membungkus” ke dalam jumlah kolom yang ditentukan—dalam kasus ini **2**. Hasilnya adalah blok 3‑baris × 2‑kolom yang terlihat seperti:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Jika Anda mengubah argumen kedua menjadi **3**, Anda akan mendapatkan tata letak tiga kolom. Itulah inti dari **cara membuat kolom** secara dinamis tanpa loop manual.

---

## Langkah 3: Menghitung Ulang Worksheet (Memastikan Formula Dievaluasi)

ClosedXML tidak secara otomatis mengevaluasi formula saat Anda menuliskannya. Anda perlu memanggil `Calculate()` pada workbook (atau pada worksheet tertentu) untuk memaksa evaluasi.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **Tips pro:** Jika Anda bekerja dengan workbook besar, panggil `Calculate()` hanya pada sheet yang memang berubah. Ini menghemat memori dan mempercepat proses.

Saat Anda membuka `WrapColsDemo.xlsx` Anda akan melihat tata letak dua kolom terisi rapi di **A1:B3**. Tidak ada kode tambahan yang diperlukan untuk melakukan loop melalui baris atau kolom – `WRAPCOLS` menangani semuanya.

---

## Langkah 4: Memverifikasi Output (Apa yang Diharapkan)

Setelah menjalankan program, buka file yang dihasilkan. Anda harus melihat:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Jika angka muncul secara vertikal (yaitu semua di kolom A), periksa kembali bahwa Anda memanggil `worksheet.Calculate()` **setelah** menetapkan formula. Beberapa engine juga memerlukan `workbook.Calculate()`; cuplikan di atas bekerja untuk evaluator bawaan ClosedXML.

---

## Variasi Umum & Kasus Tepi

### Mengubah Jumlah Kolom

Untuk **membuat tata letak dua kolom** dengan jumlah baris yang berbeda, cukup sesuaikan ukuran `SEQUENCE` atau argumen kedua `WRAPCOLS`:

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

Ini menghasilkan blok 4‑baris × 3‑kolom (12 angka dibagi ke tiga kolom).

### Menggunakan Jumlah Kolom Dinamis

Jika jumlah kolom Anda berasal dari variabel, sisipkan dengan interpolasi string:

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

Sekarang Anda memiliki **cara menambahkan formula** yang beradaptasi pada waktu berjalan.

### Worksheet Kosong

Jika worksheet kosong, `Calculate()` tetap berfungsi – formula akan mengisi sel mulai dari A1. Namun, jika Anda kemudian menghapus baris/kolom yang berpotongan dengan rentang output, Anda mungkin melihat error `#REF!`. Untuk menghindarinya, bersihkan rentang target terlebih dahulu:

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### Kompatibilitas

`WRAPCOLS` dan `SEQUENCE` merupakan bagian dari fungsi **Dynamic Array** Excel, yang diperkenalkan di Office 365. Jika Anda menargetkan versi Excel yang lebih lama, fungsi-fungsi tersebut tidak ada, dan Anda perlu menggunakan loop manual. Evaluator ClosedXML meniru perilaku Excel terbaru, sehingga aman untuk lingkungan modern.

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**Hasil yang diharapkan:** Membuka *WrapColsDemo.xlsx* menampilkan tata letak dua kolom yang rapi dengan angka 1‑6 disusun seperti yang dijelaskan sebelumnya.

---

## Kesimpulan

Kami telah membahas **cara menggunakan WRAPCOLS** untuk **membuat tata letak dua kolom**, mendemonstrasikan **cara menambahkan formula** secara programatik, dan melihat bagaimana `SEQUENCE` memungkinkan Anda **menghasilkan array urutan** tanpa loop. Dengan memanfaatkan fungsi dynamic array Excel dari C#, Anda dapat menjaga kode tetap singkat, mudah dibaca, dan dapat dipelihara.

Selanjutnya, Anda mungkin ingin menjelajahi:

- **Membuat jumlah baris dinamis** dengan `ROWS` atau `COUNTA`.  
- **Menata output** (batas, format angka) menggunakan API styling ClosedXML.  
- **Mengekspor ke CSV** setelah tata letak selesai, untuk pemrosesan selanjutnya.

Cobalah, ubah jumlah kolom, dan lihat seberapa cepat Anda dapat membuat prototipe spreadsheet yang kompleks. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}