---
category: general
date: 2026-10-01
description: Pelajari cara membuat workbook Excel dengan C# dan menerapkan format
  angka khusus, mengatur jumlah desimal sel, serta menyimpan workbook sebagai XLSX
  dalam panduan langkah demi langkah yang lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: id
lastmod: 2026-10-01
og_description: Buat workbook Excel dengan C# menggunakan format angka khusus, atur
  jumlah desimal sel, dan simpan workbook sebagai XLSX. Ikuti panduan lengkap ini
  untuk output numerik yang tepat.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: Buat workbook Excel C# – format angka khusus & ekspor XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Cara membuat workbook Excel C# dengan format angka khusus
url: /id/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat Excel workbook C# dengan format angka khusus

Jika Anda perlu **create excel workbook c#** yang menampilkan angka persis seperti yang Anda inginkan, panduan ini menunjukkan cara melakukannya dalam beberapa langkah jelas. Anda akan belajar menerapkan custom number format, mengatur cell decimal places, dan akhirnya **save workbook as xlsx** untuk konsumsi lebih lanjut.

Bekerja dengan data numerik sering berarti menyeimbangkan presisi dan keterbacaan. Pada akhir tutorial ini Anda akan memiliki pola yang dapat digunakan kembali yang membatasi digit yang ditampilkan ke jumlah angka signifikan tertentu sambil mempertahankan nilai asli dalam file. Tidak diperlukan skrip eksternal—hanya C# dan perpustakaan Aspose.Cells.

## Prasyarat

* .NET 6.0 SDK atau yang lebih baru terinstal  
* Visual Studio 2022 (atau IDE C# apa pun)  
* Paket NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`) – perpustakaan ini menyediakan kelas `Workbook`, `Worksheet`, dan `ExportTableOptions` yang digunakan dalam contoh.  

Persyaratan ini minimal; kode yang sama berfungsi di .NET Core, .NET Framework, dan bahkan di Azure Functions.

## Langkah 1: Buat Excel workbook C# – inisialisasi file

Operasi pertama adalah menginstansiasi objek `Workbook` baru. Objek ini mewakili seluruh file Excel dalam memori dan secara otomatis berisi worksheet default.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Mengapa ini penting:**  
Membuat workbook di awal memberi Anda kanvas bersih. Worksheet default (`Worksheets[0]`) siap untuk entri data, jadi Anda tidak perlu menambahkan sheet baru kecuali skenario Anda memerlukan beberapa tab.

## Langkah 2: Tulis nilai numerik ke sel

Sekarang masukkan angka contoh ke sel **A1**. Nilai yang kami gunakan (`123.456789`) memiliki lebih banyak tempat desimal daripada yang akhirnya ingin kami tampilkan, yang memungkinkan kami mendemonstrasikan pembulatan nanti.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Tip:** `PutValue` secara otomatis mendeteksi tipe data, sehingga Anda tidak perlu mengonversi angka menjadi string.

## Langkah 3: Terapkan custom number format – batasi desimal yang terlihat

Untuk mengontrol bagaimana Excel menampilkan angka, kami membuat `Style` dengan **custom number format**. Pola `"0.######"` memberi tahu Excel untuk menampilkan hingga enam tempat desimal tetapi menghilangkan nol di akhir.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**Cara kerjanya:**  
String format mengikuti sintaks custom‑format Excel. `0` memaksa menampilkan digit, sementara `#` menampilkan digit hanya jika signifikan. Dengan menggabungkannya Anda mendapatkan tampilan fleksibel yang tetap menghormati presisi asli.

## Langkah 4: Atur cell decimal places – menggunakan ExportTableOptions

Jika Anda perlu **set cell decimal places** untuk data yang diekspor (mis., saat mengonversi ke DataTable), Aspose.Cells memungkinkan Anda menentukan jumlah **significant digits**. Langkah ini memastikan CSV atau DataTable yang diekspor menghormati aturan pembulatan yang sama yang Anda terapkan di workbook.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Mengapa menggunakan `SignificantDigits`?**  
Berbeda dengan jumlah desimal tetap, significant digits mempertahankan besaran angka sambil membatasi presisi, yang sering kali menjadi harapan analis saat merangkum data.

## Langkah 5: Ekspor data worksheet dan **save workbook as xlsx**

Akhirnya, ekspor data (jika Anda membutuhkan DataTable) dan simpan workbook ke disk. Pemanggilan `ExportDataTable` menghormati `ExportTableOptions` yang kami konfigurasikan, dan `workbook.Save` menulis file XLSX standar.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Hasil yang diharapkan:**  
Saat Anda membuka *SigDigits.xlsx* di Excel, sel **A1** menampilkan `123.5`. Nilai yang mendasarinya tetap `123.456789`, tetapi angka yang ditampilkan menghormati aturan 4‑significant‑digit. Jika Anda mengekspor sheet ke DataTable, nilai dalam tabel juga akan dibulatkan menjadi `123.5`.

---

## Terapkan custom number format ke sel tambahan

Jika Anda perlu memformat rentang bukan satu sel, gunakan kembali objek `Style`:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Pro tip:** Menggunakan kembali objek style mengurangi beban memori dan menjamin format yang konsisten di seluruh sheet.

## Cara memformat angka di Excel menggunakan C# – variasi umum

| Skenario | String format | Hasil |
|----------|---------------|--------|
| Fixed two decimal places | `"0.00"` | `123.46` |
| Currency (US) | `"$#,##0.00"` | `$123.46` |
| Percentage with one decimal | `"0.0%"` | `12,346.0%` |
| Scientific notation | `"0.00E+00"` | `1.23E+02` |

Pilih pola yang sesuai dengan kebutuhan pelaporan Anda. Semua pola kompatibel dengan properti `Style.Custom` yang telah ditunjukkan sebelumnya.

## Atur cell decimal places secara dinamis berdasarkan input pengguna

Kadang-kadang presisi yang dibutuhkan tidak diketahui pada waktu kompilasi. Anda dapat membangun string format pada runtime:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Kasus tepi:** Jika `decimals` bernilai nol, format menjadi `"0"` (tampilan integer). Selalu validasi input pengguna untuk menghindari string format yang tidak valid.

## Simpan workbook sebagai XLSX – praktik terbaik

* **Gunakan path absolut** saat menulis ke direktori yang diketahui (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* **Dispose** `Workbook` jika Anda membungkusnya dalam pernyataan `using` untuk membebaskan sumber daya tak terkelola dengan cepat:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Kompatibilitas versi:** Aspose.Cells menulis file yang kompatibel dengan Excel 2010‑2023, sehingga pengguna downstream tidak akan mengalami masalah format.

---

## Contoh kerja lengkap

Berikut adalah program lengkap yang dapat Anda salin, tempel, dan jalankan segera. Program ini mencakup semua direktif `using` yang diperlukan, komentar, dan penanganan error.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Langkah verifikasi**

1. Jalankan program (`dotnet run`).  
2. Buka `SigDigits.xlsx`.  
3. Pastikan **A1** menampilkan `123.5`.  
4. Jika Anda membuka XML file (`.xlsx` adalah arsip zip), Anda akan melihat format khusus `"0.######"` disimpan di atribut `s` elemen `<c>`.

## Kesimpulan

Dalam tutorial ini Anda belajar cara **create excel workbook c#**, **apply custom number format**, **set cell decimal places**, dan **save workbook as xlsx** menggunakan Aspose.Cells. Solusi ini menunjukkan baik format visual di dalam Excel maupun pembulatan ekspor data melalui `ExportTableOptions`.  

Dari sini Anda dapat:

* Memperluas pendekatan ke seluruh rentang atau tabel.  
* Menggabungkan beberapa style (font, border) dengan `StyleFlag`.  
* Mengotomatiskan pembuatan laporan dengan melakukan loop pada sumber data dan menerapkan logika format yang sama.  

Silakan bereksperimen dengan string format yang berbeda, jumlah desimal, atau opsi ekspor untuk menyesuaikan kebutuhan pelaporan spesifik Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode kerja lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Excel Workbook C# – Terapkan Format Mata Uang dan Impor DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Buat Excel Workbook C# – Panduan Langkah‑per‑Langkah dengan Conditional Formatting](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Buat Excel Workbook C# – Tambahkan Komentar & Simpan sebagai XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}