---
category: general
date: 2026-08-04
description: Salin tabel pivot dengan Aspose.Cells untuk Java. Pelajari cara menyalin
  rentang Excel, menggandakan tabel pivot, dan menyalin lembar kerja dengan pivot
  hanya dalam beberapa baris.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy excel range
- copy range java
- duplicate pivot table
- copy worksheet with pivot
language: id
lastmod: 2026-08-04
og_description: Salin tabel pivot menggunakan Aspose.Cells untuk Java. Tutorial ini
  memandu Anda melalui penyalinan rentang Excel, menduplikasi tabel pivot, dan mempertahankan
  semua data di lembar kerja baru.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new worksheet
og_title: Menyalin tabel pivot di Java – tutorial lengkap Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  headline: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  type: TechArticle
- description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  name: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  steps:
  - name: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
    text: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
  - name: Opening the file in Excel shows a new sheet named **CopySheet**.
    text: Opening the file in Excel shows a new sheet named **CopySheet**.
  - name: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
    text: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
  - name: All formatting, filters, and calculated fields are preserved.
    text: All formatting, filters, and calculated fields are preserved.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PivotTable
- Data copying
title: Menyalin tabel pivot di Java – panduan langkah demi langkah menggunakan Aspose.Cells
url: /id/java/excel-pivot-tables/copy-pivot-table-in-java-step-by-step-guide-using-aspose-cel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menyalin tabel pivot di Java – panduan langkah demi langkah menggunakan Aspose.Cells

Jika Anda perlu **menyalin tabel pivot** dari satu lembar kerja ke lembar kerja lain di Java, panduan ini menunjukkan secara tepat cara melakukannya dengan Aspose.Cells. Baik Anda menghasilkan laporan secara programatis atau membangun alat migrasi data, Anda akan melihat contoh lengkap yang dapat dijalankan yang mempertahankan definisi dan data tabel pivot.

Menyalin tabel pivot lebih dari sekadar menyalin rentang sel; cache dan sumber data yang mendasarinya harus tetap utuh. Dalam tutorial ini kami juga membahas cara **menyalin rentang excel**, cara **menduplikasi tabel pivot** di seluruh lembar kerja, dan cara **menyalin lembar kerja dengan pivot** menggunakan API yang sama.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* Java Development Kit (JDK) 8 atau yang lebih baru.
* Maven atau Gradle untuk mengelola dependensi.
* Aspose.Cells for Java (versi terbaru, misalnya 23.12). Tambahkan koordinat Maven berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* Sebuah workbook sumber (`Source.xlsx`) yang berisi tabel pivot pada lembar kerja pertama.

## Cara menyalin tabel pivot di Java dengan Aspose.Cells

Ide utama adalah menyalin *rentang sumber* yang melingkupi tabel pivot dan kemudian menempelkannya ke lembar kerja baru. Aspose.Cells secara otomatis menyalin cache pivot, sehingga lembar yang dihasilkan berisi **tabel pivot duplikat** yang berfungsi penuh.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the PivotTable
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

        // Step 2: Define the source range (including the PivotTable) to be copied
        // The range must cover the entire pivot table area, e.g., A1:G20
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)                 // first worksheet
                                    .getCells()
                                    .createRange("A1:G20");

        // Step 3: Add a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("CopySheet");

        // Step 4: Copy the source range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Step 5: Save the workbook with the copied PivotTable intact
        workbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### Mengapa ini berhasil

* **Range copy includes the pivot cache** – Aspose.Cells memperlakukan tabel pivot sebagai objek khusus yang tertanam dalam rentang sel. Ketika Anda memanggil `Range.copy`, perpustakaan menyalin baik sel yang terlihat maupun cache tersembunyi yang menggerakkan pivot.
* **No manual recreation needed** – Anda tidak perlu membangun kembali bidang pivot atau sumber data; duplikat siap disegarkan secara instan.
* **Works with any Excel version** – File yang dihasilkan mengikuti standar Office Open XML (XLSX), sehingga Excel 2007+ dapat membukanya tanpa peringatan.

## Menyalin rentang excel – menggunakan kembali kode yang sama untuk data non‑pivot

Jika Anda hanya perlu **menyalin rentang excel** tanpa tabel pivot, pola yang sama berlaku. Cukup sesuaikan alamat rentang ke wilayah yang ingin Anda duplikat.

```java
// Example: copy A1:D10 from Sheet1 to Sheet2
Range dataRange = workbook.getWorksheets()
                          .get(0)
                          .getCells()
                          .createRange("A1:D10");
Worksheet sheet2 = workbook.getWorksheets().add("DataCopy");
dataRange.copy(sheet2.getCells().createRange("A1"));
```

Metode `copy` mempertahankan formula, pemformatan, dan komentar, menjadikannya solusi universal untuk blok data Excel apa pun.

## Duplikasi tabel pivot di beberapa lembar kerja

Kadang‑kadang Anda perlu **menduplikasi tabel pivot** beberapa kali—misalnya, satu per departemen. Lakukan perulangan pada lembar kerja tujuan dan gunakan kembali pemanggilan `sourceRange.copy` yang sama:

```java
String[] departments = {"Sales", "Marketing", "Finance"};
for (String dept : departments) {
    Worksheet ws = workbook.getWorksheets().add(dept + "Pivot");
    sourceRange.copy(ws.getCells().createRange("A1"));
}
```

Setiap lembar baru berisi pivot independen yang dapat disegarkan secara terpisah. Cache diduplikasi, sehingga perubahan pada satu lembar tidak memengaruhi yang lain.

## Menyalin lembar kerja dengan pivot – mempertahankan pengaturan tingkat lembar

Jika Anda ingin **menyalin lembar kerja dengan pivot** sekaligus mempertahankan pengaturan halaman, lebar kolom, dan named range, gunakan `Worksheet.copy` alih‑alih menyalin rentang secara manual. Metode ini menggandakan seluruh lembar, termasuk tabel pivot.

```java
Worksheet original = workbook.getWorksheets().get(0);
Worksheet clone = workbook.getWorksheets().addCopy(original);
clone.setName("FullCopy");
workbook.save("YOUR_DIRECTORY/FullCopy.xlsx");
```

`addCopy` sangat berguna ketika lembar kerja berisi diagram, gambar, atau gaya khusus yang harus dibawa bersama pivot.

## Kesalahan umum dan cara menghindarinya

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Pivot cache lost after copy** | Menggunakan `Cell.copy` pada sel individual (bukan pada rentang) mengabaikan cache tersembunyi. | Selalu salin *seluruh* rentang yang melingkupi tabel pivot, seperti yang ditunjukkan pada Langkah 2. |
| **Source range too small** | Rentang tidak mencakup area data pivot, sehingga lembar baru hanya menampilkan nilai statis. | Perluas alamat (mis., `A1:G20`) untuk mencakup seluruh tabel pivot plus slicer atau filter apa pun. |
| **Destination workbook version mismatch** | Menyimpan sebagai XLS (legacy) menghilangkan fitur pivot modern. | Simpan sebagai XLSX (default) atau secara eksplisit atur `SaveFormat.XLSX`. |
| **External data source broken** | Pivot mengacu pada sumber data di luar workbook; penyalinan tidak menyematkannya. | Gunakan `PivotTable.refreshData()` setelah menyalin, atau sematkan data sumber dalam workbook yang sama. |

## Output yang Diharapkan

Setelah menjalankan program:

1. `CopyWithPivot.xlsx` muncul di `YOUR_DIRECTORY`.
2. Membuka file di Excel menampilkan lembar baru bernama **CopySheet**.
3. **CopySheet** berisi tabel pivot yang berfungsi penuh dan identik dengan yang asli, siap disegarkan.
4. Semua pemformatan, filter, dan bidang terhitung dipertahankan.

Jika Anda membuka `FullCopy.xlsx`, Anda akan melihat replika lengkap dari lembar kerja asli, termasuk diagram atau gambar apa pun yang ada di lembar sumber.

## Ringkasan

* Anda telah belajar cara **menyalin tabel pivot** di Java menggunakan Aspose.Cells.
* Pendekatan yang sama berlaku untuk skenario **menyalin rentang excel** atau **copy range java** biasa.
* Untuk operasi massal, Anda dapat **menduplikasi tabel pivot** di banyak lembar.
* Ketika Anda memerlukan seluruh lembar, **menyalin lembar kerja dengan pivot** menggunakan `addCopy`.

## Langkah Selanjutnya

* Jelajahi **PivotTable.refreshData()** untuk memperbarui cache secara programatis setelah penyalinan.
* Gabungkan logika penyalinan dengan **Excel file streaming** untuk menangani workbook besar tanpa memuat semuanya ke memori.
* Lihat dukungan Aspose.Cells untuk **pivot slicers** jika laporan Anda mengandalkan filter interaktif.

Silakan sesuaikan kode dengan struktur proyek Anda sendiri, bereksperimen dengan ukuran rentang yang berbeda, atau integrasikan ke dalam pipeline pemrosesan data yang lebih besar. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulation Aspose Cells Java](/cells/hongkong/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}