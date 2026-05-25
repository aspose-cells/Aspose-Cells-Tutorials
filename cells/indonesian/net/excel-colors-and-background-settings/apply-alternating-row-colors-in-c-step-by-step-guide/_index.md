---
category: general
date: 2026-03-18
description: Pelajari cara menerapkan warna baris bergantian di lembar kerja menggunakan
  C#. Termasuk mengatur warna latar belakang baris, menambahkan latar belakang kuning
  muda, dan mewarnai baris secara bergantian.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: id
og_description: Terapkan warna baris bergantian di C# untuk meningkatkan keterbacaan.
  Panduan ini menunjukkan cara mengatur warna latar belakang baris, menambahkan latar
  belakang kuning muda, dan mewarnai baris secara bergantian.
og_title: Terapkan Warna Baris Bergantian di C# – Tutorial Lengkap
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: Terapkan Warna Baris Bergantian di C# – Panduan Langkah demi Langkah
url: /id/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Terapkan Warna Baris Bergantian di C# – Tutorial Lengkap

Pernahkah Anda perlu **apply alternating row colors** ke lembar kerja berbasis data tetapi tidak yakin harus mulai dari mana? Anda bukan satu‑satunya — banyak pengembang mengalami kendala ini saat pertama kali mencoba membuat tabel terlihat lebih ramah. Kabar baik? Dalam beberapa baris C# saja Anda dapat **set row background color**, menambahkan **add light yellow background**, dan menghasilkan grid yang dipoles yang langsung meningkatkan keterbacaan.

Dalam tutorial ini kami akan membahas seluruh proses, mulai dari mengambil `DataTable` ke memori hingga menata setiap baris dengan strip kuning‑putih yang halus. Pada akhir tutorial Anda akan dapat **color rows alternately** dengan percaya diri, dan Anda juga akan melihat beberapa variasi berguna untuk ketika Anda membutuhkan nuansa berbeda atau tema dinamis.

## Apa yang Anda Butuhkan

- Proyek .NET yang menargetkan .NET 6 atau lebih baru (kode ini juga berfungsi pada .NET Framework 4.7+).  
- Pustaka spreadsheet yang mendukung objek style – contoh ini menggunakan API `Workbook`/`Worksheet` generik yang mirip dengan pustaka seperti **Aspose.Cells**, **GemBox.Spreadsheet**, atau **ClosedXML**.  
- Sumber `DataTable` – dapat berasal dari kueri basis data, impor CSV, atau koleksi dalam memori apa pun.  

Tidak ada paket NuGet tambahan selain pustaka spreadsheet itu sendiri. Jika Anda menggunakan Aspose.Cells, namespace-nya adalah `Aspose.Cells`; untuk ClosedXML adalah `ClosedXML.Excel`. Ganti pemanggilan `CreateStyle` dan `ImportDataTable` sesuai kebutuhan.

## Langkah 1: Ambil Data Sumber sebagai DataTable

Hal pertama—ambil data yang ingin Anda tampilkan. Dalam aplikasi dunia nyata ini biasanya berarti mengakses basis data, tetapi untuk kejelasan kami akan membuat metode pembantu bernama `GetData()` yang mengembalikan `DataTable` terisi.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Why this matters:** `DataTable` mendefinisikan baris dan kolom yang kemudian menerima shading bergantian. Jika tabel kosong, tidak ada yang dapat ditata, jadi selalu pastikan bahwa `Rows.Count` > 0 sebelum melanjutkan.

### Tips Pro
Jika Anda mengambil data dari Entity Framework, Anda dapat menggunakan `DataTable.Load(reader)` setelah mengeksekusi `SqlCommand`. Itu membuat kode tetap rapi dan menghindari definisi kolom manual.

## Langkah 2: Alokasikan Array untuk Menampung Style untuk Setiap Baris

Selanjutnya, kita membutuhkan kontainer yang sesuai dengan jumlah baris. Sebagian besar API spreadsheet memungkinkan Anda mengirimkan array style ke metode impor, jadi kami akan membuat `Style[]` dengan ukuran tepat sesuai jumlah baris.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Explanation:** Dengan mengalokasikan array sebelumnya, kami menghindari pembuatan objek style baru pada setiap iterasi, yang dapat meningkatkan kinerja saat menangani ribuan baris.

## Langkah 3: Terapkan Warna Baris Bergantian (Light Yellow / White)

Sekarang masuk ke inti masalah: **apply alternating row colors**. Kami akan melakukan loop pada setiap baris, membuat instance style baru dari workbook, dan mengatur latar belakangnya berdasarkan indeks baris. Baris genap mendapatkan isi light yellow, baris ganjil tetap putih.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### Mengapa ini Berfungsi
- **`rowIndex % 2 == 0`** memeriksa apakah baris tersebut genap.  
- **`Color.LightYellow`** memberikan nuansa lembut dan tidak mengganggu yang sempurna untuk tabel data.  
- **`BackgroundType.Solid`** memastikan isian menutupi seluruh sel, menghasilkan efek **set row background color**.  

Anda dapat mengganti `Color.LightYellow` dengan nuansa lain (mis., `Color.LightCyan`) jika menginginkan tampilan berbeda. Logika yang sama juga memungkinkan Anda **color rows alternately** berdasarkan kriteria lain, seperti flag status.

## Langkah 4: Impor DataTable ke Worksheet dengan Styles yang Disiapkan

Akhirnya, kami memasukkan semuanya ke dalam worksheet. Sebagian besar pustaka menyediakan overload `ImportDataTable` yang menerima array style. Flag `true` memberi tahu API untuk menulis header kolom, dan koordinat `0, 0` memulai dari sel kiri‑atas.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Result:** Worksheet kini menampilkan data Anda dengan pola **alternating row shading** yang bersih—light yellow pada baris genap, putih pada baris ganjil. Pengguna dapat memindai grid tanpa mata melompat bolak‑balik.

### Output yang Diharapkan
Jika Anda membuka spreadsheet yang dihasilkan, Anda akan melihat sesuatu seperti ini:

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

Baris 1, 3, 5… memiliki **light yellow background**, sementara baris 2, 4, 6… tetap **white**. Baris header (baris 0) mewarisi style default kecuali Anda menyesuaikannya secara terpisah.

## Variasi Opsional & Kasus Tepi

### 1. Menggunakan Palet Warna yang Berbeda
Jika light yellow bertentangan dengan merek Anda, cukup ganti `Color.LightYellow` dengan `System.Drawing.Color` lain. Untuk tema biru‑abu-abu Anda dapat menggunakan:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. Shading Dinamis Berdasarkan Data
Kadang Anda ingin menyorot baris yang memenuhi kondisi tertentu (mis., persediaan rendah). Gabungkan pemeriksaan modulo dengan tes khusus:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. Menerapkan Style Hanya pada Kolom Tertentu
Jika Anda hanya membutuhkan **set row background color** pada kolom tertentu, buat style terpisah untuk setiap kolom dan tetapkan setelah impor menggunakan API rentang sel worksheet.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. Tips Kinerja untuk Tabel Besar
Saat menangani > 10.000 baris, pertimbangkan untuk menggunakan kembali satu objek style untuk setiap warna alih-alih membuat yang baru per baris. Array kemudian menyimpan referensi ke dua style bersama, secara signifikan mengurangi penggunaan memori.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## Contoh Kerja Lengkap

Berikut adalah program mandiri yang dapat Anda tempelkan ke aplikasi console. Program ini menggunakan API `Workbook`/`Worksheet` fiktif; ganti tipe dengan yang dari pustaka pilihan Anda.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Output:** Sebuah file bernama `AlternatingRows.xlsx` di mana setiap baris bergantian antara isian light yellow dan putih, membuat tabel lebih nyaman dilihat.

## Pertanyaan yang Sering Diajukan

**Q: Apakah pendekatan ini bekerja dengan pemformatan bersyarat gaya Excel?**  
A: Ya. Jika pustaka Anda mendukung aturan bersyarat, Anda dapat menerjemahkan logika yang sama ke dalam aturan yang memeriksa `MOD(ROW(),2)=0`. Metode berbasis kode yang ditunjukkan di sini lebih portabel di antara pustaka yang tidak memiliki pemformatan bersyarat bawaan.

**Q: Bagaimana jika saya perlu **color rows alternately** dalam tabel PDF alih-alih lembar Excel?**  
A: Sebagian besar generator tabel PDF (mis., iTextSharp, PdfSharp) memungkinkan Anda mengatur `BackgroundColor` per baris. Perhitungan modulo yang sama berlaku—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}