---
"description": "Pelajari cara mengonversi lembar kerja Excel ke SVG menggunakan Aspose.Cells untuk .NET dengan panduan langkah demi langkah ini. Sempurna untuk pengembang .NET yang ingin mengubah Excel ke SVG."
"linktitle": "Mengonversi Lembar Kerja ke SVG di .NET"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Mengonversi Lembar Kerja ke SVG di .NET"
"url": "/id/net/conversion-and-rendering/converting-worksheet-to-svg/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Mengonversi Lembar Kerja ke SVG di .NET

## Bevezetés

Jika Anda ingin mengonversi lembar kerja Excel ke format SVG, Anda telah datang ke tempat yang tepat! Aspose.Cells for .NET adalah alat hebat yang memungkinkan pengembang untuk memanipulasi file Excel dan mengonversinya ke berbagai format, termasuk SVG (Scalable Vector Graphics) yang didukung secara luas. Tutorial ini akan memandu Anda melalui proses mengonversi lembar kerja ke SVG di .NET, menguraikannya langkah demi langkah, sehingga bahkan pemula pun dapat mengikutinya dengan mudah.

## Előfeltételek

Sebelum menyelami kodenya, mari pastikan Anda memiliki semua yang Anda butuhkan:

1. Aspose.Cells untuk .NET: Unduh dan instal versi terbaru Aspose.Cells untuk .NET dari [Aspose.Cells .NET-hez](https://releases.aspose.com/cells/net/).
2. Lingkungan Pengembangan .NET: Anda perlu menginstal Visual Studio atau IDE .NET lainnya.
3. Pengetahuan Dasar C#: Diperlukan keakraban dengan C#, tetapi jangan khawatir, kami akan menjelaskan semuanya dengan jelas.
4. File Excel: Siapkan file Excel yang ingin Anda ubah ke format SVG.

## Szükséges csomagok importálása

Sebelum masuk ke bagian pengkodean, pastikan untuk menyertakan namespace yang diperlukan di bagian atas file C# Anda.

```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```

Paket-paket ini diperlukan untuk bekerja dengan Aspose.Cells dan menangani opsi rendering seperti ekspor SVG.

Sekarang setelah dasar-dasarnya dibahas, mari masuk ke langkah sebenarnya dalam mengonversi lembar kerja Excel ke gambar SVG.

## Langkah 1: Tetapkan Jalur ke Direktori Dokumen Anda

Hal pertama yang perlu kita lakukan adalah menentukan jalur ke folder tempat file Excel Anda berada. Hal ini penting karena kode Anda akan merujuk ke direktori untuk memuat dan menyimpan file.

```csharp
// A dokumentumok könyvtárának elérési útja
string dataDir = "Your Document Directory";
```

Mindenképpen cserélje ki `"Your Document Directory"` az Excel-fájl tényleges elérési útjával.

## Langkah 2: Muat File Excel Menggunakan `Workbook`

Selanjutnya, kita perlu memuat file Excel ke dalam instance `Workbook` kelas. Itu `Workbook` kelas mewakili keseluruhan berkas Excel, termasuk semua lembar kerja di dalamnya.

```csharp
string filePath = dataDir + "Template.xlsx";
Workbook book = new Workbook(filePath);
```

Itt, `"Template.xlsx"` adalah nama berkas Excel yang sedang Anda kerjakan. Pastikan berkas ini ada di direktori yang ditentukan, jika tidak, Anda akan mengalami galat.

## Langkah 3: Atur Opsi Gambar atau Cetak untuk Konversi SVG

Sebelum kita dapat mengonversi lembar kerja ke format SVG, kita perlu menentukan opsi gambar. `ImageOrPrintOptions` kelas memungkinkan Anda untuk mengontrol bagaimana lembar kerja akan dikonversi. Secara khusus, kita perlu mengatur `SaveFormat` hogy `SVG` dan pastikan setiap lembar kerja diubah menjadi satu halaman.

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.SaveFormat = SaveFormat.Svg;
imgOptions.OnePagePerSheet = true;
```

A `SaveFormat.Svg` opsi memastikan format keluaran akan menjadi SVG, sementara `OnePagePerSheet` memastikan bahwa setiap lembar kerja akan ditampilkan pada satu halaman.

## Langkah 4: Ulangi Setiap Lembar Kerja di Buku Kerja

Sekarang kita perlu melakukan pengulangan pada semua lembar kerja dalam berkas Excel. Setiap lembar kerja akan dikonversi secara individual.

```csharp
foreach (Worksheet sheet in book.Worksheets)
{
    // Kami akan memproses setiap lembar kerja satu per satu
}
```

Perulangan ini memastikan bahwa berapa pun banyaknya lembar kerja yang ada dalam buku kerja Anda, masing-masing lembar akan ditangani.

## Langkah 5: Buat `SheetRender` Objek untuk Rendering

Untuk setiap lembar kerja, kita akan membuat `SheetRender` objek. Objek ini bertanggung jawab untuk mengonversi lembar kerja ke format gambar yang diinginkan, yang dalam kasus ini adalah SVG.

```csharp
SheetRender sr = new SheetRender(sheet, imgOptions);
```

A `SheetRender` objek mengambil dua argumen: lembar kerja yang sedang Anda ubah dan opsi gambar yang Anda tentukan sebelumnya.

## Langkah 6: Ubah Lembar Kerja ke SVG

Terakhir, dalam loop, kita akan mengonversi setiap lembar kerja ke dalam format SVG. Kita menggunakan loop bersarang untuk mengulang halaman (meskipun dalam kasus ini, hanya ada satu halaman per lembar kerja, berkat `OnePagePerSheet` pilihan).

```csharp
for (int i = 0; i < sr.PageCount; i++)
{
    // Keluarkan lembar kerja ke dalam format gambar Svg
    sr.ToImage(i, filePath + sheet.Name + i + ".out.svg");
}
```

Kode ini akan menyimpan lembar kerja sebagai file SVG di direktori yang sama dengan file Excel. Setiap file SVG akan diberi nama sesuai dengan nama lembar kerja dan nomor indeks untuk menghindari konflik penamaan.

## Következtetés

Selesai! Anda telah berhasil mengonversi lembar kerja Excel ke dalam format SVG menggunakan Aspose.Cells for .NET. Proses ini memungkinkan Anda mempertahankan tata letak dan desain lembar kerja Anda sekaligus membuatnya dapat dilihat di browser atau perangkat apa pun yang mendukung SVG, yang mencakup hampir semuanya. Baik Anda bekerja dengan file Excel yang rumit atau hanya tabel sederhana, metode ini memastikan bahwa data Anda ditampilkan dengan indah dalam format yang ramah web.

## GYIK

### Apa itu SVG, dan mengapa saya harus menggunakannya?
SVG (Scalable Vector Graphics) adalah format yang ramah web yang dapat diskalakan tanpa batas tanpa kehilangan kualitas. Format ini sangat cocok untuk bagan, diagram, dan gambar yang perlu ditampilkan dalam berbagai ukuran.

### Bisakah Aspose.Cells menangani file Excel berukuran besar untuk konversi?
Ya, Aspose.Cells dapat secara efisien menangani file Excel berukuran besar dan mengonversinya ke SVG tanpa masalah kinerja yang signifikan.

### Apakah ada batasan jumlah lembar kerja yang dapat saya ubah ke SVG?
Tidak, tidak ada batasan bawaan di Aspose.Cells untuk mengonversi beberapa lembar kerja. Satu-satunya kendala adalah memori dan kinerja sistem Anda.

### Szükségem van licencre az Aspose.Cells használatához?
Ya, Aspose.Cells memerlukan lisensi untuk penggunaan produksi. Anda dapat memperoleh lisensi sementara [itt](https://purchase.aspose.com/temporary-license/) atau jelajahi [ingyenes próba](https://releases.aspose.com/).

### Bisakah saya menyesuaikan keluaran SVG?
Ya, Anda dapat mengubah `ImageOrPrintOptions` untuk menyesuaikan berbagai aspek keluaran SVG, seperti resolusi dan skala.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}