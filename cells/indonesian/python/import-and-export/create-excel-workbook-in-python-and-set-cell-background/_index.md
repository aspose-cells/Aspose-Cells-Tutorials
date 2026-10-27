---
category: general
date: 2026-10-07
description: Buat workbook Excel di Python, atur warna latar belakang sel, sesuaikan
  lebar kolom secara otomatis, dan isi tanggal di Excel dengan contoh kode singkat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: id
lastmod: 2026-10-07
og_description: Buat workbook Excel di Python, kemudian atur warna latar belakang
  sel, sesuaikan lebar kolom secara otomatis, dan isi tanggal di Excel. Ikuti panduan
  langkah demi langkah ini untuk menghasilkan file TimePeriodDemo.xlsx.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Buat workbook Excel di Python – atur latar belakang & sesuaikan otomatis
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: Buat buku kerja Excel di Python dan atur latar belakang sel
url: /id/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat workbook Excel di Python dan atur latar belakang sel

Buat workbook Excel di Python dan terapkan pemformatan bersyarat dengan hanya beberapa baris kode. Tutorial ini menunjukkan **cara membuat excel** secara programatis, mengatur warna latar belakang sel, menyesuaikan lebar kolom Excel secara otomatis, dan mengisi tanggal di Excel menggunakan pustaka Aspose.Cells.

Anda akan belajar cara:
* Menginisialisasi workbook dan memperoleh worksheet pertama.  
* Mendefinisikan format bersyarat yang menyorot tanggal “Yesterday”.  
* Menyisipkan tanggal contoh ke sel tertentu.  
* Menyesuaikan lebar kolom agar data terlihat jelas.  
* Menyimpan workbook ke folder yang dipilih.

Satu-satunya prasyarat adalah lingkungan Python 3 yang berfungsi dengan paket `aspose-cells` dan `aspose-pydrawing` terpasang:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Buat workbook Excel di Python – langkah demi langkah

Bagian-bagian berikut memecah proses menjadi langkah-langkah yang dapat dikelola. Setiap langkah mencakup kode yang diperlukan, penjelasan tentang **mengapa** hal itu penting, dan tip untuk menghindari jebakan umum.

### Langkah 1: Impor namespace yang diperlukan dan definisikan fungsi pembantu

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Mengapa ini penting*: Mengimpor kelas yang tepat memberi Anda akses ke pembuatan workbook, pemformatan bersyarat, dan penanganan warna.  
**Pro tip**: Simpan impor di bagian atas file; ini membuat skrip lebih mudah dibaca dan mencegah kesalahan circular‑import.

### Langkah 2: Buat workbook dan dapatkan worksheet pertama

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

Konstruktor `Workbook()` membuat workbook Excel kosong di memori.  
**Mengapa**: Memulai dengan workbook baru memastikan tidak ada format yang tersisa dari eksekusi sebelumnya.

### Langkah 3: Atur warna latar belakang sel dengan format bersyarat

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*Mengapa*: Menggunakan kondisi **time period** secara otomatis menyorot setiap sel yang berisi tanggal kemarin, menghilangkan pemeriksaan tanggal manual.  
**Tip**: `Color.pink` hanya contoh; Anda dapat menggunakan objek `Color` apa pun (`Color.yellow`, `Color.light_green`, dll.).

### Langkah 4: Isi tanggal di Excel

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

Di sini kami **mengisi tanggal di Excel** pada sel `I19` dan `K20`. Tanggal pertama akan memicu pemformatan bersyarat, sementara yang kedua tidak.  
**Mengapa ini penting**: Menunjukkan nilai yang cocok dan tidak cocok membantu Anda memverifikasi bahwa aturan berfungsi seperti yang diharapkan.

### Langkah 5: Auto‑fit kolom Excel untuk visibilitas yang lebih baik

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` menyesuaikan lebar kolom berdasarkan nilai sel terpanjang.  
**Tip**: Panggil ini setelah Anda menulis semua data; jika tidak lebar mungkin dihitung berdasarkan konten yang belum lengkap.

### Langkah 6: Simpan workbook

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

Menyimpan file menuliskan workbook yang berada di memori ke disk dalam format XLSX modern.

### Skrip lengkap – menggabungkan semuanya

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**Output yang diharapkan**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Buka file yang dihasilkan di Excel – sel `I19:K20` akan menampilkan latar belakang merah muda untuk tanggal yang jatuh pada “Yesterday,” dan kolom L akan cukup lebar untuk menampilkan label tanpa terpotong.

---

## Mengapa pendekatan ini bekerja paling baik

* **Single‑pass workflow** – Semua operasi terjadi pada instance `Workbook` yang sama, menghindari I/O yang tidak perlu.  
* **Conditional formatting** – Menggunakan `FormatConditionType.TIME_PERIOD` memungkinkan Excel menangani logika tanggal, yang lebih dapat diandalkan daripada menulis pemeriksaan tanggal Python khusus.  
* **Explicit styling** – Menetapkan `background_color` dan `pattern` menjamin hasil visual di semua versi Excel.  
* **Auto‑fit setelah data**  

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Buat Workbook Excel Python – Panduan Lengkap](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Buat Workbook Excel Python – Panduan Langkah‑per‑Langkah Lengkap](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Buat Workbook Excel Python – Panduan Lengkap dengan Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}