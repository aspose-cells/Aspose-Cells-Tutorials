---
category: general
date: 2026-08-11
description: Buat workbook baru Aspose di Java, tambahkan properti khusus Excel, lalu
  simpan workbook sebagai XLSB dengan contoh langkah demi langkah lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: id
lastmod: 2026-08-11
og_description: Buat workbook baru Aspose di Java, tambahkan properti khusus Excel,
  dan simpan workbook sebagai XLSB dengan contoh lengkap yang siap dijalankan.
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: Buat workbook baru Aspose – tambahkan properti khusus Excel
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: Buat workbook baru Aspose – tambahkan properti khusus Excel dan simpan sebagai
  XLSB
url: /id/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat workbook baru Aspose – tambahkan custom property Excel dan simpan sebagai XLSB

Jika Anda perlu **create new workbook Aspose** dalam aplikasi Java, panduan ini menunjukkan secara tepat cara melakukannya. Anda akan belajar untuk **add custom property Excel**, mengambil nilai, dan **save workbook as XLSB** tanpa kehilangan metadata apa pun.

Tutorial ini mencakup semua hal mulai dari penyiapan proyek hingga verifikasi file yang disimpan. Tidak diperlukan dokumentasi eksternal; cukup ikuti langkah-langkah dan jalankan kode.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

- Java Development Kit (JDK) 8 atau yang lebih tinggi terpasang.
- Maven atau Gradle untuk mengelola dependensi (contoh menggunakan Maven).
- Lisensi Aspose.Cells for Java yang aktif (atau gunakan mode evaluasi gratis untuk pengujian).

## Langkah 1: Tambahkan Aspose.Cells ke proyek Anda

Tambahkan artefak Maven Aspose.Cells ke `pom.xml` Anda. Dependensi ini menyediakan kelas yang diperlukan untuk objek **create new workbook Aspose**.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Jika Anda lebih suka Gradle, ganti potongan Maven dengan baris `implementation "com.aspose:aspose-cells:23.12"` yang setara.

## Langkah 2: Buat workbook baru Aspose

Langkah fungsional pertama adalah menginstansiasi objek `Workbook`. Objek ini mewakili file Excel dalam memori dan menjadi titik masuk untuk semua operasi selanjutnya.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

Membuat workbook baru Aspose memberi Anda workbook bersih dengan lembar kerja default, siap untuk penyesuaian.

## Langkah 3: Tambahkan custom property Excel

Properti khusus memungkinkan Anda menyimpan metadata sewenang-wenang di dalam file Excel. Di sini kami **add custom property Excel** bernama `ProjectId` dengan nilai numerik.

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

Metode `add` menerima nama properti dan nilai dari tipe yang didukung apa pun (string, number, date, dll.). Metadata ini ikut bersama file ke mana pun Anda menyalinnya.

## Langkah 4: Ambil dan tampilkan properti khusus

Membaca kembali properti memverifikasi bahwa properti tersebut disimpan dengan benar. Anda juga dapat menggunakan nilai yang diambil dalam logika bisnis Anda.

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

Casting ke `int` berhasil karena kami menyimpan nilai numerik. Jika Anda menyimpan string, gunakan `(String)` sebagai gantinya.

## Langkah 5: Simpan workbook sebagai XLSB

Sekarang Anda **save workbook as XLSB**. Format XLSB menyimpan workbook dalam representasi biner, yang lebih cepat dibuka dan lebih kecil di disk. Semua properti khusus secara otomatis dipertahankan.

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Ganti `"WithCustomProps.xlsb"` dengan path absolut jika Anda memerlukan file di direktori tertentu. Enum `SaveFormat.XLSB` memberi tahu Aspose.Cells untuk menulis dalam format biner.

## Langkah 6: Verifikasi output

Jalankan program dari IDE atau baris perintah Anda:

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

Anda akan melihat:

```
ProjectId = 12345
```

Buka `WithCustomProps.xlsb` di Excel. Arahkan ke **File → Info → Properties → Advanced Properties → Custom**. Entri `ProjectId` dengan nilai `12345` akan terdaftar, mengonfirmasi bahwa langkah **add custom property excel** berhasil dan operasi **save workbook as xlsb** mempertahankan metadata.

## Pertanyaan umum dan kasus tepi

### Bagaimana jika saya perlu menyimpan properti string?

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

Ambil dengan:

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### Bisakah saya menambahkan beberapa properti khusus sekaligus?

Ya. Panggil `add` berulang kali untuk setiap pasangan nama/nilai. Aspose.Cells tidak membatasi jumlah properti khusus, tetapi jaga ukuran total tetap wajar untuk menghindari pembengkakan file.

### Bagaimana format biner memengaruhi kinerja?

File XLSB memuat lebih cepat karena menghindari parsing XML. Hal ini terutama terasa pada workbook dengan banyak baris, formula, atau gambar tersemat.

### Bagaimana jika saya perlu bekerja dengan file XLSX yang sudah ada?

Ganti konstruktor `new Workbook()` dengan `new Workbook("ExistingFile.xlsx")`. Sisanya langkah (menambahkan properti, menyimpan sebagai XLSB) tetap sama.

## Kode sumber lengkap

Berikut adalah contoh lengkap yang siap dijalankan. Salin ke file bernama `CustomPropertiesXlsb.java` di dalam folder `src/main/java` Anda.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Menjalankan kelas ini menghasilkan file XLSB yang berisi properti khusus dan dapat dibuka di versi Microsoft Excel modern apa pun.

## Kesimpulan

Anda kini tahu cara **create new workbook Aspose**, **add custom property Excel**, dan **save workbook as XLSB** menggunakan Java. Contoh ini menunjukkan siklus hidup lengkap: inisialisasi, penyuntikan metadata, verifikasi, dan serialisasi biner.

Selanjutnya, jelajahi topik terkait seperti **setting document properties**, **working with Excel formulas**, atau **converting between XLSX and XLSB**. Masing‑masing topik ini dibangun di atas API Aspose.Cells yang sama yang baru saja Anda gunakan, sehingga Anda dapat memperluas solusi tanpa mempelajari pustaka baru.

Silakan bereksperimen dengan tipe data berbeda, beberapa lembar kerja, atau perlindungan kata sandi—Aspose.Cells mendukung semua skenario tersebut secara langsung. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang dibangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Simpan Workbook Excel Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Cara Membuat dan Menyimpan Workbook Excel sebagai SVG menggunakan Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Buat Workbook Excel dan Tambahkan Label dengan Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}