---
category: general
date: 2026-07-14
description: Dakikalar içinde hücre arka plan rengini ayarlayan, tarih aralığına göre
  hücreleri vurgulayan ve çalışma kitabını XLSX olarak kaydeden bir Excel çalışma
  kitabı Python kodu oluşturun.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: tr
lastmod: 2026-07-14
og_description: Python ile Excel çalışma kitabını anında oluşturun. Hücre arka plan
  rengini ayarlamayı, tarih aralığına göre hücreleri vurgulamayı ve Aspose.Cells ile
  çalışma kitabını XLSX olarak kaydetmeyi öğrenin.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Python ile Excel Çalışma Kitabı Oluştur – Adım Adım Koşullu Biçimlendirme
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Python ile Excel Çalışma Kitabı Oluşturma – Koşullu Biçimlendirme ile Tam Kılavuz
url: /tr/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel Çalışma Kitabı Python Oluşturma – Koşullu Biçimlendirme ile Tam Kılavuz

Hiç **create excel workbook python** betikleriyle Excel'i manuel olarak açmadan şık görünümler elde etmeyi düşündünüz mü? Yalnız değilsiniz. Birçok veri odaklı projede elektronik tablolar oluşturmalı, hücreleri renk kodlamalı ve belirli bir aralıktaki tarihleri işaretlemeliyiz—hepsi saf Python kodundan.

Bu öğreticide, Aspose.Cells kütüphanesini kullanarak **creates an Excel workbook python**, **sets cell background color**, **conditional formatting based on date** uygular ve sonunda **saves workbook as xlsx**. Sonunda, herhangi bir otomasyon hattına ekleyebileceğiniz yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

## Öğrenecekleriniz

- Bir çalışma kitabını başlatma ve ilk çalışma sayfasını alma.  
- Herhangi bir hücre aralığı için koşullu‑biçimlendirme koleksiyonu ekleyen yardımcı fonksiyon.  
- **conditional formatting based on date** kullanarak dünkü girişleri vurgulama.  
- Düzenli bir görünüm için sütun genişliklerini ayarlama.  
- **save workbook as xlsx** ile sonucu kalıcı hale getirme.  

Harici bir Excel kurulumu gerekmez—Aspose.Cells her şeyi bellek içinde yönetir.

## Önkoşullar

- Python 3.8+ yüklü.  
- `aspose-cells` paketi (`pip install aspose-cells`).  
- Python fonksiyonları ve datetime nesneleri hakkında temel bilgi.  

Aspose.Cells'i daha önce hiç kullanmadıysanız, Excel'in nesne modelini taklit eden güçlü, saf‑Python API'si olarak düşünün. Office paketi bulunmadığında sunucu‑tarafı oluşturma için mükemmeldir.

## Adım 1: Çalışma Kitabını Başlatma (Create Excel Workbook Python)

İlk iş olarak, **create excel workbook python** tarzında bir şey yapmamız gerekiyor. Bu adım boş bir çalışma kitabı nesnesi oluşturur ve varsayılan çalışma sayfasına yönlendirir.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **Neden önemli:** `Workbook` sınıfı her Excel işleminin giriş noktasını oluşturur. Programatik olarak oluşturduğumuzda manuel dosya işlemlerinden kaçınırız.

## Adım 2: Koşullu‑Biçimlendirme Koleksiyonu Eklemek İçin Yardımcı (Set Cell Background Color)

Koşullu biçimlendirme, bir aralığa eklenmiş bir *koleksiyon* içinde bulunur. Bu tekrarı, tüm aralık için **set cell background color** yapmamıza da izin veren küçük bir yardımcı fonksiyonla sarmalayalım.

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **Pro tip:** Yardımcı kullanmak ana akışı temiz tutar ve aynı mantığı birden fazla aralıkta yeniden kullanmayı kolaylaştırır.

## Adım 3: Tarihe Göre Koşullu Biçimlendirme Uygulama (Highlight Cells Based on Date Range)

Şimdi gerçekten **highlight cells based on date range** yapacağız. Örnek “yesterday” üzerine odaklanıyor, ancak `TimePeriodType.YESTERDAY` değerini `TODAY`, `LAST_WEEK` vb. ile değiştirebilirsiniz.

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **Ne oluyor?**  
> 1. Önce tüm aralığa nötr bir yeşil arka plan veriyoruz.  
> 2. Ardından, hücrenin tarihi dünküyle eşleştiğinde doldurmayı pembe **sadece** olarak değiştiren bir `TIME_PERIOD` koşulu ekliyoruz.  
> 3. `TimePeriodType` enum'ı tarih hesaplamasını soyutlar, böylece özel bir mantık yazmanıza gerek kalmaz.

## Adım 4: Örnek Tarihleri Doldurma (So the Rule Can Be Evaluated)

Kuralı gözlemlemek için sayfaya birkaç tarih ekleyeceğiz. Biri “yesterday” penceresine, diğeri ise dışına düşüyor.

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **Köşe durum notu:** Çalışma kitabınız farklı yerel ayarlarda açılacaksa, tutarlı bir görüntü sağlamak için `date_style.custom = "dd‑mm‑yyyy"` kullanmayı düşünün.

## Adım 5: Düzeni Düzenleme (Auto‑Fit Columns)

Sıkışık bir elektronik tablo profesyonel görünmez. **adjust column width for a tidy output** yapalım.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **Neden otomatik sığdırma?** Uzun etiketlerin veya tarihlerin tamamen görünür olmasını sağlar; bu, dosyayı teknik olmayan paydaşlarla paylaştığınızda özellikle önemlidir.

## Adım 6: Çalışma Kitabını Kaydetme (Save Workbook As XLSX)

Son olarak, **save workbook as xlsx**'i istediğiniz bir konuma kaydediyoruz. `SaveFormat.XLSX` sabiti, Aspose.Cells'in modern OpenXML formatını yazmasını söyler.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Görmeniz gereken sonuç:**  
> - I19 ve K20 hücrelerinde tarihler bulunur.  
> - I19 (dün) pembe renkle vurgulanırken, K20 yeşil kalır.  
> - L sütunu “Yesterday” etiketine sığacak şekilde otomatik genişler.  

`TimePeriodDemo.xlsx` dosyasını Excel'de açarsanız, koşullu biçimlendirme zaten uygulanmış olur—ek bir adım gerekmez.

---

![Dünün vurgulanan tarihini gösteren Excel sayfası](https://example.com/images/excel-demo.png "Oluşturulan Excel dosyasının vurgulanan hücreleri gösteren ekran görüntüsü")

*Yukarıdaki görsel, son çalışma kitabını gösterir; dün tarihini içeren hücrenin pembe vurgusuna dikkat edin.*

## Özet: Başardıklarımız

- **Created an Excel workbook python**'ı Aspose.Cells kullanarak sıfırdan oluşturduk.  
- Sayfaya görsel bir ipucu vermek için tüm aralıkta **set cell background color** uyguladık.  
- Dünkü girişleri otomatik olarak işaretlemek için **conditional formatting based on date** uyguladık.  
- **Saved workbook as xlsx**'i kaydettik, dağıtıma veya daha fazla işleme hazır.  

Tüm bunlar 60 satırdan az Python kodu ile yapıldı ve kod, Aspose.Cells çalışma zamanını destekleyen herhangi bir platformda çalışır.

## Sonraki Adımlar ve İlgili Konular

Bu içeriği faydalı bulduysanız, aşağıdaki konuları da inceleyebilirsiniz:

- **set cell background color** tüm satırlar için durum değerlerine göre (ör. “Completed”, “Pending”).  
- **highlight cells based on date range** kullanarak kayan pencereler oluşturma (son 7 gün, mevcut ay).  
- `SaveFormat.CSV` veya `SaveFormat.PDF` ile **CSV** veya **PDF** gibi diğer formatlara dışa aktarma.  
- Programatik olarak **charts** ekleyerek biçimlendirdiğiniz verileri görselleştirme.  

Tarih mantığını istediğiniz gibi ayarlayın, renk paletini değiştirin veya aralığı tüm sütunları kapsayacak şekilde genişletin. Desen aynı kalır: bir çalışma kitabı oluşturun, koşullu‑biçimlendirme koleksiyonu ekleyin, kuralı tanımlayın ve kaydedin.

Belirli bir kullanım senaryosu hakkında sorularınız mı var? Aşağıya yorum bırakın, iyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}