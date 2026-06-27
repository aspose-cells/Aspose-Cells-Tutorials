---
category: general
date: 2026-06-27
description: Salin tabel pivot Excel dengan Java dalam hitungan menit – pelajari cara
  menyalin rentang ke buku kerja lain dan temukan cara menyalin tabel pivot secara
  efisien.
draft: false
keywords:
- copy pivot table excel
- copy range to another workbook
- how to copy pivot table
language: id
og_description: Menyalin tabel pivot Excel menggunakan Java. Panduan ini menunjukkan
  cara menyalin rentang ke buku kerja lain dan menjawab cara menyalin tabel pivot
  dengan contoh lengkap.
og_title: Salin Tabel Pivot Excel – Tutorial Java
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table excel with Java in minutes – learn how to copy range
    to another workbook and discover how to copy pivot table efficiently.
  headline: Copy Pivot Table Excel – Step‑by‑Step Guide Using Java
  type: TechArticle
- description: Copy pivot table excel with Java in minutes – learn how to copy range
    to another workbook and discover how to copy pivot table efficiently.
  name: Copy Pivot Table Excel – Step‑by‑Step Guide Using Java
  steps:
  - name: Expected Result
    text: '- Opening `destination.xlsx` shows a sheet named **CopiedPivot**. - The
      sheet contains a pivot table that can be refreshed, filtered, and rearranged
      just like the original. - No error messages appear in the console, confirming
      that **copy pivot table excel** succeeded.'
  - name: What if the source workbook has multiple pivot tables?
    text: 'You can repeat the range‑selection logic for each pivot table, or you can
      copy the entire worksheet:'
  - name: How to handle external data connections?
    text: 'If your pivot table pulls data from an external database, the destination
      workbook will retain the connection string. To avoid broken links, update the
      connection after copying:'
  - name: Does this work with .xls files?
    text: Yes. Aspose.Cells abstracts the file format, so the same code works for
      `.xls`, `.xlsx`, `.xlsb`, and even `.ods`. Just change the file extension in
      the `Workbook` constructors.
  type: HowTo
tags:
- pivot-table
- excel
- java
- aspose-cells
title: Menyalin Tabel Pivot Excel – Panduan Langkah-demi-Langkah Menggunakan Java
url: /id/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salin Tabel Pivot Excel – Tutorial Java

Pernah bertanya-tanya bagaimana cara **copy pivot table excel** file tanpa kehilangan koneksi data yang mendasarinya? Anda tidak sendirian. Banyak pengembang mengalami kebuntuan ketika mencoba memindahkan tabel pivot dari satu workbook ke workbook lain, hanya untuk berakhir dengan rentang statis atau referensi yang rusak.  

Berita baiknya? Dengan beberapa baris kode Java dan pustaka yang tepat, Anda dapat **copy pivot table excel** workbook secara bersih, mempertahankan setiap bidang, filter, dan tata letak. Dalam panduan ini kami juga akan menunjukkan **how to copy pivot table** menggunakan API Aspose.Cells untuk Java, dan kami akan menambahkan tips tentang **copy range to another workbook** untuk skenario kasus pinggir.

> **Apa yang akan Anda dapatkan:** program yang dapat dijalankan sepenuhnya yang memuat workbook sumber, menyalin rentang yang berisi tabel pivot, dan menyimpan workbook baru yang tampak persis seperti aslinya.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- Java 17 atau lebih baru (kode ini dapat dikompilasi dengan JDK terbaru apa pun).
- Aspose.Cells for Java 23.10 atau yang lebih baru – versi percobaan gratis sudah cukup untuk pengujian.
- File Excel sumber (`source.xlsx`) yang sudah berisi tabel pivot pada lembar kerja pertama.
- IDE atau setup build baris perintah sederhana (Maven/Gradle).

Tidak ada dependensi eksternal lain yang diperlukan.

## Langkah 1: Siapkan Proyek dan Impor Kelas

Pertama, buat proyek Maven (atau Gradle, jika Anda lebih suka) dan tambahkan dependensi Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

Sekarang impor kelas‑kelas yang akan kita gunakan:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Tips pro:** Jaga folder `src/main/resources` Anda tetap rapi; letakkan `source.xlsx` di sana dan referensikan dengan path relatif untuk menghindari hard‑coding direktori absolut.

## Langkah 2: Muat Workbook Sumber yang Berisi Tabel Pivot

Baris pertama dari setiap operasi **copy pivot table excel** adalah memuat workbook yang berisi tabel pivot yang ingin Anda duplikasi.

```java
// Step 2: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("src/main/resources/source.xlsx");
```

Mengapa kita memuat seluruh workbook alih‑alih hanya lembarnya? Karena cache pivot berada pada level workbook; menyalin hanya lembar akan memutus cache dan tabel pivot Anda akan berubah menjadi rentang biasa.

## Langkah 3: Ambil Worksheet dan Tentukan Rentang Tabel Pivot

Selanjutnya, kita temukan worksheet dan blok sel tepat yang melingkupi tabel pivot. Pada kebanyakan kasus tabel pivot dimulai di `A1`, tetapi Anda harus menyesuaikan rentang agar cocok dengan file Anda.

```java
// Step 3: Access the worksheet where the pivot table resides
Worksheet srcWs = srcWb.getWorksheets().get(0);

// Define the range that includes the pivot table (e.g., A1:E20)
Range srcRange = srcWs.getCells().createRange("A1:E20");
```

Jika Anda tidak yakin tentang rentang tersebut, Anda dapat membiarkan Aspose.Cells menghitung sel‑sel yang terpakai:

```java
int maxRow = srcWs.getCells().getMaxDataRow();
int maxCol = srcWs.getCells().getMaxDataColumn();
String autoRange = String.format("A1:%s%d",
        CellsHelper.columnIndexToName(maxCol), maxRow + 1);
Range srcRange = srcWs.getCells().createRange(autoRange);
```

Potongan kode kecil ini berguna ketika Anda perlu **copy range to another workbook** tanpa harus menuliskan alamat secara manual.

## Langkah 4: Buat Workbook Tujuan

Sekarang kita buat workbook baru yang akan menerima tabel pivot yang disalin. Inilah inti dari **how to copy pivot table**—Anda membuat kanvas bersih lalu menempelkan rentang.

```java
// Step 4: Create a new destination workbook (or load an existing one)
Workbook dstWb = new Workbook(); // empty workbook by default
```

Jika Anda sudah memiliki file templat yang ingin diperkaya, cukup ganti konstruktor dengan `new Workbook("template.xlsx")`.

## Langkah 5: Tambahkan Worksheet ke Workbook Tujuan

Meskipun `Workbook` baru sudah berisi satu sheet default, kami akan menambahkan sheet kedua untuk mendemonstrasikan proses menyalin ke lokasi tertentu.

```java
// Step 5: Add a new worksheet to the destination workbook
Worksheet dstWs = dstWb.getWorksheets().add();
```

Anda dapat mengganti nama sheet untuk kejelasan:

```java
dstWs.setName("CopiedPivot");
```

## Langkah 6: Salin Rentang – Tabel Pivot Dipertahankan

Berikut baris ajaib yang sebenarnya **copy range to another workbook** sambil menjaga tabel pivot tetap utuh. Objek `CopyOptions` memberi tahu Aspose.Cells untuk mempertahankan semuanya, termasuk cache pivot.

```java
// Step 6: Copy the range—pivot table is preserved—to the new worksheet at A1
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);
dstWs.getCells().copyRange(srcRange, "A1", copyOptions);
```

Mengapa kami menetapkan `PasteType.PASTE_ALL`? Karena operasi paste default hanya menyalin nilai dan format, mengabaikan cache pivot. Dengan secara eksplisit meminta `PASTE_ALL`, kami memastikan workbook tujuan menerima tabel pivot yang berfungsi penuh.

## Langkah 7: Simpan Workbook Tujuan

Akhirnya, tulis file baru ke disk. Setelah langkah ini Anda dapat membuka `destination.xlsx` di Excel dan melihat tabel pivot persis seperti yang ada di file sumber.

```java
// Step 7: Save the destination workbook with the copied pivot table
dstWb.save("src/main/resources/destination.xlsx");
```

### Hasil yang Diharapkan

- Membuka `destination.xlsx` menampilkan sheet bernama **CopiedPivot**.
- Sheet tersebut berisi tabel pivot yang dapat disegarkan, difilter, dan diatur ulang persis seperti aslinya.
- Tidak ada pesan error yang muncul di konsol, mengonfirmasi bahwa **copy pivot table excel** berhasil.

## Pertanyaan Umum & Kasus Tepi

### Bagaimana jika workbook sumber memiliki beberapa tabel pivot?

Anda dapat mengulangi logika pemilihan rentang untuk setiap tabel pivot, atau Anda dapat menyalin seluruh worksheet:

```java
srcWs.getCells().copy(dstWs.getCells());
```

Menyalin seluruh sheet juga memindahkan semua cache pivot, menjadikannya cara cepat untuk **copy range to another workbook** ketika Anda memiliki banyak tabel.

### Bagaimana menangani koneksi data eksternal?

Jika tabel pivot Anda menarik data dari basis data eksternal, workbook tujuan akan mempertahankan string koneksi. Untuk menghindari tautan yang rusak, perbarui koneksi setelah menyalin:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
pt.getPivotCache().setExternalDataSource("newConnectionString");
```

### Apakah ini bekerja dengan file .xls?

Ya. Aspose.Cells mengabstraksi format file, sehingga kode yang sama bekerja untuk `.xls`, `.xlsx`, `.xlsb`, dan bahkan `.ods`. Cukup ubah ekstensi file pada konstruktor `Workbook`.

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut kelas Java siap‑jalankan yang mendemonstrasikan **how to copy pivot table** dari satu workbook ke workbook lain:

```java
import com.aspose.cells.*;

public class CopyPivotTableExcel {
    public static void main(String[] args) throws Exception {
        // Load source workbook containing the pivot table
        Workbook srcWb = new Workbook("src/main/resources/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Determine the used range automatically (covers the pivot table)
        int maxRow = srcWs.getCells().getMaxDataRow();
        int maxCol = srcWs.getCells().getMaxDataColumn();
        String rangeAddress = String.format("A1:%s%d",
                CellsHelper.columnIndexToName(maxCol), maxRow + 1);
        Range srcRange = srcWs.getCells().createRange(rangeAddress);

        // Create destination workbook and add a sheet
        Workbook dstWb = new Workbook();
        Worksheet dstWs = dstWb.getWorksheets().add();
        dstWs.setName("CopiedPivot");

        // Copy the range with all pivot information preserved
        CopyOptions opts = new CopyOptions();
        opts.setPasteType(PasteType.PASTE_ALL);
        dstWs.getCells().copyRange(srcRange, "A1", opts);

        // Save the result
        dstWb.save("src/main/resources/destination.xlsx");
        System.out.println("Pivot table copied successfully!");
    }
}
```

Jalankan kelas tersebut, buka `destination.xlsx`, dan Anda akan melihat replika persis dari tabel pivot asli. 🎉

## Kesimpulan

Kami baru saja menelusuri alur kerja lengkap **copy pivot table excel** menggunakan Java. Dengan memuat workbook sumber, menentukan rentang tabel pivot, dan menggunakan `CopyOptions` dengan `PASTE_ALL`, Anda dapat dengan andal **copy range to another workbook** sambil mempertahankan setiap fitur pivot.  

Jika Anda penasaran tentang **how to copy pivot table** dalam bahasa lain, konsep yang sama berlaku—cukup ganti SDK Aspose.Cells dengan platform yang sesuai. Selanjutnya, Anda dapat menjelajahi cara memperbarui tabel pivot yang disalin secara programatis, atau mengekspornya ke PDF untuk keperluan pelaporan.  

Punya variasi pada skenario ini? Mungkin Anda perlu menyalin grafik yang terhubung ke tabel pivot, atau ingin memproses ratusan file secara batch. Topik‑topik tersebut adalah perpanjangan alami dari apa yang kami bahas hari ini.  

Cobalah kode tersebut, sesuaikan rentangnya, dan biarkan petualangan otomatisasi Excel Anda dimulai. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Memperbarui Sumber Tabel Pivot Excel dengan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Otomatisasi Penataan dan Penyimpanan Tabel Pivot Excel dengan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)
- [Manipulasi Tabel Pivot Excel dengan Aspose.Cells Java: Panduan Komprehensif](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}