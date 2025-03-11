---
title: Salin Lembar Kerja Excel Antar Buku Kerja
linktitle: Salin Lembar Kerja Excel Antar Buku Kerja
second_title: Referensi API Aspose.Cells untuk .NET
description: Pelajari cara menyalin lembar kerja antar buku kerja Excel menggunakan Aspose.Cells untuk .NET. Panduan langkah demi langkah dengan contoh kode untuk menyederhanakan pengelolaan lembar kerja Anda.
weight: 30
url: /id/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salin Lembar Kerja Excel Antar Buku Kerja

## Perkenalan

Pernahkah Anda menyalin lembar kerja antar-buku kerja Excel secara manual? Ini seperti mencoba melakukan juggling sambil mengendarai sepeda roda satu! Namun dengan Aspose.Cells for .NET, Anda dapat menyederhanakan tugas ini dan membuatnya semudah mengiris mentega. Baik Anda mengelola set data besar atau perlu menggabungkan informasi, menyalin lembar kerja antar-buku kerja dapat menghemat banyak waktu. Dalam tutorial ini, kami akan menunjukkan kepada Anda cara melakukannya dengan tepat menggunakan Aspose.Cells for .NET. Di akhir panduan ini, Anda akan dapat menyelesaikan tugas Excel dengan mudah.

## Prasyarat

Sebelum kita menyelami kodenya, mari pastikan Anda dilengkapi dengan alat yang tepat untuk memulai:

-  Aspose.Cells untuk .NET: Anda dapat mengunduhnya[Di Sini](https://releases.aspose.com/cells/net/).
- Visual Studio atau IDE apa pun yang mendukung kerangka kerja .NET.
-  Lisensi yang valid atau[lisensi sementara](https://purchase.aspose.com/temporary-license/)jika Anda ingin menguji fungsionalitas penuh Aspose.Cells.
- Pemahaman dasar tentang C# dan kerangka kerja .NET.

 Anda juga dapat memeriksa[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) untuk rincian lebih lanjut.

## Paket Impor

Sebelum Anda dapat mulai membuat kode, Anda perlu mengimpor paket-paket yang diperlukan. Ini seperti mengepak tas sebelum melakukan perjalanan – Anda memerlukan peralatan yang tepat agar perjalanan berjalan lancar.

```csharp
using Aspose.Cells;
```

Baris kode sederhana ini mengimpor pustaka Aspose.Cells, yang merupakan gerbang Anda ke semua keajaiban Excel yang akan kita kerjakan.


Setelah semuanya siap, mari kita bahas proses menyalin lembar kerja antar-buku kerja Excel. Setiap langkah dijabarkan agar mudah dipahami. Jadi, meskipun Anda baru mengenal Aspose.Cells, Anda akan dapat mengikutinya.

## Langkah 1: Siapkan Direktori Dokumen

Pertama, Anda perlu menentukan lokasi file Anda. Anggap langkah ini seperti memilih peta untuk perburuan harta karun Anda – peta ini memberi tahu kode tempat menemukan dan menyimpan buku kerja Anda.

```csharp
// Jalur ke direktori dokumen.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

 Pada baris ini, ganti`"YOUR DOCUMENT DIRECTORY"`dengan jalur sebenarnya ke berkas Excel Anda. Di sinilah buku kerja Anda akan dimuat dan disimpan.

## Langkah 2: Buka Buku Kerja Pertama

Berikutnya, Anda akan membuka buku kerja pertama, yang berisi lembar kerja yang ingin Anda salin. Bayangkan ini seperti membuka folder untuk mengambil selembar kertas.

```csharp
string InputPath = dataDir + "book1.xls";
// Membuat Buku Kerja.
// Buka berkas ke dalam buku pertama.
Workbook excelWorkbook0 = new Workbook(InputPath);
```

 Di sini, Anda sedang memuat`book1.xls` (pastikan file tersebut ada di direktori Anda) ke dalam direktori baru`Workbook` objek yang disebut`excelWorkbook0`Ini adalah buku kerja sumber yang menampung lembar kerja yang akan Anda salin.

## Langkah 3: Buat Buku Kerja Kedua

Sekarang setelah Anda membuka buku kerja pertama, saatnya membuat buku kerja kosong lain tempat Anda akan menempelkan lembar kerja yang disalin. Anggap saja ini seperti membuka buku catatan kosong baru tempat Anda akan mentransfer data.

```csharp
// Buat Buku Kerja lainnya.
Workbook excelWorkbook1 = new Workbook();
```

 Baris ini membuat buku kerja kosong bernama`excelWorkbook1`Di sinilah lembar kerja yang disalin akan berada setelah Anda memindahkannya dari buku kerja pertama.

## Langkah 4: Salin Lembar Kerja

Di sinilah keajaibannya! Pada langkah ini, Anda akan menyalin lembar kerja dari buku kerja pertama ke buku kerja kedua. Ini seperti memindahkan catatan dari satu buku catatan ke buku catatan lainnya.

```csharp
// Salin lembar pertama buku pertama ke buku kedua.
excelWorkbook1.Worksheets[0].Copy(excelWorkbook0.Worksheets[0]);
```

 Apa yang terjadi di sini? Kode mengambil lembar kerja pertama dari`excelWorkbook0` dan menyalinnya ke lembar pertama`excelWorkbook1`Sangat mudah, bukan?

## Langkah 5: Simpan Buku Kerja Baru

Terakhir, Anda akan menyimpan buku kerja kedua dengan lembar kerja yang disalin. Ini seperti menyimpan catatan yang baru Anda tulis di folder baru di komputer Anda.

```csharp
// Simpan berkasnya.
excelWorkbook1.Save(dataDir + "CopyWorksheetsBetweenWorkbooks_out.xls");
```

 Ini menyimpan buku kerja kedua dengan lembar kerja yang disalin ke file baru bernama`CopyWorksheetsBetweenWorkbooks_out.xls`Jangan ragu untuk mengubah nama sesuai keinginan Anda!

## Kesimpulan

Selesai! Anda telah berhasil menyalin lembar kerja dari satu buku kerja Excel ke buku kerja lain menggunakan Aspose.Cells untuk .NET. Proses ini mudah dan tidak perlu menyalin-menempel secara manual, terutama saat bekerja dengan lembar kerja yang rumit atau besar. Aspose.Cells untuk .NET adalah alat canggih yang memungkinkan Anda memanipulasi file Excel dengan mudah, baik saat menyalin lembar kerja, menggabungkan buku kerja, atau melakukan tugas yang lebih rumit.

Ingat, pengodean menjadi lebih mudah jika dipecah menjadi beberapa langkah kecil. Jadi, lain kali Anda perlu mengelola berkas Excel, Anda akan siap menanganinya seperti seorang profesional.

## Pertanyaan yang Sering Diajukan

### Bisakah saya menyalin beberapa lembar kerja sekaligus?

 Ya, Anda dapat mengulang lembar kerja di buku kerja sumber dan menyalinnya ke buku kerja tujuan. Setiap lembar kerja memiliki caranya sendiri.`Copy` metode.

### Bisakah saya menyalin lembar kerja ke buku kerja yang sudah memiliki data?

Tentu saja! Anda dapat menyalin lembar kerja ke buku kerja mana pun yang sudah ada, meskipun buku kerja tersebut sudah berisi data. Cukup tentukan indeks lembar kerja yang benar.

### Apakah saya memerlukan lisensi berbayar untuk fungsi ini?

 Meskipun Anda dapat menggunakan versi gratis Aspose.Cells untuk fungsionalitas dasar, disarankan untuk mendapatkan[lisensi sementara](https://purchase.aspose.com/temporary-license/) atau lisensi berbayar untuk fitur lengkap dan menghindari batasan seperti tanda air.

### Bisakah saya menyalin lembar kerja dengan bagan dan gambar?

Ya! Aspose.Cells sepenuhnya mendukung penyalinan lembar kerja yang berisi bagan, gambar, dan objek lainnya. Semuanya akan dipertahankan selama proses penyalinan.

### Bagaimana cara menyalin lembar kerja ke posisi tertentu di buku kerja baru?

 Anda dapat menentukan indeks tempat lembar kerja yang disalin harus ditempatkan menggunakan`Worksheets.AddCopy` metode yang memungkinkan kontrol lebih besar terhadap di mana lembaran itu ditempatkan.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
