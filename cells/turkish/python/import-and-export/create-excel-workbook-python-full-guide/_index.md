---
category: general
date: 2026-06-21
description: Excel çalışma kitabı Python öğreticisi oluşturun; MAP fonksiyonunu ve
  lambda ifadesini kullanarak Santigrayı Fahrenheit'a hızlı bir şekilde dönüştürmeyi
  gösteren.
draft: false
keywords:
- create excel workbook python
- convert celsius to fahrenheit
- use map function
- how to use map
- how to use lambda
language: tr
og_description: Python ile Excel çalışma kitabı oluşturun ve MAP fonksiyonunu lambda
  ile kullanarak Celsius’u Fahrenheit’e dakikalar içinde dönüştürmeyi öğrenin.
og_title: Python ile Excel Çalışma Kitabı Oluşturma – Adım Adım Rehber
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create Excel workbook Python tutorial showing how to use MAP function
    and lambda to convert Celsius to Fahrenheit quickly.
  headline: Create Excel Workbook Python – Full Guide
  type: TechArticle
- description: Create Excel workbook Python tutorial showing how to use MAP function
    and lambda to convert Celsius to Fahrenheit quickly.
  name: Create Excel Workbook Python – Full Guide
  steps:
  - name: '**How to use map** for multi‑column transformations, e.g., converting temperatures
      and rounding in one go.'
    text: '**How to use map** for multi‑column transformations, e.g., converting temperatures
      and rounding in one go.'
  - name: '**How to use lambda** to embed conditional logic: `LAMBDA(c, IF(c<0, "below
      freezing", c*9/5+32))`.'
    text: '**How to use lambda** to embed conditional logic: `LAMBDA(c, IF(c<0, "below
      freezing", c*9/5+32))`.'
  - name: 'Saving the workbook to disk: `wb.save("temperatures.xlsx")`.'
    text: 'Saving the workbook to disk: `wb.save("temperatures.xlsx")`.'
  - name: Adding styling (fonts, borders) via Aspose’s rich formatting API.
    text: Adding styling (fonts, borders) via Aspose’s rich formatting API.
  - name: Initialize a workbook.
    text: Initialize a workbook.
  - name: Write raw data.
    text: Write raw data.
  - name: Apply a MAP‑based formula.
    text: Apply a MAP‑based formula.
  - name: Force calculation.
    text: Force calculation.
  - name: Pull the results back into Python.
    text: Pull the results back into Python.
  type: HowTo
- questions:
  - answer: Just extend the range in the `put_value` call and adjust the list comprehension
      range accordingly. The MAP formula will automatically expand if you reference
      a larger range.
    question: What if I have more than four rows?
  - answer: Absolutely. Replace the lambda body with any arithmetic you need, e.g.,
      `LAMBDA(c, c*2)` for a simple doubling operation.
    question: Can I use MAP with other conversions?
  - answer: The library offers a free evaluation mode, but for production use you’ll
      want a proper license to avoid watermarks.
    question: Do I need a license for Aspose.Cells?
  - answer: No, MAP is part of the dynamic array functions introduced in Excel 365.
      If you target legacy Excel, you’d fall back to traditional copy‑down formulas.
    question: Is the MAP function available in older Excel versions?
  type: FAQPage
tags:
- python
- excel
- aspose-cells
- data conversion
title: Python ile Excel Çalışma Kitabı Oluşturma – Tam Rehber
url: /tr/python/import-and-export/create-excel-workbook-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel Çalışma Kitabı Python – Tam Kılavuz

Hiç **create excel workbook python**‑stilinde Excel’i açmadan bir çalışma kitabı oluşturmayı düşündünüz mü? Belki bir Celsius sıcaklık listesini anında Fahrenheit’e dönüştürmeniz gerekiyor ve formülleri elle kopyala‑yapıştır etmek istemiyorsunuz. Bu öğreticide tam da bunu çözeceğiz: bir Excel dosyası oluşturmayı, bir sütun Celsius verisi eklemeyi ve ardından **MAP fonksiyonu** ve bir **lambda** kullanan tek bir zarif formülle **celsius to fahrenheit** dönüşümünü nasıl yapacağınızı göreceksiniz.

Bu neden önemli? Elektronik tabloları otomatikleştirmek zaman kazandırır, insan hatasını azaltır ve Excel’i daha büyük veri akışlarına entegre etmeyi çok basit hâle getirir. Üstelik Aspose.Cells for Python ile ağır COM etkileşimi olmadan tam Excel yeteneklerine sahip olursunuz. Hazır mısınız? Hadi başlayalım.

## Gereksinimler

- Python 3.9+ (herhangi bir yeni sürüm yeterli)
- `aspose-cells` paketi kurulu (`pip install aspose-cells`)
- Python listeleri ve fonksiyonları hakkında temel bilgi
- Önceden Excel deneyimi gerekmez; çalışma kitabı oluşturmayı sizin yerinize biz halledeceğiz

Bu maddeleri karşıladığınızda hazırsınız demektir. Aksi takdirde, kütüphaneyi kurmak için bir an durun—gerçekten buna değer.

![create excel workbook python example](excel_workbook.png)

*Görsel alt metni: create excel workbook python örneği, doldurulmuş bir elektronik tabloyu gösteriyor*

## Adım 1: Python’da Excel Çalışma Kitabı Oluşturma

İlk yapmamız gereken **create excel workbook python** Aspose.Cells kullanarak bir çalışma kitabı oluşturmaktır. Çalışma kitabını, her bir çalışma sayfasının üzerine yazabileceğiniz yeni bir defter gibi düşünün.

```python
import aspose.cells as cells

# Initialize a new workbook – this is our blank Excel file
wb = cells.Workbook()

# Grab the first worksheet (index 0) to start populating data
ws = wb.worksheets[0]
```

*Neden önemli*: `Workbook()` nesnesi, bir `.xlsx` dosyasının bellek içi temsilini verir. Henüz disk I/O yok, bu da işlemleri hızlı tutar.

## Adım 2: Sütun A’yı Celsius Sıcaklıklarıyla Doldurma

Şimdi bir sayfamız var, **A** sütununa bazı Celsius değerleri ekleyelim. `put_value` metodunu kullanacağız; bu metod bir Python listesini alır ve doğrudan hücre aralığına yazar.

```python
# Write a list of Celsius temperatures into cells A1:A4
ws.cells["A1:A4"].put_value([0, 20, 100, -10])
```

*İpucu*: `"A1:A4"` aralık dizesi esnek—listeyi daha sonra genişletirseniz sadece aralığı ayarlayın ya da dinamik bir adres kullanın.

## Adım 3: Her Celsius Değerini Fahrenheit’e Dönüştürmek İçin MAP ve LAMBDA Uygulama

İşte sihir burada gerçekleşiyor. **MAP fonksiyonu** (Excel 365’te yeni) bir **lambda**yı bir dizi elemanının her birine uygular. Bizim durumumuzda dizi `A1:A4` ve lambda klasik dönüşüm `c * 9/5 + 32` yi gerçekleştirir.

```python
# Set the formula in B1 that maps each Celsius value to Fahrenheit
ws.cells["B1"].formula = "=MAP(A1:A4, LAMBDA(c, c*9/5 + 32))"
```

*Nasıl çalışır*:  
- `MAP(array, LAMBDA(parameter, expression))` `array` üzerinde yineleme yapar.  
- `c` her bir Celsius değeri için yer tutucudur.  
- `c*9/5 + 32` ifadesi Fahrenheit eşdeğerini döndürür.

Eğer **how to use map** in Excel’e yeniyseniz, bunu Python’un yerleşik `map()` fonksiyonuna benzer bir çalışma sayfası formülü olarak düşünün. Formülleri manuel olarak aşağı sürükleme ihtiyacını ortadan kaldırır.

## Adım 4: Formülü Hesaplayarak Sonuçların Gerçekleşmesini Sağlama

Aspose.Cells, formülleri otomatik olarak değerlendirmez; siz söylemelisiniz. `calculate_formula()` çağrısı, MAP sonucunu hesaplatır ve **B** sütunundaki değerleri depolar.

```python
# Force calculation – this writes the computed Fahrenheit values into the cells
wb.calculate_formula()
```

*Köşe durumu*: Daha sonra Celsius sütununu değiştirirseniz, `calculate_formula()` komutunu tekrar çalıştırmanız gerekir ya da çalışma kitabının `calc_mode` özelliğini otomatik yapmalısınız.

## Adım 5: Fahrenheit Değerlerini B Sütunundan Alıp Görüntüleme

Son olarak, hesaplanan sayıları Python’a geri çekelim ve ekrana bastıralım. Bu, **how to use lambda** sonuçlarını programatik olarak nasıl kullanacağınızı gösterir.

```python
# Extract the Fahrenheit values from B1:B4 into a Python list
fahrenheit = [ws.cells[f"B{i}"].value for i in range(1, 5)]
print(fahrenheit)
```

**Beklenen çıktı**

```
[32.0, 68.0, 212.0, 14.0]
```

Bu sayıları görüyorsanız, tebrikler—başarıyla **create excel workbook python**‑stilinde bir dosya oluşturmuş, doldurmuş ve **use map function** ile bir **lambda** kullanarak **convert celsius to fahrenheit** işlemini gerçekleştirmiş oldunuz.

## Yaygın Sorular ve Dikkat Edilmesi Gerekenler

- **Daha fazla satırım olursa ne olur?**  
  `put_value` çağrısındaki aralığı genişletin ve liste kapsamı aralığını ona göre ayarlayın. MAP formülü, daha büyük bir aralığa referans verirseniz otomatik olarak genişleyecektir.

- **MAP’i başka dönüşümler için kullanabilir miyim?**  
  Kesinlikle. Lambda gövdesini ihtiyacınız olan herhangi bir aritmetikle değiştirin, örn. basit bir iki katına çıkarma için `LAMBDA(c, c*2)`.

- **Aspose.Cells için bir lisansa ihtiyacım var mı?**  
  Kütüphane ücretsiz bir değerlendirme modu sunar, ancak üretim ortamında filigranlardan kaçınmak için geçerli bir lisans almanız önerilir.

- **MAP fonksiyonu eski Excel sürümlerinde mevcut mu?**  
  Hayır, MAP, Excel 365’te tanıtılan dinamik dizi fonksiyonlarının bir parçasıdır. Eski Excel sürümlerini hedefliyorsanız geleneksel kopyala‑aşağı formüllerine geri dönmeniz gerekir.

## Örneği Genişletme – Sonraki Adımlar

Temel iş akışı netleştiğine göre şu deneyleri yapabilirsiniz:

1. **How to use map** ile çok‑sütunlu dönüşümler, örn. sıcaklıkları dönüştürüp aynı anda yuvarlama.  
2. **How to use lambda** ile koşullu mantık ekleme: `LAMBDA(c, IF(c<0, "below freezing", c*9/5+32))`.  
3. Çalışma kitabını diske kaydetme: `wb.save("temperatures.xlsx")`.  
4. Aspose’un zengin biçimlendirme API’siyle stil ekleme (yazı tipleri, kenarlıklar).  

Bu adımlar, az önce kurduğumuz temelin üzerine inşa edilir, kodu kısa tutarken güçlü elektronik tablo otomasyonunun kilidini açar.

## Sonuç

Sıfırdan **create excel workbook python** sürecini, Celsius verileriyle doldurmayı ve ardından **MAP fonksiyonu** ve bir **lambda** ifadesiyle **convert celsius to fahrenheit** işlemini nasıl yapacağımızı adım adım gösterdik. Adımlar şunlardı:

1. Bir çalışma kitabı başlatma.  
2. Ham veriyi yazma.  
3. MAP‑tabanlı bir formül uygulama.  
4. Hesaplamayı zorlamak.  
5. Sonuçları Python’a geri çekmek.

Bu tarifle Excel‑merkezli veri akışlarını otomatikleştirmek artık çocuk oyuncağı. Lambda’yı istediğiniz gibi özelleştirebilir, birden fazla MAP çağrısını zincirleyebilir ya da çalışma kitabını bir web hizmetine entegre edebilirsiniz. Hayal gücünüzün sınırı yok.

Farklı bir dönüşüm mü aklınızda? Yorum bırakın, birlikte keşfedelim. Mutlu kodlamalar!

## Bir Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}