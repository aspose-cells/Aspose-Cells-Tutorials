---
category: general
date: 2026-09-15
description: Python'da Aspose.Cells ile zaman dilimi koşullu biçimlendirmeyi nasıl
  uygulayacağınızı ve çalışma kitabını XLSX olarak nasıl kaydedeceğinizi öğrenin.
  Adım adım kod içerir.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: tr
lastmod: 2026-09-15
og_description: Python kullanarak Excel'de zaman dilimi koşullu biçimlendirmesi uygulayın
  ve çalışma kitabını XLSX olarak kaydedin. Aspose.Cells için bu kapsamlı rehberi
  izleyin.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Python ile Excel'de zaman dilimi koşullu biçimlendirme uygulayın
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
title: Python kullanarak Excel'de zaman dilimi koşullu biçimlendirme nasıl uygulanır
url: /tr/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Python kullanarak zaman periyodu koşullu biçimlendirmeyi nasıl uygularsınız

Bir Excel dosyasında **time period conditional formatting**'e ihtiyacınız varsa, bu öğretici Python ile bunu tam olarak nasıl yapacağınızı gösterir. Bir çalışma kitabı oluşturan, dünün tarihlerini vurgulayan ve sadece birkaç satır kodla **save workbook as XLSX** yapan eksiksiz, çalıştırılabilir bir örnek göreceksiniz.

Koşullu biçimlendirme, belirli bir kurala uyan verilere dikkat çekmenin güçlü bir yoludur. Bu rehberde “Yesterday” zaman periyoduna odaklanıyoruz, ancak aynı desen Today, LastWeek ve NextMonth gibi diğer yerleşik periyotlar için de çalışır. Öğreticinin sonunda **how to create excel workbook python**‑style betiklerini üretime hazır bir şekilde oluşturabileceksiniz.

## Önkoşullar

- Python 3.8+ yüklü  
- `aspose-cells` ve `aspose-pydrawing` paketleri (`pip install aspose-cells aspose-pydrawing`)  
- Python sözdizimi hakkında temel bilgi  

Aspose.Cells dosya oluşturmayı dahili olarak yönettiği için ek bir Office kurulumu gerekli değildir.

## Aspose.Cells ile Python'da zaman periyodu koşullu biçimlendirme

Bu bölüm, temel görev için gereken her kod satırını adım adım açıklar. Aşağıdaki kod bloğu tam betiği içerir; yorumlar her adımın amacını açıklar.

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

### Her adımın önemi

1. **Creating the workbook** size Excel'i açmadan manipüle edebileceğiniz bellek içi bir Excel dosyası sağlar.  
2. **Defining the range** (`I19:K20`) Aspose.Cells'e kuralın nerede uygulanacağını söyler, mantığı izole tutar.  
3. **Adding a TIME_PERIOD condition** Aspose'in yerleşik `TimePeriodType.YESTERDAY` enum'ını kullanır. Bu, manuel tarih hesaplamalarını önler ve dosya farklı bir günde açıldığında otomatik olarak güncellenir.  
4. **Setting the style** (`background_color` ve `pattern`) vurgulanan hücrelerin nasıl görüneceğini belirler. `Color.pink` kullanmak, kuralı kolayca fark edilmesini sağlar.  
5. **Writing sample dates** sayı formatı 30 ile Excel'in bunları seri numaraları yerine kısa tarih olarak göstermesini sağlar.  
6. **Auto‑fitting the column** dosyayı daha sonra açacak herkes için okunabilirliği artırır.  
7. **Saving as XLSX** geniş uyumluluğa sahip bir dosya üretir; bu dosya Excel, Google Sheets veya herhangi bir modern elektronik tablo programında açılabilir.

## Aspose.Cells ile Excel çalışma kitabı Python‑style oluşturma

Yukarıdaki betik zaten **how to create excel workbook python** için gerekli minimum adımları gösteriyor. Pratikte şunları yapmak isteyebilirsiniz:

- Birden fazla çalışma sayfası ekleyin (`workbook.worksheets.add("Report")`).  
- Döngüler veya pandas DataFrames ile büyük veri tablolarını doldurun (`worksheet.cells.import_data_table`).  
- `cell.get_style()` kullanarak ek biçimlendirme (yazı tipleri, kenarlıklar) uygulayın.

Bu eylemlerin tümü aynı deseni izler: nesneyi elde edin, özelliklerini değiştirin ve `set_style` ya da `save` çağırın.

## Koşullu biçimlendirme Python ekleme – diğer faydalı desenler

“Yesterday” örneğinin ötesinde, Aspose.Cells çeşitli koşullu‑biçimlendirme türlerini destekler:

| FormatConditionType | Tipik kullanım durumu |
|---------------------|-----------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | Özel formüller (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | Basit karşılaştırmalar (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | Gradyan renk ölçekleri |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | Hücre içi çubuk görselleştirme |

Sayısal bir eşik için **add conditional formatting python** eklemek istiyorsanız, `FormatConditionType.TIME_PERIOD` yerine `FormatConditionType.CELL_VALUE` koyar ve `condition.operator_type` ve `condition.formula1` ayarlarsınız.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Çalışma kitabını XLSX olarak kaydetme – en iyi uygulamalar

**save workbook as xlsx** yaparken şunları göz önünde bulundurun:

- **Specifying the correct `SaveFormat`** (`SaveFormat.XLSX`) eski formatlardan kaçınmak için.  
- **Using a deterministic file name** betik bir döngüde çalışıyorsa (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Closing resources** uzun süren hizmetlerde yerel belleği serbest bırakmak için (`workbook.dispose()`).

Örnek zaten `SaveFormat.XLSX` kullanıyor; bu, tüm koşullu‑biçimlendirme kurallarını koruyan modern, zip‑tabanlı bir çalışma kitabı üretir.

## Excel'de dünü vurgulama – doğrulama adımları

Betik çalıştırıldıktan sonra `TimePeriodExample.xlsx` dosyasını açın:

1. `I19` ve `K20` hücreleri `30‑07‑2008` ve `03‑08‑2008` tarihlerini içerir.  
2. `I20` hücresi “Yesterday” metnini gösterir.  
3. Sistem tarihini **30 July 2008** (30 Temmuz 2008) olarak değiştirip dosyayı yeniden açarsanız, eşleşen tarihlere sahip hücreler otomatik olarak pembe ile doldurulur.  
4. Sistem tarihini başka bir güne değiştirirseniz pembe dolgu kaldırılır, bu da kuralın **time period conditional formatting** mantığına tepki verdiğini doğrular.

## Yaygın tuzaklar ve nasıl kaçınılır

- **Missing `aspose-pydrawing`** – `Color` sınıfı bu pakette bulunur; kurmayı unutmak `ImportError` oluşturur.  
- **Incorrect number format** – varsayılan General formatı seri numaraları (ör. 39822) gösterir. Kısa tarih için her zaman `style.number = 30` ayarlayın.  
- **Range mismatch** – koşullu biçimlendirme aralığı vurgulamak istediğiniz hücreleri içermelidir; aksi takdirde kural etkisiz olur.

## Pro ipucu: biçimlendirme rutinini yeniden kullanma

Birden fazla çalışma kitabında aynı “Yesterday” kuralına ihtiyacınız varsa, mantığı bir yardımcı fonksiyona sarın:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Gerektiği yerde `apply_yesterday_highlight(worksheet, "A1:A10")` çağırın.

## Sonuç

Bu rehber, Python kullanarak Excel'de **time period conditional formatting** uygulamayı, **save workbook as XLSX** yapmayı ve tek bir yeniden kullanılabilir betikle **highlight yesterday in Excel**'i nasıl yapacağınızı gösterdi. Artık günlük raporlar oluşturuyor, gösterge tabloları inşa ediyor veya veri dışa aktarımları hazırlıyor olsanız da, herhangi bir otomasyon projesine **add conditional formatting python** kodunu eklemek için sağlam bir temele sahipsiniz.

**Sonraki adımlar**

- `TODAY` veya `LAST_WEEK` gibi diğer `TimePeriodType` değerlerini keşfedin.  
- Aynı aralıkta birden fazla koşullu kuralı birleştirerek daha zengin görsel ipuçları elde edin.  
- Çalışma kitabı oluşturmayı bir web servisine veya zamanlanmış işe entegre edin.

Kodlamanın tadını çıkarın ve koşullu biçimlendirmenin Excel otomasyonunuza getirdiği görsel netliğin keyfini sürün!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose.Cells .NET Kullanarak Excel'de Koşullu Biçimlendirmeyi Ustalıkla Öğrenin: Kapsamlı Bir Rehber](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Aspose.Cells .NET Ustalığı: Excel'de Alternatif Satırlara Koşullu Biçimlendirme Uygulama](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Aspose.Cells for .NET ve C# Kullanarak Excel'de Özel Yazı Tipleriyle Koşullu Biçimlendirmeyi Ustalıkla Öğrenin](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}