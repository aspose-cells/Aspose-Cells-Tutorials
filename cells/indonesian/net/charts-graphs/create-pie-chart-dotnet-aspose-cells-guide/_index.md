---
"date": "2025-04-05"
"description": "Kód oktatóanyag az Aspose.Cells Nethez"
"title": "Membuat Diagram Lingkaran di .NET dengan Aspose.Cells&#58; Panduan Lengkap"
"url": "/id/net/charts-graphs/create-pie-chart-dotnet-aspose-cells-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Cara Membuat Diagram Lingkaran di .NET Menggunakan Aspose.Cells: Panduan Langkah demi Langkah

## Bevezetés

Membuat representasi visual data merupakan keterampilan penting, terutama saat mencoba menyampaikan informasi yang kompleks secara sederhana dan efektif. Baik Anda sedang mengerjakan laporan bisnis atau menganalisis statistik demografi, diagram lingkaran menawarkan cara yang mudah untuk mengilustrasikan bagian-bagian dari keseluruhan. Panduan ini akan memandu Anda melalui proses pembuatan diagram lingkaran di .NET menggunakan Aspose.Cells—pustaka canggih yang menyederhanakan pekerjaan dengan dokumen Excel secara terprogram.

**Amit tanulni fogsz:**
- Cara menginisialisasi dan menyiapkan buku kerja Excel.
- Mengisi data ke dalam sel lembar kerja untuk visualisasi.
- Membuat dan mengonfigurasi diagram lingkaran menggunakan Aspose.Cells untuk .NET.
- Menyesuaikan warna irisan pada diagram lingkaran untuk meningkatkan daya tarik visual.
- Menyesuaikan kolom secara otomatis dan menyimpan buku kerja Anda.

Mari kita bahas cara memanfaatkan Aspose.Cells untuk membuat diagram lingkaran yang menarik dengan mudah. Sebelum memulai, pastikan Anda memenuhi prasyarat agar dapat mengikuti dengan lancar.

## Előfeltételek

Untuk memulai tutorial ini, pastikan Anda memiliki:

- **Szükséges könyvtárak:** Anda memerlukan pustaka Aspose.Cells for .NET. Pastikan proyek Anda telah diatur untuk menggunakannya.
- **Környezeti beállítási követelmények:** Lingkungan pengembangan yang sesuai seperti Visual Studio yang terinstal di sistem Anda.
- **Előfeltételek a tudáshoz:** Pemahaman dasar tentang pemrograman C# dan keakraban dengan struktur dokumen Excel.

## Az Aspose.Cells beállítása .NET-hez

Sebelum mulai membuat kode, Anda perlu memasang pustaka Aspose.Cells di proyek Anda. Berikut caranya:

### Instalasi melalui CLI
Buka terminal atau command prompt Anda dan jalankan:
```bash
dotnet add package Aspose.Cells
```

### Telepítés csomagkezelőn keresztül
Jika Anda menggunakan Visual Studio, buka Konsol Manajer Paket NuGet dan jalankan:
```powershell
PM> Install-Package Aspose.Cells
```

#### Licencbeszerzés lépései
Anda dapat memulai dengan uji coba gratis untuk mengevaluasi Aspose.Cells. Untuk penggunaan lebih lama, pertimbangkan untuk mendapatkan lisensi sementara atau membelinya langsung dari situs web mereka.

#### Alapvető inicializálás és beállítás

Untuk menginisialisasi pustaka di proyek C# Anda:
```csharp
using Aspose.Cells;

// Buat contoh kelas Buku Kerja
Workbook workbook = new Workbook();
```

Pengaturan dasar ini memungkinkan Anda untuk mulai bekerja dengan berkas Excel secara terprogram.

## Megvalósítási útmutató

### 1. funkció: Munkafüzet és munkalap inicializálása

**Áttekintés:** Fitur ini menyiapkan buku kerja baru dan mengakses lembar kerja pertamanya, mempersiapkan tahap untuk entri data dan pembuatan bagan.

#### Inisialisasi Langkah demi Langkah
```csharp
using Aspose.Cells;

class InitializeWorkbook {
    public void Run() {
        // Membuat objek buku kerja baru
        Workbook workbook = new Workbook();
        
        // A munkafüzet első munkalapjának elérése
        Worksheet worksheet = workbook.Worksheets[0];
    }
}
```
Itt, `Workbook` mewakili file Excel, dan mengakses `Worksheets[0]` memberimu lembar pertama.

### Fitur 2: Mengisi Data untuk Diagram Lingkaran

**Áttekintés:** Mengisi data sangat penting karena data tersebut menjadi dasar bagan Anda. Langkah ini melibatkan memasukkan nama negara dan persentase populasi dunia yang sesuai ke dalam sel tertentu.

#### Pengisian Data Langkah demi Langkah
```csharp
using Aspose.Cells;

class PopulateData {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Masukkan data negara di kolom C
        worksheet.Cells["C3"].PutValue("India");
        worksheet.Cells["C4"].PutValue("China");
        worksheet.Cells["C5"].PutValue("United States");
        worksheet.Cells["C6"].PutValue("Russia");
        worksheet.Cells["C7"].PutValue("United Kingdom");
        worksheet.Cells["C8"].PutValue("Others");

        // Masukkan data persentase di kolom D
        worksheet.Cells["D2"].PutValue("% of world population");
        worksheet.Cells["D3"].PutValue(25);
        worksheet.Cells["D4"].PutValue(30);
        worksheet.Cells["D5"].PutValue(10);
        worksheet.Cells["D6"].PutValue(13);
        worksheet.Cells["D7"].PutValue(9);
        worksheet.Cells["D8"].PutValue(13);
    }
}
```
Langkah ini memastikan data Anda siap untuk visualisasi.

### Fitur 3: Membuat dan Mengonfigurasi Diagram Lingkaran

**Áttekintés:** Fitur ini melibatkan pembuatan diagram lingkaran, pengaturan data seri, dan konfigurasi berbagai properti seperti judul dan posisi legenda.

#### Pembuatan Diagram Lingkaran Langkah demi Langkah
```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class CreatePieChart {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Tambahkan diagram lingkaran ke lembar kerja
        int pieIdx = worksheet.Charts.Add(ChartType.Pie, 1, 6, 15, 14);
        Chart pie = worksheet.Charts[pieIdx];

        // Tetapkan seri data untuk bagan
        pie.NSeries.Add("D3:D8", true);

        // Tentukan data kategori dan konfigurasikan judul
        pie.NSeries.CategoryData = "=Sheet1!$C$3:$C$8";
        pie.Title.LinkedSource = "D2";
        pie.Legend.Position = LegendPositionType.Bottom;
        pie.Title.Font.Name = "Calibri";
        pie.Title.Font.Size = 18;
    }
}
```
Kode ini membuat bagan menarik secara visual yang ditautkan ke data Anda.

### Fitur 4: Sesuaikan Warna Irisan pada Bagan Pai

**Áttekintés:** Personalisasi tampilan setiap irisan meningkatkan keterbacaan dan estetika. Langkah ini melibatkan pemberian warna unik pada irisan yang berbeda.

#### Kustomisasi Warna Langkah demi Langkah
```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;

class CustomizeSliceColors {
    public void Run() {
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        int pieIdx = worksheet.Charts.Add(ChartType.Pie, 1, 6, 15, 14);
        Chart pie = worksheet.Charts[pieIdx];
        
        Series srs = pie.NSeries[0];

        // Tetapkan warna khusus untuk setiap irisan
        srs.Points[0].Area.ForegroundColor = Color.FromArgb(0, 246, 22, 219);
        srs.Points[1].Area.ForegroundColor = Color.FromArgb(0, 51, 34, 84);
        srs.Points[2].Area.ForegroundColor = Color.FromArgb(0, 46, 74, 44);
        srs.Points[3].Area.ForegroundColor = Color.FromArgb(0, 19, 99, 44);
        srs.Points[4].Area.ForegroundColor = Color.FromArgb(0, 208, 223, 7);
        srs.Points[5].Area.ForegroundColor = Color.FromArgb(0, 222, 69, 8);
    }
}
```
Langkah ini menambahkan sentuhan yang semarak pada bagan Anda.

### Fitur 5: Sesuaikan Kolom Secara Otomatis dan Simpan Buku Kerja

**Áttekintés:** Langkah terakhir melibatkan penyesuaian lebar kolom untuk visibilitas data yang lebih baik dan menyimpan buku kerja dalam format Excel.

#### Penyesuaian dan Penyimpanan Kolom Langkah demi Langkah
```csharp
using Aspose.Cells;

class SaveWorkbook {
    public void Run() {
        string outputDir = "YOUR_OUTPUT_DIRECTORY";
        
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
        
        // Sesuaikan kolom secara otomatis agar sesuai dengan konten
        worksheet.AutoFitColumns();

        // Simpan buku kerja sebagai file Excel
        workbook.Save(outputDir + "outputCustomSliceSectorColorsPieChart.xlsx", SaveFormat.Xlsx);
    }
}
```
Ini memastikan dokumen akhir Anda sempurna dan siap untuk dipresentasikan.

## Gyakorlati alkalmazások

- **Üzleti jelentések:** Gunakan diagram lingkaran untuk menggambarkan distribusi penjualan menurut wilayah.
- **Studi Demografi:** Visualisasikan data populasi di berbagai negara atau wilayah.
- **Alat Pendidikan:** Buat alat bantu visual yang menarik bagi siswa dalam kursus statistik.
- **Analisis Perawatan Kesehatan:** Menampilkan distribusi data pasien dalam fasilitas perawatan kesehatan.

## Teljesítménybeli szempontok

Az Aspose.Cells használatakor az optimális teljesítmény biztosítása érdekében vegye figyelembe a következőket:

- **Hatékony adatkezelés:** Kelola kumpulan data besar dengan memprosesnya dalam potongan-potongan jika perlu.
- **Memóriakezelés:** Buang benda-benda dengan benar untuk mengosongkan sumber daya dan menghindari kebocoran memori.
- **Konfigurasi Bagan yang Dioptimalkan:** Minimalkan perhitungan rumit atau rendering selama pembuatan bagan untuk kinerja yang lebih cepat.

## Következtetés

Anda kini telah mempelajari cara membuat diagram pai di .NET menggunakan Aspose.Cells. Pustaka canggih ini menyederhanakan manipulasi dokumen Excel, sehingga Anda dapat fokus pada analisis data, bukan pada kerumitan penanganan berkas. Bereksperimenlah dengan berbagai jenis diagram dan opsi penyesuaian yang tersedia di Aspose.Cells untuk lebih menyempurnakan aplikasi Anda.

**Következő lépések:**
- Jelajahi jenis bagan lainnya seperti bagan batang atau garis.
- Integrasikan fungsionalitas Aspose.Cells ke dalam proyek .NET yang lebih besar untuk pelaporan otomatis.

Siap untuk membawa keterampilan visualisasi data Anda ke tingkat berikutnya? Pelajari lebih dalam dengan menjelajahi lebih banyak fitur Aspose.Cells dan mulailah menerapkannya dalam proyek Anda hari ini!

## GYIK szekció

1. **Untuk apa Aspose.Cells digunakan?**
   - Ini adalah pustaka untuk mengelola berkas Excel secara terprogram, yang memungkinkan Anda membuat, memodifikasi, dan menganalisis lembar kerja.

2. **Használhatom az Aspose.Cells-t licenc nélkül?**
   - Ya, tetapi ada batasannya. Uji coba gratis atau lisensi sementara memungkinkan akses penuh ke berbagai fitur.

3. **Bagaimana cara menyesuaikan tampilan diagram lingkaran saya lebih lanjut?**
   - Gunakan properti tambahan seperti `pie.NSeries[0].Area.Formatting` untuk kontrol lebih besar atas estetika.

4. **Apa saja masalah umum saat membuat bagan di Aspose.Cells?**
   - Pastikan rentang data ditentukan dengan benar dan Anda telah mengonfigurasi semua properti bagan yang diperlukan sebelum merender.

5. **Bagaimana saya dapat mengintegrasikan Aspose.Cells dengan pustaka .NET lainnya?**
   - Gunakan Aspose.Cells sebagai bagian dari solusi .NET yang lebih besar, manfaatkan kemampuannya bersama pustaka lain untuk aplikasi yang komprehensif.

## Erőforrás

- **Dokumentáció:** [Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/)
- **Letöltés:** [Aspose.Cells kiadások](https://releases.aspose.com/cells/net/)
- **Vásárlás:** [Vásároljon Aspose.Cells-t](https://purchase.aspose.com/buy)
- **Ingyenes próbaverzió:** [Aspose.Cells ingyenes próbaverzió](https://releases.aspose.com/cells/net/)
- **Ideiglenes engedély:** [Szerezzen be egy ideiglenes jogosítványt](https://purchase.aspose.com/temporary-license/)
- **Támogatás:** [Aspose Fórum](https://forum.aspose.com/c/cells/9)

Dengan mengikuti panduan ini, Anda kini siap membuat diagram lingkaran yang menarik secara visual dalam aplikasi .NET menggunakan Aspose.Cells. Selamat membuat kode!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}