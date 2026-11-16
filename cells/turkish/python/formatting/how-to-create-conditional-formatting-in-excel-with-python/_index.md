---
category: general
date: 2026-11-16
description: Python kullanarak Excel'de koşullu biçimlendirme oluşturun. Koşullu biçimlendirme
  aralığı eklemeyi, tarihleri vurgulamayı ve bir çalışma kitabını programlı olarak
  oluşturmayı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: tr
lastmod: 2026-11-16
og_description: Python ile Excel'de koşullu biçimlendirme oluşturun. Bu öğreticide,
  koşullu biçimlendirme aralığı ekleme, tarihleri vurgulama ve bir çalışma kitabı
  oluşturma gösterilmektedir.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Python ile Excel'de Koşullu Biçimlendirme Oluşturma – Adım Adım Rehber
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Python ile Excel'de koşullu biçimlendirme nasıl oluşturulur
url: /tr/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python ile Excel'de Koşullu Biçimlendirme Nasıl Oluşturulur

Python'da çalışırken bir Excel dosyasında **koşullu biçimlendirme oluşturmanız** gerekiyorsa, bu rehber tam olarak nasıl yapılacağını gösterir. **excel workbook python** tarzında bir çalışma kitabı oluşturmayı, bir biçimlendirme aralığı tanımlamayı ve IDE'den çıkmadan tarihleri vurgulamayı öğreneceksiniz.

Koşullu biçimlendirme, belirli kriterleri karşılayan hücreleri görsel olarak işaretlemenizi sağlar—panolar, raporlar veya veri doğrulama sayfaları için mükemmeldir. Bu öğreticinin sonunda, “Dün” tarihli hücreleri pembe, geri kalan aralığı ise yeşil renkte gösteren tam işlevsel bir çalışma kitabına sahip olacaksınız.

## Neyi Başaracaksınız

* Sıfırdan yeni bir çalışma kitabı oluşturun.  
* Belirli bir hücre bloğu için bir koşullu‑biçim koleksiyonu ekleyin.  
* Tarihleri vurgulayan **TIME_PERIOD** kuralını uygulayın (“tarihleri nasıl vurgularım” senaryosu).  
* Dosyayı, sonraki işlemler için hazır bir XLSX çalışma kitabı olarak kaydedin.

**Önkoşullar**  
* Python 3.8+  
* `aspose-cells` Python paketi (`pip install aspose-cells`)  
* Python’un `datetime` modülüne temel aşinalık  

---

## Python’da koşullu biçimlendirme nasıl oluşturulur

İlk adım, biçimlendirme kurallarını barındıracak çalışma kitabını ve çalışma sayfasını ayarlamaktır.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Neden önemli** – `Workbook`, tüm Excel işlemlerinin giriş noktasıdır. Çalışma kitabını programlı olarak oluşturmak, manuel “File → New” adımını ortadan kaldırır ve otomatik rapor hatlarını mümkün kılar.

---

## Koşullu‑biçim koleksiyonunu hazırlama – koşullu biçimlendirme aralığını ekleme

Şimdi kuralın uygulanacağı hücre bloğunu tanımlıyoruz. Bu örnekte aralık **I19:K20** olarak belirlenmiştir.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Açıklama** – `conditional_formattings.add`, adres dizesine bağlı yeni bir koleksiyon kaydeder. İlk koşul (`conds[0]`) bir “varsayılan” stil gibi çalışır; sonraki kural, kriterleri karşılandığında onu geçersiz kılar.

---

## TIME_PERIOD koşulu ekleme – tarihleri nasıl vurgularım

Şimdi “Dün” tarihlerini tanımlayan ve pembe renkle boyayan gerçek mantığı ekliyoruz.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Neden TIME_PERIOD kullanılır?** – Aspose.Cells, `YESTERDAY`, `TODAY` ve `LAST_WEEK` gibi yerleşik enum’lar sunar. Bu enum’lar, hücrenin tarih değerini mevcut sistem tarihine karşı değerlendirir ve özel formüllere gerek kalmaz.

---

## Örnek veri doldurma – kuralı gösterme

Biçimlendirmenin çalıştığını görmek için kurala uyan bir tarih ve uymayan bir tarih ekliyoruz.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Köşe durum notu** – `TIME_PERIOD` kuralı yalnızca *gerçek* tarihlerle çalışır. Hücrede metin (ör. “N/A”) varsa kural göz ardı edilir, beklenmedik renk değişiklikleri önlenir.

---

## Çalışma kitabını kaydetme – add conditional formatting python

Son olarak, çalışma kitabını diske yazıyoruz. Dosya, renkleri doğrulamak için herhangi bir tablo programında açılabilir.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Beklenen sonuç**  

| I19 (yeşil → pembe) | J19 (yeşil) | K19 (yeşil) |
|---------------------|------------|------------|
| 30/07/2008 (dün)    | –          | –          |
| **I20**: “Dün” etiketi | –      | –          |
| I21‑K21 (yeşil)      | –          | –          |

**I19** hücresi, tarihi “Dün” dönemine denk geldiği için pembe arka planla gösterilirken, **K20** yeşil kalır.

---

## Yaygın sorular ve pratik ipuçları

* **Yerleşik bir dönem yerine özel bir tarih aralığı kullanabilir miyim?**  
  Evet. `condition.time_period` yerine `condition.formula1 = "TODAY()-1"` yazın ve `condition.type = FormatConditionType.FORMULA` olarak ayarlayın.

* **Çalışma kitabım zaten veri içeriyorsa ne yapmalıyım?**  
  Koşullu biçimlendirme koleksiyonunu eklemeden önce `worksheet.cells.import_data` ile toplu veri yüklemesi yapın.

* **Büyük sayfalarda performans nasıl etkilenir?**  
  Çok sayıda koşul eklemek render süresini yavaşlatabilir. Aynı kuralı aynı anda birden çok hücreye uygulamak için hücreleri tek bir aralıkta (ör. “A1:C1000”) gruplayın ve koşul sayısını düşük tutun.

* **Çapraz platform uyumluluğu?**  
  Oluşturulan XLSX dosyası Office Open XML standardını izler; bu yüzden Windows, macOS ve Linux tablolama uygulamalarında çalışır.

---

## Sonuç

Artık Python kullanarak bir Excel çalışma kitabında **koşullu biçimlendirme oluşturmayı** biliyorsunuz. Eğitim, çalışma kitabı oluşturmayı, bir **add conditional formatting range** tanımlamayı, bir **how to highlight dates** kuralı uygulamayı ve dosyayı **add conditional formatting python** yöntemiyle kaydetmeyi kapsadı.

Bundan sonra şunları yapabilirsiniz:

* `TimePeriodType` değerleriyle (ör. `TODAY`, `LAST_MONTH`) kural setinizi genişletin.  
* Aynı aralıkta birden fazla koşulu birleştirerek daha zengin görsel ipuçları oluşturun.  
* Bu iş akışını otomatik raporlama hatlarına veya web servislerine entegre edin.

İyi kodlamalar, rapor ihtiyaçlarınıza uygun farklı renkler, aralıklar ve tarih mantıklarıyla denemeler yapmaktan çekinmeyin!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakın konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}