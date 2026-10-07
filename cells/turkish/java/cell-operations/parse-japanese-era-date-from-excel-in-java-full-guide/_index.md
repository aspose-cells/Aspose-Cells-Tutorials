---
category: general
date: 2026-06-18
description: Aspose.Cells kullanarak Java'da Japon dönemi tarihini ayrıştırın. Excel
  hücresinden tarihi nasıl okuyacağınızı ve Excel hücresinden tarih‑zamanı hızlıca
  nasıl çıkaracağınızı öğrenin.
draft: false
keywords:
- parse japanese era date
- read date from excel cell
- extract datetime from excel cell
language: tr
og_description: Aspose.Cells ile Java’da Japon dönemi tarihini ayrıştırın. Bu kılavuz,
  Excel hücresinden tarihi nasıl okuyacağınızı ve sadece birkaç adımda Excel hücresinden
  tarih‑saat bilgisini nasıl çıkaracağınızı gösterir.
og_title: Excel'den Japon Dönemi Tarihini Java'da Ayrıştırma – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  headline: Parse Japanese Era Date from Excel in Java – Full Guide
  type: TechArticle
- description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  name: Parse Japanese Era Date from Excel in Java – Full Guide
  steps:
  - name: Multiple Eras
    text: Japan has had several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). The `setParseDateUsingJapaneseEra(true)`
      flag covers all of them automatically, but be aware that older dates may fall
      outside the library’s supported range (typically 1868‑present). If you encounter
      a date like “昭和45年12月31日”, the sam
  - name: Blank or Invalid Cells
    text: 'If a cell is empty or contains a malformed string, `cell.getDateTime()`
      throws a `CellsException`. Guard against this with a simple check:'
  - name: Time Component
    text: The example only includes a date, but if your Excel file also stores time
      (e.g., “令和3年5月10日 14:30”), Aspose.Cells will preserve the time portion. The
      `LocalDateTime` you receive will include hours, minutes, and seconds.
  type: HowTo
tags:
- Java
- Excel
- DateTime
title: Java’da Excel’den Japon Dönemi Tarihini Ayrıştırma – Tam Rehber
url: /tr/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Japon Dönemi Tarihini Java ile Ayrıştırma – Tam Kılavuz

Bir Excel çalışma kitabında **Japon dönemi tarihini** ayrıştırmanız gerektiğinde, bunu normal bir Gregoryen `DateTime`'a nasıl dönüştüreceğinizi bilemediğiniz oldu mu? Yalnız değilsiniz—çok sayıda geliştirici, eski Japon muhasebe tabloları veya devlet formlarıyla çalışırken bu soruna takılıyor. İyi haber şu ki, birkaç satır Java kodu ve doğru kütüphane ile Excel hücresinden tarihi okuyabilir ve Excel hücresinden datetime çıkarabilirsiniz, manuel string işlemlerine gerek kalmadan.

Bu öğreticide, “令和3年5月10日” gibi **Japon dönemi tarih** dizelerini Java `java.time.LocalDateTime`'a nasıl **parse** edeceğinizi gösteren tam, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Gerekli Maven bağımlılığını açıklayacağız, neden era‑aware parsing (dönem‑duyarlı ayrıştırma) etkinleştirmeniz gerektiğini anlatacağız ve karşılaşabileceğiniz yaygın tuzakları göstereceğiz. Sonunda, herhangi bir Java projesine ekleyebileceğiniz sağlam, üretim‑hazır bir kod parçacığına sahip olacaksınız.

## Ön Koşullar

- Java 17 veya daha yeni (kod Java 8+ üzerinde de çalışır)
- Maven veya Gradle yapı sistemi
- Excel dosyaları hakkında temel bilgi
- **Aspose.Cells for Java** kütüphanesi (test için ücretsiz deneme sürümü yeterli)

Bu kavramlar size yabancı geliyorsa endişelenmeyin—kütüphaneyi nasıl ekleyeceğinizi ve nasıl başlayacağınızı adım adım göstereceğim.

## Adım 1: Aspose.Cells'i Projeye Ekleyin

İlk iş, Japon dönemi tarihlerini anlayan kütüphaneyi eklemek. Aspose.Cells bu işi sizin için yapar.

**Maven**:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for latest version -->
</dependency>
```

**Gradle**:

```groovy
implementation 'com.aspose:aspose-cells:24.9'
```

Bağımlılık çözüldükten sonra, *Excel hücresinden tarihi okuyabilir* ve *Excel hücresinden datetime çıkarabilirsiniz*.

## Adım 2: Bir Workbook Oluşturun ve İlk Worksheet'i Hedefleyin

Bellekte yeni bir workbook oluşturacağız ve ilk sayfayı alacağız. Bu, orijinal örneğin ilk iki satırını taklit eder.

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

Neden temiz bir workbook ile başlıyoruz? Her ayarı kontrol edebileceğimiz temiz bir ortam sağlar—era‑aware parsing (dönem‑duyarlı ayrıştırma) etkinleştirildiğinde kritik bir adımdır.

## Adım 3: A1 Hücresine Japon Dönemi Tarihi Dizesi Yerleştirin

Şimdi, içinde zaten bir Japon dönemi tarihi bulunan bir Excel dosyasını taklit ediyoruz. Gerçek hayatta muhtemelen mevcut bir `.xlsx` dosyasını yüklersiniz, ancak örnek olması açısından değeri **kendimiz** yazacağız.

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

Dize, standart Japon notasyonunu izler: *Era* + *Year* + *Month* + *Day*. Ek bir yapılandırma olmadan Aspose.Cells bunu bir tarih yerine düz metin olarak görür.

## Adım 4: Era‑Aware (Dönem‑Duyarlı) Tarih Ayrıştırmayı Etkinleştirin

İşte kritik kısım: workbook'a **Japon dönemi tarih** dizelerini gördüğünde ayrıştırmasını söyleyin. Bu, `ParseDateUsingJapaneseEra` bayrağıyla yapılır.

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

Neden gerekli? Varsayılan olarak Aspose.Cells Gregoryen takvimi varsayar, bu yüzden “令和3年5月10日” bir dize olarak kalır. Bayrağı etkinleştirmek, motorun bunu arka planda bir `java.util.Date` (veya `java.time` eşdeğeri) olarak dönüştürmesini sağlar.

## Adım 5: Ayrıştırılmış DateTime Değerini Alın

Workbook artık dönemi yorumlayabildiğine göre, hücreden `DateTime` temsilini isteyebiliriz.

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

`cell.getDateTime()` kullanarak **Excel hücresinden tarihi okuduğumuza** dikkat edin. Metod bir `java.util.Date` döndürür; biz bunu daha güvenli tip için hemen `LocalDateTime`'a çeviririz. Bu, **Excel hücresinden datetime çıkarma** gereksinimini temiz ve idiomatik bir şekilde karşılar.

## Adım 6: Sonucu Doğrulayın

Son olarak, dönüştürmenin başarılı olduğunu teyit etmek için Gregorian tarihi yazdıralım.

```java
        // Step 6: Output the Gregorian date
        System.out.println(dateTime); // Expected output: 2021-05-10T00:00
    }
}
```

Programı çalıştırdığınızda şu çıktıyı görmelisiniz:

```
2021-05-10T00:00
```

Bu çıktı, tek bir akışta **Japon dönemi tarihini parse** ettiğimizi, **Excel hücresinden tarihi okuduğumuzu** ve **Excel hücresinden datetime çıkardığımızı** kanıtlar.

## Gerçek Dünya Kenar Durumlarıyla Baş Etme

### Birden Çok Dönem

Japonya’nın birçok dönemi vardır (Meiji, Taishō, Shōwa, Heisei, Reiwa). `setParseDateUsingJapaneseEra(true)` bayrağı hepsini otomatik olarak kapsar, ancak daha eski tarihler kütüphanenin desteklediği aralığın dışına çıkabilir (genellikle 1868‑günümüz). “昭和45年12月31日” gibi bir tarihle karşılaşırsanız aynı kod 1970‑12‑31 tarihine dönüştürür.

### Boş veya Geçersiz Hücreler

Bir hücre boşsa ya da hatalı bir dize içeriyorsa, `cell.getDateTime()` bir `CellsException` fırlatır. Bunu basit bir kontrolle önleyin:

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### Zaman Bileşeni

Örnek sadece bir tarih içeriyor, ancak Excel dosyanızda zaman da varsa (ör. “令和3年5月10日 14:30”), Aspose.Cells zaman kısmını da korur. Aldığınız `LocalDateTime` saat, dakika ve saniyeleri içerir.

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, kopyala‑yapıştır‑hazır tam program aşağıdadır:

```java
import com.aspose.cells.*;
import java.time.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Insert Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日");

        // Enable era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);

        // Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime();
        LocalDateTime dateTime = javaDate.toInstant()
                                         .atZone(ZoneId.systemDefault())
                                         .toLocalDateTime();

        // Output the Gregorian date
        System.out.println(dateTime); // 2021-05-10T00:00
    }
}
```

Bunu `JapaneseEraDateParser.java` olarak kaydedin, `javac` ile derleyin ve `java` ile çalıştırın. Her şey doğru kurulduysa, konsola Gregorian tarih yazdırılacaktır.

## Pro İpuçları & Yaygın Tuzaklar

- **Pro ipucu:** `setParseDateUsingJapaneseEra(true)` **herhangi bir hücre değerini okumadan önce** ayarlayın. Bayrağı bir hücre okunduktan sonra değiştirmek değeri geriye dönük olarak dönüştürmez.
- **Yerel ayarları kontrol edin:** Kütüphane era dizelerini Unicode karakterlerine göre ayrıştırır, bu yüzden Japon yerel ayarını açıkça ayarlamanıza gerek yoktur.
- **Performans notu:** Era ayrıştırmayı etkinleştirmek çok küçük bir ek yük getirir. Sadece birkaç hücre için ihtiyacınız varsa, bayrağı geçici olarak açıp hücreleri okuyabilir, ardından tekrar kapatabilirsiniz.
- **Test:** Aspose’un ücretsiz deneme sürümünü kullanarak birden çok era tarihine sahip gerçek bir Excel dosyasıyla doğrulama yapın. Böylece üretim kodunuzun beklendiği gibi çalıştığından emin olursunuz.

## Sonuç

Java ve Aspose.Cells kullanarak bir Excel çalışma kitabından doğrudan **Japon dönemi tarih** değerlerini **parse** ettiğimizi gösterdik. Era‑aware parsing (dönem‑duyarlı ayrıştırma) sayesinde **Excel hücresinden tarihi okuyabilir** ve **Excel hücresinden datetime çıkarabilirsiniz** temiz, tip‑güvenli bir şekilde. Yaklaşım, modern Japon dönemlerinin tümüyle çalışır, zaman bileşenlerini ele alır ve geçersiz verilerle zarifçe başa çıkar.

Bir sonraki meydan okumaya hazır mısınız? Gregorian ve Japon dönemi tarihlerinin karışık olduğu gerçek bir `.xlsx` dosyasını yüklemeyi deneyin ya da elde ettiğiniz `LocalDateTime`'ı yerel formatınıza uygun dizelere dönüştürün. Ayrıca, dönüştürülmüş tarihleri sadece Gregorian tarihleri anlayan aşağı akış sistemleri için Excel'e geri yazmayı da keşfedebilirsiniz.

Sorularınız mı var ya da tuhaf bir kenar durumuyla mı karşılaştınız? Aşağıya yorum bırakın, mutlu kodlamalar!

## Bir Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayalı olarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımları keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose.Cells Java ile Excel'de 1904 Tarih Sistemini Ustalıkla Kullanma – Etkili Hücre İşlemleri](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Aspose.Cells for Java ile Özelleştirilmiş Tarih Formatları Kullanarak Excel'i PDF'ye Verimli Şekilde Dönüştürme](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells for Java ile Excel'de Hücre Aralıklarını Seçme (2023 Rehberi)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}