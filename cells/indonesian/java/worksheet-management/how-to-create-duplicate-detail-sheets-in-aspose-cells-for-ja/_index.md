---
category: general
date: 2026-08-17
description: Pelajari cara membuat lembar detail duplikat dengan Aspose.Cells untuk
  Java dan mengizinkan nama lembar duplikat menggunakan SmartMarkerProcessor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicate detail sheets
- allow duplicate sheet names
language: id
lastmod: 2026-08-17
og_description: Buat lembar detail duplikat di Aspose.Cells untuk Java dan izinkan
  nama lembar duplikat. Ikuti tutorial lengkap ini untuk hasil instan.
og_image_alt: Generated Excel workbook showing multiple detail sheets with the same
  name
og_title: Buat lembar detail duplikat di Aspose.Cells untuk Java – panduan langkah
  demi langkah
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  headline: How to create duplicate detail sheets in Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  name: How to create duplicate detail sheets in Aspose.Cells for Java
  steps:
  - name: Load the master template workbook.
    text: Load the master template workbook.
  - name: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
    text: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
  - name: Process the workbook so that a new detail sheet is created for each data
      group.
    text: Process the workbook so that a new detail sheet is created for each data
      group.
  - name: Save the resulting workbook that now contains duplicated detail sheets.
    text: Save the resulting workbook that now contains duplicated detail sheets.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cara membuat lembar detail duplikat di Aspose.Cells untuk Java
url: /id/java/worksheet-management/how-to-create-duplicate-detail-sheets-in-aspose-cells-for-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat lembar detail duplikat di Aspose.Cells untuk Java

Jika Anda perlu **membuat lembar detail duplikat** dalam sebuah workbook Excel, Aspose.Cells untuk Java mempermudahnya. Tutorial ini menunjukkan secara tepat cara mengizinkan nama lembar duplikat saat menghasilkan lembar detail dengan SmartMarkerProcessor, sehingga Anda dapat menghasilkan workbook yang berisi beberapa lembar dengan nama yang sama.

Anda akan melihat contoh lengkap yang dapat dijalankan, penjabaran setiap opsi konfigurasi, dan tip untuk menangani kasus tepi umum seperti tabrakan nama dan kumpulan data besar. Tidak diperlukan referensi eksternal—semua yang Anda butuhkan sudah termasuk dalam kode di bawah.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* Java Development Kit (JDK) 8 atau yang lebih baru.
* Maven atau Gradle untuk mengelola dependensi.
* Pustaka Aspose.Cells untuk Java (versi 23.9 atau lebih baru). Tambahkan dependensi Maven berikut ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

* Sebuah workbook template master (`master_template.xlsx`) yang berisi wilayah Smart Marker untuk data detail.

## Gambaran Solusi

Solusi ini mengikuti empat langkah logis:

1. Muat workbook template master.
2. Konfigurasikan `SmartMarkerProcessor` untuk **mengizinkan nama lembar duplikat**.
3. Proses workbook sehingga lembar detail baru dibuat untuk setiap grup data.
4. Simpan workbook hasil yang kini berisi lembar detail yang diduplikasi.

Setiap langkah dijelaskan secara detail di bawah, dan file sumber lengkap disediakan di akhir panduan.

## Langkah 1: Muat workbook template master

Operasi pertama membuat instance `Workbook` yang mewakili file template. Template harus berisi placeholder Smart Marker (misalnya `&=DetailData`) yang memberi tahu processor di mana harus menyisipkan data.

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Load the master template workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");
```

**Mengapa ini penting:** Memuat template memisahkan tata letak dan pemformatan dari logika pembuatan data, yang membuat kode Anda bersih dan memudahkan penggunaan kembali template yang sama untuk kumpulan data yang berbeda.

## Langkah 2: Konfigurasikan SmartMarkerProcessor untuk mengizinkan nama lembar duplikat

Secara default, Aspose.Cells menghasilkan nama lembar unik saat membuat lembar detail. Untuk **mengizinkan nama lembar duplikat**, atur opsi `DetailSheetNewName` ke nilai konstan. Processor akan menggunakan kembali nama ini untuk setiap lembar yang dihasilkan.

```java
        // Create a SmartMarkerProcessor instance
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // Enable duplicate detail sheet names by assigning a fixed name
        processor.getOptions().setDetailSheetNewName("DetailSheet");

        // Optional: if you want to keep the original sheet after processing, set this flag
        // processor.getOptions().setKeepOriginalDetailSheet(true);
```

**Mengapa ini penting:** Menetapkan `DetailSheetNewName` memberi tahu engine untuk menggunakan kembali nama yang sama untuk setiap lembar detail, yang secara langsung memenuhi kebutuhan untuk **mengizinkan nama lembar duplikat**. Pendekatan ini berguna ketika alat downstream mengidentifikasi lembar berdasarkan posisinya bukan namanya.

## Langkah 3: Proses workbook untuk menghasilkan lembar detail

Setelah konfigurasi, panggil `process` pada workbook. Processor membaca wilayah Smart Marker, membuat lembar baru untuk setiap grup data, dan mengisinya dengan baris yang sesuai.

```java
        // Process the workbook; this creates the duplicate detail sheets
        processor.process(workbook);
```

**Mengapa ini penting:** Pemanggilan `process` melakukan pekerjaan berat—mem-parsing Smart Marker, mengkloning lembar template, dan menyisipkan data. Karena opsi `DetailSheetNewName` sudah diatur, setiap lembar baru menerima nama yang sama, menghasilkan nama lembar duplikat dalam file akhir.

## Langkah 4: Simpan workbook hasil

Akhirnya, tulis workbook yang telah dimodifikasi ke file baru. File output akan berisi sebanyak tab “DetailSheet” sesuai dengan jumlah grup data.

```java
        // Save the workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

**Mengapa ini penting:** Menyimpan file menyelesaikan perubahan yang dibuat oleh processor. Workbook hasil dapat dibuka di Microsoft Excel, LibreOffice, atau aplikasi spreadsheet lain yang mendukung format XLSX.

## Kode sumber lengkap

Menggabungkan semua bagian, berikut program lengkap yang dapat Anda salin, tempel, dan jalankan:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the master template workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");

        // Step 2: Create a SmartMarkerProcessor and allow duplicate detail sheet names
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.getOptions().setDetailSheetNewName("DetailSheet"); // same name allowed for each detail sheet

        // Step 3: Process the workbook to generate the detail sheets
        processor.process(workbook);

        // Step 4: Save the resulting workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

### Output yang Diharapkan

Saat Anda membuka `duplicate_detail.xlsx`, Anda akan melihat beberapa tab bernama **DetailSheet**. Setiap tab berisi kumpulan data yang sesuai dengan grup Smart Marker tertentu dalam template. Tata letak, pemformatan, dan formula dari template master dipertahankan pada setiap lembar duplikat.

## Menangani jebakan umum

| Masalah | Penjelasan | Solusi |
|-------|-------------|--------|
| Excel menampilkan peringatan tentang nama lembar duplikat | Excel mengizinkan nama duplikat tetapi dapat menampilkan peringatan saat file dibuka. | Peringatan tersebut tidak berbahaya; workbook berfungsi dengan benar. Jika Anda ingin menekan peringatan, ganti nama lembar setelah pemrosesan menggunakan `Workbook.getWorksheets().get(i).setName("DetailSheet" + i);`. |
| Kumpulan data besar menyebabkan penggunaan memori tinggi | Setiap lembar duplikat membuat salinan penuh template, yang dapat mengonsumsi RAM. | Aktifkan mode streaming dengan `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` sebelum memuat template. |
| Wilayah Smart Marker tidak ditemukan | Processor tidak dapat menemukan `&=DetailData` dalam template. | Pastikan sintaks placeholder sesuai dengan sumber data dan lembar template tidak tersembunyi. |

## Tips Pro: menyesuaikan skema penamaan duplikat

Jika Anda memerlukan pola penamaan yang dapat diprediksi sambil tetap mengizinkan duplikat, gabungkan nama dasar dengan indeks:

```java
processor.getOptions().setDetailSheetNewName("DetailSheet_{0}");
```

Placeholder `{0}` digantikan oleh indeks lembar, menghasilkan nama seperti `DetailSheet_1`, `DetailSheet_2`, dll. Ini tetap memenuhi persyaratan **mengizinkan nama lembar duplikat** karena nama dasar tetap konstan.

## Langkah Selanjutnya

Sekarang Anda dapat **membuat lembar detail duplikat**, Anda mungkin ingin menjelajahi topik berikut:

* **Isi lembar detail dengan gambar** – gunakan objek `Picture` untuk menyisipkan logo atau diagram.
* **Terapkan pemformatan bersyarat** – tambahkan aturan `FormatCondition` untuk menyorot baris berdasarkan nilai.
* **Ekspor ke PDF** – panggil `workbook.save("output.pdf", SaveFormat.PDF);` untuk menghasilkan versi PDF dari lembar duplikat.

Setiap ekstensi ini dibangun di atas alur kerja Smart Marker yang sama seperti yang ditunjukkan di sini, memungkinkan Anda mengotomatisasi tugas pelaporan Excel yang kompleks dengan percaya diri.

---

*Anda telah mempelajari cara membuat lembar detail duplikat di Aspose.Cells untuk Java dan cara mengizinkan nama lembar duplikat menggunakan SmartMarkerProcessor. Terapkan kode, sesuaikan template, dan integrasikan teknik ini ke dalam alur pelaporan Anda.*

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang dibangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Buat & Akses Lembar Excel, Tambahkan Bookmark PDF Menggunakan Aspose.Cells untuk Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Buat & Akses Lembar Excel Tambah Bookmark PDF Aspose Cells Java](/cells/german/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Buat & Akses Lembar Excel Tambah Bookmark PDF Aspose Cells Java](/cells/french/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}