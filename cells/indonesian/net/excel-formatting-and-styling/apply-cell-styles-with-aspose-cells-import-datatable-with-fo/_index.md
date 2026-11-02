---
category: general
date: 2026-06-05
description: Terapkan gaya sel saat menggunakan impor Aspose.Cells. Pelajari cara
  mengimpor DataTable dengan pemformatan, menata baris, dan menjaga lembar kerja tetap
  rapi.
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: id
og_description: Terapkan gaya sel saat mengimpor DataTable ke dalam lembar kerja Aspose.Cells.
  Panduan langkah demi langkah dengan kode lengkap dan tips.
og_title: Terapkan Gaya Sel dengan Aspose.Cells – Impor DataTable
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  headline: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  type: TechArticle
- description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  name: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  steps:
  - name: How It Works
    text: 1. **Headers** – Because we passed `true`, Aspose writes “Name” and “Score”
      into the first row. 2. **Data Rows** – Each subsequent row receives the corresponding
      style from `importStyles`. 3. **Performance** – The method streams the data
      directly into the worksheet, which is faster than looping cell
  - name: What if My DataTable Has More Columns Than Styles?
    text: Aspose will apply the last style in the array to any extra columns. To avoid
      unexpected colors, always match the array length to the column count, or pass
      `null` for columns you don’t want styled.
  - name: Can I Apply Different Styles to Specific Rows?
    text: 'Absolutely. After the import, you can loop through rows and assign new
      `Style` objects based on conditions (e.g., highlight scores > 90 in green).
      Here’s a quick snippet:'
  - name: Does This Work with Large DataSets?
    text: Yes. `ImportDataTable` streams data efficiently, and applying a static style
      array adds negligible overhead. For millions of rows, consider using `ImportDataTable`
      in chunks or leveraging `Cells.ImportDataTable` with a `DataReader` for even
      better memory usage.
  - name: How Do I Preserve Existing Formatting in the Worksheet?
    text: If the target range already has formatting you want to keep, set the `ImportDataTable`
      overload’s `importOptions` parameter (`ImportTableOptions`) and tweak `ImportDataTableOptions.PreserveCellFormatting`.
      The default behavior overwrites styles with the ones you supply.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DataTable
title: Terapkan Gaya Sel dengan Aspose.Cells – Impor DataTable dengan Pemformatan
url: /id/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Terapkan Gaya Sel dengan Aspose.Cells – Impor DataTable dengan Pemformatan

Pernah bertanya-tanya bagaimana cara **menerapkan gaya sel** ketika Anda mengambil `DataTable` ke dalam lembar Excel? Anda tidak sendirian. Dalam banyak skenario pelaporan Anda membutuhkan data yang terlihat bagus langsung dari awal—tanpa pemformatan manual nanti. Kabar baiknya, Aspose.Cells membuatnya mudah untuk **mengimpor dengan pemformatan** sehingga baris Anda dapat berwarna merah atau biru, tebal, atau apa saja yang Anda suka.

Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang menunjukkan **cara mengimpor datatable** ke dalam worksheet **dengan gaya sel** yang diterapkan. Pada akhir tutorial Anda akan memiliki aplikasi konsol C# siap‑jalankan yang membuat workbook, memberi gaya pada dua kolom pertama, dan menyimpan file—semua menggunakan API `aspose cells import`.

## Apa yang Akan Anda Pelajari

- Menyiapkan Aspose.Cells dalam proyek .NET  
- Membuat contoh `DataTable` yang meniru data dunia nyata  
- Mendefinisikan objek `Style` untuk font merah dan biru  
- Menggunakan `Worksheet.Cells.ImportDataTable` untuk **mengimpor worksheet datatable** sambil menerapkan gaya  
- Memverifikasi hasil dan menyimpan workbook  

Tanpa alat eksternal, hanya C# murni dan Aspose.Cells. Mari kita mulai.

## Prasyarat

Sebelum kita menyelam ke kode, pastikan Anda memiliki hal berikut:

| Requirement | Mengapa penting |
|-------------|-----------------|
| .NET 6.0 or later | Aspose.Cells 23.x menargetkan .NET Standard 2.0+, jadi .NET 6 memberikan Anda fitur runtime terbaru. |
| Aspose.Cells for .NET (NuGet) | Pustaka ini menyediakan metode `Workbook`, `Worksheet`, `Style`, dan `ImportDataTable` yang kami butuhkan. |
| Pengetahuan dasar C# | Anda akan memahami kelas, array, dan pernyataan `using`. |
| IDE (Visual Studio, VS Code, Rider) | Editor apa pun dapat digunakan, tetapi Anda perlu memulihkan paket NuGet. |

Anda dapat menginstal paket tersebut dari baris perintah:

```bash
dotnet add package Aspose.Cells
```

## Langkah 1: Buat Workbook Baru dan Akses Worksheet Pertama

Pertama-tama—mari buat `Workbook` dan ambil lembar pertama. Anggap workbook sebagai buku catatan kosong; worksheet pertama adalah halaman yang akan kita tulis pada.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create a new workbook (equivalent to a new Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Pro tip:** Jika Anda pernah membutuhkan beberapa lembar, cukup tambahkan dengan `wb.Worksheets.Add()` dan referensikan mereka dengan nama atau indeks.

## Langkah 2: Siapkan Contoh DataTable (Cara Mengimpor DataTable)

Sekarang kita membutuhkan sesuatu untuk diimpor. Dalam proyek nyata Anda akan memanggil DB, tetapi untuk kejelasan kita akan membuat `DataTable` di memori.

```csharp
        // Build a sample DataTable with two columns: Name and Score
        DataTable dataTable = new DataTable("Results");
        dataTable.Columns.Add("Name", typeof(string));
        dataTable.Columns.Add("Score", typeof(int));

        // Populate rows – imagine these came from a query
        dataTable.Rows.Add("Alice", 85);
        dataTable.Rows.Add("Bob", 92);
        dataTable.Rows.Add("Charlie", 78);
        dataTable.Rows.Add("Diana", 91);
```

> **Mengapa ini penting:** Memiliki `DataTable` memungkinkan kami menguji alur **aspose cells import** tanpa ketergantungan eksternal.

## Langkah 3: Definisikan Gaya yang Akan Diterapkan pada Sel yang Diimpor

Inilah tempat keajaiban terjadi. Kami akan membuat dua objek `Style`: satu dengan font merah, satu lagi dengan font biru. Ini akan diterapkan per kolom selama proses impor.

```csharp
        // Define an array of styles – one per column
        Style[] importStyles = new Style[2];

        // Style for the first column (Name) – red text
        Style redStyle = wb.CreateStyle();
        redStyle.Font.Color = Color.Red;
        importStyles[0] = redStyle;

        // Style for the second column (Score) – blue text
        Style blueStyle = wb.CreateStyle();
        blueStyle.Font.Color = Color.Blue;
        importStyles[1] = blueStyle;
```

> **Perhatian:** Panjang `importStyles` harus sesuai dengan jumlah kolom yang Anda impor, jika tidak Aspose akan melempar `ArgumentException`.

## Langkah 4: Impor DataTable ke Worksheet **dengan Pemformatan**

Sekarang kita menggabungkan semuanya. Overload `ImportDataTable` yang kami gunakan menerima array `Style[]`, memungkinkan kami **menerapkan gaya sel** saat data masuk ke lembar.

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### Cara Kerjanya

1. **Headers** – Karena kami mengirim `true`, Aspose menulis “Name” dan “Score” ke baris pertama.  
2. **Data Rows** – Setiap baris berikutnya menerima gaya yang sesuai dari `importStyles`.  
3. **Performance** – Metode ini menyalurkan data langsung ke worksheet, yang lebih cepat daripada mengulang sel per sel.

## Langkah 5: Verifikasi Hasil dan Simpan Workbook

Mari lihat beberapa sel pertama untuk memastikan gaya telah diterapkan, lalu tulis file ke disk.

```csharp
        // Optional: Quick sanity check – print the first row's values
        Console.WriteLine("Header Row:");
        Console.WriteLine($"{worksheet.Cells[0, 0].StringValue} | {worksheet.Cells[0, 1].StringValue}");

        // Save the workbook to an Excel file
        string outputPath = "StyledImport.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Ketika Anda membuka **StyledImport.xlsx**, Anda akan melihat:

- Kolom “Name” dengan teks **merah**.  
- Kolom “Score” dengan teks **biru**.  
- Header kolom dengan gaya default (Anda dapat memberi gaya pada mereka juga, tetapi itu tutorial lain).

![Contoh penerapan gaya sel](https://example.com/images/apply-cell-styles.png "Menerapkan gaya sel di Aspose.Cells")

> **Catatan:** Gambar di atas menunjukkan tampilan akhir. Atribut `alt` berisi kata kunci utama, memenuhi persyaratan SEO.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana Jika DataTable Saya Memiliki Lebih Banyak Kolom Daripada Gaya?

Aspose akan menerapkan gaya terakhir dalam array ke kolom tambahan apa pun. Untuk menghindari warna yang tidak diharapkan, selalu sesuaikan panjang array dengan jumlah kolom, atau berikan `null` untuk kolom yang tidak ingin Anda beri gaya.

### Bisakah Saya Menerapkan Gaya Berbeda pada Baris Tertentu?

Tentu saja. Setelah impor, Anda dapat melakukan loop melalui baris dan menetapkan objek `Style` baru berdasarkan kondisi (misalnya, menyorot skor > 90 dengan hijau). Berikut cuplikan singkat:

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++) // start at 1 to skip header
{
    int score = worksheet.Cells[i, 1].IntValue;
    if (score > 90)
    {
        Style highScore = wb.CreateStyle();
        highScore.Font.Color = Color.Green;
        worksheet.Cells[i, 1].SetStyle(highScore);
    }
}
```

### Apakah Ini Bekerja dengan DataSet Besar?

Ya. `ImportDataTable` menyalurkan data secara efisien, dan menerapkan array gaya statis menambah beban yang dapat diabaikan. Untuk jutaan baris, pertimbangkan menggunakan `ImportDataTable` dalam potongan atau memanfaatkan `Cells.ImportDataTable` dengan `DataReader` untuk penggunaan memori yang lebih baik.

### Bagaimana Saya Menjaga Pemformatan yang Ada di Worksheet?

Jika rentang target sudah memiliki pemformatan yang ingin Anda pertahankan, atur parameter `importOptions` pada overload `ImportDataTable` (`ImportTableOptions`) dan sesuaikan `ImportDataTableOptions.PreserveCellFormatting`. Perilaku default menimpa gaya dengan yang Anda berikan.

## Ringkasan: Apa yang Kami Capai

- **Menerapkan gaya sel** selama operasi **aspose cells import**.  
- Mendemonstrasikan **impor dengan pemformatan** dengan memberikan array `Style[]`.  
- Menunjukkan **cara mengimpor datatable** ke dalam worksheet dan menyimpan hasilnya.  
- Membahas kasus tepi seperti jumlah gaya yang tidak cocok dan gaya baris bersyarat.

Semua ini dilakukan dalam satu aplikasi konsol yang mandiri—tanpa skrip eksternal, tanpa mengutak‑atik Excel secara manual. Anda kini memiliki fondasi yang kuat untuk fitur pelaporan atau ekspor data apa pun yang membutuhkan output Excel yang rapi.

## Langkah Selanjutnya

Siap untuk melangkah lebih jauh? Berikut beberapa ide yang membangun dari apa yang baru saja Anda pelajari:

- **Gaya baris header** (mis., tebal, warna latar).  
- **Terapkan pemformatan bersyarat** menggunakan `Worksheet.Cells[i, j].ConditionalFormattingCollection`.  
- **Ekspor ke format lain** seperti CSV atau PDF dengan `wb.Save("file.pdf", SaveFormat.Pdf)`.  
- **Gabungkan beberapa DataTable** ke dalam satu workbook, masing‑masing pada sheetnya, menggunakan pendekatan gaya yang sama.

Jika Anda mengalami kendala, tinggalkan komentar atau periksa dokumentasi resmi Aspose tentang `ImportDataTable`. Selamat coding, dan nikmati file Excel yang bergaya indah!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengimpor DataTable ke Excel Menggunakan Aspose.Cells untuk .NET (Panduan Langkah-demi-Langkah)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Cara Menetapkan Gaya Font di Excel Menggunakan Aspose.Cells untuk .NET (Panduan Langkah-demi-Langkah)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [Cara Menerapkan Bayangan Teks di Excel Menggunakan Aspose.Cells .NET: Panduan Langkah-demi-Langkah](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}