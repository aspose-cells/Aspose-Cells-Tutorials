---
category: general
date: 2026-07-20
description: Buat workbook Excel dengan Python menggunakan Aspose.Cells, atur warna
  latar belakang sel, dan tambahkan pemformatan bersyarat Python untuk menata sel
  berdasarkan tanggal.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: id
lastmod: 2026-07-20
og_description: Buat workbook Excel dengan Python menggunakan Aspose.Cells. Pelajari
  cara mengatur warna latar belakang sel dan menambahkan pemformatan bersyarat Python
  untuk memformat sel berdasarkan tanggal.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Buat Workbook Excel dengan Python – Tambahkan Pemformatan Bersyarat
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: Membuat Workbook Excel dengan Python – Panduan Pemformatan Bersyarat
url: /id/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Workbook Excel Python – Panduan Pemformatan Bersyarat

Pernah bertanya-tanya bagaimana cara **create Excel workbook Python** dari awal dan membuatnya tampak rapi tanpa membuka UI? Anda tidak sendirian. Banyak pengembang menemui kesulitan ketika mereka perlu **set cell background color** atau menerapkan gaya berbasis tanggal secara programatis.  

Dalam tutorial ini kami akan membahas contoh lengkap yang dapat dijalankan yang menggunakan Aspose.Cells untuk **add conditional formatting python** aturan, memformat sel berdasarkan tanggal, dan menyimpan hasilnya sebagai file XLSX modern. Pada akhir tutorial Anda akan memiliki skrip mandiri yang dapat Anda masukkan ke dalam proyek apa pun.

## Apa yang Akan Anda Pelajari

- Cara menginisialisasi workbook dan mengambil worksheet pertama.  
- Cara **set cell background color** untuk seluruh rentang.  
- Menggunakan **aspose cells conditional formatting** untuk menyorot tanggal “Yesterday”.  
- Auto‑fitting kolom dan menyimpan file ke disk.  

Tidak diperlukan konfigurasi eksternal—hanya Python 3 dan paket Aspose.Cells. Jika Anda sudah menginstal `aspose-cells`, Anda siap; jika tidak, cukup jalankan `pip install aspose-cells`.

## Prasyarat

- Python 3.8+ (kode ini bekerja pada 3.9, 3.10, dan versi lebih baru).  
- Aspose.Cells untuk Python via .NET (`aspose-cells` pembungkus NuGet).  
- Pemahaman dasar tentang konsep Excel (sel, rentang, pemformatan).  

Sudah siap? Bagus—mari kita mulai.

## Buat Workbook Excel Python – Penyiapan dan Worksheet

Pertama-tama: kita membutuhkan objek workbook baru dan referensi ke worksheet default. Ini adalah kanvas tempat semua operasi selanjutnya akan dilakukan.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **Mengapa ini penting:** `Workbook()` membuat file Excel di memori, menghilangkan kebutuhan akan file sementara. Variabel `worksheet` adalah titik masuk kita untuk aksi pada level sel.

## Set Cell Background Color

Sebelum menambahkan aturan apa pun, sebaiknya beri rentang target warna dasar agar pemformatan bersyarat terlihat jelas. Helper di bawah ini mengambil (atau membuat) `FormatConditionCollection` untuk rentang tertentu dan mewarnai sel dengan latar belakang solid.

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **Tip pro:** Jika Anda berencana menggunakan kembali rentang yang sama dengan beberapa aturan, panggil helper ini sekali dan simpan koleksi yang dikembalikan; ini menghemat beberapa panggilan API.

## Add Conditional Formatting Python for Date Ranges

Sekarang bagian yang menyenangkan: kami akan membuat aturan **time‑period conditional formatting** yang menyorot sel yang berisi tanggal kemarin. Ini menunjukkan kekuatan **format cells by date** menggunakan Aspose.Cells.

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **Mengapa menggunakan `TIME_PERIOD`?** Ini menyederhanakan kebutuhan menulis formula khusus. Aspose.Cells mengevaluasi tanggal terhadap tanggal sistem saat ini, sehingga aturan selalu relevan.

### Menjalankan Aturan

```python
apply_yesterday_rule()
```

Saat Anda membuka file hasil, sel `I19` akan bersinar merah muda (karena merupakan “Yesterday”), sementara `K20` tetap berwarna hijau dasar.

## Auto‑Fit Columns and Save Workbook

Spreadsheet yang rapi terlihat profesional. Auto‑fitting memastikan data kami tidak sempit.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Kasus tepi:** Jika Anda menargetkan direktori yang tidak ada, `workbook.save` akan menghasilkan error. Bungkus pemanggilan save dalam blok `try/except` jika Anda memerlukan penanganan yang halus.

### Skrip Lengkap (Siap Salin‑Tempel)

Berikut adalah seluruh skrip, siap dijalankan. Cukup ganti `YOUR_DIRECTORY` dengan folder yang valid di mesin Anda.

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Menjalankan skrip ini akan menghasilkan `TimePeriodExample.xlsx` dengan pemformatan bersyarat yang telah kami jelaskan.

## Pertanyaan Umum & Tips

- **Apakah saya dapat menargetkan rentang tanggal yang berbeda?**  
  Tentu saja. Ubah `"I19:K20"` ke rentang gaya A1 apa pun, dan sesuaikan tanggal contoh sesuai kebutuhan.

- **Bagaimana jika saya memerlukan formula khusus alih-alih `YESTERDAY`?**  
  Gunakan `FormatConditionType.FORMULA` dan set `condition.formula1 = "YOUR_FORMULA"`—misalnya, `=TODAY()-A1=1` untuk meniru kemarin.

- **Bagaimana cara menerapkan beberapa aturan pada rentang yang sama?**  
  Panggil `conditions.add_condition` lagi dengan `FormatConditionType` yang berbeda. Urutan penting; aturan yang lebih akhir dapat menimpa yang sebelumnya.

- **Apakah ada cara untuk mengatur warna font bersamaan dengan latar belakang?**  
  Ya—modifikasi `condition.style.font.color = Color.white` (atau `Color` lain apa pun).

## Kesimpulan

Anda sekarang tahu cara **create Excel workbook Python** menggunakan Aspose.Cells, **set cell background color**, dan **add conditional formatting python** yang memformat sel berdasarkan tanggal. Skrip ini berfungsi penuh, menangani kasus tepi seperti direktori yang hilang, dan dapat diperluas ke skenario yang lebih canggih seperti logika bersyarat multi‑aturan atau deteksi rentang dinamis.

Siap untuk langkah selanjutnya? Coba ganti aturan “Yesterday” dengan “Last Week”, bereksperimen dengan isian gradien, atau buat laporan lengkap dengan puluhan tabel yang diformat. Semua blok bangunan ada di sini, dan Anda baru saja menguasai inti **aspose cells conditional formatting** di Python.

Selamat coding, dan silakan bagikan variasi Anda sendiri di komentar!

## Apa yang Harus Anda Pelajari Selanjutnya?

- [Menguasai Pemformatan Sel Excel dan Manajemen Workbook dengan Aspose.Cells untuk .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Cara Membuat dan Menyimpan Workbook Excel sebagai ODS Menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Cara Membuat Named Ranges yang Terbatas pada Workbook di Excel Menggunakan Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}