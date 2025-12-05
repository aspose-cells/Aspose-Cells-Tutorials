---
date: 2025-12-05
description: Pelajari cara menambahkan label data pada diagram dan membuat diagram
  interaktif dengan Java menggunakan Aspose.Cells. Tambahkan tooltip, label data,
  dan fungsi drill‑down.
language: id
linktitle: Add Data Labels Chart with Interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Tambahkan Diagram Label Data dengan Interaktivitas di Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Diagram Label Data dengan Interaktivitas di Aspose.Cells Java

Diagram interaktif memberi pengguna kemampuan untuk menjelajahi data secara langsung. Dalam tutorial ini Anda akan **add data labels chart**—tooltip, label data, dan aksi drill‑down—menggunakan Aspose.Cells untuk Java. Pada akhir tutorial Anda akan memiliki diagram interaktif yang halus dan membuat data kompleks langsung dapat dipahami.

## Quick Answers
- **Perpustakaan apa yang saya butuhkan?** Aspose.Cells for Java  
- **Bisakah saya menambahkan tooltip ke diagram Excel?** Yes – use the API’s data‑label settings.  
- **Jenis diagram mana yang mendukung interaktivitas?** Most built‑in types (column, line, pie, etc.).  
- **Apakah saya memerlukan lisensi untuk produksi?** A valid Aspose.Cells license is required.  
- **Berapa lama implementasinya?** Roughly 10–15 minutes for a basic chart.

## Apa itu “add data labels chart”?
*add data labels chart* adalah diagram di mana setiap titik data menampilkan label (nilai, nama, atau teks khusus) langsung pada visual. Hal ini memudahkan penonton untuk membaca nilai tepat tanpa harus mengarahkan kursor atau merujuk ke legenda terpisah.

## Mengapa membuat solusi diagram interaktif Java?
Menyematkan interaktivitas—tooltip, titik yang dapat diklik, tautan drill‑down—mengubah spreadsheet statis menjadi dasbor eksploratif. Pengguna dapat:
- Dengan cepat mengidentifikasi outlier.
- Mengakses lapisan data yang lebih dalam dengan satu klik.
- Meningkatkan kecepatan pengambilan keputusan dengan mengurangi kebutuhan laporan terpisah.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- Lingkungan pengembangan Java (disarankan JDK 8+).  
- Perpustakaan Aspose.Cells untuk Java (unduh dari [here](https://releases.aspose.com/cells/java/)).  

## Langkah 1: Menyiapkan Proyek Java Anda

1. Buat proyek Java baru di IDE favorit Anda (IntelliJ, Eclipse, VS Code, dll.).  
2. Tambahkan JAR Aspose.Cells untuk Java ke classpath proyek Anda.

## Langkah 2: Memuat Data

Untuk membuat diagram interaktif, Anda terlebih dahulu memerlukan data dalam lembar kerja. Potongan kode di bawah ini memuat workbook yang sudah ada bernama **data.xlsx**.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Langkah 3: Membuat Diagram

Sekarang kita membuat diagram kolom dan menempatkannya pada lembar kerja. Silakan ganti `ChartType.COLUMN` dengan tipe lain jika Anda menginginkannya.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Langkah 4: Menambahkan Interaktivitas – Inti dari “add data labels chart”

### 4.1. Menambahkan Tooltip (add tooltips excel chart)

Tooltip muncul ketika pengguna mengarahkan kursor ke titik data. Kode berikut mengaktifkannya dengan menyalakan label data dan menampilkan nilai.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Menambahkan Label Data (add data labels chart)

Label data adalah teks visual yang berada di sebelah setiap titik. Potongan kode ini mengonfigurasi diagram untuk menampilkan label panggilan alih-alih nilai biasa.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Menerapkan Drill‑Down (create interactive chart java)

Drill‑down memungkinkan pengguna mengklik sebuah titik dan melompat ke tampilan detail. Di sini kami menempelkan hyperlink ke titik data pertama; Anda dapat mengulangi ini untuk titik mana pun yang diperlukan.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Langkah 5: Menyimpan Workbook

Setelah mengonfigurasi diagram, simpan workbook ke file baru sehingga Anda dapat membukanya di Excel dan menguji interaktivitas.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Masalah Umum & Tips

| Masalah | Solusi |
|-------|----------|
| **Tooltip tidak muncul** | Pastikan `setHasDataLabels(true)` dipanggil sebelum mengatur `ShowValue`. |
| **Hyperlink tidak dapat diklik** | Verifikasi bahwa URL terbentuk dengan baik dan pengaturan keamanan Excel mengizinkan tautan eksternal. |
| **Jenis diagram tidak cocok** | Beberapa jenis diagram (mis., radar) memiliki dukungan label terbatas—pilih jenis yang kompatibel seperti kolom atau garis. |
| **Keterlambatan kinerja pada set data besar** | Batasi jumlah titik dengan label data; pertimbangkan menggunakan `setShowValue(false)` untuk seri yang kurang penting. |

## Pertanyaan yang Sering Diajukan

**Q: Bagaimana cara mengubah jenis diagram?**  
A: Ubah enum `ChartType` pada baris pembuatan diagram (mis., `ChartType.LINE` untuk diagram garis).

**Q: Bisakah saya menyesuaikan tampilan tooltip?**  
A: Ya—gunakan properti font, warna latar belakang, dan border objek `DataLabel` untuk menata tooltip.

**Q: Bagaimana cara menangani interaksi pengguna dalam aplikasi web?**  
A: Ekspor workbook ke halaman HTML atau gunakan Aspose.Cells Cloud untuk merender diagram, kemudian tangkap peristiwa klik dengan JavaScript.

**Q: Di mana saya dapat menemukan contoh dan dokumentasi lebih lanjut?**  
A: Kunjungi [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) untuk daftar lengkap kelas dan metode terkait diagram.

## Kesimpulan

Dalam panduan ini kami menunjukkan cara menambahkan fitur **add data labels chart** dan membuat solusi **interactive chart Java** dengan Aspose.Cells. Dengan menambahkan tooltip, panggilan data, dan hyperlink drill‑down, Anda mengubah diagram Excel statis menjadi alat eksplorasi data dinamis yang meningkatkan wawasan dan kegunaan.

---

**Terakhir Diperbarui:** 2025-12-05  
**Diuji Dengan:** Aspose.Cells for Java 24.12  
**Penulis:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}