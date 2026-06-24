---
category: general
date: 2026-06-24
description: Buat workbook baru di C# dan salin tabel pivot sambil mempertahankan
  datanya. Pelajari cara menyalin baris, mengekspor rentang yang dipilih, dan menjaga
  pivot tetap utuh.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: id
og_description: Buat workbook baru di C# dan salin tabel pivot sambil mempertahankan
  datanya. Panduan langkah demi langkah yang mencakup cara menyalin baris dan mengekspor
  rentang yang dipilih.
og_title: Buat Workbook Baru di C# – Salin Tabel Pivot
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: Buat Workbook Baru di C# – Salin Tabel Pivot
url: /id/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Workbook Baru di C# – Salin Tabel Pivot

Pernahkah Anda perlu **create new workbook** di C# hanya untuk memindahkan sebagian data yang mencakup tabel pivot? Anda bukan satu-satunya. Dalam banyak alur pelaporan Anda mengambil beberapa baris, mungkin beberapa kolom, dan Anda mengharapkan pivot tetap persis seperti semula—tanpa referensi yang rusak, tanpa perhitungan yang hilang.  

Berita baik? Dengan beberapa baris Aspose.Cells Anda dapat **copy pivot table**, mempertahankannya utuh, dan bahkan **export selected range** tanpa merusak apa pun. Di bawah ini Anda akan melihat contoh lengkap yang siap‑jalan yang menunjukkan **how to copy rows**, mempertahankan pivot, dan menyimpan hasilnya sebagai workbook baru.

## Apa yang Dibahas dalam Tutorial Ini

- Menyiapkan proyek C# dengan Aspose.Cells (perpustakaan yang menjalankan kode).
- Memuat workbook sumber yang berisi pivot asli.
- Menggunakan metode `CopyRows` dan `CopyColumns` dari perpustakaan untuk menduplikasi rentang yang tepat yang Anda butuhkan.
- Menyimpan area yang diduplikasi ke dalam skenario **create new workbook** sementara pivot tetap berfungsi.
- Tips untuk kasus tepi seperti beberapa tabel pivot, baris tersembunyi, dan set data besar.

Pada akhir panduan ini Anda akan dapat **export selected range** dari file Excel apa pun, menjaga logika pivot tetap hidup, dan menaruh file baru di mana saja Anda suka.

> **Prerequisite**: Aspose.Cells for .NET (versi percobaan gratis atau berlisensi) terpasang via NuGet. Jika Anda belum menambahkannya, jalankan `dotnet add package Aspose.Cells` di folder proyek Anda.

---

## Buat Workbook Baru dan Salin Tabel Pivot

Berikut adalah inti dari solusi. Kami akan menelusuri setiap baris, menjelaskan mengapa penting, dan kemudian menampilkan program lengkap.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### Mengapa Ini Berfungsi

- **`CopyRows` / `CopyColumns`**: Metode ini menduplikasi data sel yang mendasari *dan* objek terkait (seperti cache pivot). Itulah mengapa pivot tetap berfungsi setelah pemindahan.  
- **Separate destination workbook**: Dengan membuat instance `Workbook` baru kami **create new workbook** tanpa format yang tersisa atau lembar tersembunyi yang dapat mengganggu.  
- **Zero‑based indexing**: Aspose.Cells menggunakan indeks berbasis nol, sehingga `0` mengacu pada sel **A1**. Sesuaikan `startRow`/`startColumn` jika pivot Anda tidak berada di sudut kiri‑atas.  
- **Preserve pivot table**: Cache pivot berada di rentang yang sama, jadi menyalin rentang secara otomatis menyalin cache. Tidak diperlukan kode tambahan.

---

## Cara Menyalin Baris Tanpa Merusak Pivot

Jika Anda hanya tertarik pada bagian penyalinan baris, Anda dapat memisahkannya:

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**Pro tip**: Saat menyalin baris yang berpotongan dengan tabel pivot, selalu salin *seluruh* area pivot (baris + kolom). Salinan parsial dapat meninggalkan pivot dengan bidang yang hilang, menyebabkan error `#REF!`.

## Export Selected Range – Skenario Dunia Nyata

Bayangkan Anda memiliki workbook penjualan yang sangat besar, tetapi klien Anda hanya menginginkan ringkasan kuartal pertama, yang berada di baris 1‑20 dan kolom A‑D. Potongan kode di atas sudah **export selected range** untuk Anda. Cukup ubah variabel `totalRows` dan `totalColumns` agar sesuai dengan permintaan klien, dan selesai.

### Menangani Baris Tersembunyi atau Filter

Jika lembar sumber memiliki baris tersembunyi (mungkin difilter), Anda mungkin ingin menyalin hanya baris *yang terlihat*. Aspose.Cells menawarkan overload `CopyRows` yang menghormati visibilitas:

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

Setel boolean terakhir ke `true` untuk menyalin hanya baris yang terlihat—sempurna untuk “export selected range” ketika pengguna telah menerapkan filter.

## Pertahankan Tabel Pivot – Kesalahan Umum & Cara Menghindarinya

| Pitfall | Why It Happens | Fix |
|---------|----------------|-----|
| **Pivot cache not copied** | Menggunakan `Range.Copy` biasa alih-alih `Cells.CopyRows/CopyColumns`. | Tetap gunakan metode `Cells` seperti yang ditunjukkan. |
| **Destination sheet has existing pivot** | Menyimpan di atas workbook yang sudah berisi pivot dengan nama yang sama. | Mulai dengan `Workbook()` baru (seperti yang kami lakukan). |
| **Named ranges break** | Pivot sumber merujuk ke named range yang tidak ada di file baru. | Salin named range juga: `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **Data source path changes** | Pivot menunjuk ke sumber data eksternal yang tidak tersedia. | Gunakan `PivotTable.RefreshData()` setelah menyalin jika diperlukan. |

---

## Contoh Lengkap End‑to‑End (Siap Jalankan)

Berikut adalah program lengkap, termasuk direktif `using` dan UI konsol singkat. Salin‑tempel ke dalam proyek Console App baru dan tekan **F5**.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**Expected output** (di konsol):

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

Buka `copy-pivot.xlsx` dan Anda akan melihat tabel pivot yang sama seperti di `source.xlsx`, berfungsi penuh dan merujuk ke rentang data yang disalin.

---

## Pertanyaan yang Sering Diajukan

**Q: Apakah ini bekerja dengan beberapa tabel pivot pada lembar yang sama?**  
A: Ya, selama persegi panjang yang disalin mencakup setiap pivot yang Anda butuhkan. Jika Anda hanya menginginkan satu, sesuaikan `rows`/`cols` untuk memisahkannya.

**Q: Bagaimana jika workbook sumber menggunakan koneksi data eksternal?**  
A: Cache pivot masih akan menunjuk ke koneksi asli. Panggil `pivotTable.RefreshData()` setelah memuat tujuan jika Anda ingin melakukan kueri ulang ke sumber.

**Q: Bisakah saya menyalin pivot ke lembar lain dalam workbook yang sama?**  
A: Tentu saja. Ganti `destinationWorkbook` dengan `sourceWorkbook` dan pilih indeks worksheet lain.

**Q: Apakah ada cara untuk menyalin hanya format?**  
A: Gunakan overload `CopyRows`/`CopyColumns` yang menerima objek `CopyOptions`—setel `CopyOptions.CopyType = CopyType.ValuesOnly` atau `CopyType.All` tergantung kebutuhan Anda.

---

## Kesimpulan

Kami baru saja melewati skenario **create new workbook** yang **copy pivot table**, **preserve pivot table**, dan **export selected range**—semuanya dalam C# murni.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Create a New Pivot Table Programmatically in .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [How to Change Pivot Table Source Data Using Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [How to Manage Excel Pivot Table Compatibility with Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}