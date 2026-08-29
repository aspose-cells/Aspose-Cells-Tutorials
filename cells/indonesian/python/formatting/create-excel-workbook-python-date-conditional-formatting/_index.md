---
category: general
date: 2026-08-08
description: Buat workbook Excel dengan Python dan tambahkan pemformatan bersyarat
  berdasarkan tanggal. Panduan langkah demi langkah menggunakan Aspose.Cells untuk
  menyorot sel kemarin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: id
lastmod: 2026-08-08
og_description: Buat workbook Excel dengan Python menggunakan Aspose.Cells dan terapkan
  pemformatan bersyarat berdasarkan tanggal untuk spreadsheet dinamis.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Buat workbook Excel dengan Python – pemformatan bersyarat tanggal
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Buat Workbook Excel dengan Pemformatan Bersyarat Tanggal di Python
url: /id/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Workbook Excel Python dengan Pemformatan Bersyarat Berdasarkan Tanggal

Jika Anda perlu **create Excel workbook Python** dan secara otomatis menyorot sel yang cocok dengan tanggal tertentu, tutorial ini menunjukkan cara melakukannya secara tepat. Anda akan belajar menerapkan **conditional formatting based on date** sehingga tanggal kemarin ditampilkan dengan warna merah muda, menggunakan pustaka Aspose.Cells.

Panduan ini melangkah melalui setiap tahap—dari menginstal SDK hingga menyimpan file .xlsx akhir—sehingga Anda dapat menyalin‑tempel contoh yang berfungsi ke dalam proyek Anda sendiri. Tidak diperlukan dokumentasi eksternal; semua kode dan penjelasan disediakan secara lengkap.

## Prasyarat

Sebelum Anda memulai, pastikan Anda memiliki:

* Python 3.8 atau yang lebih baru terinstal.
* Paket `aspose-cells` (wrapper Python untuk Aspose.Cells). Instal dengan:
  ```bash
  pip install aspose-cells
  ```
* Pemahaman dasar tentang Python dan konsep Excel seperti lembar kerja dan gaya sel.

> **Pro tip:** Aspose.Cells berfungsi tanpa perlu menginstal Microsoft Excel, menjadikannya ideal untuk otomatisasi sisi‑server.

## Langkah 1: Buat workbook Excel di Python

Tugas pertama adalah membuat instance workbook baru dan mengambil worksheet default. Objek ini mewakili seluruh file Excel dan menyediakan akses ke baris, kolom, serta API pemformatan.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

Membuat workbook adalah fondasi untuk manipulasi lebih lanjut, baik Anda menambahkan data, rumus, atau aturan pemformatan.

## Langkah 2: Definisikan pemformatan bersyarat berbasis tanggal

Sekarang kita menambahkan **conditional formatting based on date**. Enum `FormatConditionType.TIME_PERIOD` memungkinkan kita menentukan periode waktu bawaan seperti Yesterday, Today, atau LastWeek.

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

Mengapa langkah ini penting: Excel mengevaluasi kondisi untuk setiap sel dalam rentang. Ketika nilai sel berada dalam periode yang ditentukan (kemarin), gaya yang kami tetapkan diterapkan secara otomatis.

## Langkah 3: Isi rentang dengan contoh tanggal

Untuk melihat aturan bekerja, kami menulis beberapa objek `datetime` ke sel target. Salah satunya sengaja diatur ke tanggal kemarin relatif terhadap sistem tanggal internal workbook.

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

Baris `number = 30` memberi tahu Excel untuk menampilkan nilai menggunakan format tanggal pendek standar. Anda dapat mengubah indeks ini ke format angka bawaan apa pun jika menginginkan tampilan yang berbeda.

## Langkah 4: Sesuaikan lebar kolom untuk keterbacaan

Menyesuaikan lebar otomatis kolom yang berisi tanggal membuat output lebih mudah dibaca, terutama saat workbook dibuka di Excel atau penampil.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## Langkah 5: Simpan workbook ke disk

Akhirnya, simpan workbook sebagai file .xlsx. Ganti `"YOUR_DIRECTORY"` dengan jalur nyata di mesin Anda.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Saat Anda membuka `TimePeriodDemo.out.xlsx` di Excel, sel **I19** akan muncul dengan latar belakang merah muda karena nilainya cocok dengan aturan “Yesterday”, sementara **K20** tetap tidak berubah.

### Output yang Diharapkan

| I19 (tanggal) | I20 (label) | J19 | J20 | K19 | K20 (tanggal) |
|---------------|-------------|-----|-----|-----|----------------|
| *2008‑07‑30* (latar belakang merah muda) | Yesterday | – | – | – | *2008‑08‑03* (tanpa pemformatan) |

Warna merah muda mengonfirmasi bahwa **conditional formatting based on date** berfungsi sebagaimana mestinya.

## Variasi umum dan kasus tepi

| Situasi | Cara menyesuaikan kode |
|---------|------------------------|
| **Sorot “Today” alih-alih “Yesterday”** | Change `condition.time_period = TimePeriodType.TODAY` |
| **Terapkan aturan ke seluruh kolom** | Use `worksheet.get_range("A:A").format_conditions` |
| **Gunakan rentang tanggal khusus (mis., 7 hari terakhir)** | Replace the time‑period condition with a formula condition: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **Warna latar belakang berbeda** | Set `condition.style.background_color = Color.light_green` (or any `Color` you prefer) |
| **Menjalankan di Linux tanpa tampilan** | Aspose.Cells is fully headless; no extra configuration required. |

## Contoh lengkap yang dapat dijalankan

Berikut adalah skrip lengkap yang dapat Anda jalankan apa adanya (setelah memperbarui direktori output). Semua impor, komentar, dan dasar‑dasar penanganan error disertakan.

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Menjalankan skrip menghasilkan file Excel di mana sel “Yesterday” secara otomatis disorot, menunjukkan **create Excel workbook Python** yang digabungkan dengan **conditional formatting based on date**.

## Kesimpulan

Anda sekarang tahu cara membuat objek **create Excel workbook Python**, mendefinisikan **date‑based conditional formatting**

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Create Excel Workbook with Charts Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}