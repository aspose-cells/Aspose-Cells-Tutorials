---
title: Terapkan Freeze Panes di Lembar Kerja
linktitle: Terapkan Freeze Panes di Lembar Kerja
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menerapkan panel beku di Excel menggunakan Aspose.Cells untuk .NET dengan panduan terperinci langkah demi langkah ini. Tingkatkan kegunaan lembar kerja Anda secara efisien.
weight: 15
url: /id/net/worksheet-display/implement-freeze-panes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Terapkan Freeze Panes di Lembar Kerja

## Perkenalan
Bayangkan Anda memiliki lembar kerja Excel dengan kumpulan data yang sangat besar, dan setiap kali Anda menggulir ke bawah atau ke samping, Anda kehilangan jejak tajuk penting tersebut. Bukankah lebih nyaman jika tajuk tersebut dapat tetap berada di tempatnya saat Anda menggulir? Di sinilah panel beku berperan, membuat navigasi menjadi lancar dan efisien. Aspose.Cells untuk .NET menyederhanakan proses ini, memberi Anda kekuatan untuk menerapkan panel beku dengan lancar. Panduan ini akan memandu Anda melalui proses tersebut, menguraikannya langkah demi langkah sehingga Anda dapat menyiapkan tajuk beku tersebut dalam waktu singkat.
## Prasyarat
Sebelum memulai, pastikan Anda telah menyiapkan beberapa hal:
-  Pustaka Aspose.Cells untuk .NET: Anda perlu mengunduh pustaka ini dari[Halaman rilis Aspose](https://releases.aspose.com/cells/net/).
- .NET Framework Terpasang: Pastikan Anda telah menyiapkan .NET di lingkungan pengembangan Anda.
- Pengetahuan Dasar C#: Keakraban dengan C# akan membantu untuk diikuti.
- Berkas Excel: Siapkan berkas Excel (misalnya, “book1.xls”) yang akan Anda terapkan panel beku.
Anda dapat menjelajahi lebih detail tentang Aspose.Cells di[halaman dokumentasi](https://reference.aspose.com/cells/net/).

## Paket Impor
Mari kita mulai dengan mengimpor paket-paket yang diperlukan. Buka proyek C# Anda, dan pastikan untuk mengimpor paket-paket berikut:
```csharp
using System.IO;
using Aspose.Cells;
```
Setelah paket-paketnya siap, mari masuk ke panduan langkah demi langkah.
Kami akan membahas setiap tahap pengaturan panel pembekuan menggunakan Aspose.Cells untuk .NET. Ikuti setiap langkah dengan saksama, dan Anda akan memiliki panel pembekuan yang diterapkan ke lembar kerja Anda dengan mudah.
## Langkah 1: Tentukan Jalur ke Direktori Dokumen Anda
 Sebelum Anda dapat membuka file Excel, Anda harus menentukan jalur ke dokumen Anda. Siapkan`dataDir` variabel yang menampung jalur direktori untuk file Anda.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```
 Mengganti`"Your Document Directory"` dengan jalur sebenarnya tempat file Excel Anda disimpan. Ini akan membantu program menemukan file Anda.
## Langkah 2: Buka File Excel Menggunakan FileStream
Selanjutnya, kita perlu memuat berkas Excel agar Aspose.Cells dapat berfungsi sebagaimana mestinya. Untuk melakukannya, kita akan membuat aliran berkas dan membuka berkas Excel menggunakan aliran tersebut.
```csharp
// Membuat aliran file yang berisi file Excel yang akan dibuka
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
Dengan menggunakan aliran file, Anda membuka file agar Aspose.Cells dapat mengaksesnya tanpa mengubah file asli hingga Anda menyimpan perubahan apa pun secara eksplisit.
## Langkah 3: Buat Instansiasi Objek Buku Kerja
 Dengan aliran file yang sudah ada, sekarang saatnya untuk membuat`Workbook` objek. Objek ini penting karena mewakili seluruh buku kerja Excel Anda, yang memungkinkan Anda bekerja dengan lembar, sel, dan pengaturan individual dalam file tersebut.
```csharp
// Membuat instance objek Buku Kerja
// Membuka file Excel melalui aliran file
Workbook workbook = new Workbook(fstream);
```
 Pikirkanlah`Workbook` sebagai binder yang menyatukan semua lembar kerja Anda. Setelah Anda membuka binder, Anda dapat mengakses halaman (lembar kerja) mana pun di dalamnya.
## Langkah 4: Akses Lembar Kerja Pertama
Sekarang setelah buku kerja Anda dimuat, Anda dapat memilih lembar kerja mana yang akan diberi panel beku. Dalam contoh ini, kita akan bekerja dengan lembar pertama. Aspose.Cells memudahkan pemilihan lembar dengan pengindeksan.
```csharp
// Mengakses lembar kerja pertama dalam file Excel
Worksheet worksheet = workbook.Worksheets[0];
```
 Jika Anda perlu mengerjakan lembar yang berbeda, cukup sesuaikan indeks di`workbook.Worksheets[0]`.
## Langkah 5: Terapkan Pengaturan Freeze Panes
 Di sinilah keajaiban terjadi! Untuk mengatur panel beku, gunakan`FreezePanes`metode, menentukan baris dan kolom di mana Anda ingin pembekuan dimulai, serta berapa banyak baris dan kolom yang akan dibekukan.
```csharp
// Menerapkan pengaturan panel beku
worksheet.FreezePanes(3, 2, 3, 2);
```
Mari kita uraikan parameternya:
- Baris Pertama (3): Mulai beku di baris 3.
- Kolom Pertama (2): Mulai beku di kolom 2.
- Jumlah Baris (3): Bekukan 3 baris.
- Jumlah Kolom (2): Bekukan 2 kolom.
Sesuaikan nilai-nilai ini berdasarkan kebutuhan spesifik Anda. Titik beku akan berada di persimpangan baris dan kolom yang ditentukan.
## Langkah 6: Simpan File Excel yang Telah Dimodifikasi
 Setelah menerapkan panel beku, saatnya menyimpan perubahan Anda. Menyimpan file buku kerja yang dimodifikasi memastikan pengaturan beku Anda dipertahankan. Anda dapat menyimpan file yang diperbarui menggunakan`Save` metode.
```csharp
// Menyimpan file Excel yang dimodifikasi
workbook.Save(dataDir + "output.xls");
```
Pastikan untuk menyimpannya dengan nama yang berbeda jika Anda ingin mempertahankan berkas aslinya juga.
## Langkah 7: Tutup Aliran File
Terakhir, ingatlah untuk menutup aliran berkas. Ini akan membebaskan sumber daya sistem dan menyelesaikan semua koneksi terbuka ke berkas.
```csharp
// Menutup aliran file untuk membebaskan semua sumber daya
fstream.Close();
```
Anggaplah menutup aliran data seperti menaruh kembali berkas ke rak setelah Anda selesai menggunakannya. Ini adalah kebiasaan yang baik untuk menjaga kerapian.

## Kesimpulan
Selamat! Anda telah berhasil menerapkan panel beku ke lembar kerja Excel menggunakan Aspose.Cells for .NET. Teknik ini sangat berguna untuk mengelola kumpulan data besar, memastikan bahwa tajuk atau baris dan kolom tertentu tetap terlihat saat menggulir data. Dengan mengikuti panduan langkah demi langkah ini, Anda dapat dengan yakin menerapkan panel beku dan meningkatkan kegunaan lembar kerja Anda.
## Pertanyaan yang Sering Diajukan
### Bisakah saya membekukan lebih dari satu lembar dalam buku kerja?
 Ya, ulangi saja`FreezePanes` metode pada setiap lembar yang ingin Anda terapkan.
### Apa yang terjadi jika saya menggunakan nilai baris dan kolom yang melampaui rentang lembar?
Aspose.Cells akan memunculkan pengecualian, jadi pastikan nilai Anda berada dalam batas lembar kerja.
### Dapatkah saya menyesuaikan pengaturan panel beku setelah menerapkannya?
 Tentu saja! Hubungi saja`FreezePanes`metode lagi dengan parameter baru untuk memperbarui pengaturan.
### Apakah panel beku berfungsi pada semua versi file Excel?
Ya, panel beku akan dipertahankan di sebagian besar format Excel (misalnya, XLS, XLSX) yang didukung oleh Aspose.Cells.
### Bisakah saya mencairkan kaca tersebut?
 Untuk menghapus panel beku, cukup hubungi`UnfreezePanes()` pada lembar kerja.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
