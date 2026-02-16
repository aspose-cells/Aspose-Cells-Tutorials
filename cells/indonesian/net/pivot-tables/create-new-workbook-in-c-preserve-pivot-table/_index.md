---
category: general
date: 2026-02-15
description: Buat buku kerja baru di C# dan salin tabel pivot tanpa kehilangan definisinya.
  Pelajari cara menyalin baris, mempertahankan tabel pivot, dan menggandakan tabel
  pivot dengan mudah.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: id
og_description: Buat workbook baru di C# dan salin tabel pivot sambil mempertahankan
  definisinya. Panduan langkah demi langkah untuk pengembang.
og_title: Buat Workbook Baru di C# – Pertahankan Tabel Pivot
tags:
- Aspose.Cells
- C#
- Excel automation
title: Buat Workbook Baru di C# – Pertahankan Tabel Pivot
url: /id/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Workbook Baru di C# – Pertahankan Pivot Table

Pernahkah Anda perlu **create new workbook** di C# yang berisi salinan persis dari pivot table dari file lain? Anda bukan satu-satunya. Dalam banyak pipeline pelaporan, pivot table adalah inti analisis, dan kehilangan definisinya saat Anda memindahkan data adalah mimpi buruk.

Berita baiknya? Dengan beberapa baris kode Aspose.Cells, Anda dapat menyalin baris—termasuk pivot table—ke dalam workbook baru dan menjaga semuanya tetap utuh. Di bawah ini Anda akan melihat **how to copy rows**, **preserve pivot table** settings, dan bahkan **duplicate pivot table** antar file tanpa merusak formula atau cache.

## Apa yang Dibahas dalam Tutorial Ini

1. Memuat workbook sumber yang sudah memiliki pivot table.  
2. **Create new workbook** objek untuk tujuan.  
3. Menggunakan `CopyRows` untuk mentransfer rentang yang berisi pivot table.  
4. Menyimpan hasil sambil memastikan pivot table tetap berfungsi.  

Tidak memerlukan dokumentasi eksternal—hanya kode, penjelasannya, dan beberapa tips praktis yang dapat Anda tempel langsung ke dalam proyek Anda.

> **Pro tip:** Aspose.Cells bekerja dengan .NET Core, .NET Framework, dan bahkan Xamarin, sehingga potongan kode yang sama dapat dijalankan di mana pun Anda membutuhkannya.

![Buat workbook baru dengan pivot table yang disalin](/images/create-new-workbook-pivot.png "buat workbook baru dengan pivot table yang disalin")

## Langkah 1 – Buat Workbook Baru dan Muat File Sumber

Hal pertama yang kami lakukan adalah membuat objek **create new workbook**. Satu menyimpan data asli, yang lainnya akan menerima rentang yang disalin.

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*Mengapa ini penting:*  
`Workbook` adalah titik masuk untuk setiap manipulasi Excel di Aspose.Cells. Dengan menginstansiasi workbook baru, kami menjamin kanvas bersih—tanpa gaya tersembunyi atau lembar kerja yang mengganggu di kemudian hari.

## Langkah 2 – Cara Menyalin Baris Termasuk Pivot Table

Sekarang datang inti masalah: **how to copy rows** yang mencakup pivot table tanpa meratakannya. Metode `CopyRows` melakukan hal itu tepat.

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

Beberapa hal yang perlu dicatat:

* `startRow` dan `totalRows` menentukan blok yang berisi pivot table.  
* Metode ini menyalin **both** data mentah dan cache pivot, sehingga workbook tujuan tahu cara membangun kembali pivot table secara otomatis.  
* Jika pivot Anda mulai lebih dalam di lembar, cukup ubah indeks—tidak perlu panggilan API yang berbeda.

> **Common question:** *Apakah pivot yang disalin akan kehilangan referensi data sumbernya?*  
> Tidak. Aspose.Cells menyematkan cache langsung ke dalam worksheet, sehingga pivot menjadi mandiri dalam file baru.

## Langkah 3 – Pertahankan Pivot Table Saat Menyimpan Tujuan

Setelah baris disalin, pivot table berada di workbook tujuan persis seperti di sumber. Menyimpan file menjadi sederhana.

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

Saat Anda membuka `destination.xlsx` di Excel, Anda akan melihat pivot table siap untuk menyegarkan. Perilaku **preserve pivot table** otomatis karena cache ikut bersama baris.

### Memverifikasi Hasil

Buka file dan:

1. Klik pivot table.  
2. Perhatikan daftar bidang muncul—ini berarti cache tetap utuh.  
3. Coba segarkan; data diperbarui tanpa error.

Jika Anda menemukan error *#REF!*, periksa kembali bahwa rentang yang disalin mencakup baris cache tersembunyi (biasanya tepat setelah data yang terlihat).

## Langkah 4 – Duplikat Pivot Table ke Beberapa Workbook (Opsional)

Kadang Anda membutuhkan pivot yang sama di beberapa laporan. Pola yang baru saja kami gunakan dapat diskalakan dengan baik—cukup ulangi penyalinan untuk setiap workbook baru.

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

Potongan kode ini **duplicates pivot table** tiga kali dengan satu loop. Sesuaikan array `targets` agar cocok dengan jadwal pelaporan Anda.

### Kasus Pinggiran yang Perlu Diingat

| Situation | What to Watch For | Fix |
|-----------|-------------------|-----|
| Pivot menggunakan sumber data eksternal | Cache mungkin merujuk ke koneksi yang tidak ada di mesin baru | Sematkan sumber data atau buat ulang koneksi di workbook tujuan |
| Pivot sangat besar ( > 100 k baris ) | `CopyRows` dapat memakan banyak memori | Gunakan `CopyRows` dalam potongan atau pertimbangkan `Copy` dengan `PasteOptions` untuk membatasi penggunaan memori |
| Worksheet memiliki baris/kolom tersembunyi | Baris cache tersembunyi mungkin terlewat jika Anda menyalin hanya baris yang terlihat | Selalu salin rentang baris yang tepat yang berisi cache, bukan hanya area yang terlihat |

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program mandiri yang dapat Anda masukkan ke dalam aplikasi console.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

Jalankan program, buka `destination.xlsx`, dan Anda akan melihat pivot table yang sama siap untuk memotong dan mengolah data Anda. Tidak perlu membuat ulang secara manual.

---

## Kesimpulan

Kami baru saja menunjukkan cara **create new workbook** di C# dan **copy pivot table** sambil mempertahankan semua pengaturan. Dengan menggunakan `CopyRows` Anda mendapatkan cara andal untuk **preserve pivot table** fungsionalitas, menjawab pertanyaan lama “**how to copy rows**”, dan bahkan **duplicate pivot table** di beberapa laporan dengan kode minimal.

Langkah selanjutnya? Coba ubah rentang yang disalin untuk menyertakan grafik yang merujuk ke pivot yang sama, atau bereksperimen dengan `PasteOptions` untuk mempertahankan format secara tepat. Pola yang sama bekerja untuk objek Aspose.Cells lainnya seperti tabel dan named ranges, jadi silakan kembangkan.

Ada tantangan yang Anda hadapi—mungkin pivot yang mengambil data dari DB eksternal, atau workbook yang berada di cloud? Tinggalkan komentar di bawah, dan kami akan mengatasinya bersama. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}