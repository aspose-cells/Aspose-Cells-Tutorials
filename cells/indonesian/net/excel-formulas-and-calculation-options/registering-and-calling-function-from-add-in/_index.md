---
title: Mendaftarkan dan Memanggil Fungsi dari Add-In di Excel
linktitle: Mendaftarkan dan Memanggil Fungsi dari Add-In di Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Temukan cara mendaftarkan dan memanggil fungsi dari add-in di Excel menggunakan Aspose.Cells untuk .NET dengan tutorial langkah demi langkah kami yang mudah.
weight: 20
url: /id/net/excel-formulas-and-calculation-options/registering-and-calling-function-from-add-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mendaftarkan dan Memanggil Fungsi dari Add-In di Excel

## Perkenalan
Apakah Anda ingin meningkatkan pengalaman Excel Anda dengan memanggil fungsi dari add-in? Jika ya, Anda berada di tempat yang tepat! Add-in Excel bagaikan peri dalam spreadsheet; add-in ini secara ajaib memperluas fungsionalitas, memberi Anda banyak alat baru di ujung jari Anda. Dan dengan Aspose.Cells for .NET, lebih mudah dari sebelumnya untuk mendaftar dan menggunakan fungsi add-in ini. 
Dalam panduan ini, saya akan memandu Anda melalui proses pendaftaran dan pemanggilan fungsi dari add-in Excel menggunakan Aspose.Cells untuk .NET. Kami akan menguraikan semuanya langkah demi langkah, sehingga Anda akan merasa seperti seorang profesional dalam waktu singkat!
## Prasyarat
Sebelum kita menyelami keajaiban pengkodean, mari kita bahas apa saja yang perlu Anda siapkan:
1. Visual Studio: Pastikan Anda telah menyiapkan Visual Studio di komputer Anda. Di sinilah kita akan menulis dan menjalankan kode.
2.  Pustaka Aspose.Cells: Anda perlu memasang pustaka Aspose.Cells. Anda dapat mengunduhnya dari[halaman unduhan](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar C#: Sedikit pemahaman tentang C# akan sangat membantu; ini akan membantu Anda mengikutinya dengan lancar.
4.  Add-In Excel: Anda harus memiliki file add-in (seperti`.xlam`) yang berisi fungsi yang ingin Anda daftarkan dan gunakan.
5.  Contoh Add-In Excel: Untuk tutorial ini, kita akan menggunakan add-in Excel bernama`TESTUDF.xlam`Jadi, pastikan Anda memiliki ini!
Sekarang Anda sudah siap, mari kita mulai membuat kode!
## Mengimpor Paket
Untuk memulai, Anda perlu mengimpor beberapa namespace penting di bagian atas berkas C# Anda. Berikut ini yang perlu Anda sertakan:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Ruang nama ini akan memungkinkan Anda mengakses kelas dan metode yang akan kita gunakan dalam tutorial ini.
Mari kita uraikan ini menjadi beberapa langkah yang mudah dikelola. Di akhir panduan ini, Anda akan memiliki pemahaman yang kuat tentang cara mendaftarkan fungsi add-in dan menggunakannya di buku kerja Excel Anda.
## Langkah 1: Siapkan Direktori Sumber dan Output Anda
Sebelum Anda dapat mendaftarkan add-in Anda, Anda perlu menentukan di mana add-in dan file output Anda akan berada.
```csharp
// Direktori sumber
string sourceDir = "Your Document Directory";
// Direktori keluaran
string outputDir = "Your Document Directory";
```
 Mengganti`"Your Document Directory"` dengan jalur sebenarnya tempat Anda`.xlam` file dan file output akan disimpan. Ini seperti menyiapkan panggung sebelum pertunjukan dimulai.
## Langkah 2: Buat Buku Kerja Kosong
Berikutnya, Anda ingin membuat buku kerja kosong tempat kita dapat bermain-main dengan fungsi add-in.
```csharp
// Buat buku kerja kosong
Workbook workbook = new Workbook();
```
Baris kode ini menciptakan buku kerja baru yang akan berfungsi sebagai tempat bermain kita. Anggap saja ini sebagai kanvas baru, siap untuk goresan kreatif Anda.
## Langkah 3: Daftarkan Fungsi Add-In
Sekarang, mari kita masuk ke inti permasalahan! Saatnya mendaftarkan fungsi add-in Anda. Berikut cara melakukannya:
```csharp
// Daftarkan add-in yang mengaktifkan makro beserta nama fungsinya
int id = workbook.Worksheets.RegisterAddInFunction(sourceDir + @"TESTUDF.xlam", "TEST_UDF", false);
```
 Baris ini mendaftarkan fungsi add-in bernama`TEST_UDF` ditemukan di`TESTUDF.xlam` berkas tambahan.`false`parameter berarti bahwa add-in tidak dimuat dalam mode 'terisolasi'. 
## Langkah 4: Daftarkan Fungsi Tambahan (Jika Ada)
Jika Anda memiliki lebih banyak fungsi yang terdaftar dalam file add-in yang sama, Anda juga dapat mendaftarkannya!
```csharp
// Daftarkan lebih banyak fungsi dalam file (jika ada)
workbook.Worksheets.RegisterAddInFunction(id, "TEST_UDF1");
```
Di sini, Anda dapat melihat betapa mudahnya menambahkan lebih banyak fungsi dari add-in yang sama. Terus susun fungsi-fungsi tersebut seperti blok bangunan!
## Langkah 5: Akses Lembar Kerja
Mari kita lanjutkan dan akses lembar kerja di mana kita akan menggunakan fungsi kita. 
```csharp
// Akses lembar kerja pertama
Worksheet worksheet = workbook.Worksheets[0];
```
Kita mengakses lembar kerja pertama di buku kerja untuk meletakkan rumus kita. Ini seperti membuka pintu ke ruangan tempat kesenangan terjadi.
## Langkah 6: Mengakses Sel Tertentu
Berikutnya, kita perlu memilih sel mana yang ingin kita gunakan untuk rumus kita. 
```csharp
// Akses sel pertama
var cell = worksheet.Cells["A1"];
```
Di sini kita menunjuk ke sel A1. Di sinilah kita akan meletakkan rumus ajaib kita. Anda dapat menganggapnya sebagai penanda target pada peta harta karun Anda!
## Langkah 7: Mengatur Rumus
Sekarang saatnya untuk peluncuran besar! Mari kita tetapkan rumus yang memanggil fungsi terdaftar kita.
```csharp
// Tetapkan nama rumus yang ada di add-in
cell.Formula = "=TEST_UDF()";
```
Dengan baris ini, kita memberi tahu Excel untuk menggunakan fungsi kita di dalam sel A1. Ini seperti memberi perintah kepada Excel dan berkata, "Hei, lakukan ini!"
## Langkah 8: Simpan Buku Kerja
Terakhir namun tidak kalah pentingnya, tibalah waktunya untuk menyelamatkan karya agung kita.
```csharp
// Simpan buku kerja ke keluaran format XLSX.
workbook.Save(outputDir + @"test_udf.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
Di sini, kita menyimpan buku kerja kita sebagai file XLSX. Langkah terakhir ini seperti menaruh lukisan Anda dalam bingkai dan bersiap untuk memamerkannya!
## Langkah 9: Konfirmasi Eksekusi
Terakhir, mari kita selesaikan semuanya dengan mencetak pesan sukses pada konsol.
```csharp
Console.WriteLine("RegisterAndCallFuncFromAddIn executed successfully.");
```
Garis ini berfungsi sebagai bendera kemenangan kita. Sentuhan kecil yang bagus untuk memastikan semuanya berjalan lancar.
## Kesimpulan 
Nah, itu dia! Anda tidak hanya mempelajari cara mendaftarkan dan memanggil fungsi dari add-in Excel menggunakan Aspose.Cells for .NET, tetapi Anda juga memperoleh pemahaman yang lebih mendalam tentang setiap langkah yang terlibat. Hidup menjadi sedikit lebih mudah sekarang, bukan? Jadi, mengapa tidak mencobanya sendiri? Pelajari add-in Excel tersebut dan berikan lembar kerja Anda tingkat interaktivitas dan fungsionalitas yang baru.
## Pertanyaan yang Sering Diajukan
### Apa itu Add-In Excel?  
Add-In Excel adalah program yang menambahkan fitur, fungsi, atau perintah khusus ke Excel, yang memungkinkan pengguna untuk memperluas kemampuannya.
### Bisakah saya menggunakan Aspose.Cells tanpa menginstalnya secara lokal?  
Tidak, Anda perlu menginstal pustaka Aspose.Cells untuk menggunakannya di aplikasi .NET Anda.
### Bagaimana cara mendapatkan lisensi sementara untuk Aspose.Cells?  
 Anda dapat mengunjungi mereka[halaman lisensi sementara](https://purchase.aspose.com/temporary-license/) untuk informasi lebih lanjut.
### Apakah mungkin untuk memanggil beberapa fungsi dari satu add-in?  
 Ya! Anda dapat mendaftarkan beberapa fungsi dari file add-in yang sama menggunakan`RegisterAddInFunction` metode.
### Di mana saya dapat menemukan dokumentasi lebih lanjut tentang Aspose.Cells?  
 Anda dapat menjelajahi dokumentasi lengkap mereka di situs[Di Sini](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
