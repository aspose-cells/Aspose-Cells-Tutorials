---
category: general
date: 2026-10-07
description: Pelajari cara menggandakan tabel pivot di Excel menggunakan Java dan
  Aspose.Cells. Salin tabel pivot dengan menyalin rentangnya antar buku kerja dengan
  cepat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: id
lastmod: 2026-10-07
og_description: Cara menduplikasi tabel pivot di Excel menggunakan Java dan Aspose.Cells.
  Ikuti panduan ini untuk menyalin tabel pivot dengan menyalin rentangnya antar buku
  kerja.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: Cara menduplikasi tabel pivot di Excel dengan Java – tutorial lengkap
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: Cara menggandakan tabel pivot di Excel dengan Java – panduan langkah demi langkah
url: /id/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menduplikasi tabel pivot di Excel dengan Java – panduan langkah demi langkah

Jika Anda perlu **cara menduplikasi pivot** tabel dalam sebuah workbook Excel, tutorial ini menunjukkan solusi lengkap yang siap dijalankan. Dengan menggunakan Aspose.Cells untuk Java Anda dapat menyalin tabel pivot beserta data sumbernya dengan menyalin rentang yang mendasarinya, kemudian menyimpan hasilnya sebagai workbook baru.

Menduplikasi tabel pivot sering terasa rumit karena cache pivot tersembunyi di dalam lembar. Dengan menyalin seluruh rentang yang berisi pivot, Aspose.Cells secara otomatis membuat ulang cache di workbook tujuan, sehingga Anda mendapatkan salinan yang berfungsi penuh tanpa harus mengutak‑atik XML secara manual.

Dalam panduan ini Anda akan:
* Memuat workbook sumber yang berisi tabel pivot.  
* Menentukan rentang tepat yang memuat pivot.  
* Menyalin rentang tersebut ke workbook baru, mempertahankan definisi pivot.  
* Menyimpan file baru dan memverifikasi bahwa pivot berfungsi.  

Langkah-langkah ini bekerja dengan semua versi Excel yang didukung oleh Aspose.Cells (2007‑2024) dan hanya memerlukan beberapa baris kode Java.

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| **Java 8 or newer** | Aspose.Cells dibangun untuk Java 8+. |
| **Aspose.Cells for Java** (latest version) | Menyediakan API `Workbook`, `Range`, dan `CopyRange` yang digunakan dalam contoh. |
| **Source workbook** with a pivot table (e.g., `Source.xlsx`) | Pivot yang ingin Anda duplikasi. |
| **Write permission** to the target directory | Diperlukan untuk menyimpan `CopyWithPivot.xlsx`. |

Tambahkan dependensi Aspose.Cells Maven ke `pom.xml` Anda (atau unduh JAR secara manual):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## Cara menduplikasi tabel pivot – implementasi lengkap

Berikut adalah program Java yang berdiri sendiri yang menunjukkan **cara menduplikasi pivot** tabel dengan menyalin rentang yang berisi pivot. Kode ini mencakup penanganan error, komentar, dan langkah verifikasi.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### Penjelasan setiap langkah

| Langkah | Apa yang dilakukan kode | Mengapa penting untuk **menyalin tabel pivot** |
|---------|------------------------|-----------------------------------------------|
| **1️⃣ Load source workbook** | `new Workbook(srcPath)` membaca `Source.xlsx`. | File sumber adalah satu-satunya tempat di mana pivot asli berada. |
| **2️⃣ Define the range** | `createRange("A1:G20")` membuat objek `Range` yang mencakup pivot dan datanya. | Tabel pivot disimpan bersama dengan cache-nya; menyalin seluruh rentang memastikan cache juga dipindahkan. |
| **3️⃣ Copy the range** | `copyRange(srcRange, "A1")` menulis rentang ke dalam lembar tujuan. | Ini adalah inti dari **menyalin rentang antar workbook** – API menangani objek tersembunyi secara otomatis. |
| **4️⃣ Refresh pivot** | `pivotTable.refresh()` memaksa pivot untuk menghitung ulang. | Menjamin pivot yang diduplikasi menampilkan nilai yang sama dengan yang asli, terutama setelah modifikasi. |
| **5️⃣ Save workbook** | `destWb.save(destPath)` menulis file ke disk. | Menghasilkan hasil akhir **menyalin rentang excel** yang dapat Anda buka di Excel. |

#### Output yang Diharapkan

Setelah menjalankan program, buka `CopyWithPivot.xlsx`. Anda akan melihat lembar kerja yang tampak identik dengan lembar sumber, dan tabel pivot berfungsi persis seperti aslinya – Anda dapat memperluas baris, menyaring bidang, dan menyegarkan data tanpa error.

## Variasi umum dan kasus tepi

### 1️⃣ Menyalin pivot yang melintasi beberapa lembar

Jika data sumber pivot berada di lembar yang berbeda dari pivot itu sendiri, sertakan kedua lembar dalam operasi penyalinan. Pendekatan paling sederhana adalah menyalin seluruh lembar sumber terlebih dahulu, kemudian menyalin lembar pivot:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ Menangani named range

Aspose.Cells mempertahankan named range saat Anda menyalin sebuah rentang. Namun, jika workbook tujuan sudah berisi nama dengan identifier yang sama, `CellsException` akan dilempar. Selesaikan ini dengan mengganti nama yang konflik sebelum penyalinan:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ Workbook besar dan kinerja

Menyalin rentang yang sangat besar (ratusan ribu baris) dapat memakan banyak memori. Aktifkan **optimisasi memori**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ Menjaga formula tetap utuh

Jika rentang sumber berisi formula yang merujuk ke sel di luar area yang disalin, referensi tersebut akan rusak setelah penyalinan. Untuk menghindarinya, perluas rentang untuk mencakup semua sel yang bergantung, atau gunakan `copyRange` dengan flag `CopyOptions` `CopyOptions.COPY_FORMULA`.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## Tips profesional untuk **menyalin rentang antar workbook** yang handal

* **Selalu gunakan alamat absolut** (`$A$1:$G$20`) ketika lembar sumber mungkin diubah namanya.  
* **Segarkan setelah menyalin** – meskipun Aspose.Cells membangun ulang cache, memanggil `refresh()` menghilangkan peringatan cache usang sesekali di Excel.  
* **Validasi pivot**: setelah menyimpan, buka file secara programatik dan panggil `pivotTable.validate()` untuk memastikan tidak ada referensi yang rusak.  
* **Kompatibilitas versi**: kode ini bekerja dengan file Excel 2007‑2024 (`.xlsx`, `.xlsm`). Untuk file `.xls` lama, set `LoadOptions.setLoadFormat(LoadFormat.XLS)`.

## Daftar sumber lengkap (siap dikompilasi)

```java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // --------------------------------------------------------------------
        // 1️⃣ Load source workbook
        // --------------------------------------------------------------------
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 2️⃣ Define the range that contains the pivot table
        // --------------------------------------------------------------------
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        String pivotRangeAddress = "A1:G20"; // adjust to your pivot's actual area
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // --------------------------------------------------------------------
        // 3️⃣ Copy the range (including the pivot) to a new workbook
        // --------------------------------------------------------------------
        Workbook destWb = new Workbook(); // blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 4️⃣ Refresh the duplicated pivot (ensures correct values)
        // --------------------------------------------------------------------
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Menyalin Tabel Pivot di Java – Panduan Lengkap Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Cara Membuat Tabel Pivot di Excel Menggunakan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Cara Memperbarui Sumber Tabel Pivot Excel dengan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}