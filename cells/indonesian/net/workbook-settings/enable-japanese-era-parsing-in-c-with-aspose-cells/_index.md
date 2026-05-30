---
category: general
date: 2026-05-30
description: Aktifkan parsing era Jepang dalam C# menggunakan Aspose.Cells. Pelajari
  cara mengatur budaya workbook, mem-parsing tanggal era, dan menangani kalender Jepang
  di lembar kerja Excel.
draft: false
keywords:
- enable japanese era parsing
- Aspose.Cells Japanese era
- set workbook culture
- parse era dates
- c# excel date parsing
language: id
og_description: Aktifkan parsing era Jepang di C# dengan Aspose.Cells. Panduan ini
  menunjukkan cara mengatur budaya workbook, mengaktifkan dukungan era, dan bekerja
  dengan tanggal Jepang.
og_title: Aktifkan Parsing Era Jepang di C# – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Enable Japanese era parsing in C# using Aspose.Cells. Learn to set
    workbook culture, parse era dates, and handle Japanese calendar in Excel worksheets.
  headline: Enable Japanese Era Parsing in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Aktifkan Parsing Era Jepang di C# dengan Aspose.Cells
url: /id/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aktifkan Parsing Era Jepang di C# dengan Aspose.Cells

Pernah perlu **mengaktifkan parsing era Jepang** saat menghasilkan file Excel untuk klien Jepang? Anda tidak sendirian—banyak pengembang mengalami kesulitan ketika kalender Jepang lama (令和, 平成, dll.) muncul dalam data. Kabar baiknya, Aspose.Cells memudahkan pengenalan tanggal era tersebut dan mengubahnya menjadi nilai Gregorian standar.

Dalam tutorial ini kita akan melangkah melalui cara **mengaktifkan parsing era Jepang** menggunakan Aspose.Cells, mengatur budaya workbook ke Jepang, dan menyisipkan tanggal berformat era ke dalam sel. Pada akhir tutorial Anda akan memiliki cuplikan C# yang dapat dijalankan yang mengubah “令和3年5月1日” menjadi objek tanggal `2021‑05‑01` yang tepat. Tidak perlu dokumentasi eksternal—cukup salin, tempel, dan jalankan.

## Prasyarat

- .NET 6.0 atau lebih baru (kode ini bekerja dengan .NET Core, .NET Framework, dan .NET 5+)
- Aspose.Cells untuk .NET (paket NuGet `Aspose.Cells`)
- Pengetahuan dasar C#—jika Anda dapat menulis `Console.WriteLine`, Anda sudah siap
- IDE pilihan Anda (Visual Studio, VS Code, Rider…)

> **Pro tip:** Pastikan versi Aspose.Cells Anda terbaru; versi 24.10+ sudah mencakup definisi era Jepang terbaru.

## Mengapa Mengaktifkan Parsing Era Jepang?

Kalender Jepang menggunakan era yang terkait dengan masa pemerintahan kaisar. Untuk kebanyakan aplikasi modern Anda ingin menyimpan tanggal dalam format Gregorian yang familiar, tetapi data sumber mungkin masih datang sebagai “令和3年5月1日”. Jika Anda melewatkan **mengaktifkan parsing era Jepang**, string tersebut akan diperlakukan sebagai teks biasa, yang akan merusak perhitungan, pengurutan, dan pembuatan grafik. Dengan mengaktifkan dukungan era, Aspose.Cells secara otomatis mengonversi string tersebut menjadi nilai `DateTime` yang tepat, menjaga keterbacaan bagi pengguna Jepang serta keakuratan numerik untuk proses selanjutnya.

## Langkah 1: Atur Budaya Workbook ke Bahasa Jepang

Hal pertama yang harus Anda lakukan adalah memberi tahu Aspose.Cells bahwa locale default workbook adalah Jepang (`ja-JP`). Ini memastikan bahwa setiap parsing yang bergantung pada budaya (termasuk nama era) mengikuti aturan Jepang.

```csharp
using Aspose.Cells;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Set the workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");
```

> **Mengapa ini penting:** Objek `CultureInfo` mengontrol format angka, pemisah tanggal, dan yang paling penting bagi kita, sistem kalender yang digunakan saat mem-parsing string.

## Langkah 2: Aktifkan Parsing Era Jepang

Setelah budaya diatur, Anda perlu mengaktifkan opsi yang memberi tahu Aspose.Cells untuk mengenali tanggal era. Inilah inti dari **mengaktifkan parsing era Jepang**.

```csharp
        // Enable parsing of Japanese era dates (令和, 平成, 昭和, etc.)
        workbook.Settings.UseJapaneseEra = true;
```

> **Kesalahan umum:** Lupa mengatur flag ini berarti “令和3年5月1日” tetap menjadi string literal. Dengan flag aktif, Aspose.Cells memetakan era ke tahun Gregorian yang benar secara otomatis.

## Langkah 3: Sisipkan Tanggal Berformat Era ke dalam Sel

Dengan budaya dan dukungan era yang siap, menyisipkan string era Jepang menjadi sangat mudah. Perpustakaan akan mem-parsingnya dan menyimpan nilai `DateTime` yang sebenarnya.

```csharp
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Insert a Japanese era date string into cell A1
        // The string "令和3年5月1日" becomes 2021‑05‑01 internally
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Save the workbook to verify the result
        workbook.Save("JapaneseEraDemo.xlsx");
    }
}
```

### Output yang Diharapkan

- **Sel A1** dalam file `JapaneseEraDemo.xlsx` yang dihasilkan akan menampilkan **2021‑05‑01** (atau format tanggal Jepang lokal jika Anda membukanya di Excel dengan locale Jepang).
- Nilai dasarnya adalah `DateTime` yang sesungguhnya, sehingga Anda dapat menggunakannya dengan aman dalam formula, pivot table, atau perhitungan C# lebih lanjut.

## Langkah 4: Verifikasi Tanggal yang Diparsing Secara Programatis (Opsional)

Jika Anda ingin memastikan bahwa parsing berhasil sebelum menyimpan, Anda dapat membaca kembali sel tersebut:

```csharp
        // Retrieve the value as a DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Output: Parsed date: 2021-05-01
```

Langkah verifikasi kecil ini berguna dalam unit test atau saat memproses file Excel yang diberikan pengguna.

## Kasus Khusus & Variasi

| Skenario | Apa yang Harus Dilakukan |
|----------|--------------------------|
| **Beberapa era dalam satu workbook** | Biarkan `UseJapaneseEra = true`; Aspose.Cells akan mengenali semua era yang didukung (令和, 平成, 昭和, 大正, 明治). |
| **Campuran string Gregorian dan era** | Parser secara otomatis membedakan; string Gregorian tetap tidak berubah. |
| **Kebutuhan kalender khusus** | Anda masih dapat mengatur `Workbook.Settings.Calendar` ke instance `Calendar` tertentu jika memerlukan kontrol lebih. |
| **Versi .NET lama** | Kode yang sama bekerja pada .NET Framework 4.6+; pastikan konstruktor `System.Globalization.CultureInfo` tersedia. |

## Tips Praktis untuk Proyek Dunia Nyata

- **Cache `CultureInfo`** jika Anda membuat banyak workbook dalam loop; membuatnya berulang-ulang menambah beban.
- **Validasi input** sebelum memanggil `PutValue`; string era yang tidak sesuai format akan melempar pengecualian.
- **Matikan parsing era** (`UseJapaneseEra = false`) ketika Anda yakin data tidak pernah berisi tanggal era—ini dapat meningkatkan performa sedikit.
- **Gunakan `Workbook.SaveOptions`** untuk mengontrol format output (XLSX, XLS, CSV) sambil mempertahankan tanggal yang telah diparsing.

## Contoh Lengkap yang Siap Digunakan (Copy‑Paste)

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class EnableJapaneseEraParsingDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Set workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");

        // 3️⃣ Enable Japanese era parsing
        workbook.Settings.UseJapaneseEra = true;

        // 4️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 5️⃣ Insert an era‑formatted date
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Optional: read back the parsed value
        DateTime dt = sheet.Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed date: {dt:yyyy-MM-dd}");

        // Save the workbook
        workbook.Save("EnableJapaneseEraParsing.xlsx");
    }
}
```

Jalankan program, buka file yang dihasilkan, dan Anda akan melihat **2021‑05‑01** di sel A1—bukti bahwa kita berhasil **mengaktifkan parsing era Jepang**.

## Kesimpulan

Kami telah menunjukkan cara **mengaktifkan parsing era Jepang** di C# menggunakan Aspose.Cells, mengatur budaya workbook, dan secara mulus mengonversi tanggal era seperti “令和3年5月1日” menjadi nilai Gregorian standar. Langkahnya singkat, kode terisolasi, dan hasilnya bekerja sempurna di Excel.

Siap untuk tantangan berikutnya? Coba gabungkan **set workbook culture** dengan pemformatan angka untuk Yen Jepang, atau buat laporan multi‑sheet yang mencampur tanggal Gregorian dan era. Anda kini memiliki fondasi untuk menangani segala keanehan kalender Jepang dalam proyek otomatisasi Excel .NET Anda.

---

*Jika panduan ini membantu Anda, pertimbangkan memberi bintang pada repositori GitHub Aspose.Cells atau berbagi tips Anda di kolom komentar. Selamat coding!*

## Apa yang Harus Anda Pelajari Selanjutnya?

- [Load Excel Workbooks with Culture-Specific Dates using Aspose.Cells for .NET](/cells/english/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Load Workbook Culture Specific Dates Aspose Cells Net](/cells/chinese/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}