---
category: general
date: 2026-09-05
description: Python'da Excel çalışma kitabı oluşturun ve dün hücrelerini vurgulamak
  için koşullu biçimlendirme ekleyin. Tam kodu ve her adımın neden önemli olduğunu
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: tr
lastmod: 2026-09-05
og_description: Python'da Excel çalışma kitabı oluşturun ve dün hücrelerini vurgulamak
  için koşullu biçimlendirme ekleyin. Tam bir çözüm için bu adım adım rehberi izleyin.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Python'da Excel çalışma kitabı oluşturun – koşullu biçimlendirme ekleyin
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
title: Python'da koşullu biçimlendirme ile Excel çalışma kitabı oluştur
url: /tr/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da Koşullu Biçimlendirme ile Excel Çalışma Kitabı Oluşturma

Raporlama görevi için **create Excel workbook python**'a ihtiyacınız varsa, bu kılavuz bir çalışma kitabı oluşturmayı ve dün tarihlerini vurgulayan bir koşullu biçimlendirme kuralı uygulamayı gösterir. Tam kodu, her satırın neden mevcut olduğunu ve çözümü diğer tarih aralıkları için nasıl uyarlayacağınızı göreceksiniz.

Koşullu biçimlendirme, belirli bir koşulu karşılayan verilere dikkat çekmenin güçlü bir yoludur. Bu öğreticide Python via .NET için Aspose.Cells kütüphanesini kullanıyoruz; bu kütüphane Microsoft Office gerektirmeden tam Excel özellik desteği sağlar. Kılavuzun sonunda, *I19:K20* aralığındaki hücreler dün tarihini içerdiğinde pembe renge dönüşen bir dosyanız olacak.

## Önkoşullar

* Python 3.9+ yüklü
* `aspose-cells` paketi (`pip install aspose-cells` ile kurulur)
* Python sözdizimi hakkında temel aşinalık
* Çalışma kitabının kaydedileceği dizine yazma izni

Kod, .NET çalışma zamanı mevcut olduğu sürece Windows, macOS ve Linux'ta çalışır.

## Python'da Excel Çalışma Kitabı Oluşturma

İlk adım bir `Workbook` nesnesi oluşturmak ve varsayılan çalışma sayfasını almaktır. Bu nesne, bellekteki tüm Excel dosyasını temsil eder.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Neden önemli*: `Workbook()` tek bir çalışma sayfası içeren boş bir çalışma kitabı oluşturur. `worksheets[0]`'a erişmek, daha sonra veri, stil ve biçimlendirme eklemek için bir tutamaç sağlar.

## Koşullu Biçimlendirme Aralığını Ekle

Sonra, koşullu kural tarafından değerlendirilecek alanı tanımlarız. `I19:K20` aralığı iki satırda altı hücreyi kapsar.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Neden önemli*: Belirli bir aralığa koşullu biçimlendirme koleksiyonu eklemek, kuralı izole eder ve alakasız hücreleri etkilemesini önler. Bu, **add conditional formatting range** gereksinimini karşılar.

## Kuralı Tanımla: Tarihe Göre Hücreleri Vurgula

Şimdi `TIME_PERIOD` türünde bir koşul oluşturuyoruz. Bu, Excel'e her hücrenin değerini önceden tanımlanmış bir zaman penceresiyle karşılaştırmasını söyler.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Neden önemli*: `TIME_PERIOD`, “Yesterday”, “Today”, “Last Week” vb. doğrudan destekleyen tek yerleşik türdür. `condition.time_period` değerini `YESTERDAY` olarak ayarlayarak, kural otomatik olarak her hücrenin tarih değerini mevcut tarihin bir gün öncesiyle karşılaştırır.

## Koşulu Karşılayan Hücreleri Stilize Et

Koşullu biçimlendirme ayrıca görsel bir stile ihtiyaç duyar. Burada, eşleşen hücrelerin öne çıkması için pembe katı dolgu seçiyoruz.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Neden önemli*: Stil nesnesi, koşulu karşılayan hücrelerin Excel tarafından nasıl görüntüleneceğini tanımlar. Katı pembe dolgu kullanmak, **highlight cells based on date** gereksinimini karşılar ve sonucu doğrulamayı kolaylaştırır.

## Değerlendirme İçin Örnek Tarihler Gir

Kuralın çalışmasını görmek için iki tarih ekliyoruz—biri dün tarihine, diğeri ise düşmüyor. `number` formatı `30`, yerleşik tarih formatı `mm-dd-yy`'ye karşılık gelir.

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

*Neden önemli*: Hem eşleşen hem de eşleşmeyen bir tarih sağlamak, koşullu biçimlendirmenin doğru çalıştığını doğrulamanızı sağlar. Betiği çalıştırdığınızda tarihleri mevcut aya göre ayarlayın veya dinamik değerlerle değiştirin.

## Çalışma Kitabını Kaydet

Son olarak dosyayı diske yazıyoruz. `SaveFormat.XLSX` sabiti, çıktının modern bir Excel dosyası olmasını sağlar.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Neden önemli*: Çalışma kitabını kalıcı hale getirmek, onu Excel, LibreOffice veya XLSX destekleyen herhangi bir görüntüleyicide açmanızı sağlar. Yazdırılan yol, dosyanın nereye yazıldığını doğrular.

## Tam Betik

Tüm parçaları bir araya getirerek, eksiksiz, çalıştırılabilir betik şu şekilde görünür:

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

### Beklenen Çıktı

`TimePeriodExample.xlsx` dosyasını açtığınızda:

* **I19** hücresi, değeri dünle eşleştiği için pembe arka planla görünür.
* **K20** hücresi, tarihi dönem dışı olduğu için varsayılan arka planı korur.
* **“Yesterday”** etiketi, açıklık için I20 hücresinde bulunur.

## Ortak Varyasyonlar ve Kenar Durumları

| Durum | Ayarlama |
|-----------|------------|
| **Bugünü vurgulamak, dün yerine** | `condition.time_period = TimePeriodType.TODAY` olarak değiştirin. |
| **Kuralı daha büyük bir alana uygulamak** | `add("I19:K20")` içindeki aralık dizesini `"A1:Z100"` gibi bir değere güncelleyin. |
| **Farklı bir dolgu rengi kullanmak** | `DrawingColor.pink` yerine başka bir `DrawingColor` (ör. `DrawingColor.light_green`) ile değiştirin. |
| **Dinamik tarihlerle çalışmak** | Dün için `datetime.now() - timedelta(days=1)` hesaplayın ve kuralı uygulamadan önce bu değeri hücrelere yazın. |

**Pro ipucu:** Çalışma kitabını birçok kullanıcı için programlı olarak oluştururken, koşullu biçimlendirme tanımını veri eklemeden ayrı tutun. Böylece aynı stili birden fazla sayfada kod tekrarına gerek kalmadan yeniden kullanabilirsiniz.

## Sonucu Programlı Olarak Doğrulama (isteğe bağlı)

Excel'i açmadan biçimlendirmeyi onaylamak isterseniz, kaydettiğiniz dosyayı yükledikten sonra bir hücrenin stilini inceleyebilirsiniz:



## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir ve ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olur.

- [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}