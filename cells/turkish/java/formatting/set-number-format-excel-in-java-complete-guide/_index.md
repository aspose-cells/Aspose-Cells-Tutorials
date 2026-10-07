---
category: general
date: 2026-06-18
description: Java kullanarak Excel'de sayı formatını ayarlayın, bilimsel gösterimi
  öğrenin, hücreye değer yazın, anlamlı basamakları belirleyin ve dakikalar içinde
  verileri xlsx olarak dışa aktarın.
draft: false
keywords:
- set number format excel
- scientific notation java
- write value to cell
- set significant digits
- export data to xlsx
language: tr
og_description: Java ile Excel’de sayı formatı ayarlayın. Bilimsel gösterimi Java’da
  nasıl kullanacağınızı öğrenin, hücreye değer yazın, anlamlı basamakları belirleyin
  ve verileri verimli bir şekilde xlsx olarak dışa aktarın.
og_title: Java’da Excel Sayı Formatını Ayarlama – Adım Adım Öğretici
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Set number format Excel using Java and learn scientific notation java,
    write value to cell, set significant digits, and export data to xlsx in minutes.
  headline: Set Number Format Excel in Java – Complete Guide
  type: TechArticle
- description: Set number format Excel using Java and learn scientific notation java,
    write value to cell, set significant digits, and export data to xlsx in minutes.
  name: Set Number Format Excel in Java – Complete Guide
  steps:
  - name: Expected Output
    text: '| A (Formatted) | |---------------| | 1.235E7 |'
  - name: How do I change the number of significant digits?
    text: Just edit the format string. For three digits use `"0.###E0"`; for six digits
      use `"0.######E0"`.
  - name: What if I need a different locale (comma as decimal separator)?
    text: Add a locale‑aware format, e.g., `df.getFormat("0,####E0")`. Excel respects
      the user’s regional settings, so the comma will appear only if the workbook
      is opened on a system that uses it.
  - name: Can I apply the same style to an entire column?
    text: Absolutely. Create the style once (as shown) and then loop through rows,
      applying `cell.setCellStyle(sciStyle)` each time. For large sheets, consider
      using `sheet.setDefaultColumnStyle(columnIndex, sciStyle)` – it’s faster and
      keeps the code tidy.
  - name: What if I’m stuck with an older Java version that doesn’t support `var`?
    text: Replace `var` with the explicit type (`Workbook workbook = new XSSFWorkbook();`).
      The rest of the code stays identical.
  type: HowTo
tags:
- Java
- Excel
- Data Export
title: Java'da Excel Sayı Formatını Ayarlama – Tam Kılavuz
url: /tr/java/formatting/set-number-format-excel-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set Number Format Excel in Java – Complete Guide

Hiç **set number format Excel** i bir Java programından nasıl ayarlayacağınızı merak ettiniz mi? Tek başınıza değilsiniz. Finansal raporlar hazırlıyor ya da sensör loglarını dışa aktarıyorsanız, büyük sayıları *.xlsx* dosyasında düzgün gösterebilmek vazgeçilmez bir beceridir.

Bu öğreticide, uçtan uca bir çözüm üzerinden ilerleyeceğiz: bir çalışma kitabı oluşturma, **scientific notation java** ayarlama, **set significant digits** sınırlama, bir hücreye değer yazma ve sonunda **export data to xlsx** yapma. Sonunda projenize doğrudan ekleyebileceğiniz bağımsız bir kod parçasına sahip olacaksınız.

## What You’ll Learn

- Java’da JExcel‑API (veya Apache POI) ile bir çalışma kitabı başlatma.  
- **set number format excel** i zorlayarak bilimsel gösterim (scientific notation) ayarlamak için gereken tam çağrılar.  
- **write value to cell** yaparken hassasiyeti koruma.  
- Çalışma kitabının ayarlarını **set significant digits** ile özel bir sayıya ayarlama.  
- Dosyayı kaydedip modern bir elektronik tablo uygulamasında açılabilir hâle getirme (**export data to xlsx**).  

Harici servis yok, sihir yok. Sadece saf Java ve birkaç iyi belgelenmiş sınıf.

---

## Prerequisites

- JDK 17 veya daha yeni bir sürüm (kod eski sürümlerde de çalışır, ancak örneklerde kısalık için modern `var` sözdizimi kullanılmıştır).  
- `org.apache.poi:poi-ooxml` bağımlılığını çekmek için Maven ya da Gradle.  
- Java koleksiyonları hakkında temel bilgi – bir `for` döngüsü yazdıysanız yeterli.

---

## Step 1: Add the Apache POI Dependency

Maven kullanıyorsanız, aşağıdakini `pom.xml` dosyanıza ekleyin. Gradle kullanıcıları bunu `implementation` sözdizimine dönüştürebilir.

```xml
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

> **Pro tip:** POI’yi güncel tutun. 5.x serisi, sayı formatları ve büyük çalışma sayfaları için daha iyi destek ekliyor.

---

## Step 2: Create a Workbook and Access Its Settings  

İlk olarak yeni bir çalışma kitabı nesnesine ihtiyacımız var. Apache POI, JExcel’in `WorkbookSettings` sınıfını sunmaz, ancak daha sonra bir `CellStyle` oluşturarak aynı etkiyi elde edebiliriz.

```java
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import org.apache.poi.ss.usermodel.Workbook;

public class ExcelNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise a new workbook (this is where we "set number format excel")
        Workbook workbook = new XSSFWorkbook();   // XSSFWorkbook -> .xlsx format
        // No explicit WorkbookSettings, we'll configure a CellStyle later
```

Neden **new workbook** ile başlıyoruz? Bunu boş bir tuval gibi düşünün; daha sonra alacağımız her biçimlendirme kararı bu tuval üzerine uygulanacak.

---

## Step 3: Define a CellStyle for Scientific Notation and Significant Digits  

Apache POI, bir veri formatı dizesi oluşturmanıza izin verir. **scientific notation java** i zorlamak ve basamak sayısını sınırlamak için `"0.####E0"` desenini kullanıyoruz – `#` sembolleri, kaç anlamlı basamağın görüneceğini kontrol eder.

```java
import org.apache.poi.ss.usermodel.CellStyle;
import org.apache.poi.ss.usermodel.DataFormat;

// Inside main(), after workbook creation:
DataFormat df = workbook.createDataFormat();
CellStyle sciStyle = workbook.createCellStyle();

// "0.####E0" -> 0 before the decimal, up to 4 significant digits after, exponent part
sciStyle.setDataFormat(df.getFormat("0.####E0"));
```

*Burada ne oluyor?* Format, Excel’e şu komutu veriyor: “Sayıyı bilimsel gösterimde, ancak en fazla dört anlamlı basamakla göster.” Farklı bir hassasiyet isterseniz `#` sembollerini ekleyip çıkarabilirsiniz.

---

## Step 4: Write a Large Number to a Cell  

Şimdi **write value to cell** *A1* hücresine, az önce oluşturduğumuz stil ile yazacağız. `Sheet` ve `Row` nesneleri hafiftir, bu yüzden anlık olarak oluşturulmaları maliyetli değildir.

```java
import org.apache.poi.ss.usermodel.Sheet;
import org.apache.poi.ss.usermodel.Row;
import org.apache.poi.ss.usermodel.Cell;

// Continue inside main():
Sheet sheet = workbook.createSheet("Numbers");

// Row 0 (first row), Cell 0 (column A)
Row row = sheet.createRow(0);
Cell cell = row.createCell(0);
cell.setCellValue(12345678.9);   // The raw value we want to store
cell.setCellStyle(sciStyle);    // Apply our scientific notation style
```

Gördüğünüz gibi sayıyı cast etmeye gerek yok; POI `double` tipini otomatik olarak işler. `sciStyle` i ekleyerek, kullanıcı dosyayı açtığında Excel’in `1.235E7` (dört anlamlı basamağa yuvarlanmış) göstermesini sağlıyoruz; ham 8 haneli dize yerine.

---

## Step 5: Save the Workbook – Export Data to XLSX  

Son adım **export data to xlsx** dir. Çalışma kitabını geçerli dizine bir dosya olarak yazacağız, ancak istediğiniz bir konuma yönlendirebilirsiniz.

```java
import java.io.FileOutputStream;

// Still inside main():
try (FileOutputStream out = new FileOutputStream("sigDigits.xlsx")) {
    workbook.write(out);
}
workbook.close();   // Free resources
System.out.println("Workbook saved as sigDigits.xlsx");
    }
}
```

`sigDigits.xlsx` dosyasına çift tıkladığınızda, **A** sütununda `1.235E7` göreceksiniz – tam istediğimiz gibi.

### Expected Output

| A (Formatted) |
|---------------|
| 1.235E7       |

Dosyayı açıp hücre formatını manuel olarak değiştirirseniz, temel değerin hâlâ `12345678.9` olduğunu fark edeceksiniz. İşte **set number format excel** in büyüsü: Görünüm değişir, veri aynı kalır.

---

## Common Questions & Edge Cases

### How do I change the number of significant digits?

Format dizesini düzenleyin. Üç basamak için `"0.###E0"`; altı basamak için `"0.######E0"` kullanın.

### What if I need a different locale (comma as decimal separator)?

Yerel ayarlı bir format ekleyin, örneğin `df.getFormat("0,####E0")`. Excel, kullanıcının bölgesel ayarlarını dikkate alır; bu yüzden virgül yalnızca o ayarları kullanan bir sistemde görünür.

### Can I apply the same style to an entire column?

Kesinlikle. Stili bir kez oluşturun (yukarıdaki gibi) ve ardından satırları döngüyle gezerek `cell.setCellStyle(sciStyle)` uygulayın. Büyük sayfalarda `sheet.setDefaultColumnStyle(columnIndex, sciStyle)` kullanmak daha hızlı ve kodu temiz tutar.

### What if I’m stuck with an older Java version that doesn’t support `var`?

`var` yerine açık tip kullanın (`Workbook workbook = new XSSFWorkbook();`). Kodun geri kalanı aynı kalır.

---

## Full Working Example (Copy‑Paste Ready)

```java
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import org.apache.poi.ss.usermodel.*;

import java.io.FileOutputStream;

public class ExcelNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (set number format excel)
        Workbook workbook = new XSSFWorkbook();

        // Define a style for scientific notation with 4 significant digits
        DataFormat df = workbook.createDataFormat();
        CellStyle sciStyle = workbook.createCellStyle();
        sciStyle.setDataFormat(df.getFormat("0.####E0")); // set significant digits

        // Access the first worksheet and write a large number into cell A1
        Sheet sheet = workbook.createSheet("Numbers");
        Row row = sheet.createRow(0);
        Cell cell = row.createCell(0);
        cell.setCellValue(12345678.9);   // write value to cell
        cell.setCellStyle(sciStyle);    // apply scientific notation

        // Save the workbook – export data to xlsx
        try (FileOutputStream out = new FileOutputStream("sigDigits.xlsx")) {
            workbook.write(out);
        }
        workbook.close();

        System.out.println("Workbook saved as sigDigits.xlsx");
    }
}
```

Sınıfı çalıştırın, `sigDigits.xlsx` dosyasını açın ve sayının bilimsel gösterimde, tam dört anlamlı basamakla görüntülendiğini görün. İşte Java’da **set number format excel** iş akışının tamamı.

---

## Conclusion

Java’dan **set number format excel** i nasıl ayarlayacağınızı, bir çalışma kitabı oluşturmayı, **set significant digits** i içeren bilimsel gösterim stilini hazırlamayı, **write value to cell** i ve sonunda **export data to xlsx** i kapsayan tüm süreci ele aldık. Yaklaşım hafif, sadece Apache POI kullanıyor ve Java destekleyen her platformda çalışıyor.

İleride şunları deneyebilirsiniz:

- Belirli değerleri vurgulamak için koşullu biçimlendirme ekleme.  
- Farklı sayısal stiller (ör. para birimi vs. bilimsel) ile birden çok sayfa oluşturma.  
- Büyük veri setlerini bellek‑verimli dışa aktarmak için `SXSSFWorkbook` kullanma.

Deneyin, ekibinizde Excel otomasyonu konusunda başvurulacak kişi olun. Sorularınız veya ilginç kullanım senaryolarınız varsa aşağıya yorum bırakın—mutlu kodlamalar! 

*Image illustrating the workflow (alt text: “set number format excel workflow diagram showing Java code, scientific notation, and export to xlsx”)*


## What Should You Learn Next?


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakın ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımları keşfetmeniz için adım‑adım açıklamalı tam çalışan kod örnekleri içerir.

- [How to Set an Active Cell in Excel Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Aspose Cells Java Set Active Cell Excel](/cells/german/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Aspose Cells Java Set Active Cell Excel](/cells/french/java/cell-operations/aspose-cells-java-set-active-cell-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}