---
category: general
date: 2026-09-24
description: Ekspor rentang Excel sebagai gambar di C# menggunakan Aspose.Cells –
  panduan langkah demi langkah untuk menyimpan area lembar kerja sebagai PNG atau
  JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- Aspose.Cells export range
- C# Excel to PNG
- ImageOrPrintOptions usage
- export pivot table as image
language: id
lastmod: 2026-09-24
og_description: Ekspor rentang Excel sebagai gambar di C# dengan Aspose.Cells. Pelajari
  cara mengonversi area lembar kerja apa pun, termasuk tabel pivot, menjadi PNG atau
  JPEG dalam hitungan menit.
og_image_alt: Screenshot of a C# program exporting an Excel range to a PNG image
og_title: Ekspor rentang Excel sebagai gambar dengan C# – panduan lengkap Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  headline: How to export excel range as image with C# and Aspose.Cells
  type: TechArticle
- description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  name: How to export excel range as image with C# and Aspose.Cells
  steps:
  - name: '**Load** the workbook from disk.'
    text: '**Load** the workbook from disk.'
  - name: '**Define** the cell area that will become the image (the *print area*).'
    text: '**Define** the cell area that will become the image (the *print area*).'
  - name: '**Export** the area using `ImageOrPrintOptions` and write the file.'
    text: '**Export** the area using `ImageOrPrintOptions` and write the file.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Image export
title: Cara mengekspor rentang Excel sebagai gambar dengan C# dan Aspose.Cells
url: /id/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengekspor rentang Excel sebagai gambar dengan C# dan Aspose.Cells

Jika Anda perlu **mengekspor rentang excel sebagai gambar** dalam aplikasi .NET, panduan ini menunjukkan solusi lengkap yang siap dijalankan. Baik Anda mempublikasikan dasbor, menyematkan tabel pivot di halaman web, atau menghasilkan thumbnail laporan, Anda dapat mengubah area lembar kerja apa pun menjadi PNG (atau JPEG) dengan hanya beberapa baris kode C#.

Dalam tutorial ini Anda akan belajar cara:

* Muat workbook yang ada (`Workbook` class)  
* Tentukan rentang sel tepat yang ingin Anda tangkap (`PrintArea`)  
* Konfigurasikan opsi ekspor gambar (`ImageOrPrintOptions`)  
* Simpan gambar yang dihasilkan ke disk  

Semua prasyarat, kasus tepi, dan jebakan umum dibahas sehingga Anda dapat menyesuaikan kode ke proyek Anda sendiri tanpa kejutan.

## Prasyarat

| Persyaratan | Alasan |
|-------------|--------|
| **Aspose.Cells for .NET** (latest version) | Menyediakan API `Workbook`, `Worksheet`, dan `ImageOrPrintOptions` yang digunakan dalam contoh. |
| **.NET 6.0 or later** | Contoh ini menargetkan .NET 6, tetapi versi .NET Core/Framework apa pun yang mendukung Aspose.Cells dapat digunakan. |
| **A valid Excel file** (e.g., `input.xlsx`) | Workbook yang ingin Anda konversi. |
| **Write permission to the output folder** | Diperlukan agar `Save` berhasil. |

Anda dapat menginstal Aspose.Cells via NuGet:

```bash
dotnet add package Aspose.Cells
```

## Mengekspor rentang excel sebagai gambar – ikhtisar proses

Operasi ini terdiri dari tiga fase logis:

1. **Load** workbook dari disk.  
2. **Define** area sel yang akan menjadi gambar ( *print area* ).  
3. **Export** area menggunakan `ImageOrPrintOptions` dan menulis file.  

Setiap fase dijabarkan menjadi langkah khusus dengan kode sumber lengkap dan penjelasan.

## Langkah 1: Muat workbook

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Path to the source Excel file
string inputPath = @"YOUR_DIRECTORY\input.xlsx";

// Create a Workbook object – this reads the file into memory
Workbook workbook = new Workbook(inputPath);
```

**Mengapa ini penting:**  
`Workbook` adalah titik masuk untuk semua operasi Excel. Memuat file sekali menjaga penggunaan memori tetap rendah dan memungkinkan Anda mengakses lembar kerja mana pun nanti.

## Langkah 2: Akses lembar kerja target

```csharp
// Get the first worksheet (index 0). Change the index or use the sheet name as needed.
Worksheet sheet = workbook.Worksheets[0];
```

**Tip:** Jika Anda membutuhkan lembar tertentu berdasarkan nama, ganti indeks dengan `workbook.Worksheets["SheetName"]`. Ini menghindari kesalahan ketika tata letak workbook berubah.

## Langkah 3: Tentukan rentang yang ingin Anda ekspor

```csharp
// Define the cell range that will be exported.
// Example: A1:G20 captures a typical pivot‑table area.
sheet.PageSetup.PrintArea = "A1:G20";
```

**Mengapa mengatur `PrintArea`?**  
Aspose.Cells merender *print area* saat membuat gambar. Dengan membatasi ke rentang yang tepat, Anda menghindari ruang putih berlebih dan meningkatkan kinerja.

### Alternatif: Mengekspor seluruh lembar

Jika Anda ingin seluruh lembar kerja, cukup hilangkan penetapan `PrintArea`. Aspose.Cells akan menggunakan rentang yang digunakan pada lembar secara default.

## Langkah 4: Konfigurasikan opsi ekspor gambar

```csharp
// Create an ImageOrPrintOptions object to control the output format.
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    // Choose PNG for lossless quality; change to Jpeg for smaller files.
    ImageFormat = ImageFormat.Png,

    // Optional: set the resolution (DPI). Higher DPI yields sharper images.
    HorizontalResolution = 300,
    VerticalResolution = 300,

    // Optional: set the page orientation if the range is wide.
    PageOrientation = PageOrientationType.Landscape
};
```

**Penjelasan properti utama:**

* `ImageFormat` – Menentukan jenis file (`Png`, `Jpeg`, `Bmp`, dll.). PNG ideal untuk grafik dan teks karena mempertahankan tepi yang tajam.
* `HorizontalResolution` / `VerticalResolution` – Mengontrol kepadatan piksel. Untuk thumbnail web 96 DPI sudah cukup; untuk grafik siap cetak 300 DPI disarankan.
* `PageOrientation` – Membantu ketika rentang yang dipilih lebih lebar daripada tinggi.

## Langkah 5: Ekspor rentang ke file gambar

```csharp
// Define the output path for the image
string outputPath = @"YOUR_DIRECTORY\range.png";

// Save the first picture on the worksheet as an image.
// The Pictures collection is automatically populated after setting PrintArea.
sheet.Pictures[0].Save(outputPath, imgOptions);
```

**Apa yang terjadi di balik layar:**  
Ketika `PrintArea` diatur, Aspose.Cells menghasilkan gambar sementara yang mewakili area tersebut. Objek `Pictures[0]` kemudian disimpan menggunakan opsi yang Anda berikan.

### Menangani lembar kerja tanpa gambar

Jika lembar kerja belum berisi gambar (misalnya file baru), Anda dapat membuatnya secara langsung:

```csharp
// Create a picture from the defined range and add it to the sheet
Picture pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
pic.Save(outputPath, imgOptions);
```

## Contoh lengkap yang dapat dijalankan

Menggabungkan semuanya, berikut adalah aplikasi konsol mandiri yang dapat Anda salin, tempel, dan jalankan:

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // 2️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Define the range to export (e.g., a pivot table)
        sheet.PageSetup.PrintArea = "A1:G20";

        // 4️⃣ Set image export options (PNG, 300 DPI, landscape)
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300,
            PageOrientation = PageOrientationType.Landscape
        };

        // 5️⃣ Save the picture as an image file
        string outputPath = @"YOUR_DIRECTORY\range.png";

        // Ensure a picture exists; create one if necessary
        Picture pic;
        if (sheet.Pictures.Count == 0)
        {
            pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
        }
        else
        {
            pic = sheet.Pictures[0];
        }

        pic.Save(outputPath, imgOptions);

        System.Console.WriteLine($"Export completed: {outputPath}");
    }
}
```

**Output yang diharapkan:**  
File bernama `range.png` muncul di `YOUR_DIRECTORY`. Membukanya menampilkan sel tepat dari **A1 sampai G20** yang dirender sebagai gambar PNG yang tajam.

## Variasi umum dan penanganan kasus tepi

| Skenario | Penyesuaian |
|----------|------------|
| **Export to JPEG** | Ubah `ImageFormat = ImageFormat.Jpeg` dan opsional atur `Quality = 90` (rentang 0‑100). |
| **Multiple ranges** | Panggil `sheet.Pictures.Add` untuk setiap rentang dan simpan setiap gambar dengan nama file yang berbeda. |
| **Large worksheets** | Tingkatkan `HorizontalResolution`/`VerticalResolution` hanya untuk rentang yang diperlukan guna menghindari lonjakan memori. |
| **No picture generated** | Pastikan `PrintArea` diformat dengan benar (`"A1:G20"`). Alamat yang tidak valid menghasilkan koleksi `Pictures` kosong. |
| **Saving to a stream** | Gunakan `pic.Save(Stream, imgOptions)` ketika Anda membutuhkan gambar dalam memori (misalnya untuk respons ASP.NET). |

## Tips profesional untuk ekspor gambar yang handal

* **Validasi area cetak** – Gunakan parsing `CellArea` (`CellArea area = CellArea.CreateCellArea("A1", "G20")`) untuk membangun rentang secara programatik dan menghindari kesalahan ketik.  
* **Bebaskan sumber daya** – Bungkus `Workbook` dalam blok `using` jika Anda memproses banyak file untuk segera membebaskan sumber daya native.  
* **Pemrosesan batch** – Saat mengekspor puluhan rentang, gunakan kembali satu instance `ImageOrPrintOptions` untuk mengurangi overhead alokasi objek.  
* **Keamanan thread** – Objek Aspose.Cells **tidak** thread‑safe. Buat `Workbook` terpisah per thread atau sinkronkan akses.  

## Kesimpulan

Anda kini memiliki metode lengkap yang siap produksi untuk **mengekspor rentang excel sebagai gambar** menggunakan C# dan Aspose.Cells. Langkah‑langkah—memuat workbook, mengatur area cetak, mengonfigurasi `ImageOrPrintOptions`, dan menyimpan gambar—mencakup baik “bagaimana” maupun “mengapa”, memastikan Anda dapat menyesuaikan kode untuk tabel pivot, grafik, atau blok sel khusus apa pun.

Selanjutnya, Anda mungkin ingin menjelajahi:

* **Mengekspor rentang excel sebagai gambar** dalam format lain (SVG, BMP) – kata kunci sekunder lain untuk dicoba.  
* **Menyematkan PNG ke dalam PDF** menggunakan Aspose.PDF untuk pembuatan laporan end‑to‑end.  
* **Mengotomatiskan ekspor batch** pada banyak workbook dengan loop konsol sederhana.  

Silakan bereksperimen dengan resolusi, orientasi, dan direktori output yang berbeda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}