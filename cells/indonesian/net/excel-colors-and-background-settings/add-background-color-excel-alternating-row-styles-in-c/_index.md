---
category: general
date: 2026-04-07
description: Tambahkan warna latar belakang pada baris Excel menggunakan C#. Pelajari
  cara menerapkan warna baris bergantian, mengatur gaya latar belakang solid, dan
  mengimpor datatable ke Excel dalam satu alur kerja.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: id
og_description: Tambahkan warna latar belakang pada baris Excel dengan C#. Panduan
  ini menunjukkan cara menerapkan warna baris bergantian, mengatur latar belakang
  solid, dan mengimpor datatable ke Excel secara efisien.
og_title: Menambahkan warna latar belakang di Excel – Gaya Baris Bergantian dalam
  C#
tags:
- C#
- Excel
- DataTable
- Styling
title: Menambahkan warna latar belakang di Excel – Gaya Baris Bergantian dalam C#
url: /id/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menambahkan warna latar belakang excel – Gaya Baris Bergantian di C#

Pernah membutuhkan untuk **add background color excel** baris tetapi tidak yakin cara melakukannya tanpa ribuan baris kode yang rumit? Anda tidak sendirian—sebagian besar pengembang mengalami hal itu ketika pertama kali mencoba membuat spreadsheet mereka terlihat lebih dari sekadar tumpukan data mentah.  

Berita baiknya? Dalam beberapa menit saja Anda dapat **apply alternating row colors**, mengatur **solid background**, dan bahkan **import datatable to excel** menggunakan pola bersih dan dapat digunakan kembali di C#.  

Dalam tutorial ini kami akan membahas seluruh proses, mulai dari mengambil data ke dalam `DataTable` hingga menata setiap baris dengan pola strip kuning‑putih ringan. Tidak diperlukan pustaka eksternal selain paket penanganan Excel yang solid (seperti **ClosedXML** atau **GemBox.Spreadsheet**), dan Anda akan melihat mengapa pendekatan ini cepat dan mudah dipelihara.

## Apa yang Akan Anda Pelajari

- Bagaimana cara mengambil data dan memasukkannya ke dalam lembar kerja Excel.
- Bagaimana cara **style excel rows** dengan warna latar belakang bergantian.
- Mekanisme di balik **set solid background** menggunakan objek `Style`.
- Bagaimana cara **import datatable to excel** sambil mempertahankan gaya baris.
- Tips untuk menangani kasus tepi seperti tabel kosong atau skema warna khusus.

> **Pro tip:** Jika Anda sudah menggunakan objek workbook (`wb`) dari pustaka yang mendukung pembuatan gaya, Anda dapat menggunakan kembali instance `Style` yang sama di beberapa lembar kerja—menghemat memori dan menjaga kode Anda tetap rapi.

---

## Langkah 1: Mengambil Data – Menyiapkan DataTable

Sebelum penataan apa pun dapat dilakukan, kita memerlukan sumber baris. Dalam kebanyakan skenario dunia nyata, ini berasal dari basis data, API, atau file CSV. Untuk ilustrasi, kami hanya akan membuat `DataTable` sederhana di memori.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Mengapa ini penting:** Menggunakan `DataTable` memberi Anda wadah tabular yang sadar skema yang dapat diimpor langsung oleh pustaka Excel, menghilangkan kebutuhan menulis loop sel‑per‑sel.

---

## Langkah 2: Membuat Gaya Baris – **Apply alternating row colors**

Sekarang kami akan membuat array objek `Style`—satu per baris—sehingga setiap baris dapat menerima latar belakangnya masing‑masing. Pola yang akan kami gunakan adalah kuning‑terang klasik untuk baris genap dan putih untuk baris ganjil.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Penjelasan:**  
- `wb.CreateStyle()` memberi Anda objek gaya bersih yang dapat Anda ubah tanpa memengaruhi yang lain.  
- Operator ternary `(i % 2 == 0)` menentukan apakah baris tersebut genap (kuning terang) atau ganjil (putih).  
- Menetapkan `Pattern = BackgroundType.Solid` adalah langkah penting yang **set solid background**; tanpa itu warna akan diabaikan.

---

## Langkah 3: Mengambil Worksheet Target

Sebagian besar pustaka menyediakan koleksi worksheet. Kami akan bekerja dengan yang pertama, tetapi Anda dapat menargetkan indeks atau nama mana pun yang Anda inginkan.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

Jika workbook baru, biasanya pustaka membuat lembar default untuk Anda. Jika tidak, Anda dapat menambahkannya secara eksplisit:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## Langkah 4: Mengimpor DataTable dengan Gaya Baris – **Import datatable to excel**

Dengan gaya yang siap, langkah terakhir adalah memasukkan `DataTable` ke dalam lembar sambil menerapkan gaya yang sesuai pada setiap baris.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**Apa yang terjadi di balik layar?**  
- `true` memberi tahu metode untuk menulis header kolom sebagai baris pertama.  
- `0, 0` menandai sudut kiri‑atas (A1) sebagai titik sisipan.  
- `rowStyles` menyelaraskan setiap `Style` dengan baris data yang cocok, memberikan kita warna bergantian yang telah kami siapkan sebelumnya.

---

## Langkah 5: Menyimpan Workbook

Bagian terakhir dari puzzle adalah menyimpan workbook ke file sehingga Anda dapat membukanya di Excel dan melihat hasilnya.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Buka file dan Anda akan melihat lembar yang terformat rapi:

- Baris header dalam cetak tebal (gaya default pustaka).  
- Baris 1, 3, 5… dengan latar belakang putih bersih.  
- Baris 2, 4, 6… dengan isi kuning‑terang halus, memudahkan pemindaian.

### Snapshot Output yang Diharapkan

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

Baris 2, 4, 6, … muncul dengan latar belakang kuning‑terang—tepat efek **apply alternating row colors** yang kami tuju.

![Add background color excel example](https://example.com/excel-background.png "Add background color excel example")

*(Alt text includes the primary keyword for SEO.)*

---

## Menangani Kasus Tepi & Variasi

### DataTable Kosong

Jika `dataTable.Rows.Count` bernilai nol, array `rowStyles` akan kosong dan `ImportDataTable` tetap akan menulis baris header (jika `includeHeaders` bernilai `true`). Tidak ada pengecualian yang dilempar, tetapi Anda mungkin ingin melindungi dari menghasilkan file yang hampir kosong:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### Skema Warna Kustom

Ingin stripe biru/abu‑abu alih-alih kuning/putih? Cukup ganti nilai `Color`:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

Silakan ambil warna dari file konfigurasi sehingga non‑developer dapat menyesuaikan palet tanpa menyentuh kode.

### Menggunakan Kembali Gaya di Beberapa Worksheet

Jika Anda mengekspor beberapa tabel ke dalam workbook yang sama, Anda dapat menghasilkan array gaya sekali dan menggunakannya kembali:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Pastikan kedua tabel memiliki jumlah baris yang sama, atau buat array baru per lembar.

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program mandiri yang dapat Anda salin‑tempel ke aplikasi konsol.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Jalankan program, buka `Report.xlsx`, dan Anda akan melihat latar belakang bergantian persis seperti yang dijelaskan.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}