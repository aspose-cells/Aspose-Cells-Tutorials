---
category: general
date: 2026-06-18
description: Mengurai tanggal era Jepang di Java menggunakan Aspose.Cells. Pelajari
  cara membaca tanggal dari sel Excel dan mengekstrak datetime dari sel Excel dengan
  cepat.
draft: false
keywords:
- parse japanese era date
- read date from excel cell
- extract datetime from excel cell
language: id
og_description: Mengurai tanggal era Jepang di Java dengan Aspose.Cells. Panduan ini
  menunjukkan cara membaca tanggal dari sel Excel dan mengekstrak datetime dari sel
  Excel dalam beberapa langkah saja.
og_title: Mengurai Tanggal Era Jepang dari Excel di Java – Tutorial Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  headline: Parse Japanese Era Date from Excel in Java – Full Guide
  type: TechArticle
- description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  name: Parse Japanese Era Date from Excel in Java – Full Guide
  steps:
  - name: Multiple Eras
    text: Japan has had several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). The `setParseDateUsingJapaneseEra(true)`
      flag covers all of them automatically, but be aware that older dates may fall
      outside the library’s supported range (typically 1868‑present). If you encounter
      a date like “昭和45年12月31日”, the sam
  - name: Blank or Invalid Cells
    text: 'If a cell is empty or contains a malformed string, `cell.getDateTime()`
      throws a `CellsException`. Guard against this with a simple check:'
  - name: Time Component
    text: The example only includes a date, but if your Excel file also stores time
      (e.g., “令和3年5月10日 14:30”), Aspose.Cells will preserve the time portion. The
      `LocalDateTime` you receive will include hours, minutes, and seconds.
  type: HowTo
tags:
- Java
- Excel
- DateTime
title: Mengurai Tanggal Era Jepang dari Excel di Java – Panduan Lengkap
url: /id/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengurai Tanggal Era Jepang dari Excel di Java – Panduan Lengkap

Pernahkah Anda perlu **parse Japanese era date** yang disimpan dalam workbook Excel tetapi tidak yakin bagaimana mengubahnya menjadi `DateTime` Gregorian biasa? Anda tidak sendirian—banyak pengembang mengalami kendala ini saat menangani lembar akuntansi Jepang lama atau formulir pemerintah. Kabar baiknya, dengan beberapa baris Java dan perpustakaan yang tepat, Anda dapat membaca tanggal dari sel Excel dan mengekstrak datetime dari sel Excel tanpa harus melakukan manipulasi string manual.

Dalam tutorial ini kami akan memandu Anda melalui contoh lengkap yang dapat dijalankan yang menunjukkan secara tepat cara **parse Japanese era date** string seperti “令和3年5月10日” menjadi `java.time.LocalDateTime` Java. Kami akan membahas dependensi Maven yang diperlukan, menjelaskan mengapa Anda harus mengaktifkan parsing yang sadar era, dan menunjukkan jebakan umum yang mungkin Anda temui. Pada akhir tutorial, Anda akan memiliki potongan kode siap produksi yang dapat Anda sisipkan ke proyek Java mana pun.

## Prasyarat

- Java 17 atau lebih baru (kode ini juga berfungsi pada Java 8+)
- Sistem build Maven atau Gradle
- Familiaritas dasar dengan file Excel
- Perpustakaan **Aspose.Cells for Java** (versi trial gratis cukup untuk pengujian)

Jika ada yang belum Anda kenal, jangan khawatir—saya akan menunjukkan secara tepat cara menambahkan perpustakaan dan memulai.

## Langkah 1: Tambahkan Aspose.Cells ke Proyek Anda

Hal pertama yang harus dilakukan: Anda memerlukan perpustakaan yang memahami tanggal era Jepang. Aspose.Cells melakukan pekerjaan berat untuk Anda.

**Maven**:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for latest version -->
</dependency>
```

**Gradle**:

```groovy
implementation 'com.aspose:aspose-cells:24.9'
```

Setelah dependensi terpasang, Anda dapat mulai menulis kode yang *reads date from Excel cell* dan *extracts datetime from Excel cell*.

## Langkah 2: Buat Workbook dan Targetkan Worksheet Pertama

Kami akan memulai dengan membuat workbook baru di memori dan mengambil sheet pertama. Ini meniru dua baris pertama dari contoh asli.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

Mengapa memulai dengan workbook baru? Hal ini menjamin lingkungan bersih di mana kami dapat mengontrol setiap pengaturan—penting ketika Anda nanti mengaktifkan parsing yang sadar era.

## Langkah 3: Masukkan String Tanggal Era Jepang ke Sel A1

Sekarang kami mensimulasikan file Excel yang sudah berisi tanggal era Jepang. Dalam praktik sebenarnya Anda mungkin akan memuat file `.xlsx` yang sudah ada, tetapi untuk ilustrasi kami akan **write** nilai tersebut sendiri.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

String tersebut mengikuti notasi standar Jepang: *Era* + *Year* + *Month* + *Day*. Tanpa konfigurasi tambahan, Aspose.Cells akan memperlakukan ini sebagai teks biasa, bukan tanggal.

## Langkah 4: Aktifkan Parsing Tanggal Era‑Aware

Berikut bagian krusial: beri tahu workbook untuk **parse Japanese era date** string ketika menemukannya. Hal ini dilakukan melalui flag `ParseDateUsingJapaneseEra`.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Mengapa ini diperlukan? Secara default Aspose.Cells mengasumsikan kalender Gregorian, sehingga “令和3年5月10日” akan tetap menjadi string. Mengaktifkan flag tersebut memberi tahu engine untuk mengonversinya menjadi `java.util.Date` (atau ekuivalen `java.time`) di belakang layar.

## Langkah 5: Dapatkan Nilai DateTime yang Diurai

Sekarang workbook sudah tahu cara menafsirkan era, kami dapat meminta sel untuk representasi `DateTime`‑nya.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

Perhatikan kami **read date from Excel cell** menggunakan `cell.getDateTime()`. Metode ini mengembalikan `java.util.Date`, yang langsung kami konversi ke `LocalDateTime` untuk keamanan tipe yang lebih baik. Ini memenuhi kebutuhan **extract datetime from excel cell** dengan cara yang bersih dan idiomatis.

## Langkah 6: Verifikasi Hasil

Akhirnya, mari cetak tanggal Gregorian untuk memastikan konversi berhasil.

```java
        // Step 6: Output the Gregorian date
        System.out.println(dateTime); // Expected output: 2021-05-10T00:00
    }
}
```

Saat Anda menjalankan program, Anda seharusnya melihat:

```
2021-05-10T00:00
```

Output tersebut membuktikan bahwa kami berhasil **parse Japanese era date**, **read date from Excel cell**, dan **extract datetime from Excel cell** dalam satu alur.

## Menangani Kasus Pinggiran Dunia Nyata

### Multiple Eras

Jepang telah memiliki beberapa era (Meiji, Taishō, Shōwa, Heisei, Reiwa). Flag `setParseDateUsingJapaneseEra(true)` mencakup semuanya secara otomatis, tetapi perlu diingat bahwa tanggal yang lebih lama mungkin berada di luar rentang yang didukung perpustakaan (biasanya 1868‑sekarang). Jika Anda menemukan tanggal seperti “昭和45年12月31日”, kode yang sama akan mengonversinya menjadi 1970‑12‑31.

### Blank or Invalid Cells

Jika sebuah sel kosong atau berisi string yang tidak sesuai format, `cell.getDateTime()` akan melempar `CellsException`. Lindungi kode Anda dengan pemeriksaan sederhana:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Time Component

Contoh ini hanya mencakup tanggal, tetapi jika file Excel Anda juga menyimpan waktu (misalnya “令和3年5月10日 14:30”), Aspose.Cells akan mempertahankan bagian waktu. `LocalDateTime` yang Anda terima akan mencakup jam, menit, dan detik.

## Contoh Kerja Penuh

Menggabungkan semuanya, berikut program lengkap yang siap disalin‑tempel:

```java
import com.aspose.cells.*;
import java.time.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Insert Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日");

        // Enable era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);

        // Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime();
        LocalDateTime dateTime = javaDate.toInstant()
                                         .atZone(ZoneId.systemDefault())
                                         .toLocalDateTime();

        // Output the Gregorian date
        System.out.println(dateTime); // 2021-05-10T00:00
    }
}
```

Simpan file ini sebagai `JapaneseEraDateParser.java`, kompilasi dengan `javac`, dan jalankan dengan `java`. Jika semuanya sudah dikonfigurasi dengan benar, Anda akan melihat tanggal Gregorian tercetak di konsol.

## Tips Pro & Kesalahan Umum

- **Pro tip:** Selalu set `setParseDateUsingJapaneseEra(true)` **before** Anda membaca nilai sel apa pun. Mengubah flag setelah membaca sel tidak akan mengonversi nilai secara retroaktif.
- **Watch out for locale:** Perpustakaan mem-parsing string era berdasarkan karakter Unicode, jadi Anda tidak perlu secara eksplisit mengatur locale Jepang.
- **Performance note:** Mengaktifkan parsing era menambah overhead yang sangat kecil. Jika Anda hanya membutuhkannya untuk beberapa sel, Anda dapat menonaktifkan flag sementara, membaca sel, lalu menonaktifkannya kembali.
- **Testing:** Gunakan trial gratis Aspose untuk memvalidasi terhadap file Excel nyata yang berisi beberapa tanggal era. Ini memastikan kode produksi Anda berperilaku sebagaimana mestinya.

## Kesimpulan

Kami baru saja mendemonstrasikan cara **parse Japanese era date** langsung dari workbook Excel menggunakan Java dan Aspose.Cells. Dengan mengaktifkan parsing yang sadar era, Anda dapat **read date from Excel cell** dan **extract datetime from Excel cell** secara bersih dan type‑safe. Pendekatan ini bekerja untuk semua era Jepang modern, menangani komponen waktu, dan menangani data tidak valid dengan elegan.

Siap untuk tantangan berikutnya? Cobalah memuat file `.xlsx` nyata yang berisi campuran tanggal Gregorian dan tanggal era Jepang, atau bereksperimen dengan memformat `LocalDateTime` yang dihasilkan menjadi string yang sesuai dengan locale Anda. Anda juga dapat mengeksplorasi menulis kembali tanggal yang telah dikonversi ke Excel untuk sistem hilir yang hanya memahami tanggal Gregorian.

Ada pertanyaan atau menemukan kasus pinggiran yang unik? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Menguasai Sistem Tanggal 1904 di Excel Menggunakan Aspose.Cells Java untuk Operasi Sel yang Efektif](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Mengonversi Excel ke PDF secara Efisien dengan Format Tanggal Kustom Menggunakan Aspose.Cells untuk Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Cara Memilih Rentang Sel di Excel Menggunakan Aspose.Cells untuk Java (Panduan 2023)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}