---
category: general
date: 2026-02-21
description: Buat gaya sel di C# dengan cepat. Pelajari cara menerapkan gaya pada
  sel, memusatkan teks dalam sel, mengatur perataan sel, dan menguasai pemformatan
  sel.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: id
og_description: Buat gaya sel di C# dan pelajari cara menerapkan gaya ke sel, memusatkan
  teks di sel, serta mengatur perataan sel dengan panduan langkah demi langkah yang
  jelas.
og_title: Buat gaya sel di C# – Terapkan gaya pada sel dan rata tengah teks
tags:
- C#
- Aspose.Cells
- Excel automation
title: Buat gaya sel di C# – Cara menerapkan gaya pada sel dan memusatkan teks
url: /id/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat gaya sel di C# – Panduan Lengkap untuk Menerapkan Gaya dan Memusatkan Teks

Pernah perlu **membuat gaya sel** di lembar kerja Excel tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian. Dalam banyak proyek otomasi, kemampuan untuk **menerapkan gaya ke sel** menjadi perbedaan antara spreadsheet yang membosankan dan laporan yang rapi.  

Dalam tutorial ini kami akan menelusuri contoh lengkap yang dapat dijalankan yang menunjukkan **cara memusatkan teks** di dalam sel, mengatur perataan, dan menambahkan batas tipis—semua dalam beberapa baris C#. Pada akhir tutorial Anda akan tahu persis mengapa setiap bagian penting dan bagaimana menyesuaikannya untuk skenario Anda sendiri.

## Apa yang Akan Anda Dapatkan

- Pemahaman yang jelas tentang alur kerja **membuat gaya sel** menggunakan Aspose.Cells (atau perpustakaan serupa lainnya).
- Kode tepat yang dapat Anda salin‑tempel ke aplikasi konsol untuk **menerapkan gaya ke sel**.
- Wawasan tentang **memusatkan teks di sel**, **mengatur perataan sel**, dan menangani kasus khusus seperti sel yang digabung atau format angka khusus.
- Tips untuk memperluas gaya—font berbeda, warna latar belakang, atau pemformatan bersyarat.

> **Prasyarat:** Visual Studio 2022 (atau IDE C# apa pun) dan paket NuGet Aspose.Cells untuk .NET. Tidak ada dependensi lain yang diperlukan.

---

## Langkah 1: Siapkan Proyek Anda dan Impor Namespace

Sebelum kita dapat **membuat gaya sel**, kita memerlukan proyek yang merujuk ke perpustakaan Excel.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Mengapa ini penting:* Mengimpor `Aspose.Cells` memberi kita akses ke kelas `Workbook`, `Worksheet`, `Style`, dan `Border`. Jika Anda menggunakan perpustakaan lain (misalnya EPPlus), nama kelasnya berubah tetapi konsepnya tetap sama.

---

## Langkah 2: Buat Workbook dan Ambil Sel Pertama

Sekarang kita **membuat gaya sel** dengan pertama‑tama mendapatkan referensi ke sel yang ingin diformat.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

Perhatikan kami menggunakan `Cell` alih‑alih `var`—pengetikan eksplisit membuat kode lebih jelas bagi pemula. Pemanggilan `PutValue` menulis string sehingga kita dapat melihat efek gaya nanti.

---

## Langkah 3: Definisikan Gaya – Memusatkan Teks, Menambahkan Batas Tipis

Berikut inti dari operasi **membuat gaya sel**. Kami akan mengatur perataan horizontal, batas tipis, dan beberapa tambahan opsional.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Mengapa kami melakukannya:*  
- **HorizontalAlignment** dan **VerticalAlignment** bersama‑sama menjawab pertanyaan “**bagaimana memusatkan teks** di sel?”  
- Menambahkan keempat batas memastikan sel terlihat seperti label berkotak, yang berguna untuk header.  
- Warna latar belakang tidak wajib, tetapi menunjukkan cara memperluas gaya di kemudian hari.

---

## Langkah 4: Terapkan Gaya yang Didefinisikan ke Sel yang Dipilih

Setelah gaya ada, kami **menerapkan gaya ke sel** dengan satu pemanggilan metode.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

Itu saja—Aspose.Cells menangani penyalinan gaya ke dalam koleksi gaya internal sel. Jika Anda memerlukan pemformatan yang sama pada rentang, Anda dapat menggunakan `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });`.

---

## Langkah 5: Simpan Workbook dan Verifikasi Hasilnya

Simpan cepat memungkinkan Anda membuka file di Excel dan memastikan teks benar‑benar terpusat serta batas muncul.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Output yang diharapkan:* Saat Anda membuka **StyledCell.xlsx**, sel **A1** berisi “Hello, styled world!” terpusat secara horizontal dan vertikal, dikelilingi oleh batas abu‑abu tipis, dan memiliki latar belakang abu‑abu muda.

---

## Variasi Umum & Kasus Tepi

### 1. Memusatkan Teks di Wilayah yang Digabung

Jika Anda menggabungkan sel **A1:C1** dan tetap ingin teks terpusat, Anda harus menerapkan gaya ke sel kiri‑atas **setelah** penggabungan:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Menggunakan Format Numerik

Kadang‑kadang Anda perlu **mengatur perataan sel** *dan* menampilkan angka dengan format tertentu:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

Perataan tetap terpusat sementara angka muncul sebagai `12,345.68`.

### 3. Menggunakan Kembali Gaya Secara Efisien

Membuat `Style` baru untuk setiap sel dapat menurunkan kinerja. Sebagai gantinya, buat satu objek gaya dan gunakan kembali pada banyak sel atau rentang. Kelas `StyleFlag` memungkinkan Anda menerapkan hanya bagian yang diperlukan, menghemat memori.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## Pro Tips & Hal yang Perlu Diwaspadai

- **Jangan lupa perataan vertikal** – memusatkan hanya secara horizontal sering terlihat aneh, terutama pada baris yang tinggi.
- **Tipe batas**: `CellBorderType.Thin` cocok untuk kebanyakan laporan, tetapi Anda dapat beralih ke `Medium` atau `Dashed` untuk hierarki visual.
- **Penanganan warna**: Saat menargetkan .NET Core, gunakan `System.Drawing.Color` dari paket `System.Drawing.Common`; jika tidak, Anda akan mendapatkan error runtime.
- **Format penyimpanan**: Jika Anda memerlukan kompatibilitas dengan versi Excel lama, ubah `SaveFormat.Xlsx` menjadi `SaveFormat.Xls`.

---

![Create cell style example](https://example.com/images/create-cell-style.png "Create cell style in C#")

*Alt text: screenshot yang menampilkan sel dengan teks terpusat dan batas tipis yang dibuat oleh tutorial membuat gaya sel.*

---

## Contoh Lengkap yang Siap Digunakan (Copy‑Paste)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

Jalankan program ini, buka **StyledCell.xlsx**, dan Anda akan melihat hasil persis seperti yang dijelaskan sebelumnya. Silakan ubah teks, gaya batas, atau warna latar belakang agar sesuai dengan merek Anda.

---

## Kesimpulan

Kami baru saja **membuat gaya sel** dari awal, **menerapkan gaya ke sel**, dan mendemonstrasikan **cara memusatkan teks** baik secara horizontal maupun vertikal. Dengan menguasai blok‑blok bangunan ini, Anda kini dapat memformat header, menyorot total, atau membangun seluruh templat laporan tanpa meninggalkan C#.  

Jika Anda penasaran dengan langkah selanjutnya, coba:

- **Menerapkan gaya yang sama ke seluruh baris** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).
- **Menambahkan pemformatan bersyarat** untuk mengubah latar belakang berdasarkan nilai sel.
- **Mengekspor ke PDF** sambil mempertahankan gaya.

Ingat, pemformatan tidak hanya tentang estetika tetapi juga keterbacaan. Bereksperimen, iterasi, dan segera spreadsheet Anda akan tampak seprofesional kode Anda.

*Selamat coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}