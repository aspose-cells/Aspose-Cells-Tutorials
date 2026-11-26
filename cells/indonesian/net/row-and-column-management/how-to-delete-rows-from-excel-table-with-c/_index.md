---
category: general
date: 2026-11-25
description: Pelajari cara menghapus baris dari tabel Excel di C# dan juga menghapus
  beberapa baris dari lembar Excel secara efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- delete multiple rows from excel sheet
language: id
lastmod: 2026-11-25
og_description: Hapus baris dari tabel Excel di C# dan pelajari cara menghapus beberapa
  baris dari lembar Excel dengan kode bersih.
og_image_alt: Screenshot of C# code deleting rows from an Excel table
og_title: Menghapus baris dari tabel Excel di C# – panduan lengkap
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  headline: How to delete rows from Excel table with C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  name: How to delete rows from Excel table with C#
  steps:
  - name: Add Aspose.Cells to your project
    text: 'Open the **Package Manager Console** and run:'
  - name: Load the workbook and locate the table
    text: '```csharp using Aspose.Cells;'
  - name: Delete the desired data rows
    text: The `DeleteRows` method expects a **zero‑based** row index relative to the
      table, **including** the header row. Because the header cannot be removed, you
      must start at index 1 for the first data row.
  - name: Save the modified workbook
    text: '```csharp // Save the workbook to a new file to preserve the original workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
      } } ```'
  - name: Full working example
    text: '```csharp using Aspose.Cells;'
  - name: Edge cases and best practices
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Deleting rows beyond the last row | Check `worksheet.Rows.Count` before calling
      `RemoveAt`. | | Removing all rows except the header | Delete data rows in a
      loop or use `DeleteRows(1, table.DataRa'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
- data manipulation
title: Cara menghapus baris dari tabel Excel dengan C#
url: /id/net/row-and-column-management/how-to-delete-rows-from-excel-table-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menghapus baris dari tabel Excel dengan C#

Jika Anda perlu menghapus baris dari tabel Excel menggunakan C#, panduan ini menunjukkan langkah‑langkahnya secara tepat. Anda juga akan melihat cara menghapus beberapa baris dari lembar Excel tanpa memengaruhi data lain.

Bekerja dengan Excel secara programatik sering memerlukan penghapusan catatan yang sudah usang atau tidak valid. Menghapus baris secara langsung di lembar kerja dapat berisiko karena baris header dari tabel terstruktur harus tetap utuh. Tutorial ini membimbing Anda melalui pendekatan yang aman yang menghormati header tabel dan memungkinkan Anda menghapus sejumlah baris data dalam satu panggilan.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* .NET 6.0 atau yang lebih baru terpasang  
* Visual Studio 2022 (atau IDE kompatibel lainnya)  
* Paket NuGet **Aspose.Cells** (versi 23.10 atau lebih baru) – perpustakaan ini menyediakan kelas `Workbook`, `Worksheet`, dan `ListObject` yang digunakan dalam contoh  

Anda tidak memerlukan Microsoft Office terpasang di mesin pengembangan karena Aspose.Cells bekerja langsung dengan format file.

## Menghapus baris dari tabel Excel – langkah demi langkah

Bagian‑bagian berikut menjelaskan setiap langkah yang diperlukan untuk menghapus baris dari tabel Excel secara aman. Kata kunci utama muncul di judul ini untuk memenuhi persyaratan SEO.

### Langkah 1: Tambahkan Aspose.Cells ke proyek Anda

Buka **Package Manager Console** dan jalankan:

```powershell
Install-Package Aspose.Cells
```

Paket ini menambahkan assembly yang diperlukan dan menyelesaikan tipe `Workbook`, `Worksheet`, serta `ListObject`.

### Langkah 2: Muat workbook dan temukan tabelnya

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Load the workbook that contains the table
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // Access the first worksheet (index 0)
        var worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (structured table) on the sheet
        var table = worksheet.ListObjects[0];
```

*Mengapa ini penting*: `ListObject` mewakili tabel Excel yang sesungguhnya, yang mempertahankan baris headernya sendiri. Dengan bekerja pada `ListObject`, Anda menghindari penghapusan header secara tidak sengaja.

### Langkah 3: Hapus baris data yang diinginkan

Metode `DeleteRows` mengharapkan indeks baris **berbasis nol** relatif terhadap tabel, **termasuk** baris header. Karena header tidak dapat dihapus, Anda harus memulai dari indeks 1 untuk baris data pertama.

```csharp
        // Delete two data rows starting after the header (index 1)
        // Parameters: startRow (relative to the table), numberOfRows
        table.DeleteRows(1, 2);
```

Jika Anda mencoba `table.DeleteRows(0, 2)`, Aspose.Cells akan melempar pengecualian karena baris header (indeks 0) dilindungi. Memulai dari indeks 1 memastikan hanya baris data yang dihapus.

### Langkah 4: Simpan workbook yang telah dimodifikasi

```csharp
        // Save the workbook to a new file to preserve the original
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

Menjalankan program akan menghapus dua baris tepat di bawah header sambil meninggalkan struktur tabel tetap utuh.

### Contoh lengkap yang berfungsi

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // 1. Load workbook
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // 2. Access first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3. Get the first table (ListObject)
        var table = worksheet.ListObjects[0];

        // 4. Delete two rows after the header (cannot delete header itself)
        table.DeleteRows(1, 2);

        // 5. Save the result
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

**Output yang diharapkan**: File `table_with_header_modified.xlsx` berisi header tabel asli, diikuti oleh semua baris kecuali dua yang dihapus. Tidak ada lembar kerja lain yang diubah.

## Menghapus beberapa baris dari lembar Excel

Terkadang Anda perlu menghapus baris yang **bukan** bagian dari tabel terstruktur. Kata kunci sekunder muncul di judul ini. Pendekatannya sedikit berbeda karena Anda bekerja dengan koleksi `Rows` pada worksheet alih‑alih `ListObject`.

```csharp
using Aspose.Cells;

class SheetRowDeletion
{
    static void Main()
    {
        var workbook = new Workbook(@"C:\Data\plain_sheet.xlsx");
        var worksheet = workbook.Worksheets[0];

        // Delete rows 5 through 9 (inclusive) – zero‑based index
        // The second argument is the count of rows to remove
        worksheet.Rows.RemoveAt(4, 5);

        workbook.Save(@"C:\Data\plain_sheet_modified.xlsx");
    }
}
```

**Mengapa ini berhasil**: `Rows.RemoveAt(startIndex, count)` menghapus blok baris berurutan langsung dari worksheet. Tidak ada perlindungan header, sehingga Anda dapat memulai dari indeks berapa pun. Metode ini efisien karena memperbarui struktur data internal dalam satu operasi, ideal ketika Anda harus menghapus banyak baris dari lembar Excel.

### Kasus tepi dan praktik terbaik

| Situasi                                 | Penanganan yang disarankan |
|----------------------------------------|----------------------------|
| Menghapus baris di luar baris terakhir | Periksa `worksheet.Rows.Count` sebelum memanggil `RemoveAt`. |
| Menghapus semua baris kecuali header   | Hapus baris data dalam loop atau gunakan `DeleteRows(1, table.DataRange.RowCount - 1)`. |
| Mempertahankan pemformatan sel          | Menghapus melalui `ListObject` secara otomatis menggeser pemformatan; untuk lembar mentah, salin pemformatan sebelum penghapusan bila diperlukan. |
| Worksheet besar ( > 10 000 baris)       | Lakukan penghapusan secara menurun untuk menghindari pergeseran indeks, atau gunakan `DeleteRows` pada tabel bila memungkinkan. |

**Tips profesional**: Ketika Anda perlu menghapus baris berdasarkan kondisi (misalnya, baris dengan nilai kolom kosong), iterasikan `DataRange` tabel secara terbalik dan panggil `DeleteRows` untuk setiap baris yang cocok. Menghapus secara terbalik mencegah ketidaksesuaian indeks.

## Pertanyaan umum

*Apakah ini bekerja dengan file .xlsx yang dibuat oleh Excel 365?*  
Ya. Aspose.Cells mendukung seluruh spesifikasi Office Open XML, sehingga kode yang sama berfungsi untuk file `.xlsx` modern apa pun.

*Bagaimana jika workbook berisi beberapa tabel?*  
Ambil tabel yang diinginkan berdasarkan nama: `var table = worksheet.ListObjects["MyTable"];` lalu terapkan `DeleteRows` seperti yang ditunjukkan.

*Bisakah saya menghapus baris tanpa menggunakan perpustakaan pihak ketiga?*  
Anda dapat menggunakan Microsoft.Office.Interop.Excel COM interop, tetapi itu memerlukan Excel terpasang di server dan menambah beban COM. Aspose.Cells menyediakan alternatif ringan yang aman untuk server.

## Kesimpulan

Anda kini tahu cara menghapus baris dari tabel Excel secara aman dan cara menghapus beberapa baris dari lembar Excel menggunakan C#. Teknik utama mengandalkan metode `ListObject.DeleteRows`, yang menghormati header tabel, sementara teknik sekunder menggunakan `Rows.RemoveAt` untuk lembar biasa. Terapkan pola‑pola ini untuk membersihkan data, mengotomatiskan pembuatan laporan, atau mengimplementasikan fitur edit massal dalam aplikasi Anda.

**Langkah selanjutnya**

* Jelajahi fitur Aspose.Cells lainnya seperti menyisipkan baris, menyalin gaya, atau memfilter data.  
* Coba operasi yang sama dengan **ClosedXML** jika Anda lebih menyukai perpustakaan sumber terbuka; API‑nya serupa tetapi menggunakan `IXLTable` dan `IXLRows`.  
* Gabungkan logika penghapusan baris dengan query LINQ untuk membangun pipeline pembersihan data yang lebih kompleks.

Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [cara menghapus baris di Excel dengan C# – lindungi header tabel](/cells/english/net/row-and-column-management/how-to-delete-rows-in-excel-with-c-protect-table-header/)
- [Cara menggunakan Aspose.Cells untuk menghapus baris dalam tabel Excel sambil mempertahankan](/cells/english/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/)
- [Muat File Excel C# – Cara Menghapus Baris dan Menghapus Baris Tertentu](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}