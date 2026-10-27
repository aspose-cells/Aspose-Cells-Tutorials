---
category: general
date: 2026-08-14
description: Salin rentang antar workbook dengan Java menggunakan Aspose.Cells. Pelajari
  cara menyalin workbook tabel pivot, mengekspor gambar ke PowerPoint, dan menghapus
  AutoFilter dari tabel Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: id
lastmod: 2026-08-14
og_description: Salin rentang antar workbook di Java. Panduan ini menunjukkan cara
  menyalin workbook tabel pivot, mengekspor gambar ke PowerPoint, dan menghapus AutoFilter
  dari tabel Excel.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Menyalin rentang antar buku kerja di Java – tutorial lengkap Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Menyalin rentang antar buku kerja di Java – panduan langkah demi langkah
url: /id/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menyalin rentang antar workbook di Java – panduan langkah demi langkah

Jika Anda perlu **menyalin rentang antar workbook** di Java, Aspose.Cells menyediakan API yang bersih yang menangani objek kompleks seperti tabel pivot dan gambar. Tutorial ini menunjukkan cara **menyalin workbook tabel pivot**, **mengekspor gambar ke PowerPoint**, dan **menghapus AutoFilter dari tabel Excel** sambil menjaga kode tetap mudah dibaca dan dipelihara.

Anda akan belajar cara:

* Memuat workbook sumber dan menentukan rentang sumber.  
* Membuat workbook tujuan dan menyalin rentang sehingga tabel pivot tetap utuh.  
* Mengekspor gambar pertama pada lembar sebagai objek PowerPoint yang dapat diedit.  
* Menghapus AutoFilter dari tabel Excel pertama.  
* Memuat workbook dengan `SmartMarkerOptions` untuk memperlakukan array JSON sebagai nilai satu sel.

Contoh ini menggunakan Aspose.Cells 23.10 untuk Java, tetapi konsepnya berlaku untuk versi sebelumnya juga.

---

## Prerequisites

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Java 17 atau lebih baru | Diperlukan oleh runtime Aspose.Cells terbaru. |
| Aspose.Cells untuk Java (artefak Maven `com.aspose:aspose-cells`) | Menyediakan kelas `Workbook`, `Worksheet`, `Range`, dan kelas terkait yang digunakan dalam kode. |
| File Excel sumber (`src.xlsx`) yang berisi tabel pivot, gambar, dan tabel dengan AutoFilter. | Tutorial ini memanipulasi objek-objek tersebut untuk mendemonstrasikan setiap fitur. |

Tambahkan dependensi Maven ke `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Menyalin rentang antar workbook – memuat sumber dan tujuan

Langkah pertama adalah membuka workbook sumber, memilih rentang yang berisi data yang ingin Anda salin, dan membuat workbook tujuan yang kosong.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Mengapa ini penting:** Dengan menggunakan `Range.copy`, Aspose.Cells menyalin tidak hanya nilai sel mentah tetapi juga cache pivot yang mendasarinya, sehingga tabel pivot tetap berfungsi di workbook tujuan.

---

## Menyalin workbook tabel pivot saat menyalin rentang

Sekarang salin rentang yang telah ditentukan dari workbook sumber ke workbook tujuan. Tabel pivot dipertahankan secara otomatis karena rentang tersebut mencakup cache pivot.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Hasil:** Membuka `destination.xlsx` menampilkan tata letak tabel pivot yang sama seperti `src.xlsx`. Tidak ada kode tambahan yang diperlukan untuk membangun kembali cache pivot.

---

## Mengekspor gambar ke PowerPoint

Aspose.Cells dapat menandai gambar untuk diekspor menjadi objek PowerPoint yang dapat diedit. Kode berikut memilih gambar pertama pada lembar tujuan dan mengatur flag ekspor.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **Apa yang Anda lihat:** Membuka `destination.pptx` di PowerPoint menampilkan gambar sebagai bentuk asli yang dapat Anda edit, ubah ukuran, atau beri animasi.

---

## Menghapus AutoFilter dari tabel Excel

Jika lembar sumber berisi tabel dengan AutoFilter, Anda mungkin ingin menghapusnya setelah menyalin. Kode di bawah ini mengakses tabel pertama dan menghapus filternya.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Efek:** Tabel tetap ada di workbook, tetapi panah filter dropdown menghilang, memberi Anda tampilan data yang bersih.

---

## Memuat workbook dengan opsi SmartMarker – memperlakukan array JSON sebagai satu sel

Saat Anda menghasilkan laporan dari JSON, Aspose.Cells dapat memperlakukan seluruh array sebagai nilai satu sel. Ini berguna untuk menyisipkan string JSON ke dalam templat tanpa memperluasnya ke beberapa sel.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Mengapa Anda mungkin menggunakan ini:** Jika payload JSON Anda berisi array yang harus muncul sebagai string JSON dalam satu sel, `setArrayAsSingle(true)` mencegah Aspose.Cells memperluas array ke baris atau kolom terpisah.

---

![Menyalin rentang antar workbook di Java – contoh kode Aspose.Cells](copy-range-workbooks.png)

*Teks alt gambar:* **Menyalin rentang antar workbook di Java – contoh kode Aspose.Cells** (sesuai dengan kata kunci utama).

---

## Output yang diharapkan

| Nama file                | Berisi |
|--------------------------|--------|
| `destination.xlsx`       | Rentang yang disalin dengan tabel pivot yang berfungsi. |
| `destination.pptx`       | Gambar diekspor sebagai bentuk PowerPoint yang dapat diedit. |
| `final_output.xlsx`      | Tabel tanpa panah AutoFilter. |
| `template_filled.xlsx`   | Array JSON disimpan sebagai nilai satu sel. |

Buka setiap file di aplikasi yang sesuai (Excel atau PowerPoint) untuk memverifikasi bahwa operasi berhasil.

---

## Kesimpulan

Anda kini tahu cara **menyalin rentang antar workbook** di Java menggunakan Aspose.Cells, sambil mempertahankan tabel pivot, mengekspor gambar ke PowerPoint, dan menghapus AutoFilter dari tabel Excel. Pola yang sama dapat diperluas untuk menyalin rentang Excel apa pun ke workbook baru, menangani array JSON SmartMarker, atau menggabungkan transformasi tambahan.

Langkah selanjutnya yang dapat Anda jelajahi:

* **Menyalin rentang Excel ke workbook baru** dengan beberapa lembar kerja.  
* Gunakan **mengekspor gambar ke PowerPoint** untuk ekstraksi gambar secara batch.  
* Terapkan **menghapus autofilter dari tabel excel** dalam pipeline pelaporan yang lebih besar.  
* Gabungkan teknik ini dengan Aspose.Slides untuk otomatisasi penuh Excel‑ke‑PowerPoint.

Jangan ragu untuk bereksperimen dengan alamat rentang yang berbeda, beberapa tabel pivot, atau format gambar khusus. API Aspose.Cells dirancang untuk fleksibilitas pemrograman, sehingga Anda dapat menyesuaikan pola yang ditunjukkan di sini agar cocok dengan skenario otomatisasi Excel perusahaan apa pun.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang erat yang membangun pada teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Menyalin Gambar Antara Lembar di Excel Menggunakan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Menyalin Pengaturan Penataan Halaman Antara Lembar Kerja di Excel Menggunakan Aspose.Cells Java](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Menyalin Lembar Kerja Excel Antara Workbook](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}