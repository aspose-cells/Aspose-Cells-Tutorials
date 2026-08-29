---
category: general
date: 2026-08-01
description: Buat workbook Excel dengan Python menggunakan Aspose.Cells – pelajari
  cara menyesuaikan lebar kolom secara otomatis, memformat sel berdasarkan tanggal,
  mengatur format tanggal sel, dan menerapkan pemformatan bersyarat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- auto fit excel column
- format cells by date
- set cell date format
- aspose cells conditional formatting
language: id
lastmod: 2026-08-01
og_description: Buat workbook Excel dengan Python secara instan. Ikuti panduan ini
  untuk menyesuaikan lebar kolom Excel secara otomatis, memformat sel berdasarkan
  tanggal, mengatur format tanggal sel, dan menguasai format bersyarat Aspose Cells.
og_image_alt: Screenshot showing a Python script that creates an Excel workbook using
  Aspose.Cells
og_title: Buat Workbook Excel dengan Python – Langkah demi Langkah dengan Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-01'
  description: Create Excel workbook python using Aspose.Cells – learn auto fit excel
    column, format cells by date, set cell date format and apply conditional formatting.
  headline: Create Excel Workbook Python – Full Guide with Aspose.Cells
  type: TechArticle
tags:
- Aspose Cells
- Python
- Excel automation
- Conditional Formatting
- Date handling
title: Membuat Workbook Excel dengan Python – Panduan Lengkap dengan Aspose.Cells
url: /id/python/formatting/create-excel-workbook-python-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Workbook Excel dengan Python – Panduan Lengkap dengan Aspose.Cells

Pernah bertanya-tanya bagaimana cara **create Excel workbook python** skrip yang tampak rapi tanpa harus membuka Excel secara manual? Anda tidak sendirian. Baik Anda sedang membangun dasbor pelaporan atau mengotomatisasi dump data harian, kemampuan menghasilkan file Excel dari Python adalah pengubah permainan.

> **Pro tip:** Aspose.Cells for Python via .NET memungkinkan Anda bekerja dengan file Excel tanpa ketergantungan COM, menjadikannya sempurna untuk kontainer Linux atau pipeline CI.

## Apa yang Anda Butuhkan

- **Python 3.8+** (kode berjalan pada versi terbaru apa pun)  
- **Aspose.Cells for Python via .NET** – instal dengan `pip install aspose-cells`  
- Sebuah folder yang dapat Anda tulis (kami akan menyebutnya `YOUR_DIRECTORY`)  
- Pemahaman dasar tentang fungsi dan objek Python (tidak memerlukan pengetahuan Excel yang mendalam)  

Jika Anda sudah memiliki semua ini, bagus—mari kita mulai.

## Langkah 1: Membuat Excel Workbook Python – Inisialisasi Workbook

Hal pertama yang kita lakukan adalah membuat objek workbook baru. Anggaplah ini sebagai kanvas kosong di mana setiap operasi selanjutnya menambahkan elemen baru.

```python
from aspose.cells import Workbook, SaveFormat, FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color
from datetime import datetime
import os

# Create a new workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

> **Mengapa ini penting:** `Workbook()` membuat representasi dalam memori dari file `.xlsx`. Dengan mengakses `worksheets[0]` kita mendapatkan lembar default, siap untuk data dan pemformatan.

## Langkah 2: Tentukan Rentang Target dan Warna Dasar – Persiapan untuk Conditional Formatting

Sebelum menambahkan logika kondisional apa pun, kita memerlukan rentang yang akan menampung aturan. Rentang `I19:K20` dipilih secara sembarangan namun cukup besar untuk menampilkan beberapa sel.

```python
# Add a conditional formatting collection to the range and set a base colour
conds = worksheet.conditional_formattings.add("I19:K20", Color.medium_sea_green)
```

Metode `add` sekaligus membuat objek pemformatan dan memberikan latar belakang default, sehingga aturan selanjutnya menjadi menonjol.

## Langkah 3: Aspose Cells Conditional Formatting – Terapkan Aturan TIME_PERIOD untuk YESTERDAY

Sekarang kita sampai pada inti demo: kondisi **TIME_PERIOD** yang menyorot sel yang berisi tanggal kemarin.

```python
# Insert a TIME_PERIOD condition for YESTERDAY
condition_index = conds.add_condition(FormatConditionType.TIME_PERIOD)
condition = conds[condition_index]

# Configure the rule – yesterday, pink background, solid fill
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

> **Penjelasan:** `FormatConditionType.TIME_PERIOD` memberi tahu Aspose bahwa kita menangani aturan berbasis tanggal. Dengan mengatur `time_period` ke `YESTERDAY`, mesin secara otomatis mengevaluasi nilai setiap sel terhadap hari kalender sebelumnya.

## Langkah 4: Isi Tanggal Contoh – Atur Format Tanggal Sel dan Verifikasi Aturan

Untuk melihat aturan beraksi kita memerlukan tanggal nyata. Kita juga akan **set cell date format** sehingga nilai muncul sebagai tanggal yang dapat dibaca.

```python
# Cell I19 – a date that falls on “yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))          # July 30, 2008 is “yesterday” for demo purposes
style_i19 = cell_i19.get_style()
style_i19.number = 30          # 30 = built‑in Excel date format (e.g., mm/dd/yyyy)
cell_i19.set_style(style_i19)

# Cell K20 – a date outside the period (no formatting applied)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)
```

Perhatikan bagaimana kita menggunakan nomor **format cells by date** yang sama (`30`) untuk kedua sel. Ini memastikan tanggal ditampilkan secara konsisten, terlepas dari locale sistem.

## Langkah 5: Tambahkan Label Deskriptif – Buat Sheet Menjadi Self‑Explanatory

Label kecil membantu siapa pun yang membuka file memahami apa yang diwakili oleh sel berwarna.

```python
worksheet.cells.get("I20").put_value("Yesterday")
```

## Langkah 6: Auto Fit Excel Column – Sesuaikan Lebar Kolom Secara Otomatis

Saat Anda menghasilkan data secara programatik, lebar kolom sering tetap pada ukuran sempit default. Metode **auto fit excel column** memperluasnya cukup untuk menampilkan konten.

```python
# Auto‑fit the 12th column (which corresponds to column L) so the label is fully visible
worksheet.auto_fit_column(12)
```

> **Mengapa kolom 12?** Dalam indeks berbasis nol, kolom `12` berkorespondensi dengan kolom Excel `L`. Sesuaikan indeks jika Anda mengubah tata letak.

## Langkah 7: Simpan Workbook – Ekspor ke File Nyata

Akhirnya, kita menyimpan semuanya ke disk. Flag `SaveFormat.XLSX` memastikan workbook modern berbasis zip.

```python
output_file = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_file, SaveFormat.XLSX)
print(f"Workbook saved to {output_file}")
```

### Hasil yang Diharapkan

Buka `TimePeriodDemo.out.xlsx` di Excel (atau penampil apa pun) dan Anda akan melihat:

- Sel **I19** disorot dengan **pink** karena tanggalnya cocok dengan “yesterday”.  
- Sel **K20** tidak berubah, menunjukkan bahwa aturan kondisional dengan benar mengabaikan tanggal di luar periode.  
- Kolom **L** otomatis disesuaikan sehingga label “Yesterday” tidak terpotong.

![Contoh pembuatan workbook Excel python](/images/create_excel_workbook_python.png){: .center-image alt="Contoh pembuatan workbook Excel python"}

## Variasi Umum & Kasus Tepi

| Situasi | Cara Menyesuaikan |
|-----------|---------------|
| **Rentang tanggal berbeda** | Ubah `condition.time_period` menjadi `TimePeriodType.TODAY`, `TimePeriodType.LAST_7_DAYS`, dll. |
| **Beberapa kondisi** | Panggil `conds.add_condition()` lagi dan konfigurasikan `FormatConditionType` baru (mis., `FORMAT_CONDITION_TYPE.EXPRESSION`). |
| **Format tanggal khusus** | Gunakan `style_i19.number = 14` untuk `mm-dd-yy` atau tetapkan string format khusus melalui `style_i19.custom = "dd-mmm-yyyy"`. |
| **Worksheet besar** | Bungkus pemanggilan `auto_fit_column` dalam blok try/except untuk menghindari penurunan kinerja pada file yang sangat besar. |
| **Menjalankan di CI tanpa UI** | Tidak diperlukan UI; Aspose beroperasi sepenuhnya dalam memori, sehingga Anda dapat menghasilkan file di dalam kontainer Docker tanpa Excel terinstal. |

## Ringkasan – Apa yang Telah Dibahas

- **Create Excel workbook python** dari awal dengan Aspose.Cells.  
- **Auto fit excel column** untuk menjaga output tetap rapi.  
- **Format cells by date** dan **set cell date format** untuk tampilan konsisten.  
- Terapkan **aspose cells conditional formatting** menggunakan tipe `TIME_PERIOD`.

## Langkah Selanjutnya

Jika Anda telah menguasai dasar-dasarnya, pertimbangkan untuk menjelajahi:

- **Data bars, color scales, dan icon sets** untuk styling kondisional yang lebih kaya.  
- **Pembuatan PivotTable** melalui `worksheet.pivot_tables.add()`.  
- **Ekspor ke PDF** dengan `workbook.save("report.pdf", SaveFormat.PDF)`.  

Setiap topik ini dibangun di atas konsep dasar yang sama yang kami gunakan di sini, sehingga Anda akan merasa nyaman.

---

*Selamat coding! Jika Anda mengalami kendala, tinggalkan komentar di bawah atau periksa dokumentasi Aspose.Cells for Python untuk penjelasan lebih mendalam.*

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang dibangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Auto-Fit Baris & Kolom di Excel menggunakan Aspose.Cells Java untuk Manajemen Workbook Tanpa Hambatan](/cells/english/java/range-management/aspose-cells-java-auto-fit-rows-columns/)
- [Membuat Workbook Excel menggunakan Aspose.Cells di Java: Panduan Langkah demi Langkah](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Otomatisasi Lebar Kolom Excel: Auto-Fit Kolom menggunakan Aspose.Cells untuk .NET](/cells/english/net/range-management/excel-automation-auto-fit-columns-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}