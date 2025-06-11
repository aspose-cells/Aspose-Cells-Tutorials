---
"date": "2025-04-05"
"description": "Pelajari cara membuat diagram pai dinamis dengan garis acuan menggunakan Aspose.Cells for .NET. Ikuti panduan ini untuk meningkatkan keterampilan visualisasi data Anda."
"title": "Membuat Diagram Lingkaran dengan Garis Pemimpin di Aspose.Cells .NET&#58; Panduan Lengkap"
"url": "/id/net/charts-graphs/create-pie-charts-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Membuat Diagram Lingkaran dengan Garis Pemimpin Menggunakan Aspose.Cells .NET

## Bevezetés
Tingkatkan visualisasi data Anda dengan membuat diagram pai yang lebih informatif dengan Aspose.Cells untuk .NET. Panduan langkah demi langkah ini menunjukkan kepada Anda cara menambahkan garis pemimpin ke segmen diagram pai, sehingga memudahkan Anda mengidentifikasi kategori data yang sesuai secara sekilas. Dengan mengikuti tutorial ini, visualisasi Anda akan menarik secara visual dan sangat fungsional.

**Amit tanulni fogsz:**
- Menyiapkan Aspose.Cells untuk .NET di lingkungan Anda
- Membuat diagram lingkaran garis pemimpin khusus menggunakan C#
- Menyimpan bagan sebagai gambar atau dalam buku kerja Excel

Pastikan Anda telah menyiapkan semuanya untuk diikuti secara efektif.

## Előfeltételek
Sebelum memulai, pastikan Anda memenuhi prasyarat berikut:

- **Könyvtárak és verziók**: Instal Aspose.Cells untuk .NET. Pastikan proyek Anda telah diatur dengan versi terbaru.
- **Környezet beállítása**: Panduan ini mengasumsikan lingkungan .NET yang kompatibel untuk Aspose.Cells.
- **Ismereti előfeltételek**:Pengetahuan dasar tentang pemrograman C# dan operasi Excel akan bermanfaat.

## Az Aspose.Cells beállítása .NET-hez
Untuk memulai, instal Aspose.Cells di proyek Anda melalui:

**.NET parancssori felület**
```bash
dotnet add package Aspose.Cells
```

**Csomagkezelő**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Dapatkan lisensi untuk fungsionalitas penuh dengan memilih dari opsi berikut:
- **Ingyenes próbaverzió**:Mulai uji coba gratis Anda di [Aspose letöltési oldal](https://releases.aspose.com/cells/net/).
- **Ideiglenes engedély**: Ideiglenes jogosítvány beszerzése [itt](https://purchase.aspose.com/temporary-license/).
- **Vásárlás**: Untuk fitur lengkap, beli lisensi [itt](https://purchase.aspose.com/buy).

Inisialisasi Aspose.Cells di proyek Anda dengan membuat instance `Workbook` osztály.

## Megvalósítási útmutató

### Membuat Buku Kerja dan Lembar Kerja
1. **A munkafüzet inicializálása**
   Buat buku kerja baru dalam format XLSX:
   ```csharp
   Workbook workbook = new Workbook(FileFormatType.Xlsx);
   ```

2. **Az első munkalap elérése**
   Gunakan lembar kerja pertama untuk memasukkan data:
   ```csharp
   Worksheet worksheet = workbook.Worksheets[0];
   ```

3. **Menambahkan Data untuk Diagram Lingkaran**
   Isi lembar kerja Anda dengan kategori dan nilai:
   ```csharp
   worksheet.Cells["A1"].PutValue("Retail");
   // Tambahkan nama kategori yang tersisa...
   worksheet.Cells["B1"].PutValue(10.4);
   // Tambahkan nilai yang sesuai...
   ```

### Menambahkan Diagram Lingkaran ke Lembar Kerja
1. **Membuat Diagram Lingkaran**
   Buat diagram lingkaran dan tambahkan ke koleksi diagram lembar kerja Anda:
   ```csharp
   int id = worksheet.Charts.Add(ChartType.Pie, 3, 3, 23, 13);
   ```

2. **Konfigurasikan Data Seri dan Kategori**
   Hubungkan data untuk seri dan kategori:
   ```csharp
   Chart chart = worksheet.Charts[id];
   chart.NSeries.Add("B1:B16", true);
   chart.NSeries.CategoryData = "A1:A16";
   ```

3. **Sesuaikan Label Data**
   Matikan tampilan legenda, atur label data untuk menampilkan nama kategori dan persentase:
   ```csharp
   chart.ShowLegend = false;
   DataLabels dataLabels = chart.NSeries[0].DataLabels;
   dataLabels.ShowCategoryName = true;
   dataLabels.ShowPercentage = true;
   dataLabels.Position = LabelPositionType.OutsideEnd;
   ```

### Menerapkan Garis Pemimpin
1. **Nyalakan Garis Pemimpin**
   Aktifkan garis pemimpin untuk koneksi visual yang lebih jelas:
   ```csharp
   chart.NSeries[0].HasLeaderLines = true;
   ```

2. **Sesuaikan Posisi Label Data**
   Pastikan visibilitas dengan menyesuaikan posisi label:
   ```csharp
   int DELTA = 100;
   foreach (var point in chart.NSeries[0].Points)
   {
       int X = point.DataLabels.X;
       if (X > 2000) 
           point.DataLabels.X += DELTA;
       else 
           point.DataLabels.X -= DELTA;
   }
   ```

### Menyimpan Bagan dan Buku Kerja
1. **Simpan sebagai Gambar**
   Ubah grafik menjadi file gambar:
   ```csharp
   ImageOrPrintOptions options = new ImageOrPrintOptions { ImageType = Drawing.ImageType.Png, HorizontalResolution = 200, VerticalResolution = 200 };
   chart.ToImage("output_out.png", options);
   ```

2. **Munkafüzet mentése**
   Simpan buku kerja untuk melihat bagan dalam Excel:
   ```csharp
   workbook.Save("output_out.xlsx");
   ```

## Gyakorlati alkalmazások
- **Pénzügyi jelentések**:Mewakili alokasi anggaran secara jelas.
- **Analisis Pemasaran**: Visualisasikan data pangsa pasar secara efektif dalam presentasi atau laporan.
- **Analisis Penjualan**Menampilkan distribusi penjualan di berbagai wilayah/produk dengan mudah.

Kemungkinan integrasi mencakup mengekspor visualisasi ini ke aplikasi web atau menanamkannya dalam alat pelaporan otomatis.

## Teljesítménybeli szempontok
Saat menggunakan Aspose.Cells, pertimbangkan hal berikut untuk kinerja optimal:
- Minimalkan kumpulan data besar yang dimuat ke dalam memori sekaligus.
- Gunakan loop yang efisien dan hindari perhitungan yang tidak perlu di dalam loop.
- Bersihkan sumber daya seperti objek buku kerja secara teratur untuk mencegah kebocoran memori.

## Következtetés
Anda telah mempelajari cara membuat diagram lingkaran dengan garis pemimpin menggunakan Aspose.Cells for .NET. Fungsionalitas ini meningkatkan kejelasan visualisasi data Anda, membuatnya lebih mudah diakses dan berdampak. 

**Következő lépések:**
Jelajahi penyesuaian lebih lanjut dalam tampilan bagan atau bereksperimen dengan jenis bagan lain yang tersedia di Aspose.Cells.

## GYIK szekció
1. **Apa itu garis pemimpin pada diagram lingkaran?**
   Garis pemimpin menghubungkan label data ke segmennya masing-masing, meningkatkan keterbacaan.

2. **Ingyenesen használhatom az Aspose.Cells-t?**
   Ya, Anda dapat memulai dengan uji coba gratis, tetapi fitur lengkap memerlukan lisensi.

3. **Apakah mungkin untuk mengekspor grafik sebagai gambar?**
   Tentu saja! Gunakan `ImageOrPrintOptions` untuk menyimpan bagan Anda dalam format gambar seperti PNG atau JPEG.

4. **Bagaimana cara menyesuaikan posisi label data secara manual?**
   Ubah koordinat X dan Y label data dalam loop titik seri.

5. **Bisakah Aspose.Cells terintegrasi dengan sistem lain?**
   Ya, dapat digunakan bersama dengan basis data, layanan web, dan lainnya untuk solusi pelaporan otomatis.

## Erőforrás
- [Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/)
- [Aspose.Cells letöltése](https://releases.aspose.com/cells/net/)
- [Licenc vásárlása](https://purchase.aspose.com/buy)
- [Ingyenes próbaverzió](https://releases.aspose.com/cells/net/)
- [Ideiglenes engedély](https://purchase.aspose.com/temporary-license/)
- [Támogatási fórum](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}