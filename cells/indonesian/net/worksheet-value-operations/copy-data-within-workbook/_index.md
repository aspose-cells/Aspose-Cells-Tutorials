---
title: Menyalin Data Dalam Buku Kerja menggunakan Aspose.Cells
linktitle: Menyalin Data Dalam Buku Kerja menggunakan Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menyalin data secara efisien dalam buku kerja Excel menggunakan Aspose.Cells untuk .NET dengan panduan langkah demi langkah, contoh kode, dan kiat bermanfaat.
weight: 12
url: /id/net/worksheet-value-operations/copy-data-within-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menyalin Data Dalam Buku Kerja menggunakan Aspose.Cells

## Perkenalan
Mengelola data dalam buku kerja Excel merupakan bagian inti dari banyak aplikasi. Bayangkan Anda memiliki templat atau lembar yang diisi dengan data penting, dan Anda ingin menduplikasinya dalam buku kerja yang sama untuk penggunaan lebih lanjut. Di sinilah Aspose.Cells untuk .NET bersinar! Dalam panduan ini, kami akan memandu Anda menyalin data dalam buku kerja yang sama, menggunakan Aspose.Cells, dengan tutorial langkah demi langkah yang mudah dipahami dan jelas.
## Prasyarat
Sebelum kita mulai coding, mari pastikan kita punya semua yang dibutuhkan untuk menyelesaikan tugas ini:
1.  Aspose.Cells untuk Pustaka .NET – Unduh versi terbaru dari[Halaman unduhan Aspose.Cells untuk .NET](https://releases.aspose.com/cells/net/).
2. Lingkungan Pengembangan – Anda memerlukan IDE yang kompatibel dengan .NET, seperti Visual Studio.
3.  Lisensi – Menggunakan uji coba gratis atau lisensi yang dibeli untuk Aspose.Cells. Anda bisa mendapatkan lisensi sementara[Di Sini](https://purchase.aspose.com/temporary-license/) atau jelajahi opsi pembelian[Di Sini](https://purchase.aspose.com/buy).
## Paket Impor
Dalam kode Anda, Anda perlu mengimpor Aspose.Cells untuk memanfaatkan kelas dan metodenya:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Mari selami kodenya! Kami akan menguraikan tugas menyalin data dalam buku kerja menggunakan Aspose.Cells for .NET menjadi langkah-langkah yang mudah diikuti.
## Langkah 1: Siapkan Jalur Direktori Anda
Sebelum kita mulai menangani buku kerja, mari kita tentukan di mana file kita berada dan di mana kita ingin menyimpan output. Menyiapkan jalur direktori akan membuat semuanya teratur.
```csharp
// Tetapkan jalur direktori untuk dokumen.
string dataDir = "Your Document Directory";
string inputPath = dataDir + "book1.xls";
```
 Di sini, ganti`"Your Document Directory"` dengan jalur sebenarnya tempat buku kerja Anda disimpan. Variabel jalur ini akan memudahkan untuk merujuk ke berkas masukan dan keluaran Anda.
## Langkah 2: Buka File Excel yang Ada
Untuk bekerja dengan file Excel, kita perlu memuatnya ke objek buku kerja di Aspose.Cells. Langkah ini akan membuka file yang ingin Anda salin datanya.
```csharp
// Buka berkas Excel yang ada.
Workbook wb = new Workbook(inputPath);
```
 Dengan ini, kami`Workbook` obyek`wb` sekarang siap untuk berinteraksi dengan konten`book1.xls`.
## Langkah 3: Akses Koleksi Lembar Kerja
 Sekarang buku kerja sudah terbuka, kita akan mengakses koleksi lembar kerjanya.`WorksheetCollection` Kelas membantu kita bekerja dengan beberapa lembar dalam buku kerja.
```csharp
// Buat objek Lembar Kerja yang mereferensikan semua lembar dalam buku kerja.
WorksheetCollection sheets = wb.Worksheets;
```
 Di Sini,`sheets` akan memungkinkan kita untuk memanipulasi setiap lembar dalam buku kerja, termasuk menambahkan salinan lembar yang sudah ada.
## Langkah 4: Salin Data ke Lembar Baru
Bagian utama dari tugas kita adalah menyalin isi dari satu lembar ke lembar baru dalam buku kerja yang sama. Dalam contoh ini, kita akan menyalin data dari "Sheet1" ke lembar baru.
```csharp
// Salin data dari "Sheet1" ke lembar baru dalam buku kerja.
sheets.AddCopy("Sheet1");
```
 Itu`AddCopy`metode membuat salinan persis dari lembar yang ditentukan, menambahkannya ke buku kerja. Di sini, kita menduplikasi "Sheet1." Anda dapat menentukan nama lembar mana pun yang ingin Anda salin.
## Langkah 5: Simpan Buku Kerja dengan Lembar Baru
Setelah menyalin lembar, simpan buku kerja dengan nama baru atau di lokasi baru untuk mempertahankan perubahan.
```csharp
// Simpan buku kerja dengan data yang disalin.
wb.Save(dataDir + "CopyWithinWorkbook_out.xls");
```
 Baris ini menyimpan buku kerja yang dimodifikasi sebagai`CopyWithinWorkbook_out.xls` di direktori yang ditentukan.
## Kesimpulan
Nah, itu dia! Menyalin data dalam buku kerja menggunakan Aspose.Cells untuk .NET sangat mudah. Aspose.Cells memudahkan penanganan file Excel dan memungkinkan Anda melakukan tugas manajemen data yang rumit dengan mudah. Baik Anda perlu menduplikasi lembar untuk penggunaan templat, pencadangan, atau membuat versi baru, langkah-langkah yang kami bahas akan membantu Anda mencapai tujuan.
 Jika Anda ingin menjelajah lebih jauh, lihatlah[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) untuk fitur dan kemampuan tingkat lanjut.
## Pertanyaan yang Sering Diajukan
### Bisakah saya menyalin beberapa lembar sekaligus?
Aspose.Cells tidak mendukung penyalinan beberapa lembar dalam satu panggilan, tetapi Anda dapat mengulang lembar yang ingin diduplikasi dan menyalinnya satu per satu.
### Bisakah saya mengganti nama lembar yang disalin?
 Ya, setelah menyalin lembar, Anda dapat mengganti namanya menggunakan`sheets[sheets.Count - 1].Name = "NewSheetName";`.
### Apakah Aspose.Cells kompatibel dengan .NET Core?
Tentu saja! Aspose.Cells mendukung lingkungan .NET Framework dan .NET Core.
### Bagaimana cara menangani pemformatan saat menyalin lembar?
 Itu`AddCopy` metode ini mempertahankan semua konten dan format, sehingga lembar yang Anda salin akan terlihat seperti aslinya.
### Bagaimana jika saya ingin menyalin lembar ke buku kerja lain?
Anda dapat menggunakan`Copy` metode dengan referensi ke buku kerja lain, seperti`sheets.Add().Copy(wb.Worksheets["Sheet1"]);`.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
