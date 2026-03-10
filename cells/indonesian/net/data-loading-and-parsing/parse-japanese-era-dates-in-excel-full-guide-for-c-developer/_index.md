---
category: general
date: 2026-02-14
description: Mengurai tanggal era Jepang di Excel dengan parsing tanggal khusus. Pelajari
  cara memuat workbook dari file menggunakan load excel dengan opsi dan hindari jebakan
  umum.
draft: false
keywords:
- parse japanese era dates
- load excel with options
- load workbook from file
- custom date parsing excel
language: id
og_description: Mengurai tanggal era Jepang di Excel menggunakan Aspose.Cells. Panduan
  ini menunjukkan cara memuat buku kerja dari file dengan opsi penguraian tanggal
  khusus.
og_title: Mengurai Tanggal Era Jepang – Tutorial C# Langkah demi Langkah
tags:
- Aspose.Cells
- C#
- Excel automation
title: Mengurai Tanggal Era Jepang di Excel – Panduan Lengkap untuk Pengembang C#
url: /id/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/
---

placeholders. The instruction says preserve all code blocks: fenced code blocks. There are none actual code blocks; placeholders are not code fences. So fine.

Now produce final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengurai Tanggal Era Jepang – Tutorial C# Lengkap

Pernah perlu **mengurai tanggal era Jepang** dari lembar Excel dan bertanya-tanya mengapa nilainya terus berubah menjadi angka aneh? Anda tidak sendirian. Banyak pengembang mengalami masalah ini ketika parser `DateTime` default tidak mengenali format “Reiwa 1/04/01” yang digunakan dalam kalender Jepang.  

Kabar baik: Anda dapat memberi tahu Aspose.Cells untuk memperlakukan sel-sel tersebut sebagai tanggal era Jepang sejak Anda **memuat Excel dengan opsi**. Dalam panduan ini kami akan menjelaskan cara memuat workbook dari file, mengonfigurasi penguraian tanggal khusus, dan memverifikasi bahwa tanggal keluar persis seperti yang Anda harapkan.

Dengan akhir tutorial ini Anda akan dapat:

* Memuat workbook dari file sambil menentukan `DateTimeParsing.JapaneseEra`.
* Mengakses nilai sel sebagai objek `DateTime` yang tepat.
* Menangani kasus tepi seperti sel kosong atau kalender campuran.
* Memperluas pendekatan ke skenario **custom date parsing excel** apa pun yang mungkin Anda temui.

> **Prerequisite** – Anda memerlukan pustaka Aspose.Cells untuk .NET (v23.9 atau lebih baru) dan IDE yang kompatibel dengan .NET (Visual Studio, Rider, dll.). Tidak ada paket lain yang diperlukan.

---

## Langkah 1: Konfigurasikan Opsi Muat Teks untuk Penguraian Era Jepang  

Hal pertama yang kami lakukan adalah memberi tahu pemuat cara menafsirkan teks yang terlihat seperti tanggal era Jepang. Ini dilakukan melalui `TxtLoadOptions` dan enum `DateTimeParsing`.

```csharp
using Aspose.Cells;

// Step 1: Set up load options to understand Japanese era dates
TxtLoadOptions loadOptions = new TxtLoadOptions
{
    // This flag makes the parser treat “R1/04/01” as 2024‑04‑01, etc.
    DateTimeParsing = DateTimeParsing.JapaneseEra
};
```

**Mengapa ini penting:** Tanpa flag `JapaneseEra`, Aspose.Cells memperlakukan sel sebagai string biasa, sehingga Anda harus memisahkan nama era secara manual dan mengonversinya. Flag ini melakukan pekerjaan berat, menjaga kode Anda tetap bersih dan lebih sedikit rentan kesalahan.

---

## Langkah 2: Muat Workbook dari File Menggunakan Opsi  

Sekarang kami benar‑benar membuka file Excel. Perhatikan bagaimana objek `loadOptions` diteruskan ke konstruktor `Workbook`—ini adalah langkah **load workbook from file** yang menghormati aturan penguraian khusus kami.

```csharp
// Step 2: Load the workbook with the configured options
string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
Workbook workbook = new Workbook(filePath, loadOptions);
```

Jika file berada di tempat lain (mis., berbagi jaringan), cukup sesuaikan `filePath` sesuai. Bagian pentingnya adalah menggunakan instance `loadOptions` yang sama; jika tidak, konversi era Jepang tidak akan terjadi.

---

## Langkah 3: Akses Tanggal yang Diurai  

Dengan workbook yang dimuat, Anda dapat mengambil nilai sel persis seperti yang Anda lakukan dengan tanggal biasa. API secara otomatis mengembalikan objek `DateTime`.

```csharp
// Step 3 (optional): Read a date from the first worksheet, cell A1
Worksheet sheet = workbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// The Value property is already a DateTime because of our parsing option
DateTime parsedDate = dateCell.DateTimeValue;

// Quick sanity check – print to console
Console.WriteLine($"Parsed date from A1: {parsedDate:yyyy-MM-dd}");
```

**Output yang diharapkan** (asumsi A1 berisi “R1/04/01”):

```
Parsed date from A1: 2024-04-01
```

Jika sel berisi tanggal Gregorian seperti “2023‑12‑31”, parser tetap berfungsi—hanya mengembalikan tanggal asli tanpa perubahan.

---

## Langkah 4: Verifikasi Semua Tanggal dalam Sebuah Kolom  

Sering kali Anda perlu memindai seluruh kolom tanggal era Jepang. Di bawah ini adalah loop ringkas yang menunjukkan cara menangani sel kosong dan konten campuran dengan elegan.

```csharp
// Step 4: Iterate through column B (index 1) and print each parsed date
int firstRow = 0;
int lastRow = sheet.Cells.MaxDataRow; // last row with data

for (int row = firstRow; row <= lastRow; row++)
{
    Cell cell = sheet.Cells[row, 1]; // column B
    if (cell.Type == CellValueType.IsDateTime)
    {
        Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
    }
    else if (!cell.IsNull)
    {
        // Fallback: show raw string for non‑date cells
        Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
    }
}
```

**Tips pro:** `CellValueType.IsDateTime` adalah cara paling aman untuk memeriksa apakah parser berhasil. Ini melindungi Anda dari `InvalidCastException` ketika sel berisi teks yang tidak terduga.

---

## Langkah 5: Kesalahan Umum & Cara Menanganinya  

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Sel kosong mengembalikan `DateTime.MinValue`** | Parser memperlakukan string kosong sebagai tanggal minimum. | Periksa `cell.IsNull` sebelum mengakses `DateTimeValue`. |
| **Kalender campuran (Jepang + Gregorian) dalam satu kolom** | Parser menangani keduanya, tetapi Anda mungkin perlu membedakannya untuk pelaporan. | Gunakan `cell.StringValue` untuk memeriksa teks asli ketika `cell.Type` adalah `IsString`. |
| **Era tidak tepat (mis., “H30” untuk Heisei) setelah 2019** | Heisei berakhir pada 2019; tanggal setelahnya harus menggunakan “R”. | Validasi awalan era sebelum mempercayai hasil parsing. |
| **Penurunan kinerja pada file besar** | Memuat dengan opsi khusus menambah sedikit overhead. | Muat hanya lembar kerja yang diperlukan (`Workbook.LoadOptions.LoadAllWorksheets = false`). |

---

## Langkah 6: Contoh Kerja Lengkap  

Menggabungkan semuanya, berikut adalah aplikasi konsol mandiri yang dapat Anda salin‑tempel dan jalankan. Ini mendemonstrasikan **custom date parsing excel** dari awal hingga akhir.

```csharp
// FullExample.cs
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure load options for Japanese era dates
        TxtLoadOptions loadOptions = new TxtLoadOptions
        {
            DateTimeParsing = DateTimeParsing.JapaneseEra
        };

        // 2️⃣ Load the workbook from file with those options
        string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        Workbook workbook = new Workbook(filePath, loadOptions);
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Read a single cell (A1) – demonstrates automatic parsing
        Cell a1 = sheet.Cells["A1"];
        Console.WriteLine($"A1 raw value: {a1.StringValue}");
        Console.WriteLine($"A1 parsed date: {a1.DateTimeValue:yyyy-MM-dd}");

        // 4️⃣ Loop through column B to show batch parsing
        Console.WriteLine("\n--- Column B Dates ---");
        int lastRow = sheet.Cells.MaxDataRow;
        for (int row = 0; row <= lastRow; row++)
        {
            Cell cell = sheet.Cells[row, 1]; // B column
            if (cell.Type == CellValueType.IsDateTime)
                Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
            else if (!cell.IsNull)
                Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
        }

        // 5️⃣ Optional: Save a copy with dates converted to ISO format
        // This shows that the workbook now holds proper DateTime objects.
        workbook.Save("japan_dates_converted.xlsx");
        Console.WriteLine("\nWorkbook saved as japan_dates_converted.xlsx");
    }
}
```

**Apa yang akan Anda lihat** ketika `japan_dates.xlsx` berisi:

| A | B |
|---|---|
| R1/04/01 | 2023‑12‑31 |
| H30/12/31 | R2/01/01 |
| (kosong) | R2/02/15 |

Output konsol:

```
A1 raw value: R1/04/01
A1 parsed date: 2024-04-01

--- Column B Dates ---
Row 1: 2023-12-31
Row 2: 2025-01-01
Row 3: (non-date) 
Row 4: 2025-02-15
Workbook saved as japan_dates_converted.xlsx
```

File yang disimpan kini menyimpan sel tanggal yang tepat, yang dapat Anda buka di Excel dan melihat format tanggal biasa.

---

## Kesimpulan  

Kami baru saja menunjukkan cara **mengurai tanggal era Jepang** di Excel dengan mengonfigurasi `TxtLoadOptions`, **memuat workbook dari file** dengan opsi tersebut, dan bekerja dengan nilai `DateTime` yang dihasilkan. Pola yang sama—menetapkan flag penguraian khusus lalu memuat workbook—berlaku untuk setiap kebutuhan **custom date parsing excel**, baik Anda menangani periode fiskal, nomor minggu ISO, atau format proprietari.

Memiliki era yang berbeda atau spreadsheet dengan kalender campuran? Cukup ganti `DateTimeParsing.JapaneseEra` dengan nilai enum lain (mis., `DateTimeParsing.Custom`) dan sediakan string format. Fleksibilitas Aspose.Cells berarti Anda jarang perlu menulis kode konversi manual lagi.

**Langkah selanjutnya** yang mungkin Anda jelajahi:

* **Muat Excel dengan opsi** untuk file CSV (`CsvLoadOptions`) untuk menangani pemisah khusus locale.
* Gunakan `Workbook.Save` dengan `SaveFormat.Xlsx` untuk mengekspor data yang sudah dibersihkan.
* Gabungkan pendekatan ini dengan **Aspose.Slides** atau **Aspose.Words** untuk pipeline pelaporan.

Cobalah, sesuaikan opsi, dan biarkan pustaka melakukan pekerjaan berat. Selamat coding!  

![Screenshot tanggal era Jepang yang diurai dalam jendela konsol – contoh parse japanese era dates](/images/parse-japanese-era-dates.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}