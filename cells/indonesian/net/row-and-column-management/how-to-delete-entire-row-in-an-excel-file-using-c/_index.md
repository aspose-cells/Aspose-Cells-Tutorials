---
category: general
date: 2026-10-10
description: Pelajari cara menghapus seluruh baris dalam buku kerja Excel dengan C#.
  Panduan langkah demi langkah ini juga mencakup cara menghapus baris berdasarkan
  indeks dan menghapus baris berdasarkan indeks menggunakan Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: id
lastmod: 2026-10-10
og_description: Hapus seluruh baris dalam buku kerja Excel menggunakan C#. Ikuti panduan
  ini untuk mempelajari cara menghapus baris berdasarkan indeks, menghilangkan baris
  berdasarkan indeks, dan menyimpan file dengan aman.
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: Hapus seluruh baris di Excel dengan C# – panduan pemrograman lengkap
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Cara menghapus seluruh baris dalam file Excel menggunakan C#
url: /id/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hapus seluruh baris dalam file Excel menggunakan C#

Jika Anda perlu **delete entire row** dalam sebuah workbook Excel, panduan ini menunjukkan secara tepat cara melakukannya dengan C#. Baik Anda sedang membersihkan data yang diimpor atau membangun alat pelaporan, langkah‑langkah di bawah ini memungkinkan Anda menghapus baris berdasarkan indeksnya dan menyimpan hasilnya tanpa kehilangan data lain.

Anda juga akan melihat bagaimana pendekatan yang sama menjawab pertanyaan **how to delete row** berdasarkan indeks, bagaimana **remove row by index**, dan mengapa ini bekerja untuk skenario **delete row excel** di C#.

## Prasyarat

* .NET 6.0 atau lebih baru (kode ini juga bekerja dengan .NET Framework 4.6+).  
* Library **Aspose.Cells for .NET** (tersedia melalui NuGet: `Install-Package Aspose.Cells`)  
* Familiaritas dasar dengan proyek konsol atau desktop C#  

Tidak ada komponen Excel interop atau COM tambahan yang diperlukan, sehingga solusi tetap ringan dan aman untuk eksekusi di sisi server.

## Langkah 1: Siapkan proyek dan impor namespace

Buat aplikasi konsol baru (atau tambahkan kode ke proyek yang sudah ada) dan tambahkan direktif `using` yang diperlukan:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*Mengapa ini penting*: Mengimpor `Aspose.Cells` memberi Anda akses ke `Workbook`, `Worksheet`, dan metode `DeleteRows` yang melakukan penghapusan baris secara aktual.

## Langkah 2: Muat workbook dan pilih worksheet

Anda harus memuat file sumber (`input.xlsx`) dan memperoleh worksheet yang ingin Anda modifikasi. Worksheet pertama diakses dengan indeks `0`.

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **Tip**: Jika Anda perlu bekerja dengan lembar tertentu, ganti indeks dengan nama lembar: `workbook.Worksheets["Data"]`.

## Langkah 3: Hapus seluruh baris berdasarkan indeks berbasis nol

Aspose.Cells menggunakan indeks berbasis nol, sehingga baris pertama adalah `0`. Untuk menghapus baris 5 (baris visual keenam), panggil `DeleteRows` dengan `DeleteOptions.DeleteEntireRow`.

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*Penjelasan*:

* `ws.Cells[5, 0]` menunjuk ke sel pertama dari baris yang ingin Anda hapus.  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` memberi tahu Aspose.Cells untuk menghapus **1** baris, dan flag `DeleteEntireRow` memastikan **seluruh baris** hilang, menggeser baris di bawahnya ke atas.

### Cara menghapus baris berdasarkan indeks dalam skenario lain

* **Delete multiple consecutive rows** – ubah argumen pertama menjadi jumlah baris yang ingin Anda hapus:

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **Delete the last row** – gunakan `ws.Cells.MaxDataRow` untuk mendapatkan indeks baris terisi terbawah:

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

Potongan kode ini menjawab kebutuhan **remove row by index** sambil menjaga kode tetap mudah dibaca.

## Langkah 4: Simpan workbook dengan baris yang dihapus

Setelah penghapusan, tulis kembali workbook yang telah dimodifikasi ke disk. Anda dapat menimpa file asli atau membuat file baru.

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Jika Anda perlu menjaga file asli tetap tidak berubah, cukup ubah jalur output. Metode `Save` mendukung banyak format (`.xls`, `.csv`, `.pdf`, dll.) – cukup ubah ekstensi file.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua, berikut adalah program lengkap yang siap dijalankan:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**Output yang diharapkan**: Setelah menjalankan program, `output.xlsx` akan berisi semua baris asli kecuali yang dimulai pada baris visual 6. Semua data di bawah baris yang dihapus akan otomatis naik, mempertahankan formula dan format.

## Kesalahan umum dan cara menghindarinya

| Masalah | Mengapa terjadi | Solusi |
|-------|----------------|-----|
| **Indeks di luar jangkauan** | Mencoba menghapus indeks baris yang tidak ada (misalnya `ws.Cells[1000,0]` pada lembar dengan 200 baris) | Gunakan `ws.Cells.MaxDataRow` untuk memverifikasi indeks valid tertinggi sebelum memanggil `DeleteRows`. |
| **Penghapusan baris parsial** | Menghilangkan `DeleteOptions.DeleteEntireRow` menyebabkan hanya isi sel yang dibersihkan | Selalu berikan `DeleteOptions.DeleteEntireRow` ketika Anda membutuhkan seluruh baris dihapus. |
| **Perubahan formula yang tidak terduga** | Menghapus baris yang merupakan bagian dari rentang formula dapat memutus referensi | Hitung ulang formula setelah penghapusan (`workbook.CalculateFormula()`) jika workbook Anda bergantung pada rentang dinamis. |
| **Menyimpan ke lokasi baca‑saja** | Pemanggilan `Save` melempar pengecualian jika folder dilindungi | Pastikan direktori target dapat ditulisi atau jalankan program dengan izin yang sesuai. |

Menangani masalah‑masalah ini membuat solusi menjadi kuat untuk penggunaan produksi dan memenuhi kueri **delete row excel** serta **delete row c#**.

## Lanjutan: Menghapus baris berdasarkan kondisi

Terkadang Anda perlu menghapus baris yang memenuhi kriteria tertentu (mis., baris di mana kolom A kosong). Loop berikut menunjukkan cara aman untuk memindai dari bawah ke atas dan menghapus baris yang cocok:

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

Pemindaian ke atas mencegah masalah pergeseran indeks yang terjadi saat menghapus baris sambil iterasi maju.

## Kesimpulan

Anda kini tahu cara **delete entire row** dalam workbook Excel menggunakan C#. Panduan ini mencakup:

* Memuat workbook dan memilih worksheet  
* Menggunakan `DeleteRows` dengan `DeleteOptions.DeleteEntireRow` untuk **how to delete row** berdasarkan indeks  
* Menyimpan file yang telah dimodifikasi dengan aman  
* Penanganan kasus tepi, tips kinerja, dan contoh penghapusan bersyarat  

Dengan pengetahuan ini Anda dapat dengan percaya diri mengimplementasikan fungsionalitas **remove row by index**, mengotomatiskan pembersihan data, dan mengintegrasikan manipulasi Excel ke dalam aplikasi C# apa pun.  

**Langkah selanjutnya**: jelajahi fitur Aspose.Cells lainnya seperti menyisipkan baris, menyalin rentang, atau mengonversi workbook ke PDF—semuanya dibangun di atas objek `Workbook` dan `Worksheet` yang baru saja Anda kuasai. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang dibangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menghapus Baris Excel Menggunakan Aspose.Cells .NET: Panduan Komprehensif](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells Delete Rows – Lindungi Baris Header di Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Manajemen Baris Efisien di Excel menggunakan Aspose.Cells untuk Java: Menyisipkan dan Menghapus Baris](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}