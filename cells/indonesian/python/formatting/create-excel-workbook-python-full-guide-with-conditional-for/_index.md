---
category: general
date: 2026-07-14
description: Buat kode Python untuk workbook Excel yang mengatur warna latar belakang
  sel, menyorot sel berdasarkan rentang tanggal, dan menyimpan workbook sebagai XLSX
  dalam hitungan menit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: id
lastmod: 2026-07-14
og_description: Buat workbook Excel dengan Python secara instan. Pelajari cara mengatur
  warna latar belakang sel, menyorot sel berdasarkan rentang tanggal, dan menyimpan
  workbook sebagai XLSX dengan Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Buat Workbook Excel dengan Python – Format Bersyarat Langkah demi Langkah
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Membuat Workbook Excel dengan Python – Panduan Lengkap dengan Pemformatan Bersyarat
url: /id/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Workbook Excel dengan Python – Panduan Lengkap dengan Pemformatan Bersyarat

Pernah bertanya-tanya bagaimana cara **create excel workbook python** skrip yang tampak rapi tanpa harus membuka Excel secara manual? Anda tidak sendirian. Dalam banyak proyek berbasis data, kita perlu menghasilkan spreadsheet, memberi warna pada sel, dan bahkan menandai tanggal yang berada dalam rentang tertentu—semua dari kode Python murni.

Pada tutorial ini kami akan membahas contoh lengkap yang siap dijalankan yang **creates an Excel workbook python** menggunakan library Aspose.Cells, **sets cell background color**, menerapkan **conditional formatting based on date**, dan akhirnya **saves workbook as xlsx**. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali dan dapat dimasukkan ke dalam pipeline otomatisasi mana pun.

## Apa yang Akan Anda Pelajari

- Cara menginisialisasi workbook dan mengambil worksheet pertama.  
- Fungsi pembantu yang menambahkan koleksi conditional‑formatting untuk rentang sel apa pun.  
- Menggunakan **conditional formatting based on date** untuk menyoroti entri kemarin.  
- Menyesuaikan lebar kolom untuk tata letak yang rapi.  
- Menyimpan hasil dengan **save workbook as xlsx**.  

Tidak diperlukan instalasi Excel eksternal—Aspose.Cells menangani semuanya di memori.

## Prasyarat

- Python 3.8+ terinstal.  
- Paket `aspose-cells` (`pip install aspose-cells`).  
- Familiaritas dasar dengan fungsi Python dan objek datetime.  

Jika Anda belum pernah menggunakan Aspose.Cells sebelumnya, anggaplah itu sebagai API Python murni yang kuat yang meniru model objek Excel. Ini sempurna untuk pembuatan sisi server di mana suite Office tidak tersedia.

## Langkah 1: Inisialisasi Workbook (Create Excel Workbook Python)

Pertama-tama, kita perlu **create excel workbook python**. Langkah ini membuat objek workbook kosong dan mengarahkan kita ke worksheet default.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **Mengapa ini penting:** Kelas `Workbook` adalah titik masuk untuk setiap operasi Excel. Dengan membuatnya secara programatik, kita menghindari penanganan file manual.

## Langkah 2: Pembantu untuk Menambahkan Koleksi Conditional‑Formatting (Set Cell Background Color)

Pemformatan bersyarat berada di dalam *koleksi* yang terlampir pada sebuah rentang. Mari kita bungkus boilerplate tersebut dalam sebuah pembantu kecil yang juga memungkinkan kita **set cell background color** untuk seluruh rentang.

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **Tip pro:** Menggunakan pembantu membuat alur utama Anda tetap bersih dan memudahkan penggunaan kembali logika yang sama untuk beberapa rentang.

## Langkah 3: Terapkan Conditional Formatting Berdasarkan Tanggal (Sorot Sel Berdasarkan Rentang Tanggal)

Sekarang kita akan **highlight cells based on date range**. Contoh ini berfokus pada “kemarin” tetapi Anda dapat mengganti `TimePeriodType.YESTERDAY` dengan `TODAY`, `LAST_WEEK`, dll.

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **Apa yang terjadi?**  
> 1. Pertama kami memberi seluruh rentang latar belakang hijau netral.  
> 2. Kemudian kami menambahkan kondisi `TIME_PERIOD` yang mengganti isi dengan warna merah muda **hanya** ketika tanggal sel sama dengan kemarin.  
> 3. Enum `TimePeriodType` mengabstraksi perhitungan tanggal, sehingga Anda tidak perlu menulis logika khusus.

## Langkah 4: Isi Tanggal Contoh (Agar Aturan Dapat Dievaluasi)

Untuk melihat aturan beraksi, kami akan menambahkan beberapa tanggal ke lembar. Satu berada dalam jendela “kemarin”, yang lainnya tidak.

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **Catatan kasus tepi:** Jika workbook Anda akan dibuka di locale yang berbeda, pertimbangkan menggunakan `date_style.custom = "dd‑mm‑yyyy"` untuk memastikan tampilan yang konsisten.

## Langkah 5: Rapikan Tata Letak (Auto‑Fit Columns)

Spreadsheet yang sempit terlihat tidak profesional. Mari **adjust column width for a tidy output**.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **Mengapa auto‑fit?** Ini memastikan bahwa label atau tanggal yang panjang terlihat sepenuhnya, yang terutama penting ketika Anda membagikan file kepada pemangku kepentingan non‑teknis.

## Langkah 6: Simpan Workbook (Save Workbook As XLSX)

Akhirnya, kami **save workbook as xlsx** ke lokasi pilihan Anda. Konstanta `SaveFormat.XLSX` memberi tahu Aspose.Cells untuk menulis dalam format OpenXML modern.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Hasil yang akan Anda lihat:**  
> - Sel I19 dan K20 berisi tanggal.  
> - I19 (kemarin) disorot merah muda, sementara K20 tetap hijau.  
> - Kolom L secara otomatis memperluas untuk menampung label “Yesterday”.  

Jika Anda membuka `TimePeriodDemo.xlsx` di Excel, conditional formatting sudah diterapkan—tidak diperlukan langkah tambahan.

---

![Lembar Excel yang menampilkan tanggal kemarin yang disorot](https://example.com/images/excel-demo.png "Tangkapan layar file Excel yang dihasilkan dengan sel yang disorot")

*Gambar di atas menggambarkan workbook akhir; perhatikan sorotan merah muda pada sel yang berisi tanggal kemarin.*

## Ringkasan: Apa yang Kami Capai

- **Created an Excel workbook python** dari awal menggunakan Aspose.Cells.  
- **Set cell background color** untuk seluruh rentang guna memberikan petunjuk visual pada sheet.  
- Menerapkan **conditional formatting based on date** untuk secara otomatis menandai entri kemarin.  
- **Saved workbook as xlsx**, siap untuk distribusi atau pemrosesan lebih lanjut.  

Semua ini dilakukan dalam kurang dari 60 baris Python, dan kode tersebut bekerja di platform apa pun yang mendukung runtime Aspose.Cells.

## Langkah Selanjutnya & Topik Terkait

Jika Anda menemukan ini berguna, Anda mungkin juga ingin menjelajahi:

- **set cell background color** untuk seluruh baris berdasarkan nilai status (mis., “Completed”, “Pending”).  
- Menggunakan **highlight cells based on date range** untuk membuat jendela bergulir (7 hari terakhir, bulan berjalan).  
- Mengekspor ke format lain seperti **CSV** atau **PDF** dengan `SaveFormat.CSV` atau `SaveFormat.PDF`.  
- Menambahkan **charts** secara programatik untuk memvisualisasikan data yang baru saja Anda format.  

Silakan ubah logika tanggal, ganti palet warna, atau perluas rentang untuk mencakup seluruh kolom. Polanya tetap sama: buat workbook, lampirkan koleksi conditional‑formatting, definisikan aturan, dan simpan.

Ada pertanyaan tentang kasus penggunaan tertentu? Tinggalkan komentar di bawah, dan selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda.

- [Otomatisasi Excel dengan Aspose.Cells .NET: Buat Workbook & Atur Tautan Eksternal](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Buat & Simpan Workbook Excel Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Buat & Simpan Workbook Excel Aspose Cells .NET](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}