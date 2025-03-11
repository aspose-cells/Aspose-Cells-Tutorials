---
title: Mengatur Opsi Format Tabel Pivot di .NET
linktitle: Mengatur Opsi Format Tabel Pivot di .NET
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara memanfaatkan Aspose.Cells for .NET untuk memformat Tabel Pivot dengan mudah. Jelajahi teknik langkah demi langkah untuk menyempurnakan presentasi data Anda.
weight: 20
url: /id/net/creating-and-configuring-pivot-tables/setting-format-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengatur Opsi Format Tabel Pivot di .NET

## Perkenalan
Pernahkah Anda merasa kewalahan dengan banyaknya data yang tersedia? Atau apakah Anda merasa kesulitan untuk menyajikan data ini dengan cara yang jelas dan mendalam? Jika demikian, selamat datang! Hari ini, kita akan menyelami dunia Pivot Tables yang menakjubkan di Excel menggunakan pustaka Aspose.Cells untuk .NET. Pivot Tables dapat menjadi pahlawan super dalam penyajian data, mengubah tumpukan angka menjadi laporan terstruktur dan mendalam yang memudahkan pengambilan keputusan. Bukankah itu mengubah permainan?
## Prasyarat
Sebelum kita mulai tutorialnya, mari kita pastikan Anda telah diperlengkapi dengan semua yang Anda butuhkan untuk berhasil. Berikut ini adalah prasyaratnya:
1. Pengetahuan Dasar tentang C#: Anda harus memiliki pemahaman mendasar tentang bahasa pemrograman C#. Jika Anda memahami dasar-dasarnya, Anda siap untuk mempelajarinya!
2. Visual Studio atau IDE C# apa pun: Anda perlu memiliki lingkungan pengembangan terintegrasi (IDE) seperti Visual Studio. Di sinilah keajaiban terjadi. 
3. Pustaka Aspose.Cells: Untuk memanfaatkan kekuatan Aspose.Cells, Anda perlu mengunduh paket ini. Anda dapat menemukannya dengan mudah di[Halaman Unduhan Aspose.Cells](https://releases.aspose.com/cells/net/).
4. Berkas Excel: Contoh berkas Excel diperlukan untuk mempraktikkan tutorial ini. Jangan ragu untuk membuat kumpulan data sederhana dalam lembar Excel (seperti "Book1.xls") untuk latihan ini.
5. .NET Framework: Pastikan Anda telah menginstal .NET Framework di komputer Anda.
Sudah paham? Luar biasa! Sekarang, mari kita mulai langkah pertama.
## Paket Impor
Untuk mulai menggunakan pustaka Aspose.Cells, pertama-tama kita perlu mengimpor paket-paket yang diperlukan. Berikut caranya:
### Buka Proyek Anda
Buka Visual Studio Anda (atau IDE C# apa pun yang Anda gunakan) dan buat proyek baru. Pilih Aplikasi Konsol karena akan memudahkan Anda menjalankan skrip.
### Tambahkan Referensi Aspose.Cells
1. Klik kanan pada proyek Anda di Solution Explorer.
2. Pilih Kelola Paket NuGet.
3.  Di kotak pencarian, ketik`Aspose.Cells` dan menginstalnya.
Sekarang, Anda siap untuk memasukkan pustaka. Anda perlu menambahkan perintah berikut di awal berkas kode Anda:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Baris ini memungkinkan Anda mengakses semua kelas dan metode yang tersedia di pustaka Aspose.Cells.
Setelah memahami dasar-dasarnya, mari kita bahas setiap bagian dari proses ini langkah demi langkah. Kami akan membahas cara mengatur berbagai opsi format untuk Tabel Pivot secara efektif.
## Langkah 1: Tentukan Direktori Dokumen Anda
Pertama, Anda perlu mengatur jalur direktori dokumen tempat file Excel masukan Anda berada. Baris kode ini menentukan lokasi file Anda.
```csharp
string dataDir = "Your Document Directory";
```
 Mengganti`"Your Document Directory"` dengan jalur sebenarnya tempat file "Book1.xls" Anda disimpan. Ini membantu program mengetahui tempat mencari file input.
## Langkah 2: Muat File Template
 Selanjutnya, kita akan memuat berkas Excel yang ingin kita manipulasi. Ini dilakukan dengan menggunakan`Workbook` kelas.
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Pada dasarnya, perintah ini memerintahkan program Anda untuk membuka berkas "Book1.xls" sehingga kita dapat mengolah datanya.
## Langkah 3: Dapatkan Lembar Kerja Pertama
Sekarang setelah buku kerja kita terbuka, mari masuk ke lembar kerja yang menampung data kita. 
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Di sini, kita mengakses lembar kerja pertama dari buku kerja (karena pengindeksan dimulai dari nol). Jika data Anda ada di lembar yang berbeda, cukup sesuaikan indeksnya.
## Langkah 4: Mengakses Tabel Pivot
Tabel Pivot sangat hebat, tetapi pertama-tama, kita perlu memilih tabel yang ingin kita gunakan. Dengan asumsi Anda mengetahui indeks Tabel Pivot Anda, berikut cara mengaksesnya.
```csharp
int pivotindex = 0;
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
Dalam kasus ini, kita mengakses Tabel Pivot pertama (indeks 0) dalam lembar kerja. 
## Langkah 5: Mengatur Total Keseluruhan Tabel Pivot untuk Baris
Mari mulai memformat! Kita dapat mengonfigurasi apakah akan menampilkan total keseluruhan untuk baris di Tabel Pivot kita.
```csharp
pivotTable.RowGrand = true;
```
 Mengatur properti ini ke`true` akan menampilkan total keseluruhan di bagian bawah setiap baris di Tabel Pivot Anda. Ini adalah cara yang sederhana namun efektif untuk memberikan ringkasan.
## Langkah 6: Mengatur Total Besar Tabel Pivot untuk Kolom
Sama seperti kita menetapkan total keseluruhan untuk baris, kita juga dapat melakukan ini untuk kolom.
```csharp
pivotTable.ColumnGrand = true;
```
Mengaktifkan ini akan memberikan total di sisi kanan setiap kolom. Sekarang Tabel Pivot Anda menjadi jagoan dalam meringkas data dari kedua arah!
## Langkah 7: Menampilkan String Kustom untuk Nilai Null
Detail yang sering diabaikan adalah penanganan nilai null. Anda mungkin ingin string tertentu muncul di sel yang berisi nilai null. 
```csharp
pivotTable.DisplayNullString = true;
pivotTable.NullString = "null";
```
Ini mengatur Tabel Pivot untuk menampilkan "null" setiap kali menemukan sel kosong, menambah kejelasan dan konsistensi pada laporan Anda.
## Langkah 8: Mengatur Tata Letak Tabel Pivot
Tabel Pivot dapat memiliki berbagai tata letak, dan kita dapat menyesuaikannya berdasarkan kebutuhan kita. Mari kita atur tata letak ke "DownThenOver".
```csharp
pivotTable.PageFieldOrder = PrintOrderType.DownThenOver;
```
Perintah ini menyesuaikan urutan tampilan bidang dalam laporan Anda, membuatnya lebih mudah dibaca. 
## Langkah 9: Menyimpan File Excel
Akhirnya, setelah Anda membuat semua penyesuaian yang indah ini, Anda perlu menyimpan kembali perubahan Anda ke dalam berkas Excel. 
```csharp
workbook.Save(dataDir + "output.xls");
```
Baris ini menyimpan buku kerja yang dimodifikasi sebagai “output.xls” di direktori yang Anda tentukan. 
Dan begitu saja, Anda telah menyempurnakan Tabel Pivot Anda dengan semua opsi pemformatan yang fantastis ini!
## Kesimpulan
Wah, kita telah menempuh perjalanan yang cukup panjang bersama, bukan? Dengan memanfaatkan kemampuan pustaka Aspose.Cells untuk .NET, Anda dapat dengan mudah mengubah tampilan dan perilaku data Anda di Excel. Kami membahas cara memuat buku kerja, mengakses dan memformat Tabel Pivot, dan mengakhiri semuanya dengan menyimpan modifikasi kami. Data tidak harus suram & suram; dengan beberapa penyesuaian, data dapat bersinar cemerlang.
## Pertanyaan yang Sering Diajukan
### Apa itu Tabel Pivot?
Tabel Pivot adalah fitur Excel yang meringkas dan menganalisis data secara dinamis.
### Apakah saya perlu menginstal Excel untuk menggunakan Aspose.Cells?
Tidak, Aspose.Cells adalah pustaka mandiri yang tidak memerlukan Excel untuk diinstal.
### Bisakah saya membuat Tabel Pivot dengan Aspose.Cells?
Ya, Aspose.Cells memungkinkan Anda membuat, memodifikasi, dan memanipulasi Tabel Pivot.
### Apakah Aspose.Cells gratis?
Aspose.Cells adalah pustaka berbayar, tetapi uji coba gratis tersedia.
### Di mana saya dapat menemukan lebih banyak dokumentasi Aspose.Cells?
 Lihat di sini[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) untuk panduan dan contoh yang mendalam.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
