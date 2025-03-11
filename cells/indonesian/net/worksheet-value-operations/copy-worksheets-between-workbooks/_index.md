---
title: Menyalin Lembar Kerja antara Dua Buku Kerja menggunakan Aspose.Cells
linktitle: Menyalin Lembar Kerja antara Dua Buku Kerja menggunakan Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menyalin lembar kerja antar-buku kerja Excel menggunakan Aspose.Cells untuk .NET dalam tutorial terperinci dan langkah demi langkah ini. Sempurna untuk mengotomatiskan proses Excel.
weight: 14
url: /id/net/worksheet-value-operations/copy-worksheets-between-workbooks/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menyalin Lembar Kerja antara Dua Buku Kerja menggunakan Aspose.Cells

## Perkenalan
Mengelola file Excel secara terprogram telah menjadi kebutuhan untuk mengotomatiskan penanganan data dalam proses bisnis. Baik Anda seorang pengembang yang membangun aplikasi analitik atau analis bisnis yang mencoba mengotomatiskan laporan, Aspose.Cells for .NET menawarkan perangkat yang tangguh untuk memanipulasi file Excel dengan mudah. Dalam tutorial ini, kami akan membahas cara menyalin lembar kerja antara dua buku kerja menggunakan Aspose.Cells for .NET. Kami akan membahas prasyarat, paket impor, dan panduan terperinci langkah demi langkah yang mudah diikuti.
## Prasyarat
Sebelum kita mulai membuat kode, mari pastikan Anda memiliki semua yang perlu diikuti:
-  Aspose.Cells untuk .NET: Unduh dan instal Aspose.Cells untuk .NET dari[halaman unduhan](https://releases.aspose.com/cells/net/).
- .NET Framework: Pastikan Anda telah menginstal .NET di lingkungan pengembangan Anda.
- IDE: Anda dapat menggunakan IDE apa pun yang kompatibel dengan C# (Visual Studio direkomendasikan).
-  Lisensi: Anda dapat mencoba Aspose.Cells dengan[lisensi sementara gratis](https://purchase.aspose.com/temporary-license/) atau pertimbangkan[membeli lisensi penuh](https://purchase.aspose.com/buy) untuk fungsionalitas lengkap.
 Lihat di sini[Dokumentasi Aspose.Cells untuk .NET](https://reference.aspose.com/cells/net/) jika Anda memerlukan informasi lebih lanjut tentang fitur dan kemampuan tertentu.
## Paket Impor
Untuk memulai, Anda perlu mengimpor namespace yang diperlukan ke dalam kode Anda. Berikut cara melakukannya:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Baris tunggal ini memberi Anda akses ke semua fitur Aspose.Cells yang hebat.
Dalam tutorial ini, kami akan membagi tugas menjadi beberapa langkah yang dapat dikelola. Setiap langkah dibangun berdasarkan langkah sebelumnya, sehingga Anda akan memiliki cuplikan kode yang lengkap dan berfungsi pada akhirnya.
## Langkah 1: Tentukan Direktori Dokumen
Pertama, mari tentukan jalur tempat file buku kerja kita disimpan. Jalur ini akan memberi tahu program tempat menemukan buku kerja sumber dan tempat menyimpan file yang disalin.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```
 Di sini, ganti`"Your Document Directory"` dengan jalur sebenarnya tempat file Anda disimpan.
## Langkah 2: Mengatur Jalur File Input
Pada langkah ini, kita akan menentukan jalur ke buku kerja asli yang berisi lembar kerja yang ingin kita salin. Sebagai contoh, mari kita asumsikan file tersebut diberi nama`book1.xls`.
```csharp
string inputPath = dataDir + "book1.xls";
```
 Garis ini menggabungkan`dataDir` dengan nama file, membuat jalur lengkap ke`book1.xls`Ini adalah buku kerja yang berisi lembar yang akan kita salin.
## Langkah 3: Buka Buku Kerja Sumber
Sekarang, mari kita buka buku kerja sumber (`book1.xls` ) dengan membuat`Workbook` objek dan lewat di`inputPath` sebagai argumen.
```csharp
// Membuat Buku Kerja.
// Buka berkas ke dalam buku pertama.
Workbook sourceWorkbook = new Workbook(inputPath);
```
 Di sini, kita inisialisasi`sourceWorkbook` untuk mewakili buku kerja sumber kita. Objek ini memberi kita akses ke semua lembar kerja dalam file tersebut.
## Langkah 4: Buat Buku Kerja Tujuan
Pada langkah ini, kita akan membuat buku kerja baru yang akan bertindak sebagai tujuan untuk lembar kerja yang disalin. Ini akan berfungsi sebagai papan tulis kosong tempat kita akan menempelkan lembar yang disalin.
```csharp
// Buat Buku Kerja lainnya.
Workbook destinationWorkbook = new Workbook();
```
 Kita`destinationWorkbook` kosong secara default, hanya berisi satu lembar kerja.
## Langkah 5: Salin Lembar Kerja ke Buku Kerja Baru
Sekarang tibalah inti dari tutorial ini—menyalin lembar kerja. Kita akan menyalin lembar kerja pertama dari buku kerja sumber dan menempelkannya ke slot lembar kerja pertama dari buku kerja tujuan.
```csharp
// Salin lembar pertama buku kerja sumber ke buku kerja tujuan.
destinationWorkbook.Worksheets[0].Copy(sourceWorkbook.Worksheets[0]);
```
Dalam kode ini:
- `sourceWorkbook.Worksheets[0]` mewakili lembar kerja pertama dalam buku kerja sumber kami.
- `destinationWorkbook.Worksheets[0]` merujuk pada lembar kerja pertama dalam buku kerja tujuan.
-  Itu`.Copy` metode ini melakukan pekerjaan berat, memindahkan lembar kerja secara mulus dari satu buku kerja ke buku kerja lainnya.
## Langkah 6: Simpan Buku Kerja Tujuan
Terakhir, mari simpan buku kerja tujuan kita. Ini akan menyelesaikan proses penyalinan dan membuat file keluaran yang berisi lembar kerja yang disalin.
```csharp
// Simpan berkasnya.
destinationWorkbook.Save(dataDir + "CopyWorksheetsBetweenWorkbooks_out.xls");
```
 Mengganti`"CopyWorksheetsBetweenWorkbooks_out.xls"` dengan nama berkas keluaran pilihan Anda. Sekarang, Anda akan memiliki berkas baru di direktori yang Anda tentukan dengan lembar kerja yang disalin.

## Kesimpulan
Selamat! Anda telah berhasil menyalin lembar kerja dari satu buku kerja ke buku kerja lain menggunakan Aspose.Cells untuk .NET. Hanya dengan beberapa baris kode, Anda dapat mengotomatiskan duplikasi lembar kerja di beberapa buku kerja, menghemat waktu dan mengurangi kesalahan. Aspose.Cells adalah alat canggih yang menyederhanakan manipulasi file Excel, sehingga ideal untuk tugas otomatisasi data sederhana dan kompleks.
## Pertanyaan yang Sering Diajukan
### Bisakah saya menyalin beberapa lembar kerja sekaligus?  
Ya, Anda dapat mengulang lembar kerja di buku kerja sumber dan menyalin masing-masing satu per satu ke buku kerja tujuan.
### Apakah menyalin lembar kerja mentransfer semua format dan data?  
 Tentu saja!`.Copy` metode di Aspose.Cells mentransfer semuanya, termasuk data, pemformatan, dan rumus.
### Bisakah saya menyalin lembar kerja ke buku kerja yang sudah ada?  
Ya, Anda dapat menyalin lembar kerja ke buku kerja yang ada dengan menentukan indeks lembar kerja di buku kerja tujuan.
### Bisakah saya mengganti nama lembar kerja yang disalin?  
 Tentu saja! Setelah menyalin, gunakan`destinationWorkbook.Worksheets[0].Name = "NewSheetName";` untuk mengganti nama lembar kerja.
### Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells?  
 Anda dapat mencoba Aspose.Cells dengan[lisensi sementara gratis](https://purchase.aspose.com/temporary-license/)atau membeli lisensi penuh untuk akses tanpa batas.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
