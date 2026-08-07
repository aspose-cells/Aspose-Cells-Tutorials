---
category: general
date: 2026-07-06
description: Cara menyalin tabel pivot di Java dengan Aspose.Cells – panduan langkah
  demi langkah untuk menggandakan tabel pivot Excel secara programatis.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- duplicate excel pivot
language: id
lastmod: 2026-07-06
og_description: Cara menyalin tabel pivot di Java menggunakan Aspose.Cells memungkinkan
  Anda menggandakan tabel pivot Excel dengan cepat dan andal.
og_image_alt: Screenshot of Java code copying an Excel pivot table with Aspose.Cells
og_title: Cara menyalin tabel pivot di Java – Panduan lengkap Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
    to duplicate Excel pivot tables programmatically.
  headline: How to copy pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
title: Cara menyalin tabel pivot di Java menggunakan Aspose.Cells
url: /id/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin tabel pivot di Java menggunakan Aspose.Cells

Pernah bertanya-tanya **bagaimana menyalin pivot** tabel di dalam file Excel tanpa membuka workbook secara manual? Anda bukan satu-satunya. Dalam banyak alur pelaporan Anda perlu **menggandakan tabel pivot Excel** secara cepat—mungkin untuk membuat snapshot, memindahkannya ke lembar baru, atau menghasilkan templat untuk pengguna downstream.

Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang menunjukkan hal tersebut. Menggunakan pustaka Aspose.Cells for Java kami akan memuat workbook, menemukan rentang pivot sumber, menyalinnya ke lokasi baru, dan menyimpan hasilnya. Tidak ada referensi yang samar, hanya solusi konkret yang dapat Anda gunakan dalam proyek Anda hari ini.

---

## Prasyarat

* **Java Development Kit (JDK) 8+** – kode ini dapat dikompilasi dengan JDK terbaru apa pun.
* **Aspose.Cells for Java** versi 25.11 atau lebih baru – metode `Range.copy` yang mendukung tabel pivot diperkenalkan pada rilis ini.
* Sebuah file **input.xlsx** yang sudah berisi tabel pivot (Anda dapat membuatnya di Excel untuk pengujian).
* Alat build pilihan Anda (Maven, Gradle, atau `javac` biasa). Kami akan menampilkan dependensi Maven untuk memulai cepat.

```xml
<!-- Add this to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.12</version> <!-- Use the latest stable -->
</dependency>
```

---

## Langkah 1: Muat workbook sumber

Hal pertama yang kami lakukan adalah membuka file Excel yang berisi tabel pivot asli. Aspose.Cells memperlakukan workbook sebagai objek dalam memori, sehingga Anda dapat memanipulasinya tanpa meluncurkan Excel.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Mengapa ini penting:** Memuat workbook memberi kami akses ke lembar kerja, sel, dan yang paling penting, cache pivot yang mendukung tabel pivot. Tanpa langkah ini pustaka tidak memiliki apa pun untuk disalin.

---

## Langkah 2: Dapatkan lembar kerja yang berisi pivot

Jika workbook Anda memiliki beberapa lembar, Anda perlu menunjuk ke lembar yang tepat. Di sini kami cukup mengambil lembar pertama, tetapi Anda juga dapat menggunakan `get("SheetName")` untuk pencarian berdasarkan nama.

```java
// Obtain the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Tips pro:** Saat menangani banyak lembar, simpan indeks atau nama dalam file konfigurasi untuk menghindari hard‑coding angka.

---

## Langkah 3: Tentukan rentang sumber yang mencakup tabel pivot

Mulai dari versi 25.11 Aspose.Cells memungkinkan Anda memperlakukan tabel pivot sebagai rentang sel biasa. Tentukan sel kiri‑atas dan kanan‑bawah yang melingkupi seluruh pivot.

```java
// The range A1:D20 covers the whole pivot table in this example
Range sourceRange = worksheet.getCells().createRange("A1:D20");
```

> **Kasus tepi:** Jika pivot Anda berkembang secara dinamis (mis., baris ditambahkan kemudian), pertimbangkan menggunakan `worksheet.getPivotTables().get(0).getDataRange()` untuk mengambil rentang yang tepat secara programatis.

---

## Langkah 4: Tentukan rentang tujuan tempat pivot akan disalin

Pilih sel kosong mana pun tempat Anda ingin pivot yang digandakan muncul. Dalam demo ini kami mulai di **F1**, meninggalkan celah antara yang asli dan salinannya.

```java
// Destination starts at cell F1 – adjust as needed
Range destinationRange = worksheet.getCells().createRange("F1");
```

> **Mengapa tidak lembar baru?** Anda juga dapat membuat lembar kerja baru (`workbook.getWorksheets().add("Copy")`) dan menggunakan selnya sebagai tujuan. Metode `copy` yang sama berfungsi lintas lembar.

---

## Langkah 5: Salin tabel pivot ke lokasi baru

Sekarang keajaiban terjadi. Metode `copy` menggandakan pivot, cache-nya, pemformatan, dan bahkan slicer yang terkait (pada versi terbaru).

```java
// Perform the copy – the pivot is now duplicated at the destination
sourceRange.copy(destinationRange);
```

> **Penting:** Operasi penyalinan bersifat *deep*; tidak membuat referensi kembali ke pivot asli. Anda dapat memodifikasi pivot baru secara independen tanpa memengaruhi sumber.

---

## Langkah 6: Simpan workbook dengan pivot yang digandakan

Akhirnya, tulis workbook yang telah dimodifikasi kembali ke disk. Anda dapat menimpa yang asli atau membuat file baru; di sini kami memilih yang kedua agar sumber tetap tidak tersentuh.

```java
// Save the workbook – the duplicated pivot lives in output.xlsx
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

Saat Anda membuka **output.xlsx** di Excel, Anda akan melihat pivot asli di kolom A‑D dan salinan sempurna yang dimulai di kolom F. Kedua pivot dapat disegarkan secara terpisah.

---

## Contoh Kerja Lengkap

Menggabungkan semuanya, berikut kelas Java lengkap yang dapat Anda kompilasi dan jalankan langsung:

```java
import com.aspose.cells.*;

public class ExportPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Define the source range that includes the pivot table (supported from version 25.11)
        // Adjust the range to match your actual pivot dimensions
        Range sourceRange = worksheet.getCells().createRange("A1:D20");

        // Step 4: Define the destination range where the pivot table will be copied
        // Change "F1" to any starting cell you prefer
        Range destinationRange = worksheet.getCells().createRange("F1");

        // Step 5: Copy the pivot table to the new location
        sourceRange.copy(destinationRange);

        // Step 6: Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Hasil yang diharapkan:** Membuka `output.xlsx` menampilkan pivot asli (A1:D20) dan pivot identik yang dimulai di F1. Kedua tabel mempertahankan filter, gaya, dan field terhitung mereka.

---

## Menangani Variasi Umum

| Situasi | Apa yang harus disesuaikan |
|-----------|----------------|
| **Multiple pivots** pada lembar yang sama | Loop melalui `worksheet.getPivotTables()` dan salin masing‑masing dengan rentang tujuan masing‑masing. |
| **Dynamic data range** | Gunakan `worksheet.getPivotTables().get(0).getDataRange()` untuk mendeteksi area sumber secara otomatis. |
| **Copy to another workbook** | Muat instance `Workbook` kedua, buat lembar kerja tujuan, lalu panggil `sourceRange.copy(destWorksheet.getCells().createRange("A1"))`. |
| **Preserve slicers** | Mulai versi 25.12, slicer disalin secara otomatis ketika rentang mencakupnya. Verifikasi di Excel setelah menyimpan. |

---

## Tips Pro & Jebakan

* **Pemeriksaan versi:** Metode `copy` yang mendukung pivot ditambahkan pada **Aspose.Cells 25.11**. Jika Anda menggunakan versi yang lebih lama, akan muncul pengecualian. Selalu verifikasi versi `aspose-cells` di `pom.xml` Anda.
* **Kinerja:** Menyalin pivot besar dapat memakan banyak memori. Jika Anda hanya membutuhkan data, pertimbangkan mengekspor pivot ke tabel datar alih‑alih menggandakan seluruh objek.
* **Perilaku refresh:** Pivot yang digandakan mempertahankan cache-nya sendiri. Jika Anda mengubah data dasar, panggil `pivotTable.refresh()` pada pivot baru untuk menghitung ulang.
* **Keanehan format:** Beberapa format angka khusus mungkin tidak bertahan setelah penyalinan pada versi Excel yang sangat lama (<2007). Uji dengan versi Excel target audiens Anda.

---

## Kesimpulan

Anda kini memiliki jawaban lengkap, end‑to‑end untuk **cara menyalin pivot** tabel menggunakan Aspose.Cells for Java, dan Anda telah melihat cara **menggandakan tabel pivot Excel** dalam beberapa baris kode. Pendekatan ini bekerja untuk satu atau banyak pivot, lintas lembar kerja, bahkan antar workbook.

Langkah selanjutnya dapat meliputi:

* Mengotomatisasi penyalinan untuk setiap pivot dalam pekerjaan batch.
* Menambahkan kode untuk mengganti nama pivot yang digandakan (mis., `pivotTable.setName("Copy_of_Sales")`).
* Mengintegrasikan rutin ke dalam layanan pelaporan yang lebih besar yang menghasilkan PDF atau ekspor CSV.

Cobalah, sesuaikan rentang agar cocok dengan data nyata Anda, dan biarkan pustaka menangani pekerjaan berat. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}