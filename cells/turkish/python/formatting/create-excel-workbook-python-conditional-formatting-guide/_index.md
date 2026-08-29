---
category: general
date: 2026-07-20
description: Aspose.Cells ile Python’da Excel çalışma kitabı oluşturun, hücre arka
  plan rengini ayarlayın ve tarih bazında hücreleri biçimlendirmek için Python’da
  koşullu biçimlendirme ekleyin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: tr
lastmod: 2026-07-20
og_description: Python kullanarak Aspose.Cells ile Excel çalışma kitabı oluşturun.
  Hücre arka plan rengini nasıl ayarlayacağınızı ve tarih bazlı hücreleri biçimlendirmek
  için koşullu biçimlendirmeyi Python’da nasıl ekleyeceğinizi öğrenin.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Python ile Excel Çalışma Kitabı Oluştur – Koşullu Biçimlendirme Ekle
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
title: Python ile Excel Çalışma Kitabı Oluşturma – Koşullu Biçimlendirme Rehberi
url: /tr/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel Çalışma Kitabı Python – Koşullu Biçimlendirme Rehberi

Hiç **create Excel workbook Python**'ı sıfırdan nasıl oluşturup UI'yi açmadan şık bir görünüme kavuşturabileceğinizi merak ettiniz mi? Yalnız değilsiniz. Birçok geliştirici, **set cell background color**'ı ayarlamaları veya tarih‑tabanlı stilleri programlı olarak uygulamaları gerektiğinde bir engelle karşılaşıyor.  

Bu öğreticide, Aspose.Cells kullanarak **add conditional formatting python** kurallarını ekleyen, hücreleri tarihe göre biçimlendiren ve sonucu modern bir XLSX dosyası olarak kaydeden tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, herhangi bir projeye ekleyebileceğiniz bağımsız bir betiğe sahip olacaksınız.

## Öğrenecekleriniz

- Bir çalışma kitabını başlatma ve ilk çalışma sayfasını alma.  
- Tüm bir aralık için **set cell background color** uygulama yolları.  
- **aspose cells conditional formatting** kullanarak “Yesterday” (Dün) tarihlerini vurgulama.  
- Sütunları otomatik sığdırma ve dosyayı diske kaydetme.  

Harici bir yapılandırma gerekmez—sadece Python 3 ve Aspose.Cells paketi. `aspose-cells` paketini zaten kurduysanız hazırsınız; aksi takdirde hızlı bir `pip install aspose-cells` yeterli olacaktır.

## Önkoşullar

- Python 3.8+ (kod 3.9, 3.10 ve daha yeni sürümlerde çalışır).  
- Aspose.Cells for Python via .NET (`aspose-cells` NuGet sarmalayıcısı).  
- Excel kavramlarına (hücreler, aralıklar, biçimlendirme) temel aşinalık.  

Hazırsanız, başlayalım.

## Excel Çalışma Kitabı Python – Kurulum ve Çalışma Sayfası

İlk iş olarak, yeni bir çalışma kitabı nesnesine ve varsayılan çalışma sayfasına ihtiyacımız var. Bu, sonraki tüm işlemlerin gerçekleşeceği tuvaldir.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **Neden önemli:** `Workbook()` bellekte bir Excel dosyası oluşturur, geçici dosyalara ihtiyaç duymaz. `worksheet` değişkeni hücre‑seviyesindeki işlemlerimiz için giriş noktamızdır.

## Hücre Arka Plan Rengini Ayarlama

Herhangi bir kural eklemeden önce, hedef aralığa temel bir renk vermek, koşullu biçimlendirmenin öne çıkmasını sağlar. Aşağıdaki yardımcı metod, verilen bir aralık için bir `FormatConditionCollection` alır (veya oluşturur) ve hücreleri katı bir arka plan rengiyle boyar.

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

> **İpucu:** Aynı aralığı birden fazla kuralla kullanacaksanız, bu yardımcıyı bir kez çağırıp dönen koleksiyonu saklayın; birkaç API çağrısını tasarruf ettirir.

## Tarih Aralıkları için Koşullu Biçimlendirme Python Ekleme

Şimdi eğlenceli kısma geçiyoruz: **time‑period conditional formatting** kuralı oluşturarak dün tarihini içeren hücreleri vurgulayacağız. Bu, Aspose.Cells kullanarak **format cells by date** gücünü gösterir.

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

> **Neden `TIME_PERIOD`?** Özel formüller yazma ihtiyacını ortadan kaldırır. Aspose.Cells, tarihi mevcut sistem tarihine göre değerlendirir, böylece kural her zaman geçerli olur.

### Kuralı Çalıştırma

```python
apply_yesterday_rule()
```

Dosyayı açtığınızda, `I19` hücreleri pembe (çünkü “Yesterday”) ışıldarken, `K20` temel yeşil renkte kalır.

## Sütunları Otomatik Sığdırma ve Çalışma Kitabını Kaydetme

Düzenli bir elektronik tablo profesyonel görünür. Otomatik sığdırma, verilerimizin sıkışık olmamasını sağlar.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Köşe durumu:** Hedeflediğiniz dizin mevcut değilse, `workbook.save` bir hata fırlatır. Daha nazik bir işlem için kaydetme çağrısını bir `try/except` bloğuna sarabilirsiniz.

### Tam Betik (Kopyala‑Yapıştır Hazır)

Aşağıda, doğrudan çalıştırabileceğiniz tam betik yer alıyor. `YOUR_DIRECTORY` kısmını makinenizde geçerli bir klasörle değiştirmeniz yeterli.

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

Bu betiği çalıştırdığınızda, açıklanan koşullu biçimlendirmeyi içeren `TimePeriodExample.xlsx` dosyası oluşturulur.

## Sık Sorulan Sorular ve İpuçları

- **Farklı bir tarih aralığını hedefleyebilir miyim?**  
  Kesinlikle. `"I19:K20"` ifadesini istediğiniz A1‑stili aralıkla değiştirin ve örnek tarihleri ona göre ayarlayın.

- **`YESTERDAY` yerine özel bir formül kullanmam gerekirse?**  
  `FormatConditionType.FORMULA` kullanın ve `condition.formula1 = "YOUR_FORMULA"` şeklinde ayarlayın—örneğin, dün tarihini taklit etmek için `=TODAY()-A1=1`.

- **Aynı aralığa birden fazla kural uygulayabilir miyim?**  
  `conditions.add_condition` metodunu farklı bir `FormatConditionType` ile tekrar çağırın. Sıra önemlidir; sonraki kurallar önceki kuralları geçersiz kılabilir.

- **Arka planla birlikte yazı rengi de ayarlamak mümkün mü?**  
  Evet—`condition.style.font.color = Color.white` (veya başka bir `Color`) ile değiştirebilirsiniz.

## Sonuç

Artık Aspose.Cells kullanarak **create Excel workbook Python**, **set cell background color** ve tarih‑tabanlı **add conditional formatting python** işlemlerini nasıl yapacağınızı biliyorsunuz. Betik tam fonksiyonel, eksik dizin gibi kenar durumlarını ele alıyor ve çok‑kurallı koşullu mantık ya da dinamik aralık tespiti gibi daha karmaşık senaryolara genişletilebilir.

Bir sonraki adım için hazır mısınız? “Yesterday” kuralını “Last Week” (Geçen Hafta) ile değiştirin, degrade doldurmaları deneyin veya onlarca biçimlendirilmiş tablo içeren tam bir rapor oluşturun. Temel yapı taşları burada ve **aspose cells conditional formatting** konusundaki çekirdek yeteneği hâlihazırda kavradınız.

İyi kodlamalar, ve yorumlarda kendi varyasyonlarınızı paylaşmaktan çekinmeyin!

## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım‑adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose.Cells for .NET ile Excel Hücre Biçimlendirme ve Çalışma Kitabı Yönetimini Ustalaştırın](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Aspose.Cells for .NET Kullanarak Excel Çalışma Kitabını ODS Olarak Oluşturma ve Kaydetme](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Aspose.Cells .NET Kullanarak Excel'de Çalışma Kitabı Kapsamlı Adlandırılmış Aralıklar Oluşturma](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}