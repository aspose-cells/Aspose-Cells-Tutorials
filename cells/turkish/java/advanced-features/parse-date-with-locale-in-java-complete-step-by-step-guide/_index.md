---
category: general
date: 2026-07-03
description: Java’nın java.time API’sini kullanarak yerel ayarlarla tarih ayrıştırma.
  Japon dönemi formatı işleme, yerel tarih dönüşümü ve sağlam java tarih ayrıştırma
  tekniklerini öğrenin.
draft: false
keywords:
- parse date with locale
- java date parsing
- japanese era format
- locale date conversion
- java time API
language: tr
og_description: Java'da java.time API'si kullanarak yerel ayarlarla tarih ayrıştırma.
  Bu kılavuz, Japon dönemi formatı işleme, yerel ayar tarih dönüşümü ve güvenilir
  tarih ayrıştırma için en iyi uygulamaları gösterir.
og_title: Java'da Locale ile Tarih Ayrıştırma – Tam Programlama Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Parse date with locale using Java’s java.time API. Learn Japanese era
    format handling, locale date conversion, and robust java date parsing techniques.
  headline: Parse Date with Locale in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Parse date with locale using Java’s java.time API. Learn Japanese era
    format handling, locale date conversion, and robust java date parsing techniques.
  name: Parse Date with Locale in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Define the Era Date String
    text: First, store the Japanese era string exactly as you receive it (e.g., from
      a CSV file or UI).
  - name: Build a Locale‑Aware Formatter
    text: Java’s **java.time API** lets you tie a `DateTimeFormatter` to a specific
      chronology (calendar system) and `Locale`. For the Japanese era we use `JapaneseChronology`.
  - name: Parse and Convert to Gregorian `LocalDate`
    text: Now we actually parse the string and transform the result into a classic
      `LocalDate` that any Java library can consume.
  - name: What if the input uses a different era symbol?
    text: Japanese eras change roughly every few decades. The formatter automatically
      recognises `M` (Meiji), `T` (Taisho), `S` (Showa), `H` (Heisei), and `R` (Reiwa).
      If you receive an older era not covered by the default `JapaneseChronology`,
      you’ll get a `DateTimeParseException`. In that case, verify the s
  - name: How to support other non‑Gregorian calendars?
    text: 'The pattern is identical; you just swap the chronology and locale. For
      example, Thai Buddhist dates (`BuddhistChronology`) look like this:'
  - name: Can I parse without an era symbol (pure year‑month‑day)?
    text: Yes—simply omit `G` from the pattern and use the default `ISO_LOCAL_DATE`
      formatter. That’s the classic *java date parsing* route for Gregorian strings.
  - name: What about lenient parsing (e.g., missing leading zeros)?
    text: Switch `ResolverStyle.STRICT` to `ResolverStyle.LENIENT`. Be aware that
      lenient mode may silently roll over invalid dates (e.g., `R5/13/40` becomes
      `2024‑02‑09`). For production code, strict mode is usually safer.
  type: HowTo
tags:
- java
- date-time
- localization
title: Java'da Locale ile Tarih Ayrıştırma – Tam Adım Adım Kılavuz
url: /tr/java/advanced-features/parse-date-with-locale-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Yerel Ayar ile Tarih Ayrıştırma Java’da – Tam Adım‑Adım Kılavuz

Java’da **yerel ayar ile tarih ayrıştırma** yapmanız gerektiğinde ama hangi sınıfları kullanacağınızdan emin olmadığınız oldu mu? Tek başınıza değilsiniz—Gregoryen olmayan takvimler veya bölgesel formatlarla uğraşmak gizli bir dili çözmek gibi hissettirebilir. Bu öğreticide gerçek bir örnek üzerinden ilerleyeceğiz: `R5/04/01` gibi bir Japon dönemi dizesini standart bir Gregorian `2023‑04‑01` `Date` nesnesine dönüştürmek. Sonunda, herhangi bir yerel ayara özgü tarih formatı için yeniden kullanılabilir bir deseniniz olacak.

Gerekli importlardan kenar‑durum yönetimine kadar her şeyi ele alacağız ve birkaç ilgili kavramı da ekleyeceğiz—*java date parsing*, *japanese era format*, *locale date conversion* ve modern *java time API*—böylece çözümü kendi projelerinize uyarlayabilirsiniz. Harici kütüphane yok, sadece saf Java 8+.

---

## Bu Öğreticide Neler Kapsanıyor

- Japon dönemi (**Japanese era**) (`Reiwa`) format dizesini ayarlama.
- `DateTimeFormatter`'ı `JapaneseChronology` ve bir `Locale` ile kullanma.
- Ortaya çıkan `JapaneseDate` nesnesini `LocalDate` (Gregoryen) tipine dönüştürme.
- Son ISO‑8601 tarihini yazdırma.
- Desteklenmeyen dönemler veya uyumsuz desenler gibi yaygın tuzaklar.
- Diğer yerel ayarlar için hızlı varyasyonlar (Thai Buddhist, Islamic vb.).

**Önkoşullar**  
JDK 8 veya daha yeni bir sürüm, `java.time` hakkında temel bilgi ve Java kodunu çalıştırmak için bir IDE veya CLI. Hepsi bu—ekstra Maven bağımlılığı yok.

---

## Yerel Ayar ile Tarih Ayrıştırma – Adım‑Adım

Aşağıda çözümü üç doğal adıma bölüyoruz. Her adım, ihtiyacınız olan tam kodu, *neden* önemli olduğuna dair kısa bir açıklamayı ve resmi belgelerde bulamayabileceğiniz bir ipucunu içerir.

### Adım 1: Dönem Tarih Dizesini Tanımlama

İlk olarak, Japon dönem dizesini aldığınız şekilde tam olarak saklayın (ör. bir CSV dosyasından veya UI'dan).

```java
// Step 1: Define a date string using the Japanese era format (Reiwa 5)
String eraDateString = "R5/04/01";
```

> **Neden önemli:**  
> Baştaki `R` *Reiwa*'yı temsil eder, Japonya’nın mevcut dönemi. Dönem işaretçisini görmezden gelirseniz, ayrıştırıcı Gregorian takvimini varsayar ve yanlış bir yıl üretir.

### Adım 2: Yerel Ayar‑Farkındalıklı Biçimlendirici Oluşturma

Java’nın **java.time API**'si bir `DateTimeFormatter`'ı belirli bir kronolojiye (takvim sistemi) ve `Locale`'a bağlamanıza olanak tanır. Japon dönemi için `JapaneseChronology` kullanıyoruz.

```java
import java.time.chrono.JapaneseChronology;
import java.time.format.DateTimeFormatter;
import java.time.format.ResolverStyle;
import java.util.Locale;

// Step 2: Create a formatter that understands the Japanese era pattern
DateTimeFormatter japaneseFormatter = new DateTimeFormatterBuilder()
        .parseCaseInsensitive()
        .appendPattern("Gyy/MM/dd")          // G = era symbol, yy = year-of-era
        .toFormatter(Locale.JAPAN)           // Locale for Japanese symbols
        .withChronology(JapaneseChronology.INSTANCE)
        .withResolverStyle(ResolverStyle.STRICT);
```

**Ana noktalar**  
- `G` dönem metnini ayrıştırır (`R` Reiwa, `H` Heisei vb.).  
- `ResolverStyle.STRICT` ayrıştırıcının `R0/13/32` gibi imkansız tarihleri reddetmesini sağlar.  
- `Locale`'i `Locale.JAPAN` olarak ayarlamak, dönem sembollerinin Japon gelenekleriyle eşleşmesini sağlar.

> **Pro ipucu:** *Birden fazla* dönem formatını (ör. `HEISEI` tam yazımı) desteklemeniz gerekiyorsa, gösterildiği gibi `.parseCaseInsensitive()` ekleyin ve tam adlar için deseni `Guuuu` olarak genişletin.

### Adım 3: Gregorian `LocalDate`'e Ayrıştır ve Dönüştür

Şimdi dizeyi gerçekten ayrıştırıyor ve sonucu herhangi bir Java kütüphanesinin tüketebileceği klasik bir `LocalDate`'e dönüştürüyoruz.

```java
import java.time.LocalDate;
import java.time.chrono.JapaneseDate;

// Step 3: Parse the era string and convert to Gregorian LocalDate
JapaneseDate japaneseDate = JapaneseDate.from(japaneseFormatter.parse(eraDateString));
LocalDate gregorianDate = LocalDate.from(japaneseDate);

// Verify the conversion
System.out.println(gregorianDate);   // Expected output: 2023-04-01
```

**Açıklama**  
`JapaneseDate.from(...)` Japon takvimine bağlı bir tarih nesnesi oluşturur. `LocalDate.from(...)` çağırarak dönem bilgisini kaldırır ve eşdeğer ISO‑8601 tarihini elde ederiz—depolama, karşılaştırma veya API çağrıları için mükemmeldir.

> **Neden dönüştürülür?** Çoğu veritabanı, REST servisi ve üçüncü‑taraf kütüphane Gregorian tarih bekler. Dönüştürmeyi ayrıştırma rutininizin içinde tutmak, ilerideki ince hataları önler.

---

## Tam Çalışan Örnek

Hepsini bir araya getirerek, işte tek bir, çalıştırmaya hazır Java sınıfı. `ParseDateWithLocale.java` dosyasına kopyalayıp yapıştırıp çalıştırabilirsiniz.

```java
import java.time.LocalDate;
import java.time.chrono.JapaneseChronology;
import java.time.chrono.JapaneseDate;
import java.time.format.DateTimeFormatter;
import java.time.format.DateTimeFormatterBuilder;
import java.time.format.ResolverStyle;
import java.util.Locale;

public class ParseDateWithLocale {

    public static void main(String[] args) {
        // --- Step 1: Input ---
        String eraDateString = "R5/04/01";

        // --- Step 2: Formatter ---
        DateTimeFormatter japaneseFormatter = new DateTimeFormatterBuilder()
                .parseCaseInsensitive()
                .appendPattern("Gyy/MM/dd")
                .toFormatter(Locale.JAPAN)
                .withChronology(JapaneseChronology.INSTANCE)
                .withResolverStyle(ResolverStyle.STRICT);

        // --- Step 3: Parse & Convert ---
        JapaneseDate japaneseDate = JapaneseDate.from(japaneseFormatter.parse(eraDateString));
        LocalDate gregorianDate = LocalDate.from(japaneseDate);

        // Output
        System.out.println("Original era string: " + eraDateString);
        System.out.println("Converted Gregorian date: " + gregorianDate);
    }
}
```

**Beklenen konsol çıktısı**

```
Original era string: R5/04/01
Converted Gregorian date: 2023-04-01
```

`javac ParseDateWithLocale.java && java ParseDateWithLocale` komutuyla programı çalıştırın. Yukarıdaki iki satırı görürseniz, **yerel ayar ile tarih ayrıştırma** işlemini başarıyla tamamlamışsınız.

---

## Kenar Durumları ve Yaygın Soruların Ele Alınması

### Girdi farklı bir dönem sembolü kullanırsa ne olur?

Japon dönemleri yaklaşık her birkaç on yılda bir değişir. Biçimlendirici otomatik olarak `M` (Meiji), `T` (Taisho), `S` (Showa), `H` (Heisei) ve `R` (Reiwa) sembollerini tanır. Varsayılan `JapaneseChronology` tarafından kapsanmayan daha eski bir dönem alırsanız, `DateTimeParseException` alırsınız. Bu durumda, kaynak veriyi doğrulayın veya özel bir eşleme sağlayın.

### Diğer Gregoryen olmayan takvimleri nasıl desteklersiniz?

Desen aynı; sadece kronolojiyi ve yerel ayarı değiştirirsiniz. Örneğin, Thai Buddhist tarihleri (`BuddhistChronology`) şöyle görünür:

```java
DateTimeFormatter thaiFormatter = new DateTimeFormatterBuilder()
        .appendPattern("Gyy/MM/dd")
        .toFormatter(new Locale("th", "TH"))
        .withChronology(java.time.chrono.ThaiBuddhistChronology.INSTANCE);
```

### Dönem sembolü olmadan (sadece yıl‑ay‑gün) ayrıştırabilir miyim?

Evet—desenden sadece `G`'yi çıkarın ve varsayılan `ISO_LOCAL_DATE` biçimlendiricisini kullanın. Bu, Gregorian dizeleri için klasik *java date parsing* yoludur.

### Esnek ayrıştırma (ör. baştaki sıfırların eksik olması) ne olur?

`ResolverStyle.STRICT`'ı `ResolverStyle.LENIENT`'a değiştirin. Esnek modun geçersiz tarihleri sessizce kaydırabileceğini unutmayın (ör. `R5/13/40` → `2024‑02‑09`). Üretim kodu için genellikle sıkı mod daha güvenlidir.

---

## Sağlam Yerel Ayar Tarih Dönüşümü için Pro İpuçları

1. **Biçimlendiriciyi önbelleğe alın** – `DateTimeFormatter` oluşturmak nispeten ucuzdur, ancak saniyede binlerce tarih ayrıştırıyorsanız, onu static final bir alanda saklayın.  
2. **Girdi uzunluğunu doğrulayın** – `if (eraDateString.length() != 8)` gibi hızlı bir kontrol gereksiz ayrıştırma istisnalarını önleyebilir.  
3. **Orijinal dizeyi kaydedin** – Yerel ayar sorunlarını ayıklarken, ham girdi genellikle ayrıştırıcıyı bozan görünmez karakterleri (sıfır‑genişli boşluklar) ortaya çıkarır.  
4. **Her dönemi birim‑test edin** – `R`, `H`, `S` vb. için JUnit testleri yazarak gelecekteki Java güncellemelerinin eşlemeyi değiştirmediğini garantileyin.

---

## Sonuç

Modern *java time API*, yerel‑farkındalıklı bir `DateTimeFormatter` ve `JapaneseChronology` kullanarak Java’da **yerel ayar ile tarih ayrıştırma** nasıl yapılır gösterdik. Tam örnek, ham bir Japon dönemi dizesinden temiz bir Gregorian `LocalDate`'e kadar tüm akışı gösterir ve deseni Thai Buddhist veya İslami sistemler gibi diğer takvimler için uyarlama bilgisi sağlar.

Sonraki adımlar? `JapaneseChronology` yerine `ThaiBuddhistChronology` veya `HijrahChronology` kullanarak aynı kod yapısının tamamen farklı kültürel takvimleri nasıl yönettiğini görün. Ayrıca, elde edilen `LocalDate`'i `DateTimeFormatter.ofLocalizedDate(FormatStyle.FULL)` kullanarak yerel ayara özgü bir dizeye biçimlendirmeyi keşfedebilirsiniz.

Zor bir yerel ayar ya da beklenmedik bir ayrıştırma hatası mı var? Aşağıya yorum bırakın, birlikte sorun giderelim. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım‑adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Excel'de Veri Sunumunu Ustalaştırma: Sayı ve Özel Tarih Biçimlendirme Aspose.Cells for Java ile](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Aspose.Cells for Java Kullanarak Özel Tarih Biçimleriyle Excel'i PDF'e Verimli Bir Şekilde Dönüştürme](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Excel'de 1904 Tarih Sistemini Aspose.Cells Java ile Ustalaştırma: Etkili Hücre İşlemleri](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}