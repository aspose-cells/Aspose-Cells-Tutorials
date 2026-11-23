---
category: general
date: 2026-11-22
description: Pelajari cara mengatur locale di workbook Java, mengubah bahasa workbook,
  dan mengatur kalender ke bahasa Jepang dengan contoh kode yang jelas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: id
lastmod: 2026-11-22
og_description: Bagaimana cara mengatur locale di workbook Java dengan cepat. Ikuti
  tutorial ini untuk mengubah bahasa workbook, mengatur locale ke bahasa Jepang, dan
  mengonfigurasi kalender Jepang.
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: Cara mengatur locale di workbook Java – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  headline: How to set locale in a Java workbook using Aspose.Cells
  type: TechArticle
- description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  name: How to set locale in a Java workbook using Aspose.Cells
  steps:
  - name: Run the **FullLocaleExample** class.
    text: Run the **FullLocaleExample** class.
  - name: Open the generated `FullJapaneseLocale.xlsx` in Excel.
    text: Open the generated `FullJapaneseLocale.xlsx` in Excel.
  - name: 'Verify that:'
    text: 'Verify that:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Internationalization
- Workbook
title: Cara mengatur locale di workbook Java menggunakan Aspose.Cells
url: /id/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengatur locale di workbook Java menggunakan Aspose.Cells

Mengatur locale di workbook Java adalah kebutuhan umum ketika Anda perlu menyesuaikan spreadsheet Anda ke berbagai wilayah. Dalam panduan ini Anda akan belajar cara mengatur locale, mengubah bahasa workbook, dan mengatur kalender ke bahasa Jepang menggunakan API Aspose.Cells.

Internasionalisasi workbook melampaui penerjemahan teks; hal ini juga memengaruhi format angka, parsing tanggal, dan sistem kalender default. Pada akhir tutorial ini Anda akan dapat:

* Mengonfigurasi locale workbook ke Japanese (Japan) – **set locale to japanese**.  
* Mengubah bahasa workbook sehingga formula dan string UI menghormati budaya target – **change workbook language**.  
* Mengganti kalender ke kalender kekaisaran Jepang – **how to set calendar**.  

Langkah-langkah ini bekerja dengan versi terbaru Aspose.Cells untuk Java (v23.9 atau lebih baru) dan hanya memerlukan lingkungan pengembangan Java standar.

## Prasyarat

| Persyaratan | Alasan |
|-------------|--------|
| Java 8 atau lebih tinggi | Perpustakaan menargetkan Java 8+. |
| Aspose.Cells for Java (v23.9+) | Menyediakan `Workbook`, `WorkbookSettings`, dan utilitas locale. |
| IDE (IntelliJ IDEA, Eclipse, atau VS Code) | Untuk mengompilasi dan menjalankan contoh. |
| Pengetahuan dasar tentang Java | Diperlukan untuk memahami potongan kode. |

Tambahkan dependensi Aspose.Cells Maven ke `pom.xml` Anda (atau unduh JAR secara manual):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## Cara mengatur locale dan kalender dalam workbook

Langkah pertama adalah membuat instance workbook dan mendapatkan objek settings-nya. Objek settings menyediakan API locale dan kalender.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import java.util.Locale;
import java.util.Calendar;

public class WorkbookLocaleDemo {
    public static void main(String[] args) {
        // Step 1: Create a new workbook (empty by default)
        Workbook workbook = new Workbook();

        // Step 2: Access the workbook's settings
        WorkbookSettings settings = workbook.getSettings();

        // Step 3: Set the calendar to the Japanese calendar
        // Aspose.Cells uses java.util.Calendar; the Japanese calendar is available via Calendar.JAPANESE
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // Step 4: Set the locale to Japanese (Japan)
        // This influences number formats, date formats, and built‑in function behaviour.
        settings.setLocale(new Locale("ja", "JP"));

        // Optional: Save the workbook to verify the settings
        workbook.save("LocaleDemo.xlsx");
    }
}
```

### Mengapa setiap baris penting

* **`new Workbook()`** – Membuat instance workbook kosong yang dapat Anda manipulasi sebelum disimpan.  
* **`getSettings()`** – Mengembalikan objek `WorkbookSettings`; semua opsi regional berada di sini.  
* **`setCalendar(...)`** – Mengganti kalender Gregorian default dengan kalender kekaisaran Jepang, memengaruhi cara tanggal ditampilkan dan diparse.  
* **`setLocale(new Locale("ja","JP"))`** – Mengubah bahasa dan konvensi regional (mis., bulan, pemisah desimal). Ini adalah inti dari **how to set locale** untuk workbook.  

Menjalankan program akan membuat `LocaleDemo.xlsx`. Buka file tersebut di Excel atau LibreOffice dan Anda akan melihat nama bulan dalam bahasa Jepang, simbol mata uang Yen Jepang, serta tanggal yang diformat sesuai kalender Jepang.

## Ubah bahasa workbook (set locale ke Japanese)

Jika tujuan utama Anda adalah **mengubah bahasa workbook**, Anda dapat fokus pada pemanggilan `setLocale` saja. Potongan kode berikut mengisolasi langkah tersebut:

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**Apa yang berubah?**  
* String format sel beralih ke bahasa Jepang (mis., `#,##0.00` menjadi `#,##0.00` dengan simbol yen).  
* Nama fungsi bawaan (seperti `SUM`) tetap dalam bahasa Inggris karena locale fungsi Excel bersifat independen, namun string tanggal dan pesan error mengikuti konvensi Jepang.  

**Kapan menggunakan ini?**  
* Ketika Anda membutuhkan spreadsheet yang menampilkan angka dan tanggal untuk audiens Jepang tetapi kalender dasarnya tetap Gregorian.  
* Untuk laporan yang diekspor ke PDF atau dicetak, memastikan bahasa visual sesuai dengan pasar target.

## Cara mengatur kalender ke kalender Jepang

Kadang-kadang kebutuhan **how to set calendar** terpisah dari locale. Untuk sistem legacy yang menyimpan tanggal dalam era kekaisaran Jepang, Anda harus secara eksplisit mengatur kalender sambil tetap mempertahankan locale default secara opsional.

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Set only the calendar; keep the default (US) locale
settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

// Verify the calendar by creating a date cell
int row = 0, column = 0;
workbook.getWorksheets().get(0).getCells().putValue(row, column, new java.util.Date());

// Save to see the Japanese era (e.g., "R3/04/01" for Reiwa 3)
workbook.save("JapaneseCalendar.xlsx");
```

**Poin penting:**

* `Calendar.getInstance(Locale.JAPAN)` mengembalikan `java.util.Calendar` yang dikonfigurasi untuk era Jepang.  
* Workbook kini akan menampilkan tanggal menggunakan simbol era (R untuk Reiwa, H untuk Heisei, dll.).  
* Pengaturan ini **tidak** memengaruhi format angka atau bahasa UI; gabungkan dengan `setLocale` jika Anda memerlukan keduanya.

## Contoh lengkap end‑to‑end

Berikut adalah program lengkap yang dapat dijalankan yang menunjukkan **how to set locale**, **change workbook language**, dan **set the calendar** dalam satu alur terpadu. Program ini juga menambahkan sel contoh untuk mengilustrasikan efeknya.

```java
import com.aspose.cells.*;
import java.util.*;

public class FullLocaleExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 1️⃣ Set the locale to Japanese (Japan) – changes language & number formats
        settings.setLocale(new Locale("ja", "JP"));

        // 2️⃣ Set the calendar to the Japanese imperial calendar
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // 3️⃣ Add a sample date and number to visualize the changes
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Date cell – will show Japanese era after applying the calendar
        cells.putValue(0, 0, new Date());

        // Number cell – will use Japanese Yen symbol and comma separator
        cells.putValue(1, 0, 1234567.89);

        // Apply a style to the number cell for currency formatting
        Style style = cells.getRows().get(1).getStyle();
        style.setNumber(3); // Built‑in currency format
        cells.getRows().get(1).setStyle(style);

        // Save the workbook
        workbook.save("FullJapaneseLocale.xlsx");
        System.out.println("Workbook created with Japanese locale and calendar.");
    }
}
```

**Output yang diharapkan:**  
Membuka `FullJapaneseLocale.xlsx` menampilkan sel pertama dengan tanggal seperti `R3/04/01` (Reiwa 3) dan sel kedua diformat sebagai `¥1,234,567.89`. Ini mengonfirmasi bahwa **how to set locale**, **change workbook language**, dan **how to set calendar** semuanya bekerja bersama.

## Kesalahan umum dan cara menghindarinya

| Kesalahan | Mengapa terjadi | Solusi |
|-----------|----------------|--------|
| Menggunakan `Locale.CHINA` alih-alih `new Locale("ja","JP")` | `Locale.CHINA` mengatur bahasa Cina, bukan Jepang. | Selalu buat `Locale` dengan `"ja", "JP"` untuk bahasa Jepang. |
| Lupa memanggil `settings.setCalendar(...)` setelah `setLocale` | Kalender default ke Gregorian, sehingga tanggal muncul di era yang salah. | Panggil `setCalendar` **setelah** mengatur locale, atau atur keduanya bersamaan seperti contoh. |
| Menyimpan workbook sebelum menerapkan pengaturan | Pengaturan diterapkan pada objek dalam memori; menyimpan terlalu awal menulis locale default. | Terapkan semua perubahan locale/kalender **sebelum** memanggil `workbook.save()`. |
| Menggunakan versi Aspose.Cells yang usang | Versi lama tidak memiliki overload `setCalendar`. | Upgrade ke v23.9+ atau periksa catatan rilis untuk dukungan locale. |

## Menguji konfigurasi Anda

1. Jalankan kelas **FullLocaleExample**.  
2. Buka `FullJapaneseLocale.xlsx` yang dihasilkan di Excel.  
3. Verifikasi bahwa:  
   * Kolom tanggal menampilkan simbol era Jepang (`R`, `H`, dll.).  
   * Kolom angka menggunakan simbol Yen dan pemisah koma.  
   * Semua pesan error bawaan (mis., `#DIV/0!`) muncul dalam bahasa Jepang jika workbook berisi error.  

Jika salah satu pemeriksaan ini gagal, periksa kembali bahwa objek `WorkbookSettings` yang Anda modifikasi adalah instance yang sama yang digunakan saat menyimpan.

## Langkah Selanjutnya

* **Localize formulas** – Meskipun locale mengontrol format, Anda juga dapat menerjemahkan nama fungsi kustom menggunakan `FormulaParser`.  
* **Apply locale to existing workbooks** – Muat workbook dengan `new Workbook`

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Format Tanggal Aspose Cells: Cara Mengatur Format Tanggal Kustom di Java](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [Cara Mengatur Bahasa pada File Excel Menggunakan Aspose.Cells .NET untuk Dukungan Multibahasa](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Cara mengatur format angka sel dan mengonversi tanggal Jepang di C# menggunakan Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}