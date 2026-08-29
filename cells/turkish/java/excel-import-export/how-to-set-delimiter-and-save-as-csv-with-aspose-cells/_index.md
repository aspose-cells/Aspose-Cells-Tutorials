---
category: general
date: 2026-08-14
description: Aspose.Cells kullanarak ayırıcıyı ayarlama ve CSV olarak kaydetme, basamak
  sayısını sınırlama, CSV dizelerini dışa aktarma ve Java’da formülleri yeniden hesaplama.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: tr
lastmod: 2026-08-14
og_description: Aspose.Cells ile ayırıcıyı ayarlayıp CSV olarak kaydetme, basamak
  sayısını sınırlama, CSV dizelerini dışa aktarma ve Java’da formülleri yeniden hesaplama.
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: Ayırıcıyı nasıl ayarlayıp CSV olarak kaydedilir – Aspose.Cells kılavuzu
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  headline: How to set delimiter and save as CSV with Aspose.Cells
  type: TechArticle
- description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  name: How to set delimiter and save as CSV with Aspose.Cells
  steps:
  - name: Why this works
    text: "- `CsvSaveOptions.setDelimiter(char)` tells Aspose.Cells which character
      separates fields. By default it’s a comma, but any character (tab `'\t'`, pipe
      `'|'`, etc.) works. - `setSignificantDigits(int)` limits numeric precision,
      satisfying the **how to limit digits** requirement without manually form"
  - name: When to use this
    text: '- Returning CSV from a REST endpoint (`@RestController` in Spring) - Embedding
      CSV data into an email attachment without writing to disk - Performing quick
      sanity checks during unit tests'
  - name: Why recalculate?
    text: '- Formulas may reference external data or volatile functions (`NOW()`,
      `RAND()`) that need fresh values. - Dynamic‑array formulas (e.g., `=SORT(A1:A10)`)
      are evaluated automatically, but calling `calculateFormula()` guarantees consistency
      across all sheets.'
  - name: Verifying the result
    text: 1. Open `output.csv` in a text editor – you should see a semicolon (`;`)
      separating each column. 2. Confirm that numeric columns display at most five
      significant digits. 3. The console output will print the CSV string generated
      in step 4. 4. Open `japan_updated.xlsx` in Excel – any formulas that pre
  type: HowTo
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: Aspose.Cells ile ayırıcıyı ayarlama ve CSV olarak kaydetme
url: /tr/java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ayırıcıyı Ayarlama ve CSV Olarak Kaydetme Aspose.Cells ile

Eğer bir Excel çalışma kitabından veri dışa aktarırken **ayırıcıyı nasıl ayarlayacağınızı** öğrenmeniz gerekiyorsa, bu rehber Java için Aspose.Cells kullanarak eksiksiz, uçtan uca bir çözüm gösterir. CSV ayırıcıyı nasıl yapılandıracağınızı, anlamlı basamak sayısını nasıl sınırlayacağınızı, bir CSV dizesini nasıl dışa aktaracağınızı ve bir çalışma kitabı yüklendikten sonra dinamik‑dizi formüllerini nasıl yenileyeceğinizi öğreneceksiniz.

Bu öğretici, Japon İmparatorluk dönemi gibi özel takvimlerin işlenmesi de dahil olmak üzere, kodu kendi makinenizde çalıştırmak için ihtiyacınız olan her şeyi kapsar. Sonunda, doğru CSV dosyaları oluşturabilecek, sayısal hassasiyeti kontrol edebilecek ve formüllerin güncel olmasını sağlayabileceksiniz.

## Gereksinimler

- Java 17 veya daha yeni bir sürüm (kod JDK 11+ ile de derlenebilir)
- Aspose.Cells for Java 23.9 veya daha yeni sürüm – [Aspose web sitesinden](https://products.aspose.com/cells/java/) indirin
- Maven veya Gradle ile bağımlılık yönetimine temel aşinalık
- Bir IDE (IntelliJ IDEA, Eclipse, VS Code) veya basit bir metin editörü ve komut satırı

> **Pro ipucu:** Aspose.Cells JAR dosyasını sınıf yolunuzda tutmak için ayrı bir `libs` klasörü veya Maven Central kullanın. Aşağıdaki örnekler bir Maven projesi varsayar.

## Adım 1: Maven projesini ayarlama

Aspose.Cells bağımlılığını içeren bir `pom.xml` oluşturun:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>aspose-csv-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.9</version>
            <classifier>jdk17</classifier>
        </dependency>
    </dependencies>
</project>
```

Kütüphaneyi indirmek ve derlemenin başarılı olduğunu doğrulamak için `mvn clean compile` komutunu çalıştırın.

## Adım 2: Ayırıcıyı ayarlama ve CSV olarak kaydetme

Temel amaç, bir Excel çalışma kitabını CSV olarak kaydederken varsayılan virgül ayırıcıyı özel bir karakter (ör. noktalı virgül) ile değiştirmektir. Aspose.Cells bu amaç için `CsvSaveOptions` sağlar.

```java
package com.example;

import com.aspose.cells.*;

public class CsvDelimiterDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook (replace the path with your file)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Configure CSV save options
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        // Primary requirement: set a custom delimiter
        csvOptions.setDelimiter(';');               // <-- how to set delimiter
        // Optional: limit the number of significant digits
        csvOptions.setSignificantDigits(5);         // <-- how to limit digits

        // Save the workbook as CSV using the configured options
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);

        System.out.println("CSV file saved with ';' delimiter and 5‑digit precision.");
    }
}
```

### Neden bu şekilde çalışır

- `CsvSaveOptions.setDelimiter(char)` Aspose.Cells'e alanları hangi karakterin ayırdığını söyler. Varsayılan olarak virgül kullanılır, ancak herhangi bir karakter (sekme `'\t'`, boru `|` vb.) çalışır.
- `setSignificantDigits(int)` sayısal hassasiyeti sınırlar, **nasıl basamak sınırlanır** gereksinimini hücreleri tek tek biçimlendirmeden karşılar.

#### Beklenen çıktı

`output.csv` dosyası aşağıdaki gibi satırlar içerir:

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

Sayısal değerlerin beş anlamlı basamağa yuvarlandığını fark edin (ör. `123.45678` → `123.46`).

## Adım 3: CSV kaydederken basamakları sınırlama

Sayısal biçimlendirme üzerinde daha sıkı kontrol istiyorsanız, `CsvSaveOptions` örneğini kullanarak özel bir sayı biçim dizesi de belirtebilirsiniz.

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` .NET stilindeki desenleri izler; Aspose.Cells buna uyar.
- `setNumberFormat` ile `setSignificantDigits` kombinasyonu, farklı yerel ayarlarda tutarlı yuvarlamalar sağlar.

## Adım 4: Özel ayırıcıyla CSV'yi dize olarak dışa aktarma

Bazen fiziksel bir dosya istemezsiniz; CSV verisini bellekte tutmanız gerekir (ör. bir HTTP yanıtı olarak göndermek). `ExportTableOptions` sınıfı bir aralığı dize olarak dışa aktarmanıza olanak tanır.

```java
// Export a range (rows 0‑9, columns 0‑4) as a CSV string
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setExportAsString(true);   // return a string instead of a file
exportOptions.setDelimiter(',');         // <-- how to set delimiter for export
exportOptions.setIncludeColumnNames(true);

String csvData = workbook.getWorksheets()
                         .get(0)                     // first worksheet
                         .getCells()
                         .exportDataTableAsString(0, 0, 10, 5, exportOptions);

System.out.println("Exported CSV string:");
System.out.println(csvData);
```

### Ne zaman kullanılır

- Bir REST uç noktasından CSV döndürmek (`@RestController` içinde Spring)
- Disk yazmadan bir e‑posta ekine CSV verisi eklemek
- Birim testlerinde hızlı tutarlılık kontrolleri yapmak

## Adım 5: Çalışma kitabı yüklendikten sonra formülleri yeniden hesaplama

Çalışma kitabınızda formüller varsa—özellikle son Excel sürümlerinde tanıtılan **dinamik‑dizi formülleri**—dosya yüklendikten sonra bunları yeniden hesaplamalısınız. Aspose.Cells dinamik‑dizi sonuçlarını otomatik olarak yeniler, ancak normal formüller için `calculateFormula()` çağrısı gerekir.

```java
// Load a workbook that uses the Japanese Emperor calendar (optional step)
LoadOptions loadOptions = new LoadOptions();
loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

// Recalculate all formulas in the workbook
japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

// Save the refreshed workbook (preserves the original calendar)
japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
System.out.println("Formulas recalculated and workbook saved.");
```

### Neden yeniden hesaplamalı?

- Formüller dış veri veya değişken fonksiyonlar (`NOW()`, `RAND()`) referans alıyorsa yeni değerler gerekir.
- Dinamik‑dizi formülleri (ör. `=SORT(A1:A10)`) otomatik değerlendirilir, ancak `calculateFormula()` çağrısı tüm sayfalarda tutarlılığı garanti eder.

## Adım 6: Tam uçtan uca örnek

Aşağıda **ayırıcıyı nasıl ayarlayacağınızı**, **CSV olarak nasıl kaydedeceğinizi**, **basamakları nasıl sınırlayacağınızı**, **CSV dizesini nasıl dışa aktaracağınızı**, **özel takvimli bir çalışma kitabını nasıl yükleyeceğinizi** ve **formülleri nasıl yeniden hesaplayacağınızı** gösteren tek bir sınıf bulunmaktadır. Kod, projenize kopyala‑yapıştır yapmaya hazırdır.

```java
package com.example;

import com.aspose.cells.*;

public class AsposeCsvFullDemo {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // 1. Load an existing workbook
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // -----------------------------------------------------------------
        // 2. Configure CSV save options (delimiter + digit limit)
        // -----------------------------------------------------------------
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        csvOptions.setDelimiter(';');          // <-- how to set delimiter
        csvOptions.setSignificantDigits(5);    // <-- how to limit digits

        // -----------------------------------------------------------------
        // 3. Save the workbook as CSV
        // -----------------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);
        System.out.println("Saved CSV with ';' delimiter.");

        // -----------------------------------------------------------------
        // 4. Export a range as a CSV string (custom delimiter)
        // -----------------------------------------------------------------
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setDelimiter(',');       // <-- how to set delimiter for export
        exportOptions.setIncludeColumnNames(true);

        String csvString = workbook.getWorksheets()
                                   .get(0)
                                   .getCells()
                                   .exportDataTableAsString(0, 0, 10, 5, exportOptions);
        System.out.println("CSV string exported:");
        System.out.println(csvString);

        // -----------------------------------------------------------------
        // 5. Load a workbook that uses the Japanese Emperor calendar
        // -----------------------------------------------------------------
        LoadOptions loadOptions = new LoadOptions();
        loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
        Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

        // -----------------------------------------------------------------
        // 6. Recalculate formulas (including dynamic‑array formulas)
        // -----------------------------------------------------------------
        japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

        // -----------------------------------------------------------------
        // 7. Save the refreshed workbook
        // -----------------------------------------------------------------
        japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
        System.out.println("Japanese workbook refreshed and saved.");
    }
}
```

### Sonucu doğrulama

1. `output.csv` dosyasını bir metin düzenleyicide açın – her sütunun noktalı virgül (`;`) ile ayrıldığını görmelisiniz.
2. Sayısal sütunların en fazla beş anlamlı basamak gösterdiğini doğrulayın.
3. Konsol çıktısı, adım 4'te oluşturulan CSV dizesini yazdıracaktır.
4. `japan_updated.xlsx` dosyasını Excel'de açın – daha önce `#REF!` veya eski değer gösteren formüller artık doğru sonuçları gösterecek.

## Yaygın hatalar ve nasıl önlenir

| Sorun | Neden | Çözüm |
|-------|-------|-----|
| CSV ekstra tırnak gösteriyor | Hücrelerde virgül bulunurken ayırıcı da virgül | `setDelimiter` ile farklı bir ayırıcı (`;` veya `\t`) kullanın |
| Sayılar yanlış yuvarlanıyor | `setSignificantDigits` özel sayı formatından sonra uygulanıyor | `setNumberFormat` **setSignificantDigits**'dan **önce** uygulayın |

## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım‑adım açıklamalı tam çalışan kod örnekleri içerir.

- [How to Load and Save Excel as CSV Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [How to Load a CSV File Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [How to Load CSV Files Using Custom Parsers in Java with Aspose.Cells](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}