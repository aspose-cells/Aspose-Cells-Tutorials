---
category: general
date: 2026-09-27
description: Menyalin tabel pivot di Java dengan Aspose.Cells – panduan langkah demi
  langkah yang menunjukkan cara menyalin rentang dan mempertahankan definisi pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot table
- copy range aspose cells
language: id
lastmod: 2026-09-27
og_description: Salin tabel pivot di Java menggunakan Aspose.Cells. Ikuti tutorial
  lengkap ini untuk menyalin rentang Aspose.Cells dan menjaga definisi pivot tetap
  utuh.
og_image_alt: Screenshot of copy pivot table operation in Aspose.Cells Java
og_title: Menyalin tabel pivot di Java – Panduan cepat Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
    shows how to copy range and preserve pivot definitions.
  headline: How to copy a pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cara menyalin tabel pivot di Java menggunakan Aspose.Cells
url: /id/java/excel-pivot-tables/how-to-copy-a-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin pivot table di Java menggunakan Aspose.Cells

Jika Anda perlu **menyalin pivot table** dari satu workbook ke workbook lain, panduan ini menunjukkan secara tepat cara melakukannya dengan Aspose.Cells untuk Java. Solusi ini bekerja untuk pivot apa pun yang telah Anda buat, dan mempertahankan definisi pivot tanpa harus membuat ulang secara manual.

Anda akan belajar cara memuat file sumber, menentukan rentang yang berisi pivot, menyalin rentang tersebut ke workbook baru, dan akhirnya menyimpan hasilnya. Tutorial ini juga mencakup jebakan umum, seperti mempertahankan sumber data dan menangani workbook berukuran besar.

## Apa yang Anda perlukan

Sebelum memulai, pastikan Anda memiliki:

* Java 17 atau lebih baru (kode juga dapat dikompilasi dengan JDK 8+)
* Aspose.Cells untuk Java 23.9 atau yang lebih baru – versi terbaru menawarkan dukungan **copy range aspose cells** yang paling andal
* File Excel sumber yang berisi pivot table (misalnya `SourceWithPivot.xlsx`)
* IDE atau alat build (Maven/Gradle) yang dapat merujuk ke JAR Aspose.Cells

## Langkah 1: Muat workbook sumber yang berisi pivot table

Tindakan pertama adalah membuka workbook yang menyimpan pivot yang ingin Anda duplikat. Memuat file membuat representasi dalam memori dari semua worksheet, sel, dan cache pivot.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Access the first worksheet (adjust the index if needed)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Mengapa ini penting:**  
Aspose.Cells membaca seluruh workbook, termasuk sheet cache pivot yang tersembunyi. Jika Anda melewatkan langkah ini, operasi **copy pivot table** berikutnya akan kehilangan sumber data yang mendasarinya.

## Langkah 2: Buat workbook tujuan yang kosong

Selanjutnya, buat instance workbook baru yang akan menerima pivot yang disalin. Memulai dengan workbook bersih menghindari penimpaan yang tidak disengaja.

```java
        // Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Tip:** Workbook default berisi satu sheet kosong, yang cocok untuk penyalinan sederhana. Jika Anda perlu menyalin ke nama sheet tertentu, ubah nama `destWs` dengan `destWs.setName("TargetSheet")`.

## Langkah 3: Tentukan rentang sumber yang mencakup pivot table

Pivot table menempati blok sel berbentuk persegi panjang. Anda harus menentukan rentang yang tepat; jika tidak, hanya data mentah yang akan disalin. Pada contoh ini kami mengasumsikan pivot berada di **A1:G20**, tetapi Anda dapat menyesuaikan alamatnya sesuai file Anda.

```java
        // Define the range that includes the pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Mengapa ini berhasil:**  
Ketika Anda memanggil `createRange` pada koleksi `Cells` worksheet, Aspose.Cells menyertakan definisi pivot, cache-nya, dan semua pemformatan. Inilah inti dari **how to copy pivot table** dengan benar.

## Langkah 4: Salin rentang yang telah ditentukan ke sheet tujuan

Sekarang gunakan metode `copy` untuk menduplikasi rentang tersebut. Metode ini menyalin semua yang ada di dalam rentang, termasuk definisi pivot, formula, dan gaya.

```java
        // Copy the range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));
```

**Catatan penting:**  
Jika Anda hanya membutuhkan data tanpa pivot, Anda dapat menggunakan `srcRange.copyData`. Namun, untuk **copy pivot table** yang sesungguhnya Anda harus menyalin seluruh rentang seperti yang ditunjukkan di atas.

## Langkah 5: Simpan workbook tujuan

Terakhir, tulis workbook baru ke disk. File yang dihasilkan akan berisi pivot table yang berfungsi penuh dan identik dengan sumbernya.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Menjalankan program menghasilkan `CopyPivotResult.xlsx` dengan tata letak pivot, filter, dan perhitungan yang sama persis dengan file asli.

## Output yang diharapkan

Saat Anda membuka `CopyPivotResult.xlsx` di Excel:

* Pivot table muncul di **A1:G20** pada sheet pertama.
* Semua bidang baris/kolom, filter, dan nilai tetap utuh.
* Memperbarui pivot akan memperbarui sumber data yang sama seperti workbook sumber (jika data sumber tersemat).

## Kasus tepi dan tip praktis

| Situasi | Cara menanganinya |
|-----------|------------------|
| **Pivot mencakup lebih banyak kolom daripada yang diperkirakan** | Gunakan `srcWs.getPivotTables().get(0).getPivotTableArea()` untuk mendapatkan alamat tepat secara programatis. |
| **Workbook sumber berisi beberapa pivot** | Lakukan iterasi pada `srcWs.getPivotTables()` dan salin setiap rentang secara terpisah, sesuaikan alamat tujuan. |
| **Workbook besar menyebabkan tekanan memori** | Aktifkan `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` sebelum memuat sumber. |
| **Anda hanya perlu menyalin definisi pivot, bukan data** | Setelah menyalin, hapus baris data sumber di tujuan dengan `destWs.getCells().deleteRows(startRow, count)`. |
| **File tujuan harus mempertahankan pemformatan asli** | Atur `CopyOptions` dengan `options.setPasteType(PasteType.ALL)` untuk penyalinan dengan fidelitas penuh. |

**Pro tip:** Selalu verifikasi pivot yang disalin dengan memanggil `destWs.getPivotTables().get(0).refresh()` secara programatis. Ini memastikan cache terbaru, terutama ketika data sumber berada pada koneksi eksternal.

## Contoh lengkap yang dapat dijalankan

Berikut seluruh program yang dapat Anda salin‑tempel ke IDE. Ganti `YOUR_DIRECTORY` dengan jalur sebenarnya di mesin Anda.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 3: Define the range that includes the pivot table in the source sheet
        // Adjust the address if your pivot occupies a different area
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 4: Copy the defined range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Menjalankan kode ini akan **menyalin pivot table** persis seperti yang dijelaskan, dan memperlihatkan cara paling sederhana untuk **copy range aspose cells** sambil mempertahankan fungsionalitas pivot.

## Kesimpulan

Sekarang Anda tahu cara **menyalin pivot table** di Java menggunakan Aspose.Cells, mulai dari memuat workbook sumber hingga menyimpan file tujuan. Panduan ini mencakup langkah‑langkah penting, menjelaskan mengapa setiap langkah penting, dan menangani kasus tepi yang umum.  

Selanjutnya, Anda dapat menjelajahi:

* **how to copy pivot table** antar worksheet yang berbeda dalam satu workbook
* Menggunakan **copy range aspose cells** untuk menduplikasi chart atau conditional formatting
* Mengotomatiskan refresh pivot setelah penyalinan agar data tetap terkini

Silakan bereksperimen dengan rentang yang lebih besar, beberapa pivot, atau mengintegrasikan logika ini ke dalam pipeline pemrosesan Excel yang lebih besar. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}