---
category: general
date: 2026-09-21
description: Pelajari cara menyalin rentang di Java sambil mempertahankan tabel pivot.
  Panduan langkah demi langkah ini menunjukkan cara mengekspor tabel pivot dengan
  aman.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- preserve pivot table
- export pivot table
- how to preserve pivot
language: id
lastmod: 2026-09-21
og_description: Cara menyalin rentang di Java sambil mempertahankan tabel pivot. Ikuti
  panduan lengkap ini untuk mengekspor tabel pivot dengan aman.
og_image_alt: Screenshot of Java code copying a range and preserving a pivot table
og_title: Cara menyalin rentang dan mempertahankan tabel pivot di Java
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  headline: How to copy range and preserve a pivot table in Java
  type: TechArticle
- description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  name: How to copy range and preserve a pivot table in Java
  steps:
  - name: Load the source workbook
    text: '```java // Load the source workbook that contains the pivot table Workbook
      srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx"); Worksheet srcWs = srcWb.getWorksheets().get(0);
      ```'
  - name: Define the range that covers the pivot table
    text: '```java // Define the range covering the pivot table (including its data
      source) Range srcRange = srcWs.getCells().createRange("A1:G20"); ```'
  - name: Create an empty destination workbook
    text: '```java // Create a new, empty destination workbook Workbook destWb = new
      Workbook(); Worksheet destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range – the pivot table is preserved
    text: '```java // Copy the defined range to the destination sheet – the pivot
      table is preserved destWs.getCells().copyRange(srcRange, new CellArea("A1",
      "G20")); ```'
  - name: Save the destination workbook
    text: '```java // Save the destination workbook with the copied pivot table destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
      ```'
  - name: Copy pivot table across different workbook versions
    text: Aspose.Cells supports older `.xls` files as well as the newer `.xlsx` format.
      The same code works regardless of the file extension, making it a universal
      solution for **how to preserve pivot** across versions.
  - name: Preserving pivot table when using a filtered source
    text: 'If the source pivot is filtered, the filter state is also copied. Should
      you need to reset filters in the destination, call `PivotTable.refreshData()`
      after copying:'
  - name: Export pivot table as a static snapshot
    text: Sometimes you may want a static copy (values only) rather than a live pivot.
      Replace `copyRange` with `copyRange` followed by `pt.setEnableRefresh(false)`
      to disable further calculations.
  - name: Handling large workbooks
    text: For workbooks with many worksheets, limit the copy operation to the specific
      sheet to reduce memory usage. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to fine‑tune performance.
  type: HowTo
tags:
- Java
- Aspose.Cells
- pivot table
- Excel automation
- range copy
title: Cara menyalin rentang dan mempertahankan tabel pivot di Java
url: /id/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin rentang dan mempertahankan tabel pivot di Java

Jika Anda perlu **how to copy range** yang berisi tabel pivot, panduan ini menunjukkan cara yang dapat diandalkan untuk menjaga pivot tetap utuh. Banyak pengembang mengalami kehilangan pivot saat mengekspor data, tetapi pendekatan di bawah ini memungkinkan Anda **copy pivot table** data tanpa merusak fungsionalitasnya. Pada akhir tutorial ini Anda akan dapat **preserve pivot table** struktur, **export pivot table** file, dan memahami **how to preserve pivot** dalam berbagai skenario.

Contoh ini menggunakan Aspose.Cells for Java, sebuah perpustakaan populer untuk otomatisasi Excel. Tidak diperlukan alat tambahan selain lingkungan pengembangan Java standar.

## Prasyarat

Sebelum Anda mulai, pastikan Anda memiliki:

* Java 17 (atau lebih baru) terpasang.
* Maven atau Gradle untuk mengelola dependensi.
* Aspose.Cells for Java (versi 23.9 atau lebih baru). Tambahkan dependensi Maven berikut:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

* Sebuah workbook sumber (`Source.xlsx`) yang berisi tabel pivot yang ingin Anda salin.

## Cara menyalin rentang dan menjaga tabel pivot tetap utuh

Ide utama adalah menyalin **range** yang melingkupi seluruh pivot—termasuk sumber datanya—menggunakan `copyRange`. Metode ini menyalin baik data mentah maupun definisi pivot, memastikan workbook tujuan menerima pivot yang berfungsi penuh.

### Langkah 1: Muat workbook sumber

```java
// Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Mengapa langkah ini?*  
Muat workbook memberi Anda akses ke worksheet yang menyimpan pivot. Kelas `Workbook` mengabstraksi seluruh file Excel, sementara `Worksheet` menyediakan operasi tingkat sel.

### Langkah 2: Tentukan rentang yang mencakup tabel pivot

```java
// Define the range covering the pivot table (including its data source)
Range srcRange = srcWs.getCells().createRange("A1:G20");
```

*Mengapa langkah ini?*  
Tabel pivot bukan satu sel tunggal; ia mencakup blok yang meliputi header, baris data, dan cache pivot. Dengan menentukan rentang yang sepenuhnya mencakup pivot, Anda menjamin bahwa `copyRange` juga menyalin cache yang mendasarinya, yang penting untuk perilaku **preserve pivot table**.

### Langkah 3: Buat workbook tujuan yang kosong

```java
// Create a new, empty destination workbook
Workbook destWb = new Workbook();
Worksheet destWs = destWb.getWorksheets().get(0);
```

*Mengapa langkah ini?*  
Memulai dengan workbook bersih mencegah konflik tidak sengaja dengan sheet atau named range yang ada. Workbook tujuan akan menerima rentang yang disalin, secara efektif **export pivot table** konten.

### Langkah 4: Salin rentang – tabel pivot dipertahankan

```java
// Copy the defined range to the destination sheet – the pivot table is preserved
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
```

*Mengapa langkah ini?*  
`copyRange` melakukan deep copy: nilai sel, format, dan metadata pivot dipindahkan. Ini adalah operasi kritis yang memungkinkan **copy pivot table** tanpa kehilangan fungsionalitasnya. Objek `CellArea` menentukan di mana rentang ditempatkan di sheet tujuan.

### Langkah 5: Simpan workbook tujuan

```java
// Save the destination workbook with the copied pivot table
destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
```

*Mengapa langkah ini?*  
Menyimpan menyelesaikan proses **export pivot table**. File yang dihasilkan (`DestWithPivot.xlsx`) berisi pivot yang beroperasi penuh yang dapat Anda buka di Excel, Google Sheets, atau penampil spreadsheet lainnya.

## Memverifikasi bahwa tabel pivot dipertahankan

Buka `DestWithPivot.xlsx` di Excel dan periksa hal berikut:

1. Tabel pivot muncul di lokasi yang sama (A1:G20) seperti di sumber.
2. Menyegarkan pivot memperbarui data dengan benar, membuktikan cache telah disalin.
3. Semua format (lebar kolom, format angka) cocok dengan yang asli.

Jika salah satu pemeriksaan ini gagal, pastikan bahwa rentang sumber sepenuhnya melingkupi pivot dan sumber datanya. Kesalahan umum adalah memilih rentang yang tidak mencakup cache data, yang menyebabkan pivot rusak.

## Pertimbangan tambahan

### Menyalin tabel pivot di antara versi workbook yang berbeda

Aspose.Cells mendukung file `.xls` lama serta format `.xlsx` yang lebih baru. Kode yang sama berfungsi terlepas dari ekstensi file, menjadikannya solusi universal untuk **how to preserve pivot** di berbagai versi.

### Mempertahankan tabel pivot saat menggunakan sumber yang difilter

Jika pivot sumber difilter, keadaan filter juga disalin. Jika Anda perlu mengatur ulang filter di tujuan, panggil `PivotTable.refreshData()` setelah menyalin:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.refreshData();   // Clears filters but keeps the pivot definition
```

### Mengekspor tabel pivot sebagai snapshot statis

Kadang-kadang Anda mungkin menginginkan salinan statis (hanya nilai) alih‑alih pivot aktif. Ganti `copyRange` dengan `copyRange` diikuti oleh `pt.setEnableRefresh(false)` untuk menonaktifkan perhitungan lebih lanjut.

```java
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
PivotTable pt = destWs.getPivotTables().get(0);
pt.setEnableRefresh(false); // Makes the pivot static
```

### Menangani workbook besar

Untuk workbook dengan banyak worksheet, batasi operasi penyalinan ke sheet tertentu untuk mengurangi penggunaan memori. Gunakan `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` untuk menyesuaikan kinerja.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin, tempel, dan jalankan. Sesuaikan jalur file agar cocok dengan lingkungan Anda.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the range covering the pivot table (including its data source)
        // Adjust the range as needed to fully contain your pivot
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a new, empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 4: Copy the defined range – the pivot table is preserved
        destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));

        // Optional: If you need a static snapshot, disable refresh
        // PivotTable pt = destWs.getPivotTables().get(0);
        // pt.setEnableRefresh(false);

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");

        System.out.println("Pivot table copied successfully. File saved as DestWithPivot.xlsx");
    }
}
```

**Expected output**

```
Pivot table copied successfully. File saved as DestWithPivot.xlsx
```

Saat Anda membuka `DestWithPivot.xlsx`, Anda akan melihat tabel pivot asli berfungsi penuh, mengonfirmasi bahwa Anda telah berhasil **how to copy range** sambil **preserve pivot table**.

## Kesalahan umum dan tips profesional

| Masalah | Mengapa terjadi | Solusi |
|-------|----------------|-----|
| Pivot muncul tetapi menampilkan error `#REF!` | Rentang yang disalin tidak menyertakan sheet cache tersembunyi | Perluas rentang sumber untuk mencakup seluruh cache (biasanya baris di bawah pivot) |
| Workbook tujuan lebih besar dari yang diharapkan | `copyRange` juga menyalin format | Gunakan `CopyOptions` untuk mengecualikan format jika ukuran menjadi masalah |
| Refresh gagal dengan “Data source not found” | Workbook sumber menggunakan koneksi data eksternal | Replikasikan koneksi di tujuan atau salin sheet sumber data terlebih dahulu |

**Tip pro:** Selalu jalankan pemeriksaan cepat `destWs.getPivotTables().size()` setelah menyalin. Jika jumlahnya nol, rentang tidak mencakup definisi pivot dan Anda perlu memperluasnya.

## Kesimpulan

Dalam tutorial ini kami menunjukkan **how to copy range** yang berisi tabel pivot dan menjamin bahwa perilaku **preserve pivot table** tetap utuh. Dengan memuat workbook sumber, menentukan rentang yang komprehensif, menggunakan `copyRange`, dan menyimpan file tujuan, Anda dapat secara andal **export pivot table** data dan menjawab pertanyaan **how to preserve pivot** dalam proyek Java.

Langkah selanjutnya yang dapat Anda jelajahi meliputi:

* Mengotomatiskan penyalinan untuk beberapa sheet (gunakan kata kunci sekunder **copy pivot table** dalam loop).
* Mengonversi workbook yang diekspor ke CSV sambil mempertahankan data mentah (masih menggunakan logika **preserve pivot table** untuk sumber).

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Export Pivot Table as an Image in C# – Step‑by‑Step Guide](/cells/english/net/pivot-tables/how-to-export-pivot-table-as-an-image-in-c-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}