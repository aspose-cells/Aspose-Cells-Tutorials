---
title: Membagi Panel Lembar Kerja
linktitle: Membagi Panel Lembar Kerja
second_title: Referensi API Aspose.Cells untuk .NET
description: Pelajari cara membagi panel lembar kerja di Aspose.Cells untuk .NET dengan panduan langkah demi langkah kami. Tingkatkan navigasi file Excel dengan tutorial mudah ini.
weight: 130
url: /id/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membagi Panel Lembar Kerja

## Perkenalan

Apakah Anda siap untuk membagi panel lembar kerja Excel menggunakan Aspose.Cells untuk .NET? Bayangkan ini: Anda memiliki lembar Excel yang sangat besar, dan Anda lelah terus-menerus menggulir kembali ke tajuk hanya untuk mengingat kolom mana yang sedang Anda kerjakan. Masukkan "Split Panes." Fitur praktis ini memungkinkan Anda untuk membekukan sebagian lembar kerja Anda, sehingga lebih mudah dinavigasi. Baik Anda bekerja dengan data keuangan, manajemen inventaris, atau kumpulan data besar, membagi panel dapat meningkatkan produktivitas Anda sepuluh kali lipat. 

## Prasyarat

Sebelum kita mulai membagi panel seperti panduan spreadsheet, mari kita atur pengaturan kita dengan benar. Berikut ini yang Anda perlukan:

-  Aspose.Cells untuk .NET: Pastikan Anda telah mengunduh dan menginstalnya. Jika belum, unduh dan instal[Di Sini](https://releases.aspose.com/cells/net/).
- .NET Framework: Panduan ini mengasumsikan Anda bekerja di lingkungan .NET.
- Buku Kerja Excel: Kami akan menggunakan contoh file Excel untuk menunjukkan cara kerja fitur ini.
-  Lisensi Sementara atau Penuh: Aspose.Cells memerlukan lisensi. Jika Anda baru mencobanya, dapatkan lisensi[lisensi sementara gratis](https://purchase.aspose.com/temporary-license/) untuk menghindari keterbatasan evaluasi.

## Paket Impor

Sebelum kita mulai membuat kode, mari impor namespace yang diperlukan terlebih dahulu. Anda tidak dapat melakukan apa pun di Aspose.Cells tanpa menyertakan namespace ini.

```csharp
using System.IO;
using Aspose.Cells;
```

Setelah kita bahas hal-hal penting, mari kita lanjut ke bagian yang menarik—membagi panel!

## Langkah 1: Buat Instansiasi Buku Kerja

 Langkah pertama dalam proses ini adalah membuat`Workbook` objek, yang akan mewakili berkas Excel yang ingin Anda ubah. Dalam kasus ini, kita akan memuat berkas dari direktori. Ini adalah kanvas Anda, lembar Excel tempat Anda akan melakukan keajaiban.

Sebelum kita dapat membagi panel, kita memerlukan buku kerja untuk bekerja! Langkah ini sama pentingnya dengan membuka buku sebelum Anda mulai membacanya.

```csharp
// Jalur ke direktori dokumen
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Buat buku kerja baru dan buka file templat
Workbook book = new Workbook(dataDir + "Book1.xls");
```

 Pada kode di atas, ganti`"YOUR DOCUMENT DIRECTORY"` dengan jalur sebenarnya tempat file Excel Anda berada.`Workbook`kelas memuat berkas Excel ke dalam memori.

## Langkah 2: Mengatur Sel Aktif

 Setelah memuat buku kerja, saatnya untuk mengatur sel aktif. Dalam istilah Excel, sel aktif adalah sel yang saat ini dipilih atau menjadi fokus. Dalam tutorial ini, kita akan memilih sel`A20` pada lembar kerja pertama.

Menetapkan sel aktif sangat penting karena pemisahan panel dimulai dari sel aktif ini. Ini seperti memilih tempat untuk membuat potongan pertama pada pizza—pilih potongan Anda!

```csharp
// Mengatur sel aktif
book.Worksheets[0].ActiveCell = "A20";
```

 Potongan kode ini membuat`A20` sel yang aktif. Hal ini penting karena pemisahan terjadi di sekitar titik ini, seperti halnya navigasi di Excel yang sering kali berpusat di sekitar sel tertentu.

## Langkah 3: Membagi Lembar Kerja

Sekarang sel aktif sudah ditetapkan, mari beralih ke bagian yang menyenangkan—membagi lembar kerja! Langkah ini adalah tempat keajaiban terjadi. Anda akan dapat membagi lembar kerja menjadi beberapa panel untuk memudahkan tampilan dan navigasi.

Inilah inti dari keseluruhan tutorial. Dengan membagi lembar kerja, Anda membuat panel terpisah yang memungkinkan Anda menggulir berbagai bagian lembar Excel tanpa kehilangan tajuk atau area penting lainnya.

```csharp
// Membagi jendela lembar kerja
book.Worksheets[0].Split();
```

 Dengan`Split()` metode, Anda memberi tahu Aspose.Cells untuk membagi lembar kerja di sel aktif (`A20` dalam kasus ini). Dari titik ini, Excel membuat pembagian pada lembar yang memisahkan panel agar Anda dapat menavigasi secara independen.

## Langkah 4: Simpan Buku Kerja

Setelah membagi panel, yang tersisa hanyalah menyimpan pekerjaan Anda. Langkah terakhir ini akan memastikan bahwa perubahan Anda disimpan dalam berkas keluaran yang ditentukan.

Apa gunanya semua kerja keras Anda jika Anda tidak menyimpannya? Menyimpannya memastikan bahwa kaca yang Anda bagi dengan indah tetap utuh untuk penggunaan di masa mendatang.

```csharp
// Simpan file Excel
book.Save(dataDir + "output.xls");
```

 Di sini,`Save()` metode menyimpan buku kerja dengan panel yang baru Anda bagi menjadi file Excel keluaran. Perubahan yang Anda buat kini siap untuk Anda—atau orang lain—gunakan.

## Kesimpulan

Nah, itu dia! Anda baru saja mempelajari cara membagi panel dalam lembar kerja Excel menggunakan Aspose.Cells for .NET. Tidak ada lagi pengguliran tanpa henti atau kehilangan jejak data Anda. Metode ini membuat penanganan file Excel yang besar jauh lebih mudah dan jauh lebih efisien. Dengan kemampuan untuk membagi panel, kini Anda dapat melacak titik data penting saat bekerja dengan lembar kerja yang rumit.

## Pertanyaan yang Sering Diajukan

### Bisakah saya membagi lebih dari dua panel?  
 Ya, Anda dapat membagi lembar kerja menjadi beberapa panel dengan menentukan sel aktif yang berbeda dan memanggil`Split()` metode.

### Apa perbedaan antara panel terpisah dan panel beku?  
Memisahkan panel memungkinkan Anda untuk menggulir di kedua panel secara terpisah. Membekukan panel akan mengunci tajuk atau baris/kolom tertentu sehingga tetap terlihat saat menggulir.

### Bisakah saya menghilangkan bagian yang terbelah setelah mengaplikasikannya?  
Ya, Anda dapat menghapus pemisahan tersebut dengan menutup dan membuka kembali buku kerja atau mengatur ulang secara terprogram.

### Apakah pemisahan panel berfungsi sama untuk format file Excel yang berbeda (XLS, XLSX)?  
 Ya, itu`Split()` Metode ini berfungsi untuk format XLS dan XLSX.

### Bisakah saya menggunakan Aspose.Cells tanpa lisensi?  
 Ya, tetapi ada batasannya. Untuk pengalaman yang lengkap, sebaiknya gunakan[sementara](https://purchase.aspose.com/temporary-license/) atau[lisensi berbayar](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
