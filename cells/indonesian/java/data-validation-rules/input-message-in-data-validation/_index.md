---
title: Pesan Input dalam Validasi Data
linktitle: Pesan Input dalam Validasi Data
second_title: API Pemrosesan Java Excel Aspose.Cells
description: Pelajari cara meningkatkan validasi data di Excel menggunakan Aspose.Cells untuk Java. Panduan langkah demi langkah dengan contoh kode untuk meningkatkan akurasi data dan panduan pengguna.
weight: 18
url: /id/java/data-validation-rules/input-message-in-data-validation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pesan Input dalam Validasi Data


## Pengantar Validasi Data

Validasi data adalah fitur di Excel yang membantu menjaga keakuratan dan konsistensi data dengan membatasi jenis data yang dapat dimasukkan ke dalam sel. Fitur ini memastikan bahwa pengguna memasukkan informasi yang valid, mengurangi kesalahan, dan meningkatkan kualitas data.

## Apa itu Aspose.Cells untuk Java?

Aspose.Cells untuk Java adalah API berbasis Java yang memungkinkan pengembang untuk membuat, memanipulasi, dan mengelola lembar kerja Excel tanpa memerlukan Microsoft Excel. API ini menyediakan berbagai fitur untuk bekerja dengan file Excel secara terprogram, menjadikannya alat yang berharga bagi pengembang Java.

## Menyiapkan Lingkungan Pengembangan Anda

Sebelum memulai, pastikan Anda telah menyiapkan lingkungan pengembangan Java di sistem Anda. Anda dapat menggunakan IDE favorit Anda, seperti Eclipse atau IntelliJ IDEA, untuk membuat proyek Java baru.

## Membuat Proyek Java Baru

Mulailah dengan membuat proyek Java baru di IDE pilihan Anda. Berikan nama yang bermakna, seperti "DataValidationDemo."

## Menambahkan Aspose.Cells untuk Java ke Proyek Anda

Untuk menggunakan Aspose.Cells for Java dalam proyek Anda, Anda perlu menambahkan pustaka Aspose.Cells. Anda dapat mengunduh pustaka tersebut dari situs web dan menambahkannya ke classpath proyek Anda.

## Menambahkan Validasi Data ke Lembar Kerja

Sekarang setelah Anda menyiapkan proyek, mari mulai menambahkan validasi data ke lembar kerja. Pertama, buat buku kerja Excel baru dan lembar kerja.

```java
// Buat buku kerja baru
Workbook workbook = new Workbook();
// Akses lembar kerja pertama
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Menentukan Kriteria Validasi

Anda dapat menentukan kriteria validasi untuk membatasi jenis data yang dapat dimasukkan ke dalam sel. Misalnya, Anda hanya dapat mengizinkan bilangan bulat antara 1 dan 100.

```java
// Tentukan kriteria validasi data
DataValidation validation = worksheet.getValidations().addDataValidation("A1");
validation.setType(DataValidationType.WHOLE);
validation.setOperator(OperatorType.BETWEEN);
validation.setFormula1("1");
validation.setFormula2("100");
```

## Pesan Input untuk Validasi Data

Pesan input memberikan panduan kepada pengguna tentang jenis data yang harus mereka masukkan. Anda dapat menambahkan pesan input ke aturan validasi data menggunakan Aspose.Cells untuk Java.

```java
// Tetapkan pesan masukan untuk validasi data
validation.setInputMessage("Please enter a number between 1 and 100.");
```

## Peringatan Kesalahan untuk Validasi Data

Selain pesan input, Anda dapat mengatur peringatan kesalahan untuk memberitahukan pengguna saat mereka memasukkan data yang tidak valid.

```java
// Tetapkan peringatan kesalahan untuk validasi data
validation.setShowError(true);
validation.setErrorTitle("Invalid Data");
validation.setErrorMessage("Please enter a valid number between 1 and 100.");
```

## Menerapkan Validasi Data ke Sel

Sekarang setelah Anda menentukan aturan validasi data, Anda dapat menerapkannya ke sel tertentu di lembar kerja Anda.

```java
// Terapkan validasi data ke rentang sel
CellArea area = new CellArea();
area.startRow = 0;
area.endRow = 9;
area.startColumn = 0;
area.endColumn = 0;
validation.addArea(area);
```

## Bekerja dengan Tipe Data yang Berbeda

Aspose.Cells untuk Java memungkinkan Anda bekerja dengan berbagai tipe data untuk validasi data, termasuk bilangan bulat, bilangan desimal, tanggal, dan teks.

```java
// Tetapkan jenis validasi data ke desimal
validation.setType(DataValidationType.DECIMAL);
```

## Menyesuaikan Pesan Validasi Data

Anda dapat menyesuaikan pesan masukan dan peringatan kesalahan untuk memberikan instruksi dan panduan spesifik kepada pengguna.

```java
// Sesuaikan pesan masukan dan pesan kesalahan
validation.setInputMessage("Please enter a decimal number.");
validation.setErrorMessage("Invalid input. Please enter a valid decimal number.");
```

## Memvalidasi Entri Tanggal

Validasi data juga dapat digunakan untuk memastikan bahwa entri tanggal berada dalam rentang atau format tertentu.

```java
// Tetapkan jenis validasi data ke tanggal
validation.setType(DataValidationType.DATE);
```

## Teknik Validasi Data Lanjutan

Aspose.Cells untuk Java menawarkan teknik tingkat lanjut untuk validasi data, seperti rumus khusus dan validasi berjenjang.

## Kesimpulan

Dalam artikel ini, kami telah menjajaki cara menambahkan pesan input ke aturan validasi data menggunakan Aspose.Cells untuk Java. Validasi data merupakan aspek penting dalam menjaga keakuratan data di Excel, dan Aspose.Cells memudahkan penerapan dan penyesuaian aturan ini di aplikasi Java Anda. Dengan mengikuti langkah-langkah yang diuraikan dalam panduan ini, Anda dapat meningkatkan kegunaan dan kualitas data buku kerja Excel Anda.

## Pertanyaan yang Sering Diajukan

### Bagaimana cara menambahkan validasi data ke beberapa sel sekaligus?

 Untuk menambahkan validasi data ke beberapa sel, Anda dapat menentukan rentang sel dan menerapkan aturan validasi ke rentang tersebut. Aspose.Cells untuk Java memungkinkan Anda menentukan rentang sel menggunakan`CellArea` kelas.

### Dapatkah saya menggunakan rumus khusus untuk validasi data?

Ya, Anda dapat menggunakan rumus khusus untuk validasi data di Aspose.Cells for Java. Ini memungkinkan Anda membuat aturan validasi yang kompleks berdasarkan persyaratan khusus Anda.

### Bagaimana cara menghapus validasi data dari sel?

 Untuk menghapus validasi data dari sel, Anda cukup memanggil`removeDataValidation`metode pada sel. Ini akan menghapus semua aturan validasi yang ada untuk sel tersebut.

### Dapatkah saya mengatur pesan kesalahan yang berbeda untuk aturan validasi yang berbeda?

Ya, Anda dapat mengatur pesan kesalahan yang berbeda untuk aturan validasi yang berbeda di Aspose.Cells untuk Java. Setiap aturan validasi data memiliki pesan input dan properti pesan kesalahannya sendiri yang dapat Anda sesuaikan.

### Di mana saya dapat menemukan informasi lebih lanjut tentang Aspose.Cells untuk Java?

 Untuk informasi lebih lanjut tentang Aspose.Cells untuk Java dan fitur-fiturnya, Anda dapat mengunjungi dokumentasi di[Di Sini](https://reference.aspose.com/cells/java/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
