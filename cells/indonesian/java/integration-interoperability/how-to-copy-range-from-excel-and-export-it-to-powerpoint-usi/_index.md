---
category: general
date: 2026-09-05
description: Pelajari cara menyalin rentang di Excel, mengekspor Excel ke PowerPoint,
  dan mengonversi Excel ke pptx dengan contoh Java lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- export excel to powerpoint
- convert excel to pptx
- copy pivot table sheet
- how to export excel
language: id
lastmod: 2026-09-05
og_description: Cara menyalin rentang dan mengekspor Excel ke PowerPoint menggunakan
  Java. Ikuti panduan langkah demi langkah ini untuk mengonversi Excel ke PPTX secara
  efisien.
og_image_alt: Screenshot showing how to copy range from Excel to PowerPoint in a Java
  IDE
og_title: Cara menyalin rentang dari Excel dan mengekspornya ke PowerPoint dalam Java
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to copy range in Excel, export excel to PowerPoint and convert
    excel to pptx with a complete Java example.
  headline: How to copy range from Excel and export it to PowerPoint using Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Cara menyalin rentang dari Excel dan mengekspornya ke PowerPoint menggunakan
  Java
url: /id/java/integration-interoperability/how-to-copy-range-from-excel-and-export-it-to-powerpoint-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin rentang dari Excel dan mengekspornya ke PowerPoint menggunakan Java

Jika Anda perlu **how to copy range** dari sebuah workbook Excel dan kemudian **export excel to PowerPoint**, panduan ini memberikan solusi lengkap yang siap dijalankan. Anda akan melihat secara tepat cara menyalin rentang yang berisi pivot‑table, membuat worksheet baru untuk salinan, dan akhirnya **convert Excel to PPTX** dengan satu pemanggilan metode.

Menyalin rentang dan mengekspor workbook adalah kebutuhan umum ketika Anda menghasilkan laporan, deck slide, atau dashboard secara programatis. Pada akhir tutorial ini Anda akan memiliki program Java yang:

* Memuat file `.xlsx` yang sudah ada.
* Menyalin rentang `A1:H20` (termasuk pivot table) ke sheet baru.
* Menyimpan workbook sebagai presentasi `.pptx` yang dapat diedit.

Anda hanya memerlukan pustaka Aspose.Cells for Java; tidak ada dependensi tambahan yang diperlukan.

## Prerequisites

Sebelum Anda memulai, pastikan Anda memiliki:

* Java 17 (atau lebih baru) terpasang.
* Maven atau Gradle untuk mengelola dependensi.
* Aspose.Cells for Java 23.9 (atau versi terbaru) – tambahkan ke proyek Anda seperti yang ditunjukkan pada cuplikan Maven di bawah.
* File Excel (`input.xlsx`) yang berisi data dan pivot table yang ingin Anda salin.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

## Step 1: Load the workbook from a file

Operasi pertama dalam **how to copy range** adalah membuka workbook sumber. Ini memberi Anda akses ke worksheet, sel, dan pivot table.

```java
// Load the workbook from a file
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Mengapa langkah ini?*  
Memuat file membuat representasi dalam memori dari dokumen Excel, memungkinkan Anda memanipulasi isinya tanpa menyentuh file asli.

## Step 2: Get the source worksheet that holds the data

Biasanya sheet pertama berisi data yang ingin Anda salin. Anda dapat mengambilnya berdasarkan indeks.

```java
// Get the source worksheet (first sheet) that contains the data/pivot table
Worksheet sourceSheet = workbook.getWorksheets().get(0);
```

Jika workbook Anda menyimpan pivot table pada sheet yang berbeda, ganti `0` dengan indeks yang sesuai atau gunakan `get("SheetName")`.

## Step 3: Add a new worksheet for the copied range

Membuat sheet tujuan memisahkan data yang disalin dan membuat proses ekspor selanjutnya menjadi lebih bersih.

```java
// Add a new worksheet that will receive the copied range
Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
```

Anda dapat memberi nama sheet apa saja; nama “Copy” secara jelas menandakan bahwa sheet tersebut berisi rentang yang diduplikasi.

## Step 4: Copy the range (how to copy range) including the pivot table

Sekarang kita melakukan operasi inti **how to copy range**. Metode `copyRange` menyalin nilai dan format, serta mempertahankan definisi pivot table.

```java
// Copy the range A1:H20 (including the pivot table) to the new sheet starting at A1
sourceSheet.getCells().copyRange(
        "A1:H20",
        destinationSheet.getCells().get("A1"),
        new CopyOptions()   // default options copy values, formats, and objects
);
```

*Mengapa menggunakan `CopyOptions`?*  
Memberikan instance `CopyOptions` memungkinkan Anda menyesuaikan apa yang disalin (misalnya, formula, lebar kolom). Konstruktor default menyalin semuanya, yang ideal ketika Anda menginginkan replika persis dari **copy pivot table sheet**.

## Step 5: Prepare options to export the workbook as an editable PowerPoint presentation

Ekspor ke PowerPoint dilakukan melalui `ImageOrPrintOptions`. Menetapkan format penyimpanan ke `SaveFormat.PPTX` memberi tahu Aspose.Cells untuk menghasilkan file PowerPoint alih-alih gambar.

```java
// Prepare options to export the workbook as an editable PowerPoint presentation
ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
pptOptions.setSaveFormat(SaveFormat.PPTX);   // this enables export excel to powerpoint
```

Anda juga dapat menyesuaikan dimensi slide, DPI, dan pengaturan presentasi lainnya melalui `pptOptions` jika memerlukan tata letak khusus.

## Step 6: Save the workbook as a PPTX file (convert excel to pptx)

Akhirnya, panggil `workbook.save` dengan opsi PPTX. Langkah ini **how to export excel** ke dalam deck slide.

```java
// Save the workbook to a PPTX file using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);
```

Setelah program selesai, `output.pptx` akan berisi satu slide di mana rentang yang disalin muncul persis seperti di Excel, termasuk kontrol pivot table.

### Expected output

Buka `output.pptx` di Microsoft PowerPoint atau penampil kompatibel lainnya. Anda akan melihat satu slide dengan rentang `A1:H20` ditampilkan, mempertahankan warna sel, border, dan tata letak pivot table. Slide tersebut sepenuhnya dapat diedit—Anda dapat memindahkan, mengubah ukuran, atau memformat tabel seperti konten PowerPoint native lainnya.

## Full runnable example

Menggabungkan semua langkah memberikan Anda kelas Java yang berdiri sendiri:

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Get the source worksheet (first sheet)
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // 3. Add a destination worksheet
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // 4. Copy the range A1:H20 (including pivot table)
        sourceSheet.getCells().copyRange(
                "A1:H20",
                destinationSheet.getCells().get("A1"),
                new CopyOptions()
        );

        // 5. Configure export options for PowerPoint
        ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
        pptOptions.setSaveFormat(SaveFormat.PPTX);

        // 6. Save as PPTX
        workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);

        System.out.println("Export completed: output.pptx created successfully.");
    }
}
```

Jalankan kelas tersebut dari IDE Anda atau via command line:

```bash
mvn compile exec:java -Dexec.mainClass=ExcelToPowerPoint
```

Anda akan melihat pesan konfirmasi setelah file berhasil ditulis.

## Common questions and edge cases

| Question | Answer |
|----------|--------|
| **Can I copy a non‑contiguous range?** | Gunakan `copyRange` dengan named range yang mencakup beberapa area, atau panggil `copyRange` beberapa kali untuk tiap blok. |
| **What if the source sheet contains multiple pivot tables?** | Setiap pivot table di dalam rectangle yang disalin akan dipindahkan. Untuk tabel di luar rectangle, salin secara terpisah. |
| **How do I export multiple sheets as separate slides?** | Loop melalui worksheets, salin masing‑masing ke sheet sementara, dan panggil `workbook.save` dengan `pptOptions` untuk setiap iterasi, menambahkan ke PPTX yang sama melalui API `Presentation`. |
| **Is the generated PPTX editable?** | Ya. Ekspor menghasilkan objek PowerPoint native, sehingga Anda dapat memodifikasi teks, mengubah bentuk tabel, atau menambahkan animasi setelahnya. |
| **What about large workbooks?** | Tingkatkan `pptOptions.setDpi(300)` untuk fidelitas lebih tinggi, namun perhatikan penggunaan memori; proses sheet secara batch bila diperlukan. |

## Pro tips

* **Preserve column widths** – set `CopyOptions.setColumnWidth(true)` sebelum menyalin jika Anda memerlukan pencocokan lebar kolom yang tepat.
* **Use a custom slide size** – `pptOptions.setImageHeight(720); pptOptions.setImageWidth(1280);` untuk menyesuaikan presentasi 16:9.
* **Add a title slide** – setelah mengekspor, buka PPTX dengan Aspose.Slides dan tambahkan slide judul beserta tanggal di bagian depan.

## Conclusion

Anda kini tahu **how to copy range** dari workbook Excel, **export excel to PowerPoint**, dan **convert excel to pptx** menggunakan Java. Dengan mengikuti enam langkah di atas, Anda dapat mengotomatisasi pembuatan laporan, membuat deck slide dari data live, dan mempertahankan fungsionalitas pivot‑table.

### What’s next?

* Jelajahi variasi **copy pivot table sheet** seperti menyalin hanya pivot cache.
* Gabungkan alur kerja ini dengan **Aspose.Slides** untuk menambahkan animasi atau branding khusus.
* Otomatisasi pemrosesan batch untuk puluhan workbook dalam job terjadwal.

Silakan bereksperimen dengan opsi-opsi tersebut dan sesuaikan kode dengan pipeline pelaporan Anda sendiri. Jika Anda menemui masalah, dokumentasi Aspose.Cells for Java menyediakan wawasan lebih dalam tentang `CopyOptions` dan `ImageOrPrintOptions`. Selamat coding!

## What Should You Learn Next?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Export Excel to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java&#58; A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}