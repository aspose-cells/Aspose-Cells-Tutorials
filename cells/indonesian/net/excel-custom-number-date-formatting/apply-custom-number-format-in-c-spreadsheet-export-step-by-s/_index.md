---
category: general
date: 2026-04-07
description: Terapkan format angka khusus pada sel spreadsheet dan pelajari cara memformat
  angka dalam spreadsheet saat mengekspor nilai sel dengan C#. Panduan cepat dan lengkap.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: id
og_description: Terapkan format angka khusus pada sel spreadsheet dan ekspor sebagai
  string yang diformat. Pelajari cara memformat angka di spreadsheet dan mengekspor
  nilai sel.
og_title: Terapkan Format Angka Kustom – Tutorial Ekspor C# Lengkap
tags:
- C#
- Spreadsheet
- Number Formatting
title: Terapkan Format Angka Kustom dalam Ekspor Spreadsheet C# – Panduan Langkah
  demi Langkah
url: /id/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Terapkan Format Angka Kustom dalam Ekspor Spreadsheet C# – Tutorial Lengkap

Pernah perlu **apply custom number format** pada sebuah sel dan kemudian mengambil string yang sudah diformat itu dari spreadsheet? Anda tidak sendirian. Banyak pengembang mengalami kebingungan ketika nilai mentah yang keluar bukan string yang cantik dan sesuai locale yang mereka harapkan. Dalam panduan ini kami akan menunjukkan secara tepat cara **format number in spreadsheet** pada sel spreadsheet dan cara mengekspor nilai sel sebagai string yang diformat menggunakan perpustakaan spreadsheet C# yang populer.

Pada akhir tutorial Anda akan dapat **apply custom number format** pada sel numerik apa pun, mengekspor hasilnya dengan `ExportTable`, dan melihat output yang tepat seperti yang Anda harapkan untuk ditampilkan di UI atau laporan. Tidak perlu dokumen eksternal—semuanya ada di sini.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga berfungsi pada .NET Framework 4.7+)
- Referensi ke perpustakaan spreadsheet yang menyediakan `Workbook`, `Worksheet`, dan `ExportTableOptions` (misalnya **Aspose.Cells** atau **GemBox.Spreadsheet**; API yang ditampilkan cocok dengan Aspose.Cells)
- Pengetahuan dasar C#—jika Anda dapat menulis `Console.WriteLine`, Anda siap melanjutkan

> **Pro tip:** Jika Anda menggunakan perpustakaan yang berbeda, nama properti biasanya serupa (`NumberFormat`, `ExportAsString`). Cukup petakan sesuai kebutuhan.

## Apa yang dibahas dalam tutorial ini

1. Membuat workbook dan memilih worksheet pertama.  
2. Menyisipkan nilai numerik ke dalam sel.  
3. Menyiapkan `ExportTableOptions` untuk **apply custom number format** dan mengembalikan string.  
4. Mengekspor sel dan mencetak hasil yang diformat.  
5. Penanganan kasus tepi – bagaimana jika sel berisi formula atau nilai null?

Mari kita mulai.

![contoh apply custom number format](https://example.com/image.png "apply custom number format")

## Langkah 1 – Buat workbook dan dapatkan worksheet pertama

Hal pertama yang Anda butuhkan adalah objek workbook. Anggap saja itu sebagai file Excel yang Anda buka di aplikasi Office. Setelah Anda memilikinya, ambil sheet pertama—banyak tutorial memulai di sana karena membuat contoh tetap singkat.

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**Mengapa ini penting:** Sebuah workbook baru memberi Anda kanvas bersih, memastikan tidak ada format tersembunyi yang mengganggu **custom number format** kita nanti.

## Langkah 2 – Masukkan nilai numerik ke sel B2 (sel yang akan kami ekspor)

Sekarang kita membutuhkan sesuatu untuk diformat. Sel **B2** adalah tempat yang nyaman—mudah dirujuk dan cukup jauh dari sudut default A1 untuk menghindari penimpaan tidak sengaja.

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**Bagaimana jika nilainya adalah formula?**  
Jika Anda kemudian mengganti nilai mentah dengan formula (misalnya `=SUM(A1:A10)`), rutin ekspor tetap akan menghormati format angka yang kami terapkan pada langkah berikutnya, karena format terikat pada sel, bukan pada tipe nilai.

## Langkah 3 – Konfigurasikan opsi ekspor untuk menerima nilai sebagai string yang diformat

Berikut inti tutorial: kami memberi tahu perpustakaan untuk **apply custom number format** saat mengekspor. String `NumberFormat` mengikuti pola yang sama seperti yang Anda gunakan di kategori “Custom” Excel.

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` memastikan metode mengembalikan `string` alih-alih double mentah.  
- `NumberFormat = "#,##0.00;(#,##0.00)"` meniru pola Excel: koma untuk ribuan, dua tempat desimal, dan tanda kurung untuk angka negatif.

> **Mengapa menggunakan format kustom?** Ini menjamin konsistensi lintas budaya (mis., pemisah angka US vs. Eropa) dan memungkinkan Anda menyematkan gaya bisnis khusus seperti tanda kurung akuntansi.

## Langkah 4 – Ekspor sel menggunakan opsi yang telah dikonfigurasi

Sekarang kami benar‑benar menarik nilai dari worksheet, membiarkan perpustakaan melakukan pekerjaan berat dalam menerapkan format yang kami definisikan.

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**Kasus tepi – sel kosong:** Jika `B2` kosong, `formattedResult` akan menjadi `null`. Anda dapat melindungi dengan pemeriksaan null sederhana sebelum mencetak.

## Langkah 5 – Tampilkan string yang diformat

Akhirnya, kami menulis hasil ke konsol. Dalam aplikasi nyata Anda mungkin menyalurkan string ini ke PDF, email, atau label UI.

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**Output yang diharapkan**

```
1,234.56
```

Jika Anda mengubah nilai mentah menjadi `-9876.54`, format yang sama akan memberi Anda `(9,876.54)`—tepat seperti yang dibutuhkan banyak laporan akuntansi.

## Contoh lengkap yang dapat dijalankan

Berikut program lengkap yang dapat Anda salin‑tempel ke proyek konsol baru. Program ini dapat dikompilasi dan dijalankan apa adanya, dengan asumsi Anda telah menambahkan paket NuGet yang sesuai untuk perpustakaan spreadsheet.

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### Pemeriksaan cepat

- **Apakah dapat dikompilasi?** Ya—pastikan DLL `Aspose.Cells` (atau yang setara) direferensikan.  
- **Apakah akan berfungsi dengan budaya lain?** String format tidak bergantung pada budaya; perpustakaan menghormati pola yang Anda berikan. Jika Anda memerlukan pemisah khusus locale, Anda dapat menambahkan penanganan `CultureInfo` sebelum ekspor.

## Pertanyaan umum & variasi

### Cara **format number in spreadsheet** menggunakan pola berbeda?

Ganti string `NumberFormat`. Misalnya, untuk menampilkan persentase dengan satu tempat desimal:

```csharp
NumberFormat = "0.0%";
```

### Bagaimana jika saya perlu **how to export cell value** sebagai HTML alih‑alih teks biasa?

Sebagian besar perpustakaan memiliki overload yang menerima tipe ekspor. Anda akan mengatur `ExportAsString = true` dan menambahkan `ExportHtml = true` (atau serupa). Prinsipnya tetap sama: definisikan format, lalu pilih representasi output.

### Bisakah saya menerapkan format ke seluruh rentang, bukan hanya satu sel?

Tentu saja. Anda dapat menetapkan `NumberFormat` ke objek `Style` lalu menerapkan gaya itu ke `Range`. Panggilan ekspor tetap tidak berubah; ia akan mengambil gaya secara otomatis.

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### Apa yang terjadi ketika sel berisi formula?

Rutin ekspor mengevaluasi formula terlebih dahulu, lalu memformat nilai numerik yang dihasilkan. Tidak diperlukan kode tambahan—pastikan `Calculate` telah dipanggil jika Anda menonaktifkan perhitungan otomatis.

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## Kesimpulan

Anda kini tahu cara **apply custom number format** ke sel spreadsheet, **format number in spreadsheet** dalam konteks apa pun, dan **how to export cell value** sebagai string siap‑tampil. Contoh kode singkat di atas mencakup setiap langkah—dari pembuatan workbook hingga output akhir—sehingga Anda dapat langsung menggunakannya dalam proyek produksi.

Siap untuk tantangan berikutnya? Cobalah menggabungkan teknik ini dengan **how to format numeric cell** untuk tanggal, simbol mata uang, atau pemformatan bersyarat. Atau jelajahi mengekspor beberapa sel sebagai CSV sambil mempertahankan format kustom masing‑masing. Langit adalah batasnya, dan dengan dasar ini Anda memiliki fondasi yang kuat.

Selamat coding, dan jangan lupa bereksperimen—kadang‑kadang jawaban terbaik muncul ketika Anda mengutak‑atik string format sedikit saja!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}