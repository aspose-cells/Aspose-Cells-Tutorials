---
category: general
date: 2026-10-07
description: Python'da Excel çalışma kitabı oluşturun, hücre arka plan rengini ayarlayın,
  sütunları otomatik genişletin ve Excel'e tarihleri ekleyin; kısa bir kod örneğiyle.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: tr
lastmod: 2026-10-07
og_description: Python'da Excel çalışma kitabı oluşturun, ardından hücre arka plan
  rengini ayarlayın, sütunları otomatik olarak genişletin ve Excel'de tarihleri doldurun.
  TimePeriodDemo.xlsx dosyasını oluşturmak için bu adım adım kılavuzu izleyin.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Python’da Excel çalışma kitabı oluştur – arka plan ayarla ve otomatik sığdır
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
title: Python'da Excel çalışma kitabı oluştur ve hücre arka planını ayarla
url: /tr/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da Excel çalışma kitabı oluşturun ve hücre arka planını ayarlayın

Python'da Excel çalışma kitabı oluşturun ve sadece birkaç satır kodla koşullu biçimlendirme uygulayın. Bu öğreticide **how to create excel** dosyalarını programlı olarak nasıl oluşturacağınızı, hücre arka plan rengini ayarlamayı, Excel sütunlarını otomatik olarak genişletmeyi ve Aspose.Cells kütüphanesini kullanarak Excel'de tarihleri doldurmayı gösterir.

Şunları öğreneceksiniz:
* Bir çalışma kitabı başlatın ve ilk çalışma sayfasını alın.  
* “Yesterday” (Dün) tarihlerini vurgulayan bir koşullu biçim tanımlayın.  
* Belirli hücrelere örnek tarihleri ekleyin.  
* Verilerin net görünmesi için sütunları otomatik olarak genişletin.  
* Çalışma kitabını seçilen bir klasöre kaydedin.

Tek ön koşul, `aspose-cells` ve `aspose-pydrawing` paketlerinin yüklü olduğu çalışan bir Python 3 ortamıdır:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Python'da Excel çalışma kitabı oluşturun – adım adım

Aşağıdaki bölümler süreci yönetilebilir adımlara ayırır. Her adım gerekli kodu, **neden** önemli olduğuna dair bir açıklamayı ve yaygın hatalardan kaçınmak için bir ipucu içerir.

### Step 1: Import required namespaces and define a helper function

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Why this matters*: Importing the correct classes gives you access to workbook creation, conditional formatting, and color handling.  
**Pro tip**: Keep imports at the top of the file; it makes the script easier to read and prevents circular‑import errors.

*Why this matters*: Doğru sınıfları içe aktarmak, çalışma kitabı oluşturma, koşullu biçimlendirme ve renk işleme erişimi sağlar.  
**Pro tip**: İçe aktarmaları dosyanın en üstünde tutun; bu, betiği okumayı kolaylaştırır ve döngüsel içe aktarma hatalarını önler.

### Step 2: Create the workbook and get the first worksheet

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

The `Workbook()` constructor creates an empty Excel workbook in memory.  
**Why**: Starting with a fresh workbook ensures no leftover formatting from previous runs.

`Workbook()` yapıcı, bellekte boş bir Excel çalışma kitabı oluşturur.  
**Why**: Yeni bir çalışma kitabı ile başlamak, önceki çalıştırmalardan kalan biçimlendirmelerin olmamasını sağlar.

### Step 3: Set cell background color with a conditional format

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

*Why*: Using a **time period** condition automatically highlights any cell that contains yesterday’s date, eliminating manual date checks.  
**Tip**: `Color.pink` is just an example; you can use any `Color` object (`Color.yellow`, `Color.light_green`, etc.).

*Neden*: **time period** koşulunu kullanmak, dün tarihini içeren herhangi bir hücreyi otomatik olarak vurgular, manuel tarih kontrollerini ortadan kaldırır.  
**Tip**: `Color.pink` sadece bir örnektir; herhangi bir `Color` nesnesi (`Color.yellow`, `Color.light_green` vb.) kullanabilirsiniz.

### Step 4: Populate dates in Excel

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

Here we **populate dates in Excel** cells `I19` and `K20`. The first date will trigger the conditional formatting, while the second will not.  
**Why this matters**: Demonstrating both matching and non‑matching values helps you verify that the rule works as expected.

Burada `I19` ve `K20` hücrelerine **populate dates in Excel** hücrelerini dolduruyoruz. İlk tarih koşullu biçimlendirmeyi tetikleyecek, ikincisi ise tetiklemeyecek.  
**Why this matters**: Hem eşleşen hem de eşleşmeyen değerleri göstererek kuralın beklendiği gibi çalıştığını doğrulamanıza yardımcı olur.

### Step 5: Auto‑fit Excel columns for better visibility

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` adjusts the column width based on the longest cell value.  
**Tip**: Call this after you have written all data; otherwise the width might be calculated on incomplete content.

`auto_fit_column`, en uzun hücre değerine göre sütun genişliğini ayarlar.  
**Tip**: Bunu tüm verileri yazdıktan sonra çağırın; aksi takdirde genişlik eksik içerik üzerinden hesaplanabilir.

### Step 6: Save the workbook

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

Saving the file writes the in‑memory workbook to disk in the modern XLSX format.

Dosyayı kaydetmek, bellekteki çalışma kitabını modern XLSX formatında diske yazar.

### Full script – putting it all together

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

**Expected output**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Open the generated file in Excel – cells `I19:K20` will show a pink background for the date that falls on “Yesterday,” and column L will be wide enough to display the label without clipping.

Oluşturulan dosyayı Excel'de açın – `I19:K20` hücreleri “Yesterday” tarihine sahip hücre için pembe bir arka plan gösterecek ve L sütunu etiketi kırpılmadan gösterecek kadar geniş olacaktır.

---

## Why this approach works best

* **Single‑pass workflow** – All operations happen on the same `Workbook` instance, avoiding unnecessary I/O.  
* **Conditional formatting** – Using `FormatConditionType.TIME_PERIOD` lets Excel handle date logic, which is more reliable than writing custom Python date checks.  
* **Explicit styling** – Setting `background_color` and `pattern` guarantees the visual result across Excel versions.  
* **Auto‑fit after data** – Veri girildikten sonra otomatik genişletme.

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook Python – Full Guide](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Create Excel Workbook Python – Complete Step‑by‑Step Guide](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}