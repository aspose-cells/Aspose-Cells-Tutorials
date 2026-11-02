---
category: general
date: 2026-07-06
description: Buat workbook Excel dengan Python dengan kode untuk mengatur warna latar
  belakang sel, mengatur gaya sel secara programatis, dan menambahkan pemformatan
  bersyarat Python untuk menyoroti tanggal hari ini.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- set cell style programmatically
- highlight today date excel
- add conditional formatting python
language: id
lastmod: 2026-07-06
og_description: Buat workbook Excel dengan Python secara instan. Pelajari cara mengatur
  warna latar sel, mengatur gaya sel secara programatik, dan menambahkan pemformatan
  bersyarat Python untuk menyoroti tanggal hari ini.
og_image_alt: Screenshot of an Excel workbook created with Python showing colored
  cells and today’s date highlighted
og_title: Buat Workbook Excel Python – Gaya Sel & Sorot Hari Ini
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  headline: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  type: TechArticle
- description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  name: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  steps:
  - name: Converting a range like `"A1:C3"` into a `CellArea`.
    text: Converting a range like `"A1:C3"` into a `CellArea`.
  - name: Filling every cell in that area with a sequential number (just for demo
      purposes).
    text: Filling every cell in that area with a sequential number (just for demo
      purposes).
  - name: Applying a solid **set cell background color**.
    text: Applying a solid **set cell background color**.
  - name: Adding a conditional rule that **highlight today date excel**.
    text: Adding a conditional rule that **highlight today date excel**.
  type: HowTo
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Buat Workbook Excel dengan Python – Panduan Lengkap tentang Styling & Pemformatan
  Bersyarat
url: /id/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Workbook Excel dengan Python – Panduan Lengkap untuk Styling & Pemformatan Bersyarat

Pernah bertanya-tanya bagaimana cara **create Excel workbook Python** dari awal tanpa membuka Excel secara manual? Anda tidak sendirian. Banyak pengembang perlu menghasilkan laporan, dasbor, atau bahkan log data sederhana secara langsung, dan melakukannya secara programatik menghemat berjam‑jam kerja manual.

Dalam tutorial ini kami akan membahas seluruh proses: mulai dari membuat workbook baru, hingga **set cell background color**, hingga **set cell style programmatically**, dan akhirnya **highlight today date excel** menggunakan **add conditional formatting python**. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan yang menghasilkan file .xlsx yang rapi dalam hitungan detik.

---

## Apa yang Akan Anda Bangun

- File Excel baru dengan beberapa sel terisi.
- Sel-sel berwarna dengan latar belakang khusus.
- Nilai numerik dan tanggal diformat dengan gaya angka tertentu.
- Aturan bersyarat yang secara otomatis menyorot sel yang berisi tanggal hari ini.

Tidak diperlukan instalasi Excel eksternal—Aspose.Cells untuk Python via .NET menangani semua pekerjaan berat.

---

## Prasyarat

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| Python 3.8+ | Sintaks modern dan petunjuk tipe |
| `aspose-cells` package | Pustaka inti untuk manipulasi workbook |
| `aspose-pydrawing` (diinstal bersama Aspose.Cells) | Menyediakan kelas `Color` |
| Familiaritas dasar dengan konsep Excel (sel, rentang, pemformatan) | Membuat alur tutorial lebih lancar |

Instal pustaka dengan:

```bash
pip install aspose-cells
```

---

## Langkah 1: Inisialisasi Workbook dan Worksheet

Hal pertama yang Anda lakukan saat **create excel workbook python** adalah membuat objek `Workbook` dan mengambil worksheet default. Anggap workbook sebagai seluruh file Excel, sementara worksheet adalah satu tab di dalamnya.

```python
from aspose.cells import Workbook

# Create a new workbook – this is our empty Excel file
book = Workbook()

# Grab the first (default) worksheet
sheet = book.worksheets[0]
```

> **Pro tip:** Jika Anda membutuhkan beberapa sheet, gunakan `book.worksheets.add("MySheet")` untuk menambahkan tab lebih banyak.

---

## Langkah 2: Kelas Helper untuk Styling & Pemformatan Bersyarat

Berikut adalah kelas `ConditionalFormatting` yang ringkas namun lengkap. Kelas ini membungkus tugas berulang berupa:

1. Mengonversi rentang seperti `"A1:C3"` menjadi `CellArea`.
2. Mengisi setiap sel dalam area tersebut dengan nomor berurutan (hanya untuk tujuan demo).
3. Menerapkan **set cell background color** solid.
4. Menambahkan aturan bersyarat yang **highlight today date excel**.

```python
from aspose.cells import (
    CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """
    Utility class that demonstrates how to:
    • set cell background color
    • set cell style programmatically
    • add conditional formatting python
    """
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        """
        Creates a conditional formatting object for the given range
        and fills the range with a background color.
        """
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]

        # Convert "A1:C3" → CellArea object
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)

        # Paint the whole area with the supplied color
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        """
        Populates each cell in the range with an incrementing integer
        and applies the supplied background color.
        """
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)

                # Apply background only if a real color is supplied
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)

                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name: str) -> CellArea:
        """
        Parses an Excel‑style address (e.g. "B2:D4") into a CellArea.
        """
        area = CellArea()
        parts = name.replace("$", "").split(':')

        start_row, start_col = CellsHelper.cell_name_to_index(parts[0])
        area.start_row = start_row
        area.start_column = start_col

        if len(parts) == 2:
            end_row, end_col = CellsHelper.cell_name_to_index(parts[1])
            area.end_row = end_row
            area.end_column = end_col
        else:
            area.end_row = start_row
            area.end_column = start_col
        return area

    # -----------------------------------------------------------------
    # Step 2: Add conditional formatting for TODAY
    # -----------------------------------------------------------------
    def add_time_period_1(self):
        """
        Demonstrates add conditional formatting python that highlights
        cells containing today’s date.
        """
        # 1️⃣ Create a formatting range and give it a neutral background
        cf = self.get_format_condition("I1:K2", Color.light_slate_gray)

        # 2️⃣ Add a TIME_PERIOD condition (Today)
        idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
        cond = cf[idx]
        cond.time_period = TimePeriodType.TODAY
        cond.style.background_color = Color.pink
        cond.style.pattern = BackgroundType.SOLID

        # 3️⃣ Populate the cells with date values
        # Cell I1 – today’s date, formatted as a date
        cell = self._sheet.cells.get("I1")
        style = cell.get_style()
        style.number = 30               # 30 = “mm-dd-yy” style in Aspose
        cell.set_style(style)
        cell.put_value(datetime.today())

        # Cell K2 – an arbitrary past date for contrast
        self._sheet.cells.get("K2").put_value(datetime(2008, 7, 30))

        # Cell I2 – a label so the reader knows what’s being highlighted
        self._sheet.cells.get("I2").put_value("Today")
```

### Mengapa Kelas Helper?

- **Reusability:** Anda dapat memanggil `add_time_period_1()` untuk worksheet mana pun tanpa menulis ulang logika.
- **Clarity:** Setiap metode melakukan satu hal – ciri khas kode bersih.
- **Extensibility:** Ingin menambahkan lebih banyak aturan? Cukup tambahkan metode lain dengan pola yang sama.

---

## Langkah 3: Terapkan Pemformatan dan Simpan File

Sekarang kami menggabungkan semuanya: membuat instance helper, menjalankan rutinitas pemformatan, dan akhirnya menulis workbook ke disk.

```python
# Instantiate the helper with our worksheet
formatter = ConditionalFormatting(sheet)

# Fill a demo range with numbers and a light blue background
formatter.get_format_condition("A1:C3", Color.light_sky_blue)

# Add the “today” conditional rule
formatter.add_time_period_1()

# Save the workbook – choose any location you like
output_path = "styled_workbook.xlsx"
book.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

Saat Anda membuka *styled_workbook.xlsx* Anda akan melihat:

- Sel **A1:C3** bernomor 0‑8 dengan isi warna biru langit‑muda.
- Sel **I1** menampilkan tanggal hari ini dengan latar belakang merah muda (berkat aturan bersyarat).
- Sel **K2** menampilkan tanggal statis *2008‑07‑30* untuk perbandingan.
- Sel **I2** berisi teks “Today”.

Petunjuk visual itu persis sesuai dengan kebutuhan **highlight today date excel**.

---

## Langkah 4: Selami Lebih Dalam – Menyesuaikan Gaya

Jika Anda perlu menyesuaikan font, batas, atau format angka, Anda dapat memperluas metode `fill_cell` atau membuat helper baru:

```python
def apply_custom_style(cell, font_name="Calibri", font_size=11, bold=False):
    style = cell.get_style()
    style.font.name = font_name
    style.font.size = font_size
    style.font.bold = bold
    cell.set_style(style)
```

Anda kemudian dapat memanggil `apply_custom_style(cell, bold=True)` di dalam loop untuk **set cell style programmatically** pada setiap sel dalam rentang.

---

## Kesalahan Umum & Cara Menghindarinya

| Gejala | Penyebab Kemungkinan | Solusi |
|--------|----------------------|--------|
| Sel tetap putih meskipun `Color.light_sky_blue` | Gaya tidak diterapkan setelah mengatur `foreground_color` | Selalu panggil `cell.set_style(style)` setelah memodifikasi objek gaya. |
| Aturan bersyarat tidak pernah aktif | `style.number` tidak diatur untuk sel tanggal, sehingga Excel memperlakukan nilai sebagai string | Atur `style.number = 30` (atau format tanggal apa pun) sebelum `cell.put_value(datetime…)`. |
| Workbook disimpan sebagai .xls meskipun `SaveFormat.XLSX` | Versi Aspose yang lebih lama yang default ke format lama | Tingkatkan ke paket `aspose-cells` terbaru. |
| Rentang seperti `"A1"` menghasilkan error indeks | Menggunakan `cells.get("A1")` pada sheet yang belum diinisialisasi | Pastikan worksheet ada (ada tepat setelah `Workbook()`), atau gunakan `cells.get(row, col)` dengan indeks berbasis nol. |

---

## Skrip Lengkap untuk Salin‑Tempel

Berikut adalah skrip **seluruhnya** yang dapat Anda letakkan ke dalam file bernama `create_excel.py` dan jalankan langsung.

```python
# create_excel.py
from aspose.cells import (
    Workbook, CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """Utility for styling cells and adding conditional formatting."""
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)
                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name:


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Otomasi Excel dengan Aspose.Cells .NET: Membuat Workbook & Menetapkan Tautan Eksternal](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Menguasai Pemformatan Sel Excel dan Manajemen Workbook dengan Aspose.Cells untuk .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Otomasi Excel: Membuat Workbook dan Menambahkan ListBox Menggunakan Aspose.Cells untuk .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}