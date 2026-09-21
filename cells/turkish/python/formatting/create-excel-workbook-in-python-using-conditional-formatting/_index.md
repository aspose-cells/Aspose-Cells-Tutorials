---
category: general
date: 2026-09-21
description: Python'da Excel çalışma kitabı oluşturmayı, hücre arka plan rengini ayarlamayı
  ve Aspose.Cells ile tarih tabanlı koşullu biçimlendirme uygulamayı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: tr
lastmod: 2026-09-21
og_description: Python'da Excel çalışma kitabı oluşturun, hücre arka plan rengini
  ayarlayın ve Aspose.Cells kullanarak tarih tabanlı koşullu biçimlendirme uygulayın.
  Adım adım kılavuzu izleyin.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Python'da koşullu biçimlendirme ile Excel çalışma kitabı oluştur
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Python ile koşullu biçimlendirme kullanarak Excel çalışma kitabı oluştur
url: /tr/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da koşullu biçimlendirme kullanarak Excel çalışma kitabı oluşturma

Tarihler otomatik olarak vurgulayan **create Excel workbook python** betiklerine ihtiyacınız varsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. **set cell background color** nasıl yapılır, “Yesterday” kuralı nasıl eklenir ve dosya nasıl kaydedilir—hepsi Aspose.Cells for Python ile.

Excel dosyalarıyla programatik olarak çalışmak, genellikle aynı biçimlendirme mantığını birçok sayfada tekrarlamak anlamına gelir. Bu öğreticinin sonunda, **excel conditional formatting python** için herhangi bir projeye ekleyebileceğiniz yeniden kullanılabilir bir desen elde edeceksiniz.

## Önkoşullar

- Python 3.8+ yüklü  
- `aspose-cells` paketi (`pip install aspose-cells`)  
- Python fonksiyonları ve datetime modülü hakkında temel bilgi  

Ek bir kütüphane gerekmez; Aspose.Cells tüm Excel işlemlerini yönetir.

## Adım 1: Çalışma kitabını oluşturun ve ilk çalışma sayfasına erişin

İlk adım, **create excel workbook python** nesnelerini oluşturmak ve varsayılan çalışma sayfasını almak. Bu, sonraki stil uygulamaları için temiz bir tuval sağlar.

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Neden önemli:* `Workbook()` bellekte bir Excel dosyası oluşturur. `worksheets[0]` erişimi, sayfa adlarını sabit kodlamaktan kaçınır ve varsayılan ad değişse bile çalışır.

## Adım 2: TIME_PERIOD koşullu biçimini eklemek için yardımcı fonksiyon

Kodu düzenli tutmak için, koşullu‑biçim oluşturmayı bir yardımcı fonksiyon içinde sararız. Bu fonksiyon bir hücre aralığı, bir arka plan rengi ve istenen zaman‑periyodu kuralını alır.

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*Neden önemli:* Yardımcı, koşullu biçim oluşturmanın tekrarlayan adımlarını soyutlayarak “Today” veya “Last Week” gibi diğer tarih‑tabanlı kurallar için yeniden kullanımı kolaylaştırır.

## Adım 3: “Yesterday” kuralını bir aralığa uygulayın

Şimdi, yardımcı fonksiyonu dün tarihini içeren hücreleri vurgulamak için kullanıyoruz. `I19:K20` aralığı koşul sağlandığında **medium sea green** renge dönüşür.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Neden önemli:* `TimePeriodType.YESTERDAY`, Aspose.Cells’in yerleşik enumarasyonunun bir parçasıdır, bu yüzden tarihleri manuel olarak hesaplamanıza gerek yoktur. Kütüphane, çalışma kitabı her açıldığında kuralı değerlendirir.

## Adım 4: Aralığı örnek tarihlerle doldurun

Kuralın nasıl çalıştığını görmek için iki tarih yazıyoruz—biri “Yesterday” ile eşleşen, diğeri ise eşleşmeyen. `number` stili `30`, yerleşik bir tarih formatına karşılık gelir.

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*Neden önemli:* Somut tarihler ekleyerek, dosyayı belirli bir günde açmaya gerek kalmadan koşullu biçimlendirmenin çalıştığını doğrulayabilirsiniz.

## Adım 5: Açıklayıcı bir etiket ekleyin ve sütunu otomatik sığdırın

Küçük bir etiket, biçimlendirilmiş aralığın amacını netleştirir ve `auto_fit_column` sayfanın okunabilir olmasını sağlar.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## Adım 6: Çalışma kitabını kaydedin

Son olarak, çalışma kitabını diske yazın. `os.makedirs` çağrısı hedef klasörün var olduğundan emin olur.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

*TimePeriodDemo.xlsx* dosyasını açtığınızda şunları göreceksiniz:

- **I19** hücresi, değeri “Yesterday” kuralıyla eşleştiği için **medium sea green** renkle gölgelendirilir.  
- **K20** hücresi, tarihi koşulu sağlamadığı için varsayılan arka planı korur.  

Bu, tek bir Python satırı kullanarak **format cells by date** işlemini gösterir.

## Tam, çalıştırılabilir örnek

Tüm parçaları bir araya getirerek, kopyalayıp yapıştırıp çalıştırabileceğiniz tam betik burada:

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Betik çalıştırın, ortaya çıkan dosyayı açın ve koşullu biçimlendirmenin çalıştığını göreceksiniz.

## Yaygın varyasyonlar ve kenar durumları

| Varyasyon | Nasıl uygulanır | Ne zaman kullanılır |
|-----------|------------------|---------------------|
| **“Today” vurgulama** | `TimePeriodType.YESTERDAY` yerine `TimePeriodType.TODAY` kullanın | Gerçek‑zaman panoları |
| **Birden fazla aralık** | Her aralık için `add_time_period` çağırın, farklı renkler geçirin | Karmaşık raporlar |
| **Dinamik tarih aralığı** | `TimePeriodType.LAST_7_DAYS` veya `TimePeriodType.NEXT_MONTH` kullanın | Sürekli raporlar |
| **Özel renk** | Herhangi bir tonu oluşturmak için `Color.from_argb(255, r, g, b)` kullanın | Marka‑uyumlu stil |

**Pro ipucu:** Katı bir dolgu istediğinizde her zaman `condition.style.pattern = BackgroundType.SOLID` ayarlayın; aksi takdirde Excel, sürümler arasında tutarsız görünen bir degrade gösterebilir.

## Sonuç

Artık Aspose.Cells kullanarak **create Excel workbook python** betiklerinin **set cell background color** ayarladığını, **excel conditional formatting python** uyguladığını ve **format cells by date** yaptığını biliyorsunuz. Örnek, **date based conditional formatting** senaryosunu kapsıyor, ancak aynı desen herhangi bir zaman‑periyodu kuralı için çalışır.

Sonraki adımda şunları keşfedebilirsiniz:

- Veri çubukları veya simge setleri ekleme (`FormatConditionType.DATA_BAR`)  
- Aynı aralıkta birden fazla koşullu kuralı birleştirme  
- Raporlama için çalışma kitabını PDF olarak dışa aktarma (`SaveFormat.PDF`)  

Farklı renkler, aralıklar ve zaman‑periyodu türleriyle denemeler yapmaktan çekinmeyin; böylece raporlama ihtiyaçlarınıza uygun hale getirebilirsiniz. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells for .NET ile Excel Hücre Biçimlendirme ve Çalışma Kitabı Yönetimini Öğrenin](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Aspose.Cells .NET ile Excel Otomasyonu: Çalışma Kitabı Oluşturma & Dış Bağlantıları Ayarlama](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Aspose.Cells .NET kullanarak Excel'de Çalışma Kitabı Kapsamlı Adlandırılmış Aralıklar Oluşturma](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}