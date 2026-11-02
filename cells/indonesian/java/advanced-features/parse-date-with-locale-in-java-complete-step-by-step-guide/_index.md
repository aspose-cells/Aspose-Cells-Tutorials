---
category: general
date: 2026-07-03
description: Mengurai tanggal dengan locale menggunakan API java.time Java. Pelajari
  penanganan format era Jepang, konversi tanggal locale, dan teknik parsing tanggal
  Java yang kuat.
draft: false
keywords:
- parse date with locale
- java date parsing
- japanese era format
- locale date conversion
- java time API
language: id
og_description: Mengurai tanggal dengan locale di Java menggunakan API java.time.
  Panduan ini menunjukkan penanganan format era Jepang, konversi tanggal locale, dan
  praktik terbaik untuk penguraian tanggal yang andal.
og_title: Mengurai Tanggal dengan Locale di Java – Tutorial Pemrograman Lengkap
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Parse date with locale using Java’s java.time API. Learn Japanese era
    format handling, locale date conversion, and robust java date parsing techniques.
  headline: Parse Date with Locale in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Parse date with locale using Java’s java.time API. Learn Japanese era
    format handling, locale date conversion, and robust java date parsing techniques.
  name: Parse Date with Locale in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Define the Era Date String
    text: First, store the Japanese era string exactly as you receive it (e.g., from
      a CSV file or UI).
  - name: Build a Locale‑Aware Formatter
    text: Java’s **java.time API** lets you tie a `DateTimeFormatter` to a specific
      chronology (calendar system) and `Locale`. For the Japanese era we use `JapaneseChronology`.
  - name: Parse and Convert to Gregorian `LocalDate`
    text: Now we actually parse the string and transform the result into a classic
      `LocalDate` that any Java library can consume.
  - name: What if the input uses a different era symbol?
    text: Japanese eras change roughly every few decades. The formatter automatically
      recognises `M` (Meiji), `T` (Taisho), `S` (Showa), `H` (Heisei), and `R` (Reiwa).
      If you receive an older era not covered by the default `JapaneseChronology`,
      you’ll get a `DateTimeParseException`. In that case, verify the s
  - name: How to support other non‑Gregorian calendars?
    text: 'The pattern is identical; you just swap the chronology and locale. For
      example, Thai Buddhist dates (`BuddhistChronology`) look like this:'
  - name: Can I parse without an era symbol (pure year‑month‑day)?
    text: Yes—simply omit `G` from the pattern and use the default `ISO_LOCAL_DATE`
      formatter. That’s the classic *java date parsing* route for Gregorian strings.
  - name: What about lenient parsing (e.g., missing leading zeros)?
    text: Switch `ResolverStyle.STRICT` to `ResolverStyle.LENIENT`. Be aware that
      lenient mode may silently roll over invalid dates (e.g., `R5/13/40` becomes
      `2024‑02‑09`). For production code, strict mode is usually safer.
  type: HowTo
tags:
- java
- date-time
- localization
title: Mengurai Tanggal dengan Locale di Java – Panduan Lengkap Langkah demi Langkah
url: /id/java/advanced-features/parse-date-with-locale-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengurai Tanggal dengan Locale di Java – Panduan Lengkap Langkah‑per‑Langkah

Pernahkah Anda perlu **mengurai tanggal dengan locale** di Java tetapi tidak yakin kelas mana yang harus digunakan? Anda tidak sendirian—menghadapi kalender non‑Gregorian atau format regional dapat terasa seperti memecahkan bahasa rahasia. Dalam tutorial ini kami akan membahas contoh dunia nyata: mengubah string era Jepang seperti `R5/04/01` menjadi objek `Date` Gregorian standar `2023‑04‑01`. Pada akhir tutorial Anda akan memiliki pola yang dapat digunakan kembali untuk format tanggal spesifik locale apa pun.

Kami akan membahas semuanya mulai dari impor yang diperlukan hingga penanganan kasus tepi, dan kami akan menambahkan beberapa konsep terkait—*java date parsing*, *japanese era format*, *locale date conversion*, dan *java time API* modern—sehingga Anda dapat menyesuaikan solusi ini untuk proyek Anda sendiri. Tanpa pustaka eksternal, hanya Java 8+ biasa.

---

## Apa yang Dibahas dalam Tutorial Ini

- Menyiapkan string format **Japanese era** (`Reiwa`).
- Menggunakan `DateTimeFormatter` dengan `JapaneseChronology` dan `Locale`.
- Mengonversi `JapaneseDate` yang dihasilkan menjadi `LocalDate` (Gregorian).
- Mencetak tanggal ISO‑8601 akhir.
- Kesulitan umum seperti era yang tidak didukung atau pola yang tidak cocok.
- Variasi cepat untuk locale lain (Thai Buddhist, Islamic, dll.).

**Prasyarat**  
JDK 8 atau lebih baru, pemahaman dasar tentang `java.time`, serta IDE atau CLI untuk menjalankan kode Java. Itu saja—tanpa dependensi Maven tambahan.

---

## Mengurai Tanggal dengan Locale – Langkah‑per‑Langkah

Di bawah ini kami membagi solusi menjadi tiga langkah alami. Setiap langkah mencakup kode tepat yang Anda butuhkan, penjelasan singkat tentang *mengapa* itu penting, dan tip yang mungkin tidak Anda temukan di dokumentasi resmi.

### Langkah 1: Definisikan String Tanggal Era

Pertama, simpan string era Jepang persis seperti yang Anda terima (misalnya, dari file CSV atau UI).

```java
// Step 1: Define a date string using the Japanese era format (Reiwa 5)
String eraDateString = "R5/04/01";
```

> **Mengapa ini penting:**  
> Huruf `R` di depan mewakili *Reiwa*, era Jepang saat ini. Jika Anda mengabaikan penanda era, parser akan mengasumsikan kalender Gregorian dan menghasilkan tahun yang salah.

### Langkah 2: Bangun Formatter yang Sadar Locale

API **java.time** Java memungkinkan Anda mengaitkan `DateTimeFormatter` dengan kronologi (sistem kalender) dan `Locale` tertentu. Untuk era Jepang kami menggunakan `JapaneseChronology`.

```java
import java.time.chrono.JapaneseChronology;
import java.time.format.DateTimeFormatter;
import java.time.format.ResolverStyle;
import java.util.Locale;

// Step 2: Create a formatter that understands the Japanese era pattern
DateTimeFormatter japaneseFormatter = new DateTimeFormatterBuilder()
        .parseCaseInsensitive()
        .appendPattern("Gyy/MM/dd")          // G = era symbol, yy = year-of-era
        .toFormatter(Locale.JAPAN)           // Locale for Japanese symbols
        .withChronology(JapaneseChronology.INSTANCE)
        .withResolverStyle(ResolverStyle.STRICT);
```

**Poin utama**  
- `G` mengurai teks era (`R` untuk Reiwa, `H` untuk Heisei, dll.).  
- `ResolverStyle.STRICT` memaksa parser menolak tanggal yang tidak mungkin seperti `R0/13/32`.  
- Menetapkan `Locale` ke `Locale.JAPAN` memastikan simbol era sesuai dengan konvensi Jepang.

> **Tip pro:** Jika Anda perlu mendukung *beberapa* format era (mis., `HEISEI` ditulis lengkap), tambahkan `.parseCaseInsensitive()` seperti yang ditunjukkan, dan perpanjang pola menjadi `Guuuu` untuk nama lengkap.

### Langkah 3: Mengurai dan Mengonversi ke `LocalDate` Gregorian

Sekarang kita benar‑benarnya mengurai string dan mengubah hasilnya menjadi `LocalDate` klasik yang dapat dipakai oleh pustaka Java mana pun.

```java
import java.time.LocalDate;
import java.time.chrono.JapaneseDate;

// Step 3: Parse the era string and convert to Gregorian LocalDate
JapaneseDate japaneseDate = JapaneseDate.from(japaneseFormatter.parse(eraDateString));
LocalDate gregorianDate = LocalDate.from(japaneseDate);

// Verify the conversion
System.out.println(gregorianDate);   // Expected output: 2023-04-01
```

**Penjelasan**  
`JapaneseDate.from(...)` membuat objek tanggal yang berakar pada kalender Jepang. Dengan memanggil `LocalDate.from(...)` kami menghilangkan informasi era dan memperoleh tanggal ISO‑8601 yang setara—sempurna untuk penyimpanan, perbandingan, atau panggilan API.

> **Mengapa mengonversi?** Sebagian besar basis data, layanan REST, dan pustaka pihak ketiga mengharapkan tanggal Gregorian. Menjaga konversi di dalam rutin penguraian Anda mencegah bug halus di kemudian hari.

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut satu kelas Java yang siap dijalankan. Silakan salin‑tempel ke `ParseDateWithLocale.java` dan jalankan.

```java
import java.time.LocalDate;
import java.time.chrono.JapaneseChronology;
import java.time.chrono.JapaneseDate;
import java.time.format.DateTimeFormatter;
import java.time.format.DateTimeFormatterBuilder;
import java.time.format.ResolverStyle;
import java.util.Locale;

public class ParseDateWithLocale {

    public static void main(String[] args) {
        // --- Step 1: Input ---
        String eraDateString = "R5/04/01";

        // --- Step 2: Formatter ---
        DateTimeFormatter japaneseFormatter = new DateTimeFormatterBuilder()
                .parseCaseInsensitive()
                .appendPattern("Gyy/MM/dd")
                .toFormatter(Locale.JAPAN)
                .withChronology(JapaneseChronology.INSTANCE)
                .withResolverStyle(ResolverStyle.STRICT);

        // --- Step 3: Parse & Convert ---
        JapaneseDate japaneseDate = JapaneseDate.from(japaneseFormatter.parse(eraDateString));
        LocalDate gregorianDate = LocalDate.from(japaneseDate);

        // Output
        System.out.println("Original era string: " + eraDateString);
        System.out.println("Converted Gregorian date: " + gregorianDate);
    }
}
```

**Expected console output**

```
Original era string: R5/04/01
Converted Gregorian date: 2023-04-01
```

Jalankan program dengan `javac ParseDateWithLocale.java && java ParseDateWithLocale`. Jika Anda melihat dua baris di atas, Anda telah berhasil **mengurai tanggal dengan locale**.

---

## Menangani Kasus Tepi & Pertanyaan Umum

### Bagaimana jika input menggunakan simbol era yang berbeda?

Era Jepang berubah kira‑kira setiap beberapa dekade. Formatter secara otomatis mengenali `M` (Meiji), `T` (Taisho), `S` (Showa), `H` (Heisei), dan `R` (Reiwa). Jika Anda menerima era yang lebih lama yang tidak tercakup oleh `JapaneseChronology` default, Anda akan mendapatkan `DateTimeParseException`. Dalam kasus tersebut, verifikasi data sumber atau sediakan pemetaan khusus.

### Bagaimana cara mendukung kalender non‑Gregorian lainnya?

Pola identik; Anda hanya perlu menukar kronologi dan locale. Misalnya, tanggal Thai Buddhist (`BuddhistChronology`) terlihat seperti ini:

```java
DateTimeFormatter thaiFormatter = new DateTimeFormatterBuilder()
        .appendPattern("Gyy/MM/dd")
        .toFormatter(new Locale("th", "TH"))
        .withChronology(java.time.chrono.ThaiBuddhistChronology.INSTANCE);
```

### Bisakah saya mengurai tanpa simbol era (hanya tahun‑bulan‑hari)?

Ya—cukup hapus `G` dari pola dan gunakan formatter default `ISO_LOCAL_DATE`. Itu adalah jalur *java date parsing* klasik untuk string Gregorian.

### Bagaimana dengan parsing lenient (mis., angka nol di depan hilang)?

Ubah `ResolverStyle.STRICT` menjadi `ResolverStyle.LENIENT`. Perlu diingat bahwa mode lenient dapat secara diam-diam mengubah tanggal tidak valid (mis., `R5/13/40` menjadi `2024‑02‑09`). Untuk kode produksi, mode strict biasanya lebih aman.

---

## Tips Pro untuk Konversi Tanggal Locale yang Kuat

1. **Cache formatter** – Membuat `DateTimeFormatter` relatif murah, tetapi jika Anda mengurai ribuan tanggal per detik, simpan dalam field static final.  
2. **Validasi panjang input** – Pemeriksaan cepat `if (eraDateString.length() != 8)` dapat menghindari pengecualian parsing yang tidak perlu.  
3. **Log string asli** – Saat men-debug masalah locale, input mentah sering mengungkap karakter tak terlihat (spasi nol‑lebar) yang merusak parser.  
4. **Uji unit setiap era** – Tulis tes JUnit untuk `R`, `H`, `S`, dll., untuk memastikan pembaruan Java di masa depan tidak mengubah pemetaan.

---

## Kesimpulan

Kami baru saja mendemonstrasikan cara **mengurai tanggal dengan locale** di Java dengan memanfaatkan *java time API* modern, `DateTimeFormatter` yang sadar locale, dan `JapaneseChronology`. Contoh lengkap menunjukkan seluruh alur—dari string era Jepang mentah hingga `LocalDate` Gregorian yang bersih—dan memberi Anda pengetahuan untuk menyesuaikan pola ini untuk kalender lain, seperti sistem Thai Buddhist atau Islamic.

Langkah selanjutnya? Coba ganti `JapaneseChronology` dengan `ThaiBuddhistChronology` atau `HijrahChronology` dan lihat bagaimana struktur kode yang sama menangani kalender budaya yang sepenuhnya berbeda. Anda juga dapat menjelajahi pemformatan `LocalDate` yang dihasilkan kembali menjadi string spesifik locale menggunakan `DateTimeFormatter.ofLocalizedDate(FormatStyle.FULL)`.

Memiliki locale yang rumit atau kesalahan parsing yang tidak terduga? Tinggalkan komentar di bawah, dan mari kita selesaikan bersama. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Mastering Data Presentation in Excel: Number and Custom Date Formatting with Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Efficiently Convert Excel to PDF with Custom Date Formats Using Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Master the 1904 Date System in Excel Using Aspose.Cells Java for Effective Cell Operations](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}