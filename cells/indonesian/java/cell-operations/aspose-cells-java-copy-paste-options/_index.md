---
date: '2026-02-22'
description: Pelajari cara mengotomatiskan pelaporan Excel dengan Aspose.Cells di
  Java menggunakan CopyOptions dan PasteOptions untuk menjaga keakuratan rumus serta
  menempelkan hanya nilai yang terlihat.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: Mengotomatiskan Pelaporan Excel – Menguasai CopyOptions & PasteOptions di Java
  dengan Aspose.Cells
url: /id/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Otomatisasi Pelaporan Excel dengan Aspose.Cells: CopyOptions & PasteOptions dalam Java

Apakah Anda ingin **mengotomatisasi pelaporan Excel** menggunakan Java? Dengan Aspose.Cells Anda dapat menyalin, menempel, dan menyesuaikan rumus secara programatis sehingga laporan Anda tetap akurat dan hanya data yang Anda butuhkan yang dipindahkan. Dalam tutorial ini kami akan membahas dua fitur penting—**CopyOptions.ReferToDestinationSheet** dan **PasteOptions**—yang memungkinkan Anda mempertahankan referensi rumus dan menempel nilai hanya dari sel yang terlihat.

## Jawaban Cepat
- **Apa yang dilakukan `CopyOptions.ReferToDestinationSheet`?** Menyesuaikan rumus agar mengarah ke lembar tujuan saat menyalin data.  
- **Bagaimana cara menempel hanya sel yang terlihat?** Atur `PasteOptions.setOnlyVisibleCells(true)` dengan `PasteType.VALUES`.  
- **Versi perpustakaan apa yang diperlukan?** Aspose.Cells 25.3 atau lebih baru.  
- **Apakah saya memerlukan lisensi untuk produksi?** Ya, lisensi permanen atau sementara menghapus batas evaluasi.  
- **Apakah saya dapat menggunakan Maven atau Gradle?** Kedua-duanya didukung; lihat potongan dependensi di bawah.

## Apa itu “mengotomatisasi pelaporan Excel”?
Mengotomatisasi pelaporan Excel berarti menghasilkan, mengkonsolidasikan, dan memformat workbook Excel secara programatis, menghilangkan langkah salin‑tempel manual dan mengurangi kesalahan. Aspose.Cells menyediakan API yang kaya yang memungkinkan pengembang Java memanipulasi spreadsheet secara skala besar.

## Mengapa menggunakan CopyOptions dan PasteOptions untuk pelaporan?
- **Mempertahankan integritas rumus** saat memindahkan data antar lembar.  
- **Mengecualikan baris/kolom tersembunyi** untuk menjaga laporan tetap bersih dan fokus.  
- **Meningkatkan kinerja** dengan menyalin hanya data yang diperlukan alih-alih seluruh rentang.

## Prasyarat
- Java 8 atau lebih tinggi.  
- Maven atau Gradle untuk manajemen dependensi.  
- Aspose.Cells 25.3+ (lisensi percobaan, sementara, atau permanen).  

## Menyiapkan Aspose.Cells untuk Java

Tambahkan perpustakaan ke proyek Anda dengan salah satu cara berikut:

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
implementation 'com.aspose:aspose-cells:25.3'
```

### Akuisisi Lisensi
- **Free Trial** – Set fitur lengkap untuk evaluasi.  
- **Temporary License** – Menghapus batasan percobaan saat Anda menguji.  
- **Permanent License** – Direkomendasikan untuk beban kerja produksi.

Inisialisasi Aspose.Cells dalam kode Java Anda:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Panduan Langkah‑per‑Langkah

### 1. CopyOptions dengan ReferToDestinationSheet

#### Ikhtisar
Mengatur `CopyOptions.ReferToDestinationSheet` ke `true` menulis ulang referensi rumus sehingga mengarah ke lembar baru setelah operasi penyalinan.

#### Langkah 1: Inisialisasi Workbook dan Worksheet
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Langkah 2: Konfigurasi CopyOptions
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Langkah 3: Jalankan Operasi Penyalinan
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Mengapa ini penting*: Rumus yang awalnya merujuk ke `Sheet1` kini akan merujuk dengan benar ke `DestSheet`, menjaga laporan otomatis Anda tetap dapat diandalkan.

**Tips Pemecahan Masalah**: Jika rumus masih merujuk ke lembar lama, pastikan `setReferToDestinationSheet(true)` dipanggil **sebelum** penyalinan.

### 2. PasteOptions untuk Nilai‑Saja dari Sel yang Terlihat

#### Ikhtisar
`PasteOptions` memungkinkan Anda menentukan apa yang akan ditempel. Menggunakan `PasteType.VALUES` bersama dengan `onlyVisibleCells=true` menyalin hanya nilai yang ditampilkan, mengabaikan baris/kolom tersembunyi serta pemformatan.

#### Langkah 1: Inisialisasi Workbook dan Worksheet
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Langkah 2: Konfigurasi PasteOptions
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Langkah 3: Jalankan Operasi Tempel
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Mengapa ini penting*: Ideal untuk mengekstrak data yang difilter atau menghasilkan laporan bersih tanpa baris tersembunyi atau gangguan pemformatan.

**Tips Pemecahan Masalah**: Pastikan baris/kolom benar‑benar tersembunyi di Excel sebelum menyalin; jika tidak, mereka akan disertakan.

## Aplikasi Praktis
1. **Financial Consolidation** – Menggabungkan lembar bulanan ke dalam workbook utama sambil menjaga semua rumus tetap akurat.  
2. **Filtered Data Export** – Mengambil hanya baris yang terlihat dari tabel yang difilter ke dalam lembar ringkasan.  
3. **Scheduled Report Generation** – Mengotomatisasi pembuatan laporan Excel setiap malam dengan nilai sel yang tepat dan referensi yang benar.

## Pertimbangan Kinerja
- **Dispose of Workbooks** ketika selesai (`wb.dispose();`) untuk membebaskan sumber daya native.  
- **Batch Operations** – Mengelompokkan beberapa panggilan copy/paste untuk mengurangi overhead.  
- **Monitor Memory** – Workbook besar mungkin memerlukan heap yang lebih besar (`-Xmx2g`).

## Pertanyaan yang Sering Diajukan

**Q1: Apa kegunaan `CopyOptions.ReferToDestinationSheet`?**  
A: Itu menulis ulang referensi rumus sehingga mengarah ke lembar tujuan setelah penyalinan, memastikan rumus pelaporan tetap benar.

**Q2: Bagaimana cara menempel hanya sel yang terlihat?**  
A: Atur `PasteOptions.setOnlyVisibleCells(true)` dan pilih `PasteType.VALUES`.

**Q3: Bisakah saya menggunakan Aspose.Cells tanpa membeli lisensi?**  
A: Ya, percobaan gratis atau lisensi sementara tersedia untuk evaluasi, tetapi lisensi permanen diperlukan untuk produksi.

**Q4: Mengapa beberapa referensi masih salah setelah penyalinan?**  
A: Periksa kembali bahwa `ReferToDestinationSheet` diaktifkan **sebelum** operasi penyalinan dan bahwa rumus sumber tidak mengandung tautan workbook eksternal.

**Q5: Praktik terbaik manajemen memori apa yang harus saya ikuti?**  
A: Dispose objek `Workbook` setelah selesai, proses file besar secara bertahap, dan pantau penggunaan heap JVM.

**Q6: Apakah memungkinkan menggabungkan CopyOptions dan PasteOptions dalam satu operasi?**  
A: Ya, Anda dapat menautkannya dengan pertama menyalin menggunakan `CopyOptions` lalu menerapkan `PasteOptions` pada rentang target.

## Sumber Daya
- **Dokumentasi**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Unduh**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Pembelian**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Percobaan Gratis**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Lisensi Sementara**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Forum Dukungan**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Terakhir Diperbarui:** 2026-02-22  
**Diuji Dengan:** Aspose.Cells 25.3 for Java  
**Penulis:** Aspose