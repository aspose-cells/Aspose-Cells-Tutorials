---
category: general
date: 2026-06-08
description: Dapatkan tanggal dan waktu dari sel menggunakan Aspose.Cells Java dan
  pelajari cara menulis nilai ke sel Excel dalam beberapa langkah saja.
draft: false
keywords:
- get datetime from cell
- write value to excel cell
- Aspose.Cells Java date parsing
- Japanese era calendar Excel
- Excel formula recalculation Java
language: id
og_description: Dapatkan datetime dari sel menggunakan Aspose.Cells Java. Tutorial
  ini juga menunjukkan cara menulis nilai ke sel Excel secara efisien.
og_title: Dapatkan tanggal dan waktu dari sel di Java Excel – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  headline: Get datetime from cell in Java Excel – Complete Guide
  type: TechArticle
- description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  name: Get datetime from cell in Java Excel – Complete Guide
  steps:
  - name: What if the cell already contains a true Excel date?
    text: 'If `cell.getType()` returns `CellValueType.IS_DATE_TIME`, you can skip
      the recalculation step and read the value directly:'
  - name: How to process a whole column of era strings?
    text: 'Loop through the used range and apply the same settings once:'
  - name: Can I disable the Japanese era handling later?
    text: 'Yes—just flip the flag back:'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
title: Dapatkan tanggal dan waktu dari sel di Java Excel – Panduan Lengkap
url: /id/java/cell-operations/get-datetime-from-cell-in-java-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dapatkan datetime dari sel di Java Excel – Panduan Lengkap

Pernahkah Anda perlu **get datetime from cell** tetapi nilai terlihat seperti string era Jepang? Anda bukan satu-satunya. Di banyak spreadsheet lama tanggal disimpan sebagai “Reiwa 3/04/01”, dan mengambil `java.time.LocalDateTime` yang tepat dari itu dapat terasa seperti memecahkan pesan rahasia.  

Untungnya, Aspose.Cells for Java dapat menangani konversi untuk Anda, dan sekaligus kami akan menunjukkan cara **write value to excel cell** sehingga Anda dapat melakukan round‑trip data tanpa merusak logika sheet.

Dalam tutorial ini Anda akan belajar:

* Cara membuat workbook dan menargetkan worksheet tertentu.  
* Langkah tepat untuk mengaktifkan kalender era Jepang untuk parsing.  
* Mengapa Anda harus menghitung ulang formula sebelum membaca tanggal.  
* Cara menulis nilai baru kembali ke sel tanpa kehilangan format.  

Tanpa alat eksternal, tanpa sulap—hanya kode Java biasa yang dapat Anda masukkan ke dalam proyek Maven mana pun hari ini.

---

## Prasyarat

* **Java 8+** (contoh menggunakan API modern `java.time`).  
* **Aspose.Cells for Java** ≥ 23.9.0 – tambahkan dependensi melalui Maven atau Gradle.  
* Pemahaman dasar tentang konsep Excel (worksheets, cells, formulas).  

Jika Anda belum memiliki pustaka tersebut, dapatkan dari repositori resmi Aspose:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9.0</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Langkah 1: Buat workbook baru dan akses worksheet pertama

Untuk memulai, kita memerlukan objek `Workbook` baru. Anggap saja seperti membuka file Excel baru di memori.

```java
// Step 1: Initialize workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

*Mengapa ini penting:*  
Membuat workbook secara programatik memberi Anda kontrol penuh atas pengaturan sebelum data apa pun menyentuh sistem file. Worksheet pertama (`index 0`) adalah tempat kami akan mendemonstrasikan pembacaan dan penulisan.

---

## Langkah 2: Tulis string tanggal era Jepang ke sel A1

Sekarang kami akan **write value to excel cell** A1. Ini mencerminkan skenario dunia nyata di mana pengguna secara manual memasukkan “Reiwa 3/04/01”.

```java
// Step 2: Write the era date string into A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue("Reiwa 3/04/01"); // raw string, not yet a date
```

*Tip cepat:* `putValue` bersifat serbaguna—menerima string, angka, tanggal, bahkan formula. Ketika Anda memberikan string biasa, Aspose menyimpannya persis apa adanya, yang sempurna untuk demo kami.

---

## Langkah 3: Aktifkan kalender era Jepang untuk parsing tanggal

Secara default Aspose.Cells menggunakan kalender Gregorian. Untuk memahami “Reiwa”, kami mengaktifkan sebuah pengaturan.

```java
// Step 3: Turn on Japanese era calendar support
WorkbookSettings settings = workbook.getSettings();
settings.setUseJapaneseEraCalendar(true);
```

*Mengapa mengaktifkan ini?*  
Kalender era Jepang memetakan nama era (Reiwa, Heisei, Showa) ke padanan Gregorian mereka. Tanpa flag ini, pustaka akan memperlakukan string sebagai teks biasa, dan Anda tidak akan pernah mendapatkan objek `DateTime` yang tepat.

---

## Langkah 4: Hitung ulang formula sehingga string era dikonversi ke tanggal Gregorian

Aspose tidak secara otomatis mem-parsing string menjadi tanggal. Sebaliknya, ia memperlakukan sel sebagai hasil formula setelah satu kali perhitungan.

```java
// Step 4: Force a recalculation to convert the era string
workbook.calculateFormula(); // processes all cells, including A1
System.out.println(cell.getDateTime()); // → 2021‑04‑01
```

Ketika `calculateFormula()` dijalankan, engine mengenali pola era, menerapkan kalender Jepang, dan menyimpan tanggal Gregorian yang dihasilkan secara internal. Pemanggilan `getDateTime()` kemudian mengembalikan `java.util.Date` (atau Anda dapat mengonversinya ke `java.time`).

**Output yang diharapkan**

```
2021-04-01T00:00:00.000+00:00
```

---

## Langkah 5: Tulis nilai baru kembali ke sel yang sama (atau sel lain)

Misalkan Anda perlu menimpa string asli dengan tanggal ISO‑8601 yang bersih. Berikut cara **write value to excel cell** dengan aman, mempertahankan gaya sel.

```java
// Step 5: Overwrite A1 with a formatted date string
java.time.LocalDateTime now = java.time.LocalDateTime.now();
cell.putValue(now); // Aspose will store it as a proper Excel date
// Optional: apply a date format style
Style style = cell.getStyle();
style.setNumber(14); // built‑in "m/d/yyyy" format
cell.setStyle(style);
```

*Apa yang terjadi?*  
`putValue` mendeteksi tipe `LocalDateTime` dan mengonversinya ke representasi nomor seri Excel. Menetapkan format angka memastikan sel menampilkan tanggal persis seperti yang Anda harapkan saat dibuka di Excel.

---

## Contoh Kerja Lengkap

Menggabungkan semuanya, berikut satu kelas Java yang dapat Anda kompilasi dan jalankan. Ia membuat workbook, menulis string era, mengonversinya, dan akhirnya menyimpan file.

```java
import com.aspose.cells.*;

public class JapaneseEraDateDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first sheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ Write Japanese era date string to A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue("Reiwa 3/04/01");

        // 3️⃣ Enable Japanese era calendar
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEraCalendar(true);

        // 4️⃣ Recalculate so the string becomes a Gregorian date
        workbook.calculateFormula();
        System.out.println("Converted date: " + cell.getDateTime());

        // 5️⃣ Overwrite with a clean LocalDateTime (optional)
        java.time.LocalDateTime now = java.time.LocalDateTime.now();
        cell.putValue(now);
        Style style = cell.getStyle();
        style.setNumber(14); // m/d/yyyy
        cell.setStyle(style);

        // 6️⃣ Save the workbook
        workbook.save("output.xlsx");
        System.out.println("Workbook saved as output.xlsx");
    }
}
```

Jalankan ini dengan `java -cp aspose-cells-23.9.jar;. JapaneseEraDateDemo` dan buka **output.xlsx**. Anda akan melihat sel A1 menampilkan tanggal saat ini, sementara konsol mencatat nilai “2021‑04‑01” yang telah dikonversi.

---

## Menangani Kasus Tepi & Pertanyaan Umum

### Bagaimana jika sel sudah berisi tanggal Excel yang sebenarnya?

Jika `cell.getType()` mengembalikan `CellValueType.IS_DATE_TIME`, Anda dapat melewati langkah perhitungan ulang dan membaca nilai secara langsung:

```java
if (cell.getType() == CellValueType.IS_DATE_TIME) {
    System.out.println("Already a date: " + cell.getDateTime());
}
```

### Bagaimana cara memproses seluruh kolom string era?

Lakukan loop melalui rentang yang digunakan dan terapkan pengaturan yang sama sekali:

```java
Range used = worksheet.getCells().getMaxDisplayRange();
for (int row = 0; row < used.getRowCount(); row++) {
    Cell c = used.getCell(row, 0); // column A
    c.putValue(c.getStringValue()); // re‑assign to trigger parsing
}
workbook.calculateFormula();
```

### Bisakah saya menonaktifkan penanganan era Jepang nanti?

Ya—cukup ubah flag kembali:

```java
settings.setUseJapaneseEraCalendar(false);
```

Ingat untuk menghitung ulang lagi jika Anda mengubah pengaturan setelah menulis data.

---

## Tips Pro & Hal-hal yang Perlu Diwaspadai

* **Performance:** Mengaktifkan kalender era Jepang menambah overhead kecil. Jika Anda hanya membutuhkannya untuk beberapa sel, pertimbangkan untuk mengaktifkan pengaturan, memproses, lalu mematikannya kembali.  
* **Locale awareness:** String era harus cocok dengan pola tepat “EraName yy/MM/dd”. Salah eja “Reiwa” (misalnya, “Rewa”) akan membuat sel tetap sebagai teks biasa.  
* **Saving format:** `Workbook.save("output.xlsx")` menulis file XLSX. Gunakan `"output.xls"` jika Anda membutuhkan format biner lama, tetapi perhatikan bahwa beberapa fitur (seperti parsing era) mungkin terbatas.

---

## Kesimpulan

Anda sekarang tahu cara **get datetime from cell** ketika sumber menggunakan notasi era Jepang, dan Anda juga melihat cara bersih untuk **write value to excel cell** dengan format yang tepat. Dengan mengaktifkan `setUseJapaneseEraCalendar(true)` dan memaksa perhitungan ulang formula, Aspose.Cells menjembatani kesenjangan antara string era lama dan tanggal Gregorian modern—semua dengan beberapa baris kode Java.

Apa selanjutnya? Cobalah memperluas pola ini ke kalender budaya lain (Thai, Hijri) atau memproses batch workbook besar menggunakan pendekatan yang sama. Prinsip yang sama—aktifkan kalender yang tepat, hitung ulang, lalu baca/tulis—berlaku di seluruh situasi.

Punya format tanggal rumit yang tidak dapat Anda pecahkan? Tinggalkan komentar di bawah, dan mari kita selesaikan bersama. Selamat coding!  

![Contoh mendapatkan datetime dari sel](https://example.com/images/get-datetime-from-cell.png "Contoh mendapatkan datetime dari sel")


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Menguasai Sistem Tanggal 1904 di Excel Menggunakan Aspose.Cells Java untuk Operasi Sel yang Efektif](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Cara Mengimplementasikan Perhitungan Sel Rekursif di Aspose.Cells Java untuk Otomasi Excel yang Ditingkatkan](/cells/english/java/calculation-engine/aspose-cells-java-recursive-cell-calculations/)
- [Cara Mengonversi Nama Sel Excel ke Indeks Menggunakan Aspose.Cells untuk Java: Panduan Langkah demi Langkah](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}