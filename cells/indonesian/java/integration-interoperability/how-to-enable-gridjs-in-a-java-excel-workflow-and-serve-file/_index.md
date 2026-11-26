---
category: general
date: 2026-11-25
description: cara mengaktifkan GridJS di Java dengan cepat – memuat workbook Excel
  di Java, mengaktifkan mode kolaboratif, dan menyimpan Excel untuk web dalam satu
  panduan
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gridjs
- load excel workbook java
- save excel for web
- GridJS collaborative mode
- Aspose.Cells Java example
language: id
lastmod: 2026-11-25
og_description: Cara mengaktifkan GridJS di Java. Pelajari cara memuat workbook Excel
  di Java, mengaktifkan mode kolaboratif GridJS, dan menyimpan Excel untuk web dengan
  Aspose.Cells.
og_image_alt: Screenshot showing how to enable GridJS while loading an Excel workbook
  Java and saving it for web
og_title: Cara mengaktifkan GridJS di Java – memuat dan menyimpan Excel untuk web
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: how to enable GridJS in Java quickly – load Excel workbook Java, enable
    collaborative mode, and save Excel for web in a single guide
  headline: How to enable GridJS in a Java Excel workflow and serve files for the
    web
  type: TechArticle
tags:
- GridJS
- Java
- Excel
- Web integration
title: Cara mengaktifkan GridJS dalam alur kerja Java Excel dan menyajikan file untuk
  web
url: /id/java/integration-interoperability/how-to-enable-gridjs-in-a-java-excel-workflow-and-serve-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara mengaktifkan GridJS dalam alur kerja Java Excel dan menyajikan file untuk web

Jika Anda perlu **cara mengaktifkan GridJS** untuk spreadsheet yang akan ditampilkan di browser, panduan ini menunjukkan secara tepat cara melakukannya. Anda akan belajar **memuat workbook Excel Java**, mengaktifkan flag kolaboratif GridJS, dan **menyimpan Excel untuk web** dalam format yang dapat langsung dikonsumsi oleh GridJS.

Bekerja dengan file Excel di server sering berarti mengelola berbagai format file dan pustaka sisi klien. Dengan menggunakan Aspose.Cells untuk Java Anda menghindari konversi manual dan mendapatkan pipeline yang andal serta berperforma tinggi. Setelah mengikuti langkah‑langkah ini Anda akan memiliki file `*.gridjs` yang siap untuk komponen JavaScript GridJS mana pun.

## Prasyarat

- Java 17 atau lebih baru (kode dapat dikompilasi dengan JDK 8+ juga)
- Maven atau Gradle untuk mengelola dependensi
- Aspose.Cells untuk Java (versi 23.12 atau lebih baru) – tambahkan koordinat Maven `com.aspose:aspose‑cells:23.12`
- Pengetahuan dasar tentang penanganan exception Java
- Direktori di server tempat workbook sumber (`GridJsDemo.xlsx`) dan file output akan berada

> **Pro tip:** Simpan path workbook dalam file konfigurasi atau variabel lingkungan untuk menjaga kode Anda tetap dapat dipindahkan antar lingkungan.

## Langkah 1: Siapkan proyek dan impor kelas yang diperlukan

Buat proyek Maven standar (atau tambahkan dependensi ke build yang sudah ada). Impor berikut ini adalah semua yang Anda butuhkan untuk alur kerja inti:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import com.aspose.cells.SaveFormat;
import com.aspose.cells.LoadOptions;
import java.io.IOException;
```

Kelas-kelas ini memberi Anda akses ke pemuatan workbook, manipulasi pengaturan, dan format penyimpanan `GRID_JS`.

## Langkah 2: Muat workbook Excel Java

Memuat workbook adalah tindakan konkret pertama dalam proses **cara mengaktifkan GridJS** kami. Konstruktor `Workbook` membaca file ke memori dan secara otomatis memvalidasi formatnya.

```java
public class GridJsExporter {

    private static final String INPUT_PATH = "YOUR_DIRECTORY/GridJsDemo.xlsx";

    public static Workbook loadWorkbook() throws IOException {
        // Load the workbook from the file system
        Workbook workbook = new Workbook(INPUT_PATH);
        System.out.println("Workbook loaded successfully: " + INPUT_PATH);
        return workbook;
    }
}
```

> **Mengapa ini penting:** Memuat workbook dengan Aspose.Cells mempertahankan semua formula, gaya, dan objek tersemat, yang kemudian akan dirender oleh GridJS tanpa kehilangan.

## Langkah 3: Aktifkan mode kolaboratif GridJS

Mode kolaboratif memberi tahu Aspose.Cells untuk menyematkan metadata tambahan yang diperlukan oleh pustaka JavaScript GridJS (seperti ID sel dan informasi pelacakan perubahan). Ini adalah inti dari **cara mengaktifkan GridJS**.

```java
private static void enableGridJsMode(Workbook workbook) {
    WorkbookSettings settings = workbook.getSettings();
    // Turn on collaborative features for GridJS
    settings.setCollaborativeMode(true);
    System.out.println("GridJS collaborative mode enabled.");
}
```

> **Penjelasan:** `WorkbookSettings.setCollaborativeMode(true)` menyuntikkan struktur JSON ringan ke dalam file yang diekspor. Ketika komponen GridJS membaca file tersebut, ia dapat menyinkronkan edit di antara banyak pengguna secara real time.

## Langkah 4: Simpan Excel untuk web dalam format GridJS

Sekarang kami mengonversi workbook dalam memori ke format `GRID_JS`, yang pada dasarnya adalah bundel JSON yang langsung dikonsumsi oleh pustaka front‑end. Ini menyelesaikan bagian **menyimpan Excel untuk web** dari tutorial.

```java
private static final String OUTPUT_PATH = "YOUR_DIRECTORY/GridJsReady.xlsx";

private static void saveForWeb(Workbook workbook) throws IOException {
    // Save the workbook in the special GridJS format
    workbook.save(OUTPUT_PATH, SaveFormat.GRID_JS);
    System.out.println("Workbook saved for web at: " + OUTPUT_PATH);
}
```

> **Apa yang Anda dapatkan:** `GridJsReady.xlsx` bukan file XLSX tradisional; ia berisi JSON yang langsung diparsing oleh penampil GridJS, menghilangkan kebutuhan konversi sisi server pada saat permintaan.

## Langkah 5: Susun contoh lengkap yang dapat dijalankan

Menggabungkan semua menjadi satu menghasilkan kelas Java mandiri yang dapat Anda jalankan dari baris perintah atau diintegrasikan ke layanan Spring Boot.

```java
public class GridJsExporter {

    private static final String INPUT_PATH = "YOUR_DIRECTORY/GridJsDemo.xlsx";
    private static final String OUTPUT_PATH = "YOUR_DIRECTORY/GridJsReady.xlsx";

    public static void main(String[] args) {
        try {
            // 1. Load the Excel workbook Java
            Workbook workbook = new Workbook(INPUT_PATH);
            System.out.println("Workbook loaded successfully.");

            // 2. Enable GridJS collaborative mode (how to enable GridJS)
            WorkbookSettings settings = workbook.getSettings();
            settings.setCollaborativeMode(true);
            System.out.println("GridJS collaborative mode enabled.");

            // 3. Save Excel for web in GridJS format
            workbook.save(OUTPUT_PATH, SaveFormat.GRID_JS);
            System.out.println("Workbook saved for web at: " + OUTPUT_PATH);
        } catch (Exception e) {
            System.err.println("Error during GridJS export: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Output yang diharapkan

Menjalankan program mencetak:

```
Workbook loaded successfully.
GridJS collaborative mode enabled.
Workbook saved for web at: YOUR_DIRECTORY/GridJsReady.xlsx
```

File `GridJsReady.xlsx` kini berada di direktori target dan dapat disajikan langsung melalui server file statis atau CDN. Saat direferensikan dalam komponen GridJS front‑end, tabel akan dirender secara instan dengan dukungan edit penuh.

## Menangani kasus tepi umum

| Situasi                               | Penanganan yang disarankan                                                                        |
|----------------------------------------|---------------------------------------------------------------------------------------------|
| **File tidak ditemukan**                     | Verifikasi `INPUT_PATH` dan tangkap `java.io.FileNotFoundException` untuk mengembalikan error yang ramah pengguna. |
| **Versi Excel tidak didukung**          | Gunakan `LoadOptions` untuk menentukan format yang tepat, misalnya `new LoadOptions(LoadFormat.XLSX)`.   |
| **Workbook besar ( > 50 MB )**         | Aktifkan mode streaming: `workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` |
| **Perlu mempertahankan makro**            | Simpan sebagai `SaveFormat.XLSM` setelah ekspor GridJS jika Anda juga memerlukan file yang mendukung makro.      |

Dengan mengantisipasi skenario ini Anda memastikan pipeline **menyimpan Excel untuk web** tetap kuat dalam produksi.

## Ringkasan langkah‑demi‑langkah (referensi cepat)

| Langkah | Aksi | Potongan kode |
|------|--------|--------------|
| 1 | Muat workbook | `Workbook workbook = new Workbook(INPUT_PATH);` |
| 2 | Aktifkan GridJS | `workbook.getSettings().setCollaborativeMode(true);` |
| 3 | Simpan untuk web | `workbook.save(OUTPUT_PATH, SaveFormat.GRID_JS);` |

Anda dapat menyalin tabel ini ke dokumentasi atau README Anda sendiri untuk onboarding cepat.

## Langkah selanjutnya dan topik terkait

- **Integrasi dengan Spring MVC** – layani file `*.gridjs` melalui endpoint `@GetMapping`.
- **Konfigurasi GridJS sisi klien** – jelajahi opsi pagination, sorting, dan sinkronisasi real‑time.
- **Ekspor kembali ke XLSX** – setelah edit kolaboratif, gunakan `workbook.save("final.xlsx", SaveFormat.XLSX);`.
- **Pengoptimalan performa** – aktifkan `MemorySetting` untuk spreadsheet besar atau gunakan `Workbook.calculateFormula()` untuk mengevaluasi formula sebelum ekspor.

Ekstensi ini memungkinkan Anda membangun solusi spreadsheet full‑stack yang bekerja mulus dari back‑end Java ke front‑end JavaScript.

## Kesimpulan

Anda kini mengetahui **cara mengaktifkan GridJS** dalam aplikasi Java, cara **memuat workbook Excel Java**, dan cara **menyimpan Excel untuk web** menggunakan Aspose.Cells. Contoh lengkap yang dapat dijalankan menunjukkan setiap langkah yang diperlukan, menjelaskan alasan di balik setiap pemanggilan, dan mencakup kasus tepi yang akan Anda temui dalam proyek nyata. Deploy `GridJsReady.xlsx` yang dihasilkan ke server web mana pun, arahkan komponen GridJS Anda ke file tersebut, dan nikmati pengalaman spreadsheet kolaboratif yang instan.

--- 

![Diagram yang menggambarkan cara mengaktifkan GridJS saat memuat workbook Excel Java dan menyimpannya untuk web](/assets/images/gridjs-workflow.png){: .align-center width="600" alt="Diagram yang menunjukkan cara mengaktifkan GridJS dalam alur kerja Java Excel"}

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Membuat dan Mengekspor Excel ke HTML Menggunakan Aspose.Cells Java \| Panduan Operasi Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Cara Menyimpan File Excel dalam Berbagai Format Menggunakan Aspose.Cells Java](/cells/english/java/workbook-operations/save-excel-files-aspose-cells-java/)
- [Cara Memuat dan Menyimpan Excel sebagai CSV Menggunakan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}