---
category: general
date: 2026-06-18
description: Cara menggunakan sequence di Java untuk menghasilkan array dinamis dan
  menyimpan workbook sebagai xlsx – tutorial lengkap, praktis untuk pengembang.
draft: false
keywords:
- how to use sequence
- save workbook as xlsx
- use sequence function
- create excel workbook java
- set dynamic array formula
language: id
og_description: cara menggunakan sequence di Java untuk membuat array dinamis dan
  menyimpan workbook sebagai xlsx. ikuti panduan ini untuk solusi lengkap yang dapat
  dijalankan.
og_title: Cara Menggunakan SEQUENCE di Workbook Excel Java – Tutorial Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: how to use sequence in Java to generate dynamic arrays and save workbook
    as xlsx – a complete, hands‑on tutorial for developers
  headline: How to Use SEQUENCE in Java Excel Workbook – Step‑by‑Step Guide
  type: TechArticle
- description: how to use sequence in Java to generate dynamic arrays and save workbook
    as xlsx – a complete, hands‑on tutorial for developers
  name: How to Use SEQUENCE in Java Excel Workbook – Step‑by‑Step Guide
  steps:
  - name: Generate a Calendar Header
    text: '```java sheet.getCells().get("A1").setFormula("=SEQUENCE(1,12,1,1)"); ```'
  - name: Create a Multiplication Table
    text: '```java sheet.getCells().get("A1").setFormula("=SEQUENCE(5,5,1,1)*SEQUENCE(5,5,1,1)");
      ```'
  - name: Expected Output
    text: '- An `dynamic_sequence_demo.xlsx` file appears in your project directory.
      - Opening the file in Excel shows a 3×2 block of numbers (1‑6) automatically
      filled.'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Dynamic Arrays
title: Cara Menggunakan SEQUENCE dalam Workbook Excel Java – Panduan Langkah demi
  Langkah
url: /id/java/formulas-functions/how-to-use-sequence-in-java-excel-workbook-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menggunakan SEQUENCE dalam Workbook Excel Java – Panduan Langkah‑ demi‑Langkah

Pernah bertanya‑tanya **bagaimana cara menggunakan sequence** untuk mengisi rentang sel tanpa menulis loop? Anda tidak sendirian. Di Excel modern, fungsi `SEQUENCE` membuat rentang spill‑range berisi angka, dan dengan Java Anda dapat langsung menerapkan kekuatan itu ke dalam workbook.  

Dalam tutorial ini kami akan menjelaskan cara membuat workbook Excel dengan Java, **menetapkan formula array dinamis** menggunakan `SEQUENCE`, menghitung ulang lembar, dan akhirnya **menyimpan workbook sebagai xlsx**. Pada akhir tutorial Anda akan memiliki program yang dapat dijalankan dan dapat langsung dimasukkan ke proyek apa pun.

## Apa yang Anda Butuhkan

- Java 17 atau lebih baru (kode ini bekerja dengan Java 8+, tetapi JDK terbaru memberikan kinerja terbaik).  
- Aspose.Cells for Java (atau perpustakaan apa pun yang mendukung formula array dinamis).  
- Sebuah IDE atau editor teks sederhana—Visual Studio Code sudah cukup.  

Tidak diperlukan plugin Maven tambahan atau dependensi yang tidak umum selain perpustakaan itu sendiri.

## Langkah 1: Membuat Workbook Excel dengan Java

Hal pertama yang harus dilakukan adalah **membuat excel workbook java**. Di sinilah kita membuat objek `Workbook` baru yang akan menampung semua lembar kerja kita.

```java
import com.aspose.cells.*;

public class SequenceDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();
```

*Mengapa ini penting*: Kelas `Workbook` adalah titik masuk untuk segala manipulasi Excel. Anggap saja sebagai buku catatan kosong yang menunggu data Anda.

## Langkah 2: Mengambil Worksheet Pertama

Selanjutnya, kita memerlukan tempat untuk menaruh formula kita. Secara default workbook baru memiliki satu lembar, jadi kita cukup mengambilnya.

```java
        // Step 2: Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*Tips profesional*: Jika Anda membutuhkan beberapa lembar, cukup panggil `workbook.getWorksheets().add("Sheet2")` dan ulangi prosesnya.

## Langkah 3: **Menetapkan Formula Array Dinamis** Menggunakan Fungsi SEQUENCE

Sekarang kita sampai pada inti tutorial—**bagaimana cara menggunakan sequence** di dalam sebuah sel. Formula `=SEQUENCE(3,2)` membuat rentang spill 3‑baris kali 2‑kolom yang dimulai dari sel tempat Anda menaruhnya.

```java
        // Step 3: Insert a dynamic array formula that spills into B1:C3
        // This will generate numbers 1‑6 arranged in 3 rows and 2 columns.
        sheet.getCells().get("A1").setFormula("=SEQUENCE(3,2)");
```

*Apa yang terjadi?*  
- `SEQUENCE(rows, columns)` memberi tahu Excel untuk menghasilkan matriks angka berurutan.  
- Karena ini adalah **formula array dinamis**, Excel secara otomatis memperluas hasil ke sel‑sel tetangga (B1:C3 dalam contoh kami).  

Jika Anda penasaran dengan variasi, coba `=SEQUENCE(5,1,10,2)` untuk memulai dari 10 dan melangkah sebesar 2.

## Langkah 4: Hitung Ulang Agar Rentang Spill Terbaru

Excel tidak mengevaluasi formula sampai Anda memintanya. Di Java kami memicu proses perhitungan:

```java
        // Step 4: Recalculate formulas so the spilled range is up‑to‑date
        workbook.calculateFormula();
```

*Mengapa harus menghitung ulang?* Tanpa pemanggilan ini, sel‑sel akan berisi teks formula tetapi tidak hasil numeriknya—menyebabkan file yang disimpan terlihat kosong.

## Langkah 5: **Menyimpan Workbook sebagai XLSX**

Akhirnya, kami menyimpan file ke disk. Ini mendemonstrasikan **save workbook as xlsx** menggunakan perpustakaan yang sama.

```java
        // Step 5: Save the workbook with the dynamic array data
        workbook.save("dynamic_sequence_demo.xlsx");
        System.out.println("Workbook saved successfully!");
    }
}
```

Saat Anda membuka `dynamic_sequence_demo.xlsx` di Excel 365 atau versi lebih baru, Anda akan melihat:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |
| 7 | 8 | 9 |

*Catatan*: Angka‑angka secara otomatis spill dari A1 ke sel‑sel tetangga, persis seperti yang ditentukan oleh fungsi `SEQUENCE`.

## Menjelajahi Variasi Fungsi SEQUENCE

Sekarang Anda sudah tahu **bagaimana cara menggunakan sequence**, mari cepat menjelajahi beberapa skenario umum.

### Membuat Header Kalender

```java
sheet.getCells().get("A1").setFormula("=SEQUENCE(1,12,1,1)");
```

Ini membuat satu baris dengan angka 1‑12—sempurna untuk header bulan.

### Membuat Tabel Perkalian

```java
sheet.getCells().get("A1").setFormula("=SEQUENCE(5,5,1,1)*SEQUENCE(5,5,1,1)");
```

Di sini kami mengalikan dua rentang spill yang identik untuk mendapatkan grid perkalian 5×5.

## Kesalahan Umum dan Cara Menghindarinya

- **Versi Excel lama**: Array dinamis (termasuk `SEQUENCE`) hanya berfungsi di Excel 365/2021+. Versi lama akan menampilkan `#NAME?`.  
- **Dukungan perpustakaan**: Tidak semua perpustakaan Excel Java mengetahui tentang rentang spill. Aspose.Cells mendukungnya; Apache POI tidak (per 2024).  
- **Format penyimpanan**: Selalu gunakan `.xlsx` untuk array dinamis; format `.xls` yang lebih lama akan menghilangkan perilaku spill.

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah program lengkap yang siap dijalankan. Cukup masukkan ke dalam proyek Maven dengan Aspose.Cells sebagai dependensi.

```java
import com.aspose.cells.*;

public class SequenceDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Set the SEQUENCE formula – this will spill into B1:C3
        sheet.getCells().get("A1").setFormula("=SEQUENCE(3,2)");

        // Force calculation so the spilled values are stored
        workbook.calculateFormula();

        // Save the workbook as an XLSX file
        workbook.save("dynamic_sequence_demo.xlsx");
        System.out.println("Workbook saved successfully at dynamic_sequence_demo.xlsx");
    }
}
```

### Output yang Diharapkan

- File `dynamic_sequence_demo.xlsx` muncul di direktori proyek Anda.  
- Membuka file tersebut di Excel menampilkan blok angka 3×2 (1‑6) yang terisi secara otomatis.

## Langkah Selanjutnya: Melampaui SEQUENCE

Sekarang Anda telah menguasai **bagaimana cara menggunakan sequence**, pertimbangkan menggabungkannya dengan fungsi dinamis lainnya:

- **FILTER** – mengekstrak baris yang memenuhi kriteria.  
- **SORT** – mengurutkan rentang spill tanpa VBA.  
- **UNIQUE** – mengambil nilai unik dari sebuah daftar.  

Semua ini dapat **menetapkan formula array dinamis** dengan cara yang sama seperti yang kami lakukan dengan `SEQUENCE`. Menggabungkannya memungkinkan Anda membangun pipeline data yang kuat langsung di dalam Excel, semuanya dikendalikan dari Java.

## Kesimpulan

Kami telah membahas semua yang perlu Anda ketahui tentang **bagaimana cara menggunakan sequence** dalam file Excel yang dihasilkan oleh Java: membuat workbook, **menetapkan formula array dinamis**, menghitung ulang, dan akhirnya **menyimpan workbook sebagai xlsx**. Kode lengkap, penjelasan menjawab pertanyaan “mengapa” di balik setiap langkah, dan Anda telah melihat beberapa variasi praktis.

Cobalah contoh tersebut, ubah parameter, dan saksikan Excel melakukan pekerjaan berat untuk Anda. Jika Anda menemukan kejanggalan—apakah itu ketidaksesuaian versi atau keterbatasan perpustakaan—tinggalkan komentar di bawah. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Menyimpan Workbook Excel dengan Aspose.Cells untuk Java – Panduan Lengkap](/cells/english/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)
- [Cara Memuat dan Menyimpan Excel sebagai CSV Menggunakan Aspose.Cells untuk Java&#58; Panduan Komprehensif](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Aspose.Cells Java&#58; Cara Menambahkan XML Maps dan Menyimpan sebagai XLSX (Panduan 2023)](/cells/english/java/import-export/aspose-cells-java-add-xml-map-save-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}