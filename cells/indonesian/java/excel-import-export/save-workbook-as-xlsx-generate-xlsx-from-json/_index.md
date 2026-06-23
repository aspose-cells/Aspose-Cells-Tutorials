---
category: general
date: 2026-06-21
description: Simpan buku kerja sebagai XLSX menggunakan SmartMarkerProcessor untuk
  menghasilkan XLSX dari JSON dan dengan mudah mengisi Excel dari data JSON.
draft: false
keywords:
- save workbook as xlsx
- generate xlsx from json
- populate excel from json
language: id
og_description: Simpan workbook sebagai XLSX dengan satu potongan kode Java. Pelajari
  cara menghasilkan XLSX dari JSON dan mengisi Excel dari JSON menggunakan SmartMarker.
og_title: Simpan Buku Kerja sebagai XLSX – Hasilkan XLSX dari JSON
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Save workbook as XLSX using SmartMarkerProcessor to generate XLSX from
    JSON and easily populate Excel from JSON data.
  headline: Save Workbook as XLSX – Generate XLSX from JSON
  type: TechArticle
- description: Save workbook as XLSX using SmartMarkerProcessor to generate XLSX from
    JSON and easily populate Excel from JSON data.
  name: Save Workbook as XLSX – Generate XLSX from JSON
  steps:
  - name: Expected Result
    text: 'After you run the program, open `output.xlsx`. You’ll see a sheet named
      **Sheet1** with two rows of data:'
  - name: Customizing the Template
    text: 'If you’d rather control column order or add a header row, create a tiny
      template before running the code:'
  - name: 1. Nested JSON Objects
    text: SmartMarker can dive into nested structures using dot notation (`${jsonArray.Address.City}`).
      Just ensure your JSON string reflects that hierarchy.
  - name: 2. Large Datasets
    text: 'When dealing with thousands of rows, disable workbook calculation before
      processing:'
  - name: 3. Data Types
    text: 'Dates, numbers, and booleans are inferred automatically, but you can force
      a format:'
  - name: 4. Multiple Placeholders
    text: You can feed several JSON arrays into the same workbook by using distinct
      placeholder names (`${orders}`, `${customers}`) and calling `processor.apply`
      for each.
  type: HowTo
- questions:
  - answer: No. The library is self‑contained; just add the JAR (or Maven dependency)
      and you’re ready to **save workbook as xlsx**.
    question: Do I need to install anything besides the Aspose Cells JAR?
  - answer: 'Absolutely. Replace `workbook.save("output.xlsx", SaveFormat.XLSX);`
      with: ```java try (FileOutputStream out = new FileOutputStream("output.xlsx"))
      { workbook.save(out, SaveFormat.XLSX); } ```'
    question: Can I write directly to a stream instead of a file?
  - answer: 'Use the `SmartMarkerProcessor.setCustomFieldNames` method to map JSON
      keys to placeholder names. ## Conclusion We’ve covered everything you need to
      **save workbook as xlsx** while **generating XLSX from JSON** and **populating
      Excel from JSON** using Aspose Cells’ SmartMarker. The short program show'
    question: What if my JSON keys don’t match Excel column names?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Simpan Buku Kerja sebagai XLSX – Buat XLSX dari JSON
url: /id/java/excel-import-export/save-workbook-as-xlsx-generate-xlsx-from-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Simpan Workbook sebagai XLSX – Hasilkan XLSX dari JSON

Pernah perlu **menyimpan workbook sebagai xlsx** tetapi hanya memiliki data JSON? Anda bukan satu‑satunya yang mengalami hal itu. Baik Anda mengambil respons API, membaca file konfigurasi, atau sekadar bereksperimen dengan laporan Excel berbasis data, mengubah JSON menjadi spreadsheet yang rapi adalah permintaan yang sering.

Dalam panduan ini kami akan menelusuri contoh Java lengkap yang **menghasilkan XLSX dari JSON** dan menunjukkan secara tepat bagaimana **mengisi Excel dari JSON** menggunakan processor SmartMarker Aspose Cells. Tanpa referensi yang samar—hanya kode yang dapat Anda salin, tempel, dan jalankan.

## Apa yang Anda Butuhkan

- Java 17 (atau JDK terbaru)  
- Perpustakaan Aspose Cells untuk Java (versi trial gratis sudah cukup)  
- IDE sederhana atau alat build baris perintah (Maven/Gradle)  
- Potongan JSON yang akan dimasukkan ke dalam workbook  

Itu saja—tanpa layanan tambahan, tanpa langkah tersembunyi. Mari kita mulai.

## Simpan Workbook sebagai XLSX – Proses Lengkap

Berikut adalah seluruh program, mulai dari mengimpor perpustakaan hingga menyimpan file ke disk. Perhatikan komentar; mereka menjelaskan **mengapa** setiap baris penting, bukan hanya **apa** yang dilakukannya.

```java
// ---------------------------------------------------------------
// Save Workbook as XLSX – Complete Java Example
// ---------------------------------------------------------------
import com.aspose.cells.*;
import com.google.gson.JsonArray; // For parsing raw JSON string

public class JsonToExcelDemo {

    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook that will receive the data
        Workbook workbook = new Workbook();

        // Step 2: Initialize the SmartMarker processor for the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

        // Step 3: Enable the flag to treat an array as a single record.
        // This tells SmartMarker to iterate over each element in the JSON array.
        processor.setArrayAsSingle(true);

        // Step 4: Prepare the JSON array source.
        // In a real‑world scenario you might read this from a file or API.
        String json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // Step 5: Apply the JSON data to the SmartMarker using the placeholder ${jsonArray}
        // The JsonArray class from Aspose wraps the raw string so SmartMarker can understand it.
        processor.apply("${jsonArray}", new JsonArray(json));

        // OPTIONAL: Save the workbook to see the result.
        // This is the line that actually **save workbook as xlsx**.
        workbook.save("output.xlsx", SaveFormat.XLSX);

        System.out.println("Workbook saved successfully as output.xlsx");
    }
}
```

> **Tip pro:** Jika Anda menggunakan Maven, tambahkan dependensi berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.10.1</version>
</dependency>
```

### Hasil yang Diharapkan

Setelah menjalankan program, buka `output.xlsx`. Anda akan melihat sebuah sheet bernama **Sheet1** dengan dua baris data:

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 25  |

Itulah seluruh pengalaman **populate excel from json** dalam kurang dari 30 baris Java.

![save workbook as xlsx example](example.png)

*Image alt text: “save workbook as xlsx example”*

## Hasilkan XLSX dari JSON – Cara Kerja SmartMarker

SmartMarker pada dasarnya adalah mesin templat untuk Excel. Dengan menempatkan `${jsonArray}` di sel mana pun (atau rentang) pada workbook kosong, Anda memberi tahu processor “ganti placeholder ini dengan data dari array JSON.” Ketika `processor.apply` dijalankan, ia:

1. Mengurai JSON menjadi koleksi record.  
2. Memetakan setiap properti (`Name`, `Age`) ke kolom berdasarkan konteks placeholder.  
3. Menyisipkan baris secara otomatis, menangani tipe data untuk Anda.

Karena kami memanggil `processor.setArrayAsSingle(true)`, seluruh array diperlakukan sebagai satu set record logis, yang merupakan pola paling umum saat **generating XLSX from JSON**.

### Menyesuaikan Templat

Jika Anda ingin mengontrol urutan kolom atau menambahkan baris header, buat templat kecil sebelum menjalankan kode:

| A            | B   |
|--------------|-----|
| **Name**     | **Age** |
| ${jsonArray.Name} | ${jsonArray.Age} |

Simpan ini sebagai `template.xlsx` dan muat alih‑alih workbook kosong:

```java
Workbook workbook = new Workbook("template.xlsx");
```

Langkah‑langkah selanjutnya tetap sama, dan output akan mempertahankan baris header yang Anda definisikan.

## Populate Excel from JSON – Kasus Khusus & Tips

### 1. Objek JSON Bersarang  
SmartMarker dapat menelusuri struktur bersarang menggunakan notasi titik (`${jsonArray.Address.City}`). Pastikan string JSON Anda mencerminkan hierarki tersebut.

### 2. Dataset Besar  
Saat menangani ribuan baris, nonaktifkan perhitungan workbook sebelum pemrosesan:

```java
workbook.getSettings().setCalculateFormula(false);
```

Aktifkan kembali setelah menyimpan untuk menjaga performa tetap cepat.

### 3. Tipe Data  
Tanggal, angka, dan boolean diidentifikasi secara otomatis, tetapi Anda dapat memaksa format tertentu:

```java
processor.apply("${jsonArray.BirthDate}", new JsonArray(json));
workbook.getWorksheets().get(0).getCells().get("C2").setNumberFormat("mm/dd/yyyy");
```

### 4. Banyak Placeholder  
Anda dapat memasukkan beberapa array JSON ke dalam workbook yang sama dengan menggunakan nama placeholder yang berbeda (`${orders}`, `${customers}`) dan memanggil `processor.apply` untuk masing‑masing.

## Pertanyaan Umum Terjawab

**T: Apakah saya perlu menginstal sesuatu selain JAR Aspose Cells?**  
J: Tidak. Perpustakaan ini berdiri sendiri; cukup tambahkan JAR (atau dependensi Maven) dan Anda siap **save workbook as xlsx**.

**T: Bisakah saya menulis langsung ke stream alih‑alih file?**  
J: Tentu. Ganti `workbook.save("output.xlsx", SaveFormat.XLSX);` dengan:

```java
try (FileOutputStream out = new FileOutputStream("output.xlsx")) {
    workbook.save(out, SaveFormat.XLSX);
}
```

**T: Bagaimana jika kunci JSON saya tidak cocok dengan nama kolom Excel?**  
J: Gunakan metode `SmartMarkerProcessor.setCustomFieldNames` untuk memetakan kunci JSON ke nama placeholder.

## Kesimpulan

Kami telah membahas semua yang Anda perlukan untuk **save workbook as xlsx** sambil **generating XLSX from JSON** dan **populating Excel from JSON** menggunakan SmartMarker Aspose Cells. Program singkat ini menunjukkan siklus lengkap: membuat workbook, mengonfigurasi SmartMarker, memberi array JSON, dan akhirnya menyimpan file.

Selanjutnya, coba perpanjang templat dengan formula, styling, atau beberapa worksheet—setiap konsep tersebut dibangun langsung di atas fondasi yang baru saja Anda kuasai. Jika Anda menemukan kendala, meninjau kembali bagian “Edge Cases & Tips” biasanya dapat menghilangkan kebingungan.

Selamat coding, semoga spreadsheet Anda selalu bersih seperti JSON Anda!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Save XLSX Files Using Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/workbook-operations/save-xlsx-files-aspose-cells-dotnet/)
- [How to Save Excel Workbook in Java Using Aspose.Cells](/cells/english/java/automation-batch-processing/excel-automation-java-aspose-cells-guide/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}