---
category: general
date: 2026-09-27
description: Pelajari cara menghasilkan nama lembar dinamis di Excel dengan Java sambil
  mengisi template Excel dan membuat lembar dari data untuk pelaporan yang kuat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- dynamic sheet names
- generate multiple sheets
- create sheets from data
- populate excel template java
language: id
lastmod: 2026-09-27
og_description: Nama lembar dinamis memungkinkan Anda menghasilkan beberapa lembar
  dari satu set data. Tutorial ini menunjukkan cara mengisi templat Excel di Java
  dan membuat lembar dari data menggunakan Aspose.Cells.
og_image_alt: Screenshot showing an Excel workbook with dynamically generated sheet
  names using Java
og_title: Buat nama lembar dinamis di Excel dengan Java
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to generate dynamic sheet names in Excel with Java while
    you populate an Excel template and create sheets from data for robust reporting.
  headline: How to generate dynamic sheet names in Excel with Java
  type: TechArticle
- description: Learn how to generate dynamic sheet names in Excel with Java while
    you populate an Excel template and create sheets from data for robust reporting.
  name: How to generate dynamic sheet names in Excel with Java
  steps:
  - name: Add the Aspose.Cells for Java JAR to your project’s classpath (available
      from Maven Central or the Aspose website).
    text: Add the Aspose.Cells for Java JAR to your project’s classpath (available
      from Maven Central or the Aspose website).
  - name: Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project
      root.
    text: Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project
      root.
  - name: Execute the `main` method. The `output/` folder will contain the generated
      file.
    text: Execute the `main` method. The `output/` folder will contain the generated
      file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cara membuat nama lembar dinamis di Excel dengan Java
url: /id/java/worksheet-management/how-to-generate-dynamic-sheet-names-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menghasilkan nama lembar dinamis di Excel dengan Java

Jika Anda membutuhkan **dynamic sheet names** saat mengisi template Excel di Java, panduan ini akan memandu Anda melalui proses lengkap. Anda akan melihat cara *menghasilkan beberapa lembar* dari kumpulan data, dan bagaimana setiap lembar secara otomatis menerima nama unik. Pada akhir panduan Anda akan memiliki contoh yang dapat dijalankan yang membuat lembar dari data dan menyimpan hasilnya dengan konvensi penamaan yang diinginkan.

Membuat lembar secara dinamis merupakan kebutuhan umum untuk dasbor pelaporan, batch faktur, atau skenario apa pun di mana jumlah bagian detail tidak diketahui sebelumnya. Mesin Aspose.Cells Smart Marker membuat tugas ini ringkas dan dapat diandalkan, dan kode di bawah ini menunjukkan pendekatan yang direkomendasikan.

## Menggunakan nama lembar dinamis dengan Aspose.Cells

Aspose.Cells for Java menyediakan prosesor **Smart Marker** yang dapat membaca placeholder dalam workbook template dan memperluasnya menjadi baris, kolom, atau bahkan lembar kerja baru. Dengan mengonfigurasi `SmartMarkerOptions.DetailSheetNewName` Anda mengontrol nama setiap lembar yang dihasilkan. Placeholder `{0}` diganti dengan indeks berbasis nol dari baris data saat ini, memberikan Anda **dynamic sheet names** sepenuhnya seperti `Detail_0`, `Detail_1`, …​.

> **Pro tip:** Simpan workbook template dalam folder resources khusus dan gunakan jalur relatif bila memungkinkan. Ini menghindari hard‑coding jalur absolut yang dapat rusak di lingkungan yang berbeda.

## Langkah 1: Muat template Excel (populate excel template java)

Pertama, muat workbook yang berisi tag Smart Marker. Template harus memiliki lembar yang bernama, misalnya, `Detail` dengan penanda seperti `&=Orders!A1` yang memberi tahu prosesor di mana memulai penyisipan baris.

```java
import com.aspose.cells.*;

public class DynamicSheetNamesExample {

    public static void main(String[] args) throws Exception {
        // Load the template workbook that already contains Smart Markers.
        // Replace "templates/MasterDetailTemplate.xlsx" with the actual path.
        Workbook templateWorkbook = new Workbook("templates/MasterDetailTemplate.xlsx");
```

*Mengapa langkah ini penting:* Template mendefinisikan tata letak (header, formula, format) yang akan disalin ke setiap lembar yang dihasilkan. Tanpa template yang tepat, output akan kehilangan gaya dan formula.

## Langkah 2: Siapkan sumber data untuk membuat lembar dari data

Selanjutnya, bangun sumber data yang dapat diiterasi oleh prosesor Smart Marker. Dalam contoh ini kami menggunakan `Map<String, Object>` dimana kunci `"Orders"` cocok dengan nama penanda dalam template.

```java
        // Prepare a data source with multiple detail rows.
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();

        // Each element of the Object[] array represents one row.
        dataSource.put("Orders", new Object[] {
            new Object[] { 101, "Alice", 250.00 },
            new Object[] { 102, "Bob",   175.50 },
            new Object[] { 103, "Carol", 320.75 }
        });
```

*Mengapa langkah ini penting:* Mesin Smart Marker membaca array, membuat baris untuk setiap `Object[]` internal, dan—karena kami akan memintanya untuk menghasilkan lembar baru—membuat lembar kerja terpisah untuk setiap baris. Ini adalah inti dari **create sheets from data**.

## Langkah 3: Konfigurasikan SmartMarkerOptions untuk menghasilkan beberapa lembar dengan nama unik

Sekarang beri tahu Aspose.Cells cara menamai setiap lembar kerja baru. Placeholder `{0}` diganti dengan indeks baris saat ini.

```java
        // Configure options so every generated sheet gets a unique name.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} → row index (0‑based). Resulting names: Detail_0, Detail_1, …
        smartMarkerOptions.setDetailSheetNewName("Detail_{0}");
```

*Mengapa langkah ini penting:* Tanpa mengatur `DetailSheetNewName`, prosesor akan menggunakan kembali nama lembar asli untuk setiap baris, menimpa data. Opsi ini yang memungkinkan **dynamic sheet names**.

## Langkah 4: Proses SmartMarkers dan hasilkan workbook

Jalankan prosesor dengan sumber data dan opsi yang baru saja kami konfigurasikan.

```java
        // Execute the Smart Marker processor.
        templateWorkbook.getSmartMarkerProcessor().process(dataSource, smartMarkerOptions);
```

*Mengapa langkah ini penting:* Prosesor memperluas penanda, membuat jumlah lembar kerja yang diperlukan, menyalin tata letak template, dan mengisi setiap lembar dengan data baris yang sesuai.

## Langkah 5: Simpan dan verifikasi hasil

Akhirnya, tulis workbook ke disk. Buka file di Excel untuk melihat lembar yang dibuat secara otomatis.

```java
        // Save the workbook containing the newly generated sheets.
        templateWorkbook.save("output/MasterDetailResult.xlsx");
    }
}
```

**Output yang diharapkan**

Saat Anda membuka `MasterDetailResult.xlsx` Anda akan melihat tiga lembar kerja baru:

* `Detail_0` – berisi order 101 (Alice, 250.00)  
* `Detail_1` – berisi order 102 (Bob, 175.50)  
* `Detail_2` – berisi order 103 (Carol, 320.75)

Setiap lembar mempertahankan format, lebar kolom, dan semua formula yang ada di lembar template `Detail` asli.

## Contoh yang dapat dijalankan lengkap

Menggabungkan semua bagian memberikan Anda program mandiri yang dapat Anda kompilasi dan jalankan:

```java
import com.aspose.cells.*;

public class DynamicSheetNamesExample {

    public static void main(String[] args) throws Exception {
        // 1. Load the template workbook that contains Smart Markers.
        Workbook templateWorkbook = new Workbook("templates/MasterDetailTemplate.xlsx");

        // 2. Prepare the data source with multiple detail rows.
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        dataSource.put("Orders", new Object[] {
            new Object[] { 101, "Alice", 250.00 },
            new Object[] { 102, "Bob",   175.50 },
            new Object[] { 103, "Carol", 320.75 }
        });

        // 3. Configure SmartMarkerOptions to give each generated sheet a unique name.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.setDetailSheetNewName("Detail_{0}");

        // 4. Process the Smart Markers using the data source and the configured options.
        templateWorkbook.getSmartMarkerProcessor().process(dataSource, smartMarkerOptions);

        // 5. Save the resulting workbook with the newly created sheets.
        templateWorkbook.save("output/MasterDetailResult.xlsx");
    }
}
```

### Cara menjalankan

1. Tambahkan JAR Aspose.Cells for Java ke classpath proyek Anda (tersedia dari Maven Central atau situs web Aspose).  
2. Letakkan `MasterDetailTemplate.xlsx` di `templates/` relatif terhadap root proyek.  
3. Jalankan metode `main`. Folder `output/` akan berisi file yang dihasilkan.

## Variasi umum dan kasus tepi

| Situasi | Apa yang diubah |
|-----------|----------------|
| **Pola penamaan yang berbeda** | Gunakan `"OrderSheet_{0}_v{1}"` dan sertakan placeholder tambahan seperti `{1}` untuk indeks kedua (mis., nomor halaman). |
| **Set data besar** | Tingkatkan heap JVM (`-Xmx2g`) untuk menghindari `OutOfMemoryError` saat menghasilkan ratusan lembar. |
| **Pembuatan lembar bersyarat** | Sebelum memanggil `process`, filter array data sehingga baris yang tidak memenuhi kriteria diabaikan, sehingga mencegah lembar yang tidak diperlukan. |
| **Mempertahankan formula yang merujuk ke lembar lain** | Pertahankan nama lembar asli sebagai placeholder tersembunyi (mis., `DetailTemplate`) dan gunakan `SmartMarkerOptions.setDetailSheetNewName` hanya untuk nama yang terlihat; formula yang merujuk ke nama tersembunyi tetap akan terresolusi dengan benar. |

## Tips untuk otomatisasi Excel yang kuat

* **Validasi sumber data** – Pastikan setiap array internal memiliki jumlah elemen yang sama dengan kolom yang didefinisikan dalam template; panjang yang tidak cocok menyebabkan error runtime.  
* **Gunakan named ranges** dalam template untuk sintaks Smart Marker yang lebih jelas (`&=Orders!A1`).  
* **Tutup sumber daya** – Meskipun Aspose.Cells mengelola stream secara internal, memanggil secara eksplisit `templateWorkbook.dispose()` dalam blok `finally` dapat membebaskan memori native lebih cepat.  
* **Uji dengan nilai tepi** – Nol baris harus menghasilkan workbook hanya dengan lembar template asli; sumber data kosong memverifikasi bahwa kode Anda menangani “no data” dengan baik.

## Kesimpulan

Anda kini tahu cara **generate dynamic sheet names** di Excel menggunakan Java, cara **populate an Excel template** dan **create sheets from data**, serta cara **generate multiple sheets** secara otomatis dengan Aspose.Cells Smart Markers. Dengan mengikuti langkah-langkah di atas Anda dapat menyesuaikan pola ini untuk skenario pelaporan apa pun—apakah Anda membutuhkan puluhan lembar detail, konvensi penamaan khusus, atau pembuatan lembar bersyarat.

Siap memperluas solusi ini? Coba tambahkan chart ke setiap lembar yang dihasilkan, atau ekspor workbook ke PDF menggunakan `Workbook.save("result.pdf", SaveFormat.PDF)`. Kedua teknik tersebut dibangun di atas fondasi dynamic‑sheet yang baru saja Anda kuasai. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Menguasai Lembar Excel Dinamis di Java dengan Aspose.Cells: Panduan Komprehensif](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Panduan Lembar Excel Dinamis Aspose Cells Java](/cells/german/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Panduan Lembar Excel Dinamis Aspose Cells Java](/cells/french/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}