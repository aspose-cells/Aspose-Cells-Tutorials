---
category: general
date: 2026-08-01
description: Aspose.Cells kullanarak Python ile Excel çalışma kitabı oluşturun – Excel
  sütununu otomatik sığdırmayı öğrenin, hücreleri tarih ile biçimlendirin, hücre tarih
  formatını ayarlayın ve koşullu biçimlendirme uygulayın.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- auto fit excel column
- format cells by date
- set cell date format
- aspose cells conditional formatting
language: tr
lastmod: 2026-08-01
og_description: Python ile Excel çalışma kitabını anında oluşturun. Bu kılavuzu izleyerek
  Excel sütunlarını otomatik olarak ayarlayın, hücreleri tarihe göre biçimlendirin,
  hücre tarih formatını belirleyin ve Aspose Cells koşullu biçimlendirmesinde uzmanlaşın.
og_image_alt: Screenshot showing a Python script that creates an Excel workbook using
  Aspose.Cells
og_title: Python ile Excel Çalışma Kitabı Oluşturma – Aspose.Cells ile Adım Adım
schemas:
- author: Aspose
  dateModified: '2026-08-01'
  description: Create Excel workbook python using Aspose.Cells – learn auto fit excel
    column, format cells by date, set cell date format and apply conditional formatting.
  headline: Create Excel Workbook Python – Full Guide with Aspose.Cells
  type: TechArticle
tags:
- Aspose Cells
- Python
- Excel automation
- Conditional Formatting
- Date handling
title: Python ile Excel Çalışma Kitabı Oluşturma – Aspose.Cells ile Tam Kılavuz
url: /tr/python/formatting/create-excel-workbook-python-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python ile Excel Çalışma Kitabı Oluşturma – Aspose.Cells ile Tam Kılavuz

Hiç **create Excel workbook python** betikleri manuel olarak Excel açmadan şık görünür mü? Tek değilsiniz. Raporlama panosu oluşturuyor ya da günlük veri dökümlerini otomatikleştiriyor olun, Python’dan Excel dosyası üretme yeteneği bir oyun değiştiricidir.

Bu öğreticide, yalnızca bir çalışma kitabı oluşturan değil, aynı zamanda **auto fit excel column**, **format cells by date**, **set cell date format** ve **aspose cells conditional formatting** gösteren eksiksiz, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, herhangi bir projeye ekleyebileceğiniz bağımsız bir betiğiniz olacak.

> **Pro tip:** Aspose.Cells for Python via .NET, COM bağımlılığı olmadan Excel dosyalarıyla çalışmanıza olanak tanır; bu da Linux konteynerleri veya CI boru hatları için mükemmeldir.

## İhtiyacınız Olanlar

- **Python 3.8+** (kod herhangi bir yeni sürümde çalışır)  
- **Aspose.Cells for Python via .NET** – `pip install aspose-cells` ile kurun  
- Yazma izniniz olan bir klasör (biz `YOUR_DIRECTORY` olarak adlandıracağız)  
- Python fonksiyonları ve nesneleri hakkında temel bir anlayış (derin Excel bilgisi gerekmez)  

Eğer bunlara sahipseniz, harika—hadi başlayalım.

## Adım 1: Python ile Excel Çalışma Kitabı Oluşturma – Çalışma Kitabını Başlatma

İlk olarak yeni bir çalışma kitabı nesnesi oluşturuyoruz. Bunu, sonraki tüm işlemlerin yeni bir öğe eklediği boş bir tuval gibi düşünün.

```python
from aspose.cells import Workbook, SaveFormat, FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color
from datetime import datetime
import os

# Create a new workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

> **Neden önemli:** `Workbook()` bir `.xlsx` dosyasının bellek içi temsilini oluşturur. `worksheets[0]` ile varsayılan sayfayı alırız; veri ve biçimlendirme için hazırdır.

## Adım 2: Hedef Aralığı ve Temel Rengi Tanımlama – Koşullu Biçimlendirme İçin Hazırlık

Koşullu mantık eklemeden önce, kuralın uygulanacağı bir aralığa ihtiyacımız var. `I19:K20` aralığı keyfi bir seçimdir ancak birden fazla hücreyi gösterecek kadar büyüktür.

```python
# Add a conditional formatting collection to the range and set a base colour
conds = worksheet.conditional_formattings.add("I19:K20", Color.medium_sea_green)
```

`add` yöntemi hem biçimlendirme nesnesini oluşturur hem de ona varsayılan bir arka plan verir; bu da sonraki kuralın öne çıkmasını sağlar.

## Adım 3: Aspose Cells Koşullu Biçimlendirme – YESTERDAY için TIME_PERIOD Kuralı Uygulama

Şimdi demomuzun kalbine geliyoruz: **TIME_PERIOD** koşulu, dün tarihini içeren hücreleri vurgular.

```python
# Insert a TIME_PERIOD condition for YESTERDAY
condition_index = conds.add_condition(FormatConditionType.TIME_PERIOD)
condition = conds[condition_index]

# Configure the rule – yesterday, pink background, solid fill
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

> **Açıklama:** `FormatConditionType.TIME_PERIOD`, Aspose’a tarih‑tabanlı bir kuralla çalıştığımızı söyler. `time_period` değerini `YESTERDAY` olarak ayarladığımızda, motor her hücrenin değerini bir önceki takvim günüyle otomatik olarak karşılaştırır.

## Adım 4: Örnek Tarihlerle Doldurma – Hücre Tarih Biçimini Ayarla ve Kuralı Doğrula

Kuralın çalıştığını görmek için gerçek tarihlere ihtiyacımız var. Ayrıca **set cell date format** ile değerlerin okunabilir tarih olarak görünmesini sağlayacağız.

```python
# Cell I19 – a date that falls on “yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))          # July 30, 2008 is “yesterday” for demo purposes
style_i19 = cell_i19.get_style()
style_i19.number = 30          # 30 = built‑in Excel date format (e.g., mm/dd/yyyy)
cell_i19.set_style(style_i19)

# Cell K20 – a date outside the period (no formatting applied)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)
```

Her iki hücrede de aynı **format cells by date** numarasını (`30`) kullandığımıza dikkat edin. Bu, sistem yerel ayarından bağımsız olarak tarihlerin tutarlı görüntülenmesini sağlar.

## Adım 5: Açıklayıcı Bir Etiket Ekle – Sayfayı Kendini Açıklayan Hale Getirme

Küçük bir etiket, dosyayı açan herkesin renkli hücrelerin neyi temsil ettiğini anlamasına yardımcı olur.

```python
worksheet.cells.get("I20").put_value("Yesterday")
```

## Adım 6: Auto Fit Excel Column – Sütun Genişliklerini Otomatik Ayarlama

Verileri programatik olarak oluşturduğunuzda, sütun genişlikleri genellikle varsayılan dar boyutta kalır. **auto fit excel column** yöntemi, içeriği gösterecek kadar genişletir.

```python
# Auto‑fit the 12th column (which corresponds to column L) so the label is fully visible
worksheet.auto_fit_column(12)
```

> **Neden sütun 12?** Sıfır‑tabanlı indekslemede, sütun `12` Excel’de `L` sütununa karşılık gelir. Düzeni değiştirirseniz indeksi ayarlayın.

## Adım 7: Çalışma Kitabını Kaydet – Gerçek Bir Dosyaya Dışa Aktarma

Son olarak her şeyi diske kalıcı hâle getiriyoruz. `SaveFormat.XLSX` bayrağı, modern, zip‑tabanlı bir çalışma kitabı oluşturulmasını sağlar.

```python
output_file = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_file, SaveFormat.XLSX)
print(f"Workbook saved to {output_file}")
```

### Beklenen Sonuç

`TimePeriodDemo.out.xlsx` dosyasını Excel’de (veya herhangi bir görüntüleyicide) açın; şunları görmelisiniz:

- **I19** hücresi, tarihi “dün” olduğu için **pembe** renkle vurgulanmış.  
- **K20** hücresi değişmemiş, koşullu kuralın tarih dışındaki hücreleri doğru şekilde görmezden geldiğini gösteriyor.  
- **L** sütunu otomatik olarak boyutlandırılmış, böylece “Yesterday” etiketi kesilmemiş.

![Create Excel workbook python example](/images/create_excel_workbook_python.png){: .center-image alt="Create Excel workbook python example showing conditional formatting for yesterday's date"}

## Yaygın Varyasyonlar ve Kenar Durumları

| Durum | Nasıl Ayarlanır |
|-----------|---------------|
| **Farklı tarih aralığı** | `condition.time_period` değerini `TimePeriodType.TODAY`, `TimePeriodType.LAST_7_DAYS` vb. olarak değiştirin. |
| **Birden fazla koşul** | `conds.add_condition()` metodunu tekrar çağırın ve yeni bir `FormatConditionType` (ör. `FORMAT_CONDITION_TYPE.EXPRESSION`) yapılandırın. |
| **Özel tarih biçimi** | `style_i19.number = 14` ile `mm-dd-yy` biçimini kullanın veya `style_i19.custom = "dd-mmm-yyyy"` gibi özel bir biçim dizesi atayın. |
| **Büyük çalışma sayfaları** | `auto_fit_column` çağrısını bir try/except bloğuna sararak büyük dosyalarda performans düşüşünü önleyin. |
| **Başlıksız CI ortamında çalıştırma** | UI gerekmez; Aspose tamamen bellek içinde çalışır, bu sayede Excel yüklü olmayan bir Docker konteynerinde dosyayı üretebilirsiniz. |

## Özet – Neler Öğrendik

- **Create Excel workbook python**'ı Aspose.Cells ile sıfırdan oluşturduk.  
- **Auto fit excel column** ile çıktıyı düzenli tutmayı sağladık.  
- **Format cells by date** ve **set cell date format** ile tutarlı tarih gösterimi elde ettik.  
- `TIME_PERIOD` tipiyle **aspose cells conditional formatting** uyguladık.

Tüm bunlar, faturalar, günlük loglar veya tarihlerin görsel ipuçları oluşturduğu herhangi bir senaryo için uyarlayabileceğiniz tek bir, kolay‑çalıştırılabilir betiğe sığdırıldı.

## Sonraki Adımlar

Temelleri kavradıysanız, aşağıdakileri keşfetmeyi düşünün:

- **Veri çubukları, renk ölçekleri ve simge setleri** ile daha zengin koşullu stil oluşturma.  
- `worksheet.pivot_tables.add()` ile **PivotTable** oluşturma.  
- `workbook.save("report.pdf", SaveFormat.PDF)` ile **PDF’ye dışa aktarma**.  

Bu konular, burada kullandığımız aynı temel kavramlar üzerine inşa edildiği için kendinizi hemen rahat hissedeceksiniz.

---

*Keyifli kodlamalar! Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın veya daha derin bilgiler için Aspose.Cells for Python belgelerine göz atın.*

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak ilgili konuları ayrıntılı bir şekilde ele alır. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [Auto-Fit Rows & Columns in Excel using Aspose.Cells Java for Seamless Workbook Management](/cells/english/java/range-management/aspose-cells-java-auto-fit-rows-columns/)
- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Automate Excel Column Widths&#58; Auto-Fit Columns using Aspose.Cells for .NET](/cells/english/net/range-management/excel-automation-auto-fit-columns-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}