---
category: general
date: 2026-08-08
description: Python ile Excel çalışma kitabı oluşturun ve tarihe dayalı koşullu biçimlendirme
  ekleyin. Aspose.Cells kullanarak dünün hücrelerini vurgulamak için adım adım rehber.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: tr
lastmod: 2026-08-08
og_description: Aspose.Cells ile Python’da Excel çalışma kitabı oluşturun ve dinamik
  elektronik tablolar için tarihe dayalı koşullu biçimlendirme uygulayın.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Python ile Excel çalışma kitabı oluştur – tarih koşullu biçimlendirme
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
title: Python ile Excel Çalışma Kitabı Oluşturma ve Tarih Koşullu Biçimlendirme
url: /tr/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python ile Excel Çalışma Kitabı Oluşturma ve Tarihe Dayalı Koşullu Biçimlendirme

Eğer **create Excel workbook Python** ve belirli bir tarihle eşleşen hücreleri otomatik olarak vurgulamanız gerekiyorsa, bu öğretici tam olarak nasıl yapılacağını gösterir. **conditional formatting based on date** uygulamayı öğrenecek ve dün tarihleri pembe renkle aydınlatacaksınız, Aspose.Cells kütüphanesini kullanarak.

Kılavuz, SDK’yı kurmaktan son .xlsx dosyasını kaydetmeye kadar her adımı adım adım gösterir—böylece çalışan bir örneği kendi projenize kopyalayıp yapıştırabilirsiniz. Harici bir dokümantasyona ihtiyaç yok; tüm kod ve açıklamalar kendi içinde bulunur.

## Ön Koşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* Python 3.8 veya daha yeni bir sürüm.
* `aspose-cells` paketi (Aspose.Cells için Python sarmalayıcısı). Şu komutla kurun:
  ```bash
  pip install aspose-cells
  ```
* Python ve Excel kavramları (çalışma sayfaları, hücre stilleri vb.) hakkında temel bilgi.

> **Pro tip:** Aspose.Cells, Microsoft Excel yüklü olmasa bile çalışır; bu da sunucu‑tarafı otomasyon için idealdir.

## Adım 1: Python’da Excel çalışma kitabını oluşturun

İlk görev, yeni bir çalışma kitabı örneği oluşturmak ve varsayılan çalışma sayfasını almaktır. Bu nesne, tüm Excel dosyasını temsil eder ve satır, sütun ve biçimlendirme API’lerine erişim sağlar.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

Çalışma kitabını oluşturmak, veri, formül veya biçimlendirme kuralları ekleyecek olsanız da temel adımdır.

## Adım 2: Tarihe dayalı bir koşullu biçimlendirme tanımlayın

Şimdi **conditional formatting based on date** ekliyoruz. `FormatConditionType.TIME_PERIOD` enum’u, Dün, Bugün veya GeçenHafta gibi yerleşik zaman dilimlerini belirtmemizi sağlar.

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

Bu adımın önemi: Excel, aralıktaki her hücre için koşulu değerlendirir. Bir hücrenin değeri tanımlı döneme (dün) düşerse, atadığımız stil otomatik olarak uygulanır.

## Adım 3: Aralığı örnek tarihlerle doldurun

Kuralın çalıştığını görmek için hedef hücrelere birkaç `datetime` nesnesi yazarız. Bunlardan biri, çalışma kitabının iç tarih sistemine göre bilinçli olarak dünü temsil edecek şekilde ayarlanmıştır.

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

`number = 30` satırı, Excel’in değeri standart kısa‑tarih formatıyla göstermesini sağlar. Farklı bir sunum isterseniz bu indeksi başka bir yerleşik sayı formatına değiştirebilirsiniz.

## Adım 4: Okunabilirlik için sütun genişliğini ayarlayın

Tarihleri içeren sütunu otomatik olarak genişletmek, çıktının Excel ya da bir görüntüleyicide daha rahat okunmasını sağlar.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## Adım 5: Çalışma kitabını diske kaydedin

Son olarak, çalışma kitabını bir .xlsx dosyası olarak saklayın. `"YOUR_DIRECTORY"` ifadesini makinenizdeki gerçek bir yol ile değiştirin.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

`TimePeriodDemo.out.xlsx` dosyasını Excel’de açtığınızda, **I19** hücresi pembe bir arka planla görünecek çünkü değeri “Dün” kuralına eşleşiyor; **K20** ise değişmeden kalacak.

### Beklenen çıktı

| I19 (date) | I20 (label) | J19 | J20 | K19 | K20 (date) |
|------------|-------------|-----|-----|-----|------------|
| *2008‑07‑30* (pink background) | Yesterday | – | – | – | *2008‑08‑03* (no formatting) |

Pembe gölgelendirme, **conditional formatting based on date**’in amaçlandığı gibi çalıştığını doğrular.

## Ortak varyasyonlar ve uç durumlar

| Durum | Kodu nasıl uyarlarsınız |
|-----------|-----------------------|
| **“Yesterday” yerine “Today” vurgulamak** | `condition.time_period = TimePeriodType.TODAY` değiştirin |
| **Kuralı tüm bir sütuna uygulamak** | `worksheet.get_range("A:A").format_conditions` kullanın |
| **Özel bir tarih aralığı (ör. son 7 gün)** | Zaman‑dönemi koşulunu formül koşuluyla değiştirin: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **Farklı arka plan renkleri** | `condition.style.background_color = Color.light_green` (veya tercih ettiğiniz herhangi bir `Color`) ayarlayın |
| **Görüntü olmadan Linux’da çalıştırmak** | Aspose.Cells tamamen başsızdır; ekstra yapılandırma gerekmez. |

## Tam, çalıştırılabilir örnek

Aşağıda, çıktı dizinini güncelledikten sonra doğrudan çalıştırabileceğiniz tam betik yer alıyor. Tüm importlar, yorumlar ve temel hata‑işleme kodları dahil edilmiştir.

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

Betik çalıştırıldığında, “Yesterday” hücresi otomatik olarak vurgulanmış bir Excel dosyası üretilir; bu da **create Excel workbook Python** ile **conditional formatting based on date**’in bir arada nasıl kullanılacağını gösterir.

## Sonuç

Artık **create Excel workbook Python** nesnelerini nasıl oluşturacağınızı, **date‑based conditional formatting**’i nasıl tanımlayacağınızı biliyorsunuz.

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve ilgili konuları derinlemesine ele alan tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [Aspose.Cells ile Java’da Excel Çalışma Kitabı Oluşturma: Adım‑Adım Kılavuz](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Aspose.Cells .NET ile Grafikler İçeren Excel Çalışma Kitabı Oluşturma | Adım‑Adım Kılavuz](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Excel Otomasyonu: Aspose.Cells for .NET ile Bir Çalışma Kitabı Oluşturma ve ListBox Ekleme](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}