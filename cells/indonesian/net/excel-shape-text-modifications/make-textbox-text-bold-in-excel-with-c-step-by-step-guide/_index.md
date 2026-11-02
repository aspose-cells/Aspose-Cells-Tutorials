---
category: general
date: 2026-02-21
description: Pelajari cara membuat teks TextBox menjadi tebal, mengubah ukuran font
  TextBox, dan memuat workbook Excel C# menggunakan Aspose.Cells dalam contoh lengkap
  yang dapat dijalankan.
draft: false
keywords:
- make textbox text bold
- change textbox font size
- load excel workbook c#
- format excel shape text
language: id
og_description: Buat teks TextBox menjadi tebal dalam file Excel menggunakan C#. Tutorial
  ini juga menunjukkan cara mengubah ukuran font textbox dan memuat workbook Excel
  dengan C# menggunakan Aspose.Cells.
og_title: Buat Teks TextBox Menjadi Tebal di Excel dengan C# – Panduan Lengkap
tags:
- C#
- Aspose.Cells
- Excel automation
title: Membuat Teks TextBox Tebal di Excel dengan C# – Panduan Langkah demi Langkah
url: /id/net/excel-shape-text-modifications/make-textbox-text-bold-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Teks TextBox Tebal di Excel dengan C# – Panduan Langkah‑per‑Langkah

Perlu **menjadikan teks TextBox tebal** dalam file Excel menggunakan C#? Pada tutorial ini kami akan menunjukkan secara tepat cara *memuat workbook Excel*, **mengubah ukuran font TextBox**, dan memformat teks shape dengan Aspose.Cells.  
Jika Anda pernah menatap spreadsheet yang membosankan dan berpikir “textbox saya harus menonjol,” Anda berada di tempat yang tepat.

Kami akan menelusuri setiap baris kode, menjelaskan mengapa setiap pemanggilan penting, dan bahkan membahas apa yang harus dilakukan ketika lembar kerja tidak memiliki textbox sama sekali. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat disisipkan ke proyek .NET mana pun—tanpa perlu tautan “lihat dokumentasi” yang misterius.

## Apa yang Anda Butuhkan

- **Aspose.Cells for .NET** (versi percobaan gratis atau berlisensi) – API yang kami gunakan untuk mengakses shape Excel.  
- .NET 6 atau lebih baru (kode ini juga berfungsi dengan .NET Framework 4.7+).  
- File Excel sederhana (`input.xlsx`) yang sudah berisi setidaknya satu textbox pada lembar pertama.  

Itu saja. Tanpa paket NuGet tambahan, tanpa interop COM, hanya C# murni.

## Membuat Teks TextBox Tebal – Memuat Workbook dan Mengakses Shape

Langkah pertama adalah membuka workbook dan mengambil textbox yang ingin diedit.  
Kami juga melakukan pemeriksaan keamanan cepat agar kode tidak crash jika lembar kosong.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook (load excel workbook c#)
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];

        // Verify that at least one TextBox exists
        if (worksheet.TextBoxes.Count == 0)
        {
            Console.WriteLine("No TextBoxes found on the first sheet.");
            return;
        }

        // Step 3: Access the first TextBox shape
        Shape textBox = worksheet.TextBoxes[0];

        // From here on we can format the shape's text
```

**Mengapa ini penting:**  
*Memuat workbook* memberi kita objek `Workbook` yang mewakili seluruh file dalam memori. Mengakses `Worksheets[0]` aman karena setiap file Excel memiliki setidaknya satu lembar. Klausa penjaga (`if (worksheet.TextBoxes.Count == 0)`) mencegah `IndexOutOfRangeException`—sebuah jebakan umum saat mengotomatisasi file yang sudah ada.

## Mengubah Ukuran Font TextBox

Sebelum kita menebalkan teks, pastikan ukuran font sudah tepat sesuai kebutuhan Anda.  
Mengubah ukuran semudah menyesuaikan properti `Font.Size`.

```csharp
        // Step 4: Set the font name (optional but often useful)
        textBox.Font.Name = "Calibri";

        // Step 5: Change the font size (change textbox font size)
        textBox.Font.Size = 12; // 12 points is a comfortable default
```

**Tips profesional:**  
Jika Anda memerlukan ukuran dinamis berdasarkan input pengguna, cukup ganti `12` dengan sebuah variabel. Objek `Font` dibagikan di seluruh shape, sehingga perubahan ukuran langsung memengaruhi setiap karakter di dalam textbox.

## Membuat Teks TextBox Tebal – Aksi Inti

Sekarang untuk fitur utama: menebalkan teks.  
Flag `IsBold` mengubah ketebalan font tanpa mengubah gaya lainnya.

```csharp
        // Step 6: Make the text bold (make textbox text bold)
        textBox.Font.IsBold = true;
```

**Apa yang terjadi di balik layar?**  
Aspose.Cells menyimpan format teks dalam objek `Font` yang terlampir pada shape. Menetapkan `IsBold = true` memperbarui XML dasar (`<b>1</b>`) yang dibaca Excel saat merender lembar. Ini adalah operasi **non‑destruktif**—jika Anda kemudian mengatur `IsBold = false`, teks kembali ke berat normal.

## Menyimpan Workbook yang Dimodifikasi

Setelah pemformatan selesai, kami menulis perubahan kembali ke disk.  
Anda dapat menimpa file asli atau, seperti yang ditunjukkan di sini, membuat file baru agar sumber tetap tidak tersentuh.

```csharp
        // Step 7: Save the modified workbook
        var outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved. TextBox is now bold and 12pt Calibri in '{outputPath}'.");
    }
}
```

**Hasil yang diharapkan:**  
Buka `output.xlsx` di Excel. Textbox pertama pada lembar pertama harus menampilkan teksnya dalam **Calibri 12 pt, tebal**. Tidak ada shape lain yang terpengaruh.

## Memformat Teks Shape Excel – Opsi Styling Tambahan (Opsional)

Meskipun tujuan utama adalah **menjadikan teks TextBox tebal**, Anda mungkin juga ingin:

| Opsi | Potongan Kode | Kapan Digunakan |
|------|---------------|-----------------|
| Miring | `textBox.Font.IsItalic = true;` | Menekankan subjudul |
| Warna teks | `textBox.Font.Color = System.Drawing.Color.DarkBlue;` | Warna merek |
| Perataan | `textBox.AlignmentHorizontal = TextAlignmentType.Center;` | Judul terpusat |
| Banyak TextBox | Loop through `worksheet.TextBoxes` | Pemformatan massal |

```csharp
// Example: Apply a blue color and center alignment to all textboxes
foreach (Shape tb in worksheet.TextBoxes)
{
    tb.Font.Color = System.Drawing.Color.Blue;
    tb.AlignmentHorizontal = TextAlignmentType.Center;
}
```

Penyesuaian tambahan ini menggambarkan bagaimana *format excel shape text* dapat diperluas selain sekadar menebalkan.

## Kasus Tepi & Kesalahan Umum

1. **Tidak ada TextBox pada lembar** – Klausa penjaga yang kami tambahkan (`if (worksheet.TextBoxes.Count == 0)`) keluar dengan elegan dan memberi tahu pengguna.  
2. **Lembar kerja tersembunyi** – Lembar tersembunyi tetap dapat diakses melalui koleksi `Worksheets`; pastikan Anda merujuk indeks yang tepat.  
3. **File besar** – Memuat workbook yang sangat besar dapat mengonsumsi memori. Pertimbangkan menggunakan `Workbook.LoadOptions` untuk memuat hanya bagian yang diperlukan.  
4. **Versi Excel yang berbeda** – Aspose.Cells bekerja dengan `.xls`, `.xlsx`, dan bahkan `.xlsb`. Kode yang sama berfungsi di semua versi, tetapi Excel lama mungkin mengabaikan beberapa fitur font yang lebih baru.

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

```csharp
using System;
using Aspose.Cells;

class MakeTextboxBoldDemo
{
    static void Main()
    {
        // Load the workbook (load excel workbook c#)
        var inputFile = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputFile);

        // Get the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // Ensure a textbox exists
        if (sheet.TextBoxes.Count == 0)
        {
            Console.WriteLine("No textbox found on the first sheet.");
            return;
        }

        // Access the first textbox
        Shape txtBox = sheet.TextBoxes[0];

        // Set font name and size (change textbox font size)
        txtBox.Font.Name = "Calibri";
        txtBox.Font.Size = 12;

        // Make the text bold (make textbox text bold)
        txtBox.Font.IsBold = true;

        // Optional: extra styling (format excel shape text)
        txtBox.Font.Color = System.Drawing.Color.DarkGreen;
        txtBox.AlignmentHorizontal = TextAlignmentType.Center;

        // Save the result
        var outputFile = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputFile);

        Console.WriteLine($"Saved: {outputFile}");
    }
}
```

Jalankan program, buka `output.xlsx` yang dihasilkan, dan Anda akan melihat teks Calibri 12‑pt yang tebal di dalam textbox. Sederhana, kan?

## Kesimpulan

Anda kini tahu **cara menjadikan teks TextBox tebal** dalam workbook Excel menggunakan C#, cara **mengubah ukuran font TextBox**, dan dasar-dasar **memuat workbook Excel dengan C#** menggunakan Aspose.Cells. Contoh lengkap di atas siap disisipkan ke proyek mana pun, dan Anda juga telah melihat cara **memformat teks shape Excel** untuk styling yang lebih kaya.

Selanjutnya? Cobalah melakukan loop melalui setiap lembar kerja untuk menebalkan semua textbox, atau gabungkan ini dengan pembuatan konten berbasis data—mungkin mengisi textbox dengan nilai dari basis data. Prinsip yang sama berlaku, dan kode tetap bersih.

Ada trik yang ingin Anda bagikan, atau mengalami error yang tidak terduga? Tinggalkan komentar, dan mari teruskan diskusi. Selamat coding! 

![menjadikan teks textbox tebal di Excel menggunakan C#](/images/make-textbox-text-bold-csharp.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}