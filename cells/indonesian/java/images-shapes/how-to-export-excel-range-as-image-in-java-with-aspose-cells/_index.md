---
category: general
date: 2026-10-10
description: Pelajari cara mengekspor rentang Excel sebagai gambar dalam Java menggunakan
  Aspose.Cells. Panduan ini juga mencakup mengekspor sel yang dipilih sebagai gambar
  dan menyimpan lembar kerja Excel sebagai gambar.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- export selected cells as image
- save excel worksheet as picture
language: id
lastmod: 2026-10-10
og_description: Ekspor rentang Excel sebagai gambar di Java dengan solusi langkah
  demi langkah. Termasuk mengekspor sel yang dipilih sebagai gambar dan menyimpan
  lembar kerja Excel sebagai gambar.
og_image_alt: Diagram showing export Excel range as image using Java and Aspose.Cells
og_title: Ekspor rentang Excel sebagai gambar di Java – panduan lengkap Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  headline: How to export Excel range as image in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  name: How to export Excel range as image in Java with Aspose.Cells
  steps:
  - name: Why this method matters
    text: '* **Separation of concerns:** Loading, option configuration, and exporting
      are clearly divided. * **Flexibility:** You can change the image format or DPI
      without touching the core logic. * **Error handling:** Throwing `Exception`
      lets the caller decide whether to log, retry, or abort.'
  - name: 1. Merged cells
    text: Aspose.Cells automatically preserves merged cell appearance, but if you
      need to control the rendering, set `options.setOnePagePerSheet(true)` to force
      the whole sheet onto a single page before exporting.
  - name: 2. Hidden rows or columns
    text: 'By default, hidden rows/columns are not rendered. To include them, enable:'
  - name: 3. Large ranges and memory consumption
    text: 'Exporting very large ranges can consume significant memory. If you encounter
      `OutOfMemoryError`, consider:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- Image export
title: Cara mengekspor rentang Excel sebagai gambar di Java dengan Aspose.Cells
url: /id/java/images-shapes/how-to-export-excel-range-as-image-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengekspor rentang Excel sebagai gambar di Java dengan Aspose.Cells

Jika Anda perlu **mengekspor rentang Excel sebagai gambar**, tutorial ini akan memandu Anda melalui solusi Java lengkap menggunakan pustaka Aspose.Cells. Anda juga akan belajar cara **mengekspor sel yang dipilih sebagai gambar** dan cara **menyimpan lembar kerja Excel sebagai gambar** untuk keperluan pelaporan atau dokumentasi.

Mengekspor bagian dari workbook menjadi gambar menghilangkan kebutuhan akan alat screenshot pihak ketiga dan menjamin hasil yang pixel‑perfect. Pada akhir panduan ini Anda akan memiliki metode yang dapat digunakan kembali yang menulis PNG (atau format lain yang didukung) langsung ke disk, siap untuk dimasukkan ke PDF, email, atau halaman web.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* Java 17 atau yang lebih baru terpasang.
* Maven 3.8+ (atau alat build lain yang dapat menangani dependensi Maven).
* Lisensi Aspose.Cells untuk Java (versi evaluasi gratis tetap dapat digunakan tetapi menambahkan watermark).
* File Excel contoh (`input.xlsx`) yang ditempatkan di direktori yang diketahui.

Bagian‑bagian berikut mengasumsikan Anda sudah nyaman dengan pengembangan Java dasar dan penyiapan proyek Maven.

## Langkah 1: Tambahkan Aspose.Cells ke proyek Anda

Tambahkan dependensi Maven Aspose.Cells ke `pom.xml` Anda. Pustaka ini menyediakan kelas `Workbook`, `Worksheet`, dan `ImageOrPrintOptions` yang digunakan dalam contoh kode.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Pastikan nomor versi selalu terbaru; rilis yang lebih baru menambahkan dukungan format dan peningkatan performa.

## Langkah 2: Buat metode utilitas untuk mengekspor rentang

Membungkus logika ekspor dalam sebuah metode memudahkan penggunaan kembali di berbagai proyek dan menangani kasus tepi seperti sel yang digabung atau baris tersembunyi.

```java
import com.aspose.cells.*;

import java.io.File;

/**
 * Exports a specific cell range from an Excel worksheet to an image file.
 *
 * @param workbookPath   Full path to the source .xlsx file.
 * @param sheetIndex     Zero‑based index of the worksheet (0 = first sheet).
 * @param range          A‑style range string, e.g. "A1:G20".
 * @param outputPath     Full path where the image will be saved.
 * @param imageFormat    Desired image format (PNG, JPEG, BMP, etc.).
 * @throws Exception if the file cannot be read or written.
 */
public static void exportRangeAsImage(
        String workbookPath,
        int sheetIndex,
        String range,
        String outputPath,
        ImageFormat imageFormat) throws Exception {

    // Load the workbook
    Workbook wb = new Workbook(workbookPath);

    // Obtain the requested worksheet
    Worksheet ws = wb.getWorksheets().get(sheetIndex);

    // Configure image export options
    ImageOrPrintOptions options = new ImageOrPrintOptions();
    options.setImageFormat(imageFormat);
    // Optional: increase DPI for higher‑resolution output
    options.setHorizontalResolution(300);
    options.setVerticalResolution(300);

    // Export the defined range as an image file
    ws.getCells().exportRangeAsImage(range, outputPath, options);
}
```

### Mengapa metode ini penting

* **Pemisahan kepedulian:** Memuat, mengonfigurasi opsi, dan mengekspor dibagi secara jelas.
* **Fleksibilitas:** Anda dapat mengubah format gambar atau DPI tanpa menyentuh logika inti.
* **Penanganan error:** Melempar `Exception` memungkinkan pemanggil memutuskan apakah akan mencatat, mencoba kembali, atau menghentikan proses.

## Langkah 3: Panggil metode dengan parameter nyata

Berikut adalah metode `main` minimal yang mendemonstrasikan cara **mengekspor sel yang dipilih sebagai gambar** dan juga cara **menyimpan lembar kerja Excel sebagai gambar** dengan menggunakan rentang seluruh lembar.

```java
public class ExcelImageExporter {
    public static void main(String[] args) {
        try {
            String inputFile   = "C:/Data/input.xlsx";
            String outputFile1 = "C:/Data/range.png";
            String outputFile2 = "C:/Data/full_sheet.png";

            // Export a specific range (A1:G20)
            exportRangeAsImage(
                    inputFile,
                    0,                  // first worksheet
                    "A1:G20",
                    outputFile1,
                    ImageFormat.PNG);   // primary format for lossless quality

            // Export the entire first worksheet – effectively saving the worksheet as picture
            exportRangeAsImage(
                    inputFile,
                    0,
                    "A1:" + getLastCellAddress(inputFile, 0), // compute last used cell
                    outputFile2,
                    ImageFormat.PNG);

            System.out.println("Images generated successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * Helper that returns the address of the last used cell in a worksheet.
     */
    private static String getLastCellAddress(String workbookPath, int sheetIdx) throws Exception {
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.getWorksheets().get(sheetIdx);
        // Find the maximum row and column that contain data
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();
        // Convert column index to A‑style letter (0 -> A)
        String colLetter = CellReference.convertNumToColString(maxCol);
        return colLetter + (maxRow + 1);
    }
}
```

#### Output yang diharapkan

Menjalankan program akan membuat dua file PNG:

* `range.png` – gambar yang hanya berisi sel **A1:G20**.
* `full_sheet.png` – gambar dari seluruh area yang digunakan pada lembar kerja pertama, secara efektif **menyimpan lembar kerja Excel sebagai gambar**.

Anda dapat membuka file tersebut dengan penampil gambar apa pun untuk memverifikasi bahwa tata letak visual cocok dengan tampilan Excel, termasuk batas sel, warna, dan sel yang digabung.

## Langkah 4: Tangani kasus tepi umum

### 1. Sel yang digabung

Aspose.Cells secara otomatis mempertahankan tampilan sel yang digabung, tetapi jika Anda perlu mengontrol rendering, atur `options.setOnePagePerSheet(true)` untuk memaksa seluruh lembar berada pada satu halaman sebelum diekspor.

### 2. Baris atau kolom tersembunyi

Secara default, baris/kolom tersembunyi tidak dirender. Untuk menyertakannya, aktifkan:

```java
options.setSkipEmptyRows(false);
options.setSkipEmptyColumns(false);
```

### 3. Rentang besar dan konsumsi memori

Mengekspor rentang yang sangat besar dapat mengonsumsi memori secara signifikan. Jika Anda menemukan `OutOfMemoryError`, pertimbangkan:

* Mengurangi DPI (`options.setHorizontalResolution(150)`).
* Mengekspor rentang dalam potongan lebih kecil dan menyatukan gambar dengan pustaka grafis.

## Langkah 5: Verifikasi hasil secara programatis (opsional)

Jika proses hilir Anda perlu memastikan bahwa gambar telah dihasilkan dengan benar, Anda dapat memuat PNG menggunakan `javax.imageio.ImageIO` dan memeriksa dimensinya:

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File(outputFile1));
System.out.println("Image width: " + img.getWidth() + " px");
System.out.println("Image height: " + img.getHeight() + " px");
```

Lebar dan tinggi yang tidak nol menunjukkan ekspor berhasil.

## Kesimpulan

Anda kini tahu cara **mengekspor rentang Excel sebagai gambar** di Java, cara **mengekspor sel yang dipilih sebagai gambar**, dan cara **menyimpan lembar kerja Excel sebagai gambar** menggunakan Aspose.Cells. Metode `exportRangeAsImage` yang dapat digunakan kembali menyederhanakan kompleksitas, memberi Anda kontrol atas kualitas gambar, dan bekerja dengan indeks lembar kerja atau rentang sel apa pun.

Langkah selanjutnya yang dapat Anda jelajahi:

* Mengonversi PNG ke PDF dengan Aspose.PDF untuk pelaporan.
* Memproses batch banyak workbook dalam sebuah direktori.
* Mengintegrasikan ekspor gambar ke endpoint REST Spring Boot sehingga klien dapat meminta gambar sesuai permintaan.

Silakan bereksperimen dengan format gambar lain (`ImageFormat.JPEG`, `ImageFormat.BMP`) dan pengaturan DPI untuk memenuhi kebutuhan visual proyek Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}