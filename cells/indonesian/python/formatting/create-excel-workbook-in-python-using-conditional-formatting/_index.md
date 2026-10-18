---
category: general
date: 2026-09-21
description: Pelajari cara membuat workbook Excel di Python, mengatur warna latar
  belakang sel, dan menerapkan pemformatan bersyarat berbasis tanggal dengan Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: id
lastmod: 2026-09-21
og_description: Buat workbook Excel di Python, atur warna latar belakang sel, dan
  terapkan pemformatan bersyarat berbasis tanggal menggunakan Aspose.Cells. Ikuti
  panduan langkah demi langkah.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Buat workbook Excel di Python dengan pemformatan bersyarat
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Buat buku kerja Excel di Python menggunakan pemformatan bersyarat
url: /id/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Workbook Excel di Python dengan Pemformatan Bersyarat

Jika Anda perlu **create Excel workbook python** skrip yang menyorot tanggal secara otomatis, panduan ini menunjukkan cara melakukannya secara tepat. Anda akan melihat cara **set cell background color**, menambahkan aturan “Yesterday”, dan menyimpan file—semua dengan Aspose.Cells untuk Python.

Bekerja dengan file Excel secara programatik sering berarti mengulangi logika pemformatan yang sama di banyak lembar. Pada akhir tutorial ini Anda akan memiliki pola yang dapat digunakan kembali untuk **excel conditional formatting python** yang dapat Anda sisipkan ke proyek mana pun.

## Prerequisites

- Python 3.8+ terinstal  
- paket `aspose-cells` (`pip install aspose-cells`)  
- Familiaritas dasar dengan fungsi Python dan modul datetime  

Tidak ada pustaka tambahan yang diperlukan; Aspose.Cells menangani semua operasi Excel.

## Step 1: Create the workbook and access the first worksheet

Langkah pertama adalah **create excel workbook python** objek dan mengambil worksheet default. Ini memberi Anda kanvas bersih untuk styling lebih lanjut.

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Why this matters:* `Workbook()` membuat file Excel di memori. Mengakses `worksheets[0]` menghindari hard‑coding nama sheet dan tetap berfungsi meskipun nama default berubah.

## Step 2: Helper to add a TIME_PERIOD conditional format

Agar kode tetap rapi, kami membungkus pembuatan conditional‑format dalam sebuah helper. Helper ini menerima rentang sel, warna latar belakang, dan aturan time‑period yang diinginkan.

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*Why this matters:* Helper ini mengabstraksi langkah‑langkah berulang dalam membuat conditional format, sehingga mudah digunakan kembali untuk aturan berbasis tanggal lain seperti “Today” atau “Last Week”.

## Step 3: Apply the “Yesterday” rule to a range

Sekarang kami menggunakan helper untuk menyorot sel yang berisi tanggal kemarin. Rentang `I19:K20` akan berubah menjadi **medium sea green** ketika kondisi terpenuhi.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Why this matters:* `TimePeriodType.YESTERDAY` merupakan bagian dari enumerasi bawaan Aspose.Cells, jadi Anda tidak perlu menghitung tanggal secara manual. Library mengevaluasi aturan setiap kali workbook dibuka.

## Step 4: Populate the range with sample dates

Untuk melihat aturan beraksi, kami menulis dua tanggal—satu yang cocok dengan “Yesterday” dan satu yang tidak. Gaya `number` `30` sesuai dengan format tanggal bawaan.

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*Why this matters:* Dengan memasukkan tanggal konkret Anda dapat memverifikasi bahwa conditional formatting berfungsi tanpa harus membuka file pada hari tertentu.

## Step 5: Add a descriptive label and auto‑fit the column

Label kecil menjelaskan tujuan rentang yang diformat, dan `auto_fit_column` membuat lembar menjadi mudah dibaca.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## Step 6: Save the workbook

Akhirnya, tulis workbook ke disk. Pemanggilan `os.makedirs` memastikan folder target ada.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Saat Anda membuka *TimePeriodDemo.xlsx* Anda akan melihat:

- Sel **I19** berwarna **medium sea green** karena nilainya cocok dengan aturan “Yesterday”.  
- Sel **K20** tetap dengan latar belakang default karena tanggalnya tidak memenuhi kondisi.  

Ini mendemonstrasikan **format cells by date** menggunakan satu baris kode Python.

## Full, runnable example

Menggabungkan semua bagian, berikut skrip lengkap yang dapat Anda salin‑tempel dan jalankan:

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Jalankan skrip, buka file yang dihasilkan, dan Anda akan melihat conditional formatting beraksi.

## Common variations and edge cases

| Variation | How to implement | When to use |
|-----------|------------------|-------------|
| **Highlight “Today”** | Ganti `TimePeriodType.YESTERDAY` dengan `TimePeriodType.TODAY` | Dashboard real‑time |
| **Multiple ranges** | Panggil `add_time_period` untuk setiap rentang, dengan warna berbeda | Laporan kompleks |
| **Dynamic date range** | Gunakan `TimePeriodType.LAST_7_DAYS` atau `TimePeriodType.NEXT_MONTH` | Laporan bergulir |
| **Custom color** | Gunakan `Color.from_argb(255, r, g, b)` untuk membuat nuansa apa pun | Styling konsisten merek |

**Pro tip:** Selalu set `condition.style.pattern = BackgroundType.SOLID` ketika Anda menginginkan isian solid; jika tidak, Excel mungkin menampilkan gradien yang tampak tidak konsisten di berbagai versi.

## Conclusion

Anda kini tahu cara **create Excel workbook python** skrip yang **set cell background color**, menerapkan **excel conditional formatting python**, dan **format cells by date** menggunakan Aspose.Cells. Contoh ini mencakup skenario **date based conditional formatting**, tetapi pola yang sama dapat diterapkan untuk aturan time‑period apa pun.

Selanjutnya, Anda dapat menjelajahi:

- Menambahkan data bars atau icon sets (`FormatConditionType.DATA_BAR`)  
- Menggabungkan beberapa aturan bersyarat pada rentang yang sama  
- Mengekspor workbook ke PDF (`SaveFormat.PDF`) untuk pelaporan  

Silakan bereksperimen dengan warna, rentang, dan tipe time‑period yang berbeda untuk menyesuaikan kebutuhan pelaporan spesifik Anda. Selamat coding!

## What Should You Learn Next?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel Automation with Aspose.Cells .NET&#58; Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}