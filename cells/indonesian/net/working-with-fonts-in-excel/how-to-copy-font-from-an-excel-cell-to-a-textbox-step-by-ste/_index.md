---
category: general
date: 2026-02-15
description: cara menyalin font dan menerapkan gaya sel di C# dengan contoh sederhana.
  pelajari cara mendapatkan gaya sel dan menggunakan pemformatan sel untuk mengatur
  ukuran font textbox.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: id
og_description: cara menyalin font dari sel lembar kerja dan menerapkan gaya sel ke
  TextBox. Panduan ini menunjukkan cara mendapatkan gaya sel, menggunakan pemformatan
  sel, dan mengatur ukuran font textbox.
og_title: cara menyalin font dari sel Excel – Tutorial C# lengkap
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: Cara menyalin font dari sel Excel ke TextBox – Panduan Langkah demi Langkah
url: /id/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara menyalin font dari sel Excel ke TextBox – Tutorial C# Lengkap

Pernah perlu **copy font** dari sel spreadsheet dan membuat kotak teks UI terlihat persis sama? Anda tidak sendirian. Dalam banyak alat pelaporan atau dasbor khusus, Anda akan menemukan diri Anda menarik data dari Excel dan kemudian berusaha menjaga kesetiaan visual—font family, size, dan colour—tetap utuh.  

Kabar baiknya, dengan hanya beberapa baris C# Anda dapat **get cell style**, membaca properti fontnya, dan **apply cell style** ke kontrol text‑box apa pun. Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang menunjukkan cara **use cell formatting** dan bahkan **set textbox font size** secara programatis.

---

## Apa yang Akan Anda Pelajari

- Cara mengambil objek `TextBox` dari komponen grid (`gridJs` dalam contoh kami)
- Cara membaca font family, size, dan colour dari sel Excel tertentu (`B2`)
- Cara menyalin atribut font tersebut ke text box sehingga UI mencerminkan spreadsheet
- Kesulitan umum (mis., colour conversion) dan beberapa **pro tips** untuk menjaga kode Anda tetap kuat
- Potongan kode siap‑jalan yang dapat Anda sisipkan ke aplikasi console atau proyek WinForms

**Prerequisites**  
Anda harus memiliki:

1. .NET 6+ (atau .NET Framework 4.8) terinstal  
2. Paket NuGet EPPlus (untuk penanganan Excel)  
3. Kontrol grid yang mengekspos kamus `TextBoxes` (contoh menggunakan `gridJs` fiktif tetapi idenya bekerja dengan perpustakaan UI apa pun)

Sekarang, mari kita mulai.

---

## Langkah 1: Siapkan Proyek dan Muat Worksheet

Pertama, buat proyek console atau WinForms baru dan tambahkan EPPlus:

```bash
dotnet add package EPPlus --version 6.*
```

Kemudian, muat workbook dan ambil sel yang gaya (style)nya ingin Anda salin.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**Mengapa ini penting:** EPPlus memberi Anda akses langsung ke objek `Style`, yang berisi sub‑objek `Font`. Dari sana Anda dapat membaca `Name`, `Size`, dan `Color`. Ini adalah inti dari operasi **get cell style**.

---

## Langkah 2: Ambil TextBox Target dari Grid Anda

Dengan asumsi grid UI Anda (`gridJs`) menyimpan text box dalam kamus yang diindeks oleh nama kolom, Anda dapat mengambil yang diinginkan seperti berikut:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

Jika Anda menggunakan WinForms, `notesTextBox` bisa berupa kontrol `TextBox`; untuk WPF mungkin elemen `TextBox`, dan untuk grid berbasis web bisa menjadi objek interop JavaScript. Intinya, Anda memiliki referensi yang dapat dimanipulasi.

---

## Langkah 3: Transfer Font Family

Sekarang kita memiliki gaya sumber dan kontrol tujuan, salin font family.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Pro tip:** Tidak semua kerangka UI mengekspos properti `FontFamily` yang menerima string biasa. Di WinForms Anda akan mengatur `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`. Sesuaikan sesuai kebutuhan.

---

## Langkah 4: Transfer Font Size

Ukuran font disimpan sebagai `float` di EPPlus. Terapkan langsung:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

Jika kontrol Anda menggunakan poin (sebagian besar memang), Anda dapat menetapkan nilai tanpa konversi. Untuk grid berbasis CSS Anda mungkin perlu menambahkan `"pt"`.

---

## Langkah 5: Transfer Font Colour

Konversi warna adalah bagian tersulit karena EPPlus menyimpan warna sebagai integer ARGB, sementara banyak kerangka UI mengharapkan `System.Drawing.Color` atau string hex CSS.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Mengapa ini berhasil:** `GetColor()` menyelesaikan warna berbasis tema dan mengembalikan `System.Drawing.Color` yang konkret. Jika sel menggunakan warna default (tanpa pengaturan eksplisit), kami mengatur default ke hitam untuk menghindari pengecualian referensi null.

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut aplikasi console minimal yang membaca file Excel, mengekstrak font dari **B2**, dan menerapkannya ke text box tiruan.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Output yang diharapkan (asumsi B2 menggunakan Arial, 12 pt, biru):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

Jalankan program, buka UI Anda, dan Anda akan melihat text box “Notes” kini mencerminkan gaya font sel **B2** secara tepat. Tidak diperlukan penyesuaian manual.

---

## Pertanyaan yang Sering Diajukan & Kasus Tepi

### Bagaimana jika sel menggunakan warna tema alih-alih nilai RGB eksplisit?

`GetColor()` EPPlus secara otomatis menyelesaikan warna tema menjadi `System.Drawing.Color` yang konkret. Namun, jika Anda menggunakan perpustakaan lama yang hanya mengembalikan indeks tema, Anda harus memetakan indeks tersebut ke palet warna secara manual.

### Bisakah saya menyalin atribut gaya lain (mis., bold, italic)?

Absolutely. The `ExcelStyle.Font` object also exposes `Bold`, `Italic`, `Underline`, and `Strike`. Just set the corresponding properties on your UI control:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### Bagaimana jika kontrol grid tidak mengekspos properti `FontColor`?

Most modern UI frameworks do, but if yours only accepts a CSS string, convert the `Color` to hex:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### Bagaimana cara menangani banyak sel sekaligus?

Lakukan loop pada rentang yang diinginkan, ambil gaya setiap sel, dan terapkan ke text box yang bersesuaian. Ingat untuk menyimpan objek gaya dalam cache jika Anda memproses banyak baris untuk menghindari penurunan kinerja.

---

## Pro Tips & Kesalahan Umum

- **Cache the ExcelPackage** – membuka dan menutup file untuk setiap sel mahal. Muat workbook sekali, lalu gunakan kembali objek `ExcelWorksheet`.
- **Watch out for null colours** – sel yang mewarisi warna default mengembalikan `null`. Selalu sediakan fallback (hitam atau default kontrol).
- **Mind DPI scaling** – jika Anda menargetkan monitor high‑DPI, ukuran font mungkin tampak sedikit lebih besar. Sesuaikan menggunakan `Graphics.DpiX` bila perlu.
- **Thread safety** – EPPlus tidak thread‑safe. Jika Anda memproses banyak sheet secara paralel, buat `ExcelPackage` terpisah per thread.

---

## Kesimpulan

Anda kini tahu **how to copy font** dari sel Excel dan **apply cell style** ke kontrol text‑box apa pun menggunakan C#. Dengan mengambil `Style` sel, mengekstrak properti `Font`-nya, dan menetapkannya ke elemen UI, Anda mempertahankan konsistensi visual tanpa penyalinan manual.

Solusi lengkap—memuat workbook, mendapatkan gaya sel, dan mengatur family font, ukuran, serta warna textbox—mencakup inti dari **use cell formatting** dan menunjukkan cara **set textbox font size** dengan benar.

Selanjutnya, coba perpanjang contoh untuk menyalin warna latar belakang, border, atau bahkan seluruh isi sel. Jika Anda bekerja dengan perpustakaan data‑grid yang mendukung rendering sel kaya, Anda kini dapat memberikannya informasi styling yang sama persis yang Anda ambil dari Excel, menjaga UI dan laporan Anda tetap sinkron.

Ada pertanyaan lain? Tinggalkan komentar atau jelajahi topik terkait seperti “dynamic Excel‑to‑UI binding” dan “theme‑aware colour conversion”. Selamat coding!

---

![contoh cara menyalin font](placeholder-image.jpg "cara menyalin font dari sel Excel ke TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}