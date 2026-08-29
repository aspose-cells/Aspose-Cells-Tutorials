---
category: general
date: 2026-08-17
description: Excel'i TXT'ye aktarırken anlamlı basamakları sınırlayın – basamakları
  nasıl ayarlayacağınızı ve Java'da Excel'i metne nasıl dönüştüreceğinizi tam bir
  Aspose.Cells örneğiyle öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: tr
lastmod: 2026-08-17
og_description: Önemli basamakları sınırlayarak Excel'i TXT'ye dışa aktarın. Bu öğreticide,
  basamakları nasıl ayarlayacağınızı ve Aspose.Cells for Java kullanarak Excel'i metne
  nasıl dönüştüreceğinizi gösterir.
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: Excel'i sınırlı anlamlı basamaklarla TXT'ye dışa aktarma – Java rehberi
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: Java kullanarak sınırlı anlamlı basamaklarla Excel'i TXT'ye nasıl dışa aktarılır
url: /tr/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java kullanarak sınırlı anlamlı basamaklarla Excel'i TXT'ye dışa aktarma

Eğer **Excel'i TXT'ye dışa aktarmak** ve anlamlı basamak sayısını kontrol etmek istiyorsanız, bu kılavuz hazır‑çalıştır çözümünü sunar. Basamakları nasıl ayarlayacağınızı, Excel'i metne nasıl dönüştüreceğinizi ve tek bir yapılandırma değişikliğiyle çıktıyı nasıl düzenli tutacağınızı göreceksiniz.

Örnek, `setSignificantDigits` seçeneğini tanıtan Aspose.Cells for Java 25.10 sürümünü kullanır. Öğreticinin sonunda, ekstra yuvarlama kodu olmadan yalnızca istediğiniz basamakları içeren bir TXT dosyası oluşturabilirsiniz.

## Neler Başaracaksınız

- Programmatically bir çalışma kitabı oluşturun.
- Bir hücreye sayısal bir değer ekleyin.
- Anlamlı basamakları sınırlamak için TXT kaydetme seçeneklerini yapılandırın.
- Çalışma kitabını düz metin dosyası olarak kaydedin.
- `significantDigits` ayarının nasıl çalıştığını ve diğer senaryolara nasıl uyarlanacağını anlayın.

### Önkoşullar

- Java 17 veya daha yeni bir sürüm (kod Java 8 ile de derlenir).
- Aspose.Cells for Java 25.10 veya daha yenisi. JAR'ı [Aspose web sitesinden](https://products.aspose.com/cells/java) indirin ve projenizin sınıf yoluna ekleyin.
- Bir IDE veya basit bir metin editörü ve komut satırı derleme aracı (Maven/Gradle).

## Adım 1: Projeyi kurun ve Aspose.Cells'i içe aktarın

Yeni bir Java projesi oluşturun ve Aspose.Cells JAR'ını derleme yoluna ekleyin. Maven kullanıyorsanız, `pom.xml` dosyasına aşağıdaki bağımlılığı ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Pro ipucu:** En yeni Java çalışma zamanı için `jdk17` sınıflandırıcısını kullanın; bu, uyumluluk uyarısı riskini azaltır.

## Adım 2: Bir çalışma kitabı oluşturun ve bir değer yazın

Çalışma kitabı, bellekte bir Excel dosyasını temsil eder. `putValue` metodunu kullanarak herhangi bir hücreye veri ekleyebilirsiniz.

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

`123.456789` sayısı, TXT dışa aktarımımızın kaynağı olacaktır. Varsayılan olarak Aspose.Cells tüm ondalık basamakları yazar; bu genellikle gürültülü metin dosyalarına yol açar.

## Adım 3: Anlamlı basamakları sınırlamak için TXT kaydetme seçeneklerini yapılandırın

Aspose.Cells, düz‑metin çıktısı üzerinde ince ayar kontrolü sağlamak için `TxtSaveOptions` sunar. `setSignificantDigits` metodu, dışa aktarıcıya sadece ondalık noktadan sonra değil, **toplamda** kaç basamağın tutulacağını söyler.

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

`significantDigits` `4` olarak ayarlandığında, dışa aktarıcı `123.456789` değerini `123.5` olarak yuvarlar. Bu davranış, anlamlı rakamların matematiksel tanımına uyar: ilk dört sıfır olmayan basamak korunur.

### Ayarın “ondalıkları sınırlama”dan farkı

- **limit decimals** (`setDecimalPlaces`) ondalık noktadan *sonra* gelen basamakları, tam sayı kısmına bakılmaksızın kırpar.
- **significant digits** (`setSignificantDigits`) ilk sıfır olmayan basamaktan itibaren basamakları sayar; bu, sayıların büyüklüklerinde değişiklik olduğunda faydalıdır.

Sabitleşmiş bir ondalık basamak sayısına ihtiyacınız varsa, yukarıdaki satırı şu şekilde değiştirin:

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## Adım 4: Çalışma kitabını TXT dosyası olarak kaydedin

Şimdi, yapılandırılmış seçenekleri kullanarak çalışma kitabını diske yazın.

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Programı çalıştırmak, çalışma dizininde `significant_digits.txt` dosyasını oluşturur. Dosya tek bir satır içerir:

```
123.5
```

### Beklenen çıktı

| Hücre | Orijinal değer | Dışa aktarılan (4 anlamlı basamak) |
|------|----------------|-----------------------------------|
| A1   | 123.456789     | 123.5                             |

`setSignificantDigits(4)` değerini `6` yaparsanız, çıktı `123.457` olur. Yuvarlamanın nasıl uyduğunu görmek için farklı değerlerle deney yapın.

## Adım 5: Yaygın varyasyonlar ve kenar durumları

### Tüm bir aralığı dışa aktarma

Birden fazla hücre dışa aktarmak istiyorsanız, kaydetmeden önce aralığı doldurmanız yeterlidir:

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

Aynı `significantDigits` ayarı, dosya boyunca tutarlı hassasiyet sağlamak için her sayısal hücreye uygulanır.

### Bölgeye özgü ondalık ayırıcıları işleme

Aspose.Cells, metin yazarken sistem yerel ayarını dikkate alır. Ondalık ayırıcı olarak nokta (`.`) zorlamak için `TxtSaveOptions` kültürünü ayarlayın:

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

Bu, hedef uygulamanın sadece `.` kabul eden CSV ayrıştırıcıları gibi belirli bir format beklediği durumlarda faydalıdır.

### Mevcut dosyaların üzerine yazma

`save` metodu varsayılan olarak hedef dosyanın üzerine yazar. Kazara veri kaybını önlemek istiyorsanız, önce dosyanın varlığını kontrol edin:

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### Büyük çalışma kitapları ve bellek kullanımı

Çok büyük çalışma sayfalarını dışa aktarırken, çıktıyı akış olarak göndermeyi düşünün:

```java
saveOptions.setEnableMemorySaving(true);
```

Bu seçenek, satırları art arda yazarak yığın tüketimini azaltır.

## Tam çalışan örnek

Aşağıda, hemen kopyalayıp yapıştırıp çalıştırabileceğiniz tam program bulunmaktadır:

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Bu kodu çalıştırmak, aşağıdaki içerikle (sekme‑ayırıcı sütunlar) `significant_digits.txt` dosyasını üretir:

```
123.5	0.001235	98770
```

Her sayı, **4 anlamlı basamak** kuralına uyar; bu, ayarın farklı büyüklüklerde de çalıştığını gösterir.

## Sonuç

Artık **Excel'i TXT'ye dışa aktarmayı** ve anlamlı basamak sayısını kontrol etmeyi biliyorsunuz. `TxtSaveOptions.setSignificantDigits` kullanarak tek bir, sürdürülebilir kod satırıyla **basamakları ayarlamayı**, **ondalıkları sınırlamayı** ve **anlamlı basamakları sınırlamayı** yapabilirsiniz. Bu yaklaşım tek hücreler, tam aralıklar ve büyük çalışma kitapları için aynı şekilde çalışır.

### Sonraki adımlar

- `setDelimiter('\t')` gibi diğer `TxtSaveOptions` özelliklerini keşfederek sütun ayırıcılarını özelleştirin.
- Düz metin yerine virgülle ayrılmış değerler gerekiyorsa dışa aktarıcıyı `CsvSaveOptions` ile birleştirin.
- Bu rutini, yüklenen Excel dosyalarını kabul eden ve anında kırpılmış TXT çıktısı dönen bir web servisine entegre edin.

Farklı basamak limitleri ve yerel ayarlarla denemeler yapmaktan çekinmeyin. Yerleşik seçeneklerin özel bir gereksinimi karşılamadığı bir senaryoyla karşılaşırsanız, oluşturulan TXT dosyasını standart Java I/O araçlarıyla her zaman sonradan işleyebilirsiniz.

Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells for Java Kullanarak Excel'de Metni Sayıya Dönüştürme](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [Aspose.Cells Java ile Excel'i HTML'ye Oluşturma ve Dışa Aktarma | Çalışma Kitabı İşlemleri Kılavuzu](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Aspose.Cells for Java Kullanarak Özel Excel Özelliklerini PDF'ye Dışa Aktarma](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}