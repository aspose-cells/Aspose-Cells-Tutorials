---
category: general
date: 2026-07-14
description: Salin tabel pivot antar buku kerja menggunakan Java. Pelajari cara menyalin
  pivot, menyalin rentang Excel, dan mengekspor tabel pivot dalam hitungan menit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- copy range between workbooks
- export pivot table
language: id
lastmod: 2026-07-14
og_description: Salin tabel pivot di Java dengan cepat. Panduan ini menunjukkan cara
  menyalin pivot, menyalin rentang Excel, dan mengekspor tabel pivot dengan Aspose.Cells.
og_image_alt: Diagram illustrating copy pivot table process between two Excel workbooks
og_title: Salin Tabel Pivot Antara Buku Kerja – Tutorial Otomatisasi Java
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Copy pivot table between workbooks using Java. Learn how to copy pivot,
    copy Excel range, and export pivot table in minutes.
  headline: Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Menyalin Tabel Pivot Antara Buku Kerja – Panduan Java Langkah demi Langkah
url: /id/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salin Tabel Pivot Antara Workbook – Tutorial Java Lengkap

Pernahkah Anda perlu **copy pivot table** dari satu workbook ke workbook lain dan bertanya-tanya mengapa trik copy‑paste biasa terus merusak tata letaknya? Anda tidak sendirian. Dalam banyak alur pelaporan pivot berada di file master, tetapi proses hilir memerlukan salinan yang ringan.  

Dalam panduan ini kami akan menjelaskan cara bersih dan programatis untuk menduplikasi pivot—tanpa perlu mengutak‑atik secara manual. Pada akhir tutorial Anda akan mengetahui **how to copy pivot**, cara **copy Excel range** dengan aman, dan bahkan cara **export pivot table** ke file baru, semuanya dengan Aspose.Cells for Java.

## Apa yang Akan Anda Bangun

- Muat workbook sumber yang sudah berisi tabel pivot.  
- Buat (atau buka) workbook tujuan.  
- Tentukan rentang tepat yang berisi pivot.  
- Salin rentang tersebut—termasuk definisi pivot—ke dalam workbook baru.  
- Simpan hasilnya sehingga aplikasi lain dapat membukanya tanpa kehilangan perhitungan apa pun.

Tanpa alat eksternal, tanpa VBA, hanya kode Java murni yang dapat Anda masukkan ke dalam proyek Maven atau Gradle apa pun.

## Prasyarat

- Java 17 atau lebih baru (kode ini bekerja pada Java 8+, tetapi JDK yang lebih baru memberikan kinerja lebih baik).  
- Aspose.Cells for Java 23.9 atau yang lebih baru – tambahkan dependensinya dari Maven Central.  
- Dua file Excel: `SourceWithPivot.xlsx` (berisi pivot) dan placeholder kosong untuk salinan.

Jika Anda baru mengenal Aspose.Cells, perpustakaan ini mengabstraksi detail OOXML tingkat rendah, memungkinkan Anda memperlakukan lembar kerja seperti objek Java biasa.

## Langkah 1: Siapkan Proyek Anda

Pertama, tambahkan artefak Maven Aspose.Cells ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust if you use a different JDK -->
</dependency>
```

Atau, untuk Gradle:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

> **Pro tip:** Jika Anda menggunakan IDE seperti IntelliJ, biarkan ia mengimpor perpustakaan secara otomatis; ini menghemat banyak pengetikan.

## Langkah 2: Muat Workbook Sumber

Kita memerlukan instance `Workbook` yang menunjuk ke file yang berisi pivot. Konstruktor membaca seluruh file ke memori, sehingga Anda dapat bekerja secara offline.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {

        // Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

Mengapa harus memuatnya terlebih dahulu? Karena cache pivot, daftar bidang, dan tata letaknya semuanya disimpan di dalam lembar. Mengambil workbook ke memori memastikan kita menyalin *definisi* dan bukan hanya nilai yang dirender.

## Langkah 3: Buat atau Buka Workbook Tujuan

Anda memiliki dua pilihan: memulai dengan workbook baru, atau membuka template yang sudah ada. Di sini kami akan membuat yang kosong, yang merupakan skenario paling umum ketika Anda memerlukan salinan bersih.

```java
        // Create an empty destination workbook (or open an existing one)
        Workbook destinationWorkbook = new Workbook(); // blank workbook with a default sheet
```

Jika nanti Anda memutuskan menyalin ke lembar tertentu, cukup ganti `getWorksheets().get(0)` dengan indeks atau nama yang sesuai.

## Langkah 4: Tentukan Rentang Tepat yang Menampung Pivot

Tabel pivot biasanya menempati blok persegi panjang. Pendekatan paling aman adalah menentukan sel kiri‑atas dan kanan‑bawah secara eksplisit. Dalam contoh kami pivot berada dari **A1** hingga **H30**.

```java
        // Define the range in the source sheet that includes the pivot table
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)                     // first worksheet
                                          .getCells()
                                          .createRange("A1:H30");
```

> **Mengapa tidak menggunakan `copyRows`?**  
> `copyRows` menyalin nilai sel mentah tetapi mengabaikan cache pivot yang mendasarinya. Dengan menyalin seluruh rentang, Aspose.Cells mempertahankan metadata pivot, memungkinkan tujuan mempertahankan interaktivitas penuh.

## Langkah 5: Salin Rentang (Termasuk Pivot) ke Tujuan

Sekarang keajaiban terjadi. Metode `copy` menggandakan semuanya—nilai, formula, format, dan objek pivot itu sendiri—ke lokasi target.

```java
        // Copy the defined range (with the pivot table) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)               // destination sheet
                                            .getCells()
                                            .createRange("A1"));
```

Jika Anda perlu menempel ke sel lain, cukup ubah `"A1"` menjadi `"C5"` atau alamat apa pun yang Anda inginkan. Metode ini secara otomatis menyesuaikan referensi internal sehingga pivot tetap berfungsi.

## Langkah 6: Simpan Workbook Tujuan

Akhirnya, tulis workbook baru ke disk. File yang dihasilkan dapat dibuka di Excel, LibreOffice, atau penampil spreadsheet lainnya, dan pivot akan berperilaku persis seperti di sumber.

```java
        // Save the destination workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

### Hasil yang Diharapkan

- `CopyPivotResult.xlsx` terbuka dengan tabel pivot yang berfungsi penuh dan identik dengan yang asli.  
- Semua slicer, filter, dan bidang terhitung tetap utuh.  
- Tidak ada kehilangan data—nilai dihitung secara langsung saat Anda menyegarkan pivot.

## Variasi Umum & Kasus Tepi

| Situasi | Apa yang Harus Disesuaikan |
|-----------|----------------|
| **Copy into an existing workbook** | Muat workbook target alih-alih membuat yang baru: `new Workbook("ExistingFile.xlsx")`. |
| **Pivot spans an unknown size** | Gunakan `Worksheet.getPivotTables().get(0).getPivotTableRange()` untuk mengambil alamat tepat secara programatis. |
| **Preserve data connections** | Setelah menyalin, panggil `destinationWorkbook.getWorksheets().get(0).getPivotTables().get(0).setRefreshOnLoad(true);` untuk menjaga tautan data eksternal tetap aktif. |
| **Export pivot table as CSV** | Setelah disalin, Anda dapat memanggil `destinationWorkbook.save("PivotExport.csv", SaveFormat.CSV);` – ini meratakan hanya nilai pivot. |

> **Waspadai:** Ketika workbook sumber dan tujuan menggunakan pengaturan locale yang berbeda, format angka dapat berubah. Atur secara eksplisit `setLocale` pada workbook jika Anda memerlukan konsistensi.

## Contoh Kerja Lengkap (Semua Impor Termasuk)

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load source workbook containing the pivot
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

        // 2️⃣ Create (or open) destination workbook
        Workbook destinationWorkbook = new Workbook(); // blank workbook

        // 3️⃣ Identify the range that encloses the pivot table
        //    If you don't know the range, you can retrieve it via:
        //    PivotTable pt = sourceWorkbook.getWorksheets().get(0).getPivotTables().get(0);
        //    String address = pt.getPivotTableRange().getRefersTo();
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:H30");

        // 4️⃣ Copy the range (pivot included) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)
                                            .getCells()
                                            .createRange("A1"));

        // 5️⃣ Persist the result
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully!");
    }
}
```

Jalankan program, buka `CopyPivotResult.xlsx`, dan Anda akan melihat pivot yang persis sama dengan yang Anda mulai—siap untuk analisis lebih lanjut atau distribusi.

## Ringkasan

Kami baru saja mendemonstrasikan **how to copy pivot** dari satu workbook ke workbook lain menggunakan Aspose.Cells for Java. Langkah‑langkah mencakup memuat sumber, menentukan **copy Excel range** yang tepat, melakukan penyalinan, dan akhirnya **export pivot table** ke file baru. Dengan menangani rentang alih‑alih sel individu, kami menjamin cache internal pivot ikut terbawa, menjaga laporan tetap dinamis.

## Apa yang Harus Anda Jelajahi Selanjutnya

- **Automate refresh**: Jadwalkan operasi penyalinan dengan pekerjaan Quartz sehingga file hilir Anda tetap up‑to‑date.  
- **Copy multiple pivots**: Loop melalui `sourceWorkbook.getWorksheets().get(0).getPivotTables()` dan salin masing‑masing ke lembar terpisah.  
- **Apply styling**: Gunakan objek `Style` untuk menyelaraskan font dan warna di seluruh workbook tujuan.  

Jika Anda memiliki pertanyaan tentang menangani workbook besar atau mempertahankan sumber data eksternal, tinggalkan komentar di bawah. Selamat coding, dan nikmati kebebasan otomatisasi Excel secara programatis!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automate Excel Pivot Table Styling and Saving with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}