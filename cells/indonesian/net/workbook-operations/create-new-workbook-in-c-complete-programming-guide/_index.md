---
category: general
date: 2026-03-25
description: Buat workbook baru di C# dan pelajari cara menggunakan EXPAND, menghitung
  kotangen, serta menyimpan workbook ke file dengan kode langkah demi langkah.
draft: false
keywords:
- create new workbook
- save workbook to file
- how to use expand
- how to calculate cotangent
- how to save excel
language: id
og_description: Buat buku kerja baru di C# dan langsung lihat cara menggunakan EXPAND,
  menghitung kotangen, serta menyimpan buku kerja ke file.
og_title: Buat workbook baru di C# – Panduan Pemrograman Lengkap
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Buat buku kerja baru di C# – Panduan Pemrograman Lengkap
url: /id/net/workbook-operations/create-new-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat workbook baru di C# – Panduan Pemrograman Lengkap

Pernahkah Anda perlu **create new workbook** di C# tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian. Baik Anda mengotomatisasi pipeline pelaporan atau sekadar bermain dengan formula Excel dalam kode, kemampuan untuk membuat workbook, menyisipkan formula seperti `EXPAND` atau `COT`, dan kemudian **save workbook to file** adalah keterampilan inti bagi setiap pengembang .NET.

Dalam tutorial ini kami akan membahas contoh dunia‑nyata yang melakukan hal tersebut: kami akan menginstansiasi workbook baru, menggunakan fungsi `EXPAND` untuk mengubah array statis menjadi kolom dinamis, menghitung kotangen dengan fungsi `COT`, dan akhirnya **save workbook to file** sebagai file `.xlsx`. Pada akhir tutorial Anda akan memiliki potongan kode yang siap dijalankan, memahami *mengapa* setiap pemanggilan penting, dan melihat beberapa variasi berguna untuk kasus tepi.

> **Pro tip:** Semua kode di bawah ini bekerja dengan versi terbaru Aspose.Cells untuk .NET (per Maret 2026). Jika Anda menggunakan rilis yang lebih lama, permukaan API secara keseluruhan sama, tetapi periksa kembali impor namespace.

## Apa yang Anda Butuhkan

- .NET 6.0 atau lebih baru (contoh ini menargetkan .NET 6, tetapi .NET 5 juga dapat digunakan)  
- Aspose.Cells untuk .NET yang diinstal melalui NuGet (`Install-Package Aspose.Cells`)  
- Pengetahuan C# yang cukup (Anda pasti bisa)  

Itu saja—tidak ada DLL tambahan, tidak ada interop COM, dan tentu saja tidak ada Excel yang terinstal di mesin. Siap? Mari kita mulai.

![Tangkapan layar yang menunjukkan cara membuat workbook baru di C#](assets/create-new-workbook.png){alt="Tangkapan layar yang menunjukkan cara membuat workbook baru di C#"}

## Langkah 1: Buat workbook baru

Hal pertama yang harus Anda lakukan adalah menginstansiasi kelas `Workbook`. Anggaplah itu seperti membuka file Excel kosong di memori. Objek ini menyimpan koleksi lembar kerja, gaya, dan semua hal lain yang akan Anda perlukan nanti.

```csharp
using Aspose.Cells;

class ExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();               // <-- creates an empty .xlsx structure
        Worksheet ws = workbook.Worksheets[0];            // default sheet is named "Sheet1"
```

Mengapa langsung mengambil lembar kerja pertama? Sebagian besar contoh cepat menggunakan satu lembar, dan accessor `Worksheets[0]` adalah cara tercepat untuk mendapatkan referensi tanpa melakukan loop. Jika Anda membutuhkan beberapa lembar nanti, Anda dapat menambahkannya dengan `workbook.Worksheets.Add()`.

## Langkah 2: Cara menggunakan EXPAND untuk menghasilkan rentang dinamis

`EXPAND` adalah fungsi Excel yang lebih baru yang mengambil sebuah array dan menambahnya hingga ukuran tertentu. Dalam kode kami, kami akan memperluas array literal `{1,2,3}` menjadi **kolom 5‑baris** yang dimulai dari sel `A1`. Sintaks di dalam string persis seperti yang Anda ketik di Excel, sehingga Anda dapat menyalin‑tempelnya langsung ke sel nanti jika diinginkan.

```csharp
        // Step 2: Apply EXPAND to turn {1,2,3} into a 5‑row vertical range
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // rows=5, cols=1
```

### Apa yang terjadi di balik layar?

- `{1,2,3}` adalah literal array horizontal.  
- Argumen kedua (`5`) memberi tahu Excel untuk memperluas array menjadi **5 baris**.  
- Argumen ketiga (`1`) memaksa output **satu kolom**.  

Jika Anda menghilangkan argumen ketiga, Excel akan mencoba mempertahankan bentuk asli, yang dapat menghasilkan blok 5×3 alih‑alih satu kolom. Itu adalah jebakan umum saat Anda pertama kali bereksperimen dengan `EXPAND`.

#### Variasi yang mungkin Anda butuhkan

| Bentuk yang diinginkan | Contoh formula |
|------------------------|----------------|
| blok 3‑baris, 2‑kolom | `=EXPAND({1,2,3},3,2)` |
| Isi ke bawah saja (kolom sama) | `=EXPAND({10,20},10,1)` |
| Perluas ke jumlah kolom yang lebih besar | `=EXPAND({5},5,4)` |

Silakan ganti literal atau dimensi sesuai dengan logika pembuatan data Anda.

## Langkah 3: Cara menghitung kotangen dengan fungsi COT

Fungsi `COT` mengembalikan kotangen dari sudut yang dinyatakan dalam radian. Dalam contoh kami kami menghitung kotangen dari 45° (π/4 radian). Hasilnya, `1`, berada di sel `B1`.

```csharp
        // Step 3: Use COT to calculate cotangent of 45 degrees (π/4 radians)
        ws.Cells["B1"].Formula = "=COT(PI()/4)"; // PI() returns π, divided by 4 = 45°
```

### Mengapa menggunakan COT daripada menghitung secara manual?

Excel sudah mengetahui cara menangani konversi trigonometri, sehingga Anda menghindari kesalahan pembulatan floating‑point yang dapat muncul jika Anda mencoba `1 / TAN(angle)`. Selain itu, formula tetap mudah dibaca bagi siapa pun yang meninjau spreadsheet nanti.

#### Kasus tepi: sudut di luar 0‑360°

Jika Anda memberikan sudut yang lebih besar dari `2*PI()` (atau yang negatif), Excel akan secara otomatis membungkusnya, tetapi hasilnya bisa mengejutkan. Untuk aman, Anda mungkin ingin menormalkan sudut terlebih dahulu:

```csharp
        // Normalize angle to 0‑2π range before applying COT
        ws.Cells["C1"].Formula = "=COT(MOD(PI()*3, 2*PI()))";
```

Potongan kode tersebut menunjukkan cara menggabungkan `MOD` dengan `COT` untuk perhitungan yang kuat.

## Langkah 4: Cara menyimpan workbook ke file (Excel)

Sekarang formula sudah ditempatkan, langkah terakhir adalah **save workbook to file**. Anda dapat memilih jalur apa pun yang Anda suka—pastikan direktori ada dan Anda memiliki izin menulis.

```csharp
        // Step 4 (optional): Save the workbook so you can inspect the results
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Apa yang sebenarnya disimpan?

Saat Anda membuka `output.xlsx` di Excel, Anda akan melihat:

| A | B |
|---|---|
| 1 | 1 |
| 2 |   |
| 3 |   |
|   |   |
|   |   |

- Kolom **A** berisi array yang diperluas `{1,2,3}` diikuti dua sel kosong (karena kami meminta 5 baris).  
- Sel **B1** menampilkan `1`, kotangen dari 45°.  

Jika Anda menyegarkan workbook (tekan `F9` atau aktifkan perhitungan otomatis), Excel akan mengevaluasi formula dan menampilkan hasilnya. Aspose.Cells juga menyediakan metode `CalculateFormula` jika Anda membutuhkan nilai tanpa membuka Excel:

```csharp
        workbook.CalculateFormula();
        double cotResult = ws.Cells["B1"].DoubleValue; // should be 1.0
```

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

| Pertanyaan | Jawaban |
|------------|---------|
| **Apakah saya perlu mengaktifkan perhitungan secara manual?** | Tidak. Secara default Aspose.Cells menyimpan formula apa adanya; Excel akan menghitungnya saat dibuka. Gunakan `workbook.CalculateFormula()` untuk perhitungan sebelumnya. |
| **Apakah saya dapat menulis formula ke beberapa sel sekaligus?** | Tentu saja. Gunakan `ws.Cells["D1:D5"].Formula = "=RAND()"` untuk mengisi rentang dengan angka acak. |
| **Bagaimana jika folder target tidak ada?** | Buat dulu: `Directory.CreateDirectory(Path.GetDirectoryName(outputPath));` |
| **Apakah `EXPAND` didukung di versi Excel yang lebih lama?** | `EXPAND` muncul pada Excel 365/2019. Jika Anda memerlukan kompatibilitas dengan file yang lebih lama, pertimbangkan menggunakan kombinasi `INDEX`/`SEQUENCE` sebagai gantinya. |
| **Bagaimana cara menyembunyikan tampilan formula?** | Setel `ws.Cells["A1"].FormulaHidden = true;` dan lindungi lembar jika Anda tidak ingin pengguna melihat formula yang mendasarinya. |

## Kesimpulan

Anda sekarang tahu **how to create new workbook** objek di C#, memanfaatkan kekuatan fungsi `EXPAND` untuk menghasilkan array dinamis, menghitung kotangen dengan `COT`, dan **save workbook to file** sebagai dokumen Excel yang rapi. Contoh lengkap yang dapat dijalankan terdapat di potongan kode di atas—salin ke aplikasi konsol, tekan `F5`, dan buka `output.xlsx` yang dihasilkan untuk melihat keajaibannya.

### Apa selanjutnya?

- **Jelajahi fungsi array dinamis lainnya** seperti `SEQUENCE`, `FILTER`, dan `SORT`.  
- **Otomatisasi pembuatan diagram** dengan API diagram kaya Aspose.Cells.  
- **Integrasikan dengan sumber data** (SQL, CSV) dan masukkan nilai tersebut ke dalam formula secara programatik.  
- **Pelajari cara menyimpan Excel sebagai PDF** atau format lain—sempurna untuk pipeline pelaporan.

Silakan bereksperimen: ubah nilai array, sesuaikan sudut, atau tulis hasilnya ke lembar lain. Tidak ada batasnya ketika Anda menggabungkan C# dengan mesin formula modern Excel.

Selamat coding, semoga spreadsheet Anda selalu menghitung dengan benar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}