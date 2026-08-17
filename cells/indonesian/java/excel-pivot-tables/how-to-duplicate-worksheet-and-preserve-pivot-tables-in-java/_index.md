---
category: general
date: 2026-08-17
description: Cara menduplikasi lembar kerja di Java menggunakan Aspose.Cells, mempertahankan
  tabel pivot, menyalin pivot ke buku kerja baru, dan membuat buku kerja dari sebuah
  lembar.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: id
lastmod: 2026-08-17
og_description: Cara menduplikasi lembar kerja di Java menggunakan Aspose.Cells, mempertahankan
  tabel pivot, menyalin pivot ke buku kerja baru, dan membuat buku kerja dari sebuah
  lembar—semua langkah dijelaskan.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: Cara menduplikasi lembar kerja dan mempertahankan tabel pivot – Panduan
  Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: Cara menduplikasi lembar kerja dan mempertahankan tabel pivot di Java
url: /id/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menggandakan lembar kerja dan mempertahankan tabel pivot di Java

Menggandakan lembar kerja sambil mempertahankan tabel pivot tetap utuh adalah kebutuhan yang sering muncul ketika Anda mengotomatisasi pelaporan Excel. Panduan ini menunjukkan cara menyalin pivot ke buku kerja baru menggunakan Aspose.Cells for Java, serta membahas cara mempertahankan pivot ketika Anda membuat buku kerja dari sebuah lembar.

Anda akan belajar cara memuat buku kerja yang ada, menggandakan lembar kerja yang berisi tabel pivot, dan menyimpan hasilnya sebagai file baru. Tutorial ini mengasumsikan Anda memiliki lingkungan pengembangan Java dasar dan lisensi Aspose.Cells yang valid (evaluasi gratis dapat digunakan untuk pengujian). Tidak ada alat eksternal yang diperlukan selain JAR Aspose.Cells.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* Java Development Kit (JDK) 8 atau yang lebih baru.
* Maven atau Gradle untuk mengelola dependensi Aspose.Cells.
* File Excel (`source.xlsx`) yang berisi setidaknya satu tabel pivot pada lembar kerja pertama.
* Direktori tempat Anda dapat membaca file sumber dan menulis buku kerja yang digandakan.

Tambahkan dependensi Aspose.Cells ke `pom.xml` Anda (Maven) atau `build.gradle` (Gradle). Untuk Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## Cara menggandakan lembar kerja dengan tabel pivot

Operasi inti adalah proses tiga langkah: muat, salin, dan simpan. Setiap langkah dijelaskan di bawah ini.

### Langkah 1 – Muat buku kerja yang berisi tabel pivot

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*Mengapa langkah ini penting*: Objek `Workbook` mewakili seluruh file Excel. Dengan mengambil lembar kerja pertama (`get(0)`), Anda menargetkan lembar yang memuat tabel pivot yang ingin Anda gandakan.

### Langkah 2 – Buat buku kerja baru dan gandakan seluruh lembar kerja

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` menggandakan lembar kerja **termasuk** semua objek tertanam, formula, dan cache pivot. Ini adalah cara yang direkomendasikan untuk **how to copy pivot** karena definisi pivot dan sumber datanya dipindahkan bersama.

### Langkah 3 – Simpan buku kerja baru

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

Setelah dijalankan, `copy_with_pivot.xlsx` berisi salinan persis dari lembar asli, dan tabel pivot berfungsi tanpa konfigurasi tambahan.

**Hasil yang diharapkan**: Membuka `copy_with_pivot.xlsx` di Excel menampilkan lembar kerja yang digandakan dengan tata letak pivot, filter, dan bidang terhitung yang sama seperti file sumber.

## Cara menyalin pivot ke buku kerja lain

Jika Anda perlu memindahkan tabel pivot tanpa menyalin seluruh lembar, Anda dapat mengekstrak cache pivot dan melampirkannya ke lembar kerja baru. Potongan kode berikut mendemonstrasikan pendekatan tersebut:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

Kode ini menjawab **how to copy pivot** dengan menyalin hanya objek pivot, bukan seluruh lembar kerja. Metode `addCopy` pada koleksi `PivotTables` memastikan cache pivot digandakan, memenuhi persyaratan **how to preserve pivot**.

## Cara mempertahankan pivot saat membuat buku kerja dari lembar

Kadang‑kadang Anda memulai dengan lembar yang tidak termasuk dalam buku kerja (misalnya, Anda menghasilkan lembar di memori). Untuk **create workbook from sheet** sambil mempertahankan pivot, ikuti langkah‑langkah berikut:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

Dengan menambahkan lembar kerja ke `Workbook` baru setelah pivot sepenuhnya didefinisikan, Anda menjamin bahwa **how to preserve pivot** berfungsi bahkan ketika lembar berasal dari luar file yang ada.

## Tips praktis dan jebakan umum

| Tip | Mengapa penting |
|-----|-----------------|
| Gunakan `addCopy` alih‑alih `copy` | `addCopy` menggandakan cache pivot yang mendasari; `copy` biasa dapat kehilangan koneksi ke sumber data. |
| Simpan file sumber dan tujuan di sistem file yang sama | Jalur relatif dalam sumber data pivot terresolusikan dengan benar, mengurangi kesalahan “source not found”. |
| Verifikasi cache pivot setelah menyalin | Panggil `pivot.refresh()` jika data sumber berubah antara proses penyalinan dan penyimpanan. |
| Buang (dispose) workbook setelah selesai | `sourceWorkbook.dispose();` membebaskan sumber daya native, yang penting untuk file besar. |

## Kasus tepi yang mungkin Anda temui

* **Beberapa lembar kerja dengan pivot yang saling bergantung** – Gandakan setiap lembar kerja secara terpisah; cache yang dibagi akan digandakan secara otomatis, tetapi Anda mungkin perlu menetapkan kembali koneksi data eksternal.
* **Tabel pivot berdasarkan kueri SQL eksternal** – Pastikan lingkungan tujuan dapat mengakses basis data yang sama; jika tidak, pivot akan menampilkan kesalahan “#REF!”. 
* **Buku kerja besar (>100 MB)** – Gunakan `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` untuk mengurangi tekanan memori selama operasi penyalinan.

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang menggabungkan semua langkah yang dibahas. Simpan sebagai `CopyPivotTable.java`, sesuaikan jalur file, dan jalankan dengan IDE pilihan Anda atau melalui `javac`/`java`.



## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang erat kaitannya dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Membuat Tabel Pivot di Excel Menggunakan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Cara Memperbarui Sumber Tabel Pivot Excel dengan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Cara Menerapkan Slicer dalam Tabel Pivot Menggunakan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}