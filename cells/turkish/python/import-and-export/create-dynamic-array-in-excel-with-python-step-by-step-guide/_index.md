---
category: general
date: 2026-06-21
description: Python ve Excel'deki SEQUENCE işlevini kullanarak dinamik dizi oluşturun.
  Formül sonucunu okumayı, Excel formüllerini yeniden hesaplamayı öğrenin ve bir Excel
  SEQUENCE örneğine bakın.
draft: false
keywords:
- create dynamic array
- sequence function excel
- read formula result
- recalculate excel formulas
- excel sequence example
language: tr
og_description: Python kullanarak Excel'de dinamik dizi oluşturun. Bu öğreticide SEQUENCE
  işlevinin nasıl kullanılacağını, Excel formüllerinin yeniden nasıl hesaplanacağını
  ve formül sonucunun nasıl okunacağını gösterir.
og_title: Python ile Excel'de Dinamik Dizi Oluşturma – Tam Rehber
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create dynamic array using Python and the SEQUENCE function in Excel.
    Learn to read formula result, recalculate Excel formulas, and see an Excel SEQUENCE
    example.
  headline: Create Dynamic Array in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
tags:
- excel
- python
- xlwings
- dynamic arrays
title: Python ile Excel'de Dinamik Dizi Oluşturma – Adım Adım Kılavuz
url: /tr/python/import-and-export/create-dynamic-array-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python ile Excel’de Dinamik Dizi Oluşturma – Tam Kılavuz

Python betiğinizden çıkmadan Excel’de **dinamik dizi** formüllerini nasıl **oluşturacağınızı** hiç merak ettiniz mi? Tek başınıza değilsiniz. Aylık bir raporu otomatikleştiriyor ya da hafif bir veri motoru inşa ediyor olun, bir `SEQUENCE` formülünü bir çalışma kitabına ekleyebilmek, yeniden hesaplamak ve dökülen aralığı (spill range) Python’a geri çekebilmek büyük bir fark yaratıyor.

Bu öğreticide gerçek bir **excel sequence örneği** üzerinden ilerleyecek, **formül sonucunu okuma** yöntemini gösterecek ve yeni mantık enjekte ettikten sonra **excel formüllerini yeniden hesaplamanın** en iyi yolunu açıklayacağız. Sonunda, kopyalayıp yapıştırabileceğiniz, çalıştırabileceğiniz ve ihtiyaçlarınıza göre uyarlayabileceğiniz bağımsız bir betiğe sahip olacaksınız.

## Öğrenecekleriniz

- `SEQUENCE` fonksiyonunun nasıl çalıştığını ve matris üretmek için neden mükemmel olduğunu.
- Normal bir hücre değeri ile bir spill range adresi arasındaki fark.
- `wb.calculate_formula()` (veya eşdeğeri) kullanarak Excel’in yeni formülleri değerlendirmesini sağlama.
- `ANCHORARRAY` ile dinamik bir dizinin adresini çıkarma.
- Herhangi bir projeye ekleyebileceğiniz tam, çalıştırılabilir bir Python örneği.

Excel’in yeni dinamik‑dizi motorunda önceden deneyim gerekmez—sadece Python’a ve Excel ile iletişim kurabilen **xlwings** gibi bir kütüphaneye temel bir aşinalık yeterlidir.

---

## Python Kullanarak Excel’de SEQUENCE ile Dinamik Dizi Oluşturma

İlk adım, bir çalışma sayfası hücresine doğrudan **dinamik dizi** formülü yazmaktır. Modern Excel’de `SEQUENCE` fonksiyonu, sayıları anında bir matris olarak üretebilir. Kullanacağımız sözdizimi şu şekildedir:

```python
# Step 1: Write a dynamic array formula that generates a 3×2 matrix starting at 10 with step 5
ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"   # Returns a 3×2 array
```

**Neden `SEQUENCE`?**  
Bunu, Excel’in yerleşik `range()` fonksiyonu gibi düşünün. Tek bir satırda satır sayısı, sütun sayısı, başlangıç değeri ve artış değerini belirlemenizi sağlar. Bizim örneğimizde 3 satır ve 2 sütun istiyoruz, 10’dan başlayıp 5’er adım artıyor; sonuç şu şekildedir:

|   | A | B |
|---|---|---|
|1|10|15|
|2|20|25|
|3|30|35|

Formül `A1` hücresinde bulunduğu için Excel otomatik olarak sonucu komşu hücrelere `A1:B3` aralığına “spill” eder. Bu spill, daha sonra alacağımız veridir.

---

## Excel’de SEQUENCE Fonksiyonunu Kullanma – Hızlı Bir Excel Sequence Örneği

Excel’i manuel olarak açıp bir hücreye `=SEQUENCE(3,2,10,5)` yazarsanız aynı matrisi anında görürsünüz. Bu fonksiyon, Office 365’te tanıtılan Excel’in **dinamik dizi** motorunun bir parçasıdır, bu da şunu ifade eder:

- Ctrl+Shift+Enter gerekmez.
- Sonuç otomatik olarak genişleyebilir veya daralabilir.
- `@` veya `#` gibi fonksiyonlarla tüm spill range’e referans verebilirsiniz.

Python’da tek fark, formülü bir dize olarak hücrenin `.formula` özelliğine atamamızdır. Kütüphane geri kalanını halleder.

---

## ANCHORARRAY ile Spill Range Adresini Almak

Dinamik dizi yerleştirildikten sonra, Excel’in değerleri tam olarak nerede konumlandırdığını bilmek çoğu zaman gerekir. İşte `ANCHORARRAY` devreye girer. Spill range’in sol‑üst hücresinin adresini döndürür—betiğimize geri okumak için tam olarak ihtiyacımız olan şey.

```python
# Step 2: Retrieve the address of the spill range produced by the formula in A1
ws.cells["C1"].formula = "=ANCHORARRAY(A1)"      # Returns the address of the spill range
```

Bu formülü `C1` hücresine yerleştirdiğimizde `"A1:B3"` gibi bir metin dizesi elde ederiz. **Formül sonucunu** başka bir formül olarak değil, düz bir değer olarak okuduğumuza dikkat edin. Bu küçük hile, çalışma sayfasını manuel olarak ayrıştırma ihtiyacını ortadan kaldırır.

---

## Excel Formüllerini Yeniden Hesaplama ve Sonucu Okuma

Yeni bir formül dış bir betikten enjekte edildiğinde Excel her zaman anında yeniden hesaplamaz. Çalışma kitabının en son değişiklikleri yansıtmasını garanti etmek için açıkça bir hesaplama turu başlatırız.

```python
# Step 3: Recalculate all formulas in the workbook and read the result
wb.calculate_formula()               # Forces Excel to evaluate pending formulas
print(ws.cells["C1"].value)          # → "A1:B3"
```

**Neden `calculate_formula()` çağırıyoruz?**  
Bu adımı atlayarsanız, `ws.cells["C1"].value` hâlâ `None` ya da eski bir adres döndürebilir; çünkü Excel hâlâ bağımlılık ağacını güncelliyor olabilir. Yeniden hesaplamayı zorlayarak **formül sonucunun** güncel olmasını sağlarız.

---

## Tam Betik – Baştan Sona

Aşağıda, her şeyi bir araya getiren eksiksiz, çalıştırılabilir bir örnek bulunuyor. **xlwings**’in kurulu olduğunu (`pip install xlwings`) ve Excel’in makinenizde erişilebilir olduğunu varsayar.

```python
import xlwings as xw

def create_dynamic_array_example():
    # Open a new workbook (or attach to an existing one)
    wb = xw.Book()               # Creates a fresh Excel workbook
    ws = wb.sheets[0]            # Grab the first worksheet

    # 1️⃣ Write the SEQUENCE formula – this creates a 3×2 matrix starting at 10, step 5
    ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"

    # 2️⃣ Use ANCHORARRAY to capture the spill range address in C1
    ws.cells["C1"].formula = "=ANCHORARRAY(A1)"

    # 3️⃣ Force Excel to recalculate so that the ANCHORARRAY result is current
    wb.calculate_formula()

    # 4️⃣ Read back the address – this is our **read formula result** step
    spill_address = ws.cells["C1"].value
    print(f"The dynamic array spills into: {spill_address}")

    # 5️⃣ Optionally, fetch the actual values from the spill range
    # xlwings can read a range by address, so we demonstrate that too
    data = ws.range(spill_address).value
    print("Matrix values:")
    for row in data:
        print(row)

    # Clean up – close without saving to keep the demo tidy
    wb.close(save=False)

if __name__ == "__main__":
    create_dynamic_array_example()
```

### Beklenen Çıktı

```
The dynamic array spills into: A1:B3
Matrix values:
[10, 15]
[20, 25]
[30, 35]
```

Betik çalıştırıldığında Excel açılır, `SEQUENCE` formülü enjekte edilir, yeniden hesaplanır ve ardından spill adresi ile matris aynı anda yazdırılır. Manuel tıklama gerekmez.

---

## Yaygın Tuzaklar ve Pro İpuçları

- **Tuzak:** `wb.calculate_formula()` unutulması.  
  *Sonuç:* `C1` boş kalır ya da eski bir adres gösterir.  
  *Çözüm:* Yeni formüller yazdıktan sonra her zaman bir hesaplama tetikleyin.

- **Tuzak:** `SEQUENCE` fonksiyonunu desteklemeyen eski bir Excel sürümü kullanmak.  
  *Sonuç:* `#NAME?` hatası.  
  *Çözüm:* Office 365 ya da Excel 2021+ sürümüne sahip olduğunuzdan emin olun.

- **Pro ipucu:** Spill range’i daha ileri işleme (ör. grafik oluşturma) için ihtiyaç duyuyorsanız, yukarıda gösterildiği gibi adresi doğrudan `ws.range(spill_address)` içine besleyebilirsiniz.

- **Pro ipucu:** `ANCHORARRAY` sadece `SEQUENCE` için değil, herhangi bir dinamik diziyle çalışır. `=SORT(A2:A10)` ya da `=FILTER(...)` gibi bir formül koyarsanız yine doğru spill adresini alırsınız.

- **Köşe durum:** Hedef alan zaten doluysa, Excel `#SPILL!` hatası verir. Bu durumda ya hedef aralığı önce temizleyin ya da formülü farklı bir hücreye taşıyın.

---

## Örneği Genişletmek – Sonraki Adım Ne?

Artık **dinamik dizi** formüllerini **oluşturmayı**, **formül sonucunu okumayı** ve **excel formüllerini yeniden hesaplamayı** bildiğinize göre daha ileri senaryolar keşfedebilirsiniz:

- **Dinamik grafik verileri** – spill range’i bir grafik kaynağına besleyin ve grafiğin otomatik olarak büyümesini sağlayın.
- **Koşullu biçimlendirme** – spill range’in adresini kullanarak kurallar uygulayın.
- **Çapraz‑çalışma kitabı referansları** – bir çalışma kitabında dinamik dizi yazın ve `xlwings` bağlantılarıyla veriyi başka bir kitaba çekin.

Bu seçeneklerin her biri burada ele alınan temel kavramlar üzerine inşa edilmiştir; deney yapmaktan çekinmeyin. Tek sınırlama hayal gücünüzdür (ve belki Excel’in maksimum satır/sütun sayısı).

---

## Sonuç

Python’dan Excel’de **dinamik dizi** formülleri **oluşturma**, **SEQUENCE fonksiyonunu** kullanma, **ANCHORARRAY** ile spill range’i alma, **excel formüllerini yeniden hesaplama** ve sonunda **formül sonucunu** betiğinize geri okuma sürecini adım adım gösterdik. Kısa örnek, **xlwings** gibi otomasyon araçlarıyla birleştirildiğinde Excel’in yeni dinamik‑dizi motorunun ne kadar güçlü olabileceğini ortaya koyuyor.

Kendi projelerinizde deneyin, matris boyutlarını değiştirin ya da `SEQUENCE` yerine başka bir dinamik fonksiyon koyun. Ne kadar rahatladıkça, Excel otomasyonunun sadece mümkün olmakla kalmayıp aynı zamanda keyifli bir şekilde basit olduğunu göreceksiniz.

Sorularınız mı var ya da bu deseni nasıl genişlettiğinizi paylaşmak mı istiyorsunuz? Aşağıya bir yorum bırakın, kodlamanın tadını çıkarın!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Processing Data Using Array Function in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)
- [Create Dynamic Line Charts in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Create Dynamic Excel Charts with Aspose.Cells Java&#58; A Comprehensive Guide for Developers](/cells/english/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}