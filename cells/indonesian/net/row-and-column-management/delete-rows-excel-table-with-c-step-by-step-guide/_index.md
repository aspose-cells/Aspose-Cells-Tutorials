---
category: general
date: 2026-02-28
description: Hapus baris tabel Excel di C# dengan cepat. Pelajari cara menambahkan
  named range di Excel, mengakses worksheet berdasarkan nama, dan menghindari kesalahan
  nama duplikat.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: id
og_description: Hapus baris tabel Excel menggunakan C#. Tutorial ini juga menunjukkan
  cara menambahkan rentang bernama di Excel dan mengakses lembar kerja berdasarkan
  nama.
og_title: Menghapus Baris Tabel Excel dengan C# – Panduan Lengkap
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: Menghapus Baris Tabel Excel dengan C# – Panduan Langkah demi Langkah
url: /id/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hapus Baris Tabel Excel dengan C# – Tutorial Pemrograman Lengkap

Pernah perlu **delete rows excel table** dari sebuah workbook tetapi tidak yakin panggilan API mana yang harus digunakan? Anda bukan satu-satunya—banyak pengembang mengalami hal yang sama saat pertama kali mencoba memangkas tabel secara programatis.  

Dalam panduan ini kami akan menelusuri contoh lengkap yang dapat dijalankan, yang tidak hanya menghapus baris dari tabel Excel, tetapi juga menunjukkan **how to add defined name** (alias *named range*), cara **access worksheet by name**, dan mengapa menambahkan nama duplikat pada lembar lain melemparkan `InvalidOperationException`.  

Pada akhir artikel Anda akan dapat:

* Mengambil lembar kerja menggunakan nama tabnya.  
* Menghapus baris data dengan aman dari tabel pertama pada lembar tersebut.  
* Membuat named range yang menunjuk ke alamat tertentu.  
* Memahami jebakan nama duplikat di seluruh lembar.

Tidak diperlukan dokumentasi eksternal—semua yang Anda butuhkan ada di sini.

---

## Apa yang Anda Butuhkan

* **DevExpress Spreadsheet** (atau perpustakaan apa pun yang menyediakan objek `Workbook`, `Worksheet`, `ListObject`, dan `Names`).  
* Proyek .NET yang menargetkan **.NET 6** atau lebih baru (kode juga dapat dikompilasi dengan .NET Framework 4.8).  
* Familiaritas dasar dengan C#—jika Anda dapat menulis loop `foreach`, Anda sudah siap.

> **Pro tip:** Jika Anda menggunakan Community Edition gratis dari DevExpress, API yang digunakan di bawah ini identik dengan versi komersial.

---

## Langkah 1 – Access Worksheet by Name

Hal pertama yang harus Anda lakukan adalah menemukan lembar yang berisi tabel yang ingin Anda modifikasi.  
Sebagian besar pengembang langsung menggunakan `Worksheets[0]` karena kebiasaan, tetapi cara itu mengikat kode Anda pada urutan lembar dan akan rusak begitu seseorang mengganti nama tab.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Mengapa ini penting:* Dengan menggunakan **nama** lembar alih-alih indeks, Anda menghindari pengeditan tidak sengaja pada lembar yang salah ketika workbook berubah.  

Jika nama yang Anda berikan tidak ada, perpustakaan akan melempar `KeyNotFoundException`, yang dapat Anda tangkap untuk menampilkan pesan error yang ramah.

---

## Langkah 2 – Delete Rows Excel Table (The Safe Way)

Setelah Anda memiliki lembar kerja yang tepat, mari hapus baris data dari tabel pertama.  
Kesalahan umum adalah memanggil `DeleteRows(1, rowCount‑1)`. Sejak **DevExpress 22.2** overload tersebut **dilarang** dan akan melempar `InvalidOperationException`. Perpustakaan mengharapkan Anda menghapus baris **di dalam rentang data tabel**, bukan baris header.

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **Bagaimana jika tabel kosong?** Guard `if` mencegah pemanggilan dengan `rowCount = 0`, yang sebaliknya akan menimbulkan pengecualian.

### Gambaran Visual  

![contoh menghapus baris tabel excel](image.png "Tangkapan layar yang menunjukkan baris dihapus dari sebuah tabel Excel")  

*Alt text: contoh menghapus baris tabel excel dalam kode C#*

---

## Langkah 3 – How to Add Defined Name (Create a Named Range)

Setelah membersihkan tabel, Anda mungkin ingin merujuk ke rentang tertentu nanti—misalnya untuk diagram atau daftar validasi data. Di sinilah **add named range excel** berperan.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

Metode `Names.Add` menerima dua parameter: pengenal dan alamat bergaya A1.  
Karena kami telah **access worksheet by name** sebelumnya, string alamat dapat dengan aman merujuk ke lembar mana pun tanpa khawatir tentang perubahan indeks.

---

## Langkah 4 – Named Range pada Lembar Lain – Hindari Kesalahan Nama Duplikat

Anda mungkin berpikir dapat menggunakan kembali pengenal yang sama pada lembar berbeda, seperti ini:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

Sayangnya, ruang lingkup penamaan Excel bersifat **seluruh workbook**, bukan per‑lembar. Pemanggilan di atas memicu `InvalidOperationException` dengan pesan *“A name with the same identifier already exists.”*  

### Cara Mengatasinya

1. **Pilih nama yang unik** (`MyTable_Sheet2`).  
2. **Hapus nama yang sudah ada** sebelum menambahkannya kembali (hanya jika Anda benar‑benar ingin menggantinya).  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## Contoh Lengkap yang Dapat Dijalankan

Menggabungkan semuanya, berikut adalah aplikasi konsol mandiri yang dapat Anda masukkan ke Visual Studio dan jalankan terhadap file contoh `sample.xlsx`.

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**Hasil yang diharapkan**

* Semua baris data dari tabel pertama pada **Sheet1** menghilang, menyisakan hanya baris header.  
* Nama **MyTable** kini menunjuk ke `Sheet1!$A$1:$C$5`.  
* Nama kedua **MyTable_Sheet2** dengan aman merujuk ke rentang pada **Sheet2** tanpa melempar pengecualian.

---

## Pertanyaan Umum & Kasus Edge

| Pertanyaan | Jawaban |
|------------|---------|
| *Bagaimana jika workbook memiliki beberapa tabel?* | Ambil `ListObject` yang tepat dengan indeks (`worksheet.ListObjects[1]`) atau dengan nama (`worksheet.ListObjects["MyTable"]`). |
| *Bisakah saya menghapus baris dari tabel yang melintasi beberapa lembar?* | Tidak—tabel terbatas pada satu lembar. Anda harus mengulangi logika penghapusan untuk setiap lembar. |
| *Apakah ada cara menghapus hanya sebagian baris?* | Ya—gunakan `table.DeleteRows(startRow, count)` dimana `startRow` berbasiskan nol di dalam area data tabel. |
| *Apakah named range tetap ada setelah disimpan?* | Tentu saja. Setelah Anda memanggil `SaveDocument`, nama‑nama tersebut menjadi bagian dari XML workbook. |
| *Bagaimana cara menampilkan semua defined name di workbook?* | Iterasi `foreach (var name in workbook.Names) Console.WriteLine(name.Name);`. |

---

## Kesimpulan

Kami telah membahas **delete rows excel table** menggunakan C#, mendemonstrasikan **add named range excel**, dan menunjukkan cara yang tepat untuk **access worksheet by name** sambil menghindari pengecualian nama duplikat yang menakutkan.  

Solusi lengkap berada di potongan kode di atas—salin, tempel, dan jalankan terhadap file Anda sendiri. Dari sini Anda dapat memperluas logika untuk menangani banyak tabel, perhitungan rentang dinamis, atau bahkan mengintegrasikannya dengan UI.

**Langkah selanjutnya** yang dapat Anda jelajahi:

* Gunakan **named range pada lembar lain** untuk menggerakkan seri diagram.  
* Gabungkan logika penghapusan dengan **ExcelDataReader** untuk mengimpor data sebelum dibersihkan.  
* Otomatiskan pembaruan massal pada puluhan workbook menggunakan loop sederhana `foreach (var file in Directory.GetFiles(...))`.

Punya pertanyaan lebih lanjut tentang otomatisasi Excel di C#? Tinggalkan komentar, dan mari teruskan diskusi. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}