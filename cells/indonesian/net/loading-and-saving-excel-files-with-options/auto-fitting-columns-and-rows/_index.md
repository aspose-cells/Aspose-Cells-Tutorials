---
title: Sesuaikan Kolom dan Baris Secara Otomatis saat Memuat HTML di Buku Kerja
linktitle: Sesuaikan Kolom dan Baris Secara Otomatis saat Memuat HTML di Buku Kerja
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menyesuaikan kolom dan baris secara otomatis saat memuat HTML ke Excel menggunakan Aspose.Cells for .NET. Panduan langkah demi langkah disertakan.
weight: 10
url: /id/net/loading-and-saving-excel-files-with-options/auto-fitting-columns-and-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sesuaikan Kolom dan Baris Secara Otomatis saat Memuat HTML di Buku Kerja

## Perkenalan
Pernahkah Anda bertanya-tanya bagaimana cara menyesuaikan ukuran kolom dan baris secara otomatis saat memuat konten HTML ke dalam buku kerja Excel menggunakan Aspose.Cells for .NET? Nah, Anda berada di tempat yang tepat! Dalam tutorial ini, kita akan membahas secara mendalam cara memuat tabel HTML ke dalam buku kerja dan memastikan bahwa kolom dan baris disesuaikan secara otomatis agar sesuai dengan konten. Jika Anda bekerja dengan data dinamis yang sering berubah, panduan ini akan menjadi panduan Anda untuk membuat lembar Excel yang diformat dengan baik dari HTML.
### Prasyarat
Sebelum mulai membuat kode, ada beberapa hal yang perlu Anda siapkan di sistem Anda. Jangan khawatir, ini mudah dan sederhana!
1. Visual Studio Terpasang: Anda memerlukan Visual Studio atau lingkungan pengembangan .NET lainnya.
2.  Aspose.Cells untuk .NET: Anda dapat[unduh versi terbaru](https://releases.aspose.com/cells/net/) atau gunakan manajer paket NuGet untuk menginstalnya.
3. .NET Framework: Pastikan Anda telah menginstal .NET Framework 4.0 atau yang lebih tinggi.
4. Pemahaman Dasar tentang C#: Memiliki sedikit pengetahuan tentang C# akan membuat tutorial ini lebih lancar bagi Anda.
5. Data Tabel HTML: Siapkan beberapa konten HTML (bahkan tabel dasar) yang ingin Anda muat ke Excel.
## Paket Impor
Hal pertama yang harus dilakukan—mari impor namespace yang diperlukan untuk memulai. Berikut ini daftar sederhana tentang apa yang perlu Anda impor:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Paket ini memungkinkan Anda menangani buku kerja, memanipulasi data HTML, dan memuatnya dengan mudah ke Excel.
Mari kita bagi proses ini menjadi beberapa bagian yang mudah dikelola sehingga Anda dapat mengikutinya dengan mudah. Di akhir pembahasan ini, Anda akan memiliki contoh praktis tentang cara menyesuaikan kolom dan baris secara otomatis saat memuat HTML ke dalam buku kerja menggunakan Aspose.Cells for .NET.
## Langkah 1: Siapkan Direktori Dokumen
Untuk menyimpan dan mengambil file dengan mudah, kami akan menentukan jalur penyimpanan dokumen Anda. Anda dapat mengganti jalur direktori dengan lokasi folder Anda sendiri.
```csharp
string dataDir = "Your Document Directory";
```
Baris ini mengatur direktori tempat file Excel Anda akan disimpan. Penting untuk mengatur file Anda dengan benar saat mengerjakan beberapa proyek. Bayangkan ini sebagai lemari arsip proyek Anda!
## Langkah 2: Buat Data HTML sebagai String
Selanjutnya, kita akan mendefinisikan beberapa konten HTML dasar. Untuk contoh ini, kita akan menggunakan tabel HTML sederhana. Anda dapat menyesuaikannya sesuai dengan kebutuhan proyek Anda.
```csharp
string sampleHtml = "<html><body><table><tr><td>This is sample text.</td><td>Some text.</td></tr><tr><td>This is another sample text.</td><td>Some text.</td></tr></table></body></html>";
```
Kami mendefinisikan string HTML yang sangat mendasar di sini. String ini berisi tabel dengan beberapa baris dan kolom. Anda dapat menambahkan lebih banyak baris atau kolom sesuai kebutuhan Anda. Anggap saja seperti menyiapkan bahan-bahan sebelum memasak!
## Langkah 3: Muat String HTML ke MemoryStream
 Sekarang setelah konten HTML kita siap, langkah selanjutnya adalah memuatnya ke dalam memori menggunakan`MemoryStream`Hal ini memungkinkan kita untuk memanipulasi konten HTML dalam memori tanpa menyimpannya ke dalam disk terlebih dahulu.
```csharp
MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(sampleHtml));
```
 Dengan mengubah string HTML menjadi array byte dan memasukkannya ke dalam`MemoryStream`, kita dapat mengolah data HTML dalam memori. Bayangkan langkah ini seperti menyiapkan hidangan dalam panci sebelum memasukkannya ke dalam oven!
## Langkah 4: Muat MemoryStream ke dalam Buku Kerja (Tanpa Penyesuaian Otomatis)
 Setelah kita memiliki konten HTML di memori, kita memuatnya ke Aspose`Workbook`Pada titik ini, kami belum melakukan penyesuaian otomatis pada kolom dan baris. Ini adalah skenario "sebelum" kami, untuk dibandingkan dengan versi penyesuaian otomatis nanti.
```csharp
Workbook wb = new Workbook(ms);
wb.Save(dataDir + "outputWithout_AutoFitColsAndRows.xlsx");
```
Buku kerja dimuat dengan konten HTML, tetapi kolom dan baris belum disesuaikan secara otomatis dengan teks. Bayangkan ini seperti memanggang kue tetapi lupa memeriksa suhunya—ini berhasil, tetapi mungkin tidak sempurna!
## Langkah 5: Tentukan Opsi Pemuatan HTML dengan Penyesuaian Otomatis Diaktifkan
 Nah, inilah keajaibannya! Kita membuat sebuah contoh`HtmlLoadOptions` dan mengaktifkan`AutoFitColsAndRows` properti. Ini memastikan bahwa saat konten HTML dimuat, kolom dan baris akan menyesuaikan diri dengan konten di dalamnya.
```csharp
HtmlLoadOptions opts = new HtmlLoadOptions();
opts.AutoFitColsAndRows = true;
```
Dengan menyetel opsi ini, kita memberi tahu Aspose.Cells untuk mengubah ukuran baris dan kolom secara otomatis. Bayangkan ini seperti menyetel oven ke suhu yang sempurna sehingga kue mengembang dengan sempurna!
## Langkah 6: Muat HTML ke Buku Kerja dengan Penyesuaian Otomatis Diaktifkan
 Sekarang kita memuat konten HTML lagi, tapi kali ini dengan`AutoFitColsAndRows`opsi diaktifkan. Ini akan menyesuaikan lebar kolom dan tinggi baris berdasarkan konten di dalamnya.
```csharp
wb = new Workbook(ms, opts);
wb.Save(dataDir + "outputWith_AutoFitColsAndRows.xlsx");
```
Langkah ini memuat konten HTML ke dalam buku kerja baru dan menyimpannya sebagai file Excel, tetapi sekarang kolom dan barisnya sudah disesuaikan secara otomatis! Bayangkan ini seperti kue yang dipanggang dengan sempurna, di mana semuanya berukuran pas.
## Kesimpulan
Dengan mengikuti langkah-langkah sederhana ini, Anda telah mempelajari cara memuat konten HTML ke dalam buku kerja menggunakan Aspose.Cells for .NET dan menyesuaikan kolom dan baris secara otomatis. Ini memastikan lembar Excel Anda selalu terlihat rapi, tidak peduli seberapa dinamis kontennya. Ini adalah fitur sederhana namun hebat yang dapat menghemat banyak waktu Anda dalam memformat dan mengatur data Excel Anda.
Sekarang setelah Anda dilengkapi dengan pengetahuan ini, Anda dapat bereksperimen dengan konten HTML yang lebih kompleks, menambahkan gaya, dan bahkan membuat seluruh buku kerja Excel dari halaman web!
## Pertanyaan yang Sering Diajukan
### Bisakah saya menggunakan metode ini untuk memuat tabel HTML yang besar?
Ya, Aspose.Cells menangani tabel HTML besar secara efisien, tetapi untuk kinerja optimal, disarankan untuk menguji dengan ukuran data Anda.
### Dapatkah saya menerapkan lebar kolom dan tinggi baris tertentu secara manual setelah penyesuaian otomatis?
Tentu saja! Anda masih dapat menyesuaikan kolom dan baris individual bahkan setelah menggunakan fitur penyesuaian otomatis.
### Bagaimana saya dapat memberi gaya pada tabel setelah memuat HTML?
Anda dapat menerapkan gaya menggunakan opsi gaya Aspose.Cells yang luas setelah memuat HTML.
### Apakah Aspose.Cells untuk .NET kompatibel dengan versi .NET Framework yang lebih lama?
Ya, Aspose.Cells untuk .NET mendukung .NET Framework 4.0 dan yang lebih baru.
### Bisakah saya memuat jenis konten lain selain HTML ke Excel menggunakan Aspose.Cells?
Ya, Aspose.Cells mendukung pemuatan berbagai format seperti CSV, JSON, dan XML ke dalam Excel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
