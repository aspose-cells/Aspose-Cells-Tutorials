---
category: general
date: 2026-02-15
description: Buat buku kerja baru dan ekspor Excel ke TXT sambil mengatur presisi
  numerik. Pelajari cara mengatur digit signifikan dan membatasi digit signifikan
  dalam C#.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: id
og_description: Buat workbook baru dan ekspor Excel ke TXT, mengatur digit signifikan
  untuk presisi numerik. Panduan C# langkah demi langkah.
og_title: Buat Buku Kerja Baru – Ekspor Excel ke TXT dengan Presisi
tags:
- C#
- Aspose.Cells
- Excel automation
title: Buat Buku Kerja Baru dan Ekspor Excel ke TXT dengan Presisi
url: /id/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

with translations. Ensure no extra spaces or missing elements.

Let's assemble.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Workbook Baru – Ekspor Excel ke TXT dengan Format Numerik yang Tepat

Pernah bertanya-tanya bagaimana cara **create new workbook** objek di C# dan langsung menuliskannya ke file teks biasa? Anda tidak sendirian. Dalam banyak skenario data‑pipeline kita perlu **export Excel to TXT** sambil menjaga angka tetap dapat dibaca, yang berarti membatasi jumlah digit yang muncul setelah titik desimal.  

Dalam tutorial ini kami akan membahas seluruh proses: mulai dari membuat workbook baru, mengkonfigurasi ekspor sehingga **sets significant digits** (alias membatasi digit signifikan), dan akhirnya menulis file ke disk. Pada akhir tutorial Anda akan memiliki potongan kode siap‑jalankan yang menghormati persyaratan **numeric precision** Anda—tanpa pustaka tambahan, tanpa sulap.

> **Pro tip:** Jika Anda sudah menggunakan Aspose.Cells, kelas-kelas yang ditampilkan di bawah merupakan bagian dari perpustakaan tersebut. Jika Anda berada di platform lain, konsepnya tetap berlaku; cukup ganti panggilan API.

---

## Apa yang Anda Butuhkan

- .NET 6+ (kode ini dapat dikompilasi pada .NET Core dan .NET Framework)  
- Aspose.Cells untuk .NET (versi percobaan gratis atau berlisensi) – instal via NuGet: `dotnet add package Aspose.Cells`  
- IDE apa pun yang Anda suka (Visual Studio, Rider, VS Code)  

Itu saja. Tidak ada file konfigurasi tambahan, tidak ada langkah tersembunyi.

---

## Langkah 1: Buat Workbook Baru

Hal pertama yang harus dilakukan adalah **create new workbook**. Anggap kelas `Workbook` sebagai file Excel kosong yang menunggu lembar, sel, dan data.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Why this matters:** Dengan memulai dari workbook yang bersih Anda menghindari format tersembunyi yang dapat mengganggu pengaturan presisi nanti.

---

## Langkah 2: Konfigurasikan Opsi Penyimpanan Teks – Atur Digit Signifikan

Sekarang kami memberi tahu Aspose.Cells berapa banyak **significant digits** yang kami inginkan saat menulis ke file `.txt`. Kelas `TxtSaveOptions` menyediakan properti `SignificantDigits` yang melakukan hal tersebut.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Explanation:** `SignificantDigits = 5` berarti exporter akan mempertahankan lima digit terpenting dari setiap angka, terlepas dari posisi titik desimal. Ini cara yang praktis untuk **set numeric precision** tanpa harus memformat setiap sel secara manual.

---

## Langkah 3: Simpan Workbook sebagai File Teks Biasa

Dengan workbook dan opsi yang siap, kami akhirnya **export Excel to txt**. Metode `Save` menerima jalur file dan objek opsi yang baru saja kami konfigurasikan.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

Menjalankan program menghasilkan file yang terlihat seperti ini:

```
12346
0.00012346
3.1416
```

Perhatikan bagaimana setiap angka mematuhi aturan **limit significant digits** yang kami tetapkan sebelumnya.

---

## Langkah 4: Verifikasi Hasil (Opsional tetapi Disarankan)

Mudah untuk membuka `numbers.txt` yang dihasilkan di editor apa pun, tetapi Anda mungkin ingin mengotomatisasi langkah verifikasi, terutama dalam pipeline CI.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

Jika konsol menampilkan tiga baris di atas, Anda telah berhasil **set significant digits** dan ekspor berfungsi seperti yang diharapkan.

---

## Kesalahan Umum & Cara Menghindarinya

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Angka muncul dengan terlalu banyak tempat desimal | `SignificantDigits` dibiarkan pada nilai default (0) | Setel secara eksplisit `SignificantDigits` ke jumlah yang diinginkan |
| File kosong dibuat | Workbook tidak pernah menerima data sebelum disimpan | Isi sel **sebelum** memanggil `Save` |
| Path file melempar `UnauthorizedAccessException` | Mencoba menulis ke folder yang dilindungi | Gunakan folder yang Anda memiliki izin menulis (mis., `C:\Temp` atau `%USERPROFILE%\Documents`) |
| Presisi tampak tidak tepat untuk angka yang sangat kecil | Hitungan digit signifikan termasuk nol di depan setelah desimal | Ingat bahwa “significant” mengabaikan nol di depan; 0.000123456 dengan 5 digit menjadi `0.00012346` |

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah program lengkap yang berdiri sendiri. Tempelkan ke dalam proyek konsol baru dan tekan **Run**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**Output konsol yang diharapkan**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

Dan file `numbers.txt` akan berisi tiga baris yang ditampilkan di atas.

---

## Langkah Selanjutnya: Melampaui Dasar

- **Export other formats** – Aspose.Cells juga mendukung CSV, HTML, dan PDF. Ganti `TxtSaveOptions` dengan `CsvSaveOptions` atau `PdfSaveOptions` sesuai kebutuhan.  
- **Dynamic precision** – Anda dapat menghitung `SignificantDigits` pada waktu berjalan berdasarkan input pengguna atau file konfigurasi.  
- **Multiple worksheets** – iterasi `workbook.Worksheets` dan ekspor masing‑masing ke file `.txt` masing‑masing.  
- **Localization** – kontrol pemisah desimal (`.` vs `,`) melalui `CultureInfo` jika Anda perlu menyesuaikan dengan pengaturan regional.  

Semua ekstensi ini tetap mengandalkan ide inti yang kami bahas: **create new workbook**, konfigurasikan ekspor, dan **set numeric precision** agar sesuai dengan kebutuhan pelaporan Anda.

---

## Ringkasan

Kami telah mengambil instance **create new workbook** yang baru, mengisinya dengan data, dan mendemonstrasikan cara **export Excel to TXT** sambil **setting significant digits** untuk membatasi presisi output. Contoh lengkap dapat dijalankan langsung, dan penjelasan mencakup *mengapa* di balik setiap baris sehingga Anda dapat menyesuaikannya dengan proyek Anda.

Silakan bereksperimen—ubah nilai `SignificantDigits`, tambahkan lebih banyak lembar, atau ganti format output. Jika Anda mengalami masalah, periksa dokumentasi Aspose.Cells atau tinggalkan komentar di bawah. Selamat coding!

---

![Create new workbook example](/images/create-new-workbook.png "Screenshot showing a C# IDE with the create new workbook code")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}