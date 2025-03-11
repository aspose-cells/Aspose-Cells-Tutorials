---
title: Pratinjau Jeda Halaman Lembar Kerja
linktitle: Pratinjau Jeda Halaman Lembar Kerja
second_title: Referensi API Aspose.Cells untuk .NET
description: Pelajari cara menggunakan Aspose.Cells untuk .NET untuk mengaktifkan pratinjau hentian halaman di lembar kerja Excel melalui tutorial langkah demi langkah yang sederhana.
weight: 110
url: /id/net/excel-display-settings-csharp-tutorials/page-break-preview-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pratinjau Jeda Halaman Lembar Kerja

## Perkenalan

Membuat dan mengelola file Excel secara terprogram bisa sangat merepotkan jika Anda tidak memiliki alat yang tepat. Salah satu alat yang telah mendapatkan banyak perhatian di kalangan pengembang adalah Aspose.Cells for .NET. API yang canggih ini memungkinkan Anda untuk memanipulasi file Excel dengan lancar sekaligus menawarkan banyak fitur yang dapat membantu Anda mengoptimalkan alur kerja—seperti menyesuaikan pemisah halaman untuk tata letak cetak yang lebih baik. Dalam tutorial ini, kita akan membahas cara mengaktifkan pratinjau pemisah halaman dalam lembar kerja menggunakan Aspose.Cells for .NET.

## Prasyarat

Sebelum kita memulai, ada beberapa prasyarat yang harus Anda penuhi:

1. Pengetahuan Dasar C#: Pemahaman mendasar tentang C# dan kerangka kerja .NET tentu akan membantu Anda menavigasi tutorial ini.
2.  Aspose.Cells untuk .NET Terpasang: Anda perlu memiliki pustaka Aspose.Cells untuk .NET. Anda dapat[unduh dari sini](https://releases.aspose.com/cells/net/).
3. Visual Studio atau IDE Serupa: Anda memerlukan lingkungan pengembangan terintegrasi (IDE) seperti Visual Studio untuk menulis dan mengeksekusi kode.
4. File Excel: Anda harus memiliki file Excel (seperti`book1.xls`) tersedia di direktori dokumen Anda untuk manipulasi.
5. Ruang nama: Pastikan Anda telah menyertakan ruang nama yang diperlukan dalam kode Anda—khususnya untuk menangani berkas dan pustaka Aspose.Cells.

Sekarang setelah kita membahas prasyaratnya, mari masuk ke pengkodean sebenarnya.

## Paket Impor

Untuk memulai Aspose.Cells di proyek C# Anda, Anda perlu mengimpor paket yang diperlukan. Ini dapat dilakukan dengan menambahkan referensi ke proyek Anda.

### Sertakan Ruang Nama yang Diperlukan

Pertama, pastikan Anda telah menyertakan namespace berikut di bagian atas file C# Anda:

```csharp
using System.IO;
using Aspose.Cells;
```

### Buat File C# Baru

Buka Visual Studio atau IDE Anda dan buat file C# baru jika Anda belum melakukannya. Di sinilah kita akan menulis kode implementasi kita.


Sekarang, mari kita uraikan kode untuk mengaktifkan pratinjau hentian halaman di file Excel selangkah demi selangkah.

## Langkah 1: Tetapkan Jalur Direktori

```csharp
// Jalur ke direktori dokumen.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

 Pada langkah ini, Anda perlu mengganti`"YOUR DOCUMENT DIRECTORY"`dengan jalur sebenarnya ke folder proyek tempat file Excel Anda disimpan. Ini penting karena memberi tahu program tempat mencari file yang ingin Anda manipulasi.

## Langkah 2: Buat Aliran File

```csharp
// Membuat aliran file yang berisi file Excel yang akan dibuka
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```

 Di sini, kita membuat`FileStream` objek yang menunjuk ke file Excel yang ditentukan (`book1.xls`). Ini memungkinkan aplikasi Anda untuk membuka dan memanipulasi berkas tersebut.

## Langkah 3: Buat Instansiasi Buku Kerja

```csharp
// Membuat instance objek Buku Kerja
// Membuka file Excel melalui aliran file
Workbook workbook = new Workbook(fstream);
```

 Pada langkah ini, Anda membuat instance`Workbook` objek yang mewakili berkas Excel. Objek ini pada dasarnya adalah inti dari operasi Anda, yang memungkinkan Anda mengakses semua lembar kerja dan melakukan berbagai manipulasi.

## Langkah 4: Akses Lembar Kerja

```csharp
// Mengakses lembar kerja pertama dalam file Excel
Worksheet worksheet = workbook.Worksheets[0];
```

Di sini, kita mengakses lembar kerja pertama di buku kerja Anda menggunakan indeksnya (berbasis nol). Jika Anda memiliki beberapa lembar, Anda dapat mengakses lembar kerja lainnya dengan mengubah indeks.

## Langkah 5: Aktifkan Pratinjau Hentian Halaman

```csharp
// Menampilkan lembar kerja dalam pratinjau hentian halaman
worksheet.IsPageBreakPreview = true;
```

Langkah penting ini mengaktifkan mode pratinjau pemisah halaman untuk lembar kerja. Anda akan melihat bagaimana ini memengaruhi tata letak dan format cetak saat Anda membuka file nanti.

## Langkah 6: Simpan Buku Kerja

```csharp
// Menyimpan file Excel yang dimodifikasi
workbook.Save(dataDir + "output.xls");
```

Setelah melakukan perubahan, penting untuk menyimpan buku kerja. Di sini, kita menyimpannya sebagai`output.xls`, namun jangan ragu untuk mengubah nama berkas sesuai kebutuhan.

## Langkah 7: Bersihkan Sumber Daya

```csharp
// Menutup aliran file untuk membebaskan semua sumber daya
fstream.Close();
```

Terakhir, membersihkan sumber daya merupakan kebiasaan yang baik. Menutup aliran file akan melepaskan semua sumber daya yang terkait dengannya, sehingga mencegah kebocoran memori.

## Kesimpulan

Nah, itu dia! Anda telah berhasil mengaktifkan pratinjau pemisah halaman untuk lembar kerja menggunakan Aspose.Cells untuk .NET. Fitur ini dapat meningkatkan kemampuan Anda untuk mengelola tata letak cetak secara signifikan, sehingga memudahkan penyajian data secara terstruktur. Baik Anda membuat laporan atau menyiapkan data untuk dicetak, Aspose.Cells menawarkan berbagai alat yang diperlukan untuk melepaskan kreativitas dan produktivitas Anda. Jadi, tunggu apa lagi? Terjunlah ke proyek Excel Anda berikutnya dengan Aspose.Cells dan lihat bagaimana ia mengubah alur kerja Anda!

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells?
Aspose.Cells adalah API .NET yang memungkinkan pengembang untuk membuat, memanipulasi, dan mengonversi file Excel tanpa perlu menginstal Microsoft Excel.

### Bisakah saya menggunakan Aspose.Cells secara gratis?
 Ya, Aspose menawarkan uji coba gratis untuk tujuan pengujian. Anda dapat[dapatkan uji coba gratis di sini](https://releases.aspose.com/).

### Bagaimana saya bisa membeli Aspose.Cells?
 Kamu bisa[beli Aspose.Cells di sini](https://purchase.aspose.com/buy).

### Apakah dukungan teknis tersedia untuk Aspose.Cells?
 Tentu saja! Anda bisa mendapatkan bantuan melalui[Forum dukungan Aspose](https://forum.aspose.com/c/cells/9).

### Bisakah saya menerapkan pratinjau hentian halaman pada beberapa lembar kerja?
Ya, Anda dapat melakukan pengulangan pada lembar kerja di buku kerja Anda dan menerapkan properti yang sama untuk setiap lembar kerja secara individual.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
