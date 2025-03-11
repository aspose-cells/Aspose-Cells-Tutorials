---
title: Menerapkan Rumus Sel Lokal Mirip dengan Rumus Rentang Lokal
linktitle: Menerapkan Rumus Sel Lokal Mirip dengan Rumus Rentang Lokal
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Temukan cara menerapkan rumus sel yang mirip dengan fungsi lokal rumus rentang di Aspose.Cells untuk .NET. Pelajari cara menyesuaikan nama fungsi Excel bawaan dan banyak lagi.
weight: 13
url: /id/net/workbook-settings/implement-cell-formula-local-similar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menerapkan Rumus Sel Lokal Mirip dengan Rumus Rentang Lokal

## Perkenalan
Aspose.Cells untuk .NET adalah API manipulasi spreadsheet yang kuat dan fleksibel yang memungkinkan Anda membuat, memanipulasi, dan mengonversi file Excel secara terprogram. Salah satu dari banyak fitur yang ditawarkan oleh Aspose.Cells adalah kemampuan untuk menyesuaikan perilaku fungsi Excel bawaan, termasuk kemampuan untuk membuat nama fungsi lokal Anda sendiri. Dalam tutorial ini, kami akan memandu Anda melalui langkah-langkah untuk mengimplementasikan rumus sel yang mirip dengan fungsi lokal rumus rentang di Aspose.Cells untuk .NET.
## Prasyarat
Sebelum memulai, pastikan Anda memiliki hal berikut:
1. Microsoft Visual Studio 2010 atau yang lebih baru terinstal di sistem Anda.
2.  Versi terbaru dari pustaka Aspose.Cells for .NET yang terpasang di proyek Anda. Anda dapat mengunduh pustaka dari[Halaman unduhan Aspose.Cells untuk .NET](https://releases.aspose.com/cells/net/).
## Paket Impor
Untuk memulai, Anda perlu mengimpor paket yang diperlukan ke dalam proyek C# Anda. Tambahkan pernyataan berikut di bagian atas berkas kode Anda:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Langkah 1: Buat Kelas Pengaturan Globalisasi Kustom
 Langkah pertama adalah membuat custom`GlobalizationSettings`kelas yang akan memungkinkan Anda untuk mengganti perilaku default fungsi Excel. Dalam contoh ini, kita akan mengubah nama-nama`SUM` Dan`AVERAGE` fungsi untuk`UserFormulaLocal_SUM` Dan`UserFormulaLocal_AVERAGE`, masing-masing.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Ubah nama fungsi SUM sesuai kebutuhan Anda.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Ubah nama fungsi AVERAGE sesuai kebutuhan Anda.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Langkah 2: Buat Buku Kerja Baru dan Tetapkan Pengaturan Globalisasi Kustom
 Selanjutnya, buat instance Workbook baru dan tetapkan kustom`GlobalizationSettings` implementasi kelas ke Buku Kerja`Settings.GlobalizationSettings` milik.
```csharp
//Buat buku kerja
Workbook wb = new Workbook();
//Tetapkan kelas implementasi GlobalizationSettings
wb.Settings.GlobalizationSettings = new GS();
```
## Langkah 3: Akses Lembar Kerja Pertama dan Sel
Sekarang, mari mengakses lembar kerja pertama dalam buku kerja dan sel tertentu dalam lembar kerja tersebut.
```csharp
//Akses lembar kerja pertama
Worksheet ws = wb.Worksheets[0];
//Akses beberapa sel
Cell cell = ws.Cells["C4"];
```
## Langkah 4: Tetapkan Rumus dan Cetak RumusLokal
 Terakhir, mari kita tetapkan`SUM` Dan`AVERAGE` rumus ke dalam sel dan mencetak hasilnya`FormulaLocal` nilai-nilai.
```csharp
//Tetapkan rumus SUM dan cetak FormulaLocal-nya
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Tetapkan rumus AVERAGE dan cetak FormulaLocal-nya
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Kesimpulan
Dalam tutorial ini, Anda telah mempelajari cara menerapkan rumus sel yang mirip dengan fungsi lokal rumus rentang di Aspose.Cells untuk .NET. Dengan membuat sel khusus`GlobalizationSettings` kelas, Anda dapat mengganti perilaku default fungsi Excel dan menyesuaikan nama fungsi lokal agar sesuai dengan kebutuhan Anda. Ini dapat sangat berguna saat bekerja dengan dokumen Excel yang dilokalkan atau diinternasionalkan.
## Pertanyaan yang Sering Diajukan
###  Apa tujuan dari`GlobalizationSettings` class in Aspose.Cells?
 Itu`GlobalizationSettings` kelas di Aspose.Cells memungkinkan Anda menyesuaikan perilaku fungsi Excel bawaan, termasuk kemampuan untuk mengubah nama fungsi lokal.
###  Bisakah saya mengesampingkan perilaku fungsi selain`SUM` and `AVERAGE`?
 Ya, Anda dapat mengesampingkan perilaku fungsi Excel bawaan apa pun dengan memodifikasi`GetLocalFunctionName` metode dalam kebiasaan Anda`GlobalizationSettings` kelas.
### Apakah ada cara untuk mengatur ulang nama fungsi kembali ke nilai default?
 Ya, Anda dapat mengatur ulang nama fungsi dengan menghapus nama kustom`GlobalizationSettings` kelas atau dengan mengembalikan string kosong dari`GetLocalFunctionName` metode.
### Dapatkah saya menggunakan fitur ini untuk membuat fungsi khusus di Aspose.Cells?
 Tidak,`GlobalizationSettings`kelas dirancang untuk mengesampingkan perilaku fungsi Excel bawaan, bukan untuk membuat fungsi kustom. Jika Anda perlu membuat fungsi kustom, Anda dapat menggunakan`UserDefinedFunction` kelas di Aspose.Cells.
### Apakah fitur ini tersedia di semua versi Aspose.Cells untuk .NET?
 Ya, itu`GlobalizationSettings` kelas dan kemampuan untuk menyesuaikan nama fungsi tersedia di semua versi Aspose.Cells untuk .NET.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
