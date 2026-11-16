---
category: general
date: 2026-11-16
description: Buat pemformatan bersyarat di Excel menggunakan Python. Pelajari cara
  menambahkan rentang pemformatan bersyarat, menyorot tanggal, dan membuat buku kerja
  secara programatik.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: id
lastmod: 2026-11-16
og_description: Buat pemformatan bersyarat di Excel dengan Python. Tutorial ini menunjukkan
  cara menambahkan rentang pemformatan bersyarat, menyorot tanggal, dan menghasilkan
  workbook.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Buat pemformatan bersyarat di Excel dengan Python – panduan langkah demi
  langkah
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Cara membuat pemformatan bersyarat di Excel dengan Python
url: /id/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat conditional formatting di Excel dengan Python

Jika Anda perlu **membuat conditional formatting** dalam file Excel saat bekerja dengan Python, panduan ini menunjukkan langkah‑langkahnya secara tepat. Anda akan belajar **membuat excel workbook python**‑style, menentukan rentang pemformatan, dan menyorot tanggal tanpa meninggalkan IDE.

Conditional formatting memungkinkan Anda menandai sel secara visual yang memenuhi kriteria tertentu—sempurna untuk dasbor, laporan, atau lembar validasi data. Pada akhir tutorial ini Anda akan memiliki workbook yang berfungsi penuh yang mewarnai sel dengan tanggal “Yesterday” menjadi merah muda sementara sisanya tetap hijau.

## Apa yang akan Anda capai

* Membuat workbook baru dari awal.  
* Menambahkan koleksi conditional‑format untuk blok sel tertentu.  
* Menerapkan aturan **TIME_PERIOD** yang menyorot tanggal (skenario “cara menyorot tanggal”).  
* Menyimpan file sebagai workbook XLSX siap untuk diproses lebih lanjut.

**Prasyarat**  
* Python 3.8+  
* Paket Python `aspose-cells` (`pip install aspose-cells`)  
* Familiaritas dasar dengan modul `datetime` Python  

---

## Cara membuat conditional formatting di Python

Langkah pertama adalah menyiapkan workbook dan worksheet yang akan menampung aturan pemformatan.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Mengapa ini penting** – `Workbook` adalah titik masuk untuk semua operasi Excel. Membuat workbook secara programatik menggantikan langkah manual “File → New”, memungkinkan pipeline laporan otomatis.

---

## Menyiapkan koleksi conditional‑format – menambahkan rentang conditional formatting

Selanjutnya kita mendefinisikan blok sel yang akan menerima aturan. Pada contoh ini rentangnya adalah **I19:K20**.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Penjelasan** – `conditional_formattings.add` mendaftarkan koleksi baru yang terikat pada string alamat. Kondisi pertama (`conds[0]`) berfungsi sebagai gaya “default”; aturan berikutnya akan menimpanya ketika kriterianya terpenuhi.

---

## Menambahkan kondisi TIME_PERIOD – cara menyorot tanggal

Sekarang kita menambahkan logika yang mengidentifikasi tanggal “Yesterday” dan mewarnainya merah muda.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Mengapa menggunakan TIME_PERIOD?** – Aspose.Cells menyediakan enumerasi bawaan seperti `YESTERDAY`, `TODAY`, dan `LAST_WEEK`. Mereka mengevaluasi nilai tanggal sel terhadap tanggal sistem saat ini, sehingga tidak perlu rumus khusus.

---

## Mengisi data contoh – mendemonstrasikan aturan

Untuk melihat pemformatan beraksi, kami menyisipkan tanggal yang cocok dengan aturan dan satu lagi yang tidak.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Catatan kasus tepi** – Aturan `TIME_PERIOD` hanya bekerja dengan tanggal *nyata*. Jika sebuah sel berisi teks (misalnya “N/A”), aturan diabaikan, sehingga tidak terjadi perubahan warna yang tidak diharapkan.

---

## Menyimpan workbook – add conditional formatting python

Akhirnya, tulis workbook ke disk. File dapat dibuka di program spreadsheet apa pun untuk memverifikasi warnanya.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Hasil yang diharapkan**  

| I19 (hijau → merah muda) | J19 (hijau) | K19 (hijau) |
|--------------------------|------------|------------|
| 30/7/2008 (kemarin)      | –          | –          |
| **I20**: label “Kemarin” | –          | –          |
| I21‑K21 (hijau)           | –          | –          |

Sel **I19** muncul dengan latar belakang merah muda karena tanggalnya cocok dengan periode “Yesterday”, sementara **K20** tetap hijau.

---

## Pertanyaan umum dan tip praktis

* **Apakah saya dapat menggunakan rentang tanggal khusus alih‑alih periode bawaan?**  
  Ya. Ganti `condition.time_period` dengan `condition.formula1 = "TODAY()-1"` dan atur `condition.type = FormatConditionType.FORMULA`.

* **Bagaimana jika workbook saya sudah berisi data?**  
  Gunakan `worksheet.cells.import_data` untuk memuat data secara massal sebelum menambahkan koleksi conditional formatting.

* **Kinerja dengan lembar besar?**  
  Menambahkan banyak kondisi dapat memperlambat rendering. Kelompokkan sel dengan aturan yang sama ke dalam satu rentang (misalnya “A1:C1000”) agar jumlah kondisi tetap rendah.

* **Kompatibilitas lintas platform?**  
  File XLSX yang dihasilkan mengikuti standar Office Open XML, sehingga dapat bekerja di aplikasi spreadsheet Windows, macOS, dan Linux.

---

## Kesimpulan

Anda kini tahu cara **membuat conditional formatting** dalam workbook Excel menggunakan Python. Tutorial ini mencakup pembuatan workbook, mendefinisikan **add conditional formatting range**, menerapkan aturan **cara menyorot tanggal**, dan menyimpan file—semua dengan pendekatan **add conditional formatting python** yang disediakan oleh Aspose.Cells.

Dari sini Anda dapat:

* Memperluas set aturan dengan nilai `TimePeriodType` lainnya (misalnya `TODAY`, `LAST_MONTH`).  
* Menggabungkan beberapa kondisi pada rentang yang sama untuk petunjuk visual yang lebih kaya.  
* Mengintegrasikan alur kerja ini ke dalam pipeline pelaporan otomatis atau layanan web.

Selamat coding, dan silakan bereksperimen dengan warna, rentang, serta logika tanggal yang berbeda untuk menyesuaikan kebutuhan pelaporan Anda!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}