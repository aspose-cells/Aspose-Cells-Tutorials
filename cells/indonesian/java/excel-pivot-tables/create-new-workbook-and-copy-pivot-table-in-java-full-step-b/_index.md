---
category: general
date: 2026-07-16
description: Buat workbook baru dan salin tabel pivot menggunakan Aspose.Cells untuk
  Java. Pelajari cara menduplikasi tabel pivot dan menyalin rentang Excel dalam hitungan
  menit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- duplicate pivot table
- how to copy pivot
- copy excel range
language: id
lastmod: 2026-07-16
og_description: Buat workbook baru dan salin tabel pivot dengan Aspose.Cells untuk
  Java. Panduan ini menunjukkan cara menduplikasi tabel pivot dan menyalin rentang
  Excel secara efisien.
og_image_alt: Screenshot of Java code that creates a new workbook and copies a pivot
  table using Aspose.Cells
og_title: Buat Workbook Baru & Salin Tabel Pivot di Java – Tutorial Lengkap
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  headline: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  name: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  steps:
  - name: What if the source pivot spans more than one sheet?
    text: Aspose.Cells can only copy ranges within a single worksheet at a time. If
      your pivot stretches across sheets, you’ll need to copy each relevant range
      separately and then re‑link them manually.
  - name: Does this method preserve custom number formats?
    text: Yes. The `copy` method copies cell styles, including number formats, fonts,
      and colors. However, if you have conditional formatting that references external
      ranges, double‑check those references after the copy.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot pulls data from an external connection (e.g., a SQL query),
      the connection information is **not** transferred by `copy`. You’ll need to
      recreate the data source in the destination workbook or embed the source data
      beforehand.
  - name: Can I copy only the pivot layout without the underlying data?
    text: You can achieve that by first clearing the data cells in the source range,
      then copying only the pivot’s layout. This is a more advanced scenario and usually
      not required for a simple **duplicate pivot table** task.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Buat Workbook Baru dan Salin Pivot Table di Java – Panduan Lengkap Langkah
  demi Langkah
url: /id/java/excel-pivot-tables/create-new-workbook-and-copy-pivot-table-in-java-full-step-b/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Workbook Baru dan Salin Tabel Pivot di Java – Panduan Langkah‑per‑Langkah Lengkap

Pernah bertanya-tanya bagaimana cara **create new workbook** sambil mempertahankan tabel pivot yang kompleks dari file yang ada? Jika Anda pernah menatap lembar Excel, berpikir “Saya butuh pivot ini di workbook lain,” dan menggaruk kepala, Anda tidak sendirian. Kabar baiknya, dengan Aspose.Cells for Java Anda dapat menduplikasi tabel pivot hanya dengan beberapa baris kode.

Dalam tutorial ini kami akan menjelaskan langkah‑langkah tepat untuk menyalin data **copy pivot table**, menyalin struktur **duplicate pivot table**, dan menyalin isi **copy Excel range**—semua sambil membuat workbook baru dari awal. Pada akhir tutorial Anda akan memiliki program Java siap‑jalankan yang melakukan persis apa yang Anda minta.

## Apa yang Akan Anda Pelajari

- Cara **create new workbook** secara programatis dengan Aspose.Cells.
- Cara tepat untuk menentukan rentang yang berisi tabel pivot.
- Teknik untuk **copy pivot table** dan **duplicate pivot table** tanpa kehilangan format atau koneksi data.
- Cara **copy Excel range** secara efisien dan menyimpan hasilnya.
- Jebakan umum dan tip untuk menangani tabel pivot yang lebih besar.

Tidak diperlukan referensi eksternal—semua bersifat mandiri, dapat dijalankan, dan dijelaskan.

## Prasyarat

1. **Java Development Kit (JDK) 11+** – versi terbaru apa pun dapat digunakan.  
2. **Aspose.Cells for Java** library (versi terbaru per 2026‑07‑16). Anda dapat mengunduhnya dari Maven Central:

   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-cells</artifactId>
       <version>23.12</version>
   </dependency>
   ```

3. File Excel sumber (`SourceWithPivot.xlsx`) yang sudah berisi tabel pivot yang ingin Anda salin.  
4. IDE atau editor teks sederhana—IntelliJ IDEA, Eclipse, atau VS Code dapat digunakan.

Sudah siap? Bagus—mari kita mulai.

## Langkah 1: **Create New Workbook** dan Muat File Sumber

Hal pertama yang kita butuhkan adalah objek workbook baru yang nantinya akan menampung pivot yang diduplikasi. Pada saat yang sama kita harus memuat workbook asli agar dapat merujuk ke rentang tabel pivotnya.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that already contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Grab the first worksheet where the pivot lives
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

> **Mengapa ini penting:**  
> Memuat workbook sumber memberi kita akses ke objek `Range` yang mendasari yang mencakup pivot. Jika Anda melewatkan langkah ini, tidak akan ada yang dapat disalin, dan operasi **duplicate pivot table** akan gagal secara diam‑diam.

## Langkah 2: Tentukan **Copy Excel Range** yang Menampung Pivot

Tabel pivot bukan satu sel—ia mencakup blok persegi panjang. Kita perlu memberi tahu Aspose.Cells sel mana yang harus disalin.

```java
        // Define the cell range that includes the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

> **Tip:**  
> Jika Anda tidak yakin dengan rentang yang tepat, buka workbook sumber di Excel, pilih pivot, dan lihat kotak nama. Itu akan menampilkan sesuatu seperti `A1:G20`. Menggunakan rentang yang tepat memastikan semua pengaturan bidang, filter, dan perhitungan dipertahankan ketika kita **copy pivot table** nanti.

## Langkah 3: **Create New Workbook** yang Akan Menerima Pivot yang Disalin

Sekarang kita membuat workbook baru—di sinilah **duplicate pivot table** kita akan berada.

```java
        // Create a completely empty workbook for the destination
        Workbook dstWb = new Workbook(); // this automatically creates one empty worksheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);
```

> **Apa yang terjadi di balik layar?**  
> Konstruktor default membuat workbook dengan satu lembar kosong. Ini adalah kanvas bersih yang kita butuhkan untuk skenario **create new workbook**. Tidak ada gaya yang tersisa atau lembar tersembunyi yang perlu dikhawatirkan.

## Langkah 4: **Copy Pivot Table** – Sebenarnya Menyalin Rentang Excel yang Didefinisikan

Dengan sumber dan tujuan siap, kita melakukan operasi penyalinan. Langkah ini menyelesaikan bagian **how to copy pivot** dari teka‑teki.

```java
        // Copy the defined range (which includes the pivot) to the destination worksheet
        srcRange.copy(dstWs.getCells().createRange("A1"));
```

> **Mengapa `copy` bekerja untuk pivot:**  
> Aspose.Cells memperlakukan pivot sebagai bagian dari koleksi sel. Saat Anda menyalin rentang, ia membawa cache pivot, daftar bidang, dan tata letak. Hasilnya adalah **duplicate pivot table** yang sepenuhnya berfungsi di workbook baru.

## Langkah 5: Simpan Hasil dan Verifikasi Operasi **Copy Pivot Table**

Akhirnya, simpan workbook tujuan ke disk. Buka file di Excel untuk memastikan pivot muncul persis seperti di sumber.

```java
        // Save the destination workbook with the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

**Hasil yang diharapkan:**  
- `CopyPivotResult.xlsx` terbuka dengan lembar kerja yang berisi tabel pivot yang sama seperti yang Anda lihat di `SourceWithPivot.xlsx`.  
- Semua label baris/kolom, filter, dan bidang terhitung tetap utuh.  
- Anda kini dapat mengedit data sumber secara terpisah, dan workbook baru akan mempertahankan cache pivotnya sendiri.

## Kasus Pojok & Pertanyaan Umum

### Bagaimana jika pivot sumber melintasi lebih dari satu lembar?
Aspose.Cells hanya dapat menyalin rentang dalam satu lembar kerja pada satu waktu. Jika pivot Anda melintasi beberapa lembar, Anda harus menyalin setiap rentang yang relevan secara terpisah dan kemudian menautkannya kembali secara manual.

### Apakah metode ini mempertahankan format angka khusus?
Ya. Metode `copy` menyalin gaya sel, termasuk format angka, font, dan warna. Namun, jika Anda memiliki pemformatan bersyarat yang merujuk ke rentang eksternal, periksa kembali referensi tersebut setelah penyalinan.

### Bagaimana menyalin pivot yang menggunakan sumber data eksternal?
Ketika pivot mengambil data dari koneksi eksternal (mis., kueri SQL), informasi koneksi **tidak** dipindahkan oleh `copy`. Anda perlu membuat ulang sumber data di workbook tujuan atau menyematkan data sumber sebelumnya.

### Bisakah saya menyalin hanya tata letak pivot tanpa data dasarnya?
Anda dapat melakukannya dengan terlebih dahulu mengosongkan sel data di rentang sumber, lalu menyalin hanya tata letak pivot. Ini adalah skenario yang lebih maju dan biasanya tidak diperlukan untuk tugas **duplicate pivot table** sederhana.

## Contoh Kerja Lengkap (Semua Langkah Digabungkan)

Berikut adalah kelas Java lengkap yang siap dijalankan. Cukup ganti `YOUR_DIRECTORY` dengan jalur folder yang sebenarnya di mesin Anda.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the exact range that holds the pivot table
        // Adjust "A1:G20" to match your pivot's size
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a brand‑new workbook that will receive the copy
        Workbook dstWb = new Workbook(); // creates an empty workbook with one sheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);

        // Step 4: Copy the pivot (and any surrounding data) to the new workbook
        srcRange.copy(dstWs.getCells().createRange("A1"));

        // Step 5: Save the destination file – now it contains the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully! Check CopyPivotResult.xlsx.");
    }
}
```

Jalankan program (`java CopyPivotTableDemo`) dan Anda akan melihat pesan konsol yang mengonfirmasi keberhasilan.

## Tips Pro & Praktik Terbaik

- **Validate the range** sebelum menyalin. Gunakan `srcWs.getCells().maxDisplayRange` untuk menemukan area yang digunakan secara programatik jika Anda tidak ingin menuliskan secara keras `"A1:G20"`.
- **Turn off calculation** sementara untuk workbook besar agar mempercepat penyalinan:

  ```java
  srcWb.getSettings().setCalculateFormulaOnOpen(false);
  ```

- **Dispose of resources** (`srcWb.dispose(); dstWb.dispose();`) dalam layanan yang berjalan lama untuk menghindari kebocoran memori.
- **Version compatibility:** Kode ini bekerja dengan Aspose.Cells 23.12 dan yang lebih baru. Versi lama mungkin memerlukan `srcRange.copyTo` alih-alih `copy`.

## Langkah Selanjutnya

Sekarang Anda telah menguasai **create new workbook** dan **copy pivot table**, Anda mungkin ingin menjelajahi:

- **How to copy pivot** lintas beberapa lembar kerja dalam pekerjaan batch.  
- Menambahkan **copy excel range** untuk tabel data reguler bersama pivot.  
- Mengotomatiskan pembuatan **duplicate pivot table** untuk laporan tiap bulan menggunakan loop.  
- Mengekspor pivot yang diduplikasi ke PDF atau HTML dengan renderer bawaan Aspose.Cells.

Setiap topik ini dibangun di atas fondasi yang telah dibahas, dan semuanya mendapat manfaat dari pendekatan yang bersih dan programatis yang sama.

## Kesimpulan

Kami telah membahas seluruh proses **create new workbook**, mendefinisikan **copy excel range** sumber, dan **copy pivot table** untuk menghasilkan **duplicate pivot table** di Java menggunakan Aspose.Cells. Solusinya singkat, sepenuhnya berfungsi, dan siap untuk penggunaan produksi. Silakan sesuaikan rentang, bereksperimen dengan file sumber yang berbeda, atau menyematkan logika ini ke dalam pipeline pelaporan yang lebih besar.

Jika Anda mengalami kendala atau memiliki ide untuk memperluas tutorial ini, tinggalkan komentar di bawah. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Membuat Tabel Pivot di Excel Menggunakan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Cara Memperbarui Sumber Tabel Pivot Excel dengan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Manipulasi Tabel Pivot Excel dengan Aspose.Cells Java: Panduan Komprehensif](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}