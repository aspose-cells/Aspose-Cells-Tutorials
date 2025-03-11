---
title: Akses Label Objek OLE di Excel
linktitle: Akses Label Objek OLE di Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengakses dan mengubah label Objek OLE di Excel menggunakan Aspose.Cells untuk .NET. Panduan sederhana dengan contoh kode disertakan.
weight: 10
url: /id/net/excel-shape-label-access/access-ole-object-label-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Akses Label Objek OLE di Excel

## Perkenalan
Jika Anda pernah mencoba Excel, Anda tahu betapa hebat dan rumitnya Excel. Terkadang, Anda mungkin menemukan data yang tertanam dalam objek OLE (Object Linking and Embedding)—anggap saja sebagai 'jendela mini' ke perangkat lunak lain, seperti dokumen Word atau slide PowerPoint, yang semuanya tersimpan dengan nyaman di dalam lembar kerja Anda. Namun, bagaimana kita mengakses dan memanipulasi label ini dalam objek OLE kita menggunakan Aspose.Cells for .NET? Bersiaplah, karena dalam tutorial ini, kami akan menguraikannya langkah demi langkah!
## Prasyarat
 
Sebelum kita terjun ke dunia Aspose.Cells for .NET yang penuh aksi, berikut ini apa saja yang perlu Anda miliki dalam perangkat Anda:
1. Visual Studio Terpasang: Ini akan menjadi taman bermain Anda di mana Anda akan membuat kode dan menguji aplikasi C# Anda.
2. .NET Framework: Pastikan Anda menggunakan minimal .NET Framework 4.0 atau yang lebih tinggi. Ini akan memberi program kita fondasi yang diperlukan agar dapat bekerja dengan lancar.
3.  Pustaka Aspose.Cells: Anda memerlukan salinan pustaka Aspose.Cells. Anda dapat mengunduhnya dari[Di Sini](https://releases.aspose.com/cells/net/) Jika Anda ingin mencobanya sebelum melakukan pembelian, lihat[uji coba gratis](https://releases.aspose.com/).
4. Pemahaman Dasar C#: Keakraban dengan C# akan membantu Anda memahami kode dengan cepat.
Setelah itu, mari selami seluk-beluk mengakses dan memodifikasi label pada objek OLE!
## Paket Impor 
Untuk memulai, kita perlu mengimpor paket-paket yang diperlukan ke dalam proyek kita. Ini akan memudahkan kita dengan memberi kita akses ke semua fungsi dan kelas yang kita butuhkan. Berikut caranya:
### Buat Proyek C# Baru 
- Buka Visual Studio dan buat proyek Aplikasi Konsol C# baru.
- Beri nama seperti "OLEObjectLabelExample".
### Tambahkan Referensi Aspose.Cells 
- Klik kanan pada proyek Anda di Solution Explorer.
- Pilih "Kelola Paket NuGet".
- Cari "Aspose.Cells" dan instal pustakanya.
### Mengimpor Ruang Nama
 Di bagian atas file program Anda (misalnya,`Program.cs`), Anda perlu mengimpor namespace yang diperlukan:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Ruang nama ini akan membantu kita mengakses kelas dan metode yang dibutuhkan untuk manipulasi Excel kita.
Setelah semuanya siap, mari kita akses dan ubah label objek OLE yang tertanam dalam file Excel. Ikuti panduan langkah demi langkah di bawah ini:
## Langkah 1: Tetapkan Direktori Sumber
 Pertama, kita tentukan direktori tempat dokumen Excel Anda berada. Ganti`"Your Document Directory"` dengan jalur dokumen Anda yang sebenarnya.
```csharp
string sourceDir = "Your Document Directory";
```
## Langkah 2: Muat File Excel Sampel 
Berikutnya, kita akan memuat file Excel .xlsx yang berisi objek OLE kita:
```csharp
Workbook wb = new Workbook(sourceDir + "sampleAccessAndModifyLabelOfOleObject.xlsx");
```
 Baris ini menginisialisasi`Workbook` objek yang memberi kita akses ke semua lembar kerja dan komponen file Excel.
## Langkah 3: Akses Lembar Kerja Pertama
Sekarang, mari mengakses lembar kerja pertama di buku kerja kita:
```csharp
Worksheet ws = wb.Worksheets[0];
```
 Di Sini,`Worksheets[0]` adalah lembar kerja pertama dalam koleksi.
## Langkah 4: Akses Objek OLE Pertama 
Berikutnya, kita akan mengambil objek OLE pertama:
```csharp
Aspose.Cells.Drawing.OleObject oleObject = ws.OleObjects[0];
```
Ini akan memungkinkan kita berinteraksi dengan objek OLE yang ingin kita kerjakan.
## Langkah 5: Menampilkan Label Objek OLE
Sebelum kita mengubah label, mari kita cetak nilai saat ini:
```csharp
Console.WriteLine("Ole Object Label - Before: " + oleObject.Label);
```
Ini memberi kita pandangan yang jelas tentang label sebelum perubahan apa pun dibuat.
## Langkah 6: Ubah Labelnya 
Sekarang untuk bagian yang menyenangkan—mari kita ubah label objek OLE:
```csharp
oleObject.Label = "Aspose APIs";
```
Anda dapat mengaturnya sesuai keinginan Anda. “Aspose APIs” hanyalah cara yang bagus untuk menunjukkan apa yang sedang kita lakukan.
## Langkah 7: Simpan Buku Kerja ke Aliran Memori 
Kami kemudian akan menyimpan perubahan kami ke aliran memori sebelum memuat ulang buku kerja:
```csharp
MemoryStream ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
```
Ini menyimpan buku kerja kita yang dimodifikasi dalam memori, sehingga memudahkan akses nanti.
## Langkah 8: Atur Referensi Buku Kerja ke Null 
Untuk membersihkan memori, kita harus mengatur referensi buku kerja ke null:
```csharp
wb = null;
```
## Langkah 9: Muat Buku Kerja dari Aliran Memori 
Berikutnya, kita akan memuat ulang buku kerja kita dari aliran memori yang baru saja kita simpan:
```csharp
wb = new Workbook(ms);
```
## Langkah 10: Akses Lembar Kerja Pertama Lagi 
Sama seperti sebelumnya, kita perlu mengakses lembar kerja pertama lagi:
```csharp
ws = wb.Worksheets[0];
```
## Langkah 11: Akses Objek OLE Pertama Lagi
Sekarang, ambil kembali objek OLE untuk pemeriksaan akhir:
```csharp
oleObject = ws.OleObjects[0];
```
## Langkah 12: Menampilkan Label yang Dimodifikasi 
Untuk melihat apakah perubahan kita berlaku, mari cetak label baru:
```csharp
Console.WriteLine("Ole Object Label - After: " + oleObject.Label);
```
## Langkah 13: Konfirmasi Eksekusi 
Terakhir, berikan pesan sukses sehingga kami tahu semuanya berjalan sesuai rencana:
```csharp
Console.WriteLine("AccessAndModifyLabelOfOleObject executed successfully.");
```
## Kesimpulan 
Nah, itu dia! Anda telah berhasil mengakses dan mengubah label objek OLE di Excel menggunakan Aspose.Cells for .NET. Ini adalah cara yang bagus untuk menambahkan sentuhan pribadi ke dokumen tertanam Anda, meningkatkan kejelasan dan komunikasi dalam lembar kerja Anda. 
Baik Anda sedang mengembangkan aplikasi yang menarik atau sekadar mempercantik laporan, memanipulasi objek OLE dapat menjadi pengubah permainan. Terus jelajahi apa yang ditawarkan Aspose.Cells, dan Anda akan menemukan seluruh dunia kemungkinan.
## Pertanyaan yang Sering Diajukan
### Apa itu Objek OLE di Excel?  
Objek OLE adalah berkas tertanam yang memungkinkan Anda mengintegrasikan dokumen dari aplikasi Microsoft Office lainnya dalam lembar kerja Excel.
### Bisakah Aspose.Cells bekerja dengan format file lain?  
Ya! Aspose.Cells mendukung berbagai format, termasuk XLS, XLSX, CSV, dan banyak lagi.
### Apakah ada uji coba gratis yang tersedia untuk Aspose.Cells?  
 Ya! Anda dapat mencobanya[Di Sini](https://releases.aspose.com/).
### Bisakah saya mengakses beberapa objek OLE dalam satu lembar kerja?  
Tentu saja! Anda dapat mengulanginya`ws.OleObjects` untuk mengakses semua objek OLE yang tertanam dalam lembar kerja.
### Bagaimana cara membeli lisensi untuk Aspose.Cells?  
 Anda dapat membeli lisensi langsung dari[Di Sini](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
