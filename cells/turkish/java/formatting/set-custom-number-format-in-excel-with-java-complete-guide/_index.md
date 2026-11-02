---
category: general
date: 2026-06-30
description: Java kullanarak Excel'de özel sayı biçimi ayarlayın. Excel çalışma kitabını
  Java ile nasıl oluşturacağınızı, hücreden tarih‑saat almayı, çalışma kitabı formüllerini
  hesaplamayı ve tarih‑saat değerini çıktısını almayı öğrenin.
draft: false
keywords:
- set custom number format
- get datetime from cell
- create excel workbook java
- calculate workbook formulas
- output datetime value
language: tr
og_description: Java kullanarak Excel'de özel sayı biçimi ayarlayın. Bu kılavuz, Java
  ile Excel çalışma kitabı oluşturmayı, hücreden tarih‑saat değerini almayı, çalışma
  kitabı formüllerini hesaplamayı ve tarih‑saat değerini çıktı olarak vermeyi gösterir.
og_title: Java ile Excel'de Özel Sayı Formatı Ayarlama – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  headline: Set Custom Number Format in Excel with Java – Complete Guide
  type: TechArticle
- description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  name: Set Custom Number Format in Excel with Java – Complete Guide
  steps:
  - name: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
    text: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
  - name: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
    text: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
  - name: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
    text: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DateTime
title: Java ile Excel'de Özel Sayı Formatı Ayarlama – Tam Kılavuz
url: /tr/java/formatting/set-custom-number-format-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Java ile Özel Sayı Biçimi Ayarlama – Tam Kılavuz

Java ile çalışırken bir Excel sayfasında **özel sayı biçimi ayarlama** ihtiyacı hiç duydunuz mu? Tek başınıza değilsiniz. Raporlama motoru oluşturuyor olun ya da sadece Japonya dönemi tarihlerini doğru göstermek istiyor olun, bu püf noktasını öğrenmek size post‑işlemde sayısız saat kazandırır. Bu öğreticide **Excel workbook Java** oluşturan, yerel‑spesifik bir biçim uygulayan, formülleri yeniden hesaplayan ve sonunda **gets DateTime from cell** ile **output datetime value** yapan gerçek bir örnek üzerinden ilerleyeceğiz.

Popüler Aspose.Cells for Java kütüphanesini kullanacağız çünkü sayı biçimlerini ve kültüre duyarlı tarihleri kutudan çıkar çıkmaz yönetiyor. Kılavuzun sonunda, herhangi bir Maven veya Gradle projesine ekleyebileceğiniz, bağımsız ve çalıştırılabilir bir programınız olacak. Belirsiz “belgelere bak” kısayolları yok—sadece sağlam kod ve net açıklamalar.

---

## Öğrenecekleriniz

- Programatik olarak **create Excel workbook Java** nasıl yapılır.
- Japonya dönemi tarihleri için **set custom number format** adımlarını tam olarak öğrenin.
- Değeri çıkarmadan önce **calculate workbook formulas** çağırmanın neden gerekli olduğunu öğrenin.
- **get datetime from cell** ve **output datetime value** nasıl yapılır öğrenin.
- Yaygın tuzaklar (eksik locale, eski formüller) ve hızlı çözümler.

## Önkoşullar

- Makinenizde Java 8 veya daha yeni bir sürüm yüklü.  
- Aspose.Cells for Java 23.11 (veya herhangi bir yeni sürüm).  
- Temel bir IDE veya metin düzenleyici—IntelliJ IDEA, Eclipse, VS Code, neyi tercih ederseniz.  

Henüz projenize Aspose.Cells eklemediyseniz, aşağıdaki Maven snippet'ini `pom.xml` dosyanıza yapıştırın:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.11</version>
</dependency>
```

Gradle kullanıcıları ekleyebilir:

```gradle
implementation 'com.aspose:aspose-cells:23.11'
```

Ortam hazır olduğuna göre, koda dalalım.

---

## Adım 1: Özel Sayı Biçimi Ayarlama – Genel Bakış

Herhangi bir Java kodu yazmadan önce, neyi hedeflediğimizi görselleştirmek faydalı olur. ISO‑8601 dizesi “2020‑04‑01” yerine **“令和2年4月1日”** göstermesi gereken bir Excel hücresi hayal edin. Alttaki değer gerçek bir tarih olarak kalır (bu sayede formüller hâlâ çalışır), ancak *görünüm* Japon dönemi formatını takip eder. Bu, **set custom number format** işleminin tam olarak yaptığı şeydir.

Aşağıda tam kaynak dosyası bulunmaktadır. `src/main/java/SetCustomNumberFormatDemo.java` içine kopyalayıp yapıştırabilirsiniz:

```java
// File: SetCustomNumberFormatDemo.java
import com.aspose.cells.*;

public class SetCustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Create Excel workbook Java – a fresh workbook
        // -------------------------------------------------
        Workbook workbook = new Workbook();               // in‑memory workbook, no file yet

        // -------------------------------------------------
        // 2️⃣ Access the first worksheet
        // -------------------------------------------------
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // -------------------------------------------------
        // 3️⃣ Retrieve cell A1 where we’ll store the date string
        // -------------------------------------------------
        Cell cellA1 = worksheet.getCells().get("A1");

        // -------------------------------------------------
        // 4️⃣ Insert a Japanese era date string (Reiwa 2‑04‑01)
        // -------------------------------------------------
        // Note: Aspose.Cells will treat this as a text value until we recalc.
        cellA1.putValue("R02-04-01");

        // -------------------------------------------------
        // 5️⃣ Apply the custom number format (our primary goal)
        // -------------------------------------------------
        // [$-ja-JP] tells Excel to use the Japanese locale.
        // ggge年m月d日 renders as "令和2年4月1日".
        cellA1.setNumberFormat("[$-ja-JP]ggge年m月d日");

        // -------------------------------------------------
        // 6️⃣ Calculate workbook formulas – crucial step!
        // -------------------------------------------------
        // Without this, the cell remains a plain string and the
        // DateTime conversion below will fail.
        workbook.calculateFormula();

        // -------------------------------------------------
        // 7️⃣ Get DateTime from cell – now the value is a true date
        // -------------------------------------------------
        // The getDateTime() method returns a java.util.Calendar instance.
        java.util.Calendar dt = cellA1.getDateTime();

        // -------------------------------------------------
        // 8️⃣ Output datetime value – see the result in console
        // -------------------------------------------------
        System.out.println("Converted DateTime: " + dt.getTime()); // → Tue Apr 01 00:00:00 UTC 2020
    }
}
```

### Neden Bu Çalışır

- `setNumberFormat` Excel'e alttaki sayısal değeri *nasıl görüntüleyeceğini* söyler. `[$-ja-JP]ggge年m月d日` biçim dizesi anahtardır; `ggg` dönem adını, `e` dönemdeki yılı seçer, ardından ay ve gün sabitleri gelir.
- `calculateFormula` Aspose.Cells'in “R02-04-01” metnini Japon takvimine göre bir tarih olarak yorumlamasını zorlar. Bu adımı atlamak hücreyi düz metin bırakır ve `getDateTime()` bir istisna fırlatır.
- `getDateTime` sonunda *gerçek* `java.util.Calendar` nesnesini çıkarır; bunu manipüle edebilir, biçimlendirebilir veya başka bir yerde saklayabilirsiniz.

## Adım 2: Excel Workbook Java Oluşturma – Daha Derin Bakış

**create Excel workbook Java** yaptığınızda, sadece bellek ayırmıyorsunuz; aynı zamanda varsayılan stiller, bir varsayılan çalışma sayfası ve varsayılan kültür (genellikle sistem locale'i) oluşturuyorsunuz. Farklı bir varsayılan locale gerekirse, bir `LoadOptions` nesnesi geçirebilirsiniz:

```java
LoadOptions opts = new LoadOptions(LoadFormat.XLSX);
opts.setLocale(new java.util.Locale("ja", "JP"));
Workbook workbook = new Workbook(opts);
```

Çoğu senaryo için basit yapıcı yeterlidir, ancak alternatifi bilmek iyidir—özellikle aynı uygulamada birden fazla locale ile çalışıyorsanız.

*Pro ipucu:* Biçimlendirme işlemi bitene kadar çalışma kitabını bellekte tutun. Her değişiklikten sonra diske yazmak gereksiz I/O yükü oluşturur.

## Adım 3: Hücreden DateTime Almak – Sonucu İşlemek

`java.util.Calendar dt = cellA1.getDateTime();` satırı ağır işi yapar. Aspose.Cells arka planda içsel seri numarayı (1899‑12‑31'den itibaren geçen gün sayısı) bir `Calendar` nesnesine dönüştürür. Bu dönüşüm çalışma kitabının locale'ine saygı gösterir, böylece görüntü Japon dönemi kullanıyor olsa da doğru Gregoryen tarihini elde edersiniz.

`java.time.LocalDate` (daha yeni API) ihtiyacınız varsa, şu şekilde dönüştürün:

```java
java.time.LocalDate localDate = dt.toInstant()
        .atZone(java.time.ZoneId.systemDefault())
        .toLocalDate();
System.out.println("LocalDate: " + localDate); // 2020-04-01
```

Bu, **output datetime value** gereksinimini modern kalırken karşılar.

## Adım 4: Çalışma Kitabı Formüllerini Hesaplama – Ne Zaman Önemlidir

Şöyle düşünebilirsiniz: *“Gerçekten `calculateFormula()` çağırmam gerekiyor mu?”* Cevap kesinlikle evet, hücreye baştan yerel bir Java `Date` nesnesi vermediğiniz sürece. Bir metin dizesine **set custom number format** uyguladığınızda, Excel (ve Aspose.Cells) bunu değerlendirme gerektiren bir formül‑gibi ifade olarak görür. Yeniden hesaplama yapılmazsa, `getDateTime()` varsayılan `1900‑01‑00` değerini döndürür veya bir `CellValueException` fırlatır.

Çalışma kitabınız zaten yeni biçimlendirilmiş hücreye referans veren karmaşık formüller içeriyorsa, tüm değişikliklerden sonra `calculateFormula()` *bir kez* çağırın. Tekrarlanan çağrılar maliyetlidir.

## Adım 5: DateTime Değerini Çıktılamak – Sonucu Doğrulama

Demo çalıştırıldığında aşağıdaki gibi bir çıktı verir:

```
Converted DateTime: Tue Apr 01 00:00:00 UTC 2020
```

Bu satır üç şeyi doğrular:

1. **set custom number format** uygulandı (oluşturulan `.xlsx` dosyasını Excel'de açıp “令和2年4月1日” gördüğünüzü görebilirsiniz).
2. **calculate workbook formulas** adımı başarılı oldu, dönem dizesini gerçek bir tarihe dönüştürdü.
3. **get datetime from cell** çağrısı uygun bir `Calendar` döndürdü, ardından bunu **output datetime value** olarak konsola yazdırdık.

Çalışma kitabını bir elektronik tablo programı ile açarsanız, biçimlendirilmiş metni göreceksiniz, ancak alttaki hücre değeri seri numarası `43831` olarak kalır (2020‑04‑01 tarihinin Excel temsili). Bu ikili yapı Excel'i güçlü kılar.

---

## Yaygın Tuzaklar ve Kenar Durumları

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|-------|
| `cellA1.getDateTime()` `CellValueException` hatası verir | Hücre hâlâ bir string çünkü `calculateFormula()` atlandı. | Dönüştürülmesi gereken metin tarihini ayarladıktan sonra her zaman `workbook.calculateFormula()` çağırın. |
| Japon dönemi doğru görüntülenmiyor | Locale kodu eksik veya hatalı. | Biçim dizesinde `[$-ja-JP]` kullanın veya `LoadOptions` ile çalışma kitabı locale'ini ayarlayın. |
| Excel'de format “#VALUE!” gösteriyor | Biçim dizesi hatalı. | Köşeli parantezleri ve karakterleri kontrol edin; dönem yılı için `ggge年m月d日` deseni gereklidir. |
| Zaman bileşeni görünüyor (ör. “00:00:00”) | Kaynak dize zaman içeriyor ya da hücre stili ekliyor. | Kaynak dizeyi kırpın veya formatı `ggge年m月d日;@` olarak ayarlayın. |

---

## Tam Çalışan Örnek – Tek Tıkla Çalıştır

Ekstra yorumlar olmadan tek bir dosya tercih ediyorsanız, işte minimal sürüm:



## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells ile Java'da Excel Çalışma Kitabı Oluşturma: Adım Adım Kılavuz](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Excel'de Veri Sunumunu Ustalıkla Yönetme: Aspose.Cells for Java ile Sayı ve Özel Tarih Biçimlendirme](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Aspose.Cells for Java ile Excel Hücreleri Oluşturma ve Biçimlendirme: Adım Adım Kılavuz](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}