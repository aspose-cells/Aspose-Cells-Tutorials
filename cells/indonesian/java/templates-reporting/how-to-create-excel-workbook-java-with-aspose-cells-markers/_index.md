---
category: general
date: 2026-11-25
description: Buat contoh kode Java untuk membuat workbook Excel menggunakan smart
  markers Aspose.Cells untuk mengikat array JSON sebagai nilai tunggal.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- Aspose.Cells smart marker
- Java JSON to Excel
- setSmartMarkerData
- Excel export Java
language: id
lastmod: 2026-11-25
og_description: Buat buku kerja Excel Java dengan Aspose.Cells untuk dengan mudah
  mengekspor array JSON sebagai sel tunggal. Ikuti panduan langkah demi langkah.
og_image_alt: Screenshot of an Excel workbook created in Java using Aspose.Cells smart
  markers
og_title: Buat Buku Kerja Excel Java – Panduan Smart Marker Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  headline: How to create Excel workbook Java with Aspose.Cells markers
  type: TechArticle
- description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  name: How to create Excel workbook Java with Aspose.Cells markers
  steps:
  - name: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
    text: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
  - name: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
    text: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
  - name: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
    text: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
  - name: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
    text: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
  - name: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
    text: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
  - name: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
    text: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
  - name: Confirm that cell **A1** reads `One, Two, Three`.
    text: Confirm that cell **A1** reads `One, Two, Three`.
  - name: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
    text: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cara membuat workbook Excel Java dengan penanda Aspose.Cells
url: /id/java/templates-reporting/how-to-create-excel-workbook-java-with-aspose-cells-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat workbook Excel Java dengan penanda Aspose.Cells

Jika Anda perlu **membuat workbook Excel Java** yang menulis array JSON ke dalam satu sel, tutorial ini menunjukkan cara tepatnya. Dengan menggunakan smart marker Aspose.Cells Anda dapat memperlakukan seluruh array sebagai satu nilai, menghindari loop manual dan penulisan sel‑per‑sel.

Anda akan belajar cara menyiapkan workbook, mendefinisikan smart marker, mengikat sumber data `Map` yang berisi array bergaya JSON, dan akhirnya menyimpan file. Contoh ini bekerja dengan Java 17+, Maven, dan perpustakaan percobaan gratis Aspose.Cells for Java.

---

![Screenshot of an Excel workbook created in Java using Aspose.Cells smart markers](excel-workbook-java.png){: .center-image alt="Tangkapan layar workbook Excel yang dibuat di Java menggunakan smart marker Aspose.Cells"}

## Prerequisites

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Java 17 atau lebih baru | Fitur bahasa terbaru dan pembaruan keamanan |
| Maven 3.6+ | Menyederhanakan manajemen dependensi |
| Aspose.Cells for Java (v23.12 atau lebih baru) | Menyediakan API `Workbook`, `Worksheet`, dan smart‑marker yang digunakan dalam contoh |
| Pengetahuan dasar tentang koleksi Java | Anda akan membuat `Map<String, Object>` yang berfungsi sebagai sumber data |

Add the Aspose.Cells dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Membuat workbook Excel Java – contoh lengkap

Program berikut adalah solusi **lengkap, dapat dijalankan**. Salin ke dalam file bernama `ExcelSmartMarkerDemo.java`, kompilasi, dan jalankan.

```java
package com.example.excel;

import com.aspose.cells.*;
import java.util.HashMap;
import java.util.Map;

/**
 * Demonstrates how to create Excel workbook Java using Aspose.Cells smart markers.
 * The smart marker "{{jsonArray:ArrayAsSingle}}" treats the whole array as a single cell value.
 */
public class ExcelSmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                       // empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // first (default) sheet

        // Step 2: Define a smart marker that treats a JSON array as a single value
        // The "ArrayAsSingle" option concatenates the array elements with commas.
        String smartMarker = "{{jsonArray:ArrayAsSingle}}";
        worksheet.getCells().get("A1").putValue(smartMarker);

        // Step 3: Prepare the data source – a simple string array
        Map<String, Object> dataSource = new HashMap<>();
        dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });

        // Step 4: Bind the data to the smart marker and save the workbook
        worksheet.getCells().get("A1").setSmartMarkerData(dataSource);
        workbook.save("JsonSingleValue.xlsx");   // workbook saved to project root
        System.out.println("Workbook created successfully.");
    }
}
```

### Apa yang dilakukan kode

1. **Membuat workbook baru** – `new Workbook()` memberikan Anda file Excel dalam memori dengan lembar kerja default.  
2. **Menempatkan smart marker di sel A1** – `{{jsonArray:ArrayAsSingle}}` memberi tahu Aspose.Cells untuk mengganti penanda dengan *seluruh* array, dipisahkan oleh koma.  
3. **Membangun sumber data `Map`** – Kunci `"jsonArray"` cocok dengan nama penanda; nilainya adalah `String[]`.  
4. **Memanggil `setSmartMarkerData`** – Ini mengikat map ke penanda dan melakukan penggantian.  
5. **Menyimpan file** – `workbook.save(...)` menulis `JsonSingleValue.xlsx` ke disk.

Saat Anda membuka file Excel yang dihasilkan, sel **A1** berisi:

```
One, Two, Three
```

Array ditampilkan sebagai satu string yang dipisahkan koma karena opsi `ArrayAsSingle`.

---

## Menggunakan smart marker Aspose.Cells untuk mengikat data JSON

Aspose.Cells smart markers adalah cara yang kuat untuk memetakan objek kompleks (termasuk struktur mirip JSON) langsung ke lembar kerja. Sintaks `{{fieldName:Option}}` berfungsi seperti mesin templat:

* **fieldName** – kunci dalam sumber data Anda (`Map`, POJO, atau `DataTable`).  
* **Option** – mengontrol cara koleksi diproses. `ArrayAsSingle` memperlakukan seluruh koleksi sebagai satu nilai; opsi lain seperti `Array` akan memperluas array ke beberapa baris.

**Mengapa menggunakan smart marker alih-alih loop?**  
Loop memerlukan perhitungan alamat sel secara manual, indeks yang rawan kesalahan, dan kode tambahan untuk styling. Smart marker memungkinkan Anda menulis placeholder deklaratif, menjaga kode Java tetap singkat, dan membiarkan perpustakaan menangani detail tata letak.

---

## Menyiapkan sumber data Java Map

`Map<String, Object>` adalah kontainer data paling sederhana untuk Aspose.Cells:

```java
Map<String, Object> dataSource = new HashMap<>();
dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });
```

*Kunci (`jsonArray`) harus cocok dengan nama penanda secara tepat.*

Anda juga dapat menggunakan `List<String>`, POJO kustom, atau bahkan `Map` bersarang untuk struktur JSON yang lebih kompleks. Aspose.Cells akan menelusuri grafik objek secara otomatis.

**Tip:** Jika Anda perlu memformat string yang digabungkan secara berbeda (mis., menggunakan titik koma), pra‑proses array di Java sebelum menetapkannya ke map:

```java
String joined = String.join(";", new String[] {"One","Two","Three"});
dataSource.put("jsonArray", new String[] { joined });
```

---

## Menyimpan workbook dan memverifikasi output

```java
workbook.save("JsonSingleValue.xlsx");
```

Metode `save` mendukung banyak format (`.xlsx`, `.xls`, `.csv`, `.pdf`). Untuk tutorial ini kami menggunakan format default Excel Open XML.

**Langkah verifikasi**

1. Buka `JsonSingleValue.xlsx` di Microsoft Excel, LibreOffice Calc, atau Google Sheets.  
2. Pastikan sel **A1** berisi `One, Two, Three`.  
3. Periksa bahwa tidak ada baris atau kolom tambahan yang ditambahkan – smart marker melakukan penggantian di tempat.

Jika sel menampilkan teks penanda mentah (`{{jsonArray:ArrayAsSingle}}`), periksa kembali bahwa:

* Nama penanda cocok dengan kunci map secara tepat (case‑sensitive).  
* `setSmartMarkerData` dipanggil **setelah** penanda ditempatkan.  
* Versi Aspose.Cells mendukung opsi `ArrayAsSingle` (tersedia sejak v20.3).

---

## Variasi umum dan kasus tepi

| Skenario | Penyesuaian |
|----------|-------------|
| **Pembatas berbeda** | Gunakan `ArrayAsSingle` bersama dengan penggabungan khusus di Java (lihat tip di atas). |
| **Beberapa array dalam satu lembar** | Tempatkan penanda tambahan seperti `{{anotherArray:ArrayAsSingle}}` di sel lain dan tambahkan entri yang sesuai ke map. |
| **Objek JSON bersarang** | Berikan `Map<String, Object>` bersarang; referensikan bidang dengan notasi titik (`{{parent.child}}`). |
| **Set data besar** | Untuk ribuan baris, pilih opsi `Array` agar Aspose.Cells memperluas baris secara otomatis, yang |

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Membuat dan Mengekspor Excel ke HTML Menggunakan Aspose.Cells Java | Panduan Operasi Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Ekspor Workbook Excel sebagai Gambar Menggunakan Aspose.Cells untuk Java: Panduan Langkah‑per‑Langkah](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Cara Membuat dan Menyimpan Workbook Excel sebagai SVG menggunakan Aspose.Cells untuk Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}