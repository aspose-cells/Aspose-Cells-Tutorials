---
date: '2026-03-28'
description: Pelajari cara menambahkan watermark rahasia ke grafik Excel menggunakan
  Aspose.Cells untuk Java, termasuk dependensi Maven Aspose Cells dan gaya WordArt.
keywords:
- Aspose.Cells Java
- Excel chart watermark
- WordArt in Excel
title: Cara Menambahkan Tanda Air Rahasia pada Chart Excel Menggunakan Aspose.Cells
  untuk Java
url: /id/java/charts-graphs/add-wordart-watermark-excel-chart-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menambahkan Watermark Rahasia pada Diagram Excel Menggunakan Aspose.Cells untuk Java

## Pendahuluan

Dalam tutorial ini Anda akan belajar **cara menambahkan watermark rahasia pada diagram Excel** menggunakan Aspose.Cells untuk Java. Watermark WordArt tidak hanya memperkuat merek tetapi juga menandakan kerahasiaan—sempurna untuk laporan yang ditandai “CONFIDENTIAL.” Kami akan memandu proses lengkap, mulai dari menyiapkan dependensi Maven hingga menyimpan workbook akhir.

**Apa yang Akan Anda Pelajari**
- Cara menambahkan watermark WordArt ke diagram Excel menggunakan Aspose.Cells untuk Java.  
- Teknik untuk menyesuaikan transparansi dan format garis watermark diagram.  
- Praktik terbaik untuk menyimpan workbook yang telah dimodifikasi.

## Jawaban Cepat
- **Apa arti kata kunci utama?** Menambahkan watermark rahasia pada diagram Excel melindungi data sensitif.  
- **Perpustakaan apa yang diperlukan?** Aspose.Cells untuk Java (lihat dependensi Maven).  
- **Bisakah saya menyesuaikan efek teks?** Ya, menggunakan opsi `MsoPresetTextEffect`.  
- **Apakah lisensi diperlukan?** Versi percobaan dapat digunakan untuk pengujian; lisensi permanen diperlukan untuk produksi.  
- **Apakah ini akan memengaruhi kinerja?** Dampak minimal; hanya beberapa objek tambahan yang dibuat.

## Apa itu Watermark Rahasia di Excel?
Watermark rahasia adalah teks atau grafik semi‑transparan yang ditempatkan di belakang data diagram untuk menunjukkan bahwa kontennya sensitif. Watermark tetap terlihat pada cetakan dan layar tanpa mengaburkan data di bawahnya.

## Mengapa Menggunakan Aspose.Cells untuk Menambahkan Watermark?
Aspose.Cells menyediakan API yang kaya untuk memanipulasi file Excel tanpa memerlukan Microsoft Office. Ia mendukung bentuk WordArt, kontrol transparansi yang halus, dan bekerja di semua platform Java.

## Prasyarat
- Java Development Kit (JDK) terpasang dan terkonfigurasi.  
- IDE seperti IntelliJ IDEA atau Eclipse.  
- Pengetahuan dasar Java dan familiaritas dengan Maven/Gradle.  

### Perpustakaan yang Diperlukan
Sertakan perpustakaan Aspose.Cells dalam proyek Anda menggunakan Maven atau Gradle seperti ditunjukkan di bawah.

### Persyaratan Penyiapan Lingkungan
- Java Development Kit (JDK) terpasang dan terkonfigurasi.  
- IDE seperti IntelliJ IDEA atau Eclipse untuk pengembangan.

### Prasyarat Pengetahuan
Pemahaman dasar pemrograman Java, manipulasi file Excel dengan Aspose.Cells, dan familiaritas dengan alat build Maven/Gradle sangat disarankan.

## Dependensi Maven Aspose Cells
Untuk mulai menggunakan Aspose.Cells, tambahkan ke proyek Anda.

**Maven:**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

## Akuisisi Lisensi
Dapatkan lisensi melalui opsi pembelian Aspose, atau mulai dengan percobaan gratis dengan mengunduh lisensi sementara dari situs mereka. Inisialisasi pengaturan Anda seperti berikut:
```java
// Load an existing workbook and apply a license if available.
Workbook workbook = new Workbook("path_to_license_file");
```

## Panduan Implementasi
Mari kita uraikan implementasi menjadi bagian-bagian yang jelas.

### Tambahkan Watermark WordArt ke Diagram
1. **Buka File Excel yang Ada**  
   Load your Excel file where you want to add the watermark:
```java
String dataDir = Utils.getSharedDataDir(AddWordArtWatermarkToChart.class) + "TechnicalArticles/";
Workbook workbook = new Workbook(dataDir + "sample.xlsx");
```

2. **Akses Diagram**  
   Get the chart from the first worksheet you wish to modify:
```java
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
```

3. **Tambahkan Bentuk WordArt**  
   Insert a new WordArt shape into your chart's plot area:
```java
Shape wordart = chart.getShapes().addTextEffectInChart(
    MsoPresetTextEffect.TEXT_EFFECT_1,
    "CONFIDENTIAL",
    "Arial Black", 66, false, false, 
    1200, 500, 2000, 3000);
```

4. **Konfigurasi Isi dan Format Garis**  
   Set the transparency to make the watermark subtle:
```java
// Configure transparency.
FillFormat wordArtFormat = wordart.getFill();
wordArtFormat.setTransparency(0.9);

// Make line format invisible.
LineFormat lineFormat = wordart.getLine();
lineFormat.setWeight(0.0);
```

5. **Simpan Workbook**  
   Save your changes to a new file:
```java
workbook.save(dataDir + "AWArtWToC_out.xlsx");
```

### Tips Pemecahan Masalah
- Pastikan semua jalur file ditentukan dengan benar untuk memuat dan menyimpan file.  
- Verifikasi Anda memiliki izin membaca/menulis di direktori.  
- Periksa kompatibilitas versi Aspose.Cells dengan lingkungan Java Anda.

## Aplikasi Praktis
Menambahkan watermark WordArt dapat bermanfaat dalam skenario seperti:

1. **Branding** – Gunakan logo atau slogan perusahaan pada semua diagram untuk konsistensi merek.  
2. **Kerahasiaan** – Tandai laporan rahasia untuk mencegah penyebaran tidak sah.  
3. **Kontrol Versi** – Sertakan nomor versi selama tahap persetujuan dokumen.

## Pertimbangan Kinerja
Saat menggunakan Aspose.Cells, pertimbangkan:

- Manajemen memori yang efisien dengan membuang objek yang tidak lagi diperlukan.  
- Mengoptimalkan kinerja dengan meminimalkan operasi I/O file bila memungkinkan.  
- Menggunakan multi‑threading untuk menangani workbook besar atau manipulasi kompleks.

## Kesimpulan
Sekarang Anda memiliki pemahaman fungsional tentang **cara menambahkan watermark rahasia pada diagram Excel** menggunakan Aspose.Cells untuk Java. Fitur ini meningkatkan daya tarik visual dan menambahkan lapisan keamanan pada dokumen Anda. Untuk eksplorasi lebih lanjut, coba berbagai efek teks atau integrasikan fungsionalitas ini ke dalam aplikasi yang lebih besar.

## Bagian FAQ
1. **Apa itu Aspose.Cells?**  
   - Perpustakaan kuat untuk mengelola file Excel di Java.  
2. **Bagaimana cara memulai dengan Aspose.Cells?**  
   - Instal melalui Maven/Gradle dan siapkan lisensi jika diperlukan.  
3. **Bisakah saya menambahkan efek teks berbeda pada watermark?**  
   - Ya, jelajahi opsi `MsoPresetTextEffect` untuk berbagai gaya.  
4. **Apa masalah umum saat mengatur transparansi?**  
   - Pastikan tingkat transparansi berada antara 0 (tidak tembus) dan 1 (sepenuhnya tembus).  
5. **Di mana saya dapat menemukan lebih banyak sumber tentang Aspose.Cells?**  
   - Kunjungi [Dokumentasi](https://reference.aspose.com/cells/java/) mereka untuk panduan lengkap.

## Sumber Daya
- [Dokumentasi](https://reference.aspose.com/cells/java/)
- [Unduh Versi Terbaru](https://releases.aspose.com/cells/java/)
- [Beli Lisensi](https://purchase.aspose.com/buy)
- [Percobaan Gratis](https://releases.aspose.com/cells/java/)
- [Lisensi Sementara](https://purchase.aspose.com/temporary-license/)
- [Forum Dukungan](https://forum.aspose.com/c/cells/9)

## Pertanyaan yang Sering Diajukan

**Q: Apakah watermark muncul di lembar Excel yang dicetak?**  
A: Ya, bentuk WordArt merupakan bagian dari diagram dan dicetak bersama data diagram.

**Q: Bisakah saya menerapkan watermark yang sama ke beberapa diagram secara otomatis?**  
A: Iterasi melalui `workbook.getWorksheets().get(i).getCharts()` dan terapkan langkah yang sama pada setiap diagram.

**Q: Apakah memungkinkan mengubah warna watermark?**  
A: Tentu—gunakan `wordArtFormat.getSolidFill().setColor(Color.getRGB(255,0,0))` untuk mengatur warna khusus.

**Q: Apakah menambahkan watermark akan meningkatkan ukuran file secara signifikan?**  
A: Peningkatannya minimal, karena hanya satu objek bentuk yang ditambahkan.

**Q: Bagaimana cara menghapus watermark nanti?**  
A: Temukan bentuk tersebut berdasarkan nama atau indeksnya di `chart.getShapes()` dan panggil `shape.delete()`.

---

**Terakhir Diperbarui:** 2026-03-28  
**Diuji Dengan:** Aspose.Cells 25.3 for Java  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}