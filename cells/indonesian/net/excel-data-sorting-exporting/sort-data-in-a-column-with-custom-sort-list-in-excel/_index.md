---
"description": "Pelajari cara mengurutkan data di Excel menggunakan daftar pengurutan kustom dengan Aspose.Cells untuk .NET dalam tutorial komprehensif ini."
"linktitle": "Mengurutkan Data dalam Kolom dengan Daftar Urutan Kustom di Excel"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Mengurutkan Data dalam Kolom dengan Daftar Urutan Kustom di Excel"
"url": "/id/net/excel-data-sorting-exporting/sort-data-in-a-column-with-custom-sort-list-in-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Mengurutkan Data dalam Kolom dengan Daftar Urutan Kustom di Excel

## Bevezetés

Tutorial ini akan memandu Anda melalui proses menyiapkan proyek, memuat file Excel, dan mengurutkan data dalam rentang tertentu menggunakan tata urutan khusus. Dengan mengikuti panduan ini, Anda akan memperoleh pengalaman langsung yang dapat meningkatkan keterampilan pengelolaan data dan kegunaan pustaka Aspose.Cells.

## Előfeltételek

Sebelum masuk ke tutorial, mari kita uraikan beberapa prasyarat untuk memastikan pengalaman belajar yang lancar.

### C# alapismeretek

Meskipun tutorial ini dirancang untuk memandu Anda melalui setiap langkah, memiliki pemahaman dasar tentang C# akan memudahkan Anda memahami konsep yang disajikan.

### .NET fejlesztői környezet

Pastikan Anda memiliki lingkungan pengembangan .NET yang berfungsi. Anda dapat menggunakan Visual Studio atau IDE lain yang mendukung pengembangan .NET.

### Paket NuGet Aspose.Cells untuk .NET

Anda perlu memasang pustaka Aspose.Cells untuk .NET di proyek Anda. Anda dapat menambahkannya dengan mudah melalui NuGet Package Manager. 

Berikut cara melakukannya:

1. Nyisd meg a projektedet a Visual Studioban.
2. Buka "Alat" > "Manajer Paket NuGet" > "Kelola Paket NuGet untuk Solusi".
3. Keresés `Aspose.Cells` és telepítsd a legújabb verziót.

### File Excel Dasar untuk Pengujian

Anda memerlukan contoh berkas Excel untuk digunakan. Anda dapat membuat berkas Excel sederhana dengan nama negara acak dan kodenya.

## Csomagok importálása

Untuk memulai, mari impor paket yang diperlukan ke dalam proyek Anda. Berikut cuplikan cara menyiapkan kode Anda:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Setelah paket diimpor, kami siap untuk melangkah maju.

## Langkah 1: Tentukan Direktori Sumber dan Output 

Langkah pertama adalah menentukan lokasi berkas masukan dan lokasi penyimpanan keluaran (berkas yang telah diurutkan). Anda perlu menentukan dua jalur: satu untuk berkas Excel sumber dan satu lagi untuk menyimpan keluaran setelah diurutkan.

```csharp
string sourceDir = "Your Document Directory\\";
string outputDir = "Your Document Directory\\";
```

## 2. lépés: Töltse be a forrás Excel fájlt

Selanjutnya, kita akan memuat berkas Excel yang berisi data yang ingin Anda urutkan. Hal ini dilakukan dengan membuat contoh `Workbook` kelas dan meneruskan jalur berkas sumber Anda.

```csharp
Workbook wb = new Workbook(sourceDir + "sampleSortData_CustomSortList.xlsx");
```

## 3. lépés: Az első munkalap elérése 

Setelah berkas dimuat, kita perlu mengakses lembar kerja tertentu yang berisi data yang ingin kita urutkan. Dalam kasus ini, kita menargetkan lembar kerja pertama.

```csharp
Worksheet ws = wb.Worksheets[0];
```

## Langkah 4: Tentukan Area Sel yang Akan Diurutkan

Kita perlu menentukan rentang sel yang akan kita urutkan. Dalam contoh ini, kita akan mengurutkan sel dari A1 hingga A40. Gunakan `CellArea.CreateCellArea` metode untuk menentukan area sel.

```csharp
CellArea ca = CellArea.CreateCellArea("A1", "A40");
```

## Langkah 5: Buat Daftar Sortir Kustom

Sebelum mengurutkan, kita perlu menetapkan kriteria yang akan kita gunakan untuk pengurutan kustom kita. Anda dapat menentukan daftar pengurutan sebagai serangkaian string. Daftar pengurutan kustom akan menentukan urutan pengurutan.

```csharp
string[] customSortList = new string[] { "USA,US", "Brazil,BR", "China,CN", "Russia,RU", "Canada,CA" };
```

## Langkah 6: Tambahkan Kunci Sortir dan Lakukan Sortir

Sekarang saatnya untuk mengurutkan! Kita akan menggunakan kelas DataSorter untuk ini. Buat kunci untuk mengurutkan berdasarkan daftar kustom kita dan jalankan operasi pengurutan.

```csharp
wb.DataSorter.AddKey(0, SortOrder.Ascending, customSortList);
wb.DataSorter.Sort(ws.Cells, ca);
```

## 7. lépés: Mentse el a kimeneti Excel fájlt

Setelah pengurutan selesai, langkah terakhir adalah menyimpan perubahan ke file Excel baru. Tentukan nama file output dan simpan buku kerja.

```csharp
wb.Save(outputDir + "outputSortData_CustomSortList.xlsx");
```

## 8. lépés: A sikeres végrehajtás megerősítése

Untuk memastikan semuanya berjalan lancar, Anda dapat mencetak pesan konfirmasi ke konsol. Ini membantu dalam debugging dan memberi Anda kepuasan bahwa operasi berhasil.

```csharp
Console.WriteLine("SortDataInColumnWithCustomSortList executed successfully.\r\n");
```

## Következtetés

Nah, itu dia! Anda telah berhasil mengurutkan data dalam kolom Excel menggunakan daftar pengurutan kustom dengan Aspose.Cells untuk .NET. Pengurutan membantu memberikan struktur dan kejelasan pada data Anda, sehingga lebih mudah untuk dianalisis dan diinterpretasikan. Saya harap panduan ini akan meningkatkan keterampilan Anda ke tingkat berikutnya dan membantu Anda menyadari betapa hebatnya Aspose.Cells untuk tugas-tugas terkait Excel Anda.

## GYIK

### Mi az Aspose.Cells .NET-hez?
Aspose.Cells untuk .NET adalah pustaka komprehensif yang memungkinkan Anda memanipulasi file Excel dalam aplikasi .NET, termasuk membuat, mengedit, dan mengonversinya.

### Bisakah saya mengurutkan lebih dari satu kolom menggunakan daftar pengurutan khusus?
Ya! Anda dapat menambahkan kunci tambahan untuk mengurutkan berdasarkan beberapa kolom jika diperlukan, cukup ikuti prosedur yang sama untuk setiap kunci.

### Apakah saya perlu pengetahuan sebelumnya tentang C# untuk menggunakan Aspose.Cells?
Meskipun bermanfaat, Anda dapat mengikuti tutorial ini dan belajar sambil jalan! Memiliki pemahaman dasar tentang C# akan meningkatkan pengalaman belajar Anda.

### Apakah mungkin menggunakan lisensi sementara untuk Aspose.Cells?
Tentu saja! Anda dapat memperoleh lisensi sementara jika Anda ingin menguji fitur-fitur lengkap pustaka tanpa batasan.

### Dapatkah saya mengunduh contoh atau dokumentasi untuk Aspose.Cells?
Ya! Aspose menyediakan dokumentasi dan contoh proyek yang lengkap yang dapat sangat membantu Anda. Lihat [Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}