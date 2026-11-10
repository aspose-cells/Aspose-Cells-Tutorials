---
category: general
date: 2026-10-01
description: Pelajari cara menghapus baris dari tabel Excel dan mengubah nama tabel
  Excel menggunakan C#. Panduan langkah demi langkah dengan kode lengkap dan praktik
  terbaik.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows excel table
- change excel table name
- load excel workbook c#
- remove rows from excel table
- update excel table name
language: id
lastmod: 2026-10-01
og_description: Hapus baris dari tabel Excel dan ubah nama tabel Excel di C#. Ikuti
  tutorial lengkap ini untuk memuat buku kerja, memodifikasi tabel, dan menyimpan
  hasilnya.
og_image_alt: Screenshot showing C# code that deletes rows from an Excel table and
  updates the table name
og_title: Menghapus baris dari tabel Excel dan mengubah namanya di C# – panduan lengkap
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn to delete rows from an Excel table and change the Excel table
    name using C#. Step‑by‑step guide with full code and best practices.
  headline: How to delete rows from an Excel table and change its name in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Cara menghapus baris dari tabel Excel dan mengubah namanya di C#
url: /id/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menghapus baris dari tabel Excel dan mengubah namanya di C#

Jika Anda perlu **menghapus baris dari tabel Excel** saat bekerja dengan C#, panduan ini menunjukkan langkah‑langkah tepat yang diperlukan. Anda akan melihat cara **memuat workbook Excel di C#**, menghapus baris tertentu dari sebuah tabel, dan kemudian **memperbarui nama tabel Excel** sehingga file tetap konsisten.

Tutorial ini mencakup semua yang perlu Anda ketahui: paket NuGet yang diperlukan, kode yang dapat dijalankan lengkap, dan jebakan umum seperti pelanggaran struktur tabel. Pada akhir artikel Anda dapat memodifikasi tabel Excel apa pun secara programatis tanpa intervensi manual.

## Prasyarat

* .NET 6.0 SDK atau yang lebih baru terpasang.
* Visual Studio 2022 (atau IDE C# apa pun) yang dikonfigurasi untuk pengembangan .NET.
* Perpustakaan **Aspose.Cells for .NET** ditambahkan melalui NuGet (`Install-Package Aspose.Cells`).
* Workbook Excel yang ada (`Table.xlsx`) yang berisi setidaknya satu lembar kerja dengan sebuah tabel.

Item‑item ini menyediakan lingkungan yang diperlukan untuk **memuat kode workbook Excel c#** dan mengeksekusi operasi dengan andal.

## Langkah 1: Muat workbook yang berisi tabel

Operasi pertama adalah membuka file workbook. Aspose.Cells membaca seluruh workbook ke dalam memori, memberi Anda kontrol penuh atas lembar kerja, tabel, dan data sel.

```csharp
using Aspose.Cells;

string inputPath = @"C:\Data\Table.xlsx";

// Load the workbook from disk
Workbook workbook = new Workbook(inputPath);
```

*Mengapa ini penting*: Memuat workbook adalah dasar untuk setiap manipulasi tabel selanjutnya. Objek `Workbook` mengekspos koleksi `Worksheets`, yang akan Anda gunakan untuk menemukan tabel target.

## Langkah 2: Akses lembar kerja pertama dan tabel pertamanya

Sebagian besar file Excel menyimpan tabel di lembar kerja pertama, tetapi Anda dapat menyesuaikan indeks jika diperlukan. Kode berikut mengambil objek `Table` pertama.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Retrieve the first table on that worksheet
Table table = sheet.Tables[0];
```

Jika lembar kerja tidak berisi tabel, `sheet.Tables.Count` akan menjadi nol dan Anda harus menangani kasus tersebut. Mencoba mengakses `sheet.Tables[0]` ketika tidak ada tabel akan melempar pengecualian, itulah mengapa klausa penjaga disarankan dalam kode produksi.

## Langkah 3: Hapus baris dari tabel Excel

Untuk **menghapus baris dari tabel Excel**, panggil `DeleteRows(startRow, totalRows)`. Parameter `startRow` berbasis nol relatif terhadap baris data pertama tabel (baris setelah header).

```csharp
// Delete two rows starting from the second data row (index 1)
int startRow = 1;   // second row within the table
int rowsToDelete = 2;

table.DeleteRows(startRow, rowsToDelete);
```

### Mengapa menggunakan `DeleteRows` alih‑alih menghapus baris lembar kerja?

`DeleteRows` memperbarui rentang internal tabel, mempertahankan formula, gaya, dan nama yang didefinisikan yang menjadi milik tabel. Menghapus baris lembar kerja secara langsung dapat merusak struktur tabel dan memicu pengecualian.

**Kasus tepi**: Jika penghapusan akan meninggalkan tabel tanpa baris data, Aspose.Cells melempar `ArgumentException`. Lindungi dari hal ini dengan memeriksa `table.RowCount` sebelum menghapus.

```csharp
if (table.RowCount - rowsToDelete < 1)
{
    throw new InvalidOperationException("Cannot delete all data rows from the table.");
}
```

## Langkah 4: Ubah nama tabel Excel

Setelah baris dihapus, Anda mungkin ingin memberi tabel identifier yang lebih deskriptif. Properti `Name` menetapkan nama yang didefinisikan untuk tabel, yang digunakan dalam formula dan VBA.

```csharp
// Assign a new name to the table
string newTableName = "SalesData2026";

if (workbook.Worksheets.GetDefinedNames().Any(d => d.Text == newTableName))
{
    throw new InvalidOperationException($"The name '{newTableName}' already exists as a defined name.");
}

table.Name = newTableName;
```

*Mengapa mengganti nama?* Nama tabel yang jelas meningkatkan keterbacaan dalam formula (`=SUM(SalesData2026[Amount])`) dan menghindari benturan nama ketika beberapa tabel memiliki tujuan serupa.

## Langkah 5: Simpan workbook yang dimodifikasi (opsional)

Simpan perubahan dengan menyimpan ke file baru atau menimpa yang asli. Menyimpan ke lokasi baru lebih aman selama pengembangan.

```csharp
string outputPath = @"C:\Data\ModifiedTable.xlsx";
workbook.Save(outputPath);
```

Metode `Save` menulis workbook yang diperbarui, termasuk rentang tabel yang diubah dan nama tabel baru, ke disk.

## Contoh kerja lengkap

Menggabungkan semua langkah menghasilkan program mandiri yang dapat Anda jalankan segera.

```csharp
using System;
using System.Linq;
using Aspose.Cells;

class ExcelTableModifier
{
    static void Main()
    {
        // ----- Step 1: Load workbook -----
        string inputPath = @"C:\Data\Table.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // ----- Step 2: Access worksheet and table -----
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Tables.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        Table table = sheet.Tables[0];

        // ----- Step 3: Delete rows -----
        int startRow = 1;      // second data row (zero‑based)
        int rowsToDelete = 2;

        if (table.RowCount - rowsToDelete < 1)
        {
            Console.WriteLine("Deletion would remove all data rows; operation aborted.");
            return;
        }

        table.DeleteRows(startRow, rowsToDelete);
        Console.WriteLine($"{rowsToDelete} rows removed starting at index {startRow}.");

        // ----- Step 4: Change table name -----
        string newTableName = "SalesData2026";

        bool nameExists = workbook.Worksheets.GetDefinedNames()
                               .Any(d => d.Text.Equals(newTableName, StringComparison.OrdinalIgnoreCase));

        if (nameExists)
        {
            Console.WriteLine($"The name '{newTableName}' already exists. Choose a different name.");
            return;
        }

        table.Name = newTableName;
        Console.WriteLine($"Table renamed to '{newTableName}'.");

        // ----- Step 5: Save workbook -----
        string outputPath = @"C:\Data\ModifiedTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to '{outputPath}'.");
    }
}
```

**Output yang diharapkan** (asumsi file dan tabel ada):

```
2 rows removed starting at index 1.
Table renamed to 'SalesData2026'.
Modified workbook saved to 'C:\Data\ModifiedTable.xlsx'.
```

Menjalankan program memperbarui file Excel persis seperti yang dijelaskan: baris dihapus, nama tabel berubah, dan hasil disimpan tanpa penyuntingan manual.

## Pertanyaan umum dan pemecahan masalah

| Pertanyaan | Jawaban |
|----------|--------|
| *Apa yang terjadi jika tabel mencakup sel yang digabung?* | `DeleteRows` menghormati rentang yang digabung. Jika sel yang digabung melintasi batas penghapusan, Aspose.Cells secara otomatis menyesuaikan penggabungan. Verifikasi hasil secara visual jika Anda mengandalkan penggabungan yang kompleks. |
| *Bisakah saya menghapus baris dari tabel yang merupakan bagian dari cache pivot?* | Menghapus baris dari tabel sumber yang memberi data ke tabel pivot **tidak** secara otomatis menyegarkan cache pivot. Panggil `pivotTable.RefreshData()` setelah memodifikasi tabel sumber. |
| *Apakah memungkinkan menghapus baris berdasarkan kondisi (misalnya, nilai < 0)?* | Ya. Iterasi melalui `table.ListObjects` atau `table.Rows` untuk menemukan baris yang cocok, kemudian kumpulkan indeksnya dan panggil `DeleteRows` untuk setiap rentang. |
| *Apakah saya perlu membuang (dispose) objek `Workbook`?* | `Workbook` mengimplementasikan `IDisposable`. Bungkus dalam blok `using` untuk pelepasan sumber daya yang deterministik, terutama saat memproses file besar. |
| *Bagaimana perbedaannya dengan menggunakan EPPlus?* | EPPlus juga mendukung manipulasi tabel tetapi menggunakan API yang berbeda (`ExcelTable`). Konsep memuat workbook, menghapus baris, dan mengganti nama tabel serupa. Pilih perpustakaan yang sesuai dengan persyaratan lisensi Anda. |

## Praktik terbaik saat memodifikasi tabel Excel di C#

* **Validasi indeks** – Indeks baris tabel berbasis nol; kesalahan off‑by‑one dapat menyebabkan penghapusan yang tidak diharapkan.
* **Periksa benturan nama** – Excel tidak mengizinkan nama yang didefinisikan duplikat; selalu verifikasi keunikan sebelum menetapkan nama baru.
* **Cadangkan file asli** – Skrip otomatis dapat merusak data; simpan salinan workbook sumber.
* **Gunakan pernyataan `using`** – Menjamin bahwa handle file dilepaskan dengan cepat:

```csharp
using (Workbook wb = new Workbook(inputPath))
{
    // modify workbook
}
```

* **Uji dengan kasus tepi** – Tabel dengan satu baris data, tabel yang mencakup seluruh lembar kerja, dan tabel yang terhubung ke diagram harus diverifikasi setelah perubahan.

## Kesimpulan

Anda kini tahu cara **menghapus baris dari tabel Excel** dan **mengubah nama tabel Excel** menggunakan C#. Solusi lengkap memuat workbook, mengakses tabel target, menghapus baris yang diinginkan, mengganti nama tabel, dan menyimpan hasilnya. Terapkan teknik ini untuk mengotomatisasi pembuatan laporan, pembersihan data, atau alur kerja apa pun yang memerlukan manajemen tabel Excel secara programatis.

Selanjutnya, jelajahi topik terkait seperti **memperbarui nilai sel dalam tabel Excel**, **menambahkan baris baru secara programatis**, dan **mengekspor data tabel ke CSV**. Menguasai operasi ini akan memberi Anda kontrol penuh atas file Excel dari dalam aplikasi C# Anda.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode kerja lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengganti Nama Tabel di Excel dengan C# – Panduan Langkah‑per‑Langkah](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [Membuat Tabel Excel di C# – Panduan Langkah‑per‑Langkah](/cells/english/net/tables-and-lists/create-excel-table-in-c-step-by-step-guide/)
- [Mendapatkan Tabel Pertama dari Workbook Excel di C# – Panduan Lengkap](/cells/english/net/excel-autofilter-validation/get-first-table-from-excel-workbook-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}