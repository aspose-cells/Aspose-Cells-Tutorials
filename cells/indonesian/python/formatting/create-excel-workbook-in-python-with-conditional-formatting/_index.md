---
category: general
date: 2026-09-05
description: Buat workbook Excel dengan Python dan tambahkan pemformatan bersyarat
  untuk menyorot sel kemarin. Pelajari kode lengkapnya serta mengapa setiap langkah
  penting.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: id
lastmod: 2026-09-05
og_description: Buat workbook Excel di Python dan tambahkan pemformatan bersyarat
  untuk menyorot sel kemarin. Ikuti panduan langkah demi langkah ini untuk solusi
  lengkap.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Buat workbook Excel di Python – tambahkan pemformatan bersyarat
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Buat buku kerja Excel di Python dengan pemformatan bersyarat
url: /id/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat workbook Excel di Python dengan pemformatan bersyarat

Jika Anda perlu **membuat workbook Excel python** untuk tugas pelaporan, panduan ini menunjukkan cara menghasilkan workbook dan menerapkan aturan pemformatan bersyarat yang menyoroti tanggal kemarin. Anda akan melihat kode persis, mengapa setiap baris ada, dan cara menyesuaikan solusi untuk rentang tanggal lain.

Pemformatan bersyarat adalah cara yang kuat untuk menarik perhatian pada data yang memenuhi kondisi tertentu. Dalam tutorial ini kami menggunakan pustaka Aspose.Cells untuk Python via .NET, yang menyediakan dukungan penuh untuk fitur Excel tanpa memerlukan Microsoft Office. Pada akhir panduan Anda akan memiliki file di mana sel dalam rentang *I19:K20* berubah menjadi merah muda ketika berisi tanggal kemarin.

## Prasyarat

* Python 3.9+ terinstal
* paket `aspose-cells` (pasang dengan `pip install aspose-cells`)
* Familiaritas dasar dengan sintaks Python
* Izin menulis ke direktori tempat workbook akan disimpan

Kode ini bekerja di Windows, macOS, dan Linux selama runtime .NET tersedia.

## Buat workbook Excel di Python

Langkah pertama adalah membuat objek `Workbook` dan mengambil worksheet default. Objek ini mewakili seluruh file Excel dalam memori.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Mengapa ini penting*: `Workbook()` membuat workbook kosong dengan satu worksheet. Mengakses `worksheets[0]` memberi Anda pegangan untuk menambahkan data, gaya, dan pemformatan nanti.

## Tambahkan rentang pemformatan bersyarat

Selanjutnya kami mendefinisikan area yang akan dievaluasi oleh aturan bersyarat. Rentang `I19:K20` mencakup enam sel dalam dua baris.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Mengapa ini penting*: Menambahkan koleksi pemformatan bersyarat ke rentang tertentu mengisolasi aturan, mencegahnya memengaruhi sel yang tidak terkait. Ini memenuhi persyaratan **add conditional formatting range**.

## Definisikan aturan: sorot sel berdasarkan tanggal

Sekarang kami membuat kondisi tipe `TIME_PERIOD`. Ini memberi tahu Excel untuk membandingkan nilai setiap sel dengan jendela waktu yang telah ditentukan.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Mengapa ini penting*: `TIME_PERIOD` adalah satu‑satunya tipe bawaan yang secara langsung mendukung “Yesterday”, “Today”, “Last Week”, dll. Dengan mengatur `condition.time_period` ke `YESTERDAY`, aturan secara otomatis mengevaluasi nilai tanggal setiap sel terhadap hari sebelum tanggal saat ini.

## Gaya sel yang memenuhi kondisi

Pemformatan bersyarat juga memerlukan gaya visual. Di sini kami memilih isian padat berwarna merah muda agar sel yang cocok menonjol.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Mengapa ini penting*: Objek gaya menentukan bagaimana Excel akan menampilkan sel yang memenuhi kondisi. Menggunakan isian merah muda padat memenuhi persyaratan **highlight cells based on date** dan membuat hasil mudah diverifikasi.

## Isi tanggal contoh untuk evaluasi

Untuk melihat aturan beraksi kami menyisipkan dua tanggal—satu yang jatuh pada tanggal kemarin dan satu yang tidak. Format `number` `30` sesuai dengan format tanggal bawaan `mm-dd-yy`.

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*Mengapa ini penting*: Menyediakan tanggal yang cocok dan tidak cocok memungkinkan Anda memverifikasi bahwa pemformatan bersyarat berfungsi dengan benar. Sesuaikan tanggal ke bulan saat ini saat menjalankan skrip, atau ganti dengan nilai dinamis.

## Simpan workbook

Akhirnya kami menulis file ke disk. Konstanta `SaveFormat.XLSX` memastikan output berupa file Excel modern.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Mengapa ini penting*: Menyimpan workbook memungkinkan Anda membukanya di Excel, LibreOffice, atau penampil apa pun yang mendukung XLSX. Jalur yang dicetak mengonfirmasi di mana file disimpan.

## Skrip lengkap

Menggabungkan semua bagian, skrip lengkap yang dapat dijalankan terlihat seperti ini:

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Output yang diharapkan

Saat Anda membuka `TimePeriodExample.xlsx`:

* Sel **I19** muncul dengan latar belakang merah muda karena nilainya cocok dengan kemarin.
* Sel **K20** tetap dengan latar belakang default karena tanggalnya berada di luar periode.
* Label **“Yesterday”** berada di sel I20 untuk kejelasan.

## Variasi umum dan kasus tepi

| Situation | Adjustment |
|-----------|------------|
| **Sorot hari ini alih-alih kemarin** | Change `condition.time_period = TimePeriodType.TODAY`. |
| **Terapkan aturan ke area yang lebih besar** | Update the range string in `add("I19:K20")` to something like `"A1:Z100"`. |
| **Gunakan warna isian yang berbeda** | Replace `DrawingColor.pink` with any other `DrawingColor` (e.g., `DrawingColor.light_green`). |
| **Bekerja dengan tanggal dinamis** | Compute `datetime.now() - timedelta(days=1)` for yesterday and write that value into the cells before applying the rule. |

**Pro tip:** Saat Anda menghasilkan workbook secara programatis untuk banyak pengguna, simpan definisi pemformatan bersyarat terpisah dari penyisipan data. Dengan cara itu Anda dapat menggunakan kembali gaya yang sama di beberapa sheet tanpa menduplikasi kode.

## Verifikasi hasil secara programatis (opsional)

Jika Anda ingin mengonfirmasi pemformatan tanpa membuka Excel, Anda dapat memeriksa gaya sebuah sel setelah menyimpan:



## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun pada teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}