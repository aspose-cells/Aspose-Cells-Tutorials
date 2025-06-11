---
"date": "2025-04-07"
"description": "Pelajari cara mengonversi file Excel ke format CSV secara efisien menggunakan Aspose.Cells untuk Java. Panduan ini membahas cara memuat, mengonfigurasi, dan menyimpan buku kerja dengan langkah-langkah terperinci."
"title": "Cara Memuat dan Menyimpan Excel sebagai CSV Menggunakan Aspose.Cells untuk Java&#58; Panduan Lengkap"
"url": "/id/java/workbook-operations/aspose-cells-java-load-save-excel-csv/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Cara Memuat dan Menyimpan Excel sebagai CSV Menggunakan Aspose.Cells untuk Java
## Bevezetés
Mengonversi kumpulan data Excel ke format teks seperti CSV sambil mempertahankan detail tertentu seperti pemisah bisa jadi sulit. Panduan lengkap ini menunjukkan cara menggunakan Aspose.Cells untuk Java untuk memuat, mengonfigurasi, dan menyimpan buku kerja Excel sebagai file CSV secara efisien. Di akhir tutorial ini, Anda akan menguasai proses ini dalam aplikasi Java Anda.

**Amit tanulni fogsz:**
- Memuat file Excel yang ada ke dalam objek Buku Kerja menggunakan Aspose.Cells
- Mengonfigurasi TxtSaveOptions untuk mengelola pemisah untuk baris kosong
- Menyimpan buku kerja Anda sebagai file CSV dengan konfigurasi tertentu

## Előfeltételek
Kezdés előtt győződjön meg arról, hogy a következőkkel rendelkezik:
- **Lingkungan Pengembangan Java:** JDK terinstal dan dikonfigurasi.
- **Aspose.Cells untuk Pustaka Java:** Diperlukan versi 25.3 atau yang lebih baru.
- **IDE:** Gunakan IntelliJ IDEA, Eclipse, atau lingkungan pengembangan apa pun yang disukai.

## Menyiapkan Aspose.Cells untuk Java
### Ketergantungan Maven
Untuk memasukkan Aspose.Cells ke dalam proyek Maven Anda, tambahkan ini ke `pom.xml`:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```
### Ketergantungan Gradle
Untuk pengguna Gradle, tambahkan ini ke `build.gradle`:
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```
## Licenc megszerzése
Aspose.Cells untuk Java menawarkan lisensi percobaan dan komersial. Mulailah dengan [ingyenes próba](https://releases.aspose.com/cells/java/) untuk mengeksplorasi kemampuannya atau membeli lisensi jika sesuai. Untuk lisensi sementara, kunjungi [ideiglenes licencoldal](https://purchase.aspose.com/temporary-license/).
## Megvalósítási útmutató
### Excel munkafüzet betöltése
**Áttekintés:**
Memuat file Excel ke Aspose.Cells mudah dan penting untuk operasi selanjutnya.
#### Lépésről lépésre:
1. **Impor Kelas yang Diperlukan**
   Impor `Workbook` kelas dari paket Aspose.Cells:
   ```java
   import com.aspose.cells.Workbook;
   ```
2. **Memuat File Excel**
   Buat contoh Buku Kerja dengan jalur file Anda:
   ```java
   String dataDir = "YOUR_DATA_DIRECTORY";
   Workbook workbook = new Workbook(dataDir + "/KeepSeparatorsForBlankRow.xlsx");
   ```
### Mengonfigurasi TxtSaveOptions untuk Penanganan Pemisah
**Áttekintés:**
Sesuaikan cara penyimpanan file teks, termasuk mempertahankan pemisah di baris kosong dengan `TxtSaveOptions`.
#### Lépésről lépésre:
1. **Impor Kelas TxtSaveOptions**
   Impor kelas yang diperlukan untuk mengonfigurasi opsi penyimpanan:
   ```java
   import com.aspose.cells.TxtSaveOptions;
   ```
2. **Atur Opsi untuk Mempertahankan Pemisah**
   Konfigurálás `TxtSaveOptions` untuk mempertahankan pemisah pada baris kosong:
   ```java
   TxtSaveOptions options = new TxtSaveOptions();
   options.setKeepSeparatorsForBlankRow(true);
   ```
### Menyimpan Buku Kerja sebagai File CSV dengan Opsi
**Áttekintés:**
Langkah ini melibatkan penyimpanan buku kerja Anda sebagai berkas teks, khususnya CSV dalam contoh ini.
#### Lépésről lépésre:
1. **Siapkan Jalur Penyimpanan**
   Tentukan lokasi penyimpanan keluaran:
   ```java
   String outDir = "YOUR_OUTPUT_DIRECTORY";
   ```
2. **Simpan Buku Kerja dengan Opsi yang Dikonfigurasi**
   Használd a `save` metode untuk menulis buku kerja Anda sebagai file CSV, menerapkan opsi yang dikonfigurasi:
   ```java
   Workbook workbook = new Workbook("YOUR_DATA_DIRECTORY/KeepSeparatorsForBlankRow.xlsx");
   TxtSaveOptions options = new TxtSaveOptions();
   options.setKeepSeparatorsForBlankRow(true);
   workbook.save(outDir + "/KeepSeparatorsForBlankRow.out.csv", options);
   ```
## Gyakorlati alkalmazások
1. **Ekspor Data untuk Pelaporan:** Mengubah data Excel ke format CSV untuk alat pelaporan.
2. **Skrip Pemrosesan Batch:** Mengotomatiskan konversi beberapa file Excel dalam satu direktori.
3. **Integráció adatbázisokkal:** Siapkan dan ekspor data Excel sebagai CSV untuk impor basis data.
## Teljesítménybeli szempontok
Untuk menangani kumpulan data besar secara efisien:
- Optimalkan penggunaan memori dengan melepaskan sumber daya segera menggunakan `workbook.dispose()`.
- Memanfaatkan pengumpulan sampah Java untuk mengelola memori secara efektif dalam aplikasi yang berjalan lama.
- Profilkan aplikasi Anda untuk mengatasi hambatan I/O file apa pun.
## Következtetés
Kini Anda memahami cara memuat, mengonfigurasi, dan menyimpan buku kerja Excel sebagai file CSV menggunakan Aspose.Cells untuk Java. Panduan ini berfungsi sebagai dasar untuk mengintegrasikan kemampuan ini ke dalam aplikasi Anda.
**Következő lépések:**
Jelajahi lebih lanjut fitur Aspose.Cells seperti manipulasi data dan pemformatan lanjutan untuk meningkatkan fungsionalitas.
## GYIK szekció
1. **Bagaimana cara menangani file besar dengan Aspose.Cells?**
   - Gunakan API streaming dan optimalkan penggunaan memori dengan membuang sumber daya secara cepat.
2. **Dapatkah saya menggunakan Aspose.Cells tanpa lisensi untuk produksi?**
   - Lisensi komersial diperlukan untuk produksi; mulailah dengan uji coba untuk mengeksplorasi kemampuan.
3. **Bagaimana cara menangani pembatas CSV yang berbeda?**
   - Konfigurálás `TxtSaveOptions` menggunakan metode seperti `setSeparator(';')`.
4. **Bagaimana jika buku kerja saya berisi rumus?**
   - Aspose.Cells akan menghitung dan mengekspor hasil rumus saat menyimpan ke format teks.
5. **Bisakah saya menyesuaikan format sel selama konversi?**
   - Ya, jelajahi opsi tambahan dalam Aspose.Cells untuk gaya dan presentasi data.
## Erőforrás
- [Aspose.Cells dokumentáció](https://reference.aspose.com/cells/java/)
- [Aspose.Cells letöltése](https://releases.aspose.com/cells/java/)
- [Licenc vásárlása](https://purchase.aspose.com/buy)
- [Ingyenes próbaverzió](https://releases.aspose.com/cells/java/)
- [Ideiglenes engedély](https://purchase.aspose.com/temporary-license/)
- [Aspose Támogatási Fórum](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}