---
category: general
date: 2026-02-15
description: Cara membuat workbook, mengonversi string menjadi tanggal, dan memformat
  sel sebagai tanggal dengan Aspose.Cells. Pelajari cara mengatur format angka sel
  dan membaca tanggal Excel dengan mudah.
draft: false
keywords:
- how to create workbook
- convert string to date
- format cell as date
- set cell number format
- read excel date
language: id
og_description: Cara membuat workbook, mengonversi string menjadi tanggal, dan memformat
  sel sebagai tanggal. Panduan lengkap langkah demi langkah untuk membaca tanggal
  Excel.
og_title: Cara membuat workbook dan mengonversi string menjadi tanggal di C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Cara membuat workbook dan mengonversi string menjadi tanggal di C#
url: /id/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat workbook dan mengonversi string menjadi tanggal di C#

Pernah bertanya-tanya **cara membuat workbook** yang mengubah teks biasa seperti `"R3-04-01"` menjadi nilai `DateTime` yang sebenarnya? Anda bukan satu-satunya—banyak pengembang mengalami masalah ini saat mengambil data dari sistem warisan atau input pengguna. Kabar baik? Dengan beberapa baris C# dan Aspose.Cells Anda dapat melakukannya dengan cepat, tanpa perlu parsing manual.

Dalam tutorial ini kami akan membahas seluruh proses: membuat workbook, menyisipkan string tanggal, menerapkan **format cell as date** yang tepat, memaksa engine untuk **set cell number format**, dan akhirnya **read excel date** kembali sebagai `DateTime`. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat dijalankan dan dapat dimasukkan ke proyek .NET mana pun.

## Prasyarat

- .NET 6+ (atau .NET Framework 4.7.2+)
- **Aspose.Cells for .NET** paket NuGet (`Install-Package Aspose.Cells`)
- Pemahaman dasar tentang sintaks C#
- IDE seperti Visual Studio atau VS Code (semua dapat digunakan)

Tidak diperlukan konfigurasi tambahan—Aspose.Cells menangani semua proses berat secara internal.

## Langkah 1: Cara membuat workbook – menginisialisasi file Excel

Pertama, kita memerlukan objek workbook baru. Anggaplah itu sebagai buku catatan kosong di mana setiap worksheet adalah sebuah halaman.

```csharp
using Aspose.Cells;

 // Step 1: Create a new workbook
 var workbook = new Workbook();          // Empty workbook with one default sheet
```

*Mengapa ini penting:* Membuat workbook memberi kita wadah untuk sel, gaya, dan formula. Tanpa itu, tidak ada tempat untuk menaruh string tanggal.

## Langkah 2: Mengonversi string menjadi tanggal – menyisipkan teks mentah

Sekarang kita menaruh string tanggal mentah ke sel **A1** pada worksheet pertama. String tersebut menggunakan format khusus (`R3-04-01`) yang tidak dikenali Excel secara langsung.

```csharp
 // Step 2: Insert a date string into cell A1 of the first worksheet
 var targetCell = workbook.Worksheets[0].Cells["A1"];
 targetCell.PutValue("R3-04-01");        // Raw text, not yet a date
```

*Mengapa kami melakukan ini:* `PutValue` menyimpan teks literal. Jika kita mencoba menetapkan `DateTime` secara langsung, format khusus akan hilang. Menyimpannya sebagai teks memungkinkan kita nanti menerapkan **set cell number format** yang memberi tahu Excel cara menafsirkannya.

## Langkah 3: Memformat sel sebagai tanggal – menerapkan style number 14

Style tanggal bawaan Excel 14 berkorespondensi dengan `mm-dd-yy`. Dengan menetapkan style ini kita memberi tahu engine, “Perlakukan konten sel ini sebagai tanggal.”

```csharp
 // Step 3: Apply a date number format (style number 14) to the cell
 targetCell.SetStyle(new Style { Number = 14 });
```

*Apa yang terjadi di balik layar:* Properti `Number` memetakan ke ID format‑angka internal Excel. Ketika workbook menghitung ulang, Excel akan mencoba mengubah teks menjadi tanggal serial menggunakan format yang diberikan.

## Langkah 4: Menetapkan format angka sel – memaksa perhitungan ulang

Excel tidak akan secara otomatis mengonversi teks sampai kita memintanya untuk mengevaluasi formula (atau, dalam kasus ini, menafsirkan ulang sel). Memanggil `CalculateFormula` memicu konversi tersebut.

```csharp
 // Step 4: Recalculate any formulas so the cell value is interpreted as a date
 workbook.CalculateFormula();
```

*Tip:* Jika Anda bekerja dengan banyak sel, Anda dapat memanggil `CalculateFormula` sekali setelah selesai semua pemformatan—ini menghemat beberapa milidetik.

## Langkah 5: Membaca tanggal Excel – mendapatkan nilai DateTime

Akhirnya, kita mengambil representasi `DateTime` dari sel. Aspose.Cells menampilkannya melalui `DateTimeValue`.

```csharp
 // Step 5: Retrieve the DateTime representation and display it
 Console.WriteLine(targetCell.DateTimeValue);
```

**Output yang diharapkan (dengan asumsi kalender Gregorian default):**

```
2023-04-01 00:00:00
```

Perhatikan bagaimana awalan `"R3-"` diabaikan karena parser tanggal Excel fokus pada bagian numerik ketika style adalah tanggal. Jika string Anda mengandung awalan lain, Anda mungkin perlu memprosesnya terlebih dahulu, tetapi untuk banyak format warisan pendekatan ini bekerja dengan sempurna.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program lengkap yang siap dijalankan:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook
        var workbook = new Workbook();

        // Step 2: Insert a date string into cell A1 of the first worksheet
        var targetCell = workbook.Worksheets[0].Cells["A1"];
        targetCell.PutValue("R3-04-01");

        // Step 3: Apply a date number format (style number 14) to the cell
        targetCell.SetStyle(new Style { Number = 14 });

        // Step 4: Recalculate any formulas so the cell value is interpreted as a date
        workbook.CalculateFormula();

        // Step 5: Retrieve the DateTime representation and display it
        Console.WriteLine(targetCell.DateTimeValue);
    }
}
```

Simpan ini sebagai `Program.cs`, pulihkan paket Aspose.Cells, dan jalankan `dotnet run`. Anda akan melihat `DateTime` yang diformat tercetak di konsol.

## Variasi Umum & Kasus Tepi

### String tanggal yang berbeda

Jika data sumber Anda berupa `"2023/04/01"` atau `"01‑Apr‑2023"`, Anda masih dapat menggunakan alur kerja yang sama—cukup ubah properti **Number** ke format yang cocok dengan pola tersebut (mis., `Number = 15` untuk `d-mmm-yy`).  

### Format khusus locale

Excel menghormati pengaturan locale workbook. Untuk memaksa parsing gaya US, atur budaya workbook:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");
```

### Ketika string tidak dikenali

Terkadang Excel tidak dapat menafsirkan tanggal (mis., `"R3-13-40"`). Dalam kasus tersebut, pra‑proses string:

```csharp
string raw = "R3-04-01";
string cleaned = raw.Replace("R3-", "");   // Remove the prefix
targetCell.PutValue(cleaned);
```

Kemudian terapkan format angka yang sama.

## Tips Pro & Jebakan

- **Pro tip:** Gunakan `StyleFlag` untuk memodifikasi hanya format angka, meninggalkan atribut gaya lainnya tidak berubah.  
  ```csharp
  var style = targetCell.GetStyle();
  style.Number = 14;
  var flag = new StyleFlag { Number = true };
  targetCell.SetStyle(style, flag);
  ```
- **Watch out for:** Menimpa style yang ada pada sel yang sudah memiliki border atau font. Pendekatan `StyleFlag` mencegah hal itu.
- **Performance note:** Jika Anda memproses ribuan baris, lakukan batch pemanggilan `CalculateFormula` setelah selesai semua pembaruan; memanggilnya per baris menambah beban yang tidak perlu.

## Kesimpulan

Anda kini tahu **how to create workbook**, **convert string to date**, **format cell as date**, **set cell number format**, dan akhirnya **read excel date** kembali menjadi `DateTime`. Polanya sederhana: sisipkan teks mentah, terapkan style tanggal, paksa perhitungan ulang, lalu baca nilainya.

Dari sini Anda dapat memperluas logika ke seluruh kolom, mengimpor data CSV, atau bahkan menghasilkan laporan yang secara otomatis menerjemahkan string tanggal warisan menjadi tanggal Excel yang tepat.

Siap untuk naik level? Coba terapkan format angka khusus (`Number = 22`) untuk menampilkan tanggal sebagai `yyyy-mm-dd`, atau jelajahi utilitas `DateTimeConversion` Aspose.Cells untuk skenario yang lebih kompleks.

Selamat coding! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}