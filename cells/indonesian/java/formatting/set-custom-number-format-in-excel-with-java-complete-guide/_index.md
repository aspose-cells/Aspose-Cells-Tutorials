---
category: general
date: 2026-06-30
description: Atur format angka khusus di Excel menggunakan Java. Pelajari cara membuat
  workbook Excel dengan Java, mengambil tanggal‑waktu dari sel, menghitung formula
  workbook, dan menghasilkan nilai tanggal‑waktu.
draft: false
keywords:
- set custom number format
- get datetime from cell
- create excel workbook java
- calculate workbook formulas
- output datetime value
language: id
og_description: Tetapkan format angka khusus di Excel menggunakan Java. Panduan ini
  menunjukkan cara membuat workbook Excel dengan Java, mengambil tanggal‑waktu dari
  sel, menghitung rumus workbook, dan mengeluarkan nilai tanggal‑waktu.
og_title: Atur Format Angka Kustom di Excel dengan Java – Tutorial Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  headline: Set Custom Number Format in Excel with Java – Complete Guide
  type: TechArticle
- description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  name: Set Custom Number Format in Excel with Java – Complete Guide
  steps:
  - name: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
    text: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
  - name: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
    text: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
  - name: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
    text: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DateTime
title: Atur Format Angka Kustom di Excel dengan Java – Panduan Lengkap
url: /id/java/formatting/set-custom-number-format-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengatur Format Angka Kustom di Excel dengan Java – Panduan Lengkap

Pernahkah Anda perlu **mengatur format angka kustom** di lembar Excel saat bekerja dengan Java? Anda tidak sendirian. Baik Anda sedang membangun mesin pelaporan atau hanya mencoba menampilkan tanggal era Jepang dengan benar, menguasai trik ini menghemat berjam‑jam waktu pasca‑pemrosesan. Dalam tutorial ini kami akan membahas contoh dunia nyata yang **membuat workbook Excel Java**, menerapkan format khusus berdasarkan locale, menghitung ulang formula, dan akhirnya **mengambil DateTime dari sel** untuk **mengoutput nilai datetime**.

Kami akan menggunakan pustaka Aspose.Cells untuk Java yang populer karena menangani format angka dan tanggal yang sensitif budaya secara langsung. Pada akhir panduan Anda akan memiliki program mandiri yang dapat dijalankan dan dapat dimasukkan ke proyek Maven atau Gradle mana pun. Tanpa jalan pintas “lihat dokumen”—hanya kode solid dan penjelasan yang jelas.

---

## Apa yang Akan Anda Pelajari

- Cara **membuat Excel workbook Java** secara programatik.
- Langkah tepat untuk **mengatur format angka kustom** bagi tanggal era Jepang.
- Mengapa memanggil **calculate workbook formulas** penting sebelum mengekstrak nilai.
- Cara yang tepat untuk **mengambil datetime dari sel** dan **mengoutput nilai datetime**.
- Jebakan umum (locale yang hilang, formula usang) dan solusi cepatnya.

---

## Prasyarat

- Java 8 atau lebih baru terpasang di mesin Anda.  
- Aspose.Cells untuk Java 23.11 (atau versi terbaru apa pun).  
- IDE atau editor teks dasar—IntelliJ IDEA, Eclipse, VS Code, apa saja yang Anda suka.  

Jika Anda belum menambahkan Aspose.Cells ke proyek Anda, tempelkan cuplikan Maven berikut ke dalam `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.11</version>
</dependency>
```

Pengguna Gradle dapat menambahkan:

```gradle
implementation 'com.aspose:aspose-cells:23.11'
```

Setelah lingkungan siap, mari masuk ke kode.

---

## Langkah 1: Mengatur Format Angka Kustom – Gambaran Umum

Sebelum menulis kode Java apa pun, ada baiknya memvisualisasikan apa yang kita inginkan. Bayangkan sebuah sel Excel yang harus menampilkan **“令和2年4月1日”** alih‑alih string ISO‑8601 “2020‑04‑01”. Nilai dasarnya tetap tanggal sesungguhnya (sehingga formula tetap berfungsi), tetapi *tampilan* mengikuti format era Jepang. Inilah yang dilakukan operasi **set custom number format**.

Di bawah ini adalah file sumber lengkap. Silakan salin‑tempel ke `src/main/java/SetCustomNumberFormatDemo.java`.

```java
// File: SetCustomNumberFormatDemo.java
import com.aspose.cells.*;

public class SetCustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Create Excel workbook Java – a fresh workbook
        // -------------------------------------------------
        Workbook workbook = new Workbook();               // in‑memory workbook, no file yet

        // -------------------------------------------------
        // 2️⃣ Access the first worksheet
        // -------------------------------------------------
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // -------------------------------------------------
        // 3️⃣ Retrieve cell A1 where we’ll store the date string
        // -------------------------------------------------
        Cell cellA1 = worksheet.getCells().get("A1");

        // -------------------------------------------------
        // 4️⃣ Insert a Japanese era date string (Reiwa 2‑04‑01)
        // -------------------------------------------------
        // Note: Aspose.Cells will treat this as a text value until we recalc.
        cellA1.putValue("R02-04-01");

        // -------------------------------------------------
        // 5️⃣ Apply the custom number format (our primary goal)
        // -------------------------------------------------
        // [$-ja-JP] tells Excel to use the Japanese locale.
        // ggge年m月d日 renders as "令和2年4月1日".
        cellA1.setNumberFormat("[$-ja-JP]ggge年m月d日");

        // -------------------------------------------------
        // 6️⃣ Calculate workbook formulas – crucial step!
        // -------------------------------------------------
        // Without this, the cell remains a plain string and the
        // DateTime conversion below will fail.
        workbook.calculateFormula();

        // -------------------------------------------------
        // 7️⃣ Get DateTime from cell – now the value is a true date
        // -------------------------------------------------
        // The getDateTime() method returns a java.util.Calendar instance.
        java.util.Calendar dt = cellA1.getDateTime();

        // -------------------------------------------------
        // 8️⃣ Output datetime value – see the result in console
        // -------------------------------------------------
        System.out.println("Converted DateTime: " + dt.getTime()); // → Tue Apr 01 00:00:00 UTC 2020
    }
}
```

### Mengapa Ini Berhasil

- **`setNumberFormat`** memberi tahu Excel bagaimana *menampilkan* nilai numerik yang mendasarinya. String format `[$-ja-JP]ggge年m月d日` adalah kuncinya; `ggg` memilih nama era, `e` tahun dalam era, diikuti oleh bulan dan hari sebagai literal.
- **`calculateFormula`** memaksa Aspose.Cells menafsirkan teks “R02-04-01” sebagai tanggal berdasarkan kalender Jepang. Melewatkan langkah ini membuat sel tetap berupa teks biasa, dan `getDateTime()` akan melempar pengecualian.
- **`getDateTime`** akhirnya mengekstrak objek `java.util.Calendar` yang *nyata*, yang dapat Anda manipulasi, format, atau simpan di tempat lain.

---

## Langkah 2: Membuat Excel Workbook Java – Penjelasan Lebih Dalam

Saat Anda **create Excel workbook Java**, Anda tidak hanya mengalokasikan memori; Anda juga menetapkan gaya default, lembar kerja default, dan budaya default (biasanya locale sistem). Jika Anda memerlukan locale default yang berbeda, Anda dapat melewatkan objek `LoadOptions`:

```java
LoadOptions opts = new LoadOptions(LoadFormat.XLSX);
opts.setLocale(new java.util.Locale("ja", "JP"));
Workbook workbook = new Workbook(opts);
```

Untuk kebanyakan skenario konstruktor sederhana sudah cukup, tetapi bagus untuk mengetahui alternatifnya—terutama ketika Anda menangani banyak locale dalam satu aplikasi.

*Tips profesional:* Selalu pertahankan workbook di memori sampai selesai memformat. Menulis ke disk setelah setiap perubahan menimbulkan overhead I/O yang tidak perlu.

---

## Langkah 3: Mengambil DateTime dari Sel – Menangani Hasil

Baris `java.util.Calendar dt = cellA1.getDateTime();` melakukan pekerjaan berat. Di balik layar Aspose.Cells mengonversi nomor seri internal (jumlah hari sejak 31‑12‑1899) menjadi sebuah `Calendar`. Konversi ini menghormati locale workbook, sehingga Anda mendapatkan tanggal Gregorian yang tepat meskipun tampilan menggunakan era Jepang.

Jika Anda memerlukan `java.time.LocalDate` (API yang lebih baru), konversi seperti ini:

```java
java.time.LocalDate localDate = dt.toInstant()
        .atZone(java.time.ZoneId.systemDefault())
        .toLocalDate();
System.out.println("LocalDate: " + localDate); // 2020-04-01
```

Itu memenuhi kebutuhan **output datetime value** sambil tetap modern.

---

## Langkah 4: Menghitung Formula Workbook – Saat Penting

Anda mungkin bertanya: *“Apakah saya benar‑benar harus memanggil `calculateFormula()`?”* Jawabannya ya, kecuali Anda memberi sel objek `Date` Java native sejak awal. Saat Anda **set custom number format** pada string teks, Excel (dan Aspose.Cells) memperlakukannya sebagai ekspresi mirip formula yang perlu dievaluasi. Tanpa perhitungan ulang, `getDateTime()` akan mengembalikan nilai default `1900‑01‑00` atau melempar `CellValueException`.

Jika workbook Anda sudah berisi formula kompleks yang merujuk ke sel yang baru diformat, panggil `calculateFormula()` *sekali* setelah semua perubahan. Pemanggilan berulang mahal biayanya.

---

## Langkah 5: Mengoutput Nilai DateTime – Memverifikasi Hasil

Menjalankan demo akan mencetak sesuatu seperti:

```
Converted DateTime: Tue Apr 01 00:00:00 UTC 2020
```

Baris itu mengonfirmasi tiga hal:

1. **set custom number format** telah diterapkan (Anda dapat membuka file `.xlsx` yang dihasilkan di Excel untuk melihat “令和2年4月1日”).
2. Langkah **calculate workbook formulas** berhasil, mengubah string era menjadi tanggal nyata.
3. Panggilan **get datetime from cell** mengembalikan `Calendar` yang tepat, yang kemudian kami **output datetime value** ke konsol.

Jika Anda membuka workbook dengan program spreadsheet, Anda akan melihat teks yang diformat, tetapi nilai sel yang mendasarinya tetap nomor seri `43831` (representasi Excel untuk 2020‑04‑01). Dualitas ini yang membuat Excel begitu kuat.

---

## Jebakan Umum & Kasus Edge

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| `cellA1.getDateTime()` melempar `CellValueException` | Sel masih berupa string karena `calculateFormula()` tidak dipanggil. | Selalu panggil `workbook.calculateFormula()` setelah mengatur tanggal teks yang perlu konversi. |
| Era Jepang tidak ditampilkan dengan benar | Kode locale hilang atau salah. | Gunakan `[$-ja-JP]` dalam string format, atau set locale workbook lewat `LoadOptions`. |
| Format menampilkan “#VALUE!” di Excel | String format rusak. | Periksa kembali tanda kurung dan karakter; pola `ggge年m月d日` wajib untuk tahun era. |
| Komponen waktu muncul (misalnya “00:00:00”) | String sumber menyertakan waktu atau gaya sel menambahnya. | Potong string sumber atau sesuaikan format menjadi `ggge年m月d日;@`. |

---

## Contoh Kerja Penuh – Jalankan Sekali Klik

Jika Anda lebih suka satu file tanpa komentar tambahan, berikut versi minimalnya:



## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Membuat Workbook Excel menggunakan Aspose.Cells di Java: Panduan Langkah‑demi‑Langkah](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Menguasai Penyajian Data di Excel: Format Angka dan Tanggal Kustom dengan Aspose.Cells untuk Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Cara Membuat & Memformat Sel Excel Menggunakan Aspose.Cells untuk Java: Panduan Langkah‑demi‑Langkah](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}