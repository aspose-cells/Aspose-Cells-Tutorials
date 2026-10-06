---
category: general
date: 2026-06-17
description: Atur format tanggal di Excel menggunakan C# serta atur latar belakang
  sel, terapkan warna latar depan, dan beri warna kolom Excel saat impor. Pelajari
  langkah demi langkah.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: id
og_description: Atur format tanggal di Excel dengan C# sambil mengatur latar belakang
  sel, menerapkan warna latar depan, dan mewarnai kolom Excel saat impor. Tutorial
  lengkap.
og_title: Mengatur format tanggal di Excel dengan C# – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: Atur format tanggal di Excel dengan C# – Panduan Lengkap Pemformatan Impor
url: /id/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Atur format tanggal di Excel dengan C# – Panduan Lengkap Format Impor

Pernah perlu **mengatur format tanggal** di lembar Excel yang dihasilkan dari kode C#, tetapi juga ingin kolom memiliki latar belakang atau warna teks khusus? Anda tidak sendirian. Dalam banyak skenario pelaporan Anda mengambil `DataTable` dari basis data, menaruhnya ke lembar kerja, dan kemudian berusaha membuat tanggal terlihat benar serta kolom menonjol dengan warna yang tepat.  

Dalam tutorial ini kami akan membahas solusi bersih, end‑to‑end yang **mengatur format tanggal**, **mengatur latar belakang sel**, **menerapkan warna depan**, dan bahkan **memberi warna pada kolom Excel** saat mengimpor data. Pada akhir tutorial Anda akan memiliki pola yang dapat digunakan kembali untuk menangani **excel import formatting** tanpa trial‑and‑error yang biasa.

> **Apa yang Anda perlukan**  
> * .NET 6+ (atau .NET Framework 4.7+)  
> * Aspose.Cells for .NET (versi percobaan gratis cukup untuk pengujian)  
> * Sumber `DataTable` – kueri ADO.NET apa pun dapat digunakan  
> * Visual Studio atau IDE favorit Anda  

Mari kita mulai.

---

## Gambaran Umum Solusi

Kami akan membagi masalah menjadi tiga bagian logis:

1. **Mengambil data sumber** – sebuah `DataTable` dengan baris yang ingin Anda ekspor.  
2. **Membuat gaya khusus per kolom** – satu gaya untuk kolom tanggal, satu lagi untuk kolom teks, plus gaya tambahan apa pun yang Anda inginkan.  
3. **Mengimpor tabel dengan gaya** – gunakan `Worksheet.Cells.ImportDataTable` sehingga setiap kolom mewarisi gaya yang telah Anda siapkan.

Mengapa pendekatan ini? Karena Aspose.Cells memungkinkan Anda melampirkan array `Style` langsung ke panggilan `ImportDataTable`, artinya Anda tidak memerlukan proses kedua untuk menerapkan format lagi. Ini lebih cepat, kurang rawan kesalahan, dan membuat kode Anda tetap rapi.

---

## Langkah 1: Mengambil Data untuk Diekspor

Pertama-tama – Anda memerlukan sebuah `DataTable`. Dalam proyek nyata Anda mungkin memanggil prosedur tersimpan atau menggunakan Entity Framework untuk mengisinya, tetapi untuk ilustrasi kami akan membuat tabel sederhana dengan kolom tanggal dan teks.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **Pro tip:** Jika sumber Anda menggunakan tanggal nullable, pastikan tipe kolomnya `typeof(DateTime?)` – Aspose tetap akan menghormati format yang Anda tetapkan nanti.

---

## Langkah 2: Menyiapkan Array Gaya – Satu per Kolom

Sekarang kami membuat `Style[]` yang panjangnya sesuai dengan jumlah kolom di `DataTable`. Setiap entri akan menyimpan format untuk kolom masing‑masing.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 Atur Format Tanggal untuk Kolom Pertama

Kolom pertama (`OrderDate`) harus ditampilkan sebagai “MM/dd/yyyy”. Aspose menggunakan indeks format angka bawaan 14 untuk tanggal singkat, tetapi Anda juga dapat memberikan string format khusus jika lebih suka.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Mengapa ini penting:** Excel menyimpan tanggal sebagai angka seri. Dengan menetapkan format angka, Anda memberi tahu Excel untuk menampilkan seri tersebut sebagai tanggal yang dapat dibaca manusia alih‑alih angka mentah.

### 2.2 Atur Latar Belakang Sel untuk Kolom Kedua

Mari beri kolom `CustomerName` latar belakang biru muda. Di sinilah **set cell background** berperan.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **Catatan:** Tanpa mengatur `Pattern` ke `Solid`, warna depan tidak akan muncul karena pola default adalah “None”.

### 2.3 Terapkan Warna Depan (Teks) – Tambahan Opsional

Jika Anda juga ingin teksnya berwarna kontras, Anda dapat menyesuaikan gaya yang sama:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

Itu memenuhi kebutuhan **apply foreground color** sambil mempertahankan latar belakang kolom.

---

## Langkah 3: Mengimpor DataTable dengan Gaya yang Didefinisikan

Dengan gaya siap, langkah terakhir adalah satu baris kode yang mengimpor data dan menerapkan gaya per kolom.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Cara kerjanya:** Aspose membaca array `columnStyles` dan memetakan setiap `Style` ke indeks kolom yang bersesuaian. Baris header mewarisi gaya default kecuali Anda menyediakan gaya terpisah untuk baris 0.

### 3.1 Simpan Workbook

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

Jalankan program, buka *FormattedReport.xlsx*, dan Anda akan melihat:

- Kolom **OrderDate** ditampilkan sebagai tanggal (misalnya `06/15/2026`).  
- Kolom **CustomerName** dengan isi berwarna biru muda dan teks biru tua.  

Itulah seluruh alur kerja **excel import formatting** dalam kurang dari 30 baris C#.

---

## Ringkasan Langkah‑per‑Langkah (dengan Alasan)

| Langkah | Apa yang Anda lakukan | Mengapa penting |
|------|-------------|----------------|
| **Retrieve data** | Panggil `GetData()` untuk mengisi `DataTable`. | Menyediakan sumber terstruktur yang dapat langsung diproses Aspose. |
| **Create style array** | Alokasikan `Style[]` yang sesuai dengan jumlah kolom. | Memungkinkan styling per kolom dalam satu panggilan impor. |
| **Set date format** | `columnStyles[0].Number = 14;` | Memastikan tanggal ditampilkan dengan benar di Excel. |
| **Set background color** | `ForegroundColor = LightBlue; Pattern = Solid;` | Menyorot kolom, memenuhi **set cell background**. |
| **Apply foreground color** | `Font.Color = DarkBlue;` | Meningkatkan keterbacaan dan memenuhi **apply foreground color**. |
| **Import with styles** | `ImportDataTable(..., columnStyles);` | Impor satu kali yang menghormati semua format. |
| **Save workbook** | `wb.Save(...);` | Menyimpan hasil untuk pengguna selanjutnya. |

---

## Menangani Kasus Tepi & Pertanyaan Umum

### Bagaimana jika saya memiliki lebih dari dua kolom?

Perluas saja array `columnStyles` dan tetapkan `Style` ke setiap indeks yang Anda perlukan. Indeks yang tidak ditetapkan akan kembali ke gaya default, yang sepenuhnya dapat diterima.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### Bagaimana cara memformat kolom sebagai mata uang?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### Bisakah saya mengubah gaya baris header secara terpisah?

Ya. Setelah impor, Anda dapat mengambil baris pertama dan menerapkan gaya yang berbeda:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### Bagaimana jika DataTable berisi tanggal null?

Aspose akan membiarkan sel tersebut kosong. Jika Anda lebih suka placeholder seperti “N/A”, Anda dapat memproses tabel terlebih dahulu:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

Kemudian sesuaikan gaya untuk menampilkan format khusus yang menampilkan “N/A” untuk nilai sentinel.

---

## Contoh Kerja Lengkap

Berikut adalah program lengkap yang siap disalin‑tempel. Jalankan sebagai aplikasi konsol, dan Anda akan mendapatkan file Excel yang terformat dengan baik.



## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Set Font Color in Excel Cells using Aspose.Cells for .NET](/cells/english/net/formatting/setting-font-color/)
- [Set Font Color in .NET Excel with Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Set Excel Column Widths in Pixels Using Aspose.Cells for .NET | Step-by-Step Guide](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}