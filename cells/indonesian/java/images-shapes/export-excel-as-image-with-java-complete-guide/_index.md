---
category: general
date: 2026-11-22
description: Ekspor Excel sebagai gambar dengan Java menggunakan Aspose.Cells. Pelajari
  cara menambahkan gambar ke lembar kerja dan menyimpan Excel sebagai file PNG dalam
  beberapa langkah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as image
- add picture to worksheet
- export excel sheet to png
- save excel as png file
- save workbook as image
language: id
lastmod: 2026-11-22
og_description: Ekspor Excel sebagai gambar dengan Java menggunakan Aspose.Cells.
  Ikuti panduan ini untuk menambahkan gambar ke lembar kerja dan menyimpan Excel sebagai
  file PNG dengan cepat.
og_image_alt: Code snippet showing Java export of an Excel worksheet to a PNG image
og_title: Ekspor Excel menjadi gambar dengan Java – tutorial langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Export Excel as image with Java using Aspose.Cells. Learn how to add
    picture to worksheet and save Excel as PNG file in a few steps.
  headline: Export Excel as image with Java – complete guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Image export
title: Ekspor Excel sebagai gambar dengan Java – panduan lengkap
url: /id/java/images-shapes/export-excel-as-image-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor Excel sebagai gambar dengan Java – panduan lengkap

Jika Anda perlu **export Excel as image** dalam aplikasi Java, tutorial ini menunjukkan solusi siap‑jalan. Anda akan melihat cara menambahkan gambar ke worksheet, mengonfigurasi opsi ekspor, dan akhirnya **save Excel as PNG file** dengan hanya beberapa baris kode.

Panduan ini mencakup semua hal mulai dari pengaturan Maven hingga penanganan kasus tepi, sehingga Anda dapat mengintegrasikan teknik ini ke dalam proyek apa pun yang memerlukan snapshot visual dari spreadsheet.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* Java 17 atau lebih baru terinstal.
* Maven 3.6+ (atau Gradle) untuk manajemen dependensi.
* Lisensi Aspose.Cells for Java (evaluasi gratis dapat digunakan untuk pengujian).
* Sebuah workbook Excel contoh (`sample.xlsx`) yang berisi data yang ingin Anda ekspor.

## Langkah 1: Tambahkan dependensi Aspose.Cells

Aspose.Cells menyediakan kelas `ImageOrPrintOptions` yang digunakan untuk **export Excel as image**. Tambahkan dependensi berikut ke `pom.xml` Anda (atau entri Gradle yang setara).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Pertahankan nomor versi tetap terbaru; rilis yang lebih baru mencakup peningkatan kinerja untuk rendering gambar.

## Langkah 2: Muat workbook dan pilih worksheet

Langkah pemrograman pertama adalah membuka file Excel dan mendapatkan referensi ke worksheet yang ingin Anda ekspor.

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load the workbook from disk
        Workbook wb = new Workbook("sample.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);
```

*Mengapa ini penting*: Memuat workbook memberi Anda akses ke objek internalnya, dan memilih worksheet yang tepat memastikan rentang yang benar dirender.

## Langkah 3: Konfigurasikan ImageOrPrintOptions (export excel as image)

`ImageOrPrintOptions` mengontrol format gambar, resolusi, dan detail rendering lainnya. Di sini kami mengatur format ke PNG, yang memenuhi persyaratan **export excel sheet to png**.

```java
        // Create options for image export
        ImageOrPrintOptions opts = new ImageOrPrintOptions();

        // Set the desired image format (PNG)
        opts.setSaveFormat(SaveFormat.PNG);

        // Optional: increase resolution for sharper output
        opts.setResolution(300);
```

Mengatur format ke `PNG` menjamin kompresi lossless, membuat file cocok untuk pemrosesan lebih lanjut atau dimasukkan ke dalam laporan.

## Langkah 4: Tambahkan gambar ke worksheet (add picture to worksheet)

Jika Anda perlu menyematkan gambar—seperti logo atau snapshot dari rentang lain—gunakan koleksi `Pictures`. Kode berikut menyisipkan gambar dari rentang `A1:G20` di sudut kiri‑atas worksheet.

```java
        // Insert a picture of the range A1:G20 at cell (0,0)
        ws.getPictures().add(0, 0, "A1:G20");
```

> **Mengapa Anda mungkin melakukan ini:** Menambahkan gambar sebelum mengekspor memungkinkan Anda menggabungkan grafik statis dengan data worksheet, menghasilkan gambar akhir yang lebih kaya.

## Langkah 5: Simpan worksheet sebagai file PNG (save excel as png file, save workbook as image)

Akhirnya, panggil `Workbook.save` dengan opsi yang telah dikonfigurasi. Metode ini menulis file PNG ke direktori yang ditentukan.

```java
        // Save the worksheet as an image file
        wb.save("output/pivot.png", opts);

        System.out.println("Export completed: output/pivot.png");
    }
}
```

Setelah program selesai, `output/pivot.png` berisi representasi pixel‑perfect dari worksheet, termasuk gambar yang Anda tambahkan.

### File sumber lengkap

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook wb = new Workbook("sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // Configure export options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PNG);
        opts.setResolution(300); // optional high‑DPI output

        // Add picture to worksheet
        ws.getPictures().add(0, 0, "A1:G20");

        // Export worksheet as PNG image
        wb.save("output/pivot.png", opts);
        System.out.println("Export completed: output/pivot.png");
    }
}
```

Menjalankan kelas menghasilkan file PNG yang ditampilkan di bawah (gambar bersifat ilustratif; file Anda akan mencerminkan konten worksheet yang sebenarnya).

![Worksheet Excel yang diekspor sebagai PNG](/images/excel-to-png.png "Hasil ekspor excel sebagai gambar menggunakan Java")

*Teks alt (image alt):* **Result of export Excel as image using Java – a PNG snapshot of the worksheet** (memenuhi persyaratan alt gambar).

## Kesulitan umum dan cara menghindarinya

| Issue | Reason | Fix |
|-------|--------|-----|
| **File not found** | Path ke `sample.xlsx` tidak benar. | Gunakan path absolut atau letakkan file di root proyek. |
| **Blank image** | Worksheet tidak memiliki konten yang terlihat atau rentang gambar kosong. | Pastikan sel `A1:G20` berisi data atau sesuaikan rentangnya. |
| **Low resolution** | DPI default adalah 96, yang dapat terlihat buram saat dicetak. | Panggil `opts.setResolution(300)` (atau lebih tinggi) sebelum menyimpan. |
| **License exception** | Menggunakan versi evaluasi dapat menambahkan watermark. | Terapkan lisensi Aspose.Cells yang valid dengan `License license = new License(); license.setLicense("Aspose.Total.lic");`. |

## Langkah selanjutnya

Sekarang Anda dapat **export Excel as image**, Anda mungkin ingin menjelajahi:

* **Export excel sheet to png** untuk setiap worksheet dalam workbook (loop melalui `wb.getWorksheets()`).
* Mengonversi PNG ke PDF menggunakan Aspose.PDF jika Anda memerlukan format yang ramah dokumen.
* Menyematkan PNG yang dihasilkan ke halaman web atau lampiran email langsung dari Java.

Ekstensi ini dibangun di atas pola `ImageOrPrintOptions` yang sama, menjaga konsistensi basis kode.

## Kesimpulan

Anda telah mempelajari cara **export Excel as image** dengan Java, cara **add picture to worksheet**, dan cara **save Excel as PNG file** menggunakan Aspose.Cells. Contoh lengkap menunjukkan cara yang dapat diandalkan untuk **save workbook as image**, menangani resolusi, dan menghindari kesalahan umum. Terapkan pola ini untuk mengotomatisasi pelaporan, menghasilkan thumbnail, atau mengintegrasikan visual spreadsheet ke dalam alur kerja berbasis Java apa pun.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang dibangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengekspor Worksheet Excel ke PNG Menggunakan Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Ekspor Workbook Excel sebagai Gambar Menggunakan Aspose.Cells untuk Java: Panduan Langkah demi Langkah](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Ekspor Workbook Excel Sebagai Gambar Menggunakan Aspose Cells Untuk Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}