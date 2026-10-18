---
category: general
date: 2026-08-20
description: Pelajari cara menulis JSON ke Excel dan mengisi workbook Excel dari JSON
  menggunakan smart markers Aspose dan Java – panduan langkah demi langkah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose smart markers
- convert json to excel
- write json to excel
- populate excel from json
- create excel workbook java
language: id
lastmod: 2026-08-20
og_description: Smart markers Aspose memungkinkan Anda menulis JSON ke Excel dan membuat
  contoh kode Java untuk workbook Excel. Ikuti tutorial ini untuk mengisi Excel dari
  JSON dengan cepat.
og_image_alt: Screenshot of an Excel file generated from a JSON array using Aspose.Cells
og_title: 'aspose smart markers: mengonversi JSON ke Excel di Java – panduan lengkap'
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to write JSON to Excel and populate an Excel workbook from JSON
    using aspose smart markers and Java – step‑by‑step guide.
  headline: How to use aspose smart markers to convert JSON to Excel in Java
  type: TechArticle
- description: Learn to write JSON to Excel and populate an Excel workbook from JSON
    using aspose smart markers and Java – step‑by‑step guide.
  name: How to use aspose smart markers to convert JSON to Excel in Java
  steps:
  - name: Expected output
    text: 'When you open `JsonArraySingleCell.xlsx`, cell **A1** contains:'
  - name: 1. Populating multiple cells with different JSON objects
    text: 'If you need to fill a table rather than a single cell, omit `ArrayAsSingle`
      and use the default array handling:'
  - name: 2. Using a JSON file instead of a hard‑coded string
    text: '```java String jsonPath = "data/people.json"; String jsonArray = new String(Files.readAllBytes(Paths.get(jsonPath)),
      StandardCharsets.UTF_8); ```'
  - name: 3. Handling nested JSON structures
    text: 'For nested objects, reference sub‑properties in the smart marker:'
  - name: 4. License activation
    text: 'To avoid the evaluation watermark, activate your license before creating
      the workbook:'
  type: HowTo
tags:
- Aspose
- Java
- Excel
- JSON
title: Cara menggunakan smart markers Aspose untuk mengonversi JSON ke Excel di Java
url: /id/java/excel-import-export/how-to-use-aspose-smart-markers-to-convert-json-to-excel-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menggunakan aspose smart markers untuk mengonversi JSON ke Excel di Java

Jika Anda perlu **aspose smart markers** untuk mengonversi JSON ke Excel, tutorial ini menunjukkan solusi siap‑jalankan. Anda akan melihat cara menulis JSON ke Excel, mengisi workbook Excel dari JSON, dan menghasilkan file dengan satu baris kode.

Contoh ini menggunakan Aspose.Cells for Java, sebuah perpustakaan yang menghilangkan kebutuhan Microsoft Office di server. Pada akhir panduan, Anda akan memiliki program Java lengkap yang membuat workbook Excel, menyisipkan array JSON ke dalam satu sel, dan menyimpan hasilnya sebagai `JsonArraySingleCell.xlsx`.

## Prasyarat

* Java Development Kit 17 atau yang lebih baru terpasang.
* Maven atau Gradle untuk mengelola dependensi (contoh menggunakan Maven).
* Lisensi Aspose.Cells for Java (evaluasi gratis dapat digunakan untuk pengujian).
* Familiaritas dasar dengan sintaks Java dan format JSON.

> **Tips profesional:** Jika Anda menjalankan kode tanpa lisensi, workbook yang dihasilkan akan berisi watermark evaluasi kecil pada lembar pertama.

## Tambahkan Aspose.Cells ke proyek Anda

Tambahkan dependensi berikut ke `pom.xml` Anda (Maven) atau yang setara di Gradle:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Perpustakaan ini menyediakan kelas `Workbook`, `Worksheet`, `JsonDataSource`, dan `SmartMarker` yang digunakan sepanjang tutorial ini.

## Langkah 1: Buat workbook Excel di Java

Pertama, buat instance objek `Workbook` baru. Ini mewakili file Excel kosong dalam memori.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // Creates a blank .xlsx file
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();
```

`Workbook` adalah titik masuk untuk semua operasi Excel. Secara default ia berisi satu worksheet, yang kami ambil untuk manipulasi lebih lanjut.

## Langkah 2: Siapkan array JSON yang ingin Anda tulis ke Excel

String JSON dapat berasal dari file, layanan web, atau dibangun secara programatis. Untuk tutorial ini kami menggunakan array inline sederhana:

```java
// Step 2: Define the JSON array that will be used as the data source
String jsonArray = "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]";
```

Struktur JSON cocok dengan bentuk yang diharapkan oleh smart markers Aspose.Cells: sebuah array objek dimana setiap objek memiliki properti `Name`.

## Langkah 3: Sisipkan smart marker yang memperlakukan array sebagai satu sel

Smart markers Aspose memungkinkan Anda menyisipkan placeholder langsung ke dalam sel. Opsi `ArrayAsSingle` memberi tahu engine untuk menempatkan seluruh array JSON ke dalam satu sel alih-alih memperluasnya menjadi tabel.

```java
// Step 3: Insert a smart marker that tells Aspose.Cells to treat the array as a single cell
cells.putValue("A1", "${jsonArray,ArrayAsSingle}");
```

Saat workbook diproses, `${jsonArray,ArrayAsSingle}` akan digantikan dengan teks JSON mentah.

## Langkah 4: Daftarkan sumber data JSON dengan nama smart marker

Hubungkan nama placeholder (`jsonArray`) ke instance `JsonDataSource`. Langkah ini mengikat string JSON ke marker.

```java
// Step 4: Register the JSON data source with the smart marker name
JsonDataSource dataSource = new JsonDataSource(jsonArray);
worksheet.getSmartMarkers().setDataSource("jsonArray", dataSource);
```

`JsonDataSource` mengurai JSON dan membuatnya tersedia untuk engine smart marker. Pemanggilan `setDataSource` mendaftarkannya dengan nama yang digunakan dalam sel (`jsonArray`).

## Langkah 5: Simpan workbook ke disk

Akhirnya, tulis workbook ke file fisik. Anda dapat memilih direktori mana saja yang Anda inginkan.

```java
// Step 5: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/JsonArraySingleCell.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Menjalankan program menghasilkan file Excel yang berisi array JSON di sel **A1**. Buka file tersebut dengan Excel, LibreOffice, atau penampil apa pun yang mendukung `.xlsx` untuk memverifikasi hasilnya.

![Tangkapan layar file Excel yang dihasilkan dari array JSON menggunakan Aspose.Cells.](/images/json-to-excel.png)

*Teks alt gambar: Tangkapan layar file Excel yang dihasilkan dari array JSON menggunakan Aspose.Cells.*

## Kode sumber lengkap

Menggabungkan semua bagian, berikut adalah kelas Java lengkap yang dapat dijalankan:

```java
import com.aspose.cells.*;

public class JsonArraySmartMarker {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                       // Empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Define the JSON array that will be used as the data source
        String jsonArray = "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]";

        // Step 3: Insert a smart marker that tells Aspose.Cells to treat the array as a single cell
        cells.putValue("A1", "${jsonArray,ArrayAsSingle}");

        // Step 4: Register the JSON data source with the smart marker name
        JsonDataSource dataSource = new JsonDataSource(jsonArray);
        worksheet.getSmartMarkers().setDataSource("jsonArray", dataSource);

        // Step 5: Save the workbook to a file
        String outputPath = "YOUR_DIRECTORY/JsonArraySingleCell.xlsx";
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### Output yang diharapkan

Saat Anda membuka `JsonArraySingleCell.xlsx`, sel **A1** berisi:

```
[{"Name":"John"},{"Name":"Jane"}]
```

Tidak ada baris atau kolom tambahan yang ditambahkan—ini menunjukkan bagaimana **aspose smart markers** memungkinkan Anda **menulis JSON ke Excel** sambil mempertahankan payload JSON tetap utuh.

## Variasi umum dan kasus tepi

### 1. Mengisi beberapa sel dengan objek JSON yang berbeda

Jika Anda perlu mengisi tabel daripada satu sel, hapus `ArrayAsSingle` dan gunakan penanganan array default:

```java
cells.putValue("A1", "${jsonArray}");
```

Aspose.Cells akan memperluas array menjadi baris, membuat kolom untuk setiap properti (`Name` dalam kasus ini). Ini berguna ketika Anda menginginkan tampilan tabel tradisional.

### 2. Menggunakan file JSON alih-alih string yang ditulis keras

```java
String jsonPath = "data/people.json";
String jsonArray = new String(Files.readAllBytes(Paths.get(jsonPath)), StandardCharsets.UTF_8);
```

Baca isi file ke dalam string, lalu ikuti Langkah 3‑5 tanpa perubahan. Pendekatan ini cocok untuk payload besar atau data yang diterima dari API eksternal.

### 3. Menangani struktur JSON bersarang

Untuk objek bersarang, referensikan sub‑properti dalam smart marker:

```java
cells.putValue("B2", "${jsonArray.Address.City}");
```

Aspose.Cells menelusuri hierarki secara otomatis, memungkinkan Anda mengisi laporan kompleks tanpa parsing manual.

### 4. Aktivasi lisensi

Untuk menghindari watermark evaluasi, aktifkan lisensi Anda sebelum membuat workbook:

```java
License license = new License();
license.setLicense("Aspose.Total.Java.lic");
```

Letakkan kode ini di awal `main`. File lisensi dapat disematkan sebagai sumber daya atau dimuat dari lokasi yang aman.

## Tips untuk penggunaan produksi

* **Gunakan kembali objek workbook** – Jika Anda menghasilkan banyak laporan dalam satu run, buat satu `Workbook` dan kloning worksheet alih-alih menginstansiasi workbook baru setiap kali.
* **Alirkan output** – Untuk file besar, gunakan `workbook.save(OutputStream, SaveFormat.XLSX)` untuk menulis langsung ke aliran respons dalam aplikasi web.
* **Validasi JSON** – Sebelum mengirim data ke `JsonDataSource`, validasi format JSON untuk mencegah kesalahan runtime.
* **Kinerja** – Smart markers dioptimalkan untuk operasi bulk; hindari mencampur penulisan sel‑per‑sel dengan pemrosesan smart marker dalam lembar yang sama.

## Kesimpulan

Anda sekarang tahu cara menggunakan **aspose smart markers** untuk **mengonversi JSON ke Excel**, **menulis JSON ke Excel**, dan **mengisi Excel dari JSON** menggunakan Java. Contoh lengkap membuat workbook Excel, menyisipkan array JSON ke dalam satu sel, dan menyimpan file—semua dengan hanya lima langkah singkat.

Selanjutnya, Anda mungkin ingin menjelajahi:

* Menghasilkan laporan multi‑sheet dari struktur JSON kompleks.
* Menggabungkan smart markers dengan formula Excel untuk perhitungan dinamis.
* Menggunakan `JsonDataSource` bersama `DataTable` untuk ekspor gaya CSV.

Silakan bereksperimen dengan payload JSON yang berbeda, rentang sel, dan opsi pemformatan. Dengan Aspose.Cells, mengubah data JSON menjadi workbook Excel yang rapi menjadi proses yang sederhana, berfokus pada kode. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Workbook Excel menggunakan Aspose.Cells di Java: Panduan Langkah‑per‑Langkah](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Membuat Laporan Excel Dinamis Menggunakan Aspose.Cells Java dan Smart Markers](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java-smart-markers/)
- [Menguasai Aspose.Cells Java: Implementasi Smart Markers & Formula untuk Otomatisasi Excel](/cells/english/java/formulas-functions/aspose-cells-java-smart-markers-formulas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}