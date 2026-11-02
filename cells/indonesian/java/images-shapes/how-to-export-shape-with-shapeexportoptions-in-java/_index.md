---
category: general
date: 2026-10-01
description: Pelajari cara mengekspor shape dengan ShapeExportOptions di Java, menjaga
  shape tetap dapat diedit saat mengonversi ke PPTX menggunakan Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export shape with ShapeExportOptions
- Aspose Cells export shape
- Java export shape to PPTX
- editable shape export
- ShapeExportOptions setExportAsEditable
- export textbox shape
language: id
lastmod: 2026-10-01
og_description: Ekspor bentuk dengan ShapeExportOptions di Java untuk membuat file
  PPTX yang dapat diedit. Tutorial ini memandu Anda melalui proses lengkap menggunakan
  Aspose.Cells.
og_image_alt: Screenshot showing Java code exporting a textbox shape to PPTX using
  ShapeExportOptions
og_title: Ekspor bentuk dengan ShapeExportOptions di Java – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  headline: How to export shape with ShapeExportOptions in Java
  type: TechArticle
- description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  name: How to export shape with ShapeExportOptions in Java
  steps:
  - name: Expected result
    text: '- `textbox.pptx` appears in the specified directory. - Opening the file
      in PowerPoint shows a single slide with the original textbox. - The textbox
      is fully editable (you can change text, font, size, etc.).'
  - name: Verify programmatically
    text: '```java // Load the generated PPTX to confirm it contains one slide Presentation
      presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx"); int slideCount
      = presentation.getSlides().size(); System.out.println("Slides in exported PPTX:
      " + slideCount); ```'
  - name: 'Edge case: Multiple shapes'
    text: 'If the worksheet contains several shapes and you only want a specific one,
      locate it by name:'
  - name: 'Edge case: Shape not found'
    text: '```java if (worksheet.getShapes().size() == 0) { throw new IllegalStateException("No
      shapes found on the worksheet."); } ```'
  - name: 'Edge case: Export to other formats'
    text: '`ShapeExportOptions` also supports PNG, JPEG, SVG, and EMF. Change the
      file extension and optionally set `exportOptions.setImageFormat(ImageFormat.PNG)`.'
  - name: Conclusion
    text: You now know how to **export shape with ShapeExportOptions** in Java, preserving
      editability when converting a textbox (or any other shape) to a PPTX file. By
      following the steps above—setting up the library, loading the workbook, configuring
      `ShapeExportOptions`, and invoking `exportToImage`—you ca
  type: HowTo
tags:
- Aspose.Cells
- Java
- ShapeExportOptions
- PPTX
- Export
title: Cara mengekspor bentuk dengan ShapeExportOptions di Java
url: /id/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengekspor shape dengan ShapeExportOptions di Java

Jika Anda perlu **mengekspor shape dengan ShapeExportOptions** dari workbook Excel, panduan ini menunjukkan langkah‑langkah tepatnya. Anda akan melihat cara menjaga shape tetap dapat diedit saat mengonversinya menjadi file PPTX, yang penting untuk penyuntingan lanjutan di PowerPoint.

Mengekspor shape adalah tugas umum ketika Anda menghasilkan deck slide dari spreadsheet—baik Anda membuat deck penjualan, dasbor pelaporan, atau presentasi otomatis. Tutorial ini mencakup semua yang Anda perlukan, mulai dari penyiapan proyek hingga memverifikasi file yang diekspor, dan menggunakan pustaka **Aspose.Cells for Java**.

## Apa yang Anda perlukan

- Java 17 atau lebih baru (kode dapat dikompilasi dengan JDK terbaru apa pun)
- Maven atau Gradle untuk manajemen dependensi
- File Excel (`Shapes.xlsx`) yang berisi setidaknya satu textbox atau shape lain
- Familiaritas dasar dengan API Aspose.Cells

## Langkah 1: Tambahkan Aspose.Cells ke proyek Anda (Aspose Cells export shape)

Jika Anda menggunakan Maven, tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest stable version -->
</dependency>
```

Untuk Gradle, letakkan ini di `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Pro tip:** Daftarkan lisensi Anda lebih awal untuk menghindari watermark evaluasi.  
> ```java
> License license = new License();
> license.setLicense("Aspose.Total.Java.lic");
> ```

## Langkah 2: Muat workbook yang berisi shape

```java
// Load the workbook that contains the shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

Objek `Workbook` mewakili seluruh file Excel. Memuatnya adalah prasyarat pertama untuk manipulasi shape apa pun.

## Langkah 3: Akses worksheet dan ambil shape yang diinginkan (Java export shape to PPTX)

```java
// Access the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);

// Retrieve the first shape on the sheet.
// You can also use get("ShapeName") if you know the shape's name.
Shape textBoxShape = worksheet.getShapes().get(0);
```

> **Mengapa ini penting:** Shape disimpan per‑worksheet, jadi Anda harus menavigasi ke sheet yang tepat sebelum dapat mengekspor shape tertentu.

## Langkah 4: Konfigurasikan **ShapeExportOptions** agar shape tetap dapat diedit (editable shape export)

```java
// Create export options and enable editable export
ShapeExportOptions exportOptions = new ShapeExportOptions();
exportOptions.setExportAsEditable(true); // <-- makes the shape editable in PPTX
```

Mengatur `ExportAsEditable` ke `true` memberi tahu Aspose.Cells untuk mempertahankan data vektor shape, memungkinkan pengguna PowerPoint mengubah shape setelah diimpor.

## Langkah 5: Ekspor shape langsung ke file PPTX (export textbox shape)

```java
// Export the shape as a PPTX file
textBoxShape.exportToImage("YOUR_DIRECTORY/textbox.pptx", exportOptions);
```

Metode `exportToImage` bekerja untuk beberapa format gambar; ketika nama file target diakhiri dengan `.pptx`, Aspose.Cells menulis slide PowerPoint yang berisi shape tersebut.

### Hasil yang diharapkan

- `textbox.pptx` muncul di direktori yang ditentukan.
- Membuka file di PowerPoint menampilkan satu slide dengan textbox asli.
- Textbox dapat diedit sepenuhnya (Anda dapat mengubah teks, font, ukuran, dll.).

## Langkah 6: Verifikasi output dan tangani kasus tepi umum

### Verifikasi secara programatik

```java
// Load the generated PPTX to confirm it contains one slide
Presentation presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx");
int slideCount = presentation.getSlides().size();
System.out.println("Slides in exported PPTX: " + slideCount);
```

Jika `slideCount` sama dengan `1`, ekspor berhasil.

### Kasus tepi: Banyak shape

Jika worksheet berisi beberapa shape dan Anda hanya menginginkan satu tertentu, temukan dengan nama:

```java
Shape targetShape = worksheet.getShapes().get("MyTextBox");
targetShape.exportToImage("output.pptx", exportOptions);
```

### Kasus tepi: Shape tidak ditemukan

```java
if (worksheet.getShapes().size() == 0) {
    throw new IllegalStateException("No shapes found on the worksheet.");
}
```

### Kasus tepi: Ekspor ke format lain

`ShapeExportOptions` juga mendukung PNG, JPEG, SVG, dan EMF. Ubah ekstensi file dan opsional set `exportOptions.setImageFormat(ImageFormat.PNG)`.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua bagian memberikan Anda program mandiri yang dapat Anda salin‑tempel ke IDE Anda:

```java
import com.aspose.cells.*;

public class ExportShapeExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");

        // 2️⃣ Get first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Retrieve the first shape (or use get("ShapeName"))
        Shape shape = worksheet.getShapes().get(0);

        // 4️⃣ Prepare export options for editable PPTX
        ShapeExportOptions options = new ShapeExportOptions();
        options.setExportAsEditable(true); // keep shape editable

        // 5️⃣ Export to PPTX
        String outPath = "YOUR_DIRECTORY/textbox.pptx";
        shape.exportToImage(outPath, options);
        System.out.println("Shape exported to " + outPath);

        // 6️⃣ Optional verification
        Presentation pres = new Presentation(outPath);
        System.out.println("Slide count: " + pres.getSlides().size());
    }
}
```

Menjalankan program membuat `textbox.pptx`. Buka di PowerPoint, klik kanan pada textbox, dan Anda akan melihat pegangan penyuntingan biasa—mengonfirmasi bahwa **export shape with ShapeExportOptions** mempertahankan kemampuan edit.

## Pertanyaan yang sering diajukan

| Pertanyaan | Jawaban |
|------------|---------|
| *Apakah saya dapat mengekspor shape chart?* | Ya. Panggilan `exportToImage` yang sama berfungsi untuk chart, gambar, dan SmartArt. |
| *Bagaimana jika saya membutuhkan PNG dengan resolusi lebih tinggi?* | Setel `options.setImageFormat(ImageFormat.PNG)` dan sesuaikan `options.setResolution(300)` sebelum mengekspor. |
| *Apakah PPTX yang diekspor kompatibel dengan versi PowerPoint yang lebih lama?* | Pustaka menulis Office Open XML (PPTX) yang didukung oleh PowerPoint 2007 dan versi selanjutnya. |
| *Apakah saya memerlukan lisensi agar ini berfungsi?* | Evaluasi gratis berfungsi tetapi menambahkan watermark. Daftarkan lisensi untuk menghilangkannya. |

## Langkah selanjutnya

- Jelajahi **Aspose.Slides for Java** jika Anda perlu menggabungkan beberapa shape yang diekspor menjadi satu deck slide.
- Gunakan **ShapeExportOptions.setExportAsEditable(false)** ketika Anda lebih memilih gambar raster (PNG/JPEG) untuk rendering yang lebih cepat.
- Otomatiskan pemrosesan batch: iterasi semua worksheet dan ekspor setiap shape ke file PPTX terpisah.

---

### Kesimpulan

Anda sekarang tahu cara **mengekspor shape dengan ShapeExportOptions** di Java, mempertahankan kemampuan edit saat mengonversi textbox (atau shape lain) ke file PPTX. Dengan mengikuti langkah‑langkah di atas—menyiapkan pustaka, memuat workbook, mengonfigurasi `ShapeExportOptions`, dan memanggil `exportToImage`—Anda dapat mengintegrasikan ekspor shape ke dalam pipeline pelaporan otomatis apa pun.

Silakan bereksperimen dengan berbagai shape, format output, dan pengaturan resolusi. Jika Anda menemukan panduan ini berguna, bagikan kepada rekan tim atau tandai untuk referensi di masa mendatang. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menyesuaikan Margin Shape di Excel Menggunakan Aspose.Cells untuk Java](/cells/english/java/images-shapes/excel-aspose-cells-java-shape-margins/)
- [Cara Menerapkan Pemformatan Shape 3D di Excel Menggunakan Aspose.Cells untuk Java](/cells/english/java/images-shapes/aspose-cells-java-3d-shape-formatting/)
- [Panduan Penyalinan Shape Workbook Aspose Cells Java](/cells/hindi/java/images-shapes/aspose-cells-java-workbook-shape-copying-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}