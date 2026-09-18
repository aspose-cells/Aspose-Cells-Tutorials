---
category: general
date: 2026-09-18
description: Ekspor JSON ke Excel menggunakan Aspose.Cells di Java. Pelajari cara
  menyisipkan JSON ke dalam Excel, mengonversi JSON ke Excel, dan menyimpan workbook
  sebagai XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export json to excel
- insert json into excel
- how to insert json
- convert json to excel
- save workbook as xlsx
language: id
lastmod: 2026-09-18
og_description: Ekspor JSON ke Excel menggunakan Aspose.Cells untuk Java. Tutorial
  langkah demi langkah menunjukkan cara menyisipkan JSON ke dalam Excel, mengonversi
  JSON ke Excel, dan menyimpan buku kerja sebagai XLSX.
og_image_alt: Aspose.Cells Java code inserting JSON array into a single Excel cell
og_title: Ekspor JSON ke Excel dengan Aspose.Cells – Panduan Java
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Export JSON to Excel using Aspose.Cells in Java. Learn to insert JSON
    into Excel, convert JSON to Excel, and save workbook as XLSX.
  headline: Export JSON to Excel with Aspose.Cells in Java
  type: TechArticle
- description: Export JSON to Excel using Aspose.Cells in Java. Learn to insert JSON
    into Excel, convert JSON to Excel, and save workbook as XLSX.
  name: Export JSON to Excel with Aspose.Cells in Java
  steps:
  - name: Prepare your development environment.
    text: Prepare your development environment.
  - name: Define the JSON data source.
    text: Define the JSON data source.
  - name: Create a workbook and worksheet.
    text: Create a workbook and worksheet.
  - name: Insert JSON into Excel using a Smart Marker.
    text: Insert JSON into Excel using a Smart Marker.
  - name: Process the Smart Marker so the JSON appears in a single cell.
    text: Process the Smart Marker so the JSON appears in a single cell.
  - name: Save the workbook as an XLSX file.
    text: Save the workbook as an XLSX file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Ekspor JSON ke Excel dengan Aspose.Cells di Java
url: /id/java/excel-import-export/export-json-to-excel-with-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor JSON ke Excel dengan Aspose.Cells di Java

Jika Anda perlu **mengekspor JSON ke Excel**, panduan ini menunjukkan solusi lengkap menggunakan Aspose.Cells untuk Java. Anda akan melihat secara tepat cara menyisipkan JSON ke Excel, mengonversi JSON ke Excel, dan akhirnya **menyimpan workbook sebagai XLSX** tanpa meninggalkan IDE Anda.

Bekerja dengan data JSON umum terjadi saat membangun API, dasbor pelaporan, atau alat migrasi data. Daripada menyalin‑tempel secara manual, pendekatan di bawah ini mengotomatiskan seluruh alur sehingga Anda dapat menghasilkan file Excel secara programatis.

## Ekspor JSON ke Excel – panduan langkah‑demi‑langkah

Bagian‑bagian berikut akan memandu Anda melalui setiap langkah yang diperlukan:

1. Siapkan lingkungan pengembangan Anda.  
2. Definisikan sumber data JSON.  
3. Buat workbook dan worksheet.  
4. Sisipkan JSON ke Excel menggunakan Smart Marker.  
5. Proses Smart Marker sehingga JSON muncul dalam satu sel.  
6. Simpan workbook sebagai file XLSX.

Pada akhir tutorial ini Anda akan memiliki program Java yang dapat dijalankan dan menghasilkan file `JsonExport.xlsx` yang berisi array JSON di sel **A1**.

## Prasyarat

- Java Development Kit 8 atau yang lebih baru.  
- Maven atau Gradle untuk mengelola dependensi.  
- Aspose.Cells untuk Java (versi terbaru pada saat penulisan, 24.10).  
- Pengetahuan dasar tentang sintaks Java dan format JSON.

> **Tips profesional:** Aspose.Cells adalah pustaka komersial, tetapi lisensi evaluasi gratis dapat digunakan untuk pengembangan dan pengujian.

## Langkah 1: Siapkan proyek Java Anda

Tambahkan dependensi Aspose.Cells ke `pom.xml` (Maven) atau `build.gradle` (Gradle).

**Maven**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

**Gradle**

```groovy
implementation 'com.aspose:aspose-cells:24.10'
```

Setelah dependensi ter‑resolve, Anda dapat mengimpor kelas‑kelas yang diperlukan:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerException;
```

## Langkah 2: Definisikan sumber data JSON

String JSON mewakili sebuah array objek. Pada proyek nyata Anda mungkin membaca ini dari file, endpoint REST, atau basis data. Untuk ilustrasi kami menyematkan JSON langsung di dalam kode.

```java
// Step 2: Define the JSON data source (an array of objects)
String jsonData = "[{\"Name\":\"John\",\"Score\":85},{\"Name\":\"Anna\",\"Score\":92}]";
```

**Mengapa ini penting:** Aspose.Cells dapat memperlakukan array JSON sebagai satu sel ketika Anda menggunakan opsi `ArrayAsSingle`. Hal ini menghindari kebutuhan untuk memecah array ke baris dan kolom, yang ideal untuk mengekspor payload JSON mentah.

## Langkah 3: Buat workbook dan dapatkan worksheet pertama

Objek `Workbook` mewakili seluruh file Excel. Worksheet pertama (indeks 0) adalah tempat kami akan menempatkan JSON.

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Penjelasan:** Menginstansiasi `Workbook` tanpa parameter membuat workbook kosong dengan lembar default. Anda dapat menambahkan lembar lain nanti jika skenario Anda memerlukan beberapa set data.

## Langkah 4: Sisipkan JSON ke Excel menggunakan Smart Marker

Smart Markers adalah placeholder yang digantikan Aspose.Cells dengan data pada waktu runtime. Marker `&=jsonArray(ArrayAsSingle)` memberi tahu mesin untuk menulis seluruh array JSON ke dalam satu sel.

```java
// Step 4: Insert a Smart Marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=jsonArray(ArrayAsSingle)");
```

**Mengapa menggunakan Smart Marker?** Ia mengabstraksi logika binding data, memungkinkan Anda fokus pada format sumber (JSON) alih‑alih manipulasi sel tingkat rendah.

## Langkah 5: Kaitkan nama Smart Marker dengan data JSON

Anda harus mengikat identifier marker (`jsonArray`) dengan string JSON yang sebenarnya.

```java
// Step 5: Associate the Smart Marker name with the JSON data
workbook.getSmartMarkers().setDataSource("jsonArray", jsonData);
```

**Catatan:** Metode `setDataSource` menerima objek apa pun yang dapat diserialisasi oleh mesin Smart Marker, termasuk string JSON, koleksi Java, atau DataTables.

## Langkah 6: Proses Smart Marker sehingga array JSON ditulis ke sel

Memanggil `processSmartMarkers()` memicu penggantian marker dengan JSON yang terikat.

```java
// Step 6: Process the Smart Markers so the JSON array is written into the cell
workbook.processSmartMarkers();
```

Jika JSON tidak valid, Aspose.Cells akan melempar `SmartMarkerException`. Bungkus pemanggilan dalam blok try‑catch untuk ketahanan tingkat produksi.

## Langkah 7: Simpan workbook sebagai file XLSX

Akhirnya, tulis workbook ke disk. Ekstensi file menentukan format output; menggunakan `.xlsx` memastikan format Office Open XML modern.

```java
// Step 7: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/JsonExport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

**Hasil:** Membuka `JsonExport.xlsx` menampilkan array JSON persis seperti yang ada di `jsonData`, berada di sel **A1**.

## Contoh lengkap yang dapat dijalankan

Berikut adalah kelas Java yang berdiri sendiri yang dapat Anda salin, tempel, dan jalankan.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerException;

/**
 * Demonstrates how to export JSON to Excel using Aspose.Cells.
 * The program inserts a JSON array into a single cell and saves the workbook as XLSX.
 */
public class JsonToExcelExporter {
    public static void main(String[] args) {
        // 1. Define the JSON data source (an array of objects)
        String jsonData = "[{\"Name\":\"John\",\"Score\":85},{\"Name\":\"Anna\",\"Score\":92}]";

        try {
            // 2. Create a new workbook and obtain the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // 3. Insert a Smart Marker that treats the JSON array as a single cell
            worksheet.getCells().putValue(0, 0, "&=jsonArray(ArrayAsSingle)");

            // 4. Bind the Smart Marker name to the JSON string
            workbook.getSmartMarkers().setDataSource("jsonArray", jsonData);

            // 5. Process Smart Markers – this writes the JSON into cell A1
            workbook.processSmartMarkers();

            // 6. Save the workbook as an XLSX file
            String outputPath = "JsonExport.xlsx";
            workbook.save(outputPath);
            System.out.println("Workbook saved to " + outputPath);
        } catch (SmartMarkerException e) {
            System.err.println("Error processing Smart Markers: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error: " + e.getMessage());
        }
    }
}
```

### Output yang diharapkan

Menjalankan program mencetak:

```
Workbook saved to JsonExport.xlsx
```

Membuka **JsonExport.xlsx** menampilkan sel **A1** berisi:

```
[{"Name":"John","Score":85},{"Name":"Anna","Score":92}]
```

## Variasi umum dan kasus tepi

| Situasi | Cara menyesuaikan kode |
|-----------|----------------------|
| **Payload JSON besar** ( > 1 MB) | Tingkatkan ukuran heap JVM (`-Xmx2g`) untuk menghindari `OutOfMemoryError`. |
| **Beberapa objek JSON** yang memerlukan baris terpisah | Gunakan `ArrayAsRows` alih‑alih `ArrayAsSingle` dan petakan marker ke koleksi POJO. |
| **Menyimpan ke CSV** | Ganti `workbook.save(outputPath)` dengan `workbook.save(outputPath, com.aspose.cells.SaveFormat.CSV);`. |
| **Menambahkan baris header** | Tulis string statis ke `worksheet.getCells().putValue(0, 0, "JSON Payload");` sebelum menyisipkan Smart Marker. |
| **Menggunakan direktori berbeda** | Pastikan direktori ada atau buat dengan `new java.io.File(dir).mkdirs();`. |

## Tips untuk penggunaan produksi

- **Validasi JSON** sebelum memberikannya ke Aspose.Cells untuk mencegah pengecualian runtime.  
- **Gunakan try‑with‑resources** untuk setiap stream yang Anda buka saat membaca JSON dari sumber eksternal.  
- **Kunci workbook** jika beberapa thread mungkin menulis ke file yang sama secara bersamaan.  
- **Registrasi lisensi**: panggil `com.aspose.cells.License license = new com.aspose.cells.License(); license.setLicense("Aspose.Cells.lic");` pada saat aplikasi mulai.

## Langkah selanjutnya

Sekarang Anda dapat **mengekspor JSON ke Excel**, pertimbangkan untuk mengeksplorasi kemampuan terkait:

- **Menyisipkan JSON ke Excel** dengan pemformatan: terapkan gaya sel setelah memproses Smart Marker.  
- **Mengonversi JSON ke tabel Excel**: petakan objek JSON ke baris dan kolom


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik yang berhubungan erat dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Import JSON Data into Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [How to Insert Multiple Rows into Excel Using Aspose.Cells for Java](/cells/english/java/cell-operations/excel-automation-aspose-cells-java-insert-multiple-rows/)
- [How to Insert Images into Excel Using Java and Aspose.Cells](/cells/english/java/images-shapes/insert-image-into-excel-java-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}