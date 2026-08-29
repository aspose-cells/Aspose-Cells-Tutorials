---
date: '2026-08-16'
description: Aspose.Cells kullanarak Java'da küreselleştirme eklemeyi, Excel hata
  mesajlarını özelleştirmeyi ve Maven bağımlılığını kurmayı öğrenin.
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: Aspose.Cells kullanarak Java'da küreselleştirme eklemeyi, Excel hata
  mesajlarını özelleştirmeyi ve Maven bağımlılığını kurmayı öğrenin. Adım adım kılavuzu
  izleyin.
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: Java'da Aspose.Cells ile küreselleştirme nasıl eklenir
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: Java'da Aspose.Cells ile küreselleştirme nasıl eklenir
url: /tr/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Java ile Aspose.Cells'te globalleşme nasıl eklenir

## Giriş

Java çalışma kitabınıza globalleşme eklemek, hata mesajlarını, boolean değerlerini ve diğer yerel‑özel dizeleri kullanıcılarınızın beklediği dilde sunmanızı sağlar. Bu öğreticide **globalleşmenin nasıl ekleneceğini** Rusça için öğreneceksiniz, ancak aynı desen herhangi bir dil için çalışır. Kılavuzun sonunda şunları yapabilecek duruma geleceksiniz:

- Varsayılan hata metnini ve boolean temsillerini geçersiz kılmak.
- Özel ayarlarınızı herhangi bir `Workbook` örneğine uygulamak.
- Çözümü tipik bir Maven‑tabanlı Java projesine entegre etmek.

Excel dosyalarınızı gerçekten çok dilli hâle getirmeye hazır mısınız? Öncelikle geliştirme ortamınızın gereksinimleri karşıladığını doğrulayalım.

## Hızlı cevaplar
- **Aspose.Cells'te globalleşme nedir?** Yerel‑duyarlı dizelerin (hatalar, boolean değerler vb.) bir kümesidir ve bunları özel metinle değiştirebilirsiniz.  
- **Hangi Maven artefaktı gereklidir?** `com.aspose:aspose-cells:25.3`.  
- **Rusça dışındaki dilleri hedefleyebilir miyim?** Evet – `GlobalizationSettings` sınıfını genişletip her yerel için gerekli yöntemleri geçersiz kılabilirsiniz.  
- **Geliştirme için lisansa ihtiyacım var mı?** Test için ücretsiz deneme sürümü yeterlidir; kalıcı bir lisans değerlendirme filigranlarını kaldırır.  
- **Çözüm iş parçacığı‑güvenli mi?** Ayarları çalışma kitabı başına uygulayın; `GlobalizationSettings` nesnesi oluşturulduktan sonra değiştirilemez.

## Aspose.Cells'te globalleşme nedir?

`GlobalizationSettings`, Aspose.Cells'in hata mesajları, boolean değerleri, para birimi simgeleri ve tarih desenleri gibi yerel‑özel dizeleri kontrol eden yapılandırma nesnesidir. Kendi alt sınıfınızı sağlayarak kütüphaneye her kültür için hangi metnin gösterileceğini söylersiniz; böylece varsayılan İngilizce dizeleri, son kullanıcıların dili ve bölgesel geleneklerine uygun çevirilerle değiştirebilirsiniz.

## Özel globalleşme neden eklenir?

Aspose.Cells **50+ giriş ve çıkış formatını** destekler – XLSX, CSV, PDF ve ODS dahil – ve **200 000 satıra** kadar çalışma kitabını tüm dosyayı belleğe yüklemeden işleyebilir. Globalleşmeyi özelleştirmek, son kullanıcıların mesajları kendi ana dillerinde görmesini sağlar ve çok uluslu dağıtımlarda destek taleplerini yaklaşık **%30** azaltır.

## Önkoşullar

- **Java Development Kit** 8 veya üzeri.
- **IDE** (IntelliJ IDEA veya Eclipse gibi).
- **Aspose.Cells for Java** sürüm 25.3 (veya daha yeni) Maven veya Gradle aracılığıyla eklenmiş.

### Aspose.Cells for Java'ı kurma

`pom.xml` dosyanıza Maven bağımlılığını ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Veya Gradle tercih ediyorsanız, `build.gradle` dosyasına aşağıdakileri ekleyin:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Lisans edinme

Aspose çeşitli lisans seçenekleri sunar:

- **Ücretsiz deneme** – 30 gün tam özellikli değerlendirme.  
- **Geçici lisans** – filigransız sınırsız değerlendirme.  
- **Ticari lisans** – üretim ortamı için, öncelikli destek ile.

Bir lisans dosyası edindikten sonra, uygulama başlangıcında bir kez ayarlayın:

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## Rusça için globalleşme nasıl eklenir?

`Workbook` nesnesi, belleğe yüklenmiş bir Excel dosyasını temsil eder ve sayfalara, hücrelere ve ayarlara erişim sağlar. Çalışma kitabınızı yükleyin, `GlobalizationSettings` sınıfının bir alt sınıfını oluşturun ve bunu çalışma kitabına ekleyin. Doğrudan cevap: **özel bir `GlobalizationSettings` sınıfı örnekleyin, `getErrorValueString` ve `getBooleanValueString` yöntemlerini geçersiz kılın, ardından `workbook.setGlobalizationSettings(customSettings)` çağrısını yapın**. Bu iki adımlı yaklaşım, varsayılan Rusça dizeleri kendi metinlerinizle değiştirir.

### Özel ayarların tanımlanması

Bu kılavuzda ilk kez `GlobalizationSettings` referansını gördüğünüzde, tanımını not edin:

`GlobalizationSettings`, Aspose.Cells'in yerel‑özel dizeleri almak için kullandığı temel sınıftır.  

Şimdi Rusça‑özel metin döndüren bir alt sınıf oluşturun:

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### Ayarları bir çalışma kitabına uygulama

Alt sınıfı tanımladıktan sonra, herhangi bir `Workbook` örneğine ekleyin:

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## Pratik uygulamalar

- **Finansal raporlama** – muhasebecinin ana dilinde hata kodlarını göstererek yanlış yorumlamayı azaltır.  
- **Kurumsal araçlar** – onlarca iç Excel‑tabanlı yardımcı programda aynı globalleşme mantığını gömün.  
- **Otomatik veri boru hatları** – aşağı akış sistemlerinin ekstra çeviri adımları olmadan yerel‑duyarlı değerler almasını sağlayın.

## Performans değerlendirmeleri

Özel globalleşmeyi etkinleştirdiğinizde, Aspose.Cells formülleri ve I/O işlemlerini aynı yüksek performansla işler. Bellek kullanımını düşük tutmak için:

- Kaydetme sonrası çalışma kitabı referanslarını serbest bırakın (`wb.dispose()`).  
- `CalculationOptions.setEnableIterativeCalculation(true)` yalnızca gerektiğinde kullanın.  
- 100 MB'den büyük çalışma kitapları için JVM yığın ayarını (`-Xmx2g`) ayarlayın.

## Sıkça sorulan sorular

**Q: Aynı globalleşme ayarlarını birden fazla çalışma kitabına aynı anda uygulayabilir miyim?**  
A: Evet. Tek bir `RussianGlobalization` örneği oluşturup, her çalışma kitabına `setGlobalizationSettings` ile geçirebilirsiniz.

**Q: Sağ‑to‑sol (RTL) betik kullanan bir dili desteklemem gerekirse ne yapmalıyım?**  
A: Alt sınıfınızda `getCurrencySymbol` ve `getDatePattern` gibi ek yöntemleri geçersiz kılarak uygun RTL sembollerini döndürün.

**Q: Deneme sürümünde özel globalleşme kullanmak için lisans gerekli mi?**  
A: Hayır. Deneme sürümü `GlobalizationSettings`i tam olarak destekler; yalnızca belirli çıktı formatlarında değerlendirme filigranları görünür.

**Q: Hatalı hata dizelerini nasıl debug edebilirim?**  
A: Geçersiz kıldığınız yöntemlerde `System.out.println` ekleyerek gelen `err` değerinin switch durumlarıyla eşleştiğini doğrulayın.

**Q: Bu, formül hesaplama hızını etkiler mi?**  
A: İhmal edilebilir. Kütüphane dizeyi yalnızca hücre değerleri render edilirken arar, ara hesaplama adımlarında değil.

## Ek kaynaklar

- **Dokümantasyon**: Ayrıntılı kılavuzları inceleyin [Aspose.Cells Dokümantasyonu](https://reference.aspose.com/cells/java/)  
- **İndirme**: En son sürümleri alın [Aspose İndirmeleri](https://releases.aspose.com/cells/java/)  
- **Satın Alma**: Ticari kullanım için lisans satın alın [Aspose Satın Alma](https://purchase.aspose.com/buy)  
- **Ücretsiz deneme**: Ücretsiz deneme sürümüyle başlayın [Aspose Ücretsiz Deneme](https://releases.aspose.com/cells/java/)  
- **Geçici lisans**: Geçici lisans edinin [Aspose Geçici Lisans](https://purchase.aspose.com/temporary-license/)  
- **Destek**: Topluluktan yardım alın [Aspose Destek Forumu](https://forum.aspose.com/c/cells/9)

---

**Son Güncelleme:** 2026-08-16  
**Test Edilen Sürüm:** Aspose.Cells 25.3 for Java  
**Yazar:** Aspose

## İlgili Eğitimler

- [Aspose.Cells Java: Özel Hesaplama Motoru Kılavuzu](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [Aspose Cells Kullanımı – Java için Excel Motoru Eğitimleri](/cells/java/calculation-engine/)
- [Aspose Cells Maven Bağımlılığı – Java'da Aspose.Cells ile Excel Veri Bağlantılarını Yönetme](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}