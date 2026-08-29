---
category: general
date: 2026-07-03
description: Ekspor gambar tabel pivot Excel menggunakan Java. Pelajari cara mengatur
  format gambar PNG dengan Aspose.Cells langkah demi langkah.
draft: false
keywords:
- excel pivot table image
- set image format png
- Aspose.Cells export
- Java Excel automation
- pivot table to image
language: id
og_description: Ekspor gambar tabel pivot Excel di Java dijelaskan. Ikuti tutorial
  ini untuk mengatur format gambar PNG dengan cepat dan andal.
og_title: gambar tabel pivot Excel – panduan Java untuk ekspor PNG
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Export an excel pivot table image using Java. Learn how to set image
    format png with Aspose.Cells step‑by‑step.
  headline: 'excel pivot table image: Export to PNG with Java'
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel
- ImageExport
title: 'gambar tabel pivot excel: Ekspor ke PNG dengan Java'
url: /id/java/excel-pivot-tables/excel-pivot-table-image-export-to-png-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel pivot table image – Ekspor Pivot Table sebagai PNG di Java

Pernah perlu mengubah **excel pivot table image** menjadi PNG siap‑bagikan tetapi tidak tahu harus mulai dari mana? Anda tidak sendirian. Dalam banyak alur pelaporan pivot table adalah bintang utama, namun tim lain hanya menginginkan gambar statis. Kabar baik? Dengan beberapa baris Java dan Aspose.Cells Anda dapat **set image format png** dan mendapatkan apa yang Anda butuhkan.

Dalam panduan ini kami akan membahas proses lengkap: memuat workbook, mengambil pivot table pertama, mengonfigurasi opsi ekspor, dan akhirnya menulis file PNG yang tajam ke disk. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat dipakai ulang di proyek Java mana pun.

## Apa yang Akan Anda Pelajari

- Cara memuat workbook Excel dari sistem file.
- Cara menemukan pivot table tertentu pada sebuah worksheet.
- Langkah tepat untuk **set image format png** pada gambar yang diekspor.
- Kesulitan umum (banyak pivot table, dataset besar) dan cara menghindarinya.
- Kelas Java siap‑jalankan yang dapat Anda salin‑tempel.

### Prasyarat

- Java 8 atau lebih baru terpasang.
- Perpustakaan Aspose.Cells for Java (versi terbaru per 2026‑07‑03).
- File Excel (`input.xlsx`) yang berisi setidaknya satu pivot table.
- Familiaritas dasar dengan Maven atau Gradle untuk manajemen dependensi.

---

## Langkah 1: Tambahkan Aspose.Cells ke Proyek Anda

Pertama‑tama—pastikan JAR Aspose.Cells ada di classpath Anda. Jika Anda menggunakan Maven, letakkan ini di `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest at time of writing -->
</dependency>
```

Untuk Gradle, caranya serupa sederhana:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Tip pro:** Aspose menyediakan kunci evaluasi gratis selama 30 hari. Daftar di situs mereka, lalu tambahkan `License.setLicense("Aspose.Cells.lic");` di awal program Anda untuk membuka semua fitur.

## Langkah 2: Muat Workbook dan Akses Pivot Table

Sekarang kita akan membuka file Excel dan mengambil pivot table pertama. Kode di bawah melakukan hal itu, dan sengaja dibuat defensif—jika workbook tidak memiliki worksheet atau sheet tidak memiliki pivot table, kami akan melemparkan pengecualian yang jelas.

```java
import com.aspose.cells.*;

import java.io.File;

public class PivotTableToPng {

    public static void main(String[] args) {
        // Adjust these paths to match your environment
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        try {
            // Load the workbook from disk
            Workbook wb = new Workbook(inputPath);

            // Ensure there is at least one worksheet
            if (wb.getWorksheets().getCount() == 0) {
                throw new IllegalStateException("The workbook contains no worksheets.");
            }

            // Grab the first worksheet (index 0)
            Worksheet ws = wb.getWorksheets().get(0);

            // Verify that the worksheet actually has a pivot table
            if (ws.getPivotTables().getCount() == 0) {
                throw new IllegalStateException("No pivot tables found on the first worksheet.");
            }

            // Retrieve the first pivot table
            PivotTable pt = ws.getPivotTables().get(0);

            // -------------------------------------------------
            // Step 3: Configure image export options (PNG)
            // -------------------------------------------------
            ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
            // This is where we **set image format png**
            imgOpt.setImageFormat(ImageFormat.PNG);
            // Optional: increase the DPI for sharper output (default is 96)
            imgOpt.setResolution(300);

            // -------------------------------------------------
            // Step 4: Export the pivot table as an image file
            // -------------------------------------------------
            pt.toImage(outputPath, imgOpt);

            System.out.println("Successfully exported the excel pivot table image to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### Mengapa Langkah‑Langkah Ini Penting

- **Memuat workbook** memberi kita akses ke struktur data di dalamnya; Aspose.Cells menyembunyikan parsing OpenXML tingkat rendah.
- **Mengakses worksheet** diperlukan karena pivot table terikat pada sheet tertentu. Jika Anda memiliki banyak sheet, Anda dapat melakukan loop melalui `wb.getWorksheets()` dan memilih yang berisi pivot yang diinginkan.
- **Mengambil pivot table** adalah inti dari operasi. `ws.getPivotTables().get(0)` mengambil yang pertama, tetapi Anda juga dapat mencari berdasarkan nama dengan `ws.getPivotTables().get("MyPivot")`.
- **Setting image format png** (kata kunci sekunder) memberi tahu Aspose.Cells untuk merender output sebagai PNG lossless. Format ini mempertahankan garis tajam dan teks, ideal untuk laporan.
- **Ekspor dengan `toImage`** menulis file dalam satu panggilan, menangani pagination dan scaling secara otomatis.

## Langkah 3: Verifikasi Output

Setelah Anda menjalankan program, buka `YOUR_DIRECTORY` dan Anda akan melihat `pivot.png`. Buka dengan penampil gambar apa pun—perhatikan garis kisi yang tajam dan tata letak persis seperti di Excel. Jika gambar terlihat buram, naikkan DPI di `imgOpt.setResolution()`; 300‑600 biasanya cukup untuk aset kualitas cetak.

![excel pivot table image exported as PNG](excel-pivot-table-image.png "excel pivot table image exported as PNG")

*Teks alt gambar:* **excel pivot table image exported as PNG**

## Menangani Banyak Pivot Table

Bagaimana jika sheet Anda berisi lebih dari satu pivot table? Potongan kode di atas mengambil yang pertama, tetapi Anda dapat melakukan iterasi:

```java
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    String outFile = "YOUR_DIRECTORY/pivot_" + i + ".png";
    pt.toImage(outFile, imgOpt);
}
```

Loop ini akan menghasilkan `pivot_0.png`, `pivot_1.png`, dll., masing‑masing mewakili pivot table yang berbeda. Ingat untuk **set image format png** sekali sebelum loop; instance `ImageOrPrintOptions` yang sama dapat dipakai ulang.

## Kasus Khusus & Tips

| Situasi | Hal yang Perlu Diperhatikan | Solusi yang Disarankan |
|-----------|-------------------|---------------|
| **Pivot besar (banyak baris/kolom)** | PNG dapat menjadi sangat besar, menimbulkan tekanan memori. | Gunakan `imgOpt.setOnePagePerSheet(false)` untuk membagi menjadi beberapa halaman, atau turunkan DPI. |
| **Baris/kolom tersembunyi** | Aspose menghormati visibilitas; data tersembunyi tidak akan muncul. | Tampilkan secara programatis dengan `ws.showRows(start, count, true)`. |
| **Gaya khusus (font, warna)** | Beberapa font korporat mungkin tidak ter‑render jika tidak terpasang di server. | Embed font di JVM atau fallback ke font sistem via `imgOpt.setFontEmbeddingMode(FontEmbeddingMode.EMBED_ALL)`. |
| **Format output berbeda diperlukan kemudian** | Anda mungkin menginginkan JPEG atau BMP. | Ganti `imgOpt.setImageFormat(ImageFormat.JPEG)`—kode yang sama tetap berlaku, hanya nilai enum yang berubah. |

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

Berikut seluruh kelas, siap untuk dikompilasi. Tempelkan ke `PivotTableToPng.java`, sesuaikan jalur, dan jalankan `javac PivotTableToPng.java && java PivotTableToPng`.

```java
import com.aspose.cells.*;

public class PivotTableToPng {

    public static void main(String[] args) {
        // ----- Configuration -----
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        try {
            // Load workbook
            Workbook wb = new Workbook(inputPath);

            // Guard clauses
            if (wb.getWorksheets().getCount() == 0) {
                throw new IllegalStateException("Workbook has no worksheets.");
            }

            Worksheet ws = wb.getWorksheets().get(0);
            if (ws.getPivotTables().getCount() == 0) {
                throw new IllegalStateException("No pivot tables on the first worksheet.");
            }

            // Retrieve the first pivot table
            PivotTable pt = ws.getPivotTables().get(0);

            // ----- Set image format png -----
            ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
            imgOpt.setImageFormat(ImageFormat.PNG);   // <-- key line
            imgOpt.setResolution(300);                // optional, for sharper output

            // Export to PNG
            pt.toImage(outputPath, imgOpt);

            System.out.println("excel pivot table image exported successfully: " + outputPath);
        } catch (Exception ex) {
            System.err.println("Error during export:");
            ex.printStackTrace();
        }
    }
}
```

Jalankan, dan Anda akan memiliki **excel pivot table image** yang tersimpan sebagai file PNG—tepat seperti yang dijanjikan tutorial.

---

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **mengekspor excel pivot table image** menggunakan Java, dan menunjukkan cara **set image format png** dengan Aspose.Cells. Dari memuat workbook hingga menangani kasus khusus, solusi ini ringkas, dapat diandalkan, dan siap produksi.

Apa selanjutnya? Coba ekspor beberapa pivot secara batch, bereksperimen dengan pengaturan DPI untuk aset siap cetak, atau ubah format ke JPEG untuk gambar yang dioptimalkan web. Anda juga dapat menjelajahi penyisipan PNG ke dalam laporan PDF—Aspose.PDF membuatnya sangat mudah.

Punya alur kerja yang berbeda atau menemui kendala? Tinggalkan komentar, dan kami akan membantu memecahkan masalah bersama. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}