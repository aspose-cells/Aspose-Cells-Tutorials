---
date: '2026-09-02'
description: Pelajari cara membuat buku kerja Excel dengan gambar yang dapat diklik
  menggunakan Aspose.Cells untuk Java, menambahkan hyperlink ke gambar untuk spreadsheet
  interaktif.
keywords:
- create clickable image
- add image hyperlink
- add hyperlink to picture
- interactive excel spreadsheet
- how to add hyperlink
lastmod: '2026-09-02'
og_description: Pelajari cara membuat buku kerja Excel dengan gambar yang dapat diklik
  menggunakan Aspose.Cells untuk Java, menambahkan hyperlink, tip layar, dan mengoptimalkan
  kinerja hanya dengan beberapa baris kode.
og_image_alt: 'Developer guide: create clickable image Excel using Aspose.Cells for
  Java'
og_title: Buat gambar Excel yang dapat diklik menggunakan Aspose.Cells untuk Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  headline: Create clickable image Excel using Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  name: Create clickable image Excel using Aspose.Cells for Java
  steps:
  - name: prepare your workbook
    text: We start by creating a new workbook and selecting the first sheet.
  - name: insert a label and adjust cell size
    text: Add a descriptive label and give the cell enough space for the picture.
  - name: add the image
    text: '`Picture` represents an image object placed on a worksheet. *Tip*: Replace
      `"path/to/aspose-logo.jpg"` with the actual path to your image file.'
  - name: configure placement and add the hyperlink
    text: '`Hyperlink` defines a link associated with a cell, shape, or picture, enabling
      navigation when clicked.'
  - name: set a screen tip and save the workbook
    text: Provide a helpful tooltip and write the workbook to disk.
  type: HowTo
- questions:
  - answer: Aspose.Cells for Java.
    question: What library is required?
  - answer: Yes – the API works with both .xls and .xlsx.
    question: Can I use .xlsx files?
  - answer: A trial works for evaluation; a permanent license is required for production.
    question: Do I need a license?
  - answer: About 20 lines to add a clickable image.
    question: How many lines of code?
  - answer: Workbook objects are not thread‑safe; create separate instances per thread.
    question: Is it thread‑safe?
  type: FAQPage
tags:
- create clickable image
- Aspose.Cells
- Java Excel automation
title: Buat gambar Excel yang dapat diklik menggunakan Aspose.Cells untuk Java
url: /id/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat gambar Excel yang dapat diklik menggunakan Aspose.Cells untuk Java

## Pendahuluan

Jika Anda ingin **create clickable image Excel** workbook yang memungkinkan pengguna melompat ke situs web, dokumen, atau sumber lain dengan satu klik, Anda berada di tempat yang tepat. Dalam tutorial ini kami akan menjelaskan bagaimana Aspose.Cells untuk Java memungkinkan Anda **add hyperlink Excel picture** objek, mengonfigurasi screen tip, dan menjaga spreadsheet Anda tetap indah dan fungsional.

### Apa yang akan Anda pelajari
- Menginisialisasi workbook Aspose.Cells di Java.  
- Menyisipkan gambar dan mengubahnya menjadi hyperlink yang dapat diklik.  
- Metode kunci seperti `addHyperlink`, `setPlacement`, dan `setScreenTip`.  
- Praktik terbaik untuk kinerja dan lisensi.

## Jawaban Cepat
- **Library apa yang diperlukan?** Aspose.Cells for Java.  
- **Bisakah saya menggunakan file .xlsx?** Ya – API bekerja dengan .xls dan .xlsx.  
- **Apakah saya memerlukan lisensi?** Versi percobaan dapat digunakan untuk evaluasi; lisensi permanen diperlukan untuk produksi.  
- **Berapa baris kode?** Sekitar 20 baris untuk menambahkan gambar yang dapat diklik.  
- **Apakah thread‑safe?** Objek Workbook tidak thread‑safe; buat instance terpisah per thread.  
- **Bisakah saya menambahkan screen tip Excel?** Ya – gunakan `Hyperlink.setScreenTip()` untuk menampilkan teks hover yang membantu.

## Cara membuat gambar Excel yang dapat diklik dengan Aspose.Cells untuk Java

Anda membuat workbook Excel dengan gambar yang dapat diklik dengan memuat atau membuat sebuah `Workbook`, menyisipkan objek `Picture`, melampirkan `Hyperlink` ke gambar tersebut, secara opsional mengatur screen tip, dan akhirnya menyimpan file. API menangani semua XML Excel tingkat rendah, sehingga Anda hanya menulis beberapa baris kode Java yang sederhana.

### Prasyarat
Sebelum Anda memulai, pastikan Anda memiliki:

- **Aspose.Cells for Java** (v25.3 atau lebih baru).  
- **JDK 8+** terpasang.  
- Sebuah IDE (IntelliJ IDEA, Eclipse, atau NetBeans) serta Maven atau Gradle untuk manajemen dependensi.  

### Pustaka yang diperlukan
Tambahkan Aspose.Cells ke proyek Anda:

**Maven**  
```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```  

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```  

### Perolehan lisensi
Aspose.Cells bersifat komersial, tetapi Anda dapat memulai dengan percobaan gratis atau meminta lisensi sementara:

- Percobaan gratis: Unduh dari [Unduhan Aspose](https://releases.aspose.com/cells/java/).  
- Lisensi sementara: Minta melalui [Halaman Lisensi Sementara](https://purchase.aspose.com/temporary-license/).  
- Pembelian: Untuk penggunaan jangka panjang, kunjungi [Pembelian Aspose](https://purchase.aspose.com/buy).

### Inisialisasi dasar
Kelas `Workbook` mewakili seluruh file Excel dalam memori. Anda menginstansiasinya, kemudian mendapatkan referensi ke lembar kerja pertama. `Worksheet` mewakili satu lembar dalam workbook.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

## Implementasi langkah demi langkah

### Langkah 1: siapkan workbook Anda
Kita mulai dengan membuat workbook baru dan memilih lembar pertama.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

### Langkah 2: sisipkan label dan sesuaikan ukuran sel
Tambahkan label deskriptif dan beri sel cukup ruang untuk gambar.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```  

### Langkah 3: tambahkan gambar
`Picture` mewakili objek gambar yang ditempatkan pada lembar kerja.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```  
*Tip*: Ganti `"path/to/aspose-logo.jpg"` dengan jalur sebenarnya ke file gambar Anda.

### Langkah 4: konfigurasikan penempatan dan tambahkan hyperlink
`Hyperlink` mendefinisikan tautan yang terkait dengan sel, bentuk, atau gambar, memungkinkan navigasi saat diklik.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```  

### Langkah 5: atur screen tip dan simpan workbook
Berikan tooltip yang membantu dan tulis workbook ke disk.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```  

## Mengapa menambahkan hyperlink pada gambar Excel?

Menyematkan gambar yang dapat diklik memungkinkan Anda mengubah elemen merek, ikon, atau diagram menjadi titik navigasi langsung, mengurangi jumlah klik yang diperlukan untuk mencapai konten terkait. Pendekatan ini meningkatkan efisiensi pengguna dalam dasbor pemasaran, manual teknis, dan lembar kerja edukasi.

## Cara menambahkan screen tip di Excel

Anda menambahkan screen tip dengan memanggil `hyperlink.setScreenTip("Your tip here")` pada objek `Hyperlink` yang terlampir pada gambar. Tip muncul ketika kursor melayang di atas gambar, memberikan panduan kontekstual kepada pengguna tanpa mengacaukan lembar.

## Tips pemecahan masalah
- **Kesalahan jalur gambar** – periksa kembali lokasi file dan pastikan aplikasi memiliki izin baca.  
- **Lisensi tidak diterapkan** – jika percobaan berakhir, hyperlink mungkin tidak berfungsi; terapkan lisensi yang valid dengan `License.setLicense`.  
- **Hyperlink tidak dapat diklik** – pastikan `PlacementType` gambar diatur ke `FREE_FLOATING`.

## Aplikasi praktis
Menyematkan gambar yang dapat diklik berguna dalam banyak skenario:

1. **Laporan pemasaran** – tautkan logo merek ke halaman produk.  
2. **Dokumentasi teknis** – lampirkan diagram yang membuka skematik detail.  
3. **Lembar kerja edukasi** – ubah ikon menjadi pintasan untuk video tambahan.  
4. **Dasbor proyek** – buat ikon status membuka pelacak tugas terkait.

## Pertimbangan kinerja
- Jaga ukuran file gambar tetap wajar; gambar besar meningkatkan penggunaan memori workbook.  
- Buang objek yang tidak terpakai (`workbook.dispose()`) saat memproses banyak file dalam loop.  
- Tingkatkan ke versi Aspose.Cells terbaru untuk perbaikan kinerja dan perbaikan bug.

## Kesimpulan
Anda kini tahu cara menambahkan hyperlink ke gambar di Excel menggunakan Aspose.Cells untuk Java, memungkinkan Anda **create clickable image Excel** workbook yang lebih kaya dan interaktif. Bereksperimenlah dengan berbagai URL, screen tip, dan penempatan gambar untuk menyesuaikan kebutuhan pelaporan Anda. Selanjutnya, Anda dapat mengeksplorasi menambahkan hyperlink ke bentuk atau mengotomatisasi penyisipan gambar massal di beberapa lembar kerja.

## Pertanyaan yang sering diajukan

**Q:** Apa ukuran gambar maksimum yang didukung oleh Aspose.Cells untuk Java?  
**A:** Tidak ada batas ketat, tetapi gambar yang sangat besar dapat memengaruhi kinerja dan meningkatkan ukuran file.

**Q:** Bisakah saya menggunakan fitur ini dengan file .xlsx?  
**A:** Ya, API bekerja dengan format `.xls` dan `.xlsx`.

**Q:** Bagaimana saya harus menangani pengecualian saat menambahkan hyperlink?  
**A:** Bungkus kode dalam blok try‑catch dan log detail `Exception` untuk mendiagnosis masalah jalur atau lisensi.

**Q:** Apakah memungkinkan menghapus hyperlink dari gambar setelah ditambahkan?  
**A:** Ya – dapatkan objek `Picture` dan panggil `pic.getHyperlink().remove()` atau hapus gambar dari koleksi.

**Q:** Mengapa hyperlink saya mungkin tidak berfungsi seperti yang diharapkan?  
**A:** Penyebab umum meliputi string URL yang salah, tidak adanya awalan `http://`/`https://`, atau percobaan tanpa lisensi yang menonaktifkan fitur tertentu.

## Sumber daya tambahan
- **Dokumentasi:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Unduhan:** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Pembelian dan percobaan:** Kunjungi [Aspose Purchase](https://purchase.aspose.com/buy) atau [Temporary License Page](https://purchase.aspose.com/temporary-license/) untuk opsi lisensi.  
- **Forum dukungan:** Untuk bantuan, lihat [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**Terakhir diperbarui:** 2026-09-02  
**Diuji dengan:** Aspose.Cells for Java 25.3  
**Penulis:** Aspose

## Tutorial Terkait

- [Cara Membuat Hyperlink di Excel Menggunakan Aspose.Cells untuk Java - Panduan Langkah‑per‑Langkah](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [Cara Menata Sel Excel dan Menambahkan Hyperlink Menggunakan Aspose.Cells untuk Java](/cells/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Menambahkan Gambar ke Komentar Excel dengan Aspose.Cells untuk Java: Panduan Lengkap](/cells/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}