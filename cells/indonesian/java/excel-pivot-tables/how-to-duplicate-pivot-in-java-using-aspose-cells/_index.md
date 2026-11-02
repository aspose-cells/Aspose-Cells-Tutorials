---
category: general
date: 2026-09-18
description: cara menduplikasi pivot di Java dengan Aspose.Cells – menyalin tabel
  pivot antar workbook dengan cepat dan andal
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: id
lastmod: 2026-09-18
og_description: cara menduplikasi pivot di Java menggunakan Aspose.Cells. Ikuti tutorial
  lengkap ini untuk menyalin tabel pivot antar workbook dengan kode Java yang bersih.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: Duplikat tabel pivot di Java – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cara menduplikasi pivot di Java menggunakan Aspose.Cells
url: /id/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menggandakan pivot di Java menggunakan Aspose.Cells

Jika Anda perlu **how to duplicate pivot** dalam aplikasi Java, panduan ini menunjukkan langkah‑langkah tepatnya. Dengan memuat workbook Excel, mendefinisikan area sel pivot, dan menyalin rentang tersebut ke workbook baru, Anda dapat memindahkan tabel pivot tanpa kehilangan definisi atau datanya.

Menyalin tabel pivot adalah kebutuhan umum saat Anda menghasilkan laporan, mengarsipkan analisis, atau memecah workbook besar menjadi bagian‑bagian modular. Dalam tutorial ini Anda akan belajar cara **copy range between workbooks**, cara **load Excel workbook Java**, dan nuansa **how to copy pivot** dengan aman.

Anda akan selesai dengan program Java siap‑jalankan yang menggandakan tabel pivot dari `Source.xlsx` ke `PivotCopied.xlsx` menggunakan Aspose.Cells for Java.

## Prasyarat

* JDK 8 atau yang lebih baru terpasang.
* Maven (atau alat build lain) untuk mengelola dependensi.
* Aspose.Cells for Java versi 23.10 atau lebih baru. Tambahkan dependensi Maven berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* Sebuah workbook sumber (`Source.xlsx`) yang berisi tabel pivot dalam rentang **A1:H30**.

## Cara menggandakan pivot di Java

Ide dasarnya sederhana:

1. **Load the source workbook** – ini memberi Anda akses ke worksheet yang menyimpan pivot.
2. **Define the cell area** yang melingkupi pivot.
3. **Create a destination workbook** – file kosong yang akan menerima rentang yang disalin.
4. **Copy the range** – Aspose.Cells secara otomatis menggandakan definisi pivot.
5. **Save the destination workbook** – kini Anda memiliki file terpisah dengan pivot yang sama.

Berikut adalah program Java lengkap yang dapat dijalankan yang mengikuti langkah‑langkah tersebut.

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### Mengapa ini berhasil

* **Aspose.Cells** memperlakukan tabel pivot sebagai bagian dari koleksi sel worksheet. Saat Anda memanggil `copyRange`, perpustakaan menyalin tidak hanya nilai sel tetapi juga cache pivot dan definisinya, sehingga workbook baru berisi duplikat yang berfungsi penuh.
* Objek `CopyOptions` secara default mempertahankan formula, format, dan objek tersemat. Anda dapat menyesuaikannya (mis., `setCopyColumnWidths(true)`) jika memerlukan kontrol tambahan.

## Menyalin rentang antar workbook – tinjauan mendalam

Meskipun contoh di atas menyalin satu blok berkelanjutan, `copyRange` dapat menangani area persegi panjang apa pun. Jika pivot Anda mencakup rentang yang tidak berdekatan, Anda dapat memanggil `copyRange` beberapa kali atau menggunakan `Worksheet.copy` untuk menggandakan seluruh sheet.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**Tip:** Saat menyalin workbook besar, aktifkan `CopyOptions.setPreserveCellStyle(true)` untuk menghindari duplikasi gaya yang tidak perlu, yang dapat meningkatkan kinerja.

## Cara menyalin pivot ke workbook – menangani multiple pivots

Jika sheet sumber berisi lebih dari satu pivot, Anda dapat mengiterasi tabel pivot pada worksheet dan menyalin masing‑masing secara individual:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

Pendekatan ini memastikan setiap pivot mempertahankan nama dan sumber data aslinya.

## Memuat workbook Excel Java – jebakan umum

* **File path separators:** Gunakan garis miring maju (`/`) atau `File.separator` untuk menjaga kode tetap platform‑independen.
* **Missing license:** Aspose.Cells beroperasi dalam mode evaluasi, tetapi output akan berisi watermark. Daftarkan lisensi dengan `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` sebelum memuat workbook untuk menghapus watermark.
* **Large files:** Untuk workbook lebih besar dari 100 MB, pertimbangkan menggunakan `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` dengan opsi streaming untuk mengurangi konsumsi memori.

## Ringkasan contoh lengkap end‑to‑end

Menggabungkan semuanya, berikut program akhir yang dapat Anda salin‑tempel ke IDE Anda:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Expected output:** Setelah dieksekusi, `PivotCopied.xlsx` muncul di direktori yang ditentukan. Membukanya di Excel menampilkan tata letak tabel pivot yang sama, filter, dan data seperti di `Source.xlsx`. Semua bidang terhitung dan pemformatan dipertahankan.

## Pertanyaan yang sering diajukan

* **Does this work with older Excel formats (.xls)?**  
  Ya. Aspose.Cells secara otomatis mendeteksi formatnya. Gunakan `new Workbook("file.xls")` dan logika penyalinan yang sama berlaku.

* **What if the pivot references external data sources?**  
  Salinan mempertahankan referensi sumber data asli. Jika lingkungan tujuan tidak dapat mengakses sumber tersebut, pivot akan menampilkan error `#REF!`. Untuk menghindarinya, segarkan pivot setelah menyalin atau ubah sumber datanya melalui `PivotTable.setDataSource(...)`.

* **Can I copy a pivot to a specific sheet name?**  
  Tentu saja. Setelah membuat worksheet tujuan, ubah namanya:

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## Kesimpulan

Anda kini mengetahui **how to duplicate pivot** tabel di Java menggunakan Aspose.Cells, cara **copy range between workbooks**, dan praktik terbaik untuk **load Excel workbook Java**. Dengan mengikuti proses lima langkah—load, define, create destination, copy, dan save—Anda dapat mengotomatisasi pembuatan laporan, mengarsipkan analisis, atau memecah workbook kompleks tanpa kehilangan fungsionalitas pivot.

Selanjutnya, jelajahi topik terkait seperti **copy pivot to workbook** dengan beberapa sheet, atau integrasikan pivot yang digandakan ke dalam pipeline pemrosesan data yang lebih besar menggunakan Apache POI untuk skenario non‑Aspose. Bereksperimenlah dengan berbagai pengaturan `CopyOptions` untuk menyempurnakan kinerja pada workbook berskala besar.

Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Membuat Tabel Pivot di Excel Menggunakan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Cara Memperbarui Sumber Tabel Pivot Excel dengan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Mengelompokkan Field Pivot dalam Workbook Excel Menggunakan Aspose.Cells untuk Java - Panduan Komprehensif](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}