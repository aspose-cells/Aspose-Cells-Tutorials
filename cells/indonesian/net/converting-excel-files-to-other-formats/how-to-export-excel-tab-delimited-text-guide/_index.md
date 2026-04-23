---
category: general
date: 2026-02-26
description: cara mengekspor excel ke file txt berformat tab‑delimited menggunakan
  C#. pelajari mengekspor excel sebagai tab, mengonversi excel ke txt, dan mengekspor
  excel dengan delimiter dalam tiga langkah mudah.
draft: false
keywords:
- how to export excel
- export excel as tab
- convert excel to txt
- export excel with delimiter
- export excel range
language: id
og_description: cara mengekspor excel ke file txt berformat tab‑delimited menggunakan
  C#. tutorial ini menunjukkan cara mengekspor excel sebagai tab, mengonversi excel
  ke txt, dan mengekspor excel dengan delimiter.
og_title: cara mengekspor excel – Panduan Teks Berpemisah Tab
tags:
- csharp
- excel
- file-conversion
title: cara mengekspor excel – Panduan Teks Berpemisah Tab
url: /id/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/
---

.

Also keep markdown formatting.

Let's write translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara mengekspor excel – Tutorial C# Lengkap

Pernah bertanya-tanya **bagaimana cara mengekspor excel** ke file teks biasa tanpa kehilangan format? Mungkin Anda membutuhkan TSV (tab‑separated values) cepat untuk pipeline data, atau Anda memberi data ke sistem lama yang hanya membaca `.txt`. Bagaimanapun, Anda tidak sendirian—para pengembang sering menemui kendala ini saat memindahkan data keluar dari spreadsheet.

Kabar baiknya? Dalam tiga langkah sederhana Anda dapat **mengekspor excel sebagai tab**‑delimited text, **mengonversi excel ke txt**, dan bahkan memilih delimiter khusus jika berubah pikiran nanti. Di bawah ini Anda akan melihat contoh C# yang dapat dijalankan sepenuhnya, mengapa setiap baris penting, serta beberapa tips untuk menghindari jebakan umum.

> **Pro tip:** Pendekatan ini bekerja dengan library Aspose.Cells yang populer, tetapi konsepnya dapat diterapkan pada API Excel .NET mana pun yang menyediakan metode bergaya `ExportTable`.

## Apa yang Anda Butuhkan

- **.NET 6+** (atau .NET Framework 4.6+). Kode ini dapat dikompilasi pada runtime terbaru apa pun.
- **Aspose.Cells for .NET** (versi percobaan gratis atau berlisensi). Instal via NuGet: `dotnet add package Aspose.Cells`.
- Sebuah workbook input bernama `input.xlsx` yang ditempatkan di folder yang Anda kontrol.
- Sedikit rasa ingin tahu—tidak memerlukan pengetahuan mendalam tentang internal Excel.

Jika Anda sudah memiliki semua itu, mari langsung ke solusinya.

## Langkah 1 – Muat Workbook yang Ingin Diekspor

Pertama kita membuat objek `Workbook` yang menunjuk ke file sumber. Objek ini mewakili seluruh file Excel, termasuk semua worksheet, named range, dan formatnya.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook that contains the data to export
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*Mengapa ini penting:*  
Memuat workbook memberi Anda akses ke koleksi worksheet (`workbook.Worksheets`). Tanpa objek ini Anda tidak dapat mengakses sel, range, atau pengaturan ekspor.

> **Catatan:** Jika file Anda berada di share jaringan, tambahkan awalan `\\` atau gunakan path UNC—Aspose.Cells menangani hal ini dengan baik.

## Langkah 2 – Konfigurasikan Opsi Ekspor (Nilai String & Delimiter Tab)

Sekarang kita memberi tahu library bagaimana data harus ditulis. Dengan mengatur `ExportAsString = true` kita memaksa setiap sel diperlakukan sebagai string biasa, yang menghilangkan format angka spesifik lokal Excel. Bagian `Delimiter = "\t"` adalah inti dari **mengekspor excel sebagai tab**.

```csharp
// Step 2: Configure the export options – export values as strings and use a tab delimiter
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,   // ensures numbers become plain text, not scientific notation
    Delimiter = "\t"         // tab character – perfect for TSV files
};
```

*Mengapa ini penting:*  
Jika Anda melewatkan `ExportAsString`, sel berisi `12345` bisa menjadi `12,345` pada beberapa locale, yang merusak parser downstream. Delimiter dapat diganti dengan koma, pipa, atau karakter apa pun jika Anda kemudian memutuskan untuk **mengekspor excel dengan delimiter** selain tab.

## Langkah 3 – Ekspor Range Spesifik ke File Teks

Akhirnya, kita pilih range yang diinginkan (`A1:D10` dalam contoh ini) dan menuliskannya ke `out.txt`. Metode `ExportTable` melakukan semua pekerjaan berat: membaca sel, menerapkan opsi, dan menuliskan hasil ke disk.

```csharp
// Step 3: Export the range A1:D10 from the first worksheet to a text file
Worksheet sheet = workbook.Worksheets[0]; // first worksheet (index 0)
sheet.Cells.ExportTable("A1", "D10", @"C:\Data\out.txt", exportOptions);
```

Setelah dijalankan, Anda akan menemukan `out.txt` dengan konten seperti berikut:

```
Name    Age    City    Score
Alice   30     NY      85
Bob     25     LA      90
...
```

Setiap kolom dipisahkan oleh **tab**, sehingga siap untuk `awk`, `PowerShell`, atau alat kompatibel CSV apa pun yang menghormati tab.

### Verifikasi Cepat

Buka file yang dihasilkan di editor teks biasa (Notepad, VS Code) dan pastikan:

1. Kolom berbaris ketika Anda mengaktifkan “Show whitespace”.
2. Tidak ada kutip atau koma tambahan yang muncul.
3. Semua sel numerik tampil persis seperti di Excel (berkat `ExportAsString`).

Jika ada yang tampak tidak tepat, periksa kembali bahwa workbook sumber tidak menyembunyikan baris/kolom, dan pastikan Anda merujuk indeks worksheet yang benar.

## Variasi Umum & Kasus Edge

### Mengekspor Seluruh Worksheet

Jika Anda ingin **mengekspor range excel** yang mencakup seluruh lembar, Anda dapat menggunakan `sheet.Cells.MaxDisplayRange`:

```csharp
var maxRange = sheet.Cells.MaxDisplayRange;
sheet.Cells.ExportTable(maxRange.FirstRow, maxRange.FirstColumn,
                       maxRange.RowCount, maxRange.ColumnCount,
                       @"C:\Data\fullSheet.txt", exportOptions);
```

### Menggunakan Delimiter Berbeda

Berpindah dari tab ke pipa (`|`) semudah mengubah satu baris:

```csharp
exportOptions.Delimiter = "|"; // now we have a pipe‑delimited file
```

Itu memenuhi skenario **mengekspor excel dengan delimiter** tanpa menulis ulang kode lain.

### Menangani File Besar (> 100 MB)

Untuk workbook yang sangat besar, stream hasil ekspor untuk menghindari memuat semuanya ke memori:

```csharp
using (FileStream fs = new FileStream(@"C:\Data\largeOut.txt", FileMode.Create, FileAccess.Write))
{
    sheet.Cells.ExportTable("A1", "Z5000", fs, exportOptions);
}
```

### Mengonversi Beberapa Sheet dalam Satu Pass

Jika Anda perlu **mengonversi excel ke txt** untuk beberapa sheet, lakukan loop pada masing‑masing:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outPath = $@"C:\Data\Sheet{i + 1}.txt";
    workbook.Worksheets[i].Cells.ExportTable("A1", "D10", outPath, exportOptions);
}
```

Setiap sheet menghasilkan file TSV‑nya sendiri—praktis untuk pekerjaan batch.

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

Berikut seluruh program, siap dikompilasi. Ganti saja path file dengan milik Anda.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            string inputPath = @"C:\Data\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Set export options – strings + tab delimiter
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                Delimiter = "\t"
            };

            // 3️⃣ Export range A1:D10 from the first worksheet
            Worksheet sheet = workbook.Worksheets[0];
            string outputPath = @"C:\Data\out.txt";
            sheet.Cells.ExportTable("A1", "D10", outputPath, exportOptions);

            Console.WriteLine($"Export complete! Check {outputPath}");
        }
    }
}
```

**Output yang diharapkan:** Sebuah file bernama `out.txt` dimana setiap kolom dipisahkan oleh karakter tab, dan setiap nilai sel muncul persis seperti di Excel.

## Pertanyaan yang Sering Diajukan

- **Apakah ini bekerja dengan file .xls?**  
  Ya. Aspose.Cells secara otomatis mendeteksi format, sehingga Anda dapat menunjuk `Workbook` ke file `.xls` lama dan kode yang sama tetap berlaku.

- **Bagaimana jika data saya mengandung tab?**  
  Tab di dalam sel akan dipertahankan, yang dapat merusak parser TSV. Dalam kasus tersebut, pertimbangkan mengganti delimiter ke pipa (`|`) dengan memperbarui `exportOptions.Delimiter`.

- **Bisakah saya mengekspor formula alih‑alih nilai?**  
  Atur `exportOptions.ExportAsString = false` dan gunakan overload `ExportTableOptions` yang mencakup `ExportFormula = true`. Output akan berisi teks formula mentah.

- **Apakah ada cara untuk melewatkan baris tersembunyi?**  
  Ya. Atur `exportOptions.ExportHiddenRows = false` (defaultnya `true`). Baris tersembunyi tidak akan disertakan dalam file teks akhir.

## Kesimpulan

Sekarang Anda memiliki resep solid dan siap produksi untuk **mengekspor data excel** sebagai file teks ber‑delimiter tab, cara **mengekspor excel sebagai tab**, dan cara **mengonversi excel ke txt** dengan kontrol penuh atas delimiter dan pemilihan range. Dengan memanfaatkan metode `ExportTable` milik Aspose.Cells, Anda menghindari pembuatan CSV manual, mempertahankan integritas data, dan menjaga kode tetap bersih.

Siap untuk tantangan berikutnya? Coba:

- Mengekspor langsung ke `MemoryStream` untuk API web.  
- Menambahkan baris header secara dinamis berdasarkan konten baris pertama.  
- Mengintegrasikan rutin ini ke Azure Function yang memantau bucket storage untuk unggahan Excel baru.

Cobalah, ubah delimiter sesuai kebutuhan, dan biarkan data mengalir ke mana pun Anda perlukan. Selamat coding!  

<img src="export-excel.png" alt="how to export excel example" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}