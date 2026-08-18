---
category: general
date: 2026-08-17
description: Ekspor Excel ke TXT sambil membatasi digit signifikan – pelajari cara
  mengatur digit dan mengonversi Excel ke teks dalam Java dengan contoh lengkap Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: id
lastmod: 2026-08-17
og_description: Ekspor Excel ke TXT sambil membatasi digit signifikan. Tutorial ini
  menunjukkan cara mengatur digit dan mengonversi Excel ke teks menggunakan Aspose.Cells
  untuk Java.
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: Ekspor Excel ke TXT dengan digit signifikan terbatas – Panduan Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: Cara mengekspor Excel ke TXT dengan digit signifikan terbatas menggunakan Java
url: /id/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel to TXT with limited significant digits using Java

Jika Anda perlu **mengekspor Excel ke TXT** sambil mengontrol jumlah digit signifikan, panduan ini menyediakan solusi siap‑jalankan. Anda akan melihat cara mengatur digit, mengonversi Excel ke teks, dan menjaga output tetap rapi dengan satu perubahan konfigurasi.

Contoh menggunakan Aspose.Cells for Java 25.10, yang memperkenalkan opsi `setSignificantDigits`. Pada akhir tutorial Anda dapat menghasilkan file TXT yang hanya berisi digit yang Anda inginkan, tanpa kode pembulatan tambahan.

## What you’ll achieve

- Membuat workbook secara programatis.
- Menyisipkan nilai numerik ke dalam sel.
- Mengonfigurasi opsi penyimpanan TXT untuk membatasi digit signifikan.
- Menyimpan workbook sebagai file teks biasa.
- Memahami cara kerja pengaturan `significantDigits` dan cara menyesuaikannya untuk skenario lain.

### Prerequisites

- Java 17 atau lebih baru (kode juga dapat dikompilasi dengan Java 8).
- Aspose.Cells for Java 25.10 atau yang lebih baru. Unduh JAR dari [situs Aspose](https://products.aspose.com/cells/java) dan tambahkan ke classpath proyek Anda.
- IDE atau editor teks sederhana serta alat build baris perintah (Maven/Gradle).

## Step 1: Set up the project and import Aspose.Cells

Buat proyek Java baru dan tambahkan JAR Aspose.Cells ke jalur build. Jika Anda menggunakan Maven, tambahkan dependensi berikut ke `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Tip pro:** Gunakan classifier `jdk17` untuk runtime Java terbaru; ini mengurangi risiko peringatan kompatibilitas.

## Step 2: Create a workbook and write a value

Workbook mewakili file Excel dalam memori. Anda dapat menambahkan data ke sel mana pun menggunakan metode `putValue`.

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

Angka `123.456789` akan menjadi sumber untuk ekspor TXT kami. Secara default Aspose.Cells akan menulis semua tempat desimal, yang sering menghasilkan file teks berisik.

## Step 3: Configure TXT save options to limit significant digits

Aspose.Cells menyediakan `TxtSaveOptions` untuk kontrol halus atas output teks biasa. Metode `setSignificantDigits` memberi tahu exporter berapa banyak digit yang harus dipertahankan **secara keseluruhan**, bukan hanya setelah titik desimal.

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

Ketika `significantDigits` diatur ke `4`, exporter membulatkan nilai `123.456789` menjadi `123.5`. Perilaku ini sesuai dengan definisi matematis angka signifikan: empat digit non‑nol pertama dipertahankan.

### How the setting differs from “limit decimals”

- **limit decimals** (`setDecimalPlaces`) memotong digit *setelah* titik desimal, terlepas dari bagian bilangan bulat.
- **significant digits** (`setSignificantDigits`) menghitung digit mulai dari digit non‑nol pertama, yang berguna ketika angka bervariasi dalam besaran.

Jika Anda memerlukan jumlah tempat desimal tetap, ganti baris di atas dengan:

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## Step 4: Save the workbook as a TXT file

Sekarang tulis workbook ke disk menggunakan opsi yang telah dikonfigurasi.

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Menjalankan program akan membuat `significant_digits.txt` di direktori kerja. File tersebut berisi satu baris:

```
123.5
```

### Expected output

| Sel | Nilai asli | Diekspor (4 digit signifikan) |
|------|------------|--------------------------------|
| A1   | 123.456789 | 123.5                          |

Jika Anda mengubah `setSignificantDigits(4)` menjadi `6`, outputnya menjadi `123.457`. Bereksperimenlah dengan nilai berbeda untuk melihat bagaimana pembulatan beradaptasi.

## Step 5: Common variations and edge cases

### Exporting a whole range

Jika Anda ingin mengekspor lebih dari satu sel, cukup isi rentang sebelum menyimpan:

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

Pengaturan `significantDigits` yang sama berlaku untuk setiap sel numerik, memastikan presisi konsisten di seluruh file.

### Handling locale‑specific decimal separators

Aspose.Cells menghormati locale sistem saat menulis teks. Untuk memaksa titik (`.`) sebagai pemisah desimal, atur budaya `TxtSaveOptions`:

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

Ini berguna ketika aplikasi target mengharapkan format tertentu, seperti parser CSV yang hanya menerima `.`.

### Overwriting existing files

Metode `save` secara default menimpa file target. Jika Anda perlu menghindari kehilangan data secara tidak sengaja, periksa keberadaan file terlebih dahulu:

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### Large workbooks and memory usage

Saat mengekspor worksheet yang sangat besar, pertimbangkan untuk melakukan streaming output:

```java
saveOptions.setEnableMemorySaving(true);
```

Opsi ini mengurangi konsumsi heap dengan menulis baris secara bertahap.

## Full working example

Berikut adalah program lengkap yang dapat Anda salin, tempel, dan jalankan segera:

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Menjalankan kode ini menghasilkan `significant_digits.txt` dengan konten berikut (kolom dipisahkan tab):

```
123.5	0.001235	98770
```

Setiap angka menghormati aturan **4 digit signifikan**, menunjukkan bahwa pengaturan ini berfungsi pada berbagai besaran.

## Conclusion

Sekarang Anda tahu cara **mengekspor Excel ke TXT** sambil mengontrol jumlah digit signifikan. Dengan menggunakan `TxtSaveOptions.setSignificantDigits`, Anda dapat **mengatur digit**, **membatasi tempat desimal**, dan **membatasi digit signifikan** dalam satu baris kode yang dapat dipelihara. Pendekatan ini bekerja untuk sel tunggal, rentang penuh, dan workbook besar sekaligus.

### Next steps

- Jelajahi properti `TxtSaveOptions` lain seperti `setDelimiter('\t')` untuk menyesuaikan pemisah kolom.
- Gabungkan exporter dengan `CsvSaveOptions` jika Anda memerlukan nilai yang dipisahkan koma alih‑alih teks biasa.
- Integrasikan rutinitas ini ke dalam layanan web yang menerima file Excel yang diunggah dan mengembalikan output TXT yang dipangkas secara langsung.

Silakan bereksperimen dengan batas digit dan locale yang berbeda. Jika Anda menemukan skenario di mana opsi bawaan tidak memenuhi kebutuhan khusus, Anda selalu dapat memproses file TXT yang dihasilkan dengan utilitas I/O Java standar.

Selamat coding!

## What Should You Learn Next?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Convert Text to Numbers in Excel Using Aspose.Cells for Java](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Export Custom Excel Properties to PDF Using Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}