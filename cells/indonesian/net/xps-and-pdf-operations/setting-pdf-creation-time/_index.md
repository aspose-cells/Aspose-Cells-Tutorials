---
title: Mengatur Waktu Pembuatan PDF di .NET
linktitle: Mengatur Waktu Pembuatan PDF di .NET
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengatur waktu pembuatan PDF di .NET menggunakan Aspose.Cells. Ikuti panduan langkah demi langkah kami untuk konversi Excel ke PDF yang lancar.
weight: 11
url: /id/net/xps-and-pdf-operations/setting-pdf-creation-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengatur Waktu Pembuatan PDF di .NET

## Perkenalan
Di era digital saat ini, kemampuan untuk mengonversi dokumen ke berbagai format sangat penting bagi banyak aplikasi. Salah satu kebutuhan umum adalah mengonversi lembar kerja Excel ke berkas PDF. Hal ini tidak hanya mempertahankan format, tetapi juga membuat berbagi dan mencetak menjadi jauh lebih mudah. Jika Anda seorang pengembang yang bekerja dengan .NET, Aspose.Cells adalah pustaka fantastis yang menyederhanakan proses ini. Dalam tutorial ini, kita akan membahas cara mengatur waktu pembuatan PDF saat mengonversi berkas Excel ke PDF menggunakan Aspose.Cells untuk .NET.
## Prasyarat
Sebelum kita masuk ke inti kode, mari pastikan Anda memiliki semua yang dibutuhkan untuk memulai.
### Apa yang Anda Butuhkan
1. Visual Studio: Pastikan Anda telah menginstal Visual Studio di komputer Anda. Ini akan menjadi lingkungan pengembangan Anda.
2.  Aspose.Cells untuk .NET: Unduh pustaka Aspose.Cells dari[situs web](https://releases.aspose.com/cells/net/)Anda juga dapat memulai dengan uji coba gratis untuk menguji fungsinya.
3. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan membantu Anda memahami potongan kode dengan lebih baik.
4.  File Excel: Siapkan file Excel untuk konversi. Untuk contoh ini, kami akan menggunakan file bernama`Book1.xlsx`.
Sekarang setelah Anda menyiapkan prasyaratnya, mari masuk ke bagian yang menyenangkan—mengimpor paket yang diperlukan dan menulis kode!
## Paket Impor
Untuk memulai, Anda perlu mengimpor namespace yang diperlukan dalam berkas C# Anda. Hal ini penting karena memungkinkan Anda mengakses kelas dan metode yang disediakan oleh pustaka Aspose.Cells.
### Buka Proyek C# Anda
Buka Visual Studio dan buat proyek baru atau buka proyek yang sudah ada di mana Anda ingin menerapkan fitur konversi PDF.
### Tambahkan Referensi Aspose.Cells
Anda dapat menambahkan pustaka Aspose.Cells ke proyek Anda dengan mengklik kanan proyek Anda di Solution Explorer, memilih “Manage NuGet Packages,” dan mencari “Aspose.Cells.” Instal paket tersebut.
### Mengimpor Ruang Nama
Di bagian atas file C# Anda, sertakan namespace berikut:
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
Ruang nama ini akan memberi Anda akses ke kelas Buku Kerja dan fungsi penting lainnya.

Sekarang setelah paket kita diimpor, mari kita uraikan proses konversi file Excel ke PDF sambil mengatur waktu pembuatan.
## Langkah 1: Tentukan Direktori Dokumen
Pertama, Anda perlu menentukan direktori tempat dokumen Anda disimpan. Di sinilah file Excel Anda berada dan tempat PDF keluaran akan disimpan.
```csharp
string dataDir = "Your Document Directory"; // Tentukan direktori dokumen Anda
```
 Mengganti`"Your Document Directory"` dengan jalur sebenarnya tempat Anda`Book1.xlsx` file berada. Jalur ini akan membantu aplikasi menemukan file untuk diproses.
## Langkah 2: Muat File Excel
 Selanjutnya, Anda akan memuat file Excel ke dalam`Workbook` objek. Di sinilah Aspose.Cells unggul, karena memungkinkan Anda bekerja dengan file Excel dengan mudah.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Jalur ke file Excel Anda
Workbook workbook = new Workbook(inputPath); // Memuat file Excel
```
 Itu`Workbook` class digunakan untuk memuat dan memanipulasi file Excel. Dengan meneruskan jalur input, Anda memberi tahu aplikasi file mana yang akan digunakan.
## Langkah 3: Buat PdfSaveOptions
 Sekarang saatnya membuat contoh`PdfSaveOptions`Kelas ini memungkinkan Anda menentukan berbagai opsi untuk menyimpan buku kerja Anda sebagai PDF, termasuk waktu pembuatannya.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // Buat instance PdfSaveOptions
options.CreatedTime = DateTime.Now; // Atur waktu pembuatan ke sekarang
```
 Dengan pengaturan`options.CreatedTime` ke`DateTime.Now`, Anda memastikan bahwa PDF akan mencerminkan tanggal dan waktu saat ini saat dibuat.
## Langkah 4: Simpan Buku Kerja sebagai PDF
Terakhir, Anda akan menyimpan buku kerja sebagai berkas PDF menggunakan opsi yang baru saja Anda tentukan.
```csharp
workbook.Save(dataDir + "output.pdf", options); //Simpan sebagai PDF
```
 Baris kode ini mengambil buku kerja dan menyimpannya dalam format PDF di lokasi yang ditentukan.`options` parameter dilewatkan untuk menyertakan waktu pembuatan dalam metadata PDF.

## Kesimpulan
Nah, itu dia! Anda telah berhasil mengonversi file Excel ke PDF menggunakan Aspose.Cells for .NET, lengkap dengan stempel waktu pembuatan. Fitur ini dapat sangat berguna saat Anda perlu melacak versi dokumen atau saat Anda ingin memberikan informasi kepada penerima tentang kapan dokumen tersebut dibuat.
 Jika Anda ingin menjelajahi lebih banyak fitur Aspose.Cells, jangan ragu untuk memeriksa[dokumentasi](https://reference.aspose.com/cells/net/).
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka hebat untuk .NET yang memungkinkan pengembang untuk membuat, memanipulasi, dan mengonversi file Excel.
### Bisakah saya menggunakan Aspose.Cells secara gratis?
 Ya, Anda dapat memulai dengan uji coba gratis yang tersedia di[Situs web Aspose](https://releases.aspose.com/).
### Bagaimana cara mengatur properti PDF lainnya?
 Anda dapat mengatur berbagai properti PDF menggunakan`PdfSaveOptions` kelas, seperti ukuran halaman, kompresi, dan lainnya.
### Apakah mungkin untuk mengonversi beberapa file Excel sekaligus?
Ya, Anda dapat mengulang daftar file dan menerapkan proses konversi yang sama pada setiap file.
### Di mana saya bisa mendapatkan dukungan untuk Aspose.Cells?
 Anda bisa mendapatkan dukungan dari komunitas Aspose di[forum dukungan](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
