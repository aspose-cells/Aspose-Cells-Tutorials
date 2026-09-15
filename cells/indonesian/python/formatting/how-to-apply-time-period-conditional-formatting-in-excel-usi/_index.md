---
category: general
date: 2026-09-15
description: Pelajari cara menerapkan pemformatan bersyarat periode waktu dan menyimpan
  workbook sebagai XLSX dengan Aspose.Cells di Python. Termasuk kode langkah demi
  langkah.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: id
lastmod: 2026-09-15
og_description: Terapkan pemformatan bersyarat periode waktu di Excel menggunakan
  Python dan simpan buku kerja sebagai XLSX. Ikuti panduan lengkap ini untuk Aspose.Cells.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Terapkan pemformatan bersyarat periode waktu di Excel dengan Python
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Cara menerapkan pemformatan bersyarat periode waktu di Excel menggunakan Python
url: /id/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menerapkan conditional formatting periode waktu di Excel menggunakan Python

Jika Anda memerlukan **conditional formatting periode waktu** dalam file Excel, tutorial ini menunjukkan secara tepat cara melakukannya dengan Python. Anda akan melihat contoh lengkap yang dapat dijalankan yang membuat workbook, menyorot tanggal kemarin, dan **menyimpan workbook sebagai XLSX** hanya dalam beberapa baris kode.

Conditional formatting adalah cara yang kuat untuk menarik perhatian ke data yang memenuhi aturan tertentu. Dalam panduan ini kami fokus pada periode waktu “Yesterday”, tetapi pola yang sama berlaku untuk periode bawaan lainnya seperti Today, LastWeek, dan NextMonth. Pada akhir tutorial Anda akan dapat **how to create excel workbook python**‑style script yang siap produksi.

## Prasyarat

- Python 3.8+ terpasang  
- Paket `aspose-cells` dan `aspose-pydrawing` (`pip install aspose-cells aspose-pydrawing`)  
- Familiaritas dasar dengan sintaks Python  

Tidak diperlukan instalasi Office tambahan karena Aspose.Cells menangani pembuatan file secara internal.

## Conditional formatting periode waktu dengan Aspose.Cells di Python

Bagian ini menjelaskan setiap baris kode yang diperlukan untuk tugas utama. Blok kode di bawah ini adalah skrip lengkap; komentar menjelaskan tujuan setiap langkah.

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### Mengapa setiap langkah penting

1. **Membuat workbook** memberi Anda file Excel dalam memori yang dapat dimanipulasi tanpa membuka Excel.  
2. **Mendefinisikan rentang** (`I19:K20`) memberi tahu Aspose.Cells di mana aturan diterapkan, sehingga logika terisolasi.  
3. **Menambahkan kondisi TIME_PERIOD** menggunakan enumerasi bawaan Aspose `TimePeriodType.YESTERDAY`. Ini menghindari perhitungan tanggal manual dan secara otomatis memperbarui ketika file dibuka pada hari yang berbeda.  
4. **Menetapkan gaya** (`background_color` dan `pattern`) menentukan bagaimana sel yang disorot akan terlihat. Menggunakan `Color.pink` membuat aturan mudah dikenali.  
5. **Menulis tanggal contoh** dengan format angka 30 memastikan Excel menampilkannya sebagai tanggal singkat, bukan nomor seri.  
6. **Auto‑fitting kolom** meningkatkan keterbacaan bagi siapa pun yang membuka file nanti.  
7. **Menyimpan sebagai XLSX** menghasilkan file yang sangat kompatibel yang dapat dibuka di Excel, Google Sheets, atau program spreadsheet modern lainnya.

## Cara membuat Excel workbook Python‑style dengan Aspose.Cells

Skrip di atas sudah memperlihatkan langkah minimal untuk **how to create excel workbook python**. Dalam praktiknya Anda mungkin ingin:

- Menambahkan beberapa lembar kerja (`workbook.worksheets.add("Report")`).  
- Mengisi tabel data besar dengan loop atau pandas DataFrames (`worksheet.cells.import_data_table`).  
- Menerapkan format tambahan (font, border) menggunakan `cell.get_style()`.

Semua tindakan ini mengikuti pola yang sama: dapatkan objek, ubah propertinya, dan panggil `set_style` atau `save`.

## Tambahkan conditional formatting Python – pola berguna lainnya

Selain contoh “Yesterday”, Aspose.Cells mendukung beberapa tipe conditional‑formatting:

| FormatConditionType | Kasus penggunaan umum |
|---------------------|-----------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | Rumus khusus (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | Perbandingan sederhana (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | Skala warna gradasi |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | Visualisasi bar dalam sel |

Untuk **add conditional formatting python** pada ambang nilai numerik, Anda cukup mengganti `FormatConditionType.TIME_PERIOD` dengan `FormatConditionType.CELL_VALUE` dan mengatur `condition.operator_type` serta `condition.formula1`.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Simpan workbook sebagai XLSX – praktik terbaik

Saat Anda **save workbook as xlsx**, pertimbangkan:

- **Menentukan `SaveFormat` yang tepat** (`SaveFormat.XLSX`) agar tidak menggunakan format lama.  
- **Menggunakan nama file deterministik** jika skrip dijalankan dalam loop (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Menutup sumber daya** (`workbook.dispose()`) pada layanan yang berjalan lama untuk membebaskan memori native.

Contoh di atas sudah menggunakan `SaveFormat.XLSX`, yang menghasilkan workbook modern berbasis zip yang mempertahankan semua aturan conditional‑formatting.

## Sorot kemarin di Excel – langkah verifikasi

Setelah menjalankan skrip, buka `TimePeriodExample.xlsx`:

1. Sel `I19` dan `K20` berisi tanggal `30‑07‑2008` dan `03‑08‑2008`.  
2. Sel `I20` menampilkan teks “Yesterday”.  
3. Jika Anda mengubah tanggal sistem ke **30 Juli 2008** dan membuka kembali file, sel dengan tanggal yang cocok otomatis terisi warna pink.  
4. Mengubah tanggal sistem ke hari lain menghilangkan isi pink, mengonfirmasi bahwa aturan merespons logika **time period conditional formatting**.

## Kesalahan umum dan cara menghindarinya

- **Kehilangan `aspose-pydrawing`** – kelas `Color` berada di paket ini; lupa menginstalnya akan menimbulkan `ImportError`.  
- **Format angka tidak tepat** – menggunakan format General default menampilkan nomor seri (misalnya 39822). Selalu set `style.number = 30` untuk tanggal singkat.  
- **Rentang tidak cocok** – rentang conditional formatting harus mencakup sel yang ingin Anda sorot; bila tidak, aturan tidak berpengaruh.

## Pro tip: gunakan kembali rutin formatting

Jika Anda membutuhkan aturan “Yesterday” yang sama di beberapa workbook, bungkus logika dalam fungsi pembantu:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Panggil `apply_yesterday_highlight(worksheet, "A1:A10")` di mana pun diperlukan.

## Kesimpulan

Panduan ini menunjukkan cara mengimplementasikan **time period conditional formatting** di Excel menggunakan Python, cara **save workbook as XLSX**, dan cara **highlight yesterday in Excel** dengan satu skrip yang dapat digunakan kembali. Anda kini memiliki fondasi yang kuat untuk **add conditional formatting python** ke proyek otomasi apa pun, baik Anda menghasilkan laporan harian, membangun dasbor, atau menyiapkan ekspor data.

**Langkah selanjutnya**

- Jelajahi nilai `TimePeriodType` lain seperti `TODAY` atau `LAST_WEEK`.  
- Gabungkan beberapa aturan conditional pada rentang yang sama untuk petunjuk visual yang lebih kaya.  
- Integrasikan pembuatan workbook ke layanan web atau pekerjaan terjadwal.

Selamat coding, dan nikmati kejelasan visual yang dibawa conditional formatting ke otomasi Excel Anda!

## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET : A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Master Aspose.Cells .NET : Apply Conditional Formatting to Alternate Rows in Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}