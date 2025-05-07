---
"description": "Pelajari cara membuat validasi data khusus menggunakan Aspose.Cells untuk Java. Panduan langkah demi langkah dengan kode sumber."
"linktitle": "Membuat Validasi Data Kustom"
"second_title": "API Pemrosesan Java Excel Aspose.Cells"
"title": "Membuat Validasi Data Kustom"
"url": "/id/java/data-validation-rules/creating-custom-data-validation/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Validasi Data Kustom


## Perkenalan

Validasi data membantu menjaga integritas data dengan mencegah pengguna memasukkan data yang salah atau tidak valid ke dalam lembar kerja Excel. Meskipun Excel menawarkan opsi validasi data bawaan, ada beberapa skenario di mana Anda perlu menentukan aturan validasi khusus. Aspose.Cells untuk Java memungkinkan Anda mencapainya secara efisien.

## Prasyarat

Sebelum menyelami kode, pastikan Anda memiliki prasyarat berikut:

- Aspose.Cells untuk Java: Unduh dan instal pustaka dari [Di Sini](https://releases.aspose.com/cells/java/).

## Langkah 1: Menyiapkan Proyek Java Anda

Untuk memulai, buat proyek Java baru di Lingkungan Pengembangan Terpadu (IDE) pilihan Anda. Tambahkan pustaka Aspose.Cells for Java ke classpath proyek Anda.

## Langkah 2: Membuat Buku Kerja Excel

Mari kita mulai dengan membuat buku kerja Excel baru menggunakan Aspose.Cells untuk Java.

```java
// Kode Java untuk membuat buku kerja Excel baru
Workbook workbook = new Workbook();
```

## Langkah 3: Menambahkan Lembar Kerja

Sekarang, mari tambahkan lembar kerja ke buku kerja tempat kita akan menerapkan validasi data khusus kita.

```java
// Kode Java untuk menambahkan lembar kerja
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Langkah 4: Menentukan Kriteria Validasi Kustom

Pada langkah ini, kita akan menentukan kriteria validasi khusus yang harus dipatuhi oleh data kita. Misalnya, kita ingin membatasi usia yang dimasukkan dalam sel antara 18 dan 60 tahun.

```java
// Kode Java untuk menentukan kriteria validasi khusus
Validation validation = worksheet.getValidations().add();
validation.setType(ValidationType.WHOLE);
validation.setOperator(OperatorType.BETWEEN);
validation.setFormula1("18");
validation.setFormula2("60");
validation.setShowError(true);
validation.setAlertStyle(ValidationAlertType.STOP);
validation.setErrorTitle("Invalid Age");
validation.setErrorMessage("Age must be between 18 and 60.");
```

## Langkah 5: Menerapkan Validasi Data ke Rentang

Sekarang setelah kita menentukan kriteria validasi khusus, mari terapkan pada rentang sel tertentu.

```java
// Kode Java untuk menerapkan validasi data ke suatu rentang
CellArea area = new CellArea();
area.startRow = 0;
area.startColumn = 0;
area.endRow = 9; // Terapkan validasi ke sepuluh baris pertama
area.endColumn = 0;

validation.addArea(area);
```

## Langkah 6: Menyimpan File Excel

Terakhir, simpan file Excel dengan aturan validasi data khusus yang diterapkan.

```java
// Kode Java untuk menyimpan file Excel
workbook.save("CustomDataValidation.xlsx");
```

## Kesimpulan

Dalam tutorial ini, kami telah mempelajari cara membuat aturan validasi data kustom menggunakan Aspose.Cells untuk Java. Dengan mengikuti langkah-langkah ini, Anda dapat memastikan bahwa data Excel Anda mematuhi kriteria tertentu, sehingga meningkatkan integritas dan akurasi data.

## Pertanyaan yang Sering Diajukan

### Bagaimana cara mengunduh Aspose.Cells untuk Java?

Anda dapat mengunduh Aspose.Cells untuk Java dari situs web di [Di Sini](https://releases.aspose.com/cells/java/).

### Dapatkah saya menerapkan validasi data khusus ke beberapa rentang di lembar kerja yang sama?

Ya, Anda dapat menerapkan validasi data kustom ke beberapa rentang dalam lembar kerja yang sama dengan mengulangi Langkah 5 untuk setiap rentang yang diinginkan.

### Apakah ada jenis validasi data lain yang didukung oleh Aspose.Cells untuk Java?

Ya, Aspose.Cells untuk Java mendukung berbagai jenis validasi data, termasuk bilangan bulat, desimal, tanggal, waktu, panjang teks, dan banyak lagi.

### Bagaimana saya dapat menyesuaikan pesan kesalahan yang ditampilkan saat validasi data gagal?

Anda dapat menyesuaikan pesan kesalahan dengan memodifikasi `setErrorMessage` metode pada Langkah 4, di mana Anda menentukan kriteria validasi.

### Apakah Aspose.Cells untuk Java berfungsi dengan file Excel dalam format yang berbeda?

Ya, Aspose.Cells untuk Java mendukung berbagai format file Excel, termasuk XLS, XLSX, XLSM, dan banyak lagi.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}