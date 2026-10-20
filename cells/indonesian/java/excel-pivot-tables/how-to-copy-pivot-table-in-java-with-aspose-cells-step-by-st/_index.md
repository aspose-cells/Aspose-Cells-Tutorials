---
category: general
date: 2026-10-20
description: Pelajari cara menyalin tabel pivot menggunakan Aspose.Cells di Java.
  Tutorial ini menunjukkan cara menyalin rentang ke lembar baru dan menduplikasi lembar
  tabel pivot dengan aman.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new sheet
- duplicate pivot table sheet
language: id
lastmod: 2026-10-20
og_description: Cara menyalin tabel pivot dengan Aspose.Cells di Java. Ikuti panduan
  ini untuk menyalin rentang ke lembar baru dan menggandakan lembar tabel pivot tanpa
  kehilangan data.
og_image_alt: Screenshot showing how to copy pivot table from one worksheet to another
  in a Java program
og_title: Cara menyalin tabel pivot di Java – tutorial lengkap Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  headline: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  name: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that holds the original pivot table.
    text: Load the workbook that holds the original pivot table.
  - name: Identify the exact range that includes the pivot table.
    text: Identify the exact range that includes the pivot table.
  - name: Create a new worksheet that will receive the copied data.
    text: Create a new worksheet that will receive the copied data.
  - name: Use the `Range.copy` method to transfer the range to the new sheet.
    text: Use the `Range.copy` method to transfer the range to the new sheet.
  - name: Save the workbook to a new file.
    text: Save the workbook to a new file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cara menyalin tabel pivot di Java dengan Aspose.Cells – panduan langkah demi
  langkah
url: /id/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyalin pivot table di Java dengan Aspose.Cells – panduan langkah‑demi‑langkah

Jika Anda perlu **menyalin pivot table** dalam aplikasi Java, panduan ini akan memandu Anda melalui langkah‑langkah yang tepat. Baik Anda sedang membangun mesin pelaporan atau mengotomatisasi migrasi data, Anda akan melihat cara menyalin rentang ke lembar baru sambil mempertahankan definisi dan data pivot table.

Menyalin pivot table dapat terasa berisiko karena cache dasar dan pengaturan bidang sering hilang. Tutorial ini menunjukkan pendekatan yang dapat diandalkan menggunakan Aspose.Cells, menampilkan kode yang dapat dijalankan lengkap, dan menjelaskan mengapa setiap baris penting. Pada akhir tutorial, Anda akan dapat menduplikasi lembar pivot table dalam hitungan detik.

## Prasyarat

Sebelum memulai, pastikan Anda memiliki:

* Java 8 atau yang lebih baru terpasang.
* Aspose.Cells for Java (versi 23.10 atau lebih baru) ditambahkan ke classpath proyek Anda.
* Sebuah workbook sumber (`source.xlsx`) yang berisi pivot table pada rentang `A1:G20`.
* Pengetahuan dasar tentang Java dan konsep Excel.

Tidak ada pustaka tambahan yang diperlukan; Aspose.Cells menangani semua operasi Excel secara internal.

## Cara menyalin pivot table – strategi keseluruhan

Inti idenya sederhana:

1. Muat workbook yang berisi pivot table asli.
2. Identifikasi rentang tepat yang mencakup pivot table.
3. Buat worksheet baru yang akan menerima data yang disalin.
4. Gunakan metode `Range.copy` untuk memindahkan rentang ke lembar baru.  
   Metode ini secara otomatis menyalin pivot cache, sehingga pivot table tetap berfungsi.
5. Simpan workbook ke file baru.

Karena operasi penyalinan bekerja pada level rentang, **lembar pivot table duplikat** mempertahankan semua konfigurasi bidang, filter, dan item terhitung.

## Langkah 1: Muat workbook sumber

```java
// Import Aspose.Cells classes
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Mengapa ini penting*: Memuat workbook memberi Anda akses ke worksheet, sel, dan pivot cache‑nya. Aspose.Cells membaca seluruh file ke dalam memori, sehingga operasi selanjutnya cepat dan thread‑safe.

## Langkah 2: Tentukan rentang sumber yang berisi pivot table

```java
        // Locate the first worksheet (index 0) and create a range covering the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)               // first sheet
                                    .getCells()
                                    .createRange("A1:G20"); // adjust if your pivot table is larger
```

*Mengapa ini penting*: Pemanggilan `createRange` memberi tahu Aspose.Cells tepat sel mana yang akan disalin. Menyertakan seluruh area pivot table memastikan baris cache tersembunyi juga dipindahkan. Jika Anda melewatkan bagian cache mana pun, pivot table yang disalin akan muncul kosong.

## Langkah 3: Tambahkan worksheet tujuan untuk data yang disalin

```java
        // Add a new worksheet that will hold the duplicated pivot table
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");
```

*Mengapa ini penting*: Menambahkan lembar khusus memisahkan pivot table yang disalin dari yang asli, memudahkan perbandingan hasil atau penggunaan lembar sebagai templat untuk pemrosesan lebih lanjut.

## Langkah 4: Salin rentang ke worksheet tujuan (pivot table tetap terjaga)

```java
        // Copy the defined range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

*Mengapa ini penting*: Metode `copy` tidak hanya menyalin nilai sel dan format, tetapi juga mereplikasi pivot cache. Inilah langkah kunci yang memungkinkan Anda **menduplikasi lembar pivot table** tanpa kehilangan fungsi apa pun.

## Langkah 5: Simpan workbook dengan rentang yang disalin

```java
        // Persist the workbook to a new file
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

*Mengapa ini penting*: Penyimpanan menghasilkan file Excel baru (`result.xlsx`) yang berisi baik data asli maupun lembar pivot table yang diduplikasi. Anda kini dapat membuka file tersebut di Excel untuk memverifikasi bahwa pivot table berfungsi persis seperti sebelumnya.

## Contoh lengkap yang dapat dijalankan

Menggabungkan semua bagian, berikut program lengkap yang dapat Anda salin‑tempel ke IDE:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1. Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2. Define the source range that contains the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)
                                    .getCells()
                                    .createRange("A1:G20");

        // 3. Add a destination worksheet for the copied data
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");

        // 4. Copy the range to the destination worksheet (pivot table is preserved)
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5. Save the workbook with the copied range
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

### Output yang diharapkan

* Membuka `result.xlsx` menampilkan dua worksheet:
  * **Sheet1** – data dan pivot table asli.
  * **CopyResult** – duplikat tepat pivot table, berfungsi penuh.
* Semua bidang pivot, filter, dan item terhitung berperilaku identik dengan sumber.

Jika Anda memodifikasi pivot table sumber setelah penyalinan, lembar yang diduplikasi **tidak** akan mencerminkan perubahan tersebut karena cache telah diduplikasi pada saat penyalinan. Isolasi ini sering diinginkan ketika Anda memerlukan snapshot laporan.

## Kesalahan umum dan cara menghindarinya

| Masalah | Mengapa terjadi | Solusi |
|-------|----------------|-----|
| **Pivot table muncul kosong** | Rentang yang disalin tidak menyertakan baris cache tersembunyi. | Pastikan rentang mencakup seluruh cache (biasanya beberapa baris di bawah tabel yang terlihat). |
| **Nama sheet tujuan sudah ada** | `add("CopyResult")` melempar pengecualian jika nama sudah dipakai. | Gunakan `workbook.getWorksheets().addUniqueName("CopyResult")` atau periksa `contains` sebelum menambah. |
| **Kesalahan jalur file** | `YOUR_DIRECTORY` yang salah menyebabkan `FileNotFoundException`. | Gunakan jalur absolut atau `Paths.get(...).toAbsolutePath()` di Java untuk menyelesaikan lokasi. |
| **Penurunan performa pada workbook besar** | Menyalin rentang besar menyalin sel yang tidak diperlukan. | Batasi rentang hanya pada area pivot yang tepat, atau gunakan `Range.copy` dengan `CopyOptions` untuk melewatkan format jika tidak diperlukan. |

## Tips pro: Menggunakan `CopyOptions` untuk kontrol lebih halus

Jika Anda hanya membutuhkan data pivot table dan ingin melewatkan format sel, Anda dapat memberikan objek `CopyOptions`:

```java
CopyOptions options = new CopyOptions();
options.setCopyStyle(false);        // skip styles
options.setCopyMerged(true);        // keep merged cells
sourceRange.copy(destinationSheet.getCells().createRange("A1"), options);
```

Ini mengurangi ukuran file lembar duplikat dan mempercepat operasi penyalinan, terutama untuk workbook yang besar.

## Cara menyalin rentang ke lembar baru tanpa kehilangan formula

Contoh di atas sudah menyalin formula karena `Range.copy` mempertahankannya secara default. Jika Anda hanya menginginkan nilai (misalnya untuk membekukan keadaan saat ini), atur `options.setPasteType(PasteType.VALUES)`.

```java
CopyOptions opt = new CopyOptions();
opt.setPasteType(PasteType.VALUES);
sourceRange.copy(destinationSheet.getCells().createRange("A1"), opt);
```

Sekarang lembar tujuan berisi nilai statis, tetapi pivot table tetap berfungsi karena cache-nya merupakan bagian dari rentang.

## Ringkasan solusi

* **Cara menyalin pivot table** – muat workbook, tentukan rentang tepat, tambahkan worksheet baru, salin rentang, dan simpan.
* Proses ini juga menunjukkan **menyalin rentang ke lembar baru** dan cara **menduplikasi lembar pivot table** secara aman.
* Anda dapat menyesuaikan penyalinan dengan `CopyOptions` untuk performa atau skenario nilai‑saja.

## Langkah selanjutnya dan topik terkait

* **Menyegarkan pivot cache secara programatik** – gunakan `PivotTable.refreshData()` setelah memperbarui data sumber.
* **Mengekspor pivot table ke PDF** – gabungkan teknik penyalinan ini dengan `PdfSaveOptions` untuk membuat laporan snapshot.
* **Mengotomatisasi duplikasi multi‑sheet** – iterasi melalui semua worksheet dan terapkan logika penyalinan yang sama.

Cobalah variasi ini untuk menyesuaikan pola dengan pipeline pelaporan spesifik Anda. Jika Anda menemukan kasus tepi, seperti sumber data eksternal atau pivot yang dipicu VBA, pendekatan penyalinan rentang yang sama tetap berlaku, namun Anda mungkin perlu menyalin objek koneksi yang mendasarinya juga.

---

*Selamat coding! Jika tutorial ini membantu Anda belajar **cara menyalin pivot table**, jangan ragu untuk membagikannya dengan rekan tim atau berkontribusi pada perbaikan.*


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang erat dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Create New Workbook in Java – Full Guide to Copy Pivot Table](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}