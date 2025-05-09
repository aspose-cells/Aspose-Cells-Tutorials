---
"date": "2025-04-05"
"description": "Pelajari cara menambahkan dan menyesuaikan bentuk oval di Excel menggunakan Aspose.Cells for .NET. Sempurnakan presentasi data Anda dengan mudah."
"title": "Menambahkan Bentuk Oval ke Excel dengan Aspose.Cells untuk .NET | Panduan Langkah demi Langkah"
"url": "/id/net/images-shapes/add-oval-shapes-excel-aspose-cells-dotnet/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Cara Menambahkan Bentuk Oval ke Lembar Kerja Excel Menggunakan Aspose.Cells untuk .NET

## Bevezetés

Dalam dunia presentasi data, membuat lembar Excel Anda menarik secara visual dapat meningkatkan pemahaman dan keterlibatan secara signifikan. Menambahkan bentuk khusus seperti oval tidak selalu mudah dengan fungsi Excel dasar. **Aspose.Cells .NET-hez** menyediakan cara yang hebat untuk memasukkan dan menyesuaikan bentuk oval secara terprogram dalam lembar kerja Anda. Panduan langkah demi langkah ini akan menunjukkan kepada Anda cara memanfaatkan Aspose.Cells untuk menambahkan bentuk oval ke berkas Excel Anda secara efisien.

### Amit tanulni fogsz:
- Az Aspose.Cells beállítása a .NET projektben
- Proses penambahan dan konfigurasi bentuk oval di lembar kerja Excel
- Opsi penyesuaian utama untuk bentuk oval
- Praktik terbaik untuk mengintegrasikan fitur-fitur ini ke dalam proyek yang lebih besar

Mari selami prasyaratnya sebelum memulai coding!

## Előfeltételek

Sebelum Anda dapat mulai menambahkan oval ke lembar kerja Anda, pastikan Anda memiliki hal berikut:

- **Aspose.Cells .NET-hez**: Pustaka hebat yang memungkinkan manipulasi file Excel secara ekstensif.
  - Untuk instalasi, gunakan salah satu dari berikut ini:
    - **.NET parancssori felület**:
      ```bash
dotnet csomag hozzáadása Aspose.Cells
```
    - **Package Manager**:
      ```powershell
PM> NuGet\Install-Package Aspose.Cells
```
- **Fejlesztői környezet**Pastikan Anda telah menyiapkan lingkungan pengembangan .NET yang sesuai, seperti Visual Studio atau VS Code dengan .NET SDK.
- **Pengetahuan Dasar tentang C# dan .NET Frameworks**:Keakraban dengan konsep pemrograman berorientasi objek dalam C# akan sangat membantu.

## Az Aspose.Cells beállítása .NET-hez

Menyiapkan Aspose.Cells mudah. Ikuti langkah-langkah berikut untuk memulai:

1. **Telepítse a csomagot**:
   Gunakan perintah yang disediakan di atas untuk menginstal paket Aspose.Cells ke dalam proyek Anda.
   
2. **Licencszerzés**:
   - Kezdheted egy [ingyenes próba](https://releases.aspose.com/cells/net/) untuk menguji fungsionalitas.
   - Untuk fitur yang diperluas, pertimbangkan untuk mendapatkan lisensi sementara atau membelinya melalui [Az Aspose vásárlási oldala](https://purchase.aspose.com/buy).

3. **Inicializálás**:
   Setelah terinstal dan dilisensikan, Anda dapat menginisialisasi Aspose.Cells di aplikasi Anda:
   
   ```csharp
menggunakan Aspose.Cells;
```

With the environment set up, let's move on to implementing oval shapes.

## Implementation Guide

### Adding an Oval Shape

This feature guides you through adding a basic oval shape to an Excel worksheet.

#### Overview
Adding ovals can enhance the visual appeal of your data presentation. In this section, we'll add and configure an oval in the first worksheet of our Excel file using Aspose.Cells.

#### Steps:

##### Step 1: Define Directory for Output

First, define where you want to save your output files:

```csharp
string SourceDir = "YOUR_SOURCE_DIRECTORY";
string outputDir = "YOUR_OUTPUT_DIRECTORY";
string dataDir = Path.Combine(outputDir, "OvalShapeExample");

if (!Directory.Exists(dataDir))
    Directory.CreateDirectory(dataDir);
```

##### Langkah 2: Buat Instansiasi Buku Kerja

Hozz létre egy példányt a `Workbook` kelas untuk mulai bekerja dengan file Excel:

```csharp
Workbook excelbook = new Workbook();
```

##### Langkah 3: Tambahkan Bentuk Oval

Használd a `AddOval` metode untuk menempatkan bentuk oval di lembar kerja:

```csharp
// Tambahkan oval pada koordinat dan ukuran yang ditentukan
Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```

##### Langkah 4: Konfigurasikan Penempatan

Atur jenis penempatan ke `FreeFloating` untuk kontrol lebih lanjut atas posisi:

```csharp
oval1.Placement = PlacementType.FreeFloating;
```

##### Langkah 5: Tetapkan Properti Garis

Sesuaikan tampilan garis luar oval dengan mengatur ketebalan garis dan gaya garis putus-putus:

```csharp
// Atur ketebalan garis dan gaya garis putus-putus
oval1.Line.Weight = 1;
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```

##### Langkah 6: Simpan Buku Kerja

Terakhir, simpan buku kerja Anda ke file di direktori yang ditentukan:

```csharp
excelbook.Save(Path.Combine(dataDir, "OvalShapeExample.xls"));
```

#### Hibaelhárítási tippek:
- Pastikan semua jalur direktori diatur dengan benar untuk mencegah kesalahan file tidak ditemukan.
- Periksa apakah Aspose.Cells memiliki lisensi yang sesuai jika Anda menggunakan fitur di luar batasan uji coba.

### Menambahkan Bentuk Oval Lain (Lingkaran)

Sekarang mari tambahkan bentuk oval lain, yang dikonfigurasikan sebagai lingkaran, dengan properti yang berbeda.

#### Áttekintés
Menambahkan beberapa bentuk dapat membantu dalam menciptakan visualisasi yang lebih kompleks. Di sini, kami akan menunjukkan cara menambahkan bentuk oval melingkar ke lembar kerja Anda.

#### Lépések:

##### Langkah 1: Pastikan Direktori Ada

Langkah ini mirip dengan bagian sebelumnya; pastikan direktori Anda diatur dengan benar.

```csharp
if (!Directory.Exists(dataDir))
    Directory.CreateDirectory(dataDir);
```

##### 2. lépés: Munkafüzet példányosítása

Hozz létre egy újat `Workbook` contoh untuk penambahan bentuk ini:

```csharp
Workbook excelbook = new Workbook();
```

##### Langkah 3: Tambahkan Bentuk Lingkaran

Tambahkan oval lain dengan dimensi untuk membuatnya tampak seperti lingkaran:

```csharp
// Tambahkan bentuk lingkaran pada koordinat dan ukuran yang berbeda
Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```

##### Langkah 4: Konfigurasikan Penempatan

Tetapkan jenis penempatan untuk bentuk baru:

```csharp
oval2.Placement = PlacementType.FreeFloating;
```

##### Langkah 5: Tetapkan Properti Garis

Tentukan ketebalan garis dan gaya garis putus-putus untuk penyesuaian:

```csharp
// Sesuaikan properti garis
oval2.Line.Weight = 1;
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```

##### Langkah 6: Simpan Buku Kerja dengan Bentuk Baru

Simpan buku kerja lagi, kali ini termasuk kedua bentuk:

```csharp
excelbook.Save(Path.Combine(dataDir, "OvalShapeExampleWithCircle.xls"));
```

## Gyakorlati alkalmazások

Aspose.Cells memungkinkan berbagai aplikasi praktis untuk menambahkan bentuk oval ke lembar kerja Excel:

1. **Adatvizualizáció**: Tingkatkan bagan data dengan anotasi berbentuk khusus.
2. **Desain Dasbor**: Gunakan oval untuk menyorot metrik atau bagian utama di dasbor keuangan.
3. **Sablon létrehozása**: Bangun templat yang dapat digunakan kembali untuk laporan yang memerlukan elemen visual yang konsisten.

Kasus penggunaan ini menunjukkan fleksibilitas Aspose.Cells di lingkungan profesional dan bisnis.

## Teljesítménybeli szempontok

Saat bekerja dengan kumpulan data besar atau lembar kerja yang kompleks, mengoptimalkan kinerja sangatlah penting:

- **Hatékony memóriakezelés**: Pastikan pembuangan objek dilakukan dengan benar untuk mengosongkan memori.
- **Kötegelt műveletek**: Lakukan operasi secara berkelompok jika memungkinkan untuk meminimalkan waktu pemrosesan.
- **Pemanfaatan Sumber Daya**Memantau penggunaan sumber daya dan mengoptimalkan jalur kode yang memerlukan banyak komputasi.

Mengikuti praktik terbaik ini dapat membantu menjaga kinerja lancar saat menggunakan Aspose.Cells untuk manipulasi Excel yang ekstensif.

## Következtetés

Dalam tutorial ini, kami mengeksplorasi cara menambahkan dan mengonfigurasi bentuk oval di lembar kerja Excel menggunakan Aspose.Cells untuk .NET. Dengan mengikuti langkah-langkah yang diuraikan, Anda dapat menyempurnakan presentasi data dengan visual khusus dengan mudah. Untuk eksplorasi lebih lanjut, pertimbangkan untuk mendalami fitur Aspose.Cells yang lebih canggih atau mengintegrasikan teknik ini ke dalam proyek yang lebih besar.

## GYIK szekció

1. **Használhatom az Aspose.Cells-t licenc nélkül?**
   - Ya, tetapi dengan beberapa batasan. Versi uji coba tersedia untuk tujuan pengujian.
2. **Bagaimana cara mengubah warna bentuk oval?**
   - Használd a `FillFormat` properti untuk menyesuaikan warna dan gaya isian.
3. **Apakah mungkin untuk menambahkan teks di dalam bentuk oval?**
   - Ya, Anda dapat menyisipkan bentuk teks dalam oval menggunakan API Aspose.Cells.
4. **Automatizálhatom ezt a folyamatot több fájlra vonatkozóan?**
   - Tentu saja, ulangi set berkas Anda dan terapkan metode ini secara terprogram.
5. **Milyen rendszerkövetelmények szükségesek az Aspose.Cells futtatásához?**
   - Mendukung .NET Framework 2.0 dan di atasnya, termasuk .NET Core dan .NET 5/6.

## Erőforrás
- [Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/)
- [Aspose.Cells letöltése .NET-hez](https://releases.aspose.com/cells/net/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}