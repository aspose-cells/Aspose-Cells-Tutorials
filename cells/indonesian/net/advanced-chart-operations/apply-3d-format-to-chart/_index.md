---
"description": "Temukan cara membuat grafik 3D yang menakjubkan di Excel menggunakan Aspose.Cells for .NET. Ikuti panduan langkah demi langkah kami yang mudah."
"linktitle": "Terapkan Format 3D ke Bagan"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Terapkan Format 3D ke Bagan"
"url": "/id/net/advanced-chart-operations/apply-3d-format-to-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Terapkan Format 3D ke Bagan

## Bevezetés

Di era di mana visualisasi data menjadi hal yang terpenting, cara kita menyajikan data tidak hanya terbatas pada grafik dan bagan dasar. Dengan alat seperti Aspose.Cells for .NET, Anda dapat meningkatkan penyajian data dengan bagan 3D yang memukau yang tidak hanya menarik perhatian tetapi juga menyampaikan informasi secara efektif. Panduan ini akan memandu Anda melalui langkah-langkah untuk menerapkan format 3D ke bagan menggunakan Aspose.Cells, mengubah data mentah Anda menjadi tampilan yang menarik.

## Előfeltételek

Sebelum kita menyelami seluk-beluk penerapan format 3D ke bagan, mari pastikan Anda memiliki semua yang dibutuhkan.

### Persyaratan Perangkat Lunak

- Visual Studio: Pastikan Anda telah menginstal Visual Studio untuk bekerja dengan aplikasi .NET.
- Aspose.Cells untuk .NET: Jika Anda belum melakukannya, unduh dan instal Aspose.Cells dari [itt](https://releases.aspose.com/cells/net/).

### Pengaturan Lingkungan Pengkodean

1. Buat Proyek .NET baru: Buka Visual Studio, pilih “Buat proyek baru,” lalu pilih Aplikasi Konsol.
2. Tambahkan Referensi Aspose.Cells: Melalui NuGet Package Manager, tambahkan Aspose.Cells dengan mencarinya atau melalui Konsol Package Manager:

```bash
Install-Package Aspose.Cells
```

3. Siapkan Direktori Output: Tentukan direktori output tempat file yang Anda buat akan disimpan—ini bisa semudah membuat folder di desktop Anda.

Sekarang semuanya sudah siap, waktunya untuk masuk ke kode dan membuat beberapa grafik 3D yang menakjubkan!

## Csomagok importálása

Untuk memulai, Anda perlu mengimpor namespace yang diperlukan. Ini akan membantu Anda mengakses kelas dan metode yang disediakan oleh Aspose.Cells. Berikut cara melakukannya:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Bagian ini akan menguraikan proses menjadi beberapa langkah yang dapat dikelola, memberikan Anda pemahaman yang jelas tentang setiap tahapan.

## 1. lépés: A munkafüzet inicializálása

Pertama, Anda perlu membuat instance dari `Workbook` kelas. Objek ini akan berfungsi sebagai dasar untuk dokumen Excel Anda.

```csharp
//Kimeneti könyvtár
string outputDir = "Your Document Directory";
Workbook book = new Workbook();
```
Pikirkanlah hal ini `Workbook` sebagai kanvas kosong—siap untuk Anda isi dengan data berwarna dan visualisasi yang berdampak.

## Langkah 2: Ganti Nama Lembar Kerja Pertama

Selanjutnya, mari kita ganti nama lembar kerja pertama. Ini akan memberikan kejelasan tentang data apa yang sedang kita kerjakan.

```csharp
book.Worksheets[0].Name = "DataSheet";
```

Nama harus intuitif. Dalam kasus ini, kami menamakannya "DataSheet" agar kami tahu di mana data kami berada.

## Langkah 3: Buat Data untuk Bagan

Sekarang, kita akan menambahkan beberapa data ke "DataSheet" kita. Mari kita isi dengan nilai-nilai yang akan digunakan oleh diagram kita.

```csharp
Worksheet dataSheet = book.Worksheets["DataSheet"];
dataSheet.Cells["B1"].PutValue(1);
dataSheet.Cells["B2"].PutValue(2);
dataSheet.Cells["B3"].PutValue(3);
dataSheet.Cells["A1"].PutValue("A");
dataSheet.Cells["A2"].PutValue("B");
dataSheet.Cells["A3"].PutValue("C");
```

Sama seperti resep yang bergantung pada bahan-bahannya, efektivitas bagan Anda bergantung pada kualitas dan organisasi data masukan Anda.

## Langkah 4: Siapkan Lembar Kerja Bagan Baru

Saatnya membuat lembar kerja baru untuk bagan itu sendiri. Ini membantu menjaga visualisasi data Anda tetap teratur.

```csharp
Worksheet sheet = book.Worksheets.Add("MyChart");
```

Anggap lembar kerja ini sebagai tahap Anda—tempat kinerja data Anda terungkap.

## Langkah 5: Tambahkan Bagan

Di sini, kita akan menambahkan bagan kolom ke lembar kerja yang baru dibuat.  

```csharp
ChartCollection charts = sheet.Charts;
int chartSheetIdx = charts.Add(ChartType.Column, 5, 0, 25, 15);
```

Kami mendefinisikan ruang untuk bagan kami dan menentukan jenisnya. Anggap saja seperti memilih jenis bingkai untuk karya seni Anda.

## Langkah 6: Sesuaikan Tampilan Bagan

Sekarang, mari sesuaikan tampilan grafik kita dengan mengatur warna latar belakang. 

```csharp
Aspose.Cells.Charts.Chart chart = book.Worksheets["MyChart"].Charts[0];
chart.PlotArea.Area.BackgroundColor = Color.White;
chart.ChartArea.Area.BackgroundColor = Color.White;
chart.PlotArea.Area.ForegroundColor = Color.White;
chart.ChartArea.Area.ForegroundColor = Color.White;
chart.ShowLegend = false;
```

Latar belakang putih bersih sering kali membuat warna data Anda menonjol, meningkatkan visibilitas.

## 7. lépés: Adatsorok hozzáadása a diagramhoz

Saatnya memasukkan data ke dalam bagan kita. Kita akan menambahkan rangkaian data dari "Lembar Data" kita untuk memastikan bagan kita mencerminkan data yang kita butuhkan.

```csharp
chart.NSeries.Add("DataSheet!B1:B3", true);
chart.NSeries.CategoryData = "DataSheet!A1:A3";
```

Ini sama saja dengan seorang koki yang menyiapkan hidangan dengan bahan-bahan tertentu. Setiap poin data penting!

## Langkah 8: Akses dan Format Seri Data

Sekarang setelah data kita terhubung, mari ambil rangkaian data dan mulai menerapkan beberapa efek 3D.

```csharp
Aspose.Cells.Charts.Series ser = chart.NSeries[0];
ShapePropertyCollection spPr = ser.ShapeProperties;
Format3D fmt3d = spPr.Format3D;
```

Kami bersiap untuk menambahkan sedikit cita rasa pada masakan kami—anggap saja itu sebagai bumbu yang meningkatkan rasa keseluruhan.

## Langkah 9: Terapkan Efek Bevel 3D

Berikutnya, kita akan menambahkan efek bevel untuk memberikan dimensi pada diagram kita.

```csharp
Bevel bevel = fmt3d.TopBevel;
bevel.Type = BevelPresetType.Circle;
bevel.Height = 2;
bevel.Width = 5;
```

Seperti halnya seorang pematung membentuk batu, kita menciptakan kedalaman yang membuat bagan kita menjadi hidup!

## Langkah 10: Sesuaikan Material Permukaan dan Pencahayaan

Mari kita buat grafik kita bersinar terang! Kita akan menyesuaikan material permukaan dan pengaturan pencahayaan.

```csharp
fmt3d.SurfaceMaterialType = PresetMaterialType.WarmMatte;
fmt3d.SurfaceLightingType = LightRigType.ThreePoint;
fmt3d.LightingAngle = 20;
```

Pencahayaan dan material yang tepat dapat mengubah objek datar menjadi visual yang memikat. Bayangkan set film yang pencahayaannya dirancang khusus untuk menyempurnakan setiap adegan.

## Langkah 11: Sentuhan Akhir pada Penampilan Seri

Sekarang untuk menyelesaikan tampilan rangkaian data kita dengan menyesuaikan warnanya.

```csharp
ser.Area.BackgroundColor = Color.Maroon;
ser.Area.ForegroundColor = Color.Maroon;
ser.Border.Color = Color.Maroon;
```

Warna yang tepat dapat membangkitkan perasaan dan reaksi tertentu—merah marun menambahkan sentuhan keanggunan dan kecanggihan.

## Langkah 12: Simpan Buku Kerja Anda

Akhirnya, saatnya menyimpan karya agung Anda! Jangan lupa untuk menentukan lokasi penyimpanannya.

```csharp
book.Save(outputDir + "outputApplying3DFormat.xlsx");
Console.WriteLine("Applying3DFormat executed successfully.");
```

Menyimpan hasil karya Anda seperti memajang karya seni Anda di galeri; momen yang patut dikenang dan dibagikan.

## Következtetés

Selamat! Anda telah berhasil membuat bagan 3D yang menarik secara visual menggunakan Aspose.Cells for .NET. Dengan mengikuti langkah-langkah ini, Anda kini memiliki alat yang hebat untuk menyempurnakan presentasi data Anda, membuatnya tidak hanya informatif tetapi juga memikat secara visual. Saat Anda menyempurnakan bagan Anda, ingatlah bahwa setiap visualisasi adalah sebuah cerita—buatlah menarik, jelas, dan berdampak!

## GYIK

### Mi az Aspose.Cells .NET-hez?
Aspose.Cells untuk .NET adalah pustaka hebat yang memungkinkan pengembang untuk memanipulasi dokumen Excel secara terprogram, termasuk membuat bagan dan diagram.

### Bisakah saya menyesuaikan jenis bagan di Aspose.Cells?
Ya! Aspose.Cells mendukung berbagai jenis bagan seperti Kolom, Garis, Pai, dan masih banyak lagi, yang dapat disesuaikan dengan mudah.

### Van ingyenes próbaverzió az Aspose.Cells-hez?
Tentu saja! Anda dapat mengunduh uji coba gratis dari [itt](https://releases.aspose.com/).

### Bisakah saya menerapkan efek lain ke grafik selain format 3D?
Ya, Anda dapat menerapkan berbagai efek seperti bayangan, gradien, dan gaya berbeda untuk menyempurnakan bagan Anda di luar 3D.

### Hol találok támogatást az Aspose.Cells-hez?
Támogatásért látogassa meg a következőt: [Aspose Fórum](https://forum.aspose.com/c/cells/9) untuk bantuan dan pertolongan masyarakat.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}