---
category: general
date: 2026-10-26
description: Pelajari cara menyalin tabel pivot ke buku kerja baru menggunakan Java,
  sambil mempertahankan pemformatan dan definisi pivot saat menyalin rentang Excel
  dengan pemformatan melalui Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: id
lastmod: 2026-10-26
og_description: Salin tabel pivot ke buku kerja baru di Java dengan Aspose.Cells.
  Panduan ini menunjukkan cara menyalin rentang Excel, mempertahankan format, dan
  membuat buku kerja kosong secara efisien.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: Salin tabel pivot ke workbook baru di Java – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cara menyalin tabel pivot ke buku kerja baru dalam Java
url: /id/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin pivot table ke workbook baru di Java

Jika Anda perlu **menyalin pivot table** dari satu file Excel ke file lain, panduan ini menunjukkan solusi lengkap yang dapat dijalankan. Anda akan melihat cara mempertahankan definisi pivot, menjaga semua pemformatan, dan menghindari jebakan umum saat menyalin rentang Excel.

Menyalin pivot table sering menimbulkan pertanyaan seperti *bagaimana menyalin pivot* tanpa merusak sumber data atau kehilangan gaya. Pada akhir tutorial ini Anda akan memiliki program Java yang berdiri sendiri, yang membuat workbook kosong, menyalin rentang yang diinginkan, dan menyimpan hasilnya dengan pivot tetap utuh.

## Apa yang akan Anda capai

* Memuat workbook sumber yang berisi pivot table.  
* **Membuat workbook kosong** yang akan menerima data yang disalin.  
* **Menyalin rentang Excel** yang mencakup pivot, menggunakan opsi yang mempertahankan pivot dan pemformatan.  
* Menyimpan file tujuan dan memverifikasi bahwa pivot berfungsi persis seperti aslinya.

### Prasyarat

* Java 17 atau lebih baru.  
* Aspose.Cells untuk Java (versi 23.10 atau lebih baru).  
* Familiaritas dasar dengan IDE Java (IntelliJ IDEA, Eclipse, dll.).  

> **Pro tip:** Gunakan lisensi evaluasi gratis Aspose.Cells untuk pengujian cepat; ganti dengan lisensi penuh sebelum penggunaan produksi.

## Menyalin pivot table ke workbook baru

Langkah pertama adalah menyiapkan workbook sumber dan tujuan. Tujuan dimulai dengan pemanggilan **create empty workbook**, yang memberi Anda file bersih dengan satu lembar kerja.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### Mengapa ini berhasil

* `new Workbook()` **creates empty workbook** dengan lembar default, menghindari kebutuhan menghapus data yang ada.  
* `CopyOptions` memberi tahu Aspose.Cells untuk menyalin metadata **pivot table**, bukan hanya nilai mentah. Mode `PASTE_ALL` juga membawa gaya sel, format angka, dan pemformatan bersyarat—memenuhi persyaratan **copy range with formatting**.  
* `copyRange` melakukan operasi **copy excel range** yang menghormati struktur internal sumber, sehingga pivot tetap berfungsi setelah penyalinan.

## Cara menyalin pivot tanpa kehilangan pemformatan

Jika Anda hanya menggunakan `CopyOptions` default, beberapa informasi gaya mungkin terlewat pada versi Aspose.Cells yang lebih lama. Menetapkan tipe tempel secara eksplisit menjamin bahwa **copy range with formatting** dipatuhi.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

Menambahkan `setPasteSpecialType` memastikan lebar kolom, tinggi baris, dan bahkan aturan validasi data ikut bersama rentang. Ini sangat berguna ketika pivot table mencakup beberapa kolom dengan lebar khusus.

## Membuat workbook kosong sebelum menyalin

Kadang pengembang mencoba menyalin ke workbook yang sudah ada dan berisi data. Hal itu dapat menyebabkan tumpang tindih rentang atau penimpaan yang tidak terduga. Memulai dengan pemanggilan **create empty workbook** mengisolasi operasi:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

Jika Anda memerlukan lebih dari satu lembar di tujuan, Anda dapat menambahkannya setelah penyalinan:

```java
destWb.getWorksheets().add("Summary");
```

## Menyalin rentang Excel dengan pemformatan menggunakan CopyOptions

Selain pivot table, pola yang sama berlaku untuk **copy excel range** apa pun yang memerlukan pelestarian pemformatan—grafik, tabel, atau format bersyarat.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

Instansi `CopyOptions` tetap sama, sehingga Anda mendapatkan perilaku konsisten di berbagai rentang.

### Kasus tepi yang perlu dipertimbangkan

| Situasi                                 | Penanganan yang disarankan |
|-----------------------------------------|----------------------------|
| Workbook sumber memiliki beberapa pivot | Salin rentang masing‑masing pivot secara terpisah atau salin seluruh lembar. |
| Tujuan sudah berisi data                | Pilih sel mulai yang tidak berbenturan (misalnya, "H1") saat memanggil `copyRange`. |
| Sumber data pivot berada di luar (mis. DB) | Pastikan workbook tujuan mengacu pada sumber data eksternal yang sama, atau segarkan pivot setelah penyalinan. |
| Workbook besar ( > 10 MB )              | Tingkatkan ukuran heap Java (`-Xmx2g`) untuk menghindari `OutOfMemoryError`. |

## Memverifikasi hasil

Setelah menjalankan program, buka `destination.xlsx`. Anda harus melihat:

* Tata letak pivot table yang sama seperti di `source.xlsx`.  
* Semua warna sel, format angka, dan lebar kolom tetap terjaga.  
* Sumber data pivot masih mengacu pada rentang data asli di dalam file baru, sehingga menyegarkan pivot memperbarui nilai dengan benar.

Jika pivot muncul sebagai tabel statis, periksa kembali bahwa `CopyOptions.setPasteType(PasteType.PASTE_ALL)` telah diatur. Tanpa opsi ini Aspose.Cells memperlakukan pivot sebagai data biasa.

## Kesimpulan

Anda kini tahu cara **menyalin pivot table** ke workbook baru di Java sambil mempertahankan pemformatan, koneksi data, dan tata letak lembar. Solusi lengkap ini memperlihatkan cara memuat file sumber, **create empty workbook**, mengonfigurasi opsi **copy excel range**, dan menyimpan hasilnya.  

Selanjutnya Anda dapat menjelajahi topik terkait seperti **bagaimana menyalin pivot** antar lembar kerja, menyematkan grafik bersama pivot, atau mengotomatisasi pemrosesan batch banyak workbook. Bereksperimenlah dengan pengaturan `CopyOptions` untuk menyesuaikan kebutuhan otomatisasi Anda, dan Anda akan memiliki toolkit manipulasi Excel yang kuat di ujung jari.

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang sangat terkait dan membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Create New Workbook in Java – Full Guide to Copy Pivot Table](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}