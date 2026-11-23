---
category: general
date: 2026-11-22
description: Java çalışma kitabında yerel ayarı nasıl yapacağınızı, çalışma kitabı
  dilini nasıl değiştireceğinizi ve takvimi Japonca'ya nasıl ayarlayacağınızı net
  kod örnekleriyle öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: tr
lastmod: 2026-11-22
og_description: Java çalışma kitabında yerel ayarı hızlıca nasıl ayarlarsınız. Bu
  öğreticiyi izleyerek çalışma kitabı dilini değiştirin, yerel ayarı Japonca'ya ayarlayın
  ve Japon takvimini yapılandırın.
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: Java çalışma kitabında yerel ayarı nasıl ayarlarsınız – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  headline: How to set locale in a Java workbook using Aspose.Cells
  type: TechArticle
- description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  name: How to set locale in a Java workbook using Aspose.Cells
  steps:
  - name: Run the **FullLocaleExample** class.
    text: Run the **FullLocaleExample** class.
  - name: Open the generated `FullJapaneseLocale.xlsx` in Excel.
    text: Open the generated `FullJapaneseLocale.xlsx` in Excel.
  - name: 'Verify that:'
    text: 'Verify that:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Internationalization
- Workbook
title: Aspose.Cells kullanarak Java çalışma kitabında yerel ayarı nasıl ayarlarsınız
url: /tr/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java çalışma kitabında bölge ayarını (locale) Aspose.Cells kullanarak nasıl ayarlarsınız

Java çalışma kitabında bölge ayarını (locale) ayarlamak, elektronik tablonuzu farklı bölgelere uyarlamanız gerektiğinde yaygın bir gereksinimdir. Bu rehberde, bölge ayarını nasıl belirleyeceğinizi, çalışma kitabı dilini nasıl değiştireceğinizi ve takvimi Japonca'ya nasıl ayarlayacağınızı Aspose.Cells API'si kullanarak öğreneceksiniz.

Bir çalışma kitabını uluslararasılaştırmak yalnızca metni çevirmekle kalmaz; sayı formatlarını, tarih ayrıştırmayı ve varsayılan takvim sistemini de etkiler. Bu öğreticinin sonunda şunları yapabilecek durumdasınız:

* Çalışma kitabının bölge ayarını Japonca (Japonya) olarak yapılandırın – **set locale to japanese**.  
* Çalışma kitabı dilini değiştirin, böylece formüller ve UI dizeleri hedef kültüre uygun olur – **change workbook language**.  
* Takvimi Japon imparatorluk takvimine değiştirin – **how to set calendar**.  

Adımlar, Aspose.Cells for Java'ın (v23.9 veya daha yeni) herhangi bir güncel sürümüyle çalışır ve yalnızca standart bir Java geliştirme ortamı gerektirir.

## Prerequisites

| Requirement | Reason |
|-------------|--------|
| Java 8 ve üzeri | Kütüphane Java 8+ hedeflemektedir. |
| Aspose.Cells for Java (v23.9+) | `Workbook`, `WorkbookSettings` ve bölge yardımcılarını sağlar. |
| IDE (IntelliJ IDEA, Eclipse, veya VS Code) | Örneği derlemek ve çalıştırmak için. |
| Java temel bilgisi | Kod parçacıklarını anlamak için gereklidir. |

Add the Aspose.Cells Maven dependency to your `pom.xml` (or download the JAR manually):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## How to set locale and calendar in a workbook

The first step is to create a workbook instance and obtain its settings object. The settings object exposes the locale and calendar APIs.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import java.util.Locale;
import java.util.Calendar;

public class WorkbookLocaleDemo {
    public static void main(String[] args) {
        // Step 1: Create a new workbook (empty by default)
        Workbook workbook = new Workbook();

        // Step 2: Access the workbook's settings
        WorkbookSettings settings = workbook.getSettings();

        // Step 3: Set the calendar to the Japanese calendar
        // Aspose.Cells uses java.util.Calendar; the Japanese calendar is available via Calendar.JAPANESE
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // Step 4: Set the locale to Japanese (Japan)
        // This influences number formats, date formats, and built‑in function behaviour.
        settings.setLocale(new Locale("ja", "JP"));

        // Optional: Save the workbook to verify the settings
        workbook.save("LocaleDemo.xlsx");
    }
}
```

### Why each line matters

* **`new Workbook()`** – Kaydetmeden önce manipüle edebileceğiniz boş bir çalışma kitabı oluşturur.  
* **`getSettings()`** – Bir `WorkbookSettings` nesnesi döndürür; tüm bölgesel seçenekler burada bulunur.  
* **`setCalendar(...)`** – Varsayılan Gregoryen takvimi Japon imparatorluk takvimiyle değiştirir, tarihlerin nasıl görüntüleneceğini ve ayrıştırılacağını etkiler.  
* **`setLocale(new Locale(\"ja\",\"JP\"))`** – Dil ve bölgesel kuralları (ör. aylar, ondalık ayırıcılar) değiştirir. Bu, çalışma kitabı için **how to set locale** unsurunun özüdür.  

Running the program creates `LocaleDemo.xlsx`. Open it in Excel or LibreOffice and you will see Japanese month names, Japanese Yen currency symbols, and dates formatted according to the Japanese calendar.

## Change workbook language (set locale to Japanese)

If your primary goal is to **change workbook language**, you can focus on the `setLocale` call alone. The following snippet isolates that step:

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**Ne değişir?**  
* Hücre biçimlendirme dizeleri Japoncaya geçer (ör. `#,##0.00` bir yen simgesiyle `#,##0.00` olur).  
* Yerleşik fonksiyon adları (ör. `SUM`) İngilizce kalır çünkü Excel'in fonksiyon bölgesi bağımsızdır, ancak tarih dizeleri ve hata mesajları Japonca kurallara uyar.  

**Ne zaman kullanılır?**  
* Japon izleyicileri için sayıları ve tarihleri gösteren bir elektronik tabloya ihtiyacınız olduğunda, ancak temel takvim Gregorian kalabilir.  
* PDF'ye dışa aktarılan veya yazdırılan raporlar için, görsel dilin hedef pazara uygun olmasını sağlamak.  

## How to set calendar to the Japanese calendar

Sometimes the **how to set calendar** requirement is separate from the locale. For legacy systems that store dates in the Japanese imperial era, you must explicitly set the calendar while optionally keeping the default locale.

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Set only the calendar; keep the default (US) locale
settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

// Verify the calendar by creating a date cell
int row = 0, column = 0;
workbook.getWorksheets().get(0).getCells().putValue(row, column, new java.util.Date());

// Save to see the Japanese era (e.g., "R3/04/01" for Reiwa 3)
workbook.save("JapaneseCalendar.xlsx");
```

**Anahtar noktalar:**

* `Calendar.getInstance(Locale.JAPAN)` Japon dönemi için yapılandırılmış bir `java.util.Calendar` döndürür.  
* Çalışma kitabı artık tarihleri dönem sembolleriyle (Reiwa için R, Heisei için H vb.) görüntüler.  
* Bu ayar sayı biçimlendirmesini veya UI dilini **etkilemez**; her ikisine de ihtiyacınız varsa `setLocale` ile birleştirin.  

## Full end‑to‑end example

Below is a complete, runnable program that demonstrates **how to set locale**, **change workbook language**, and **set the calendar** in one cohesive flow. It also adds a sample cell to illustrate the effect.

```java
import com.aspose.cells.*;
import java.util.*;

public class FullLocaleExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 1️⃣ Set the locale to Japanese (Japan) – changes language & number formats
        settings.setLocale(new Locale("ja", "JP"));

        // 2️⃣ Set the calendar to the Japanese imperial calendar
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // 3️⃣ Add a sample date and number to visualize the changes
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Date cell – will show Japanese era after applying the calendar
        cells.putValue(0, 0, new Date());

        // Number cell – will use Japanese Yen symbol and comma separator
        cells.putValue(1, 0, 1234567.89);

        // Apply a style to the number cell for currency formatting
        Style style = cells.getRows().get(1).getStyle();
        style.setNumber(3); // Built‑in currency format
        cells.getRows().get(1).setStyle(style);

        // Save the workbook
        workbook.save("FullJapaneseLocale.xlsx");
        System.out.println("Workbook created with Japanese locale and calendar.");
    }
}
```

**Beklenen çıktı:**  
Opening `FullJapaneseLocale.xlsx` shows the first cell with a date like `R3/04/01` (Reiwa 3) and the second cell formatted as `¥1,234,567.89`. This confirms that **how to set locale**, **change workbook language**, and **how to set calendar** all work together.

## Common pitfalls and how to avoid them

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| `Locale.CHINA` yerine `new Locale("ja","JP")` kullanmak | `Locale.CHINA` Çince dilini ayarlar, Japonca değil. | Japonca için her zaman `"ja", "JP"` ile `Locale` oluşturun. |
| `setLocale` sonrası `settings.setCalendar(...)` çağırmayı unutmak | Takvim varsayılan olarak Gregorian olur, tarihler yanlış dönemde gösterilir. | Bölge ayarını yaptıktan **sonra** `setCalendar` çağırın veya ikisini birlikte ayarlayın. |
| Ayarları uygulamadan önce çalışma kitabını kaydetmek | Ayarlar bellekteki nesneye uygulanır; erken kaydetmek varsayılan bölgeyi yazar. | `workbook.save()` çağırmadan **önce** tüm bölge/takvim değişikliklerini uygulayın. |
| Eski bir Aspose.Cells sürümü kullanmak | Eski sürümlerde `setCalendar` aşırı yüklemeleri bulunmaz. | v23.9+ sürümüne yükseltin veya bölge desteği için sürüm notlarını kontrol edin. |

## Testing your configuration

1. **FullLocaleExample** sınıfını çalıştırın.  
2. Oluşturulan `FullJapaneseLocale.xlsx` dosyasını Excel'de açın.  
3. Şu öğeleri doğrulayın:  
   * Tarih sütunu Japon dönem sembollerini (`R`, `H` vb.) gösteriyor.  
   * Sayı sütunu Yen simgesi ve virgül ayırıcıları kullanıyor.  
   * Çalışma kitabında hata varsa, yerleşik hata mesajları (ör. `#DIV/0!`) Japonca görünüyor.  

If any of these checks fail, double‑check that the `WorkbookSettings` object you modified is the same instance used when saving.

## Next steps

* **Localize formulas** – While the locale controls formatting, you can also translate custom function names using `FormulaParser`.  
* **Apply locale to existing workbooks** – Load a workbook with `new Workbook

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose Cells Tarih Formatı: Java'da Özel Tarih Formatı Nasıl Ayarlanır](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [Excel Dosyalarında Dil Nasıl Ayarlanır Aspose.Cells .NET ile Çok Dilli Destek İçin](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Aspose.Cells kullanarak C#'ta hücre sayı formatı nasıl ayarlanır ve Japon tarihleri nasıl dönüştürülür](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}