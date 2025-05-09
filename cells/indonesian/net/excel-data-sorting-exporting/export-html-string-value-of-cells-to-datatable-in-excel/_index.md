---
"description": "Pelajari cara mengekspor nilai string HTML dari sel Excel ke DataTable menggunakan Aspose.Cells untuk .NET dalam tutorial langkah demi langkah yang sederhana."
"linktitle": "Ekspor Nilai String HTML dari Sel ke DataTable di Excel"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Ekspor Nilai String HTML dari Sel ke DataTable di Excel"
"url": "/id/net/excel-data-sorting-exporting/export-html-string-value-of-cells-to-datatable-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor Nilai String HTML dari Sel ke DataTable di Excel

## Bevezetés

Saat bekerja dengan file Excel di lingkungan .NET, Anda mungkin perlu mengekstrak informasi dari sel, tidak hanya sebagai teks biasa, tetapi juga sebagai string HTML. Ini bisa sangat berguna saat Anda menangani data teks kaya atau saat Anda ingin mempertahankan format. Dalam panduan ini, saya akan memandu Anda mengekspor nilai string HTML sel ke DataTable menggunakan Aspose.Cells untuk .NET. 

## Előfeltételek

Sebelum menyelami kode, mari pastikan Anda memiliki semua yang Anda butuhkan. Berikut daftar periksa singkatnya:

1. Pengetahuan Dasar C# dan .NET: Sebelum terjun ke coding, pastikan Anda sudah familiar dengan pemrograman C# dan dasar-dasar kerangka .NET.
2. Aspose.Cells untuk .NET: Jika Anda belum melakukannya, Anda perlu menginstal Aspose.Cells untuk .NET. Anda dapat mengunduh uji coba gratis dari [itt](https://releases.aspose.com/).
3. Visual Studio atau IDE Pilihan Anda: Siapkan lingkungan Anda untuk menulis kode C#. Visual Studio direkomendasikan karena berbagai fiturnya dan kemudahan penggunaannya.
4. Contoh File Excel: Anda akan memerlukan contoh file Excel (`sampleExportTableAsHtmlString.xlsx`) untuk digunakan. Pastikan file tersebut berada di direktori yang dapat diakses.
5. Pengelola Paket NuGet: Pastikan Anda memiliki akses ke Pengelola Paket NuGet di proyek Anda untuk menambahkan pustaka Aspose.Cells dengan mudah.

Jika semua prasyarat ini terpenuhi, mari kita mulai membuat kode!

## Csomagok importálása

Sebelum kita dapat mulai bekerja dengan Aspose.Cells, kita perlu mengimpor paket-paket yang diperlukan. Ini biasanya melibatkan penambahan paket Aspose.Cells NuGet ke proyek Anda. Berikut cara melakukannya:

### Buka Pengelola Paket NuGet

Di Visual Studio, klik kanan proyek Anda di Solution Explorer, dan pilih Kelola Paket NuGet.

### Aspose.Cells keresése

Di Pengelola Paket NuGet, ketik `Aspose.Cells` di bilah pencarian.

### Telepítse a csomagot

Setelah Anda menemukan Aspose.Cells, klik tombol Install. Ini akan menambahkan pustaka ke proyek Anda dan memungkinkan Anda untuk mengimpornya ke dalam kode Anda.

### A névtér importálása

Add hozzá a következő using direktívát a kódfájl elejéhez:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Data;
```

Sekarang setelah kita menyiapkan semuanya, mari selami proses langkah demi langkah mengekspor nilai string HTML dari file Excel ke DataTable. 

## 1. lépés: A forráskönyvtár meghatározása

Anda akan mulai dengan menentukan direktori tempat file Excel contoh Anda disimpan. Hal ini penting karena memberi tahu aplikasi Anda tempat menemukan file tersebut. Berikut kode untuk itu:

```csharp
string sourceDir = "Your Document Directory";
```

Mindenképpen cserélje ki `"Your Document Directory"` az Excel-fájl tényleges elérési útjával.

## 2. lépés: Töltse be a minta Excel-fájlt

Langkah selanjutnya adalah memuat buku kerja Excel. Anda akan menggunakan `Workbook` class dari Aspose.Cells untuk melakukan hal ini. Berikut cara memuat file tersebut:

```csharp
Workbook wb = new Workbook(sourceDir + "sampleExportTableAsHtmlString.xlsx");
```

Baris kode sederhana ini menginisialisasi buku kerja dan memuat file Excel yang ditentukan.

## 3. lépés: Az első munkalap elérése

Setelah buku kerja dimuat, Anda akan ingin mengakses lembar kerja tertentu yang berisi data yang Anda minati. Umumnya, Anda akan memulai dengan lembar kerja pertama:

```csharp
Worksheet ws = wb.Worksheets[0];
```

Di sini, kita bekerja dengan lembar kerja pertama (indeks 0). Pastikan data Anda ada di lembar yang benar.

## Langkah 4: Tentukan Opsi Tabel Ekspor

Untuk mengontrol bagaimana data diekspor, Anda perlu mengatur `ExportTableOptions`Dalam kasus ini, Anda ingin memastikan bahwa nama kolom tidak diekspor, dan Anda ingin data sel diekspor sebagai string HTML:

```csharp
ExportTableOptions opts = new ExportTableOptions();
opts.ExportColumnName = false;
opts.ExportAsHtmlString = true;
```

Konfigurasi ini memungkinkan Anda mempertahankan format yang kaya pada data sel saat mengekspor.

## Langkah 5: Ekspor Sel ke DataTable

Sekarang tibalah pada bagian penting di mana Anda benar-benar mengekspor data. Menggunakan `ExportDataTable` metode, Anda dapat menarik data dari lembar kerja ke dalam `DataTable`Berikut cara melakukannya:

```csharp
DataTable dt = ws.Cells.ExportDataTable(0, 0, 3, 3, opts);
```

Kode ini mengekspor rentang sel tertentu (dari baris 0, kolom 0 hingga baris 3, kolom 3) ke dalam DataTable menggunakan opsi yang ditentukan sebelumnya.

## Langkah 6: Cetak Nilai String HTML

Terakhir, mari cetak nilai string HTML dari sel tertentu di DataTable untuk melihat apa yang berhasil kita ekspor. Misalnya, jika Anda ingin mencetak nilai dari baris ketiga dan kolom kedua, Anda akan melakukan hal berikut:

```csharp
Console.WriteLine(dt.Rows[2][1].ToString());
```

Baris ini mencetak string HTML yang diinginkan dari DataTable ke konsol. 

## Következtetés 

Nah, itu dia! Anda telah berhasil mengekspor nilai string HTML dari sel dalam file Excel ke DataTable menggunakan Aspose.Cells for .NET. Kemampuan ini tidak hanya memperkaya keterampilan manipulasi data Anda, tetapi juga memperluas opsi Anda saat menangani konten yang diformat langsung dari file Excel. 

## GYIK

### Dapatkah saya menggunakan Aspose.Cells untuk format file lain selain Excel?  
Ya, Aspose.Cells terutama untuk Excel, tetapi Aspose menawarkan pustaka lain untuk format yang berbeda.

### Szükségem van licencre az Aspose.Cells-hez?  
Ya, lisensi yang valid diperlukan untuk penggunaan produksi. Anda bisa mendapatkan lisensi sementara [itt](https://purchase.aspose.com/temporary-license/).

### Bagaimana jika file Excel saya berisi rumus? Apakah rumus tersebut dapat diekspor dengan benar?  
Ya, Aspose.Cells dapat menangani rumus, dan saat mengekspor, rumus akan dievaluasi berdasarkan nilai yang dihasilkan.

### Apakah mungkin untuk mengubah opsi ekspor?  
Tentu saja! Anda dapat menyesuaikannya `ExportTableOptions` agar sesuai dengan kebutuhan spesifik Anda.

### Di mana saya dapat menemukan dokumentasi yang lebih rinci untuk Aspose.Cells?  
Bőséges dokumentációt találhat [itt](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}