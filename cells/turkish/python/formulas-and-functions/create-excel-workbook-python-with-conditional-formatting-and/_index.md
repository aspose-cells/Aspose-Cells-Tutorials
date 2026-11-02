---
category: general
date: 2026-10-04
description: Aspose.Cells kullanarak Python ile Excel çalışma kitabı oluşturun. Python’da
  Excel koşullu biçimlendirmeyi, hücre arka plan rengini ve hücre tarih biçimlendirmesini
  tam bir örnek içinde öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: tr
lastmod: 2026-10-04
og_description: Aspose.Cells kullanarak Python ile Excel çalışma kitabı oluşturun.
  Bu öğreticide, Python ile Excel koşullu biçimlendirme, hücre arka plan rengi ve
  hücre tarih biçimlendirme adım adım gösterilmektedir.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Python ile Excel çalışma kitabı oluşturma – koşullu biçimlendirme içeren
  tam rehber
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Python ile koşullu biçimlendirme ve hücre arka plan rengi içeren Excel çalışma
  kitabı oluştur
url: /tr/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Koşullu biçimlendirme ve hücre arka plan rengiyle Excel çalışma kitabı oluşturma python

Eğer **create Excel workbook python** hızlı bir şekilde oluşturmanız gerekiyorsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. **excel conditional formatting python**, **cell background color python** değiştirir ve **format cells date python** ile “Yesterday” vurgusu ekleyen eksiksiz, çalıştırılabilir bir örnek göreceksiniz.  

Birçok raporlama senaryosunda renkli bir hücrenin görsel ipucu, veriyi anında anlaşılır kılar. Bu öğretici, kodun her satırını adım adım anlatır, her adımın neden önemli olduğunu açıklar ve kendi projelerinize uyarlayabileceğiniz hazır‑çalıştırılabilir bir betik sunar.

## Başaracaklarınız

Bu makalenin sonunda şunları yapabilecek:

1. **create Excel workbook python** Aspose.Cells kütüphanesini kullanarak.  
2. **excel conditional formatting python** otomatik olarak “Yesterday” tarihlerini vurgulayan bir biçimlendirme uygular.  
3. **cell background color python**'ı pembe (veya tercih ettiğiniz herhangi bir renk) olarak ayarlar.  
4. **format cells date python** tarihlerin standart Excel tarih biçiminde görünmesini sağlar.  

Aspose.Cells ile ilgili önceden bir deneyime gerek yok—sadece çalışan bir Python 3 ortamı ve pip erişimi yeterli.

## Önkoşullar

- Python 3.8 veya daha yeni bir sürüm yüklü.  
- `aspose-cells` ve `aspose-pydrawing` paketleri `pip install aspose-cells aspose-pydrawing` ile kurulu.  
- Python sözdizimi ve Excel kavramları (çalışma kitapları, çalışma sayfaları, hücreler) hakkında temel bilgi.  

> **Pro ipucu:** Betiği bir sanal ortamda çalıştırırsanız, diğer projelerle sürüm çakışmalarını önlersiniz.

## Adım 1: Projeyi kurun ve gerekli sınıfları içe aktarın

**create Excel workbook python** yaparken ilk adım, ihtiyacınız olan Aspose.Cells sınıflarını içe aktarmaktır. Bu sınıflar, çalışma kitabı oluşturma, koşullu biçimlendirme ve stil uygulamaya doğrudan erişim sağlar.

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*Bu neden önemlidir:* Yalnızca gereken sembolleri içe aktarmak ad alanını temiz tutar ve betiği okumayı kolaylaştırır. `Workbook` **create Excel workbook python** için giriş noktası iken, `FormatConditionType` ve `TimePeriodType` **excel conditional formatting python** için gereklidir.

## Adım 2: Yeni bir çalışma kitabı oluşturun ve ilk çalışma sayfasını alın

Şimdi gerçekten **create Excel workbook python**. `Workbook()` yapıcı, varsayılan bir çalışma sayfası içeren boş bir Excel dosyası oluşturur.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Açıklama:* Her Excel dosyası en az bir çalışma sayfası ile başlar. Varsayılan olarak Aspose.Cells ona “Sheet1” adını verir. Daha sonra daha fazla sayfa ekleyebilirsiniz, ancak bu gösterimde tek bir sayfa örneği odaklamak için yeterlidir.

## Adım 3: Koşullu biçimlendirme için hedef aralığı tanımlayın

Koşullu biçimlendirme dikdörtgen bir aralıkta çalışır. Burada `I19:K20` aralığını seçiyoruz; bu bize üç sütun ve iki satır verir.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Bunu neden yapıyoruz:* `get` yöntemi, belirtilen aralıkla ilişkili bir `ConditionalFormatting` nesnesi döndürür. Eğer aralıkta henüz bir biçimlendirme yoksa, Aspose.Cells otomatik olarak yeni bir koleksiyon oluşturur.

## Adım 4: Bir TIME_PERIOD koşulu ekleyin ve arka plan rengini ayarlayın

Bu, **excel conditional formatting python**'ın çekirdeğidir. “Yesterday” tarihlerini içeren hücreleri vurgulayan bir `TIME_PERIOD` kuralı ekliyoruz.

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*Derinlemesine:*  
- `FormatConditionType.TIME_PERIOD`, Excel'in tarihleri geçerli tarihe göre değerlendirmesini söyler.  
- `TimePeriodType.YESTERDAY`, her gün otomatik olarak güncellenen yerleşik bir enum'dur; böylece çalışma kitabı her zaman en son “Yesterday” tarihini vurgular.  
- `background_color`'ı `Color.pink` ve deseni `SOLID` olarak ayarlayarak **cell background color python** etkisini ekstra VBA kodu olmadan elde ederiz.

## Adım 5: Aralığı örnek tarihlerle doldurun ve tarih biçimlendirmesini uygulayın

Koşullu biçimlendirmeyi görmek için gerçek tarih değerlerine ihtiyacımız var. Ayrıca **format cells date python** yaparak Excel'in hücreleri sayı yerine tarih olarak algılamasını sağlarız.

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*Açıklama:*  
- `style.number = 30` satırı **format cells date python** adımıdır. Biçim kodu 30, kısa tarih formatına (`m/d/yy`) karşılık gelir.  
- Yardımcı bir fonksiyon kullanmak kodu DRY (Don’t Repeat Yourself) tutar ve daha fazla tarih eklemeyi kolaylaştırır.

## Adım 6: Açıklayıcı bir etiket ekleyin

Küçük bir etiket, çalışma kitabını açan herkesin hücrelerin neden renkli olduğunu anlamasına yardımcı olur.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## Adım 7: Çalışma kitabını diske kaydedin

Son olarak, `save` metodunu çağırarak **create Excel workbook python**'ı diske yazarız. `SaveFormat.XLSX` sabiti dosyanın modern Office Open XML formatında olmasını sağlar.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

`TimePeriodDemo.xlsx` dosyasını Excel'de açtığınızda şunları göreceksiniz:

- `I19` ve `K20` hücreleri tarih içerir.  
- “Yesterday” ile eşleşen hücre (bu statik örnekte `I19`) pembe renkle vurgulanır.  
- “Yesterday” etiketi `I20` hücresinde görünür.  

> **İpucu:** Betiği farklı bir günde çalıştırırsanız, koşullu biçimlendirme hâlâ geçerli sistem tarihinden tam bir gün önceki tarihi vurgular—kodda hiçbir değişiklik yapmanıza gerek kalmaz.

## Tam betik – kopyalayıp çalıştırmaya hazır

Aşağıda, yukarıdaki tüm adımları içeren eksiksiz, bağımsız program yer alıyor. `conditional_format_demo.py` adlı bir dosyaya kopyalayın, `YOUR_DIRECTORY`'yi ayarlayın ve `python conditional_format_demo.py` ile çalıştırın.

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Beklenen çıktı

Betik çalıştırıldığında bir onay satırı yazdırır:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Oluşturulan dosyayı açtığınızda “Yesterday” kuralına uyan hücrede pembe arka plan görürsünüz; bu da **excel conditional formatting python** ve **cell background color python**'ın birlikte çalıştığını kanıtlar.

## Yaygın varyasyonlar ve kenar durumları

| Durum | Kodu nasıl uyarlarsınız |
|-----------|-----------------------|
| **Farklı vurgulama rengi** | `Color.pink` yerine `Color.light_green` gibi başka bir `Color` sabiti kullanın. |
| **“Yesterday” yerine “Today” vurgulama** | `condition.time_period = TimePeriodType.TODAY` olarak ayarlayın. |
| **Bir bütün sütuna biçimlendirme uygulama** | `"A:A"` gibi bir aralık kullanın ve `target_range` değişkenini buna göre ayarlayın. |
| **Özel tarih formatı kullanma** | Daha okunabilir bir format için `style.number = 30` yerine `style.custom = "dd-mmm-yyyy"` kullanın. |
| **Aynı aralıkta birden fazla koşul** |  |

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak eksiksiz çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Excel Çalışma Kitabı Python Oluşturma – Lambda ile Tam Kılavuz](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Aspose.Cells Kullanarak ASP.NET'te Excel Çalışma Kitabını PDF Olarak Oluşturma ve Kaydetme](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Aspose.Cells for .NET Kullanarak Excel Çalışma Kitabını ODS Olarak Oluşturma ve Kaydetme](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}