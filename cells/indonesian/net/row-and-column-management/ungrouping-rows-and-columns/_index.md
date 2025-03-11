---
title: Memisahkan Baris dan Kolom di Excel dengan Aspose.Cells
linktitle: Memisahkan Baris dan Kolom di Excel dengan Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara memisahkan baris dan kolom di Excel menggunakan Aspose.Cells for .NET dengan panduan lengkap ini. Sederhanakan manipulasi data Excel Anda.
weight: 15
url: /id/net/row-and-column-management/ungrouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Memisahkan Baris dan Kolom di Excel dengan Aspose.Cells

## Perkenalan
Saat menangani file Excel, Anda mungkin menemukan diri Anda dalam situasi di mana Anda perlu memisahkan baris dan kolom. Baik Anda sedang membersihkan spreadsheet atau memformat ulang data untuk presentasi yang lebih baik, Aspose.Cells untuk .NET adalah alat fantastis yang menyederhanakan proses tersebut. Dalam tutorial ini, saya akan memandu Anda melalui langkah-langkah untuk memisahkan baris dan kolom di Excel menggunakan Aspose.Cells. Pada akhirnya, Anda akan memiliki pemahaman yang kuat tentang cara bekerja dengan file Excel secara terprogram.
## Prasyarat
Sebelum mulai menggunakan kode, pastikan Anda telah menyiapkan semuanya. Berikut ini yang Anda perlukan:
1.  Visual Studio: Anda harus memiliki versi Visual Studio yang berfungsi yang terpasang di komputer Anda. Jika Anda belum memilikinya, Anda dapat mengunduhnya dari[Situs Visual Studio](https://visualstudio.microsoft.com/).
2. Aspose.Cells untuk .NET: Anda perlu mengunduh pustaka Aspose.Cells. Anda dapat mengunduhnya dari[Halaman Rilis Aspose](https://releases.aspose.com/cells/net/) Pastikan Anda memiliki lisensi yang diperlukan, yang dapat dibeli atau diperoleh melalui[lisensi sementara](https://purchase.aspose.com/temporary-license/).
3. Pengetahuan Dasar C#: Pemahaman mendasar tentang pemrograman C# akan membantu Anda mengikutinya dengan lebih mudah.
Setelah semuanya siap, kita dapat masuk ke bagian yang menyenangkan: kode!
## Paket Impor
Untuk memulai, Anda perlu mengimpor paket yang diperlukan ke dalam proyek C# Anda. Berikut cara melakukannya:
1. Buka proyek Anda di Visual Studio.
2. Tambahkan referensi ke pustaka Aspose.Cells. Anda dapat melakukannya dengan mengklik kanan pada Referensi di proyek Anda dan memilih Tambahkan Referensi. Telusuri lokasi tempat Anda menyimpan Aspose.Cells DLL.
3. Di bagian atas file C# Anda, tambahkan perintah penggunaan berikut:
```csharp
using System.IO;
using Aspose.Cells;
```
Sekarang semuanya sudah disiapkan, mari kita ikuti langkah-langkah untuk memisahkan baris dan kolom di lembar Excel Anda. 
## Langkah 1: Tentukan Direktori Dokumen
Pertama, Anda perlu menentukan direktori tempat file Excel Anda berada. Anda dapat mengaturnya sebagai berikut:
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```
 Mengganti`"Your Document Directory"` dengan jalur sebenarnya di komputer Anda tempat file Excel disimpan. 
## Langkah 2: Buat Aliran File
Selanjutnya, Anda perlu membuat aliran file untuk membuka file Excel. Berikut cara melakukannya:
```csharp
// Membuat aliran file yang berisi file Excel yang akan dibuka
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
 Di sini, Anda membuka file bernama`book1.xls`Pastikan berkas ini ada di direktori yang Anda tentukan, atau Anda akan mengalami kesalahan berkas tidak ditemukan.
## Langkah 3: Membuat Instansi Objek Buku Kerja
Sekarang, mari kita muat berkas Excel ke dalam objek Buku Kerja. Ini memungkinkan Anda untuk memanipulasi buku kerja secara terprogram:
```csharp
// Membuat instance objek Buku Kerja
// Membuka file Excel melalui aliran file
Workbook workbook = new Workbook(fstream);
```
Dengan baris kode ini, Anda telah berhasil memuat file Excel ke dalam memori dan siap bekerja dengannya.
## Langkah 4: Akses Lembar Kerja
Setelah Anda memiliki buku kerja, langkah berikutnya adalah mengakses lembar kerja tertentu tempat Anda ingin memisahkan baris dan kolom. Berikut cara melakukannya:
```csharp
// Mengakses lembar kerja pertama dalam file Excel
Worksheet worksheet = workbook.Worksheets[0];
```
Dalam kasus ini, kita mengakses lembar kerja pertama. Jika data Anda ada di lembar lain, Anda dapat mengubah indeksnya.
## Langkah 5: Pisahkan Baris
Sekarang tibalah bagian yang menarik! Mari kita pisahkan enam baris pertama (dari baris 0 hingga baris 5). Gunakan kode berikut:
```csharp
// Memisahkan enam baris pertama (dari 0 hingga 5)
worksheet.Cells.UngroupRows(0, 5);
```
Metode ini menghapus pengelompokan apa pun yang telah diterapkan pada baris yang ditentukan. Semudah itu!
## Langkah 6: Pisahkan Kolom
Sama seperti baris, Anda juga dapat memisahkan kolom. Berikut cara memisahkan tiga kolom pertama (dari kolom 0 hingga kolom 2):
```csharp
// Memisahkan tiga kolom pertama (dari 0 hingga 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## Langkah 7: Simpan File Excel yang Telah Dimodifikasi
 Setelah Anda memisahkan baris dan kolom, langkah selanjutnya adalah menyimpan perubahan kembali ke file Excel. Anda dapat melakukannya dengan menggunakan`Save` metode:
```csharp
// Menyimpan file Excel yang dimodifikasi
workbook.Save(dataDir + "output.xls");
```
 Dalam contoh ini, kami menyimpan file yang dimodifikasi sebagai`output.xls`Anda dapat mengubah nama berkas sesuai keinginan Anda.
## Langkah 8: Tutup Aliran File
Terakhir, untuk mengosongkan sumber daya, Anda harus menutup aliran file:
```csharp
// Menutup aliran file untuk membebaskan semua sumber daya
fstream.Close();
```
Ini merupakan praktik yang baik untuk memastikan bahwa aplikasi Anda tidak menahan pegangan berkas lebih lama dari yang diperlukan.
## Kesimpulan
Nah, itu dia! Anda telah berhasil mempelajari cara memisahkan baris dan kolom dalam file Excel menggunakan Aspose.Cells for .NET. Hanya dengan beberapa baris kode, Anda dapat membuat perubahan signifikan pada file Excel secara terprogram. Baik Anda mengotomatiskan laporan atau menyiapkan data untuk analisis, menguasai teknik ini dapat menghemat banyak waktu.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka yang hebat untuk bekerja dengan file Excel dalam aplikasi .NET, yang memungkinkan manipulasi, konversi, dan pembuatan lembar kerja dengan mudah.
### Bisakah saya memisahkan baris dan kolom di Excel menggunakan pustaka lain?
Ya, ada pustaka lain yang tersedia untuk manipulasi Excel di .NET, tetapi Aspose.Cells menawarkan fitur yang luas dan kemudahan penggunaan.
### Apakah ada cara untuk membatalkan perubahan setelah menyimpan?
Setelah Anda menyimpan berkas Excel, keadaan sebelumnya tidak dapat dipulihkan kecuali Anda memiliki cadangan berkas asli.
### Bagaimana cara mendapatkan dukungan untuk Aspose.Cells?
 Anda dapat menemukan dukungan dengan mengunjungi[Forum Dukungan Aspose](https://forum.aspose.com/c/cells/9), tempat Anda dapat mengajukan pertanyaan dan menemukan solusi.
### Bisakah saya menggunakan Aspose.Cells tanpa lisensi?
Ya, Anda dapat menggunakan Aspose.Cells secara gratis dengan batasan tertentu, dan Anda dapat memulai dengan[lisensi sementara](https://purchase.aspose.com/temporary-license/) untuk fungsionalitas penuh.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
