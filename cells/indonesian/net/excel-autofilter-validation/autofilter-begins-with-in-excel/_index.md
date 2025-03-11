---
title: Filter Otomatis Dimulai Dengan di Excel
linktitle: Filter Otomatis Dimulai Dengan di Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara memfilter otomatis baris Excel menggunakan Aspose.Cells di .NET dengan mudah dengan panduan langkah demi langkah yang komprehensif ini.
weight: 10
url: /id/net/excel-autofilter-validation/autofilter-begins-with-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Filter Otomatis Dimulai Dengan di Excel

## Perkenalan

Dalam hal mengolah data, Excel telah memantapkan dirinya sebagai aplikasi andalan untuk berbagai industri dan tujuan. Salah satu fiturnya yang paling hebat adalah AutoFilter, yang memudahkan penyaringan kumpulan data yang luas. Jika Anda menggunakan Aspose.Cells untuk .NET, Anda dapat memanfaatkan fungsi ini secara terprogram dan menyempurnakan tugas pengelolaan data Anda secara signifikan. Dalam panduan ini, kami akan memandu Anda melalui proses penerapan fitur yang memfilter baris Excel berdasarkan apakah baris tersebut dimulai dengan string tertentu.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki prasyarat berikut ini:

1. Lingkungan Pengembangan: Biasakan diri Anda dengan lingkungan pengembangan .NET. Ini bisa berupa Visual Studio atau IDE lain pilihan Anda.
2.  Aspose.Cells untuk .NET: Anda perlu menginstal Aspose.Cells untuk .NET. Jika Anda belum melakukannya, Anda dapat mengunduhnya dengan mudah[Di Sini](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar C#: Pemahaman mendasar tentang C# dan cara bekerja dengan pustaka .NET akan membantu Anda mengikutinya dengan lancar.
4.  Contoh Data: Anda harus memiliki file Excel, sebaiknya diberi nama`sourseSampleCountryNames.xlsx`, yang terletak di direktori sumber yang Anda tentukan. File ini akan berisi data yang akan kami saring.
5.  Lisensi: Untuk fungsionalitas penuh, pertimbangkan untuk memperoleh lisensi melalui ini[link](https://purchase.aspose.com/buy) Jika Anda ingin menguji fitur-fiturnya, Anda dapat meminta[lisensi sementara](https://purchase.aspose.com/temporary-license/).

Sudah siap? Ayo!

## Paket Impor

Untuk memulai, impor namespace yang diperlukan di bagian atas file C# Anda:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Ini mengimpor fungsionalitas inti Aspose.Cells bersama fitur sistem dasar yang akan kita andalkan untuk interaksi konsol.

Sekarang setelah Anda menyiapkan lingkungan dan mengimpor paket yang diperlukan, mari kita uraikan fitur Autofilter menjadi beberapa langkah yang dapat dikelola. Kita akan menerapkan filter yang mengekstrak baris yang dimulai dengan "Ba".

## Langkah 1: Tentukan Direktori Sumber dan Output

Pertama, mari tentukan di mana file Excel input kita berada, dan juga di mana kita ingin menyimpan output yang telah difilter:

```csharp
// Direktori sumber
string sourceDir = "Your Document Directory\\";

// Direktori keluaran
string outputDir = "Your Document Directory\\";
```

 Penjelasan: Di sini, ganti`"Your Document Directory\\"` dengan jalur sebenarnya ke direktori Anda. Pastikan untuk mengakhiri jalur direktori dengan garis miring terbalik ganda (`\\`) untuk menghindari masalah jalur apa pun.

## Langkah 2: Membuat Instansiasi Objek Buku Kerja

Berikutnya, kita akan membuat objek Buku Kerja yang menunjuk ke file Excel kita:

```csharp
// Membuat instance objek Buku Kerja yang berisi data sampel
Workbook workbook = new Workbook(sourceDir + "sourseSampleCountryNames.xlsx");
```

 Penjelasan: Baris ini menginisialisasi instance Workbook baru menggunakan jalur file yang ditentukan.`Workbook` kelas itu mendasar karena mewakili keseluruhan berkas Excel.

## Langkah 3: Mengakses Lembar Kerja Pertama

Sekarang, kita perlu mengakses lembar kerja spesifik yang ingin kita kerjakan:

```csharp
// Mengakses lembar kerja pertama dalam file Excel
Worksheet worksheet = workbook.Worksheets[0];
```

 Penjelasan:`Worksheets` koleksi memungkinkan kita untuk mengakses lembar-lembar individual. Menggunakan`[0]` merujuk pada lembar kerja pertama dalam berkas Excel Anda, yang umumnya merupakan praktik umum saat bekerja dengan berkas satu lembar.

## Langkah 4: Menyiapkan AutoFilter

Di sinilah keajaiban dimulai! Kita akan membuat rentang AutoFilter untuk data kita:

```csharp
// Membuat AutoFilter dengan memberikan rentang sel
worksheet.AutoFilter.Range = "A1:A18";
```

 Penjelasan:`AutoFilter.Range` Properti ini memungkinkan Anda menentukan baris mana yang akan difilter. Dalam kasus ini, kami memfilter baris dalam rentang A1 hingga A18, yang diasumsikan berisi data kami.

## Langkah 5: Terapkan Kondisi Filter

Langkah selanjutnya adalah menentukan kondisi filter. Kami ingin menampilkan hanya baris-baris yang nilai kolom pertamanya dimulai dengan "Ba":

```csharp
// Inisialisasi filter untuk baris yang dimulai dengan string "Ba"
worksheet.AutoFilter.Custom(0, FilterOperatorType.BeginsWith, "Ba");
```

 Penjelasan:`Custom` metode mendefinisikan logika penyaringan kami. Argumen pertama (`0` ) menunjukkan bahwa kita memfilter berdasarkan kolom pertama (A), dan`FilterOperatorType.BeginsWith` menentukan kondisi kita untuk mencari baris yang dimulai dengan "Ba".

## Langkah 6: Segarkan Filter

Setelah menerapkan kondisi filter, kita perlu memastikan Excel melakukan penyegaran untuk mencerminkan perubahan:

```csharp
// Segarkan filter untuk menampilkan/menyembunyikan baris yang difilter
worksheet.AutoFilter.Refresh();
```

Penjelasan: Baris ini memanggil penyegaran pada AutoFilter untuk memastikan bahwa baris yang terlihat sesuai dengan kriteria filter yang diterapkan. Mirip dengan menekan tombol penyegaran di Excel.

## Langkah 7: Simpan File Excel yang Telah Dimodifikasi

Sekarang saatnya untuk menyimpan perubahan yang telah kita buat:

```csharp
// Menyimpan file Excel yang dimodifikasi
workbook.Save(outputDir + "outSourseSampleCountryNames.xlsx");
```

 Penjelasan:`Save` metode menulis kembali Buku Kerja yang dimodifikasi ke jalur keluaran yang ditentukan. Ini termasuk dalam penulisan filter yang Anda tentukan ke dalam file baru sehingga data asli Anda tetap utuh.

## Langkah 8: Konfirmasi Output

Terakhir, mari kita konfirmasikan bahwa operasi kita berhasil:

```csharp
Console.WriteLine("AutofilterBeginsWith executed successfully.\r\n");
```

Penjelasan: Baris sederhana ini menampilkan pesan konfirmasi ke konsol, yang memberi tahu Anda bahwa proses penyaringan telah selesai tanpa kesalahan.

## Kesimpulan

Di dunia di mana manajemen data dapat terasa memberatkan, menguasai fitur seperti AutoFilter di Excel melalui Aspose.Cells untuk .NET memberdayakan Anda untuk memanipulasi data secara efisien dan efektif. Anda telah mempelajari cara memfilter baris Excel yang dimulai dengan "Ba," dengan menerapkan metode ini langkah demi langkah. Dengan latihan, Anda akan dapat mengadaptasi metode ini untuk berbagai kebutuhan pemfilteran data dalam proyek Anda yang sedang berjalan.

## Pertanyaan yang Sering Diajukan

### Apa tujuan AutoFilter di Excel?  
AutoFilter memungkinkan pengguna untuk dengan cepat menyortir dan memfilter data dalam spreadsheet, sehingga memudahkan untuk fokus pada kumpulan data tertentu.

### Bisakah saya memfilter berdasarkan beberapa kriteria dengan Aspose.Cells?  
Ya, Aspose.Cells mendukung opsi pemfilteran tingkat lanjut yang memungkinkan Anda menetapkan beberapa kriteria.

### Apakah saya memerlukan lisensi agar Aspose.Cells dapat menggunakannya?  
Meskipun Anda dapat memulai dengan uji coba gratis, lisensi diperlukan untuk fungsionalitas penuh dan untuk menghapus segala batasan uji coba.

### Jenis pemfilteran apa yang dapat saya lakukan menggunakan Aspose.Cells?  
Anda dapat memfilter data berdasarkan nilai, kondisi (seperti dimulai dengan atau diakhiri dengan), dan pemfilteran khusus untuk memenuhi persyaratan spesifik Anda.

### Di mana saya dapat menemukan informasi lebih lanjut tentang Aspose.Cells untuk .NET?  
 Anda dapat memeriksa dokumentasinya[Di Sini](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
