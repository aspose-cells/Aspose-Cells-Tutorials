---
"date": "2025-04-05"
"description": "Pelajari cara membuat dan menyesuaikan buku kerja Excel dengan diagram pai menggunakan Aspose.Cells untuk .NET. Ikuti panduan langkah demi langkah ini untuk menyempurnakan tugas visualisasi data Anda secara efisien."
"title": "Membuat Buku Kerja Excel dengan Bagan Pai Menggunakan Aspose.Cells .NET - Panduan Lengkap"
"url": "/id/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Membuat Buku Kerja Excel dengan Bagan Pai Menggunakan Aspose.Cells .NET

## Bevezetés

Dalam dunia yang digerakkan oleh data saat ini, visualisasi informasi yang efektif sangatlah penting. Baik Anda mengelola data penjualan atau menganalisis metrik kinerja regional, diagram pai yang dibuat dengan baik di Excel dapat membuat wawasan Anda lebih mudah dipahami dan berdampak. Membuat diagram ini secara manual dapat memakan waktu. Gunakan Aspose.Cells for .NET—pustaka canggih yang menyederhanakan pembuatan laporan Excel dinamis secara terprogram.

Tutorial ini akan memandu Anda melalui proses pembuatan buku kerja Excel dari awal, mengisinya dengan data, dan menambahkan diagram pai yang menarik—semuanya menggunakan C#. Panduan ini dirancang khusus bagi mereka yang ingin memanfaatkan Aspose.Cells untuk .NET, menjadikan tugas visualisasi data Anda lancar dan efisien.

**Amit tanulni fogsz:**
- Cara mengatur Aspose.Cells di proyek .NET Anda.
- Langkah-langkah untuk membuat buku kerja Excel baru dan mengisinya dengan contoh data penjualan.
- Teknik untuk menambahkan dan menyesuaikan diagram lingkaran menggunakan Aspose.Cells.
- Praktik terbaik untuk mengoptimalkan kinerja saat menangani kumpulan data besar.

Mari kita mulai dengan membahas prasyarat yang Anda perlukan sebelum memulai perjalanan ini.

## Előfeltételek

Mielőtt elkezdenénk, győződjünk meg arról, hogy a következőkkel rendelkezünk:

### Kötelező könyvtárak
- **Aspose.Cells .NET-hez**: Pustaka ini memungkinkan pembuatan dan manipulasi file Excel yang lancar dalam aplikasi .NET.
- **Visual Studio atau IDE C# apa pun**Pastikan lingkungan Anda disiapkan untuk mendukung pengembangan .NET.

### Környezeti beállítási követelmények
- .NET Framework 4.6.1 atau yang lebih baru, atau .NET Core/5+/6+ untuk kompatibilitas lintas platform.

### Ismereti előfeltételek
- C# programozás alapjainak ismerete.
- Kemampuan menggunakan operasi Excel (opsional namun membantu).

## Az Aspose.Cells beállítása .NET-hez

Untuk memulai, Anda perlu memasang pustaka Aspose.Cells di proyek Anda. Berikut cara melakukannya:

**.NET parancssori felület használata:**
```bash
dotnet add package Aspose.Cells
```

**A csomagkezelő használata:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### Licencszerzés

Az Aspose különböző licencelési lehetőségeket kínál:
- **Ingyenes próbaverzió**: Uji pustaka dengan beberapa batasan.
- **Ideiglenes engedély**: Dapatkan lisensi sementara untuk pengujian ekstensif.
- **Vásárlás**: Dapatkan lisensi penuh untuk penggunaan komersial.

Untuk menginisialisasi dan mengatur, cukup tambahkan:
```csharp
using Aspose.Cells;
```

## Megvalósítási útmutató

Kami akan membagi proses ini menjadi beberapa bagian logis berdasarkan fitur. Setiap bagian akan memberikan ikhtisar yang diikuti dengan petunjuk langkah demi langkah dengan potongan kode.

### Membuat dan Mengisi Buku Kerja

**Áttekintés**Fitur ini menunjukkan cara membuat buku kerja baru, mengakses lembar kerja pertamanya, mengatur nama lembar, dan mengisinya dengan data.

1. **Új munkafüzet létrehozása**
   
   ```csharp
   string SourceDir = "YOUR_SOURCE_DIRECTORY";
   string outputDir = "YOUR_OUTPUT_DIRECTORY";

   Workbook workbook = new Workbook();
   ```

2. **Akses Lembar Kerja Pertama dan Nama Set**
   
   ```csharp
   Worksheet sheet = workbook.Worksheets[0];
   sheet.Name = "Data";
   ```

3. **Mengisi Lembar Kerja dengan Data**
   
   ```csharp
   Cells cells = sheet.Cells;
   cells["A1"].PutValue("Region");
   // Mengisi data wilayah
   cells["A2"].PutValue("France");
   // Lanjutkan untuk wilayah lain...

   cells["B1"].PutValue("Sale");
   // Mengisi angka penjualan
   cells["B2"].PutValue(70000);
   ```

### Menambahkan Lembar Bagan dan Membuat Bagan Pai

**Áttekintés**: Pelajari cara menambahkan lembar bagan baru, membuat bagan pai, dan mengatur properti dasarnya.

1. **Tambahkan Lembar Bagan Baru**
   
   ```csharp
   int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
   Worksheet chartSheet = workbook.Worksheets[sheetIndex];
   chartSheet.Name = "Chart";
   ```

2. **Membuat Diagram Lingkaran**
   
   ```csharp
   int chartIndex = chartSheet.Charts.Add(ChartType.Pie, 5, 0, 25, 10);
   Chart chart = chartSheet.Charts[chartIndex];
   ```

### Mengonfigurasi Properti Bagan

**Áttekintés**: Sesuaikan area plot, judul, dan properti seri diagram pai Anda.

1. **Konfigurasikan Area dan Judul Plot**
   
   ```csharp
   chart.PlotArea.Area.ForegroundColor = Color.Coral;
   chart.Title.Text = "Sales By Region";
   chart.Title.Font.Color = Color.Blue;
   ```

2. **Tetapkan Properti Seri**
   
   ```csharp
   chart.NSeries.Add("Data!B2:B8", true);
   chart.NSeries.CategoryData = "Data!A2:A8";
   chart.NSeries.IsColorVaried = true;
   ```

### Menetapkan Label Data untuk Seri Bagan

**Áttekintés**: Sempurnakan diagram lingkaran Anda dengan menambahkan label data ke setiap seri.

1. **Tambahkan Label Data**
   
   ```csharp
   for (int i = 0; i < chart.NSeries.Count; i++) {
       DataLabels datalabels = chart.NSeries[i].DataLabels;
       datalabels.Position = LabelPositionType.InsideBase;
       datalabels.ShowCategoryName = true;
       datalabels.ShowValue = true;
   }
   ```

### Menyesuaikan Area dan Legenda Bagan

**Áttekintés**: Personalisasi lebih lanjut diagram lingkaran Anda dengan menyesuaikan area diagram dan properti legenda.

1. **Sesuaikan Area Bagan**
   
   ```csharp
   ChartArea chartarea = chart.ChartArea;
   chartarea.Area.Formatting = FormattingType.Custom;
   chartarea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
   ```

2. **Ubah Properti Legenda**
   
   ```csharp
   Legend legend = chart.Legend;
   legend.Position = LegendPositionType.Left;
   legend.Font.IsBold = true;
   legend.Border.Color = Color.Blue;
   ```

### A munkafüzet mentése

**Áttekintés**: Simpan buku kerja Anda dengan semua bagan dan data yang telah Anda konfigurasikan.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Gyakorlati alkalmazások

Berikut adalah beberapa kasus penggunaan dunia nyata di mana pembuatan buku kerja Excel dengan diagram lingkaran dapat sangat berguna:

1. **Analisis Kinerja Penjualan**: Visualisasikan data penjualan regional untuk mengidentifikasi wilayah dengan kinerja terbaik.
2. **Alokasi Anggaran**: Menampilkan distribusi anggaran di berbagai departemen atau proyek.
3. **Demografi Pelanggan**: Menganalisis segmen pelanggan berdasarkan usia, lokasi, atau preferensi.
4. **Készletgazdálkodás**Melacak kategori produk dan kontribusinya terhadap nilai inventaris keseluruhan.

## Teljesítménybeli szempontok

Saat bekerja dengan Aspose.Cells untuk .NET, pertimbangkan tips berikut:
- **Mengoptimalkan Kumpulan Data Besar**: Gunakan metode pemrosesan batch untuk menangani kumpulan data besar secara efisien.
- **Memóriakezelés**: A tárgyakat megfelelően ártalmatlanítsd az erőforrások felszabadítása érdekében.
- **Memanfaatkan Multithreading**: Untuk operasi intensif, gunakan kemampuan multi-threading yang tersedia di .NET.

## Következtetés

Membuat buku kerja Excel dengan diagram lingkaran menggunakan Aspose.Cells for .NET merupakan cara yang ampuh untuk menyajikan data secara visual dan efektif. Dengan mengikuti panduan ini, Anda telah mempelajari cara menyiapkan lingkungan, mengisi buku kerja Excel, membuat diagram, dan menyesuaikannya dengan kebutuhan Anda.

**Következő lépések**: Bereksperimenlah dengan berbagai jenis bagan dan jelajahi fitur tambahan Aspose.Cells untuk lebih menyempurnakan aplikasi Anda.

## GYIK szekció

1. **Hogyan telepíthetem az Aspose.Cells for .NET-et?**
   - Gunakan .NET CLI atau Manajer Paket seperti yang dijelaskan di bagian pengaturan.

2. **Ingyenesen használhatom az Aspose.Cells-t?**
   - Uji coba gratis tersedia, tetapi lisensi diperlukan untuk fitur tambahan dan penggunaan komersial.

3. **Jenis bagan apa yang dapat saya buat dengan Aspose.Cells?**
   - Selain diagram lingkaran, Anda dapat membuat diagram batang, garis, sebaran, area, dan lainnya menggunakan Aspose.Cells.

4. **Bagaimana cara menangani kumpulan data besar di Excel dengan Aspose.Cells?**
   - Gunakan fitur penanganan data perpustakaan yang efisien untuk mengelola dan memproses kumpulan data besar secara efektif.

5. **Az Aspose.Cells kompatibilis a .NET összes verziójával?**
   - Ya, ini kompatibel dengan berbagai versi .NET Framework dan .NET Core.

## Rekomendasi Kata Kunci
- "Aspose.Cells untuk .NET"
- "Buat Buku Kerja Excel"
- "Diagram Lingkaran Excel"

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}