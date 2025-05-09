---
"description": "Pelajari cara mengimpor data ke Excel dengan format DB Num kustom menggunakan Aspose.Cells untuk .NET dalam tutorial yang mudah diikuti ini."
"linktitle": "Mengimpor Data ke Excel dengan Pemformatan Pola Angka DB Kustom"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Mengimpor Data ke Excel dengan Pemformatan Pola Angka DB Kustom"
"url": "/id/net/excel-data-import-export/import-data-to-worksheet-in-excel-with-specified-db-num-custom-pattern-formatting/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Mengimpor Data ke Excel dengan Pemformatan Pola Angka DB Kustom

## Bevezetés

Jika menyangkut manipulasi lembar kerja, mengimpor data ke Excel dan memformatnya dengan benar bisa terasa seperti tugas yang sangat berat, terutama jika Anda ingin menggunakan format berbasis budaya tertentu seperti pola DB Num. Jika Anda pernah merasa terhambat oleh teknis pemformatan Excel, Anda berada di tempat yang tepat! Dalam panduan ini, kami akan menguraikan semuanya menjadi beberapa langkah sederhana menggunakan Aspose.Cells untuk .NET, yang membuat impor data Anda tidak hanya mudah tetapi juga menarik secara estetika. Jadi, tunggu sebentar karena kami akan langsung menyelami dunia pemrograman .NET, pemformatan, dan pengeksporan file Excel dengan mudah!

## Előfeltételek

Sebelum kita masuk ke inti permasalahan, mari pastikan Anda memiliki semua yang Anda butuhkan. Berikut ini adalah daftar periksa singkat tentang prasyarat untuk mempersiapkan Anda meraih kesuksesan:

1. .NET Framework: Pastikan Anda telah menginstal .NET Framework di komputer Anda. Aspose.Cells bekerja dengan lancar dengan berbagai versi .NET.
2. Aspose.Cells untuk .NET: Anda perlu mengunduh dan memasang pustaka Aspose.Cells. Anda dapat mengunduhnya dari [letöltési link](https://releases.aspose.com/cells/net/).
3. Lingkungan Pengembangan Terpadu (IDE): Gunakan IDE seperti Visual Studio tempat Anda dapat menulis dan mengeksekusi kode C# Anda.
4. Pengetahuan Dasar C#: Memiliki pemahaman dasar tentang C# akan membantu Anda mengikuti praktik pengkodean yang akan kami gunakan dalam panduan ini.

Sudah punya semuanya? Bagus! Mari kita lanjutkan dengan mengimpor paket yang diperlukan.

## Csomagok importálása

Agar dapat bekerja secara efektif dengan Aspose.Cells, Anda perlu mengimpor namespace yang diperlukan di awal file C# Anda. Mari kita uraikan langkah demi langkah.

### Buat File C# Anda

Buka IDE Anda (Visual Studio direkomendasikan) dan buat proyek C# baru. Beri nama yang relevan seperti `ExcelDataImport`.

### Referensi Aspose.Cells

Anda harus menyertakan pustaka Aspose.Cells dalam proyek Anda. Klik kanan pada proyek Anda di Solution Explorer dan pilih 'Add Reference'. Telusuri tempat Anda menginstal Aspose.Cells dan pilih.

### Impor Ruang Nama yang Diperlukan

Di bagian atas file C# Anda, impor namespace berikut:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Baris sederhana ini adalah gerbang Anda ke semua fungsionalitas yang ditawarkan Aspose.Cells. 

Sekarang setelah kita memenuhi semua prasyarat dan mengimpor paket yang diperlukan, mari selami proses langkah demi langkah mengimpor data ke Excel dan menerapkan format pola DB Num kustom. Kita akan melakukannya secara metodis untuk memastikan kejelasan dan pemahaman.

## Langkah 1: Mengatur Direktori Data

Pertama, Anda perlu menentukan jalur ke direktori dokumen tempat output akan disimpan. Sesuaikan ini menurut struktur file Anda.

```csharp
string dataDir = "Your Document Directory";
```

Dalam contoh ini, ganti `Your Document Directory` dengan jalur Anda yang sebenarnya, seperti `C:\\Users\\YourName\\Documents\\`.

## 2. lépés: Munkafüzet létrehozása

Berikutnya, Anda akan membuat buku kerja baru, yang pada dasarnya adalah file Excel Anda.

```csharp
Workbook wb = new Workbook();
```

Di sini, kita membuat instance baru `Workbook` objek. Ini kanvas kosong Anda!

## 3. lépés: Az első munkalap elérése

Setiap buku kerja berisi beberapa lembar kerja. Anda perlu mengakses lembar kerja pertama untuk mulai memasukkan data.

```csharp
Worksheet ws = wb.Worksheets[0];
```

Sama seperti membuka buku ke halaman pertama, Anda mengakses lembar kerja pertama untuk menambahkan data Anda.

## Langkah 4: Masukkan Data ke dalam Sel

Sekarang, mari kita isi sel dengan beberapa data. Untuk contoh ini, kita akan memasukkan nilai `123` ke dalam sel A1.

```csharp
Cell cell = ws.Cells["A1"];
cell.PutValue(123);
```

Anda berbicara langsung dengan Excel di sini—memasukkan data langsung ke sel A1! 

## Langkah 5: Akses Gaya Sel

Setiap sel memiliki gaya, dan Anda dapat menyesuaikan tampilannya. Untuk menerapkan format khusus, pertama-tama, Anda perlu mengakses gaya sel tersebut.

```csharp
Style st = cell.GetStyle();
```

Dengan mengambil gaya sel, Anda bersiap untuk menambahkan sentuhan unik Anda!

## Langkah 6: Tentukan Pemformatan Pola Kustom DBNum

Di sinilah keajaiban terjadi. Anda dapat menentukan pola format khusus menggunakan gaya format DBNum.

```csharp
st.Custom = "[DBNum2][$-804]General";
```

Baris ini memberi tahu Excel untuk memformat angka `123` sesuai dengan pola DBNum yang sesuai dengan bahasa Mandarin. Cukup rapi, bukan?

## Langkah 7: Mengatur Gaya Sel yang Diperbarui

Sekarang setelah Anda menentukan gaya khusus Anda, saatnya menerapkannya ke sel.

```csharp
cell.SetStyle(st);
```

Ini seperti mendandani sel Anda dengan pakaian baru yang bergaya!

## Langkah 8: Sesuaikan Lebar Kolom

Pastikan semuanya terlihat bagus dan rapi. Anda dapat menyesuaikan lebar kolom pertama agar lebih sesuai dengan data Anda.

```csharp
ws.Cells.SetColumnWidth(0, 30);
```

Di sini, kami memperluas lebar kolom, sehingga data Anda tidak terasa sempit. Anggap saja seperti memberi ruang bagi data Anda untuk bernapas!

## 9. lépés: A munkafüzet mentése

Terakhir, mari kita simpan karya agung ini dalam format PDF. Inilah akhir yang hebat!

```csharp
wb.Save(dataDir + "outputDBNumCustomFormatting.pdf", SaveFormat.Pdf);
```

Selamat! Anda baru saja membuat file PDF yang menampilkan nomor Anda yang diformat dengan gaya DB Num.

## Következtetés

Nah, itu dia! Anda telah berhasil mengimpor data ke Excel, menerapkan format DB Num kustom, dan menyimpannya dalam format PDF. Dengan Aspose.Cells untuk .NET, proses ini tidak hanya menjadi lebih mudah tetapi juga jauh lebih fleksibel dan canggih. Tidak perlu lagi bersusah payah dengan opsi format bawaan Excel—sekarang Anda memiliki kendali langsung melalui kode!

Baik Anda sedang mempersiapkan laporan data atau membuat laporan keuangan, memanfaatkan kekuatan Aspose.Cells akan meningkatkan kemampuan spreadsheet Anda ke tingkat yang sama sekali baru. Jadi, tunggu apa lagi? Terjunlah ke dalam proyek Anda dengan percaya diri, dan biarkan data Anda bersinar!

## GYIK

### Mi az Aspose.Cells?  
Aspose.Cells adalah pustaka hebat untuk .NET yang memungkinkan pengembang membuat, memanipulasi, dan mengonversi file Excel secara terprogram.

### Bisakah saya memformat jenis sel lainnya?  
Ya! Anda dapat menerapkan berbagai gaya, format, dan bahkan rumus ke sel mana pun dalam lembar kerja Anda.

### Van ingyenes próbaverzió?  
Tentu saja! Anda dapat mencoba versi uji coba gratis [itt](https://releases.aspose.com/).

### Dalam format apa saya dapat menyimpan file Excel?  
Aspose.Cells mendukung berbagai format termasuk XLSX, XLS, CSV, PDF, dan masih banyak lagi.

### Di mana saya dapat menemukan dukungan lebih lanjut?  
Jika Anda memerlukan bantuan, kunjungi [támogató fórum](https://forum.aspose.com/c/cells/9) untuk bantuan dari masyarakat dan para ahli.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}