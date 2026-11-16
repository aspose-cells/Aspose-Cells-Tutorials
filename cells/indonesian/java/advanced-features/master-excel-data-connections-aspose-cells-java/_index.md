---
date: '2026-11-16'
description: Pelajari cara mengotomatiskan penyegaran data Excel dengan memperbarui
  koneksi data Excel secara programatis menggunakan Aspose.Cells for Java. Termasuk
  penyiapan, penjelasan kode, dan pemecahan masalah.
keywords:
- automate excel data refresh
- update excel data source
- how to change connection
- excel external data connection
- modify excel data connections
lastmod: '2026-11-16'
og_description: Pelajari cara mengotomatiskan penyegaran data Excel dengan memperbarui
  koneksi data Excel secara programatis menggunakan Aspose.Cells for Java. Termasuk
  penyiapan, penjelasan kode, dan pemecahan masalah.
og_image_alt: Guide to automate Excel data refresh using Aspose.Cells for Java
og_title: Otomatisasi penyegaran data Excel dengan Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to automate Excel data refresh by updating Excel data connections
    programmatically using Aspose.Cells for Java. Includes setup, code walkthrough,
    and troubleshooting.
  headline: Automate excel data refresh with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to automate Excel data refresh by updating Excel data connections
    programmatically using Aspose.Cells for Java. Includes setup, code walkthrough,
    and troubleshooting.
  name: Automate excel data refresh with Aspose.Cells for Java
  steps:
  - name: '**Automated reporting** – Generate reports that pull live data from a database
      without manual refreshes.'
    text: '**Automated reporting** – Generate reports that pull live data from a database
      without manual refreshes.'
  - name: '**Data syncing** – Keep Excel dashboards in sync with back‑end systems,
      reducing stale data risk.'
    text: '**Data syncing** – Keep Excel dashboards in sync with back‑end systems,
      reducing stale data risk.'
  - name: '**Custom dashboards** – Build interactive dashboards that reflect real‑time
      data changes for finance or sales teams.'
    text: '**Custom dashboards** – Build interactive dashboards that reflect real‑time
      data changes for finance or sales teams.'
  type: HowTo
- questions:
  - answer: Use `workbook.getDataConnections().get(index)` to retrieve each connection
      individually, then modify them as needed.
    question: How do I handle multiple data connections in a workbook?
  - answer: Absolutely. The API supports cell formatting, worksheet management, chart
      creation, and more.
    question: Can I modify other workbook properties with Aspose.Cells Java?
  - answer: Double‑check the connection string and ensure the database user has the
      required permissions. Review the exception details for clues.
    question: What should I do if my SQL command fails at runtime?
  - answer: Visit the [Aspose forum](https://forum.aspose.com/c/cells/9) to ask questions
      or browse existing solutions.
    question: Where can I get help if I encounter issues?
  - answer: The evaluation version adds watermarks to generated files and may limit
      processing size. A licensed version removes these restrictions.
    question: Are there limitations with the free trial version?
  type: FAQPage
tags:
- automate excel refresh
- aspose.cells java
- excel data connections
- java data integration
title: Otomatisasi penyegaran data Excel dengan Aspose.Cells for Java
url: /id/java/advanced-features/master-excel-data-connections-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Otomatisasi penyegaran data Excel dengan Aspose.Cells untuk Java

## Pendahuluan
Jika Anda perlu **mengotomatisasi penyegaran data Excel** dengan mengubah pengaturan koneksi di dalam workbook tanpa membukanya secara manual, Anda berada di tempat yang tepat. Tutorial ini akan memandu Anda memuat file Excel, memperbarui koneksi datanya, dan menyimpan perubahan—semua dengan **Aspose.Cells untuk Java**. Pada akhir tutorial, Anda akan terbiasa dengan *load excel workbook java*, *save excel workbook java*, dan bahkan *change excel connection string* secara programatik.

### Apa yang akan Anda pelajari
- Cara menyiapkan lingkungan Anda menggunakan Aspose.Cells Java.  
- Instruksi langkah demi langkah untuk **memuat workbook Excel** dari sebuah file.  
- Teknik untuk **memodifikasi koneksi data yang ada** (termasuk mengubah connection string).  
- Cara **menyimpan workbook** setelah pembaruan.  

Mari kita mulai dengan memastikan Anda memiliki semua yang diperlukan untuk tutorial ini!

## Jawaban Cepat
- **Apa kelas utama untuk menangani workbook?** `com.aspose.cells.Workbook`  
  `com.aspose.cells.Workbook` adalah kelas utama yang mewakili sebuah workbook Excel dalam memori.  
- **Metode mana yang menyimpan perubahan ke file?** `workbook.save()`  
  `workbook.save()` menulis workbook ke file di disk.  
- **Apakah saya dapat mengubah connection string?** Ya, gunakan `DBConnection.setConnectionInfo()`  
  `DBConnection.setConnectionInfo()` mengatur connection string dan properti terkait untuk koneksi database.  
- **Apakah saya memerlukan lisensi untuk produksi?** Versi berlisensi menghapus watermark evaluasi.  
- **Alat build Java mana yang didukung?** Maven dan Gradle (kedua contoh ditampilkan di bawah).

## Apa itu “cara mengubah koneksi” dalam konteks Excel?
Mengubah koneksi berarti memperbarui informasi sumber data—seperti nama server, database, atau kueri—yang digunakan oleh workbook Excel untuk mengambil data eksternal. Dengan Aspose.Cells, Anda dapat melakukan ini sepenuhnya melalui kode, memungkinkan pembuatan laporan otomatis dan sinkronisasi data.

## Mengapa menggunakan Aspose.Cells Java untuk memodifikasi koneksi Excel?
Anda dapat **mengotomatisasi penyegaran data Excel** tanpa menginstal Microsoft Office. Aspose.Cells berjalan di server mana pun, menangani workbook dengan hingga 1 juta baris tanpa memuat seluruh file ke memori, dan mendukung **lebih dari 70 format input dan output** termasuk XLSX, CSV, dan ODS. Library ini berfungsi konsisten di Windows, Linux, dan macOS, memberikan solusi lintas‑platform yang handal.

## Prasyarat
Sebelum menyelami kode, pastikan Anda memiliki hal berikut:

### Perpustakaan yang Diperlukan
Aspose.Cells untuk Java versi 25.3 atau lebih baru.

### Persyaratan Penyiapan Lingkungan
- Java Development Kit (JDK) terpasang.  
- IDE seperti IntelliJ IDEA, Eclipse, atau NetBeans.

### Prasyarat Pengetahuan
Pengetahuan dasar pemrograman Java dan familiaritas dengan Maven atau Gradle.

## Menyiapkan Aspose.Cells untuk Java
Untuk mulai menggunakan Aspose.Cells dalam proyek Anda, ikuti langkah instalasi di bawah ini.

**Pengaturan Maven**  
Tambahkan dependensi berikut dalam file `pom.xml` Anda:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Pengaturan Gradle**  
Sertakan baris ini dalam file `build.gradle` Anda:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Langkah Akuisisi Lisensi
Aspose.Cells menawarkan trial gratis sehingga Anda dapat mengevaluasi library sebelum membeli. Untuk memulai:
- Kunjungi [halaman trial gratis](https://releases.aspose.com/cells/java/) dan unduh paket evaluasi.  
- Untuk penggunaan komersial, beli lisensi dari [portal pembelian Aspose](https://purchase.aspose.com/buy).  
- Jika Anda memerlukan akses penuh sementara, minta [lisensi sementara](https://purchase.aspose.com/temporary-license/).

Setelah penyiapan Anda siap, kita dapat melanjutkan ke implementasi sebenarnya.

## Panduan Implementasi

### Fitur 1: memuat workbook dari file
**Ikhtisar:** Fitur ini menunjukkan cara **load excel workbook java** menggunakan Aspose.Cells.

#### Instruksi langkah demi langkah
**Tentukan direktori data Anda**  
Pertama, atur folder yang berisi file sumber:

```java
String dataDir = "YOUR_DATA_DIRECTORY";
```
Pastikan `DataConnection.xlsx` ada di folder ini.

**Muat workbook**  
Sekarang bawa workbook ke memori:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook(dataDir + "DataConnection.xlsx");
```
`Workbook` adalah kelas inti yang mewakili seluruh file Excel dalam memori, memberi Anda kontrol programatik penuh atas sheet, sel, dan koneksi.

### Fitur 2: memodifikasi koneksi data dalam workbook
**Ikhtisar:** Pelajari cara mengakses dan **change excel connection string** serta properti koneksi lainnya.

#### Instruksi langkah demi langkah
**Akses koneksi data**  
Ambil koneksi data pertama dari workbook:

```java
import com.aspose.cells.DBConnection;
import com.aspose.cells.ExternalConnection;
import com.aspose.cells.OLEDBCommandType;

ExternalConnection conn = workbook.getDataConnections().get(0);
```
`getDataConnections()` mengembalikan koleksi semua koneksi, memungkinkan Anda bekerja dengan masing‑masing secara individual.

**Modifikasi properti koneksi**  
Perbarui nama koneksi dan jalur file ODC:

```java
conn.setName("MyConnectionName");
conn.setOdcFile(dataDir + "MyDefaulConnection.odc");
```

Lakukan cast ke `DBConnection` untuk perubahan yang lebih mendalam:

```java
DBConnection dbConn = (DBConnection) conn;
dbConn.setCommandType(OLEDBCommandType.SQL_STATEMENT);
dbConn.setCommand("SELECT * FROM AdminTable");

String connectionString = "Server=myServerAddress;Database=myDataBase;User ID=myUsername;Password=myPassword;Trusted_Connection=False";
dbConn.setConnectionInfo(connectionString);
```
`DBConnection` adalah kelas yang mengenkapsulasi pengaturan spesifik database seperti perintah SQL dan connection string, memungkinkan Anda mengarahkan workbook ke server atau database baru.

### Fitur 3: menyimpan workbook ke file
**Ikhtisar:** Setelah menyesuaikan koneksi, Anda ingin **save excel workbook java** dengan pengaturan baru.

#### Instruksi langkah demi langkah
**Tentukan direktori output**  
Tentukan di mana file yang diperbarui harus ditulis:

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
```

**Simpan workbook**  
Simpan perubahan:

```java
workbook.save(outDir + "MESQLDataConnection_out.xlsx");
```
Metode `save()` menulis semua modifikasi kembali ke file fisik, menyelesaikan alur kerja **automate excel data refresh**.

## Aplikasi Praktis
Memahami pengaturan **how to change connection** di Excel membuka pintu ke banyak skenario dunia nyata:

1. **Pelaporan otomatis** – Menghasilkan laporan yang menarik data live dari database tanpa penyegaran manual.  
2. **Sinkronisasi data** – Menjaga dasbor Excel tetap sinkron dengan sistem back‑end, mengurangi risiko data usang.  
3. **Dasbor khusus** – Membuat dasbor interaktif yang mencerminkan perubahan data real‑time untuk tim keuangan atau penjualan.

Mengintegrasikan Aspose.Cells Java ke dalam pipeline CRM, ERP, atau BI dapat secara dramatis mengurangi upaya manual.

## Pertimbangan Kinerja
Saat menangani workbook besar atau set data berat:

- Muat hanya sheet yang Anda butuhkan, jika memungkinkan.  
- Tuliskan kueri SQL yang efisien untuk meminimalkan waktu transfer data.  
- Lepaskan sumber daya segera dengan `workbook.dispose()` ketika workbook tidak lagi diperlukan.  

Mengikuti tip ini membantu mempertahankan kinerja optimal saat Anda **update excel data source** objek.

## Masalah Umum dan Solusinya
| Masalah | Solusi yang Disarankan |
|-------|---------------|
| **Kesalahan connection string** | Verifikasi nama server, nama database, dan kredensial. Uji kueri di klien database terlebih dahulu. |
| **Tidak ada data yang dikembalikan setelah perubahan** | Pastikan perintah SQL sesuai dengan skema target dan pengguna memiliki izin baca. |
| **Watermark evaluasi muncul** | Terapkan lisensi Aspose.Cells yang valid; versi trial menambahkan watermark pada file output. |
| **OutOfMemoryError pada file besar** | Proses workbook dalam potongan atau tingkatkan ukuran heap JVM (`-Xmx`). |

## Pertanyaan yang Sering Diajukan

**T: Bagaimana cara menangani banyak koneksi data dalam sebuah workbook?**  
J: Gunakan `workbook.getDataConnections().get(index)` untuk mengambil setiap koneksi secara individual, kemudian modifikasi sesuai kebutuhan.

**T: Bisakah saya memodifikasi properti workbook lain dengan Aspose.Cells Java?**  
J: Tentu saja. API mendukung pemformatan sel, manajemen worksheet, pembuatan diagram, dan lainnya.

**T: Apa yang harus saya lakukan jika perintah SQL saya gagal saat runtime?**  
J: Periksa kembali connection string dan pastikan pengguna database memiliki izin yang diperlukan. Tinjau detail pengecualian untuk petunjuk.

**T: Di mana saya dapat mendapatkan bantuan jika mengalami masalah?**  
J: Kunjungi [forum Aspose](https://forum.aspose.com/c/cells/9) untuk mengajukan pertanyaan atau menelusuri solusi yang ada.

**T: Apakah ada batasan pada versi trial gratis?**  
J: Versi evaluasi menambahkan watermark pada file yang dihasilkan dan mungkin membatasi ukuran pemrosesan. Versi berlisensi menghapus pembatasan ini.

## Sumber Daya
- **Dokumentasi:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Unduhan:** [Aspose.Cells for Java Releases](https://releases.aspose.com/cells/java/)

---

**Last Updated:** 2026-11-16  
**Tested With:** Aspose.Cells Java 25.3  
**Author:** Aspose  

---

## Tutorial Terkait

- [Aspose.Cells Java: Menguasai Koneksi Workbook Excel untuk Integrasi dan Analisis Data](/cells/java/import-export/aspose-cells-java-excel-connections/)
- [Otomatisasi Pivot Table Excel Menggunakan Aspose.Cells Java untuk Analisis Data](/cells/java/data-analysis/automate-excel-pivot-tables-aspose-cells-java/)
- [Cara Memperbarui Sumber Pivot Table Excel dengan Aspose.Cells untuk Java: Panduan Komprehensif](/cells/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}