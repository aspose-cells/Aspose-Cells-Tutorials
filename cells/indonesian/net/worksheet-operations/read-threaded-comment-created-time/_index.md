---
title: Baca Waktu Pembuatan Komentar Berulir di Lembar Kerja
linktitle: Baca Waktu Pembuatan Komentar Berulir di Lembar Kerja
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara membaca waktu pembuatan komentar berulir di Excel menggunakan Aspose.Cells for .NET. Panduan langkah demi langkah dengan contoh kode disertakan.
weight: 21
url: /id/net/worksheet-operations/read-threaded-comment-created-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Baca Waktu Pembuatan Komentar Berulir di Lembar Kerja

## Perkenalan
Saat bekerja dengan file Excel, mengelola komentar dapat menjadi aspek penting dari kolaborasi dan umpan balik data. Jika Anda menggunakan Aspose.Cells untuk .NET, Anda akan merasa alat ini sangat hebat dalam menangani berbagai fungsi Excel, termasuk komentar berulir. Dalam tutorial ini, kita akan fokus pada cara membaca waktu pembuatan komentar berulir dalam lembar kerja. Baik Anda seorang pengembang berpengalaman atau baru memulai, panduan ini akan memandu Anda melalui proses ini langkah demi langkah.
## Prasyarat
Sebelum kita masuk ke kode, mari pastikan Anda memiliki semua yang dibutuhkan untuk memulai:
1. Aspose.Cells untuk .NET: Pastikan Anda telah menginstal pustaka Aspose.Cells. Anda dapat mengunduhnya dari[Situs web Aspose](https://releases.aspose.com/cells/net/).
2. Visual Studio: Instalasi Visual Studio atau IDE .NET lainnya yang berfungsi tempat Anda dapat menulis dan mengeksekusi kode C#.
3. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan membantu Anda memahami potongan kode dengan lebih baik.
4.  File Excel: Siapkan file Excel dengan beberapa komentar berulir. Untuk contoh ini, kita akan menggunakan file bernama`ThreadedCommentsSample.xlsx`.
Sekarang setelah prasyarat kita terpenuhi, mari impor paket yang diperlukan.
## Paket Impor
Untuk memulai Aspose.Cells, Anda perlu mengimpor namespace yang diperlukan. Berikut cara melakukannya:
### Impor Namespace Aspose.Cells
Buka proyek C# Anda di Visual Studio dan tambahkan perintah berikut di bagian atas berkas kode Anda:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Ruang nama ini memungkinkan Anda mengakses semua kelas dan metode yang disediakan oleh pustaka Aspose.Cells.
Setelah kita menyiapkan tahapannya, mari kita uraikan proses membaca waktu yang dibuat pada komentar berulir menjadi beberapa langkah yang lebih mudah dikelola.
## Langkah 1: Tentukan Direktori Sumber
Pertama, Anda perlu menentukan direktori tempat file Excel Anda berada. Hal ini penting karena program perlu mengetahui tempat mencari file tersebut.
```csharp
// Direktori sumber
string sourceDir = "Your Document Directory";
```
 Mengganti`"Your Document Directory"`dengan jalur sebenarnya ke berkas Excel Anda. Ini bisa jadi seperti ini`"C:\\Documents\\"`.
## Langkah 2: Muat Buku Kerja
Berikutnya, Anda akan memuat buku kerja Excel yang berisi komentar berulir. Berikut cara melakukannya:
```csharp
Workbook workbook = new Workbook(sourceDir + "ThreadedCommentsSample.xlsx");
```
 Baris kode ini membuat yang baru`Workbook` objek dengan memuat berkas Excel yang ditentukan. Jika berkas tidak ditemukan, pengecualian akan ditampilkan, jadi pastikan jalurnya benar.
## Langkah 3: Akses Lembar Kerja
Setelah buku kerja dimuat, langkah berikutnya adalah mengakses lembar kerja tertentu yang berisi komentar. Dalam kasus kita, kita akan mengakses lembar kerja pertama:
```csharp
// Akses lembar kerja pertama
Worksheet worksheet = workbook.Worksheets[0];
```
Baris ini mengambil lembar kerja pertama (indeks 0) dari buku kerja. Jika komentar Anda berada di lembar kerja lain, sesuaikan indeksnya.
## Langkah 4: Dapatkan Komentar Berulir
Sekarang, saatnya mengambil komentar berulir dari sel tertentu. Dalam contoh ini, kita akan mendapatkan komentar dari sel A1:
```csharp
// Dapatkan Komentar Berulir
ThreadedCommentCollection threadedComments = worksheet.Comments.GetThreadedComments("A1");
```
Baris ini mengambil semua komentar berulir yang terkait dengan sel A1. Jika tidak ada komentar, koleksi akan kosong.
## Langkah 5: Ulangi Melalui Komentar
Setelah komentar berulir diambil, kita sekarang dapat mengulanginya dan menampilkan detailnya, termasuk waktu yang dibuat:
```csharp
foreach (ThreadedComment comment in threadedComments)
{
    Console.WriteLine("Comment: " + comment.Notes);
    Console.WriteLine("Author: " + comment.Author.Name);
    Console.WriteLine("Created Time: " + comment.CreatedTime);
}
```
 Loop ini melewati setiap komentar di`threadedComments` koleksi dan mencetak teks komentar, nama penulis, dan waktu komentar dibuat.
## Langkah 6: Pesan Konfirmasi
Terakhir, setelah menjalankan logika pembacaan komentar, sebaiknya berikan pesan konfirmasi. Ini membantu dalam debugging dan memastikan bahwa kode telah berhasil dijalankan:
```csharp
Console.WriteLine("ReadThreadedCommentCreatedTime executed successfully.");
```
## Kesimpulan
Selamat! Anda telah berhasil mempelajari cara membaca waktu pembuatan komentar berulir dalam lembar kerja Excel menggunakan Aspose.Cells for .NET. Fungsionalitas ini dapat sangat berguna untuk melacak umpan balik dan kolaborasi dalam dokumen Excel Anda. Hanya dengan beberapa baris kode, Anda dapat mengekstrak informasi berharga yang dapat meningkatkan analisis data dan proses pelaporan Anda.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells untuk .NET?
Aspose.Cells untuk .NET adalah pustaka hebat yang memungkinkan pengembang untuk membuat, memanipulasi, dan mengonversi file Excel dalam aplikasi .NET.
### Bagaimana cara mengunduh Aspose.Cells untuk .NET?
 Anda dapat mengunduhnya dari[Situs web Aspose](https://releases.aspose.com/cells/net/).
### Apakah ada uji coba gratis yang tersedia?
 Ya, Anda dapat mencoba Aspose.Cells secara gratis dengan mengunjungi[halaman percobaan gratis](https://releases.aspose.com/).
### Bisakah saya mengakses komentar dari sel lain?
Tentu saja! Anda dapat mengubah referensi sel di`GetThreadedComments` metode untuk mengakses komentar dari sel mana pun.
### Di mana saya bisa mendapatkan dukungan untuk Aspose.Cells?
 Untuk dukungan, Anda dapat mengunjungi[Forum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
