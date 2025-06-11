---
"description": "Buat PDF dengan bagan Excel Anda menggunakan Aspose.Cells for .NET. Pelajari caranya dengan panduan langkah demi langkah ini."
"linktitle": "Buat Bagan PDF dengan Ukuran Halaman yang Diinginkan"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Buat Bagan PDF dengan Ukuran Halaman yang Diinginkan"
"url": "/id/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Buat Bagan PDF dengan Ukuran Halaman yang Diinginkan

## Bevezetés

Membuat bagan yang menarik secara visual dan informatif sangat penting untuk representasi data di berbagai bidang. Baik Anda berurusan dengan data penjualan, metrik kinerja, atau jenis informasi lainnya, memiliki kemampuan untuk menghasilkan bagan berkualitas tinggi akan memberikan kedalaman dan kejelasan pada temuan Anda. Jika Anda bekerja dengan aplikasi .NET, Aspose.Cells adalah pustaka canggih yang memudahkan penanganan dokumen Excel dan pembuatan bagan. Dalam tutorial ini, kami akan memandu Anda melalui proses pembuatan bagan dalam format PDF dari file Excel dengan ukuran halaman yang diinginkan.

## Előfeltételek

Sebelum menyelami kode, ada beberapa prasyarat yang harus Anda penuhi untuk memastikan pengalaman yang lancar:

### C# és .NET alapismeretek

Anda memerlukan pemahaman dasar tentang pemrograman C# dan kerangka kerja .NET. Ini akan membantu Anda memahami struktur kode yang akan Anda temukan dalam panduan ini.

### Aspose.Cells .NET-hez

Pastikan Anda telah menginstal Aspose.Cells for .NET. Anda dapat menemukan semua detailnya di [Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/). 

### Fejlesztői környezet

Siapkan lingkungan pengembangan Anda. Ini bisa berupa Visual Studio atau IDE lain yang mendukung C#. Unduh dan instal pustaka Aspose.Cells dari [letöltési oldal](https://releases.aspose.com/cells/net/).

### Contoh File Excel

Anda akan memerlukan contoh berkas Excel yang berisi setidaknya satu bagan. Anda dapat membuat contoh berkas atau mengunduhnya untuk digunakan dalam tutorial ini.

## Csomagok importálása

Untuk mulai bekerja dengan Aspose.Cells, Anda perlu mengimpor namespace yang diperlukan ke dalam aplikasi C# Anda. Berikut cara melakukannya:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

Ruang nama ini memberi Anda akses ke kelas dan metode yang diperlukan untuk memanipulasi buku kerja Excel dan kontennya.

Sekarang setelah semua prasyarat terpenuhi, mari kita uraikan prosesnya ke dalam langkah-langkah terperinci.

## Langkah 1: Siapkan Direktori Output dan Sumber

Untuk memulai, Anda perlu menentukan di mana keluaran PDF akan disimpan dan di mana dokumen Excel sumber Anda berada.

```csharp
//Kimeneti könyvtár
string outputDir = "Your Output Directory";

//Forráskönyvtár
string sourceDir = "Your Document Directory";
```

Pastikan untuk mengganti "Your Output Directory" dan "Your Document Directory" dengan jalur yang sebenarnya pada sistem Anda. Ini menentukan di mana Aspose akan menyimpan PDF yang dihasilkan dan di mana ia akan menemukan file Excel.

## 2. lépés: Töltse be a minta Excel-fájlt

Selanjutnya, Anda perlu memuat berkas Excel yang berisi bagan tersebut. Berikut caranya:

```csharp
//Muat contoh file Excel yang berisi bagan.
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

A `Workbook` class merupakan bagian penting dalam berinteraksi dengan dokumen Excel Anda. Pastikan jalur mengarah dengan benar ke berkas Excel Anda—kesalahan di sini akan mencegah kode lainnya untuk dijalankan.

## 3. lépés: Az első munkalap elérése

Setelah buku kerja dimuat, langkah berikutnya adalah mengakses lembar kerja yang berisi bagan yang diinginkan.

```csharp
//Akses lembar kerja pertama.
Worksheet ws = wb.Worksheets[0];
```

Di Aspose.Cells, lembar kerja diindeks mulai dari nol, jadi `Worksheets[0]` mengacu pada lembar pertama.

## Langkah 4: Akses Bagan Pertama

Sekarang, mari akses diagram yang ingin Anda ekspor ke PDF. Langkah ini mengasumsikan bahwa lembar kerja Anda berisi setidaknya satu diagram.

```csharp
//Akses bagan pertama di dalam lembar kerja.
Chart ch = ws.Charts[0];
```

Sekali lagi, ini mengakses bagan pertama dalam lembar kerja; pastikan struktur lembar kerja Anda sesuai dengan pendekatan ini.

## Langkah 5: Buat PDF dengan Ukuran Halaman yang Diinginkan

Akhirnya, saatnya membuat PDF dari bagan dengan ukuran halaman tertentu. Berikut ini adalah baris kode ajaib yang melakukan semuanya:

```csharp
//Buat bagan pdf dengan ukuran halaman yang diinginkan.
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

Ebben a kódban:
- PDF akan disimpan ke direktori keluaran yang Anda tentukan sebelumnya.
- A számok `7, 7` masing-masing mewakili lebar dan tinggi ukuran halaman yang diinginkan.
- PageLayoutAlignmentType.Center memastikan bagan berada di tengah halaman.

## 6. lépés: Megerősítő üzenet

Untuk memberi tahu diri Anda (dan orang lain) bahwa semuanya berjalan lancar, sertakan pesan konfirmasi di akhir kode Anda:

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

Pesan ini akan muncul di jendela konsol setelah proses selesai, menandakan bahwa PDF Anda telah dibuat tanpa hambatan.

## Következtetés

Selamat! Anda baru saja mempelajari cara memanfaatkan Aspose.Cells untuk .NET guna membuat PDF dari bagan yang terdapat dalam berkas Excel. Pustaka canggih ini menyederhanakan proses manipulasi dokumen Excel dan pembuatan representasi visual data, sehingga menghemat waktu Anda dalam memformat secara manual. Pastikan untuk menjelajahi berbagai fitur lain yang ditawarkan Aspose.Cells selain pembuatan PDF—Anda tidak akan pernah tahu apa yang dapat menyempurnakan proyek Anda lebih jauh!

## GYIK

### Mire használják az Aspose.Cells for .NET-et?  
Aspose.Cells untuk .NET digunakan untuk membuat, mengedit, dan mengonversi dokumen Excel secara terprogram dalam aplikasi .NET.

### Ingyenesen használhatom az Aspose.Cells-t?  
Ya, Aspose.Cells menawarkan [ingyenes próba](https://releases.aspose.com/) értékelési célokra.

### Apakah ada cara untuk memperpanjang masa uji coba saya melampaui periode awal?  
Pályázatot tehet egy [ideiglenes engedély](https://purchase.aspose.com/temporary-license/) untuk pengujian lanjutan.

### Bagaimana jika saya mengalami masalah atau memiliki pertanyaan?  
Segítséget kérhetsz az Aspose közösségtől a következő címen: [támogató fórum](https://forum.aspose.com/c/cells/9).

### Hogyan vásárolhatom meg az Aspose.Cells-t?  
Anda dapat membeli Aspose.Cells dari [vásárlási oldal](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}