---
category: general
date: 2026-06-21
description: Salin buku kerja di C# dan ekspor tabel ke lembar kerja lain menggunakan
  Aspose.Cells. Ikuti panduan langkah demi langkah ini untuk solusi yang bersih dan
  dapat digunakan kembali.
draft: false
keywords:
- copy workbook in c#
- export table to another worksheet
language: id
og_description: Salin workbook di C# dan ekspor tabel ke lembar kerja lain dengan
  contoh lengkap yang dapat dijalankan. Pelajari mengapa pendekatan ini paling efektif.
og_title: Salin Workbook di C# – Ekspor Tabel ke Lembar Kerja Lain
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Copy workbook in C# and export table to another worksheet using Aspose.Cells.
    Follow this step‑by‑step guide for a clean, reusable solution.
  headline: Copy Workbook in C# – Export Table to Another Worksheet
  type: TechArticle
- description: Copy workbook in C# and export table to another worksheet using Aspose.Cells.
    Follow this step‑by‑step guide for a clean, reusable solution.
  name: Copy Workbook in C# – Export Table to Another Worksheet
  steps:
  - name: '**`Workbook.Copy()`** performs a deep clone of every worksheet, style,
      and formula. It’s the cleanest way to **copy workbook in C#** without manually
      iterating over sheets.'
    text: '**`Workbook.Copy()`** performs a deep clone of every worksheet, style,
      and formula. It’s the cleanest way to **copy workbook in C#** without manually
      iterating over sheets.'
  - name: '**`ExportTableOptions.ExportAsString = true`** tells Aspose.Cells to give
      us a CSV‑style string rather than a binary block. This makes it trivial to drop
      the data into any cell using `PutValue`.'
    text: '**`ExportTableOptions.ExportAsString = true`** tells Aspose.Cells to give
      us a CSV‑style string rather than a binary block. This makes it trivial to drop
      the data into any cell using `PutValue`.'
  - name: By exporting from the **source workbook** and inserting into the **destination
      workbook**, we keep the two files completely independent—no accidental cross‑contamination
      of references.
    text: By exporting from the **source workbook** and inserting into the **destination
      workbook**, we keep the two files completely independent—no accidental cross‑contamination
      of references.
  type: HowTo
tags:
- csharp
- aspose.cells
- excel automation
title: Menyalin Workbook di C# – Mengekspor Tabel ke Lembar Kerja Lain
url: /id/net/excel-copy-worksheet/copy-workbook-in-c-export-table-to-another-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salin Workbook di C# – Ekspor Tabel ke Worksheet Lain

Pernah bertanya-tanya bagaimana cara **copy workbook in C#** sambil memindahkan rentang data tertentu ke lembar baru? Anda tidak sendirian. Banyak pengembang mengalami kendala ini saat mengotomatiskan laporan, faktur, atau migrasi data. Kabar baiknya? Dengan beberapa baris kode Aspose.Cells Anda dapat menduplikasi workbook dan **export table to another worksheet** dalam satu alur kerja yang rapi.

Dalam tutorial ini kami akan membahas seluruh proses—mulai dari memuat file sumber, mengkloningnya, dan mengekspor rentang sebagai string, hingga menempelkan string tersebut ke lembar tujuan. Pada akhir tutorial Anda akan memiliki potongan kode yang mandiri dan siap produksi yang dapat Anda sisipkan ke proyek .NET mana pun.

## Apa yang Anda Butuhkan

- **Aspose.Cells for .NET** (versi 23.12 atau lebih baru). Ini adalah pustaka kuat yang menangani file Excel tanpa perlu menginstal Office.
- Lingkungan pengembangan .NET (Visual Studio, Rider, atau VS Code dengan ekstensi C#).
- Sebuah workbook contoh bernama `Formatted.xlsx` yang ditempatkan di direktori yang diketahui (kami akan merujuknya sebagai `YOUR_DIRECTORY/Formatted.xlsx`).

Tidak ada paket NuGet tambahan yang diperlukan selain Aspose.Cells, dan kode ini bekerja pada .NET 6+, .NET Framework 4.7+, atau .NET Core.

## Implementasi Langkah‑per‑Langkah

Berikut adalah program lengkap yang dapat dijalankan. Silakan salin‑tempel ke proyek aplikasi konsol dan tekan **F5**.

```csharp
using System;
using Aspose.Cells;

namespace WorkbookCopyExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load the source workbook
            // -------------------------------------------------
            // Adjust the path to point at your actual file location.
            string sourcePath = @"YOUR_DIRECTORY/Formatted.xlsx";
            Workbook sourceWorkbook = new Workbook(sourcePath);
            Console.WriteLine("Source workbook loaded successfully.");

            // -------------------------------------------------
            // Step 2: Set up export options – we want the range as a string
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true   // This forces the export to return CSV‑style text.
            };
            Console.WriteLine("Export options configured (ExportAsString = true).");

            // -------------------------------------------------
            // Step 3: Copy workbook in C# – creates an isolated clone
            // -------------------------------------------------
            // Using the Copy method ensures the original stays untouched.
            Workbook destinationWorkbook = sourceWorkbook.Copy();
            Console.WriteLine("Destination workbook created as a copy of the source.");

            // -------------------------------------------------
            // Step 4: Export the specified range (B2:B10) from the source sheet
            // -------------------------------------------------
            // The range is taken from the first worksheet (index 0).
            // ExportTable returns a string that can be written directly.
            string exportedTable = sourceWorkbook.Worksheets[0]
                .Cells.ExportTable(sourceWorkbook.Worksheets[0].Cells["B2:B10"],
                                   exportOptions);
            Console.WriteLine("Range B2:B10 exported as string:");
            Console.WriteLine(exportedTable);

            // -------------------------------------------------
            // Step 5: Paste the exported string into the destination sheet
            // -------------------------------------------------
            // We start at cell A1 of the first worksheet in the destination.
            destinationWorkbook.Worksheets[0].Cells["A1"]
                .PutValue(exportedTable);
            Console.WriteLine("Exported data placed at A1 in the destination workbook.");

            // -------------------------------------------------
            // Step 6: Save the result so you can verify it
            // -------------------------------------------------
            string resultPath = @"YOUR_DIRECTORY/Copy_With_ExportedTable.xlsx";
            destinationWorkbook.Save(resultPath);
            Console.WriteLine($"Result saved to {resultPath}");
        }
    }
}
```

### Mengapa Pendekatan Ini Berhasil

1. **`Workbook.Copy()`** melakukan kloning mendalam pada setiap worksheet, gaya, dan formula. Ini adalah cara paling bersih untuk **copy workbook in C#** tanpa harus iterasi manual pada lembar.
2. **`ExportTableOptions.ExportAsString = true`** memberi tahu Aspose.Cells untuk memberikan string bergaya CSV alih-alih blok biner. Hal ini memudahkan menempatkan data ke sel mana pun menggunakan `PutValue`.
3. Dengan mengekspor dari **source workbook** dan menyisipkan ke **destination workbook**, kita menjaga kedua file tetap sepenuhnya independen—tanpa kontaminasi referensi yang tidak disengaja.

## Kasus Tepi & Kesalahan Umum

| Situasi | Hal yang Perlu Diperhatikan | Perbaikan / Rekomendasi |
|-----------|-------------------|-----------------------|
| **Berbeda indeks worksheet** | Jika workbook sumber atau tujuan memiliki beberapa lembar, menghard‑code indeks `0` dapat menargetkan lembar yang salah. | Gunakan `Worksheets["SheetName"]` atau iterasi melalui `Worksheets` untuk menemukan lembar yang diinginkan. |
| **Rentang besar** | Mengekspor rentang yang sangat besar sebagai string dapat mencapai batas memori. | Pertimbangkan mengekspor dalam potongan atau menggunakan `ExportTable` dengan `ExportAsString = false` dan menangani aliran biner. |
| **Kehilangan format** | `ExportAsString` menghapus semua format; hanya nilai mentah yang dipertahankan. | Jika Anda membutuhkan gaya, ekspor sebagai `IEnumerable<CellArea>` dan salin sel secara individual. |
| **Masalah jalur file** | Jalur relatif dapat rusak ketika aplikasi dijalankan dari direktori kerja yang berbeda. | Gunakan `Path.Combine(Environment.CurrentDirectory, "Formatted.xlsx")` atau simpan jalur dalam konfigurasi. |

### Tips Pro

Jika Anda berencana menggunakan kembali data yang diekspor di beberapa workbook, bungkus logika ekspor‑dan‑tempel ke dalam metode bantu:

```csharp
static void ExportRangeToWorkbook(Workbook src, string range, Workbook dest, string destCell)
{
    var opts = new ExportTableOptions { ExportAsString = true };
    string data = src.Worksheets[0].Cells.ExportTable(src.Worksheets[0].Cells[range], opts);
    dest.Worksheets[0].Cells[destCell].PutValue(data);
}
```

Sekarang Anda dapat memanggil `ExportRangeToWorkbook(sourceWorkbook, "B2:B10", destinationWorkbook, "A1");` di mana pun Anda membutuhkannya.

## Memverifikasi Hasil

Buka `Copy_With_ExportedTable.xlsx` di Excel atau penampil spreadsheet apa pun:

- Worksheet pertama harus terlihat identik dengan `Formatted.xlsx` **kecuali** blok data baru yang dimulai di **A1**.
- Sel A1 hingga A9 (atau sebanyak baris yang dicakup B2:B10) akan berisi nilai yang diekspor, masing‑masing dipisahkan oleh pemisah default (koma untuk CSV). Jika Anda membutuhkan pemisah lain, atur `exportOptions.Separator` sebelum mengekspor.

Pemeriksaan visual tersebut mengonfirmasi bahwa operasi **copy workbook in C#** dan **export table to another worksheet** berhasil.

## Kesimpulan

Kami baru saja menunjukkan pola bersih dan dapat diulang untuk **copy workbook in C#** sekaligus **exporting a table to another worksheet**. Hal utama yang dapat dipelajari adalah:

- Gunakan `Workbook.Copy()` untuk kloning mendalam yang aman.
- Manfaatkan `ExportTableOptions.ExportAsString` untuk mengubah rentang menjadi string yang dapat dipindahkan.
- Sisipkan string tersebut di mana pun Anda membutuhkannya dengan `PutValue`.

Dari sini Anda dapat mengeksplorasi:

- Mengekspor beberapa rentang yang tidak berurutan.
- Mengonversi string menjadi array 2‑D untuk manipulasi data yang lebih kaya.
- Mengotomatiskan proses di seluruh folder workbook (pemrosesan batch).

Cobalah, sesuaikan rentangnya, dan lihat bagaimana teknik ini menyederhanakan pipeline otomatisasi Excel Anda. Jika Anda menemukan kendala atau memiliki ide untuk ekstensi, silakan tinggalkan komentar di bawah. Selamat coding!

![Diagram contoh copy workbook di C#](https://example.com/images/copy-workbook-diagram.png "Contoh copy workbook di C# yang menunjukkan langkah sumber, ekspor, dan tujuan")


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Salin Worksheet dari Satu Workbook ke Workbook Lain menggunakan Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)
- [Salin Sheet dalam Workbook Menggunakan Aspose.Cells untuk .NET - Panduan Langkah-demi-Langkah](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [Salin Data dalam Workbook menggunakan Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-data-within-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}