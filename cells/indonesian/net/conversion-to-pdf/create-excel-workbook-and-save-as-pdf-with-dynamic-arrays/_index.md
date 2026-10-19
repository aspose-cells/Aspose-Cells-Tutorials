---
category: general
date: 2026-09-15
description: Buat workbook Excel dengan C# dan pelajari cara menyimpan workbook sebagai
  PDF sambil menyebarkan array dinamis menggunakan fungsi EXPAND.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: id
lastmod: 2026-09-15
og_description: Buat workbook Excel dengan C# dan dengan cepat simpan workbook sebagai
  PDF sambil menggunakan fungsi EXPAND untuk menumpahkan array dinamis.
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: Buat buku kerja Excel dan simpan sebagai PDF dengan array dinamis
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: Buat buku kerja Excel dan simpan sebagai PDF dengan array dinamis
url: /id/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Buku Kerja Excel dan Simpan sebagai PDF dengan Array Dinamis

Jika Anda perlu **create Excel workbook** secara programatis dan kemudian **save workbook as PDF**, panduan ini menunjukkan solusi lengkap end‑to‑end dalam C#. Anda juga akan melihat cara **spill dynamic array** hasil dengan menggunakan **EXPAND function**, yang merupakan cara modern untuk menghasilkan array tanpa VBA.  

Apakah Anda sedang membangun layanan pelaporan, fitur ekspor untuk sistem ERP, atau dasbor berbasis data, langkah‑langkah di bawah ini memungkinkan Anda menghasilkan sebuah workbook, mengisinya dengan data smart‑marker, dan menghasilkan PDF yang mempertahankan fitur font lanjutan.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* .NET 6.0 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.8)
* Versi terbaru **Aspose.Cells for .NET** (v25.8 atau lebih baru) – menyediakan `Workbook`, `PdfSaveOptions`, dan `SmartMarkerProcessor`.
* IDE seperti Visual Studio 2022 (editor apa pun yang dapat mengompilasi C# dapat digunakan).

Tambahkan paket NuGet ke proyek Anda:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## Langkah 1: Create Excel workbook dan siapkan lembar kerja pertama

Tugas pertama adalah **create Excel workbook** dan mendapatkan referensi ke lembar kerja default. Lembar kerja ini akan menampung array dinamis dan template Smart Marker.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*Mengapa ini penting*: Menginstansiasi `Workbook` mengalokasikan struktur internal workbook, sementara mengakses `Worksheets[0]` memberi Anda lembar siap pakai tanpa harus menambahkannya secara manual.

## Langkah 2: Spill dynamic array menggunakan EXPAND function

**EXPAND function** Excel dapat mengubah literal array statis menjadi rentang spill dengan ukuran apa pun. Di sini kami meminta Excel untuk memperluas `{1,2,3}` menjadi rentang 5‑baris × 1‑kolom yang dimulai dari `A1`.

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*Mengapa ini penting*: Menggunakan `EXPAND` menghindari loop manual di C#. Mesin menghitung rentang spill dan menyimpan nilai langsung ke lembar kerja, yang kemudian muncul di PDF.

## Langkah 3: Save workbook as PDF sambil mempertahankan font variation selectors

Saat Anda perlu **save workbook as PDF**, Anda juga dapat mengaktifkan fitur tipografi lanjutan seperti font variation selectors (tersedia sejak Aspose.Cells v25.8). Ini memastikan PDF menampilkan skrip kompleks dengan benar.

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*Mengapa ini penting*: Menetapkan `FontVariationSelectors` ke `true` penting untuk bahasa yang bergantung pada variasi glyph (mis., Cina, Jepang, emoji). PDF yang dihasilkan mencerminkan tampilan Excel di layar.

## Langkah 4: Insert a Smart Marker template yang merujuk ke sumber data bersarang

Smart Markers memungkinkan Anda menyisipkan placeholder langsung di lembar kerja. Template di bawah ini akan menghasilkan daftar pesanan dan itemnya.

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*Mengapa ini penting*: Dengan menempatkan template di `A1`, Anda memberi tahu Aspose.Cells di mana memulai ekspansi data. Sintaks `:` (`Items:ItemName`) memberi tahu processor untuk mengiterasi koleksi bersarang.

## Langkah 5: Define the nested data source (orders containing items)

Kami membuat array anonim dari orders, masing‑masing berisi koleksi objek itemnya. Ini mencerminkan skenario master‑detail yang umum.

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*Mengapa ini penting*: Struktur bersarang ini menunjukkan **how to create dynamic array in Excel** melalui Smart Markers, tanpa menulis VBA atau loop sel manual.

## Langkah 6: Process the Smart Markers dan simpan file Excel akhir

Sekarang kami menyerahkan workbook dan sumber data ke `SmartMarkerProcessor`. Setelah diproses, placeholder digantikan dengan baris sebenarnya, dan kami menyimpan hasilnya sebagai file `.xlsx` biasa.

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*Mengapa ini penting*: `SmartMarkerProcessor` secara otomatis memperluas template, membuat baris yang diperlukan, dan mengisinya dengan data. Workbook akhir dapat dibuka di Excel untuk memverifikasi bahwa setiap order dan itemnya muncul dengan benar.

## Output yang Diharapkan

* **VarSelector.pdf** – file PDF yang menampilkan angka 1‑3 spill ke bawah lima baris, dirender dengan variasi font OpenType apa pun yang Anda aktifkan.
* **NestedSmartMarker.xlsx** – file Excel dengan baris berikut (dimulai dari `A1`):

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

Versi PDF mempertahankan spill numerik yang sama karena keadaan lembar kerja disimpan sebelum pemrosesan Smart Marker; Anda dapat mengulangi penyimpanan PDF setelah pemrosesan jika memerlukan data akhir dalam PDF juga.

## Tips Pro dan Kesalahan Umum

| Tip | Penjelasan |
|-----|------------|
| **Reuse the same `PdfSaveOptions`** | Membuat objek opsi sekali dan menggunakannya kembali menghindari perbedaan halus dalam rendering (mis., selector variasi yang hilang). |
| **Call `ws.Calculate()` after setting formulas** | Tanpa perhitungan eksplisit, rentang spill mungkin tetap kosong saat Anda memeriksa workbook secara programatis. |
| **Place Smart Marker templates on a clean sheet** | Mencampur template dengan data yang ada dapat menyebabkan penyisipan baris yang tidak terduga. Gunakan lembar khusus jika memungkinkan. |
| **Mind the file paths** | Gunakan `Path.Combine(Environment.CurrentDirectory, "output.pdf")` untuk menghindari direktori yang di‑hard‑code pada mesin yang berbeda. |
| **Version check** | `FontVariationSelectors` hanya tersedia mulai versi 25.8; versi lebih lama akan mengabaikan properti ini tanpa menimbulkan error. |

## Langkah Selanjutnya

Sekarang Anda tahu cara **create Excel workbook**, **spill dynamic array**, dan **save workbook as PDF**, Anda dapat menjelajahi:

* Menambahkan diagram atau gambar sebelum konversi PDF.
* Mengekspor workbook yang sama ke format lain (mis., HTML, CSV) menggunakan overload `Save`.
* Menggunakan **Smart Marker expressions** (`${Orders.Total:SUM(Items.Price)}`) untuk menghitung agregat secara langsung.
* Mengintegrasikan kode ini ke dalam API ASP.NET Core sehingga pengguna dapat mengunduh PDF yang dihasilkan langsung dari endpoint web.

---

**Ringkasan** – Tutorial ini menunjukkan cara **create Excel workbook**, menggunakan **EXPAND function** untuk **spill dynamic array**, menyematkan **Smart Marker** yang bekerja dengan sumber data bersarang, dan akhirnya **save workbook as PDF** sambil mempertahankan fitur font lanjutan. Contoh lengkap yang dapat dijalankan dapat disalin ke proyek C# mana pun dan disesuaikan dengan struktur data Anda sendiri. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat dan Simpan Buku Kerja Excel sebagai PDF di ASP.NET Menggunakan Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Cara Membuat dan Menyimpan Buku Kerja Excel sebagai ODS Menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Cara Membuat dan Menyimpan Buku Kerja Excel sebagai SVG menggunakan Aspose.Cells untuk Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}