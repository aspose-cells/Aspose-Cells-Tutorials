---
title: Mengatur Format Bidang Halaman Secara Terprogram di .NET
linktitle: Mengatur Format Bidang Halaman Secara Terprogram di .NET
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengatur format bidang halaman di PivotTable secara terprogram menggunakan Aspose.Cells untuk .NET. Ikuti tutorial langkah demi langkah kami untuk manajemen data yang lancar.
weight: 21
url: /id/net/creating-and-configuring-pivot-tables/setting-page-field-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengatur Format Bidang Halaman Secara Terprogram di .NET

## Perkenalan
Membuat dan memanipulasi file Excel melalui kode bisa sangat memberdayakan, terutama saat Anda perlu menganalisis kumpulan data besar. Salah satu alat hebat dalam gudang senjata Anda adalah Aspose.Cells for .NET, yang memungkinkan Anda berinteraksi secara terprogram dengan file Excel dan membuat struktur pelaporan yang kompleks. Dalam tutorial ini, kita akan mempelajari cara menyiapkan format bidang halaman dalam PivotTable menggunakan pustaka yang hebat ini. Baik Anda pengembang berpengalaman atau pemula, di akhir panduan ini, Anda akan memiliki pemahaman yang kuat tentang cara mengoperasikan PivotTable dan berbagai pengaturannya di .NET.
## Prasyarat
Sebelum kita mulai membuat kode, pastikan Anda telah menyiapkan semuanya dengan benar. Anda memerlukan hal berikut:
- Visual Studio: Lingkungan kerja tempat Anda dapat menulis dan mengeksekusi kode .NET Anda.
-  Aspose.Cells: Anda dapat mengunduh pustaka[Di Sini](https://releases.aspose.com/cells/net/).
- Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan membantu Anda memahami potongan kode dengan lebih baik.
-  File Excel: Siapkan file Excel (seperti`Book1.xls`) berisi data yang cocok untuk pembuatan PivotTable. 
 Jika Anda belum melakukannya, dapatkan uji coba gratis Aspose.Cells Anda[Di Sini](https://releases.aspose.com/).
## Paket Impor
Untuk memulai, Anda perlu mengimpor paket yang tepat ke dalam proyek Anda. Mulailah dengan menambahkan referensi ke pustaka Aspose.Cells di proyek C# Anda. Berikut cara melakukannya:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Ini akan menarik semua kelas dan metode yang diperlukan untuk memanipulasi file Excel menggunakan Aspose.Cells.
## Langkah 1: Siapkan Ruang Kerja Anda
Mulailah dengan menentukan direktori kerja tempat file Excel akan disimpan. Misalnya, Anda dapat mendeklarasikan variabel seperti ini:
```csharp
string dataDir = "Your Document Directory";
```
## Memuat Buku Kerja
Berikutnya, kita perlu memuat templat Excel kita. Ini adalah langkah penting karena ini menetapkan konteks untuk operasi kita:
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Baris ini memuat buku kerja yang ada dari direktori yang ditentukan.
## Langkah 2: Akses Lembar Kerja
Setelah buku kerja Anda dimuat, saatnya mengakses lembar kerja yang berisi PivotTable atau data yang ingin Anda analisis. Berikut cara melakukannya:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Ini akan mengambil lembar kerja pertama dari buku kerja yang dimuat. Anda dapat dengan mudah mengubah indeks jika Anda bekerja dengan beberapa lembar.
## Langkah 3: Mengakses PivotTable
 Melanjutkan, mari kita akses PivotTable di lembar kerja pilihan kita. Jika Anda menggunakan satu PivotTable, Anda dapat mengatur indeksnya menjadi`0`:
```csharp
int pivotindex = 0;
// Mengakses PivotTable
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
Potongan kode ini memilih PivotTable pertama dalam lembar kerja. 
## Langkah 4: Mengonfigurasi PivotTable
Sekarang tibalah bagian yang menarik! Mari kita atur PivotTable untuk menampilkan total keseluruhan untuk baris-baris:
```csharp
pivotTable.RowGrand = true;
```
Baris ini memastikan bahwa laporan Anda akan menampilkan total keseluruhan yang dapat menjadi ringkasan yang berguna untuk analisis data.
## Langkah 5: Akses dan Konfigurasikan Bidang Baris
Berikutnya, kita perlu mengakses bidang baris PivotTable:
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.RowFields;
```
Koleksi ini memungkinkan kita memanipulasi bidang sesuai kebutuhan.
## Konfigurasikan Bidang Baris Pertama
Ingin menetapkan tipe subtotal tertentu? Mari akses kolom pertama dalam koleksi kita dan konfigurasikan:
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
// Menetapkan Subtotal.
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
 Dengan mengaktifkan`Sum` Dan`Count` subtotal, kita dapat dengan cepat meringkas data dalam laporan kita.
## Langkah 6: Mengatur Opsi Penyortiran Otomatis
Selanjutnya, mari kita terapkan pengurutan cerdas. Dengan cara ini, PivotTable Anda akan menyusun data dalam urutan yang tepat:
```csharp
// Mengatur opsi sortir otomatis.
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; // Menggunakan bidang penyortiran yang telah ditentukan sebelumnya.
```
Cuplikan kode ini memungkinkan penyortiran otomatis dan menentukan urutan menaik. 
## Langkah 7: Mengatur Opsi AutoShow
Apakah Anda ingin memfilter data Anda lebih lanjut? Opsi AutoShow berguna untuk menampilkan titik data tertentu dalam kondisi yang ditentukan:
```csharp
// Mengatur opsi autoShow.
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; // Tentukan bidang yang akan ditampilkan otomatis.
```
Ini memastikan bahwa PivotTable Anda hanya menampilkan data yang relevan, meningkatkan kejelasan dan fokus.
## Langkah 8: Menyimpan Pekerjaan Anda
Setelah semua konfigurasi tersebut, Anda tentu tidak ingin kehilangan pekerjaan Anda! Simpan buku kerja yang dimodifikasi seperti ini:
```csharp
workbook.Save(dataDir + "output.xls");
```
Sekarang, Anda dapat menemukan file Excel yang baru dibuat di direktori dokumen Anda.
## Kesimpulan
Nah, itu dia! Kami telah membahas pendekatan yang komprehensif dan praktis untuk menetapkan format bidang halaman secara terprogram dalam PivotTable menggunakan Aspose.Cells untuk .NET. Dengan langkah-langkah sederhana yang disediakan, Anda akan merasa yakin dalam memodifikasi data Excel Anda agar sesuai dengan kebutuhan pelaporan Anda. Sungguh luar biasa apa yang dapat Anda capai saat menggabungkan kekuatan C# dengan Aspose.Cells.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET yang memungkinkan pengembang untuk membuat, memanipulasi, dan mengonversi file Excel secara terprogram.
### Bagaimana cara menginstal Aspose.Cells?
 Anda dapat mengunduhnya langsung dari[Situs web Aspose](https://releases.aspose.com/cells/net/).
### Bisakah saya menggunakan Aspose.Cells tanpa instalasi Excel?
Ya, Aspose.Cells adalah pustaka mandiri yang tidak memerlukan penginstalan Microsoft Excel.
### Di mana saya dapat menemukan dukungan terperinci?
 Anda dapat mengakses dukungan dan forum terperinci di[Dukungan Aspose](https://forum.aspose.com/c/cells/9).
### Bagaimana saya bisa mendapatkan lisensi sementara?
 Anda dapat memperoleh lisensi sementara dari[Di Sini](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
