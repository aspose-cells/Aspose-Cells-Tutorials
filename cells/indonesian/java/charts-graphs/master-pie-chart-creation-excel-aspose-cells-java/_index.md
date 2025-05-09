---
"date": "2025-04-07"
"description": "Pelajari cara membuat dan menyesuaikan diagram pai di Excel dengan Aspose.Cells untuk Java. Ikuti panduan langkah demi langkah ini untuk meningkatkan keterampilan visualisasi data Anda."
"title": "Membuat Diagram Lingkaran di Excel Menggunakan Aspose.Cells untuk Java; Panduan Lengkap"
"url": "/id/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Membuat Diagram Lingkaran di Excel Menggunakan Aspose.Cells untuk Java
## Bevezetés
Membuat diagram lingkaran yang menarik dan informatif di Excel dapat mengubah data mentah menjadi wawasan yang kuat, sehingga Anda dapat membuat keputusan bisnis yang tepat dengan cepat. Kesulitan dengan fitur bawaan Microsoft Excel atau mencari solusi yang dapat diskalakan yang terintegrasi dengan lancar dengan aplikasi Java Anda? Aspose.Cells untuk Java hadir untuk membantu.

Tutorial ini memandu Anda membuat dan menyesuaikan diagram pai dalam file Excel menggunakan Aspose.Cells untuk Java. Temukan cara menambahkan data secara efisien, mengonfigurasi elemen diagram, dan menyelesaikan buku kerja Anda—semuanya dengan mudah dan tepat.

**Amit tanulni fogsz:**
- Menyiapkan dan menggunakan Aspose.Cells untuk Java
- Membuat buku kerja baru dan mengisinya dengan data sampel
- Menambahkan dan menyesuaikan diagram lingkaran dalam lembar kerja Excel
- Praktik terbaik untuk konfigurasi dan pengoptimalan bagan

Mari kita mulai dengan membahas prasyaratnya.
## Előfeltételek
Mielőtt elkezdené, győződjön meg arról, hogy a következőkkel rendelkezik:
### Szükséges könyvtárak, verziók és függőségek
Pastikan Aspose.Cells untuk Java versi 25.3 atau yang lebih baru disertakan dalam proyek Anda menggunakan Maven atau Gradle.
**Pakar:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```
**Gradasi:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```
### Környezeti beállítási követelmények
- Java Development Kit (JDK) terinstal pada sistem Anda.
- Lingkungan Pengembangan Terpadu (IDE) seperti IntelliJ IDEA, Eclipse, atau NetBeans.
### Ismereti előfeltételek
Pemahaman dasar tentang pemrograman Java dan keakraban dengan struktur file Excel akan bermanfaat.
## Menyiapkan Aspose.Cells untuk Java
Aspose.Cells adalah pustaka canggih yang memungkinkan pengembang membuat, memodifikasi, dan menyajikan lembar kerja Excel dalam aplikasi Java. Berikut cara mengaturnya:
1. **Telepítés**: Tambahkan dependensi Maven atau Gradle seperti yang ditunjukkan di atas.
2. **Licencszerzés**:
   - Dapatkan lisensi uji coba gratis untuk pengujian awal dari [Aspose ingyenes próbaverzió](https://releases.aspose.com/cells/java/).
   - Ajukan lisensi sementara untuk menguji fitur lengkap tanpa batasan melalui [Ideiglenes engedély](https://purchase.aspose.com/temporary-license/).
3. **Alapvető inicializálás**: Mulailah dengan membuat sebuah instance dari `Workbook` kelas, yang mewakili berkas Excel Anda.
```java
import com.aspose.cells.Workbook;
// Membuat dan menginisialisasi buku kerja baru
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook();
```
## Megvalósítási útmutató
Sekarang, mari kita terapkan setiap fitur langkah demi langkah untuk membuat buku kerja Excel dengan diagram lingkaran.
### 1. Membuat dan Menginisialisasi Buku Kerja
**Áttekintés**:Kita mulai dengan menginisialisasi `Workbook` objek dan mengakses lembar kerja pertamanya di mana kita akan menambahkan data dan bagan.
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorksheetCollection;

String dataDir = "YOUR_DATA_DIRECTORY";
// Új munkafüzet-példány létrehozása
Workbook workbook = new Workbook();
// A munkafüzet első munkalapjának elérése
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
```
### 2. Menambahkan Data Sampel ke Sel
**Áttekintés**: Isi lembar kerja Anda dengan data contoh yang akan ditampilkan dalam diagram lingkaran.
```java
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

Cells cells = sheet.getCells();
// Tambahkan nama negara di kolom A
Cell cell = cells.get("A1");
cell.setValue("Italy");
cell = cells.get("A2");
cell.setValue("Germany");
// Lanjutkan untuk negara lain...
// Tambahkan data penjualan yang sesuai di kolom B
cell = cells.get("B1");
cell.setValue(10000);
cell = cells.get("B2");
cell.setValue(20000);
// Lanjutkan untuk sisa data...
```
### 3. Menambahkan Diagram Lingkaran ke Lembar Kerja
**Áttekintés**Masukkan diagram lingkaran ke dalam lembar kerja menggunakan rentang data yang telah ditentukan sebelumnya.
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;

ChartCollection charts = sheet.getCharts();
// Tambahkan diagram lingkaran di lokasi dan ukuran yang ditentukan
int chartIndex = charts.add(ChartType.PIE, 15, 4, 40, 15);
Chart chart = charts.get(chartIndex);
```
### 4. Mengonfigurasi Seri Bagan
**Áttekintés**: Tentukan rentang data untuk data penjualan dan kategori (nama negara) untuk memastikan diagram lingkaran secara akurat mewakili kumpulan data Anda.
```java
import com.aspose.cells.SeriesCollection;

SeriesCollection serieses = chart.getNSeries();
// Tetapkan data penjualan sebagai sumber data bagan
serieses.add("B1:B8", true);
// Tentukan data kategori (nama negara)
serieses.setCategoryData("A1:A8");
// Aktifkan warna bervariasi untuk setiap irisan pai
serieses.setColorVaried(true);

// Menampilkan tabel data pada grafik untuk kejelasan
chart.setShowDataTable(true);
```
### 5. Mengatur Judul dan Gaya Bagan
**Áttekintés**: Sesuaikan judul bagan Anda untuk meningkatkan keterbacaan dan penyajian.
```java
import com.aspose.cells.Color;

// Tetapkan judul bagan dengan opsi gaya
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```
### 6. Mengonfigurasi Label Data untuk Seri Bagan
**Áttekintés**: Tambahkan label data ke setiap irisan kue, berikan rincian nilai yang jelas.
```java
import com.aspose.cells.DataLabels;
import com.aspose.cells.LabelPositionType;

for (int i = 0; i < serieses.getCount(); i++) {
    DataLabels datalabels = serieses.get(i).getDataLabels();
    // Posisikan label di dalam dasar setiap irisan pai
    datalabels.setPosition(LabelPositionType.INSIDE_BASE);
    // Konfigurasikan opsi tampilan label
    datalabels.setShowCategoryName(true);
    datalabels.setShowValue(true);
    datalabels.setShowPercentage(false);
    datalabels.setShowLegendKey(true);
}
```
### 7. Menyimpan Buku Kerja
**Áttekintés**Selesaikan berkas Excel Anda dengan semua data dan grafik yang disimpan ke disk.
```java
import com.aspose.cells.SaveFormat;

String outDir = "YOUR_OUTPUT_DIRECTORY";
// Simpan buku kerja ke file Excel
workbook.save(outDir + "/HTCPChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```
## Gyakorlati alkalmazások
- **Üzleti elemzés**: Gunakan diagram lingkaran dalam laporan penjualan untuk memvisualisasikan pangsa pasar atau distribusi pendapatan di seluruh wilayah.
- **Alat Pendidikan**: Membuat modul pembelajaran interaktif yang menampilkan distribusi data statistik.
- **Projektmenedzsment**: Mewakili alokasi sumber daya dan pemanfaatan anggaran secara visual kepada para pemangku kepentingan.
## Teljesítménybeli szempontok
A teljesítmény optimalizálása érdekében:
- Minimalkan penggunaan memori dengan mengelola ukuran buku kerja secara efisien.
- Manfaatkan fitur Aspose.Cells seperti streaming file besar jika menangani kumpulan data yang luas.
- Ikuti praktik terbaik Java untuk manajemen memori, pastikan sumber daya dilepaskan dengan tepat setelah digunakan.
## Következtetés
Dengan mengikuti panduan ini, Anda telah mempelajari cara membuat, mengonfigurasi, dan menyesuaikan diagram pai di Excel menggunakan Aspose.Cells untuk Java. Pustaka canggih ini memungkinkan pengembang untuk mengintegrasikan fungsionalitas spreadsheet tingkat lanjut ke dalam aplikasi Java mereka dengan lancar.
Untuk penjelajahan lebih lanjut, pertimbangkan untuk mempelajari jenis bagan lain atau memperluas kemampuan manipulasi data Anda dengan fitur tambahan yang ditawarkan oleh Aspose.Cells.
## GYIK szekció
1. **Ingyenesen használhatom az Aspose.Cells-t?**
   - Ya, uji coba gratis tersedia. Untuk akses fitur lengkap tanpa batasan, Anda dapat mengajukan lisensi sementara.
2. **Apakah mungkin untuk membuat jenis bagan lain menggunakan Aspose.Cells?**
   - Tentu saja! Anda dapat membuat diagram batang, diagram garis, dan lainnya dengan menyesuaikan `ChartType`.
3. **Bagaimana cara menangani kumpulan data besar di Excel dengan Java?**
   - Gunakan teknik pemuatan data yang efisien dan pertimbangkan streaming untuk file yang sangat besar.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}