---
category: general
date: 2026-02-21
description: Simpan Excel sebagai txt dengan kontrol presisi atas digit signifikan.
  Ekspor Excel ke txt dalam C# dan atur digit signifikan dengan mudah.
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: id
og_description: Simpan Excel sebagai txt dengan cepat. Pelajari cara mengekspor Excel
  ke txt, mengatur digit signifikan, dan mengontrol output teks menggunakan C#.
og_title: Simpan Excel sebagai txt – Ekspor Angka dengan Digit Signifikan di C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Simpan Excel sebagai txt – Panduan Lengkap C# untuk Mengekspor Angka dengan
  Digit Signifikan
url: /id/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Simpan Excel sebagai txt – Panduan Lengkap C# untuk Mengekspor Angka dengan Digit Signifikan

Pernah perlu **save Excel as txt** tetapi khawatir angka-angka akan kehilangan presisinya? Anda tidak sendirian. Banyak pengembang menemui kendala ketika mencoba mengekspor Excel ke txt dan berakhir dengan terlalu banyak angka desimal atau hasil yang dibulatkan berantakan.  

Dalam tutorial ini kami akan menunjukkan cara **export Excel to txt** yang sederhana sambil **setting significant digits** sehingga output terlihat persis seperti yang Anda inginkan. Pada akhir tutorial Anda akan memiliki potongan kode C# siap‑jalankan yang menyimpan workbook sebagai teks, mengekspor angka ke txt, dan memberi Anda kontrol penuh atas format numerik.

## Apa yang Akan Anda Pelajari

- Cara membuat workbook baru dan menulis data numerik.
- Cara yang tepat untuk **set significant digits** menggunakan `TxtSaveOptions`.
- Cara **save workbook as text** dan memverifikasi hasilnya.
- Penanganan kasus tepi (angka besar, nilai negatif, masalah locale).
- Tips cepat untuk menyesuaikan output lebih lanjut (perubahan delimiter, encoding).

### Prasyarat

- .NET 6.0 atau lebih baru (kode ini juga bekerja pada .NET Framework 4.6+).
- Paket NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`).
- Pemahaman dasar tentang sintaks C#—tidak memerlukan pengetahuan mendalam tentang interop Excel.

> **Pro tip:** Jika Anda menggunakan Visual Studio, aktifkan *nullable reference types* (`<Nullable>enable</Nullable>`) untuk menangkap potensi bug null lebih awal.

---

## Langkah 1: Inisialisasi Workbook dan Tulis Angka

Pertama, kita memerlukan objek workbook. Anggap saja sebagai representasi dalam memori dari sebuah file Excel.  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**Mengapa ini penting:**  
Membuat workbook secara programatik menghindari beban COM interop, dan `PutValue` secara otomatis mendeteksi tipe data, memastikan sel diperlakukan sebagai angka—bukan string.

---

## Langkah 2: Konfigurasi TxtSaveOptions untuk Mengontrol Digit Signifikan

Kelas `TxtSaveOptions` adalah tempat keajaiban terjadi. Dengan mengatur `SignificantDigits`, Anda memberi tahu Aspose.Cells berapa banyak digit bermakna yang harus dipertahankan saat file ditulis.

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**Mengapa Anda harus mengatur ini:**  
Saat Anda **export numbers to txt**, sering kali diperlukan representasi yang ringkas (misalnya, untuk sistem pelaporan yang hanya menerima presisi tertentu). Properti `SignificantDigits` menjamin pembulatan yang konsisten terlepas dari panjang angka asli.

---

## Langkah 3: Simpan Workbook sebagai File Teks

Sekarang kita menulis workbook ke disk menggunakan opsi yang baru saja kita definisikan.

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**Apa yang akan Anda lihat:**  
Buka `Numbers.txt` dan Anda akan mendapatkan satu baris tunggal:

```
12350
```

Angka asli `12345.6789` telah dibulatkan menjadi **empat digit signifikan**, persis seperti yang diminta.

---

## Langkah 4: Verifikasi Output (Opsional tetapi Disarankan)

Tes otomatis adalah kebiasaan yang baik. Berikut pemeriksaan cepat yang dapat Anda jalankan segera setelah menyimpan:

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

Menjalankan blok ini akan mencetak tanda centang hijau jika semuanya cocok, memberi Anda keyakinan bahwa operasi **save excel as txt** berperilaku seperti yang diharapkan.

---

## Variasi Umum & Kasus Tepi

### Mengekspor Beberapa Sel atau Rentang

Jika Anda perlu **export excel to txt** untuk seluruh rentang, cukup isi lebih banyak sel sebelum menyimpan:

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

`TxtSaveOptions` yang sama akan menerapkan aturan 4‑digit pada setiap nilai, menghasilkan:

```
12350
0.0001235
-98800
```

### Mengubah Delimiter

Beberapa sistem downstream mengharapkan nilai dipisahkan tab. Sesuaikan delimiter seperti berikut:

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

Sekarang setiap sel dalam satu baris dipisahkan oleh tab.

### Menangani Pemisah Desimal Spesifik Locale

Jika audiens Anda menggunakan koma untuk desimal, atur budaya:

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

Output akan menghormati locale, mengubah `12350` menjadi `12 350` (spasi sebagai pemisah ribuan dalam bahasa Prancis).

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**Konten `Numbers.txt` yang diharapkan (delimiter default, 4 digit signifikan):**

```
12350	0.0001235	-98800
```

Tab (`\t`) muncul karena kami membiarkan delimiter pada nilai default (tab) dalam contoh; ubah menjadi koma jika Anda lebih suka format CSV.

---

## Kesimpulan

Anda kini tahu persis **how to save Excel as txt** sambil mengontrol jumlah digit signifikan. Langkah‑langkah—membuat workbook, mengatur `TxtSaveOptions.SignificantDigits`, dan menyimpan—adalah semua yang Anda perlukan untuk **export excel to txt** secara andal.  

Dari sini Anda dapat:

- **Export numbers to txt** untuk set data yang lebih besar.
- Sesuaikan delimiter, encoding, atau pengaturan budaya untuk mencocokkan sistem downstream mana pun.
- Gabungkan pendekatan ini dengan fitur Aspose.Cells lainnya (styles, formulas) sebelum ekspor.

Cobalah, ubah `SignificantDigits` menjadi 2 atau 6, dan lihat bagaimana output berubah. Fleksibilitas **save workbook as text** menjadikannya alat yang berguna dalam setiap pipeline pertukaran data.

---

### Topik Terkait yang Mungkin Anda Jelajahi Selanjutnya

- **Export Excel to CSV** dengan urutan kolom khusus.
- **Read txt files back into a workbook** (`Workbook.Load` dengan `LoadOptions`).
- **Batch processing** beberapa worksheet dan mengkonsolidasikannya menjadi satu file txt.
- **Performance tuning** untuk ekspor skala besar (streaming vs. in‑memory).

Silakan tinggalkan komentar jika Anda mengalami kendala, atau bagikan bagaimana Anda menyesuaikan ekspor untuk proyek Anda sendiri. Selamat coding!  

---  

*Image: Sebuah tangkapan layar file `Numbers.txt` yang dihasilkan menampilkan nilai yang dibulatkan.*  
*Alt text: “File Numbers.txt menampilkan 12350, 0.0001235, dan -98800 setelah menyimpan Excel sebagai txt dengan 4 digit signifikan.”*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}