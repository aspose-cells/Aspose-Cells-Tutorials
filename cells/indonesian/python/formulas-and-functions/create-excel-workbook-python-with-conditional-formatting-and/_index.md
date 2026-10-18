---
category: general
date: 2026-10-04
description: Buat workbook Excel dengan Python menggunakan Aspose.Cells. Pelajari
  pemformatan bersyarat Excel dengan Python, mengubah warna latar belakang sel dengan
  Python, dan memformat tanggal sel dengan Python dalam contoh lengkap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: id
lastmod: 2026-10-04
og_description: Buat workbook Excel dengan Python menggunakan Aspose.Cells. Tutorial
  ini menunjukkan pemformatan bersyarat Excel dengan Python, warna latar belakang
  sel dengan Python, dan pemformatan tanggal sel dengan Python langkah demi langkah.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Buat workbook Excel dengan Python – panduan lengkap dengan pemformatan bersyarat
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Buat workbook Excel dengan Python, dengan pemformatan bersyarat dan warna latar
  sel
url: /id/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel workbook python dengan conditional formatting dan warna latar belakang sel

Jika Anda perlu **create Excel workbook python** dengan cepat, panduan ini menunjukkan secara tepat cara melakukannya. Anda akan melihat contoh lengkap yang dapat dijalankan yang menambahkan **excel conditional formatting python**, mengubah **cell background color python**, dan **format cells date python** untuk penyorotan “Yesterday”.

Dalam banyak skenario pelaporan, petunjuk visual berupa sel berwarna membuat data langsung dapat dipahami. Tutorial ini memandu Anda melalui setiap baris kode, menjelaskan mengapa setiap langkah penting, dan memberikan skrip siap‑jalankan yang dapat Anda sesuaikan dengan proyek Anda.

## Apa yang akan Anda capai

1. **create Excel workbook python** menggunakan library Aspose.Cells.  
2. Terapkan **excel conditional formatting python** yang secara otomatis menyorot tanggal yang jatuh pada “Yesterday”.  
3. Atur **cell background color python** menjadi pink (atau warna apa pun yang Anda suka).  
4. **format cells date python** sehingga tanggal muncul dalam gaya tanggal standar Excel.  

Tidak diperlukan pengalaman sebelumnya dengan Aspose.Cells—hanya lingkungan Python 3 yang berfungsi dan akses pip.

## Prasyarat

- Python 3.8 atau yang lebih baru terpasang.  
- Paket `aspose-cells` dan `aspose-pydrawing` terpasang melalui `pip install aspose-cells aspose-pydrawing`.  
- Familiaritas dasar dengan sintaks Python dan konsep Excel (workbooks, worksheets, cells).  

> **Pro tip:** Jika Anda menjalankan skrip dalam lingkungan virtual, Anda menghindari konflik versi dengan proyek lain.

## Langkah 1: Siapkan proyek dan impor kelas yang diperlukan

Langkah pertama saat Anda **create Excel workbook python** adalah mengimpor kelas Aspose.Cells yang Anda perlukan. Kelas-kelas ini memberi Anda akses langsung ke pembuatan workbook, conditional formatting, dan styling.

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*Mengapa ini penting:* Mengimpor hanya simbol yang dibutuhkan menjaga namespace tetap rapi dan membuat skrip lebih mudah dibaca. `Workbook` adalah titik masuk untuk **create Excel workbook python**, sementara `FormatConditionType` dan `TimePeriodType` penting untuk **excel conditional formatting python**.

## Langkah 2: Buat workbook baru dan dapatkan worksheet pertama

Sekarang kita benar‑benar **create Excel workbook python**. Konstruktor `Workbook()` memberi Anda file Excel kosong dengan worksheet default.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Penjelasan:* Setiap file Excel dimulai dengan setidaknya satu worksheet. Secara default Aspose.Cells menamainya “Sheet1”. Anda dapat menambahkan lebih banyak sheet nanti, tetapi untuk demonstrasi ini satu sheet menjaga contoh tetap fokus.

## Langkah 3: Tentukan rentang target untuk conditional formatting

Conditional formatting bekerja pada rentang persegi panjang. Di sini kami memilih rentang `I19:K20`, yang memberikan tiga kolom dan dua baris untuk dimainkan.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Mengapa kami melakukan ini:* Metode `get` mengembalikan objek `ConditionalFormatting` yang terikat pada rentang yang ditentukan. Jika rentang belum memiliki pemformatan apa pun, Aspose.Cells secara otomatis membuat koleksi baru.

## Langkah 4: Tambahkan kondisi TIME_PERIOD dan atur warna latar belakang

Ini adalah inti dari **excel conditional formatting python**. Kami menambahkan aturan `TIME_PERIOD` yang menyorot sel yang berisi tanggal yang jatuh pada “Yesterday”.

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*Penjelasan mendalam:*  
- `FormatConditionType.TIME_PERIOD` memberi tahu Excel untuk mengevaluasi tanggal relatif terhadap tanggal saat ini.  
- `TimePeriodType.YESTERDAY` adalah enum bawaan yang secara otomatis diperbarui setiap hari, sehingga workbook selalu menyorot “Yesterday” terbaru.  
- Dengan mengatur `background_color` ke `Color.pink` dan pola ke `SOLID`, kami mencapai efek **cell background color python** tanpa kode VBA tambahan.

## Langkah 5: Isi rentang dengan tanggal contoh dan terapkan pemformatan tanggal

Untuk melihat conditional formatting beraksi, kita membutuhkan nilai tanggal nyata. Kita juga perlu **format cells date python** agar Excel memperlakukan mereka sebagai tanggal, bukan sekadar angka.

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*Penjelasan:*  
- Baris `style.number = 30` adalah langkah **format cells date python**. Kode format 30 sesuai dengan format tanggal singkat (`m/d/yy`).  
- Menggunakan fungsi pembantu menjaga kode tetap DRY (Don’t Repeat Yourself) dan memudahkan penambahan tanggal lebih lanjut.

## Langkah 6: Tambahkan label deskriptif

Label kecil membantu siapa pun yang membuka workbook memahami mengapa sel berwarna.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## Langkah 7: Simpan workbook ke disk

Akhirnya, kami **create Excel workbook python** di disk dengan memanggil `save`. Konstanta `SaveFormat.XLSX` memastikan file berada dalam format Office Open XML modern.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Ketika Anda membuka `TimePeriodDemo.xlsx` di Excel, Anda akan melihat:

- Sel `I19` dan `K20` berisi tanggal.  
- Sel yang cocok dengan “Yesterday” (dalam contoh statis ini, `I19`) disorot pink.  
- Label “Yesterday” muncul di `I20`.  

> **Tip:** Jika Anda menjalankan skrip pada hari yang berbeda, conditional formatting tetap menyorot sel yang tanggalnya tepat satu hari sebelum tanggal sistem saat ini—tanpa perlu mengubah kode.

## Skrip lengkap – siap disalin dan dijalankan

Berikut adalah program lengkap yang berdiri sendiri yang menggabungkan semua langkah di atas. Salin ke dalam file bernama `conditional_format_demo.py`, sesuaikan `YOUR_DIRECTORY`, dan jalankan dengan `python conditional_format_demo.py`.

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Output yang diharapkan

Menjalankan skrip mencetak baris konfirmasi:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Membuka file yang dihasilkan menunjukkan latar belakang pink pada sel yang cocok dengan aturan “Yesterday”, mengonfirmasi bahwa **excel conditional formatting python** dan **cell background color python** bekerja bersama.

## Variasi umum dan kasus tepi

| Situasi | Cara menyesuaikan kode |
|-----------|-----------------------|
| **Warna sorot berbeda** | Ubah `Color.pink` ke konstanta `Color` lain, misalnya `Color.light_green`. |
| **Sorot “Today” alih-alih “Yesterday”** | Setel `condition.time_period = TimePeriodType.TODAY`. |
| **Terapkan pemformatan ke seluruh kolom** | Gunakan rentang seperti `"A:A"` dan sesuaikan variabel `target_range` sesuai. |
| **Gunakan format tanggal khusus** | Ganti `style.number = 30` dengan `style.custom = "dd-mmm-yyyy"` untuk format yang lebih mudah dibaca. |
| **Beberapa kondisi pada rentang yang sama** |  |

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}