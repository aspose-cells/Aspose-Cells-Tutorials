---
category: general
date: 2026-11-19
description: Cara menggunakan wrapcols di C# untuk membungkus data di Excel dan menghitung
  rumus Excel dengan cepat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- calculate excel formulas
- wrap data in excel
- save excel file c#
- load excel workbook c#
language: id
lastmod: 2026-11-19
og_description: Cara menggunakan wrapcols di C# untuk membungkus data di Excel. Pelajari
  cara menghitung rumus Excel dan menyimpan workbook secara programatik.
og_image_alt: Screenshot showing wrapped data in an Excel worksheet after applying
  WRAPCOLS
og_title: Cara menggunakan wrapcols di C# – membungkus data di Excel
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to use wrapcols in C# to wrap data in Excel and calculate Excel
    formulas quickly.
  headline: How to use wrapcols in C# to wrap data in Excel
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Data Wrapping
title: Cara menggunakan wrapcols di C# untuk membungkus data di Excel
url: /id/net/formatting-rows-and-columns-in-excel/how-to-use-wrapcols-in-c-to-wrap-data-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menggunakan wrapcols di C# untuk membungkus data di Excel

Jika Anda perlu **how to use wrapcols** untuk mengatur ulang daftar vertikal menjadi beberapa kolom, panduan ini menunjukkan langkah‑langkah tepatnya. Anda juga akan belajar cara **calculate Excel formulas** sehingga hasilnya disimpan dalam file yang Anda simpan.

Bekerja dengan Excel dari C# sering dimulai dengan memuat workbook, menerapkan formula, dan akhirnya menyimpan perubahan. Tutorial ini mencakup semua tahapan tersebut sambil menjaga kode tetap mudah disalin‑tempel ke proyek Anda.

## Apa yang akan Anda capai

* Muat file `.xlsx` yang sudah ada dari disk (**load excel workbook c#**).
* Terapkan fungsi `WRAPCOLS` ke suatu rentang, secara efektif **wrap data in Excel**.
* Paksa mesin untuk mengevaluasi formula (**calculate Excel formulas**).
* Simpan workbook yang telah dimodifikasi (**save Excel file c#**).

Satu‑satunya prasyarat adalah referensi ke **Aspose.Cells for .NET** (atau perpustakaan apa pun yang mendukung fungsi `WRAPCOLS`). Kode ini bekerja dengan .NET 6+ dan Visual Studio 2022, tetapi IDE C# apa pun dapat digunakan.

## Cara menggunakan wrapcols dengan Aspose.Cells

Fungsi lembar kerja `WRAPCOLS` mengambil rentang satu‑dimensi dan mengembalikan array dua‑dimensi yang mengisi jumlah kolom yang ditentukan. Aspose.Cells mengevaluasi fungsi ini seperti Excel, sehingga Anda dapat menggunakannya langsung dalam formula sel.

```csharp
using System;
using Aspose.Cells;          // Install-Package Aspose.Cells via NuGet

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook and get the first worksheet
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.Worksheets[0];

        // Step 2: Write the WRAPCOLS formula into a cell
        // This wraps the values from A2:A10 into 3 columns, starting at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";

        // Step 3: Force calculation so the result becomes a static range
        wb.CalculateFormula();

        // Step 4: Save the workbook so you can open it in Excel
        var outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);

        Console.WriteLine("Workbook saved to " + outputPath);
    }
}
```

### Mengapa setiap baris penting

* **Loading the workbook** memberi Anda model objek langsung yang mencerminkan file Excel di disk.  
* **Assigning the formula** ke `A1` memberi tahu Excel (atau Aspose.Cells) untuk memperlakukan rentang tersebut sebagai array dinamis.  
* **`CalculateFormula()`** memicu mesin perhitungan; tanpa itu formula akan tetap tidak dievaluasi sampai file dibuka di Excel.  
* **Saving** menulis nilai yang dihitung kembali ke file baru, membuat data yang dibungkus terlihat oleh siapa pun yang membuka workbook.

## Menghitung formula Excel secara programatik

Memanggil `Workbook.CalculateFormula()` adalah cara yang direkomendasikan untuk **calculate Excel formulas** ketika Anda membutuhkan hasilnya secara langsung. Metode ini menghormati semua fungsi bawaan, fungsi buatan pengguna, dan referensi eksternal yang sudah terresolusi.

Jika Anda memiliki beberapa lembar kerja yang saling bergantung, Anda juga dapat mengirimkan objek `CalculationOptions` untuk mengontrol batas iterasi atau mengaktifkan perhitungan multi‑threaded:

```csharp
var options = new CalculationOptions
{
    // Enable iterative calculation for circular references
    IterativeCalculation = true,
    MaxIterations = 100,
    // Use all available CPU cores
    EnableMultiThreadedCalculation = true
};

wb.CalculateFormula(options);
```

Langkah tambahan ini opsional untuk contoh `WRAPCOLS` yang sederhana, tetapi menjadi penting pada workbook yang lebih besar di mana kinerja menjadi faktor.

## Simpan file Excel C# setelah membungkus data

Pemanggilan `Workbook.Save()` menulis seluruh workbook, termasuk array baru yang dihasilkan oleh `WRAPCOLS`. Anda dapat memilih salah satu format yang didukung (`.xlsx`, `.xls`, `.csv`, dll.):

```csharp
// Save as a standard XLSX file (default)
wb.Save(@"YOUR_DIRECTORY\wrapped.xlsx");

// Save as CSV – only the active sheet is exported
wb.Save(@"YOUR_DIRECTORY\wrapped.csv", SaveFormat.Csv);
```

Langkah **save Excel file c#** memastikan data yang dibungkus tetap tersimpan, sehingga saat berikutnya seseorang membuka file, mereka melihat tabel statis bukan formula.

## Muat workbook Excel C# dan siapkan lembar kerja

Jika file sumber Anda belum berisi data yang ingin Anda bungkus, Anda dapat membuatnya secara langsung:

```csharp
// Create a new workbook with a single worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Populate column A with sample values
for (int i = 0; i < 9; i++)
{
    ws.Cells[i + 2, 0].PutValue($"Item {i + 1}");
}
```

Potongan kode ini menunjukkan **load excel workbook c#** dalam arti Anda dapat memulai dari workbook kosong, mengisinya, dan kemudian menerapkan `WRAPCOLS`. Pola yang sama berlaku ketika Anda perlu mengimpor data dari basis data atau file CSV sebelum membungkus.

## Tips pro: verifikasi hasil tanpa membuka Excel

Setelah menyimpan, Anda dapat secara programatik membaca kembali area yang dibungkus untuk memastikan operasi berhasil:

```csharp
// Reload the saved file
Workbook checkWb = new Workbook(@"YOUR_DIRECTORY\output.xlsx");
Worksheet checkWs = checkWb.Worksheets[0];

// Print the first three rows of the wrapped area
for (int row = 0; row < 3; row++)
{
    for (int col = 0; col < 3; col++)
    {
        Console.Write($"{checkWs.Cells[row, col].StringValue}\t");
    }
    Console.WriteLine();
}
```

Konsol harus menampilkan daftar asli yang terbagi menjadi tiga kolom, mengonfirmasi bahwa **wrap data in excel** berfungsi sebagaimana mestinya.

## Pertanyaan umum dan kasus tepi

| Question | Answer |
|----------|--------|
| *Bagaimana jika rentang sumber memiliki lebih banyak baris daripada yang dapat diisi oleh `WRAPCOLS`?* | Fungsi ini terus membuat baris baru sesuai kebutuhan. Jumlah kolom tetap tetap. |
| *Apakah saya dapat membungkus ke jumlah kolom yang berbeda?* | Ya—ubah argumen kedua, misalnya `=WRAPCOLS(A2:A10,5)` untuk lima kolom. |
| *Apakah saya perlu menghapus formula setelah perhitungan?* | Tidak jika Anda memanggil `CalculateFormula()`. Fungsi mengembalikan array statis, tetapi formula tetap berada di sel. Jika Anda menginginkan nilai murni, salin rentang dan tempel‑nilai di atasnya. |
| *Apakah ini akan bekerja dengan file `.xls` lama?* | `WRAPCOLS` adalah fungsi array‑dinamis yang diperkenalkan di Excel 365. Format file lama yang tidak mendukung array dinamis akan menyimpan formula tetapi mungkin tidak menampilkan hasil yang dibungkus dengan benar. Gunakan `.xlsx` untuk perilaku yang dapat diandalkan. |

## Kesimpulan

Anda kini tahu **how to use wrapcols** di C# untuk **wrap data in Excel**, cara **calculate Excel formulas** secara langsung, dan cara **save Excel file C#** setelah transformasi. Contoh lengkap menunjukkan cara memuat workbook, menerapkan fungsi `WRAPCOLS`, memaksa perhitungan, dan menyimpan hasilnya.

### Langkah selanjutnya

* Jelajahi fungsi array‑dinamis lainnya seperti `UNWRAPCOLS` atau `SEQUENCE`.  
* Gunakan **Aspose.Cells** untuk mengimpor data dari basis data dan kemudian membungkusnya secara otomatis.  
* Gabungkan `WRAPCOLS` dengan pemformatan bersyarat untuk menyorot baris tertentu setelah pembungkusan.

Silakan bereksperimen dengan rentang sumber, jumlah kolom, dan format output yang berbeda. Jika Anda menemui masalah, meninjau kembali langkah **calculate Excel formulas** atau memeriksa pengaturan perhitungan workbook biasanya dapat menyelesaikannya.

--- 

*Gambar: ![Screenshot of wrapped data in Excel](/images/wrapcols-example.png){.align-center alt="Tangkapan layar yang menunjukkan data yang dibungkus dalam lembar kerja Excel setelah menerapkan WRAPCOLS"}*

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara menggunakan WRAPCOLS di C# untuk array Excel dan penyimpanan workbook](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-for-excel-arrays-and-workbook-savin/)
- [Cara membuat workbook Excel dan membagi data dengan WRAPCOLS di C#](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}