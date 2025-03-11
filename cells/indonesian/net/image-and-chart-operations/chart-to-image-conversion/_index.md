---
title: Konversi Bagan ke Gambar dalam .NET
linktitle: Konversi Bagan ke Gambar dalam .NET
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengonversi grafik menjadi gambar dalam .NET menggunakan Aspose.Cells dengan panduan langkah demi langkah ini. Ubah grafik Excel menjadi gambar berkualitas tinggi dengan mudah.
weight: 10
url: /id/net/image-and-chart-operations/chart-to-image-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konversi Bagan ke Gambar dalam .NET

## Perkenalan
Mengonversi bagan dari Excel menjadi gambar dapat menjadi persyaratan penting saat membangun sistem pelaporan atau berbagi representasi data visual. Untungnya, dengan Aspose.Cells for .NET, proses ini semudah membuat pai! Baik Anda membuat laporan atau sekadar mengonversi bagan Excel menjadi gambar untuk tampilan yang lebih baik, panduan ini akan memandu Anda melalui proses tersebut langkah demi langkah.
## Prasyarat
Sebelum memulai, mari pastikan Anda telah menyiapkan semua perlengkapan untuk mengikuti tutorial ini.
### Pustaka Aspose.Cells untuk .NET
Pertama, Anda perlu mengunduh dan merujuk pustaka Aspose.Cells for .NET di proyek Anda. Anda dapat mengunduh versi terbarunya di sini:
- [Unduh Aspose.Cells untuk .NET](https://releases.aspose.com/cells/net/)
### Lingkungan .NET
Pastikan Anda telah menginstal .NET framework di sistem Anda. Anda dapat menggunakan Visual Studio atau lingkungan pengembangan .NET lainnya untuk menjalankan contoh ini.
### Pengaturan Lisensi (Opsional)
 Meskipun Anda dapat menggunakan Aspose.Cells dengan uji coba gratis, untuk fungsionalitas lengkap tanpa batasan, pertimbangkan untuk mengajukan permohonan[lisensi sementara](https://purchase.aspose.com/temporary-license/) atau beli satu dari[Di Sini](https://purchase.aspose.com/buy).

## Paket Impor
Untuk memulai, mari impor namespace yang diperlukan untuk bekerja dengan pustaka Aspose.Cells. Ini akan memungkinkan kita untuk memanipulasi file Excel dan menghasilkan gambar.
```csharp
using System.IO;
using System.Drawing;
using Aspose.Cells;
```
Pastikan Anda telah menyiapkan paket-paket ini sebelum memulai bagian pengkodean.

Sekarang, mari kita uraikan proses mengubah bagan menjadi gambar ke dalam beberapa langkah sederhana.
## Langkah 1: Siapkan Direktori Proyek Anda
Anda memerlukan tempat untuk menyimpan gambar yang dihasilkan, bukan? Pertama-tama mari kita buat direktori tempat gambar keluaran akan disimpan.

Kita mulai dengan menentukan jalur untuk direktori dokumen kita dan memastikan bahwa folder tersebut ada. Jika tidak ada, kita akan membuatnya.
```csharp
// Tentukan direktori untuk menyimpan gambar
string dataDir = "Your Document Directory";
//Periksa apakah direktori tersebut ada
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Dengan langkah ini, Anda siap membuat dan menyimpan gambar bagan ke direktori ini.
## Langkah 2: Buat Buku Kerja Baru
Di sini, kita akan membuat objek Workbook. Objek ini akan mewakili berkas Excel tempat diagram akan disematkan.

Buku kerja seperti berkas Excel yang berisi lembar-lembar kerja. Dengan membuat buku kerja baru, kita memulai dari awal dengan berkas Excel yang kosong.
```csharp
// Buat objek Buku Kerja baru
Workbook workbook = new Workbook();
```
## Langkah 3: Tambahkan Lembar Kerja Baru
Setiap file Excel memiliki lembar kerja (atau tab). Mari tambahkan satu ke buku kerja kita.

Menambahkan lembar kerja baru sangat penting karena kita akan memasukkan data dan grafik ke dalam lembar ini. Setelah lembar ditambahkan, kita mengambil referensinya.
```csharp
// Tambahkan lembar kerja baru ke buku kerja
int sheetIndex = workbook.Worksheets.Add();
// Ambil lembar kerja yang baru ditambahkan
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
## Langkah 4: Isi Lembar Kerja dengan Data
Untuk membuat bagan yang bermakna, kita memerlukan sejumlah data, bukan? Mari kita isi beberapa sel dengan nilai sampel.

Kita akan menambahkan data ke sel tertentu pada lembar kerja. Data ini akan digunakan untuk membuat diagram kita nanti.
```csharp
// Tambahkan data sampel ke sel
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
## Langkah 5: Tambahkan Bagan ke Lembar Kerja
Sekarang, mari membuat bagan kolom yang memvisualisasikan data yang baru saja kita tambahkan.

Kami menentukan jenis bagan (bagan kolom) dan menentukan ukuran dan posisinya dalam lembar kerja.
```csharp
// Tambahkan bagan kolom ke lembar kerja
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
```
## Langkah 6: Tentukan Sumber Data Bagan
Di sinilah keajaiban terjadi: menghubungkan bagan ke data dalam lembar kerja!

Kami menautkan diagram ke data di kolom A1 hingga B3. Ini memberi tahu diagram dari mana data akan diambil.
```csharp
// Hubungkan bagan ke data dalam rentang A1 hingga B3
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("A1:B3", true);
```
## Langkah 7: Ubah Bagan menjadi Gambar
Momen kebenaran: kita akan mengubah bagan ini menjadi berkas gambar!

 Di sini, kami menggunakan`ToImage` metode untuk mengonversi grafik ke format gambar pilihan Anda. Dalam kasus ini, kami mengonversinya ke format EMF (Enhanced Metafile).
```csharp
// Ubah grafik menjadi gambar dan simpan ke direktori
chart.ToImage(dataDir + "Chart.emf", ImageFormat.Emf);
```
Selesai! Bagan Anda kini telah disimpan sebagai gambar. Saatnya memberi selamat kepada diri sendiri.
## Langkah 8: Menampilkan Pesan Sukses
Untuk mengakhiri, mari tampilkan pesan yang mengonfirmasi pembuatan gambar.
```csharp
// Menampilkan pesan untuk menunjukkan keberhasilan
System.Console.WriteLine("Image generated successfully.");
```
## Kesimpulan
Wah! Begitu mudahnya mengonversi bagan dari Excel ke gambar menggunakan Aspose.Cells for .NET. Proses ini tidak hanya menyederhanakan penyajian data, tetapi juga meningkatkan fleksibilitas laporan atau dasbor yang lebih mengutamakan gambar daripada bagan tertanam.
Dengan mengikuti langkah-langkah yang diuraikan dalam panduan ini, Anda sekarang dapat mengubah bagan Excel apa pun menjadi gambar, sehingga memungkinkan Anda mengintegrasikan data visual ke dalam berbagai aplikasi dengan mulus.
## Pertanyaan yang Sering Diajukan
### Bisakah saya mengonversi berbagai jenis grafik menggunakan metode ini?
Ya, Anda dapat mengonversi jenis bagan apa pun yang didukung oleh Aspose.Cells termasuk bagan pai, bagan batang, bagan garis, dan banyak lagi!
### Apakah mungkin untuk mengubah format gambar?
 Tentu saja! Meskipun kami menggunakan EMF dalam contoh ini, Anda dapat mengubah format gambar menjadi PNG, JPEG, BMP, dan lainnya hanya dengan memodifikasi`ImageFormat` parameter.
### Apakah Aspose.Cells mendukung gambar beresolusi tinggi?
Ya, Aspose.Cells memungkinkan Anda mengontrol resolusi gambar dan pengaturan kualitas saat mengekspor bagan ke gambar.
### Bisakah saya mengubah beberapa bagan menjadi gambar sekaligus?
Ya, Anda dapat membuat pengulangan pada beberapa bagan dalam satu buku kerja dan mengonversi semuanya menjadi gambar hanya dalam beberapa baris kode.
### Apakah ada batasan jumlah grafik yang dapat saya konversi?
Tidak ada batasan bawaan yang diberlakukan oleh Aspose.Cells, tetapi pemrosesan data dalam jumlah besar mungkin bergantung pada memori dan kemampuan kinerja sistem Anda.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
