---
"description": "Pelajari cara menambahkan TextBox ke bagan di Excel menggunakan Aspose.Cells for .NET. Sempurnakan visualisasi data Anda dengan mudah."
"linktitle": "Tambahkan Kontrol Kotak Teks ke Bagan"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Tambahkan Kontrol Kotak Teks ke Bagan"
"url": "/id/net/inserting-controls-in-charts/add-textbox-control-to-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Kontrol Kotak Teks ke Bagan

## Bevezetés

Membuat bagan yang dinamis dan menarik secara visual di Excel adalah cara yang fantastis untuk menyajikan data secara efektif. Salah satu fitur praktis yang dapat Anda gunakan adalah menambahkan TextBox ke bagan. Dengan Aspose.Cells for .NET, tugas ini menjadi mudah dan menyenangkan! Dalam panduan ini, kami akan memandu Anda melalui proses mengintegrasikan TextBox ke dalam bagan Anda langkah demi langkah. Baik Anda seorang pengembang berpengalaman atau baru memulai, tutorial ini akan memberi Anda semua alat yang Anda butuhkan untuk menyempurnakan bagan Excel Anda. Jadi, apakah Anda siap untuk mencobanya?

## Előfeltételek

Sebelum kita mulai membuat kode, ada beberapa hal yang harus Anda siapkan:

- Pemahaman Dasar tentang C#: Pemahaman dasar tentang pemrograman C# akan sangat membantu. Jangan khawatir; Anda tidak perlu menjadi seorang ahli, cukup pahami sintaksnya.
- Pustaka Aspose.Cells Terpasang: Pastikan Anda telah memasang pustaka Aspose.Cells untuk .NET. Anda dapat mengunduhnya dari [itt](https://releases.aspose.com/cells/net/) jika Anda belum melakukannya.
- Visual Studio: Keakraban dengan Visual Studio atau IDE apa pun yang ingin Anda gunakan untuk kerangka kerja .NET sangatlah penting.
- File Excel yang Ada: Untuk contoh ini, kita akan menggunakan file Excel yang sudah ada bernama "sampleAddingTextBoxControlInChart.xls". Anda dapat membuat file tersebut atau mengunduh contohnya.

Sekarang setelah semuanya siap, mari kita masuk ke bagian pengkodean!

## Csomagok importálása

Pertama-tama, kita perlu mengimpor namespace Aspose.Cells yang diperlukan ke proyek C# kita. Anda dapat melakukannya dengan mudah dengan menyertakan baris berikut di bagian atas berkas kode Anda:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using System.Drawing;
```

## 1. lépés: A forrás- és kimeneti könyvtárak meghatározása

Sebelum kita mulai bekerja dengan berkas Excel, penting untuk menentukan di mana berkas masukan Anda berada dan di mana Anda ingin menyimpan berkas keluaran. Ini membantu menjaga proyek Anda tetap teratur.

```csharp
// Forráskönyvtár
string sourceDir = "Your Document Directory";

// Kimeneti könyvtár
string outputDir = "Your Output Directory";
```
Csere `"Your Document Directory"` és `"Your Output Directory"` dengan jalur sebenarnya pada sistem Anda.

## 2. lépés: Nyissa meg a meglévő Excel-fájlt

Selanjutnya, kita perlu membuka berkas Excel yang berisi bagan yang ingin kita ubah. Ini akan memungkinkan kita untuk mengambil bagan dan membuat perubahan.

```csharp
// Buka berkas yang ada.
Workbook workbook = new Workbook(sourceDir + "sampleAddingTextBoxControlInChart.xls");
```
Baris ini menginisialisasi objek Buku Kerja baru dengan file yang kita tentukan.

## Langkah 3: Akses Bagan di Lembar Kerja

Karena grafik di Excel disimpan dalam lembar kerja, pertama-tama kita perlu mengakses lembar kerja tersebut dan kemudian mendapatkan grafik yang diinginkan. Untuk contoh ini, kita akan mengakses grafik pertama di lembar kerja pertama.

```csharp
// Dapatkan bagan desainer pada lembar pertama.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```
Dengan mengubah nilai indeks, Anda dapat memilih lembar kerja atau bagan yang berbeda jika berkas Anda memiliki lebih banyak.

## Langkah 4: Tambahkan Kotak Teks Baru ke Bagan

Sekarang, kita siap untuk menambahkan TextBox. Kita akan menentukan posisi dan ukurannya saat membuatnya.

```csharp
// Tambahkan kotak teks baru ke bagan.
Aspose.Cells.Drawing.TextBox textbox0 = chart.Shapes.AddTextBoxInChart(400, 1100, 350, 2550);
```
Dalam perintah ini, parameter menentukan lokasi (x, y) dan ukuran (lebar, tinggi) TextBox dalam bagan. Sesuaikan nilai ini berdasarkan kebutuhan tata letak spesifik Anda.

## Langkah 5: Mengatur Teks untuk Kotak Teks

Setelah TextBox terpasang, saatnya untuk mengisinya dengan konten. Anda dapat menambahkan teks apa pun yang Anda anggap perlu untuk bagan Anda.

```csharp
// Isi teksnya.
textbox0.Text = "Sales By Region";
```
Jangan ragu untuk mengganti "Penjualan Berdasarkan Wilayah" dengan teks apa pun yang relevan dengan data Anda.

## Langkah 6: Sesuaikan Properti TextBox

Sekarang, mari kita buat TextBox kita terlihat bagus! Anda dapat menyesuaikan berbagai properti seperti warna, ukuran, dan gaya font.

```csharp
// Mengatur warna font.
textbox0.Font.Color = Color.Maroon; // Ubah ke warna yang Anda inginkan

// Atur font menjadi tebal.
textbox0.Font.IsBold = true;

// Mengatur ukuran font.
textbox0.Font.Size = 14;

// Atur atribut font menjadi miring.
textbox0.Font.IsItalic = true;
```

Masing-masing baris ini mengubah tampilan teks di dalam Kotak Teks Anda, meningkatkan visibilitas dan daya tarik.

## Langkah 7: Format Tampilan Kotak Teks

Penting juga untuk memformat latar belakang dan batas TextBox. Ini akan membuatnya menonjol pada diagram.

```csharp
// Dapatkan format isian kotak teks.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;

// Dapatkan jenis format baris kotak teks.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;

// Tetapkan ketebalan garis.
lineformat.Weight = 2;

// Atur gaya tanda hubung menjadi padat.
lineformat.DashStyle = Aspose.Cells.Drawing.MsoLineDashStyle.Solid;
```

Pilihan ini memungkinkan Anda untuk mengatur isian latar belakang TextBox dan menyesuaikan batasnya.

## Langkah 8: Simpan File Excel yang Telah Dimodifikasi

Langkah terakhir adalah menyimpan perubahan yang telah Anda buat pada file Excel baru. Ini akan memastikan bahwa file asli Anda tetap utuh.

```csharp
// Mentse el az excel fájlt.
workbook.Save(outputDir + "outputAddingTextBoxControlInChart.xls");
```
Csere `"outputAddingTextBoxControlInChart.xls"` dengan nama berkas apa pun yang Anda sukai.

## Következtetés

Selamat! Anda telah berhasil menambahkan kontrol TextBox ke bagan menggunakan Aspose.Cells for .NET. Perubahan sederhana namun efektif ini dapat membuat bagan Anda lebih informatif dan menarik secara visual. Representasi data adalah kunci komunikasi yang efektif, dan dengan alat seperti Aspose, Anda memiliki kekuatan untuk menyempurnakan presentasi tersebut dengan upaya minimal.

## GYIK

### Mi az Aspose.Cells .NET-hez?
Aspose.Cells untuk .NET adalah pustaka yang hebat untuk membuat, memanipulasi, dan mengonversi file Excel tanpa perlu bergantung pada Microsoft Excel.

### Bisakah saya menambahkan beberapa Kotak Teks ke satu bagan?
Ya! Anda dapat menambahkan TextBox sebanyak yang Anda perlukan dengan mengulangi langkah-langkah pembuatan TextBox dengan posisi yang berbeda.

### Ingyenesen használható az Aspose.Cells?
Aspose.Cells adalah pustaka berbayar, tetapi Anda dapat mengunduh versi uji coba gratis dari [itt](https://releases.aspose.com/).

### Hol találok további dokumentációt az Aspose.Cells-ről?
Anda dapat mengakses dokumentasi yang komprehensif [itt](https://reference.aspose.com/cells/net/).

### Bagaimana cara mendapatkan dukungan jika saya mengalami masalah?
Anda dapat mencari bantuan melalui forum dukungan Aspose [itt](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}