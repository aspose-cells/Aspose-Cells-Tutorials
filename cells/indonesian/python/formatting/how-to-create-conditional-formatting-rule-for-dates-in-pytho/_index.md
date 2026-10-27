---
category: general
date: 2026-08-24
description: Buat aturan pemformatan bersyarat di Python menggunakan Aspose.Cells
  untuk menyoroti tanggal, dengan penyesuaian otomatis lebar kolom dan pemformatan
  warna latar belakang.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: id
lastmod: 2026-08-24
og_description: Buat aturan pemformatan bersyarat di Python dengan Aspose.Cells. Pelajari
  cara menyorot tanggal, mengatur warna latar belakang, dan menyesuaikan lebar kolom
  secara otomatis hanya dengan beberapa baris kode.
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: Buat aturan pemformatan bersyarat untuk tanggal di Python – panduan langkah
  demi langkah
schemas:
- author: Aspose
  dateModified: '2026-08-24'
  description: Create conditional formatting rule in Python using Aspose.Cells to
    highlight dates, with auto‑fit column and background color formatting.
  headline: How to create conditional formatting rule for dates in Python
  type: TechArticle
tags:
- Aspose.Cells
- Python
- Excel automation
- Conditional formatting
title: Cara membuat aturan format bersyarat untuk tanggal di Python
url: /id/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara membuat aturan pemformatan bersyarat untuk tanggal di Python

Jika Anda perlu **membuat aturan pemformatan bersyarat** yang merespons tanggal, panduan ini menunjukkan secara tepat cara melakukannya dengan Aspose.Cells untuk Python. Baik Anda sedang membangun dasbor pelaporan maupun spreadsheet otomatis, Anda akan melihat cara menyorot tanggal kemarin, menerapkan warna latar belakang khusus, dan **menyesuaikan lebar kolom secara otomatis** sehingga hasilnya tampak rapi.

Dalam tutorial ini kami akan membahas **pemformatan bersyarat berdasarkan tanggal**, mendemonstrasikan **pemformatan bersyarat warna latar belakang**, dan mengakhiri dengan menyimpan workbook sebagai file XLSX. Pada akhir tutorial Anda akan memiliki helper yang dapat digunakan kembali dan dapat disesuaikan untuk **pemformatan bersyarat berbasis tanggal** apa pun yang Anda perlukan.

## Apa yang akan Anda pelajari

* Menyiapkan workbook dan worksheet menggunakan Aspose.Cells.  
* Menulis fungsi helper yang menambahkan **pemformatan bersyarat berbasis tanggal** ke rentang sel mana pun.  
* Mengisi sel dengan contoh tanggal agar aturan dapat dievaluasi.  
* Menerapkan **auto fit column** untuk membuat konten dapat dibaca.  
* Menyimpan workbook dan memverifikasi sel yang disorot.

Prasyarat satu-satunya adalah lingkungan Python yang berfungsi dengan paket `aspose-cells` terpasang.

## Prasyarat

| Persyaratan | Detail |
|-------------|--------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Pengetahuan dasar tentang konsep Excel | worksheets, cells, formatting |
| Opsional: IDE (VS Code, PyCharm, dll.) | editor apa pun yang dapat menjalankan skrip Python |

## Langkah 1: Buat workbook dan dapatkan worksheet pertama

Langkah pertama adalah menyiapkan objek yang **siap untuk membuat aturan pemformatan bersyarat**: sebuah `Workbook` dan `Worksheet` default‑nya. Objek‑objek ini merupakan titik masuk untuk semua operasi selanjutnya.

```python
# Step 1 – initialize workbook and worksheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create a new, empty workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Mengapa ini penting:* `Workbook` menyimpan seluruh file Excel, sementara `Worksheet` adalah tempat Anda menerapkan sel, gaya, dan **pemformatan bersyarat berdasarkan tanggal**. Tanpa objek‑objek ini kode selanjutnya tidak memiliki tempat untuk beraksi.

## Langkah 2: Bangun helper untuk menambahkan format TIME_PERIOD

Alih‑alih mengulangi boiler‑plate yang sama untuk setiap rentang, kami membungkus logika dalam fungsi helper. Fungsi ini menempelkan **pemformatan bersyarat warna latar belakang** yang memberi warna pada sel berdasarkan `TimePeriodType` (misalnya Yesterday, Today, LastWeek).

```python
def add_time_period_condition(cell_range: str, bg_color: Color, period: TimePeriodType):
    """
    Attach a TIME_PERIOD conditional format to `cell_range`.
    The rule highlights cells that fall within `period` using `bg_color`.

    Args:
        cell_range: A1‑style range string, e.g., "I19:K20".
        bg_color:   Desired background color for matching cells.
        period:     Aspose.Cells TimePeriodType enum value.
    Returns:
        The FormatConditionCollection for further customization if needed.
    """
    # 1️⃣ Attach a new ConditionalFormatting block to the specified range
    worksheet.conditional_formattings.add(cell_range)

    # 2️⃣ Grab the collection of conditions for that block
    conditions = worksheet.conditional_formattings[-1].format_conditions

    # 3️⃣ (Optional) Set a default background for the whole range
    conditions.back_color = bg_color

    # 4️⃣ Add a TIME_PERIOD condition and configure its appearance
    idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[idx]

    # Apply the visual style – pink background in this example
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Define which period triggers the formatting
    condition.time_period = period

    return conditions
```

*Mengapa kami menggunakan helper:* Ia memisahkan logika **pemformatan bersyarat berbasis tanggal**, sehingga kode lebih mudah dibaca, diuji, dan digunakan kembali di banyak sheet atau proyek.

## Langkah 3: Terapkan aturan pemformatan bersyarat ke rentang tertentu

Sekarang kami menggunakan helper untuk menyorot sel yang berisi “Yesterday”. Inilah inti dari operasi **membuat aturan pemformatan bersyarat** kami.

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

Saat workbook dibuka, setiap sel di `I19:K20` yang tanggalnya sama dengan tanggal kemarin akan muncul dengan isian warna merah muda (gaya yang kami tetapkan di helper). Argumen `bg_color` menunjukkan cara menambahkan latar belakang default di belakang warna bersyarat bila diinginkan.

## Langkah 4: Isi rentang dengan contoh tanggal

Aturan bersyarat hanya terlihat setelah worksheet berisi data yang memenuhi kondisi. Kami akan menyisipkan dua tanggal: satu yang cocok dengan “Yesterday” dan satu lagi yang berada di luar periode tersebut.

```python
# Step 4 – insert sample dates for demonstration

# Cell I19 will match the YESTERDAY period
yesterday_cell = worksheet.cells.get("I19")
yesterday_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008 is “yesterday” relative to 31‑Jul‑2008
yesterday_cell.get_style().number = 30          # 30 = built‑in date format
yesterday_cell.set_style(yesterday_cell.get_style())

# Cell K20 will NOT match the period (it’s a later date)
outside_cell = worksheet.cells.get("K20")
outside_cell.put_value(datetime(2008, 8, 3))     # 03‑Aug‑2008 is outside “Yesterday”
outside_cell.get_style().number = 30
outside_cell.set_style(outside_cell.get_style())

# Optional label for clarity – not part of the rule
worksheet.cells.get("I20").put_value("Yesterday")
```

*Mengapa ini penting:* Dengan menggunakan objek `datetime` kami memastikan Excel memperlakukan nilai sebagai tanggal sebenarnya, yang diperlukan agar **pemformatan bersyarat berdasarkan tanggal** berfungsi dengan benar. Format numerik (`30`) menjamin sel menampilkan tanggal yang dapat dikenali.

## Langkah 5: Auto‑fit kolom dan simpan workbook

Setelah data dan pemformatan berada pada tempatnya, sentuhan akhir adalah **menyesuaikan lebar kolom secara otomatis** sehingga tanggal terlihat lengkap. Kemudian kami menulis file ke disk.

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

Pemanggilan `auto_fit_column` memeriksa konten terpanjang di kolom 12 (yang berkorespondensi dengan kolom **L** di Excel) dan memperlebar lebar kolom sesuai. Langkah kecil ini mencegah tanggal terpotong dan membuat **pemformatan bersyarat warna latar belakang** terlihat jelas.

### Hasil yang diharapkan

Saat Anda membuka `TimePeriodDemo.out.xlsx`:

| I19 (tanggal) | I20 (label) | K20 (tanggal) |
|---------------|------------|---------------|
| 30‑Jul‑2008 (disorot merah muda) | Yesterday | 03‑Aug‑2008 (tanpa sorotan) |

* Sel dengan tanggal kemarin menampilkan latar belakang merah muda karena **membuat aturan pemformatan bersyarat** cocok dengan periode `YESTERDAY`.  
* Semua sel lain mempertahankan latar belakang default (atau `medium_sea_green` opsional yang Anda berikan).  
* Kolom L secara otomatis diperlebar, sehingga tanggal dapat dibaca sepenuhnya.

## Variasi umum dan kasus tepi

| Situasi | Cara menyesuaikan kode |
|---------|------------------------|
| **Sorot “Today” alih‑alih “Yesterday”** | Ganti `TimePeriodType.YESTERDAY` dengan `TimePeriodType.TODAY`. |
| **Gunakan warna latar belakang berbeda** | Ubah `condition.style.background_color = Color.pink` menjadi `Color` lain (misalnya `Color.light_sky_blue`). |
| **Terapkan aturan ke rentang tidak berurutan** | Panggil `add_time_period_condition` beberapa kali dengan string `cell_range` yang berbeda (misalnya `"A1:A10", "C1:C10"`). |
| **Bekerja dengan workbook yang sudah ada** | Muat file dengan `Workbook("myfile.xlsx")` alih‑alih membuat yang baru. |
| **Beberapa kondisi berbasis tanggal pada rentang yang sama** | Setelah pemanggilan pertama `add_time_period_condition`, tambahkan kondisi lain dengan `conditions.add_condition(FormatConditionType.TIME_PERIOD)` dan setel `time_period` yang berbeda. |

## Kesimpulan

Anda kini tahu cara **membuat aturan pemformatan bersyarat** yang merespons tanggal, menerapkan **pemformatan bersyarat warna latar belakang**, dan **menyesuaikan lebar kolom secara otomatis** menggunakan Aspose.Cells untuk Python. Fungsi helper mengabstraksi logika, memungkinkan Anda menggunakan pola yang sama untuk skenario **pemformatan bersyarat berdasarkan tanggal** apa pun—baik itu “Yesterday”, “LastWeek”, atau rentang khusus.

Selanjutnya, Anda dapat menjelajahi:

* Menambahkan **icon sets** atau **data bars** bersama aturan tanggal.  
* Menghasilkan laporan dinamis yang mengambil tanggal dari basis data.  
* Menggabungkan beberapa aturan **pemformatan bersyarat berbasis tanggal** pada satu sheet.

Silakan bereksperimen dengan warna, periode, dan rentang yang berbeda untuk menyesuaikan kebutuhan proyek Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [How to Extract Conditional Formatting Colors Using Aspose.Cells for .NET](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}