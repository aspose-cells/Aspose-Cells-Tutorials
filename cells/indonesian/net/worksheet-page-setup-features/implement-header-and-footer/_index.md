---
title: Menerapkan Header dan Footer di Lembar Kerja
linktitle: Menerapkan Header dan Footer di Lembar Kerja
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengatur header dan footer di lembar kerja Excel menggunakan Aspose.Cells untuk .NET dengan tutorial langkah demi langkah, contoh praktis, dan kiat bermanfaat.
weight: 22
url: /id/net/worksheet-page-setup-features/implement-header-and-footer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menerapkan Header dan Footer di Lembar Kerja

## Perkenalan

Saat bekerja dengan lembar kerja Excel, header dan footer memainkan peran penting dalam menyampaikan informasi kontekstual penting, seperti nama file, tanggal, atau nomor halaman, kepada audiens Anda. Baik Anda mengotomatiskan laporan atau membuat file dinamis, Aspose.Cells for .NET memudahkan Anda untuk menyesuaikan header dan footer di lembar kerja secara terprogram. Panduan ini membahas pendekatan langkah demi langkah yang komprehensif untuk menambahkan header dan footer dengan Aspose.Cells for .NET, yang memberikan file Excel Anda polesan dan profesionalisme ekstra.

## Prasyarat

Sebelum memulai, pastikan Anda telah menyiapkan hal-hal berikut:

1.  Aspose.Cells untuk .NET: Anda perlu menginstal Aspose.Cells untuk .NET.[Unduh di sini](https://releases.aspose.com/cells/net/).
2. Pengaturan IDE: Visual Studio (atau IDE pilihan Anda) dengan kerangka kerja .NET terpasang.
3.  Lisensi: Meskipun Anda dapat memulai dengan uji coba gratis, memperoleh lisensi penuh atau sementara akan membuka potensi penuh Aspose.Cells.[Dapatkan lisensi sementara](https://purchase.aspose.com/temporary-license/).

Dokumentasi untuk Aspose.Cells merupakan sumber referensi yang berguna selama proses ini. Anda dapat menemukannya[Di Sini](https://reference.aspose.com/cells/net/).

## Mengimpor Paket

Dalam proyek Anda, impor namespace yang diperlukan:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Dengan mengimpor paket ini, Anda akan memiliki akses ke kelas dan metode yang diperlukan untuk bekerja dengan header, footer, dan fungsi Excel lainnya dalam Aspose.Cells.

Dalam panduan ini, kami akan menguraikan setiap langkah sehingga Anda dapat dengan mudah mengikutinya, bahkan jika Anda baru mengenal Aspose.Cells atau .NET.

## Langkah 1: Siapkan Buku Kerja dan Pengaturan Halaman Anda

Hal pertama yang harus dilakukan: buat buku kerja baru dan akses pengaturan halaman lembar kerja. Ini akan memberi Anda alat yang Anda perlukan untuk mengubah header dan footer untuk lembar kerja.

```csharp
// Tentukan jalur untuk menyimpan dokumen Anda
string dataDir = "Your Document Directory";

// Membuat instance objek Buku Kerja
Workbook excel = new Workbook();
```

 Di sini, kami telah membuat`Workbook` objek, yang mewakili file Excel kita.`PageSetup` lembar kerja adalah tempat kita dapat memodifikasi opsi header dan footer.


## Langkah 2: Mengakses Properti Lembar Kerja dan PageSetup

 Di Aspose.Cells, setiap lembar kerja memiliki`PageSetup`properti yang mengontrol fitur tata letak, termasuk header dan footer. Mari kita dapatkan`PageSetup` objek untuk lembar kerja kita.

```csharp
// Dapatkan referensi ke PageSetup dari lembar kerja pertama
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

 Dengan ini,`pageSetup` sekarang berisi semua pengaturan yang diperlukan untuk menyesuaikan header dan footer.


## Langkah 3: Mengatur Bagian Kiri Header

Header di Excel dibagi menjadi tiga bagian: kiri, tengah, dan kanan. Mari kita mulai dengan mengatur bagian kiri untuk menampilkan nama lembar kerja.

```csharp
// Tetapkan nama lembar kerja di bagian kiri header
pageSetup.SetHeader(0, "&A");
```

 Menggunakan`&A` memungkinkan Anda menampilkan nama lembar kerja secara dinamis. Ini sangat membantu jika Anda memiliki beberapa lembar dalam buku kerja dan ingin setiap tajuk mencerminkan judul lembarnya.


## Langkah 4: Tambahkan Tanggal dan Waktu ke Tengah Header

Selanjutnya, mari tambahkan tanggal dan waktu saat ini ke bagian tengah header. Selain itu, kita akan menggunakan font khusus untuk penataan gaya.

```csharp
// Atur tanggal dan waktu di bagian tengah header dengan font tebal
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

Dalam kode ini:
- `&D`memasukkan tanggal saat ini.
- `&T` memasukkan waktu saat ini.
- `"Times New Roman,Bold"` menerapkan Times New Roman yang dicetak tebal pada elemen-elemen ini.


## Langkah 5: Menampilkan Nama File di Bagian Kanan Header

Untuk melengkapi header, mari tampilkan nama berkas di sisi kanan, disertai penyesuaian font.

```csharp
// Menampilkan nama file di bagian kanan header dengan ukuran font khusus
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

- `&F` melambangkan nama berkas, sehingga jelas berkas mana yang memuat halaman yang dicetak.
- `&12` mengubah ukuran font menjadi 12 untuk bagian ini.


## Langkah 6: Tambahkan Teks dengan Font Kustom ke Bagian Footer Kiri

Beralih ke footer! Kita akan mulai dengan menyiapkan bagian footer kiri dengan teks khusus dan gaya font tertentu.

```csharp
// Tambahkan teks khusus dengan gaya font ke bagian kiri footer
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

 Itu`&\"Courier New\"&14` pengaturan pada kode di atas menerapkan font "Courier New" dengan ukuran 14 ke teks yang ditentukan (`123`). Sisa teks tetap menggunakan font footer default.


## Langkah 7: Masukkan Nomor Halaman di Tengah Footer

Menyertakan nomor halaman di bagian bawah merupakan cara yang bagus untuk membantu pembaca melacak dokumen yang memiliki banyak halaman.

```csharp
// Masukkan nomor halaman di bagian tengah footer
pageSetup.SetFooter(1, "&P");
```

 Di Sini,`&P` menambahkan nomor halaman saat ini ke bagian tengah footer. Ini detail kecil, tetapi penting untuk dokumen yang tampak profesional.


## Langkah 8: Tampilkan Jumlah Halaman Total di Bagian Footer Kanan

Terakhir, mari lengkapi footer dengan menampilkan jumlah halaman total di bagian kanan.

```csharp
// Menampilkan jumlah halaman total di bagian kanan footer
pageSetup.SetFooter(2, "&N");
```

- `&N` menyediakan jumlah halaman total, yang memberi tahu pembaca seberapa panjang dokumen tersebut.


## Langkah 9: Simpan Buku Kerja

Setelah Anda menyiapkan header dan footer, saatnya menyimpan buku kerja. Ini adalah langkah terakhir untuk membuat file Excel dengan header dan footer yang sepenuhnya disesuaikan.

```csharp
// Simpan Buku Kerja
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

Baris ini menyimpan berkas ke direktori yang Anda tentukan dengan header dan footer khusus yang sudah ada.


## Kesimpulan

Menambahkan header dan footer ke lembar kerja Excel merupakan keterampilan yang berharga untuk membuat dokumen yang terorganisasi dan profesional. Dengan Aspose.Cells for .NET, Anda memiliki kendali penuh atas header dan footer file Excel Anda, mulai dari menampilkan nama lembar kerja hingga memasukkan teks kustom, tanggal, waktu, dan bahkan nomor halaman dinamis. Sekarang setelah Anda melihat setiap langkah dalam tindakan, Anda dapat membawa otomatisasi Excel Anda ke tingkat berikutnya.

## Pertanyaan yang Sering Diajukan

### Dapatkah saya menggunakan font yang berbeda untuk bagian header dan footer yang berbeda?  
Ya, Aspose.Cells untuk .NET memungkinkan Anda menentukan font untuk setiap bagian header dan footer menggunakan tag font tertentu.

### Bagaimana cara menghapus header dan footer?  
 Anda dapat menghapus header dan footer dengan mengatur teks header atau footer ke string kosong dengan`SetHeader` atau`SetFooter`.

### Bisakah saya menyisipkan gambar ke dalam header atau footer dengan Aspose.Cells untuk .NET?  
Saat ini, Aspose.Cells terutama mendukung teks di header dan footer. Gambar mungkin memerlukan solusi, seperti memasukkan gambar ke dalam lembar kerja itu sendiri.

### Apakah Aspose.Cells mendukung data dinamis dalam header dan footer?  
 Ya, Anda dapat menggunakan berbagai kode dinamis (seperti`&D` untuk tanggal atau`&P` untuk nomor halaman) untuk menambahkan konten dinamis.

### Bagaimana cara menyesuaikan tinggi header atau footer?  
 Aspose.Cells menyediakan opsi dalam`PageSetup` kelas untuk menyesuaikan margin header dan footer, memberi Anda kendali atas spasi.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
