---
category: general
date: 2026-08-04
description: Java ile bir Excel çalışma kitabı oluşturun ve Japon era tarihlerini
  ayrıştırın, ardından Aspose.Cells for Java kullanarak çalışma kitabını xlsx olarak
  kaydedin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- java excel date conversion
- Aspose.Cells Java
- japanese era date parsing
language: tr
lastmod: 2026-08-04
og_description: Java ile bir Excel çalışma kitabı oluşturun, Japon era tarihlerini
  otomatik olarak Gregoryen takvimine dönüştürün ve ardından çalışma kitabını Aspose.Cells
  ile xlsx olarak kaydedin.
og_image_alt: Java code creating an Excel workbook and converting a Japanese era date
  to Gregorian
og_title: Java ile Excel çalışma kitabı oluşturma – Japon tarih dönüşüm rehberi
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create excel workbook java and parse Japanese era dates, then save
    workbook as xlsx using Aspose.Cells for Java.
  headline: 'Create excel workbook java: handle Japanese era dates'
  type: TechArticle
tags:
- java
- excel
- Aspose.Cells
- date conversion
- xlsx
title: 'Excel çalışma kitabı oluşturma Java: Japon era tarihlerini işleme'
url: /tr/java/workbook-operations/create-excel-workbook-java-handle-japanese-era-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel çalışma kitabı oluşturma java: Japon era tarihlerini işleme

Eğer **create excel workbook java** yapmanız ve Japon era tarihleriyle çalışmanız gerekiyorsa, bu öğretici size tam olarak nasıl yapılacağını gösterir. “R3/05/01” gibi bir tarihi girmeyi, Aspose.Cells'in bunu Gregorian tarih olarak yorumlamasını ve ardından **save workbook as xlsx** öğreneceksiniz.

Era‑tabanlı takvimlerle çalışmak kafa karıştırıcı olabilir, özellikle varsayılan Excel ayrıştırıcısı standart Gregorian formatını beklediğinde. Japon era ayrıştırmasını etkinleştirerek manuel dize manipülasyonundan kaçınır ve kütüphanenin dönüşümü sizin için yapmasını sağlarsınız. Bu kılavuz ayrıca dosyayı bir `.xlsx` dosyası olarak kalıcı hale getirme adımını da kapsar.

## Önkoşullar

* Java 17 ve üzeri yüklü.
* Maven 3.6+ (veya Gradle) bağımlılıkları yönetmek için.
* IntelliJ IDEA veya Eclipse gibi bir IDE.
* Aspose.Cells for Java kütüphanesi (örnek sürüm 23.10 kullanıyor, ancak herhangi bir yeni sürüm çalışır).

## Adım 1: Aspose.Cells'i projenize ekleyin

Kütüphane, bu öğreticide kullanılan `Workbook`, `Worksheet` ve `WorkbookSettings` sınıflarını sağlar.

**Maven**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

**Gradle**

```gradle
implementation 'com.aspose:aspose-cells:23.10:jdk17'
```

> **Pro ipucu:** Kod yazarken satır içi belgeler elde etmek için `javadoc` JAR'ını kullanın.

## Adım 2: Çalışma kitabını oluşturun ve ilk çalışma sayfasına erişin

Şimdi yeni bir workbook nesnesi oluşturuyor ve varsayılan ilk sayfayı alıyoruz.

```java
import com.aspose.cells.*;

public class JapaneseEraExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                // create an empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet (index 0)
```

*Neden bu adım önemlidir:* `Workbook`, tüm Excel dosyasını temsil ederken, `Worksheet` hücreleri yerleştirdiğiniz tuvaldir. Temiz bir workbook ile başlamak, tarih ayrıştırmasını etkileyebilecek gizli biçimlendirmelerin olmamasını sağlar.

## Adım 3: Bir hücreye Japon era tarihi girin

Japon era tarihleri “<EraLetter><Year>/<Month>/<Day>” desenini izler. Bu örnekte “R3” (Reiwa 3 = 2021) kullanıyoruz.

```java
        // Step 3: Put a Japanese era date into cell A1
        Cell dateCell = worksheet.getCells().get("A1");
        dateCell.putValue("R3/05/01");   // Reiwa 3, May 1st
```

*Neden bu adım önemlidir:* Era dizesini doğrudan yazarak, dönüşümü daha sonra Aspose.Cells'in yapmasına izin verirsiniz. “R3”ü “2021”e kendiniz çevirmeniz gerekmez.

## Adım 4: Japon era ayrıştırmasını etkinleştirin ve formülleri yeniden hesaplayın

Workbook'e era dizelerini tarih olarak ele almasını söyleyin. Ayarı değiştirdikten sonra, `calculateFormula()` metodunu çağırın, böylece bağımlı formüller (daha sonra eklerseniz) doğru Gregorian değerini görür.

```java
        // Step 4: Turn on Japanese era parsing
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEra(true);   // enable era conversion
        workbook.calculateFormula();        // refresh any formulas
```

*Neden bu adım önemlidir:* `setUseJapaneseEra(true)` bayrağı, Aspose.Cells'in “R3/05/01” gibi dizeleri Gregorian tarihler olarak yorumlamasını sağlar. Bu bayrak olmadan, hücre metni olduğu gibi tutar ve sonraki hesaplamaları bozar.

## Adım 5: Dönüşümü doğrulayın ve **save workbook as xlsx**

Dönüştürülen değeri konsola yazdırın ve workbook'u kaydedin.

```java
        // Step 5: Verify conversion and save the file
        System.out.println("Converted date: " + dateCell.getStringValue()); // → 2021-05-01
        workbook.save("JapaneseEra.xlsx");   // saves as .xlsx by default
    }
}
```

**Expected console output**

```
Converted date: 2021-05-01
```

`JapaneseEra.xlsx` dosyası artık hücre A1'de `2021‑05‑01` Gregorian tarihini içeriyor, kaynak dize Japon era formatını kullansa da.

## Adım 6: Yaygın varyasyonlar ve uç‑durum yönetimi

| Senaryo | Kodu nasıl uyarlamalısınız |
|----------|-----------------------------|
| Farklı era (ör. Heisei) | Heisei 30 = 2018‑12‑31 için “H30/12/31” kullanın. Aynı `setUseJapaneseEra(true)` bayrağı tüm desteklenen era'lar için çalışır. |
| Boş veya hatalı biçimlendirilmiş dize | `putValue`'yi try‑catch bloğuna sarın ve `^[RHS][0-9]+/[0-9]{2}/[0-9]{2}$` gibi bir regex ile doğrulayın. |
| Denetim için orijinal era dizesini tutmanız gerekiyorsa | Dönüştürmeden önce ham dizeyi gizli bir sütunda saklayın, ardından final workbook'ta o sütunu gizleyin. |
| Büyük veri setleri | Birçok satır era tarihleri kullandığında formül yeniden hesaplamasını hızlandırmak için `WorkbookSettings.setEnableThreadedCalculation(true)`'ı etkinleştirin. |

> **Dikkat edin:** Japon era desteği öncesi (2020 öncesi) bir Aspose.Cells sürümü kullanmak, `setUseJapaneseEra` bayrağını görmezden gelecek ve hücre değişmeden kalacaktır.

## Adım 7: Örneği çalıştırın

Sınıfı IDE'nizden veya komut satırından derleyip çalıştırın:

```bash
javac -cp "path/to/aspose-cells-23.10.jar" JapaneseEraExample.java
java -cp ".:path/to/aspose-cells-23.10.jar" JapaneseEraExample
```

Çalıştırmadan sonra, Excel'de `JapaneseEra.xlsx` dosyasını açın. Hücre A1 `2021-05-01` gösterir ve **java excel date conversion** işleminin başarılı olduğunu doğrular.

## Sonuç

Artık **create excel workbook java** yapmayı, Japon era tarihini girmeyi, otomatik era ayrıştırmasını etkinleştirmeyi ve **save workbook as xlsx** yapmayı biliyorsunuz. Bu yaklaşım manuel tarih hesaplamalarını ortadan kaldırır ve Excel dosyalarınızın standart Gregorian takvimlerle uyumlu kalmasını sağlar.

### Sonraki keşifler

* **Formatting dates** – hücre stilleri (`Style style = workbook.createStyle(); style.setNumber(14);`) uygulayarak tarihleri tercih ettiğiniz yerelde gösterin.
* **Bulk conversion** – era dizesi içeren bir sütunu döngüyle gezerek her hücreyi dönüştürün.
* **Export to other formats** – Aspose.Cells ayrıca PDF, CSV ve ODS formatlarını da destekler; sadece `workbook.save(...)` içinde dosya uzantısını değiştirin.

Diğer era'ları, özel formatları denemekten veya bu tekniği formül‑tabanlı raporlarla birleştirmekten çekinmeyin. İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells for Java kullanarak Excel Çalışma Kitabını SVG olarak Oluşturma ve Kaydetme](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Excel Çalışma Kitabını Oluştur ve Kaydet Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Excel Çalışma Kitabını Oluştur ve Kaydet Aspose Cells Java](/cells/french/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}