---
"description": "Pelajari cara mengonversi grafik Excel ke PDF menggunakan Aspose.Cells for .NET dengan panduan langkah demi langkah yang mudah ini. Jelajahi kiat-kiat penting dan contoh-contoh pengodean."
"linktitle": "Konversi Bagan ke PDF"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Konversi Bagan ke PDF"
"url": "/id/net/chart-rendering-and-conversion/convert-chart-to-pdf/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Konversi Bagan ke PDF

## Bevezetés

Dalam hal penanganan lembar kerja, bagan sering kali memainkan peran penting dalam memvisualisasikan data secara efektif. Baik Anda sedang mempersiapkan laporan, melakukan presentasi, atau sekadar memfasilitasi analisis data, mengonversi bagan ini ke PDF memberikan sentuhan profesional. Di sini, kami akan memandu Anda melalui langkah-langkah untuk mengonversi bagan Excel ke format PDF menggunakan Aspose.Cells for .NET, pustaka canggih yang dirancang untuk menyederhanakan manipulasi Excel.

## Előfeltételek

Sebelum memulai tutorial, Anda perlu memastikan bahwa Anda memiliki pengaturan yang tepat. Berikut ini yang Anda perlukan:

### .NET keretrendszer
Pastikan Anda telah menginstal .NET Framework di komputer Anda. Aspose.Cells kompatibel dengan berbagai versi tetapi cenderung berfungsi paling baik dengan versi terbaru.

### Aspose.Cells könyvtár
Anda akan memerlukan pustaka Aspose.Cells for .NET. Anda dapat mengunduhnya dari [itt](https://releases.aspose.com/cells/net/)Pustaka ini dilengkapi dengan API lengkap yang merangkum semua fungsi yang Anda perlukan untuk manipulasi Excel.

### Vizuális Stúdió
Menginstal Visual Studio sangatlah penting, karena ini merupakan IDE hebat untuk menulis kode .NET Anda dengan lancar.

### C# alapismeretek
Sedikit pengetahuan tentang bahasa pemrograman C# akan membantu Anda memahami segmen kode dengan lebih baik.

## Csomagok importálása

Untuk berhasil menggunakan Aspose.Cells di proyek Anda, Anda perlu mengimpor paket yang diperlukan. Berikut cara melakukannya:

### Új projekt létrehozása

Mulailah dengan membuat proyek C# baru di Visual Studio:

1. Nyisd meg a Visual Studio-t.
2. Klik “Buat proyek baru.”
3. Pilih “Aplikasi Konsol (.NET Core)” atau “Aplikasi Konsol (.NET Framework)” berdasarkan kebutuhan Anda.
4. Beri nama proyek Anda dan klik “Buat.”

### Aspose.Cells hivatkozás hozzáadása

Setelah membuat proyek Anda, Anda harus menambahkan referensi ke pustaka Aspose.Cells:

1. Di Solution Explorer, klik kanan pada proyek Anda.
2. Pilih “Kelola Paket NuGet.”
3. Keresd meg az „Aspose.Cells” fájlt, és telepítsd.

Setelah pustaka disertakan dalam proyek Anda, Anda siap untuk beralih ke kode.

### Importálja a szükséges névtereket

A te tetején `Program.cs` file, tambahkan namespace berikut:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Charts;
using System.IO;
```

Berikut cara mengonversi grafik Excel ke PDF secara sistematis. Ikuti langkah demi langkah!

## Langkah 1: Siapkan Direktori Output dan Sumber

Untuk memulai kode Anda, pertama-tama Anda ingin menentukan di mana Anda akan menyimpan keluaran Anda dan di mana dokumen sumber Anda berada.

```csharp
// Kimeneti könyvtár
string outputDir = "Your Output Directory";

// Forráskönyvtár
string sourceDir = "Your Document Directory";
```

Mindenképpen cserélje ki `"Your Output Directory"` és `"Your Document Directory"` a fájlok tényleges elérési útjával.

## 2. lépés: Töltse be az Excel-munkafüzetet

Sekarang, mari kita muat berkas Excel yang berisi grafik yang ingin Anda ubah. Ini cukup mudah:

```csharp
// Memuat file excel yang berisi grafik
Workbook workbook = new Workbook(sourceDir + "sampleChartToPdf.xlsx");
```

Kode ini menginisialisasi objek buku kerja baru dan memuat berkas Excel yang ditentukan. Pastikan nama berkas sesuai dengan yang ada di direktori sumber Anda.

## 3. lépés: A munkalap elérése

Selanjutnya, Anda perlu mengakses lembar kerja yang berisi bagan yang ingin Anda ubah. Berikut cara melakukannya:

```csharp
// Első munkalap elérése
Worksheet worksheet = workbook.Worksheets[0];
```

Kode ini mengakses lembar kerja pertama dalam buku kerja Anda, memungkinkan Anda untuk mengerjakannya.

## 4. lépés: Hozzáférés a diagramhoz 

Setelah Anda memiliki lembar kerja, saatnya mengakses bagan spesifik yang ingin Anda ubah:

```csharp
// Hozzáférés a munkalap első diagramjához
Chart chart = worksheet.Charts[0];
```

Baris ini mengambil bagan pertama yang terdapat dalam lembar kerja. Jika lembar kerja Anda memiliki beberapa bagan dan Anda perlu menargetkan satu bagan tertentu, sesuaikan indeks sebagaimana mestinya.

## Langkah 5: Ubah Bagan ke PDF

Sekarang tibalah bagian yang menarik—mengonversi grafik ke format PDF. Anda dapat menyimpannya ke dalam file atau aliran memori.

### Opsi 1: Simpan Bagan ke File

Untuk menyimpan grafik langsung ke berkas PDF, gunakan kode berikut:

```csharp
// Simpan grafik ke dalam format pdf
chart.ToPdf(outputDir + "outputChartToPdf.pdf");
```

Pastikan saja direktori keluaran memang ada untuk menghindari kesalahan apa pun.

### Opsi 2: Simpan Bagan ke Aliran Memori

Jika Anda ingin memanipulasi PDF lebih lanjut atau perlu segera menggunakannya di aplikasi Anda, menyimpannya ke aliran memori mungkin merupakan pilihan yang lebih baik:

```csharp
// Simpan grafik ke dalam format pdf di aliran
MemoryStream ms = new MemoryStream();
chart.ToPdf(ms);
```

Di sini, Anda menyimpan PDF ke dalam aliran memori, yang dapat digunakan sesuai dengan kebutuhan aplikasi Anda.

## Langkah 6: Menampilkan Pesan Sukses

Terakhir, akan lebih baik jika Anda menunjukkan bahwa operasi Anda berhasil. Anda cukup mencetak pesan sukses ke konsol:

```csharp
Console.WriteLine("ChartToPdf executed successfully.");
```

## Következtetés

Nah, itu dia! Dengan memanfaatkan Aspose.Cells for .NET, mengonversi grafik Excel ke format PDF menjadi sangat mudah. Baik Anda memilih untuk menyimpan ke file atau aliran memori, pustaka ini menjanjikan fleksibilitas dan kemudahan penggunaan. Jadi, mengapa tidak mencobanya? Laporan Anda akan terlihat jauh lebih tajam dengan grafik PDF yang diformat secara profesional!

## GYIK

### Bisakah Aspose.Cells mengonversi beberapa bagan sekaligus?
Ya, Anda dapat melakukan pengulangan melalui `worksheet.Charts` koleksi untuk mengonversi setiap grafik satu per satu.

### Apakah Aspose.Cells cocok untuk file Excel berukuran besar?
Tentu saja! Aspose.Cells dioptimalkan untuk kinerja dan dapat menangani file Excel berukuran besar secara efisien.

### A .NET mely verzióit támogatja az Aspose.Cells?
Aspose.Cells mendukung berbagai versi .NET, termasuk .NET Framework dan .NET Core.

### Di mana saya dapat menemukan dokumentasi terperinci?
Látogassa meg a [Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/) untuk informasi dan contoh yang mendalam.

### Apakah ada versi uji coba gratis yang tersedia?
Ya! Anda dapat mengunduh uji coba gratis dari [itt](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}