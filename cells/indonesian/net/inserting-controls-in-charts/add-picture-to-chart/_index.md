---
title: Tambahkan Gambar ke Bagan
linktitle: Tambahkan Gambar ke Bagan
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mudah menambahkan gambar ke bagan Excel menggunakan Aspose.Cells for .NET. Sempurnakan bagan dan presentasi Anda hanya dalam beberapa langkah mudah.
weight: 11
url: /id/net/inserting-controls-in-charts/add-picture-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Gambar ke Bagan

## Perkenalan

Apakah Anda bosan dengan bagan yang membosankan dan kurang memiliki sentuhan pribadi? Ingin mempelajari cara mempercantik tampilan Excel Anda dengan menambahkan gambar? Nah, Anda beruntung! Dalam tutorial ini, kita akan menyelami dunia Aspose.Cells untuk .NET dan mempelajari cara menambahkan gambar ke bagan di Excel. Jadi, ambil secangkir kopi favorit Anda, dan mari kita mulai!

## Prasyarat

Sebelum kita masuk ke inti coding, ada beberapa prasyarat yang perlu Anda ikuti agar dapat berjalan lancar:

- Visual Studio: Di sinilah Anda akan menulis dan menjalankan kode .NET. Pastikan Anda telah menginstalnya.
-  Aspose.Cells untuk .NET: Anda memerlukan pustaka ini untuk bekerja dengan file Excel. Anda dapat[unduh disini](https://releases.aspose.com/cells/net/).
- Pemahaman Dasar C#: Sementara saya akan memandu Anda melalui kodenya, memahami dasar-dasar C# akan membuat segalanya lebih jelas.

### Langkah-langkah Instalasi

1. Instal Aspose.Cells: Anda dapat menambahkan Aspose.Cells ke proyek Visual Studio Anda melalui NuGet Package Manager. Lakukan ini dengan membuka Tools > NuGet Package Manager > Manage NuGet Packages for Solution dan cari “Aspose.Cells.” Klik Instal.
2. Menyiapkan Proyek Anda: Buat proyek aplikasi konsol C# baru di Visual Studio.

## Paket Impor

Setelah semuanya siap, langkah selanjutnya adalah mengimpor paket yang diperlukan ke dalam proyek Anda. Berikut cara melakukannya:

### Impor Namespace yang Diperlukan

Di bagian atas berkas kode C# Anda, Anda perlu mengimpor namespace berikut:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

Ini memberi tahu program Anda, “Hai! Saya akan menggunakan fitur-fitur keren ini dari Aspose.Cells.”

Sekarang setelah prasyaratnya terpenuhi, mari kita uraikan prosesnya menjadi beberapa langkah kecil. 

## Langkah 1: Tentukan Direktori Anda

Pertama-tama, kita perlu mengatur jalur untuk berkas masukan dan keluaran. Langkah ini penting karena kita perlu mengetahui di mana menemukan berkas Excel yang sudah ada dan di mana menyimpan berkas yang dimodifikasi.

```csharp
//Direktori sumber
string sourceDir = "Your Document Directory/";

//Direktori keluaran
string outputDir = "Your Output Directory/";
```

 Mengganti`Your Document Directory` Dan`Your Output Directory` dengan jalur sebenarnya di komputer Anda. 

## Langkah 2: Muat Buku Kerja yang Ada

Sekarang, mari muat berkas Excel yang ada di mana kita ingin menambahkan gambar ke dalam bagan.

```csharp
// Buka berkas yang ada.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

Kode ini membuka buku kerja, membuatnya siap untuk diedit.

## Langkah 3: Siapkan Aliran Gambar

Sebelum menambahkan gambar, kita perlu membaca gambar yang ingin kita masukkan ke dalam bagan. 

```csharp
// Dapatkan berkas gambar ke aliran.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Pastikan Anda menyimpan gambar di direktori yang ditentukan.

## Langkah 4: Targetkan Grafik

Sekarang, mari tentukan diagram mana yang akan kita tambahkan gambar. Dalam contoh ini, kita akan menargetkan diagram pertama pada lembar kerja pertama.

```csharp
// Dapatkan bagan desainer di lembar kedua.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Anda dapat mengakses lembar kerja mana pun dengan mengubah indeksnya.

## Langkah 5: Tambahkan Gambar ke Bagan

Setelah bagan dipilih, waktunya menambahkan gambar! 

```csharp
// Tambahkan gambar baru ke bagan.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

 Di Sini,`50` Dan`50` adalah koordinat X dan Y di mana gambar akan ditempatkan, dan`200` adalah lebar dan tinggi gambar.

## Langkah 6: Sesuaikan Format Garis Gambar

Ingin menambahkan sedikit gaya pada gambar Anda? Anda dapat menyesuaikan pinggirannya! Berikut cara melakukannya:

```csharp
// Dapatkan jenis format garis gambar.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Mengatur gaya tanda hubung.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Tetapkan ketebalan garis.
lineformat.Weight = 4;    
```

Cuplikan ini memungkinkan Anda memilih tampilan dan ketebalan bingkai. Pilih gaya apa pun yang sesuai dengan presentasi Anda!

## Langkah 7: Simpan Buku Kerja yang Dimodifikasi

Setelah semua kerja keras itu, mari simpan modifikasi Anda dengan mengeksekusi baris kode berikut:

```csharp
// Simpan berkas excel.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Sekarang gambar Anda berhasil diintegrasikan ke dalam bagan, dan berkas keluaran Anda siap untuk dilihat!

## Langkah 8: Tunjukkan Keberhasilan

Terakhir, Anda dapat menambahkan pesan sederhana untuk mengonfirmasi bahwa operasi Anda berhasil:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Kesimpulan

Dalam tutorial ini, kami telah menjajaki cara menambahkan sedikit kepribadian ke dalam bagan Excel Anda dengan menambahkan gambar menggunakan Aspose.Cells for .NET. Hanya dengan beberapa langkah sederhana, Anda dapat mengubah presentasi Anda dari biasa menjadi berkesan. Jadi, tunggu apa lagi? Cobalah dan biarkan bagan Anda bersinar!

## Pertanyaan yang Sering Diajukan

### Bisakah saya menambahkan beberapa gambar ke satu bagan?
 Ya! Anda dapat menelepon`AddPictureInChart` metode beberapa kali untuk menambahkan gambar sebanyak yang Anda inginkan.

### Format gambar apa yang didukung Aspose.Cells?
Aspose.Cells mendukung berbagai format gambar, termasuk PNG, JPEG, BMP, dan GIF.

### Bisakah saya menyesuaikan posisi gambar?
 Tentu saja! Koordinat X dan Y di`AddPictureInChart` metode memungkinkan penentuan posisi yang tepat.

### Apakah Aspose.Cells gratis untuk digunakan?
Aspose.Cells menawarkan uji coba gratis, tetapi untuk fitur lengkap, diperlukan lisensi. Anda dapat menemukan harganya[Di Sini](https://purchase.aspose.com/buy).

### Di mana saya dapat menemukan lebih banyak contoh?
 Lihat di sini[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) untuk contoh dan fungsi yang lebih rinci.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
