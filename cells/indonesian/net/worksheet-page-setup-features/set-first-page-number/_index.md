---
title: Mengatur Nomor Halaman Pertama Lembar Kerja
linktitle: Mengatur Nomor Halaman Pertama Lembar Kerja
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengatur nomor halaman pertama di lembar kerja Excel menggunakan Aspose.Cells for .NET dengan panduan yang mudah diikuti ini. Petunjuk langkah demi langkah disertakan.
weight: 21
url: /id/net/worksheet-page-setup-features/set-first-page-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengatur Nomor Halaman Pertama Lembar Kerja

## Perkenalan
Menetapkan nomor halaman pertama dalam lembar kerja Excel dapat menjadi pengubah permainan jika Anda memformat halaman untuk dicetak atau membuat dokumen Anda tampak lebih profesional. Dalam tutorial ini, kami akan menguraikan cara menetapkan nomor halaman pertama lembar kerja menggunakan Aspose.Cells untuk .NET. Baik Anda memberi nomor halaman untuk referensi mudah atau menyelaraskan dengan dokumen yang lebih besar, Aspose.Cells menyediakan cara yang ampuh namun mudah untuk menyelesaikannya.
## Prasyarat
Sebelum kita mulai, pastikan Anda memiliki hal berikut:
-  Pustaka Aspose.Cells untuk .NET: Anda dapat mengunduh versi terbaru[Di Sini](https://releases.aspose.com/cells/net/).
- Lingkungan Pengembangan .NET: Visual Studio berfungsi dengan baik, tetapi editor apa pun yang kompatibel dengan .NET juga baik-baik saja.
- Pengetahuan Dasar C# dan Excel: Keakraban dengan penanganan file C# dan Excel akan sangat membantu.
 Untuk panduan pengaturan, lihat[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/).
## Paket Impor
Sebelum memulai, impor namespace Aspose.Cells yang diperlukan ke dalam proyek C# Anda untuk bekerja dengan pustaka tersebut:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Dalam panduan ini, kita akan membahas langkah-langkah pengaturan nomor halaman pertama lembar kerja di Excel menggunakan Aspose.Cells untuk .NET.
## Langkah 1: Tentukan Jalur Direktori
Agar penyimpanan berkas Anda lancar, mulailah dengan menetapkan jalur direktori tempat dokumen Anda akan disimpan. Ini akan memudahkan Anda menemukan dan mengatur berkas keluaran Anda.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```
 Di sini, ganti`"Your Document Directory"` dengan jalur sebenarnya yang ingin Anda gunakan. Variabel ini akan membantu dalam merujuk lokasi untuk menyimpan berkas keluaran akhir.
## Langkah 2: Inisialisasi Objek Buku Kerja
 Sekarang, buat instance baru dari`Workbook` class. Anggap ini sebagai wadah inti berkas Excel Anda. Objek ini mewakili seluruh buku kerja, tempat setiap lembar, sel, dan pengaturan disimpan.
```csharp
// Membuat instance objek Buku Kerja
Workbook workbook = new Workbook();
```
 Dengan membuat sebuah`Workbook`, Anda sedang menyiapkan panggung untuk semua penyesuaian terkait Excel.
## Langkah 3: Akses Lembar Kerja
Buku kerja dapat berisi beberapa lembar kerja. Untuk mengatur nomor halaman pada lembar kerja tertentu, akses lembar kerja pertama dengan menargetkan indeks`0`Ini memungkinkan Anda mengonfigurasi lembar dalam buku kerja.
```csharp
// Mengakses lembar kerja pertama dalam file Excel
Worksheet worksheet = workbook.Worksheets[0];
```
 Jika buku kerja Anda berisi beberapa lembar, Anda dapat mengakses masing-masing lembar dengan mengubah indeksnya. Misalnya,`workbook.Worksheets[1]` akan mengakses lembar kerja kedua.
## Langkah 4: Tetapkan Nomor Halaman Pertama
Sekarang tibalah pada langkah inti—menetapkan nomor halaman pertama. Secara default, Excel memulai penomoran halaman pada angka 1, tetapi Anda dapat menyesuaikannya untuk memulai pada angka berapa pun. Ini sangat berguna jika Anda melanjutkan urutan dari dokumen lain.
```csharp
// Mengatur nomor halaman pertama dari halaman lembar kerja
worksheet.PageSetup.FirstPageNumber = 2;
```
Dalam contoh ini, nomor halaman akan dimulai dari 2 saat Anda mencetak dokumen. Anda dapat mengaturnya ke bilangan bulat apa pun yang sesuai dengan kebutuhan Anda.
## Langkah 5: Simpan Buku Kerja
Langkah terakhir adalah menyimpan buku kerja Anda dengan pengaturan yang telah dimodifikasi. Tentukan format file dan jalurnya sehingga Anda dapat meninjau perubahan Anda di Excel.
```csharp
// Simpan Buku Kerja.
workbook.Save(dataDir + "SetFirstPageNumber_out.xls");
```
 Di Sini,`"SetFirstPageNumber_out.xls"`adalah nama berkas keluaran. Anda dapat mengganti namanya sesuai keinginan. Setelah disimpan, buka berkas di Excel untuk melihat penomoran halaman yang diperbarui.
## Kesimpulan
Menetapkan nomor halaman pertama lembar kerja Excel menggunakan Aspose.Cells for .NET mudah, terutama jika Anda menguraikannya langkah demi langkah. Hanya dengan beberapa baris kode, Anda dapat mengontrol penomoran halaman untuk meningkatkan profesionalisme dan keterbacaan dokumen Anda. Fitur ini sangat berguna untuk laporan cetak, presentasi formal, dan banyak lagi.
## Pertanyaan yang Sering Diajukan
### Bisakah saya menetapkan nomor halaman pertama ke nilai apa pun?  
Ya, Anda dapat mengatur nomor halaman pertama ke bilangan bulat apa pun, bergantung pada kebutuhan Anda.
### Apa yang terjadi jika saya tidak menetapkan nomor halaman pertama?  
Jika tidak ditentukan, Excel secara default memulai nomor halaman pada 1.
### Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells?  
 Ya, untuk fungsionalitas penuh dalam lingkungan produksi, Anda memerlukan lisensi. Anda dapat[dapatkan uji coba gratis](https://releases.aspose.com/) atau[beli satu disini](https://purchase.aspose.com/buy).
### Apakah metode ini berfungsi dengan properti lembar kerja lainnya?  
Ya, Aspose.Cells memungkinkan Anda mengontrol berbagai properti lembar kerja seperti header, footer, dan margin.
### Di mana saya dapat menemukan dokumentasi lebih lanjut tentang Aspose.Cells?  
 Untuk panduan terperinci dan referensi API, kunjungi[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
