---
category: general
date: 2026-05-30
description: Pelajari cara menambahkan warna baris bergantian di lembar kerja C#,
  mengatur latar belakang sel dengan pola isian solid, dan menyesuaikan gaya sel lembar
  kerja dengan mudah.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: id
og_description: Warna baris bergantian di lembar kerja C# menjadi mudah. Pelajari
  cara mengatur latar belakang sel, gunakan pola isian solid, dan kuasai gaya sel
  lembar kerja.
og_title: Warna Baris Bergantian di Lembar Kerja C# – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Warna Baris Bergantian di Lembar Kerja C# – Panduan Lengkap
url: /id/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Warna Baris Bergantian di Worksheet C# – Panduan Lengkap

Pernah bertanya-tanya bagaimana membuat ekspor Excel Anda terlihat rapi dengan menggunakan **alternating row colors**? Anda tidak sendirian—para pengembang terus-menerus menanyakan cara *add background color* ke baris tanpa menulis jutaan baris kode.  

Dalam tutorial ini kami akan membahas cara sederhana untuk **set cell background** pada setiap baris, menerapkan **solid fill pattern**, dan mengontrol **worksheet cell style** sehingga hasilnya dapat dibaca dan tampak menarik secara visual.

## Apa yang Akan Anda Pelajari

- Mengambil data ke dalam `DataTable` (atau sumber tabular apa pun).  
- Membangun array objek `Style` yang bergantian antara dua warna.  
- Mengimpor `DataTable` ke dalam worksheet sambil menerapkan gaya tersebut.  
- Memverifikasi output dan menyesuaikan warna atau pola jika diperlukan.  

Tidak diperlukan alat eksternal selain lingkungan .NET dan perpustakaan spreadsheet (kami akan menggunakan **Aspose.Cells** dalam contoh) . Pada akhirnya Anda akan memiliki metode yang dapat digunakan kembali yang dapat Anda masukkan ke dalam pipeline pelaporan apa pun.

---

## Langkah 1: Mengambil Data Sumber sebagai `DataTable`

Pertama-tama—tanpa data tidak ada yang dapat di-styling. Di bawah ini adalah helper kecil yang membangun `DataTable` dengan baris contoh. Dalam proyek nyata Anda akan menggantinya dengan panggilan basis data atau parser CSV.

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **Mengapa ini penting:** Memiliki data dalam `DataTable` memungkinkan mesin worksheet *import* dalam satu panggilan, secara otomatis mempertahankan nama kolom dan tipe data.

## Langkah 2: Membuat Gaya **Alternating Row Colors**

Sekarang kami akan menghasilkan array objek `Style`—satu per baris—sehingga baris genap mendapatkan nuansa kuning muda sementara baris ganjil menerima warna cyan lembut. Ini adalah inti dari teknik **alternating row colors**.

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### Mengapa Menggunakan **Solid Fill Pattern**?

`Property` `Pattern` memberi tahu mesin cara merender warna. Pengisian `Solid` menjamin seluruh latar belakang sel terisi, menghilangkan garis kisi tipis yang mungkin muncul. Ini adalah cara paling umum untuk **set cell background** ketika Anda menginginkan tampilan bersih.

## Langkah 3: Mengimpor `DataTable` dengan Gaya yang Disiapkan

Dengan array gaya siap, panggilan impor menjadi satu baris. Aspose.Cells akan secara otomatis menerapkan gaya yang sesuai ke setiap baris.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **Apa yang terjadi di balik layar?**  
> Perpustakaan mengiterasi setiap baris, menyalin nilai ke sel, dan kemudian menerapkan `Style` yang cocok dari `rowStyles`. Karena kami sudah mendefinisikan **solid fill pattern**, setiap sel dalam baris mewarisi warna latar belakang yang sama, memberi Anda **alternating row colors** yang sempurna.

## Langkah 4: Simpan Workbook dan Verifikasi Hasil

Simpan cepat memungkinkan Anda membuka file di Excel (atau penampil kompatibel lainnya) dan melihat efeknya.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

Saat Anda membuka file, baris 1, 3, 5… akan berwarna kuning muda, sementara baris 2, 4, 6… akan berwarna cyan muda. Header kolom tetap putih, membuat data menonjol.

![Worksheet menampilkan warna baris bergantian](/images/alternating-row-colors.png "Tangkapan layar worksheet dengan warna baris bergantian")

*Image alt text:* **alternating row colors** tangkapan layar worksheet di mana latar belakang setiap baris bergantian antara kuning muda dan cyan muda.

## Langkah 5: Kustomisasi Lebih Lanjut (Opsional)

### Ubah Warnanya

Jika merek Anda menggunakan nuansa berbeda, cukup ganti `Color.LightYellow` dan `Color.LightCyan` dengan `System.Drawing.Color` apa pun yang Anda suka. Misalnya:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### Gunakan **Background Type** yang Berbeda

Meskipun `BackgroundType.Solid` adalah yang paling umum, Anda dapat bereksperimen dengan `BackgroundType.Gray125`, `BackgroundType.Horizontal`, atau pola apa pun yang didukung perpustakaan. Ini mengubah tekstur visual sambil tetap **adding background color**.

### Terapkan **Worksheet Cell Style** ke Kolom Tertentu

Terkadang Anda hanya menginginkan efek bergantian pada kolom data, meninggalkan kolom pertama (mis., ID) tidak tersentuh. Buat gaya terpisah untuk kolom itu dan tetapkan setelah impor:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## Kesimpulan

Anda sekarang memiliki solusi lengkap dan dapat digunakan kembali untuk **alternating row colors** di worksheet C#. Dengan membangun array objek `Style`, **setting cell background** dengan **solid fill pattern**, dan mengimpor `DataTable` dalam satu panggilan, Anda dapat menghasilkan laporan berpenampilan profesional dengan kode minimal.

Dari sini Anda mungkin:

- **Add background color** ke baris header untuk penekanan ekstra.  
- Menggabungkan teknik ini dengan conditional formatting untuk petunjuk visual dinamis.  
- Mengeksplorasi properti **worksheet cell style** lainnya seperti font, border, atau format angka.

Cobalah dalam rutinitas ekspor berikutnya—pengguna Anda akan berterima kasih atas spreadsheet yang lebih bersih dan lebih mudah dibaca. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

- [Atur Tinggi Baris di Worksheet dengan Aspose.Cells untuk .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Konversi Nama Sel Excel ke Indeks Baris dan Kolom Menggunakan Aspose.Cells untuk .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Atur Warna Tab Worksheet di Excel Menggunakan Aspose.Cells .NET - Panduan Komprehensif](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}