---
category: general
date: 2026-06-21
description: Menyalin rentang lembar kerja secara programatis di Java menggunakan
  Aspose.Cells. Pelajari cara menyalin rentang Excel ke buku kerja lain secara efisien.
draft: false
keywords:
- programmatically copy worksheet range
- how to copy excel range to another workbook
- Aspose.Cells copy range Java
- copy pivot table between workbooks
- Java Excel automation
language: id
og_description: Menyalin rentang lembar kerja secara programatis di Java. Panduan
  ini menunjukkan cara menyalin rentang Excel ke buku kerja lain dengan kode lengkap
  dan tips.
og_title: Menyalin Rentang Lembar Kerja Secara Programatis – Java Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  headline: Programmatically Copy Worksheet Range – Complete Java Guide
  type: TechArticle
- description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  name: Programmatically Copy Worksheet Range – Complete Java Guide
  steps:
  - name: 1. Copying Across Different Excel Versions
    text: Aspose.Cells works with `.xls`, `.xlsx`, `.xlsb`, and even `.csv`. If the
      source and destination use different formats, the library automatically converts
      them. Just ensure the file extensions match your desired output.
  - name: 2. Preserving External Data Sources in Pivot Tables
    text: If the pivot table in the source references an external data source (e.g.,
      a database connection), the copied pivot will retain the connection string but
      **won’t automatically refresh**. Call `pivotTable.refreshData()` after copying
      if you need up‑to‑date results.
  - name: 3. Large Ranges and Memory Consumption
    text: Copying massive ranges (hundreds of thousands of rows) can spike memory
      usage. Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` before
      loading large files to keep the footprint low.
  - name: 4. Multiple Sheets or Ranges
    text: If you need to copy several non‑contiguous ranges, repeat steps 4‑6 for
      each range, or use `copyRange` with a union range (`Cells.createRange("A1:B10,C1:D10")`).
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook
- Automation
title: Menyalin Rentang Lembar Kerja Secara Programatis – Panduan Java Lengkap
url: /id/java/range-management/programmatically-copy-worksheet-range-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menyalin Rentang Worksheet Secara Programatis – Panduan Java Lengkap

Pernah bertanya-tanya bagaimana cara **menyalin rentang worksheet secara programatis** tanpa membuka Excel secara manual? Anda tidak sendirian. Baik Anda perlu menggandakan laporan, mengkloning dasbor berbasis pivot, atau sekadar memindahkan data antar file, melakukannya dalam kode menghemat waktu dan menghilangkan kesalahan manusia.

Dalam tutorial ini kami akan membahas solusi bersih, end‑to‑end yang menunjukkan **cara menyalin rentang excel ke workbook lain** menggunakan Java dan pustaka Aspose.Cells. Pada akhir tutorial Anda akan memiliki program siap‑jalankan, memahami alasan di balik setiap langkah, dan mengetahui jebakan yang perlu diwaspadai.

---

## Apa yang Anda Butuhkan

- **Java Development Kit (JDK) 11+** – kode ini dapat dikompilasi dengan JDK terbaru apa pun.
- **Aspose.Cells for Java** (versi percobaan gratis atau berlisensi). Tambahkan dependensi Maven atau unduh JAR.
- Dua file Excel: sebuah `input.xlsx` yang berisi rentang sumber (termasuk tabel pivot) dan sebuah `output.xlsx` kosong tempat rentang akan ditempatkan.
- IDE apa pun yang Anda suka – IntelliJ IDEA, Eclipse, atau bahkan editor teks sederhana.

Itu saja. Tidak ada layanan tambahan, tidak ada interop COM, hanya Java murni.

![Diagram yang menggambarkan penyalinan rentang worksheet secara programatis antara dua workbook](image.png)

*Teks alt gambar: ilustrasi penyalinan rentang worksheet secara programatis*

## Langkah 1: Siapkan Proyek dan Impor Aspose.Cells

Pertama-tama, kita perlu pustaka di classpath. Jika Anda menggunakan Maven, tambahkan:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Jika Anda lebih suka JAR manual, letakkan di folder `libs` Anda dan tambahkan ke jalur build.

Mengapa ini penting: Aspose.Cells memberikan model objek yang kaya (`Workbook`, `Worksheet`, `Range`) yang memungkinkan kita menyalin data **termasuk tabel pivot, formula, dan pemformatan** dalam satu panggilan—sesuatu yang tidak dapat dilakukan pustaka Apache POI biasa secara bersih.

## Langkah 2: Muat Workbook Sumber

Kami akan membuka workbook yang berisi data yang ingin kami kloning. Konstruktor `Workbook` menerima jalur file, dan Aspose akan membaca seluruh file ke dalam memori.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Tip pro:* Bungkus pemuatan dalam blok try‑catch jika file mungkin tidak ada; jika tidak, program akan berhenti dengan error yang jelas.

## Langkah 3: Buat Workbook Tujuan yang Kosong

Workbook baru memberi kita kanvas bersih. Kita tidak perlu mengisi sheet sebelumnya; Aspose akan menambahkan satu untuk kita.

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();
```

Mengapa tidak menggunakan kembali sumber? Memisahkannya mencegah penimpaan tidak sengaja dan membuat kode dapat digunakan kembali untuk operasi batch.

## Langkah 4: Tentukan Rentang Tepat untuk Disalin

Di sinilah magi **menyalin rentang worksheet secara programatis** dimulai. Kami memilih sel `A1:D20` dari worksheet pertama file sumber. Metode `createRange` mengembalikan objek `Range` yang mewakili tepat sel‑sel tersebut, termasuk tabel pivot.

```java
        // Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)               // first sheet (index 0)
                                          .getCells()
                                          .createRange("A1:D20");
```

Jika Anda membutuhkan rentang dinamis (misalnya, “baris terakhir yang digunakan”), Anda dapat mengganti alamat yang ditulis keras dengan `Cells.maxDisplayRange` atau menghitungnya dengan `Cells.getMaxDataColumn()` dan `Cells.getMaxDataRow()`.

## Langkah 5: Tambahkan Worksheet Target di Workbook Tujuan

Aspose membuat sheet default bernama “Sheet1” saat Anda menginstansiasi `Workbook`. Kami akan menambahkan yang baru untuk menjaga kerapihan, terutama jika Anda berencana menyalin beberapa rentang nanti.

```java
        // Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
```

Anda dapat memberi sheet nama yang ramah:

```java
        targetWorksheet.setName("CopiedData");
```

## Langkah 6: Lakukan Penyalinan – Termasuk Tabel Pivot

Sekarang operasi inti: `copyRange`. Metode ini menyalin **nilai, formula, pemformatan, dan objek tersemat** (seperti tabel pivot) dari rentang sumber ke sel tujuan (`A1` di sheet baru kami). Ini adalah cara paling sederhana untuk mencapai **cara menyalin rentang excel ke workbook lain** tanpa harus berurusan dengan loop sel tingkat rendah.

```java
        // Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)               // source sheet index
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");
```

Di balik layar, Aspose menserialisasi rentang sumber ke format menengah, lalu mendeserialisasikannya ke sheet target—sehingga semuanya tetap utuh.

## Langkah 7: Simpan Workbook Tujuan dan Verifikasi

Akhirnya, kami menulis workbook tujuan ke disk. Buka `output.xlsx` di Excel untuk melihat rentang yang disalin, tabel pivot, dan semua gaya yang dipertahankan.

```java
        // (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");
        System.out.println("Range copied successfully!");
    }
}
```

Saat Anda membuka `output.xlsx`, Anda akan melihat sheet bernama “CopiedData” dengan tata letak yang sama seperti `A1:D20` dari sumber, termasuk tabel pivot yang kini mengacu pada data yang disalin.

## Menangani Kasus Tepi Umum

### 1. Menyalin Antara Versi Excel yang Berbeda
Aspose.Cells bekerja dengan `.xls`, `.xlsx`, `.xlsb`, dan bahkan `.csv`. Jika sumber dan tujuan menggunakan format berbeda, pustaka secara otomatis mengonversinya. Pastikan ekstensi file sesuai dengan output yang diinginkan.

### 2. Mempertahankan Sumber Data Eksternal pada Tabel Pivot
Jika tabel pivot di sumber merujuk ke sumber data eksternal (misalnya, koneksi basis data), pivot yang disalin akan mempertahankan string koneksi tetapi **tidak akan menyegarkan secara otomatis**. Panggil `pivotTable.refreshData()` setelah menyalin jika Anda memerlukan hasil yang terbaru.

```java
        PivotTable pt = targetWorksheet.getPivotTables().get(0);
        pt.refreshData();
        pt.calculateData();
```

### 3. Rentang Besar dan Konsumsi Memori
Menyalin rentang yang sangat besar (ratusan ribu baris) dapat meningkatkan penggunaan memori. Gunakan `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` sebelum memuat file besar untuk menjaga jejak memori tetap rendah.

### 4. Beberapa Sheet atau Rentang
Jika Anda perlu menyalin beberapa rentang yang tidak bersebelahan, ulangi langkah 4‑6 untuk setiap rentang, atau gunakan `copyRange` dengan rentang gabungan (`Cells.createRange("A1:B10,C1:D10")`).

## Tips Pro untuk Otomasi yang Kuat

- **Validasi rentang sumber** sebelum menyalin. Gunakan `sourceRange.isValid()` untuk menghindari error pada runtime.
- **Kunci file tujuan** dengan `FileInfo.setReadOnly(false)` jika Anda menimpa workbook yang sudah ada.
- **Catat aksi** dengan logger ringan (SLF4J) – sangat berguna saat memproses batch.
- **Bebaskan workbook** (`sourceWorkbook.dispose(); destinationWorkbook.dispose();`) dalam layanan yang berjalan lama untuk membebaskan sumber daya native.

## Ringkasan Contoh Kerja Lengkap

Berikut adalah kelas Java lengkap yang berdiri sendiri yang dapat Anda tempelkan ke IDE dan jalankan. Ingatlah untuk mengganti `YOUR_DIRECTORY` dengan jalur folder sebenarnya di mesin Anda.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2️⃣ Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 3️⃣ Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:D20");

        // 4️⃣ Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
        targetWorksheet.setName("CopiedData");

        // 5️⃣ Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");

        // 6️⃣ (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");

        System.out.println("Programmatically copy worksheet range completed successfully.");
    }
}
```

**Output yang diharapkan:** Sebuah file `output.xlsx` dengan sheet bernama “CopiedData”. Sel `A1:D20` akan mencerminkan sumber, dan setiap tabel pivot di dalam blok tersebut akan berfungsi penuh, mengacu pada data yang disalin.

## Kesimpulan

Kami baru saja mendemonstrasikan solusi bersih, **menyalin rentang worksheet secara programatis** dalam Java, menjawab pertanyaan umum **cara menyalin rentang excel ke workbook lain**. Dengan memanfaatkan API tingkat tinggi Aspose.Cells kami menghindari loop sel tingkat rendah, mempertahankan tabel pivot, dan menjaga kode tetap mudah dibaca.

Apa selanjutnya? Cobalah memperluas pola ini ke:

- Menyalin seluruh worksheet alih-alih satu rentang.
- Memproses batch puluhan workbook dalam sebuah folder.
- Mengekspor rentang yang disalin ke CSV atau PDF untuk pipeline pelaporan.

Silakan bereksperimen, dan bila Anda menemui kendala, tinggalkan komentar. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode kerja lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menyalin Beberapa Kolom di Excel Menggunakan Aspose.Cells Java: Panduan Lengkap](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Menyalin Kolom Excel Secara Efisien Menggunakan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/range-management/copy-excel-columns-aspose-cells-java/)
- [Menyalin Gambar Antara Sheet di Excel Menggunakan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}