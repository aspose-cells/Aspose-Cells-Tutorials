---
category: general
date: 2026-03-29
description: Pelajari cara mengekspor tabel Excel ke teks biasa, menulis string ke
  file, dan mengonversi tabel Excel menjadi CSV atau TXT menggunakan C#. Termasuk
  kode lengkap dan tips.
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: id
og_description: Cara mengekspor tabel Excel ke file teks di C#. Dapatkan solusi lengkap,
  kode, dan praktik terbaik untuk mengonversi tabel Excel serta menyimpan file TXT.
og_title: Cara Mengekspor Data Excel – Tutorial C# Lengkap
tags:
- C#
- Excel
- File I/O
title: Cara Mengekspor Data Excel – Panduan C# Langkah demi Langkah
url: /id/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengekspor Data Excel – Panduan Lengkap C#

Pernah bertanya-tanya **bagaimana cara mengekspor data Excel** tanpa membuka spreadsheet secara manual? Mungkin Anda perlu mengekspor sebuah tabel ke file teks sederhana untuk sistem legacy, atau Anda menginginkan ekspor CSV cepat untuk pipeline analisis data. Dalam tutorial ini kami akan membahas solusi praktis end‑to‑end yang **menulis string ke file** dan menunjukkan secara tepat cara **mengonversi tabel Excel** menjadi format teks berdelimiter menggunakan C#.

Kami akan membahas semuanya mulai dari memuat workbook, memilih tabel yang tepat, mengonfigurasi opsi ekspor, hingga akhirnya menyimpan hasilnya sebagai file `.txt`. Pada akhir tutorial Anda akan dapat **mengekspor tabel sebagai CSV** (atau delimiter apa pun yang Anda pilih) dan juga akan melihat beberapa trik berguna untuk **menyimpan file txt C#**. Tidak diperlukan alat eksternal—hanya beberapa paket NuGet dan sedikit kode.

---

## Apa yang Anda Butuhkan

- **.NET 6.0+** (atau .NET Framework 4.7.2 jika Anda lebih suka klasik)
- **Syncfusion.XlsIO** paket NuGet (kelas `ExportTableOptions` berada di sini)
- IDE C# dasar (Visual Studio, VS Code, Rider—semua dapat digunakan)
- Workbook Excel yang berisi setidaknya satu tabel (kami akan menggunakan `ws.Tables[0]` dalam contoh)

> Pro tip: Jika Anda belum memiliki library Syncfusion, jalankan  
> `dotnet add package Syncfusion.XlsIO.Net.Core` dari command line.

---

## Langkah 1 – Buka Workbook dan Ambil Tabel Pertama  

Hal pertama yang harus dilakukan adalah memuat file Excel dan mendapatkan referensi ke worksheet yang berisi tabel. Langkah ini penting karena operasi **convert excel table** bekerja pada objek `ITable`, bukan pada rentang sel mentah.

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*Mengapa ini penting:* Membuka workbook dengan `using` memastikan semua sumber daya yang tidak dikelola dibebaskan, mencegah masalah penguncian file nantinya ketika Anda mencoba **menulis string ke file**.

---

## Langkah 2 – Konfigurasikan Opsi Ekspor (Teks Biasa, Tanpa Header, Delimiter Titik Koma)  

Sekarang kita memberi tahu Syncfusion bagaimana tabel harus diserialisasi. `ExportTableOptions` memungkinkan Anda mengatur inklusi header, memilih delimiter, dan memutuskan apakah akan mendapatkan string atau array byte.

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*Mengapa ini penting:* Menetapkan `IncludeHeaders = false` seringkali sesuai dengan harapan sistem downstream yang sudah mengetahui urutan kolom. Mengubah delimiter adalah cara Anda **mengekspor tabel sebagai CSV** dengan pemisah khusus.

---

## Langkah 3 – Ekspor Tabel ke String  

Dengan opsi yang siap, kita memanggil `ExportToString`. Metode ini mengambil seluruh tabel (termasuk semua baris) dan mengembalikan satu string yang siap untuk output ke file.

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*Mengapa ini penting:* Pemanggilan `ExportToString` melakukan pekerjaan berat mengonversi grid Excel menjadi format berdelimiter. Ia menghormati `Delimiter` yang Anda tetapkan, sehingga Anda mendapatkan hasil **export table as csv** yang bersih tanpa pemrosesan tambahan.

---

## Langkah 4 – Tulis Teks yang Diekspor ke File  

Akhirnya, kita menyimpan string ke disk. `File.WriteAllText` adalah cara paling sederhana untuk **save txt file C#**; ia secara otomatis membuat file jika belum ada dan menimpanya jika sudah ada.

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*Mengapa ini penting:* Dengan menulis string secara langsung, Anda menghindari langkah konversi tambahan. File kini berisi baris seperti `Value1;Value2;Value3`, siap untuk parser downstream mana pun.

---

## Contoh Lengkap yang Berfungsi (Semua Langkah dalam Satu Tempat)  

Berikut adalah program lengkap yang siap disalin‑tempel yang menggabungkan semua yang telah dibahas. Program ini mencakup penanganan error dan komentar untuk kejelasan.

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**Output yang diharapkan** (isi dari `ExportedTable.txt`):

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

Setiap baris sesuai dengan baris dari tabel Excel asli, dengan nilai dipisahkan oleh titik koma. Jika Anda mengubah `Delimiter = ","` Anda akan mendapatkan file CSV klasik sebagai gantinya.

---

## Pertanyaan Umum & Kasus Tepi  

### Bagaimana Jika Workbook Saya Memiliki Beberapa Tabel?  
Anda dapat cukup mengubah `ws.Tables[0]` ke indeks yang sesuai, atau melakukan loop melalui `ws.Tables`:

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### Bagaimana Cara Menyertakan Header Kolom?  
Set `IncludeHeaders = true` di `ExportTableOptions`. Ini berguna ketika sistem downstream mengharapkan baris header.

### Bisakah Saya Mengekspor ke Folder Berbeda Secara Dinamis?  
Tentu saja. Gunakan `Path.Combine` dengan `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` atau jalur yang diberikan pengguna untuk membuat solusi lebih fleksibel.

### Bagaimana dengan File Besar?  
Untuk tabel yang sangat besar, pertimbangkan streaming output alih-alih memuat seluruh string ke memori:

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### Apakah Ini Berfungsi di .NET Core?  
Ya—Syncfusion.XlsIO mendukung .NET 5/6/7. Cukup referensikan paket NuGet yang sesuai dan Anda siap.

---

## Tips Pro untuk Ekspor yang Handal  

- **Validasi jalur file** sebelum menulis. Direktori yang hilang akan melempar `DirectoryNotFoundException`.  
- **Periksa `ExportAsString`** hanya ketika tabel muat dengan nyaman di memori; jika tidak, gunakan `ExportToStream` untuk dataset yang sangat besar.  
- **Perhatikan budaya**: jika data Anda menggunakan koma sebagai pemisah desimal, pilih delimiter titik koma (`;`) atau tab (`\t`) untuk menghindari kesalahan parsing CSV.  
- **Kunci versi**: Syncfusion kadang mengubah tanda tangan API. Tetapkan versi NuGet (`<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`) untuk menjaga reproducibility build Anda.

---

## Kesimpulan  

Dalam panduan ini kami menunjukkan **bagaimana cara mengekspor tabel Excel** ke file teks biasa menggunakan C#. Dengan memuat workbook, mengonfigurasi `ExportTableOptions`, mengekspor tabel ke string, dan akhirnya **menulis string ke file**, Anda kini memiliki pola yang kuat untuk tugas **convert excel table**, **export table as csv**, dan **save txt file C#**.

Silakan bereksperimen—ganti delimiter, sertakan header, atau lakukan loop pada beberapa tabel. Pendekatan yang sama bekerja untuk menghasilkan laporan CSV, memberi data ke parser legacy, atau sekadar mengarsipkan isi spreadsheet sebagai file teks ringan.

Ada skenario lain yang ingin Anda tangani? Mungkin Anda perlu **write string to file** secara asynchronous, atau ingin meng-zip output secara langsung. Lihat tutorial berikutnya tentang *asynchronous file I/O in C#* dan *zipping files with .NET* untuk melanjutkan momentum.

Selamat coding! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}