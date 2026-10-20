---
category: general
date: 2026-10-07
description: Pelajari cara memuat JSON ke dalam Excel dan menghasilkan XLSX dari JSON
  menggunakan Aspose.Cells. Panduan langkah demi langkah ini juga menunjukkan cara
  mengisi Excel dari JSON dan menyimpan buku kerja sebagai XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- load json into excel
- generate xlsx from json
- populate excel from json
- save workbook as xlsx
- create workbook from json
language: id
lastmod: 2026-10-07
og_description: Muat JSON ke dalam Excel dan hasilkan XLSX dari JSON menggunakan Aspose.Cells
  untuk Java. Ikuti panduan ini untuk mengisi Excel dari JSON dan menyimpan buku kerja
  sebagai XLSX.
og_image_alt: Screenshot of an Excel workbook that was loaded with JSON data using
  Aspose.Cells
og_title: Muat JSON ke Excel dengan Aspose.Cells – panduan lengkap Java
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  headline: How to load JSON into Excel with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  name: How to load JSON into Excel with Aspose.Cells for Java
  steps:
  - name: 'Compile the program:'
    text: 'Compile the program:'
  - name: 'Run it:'
    text: 'Run it:'
  - name: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
    text: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cara memuat JSON ke Excel dengan Aspose.Cells untuk Java
url: /id/java/excel-import-export/how-to-load-json-into-excel-with-aspose-cells-for-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Muat JSON ke Excel dengan Aspose.Cells untuk Java

Jika Anda perlu **memuat JSON ke Excel**, tutorial ini menunjukkan cara yang andal untuk melakukannya dengan Aspose.Cells untuk Java. Anda akan melihat cara menghasilkan XLSX dari JSON, mengisi Excel dari JSON, dan akhirnya **menyimpan workbook sebagai XLSX**—semua dalam satu program yang berdiri sendiri.

Bekerja dengan JSON dalam spreadsheet umum ketika Anda mengekspor data dari layanan web, API, atau penyimpanan NoSQL. Pada akhir panduan ini Anda akan memiliki kelas Java siap‑jalankan yang membuat workbook dari JSON dan menulis hasilnya ke file di disk.

## Prasyarat

* Java 8 atau yang lebih baru terpasang (kode menggunakan fitur standar Java).
* Perpustakaan Aspose.Cells untuk Java (versi 23.10 atau lebih baru). Anda dapat memperolehnya dari [situs Aspose](https://downloads.aspose.com/cells/java) atau melalui Maven Central.
* IDE atau editor teks sederhana dan terminal untuk mengompilasi serta menjalankan kode Java.
* Familiaritas dasar dengan sintaks JSON dan konsep Excel.

> **Tips Pro:** Jika Anda menggunakan Maven, tambahkan dependensi berikut ke `pom.xml` Anda untuk menghindari pengelolaan JAR manual:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

## Langkah 1: Siapkan proyek dan impor kelas yang diperlukan

Buat kelas Java baru bernama `JsonToExcelDemo`. Impor kelas Aspose.Cells yang Anda perlukan untuk pembuatan workbook, penanganan worksheet, dan pemrosesan Smart Marker.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // The full implementation starts in the next step.
    }
}
```

*Mengapa langkah ini penting:* Mengimpor kelas yang tepat memastikan kompiler dapat menemukan API Aspose.Cells. Kelas `Workbook` mewakili file Excel, sementara `SmartMarkerProcessor` menjalankan konversi JSON‑ke‑Excel.

## Langkah 2: Tentukan sumber JSON yang akan dimuat ke Excel

Untuk contoh ini kami menggunakan array JSON kecil yang berisi dua objek. Dalam skenario nyata Anda dapat membaca JSON dari file, endpoint REST, atau basis data.

```java
// Step 2: Define the JSON data that will be used as the smart‑marker source
String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";
```

*Mengapa langkah ini penting:* String JSON adalah sumber data untuk operasi **populate Excel from JSON**. Menyimpan JSON dalam variabel `String` memudahkan untuk diteruskan ke `SmartMarkerProcessor`.

## Langkah 3: Buat workbook baru dan dapatkan worksheet pertama

Workbook baru memberi Anda kanvas bersih. Worksheet pertama (indeks 0) adalah tempat kami akan menyisipkan Smart Marker.

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty XLSX workbook
Worksheet worksheet = workbook.getWorksheets().get(0);
```

*Mengapa langkah ini penting:* Aspose.Cells bekerja dengan objek `Workbook` yang dapat disimpan nanti sebagai file XLSX. Mengakses `Worksheet` pertama memungkinkan kami menempatkan marker pada alamat sel yang diketahui.

## Langkah 4: Sisipkan Smart Marker yang memberi tahu Aspose.Cells cara memperlakukan JSON

Smart Markers adalah placeholder yang digantikan Aspose.Cells dengan data dari sumber. Marker `&=JSONData.ArrayAsSingle` memberi instruksi pada perpustakaan untuk memperlakukan seluruh array JSON sebagai nilai sel tunggal.

```java
// Step 4: Insert a smart‑marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");
```

*Mengapa langkah ini penting:* Menggunakan `ArrayAsSingle` menghindari perilaku default memperluas setiap elemen array menjadi baris terpisah. Ini berguna ketika Anda ingin teks JSON muncul persis dalam sel, atau ketika Anda berencana memecahnya nanti dengan formula.

## Langkah 5: Konfigurasikan SmartMarkerProcessor dengan sumber data JSON

Sekarang ikat string JSON ke nama logis `JSONData`. Processor akan menggantikan marker dengan data sebenarnya.

```java
// Step 5: Configure the SmartMarkerProcessor with the JSON data source
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
processor.setDataSource("JSONData", jsonData);
processor.process();   // expands the marker and writes JSON into the worksheet
```

*Mengapa langkah ini penting:* `setDataSource` menghubungkan nama yang digunakan dalam marker (`JSONData`) dengan payload JSON sebenarnya. `process()` melakukan pekerjaan berat: mengurai JSON, menerapkan logika marker, dan menulis hasil ke worksheet.

## Langkah 6: Simpan workbook yang dihasilkan sebagai file XLSX

Akhirnya, tulis workbook ke disk. Konstanta `SaveFormat.XLSX` menjamin format Office Open XML yang tepat.

```java
// Step 6: Save the resulting workbook
String outputPath = "JsonSingleCell.xlsx";   // adjust the path as needed
workbook.save(outputPath, SaveFormat.XLSX);
System.out.println("Workbook saved to " + outputPath);
```

*Mengapa langkah ini penting:* Menyimpan file menyelesaikan alur kerja **generate XLSX from JSON**. File yang dihasilkan dapat dibuka di Excel, LibreOffice, atau program spreadsheet lain yang mendukung XLSX.

### Kode sumber lengkap

Menggabungkan semua bagian, berikut adalah program lengkap yang dapat dijalankan yang **membuat workbook dari JSON**, **mengisi Excel dari JSON**, dan **menyimpan workbook sebagai XLSX**.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // 1. JSON source – replace with your own data if needed
        String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // 2. Create a fresh workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3. Place a smart‑marker that treats the JSON array as a single cell
        worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");

        // 4. Bind the JSON string to the marker name and process it
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
        processor.setDataSource("JSONData", jsonData);
        processor.process();

        // 5. Save the workbook as an XLSX file
        String outputPath = "JsonSingleCell.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### Hasil yang diharapkan

Saat Anda membuka `JsonSingleCell.xlsx` Anda akan melihat array JSON ditampilkan di sel **A1** persis seperti string asli:

```
[{"Name":"John","Age":30},{"Name":"Anna","Age":25}]
```

Jika Anda lebih suka setiap objek pada baris terpisah, ganti marker dengan `&=JSONData` (tanpa `.ArrayAsSingle`). Processor kemudian akan memperluas array menjadi baris individual, menunjukkan teknik **populate Excel from JSON** yang berbeda.

## Variasi umum dan kasus tepi

| Situasi | Penyesuaian |
|-----------|------------|
| **Payload JSON besar ( > 10 MB )** | Tingkatkan ukuran heap JVM (`-Xmx2g`) dan pertimbangkan streaming JSON untuk menghindari `OutOfMemoryError`. |
| **Objek bersarang** | Gunakan marker hierarkis seperti `&=JSONData.Name` dan `&=JSONData.Age` di dalam tabel untuk memetakan setiap properti ke kolom. |
| **File JSON alih-alih string** | Baca file ke dalam `String` dengan `java.nio.file.Files.readString(Path.of("data.json"))` dan berikan ke `setDataSource`. |
| **Perlu mempertahankan format JSON asli** | Pertahankan akhiran `.ArrayAsSingle`, atau bungkus JSON dalam CDATA jika Anda berencana menggunakan formula Excel yang mengurai JSON nanti. |
| **Beberapa worksheet** | Buat worksheet tambahan (`workbook.getWorksheets().add("Sheet2")`) dan ulangi penyisipan marker pada setiap sheet. |

> **Peringatan:** Smart Markers bersifat case‑sensitive. Pastikan nama logis (`JSONData`) cocok persis antara marker dan `setDataSource`.

## Menguji solusi

1. Kompilasi program:

   ```bash
   javac -cp ".:aspose-cells-23.10.jar" com/example/exceljson/JsonToExcelDemo.java
   ```

2. Jalankan program:

   ```bash
   java -cp ".:aspose-cells-23.10.jar" com.example.exceljson.JsonToExcelDemo
   ```

3. Verifikasi bahwa `JsonSingleCell.xlsx` muncul di direktori kerja dan dapat dibuka tanpa error.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Workbook Excel dari JSON – Panduan Lengkap Aspose.Cells](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Buat Workbook Excel C# – Sisipkan JSON dan Simpan sebagai XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)
- [Simpan Workbook Excel dari JSON – Panduan Lengkap](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}