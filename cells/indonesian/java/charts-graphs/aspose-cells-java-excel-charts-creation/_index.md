---
"date": "2025-04-07"
"description": "Pelajari cara membuat dan menyesuaikan bagan di Excel menggunakan Aspose.Cells untuk Java. Otomatiskan pembuatan bagan, tingkatkan visualisasi data, dan hemat waktu dengan panduan terperinci ini."
"title": "Membuat dan Menata Bagan Excel dengan Aspose.Cells Java; Panduan Lengkap"
"url": "/id/java/charts-graphs/aspose-cells-java-excel-charts-creation/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Membuat dan Menata Bagan Excel dengan Aspose.Cells Java

## Bevezetés

Dalam dunia yang digerakkan oleh data saat ini, visualisasi informasi yang efektif sangat penting untuk analisis dan pengambilan keputusan. Sering kali, ada kebutuhan untuk membuat bagan dinamis dalam buku kerja Excel secara terprogram—terutama saat menangani kumpulan data besar atau sistem pelaporan otomatis. Tutorial ini menunjukkan cara menggunakan Aspose.Cells untuk Java untuk membuat dan menyesuaikan bagan di Excel dengan lancar. Dengan mengintegrasikan Aspose.Cells ke dalam aplikasi Java Anda, Anda dapat mengotomatiskan pembuatan bagan, meningkatkan penyajian data, dan menghemat waktu.

**Amit tanulni fogsz:**
- Menginisialisasi buku kerja dan mengisinya dengan data menggunakan Aspose.Cells.
- Membuat dan mengonfigurasi diagram garis dengan penanda data.
- Menyesuaikan tampilan dan warna seri untuk visualisasi yang lebih baik.
- Menyimpan buku kerja dengan bagan yang baru dibuat dalam format Excel.

Mari kita mulai dengan membahas prasyarat yang diperlukan untuk memulai.

## Előfeltételek

Sebelum membuat dan menata bagan menggunakan Aspose.Cells untuk Java, pastikan Anda memiliki pengaturan berikut:

### Kötelező könyvtárak
Sertakan Aspose.Cells sebagai dependensi dalam proyek Anda. Berikut adalah petunjuk untuk pengguna Maven dan Gradle:

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
- Java Development Kit (JDK) terinstal di sistem Anda.
- Lingkungan Pengembangan Terpadu (IDE) seperti IntelliJ IDEA atau Eclipse untuk pengkodean dan pengujian.

### Ismereti előfeltételek
Diperlukan pemahaman dasar tentang pemrograman Java, beserta pengetahuan tentang buku kerja Excel dan konsep pembuatan grafik. 

### Licencszerzés
Aspose.Cells adalah produk komersial yang memerlukan lisensi untuk fungsionalitas penuh. Anda dapat memperoleh uji coba gratis untuk mengevaluasi fitur-fiturnya, meminta lisensi sementara untuk pengujian lebih lanjut, atau membeli produk untuk penggunaan jangka panjang.

- **Ingyenes próbaverzió:** [Ingyenes próbaverzió letöltése](https://releases.aspose.com/cells/java/)
- **Ideiglenes engedély:** [Ideiglenes engedély igénylése](https://purchase.aspose.com/temporary-license/)
- **Vásárlás:** [Vásároljon Aspose.Cells-t](https://purchase.aspose.com/buy)

## Menyiapkan Aspose.Cells untuk Java

Setelah Anda memasang dependensi yang diperlukan, siapkan lingkungan pengembangan Anda untuk menggunakan Aspose.Cells. Mulailah dengan mengimpor pustaka dan menginisialisasi objek Workbook di aplikasi Java Anda:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Új munkafüzetpéldány inicializálása
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Megvalósítási útmutató

Di bagian ini, kita akan menguraikan implementasi menjadi beberapa fitur berbeda: Inisialisasi Buku Kerja dan Pengisian Data, Pembuatan dan Konfigurasi Bagan, Kustomisasi Seri, dan Penyimpanan Buku Kerja.

### Fitur 1: Inisialisasi Buku Kerja dan Pengisian Data

**Áttekintés:** Fitur ini berfokus pada pembuatan buku kerja baru, mengakses lembar kerja pertamanya, dan mengisinya dengan data untuk pembuatan bagan.

#### 1. lépés: A munkafüzet inicializálása
Mulailah dengan membuat instance `Workbook` objektum:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Munkafüzet példányosítása
        Workbook workbook = new Workbook();
        
        // Első munkalap elérése
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Langkah 2: Tetapkan Judul Kolom dan Isi Data
Tentukan tajuk kolom dan isi baris dengan data contoh:

```java
        // Oszlopcím beállítása 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Buat data acak untuk seri 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Buat data acak untuk seri 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Fitur 2: Pembuatan dan Konfigurasi Bagan

**Áttekintés:** Fitur ini menunjukkan cara menambahkan bagan ke lembar kerja buku kerja, mengatur gayanya, dan mengonfigurasi properti dasar.

#### Langkah 3: Tambahkan Bagan ke Lembar Kerja
Tambahkan diagram garis dengan penanda data:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Munkafüzet példányosítása
        Workbook workbook = new Workbook();
        
        // Első munkalap elérése
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Tambahkan bagan ke lembar kerja
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Akses dan konfigurasikan bagan
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Tetapkan gaya yang telah ditentukan sebelumnya
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Fitur 3: Konfigurasi dan Kustomisasi Seri

**Áttekintés:** Tingkatkan daya tarik visual bagan Anda dengan menyesuaikan pengaturan seri, seperti berbagai warna dan gaya penanda.

#### Langkah 4: Sesuaikan Pengaturan Seri
Konfigurasikan data seri, terapkan pemformatan khusus, dan sesuaikan penanda:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Munkafüzet példányosítása
        Workbook workbook = new Workbook();
        
        // Első munkalap elérése
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Tambahkan seri ke bagan
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Aktifkan warna bervariasi untuk titik seri
        chart.getNSeries().setColorVaried(true);

        // Sesuaikan gaya dan warna penanda seri pertama
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Tetapkan nilai X dan Y untuk seri pertama
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Sesuaikan gaya dan warna penanda seri kedua
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Tetapkan nilai X dan Y untuk seri kedua
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Fitur 4: Menyimpan Buku Kerja

**Áttekintés:** Terakhir, simpan buku kerja untuk mempertahankan perubahan Anda dan pastikan bagan disertakan dalam berkas Excel.

#### 5. lépés: A munkafüzet mentése
Simpan buku kerja Anda dengan grafik yang baru dibuat:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Munkafüzet példányosítása
        Workbook workbook = new Workbook();
        
        // Akses lembar kerja pertama dan tambahkan data, konfigurasi bagan sesuai langkah sebelumnya...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementasi penambahan data dan konfigurasi grafik ada di sini)

        // Simpan buku kerja ke file Excel
        workbook.save("StyledChart.xlsx");
    }
}
```

**Rekomendasi Kata Kunci:**
- "Aspose.Cells untuk Java"
- "Pembuatan grafik Excel dengan Java"
- "Pemrograman Java untuk otomatisasi Excel"

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}